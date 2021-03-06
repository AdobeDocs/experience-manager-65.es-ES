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
feature: Imágenes panorámicas,Administración de activos
role: User, Admin
exl-id: 4d6fbeb1-94db-4154-9e41-b76033fb4398
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Imágenes panorámicas{#panoramic-images}

En esta sección se describe cómo trabajar con el visor de imágenes panorámicas para representar imágenes panorámicas esféricas y así obtener una experiencia de visualización de 360° inmersiva de una habitación, propiedad, ubicación o paisaje.

Consulte también [Administrar ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md).

![imagen panorámica2](assets/panoramic-image2.png)

## Cargar recursos para utilizarlos con el visor de imágenes panorámicas {#uploading-assets-for-use-with-the-panoramic-image-viewer}

Para que un recurso cargado pueda considerarse una imagen panorámica esférica que pretenda usar con el visor de imágenes panorámicas, el recurso debe tener una o ambas de las siguientes opciones:

* Una relación de aspecto de 2.
Puede anular la configuración predeterminada de relación de aspecto de 2 en CRXDE Lite de la siguiente manera:
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* Etiquetado con las palabras clave `equirectangular`, o `spherical`y `panorama`, o `spherical` y `panoramic`. Consulte [Uso de etiquetas](/help/sites-authoring/tags.md).

Tanto la proporción de aspecto como los criterios de palabra clave se aplican a los recursos panorámicos para la página de detalles del recurso y el componente WCM `Panoramic Media`.

Para cargar recursos para usarlos con el visor de imágenes panorámicas, consulte [Cargar recursos](/help/assets/manage-assets.md#uploading-assets).

## Configuración de Dynamic Media Classic {#configuring-dynamic-media-classic-scene}

Para que el visor de imágenes panorámicas funcione correctamente en Adobe Experience Manager, sincronice los ajustes preestablecidos del visor de imágenes panorámicas con los metadatos específicos de Dynamic Media Classic y Dynamic Media Classic para que los ajustes preestablecidos del visor se actualicen en el JCR. Para realizar esta sincronización, configure Dynamic Media Classic de la siguiente manera:

1. Abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e inicie sesión en su cuenta.

1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración de publicación]** > **[!UICONTROL Servidor de imágenes]**.
1. En la página Publicación del servidor de imágenes , en el menú desplegable **[!UICONTROL Publicar contexto]** cerca de la parte superior, seleccione **[!UICONTROL Servicio de imágenes]**.

1. En la misma página Publicación del servidor de imágenes, busque el encabezado **[!UICONTROL Atributos de solicitud]**.
1. En el encabezado Atributos de solicitud, busque **[!UICONTROL Límite de tamaño de imagen de respuesta]**. A continuación, en los campos de anchura y altura asociados, aumente el tamaño máximo permitido de imagen para imágenes panorámicas.

   Dynamic Media Classic tiene un límite de 25 000 000 píxeles. El tamaño máximo permitido para imágenes con una proporción de aspecto de 2:1 es de 7000 x 3500. Sin embargo, para las pantallas de escritorio típicas, 4096 x 2048 píxeles es suficiente.

   >[!NOTE]
   >
   >Solo se admiten las imágenes que se encuentran dentro del tamaño máximo permitido de imagen. Las solicitudes de imágenes que están por encima del límite de tamaño dan como resultado una respuesta 403.

1. En el encabezado Atributos de solicitud , haga lo siguiente:

   * Establezca el modo de ofuscación de solicitud en **[!UICONTROL Deshabilitado]**.
   * Establezca el modo de bloqueo de solicitud en **[!UICONTROL Deshabilitado]**.

   Estos ajustes son necesarios para utilizar el componente WCM `Panoramic Media` en el Experience Manager.

1. En la parte inferior de la página Publicación del servidor de imágenes, en la parte izquierda, seleccione **[!UICONTROL Guardar]**.

1. En la esquina inferior derecha, seleccione **[!UICONTROL Cerrar]**.

### Solución de problemas del componente WCM de medios panorámicos {#troubleshooting-the-panoramic-media-wcm-component}

Si ha colocado una imagen en el componente de medios panorámicos de su WCM y el marcador de posición del componente se ha contraído, solucione los problemas siguientes:

* Si se produce un error de 403 prohibido, puede deberse a que el tamaño de la imagen solicitada sea demasiado grande. Revise la configuración de **[!UICONTROL Reply Image Size Limit]** en [Configurar Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

* Para obtener un &quot;Bloqueo no válido&quot; en el recurso o un &quot;Error de análisis&quot; mostrado en la página, marque Modo de ofuscación de solicitudes y Modo de bloqueo de solicitudes para asegurarse de que están desactivados.
* En caso de error de lienzo contaminado, configure una Ruta de archivo de definición de conjunto de reglas e Invalidar CTN para las solicitudes anteriores del recurso de imagen.
* Si la calidad de la imagen es baja después de una solicitud de imagen con un tamaño superior al límite admitido, compruebe que la configuración **[!UICONTROL JPEG Encoding Attributes > Quality]** no esté vacía. Una configuración típica para el campo **[!UICONTROL Quality]** es `95`. Puede encontrar la configuración en la página Publicación del servidor de imágenes . Para acceder a la página, consulte [Configuración de Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

## Vista previa de imágenes panorámicas {#previewing-panoramic-images}

Consulte [Vista previa de recursos](/help/assets/previewing-assets.md).

## Publicar imágenes panorámicas {#publishing-panoramic-images}

Consulte [Publicar recursos](/help/assets/publishing-dynamicmedia-assets.md).
