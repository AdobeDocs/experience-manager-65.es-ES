---
title: Editor de imágenes
seo-title: Editor de imágenes
description: El Editor de imágenes es un elemento central de la AEM y se puede aprovechar mediante componentes para facilitar la manipulación de imágenes por parte de los autores de contenido.
seo-description: El Editor de imágenes es un elemento central de la AEM y se puede aprovechar mediante componentes para facilitar la manipulación de imágenes por parte de los autores de contenido.
uuid: de6ac71b-380a-4b67-b697-ac34a79a9cc4
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: f6347492-cf48-4835-b8fd-ce9a75a09abe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 6%

---


# Editor de imágenes{#image-editor}

El Editor de imágenes es un elemento central de la AEM y se puede aprovechar mediante componentes para facilitar la manipulación de imágenes por parte de los autores de contenido.

>[!CAUTION]
>
>Para utilizar las funciones del Editor de imágenes que se describen en este artículo, se debe instalar el [paquete de funciones 24267](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/cq-6.4.0-featurepack-24267).

## Unidades relativas para mapa de imagen {#relative-units-for-image-map}

El Editor de imágenes mantiene las áreas del mapa de imágenes como unidades absolutas y relativas. Las unidades relativas son útiles cuando se proporcionan como atributos de datos para cambiar de tamaño dinámicamente un mapa de imagen (en relación con el tamaño de imagen) en el lado del cliente en un componente de imagen interactivo.

### imageMap (propiedad) {#imagemap-property}

El Editor de imágenes mantiene las coordenadas del mapa de imagen en el JCR como una propiedad `imageMap`. Tiene el siguiente formato:

La propiedad almacena las áreas de mapa de la siguiente manera:

`[area1][area2][...]`

Formato de área:

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

Ejemplo:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## Compatibilidad con imágenes SVG {#support-for-svg-images}

El Editor de imágenes admite gráficos vectoriales escalables (SVG).

* Se admiten la función de arrastrar y soltar un recurso SVG desde DAM y la carga de un archivo SVG desde un sistema de archivos local.

## Habilitación de complementos por tipo MIME {#enabling-plugins-by-mime-type}

En determinadas situaciones, las acciones de creación deben estar restringidas para determinados tipos MIME, debido a la falta de compatibilidad con el procesamiento en el servidor. Por ejemplo, puede que no se permita editar imágenes SVG.

Los complementos del Editor de imágenes se pueden habilitar selectivamente por tipo MIME estableciendo una propiedad `supportedMimeTypes` en el nodo de configuración del complemento individual.

### Ejemplo {#example}

Por ejemplo, supongamos que la capacidad de recortar solo debe permitirse para imágenes GIF, JPEG, PNG, WEBP y TIFF.

La propiedad `supportedMimeTypes` debe establecerse como una cadena de los tipos MIME permitidos en el nodo de configuración del complemento en el nodo `cq:editConfig` del componente de imagen.

`/apps/core/wcm/components/image/v2/image/cq:editConfig`

```xml
 jcr:primaryType="cq:EditConfig">
     <cq:dropTargets jcr:primaryType="nt:unstructured">
         <image ...>
            ...
         </image>
     </cq:dropTargets>
     <cq:inplaceEditing
         jcr:primaryType="cq:InplaceEditingConfig"
         active="{Boolean}true"
         editorType="image">
         <config jcr:primaryType="nt:unstructured">
             <plugins jcr:primaryType="nt:unstructured">
                 <crop
                     jcr:primaryType="nt:unstructured"
                     supportedMimeTypes="[image/gif,image/jpeg,image/png,image/webp,image/tiff]"
                     features="*">
                     <aspectRatios jcr:primaryType="nt:unstructured">
                        ...
                     </aspectRatios>
                 </crop>
                 ...
             </plugins>
             <ui jcr:primaryType="nt:unstructured">
                 ...
             </ui>
         </config>
     </cq:inplaceEditing>
 </jcr:root>
```

