---
title: Adición de una marca de agua a los recursos digitales
description: Aprenda a utilizar la función de marca de agua para agregar una marca de agua digital a los recursos.
contentOwner: AG
role: Profesional empresarial, administrador
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Marcar los recursos digitales {#watermarking}

[!DNL Adobe Experience Manager Assets] le permite agregar una marca de agua digital a los recursos para ayudar a los usuarios a verificar la autenticidad y propiedad de los recursos protegida por derechos de autor. [!DNL Experience Manager Assets] admite texto que se utilizará como marca de agua en archivos PNG y JPEG.

Para poder aplicar una marca de agua en los recursos, agregue el paso de marca de agua en el flujo de trabajo [!UICONTROL DAM Update Asset] .

1. Acceda a la interfaz de usuario [!DNL Experience Manager] y vaya a **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. En la página **[!UICONTROL Workflow Models]**, seleccione el flujo de trabajo **[!UICONTROL DAM Update Asset]** y haga clic en **[!UICONTROL Edit]**.

1. En el panel lateral, arrastre el paso **[!UICONTROL Add Watermark]** al flujo de trabajo [!UICONTROL DAM Update Asset].

   ![Arrastre el paso  [!UICONTROL Agregar ] marca de agua y añádalo al flujo de trabajo de  [!UICONTROL recursos de actualización de ] DAM](assets/add_watermark_step_aem_assets.png)

   *Figura: Arrastre el paso  [!UICONTROL Agregar ] marca de agua y añádalo al flujo de trabajo de  [!UICONTROL recursos de actualización de ] DAM.*

   >[!NOTE]
   >
   >Coloque el paso [!UICONTROL Add Watermark] en cualquier lugar antes del paso [!UICONTROL Process Thumbnail].

1. Abra el paso **[!UICONTROL Agregar marca de agua]** para mostrar sus propiedades.
1. En la pestaña **[!UICONTROL Argumentos]**, especifique valores válidos en los distintos campos, como texto, tipo de fuente, tamaño, color, posición, orientación, etc. Para confirmar los cambios, haga clic en **[!UICONTROL Listo]**.

   ![Proporcione los argumentos en el paso agregar marca de agua de  [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *Figura: Proporcione los argumentos en el paso agregar marca de agua de  [!DNL Assets].*

1. Guarde el flujo de trabajo **[!UICONTROL DAM Update Asset]** con el paso de marca de agua.
1. Desde la interfaz de usuario [!DNL Assets], cargue un recurso de ejemplo. La marca de agua aparece con el tamaño de fuente, el color, etc., en la posición que configuró en los pasos anteriores.

Para marcar documentos PDF mediante programación o con información dinámica, considere la posibilidad de utilizar la oferta [Experience Manager Document Services](/help/forms/using/overview-aem-document-services.md).

## Sugerencias y limitaciones {#tips-limitations}

* Solo se admiten marcas de agua basadas en texto. Las imágenes no se utilizan como marcas de agua, aunque se pueden cargar imágenes al crear el [!UICONTROL Proceso de adición de marca de agua].
* Solo se admiten archivos PNG y JPEG con marca de agua. Otros formatos de recursos no están marcados con agua.
