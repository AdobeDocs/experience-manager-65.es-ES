---
title: Usar rasterizador de PDF para generar representaciones
description: En este artículo se describe cómo generar miniaturas y representaciones de alta calidad con la biblioteca Rasterizer de Adobe PDF.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Usar rasterizador de PDF {#using-pdf-rasterizer}

A veces, cuando se cargan archivos PDF o AI de gran tamaño con mucho contenido en Recursos Adobe Experience Manager (AEM), es posible que la biblioteca predeterminada no genere una salida precisa. En estos casos, la biblioteca Rasterizer de PDF de Adobe puede generar resultados más fiables y precisos que los de una biblioteca predeterminada.

Adobe recomienda utilizar la biblioteca Rasterizer de PDF para lo siguiente:

* Archivos AI/PDF intensos y con gran contenido
* Archivos AI/PDF con miniaturas no generados de forma predeterminada
* Archivos AI con colores Pantone Matching System (PMS)

Las miniaturas y las vistas previas generadas con el rasterizador de PDF tienen una mejor calidad en comparación con la salida lista para usar y, por lo tanto, ofrecen una experiencia de visualización uniforme en todos los dispositivos. La biblioteca Rasterizer de Adobe PDF no admite conversión de espacio de color. Siempre se envía a RGB independientemente del espacio de color del archivo de origen.

1. Instale el paquete Rasterizer PDF en su instancia de AEM desde Uso compartido de [paquetes](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/product/assets/aem-assets-pdf-rasterizer-pkg).

   >[!NOTE]
   >
   >La biblioteca Rasterizer PDF solo está disponible para Windows y Linux.

1. Acceda a la consola de flujo de trabajo de Recursos AEM en `https://[server]:[port]/workflow`.

   Abra la página de flujo de trabajo de recursos de actualización de DAM.

1. Para evitar que la generación de miniaturas y representaciones web para archivos PDF y AI utilice los métodos predeterminados, siga estos pasos:

   * Abra el paso **[!UICONTROL Procesar miniaturas]** y agregue `application/pdf` o `application/postscript` en el campo **[!UICONTROL Omitir tipos]** de MIME en la ficha **[!UICONTROL Miniaturas]** , según sea necesario.
   ![Ski_mime_types-2](assets/skip_mime_types-2.png)

   * En la ficha Imagen **[!UICONTROL habilitada para]** Web, agregue `application/pdf` o `application/postscript` debajo de **[!UICONTROL Omitir lista]** según sus necesidades.
   ![Configuración para omitir el procesamiento de miniaturas para un formato de imagen](assets/web_enabled_imageskiplist.png)

1. Abra el paso **[!UICONTROL Rasterizar representación]** de vista previa de imágenes PDF/AI y elimine el tipo MIME para el que desea omitir la generación predeterminada de representaciones de imágenes de vista previa. Por ejemplo, elimine el tipo MIME `application/pdf`, `application/postscript`o `application/illustrator` de la lista Tipos **** MIME.

   ![process_words](assets/process_arguments.png)

1. Arrastre el paso Controlador de rasterizador **** PDF desde el panel lateral hasta debajo del paso Miniaturas **[!UICONTROL de]** proceso.
1. Configure los siguientes argumentos para el paso del controlador de rasterizador **** PDF:

   * Tipos MIME: `application/pdf` o `application/postscript`

   * Comandos: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * Agregar tamaños de miniaturas: 319:319, 140:100, 48:48. Agregue la configuración de miniaturas personalizada, si es necesario.
   Los argumentos de la línea de comandos del `PDFRasterizer` comando pueden incluir lo siguiente:

   * `-d`:: Marca para permitir la representación suave de texto, ilustraciones vectoriales e imágenes. Crea imágenes de mejor calidad. Sin embargo, si se incluye este parámetro, el comando se ejecuta lentamente y aumenta el tamaño de las imágenes.

   * `-p`:: Número de página. El valor predeterminado son todas las páginas. &#39;*&#39; indica todas las páginas.

   * `-s`:: Dimensión máxima de la imagen (altura o anchura). Se convierte a PPP para cada página. Si las páginas tienen un tamaño diferente, cada página podría escalarse en una cantidad diferente. El valor predeterminado es el tamaño real de la página.

   * `-t`:: Tipo de imagen de salida. Los tipos válidos son JPEG, PNG, GIF y BMP. El valor predeterminado es JPEG.

   * `-i`:: Ruta para el PDF de entrada. Es un parámetro obligatorio.

   * `-h`: Ayuda


1. Para eliminar representaciones intermedias, seleccione **[!UICONTROL Eliminar representación]** generada.
1. Para permitir que Rasterizar PDF genere representaciones web, seleccione **[!UICONTROL Generar representación]** web.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Especifique la configuración en la ficha Imagen **[!UICONTROL habilitada para]** Web.

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. Guarde el flujo de trabajo.
1. Para habilitar el rasterizador de PDF para procesar páginas PDF con bibliotecas PDF, abra el modelo **[!UICONTROL DAM Process Subasset]** desde la consola Flujo de trabajo.
1. En el panel lateral, arrastre el paso Controlador de rasterizador de PDF debajo del paso **[!UICONTROL Crear representación]** de imagen habilitada para Web.
1. Configure los siguientes argumentos para el paso del controlador de rasterizador **** PDF:

   * Tipos MIME: `application/pdf` o `application/postscript`

   * Comandos: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * Agregar tamaños de miniaturas: 319:319, 140:100, 48:48. Agregue la configuración de miniaturas personalizada, si es necesario.
   Los argumentos de la línea de comandos para el comando PDFRasterizer pueden incluir lo siguiente:

   * `-d`:: Marca para permitir la representación suave de texto, ilustraciones vectoriales e imágenes. Crea imágenes de mejor calidad. Sin embargo, si se incluye este parámetro, el comando se ejecuta lentamente y aumenta el tamaño de las imágenes.

   * `-p`:: Número de página. El valor predeterminado son todas las páginas. `*` indica todas las páginas.

   * `-s`:: Dimensión máxima de la imagen (altura o anchura). Se convierte a PPP para cada página. Si las páginas tienen un tamaño diferente, cada página podría escalarse en una cantidad diferente. El valor predeterminado es el tamaño real de la página.

   * `-t`:: Tipo de imagen de salida. Los tipos válidos son JPEG, PNG, GIF y BMP. El valor predeterminado es JPEG.

   * `-i`:: Ruta para el PDF de entrada. Es un parámetro obligatorio.

   * `-h`: Ayuda


1. Para eliminar representaciones intermedias, seleccione **[!UICONTROL Eliminar representación]** generada.
1. Para permitir que Rasterizar PDF genere representaciones web, seleccione **[!UICONTROL Generar representación]** web.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Especifique la configuración en la ficha Imagen **[!UICONTROL habilitada para]** Web.

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. Guarde el flujo de trabajo.
1. Cargue un archivo PDF o AI en Recursos AEM. PDF Rasterizer genera las miniaturas y las representaciones web del archivo.
