---
title: Conceptos básicos de los componentes de comunidades
seo-title: Conceptos básicos de los componentes de comunidades
description: Añadir funciones de comunidades a sitios AEM en modo de edición y configurar componentes
seo-description: Añadir funciones de comunidades a sitios AEM en modo de edición y configurar componentes
uuid: c017a7c5-40d1-4592-9317-96fd727dac86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 21714581-7645-4b47-a9b0-9f1424013240
translation-type: tm+mt
source-git-commit: c77a353d43a3a6f33dffecf0b4e7672ed3e2dd3f
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 1%

---


# Conceptos básicos de los componentes de comunidades {#communities-components-basics}

## Información general {#overview}

La sección de creación de la documentación describe cómo agregar funciones de Comunidades a AEM sitios en modo de edición de autor, así como la descripción de las configuraciones de componentes.

Los componentes pueden explorarse con una instancia de AEM y la guía [interactiva](components-guide.md)Community Components.

## Acceso a componentes de comunidades {#accessing-communities-components}

Al crear contenido de página, si la plantilla subyacente permite cambios en el diseño de la página, es posible activar componentes que no están disponibles en el navegador de componentes como parte del diseño del sitio.

Los componentes de Comunidades disponibles se enumeran [aquí](author-communities.md#available-communities-components).

>[!NOTE]
>
>Para obtener información general sobre la creación, consulte la guía [rápida de creación de páginas](../../help/sites-authoring/qg-page-authoring.md).
>
>Si no está familiarizado con AEM, vista la documentación sobre la gestión [](../../help/sites-authoring/basic-handling.md)básica.


### Introducción al modo de diseño {#entering-design-mode}

Si no se encuentra un componente de **Comunidades** en el navegador de componentes (barra de tareas), será necesario introducir `Design Mode` para agregar otros componentes de Comunidades. [También es posible que sea necesario agregar bibliotecas](#required-clientlibs) de cliente (clientlibs) requeridas.

Para obtener más información, consulte [Configuración de componentes en modo](../../help/sites-authoring/default-components-designmode.md)de diseño.

A continuación se muestran imágenes de la selección de algunos componentes de Communities y su visualización en el navegador de componentes:

![componente-diseño](assets/component-design.png)

Los componentes seleccionados ya están disponibles en el navegador de componentes:

![component-design1](assets/component-design1.png)

## Clientlibs requeridos {#required-clientlibs}

[Las bibliotecas](../../help/sites-developing/clientlibs.md) del lado del cliente (clientlibs) son necesarias para el correcto funcionamiento (JavaScript) y el estilo (CSS) de un componente.

Cuando se agrega un componente Comunidades a una página, si el resultado es un error o una apariencia inesperada, lo primero que se debe intentar es agregar los clientes necesarios para el componente Comunidades. Para obtener más información, consulte [Clientlibs for Communities Components](clientlibs.md).

### Ejemplo: Revisiones colocadas inicialmente sin bibliotecas de cliente... {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ... Y con bibliotecas de cliente {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## Etiquetado {#tagging}

Muchas funciones de Comunidades se pueden configurar para permitir que los miembros etiqueten el contenido introducido (publicado) en el entorno de publicación.

Si se permite el etiquetado, la configuración del sitio de la comunidad puede establecerse para limitar las Áreas de nombres presentadas a los miembros en el entorno de publicación. Consulte la consola Sitios [de comunidad](sites-console.md#tagging).

Características que permiten el etiquetado: [blog](blog-feature.md), [calendario](calendar.md), biblioteca [](file-library.md)de archivos, [foro](forum.md)

Funciones que utilizan etiquetas: [catálogo](catalog.md), [búsqueda](search.md), nube de etiquetas [sociales](tagcloud.md)

Para obtener información sobre la creación:

* [Uso de etiquetas](../../help/sites-authoring/tags.md)

Para información administrativa:

* Creación de Áreas de nombres de etiquetas (taxonomía): [Administración de etiquetas](../../help/sites-administering/tags.md)
* Configuración del sitio de la comunidad: consulte [ETIQUETADO](sites-console.md#tagging)
* [Etiquetado de contenido generado por el usuario](../../help/sites-authoring/tags.md)
* [Etiquetado de recursos de habilitación](tag-resources.md)

Para obtener información sobre desarrolladores:

* [AEM marco de etiquetado](../../help/sites-developing/framework.md)
* [Etiquetado de elementos esenciales](tag.md)

