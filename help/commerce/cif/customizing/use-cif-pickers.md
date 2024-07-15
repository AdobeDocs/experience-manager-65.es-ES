---
title: CIF Uso del selector de productos y categorías de la
description: CIF Aprenda a utilizar el selector de productos y categorías en los componentes de comercio de clientes para ayudar a los autores y especialistas en marketing a trabajar de forma eficaz con los datos de catálogos y de productos de comercio.
sub-product: Commerce
topics: Development
version: Cloud Service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 1e7c3748-92b5-45f1-8dd9-f1816e3e34aa
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# AEM Selector de creación de contenido y Commerce {#cif-pickers}

AEM La creación de contenido y Commerce AEM proporciona un conjunto de herramientas de creación para ayudar a los autores y especialistas en marketing a trabajar de forma eficaz con los datos y los catálogos de productos de comercio. CIF CIF El Selector de productos y el Selector de categorías forman parte de los complementos de productos y son utilizados por los componentes principales de la. Los proyectos pueden utilizar estos selectores en cualquier cuadro de diálogo de componente para seleccionar productos o categorías.

## Selector de productos {#product-picker}

Para usar el selector de productos en un componente de proyecto, un desarrollador debe agregar `commerce/gui/components/common/cifproductfield` a un cuadro de diálogo de componentes. Por ejemplo, use lo siguiente para `cq:dialog`:

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

El campo de producto permite la navegación al producto que un usuario desea seleccionar mediante las diferentes vistas. De forma predeterminada, el campo de producto devuelve el ID del producto, pero se puede configurar con el atributo `selectionId`.

El campo selector de productos admite las siguientes propiedades opcionales:

- selectionId (id, uid, sku, slug, mergedSlug, mergedSku): permite elegir el atributo de producto que devolverá el selector (predeterminado = id). El uso de SKU devuelve el SKU del producto seleccionado, mientras que el uso de Sku combinado y devuelve una cadena como base#variant con los SKU del producto base y la variante seleccionada, o un único SKU si se selecciona un producto base.
- filter (folderOrProduct, folderOrProductOrVariant): filtra el contenido que el selector procesará al navegar por el árbol de productos. folderOrProduct: procesa carpetas y productos. folderOrProductOrVariant: procesa carpetas, productos y variantes de productos. Si se procesa un producto o una variante de producto, también se puede seleccionar en el selector. (predeterminado = folderOrProduct)
- multiple (true, false): habilita la selección de uno o varios productos (default = false)
- emptyText: para configurar el valor de texto vacío del campo selector

Además, también se admiten propiedades de campo de diálogo estándar como `name`, `fieldLabel` o `fieldDescription`.

>[!CAUTION]
>
>El componente `cifproductfield` requiere clientlib `cif.shell.picker`. Para agregar clientlib a un cuadro de diálogo, puede utilizar la propiedad extraClientlibs.
>[!CAUTION]
>
>CIF A partir de la versión 2.0.0 de los componentes principales de la, se quitó la compatibilidad con `id` y se reemplazó con `uid`. El Adobe recomienda usar `sku` o `slug` como identificador de producto. El Adobe CIF de trabajo sigue admitiendo `id` solamente en proyectos que usan la versión 1.x de los componentes principales de la.

CIF Se puede encontrar un ejemplo de trabajo completo de `cifproductfield` en el proyecto de [Componentes principales](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml) de la. AEM Consulte también [Personalización de cuadros de diálogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) de la documentación de los componentes principales de la.

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

- selectionId(id, uid, slug, urlPath, idAndUrlPath _(obsoleto)_, uidAndUrlPath _(obsoleto)_): permite elegir el atributo de categoría que el selector devolverá (predeterminado = id).
- multiple (true, false): habilita la selección de una o varias categorías (default = false)

Además, también se admiten propiedades de campo de diálogo estándar como `name`, `fieldLabel` o `fieldDescription`.

>[!CAUTION]
>
>Igual que el componente `cifproductfield`, el componente `cifcategoryfield` también requiere la clientlib `cif.shell.picker`. Para agregar clientlib a un cuadro de diálogo, puede utilizar la propiedad `extraClientlibs`. AEM Consulte [Personalización de cuadros de diálogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) de la documentación de los componentes principales de la.
>[!CAUTION]
>
>CIF A partir de la versión 2.0.0 de los componentes principales de la, se quitó la compatibilidad con `id` y se reemplazó con `uid`. El Adobe recomienda usar `uid` o `urlPath` como identificador de categoría. El Adobe CIF de trabajo sigue admitiendo `id` y `idAndUrlPath` solamente en proyectos que utilizan la versión 1.x de los componentes principales ().

CIF Se puede encontrar un ejemplo de trabajo completo de `cifcategoryfield` en el proyecto de [Componentes principales](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml) de la.
