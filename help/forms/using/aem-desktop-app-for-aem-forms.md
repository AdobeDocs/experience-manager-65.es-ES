---
title: Aplicación de escritorio AEM para AEM Forms
seo-title: Aplicación de escritorio AEM para AEM Forms
description: nulo
seo-description: nulo
uuid: 99e0f2fb-8623-45bb-8e2e-5c5d6f482366
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
discoiquuid: c30332b6-e012-442d-8e84-28832c116c7b
noindex: true
translation-type: tm+mt
source-git-commit: 3460909eb77cc078b728d1af4becd47cc4377b73

---


# Aplicación de escritorio AEM para AEM Forms {#aem-desktop-app-for-aem-forms}

La aplicación de escritorio de AEM le permite asignar el repositorio de recursos de Adobe Experience Manager (AEM) y los archivos binarios de AEM Forms a un directorio de red del sistema. Puede ver los recursos sincronizados y los archivos binarios en un explorador de archivos y utilizar varias aplicaciones para editar los archivos como desee. Además de ver los archivos, también puede crear, cargar y eliminar los archivos binarios. También puede abrir, editar y guardar archivos directamente desde el software. Por ejemplo, puede abrir y editar directamente un archivo XDP desde Designer. Los cambios realizados en los recursos localmente se reflejan en el repositorio de AEM Assets y en la interfaz de usuario de AEM Forms.

Puede descargar la aplicación desde una instancia de AEM. Para obtener información detallada sobre la descarga de la aplicación, consulte Notas [de la versión de la aplicación de escritorio de](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html)AEM.

## Recursos de AEM Forms admitidos en la aplicación de escritorio de AEM {#aem-forms-assets-supported-in-aem-desktop-app}

Puede utilizar la aplicación para sincronizar archivos binarios de AEM Forms de los siguientes tipos: Plantillas de formulario (.xdp), Formulario PDF (.pdf), Documento (.pdf), Imágenes, Esquema XML (.xsd), Hojas de estilo (.xfs). La aplicación muestra todos los demás archivos (archivos no admitidos) como archivos de 0 bytes. La lista de archivos no admitidos como archivos de 0 bytes garantiza que el usuario conozca la existencia de otros recursos disponibles en el servidor de AEM Forms.

>[!NOTE]
>
>Un nombre de archivo solo puede contener caracteres alfanuméricos, guiones o guiones bajos.

## Habilitar AEM Forms para la aplicación de escritorio de AEM {#enable-aem-forms-for-aem-desktop-app}

AEM Desktop App utiliza el protocolo WebDAV en Microsoft Windows y SMB1 en Mac OS X para conectarse a un servidor de AEM Forms. De forma predeterminada, el servidor de AEM Forms no está habilitado para sincronizar archivos binarios y otros recursos con un cliente WebDAV o SMB. Siga estos pasos para activar AEM Forms para la aplicación de escritorio de AEM:

1. Inicie sesión en AEM Forms como administrador.
1. En la instancia de autor, haga clic en ![adobeexperience emanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > Herramientas]** ![martillo](assets/hammer.png) **[!UICONTROL > Implementación > Operaciones > Consola]** web. La consola web se abre en una ventana nueva.
1. En la ventana de la consola web, busque y abra la opción de configuración **[!UICONTROL de]** FormsManager AddOn.
1. En el cuadro de diálogo Configuración de FormsManager AddOn, desactive la casilla de verificación Sincronizar recursos **** asincrónicamente y haga clic en **[!UICONTROL Guardar]**.
1. Reinicie el servidor de AEM Forms. Tras el reinicio, el servidor de AEM Forms está habilitado para aceptar y compartir contenido con la aplicación de escritorio de AEM.
1. Abra la aplicación y conéctese al servidor de AEM Forms.

   Si la conexión es correcta, la aplicación rellena las `content/dam` carpetas y `content/dam/formsanddocuments` . Junto con mover archivos de carpetas anteriores a carpetas locales y viceversa, puede utilizar la aplicación para mover contenido entre carpetas rellenadas automáticamente.

