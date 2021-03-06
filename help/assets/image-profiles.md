---
title: Perfiles de imagen de Dynamic Media
description: Cree perfiles de imagen que contengan ajustes para máscara de enfoque, recorte inteligente o muestra inteligente, o ambos, y aplique el perfil a una carpeta de recursos de imagen.
uuid: 9049fab9-d2be-4118-8684-ce58f3c8c16a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 4f9301db-edf8-480b-886c-b5e8fca5bf5c
feature: Image Profiles
role: User, Admin
exl-id: 67240ad0-1a7c-4e58-a518-1e36d771f1a1
source-git-commit: d83a647d8ac5466ba09230c584d5d501aab55274
workflow-type: tm+mt
source-wordcount: '2831'
ht-degree: 10%

---

# Perfiles de imagen de Dynamic Media {#image-profiles}

Al cargar imágenes, puede recortar automáticamente la imagen al cargarla aplicando un perfil de imagen a la carpeta.

>[!NOTE]
>
>El recorte inteligente solo está disponible en el modo Dynamic Media - Scene7.

>[!IMPORTANT]
>
>Los perfiles de imagen no son aplicables a archivos PDF, GIF animado o INDD (Adobe InDesign).

## Opciones de recorte {#crop-options}

Al implementar Recorte inteligente en imágenes, Adobe recomienda las siguientes prácticas recomendadas y aplica el siguiente límite:

| Tipo de límite | Práctica recomendada | Límite impuesto | Cambio al límite el 31 de diciembre de 2022 |
| --- | --- | --- | --- |
| Número de recortes inteligentes por imagen | 5 | 100 | 20 |

Consulte también [Limitaciones de Dynamic Media](/help/assets/limitations.md).

<!-- CQDOC-16069 for paragraph directly below -->

Las coordenadas de recorte inteligentes dependen de la relación de aspecto. Para los distintos ajustes de recorte inteligente de un perfil de imagen, si la proporción de aspecto es la misma para las dimensiones agregadas en el perfil de imagen, se envía la misma proporción de aspecto a Dynamic Media. Adobe recomienda utilizar el mismo área de recorte. De este modo, se garantiza que no haya ningún impacto en las diferentes dimensiones utilizadas en el perfil de la imagen.

Cada generación de recorte inteligente que cree requiere un procesamiento adicional. Por ejemplo, si se agregan más de cinco relaciones de aspecto de recorte inteligente, la tasa de consumo de los recursos puede ser lenta. También causa un aumento de la carga en los sistemas. Como puede aplicar Recorte inteligente en el nivel de carpeta, Adobe recomienda utilizarlo en las carpetas *only* donde sea necesario.

Tiene dos opciones de recorte de imagen entre las que elegir. También tiene la opción de automatizar la creación de muestras de color e imagen.

| Opción | Cuándo se usa | Descripción |
| --- | --- | --- |
| Recorte de píxeles | Recorte masivo de imágenes basado únicamente en dimensiones. | Para utilizar esta opción, seleccione **[!UICONTROL Recorte de píxeles]** en la lista desplegable Opciones de recorte .<br><br>Para recortar desde los lados de una imagen, introduzca el número de píxeles que se recortarán desde cualquier lado o lado de la imagen. La cantidad de imagen recortada depende de la configuración de ppi (píxeles por pulgada) en el archivo de imagen.<br><br>Un recorte de píxeles del perfil de imagen se representa de la siguiente manera:<br>・ Los valores son Superior, Inferior, Izquierda y Derecha.<br>・ Se considera la parte superior izquierda `0,0` y el recorte de píxeles se calcula a partir de ahí.<br>・ Punto inicial del recorte: La izquierda es X y la superior es Y<br>・ Cálculo horizontal: dimensión de píxeles horizontal de la imagen original menos Izquierda y luego menos Derecha.<br>・ Cálculo vertical: altura vertical de píxeles menos Superior y, a continuación, menos Inferior.<br><br>Por ejemplo, supongamos que tiene una imagen de 4000 x 3000 píxeles. Se utilizan valores: Superior=250, Inferior=500, Izquierda=300, Derecha=700.<br><br>Desde la parte superior izquierda (300.250), recorte utilizando el espacio de relleno (4000-300-700, 3000-250-500 o 3000.2250). |
| Recorte inteligente | Imágenes de recorte masivo basadas en su punto focal visual. | Smart Crop utiliza el poder de la inteligencia artificial en Adobe Sensei para automatizar rápidamente el recorte de imágenes en masa. El recorte inteligente detecta y recorta automáticamente al punto focal de cualquier imagen para capturar el punto de interés deseado, independientemente del tamaño de la pantalla.</p> <p>Para utilizar el Recorte inteligente, seleccione **[!UICONTROL Recorte inteligente]** en la lista desplegable Opciones de recorte y, a continuación, a la derecha de Recorte de imagen adaptable, habilite (active) la función.</p> <p>Los tamaños predeterminados de los puntos de interrupción Grande, Medio y Pequeño generalmente abarcan toda la gama de tamaños que la mayoría de las imágenes se utilizan en dispositivos móviles y tabletas, equipos de escritorio y titulares. Si lo desea, puede editar los nombres predeterminados de Grande, Medio y Pequeño.</p> <p>Para agregar más puntos de interrupción, seleccione **[!UICONTROL Agregar recorte]** para eliminar un recorte, seleccione el icono de la papelera. |
| Muestra de color e imagen | Bulk genera una muestra de imagen para cada imagen. | **Nota**: La muestra inteligente no es compatible con Dynamic Media Classic.<br><br>Localice y genere automáticamente muestras de alta calidad a partir de imágenes de productos que muestren color o textura.<br><br>Para utilizar la muestra de color e imagen, seleccione **[!UICONTROL Recorte inteligente]** en la lista desplegable Opciones de recorte y, a continuación, a la derecha de Color y Muestra de imagen, habilite (active) la función. Introduzca un valor de píxel en los cuadros de texto Ancho y Alto.<br><br>Aunque todos los cultivos de imagen están disponibles en el carril Representaciones , las muestras solo se utilizan mediante la función Copiar URL . Utilice su propio componente de visualización para representar la muestra en el sitio. (La excepción a esta regla son los banners de carrusel. Dynamic Media proporciona el componente de visualización para la muestra utilizada en los banners de carrusel).<br><br>**Uso de muestras de imagen**<br> La dirección URL de las muestras de imagen es sencilla. Es:<br><br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>donde `:Swatch` se anexa a la solicitud de recurso.<br><br>**Uso de muestras de color**<br> Para utilizar muestras de color, debe realizar una `req=userdata` con lo siguiente:<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>Por ejemplo, el siguiente es un recurso de muestra en Dynamic Media Classic:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>y aquí está el correspondiente del recurso de muestra `req=userdata` URL:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br><br>La variable `req=userdata` la respuesta es la siguiente:<br>`SmartCropDef=Swatch SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br><br>También puede solicitar un `req=userdata` en formato XML o JSON, como en los siguientes ejemplos de URL respectivos:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**Nota:** Cree su propio componente WCM para solicitar una muestra de color y analizar el `SmartSwatchColor` , representado por un valor hexadecimal RGB de 24 bits.<br><br>Consulte también [`userdata` en la Guía de referencia de visores](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata.html). |

## Máscara de enfoque {#unsharp-mask}

La **[!UICONTROL máscara de enfoque]** se utiliza para ajustar un efecto de filtro de enfoque en la imagen final con disminución de resolución. Puede controlar la intensidad del efecto, el radio del efecto (medido en píxeles) y un umbral de contraste que se ignora. Este efecto utiliza las mismas opciones que el de Adobe Photoshop *Máscara de enfoque* filtro.

>[!NOTE]
>
>La máscara de enfoque solo se aplica a las representaciones a escala reducida dentro del PTIFF (tiff piramidal) que se reducen a más del 50%. Esto significa que las representaciones de mayor tamaño dentro de la matriz no se ven afectadas por la máscara de enfoque, mientras que las representaciones de menor tamaño, como las miniaturas, se modifican (y muestran la máscara de enfoque).

En **[!UICONTROL Máscara de enfoque]**, tiene las siguientes opciones de filtrado:

| Opción | Descripción |
| --- | --- |
| Cantidad | Controla la cantidad de contraste aplicada a los píxeles de borde. El valor predeterminado es 1,75. Para imágenes de alta resolución, puede aumentarlo hasta 5. Piense en Amount como una medida de la intensidad del filtro. El rango es 0-5. |
| Radio | Determina el número de píxeles adyacentes a los píxeles de borde que afectarán al enfoque. En las imágenes de alta resolución, especifique un valor entre 1 y 2. Un valor bajo solo aplica enfoque a los píxeles de borde; un valor alto enfoca una banda más ancha de píxeles. El valor adecuado depende del tamaño de la imagen. El valor predeterminado es 0,2. El rango es 0-250. |
| Umbral | Determina el intervalo de contraste que se debe ignorar cuando se aplica el filtro de máscara de enfoque. En otras palabras, esta opción determina la diferencia entre los píxeles enfocados y el área circundante antes de que se consideren píxeles de borde y se agranden. Para evitar la introducción del ruido, experimente con valores entre 0 y 255. |

El enfoque se describe en [Enfoque de imágenes](/help/assets/assets/sharpening_images.pdf.

## Creación de perfiles de imagen de Dynamic Media {#creating-image-profiles}

Para definir parámetros de procesamiento avanzados para otros tipos de recursos, consulte [Configuración del procesamiento de recursos](config-dms7.md#configuring-asset-processing).

Consulte [Perfiles para el procesamiento de metadatos, imágenes y vídeos](processing-profiles.md).

Consulte también [Prácticas recomendadas para organizar los recursos digitales con el fin de utilizar perfiles de procesamiento](/help/assets/organize-assets.md).

**Para crear perfiles de imagen de Dynamic Media:**

1. Seleccione el logotipo de Adobe Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Perfiles de imagen]**.
1. Select **[!UICONTROL Crear]** para agregar un perfil de imagen.
1. Introduzca un nombre de perfil y valores para máscara de enfoque, recorte o muestra, o ambos.

   Utilice un nombre de perfil específico para el propósito deseado. Por ejemplo, si desea crear un perfil que genere muestras únicamente, es decir, el Recorte inteligente está desactivado y la Muestra de color e imagen está activada, utilice el nombre de perfil &quot;Muestras inteligentes&quot;.

   Consulte también [Opciones de recorte y muestra inteligente](#crop-options) y [Máscara de enfoque](#unsharp-mask).

   ![recortarla](assets/crop.png)

1. Seleccione **[!UICONTROL Guardar]**. El perfil recién creado aparece en la lista de perfiles disponibles.

## Editar o eliminar perfiles de imagen de Dynamic Media {#editing-or-deleting-image-profiles}

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Perfiles de imagen]**.
1. Seleccione el perfil de imagen que desee editar o eliminar. Para editarlo, seleccione **[!UICONTROL Editar perfil de imagen]**. Para quitarlo, seleccione **[!UICONTROL Eliminar perfil de imagen]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. Si está editando, guarde los cambios. Si elimina, confirme que desea eliminar el perfil.

## Aplicar un perfil de imagen de Dynamic Media a las carpetas {#applying-an-image-profile-to-folders}

Al asignar un perfil de imagen a una carpeta, las subcarpetas heredan automáticamente el perfil de su carpeta principal. Este flujo de trabajo significa que solo puede asignar un perfil de imagen a una carpeta. Como tal, considere detenidamente la estructura de carpetas en la que carga, almacena, utiliza y archiva recursos.

Si ha asignado un perfil de imagen diferente a una carpeta, el nuevo perfil anula el perfil anterior. Los recursos de carpeta existentes no cambian. El nuevo perfil se aplica a los recursos que se agregan a la carpeta más adelante.

Las carpetas que tienen un perfil asignado se indican en la interfaz de usuario utilizando el nombre de perfil que aparece en la tarjeta.

<!-- When you add smart crop to an existing image profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

Puede aplicar perfiles de imagen a carpetas específicas o globalmente a todos los recursos.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de imagen existente que haya cambiado posteriormente. Consulte [Volver a procesar los recursos en una carpeta después de editar su perfil de procesamiento](processing-profiles.md#reprocessing-assets).

### Aplicación de perfiles de imagen de Dynamic Media a carpetas específicas {#applying-image-profiles-to-specific-folders}

Puede aplicar un perfil de imagen a una carpeta desde el menú **[!UICONTROL Herramientas]** o si está en la carpeta, desde **[!UICONTROL Propiedades]**. En esta sección se describe cómo aplicar perfiles de imagen a las carpetas de ambos modos.

Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de vídeo existente que haya cambiado posteriormente. Consulte [Volver a procesar los recursos en una carpeta después de editar su perfil de procesamiento](processing-profiles.md#reprocessing-assets).

#### Aplicación de perfiles de imagen de Dynamic Media a carpetas desde la interfaz de usuario Perfiles {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Perfiles de imagen]**.
1. Seleccione el perfil de imagen que desea aplicar a una o varias carpetas.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Select **[!UICONTROL Aplicar perfil de procesamiento a las carpetas]** y seleccione la carpeta o carpetas múltiples que desee utilizar para recibir los recursos cargados recientemente y seleccione **[!UICONTROL Aplicar]**. Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

#### Aplicación de perfiles de imagen de Dynamic Media a carpetas desde Propiedades {#applying-image-profiles-to-folders-from-properties}

1. Seleccione el logotipo del Experience League y vaya a **[!UICONTROL Recursos]**. A continuación, vaya a la carpeta principal de la carpeta a la que desea aplicar un perfil de imagen.
1. En la carpeta, seleccione la marca de verificación para seleccionarla y, a continuación, seleccione **[!UICONTROL Propiedades]**.
1. Seleccione el **[!UICONTROL Perfiles de imagen]** pestaña . En el **[!UICONTROL Nombre del perfil]** lista desplegable, seleccione el perfil y, a continuación, seleccione **[!UICONTROL Guardar y cerrar]**. Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Aplicar un perfil de imagen de Dynamic Media globalmente {#applying-an-image-profile-globally}

Además de aplicar un perfil a una carpeta, también puede aplicarlo de forma global para que cualquier contenido cargado en recursos de Experience Manager en cualquier carpeta tenga aplicado el perfil seleccionado.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de vídeo existente que haya cambiado posteriormente. Consulte el artículo [Reprocesamiento de recursos en una carpeta después de editar su perfil de procesamiento](processing-profiles.md#reprocessing-assets).

**Para aplicar un perfil de imagen de Dynamic Media globalmente:**

1. Realice una de las acciones siguientes:

   * Vaya a `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` y aplique el perfil adecuado y seleccione **[!UICONTROL Guardar]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * Vaya al CRXDE Lite al nodo siguiente: `/content/dam/jcr:content`.

      Añadir la propiedad `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` y seleccione **[!UICONTROL Guardar todo]**.

      ![configure_image_profiles](assets/configure_image_profiles.png)

## Editar el recorte inteligente o la muestra inteligente de una sola imagen {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!NOTE]
>
>El recorte inteligente solo está disponible en el modo Dynamic Media - Scene7.

Puede realinear manualmente o cambiar el tamaño de la ventana de recorte inteligente de una imagen para refinar aún más su punto focal.

Después de editar un recorte inteligente y guardarlo, el cambio se propaga en todas partes donde utilice el recorte para imágenes específicas.

Si es necesario, puede volver a ejecutar el recorte inteligente para volver a generar los cultivos adicionales.

Consulte también [Editar el recorte inteligente o la muestra inteligente de varias imágenes](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**Para editar el recorte inteligente o la muestra inteligente de una sola imagen:**

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Recursos]** y, a continuación, a la carpeta a la que se le haya aplicado un recorte inteligente o un perfil de imagen de muestra inteligente.

1. Seleccione la carpeta para poder abrir su contenido.
1. Seleccione la imagen cuyo recorte inteligente o muestra inteligente desee ajustar.
1. En la barra de herramientas, seleccione **[!UICONTROL Recorte inteligente]**.

1. Realice una de las acciones siguientes:

   * Cerca de la esquina superior derecha de la página, arrastre la barra deslizante a la izquierda o a la derecha para aumentar o reducir la visualización de la imagen, respectivamente.
   * En la imagen, arrastre un controlador de esquina para ajustar el tamaño del área visible del recorte o muestra.
   * En la imagen, arrastre el cuadro/muestra a una nueva ubicación. Solo se pueden editar muestras de imágenes; las muestras de color son estáticas.
   * Sobre la imagen, seleccione  **[!UICONTROL Revertir]** para deshacer todas las ediciones y restaurar el recorte o muestra original.

1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]** y, a continuación, seleccione **[!UICONTROL Cerrar]** para volver a la carpeta de recursos.

## Editar el recorte inteligente o la muestra inteligente de varias imágenes {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

Después de aplicar un perfil de imagen (que contiene Recorte inteligente) a una carpeta, todas las imágenes de esa carpeta tienen un recorte aplicado a ellas. Si lo desea, puede *manualmente* vuelva a alinear o cambie el tamaño de la ventana de recorte inteligente en varias imágenes para restringir aún más su punto focal.

Después de editar un recorte inteligente y guardarlo, el cambio se propaga en todas partes donde utilice el recorte para imágenes específicas.

Si es necesario, puede volver a ejecutar el recorte inteligente para volver a generar los cultivos adicionales.

**Para editar el recorte inteligente o la muestra inteligente de varias imágenes:**

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Recursos]** y, a continuación, a una carpeta que tenga aplicado un recorte inteligente o un perfil de imagen de muestra inteligente.
1. En la carpeta , seleccione la opción **[!UICONTROL Más acciones]** (...) y, a continuación, seleccione **[!UICONTROL Recorte inteligente]**.

1. En el **[!UICONTROL Editar recortes inteligentes]** , realice una de las acciones siguientes:

   * Ajuste el tamaño de visualización de las imágenes en la página.

      A la derecha de la lista desplegable de nombre del punto de interrupción, arrastre la barra deslizante hacia la izquierda o la derecha para cambiar el tamaño de la visualización de la imagen visible.

      ![edit_smart_farms-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * Filtre la lista de imágenes visibles en función de los nombres de puntos de interrupción. En el ejemplo siguiente, las imágenes se filtran en el nombre del punto de interrupción &quot;Medio&quot;.

      Cerca de la esquina superior derecha de la página, en la lista desplegable, seleccione un nombre de punto de interrupción para filtrar las imágenes que ve. (Consulte la imagen anterior).

      ![edit_smart_farms-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * Cambie el tamaño del cuadro de recorte inteligente. Realice una de las siguientes acciones:

      * Si la imagen tiene un recorte inteligente o solo una muestra inteligente, arrastre en la imagen el controlador de esquina del cuadro de recorte para ajustar el tamaño del área visible del recorte.
      * Si la imagen tiene un recorte inteligente y una muestra inteligente, arrastre el controlador de esquina del cuadro de recorte para ajustar el tamaño del área visible del recorte. O bien, seleccione la muestra inteligente debajo de la imagen (las muestras de color son estáticas) y, a continuación, arrastre el controlador de esquina del cuadro de recorte para ajustar el tamaño del área visible de la muestra.

      ![Cambiar el tamaño del recorte inteligente de una imagen](assets/edit_smart_crops-resize.png)

   * Mueva el cuadro de recorte inteligente. Realice una de las siguientes acciones:

      * Si la imagen tiene un recorte inteligente o solo una muestra inteligente, arrastre el cuadro de recorte a una nueva ubicación.
      * Si la imagen tiene un recorte inteligente y una muestra inteligente, arrastre el cuadro de recorte inteligente a una nueva ubicación. O bien, seleccione la muestra inteligente debajo de la imagen (las muestras de color son estáticas) y, a continuación, arrastre el cuadro de recorte de muestras inteligentes a una nueva ubicación.

      ![edit_smart_farms-move](assets/edit_smart_crops-move.png)

   * Deshacer todas las ediciones y restaurar el recorte inteligente o la muestra inteligente original (se aplica solo a la sesión de edición actual).

      Select **[!UICONTROL Revertir]** encima de la imagen.

      ![edit_smart_farms-revert](assets/edit_smart_crops-revert.png)



1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]** y, a continuación, seleccione **[!UICONTROL Cerrar]** para volver a la carpeta de recursos.

## Eliminación de un perfil de imagen de Dynamic Media de las carpetas {#removing-an-image-profile-from-folders}

Al quitar un perfil de imagen de una carpeta, las subcarpetas heredan automáticamente la eliminación del perfil de su carpeta principal. Sin embargo, cualquier procesamiento de archivos que se haya producido dentro de las carpetas permanece intacto.

Puede quitar un perfil de imagen de una carpeta desde el menú **[!UICONTROL Herramientas]** o, si está en la carpeta, desde **[!UICONTROL Propiedades]**. En esta sección se describe cómo quitar perfiles de imagen de las carpetas de ambos modos.

### Eliminación de perfiles de imagen de Dynamic Media de las carpetas mediante la interfaz de usuario Perfiles {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Perfiles de imagen]**.
1. Seleccione el perfil de imagen que desea eliminar de una carpeta o de varias carpetas.
1. Select **[!UICONTROL Eliminación del perfil de procesamiento de las carpetas]** y seleccione la carpeta o carpetas múltiples que desee utilizar para quitar el perfil y seleccione **[!UICONTROL Eliminar]**.

   Puede confirmar que el perfil de imagen ya no se aplica a una carpeta porque el nombre ya no aparece debajo del nombre de la carpeta.

### Eliminación de perfiles de imagen de Dynamic Media de las carpetas mediante Propiedades {#removing-image-profiles-from-folders-via-properties}

1. Seleccione el logotipo del Experience Manager y navegue **[!UICONTROL Recursos]** y, a continuación, a la carpeta desde la que desea eliminar un perfil de imagen.
1. En la carpeta, seleccione la marca de verificación para seleccionarla y, a continuación, seleccione **[!UICONTROL Propiedades]**.
1. Seleccione el **[!UICONTROL Perfiles de imagen]** pestaña .
1. En el **[!UICONTROL Nombre del perfil]** lista desplegable, seleccione **[!UICONTROL Ninguna]** y, a continuación, seleccione **[!UICONTROL Guardar y cerrar]**.

   Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.
