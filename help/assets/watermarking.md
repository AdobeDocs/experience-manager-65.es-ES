---
title: Añada una marca de agua en los recursos digitales.
description: Aprenda a utilizar la función de marca de agua para añadir una marca de agua digital a los recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Marcar sus recursos digitales {#watermarking}

[!DNL Adobe Experience Manager Assets] le permite agregar una marca de agua digital a los recursos para ayudar a los usuarios a verificar la autenticidad y propiedad de los derechos de autor de los recursos. [!DNL Experience Manager Assets] admite texto que se va a utilizar como marca de agua en archivos PNG y JPEG.

Para poder aplicar marcas de agua a los recursos, agregue el paso de la marca de agua en el flujo de trabajo de recursos [!UICONTROL de actualización de] DAM.

1. Acceda a la [!DNL Experience Manager] interfaz de usuario y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página Modelos **[!UICONTROL de]** flujo de trabajo, seleccione el flujo de trabajo de recursos **[!UICONTROL de actualización de]** DAM y haga clic en **[!UICONTROL Editar]**.

1. En el panel lateral, arrastre el paso **[!UICONTROL Añadir marca de agua]** al flujo de trabajo de actualización de recursos [!UICONTROL de] DAM.

   ![Arrastre el paso [!UICONTROL Añadir marca de agua] y añádalo al flujo de trabajo de recursos [!UICONTROL de actualización de] DAM](assets/add_watermark_step_aem_assets.png)2
   *Figura: Arrastre el paso[!UICONTROL Añadir marca de agua]y añádalo al flujo de trabajo de recursos[!UICONTROL de actualización de]DAM.*

   >[!NOTE]
   >
   >Coloque el paso [!UICONTROL Añadir marca de agua] en cualquier lugar antes del paso [!UICONTROL Procesar miniatura] .

1. Abra el paso **[!UICONTROL Añadir marca de agua]** para mostrar sus propiedades.
1. En la ficha **[!UICONTROL Argumentos]** , especifique valores válidos en los distintos campos, como texto, tipo de fuente, tamaño, color, posición, orientación, etc. Para confirmar los cambios, haga clic en **[!UICONTROL Hecho]**.

   ![Proporcione los argumentos en el paso de adición de marca de agua en Recursos](assets/arguments_add_watermark_aem_assets.png)

   *Figura: Proporcione los argumentos del paso de adición de marca de agua en[!DNL Assets].*

1. Save the **[!UICONTROL DAM Update Asset]** workflow with the watermark step.
1. En la interfaz de usuario, cargue un recurso de ejemplo. [!DNL Assets] La marca de agua aparece con el tamaño de fuente, el color, etc., en la posición configurada en los pasos anteriores.

Para marcar documentos PDF mediante programación o con información dinámica, considere la posibilidad de utilizar la oferta de servicios [de Documento de](/help/forms/using/overview-aem-document-services.md) Experience Manager.
