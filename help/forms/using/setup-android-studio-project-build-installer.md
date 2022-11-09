---
title: Configure el proyecto de Android Studio y cree la aplicación de Android.
seo-title: Set up the Android studio project and build the Android app
description: Pasos para configurar el proyecto de Android Studio y crear el instalador para la aplicación de AEM Forms
seo-description: Steps to set up the Android Studio project and build the installer for the AEM Forms app
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
exl-id: 47d6af00-34d8-4e5d-8117-86fc1b6f58cb
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 7%

---

# Configure el proyecto de Android Studio y cree la aplicación de Android. {#set-up-the-android-studio-project-and-build-the-android-app}

Este artículo se destina a la creación de la aplicación AEM Forms 6.3.1.1 y versiones posteriores. Para crear una aplicación a partir del código fuente del código fuente de la aplicación AEM Forms 6.3, consulte [Configure el proyecto Eclipse y cree la aplicación Android™](/help/forms/using/setup-eclipse-project-build-installer.md).

AEM Forms proporciona el código fuente completo de la aplicación AEM Forms. La fuente contiene todos los componentes para crear una aplicación de AEM Forms personalizada. El archivo de código fuente, `adobe-lc-mobileworkspace-src-<version>.zip` forma parte de la función `adobe-aemfd-forms-app-src-pkg-<version>.zip` en Distribución de software.

Para obtener la fuente de la aplicación de AEM Forms, realice los siguientes pasos:

1. Abra [Distribución de software](https://experience.adobe.com/downloads). Necesitará un Adobe ID para iniciar sesión en la distribución de software.
1. Pulse **[!UICONTROL Adobe Experience Manager]**, disponible en el menú del encabezado.
1. En el **[!UICONTROL Filtros]** sección:
   1. Select **[!UICONTROL Forms]** de la variable **[!UICONTROL Solución]** lista desplegable.
   2. Seleccione la versión y el tipo del paquete. También puede usar la variable **[!UICONTROL Descargas de búsqueda]** para filtrar los resultados.
1. Pulse el nombre del paquete aplicable a su sistema operativo, seleccione **[!UICONTROL Aceptar términos de EULA]** y toque **[!UICONTROL Descargar]**.
1. Abra [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es) y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete.
1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

La siguiente imagen muestra el contenido extraído del `adobe-lc-mobileworkspace-src-<version>.zip`.

![Contenido extraído de la fuente comprimida de Android™](assets/mws-content-1.png)

La siguiente imagen muestra la estructura de directorio del `android`en la carpeta `src`carpeta.

![Estructura de directorio de la carpeta android en src](assets/android-folder.png)

## Generar aplicación de AEM Forms estándar {#set-up-the-xcode-project}

1. Siga los siguientes pasos para configurar un proyecto en Android™ Studio y proporcionar una identidad de firma:

   Inicie sesión en un equipo que tenga instalado y configurado Android™ Studio.

1. Copie el `adobe-lc-mobileworkspace-src-<version>.zip` archivar en:

   **Para usuarios de MAC**: `[User_Home]/Projects`

   **Para usuarios de Windows®**: `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >Para Windows®, se recomienda mantener el proyecto android en la unidad del sistema.

1. Extraiga el archivo en el siguiente directorio:

   **Para usuarios de MAC**: `[User_Home]/Projects/[your-project]`

   **Para usuarios de Windows®**: `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >Se recomienda mantener el proyecto de Android extraído en la unidad del sistema antes de importar el proyecto en Android Studio.

1. Inicie Android™ Studio.

   **Para usuarios de MAC**: Actualice el `local.properties` presente en la variable `[User_Home]/Projects/[your-project]/android` y señale `sdk.dir` a `SDK` en su escritorio.

   **Para usuarios de Windows®**: Actualice el `local.properties` presente en la variable `%HOMEPATH%\Projects\[your-project]\android` y señale `sdk.dir` a `SDK` en su escritorio.

1. Haga clic en **[!UICONTROL Finalizar]** para crear el proyecto.

   El proyecto está disponible en el explorador de proyectos de ADT.

   ![proyecto eclipse después de crear la aplicación](assets/eclipsebuildmws.png)

1. En Android™ Studio, seleccione **[!UICONTROL Importar Proyecto (Eclipse ADT, Gradle, Etc.)]**.
1. En el explorador del proyecto, seleccione el directorio raíz del proyecto que desea crear en la variable **Directorio raíz** cuadro de texto:

   **Para usuarios de Mac:** [User_Home]/Projects/MobileWorkspace/src/android

   **Para usuarios de Windows®:** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. Una vez importado el proyecto, aparece una ventana emergente con la opción de actualizar el complemento Android™ Gradle. Haga clic en el botón correspondiente según sus necesidades.

   ![dontremindmeagainfrancouisproject](assets/dontremindmeagainforthisproject.png)

1. Después de compilar correctamente el gradle, aparece la siguiente pantalla. Conecte el dispositivo o emulador apropiado con el sistema y haga clic en **[!UICONTROL Ejecutar Android™]**.

   ![gradleconsole](assets/gradleconsole.png)

1. Android™ Studio muestra los dispositivos conectados y los emuladores disponibles. Seleccione el dispositivo en el que desea ejecutar la aplicación y, a continuación, haga clic en **OK**.

   ![connecteddevice](assets/connecteddevice.png)

Una vez creado el proyecto, puede elegir instalar la aplicación mediante Android™ Debug Bridge o Android™ Studio.

### Uso del puente de depuración de Android™ {#andriod-debug-bridge}

Puede instalar la aplicación en un dispositivo Android™ a través del [Puente de depuración de Android™](https://developer.android.com/tools/help/adb.html) con el siguiente comando:

**Para usuarios de MAC**: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**Para usuarios de Windows®**: `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
