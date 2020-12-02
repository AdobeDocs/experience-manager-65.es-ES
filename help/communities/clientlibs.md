---
title: Componentes Clientlibs for Communities
seo-title: Componentes Clientlibs for Communities
description: Bibliotecas de cliente para comunidades
seo-description: Bibliotecas de cliente para comunidades
uuid: d2a9f986-96cf-4ee8-81e6-36a96f45ddcb
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 68ce47c8-a03f-40d6-a7f3-2cc64aee0594
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Componentes de Clientlibs para Comunidades {#clientlibs-for-communities-components}

## Introducción {#introduction}

Esta sección de la documentación describe cómo agregar bibliotecas de cliente (clientlibs) a una página para componentes de Comunidades.

Para obtener información básica, visite :

* [Uso de ](/help/sites-developing/clientlibs.md) las bibliotecas del lado del cliente que proporcionan detalles de uso, así como herramientas de depuración
* [Clientlibs para ](/help/communities/client-customize.md#clientlibs) SCFque proporciona información útil al personalizar componentes SCF
* [Blog: Bibliotecas de clientes de AEM explicadas por ejemplo](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)

## Por qué los clientes son necesarios {#why-clientlibs-are-required}

Los clientes son necesarios para el correcto funcionamiento (JavaScript) y el estilo (CSS) de un componente.

Cuando existe una [función de comunidad](/help/communities/functions.md) para una función, todos los componentes y configuraciones necesarios, incluidos los clientes requeridos, estarán presentes en el sitio de la comunidad. Solo si los autores disponen de componentes adicionales, se necesitarían agregar clientes adicionales.

Cuando faltan los clientes requeridos, [la adición de un componente Communities a una página](/help/communities/author-communities.md) podría provocar errores de javascript y un aspecto inesperado.

### Ejemplo: Revistas colocadas sin Clientlibs {#example-placed-reviews-without-clientlibs}

![colocar revisiones](assets/placed-reviews.png)

### Ejemplo: Revistas colocadas con Clientlibs {#example-placed-reviews-with-clientlibs}

![reseñas-clientlibs](assets/reviews-clientlibs.png)

## Identificación de Clientlibs requeridos {#identifying-required-clientlibs}

La información esencial de las funciones para los desarrolladores identifica a los clientes requeridos.

Además, desde una instancia de AEM, la búsqueda en la [Guía de componentes de comunidad](/help/communities/components-guide.md) proporciona acceso a una lista de categorías clientlib necesarias para un componente.

Por ejemplo: en la parte superior de la [página de revisiones](https://localhost:4502/content/community-components/en/reviews.html), los clientes requeridos que aparecen son

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-review](assets/clientlibs-reviews.png)

## Añadir Clientlibs requeridos {#adding-required-clientlibs}

Cuando se desee agregar un componente Comunidades a una página, será necesario agregar los clientes necesarios para el componente si no están presentes.

Utilice [CRXDE|Lite](#using-crxde-lite) para modificar una lista de clientes existente para una página de sitio de comunidad.

Para agregar una clientlib para un sitio de comunidad mediante [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Vaya a [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* Busque el nodo `clientlibslist` de la página en la que desea agregar el componente:

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Con el nodo `clientlibslist` seleccionado:

   * Busque la propiedad String[] `scg:requiredClientLibs`.
   * Seleccione su `Value` para acceder al cuadro de diálogo de matriz de cadenas.

      * Desplácese hacia abajo si es necesario.
      * Seleccione + para introducir una nueva biblioteca de cliente.

         * Repita el procedimiento para agregar más bibliotecas de cliente.

         * Seleccione **Aceptar**.
   * Seleccione **Guardar todo**.


>[!NOTE]
>
>Si el sitio no es un sitio de la comunidad, es necesario descubrir la existencia o ubicación de las bibliotecas cliente que se utilizan para el sitio.

Utilizando el ejemplo [Introducción a AEM Communities](/help/communities/getting-started.md), donde `site-name` es *engagement*, así es como aparecerá clientliblist si agrega el componente de revisiones:

![revisión-componente](assets/review-component.png)

