---
title: Adición de recursos de Dynamic Media a páginas
seo-title: Adición de recursos de Dynamic Media a páginas
description: Para añadir la funcionalidad de Dynamic Media a los recursos que se usan en las páginas web, puede añadir el componente de Dynamic Media o Medios interactivos directamente en la página.
seo-description: Para añadir la funcionalidad de Dynamic Media a los recursos que se usan en las páginas web, puede añadir el componente de Dynamic Media o Medios interactivos directamente en la página.
uuid: 650d0867-a079-4936-a466-55b7a30803a2
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 331f4980-5193-4546-a22e-f27e38bb8250
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# Adding Dynamic Media assets to pages{#adding-dynamic-media-assets-to-pages}

To add the Dynamic Media functionality to assets you use on your websites, you can add the **[!UICONTROL Dynamic Media]** or **[!UICONTROL Interactive Media]** component directly on the page. You do this by entering [!UICONTROL Design] mode and enabling the dynamic media components. A continuación, puede añadir estos componentes a la página y añadir recursos al componente. Los componentes de Dynamic Media y Medios interactivos son inteligentes; es decir, saben si va a añadir una imagen o un vídeo, y las opciones disponibles cambian según corresponda.

Puede añadir recursos de medios dinámicos directamente a la página si utiliza AEM como WCM.

>[!NOTE]
>
>Para los titulares de carrusel, hay mapas de imágenes disponibles de fábrica.

## Adding a Dynamic Media component to a page {#adding-a-dynamic-media-component-to-a-page}

Adding the [!UICONTROL Dynamic Media] or [!UICONTROL Interactive Media] component to a page is the same as adding a component to any page. The [!UICONTROL Dynamic Media] and [!UICONTROL Interactive Media] components are described in detail in the following sections.

Para añadir un componente o visor de Dynamic Media a una página:

1. En AEM, abra la página a la que desea añadir el componente de Dynamic Media.
1. If no Dynamic Media component is available, click the ruler in the [!UICONTROL Sidekick] to enter **[!UICONTROL Design]** mode, click **[!UICONTROL Edit]** parsys, and select **[!UICONTROL Dynamic Media]** to make the Dynamic Media components available.

   >[!NOTE]
   >
   >Consulte [Configuración de componentes en el modo Diseño](/help/sites-authoring/default-components-designmode.md) para obtener más información.

1. Return to **[!UICONTROL Edit]** mode by clicking the pencil icon in the [!UICONTROL Sidekick].
1. Drag the **[!UICONTROL Dynamic Media]** or **[!UICONTROL Interactive Media]** component from the **[!UICONTROL Other]** group in the sidekick onto the page in the desired location.
1. Haga clic en **[!UICONTROL Editar]** para abrir el componente.
1. [](#dynamic-media-component)Edite el componente según sea necesario y haga clic en **[!UICONTROL Aceptar]** para guardar los cambios.

## Componentes de Dynamic Media {#dynamic-media-components}

[!UICONTROL Los medios] dinámicos y los medios [!UICONTROL interactivos] están disponibles en la [!UICONTROL barra de tareas] en Medios **[!UICONTROL dinámicos]**. El componente de **[!UICONTROL Medios interactivos]** se utiliza para cualquier recurso interactivo, como vídeo interactivo, imágenes interactivas o conjuntos de carrusel. Para todos los demás componentes de Dynamic Media, utilice el componente de **[!UICONTROL Dynamic Media]**.

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>Estos componentes no están disponibles de forma predeterminada y se deben seleccionar en el modo Diseño para que se puedan usar. [Una vez que estén disponibles en modo](/help/sites-authoring/default-components-designmode.md)de diseño, puede añadir los componentes a la página como lo haría con cualquier otro componente de AEM.

### Componente de Dynamic Media {#dynamic-media-component}

El componente Dynamic Media es inteligente, ya sea que agregue una imagen o un vídeo, tiene varias opciones. El componente admite ajustes preestablecidos de imagen, visores basados en imágenes, como conjuntos de imágenes, conjuntos de giros, conjuntos de medios mixtos y vídeo. Además, el visor responde. Es decir, el tamaño de la pantalla cambia automáticamente en función del tamaño de la pantalla. Todos los visores son visores basados en HTML5.

>[!NOTE]
>
>When you add the [!UICONTROL Dynamic Media] component, and **[!UICONTROL Dynamic Media Settings]** is blank or you cannot add an asset properly, check the following:
>
>* [Dynamic Media](/help/assets/config-dynamic.md) se ha activado. Dynamic Media está desactivado de forma predeterminada.
>* La imagen tiene un archivo TIFF piramidal. Las imágenes importadas antes de la activación de Dynamic Media no tienen un archivo TIFF piramidal.
>



#### Uso de imágenes {#when-working-with-images}

The [!UICONTROL Dynamic Media] component lets you add dynamic images, including image sets, spin sets, and mixed media sets. Puede acercar, alejar y, si procede, girar una imagen en un conjunto de giros o seleccionar una imagen de otro tipo de conjunto.

También puede configurar el ajuste preestablecido de visor, el ajuste preestablecido de imagen o el formato de imagen directamente en el componente. Para hacer que en una imagen sea interactiva, puede establecer puntos de interrupción o aplicar un ajuste preestablecido de imagen interactiva.

![chlimage_1-72](assets/chlimage_1-72a.png)

You can edit the following Dynamic Media settings by clicking **[!UICONTROL Edit]** in the component and then clicking the **[!UICONTROL Dynamic Media Settings]** tab.

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>De forma predeterminada, el componente de imagen de Dynamic Media es adaptable. If you want to make it a fixed size, set it in the component in the **[!UICONTROL Advanced]** tab with the **[!UICONTROL Width]** and **[!UICONTROL Height]** properties.

**[!UICONTROL Ajuste preestablecido]** de visor: seleccione un ajuste preestablecido de visor existente en el menú desplegable. Si el ajuste preestablecido de visor que busca no está visible, es posible que tenga que hacerlo visible. Consulte [Administración de ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md). No es posible seleccionar un ajuste preestablecido de visor si utiliza un ajuste preestablecido de imagen, y viceversa.

Esta es la única opción disponible al visualizar conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos. Los ajustes preestablecidos de visor que se muestran también son inteligentes; solo aparecen los ajustes preestablecidos de visor relevantes.

**[!UICONTROL Ajuste preestablecido]** de imagen: seleccione un ajuste preestablecido de imagen existente en el menú desplegable. Si el ajuste preestablecido de imagen que busca no está visible, es posible que tenga que hacerlo visible. Consulte [Administración de ajustes preestablecidos de imagen](/help/assets/managing-image-presets.md). No es posible seleccionar un ajuste preestablecido de visor si utiliza un ajuste preestablecido de imagen, y viceversa.

Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

**[!UICONTROL Modificadores]** de imagen: puede cambiar los efectos de imagen proporcionando comandos de imagen adicionales. These are described in [Managing Image Presets](/help/assets/managing-viewer-presets.md) and the [Command reference](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/http_ref/c_command_reference.html).

Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

**[!UICONTROL Puntos de interrupción]** : si utiliza este recurso en un sitio interactivo, debe agregar los puntos de interrupción de la página. Los puntos de interrupción de imagen deben separarse por comas (,). Esta opción funciona cuando no se ha definido ninguna altura o anchura en el ajuste preestablecido de una imagen.

Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

You can edit the following [!UICONTROL Advanced Settings] by clicking **[!UICONTROL Edit]** in the component.

**[!UICONTROL Título]** : cambie el título de la imagen.

**[!UICONTROL Texto]** alternativo: Agregue un título a la imagen para los usuarios que tienen gráficos desactivados.

Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

**[!UICONTROL URL, Abrir en]** : puede definir un recurso desde para abrir un vínculo. Set the **[!UICONTROL URL]** and **[!UICONTROL Open in]** to indicate whether you want it to open in the same window or a new window.

Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

**[!UICONTROL Anchura y altura]** : introduzca el valor en píxeles si desea que la imagen tenga un tamaño fijo. Si deja estos valores en blanco, hace que el recurso sea adaptable.

#### When working with video {#when-working-with-video}

Use the [!UICONTROL Dynamic Media] component to add dynamic video to your web pages. Cuando edita el componente, tiene la opción de usar un ajuste preestablecido de visor de vídeo predefinido para reproducir el vídeo en la página.

![chlimage_1-74](assets/chlimage_1-74a.png)

You can edit the following [!UICONTROL Dynamic Media Settings] by clicking **[!UICONTROL Edit]** in the component.

>[!NOTE]
>
>De forma predeterminada, el componente de vídeo de Dynamic Media es adaptable. If you want to make it a fixed size, set it in the component with the **[!UICONTROL Width]** and **[!UICONTROL Height]** in the **[!UICONTROL Advanced]** tab.

**[!UICONTROL Ajuste preestablecido]** de visor: seleccione un ajuste preestablecido de visor de vídeo existente en el menú desplegable. Si el ajuste preestablecido de visor que busca no está visible, es posible que tenga que hacerlo visible. Consulte [Administración de ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md). 

You can edit the following [!UICONTROL Advanced] settings by clicking **[!UICONTROL Edit]** in the component.

**[!UICONTROL Título]** : cambie el título del vídeo.

**[!UICONTROL Anchura y altura]** : introduzca el valor en píxeles si desea que el vídeo tenga un tamaño fijo. Si deja estos valores en blanco, hace que el vídeo sea adaptable.

#### Procedimiento para enviar vídeo seguro {#how-to-delivery-secure-video}

En AEM 6.2, cuando instala [FP-13480](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480), puede controlar si un vídeo se entrega sobre una conexión SSL segura (HTTPS) o una conexión no segura (HTTP). De manera predeterminada, el protocolo de envío de vídeo se hereda automáticamente del protocolo de la página web en el que se integra el vídeo. Si la página web se carga sobre HTTPS, el vídeo también se envía sobre HTTPS. Del mismo modo, si la página web se carga sobre HTTP, el vídeo se envía sobre HTTP. En la mayoría de los casos, el comportamiento predeterminado es adecuado y no hace falta realizar cambios en la configuración. Sin embargo, puede sustituir este comportamiento predeterminado si anexa `VideoPlayer.ssl=on` al final de una ruta de URL o a la lista de otros parámetros de configuración de visor en un fragmento de código integrado para forzar el envío de vídeo seguro.

Para obtener más información sobre el envío de vídeo seguro y el uso del atributo de configuración `VideoPlayer.ssl`   en la ruta de URL, consulte [Envío de vídeo seguro](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_video_viewer_20_securevideodelivery.html) en la Guía de referencia de visores. Además del visor de vídeo, la entrega de vídeo segura está disponible para el visor de medios mixtos y el visor de vídeo interactivo.

### Componente de Medios interactivos {#interactive-media-component}

El componente de Medios interactivos es para los recursos que tienen elementos interactivos integrados en ellos, como puntos interactivos o mapas de imágenes. Si tiene una imagen interactiva, un vídeo interactivo o un titular de carrusel, utilice el componente de **[!UICONTROL Medios interactivos]**.

The [!UICONTROL Interactive Media] component is smart – depending on whether you add an image or a video, you have various options. Además, el visor responde. Es decir, el tamaño de la pantalla cambia automáticamente en función del tamaño de la pantalla. Todos los visores son visores basados en HTML5.

![chlimage_1-75](assets/chlimage_1-75a.png)

Puede editar las siguientes opciones de configuración **[!UICONTROL General]** al hacer clic en **[!UICONTROL Editar]** en el componente.

**[!UICONTROL Ajuste preestablecido]** de visor: seleccione un ajuste preestablecido de visor existente en el menú desplegable. Si el ajuste preestablecido de visor que busca no está visible, es posible que tenga que hacerlo visible. Los ajustes preestablecidos de visor se deben publicar para que se puedan usar. Consulte Administración de ajustes preestablecidos de visor. 

**[!UICONTROL Título]** : cambie el título del vídeo.

**[!UICONTROL Anchura y altura]** : introduzca el valor en píxeles si desea que el vídeo tenga un tamaño fijo. Si deja estos valores en blanco, hace que el vídeo sea adaptable.

You can edit the following **[!UICONTROL Add To Cart** settings by clicking **[!UICONTROL Edit]** in the component.

**[!UICONTROL Mostrar recurso]** de producto: este valor está seleccionado de forma predeterminada. El recurso del producto muestra una imagen del producto, según se ha definido en el módulo Commerce. Desactive la casilla para no mostrar el recurso del producto.

**[!UICONTROL Mostrar precio]** del producto: este valor está seleccionado de forma predeterminada. El precio del producto muestra el precio del artículo, según se ha definido en el módulo Commerce. Desactive la casilla para no mostrar el precio del producto.

**[!UICONTROL Mostrar formulario]** de producto: de forma predeterminada, este valor no está seleccionado. En el formulario del producto se incluye las variantes de producto, como talla y color. Desactive la casilla para no mostrar las variantes del producto.
