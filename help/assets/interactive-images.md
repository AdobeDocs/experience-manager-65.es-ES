---
title: Imágenes interactivas
description: Aprenda a trabajar con imágenes interactivas en Dynamic Media
uuid: 0bdb73f7-6ce9-4cdf-b6b5-a4d3d4e19a23
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: a6f58f6a-015a-4ced-941c-ef1b6d3e1d6f
docset: aem65
feature: Imágenes interactivas
role: User, Admin
exl-id: 8a609024-e9e6-4805-8306-48d095110eb6
source-git-commit: 4b8369de9e6a10b73115d53358ce98729d92ed44
workflow-type: tm+mt
source-wordcount: '4277'
ht-degree: 1%

---

# Imágenes interactivas{#interactive-images}

Puede hacer que las imágenes estáticas sean ricas y atractivas para los clientes arrastrando y soltando puntos interactivos &quot;de ventas&quot; en una imagen. Los hotspots de ventas combinan información adicional sobre un producto o servicio con una capacidad directa y de punto de venta &quot;Añadir al carro&quot; o &quot;Comprar&quot;. Los clientes pueden seleccionar estos puntos interactivos y estar vinculados directamente al producto o servicio, agregarlos a un carro de compras o estar vinculados a una página web. Las experiencias directas como estas aumentan las participaciones de los clientes y las conversiones en el sitio web.

El siguiente es un banner de ventas con una ventana emergente de vista rápida. Un usuario activa la vista rápida seleccionando el círculo o la &quot;zona interactiva&quot; en el modelo.

![chlimage_1-152](assets/chlimage_1-368.png)

Consulte imágenes interactivas en acción en la página web anterior. Para ello, vaya a:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html)

## Ver cómo se crean los titulares de imagen interactivos {#watch-how-interactive-image-banners-are-created}

Reproduzca un tutorial en [cómo se crean los banners de imagen interactivos](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner) (10 minutos y 33 segundos). También aprenderá a previsualizar, editar y distribuir banners de imagen interactivos.

## Inicio rápido: Imágenes interactivas {#quick-start-interactive-images}

La siguiente descripción paso a paso del flujo de trabajo está diseñada para ayudarle a poner en marcha las imágenes interactivas con rapidez en Adobe Experience Manager Assets.

Busque el encabezado **Example** dentro de algunas de las tareas de inicio rápido. Contiene un breve tutorial basado en el siguiente ejemplo de página web que aún no tiene imágenes interactivas agregadas:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)

El tutorial ayuda a ilustrar los pasos para integrar imágenes interactivas en su propio sitio web.

Pasos de imágenes interactivas:

1. **(Opcional) Identifique las variables de puntos interactivos** : si utiliza Recursos de Experience Manager y Dynamic Media de forma independiente, comience por identificar las variables dinámicas que se usan en la implementación de vista rápida existente. A continuación, puede introducir datos de puntos interactivos al crear la imagen interactiva. Consulte [(Opcional) Identificar variables de puntos interactivos](#optional-identifying-hotspot-variables).
Sin embargo, si utiliza Adobe Experience Manager Sites, Adobe Experience Manager eCommerce, o ambos, este paso no es necesario.
Consulte [eCommerce concepts in Experience Manager Assets](/help/commerce/cif-classic/administering/concepts.md).

1. **(Opcional) Crear un ajuste preestablecido de visualizador de imagen interactiva** : personalice la imagen gráfica que se utiliza para representar zonas interactivas. No es necesario crear su propio ajuste preestablecido de visualizador de imagen interactiva si quiere usar el ajuste preestablecido de visualizador de imagen interactiva predeterminado, denominado `Shoppable_Banner` en su lugar.
Consulte [(Opcional) Crear un ajuste preestablecido de visualizador de imagen interactivo](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset).

1. **Cargar un banner de imagen** : cargue banners de imagen que desee hacer interactivos.
Consulte [Cargar un banner de imagen](#uploading-an-image-banner).

1. **Agregar zonas interactivas a un banner de imagen** : agregue una o varias zonas interactivas a un banner de imagen y asocie cada una de ellas a una acción como un hipervínculo, una vista rápida o un fragmento de experiencia. Después de agregar zonas interactivas, terminará esta tarea publicando la imagen interactiva.

   * Consulte [Agregar zonas interactivas a un titular de imagen](#adding-hotspots-to-an-image-banner).
   * Consulte [Vista previa de imágenes interactivas](#optional-previewing-interactive-images) - Opcional. Si lo desea, puede ver una representación del banner de ventas y probar su interactividad.
   * Consulte [Publicar recursos](/help/assets/publishing-dynamicmedia-assets.md) para obtener más información sobre cómo publicar recursos de imagen interactivos.

1. **Agregar una imagen interactiva a su sitio web** : si usa Sitios Experience Manager o Comercio electrónico, o ambos, puede agregar la imagen interactiva a una página web en Experience Manager. Arrastre el componente Medios interactivos a la página. Consulte [Agregar recursos de Dynamic Media a páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).

   Si utiliza Recursos de Experience Manager y Dynamic Media de forma independiente, debe copiar el código incrustado en el sitio web y, a continuación, integrarlo con la vista rápida existente. Consulte [Integrar una imagen interactiva con su sitio web](#integrating-an-interactive-image-with-your-website).

   Si utiliza un WCM de terceros (Web Content Manager), debe integrar el nuevo vídeo interactivo con la implementación de vista rápida existente que se utiliza en el sitio web. Consulte [Integrar una imagen interactiva con una vista rápida](#integrating-an-interactive-image-with-an-existing-quickview) existente.

## (Opcional) Identifique las variables de puntos interactivos {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>Esta tarea solo es necesaria si los siguientes son verdaderos:
>
>* Desea añadir interactividad a la imagen activando en Quickview.
>* Su implementación de Experience Manager *no* utiliza un marco de integración de comercio electrónico para extraer datos de productos a Experience Manager desde cualquier solución de comercio electrónico, como IBM® WebSphere® Commerce, Elastic Path, hybris o Intershop. Consulte [eCommerce concepts in Experience Manager Assets](/help/commerce/cif-classic/administering/concepts.md).

>
>
Si su implementación de Experience Manager utiliza eCommerce, puede omitir esta tarea y continuar con la siguiente tarea.

Comience por identificar las variables dinámicas que usa la implementación de vista rápida existente, de modo que pueda introducir datos de zona interactiva para crear la imagen interactiva.

Al agregar zonas interactivas a una imagen de titular en Recursos Experience Manager, debe asignar un SKU (unidad de mantenimiento de existencias) y variables adicionales opcionales a cada zona interactiva. Estas variables de puntos interactivos se utilizan más adelante para hacer coincidir puntos interactivos con contenido de vista rápida.

Es importante identificar correctamente el número y el tipo de variables que se asociarán con los datos de puntos interactivos. Cada zona interactiva agregada a una imagen de banner debe contener suficiente información para identificar el producto de forma inequívoca en el sistema back-end existente.

Existen diferentes maneras de identificar un conjunto de variables que se utilizarán para los datos de puntos interactivos.

A veces es suficiente consultar a los especialistas de TI responsables de la implementación de Quickview existente. Es probable que los especialistas en TI sepan cuál es el conjunto mínimo de datos necesario para la identificación de Quickview en el sistema. Sin embargo, también es posible simplemente analizar el comportamiento existente del código front-end.

La mayoría de las implementaciones de vista rápida utilizan el siguiente paradigma:

* El usuario activa un elemento de interfaz de usuario en el sitio web. Por ejemplo, si selecciona el botón &quot;Vista rápida&quot;.
* El sitio web envía una solicitud de Ajax al servidor para cargar los datos o el contenido de la vista rápida, si es necesario.
* Los datos de vista rápida se traducen al contenido como preparación para su renderización en la página web.
* Por último, el código front-end procesa visualmente dicho contenido en la pantalla.

El método entonces es visitar diferentes áreas del sitio web existente donde se implementa la función Vista rápida. A continuación, se déclencheur la vista rápida y se captura la URL de Ajax que envía la página web para cargar los datos o el contenido de la vista rápida.

Normalmente no es necesario que utilice ninguna herramienta de depuración especializada. Los navegadores web modernos cuentan con inspectores web que realizan un trabajo adecuado. A continuación se indican algunos ejemplos de exploradores web que incluyen inspectores web:

* Para ver todas las solicitudes HTTP salientes en Google Chrome, pulse F12 para abrir el panel Herramientas para desarrolladores y, a continuación, seleccione la pestaña Red.
En un Mac, pulse Comando+Opción+I para abrir el panel Herramientas para desarrolladores y, a continuación, seleccione la ficha Red.

* En Firefox, puede activar el complemento Firebug pulsando F12 y utilizando su pestaña Red, o puede utilizar la herramienta Inspector integrada y su pestaña Red.
En un Mac, pulse Comando+Opción+I para abrir el panel Herramientas para desarrolladores y, a continuación, seleccione la ficha Inspector .

Cuando la supervisión de red está activada en el explorador, ponga en déclencheur la vista rápida en la página.

Ahora, busque la URL de Ajax de vista rápida en el registro de red y copie la URL grabada para su análisis futuro. Por lo general, cuando se déclencheur la vista rápida hay numerosas solicitudes que se envían al servidor. Normalmente, la URL de Ajax de vista rápida es una de las primeras de la lista. Tiene una ruta o parte de una cadena de consulta compleja y su tipo MIME de respuesta es `text/html`, `text/xml` o `text/javascript`.

Durante este proceso, es importante visitar diferentes áreas del sitio web, con diferentes tipos y categorías de productos. El motivo es que las URL de vista rápida pueden tener partes que son comunes para una categoría de sitio web determinada, pero cambian solo si visita un área diferente del sitio web.

En el caso más simple, la única parte de la variable en la URL de vista rápida es el SKU del producto. En este caso, el valor SKU es la única pieza de datos que necesita para agregar zonas interactivas a la imagen del banner.

Sin embargo, en casos complejos, la URL de vista rápida tiene diferentes elementos además del SKU, como el ID de categoría, el código de color y el código de tamaño. En estos casos, cada elemento es una variable independiente en la definición de datos de puntos interactivos de la función de imagen interactiva de ventas en Recursos Experience Manager.

Veamos los siguientes ejemplos de direcciones URL de vista rápida y las variables de puntos interactivos resultantes:

<table>
  <tbody>
  <tr>
    <td><p>SKU único, que se encuentra en la cadena de consulta.</p> </td>
    <td><p>Las direcciones URL de vista rápida registradas incluyen lo siguiente:</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>La única parte de variable en la dirección URL es el valor del parámetro de cadena de consulta productId= y es claramente un valor SKU. Por lo tanto, las zonas interactivas solo necesitan campos de SKU rellenados con valores como <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU único, que se encuentra en la ruta de URL.</p> </td>
    <td><p>Las direcciones URL de vista rápida registradas incluyen lo siguiente:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte variable se encuentra en la última parte de la ruta y se convierte en el valor SKU de las zonas interactivas: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU e ID de categoría en la cadena de consulta.</p> </td>
    <td><p>Las direcciones URL de vista rápida registradas incluyen lo siguiente:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>En este caso, hay dos partes diferentes en la dirección URL. El SKU se almacena en el parámetro <code>prodId</code> y el ID de categoría<code></code> se almacena en el parámetro <code>category=</code>.</p> <p>Como tal, las definiciones de puntos interactivos son pares. Es decir, un valor de SKU y una variable adicional llamada <code>categoryId</code>. Los pares resultantes son los siguientes:</p>
    <ul>
      <li><p>El SKU es <strong><code>305466</code></strong> y <code>categoryId</code> es <code>1100004</code>.</p> </li>
      <li><p>El SKU es <strong><code>310181</code></strong> y <code>categoryId</code> es <strong><code>1100004</code></strong>.</p> </li>
      <li><p>El SKU es <strong><code>308706</code></strong> y <code>categoryId</code> es <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Ejemplo**

Puede aplicar el mismo enfoque utilizado en los tres ejemplos anteriores a la página web de demostración:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)

La página web de demostración tiene varias miniaturas de productos, cada una con un botón de vista rápida etiquetado como &quot;Ver más&quot;. Con la herramienta de depuración del explorador web aún activada, seleccione cada botón y anote las URL de vista rápida registradas. Después de activar los cuatro productos de Quickview disponibles en la página, tiene la siguiente lista de solicitudes de Quickview realizadas en el servidor:

* `/datafeed/Male-Windbreaker.json`
* `/datafeed/Male-SimpleHenley.json`
* `/datafeed/Male-CamoPullover.json`
* `/datafeed/Female-QuiltedDownJacket.json`

Al examinar las llamadas al servidor, verá que la información específica del producto solo está presente en la ruta de solicitud. También observa que la cadena de consulta no se utiliza en absoluto y que hay dos tipos distintos de fragmentos de datos involucrados:

* El primer tipo es Masculino o Femenino. Puede llamar a esta &quot;categoría de producto&quot;.
* El segundo tipo es el nombre del producto, como CamoPullover. Puede suponer que esta información es el SKU del producto.

Dada esta información, toda la URL de vista rápida tiene el siguiente patrón:

`/datafeed/$categoryId$-$SKU$.json`

En función de este análisis, utilizaría `categoryId` y `SKU` para las zonas interactivas.

Ya está listo para cargar un titular de imagen y agregarle zonas interactivas mediante la función de imagen interactiva de ventas en Recursos Experience Manager.

## (Opcional) Crear un ajuste preestablecido de visualizador de imagen interactivo {#optional-creating-an-interactive-image-viewer-preset}

Puede elegir utilizar el ajuste preestablecido predeterminado y listo para usar del visualizador de imagen interactiva llamado `Shoppable_Banner` que se incluye con los recursos de Experience Manager. O puede crear su propio ajuste preestablecido de visualizador personalizado para utilizarlo con imágenes interactivas.

Al crear un ajuste preestablecido personalizado del visualizador de imagen interactiva, puede determinar el aspecto de las zonas interactivas en el banner de imagen. Como parte de la creación del ajuste preestablecido de visualizador, puede elegir utilizar un gráfico de zona interactiva de una galería de imágenes predefinidas.

Después de guardar el ajuste preestablecido de visualizador, se activa automáticamente (se activa) en la página de lista Ajustes preestablecidos de visualizador en Recursos de Experience Manager. Esta funcionalidad significa que está visible en el componente de Medios interactivos y siempre que se vea un recurso. Sin embargo, para *entregar* un banner interactivo con este ajuste preestablecido de visualizador, también debe *publicar* el ajuste preestablecido de visualizador. Esta regla es verdadera para los ajustes preestablecidos de visor personalizados o predeterminados.

**Para crear un ajuste preestablecido de visualizador de imagen interactiva:**

1. En el carril izquierdo, vaya a **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Viewer Presets]**.
1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Crear]**.
1. En el cuadro de diálogo Nuevo ajuste preestablecido de visualizador, escriba un nombre para describir el ajuste preestablecido de visualizador de banners interactivo.

   El título aparece en la página de lista Ajustes preestablecidos de visor después de guardarlo.

1. En el menú desplegable Tipo de medio enriquecido, seleccione **[!UICONTROL Imagen interactiva]**.
1. Seleccione **[!UICONTROL Crear]**.
1. En la página Editar ajuste preestablecido de visualizador, seleccione la pestaña **[!UICONTROL Aspecto]**.
1. Realice una de las acciones siguientes:

   * Para cargar su propia imagen de zona interactiva que desee utilizar en imágenes, seleccione el icono Selector de recursos . En la página Seleccionar contenido , vaya a la imagen de zona interactiva que desee utilizar, selecciónela y, a continuación, seleccione el icono Marca de verificación en la esquina superior derecha.
   * Para seleccionar una imagen de zona interactiva predefinida, seleccione el icono Galería de puntos interactivos . En la paleta Galería de puntos interactivos, seleccione la imagen de zona interactiva que desee utilizar.

1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]**.

   Asegúrese de publicar el nuevo ajuste preestablecido de visor.

   Consulte [Ajustes preestablecidos de visualizador de publicaciones que ha agregado](/help/assets/managing-viewer-presets.md#publishing-viewer-presets).

   Ya está listo para cargar un titular de imagen.

## Cargar un titular de imagen {#uploading-an-image-banner}

Si ya ha cargado las imágenes que desea usar, avance al siguiente paso, [Añadir zonas interactivas a un titular de imagen](#adding-hotspots-to-an-image-banner).

**Para cargar un titular de imagen:**

1. Cargue banners de imagen que desee hacer interactivos.

   Consulte [Carga de recursos](/help/assets/manage-assets.md#uploading-assets).

   Ya está listo para agregar zonas interactivas al titular de la imagen; consulte la siguiente tarea a continuación.

## Agregar zonas interactivas a un banner de imagen {#adding-hotspots-to-an-image-banner}

Puede agregar zonas interactivas a un banner de imagen mediante el editor de la página Administración de puntos interactivos .

Cuando agregue zonas interactivas, puede definirlas como una visualización emergente de vista rápida, como un hipervínculo o un fragmento de experiencia.

Consulte [Fragmentos de experiencias](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
>
>Las herramientas de uso compartido de medios sociales en Imagen interactiva no son compatibles cuando se incrusta el visor en un fragmento de experiencia. Para solucionar este problema, puede utilizar o crear ajustes preestablecidos de visualizador que no tengan herramientas de uso compartido en redes sociales. Estos ajustes preestablecidos de visor permiten incrustarlos correctamente en fragmentos de experiencias.

Las opciones Deshacer y Rehacer, cerca de la esquina superior derecha de la página, son compatibles durante la sesión de creación/edición actual.

Cuando termine de crear la imagen interactiva, puede utilizar Vista previa para ver una representación de cómo la imagen interactiva aparece para los clientes.

Consulte [(Opcional) Vista previa de imágenes interactivas](#optional-previewing-interactive-images).

>[!NOTE]
>
>Cuando se añaden zonas interactivas a una imagen en una imagen interactiva o un titular de carrusel, la información del punto interactivo se almacena en la misma ubicación de metadatos. Esa ubicación es relativa a la ubicación de la imagen, independientemente de si es una imagen interactiva o un titular de carrusel. Esta funcionalidad significa que puede reutilizar fácilmente la misma imagen (junto con sus datos de puntos interactivos definidos) en cualquier visor.
Los titulares de carrusel admiten mapas de imágenes en imágenes que también pueden contener zonas interactivas; las imágenes interactivas no. Tenga en cuenta esta regla si desea crear una imagen interactiva o un titular de carrusel que utilice la misma imagen. Puede crear imágenes interactivas y titulares de carrusel utilizando copias independientes de la misma imagen.
Consulte también [Banners de carrusel](/help/assets/carousel-banners.md).

>[!NOTE]
Si edita imágenes interactivas con zonas interactivas y recorta la imagen, se eliminarán las zonas interactivas.

**Para agregar zonas interactivas a un titular de imagen:**

1. En la vista Recursos, desplácese hasta el banner de imagen que desee convertir en interactivo.
1. Realice una de las acciones siguientes:

   * Pase el ratón sobre la imagen y, a continuación, seleccione **[!UICONTROL Seleccionar]** (icono de marca de verificación). En la barra de herramientas, seleccione **[!UICONTROL Editar]**.

   * Pase el ratón sobre la imagen y, a continuación, seleccione **[!UICONTROL Más acciones]** (icono de tres puntos) **[!UICONTROL Editar]**.

   * Seleccione la imagen para abrirla en la página Vista de detalles . En la barra de herramientas, seleccione **[!UICONTROL Editar]**.

1. Cerca de la esquina superior izquierda de la página, seleccione **[!UICONTROL Agregar zona interactiva]** (icono con el dedo) para abrir la página de administración de puntos interactivos.
1. Cerca de la esquina superior izquierda de la página, seleccione **[!UICONTROL Zona interactiva]**.

   1. Cerca de la esquina superior izquierda de la página Administración de puntos interactivos, seleccione **[!UICONTROL Zona interactiva]**.
   1. En la imagen, seleccione una ubicación en la que desee que aparezca el punto interactivo. Si es necesario, arrastre la zona interactiva para ajustar su ubicación.
   1. Agregue más zonas interactivas según sea necesario repitiendo los pasos a y b.
   1. (Opcional) Para eliminar una zona interactiva, selecciónela en la imagen y, a continuación, seleccione **[!UICONTROL Eliminar]** (icono de la papelera) en el encabezado **[!UICONTROL Zonas interactivas]**.

1. En el campo de texto Nombre , escriba el nombre de la zona interactiva. Este nombre también aparece en la lista desplegable Zona interactiva seleccionada .
1. Realice una de las acciones siguientes:

   * Seleccione **[!UICONTROL Quickview]**.

      * Si es Experience Manager de Sitios o cliente de comercio electrónico, seleccione el icono Selector de productos (lupa) para abrir la página Seleccionar producto . Seleccione el producto que desea utilizar y, a continuación, seleccione **[!UICONTROL Seleccionar]** en la esquina superior derecha de la página para que pueda volver a la página de administración de puntos interactivos.
      * Si es *no* cliente de Sites Experience Manager o comercio electrónico

         * Consulte [Identificar variables de puntos interactivos](#optional-identifying-hotspot-variables); debe definir estas variables.
         * A continuación, introduzca manualmente el valor de SKU. En el campo de texto Valor de SKU , escriba el SKU del producto (unidad de mantenimiento de stock), que es un identificador único para cada producto o servicio distinto que ofrezca. El valor SKU introducido rellena automáticamente la parte variable de la plantilla de vista rápida, de modo que el sistema sepa asociar la zona interactiva seleccionada con la vista rápida de un SKU concreto.
         * (Opcional) Si hay otras variables dentro de la vista rápida que debe utilizar para identificar un producto, seleccione **[!UICONTROL Agregar variable genérica]**. En el campo de texto, especifique una variable adicional. Por ejemplo, `category=Males` es una variable agregada.
   * Seleccione **[!UICONTROL Hipervínculo]**.

      * Si es cliente de Sites Experience Manager, seleccione el icono Selector de sitio (carpeta) para navegar a una dirección URL. El método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a páginas de sitios Experience Manager.
      * Si es cliente independiente, en el campo de texto HREF especifique la ruta de URL completa a una página web vinculada.

   Asegúrese de especificar si desea abrir el vínculo en una nueva pestaña del explorador (opción predeterminada recomendada) o en la misma pestaña.

   Consulte [Trabajar con selectores](/help/assets/working-with-selectors.md) para obtener más información.

   * Seleccione **[!UICONTROL Fragmento de experiencia]**.

      * Si es cliente de Sitios Experience Manager, seleccione el icono de búsqueda (lupa) para abrir la página Fragmento de experiencias . Seleccione el fragmento de experiencia que desee utilizar y, a continuación, seleccione **[!UICONTROL Seleccionar]** en la esquina superior derecha de la página para que pueda volver a la página de administración de puntos interactivos.
Consulte [Fragmentos de experiencias](/help/sites-authoring/experience-fragments.md).

      * Especifique la anchura y la altura del fragmento de experiencia tal como desea que aparezca en el banner.

         >[!NOTE]
         Las herramientas de uso compartido de medios sociales en Imagen interactiva no son compatibles cuando se incrusta el visor en un fragmento de experiencia. Para solucionar este problema, puede utilizar o crear ajustes preestablecidos de visualizador que no tengan herramientas de uso compartido en redes sociales. Estos ajustes preestablecidos de visor permiten incrustarlos correctamente en fragmentos de experiencias.



1. Seleccione **[!UICONTROL Guardar]** para guardar el trabajo y volver a la página Examinar.
1. Publique la imagen interactiva. La publicación permite entregar el banner a través de la nube y también genera código incrustado si necesita integrarlo con un sitio web de terceros.

   Consulte [Publicar recursos](/help/assets/manage-assets.md#publishing-assets).

   Después de agregar zonas interactivas y publicar la imagen interactiva, ya está listo para agregarla al sitio web existente.

   Consulte [Integrar una imagen interactiva con su sitio web](#integrating-an-interactive-image-with-your-website).

   >[!NOTE]
   Si edita imágenes interactivas con zonas interactivas y recorta la imagen, se eliminarán las zonas interactivas.

### (Opcional) Previsualizar imágenes interactivas {#optional-previewing-interactive-images}

Puede utilizar Vista previa para ver una representación del aspecto que tiene la imagen interactiva para los clientes y para probar las zonas interactivas de la imagen para asegurarse de que se comportan del modo esperado.

Cuando esté satisfecho con la imagen interactiva, puede publicarla.
Consulte [Incrustar el visualizador de imágenes o vídeos en una página web](/help/assets/embed-code.md).
Consulte [Vincular URL a su aplicación web](/help/assets/linking-urls-to-yourwebapplication.md). El método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a páginas de sitios Experience Manager.
Consulte [Agregar recursos de Dynamic Media a páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).

**Para previsualizar imágenes interactivas:**

1. En la vista Recursos, desplácese a la imagen interactiva existente que haya creado y seleccione para abrirla en Vista previa.
1. Cerca de la esquina superior izquierda de la página Vista previa, en la lista desplegable Contenido, seleccione **[!UICONTROL Visualizadores]**.
1. En la lista Visualizadores, seleccione **[!UICONTROL Shoppable_Banner]** o el nombre del ajuste preestablecido del visualizador de imágenes interactivo que ha creado.
1. Seleccione las zonas interactivas de la imagen si desea probar las acciones asociadas.

## Publicar recursos de imagen interactivos {#publishing-interactive-image-assets}

Consulte [Publicar recursos](/help/assets/publishing-dynamicmedia-assets.md) para obtener más información sobre cómo publicar recursos de imagen interactivos.

## Integración de una imagen interactiva con el sitio web {#integrating-an-interactive-image-with-your-website}

Después de cargar una imagen de banner, agregar zonas interactivas a la imagen y publicar la imagen interactiva, ya está listo para agregarla a la página del sitio web.

Si es cliente de Sitios Experience Manager, puede agregar la imagen interactiva arrastrando el componente de Medios interactivos a su página. Consulte [Agregar recursos de Dynamic Media a páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).

Si es cliente independiente de Recursos Experience Manager, puede agregar manualmente la imagen interactiva al sitio web tal como se describe en esta sección.

1. Copie el código incrustado de la imagen interactiva publicada.
Consulte [Incrustar el visualizador de imágenes o vídeos en una página web](/help/assets/embed-code.md).

1. Agregue el código incrustado copiado en la ubicación deseada dentro de la página web.
El código incrustado copiado está configurado para un entorno interactivo, de modo que se ajusta automáticamente al área asignada.

**Ejemplo**

Ejemplo de uso del sitio web de demostración:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)

Observe que la imagen de los tres machos es una etiqueta estática `IMG`:

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

La integración es tan sencilla como eliminar la etiqueta `IMG` y sustituirla por el código incrustado copiado de los recursos de Experience Manager. Puede ver el resultado en la siguiente URL que muestra la imagen interactiva de ventas en la página con tres puntos interactivos de círculo:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html)

>[!NOTE]
En este punto, las zonas interactivas de la imagen interactiva de la tienda del sitio web de la demostración solo tienen fines de visualización; aún no están integrados con la vista rápida existente.

Para aplicar un &quot;recorte&quot; a una imagen interactiva de ventas para un entorno interactivo, puede incluir el atributo de configuración de imagen interactiva `ZoomView.iscommand` a la ruta. El componente `ZoomView` se llama y `iscommand` es el comando de servidor de imágenes &quot;recortar&quot; que se aplica.

Consulte el atributo de configuración [ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html).

Consulte el comando [recortar](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html) servidor de imágenes.

Ya está listo para integrar la imagen interactiva con una vista rápida existente en su sitio web.

## Integrar una imagen interactiva con una vista rápida existente {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
Esta tarea solo se aplica si es cliente independiente de Recursos Experience Manager.

El último paso de este proceso es integrar la imagen interactiva con una implementación de vista rápida existente en el sitio web. No existe una solución para la integración que funcione en todos los casos. Cada implementación de QuickView es única y se necesita un enfoque específico. Probablemente implique la asistencia de una persona de TI de front-end.

La implementación de vista rápida existente representa normalmente una cadena de acciones interrelacionadas que se producen en la página web en el siguiente orden:

1. Un usuario déclencheur un elemento en la interfaz de usuario del sitio web.
1. El código del front-end obtiene una URL de vista rápida basada en el elemento de la interfaz de usuario que se activó en el paso 1.
1. El código front-end envía una solicitud de Ajax utilizando la URL obtenida en el paso 2.
1. La lógica back-end devuelve los datos o el contenido de vista rápida correspondientes al código front-end.
1. El código front-end carga los datos o el contenido de Quickview.
1. De forma opcional, el código front-end convierte los datos de Quickview cargados en una representación HTML.
1. El código front-end muestra un cuadro de diálogo modal o panel y representa el contenido HTML en la pantalla para el usuario final.

Estas llamadas no representan llamadas de API públicas independientes a las que la lógica de página web puede llamar desde un paso arbitrario. En su lugar, se trata de una llamada encadenada en la que cada paso siguiente se oculta en la última fase (llamada de retorno) del paso anterior.

Al mismo tiempo que la imagen interactiva de ventas sustituye al paso 1 y al paso 2 parcialmente, cuando un usuario selecciona un punto interactivo dentro de la imagen de ventas, el visor gestiona dicha interacción del usuario. El visor devuelve un evento a la página web que contiene todos los datos de zona interactiva añadidos anteriormente a Recursos de Experience Manager.

En un controlador de eventos de este tipo, el código front-end hace lo siguiente:

* Escucha un evento emitido por la imagen interactiva de ventas.
* Crea una URL de vista rápida basada en los datos de zona interactiva.
* Déclencheur el proceso de carga de la vista rápida desde el servidor y de renderización en la pantalla para su visualización.

El código incrustado devuelto por Recursos de Experience Manager ya tiene un controlador de eventos listo para usar que se comenta, como se ve en el siguiente fragmento de código resaltado:

```xml
        var s7interactiveimageviewer = new s7viewers.InteractiveImage({
            "containerId" : "s7interactiveimage_div",
            "params" : {
                "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
                "contenturl" : "https://aodmarketingna.assetsadobe.com/",
                "config" : "/etc/dam/presets/viewer/Shoppable_Media",
                "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
        })
        /* // Example of interactive image event for Quickview.
             s7interactiveimageviewer.setHandlers({
                "quickViewActivate": function(inData) {
                    var sku=inData.sku; //SKU for product ID
                    //To pass other parameter from the hotspot, you will need to add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //Please refer to your Quickviewer plugin for the Quickview call
                 },
             });
        */
        s7interactiveimageviewer.init();
```

Por lo tanto, solo es necesario descomentar el código y reemplazar el cuerpo del controlador ficticio con el código específico de la página web en particular.

El proceso de construcción de la URL de vista rápida es opuesto al proceso utilizado para identificar las variables de zona interactiva incluidas anteriormente.

Consulte [Identificar variables de puntos interactivos](#optional-identifying-hotspot-variables).

En los ejemplos anteriores de URL de vista rápida, se puede ver en los ejemplos siguientes cómo se construye la URL de vista rápida en cada caso:

<table>
 <tbody>
  <tr>
   <td><p>SKU único, que se encuentra en la cadena de consulta</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>SKU único, que se encuentra en la ruta de URL</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>SKU e ID de categoría en la cadena de consulta</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

El último paso para almacenar en déclencheur la URL de vista rápida y activar el panel de vista rápida requiere, muy probablemente, la asistencia de una persona de TI de front-end de su departamento de TI. Tienen conocimientos para saber mejor cómo realizar un déclencheur exacto de la implementación de QuickView desde el paso adecuado, teniendo una URL de Quickview lista para usar.

Puede ver cómo se aplican estos pasos al sitio web de demostración para integrar completamente una imagen interactiva de ventas con el código de vista rápida. Anteriormente, la estructura de la URL de vista rápida se identificaba como la siguiente:

```xml
/datafeed/$categoryId$-$SKU$.json
```

Para reconstruir esta URL dentro del controlador `quickViewActivate` , puede utilizar los campos `categoryId` y `SKU` disponibles en el objeto `inData` que el código del visor pasa al controlador:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

El sitio web de demostración activa el cuadro de diálogo Vista rápida utilizando una llamada de función `loadQuickView()` simple. Esta función toma solo un argumento, que es la URL de datos de vista rápida. Como tal, el último paso para integrar la imagen interactiva de ventas es agregar la siguiente línea de código al controlador `quickViewActivate`:

```xml
loadQuickView(quickViewUrl);
```

El siguiente es el código fuente completo:

```xml
 var s7interactiveimageviewer = new s7viewers.InteractiveImage({
  "containerId" : "s7interactiveimage_div",
  "params" : {
   "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
   "contenturl" : "https://aodmarketingna.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Media",
   "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
 })
   s7interactiveimageviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku;
     var categoryId=inData.categoryId;
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   });
 s7interactiveimageviewer.init();
```

El sitio web de demostración final con la imagen interactiva completamente integrada tiene el siguiente aspecto:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html)

## Utilice la vista rápida para crear ventanas emergentes personalizadas {#using-quickviews-to-create-custom-pop-ups}

Consulte [Creación de ventanas emergentes personalizadas mediante Quickview](/help/assets/custom-pop-ups.md).
