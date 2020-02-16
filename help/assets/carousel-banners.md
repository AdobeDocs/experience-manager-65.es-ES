---
title: Pancartas de carrusel
description: Aprenda a trabajar con letreros de carrusel en Dynamic Media
uuid: 73684a08-d84d-4665-ab89-3a1bf88ac5dd
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e26c7f7f-bdd7-421a-8614-ba48abf381d2
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Pancartas de carrusel{#carousel-banners}

Los letreros de carrusel permiten a los especialistas en marketing impulsar la conversión creando fácilmente contenido promocional interactivo rotatorio y entregándolo en cualquier pantalla.

La creación y modificación de contenido destacado en las pancartas promocionales puede llevar mucho tiempo, lo que limita la capacidad de publicar contenido nuevo rápidamente o de hacerlo más específico. Los letreros de carrusel le permiten crear o modificar rápidamente letreros rotativos, agregar interactividad, como puntos interactivos vinculados a los detalles del producto o recursos relacionados, y distribuirlos en cualquier pantalla, lo que le permite comercializar más rápidamente contenido promocional.

Los letreros de carrusel se designan mediante un letrero con la palabra **[!UICONTROL CAROUSELSET]**:

![chlimage_1-438](assets/chlimage_1-438.png)

En su sitio web, una pancarta de carrusel puede tener el siguiente aspecto:

![chlimage_1-439](assets/chlimage_1-439.png)

Aquí puede navegar por las imágenes (haciendo clic en los números). Además, las diapositivas giran automáticamente en función del intervalo de tiempo que se pueda personalizar. Las imágenes agregadas en la pancarta de carrusel admiten zonas interactivas y mapas de imagen, donde los usuarios pueden tocar o ir a un hipervínculo o acceder a una ventana de vista rápida.

En este ejemplo, un usuario tocó o hizo clic en un mapa de imagen y accedió a la ventana de vista rápida para obtener guantes:

![chlimage_1-440](assets/chlimage_1-440.png)

## Ver cómo se crean los letreros de carrusel {#watch-how-carousel-banners-are-created}

Vea un tutorial de 10 minutos y 33 segundos sobre [cómo se crean](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&emailurl=https://s7d5.scene7.com/s7/emailFriend&serverUrl=https://s7d5.scene7.com/is/image/&config=Scene7SharedAssets/Universal_HTML5_Video_social&contenturl=https://s7d5.scene7.com/skins/&asset=S7tutorials/InteractiveCarouselBanner)los letreros de carrusel. También aprenderá a previsualizar, editar y distribuir letreros de carrusel.

>[!NOTE]
>
>Los usuarios no administrativos deben agregarse al grupo de usuarios **[!UICONTROL de]** presas para poder crear o editar letreros de carrusel. Si tiene problemas para crear o editar, póngase en contacto con el administrador del sistema, el cual puede agregarle al grupo de usuarios **[!UICONTROL de ]**presas.

## Inicio rápido: Pancartas de carrusel {#quick-start-carousel-banners}

Para ayudarle a ponerse en marcha rápidamente:

1. [Identifique las variables](#identifying-hotspot-and-image-map-variables) de puntos interactivos y mapas de imagen (solo para clientes que utilizan Recursos AEM + Medios dinámicos)

   Comience identificando las variables dinámicas que utiliza la implementación de vista rápida existente para poder introducir los puntos interactivos y los datos de mapas de imagen correctamente durante el proceso de creación de letreros de carrusel en Recursos AEM.

   >[!NOTE]
   >
   >Si es cliente de AEM Sites o de comercio electrónico, puede utilizar la función integrada para navegar a las páginas de productos y buscar el SKU existente en el catálogo de productos. No es necesario introducir manualmente variables de zona interactiva o mapa de imagen. Consulte la información sobre la [configuración del comercio electrónico](/help/sites-administering/generic.md).
   >
   >
   >Si es cliente de Recursos AEM y Dynamic Media, introducirá manualmente los datos de las zonas interactivas y los mapas de imagen y, a continuación, integrará la URL publicada o el código incrustado en su sistema de gestión de contenido de terceros.

1. Opcional: [Cree un ajuste preestablecido](/help/assets/managing-viewer-presets.md)de visor de conjuntos de carrusel, según sea necesario.

   Si es un administrador, puede personalizar el comportamiento y el aspecto del carrusel creando su propio ajuste preestablecido de visor de carrusel. La principal ventaja es que puede volver a utilizar este ajuste preestablecido de visor personalizado para varios carruseles. Sin embargo, los usuarios también tienen la opción de personalizar el comportamiento y el aspecto del carrusel directamente durante la creación del carrusel. Este es el método preferido cuando desea un diseño muy específico para un determinado carrusel.

1. [Cargue una pancarta](#uploading-image-banners)de imagen.

   Cargue letreros de imagen que desee convertir en interactivos.

1. [Crear un conjunto](#creating-carousel-sets)de carrusel.

   En Conjuntos de carruseles, los usuarios navegan por las imágenes de pancarta y tocan zonas interactivas o mapas de imagen para acceder al contenido relevante.

   Para crear un conjunto de carrusel en Recursos, toque **[!UICONTROL Crear]** y, a continuación, seleccione Conjuntos de **[!UICONTROL carrusel]**. Agregue recursos a las diapositivas y toque **[!UICONTROL Guardar]**. También puede editar el aspecto y el comportamiento del carrusel directamente en el editor.

1. [Agregue zonas interactivas o mapas de imagen a una pancarta de imagen.](#adding-hotspots-or-image-maps-to-an-image-banner)

   Agregue una o varias zonas interactivas o mapas de imagen a una pancarta de imagen y asocie cada una de ellas a una acción como un vínculo, una vista rápida o un fragmento de experiencia. Después de agregar zonas interactivas o mapas de imagen, esta tarea se finaliza publicando el conjunto de carrusel. La publicación crea el código incrustado que puede utilizar para copiar y aplicar a la página de aterrizaje del sitio web.

   Consulte [(Opcional) Vista previa de letreros](#optional-previewing-carousel-banners) de carrusel: Opcional. Si lo desea, puede ver una representación del conjunto de carrusel y probar su interactividad.

1. [Publicar letreros de carrusel.](#publishing-carousel-banners)

   Puede publicar un conjunto de carrusel como lo haría con cualquier recurso. En Recursos, vaya al conjunto de carrusel, selecciónelo y toque **[!UICONTROL Publicar]**. Al publicar un conjunto de carrusel, se activa la URL y la cadena Incrustar.

1. Realice una de las acciones siguientes:

   * [Agregar una pancarta de carrusel a la página del sitio web
      ](#adding-a-carousel-banner-to-your-website-page)Puede agregar la dirección URL de la pancarta de carrusel o el código incrustado que ha copiado en la página del sitio web.

      * [Integre la pancarta de carrusel con una vista rápida](#integrating-the-carousel-banner-with-an-existing-quickview)existente. Si utiliza un sistema de administración de contenido web de terceros, deberá integrar la nueva pancarta de carrusel con la implementación de vista rápida existente en su sitio web.
   * [Adición de una pancarta de carrusel a su sitio web en AEM
      ](/help/assets/adding-dynamic-media-assets-to-pages.md)Si es cliente de AEM Sites, puede añadir el conjunto de carrusel directamente a la página en AEM mediante el componente de medios interactivos.


Si necesita editar conjuntos de carrusel, consulte [Edición de conjuntos de carrusel.](#editing-carousel-sets) Además, puede ver y editar las propiedades [del conjunto de](https://helpx.adobe.com/experience-manager/6-5/help/assets/managing-assets-touch-ui.md#editingproperties)carrusel.

## Identificación de variables de puntos interactivos y mapas de imagen {#identifying-hotspot-and-image-map-variables}

Comience identificando las variables dinámicas que utiliza la implementación de vista rápida existente para poder introducir puntos interactivos o datos de mapa de imagen correctamente durante el proceso de creación de conjuntos de carrusel en Recursos AEM.

Al añadir zonas interactivas o mapas de imagen a una imagen de pancarta en Recursos AEM, debe asignar un SKU y variables adicionales opcionales a cada zona interactiva o mapa de imagen. Estas variables se utilizan más adelante para hacer coincidir puntos interactivos o mapas de imagen con el contenido de vista rápida.

>[!NOTE]
>
>Si es cliente de AEM Sites o de comercio electrónico de AEM, omita este paso. No es necesario identificar manualmente las variables de puntos interactivos o mapas de imagen; puede utilizar la integración con comercio electrónico para la integración de productos. Consulte la información sobre la [configuración del comercio electrónico](/help/sites-administering/generic.md). Además, puede utilizar el componente interactivo y agregarlo a su página web.
>
>Si es cliente de Recursos AEM o Medios, publique la URL o el código incrustado y, a continuación, integre el sistema de gestión de contenido de terceros e identifique manualmente las zonas interactivas y los mapas de imagen.

Es importante identificar correctamente el número y el tipo de variables que se asociarán con los datos de puntos interactivos o mapas de imagen. Cada zona interactiva o mapa de imagen que se añada a una imagen de pancarta debe contener suficiente información para identificar sin ambigüedades el producto en el sistema back-end existente. Al mismo tiempo, cada zona interactiva o mapa de imagen no debe incluir más datos de los necesarios. El motivo es que esto haría que el proceso de entrada de datos fuera demasiado complejo y la administración de puntos interactivos o mapas de imagen en curso fuera más propensa a errores.

Existen diferentes maneras de identificar un conjunto de variables que se utilizarán para los datos de puntos interactivos o mapas de imagen.

A veces puede bastar con consultar con los especialistas de TI responsables de la implementación de vista rápida existente, ya que es probable que sepan cuál es el conjunto mínimo de datos necesario para identificar una vista rápida en el sistema. Sin embargo, en la mayoría de los casos también es posible simplemente analizar el comportamiento existente del código front-end.

La mayoría de las implementaciones de vista rápida utilizan el siguiente paradigma:

* El usuario activa un elemento de interfaz de usuario en el sitio web. Por ejemplo, al tocar un botón de vista **[!UICONTROL rápida]** .
* El sitio web envía una solicitud de Ajax al servidor para cargar los datos de vista rápida o el contenido, si es necesario.
* Los datos de vista rápida se traducen al contenido como preparación para su procesamiento en la página web.
* Por último, el código front-end procesa visualmente dicho contenido en la pantalla.

El método consiste en visitar diferentes áreas del sitio web existente en las que se implementa la función de vista rápida, activar la vista rápida y capturar la URL de Ajax enviada por la página web para cargar los datos de vista rápida o el contenido.

Normalmente no es necesario que utilice ninguna herramienta de depuración especializada. Los navegadores web modernos cuentan con inspectores web que realizan un trabajo adecuado. Estos son algunos ejemplos de exploradores Web que incluyen inspectores Web:

* Para ver todas las solicitudes HTTP salientes en Google Chrome, pulse F12 (Windows) o Comando-Opción-I (Mac) para abrir el panel Herramientas del desarrollador y, a continuación, toque la ficha Red.
* En Firefox, puede activar el complemento Firebug pulsando F12 (Windows) o Comando-Opción-I (Mac) y utilizar su ficha Red, o puede utilizar la herramienta Inspector integrada y su ficha Red.

Cuando la supervisión de red está activada en el explorador, active la vista rápida en la página.

Encuentre ahora la URL de Ajax de vista rápida en el registro de red y copie la URL grabada para análisis futuros. En la mayoría de los casos, cuando se activa la vista rápida, se envían al servidor numerosas solicitudes. Normalmente, la URL de Ajax de vista rápida es una de las primeras de la lista. Tiene una ruta o una porción de cadena de consulta compleja y su tipo MIME de respuesta es `text/html`, `text/xml`o `text/javascript`.

Durante este proceso es importante visitar diferentes áreas del sitio web, con diferentes tipos y categorías de productos. El motivo es que las direcciones URL de vista rápida pueden tener partes que son comunes para una categoría de sitio web determinada, pero que solo cambian si se visita un área diferente del sitio web.

En el caso más sencillo, la única parte variable de la URL de vista rápida es el SKU del producto. En este caso, el valor de SKU es la única pieza de datos que necesita para agregar zonas interactivas o mapas de imagen a la imagen de la pancarta.

Sin embargo, en casos complejos, la dirección URL de vista rápida tiene distintos elementos además del SKU, como ID de categoría, código de color, código de tamaño, etc. En estos casos, cada elemento es una variable independiente en la definición de datos de puntos interactivos o mapas de imagen en la función de pancarta de carrusel.

Considere los siguientes ejemplos de direcciones URL de vista rápida y las variables de mapa de imagen o zona interactiva resultantes:

<table>
 <tbody>
  <tr>
   <td>SKU único, que se encuentra en la cadena de consulta.</td>
   <td><p>Las direcciones URL de vista rápida grabadas incluyen lo siguiente:</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>La única parte variable de la dirección URL es el valor del parámetro de cadena de <code>productId=</code> consulta y es claramente un valor de SKU. Por lo tanto, nuestras zonas interactivas o mapas de imagen solo necesitan campos SKU rellenados con valores como <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>SKU único, que se encuentra en la ruta de URL.</td>
   <td><p>Las direcciones URL de vista rápida grabadas incluyen lo siguiente:</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte variable se encuentra en la última parte de la ruta y se convierte en el valor de SKU de las zonas interactivas/mapas de imagen:<strong><code>6422350843</code>, <code>1607745002,</code></strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>SKU y ID de categoría en la cadena de consulta.</td>
   <td><p>Las direcciones URL de vista rápida grabadas incluyen lo siguiente:</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>En este caso, hay dos partes diferentes en la dirección URL. El SKU se almacena en el parámetro <code>prodId</code> y el ID de categoría se almacena en el <code>category=</code>parámetro.</p> <p>Por lo tanto, las definiciones de zona interactiva/mapa de imagen son pares. Es decir, un valor de SKU y una variable adicional llamada <code>categoryId</code>. Los pares resultantes son los siguientes:</p>
    <ul>
     <li><p>El SKU es <strong><code>305466</code></strong> y <code>categoryId</code> es <code>1100004</code>.</p> </li>
     <li><p>El SKU es <strong><code>310181</code></strong> y <code>categoryId</code> es <strong><code>1100004</code></strong>.</p> </li>
     <li><p>El SKU es <strong><code>308706</code></strong> y <code>categoryId</code> es <strong><code>1740148</code></strong>.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Carga de letreros de imagen {#uploading-image-banners}

Si ya ha cargado las imágenes que desea utilizar, avance al paso siguiente, [Creación de conjuntos](#creating-carousel-sets)de carrusel. Tenga en cuenta que las imágenes utilizadas en el carrusel deben cargarse después de habilitar Dynamic Media.

Para cargar letreros de imagen, consulte [Carga de recursos](/help/assets/managing-assets-touch-ui.md).

## Creación de conjuntos de carruseles {#creating-carousel-sets}

>[!NOTE]
>
>Los usuarios no administrativos deben agregarse al grupo de usuarios **[!UICONTROL de]** presas para poder crear o editar letreros de carrusel. Si tiene problemas para crear o editar, póngase en contacto con el administrador del sistema, el cual puede agregarle al grupo de usuarios **[!UICONTROL de]** presas.

**Creación de un conjunto de carruseles**

1. En Recursos, vaya a la carpeta en la que desea crear el conjunto de carrusel y toque **[!UICONTROL Crear > Conjunto]** de carrusel.
1. En la página Editor de letreros de carrusel, toque **[!UICONTROL Tocar para abrir el Selector]** de recursos para seleccionar la imagen de la primera diapositiva.

   En la página Editor de letreros de carrusel, realice una de las acciones siguientes:

   * Cerca de la esquina superior izquierda de la página, toque el icono **[!UICONTROL Agregar diapositiva]** .

   * Cerca del centro de la página, toque **[!UICONTROL Tocar para abrir el Selector]** de recursos.
   Toque para seleccionar los recursos que desea incluir en el conjunto de carrusel. Los recursos seleccionados tienen un icono de marca de verificación sobre ellos. Cuando haya terminado, toque **[!UICONTROL Seleccionar** cuando esté cerca de la esquina superior derecha de la página.

   Con el Selector de recursos, puede buscar recursos escribiendo una palabra clave y tocando o haciendo clic en **[!UICONTROL Retorno]**. También puede aplicar filtros para restringir los resultados de búsqueda. Puede filtrar por ruta, colección, tipo de archivo y etiqueta. Seleccione el filtro y, a continuación, toque el icono **[!UICONTROL Filtro]** en la barra de herramientas. Para cambiar la vista, toque el icono Ver y seleccione Vista **[!UICONTROL de]** columna, Vista **[!UICONTROL de]** tarjeta o Vista **[!UICONTROL de]** lista.

   Consulte [Uso de selectores](/help/assets/working-with-selectors.md) para obtener más información.

1. Continúe agregando diapositivas hasta que haya agregado todas las imágenes que desee rotar en el conjunto de carrusel.
1. (Opcional) Realice cualquiera de las siguientes acciones:

   * Si es necesario, arrastre las diapositivas para reordenar las imágenes en la lista de conjuntos.
   * Para eliminar una imagen, selecciónela y, a continuación, toque **[!UICONTROL Eliminar diapositiva]** en la barra de herramientas.

   * Para aplicar un ajuste preestablecido, cerca de la esquina superior derecha de la página, toque la lista desplegable de ajustes preestablecidos y, a continuación, seleccione un ajuste preestablecido para aplicarlo al conjunto a la vez.
   Para eliminar una diapositiva, toque o haga clic en la diapositiva y toque o haga clic en **[!UICONTROL Eliminar diapositiva]** en la barra de herramientas. Para mover una diapositiva, toque el icono del redirector y manténgalo presionado y desplácese a la ubicación deseada.

1. Después de añadir las imágenes en las diapositivas, puede añadir un punto interactivo, un mapa de imágenes o ambos a la imagen. Consulte [Adición de zonas interactivas o mapas](#adding-hotspots-or-image-maps-to-an-image-banner)de imagen.
1. Puede cambiar el diseño visual y el comportamiento de los conjuntos de carrusel tocando o haciendo clic en las fichas Comportamiento y Aspecto y haciendo ajustes en el aspecto del letrero carrusel o en el comportamiento de componentes específicos. Consulte [Gestión de ajustes preestablecidos](/help/assets/viewer-presets.md) de visor para obtener más información sobre cómo utilizar el editor de visor.

   >[!NOTE]
   >
   >En el caso de los letreros de carrusel, puede que lo siguiente sea lo que desee ajustar:
   >    * Duración que muestra una imagen. De forma predeterminada, cada imagen se muestra durante 9 segundos.
   >    * Animación. De forma predeterminada, cada transición de diapositiva es una atenuación. Puede cambiarlo a una transición de diapositivas.
   >    * Estilo de los botones. Los usuarios pueden rotar los letreros tocando cada punto o número. Puede cambiar dónde aparecen los botones del indicador de conjunto (y si son numéricos o de un estilo de puntos) y su tamaño.
   >    * Cambie el estilo de resaltado de un mapa de imagen o el icono utilizado para las zonas interactivas.
   >    * Antes de editar un ajuste preestablecido de visor, elija el estilo en el que desea basar el ajuste preestablecido. Si no lo hace, cuando comience a editar el ajuste preestablecido de visor, perderá todos los cambios si decide cambiar a otro ajuste preestablecido
   >
   >
   >Consulte Consideraciones [especiales para letreros](/help/assets/viewer-presets.md#specialconsiderationsforcreatingacarouselbannerviewerpreset) de carrusel para obtener instrucciones detalladas y más información sobre el editor del visor.

   También puede obtener una vista previa del aspecto que tendrá la pancarta de carrusel. Consulte [(Opcional) Vista previa de letreros](#optional-previewing-carousel-banners)de carrusel.

1. Toque **[!UICONTROL Guardar]** cuando termine.

## Adición de zonas interactivas o mapas de imagen a un letrero de imagen {#adding-hotspots-or-image-maps-to-an-image-banner}

Puede agregar zonas interactivas o mapas de imagen a un letrero mediante el editor de conjuntos de carrusel.

Al agregar zonas interactivas o mapas de imagen, puede definirlos como una visualización emergente de vista rápida, como un hipervínculo o como un fragmento de experiencia.

Consulte Fragmento [de experiencias](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
>
>Tenga en cuenta que las herramientas de uso compartido en medios sociales de la pancarta de carrusel no son compatibles cuando incrusta el visor en un fragmento de experiencia.
Para solucionar este problema, puede utilizar o crear ajustes preestablecidos de visor que no tengan herramientas de uso compartido en medios sociales. Estos ajustes preestablecidos de visor permiten incrustarlos correctamente en fragmentos de experiencia.

Cuando agregue zonas interactivas o mapas de imagen a una imagen, recuerde guardar el trabajo. Las opciones Deshacer y Rehacer, cerca de la esquina superior derecha de la página, son compatibles durante la sesión de creación/edición actual.

Cuando termine de crear la pancarta de carrusel, puede utilizar de forma opcional Vista previa para ver una representación de cómo aparecerá la pancarta de carrusel para los clientes.

Consulte [(Opcional) Vista previa de letreros de carrusel.](#optional-previewing-carousel-banners)

>[!NOTE]
>
>Cuando se agregan zonas interactivas a una imagen en una imagen [interactiva](/help/assets/interactive-images.md) o una pancarta de carrusel, la información de puntos interactivos se almacena en la misma ubicación de metadatos, en relación con la ubicación y el mdashindependientemente de si se trata de una imagen interactiva o de una pancarta de carrusel. Esta funcionalidad significa que puede reutilizar fácilmente la misma imagen (junto con los datos de puntos interactivos definidos) en cualquier visor.

>Sin embargo, tenga en cuenta que los letreros de carrusel admiten mapas de imagen en imágenes que también pueden contener zonas interactivas; una imagen interactiva no. Tenga esto en cuenta si desea crear una imagen interactiva o una pancarta de carrusel que utilice la misma imagen. Puede que desee crear imágenes interactivas y letreros de carrusel con copias independientes de la misma imagen.

>[!NOTE]
Si está editando imágenes interactivas con zonas interactivas y recortando la imagen, las zonas interactivas se eliminan.

Consulte también [Adición de mapas de imagen](/help/assets/image-maps.md).

**Para agregar zonas interactivas o mapas de imagen a un letrero de imagen**

1. En Recursos, desplácese hasta el conjunto de carrusel que desee hacer interactivo.
1. Seleccione el conjunto de carrusel y toque **[!UICONTROL Editar]**. Se abre el Editor del visor de carrusel.
1. Seleccione la diapositiva que desee hacer interactiva.
1. Cerca de la esquina superior izquierda de la página, toque **[!UICONTROL Zona interactiva]** o Mapa **[!UICONTROL de imagen]**.
1. Realice una de las acciones siguientes:

   * Para zonas interactivas: En la imagen, toque una ubicación en la que desee que aparezca el punto interactivo.
   * Para mapas de imagen: En la imagen, haga clic en y arrastre desde la parte superior izquierda a la parte inferior derecha para crear el área del mapa de imagen. Puede ajustar el tamaño del mapa de imagen arrastrando las esquinas.
   Si es necesario, arrastre el punto interactivo o el mapa de imagen a una nueva ubicación. Agregue zonas interactivas o mapas de imagen adicionales según sea necesario.

   Para eliminar una zona interactiva o un mapa de imagen, toque la ficha **[!UICONTROL Acciones]** . En el encabezado **[!UICONTROL Mapas y zonas interactivas]** , en el menú desplegable Tipo **** seleccionado, seleccione el nombre del punto interactivo o del mapa de imagen que desea eliminar. Toque el icono **[!UICONTROL Papelera]** situado junto al menú y, a continuación, toque **[!UICONTROL Eliminar]**.

1. En el campo de texto Nombre, escriba el nombre del punto interactivo o del mapa de imagen. Este nombre también aparece en la lista desplegable **[!UICONTROL Mapas y puntos interactivos]** . Proporcionar un nombre facilita la identificación del punto interactivo o mapa de imagen si decide realizar cambios en él en el futuro.
1. Realice una de las siguientes acciones en la ficha **[!UICONTROL Acciones]** :

   * Toque **[!UICONTROL Vista]** rápida.

      * Si es cliente de Sitios AEM y comercio electrónico, toque el icono Selector de producto (lupa) para abrir la página Seleccionar producto. Toque el producto que desee utilizar y, a continuación, toque la marca de verificación situada en la esquina superior derecha de la página para volver al Editor de letreros de carrusel.
      * Si no es cliente de AEM Sites o de comercio electrónico

         * Consulte [Identificación de las variables](#identifying-hotspot-and-image-map-variables) de puntos interactivos tal como desee definir estas variables.
         * A continuación, introduzca manualmente el valor de SKU. En el campo de texto Valor de SKU, escriba el SKU del producto (Unidad de almacenamiento de información), que es un identificador único para cada producto o servicio distinto que ofrezca. El valor de SKU introducido rellena automáticamente la parte variable de la plantilla de vista rápida, de modo que el sistema sepa asociar la zona interactiva tocada con una vista rápida de SKU concreta.
         * (Opcional) Si hay otras variables dentro de la vista rápida que debe utilizar para identificar un producto, toque **[!UICONTROL Agregar variable]** genérica. En el campo de texto, especifique una variable adicional. Por ejemplo, category=Mens es una variable agregada.

         * Consulte [Uso de selectores](/help/assets/working-with-selectors.md) para obtener más información.
   * Toque **[!UICONTROL Hipervínculo]**.

      * Si es cliente de AEM Sites, toque el icono (carpeta) Selector de sitio para navegar a una URL.
         >[!NOTE]
         El método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, en particular vínculos a páginas de AEM Sites.

      * Si es un cliente independiente, en el campo de texto HREF, especifique la ruta de URL completa a una página web vinculada.
   Asegúrese de especificar si desea abrir el vínculo en una nueva ficha del explorador (opción predeterminada recomendada) o en la misma ficha.

   Consulte [Uso de selectores](/help/assets/working-with-selectors.md) para obtener más información.

   * Puntee en Fragmento **[!UICONTROL de experiencias]**.

      * Si es cliente de AEM Sites, toque el icono de búsqueda (lupa) para abrir la página Fragmento de experiencias. Toque o haga clic en el fragmento de experiencias que desee utilizar y, a continuación, toque Seleccionar en la esquina superior derecha de la página para volver a la página de administración de puntos interactivos.
Consulte Fragmentos [de experiencias](/help/sites-authoring/experience-fragments.md).

      * Especifique la anchura y la altura del fragmento de experiencias tal como aparecerán en el letrero.

         >[!NOTE]
         Tenga en cuenta que las herramientas de uso compartido en medios sociales de la pancarta de carrusel no son compatibles cuando incrusta el visor en un fragmento de experiencia.
Para solucionar este problema, puede utilizar o crear ajustes preestablecidos de visor que no tengan herramientas de uso compartido en medios sociales. Estos ajustes preestablecidos de visor permiten incrustarlos correctamente en fragmentos de experiencia.
   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   También puede obtener una vista previa del aspecto que tendrá la pancarta de carrusel. Consulte [(Opcional) Vista previa de letreros](#optional-previewing-carousel-banners)de carrusel.

1. Toque **[!UICONTROL Guardar]**.
1. Publique el conjunto de carrusel. La publicación crea el código incrustado o la URL que puede utilizar en la página del sitio web. Si es cliente de AEM Sites, puede agregar el conjunto de carrusel directamente a su página web.

   Consulte [Publicación de recursos](/help/assets/publishing-dynamicmedia-assets.md).

   Consulte [Adición de un conjunto de carrusel a la página de aterrizaje del sitio web](#adding-a-carousel-banner-to-your-website-page)

## Edición de conjuntos de carruseles {#editing-carousel-sets}

>[!NOTE]
Los usuarios no administrativos deben agregarse al grupo de usuarios **[!UICONTROL de]** presas para poder crear o editar letreros de carrusel. Si tiene problemas para crear o editar, póngase en contacto con el administrador del sistema, el cual puede agregarle al grupo de usuarios **[!UICONTROL de]** presas.

Puede realizar diversas tareas de edición en conjuntos de carrusel, como las siguientes:

* Agregue diapositivas a un conjunto de carrusel. Consulte también [Uso de selectores](/help/assets/working-with-selectors.md).
* Vuelva a ordenar las diapositivas en el conjunto de carrusel.
* Eliminar recursos del conjunto de carrusel.
* Aplique un ajuste preestablecido de visor.
* Elimine el conjunto de carrusel.
* Agregue o edite zonas interactivas y mapas de imagen. Consulte también [Uso de selectores](/help/assets/working-with-selectors.md).

**Edición de un conjunto de carruseles**

1. Realice una de las siguientes acciones:

   * Pase el ratón sobre un recurso de conjunto de carrusel y, a continuación, toque **[!UICONTROL Editar]** (icono de lápiz).
   * Pase el ratón sobre un recurso de conjunto de carrusel, toque **[!UICONTROL Seleccionar]** (icono de marca de verificación) y, a continuación, toque **[!UICONTROL Editar]** en la barra de herramientas.

   * Puntee en un recurso de conjunto de carrusel y, a continuación, en la esquina superior izquierda de la página, toque **[!UICONTROL Editar]** (icono de lápiz).

1. Para editar el conjunto de carrusel, realice una de las siguientes acciones:

   * Para agregar una diapositiva, toque el icono **[!UICONTROL Agregar diapositiva]** y luego navegue hasta el recurso que desee agregar a esa diapositiva y toque o haga clic en la marca de verificación.
   * Para reordenar las diapositivas, arrastre una diapositiva a una nueva ubicación (seleccione el icono de reordenar para mover elementos).
   * Para agregar un punto interactivo o un mapa de imagen, haga clic en los iconos de zona interactiva o mapa de imagen y consulte [adición de zonas interactivas y mapas](#adding-hotspots-or-image-maps-to-an-image-banner)de imagen.
   * Para editar el aspecto o el comportamiento del conjunto de carrusel, toque la ficha **[!UICONTROL Aspecto]** o **[!UICONTROL Comportamiento]** y, a continuación, defina las opciones que desee.
   * Para editar zonas interactivas o mapas de imagen, en la diapositiva adecuada, seleccione un punto interactivo o mapa de imagen y realice los cambios necesarios en la ficha **[!UICONTROL Acciones]** .
   * Para eliminar una diapositiva, selecciónela y, a continuación, toque **[!UICONTROL Eliminar diapositiva]** en la barra de herramientas.
   * Para aplicar un ajuste preestablecido, cerca de la esquina superior derecha de la página, toque la lista desplegable **[!UICONTROL Ajuste preestablecido]** y, a continuación, seleccione un ajuste preestablecido de visor.
   * Para eliminar un conjunto de carrusel completo, vaya al conjunto de carrusel, selecciónelo y, a continuación, toque **[!UICONTROL Eliminar]**.
   >[!NOTE]
   Si está editando imágenes interactivas con zonas interactivas y recortando la imagen, las zonas interactivas se eliminan.

## (Opcional) Vista previa de letreros de carrusel {#optional-previewing-carousel-banners}

Puede utilizar Vista previa para ver el aspecto que tendrá la pancarta de carrusel para los clientes y probar las zonas interactivas y los mapas de imagen de las pancartas de carrusel para asegurarse de que se comportan de la forma esperada.

Cuando esté satisfecho con la pancarta de carrusel, puede publicarla.
Consulte [Incrustación del visor de imágenes o vídeos en una página](/help/assets/embed-code.md)Web.
See [Linking URLs to your web application](/help/assets/linking-urls-to-yourwebapplication.md). Tenga en cuenta que el método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, en particular vínculos a páginas de AEM Sites.
See [Adding Dynamic Media Assets to pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)

Puede obtener una vista previa de las pancartas de carrusel desde el Editor de carrusel (método preferido) o desde la lista **[!UICONTROL Visores]** .

**Para obtener una vista previa de las pancartas de carrusel**

1. En **[!UICONTROL Recursos]**, desplácese hasta una pancarta de carrusel existente que haya creado y toque para abrirla.
1. Toque **[!UICONTROL Editar]**.
1. En la lista de ajustes preestablecidos de visor situada en la esquina derecha de la barra de herramientas, seleccione un visor para previsualizar la pancarta de carrusel.

   ![experience_fragment-carouselbanner-viewerdropdown](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. Toque **Vista previa]**.
1. Toque las zonas interactivas o los mapas de imagen de la imagen para probar las acciones asociadas.

**Para obtener una vista previa de las pancartas de carrusel desde la lista Visores**

1. En **[!UICONTROL Recursos]**, desplácese hasta una pancarta de carrusel existente que haya creado y toque para abrirla.
1. Cerca de la esquina superior izquierda de la página Vista previa, haga clic en el icono Contenido.
1. En la lista **[!UICONTROL Visores]** del panel de la izquierda de la página, toque el nombre del ajuste preestablecido de visor de pancartas carrusel que desee utilizar.
1. Toque las zonas interactivas o los mapas de imagen de la imagen para probar las acciones asociadas.

## Publicación de letreros de carrusel {#publishing-carousel-banners}

Debe publicar el carrusel para utilizarlo. Al publicar un conjunto de carrusel se activan la URL y el código incrustado. También publica el carrusel en la nube de Dynamic Media, que está integrada con una CDN para una entrega escalable y con rendimiento.

>[!NOTE]
Si utiliza una imagen interactiva existente con zonas interactivas para la pancarta de carrusel, debe publicar la imagen interactiva por separado después de publicar la pancarta de carrusel.
Además, si modifica una imagen interactiva publicada previamente que está utilizando en una pancarta de carrusel, debe publicar la imagen interactiva antes de que esos cambios se reflejen en la pancarta de carrusel.

Consulte [Publicación de recursos](/help/assets/publishing-dynamicmedia-assets.md) de Dynamic Media para obtener información sobre cómo publicar letreros de carrusel.

## Adición de un letrero de carrusel a la página del sitio web {#adding-a-carousel-banner-to-your-website-page}

Una vez cargadas las imágenes de los letreros para crear un carrusel, añadidas zonas interactivas y/o mapas de imagen al letrero y publicado el conjunto de carrusel, ya estará listo para agregarlo a la página del sitio web existente.

>[!NOTE]
Si es cliente de AEM Sites, puede añadir la pancarta de carrusel directamente a la página arrastrando el componente de medios interactivos a la página. See [Adding Dynamic Media Assets to Pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)

Sin embargo, si es cliente independiente de Recursos AEM, puede agregar manualmente la pancarta de carrusel a la página de aterrizaje del sitio web, tal como se describe en esta sección.

1. Copie el código incrustado del conjunto de carrusel publicado.
Consulte [Incrustación del visor de imágenes o vídeos en una página](/help/assets/embed-code.md)Web.

1. Agregue el código incrustado que ha copiado de Recursos AEM a su página web.
El código incrustado copiado responde, por lo que debe ajustarse automáticamente al área de incrustación de la página.

## Integración del letrero carrusel con una vista rápida existente {#integrating-the-carousel-banner-with-an-existing-quickview}

Nota: este paso solo se aplica si es cliente independiente de Recursos AEM.

El último paso de este proceso es integrar la pancarta de carrusel con una implementación de vista rápida existente en el sitio web. Cada implementación de vista rápida es única y se necesita un enfoque específico que muy probablemente involucre la asistencia de una persona de TI de primer nivel.

La implementación de vista rápida existente normalmente representa una cadena de acciones interrelacionadas que se producen en la página web en el siguiente orden:

1. Un usuario activa un elemento en la interfaz de usuario del sitio web.
1. El código front-end obtiene una URL de vista rápida basada en el elemento de interfaz de usuario que se activó en el paso 1.
1. El código front-end envía una solicitud de Ajax utilizando la dirección URL obtenida en el paso 2.
1. La lógica back-end devuelve los datos o el contenido de vista rápida correspondientes al código front-end.
1. El código front-end carga el contenido o los datos de vista rápida.
1. De forma opcional, el código front-end convierte los datos de vista rápida cargados en una representación HTML.
1. El código front-end muestra un cuadro de diálogo o panel modal y representa el contenido HTML en la pantalla para el usuario final.

Es posible que estas llamadas no representen llamadas de API públicas independientes a las que la lógica de página web puede llamar de forma arbitraria. En su lugar, es una llamada encadenada donde cada paso siguiente se oculta en la última fase (llamada de retorno) del paso anterior.

Al mismo tiempo que la pancarta de carrusel sustituye al paso 1 y al paso 2 parcial, cuando un usuario hace clic en un punto interactivo o mapa de imagen dentro de la pancarta de carrusel, el visor controla dicha interacción del usuario. El visor devuelve un evento a la página web que contiene todos los datos de puntos interactivos o mapas de imagen añadidos anteriormente.

En un controlador de eventos de este tipo, el código front-end hace lo siguiente:

* Escucha un evento emitido por la pancarta de carrusel.
* Construye una URL de vista rápida en función de los datos de zona interactiva o mapa de imagen.
* Activa el proceso de cargar la vista rápida desde el servidor y procesarla en la pantalla para su visualización.

El código incrustado devuelto por Recursos AEM ya tiene un controlador de eventos listo para usar que se comenta.

Por lo tanto, solo es necesario descomentar el código y reemplazar el cuerpo del controlador ficticio por el código específico de la página web en particular.

El proceso de construir la URL de vista rápida es básicamente opuesto al proceso utilizado para identificar las variables de zona interactiva y mapa de imagen que se han cubierto anteriormente.

Consulte [Identificación de variables](#identifying-hotspot-and-image-map-variables)de zona interactiva y mapa de imagen.

El último paso para activar la dirección URL de vista rápida y activar el panel de vista rápida requiere probablemente la asistencia de una persona de TI del cliente de su departamento de TI. Tienen los conocimientos para saber cómo activar con precisión la implementación de vista rápida desde el paso adecuado, con una URL de vista rápida lista para usar.

## Uso de las vistas rápidas para crear ventanas emergentes personalizadas {#using-quickviews-to-create-custom-pop-ups}

Consulte [Uso de las vistas rápidas para crear ventanas emergentes](/help/assets/custom-pop-ups.md)personalizadas.
