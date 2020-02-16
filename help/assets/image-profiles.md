---
title: Perfiles de imagen de Dynamic Media
description: Cree perfiles de imagen que contengan ajustes para máscara de enfoque, recorte inteligente, muestra inteligente o ambas, y aplique el perfil a una carpeta de recursos de imagen.
uuid: 9049fab9-d2be-4118-8684-ce58f3c8c16a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 4f9301db-edf8-480b-886c-b5e8fca5bf5c
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Perfiles de imagen de Dynamic Media {#image-profiles}

Al cargar imágenes, puede recortar automáticamente la imagen al cargarla aplicando un perfil de imagen a la carpeta.

>[!NOTE]
>
>El recorte inteligente solo está disponible en el modo Dynamic Media - Scene7.

## Crop options {#crop-options}

Tiene dos opciones de recorte de imágenes entre las que elegir y una opción para automatizar la creación de muestras de color e imagen.

<table>
 <tbody>
  <tr>
   <td><strong>Opción</strong></td>
   <td><strong>Cuándo usar</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Recorte de píxeles</td>
   <td>Recorte masivo de imágenes solo en función de las dimensiones.</td>
   <td><p>Para utilizar esta opción, seleccione Recorte de <strong>píxeles</strong> en la lista desplegable Opciones de recorte.</p> <p>Para recortar de los lados de una imagen, introduzca el número de píxeles que recortar de cualquier lado o de cada lado de la imagen. La cantidad de imagen que se recorta depende de la configuración de ppp (píxeles por pulgada) en el archivo de imagen.</p> <p>El recorte de píxeles de un perfil de imagen se representa de la siguiente manera:<br /> </p>
    <ul>
     <li>Los valores son Superior, Inferior, Izquierda y Derecha.</li>
     <li>La parte superior izquierda se considera 0,0 y el recorte de píxeles se calcula a partir de ahí.</li>
     <li>Punto inicial de recorte: La izquierda es X y la superior es Y</li>
     <li>Cálculo horizontal: dimensión de píxeles horizontal de la imagen original menos Izquierda y, a continuación, menos Derecha.</li>
     <li>Cálculo vertical: altura vertical de píxel menos Superior y, a continuación, menos Inferior.</li>
    </ul> <p>Por ejemplo, supongamos que tiene una imagen de 4000 x 3000 píxeles. Los valores se utilizan: Top=250; Bottom=500; Left=300; Right=700.</p> <p>Desde la parte superior izquierda (300.250), recorte utilizando el espacio de relleno de (4000-300-700, 3000-250-500 o 3000.2250).</p> </td>
  </tr>
  <tr>
   <td>Recorte inteligente</td>
   <td>Recorte masivo de imágenes en función de su punto focal visual.</td>
   <td><p>Smart Crop utiliza el poder de la inteligencia artificial en Adobe Sensei para automatizar rápidamente el recorte masivo de imágenes. El recorte inteligente detecta y recorta automáticamente al punto focal de cualquier imagen para capturar el punto de interés deseado, independientemente del tamaño de la pantalla.</p> <p>Para utilizar Recorte inteligente, seleccione Recorte <strong>inteligente</strong> en la lista desplegable Opciones de recorte y, a continuación, a la derecha de Recorte de imagen interactivo, active (active) la función.</p> <p>Los tamaños predeterminados de los puntos de interrupción Grande, Medio y Pequeño generalmente cubren toda la gama de tamaños que la mayoría de las imágenes se utilizan en dispositivos móviles y tabletas, equipos de escritorio y pancartas. Si lo desea, puede editar los nombres predeterminados de Grande, Medio y Pequeño.</p> <p>Para agregar más puntos de interrupción, haga clic en <strong>Agregar recorte</strong>; para eliminar un recorte, haga clic en el icono de papelera.</p> </td>
  </tr>
  <tr>
   <td>Muestra de color e imagen</td>
   <td>Genera de forma masiva una muestra de imagen para cada imagen.</td>
   <td><p><strong>Nota</strong>: La muestra inteligente no es compatible con Dynamic Media Classic.</p> <p>Localice y genere automáticamente muestras de alta calidad a partir de imágenes de productos que muestren color o textura.</p> <p>Para utilizar la muestra de color e imagen, seleccione Recorte <strong>inteligente</strong> en la lista desplegable Opciones de recorte y, a continuación, a la derecha de la muestra de color e imagen, active (active) la función. Introduzca un valor de píxel en los cuadros de texto Anchura y Altura.</p> <p>Aunque todos los recortes de imagen están disponibles en el carril Representaciones, las muestras solo se utilizan mediante la función Copiar URL. Tenga en cuenta que debe utilizar su propio componente de visualización para representar la muestra en el sitio. (La excepción son las pancartas carrusel. Dynamic Media proporciona el componente de visualización de la muestra utilizada en las pancartas de carrusel).</p> <p><strong>Uso de muestras de imagen</strong></p> <p>La dirección URL de las muestras de imagen es sencilla. Esto es:</p> <p><code>/is/image/company/&lt;asset_name&gt;:Swatch</code></p> <p>donde <code>:Swatch</code> se anexa a la solicitud de recurso.</p> <p><strong>Uso de muestras de color</strong></p> <p>Para utilizar muestras de color, realice una <code>req=userdata</code> solicitud con lo siguiente:</p> <p><code>/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata</code></p> <p>Por ejemplo, a continuación se muestra un recurso de muestra en Dynamic Media Classic (Scene7):</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch</code></p> <p>y aquí está la <code>req=userdata</code> URL correspondiente del recurso de muestra:</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata</code></p> <p>La <code>req=userdata</code> respuesta es la siguiente:</p> <p><code class="code">SmartCropDef=Swatch
       SmartCropHeight=200.0
       SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200
       SmartCropType=Swatch
       SmartCropWidth=200.0
       SmartSwatchColor=0xA56DB2</code></p> <p>También puede solicitar una <code>req=userdata</code> respuesta en formato XML o JSON, como en los siguientes ejemplos de URL:</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml</code></p><p><code>SmartSwatchColor</code></p><p></p></td></tr></tbody></table>

## Máscara de enfoque {#unsharp-mask}

La máscara **[!UICONTROL de]** enfoque se utiliza para ajustar un efecto de filtro de enfoque en la imagen final con disminución de resolución. Puede controlar la intensidad del efecto, el radio del efecto (medido en píxeles) y un umbral de contraste que se omitirá. Este efecto utiliza las mismas opciones que el filtro &quot;Máscara de enfoque&quot; de Adobe Photoshop.

>[!NOTE]
>
>La máscara de enfoque solo se aplica a las representaciones a menor escala dentro del PTIFF (tiff piramidal) con una disminución de la resolución superior al 50 %. Esto significa que las representaciones de mayor tamaño dentro de la etiqueta no se ven afectadas por la máscara de enfoque, mientras que las representaciones de menor tamaño, como las miniaturas, se modifican (y mostrarán la máscara de enfoque).

En Máscara de **[!UICONTROL enfoque]**, tiene las siguientes opciones de filtrado:

<table>
 <tbody>
  <tr>
   <td><strong>Opción</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Cantidad</td>
   <td>Controla la cantidad de contraste aplicado a los píxeles del borde. El valor predeterminado es 1,75. Para imágenes de alta resolución, puede aumentarlas hasta 5.  Considere la cantidad como una medida de la intensidad del filtro. El rango es 0-5.</td>
  </tr>
  <tr>
   <td>Radio</td>
   <td>Determina el número de píxeles adyacentes a los píxeles de borde que afectarán al enfoque. En las imágenes de alta resolución, especifique un valor entre 1 y 2. Un valor bajo solo aplica enfoque a los píxeles de borde; un valor alto enfoca una banda más ancha de píxeles. El valor adecuado depende del tamaño de la imagen. El valor predeterminado es 0,2. El rango es 0-250.</td>
  </tr>
  <tr>
   <td>Umbral</td>
   <td><p>Determina el rango de contraste que se debe ignorar al aplicar el filtro de máscara de enfoque.En otras palabras, esta opción determina la diferencia entre los píxeles enfocados y el área que los rodea antes de que se consideren píxeles de borde y se enfoquen. Para evitar introducir ruido, experimente con valores entre 0 y 255.</p> </td>
  </tr>
 </tbody>
</table>

El enfoque se describe en [Enfoque de imágenes](/help/assets/assets/s7_sharpening_images.pdf).

## Creación de perfiles de imagen de Dynamic Media {#creating-image-profiles}

Para definir parámetros de procesamiento avanzados para otros tipos de recursos, consulte [Configuración del procesamiento](config-dms7.md#configuring-asset-processing)de recursos.

Consulte [Perfiles para procesar metadatos, imágenes y vídeos](processing-profiles.md).

Consulte también [Prácticas recomendadas para organizar los recursos digitales con el fin de utilizar perfiles](/help/assets/organize-assets.md)de procesamiento.

**Para crear perfiles de imagen de Dynamic Media**

1. Toque el logotipo de AEM y vaya a **[!UICONTROL Herramientas > Recursos > Perfiles]** de imagen.
1. Toque **[!UICONTROL Crear]** para agregar un nuevo perfil de imagen.
1. Introduzca un nombre de perfil y valores para máscara de enfoque, recorte o muestra, o ambos.

   Puede que le resulte útil utilizar un nombre de perfil que sea específico para su propósito. Por ejemplo, si desea crear un perfil que genere muestras únicamente (es decir, el recorte inteligente se desactiva y la muestra de color e imagen se activa), puede utilizar el nombre de perfil &quot;Muestras inteligentes&quot;.

   Consulte también Opciones [de recorte](#crop-options) inteligente y de muestra inteligente y Máscara de [enfoque](#unsharp-mask).

   ![recortarla](assets/crop.png)

1. Toque **[!UICONTROL Guardar]**. El perfil recién creado aparece en la lista de perfiles disponibles.

## Edición o eliminación de perfiles de imagen de Dynamic Media {#editing-or-deleting-image-profiles}

1. Toque el logotipo de AEM y vaya a **[!UICONTROL Herramientas > Recursos > Perfiles]** de imagen.
1. Seleccione el perfil de imagen que desee editar o eliminar. Para editarlo, seleccione **[!UICONTROL Editar perfil]** de procesamiento de imágenes. Para eliminarlo, seleccione **[!UICONTROL Eliminar perfil]** de procesamiento de imágenes.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. Si está editando, guarde los cambios. Si elimina, confirme que desea eliminar el perfil.

## Aplicación de un perfil de imagen de Dynamic Media a carpetas {#applying-an-image-profile-to-folders}

Al asignar un perfil de imagen a una carpeta, las subcarpetas heredan automáticamente el perfil de su carpeta principal. Esto significa que solo puede asignar un perfil de imagen a una carpeta. Como tal, considere cuidadosamente la estructura de carpetas en la que carga, almacena, utiliza y archiva los recursos.

Si ha asignado un perfil de imagen diferente a una carpeta, el nuevo perfil anula el perfil anterior. Los recursos de carpeta existentes anteriormente permanecen sin cambios. El nuevo perfil se aplica a los recursos que se agregan a la carpeta más adelante.

Las carpetas que tienen un perfil asignado se indican en la interfaz de usuario por el nombre del perfil que aparece en la tarjeta.

<!-- When you add smart crop to an existing image profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

Puede aplicar perfiles de imagen a carpetas específicas o globalmente a todos los recursos.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de imagen existente que haya cambiado posteriormente. Consulte el artículo [Reprocesamiento de recursos en una carpeta después de editar su perfil de procesamiento](processing-profiles.md#reprocessing-assets).

### Aplicación de perfiles de imagen de Dynamic Media a carpetas específicas {#applying-image-profiles-to-specific-folders}

Puede aplicar un perfil de imagen a una carpeta desde el menú **[!UICONTROL Herramientas]** o si está en la carpeta, desde **[!UICONTROL Propiedades]**. En esta sección se describe cómo aplicar perfiles de imagen a las carpetas de ambos modos.

Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de vídeo existente que haya cambiado posteriormente. Consulte el artículo [Reprocesamiento de recursos en una carpeta después de editar su perfil de procesamiento](processing-profiles.md#reprocessing-assets).

#### Aplicación de perfiles de imagen de Dynamic Media a carpetas desde la interfaz de usuario Perfiles {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Toque el logotipo de AEM y vaya a **[!UICONTROL Herramientas > Recursos > Perfiles]** de imagen.
1. Seleccione el perfil de imagen que desea aplicar a una o varias carpetas.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Toque **[!UICONTROL Aplicar perfil de procesamiento a las carpetas]** y seleccione la carpeta o varias carpetas que desee utilizar para recibir los recursos cargados recientemente y toque o haga clic en **[!UICONTROL Aplicar]**. Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

#### Aplicación de perfiles de imagen de Dynamic Media a carpetas de Propiedades {#applying-image-profiles-to-folders-from-properties}

1. Toque el logotipo de AEM, vaya a **[!UICONTROL Recursos]** y, a continuación, a la carpeta a la que desee aplicar un perfil de imagen.
1. En la carpeta, toque la marca de verificación para seleccionarla y, a continuación, **[!UICONTROL Propiedades]**.
1. Toque la ficha Perfiles **[!UICONTROL de imagen]** . En la lista desplegable Nombre **** del perfil, seleccione el perfil y, a continuación, toque **[!UICONTROL Guardar y cerrar]**. Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Aplicación global de un perfil de imagen de Dynamic Media {#applying-an-image-profile-globally}

Además de aplicar un perfil a una carpeta, también puede aplicarlo de forma global para que cualquier contenido cargado en recursos de AEM en cualquier carpeta tenga aplicado el perfil seleccionado.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de vídeo existente que haya cambiado posteriormente. Consulte el artículo [Reprocesamiento de recursos en una carpeta después de editar su perfil de procesamiento](processing-profiles.md#reprocessing-assets).

**Para aplicar un perfil de imagen de Dynamic Media globalmente**:

1. Realice una de las acciones siguientes:

   * Vaya a `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` y aplique el perfil adecuado y toque **[!UICONTROL Guardar]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * Vaya a CRXDE Lite al nodo siguiente: `/content/dam/jcr:content`.

      Agregue la propiedad `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` y toque **[!UICONTROL Guardar todo]**.

      ![configure_image_files](assets/configure_image_profiles.png)

## Edición del recorte inteligente o muestra inteligente de una sola imagen {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!NOTE]
>
>El recorte inteligente solo está disponible en el modo Dynamic Media - Scene7.

Puede realinear o cambiar el tamaño de la ventana de recorte inteligente de una imagen manualmente para reducir aún más su punto focal.

Después de editar un recorte inteligente y guardarlo, el cambio se propaga dondequiera que utilice el recorte para las imágenes específicas.

Puede volver a ejecutar el recorte inteligente para generar los cultivos adicionales de nuevo, si es necesario.

Consulte también [Edición del recorte inteligente o muestra inteligente de varias imágenes](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**Para editar el recorte inteligente o la muestra inteligente de una sola imagen**:

1. Toque el logotipo de AEM y vaya a **[!UICONTROL Recursos]** y, a continuación, a la carpeta en la que se le haya aplicado un perfil de imagen de muestra inteligente o de recorte inteligente.

1. Toque la carpeta para abrir su contenido.
1. Toque la imagen cuyo recorte inteligente o muestra inteligente desee ajustar.
1. En la barra de herramientas, toque Recorte **[!UICONTROL inteligente]**.

1. Realice una de las acciones siguientes:

   * Cerca de la esquina superior derecha de la página, arrastre la barra deslizante hacia la izquierda o la derecha para aumentar o reducir la visualización de la imagen, respectivamente.
   * En la imagen, arrastre un controlador de esquina para ajustar el tamaño del área visible del recorte o muestra.
   * En la imagen, arrastre el cuadro/muestra a una nueva ubicación. Solo puede editar muestras de imagen; las muestras de color son estáticas.
   * Por encima de la imagen, toque **[!UICONTROL Revertir]** para deshacer todas las ediciones y restaurar el recorte o muestra original.

1. Cerca de la esquina superior derecha de la página, toque **[!UICONTROL Guardar]** y, a continuación, **[!UICONTROL Cerrar]** para volver a la carpeta de recursos.

## Edición del recorte inteligente o muestra inteligente de varias imágenes {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

Después de aplicar un perfil de imagen (que contiene recorte inteligente) a una carpeta, todas las imágenes de la carpeta tienen un recorte aplicado. Si lo desea, puede volver a alinear *manualmente* o cambiar el tamaño de la ventana de recorte inteligente en varias imágenes para reducir aún más su punto focal.

Después de editar un recorte inteligente y guardarlo, el cambio se propaga dondequiera que utilice el recorte para las imágenes específicas.

Puede volver a ejecutar el recorte inteligente para generar los cultivos adicionales de nuevo, si es necesario.

**Para editar el recorte inteligente o la muestra inteligente de varias imágenes**:

1. Toque el logotipo de AEM y vaya a **[!UICONTROL Recursos]** y, a continuación, a una carpeta que tenga un recorte inteligente o un perfil de imagen de muestra inteligente aplicado.
1. En la carpeta, toque el icono **[!UICONTROL Más acciones]** (...) y luego **[!UICONTROL Recorte]** inteligente.

1. En la página **[!UICONTROL Editar cultivos]** inteligentes, realice una de las siguientes acciones:

   * Ajuste el tamaño de visualización de las imágenes en la página.

      A la derecha de la lista desplegable del nombre del punto de interrupción, arrastre la barra deslizante hacia la izquierda o la derecha para cambiar el tamaño de la visualización de la imagen visible.

      ![edit_smart_groups-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * Filtre la lista de imágenes visualizables en función de los nombres de los puntos de interrupción. En el ejemplo siguiente, las imágenes se filtran en el nombre del punto de interrupción &quot;Medio&quot;.

      Cerca de la esquina superior derecha de la página, en la lista desplegable, seleccione un nombre de punto de interrupción para filtrar las imágenes que ve. (Consulte la imagen de arriba).

      ![edit_smart_bars-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * Cambie el tamaño del cuadro de recorte inteligente. Realice una de las siguientes acciones:

      * Si la imagen solo tiene un recorte inteligente o una muestra inteligente, arrastre el controlador de esquina del cuadro de recorte para ajustar el tamaño del área visible del recorte.
      * Si la imagen tiene un recorte inteligente y una muestra inteligente, arrastre el controlador de esquina del cuadro de recorte para ajustar el tamaño del área visible del recorte. O bien, toque o haga clic en la muestra inteligente debajo de la imagen (las muestras de color son estáticas) y, a continuación, arrastre el controlador de esquina del cuadro de recorte para ajustar el tamaño del área visible de la muestra.
      ![Cambiar el tamaño del recorte inteligente de una imagen.](assets/edit_smart_crops-resize.png)

   * Mueva el cuadro de recorte inteligente. Realice una de las siguientes acciones:

      * Si la imagen solo tiene un recorte inteligente o una muestra inteligente, arrastre el cuadro de recorte a una nueva ubicación.
      * Si la imagen tiene un recorte inteligente y una muestra inteligente, arrastre el cuadro de recorte inteligente a una nueva ubicación. O bien, toque o haga clic en la muestra inteligente situada debajo de la imagen (las muestras de color son estáticas) y, a continuación, arrastre el cuadro de recorte de muestras inteligente a una nueva ubicación.
      ![edit_smart_groups-move](assets/edit_smart_crops-move.png)

   * Deshace todas las ediciones y restaura el recorte inteligente o la muestra inteligente original (solo se aplica a la sesión de edición actual).

      Toque **[!UICONTROL Revertir]** sobre la imagen.

      ![edit_smart_bars-revert](assets/edit_smart_crops-revert.png)



1. Near the upper-right corner of the page, tap **[!UICONTROL Save]**. a continuación, toque **[!UICONTROL Cerrar]** para volver a la carpeta de recursos.

## Eliminación de un perfil de imagen de carpetas {#removing-an-image-profile-from-folders}

Al eliminar un perfil de imagen de una carpeta, las subcarpetas heredan automáticamente la eliminación del perfil de su carpeta principal. Sin embargo, cualquier procesamiento de archivos que se haya producido dentro de las carpetas permanece intacto.

Puede quitar un perfil de imagen de una carpeta desde el menú **[!UICONTROL Herramientas]** o, si está en la carpeta, desde **[!UICONTROL Propiedades]**. En esta sección se describe cómo quitar perfiles de imagen de las carpetas de ambos modos.

### Eliminación de perfiles de imagen de Dynamic Media de las carpetas mediante la interfaz de usuario Perfiles {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Toque el logotipo de AEM y vaya a **[!UICONTROL Herramientas > Recursos > Perfiles]** de imagen.
1. Seleccione el perfil de imagen que desea eliminar de una carpeta o de varias carpetas.
1. Puntee en **[!UICONTROL Eliminar perfil de procesamiento de las carpetas]** y seleccione la carpeta o varias carpetas que desee utilizar para quitar el perfil y toque **[!UICONTROL Eliminar]**.

   Puede confirmar que el perfil de imagen ya no se aplica a una carpeta porque el nombre ya no aparece debajo del nombre de la carpeta.

### Eliminación de perfiles de imagen de Dynamic Media de carpetas mediante Propiedades {#removing-image-profiles-from-folders-via-properties}

1. Toque el logotipo de AEM, desplácese por **[!UICONTROL Recursos]** y, a continuación, por la carpeta desde la que desea quitar un perfil de imagen.
1. En la carpeta, toque la marca de verificación para seleccionarla y, a continuación, **[!UICONTROL Propiedades]**.
1. Seleccione la ficha Perfiles **[!UICONTROL de imagen]** .
1. En el menú desplegable Nombre **** del perfil, seleccione **[!UICONTROL Ninguno]** y, a continuación, toque **[!UICONTROL Guardar y cerrar]**.

   Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.
