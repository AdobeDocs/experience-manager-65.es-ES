---
title: Instalación de Workbench
seo-title: Instalación de Workbench
description: Instale Workbench.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
role: Administrador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2247'
ht-degree: 0%

---


# Instalar Workbench {#install-workbench}

Este documento proporciona instrucciones para instalar y configurar AEM Forms Workbench. El programa de instalación también instala Forms Designer.

## ¿Quién debe leer este documento? {#who-should-read-this-doc}

Este documento está diseñado para administradores o desarrolladores responsables de la instalación, configuración, administración o implementación de Workbench. También se incluye información necesaria para configurar el sistema de modo que admita los procesos actualizados de AEM Forms. La información proporcionada se basa en el supuesto de que cualquiera que lea este documento está familiarizado con el sistema operativo Microsoft® Windows®.

## Información adicional {#additional-information}

Los recursos de esta tabla pueden ayudarle a obtener más información y a empezar a utilizar AEM Forms.
<table>
 <tbody>
  <tr>
   <td><p><strong>Para obtener información acerca de</strong></p> </td>
   <td><p><strong>Consulte</strong></p> </td>
  </tr>
  <tr>
   <td><p>Información de procedimiento para Workbench</p> </td>
   <td><p><a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">Ayuda de Workbench</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Información general sobre AEM Forms y cómo se integra con otros productos de Adobe</p> </td>
   <td><p><a href="http://adobe.com/go/learn_aemforms_introduction_65">Información general de AEM Forms</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Toda la documentación disponible para AEM Forms</p> </td>
   <td><p><a href="http://adobe.com/go/learn_aemforms_introduction_65">Documentación de AEM Forms</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Actualizaciones de parches, notas técnicas e información adicional sobre esta versión del producto</p> </td>
   <td><p>Soporte empresarial de Adobe de contacto</a><br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Flex Workspace está en desuso para AEM Forms. Está disponible para la versión de AEM Forms.

## Antes de instalar {#before-you-install}

### Información general sobre la instalación de Workbench {#workbench-installation-overview}

Workbench es un entorno de desarrollo integrado (IDE) que los desarrolladores y autores de formularios utilizan para crear formularios y procesos empresariales automatizados. También se utiliza para administrar los recursos y servicios que utilizan los procesos y formularios.

La siguiente ilustración muestra la instalación de Workbench, que incluye:
* Diseño de procesos con Workbench
* Diseño de formulario con Designer

>[!NOTE]
>
>El servidor de AEM Forms requiere un programa de instalación independiente. Para obtener más información, consulte la documentación de instalación de AEM Forms en JEE.

![default-render-form](assets/installing-workbench.png)

## Requisitos previos del sistema {#system-prerequisites}

Esta sección describe los requisitos de hardware y software y las plataformas soportadas.

### Requisitos mínimos de hardware y software {#minimum-hardware-software-requirements}

****
WorkbenchSe recomiendan los siguientes requisitos como mínimo: Espacio en disco para la instalación:
* 680 MB solo para Workbench.
* 2,15 GB en una sola unidad para una instalación completa de Workbench, Designer y el conjunto de muestras.
* 400 MB para directorios de instalación temporales - 200 MB en el directorio \temp de usuario y 200 MB en el directorio temporal de Windows.

>[!NOTE]
>
>Si todas estas ubicaciones residen en una sola unidad, debe haber 1,5 GB de espacio disponible durante la instalación. Los archivos copiados en los directorios temporales se eliminan cuando se completa la instalación.

* Requisitos de hardware: Procesador Intel® Pentium® 4 o AMD equivalente, 1 GHz.
* Java™ Runtime Environment (JRE) 7.0 update 51 o posterior actualiza a 7.0.
* Mínimo1024 X 768 píxeles o buena resolución del monitor con color de 16 bits o superior.
* Conexión de red TCP/IPv4 o TCP/IPv6 al servidor AEM Forms.
* Instale los paquetes de tiempo de ejecución redistribuibles de Visual C++ 2012 de 32 bits.
* Instale los paquetes de tiempo de ejecución redistribuibles de Visual C++ 2013 de 32 bits.

>[!NOTE]
>
>Debe tener privilegios administrativos para instalar Workbench. Si va a realizar la instalación con una cuenta que no sea de administrador, el instalador le pedirá las credenciales de una cuenta adecuada.

### Plataformas compatibles {#supported-platforms}

Consulte la lista completa de plataformas admitidas para Workbench en [Plataformas admitidas por AEM Forms](http://adobe.com/go/learn_aemforms_supportedplatforms_65).

## Consideraciones de instalación de Designer {#designer-installation-considerations}

De forma predeterminada, la instalación de Workbench incluye una versión correspondiente de Designer en inglés únicamente. Si la aplicación de instalación de Workbench detecta una versión existente de Designer en el equipo, la instalación puede finalizar y se le pedirá que elimine la versión actual de Designer antes de poder continuar.
La tabla siguiente contiene una lista completa de los posibles escenarios de instalación de Designer que puede encontrar, así como las acciones que debe realizar al instalar Workbench.

<table>
 <tbody>
  <tr>
   <td><p><strong>Versión de Designer instalada actualmente</strong></p> </td>
   <td><p><strong>Acciones necesarias</strong></p> </td>
  </tr>
  <tr>
   <td><p>Acrobat Pro o Acrobat Pro Extended (incluye Designer)</p> </td>
   <td><p>Ninguna.<br /> 
La instalación de Workbench detecta una instancia de Designer instalada en el equipo con Acrobat Pro o Acrobat Pro Extended.<br />
En el mismo sistema pueden coexistir distintas versiones de Designer, por ejemplo, Designer 6.4.x para Workbench 6.4 y Designer 6.5.0.x para Workbench 6.5. No es necesario desinstalar la versión de Designer instalada con Acrobat 10 Pro o Acrobat 10 Pro Extended, o superior.
<br /></p> </td>
  </tr>
  <tr>
   <td><p>Designer (independiente)</p> </td>
   <td><p>Ninguna. <br />La versión de Designer incluida con Workbench solo está en inglés. <br />El instalador de Workbench no reinstala una nueva versión de Designer. En su lugar, se parcheará una versión actualizada, incluida con el instalador de Workbench. Esto también le permite utilizar la versión localizada de Designer en Workbench.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Para desinstalar Designer (independiente) en Windows 10 {#uninstall-designer-standalone-windows10}

1. Vaya a **Panel de control de Campaign > Programas > Programas y características**
1. En la lista Programas instalados actualmente, seleccione **Diseñador de Adobe**.
1. Haga clic en **Desinstalar** y, a continuación, haga clic en **Yes**.

## Instalación de Workbench {#installing-workbench}

En este capítulo se describe cómo instalar Workbench.

### Instalación y ejecución de Workbench {#installing-and-running-workbench}

Antes de instalar Workbench, debe asegurarse de que su entorno incluya el software y el hardware necesarios para ejecutarlo (consulte la sección: **Antes de instalar**).

**Para instalar y ejecutar Workbench:**

1. Realice una de estas tareas:
   * Vaya al directorio \workbench del medio de instalación y haga doble clic en el archivo run_windows_installer.bat.
   * Descargue y descomprima el área de trabajo en su sistema de archivos. Una vez descargado, vaya al directorio \workbench y haga doble clic en el archivo run_windows_installer.bat.

   >[!IMPORTANT]
   >
   >El instalador de Workbench solo se ejecuta desde una unidad local. No se puede ejecutar desde un sitio remoto.

   >[!NOTE]
   >
   >Si aparece el error &quot;No se pudo crear la máquina virtual Java&quot;, cree una variable de entorno llamada _JAVA_OPTIONS con valor -Xmx512M y ejecute el instalador.

1. En la pantalla Introducción, haga clic en Siguiente.
1. Lea el Acuerdo de licencia del producto, seleccione Acepto los términos del Acuerdo de licencia y, a continuación, haga clic en Siguiente.
1. (Opcional) Seleccione Instalar Adobe Designer si necesita esta herramienta para crear y modificar formularios.

   >[!NOTE]
   >
   >Puede seguir utilizando Designer instalado con Acrobat 10 dejando esta opción sin seleccionar.

1. Acepte el directorio predeterminado como aparece enumerado o   haga clic en Elegir y vaya al directorio donde instalará Workbench y, a continuación, haga clic en Siguiente.

   >[!NOTE]
   >
   >La ruta del directorio de instalación no debe contener caracteres # (libras) y $ (dólares).

1. Revise el resumen de la preinstalación y haga clic en Instalar. El programa de instalación muestra el progreso de la instalación.
1. Revise el resumen de la instalación. Seleccione Iniciar AEM Forms Workbench para iniciar Workbench y haga clic en Siguiente.
1. Revise las Notas de la versión y haga clic en Finalizado.
1. Los siguientes elementos ya están instalados en el equipo:
   * **Workbench**: Para ejecutar Workbench desde el menú Inicio, seleccione Todos los programas > AEM Forms > Workbench si elige almacenar la carpeta de acceso directo allí. Para obtener información,   consulte la documentación <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">Uso de Workbench</a> .
   * **Designer**: Puede acceder a Designer desde Workbench. Para obtener más información, consulte el tema Introducción en <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf">Ayuda de Designer</a>.
   * **SDK** de AEM Forms: Para obtener más información sobre el uso del SDK, consulte  <a href="http://www.adobe.com/go/learn_aemforms_programming_65">Programación con AEM Forms</a>.

## Actualización de procesos {#upgrading-processes}

Los procesos de AEM Forms en JEE se pueden actualizar a aplicaciones de AEM Forms mediante el Asistente para actualización. Consulte Actualización de la documentación de artefactos heredados en la Ayuda de Workbench para obtener más información.

### Configuración e inicio de sesión en un servidor {#configuring-and-logging-server}

Para utilizar Workbench, debe tener una instancia de AEM Forms en ejecución, normalmente en un equipo independiente. Debe tener un nombre de usuario y una contraseña para iniciar sesión en AEM Forms, así como detalles sobre la ubicación del servidor.

>[!NOTE]
>
>Si configuró AEM Forms para utilizar el proveedor de repositorios de Documentum de EMC o IBM FileNet y desea iniciar sesión en un repositorio que no sea el repositorio configurado como predeterminado en AEM consola de administración de formularios, proporcione el nombre de usuario como username@Repository.

### Configuración del tiempo de espera {#configuring-timeout-settings}

De forma predeterminada, el tiempo de espera de Workbench es de dos horas, independientemente de la actividad o la inactividad. Para editar la configuración de tiempo de espera, consulte &quot;Configuración de la administración de usuarios > Configurar atributos avanzados del sistema&quot; en la <a href="https://docs.adobe.com/content/help/en/experience-manager-65/forms/administrator-help/configure-user-management/configure-advanced-system-attributes.html">ayuda de la consola de administración</a>.

### Configuración de Workbench para que se conecte a través de HTTPS {#configuring-workbench-to-connect-over-HTTPS}

Para conectar Workbench a un servidor de AEM Forms a través de HTTPS, debe asegurarse de que Workbench reconozca la autoridad de certificación (CA) que emitió la clave pública como de confianza. Si no se reconoce que el certificado proviene de un origen de confianza, debe actualizar el archivo cacert ubicado en el directorio [Workbench_HOME]/workbench/jre/lib/security.

>[!NOTE]
>
>[Workbench_] HOME representa el directorio donde instaló Workbench. La ubicación predeterminada es C:\Program Files (x86)\Adobe Experience Manager forms Workbench.

Asegúrese de conectarse a HTTPS utilizando el nombre especificado en el certificado. Normalmente, este nombre es el nombre de host completo.

**Para actualizar el archivo** cacert:
1. Asegúrese de tener una copia del certificado Secure Sockets Layer (SSL). Póngase en contacto con el administrador que configuró el servidor SSL o exporte el certificado utilizando un explorador web.

   >[!NOTE]
   >
   >Para exportar el certificado, abra un explorador web e inicie sesión en la consola de administración, instale el certificado en el explorador y, a continuación, exporte el certificado desde el explorador a una ubicación de almacenamiento temporal (o directamente al directorio [Workbench_HOME]/workbench/jre/lib/security ).

1. Copie el certificado en el directorio [Workbench_HOME]/workbench/jre/lib/security.

1. Abra una ventana del símbolo del sistema, vaya a [Workbench_HOME]/workbench/jre/bin y, a continuación, escriba el siguiente comando:
   `keytool -import -storepass changeit -file [Workbench_HOME]\workbench\jre\lib\security\ssl_cert_for_certname.cer -keystore [Workbench_HOME]\workbench\jre\lib\security\cacerts -alias example`
Donde:
   * cambiar es la contraseña predeterminada para el almacén de claves cacerts.
   * certname es el certificado seleccionado en el paso 1.
   * Por ejemplo, el alias que elija para el certificado. Este valor puede cambiarse

1. Cuando se le pida que confíe en el certificado, escriba Yes y pulse la tecla Intro. La herramienta de teclas procede a importar el archivo cacerts en el directorio [Workbench_HOME]/workbench/jre/lib/security.

1. Cierre y reinicie Workbench para aplicar los cambios.

### Configuración de la caché para plantillas generadas dinámicamente {#configuring-cache-settings-for-dynamically-generated-templates}

Los siguientes aspectos de la operación de caché deben tenerse en cuenta si la aplicación genera plantillas únicas sobre la marcha al actualizar automáticamente el contenido XFA. De hecho, cada transacción utiliza una plantilla nueva y única.

Cuando el generador de formularios o la salida buscan, o actualizan, entradas en la caché para una plantilla de formulario específica, utiliza varios valores clave para localizar la entrada de caché específica a la que se accederá.

* **Nombre** del archivo de plantilla: Ubicación y nombre de archivo de la plantilla utilizada como identificador único principal del formulario en caché.
* **Marca de tiempo**: El archivo de plantilla contiene una marca de tiempo que se utiliza para determinar la hora de la última actualización del formulario.
* **UUID** de plantilla: Designer inserta en cada plantilla un identificador único (UUID) para el formulario y su versión. Cada vez que se actualiza el formulario, se actualiza el UUID incrustado. Por ejemplo, una plantilla XDP puede mostrar el siguiente contenido:

   `<?xml version="1.0" encoding="UTF-8"?>`
   `<?xfa generator="AdobeAEM formsDesignerES_V8.2" APIVersion="2.6.7185.0"?><xdp:xdp xmlns:xdp=http://ns.adobe.com/xdp/ timeStamp="2008-07-29T21:22:12Z" uuid="823e538f-ff6c-4961-b759-f7626978a223"><template xmlns="http://www.xfa.org/schema/xfa-template/2.6/">`

* **Opciones** de procesamiento: Dentro de la caché de formularios procesados, el contenido de la caché se almacena por separado para cada conjunto de opciones de procesamiento únicas.


El servicio Forms recibe las plantillas por referencia al nombre de archivo o la ubicación del repositorio, o por valor como objeto XML en la memoria.
* **Plantillas pasadas por referencia**: Utiliza la raíz del contenido y el nombre del formulario. Si se pasan plantillas únicas con diferentes nombres de archivo en cada solicitud utilizando este método, la caché de disco crecerá indefinidamente y nunca se reutilizará. Para evitarlo, las plantillas únicas deben pasarse con el mismo nombre de archivo para garantizar que la misma caché se actualice para todas las solicitudes.
* **Plantillas pasadas por valor**: Utiliza bytes de plantilla pasados junto con los datos mediante el parámetro inDataDoc . Si se pasan plantillas únicas con un UUID diferente mediante este método, la caché del disco crecerá indefinidamente y nunca se reutilizará. Para evitarlo, el atributo UUID debe eliminarse de todas las plantillas para garantizar que no se cree ninguna caché para la plantilla. Alternativamente, pasar el mismo UUID no nulo permite crear los objetos de caché, pero garantiza que la misma caché se actualice con cada solicitud.

Para evitar que la caché crezca indefinidamente, tenga en cuenta los siguientes factores para procesar plantillas generadas dinámicamente con las nuevas API de AEM Forms, las que son renderHTMLForm2 y renderPDFForm2.

Al utilizar las nuevas API, la plantilla se pasa como un objeto de documento, que se gestiona en el servicio de Forms en función de si está pasivada o no.

Para documentos pasivados en los que el UUID y la raíz de contenido sirven como clave de caché, tenga en cuenta los siguientes aspectos:
* La caché no se crea para plantillas de entrada pasivadas sin UUID.
* Si se pasa más de una plantilla de entrada pasiva que tiene el mismo UUID y la misma raíz de contenido, se sobrescribe la misma caché.

Para los documentos no pasivados en los que el nombre de archivo y la raíz de contenido sirven como clave de caché, tenga en cuenta el siguiente aspecto:
* Para las plantillas de entrada no pasivadas, el almacenamiento en caché depende de la raíz del contenido y del nombre de archivo desde el que se generó el documento.
La misma caché se utilizará solo para solicitudes con la misma raíz de contenido y el mismo nombre de archivo de plantilla.
Las siguientes prácticas recomendadas garantizarán que la caché no crezca indefinidamente cuando se pasen plantillas generadas dinámicamente al servicio de Forms:
   * Elimine el UUID o pase el mismo UUID en todas las plantillas generadas dinámicamente.
   * Genere el documento desde bytes de plantilla o desde el mismo nombre de archivo en disco.

### Desinstalación de Workbench {#uninstalling-workbench}

Utilice la función Agregar o quitar programas del Panel de control de Campaign para iniciar el programa de desinstalación. Las aplicaciones Workbench y Designer tienen programas de desinstalación independientes.

## Configuración del Editor XDC de AEM Forms {#configuring-aem-forms-xdc-editor}

Con el Editor XDC, los administradores de impresoras de red pueden crear y modificar archivos XML Forms Architecture Device Configuration (XDC). Los archivos XDC describen las capacidades de las impresoras, como el idioma de la impresora o la correlación entre el tamaño del papel y la ubicación de la bandeja.

Antes de que el administrador de la impresora de red utilice el Editor XDC, reubique los archivos XDC de muestra y consulte Creación de perfiles de dispositivo mediante el Editor XDC.

**Para obtener los archivos** XDC de ejemplo:
1. En el servidor de AEM Forms, busque la carpeta XDC en [AEM Forms root]\sdk\samples\Output\IVS.
1. Copie el contenido de esta carpeta en un directorio al que se pueda acceder desde el sistema Workbench o Eclipse.

**Para obtener la ayuda** del Editor XDC:
1. Vaya al sitio web de documentación de AEM Forms.
1. Haga clic en la pestaña **Develop** y vaya a Creación de perfiles de dispositivo mediante el Editor XDC. Descargue el archivo xdc_editor_help_web.zip e instale los archivos de ayuda siguiendo las instrucciones proporcionadas en el archivo Léame.

