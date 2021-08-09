---
title: Conjuntos de medios mixtos
description: Aprenda a trabajar con conjuntos de medios mixtos en Dynamic Media
uuid: cecad772-ed05-46f6-ba44-107195866b0d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ed84157a-e6b4-4dde-af2e-a1e0b6259628
docset: aem65
feature: Conjuntos de medios mixtos,Administración de recursos
role: User, Admin
exl-id: 70a72fb9-a289-4eda-abcc-300edf9f1961
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '1464'
ht-degree: 17%

---

# Conjuntos de medios mixtos{#mixed-media-sets}

Los conjuntos de medios mixtos permiten proporcionar una combinación de imágenes, conjuntos de imágenes, conjuntos de giros y vídeos en una presentación.

Los conjuntos de medios mixtos se designan mediante un banner con la palabra **[!UICONTROL MixedMediaSet]**. Además, si se publica el conjunto de medios mixtos, se muestra la fecha de publicación, indicada por el icono **[!UICONTROL Mundo]**, junto a la fecha de la última modificación, indicada por el icono **[!UICONTROL Lápiz]**.

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>Para obtener información sobre la interfaz de usuario de Assets, consulte [Administrar recursos](/help/assets/manage-assets.md).

## Inicio rápido: Conjuntos de medios mixtos {#quick-start-mixed-media-sets}

Para poner en marcha rápidamente los conjuntos de medios mixtos, siga estos pasos:

1. [Cargue los recursos](#uploading-assets).

   Comience por cargar las imágenes y los vídeos de los conjuntos de medios mixtos. Si es necesario, cree los [conjuntos de imágenes](/help/assets/image-sets.md) y los [conjuntos de giros](/help/assets/spin-sets.md). Dado que los usuarios pueden hacer zoom en las imágenes en el visualizador de conjuntos de medios mixtos, elija las imágenes con cuidado. Compruebe que las imágenes tengan al menos 2000 píxeles en la dimensión más grande.

1. [Crear conjuntos de medios mixtos](#creating-mixed-media-sets).

   Para crear un conjunto de medios mixtos, en la página Recursos, seleccione **[!UICONTROL Crear]** > **[!UICONTROL Conjunto de medios mixtos]** y, a continuación, asigne un nombre al conjunto, elija los recursos y elija el orden en que aparecen las imágenes.

   Consulte [Trabajar con selectores](/help/assets/working-with-selectors.md).

1. Configure los [ajustes preestablecidos del visualizador de medios mixtos](/help/assets/managing-viewer-presets.md) según sea necesario.

   Los administradores pueden crear o modificar ajustes preestablecidos del visualizador de conjuntos de medios mixtos. Para ver los medios mixtos con un ajuste preestablecido del visualizador, seleccione el conjunto de medios mixtos y, en el menú desplegable del carril izquierdo, seleccione **[!UICONTROL Visualizadores]**.

   Para crear o editar ajustes preestablecidos de visualizador, consulte **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Ajustes preestablecidos de visualizador]**.

   Consulte [Agregar y editar ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md).

1. [Vista previa de conjuntos de medios mixtos](#previewing-mixed-media-sets).

   Seleccione el conjunto de medios mixtos y podrá previsualizarlo. Seleccione los iconos de miniaturas para que pueda examinar el conjunto de medios mixtos en el visualizador seleccionado. Puede elegir diferentes visores desde el menú **[!UICONTROL Visualizadores]**, disponible en el menú desplegable del carril izquierdo.

1. [Publicar conjuntos de medios mixtos](#publishing-mixed-media-sets).

   Al publicar un conjunto de medios mixtos, se activa la dirección URL y la cadena de incrustación. Además, debe [publicar el ajuste preestablecido de visor](/help/assets/managing-viewer-presets.md#publishing-viewer-presets).

1. [Vincule las URL a su ](/help/assets/linking-urls-to-yourwebapplication.md) aplicación web o  [incruste el visualizador de imágenes o vídeos](/help/assets/embed-code.md).

   Adobe Experience Manager Assets crea llamadas URL para conjuntos de medios mixtos y los activa después de publicar los conjuntos de medios mixtos. Puede copiar estas direcciones URL cuando obtiene una vista previa de los recursos. También puede incrustarlos en el sitio web.

   Seleccione el conjunto de medios mixtos y, a continuación, en el menú desplegable del carril izquierdo, seleccione **[!UICONTROL Visualizadores]**.

   Consulte [Vincular un conjunto de medios mixtos a una página web](/help/assets/linking-urls-to-yourwebapplication.md) e [Incrustar el visualizador de imágenes o vídeos](/help/assets/embed-code.md).

Si es necesario, puede editar [Conjuntos de medios mixtos](#editing-mixed-media-sets). Además, puede ver y modificar [Propiedades de conjuntos de medios mixtos](/help/assets/manage-assets.md#editing-properties).

>[!NOTE]
>
>Si tiene problemas al crear conjuntos, consulte [Resolución de problemas de Dynamic Media - modo Scene7](/help/assets/troubleshoot-dms7.md).

## Cargar recursos {#uploading-assets}

Comience por cargar las imágenes y los vídeos de los conjuntos de medios mixtos. Dado que los usuarios pueden hacer zoom en las imágenes en el visualizador de conjuntos de medios mixtos, elija las imágenes con cuidado. Compruebe que las imágenes tengan al menos 2000 píxeles en la dimensión más grande.

Además, si desea agregar conjuntos de giros o conjuntos de imágenes al conjunto de medios mixtos, cree también esos conjuntos.

## Crear un conjunto de medios mixtos {#creating-mixed-media-sets}

Puede agregar imágenes, conjuntos de imágenes, conjuntos de giros y vídeos al conjunto de medios mixtos. Asegúrese de que los archivos, conjuntos de imágenes y conjuntos de giros estén listos para publicarse antes de agregarlos al conjunto de medios mixtos.

Cuando se añaden recursos al conjunto, estos se añaden automáticamente en orden alfanumérico. Puede reordenar u ordenar manualmente los recursos una vez añadidos.

**Para crear un conjunto de medios mixtos:**

1. En Assets, desplácese hasta donde desee crear un conjunto de medios mixtos, seleccione **[!UICONTROL Crear]** y seleccione **[!UICONTROL Conjunto de medios mixtos]**. También puede crear el conjunto desde una carpeta que contenga los recursos. Se muestra el Editor de conjuntos de medios mixtos.

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. En el Editor de conjuntos de medios mixtos, en **[!UICONTROL Título]**, introduzca un nombre para el conjunto de medios mixtos. El nombre aparece en el banner del conjunto de medios mixtos. De forma opcional, introduzca una descripción.

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >Al crear el conjunto de medios mixtos, puede cambiar la miniatura del conjunto de medios mixtos o permitir que el Experience Manager seleccione la miniatura automáticamente en función de los recursos del conjunto de medios mixtos. Para seleccionar una miniatura, seleccione **[!UICONTROL Cambiar miniatura]** y seleccione cualquier imagen (también puede navegar a otras carpetas para buscar imágenes). Si ha seleccionado una miniatura y, a continuación, decide que desea que el Experience Manager genere una del conjunto de medios mixtos, seleccione **[!UICONTROL Cambiar a miniatura automática]**.

1. Seleccione el Selector de recursos para que pueda seleccionar los recursos que desea incluir en su conjunto de medios mixtos. Selecciónelos y luego seleccione **[!UICONTROL Select]**.

   Con el Selector de recursos, puede buscar recursos escribiendo una palabra clave y pulsando **[!UICONTROL Retorno]**. También puede aplicar filtros para restringir los resultados de búsqueda. Puede filtrar por ruta, colección, tipo de archivo y etiqueta. Seleccione el filtro y, a continuación, seleccione el icono **[!UICONTROL Filter]** en la barra de herramientas. Para cambiar la vista, seleccione el icono **[!UICONTROL Ver]** y seleccione **[!UICONTROL Vista de lista]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de tarjeta]**.

   Consulte [Trabajar con selectores](/help/assets/working-with-selectors.md).

   ![chlimage_1-140](assets/chlimage_1-383.png)

1. Reordene los recursos arrastrándolos hacia arriba o hacia abajo en la lista (debe seleccionar el icono **[!UICONTROL Reordenar]**), según sea necesario.

   ![chlimage_1-141](assets/chlimage_1-352.png)

   Si desea agregar miniaturas, seleccione el icono **+** **[!UICONTROL miniatura]** situado junto a la imagen y vaya a la miniatura que desee. Cuando termine de seleccionar todas las imágenes en miniatura, seleccione **[!UICONTROL Guardar]**.

   >[!NOTE]
   >
   >Si desea agregar recursos, seleccione **[!UICONTROL Agregar recurso]**.

1. Para eliminar un recurso, seleccione la casilla de verificación correspondiente y seleccione **[!UICONTROL Eliminar recurso]**.
1. Para aplicar un ajuste preestablecido, seleccione **[!UICONTROL Ajuste preestablecido]** en la esquina superior derecha y seleccione un ajuste preestablecido para aplicar a los recursos.
1. Seleccione **[!UICONTROL Guardar]**. El conjunto de medios mixtos recién creado aparece en la carpeta en la que lo creó.

## Editar un conjunto de medios mixtos {#editing-mixed-media-sets}

Puede realizar varias tareas de edición en los recursos de los conjuntos de medios mixtos directamente en la interfaz de usuario [como lo haría con cualquier recurso de Assets](/help/assets/manage-assets.md). También puede realizar las siguientes acciones en conjuntos de medios mixtos:

* Agregue recursos al conjunto de medios mixtos.
* Reordenar recursos en el conjunto de medios mixtos.
* Eliminar recursos del conjunto de medios mixtos.
* Aplicar ajustes preestablecidos de visor.
* Cambie la miniatura predeterminada.

**Para editar un conjunto de medios mixtos:**

1. Realice una de las siguientes acciones:

   * Pase el ratón sobre un recurso de conjunto de medios mixtos y, a continuación, seleccione **[!UICONTROL Editar]** (icono de lápiz).
   * Pase el ratón sobre un recurso de conjunto de medios mixtos, seleccione **[!UICONTROL Seleccionar]** (icono de marca de verificación) y, a continuación, seleccione **[!UICONTROL Editar]** en la barra de herramientas.

   * Seleccione un recurso de conjunto de medios mixtos y, a continuación, seleccione **[!UICONTROL Editar]** (icono de lápiz) en la barra de herramientas.

1. En el Editor de conjuntos de medios mixtos, realice una de las acciones siguientes:

   * Para reordenar recursos: en el panel izquierdo, seleccione **[!UICONTROL Assets]** (icono de imagen) y arrastre un recurso a una nueva ubicación.
   * Para agregar recursos: en la barra de herramientas, seleccione **[!UICONTROL Agregar recurso]**. Vaya a los recursos. Para cada recurso que desee agregar, pase el ratón sobre la imagen del recurso (no el nombre del recurso) y, a continuación, seleccione el icono de marca de verificación. En la esquina superior derecha, seleccione **[!UICONTROL Seleccionar]**.

   * Para eliminar un recurso: en el panel izquierdo, seleccione **[!UICONTROL Assets]** (icono de imagen) y, a continuación, seleccione el recurso. En la barra de herramientas, seleccione **[!UICONTROL Eliminar recurso]**.

   * Para ordenar los recursos por su nombre en orden ascendente o descendente, en el panel izquierdo, seleccione **[!UICONTROL Assets]** (icono de imagen). A la derecha del encabezado **[!UICONTROL Assets]**, seleccione los iconos de acento circunflejo arriba o abajo.

      >[!NOTE]
      >
      >* Para eliminar un conjunto de medios mixtos completo, en cualquier modo de visualización (como **[!UICONTROL Vista de tarjeta]** o **[!UICONTROL Vista de columna]**) vaya al conjunto de medios mixtos. Pase el ratón sobre el recurso y seleccione el icono de marca de verificación para seleccionarlo. Pulse **[!UICONTROL Retroceso]** en el teclado o seleccione **[!UICONTROL Más]** (tres puntos) en la barra de herramientas y, a continuación, seleccione **[!UICONTROL Eliminar]**.
         >
         >
      * Para editar recursos en un conjunto de medios mixtos, vaya al conjunto y haga clic en **[!UICONTROL Definir miembros]** en el carril izquierdo. Seleccione el icono **[!UICONTROL Lápiz]** en un recurso individual para abrirlo en la ventana de edición.


1. Seleccione **[!UICONTROL Guardar]** cuando haya terminado de editar.

   >[!NOTE]
   >
   >* Para editar los recursos de un conjunto de medios mixtos, vaya al conjunto de medios mixtos. Pulse (no seleccione) el conjunto para que se abra en la página Vista previa del conjunto de Experience Manager . En el carril izquierdo, seleccione el circunflejo invertido para abrir la lista desplegable y, a continuación, seleccione **[!UICONTROL Definir miembros]**. En la página Definir miembros, pase el ratón sobre un recurso y, a continuación, seleccione **[!UICONTROL Editar]** (icono de lápiz) para abrir la página de edición.
      >
      >
   * Para eliminar un conjunto de medios mixtos completo, en cualquier modo de visualización (como la vista de tarjeta o la vista de columna), vaya al conjunto de medios mixtos. Pase el ratón sobre el conjunto y, a continuación, seleccione **Seleccionar** (icono de marca de verificación). Pulse **[!UICONTROL Retroceso]** en el teclado o seleccione **[!UICONTROL Más]** (fila de tres puntos) y, a continuación, seleccione **[!UICONTROL Eliminar]**.


## Vista previa de un conjunto de medios mixtos {#previewing-mixed-media-sets}

Consulte [Vista previa de recursos](/help/assets/previewing-assets.md) para obtener más información sobre cómo previsualizar conjuntos de medios mixtos.

## Publicar un conjunto de medios mixtos {#publishing-mixed-media-sets}

Consulte [Publicar recursos](/help/assets/publishing-dynamicmedia-assets.md) para obtener más información sobre cómo publicar conjuntos de medios mixtos.

>[!NOTE]
>
>Si el conjunto de medios mixtos no termina completamente en el servicio de envío la primera vez que lo publica, publique el conjunto de medios mixtos una segunda vez.
