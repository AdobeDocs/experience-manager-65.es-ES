---
title: Agregar recursos de Dynamic Media a las páginas
description: Para añadir la funcionalidad de Dynamic Media a los recursos que utilice en sus sitios web, puede añadir el componente Dynamic Media o Medios interactivos directamente en la página.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: d2ebfca5-19f9-4fa5-b142-b978f46a912f
source-git-commit: 1349d9929fc64ad46fc91f0d189bab54cca9de81
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 32%

---

# Agregar recursos de Dynamic Media a las páginas{#adding-dynamic-media-assets-to-pages}

Para añadir la funcionalidad de Dynamic Media a los recursos que utilice en sus sitios web, puede añadir el componente **[!UICONTROL Dynamic Media]** o **[!UICONTROL Interactive Media]** directamente en la página. Introduzca el modo **[!UICONTROL Design]** y habilite los componentes de Dynamic Media. A continuación, puede añadir estos componentes a la página y añadir recursos al componente. Los componentes Dynamic Media y los medios interactivos son inteligentes: saben si va a añadir una imagen o un vídeo y las opciones disponibles cambian en consecuencia.

Los recursos de Dynamic Media se agregan directamente a la página si utiliza Adobe Experience Manager como WCM.

>[!NOTE]
>
>Para los titulares de carrusel, hay mapas de imágenes disponibles de fábrica.

## Adición de un componente Dynamic Media a una página {#adding-a-dynamic-media-component-to-a-page}

Añadir el componente [!UICONTROL Dynamic Media] o [!UICONTROL Medios interactivos] a una página es lo mismo que añadir un componente a cualquier página. Los componentes [!UICONTROL Dynamic Media] y [!UICONTROL Interactive Media] se describen detalladamente en las secciones siguientes.

Para añadir un componente o visor de Dynamic Media a una página:

1. En el Experience Manager, abra la página a la que desee añadir el componente Dynamic Media.
1. Si no hay ningún componente de Dynamic Media disponible, haga clic en la regla de la [!UICONTROL Barra de tareas] para entrar en el modo **[!UICONTROL Diseño]**, haga clic en **[!UICONTROL Editar]** parsys y seleccione **[!UICONTROL Dynamic Media]** para que los componentes de Dynamic Media estén disponibles.

   >[!NOTE]
   >
   >Consulte [Configuración de componentes en el modo Diseño](/help/sites-authoring/default-components-designmode.md) para obtener más información.

1. Vuelva al modo **[!UICONTROL Editar]** haciendo clic en el icono de lápiz de la [!UICONTROL Barra de tareas].
1. Arrastre el componente **[!UICONTROL Dynamic Media]** o **[!UICONTROL Medios interactivos]** del grupo **[!UICONTROL Otro]** de la barra de tareas a la página en la ubicación deseada.
1. Haga clic en **[!UICONTROL Editar]** para que se abra el componente.
1. [](#dynamic-media-component)Edite el componente según sea necesario y haga clic en **[!UICONTROL Aceptar]** para guardar los cambios.

## Componentes de Dynamic Media {#dynamic-media-components}

[!UICONTROL Dynamic Media ] y  [!UICONTROL Medios interactivos ] están disponibles en   Sidekickunder  **[!UICONTROL Dynamic Media]**. El componente de **[!UICONTROL Medios interactivos]** se utiliza para cualquier recurso interactivo, como vídeo interactivo, imágenes interactivas o conjuntos de carrusel. Para todos los demás componentes de Dynamic Media, utilice el componente **[!UICONTROL Dynamic Media]**.

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>Estos componentes no están disponibles de forma predeterminada y deben seleccionarse en el modo Diseño antes de utilizarlos. [Una vez que estén disponibles en el modo](/help/sites-authoring/default-components-designmode.md) de diseño, puede añadir los componentes a la página como lo haría con cualquier otro componente de Experience Manager.

### Componente de Dynamic Media {#dynamic-media-component}

El componente Dynamic Media es inteligente: en función de si se añade una imagen o un vídeo, hay varias opciones. El componente admite ajustes preestablecidos de imagen, visores basados en imágenes, como conjuntos de imágenes, conjuntos de giros, conjuntos de medios mixtos y vídeo. Además, el visor es interactivo. Es decir, el tamaño de la pantalla cambia automáticamente según el tamaño de la pantalla. Todos los visores son visores basados en HTML5.

>[!NOTE]
>
>Cuando agregue el componente [!UICONTROL Dynamic Media] y **[!UICONTROL Configuración de Dynamic Media]** esté en blanco o no pueda agregar un recurso correctamente, compruebe lo siguiente:
>
>* [Dynamic Media](/help/assets/config-dynamic.md) se ha activado. Dynamic Media está desactivado de forma predeterminada.
>* La imagen tiene un archivo TIFF piramidal. Las imágenes importadas antes de que Dynamic Media esté habilitado no tienen un archivo tiff piramidal.

>



#### Uso de imágenes {#when-working-with-images}

El componente [!UICONTROL Dynamic Media] permite agregar imágenes dinámicas, incluidos conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos. Puede acercar, alejar y, si procede, girar una imagen en un conjunto de giros o seleccionar una imagen de otro tipo de conjunto.

También puede configurar el ajuste preestablecido de visor, el ajuste preestablecido de imagen o el formato de imagen directamente en el componente. Para que una imagen sea interactiva, puede establecer puntos de interrupción o aplicar un ajuste preestablecido de imagen interactiva.

![chlimage_1-72](assets/chlimage_1-72a.png)

Puede editar las siguientes configuraciones de Dynamic Media haciendo clic en **[!UICONTROL Editar]** en el componente y luego en la pestaña **[!UICONTROL Configuración de Dynamic Media]**.

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>De forma predeterminada, el componente de imagen Dynamic Media es adaptable. Si desea que tenga un tamaño fijo, configúrelo en el componente de la pestaña **[!UICONTROL Avanzado]** con las propiedades **[!UICONTROL Width]** y **[!UICONTROL Height]**.

**[!UICONTROL Ajuste preestablecido de visualizador]** : seleccione un ajuste preestablecido de visualizador existente en el menú desplegable. Si el ajuste preestablecido de visualizador que está buscando no está visible, debe hacerlo visible. Consulte [Administración de ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md). No se puede seleccionar un ajuste preestablecido de visualizador si se utiliza un ajuste preestablecido de imagen y, a la inversa,

Esta opción solo está disponible si se ven conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos. Los ajustes preestablecidos de visor que se muestran son inteligentes. Es decir, solo aparecen los ajustes preestablecidos de visualizador relevantes.

**[!UICONTROL Ajuste preestablecido de imagen]** : seleccione un ajuste preestablecido de imagen existente en el menú desplegable. Si el ajuste preestablecido de imagen que está buscando no está visible, debe hacerlo visible. Consulte [Administración de ajustes preestablecidos de imagen](/help/assets/managing-image-presets.md). No se puede seleccionar un ajuste preestablecido de visualizador si se utiliza un ajuste preestablecido de imagen y, a la inversa,

Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

**[!UICONTROL Modificadores de imagen]** : puede cambiar los efectos de imagen suministrando comandos de imagen adicionales. Estos comandos se describen en [Administración de ajustes preestablecidos de imagen](/help/assets/managing-viewer-presets.md) y en la [Referencia de comandos](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

**[!UICONTROL Puntos de interrupción]** : si utiliza este recurso en un sitio interactivo, debe agregar los puntos de interrupción de la página. Los puntos de interrupción de la imagen están separados por comas (,). Esta opción funciona cuando no se ha definido ninguna altura o anchura en el ajuste preestablecido de una imagen.

Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

Puede editar la siguiente [!UICONTROL Configuración avanzada] haciendo clic en **[!UICONTROL Editar]** en el componente.

**[!UICONTROL Título]** : cambie el título de la imagen.

**[!UICONTROL Texto alternativo]** : agregue un título a la imagen para los usuarios que tengan los gráficos desactivados.

Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

**[!UICONTROL URL, Abrir en]** : puede configurar un recurso de para abrir un vínculo. Configure las **[!UICONTROL URL]** y **[!UICONTROL Abrir en]** para indicar si desea que se abra en la misma ventana o en una nueva ventana.

Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

**[!UICONTROL Anchura y altura]** : introduzca el valor en píxeles si desea que la imagen tenga un tamaño fijo. Si deja estos valores en blanco, hace que el recurso sea adaptable.

#### Al trabajar con vídeo {#when-working-with-video}

Utilice el componente **[!UICONTROL Dynamic Media]** para añadir vídeo dinámico a las páginas web. Al editar el componente, puede elegir utilizar un ajuste preestablecido de visualizador de vídeo predefinido para reproducir el vídeo en la página.

![chlimage_1-74](assets/chlimage_1-74a.png)

Puede editar la siguiente [!UICONTROL Configuración de Dynamic Media] haciendo clic en **[!UICONTROL Editar]** en el componente.

>[!NOTE]
>
>De forma predeterminada, el componente de vídeo de Dynamic Media es adaptable. Si desea que tenga un tamaño fijo, configúrelo en el componente con la **[!UICONTROL Anchura]** y **[!UICONTROL Altura]** en la pestaña **[!UICONTROL Avanzado]**.

**[!UICONTROL Ajuste preestablecido de visualizador]** : seleccione un ajuste preestablecido de visualizador de vídeo existente en el menú desplegable. Si el ajuste preestablecido de visualizador que está buscando no está visible, debe hacerlo visible. Consulte [Administración de ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md). 

Puede editar las siguientes opciones de configuración [!UICONTROL Advanced] haciendo clic en **[!UICONTROL Editar]** en el componente.

**[!UICONTROL Título]** : cambie el título del vídeo.

**[!UICONTROL Anchura y altura]** : introduzca el valor en píxeles si desea que el vídeo tenga un tamaño fijo. Si deja estos valores en blanco, hace que el vídeo sea adaptable.

#### Procedimiento para enviar vídeo seguro {#how-to-delivery-secure-video}

En el Experience Manager 6.2, al instalar [FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480), puede controlar si un vídeo se entrega a través de una conexión SSL segura (HTTPS) o una conexión no segura (HTTP). De manera predeterminada, el protocolo de envío de vídeo se hereda automáticamente del protocolo de la página web en el que se integra el vídeo. Si la página web se carga sobre HTTPS, el vídeo también se envía sobre HTTPS. Por el contrario, si la página web está en HTTP, el vídeo se envía a través de HTTP. Normalmente, este comportamiento predeterminado es correcto y no es necesario realizar ningún cambio en la configuración. Sin embargo, puede anular este comportamiento predeterminado. Anexe `VideoPlayer.ssl=on` al final de una ruta de URL o a la lista de otros parámetros de configuración del visor en un fragmento de código incrustado. Cualquier acción fuerza la entrega segura de vídeo.

Para obtener más información sobre el envío de vídeo seguro y el uso del atributo de configuración `VideoPlayer.ssl`   en la ruta de URL, consulte [Envío de vídeo seguro](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html) en la Guía de referencia de visores. Además del visor de vídeo, el envío de vídeo seguro está disponible para el visor de medios mixtos y el visor de vídeo interactivo.

### Componente de Medios interactivos {#interactive-media-component}

El componente de Medios interactivos es para los recursos que tienen elementos interactivos integrados en ellos, como puntos interactivos o mapas de imágenes. Si tiene una imagen interactiva, un vídeo interactivo o un titular de carrusel, utilice el componente de **[!UICONTROL Medios interactivos]**.

El componente [!UICONTROL Medios interactivos] es inteligente, ya que, dependiendo de si agrega una imagen o un vídeo, dispone de varias opciones. Además, el visor es interactivo. Es decir, el tamaño de la pantalla cambia automáticamente según el tamaño de la pantalla. Todos los visores son visores basados en HTML5.

![chlimage_1-75](assets/chlimage_1-75a.png)

Puede editar las siguientes opciones de configuración **[!UICONTROL General]** al hacer clic en **[!UICONTROL Editar]** en el componente.

**[!UICONTROL Ajuste preestablecido de visualizador]** : seleccione un ajuste preestablecido de visualizador existente en el menú desplegable. Si el ajuste preestablecido de visualizador que está buscando no está visible, debe hacerlo visible. Los ajustes preestablecidos de visor se deben publicar para que se puedan usar. Consulte [Administración de ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md). 

**[!UICONTROL Título]** : cambie el título del vídeo.

**[!UICONTROL Anchura y altura]** : introduzca el valor en píxeles si desea que el vídeo tenga un tamaño fijo. Si deja estos valores en blanco, hace que el vídeo sea adaptable.

Puede editar las siguientes opciones de configuración **[!UICONTROL Añadir a carro]** al hacer clic en **[!UICONTROL Editar]** en el componente.

**[!UICONTROL Mostrar recurso de producto]** : de forma predeterminada, este valor está seleccionado. El recurso del producto muestra una imagen del producto, según se ha definido en el módulo Commerce. Desactive la casilla para no mostrar el recurso del producto.

**[!UICONTROL Mostrar precio del producto]** : de forma predeterminada, se selecciona este valor. El precio del producto muestra el precio del artículo, según se ha definido en el módulo Commerce. Desactive la casilla para no mostrar el precio del producto.

**[!UICONTROL Mostrar formulario de producto]** : de forma predeterminada, este valor no está seleccionado. En el formulario del producto se incluye las variantes de producto, como talla y color. Desactive la casilla para no mostrar las variantes del producto.
