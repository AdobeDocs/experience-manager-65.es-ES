---
title: Configuraciones de URL avanzadas
description: Aprenda a personalizar las direcciones URL de las páginas de productos y categorías. Esto permite que las implementaciones optimicen las direcciones URL de los motores de búsqueda y promuevan la detección.
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 0125021a-1c00-4ea3-b7fb-1533b7b9f4f2
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 24%

---

# Configuraciones de URL avanzadas {#url}

>[!NOTE]
>
>La optimización de los motores de búsqueda (SEO) se ha convertido en una preocupación clave para muchos expertos en marketing. AEM Como resultado, las preocupaciones de SEO deben ser abordadas en muchos Proyectos de. Consulte [Prácticas recomendadas para la optimización de los motores de búsqueda y administración URL](https://experienceleague.adobe.com/docs/experience-manager-65/managing/managing-further-reference/seo-and-url-management.html) para obtener más información.

Los [componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components) proporcionan configuraciones avanzadas para personalizar las direcciones URL de las páginas de productos y categorías. Muchas implementaciones personalizan estas direcciones URL con fines de optimización de los motores de búsqueda (SEO). En el siguiente vídeo se explica cómo configurar el `UrlProvider` servicio y las funciones de las [Asignaciones de Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para personalizar las direcciones URL de las páginas de productos y categorías.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configuración {#configuration}

Para configurar la variable `UrlProvider` CIF según los requisitos de SEO y las necesidades, un proyecto debe proporcionar una configuración OSGI para la &quot;configuración del proveedor de URL&quot;.

>[!NOTE]
>
>AEM CIF Desde la versión 2.0.0 de los componentes principales de la de trabajo, la configuración del proveedor de URL solo proporciona formatos de URL predefinidos, en lugar de los formatos configurables de texto libre conocidos en las versiones 1.x. Además, el uso de selectores para pasar datos en direcciones URL se ha sustituido por sufijos.

### Formato de URL de página de producto {#product}

Esto configura las direcciones URL de las páginas de productos y admite las siguientes opciones:

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (predeterminada)
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

Si existe el [Tienda de referencia de Venia](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` se ha reemplazado por `/content/venia/us/en/products/product-page`
* `{{sku}}` se sustituye por el SKU del producto, por ejemplo, `VP09`
* `{{url_key}}` se sustituye por el del producto `url_key` , por ejemplo, `lenora-crochet-shorts`
* `{{url_path}}` se sustituye por el del producto `url_path`, por ejemplo, `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` se reemplaza por la variante seleccionada actualmente, por ejemplo, `VP09-KH-S`

Dado que la variable `url_path` se han quedado obsoletos, los formatos de URL de producto predefinidos utilizan un `url_rewrites` y elija el que tenga la mayor cantidad de segmentos de ruta como alternativa si la variable `url_path` no está disponible.

Con los datos de ejemplo anteriores, una URL de variante de producto con formato URL predeterminada tiene el siguiente aspecto `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### Formato de URL de página de categoría {#product-list}

Esto configura las direcciones URL de las páginas de categorías o listas de productos y admite las siguientes opciones:

* `{{page}}.html/{{url_path}}.html` (predeterminada)
* `{{page}}.html/{{url_key}}.html`

Si existe el [Tienda de referencia de Venia](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` se ha reemplazado por `/content/venia/us/en/products/category-page`
* `{{url_key}}` se sustituye por el de la categoría `url_key` propiedad
* `{{url_path}}` se sustituye por el de la categoría `url_path`

Con los datos del ejemplo anterior, la dirección URL de una página de categoría con formato URL predeterminado tiene el siguiente aspecto `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
>El `url_path` es una concatenación de `url_keys` de los antecesores de un producto o categoría y del producto o categoría `url_key` separado por `/` barra diagonal.

### Páginas específicas de productos y categorías {#specific-pages}

Es posible crear lo siguiente [páginas de múltiples productos y categorías](multi-template-usage.md) solo para un subconjunto específico de categorías o productos de un catálogo.

El `UrlProvider` está preconfigurado para generar vínculos profundos a dichas páginas en instancias de nivel de creación. Esto resulta útil para los editores que exploran un sitio mediante el modo de vista previa, navegan a una página de producto o categoría específica y vuelven al modo de edición para editar la página.

En las instancias de nivel de publicación, por otro lado, las direcciones URL de la página del catálogo deben mantenerse estables para no perder ganancias en las clasificaciones de los motores de búsqueda, por ejemplo. Debido a esto, las instancias del nivel de publicación no procesarán vínculos profundos a páginas de catálogo específicas de forma predeterminada. Para cambiar este comportamiento, la variable _CIF Estrategia de página específica del proveedor de URL_ se puede configurar para que siempre genere direcciones url de página específicas.

## Formatos de URL personalizados {#custom-url-format}

Para proporcionar un formato de URL personalizado que un proyecto pueda implementar, se debe usar el [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) o el [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) y registre la implementación como servicio OSGI. Estas implementaciones, si están disponibles, reemplazan el formato configurado y predefinido. Si hay varias implementaciones registradas, la que tenga la clasificación de servicio más alta reemplaza a las que tienen la clasificación de servicio más baja.

Las implementaciones de formato de URL personalizadas deben implementar un par de métodos para crear una dirección URL a partir de parámetros determinados y para analizar una dirección URL y devolver los mismos parámetros respectivamente.

## Combinación con asignaciones de Sling {#sling-mapping}

Además de las `UrlProvider`, también es posible configurar [Asignaciones de Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para reescribir y procesar direcciones URL. AEM El proyecto Archetype también proporciona lo siguiente [un ejemplo de configuración](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) para configurar algunas asignaciones de Sling para el puerto 4503 (publicación) y 80 (Dispatcher).

## AEM Combinación con Dispatcher de la {#dispatcher}

AEM Las reescrituras de URL también se pueden lograr utilizando el servidor HTTP de Dispatcher de la aplicación de la red de distribución de datos con `mod_rewrite` módulo. El [tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype) proporciona una referencia a la configuración de AEM Dispatcher que ya incluye las [reglas de reescritura](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) básicas para el tamaño generado.

## Ejemplo

El proyecto [Tienda de referencia de Venia](https://github.com/adobe/aem-cif-guides-venia) incluye configuraciones de muestra para demostrar el uso de direcciones URL personalizadas para páginas de productos y categorías. Esto permite que cada proyecto configure patrones de URL individuales para páginas de productos y categorías según sus necesidades de SEO. Se utiliza una combinación de asignaciones de CIF `UrlProvider` y de Sling como se describe anteriormente.

>[!NOTE]
>
>Esta configuración debe ajustarse con el dominio externo utilizado por el proyecto. Las asignaciones de Sling funcionan según el nombre de host y el dominio. Por lo tanto, esta configuración está deshabilitada de forma predeterminada y debe habilitarse antes de la implementación. Para ello, cambie el nombre de la `hostname.adobeaemcloud.com` carpeta Asignaciones de Sling en `ui.content/src/main/content/jcr_root/etc/map.publish/https` función del nombre de dominio utilizado y habilite esta configuración añadiendo `resource.resolver.map.location="/etc/map.publish"` a la `JcrResourceResolver` configuración del proyecto.

## Recursos adicionales

* [Tienda de referencia de Venia](https://github.com/adobe/aem-cif-guides-venia)
* [Asignación de recursos de AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Asignaciones de Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
