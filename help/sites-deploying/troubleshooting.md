---
title: Solución de problemas
seo-title: Solución de problemas
description: Este artículo trata algunos de los problemas de instalación que puede encontrar con AEM.
seo-description: Este artículo trata algunos de los problemas de instalación que puede encontrar con AEM.
uuid: 2ca898c3-b074-4ccd-a383-b92f226e6c14
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 5542de4e-6262-4300-9cf8-0eac79ba4f9a
translation-type: tm+mt
source-git-commit: 9b65f7194dc648ba9a6dbc127bc8d5951f126269
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 1%

---


# Solución de problemas{#troubleshooting}

Esta sección incluye información detallada sobre los registros disponibles para ayudarle a solucionar los problemas y también incluye información sobre algunos de los problemas que podría encontrar con AEM.

## Solución de problemas de rendimiento del autor {#troubleshoot-author-performance}

Analizar el rendimiento lento en la instancia de creación puede resultar bastante complejo. Como primer paso, es necesario averiguar en qué nivel de pila de tecnología disminuye el rendimiento.

El siguiente árbol de decisión proporciona orientación para reducir el cuello de botella.

![chlimage_1-75](assets/chlimage_1-75.png)

## Optimización básica {#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## Configuración de archivos de registro y registros de auditoría {#configuring-log-files-and-audit-logs}

AEM registros detallados que puede que desee configurar para solucionar problemas de instalación. Para obtener más información, consulte la sección [Trabajo con registros de auditoría y archivos de registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files).

## Uso de la opción Verbose {#using-the-verbose-option}

Cuando inicio AEM WCM, puede agregar la opción -v (detallado) a la línea de comandos como en: java -jar cq-wcm-quickstart-&lt;version>.jar -v.

La opción &quot;verbose&quot; muestra algunos de los resultados del registro de inicio rápido en la consola, para que se puedan utilizar en la resolución de problemas.

## Problemas comunes de instalación {#common-installation-issues}

En la siguiente sección se describen algunos problemas de instalación y sus soluciones.

### Al hacer clic en el tarro de inicio rápido no se produce ningún efecto o se abre el archivo jar con otro programa (por ejemplo, archive manager) {#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}

Esto suele indicar un problema con la configuración del entorno de escritorio del sistema operativo para abrir archivos con la extensión .jar. También puede indicar que no tiene Java instalado o que está utilizando una versión no compatible de Java.

Dado que los archivos jar utilizan el formato ZIP omnipresente, algunos de los programas de archivado pueden configurar automáticamente el escritorio para abrir archivos jar como archivos de archivo.

Para solucionar problemas, haga lo siguiente:

* Doble compruebe que tiene al menos Java versión 1.6 instalada.
* Pruebe un menú contextual (generalmente clic con el botón derecho del ratón) en el AEM WCM Quickstart y seleccione &quot;Abrir con....&quot;
* Compruebe si Java o Sun Java están en la lista e intente ejecutar AEM WCM con él. Si tiene varias versiones de Java instaladas, seleccione la admitida.

   Si tiene éxito con este paso y su sistema operativo oferta una opción para utilizar siempre el programa seleccionado para ejecutar los archivos .jar, selecciónelo. A partir de ahora, hacer clic en el doble debería funcionar.

* A veces, la reinstalación de la versión de Java admitida ayuda a restaurar la asociación correcta.
* Siempre puede ejecutar CRX mediante la línea de comandos o las secuencias de comandos de inicio/parada como se describe anteriormente en este documento.

### Mi aplicación que se ejecuta en CRX genera errores de memoria insuficiente {#my-application-running-on-crx-throws-out-of-memory-errors}

>[!NOTE]
>
>Consulte también [Analizar problemas de memoria](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html).


El propio CRX tiene una huella de memoria muy baja. Si la aplicación que se ejecuta dentro de CRX tiene requisitos de memoria mayores o solicita operaciones con gran cantidad de memoria (por ejemplo, transacciones grandes), la instancia de JVM en la que se ejecuta CRX debe iniciarse con la configuración de memoria adecuada.

Utilice las opciones de comando de Java para definir la configuración de memoria de JVM (por ejemplo, java -Xmx512m -jar crx&amp;ast;.jar para establecer el tamaño máximo en 512MB).

Especifique la opción de configuración de memoria al iniciar AEM WCM desde la línea de comandos. Los scripts de inicio/parada de WCM AEM o los scripts personalizados para administrar AEM inicio de WCM también se pueden modificar para definir la configuración de memoria necesaria.

Si ya ha definido su tamaño de pila en 512 MB, puede que desee analizar el problema de la memoria creando un volcado de pila:

Para crear automáticamente un volcado de pila al agotarse la memoria, utilice el siguiente comando:

java -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -jar &amp;ast;.jar

Esto genera un archivo de volcado de pila (**java_...hprof**) siempre que el proceso se quede sin memoria. El proceso puede continuar ejecutándose después de que se generara el volcado de pila. Normalmente, un archivo de volcado de pila es suficiente para analizar el problema.

### La pantalla de bienvenida de AEM no se muestra en el navegador después de hacer doble clic en el inicio rápido de AEM {#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}

En determinadas situaciones, las pantallas de bienvenida de AEM WCM no se muestran automáticamente aunque el repositorio se esté ejecutando correctamente. Esto puede depender de la configuración del sistema operativo, de la configuración del explorador o de factores similares.

El síntoma habitual es que la ventana AEM WCM Quickstart muestra &quot;AEM WCM comenzando, esperando el inicio del servidor....&quot; Si ese mensaje se muestra durante un tiempo relativamente largo, introduzca la URL de AEM WCM en la ventana del explorador de forma manual, utilizando el puerto predeterminado 4502 o el puerto en el que se está ejecutando la instancia: http://localhost:4502/.

Además, los registros pueden revelar el motivo por el que el explorador no se inicia.

A veces, la ventana de inicio rápido de WCM AEM tiene el mensaje &quot;AEM WCM en ejecución en http://localhost:port/&quot; y el navegador no se inicio automáticamente. En este caso, haga clic en la URL en la ventana Inicio rápido de WCM AEM (es un hipervínculo) o introduzca la URL manualmente en el explorador.

Si todo lo demás falla, compruebe los registros para averiguar qué ha pasado.

## Resolución de problemas de instalación con un servidor de aplicaciones {#troubleshooting-installations-with-an-application-server}

### Página no encontrada devuelta al solicitar una página de geometrixx-exterior {#page-not-found-returned-when-requesting-a-geometrixx-outdoor-page}

**Se aplica a WebLogic 10.3.5 y JBoss 5.1**

Cuando una solicitud a la página geometrixx-outdoors/en devuelve un valor 404 (Página no encontrada), puede volver a comprobar que ha establecido la propiedad sling adicional en el archivo sling.properties necesaria para estos servidores de aplicaciones específicos.

Consulte los pasos *Implementar AEM aplicación Web* para obtener más información.

### El tamaño del encabezado de respuesta puede ser bueno de 4 Kb {#response-header-size-can-be-greater-than-kb}

Los errores 502 pueden indicar que el servidor web no puede gestionar el tamaño del encabezado de respuesta HTTP AEM. AEM generar encabezados de respuesta HTTP que incluyen cookies de tamaño bueno superior a 4 Kb. Asegúrese de que el contenedor del servlet esté configurado para que el tamaño máximo del encabezado de respuesta pueda superar los 4 kb.

Por ejemplo, para Tomcat 7.0, el atributo maxHttpHeaderSize de [HTTP Connector](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html) controla las limitaciones del tamaño del encabezado.

## Desinstalación de Adobe Experience Manager {#uninstalling-adobe-experience-manager}

Debido a que AEM instala en un único directorio, no es necesario instalar una utilidad de desinstalación. La desinstalación puede ser tan simple como eliminar todo el directorio de instalación, aunque la forma de desinstalarlo AEM depende de lo que desee lograr y del almacenamiento persistente que utilice.

Si el almacenamiento persistente está incrustado en el directorio de instalación, por ejemplo, en la instalación predeterminada de TarPM, la eliminación de carpetas también elimina datos.

>[!NOTE]
>
>Adobe recomienda encarecidamente que realice una copia de seguridad del repositorio antes de eliminar AEM. Si elimina todo el &lt;cq-installation-directory>, eliminará el repositorio. Para conservar los datos del repositorio antes de eliminarlos, mueva o copie la carpeta &lt;cq-installation-directory>/crx-quickstart/repository antes de eliminar las otras carpetas.

Si la instalación de AEM utiliza almacenamiento externo, por ejemplo, un servidor de base de datos, la eliminación de la carpeta no elimina los datos automáticamente, pero sí elimina la configuración de almacenamiento, lo que dificulta la restauración del contenido de JCR.

### Los archivos JSP no se compilan en JBoss {#jsp-files-are-not-compiled-on-jboss}

Si instala o actualiza archivos JSP al Experience Manager en JBoss y no se compilan los servlets correspondientes, asegúrese de que el compilador JBoss JSP esté correctamente configurado. Para obtener más información, consulte la
[Artículo Problemas de compilación JSP en JBoss](https://helpx.adobe.com/experience-manager/kb/jsps-dont-compile-jboss.html).

### El sitio web no se carga o falla intermitentemente con Java 11 {#the-website-does-not-load-or-fails-intermittently-with-java11}

Existe un problema conocido con AEM 6.5 ejecutándose en Java 11 en el que es posible que el sitio web no se cargue o falle de forma intermitente.

Si esto sucede, siga la siguiente solución:

1. Abra el archivo `sling.properties` en la carpeta `crx-quickstart/conf/`
1. Busque la línea siguiente:

   `org.osgi.framework.bootdelegation=sun.,com.sun.`

1. Sustitúyalo por lo siguiente:

   `org.osgi.framework.bootdelegation=sun.,com.sun.,jdk.internal.reflect,jdk.internal.reflect.*`

1. Reinicie la instancia.