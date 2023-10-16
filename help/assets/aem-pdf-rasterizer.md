---
title: Usar PDF Rasterizer para generar representaciones
description: Genere miniaturas y representaciones de alta calidad con la biblioteca Adobe PDF Rasterizer.
contentOwner: AG
role: Developer, Admin
feature: Developer Tools,Renditions
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
source-git-commit: e6e0ad29bc5b3a644f74427d8d60233c9e26aa03
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 1%

---

# Usar PDF Rasterizer {#using-pdf-rasterizer}

Cuando se cargan archivos AI o PDF grandes y de gran contenido a [!DNL Adobe Experience Manager Assets], es posible que la biblioteca predeterminada no genere un resultado preciso. La biblioteca Rasterizer de PDF de Adobe puede generar una salida más fiable y precisa en comparación con la salida de una biblioteca predeterminada. El Adobe recomienda utilizar la biblioteca Rasterizer de PDF para los siguientes casos:

El Adobe recomienda utilizar la biblioteca Rasterizer de PDF para lo siguiente:

* Archivos AI o archivos de PDF pesados y con gran cantidad de contenido.
* Archivos AI y archivos del PDF con miniaturas que no se generan de forma predeterminada.
* Archivos AI con colores del Sistema de coincidencia de Pantone (PMS).

Las miniaturas y vistas previas generadas con PDF Rasterizer son de mejor calidad en comparación con la salida predeterminada y, por lo tanto, proporcionan una experiencia de visualización uniforme en todos los dispositivos. La biblioteca Rasterizer de Adobe PDF no admite ninguna conversión de espacio de color. Siempre se envía al RGB independientemente del espacio de color del archivo de origen.

1. Instale el paquete PDF Rasterizer en su [!DNL Adobe Experience Manager] implementación desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.6.zip).

   >[!NOTE]
   >
   >La biblioteca Rasterizer de PDF solo está disponible para Windows y Linux®.

1. Acceda a la [!DNL Assets] consola de flujo de trabajo en `https://[aem_server]:[port]/workflow`. Abrir [!UICONTROL Recurso de actualización DAM] flujo de trabajo.

1. Para evitar la generación de miniaturas y representaciones web para archivos de PDF y archivos AI mediante los métodos predeterminados, siga estos pasos:

   * Abra el **[!UICONTROL Procesar miniaturas]** paso y agregue `application/pdf` o `application/postscript` en el **[!UICONTROL Tipos MIME omitidos]** en el campo **[!UICONTROL Miniaturas]** según sea necesario.

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * En el **[!UICONTROL Imagen Web]** pestaña, añadir `application/pdf` o `application/postscript` bajo **[!UICONTROL Lista para omitir]** según sus necesidades.

   ![Configuración para omitir el procesamiento de miniaturas para un formato de imagen](assets/web_enabled_imageskiplist.png)

1. Abra el **[!UICONTROL Rasterizar PDF/AI a una representación de previsualización de imagen]** y elimine el tipo MIME para el que desea omitir la generación predeterminada de representaciones de imágenes de vista previa. Por ejemplo, quite el tipo MIME `application/pdf`, `application/postscript`, o `application/illustrator` desde el **[!UICONTROL Tipos MIME]** lista.

   ![process_arguments](assets/process_arguments.png)

1. Arrastre el **[!UICONTROL Controlador de rasterizador de PDF]** del panel lateral a debajo de la etiqueta **[!UICONTROL Procesar miniaturas]** paso.
1. Configure los siguientes argumentos para **[!UICONTROL Controlador de rasterizador de PDF]** paso:

   * Tipos MIME: `application/pdf` o `application/postscript`
   * Comandos: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Añadir tamaños de miniatura: 319:319, 140:100, 48:48. Añada la configuración de miniaturas personalizada, si es necesario.

   Los argumentos de la línea de comandos para `PDFRasterizer` puede incluir lo siguiente:

   * `-d`: marca para permitir una representación suave del texto, las ilustraciones vectoriales y las imágenes. Crea imágenes de mejor calidad. Sin embargo, si se incluye este parámetro, el comando se ejecuta lentamente y aumenta el tamaño de las imágenes.

   * `-s`: dimensión de imagen máxima (altura o anchura). Se convierte a ppp en cada página. Si las páginas tienen un tamaño diferente, cada página puede escalarse potencialmente en una cantidad diferente. El valor predeterminado es el tamaño de página real.

   * `-t`: Tipo de imagen de salida. Los tipos válidos son JPEG, PNG, GIF y BMP. El valor predeterminado es JPEG.

   * `-i`: ruta para el PDF de entrada. Es un parámetro obligatorio.

   * `-h`: Ayuda

1. Para eliminar representaciones intermedias, seleccione **[!UICONTROL Eliminar representación generada]**.
1. Para permitir que PDF Rasterizer genere representaciones web, seleccione **[!UICONTROL Generar representación web]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Especifique la configuración en la **[!UICONTROL Imagen Web]** pestaña.

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. Guarde el flujo de trabajo.
1. Para permitir que PDF Rasterizer procese páginas de PDF con bibliotecas de PDF, abra el **[!UICONTROL Subactivo de proceso DAM]** modelo desde el [!UICONTROL Flujo de trabajo] consola.
1. En el panel lateral, arrastre el paso Controlador de rasterizador de PDF a la parte inferior de la **[!UICONTROL Crear representación de imagen habilitada para web]** paso.
1. Configure los siguientes argumentos para **[!UICONTROL Controlador de rasterizador de PDF]** paso:

   * Tipos MIME: `application/pdf` o `application/postscript`
   * Comandos: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Añadir tamaños de miniatura: `319:319`, `140:100`, `48:48`. Añada la configuración de miniaturas personalizada según sea necesario.

   Los argumentos de la línea de comandos para `PDFRasterizer` puede incluir lo siguiente:

   * `-d`: marca para permitir una representación suave del texto, las ilustraciones vectoriales y las imágenes. Crea imágenes de mejor calidad. Sin embargo, si se incluye este parámetro, el comando se ejecuta lentamente y aumenta el tamaño de las imágenes.

   * `-s`: dimensión de imagen máxima (altura o anchura). Se convierte a ppp en cada página. Si las páginas tienen un tamaño diferente, cada página puede escalarse potencialmente en una cantidad diferente. El valor predeterminado es el tamaño de página real.

   * `-t`: Tipo de imagen de salida. Los tipos válidos son JPEG, PNG, GIF y BMP. El valor predeterminado es JPEG.

   * `-i`: ruta para el PDF de entrada. Es un parámetro obligatorio.

   * `-h`: Ayuda

1. Para eliminar representaciones intermedias, seleccione **[!UICONTROL Eliminar representación generada]**.
1. Para permitir que PDF Rasterizer genere representaciones web, seleccione **[!UICONTROL Generar representación web]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Especifique la configuración en la **[!UICONTROL Imagen Web]** pestaña.

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. Guarde el flujo de trabajo.
1. Cargar un archivo de PDF o un archivo AI a [!DNL Experience Manager Assets]. PDF Rasterizer genera las miniaturas y representaciones web del archivo.
