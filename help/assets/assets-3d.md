---
title: Uso de recursos 3D en Dynamic Media
seo-title: Uso de recursos 3D en Dynamic Media
description: Aprenda a trabajar con recursos 3D en Dynamic Media
seo-description: Aprenda a trabajar con recursos 3D en Dynamic Media
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: 2f0e626aa16a62203755e29800a5935b350ffe79
workflow-type: tm+mt
source-wordcount: '2162'
ht-degree: 4%

---


# Uso de recursos 3D en Dynamic Media {#working-with-three-d-assets-dm}

Dynamic Media le permite cargar, gestionar, vista y distribuir recursos 3D como experiencias envolventes.

* Publicación con un solo clic (mediante Publicación **** rápida en la barra de herramientas) de imágenes 3D para generar su URL.
* Compatibilidad optimizada para ver recursos 3D con el ajuste preestablecido de visor de dimensiones interactivo y de alta calidad con tecnología Adobe Dimension. El ajuste preestablecido de visor incluye, entre otras cosas, una colección de controles de cámara interactivos que le permiten orbitar, aplicar zoom y desplazarse.
* El componente WCM de medios 3D le permite añadir fácilmente recursos 3D a sus páginas Sitios de AEM.

No hay instalación ni configuración de ningún tipo para utilizar recursos 3D en Dynamic Media.

![zapato en 3d](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formatos de archivo 3D admitidos en Dynamic Media {#supported-three-d-file-formats-in-dm}

Dynamic Media admite los siguientes formatos de archivo 3D:

| Extensión de archivo 3D | Formato de archivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmisión binaria de GL | model/gltf-binary | Incluye las texturas con el recurso en lugar de hacer referencia a ellas como imágenes externas. |
| OBJ | Archivo de objeto WaveFront 3D | application/x-tgif |  |
| STL | Esteroolitografía | application/vnd.ms-pki.stl |  |
| USDZ | Archivo zip de descripción de escena universal | model/vnd.usdz+zip | *Apoyo a la ingestión únicamente; no hay visualización ni interacción disponibles.* USDZ es el formato 3D propiedad de Apple que solo puede ser vista por Safari o iOS. |

## Inicio rápido: Recursos 3D en Dynamic Media {#quick-start-three-d}

La siguiente descripción paso a paso del flujo de trabajo se ha diseñado para ayudarle en el uso inicial de los recursos 3D en el modo Dynamic Media - Scene7.

>[!NOTE]
>
>Los recursos 3D no son compatibles con Dynamic Media: modo híbrido.

Antes de trabajar con recursos 3D en Dynamic Media, asegúrese de que el administrador de AEM ya ha activado y configurado los servicios de Dynamic Media Cloud en el modo Dynamic Media - Scene7.

Consulte [Configuración de los servicios](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) de Dynamic Media Cloud en Configuración de Dynamic Media - modo Scene7 y [Resolución de problemas de Dynamic Media - modo Scene7.](/help/assets/troubleshoot-dms7.md)

1. **Carga de recursos 3D**

   * [Carga de recursos 3D para su uso en Dynamic Media](/help/assets/managing-assets-touch-ui.md#uploading-assets).
   * [Formatos de archivo 3D admitidos para la carga en Dynamic Media](#supported-three-d-file-formats-in-dm).

1. **Gestión de recursos 3D**

   * Organización y búsqueda de recursos 3D

      * [Organización de recursos](/help/assets/organize-assets.md#organize-digital-assets)digitales.
      * [Búsqueda de recursos](/help/assets/search-assets.md)3D.
      * [Uso de predicados personalizados para filtrar los resultados](/help/assets/search-assets.md#custompredicates)de búsqueda.
   * Recursos 3D de Vista

      * [Visualización e interacción con recursos](#viewing-three-d-assets)3D.
      * [Administración del ajuste preestablecido](/help/assets/managing-viewer-presets.md)de visor de dimensiones.
   * Trabajo con metadatos de recursos 3D

      * [Administración de metadatos para recursos](/help/assets/metadata.md)digitales.
      * [Esquemas de metadatos](/help/assets/metadata-schemas.md).



1. **Publicación de recursos 3D**

   * [Publicación de recursos 3D de Dynamic Media](#publishing-three-d-assets)

## Visualización e interacción con recursos 3D {#viewing-three-d-assets}

En esta sección se describe cómo vista e interacción con recursos 3D de dos formas diferentes: desde la página de detalles del recurso y desde el componente de medios 3D en Sitios.

El visor 3D interactivo incluye, entre otras cosas, una colección de controles de cámara interactivos que le permiten orbitar, aplicar zoom y recorrer el recurso 3D.

Tenga en cuenta que el tiempo que tarda en abrir un recurso 3D en la vista de la página Detalles del recurso depende de varios factores. Estos factores incluyen elementos como los siguientes:

* Ancho de banda del servidor.
* Latencias en el servidor
* Complejidad de la imagen.

Además, las capacidades del ordenador cliente, como una estación de trabajo, un ordenador portátil o un dispositivo móvil táctil, también son importantes para tener en cuenta al manipular la cámara de forma interactiva. Un sistema razonablemente potente con buenas capacidades gráficas puede hacer que la experiencia de visualización interactiva en 3D sea más cómoda y agradable.

>[!TIP]
>
>Puede abrir el ajuste preestablecido de visor de dimensiones en el Editor de ajustes preestablecidos de visor para practicar la navegación por un recurso 3D sin necesidad de cargar primero ningún archivo 3D. El ajuste preestablecido de visor de dimensiones tiene un recurso 3D integrado con el que interactuar.
>
>See [Managing viewer presets](/help/assets/managing-viewer-presets.md).

## Visualización e interacción con un recurso 3D desde la página de detalles del recurso {#viewing-three-d-assets-from-asset-details-page}

Consulte también [Vista previa de recursos mediante la interfaz](/help/assets/previewing-assets.md)de software.

**vista e interacción con un recurso 3D desde la página de detalles del recurso**

1. Asegúrese de que ha cargado los recursos 3D en AEM.

   Consulte [Carga de recursos 3D para su uso en Dynamic Media](/help/assets/managing-assets-touch-ui.md#uploading-assets).

1. En AEM, en la página **[!UICONTROL Navegación]** , toque **[!UICONTROL Recursos > Archivos]**.
1. Near the upper-right corner of the page, from the **[!UICONTROL View]** drop-down list, tap **[!UICONTROL Card View]**.
1. Vaya a un recurso 3D que desee ver.
1. Toque la tarjeta del recurso 3D para abrirlo en la página de información del recurso.
1. En la página de vista de detalles del recurso 3D, realice una de las siguientes acciones:

   * **Gire la cámara** : ordene la vista alrededor de la escena y los objetos 3D.
      * _Ratón_: Haga clic y arrastre.
      * _Pantalla_ táctil: Presione con un solo dedo y arrastre.
   * **Recorra la cámara** : deslice la vista hacia la izquierda, hacia la derecha, hacia arriba o hacia abajo.
      * _Ratón_: Haga clic con el botón derecho y arrastre.
      * _Pantalla_ táctil: Presione dos dedos y arrastre.
   * **Zoom en la cámara** : haga zoom en la cámara para entrar y salir de áreas de la escena 3D.
      * _Ratón_: Rueda de desplazamiento.
      * _Pantalla_ táctil: Pellizque con dos dedos.
   * **Volver a introducir la cámara** : vuelva a introducir la cámara en un punto de la escena 3D.
      * _Ratón_: Haga clic con el Doble.
      * _Pantalla_ táctil: Toque el Doble.
   * **Restaurar** : cerca de la esquina inferior derecha de la página, toque el icono Restablecer para restaurar el punto de destinatario de vista al centro del recurso 3D. El reinicio también hace que la cámara se acerque o se aleje para mostrar el recurso en su totalidad y con un tamaño de visualización razonable.
   * **Modo** de pantalla completa: para acceder al modo de pantalla completa, en la esquina inferior derecha de la página, toque el icono de pantalla completa.

1. En la esquina superior derecha de la página, toque **[!UICONTROL Cerrar]** para volver a la página Recursos.

## Visualización e interacción con un recurso 3D dentro de un componente de medios 3D {#interacting-with-asset-inside-three-d-media-component}

Cuando una página web está en modo de **[!UICONTROL edición]** , no es posible interactuar con un recurso 3D. Para que el recurso sea interactivo, puede utilizar la función de **[!UICONTROL Previsualización]** para vista de la página web en el editor de páginas con acceso completo a la funcionalidad del componente de medios 3D.

>[!IMPORTANT]
>
>Esta tarea solo se puede realizar una vez que haya agregado un componente de medios 3D a una página web y haya asignado un recurso 3D al componente. Consulte [Añadir el componente de medios 3D en una página](#adding-the-three-d-media-component-to-a-web-page) web y [Asignación de un recurso 3D a un componente](#assigning-a-three-d-asset-to-the-component)de medios 3D.

Consulte también [Vista previa de recursos mediante la interfaz](/help/assets/previewing-assets.md)de software.

**vista e interacción con un recurso 3D dentro de un componente de medios 3D**

1. Mientras una página web está en modo de **[!UICONTROL edición]** , realice una de las siguientes acciones:

   * Cerca de la esquina superior derecha de la página, haga clic en **[!UICONTROL Previsualización]** para acceder al modo de **[!UICONTROL Previsualización]** .
   * Elimine `/editor.html` de la dirección URL de la página en el explorador.
   ![Recurso 3D que se muestra dentro del componente](/help/assets/assets-dm/3d-asset-in-3d-media.png)Medios 3D Un recurso 3D completamente interactivo, tal como se muestra en el modo de **[!UICONTROL Previsualización]** .

1. En el modo de **[!UICONTROL Previsualización]** , realice una de las siguientes acciones:

   * **Gire la cámara** : ordene la vista alrededor de la escena y los objetos 3D.
      * _Ratón_: Haga clic y arrastre.
      * _Pantalla_ táctil: Presione con un solo dedo y arrastre.
   * **Recorra la cámara** : deslice la vista hacia la izquierda, hacia la derecha, hacia arriba o hacia abajo.
      * _Ratón_: Haga clic con el botón derecho y arrastre.
      * _Pantalla_ táctil: Presione dos dedos y arrastre.
   * **Zoom en la cámara** : haga zoom en la cámara para entrar y salir de áreas de la escena 3D.
      * _Ratón_: Rueda de desplazamiento.
      * _Pantalla_ táctil: Pellizque con dos dedos.
   * **Volver a introducir la cámara** : vuelva a introducir la cámara en un punto de la escena 3D.
      * _Ratón_: Haga clic con el Doble.
      * _Pantalla_ táctil: Toque el Doble.
   * **Restaurar** : cerca de la esquina inferior derecha de la página, toque el icono Restablecer para restaurar el punto de destinatario de vista al centro del recurso 3D. El reinicio también hace que la cámara se acerque o se aleje para mostrar el recurso en su totalidad y con un tamaño de visualización razonable.
   * **Modo** de pantalla completa: para acceder al modo de pantalla completa, en la esquina inferior derecha de la página, toque el icono de pantalla completa.

## Acerca del trabajo con el componente de medios 3D {#working-with-three-d-media-component}

Dynamic Media incluye un componente de Dynamic Media 3D que puede utilizar en los sitios AEM para permitir la visualización interactiva de modelos 3D en sus páginas web.

* [Añadir el componente de medios 3D en la plantilla de página](#adding-three-d-media-component-to-page-template)
* [Añadir el componente de medios 3D en una página web](#adding-the-three-d-media-component-to-a-web-page)
   * [Opcional: Configuración del componente de medios 3D](#configuring-the-three-d-component)
* [Asignación de un recurso 3D al componente de medios 3D](#assigning-a-three-d-asset-to-the-component)


## Añadir el componente de medios 3D en la plantilla de página {#adding-three-d-media-component-to-page-template}

1. Vaya a **[!UICONTROL Herramientas > General > Plantillas]**.
1. Vaya a la plantilla de página en la que desea habilitar el componente 3D y seleccione la plantilla.
1. Toque **[!UICONTROL Editar]** para abrir la plantilla.
1. Cerca de la esquina superior derecha de la página, en el menú desplegable, seleccione el modo **[!UICONTROL Estructura]** , si aún no está activo.

   ![3d-media-component-structure](/help/assets/assets-dm/3d-media-component-structure.png)

1. Toque un área vacía en la región del Contenedor **** Diseño para seleccionarla y abrir la barra de herramientas asociada.
1. En la barra de herramientas, toque el icono **[!UICONTROL Política]** para abrir el Editor **[!UICONTROL de directivas]**.
1. En la sección **[!UICONTROL Propiedades]** , en la ficha Componentes **** permitidos, desplácese hasta Medios **** dinámicos y, a continuación, expanda la lista y marque Medios **** 3D.
1. Toque **[!UICONTROL Listo]** para guardar los cambios y cerrar el Editor **[!UICONTROL de directivas]**.

   Ahora puede colocar el componente Medios 3D de Dynamic Media en todas las páginas que utilicen esta plantilla.

## Añadir el componente de medios 3D en una página web {#adding-the-three-d-media-component-to-a-web-page}

Si utiliza Adobe Experience Manager como sistema de gestor de contenido web, puede añadir recursos 3D a las páginas web mediante el componente de medios 3D.

See also [Adding Dynamic Media assets to pages](/help/assets/adding-dynamic-media-assets-to-pages.md).

1. Abra Sitios AEM y seleccione la página web a la que desea agregar el componente Medios 3D de Dynamic Media.
1. Toque el icono **[!UICONTROL Editar]** (lápiz) para abrir la página en el editor de páginas. Asegúrese de que el modo **[!UICONTROL Editar]** está seleccionado cerca de la esquina superior derecha de la página.

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. En la barra de herramientas, toque el icono del panel lateral para activar o desactivar la visualización del panel.

1. En el panel lateral, toque el icono de signo más para abrir la lista **[!UICONTROL Componentes]** .

   ![3d-media-component-drag-drop](/help/assets/assets-dm/3d-assets-filter.png)

1. Arrastre el componente **[!UICONTROL 3D Media]** de la lista **[!UICONTROL Componentes]** a la ubicación de la página en la que desea que aparezca el visor 3D.

Ya está listo para asignar un recurso 3D al componente.

Consulte [Asignación de un recurso 3D a un componente](#assigning-a-three-d-asset-to-the-component)de medios 3D.

### Opcional: Configuración del componente de medios 3D {#configuring-the-three-d-component}

1. En el editor de páginas de AEM Sites, seleccione el componente de visor **[!UICONTROL de medios]** 3D que agregó anteriormente a la página.
1. Toque el icono **[!UICONTROL Configuración]** (llave inglesa) para abrir el cuadro de diálogo de configuración del componente.

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. En el cuadro de diálogo Medios 3D, en la lista desplegable Ajuste preestablecido de visor, seleccione **[!UICONTROL Dimensional]** para asignar el ajuste preestablecido de visor de dimensiones al componente.

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. En la esquina superior derecha, toque la marca de verificación para guardar los cambios.

## Asignación de un recurso 3D al componente de medios 3D {#assigning-a-three-d-asset-to-the-component}

Después de agregar un componente de medios 3D a una página web, puede asignarle un recurso 3D.

Consulte [Añadir el componente de medios 3D en una página](#adding-the-three-d-media-component-to-a-web-page)web.

1. En el editor de páginas de AEM Sites, haga clic en el icono **[!UICONTROL Recursos]** para abrir **[!UICONTROL Recursos]** en el panel lateral.
1. En la lista desplegable, seleccione **[!UICONTROL 3D]** para mostrar solo los tipos de archivo de recursos 3D.
1. En el panel lateral, busque o desplácese hasta el recurso 3D cuya vista desee realizar en la página que se esté editando.
1. Arrastre el recurso 3D desde el panel lateral Recursos y suéltelo en el componente Medios **** 3D que agregó anteriormente a la página.

   ![Asignación de un recurso 3d al componente de medios 3d](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>Mientras una página web está en el modo de **[!UICONTROL edición]** de sitios AEM, el componente de medios 3D muestra el recurso 3D, pero no es posible interactuar con el recurso. Para que el recurso sea interactivo, puede utilizar la función de **[!UICONTROL Previsualización]** para vista de la página web en el editor de páginas con acceso completo a la funcionalidad del componente de medios 3D.

## Publishing Dynamic Media 3D assets {#publishing-three-d-assets}

Dynamic Media acepta diversos formatos de archivo 3D que se admiten como contenido ** estático en Dynamic Media. El contenido estático significa que se pueden cargar y publicar recursos 3D, pero no se admiten imágenes *dinámicas* ni redireccionamiento de imágenes asociados al recurso 3D. El motivo es que el servidor de imágenes de Dynamic Media no reconoce los formatos 3D. Como tal, después de publicar un recurso 3D en Dynamic Media, tiene una URL instantánea que puede copiar. La URL del recurso 3D sigue la estructura de URL de Dynamic Media habitual. Sin embargo, no puede editar ningún parámetro en la URL del recurso, a diferencia de los recursos de imagen tradicionales en Dynamic Media.

En la Vista **[!UICONTROL de]** tarjeta, aparece un pequeño icono de globo terráqueo directamente debajo del nombre de un recurso y a la izquierda de la fecha y hora para indicar que se ha publicado. En la **[!UICONTROL vista de lista]**, una columna **[!UICONTROL Publicada]** indica qué recursos se publican o cuáles no.

Consulte también [Publicación de recursos](publishing-dynamicmedia-assets.md)de Dynamic Media.

Consulte también [Publicación de páginas](/help/sites-authoring/publishing-pages.md).

>[!MORELIKETHIS]
>
>Si utiliza un sistema de gestor de contenido web de terceros, puede vincular o incrustar recursos 3D en sus páginas web.
>
>See [Linking URLs to your web application](linking-urls-to-yourwebapplication.md).


**Para publicar recursos 3D de Dynamic Media**

1. Abra un recurso 3D (formato de archivo GLB, OBJ o STL) para vista en la página de detalles del recurso.
1. En la barra de herramientas, toque **[!UICONTROL Publicación]** rápida.

   ![3d-asset-quick-publish](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. Toque **[!UICONTROL Cerrar]** para salir del cuadro de diálogo y volver a la página de detalles del recurso.
1. En la lista desplegable situada a la izquierda del nombre de archivo del recurso 3D, toque **[!UICONTROL Representaciones]**.

   ![3d-asset-renditions](/help/assets/assets-dm/3d-asset-renditions.png)

1. Toque **[!UICONTROL original]**. Cuando se publica un recurso 3D (o se &quot;activa&quot;), el botón URL aparece cerca de la esquina inferior izquierda de la página si se cumplen todas las condiciones de recursos 3D siguientes:
   * El recurso 3D es un formato admitido (GLB, OBJ, STL y USDZ).
   * El recurso 3D se ha incorporado al sistema de producción de imágenes de Dynamic Media (IPS).
   * Se publica el recurso 3D.
   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. Toque **[!UICONTROL URL]** para mostrar la URL de producción del recurso 3D.
