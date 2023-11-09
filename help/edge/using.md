---
title: Uso de Edge Delivery Services
description: Uso de Edge Delivery Services (EDS)
exl-id: 6c9178b0-c8f3-4fc7-8614-8e71ffc2f0b8
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 93%

---

# Uso de Edge Delivery Services {#usingedge}

Con Edge Delivery, puede crear entornos de desarrollo rápidos en los que los autores pueden actualizar y publicar contenido rápidamente y en los que se pueden iniciar nuevos sitios rápidamente. Con este fin, puede trabajar con varias fuentes de contenido en el mismo sitio web y la publicación se realizará sin problemas y optimizada, independientemente de la fuente elegida. Como tal, tan solo se tarda un par de segundos en pasar de la edición a ver el contenido en directo en Internet.

## Creación {#authoring-edge}

Con Edge Delivery, la creación es fácil, rápida y flexible. Puede seguir dos rutas diferentes para la creación de contenido en el contexto de Edge Delivery Services:

* Creación basada en documentos (como Microsoft Word o Google Docs): [consulte este vínculo para obtener más información](https://www.hlx.live/docs/authoring).
* Editor de página/Editor universal: póngase en contacto con su representante de ventas de Adobe.

Si existe la creación basada en documentos, puede trabajar con una variedad de fuentes, como Microsoft Word y Google Docs. Los documentos de estas fuentes se convierten en páginas del sitio web. Encabezados, listas, imágenes, elementos de fuente, vídeos se pueden transferir desde la fuente inicial a su sitio web. Puede añadir metadatos con fines de SEO o utilizar bloques para trabajar con contenido estructurado y añadir funcionalidad.

## Publicación {#publishing-edge}

Con Edge Delivery, la publicación de contenido se realiza sin problemas independientemente de la fuente de contenido. El proceso es el siguiente: se utiliza la [extensión de barra de tareas](#using-sidekick) para activar el mecanismo de publicación y el contenido estará disponible en directo en el sitio web en un par de segundos.

## Edge Delivery Services y GitHub {#github-edge}

Edge Delivery utiliza GitHub para que los clientes puedan administrar e implementar código directamente desde su repositorio de GitHub. Por ejemplo, puede escribir contenido en Google Docs o Microsoft Word y desarrollar la funcionalidad del sitio utilizando CSS y JavaScript en GitHub. Los sitios web se crean automáticamente para cada una de las ramas, desde la previsualización de contenido hasta la producción. Todos los recursos que introduce en el repositorio de GitHub están disponibles en el sitio web sin un proceso de compilación.

## Uso de Sidekick {#using-sidekick}

AEM Sidekick ofrece una barra de herramientas con opciones según el contexto para que pueda editar, previsualizar y publicar contenido fácilmente. Tras la [instalación](https://www.hlx.live/docs/sidekick-extension), la extensión de AEM Sidekick se puede utilizar en entornos de proyecto o al editar el contenido (por ejemplo, en documentos de Google). Según el entorno, tiene varias acciones disponibles, como Previsualizar, Recargar, Editar y Publicar. También puede cambiar de entorno al utilizar la barra de tareas, pasando de la vista previa a la producción y viceversa.

**Para publicar**, abra Sidekick en una página de vista previa y utilice la acción Publicar. Después de hacer clic en Publicar, la versión de vista previa actual de la página estará disponible en los entornos en directo y de producción.

## Integración de AEM Assets con la creación basada en documentos {#integrate-assets-edge}

Edge Delivery permite utilizar imágenes disponibles en repositorios de AEM Assets durante la creación de documentos en Microsoft Word o Google Docs.

Las opciones para utilizar imágenes en los documentos solo están disponibles después de [configurar el complemento Sidekick de AEM Assets](https://www.hlx.live/developer/configuring-aem-assets-sidekick-plugin).

El complemento Sidekick de AEM Assets admite el acceso a:

* AEM Assets as a Cloud Service

* AEM Assets Essentials

Después de configurar el complemento Sidekick de AEM Assets, puede [empezar a utilizar imágenes en los documentos de Google Docs o Microsoft Word](https://www.hlx.live/docs/aem-assets-sidekick-plugin).

## Lectura adicional {#further-reading}

Para obtener más información, consulte las siguientes páginas:

* Para obtener más información sobre cómo empezar a utilizar Edge Delivery, consulte la sección [Generar](https://www.hlx.live/docs/#build) de la documentación de Edge delivery.
* Para obtener información sobre cómo crear y publicar contenido mediante Edge Delivery, consulte la sección [Publicar](https://www.hlx.live/docs/authoring).
* Para comprender cómo usar la extensión de Sidekick, consulte la página [Uso de Sidekick](https://www.hlx.live/docs/sidekick).
* Para la creación de AEM, consulte la [página Conceptos de creación](/help/sites-authoring/author.md))
