---
title: Productor de catálogos
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
description: Productor de catálogos
exl-id: 76a46c62-d47d-4970-8a3a-d56015639548
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: ht
source-wordcount: '846'
ht-degree: 100%

---

# Productor de catálogos{#catalog-producer}

Aprenda a utilizar el Productor de catálogos en AEM Assets para generar catálogos de productos con sus recursos digitales.

Con el Productor de catálogos de Adobe Experience Manager (AEM) Assets, puede crear catálogos para los productos de su marca mediante plantillas de InDesign importadas desde una aplicación de InDesign. Para importar plantillas de InDesign, primero integre AEM Assets con servidor de InDesign.

## Integración con el servidor de InDesign {#integrating-with-indesign-server}

Como parte del proceso de integración, configure el flujo de trabajo **Actualizar recurso de DAM**, que es adecuado para la integración con InDesign. Además, configure un trabajador proxy para el servidor de InDesign. Para obtener más información, consulte [Integración de AEM Assets con InDesign Server](/help/assets/indesign.md).

>[!NOTE]
>
>Puede generar plantillas de InDesign a partir de archivos de InDesign antes de importarlas a AEM Assets. Para obtener más información, vea [Uso de archivos y plantillas](https://helpx.adobe.com/es/indesign/using/files-templates.html).
>
>Puede asignar los elementos de las plantillas de InDesign a las etiquetas XML. Las etiquetas asignadas se muestran como propiedades cuando se asignan propiedades de producto con propiedades de plantilla en el Productor de catálogos. Para obtener más información sobre el etiquetado XML en archivos InDesign, consulte [Etiquetado de contenido para XML](https://helpx.adobe.com/es/indesign/using/tagging-content-xml.html).

>[!NOTE]
>
>Solo se utilizan como plantillas los archivos InDesign (.indd). Los archivos con la extensión .indt no son compatibles.

## Creación de un catálogo {#creating-a-catalog}

El Productor de catálogos utiliza datos de administración de la información del producto (PIM) para asignar propiedades del producto con las propiedades XML mostradas en la plantilla. Para crear un catálogo, siga estos pasos:

1. En la interfaz de usuario de Assets, haga clic en el **logotipo de AEM** y vaya a **Assets > Catálogos**.
1. En la página **Catálogos**, haga clic en **Crear** en la barra de herramientas y, a continuación, seleccione **Catálogo** en la lista.
1. En la página **Crear catálogo**, escriba un nombre y una descripción (opcional) para el catálogo y especifique las etiquetas, si las hay. También puede añadir una imagen en miniatura para el catálogo.

   ![create_catalog](assets/create_catalog.png)

1. Haga clic en **Guardar**. Un cuadro de diálogo de confirmación notifica que se ha creado el catálogo. Haga clic en **Listo** para cerrar el cuadro de diálogo.
1. Para abrir el catálogo que ha creado, haga clic en él desde la página **Catálogos**.

   >[!NOTE]
   >
   >Para abrir el catálogo, también puede hacer clic en **Abrir** en el cuadro de diálogo de confirmación mencionado en el paso anterior.

1. Para añadir páginas al catálogo, haga clic en **Crear** en la barra de herramientas y, a continuación, elija la opción **Nueva página**.
1. En el asistente, seleccione una plantilla de InDesign para su página. A continuación, haga clic en **Siguiente**.
1. Especifique un nombre para la página y una descripción opcional. Especifique las etiquetas, si las hay.
1. Haga clic en **Crear** en la barra de herramientas. A continuación, haga clic en **Abrir** en el cuadro de diálogo. Las propiedades del producto se muestran en el panel izquierdo. Las propiedades predefinidas de la plantilla de InDesign aparecen en el panel derecho.
1. En el panel izquierdo, arrastre las propiedades del producto a las propiedades de la plantilla de InDesign y cree una asignación entre ellas.

   Para ver cómo aparece la página en tiempo real, haga clic en la pestaña **Vista previa** del panel derecho.

1. Para crear más páginas, repita los pasos del 6 al 9. Para crear páginas similares para otros productos, seleccione la página y haga clic en el icono **Crear páginas similares** de la barra de herramientas.

   ![create_similar_pages](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >Solo puede crear páginas similares para productos con una estructura similar.

   Haga clic en el icono Añadir, seleccione productos en el selector de productos y, a continuación, haga clic en **Seleccionar** en la barra de herramientas.

   ![select_product](assets/select_product.png)

1. En la barra de herramientas, haga clic en **Crear**. Haga clic en **Listo** para cerrar el cuadro de diálogo. Se incluyen páginas similares en su catálogo.
1. Para añadir cualquier archivo de InDesign existente al catálogo, haga clic en **Crear** en la barra de herramientas y elija la opción **Añadir a la página existente**.
1. Seleccione el archivo de InDesign y haga clic en **Añadir** en la barra de herramientas. Después, haga clic en **Aceptar** para cerrar el cuadro de diálogo.

   Si se cambian los metadatos de los productos a los que hace referencia en las páginas del catálogo, los cambios no se reflejan de forma automática en las páginas del catálogo. Aparece un banner con la etiqueta **Obsoleto** en las imágenes de producto de las páginas del catálogo de referencia, que indica que los metadatos de los productos a los que se hace referencia no están actualizados.

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   Para asegurarse de que las imágenes de producto reflejen los cambios de metadatos más recientes, seleccione la página en la consola Catálogo y haga clic en el icono **Actualizar página** de la barra de herramientas.

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >Para cambiar los metadatos de un producto al que se hace referencia, vaya a la consola Productos (**Logotipo de AEM** > **Commerce** > **Productos**) y seleccione el producto. A continuación, haga clic en el icono **Ver propiedades** de la barra de herramientas y edite los metadatos en la página Propiedades del recurso.

1. Para reorganizar las páginas del catálogo, haga clic en el icono **Crear** de la barra de herramientas y, a continuación, elija **Combinar** en el menú. En el asistente, el carrusel de la parte superior permite reordenar las páginas arrastrándolas. También puede quitar páginas.

1. Haga clic en **Siguiente**. Para añadir un archivo de InDesign existente como portada, haga clic en **Examinar** junto al cuadro **Elegir portada** y especifique la ruta de acceso para la plantilla de portada.
1. Haga clic en **Guardar** y, a continuación, en **Listo** para cerrar el cuadro de diálogo de confirmación.
Al seleccionar la opción **Listo**, se abre un cuadro de diálogo para seleccionar si desea la representación de .pdf.
   ![Exportar a PDF](assets/CatalogPDF.png)
Si se selecciona la opción Acrobat (PDF), se crea una representación del PDF en **/jcr:content/renditions**, además de la representación de InDesign. Puede descargar todas las representaciones seleccionando la casilla “Representaciones” en el cuadro de diálogo de descarga.

1. Para generar una vista previa del catálogo que ha creado, selecciónelo en la consola **Catálogos** y, a continuación, haga clic en el icono **Vista previa** de la barra de herramientas.

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   Revise las páginas del catálogo en la vista previa. Haga clic en **Cerrar** para cerrar la vista previa.
