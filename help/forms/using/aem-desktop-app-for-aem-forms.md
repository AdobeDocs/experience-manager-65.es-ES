---
title: Aplicación de escritorio de Adobe Experience Manager AEM () para AEM Forms
description: Aplicación de escritorio de Adobe Experience Manager AEM () para AEM Forms
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
noindex: true
role: Admin
exl-id: b87e07b1-4a19-4888-bad0-c0f5327b9ad3
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 86%

---

# Aplicación de escritorio de Adobe Experience Manager AEM () para AEM Forms {#aem-desktop-app-for-aem-forms}

La aplicación de escritorio de AEM le permite asignar el repositorio de recursos de Adobe Experience Manager (AEM) y los archivos binarios de AEM Forms a un directorio de red del sistema. Puede ver los recursos sincronizados y los archivos binarios en un explorador de archivos y usar varias aplicaciones para editar los archivos como desee. Además de ver los archivos, también puede crear, cargar y eliminar los archivos binarios. También puede abrir, editar y guardar archivos directamente desde el software. Por ejemplo, puede abrir y editar directamente un archivo XDP desde Designer. Los cambios que realice en los recursos localmente se reflejarán en el repositorio de AEM Assets y en la interfaz de usuario de AEM Forms.

Puede descargar la aplicación desde una instancia de AEM. Para obtener información detallada sobre cómo descargar la aplicación, consulte [Notas de la versión de la aplicación de escritorio de AEM](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=en).

## Recursos de AEM Forms compatibles con la aplicación de escritorio de AEM {#aem-forms-assets-supported-in-aem-desktop-app}

Puede utilizar la aplicación para sincronizar archivos binarios de AEM Forms del siguiente tipo: Plantillas de formulario (.xdp), Formulario PDF (.pdf), Documento (.pdf), Imágenes, Esquema XML (.xsd), Hojas de estilo (.xfs). La aplicación enumera todos los demás archivos (archivos no compatibles) como archivos de 0 bytes. La lista de archivos no compatibles como los archivos de 0 bytes garantiza que el usuario conozca la existencia de otros recursos disponibles en el servidor de AEM Forms.

>[!NOTE]
>
>Un nombre de archivo solo puede contener caracteres alfanuméricos, guiones o guiones bajos.

## Habilitar AEM Forms para la aplicación de escritorio de AEM {#enable-aem-forms-for-aem-desktop-app}

La aplicación de escritorio de AEM utiliza el protocolo WebDAV en Microsoft Windows y SMB1 en Mac OS X para conectarse a un servidor de AEM Forms. De serie, el servidor de AEM Forms no está habilitado para sincronizar archivos binarios y otros recursos con un cliente WebDAV o SMB. Siga estos pasos para habilitar AEM Forms para la aplicación de escritorio de AEM:

1. Inicie sesión en AEM Forms como administrador.
1. En la instancia de autor, haga clic en ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > Herramientas]** ![hammer](assets/hammer.png) **[!UICONTROL > Implementación > Operaciones> Consola Web]**. La consola web se abre en una nueva ventana.
1. En la ventana de la consola web, busque y abra la opción **[!UICONTROL Configuración del complemento FormsManager]**.
1. En el cuadro de diálogo Configuración del complemento FormsManager, anule la selección de **[!UICONTROL Sincronizar recursos asincrónicamente]** y haga clic en **[!UICONTROL Guardar]**.
1. Reinicie el servidor de AEM Forms. Después reiniciarlo, el servidor de AEM Forms estará habilitado para aceptar y compartir contenido con la aplicación de escritorio de AEM.
1. Abra la aplicación y conéctese al servidor de AEM Forms.

   Si la conexión se realiza correctamente, la aplicación rellenará las carpetas `content/dam` y `content/dam/formsanddocuments`. Además de mover archivos de carpetas anteriores a carpetas locales y a la inversa, puede utilizar la aplicación para mover contenido entre carpetas rellenadas automáticamente.
