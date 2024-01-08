---
title: AEM Solución de problemas de instalación con la
description: AEM Este artículo trata algunos de los problemas de instalación con los que podría encontrar problemas de instalación de los que podría tener que lidiar con la.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 55576729-be9c-412e-92ac-4be90650c6fa
source-git-commit: 3adf2b03ac4e227af2b33099c24ec177b8ea7e1b
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# AEM Solución de problemas de instalación con la{#troubleshooting}

AEM Esta sección incluye información detallada sobre los registros disponibles para ayudarle a solucionar problemas, así como información sobre algunos de los problemas que puede encontrar con los.

## Solucionar problemas de rendimiento de autor {#troubleshoot-author-performance}

El análisis de un rendimiento lento en la instancia de creación puede resultar complejo. Como primer paso, es necesario averiguar en qué nivel de la pila de tecnología está disminuyendo el rendimiento.

El siguiente árbol de decisión proporciona instrucciones para reducir el cuello de botella.

![chlimage_1-75](assets/chlimage_1-75.png)

## Optimización básica {#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## Configuración de archivos de registro y registros de auditoría {#configuring-log-files-and-audit-logs}

AEM Registra registros detallados que es posible que desee configurar para solucionar los problemas de instalación. Para obtener más información, consulte [Trabajar con registros de auditoría y archivos de registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) sección.

## Uso de la opción Detallada {#using-the-verbose-option}

AEM Al iniciar WCM, puede agregar la opción -v (detallada) a la línea de comandos como en: java -jar cq-wcm-quickstart-&lt;version>.jar -v.

La opción detallada muestra parte de la salida del registro de inicio rápido en la consola, por lo que se puede utilizar para solucionar problemas.

## Problemas comunes de instalación {#common-installation-issues}

En la siguiente sección se describen algunos problemas de instalación y sus soluciones.

### Al hacer doble clic en Quickstart jar no se producirá ningún efecto o se abrirá el archivo jar con otro programa (por ejemplo, archive manager) {#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}

Este problema normalmente indica un problema con la forma en que el entorno de escritorio de su sistema operativo está configurado para abrir los archivos con la extensión .jar. También puede indicar que no tiene Java™ instalado o que está utilizando una versión incompatible de Java™.

Como los archivos jar utilizan el omnipresente formato ZIP, algunos de los programas de archivado pueden configurar automáticamente el escritorio para abrir archivos jar como archivos de archivado.

Para solucionar problemas, haga lo siguiente:

* Compruebe que tiene al menos Java™ versión 1.6 instalado.
* AEM Pruebe con un menú contextual (normalmente haciendo clic con el botón derecho del ratón) en el Inicio rápido de WCM de la y seleccione &quot;Abrir con&quot;....
* AEM Compruebe si Java™ o Sun Java™ se encuentra en la lista e intente ejecutar WCM de forma independiente con la lista de parámetros de la aplicación. Si tiene instaladas varias versiones de Java™, seleccione la compatible.

  Si lo consigue, y el sistema operativo ofrece la opción de usar siempre el programa seleccionado para ejecutar los archivos .jar, selecciónelo. Hacer doble clic debería funcionar a partir de ahora.

* A veces, la reinstalación de la versión de Java™ admitida ayuda a restaurar la asociación correcta.
* Siempre puede ejecutar CRX mediante la línea de comandos o secuencias de comandos de inicio y detención, tal como se ha descrito anteriormente en este documento.

### Mi aplicación que se ejecuta en CRX genera errores de memoria insuficiente {#my-application-running-on-crx-throws-out-of-memory-errors}

>[!NOTE]
>
>Consulte también [Analizar problemas de memoria](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html).


CRX tiene un espacio de memoria bajo. Si la aplicación que se ejecuta en CRX tiene requisitos de memoria más grandes o solicita operaciones con gran cantidad de memoria (por ejemplo, transacciones grandes), la instancia de JVM donde se ejecuta CRX debe iniciarse con la configuración de memoria adecuada.

Utilice las opciones de comando de Java™ para definir la configuración de memoria de JVM (por ejemplo, java -Xmx512m -jar crx&amp;ast;.jar para establecer el tamaño de la pila en 512 MB).

AEM Especifique la opción de configuración de memoria al iniciar WCM desde la línea de comandos. AEM AEM Los scripts de inicio/parada de WCM de WCM de WCM o los scripts personalizados para administrar el inicio de WCM también se pueden modificar para definir la configuración de memoria necesaria.

Si ya ha definido el tamaño de la pila en 512 MB, puede que desee analizar más el problema de memoria creando un volcado.

Para crear automáticamente un volcado de la pila cuando se agote la memoria, utilice el siguiente comando:

java -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -jar &amp;ast;.jar

Este método genera un archivo de volcado de pila (**java_...hprof**) siempre que el proceso se quede sin memoria. El proceso puede seguir ejecutándose después de que se haya generado el volcado de la pila.

A menudo, se requieren tres archivos de volcado de la pila, recopilados durante un período de tiempo, para analizar el problema:

* Antes de que se produzca un error
* Durante el fallo 1
* Durante el fallo 2
* *Lo ideal es que también sea bueno recopilar información después de resolver el evento*

Se pueden comparar para ver los cambios y cómo los objetos utilizan la memoria.

>[!NOTE]
>
>Si recopila con regularidad dicha información o tiene experiencia en la lectura de volcados de la pila, un archivo de volcado de la pila puede ser suficiente para analizar el problema.

### AEM AEM La pantalla de bienvenida de la pantalla no se muestra en el explorador después de hacer doble clic en el inicio rápido de la aplicación de la {#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}

AEM En determinadas situaciones, las pantallas de bienvenida de WCM no se muestran automáticamente aunque el repositorio en sí se esté ejecutando correctamente. Este problema puede depender de la configuración del sistema operativo, del explorador o de factores similares.

AEM AEM El síntoma habitual es que la ventana Inicio rápido de WCM de la muestra &quot;Inicio rápido de WCM de la, esperando al inicio del servidor&quot;.... AEM Si ese mensaje se muestra durante un tiempo relativamente largo, introduzca manualmente la dirección URL de WCM de la en la ventana del explorador, utilizando el puerto 4502 predeterminado o el puerto en el que se está ejecutando la instancia: http://localhost:4502/.

Además, los registros pueden revelar el motivo por el que el explorador no se inicia.

AEM AEM A veces, la ventana Inicio rápido de WCM de la tiene el mensaje &quot;WCM se ejecuta en http://localhost:port/&quot; y el explorador no se inicia automáticamente. AEM En este caso, haga clic en la dirección URL en la ventana Inicio rápido de WCM de la (es un hipervínculo) o introduzca manualmente la dirección URL en el explorador.

Si todo lo demás falla, consulte los registros para averiguar qué ha sucedido.

### El sitio web no se carga o falla intermitentemente con Java™ 11 {#the-website-does-not-load-or-fails-intermittently-with-java11}

AEM Hay un problema conocido con la ejecución de ™ 6.5 en JavaScript 11 en el que el sitio web podría no cargarse o fallar intermitentemente.

Si se produce este problema, haga lo siguiente:

1. Abra el `sling.properties` en el archivo `crx-quickstart/conf/` carpeta
1. Busque la siguiente línea:

   `org.osgi.framework.bootdelegation=sun.,com.sun.`

1. Sustitúyala por lo siguiente:

   `org.osgi.framework.bootdelegation=sun.,com.sun.,jdk.internal.reflect,jdk.internal.reflect.*`

1. Reinicie la instancia.

## Solución de problemas de instalaciones con un servidor de aplicaciones {#troubleshooting-installations-with-an-application-server}

### Página no encontrada devuelta al solicitar una página de geometrixx-outdoor {#page-not-found-returned-when-requesting-a-geometrixx-outdoor-page}

**Se aplica a WebLogic 10.3.5 y JBoss® 5.1**

Cuando una solicitud a la página geometrixx-outdoors/es devuelve un error 404 (página no encontrada), puede volver a comprobar que ha establecido la propiedad sling adicional en el archivo sling.properties necesario para estos servidores de aplicaciones específicos.

Consulte en la *AEM Implementación de aplicación web* pasos para obtener los detalles.

### El tamaño del encabezado de respuesta puede ser superior a 4 KB {#response-header-size-can-be-greater-than-kb}

AEM Los errores 502 pueden indicar que el servidor web no puede gestionar el tamaño del encabezado de respuesta HTTP de la. AEM Puede generar encabezados de respuesta HTTP que incluyan cookies de tamaño superior a 4 KB. Asegúrese de que el contenedor del servlet esté configurado para que el tamaño máximo del encabezado de respuesta pueda superar los 4 KB.

Por ejemplo, para Tomcat 7.0, el atributo maxHttpHeaderSize del [Conector HTTP](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html) controla las limitaciones en el tamaño del encabezado.

## Desinstalación de Adobe Experience Manager {#uninstalling-adobe-experience-manager}

AEM Debido a que se instala en un único directorio, no es necesario instalar ninguna utilidad de desinstalación. AEM La desinstalación puede ser tan sencilla como eliminar todo el directorio de instalación, aunque la forma de desinstalar depende de lo que desee conseguir y del almacenamiento persistente que utilice.

Si el almacenamiento persistente está incrustado en el directorio de instalación, por ejemplo, en la instalación predeterminada de TarPM, al eliminar carpetas también se eliminan datos.

>[!NOTE]
>
>El Adobe AEM recomienda realizar una copia de seguridad del repositorio antes de eliminar la. Si elimina todo el &lt;cq-installation-directory>, también se elimina el repositorio. Para conservar los datos del repositorio antes de eliminarlos, mueva o copie el &lt;cq-installation-directory>La carpeta /crx-quickstart/repository se encuentra en otro lugar antes de eliminar las demás carpetas.

AEM Si la instalación de la utiliza almacenamiento externo, por ejemplo, un servidor de base de datos, al eliminar la carpeta no se eliminan los datos automáticamente, pero sí la configuración de almacenamiento, lo que dificulta la restauración del contenido JCR.

### Los archivos JSP no se compilan en JBoss® {#jsp-files-are-not-compiled-on-jboss}

Si instala o actualiza archivos JSP en Experience Manager en JBoss® y no se compilan los servlets correspondientes, asegúrese de que el compilador JSP de JBoss® esté configurado correctamente. Para obtener más información, consulte
[Problemas de compilación de JSP en JBoss®](https://helpx.adobe.com/experience-manager/kb/jsps-dont-compile-jboss.html) artículo.
