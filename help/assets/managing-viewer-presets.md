---
title: Administración de ajustes preestablecidos de visor
description: Creación y administración de ajustes preestablecidos de visor
uuid: 64fcf16a-7c4a-435b-bf1a-f27b8b39a715
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: cf7823f4-82c2-4e36-9b65-3c58359b8104
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/viewer-presets
feature: Ajustes preestablecidos de visor
role: User, Admin
exl-id: 0899e497-88e9-4fc3-a6be-b3a149fb5b32
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '4339'
ht-degree: 14%

---

# Administración de ajustes preestablecidos de visor{#managing-viewer-presets}

Un ajuste preestablecido de visor es una colección de ajustes que determinan cómo ven los usuarios los recursos de medios enriquecidos en sus pantallas de equipo y dispositivos móviles. Si es un administrador, puede crear ajustes preestablecidos de visor. La configuración está disponible para una matriz de opciones de configuración del visor. Por ejemplo, puede cambiar el tamaño de visualización del visor o el comportamiento de zoom.

Para obtener instrucciones sobre la creación y personalización de sus propios ajustes preestablecidos de visor HTML5, consulte la documentación de la API del SDK del visor HTML5 de Dynamic Media *Adobe*. El SDK está disponible en el servidor de publicación IS incrustado en el propio SDK. Cada versión de la biblioteca tiene su propia documentación de SDK incluida.

Ruta: `<scene7_domain>/s7sdk/<library_version>/docs/jsdocs/index.html`.\
Por ejemplo, SDK 3.10: [https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html)

Consulte también la [Guía de referencia de visores de Dynamic Media de Adobe](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html).

En esta sección se describe cómo crear, editar y administrar ajustes preestablecidos de visualizador. Puede aplicar un ajuste preestablecido de visualizador a un recurso cada vez que lo previsualice. Consulte [Aplicación de ajustes preestablecidos de visor](#applying-a-viewer-preset-to-an-asset).

>[!NOTE]
>
>Tenga en cuenta que no se admite la edición de *ajustes preestablecidos de visor predefinidos y listos para usar*. Si intenta editar un ajuste preestablecido de visualizador listo para usar, se le pedirá que guarde el ajuste preestablecido de visualizador con un nuevo nombre.

## Accesibilidad de teclado para visualizadores {#keyboard-accessibility-for-viewers}

Todos los visores integrados admiten la accesibilidad del teclado.

Consulte también [Accesibilidad y navegación del teclado](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html).

## Administración de ajustes preestablecidos de visor {#managing-viewer-presets-1}

Puede agregar, editar, eliminar, publicar, cancelar la publicación y previsualizar ajustes preestablecidos de visualizador en AEM tocando **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Recursos]** > **[!UICONTROL Ajustes preestablecidos de visualizador]**.

![6_5_tools-assets-viewerpresets](assets/6_5_tools-assets-viewerpresets.png)

>[!NOTE]
>
>De forma predeterminada, el sistema muestra 15 ajustes preestablecidos de visualizador al seleccionar Visualizadores en la vista de detalles de un recurso. Puede aumentar este límite. Consulte [Aumento del número de ajustes preestablecidos de visor que se muestran](#increasing-the-number-of-viewer-presets-that-display).

### Compatibilidad del visor con páginas web diseñadas para adaptarse {#viewer-support-for-responsive-designed-web-pages}

Las diferentes páginas Web tienen diferentes necesidades. Por ejemplo, a veces se desea una página web que proporcione un vínculo que abra el visor HTML5 en una ventana de navegador independiente. En otros casos, puede ser necesario incrustar el visor HTML5 directamente en la página de alojamiento. En este último caso, la página web puede tener un diseño estático. O puede ser &quot;interactivo&quot; y mostrarse de forma diferente en diferentes dispositivos o para diferentes tamaños de ventana del navegador. Para satisfacer estas necesidades, todos los visores HTML5 predefinidos y listos para usar que se incluyen con Dynamic Media admiten tanto páginas web estáticas como páginas web diseñadas con capacidad de respuesta.

Consulte [Biblioteca de imágenes interactivas](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/responsive-static-image-library/c-about-responsive-static-image-library.html) en para obtener más información sobre cómo incrustar visores interactivos en las páginas web.

>[!NOTE]
>
>Tenga en cuenta que debe publicar todos los visores integrados antes de usarlos por primera vez.
>Consulte [Ajustes preestablecidos del visualizador de publicaciones].(#publishing-viewer-presets)

### Compatibilidad del sistema con ajustes preestablecidos del visor  {#viewer-preset-system-compatibility}

Todos los ajustes preestablecidos de visor integrados que se incluyen con Dynamic Media son totalmente compatibles con los siguientes sistemas:

* Computadoras de escritorio
* Apple iPhone
* Apple iPad
* Smartphone de Android
* Android Tablet
* Para vídeo, se proporciona compatibilidad adicional con la reproducción de MP4 para [Blackberry](https://developer.blackberry.com/devzone/develop/supported_media/bb_media_support_at_a_glance.html#kba1328730952678) y [Windows Phone](https://msdn.microsoft.com/library/windows/apps/ff462087%28v=vs.105%29.aspx).

### Tipos de medios enriquecidos para ajustes preestablecidos de visor {#rich-media-types-for-viewer-presets}

Los administradores pueden agregar y personalizar los siguientes tipos de medios enriquecidos al crear nuevos ajustes preestablecidos de visor.

<table>
 <tbody>
  <tr>
   <td><strong>Conjunto de carrusel</strong><br /> </td>
   <td><p>Las zonas interactivas, los mapas de imágenes o ambas se añaden a una serie de dos o más imágenes. Un cliente puede obtener una panorámica de las imágenes a la izquierda o a la derecha y, a continuación, hacer clic en un punto interactivo de una imagen para obtener más detalles o para realizar compras directamente desde las páginas de categoría, de inicio o de aterrizaje de un sitio web.</p> </td>
  </tr>
  <tr>
   <td><strong>Dimensional</strong><br /> </td>
   <td><p>Muestra escenas 3D que le permiten girar, recorrer, acercar o volver a entrar en la cámara.</p> </td>
  </tr>
  <tr>
   <td><strong>Zoom flotante </strong></td>
   <td><p>Muestra una segunda imagen del área ampliada junto a la imagen original. No hay controles que utilizar: los usuarios mueven la selección sobre el área que desean ver.</p> <p>Al determinar el uso completo del ancho de banda para este visor, tenga en cuenta que tanto la imagen principal como la imagen flotante se proporcionan en el visor. El tamaño de la imagen principal (ancho y alto del escenario) y el factor de zoom determinan el tamaño de la imagen flotante. Para evitar que el tamaño del archivo flotante sea demasiado grande, equilibre estos dos valores: si tiene un tamaño de imagen principal grande, reduzca el valor del factor de zoom. (La anchura flotante y la altura flotante determinan el tamaño de la ventana flotante, pero no el tamaño de la imagen flotante que se proporciona al visor).</p> <p>Por ejemplo, si el tamaño de la imagen principal es de 350 por 350 píxeles, con un factor de zoom de 3, la imagen flotante resultante es de 1050 por 1050 píxeles. Si el tamaño de la imagen principal es de 300 por 300 píxeles, con un factor de zoom de 4, la imagen flotante es de 1200 por 1200 píxeles. Dependiendo del ajuste de calidad JPEG (los ajustes recomendados están entre 80 y 90), puede reducir el tamaño del archivo de forma significativa. Los factores de zoom recomendados son de 2,5 a 4, dependiendo del tamaño de la imagen principal.</p> </td>
  </tr>
  <tr>
   <td><strong>Zoom en línea</strong></td>
   <td>Muestra una imagen del área ampliada dentro del visor original. No hay controles que usar. Es decir, los usuarios mueven la selección sobre el área que desean ver.</td>
  </tr>
  <tr>
   <td><strong>Conjunto de imágenes</strong></td>
   <td>En el visor de conjuntos de imágenes, los usuarios pueden ver diferentes vistas o variaciones de color de un elemento haciendo clic en una imagen en miniatura. Este visor también ofrece herramientas de zoom para examinar las imágenes de cerca.</td>
  </tr>
  <tr>
   <td><strong>Imagen interactiva</strong></td>
   <td>Las zonas interactivas se añaden a partes de una imagen en las que un cliente puede hacer clic para obtener más información o para realizar compras directamente desde las páginas de aterrizaje, de inicio o de categoría de un sitio web.</td>
  </tr>
  <tr>
   <td><strong>Vídeo interactivo</strong></td>
   <td>Las miniaturas se añaden a los segmentos de cronología de un vídeo en los que un cliente puede hacer clic para obtener más información o para realizar compras directamente desde las páginas de aterrizaje, inicio o categoría de un sitio web.</td>
  </tr>
  <tr>
   <td><strong>Medios mixtos</strong></td>
   <td>Muestra diferentes tipos de medios en un visualizador. Puede incluir conjuntos de giros, conjuntos de imágenes, imágenes y vídeos.</td>
  </tr>
  <tr>
   <td><strong>Imagen panorámica</strong></td>
   <td><p>Los visores Panoramic Image y PanoramicVR representan imágenes panorámicas esféricas para sumergir a los usuarios en una experiencia de visualización de 360° de una habitación, propiedad, ubicación o paisaje.</p> <p>Para que una imagen cargada se califique como un panorama esférico, debe tener una o ambas de las siguientes opciones:</p>
    <ul>
     <li>Una relación de aspecto de 2:1.</li>
     <li>Etiquetado con las palabras clave <code>equirectangular</code>, o <code>spherical</code> y <code>panorama</code>, o <code>spherical </code>y <code>panoramic</code>. Consulte <a href="/help/sites-authoring/tags.md">Uso de etiquetas</a>.</li>
    </ul> <p>Tanto la proporción de aspecto como los criterios de palabra clave se aplican a los recursos panorámicos para la página de detalles de recursos y el componente WCM "Medios panorámicas".</p> <p><strong>Importante</strong>: Este visor solo está disponible en el modo Dynamic Media - Scene7 .</p> </td>
  </tr>
  <tr>
   <td><strong>Recorte inteligente de vídeos</strong><br /> </td>
   <td><p>Utilice este visor para detectar y recortar automáticamente al punto focal de cualquier vídeo.</p> </td>
  </tr>
  <tr>
   <td><strong>Conjunto de giros</strong></td>
   <td>Proporciona varias vistas de una imagen para que los usuarios puedan girar el objeto para examinar los diferentes lados y ángulos.</td>
  </tr>
  <tr>
   <td><strong>Vídeo 360</strong></td>
   <td><p>Utilice el visor de vídeo 360/VR para representar un vídeo equirectangular que ofrezca una experiencia de visualización inmersiva de una habitación, propiedad, ubicación, paisaje o procedimiento médico.</p> <p>Durante la reproducción en una pantalla plana, el usuario controla el ángulo de visualización; la reproducción en dispositivos móviles suele aprovechar sus controles giroscópicos integrados.</p> <p>El visor incluye compatibilidad nativa con la entrega de 360 recursos de vídeo. De forma predeterminada, no es necesaria ninguna configuración adicional para la visualización o reproducción. El vídeo 360 se entrega con extensiones de vídeo estándar como .mp4, .mkv y .mov. El códec más común es H.264.</p> <p><strong>Importante</strong>: Este visor solo está disponible en el modo Dynamic Media - Scene7 .</p> </td>
  </tr>
  <tr>
   <td><strong>Vídeo</strong></td>
   <td><p>Reproduce el vídeo mediante flujo continuo de velocidad de bits progresiva o adaptable. La transmisión de velocidad de bits adaptable realiza automáticamente la detección de dispositivos y ancho de banda para ofrecer el vídeo de calidad adecuada en el formato correcto.</p> </td>
  </tr>
  <tr>
   <td><strong>Zoom vertical</strong></td>
   <td><p>El visor de zoom vertical le permite maximizar una experiencia de visualización de imágenes de producto para ofrecer a los usuarios la mejor representación de un producto. La ubicación vertical de las muestras hace lo siguiente:</p>
    <ul>
     <li>Garantiza que las muestras estén "por encima del pliegue".<br/> Con muestras horizontales, dependiendo del tamaño de la pantalla del escritorio del usuario, las muestras no eran visibles hasta que el usuario se desplazaba hacia abajo por la página. Al colocar las muestras verticalmente en el visor, se garantiza que sean visibles independientemente del tamaño de pantalla del usuario.</li>
     <li>Maximiza el tamaño de la imagen principal.<br /> Con las muestras horizontales, es necesario reservar espacio en la página para garantizar que sean visibles. Esta posición redujo el tamaño de la imagen principal. Sin embargo, con un diseño de muestra vertical, no es necesario asignar este espacio. Como tal, puede maximizar el tamaño de la imagen principal.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Zoom</strong></td>
   <td>Permite a los usuarios acercarse al área haciendo clic en ella. Los usuarios pueden hacer clic en los controles para acercar, alejar y restablecer la imagen a su tamaño predeterminado.</td>
  </tr>
 </tbody>
</table>

### Lista de ajustes preestablecidos de visor integrados {#list-of-out-of-the-box-viewer-presets}

La siguiente tabla identifica todos los ajustes preestablecidos de visor predefinidos y listos para usar que se incluyen con Dynamic Media.

Consulte también [Demostraciones en directo](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html).

Para obtener información sobre las versiones compatibles del navegador web y del sistema operativo de los visores, consulte las Notas de la versión de los visores.

Consulte &quot;Notas de la versión de los visores&quot; en la tabla de contenido de la [Guía de referencia de visores](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html).

>[!NOTE]
>
>Todos los ajustes preestablecidos de visualizador integrados en Dynamic Media ya están activados (activados), pero debe publicarlos.
>Consulte [Ajustes preestablecidos del visualizador de publicaciones](#publishing-viewer-presets).
>
>Los ajustes preestablecidos de visor nuevos que cree y agregue deben activarse *y *publicarse.
>Consulte [Activación o desactivación de ajustes preestablecidos de visualizador](#activating-or-deactivating-viewer-presets) y [Ajustes preestablecidos de visualizador de publicaciones](#publishing-viewer-presets).

<table>
 <tbody>
  <tr>
   <td><strong>Título preestablecido del visor</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Nombre de archivo CSS</strong><br /> </td>
  </tr>
  <tr>
   <td>Carrusel_Dotted_dark</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_dotted_dark.css</code></td>
  </tr>
  <tr>
   <td>Carrusel_Dotted_light</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_dotted_light.css</code></td>
  </tr>
  <tr>
   <td>Carrusel_Numeric_dark</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_numeric_dark.css</code></td>
  </tr>
  <tr>
   <td>Carrusel_Numeric_light</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_numeric_light.css</code></td>
  </tr>
  <tr>
   <td>Dimensional</td>
   <td>Dimensional</td>
   <td><code>html5_dimensionalviewer.css</code></td>
  </tr>
  <tr>
   <td>Flotante</td>
   <td>Zoom flotante</td>
   <td><code>html5_flyoutviewer.css</code></td>
  </tr>
  <tr>
   <td>ImageSet_dark</td>
   <td>Conjunto de imágenes</td>
   <td><code>html5_zoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ImageSet_light</td>
   <td>Conjunto de imágenes</td>
   <td><code>html5_zoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_dark</td>
   <td>Mixed_Media</td>
   <td><code>html5_inlinemixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_light</td>
   <td>Mixed_Media</td>
   <td><code>html5_inlinemixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineZoom</td>
   <td>Zoom flotante</td>
   <td><code>html5_inlinezoomviewer.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_dark</td>
   <td>Mixed_Media</td>
   <td><code>html5_mixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_light</td>
   <td>Mixed_Media</td>
   <td><code>html5_mixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>PanoramicImage</td>
   <td>Panoramic_Image</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>PanoramicImageVR</td>
   <td>Panoramic_Image</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Banner</td>
   <td>Interactive_Image</td>
   <td><code>html5_interactiveimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_dark</td>
   <td>Interactive_Video</td>
   <td><code>html5_interactivevideoviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_light</td>
   <td>Interactive_Video</td>
   <td><code>html5_interactivevideovewer_light.css</code></td>
  </tr>
  <tr>
   <td>SmartCropVideo</td>
   <td>Smart_Crop_Video</td>
   <td><code>html5_smartcropvideoviewer.css</code></td>
  </tr>
  <tr>
   <td>SmartCropVideo_social</td>
   <td>Smart_Crop_Video</td>
   <td><code>html5_smartcropvideoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_dark</td>
   <td>Conjunto de giros</td>
   <td><code>html5_spinviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_light</td>
   <td>Conjunto de giros</td>
   <td><code>html5_spinviewer_light.css</code></td>
  </tr>
  <tr>
   <td><p>Vídeo</p> <p>(Incluye compatibilidad con subtítulos optativos)</p> </td>
   <td>Vídeo</td>
   <td><code>html5_videoviewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video360_social</p> <p>(Incluye controles básicos de reproducción de vídeo, el procesamiento de vídeo se realiza en modo estéreo, el control manual del punto de vista está desactivado, pero el control giroscópico está activado y no hay funciones de medios sociales)</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewersocial.css</code></td>
  </tr>
  <tr>
   <td><p>Video360VR</p> <p>(Diseñado para usuarios finales que utilizan lentes de realidad virtual. Incluye controles básicos de reproducción de vídeo y funciones de medios sociales)</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video_social</p> <p>(Incluye compatibilidad con subtítulos y redes sociales)</p> </td>
   <td>Vídeo</td>
   <td><code>html5_videoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>Zoom_dark<br /> </td>
   <td>Zoom<br /> </td>
   <td><code>html5_basiczoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Zoom_light<br /> </td>
   <td>Zoom</td>
   <td><code>html5_basiczoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_dark<br /> </td>
   <td>Vertical_Zoom</td>
   <td><code>html5_zoomverticalviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_light</td>
   <td>Vertical_Zoom</td>
   <td><code>html5_zoomverticalviewer_light.css</code></td>
  </tr>
 </tbody>
</table>

### Matriz de gestos de visores móviles compatibles {#supported-mobile-viewers-gestures-matrix}

La siguiente tabla identifica los gestos del visor móvil compatibles con los dispositivos iOS, Android 2.x y Android 3.x.

<table>
 <tbody>
  <tr>
   <td><strong>Gesto</strong></td>
   <td><strong>Zoom flotante </strong></td>
   <td><strong>Zoom</strong></td>
   <td><strong>Giro</strong></td>
  </tr>
  <tr>
   <td><p><strong>Arrastrar</strong></p> </td>
   <td><p>Pans</p> </td>
   <td><p>Pans</p> </td>
   <td><p>Pans</p> </td>
  </tr>
  <tr>
   <td><p><strong>Tocar</strong></p> </td>
   <td><p>Muestra la ventana flotante</p> </td>
   <td><p>Muestra u oculta la interfaz de usuario</p> </td>
   <td><p>Muestra u oculta la interfaz de usuario</p> </td>
  </tr>
  <tr>
   <td><p><strong>Pulsar dos veces</strong></p> </td>
   <td><p>No se aplica</p> </td>
   <td><p>Amplía o restablece</p> </td>
   <td><p>Amplía o restablece</p> </td>
  </tr>
  <tr>
   <td><p><strong>Abrir el lápiz</strong></p> </td>
   <td><p>No se aplica</p> </td>
   <td><p>Amplía (solo iOS y Android 3x)</p> </td>
   <td><p>Amplía (solo iOS y Android 3x)</p> </td>
  </tr>
  <tr>
   <td><p><strong>Pellizque</strong></p> </td>
   <td><p>No se aplica</p> </td>
   <td><p>Reduce el tamaño de la página (solo iOS y Android 3x)</p> </td>
   <td><p>Reduce el tamaño de la página (solo iOS y Android 3x)</p> </td>
  </tr>
  <tr>
   <td><p><strong>Deslizar</strong></p> </td>
   <td><p>Desplaza la barra de muestra</p> </td>
   <td><p>Desplazamiento por imágenes</p> </td>
   <td><p>Giros</p> </td>
  </tr>
  <tr>
   <td><p><strong>Flick</strong></p> </td>
   <td><p>Desplaza la barra de muestra</p> </td>
   <td><p>Desplazamiento por imágenes</p> </td>
   <td><p>Giros</p> </td>
  </tr>
 </tbody>
</table>

## Aumento del número de ajustes preestablecidos de visor que se muestran {#increasing-the-number-of-viewer-presets-that-display}

AEM muestra una amplia variedad de ajustes preestablecidos de visualizador al ver un recurso desde **[!UICONTROL Vista de detalles]** > **[!UICONTROL Visualizadores]**. Puede aumentar o disminuir el número de visualizadores que se muestran.

**Para aumentar el número de ajustes preestablecidos de visor mostrados:**

1. Vaya al CRXDE Lite ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Vaya al nodo de listado de ajustes preestablecidos de visor en `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist`

   ![chlimage_1-221](assets/chlimage_1-221.png)

1. En la propiedad **[!UICONTROL limit]**, cambie el **[!UICONTROL valor]**, que se establece en 15 de forma predeterminada, por el número deseado.
1. Vaya a la fuente de datos del ajuste preestablecido de visor en `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist/datasource`

   ![chlimage_1-222](assets/chlimage_1-222.png)

1. En la propiedad limit , cambie el número por el número deseado, por ejemplo `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. Toque **[!UICONTROL Guardar todo]**.

## Creación de un ajuste preestablecido de visualizador {#creating-a-new-viewer-preset}

La creación de ajustes preestablecidos de visualizador le permite aplicar distintos ajustes para ver e interactuar con los recursos. Sin embargo, no es necesario crear nuevos ajustes preestablecidos de visor. Si lo prefiere, puede utilizar los ajustes preestablecidos de visualizador predeterminados que ya se incluyen con AEM Assets.

Si elige crear un nuevo ajuste preestablecido de visualizador, después de guardarlo, el estado del visualizador se activa automáticamente (establecido en **[!UICONTROL On]**) en la página Ajustes preestablecidos de visualizador. Este estado significa que está visible en el componente Dynamic Media y en el componente Medios interactivos y siempre que se obtiene una vista previa de una imagen o un vídeo.

Algunos ajustes preestablecidos de visualizador tienen una configuración exclusiva que puede afectar al uso y al comportamiento general del visualizador. En función del ajuste preestablecido de visualizador que esté creando, es posible que desee tener en cuenta estas consideraciones especiales.

Consulte [Consideraciones especiales para crear un ajuste preestablecido de visualizador interactivo](#special-considerations-for-creating-an-interactive-viewer-preset).

Consulte [Consideraciones especiales para crear un ajuste preestablecido de visor de banners de carrusel](#special-considerations-for-creating-a-carousel-banner-viewer-preset).

**Para crear un ajuste preestablecido de visualizador**

1. En la esquina superior izquierda de AEM, pulse el logotipo de AEM y, a continuación, en el carril izquierdo, pulse **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Recursos] > [!UICONTROL Ajustes preestablecidos de visualizador]**.

   ![6_5_viewerpresets](assets/6_5_viewerpresets.png)

1. En la página Ajustes preestablecidos de visor , en la barra de herramientas, pulse **[!UICONTROL Crear]**.
1. En el cuadro de diálogo **[!UICONTROL Nuevo ajuste preestablecido de visualizador]**, en el campo **[!UICONTROL Nombre de ajuste preestablecido]**, introduzca el nombre del nuevo ajuste preestablecido. Elija un nombre con cuidado; no se pueden editar después de pulsar la opción **[!UICONTROL Crear]**.

   Cuando guarde el ajuste preestablecido más adelante en estos pasos, el nombre aparecerá en la página Ajustes preestablecidos de visor debajo del encabezado de la columna Título preestablecido .

1. En el menú desplegable Tipo de medio enriquecido , seleccione el tipo de ajuste preestablecido de visualizador que desea crear y, a continuación, en la esquina superior derecha de la página, pulse **[!UICONTROL Crear]**.

   Consulte [Tipos de medios enriquecidos para ajustes preestablecidos de visor](#rich-media-types-for-viewer-presets).

1. En la página Editor de ajustes preestablecidos de visualizar, pulse la pestaña **[!UICONTROL Aspecto]**.
1. Realice una de las acciones siguientes:

   * En el menú desplegable **[!UICONTROL Tipo seleccionado]**, seleccione un componente cuyo diseño visual desee personalizar. Como alternativa, puede tocar o hacer clic en cualquier elemento visual del visualizador y seleccionarlo para su configuración.

      El editor visual permite ver qué efecto tiene una propiedad determinada en un estilo. Solo tiene que configurar o ajustar cualquier propiedad para ver instantáneamente qué efecto tiene en el visor con la muestra a la izquierda del editor.

      Las propiedades de estilo CSS para cada tipo de ajuste preestablecido de visualizador se describen en el tema de ayuda &quot;Personalización del *`<viewer name>`* visualizador&quot; de la [Guía de referencia del visualizador](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html). Por ejemplo, si está creando un ajuste preestablecido de visualizador del tipo `Mixed_Media`, consulte [Personalización del visualizador de medios mixtos](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/mixed-media/customing-mixed-media/c-html5-mixedmedia-viewer-customizingviewer.html) para obtener una lista y una descripción de cada propiedad.

   * Si ha definido la configuración de estilo en un archivo CSS independiente, puede cargar el archivo CSS en AEM Assets. Pulse **[!UICONTROL Importar CSS]** debajo del menú desplegable **[!UICONTROL Tipo seleccionado]** (puede que necesite desplazar el editor visual hacia arriba para verlo) para encontrar el archivo CSS cargado y asociarlo al ajuste preestablecido de visor.

      Al importar un archivo CSS, el editor visual comprueba si el CSS utiliza los marcadores de visor correctos. Por ejemplo, si está creando un visor de zoom, todas las reglas CSS que importe deben definirse con su nombre de clase de visor `.s7mixedmediaviewer` definido en un elemento de visor principal.

      Puede importar CSS arbitraria hecha a mano siempre y cuando defina correctamente los marcadores CSS de un visor determinado. (Los marcadores CSS se describen en cualquier tema de ayuda &quot;Personalización del *&lt;nombre del visor>* Visor&quot; en la [Guía de referencia de visores](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html). Por ejemplo, si desea obtener información sobre los marcadores de CSS para el visor de zoom, consulte [Personalización del visor de zoom](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/zoom/customizing-zoom/c-html5-20-zoom-viewer-customizingviewer.html)). Sin embargo, es posible que el editor visual no entienda algunos valores de CSS. En estos casos, el editor visual intenta anular los errores para que el CSS pueda seguir funcionando.
   >[!NOTE]
   >
   >Si prefiere editar la CSS directamente en su formulario sin procesar, pulse **[!UICONTROL Mostrar/Ocultar CSS]** debajo del menú desplegable Tipo seleccionado (puede que necesite desplazar el editor visual hacia arriba para verlo).
   >Al igual que el editor visual, cuando realiza un cambio en una propiedad directamente en el CSS, puede ver instantáneamente qué efecto tiene en la muestra del visor. Y, esa misma propiedad se actualiza automáticamente al mismo tiempo en el editor visual. Como tal, puede utilizar el editor CSS sin procesar o el editor visual, o ambos de forma intercambiable.

   >[!NOTE]
   >
   >Para las ilustraciones de botones, elija la imagen 2x y cargue las ilustraciones de alta resolución. Al trabajar con imágenes interactivas y banners de ventas, también puede seleccionar entre una variedad de botones de puntos interactivos predeterminados.

1. (Opcional) Cerca de la parte superior de la página Editar ajuste preestablecido de visualizador, pulse **[!UICONTROL Escritorio]**, **[!UICONTROL Tablet]** o **[!UICONTROL Teléfono]** para definir de forma exclusiva estilos visuales para distintos tipos de dispositivos y pantallas.
1. En la página Editor de ajustes preestablecidos de visualizador, pulse la pestaña **[!UICONTROL Funcionamiento]**. Como alternativa, puede tocar o hacer clic en cualquier elemento visual del visualizador y seleccionarlo para su configuración.
1. En el menú desplegable **[!UICONTROL Tipo seleccionado]**, seleccione un componente cuyos comportamientos desee cambiar.

   Muchos componentes del editor visual tienen una descripción detallada asociada. Estas descripciones aparecen en cuadros azules al expandir un componente para mostrar sus parámetros asociados.

   Algunos tipos de visualizador tienen componentes que permiten especificar comandos del servicio de imágenes en un campo de texto **[!UICONTROL Comando IS]**. Para obtener una lista de los comandos que puede utilizar, consulte la [Referencia de API del servicio de imágenes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-is-home.html).

   >[!NOTE]
   >
   >**Si utiliza un dispositivo táctil, como un teléfono o una tableta...**
   >
   >
   >Después de escribir un valor en el campo de texto, pulse en cualquier parte de la interfaz de usuario para enviar el cambio y cerrar el teclado virtual. Si pulsa Intro, no se producirá ninguna acción.

1. Cerca de la esquina superior derecha de la página, pulse **[!UICONTROL Guardar]**.
1. Publique el nuevo ajuste preestablecido de visor. Debe publicar el ajuste preestablecido para poder utilizarlo en el sitio web.

   Consulte [Ajustes preestablecidos del visualizador de publicaciones](#publishing-viewer-presets).

### Consideraciones especiales para crear un ajuste preestablecido de visualizador interactivo {#special-considerations-for-creating-an-interactive-viewer-preset}

**Acerca de los modos de visualización de las miniaturas de imágenes en el panel**

Cuando se crea o edita un ajuste preestablecido de visualizador de vídeo interactivo, se puede elegir qué ajuste de modo de visualización se utilizará al seleccionar `InteractiveSwatches` en el menú desplegable **[!UICONTROL Componente seleccionado]** en la pestaña **[!UICONTROL Comportamiento]**. El modo de visualización que elija afecta a cómo y cuándo aparecerán las miniaturas mientras se reproduce el vídeo. Puede elegir un `segment`modo de visualización (predeterminado) o un `continuous` modo de visualización.

<table>
 <tbody>
  <tr>
   <td><strong>Modo de visualización</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Segmento</td>
   <td><p><code>Segment </code>es el modo de visualización predeterminado de los ajustes preestablecidos de visualizador de vídeo interactivo <code>Shoppable_Video_light</code> y <code>Shoppable_Video_dark</code> y de cualquier ajuste preestablecido de visualizador de vídeo interactivo que cree usted mismo.</p> <p>En este modo, cuando hay menos miniaturas asignadas a un segmento de vídeo que el número de puntos visibles en el panel de visualización, las miniaturas de los subsegmentos siguientes o anteriores se extraen <i>no </i>para rellenar cualquier punto vacío en el panel. Es decir, conserva la visualización de muestras asignadas al segmento de vídeo concreto.</p> </td>
  </tr>
  <tr>
   <td>Continuo</td>
   <td><p>En el modo de <code>continuous </code>visualización, si el número de miniaturas de un segmento es menor que el número visible en el panel, el visor incluye automáticamente la visualización de miniaturas del segmento siguiente o del segmento anterior, en los casos en que se muestre la última miniatura.</p> <p>El <a href="/help/assets/interactive-videos.md">vídeo de este tema</a> es un ejemplo del modo de visualización <code>continuous </code>.</p> </td>
  </tr>
 </tbody>
</table>

**Acerca del comportamiento de desplazamiento automático en el visualizador de vídeo interactivo**

El comportamiento de desplazamiento automático de las miniaturas del visor de vídeo interactivo funciona independientemente del modo de visualización que haya elegido.

Cuando cree o edite un ajuste preestablecido de visualizador de vídeo interactivo, accede al desplazamiento automático desde la pestaña Comportamiento. En la pestaña Comportamiento, en el menú desplegable **[!UICONTROL Componentes seleccionados]**, pulse **[!UICONTROL Muestras interactivas]**. La casilla de verificación Desplazamiento automático aparece debajo del campo de texto Comando IS.

Si desactiva el **[!UICONTROL desplazamiento automático]** (desactive la casilla de verificación) en el ajuste preestablecido de visualizador, durante la reproducción del vídeo por parte del usuario, el panel solo muestra la primera imagen en miniatura durante toda la duración del vídeo. Sin embargo, un usuario puede desplazarse manualmente por las miniaturas utilizando los iconos de flecha arriba y abajo, si lo desea.

Al activar (seleccionar) **[!UICONTROL Desplazamiento automático]** en el ajuste preestablecido de visualizador, durante la reproducción de vídeo, las imágenes en miniatura asignadas a un segmento de vídeo se desplazan hasta la vista al principio de un segmento. Sin embargo, hay instancias en las que ciertas miniaturas de un segmento se muestran el doble de tiempo que otras miniaturas antes o después de este segmento. Este comportamiento se produce porque el número de miniaturas de un segmento es mayor que el número visible en el panel y no se puede dividir de manera uniforme.

Como ejemplo, supongamos que tiene un segmento de vídeo de 30 segundos. Además, hay un total de nueve miniaturas para mostrar durante los 30 segundos. El tamaño del navegador es tal que hay cuatro posiciones de miniaturas visibles en el panel de visualización. El segmento de vídeo de 30 segundos se divide en tres subsegmentos. La tabla siguiente muestra el desglose de las miniaturas que se muestran para un subsegmento de tiempo determinado:

| **Subsegmento de vídeo** | **Tiempo de subsegmento en segundos** | **Miniaturas visibles en el panel** |
|---|---|---|
| 1 | 0-10 | 1, 2, 3, 4 |
| 2 | 10-20 | 4, 5, 6, 7 |
| 3 | 20-30 | 6, 7, 8, 9 |

El subsegmento de vídeo 3 no se extiende más allá de las miniaturas asignadas a él. También observe que las miniaturas 4, 6 y 7 son visibles en el panel el doble de tiempo que las demás miniaturas.

La lógica que utiliza el visor para ver cuántas miniaturas se muestran en el panel en función del número de posiciones disponibles es la siguiente:

* Número de subsegmentos = redondear al subsegmento siguiente (número de miniaturas/número de espacios visibles en el panel de miniaturas, según el tamaño de la ventana del navegador).
Con el ejemplo de la tabla anterior, 9 miniaturas / 4 ranuras = 2,25; la lógica del visor lo redondea a tres subsegmentos.

* Número de miniaturas = redondear a la siguiente miniatura (número de miniaturas/número de subsegmentos de vídeo).
Con el ejemplo de la tabla anterior, 9 miniaturas / 3 subsegmentos de vídeo = 3 miniaturas.

* Duración del subsegmento = duración total del vídeo/número de subsegmentos de vídeo.
Con el ejemplo de la tabla anterior, 30 segundos / 3 subsegmentos de vídeo = 10 segundos de visualización de cada subsegmento de vídeo.

#### Consideraciones especiales para la creación de ajustes preestablecidos de visualizador de titular de carrusel {#special-considerations-for-creating-a-carousel-banner-viewer-preset}

Al crear ajustes preestablecidos de visor de titular de carrusel, se puede acceder a cambiar el estilo de las zonas interactivas de la siguiente manera:

|  | **Descripción** | **Acciones** |
|---|---|---|
| **[!UICONTROL Icono de zona interactiva]** | Cambiar el icono utilizado para la zona interactiva | Para cambiar la imagen del icono de zona interactiva, en la pestaña **[!UICONTROL Aspecto]**, en **[!UICONTROL Componente seleccionado]**, pulse **[!UICONTROL ImageMapEffect]**. En **[!UICONTROL Icono]**, seleccione **[!UICONTROL Fondo]** y, en el campo **[!UICONTROL Imagen]**, vaya a la imagen de fondo que desee. |

## Activación o desactivación de ajustes preestablecidos de visor {#activating-or-deactivating-viewer-presets}

Los ajustes preestablecidos de visor disponibles en la interfaz de usuario dependen de los que estén activos en el modo Autor. De forma predeterminada, un ajuste preestablecido de visualizador es &quot;Activado&quot; después de crearlo. Si desactiva el ajuste preestablecido, no lo verá en modo Autor. Si se publica el ajuste preestablecido. siempre se publicará independientemente de si está activada o desactivada. Puede que desee desactivar los ajustes preestablecidos de visor si la lista es demasiado complicada o si no desea que haya un ajuste preestablecido de visor disponible para su uso.

**Para activar o desactivar ajustes preestablecidos de visor**

1. En la esquina superior izquierda de AEM, pulse el logotipo de AEM y, a continuación, en el carril izquierdo, pulse **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Recursos]** > **[!UICONTROL Ajustes preestablecidos de visualizador]**.
1. En la página Ajuste preestablecido de visualizador, en el encabezado de columna **[!UICONTROL Estado]**, pulse el botón de alternancia para activar o desactivar un ajuste preestablecido de visualizador.

   Los ajustes preestablecidos de visor que se activan tienen el botón de alternancia a la derecha, dentro de un cuadro azul; los ajustes preestablecidos de visualizador desactivados tienen la opción que aparece a la izquierda, dentro de un cuadro gris claro.

## Ajustes preestablecidos del visualizador de publicaciones {#publishing-viewer-presets}

Activar (o activar) el estado de un ajuste preestablecido de visualizador significa que está visible en el componente Dynamic Media, en el componente de Medios interactivos y siempre que se vea un recurso.

Sin embargo, para *entregar* un recurso con un ajuste preestablecido de visualizador, también se debe publicar el ajuste preestablecido de visualizador. Todos los ajustes preestablecidos de visualizador deben activarse *y* publicarse para obtener la URL o el código incrustado de un recurso. Debe activar y publicar todos los ajustes preestablecidos de visualizador integrados que se incluyen con Dynamic Media. Los ajustes preestablecidos de visualizador personalizado que cree y agregue se activan automáticamente, pero también se deben publicar.

Consulte [Activación o desactivación de ajustes preestablecidos de visor](#activating-or-deactivating-viewer-presets).

Consulte también [Vista previa de recursos](/help/assets/previewing-assets.md).

**Para publicar ajustes preestablecidos de visor:**

1. En la esquina superior izquierda de AEM, pulse el logotipo de AEM y, a continuación, en el carril izquierdo, pulse **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Recursos]** > **[!UICONTROL Ajustes preestablecidos de visualizador]**.
1. Seleccione uno o varios ajustes preestablecidos de visor que desee publicar.
1. En la barra de herramientas, pulse el icono **[!UICONTROL Publicar]**.

## Ordenar ajustes preestablecidos del visualizador {#sorting-viewer-presets}

1. En la esquina superior izquierda de AEM, pulse el logotipo de AEM y, a continuación, en el carril izquierdo, pulse **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Recursos]** > **[!UICONTROL Ajustes preestablecidos de visualizador]**.
1. Haga clic en **[!UICONTROL Título preestablecido]**, **[!UICONTROL Tipo]**, **[!UICONTROL Publicado]** o **[!UICONTROL Estado]** para ordenar por ese encabezado de la columna. Por ejemplo, haga clic en **[!UICONTROL Tipo]** para ordenar los tipos de ajustes preestablecidos de visualizador en orden alfabético o alfabético inverso.

## Edición de ajustes preestablecidos de visor {#editing-viewer-presets}

Tenga en cuenta que no se admite la edición de *ajustes preestablecidos de visor predefinidos y listos para usar*. Si edita un ajuste preestablecido de visualizador incorporado, se le pedirá que lo guarde con un nuevo nombre.

**Para editar ajustes preestablecidos de visor:**

1. En la esquina superior izquierda del Experience Manager, pulse el logotipo de AEM y, a continuación, en el carril izquierdo, pulse **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Recurso]** > **[!UICONTROL Ajustes preestablecidos de visualizador]**.
1. Seleccione un ajuste preestablecido marcando la casilla a la izquierda del título del ajuste preestablecido de visualizador.
1. En la barra de herramientas, pulse **[!UICONTROL Editar]**.
1. En la página **[!UICONTROL Editor]** de ajustes preestablecidos de visualizador, realice los cambios que desee con las opciones que se encuentran en las pestañas **[!UICONTROL Aspecto]** y **[!UICONTROL Comportamiento]**.

   En la pestaña **[!UICONTROL Aspecto]**, cerca de la esquina superior izquierda de la página Editor de ajustes preestablecidos de visualizador, pulse **[!UICONTROL Escritorio]**, **[!UICONTROL Tablet]** o **[!UICONTROL Teléfono]** para cambiar el modo de presentación del recurso.

1. Cerca de la esquina superior derecha de la página, realice una de las siguientes acciones:

   * Toque **[!UICONTROL Guardar]** para guardar los cambios y volver a la página Ajuste preestablecido de visor.
   * Toque **[!UICONTROL Cancelar]** para anular los cambios realizados y volver a la página Ajuste preestablecido de visor.

## Eliminación de ajustes preestablecidos de visor personalizados {#deleting-custom-viewer-presets}

Puede eliminar los ajustes preestablecidos de visor que haya creado y agregado a Dynamic Media.

**Eliminar ajustes preestablecidos de visor personalizado**

1. En la esquina superior izquierda de AEM, pulse el logotipo de AEM y, a continuación, en el carril izquierdo, pulse **[!UICONTROL Herramientas]** (icono de martillo) **[!UICONTROL Recursos]** > **[!UICONTROL Ajustes preestablecidos de visualizador]**.
1. En la página Ajustes preestablecidos de visor , marque un Título preestablecido y, a continuación, pulse el icono **[!UICONTROL Papelera]**.
1. Toque **[!UICONTROL Eliminar]**.

## Aplicación de ajustes preestablecidos de visualizador a un recurso {#applying-a-viewer-preset-to-an-asset}

Si ya ha publicado el recurso y el visualizador seleccionado, los botones **[!UICONTROL URL]** e **[!UICONTROL Incrustar]** aparecerán después de seleccionar un ajuste preestablecido de visualizador.

**Para aplicar un ajuste preestablecido de visualizador a un recurso:**

1. Abra el recurso y, cerca de la esquina superior izquierda de la página, pulse el menú desplegable y, a continuación, seleccione **[!UICONTROL Visualizadores]**.

   >[!NOTE]
   >
   >Si ya ha publicado el recurso y el visualizador seleccionado, los botones **[!UICONTROL URL]** e **[!UICONTROL Incrustar]** aparecerán después de seleccionar un ajuste preestablecido de visualizador.

1. Seleccione un ajuste preestablecido de visualizador en el panel izquierdo para aplicarlo al recurso.

   Puede [copiar la dirección URL para compartir](/help/assets/linking-urls-to-yourwebapplication.md) con otros usuarios.

## Entrega de recursos con ajustes preestablecidos de visor {#delivering-assets-with-viewer-presets}

Para obtener las direcciones URL de los ajustes preestablecidos de visor, consulte [Vinculación de direcciones URL a la aplicación web](/help/assets/linking-urls-to-yourwebapplication.md). Consulte también [Incrustación del visualizador de vídeo en una página web](/help/assets/embed-code.md).

Si utiliza AEM como WCM, puede añadir recursos utilizando los ajustes preestablecidos de visor directamente en la página. Consulte [Adición de recursos de Dynamic Media a páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).
