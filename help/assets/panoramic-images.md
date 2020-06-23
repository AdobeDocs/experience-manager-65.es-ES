---
title: Imágenes panorámicas
description: Aprenda a trabajar con imágenes panorámicas en Dynamic Media.
uuid: ced3e5bd-93c8-4d5f-a397-1380d4d0a5e7
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 632a9074-b747-49a1-a57d-1f42bba1f4e9
docset: aem65
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 0%

---


# Panoramic images{#panoramic-images}

En esta sección se describe cómo trabajar con el visor de imágenes panorámicas para procesar imágenes panorámicas esféricas y así disfrutar de una experiencia de visualización inmersiva de 360° de una habitación, propiedad, ubicación o paisaje.

See also [Managing Viewer Presets](/help/assets/managing-viewer-presets.md).

![panoramic-image2](assets/panoramic-image2.png)

## Carga de recursos para su uso con el visor de imágenes panorámicas {#uploading-assets-for-use-with-the-panoramic-image-viewer}

Para que un recurso cargado se considere una imagen panorámica esférica que se va a utilizar con el visor de imágenes panorámicas, el recurso debe tener una o ambas de las opciones siguientes:

* Proporción de aspecto de 2.
En CRXDE Lite puede anular la configuración de proporción de aspecto predeterminada de 2 en:
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* Etiquetado con las palabras clave `equirectangular`, o `spherical`y `panorama`, o `spherical` y `panoramic`. Consulte [Uso de etiquetas](/help/sites-authoring/tags.md).

Both the aspect ratio and keyword criteria apply to panoramic assets for the asset details page and the `Panoramic Media` WCM component.

Para cargar recursos para utilizarlos con el visor de imágenes panorámicas, consulte [Carga de recursos](/help/assets/managing-assets-touch-ui.md#uploading-assets).

## Configuración de Dynamic Media Classic (Scene7) {#configuring-dynamic-media-classic-scene}

Para que el visor de imágenes panorámicas funcione correctamente en AEM, debe sincronizar los ajustes preestablecidos de visor de imágenes panorámicas con metadatos específicos de Dynamic Media Classic (Scene7) y Dynamic Media Classic (Scene7) para que los ajustes preestablecidos de visor se actualicen en el JCR. Para ello, configure Dynamic Media Classic (Scene7) de la siguiente manera:

1. [Inicie sesión en la instancia de Dynamic Media Classic (Scene7)](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) para cada cuenta de compañía.

1. Cerca de la esquina superior derecha de la página, haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Ajustes de publicación > Servidor de imágenes.]**
1. En la página Publicación del servidor de imágenes, en el menú desplegable **[!UICONTROL Publicar contexto]** cerca de la parte superior, seleccione Servicio **[!UICONTROL de imágenes.]**

1. En la misma página de publicación de Image Server, busque el encabezado Atributos de **[!UICONTROL solicitud.]**
1. En el encabezado Atributos de solicitud, busque Límite de tamaño de imagen de **[!UICONTROL respuesta.]** A continuación, en los campos de anchura y altura asociados, aumente el tamaño máximo permitido de imagen para las imágenes panorámicas.

   Dynamic Media Classic (Scene7) tiene un límite de 25.000.000 píxeles. El tamaño máximo permitido para imágenes con una proporción de aspecto de 2:1 es de 7000 x 3500. Sin embargo, para las pantallas de escritorio típicas, 4096 x 2048 píxeles es suficiente.

   >[!NOTE]
   >
   >Solo se admiten las imágenes que alcanzan el tamaño máximo permitido de imagen. Las solicitudes de imágenes que superen el límite de tamaño darán como resultado una respuesta de 403.

1. En el encabezado Atributos de solicitud, haga lo siguiente:

   * Establezca el modo de confusión de solicitudes en **[!UICONTROL Deshabilitado.]**
   * Establezca el modo de bloqueo de solicitudes en **[!UICONTROL Deshabilitado.]**

   Esta configuración es necesaria para utilizar el componente `Panoramic Media` WCM en AEM.

1. En la parte inferior de la página Servidor de imágenes, en la parte izquierda, haga clic en **[!UICONTROL Guardar.]**

1. En la esquina inferior derecha, haga clic en **[!UICONTROL Cerrar.]**

### Resolución de problemas del componente WCM de medios panorámicos {#troubleshooting-the-panoramic-media-wcm-component}

Si ha colocado una imagen en el componente de medios panorámicos de WCM y el marcador de posición del componente se ha contraído, es posible que desee solucionar los problemas siguientes:

* Si se produce un error 403 Prohibido, es posible que el tamaño de la imagen solicitada sea demasiado grande. Revise la configuración de Límite **[!UICONTROL de tamaño de imagen de]** respuesta en [Configuración de Dynamic Media Classic (Scene7)](/help/assets/panoramic-images.md#configuring%20dynamic%20media%20classic%20(scene7)).

* Para ver un &quot;bloqueo no válido&quot; en el recurso o &quot;error de análisis&quot; en la página, marque el modo de confusión de solicitudes y el modo de bloqueo de solicitudes para asegurarse de que están desactivados.
* Si se produce un error de lienzo contaminado, configure una ruta de archivo de definición de conjunto de reglas e Invalide CTN para las solicitudes anteriores del recurso de imagen.
* Si la calidad de la imagen es muy baja después de una solicitud de imagen con un tamaño superior al límite admitido, compruebe que el ajuste Atributos de codificación **[!UICONTROL JPEG > Calidad]** no esté vacío. Una configuración típica del campo **[!UICONTROL Calidad]** es `95`. La configuración se encuentra en la página Servidor de imágenes. Para acceder a la página, consulte [Configuración de Dynamic Media Classic (Scene7)](/help/assets/panoramic-images.md#configuring%20dynamic%20media%20classic%20(scene7)).

## Vista previa de imágenes panorámicas {#previewing-panoramic-images}

Consulte [Vista previa de recursos](/help/assets/previewing-assets.md).

## Publicación de imágenes panorámicas {#publishing-panoramic-images}

Consulte [Publicación de recursos](/help/assets/publishing-dynamicmedia-assets.md).
