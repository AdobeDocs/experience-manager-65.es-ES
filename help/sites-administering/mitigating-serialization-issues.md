---
title: Mitigación de problemas de serialización en AEM
seo-title: Mitigación de problemas de serialización en AEM
description: Obtenga información sobre cómo mitigar los problemas de serialización en AEM.
seo-description: Obtenga información sobre cómo mitigar los problemas de serialización en AEM.
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
translation-type: tm+mt
source-git-commit: 3cbbad3ce9d93a353f48fc3206df989a8bf1991a
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---


# Mitigación de problemas de serialización en AEM{#mitigating-serialization-issues-in-aem}

## Información general {#overview}

El equipo de AEM en Adobe ha estado trabajando estrechamente con el proyecto de código abierto [NotSoSerial](https://github.com/kantega/notsoserial) para ayudar a mitigar las vulnerabilidades descritas en **CVE-2015-7501**. NotSoSerial tiene licencia bajo la [licencia de Apache 2](https://www.apache.org/licenses/LICENSE-2.0) e incluye código ASM con licencia propia [tipo BSD](https://asm.ow2.org/license.html).

El frasco del agente incluido en este paquete es la distribución modificada de NotSoSerial por parte del Adobe.

NotSoSerial es una solución de nivel Java para un problema de nivel Java y no es AEM específico. Agrega una verificación previa a un intento de deserializar un objeto. Esta comprobación probará un nombre de clase con una lista de permitidos o lista de bloqueados de estilo cortafuegos. Debido al número limitado de clases en la lista de bloqueados predeterminada, es poco probable que esto afecte a los sistemas o el código.

De forma predeterminada, el agente realizará una comprobación de lista de bloqueados con las clases vulnerables conocidas actuales. Esta lista de bloqueados tiene por objeto protegerle de la lista actual de vulnerabilidades que utilizan este tipo de vulnerabilidad.

La lista de bloqueados y la lista de permitidos se pueden configurar siguiendo las instrucciones de la sección [Configuración del agente](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) de este artículo.

El agente está diseñado para ayudar a mitigar las últimas clases vulnerables conocidas. Si el proyecto está deserializando datos que no son de confianza, es posible que siga siendo vulnerable a ataques de denegación de servicio, ataques de memoria insuficiente y explosiones de deserialización futuras desconocidas.

Adobe admite oficialmente Java 6, 7 y 8, pero entendemos que NotSoSerial también admite Java 5.

## Instalación del agente {#installing-the-agent}

>[!NOTE]
>
>Si ya ha instalado la revisión de serialización para AEM 6.1, elimine los comandos de inicio del agente de la línea de ejecución de java.

1. Instale el paquete **com.adobe.cq.cq-serialization-tester**.

1. Vaya a la consola web del paquete en `https://server:port/system/console/bundles`
1. Busque el paquete de serialización y inicio. Esto debe cargar automáticamente el agente NotSoSerial.

## Instalación del agente en servidores de aplicaciones {#installing-the-agent-on-application-servers}

El agente NotSoSerial no se incluye en la distribución estándar de AEM para servidores de aplicaciones. Sin embargo, puede extraerlo de la distribución jar de AEM y utilizarlo con la configuración del servidor de aplicaciones:

1. En primer lugar, descargue el archivo de inicio rápido AEM y extráigalo:

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. Vaya a la ubicación del inicio rápido AEM recién descomprimido y copie la carpeta `crx-quickstart/opt/notsoserial/` en la carpeta `crx-quickstart` de la instalación del servidor de aplicaciones de AEM.

1. Cambie la propiedad de `/opt` al usuario que ejecuta el servidor:

   ```shell
   chown -R opt <user running the server>
   ```

1. Configure y verifique que el agente se haya activado correctamente, como se muestra en las siguientes secciones de este artículo.

## Configuración del agente {#configuring-the-agent}

La configuración predeterminada es adecuada para la mayoría de las instalaciones. Esto incluye una lista de bloqueados de clases vulnerables de ejecución remota conocidas y una lista de permitidos de paquetes donde la deserialización de datos de confianza debería ser relativamente segura.

La configuración del cortafuegos es dinámica y se puede cambiar en cualquier momento:

1. Ir a la consola web en `https://server:port/system/console/configMgr`
1. Buscando y haciendo clic en **Deserialización de la configuración del cortafuegos.**

   >[!NOTE]
   >
   >También puede acceder directamente a la página de configuración accediendo a la dirección URL en:
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


Esta configuración contiene el registro de lista de permitidos, lista de bloqueados y deserialización.

**Permitir listado**

En la sección Permitir listado, son clases o prefijos de paquete que se permitirán para la deserialización. Es importante tener en cuenta que si está deserializando clases propias, deberá agregar las clases o paquetes a esta lista de permitidos.

**Lista de bloques**

En la sección de listado de bloques hay clases que nunca se permiten para la deserialización. El conjunto inicial de estas clases se limita a las clases que se han encontrado vulnerables a ataques de ejecución remota. La lista de bloqueados se aplica antes de permitir entradas enumeradas.

**Registro de diagnóstico**

En la sección para el registro de diagnóstico, puede elegir varias opciones para el registro cuando se esté realizando la deserialización. Solo se han iniciado sesión por primera vez y no se han vuelto a iniciar sesión en usos posteriores.

El valor predeterminado de **class-name-only** le informará de las clases que se están deserializando.

También puede establecer la opción **pila completa**, que registrará una pila Java del primer intento de deserialización para informarle de dónde se está llevando a cabo la deserialización. Esto puede resultar útil para buscar y eliminar la deserialización de su uso.

## Verificación de la Activación del agente {#verifying-the-agent-s-activation}

Puede comprobar la configuración del agente de deserialización navegando hasta la dirección URL en:

* `https://server:port/system/console/healthcheck?tags=deserialization`

Una vez que acceda a la dirección URL, se mostrará una lista de las comprobaciones de estado relacionadas con el agente. Puede determinar si el agente está correctamente activado verificando que se están superando las comprobaciones de estado. Si están fallando, es posible que tenga que cargar el agente manualmente.

Para obtener más información sobre la resolución de problemas con el agente, consulte [Gestión de errores con carga de agente dinámico](#handling-errors-with-dynamic-agent-loading) a continuación.

>[!NOTE]
>
>Si agrega `org.apache.commons.collections.functors` a la lista de permitidos, la comprobación de estado siempre fallará.

## Gestión de errores con carga de agente dinámico {#handling-errors-with-dynamic-agent-loading}

Si se exponen errores en el registro o los pasos de verificación detectan un problema al cargar el agente, es posible que tenga que cargar el agente manualmente. Esto también se recomienda en caso de que utilice un JRE (Java Runtime Entorno) en lugar de un JDK (Java Development Toolkit), ya que las herramientas para la carga dinámica no están disponibles.

Para cargar el agente manualmente, siga las instrucciones siguientes:

1. Modifique los parámetros de inicio de JVM del tarro de CQ, agregando la siguiente opción:

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >Esto requiere también el uso de la opción -nofork CQ/AEM, junto con la configuración de memoria JVM adecuada, ya que el agente no se habilitará en una JVM falsificada.

   >[!NOTE]
   >
   >La distribución de Adobe del tarro del agente NotSoSerial se encuentra en la carpeta `crx-quickstart/opt/notsoserial/` de la instalación de AEM.

1. Detenga y reinicie el JVM;

1. Vuelva a verificar la activación del agente siguiendo los pasos descritos anteriormente en [Verificación de la Activación del agente](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## Otras consideraciones {#other-considerations}

Si está ejecutando un JVM de IBM, consulte la documentación sobre la compatibilidad con la API de conexión de Java en [esta ubicación](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html).
