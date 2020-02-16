---
title: Creación de una aplicación segura de AEM Forms para iOS
seo-title: Creación de una aplicación segura de AEM Forms para iOS
description: Pasos para crear una aplicación segura de AEM Forms.
seo-description: Pasos para crear una aplicación segura de AEM Forms.
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
translation-type: tm+mt
source-git-commit: 4a0f3f64095b4726f295a0c1857a1e999353f5f5

---


# Creación de una aplicación segura de AEM Forms para iOS {#building-a-secure-aem-forms-app-for-ios}

Debe archivar el proyecto Xcode para la aplicación de AEM Forms para crear el archivo de instalación (archivo .ipa) y una lista de propiedades (archivo .plist). El archivo de lista de propiedades contiene información de configuración de la aplicación interna alojada, como el nombre y la ubicación de alojamiento de la aplicación. Para obtener más información sobre el archivo de lista de propiedades, consulte [Acerca de los archivos](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)de lista de propiedades de información.

1. Inicie sesión en el siguiente sitio web:

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. Cree un ID de aplicación. Para ver los pasos detallados para crear un ID de aplicación, consulte [Creación y configuración de ID](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html)de aplicación.
1. Para configurar el identificador del paquete para la aplicación iOS para su aplicación, haga clic en **[!UICONTROL Configurar ID]** de aplicación.
1. En la parte inferior de la página web, seleccione **[!UICONTROL Activar para protección]** de datos. Especifique las opciones de protección de datos.

   Haga clic en **[!UICONTROL Finalizado]**.

1. Vaya a Provisioning->Distribution y cree un nuevo perfil con el ID de la aplicación configurado en el paso 3.
1. Descargue y agregue el perfil de datos al Xcode y al iPad.
1. Inicie sesión en el equipo Mac que tenga Xcode y iOS SDK instalados y configurados.
1. Abra el `AEM Forms.xcodeproj` proyecto en Xcode.
1. Haga clic en **[!UICONTROL AEM Forms]**, en **[!UICONTROL TARGET]**, seleccione **[!UICONTROL AEM Forms]**. Seleccione la ficha **[!UICONTROL Generar configuración]** , busque la sección Asignación de derechos **[!UICONTROL de firma de]** código y, en el menú desplegable Asignación de derechos, seleccione la opción Empresa **** LC.
1. Busque y abra el `LC Enterprise.entitlements` archivo en el Xcode para editarlo. En las autorizaciones **de** XCode, agregue el mismo par clave-valor que está presente en el perfil de datos.
1. En la ficha **[!UICONTROL Configuración]** de compilación, haga clic en **[!UICONTROL Todo]** y, a continuación, en **[!UICONTROL Combinado]**.
1. En la lista **[!UICONTROL Configuración]** , expanda Firma **[!UICONTROL de código]**.
1. Para Identidad **[!UICONTROL de firma de]** código, seleccione la firma adecuada. Asegúrese de que la misma firma está seleccionada para **[!UICONTROL Depurar]**, **[!UICONTROL Versión]** y **[!UICONTROL Cualquier SDK]** de iOS.
1. En **[!UICONTROL PROJECT]**, seleccione **[!UICONTROL AEM Forms]** y asegúrese de que la firma adecuada está seleccionada para Identidad **[!UICONTROL de firma de]** código, **[!UICONTROL Depurar]**, **[!UICONTROL Liberar]** **** y Cualquier SDK de iOS.
1. Compilación y distribución de aplicaciones de AEM Forms. Para obtener instrucciones detalladas sobre cómo crear y distribuir la aplicación de AEM Forms, consulte [Compilación del instalador para la aplicación](/help/forms/using/setup-xcode-project-build-installer.md#main-pars-text-12)de AEM Forms.

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
