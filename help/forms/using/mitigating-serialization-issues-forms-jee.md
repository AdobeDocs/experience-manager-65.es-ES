---
title: Mitigación de problemas de serialización en AEM Forms JEE | ADOBE EXPERIENCE MANAGER
description: Obtenga información sobre cómo mitigar los problemas de deserialización de Java en AEM Forms JEE cuando se ejecuta en JDK 8.
solution: Experience Manager, Experience Manager Forms
feature: Security
version: Experience Manager 6.5
type: Documentation
role: Admin
source-git-commit: ec3941675081255879065c3be9d5af77474b2072
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---


# Mitigación de problemas de serialización en AEM Forms JEE {#mitigating-serialization-issues-in-aem-forms-jee}

AEM Forms JEE incluye un cortafuegos de deserialización que añade una comprobación previa antes de cualquier intento de deserialización de un objeto. Esta comprobación compara un nombre de clase con una lista de permitidos, lista de bloqueados o ambas del tipo de cortafuegos, y rechaza las clases que se sabe que se pueden aprovechar mediante ataques de deserialización de Java™. El agente subyacente es la distribución modificada por Adobe del proyecto de código abierto [NotSoSerial](https://github.com/kantega/notsoserial), con licencia de [Apache 2](https://www.apache.org/licenses/LICENSE-2.0).

En instalaciones que ejecutan **JDK 11 o posterior**, esta protección se activa mediante el filtrado de serialización nativo de la plataforma y no requiere pasos manuales. En instalaciones que ejecutan **JDK 8**, el filtrado de serialización nativa no es efectivo, por lo que el agente debe adjuntarse explícitamente a la JVM al inicio. Este artículo describe cómo hacerlo.

>[!NOTE]
>
>Si la comprobación de estado del filtro de deserialización ya informa como activo en su servidor (consulte [Verificación de la activación del agente](#verifying-the-agents-activation)), su servidor de aplicaciones ya está protegido y puede omitir los pasos restantes de este documento.

## Antes de empezar {#before-you-begin}

Confirme la versión de Java™ con la que se ejecuta el servidor de aplicaciones:

```shell
java -version
```

Si la versión del informe es `1.8.x` (JDK 8), se aplican los pasos de este artículo. Si es 11 o posterior, no se requiere ninguna acción manual; compruebe la protección mediante la comprobación de estado descrita en [Verificación de la activación del agente](#verifying-the-agents-activation).

En los pasos siguientes, `<jee-installation-directory>` hace referencia a la raíz de la instalación de AEM Forms JEE.

## Aplicación del agente {#applying-the-agent}

>[!IMPORTANT]
>
>Estos pasos requieren reiniciar el servidor de aplicaciones. Aplíquelas en cada instancia afectada.

1. **Validar el estado actual.** Vaya a la comprobación de estado del filtro de deserialización:

   ```text
   https://<server>:<port>/system/console/healthcheck?tags=deserialization
   ```

   Si la comprobación informa como activa, la instancia ya está protegida y no es necesario realizar más acciones. Si se produce un error, continúe con los siguientes pasos.

1. **Compruebe si el JAR del agente ya está presente.** Buscar `notsoserial.jar` en la siguiente ubicación:

   ```text
   <jee-installation-directory>/crx-quickstart/opt/notsoserial/
   ```

1. **Agregue el JAR si falta.** Descargue [`notsoserial.jar`](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/notsoserial.jar) y cópielo en la carpeta de arriba en cada instancia:

   ```text
   <jee-installation-directory>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >Reemplace este paso por la ubicación de descarga oficial de Adobe para la distribución JEE de Forms del agente antes de publicar.

1. **Actualice los parámetros de inicio de JVM** de su servidor de aplicaciones para adjuntar el agente. Añada la siguiente opción a la línea de ejecución de Java™:

   ```shell
   -javaagent:<jee-installation-directory>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   La ubicación exacta de la línea de ejecución de Java™ depende del servidor de aplicaciones (por ejemplo, JBoss, WebLogic o WebSphere®). Añada la opción a las opciones de JVM utilizadas para iniciar el servidor de aplicaciones JEE de AEM Forms.

1. **Reinicie el servidor JEE** para que el agente se cargue al iniciar JVM.

1. **Volver a validar.** Vuelva a examinar la comprobación de estado:

   ```text
   https://<server>:<port>/system/console/healthcheck?tags=deserialization
   ```

   La comprobación de estado debe informar ahora de que está saludable.

## Verificación de la activación del agente {#verifying-the-agents-activation}

Puede verificar la configuración del agente de deserialización en cualquier momento navegando a la siguiente URL:

```text
https://<server>:<port>/system/console/healthcheck?tags=deserialization
```

Se muestra una lista de las comprobaciones de estado relacionadas con el agente. Si las comprobaciones son correctas, el agente se activa correctamente. Si hay errores en una instancia de JDK 8, el agente no se ha cargado y debe adjuntarlo manualmente siguiendo los pasos de [Aplicación del agente](#applying-the-agent).

## Configuración del agente {#configuring-the-agent}

Los siguientes pasos se aplican si la versión Java™ del servidor de aplicaciones se ejecuta con JDK 8. Puede configurar el agente después de adjuntarlo y cargarlo siguiendo los pasos de [Aplicación del agente](#applying-the-agent).

La configuración predeterminada es adecuada para la mayoría de las instalaciones. Incluye una lista de bloqueados de clases conocidas que se pueden aprovechar de forma remota y una lista de permitidos de paquetes en los que la deserialización de datos de confianza es segura. La lista de bloqueados se aplica antes de las entradas incluidas en la lista de permitidos.

La configuración del cortafuegos es dinámica y se puede cambiar en cualquier momento:

1. Vaya a la consola web en `https://<server>:<port>/system/console/configMgr`.

1. Busque y haga clic en **Configuración del firewall de deserialización**.

Esta configuración contiene las opciones de lista de permitidos, lista de bloqueados y registro de diagnóstico:

* **Permitir listado** - clases o prefijos de paquete permitidos para la deserialización. Si deserializa sus propias clases, agregue aquí las clases o paquetes relevantes.
* **Lista de bloqueados**: clases a las que nunca se permite la deserialización. El conjunto inicial se limita a las clases que se encuentran vulnerables a los ataques de ejecución remota.
* **Registro de diagnósticos**: opciones para registrar cuando se produce la deserialización. El valor predeterminado **solo nombre de clase** indica las clases que se están deserializando. La opción **full-stack** registra una pila Java™ para el primer intento de deserialización, lo que resulta útil para localizar y eliminar la deserialización que no es de confianza en su uso. Estas opciones solo se registran la primera vez que se utilizan.

## Otras consideraciones {#other-considerations}

* El agente está diseñado para mitigar las clases vulnerables conocidas actualmente. Si el proyecto deserializa datos que no son de confianza, es posible que siga expuesto a ataques de denegación de servicio, falta de memoria o desconocidos de deserialización futura.
* Si ejecuta en un JRE (Java™ Runtime Environment) en lugar de en un JDK (Java™ Development Kit), las herramientas necesarias para la carga dinámica del agente no estarán disponibles y el agente deberá adjuntarse manualmente al inicio, tal como se describe en [Aplicación del agente](#applying-the-agent).
* Si está ejecutando una JVM de IBM®, consulte la documentación sobre la compatibilidad con la API de Java™ Attach.
