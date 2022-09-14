---
title: Instalación y configuración de document services
seo-title: Installing and configuring document services
description: Instale AEM Forms document services para crear, ensamblar, distribuir, archivar documentos PDF, agregar firmas digitales para limitar el acceso a los documentos y descodificar Forms codificado por barras.
seo-description: Install AEM Forms document services to create, assemble, distribute, archive PDF documents, add digital signatures to limit access to documents, and decode barcoded forms.
uuid: 908806a9-b0d4-42d3-9fe4-3eae44cf4326
topic-tags: installing
discoiquuid: b53eae8c-16ba-47e7-9421-7c33e141d268
role: Admin
exl-id: 5d48e987-16c2-434b-8039-c82181d2e028
source-git-commit: 32b97aeff398a19556d46ff6c905dc3019988bc1
workflow-type: tm+mt
source-wordcount: '5389'
ht-degree: 2%

---

# Instalación y configuración de document services {#installing-and-configuring-document-services}

AEM Forms proporciona un conjunto de servicios OSGi para realizar distintas operaciones a nivel de documento, por ejemplo, servicios para crear, ensamblar, distribuir y archivar documentos PDF, agregar firmas digitales para limitar el acceso a documentos y descodificar Forms codificado por barras. Estos servicios se incluyen en el paquete de complementos de AEM Forms. En conjunto, estos servicios se conocen como servicios de documentos. La lista de servicios de documentos disponibles y sus principales funciones es la siguiente:

* **Servicio del ensamblador:** Permite combinar, reorganizar y aumentar documentos de PDF y XDP y obtener información sobre documentos de PDF. También ayuda a convertir y validar documentos de PDF a estándar de PDF/A, transforma PDF forms, formularios XML y PDF forms a PDF/A-1b, PDF/A-2b y PDFA/A-3b. Para obtener más información, consulte [Servicio del ensamblador](/help/forms/using/assembler-service.md).

* **Servicio ConvertPDF:** Permite convertir documentos de PDF a archivos PostScript o de imagen (JPEG, JPEG 2000, PNG y TIFF). Para obtener más información, consulte [Servicio ConvertPDF](/help/forms/using/using-convertpdf-service.md).

* **Servicio de Forms con códigos de barras:** Permite extraer datos de imágenes electrónicas de códigos de barras. El servicio acepta archivos de TIFF y PDF que incluyen uno o más códigos de barras como entrada y extrae los datos del código de barras. Para obtener más información, consulte [Servicio de Forms con códigos de barras](/help/forms/using/using-barcoded-forms-service.md).

* **Servicio DocAssurance:** Permite cifrar y descifrar documentos, ampliar la funcionalidad de Adobe Reader con derechos de uso adicionales y agregar firmas digitales a los documentos. El servicio Doc Assurance contiene tres servicios: firma, cifrado y extensión de lector. Para obtener más información, consulte [Servicio DocAssurance](/help/forms/using/overview-aem-document-services.md).

* **Servicio de cifrado:** Permite cifrar y descifrar documentos. Cuando se cifra un documento, su contenido se vuelve ilegible. Un usuario autorizado puede descifrar el documento para obtener acceso a su contenido. Para obtener más información, consulte [Servicio de cifrado](/help/forms/using/overview-aem-document-services.md#encryption-service).

* **Servicio de Forms:** Permite crear aplicaciones de cliente de captura de datos interactivas que validen, procesan, transforman y entregan formularios que normalmente se crean en Forms Designer. El servicio Forms procesa cualquier diseño de formulario que desarrolle en documentos de PDF. Para obtener más información, consulte [Servicio de Forms](/help/forms/using/forms-service.md).

* **Servicio de salida:** Permite crear documentos en diferentes formatos, incluidos PDF, formatos de impresora láser y formatos de impresora de etiquetas. Los formatos de impresora láser son PostScript y Printer Control Language (PCL). Para obtener más información, consulte [Servicio de salida](/help/forms/using/output-service.md).

* **Servicio Generador de PDF:** El servicio Generador de PDF proporciona API para convertir formatos de archivo nativos a PDF. También convierte el PDF a otros formatos de archivo y optimiza el tamaño de los documentos del PDF. Para obtener más información, consulte [PDF Generator Service](aem-document-services-programmatically.md#pdfgeneratorservice).

* **Servicio de extensión del Reader:** Permite a su organización compartir fácilmente documentos de PDF interactivos mediante la ampliación de la funcionalidad de Adobe Reader con derechos de uso adicionales. El servicio activa funciones que no están disponibles cuando se abre un documento de PDF con Adobe Reader, como agregar comentarios a un documento, rellenar formularios y guardar el documento. Para obtener más información, consulte [Servicio de extensión de Reader](/help/forms/using/overview-aem-document-services.md#reader-extension-service).

* **Servicio de firmas:** Permite trabajar con firmas digitales y documentos en el servidor de AEM. Por ejemplo, el servicio de firma se suele utilizar en las siguientes situaciones:

   * El servidor de AEM certifica un formulario antes de enviarlo a un usuario para que lo abra con Acrobat o Adobe Reader.
   * El servidor de AEM valida una firma que se agregó a un formulario mediante Acrobat o Adobe Reader.
   * El servidor de AEM firma un formulario en nombre de un notario público.

   El servicio de firma accede a los certificados y credenciales almacenados en el almacén de confianza. Para obtener más información, consulte [Servicio de firmas](/help/forms/using/aem-document-services-programmatically.md).

AEM Forms es una potente plataforma de clase empresarial y document services es solo una de las capacidades de AEM Forms. Para obtener la lista completa de funcionalidades, consulte [Introducción a AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topología de implementación {#deployment-topology}

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. Por lo general, solo se necesita una instancia de AEM (autor o publicación) para ejecutar AEM Forms document services. Se recomienda la siguiente topología para ejecutar AEM Forms document services. Para obtener información detallada sobre topologías, consulte [Arquitectura y topologías de implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![Arquitectura y topologías de implementación para AEM Forms](do-not-localize/document-services.png)

>[!NOTE]
>
>Aunque AEM Forms le permite configurar y ejecutar todas las funcionalidades desde un solo servidor, debe planificar la capacidad, equilibrar la carga y configurar servidores dedicados para funcionalidades específicas en un entorno de producción. Por ejemplo, para un entorno que utiliza el servicio Generador de PDF para convertir miles de páginas al día y varios formularios adaptables para capturar datos, configure servidores AEM Forms independientes para el servicio Generador de PDF y las funcionalidades de formularios adaptables. Ayuda a proporcionar un rendimiento óptimo y a escalar los servidores de forma independiente entre sí.

## Requisitos del sistema {#system-requirements}

Antes de empezar a instalar y configurar AEM Forms document services, asegúrese de que:

* La infraestructura de hardware y software está implementada. Para obtener una lista detallada del hardware y software compatibles, consulte [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

* La ruta de instalación de la instancia de AEM no contiene espacios en blanco.
* Se está ejecutando una instancia de AEM. En AEM terminología, una &quot;instancia&quot; es una copia de AEM que se ejecuta en un servidor en modo de autor o publicación. Por lo general, solo necesita una instancia de AEM (autor o publicación) para ejecutar AEM Forms document services:

   * **Autor**: Instancia de AEM utilizada para crear, cargar y editar contenido y para administrar el sitio web. Una vez que el contenido está listo para su lanzamiento, se duplica en la instancia de publicación.
   * **Publicación**: Instancia de AEM que sirve el contenido publicado al público a través de Internet o una red interna.

* Se cumplen los requisitos de memoria. El paquete de complementos de AEM Forms requiere:

   * 15 GB de espacio temporal para instalaciones basadas en Microsoft® Windows.
   * 6 GB de espacio temporal para instalaciones basadas en UNIX.

* El software cliente necesario para que el generador de PDF realice la conversión en Microsoft® Windows y Linux® está instalado:

   * **Microsoft® Windows**: Instalar [Microsoft® Office](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p) o [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux®**: Instalar [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* En Microsoft® Windows, el Generador de PDF admite las rutas de conversión WebKit, Acrobat WebCapture y PhantomJS para convertir archivos HTML en documentos PDF.
>* En sistemas operativos basados en UNIX, el Generador de PDF admite rutas de conversión de WebKit y PhantomJS para convertir archivos HTML en documentos PDF.
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

* **(solo generador de PDF)**) Instale la versión de 32 bits de las bibliotecas libcurl, libcrypto y libssl y cree los siguientes enlaces simbólicos. Los enlaces simbólicos señalan a la última versión de las bibliotecas respectivas:

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **(solo generador de PDF)** El servicio Generador de PDF admite rutas WebKit y PhantomJS para convertir archivos HTML a documentos PDF. Para habilitar la conversión para la ruta PhantomJS, instale las bibliotecas de 64 bits que se enumeran a continuación. Por lo general, estas bibliotecas ya están instaladas. Si falta alguna biblioteca, instálela manualmente:

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

## Configuraciones previas a la instalación {#preinstallationconfigurations}

Las configuraciones enumeradas en la sección de configuraciones previas a la instalación solo se aplican al servicio Generador de PDF. Si no está configurando el servicio Generador de PDF, puede omitir la sección de configuración previa a la instalación.

### Instalación de Adobe Acrobat y aplicaciones de terceros {#install-adobe-acrobat-and-third-party-applications}

Si va a usar el servicio Generador de PDF para convertir formatos de archivo nativos como Microsoft® Word, Microsoft® Excel, Microsoft® PowerPoint, OpenOffice, WordPerfect X7 y Adobe Acrobat a documentos PDF, asegúrese de que estas aplicaciones estén instaladas en el servidor AEM Forms.

>[!NOTE]
>
>* Si el servidor de AEM Forms se encuentra en un entorno sin conexión o seguro y Internet no está disponible para activar Adobe Acrobat, consulte [Activación sin conexión](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en) para obtener instrucciones para activar estas instancias de Adobe Acrobat.
>* Adobe Acrobat, Microsoft® Word, Excel y Powerpoint solo están disponibles para Microsoft® Windows. Si está utilizando el sistema operativo basado en UNIX, instale OpenOffice para convertir archivos de texto enriquecido y archivos compatibles de Microsoft® Office a documentos de PDF.
>* Descarte todos los cuadros de diálogo que se muestran después de instalar Adobe Acrobat y software de terceros para todos los usuarios configurados para utilizar el servicio Generador de PDF.
>* Inicie todo el software instalado al menos una vez. Descartar todos los cuadros de diálogo de todos los usuarios configurados para utilizar el servicio Generador de PDF.
>* [Comprobar la fecha de caducidad de sus números de serie de Adobe Acrobat](https://helpx.adobe.com/enterprise/kb/volume-license-expiration-check.html) y establecer una fecha para actualizar la licencia o [migrar su número de serie](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) en función de la fecha de caducidad.


Después de instalar Acrobat, abra Microsoft® Word. En el **Acrobat** , haga clic en **Crear PDF** y convertir un archivo .doc o .docx disponible en su equipo a un documento PDF. Si la conversión se realiza correctamente, AEM Forms está listo para usar Acrobat con el servicio Generador de PDF.

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
>* No configure variables de entorno para aplicaciones de Microsoft® Office como Word, PowerPoint, Excel y Project, o para AutoCAD. Si estas aplicaciones están instaladas en el servidor, el servicio Generate PDF inicia automáticamente estas aplicaciones.
>* En plataformas basadas en UNIX, instale OpenOffice como /root. Si OpenOffice no está instalado como raíz, el servicio Generador de PDF no convierte los documentos de OpenOffice en documentos PDF. Si necesita instalar y ejecutar OpenOffice como un usuario no raíz, proporcione derechos de sudo al usuario no raíz.
>* Si está utilizando OpenOffice en una plataforma basada en UNIX, ejecute el siguiente comando para configurar la variable path:
>
> `export OpenOffice_PATH=/opt/openoffice.org4`

### (Solo para IBM® WebSphere®) Configure el proveedor de sockets IBM® SSL {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

Realice los siguientes pasos para configurar el proveedor de sockets IBM® SSL:

1. Cree una copia del archivo java.security. La ubicación predeterminada del archivo es `[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`.
1. Abra el archivo java.security copiado para editarlo.
1. Cambie las fábricas de socket SSL predeterminadas para utilizar las fábricas JSSE2 en lugar de las fábricas IBM® WebSphere® predeterminadas:

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

1. Para permitir que AEM Forms Server use el archivo java.security actualizado, al iniciar el servidor AEM Forms, agregue el siguiente argumento java:

   `-Djava.security.properties= [path of newly created Java.security file].`

### (Solo Windows) Configurar el servicio Instalar tinta y escritura a mano {#configure-install-ink-and-handwriting-service}

Si está ejecutando Microsoft® Windows Server, configure el servicio de tinta y escritura a mano. El servicio es necesario para abrir archivos de Microsoft® PowerPoint que utilizan funciones de vinculación de Microsoft® Office:

1. Abra el Administrador de servidores. Haga clic en el **[!UICONTROL Administrador del servidor]** en la bandeja de inicio rápido.
1. Haga clic en **[!UICONTROL Agregar características]** en el **[!UICONTROL Funciones]** para abrir el Navegador. Seleccione el **[!UICONTROL Servicios de escritura a mano y tinta]** en el Navegador.
1. **[!UICONTROL Seleccionar características]** cuadro de diálogo con **[!UICONTROL Servicios de escritura a mano y tinta]** seleccionados. Haga clic en **[!UICONTROL Instalar]** y el servicio está instalado.

### (Solo Windows) Configure las opciones del bloque de archivos para Microsoft® Office {#configure-the-file-block-settings-for-microsoft-office}

Cambie la configuración del centro de confianza de Microsoft® Office para permitir que el servicio Generador de PDF convierta archivos creados con versiones anteriores de Microsoft® Office.

1. Abra una aplicación de Microsoft® Office. Por ejemplo, Microsoft® Word. Vaya a **[!UICONTROL Archivo]**> **[!UICONTROL Opciones]**. Aparecerá el cuadro de diálogo de opciones.

1. Haga clic en **[!UICONTROL Centro de confianza]** y haga clic en **[!UICONTROL Configuración del centro de confianza]**.
1. En el **[!UICONTROL Configuración del Centro de confianza]**, haga clic en **[!UICONTROL Configuración de bloque de archivos]**.
1. En el **[!UICONTROL Tipo de archivo]** lista, anular selección **[!UICONTROL Apertura]** para el tipo de archivo que debe permitirse al servicio Generador de PDF convertir en documentos PDF.

### (Solo Windows) Conceder el privilegio Replace a process level token {#grant-the-replace-a-process-level-token-privilege}

La cuenta de usuario utilizada para iniciar el servidor de aplicaciones requiere la variable **Reemplazar un token de nivel de proceso** . La cuenta del sistema local tiene la variable **Reemplazar un token de nivel de proceso** de forma predeterminada. Para los servidores que se ejecutan con un usuario del grupo Administradores locales, el privilegio debe otorgarse explícitamente. Siga estos pasos para conceder el privilegio:

1. Abra el Editor de directivas de grupo para Microsoft® Windows. Para abrir el Editor de directivas de grupo, haga clic en **[!UICONTROL Inicio]**, tipo **gpedit.msc** en el cuadro Iniciar búsqueda y haga clic en **[!UICONTROL Editor de directivas de grupo]**.
1. Vaya a **[!UICONTROL Política de equipo local]** > **[!UICONTROL Configuración del equipo]** > **[!UICONTROL Configuración de Windows]** > **[!UICONTROL Configuración de seguridad]** > **[!UICONTROL Políticas locales]** > **[!UICONTROL Asignación de derechos de usuario]** y edite el **[!UICONTROL Reemplazar un token de nivel de proceso]** e incluya el grupo Administradores.
1. Agregue el usuario a la entrada Reemplazar un token de nivel de proceso .

### (Solo Windows) Habilite el servicio Generador de PDF para usuarios que no sean administradores {#enable-the-pdf-generator-service-for-non-administrators}

Puede habilitar a un usuario que no sea administrador para que utilice el servicio Generador de PDF. Normalmente, solo los usuarios con privilegios administrativos pueden utilizar el servicio:

1. Cree una variable de entorno, PDFG_NON_ADMIN_ENABLED.
1. Establezca el valor de la variable de entorno en TRUE.
1. Reinicie la instancia de AEM Forms.

### (Solo Windows) Deshabilitar el control de cuentas de usuario (UAC) {#disable-user-account-control-uac}

1. Para acceder a la Utilidad de configuración del sistema, vaya a **[!UICONTROL Inicio > Ejecutar]** y, a continuación, introduzca **[!UICONTROL MSCONFIG]**.
1. Haga clic en el **[!UICONTROL Herramientas]** desplácese hacia abajo y seleccione **[!UICONTROL Cambiar configuración de UAC]**. Haga clic en **[!UICONTROL Launch]** para ejecutar el comando en una nueva ventana.
1. Ajuste el control deslizante al nivel No notificar nunca. Cuando termine, cierre la ventana de comandos y cierre la ventana Configuración del sistema.
1. Compruebe que la configuración del Registro para UAC está establecida en 0 (cero). Siga estos pasos para verificar:

   1. Microsoft® recomienda realizar una copia de seguridad del registro antes de modificarlo. Para ver los pasos detallados, consulte [Cómo realizar una copia de seguridad y restaurar el Registro en Windows](https://support.microsoft.com/en-us/help/322756).
   1. Abra el editor del Registro de Windows de Microsoft®. Para abrir el editor del Registro, vaya a Inicio > Ejecutar, escriba regedit y haga clic en Aceptar.
   1. Vaya a `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Asegúrese de que el valor de EnableLUA está establecido en 0 (cero).
   1. Garantizar el valor de **EnableLUA** se establece en 0 (cero). Si el valor no es 0, cambie el valor a 0. Cierre el Editor del Registro.

1. Reinicie el equipo.

### (Solo Windows) Deshabilitar el servicio de informes de errores {#disable-error-reporting-service}

Al convertir un documento a PDF mediante el servicio Generador de PDF en Windows Server, ocasionalmente Windows Server informa de que el archivo ejecutable ha encontrado un problema y debe cerrarse. Sin embargo, no afecta a la conversión del PDF, ya que continúa en segundo plano.

Para evitar recibir el error, puede deshabilitar el informe de errores de Windows. Para obtener más información sobre cómo deshabilitar los informes de errores, consulte [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx).

### (Solo Windows) Configurar la conversión de HTML a PDF {#configure-html-to-pdf-conversion}

El servicio Generador de PDF proporciona rutas o métodos WebKit, WebCapture y PhantomJS para convertir archivos HTML en documentos PDF. En Windows, para habilitar la conversión para rutas WebKit y Acrobat WebCapture, copie la fuente Unicode al directorio %windir%\fonts.

>[!NOTE]
>
>Siempre que instale fuentes nuevas en la carpeta de fuentes, reinicie la instancia de AEM Forms.

### (Solo plataformas basadas en UNIX) Configuraciones adicionales para la conversión de HTML a PDF  {#extra-configurations-for-html-to-pdf-conversion}

En plataformas basadas en UNIX, el servicio Generador de PDF admite rutas WebKit y PhantomJS para convertir archivos HTML en documentos PDF. Para habilitar la conversión de HTML a PDF, realice las siguientes configuraciones, según la ruta de conversión que prefiera:

### (Solo plataformas basadas en UNIX) Habilitar la compatibilidad con fuentes Unicode (solo WebKit) {#enable-support-for-unicode-fonts-webkit-only}

Copie la fuente Unicode en cualquiera de los siguientes directorios según corresponda para su sistema:

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType (Solaris™)

>[!NOTE]
>
>* En Red Hat® Enterprise Linux® 6.x y versiones posteriores, las fuentes de mensajería no están disponibles. Para instalar las fuentes de mensajería, descargue el archivo font-ibm-type1-1.0.3.zip. Extraiga el archivo en /usr/share/fonts. Cree un enlace simbólico desde /usr/share/X11/fonts a /usr/share/fonts.
>* Elimine todos los archivos de caché de fuentes .lst de los directorios Html2PdfSvc/bin y /usr/share/fonts.
>* Asegúrese de que los directorios /usr/lib/X11/fonts y /usr/share/fonts existan. Si los directorios no existen, utilice el comando ln para crear un enlace simbólico de /usr/share/X11/fonts a /usr/lib/X11/fonts y otro enlace simbólico de /usr/share/fonts a /usr/share/X11/fonts. Asegúrese también de que las fuentes de mensajería estén disponibles en /usr/lib/X11/fonts.
>* Asegúrese de que todas las fuentes (Unicode y no Unicode) estén disponibles en el directorio /usr/share/fonts o /usr/share/X11/fonts.
>* Cuando ejecute el servicio Generador de PDF como usuario no raíz, proporcione al usuario no raíz acceso de lectura y escritura a todos los directorios de fuentes.
>* Siempre que instale fuentes nuevas en la carpeta de fuentes, reinicie la instancia de AEM Forms.
>


## Instalación del paquete de complementos de AEM Forms {#install-aem-forms-add-on-package}

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. El paquete contiene AEM Forms Document Services y otras funciones de AEM Forms. Realice los siguientes pasos para instalar el paquete:

1. Abra [Distribución de software](https://experience.adobe.com/downloads). Necesitará un Adobe ID para iniciar sesión en la distribución de software.
1. Pulse **[!UICONTROL Adobe Experience Manager]**, disponible en el menú del encabezado.
1. En el **[!UICONTROL Filtros]** sección:
   1. Select **[!UICONTROL Forms]** de la variable **[!UICONTROL Solución]** lista desplegable.
   2. Seleccione la versión y el tipo del paquete. También puede usar la variable **[!UICONTROL Descargas de búsqueda]** para filtrar los resultados.
1. Pulse el nombre del paquete aplicable a su sistema operativo, seleccione **[!UICONTROL Aceptar términos de EULA]** y toque **[!UICONTROL Descargar]**.
1. Abra [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es) y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete.
1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

   También puede descargar el paquete a través del vínculo directo enumerado en la [Versiones de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) artículo.

1. Una vez instalado el paquete, se le pedirá que reinicie la instancia de AEM. **No detenga el servidor inmediatamente.** Antes de detener el servidor de AEM Forms, espere hasta que los mensajes ServiceEvent REGISTER y ServiceEvent UNREGISTER dejen de aparecer en la variable `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log y el registro es estable.

## Configuraciones posteriores a la instalación {#post-installation-configurations}

### Configuración de la delegación de arranque para bibliotecas RSA/BouncyCastle  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. Detenga la instancia de AEM. Vaya a la [directorio de instalación de AEM]\crx-quickstart\conf\ folder. Abra el archivo sling.properties para editarlo.

   Si usa `[AEM installation directory]\crx-quickstart\bin\start.bat` para iniciar una instancia de AEM, edite sling.properties ubicada en `[AEM_root]\crx-quickstart\`.

1. Agregue las siguientes propiedades al archivo sling.properties :

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. (Solo AIX®) Agregue las siguientes propiedades al archivo sling.properties :

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. Guarde y cierre el archivo.

### Configuración del servicio del administrador de fuentes  {#configuring-the-font-manager-service}

1. Iniciar sesión en [Administrador de configuración de AEM](http://localhost:4502/system/console/configMgr) como administrador.
1. Busque y abra el **[!UICONTROL Gestores de fuentes CQ-DAM-Handler-Gibson]** servicio. Especifique la ruta de los directorios Fuentes del sistema, Fuentes del servidor de Adobe y Fuentes del cliente. Haga clic en **[!UICONTROL Guardar]**.

   >[!NOTE]
   >
   >Su derecho a utilizar las fuentes proporcionadas por terceros que no sean Adobes se rige por los acuerdos de licencia que estas entidades le proporcionen, y no está cubierto por su licencia para utilizar software de Adobe. Adobe recomienda revisar y asegurarse de que cumple todos los acuerdos de licencia aplicables que no sean de Adobe antes de utilizar fuentes que no sean de Adobe con software de Adobe, especialmente en lo que respecta al uso de fuentes en un entorno de servidor.
   > Cuando instale nuevas fuentes en la carpeta de fuentes, reinicie la instancia de AEM Forms.

### Configuración de una cuenta de usuario local para ejecutar el servicio Generador de PDF  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

Se necesita una cuenta de usuario local para ejecutar el servicio Generador de PDF. Para ver los pasos para crear un usuario local, consulte [Crear una cuenta de usuario en Windows](https://support.microsoft.com/en-us/help/13951/windows-create-user-account) o crear una cuenta de usuario en plataformas basadas en UNIX.

1. Abra el [Configuración del Generador de PDF de AEM Forms](http://localhost:4502/libs/fd/pdfg/config/ui.html) página.

1. En el **[!UICONTROL Cuentas de usuario]** , proporcione las credenciales de una cuenta de usuario local y haga clic en **[!UICONTROL Submit]**. Si Microsoft® Windows se solicita, permita el acceso al usuario. Cuando se añade correctamente, el usuario configurado se muestra en la sección **[!UICONTROL Sus cuentas de usuario]** en la sección **[!UICONTROL Cuentas de usuario]** pestaña .

### Configuración de la configuración de tiempo de espera {#configure-the-time-out-settings}

1. En [Administrador de configuración de AEM](http://localhost:4502/system/console/configMgr), busque y abra el **[!UICONTROL Proveedor de Jacorb ORB]** servicio.

   Agregue lo siguiente a **[!UICONTROL Propiedades personalizadas.name]** y haga clic en **[!UICONTROL Guardar]**. Establece el tiempo de espera de respuesta pendiente (también conocido como tiempo de espera de cliente CORBA) en 600 segundos.

   `jacorb.connection.client.pending_reply_timeout=600000`

1. Inicie sesión en la instancia de autor de AEM y vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Herramientas]** > **[!UICONTROL Forms]** > **[!UICONTROL Configuración del Generador de PDF]**. La dirección URL predeterminada es <http://localhost:4502/libs/fd/pdfg/config/ui.html>.

   Abra el **[!UICONTROL Configuración general]** y modifique el valor de los campos siguientes para su entorno:

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
   <td>Número de segundos necesarios para realizar operaciones posteriores a la conversión.<br /> </td>
   <td>3600 segundos</td>
  </tr>
  <tr>
   <td>Segundos de caducidad del trabajo</td>
   <td>Duración durante la cual el servicio de Generador de PDF puede ejecutar una conversión. Asegúrese de que el valor de los segundos de caducidad del trabajo sea bueno que el valor de segundos del análisis de limpieza PDFG.</td>
   <td>7200 segundos</td>
  </tr>
 </tbody>
</table>

### (Solo Windows) Configurar Acrobat para el servicio Generador de PDF {#configure-acrobat-for-the-pdf-generator-service}

En Microsoft® Windows, el servicio Generador de PDF utiliza Adobe Acrobat para convertir los formatos de archivo admitidos a un documento PDF. Siga estos pasos para configurar Adobe Acrobat para el servicio Generador de PDF:

1. Abra Acrobat y seleccione **[!UICONTROL Editar]**> **[!UICONTROL Preferencias]**> **[!UICONTROL Actualizador]**. En Buscar actualizaciones, anule la selección **[!UICONTROL Instalar actualizaciones automáticamente]** y haga clic en **[!UICONTROL OK]**. Cierre Acrobat.
1. Haga doble clic en un documento PDF del sistema. Cuando Acrobat se inicia por primera vez, aparecen los cuadros de diálogo Iniciar sesión, Pantalla de bienvenida y EULA. Descartar estos cuadros de diálogo para todos los usuarios configurados para usar el Generador de PDF.
1. Ejecute el archivo por lotes de la utilidad Generador de PDF para configurar Acrobat para el servicio Generador de PDF:

   1. Apertura [Administrador de paquetes AEM](http://localhost:4502/crx/packmgr/index.jsp) y descargue el `adobe-aemfd-pdfg-common-pkg-[version].zip` del Administrador de paquetes.
   1. Descomprima el archivo .zip descargado. Abra el símbolo del sistema con privilegios administrativos.
   1. Vaya a la [extracted-zip-file]`\jcr_root\etc\packages\day\cq60\fd\adobe-aemds-common-pkg-[version]\jcr_root\etc\packages\day\cq60\fd\adobe-aemfd-pdfg-common-pkg-[version]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]` directorio. Ejecute el siguiente archivo por lotes:

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat está configurado para ejecutarse con el servicio Generador de PDF.

1. Ejecutar [Herramienta de preparación del sistema (SRT)](#SRT) para validar la instalación de Acrobat.

### (Solo Windows) Configure la ruta principal para la conversión de HTML a PDF {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

El servicio Generador de PDF ofrece varias rutas para convertir archivos HTML en documentos PDF: Webkit, Acrobat WebCapture (solo Windows) y PhantomJS. Adobe recomienda utilizar la ruta PhantomJS porque tiene la capacidad de gestionar contenido dinámico y no depende de bibliotecas de 32 bits, JDK de 32 bits o no requiere fuentes adicionales. Además, la ruta PhantomJS no requiere acceso raíz o sudo para ejecutar la conversión.

La ruta principal predeterminada para la conversión de HTML a PDF es Webkit. Para cambiar la ruta de conversión:

1. En AEM instancia de autor, vaya a **[!UICONTROL Herramientas]**> **[!UICONTROL Forms]**> **[!UICONTROL Configuración del Generador de PDF]**.

1. En el **[!UICONTROL Configuración general]** seleccione la ruta de conversión preferida en la pestaña **[!UICONTROL Ruta principal para conversiones de HTML a PDF]** lista desplegable.

### Inicializar el almacén de confianza global {#intialize-global-trust-store}

Con la Administración de almacén de confianza, puede importar, editar y eliminar certificados en los que confía en el servidor para validar firmas digitales y autenticación de certificados. Puede importar y exportar cualquier número de certificados. Una vez importado un certificado, puede editar la configuración de confianza y el tipo de almacén de confianza. Realice los siguientes pasos para inicializar un almacén de confianza:

1. Inicie sesión en la instancia de AEM Forms como administrador.
1. Vaya a  **[!UICONTROL Herramientas]** >  **[!UICONTROL Seguridad]** >  **[!UICONTROL Almacén de confianza]**.
1. Haga clic en  **[!UICONTROL Crear TrustStore]**. Establecer contraseña y pulsar **[!UICONTROL Guardar]**.

### Configuración de certificados para el servicio de cifrado y extensión del Reader {#set-up-certificates-for-reader-extension-and-encryption-service}

El servicio DocAssurance puede aplicar derechos de uso a documentos del PDF. Para aplicar derechos de uso a documentos de PDF, configure los certificados.

Antes de configurar los certificados, asegúrese de que dispone de:

* Archivo de certificado (.pfx).

* Contraseña de clave privada proporcionada con el certificado.

* Alias de clave privada. Puede ejecutar el comando de la herramienta de teclas Java para ver el alias de la clave privada:
   `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* Contraseña del archivo del almacén de claves. Si utiliza el certificado de extensiones de Reader de Adobe, la contraseña del archivo del almacén de claves siempre es la misma que la contraseña de Clave privada.

Siga estos pasos para configurar los certificados:

1. Inicie sesión en la instancia de AEM Author como administrador. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.
1. Haga clic en el **[!UICONTROL name]** de la cuenta de usuario. La variable **[!UICONTROL Editar configuración de usuario]** se abre. En la instancia de AEM Author, los certificados residen en un KeyStore. Si no ha creado un almacén de claves anteriormente, haga clic en **[!UICONTROL Crear KeyStore]** y establezca una nueva contraseña para KeyStore. Si el servidor ya contiene un KeyStore, omita este paso.  Si utiliza el certificado de extensiones de Reader de Adobe, la contraseña del archivo del almacén de claves siempre es la misma que la contraseña de Clave privada.
1. En el **[!UICONTROL Editar configuración de usuario]** seleccione **[!UICONTROL KeyStore]** pestaña . Expanda el **[!UICONTROL Añadir clave privada del archivo del almacén de claves]** y proporcione un alias. El alias se utiliza para realizar la operación Extensiones de Reader.
1. Para cargar el archivo de certificado, haga clic en **[!UICONTROL Seleccionar archivo de almacén de claves]** y cargue un &lt;filename>archivo .pfx.

   Agregue la variable **[!UICONTROL Contraseña del almacén de claves]**, **[!UICONTROL Contraseña de clave privada]** y **[!UICONTROL Alias de clave privada]** que está asociado con el certificado a los campos respectivos. Haga clic en **[!UICONTROL Submit]**.

   >[!NOTE]
   >
   >En el entorno de producción, sustituya las credenciales de evaluación por credenciales de producción. Asegúrese de eliminar las credenciales antiguas de Extensiones de Reader antes de actualizar una credencial de caducada o de evaluaciones.

1. Haga clic en **[!UICONTROL Guardar y cerrar]** en el **[!UICONTROL Editar configuración de usuario]** página.

### Habilitar AES-256 {#enable-aes}

Para utilizar el cifrado AES 256 para archivos PDF, obtenga e instale los archivos de la Extensión de cifrado de Java (JCE) de directivas de jurisdicción de fuerza ilimitada (Unlimited Strength Jurisdiction. Reemplace los archivos local_policy.jar y US_export_policy.jar en la carpeta jre/lib/security. Por ejemplo, si está utilizando Sun JDK, copie los archivos descargados en el `[JAVA_HOME]/jre/lib/security` carpeta.

El servicio Assembler depende del servicio Reader Extensions, del servicio Signature, del servicio Forms y del servicio Output. Realice los siguientes pasos para verificar que los servicios necesarios estén en funcionamiento:

1. Iniciar sesión en la dirección URL `https://'[server]:[port]'/system/console/bundles` como administrador.
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

* La conversión de HTML a PDF falla si un archivo de entrada comprimido contiene archivos HTML con caracteres de doble byte en los nombres de archivo. Para evitar este problema, no utilice caracteres de doble byte al dar nombre a los archivos HTML.

* En sistemas operativos basados en UNIX, haga lo siguiente para encontrar las bibliotecas que faltan:

1. Vaya a `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`.

1. Ejecute el siguiente comando para enumerar todas las bibliotecas que PhantomJS requiere para la conversión de HTML a PDF.

   `ldd phantomjs`

   Ejecute el siguiente comando para enumerar las bibliotecas que faltan.

   `ldd phantomjs | grep not`

1. Instale manualmente las bibliotecas que faltan.

## Herramienta de preparación del sistema (SRT) {#SRT}

La herramienta de preparación del sistema comprueba si el equipo está configurado correctamente para ejecutar las conversiones del Generador de PDF. La herramienta genera el informe en la ruta especificada. Para ejecutar la herramienta:

1. Abra el símbolo del sistema. Vaya a la `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools` carpeta.

1. Ejecute el siguiente comando desde el símbolo del sistema:

   `java -jar forms-srt-[version].jar [Path_of_reports_folder] en`

   El comando genera el informe y también crea el archivo srt_config.yaml.

   >[!NOTE]
   >
   > * Si la herramienta de preparación del sistema informa de que el archivo pdfgen.api no está disponible en la carpeta de complementos de Acrobat, copie el archivo pdfgen.api de la `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]\plugins\x86_win32` para `[Acrobat_root]\Acrobat\plug_ins` directorio.
   >
   > * Puede utilizar el archivo srt_config.yaml para configurar varias configuraciones de . El formato del archivo es:


   ```
      # =================================================================
      # SRT Configuration
      # =================================================================
      #Note - follow correct format to avoid parsing failures
      #e.g. <param name>:<space><param value> 
      #locale: (mandatory field)Locale to be used for SRT. Supported locales [en/fr/de/ja].
      locale: en
   
      #aemTempDir: AEM Temp direcotry
      aemTempDir:
   
      #users: provide PDFG converting users list
      #users:
      # - user1
      # - user2
      users:
   
      #profile: select profile to run specific checks. Choose from [LCM], more will be added soon 
      profile:
   
      #outputDir: directory where output files will be saved
      outputDir:
   ```

1. Vaya a `[Path_of_reports_folder]`. Abra el archivo SystemReadinessTool.html . Compruebe el informe y corrija los problemas mencionados.

## Solución de problemas

Si tiene problemas incluso después de corregir todos los problemas notificados por la herramienta SRT, realice las siguientes comprobaciones:

Antes de realizar las siguientes comprobaciones, asegúrese de que [Herramienta de preparación del sistema](#SRT) no informa de ningún error.

+++ Adobe Acrobat

* Asegúrese de que [versión compatible](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) de Microsoft® Office (32 bits) y Adobe Acrobat están instalados y los cuadros de diálogo de apertura se cancelan.
* Asegúrese de que Adobe Acrobat Update Service esté deshabilitado.
* Asegúrese de que la variable [Acrobat_for_PDFG_Configuration.bat](#configure-acrobat-for-the-pdf-generator-service) el archivo por lotes se ejecutó con privilegios de administrador.
* Asegúrese de que se agrega un usuario de Generador de PDF en la interfaz de usuario de configuración del PDF.
* Asegúrese de que la variable [Reemplazar un token de nivel de proceso](#grant-the-replace-a-process-level-token-privilege) se agrega para el usuario de Generador de PDF.
* Asegúrese de que el complemento Acrobat PDFMaker Office COM esté habilitado para las aplicaciones de Microsoft Office.

+++

+++OpenOffice

**Microsoft® Windows**

* Asegúrese de que los bits de 32 bits [versión compatible ](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) de Microsoft Office está instalado y los cuadros de diálogo de apertura se cancelan para todas las aplicaciones.
* Asegúrese de que se agrega un usuario de Generador de PDF en la interfaz de usuario de configuración del PDF.
* Asegúrese de que el usuario del Generador de PDF sea miembro del grupo de administradores y de que la variable [Reemplazar un token de nivel de proceso](#grant-the-replace-a-process-level-token-privilege) se establece para el usuario.
* Asegúrese de que el usuario está configurado en la interfaz de usuario del Generador de PDF y realice las siguientes acciones:
   1. Inicie sesión en Microsoft® Windows con el usuario del Generador de PDF.
   1. Abra las aplicaciones de Microsoft® Office u Open Office y cancele todos los cuadros de diálogo.
   1. Establezca AdobePDF como impresora predeterminada.
   1. Establezca Acrobat como programa predeterminado para archivos de PDF.
   1. Realice la conversión manual mediante las opciones Archivo > Imprimir y cinta Acrobat en las aplicaciones de Microsoft Office y cancele todos los cuadros de diálogo.
   1. Finalice todos los procesos relacionados con la conversión, como winword.exe, powerpoint.exe y excel.exe.
   1. Reinicie el servidor de AEM Forms.

**Linux®**

* Instale el [versión compatible](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) de OpenOffice. AEM Forms admite versiones de 32 y 64 bits. Después de la instalación, abra todas las aplicaciones de OpenOffice, cancele todas las ventanas de diálogo y cierre las aplicaciones. Vuelva a abrir las aplicaciones y asegúrese de que no aparece ningún cuadro de diálogo al abrir una aplicación de OpenOffice.

* Crear una variable de entorno `OpenOffice_PATH` y configúrelo para que apunte a que la instalación de OpenOffice está configurada en la [consola](https://linuxize.com/post/how-to-set-and-list-environment-variables-in-linux/) o el perfil dt (árbol de dispositivos).
* Si hay problemas al instalar OpenOffice, asegúrese de que [Bibliotecas de 32 bits](#extrarequirements) se requiere para la instalación de OpenOffice.

+++

++HTML a problemas de conversión de PDF

* Asegúrese de que los directorios de fuentes se añaden en la interfaz de usuario de configuración de PDF Generator.

**Linux y Solaris (ruta de conversión PhantomJS)**

* Asegúrese de que la biblioteca de 32 bits esté disponible (libicudata.so.42) para la conversión HTMLoPDF basada en Webkit y que las bibliotecas de 64 bits (libicudata.so.42) estén disponibles para la conversión HTMLoPDF basada en PhantomJS.

* Ejecute el siguiente comando para enumerar las bibliotecas que faltan para phantomjs:

   ```
   ldd phantomjs | grep not
   ```

* Asegúrese de que la variable de entorno JAVA_HOME_32 señala a la ubicación correcta.

**Linux® y Solaris™ (ruta de conversión WebKit)**

* Asegúrese de que los directorios `/usr/lib/X11/fonts` y `/usr/share/fonts` existe. Si los directorios no existen, cree un vínculo simbólico desde `/usr/share/X11/fonts` a `/usr/lib/X11/fonts` y otro vínculo simbólico de `/usr/share/fonts` a `/usr/share/X11/fonts`.

   ```
   ln -s /usr/share/fonts /usr/share/X11/fonts
   
   ln -s /usr/share/X11/fonts /usr/lib/X11/fonts
   ```

* Asegúrese de que las fuentes de IBM se copien en usr/share/fonts.
* Asegúrese de que la corrección de vulnerabilidades fantasma glibc esté disponible en el equipo. Utilice su gestor de paquetes predeterminado para actualizar a la última versión de glibc. Incluye corrección de vulnerabilidades fantasma.
* Asegúrese de que las últimas versiones de las bibliotecas lib curl, libcrypto y libssl de 32 bits estén instaladas en el sistema. Crear también enlaces simbólicos `/usr/lib/libcurl.so` (o libcurl.a para AIX®), `/usr/lib/libcrypto.so` (o libcrypto.a para AIX®) y `/usr/lib/libssl.so` (o libssl.a para AIX®) que señala a las últimas versiones (32 bits) de las bibliotecas correspondientes.

* Realice los siguientes pasos para el proveedor de IBM® SSL Socket:
   1. Copie el archivo java.security de `<WAS_Installed_JAVA>\jre\lib\security` a cualquier ubicación de su servidor de AEM Forms. La ubicación predeterminada es Ubicación predeterminada es = `<WAS_Installed>\Appserver\java_[version]\jre\lib\security`.

   1. Edite el archivo java.security en la ubicación copiada y cambie las fábricas SSL Socket predeterminadas con fábricas JSSE2 (utilice fábricas JSSE2 en lugar de WebSphere®).

      Cambie las siguientes fábricas de socket JSSE predeterminadas:

      ```
      #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

      con

      ```
      ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

+++

+++ No se puede agregar un usuario del Generador de PDF (PDFG)

* Asegúrese de que Microsoft® Visual C++ 2012 x86 y Microsoft® Visual C++ 2013 x86 (32 bits) redistribuibles estén instalados en Windows.

+++

+++Fallas en la prueba de automatización

* Para Microsoft® Office y OpenOffice, realice al menos una conversión manualmente (como cada usuario) para asegurarse de que no aparece ningún cuadro de diálogo durante la conversión. Si aparece algún diálogo, descártelo. No debería aparecer ningún cuadro de diálogo de este tipo durante la conversión automatizada.

* Antes de ejecutar la automatización en un AEM Forms en un entorno OSGi, asegúrese de que el paquete de prueba esté instalado y activo.

+++

+++Fallas en la conversión de varios usuarios

* Compruebe los registros del servidor para comprobar si la conversión está fallando para un usuario en particular.(Process Explorer puede ayudarle a comprobar el proceso de ejecución de distintos usuarios)

* Asegúrese de que el usuario configurado para el Generador de PDF tiene derechos de administrador local.

* Asegúrese de que el usuario del Generador de PDF tenga permisos de lectura, escritura y ejecución en los usuarios temporales LC y PDFG.

* Para Microsoft® Office y OpenOffice, realice al menos una conversión manualmente (como cada usuario) para asegurarse de que no aparece ningún cuadro de diálogo durante la conversión. Si aparece algún diálogo, descártelo. No debería aparecer ningún cuadro de diálogo de este tipo durante la conversión automatizada.

* Realice una conversión de muestra.

+++

+++La licencia de Adobe Acrobat instalada en el servidor de AEM Forms caduca

* Si tiene una licencia existente de Adobe Acrobat y esta ha caducado, [Descargue la versión más reciente de Adobe Application Manager](https://helpx.adobe.com/in/creative-suite/kb/aam-troubleshoot-download-install.html)y migrando su número de serie. Antes [migración del número de serie](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number).

   * Utilice los siguientes comandos para generar prov.xml y volver a serializar la instalación existente usando el archivo prov.xml en lugar de los comandos proporcionados en [migración del número de serie](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) artículo numérico.

          &quot;
          
          adobe_prtk —tool=VolumeSerialize —generate —serial=&lt;serialnum> [—leid=&lt;leid>] [—regsuppress=ss] [—eulasuppress] [—configuraciones regionales=lista limitada de configuraciones regionales en formato xx_XX o ALL>] [—provfile=&lt;absolute path=&quot;&quot; to=&quot;&quot; prov.xml=&quot;&quot;>]
          
          &quot;
      
   * Serialice el paquete por volumen (vuelva a serializar la instalación existente usando el archivo prov.xml y la nueva serie): Ejecute el siguiente comando desde la carpeta de instalación de PRTK como administrador para serializar y activar los paquetes implementados en los equipos cliente:

          &quot;
          adobe_prtk —tool=VolumeSerialize —provfile=C:\prov.xml -stream
          
          &quot;
      
* Para instalaciones a gran escala, utilice el [Customization Wizard de Acrobat](https://www.adobe.com/devnet-docs/acrobatetk/tools/Wizard/index.html) para eliminar las versiones anteriores de Reader y Acrobat. Personalice el instalador e impleméntelo en todos los equipos de su organización.

+++

+++ AEM Forms Server se encuentra en un entorno seguro o sin conexión y Internet no está disponible para activar Acrobat.

* Puede conectarse en un plazo de 7 días a partir del primer lanzamiento del producto de Adobe para realizar una activación y registro en línea o utilizar un dispositivo con acceso a Internet y el número de serie de su producto para completar este proceso. Para obtener instrucciones detalladas, consulte [Activación sin conexión](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en).

+++

## Pasos siguientes {#next-steps}

Tiene un entorno de AEM Forms document services en funcionamiento. Puede utilizar document services mediante:

* [Flujos de trabajo centrados en formularios en OSGi](/help/forms/using/aem-forms-workflow.md)
* [Carpetas inspeccionadas](/help/forms/using/watched-folder-in-aem-forms.md)
* [API de servicios de documentos](/help/forms/using/aem-document-services-programmatically.md)
