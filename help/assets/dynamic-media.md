---
title: Trabajo con Dynamic Media
description: Aprenda a utilizar Dynamic Media para entregar recursos para su consumo en sitios web, móviles y sociales.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
role: User, Admin
exl-id: f8a80b22-b1a6-475f-b3f1-b2f47822f21d
feature: Collaboration,Asset Management
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 7%

---

# Uso de Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) ayuda a ofrecer recursos de marketing y comercialización visual enriquecidos bajo demanda, adaptados automáticamente para el consumo en sitios web, móviles y sociales. Con un conjunto de recursos de origen primarios, Dynamic Media genera y ofrece varias variaciones de contenido enriquecido en tiempo real a través de su red global, escalable y optimizada para el rendimiento.

Dynamic Media ofrece experiencias de visualización interactivas, como zoom, giro de 360 grados y vídeo. Dynamic Media incorpora de forma exclusiva los flujos de trabajo de la solución Adobe Experience Manager digital asset management (Assets) para simplificar y optimizar el proceso de administración de campañas digitales.

<!-- >ARTICLE IS MISSING. GIVES 404 [!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## Qué puede hacer con Dynamic Media {#what-you-can-do-with-dynamic-media}

Dynamic Media permite administrar los recursos antes de publicarlos. [Trabajar con recursos digitales](manage-assets.md) explica en detalle cómo usar recursos en general. Los temas generales incluyen cargar, descargar, editar y publicar recursos; ver y editar propiedades y buscar recursos.

Las funciones solo de Dynamic Media incluyen lo siguiente:

* [Banner de carrusel](carousel-banners.md)
* [Conjuntos de imágenes](image-sets.md)
* [Imágenes interactivas](interactive-images.md)
* [Vídeos interactivos](interactive-videos.md)
* [Conjuntos de medios mixtos](mixed-media-sets.md)
* [Imágenes panorámicas](panoramic-images.md)

* [Conjuntos de giros](spin-sets.md)
* [Vídeo](video.md)
* [Entrega de recursos de Dynamic Media](delivering-dynamic-media-assets.md)
* [Administración de recursos](managing-assets.md)
* [Creación de ventanas emergentes personalizadas con Quickview](custom-pop-ups.md)

Ver también [Configurar Dynamic Media](administering-dynamic-media.md).

>[!NOTE]
>
>Para comprender las diferencias entre usar Dynamic Media e integrar Dynamic Media Classic con Adobe Experience Manager, consulte [Integración de Dynamic Media Classic frente a Dynamic Media](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media).

## Dynamic Media habilitado frente a Dynamic Media deshabilitado {#dynamic-media-on-versus-dynamic-media-off}

Puede comprobar si Dynamic Media está habilitado (activado) por las siguientes características:

* Las representaciones dinámicas están disponibles al descargar o previsualizar recursos.
* Hay disponibles conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos.
* Se crean representaciones PTIFF.

Al seleccionar un recurso de imagen, la vista del recurso es diferente con Dynamic Media [habilitado](config-dynamic.md#enabling-dynamic-media). Dynamic Media utiliza los visores de HTML5 bajo demanda.

### Representaciones dinámicas {#dynamic-renditions}

Las representaciones dinámicas, como los ajustes preestablecidos de imagen y visor (en **[!UICONTROL Dynamic]**), están disponibles cuando Dynamic Media está habilitado.

![chlimage_1-358](assets/chlimage_1-358.png)

### Conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos {#image-sets-spins-sets-mixed-media-sets}

Los conjuntos de imágenes, los conjuntos de giros y los conjuntos de medios mixtos están disponibles si Dynamic Media está habilitado.

![chlimage_1-359](assets/chlimage_1-359.png)

### Representaciones PTIFF {#ptiff-renditions}

Los recursos habilitados para Dynamic Media incluyen `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Cambio de vistas de recursos {#asset-views-change}

Con Dynamic Media habilitado, puede acercar y alejar haciendo clic en los botones `+` y `-`. También puede hacer clic en para ampliar una zona concreta. Revertir le lleva a la versión original y puede hacer que la imagen de pantalla completa haciendo clic en las flechas diagonales. Dynamic Media habilitado tiene este aspecto:

![chlimage_1-361](assets/chlimage_1-361.png)

Con Dynamic Media deshabilitado, puede aumentar y reducir el tamaño y volver al original:

![chlimage_1-362](assets/chlimage_1-362.png)
