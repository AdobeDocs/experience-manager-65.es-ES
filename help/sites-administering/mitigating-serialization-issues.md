---
title: Mitigación de problemas de serialización en AEM
seo-title: Mitigating serialization issues in AEM
description: Obtenga información sobre cómo mitigar los problemas de serialización en AEM.
seo-description: Learn how to mitigate serialization issues in AEM.
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
exl-id: 01e9ab67-15e2-4bc4-9b8f-0c84bcd56862
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---

# Mitigación de problemas de serialización en AEM{#mitigating-serialization-issues-in-aem}

## Información general {#overview}

El equipo de AEM en el Adobe ha estado trabajando estrechamente con el proyecto de código abierto [NotSoSerial](https://github.com/kantega/notsoserial) para ayudar a mitigar las vulnerabilidades descritas en **CVE-2015-7501**. NotSoSerial tiene licencia de [Licencia de Apache 2](https://www.apache.org/licenses/LICENSE-2.0) e incluye código ASM con licencia propia [Licencia similar a BSD](https://asm.ow2.org/license.html).

El jar del agente incluido en este paquete es la distribución modificada de NotSoSerial por parte del Adobe.

NotSoSerial es una solución a nivel de Java para un problema a nivel de Java y no es AEM específico. Agrega una comprobación preliminar a un intento de deserializar un objeto. Esta comprobación probará un nombre de clase con una lista de permitidos o lista de bloqueados de estilo firewall. Debido al número limitado de clases en la lista de bloqueados predeterminada, es poco probable que esto afecte a los sistemas o el código.

De forma predeterminada, el agente realizará una comprobación de lista de bloqueados con las clases vulnerables conocidas actualmente. Esta lista de bloqueados está diseñada para protegerle de la lista actual de vulnerabilidades que utilizan este tipo de vulnerabilidad.

La lista de bloqueados y la lista de permitidos se pueden configurar siguiendo las instrucciones de la sección [Configuración del agente](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) de este artículo.

El agente pretende ayudar a mitigar las últimas clases vulnerables conocidas. Si el proyecto está deserializando datos que no son de confianza, puede que siga siendo vulnerable a ataques de denegación de servicio, ataques de memoria insuficiente y explosiones de deserialización futuras desconocidas.

Adobe es compatible oficialmente con Java 6, 7 y 8, pero entendemos que NotSoSerial también admite Java 5.

## Instalación del agente {#installing-the-agent}

>[!NOTE]
>
>Si ha instalado anteriormente la corrección de serialización para AEM 6.1, elimine los comandos de inicio del agente de la línea de ejecución de java.

1. Instale el **com.adobe.cq.cq-serialization-tester** paquete.

1. Vaya a la consola web de paquetes en `https://server:port/system/console/bundles`
1. Busque el paquete de serialización e inícielo. Esto debería cargar automáticamente el agente NotSoSerial de forma dinámica.

## Instalación del agente en servidores de aplicaciones {#installing-the-agent-on-application-servers}

El agente NotSoSerial no está incluido en la distribución estándar de AEM para servidores de aplicaciones. Sin embargo, puede extraerlo de la distribución jar de AEM y utilizarlo con la configuración del servidor de aplicaciones:

1. En primer lugar, descargue el archivo de inicio rápido AEM y extráigalo:

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. Vaya a la ubicación del inicio rápido AEM recién descomprimido y copie el `crx-quickstart/opt/notsoserial/` a la `crx-quickstart` carpeta de la instalación del servidor de aplicaciones de AEM.

1. Cambiar la propiedad de `/opt` al usuario que ejecuta el servidor:

   ```shell
   chown -R opt <user running the server>
   ```

1. Configure y compruebe que el agente se haya activado correctamente, tal y como se muestra en las siguientes secciones de este artículo.

## Configuración del agente {#configuring-the-agent}

La configuración predeterminada es adecuada para la mayoría de las instalaciones. Esto incluye una lista de bloqueados de clases vulnerables de ejecución remota conocidas y una lista de permitidos de paquetes donde la deserialización de datos de confianza debería ser relativamente segura.

La configuración del cortafuegos es dinámica y se puede cambiar en cualquier momento:

1. Ir a la consola web en `https://server:port/system/console/configMgr`
1. Buscando y haciendo clic en **Deserialización de la configuración del cortafuegos.**

   >[!NOTE]
   >
   >También puede llegar a la página de configuración directamente accediendo a la dirección URL en:
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


Esta configuración contiene el registro de lista de permitidos, lista de bloqueados y deserialización.

**Permitir lista**

En la sección de lista de permitidos, son clases o prefijos de paquete que se permitirán para la deserialización. Es importante tener en cuenta que si está deserializando clases propias, necesitará añadir las clases o paquetes a esta lista de permitidos.

**Listado de Bloques**

En la sección de lista de bloques hay clases que nunca se permiten para la deserialización. El conjunto inicial de estas clases se limita a las clases que se han encontrado vulnerables a ataques de ejecución remota. La lista de bloqueados se aplica antes de cualquier entrada permitida en la lista de entradas.

**Registro de diagnóstico**

En la sección para el registro de diagnóstico, puede elegir varias opciones para registrar cuándo se está realizando la deserialización. Solo se inician sesión en el primer uso y no se vuelven a iniciar sesión en usos posteriores.

El valor predeterminado de **class-name-only** le informará de las clases que se están deserializando.

También puede configurar la variable **pila completa** que registrará una pila java del primer intento de deserialización para informarle dónde se está realizando la deserialización. Esto puede resultar útil para encontrar y eliminar la deserialización de su uso.

## Verificación de la activación del agente {#verifying-the-agent-s-activation}

Puede verificar la configuración del agente de deserialización navegando a la dirección URL en:

* `https://server:port/system/console/healthcheck?tags=deserialization`

Una vez que acceda a la dirección URL, se mostrará una lista de comprobaciones de estado relacionadas con el agente. Puede determinar si el agente está correctamente activado comprobando que los controles de estado están pasando. Si están fallando, es posible que tenga que cargar el agente manualmente.

Para obtener más información sobre la resolución de problemas con el agente, consulte [Gestión De Errores Con Carga Dinámica Del Agente](#handling-errors-with-dynamic-agent-loading) más abajo.

>[!NOTE]
>
>Si agrega `org.apache.commons.collections.functors` a la lista de permitidos, la comprobación de estado siempre fallará.

## Gestión de errores con carga de agentes dinámicos {#handling-errors-with-dynamic-agent-loading}

Si se exponen errores en el registro o los pasos de verificación detectan un problema al cargar el agente, es posible que tenga que cargar el agente manualmente. Esto también se recomienda en caso de que esté utilizando un JRE (Java Runtime Environment) en lugar de un JDK (Java Development Toolkit), ya que las herramientas para la carga dinámica no están disponibles.

Para cargar el agente manualmente, siga las siguientes instrucciones:

1. Modifique los parámetros de inicio de JVM del jar CQ, agregando la siguiente opción:

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >Esto requiere utilizar la opción -nofork CQ/AEM, junto con la configuración de memoria JVM adecuada, ya que el agente no se habilitará en una JVM ramificada.

   >[!NOTE]
   >
   >La distribución de Adobe del jar del agente NotSoSerial se encuentra en la `crx-quickstart/opt/notsoserial/` carpeta de la instalación de AEM.

1. Detenga y reinicie la JVM;

1. Vuelva a verificar la activación del agente siguiendo los pasos descritos anteriormente en [Verificación de la activación del agente](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## Otras consideraciones {#other-considerations}

Si está ejecutando una JVM de IBM, consulte la documentación sobre la compatibilidad con la API de conexión de Java en [esta ubicación](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html).
