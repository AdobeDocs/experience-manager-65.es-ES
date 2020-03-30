---
title: Configure el proyecto Xcode y cree la aplicación de iOS
seo-title: Configure el proyecto Xcode y cree la aplicación de iOS
description: Explica cómo crear una aplicación estándar de AEM Forms para iOS.
seo-description: Explica cómo crear una aplicación estándar de AEM Forms para iOS.
uuid: 29779bbb-06b4-4ece-9f29-786afab59eaf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 88555db2-712f-4ef9-bf47-76c7ba83d964
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Configure el proyecto Xcode y cree la aplicación de iOS{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms proporciona el código fuente completo de la aplicación de AEM Forms. El origen contiene todos los componentes para crear una aplicación personalizada de AEM Forms. El archivo de código fuente `adobe-lc-mobileworkspace-src-<version>.zip` es parte del `adobe-aemfd-forms-app-src-pkg-<version>.zip` paquete en el uso compartido de paquetes.

Para obtener el origen de la aplicación de AEM Forms, realice los siguientes pasos:

1. Vaya a package shareURL: `https://<server>:<port>/crx/packageshare`.

1. Descargue el paquete de origen. Al descargar el paquete, se agrega al administrador de paquetes de AEM Forms.
1. Después de descargarlo, navegue a: `https://<server>:<port>/crx/packmgr/index.jsp`e instálelo `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

1. Para descargar el archivo de código fuente, abra `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` en el explorador.
El paquete de origen se descarga en el dispositivo.

La siguiente imagen muestra el contenido extraído del `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

En la tabla siguiente se detalla el contenido de la `adobe-lc-mobileworkspace-src-[version]/ios` carpeta.

<table>
 <tbody>
  <tr>
   <th><p>Directorio</p> </th>
   <th><p>Contenido</p> </th>
  </tr>
  <tr>
   <td><p><code>CordovaLib</code></p> </td>
   <td><p>PhoneGap SDK 6.4.0</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms</code></p> </td>
   <td><p>Recursos, complementos PhoneGap y módulo principal de la aplicación</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms.xcodeproj</code></p> </td>
   <td><p>Proyecto Xcode para la aplicación AEM Forms</p> </td>
  </tr>
  <tr>
   <td><p><code>www</code></p> </td>
   <td><p>Archivos HTML, CSS, imágenes y JavaScript para el proyecto de la aplicación AEM Forms</p> </td>
  </tr>
 </tbody>
</table>

Para obtener información detallada sobre la firma de código y la adición de dispositivos al portal de aprovisionamiento de iOS, consulte Configuración, proceso y resolución de problemas [de firma de código de](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html)iOS.

## Compilación de la aplicación estándar de AEM Forms {#set-up-the-xcode-project}

1. Realice los siguientes pasos para configurar un proyecto en Xcode y proporcionar una identidad de firma:

   Inicie sesión en el equipo Mac que tenga Xcode y iOS SDK instalados y configurados.

1. Copie el `adobe-lc-mobileworkspace-src-<version>.zip` archivo de la carpeta de descargas a `[User_Home]/Projects/`.
1. Extraiga el archivo en el `[User_Home]/Projects/[your-project]`directorio.
1. Vaya al directorio del ` [User_Home]/Projects/ `[proyecto]`/adobe-lc-mobileworkspace-src-[version]/ios` .
1. Abra el `AEM Forms.xcodeproj` proyecto en Xcode.
1. Haga clic en **AEM Forms** y, en **DESTINATARIOS**, seleccione **AEM Forms**. Seleccione la ficha **Configuración de compilación **, localice la sección Asignación de derechos **de firma de** código y, en los campos Depurar y liberar, realice una de las siguientes acciones:

   * Deje los campos sin especificar para crear una aplicación estándar de Mobile Workspace
   * Especifique los campos a los que se explica en [Creación de una aplicación segura de AEM Forms para iOS](/help/forms/using/building-secure-mobile-workspace-app.md) para crear una aplicación segura de AEM Forms.

1. En la ficha **Configuración** de compilación, haga clic en **Todo** y, a continuación, en **Combinado**.
1. En la lista **Configuración** , expanda Firma **de código**.
1. Para Identidad **de firma de** código, seleccione la firma adecuada. Para obtener información detallada sobre la creación de nuevas firmas, consulte [Creación y descarga de Perfiles](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)de provisión de desarrollo.
1. Asegúrese de que la misma firma está seleccionada para **Depurar**, **Versión** y **Cualquier SDK** de iOS.
1. Reemplace el siguiente código en el `AEM Forms-info.plist` archivo:

   ```java
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   con lo siguiente mientras sustituye `yourserver.com` por un nombre de host adecuado para su servidor.

   ```java
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
   >Este paso solo es necesario si la aplicación de AEM Forms necesita conectarse a un servidor que no cumpla los requisitos de seguridad de transporte de aplicaciones.

1. En **PROJECT**, seleccione **AEM Forms** y asegúrese de que la firma adecuada está seleccionada para Identidad **de firma de** código, **Depurar**, **Liberar** **** y Cualquier SDK de iOS.
1. Conecte un iPad aprovisionado a un ordenador Mac.
1. Seleccione el dispositivo aprovisionado para el proyecto de **AEM Forms** .

   ![ipad](assets/ipad.png)

   Se ha seleccionado un dispositivo suministrado, iPad Air 2.

1. Seleccione **Producto** > **Limpiar**.
1. Seleccione **Producto** > **Generar**.

## Creación del instalador para la aplicación de AEM Forms {#build-the-installer-for-the-mobile-workspace-app}

Debe archivar el proyecto Xcode para crear el archivo de instalación (archivo .ipa) y una lista de propiedades (archivo .plist). El archivo de lista de propiedades contiene información de configuración de la aplicación interna alojada, como el nombre y la ubicación de alojamiento de la aplicación. Para obtener más información sobre el archivo de lista de propiedades, consulte [Acerca de los archivos](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)de Lista de propiedades de información.

1. Conecte un iPad aprovisionado a un ordenador Mac. Para obtener información detallada sobre el aprovisionamiento de un iPad, consulte [Creación y descarga de Perfiles de aprovisionamiento de desarrollo](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. Seleccione el dispositivo aprovisionado para el proyecto de **AEM Forms** .

   ![ipad-1](assets/ipad-1.png)

   Se ha seleccionado un dispositivo suministrado, iPad Air 2.

1. Seleccione **Producto** > **Limpiar**.
1. Seleccione **Producto** > **Generar**.
1. Seleccione **Producto** > **Archivar**.
1. En Organizador - Archivos, seleccione el archivo más reciente del proyecto y haga clic en **Distribuir**.
1. Seleccione **Guardar para la implementación** empresarial o ad-hoc como método de distribución y haga clic en **Siguiente**.
1. Seleccione la identidad **de firma** de código adecuada y haga clic en **Siguiente**. Haga clic en **Permitir** para aplicar la firma.
1. Proporcione el nombre de la aplicación y seleccione **Guardar para distribución** empresarial.
1. Proporcione la URL **de la** aplicación para la aplicación. Por ejemplo, para alojar la aplicación en un servidor CRX, proporcione la URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. En el campo **Título** , especifique AEM Forms.
1. Haga clic en **Guardar** y cierre Xcode.

   Se crea un archivo de instalación `AEM Forms.ipa`y un archivo de lista de propiedades `AEM Forms-info.plist`en la ubicación especificada.

1. Abra el `AEM Forms-info.plist` archivo en un editor.
1. Reemplace todos los espacios en la dirección URL del archivo .ipa con %20.
1. Guarde y cierre el `AEM Forms-info.plist` archivo.