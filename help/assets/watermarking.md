---
title: Adición de una marca de agua a los recursos digitales
description: Aprenda a utilizar la función de marca de agua para agregar una marca de agua digital a los recursos.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 3%

---

# Marcar sus recursos digitales {#watermarking}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=en) |
| AEM 6.5 | Este artículo |
| AEM 6.4 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/watermarking.html?lang=en) |

[!DNL Adobe Experience Manager Assets] le permite agregar una marca de agua digital a los recursos para ayudar a los usuarios a verificar la autenticidad y propiedad de los recursos protegida por derechos de autor. [!DNL Experience Manager Assets] admite texto que se utilizará como marca de agua en archivos PNG y JPEG.

Para poder aplicar una marca de agua a los recursos, agregue el paso de marca de agua en el [!UICONTROL Recurso de actualización DAM] flujo de trabajo.

1. Acceda a la [!DNL Experience Manager] interfaz de usuario y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En el **[!UICONTROL Modelos de flujo de trabajo]** seleccione **[!UICONTROL Recurso de actualización DAM]** flujo de trabajo y haga clic en **[!UICONTROL Editar]**.

1. En el panel lateral, arrastre el **[!UICONTROL Agregar marca de agua]** paso a [!UICONTROL Recurso de actualización DAM] flujo de trabajo.

   ![Arrastre el [!UICONTROL Agregar marca de agua] y añada al [!UICONTROL Recurso de actualización DAM] flujo de trabajo](assets/add_watermark_step_aem_assets.png)

   *Figura: Arrastre el [!UICONTROL Agregar marca de agua] y añada al [!UICONTROL Recurso de actualización DAM] flujo de trabajo.*

   >[!NOTE]
   >
   >Coloque el [!UICONTROL Agregar marca de agua] pase a cualquier lugar antes de que [!UICONTROL Miniatura de proceso] paso a paso.

1. Abra el **[!UICONTROL Agregar marca de agua]** para mostrar sus propiedades.
1. En el **[!UICONTROL Argumentos]** , especifique valores válidos en los distintos campos, como texto, tipo de fuente, tamaño, color, posición, orientación, etc. Para confirmar los cambios, haga clic en **[!UICONTROL Listo]**.

   ![Proporcione los argumentos en el paso agregar marca de agua de [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *Figura: Proporcione los argumentos en el paso agregar marca de agua de [!DNL Assets].*

1. Guarde el **[!UICONTROL Recurso de actualización DAM]** flujo de trabajo con el paso de marca de agua.
1. En el [!DNL Assets] interfaz de usuario de , cargue un recurso de ejemplo. La marca de agua aparece con el tamaño de fuente, el color, etc., en la posición que configuró en los pasos anteriores.

Para marcar con agua documentos de PDF mediante programación o con información dinámica, considere la posibilidad de utilizar [Servicios de documentos de Experience Manager](/help/forms/using/overview-aem-document-services.md) oferta.

## Sugerencias y limitaciones {#tips-limitations}

* Solo se admiten marcas de agua basadas en texto. Las imágenes no se utilizan como marcas de agua, aunque se pueden cargar imágenes al crear la variable [!UICONTROL Agregar proceso de marca de agua].
* Solo se admiten archivos PNG y JPEG para marcar con agua. Otros formatos de recursos no están marcados con agua.
