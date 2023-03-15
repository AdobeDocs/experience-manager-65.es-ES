---
title: Agregar una marca de agua a los recursos digitales
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

# Marca de agua de recursos digitales {#watermarking}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=en) |
| AEM 6.5 | Este artículo |
| AEM 6.4 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/watermarking.html?lang=en) |

[!DNL Adobe Experience Manager Assets] permite agregar una marca de agua digital a los recursos que ayuda a los usuarios a verificar la autenticidad y la propiedad de los derechos de autor de los recursos. [!DNL Experience Manager Assets] admite texto para utilizarlo como marca de agua en archivos PNG y JPEG.

Para poder aplicar una marca de agua en los recursos, agregue el paso de marca de agua en [!UICONTROL Recurso de actualización DAM] flujo de trabajo.

1. Acceda a la [!DNL Experience Manager] interfaz de usuario de y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. Desde el **[!UICONTROL Modelos de flujo de trabajo]** , seleccione la **[!UICONTROL Recurso de actualización DAM]** flujo de trabajo y clic **[!UICONTROL Editar]**.

1. En el panel lateral, arrastre el **[!UICONTROL Agregar filigrana]** paso a la [!UICONTROL Recurso de actualización DAM] flujo de trabajo.

   ![Arrastre el [!UICONTROL Agregar filigrana] paso y añadir a [!UICONTROL Recurso de actualización DAM] workflow](assets/add_watermark_step_aem_assets.png)

   *Imagen: arrastre el [!UICONTROL Agregar filigrana] paso y añadir a [!UICONTROL Recurso de actualización DAM] flujo de trabajo.*

   >[!NOTE]
   >
   >Coloque el [!UICONTROL Agregar filigrana] paso en cualquier lugar antes de [!UICONTROL Procesar miniatura] paso.

1. Abra el **[!UICONTROL Agregar filigrana]** paso para mostrar sus propiedades.
1. En el **[!UICONTROL Argumentos]** , especifique valores válidos en los distintos campos, incluido texto, tipo de fuente, tamaño, color, posición, orientación, etc. Para confirmar los cambios, haga clic en **[!UICONTROL Listo]**.

   ![Proporcione los argumentos en el paso para agregar una marca de agua en [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *Imagen: proporcione los argumentos en el paso para agregar una marca de agua en [!DNL Assets].*

1. Guarde el **[!UICONTROL Recurso de actualización DAM]** flujo de trabajo con el paso filigrana.
1. Desde el [!DNL Assets] interfaz de usuario, cargue un recurso de ejemplo. La marca de agua aparece con el tamaño de fuente, el color, etc., en la posición configurada en los pasos anteriores.

Para marcar como agua documentos de PDF mediante programación o con información dinámica, considere la posibilidad de utilizar [Experience Manager Document Services](/help/forms/using/overview-aem-document-services.md) oferta.

## Sugerencias y limitaciones {#tips-limitations}

* Solo se admiten marcas de agua basadas en texto. Las imágenes no se utilizan como marcas de agua, aunque puede cargar imágenes al crear el [!UICONTROL Agregar proceso de filigrana].
* Solo se admiten archivos PNG y de JPEG para la marca de agua. Otros formatos de recurso no están marcados con agua.
