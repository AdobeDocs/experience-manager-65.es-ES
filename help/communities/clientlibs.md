---
title: Componentes de Clientlibs para Communities
description: Obtenga información sobre cómo agregar bibliotecas del lado del cliente (clientlibs) a una página para que pueda recopilar detalles de uso y utilizar herramientas de depuración para componentes de Communities.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Componentes de Clientlibs para Communities {#clientlibs-for-communities-components}

## Introducción {#introduction}

En esta sección de la documentación se describe cómo agregar bibliotecas del lado del cliente (clientlibs) a una página para componentes de Communities.

Para obtener información básica, consulte lo siguiente:

* [Uso de bibliotecas del lado del cliente](/help/sites-developing/clientlibs.md) que proporciona detalles de uso y herramientas de depuración
* [Clientlibs para SCF](/help/communities/client-customize.md#clientlibs) que proporciona información útil al personalizar componentes de SCF


## Por qué se requieren Clientlibs {#why-clientlibs-are-required}

Clientlibs son necesarios para el correcto funcionamiento (JavaScript) y el estilo (CSS) de un componente.

Cuando existe un [función comunitaria](/help/communities/functions.md) para una función, todos los componentes y configuraciones necesarios, incluidos los clientlibs necesarios, están presentes en el sitio de la comunidad. Solo si los autores deben tener disponibles componentes adicionales, se deben agregar clientlibs adicionales.

Cuando faltan los clientlibs requeridos, [agregar un componente de Communities a una página](/help/communities/author-communities.md) podría provocar errores de JavaScript y una aparición inesperada.

### Ejemplo : Revisiones colocadas sin Clientlibs {#example-placed-reviews-without-clientlibs}

![placement-review](assets/placed-reviews.png)

### Ejemplo : Revisiones colocadas con Clientlibs {#example-placed-reviews-with-clientlibs}

![review-clientlibs](assets/reviews-clientlibs.png)

## Identificación De Clientlibs Requeridos {#identifying-required-clientlibs}

La información sobre funciones esenciales para los desarrolladores de identifica los clientlibs necesarios.

AEM Además, desde una instancia de, navegar hasta el [Guía de componentes de la comunidad](/help/communities/components-guide.md) proporciona acceso a una lista de categorías clientlib necesarias para un componente.

Por ejemplo, en la parte superior de la [Página de críticas](https://localhost:4502/content/community-components/en/reviews.html) los clientlibs necesarios enumerados son

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-review](assets/clientlibs-reviews.png)

## Añadir Clientlibs Requeridos {#adding-required-clientlibs}

Si desea agregar un componente de Communities a una página, es necesario agregar los clientlibs necesarios para el componente si no están presentes.

Uso [CRXDE|Lite](#using-crxde-lite) para modificar una lista clientlibs existente para una página de sitio de la comunidad.

Para agregar una clientlib para un sitio de la comunidad utilizando [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Navegar a [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* Busque el `clientlibslist` para la página en la que desea agregar el componente:

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Con `clientlibslist` nodo seleccionado:

   * Busque la cadena[] propiedad `scg:requiredClientLibs`.
   * Seleccione su `Value` para tener acceso al cuadro de diálogo Matriz de cadenas.

      * Desplácese hacia abajo si es necesario.
      * Seleccione + para introducir una nueva biblioteca de cliente.

         * Repita el proceso para agregar más bibliotecas de cliente.

         * Seleccionar **OK**.

   * Seleccionar **Guardar todo**.

>[!NOTE]
>
>Si el sitio no es un sitio de la comunidad, se debe descubrir la existencia o la ubicación de las bibliotecas de cliente que se utilizan para el sitio.

Uso del [Introducción a AEM Communities](/help/communities/getting-started.md) ejemplo, donde `site-name` es *enganchar* Sin embargo, esto es lo que aparecería clientliblist si se añade el componente Revisiones:

![review-component](assets/review-component.png)
