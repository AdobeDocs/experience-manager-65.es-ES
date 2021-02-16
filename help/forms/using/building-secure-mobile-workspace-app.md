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
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---


# Creación de una aplicación segura de AEM Forms para iOS {#building-a-secure-aem-forms-app-for-ios}

Debe archivar el proyecto Xcode para la aplicación de AEM Forms para crear el archivo de instalación (archivo .ipa) y una lista de propiedades (archivo .plist). El archivo de lista de propiedades contiene información de configuración de la aplicación interna alojada, como el nombre y la ubicación de alojamiento de la aplicación. Para obtener más información sobre el archivo de lista de propiedades, consulte [Acerca de los archivos de Lista de propiedades de información](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Inicie sesión en el siguiente sitio web:

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. Cree un ID de aplicación. Para ver los pasos detallados para crear un ID de aplicación, consulte [Creación y configuración de ID de aplicación](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. Para configurar el identificador del paquete para la aplicación iOS para su aplicación, haga clic en **[!UICONTROL Configurar ID de aplicación]**.
1. En la parte inferior de la página web, seleccione **[!UICONTROL Habilitar para protección de datos]**. Especifique las opciones de protección de datos.

   Haga clic en **[!UICONTROL Listo]**.

1. Vaya a Provisioning->Distribution y cree un Perfil nuevo con el ID de la aplicación configurado en el paso 3.
1. Descargue y agregue el perfil de aprovisionamiento al Xcode y al iPad.
1. Inicie sesión en el equipo Mac que tenga Xcode y iOS SDK instalados y configurados.
1. Abra el proyecto `AEM Forms.xcodeproj` en Xcode.
1. Haga clic en **[!UICONTROL AEM Forms]**, en **[!UICONTROL DESTINATARIOS]**, seleccione **[!UICONTROL AEM Forms]**. Seleccione la ficha **[!UICONTROL Configuración de compilación]**, busque la sección **[!UICONTROL Asignación de derechos de firma de código]** y, en el menú desplegable Asignación de derechos, seleccione la opción **[!UICONTROL Empresa de LC]**.
1. Busque y abra el archivo `LC Enterprise.entitlements` en el Xcode para editarlo. En **autorizaciones de XCode**, agregue el mismo par clave-valor que está presente en el perfil de aprovisionamiento.
1. En la ficha **[!UICONTROL Configuración de compilación]**, haga clic en **[!UICONTROL Todo]** y, a continuación, haga clic en **[!UICONTROL Combinado]**.
1. En la lista **[!UICONTROL Settings]**, expanda **[!UICONTROL Code Signing]**.
1. Para **[!UICONTROL Identidad de firma de código]**, seleccione la firma adecuada. Asegúrese de que la misma firma está seleccionada para **[!UICONTROL Depurar]**, **[!UICONTROL Versión]** y **[!UICONTROL Cualquier SDK para iOS]**.
1. En **[!UICONTROL PROJECT]**, seleccione **[!UICONTROL AEM Forms]** y asegúrese de que la firma apropiada está seleccionada para **[!UICONTROL Identidad de firma de código]**, **[!UICONTROL Depurar]**, **[!UICONTROL Versión]** y **[!UICONTROL Cualquier SDK para iOS]**.
1. Compilación y distribución de aplicaciones de AEM Forms. Para obtener instrucciones detalladas sobre cómo crear y distribuir aplicaciones de AEM Forms, consulte [Compilación del instalador para la aplicación de AEM Forms](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app).
