---
title: Personalización de promoción de la marca
seo-title: Personalización de promoción de la marca
description: Personalice el icono de la aplicación, el nombre de la aplicación, las imágenes de inicio y la página de inicio de sesión para proporcionar a la aplicación de AEM Forms un aspecto y una presentación distintos específicos de la organización.
seo-description: Personalice el icono de la aplicación, el nombre de la aplicación, las imágenes de inicio y la página de inicio de sesión para proporcionar a la aplicación de AEM Forms un aspecto y una presentación distintos específicos de la organización.
uuid: fece0fa8-c417-45eb-93f1-a91b49835fa0
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f6440a36-719a-4f89-b7db-1af918a3469a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Personalización de promoción de la marca {#branding-customization}

Puede personalizar el icono de la aplicación, el nombre de la aplicación, las imágenes de inicio y la página de inicio de sesión para que la aplicación de AEM Forms tenga un aspecto específico de la organización. Por ejemplo, puede cambiar las imágenes para utilizar logotipos de su organización. La aplicación de AEM Forms admite las siguientes personalizaciones:

* Personalización del icono de la aplicación y las imágenes de inicio
* Personalización del nombre de la aplicación
* Personalización de imágenes en la página de inicio de sesión
* Personalización del logotipo en el menú de la aplicación

## Personalización de imágenes de inicio e iconos {#customizing-icon-and-launch-images}

Siga estos pasos para personalizar el icono predeterminado de la aplicación y la imagen de inicio de la aplicación de AEM Forms:

>[!NOTE]
>
>Para todos los iconos e imágenes, utilice formato PNG no entrelazado.

### Personalización de iconos e imágenes de inicio {#to-customize-icon-and-launch-images}

#### Para iOS {#for-ios}

1. Abra el `Capture.xcodeproj` proyecto en Xcode.
1. (***Para personalizar el icono***) En la vista del navegador de Captura, vaya a **[!UICONTROL Capturar > Capturar > Archivos de soporte > Capturar-información.plist]**. Haga clic en la lista desplegable situada junto a los archivos de icono. Especifique el nombre del archivo de icono (.png) y cargue el archivo en **[!UICONTROL Captura > Captura > Recursos > iconos]**. Las dimensiones admitidas actualmente son: 29 x 29, 50 x 50, 58 x 58, 72 x 72, 100 x 100 y 144 x 144.
1. (***Para personalizar imágenes*** de inicio) Asegúrese de que los nombres de archivo de las imágenes son:

   * Para vertical: `Default-Portrait~ipad.png` y `Default-Portrait@2x~ipad.png`
   * Para horizontal: `Default-Landscape~ipad.png` y `Default-Landscape@2x~ipad.png`
   Cargue los archivos en el proyecto Capturar para reemplazar los archivos existentes en el proyecto.

   >[!NOTE]
   >
   >Asegúrese de que el nombre y la resolución de la imagen coinciden con la imagen que reemplaza en el proyecto.

1. Cree y ejecute la aplicación de AEM Forms en dispositivos iOS o simulador de iOS.

#### Para Android {#for-android}

1. Asigne un nombre a los archivos de icono de la aplicación como:

   `ic_launcher.png`

1. Coloque los archivos de icono correspondientes en los directorios siguientes:

   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-hdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-mdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxxhdpi`
   >[!NOTE]
   >
   >Asegúrese de que el nombre y la resolución de la imagen coinciden con la imagen que reemplaza en el proyecto.

1. Vuelva a compilar la aplicación de AEM Forms.

### Para Windows {#for-windows}

1. Reemplace los iconos de la ruta:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. Reemplazar la imagen del iniciador en la ruta:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >Asegúrese de que el nombre y la resolución de la imagen coinciden con la imagen que reemplaza en el proyecto.

1. Vuelva a compilar la aplicación de AEM Forms.

## Personalización del nombre de la aplicación {#customize-the-app-name}

### Para iOS {#for-ios-1}

1. Abra el `Capture.xcodeproj` proyecto en Xcode.
1. En la vista del navegador de Captura, vaya a **[!UICONTROL Captura > Captura > Archivos de soporte > InfoPlist.strings]**.

   Actualice el valor del `CFBundleDisplayName` atributo a un nombre que desee mostrar para la aplicación.

1. Cree y ejecute la aplicación de AEM Forms en dispositivos iOS o simulador de iOS.

   Para obtener más información sobre la creación de la aplicación para iOS, consulte [Configuración del proyecto Xcode y compilación de la aplicación](/help/forms/using/setup-xcode-project-build-installer.md)iOS.

### Para Android {#for-android-1}

1. Abra el siguiente XML en cualquier editor de texto o XML:

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. Actualice el valor de la clave `app_name`.
1. Vuelva a compilar la aplicación de AEM Forms.

   Para obtener más información sobre la creación de la aplicación para Android, consulte [Configuración del proyecto Eclipse y compilación de la aplicación](/help/forms/using/setup-eclipse-project-build-installer.md)para Android.

### Para Windows {#for-windows-1}

1. Abra el siguiente XML en cualquier editor de texto:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. Actualice el valor en la `<name>...</name>` etiqueta .
1. Vuelva a compilar la aplicación de AEM Forms.

   Para obtener más información sobre la creación de la aplicación para Windows, consulte [Configuración del proyecto de Visual Studio y compilación de la aplicación](/help/forms/using/setup-visual-studio-project-build-installer.md)de Windows.

## Personalización de imágenes en la página de inicio de sesión {#customizing-images-on-the-login-page}

La página de inicio de sesión de la aplicación de AEM Forms tiene un logotipo e imágenes de fondo. El logotipo se encuentra encima del cuadro de diálogo de inicio de sesión y la imagen de fondo se encuentra debajo del cuadro de diálogo de inicio de sesión. Realice los siguientes pasos para personalizar la imagen predeterminada en la página de inicio de sesión:

**Antes de comenzar**

Asegúrese de que tiene las siguientes imágenes:

<table>
 <tbody>
  <tr>
   <th><p>Descripción</p> </th>
   <th><p>Tamaño</p> </th>
   <th><p>Nombre de archivo</p> </th>
  </tr>
  <tr>
   <td><p>Logotipo</p> </td>
   <td><p>72 x 72 píxeles</p> </td>
   <td><p>LC-logo.png</p> </td>
  </tr>
  <tr>
   <td><p>Imagen de fondo (vertical)</p> </td>
   <td><p>1280 x 989 píxeles</p> </td>
   <td><p>Landing_bg.jpeg</p> </td>
  </tr>
 </tbody>
</table>

**Personalización de imágenes en la página de inicio de sesión con Xcode**

1. Abra el `Capture.xcodeproj` proyecto en Xcode.

1. Vaya a la `www/wsmobile/images`carpeta.
1. Para cambiar el logotipo, reemplace el `LC-logo.png` archivo predeterminado por el `LC-logo.png` archivo personalizado.
1. Para cambiar el fondo, reemplace el `Landing_bg.jpeg` archivo predeterminado por el `Landing_bg.jpeg`archivo personalizado.
1. Cree y ejecute la aplicación de AEM Forms en dispositivos iOS o simulador de iOS.

### Personalización de imágenes en las páginas de inicio de sesión con Eclipse {#to-customize-images-on-the-login-pages-using-eclipse}

1. Abra el proyecto de Android en Eclipse.

1. Vaya a la `assets/www/wsmobile/images`carpeta.
1. Para cambiar el logotipo, reemplace el `LC-logo.png` archivo predeterminado por el `LC-logo.png` archivo personalizado.
1. Para cambiar el fondo, reemplace el `Landing_bg.jpeg` archivo predeterminado por el `Landing_bg.jpeg`archivo personalizado.
1. Cree y ejecute la aplicación de AEM Forms en dispositivos Android.

### Personalización de imágenes en las páginas de inicio de sesión con Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio}

1. Abra el `MWSWindows.sln` proyecto en Visual Studio.

1. Vaya a la `MWSWindows\www\wsmobile\images`carpeta.
1. Para cambiar el logotipo, reemplace el `LC-logo.png` archivo predeterminado por el `LC-logo.png` archivo personalizado.
1. Para cambiar el fondo, reemplace el `Landing_bg.jpeg` archivo predeterminado por el `Landing_bg.jpeg`archivo personalizado.
1. Cree y ejecute la aplicación de AEM Forms en el dispositivo Windows.

## Personalización del logotipo en el menú de la aplicación {#customizing_images_on_the_login_page-1}

Después de iniciar sesión en la aplicación de AEM Forms y tocar el botón de menú, puede ver el logotipo encima del menú. Siga estos pasos para personalizar el logotipo predeterminado:

**Antes de comenzar**

Asegúrese de que tiene la siguiente imagen:

<table>
 <tbody>
  <tr>
   <th><p>Descripción</p> </th>
   <th><p>Tamaño</p> </th>
   <th><p>Nombre de archivo</p> </th>
  </tr>
  <tr>
   <td><p>Logotipo</p> </td>
   <td><p>72 x 72 píxeles</p> </td>
   <td><p>aem_icon.png</p> </td>
  </tr>
 </tbody>
</table>

**Personalización de imágenes en la página de inicio de sesión con Xcode**

1. Abra el `Capture.xcodeproj` proyecto en Xcode.

1. Vaya a la `www/wsmobile/images`carpeta.
1. Para cambiar el logotipo, reemplace el `aem_icon.png` archivo predeterminado por el `aem_icon.png` archivo personalizado.
1. Cree y ejecute la aplicación de AEM Forms en dispositivos iOS o simulador de iOS.

### Personalización de imágenes en las páginas de inicio de sesión con Eclipse {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. Abra el proyecto de Android en Eclipse.

1. Vaya a la `assets/www/wsmobile/images`carpeta.
1. Para cambiar el logotipo, reemplace el `aem_icon.png` archivo predeterminado por el `aem_icon.png` archivo personalizado.
1. Cree y ejecute la aplicación de AEM Forms en dispositivos Android.

### Personalización de imágenes en las páginas de inicio de sesión con Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. Abra el `MWSWindows.sln` proyecto en Visual Studio.

1. Vaya a la `MWSWindows\www\wsmobile\images`carpeta.
1. Para cambiar el logotipo, reemplace el `aem_icon.png` archivo predeterminado por el `aem_icon.png` archivo personalizado.
1. Cree y ejecute la aplicación de AEM Forms en el dispositivo Windows.

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
