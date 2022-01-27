---
title: Product Cockpit
description: Trabajo con Product Cockpit
source-git-commit: f3e286c7b5404812655f3b257de17be7bfde7487
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 1%

---

# Product Cockpit {#product-cockpit}

## Información general {#overview}

El modelo Product Cockpit ofrece una visión general unificada de los catálogos de productos vinculados y el contenido asociado. Todo el contenido asociado tiene vínculos para acceder rápidamente a él desde la cabina.

Los datos de productos clasificados incluyen cualquier mutación futura, como nuevas categorías, productos o propiedades actualizadas.

>[!NOTE]
>
>El término catálogo de productos se puede intercambiar con tienda de comercio, vista de tienda y expresiones similares.

## Configuración {#configuration}

Los catálogos de productos deben configurarse en AEM. Consulte [configuración de tiendas y catálogos](/help/commerce/cif/getting-started.md#catalog) para obtener más información.

La activación de las funciones del catálogo por etapas requiere autenticación. Consulte [Introducción](/help/commerce/cif/getting-started.md) para obtener más información.

>[!NOTE]
>
>Las funciones del catálogo por etapas solo están disponibles con los conectores de Adobe Commerce y de terceros que admiten la autenticación basada en token.

## Apertura de la cabina de productos {#opening-product-cockpit}

La manera más fácil de acceder a la Cockpit del producto es a través del menú &quot;Comercio&quot; en AEM menú principal. También es posible utilizar Omnisearch (buscar comercio) o abrir `https://<yourAEMInstance>/commerce.html`.

![menú AEM](/help/commerce/cif/assets/aem-menu.png)

## Exploración de catálogos de productos {#browsing-product-catalogs}

La Cockpit del producto está organizada jerárquicamente siguiendo la estructura del catálogo del producto. El primer nivel muestra el nivel raíz del catálogo de todos los catálogos de productos configurados, incluida la metainformación del servidor de comercio.

![Catálogos configurados](/help/commerce/cif/assets/catalog-overview.png)

Al hacer clic en una categoría, se cargarán los elementos secundarios de la categoría en la que se hizo clic.

![Elementos secundarios de la categoría](/help/commerce/cif/assets/catalog-category-children.png)

Al hacer clic en un producto, se cargarán las variaciones de producto si están disponibles.

![Variaciones de productos](/help/commerce/cif/assets/catalog-product-variation.png)

>[!NOTE]
>
>Los datos del catálogo de productos en AEM son datos que se recuperan en tiempo real mediante el extremo de comercio configurado. No se almacenan datos del catálogo de productos en AEM.

## Búsqueda de catálogos de productos {#searching-product-catalog}

Se proporciona una búsqueda de texto completo sobre el catálogo de productos completo en la pestaña del filtro izquierdo para encontrar rápidamente los productos.

![búsqueda](/help/commerce/cif/assets/search-cockpit.png)

## Exploración del catálogo de productos escalonado {#staged-product-catalogs}

De forma predeterminada, la cabina de productos muestra datos del catálogo de productos en directo. El uso del &quot;CATÁLOGO ENSAYADO&quot; en la pestaña de filtro de la izquierda cargará el catálogo de productos para cualquier fecha seleccionada.

![catálogo por etapas](/help/commerce/cif/assets/staged-cockpit.png)

## Propiedades del catálogo de productos {#catalog-properties}

Al hacer clic en el icono de propiedades de un producto o categoría, se abrirá la vista de propiedades del objeto seleccionado. Las propiedades abiertas de una variante de producto son iguales a abrir las propiedades de producto principales.

### Pestañas de comercio {#tabs}

Las pestañas general y variante muestran propiedades de comercio predefinidas que provienen del servidor de comercio. Estos datos (incl. variantes) son datos de solo lectura en AEM, ya que el sistema de registro es el back-end de comercio. La pestaña variante solo aparece para productos con variantes y muestra una lista de todas las variantes.

![propiedades del catálogo](/help/commerce/cif/assets/catalog-properties.png)

### Pestañas de contenido de AEM {#content-tabs}

Estas pestañas, agrupadas por AEM tipos de contenido (fragmentos de experiencias, fragmentos de contenido, recursos asociados), muestran AEM contenido asociado al objeto de comercio. La acción &quot;Ver detalles&quot; abre una nueva pestaña del navegador con el contenido seleccionado.

![propiedades de contenido](/help/commerce/cif/assets/content-properties.png)
