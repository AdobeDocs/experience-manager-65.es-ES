---
title: Usar el rasterizador de PDF para generar representaciones
description: Genere miniaturas y representaciones de alta calidad utilizando la biblioteca Adobe PDF Rasterizer.
contentOwner: AG
role: Developer, Admin
feature: Developer Tools,Renditions
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# Usar rasterizador PDF {#using-pdf-rasterizer}

Cuando se cargan archivos AI o PDF grandes y con gran contenido en [!DNL Adobe Experience Manager Assets], es posible que la biblioteca predeterminada no genere una salida precisa. La biblioteca Rasterizer del PDF de Adobe puede generar una salida más fiable y precisa en comparación con la salida de una biblioteca predeterminada. Adobe recomienda utilizar la biblioteca PDF Rasterizer para los siguientes escenarios:

Adobe recomienda utilizar la biblioteca PDF Rasterizer para lo siguiente:

* Archivos AI o archivos PDF pesados y con gran contenido.
* Los archivos AI y los archivos PDF con miniaturas que no se generan de forma predeterminada.
* Archivos AI con colores del sistema de coincidencia de Pantone (PMS).

Las miniaturas y vistas previas generadas mediante el Rasterizador de PDF son de mejor calidad en comparación con la salida predeterminada y, por lo tanto, ofrecen una experiencia de visualización uniforme en todos los dispositivos. La biblioteca Rasterizer de Adobe PDF no admite conversión de espacios de color. Siempre envía al RGB independientemente del espacio de color del archivo de origen.

1. Instale el paquete del PDF Rasterizer en su [!DNL Adobe Experience Manager] implementación desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.4.zip).

   >[!NOTE]
   >
   >La biblioteca PDF Rasterizer está disponible solo para Windows y Linux.

1. Acceda a la [!DNL Assets] consola de flujo de trabajo en `https://[aem_server]:[port]/workflow`. Apertura [!UICONTROL Recurso de actualización DAM] flujo de trabajo.

1. Para evitar la generación de miniaturas y representaciones web para archivos PDF y archivos AI mediante los métodos predeterminados, siga estos pasos:

   * Abra el **[!UICONTROL Miniaturas de proceso]** paso y añadir `application/pdf` o `application/postscript` en el **[!UICONTROL Omitir tipos de mime]** en el campo **[!UICONTROL Miniaturas]** como sea necesario.

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * En el **[!UICONTROL Imagen habilitada para web]** ficha, agregar `application/pdf` o `application/postscript` under **[!UICONTROL Omitir lista]** según sus necesidades.

   ![Configuración para omitir el procesamiento de miniaturas para un formato de imagen](assets/web_enabled_imageskiplist.png)

1. Abra el **[!UICONTROL Rasterizar representación de PDF/vista previa de imagen de IA]** y elimine el tipo MIME para el que desea omitir la generación predeterminada de representaciones de imagen de vista previa. Por ejemplo, elimine el tipo MIME `application/pdf`, `application/postscript`o `application/illustrator` de la variable **[!UICONTROL Tipos MIME]** lista.

   ![process_discussions](assets/process_arguments.png)

1. Arrastre el **[!UICONTROL Controlador Rasterizador del PDF]** pase del panel lateral a la parte inferior de la **[!UICONTROL Miniaturas de proceso]** paso a paso.
1. Configure los siguientes argumentos para la variable **[!UICONTROL Controlador Rasterizador del PDF]** paso:

   * Tipos MIME: `application/pdf` o `application/postscript`
   * Comandos: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Añadir tamaños de miniatura: 319:319, 140:100, 48:48. Agregue la configuración de miniaturas personalizada, si es necesario.

   Los argumentos de la línea de comandos para la variable `PDFRasterizer` puede incluir lo siguiente:

   * `-d`: Indicador que permite procesar texto, ilustraciones vectoriales e imágenes sin problemas. Crea imágenes de mejor calidad. Sin embargo, si se incluye este parámetro, el comando se ejecuta lentamente y aumenta el tamaño de las imágenes.

   * `-s`: Dimensión máxima de la imagen (altura o anchura). Se convierte a DPI para cada página. Si las páginas tienen un tamaño diferente, cada página puede escalarse potencialmente en una cantidad diferente. El valor predeterminado es el tamaño real de la página.

   * `-t`: Tipo de imagen de salida. Los tipos válidos son JPEG, PNG, GIF y BMP. El valor predeterminado es JPEG.

   * `-i`: Ruta para el PDF de entrada. Es un parámetro obligatorio.

   * `-h`: Ayuda


1. Para eliminar representaciones intermedias, seleccione **[!UICONTROL Eliminar representación generada]**.
1. Para permitir que el PDF Rasterizer genere representaciones web, seleccione **[!UICONTROL Generar representación web]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Especifique la configuración en la **[!UICONTROL Imagen habilitada para web]** pestaña .

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. Guarde el flujo de trabajo.
1. Para permitir que el Rasterizador de PDF procese páginas de PDF con bibliotecas de PDF, abra el **[!UICONTROL Subconjunto de procesos DAM]** modelo de [!UICONTROL Flujo de trabajo] consola.
1. Desde el panel lateral, arrastre el paso del controlador del rasterizador del PDF debajo del **[!UICONTROL Creación de una representación de imagen habilitada para web]** paso a paso.
1. Configure los siguientes argumentos para la variable **[!UICONTROL Controlador Rasterizador del PDF]** paso:

   * Tipos MIME: `application/pdf` o `application/postscript`
   * Comandos: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Añada tamaños de miniaturas: `319:319`, `140:100`, `48:48`. Agregue la configuración de miniaturas personalizada según sea necesario.

   Los argumentos de la línea de comandos para la variable `PDFRasterizer` puede incluir lo siguiente:

   * `-d`: Indicador que permite procesar texto, ilustraciones vectoriales e imágenes sin problemas. Crea imágenes de mejor calidad. Sin embargo, si se incluye este parámetro, el comando se ejecuta lentamente y aumenta el tamaño de las imágenes.

   * `-s`: Dimensión máxima de la imagen (altura o anchura). Se convierte a DPI para cada página. Si las páginas tienen un tamaño diferente, cada página puede escalarse potencialmente en una cantidad diferente. El valor predeterminado es el tamaño real de la página.

   * `-t`: Tipo de imagen de salida. Los tipos válidos son JPEG, PNG, GIF y BMP. El valor predeterminado es JPEG.

   * `-i`: Ruta para el PDF de entrada. Es un parámetro obligatorio.

   * `-h`: Ayuda


1. Para eliminar representaciones intermedias, seleccione **[!UICONTROL Eliminar representación generada]**.
1. Para permitir que el PDF Rasterizer genere representaciones web, seleccione **[!UICONTROL Generar representación web]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Especifique la configuración en la **[!UICONTROL Imagen habilitada para web]** pestaña .

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. Guarde el flujo de trabajo.
1. Cargar un archivo de PDF o un archivo de IA a [!DNL Experience Manager Assets]. El PDF Rasterizer genera las miniaturas y las representaciones web del archivo.
