---
title: Uso del selector de productos y categorías del CIF
description: Aprenda a utilizar el selector de productos y categorías del CIF en los componentes de comercio del cliente para ayudar a los autores y especialistas en marketing a trabajar de forma eficaz con los datos de catálogos y de productos de comercio.
sub-product: Commerce
topics: Development
version: Cloud Service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 1e7c3748-92b5-45f1-8dd9-f1816e3e34aa
source-git-commit: dceb187ba28ad7c377e98d29d6c815fe37e23077
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# AEM Seleccionadores de creación de contenido y comercio de {#cif-pickers}

AEM AEM La creación de contenido y comercio proporciona un conjunto de herramientas de creación para ayudar a los autores y especialistas en marketing a trabajar de forma eficaz con los datos y catálogos de productos de comercio. El Selector de productos y el Selector de categorías forman parte del complemento CIF y los utilizan los componentes principales del CIF. Los proyectos pueden utilizar estos selectores en cualquier cuadro de diálogo de componente para seleccionar productos o categorías.

## Selector de productos {#product-picker}

Para utilizar el selector de productos en un componente de proyecto, un desarrollador debe agregar `commerce/gui/components/common/cifproductfield` al cuadro de diálogo de componente. Por ejemplo, use lo siguiente para cq:dialog:

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

El campo de producto permite a los usuarios navegar hasta el producto que desean seleccionar a través de las diferentes vistas. De forma predeterminada, el campo product devuelve el ID del producto, pero se puede configurar con la variable `selectionId` atributo.

El campo selector de productos admite las siguientes propiedades opcionales:

- selectionId (id, uid, sku, slug, mergedSlug, mergedSku): permite elegir el atributo de producto que devolverá el selector (predeterminado = id). El uso de SKU devuelve el SKU del producto seleccionado, mientras que el uso de Sku combinado y devuelve una cadena como base#variant con los SKU del producto base y la variante seleccionada, o un único SKU si se selecciona un producto base.
- filter (folderOrProduct, folderOrProductOrVariant): filtra el contenido que el selector procesará al navegar por el árbol de productos. folderOrProduct: procesa carpetas y productos. folderOrProductOrVariant: procesa carpetas, variantes de productos y productos. Si se procesa un producto o una variante de producto, también se puede seleccionar en el selector. (predeterminado = folderOrProduct)
- multiple (true, false): habilita la selección de uno o varios productos (default = false)
- emptyText: para configurar el valor de texto vacío del campo selector

Además, las propiedades de campo de diagnóstico estándar como `name`, `fieldLabel`, o `fieldDescription` también son compatibles.

>[!CAUTION]
>
>El `cifproductfield` el componente requiere el `cif.shell.picker` clientlib. Para agregar clientlib a un cuadro de diálogo, puede utilizar la propiedad extraClientlibs.
>[!CAUTION]
>
>A partir de la versión 2.0.0 de los componentes principales del CIF, la compatibilidad con `id` se ha eliminado y reemplazado por `uid`. Recomendamos encarecidamente utilizar `sku` o `slug` como identificador de producto. Seguimos brindando nuestro apoyo `id` solo para proyectos que utilizan la versión 1.x de los componentes principales del CIF.

Un ejemplo práctico completo de la `cifproductfield` se puede encontrar en la [Componentes principales del CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml) proyecto. Consulte también [Personalización de cuadros de diálogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) AEM de la documentación de componentes principales de la.

## Selector de categoría {#category-picker}

El selector de categorías se puede utilizar en un cuadro de diálogo de componentes de forma similar al selector de productos.

El siguiente fragmento se puede utilizar en una configuración cq:dialog:

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

El campo selector de categorías admite las siguientes propiedades opcionales:

- selectionId(id, uid, slug, urlPath, idAndUrlPath) _(obsoleto)_, uidAndUrlPath _(obsoleto)_): permite elegir el atributo de categoría que el selector devolverá (predeterminado = id).
- multiple (true, false): habilita la selección de una o varias categorías (default = false)

Además, las propiedades de campo de diagnóstico estándar como `name`, `fieldLabel`, o `fieldDescription` también son compatibles.

>[!CAUTION]
>
>Igual que el `cifproductfield` Componente el `cifcategoryfield` Este componente también requiere el `cif.shell.picker` clientlib. Para agregar una clientlib a un cuadro de diálogo, puede utilizar la variable `extraClientlibs` propiedad. Consulte [Personalización de cuadros de diálogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) AEM de la documentación de componentes principales de la.
>[!CAUTION]
>
>A partir de la versión 2.0.0 de los componentes principales del CIF, la compatibilidad con `id` se ha eliminado y reemplazado por `uid`. Recomendamos encarecidamente utilizar `uid` o `urlPath` como identificador de categoría. Seguimos brindando nuestro apoyo `id` &amp; `idAndUrlPath` solo para proyectos que utilizan la versión 1.x de los componentes principales del CIF.

Un ejemplo práctico completo de la `cifcategoryfield` se puede encontrar en la [Componentes principales del CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml) proyecto.
