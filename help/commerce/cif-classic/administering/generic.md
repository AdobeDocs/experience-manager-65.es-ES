---
title: Administración de comercio electrónico genérico
description: AEM La solución genérica de la aplicación proporciona métodos para administrar la información comercial que se mantiene dentro del repositorio.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '2907'
ht-degree: 2%

---

# Administración de comercio electrónico genérico {#administering-generic-ecommerce}

La solución genérica de Adobe Experience Manager AEM () proporciona métodos para administrar la información comercial que se mantiene dentro del repositorio (en lugar de utilizar un motor de comercio electrónico externo). Esto incluye:

* [Productos](/help/commerce/cif-classic/administering/concepts.md#products)
* [Variantes del producto](/help/commerce/cif-classic/administering/concepts.md#product-variants)
* [Catálogos](/help/commerce/cif-classic/administering/concepts.md#catalogs)
* [Promociones](/help/commerce/cif-classic/administering/concepts.md#promotions)
* [Cupones](/help/commerce/cif-classic/administering/concepts.md#vouchers)
* [Pedidos](/help/commerce/cif-classic/administering/concepts.md#shopping-cart-and-orders)
* [Páginas proxy](/help/commerce/cif-classic/administering/concepts.md#proxy-pages)

>[!NOTE]
>
>AEM AEM La instalación estándar de la incluye la implementación genérica de comercio electrónico de (JCR).
>
>Se ha diseñado con fines de demostración o como base básica para una implementación personalizada según sus necesidades.

## Productos y variaciones de productos {#products-and-product-variations}

>[!NOTE]
>
>Los siguientes procedimientos se aplican tanto a los productos como a las variaciones de productos.

Antes de crear productos, define un [andamio](/help/sites-authoring/scaffolding.md). Esto especifica los campos que debe definir, los productos y cómo se editan.

Se necesita un andamio para cada tipo de producto distinto. El andamio adecuado está asociado con los productos mediante:

* path
* el producto puede hacer referencia al andamio

>[!NOTE]
>
>La tienda de Geometrixx-Outdoors tiene un solo tipo de producto (y por lo tanto un solo andamio):
>
>`/etc/scaffolding/geometrixx-outdoors`
>
>El tipo de producto de Geometrixx-Outdoors está activo en:
>
>`/etc/commerce/products/geometrixx-outdoors`
>
>Puede crear una definición de producto en cualquier lugar debajo de sin ninguna configuración adicional.

### Importación de productos {#importing-products}

#### Importación de productos: IU táctil optimizada {#importing-products-touch-optimized-ui}

1. Vaya a la consola **Productos** a través de **Commerce**.
1. Con la consola **Productos**, vaya a la ubicación requerida.
1. Use el icono **Importar productos** para abrir el asistente.

   ![Icono Importar productos](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. Especifique:

   * **Importador**

     El importador del [proveedor comercial](/help/commerce/cif-classic/administering/concepts.md#commerce-providers) específico, de forma predeterminada `Geometrixx`.

   * **Origen**

     El archivo que desea importar; puede utilizar el explorador para seleccionar un archivo.

   * **Importación incremental**

     Indique si se trata de una importación incremental (en lugar de una importación completa).

   >[!NOTE]
   >
   >La importación incremental (del importador de muestra de geometrixx-outdoor) funciona en el nivel de producto.
   >
   >Se puede definir un importador personalizado para que funcione según sea necesario.

1. Seleccione **Siguiente** para importar los productos; se mostrará un registro de las acciones realizadas.

   >[!NOTE]
   >
   >Los productos se importan en la ubicación actual o en relación con ella.

   >[!NOTE]
   >
   >Al usar repetidamente **Next** y **Back**, se importan repetidamente las definiciones de productos. Sin embargo, como tienen los mismos SKU, la información existente en el repositorio se sobrescribe.

1. Seleccione **Listo** para cerrar el asistente.

#### Importación de productos: IU clásica {#importing-products-classic-ui}

1. Con la consola **Herramientas**, abra la carpeta **Commerce**.
1. Haga doble clic para abrir **Importador de productos**:

   ![Consola de importador de productos](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. Especifique:

   * **Nombre de tienda**

     Los productos se importan en:

     `/etc/commerce/products/<*store name*>/`

   * **Proveedor de Commerce**

     Geometrixx El importador de su [proveedor comercial](/help/commerce/cif-classic/administering/concepts.md#commerce-providers); de forma predeterminada.

   * **Archivo Source**

     La ubicación en el repositorio del archivo que desea importar.

   * **Importación incremental**

     Indique si se trata de una importación incremental (en lugar de una importación completa).

1. Haga clic en **Importar productos**.

### Creación de información del producto {#creating-product-information}

>[!NOTE]
>
>La administración de productos estándar es básica, ya que el conjunto de productos de Geometrixx-Outdoors se ha mantenido básico. La complejidad se basa en el producto [andamiaje](/help/sites-authoring/scaffolding.md), por lo que con su propio andamiaje de productos es posible lograr una edición más sofisticada.

#### Creación de información del producto: IU táctil optimizada {#creating-product-information-touch-optimized-ui}

1. Con la consola **Productos** (a través de **Commerce**), vaya a la ubicación requerida.
1. Utilice el icono **Crear** para seleccionar (según la estructura y la ubicación):

   * **Crear producto**
   * **Crear variación de producto**

   ![Icono de crear con forma de más](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. Se abre el asistente. Use **Básico** y **Fichas de producto** para introducir los [atributos de producto](/help/commerce/cif-classic/administering/concepts.md#product-attributes) para la nueva variante de producto o producto.

   >[!NOTE]
   >
   >**Title** y **SKU** son los requisitos mínimos para crear un producto o variante.

1. Seleccione **Crear** para guardar la información.

>[!NOTE]
>
>Muchos productos se ofrecen en una gama de colores y / o tamaños. La información sobre el producto básico y las variantes de producto relacionadas se puede administrar desde la consola **Productos**.
>
>Los productos y sus variantes se almacenan como una estructura de árbol, la información del producto se encuentra en la parte superior y las variantes debajo (esta estructura la aplica la interfaz de usuario).

### Edición de información de producto {#editing-product-information}

>[!NOTE]
>
>Las imágenes de productos en geometrixx-outdoors se proporcionan desde:
>
>`/etc/commerce/products/...`
>
>Esto significa que, de forma predeterminada, están bloqueados por [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html), por lo que debe configurarlos según sea necesario.

#### Edición de información de producto: IU táctil optimizada {#editing-product-information-touch-optimized-ui}

1. Con la consola **Productos** (a través de **Commerce**), desplácese hasta la información de su producto.
1. Con:

   * [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modo de selección](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleccione el icono **Ver datos del producto**:

   ![icono de ver datos del producto - icono de información](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. Se muestran [atributos de producto](/help/commerce/cif-classic/administering/concepts.md#product-attributes). Use **Editar** y **Listo** para realizar cualquier cambio.

### Mostrando referencias del producto {#showing-product-references}

#### Mostrando referencias del producto: IU táctil optimizada {#showing-product-references-touch-optimized-ui}

1. Con la consola **Productos** (a través de **Commerce**), desplácese hasta la información de su producto.
1. Abra el carril secundario de Referencias con el icono:

   ![icono de flecha doble](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. Seleccione el producto necesario: las actualizaciones del carril secundario, que muestran los tipos de referencia disponibles:

   ![consola de productos con referencias abiertas](/help/sites-administering/assets/chlimage_1-88.png)

1. Haga clic en el tipo de referencia (por ejemplo, Páginas de producto) para expandir la lista.
1. Seleccione una referencia específica para que pueda mostrar las opciones:

   * Navegar a pág. producto
   * Editar página del producto

   ![Panel de referencia de la consola Productos](/help/sites-administering/assets/chlimage_1-89.png)

### Buscar productos {#search-for-products}

1. Vaya a la consola **Productos** a través de **Commerce**.
1. Abra el carril secundario para Buscar con el icono:

   ![icono de lupa](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. Hay varias facetas disponibles para que busque productos. Para realizar una búsqueda sólo se pueden utilizar una o varias facetas. Aparecen los productos encontrados:

   ![Datos del producto en la consola de productos](/help/sites-administering/assets/chlimage_1-90.png)

1. Al tocar o hacer clic en un producto, se abre. También puede publicarlo o ver los datos del producto.

#### Ampliación de la búsqueda {#extending-search}

Puede modificar una faceta existente o agregar otras nuevas mediante el CRXDE Lite:

1. Vaya a:

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. Puede editar, por ejemplo, los tamaños que aparecen en la página de búsqueda del producto. Haga clic en el nodo `sizegroup`.
1. Haga clic en el nodo `items` y luego en el nodo `propertypredicate`.
1. Puede editar `propertyValues`. Por ejemplo, puede agregar XS o XXL, o quitar un tamaño.
1. Haga clic en **Guardar todo** y vaya a la página de búsqueda de productos. Los cambios deberían aparecer.

### Múltiples Assets {#multiple-assets}

Puede agregar varios recursos en el componente del producto y, a continuación, especificar el recurso que desea que aparezca en la página del producto.

>[!NOTE]
>
>Todo lo relacionado con varios recursos se realiza con la IU táctil optimizada.

#### Adición de varios Assets {#adding-multiple-assets}

1. Vaya a la consola **Productos** a través de **Commerce**.
1. Con la consola **Productos**, desplácese hasta el producto requerido.

   >[!NOTE]
   >
   >Debe estar en el nivel de producto, no de variante.

1. Seleccione el icono **Ver datos del producto** con el modo de selección o acciones rápidas.
1. Seleccione el icono Editar.
1. Desplácese a **Agregar**.

   ![Agregando captura de pantalla de datos del producto](/help/sites-administering/assets/chlimage_1-91.png)

1. Seleccione **Agregar**. Aparece un nuevo marcador de posición de recurso.
1. Al seleccionar **Cambiar**, se abre un cuadro de diálogo que le permite elegir un recurso.
1. Seleccione el recurso que desea agregar.

   >[!NOTE]
   >
   >Los recursos que puede seleccionar se encuentran en [Assets](/help/assets/assets.md).

1. Seleccione el icono Listo.

Ahora hay dos recursos almacenados en el componente del producto. Puede configurar cuál aparece en la página del producto. Esto funciona con un sistema de categorías. Primero debe agregar una categoría a los recursos individuales:

1. Seleccione **Ver datos del producto**.
1. Escriba una **Categoría de recursos** bajo los recursos, por ejemplo, `cat1` y `cat2`.

   >[!NOTE]
   >
   >También puede utilizar etiquetas para las categorías.

1. Seleccione el icono Listo. Ahora tiene que [desplegar](#rolling-out-a-catalog) sus cambios.

Ahora los recursos del componente de producto tienen una categoría. Puede configurar qué categoría se muestra en tres niveles diferentes:

* [Página de productos](#product-page)
* [Catálogo](#catalog)
* [Consola Productos](#products-console)

>[!NOTE]
>
>Si no establece categorías, el primer recurso se muestra en la página del producto.

El mecanismo para seleccionar la imagen que se va a mostrar es el siguiente:

1. Compruebe si hay una categoría configurada para la página de productos.
1. Si no es así, compruebe si hay una categoría configurada para el catálogo.
1. Si no es así, compruebe si hay una categoría configurada para la consola Productos.

>[!NOTE]
>
>Tanto en el nivel de catálogo como en el de consola de productos, debe desplegar los cambios para aplicar las modificaciones y ver la diferencia en la página del producto.

#### Página de productos {#product-page}

1. Vaya a la página del producto.
1. **Editar** el componente del producto.
1. Escriba la **Categoría de imagen** que eligió (`cat1` por ejemplo).
1. Seleccione **Listo**.  La página se actualiza y se debe mostrar el recurso correcto.

#### Catálogo  {#catalog}

1. Vaya al catálogo.
1. Seleccione **Ver propiedades**.
1. Seleccione **Editar**.
1. Seleccione la pestaña **Recursos**.
1. Escriba la **Categoría de recursos del producto** requerida.
1. Seleccione **Listo**.
1. [Despliegue](#rolling-out-a-catalog) sus cambios.

#### Consola Productos {#products-console}

1. Mediante la consola **Productos**, desplácese hasta el Producto requerido.
1. Seleccione **Ver datos del producto**.
1. Seleccione **Editar**.
1. Escriba una **categoría de recursos predeterminada**.
1. Seleccione **Listo**.
1. [Despliegue](#rolling-out-a-catalog) sus cambios.

### Publicar/Cancelar la publicación de información del producto {#publishing-unpublishing-product-information}

#### Publicación/cancelación de la publicación de información de producto: IU táctil optimizada {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>A menudo, la información del producto se publica a través de las páginas que hacen referencia a ella. AEM Por ejemplo, al publicar la página X que hace referencia al producto Y, el usuario pregunta si también desea publicar el producto Y.
>
>AEM Para casos especiales, también admite la publicación directa desde los datos del producto de, lo que también es compatible con la.

1. Con la consola **Productos** (a través de **Commerce**), desplácese hasta la información de su producto.
1. Con:

   * [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modo de selección](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleccione el icono **Publish** o **Cancelar publicación** según sea necesario:

   ![icono del mundo](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![icono del mundo con una cruz - sin signo](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   La información del producto se publica o se cancela su publicación, según corresponda.

<!-- Search&Promote is end of life as of September 1, 2022 ### Product Feed {#product-feed} -->

<!-- Search&Promote is end of life as of September 1, 2022 The Search&Promote integration lets you: -->

<!-- Search&Promote is end of life as of September 1, 2022 * use the eCommerce API, independently of the underlying repository structure and commerce platform. -->
<!-- Search&Promote is end of life as of September 1, 2022 * use the Index Connector feature of Search&Promote to provide a product feed in XML format. -->
<!-- Search&Promote is end of life as of September 1, 2022 * use the Remote Control feature of Search&Promote to perform on-demand or scheduled requests of the product feed -->
<!-- Search&Promote is end of life as of September 1, 2022 * feed generation for different Search&Promote accounts, configured as cloud services configurations. -->

<!-- Search&Promote is end of life as of September 1, 2022 For more information, read [Product Feed](/help/sites-administering/product-feed.md). -->

### Controlador de eventos para actualizaciones de productos {#event-handler-for-product-updates}

Existe un controlador de eventos que registra un evento cuando se agrega, edita o elimina un producto, y cuando se agrega, edita o elimina una página de producto. Hay los siguientes eventos OSGi:

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

Para los eventos `PRODUCT_*`, la ruta de acceso apunta al producto base en `/etc/commerce/products`. Para los eventos `PRODUCT_PAGE_*`, la ruta apunta al nodo `cq:Page`.

Puede verlas en la consola web en eventos OSGI ( `/system/console/events`), por ejemplo:

![ejemplos de eventos OSGI](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>AEM Lea también [Control de eventos en el ](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/) de la página de la aplicación de eventos de la página de.

### La imagen con vínculos Añadir a carro {#image-with-add-to-cart-links}

El componente Imagen con vínculos Añadir al carro de compras permite agregar rápidamente un producto al carro de compras creando un punto interactivo vinculado con un producto en una imagen.

Al hacer clic en el punto interactivo se abre un cuadro de diálogo que le permite elegir el tamaño y la cantidad del producto.

1. Vaya a la página en la que desea agregar el componente.
1. Arrastre y suelte el componente en la página.
1. Arrastre y suelte una imagen en el componente desde el [explorador de recursos](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. Puede:

   * haga clic en el componente y, a continuación, en el icono Editar
   * hacer un doble clic lento

1. Haga clic en el icono de pantalla completa.

   ![icono de pantalla completa](/help/sites-administering/assets/chlimage_1-92.png)

1. Haga clic en el icono Iniciar mapa.

   ![icono de mapa de lanzamiento](/help/sites-administering/assets/chlimage_1-93.png)

1. Haga clic en uno de los iconos de forma.

   ![iconos de forma](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. Modifique y mueva la forma según sea necesario.
1. Haga clic en la forma.
1. Al hacer clic en el icono Examinar, se abre [Selector de recursos](/help/assets/search-assets.md#assetpicker).

   >[!NOTE]
   >
   >Como alternativa, puede escribir directamente la ruta de producto que debe estar en el nivel de producto, no en el de variante.

   ![ruta de acceso de tipo](/help/sites-administering/assets/chlimage_1-94.png)

1. Haga clic en el icono de confirmación dos veces y luego haga clic en salir de pantalla completa.
1. Haga clic en algún lugar de la página junto al componente. La página debería actualizarse y debería ver el siguiente símbolo en su imagen:

   ![símbolo más](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. Cambiar al modo [vista previa](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui).
1. Haga clic en el punto interactivo +. Se abre un cuadro de diálogo en el que puede elegir el tamaño y la cantidad del producto que ha introducido en **Ruta**.

   ![ejemplo de producto: poncho](/help/sites-administering/assets/chlimage_1-95.png)

1. Introduzca un tamaño y una cantidad.
1. Haga clic en el botón Añadir al carro de compras. El cuadro de diálogo se cierra.
1. Vaya al carro de compras. El producto debe estar aquí.

#### Opciones de configuración {#configuration-options}

Puede configurar el aspecto del cuadro de diálogo al hacer clic en el punto interactivo:

1. Haga clic en el componente y haga clic en el icono de configuración.

   ![icono de configuración](/help/sites-administering/assets/chlimage_1-96.png)

1. Desplácese hacia abajo. Hay una ficha **AGREGAR AL CARRO**.

   ![agregar a la ficha de carro](/help/sites-administering/assets/chlimage_1-97.png)

1. Haga clic en **AGREGAR AL CARRO**. Hay tres opciones de configuración que puede utilizar.

   ![opciones de configuración](/help/sites-administering/assets/chlimage_1-98.png)

1. Haga clic en el icono Listo.

## Catálogos {#catalogs}

### Generación de catálogos {#generating-a-catalog}

#### Generación de un catálogo: IU táctil optimizada {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>El catálogo hace referencia a los datos del producto.

Para generar un catálogo:

1. Abra la consola Sitios (por ejemplo, [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)).
1. Vaya a la ubicación en la que desea crear la página.
1. Para abrir la lista de opciones, usa el icono **Crear**:

   ![create-icon](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. En la lista, seleccione **Crear catálogo**. Se abre el asistente Crear catálogo.

   ![crear asistente de catálogo](/help/sites-administering/assets/chlimage_1-99.png)

1. Vaya al modelo de catálogo necesario.
1. Seleccione el botón **Seleccionar** y haga clic en el modelo de catálogo requerido.
1. Seleccione **Siguiente**.

   ![asistente de propiedades de catálogo](/help/sites-administering/assets/chlimage_1-100.png)

1. Escriba **Title** y **Name**.
1. Seleccione el botón **Crear**. Se crea el catálogo y se abre un cuadro de diálogo.

   ![cuadro de diálogo creado en el catálogo](/help/sites-administering/assets/chlimage_1-101.png)

1. Al seleccionar el botón **Listo**, volverá a la consola Sitios, donde podrá ver el catálogo.

   Al tocar o hacer clic en el botón **Abrir catálogo**, se abre el catálogo (por ejemplo, `http://localhost:4502/editor.html/content/test-catalog.html`).

#### Generación de un catálogo: IU clásica {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>El catálogo hace referencia a sus [Datos del producto](#products-and-product-variants).

1. Usando la consola **Sitios web**, vaya a su **Modelo de catálogo** y luego al Catálogo base.

   Por ejemplo:

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. Cree una página con la plantilla **Modelo de sección**.

   Por ejemplo, `Swimwear`.

1. Abra la nueva página de `Swimwear` y luego haga clic en **Editar modelo**. Se abre el cuadro de diálogo **Propiedades** para que pueda configurar la selección de **Productos**.

   Por ejemplo, abra el campo **Etiquetas/Palabras clave** para seleccionar Actividad y, a continuación, Natación en la sección Geometrixx-Naturaleza.

1. Haga clic en **Aceptar** para guardar las propiedades; los productos de ejemplo se muestran bajo los **criterios de selección de productos** en la página de modelo.
1. Haga clic en **Cambios de despliegue...**, seleccione **Página de despliegue y todas las páginas secundarias**, luego haga clic en **Siguiente** y después en **Despliegue**. Una vez que el despliegue se complete correctamente, el indicador **Status** se mostrará en verde.
1. Ahora puede hacer clic en **Cerrar** y comprobar la nueva sección del catálogo; por ejemplo, en:

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. De nuevo desde la página de modelos haga clic en **Editar modelo** y en el cuadro de diálogo **Propiedades** abra la pestaña **Página generada**. En el campo Lista de titulares, seleccione la imagen que desee mostrar; por ejemplo, `summer.jpg`
1. Haga clic en **Aceptar** para guardar las propiedades; la información del banner se muestra en **Criterios de selección de productos** en la página de modelo.
1. Despliegue estos cambios nuevos.

### Despliegue de un catálogo {#rolling-out-a-catalog}

#### Despliegue de un catálogo: IU táctil optimizada {#rolling-out-a-catalog-touch-optimized-ui}

Para desplegar un catálogo:

1. Vaya a la consola **Catálogos** a través de **Commerce**.
1. Desplácese hasta el catálogo que desee desplegar.
1. Con:

   * [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modo de selección](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleccione el icono **Cambios de despliegue**:

   ![despliegue](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. En el asistente, establezca el despliegue según sea necesario y haga clic en **Cambios de despliegue**.
1. Se abre un cuadro de diálogo. Seleccione **Listo** cuando finalice el proceso.

#### Despliegue de un catálogo: IU clásica {#rolling-out-a-catalog-classic-ui}

Para desplegar un catálogo:

1. Desplácese hasta el catálogo que desee desplegar. Por ejemplo:

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. Haga clic en **Cambios de despliegue...**
1. Configure el despliegue según sea necesario.
1. Haga clic en **Despliegue**.

### Importador de modelo {#blueprint-importer}

#### Importador de modelos: IU táctil optimizada {#blueprint-importer-touch-optimized-ui}

1. Vaya a la consola **Catálogos** a través de **Commerce**.
1. Vaya a la ubicación en la que desea importar el modelo de catálogo.
1. Seleccione el icono **Importar modelos**.

   ![Icono de importar modelos](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. En el asistente, seleccione el Source según sea necesario y haga clic en **Siguiente**.

   ![asistente de modelo](/help/sites-administering/assets/chlimage_1-102.png)

1. Seleccione **Listo** cuando finalice la importación.

#### Importador de modelos: IU clásica {#blueprint-importer-classic-ui}

1. Con la consola **Herramientas**, vaya a **Commerce**.

   Por ejemplo:

   `http://localhost:4502/miscadmin#/etc/commerce`

1. Abra **Importador de modelo de catálogo**.
1. Configure la importación según sea necesario.
1. Haga clic en **Importar modelos de catálogo**.

## Promociones {#promotions}

### Creación de una promoción {#creating-a-promotion}

#### Creación de una promoción: IU clásica {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>El siguiente ejemplo trata de una promoción realizada directamente en una [campaña](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md), que se usa para cupones.
>
>Una promoción también puede estar en una [experiencia](/help/sites-authoring/personalization.md) dentro de una campaña.
>
>Para obtener más información, consulte [Promociones y cupones](#promotions-and-vouchers).

1. Abra la consola **Sitios web** de su instancia de autor.
1. En el panel izquierdo, seleccione la **Campaña** que desee.
1. Haz clic en **Nuevo**, selecciona la plantilla de **Promoción** y después especifica un **Título** (y **Nombre** si es necesario) para tu nuevo cupón.
1. Haga clic en **Crear**. La nueva página de promoción se muestra en el panel derecho.

1. Edite las **propiedades** mediante:

   * al abrir la página y, a continuación, hacer clic en el botón Editar para abrir el cuadro de diálogo Propiedades
   * seleccionar la página en la consola Sitios web y, a continuación, utilizar el menú contextual (normalmente el botón secundario del mouse) para seleccionar **Propiedades...** y abrir el cuadro de diálogo de propiedades

   Especifique **Tipo de promoción**, **Tipo de descuento**, **Valor de descuento** y cualquier otro campo según sea necesario.

1. Haga clic en **Aceptar** para guardar.

1. Ahora puede activar la promoción para que los compradores la vean en la instancia de publicación.

## Cupones {#vouchers}

### Creación de un cupón {#creating-a-voucher}

#### Creación de un cupón: IU clásica {#creating-a-voucher-classic-ui}

1. Abra la consola **Sitios web** de su instancia de autor.
1. En el panel izquierdo, seleccione la **Campaña** que desee.
1. Haga clic en **Nuevo**, seleccione la plantilla **Cupón** y, a continuación, especifique un **Título** (y **Nombre** si es necesario) para el nuevo cupón.
1. Haga clic en **Crear**. La nueva página de cupones se muestra en el panel derecho.

1. Abra la nueva página de cupones con un doble clic, luego haga clic en **Editar** y configure la información según sea necesario.
1. Haga clic en **Aceptar** para guardar.

1. Ahora puede activar el cupón para que los compradores puedan utilizarlo en sus carros de compras en la instancia de publicación.

### Eliminación de cupones {#removing-vouchers}

#### Quitar cupones: IU clásica {#removing-vouchers-classic-ui}

Para que un cupón no esté disponible para los clientes, puede:

* Desactive el cupón: permanece disponible en el entorno de creación para que pueda reactivarlo más tarde.
* Elimínelo por completo.

Ambas acciones se pueden realizar desde la consola **Sitios web**.

### Modificación de cupones {#modifying-vouchers}

#### Modificación de cupones: IU clásica {#modifying-vouchers-classic-ui}

Para cambiar las propiedades de un cupón o promoción, puedes hacer doble clic en él en la consola de **Sitios web** y hacer clic en **Editar**. Después de guardarlo, debe activarlo para que los cambios se inserten en las instancias de publicación.

### Adición de cupones a un carro de compras {#adding-vouchers-to-a-cart}

Para permitir que los usuarios agreguen cupones a sus carros de compras, puede usar el componente integrado **Cupones** (categoría Commerce). Añádalo a la misma página donde se muestra el carro de compras (pero esto no es obligatorio). El componente de cupones es simplemente una forma en la que el usuario puede introducir un código de cupón, es el componente del carro de compras el que realmente muestra la lista de cupones aplicados y su descuento.

En el sitio de demostración (Geometrixx Outdoors - Inglés) puede ver el formulario de cupón en la página del carro de compras, debajo del carro de compras real.

## Pedidos {#orders}

>[!NOTE]
>
>AEM Debe tenerse en cuenta que el servicio preestablecido no tiene las acciones necesarias para la funcionalidad estándar relacionada con los pedidos, como devolver mercancía, actualizar el estado del pedido, realizar el cumplimiento o generar albaranes. Está pensado principalmente como una previsualización tecnológica.
>
>El Order Management AEM genérico en el que se ha mantenido la configuración se ha mantenido básica; los campos disponibles en el asistente dependen del andamio:
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>Si crea un andamio personalizado, puede almacenar más información sobre los pedidos.

>[!NOTE]
>
>La consola pedidos expone la información de pedidos del proveedor, que nunca se publica.
>
>La información de pedidos de los clientes se almacena en sus directorios particulares y se expone en el historial de pedidos de su cuenta. Esta información se publica junto con el resto de su directorio de inicio.

### Creación de Información de Pedido {#creating-order-information}

#### Creación de información de pedidos: IU táctil optimizada {#creating-order-information-touch-optimized-ui}

1. Con la consola **Pedidos**, vaya a la ubicación requerida.
1. Utilice el icono **Crear** para seleccionar **Crear pedido**.

   ![Icono de crear con forma de más](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. Se abre el asistente. Use las fichas **Básico**, **Contenido**, **Pago** y **Cumplimiento** para escribir la [información sobre el nuevo pedido](/help/commerce/cif-classic/administering/concepts.md#order-information).

1. Seleccione **Crear** para guardar la información.

### Edición de información de pedidos {#editing-order-information}

#### Edición de información de pedidos: IU táctil optimizada {#editing-order-information-touch-optimized-ui}

1. Con la consola **Pedidos**, vaya al pedido.
1. Con:

   * [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modo de selección](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleccione el icono **Ver datos del pedido**:

   ![icono de información](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. Se muestra [información de pedido](/help/commerce/cif-classic/administering/concepts.md#order-information). Use **Editar** y **Listo** para realizar cualquier cambio.

