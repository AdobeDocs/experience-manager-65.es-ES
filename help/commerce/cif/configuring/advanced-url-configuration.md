---
title: Configuraciones de URL avanzadas
description: Obtenga información sobre cómo personalizar las direcciones URL para páginas de productos y categorías. Esto permite que las implementaciones optimicen las direcciones URL de los motores de búsqueda y promuevan la detección.
sub-product: Comercio
doc-type: technical-video
activity: setup
audience: administrator
feature: Marco de integración de Commerce
kt: 4933
thumbnail: 34350.jpg
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 88%

---

# Configuraciones de URL avanzadas {#url}

Los [componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components) proporcionan configuraciones avanzadas para personalizar las direcciones URL de las páginas de productos y categorías. Muchas implementaciones personalizan estas direcciones URL con fines de optimización de los motores de búsqueda (SEO). En el siguiente vídeo se explica cómo configurar el `UrlProvider` servicio y las funciones de las [Asignaciones de Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para personalizar las direcciones URL de las páginas de productos y categorías.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configuración {#configuration}

Para configurar el servicio `UrlProvider` según los requisitos de SEO y las necesidades, un proyecto debe proporcionar una configuración OSGI para la configuración del &quot;proveedor de URL del CIF&quot; y configurar el servicio como se describe a continuación.

>[!NOTE]
>
> El proyecto [Tienda de referencia de Venia](https://github.com/adobe/aem-cif-guides-venia) que se muestra a continuación, incluye configuraciones de muestra para demostrar el uso de direcciones URL personalizadas para páginas de productos y categorías.

### Plantilla de dirección URL de la página del producto {#product}

Esto configura las direcciones URL de las páginas de productos con las siguientes propiedades:

* **Plantilla de dirección URL del producto**: define el formato de las direcciones URL con un conjunto de marcadores de posición. El valor predeterminado es `{{page}}.{{url_key}}.html#{{variant_sku}}`, que termina generando direcciones URL como, por ejemplo, `/content/venia/us/en/products/product-page.chaz-kangeroo-hoodie.html#MH01-M-Orange` donde
   * `{{page}}` se ha reemplazado con `/content/venia/us/en/products/product-page`
   * `{{url_key}}` se ha reemplazado por la propiedad `url_key` del producto Magento, aquí `chaz-kangeroo-hoodie`
   * `{{variant_sku}}` se ha reemplazado por la variante seleccionada actualmente, aquí `MH01-M-Orange`
* **Ubicación del identificador de producto**: define la ubicación del identificador que se utilizará para recuperar los datos del producto. El valor predeterminado es `SELECTOR`, el otro valor posible es `SUFFIX`. Con la URL del ejemplo anterior, esto significa que el identificador `chaz-kangeroo-hoodie` se utilizará para recuperar los datos del producto.
* **Tipo del identificador de producto**: define el tipo del identificador que se utiliza para recuperar los datos del producto. El valor predeterminado es `URL_KEY`, el otro valor posible es `SKU`. Con la URL del ejemplo anterior, esto significa que los datos del producto se recuperarán con un filtro de Magento GraphQL como `filter:{url_key:{eq:"chaz-kangeroo-hoodie"}}`.

### Plantilla URL de la página de lista de productos {#product-list}

Esto configura las direcciones URL de las páginas de categorías o listas de productos con las siguientes propiedades:

* **Plantilla de dirección URL de categorías**: define el formato de las direcciones URL con un conjunto de marcadores de posición. El valor predeterminado es `{{page}}.{{id}}.html`, que termina generando direcciones URL como, por ejemplo, `/content/venia/us/en/products/category-page.3.html` donde
   * `{{page}}` se ha reemplazado con `/content/venia/us/en/products/category-page`
   * `{{id}}` es reemplazado por la propiedad de la `id` categoría de Magento aquí `3`
* **Ubicación del identificador de categoría**: define la ubicación del identificador que se utilizará para recuperar los datos del producto. El valor predeterminado es `SELECTOR`, el otro valor posible es `SUFFIX`. Con la URL del ejemplo anterior, esto significa que el identificador `3` se utilizará para recuperar los datos del producto.
* **Tipo del identificador de categoría**: define el tipo del identificador que se utiliza para recuperar los datos del producto. El valor predeterminado y solo el valor admitido actualmente es `ID`. Con la URL del ejemplo anterior, esto significa que los datos de la categoría se recuperarán con un filtro de Magento GraphQL como `category(id:3)`.

Es posible añadir propiedades personalizadas para cada plantilla, siempre que los componentes que utilicen la plantilla estén configurando los datos correspondientes de `UrlProvider`. Consulte, por ejemplo, el código de la `ProductListItemImpl` clase para averiguar cómo se implementa.

También es posible reemplazar el servicio `UrlProvider` con un servicio OSGi completamente personalizado. En este caso, se debe implementar la `UrlProvider` interfaz y registrarla con una clasificación de servicio más alta para reemplazar la implementación predeterminada.

## Combinación con asignaciones de Sling {#sling-mapping}

Además del `UrlProvider`, también es posible configurar las [asignaciones de Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para reescribir y procesar direcciones URL. El tipo de archivo del proyecto AEM también proporciona [una configuración de ejemplo](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) para configurar algunas asignaciones de Sling para el puerto 4503 (publicación) y 80 (Dispatcher).

## Combinación con AEM Dispatcher {#dispatcher}

Las reescrituras de URL también se pueden realizar mediante una HTTP del servidor AEM Dispatcher con `mod_rewrite` módulo. El [tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype) proporciona una referencia a la configuración de AEM Dispatcher que ya incluye las [reglas de reescritura](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) básicas para el tamaño generado.

## Ejemplo

El proyecto [Tienda de referencia de Venia](https://github.com/adobe/aem-cif-guides-venia) incluye configuraciones de muestra para demostrar el uso de direcciones URL personalizadas para páginas de productos y categorías. Esto permite que cada proyecto configure patrones de URL individuales para páginas de productos y categorías según sus necesidades de SEO. Se utiliza una combinación de asignaciones de CIF `UrlProvider` y de Sling como se describe anteriormente.

>[!NOTE]
>
>Esta configuración debe ajustarse con el dominio externo utilizado por el proyecto. Las asignaciones de Sling funcionan según el nombre de host y el dominio. Por lo tanto, esta configuración está deshabilitada de forma predeterminada y debe habilitarse antes de la implementación. Para ello, cambie el nombre de la `hostname.adobeaemcloud.com` carpeta Asignaciones de Sling en `ui.content/src/main/content/jcr_root/etc/map.publish/https` función del nombre de dominio utilizado y habilite esta configuración añadiendo `resource.resolver.map.location="/etc/map.publish"` a la `JcrResourceResolver` configuración del proyecto.

## Recursos adicionales

* [Tienda de referencia de Venia](https://github.com/adobe/aem-cif-guides-venia)
* [Asignación de recursos de AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Asignaciones de Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
