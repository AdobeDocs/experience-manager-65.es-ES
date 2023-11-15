---
title: Conceptos básicos de componentes de comunidades
description: AEM Agregar características de Communities a sitios de la comunidad en modo de edición y configurar componentes de la página
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: eb5ce76a-bf28-4540-bc2d-3b5ecb8286f2
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 2%

---

# Conceptos básicos de componentes de comunidades {#communities-components-basics}

## Información general {#overview}

AEM En la sección de creación de la documentación se describe cómo agregar funciones de comunidades a sitios de creación en el modo de edición de creación, así como la descripción de configuraciones de componentes.

AEM Los componentes se pueden explorar mediante una instancia de y la función interactiva [Guía de componentes de la comunidad](components-guide.md).

## Acceder a componentes de Communities {#accessing-communities-components}

Al crear contenido de página, si la plantilla subyacente permite realizar cambios en el diseño de la página, es posible habilitar componentes que aún no estén disponibles en el explorador de componentes como parte del diseño del sitio.

Se muestran los componentes disponibles de Communities [aquí](author-communities.md#available-communities-components).

>[!NOTE]
>
>Para obtener información general sobre la creación de, consulte [guía rápida para la creación de páginas](../../help/sites-authoring/qg-page-authoring.md).
>
>AEM Si no está familiarizado con el uso de la, consulte la documentación de en [manipulación básica](../../help/sites-authoring/basic-handling.md).

### Entrando en modo de diseño {#entering-design-mode}

Si un **Communities** el componente no se encuentra en el navegador de componentes (barra de tareas), será necesario introducir `Design Mode` para agregar otros componentes de Communities. [Bibliotecas de cliente necesarias](#required-clientlibs) (clientlibs) también puede ser necesario añadirlas.

Para obtener más información, consulte [Configuración de componentes en modo de diseño](../../help/sites-authoring/default-components-designmode.md).

A continuación se muestran imágenes de cómo seleccionar algunos componentes de Communities y verlos en el explorador de componentes:

![diseño de componentes](assets/component-design.png)

Los componentes seleccionados están ahora disponibles en el explorador de componentes:

![component-design1](assets/component-design1.png)

## Clientlibs Requeridos {#required-clientlibs}

[Bibliotecas del lado cliente](../../help/sites-developing/clientlibs.md) (clientlibs) son necesarios para el funcionamiento adecuado (JavaScript) y el estilo (CSS) de un componente.

Al agregar un componente de Communities a una página, si el resultado es un error o una apariencia inesperada, lo primero que debe intentar es agregar los clientlibs necesarios para el componente Communities. Para obtener más información, consulte [Componentes de Clientlibs para Communities](clientlibs.md).

### Ejemplo: Revisiones colocadas inicialmente sin bibliotecas de cliente... {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ... Y con bibliotecas de cliente {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## Etiquetado {#tagging}

Se pueden configurar muchas funciones de Communities para permitir que los miembros etiqueten el contenido introducido (publicado) en el entorno de publicación.

Si se permite el etiquetado, la configuración del sitio de la comunidad puede establecerse para limitar las áreas de nombres que se presentan a los miembros en el entorno de publicación. Consulte la [Consola Sitios de la comunidad](sites-console.md#tagging).

Funciones que permiten el etiquetado: [blog](blog-feature.md), [calendario](calendar.md), [biblioteca de archivos](file-library.md), [foro](forum.md)

Funciones que utilizan etiquetas: [búsqueda](search.md), [nube de etiquetas sociales](tagcloud.md)

Para crear información:

* [Uso de etiquetas](../../help/sites-authoring/tags.md)

Para información administrativa:

* Creación de áreas de nombres de etiquetas (taxonomía): [Administración de etiquetas](../../help/sites-administering/tags.md)
* Configuración del sitio de la comunidad: consulte [ETIQUETADO](sites-console.md#tagging)
* [Etiquetado del contenido generado por el usuario](../../help/sites-authoring/tags.md)

Para obtener información del desarrollador:

* [Marco de trabajo de etiquetado de AEM](../../help/sites-developing/framework.md)
* [Etiquetado de elementos esenciales](tag.md)
