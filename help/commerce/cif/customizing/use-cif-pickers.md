---
title: Uso del selector de productos y categorías del CIF
description: Aprenda a utilizar el selector de productos y categorías del CIF en los componentes de comercio de clientes para ayudar a los autores y especialistas en marketing a trabajar de forma eficaz con los datos de catálogos y productos de comercio.
sub-product: Comercio
topics: Development
version: cloud-service
activity: develop
audience: developer
feature: Marco de integración de Commerce
exl-id: 1e7c3748-92b5-45f1-8dd9-f1816e3e34aa
source-git-commit: 61b8d0bf960bd03a19d22061f3c897a56259dd24
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%

---

# Selector de contenido y comercio de AEM {#cif-pickers}

AEM Creación de contenido y comercio proporciona un conjunto de herramientas de creación para ayudar a AEM autores y especialistas en marketing a trabajar de forma eficiente con los datos y catálogos de productos comerciales. El Selector de productos y el Selector de categorías forman parte del complemento CIF y los componentes principales del CIF lo utilizan. Los proyectos pueden utilizar estos selectores en cualquier cuadro de diálogo de componentes para seleccionar productos o categorías.

## Selector de productos {#product-picker}

Para utilizar el selector de productos en un componente de proyecto, un desarrollador debe agregar `commerce/gui/components/common/cifproductfield` a un cuadro de diálogo de componente. Por ejemplo, use lo siguiente para el cq:dialog:

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

El campo de producto permite navegar hasta el producto que un usuario desea seleccionar mediante las diferentes vistas. De forma predeterminada, el campo product devuelve el ID del producto, pero se puede configurar utilizando el atributo `selectionId` .

El campo Selector de producto admite las siguientes propiedades opcionales:

- selectionId (id, uid, sku, anotaciones, combinarSlug, mergeSku) - permite elegir el atributo de producto que el selector devolverá (valor predeterminado = id). Si se utiliza sku, se devuelve el SKU del producto seleccionado, mientras que se utiliza mergeSku y se devuelve una cadena como base#variant con el SKU del producto base y la variante seleccionada, o un sku único si se selecciona un producto base.
- filter (folderOrProduct, folderOrProductOrVariant): filtra el contenido que el selector va a representar mientras navega por el árbol de productos. folderOrProduct: procesa carpetas y productos. folderOrProductOrVariant : procesa carpetas, productos y variantes de producto. Si se representa una variante de producto o producto, también se puede seleccionar en el selector. (predeterminado = folderOrProduct)
- multiple (true, false) : permite la selección de uno o varios productos (default = false)
- emptyText : para configurar el valor de texto vacío del campo de selección

Además, también se admiten propiedades de campo de diagnóstico estándar como `name`, `fieldLabel` o `fieldDescription`.

>[!CAUTION]
>
>El componente `cifproductfield` requiere la clientlib `cif.shell.picker`. Para agregar una clientlib a un cuadro de diálogo, puede utilizar la propiedad extraClientlibs .
>[!CAUTION]
>
>A partir de la versión 2.0.0 de los componentes principales de CIF, la compatibilidad con `id` se eliminó y se reemplazó por `uid`. Se recomienda utilizar `sku` o `slug` como identificador de producto. Seguimos admitiendo `id` solo para proyectos que usan componentes principales del CIF versión 1.x.

Puede encontrar un ejemplo de funcionamiento completo del `cifproductfield` en el proyecto [Componentes principales del CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml). Consulte también [Personalización de cuadros de diálogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) de la documentación de componentes principales de AEM.

## Selector de categoría {#category-picker}

El selector de categorías se puede utilizar en un cuadro de diálogo de componentes de forma similar al selector de productos.

Se puede utilizar el siguiente fragmento de código en una configuración cq:dialog:

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

El campo Selector de categoría admite las siguientes propiedades opcionales:

- selectionId(id, uid, anotaciones, idAndUrlPath, uidAndUrlPath) : permite elegir el atributo de categoría que el selector devolverá (valor predeterminado = id). idAndUrlPath &amp; uidAndUrlPath son opciones especiales que almacenan la categoría id/uid y url_path separadas por una | caracteres como, por ejemplo, 1|hombres/top.
- multiple (true, false) : permite la selección de una o varias categorías (default = false)

Además, también se admiten propiedades de campo de diagnóstico estándar como `name`, `fieldLabel` o `fieldDescription`.

>[!CAUTION]
>
>Al igual que el componente `cifproductfield`, el componente `cifcategoryfield` también requiere la clientlib `cif.shell.picker`. Para agregar una clientlib a un cuadro de diálogo, puede utilizar la propiedad `extraClientlibs`. Consulte [Personalización de cuadros de diálogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) de la documentación de componentes principales de AEM.
>[!CAUTION]
>
>A partir de la versión 2.0.0 de los componentes principales de CIF, la compatibilidad con `id` se eliminó y se reemplazó por `uid`. Se recomienda utilizar `uid` o `slug` como identificador de categoría. Seguimos admitiendo `id` y `idAndUrlPath` solo para proyectos que usan componentes principales del CIF versión 1.x.

Puede encontrar un ejemplo de funcionamiento completo del `cifcategoryfield` en el proyecto [Componentes principales del CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml).
