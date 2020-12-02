---
title: Cambio del contenido de página cero en Designer
seo-title: Cambio del contenido de página cero en Designer
description: ¿Sabe cómo puede cambiar el mensaje mostrado en la página cero de un archivo PDF XFA al visualizarlo en un visor que no es de Adobe PDF?
seo-description: ¿Sabe cómo puede cambiar el mensaje mostrado en la página cero de un archivo PDF XFA al visualizarlo en un visor que no es de Adobe PDF?
uuid: ac23fb21-3f15-48ea-aeeb-4ecc12b771ac
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 56b6a573-8aba-43e7-acb7-c2da45869d95
docset: aem65
translation-type: tm+mt
source-git-commit: 3cbcd23254e16231a199276aa2f9e70d6ff39b34
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---


# Cambio del contenido de Página cero en Designer {#changing-page-zero-content-in-designer}

El contenido de Página cero se muestra de forma predeterminada cuando un visor que no es de Adobe PDF, como el visor de PDF predeterminado en [!DNL Chrome] o [!DNL Firefox], no puede leer el contenido del formulario PDF/XFA. El mensaje predeterminado Página cero se muestra a continuación.

![defaultpage0message](assets/defaultpage0message.png)

[!DNL AEM Forms] la versión de Designer permite cambiar el mensaje que se muestra en la página cero. Para cambiar el mensaje Página cero, realice los siguientes pasos:

1. Asegúrese de tener instalada la versión [!DNL AEM Forms] de Designer. Puede comprobar la versión desde la pantalla Acerca de del diseñador.

1. Abra el formulario para el que desea cambiar el contenido de Página cero.

1. Haga clic en **[!UICONTROL Archivo]** > **[!UICONTROL Propiedades del formulario]**.

1. En el cuadro de diálogo [!UICONTROL Propiedades del formulario], haga clic en ![más](assets/plus.png) (icono de signo más) para agregar una propiedad personalizada.

1. Especifique **_pagezerocontent** como nombre de la propiedad.
1. Añada el nuevo mensaje Página cero, en formato de texto enriquecido, como valor. Por ejemplo:


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. Guarde el formulario como PDF.

1. Vista el formulario PDF en el navegador para confirmar que el mensaje se ha actualizado. El valor de ejemplo anterior aparece de la siguiente manera:

   ![change message](assets/changedmessage.png)

>[!NOTE]
>
>Es posible que la propiedad personalizada que acaba de crear no aparezca correctamente en el cuadro de diálogo Propiedades del formulario al volver a abrir el formulario. Sin embargo, funciona bien y el formulario muestra el mensaje Página cero actualizado.
