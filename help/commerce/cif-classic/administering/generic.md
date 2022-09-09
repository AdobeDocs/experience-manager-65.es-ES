---
title: Administración del comercio electrónico genérico
seo-title: Administering generic eCommerce
description: La solución genérica AEM proporciona métodos para administrar la información comercial que se encuentra en el repositorio.
seo-description: The AEM generic solution provides methods of managing the commerce information held within the repository.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '2910'
ht-degree: 5%

---

# Administración del comercio electrónico genérico {#administering-generic-ecommerce}

La solución genérica AEM proporciona métodos para administrar la información de comercio que se encuentra en el repositorio (en lugar de utilizar un motor de comercio electrónico externo). Esto incluye:

* [Productos](/help/commerce/cif-classic/administering/concepts.md#products)
* [Variantes del producto](/help/commerce/cif-classic/administering/concepts.md#product-variants)
* [Catálogo(s)](/help/commerce/cif-classic/administering/concepts.md#catalogs)
* [Promociones](/help/commerce/cif-classic/administering/concepts.md#promotions)
* [Cupones](/help/commerce/cif-classic/administering/concepts.md#vouchers)
* [Pedidos](/help/commerce/cif-classic/administering/concepts.md#shopping-cart-and-orders)
* [Páginas proxy](/help/commerce/cif-classic/administering/concepts.md#proxy-pages)

>[!NOTE]
>
>La instalación de AEM estándar incluye la implementación de comercio electrónico de AEM genérica (JCR).
>
>Actualmente está pensado para fines de demostración o como base básica de una implementación personalizada según sus necesidades.

## Productos y variaciones de producto {#products-and-product-variations}

>[!NOTE]
>
>Los siguientes procedimientos se aplican tanto a los productos como a las variaciones de productos.

Antes de crear productos, debe definir una [scaffold](/help/sites-authoring/scaffolding.md). Esto especifica los campos que debe definir los productos y cómo se editan.

Se necesita un scaffold para cada tipo de producto distinto. El scaffold adecuado está asociado con los productos mediante:

* path
* el producto puede hacer referencia al scaffold

>[!NOTE]
>
>La tienda Geometrixx-Outdoors tiene un solo tipo de producto (y, por lo tanto, un solo scaffold):
>
>`/etc/scaffolding/geometrixx-outdoors`
>
>El tipo de producto Geometrixx-exterior está activo en:
>
>`/etc/commerce/products/geometrixx-outdoors`
>
>Puede crear una nueva definición de producto en cualquier lugar bajo ella sin ninguna configuración adicional.

### Importación de productos {#importing-products}

#### Importación de productos: IU táctil {#importing-products-touch-optimized-ui}

1. Vaya a la **Productos** consola, mediante **Comercio**.
1. Al usar la variable **Productos** vaya a la ubicación requerida.
1. Utilice la variable **Importar productos** para abrir el asistente.

   ![Chlimage_1-1](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. Especifique:

   * **Importador**

      El importador para el [proveedor de comercio](/help/commerce/cif-classic/administering/concepts.md#commerce-providers), de forma predeterminada `Geometrixx`.

   * **Origen**

      El archivo que desea importar; puede utilizar el explorador para seleccionar un archivo.

   * **Importación incremental**

      Indique si se trata de una importación incremental (en lugar de una importación completa).
   >[!NOTE]
   >
   >La importación incremental (del importador al aire libre de geometrixx de muestra) funciona a nivel de producto.
   >
   >Se puede definir un importador personalizado para que funcione según sea necesario.

1. Select **Siguiente** para importar los productos, se mostrará un registro de las acciones realizadas.

   >[!NOTE]
   >
   >Los productos se importarán en la ubicación actual o en relación con ella.

   >[!NOTE]
   >
   >Repetidamente utilizando **Siguiente** y **Atrás** importará repetidamente las definiciones de producto. Sin embargo, como tienen los mismos SKU, la información existente en el repositorio simplemente se sobrescribirá.

1. Select **Listo** para cerrar el asistente.

#### Importación de productos: IU clásica {#importing-products-classic-ui}

1. Al usar la variable **Herramientas** abra la consola **Comercio** carpeta.
1. Haga doble clic para abrir el **Importador de productos**:

   ![imagen_1-22](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. Especifique:

   * **Nombre del almacén**

      Los productos se importarán a:

      `/etc/commerce/products/<*store name*>/`

   * **Proveedor comercial**

      El importador para su [proveedor de comercio](/help/commerce/cif-classic/administering/concepts.md#commerce-providers); de forma predeterminada, Geometrixx.

   * **Archivo de origen**

      Ubicación en el repositorio del archivo que desea importar.

   * **Importación incremental**

      Indique si se trata de una importación incremental (en lugar de una importación completa).

1. Haga clic en **Importar productos**.

### Creación de información del producto {#creating-product-information}

>[!NOTE]
>
>La gestión de productos estándar es básica, ya que el conjunto de productos Geometrixx al aire libre se ha mantenido básico. La complejidad se basa en el producto [andamiaje](/help/sites-authoring/scaffolding.md), por lo que con su propio andamiaje de productos es posible lograr una edición más sofisticada.

#### Creación de información del producto: IU táctil {#creating-product-information-touch-optimized-ui}

1. Al usar la variable **Productos** consola (mediante **Comercio**) navegue a la ubicación requerida.
1. Utilice la variable **Crear** para seleccionar una (según la estructura y la ubicación):

   * **Crear el producto**
   * **Crear variación de producto**

   ![imagen_1-14](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. Se abrirá el asistente. Utilice la variable **Básico** y **Pestañas de producto** para introducir el [atributos del producto](/help/commerce/cif-classic/administering/concepts.md#product-attributes) para la nueva variante de producto o producto.

   >[!NOTE]
   >
   >**Título** y **SKU** son el mínimo necesario para crear un producto o una variante.

1. Select **Crear** para guardar la información.

>[!NOTE]
>
>Muchos productos se ofrecen en una gama de colores y/o tamaños. La información sobre el producto básico y las variantes de producto relacionadas se pueden administrar desde el **Productos** consola.
>
>Los productos y sus variantes se almacenan como una estructura de árbol, la información del producto se encuentra en la parte superior, con las variantes debajo (esta estructura la aplica la IU).

### Edición de la información del producto {#editing-product-information}

>[!NOTE]
>
>Las imágenes de producto en geometrixx outdoors se proporcionan desde:
>
>`/etc/commerce/products/...`
>
>Esto significa que, de forma predeterminada, están bloqueados por la variable [dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es), configure como sea necesario.

#### Edición de la información del producto: IU táctil {#editing-product-information-touch-optimized-ui}

1. Al usar la variable **Productos** consola (mediante **Comercio**) vaya a la información del producto.
1. Mediante:

   * [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modo de selección](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleccione el **Ver datos del producto** icono:

   ![Chlimage_1-3](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. La variable [atributos del producto](/help/commerce/cif-classic/administering/concepts.md#product-attributes) se mostrará. Uso **Editar** y **Listo** para realizar cualquier cambio.

### Mostrar referencias del producto {#showing-product-references}

#### Mostrar referencias del producto: IU táctil {#showing-product-references-touch-optimized-ui}

1. Al usar la variable **Productos** consola (mediante **Comercio**) vaya a la información del producto.
1. Abra el carril secundario Referencias con el icono :

   ![Chlimage_1-4](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. Seleccione el producto requerido: el carril secundario se actualizará para mostrar los tipos de referencia disponibles:

   ![chlimage_1-88](/help/sites-administering/assets/chlimage_1-88.png)

1. Toque o haga clic en el tipo de referencia (p. ej. Páginas de producto) para expandir la lista.
1. Seleccione una referencia específica para mostrar las opciones:

   * Navegar a pág. producto
   * Editar página del producto

   ![chlimage_1-89](/help/sites-administering/assets/chlimage_1-89.png)

### Buscar productos {#search-for-products}

1. Vaya a la **Productos** consola, mediante **Comercio**.
1. Abra el carril secundario para Buscar con el icono :

   ![](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. Hay varias facetas disponibles para buscar productos. Solo se pueden usar una o varias facetas para una búsqueda. Aparecerán los productos encontrados:

   ![chlimage_1-90](/help/sites-administering/assets/chlimage_1-90.png)

1. Al tocar o hacer clic en un producto, se abre. También puede publicarlo o ver los datos del producto.

#### Ampliación de la búsqueda {#extending-search}

Puede modificar una faceta existente o agregar otras nuevas mediante el CRXDE Lite :

1. Vaya a:

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. Puede modificar, por ejemplo, los tamaños que aparecerán en la página de búsqueda de productos. Haga clic en el `sizegroup` nodo .
1. Haga clic en `items` nodo y haga clic en `propertypredicate` nodo .
1. Puede modificar el `propertyValues`. Por ejemplo, puede agregar XS o XXL, o quitar un tamaño.
1. Haga clic en **Guardar todo** y vaya a la página de búsqueda de productos. Los cambios deben aparecer.

### Varios recursos {#multiple-assets}

Puede agregar varios recursos en el componente del producto y, a continuación, especificar el recurso que aparecerá en la página del producto.

>[!NOTE]
>
>Todo lo relacionado con varios recursos se realiza con la IU táctil optimizada.

#### Adición de varios recursos {#adding-multiple-assets}

1. Vaya a la **Productos** consola, mediante **Comercio**.
1. Al usar la variable **Productos** , vaya al producto requerido.

   >[!NOTE]
   >
   >Debe estar en el nivel de producto, no en el nivel de variante.

1. Toque o haga clic **Ver datos del producto** con el modo de selección o las acciones rápidas.
1. Toque o haga clic en el icono Editar .
1. Desplácese hasta **Agregar**.

   ![imagen_1-91](/help/sites-administering/assets/chlimage_1-91.png)

1. Toque o haga clic **Agregar**. Aparece un nuevo marcador de posición de recurso.
1. Al tocar o hacer clic en **Cambiar **se abre un cuadro de diálogo que le permite elegir un recurso.
1. Seleccione el recurso que desee añadir.

   >[!NOTE]
   >
   >Los recursos que puede seleccionar proceden de [Recursos](/help/assets/assets.md).

1. Toque o haga clic en el icono Listo .

Dos recursos ahora se almacenan en el componente del producto. Puede configurar cuál aparecerá en la página del producto. Esto funciona con un sistema de categorías. En primer lugar, debe añadir una categoría a los recursos individuales:

1. Toque o haga clic **Ver datos del producto**.
1. Escriba un **Categoría del recurso** en los recursos, por ejemplo `cat1` y `cat2`.

   >[!NOTE]
   >
   >También puede utilizar etiquetas para las categorías.

1. Toque o haga clic en el icono Listo . Ahora tiene que [despliegue](#rolling-out-a-catalog) los cambios.

Ahora los recursos del componente de producto tienen una categoría. Puede configurar qué categoría se mostrará en tres niveles diferentes:

* [Página de productos](#product-page)
* [Catálogo](#catalog)
* [Consola Productos](#products-console)

>[!NOTE]
>
>Si no establece categorías, el primer recurso se mostrará en la página del producto.

El mecanismo para seleccionar la imagen que se va a mostrar es el siguiente:

1. Compruebe si hay una categoría configurada para la página del producto.
1. Si no es así, compruebe si hay una categoría configurada para el catálogo.
1. Si no es así, compruebe si hay una categoría configurada para la consola Productos.

>[!NOTE]
>
>Para los niveles de Catálogo y Consola de productos, debe implementar los cambios para aplicar las modificaciones y ver la diferencia en la página de producto.

#### Página de productos {#product-page}

1. Vaya a la página del producto.
1. **Editar** el componente de producto.
1. Escriba la **Categoría de imagen** ha elegido ( `cat1` por ejemplo).
1. Toque o haga clic **Listo**. La página se actualiza y se debe mostrar el recurso correcto.

#### Catálogo  {#catalog}

1. Vaya al catálogo.
1. Toque o haga clic **Ver propiedades**.
1. Pulse o haga clic en **Editar**.
1. Toque o haga clic en el botón **Recursos** pestaña .
1. Escriba el **Categoría del recurso del producto**.
1. Toque o haga clic **Listo**.
1. [Despliegue](#rolling-out-a-catalog) los cambios.

#### Consola Productos {#products-console}

1. Al usar la variable **Productos** , vaya al producto requerido.
1. Toque o haga clic **Ver datos del producto**.
1. Pulse o haga clic en **Editar**.
1. Tipo a **Categoría de recurso predeterminada**.
1. Toque o haga clic **Listo**.
1. [Despliegue](#rolling-out-a-catalog) los cambios.

### Publicar/cancelar la publicación de información de producto {#publishing-unpublishing-product-information}

#### Publicación/cancelación de la publicación de información del producto: IU táctil {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>A menudo, la información del producto se publica a través de las páginas que hacen referencia a ella. Por ejemplo, al publicar la página X que hace referencia al producto Y, AEM preguntará si también desea publicar el producto Y.
>
>En casos especiales, AEM también admite la publicación directa a partir de los datos del producto.

1. Al usar la variable **Productos** consola (mediante **Comercio**) vaya a la información del producto.
1. Mediante:

   * [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modo de selección](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleccione el **Publicación** o **Cancelar la publicación** como sea necesario:

   ![Chlimage_1-6](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![Chlimage_1-7](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   La información del producto se publicará o dejará de publicarse, según proceda.

<!-- Search&Promote is end of life as of September 1, 2022 ### Product Feed {#product-feed} -->

<!-- Search&Promote is end of life as of September 1, 2022 The Search&Promote integration allows you to: -->

<!-- Search&Promote is end of life as of September 1, 2022 * use the eCommerce API, independently of the underlying repository structure and commerce platform. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Index Connector feature of Search&Promote to provide a product feed in XML format. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Remote Control feature of Search&Promote to perform on-demand or scheduled requests of the product feed -->
<!-- Search&Promote is end of life as of September 1, 2022 * feed generation for different Search&Promote accounts, configured as cloud services configurations. -->

<!-- Search&Promote is end of life as of September 1, 2022 For more information, read [Product Feed](/help/sites-administering/product-feed.md). -->

### Controlador de eventos para actualizaciones de productos {#event-handler-for-product-updates}

Existe un controlador de eventos que registra un evento cuando se agrega, modifica o elimina un producto y cuando se añade, modifica o elimina una página de producto. Existen los siguientes eventos de OSGi:

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

Para la variable `PRODUCT_*` , la ruta apunta al producto base en `/etc/commerce/products`. Para la variable `PRODUCT_PAGE_*` , la ruta señala a la variable `cq:Page` nodo .

Puede verlas en la consola web en los eventos OSGI ( `/system/console/events`), por ejemplo:

![](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>Lea también [Gestión de eventos en AEM](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/).

### Imagen con vínculos Añadir a carro {#image-with-add-to-cart-links}

El componente Imagen con vínculos Agregar al carro de compras le permite agregar rápidamente un producto al carro de compras creando un punto interactivo vinculado a un producto en una imagen.

Al hacer clic en la zona interactiva, se abre un cuadro de diálogo que le permite elegir el tamaño y la cantidad del producto.

1. Desplácese a la página donde desee agregar el componente.
1. Arrastre y suelte el componente en la página .
1. Arrastre y suelte una imagen en el componente desde el [navegador de recursos](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. Puede:

   * haga clic en el componente y, a continuación, en el icono Editar
   * hacer un doble clic lento

1. Haga clic en el icono de pantalla completa.

   ![chlimage_1-92](/help/sites-administering/assets/chlimage_1-92.png)

1. Haga clic en el icono de Launch Map .

   ![imagen_1-93](/help/sites-administering/assets/chlimage_1-93.png)

1. Haga clic en uno de los iconos de forma.

   ![imagen_1-21](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. Modifique y mueva la forma según sea necesario.
1. Haga clic en la forma.
1. Al hacer clic en el icono Examinar se abre la [Selector de recursos](/help/assets/search-assets.md#assetpicker).

   >[!NOTE]
   >
   >Como alternativa, puede escribir directamente la ruta de producto que debe estar en el nivel de producto, no en el nivel de variante.

   ![imagen_1-94](/help/sites-administering/assets/chlimage_1-94.png)

1. Haga clic dos veces en el icono de confirmación y, a continuación, haga clic en salir de pantalla completa.
1. Haga clic en cualquier lugar de la página junto al componente. La página se debe actualizar y debería ver el siguiente símbolo en la imagen:

   ![](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. Cambie a [vista previa](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui) en el menú contextual.
1. Haga clic en el punto interactivo + . Se abre un cuadro de diálogo en el que puede elegir el tamaño y la cantidad del producto introducido **Ruta**.

   ![chlimage_1-95](/help/sites-administering/assets/chlimage_1-95.png)

1. Introduzca un tamaño y una cantidad.
1. Haga clic en el botón Agregar al carro de compras . El cuadro de diálogo se cierra.
1. Vaya al carro de compras. El producto debería estar aquí.

#### Opciones de configuración {#configuration-options}

Puede configurar el aspecto del cuadro de diálogo al hacer clic en el punto interactivo:

1. Haga clic en el componente y en el icono de configuración.

   ![imagen_1-96](/help/sites-administering/assets/chlimage_1-96.png)

1. Desplazar hacia abajo. Hay un **AGREGAR AL CARRO DE COMPRAS** pestaña .

   ![chlimage_1-97](/help/sites-administering/assets/chlimage_1-97.png)

1. Haga clic en **AGREGAR AL CARRO DE COMPRAS**. Puede utilizar tres opciones de configuración.

   ![imagen_1-98](/help/sites-administering/assets/chlimage_1-98.png)

1. Haga clic en el icono Listo .

## Catálogos {#catalogs}

### Generación de un catálogo {#generating-a-catalog}

#### Generación de un catálogo: IU táctil {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>El catálogo hace referencia a los datos del producto.

Para generar un catálogo:

1.  Abra la consola Sitios (por ejemplo, [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)).
1. Desplácese hasta la ubicación en la que desee crear la nueva página.
1. Para abrir la lista de opciones, utilice el icono **Crear**:

   ![create-icon](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. En la lista, seleccione **Crear catálogo**, se abrirá el asistente Crear catálogo .

   ![imagen_1-99](/help/sites-administering/assets/chlimage_1-99.png)

1. Vaya al modelo de catálogo requerido.
1. Toque o haga clic **Select** y pulse o haga clic en el modelo de catálogo requerido.
1. Toque o haga clic **Siguiente**.

   ![chlimage_1-100](/help/sites-administering/assets/chlimage_1-100.png)

1. Tipo a **Título** y **Nombre**.
1. Toque o haga clic en el botón **Crear** botón. Se crea el catálogo y se abre un cuadro de diálogo.

   ![chlimage_1-101](/help/sites-administering/assets/chlimage_1-101.png)

1. Tocar/hacer clic **Listo** le lleva de nuevo a la consola Sitios, donde podrá ver su catálogo.

   Tocar/hacer clic **Abrir catálogo** abre el catálogo (por ejemplo `http://localhost:4502/editor.html/content/test-catalog.html`).

#### Generación de un catálogo: IU clásica {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>El catálogo hará referencia a su [Datos del producto](#products-and-product-variants).

1. Al usar la variable **Sitios web** consola, vaya a la **Modelo de catálogo** y, a continuación, el Catálogo base.

   Por ejemplo:

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. Cree una nueva página utilizando el **Modelo de sección** plantilla.

   Por ejemplo, `Swimwear`.

1. Abra el nuevo `Swimwear` página y, a continuación, haga clic en **Editar modelo** para abrir el **Propiedades** , donde puede configurar la variable **Productos** selección.

   Por ejemplo, abra el **Etiquetas/Palabras clave** para seleccionar Actividad y, a continuación, Nadar desde la sección Geometrixx al aire libre .

1. Haga clic en **OK** para guardar las propiedades; los productos de ejemplo se mostrarán en la sección **Criterios de selección de productos** en la página de modelo.
1. Haga clic en **Desplegar cambios...**, seleccione **Desplegar página y todas las páginas secundarias** y haga clic en **Siguiente** then **Despliegue**. Una vez que la implementación se haya completado correctamente, la variable **Estado** se mostrará como verde.
1. Ahora puede hacer clic en **Cerrar** y compruebe la nueva sección del catálogo; por ejemplo, en y en:

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. Una vez más, desde la página modelos, haga clic en **Editar modelo** y en el **Propiedades** abra el cuadro de diálogo **Página generada** pestaña . En el campo Banner de lista , seleccione la imagen que desee mostrar; por ejemplo, `summer.jpg`
1. Haga clic en **OK** para guardar las propiedades; la información del banner se mostrará en la sección **Criterios de selección de productos** en la página de modelo.
1. Despliegue estos nuevos cambios.

### Despliegue de un catálogo {#rolling-out-a-catalog}

#### Despliegue de un catálogo: IU táctil {#rolling-out-a-catalog-touch-optimized-ui}

Para desplegar un catálogo:

1. Vaya a la **Catálogos** consola, mediante **Comercio**.
1. Desplácese al catálogo que desee desplegar.
1. Mediante:

   * [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modo de selección](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleccione el **Desplegar cambios** icono:

   ![despliegue](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. En el asistente, configure el despliegue como sea necesario y, a continuación, toque o haga clic en **Desplegar cambios**.
1. Se abre un cuadro de diálogo. Toque o haga clic **Listo** cuando el proceso haya finalizado.

#### Despliegue de un catálogo: IU clásica {#rolling-out-a-catalog-classic-ui}

Para desplegar un catálogo:

1. Desplácese al catálogo que desee desplegar. Por ejemplo:

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. Haga clic en **Desplegar cambios...**
1. Defina el despliegue según sea necesario.
1. Haga clic en **Despliegue**.

### Importador de modelo {#blueprint-importer}

#### Importador de modelos: IU táctil {#blueprint-importer-touch-optimized-ui}

1. Vaya a la **Catálogos** consola, mediante **Comercio**.
1. Desplácese a la ubicación en la que desea importar el modelo de catálogo.
1. Toque o haga clic en el botón **Importar modelos** icono.

   ![](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. En el asistente, seleccione el origen según sea necesario y toque o haga clic en **Siguiente**.

   ![chlimage_1-340](/help/sites-administering/assets/chlimage_1-102.png)

1. Toque o haga clic **Listo** una vez finalizada la importación.

#### Importador de modelo: IU clásica {#blueprint-importer-classic-ui}

1. Al usar la variable **Herramientas** consola, vaya a **Comercio**.

   Por ejemplo:

   `http://localhost:4502/miscadmin#/etc/commerce`

1. Abra el **Importador de modelo de catálogo**.
1. Establezca la importación según sea necesario.
1. Haga clic en **Importar modelos de catálogo**.

## Promociones {#promotions}

### Creación de una promoción {#creating-a-promotion}

#### Creación de una promoción: IU clásica {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>El siguiente ejemplo trata una promoción realizada directamente en un [campaign](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md), se utiliza para cupones.
>
>Una promoción también puede estar en una [experiencia](/help/sites-authoring/personalization.md) dentro de una campaña.
>
>Para obtener más información, consulte [Promociones y cupones](#promotions-and-vouchers).

1. Abra el **Sitios web** de la instancia de autor.
1. En el panel izquierdo, seleccione el que desee **Campaign**.
1. Haga clic en **Nuevo**, seleccione **Promoción** plantilla y, a continuación, especifique un **Título** (y **Nombre** si es necesario) para su nuevo cupón.
1. Haga clic en **Crear**. La nueva página de promoción se mostrará en el panel derecho.

1. Edite el **Propiedades** mediante:

   * abrir la página y, a continuación, hacer clic en el botón Editar para abrir el cuadro de diálogo Propiedades
   * seleccionar la página en la consola Sitios web y, a continuación, utilizar el menú contextual (generalmente el botón derecho del ratón) para seleccionar **Propiedades...** y abra el cuadro de diálogo de propiedades

   Especifique la variable **Tipo de promoción**, **Tipo de descuento**, **Valor de descuento** y cualquier otro campo según sea necesario.

1. Haga clic en **Aceptar** para guardar.

1. Ahora puede activar la promoción para que los compradores la vean en la instancia de publicación.

## Cupones {#vouchers}

### Creación de un cupón {#creating-a-voucher}

#### Creación de un cupón: IU clásica {#creating-a-voucher-classic-ui}

1. Abra el **Sitios web** de la instancia de autor.
1. En el panel izquierdo, seleccione el que desee **Campaign**.
1. Haga clic en **Nuevo**, seleccione **Cupón** plantilla y, a continuación, especifique un **Título** (y **Nombre** si es necesario) para su nuevo cupón.
1. Haga clic en **Crear**. La nueva página de cupones se mostrará en el panel derecho.

1. Abra la nueva página de cupones con un doble clic y, a continuación, haga clic en **Editar** para configurar la información según sea necesario.
1. Haga clic en **Aceptar** para guardar.

1. Ahora puede activar el vale, de modo que los compradores puedan utilizarlo en sus carros en la instancia de publicación.

### Eliminación de cupones {#removing-vouchers}

#### Eliminación de cupones: IU clásica {#removing-vouchers-classic-ui}

Para que un vale no esté disponible para los clientes, puede:

* Desactivar el vale - permanecerá disponible en el entorno de creación para que pueda reactivarlo más tarde.
* Eliminarlo por completo.

Ambas acciones se pueden realizar desde el **Sitios web** consola.

### Modificación de comprobantes {#modifying-vouchers}

#### Modificación de cupones: IU clásica {#modifying-vouchers-classic-ui}

Para cambiar las propiedades de un vale o promoción, puede hacer doble clic en él en la **Sitios web** consola y haga clic en **Editar**. Después de guardarlo, debe activarlo para que los cambios se inserten en las instancias de publicación.

### Adición de cupones a un carro de compras {#adding-vouchers-to-a-cart}

Para permitir que los usuarios agreguen cupones a sus carros, puede utilizar el complemento **Cupones** componente (categoría Comercio). Debe agregarlo a la misma página en la que se muestra el carro de compras (pero no es obligatorio). El componente de cupones es simplemente un formulario en el que el usuario puede introducir un código de cupón; es el componente de carro de compras el que muestra la lista de cupones aplicados y su descuento.

En el sitio de demostración (Geometrixx Outdoors - Inglés) puede ver el formulario de cupones en la página del carro de compras, debajo del carro de compras real.

## Pedidos {#orders}

>[!NOTE]
>
>Debe recordarse que las AEM listas para usar no tienen acciones requeridas para la funcionalidad estándar relacionada con pedidos, como devolución de mercancías, actualización del estado de pedidos, realización de entregas, generación de paquetes. Se ha diseñado principalmente como una vista previa de la tecnología.
>
>La gestión genérica de pedidos en AEM se ha mantenido básica; los campos disponibles en el asistente dependen del scaffold:
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>Si crea un scaffold personalizado, puede almacenar más información de pedido.

>[!NOTE]
>
>La consola de pedidos muestra la información de pedidos del proveedor, que nunca se publica.
>
>La información de pedidos de los clientes se guarda en sus directorios principales y se expone en el Historial de pedidos de su cuenta. Esta información se publica junto con el resto de su directorio de inicio.

### Creación de la información del pedido {#creating-order-information}

#### Creación de información del pedido: IU táctil {#creating-order-information-touch-optimized-ui}

1. Al usar la variable **Pedidos** vaya a la ubicación requerida.
1. Utilice la variable **Crear** icono para seleccionar **Crear orden**.

   ![](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. Se abrirá el asistente. Utilice la variable **Básico**, **Contenido**, **Pago** y **Cumplimiento** para especificar [información sobre el nuevo pedido](/help/commerce/cif-classic/administering/concepts.md#order-information).

1. Select **Crear** para guardar la información.

### Edición de la información del orden {#editing-order-information}

#### Edición de la información del orden: IU táctil {#editing-order-information-touch-optimized-ui}

1. Al usar la variable **Pedidos** vaya al orden.
1. Mediante:

   * [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modo de selección](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleccione el **Ver datos de pedido** icono:

   ![](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. La variable [información de pedido](/help/commerce/cif-classic/administering/concepts.md#order-information) se mostrará. Uso **Editar** y **Listo** para realizar cualquier cambio.

