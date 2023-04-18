---
title: 'Creación: entorno y herramientas'
description: La consola Sitios web permite desplazarse por el sitio web y administrarlo. Con dos paneles, la estructura del sitio web se puede ampliar y se pueden realizar acciones en los elementos necesarios.
uuid: 0a9ce725-042a-4697-81fe-ac86cbab0398
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 67625e62-7035-4eb5-8dd5-6840d775a547
docset: aem65
exl-id: 5d7b6b2e-d1d8-4efe-b9ff-c9542b4e67d7
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 6%

---

# Creación: entorno y herramientas {#authoring-the-environment-and-tools}

El entorno de creación AEM ofrece varios mecanismos para organizar y editar el contenido. Se puede acceder a las herramientas desde varios editores de páginas y consolas.

## Administración del sitio {#site-administration}

La variable **Sitios web** permite administrar y desplazarse por el sitio web. Con los dos paneles, la estructura del sitio web se puede ampliar y se pueden realizar acciones en el elemento requerido:

![chlimage_1-108](assets/chlimage_1-108.png)

## Edición del contenido de la página {#editing-your-page-content}

Hay un editor de páginas independiente con la IU clásica, que utiliza el buscador de contenido y la barra de tareas:

`https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

![chlimage_1-109](assets/chlimage_1-109.png)

## Acceso a la Ayuda   {#accessing-help}

Varios **Ayuda** se puede acceder directamente a los recursos desde AEM:

Además de acceder a [ayuda desde las barras de herramientas de la consola](/help/sites-classic-ui-authoring/author-env-basic-handling.md#accessing-help), también puede acceder a la ayuda desde la barra de tareas (mediante el icono ? ) al editar una página:

![](do-not-localize/sidekick-collapsed-2.png)

O utilizando la variable **Ayuda** en el cuadro de diálogo de edición de componentes específicos; esto mostrará ayuda contextual.

## Barra de tareas {#sidekick}

La variable **Componentes** de la barra de tareas le permite examinar los componentes que se pueden añadir a la página actual. El grupo requerido puede expandirse y luego un componente arrastrado a la ubicación requerida en la página.

![chlimage_1-110](assets/chlimage_1-110.png)

## Buscador de contenido {#the-content-finder}

El buscador de contenido es una forma rápida y sencilla de encontrar recursos o contenido dentro del repositorio al editar una página.

Puede utilizar el buscador de contenido para localizar una serie de recursos. Cuando proceda, puede arrastrar un elemento y colocarlo en un párrafo de la página:

* [Imágenes](#finding-images)
* [Documentos](#finding-documents)
* [Películas](#finding-movies)
* [Explorador Dynamic Media](/help/sites-administering/scene7.md#scene7contentbrowser)
* [Páginas](#finding-pages)

* [Párrafos](#referencing-paragraphs-from-other-pages)
* [Productos](#products)
* O bien [examinar el sitio web según la estructura del repositorio](#the-content-finder)

Con todas las opciones, puede [buscar elementos específicos](#the-content-finder).

### Búsqueda de imágenes {#finding-images}

Esta ficha enumera las imágenes del repositorio.

Después de crear un párrafo de imagen en la página, puede arrastrar un elemento y colocarlo dentro del párrafo.

![chlimage_1-111](assets/chlimage_1-111.png)

### Búsqueda de documentos {#finding-documents}

Esta ficha enumera los documentos del repositorio.

Después de crear un párrafo de descarga en la página, puede arrastrar un elemento y colocarlo dentro del párrafo.

![chlimage_1-112](assets/chlimage_1-112.png)

### Búsqueda de películas {#finding-movies}

Esta ficha enumera cualquier película (por ejemplo, elementos de Flash) en el repositorio.

Después de crear un párrafo apropiado (por ejemplo, un Flash) en la página, puede arrastrar un elemento y colocarlo dentro del párrafo.

![chlimage_1-113](assets/chlimage_1-113.png)

### Productos {#products}

Esta ficha enumera los productos. Después de crear un párrafo apropiado (por ejemplo, Producto) en la página, puede arrastrar un elemento y colocarlo dentro del párrafo.

![chlimage_1-114](assets/chlimage_1-114.png)

### Búsqueda de páginas {#finding-pages}

Esta ficha muestra todas las páginas. Haga doble clic en cualquier página para abrirla y editarla.

![chlimage_1-115](assets/chlimage_1-115.png)

### Referencia a párrafos de otras páginas {#referencing-paragraphs-from-other-pages}

Esta pestaña le permite buscar otra página. Se enumerarán todos los párrafos de esa página. A continuación, puede arrastrar un párrafo a su página actual para crear una referencia al párrafo original.

![chlimage_1-116](assets/chlimage_1-116.png)

### Uso de la vista de repositorio completo {#using-the-full-repository-view}

Esta ficha muestra todos los recursos del repositorio.

![chlimage_1-117](assets/chlimage_1-117.png)

### Uso de la búsqueda con el navegador de contenido {#using-search-with-the-content-browser}

En todas las opciones puede buscar elementos específicos. Cualquier etiqueta y recurso que coincida con el patrón de búsqueda aparece en la lista:

![screen_shot_2012-02-08at100746am](assets/screen_shot_2012-02-08at100746am.png)

También puede utilizar caracteres comodín para la búsqueda. Los caracteres comodín admitidos son:

* `*`
coincide con una secuencia de cero o más caracteres.

* `?`
hace coincidir un solo carácter.

>[!NOTE]
>
>Hay una pseudo propiedad &quot;name&quot; que debe utilizarse para realizar una búsqueda comodín.

Por ejemplo, si hay una imagen disponible con el nombre:

`ad-nmvtis.jpg`

los siguientes patrones de búsqueda la encontrarán (y cualquier otra imagen que coincida con el patrón):

* `name:*nmv*`
* `name:AD*`
la coincidencia de caracteres es *not* distingue entre mayúsculas y minúsculas.

* `name:ad?nm??is.*`
puede utilizar cualquier número de caracteres comodín en una consulta.

>[!NOTE]
>
>También puede utilizar [SQL2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/commons/query/sql2/package-summary.html) buscar.

## Mostrar referencias {#showing-references}

AEM permite ver qué páginas están vinculadas a la página en la que está trabajando.

Para mostrar referencias de página directas:

1. En la barra de tareas, seleccione la **Página** icono de ficha.

   ![screen_shot_2012-02-16at83127pm](assets/screen_shot_2012-02-16at83127pm.png)

1. Select **Mostrar referencias...** AEM abre la ventana Referencias y muestra qué páginas hacen referencia a la página seleccionada, incluidas sus rutas de acceso.

   ![screen_shot_2012-02-16at83311pm](assets/screen_shot_2012-02-16at83311pm.png)

En determinadas situaciones, hay disponibles acciones adicionales en la barra de tareas, como:

* [Lanzamientos](/help/sites-classic-ui-authoring/classic-launches.md)
* [Live Copies](/help/sites-administering/msm.md)

* [Modelo](/help/sites-administering/msm-best-practices.md)

Otro [las relaciones entre páginas se pueden ver en la consola Sitios web](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console).

## Registro de auditorías {#audit-log}

La variable **Registro de auditoría** se puede acceder desde el **Información** de la barra de tareas. Enumera las acciones recientes realizadas en la página actual; por ejemplo:

![chlimage_1-118](assets/chlimage_1-118.png)

## Información de la página {#page-information}

La consola Sitios web también [proporciona información sobre el estado actual de la página](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) como publicación, modificación, bloqueo, Live Copy, etc.

## Modos de página   {#page-modes}

Al editar una página con la IU clásica hay varios modos a los que se puede acceder mediante los iconos en la parte inferior de la barra de tareas:

![](do-not-localize/chlimage_1-12.png)

La fila de iconos situada en la parte inferior de la barra de tareas se utiliza para cambiar los modos de trabajo de las páginas:

* [Editar](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md)
Este es el modo predeterminado y le permite editar la página, agregar o eliminar componentes y realizar otros cambios.

* [Vista previa](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#previewing-pages)
Este modo permite obtener una vista previa de la página como si apareciera en el sitio web con formato final.

* [Diseño](/help/sites-classic-ui-authoring/classic-page-author-design-mode.md#main-pars-procedure-0)
En este modo, puede editar el diseño de la página configurando los componentes accesibles.

>[!NOTE]
>
>También hay otras opciones disponibles:
>
>* [Andamiaje](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md)
>* [Client Context](/help/sites-administering/client-context.md)
>* Sitios web: abrirá la consola Sitios web .
>* Volver a cargar: actualizará la página.


## Métodos abreviados de teclado {#keyboard-shortcuts}

Hay varios [métodos abreviados del teclado](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) disponibles.
