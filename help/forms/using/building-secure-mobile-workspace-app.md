---
title: Creación de una aplicación segura de AEM Forms para iOS
seo-title: Building a secure AEM Forms app for iOS
description: Pasos para crear una aplicación segura de AEM Forms.
seo-description: Steps to build a secure AEM Forms app.
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
exl-id: 12cc2027-ae94-40c3-a7d1-553469426114
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# Creación de una aplicación segura de AEM Forms para iOS {#building-a-secure-aem-forms-app-for-ios}

Debe archivar el proyecto Xcode para la aplicación AEM Forms para crear el archivo instalador (un archivo .ipa) y un archivo de lista de propiedades (un archivo .plist). El archivo de lista de propiedades contiene información de configuración de la aplicación interna alojada, como el nombre y la ubicación de alojamiento de la aplicación. Para obtener más información sobre el archivo de lista de propiedades, consulte [Acerca de los archivos de lista de propiedades de información](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Inicie sesión en el siguiente sitio web:

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. Crear un ID de aplicación. Para ver los pasos detallados para crear un ID de aplicación, consulte [Creación y configuración de ID de aplicación](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. Para configurar el identificador del paquete para la aplicación iOS de su aplicación, haga clic en **[!UICONTROL Configurar ID de aplicación]**.
1. En la parte inferior de la página web, seleccione **[!UICONTROL Habilitar para la protección de datos]**. Especifique las opciones de protección de datos.

   Haga clic en **[!UICONTROL Listo]**.

1. Vaya a Provisioning->Distribution y cree un nuevo perfil con el ID de aplicación configurado en el paso 3.
1. Descargue y añada el perfil de aprovisionamiento al Xcode y al iPad.
1. Inicie sesión en el equipo de Mac que tenga Xcode y iOS SDK instalados y configurados.
1. Abra el `AEM Forms.xcodeproj` proyecto en Xcode.
1. Haga clic en **[!UICONTROL AEM Forms]**, en **[!UICONTROL OBJETIVOS]**, seleccione **[!UICONTROL AEM Forms]**. Seleccione el **[!UICONTROL Configuración de compilación]** , busque **[!UICONTROL Derecho de firma de código]** y, en la lista desplegable Derechos , seleccione la opción **[!UICONTROL LC Enterprise]** .
1. Busque y abra el `LC Enterprise.entitlements` en el Xcode para editarlo. En el **Derechos XCode**, agregue el mismo par clave-valor que está presente en el perfil de aprovisionamiento.
1. En el **[!UICONTROL Configuración de compilación]** , haga clic en **[!UICONTROL Todo]** y haga clic en **[!UICONTROL Combinado]**.
1. En el **[!UICONTROL Configuración]** lista, expandir **[!UICONTROL Firma de código]**.
1. Para **[!UICONTROL Identidad de firma de código]**, seleccione la firma adecuada. Asegúrese de que se ha seleccionado la misma firma para **[!UICONTROL Depuración]**, **[!UICONTROL Versión]** y **[!UICONTROL Cualquier SDK de iOS]**.
1. En **[!UICONTROL PROYECTO]**, seleccione **[!UICONTROL AEM Forms]** y asegúrese de que la firma adecuada está seleccionada para **[!UICONTROL Identidad de firma de código]**, **[!UICONTROL Depuración]**, **[!UICONTROL Versión]** y **[!UICONTROL Cualquier SDK de iOS]**.
1. Compile y distribuya la aplicación de AEM Forms. Para obtener instrucciones detalladas sobre la compilación y distribución de la aplicación de AEM Forms, consulte [Creación del instalador para la aplicación AEM Forms](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app).
