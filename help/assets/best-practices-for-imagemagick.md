---
title: Instale y configure ImageMagick para trabajar con [!DNL Adobe Experience Manager Assets].
description: Obtenga información sobre el software ImageMagick, cómo instalarlo, cómo configurar el paso del proceso de la línea de comandos y cómo utilizarlo para editar, componer y generar miniaturas de imágenes.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5d66bf75a6751e41170e6297d26116ad33c2df44
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 1%

---


# Instalar y configurar ImageMagick para trabajar con [!DNL Experience Manager Assets] {#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick es un complemento de software para crear, editar, componer o convertir imágenes de mapa de bits. Puede leer y escribir imágenes en varios formatos (más de 200), incluidos PNG, JPEG, JPEG-2000, GIF, TIFF, DPX, EXR, WebP, Postscript, PDF y SVG. Utilice ImageMagick para cambiar el tamaño, voltear, reflejar, rotar, distorsionar, distorsionar y transformar imágenes. También puede ajustar los colores de la imagen, aplicar diversos efectos especiales o dibujar texto, líneas, polígonos, elipses y curvas mediante ImageMagick.

Utilice el controlador de [!DNL Adobe Experience Manager] medios de la línea de comandos para procesar las imágenes a través de ImageMagick. Para trabajar con varios formatos de archivo mediante ImageMagick, consulte Prácticas recomendadas sobre los formatos de archivo de [Assets](/help/assets/assets-file-format-best-practices.md). Para obtener información sobre todos los formatos de archivo admitidos, consulte [Formatos](/help/assets/assets-formats.md)admitidos de Assets.

Para procesar archivos de gran tamaño con ImageMagick, considere la posibilidad de que los requisitos de memoria sean superiores a los habituales, los posibles cambios necesarios en las políticas de mensajería instantánea y el impacto general en el rendimiento. Los requisitos de memoria dependen de varios factores, como la resolución, la profundidad de bits, el perfil de color y el formato de archivo. Si desea procesar archivos muy grandes con ImageMagick, realice pruebas de rendimiento del [!DNL Experience Manager] servidor correctamente. Al final se proporcionan algunos recursos útiles.

>[!NOTE]
>
>Si utiliza [!DNL Experience Manager] en [!DNL Adobe Managed Services] (AMS), póngase en contacto con el servicio de atención al cliente de Adobe si tiene previsto procesar muchos archivos PSD o PSB de alta resolución. [!DNL Experience Manager] es posible que no procese archivos PSB de alta resolución que superen los 30000 x 23000 píxeles.

## Instalar ImageMagick {#installing-imagemagick}

Hay disponibles varias versiones de los archivos de instalación de ImageMagic para varios sistemas operativos. Utilice la versión adecuada para su sistema operativo.

1. Descargue los archivos [de instalación](https://www.imagemagick.org/script/download.php) ImageMagick correspondientes para su sistema operativo.
1. Para instalar ImageMagick en el disco que aloja el [!DNL Experience Manager] servidor, inicie el archivo de instalación.

1. Establezca la variable de Entorno de ruta en el directorio de instalación de ImageMagic.
1. Para comprobar si la instalación se ha realizado correctamente, ejecute el `identify -version` comando.

## Configurar el paso del proceso de la línea de comandos {#set-up-the-command-line-process-step}

Puede configurar el paso del proceso de la línea de comandos para un caso de uso concreto. Siga estos pasos para generar una imagen y unas miniaturas volteadas (140 x 100, 48 x 48, 319 x 319 y 1280 x 1280) cada vez que agregue un archivo de imagen JPEG a `/content/dam` en el [!DNL Experience Manager] servidor:

1. En el [!DNL Experience Manager] servidor, vaya a la consola Flujo de trabajo (`https://[aem_server]:[port]/workflow`) y abra el modelo de flujo de trabajo de recursos **[!UICONTROL de actualización de]** DAM.
1. En el modelo de flujo de trabajo de recursos **[!UICONTROL de actualización de]** DAM, abra el paso de miniaturas **[!UICONTROL EPS (con tecnología ImageMagick)]** .
1. En la ficha **** Argumentos, agregue `image/jpeg` a la lista **[!UICONTROL Tipos]** de MIME.

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. En el cuadro **[!UICONTROL Comandos]** , introduzca el siguiente comando:

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. Seleccione los indicadores **[!UICONTROL Eliminar representación]** generada y **[!UICONTROL Generar representación]** web.

   ![select_flag](assets/select_flags.png)

1. En la ficha Imagen **[!UICONTROL habilitada para]** Web, especifique los detalles de la representación con dimensiones de 1280 x 1280 píxeles. Además, especifique `image/jpeg` en el cuadro **[!UICONTROL Mimetype]** .

   ![web_enabled_image](assets/web_enabled_image.png)

1. Haga clic en **[!UICONTROL Aceptar]** para guardar los cambios.

   >[!NOTE]
   >
   >Es posible que el `convert` comando no se ejecute con ciertas versiones de Windows (por ejemplo, Windows SE), ya que está en conflicto con la utilidad nativa `convert` que forma parte de la instalación de Windows. En este caso, mencione la ruta completa de la utilidad ImageMagick. Por ejemplo, especifique,
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. Abra el paso **[!UICONTROL Procesar miniaturas]** y agregue el tipo MIME `image/jpeg` en **[!UICONTROL Omitir tipos]** de MIME.

   ![Ski_mime_types](assets/skip_mime_types.png)

1. En la ficha Imagen **[!UICONTROL habilitada para]** Web, agregue el tipo MIME `image/jpeg` en la Lista **** Omitir. Haga clic en **[!UICONTROL Aceptar]** para guardar los cambios.

   ![web_enabled](assets/web_enabled.png)

1. Guarde el flujo de trabajo.

1. Para verificar el procesamiento correcto, cargue una imagen JPG en [!DNL Assets]. Una vez completado el procesamiento, compruebe si se genera o no una imagen volteada y las representaciones.

## Mitigación de vulnerabilidades de seguridad {#mitigating-security-vulnerabilities}

Existen varias vulnerabilidades de seguridad asociadas con el uso de ImageMagick para procesar imágenes. Por ejemplo, el procesamiento de imágenes enviadas por el usuario implica el riesgo de ejecución remota de código (RCE).

Además, varios complementos de procesamiento de imágenes dependen de la biblioteca de ImageMagick, incluida, entre otras, la imagen de PHP, la imagen y el clip de Ruby y la imagen de nodejs.

Si utiliza ImageMagick o una biblioteca afectada, Adobe recomienda mitigar las vulnerabilidades conocidas realizando al menos una de las siguientes tareas (pero preferiblemente ambas):

1. Compruebe que todos los archivos de imagen comienzan con los [&quot;bytes mágicos&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures) esperados correspondientes a los tipos de archivo de imagen que admite antes de enviarlos a ImageMagick para su procesamiento.
1. Utilice un archivo de política para deshabilitar los codificadores de ImageMagick vulnerables. La política global para ImageMagick se encuentra en `/etc/ImageMagick`.
