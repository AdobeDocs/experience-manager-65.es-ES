---
title: AEM Mitigación de problemas de serialización en la
seo-title: Mitigating serialization issues in AEM
description: AEM Obtenga información sobre cómo mitigar los problemas de serialización en la.
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

# AEM Mitigación de problemas de serialización en la{#mitigating-serialization-issues-in-aem}

## Información general {#overview}

AEM El equipo de Adobe de la ha estado trabajando estrechamente con el proyecto de código abierto [NotSoSerial](https://github.com/kantega/notsoserial) para ayudar a mitigar las vulnerabilidades descritas en **CVE-2015-7501**. NotSoSerial tiene licencia bajo el [Licencia de Apache 2](https://www.apache.org/licenses/LICENSE-2.0) e incluye código ASM con licencia propia [Licencia similar a BSD](https://asm.ow2.org/license.html).

El JAR del agente incluido con este paquete es la distribución modificada de NotSoSerial por parte de Adobe.

AEM NotSoSerial es una solución de nivel Java para un problema de nivel Java y no es específica de la aplicación de nivel de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación. Agrega una comprobación preliminar a un intento de deserializar un objeto. Esta comprobación comprobará el nombre de clase con una lista de permitidos o lista de bloqueados de tipo cortafuegos. Debido al número limitado de clases en la lista de bloqueados predeterminada, es poco probable que esto afecte a sus sistemas o código.

De forma predeterminada, el agente realizará una comprobación de lista de bloqueados en relación con las clases vulnerables conocidas actuales. Esta lista de bloqueados pretende protegerle de la lista actual de vulnerabilidades que utilizan este tipo de vulnerabilidad.

La lista de bloqueados y la lista de permitidos se pueden configurar siguiendo las instrucciones de la [Configuración del agente](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) de este artículo.

El agente está diseñado para ayudar a mitigar las últimas clases vulnerables conocidas. Si el proyecto está deserializando datos que no son de confianza, puede seguir siendo vulnerable a ataques de denegación de servicio, ataques de falta de memoria y ataques de deserialización futuros desconocidos.

Adobe es compatible oficialmente con Java 6, 7 y 8, sin embargo, nuestro entendimiento es que NotSoSerial también es compatible con Java 5.

## Instalación del agente {#installing-the-agent}

>[!NOTE]
>
>AEM Si ya ha instalado la revisión de serialización para la versión 6.1 de, elimine los comandos de inicio del agente de la línea de ejecución de java.

1. Instale el **com.adobe.cq.cq-serialization-tester** paquete.

1. Vaya a la consola web del paquete en `https://server:port/system/console/bundles`
1. Busque el paquete de serialización e inícielo. Esto debe cargar automáticamente de forma dinámica el agente NotSoSerial.

## Instalación del agente en servidores de aplicaciones {#installing-the-agent-on-application-servers}

AEM El agente NotSoSerial no se incluye en la distribución estándar de los recursos para servidores de aplicaciones de la red de distribución de la interfaz de usuario de la aplicación de la red de distribución de la red. AEM Sin embargo, puede extraerlo de la distribución jar de la y utilizarlo con la configuración del servidor de aplicaciones:

1. AEM En primer lugar, descargue el archivo de inicio rápido de la y extráigalo:

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. AEM Vaya a la ubicación del inicio rápido de la aplicación recién descomprimida y copie la variable `crx-quickstart/opt/notsoserial/` a la carpeta `crx-quickstart` AEM carpeta de la instalación del servidor de aplicaciones de.

1. Cambiar la propiedad de `/opt` al usuario que ejecuta el servidor:

   ```shell
   chown -R opt <user running the server>
   ```

1. Configure y compruebe que el agente se ha activado correctamente, tal y como se muestra en las siguientes secciones de este artículo.

## Configuración del agente {#configuring-the-agent}

La configuración predeterminada es adecuada para la mayoría de las instalaciones. Esto incluye una lista de bloqueados de clases vulnerables conocidas de ejecución remota y una lista de permitidos de paquetes en los que la deserialización de datos de confianza debería ser relativamente segura.

La configuración del cortafuegos es dinámica y se puede cambiar en cualquier momento mediante:

1. Vaya a la consola web en `https://server:port/system/console/configMgr`
1. Buscar y hacer clic en **Configuración del firewall de deserialización.**

   >[!NOTE]
   >
   >También puede acceder a la página de configuración directamente accediendo a la dirección URL en:
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


Esta configuración contiene los registros de lista de permitidos, lista de bloqueados y deserialización.

**Permitir listado**

En la sección de inclusión en la lista de permitidos, se trata de clases o prefijos de paquete que se permitirán para la deserialización. Es importante tener en cuenta que si está deserializando clases propias, deberá agregar las clases o paquetes a esta lista de permitidos.

**Bloquear lista**

En la sección de la lista de bloques hay clases que nunca se permiten para la deserialización. El conjunto inicial de estas clases se limita a las clases que se han encontrado vulnerables a ataques de ejecución remota. La lista de bloqueados se aplica antes de las entradas de la lista de permitidos.

**Registro de diagnóstico**

En la sección para el registro de diagnóstico, puede elegir varias opciones para registrar cuando se produce la deserialización. Solo se registran la primera vez que se utilizan y no se registran de nuevo en usos posteriores.

El valor predeterminado de **class-name-only** le informará de las clases que se están deserializando.

También puede establecer el **de pila completa** opción que registrará una pila java del primer intento de deserialización para informarle dónde se está realizando la deserialización. Esto puede resultar útil para buscar y eliminar la deserialización de su uso.

## Verificación de la activación del agente {#verifying-the-agent-s-activation}

Puede verificar la configuración del agente de deserialización navegando hasta la URL en:

* `https://server:port/system/console/healthcheck?tags=deserialization`

Una vez que acceda a la dirección URL, se mostrará una lista de comprobaciones de estado relacionadas con el agente. Puede determinar si el agente está correctamente activado comprobando que las comprobaciones de estado son correctas. Si se producen errores, es posible que tenga que cargar el agente manualmente.

Para obtener más información sobre la resolución de problemas con el agente, consulte [Gestión De Errores Con La Carga Del Agente Dinámico](#handling-errors-with-dynamic-agent-loading) más abajo.

>[!NOTE]
>
>Si añade `org.apache.commons.collections.functors` en la lista de permitidos, la comprobación de estado siempre fallará.

## Gestión de errores al cargar el agente dinámico {#handling-errors-with-dynamic-agent-loading}

Si se exponen errores en el registro o los pasos de verificación detectan un problema al cargar el agente, es posible que tenga que cargar el agente manualmente. Esto también se recomienda en caso de que utilice un JRE (Entorno de tiempo de ejecución de Java) en lugar de un JDK (Kit de herramientas de desarrollo de Java), ya que las herramientas para la carga dinámica no están disponibles.

Para cargar el agente manualmente, siga las siguientes instrucciones:

1. Modifique los parámetros de inicio de JVM del JAR de CQ, añadiendo la siguiente opción:

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >AEM Esto también requiere el uso de la opción -nofork CQ/, junto con la configuración de memoria JVM adecuada, ya que el agente no se habilitará en una JVM ramificada.

   >[!NOTE]
   >
   >La distribución de Adobe del JAR del agente NotSoSerial se encuentra en el `crx-quickstart/opt/notsoserial/` AEM carpeta de la instalación de la.

1. Detenga y reinicie JVM;

1. Vuelva a comprobar la activación del agente siguiendo los pasos descritos anteriormente en [Verificación de la activación del agente](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## Otras consideraciones {#other-considerations}

Si está ejecutando una JVM de IBM, consulte la documentación sobre la compatibilidad con la API de Java Attach en [esta ubicación](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html).
