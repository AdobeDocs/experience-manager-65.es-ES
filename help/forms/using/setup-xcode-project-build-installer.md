---
title: Configuración del proyecto Xcode y compilación de la aplicación iOS
seo-title: Set up the Xcode project and build the iOS app
description: Explica cómo crear una aplicación de AEM Forms estándar para iOS.
seo-description: Explains how to build standard AEM Forms app for iOS.
uuid: 29779bbb-06b4-4ece-9f29-786afab59eaf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 88555db2-712f-4ef9-bf47-76c7ba83d964
docset: aem65
exl-id: 78ce6107-8821-47d6-86ab-7ab968945e7c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 6%

---

# Configuración del proyecto Xcode y compilación de la aplicación iOS{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms proporciona el código fuente completo de la aplicación AEM Forms. La fuente contiene todos los componentes para crear una aplicación de AEM Forms personalizada. El archivo de código fuente, `adobe-lc-mobileworkspace-src-<version>.zip` forma parte de la función `adobe-aemfd-forms-app-src-pkg-<version>.zip` en Distribución de software.

Para obtener la fuente de la aplicación de AEM Forms, realice los siguientes pasos:

1. Abra [Distribución de software](https://experience.adobe.com/downloads). Necesitará un Adobe ID para iniciar sesión en la distribución de software.
1. Pulse **[!UICONTROL Adobe Experience Manager]**, disponible en el menú del encabezado.
1. En el **[!UICONTROL Filtros]** sección:
   1. Select **[!UICONTROL Forms]** de la variable **[!UICONTROL Solución]** lista desplegable.
   2. Seleccione la versión y el tipo del paquete. También puede usar la variable **[!UICONTROL Descargas de búsqueda]** para filtrar los resultados.
1. Pulse el nombre del paquete aplicable a su sistema operativo, seleccione **[!UICONTROL Aceptar términos de EULA]** y toque **[!UICONTROL Descargar]**.
1. Abra [Administrador de paquetes](https://docs.adobe.com/content/help/es/experience-manager-65/administering/contentmanagement/package-manager.html) y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete.
1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

1. Para descargar el archivo de código fuente, abra `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` en su navegador.
El paquete de origen se descarga en el dispositivo.

La siguiente imagen muestra el contenido extraído del `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

La siguiente tabla detalla el contenido de la `adobe-lc-mobileworkspace-src-[version]/ios` carpeta.

<table>
 <tbody>
  <tr>
   <th><p>Directorio</p> </th>
   <th><p>Contenido</p> </th>
  </tr>
  <tr>
   <td><p><code>CordovaLib</code></p> </td>
   <td><p>SDK 6.4.0 de PhoneGap</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms</code></p> </td>
   <td><p>Recursos, complementos de PhoneGap y módulo principal de la aplicación</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms.xcodeproj</code></p> </td>
   <td><p>Proyecto Xcode para la aplicación AEM Forms</p> </td>
  </tr>
  <tr>
   <td><p><code>www</code></p> </td>
   <td><p>HTML, CSS, imágenes y archivos JavaScript para el proyecto de aplicación de AEM Forms</p> </td>
  </tr>
 </tbody>
</table>

Para obtener información detallada sobre la firma de código y la adición de dispositivos al portal de aprovisionamiento de iOS, consulte [Configuración, proceso y solución de problemas de iOS Code Signing](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html).

## Generar aplicación de AEM Forms estándar {#set-up-the-xcode-project}

1. Realice los siguientes pasos para configurar un proyecto en Xcode y proporcionar una identidad de firma:

   Inicie sesión en su equipo de Mac que tenga Xcode y iOS SDK instalados y configurados.

1. Copie el `adobe-lc-mobileworkspace-src-<version>.zip` archivar desde la carpeta de descargas a `[User_Home]/Projects/`.
1. Extraiga el archivo en el `[User_Home]/Projects/[your-project]`directorio.
1. Vaya a la ` [User_Home]/Projects/ `[su proyecto]`/adobe-lc-mobileworkspace-src-[version]/ios` directorio.
1. Abra el `AEM Forms.xcodeproj` proyecto en Xcode.
1. Haga clic en **AEM Forms**, en **OBJETIVOS**, seleccione **AEM Forms**. Seleccione el **Configuración de compilación** , busque **Derecho de firma de código** , y en los campos Depurar y Liberar , realice una de las siguientes acciones:

   * Deje los campos sin especificar para crear una aplicación estándar de Mobile Workspace.
   * Especifique los campos a como se explica en [Creación de una aplicación segura de AEM Forms para iOS](/help/forms/using/building-secure-mobile-workspace-app.md) para crear una aplicación segura de AEM Forms.

1. En el **Configuración de compilación** , haga clic en **Todo** y haga clic en **Combinado**.
1. En el **Configuración** lista, expandir **Firma de código**.
1. Para **Identidad de firma de código**, seleccione la firma adecuada. Para obtener información detallada sobre la creación de nuevas firmas, consulte [Creación y descarga de perfiles de aprovisionamiento de desarrollo](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html).
1. Asegúrese de que se ha seleccionado la misma firma para **Depuración**, **Versión** y **Cualquier SDK de iOS**.
1. Reemplace el siguiente código en la variable `AEM Forms-info.plist` archivo:

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   por lo siguiente, al reemplazar `yourserver.com` con un nombre de host apropiado para su servidor.

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSExceptionDomains</key>
   <dict>
   <key>yourserver.com</key>
   <dict>
   <!-Include to allow subdomains->
   <key>NSIncludesSubdomains</key>
   <true/>
   <!-Include to allow HTTP requests->
   <key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
   <true/>
   <!-Include to support forward secrecy->
   <key>NSExceptionRequiresForwardSecrecy</key>
   <false/>
   <!-Include to specify minimum TLS version->
   <key>NSTemporaryExceptionMinimumTLSVersion</key>
   <string>TLSv1.1</string>
   </dict>
   </dict>
   </dict>
   ```

   >[!NOTE]
   >
   >Este paso solo es necesario si la aplicación de AEM Forms necesita conectarse a un servidor que no cumpla los requisitos de App Transport Security.

1. En **PROYECTO**, seleccione **AEM Forms** y asegúrese de que la firma adecuada está seleccionada para **Identidad de firma de código**, **Depuración**, **Versión** y **Cualquier SDK de iOS**.
1. Conecte un iPad aprovisionado a un equipo Mac.
1. Seleccione el dispositivo aprovisionado para la variable **AEM Forms** proyecto.

   ![ipad](assets/ipad.png)

   Se ha seleccionado un dispositivo aprovisionado, iPad Air 2.

1. Select **Product** > **Limpiar**.
1. Select **Product** > **Generar**.

## Cree el instalador para la aplicación de AEM Forms {#build-the-installer-for-the-mobile-workspace-app}

Debe archivar el proyecto Xcode para crear el instalador (un archivo .ipa) y un archivo de lista de propiedades (un archivo .plist). El archivo de lista de propiedades contiene información de configuración de la aplicación interna alojada, como el nombre y la ubicación de alojamiento de la aplicación. Para obtener más información sobre el archivo de lista de propiedades, consulte [Acerca de los archivos de lista de propiedades de información](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Conecte un iPad aprovisionado a un equipo Mac. Para obtener información detallada sobre el aprovisionamiento de un iPad, consulte [Creación y descarga de perfiles de aprovisionamiento de desarrollo](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. Seleccione el dispositivo aprovisionado para la variable **AEM Forms** proyecto.

   ![ipad-1](assets/ipad-1.png)

   Se ha seleccionado un dispositivo aprovisionado, iPad Air 2.

1. Select **Product** > **Limpiar**.
1. Select **Product** > **Generar**.
1. Select **Product** > **Archivo**.
1. En Organizer - Archivos, seleccione el último archivo del proyecto y haga clic en **Distribuir**.
1. Select **Guardar para implementación empresarial o ad hoc** como método de distribución y haga clic en **Siguiente**.
1. Seleccione el **Identidad de firma de código** y haga clic en **Siguiente**. Haga clic en **Permitir** para aplicar la firma.
1. Proporcione el nombre de la aplicación y seleccione **Guardar para distribución empresarial**.
1. Proporcione la variable **URL de la aplicación** para la aplicación. Por ejemplo, para alojar la aplicación en un servidor CRX, proporcione la URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. En el **Título** , especifique AEM Forms.
1. Haga clic en **Guardar** y cierre Xcode.

   Un archivo de instalación, `AEM Forms.ipa`y el archivo de lista de propiedades, `AEM Forms-info.plist`, se crean en la ubicación especificada.

1. Abra el `AEM Forms-info.plist` en un editor.
1. Reemplace todos los espacios en la dirección URL del archivo .ipa por %20.
1. Guarde y cierre el archivo `AEM Forms-info.plist`.
