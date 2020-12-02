---
title: '[!DNL Adobe Camera Raw] asistencia técnica.'
description: Obtenga información sobre cómo habilitar la compatibilidad con [!DNL Adobe Camera Raw] en [!DNL Adobe Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: bccc937c1e1a349ab292a748c3c7b9d0c68b6199
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 1%

---


# Procesar imágenes con {#camera-raw-support} Camera Raw

Puede habilitar la compatibilidad con [!DNL Adobe Camera Raw] para procesar formatos de archivo sin procesar, como CR2, NEF y RAF, y procesar las imágenes en formato JPEG. La funcionalidad se admite en [!DNL Adobe Experience Manager Assets] usando el [paquete Camera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) disponible en Distribución de software.

>[!NOTE]
>
>La funcionalidad solo admite representaciones JPEG. Se admite en Windows de 64 bits, Mac OS y RHEL 7.x.

Para habilitar la compatibilidad con [!DNL Camera Raw] en [!DNL Experience Manager Assets], siga estos pasos:

1. Descargue el [paquete Camera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) de Distribución de software.
1. Acceso `https://[aem_server]:[port]/workflow`. Abra el flujo de trabajo **[!UICONTROL Recurso de actualización de DAM]**.
1. Abra el paso **[!UICONTROL Miniaturas de proceso]**.
1. Proporcione la siguiente configuración en la ficha **[!UICONTROL Miniaturas]**:

   * **[!UICONTROL Miniaturas]**:  `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL Tipos MIME omitidos]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. En la ficha **[!UICONTROL Imagen habilitada para Web]**, en el campo **[!UICONTROL Omitir Lista]**, especifique `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. Desde el panel lateral, agregue el paso **[!UICONTROL Controlador Camera Raw/DNG]** debajo del paso **[!UICONTROL Creación de miniaturas]**.
1. En el paso **[!UICONTROL Controlador Camera Raw/DNG]**, agregue la siguiente configuración en la ficha **[!UICONTROL Argumentos]**:

   * **[!UICONTROL Tipos]** Mime:  `image/dng` y  `image/x-raw-(.*)`
   * **[!UICONTROL Comando]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. Haga clic en **[!UICONTROL Guardar]**.

>[!NOTE]
>
>Asegúrese de que la configuración anterior es la misma que la configuración del **[!UICONTROL recurso de actualización DAM de muestra con la configuración del paso de control Camera Raw y DNG]**.

Ahora puede importar archivos sin procesar de cámara en Assets. Después de instalar el paquete Camera Raw y configurar el flujo de trabajo necesario, aparece la opción **[!UICONTROL Ajuste de imagen]** en la lista de paneles laterales.

![chlimage_1-131](assets/chlimage_1-337.png)

*Figura: Opciones del panel lateral.*

![chlimage_1-132](assets/chlimage_1-338.png)

*Figura: Utilice esta opción para realizar ediciones ligeras en las imágenes.*

Después de guardar las ediciones en una imagen [!DNL Camera Raw], se genera una nueva representación `AdjustedPreview.jpg` para la imagen. Para otros tipos de imagen excepto [!DNL Camera Raw], los cambios se reflejan en todas las representaciones.

## Prácticas recomendadas, problemas conocidos y limitaciones {#best-practices}

La funcionalidad tiene las siguientes limitaciones:

* La funcionalidad solo admite representaciones JPEG. Se admite en Windows de 64 bits, Mac OS y RHEL 7.x.
* La reescritura de metadatos no es compatible con los formatos RAW y DNG.
* La biblioteca [!DNL Camera Raw] tiene limitaciones en cuanto al total de píxeles que puede procesar a la vez. Actualmente, puede procesar un máximo de 65000 píxeles en el lado largo de un archivo o 512 MP, sea cual sea el criterio que se encuentre primero.
