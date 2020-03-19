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
source-git-commit: 5b8b1544645465d10e7c2018364b6a74f1ad9a8e

---


# Componentes Clientlibs for Communities {#clientlibs-for-communities-components}

## Introducción {#introduction}

En esta sección de la documentación se describe cómo agregar bibliotecas del lado del cliente (clientlibs) a una página para componentes de Communities.

Para obtener información básica, visite :

* [Uso de las bibliotecas](/help/sites-developing/clientlibs.md) del lado del cliente que proporcionan detalles de uso, así como herramientas de depuración
* [Clientlibs para SCF](/help/communities/client-customize.md#clientlibs) que proporciona información útil al personalizar componentes de SCF
* [Blog: Las bibliotecas de cliente de AEM se explican por ejemplo](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)

## Por qué se requieren los clientes {#why-clientlibs-are-required}

Los clientes son necesarios para el correcto funcionamiento (JavaScript) y el estilo (CSS) de un componente.

Cuando exista una función [de](/help/communities/functions.md) comunidad para una función, todos los componentes y configuraciones necesarios, incluidos los clientes requeridos, estarán presentes en el sitio de la comunidad. Solo si los autores disponen de componentes adicionales, se necesitarían agregar clientes adicionales.

Cuando faltan los clientes requeridos, [agregar un componente Comunidades a una página](/help/communities/author-communities.md) podría provocar errores de javascript y un aspecto inesperado.

### Ejemplo: Revistas colocadas sin clientes {#example-placed-reviews-without-clientlibs}

![chlimage_1-132](assets/chlimage_1-132.png)

### Ejemplo: Revistas colocadas con Clientlibs {#example-placed-reviews-with-clientlibs}

![chlimage_1-133](assets/chlimage_1-133.png)

## Identificación de los clientes requeridos {#identifying-required-clientlibs}

La información esencial de las funciones para los desarrolladores identifica a los clientes requeridos.

Además, desde una instancia de AEM, la navegación por la Guía [de componentes de](/help/communities/components-guide.md) comunidad proporciona acceso a una lista de categorías de clientlib necesarias para un componente.

Por ejemplo: en la parte superior de la página [](https://localhost:4502/content/community-components/en/reviews.html) Reseñas, los clientes requeridos que aparecen son

* cq.ckeditor
* cq.social.hbs.reseñas

![chlimage_1-134](assets/chlimage_1-134.png)

## Adición de Clientlibs requeridos {#adding-required-clientlibs}

Cuando se desee agregar un componente Comunidades a una página, será necesario agregar los clientes necesarios para el componente si no están presentes.

Utilice [CRXDE|Lite](#using-crxde-lite) para modificar una lista de clientes existente para una página de sitio de comunidad.

Para agregar una clientlib para un sitio de comunidad mediante [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* Vaya a [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* Busque el nodo de la `clientlibslist` página en la que desea agregar el componente

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Con `clientlibslist` nodo seleccionado

   * Localizar la propiedad String[]`scg:requiredClientLibs`
   * Seleccione su `Value` para acceder al cuadro de diálogo de la matriz String

      * Desplácese hacia abajo si es necesario
      * Seleccione + para introducir una nueva biblioteca de cliente

         * Repetir para agregar más bibliotecas de cliente
      * Seleccione **Aceptar**
   * Seleccione **Guardar todo**



>[!NOTE]
>
>Si el sitio no es un sitio de la comunidad, es necesario descubrir la existencia o ubicación de las bibliotecas cliente que se utilizan para el sitio.

Con el ejemplo [Introducción a Comunidades](/help/communities/getting-started.md) de AEM, donde `site-name` se *involucra*, así es como aparecerá clientliblist si se agrega el componente Reseñas:

![chlimage_1-135](assets/chlimage_1-135.png)

