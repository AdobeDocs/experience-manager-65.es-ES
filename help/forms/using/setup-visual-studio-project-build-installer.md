---
title: Configurar el proyecto de Visual Studio y crear la aplicación de Windows
seo-title: Set up the Visual Studio project and build the Windows app
description: Obtenga información sobre cómo configurar un proyecto de Visual Studio para crear la aplicación para dispositivos móviles AEM Forms Windows.
seo-description: Learn how to set up a Visual Studio project to build the AEM Forms Windows mobile device app.
uuid: 9559e584-2a40-4740-a29a-d7ad66220224
topic-tags: forms-app
discoiquuid: c71c2a17-54f9-4c95-a90a-3c89d6d45721
docset: aem65
exl-id: ae7340c8-38cc-4b2b-ba17-22011471fd7d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 5%

---

# Configurar el proyecto de Visual Studio y crear la aplicación de Windows{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms proporciona el código fuente completo de la aplicación AEM Forms. El origen contiene todos los componentes para crear una aplicación de espacio de trabajo personalizada. El archivo de código fuente, `adobe-lc-mobileworkspace-src-<version>.zip`forma parte de la función `adobe-aemfd-forms-app-src-pkg-<version>.zip` en Distribución de software.

Para obtener la fuente de la aplicación de AEM Forms, realice los siguientes pasos:

1. Abra [Distribución de software](https://experience.adobe.com/downloads). Necesitará un Adobe ID para iniciar sesión en la distribución de software.
1. Pulse **[!UICONTROL Adobe Experience Manager]**, disponible en el menú del encabezado.
1. En el **[!UICONTROL Filtros]** sección:
   1. Select **[!UICONTROL Forms]** de la variable **[!UICONTROL Solución]** lista desplegable.
   2. Seleccione la versión y el tipo del paquete. También puede usar la variable **[!UICONTROL Descargas de búsqueda]** para filtrar los resultados.
1. Pulse el nombre del paquete aplicable a su sistema operativo, seleccione **[!UICONTROL Aceptar términos de EULA]** y toque **[!UICONTROL Descargar]**.
1. Abra [Administrador de paquetes](https://docs.adobe.com/content/help/es/experience-manager-65/administering/contentmanagement/package-manager.html) y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete.
1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

1. Para descargar el archivo de código fuente, abra `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` en su navegador.\
   El paquete de origen se descarga en el dispositivo.

La siguiente imagen muestra el contenido extraído del `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content-1](assets/mws-content-1.png)

La siguiente imagen muestra la estructura de directorio del `windows` en la carpeta `src` carpeta.

![win-dir](assets/win-dir.png)

## Configuración del entorno {#setting-up-the-environment}

Para dispositivos Windows, necesita:

* Microsoft Windows 8.1 o Windows 10
* Microsoft Visual Studio 2015
* Microsoft Visual Studio Tools para Apache Cordova

## Configuración del proyecto de Visual Studio para la aplicación AEM Forms {#setting-up-visual-studio-project-for-aem-forms-app}

Siga estos pasos para configurar el proyecto de aplicación de AEM Forms en Visual Studio.

1. Copie el `adobe-lc-mobileworkspace-src-<version>.zip` archivar en `%HOMEPATH%\Projects` en el dispositivo Windows 8.1 o Windows 10 con Visual Studio 2015 instalado y configurado.
1. Extraiga el archivo en el `%HOMEPATH%\Projects\MobileWorkspace` directorio.
1. Vaya a la `%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows` directorio.
1. Abra el `CordovaApp.sln` con Visual Studio 2015 y continúe con la creación de la aplicación de AEM Forms.

## Generar aplicación de AEM Forms {#build-aem-forms-app}

Siga estos pasos para crear e implementar la aplicación AEM Forms.

>[!NOTE]
>
>Los datos almacenados en el sistema de archivos de Windows para la aplicación AEM Forms no están cifrados. Se recomienda usar una herramienta de terceros como Cifrado de unidad BitLocker de Windows para cifrar datos de disco.

1. En la barra de herramientas de Visual Studio Standard, seleccione **Versión** en la lista desplegable del modo de compilación.

1. Seleccione Windows-AnyCPU, Windows-x64 o Windows-x86 según su plataforma. Se recomienda Windows-AnyCPU.
1. En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en el proyecto **CordovaApp.Windows** y seleccione **Tienda > Crear paquetes de aplicaciones**.

   ![createapppackages](assets/createapppackages.png)

   Aparece el asistente Crear paquetes de aplicaciones .

   El archivo del instalador CordovaApp.Windows_3.0.2.0_anycpu.appx se crea en el directorio platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test .

   Si aparece el error `Retarget to windows 8.1 required`, haga clic con el botón derecho en el error y, en el menú emergente, seleccione **Redestinar A Windows 8.1**.

   ![retarget-solution](assets/retarget-solution.png)

1. En el asistente Crear paquetes de aplicaciones , seleccione el tiempo que desee o no cargar la aplicación en la tienda de Windows y, a continuación, haga clic en **Siguiente**.

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. Realice los cambios necesarios en los parámetros, como la versión y la ubicación de salida de la compilación de la aplicación.

   ![createapppackageswizard2](assets/createapppackageswizard2.png)

1. Una vez creado el proyecto, puede instalar la aplicación mediante:

   * Windows PowerShell
   * Visual Studio

   La variable `.appx` requiere que los siguientes elementos se instalen correctamente:

   1. Biblioteca WinJS
   1. Asegúrese de que el paquete incluye un certificado autofirmado o un certificado público firmado por una autoridad de confianza, como VeriSign.
   1. Licencia para desarrolladores

   El directorio Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test contiene los cuatro componentes principales:

   1. `.appx` file
   1. Certificado (actualmente es un certificado autofirmado por Apache Cordova)
   1. Carpeta de dependencias
   1. Archivo PowerShell (extensión .ps1)



## Implementación de una aplicación mediante Windows PowerShell {#deploying-an-app-using-windows-powershell}

Existen dos maneras de instalar la aplicación en un dispositivo Windows.

### Adquiriendo la licencia de desarrollador {#by-acquiring-the-developer-license}

1. Haga clic con el botón derecho en el archivo de PowerShell ( `Add-AppDevPackage.ps1)`y elija **Ejecutar con PowerShell**.

1. La configuración le solicita una licencia para desarrolladores. Utilice las credenciales de cuenta de Microsoft para adquirir una licencia de desarrollador.\
   Esta licencia es válida durante 30 días, y usted puede renovarla gratis.
1. Cuando adquiere la licencia de desarrollador, el programa de instalación instala el certificado autofirmado en el sistema y la aplicación se instala correctamente.

### Mediante dispositivos de propiedad empresarial {#by-using-enterprise-owned-devices}

Para los dispositivos de propiedad empresarial unidos al dominio de la empresa, no es necesario adquirir una licencia de desarrollador.

Los dispositivos de propiedad empresarial utilizan las ediciones Professional y Enterprise de Windows.

Microsoft recomienda instalar un certificado público emitido por una autoridad de confianza, como VeriSign.

Para implementar la aplicación:

* Asegúrese de que el dispositivo esté unido al dominio de la empresa.
* Habilite la configuración de directiva de grupo.

**Para habilitar la configuración de directiva de grupo:**

1. En el dispositivo, ejecute `gpedit.msc`.
1. Vaya a **Configuración del equipo > Plantillas administrativas > Componente de Windows > Implementación del paquete de aplicaciones**.
1. Haga clic con el botón derecho en **Permitir que todas las aplicaciones de confianza instalen**.
1. Haga clic en **Editar** y seleccione **Habilitado**.

1. Haga clic en **Aceptar**.

Edite el script de PowerShell generado por Visual Studio para evitar que adquiera una licencia de desarrollador.

En el script de PowerShell, establezca la variable : `$NeedDeveloperLicense = $false`.

Para los dispositivos que no están unidos al dominio, se requiere una clave de activación de producto de carga secundaria. Puede comprarlo a un distribuidor de Windows.

Para Windows 8.1 Home Edition, no hay directiva de grupo, no se permite la carga secundaria de empresa y no se puede unir con el dominio de empresa. Implemente la aplicación en un dispositivo Windows 8.1 Home Edition con licencia de desarrollador.

Para obtener más información, haga clic en [here](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx).

## Implementación de una aplicación mediante Visual Studio {#deploying-an-app-using-visual-studio}

Para instalar la aplicación en Windows mediante Visual Studio:

1. Conecte el dispositivo con el depurador remoto.\
   Para obtener más información, consulte [Ejecutar aplicaciones de la Tienda Windows en un equipo remoto](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine).

1. Con la aplicación abierta en Visual Studio, elija Windows-x64, Windows-x86 o Windows-AnyCPU en la lista Plataformas de solución y seleccione **Máquina remota**.
1. La aplicación se implementa en el equipo remoto.
