---
title: Administración del comercio electrónico genérico
seo-title: Administración del comercio electrónico genérico
description: La solución genérica AEM proporciona métodos para administrar la información comercial que se encuentra en el repositorio.
seo-description: La solución genérica AEM proporciona métodos para administrar la información comercial que se encuentra en el repositorio.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '3009'
ht-degree: 4%

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

Antes de crear productos, debe definir un [scaffold](/help/sites-authoring/scaffolding.md). Esto especifica los campos que debe definir los productos y cómo se editan.

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

1. Vaya a la consola **Products** a través de **Commerce**.
1. Con la consola **Products** vaya a la ubicación requerida.
1. Utilice el icono **Importar productos** para abrir el asistente.

   ![Chlimage_1-1](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. Especifique:

   * **Importador**

      El importador para el [proveedor de comercio](/help/commerce/cif-classic/administering/concepts.md#commerce-providers) específico, de forma predeterminada `Geometrixx`.

   * **Origen**

      El archivo que desea importar; puede utilizar el explorador para seleccionar un archivo.

   * **Importación incremental**

      Indique si se trata de una importación incremental (en lugar de una importación completa).
   >[!NOTE]
   >
   >La importación incremental (del importador al aire libre de geometrixx de muestra) funciona a nivel de producto.
   >
   >Se puede definir un importador personalizado para que funcione según sea necesario.

1. Seleccione **Next** para importar los productos, se mostrará un registro de las acciones realizadas.

   >[!NOTE]
   >
   >Los productos se importarán en la ubicación actual o en relación con ella.

   >[!NOTE]
   >
   >Si se utiliza **Next** y **Back** repetidamente, se importarán las definiciones de producto. Sin embargo, como tienen los mismos SKU, la información existente en el repositorio simplemente se sobrescribirá.

1. Seleccione **Listo** para cerrar el asistente.

#### Importación de productos: IU clásica {#importing-products-classic-ui}

1. Con la consola **Tools**, abra la carpeta **Commerce**.
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
>La gestión de productos estándar es básica, ya que el conjunto de productos Geometrixx al aire libre se ha mantenido básico. La complejidad se basa en el producto [scaffolding](/help/sites-authoring/scaffolding.md), por lo que con su propio scaffolding de producto es posible lograr una edición más sofisticada.

#### Creación de información del producto: IU táctil {#creating-product-information-touch-optimized-ui}

1. Mediante la consola **Products** (a través de **Commerce**) vaya a la ubicación requerida.
1. Utilice el icono **Create** para seleccionar cualquiera de los dos (según la estructura y la ubicación):

   * **Crear el producto**
   * **Crear variación de producto**

   ![imagen_1-14](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. Se abrirá el asistente. Utilice las **Fichas de producto** y **Básicas** para introducir los [atributos de producto](/help/commerce/cif-classic/administering/concepts.md#product-attributes) para el nuevo producto o variante de producto.

   >[!NOTE]
   >
   >**** Título y  **** SKU son los requisitos mínimos para crear un producto o una variante.

1. Seleccione **Crear** para guardar la información.

>[!NOTE]
>
>Muchos productos se ofrecen en una gama de colores y/o tamaños. La información sobre el producto básico y las variantes de producto relacionadas se pueden administrar desde la consola **Products**.
>
>Los productos y sus variantes se almacenan como una estructura de árbol, la información del producto se encuentra en la parte superior, con las variantes debajo (esta estructura la aplica la interfaz de usuario).

### Edición de la información del producto {#editing-product-information}

>[!NOTE]
>
>Las imágenes de producto en geometrixx outdoors se proporcionan desde:
>
>`/etc/commerce/products/...`
>
>Esto significa que, de forma predeterminada, el [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html) los bloquea, por lo que debe configurarlos según sea necesario.

#### Edición de la información del producto: IU táctil {#editing-product-information-touch-optimized-ui}

1. Mediante la consola **Products** (a través de **Commerce**) vaya a la información del producto.
1. Mediante:

   * [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Modo de selección](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleccione el icono **Ver datos del producto**:

   ![Chlimage_1-3](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. Se mostrarán los [atributos de producto](/help/commerce/cif-classic/administering/concepts.md#product-attributes). Utilice **Editar** y **Listo** para realizar cualquier cambio.

### Muestra de referencias del producto {#showing-product-references}

#### Muestra de referencias del producto: IU táctil {#showing-product-references-touch-optimized-ui}

1. Mediante la consola **Products** (a través de **Commerce**) vaya a la información del producto.
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

1. Vaya a la consola **Products** a través de **Commerce**.
1. Abra el carril secundario para Buscar con el icono :

   ![](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. Hay varias facetas disponibles para buscar productos. Solo se pueden usar una o varias facetas para una búsqueda. Aparecerán los productos encontrados:

   ![chlimage_1-90](/help/sites-administering/assets/chlimage_1-90.png)

1. Al tocar o hacer clic en un producto, se abre. También puede publicarlo o ver los datos del producto.

#### Ampliación de la búsqueda {#extending-search}

Puede modificar una faceta existente o agregar otras nuevas mediante el CRXDE Lite :

1. Ir a:

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. Puede modificar, por ejemplo, los tamaños que aparecerán en la página de búsqueda de productos. Haga clic en el nodo `sizegroup` .
1. Haga clic en el nodo `items` y, a continuación, haga clic en el nodo `propertypredicate`.
1. Puede modificar el `propertyValues`. Por ejemplo, puede agregar XS o XXL, o quitar un tamaño.
1. Haga clic en **Guardar todo** y vaya a la página de búsqueda de productos. Los cambios deben aparecer.

### Recursos múltiples {#multiple-assets}

Puede agregar varios recursos en el componente del producto y, a continuación, especificar el recurso que aparecerá en la página del producto.

>[!NOTE]
>
>Todo lo relacionado con varios recursos se realiza con la IU táctil optimizada.

#### Adición de varios recursos {#adding-multiple-assets}

1. Vaya a la consola **Products** a través de **Commerce**.
1. Mediante la consola **Products**, vaya al producto requerido.

   >[!NOTE]
   >
   >Debe estar en el nivel de producto, no en el nivel de variante.

1. Toque o haga clic en el icono **Ver datos del producto** con el modo de selección o las acciones rápidas.
1. Toque o haga clic en el icono Editar .
1. Desplácese a **Add**.

   ![imagen_1-91](/help/sites-administering/assets/chlimage_1-91.png)

1. Toque o haga clic en **Agregar**. Aparece un nuevo marcador de posición de recurso.
1. Al tocar o hacer clic en **Cambiar **se abre un cuadro de diálogo que le permite elegir un recurso.
1. Seleccione el recurso que desee añadir.

   >[!NOTE]
   >
   >Los recursos que puede seleccionar proceden de [Assets](/help/assets/assets.md).

1. Toque o haga clic en el icono Listo .

Dos recursos ahora se almacenan en el componente del producto. Puede configurar cuál aparecerá en la página del producto. Esto funciona con un sistema de categorías. En primer lugar, debe añadir una categoría a los recursos individuales:

1. Toque o haga clic en **Ver datos del producto**.
1. Escriba una **Categoría del recurso** en los recursos, por ejemplo `cat1` y `cat2`.

   >[!NOTE]
   >
   >También puede utilizar etiquetas para las categorías.

1. Toque o haga clic en el icono Listo . Ahora tiene que [desplegar](#rolling-out-a-catalog) los cambios.

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
1. **** Edite el componente del producto.
1. Escriba la **Categoría de imagen** que eligió ( `cat1` por ejemplo).
1. Toque o haga clic en **Listo**. La página se actualiza y se debe mostrar el recurso correcto.

#### Catálogo  {#catalog}

1. Vaya al catálogo.
1. Toque o haga clic en **Ver propiedades**.
1. Toque o haga clic en **Editar**.
1. Toque o haga clic en la pestaña **Assets**.
1. Escriba la **Categoría del recurso del producto** necesaria.
1. Toque o haga clic en **Listo**.
1. [](#rolling-out-a-catalog) Despliegue los cambios.

#### Consola Productos {#products-console}

1. Mediante la consola **Products**, vaya al producto requerido.
1. Toque o haga clic en **Ver datos del producto**.
1. Toque o haga clic en **Editar**.
1. Escriba **Categoría de recurso predeterminada**.
1. Toque o haga clic en **Listo**.
1. [](#rolling-out-a-catalog) Despliegue los cambios.

### Publicar/cancelar la publicación de información de producto {#publishing-unpublishing-product-information}

#### Publicación/Cancelación de la publicación de información del producto: IU táctil {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>A menudo, la información del producto se publica a través de las páginas que hacen referencia a ella. Por ejemplo, al publicar la página X que hace referencia al producto Y, AEM preguntará si también desea publicar el producto Y.
>
>En casos especiales, AEM también admite la publicación directa a partir de los datos del producto.

1. Mediante la consola **Products** (a través de **Commerce**) vaya a la información del producto.
1. Mediante:

   * [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Modo de selección](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleccione el icono **Publicar** o **Cancelar publicación** según sea necesario:

   ![chlimage_1-6](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![chlimage_1-7](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   La información del producto se publicará o dejará de publicarse, según proceda.

### Fuente de productos {#product-feed}

La integración de Search&amp;Promote le permite:

* utilice la API de comercio electrónico, independientemente de la estructura de repositorios subyacente y la plataforma de comercio.
* utilice la función Conector de índice de Search&amp;Promote para proporcionar una fuente de producto en formato XML.
* aproveche la función Control remoto de Search&amp;Promote para realizar solicitudes programadas o bajo demanda de la fuente de productos
* generación de fuentes para distintas cuentas de Search&amp;Promote, configuradas como configuraciones de servicios en la nube.

Para obtener más información, lea [Fuente de productos](/help/sites-administering/product-feed.md).

### Controlador de eventos para actualizaciones de producto {#event-handler-for-product-updates}

Existe un controlador de eventos que registra un evento cuando se agrega, modifica o elimina un producto y cuando se añade, modifica o elimina una página de producto. Existen los siguientes eventos de OSGi:

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

Para los eventos `PRODUCT_*` , la ruta señala al producto base en `/etc/commerce/products`. Para los eventos `PRODUCT_PAGE_*`, la ruta apunta al nodo `cq:Page`.

Puede verlas en la consola web en los eventos OSGI ( `/system/console/events`), por ejemplo:

![](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>Lea también [Gestión de eventos en AEM](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/). [](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/)

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
1. Al hacer clic en el icono Examinar se abre el [Selector de recursos](/help/assets/search-assets.md#assetpicker).

   >[!NOTE]
   >
   >Como alternativa, puede escribir directamente la ruta de producto que debe estar en el nivel de producto, no en el nivel de variante.

   ![imagen_1-94](/help/sites-administering/assets/chlimage_1-94.png)

1. Haga clic dos veces en el icono de confirmación y, a continuación, haga clic en salir de pantalla completa.
1. Haga clic en cualquier lugar de la página junto al componente. La página se debe actualizar y debería ver el siguiente símbolo en la imagen:

   ![](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. Cambie al modo [preview](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui).
1. Haga clic en el punto interactivo + . Se abre un cuadro de diálogo en el que puede elegir el tamaño y la cantidad del producto introducido en **Path**.

   ![chlimage_1-95](/help/sites-administering/assets/chlimage_1-95.png)

1. Introduzca un tamaño y una cantidad.
1. Haga clic en el botón Agregar al carro de compras . El cuadro de diálogo se cierra.
1. Vaya al carro de compras. El producto debería estar aquí.

#### Opciones de configuración {#configuration-options}

Puede configurar el aspecto del cuadro de diálogo al hacer clic en el punto interactivo:

1. Haga clic en el componente y en el icono de configuración.

   ![imagen_1-96](/help/sites-administering/assets/chlimage_1-96.png)

1. Desplazar hacia abajo. Hay una pestaña **ADD TO CART**.

   ![chlimage_1-97](/help/sites-administering/assets/chlimage_1-97.png)

1. Haga clic en **AGREGAR AL CARRO**. Puede utilizar tres opciones de configuración.

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

1. En la lista seleccione **Crear catálogo**, se abrirá el asistente Crear catálogo.

   ![imagen_1-99](/help/sites-administering/assets/chlimage_1-99.png)

1. Vaya al modelo de catálogo requerido.
1. Pulse o haga clic en el botón **Seleccionar** y pulse o haga clic en el modelo de catálogo requerido.
1. Toque o haga clic en **Siguiente**.

   ![chlimage_1-100](/help/sites-administering/assets/chlimage_1-100.png)

1. Escriba un **Título** y un **Nombre**.
1. Toque o haga clic en el botón **Create**. Se crea el catálogo y se abre un cuadro de diálogo.

   ![chlimage_1-101](/help/sites-administering/assets/chlimage_1-101.png)

1. Al pulsar o hacer clic en el botón **Listo** regresa a la consola Sitios donde podrá ver su catálogo.

   Al pulsar o hacer clic en el botón **Abrir catálogo** se abre el catálogo (por ejemplo `http://localhost:4502/editor.html/content/test-catalog.html`).

#### Generación de un catálogo: IU clásica {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>El catálogo hará referencia a sus [Datos del producto](#products-and-product-variants).

1. Mediante la consola **Sitios web**, vaya al **Modelo de catálogo** y, a continuación, al Catálogo base.

   Por ejemplo:

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. Cree una nueva página con la plantilla **Section Blueprint** .

   Por ejemplo, `Swimwear`.

1. Abra la nueva página `Swimwear` y haga clic en **Editar modelo** para abrir el cuadro de diálogo **Propiedades**, donde puede configurar la selección **Productos**.

   Por ejemplo, abra el campo **Etiquetas/Palabras clave** para seleccionar Actividad y, a continuación, Nadar desde la sección Geometrixx exteriores.

1. Haga clic en **OK** para guardar sus propiedades; los productos de ejemplo se mostrarán en los **Criterios de selección de productos** en la página de modelo.
1. Haga clic en **Rollout Changes...**, seleccione **Despliegue de página y todas las páginas secundarias**, haga clic en **Siguiente** y, a continuación, en **Despliegue**. Una vez completado el despliegue correctamente, el indicador **Status** se mostrará como verde.
1. Ahora puede hacer clic en **Close** y comprobar la nueva sección del catálogo; por ejemplo, en y en:

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. De nuevo, en la página modelos, haga clic en **Editar modelo** y, en el cuadro de diálogo **Propiedades**, abra la pestaña **Página generada**. En el campo Banner de lista , seleccione la imagen que desee mostrar; por ejemplo, `summer.jpg`
1. Haga clic en **OK** para guardar sus propiedades; la información del banner se mostrará en los **Criterios de selección de productos** en la página del modelo.
1. Despliegue estos nuevos cambios.

### Despliegue de un catálogo {#rolling-out-a-catalog}

#### Despliegue de un catálogo: IU táctil {#rolling-out-a-catalog-touch-optimized-ui}

Para desplegar un catálogo:

1. Vaya a la consola **Catálogos** a través de **Comercio**.
1. Desplácese al catálogo que desee desplegar.
1. Mediante:

   * [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Modo de selección](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleccione el icono **Rollout Changes**:

   ![despliegue](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. En el asistente, configure el despliegue según sea necesario y, a continuación, toque o haga clic en **Desplegar cambios**.
1. Se abre un cuadro de diálogo. Toque o haga clic en **Listo** cuando finalice el proceso.

#### Despliegue de un catálogo: IU clásica {#rolling-out-a-catalog-classic-ui}

Para desplegar un catálogo:

1. Desplácese al catálogo que desee desplegar. Por ejemplo:

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. Haga clic en **Desplegar cambios...**
1. Defina el despliegue según sea necesario.
1. Haga clic en **Despliegue**.

### Importador de modelo {#blueprint-importer}

#### Importador de modelo: IU táctil {#blueprint-importer-touch-optimized-ui}

1. Vaya a la consola **Catálogos** a través de **Comercio**.
1. Desplácese a la ubicación en la que desea importar el modelo de catálogo.
1. Pulse o haga clic en el icono **Import Blueprints**.

   ![](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. En el asistente, seleccione el Origen según sea necesario y pulse o haga clic en **Siguiente**.

   ![chlimage_1-340](/help/sites-administering/assets/chlimage_1-102.png)

1. Toque o haga clic en **Listo** una vez finalizada la importación.

#### Importador de modelo: IU clásica {#blueprint-importer-classic-ui}

1. Mediante la consola **Tools**, vaya a **Commerce**.

   Por ejemplo:

   `http://localhost:4502/miscadmin#/etc/commerce`

1. Abra **Catalog Bluprint Importer**.
1. Establezca la importación según sea necesario.
1. Haga clic en **Importar modelos de catálogo**.

## Promociones {#promotions}

### Creación de una promoción {#creating-a-promotion}

#### Creación de una promoción: IU clásica {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>El siguiente ejemplo trata de una promoción llevada a cabo directamente en una [campaña](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md), que se utiliza para los comprobantes.
>
>Una promoción también puede estar en una [experiencia](/help/sites-authoring/personalization.md) dentro de una campaña.
>
>Para obtener más información, consulte [Promociones y Cupones](#promotions-and-vouchers).

1. Abra la consola **Sitios web** de la instancia de autor.
1. En el panel izquierdo, seleccione la **Campaña** requerida.
1. Haga clic en **Nuevo**, seleccione la plantilla **Promoción** y, a continuación, especifique un **Título** (y **Nombre** si es necesario) para el nuevo cupón.
1. Haga clic en **Crear**. La nueva página de promoción se mostrará en el panel derecho.

1. Edite las **Propiedades** mediante:

   * abrir la página y, a continuación, hacer clic en el botón Editar para abrir el cuadro de diálogo Propiedades
   * seleccionando la página en la consola Sitios web y utilizando el menú contextual (generalmente el botón derecho del ratón) para seleccionar **Propiedades...** y abra el cuadro de diálogo de propiedades

   Especifique el **Tipo de promoción**, **Tipo de descuento**, **Valor de descuento** y cualquier otro campo según sea necesario.

1. Haga clic en **Aceptar** para guardar.

1. Ahora puede activar la promoción para que los compradores la vean en la instancia de publicación.

## Cupones {#vouchers}

### Creación de un cupón {#creating-a-voucher}

#### Creación de un cupón: IU clásica {#creating-a-voucher-classic-ui}

1. Abra la consola **Sitios web** de la instancia de autor.
1. En el panel izquierdo, seleccione la **Campaña** requerida.
1. Haga clic en **Nuevo**, seleccione la plantilla **Cupón** y, a continuación, especifique un **Título** (y **Nombre** si es necesario) para el nuevo cupón.
1. Haga clic en **Crear**. La nueva página de cupones se mostrará en el panel derecho.

1. Abra la nueva página de cupones con un doble clic y haga clic en **Editar** para configurar la información según sea necesario.
1. Haga clic en **Aceptar** para guardar.

1. Ahora puede activar el vale, de modo que los compradores puedan utilizarlo en sus carros en la instancia de publicación.

### Eliminación de comprobantes {#removing-vouchers}

#### Eliminación de cupones: IU clásica {#removing-vouchers-classic-ui}

Para que un vale no esté disponible para los clientes, puede:

* Desactivar el vale - permanecerá disponible en el entorno de creación para que pueda reactivarlo más tarde.
* Eliminarlo por completo.

Ambas acciones se pueden realizar desde la consola **Sitios web**.

### Modificación de contadores {#modifying-vouchers}

#### Modificación de comprobadores: IU clásica {#modifying-vouchers-classic-ui}

Para cambiar las propiedades de un vale o promoción, puede hacer doble clic en él en la consola **Sitios web** y hacer clic en **Editar**. Después de guardarlo, debe activarlo para que los cambios se inserten en las instancias de publicación.

### Adición de cupones a un carro {#adding-vouchers-to-a-cart}

Para permitir que los usuarios agreguen comprobantes a sus carros, puede utilizar el componente integrado **Cupones** (categoría Comercio). Debe agregarlo a la misma página en la que se muestra el carro de compras (pero no es obligatorio). El componente de cupones es simplemente un formulario en el que el usuario puede introducir un código de cupón; es el componente de carro de compras el que muestra la lista de cupones aplicados y su descuento.

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

### Creación de Información de Pedido {#creating-order-information}

#### Creación de información de pedido: IU táctil {#creating-order-information-touch-optimized-ui}

1. Con la consola **Orders** vaya a la ubicación requerida.
1. Utilice el icono **Crear** para seleccionar **Crear orden**.

   ![](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. Se abrirá el asistente. Utilice las pestañas **Básico**, **Contenido**, **Pago** y **Cumplimiento** para introducir la [información sobre el nuevo pedido](/help/commerce/cif-classic/administering/concepts.md#order-information).

1. Seleccione **Crear** para guardar la información.

### Edición de la información del pedido {#editing-order-information}

#### Edición de la información del orden: IU táctil {#editing-order-information-touch-optimized-ui}

1. Con la consola **Pedidos** vaya al orden.
1. Mediante:

   * [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Modo de selección](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleccione el icono **Ver datos de pedido**:

   ![](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. Se mostrará la [información de pedido](/help/commerce/cif-classic/administering/concepts.md#order-information). Utilice **Editar** y **Listo** para realizar cualquier cambio.

