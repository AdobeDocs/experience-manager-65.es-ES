---
title: Trabajo con Dynamic Media
description: Aprenda a utilizar Dynamic Media para distribuir recursos para consumo en sitios web, móviles y sociales.
uuid: 4dc0f436-d20e-4e8b-aeff-5515380fa44d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
discoiquuid: a8063d43-923a-42ac-9a16-0c7fadd8f73f
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 21%

---


# Trabajo con Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html) ayuda a proporcionar bajo demanda recursos de marketing y mercadotecnia de rico contenido visual, escalados automáticamente para el consumo en la Web, dispositivos móviles y redes sociales. Con un conjunto de recursos de origen principales, Dynamic Media genera y ofrece múltiples variaciones de contenido enriquecido en tiempo real a través de su red global, escalable y optimizada para el rendimiento.

Dynamic Media proporciona experiencias de visualización interactivas, que incluyen zoom, giro de 360 grados y vídeo. Dynamic Media introduce de forma exclusiva los flujos de trabajo de la solución de administración de recursos digitales (Recursos) de Adobe Experience Manager para simplificar y agilizar el proceso de administración de campañas digitales.

>[!NOTE]
>
>Hay un artículo de la comunidad disponible en [Uso de Adobe Experience Manager y Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html).

## Qué puede hacer con Dynamic Media {#what-you-can-do-with-dynamic-media}

Dynamic Media permite administrar los recursos antes de publicarlos. La forma de trabajar con los recursos en general se describe en detalle en [Uso de recursos digitales](manage-assets.md). Los temas generales incluyen la carga, descarga, edición y publicación de recursos; visualización y edición de propiedades y búsqueda de recursos.

Las funciones solo para Dynamic Media incluyen lo siguiente:

* [Banner de carrusel](carousel-banners.md)
* [Conjuntos de imágenes](image-sets.md)
* [Imágenes interactivas](interactive-images.md)
* [Vídeos interactivos](interactive-videos.md)
* [Conjuntos de medios mixtos](mixed-media-sets.md)
* [Imágenes panorámicas](panoramic-images.md)

* [Conjuntos de giros](spin-sets.md)
* [Vídeo](video.md)
* [Envío de recursos de Dynamic Media](delivering-dynamic-media-assets.md)
* [Administración de recursos](managing-assets.md)
* [Uso de las vistas rápidas para crear ventanas emergentes personalizadas](custom-pop-ups.md)

Consulte también [Configuración de Dynamic Media](administering-dynamic-media.md).

>[!NOTE]
>
>Para comprender las diferencias entre el uso de Dynamic Media y la integración de Dynamic Media Classic con AEM, consulte [Integración de Dynamic Media Classic en comparación con Dynamic Media](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media).

## Dynamic Media habilitado frente a Dynamic Media deshabilitado {#dynamic-media-on-versus-dynamic-media-off}

Puede saber si Dynamic Media está habilitado (activado) según las características siguientes:

* Las representaciones dinámicas están disponibles al descargar o previsualizar recursos.
* Hay disponibles conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos.
* Se crean representaciones PTIFF.

Al hacer clic en un recurso de imagen, la vista del recurso es diferente con Dynamic Media [enabled](config-dynamic.md#enabling-dynamic-media). Dynamic Media utiliza los visores HTML5 a petición.

### Representaciones dinámicas {#dynamic-renditions}

Las representaciones dinámicas, como los ajustes preestablecidos de imagen y visor (en **[!UICONTROL Dynamic]**), están disponibles cuando Dynamic Media está habilitado.

![chlimage_1-358](assets/chlimage_1-358.png)

### Conjuntos de imágenes, conjuntos de giros, conjuntos de medios mixtos {#image-sets-spins-sets-mixed-media-sets}

Los conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos están disponibles si Dynamic Media está activado.

![chlimage_1-359](assets/chlimage_1-359.png)

### Representaciones PTIFF {#ptiff-renditions}

Los recursos habilitados para Dynamic Media incluyen `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Cambio de vistas de recursos {#asset-views-change}

Con Dynamic Media habilitado, puede acercar y alejar haciendo clic en los botones `+` y `-`. También puede tocar o hacer clic para acercar cierta área. Revertir le lleva a la versión original y puede hacer que la imagen esté a pantalla completa haciendo clic en las flechas diagonales. Dynamic Media habilitado tiene este aspecto:

![chlimage_1-361](assets/chlimage_1-361.png)

Con Dynamic Media desactivado, puede acercar y alejar y volver al tamaño original:

![chlimage_1-362](assets/chlimage_1-362.png)
