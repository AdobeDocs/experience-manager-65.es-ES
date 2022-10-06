---
title: Productor de catálogos
seo-title: Catalog Producer
seo-description: Learn how to use Catalog Producer in AEM Assets to generate product catalogs using your digital assets.
uuid: da822d83-8b99-4089-ae1b-11d897d4044e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 90e36522-3af1-4a8a-b044-1c828c52974e
description: Productor de catálogos
exl-id: 76a46c62-d47d-4970-8a3a-d56015639548
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---

# Productor de catálogos{#catalog-producer}

Aprenda a utilizar Catalog Producer en AEM Assets para generar catálogos de productos con sus recursos digitales.

Con Adobe Experience Manager (AEM) Assets Catalog Producer, puede crear catálogos para sus productos de marca mediante plantillas de InDesign importadas desde una aplicación de InDesign. Para importar plantillas de InDesign, primero integre AEM Assets con un servidor de InDesign.

## Integración con el servidor de InDesign {#integrating-with-indesign-server}

Como parte del proceso de integración, configure la variable **Recurso de actualización DAM** flujo de trabajo, adecuado para la integración con InDesign. Además, configure un trabajador proxy para el servidor de InDesign. Para obtener más información, consulte [Integración de AEM Assets con InDesign Server](/help/assets/indesign.md).

>[!NOTE]
>
>Puede generar plantillas de InDesign a partir de archivos de InDesign antes de importarlas a AEM Assets. Para obtener más información, consulte [Uso de archivos y plantillas](https://helpx.adobe.com/indesign/using/files-templates.html).
>
>Puede asignar los elementos de las plantillas de InDesign a las etiquetas XML. Las etiquetas asignadas se muestran como propiedades cuando se asignan propiedades de producto con propiedades de plantilla en Catalog Producer. Para obtener más información sobre el etiquetado XML en los archivos de InDesign, consulte [Etiquetado de contenido para XML](https://helpx.adobe.com/indesign/using/tagging-content-xml.html).

>[!NOTE]
>
>Solo se utilizan como plantillas los archivos de InDesign (.indd). Los archivos con la extensión .indt no son compatibles.

## Creación de un catálogo {#creating-a-catalog}

Catalog Producer utiliza datos de administración de información de producto (PIM) para asignar propiedades de producto con las propiedades XML mostradas en la plantilla. Para crear un catálogo, siga estos pasos:

1. En la interfaz de usuario de Assets, toque o haga clic en el botón **Logotipo de AEM** y vaya a **Assets > Catálogos**.
1. En el **Catálogos** página, toque o haga clic **Crear** en la barra de herramientas y, a continuación, seleccione **Catálogo** de la lista.
1. En el **Crear catálogo** , introduzca un nombre y una descripción (opcional) para el catálogo y especifique las etiquetas, si las hay. También puede añadir una imagen en miniatura para el catálogo.

   ![create_catalog](assets/create_catalog.png)

1. Toque o haga clic **Guardar**. Un cuadro de diálogo de confirmación notifica que se ha creado el catálogo. Toque o haga clic **Listo** para cerrar el cuadro de diálogo.
1. Para abrir el catálogo que ha creado, toque o haga clic en él desde el **Catálogos** página.

   >[!NOTE]
   >
   >Para abrir el catálogo, también puede tocar o hacer clic en **Apertura** en el cuadro de diálogo de confirmación mencionado en el paso anterior.

1. Para añadir páginas al catálogo, toque o haga clic en **Crear** en la barra de herramientas y, a continuación, elija la **Nueva página** .
1. En el asistente, seleccione una plantilla de InDesign para la página. A continuación, toque o haga clic en **Siguiente**.
1. Especifique un nombre para la página y una descripción opcional. Especifique las etiquetas, si las hay.
1. Toque o haga clic en el botón **Crear** en la barra de herramientas. A continuación, toque o haga clic en **Apertura** del cuadro de diálogo. Las propiedades del producto se muestran en el panel izquierdo. Las propiedades predefinidas para la plantilla de InDesign aparecen en el panel derecho.
1. En el panel izquierdo, arrastre las propiedades del producto a las propiedades de la plantilla de InDesign y cree una asignación entre ellas.

   Para ver cómo aparece la página en tiempo real, toque o haga clic en el botón **Vista previa** en el panel derecho.

1. Para crear más páginas, repita los pasos del 6 al 9. Para crear páginas similares para otros productos, seleccione la página y toque o haga clic en el botón **Crear páginas similares** de la barra de herramientas.

   ![create_similar_pages](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >Solo puede crear páginas similares para productos con una estructura similar.

   Toque o haga clic en el icono Agregar , seleccione productos del selector de productos y, a continuación, toque o haga clic en **Select** en la barra de herramientas.

   ![select_product](assets/select_product.png)

1. En la barra de herramientas, toque o haga clic en **Crear**. Toque o haga clic **Listo** para cerrar el cuadro de diálogo. En el catálogo se incluyen páginas similares.
1. Para agregar cualquier archivo de InDesign existente al catálogo, toque o haga clic en **Crear** en la barra de herramientas, y seleccione **Agregar a una página existente** .
1. Seleccione el archivo de InDesign y pulse o haga clic en **Agregar** en la barra de herramientas. A continuación, toque o haga clic en **OK** para cerrar el cuadro de diálogo.

   Si se cambian los metadatos de los productos a los que hace referencia en las páginas del catálogo, los cambios no se reflejan automáticamente en las páginas del catálogo. Un banner etiquetado **Stale** aparece en las imágenes del producto en las páginas del catálogo de referencia, lo que indica que los metadatos de los productos a los que se hace referencia no están actualizados.

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   Para asegurarse de que las imágenes de producto reflejan los cambios más recientes en los metadatos, seleccione la página en la consola Catálogo y pulse o haga clic en el **Actualizar página** de la barra de herramientas.

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >Para cambiar los metadatos de un producto al que se hace referencia, vaya a la consola Productos (**Logotipo AEM** > **Comercio** > **Productos**) y seleccione el producto. A continuación, toque o haga clic en el **Ver propiedades** de la barra de herramientas y edite los metadatos en la página Propiedades del recurso.

1. Para reorganizar las páginas en el catálogo, toque o haga clic en el botón **Crear** en la barra de herramientas y, a continuación, elija **Combinar** del menú . En el asistente, el carrusel de la parte superior le permite reordenar las páginas arrastrándolas. También puede eliminar páginas.

1. Toque o haga clic **Siguiente**. Para añadir un archivo de InDesign existente como portada, toque o haga clic en **Examinar** al lado del **Elegir página de portada** y especifique la ruta para la plantilla de portada.
1. Toque o haga clic **Guardar** y, a continuación, toque o haga clic **Listo** para cerrar el cuadro de diálogo de confirmación.
Al seleccionar la variable **Listo** , se abre un cuadro de diálogo para seleccionar si desea la representación en .pdf.
   ![exportación a pdf](assets/CatalogPDF.png)
Si la opción Acrobat(PDF) está seleccionada, se crea una representación en pdf en  **/jcr:content/renditions** además de la representación de indesign. Puede descargar todas las representaciones seleccionando la casilla &quot;Representaciones&quot; en el cuadro de diálogo de descarga.

1. Para generar una previsualización del catálogo que ha creado, selecciónelo en la **Catálogos** y, a continuación, haga clic en **Vista previa** de la barra de herramientas.

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   Revise las páginas del catálogo en la vista previa. Toque o haga clic **Cerrar** para cerrar la vista previa.
