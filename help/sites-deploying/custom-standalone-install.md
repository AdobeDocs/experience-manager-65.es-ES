---
title: Instalación independiente personalizada
seo-title: Instalación independiente personalizada
description: Obtenga información sobre las opciones disponibles al instalar una instancia independiente de AEM.
seo-description: Obtenga información sobre las opciones disponibles al instalar una instancia independiente de AEM.
uuid: 83fc49d8-2c44-4bb2-988a-f29475066efc
contentOwner: Tyler Rushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: deae8ecb-a2ee-4442-97ca-98bfd1b85738
docset: aem65
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1

---


# Instalación independiente personalizada{#custom-standalone-install}

En esta sección se describen las opciones disponibles al instalar una instancia independiente de AEM. También puede leer Elementos [de almacenamiento](/help/sites-deploying/storage-elements-in-aem-6.md) para obtener más información sobre cómo elegir el tipo de almacenamiento back-end después de instalar AEM 6 recientemente.

## Cambio del número de puerto cambiando el nombre del archivo {#changing-the-port-number-by-renaming-the-file}

El puerto predeterminado para AEM es 4502. Si ese puerto no está disponible o ya está en uso, Quickstart se configura automáticamente para utilizar el primer número de puerto disponible de la siguiente manera: 4502, 8080, 8081, 8082, 8083, 8084, 8085, 8888, 9362, `<*random*>`.

También puede configurar el número de puerto cambiando el nombre del archivo jar de inicio rápido, de modo que el nombre del archivo incluya el número de puerto; por ejemplo, `cq5-publish-p4503.jar` o `cq5-author-p6754.jar`.

Hay varias reglas que deben seguirse al cambiar el nombre del archivo jar de inicio rápido:

* Al cambiar el nombre del archivo, éste debe comenzar por `cq;` como en `cq5-publish-p4503.jar`.

* Se recomienda que *siempre* añada el prefijo -p al número de puerto; como en cq5-publish-p4503.jar o cq5-author-p6754.jar.

>[!NOTE]
>
>Esto sirve para garantizar que no tenga que preocuparse por cumplir las reglas utilizadas para extraer el número de puerto:
>
>* el número de puerto debe ser de 4 o 5 dígitos
>* estos dígitos deben aparecer después de un guión
>* si hay otros dígitos en el nombre del archivo, el número de puerto debe tener el prefijo `-p`
>* se omite el prefijo &quot;cq5&quot; al principio del nombre del archivo
>



>[!NOTE]
>
>También puede cambiar el número de puerto utilizando la `-port` opción del comando start.

### Consideraciones de Java 11 {#java-considerations}

Si está ejecutando Oracle Java 11 (o versiones generales de Java más recientes que 8), será necesario agregar modificadores adicionales a la línea de comandos al iniciar AEM.

* Los siguientes - `-add-opens` conmutadores deben agregarse para evitar los mensajes de ADVERTENCIA de acceso a reflexión relacionados en la variable `stdout.log`

```shell
--add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

* Además, debe utilizar el `-XX:+UseParallelGC` conmutador para mitigar cualquier problema de rendimiento potencial.

A continuación se muestra una muestra de cómo deberían verse los parámetros de JVM adicionales al iniciar AEM en Java 11:

```shell
-XX:+UseParallelGC --add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

Por último, si está ejecutando una instancia actualizada desde AEM 6.3, asegúrese de que la siguiente propiedad se establece en **true** en `sling.properties`:

* `felix.bootdelegation.implicit`

## Ejecutar modos {#run-modes}

**Los modos** de ejecución permiten ajustar la instancia de AEM para un fin específico; por ejemplo, crear o publicar, probar, desarrollar, intranet, etc. Estos modos también le permiten controlar el uso del contenido de muestra. Este contenido de muestra se define antes de que se cree el inicio rápido y puede incluir paquetes, configuraciones, etc. Esto puede resultar especialmente útil para instalaciones preparadas para la producción cuando desea mantener la instalación limpia y sin contenido de muestra. Para obtener más información, consulte:

* [Ejecutar modos](/help/sites-deploying/configure-runmodes.md)

## Adición de un proveedor de instalación de archivos {#adding-a-file-install-provider}

De forma predeterminada, la carpeta `crx-quickstart/install` está vigilada en busca de archivos.
Esta carpeta no existe, pero simplemente se puede crear en tiempo de ejecución.

Si se coloca un paquete de contenido, configuración o paquete de paquetes en este directorio, se toma e instala automáticamente. Si se elimina, se desinstala.
Es otra forma de colocar paquetes, paquetes de contenido o configuraciones en el repositorio.

Esto es especialmente interesante para varios casos de uso:

* Durante el desarrollo, podría ser más fácil colocar algo en el sistema de archivos.
* Si algo sale mal, la consola web y el repositorio no están disponibles. Con esto puede poner paquetes adicionales en este directorio y se deben instalar.
* La `crx-quickstart/install` carpeta se puede crear antes de que se inicie el inicio rápido y se pueden colocar paquetes adicionales allí.

>[!NOTE]
>
>Consulte también [Cómo instalar paquetes CRX automáticamente al iniciar](https://helpx.adobe.com/experience-manager/kb/HowToInstallPackagesUsingRepositoryInstall.html) el servidor para ver ejemplos.

## Instalación e inicio de Adobe Experience Manager como un servicio de Windows {#installing-and-starting-adobe-experience-manager-as-a-windows-service}

>[!NOTE]
>
>Asegúrese de realizar el siguiente procedimiento mientras ha iniciado sesión como administrador o inicie o ejecute estos pasos mediante la selección del menú contextual **Ejecutar como administrador** .
>
>Iniciar sesión como usuario con privilegios de administrador es **insuficiente**. Si no ha iniciado sesión como administrador al completar estos pasos, recibirá errores de **acceso denegado** .

Para instalar e iniciar AEM como un servicio de Windows:

1. Abra el archivo crx-quickstart\opt\helpers\instsrv.bat en un editor de texto.
1. Si está configurando un servidor Windows de 64 bits, reemplace todas las instancias de prunsrv con uno de los siguientes comandos, según el sistema operativo:

   * prunsrv_amd64
   * prunsrv_ia64
   Este comando invoca la secuencia de comandos adecuada que inicia el daemon de servicio de Windows en Java de 64 bits en lugar de Java de 32 bits.

1. Para evitar que el proceso se ramifique en más de un proceso, aumente el tamaño máximo del montón y los parámetros JVM de PermGen. Busque el `set jvm_options` comando y establezca el valor de la siguiente manera:

   `set jvm_options=-XX:MaxPermSize=256M;-Xmx1792m`

1. Abra el símbolo del sistema, cambie el directorio actual a la carpeta crx-quickstart/opt/helpers de la instalación de AEM e introduzca el siguiente comando para crear el servicio:

   `instsrv.bat cq5`

   Para comprobar que se ha creado el servicio, abra Servicios en el panel de control Herramientas administrativas o escriba `start services.msc` en el símbolo del sistema. El servicio cq5 aparece en la lista.

1. Inicie el servicio realizando una de las siguientes acciones:

   * En el panel de control Servicios, haga clic en cq5 y en Inicio.
   ![chlimage_1-11](assets/chlimage_1-11.png)

   * En la línea de comandos, escriba net start cq5.
   ![chlimage_1-12](assets/chlimage_1-12.png)

1. Windows indica que el servicio se está ejecutando. AEM se inicia y el ejecutable prunsrv aparece en el Administrador de tareas. En el navegador web, vaya a AEM, por ejemplo, `https://localhost:4502` para empezar a usar AEM.

   ![chlimage_1-13](assets/chlimage_1-13.png)

>[!NOTE]
>
>Los valores de propiedad del archivo instsrv.bat se utilizan al crear el servicio de Windows. Si edita los valores de propiedad en instsrv.bat, debe desinstalar y volver a instalar el servicio.

>[!NOTE]
>
>Al instalar AEM como servicio, debe proporcionar la ruta absoluta para el directorio de registros en `com.adobe.xmp.worker.files.ncomm.XMPFilesNComm` Configuration Manager.

Para desinstalar el servicio, haga clic en **Detener** en el panel de control de **Servicios** o en la línea de comandos, vaya a la carpeta y escriba `instsrv.bat -uninstall cq5`. El servicio se elimina de la lista del panel de control de **Servicios** o de la lista de la línea de comandos cuando se escribe `net start`.

## Redefinición de la ubicación del directorio de trabajo temporal {#redefining-the-location-of-the-temporary-work-directory}

La ubicación predeterminada de la carpeta temporal del equipo Java es `/tmp`. AEM también utiliza esta carpeta, por ejemplo, al compilar paquetes.

Si desea cambiar la ubicación de la carpeta temporal (por ejemplo, si necesita un directorio con más espacio libre), defina un * `<new-tmp-path>`* agregando el parámetro JVM:

`-Djava.io.tmpdir="/<*new-tmp-path*>"`

para:

* la línea de comandos de inicio del servidor
* parámetro de entorno CQ_JVM_OPTS en la secuencia de comandos serverctl o start

## Otras opciones disponibles en el archivo QuickStart {#further-options-available-from-the-quickstart-file}

Las opciones adicionales y las convenciones de cambio de nombre se describen en el archivo de ayuda de QuickStart, que está disponible a través de la opción -help. Para acceder a la ayuda, escriba:

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

Al instalar AEM en una instancia de Amazon Elastic Compute Cloud (EC2), si instala tanto el autor como la publicación en la instancia EC2, la instancia de Autor se instala correctamente siguiendo el procedimiento de [instalación de instancias de AEM Manager](#installinginstancesofaemmanager); sin embargo, la instancia Publicar se convierte en Autor.

Antes de instalar la instancia de Publish en el entorno EC2, haga lo siguiente:

1. Descomprima el archivo jar para la instancia de Publish antes de iniciar la instancia por primera vez. Para desempaquetar el archivo, utilice el siguiente comando:

   ```xml
   java -jar quickstart.jar -unpack
   ```

   >[!NOTE]
   >
   >Si cambia el modo **después** de iniciar la instancia por primera vez, no podrá cambiar el modo de ejecución.

1. Inicie la instancia ejecutando:

   ```xml
   java -jar quickstart.jar -r publish
   ```

   >[!CAUTION]
   >
   >Asegúrese de ejecutar primero la instancia después de desempaquetarla ejecutando el comando anterior. De lo contrario, no se generará el relleno quickstart.properties. Sin este archivo, las futuras actualizaciones de AEM fallarán.

1. En la carpeta **bin** , abra la secuencia de comandos de **inicio** y compruebe la siguiente sección:

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='author'
   fi
   ```

1. Cambie el modo de ejecución para **publicar** y guardar el archivo.

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='publish'
   fi
   ```

1. Detenga la instancia y reiníciela ejecutando la secuencia de comandos de **inicio** .

## Verificación de la instalación {#verifying-the-installation}

Los siguientes vínculos pueden utilizarse para verificar que la instalación está operativa (todos los ejemplos se basan en que la instancia se está ejecutando en el puerto 8080 del localhost, que CRX está instalado en /crx y Launchpad en /):

* `https://localhost:8080/crx/de`
La consola CRXDE Lite.

* `https://localhost:8080/system/console`
Consola Web.

## Acciones después de la instalación {#actions-after-installation}

Aunque hay muchas posibilidades de configurar AEM WCM, se deben realizar determinadas acciones o, al menos, revisarlas inmediatamente después de la instalación:

* Consulte la lista [de comprobación de](/help/sites-administering/security-checklist.md) seguridad para las tareas necesarias para asegurarse de que el sistema permanece seguro.
* Revise la lista de usuarios y grupos predeterminados instalados con AEM WCM. Compruebe si desea realizar alguna acción en otras cuentas: consulte [Seguridad y administración](/help/sites-administering/security.md) de usuarios para obtener más detalles.

## Acceso a CRXDE Lite y a la consola web {#accessing-crxde-lite-and-the-web-console}

Una vez que se ha iniciado AEM WCM, también puede acceder a:

* [CRXDE Lite](#accessing-crxde-lite) : se utiliza para acceder y administrar el repositorio
* [Consola](#accessing-the-web-console) Web: se utiliza para administrar o configurar los paquetes OSGi (también conocidos como la Consola OSGi)

### Acceso a CRXDE Lite {#accessing-crxde-lite}

Para abrir CRXDE Lite, puede seleccionar **CRXDE Lite** en la pantalla de bienvenida o utilizar el navegador para desplazarse

```
 https://<<i>host</i>>:<<i>port</i>>/crx/de/index.jsp
```

Por ejemplo:
`https://localhost:4502/crx/de/index.jsp`

![installcq_crxdelite](assets/installcq_crxdelite.png)

#### Acceso a la consola web {#accessing-the-web-console}

Para acceder a la consola web de Adobe CQ, puede seleccionar la consola **** OSGi en la pantalla de bienvenida o utilizar el navegador para desplazarse

```
 https://<host>:<port>/system/console
```

Por ejemplo:
`https://localhost:4502/system/console`o para la página Paquetes`https://localhost:4502/system/console/bundles`

![chlimage_1-14](assets/chlimage_1-14.png)

Consulte Configuración de [OSGi con la consola](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) Web para obtener más detalles.

## Solución de problemas {#troubleshooting}

Para obtener información sobre cómo solucionar los problemas que pueden surgir durante la instalación, consulte:

* [Solución de problemas](/help/sites-deploying/troubleshooting.md)

## Uninstalling Adobe Experience Manager {#uninstalling-adobe-experience-manager}

Debido a que AEM se instala en un único directorio, no es necesario disponer de una utilidad de desinstalación. La desinstalación puede ser tan simple como eliminar todo el directorio de instalación, aunque la forma en que desinstale AEM depende de lo que desee lograr y del almacenamiento persistente que utilice.

Si el almacenamiento persistente está incrustado en el directorio de instalación, por ejemplo, en la instalación predeterminada de TarPM, al eliminar carpetas también se eliminan datos.

>[!NOTE]
>
>Adobe recomienda realizar una copia de seguridad del repositorio antes de eliminar AEM. Si elimina todo el &lt;cq-installation-directory>, eliminará el repositorio. Para conservar los datos del repositorio antes de eliminarlos, mueva o copie la carpeta &lt;cq-installation-directory>/crx-quickstart/repository antes de eliminar las otras carpetas.

Si la instalación de AEM utiliza almacenamiento externo, por ejemplo, un servidor de bases de datos, la eliminación de carpetas no elimina los datos automáticamente, pero sí elimina la configuración de almacenamiento, lo que dificulta la restauración del contenido de JCR.
