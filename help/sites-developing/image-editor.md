---
title: Editor de imágenes
description: El Editor de imágenes es una pieza central de AEM y los componentes pueden utilizarlo para facilitar la manipulación de imágenes por parte de los autores de contenido.
uuid: de6ac71b-380a-4b67-b697-ac34a79a9cc4
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: f6347492-cf48-4835-b8fd-ce9a75a09abe
exl-id: af6cf1e0-8901-4621-9f72-e791cb8d68ae
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 16%

---

# Editor de imágenes{#image-editor}

El Editor de imágenes es una pieza central de AEM y los componentes pueden utilizarlo para facilitar la manipulación de imágenes por parte de los autores de contenido.

>[!CAUTION]
>
>Para utilizar las funciones del Editor de imágenes descrito en este artículo, [feature pack 24267](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/cq-6.4.0-featurepack-24267) debe estar instalado.

## Unidades relativas para mapa de imagen {#relative-units-for-image-map}

El Editor de imágenes mantiene las áreas del mapa de imágenes como unidades absolutas y relativas. Las unidades relativas son útiles cuando se proporcionan como atributos de datos para cambiar dinámicamente el tamaño de un mapa de imagen (en relación con el tamaño de la imagen) en el lado del cliente en un componente de imagen interactivo.

### Propiedad imageMap {#imagemap-property}

Las coordenadas del mapa de imagen se mantienen en el JCR como un `imageMap` propiedad del Editor de imágenes. Tiene el siguiente formato.

La propiedad almacena las áreas de asignación de la siguiente manera:

`[area1][area2][...]`

Formato de área:

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

Ejemplo:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## Compatibilidad con imágenes de SVG {#support-for-svg-images}

Los gráficos vectoriales escalables (SVG) son compatibles con el Editor de imágenes.

* Se admiten las funciones de arrastrar y soltar un recurso SVG desde DAM y de cargar un archivo SVG cargado desde un sistema de archivos local.

## Activación de complementos por tipo MIME {#enabling-plugins-by-mime-type}

En determinadas situaciones, las acciones de creación deben restringirse para ciertos tipos de MIME, debido a la falta de compatibilidad con el procesamiento en el servidor. Por ejemplo, es posible que no se permita la edición de imágenes de SVG.

Los complementos del Editor de imágenes se pueden habilitar selectivamente por tipo MIME estableciendo un `supportedMimeTypes` en el nodo de configuración del complemento individual.

### Ejemplo {#example}

Por ejemplo, supongamos que la capacidad de recorte solo debería permitirse para imágenes de GIF, JPEG, PNG, WEBP y TIFF.

La variable `supportedMimeTypes` La propiedad debe establecerse como una cadena de los tipos MIME permitidos en el nodo de configuración del complemento en la variable `cq:editConfig` nodo del componente de imagen.

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
