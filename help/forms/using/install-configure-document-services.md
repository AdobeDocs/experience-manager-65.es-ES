---
title: Instalación y configuración de document services
seo-title: Instalación y configuración de document services
description: Instale AEM Forms document services para crear, ensamblar, distribuir, archivar documentos PDF, agregar firmas digitales para limitar el acceso a los documentos y descodificar formularios con códigos de barras.
seo-description: Instale AEM Forms document services para crear, ensamblar, distribuir, archivar documentos PDF, agregar firmas digitales para limitar el acceso a los documentos y descodificar formularios con códigos de barras.
uuid: 908806a9-b0d4-42d3-9fe4-3eae44cf4326
topic-tags: installing
discoiquuid: b53eae8c-16ba-47e7-9421-7c33e141d268
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '4296'
ht-degree: 2%

---


# Instalación y configuración de document services {#installing-and-configuring-document-services}

AEM Forms proporciona un conjunto de servicios de OSGi para realizar distintas operaciones a nivel de documento, por ejemplo, servicios para crear, ensamblar, distribuir y archivar documentos PDF, agregar firmas digitales para limitar el acceso a documentos y descodificar formularios codificados de barras. Estos servicios se incluyen en el paquete de complementos de AEM Forms. En conjunto, estos servicios se conocen como servicios de documentos. La lista de servicios de documentos disponibles y sus principales funciones es la siguiente:

* **Servicio Assembler:** permite combinar, reorganizar y aumentar documentos PDF y XDP y obtener información sobre documentos PDF. También ayuda a convertir y validar documentos PDF a PDF/A estándar, transforma PDF forms, formularios XML y PDF forms a PDF/A-1b, PDF/A-2b y PDFA/A-3b. Para obtener más información, consulte [Servicio del ensamblador](/help/forms/using/assembler-service.md).

* **Servicio ConvertPDF:** permite convertir documentos PDF a archivos PostScript o de imagen (JPEG, JPEG 2000, PNG y TIFF). Para obtener más información, consulte [ConvertPDF Service](/help/forms/using/using-convertpdf-service.md).

* **Servicio de Forms con códigos de barras:** permite extraer datos de imágenes electrónicas de códigos de barras. El servicio acepta archivos TIFF y PDF que incluyen uno o más códigos de barras como entrada y extrae los datos del código de barras. Para obtener más información, consulte [Servicio de Forms con códigos de barras](/help/forms/using/using-barcoded-forms-service.md).

* **Servicio DocAssurance:** permite cifrar y descifrar documentos, ampliar la funcionalidad de Adobe Reader con derechos de uso adicionales y agregar firmas digitales a sus documentos. El servicio Doc Assurance contiene tres servicios: firma, cifrado y extensión de lector. Para obtener más información, consulte [DocAssurance Service](/help/forms/using/overview-aem-document-services.md).

* **Servicio de cifrado:** permite cifrar y descifrar documentos. Cuando se cifra un documento, su contenido se vuelve ilegible. Un usuario autorizado puede descifrar el documento para obtener acceso a su contenido. Para obtener más información, consulte [Servicio de cifrado](/help/forms/using/overview-aem-document-services.md#encryption-service).

* **Servicio Forms:** permite crear aplicaciones cliente de captura de datos interactivas que validan, procesen, transformen y entreguen formularios que normalmente se crean en Forms Designer. El servicio Forms procesa cualquier diseño de formulario que se desarrolle en documentos PDF. Para obtener más información, consulte [Servicio de Forms](/help/forms/using/forms-service.md).

* **Servicio de salida:** permite crear documentos en distintos formatos, incluidos PDF, formatos de impresora láser y formatos de impresora de etiquetas. Los formatos de impresora láser son PostScript y Printer Control Language (PCL). Para obtener más información, consulte [Servicio de salida](/help/forms/using/output-service.md).

* **Servicio Generador de PDF:** el servicio Generador de PDF proporciona API para convertir formatos de archivo nativos a PDF. También convierte PDF a otros formatos de archivo y optimiza el tamaño de los documentos PDF. Para obtener más información, consulte [PDF Generator Service](aem-document-services-programmatically.md#pdfgeneratorservice).

* **Servicio de extensión de Reader:**  permite a su organización compartir fácilmente documentos PDF interactivos mediante la ampliación de la funcionalidad de Adobe Reader con derechos de uso adicionales. El servicio activa funciones que no están disponibles cuando se abre un documento PDF con Adobe Reader, como agregar comentarios a un documento, rellenar formularios y guardar el documento. Para obtener más información, consulte [Servicio de extensión de Reader](/help/forms/using/overview-aem-document-services.md#reader-extension-service).

* **Servicio de firma:** permite trabajar con firmas digitales y documentos en el servidor de AEM. Por ejemplo, el servicio de firma se suele utilizar en las siguientes situaciones:

   * El servidor de AEM certifica un formulario antes de enviarlo a un usuario para que lo abra con Acrobat o Adobe Reader.
   * El servidor de AEM valida una firma que se agregó a un formulario mediante Acrobat o Adobe Reader.
   * El servidor de AEM firma un formulario en nombre de un notario público.

   El servicio de firma accede a los certificados y credenciales almacenados en el almacén de confianza. Para obtener más información, consulte [Servicio de firma](/help/forms/using/aem-document-services-programmatically.md).

AEM Forms es una potente plataforma de clase empresarial y document services es solo una de las capacidades de AEM Forms. Para obtener la lista completa de las funcionalidades, consulte [Introducción a AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topología de implementación {#deployment-topology}

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. Por lo general, solo se necesita una instancia de AEM (autor o publicación) para ejecutar AEM Forms document services. Se recomienda la siguiente topología para ejecutar AEM Forms document services. Para obtener información detallada sobre topologías, consulte [Arquitectura y topologías de implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![Arquitectura y topologías de implementación para AEM Forms](do-not-localize/document-services.png)

>[!NOTE]
>
>Aunque AEM Forms le permite configurar y ejecutar todas las funcionalidades desde un solo servidor, debe planificar la capacidad, equilibrar la carga y configurar servidores dedicados para funcionalidades específicas en un entorno de producción. Por ejemplo, para un entorno que utiliza el servicio Generador de PDF para convertir miles de páginas al día y varios formularios adaptables para capturar datos, configure servidores AEM Forms independientes para el servicio Generador de PDF y las funciones de formularios adaptables. Ayuda a proporcionar un rendimiento óptimo y a escalar los servidores de forma independiente entre sí.

## Requisitos del sistema {#system-requirements}

Antes de empezar a instalar y configurar AEM Forms document services, asegúrese de que:

* La infraestructura de hardware y software está implementada. Para obtener una lista detallada del hardware y el software compatibles, consulte [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

* La ruta de instalación de la instancia de AEM no contiene espacios en blanco.
* Se está ejecutando una instancia de AEM. En AEM terminología, una &quot;instancia&quot; es una copia de AEM que se ejecuta en un servidor en modo de autor o publicación. Por lo general, solo necesita una instancia de AEM (autor o publicación) para ejecutar AEM Forms document services:

   * **Autor**: Instancia de AEM utilizada para crear, cargar y editar contenido y para administrar el sitio web. Una vez que el contenido está listo para su lanzamiento, se duplica en la instancia de publicación.
   * **Publicar**: Instancia de AEM que sirve el contenido publicado al público a través de Internet o una red interna.

* Se cumplen los requisitos de memoria. El paquete de complementos de AEM Forms requiere:

   * 15 GB de espacio temporal para instalaciones basadas en Microsoft Windows.
   * 6 GB de espacio temporal para instalaciones basadas en UNIX.

* El software cliente necesario para que el generador de PDF realice la conversión en Microsoft Windows y Linux está instalado:

   * **Microsoft Windows**: Instalar  [Microsoft ](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)Office o  [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux**: Instalación de  [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* En Microsoft Windows, PDF Generator admite rutas de conversión WebKit, Acrobat WebCapture y PhantomJS para convertir archivos HTML en documentos PDF.
>* En sistemas operativos basados en UNIX, PDF Generator admite rutas de conversión de WebKit y PhantomJS para convertir archivos HTML en documentos PDF.

>



### Requisitos adicionales para sistemas operativos basados en UNIX {#extrarequirements}

Si está utilizando el sistema operativo basado en UNIX, instale los siguientes paquetes del medio de instalación del sistema operativo correspondiente:

<table> 
 <tbody> 
  <tr> 
   <td> 
    <ul> 
     <li>expat</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libxcb</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>freetype</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libXau</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 
    <ul> 
     <li>libSM</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>zlib</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libICE</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libuuid</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 
    <ul> 
     <li>glibc</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libXext</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>nss-softokn-freebl</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>fontconfig</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 
    <ul> 
     <li>libX11</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libXrender</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libXrandr</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libXinerama</li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

* **(Solo** generador de PDF) Instale la versión de 32 bits de las bibliotecas libcurl, libcrypto y libssl y cree los siguientes enlaces simbólicos. Los enlaces simbólicos señalan a la última versión de las bibliotecas respectivas:

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **(Solo generador de PDF)** El servicio Generador de PDF es compatible con las rutas WebKit y PhantomJS para convertir archivos HTML en documentos PDF. Para habilitar la conversión para la ruta PhantomJS, instale las bibliotecas de 64 bits que se enumeran a continuación. Por lo general, estas bibliotecas ya están instaladas. Si falta alguna biblioteca, instálela manualmente:

   * linux-gate.so.1
   * libz.so.1
   * libfontconfig.so.1
   * libfreetype.so.6
   * libdl.so.2
   * librt.so.1
   * libpthread.so.0
   * libstdc++.so.6
   * libm.so.6
   * libgcc_s.so.1
   * libc.so.6
   * ld-linux.so.2
   * libexpat.so.1

## Configuraciones de preinstalación {#preinstallationconfigurations}

Las configuraciones enumeradas en la sección de configuraciones previas a la instalación solo se aplican al servicio de Generador de PDF. Si no está configurando el servicio PDF Generator, puede omitir la sección de configuración previa a la instalación.

### Instalación de aplicaciones de Adobe Acrobat y de terceros {#install-adobe-acrobat-and-third-party-applications}

Si va a usar el servicio Generador de PDF para convertir formatos de archivo nativos como Microsoft Word, Microsoft Excel, Microsoft PowerPoint, OpenOffice, WordPerfect X7 y Adobe Acrobat a documentos PDF, asegúrese de que estas aplicaciones estén instaladas en el servidor AEM Forms.

>[!NOTE]
>
>* Adobe Acrobat, Microsoft Word, Excel y Powerpoint solo están disponibles para Microsoft Windows. Si está utilizando el sistema operativo basado en UNIX, instale OpenOffice para convertir archivos de texto enriquecido y archivos compatibles de Microsoft Office a documentos PDF.
>* Descarte todos los cuadros de diálogo que se muestran después de instalar Adobe Acrobat y software de terceros para todos los usuarios configurados para utilizar el servicio PDF Generator.
>* Inicie todo el software instalado al menos una vez. Descartar todos los cuadros de diálogo de todos los usuarios configurados para utilizar el servicio PDF Generator.

>



Después de instalar Acrobat, abra Microsoft Word. En la ficha **Acrobat** haga clic en **Crear PDF** y convierta un archivo .doc o .docx disponible en el equipo a un documento PDF. Si la conversión se realiza correctamente, AEM Forms está listo para utilizar Acrobat con el servicio de Generador de PDF.

### Configuración de variables de entorno {#setup-environment-variables}

Establezca variables de entorno para el Kit de desarrollo de Java de 32 y 64 bits, aplicaciones de terceros y Adobe Acrobat. Las variables de entorno deben contener la ruta absoluta del ejecutable utilizado para iniciar la aplicación correspondiente, por ejemplo, la tabla siguiente enumera las variables de entorno para algunas aplicaciones:

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Aplicación</strong></p> </td> 
   <td><p><strong>Variable de entorno</strong></p> </td> 
   <td><p><strong>Ejemplo</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>JDK (64 bits)</strong></p> </td> 
   <td><p>JAVA_HOME</p> </td> 
   <td><p>C:\Program Files\Java\jdk1.8.0_74</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>JDK (32 bits)</strong></p> </td> 
   <td><p>JAVA_HOME_32</p> </td> 
   <td><p>C:\Program Files (x86)\Java\jdk1.8.0_74</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>Adobe Acrobat</strong></p> </td> 
   <td><p>Acrobat_PATH</p> </td> 
   <td><p>C:\Program Files (x86)\Adobe\Acrobat 2015\Acrobat\Acrobat.exe</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>Bloc de notas</strong></p> </td> 
   <td><p>Notepad_PATH</p> </td> 
   <td><p>C:\WINDOWS\notepad.exe<br /> <strong></strong></p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>OpenOffice</strong></p> </td> 
   <td><p>OpenOffice_PATH</p> </td> 
   <td><p>C:\Program Files (x86)\OpenOffice.org4</p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>* Todas las variables de entorno y las rutas respectivas distinguen entre mayúsculas y minúsculas.
>* JAVA_HOME, JAVA_HOME_32 y Acrobat_PATH (solo Windows) son variables de entorno obligatorias.
>* La variable de entorno OpenOffice_PATH se establece en la carpeta de instalación en lugar de en la ruta del ejecutable.
>* No configure variables de entorno para aplicaciones de Microsoft Office como Word, PowerPoint, Excel y Project, o para AutoCAD. Si estas aplicaciones están instaladas en el servidor, el servicio Generate PDF inicia automáticamente estas aplicaciones.
>* En plataformas basadas en UNIX, instale OpenOffice como /root. Si OpenOffice no está instalado como raíz, el servicio PDF Generator no convierte los documentos de OpenOffice a documentos PDF. Si necesita instalar y ejecutar OpenOffice como un usuario no raíz, proporcione derechos de sudo al usuario no raíz.
>* Si está utilizando OpenOffice en una plataforma basada en UNIX, ejecute el siguiente comando para configurar la variable path:

>
>  
`export OpenOffice_PATH=/opt/openoffice.org4`

### (Solo para IBM WebSphere) Configure el proveedor de socket SSL de IBM {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

Realice los siguientes pasos para configurar el proveedor de sockets SSL de IBM:

1. Cree una copia del archivo java.security. La ubicación predeterminada del archivo es `[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`.
1. Abra el archivo java.security copiado para editarlo.
1. Cambie las fábricas de socket SSL predeterminadas para utilizar las fábricas JSSE2 en lugar de las fábricas predeterminadas de IBM WebSphere:

   **Contenido predeterminado:**

   ```shell
   #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   #WebSphere socket factories (in cryptosf.jar)
   ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

   **Contenido modificado:**

   ```shell
   ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   
   #WebSphere socket factories (in cryptosf.jar)
   #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

1. Para permitir que el servidor de AEM Forms utilice el archivo java.security actualizado, al iniciar el servidor de AEM Forms, agregue el siguiente argumento java:

   `-Djava.security.properties= [path of newly created Java.security file].`

### (Solo Windows) Configure el servicio de instalación de tinta y escritura a mano {#configure-install-ink-and-handwriting-service}

Si está ejecutando Microsoft Windows Server, configure el servicio de escritura a mano y tinta. El servicio es necesario para abrir archivos de Microsoft PowerPoint que utilizan funciones de vinculación de Microsoft Office:

1. Abra el Administrador de servidores. Haga clic en el icono **[!UICONTROL Server Manager]** en la bandeja de inicio rápido.
1. Haga clic en **[!UICONTROL Agregar características]** en el menú **[!UICONTROL Funciones]**. Seleccione la casilla **[!UICONTROL Ink and Handwrite Services]**.
1. **[!UICONTROL Seleccione]** Cuadro de diálogo Funciones con  **[!UICONTROL Ink y Servicios de escritura a mano]** seleccionados. Haga clic en **[!UICONTROL Instalar]** y el servicio estará instalado.

### (Solo Windows) Configure las opciones del bloque de archivos para Microsoft Office {#configure-the-file-block-settings-for-microsoft-office}

Cambie la configuración del centro de confianza de Microsoft Office para habilitar el servicio PDF Generator para convertir archivos creados con versiones anteriores de Microsoft Office.

1. Abra una aplicación de Microsoft Office. Por ejemplo, Microsoft Word. Vaya a **[!UICONTROL Archivo]** **[!UICONTROL Opciones]**. Aparecerá el cuadro de diálogo de opciones.

1. Haga clic en **[!UICONTROL Centro de confianza]** y en **[!UICONTROL Configuración del centro de confianza]**.
1. En la **[!UICONTROL configuración del Centro de confianza]**, haga clic en **[!UICONTROL Configuración del bloque de archivos]**.
1. En la lista **[!UICONTROL Tipo de archivo]**, anule la selección de **[!UICONTROL Abrir]** para el tipo de archivo que el servicio Generador de PDF debe poder convertir a documentos PDF.

### (Solo Windows) Otorgue el privilegio Reemplazar un token a nivel de proceso {#grant-the-replace-a-process-level-token-privilege}

La cuenta de usuario utilizada para iniciar el servidor de aplicaciones requiere el privilegio **Replace a process level token**. La cuenta del sistema local tiene el privilegio **Replace a process level token** de forma predeterminada. Para los servidores que se ejecutan con un usuario del grupo Administradores locales, el privilegio debe otorgarse explícitamente. Siga estos pasos para conceder el privilegio:

1. Abra el Editor de directivas de grupo para Microsoft Windows. Para abrir el Editor de directivas de grupo, haga clic en **[!UICONTROL Inicio]**, escriba **gpedit.msc** en el cuadro Iniciar búsqueda y haga clic en **[!UICONTROL Editor de directivas de grupo]**.
1. Vaya a **[!UICONTROL Política de equipo local]** > **[!UICONTROL Configuración de equipo]** > **[!UICONTROL Configuración de Windows]** > **[!UICONTROL Configuración de seguridad]** > **[!UICONTROL Políticas locales]** > **[!UICONTROL Asignación de derechos de usuario]** y edite el **[!UICONTROL Reemplazar a token]** de nivel de proceso e incluya el grupo Administradores.
1. Agregue el usuario a la entrada Reemplazar un token de nivel de proceso .

### (Solo Windows) Habilite el servicio Generador de PDF para usuarios que no sean administradores {#enable-the-pdf-generator-service-for-non-administrators}

Puede habilitar a un usuario que no sea administrador para que utilice el servicio de Generador de PDF. Normalmente, solo los usuarios con privilegios administrativos pueden utilizar el servicio:

1. Cree una variable de entorno, PDFG_NON_ADMIN_ENABLED.
1. Establezca el valor de la variable de entorno en TRUE.
1. Reinicie la instancia de AEM Forms.

### (Solo Windows) Deshabilitar el control de cuentas de usuario (UAC) {#disable-user-account-control-uac}

1. Para acceder a la Utilidad de configuración del sistema, vaya a **[!UICONTROL Inicio > Ejecutar]** y, a continuación, introduzca **[!UICONTROL MSCONFIG]**.
1. Haga clic en la pestaña **[!UICONTROL Tools]** y desplácese hacia abajo y seleccione **[!UICONTROL Change UAC Settings]**. Haga clic en **[!UICONTROL Launch]** para ejecutar el comando en una nueva ventana.
1. Ajuste el control deslizante al nivel No notificar nunca. Cuando termine, cierre la ventana de comandos y cierre la ventana Configuración del sistema.
1. Compruebe que la configuración del Registro para UAC está establecida en 0 (cero). Siga estos pasos para verificar:

   1. Microsoft recomienda realizar una copia de seguridad del registro antes de modificarlo. Para ver los pasos detallados, consulte [Cómo realizar una copia de seguridad y restaurar el Registro en Windows](https://support.microsoft.com/en-us/help/322756).
   1. Abra el editor del Registro de Microsoft Windows. Para abrir el editor del Registro, vaya a Inicio > Ejecutar, escriba regedit y haga clic en Aceptar.
   1. Ir a `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Asegúrese de que el valor de EnableLUA está establecido en 0 (cero).
   1. Asegúrese de que el valor de **EnableLUA** esté establecido en 0 (cero). Si el valor no es 0, cambie el valor a 0. Cierre el Editor del Registro.

1. Reinicie el equipo.

### (Solo Windows) Deshabilitar el servicio de informes de errores {#disable-error-reporting-service}

Al convertir un documento a PDF mediante el servicio de Generador de PDF en Windows Server, ocasionalmente, Windows Server informa de que el archivo ejecutable ha encontrado un problema y debe cerrarse. Sin embargo, no afecta a la conversión de PDF, ya que continúa en segundo plano.

Para evitar recibir el error, puede deshabilitar el informe de errores de Windows. Para obtener más información sobre cómo deshabilitar los informes de errores, consulte [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx).

### (Solo Windows) Configure la conversión de HTML a PDF {#configure-html-to-pdf-conversion}

El servicio Generador de PDF proporciona rutas o métodos WebKit, WebCapture y PhantomJS para convertir archivos HTML en documentos PDF. En Windows, para habilitar la conversión para rutas WebKit y Acrobat WebCapture, copie la fuente Unicode al directorio %windir%\fonts.

>[!NOTE]
>
>Siempre que instale fuentes nuevas en la carpeta de fuentes, reinicie la instancia de AEM Forms.

### (Solo plataformas basadas en UNIX) Configuraciones adicionales para la conversión de HTML a PDF {#extra-configurations-for-html-to-pdf-conversion}

En plataformas basadas en UNIX, el servicio Generador de PDF admite rutas WebKit y PhantomJS para convertir archivos HTML en documentos PDF. Para habilitar la conversión de HTML a PDF, realice las siguientes configuraciones, según la ruta de conversión que prefiera:

### (Solo plataformas basadas en UNIX) Habilite la compatibilidad con fuentes Unicode (solo WebKit) {#enable-support-for-unicode-fonts-webkit-only}

Copie la fuente Unicode en cualquiera de los siguientes directorios según corresponda para su sistema:

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType (Solaris)

>[!NOTE]
>
>* En RedHat Enterprise Linux 6.x y versiones posteriores, las fuentes de mensajería no están disponibles. Para instalar las fuentes de mensajería, descargue el archivo font-ibm-type1-1.0.3.zip. Extraiga el archivo en /usr/share/fonts. Cree un enlace simbólico desde /usr/share/X11/fonts a /usr/share/fonts.
>* Elimine todos los archivos de caché de fuentes .lst de los directorios Html2PdfSvc/bin y /usr/share/fonts.
>* Asegúrese de que los directorios /usr/lib/X11/fonts y /usr/share/fonts existan. Si los directorios no existen, utilice el comando ln para crear un enlace simbólico de /usr/share/X11/fonts a /usr/lib/X11/fonts y otro enlace simbólico de /usr/share/fonts a /usr/share/X11/fonts. Asegúrese también de que las fuentes de mensajería estén disponibles en /usr/lib/X11/fonts.
>* Asegúrese de que todas las fuentes (Unicode y no Unicode) estén disponibles en el directorio /usr/share/fonts o /usr/share/X11/fonts.
>* Cuando ejecute el servicio de Generador de PDF como usuario no raíz, proporcione al usuario no raíz acceso de lectura y escritura a todos los directorios de fuentes.
>* Siempre que instale fuentes nuevas en la carpeta de fuentes, reinicie la instancia de AEM Forms.

>



## Instalación del paquete de complementos de AEM Forms {#install-aem-forms-add-on-package}

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. El paquete contiene AEM Forms Document Services y otras funciones de AEM Forms. Realice los siguientes pasos para instalar el paquete:

1. Abra [Distribución de software](https://experience.adobe.com/downloads). Necesitará un Adobe ID para iniciar sesión en la distribución de software.
1. Pulse **[!UICONTROL Adobe Experience Manager]**, disponible en el menú del encabezado.
1. En la sección **[!UICONTROL Filters]**:
   1. Seleccione **[!UICONTROL Forms]** en la lista desplegable **[!UICONTROL Solución]**.
   2. Seleccione la versión y el tipo del paquete. También puede utilizar la opción **[!UICONTROL Search Downloads]** para filtrar los resultados.
1. Pulse el nombre del paquete aplicable a su sistema operativo, seleccione **[!UICONTROL Aceptar términos EULA]** y pulse **[!UICONTROL Descargar]**.
1. Abra [Administrador de paquetes](https://docs.adobe.com/content/help/es-ES/experience-manager-65/administering/contentmanagement/package-manager.html) y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete.
1. Seleccione el paquete y haga clic en **[!UICONTROL Install]**.

   También puede descargar el paquete a través del enlace directo que aparece en el artículo [AEM Forms releases](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html).

1. Una vez instalado el paquete, se le pedirá que reinicie la instancia de AEM. **No detenga el servidor inmediatamente.** Antes de detener el servidor de AEM Forms, espere hasta que los mensajes ServiceEvent REGISTER y ServiceEvent UNREGISTER dejen de aparecer en el archivo  `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log y el registro sea estable.

## Configuraciones posteriores a la instalación {#post-installation-configurations}

### Configure la delegación de arranque para las bibliotecas RSA/BouncyCastle {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. Detenga la instancia de AEM. Vaya al [AEM directorio de instalación]\crx-quickstart\conf\ folder. Abra el archivo sling.properties para editarlo.

   Si utiliza `[AEM installation directory]\crx-quickstart\bin\start.bat` para iniciar una instancia de AEM, edite las propiedades sling que se encuentran en `[AEM_root]\crx-quickstart\`.

1. Agregue las siguientes propiedades al archivo sling.properties :

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. (Solo AIX) Agregue las siguientes propiedades al archivo sling.properties :

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. Guarde y cierre el archivo.

### Configuración del servicio del administrador de fuentes {#configuring-the-font-manager-service}

1. Inicie sesión en [AEM Configuration Manager](http://localhost:4502/system/console/configMgr) como administrador.
1. Busque y abra el servicio **[!UICONTROL CQ-DAM-Handler-Gibson Font Managers]**. Especifique la ruta de los directorios Fuentes del sistema, Fuentes del servidor de Adobe y Fuentes del cliente. Haga clic en **[!UICONTROL Guardar]**.

   >[!NOTE]
   >
   >Su derecho a utilizar las fuentes proporcionadas por terceros que no sean Adobes se rige por los acuerdos de licencia que estas entidades le proporcionen, y no está cubierto por su licencia para utilizar software de Adobe. Adobe recomienda revisar y asegurarse de que cumple todos los acuerdos de licencia aplicables que no sean de Adobe antes de utilizar fuentes que no sean de Adobe con software de Adobe, especialmente con respecto al uso de fuentes en un entorno de servidor.
   > Cuando instale nuevas fuentes en la carpeta de fuentes, reinicie la instancia de AEM Forms.

### Configure una cuenta de usuario local para ejecutar el servicio PDF Generator {#configure-a-local-user-account-to-run-the-pdf-generator-service}

Se necesita una cuenta de usuario local para ejecutar el servicio PDF Generator. Para ver los pasos para crear un usuario local, consulte [Crear una cuenta de usuario en Windows](https://support.microsoft.com/en-us/help/13951/windows-create-user-account) o [crear una cuenta de usuario en plataformas basadas en UNIX](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/4/html/Step_by_Step_Guide/s1-starting-create-account.html).

1. Abra la página [Configuración del generador de PDF de AEM Forms](http://localhost:4502/libs/fd/pdfg/config/ui.html).

1. En la pestaña **[!UICONTROL User Accounts]**, proporcione las credenciales de una cuenta de usuario local y haga clic en **[!UICONTROL Submit]**. Si se solicita Microsoft Windows, permita el acceso al usuario. Cuando se añade correctamente, el usuario configurado se muestra en la sección **[!UICONTROL Your user accounts]** de la pestaña **[!UICONTROL User Accounts]**.

### Configure los ajustes de tiempo de espera {#configure-the-time-out-settings}

1. En [AEM administrador de configuración](http://localhost:4502/system/console/configMgr), localice y abra el servicio **[!UICONTROL proveedor de Jacorb ORB]**.

   Agregue lo siguiente al campo **[!UICONTROL Custom Properties.name]** y haga clic en **[!UICONTROL Save]**. Establece el tiempo de espera de respuesta pendiente (también conocido como tiempo de espera de cliente CORBA) en 600 segundos.

   `jacorb.connection.client.pending_reply_timeout=600000`

1. Inicie sesión en la instancia de autor de AEM y vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Forms]** > **[!UICONTROL Configure PDF Generator]**. La dirección URL predeterminada es http://localhost:4502/libs/fd/pdfg/config/ui.html.

   Abra la pestaña **[!UICONTROL General Configuration]** y modifique el valor de los siguientes campos para su entorno:

<table> 
 <tbody> 
  <tr> 
   <td>Campo</td> 
   <td>Descripción</td> 
   <td>Valor predeterminado</td> 
  </tr> 
  <tr> 
   <td>Tiempo de espera de conversión del servidor</td> 
   <td>Una conversión PDFG permanece activa durante el número de segundos definido en el tiempo de espera de conversión del servidor</td> 
   <td>270 segundos<br /> </td> 
  </tr> 
  <tr> 
   <td>Segundos de análisis de limpieza del generador de PDF</td> 
   <td>El número de segundos necesarios para realizar operaciones posteriores a la conversión.<br /> </td> 
   <td>3600 segundos</td> 
  </tr> 
  <tr> 
   <td>Segundos de caducidad del trabajo</td> 
   <td>Duración durante la cual el servicio de Generador de PDF puede ejecutar una conversión. Asegúrese de que el valor de los segundos de caducidad del trabajo sea bueno que el valor de segundos del análisis de limpieza PDFG.</td> 
   <td>7200 segundos</td> 
  </tr> 
 </tbody> 
</table>

### (Solo Windows) Configure Acrobat para el servicio PDF Generator {#configure-acrobat-for-the-pdf-generator-service}

En Microsoft Windows, el servicio PDF Generator utiliza Adobe Acrobat para convertir los formatos de archivo admitidos a un documento PDF. Siga estos pasos para configurar Adobe Acrobat para el servicio PDF Generator:

1. Abra Acrobat y seleccione **[!UICONTROL Edit]** **[!UICONTROL Preferences]** **[!UICONTROL Updater]**. En Buscar actualizaciones, anule la selección de **[!UICONTROL Instalar automáticamente actualizaciones]** y haga clic en **[!UICONTROL Aceptar]**. Cierre Acrobat.
1. Haga doble clic en un documento PDF del sistema. Cuando Acrobat se inicia por primera vez, aparecen los cuadros de diálogo Iniciar sesión, Pantalla de bienvenida y EULA. Descartar estos cuadros de diálogo para todos los usuarios configurados para usar PDF Generator.
1. Ejecute el archivo por lotes de la utilidad PDF Generator para configurar Acrobat para el servicio PDF Generator:

   1. Abra [AEM Package Manager](http://localhost:4502/crx/packmgr/index.jsp) y descargue el archivo `adobe-aemfd-pdfg-common-pkg-[version].zip` desde el administrador de paquetes.
   1. Descomprima el archivo .zip descargado. Abra el símbolo del sistema con privilegios administrativos.
   1. Vaya al directorio `[extracted-zip-file]\jcr_root\etc\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\scripts`. Ejecute el siguiente archivo por lotes:

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat está configurado para ejecutarse con el servicio PDF Generator.

1. Ejecute la herramienta de preparación del sistema (SRT) para validar la instalación de Acrobat. La herramienta comprueba si el equipo está configurado correctamente para ejecutar conversiones de PDF Generator y genera un informe en la ruta especificada:

   1. Abra el símbolo del sistema. Vaya a la carpeta `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\etc\fd\ pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\srt` . Ejecute el siguiente comando desde el símbolo del sistema:

      `cscript SystemReadinessTool.vbs [Path_of_reports_folder] en`

      >[!NOTE]
      >
      >Si la herramienta de preparación del sistema informa de que el archivo pdfgen.api no está disponible en la carpeta de complementos de acrobat, copie el archivo pdfgen.api del directorio `[extracted-adobe-aemfd-pdfg-common-pkg]\plugins\x86_win32` al directorio `[Acrobat_root]\Acrobat\plug_ins` .

   1. Ir a `[Path_of_reports_folder]`. Abra el archivo SystemReadinessTool.html . Compruebe el informe y corrija los problemas mencionados.

### (Solo Windows) Configure la ruta principal para la conversión de HTML a PDF {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

El servicio PDF Generator ofrece varias rutas para convertir archivos HTML en documentos PDF: Webkit, Acrobat WebCapture (solo Windows) y PhantomJS. Adobe recomienda utilizar la ruta PhantomJS porque tiene la capacidad de gestionar contenido dinámico y no depende de bibliotecas de 32 bits, JDK de 32 bits o no requiere fuentes adicionales. Además, la ruta PhantomJS no requiere acceso raíz o sudo para ejecutar la conversión.

La ruta principal predeterminada para la conversión de HTML a PDF es Webkit. Para cambiar la ruta de conversión:

1. En AEM instancia de autor, vaya a **[!UICONTROL Tools]** **[!UICONTROL Forms]** **[!UICONTROL Configure PDF Generator]**.

1. En la pestaña **[!UICONTROL General Configuration]**, seleccione la ruta de conversión preferida de la lista desplegable **[!UICONTROL Primary Route for HTML to PDF conversions]**.

### Inicializar el almacén de confianza global {#intialize-global-trust-store}

Con la Administración de almacén de confianza, puede importar, editar y eliminar certificados en los que confía en el servidor para validar firmas digitales y autenticación de certificados. Puede importar y exportar cualquier número de certificados. Una vez importado un certificado, puede editar la configuración de confianza y el tipo de almacén de confianza. Realice los siguientes pasos para inicializar un almacén de confianza:

1. Inicie sesión en la instancia de AEM Forms como administrador.
1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Almacén de confianza]**.
1. Haga clic en **[!UICONTROL Crear TrustStore]**. Establezca la contraseña y pulse **[!UICONTROL Guardar]**.

### Configurar certificados para la extensión de Reader y el servicio de cifrado {#set-up-certificates-for-reader-extension-and-encryption-service}

El servicio DocAssurance puede aplicar derechos de uso a documentos PDF. Para aplicar derechos de uso a documentos PDF, configure los certificados.

Antes de configurar los certificados, asegúrese de que dispone de:

* Archivo de certificado (.pfx).

* Contraseña de clave privada proporcionada con el certificado.

* Alias de clave privada. Puede ejecutar el comando de la herramienta de teclas Java para ver el alias de la clave privada:
   `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* Contraseña del archivo del almacén de claves. Si utiliza el certificado de extensiones de Reader de Adobe, la contraseña del archivo del almacén de claves siempre es la misma que la contraseña de Clave privada.

Siga estos pasos para configurar los certificados:

1. Inicie sesión en la instancia de AEM Author como administrador. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.
1. Haga clic en el campo **[!UICONTROL name]** de la cuenta de usuario. Se abre la página **[!UICONTROL Editar configuración de usuario]**. En la instancia de AEM Author, los certificados residen en un KeyStore. Si no ha creado un almacén de claves anteriormente, haga clic en **[!UICONTROL Crear almacén de claves]** y establezca una nueva contraseña para el almacén de claves. Si el servidor ya contiene un KeyStore, omita este paso.  Si utiliza el certificado de extensiones de Reader de Adobe, la contraseña del archivo del almacén de claves siempre es la misma que la contraseña de Clave privada.
1. En la página **[!UICONTROL Editar configuración de usuario]**, seleccione la pestaña **[!UICONTROL KeyStore]**. Expanda la opción **[!UICONTROL Agregar clave privada del archivo del almacén de claves]** y proporcione un alias. El alias se utiliza para realizar la operación Extensiones de Reader.
1. Para cargar el archivo de certificado, haga clic en **[!UICONTROL Seleccionar archivo de almacén de claves]** y cargue un archivo &lt;filename>.pfx.

   Agregue la **[!UICONTROL Contraseña del almacén de claves]**, la **[!UICONTROL Contraseña de clave privada]** y el **[!UICONTROL Alias de clave privada]** asociado al certificado a los campos respectivos. Haga clic en **[!UICONTROL Submit]**.

   >[!NOTE]
   >
   >En el entorno de producción, sustituya las credenciales de evaluación por credenciales de producción. Asegúrese de eliminar las credenciales antiguas de Extensiones de Reader antes de actualizar una credencial de caducada o de evaluaciones.

1. Haga clic en **[!UICONTROL Guardar y cerrar]** en la página **[!UICONTROL Editar configuración de usuario]**.

### Habilitar AES-256 {#enable-aes}

Para utilizar el cifrado AES 256 para archivos PDF, obtenga e instale los archivos de la Extensión de criptografía Java (JCE) Unlimited Strength Jurisdiction Policy . Reemplace los archivos local_policy.jar y US_export_policy.jar en la carpeta jre/lib/security. Por ejemplo, si está utilizando Sun JDK, copie los archivos descargados en la carpeta `[JAVA_HOME]/jre/lib/security`.

El servicio Assembler depende del servicio Reader Extensions, del servicio Signature, del servicio Forms y del servicio Output. Realice los siguientes pasos para verificar que los servicios necesarios estén en funcionamiento:

1. Inicie sesión en la dirección URL `https://'[server]:[port]'/system/console/bundles` como administrador.
1. Busque el siguiente servicio y asegúrese de que los servicios estén en funcionamiento:

<table> 
 <tbody> 
  <tr> 
   <th>Nombre de servicio</th> 
   <th>Nombre de paquete</th> 
  </tr> 
  <tr> 
   <td>Servicio de firmas</td> 
   <td>adobe-aemfd-signatures</td> 
  </tr> 
  <tr> 
   <td>Reader Extensions Service</td> 
   <td>com.adobe.aemfd.adobe-aemfd-readerextensions<br /> </td> 
  </tr> 
  <tr> 
   <td>Servicio de Forms</td> 
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector<br /> </td> 
  </tr> 
  <tr> 
   <td>Servicio de salida</td> 
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector</td> 
  </tr> 
 </tbody> 
</table>

## Problemas conocidos y solución de problemas {#known-issues-and-troubleshooting}

* La conversión de HTML a PDF falla si un archivo de entrada comprimido contiene archivos HTML con caracteres de doble byte en los nombres de archivo. Para evitar este problema, no utilice caracteres de doble byte al dar nombre a archivos HTML.

* En sistemas operativos basados en UNIX, haga lo siguiente para encontrar las bibliotecas que faltan:

1. Ir a `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`.

1. Ejecute el siguiente comando para enumerar todas las bibliotecas que PhantomJS requiere para la conversión de HTML a PDF.

   `ldd phantomjs`

   Ejecute el siguiente comando para enumerar las bibliotecas que faltan.

   `ldd phantomjs | grep not`

1. Instale manualmente las bibliotecas que faltan.

## Pasos siguientes {#next-steps}

Tiene un entorno de AEM Forms document services en funcionamiento. Puede utilizar document services mediante:

* [Flujos de trabajo centrados en formularios en OSGi](/help/forms/using/aem-forms-workflow.md)
* [Carpetas inspeccionadas](/help/forms/using/watched-folder-in-aem-forms.md)
* [API de servicios de documentos](/help/forms/using/aem-document-services-programmatically.md)

