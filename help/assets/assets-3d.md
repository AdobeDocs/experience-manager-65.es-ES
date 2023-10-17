---
title: Uso de recursos 3D en Dynamic Media
description: Descubra cómo puede cargar, gestionar, ver y distribuir recursos 3D en Dynamic Media como una experiencia envolvente.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
feature: 3D Assets,Asset Management
role: User, Admin
exl-id: 01c96f1e-c0e6-497d-bd7a-c0fd547a34da
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '2354'
ht-degree: 3%

---

# Uso de recursos 3D en Dynamic Media {#working-with-three-d-assets-dm}

Dynamic Media le permite cargar, gestionar, ver y distribuir recursos 3D como experiencias envolventes.

* Publicación con un clic (con **[!UICONTROL Publicación rápida]** en la barra de herramientas) de recursos 3D para generar una URL.
* Compatibilidad optimizada para ver recursos 3D con el ajuste preestablecido de visualizador dimensional interactivo de alta calidad con tecnología Adobe Dimension.
* El componente 3D Media WCM permite añadir fácilmente recursos 3D a las páginas de Adobe Experience Manager Sites.

No se requiere ninguna configuración adicional para utilizar recursos 3D en Dynamic Media.

![Zapato en 3d](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png) *Página de detalles de un zapato tridimensional.*

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formatos 3D admitidos en Dynamic Media {#supported-three-d-file-formats-in-dm}

Dynamic Media admite los siguientes formatos 3D.

Consulte también [Formatos 3D admitidos](/help/assets/assets-formats.md).

| Extensión de archivo 3D | Formato de archivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmisión binaria GL | model/gltf-binary | Incluye los materiales y las texturas como un solo recurso. |
| OBJ | Archivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Estereolitografía | application/vnd.ms-pki.stl |  |
| USDZ | Universal Scene Description Archivo zip | model/vnd.usdz+zip | *Compatibilidad únicamente con la ingesta; no hay visualización ni interacción disponibles.* USDZ es un formato 3D patentado que los dispositivos Safari y iOS pueden ver de forma nativa. |

>[!NOTE]
>
>El componente WCM de medios en 3D y la vista previa 3D de la página de detalles de un recurso no son compatibles con la última versión de Chrome (97.x). En su lugar, para trabajar con recursos 3D, utilice Firefox o Safari, o bien utilice una versión anterior de Chrome (96.x).

## Inicio rápido: Recursos 3D en Dynamic Media {#quick-start-three-d}

La siguiente descripción paso a paso del flujo de trabajo se ha diseñado para ayudarle a ponerse en marcha rápidamente con los recursos 3D en el modo Dynamic Media - Scene7.

>[!IMPORTANT]
>
>Los recursos 3D no son compatibles con Dynamic Media: modo híbrido.

Antes de trabajar con recursos 3D en Dynamic Media, asegúrese de que su Experience Manager de ya ha activado y configurado los Cloud Service de Dynamic Media en el modo Dynamic Media - Scene7.

Consulte [CLOUD SERVICE ConfigurE DE DYNAMIC MEDIA](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) en Configuración de Dynamic Media: modo Scene7 y [Solución de problemas de Dynamic Media - Modo Scene7](/help/assets/troubleshoot-dms7.md).

1. **Carga de recursos 3D**

   * [Carga de recursos 3D para su uso en Dynamic Media](/help/assets/manage-assets.md#uploading-assets).
   * [Formatos de archivo 3D compatibles para la carga en Dynamic Media](#supported-three-d-file-formats-in-dm).

1. **Administración de recursos 3D**

   * Organización y búsqueda de recursos 3D

      * [Organización de recursos digitales](/help/assets/organize-assets.md#organize-digital-assets).
      * [Búsqueda de recursos 3D](/help/assets/search-assets.md).
      * [Uso de predicados personalizados para filtrar los resultados de búsqueda](/help/assets/search-assets.md#custompredicates).

   * Ver recursos 3D

      * [Visualización e interacción con recursos 3D](#viewing-three-d-assets).
      * [Administrar el ajuste preestablecido de visualizador dimensional](/help/assets/managing-viewer-presets.md).

   * Trabajo con metadatos de recursos 3D

      * [Administración de metadatos para recursos digitales](/help/assets/metadata.md).
      * [Esquemas de metadatos](/help/assets/metadata-schemas.md).

1. **Publicación de recursos 3D**

   * [Publicación de recursos estáticos de Dynamic Media 3D](#publishing-three-d-assets)
   * [Métodos alternativos para publicar recursos de Dynamic Media 3D mediante el visualizador dimensional](#alternate-publish-methods)

## Visualización e interacción con recursos 3D {#viewing-three-d-assets}

En esta sección se describe cómo ver recursos 3D e interactuar con ellos de dos formas diferentes: desde la página de detalles de recursos y desde el componente Medios 3D en Experience Manager Sites.

El visor 3D interactivo incluye, entre otras cosas, una colección de controles de cámara interactivos que le permiten orbitar, aplicar zoom y recorrer el recurso 3D.

El tiempo que se tarda en abrir un recurso 3D en la vista de página Detalles del recurso depende de varios factores. Estos factores incluyen cosas como las siguientes:

* Ancho de banda al servidor.
* Latencias al servidor
* Complejidad de la imagen.

Además, las capacidades del equipo cliente, como una estación de trabajo, un portátil o un dispositivo táctil móvil, también son importantes a la hora de manipular la cámara de forma interactiva. Un sistema razonablemente potente con buenas capacidades gráficas puede hacer que la experiencia de visualización 3D interactiva sea más fluida y favorable.

>[!TIP]
>
>Puede abrir el ajuste preestablecido de visualizador dimensional en el Editor de ajustes preestablecidos de visualizador para practicar la navegación por un recurso 3D sin necesidad de cargar primero ningún archivo 3D. El ajuste preestablecido de visualizador dimensional tiene un recurso 3D integrado con el que puede interactuar.
>
>Consulte [Administrar ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md).

## Ver e interactuar con un recurso 3D desde la página de detalles del recurso {#viewing-three-d-assets-from-asset-details-page}

Consulte también [Vista previa de recursos mediante la interfaz de software](/help/assets/previewing-assets.md).

**Para ver e interactuar con un recurso 3D desde la página de detalles de recursos:**

1. Asegúrese de haber cargado recursos 3D en Experience Manager.

   Consulte [Carga de recursos 3D para su uso en Dynamic Media](/help/assets/manage-assets.md#uploading-assets).

1. Del Experience Manager, en el **[!UICONTROL Navegación]** página, vaya a **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. Cerca de la esquina superior derecha de la página, desde el **[!UICONTROL Ver]** , seleccione la opción **[!UICONTROL Vista de tarjeta]**.
1. Desplácese hasta un recurso 3D que desee ver.
1. Seleccione la tarjeta del recurso 3D.
1. En la página de vista de detalles del recurso 3D, realice una de las acciones siguientes:

   | Ver | Descripción | Acción del ratón | Acción de pantalla táctil |
   | --- | --- | --- | --- |
   | **Gire la cámara** | Haga girar la vista alrededor de la escena 3D y de los objetos. | Haga clic con el botón izquierdo + arrastre. | Presione con un solo dedo + arrastre. |
   | **Panorámica de la cámara** | Mueva la vista de forma panorámica a la izquierda, a la derecha, arriba o abajo. | Haga clic con el botón derecho y arrastre. | Presione con dos dedos + arrastre. |
   | **Zoom de la cámara** | Desplazarse dentro y fuera de las áreas de la escena 3D. | Rueda de desplazamiento. | Pellizco de dos dedos. |
   | **Vuelva a centrar su cámara** | Vuelva a centrar la cámara en un punto de un objeto de la escena 3D. | Haga doble clic en. | Pulse dos veces. |
   | **Restablecer** | Cerca de la esquina inferior derecha de la página, seleccione el icono Restablecer para restaurar el punto de destino de vista en el centro del recurso 3D. El restablecimiento también acerca o aleja la cámara para mostrar el recurso en su totalidad y a un tamaño de visualización razonable. |   |   |
   | **Modo de pantalla completa** | Para acceder al modo de pantalla completa, en la esquina inferior derecha de la página, seleccione el icono Pantalla completa. |   |   |

1. En la esquina superior derecha de la página, seleccione **[!UICONTROL Cerrar]** para volver a la página Assets.

## Visualización e interacción de un recurso 3D dentro de un componente de medios 3D {#interacting-with-asset-inside-three-d-media-component}

Cuando una página web está en **[!UICONTROL Editar]** modo, no es posible interactuar con un recurso 3D. Para que el recurso sea interactivo, puede utilizar el **[!UICONTROL Previsualizar]** función para ver la página web en el editor de páginas con acceso completo a la funcionalidad del componente de medios 3D.

>[!IMPORTANT]
>
>Solo podrá realizar esta tarea una vez que haya añadido un componente de medios 3D a una página web y le haya asignado un recurso 3D. Consulte [Adición del componente de medios 3D a una página web](#adding-the-three-d-media-component-to-a-web-page) y [Asignación de un recurso 3D a un componente de medios 3D](#assigning-a-three-d-asset-to-the-component).

Consulte también [Vista previa de recursos mediante la interfaz de software](/help/assets/previewing-assets.md).

**Para ver e interactuar con un recurso 3D dentro de un componente de medios 3D:**

1. Mientras una página web se encuentra en **[!UICONTROL Editar]** modo, realice una de las siguientes acciones:

   * Cerca de la parte superior derecha de la página, seleccione **[!UICONTROL Previsualizar]** para entrar **[!UICONTROL Previsualizar]** modo.
   * Eliminar `/editor.html` desde la dirección URL de la página en el explorador.

   ![Recurso 3D que se muestra dentro del componente de medios 3D](/help/assets/assets-dm/3d-asset-in-3d-media.png)
Un recurso 3D completamente interactivo, como se muestra en **[!UICONTROL Previsualizar]** modo.

1. Mientras está en **[!UICONTROL Previsualizar]** modo, realice una de las siguientes acciones:

   | Ver | Descripción | Acción del ratón | Acción de pantalla táctil |
   | --- | --- | --- | --- |
   | **Gire la cámara** | Haga girar la vista alrededor de la escena 3D y de los objetos. | Haga clic con el botón izquierdo + arrastre. | Presione con un solo dedo + arrastre. |
   | **Panorámica de la cámara** | Mueva la vista de forma panorámica a la izquierda, a la derecha, arriba o abajo. | Haga clic con el botón derecho y arrastre. | Presione con dos dedos + arrastre. |
   | **Zoom de la cámara** | Desplazarse dentro y fuera de las áreas de la escena 3D. | Rueda de desplazamiento. | Pellizco de dos dedos. |
   | **Vuelva a centrar su cámara** | Vuelva a centrar la cámara en un punto de un objeto de la escena 3D. | Haga doble clic en. | Pulse dos veces. |
   | **Restablecer** | Cerca de la esquina inferior derecha de la página, seleccione el icono Restablecer para restaurar el punto de destino de vista en el centro del recurso 3D. El restablecimiento también acerca o aleja la cámara para mostrar el recurso en su totalidad y a un tamaño de visualización razonable. |   |   |
   | **Modo de pantalla completa** | Para acceder al modo de pantalla completa, en la esquina inferior derecha de la página, seleccione el icono Pantalla completa. |   |   |

## Acerca del trabajo con el componente de medios en 3D {#working-with-three-d-media-component}

Dynamic Media incluye un componente multimedia 3D de Dynamic Media que puede utilizar en Adobe Experience Manager Sites para permitir la visualización interactiva de modelos 3D en sus páginas web.

* [Añadir el componente Medios 3D a la plantilla de página](#adding-three-d-media-component-to-page-template)
* [Adición del componente Medios 3D a una página web](#adding-the-three-d-media-component-to-a-web-page)
   * [Opcional: configuración del componente de medios en 3D](#configuring-the-three-d-component)
* [Asignar un recurso 3D al componente de medios 3D](#assigning-a-three-d-asset-to-the-component)

## Añadir el componente Medios 3D a la plantilla de página {#adding-three-d-media-component-to-page-template}

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL Plantillas]**.
1. Desplácese hasta la plantilla de página en la que desea activar el componente 3D y seleccione la plantilla.
1. Seleccionar **[!UICONTROL Editar]** para poder abrir la plantilla.
1. Cerca de la parte superior derecha de la página, en el menú desplegable, seleccione **[!UICONTROL Estructura]** modo, si aún no está activo.

   ![3d-media-component-structure](/help/assets/assets-dm/3d-media-component-structure.png)

1. Seleccione un área vacía en la **[!UICONTROL Contenedor de diseño]** región para seleccionarla y abrir su barra de herramientas asociada.
1. En la barra de herramientas, seleccione **[!UICONTROL Política]** para abrir el **[!UICONTROL Editor de directivas]**.
1. En el **[!UICONTROL Propiedades]** , en la sección **[!UICONTROL Componentes permitidos]** pestaña, desplácese hasta **[!UICONTROL Dynamic Media]**, luego expanda la lista y marque **[!UICONTROL Medios en 3D]**.
1. Seleccionar **[!UICONTROL Listo]** para guardar los cambios y cerrar el **[!UICONTROL Editor de directivas]**.

   Ahora puede colocar el componente Dynamic Media 3D Media en todas las páginas que utilicen esta plantilla.

## Adición del componente Medios 3D en una página web {#adding-the-three-d-media-component-to-a-web-page}

Si utiliza Experience Manager como sistema de gestión de contenido web, puede añadir recursos 3D a sus páginas web mediante el componente de medios 3D.

Consulte también [Adición de recursos de Dynamic Media en páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).

**Para añadir el componente Medios 3D en una página web:**

1. Abra Experience Manager Sites y seleccione la página web a la que desea agregar el componente Dynamic Media 3D Media.
1. Seleccione el **[!UICONTROL Editar]** Icono (lápiz) para poder abrir la página en el editor de páginas. Asegúrese de que **[!UICONTROL Editar]** El modo está seleccionado cerca de la parte superior derecha de la página.

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. En la barra de herramientas, seleccione el icono Panel lateral para activar o desactivar la visualización del panel.

1. En el panel lateral, seleccione el icono del signo más para abrir **[!UICONTROL Componentes]** lista.

   ![3d-media-component-drag-drop](/help/assets/assets-dm/3d-assets-filter.png)

1. Arrastre el **[!UICONTROL Medios en 3D]** del componente de **[!UICONTROL Componentes]** a la ubicación de la página donde desea que aparezca el visor 3D.

Ya está listo para asignar un recurso 3D al componente.

Consulte [Asignar un recurso 3D al componente de medios 3D](#assigning-a-three-d-asset-to-the-component).

### Opcional: configuración del componente de medios en 3D {#configuring-the-three-d-component}

1. En el editor de páginas de Experience Manager Sites, seleccione **[!UICONTROL Visor de medios en 3D]** componente que agregó anteriormente a la página.
1. Seleccione el **[!UICONTROL Configuración]** (llave inglesa) para abrir el cuadro de diálogo de configuración de componentes.

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. En el cuadro de diálogo Medios 3D, en la lista desplegable Ajuste preestablecido de visualizador, seleccione **[!UICONTROL Dimensional]** para asignar el ajuste preestablecido de visualizador dimensional al componente.

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. En la esquina superior derecha, seleccione la marca de verificación para guardar los cambios.

## Asignar un recurso 3D al componente de medios 3D {#assigning-a-three-d-asset-to-the-component}

Después de agregar un componente de medios 3D a una página web, puede asignarle un recurso 3D.

Consulte [Adición del componente Medios 3D a una página web](#adding-the-three-d-media-component-to-a-web-page).

**Para asignar un recurso 3D al componente de medios 3D:**

1. En el editor de páginas de Experience Manager Sites, seleccione **[!UICONTROL Assets]** icono para abrir **[!UICONTROL Assets]** en el panel lateral.
1. En la lista desplegable, seleccione **[!UICONTROL 3D]** para mostrar solo tipos de archivos de recursos 3D.
1. En el panel lateral, busque o desplácese hasta el recurso 3D que desee ver en la página que está editando.
1. Arrastre el recurso 3D desde el panel lateral Recursos y suéltelo en el **[!UICONTROL Medios en 3D]** componente que agregó anteriormente a la página.

   ![Asignar recursos 3D al componente de medios 3D](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>Mientras una página web está en Experience Manager Sites **[!UICONTROL Editar]** modo, el componente de medios 3D muestra el recurso 3D, pero no es posible interactuar con él. Para que el recurso sea interactivo, puede utilizar el **[!UICONTROL Previsualizar]** función para ver la página web en el editor de páginas con acceso completo a la funcionalidad del componente de medios 3D.

## Publicación de recursos estáticos de Dynamic Media 3D {#publishing-three-d-assets}

Dynamic Media acepta varios formatos de archivo 3D compatibles con *contenido estático* en Dynamic Media. El contenido estático significa que puede cargar y publicar recursos 3D, pero no es compatible con *imágenes variables* o ajuste de imagen asociado al recurso 3D. El motivo es que Dynamic Media Imaging Server no reconoce formatos 3D. De este modo, después de publicar un recurso 3D en Dynamic Media, tiene una URL instantánea que puede copiar. La dirección URL del recurso 3D sigue la estructura URL habitual de Dynamic Media. Sin embargo, no se puede editar ningún parámetro en la dirección URL del recurso, a diferencia de los recursos de imagen tradicionales de Dynamic Media.

Consulte también [Obtener una URL para un recurso estático](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

En el **[!UICONTROL Vista de tarjeta]**, aparece un pequeño icono de globo terráqueo directamente debajo del nombre de un recurso y a la izquierda de su fecha y hora para indicar que se ha publicado. En la **[!UICONTROL vista de lista]**, una columna **[!UICONTROL Publicada]** indica qué recursos se publican o cuáles no.

Si utiliza Experience Manager como WCM, utilice este método de publicación para añadir los recursos 3D de Dynamic Media directamente en la página web.

Consulte también [Publicar recursos de Dynamic Media](publishing-dynamicmedia-assets.md).

Consulte también [Publicar páginas](/help/sites-authoring/publishing-pages.md).

**Para publicar recursos estáticos de Dynamic Media 3D:**

1. Abra un recurso 3D (formato de archivo GLB, OBJ o STL) para poder verlo en la página de detalles del recurso.
1. En la barra de herramientas, seleccione **[!UICONTROL Publicación rápida]**.

   ![3d-asset-quick-publish](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. Seleccionar **[!UICONTROL Cerrar]** para salir del cuadro de diálogo y volver a la página de detalles del recurso.
1. En la lista desplegable situada a la izquierda del nombre de fichero del recurso 3D, seleccione **[!UICONTROL Representaciones]**.

   ![3d-asset-renditions](/help/assets/assets-dm/3d-asset-renditions.png)

1. Seleccionar **[!UICONTROL original]**. Cuando se publica un recurso 3D (o &quot;activado&quot;), la variable **[!UICONTROL URL]** aparece cerca de la esquina inferior izquierda de la página si se cumplen todas las condiciones de recurso 3D siguientes:
   * El recurso 3D es un formato compatible (GLB, OBJ, STL y USDZ).
   * El recurso 3D se ha introducido en Dynamic Media Image Production System (IPS).
   * Se publica el recurso 3D.

   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. Seleccionar **[!UICONTROL URL]** para que pueda mostrar la URL de producción directa del recurso 3D, que puede copiar y utilizar en páginas web.

### Métodos alternativos para publicar recursos de Dynamic Media 3D mediante el visualizador dimensional {#alternate-publish-methods}

Utilice los dos métodos siguientes para publicar recursos de Dynamic Media 3D si lo hace *no* utilice Experience Manager como WCM.

* **[!UICONTROL URL]** - Uso **[!UICONTROL URL]** si utiliza un sistema de administración de contenido web de terceros y desea vincular recursos de Dynamic Media 3D a sus páginas web mediante el visualizador dimensional.

  Consulte [Vinculación de URL en la aplicación web](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset).

* **[!UICONTROL Incrustar]** - Uso **[!UICONTROL Incrustar]** si desea ver un recurso de Dynamic Media 3D incrustado en una página web mediante el visualizador dimensional. El código incrustado se copia en el portapapeles para pegarlo en las páginas web. No se permite la edición del código en **[!UICONTROL Incrustar]** Cuadro de diálogo.

  Consulte [Incrustar Dynamic Media Video, el visualizador de imágenes o el visualizador dimensional en una página web](/help/assets/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page).
