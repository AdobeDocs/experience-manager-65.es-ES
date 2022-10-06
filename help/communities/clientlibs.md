---
title: Clientlibs para componentes de Communities
seo-title: Clientlibs for Communities Components
description: Bibliotecas de cliente para comunidades
seo-description: Client-side libraries for Communities
uuid: d2a9f986-96cf-4ee8-81e6-36a96f45ddcb
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 68ce47c8-a03f-40d6-a7f3-2cc64aee0594
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# Clientlibs para componentes de Communities {#clientlibs-for-communities-components}

## Introducción {#introduction}

En esta sección de la documentación se describe cómo agregar bibliotecas del lado del cliente (clientlibs) a una página para componentes de Communities.

Para obtener información básica, visite :

* [Uso de bibliotecas del lado del cliente](/help/sites-developing/clientlibs.md) que proporciona detalles de uso, así como herramientas de depuración
* [Clientlibs para SCF](/help/communities/client-customize.md#clientlibs) que proporciona información útil al personalizar componentes de SCF


## Por qué se requieren Clientlibs {#why-clientlibs-are-required}

Las bibliotecas de clientes son necesarias para el correcto funcionamiento (JavaScript) y el estilo (CSS) de un componente.

Cuando existe un [función de comunidad](/help/communities/functions.md) para una función, todos los componentes y configuraciones necesarios, incluido el clientlibs requerido, estarán presentes en el sitio de la comunidad. Solo si los componentes adicionales van a estar disponibles para los autores, se necesitarán añadir clientlibs adicionales.

Cuando faltan las clientlibs requeridas, [adición de un componente Comunidades a una página](/help/communities/author-communities.md) podría provocar errores de javascript y un aspecto inesperado.

### Ejemplo : Revistas colocadas sin Clientlibs {#example-placed-reviews-without-clientlibs}

![colocado-review](assets/placed-reviews.png)

### Ejemplo : Revisiones colocadas con Clientlibs {#example-placed-reviews-with-clientlibs}

![review-clientlibs](assets/reviews-clientlibs.png)

## Identificación de Clientlibs Requeridos {#identifying-required-clientlibs}

La información de funciones esenciales para los desarrolladores identifica los clientlibs necesarios.

Además, desde una instancia de AEM, vaya a la [Guía de componentes de comunidad](/help/communities/components-guide.md) proporciona acceso a una lista de categorías clientlib requeridas para un componente.

Por ejemplo, en la parte superior del [Página de revisiones](https://localhost:4502/content/community-components/en/reviews.html) los clientlibs requeridos enumerados son

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-review](assets/clientlibs-reviews.png)

## Adición de Clientlibs Necesarios {#adding-required-clientlibs}

Cuando se desee añadir un componente Comunidades a una página, será necesario agregar las clientlibs necesarias para el componente si no está presente.

Uso [CRXDE|Lite](#using-crxde-lite) para modificar una lista de clientlibslist existente para una página de sitio de la comunidad.

Para agregar una clientlib para un sitio de la comunidad usando [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Vaya a [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* Busque la variable `clientlibslist` para la página en la que desea añadir el componente:

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* con `clientlibslist` nodo seleccionado:

   * Localizar la cadena[] property `scg:requiredClientLibs`.
   * Seleccione su `Value` para acceder al cuadro de diálogo matriz de cadenas .

      * Desplácese hacia abajo si es necesario.
      * Seleccione + para introducir una nueva biblioteca de cliente.

         * Repita el proceso para agregar más bibliotecas de cliente.

         * Select **OK**.
   * Select **Guardar todo**.


>[!NOTE]
>
>Si el sitio no es un sitio de la comunidad, es necesario descubrir la existencia o ubicación de las bibliotecas de cliente que se utilizan para el sitio.

Al usar la variable [Introducción a AEM Communities](/help/communities/getting-started.md) ejemplo, donde `site-name` es *participación*, así es como aparecerá clientliblist si agrega el componente de revisiones:

![review-component](assets/review-component.png)
