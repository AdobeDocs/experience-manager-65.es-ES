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
exl-id: 0125021a-1c00-4ea3-b7fb-1533b7b9f4f2
source-git-commit: dbd38aa75caa7c3c2feee79702ab85ab397eb583
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 42%

---

# Configuraciones de URL avanzadas {#url}

Los [componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components) proporcionan configuraciones avanzadas para personalizar las direcciones URL de las páginas de productos y categorías. Muchas implementaciones personalizan estas direcciones URL con fines de optimización de los motores de búsqueda (SEO). En el siguiente vídeo se explica cómo configurar el `UrlProvider` servicio y las funciones de las [Asignaciones de Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para personalizar las direcciones URL de las páginas de productos y categorías.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configuración {#configuration}

Para configurar el servicio `UrlProvider` según los requisitos de SEO y las necesidades, un proyecto debe proporcionar una configuración OSGI para la &quot;configuración del proveedor de URL del CIF&quot;.

>[!NOTE]
>
> Desde la versión 2.0.0 de los componentes principales del CIF de AEM, la configuración del proveedor de URL solo proporciona formatos de URL predefinidos, en lugar de los formatos configurables de texto libre conocidos en las versiones 1.x. Además, el uso de selectores para pasar datos en direcciones URL se ha sustituido por sufijos.

### Formato de la dirección URL de la página del producto {#product}

Esto configura las direcciones URL de las páginas de producto y admite las siguientes opciones:

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (predeterminada)
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

En el caso del [Tienda de referencia de Venia](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` se sustituye por  `/content/venia/us/en/products/product-page`
* `{{sku}}` será reemplazado por el sku del producto, p. ej.  `VP09`
* `{{url_key}}` se reemplazará por la  `url_key` propiedad del producto, por ejemplo  `lenora-crochet-shorts`
* `{{url_path}}` se reemplazarán por el  `url_path`del producto, p. ej.  `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` se reemplazará por la variante seleccionada actualmente, por ejemplo:  `VP09-KH-S`

Con los datos del ejemplo anterior, la dirección URL de una variante de producto con formato de URL predeterminada será similar a `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### Formato de dirección URL de la página de categoría {#product-list}

Esto configura las direcciones URL de las páginas de categorías o listas de productos y admite las siguientes opciones:

* `{{page}}.html/{{url_path}}.html` (predeterminada)
* `{{page}}.html/{{url_key}}.html`

En el caso del [Tienda de referencia de Venia](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` se sustituye por  `/content/venia/us/en/products/category-page`
* `{{url_key}}` se reemplazará por la  `url_key` propiedad de la categoría
* `{{url_path}}` se reemplazará por el  `url_path`

Con los datos del ejemplo anterior, la dirección URL de una página de categoría con formato de URL predeterminado será como `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> El `url_path` es una concatenación de los `url_keys` antepasados de un producto o categoría y de los `url_key` del producto o categoría separados por `/` barra oblicua.

## Formatos de URL personalizados {#custom-url-format}

Para proporcionar un formato de URL personalizado, un proyecto puede implementar la [`UrlFormat` interfaz](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/UrlFormat.html) y registrar la implementación como servicio OSGI, usándola como página de categoría o formato de URL de página de producto. La propiedad de servicio `UrlFormat#PROP_USE_AS` indica cuál de los formatos predefinidos configurados para reemplazar:

* `useAs=productPageUrlFormat`, reemplazará el formato de URL de la página de producto configurado
* `useAs=categoryPageUrlFormat`, reemplazará el formato de dirección url de la página de categoría configurado

Si hay varias implementaciones del `UrlFormat` registrado como servicios OSGI, el que tenga la clasificación de servicio más alta reemplaza a los que tengan la clasificación de servicio más baja.

El `UrlFormat` debe implementar un par de métodos para generar una URL a partir de un mapa de parámetros determinado y para analizar una URL y devolver el mismo mapa de parámetros. Los parámetros son los mismos que se describieron anteriormente, solo para las categorías se proporciona un parámetro `{{uid}}` adicional al `UrlFormat`.

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
