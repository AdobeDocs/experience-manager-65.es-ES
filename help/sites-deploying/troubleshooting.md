---
title: Solución de problemas de instalación con AEM
description: Este artículo cubre algunos de los problemas de instalación que podría encontrar con AEM.
uuid: 2ca898c3-b074-4ccd-a383-b92f226e6c14
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 5542de4e-6262-4300-9cf8-0eac79ba4f9a
exl-id: 55576729-be9c-412e-92ac-4be90650c6fa
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 0%

---

# Solución de problemas de instalación con AEM{#troubleshooting}

Esta sección incluye información detallada sobre los registros disponibles para ayudarle a solucionar los problemas y también incluye información sobre algunos de los problemas con los que podría encontrar AEM.

## Resolución de problemas del rendimiento del autor {#troubleshoot-author-performance}

Analizar el rendimiento lento en la instancia de creación puede resultar complejo. Como primer paso, es necesario averiguar en qué nivel de pila de tecnología disminuye el rendimiento.

El siguiente árbol de decisión proporciona instrucciones para reducir el cuello de botella.

![chlimage_1-75](assets/chlimage_1-75.png)

## Optimización básica {#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## Configuración de archivos de registro y registros de auditoría {#configuring-log-files-and-audit-logs}

AEM registra registros detallados que puede que desee configurar para solucionar problemas de instalación. Para obtener más información, consulte la [Uso de registros de auditoría y archivos de registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) para obtener más información.

## Uso de la opción Verbose {#using-the-verbose-option}

Al iniciar AEM WCM, puede añadir la opción -v (verbose) a la línea de comandos como en: java -jar cq-wcm-quickstart&lt;version>.jar -v.

La opción &quot;verbose&quot; muestra algunos de los resultados del registro de inicio rápido en la consola, por lo que se pueden utilizar para solucionar problemas.

## Problemas comunes de instalación {#common-installation-issues}

En la siguiente sección se describen algunos problemas de instalación y sus soluciones.

### Hacer doble clic en el jar de inicio rápido no tiene ningún efecto o abre el archivo jar con otro programa (por ejemplo, el administrador de archivos) {#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}

Este problema suele indicar un problema con la forma en que el entorno de escritorio del sistema operativo está configurado para abrir archivos con la extensión .jar. También puede indicar que no tiene Java™ instalado o que está utilizando una versión incompatible de Java™.

Como los archivos jar utilizan el formato ZIP ubicuo, algunos de los programas de archivado pueden configurar automáticamente el escritorio para abrir archivos jar como archivos de archivo.

Para solucionar problemas, haga lo siguiente:

* Compruebe que tiene al menos Java™ versión 1.6 instalada.
* Pruebe un menú contextual (normalmente con el botón derecho del ratón) en el AEM WCM Quickstart y seleccione &quot;Abrir con....&quot;
* Compruebe si Java™ o Sun Java™ están en la lista e intente ejecutar AEM WCM con él. Si tiene varias versiones de Java™ instaladas, seleccione la compatible.

   Si tiene éxito con este paso, y su sistema operativo ofrece la opción de usar siempre el programa seleccionado para ejecutar los archivos .jar, selecciónelo. Hacer doble clic debería funcionar a partir de ahora.

* A veces, la reinstalación de la versión compatible de Java™ ayuda a restaurar la asociación correcta.
* Siempre puede ejecutar CRX utilizando la línea de comandos o los scripts de inicio/parada como se describió anteriormente en este documento.

### Mi aplicación que se ejecuta en CRX arroja errores de memoria insuficiente {#my-application-running-on-crx-throws-out-of-memory-errors}

>[!NOTE]
>
>Consulte también [Analizar problemas de memoria](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=en).


El propio CRX tiene una huella de memoria baja. Si la aplicación que se ejecuta dentro de CRX tiene requisitos de memoria mayores o solicita operaciones con gran cantidad de memoria (por ejemplo, transacciones grandes), la instancia de JVM donde se ejecuta CRX debe iniciarse con la configuración de memoria adecuada.

Utilice las opciones de comando de Java™ para definir la configuración de memoria de JVM (por ejemplo, java -Xmx512m -jar crx&amp;ast;.jar para establecer el tamaño de pila en 512 MB).

Especifique la opción de configuración de memoria al iniciar AEM WCM desde la línea de comandos. Los scripts de inicio/parada de WCM AEM o los scripts personalizados para administrar AEM inicio de WCM también se pueden modificar para definir la configuración de memoria necesaria.

Si ya ha definido su tamaño de pila en 512 MB, es posible que desee analizar el problema de la memoria creando un volcado de memoria:

Para crear automáticamente un volcado de montículos cuando se quede sin memoria, utilice el siguiente comando:

java -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -jar &amp;ast;.jar

Este método genera un archivo de volcado de montículos (**java_...hprof**) siempre que el proceso se quede sin memoria. El proceso puede seguir ejecutándose después de que se haya generado el volcado de montículos. Normalmente, un archivo de volcado de montículos es suficiente para analizar el problema.

### La pantalla de bienvenida de AEM no se muestra en el explorador después de hacer doble clic AEM inicio rápido. {#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}

En determinadas situaciones, las pantallas de bienvenida de WCM AEM no se muestran automáticamente aunque el repositorio en sí se esté ejecutando correctamente. Este problema puede depender de la configuración del sistema operativo, la configuración del explorador o factores similares.

El síntoma habitual es que la ventana AEM WCM Quickstart muestra &quot;AEM WCM iniciándose, esperando el inicio del servidor....&quot; Si ese mensaje se muestra durante un tiempo relativamente largo, introduzca la URL AEM WCM en la ventana del explorador manualmente, utilizando el puerto predeterminado 4502 o el puerto en el que se está ejecutando la instancia: http://localhost:4502/.

Además, los registros pueden revelar el motivo de que el explorador no se inicie.

A veces, la ventana AEM WCM Quickstart tiene el mensaje &quot;AEM WCM se ejecuta en http://localhost:port/&quot; y el explorador no se inicia automáticamente. En este caso, haga clic en la URL de la ventana de inicio rápido de WCM AEM (es un hipervínculo) o introduzca manualmente la URL en el explorador.

Si todo lo demás falla, compruebe los registros para averiguar qué ha pasado.

### El sitio web no se carga o falla intermitentemente con Java™ 11 {#the-website-does-not-load-or-fails-intermittently-with-java11}

Hay un problema conocido con AEM 6.5 que se ejecuta en Java™ 11 en el que es posible que el sitio web no se cargue o falle de forma intermitente.

Si se produce este problema, haga lo siguiente:

1. Abra el `sling.properties` en el `crx-quickstart/conf/` carpeta
1. Busque la línea siguiente:

   `org.osgi.framework.bootdelegation=sun.,com.sun.`

1. Sustitúyalo por el siguiente:

   `org.osgi.framework.bootdelegation=sun.,com.sun.,jdk.internal.reflect,jdk.internal.reflect.*`

1. Reinicie la instancia.

## Solución de problemas de instalación con un servidor de aplicaciones {#troubleshooting-installations-with-an-application-server}

### Página no encontrada devuelta al solicitar una página al aire libre de geometrixx {#page-not-found-returned-when-requesting-a-geometrixx-outdoor-page}

**Se aplica a WebLogic 10.3.5 y JBoss® 5.1**

Cuando una solicitud a la página geometrixx-outdoors/en devuelve un valor 404 (Página no encontrada), puede volver a comprobar que ha establecido la propiedad sling adicional en el archivo sling.properties necesaria para estos servidores de aplicaciones específicos.

Consulte en la *Implementación AEM aplicación web* para obtener más información.

### El tamaño del encabezado de respuesta puede ser bueno a más de 4 KB {#response-header-size-can-be-greater-than-kb}

Los errores 502 pueden indicar que el servidor web no puede gestionar el tamaño del encabezado de respuesta HTTP AEM. AEM generar encabezados de respuesta HTTP que incluyan cookies de tamaño bueno a más de 4 KB. Asegúrese de que el contenedor de servlet esté configurado para que el tamaño máximo del encabezado de respuesta pueda superar los 4 KB.

Por ejemplo, para Tomcat 7.0, el atributo maxHttpHeaderSize de la variable [Conector HTTP](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html) controla las limitaciones del tamaño del encabezado.

## Desinstalación de Adobe Experience Manager {#uninstalling-adobe-experience-manager}

Debido a que AEM instala en un solo directorio, no es necesario desinstalar una utilidad. La desinstalación puede ser tan simple como borrar todo el directorio de instalación, aunque la forma en que desinstale AEM depende de lo que desee conseguir y del almacenamiento persistente que utilice.

Si el almacenamiento persistente está incrustado en el directorio de instalación, por ejemplo, en la instalación predeterminada de TarPM, al eliminar carpetas también se eliminan datos.

>[!NOTE]
>
>Adobe recomienda realizar una copia de seguridad del repositorio antes de eliminar AEM. Si elimina todo el &lt;cq-installation-directory>, también elimina el repositorio. Para conservar los datos del repositorio antes de eliminarlos, moverlos o copiarlos &lt;cq-installation-directory>/crx-quickstart/repository carpeta en otro lugar antes de eliminar las otras carpetas.

Si la instalación de AEM utiliza almacenamiento externo, por ejemplo, un servidor de base de datos, la eliminación de la carpeta no elimina los datos automáticamente, pero sí la configuración de almacenamiento, lo que dificulta la restauración del contenido de JCR.

### Los archivos JSP no están compilados en JBoss® {#jsp-files-are-not-compiled-on-jboss}

Si instala o actualiza archivos JSP al Experience Manager en JBoss® y los servlets correspondientes no están compilados, asegúrese de que el compilador JSP de JBoss® esté configurado correctamente. Para obtener más información, consulte la
[Problemas de compilación de JSP en JBoss®](https://helpx.adobe.com/experience-manager/kb/jsps-dont-compile-jboss.html) artículo.
