---
title: Instalación independiente personalizada
seo-title: Instalación independiente personalizada
description: Obtenga información sobre las opciones disponibles al instalar una instancia de AEM independiente.
seo-description: Obtenga información sobre las opciones disponibles al instalar una instancia de AEM independiente.
content-type: reference
topic-tags: deploying
exl-id: d6484bb7-8123-4f42-96e8-aa441b1093f3
source-git-commit: 3e18eed63d676e22e12483a1ee68e7e0148d8083
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 1%

---

# Instalación independiente personalizada{#custom-standalone-install}

Esta sección describe las opciones disponibles al instalar una instancia de AEM independiente. También puede leer [Elementos de almacenamiento](/help/sites-deploying/storage-elements-in-aem-6.md) para obtener más información sobre cómo elegir el tipo de almacenamiento back-end después de instalar recién AEM 6.

## Cambio del número de puerto cambiando el nombre del archivo {#changing-the-port-number-by-renaming-the-file}

El puerto predeterminado para AEM es 4502. Si ese puerto no está disponible o ya está en uso, Quickstart se configura automáticamente para utilizar el primer número de puerto disponible de la siguiente manera: 4502, 8080, 8081, 8082, 8083, 8084, 8085, 8888, 9362, `<*random*>`.

También puede establecer el número de puerto cambiando el nombre del archivo jar de inicio rápido, de modo que el nombre del archivo incluya el número de puerto; por ejemplo, `cq5-publish-p4503.jar` o `cq5-author-p6754.jar`.

Hay varias reglas que se deben seguir al cambiar el nombre del archivo jar de inicio rápido:

* Cuando cambie el nombre del archivo, debe comenzar por `cq;` como en `cq5-publish-p4503.jar`.

* Se recomienda que *always* anteponga el número de puerto con -p; como en cq5-publish-p4503.jar o cq5-author-p6754.jar.

>[!NOTE]
>
>Esto sirve para garantizar que no tenga que preocuparse por cumplir las reglas utilizadas para extraer el número de puerto:
>
>* el número de puerto debe ser de 4 o 5 dígitos
>* estos dígitos deben aparecer después de un guión
>* si hay otros dígitos en el nombre del archivo, el número de puerto debe añadirse con el prefijo `-p`
>* se ignora el prefijo &quot;cq5&quot; al principio del nombre del archivo

>



>[!NOTE]
>
>También puede cambiar el número de puerto utilizando la opción `-port` en el comando start.

### Consideraciones de Java 11 {#java-considerations}

Si ejecuta Oracle Java 11 (o versiones generales de Java más recientes que 8), será necesario agregar modificadores adicionales a la línea de comandos al iniciar AEM.

* Es necesario agregar los siguientes modificadores - `-add-opens` para evitar mensajes de ADVERTENCIA de acceso a la reflexión relacionados en el `stdout.log`

```shell
--add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

* Además, debe utilizar el conmutador `-XX:+UseParallelGC` para mitigar cualquier posible problema de rendimiento.

A continuación se muestra una muestra de cómo deberían aparecer los parámetros adicionales de JVM al comenzar AEM en Java 11:

```shell
-XX:+UseParallelGC --add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

Finalmente, si está ejecutando una instancia actualizada desde AEM 6.3, asegúrese de que la siguiente propiedad esté configurada como **true** en `sling.properties`:

* `felix.bootdelegation.implicit`

## Ejecutar modos {#run-modes}

**Los** modos de ejecución le permiten ajustar la instancia de AEM para un fin específico; por ejemplo, crear o publicar, probar, desarrollar, intranet, etc. Estos modos también permiten controlar el uso del contenido de muestra. Este contenido de muestra se define antes de que se cree el inicio rápido y puede incluir paquetes, configuraciones, etc. Esto puede resultar especialmente útil para instalaciones preparadas para la producción cuando desea mantener la instalación limpia y sin contenido de muestra. Para obtener más información, consulte:

* [Ejecutar modos](/help/sites-deploying/configure-runmodes.md)

## Adición de un proveedor de instalación de archivos {#adding-a-file-install-provider}

De forma predeterminada, la carpeta `crx-quickstart/install` se observa en busca de archivos.
Esta carpeta no existe, pero simplemente se puede crear durante la ejecución.

Si un paquete, configuración o paquete de contenido se coloca en este directorio, se recoge e instala automáticamente. Si se elimina, se desinstala.
Es otra forma de colocar paquetes, paquetes de contenido o configuraciones en el repositorio.

Esto es especialmente interesante para varios casos de uso:

* Durante el desarrollo, puede ser más fácil colocar algo en el sistema de archivos.
* Si algo sale mal, la consola web y el repositorio no están disponibles. Con esto puede poner paquetes adicionales en este directorio y deben instalarse.
* La carpeta `crx-quickstart/install` se puede crear antes de que se inicie el inicio rápido, y se pueden colocar paquetes adicionales allí.

>[!NOTE]
>
>Consulte también [Cómo instalar los paquetes CRX automáticamente al iniciar el servidor](https://helpx.adobe.com/experience-manager/kb/HowToInstallPackagesUsingRepositoryInstall.html) para ver ejemplos.

## Instalación e inicio de Adobe Experience Manager as a Windows Service {#installing-and-starting-adobe-experience-manager-as-a-windows-service}

>[!NOTE]
>
>Asegúrese de realizar el siguiente procedimiento mientras ha iniciado sesión como administrador o inicie/ejecute estos pasos utilizando la selección del menú contextual **Ejecutar como administrador**.
>
>Iniciar sesión como usuario con privilegios de administrador es **insuficiente**. Si no ha iniciado sesión como administrador al completar estos pasos, recibirá errores de **Acceso denegado**.

Para instalar e iniciar AEM como un servicio de Windows:

1. Abra el archivo crx-quickstart\opt\helpers\instsrv.bat en un editor de texto.
1. Si está configurando un servidor Windows de 64 bits, reemplace todas las instancias de prunsrv con uno de los siguientes comandos, según su sistema operativo:

   * prunsrv_amd64
   * prunsrv_ia64

   Este comando invoca el script apropiado que inicia el daemon de servicio de Windows en Java de 64 bits en lugar de Java de 32 bits.

1. Para evitar que el proceso se ramifique en más de un proceso, aumente el tamaño máximo de pila y los parámetros JVM de PermGen. Busque el comando `set jvm_options` y establezca el valor como se indica a continuación:

   `set jvm_options=-XX:MaxPermSize=256M;-Xmx1792m`

1. Abra el símbolo del sistema, cambie el directorio actual a la carpeta crx-quickstart/opt/helpers de la instalación de AEM e introduzca el siguiente comando para crear el servicio:

   `instsrv.bat cq5`

   Para comprobar que el servicio se ha creado, abra Servicios en el panel de control Herramientas administrativas o escriba `start services.msc` en el símbolo del sistema. El servicio cq5 aparece en la lista.

1. Inicie el servicio haciendo una de las siguientes acciones:

   * En el panel de control de Servicios, haga clic en cq5 y en Inicio.

   ![imagen_1-11](assets/chlimage_1-11.png)

   * En la línea de comandos, escriba net start cq5.

   ![imagen_1-12](assets/chlimage_1-12.png)

1. Windows indica que el servicio se está ejecutando. AEM se inicia y el ejecutable prunsrv aparece en el Administrador de tareas. En el explorador web, vaya a AEM, por ejemplo, `https://localhost:4502` para empezar a usar AEM.

   ![imagen_1-13](assets/chlimage_1-13.png)

>[!NOTE]
>
>Los valores de propiedad del archivo instsrv.bat se utilizan al crear el servicio de Windows. Si edita los valores de las propiedades en instsrv.bat, debe desinstalar y volver a instalar el servicio.

>[!NOTE]
>
>Al instalar AEM como servicio, debe proporcionar la ruta absoluta para el directorio de registros en `com.adobe.xmp.worker.files.ncomm.XMPFilesNComm` desde Configuration Manager.

Para desinstalar el servicio, haga clic en **Stop** en el panel de control **Services** o, en la línea de comandos, vaya a la carpeta y escriba `instsrv.bat -uninstall cq5`. El servicio se elimina de la lista del panel de control **Services** o de la lista de la línea de comandos cuando escribe `net start`.

## Redefinición de la ubicación del directorio de trabajo temporal {#redefining-the-location-of-the-temporary-work-directory}

La ubicación predeterminada de la carpeta temporal de la máquina Java es `/tmp`. AEM utiliza esta carpeta también, por ejemplo, al crear paquetes.

Si desea cambiar la ubicación de la carpeta temporal (por ejemplo, si necesita un directorio con más espacio libre), defina un * `<new-tmp-path>`* añadiendo el parámetro JVM:

`-Djava.io.tmpdir="/<*new-tmp-path*>"`

para:

* la línea de comandos de inicio del servidor
* el parámetro de entorno CQ_JVM_OPTS en el script serverctl o start

## Más opciones disponibles en el archivo de inicio rápido {#further-options-available-from-the-quickstart-file}

En el archivo de ayuda de inicio rápido, que está disponible a través de la opción -help , se describen más opciones y convenciones de cambio de nombre. Para acceder a la ayuda, escriba:

* `java -jar cq5-<*version*>.jar -help`

```shell
Loading quickstart properties: default
Loading quickstart properties: instance
Setting properties from filename '/Users/Desktop/AEM/cq-quickstart-5.6.0.jar'
--------------------------------------------------------------------------------
Adobe Experience Manager Quickstart (build 20130129)
--------------------------------------------------------------------------------
Usage:
 Use these options on the Quickstart command line.
--------------------------------------------------------------------------------

-help (--help,-h)
         Show this help message
-quickstart.server.port (-p,-port) <port>
         Set server port number
-contextpath (-c,-org.apache.felix.http.context_path) <contextpath>
         Set context path
-debug <port>
         Enable Java Debugging on port number; forces forking
-gui
         Show GUI if running on a terminal
-nobrowser (-quickstart.nobrowser)
         Do not open browser at startup
-unpack
         Unpack installation files only, do not start the server (implies
         -verbose)
-v (-verbose)
         Do not redirect stdout/stderr to files and do not close stdin
-nofork
         Do not fork the JVM, even if not running on a console
-fork
         Force forking the JVM if running on a console, using recommended
         default memory settings for the forked JVM.
-forkargs <args> [<args> ...]
         Additional arguments for the forked JVM, defaults to '-Xmx1024m
         -XX:MaxPermSize=256m '.  Use -- to specify values starting with -,
         example: '-forkargs -- -server'
-a (--interface) <interface>
         Optional IP address (interface) to bind to
-pt <string>
         Process type (main/fork) - do not use directly, used when forking a
         process
-r <string> [<string> [<string> [<string> [<string> [<string> [<string> [<string> [<string> [<string>]]]]]]]]]
         Runmode(s) - Use this to define the run mode(s)
-b <string>
         Base folder - defines the path under which the quickstart work folder
         is created
-low-mem-action <string>
         Low memory action - what to do if memory is insufficient at startup
-use-control-port
         Start a control port
-ll <level>
         Define launchpad log level (1 = error...4 = debug)
--------------------------------------------------------------------------------
Quickstart filename options
--------------------------------------------------------------------------------
Usage:
 Rename the jar file, including one of the patterns shown below, to set the
corresponding option. Command-line options have priority on these filename
patterns.
--------------------------------------------------------------------------------

-NNNN
         Include -NNNN.jar or -pNNNN in the renamed jar filename to run on port
         NNNN, for example: quickstart-8085.jar
-nobrowser
         Include -nobrowser in the renamed jar filename to avoid opening the
         browser at startup, example: quickstart-nobrowser-8085.jar
-publish
         Include -publish in the renamed jar filename to run cq5 in "publish"
         mode, example: cq5-publish-7502.jar
--------------------------------------------------------------------------------
The license.properties file
--------------------------------------------------------------------------------
  The license.properties file stores licensing information, created from the
  licensing form displayed on first startup and stored in the folder from where
  Quickstart is run.
--------------------------------------------------------------------------------
Log files
--------------------------------------------------------------------------------
  Once Quickstart has been unpacked and started, log files can be found under
  ./crx-quickstart/logs.
--------------------------------------------------------------------------------
```

## Instalación de AEM en el entorno Amazon EC2 {#installing-aem-in-the-amazon-ec-environment}

Al instalar AEM en una instancia de Amazon Elastic Compute Cloud (EC2), si instala author y publish en la instancia EC2, la instancia de Autor se instala correctamente siguiendo el procedimiento de [Installing Instances of AEM Manager](#installinginstancesofaemmanager); sin embargo, la instancia Publicar se convierte en Autor.

Antes de instalar la instancia de publicación en el entorno EC2, haga lo siguiente:

1. Desempaquete el archivo jar para la instancia Publicar antes de iniciar la instancia por primera vez. Para desempaquetar el archivo, utilice el siguiente comando:

   ```xml
   java -jar quickstart.jar -unpack
   ```

   >[!NOTE]
   >
   >Si cambia el modo **después** de iniciar la instancia por primera vez, no puede cambiar el modo de ejecución.

1. Inicie la instancia ejecutando:

   ```xml
   java -jar quickstart.jar -r publish
   ```

   >[!CAUTION]
   >
   >Asegúrese de ejecutar primero la instancia después de descomprimirla ejecutando el comando anterior. De lo contrario, el relleno quickstart.properties no se generará. Sin este archivo, cualquier actualización AEM futura fallará.

1. En la carpeta **bin**, abra la secuencia de comandos **start** y compruebe la siguiente sección:

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='author'
   fi
   ```

1. Cambie el modo de ejecución a **publish** y guarde el archivo.

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='publish'
   fi
   ```

1. Detenga la instancia y reiníciela ejecutando el script **start**.

## Verificación de la instalación {#verifying-the-installation}

Los siguientes vínculos pueden utilizarse para verificar que su instalación está operativa (todos los ejemplos se basan en que la instancia se está ejecutando en el puerto 8080 del host local, que CRX está instalado en /crx y Launchpad en /):

* `https://localhost:8080/crx/de`
La consola del CRXDE Lite.

* `https://localhost:8080/system/console`
La Consola Web.

## Acciones después de la instalación {#actions-after-installation}

Aunque hay muchas posibilidades de configurar AEM WCM, se deben realizar determinadas acciones o, al menos, revisarlas inmediatamente después de la instalación:

* Consulte la [Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md) para las tareas necesarias para asegurarse de que el sistema sigue siendo seguro.
* Revise la lista de usuarios y grupos predeterminados que están instalados con AEM WCM. Compruebe si desea realizar alguna acción en otras cuentas; consulte [Seguridad y administración de usuarios](/help/sites-administering/security.md) para obtener más información.

## Acceso al CRXDE Lite y a la consola web {#accessing-crxde-lite-and-the-web-console}

Una vez iniciado AEM WCM, también puede acceder a:

* [CRXDE Lite](#accessing-crxde-lite) : se utiliza para acceder y administrar el repositorio
* [Consola web](#accessing-the-web-console) : se utiliza para administrar o configurar los paquetes OSGi (también conocidos como la consola OSGi)

### Acceso al CRXDE Lite {#accessing-crxde-lite}

Para abrir el CRXDE Lite, puede seleccionar **CRXDE Lite** en la pantalla de bienvenida o utilizar el navegador para desplazarse hasta

```
 https://<<i>host</i>>:<<i>port</i>>/crx/de/index.jsp
```

Por ejemplo:
`https://localhost:4502/crx/de/index.jsp`

![installcq_crxdelite](assets/installcq_crxdelite.png)

#### Acceso a la consola web {#accessing-the-web-console}

Para acceder a la consola web de Adobe CQ, puede seleccionar **Consola OSGi** en la pantalla de bienvenida o utilizar el navegador para desplazarse a

```
 https://<host>:<port>/system/console
```

Por ejemplo:
`https://localhost:4502/system/console`
o para la página Paquetes
`https://localhost:4502/system/console/bundles`

![imagen_1-14](assets/chlimage_1-14.png)

Consulte [Configuración de OSGi con la Consola Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) para obtener más información.

## Solución de problemas {#troubleshooting}

Para obtener información sobre cómo tratar los problemas que pueden surgir durante la instalación, consulte:

* [Solución de problemas](/help/sites-deploying/troubleshooting.md)

## Desinstalación de Adobe Experience Manager {#uninstalling-adobe-experience-manager}

Debido a que AEM instala en un solo directorio, no es necesario desinstalar una utilidad. La desinstalación puede ser tan simple como borrar todo el directorio de instalación, aunque la forma en que desinstale AEM depende de lo que desee conseguir y del almacenamiento persistente que utilice.

Si el almacenamiento persistente está incrustado en el directorio de instalación, por ejemplo, en la instalación predeterminada de TarPM, al eliminar carpetas también se eliminan datos.

>[!NOTE]
>
>Adobe recomienda encarecidamente que realice una copia de seguridad del repositorio antes de eliminar AEM. Si elimina todo el &lt;cq-installation-directory>, eliminará el repositorio. Para conservar los datos del repositorio antes de borrar, mover o copiar la carpeta &lt;cq-installation-directory>/crx-quickstart/repository en otro lugar antes de eliminar las otras carpetas.

Si la instalación de AEM utiliza almacenamiento externo, por ejemplo, un servidor de base de datos, la eliminación de la carpeta no elimina los datos automáticamente, pero sí la configuración de almacenamiento, lo que dificulta la restauración del contenido de JCR.
