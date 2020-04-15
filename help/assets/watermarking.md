---
title: Añada una marca de agua en los recursos digitales.
description: Aprenda a utilizar la función de marca de agua para añadir una marca de agua digital a los recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# Marcar sus recursos digitales {#watermarking}

Recursos Adobe Experience Manager (AEM) le permite agregar una marca de agua digital a los recursos para ayudar a los usuarios a comprobar la autenticidad y propiedad de los recursos con copyright. AEM Assets admite texto que se va a utilizar como marca de agua en archivos PNG y JPEG.

Para poder aplicar marcas de agua a los recursos, agregue el paso de la marca de agua en el flujo de trabajo de recursos [!UICONTROL de actualización de] DAM.

1. Acceda a la interfaz de usuario de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página Modelos **[!UICONTROL de]** flujo de trabajo, seleccione el flujo de trabajo de recursos **[!UICONTROL de actualización de]** DAM y haga clic en **[!UICONTROL Editar]**.

1. En el panel lateral, arrastre el paso **[!UICONTROL Añadir marca de agua]** al flujo de trabajo de actualización de recursos [!UICONTROL de] DAM.

   ![Arrastre el paso [!UICONTROL Añadir marca de agua] y añádalo al flujo de trabajo del recurso [!UICONTROL de actualización de] DAM](assets/add_watermark_step_aem_assets.png)2
   *Figura: Arrastre el paso[!UICONTROL Añadir marca de agua]y añádalo al flujo de trabajo del recurso[!UICONTROL de actualización de]DAM*

   >[!NOTE]
   >
   >Coloque el paso [!UICONTROL Añadir marca de agua] en cualquier lugar antes del paso [!UICONTROL Procesar miniatura] .

1. Abra el paso **[!UICONTROL Añadir marca de agua]** para mostrar sus propiedades.
1. En la ficha **[!UICONTROL Argumentos]** , especifique valores válidos en los distintos campos, como texto, tipo de fuente, tamaño, color, posición, orientación, etc. Para confirmar los cambios, toque o haga clic en el icono Listo.

   ![Proporcione los argumentos en el paso de adición de marca de agua en Recursos](assets/arguments_add_watermark_aem_assets.png)

   *Figura: Proporcione los argumentos en el paso de adición de marca de agua en Recursos*

1. Save the **[!UICONTROL DAM Update Asset]** workflow with the watermark step.
1. En la interfaz de usuario de Recursos, cargue un recurso de ejemplo. La marca de agua aparece con el tamaño de fuente, el color, etc., en la posición configurada en los pasos anteriores.
