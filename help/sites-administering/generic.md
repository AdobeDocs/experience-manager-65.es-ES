---
ttitle: Administering generic eCommerce
seo-title: Administración de comercio electrónico genérico
description: La solución genérica de AEM proporciona métodos para administrar la información de comercio contenida en el repositorio.
seo-description: La solución genérica de AEM proporciona métodos para administrar la información de comercio contenida en el repositorio.
uuid: 8d2b02a6-0658-4957-a366-29a59350f3e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 9167cbe2-2efb-422d-b58b-0c24b9476fe6
docset: aem65
translation-type: tm+mt
source-git-commit: 95d9ed8a0ccfa7651b83058d337511dd6b15665f

---


# Administración de comercio electrónico genérico {#administering-generic-ecommerce}

La solución genérica de AEM proporciona métodos para administrar la información de comercio contenida en el repositorio (en lugar de utilizar un motor de comercio electrónico externo). Esto incluye:

* [Productos](/help/sites-administering/concepts.md#products)
* [Variantes del producto](/help/sites-administering/concepts.md#product-variants)
* [Catálogo(s)](/help/sites-administering/concepts.md#catalogs)
* [Promociones](/help/sites-administering/concepts.md#promotions)
* [Cupones](/help/sites-administering/concepts.md#vouchers)
* [Pedidos](/help/sites-administering/concepts.md#shopping-cart-and-orders)
* [Páginas proxy](/help/sites-administering/concepts.md#proxy-pages)

>[!NOTE]
>
>La instalación estándar de AEM incluye la implementación genérica de comercio electrónico de AEM (JCR).
>
>Actualmente, se ha diseñado para fines de demostración o como base básica de una implementación personalizada según sus necesidades.

## Productos y variaciones de producto {#products-and-product-variations}

>[!NOTE]
>
>Los siguientes procedimientos se aplican tanto a los productos como a las variaciones de productos.

Antes de crear productos, debe definir un [scaffold](/help/sites-authoring/scaffolding.md). Esto especifica los campos que necesita para definir los productos y cómo se editan.

Se necesita un scaffold para cada tipo de producto distinto. El scaffold correspondiente se asocia con los productos mediante:

* path
* el producto puede hacer referencia al scaffold

>[!NOTE]
>
>La tienda Geometrixx-Outdoors tiene un solo tipo de producto (y por lo tanto un solo scaffold):
>
>`/etc/scaffolding/geometrixx-outdoors`
>
>El tipo de producto Geometrixx-Outdoors está activo en:
>
>`/etc/commerce/products/geometrixx-outdoors`
>
>Puede crear una nueva definición de producto en cualquier lugar sin ninguna configuración adicional.

### Importing Products {#importing-products}

#### Importación de productos: IU táctil {#importing-products-touch-optimized-ui}

1. Navegue hasta la consola **Productos** , a través de **Comercio**.
1. Con la consola **Productos** vaya a la ubicación requerida.
1. Utilice el icono **Importar productos** para abrir el asistente.

   ![chlimage_1-1](do-not-localize/chlimage_1-13.png)

1. Especifique:

   * **Importador**

      El importador del proveedor [de](/help/sites-administering/concepts.md#commerce-providers)comercio específico, de forma predeterminada `Geometrixx`.

   * **Origen**

      El archivo que desea importar; puede utilizar el explorador para seleccionar un archivo.

   * **Importación incremental**

      Indique si se trata de una importación incremental (a diferencia de la importación completa).
   >[!NOTE]
   >
   >La importación incremental (del importador al aire libre de geometrixx de muestra) funciona a nivel de producto.
   >
   >Se puede definir un importador personalizado para que funcione según sea necesario.

1. Seleccione **Siguiente** para importar los productos y se mostrará un registro de las acciones realizadas.

   >[!NOTE]
   >
   >Los productos se importarán en la ubicación actual o en relación con ella.

   >[!NOTE]
   >
   >Si se utiliza repetidamente **Siguiente** y **Atrás** , se importarán las definiciones del producto. Sin embargo, como tienen los mismos SKU, la información existente en el repositorio simplemente se sobrescribirá.

1. Seleccione **Listo** para cerrar el asistente.

#### Importación de productos: IU clásica {#importing-products-classic-ui}

1. Con la consola **Herramientas** , abra la carpeta **Comercio** .
1. Haga doble clic para abrir el Importador **de productos**:

   ![chlimage_1-22](assets/chlimage_1-22.jpeg)

1. Especifique:

   * **Nombre del almacén**

      Los productos se importarán a:

      `/etc/commerce/products/<*store name*>/`

   * **Proveedor comercial**

      El importador de su proveedor [comercial](/help/sites-administering/concepts.md#commerce-providers); de forma predeterminada, Geometrixx.

   * **Archivo de origen**

      Ubicación en el repositorio del archivo que desea importar.

   * **Importación incremental**

      Indique si se trata de una importación incremental (a diferencia de la importación completa).

1. Haga clic en **Importar productos**.

### Creación de información del producto {#creating-product-information}

>[!NOTE]
>
>La administración de productos estándar es básica, ya que el conjunto de productos Geometrixx-Outdoors se ha mantenido básico. La complejidad se basa en el [andamiaje](/help/sites-authoring/scaffolding.md)del producto, por lo que con su propio andamiaje de productos es posible conseguir una edición más sofisticada.

#### Creación de información del producto: IU táctil {#creating-product-information-touch-optimized-ui}

1. Con la consola **Productos** (a través de **Comercio**) navegue a la ubicación requerida.
1. Utilice el icono **Crear** para seleccionar una de estas opciones (según la estructura y la ubicación):

   * **Crear el producto**
   * **Crear variación de producto**
   ![chlimage_1-14](do-not-localize/chlimage_1-14.png)

1. Se abrirá el asistente. Utilice las fichas **Básico** y **Producto** para introducir los atributos [del](/help/sites-administering/concepts.md#product-attributes) producto para la nueva variante de producto o producto.

   >[!NOTE]
   >
   >**Título** y **SKU** son los requisitos mínimos para crear un producto o una variante.

1. Seleccione **Crear** para guardar la información.

>[!NOTE]
>
>Muchos productos se ofrecen en una gama de colores y/o tamaños. La información sobre el producto básico y las variantes de producto relacionadas se pueden administrar desde la consola **Productos** .
>
>Los productos y sus variantes se almacenan como una estructura de árbol, la información del producto se encuentra en la parte superior, con las variantes debajo (esta estructura la impone la interfaz de usuario).

### Edición de la información del producto {#editing-product-information}

>[!NOTE]
>
>Las imágenes de producto en geometrixx-outdoors se sirven desde:
>
>`/etc/commerce/products/...`
>
>Esto significa que, de forma predeterminada, el [despachante](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)los bloquea, por lo que debe configurarlos según sea necesario.

#### Edición de la información del producto: IU táctil {#editing-product-information-touch-optimized-ui}

1. Con la consola **Productos** (a través de **Comercio**) vaya a la información del producto.
1. Mediante:

   * [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Modo de selección](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)
   Seleccione el icono **Ver datos** del producto:

   ![climage_1-3](do-not-localize/chlimage_1-15.png)

1. Se mostrarán los atributos [](/help/sites-administering/concepts.md#product-attributes) del producto. Utilice **Editar** y **Listo** para realizar cualquier cambio.

### Visualización de referencias del producto {#showing-product-references}

#### Showing Product References - Touch-optimized UI {#showing-product-references-touch-optimized-ui}

1. Con la consola **Productos** (a través de **Comercio**) vaya a la información del producto.
1. Abra el carril secundario de Referencias con el icono:

   ![climage_1-4](do-not-localize/chlimage_1-16.png)

1. Seleccione el producto requerido: el carril secundario se actualizará para mostrar los tipos de referencia disponibles:

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Toque o haga clic en el tipo de referencia (por ejemplo: Páginas de producto) para expandir la lista.
1. Seleccione una referencia específica para mostrar las opciones:

   * Navegar a pág. producto
   * Editar página del producto
   ![chlimage_1-89](assets/chlimage_1-89.png)

### Search for Products {#search-for-products}

1. Navegue hasta la consola **Productos** , a través de **Comercio**.
1. Abra el carril secundario para la búsqueda con el icono:

   ![](do-not-localize/chlimage_1-17.png)

1. Hay varias facetas disponibles para buscar productos. Puede utilizar solo una o varias facetas para una búsqueda. Aparecerán los productos encontrados:

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Al tocar o hacer clic en un producto se abre. También puede publicarla o ver los datos del producto.

#### Ampliación de la búsqueda {#extending-search}

Puede modificar una faceta existente o agregar otra nueva mediante CRXDE Lite:

1. Ir a:

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. Puede modificar, por ejemplo, los tamaños que aparecerán en la página de búsqueda de productos. Haga clic en el `sizegroup` nodo.
1. Haga clic en `items` nodo y, a continuación, haga clic en `propertypredicate` nodo.
1. Puede modificar el `propertyValues`. Por ejemplo, puede agregar XS, XXL o quitar un tamaño.
1. Haga clic en **Guardar todo** y vaya a la página de búsqueda de productos. Deben aparecer los cambios.

### Varios recursos {#multiple-assets}

Puede agregar varios recursos en el componente de producto y luego especificar el recurso que aparecerá en la página de producto.

>[!NOTE]
>
>Todo lo relacionado con varios recursos se realiza con la IU táctil.

#### Adición de varios recursos {#adding-multiple-assets}

1. Navegue hasta la consola **Productos** , a través de **Comercio**.
1. Con la consola **Productos** , vaya al producto requerido.

   >[!NOTE]
   >
   >Debe estar en el nivel de producto, no en el nivel de variante.

1. Toque o haga clic en el icono **Ver datos** del producto con el modo de selección o acciones rápidas.
1. Toque o haga clic en el icono Editar.
1. Desplácese hasta **Agregar**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Toque o haga clic en **Agregar**. Aparece un nuevo marcador de posición de recurso.
1. Al tocar/hacer clic **Cambiar **se abre un cuadro de diálogo que le permite elegir un recurso.
1. Seleccione el recurso que desee agregar.

   >[!NOTE]
   >
   >Los recursos que puede seleccionar proceden de [Recursos](https://helpx.adobe.com/experience-manager/aem-previous-versions.html#assets).

1. Toque o haga clic en el icono Listo.

Dos recursos se almacenan ahora en el componente de producto. Puede configurar cuál aparecerá en la página del producto. Esto funciona con un sistema de categorías. En primer lugar, debe agregar una categoría a los recursos individuales:

1. Toque o haga clic en **Ver datos** del producto.
1. Escriba una categoría **de** recurso debajo de los recursos, por ejemplo `cat1` y `cat2`.

   >[!NOTE]
   >
   >También puede utilizar etiquetas para categorías.

1. Toque o haga clic en el icono Listo. Ahora tiene que [implementar](#rolling-out-a-catalog) los cambios.

Ahora los recursos del componente de producto tienen una categoría. Puede configurar qué categoría se mostrará en tres niveles diferentes:

* [Página de productos](#product-page)
* [Catálogo](#catalog)
* [Consola de productos](#products-console)

>[!NOTE]
>
>Si no establece categorías, el primer recurso se mostrará en la página de productos.

El mecanismo para seleccionar la imagen que se va a mostrar es el siguiente:

1. Compruebe si se ha establecido una categoría para la página de producto.
1. De lo contrario, compruebe si se ha establecido una categoría para el catálogo.
1. Si no es así, compruebe si se ha establecido una categoría para la consola Productos.

>[!NOTE]
>
>Tanto en el nivel de catálogo como en el nivel de consola de productos, debe implementar los cambios para aplicar las modificaciones y ver la diferencia en la página de productos.

#### Página de productos {#product-page}

1. Vaya a la página de productos.
1. **Edite** el componente de producto.
1. Escriba la categoría **de** imagen que ha elegido ( `cat1` por ejemplo).
1. Toque o haga clic en **Hecho**. Se actualizará la página y se mostrará el recurso correcto.

#### Catálogo  {#catalog}

1. Vaya al catálogo.
1. Toque o haga clic en **Ver propiedades**.
1. Tap/click **Edit**.
1. Toque o haga clic en la ficha **Recursos** .
1. Escriba la categoría **de recursos** del producto requerida.
1. Toque o haga clic en **Hecho**.
1. [Despliegue](#rolling-out-a-catalog) los cambios.

#### Consola de productos {#products-console}

1. Con la consola **Productos** , vaya al producto requerido.
1. Toque o haga clic en **Ver datos** del producto.
1. Tap/click **Edit**.
1. Escriba una categoría **de recurso** predeterminada.
1. Toque o haga clic en **Hecho**.
1. [Despliegue](#rolling-out-a-catalog) los cambios.

### Publicación/Cancelación de la publicación de información del producto {#publishing-unpublishing-product-information}

#### Publicación/Cancelación de la publicación de información del producto: IU táctil {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>A menudo, la información del producto se publica a través de las páginas que la hacen referencia. Por ejemplo, al publicar la página X que hace referencia al producto Y, AEM le preguntará si también desea publicar el producto Y.
>
>En casos especiales, AEM también admite la publicación directa a partir de los datos del producto.

1. Con la consola **Productos** (a través de **Comercio**) vaya a la información del producto.
1. Mediante:

   * [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Modo de selección](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)
   Seleccione el icono **Publicar** o **Cancelar publicación** según sea necesario:

   ![chlimage_1-6](do-not-localize/chlimage_1-18.png) ![chlimage_1-7](do-not-localize/chlimage_1-19.png)

   La información del producto se publicará o dejará de publicarse según corresponda.

### Product Feed {#product-feed}

La integración de Search&amp;Promote permite:

* utilice la API de comercio electrónico, independientemente de la estructura de repositorio subyacente y la plataforma de comercio.
* aproveche la función Conector de índice de Search&amp;Promote para proporcionar una fuente de producto en formato XML.
* aproveche la función de control remoto de Search&amp;Promote para realizar solicitudes programadas o a petición de la fuente de productos
* generación de fuentes para distintas cuentas de Search&amp;Promote, configuradas como configuraciones de servicios en la nube.

Para obtener más información, consulte [Alimentación](/help/sites-administering/product-feed.md)de productos.

### Controlador de eventos para actualizaciones de producto {#event-handler-for-product-updates}

Existe un controlador de eventos que registra un evento cuando se agrega, modifica o elimina un producto y cuando se agrega, modifica o elimina una página de producto. Existen los siguientes eventos OSGi:

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

Para los `PRODUCT_*` eventos, la ruta apunta al producto base en `/etc/commerce/products`. Para los `PRODUCT_PAGE_*` eventos, la ruta apunta al `cq:Page` nodo.

Puede verlos en la consola web en eventos OSGI ( `/system/console/events`), por ejemplo:

![](do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>Lea también Gestión [de eventos en AEM](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/). [](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/)

### Imagen con vínculos Añadir a carro {#image-with-add-to-cart-links}

El componente Imagen con vínculos Agregar al carro de compras permite agregar rápidamente un producto al carro de compras mediante la creación de una zona interactiva vinculada con un producto en una imagen.

Al hacer clic en la zona interactiva se abre un cuadro de diálogo que permite elegir el tamaño y la cantidad del producto.

1. Vaya a la página donde desee agregar el componente.
1. Arrastre y suelte el componente en la página.
1. Arrastre y coloque una imagen en el componente desde el navegador [de](/help/sites-authoring/author-environment-tools.md#assets-browser)recursos.
1. Puede:

   * haga clic en el componente y, a continuación, en el icono Editar
   * hacer un doble clic lento

1. Haga clic en el icono de pantalla completa.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Haga clic en el icono Iniciar mapa.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. Haga clic en uno de los iconos de forma.

   ![chlimage_1-21](do-not-localize/chlimage_1-21.png)

1. Modifique y mueva la forma según sea necesario.
1. Haga clic en la forma.
1. Al hacer clic en el icono Examinar, se abre el selector de [recursos](../assets/search-assets.md#assetselector).

   >[!NOTE]
   >
   >Como alternativa, puede escribir directamente la ruta del producto que debe estar en el nivel del producto, no en el nivel de variante.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Haga clic dos veces en el icono de confirmación y, a continuación, haga clic en Salir de pantalla completa.
1. Haga clic en alguna parte de la página junto al componente. La página debe actualizarse y debe ver el siguiente símbolo en la imagen:

   ![](do-not-localize/chlimage_1-22.png)

1. Switch to [preview](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui) mode.
1. Haga clic en el punto interactivo +. Se abre un cuadro de diálogo en el que puede elegir el tamaño y la cantidad del producto introducido en **Ruta**.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Introduzca un tamaño y una cantidad.
1. Haga clic en el botón Agregar al carro de compras. El cuadro de diálogo se cierra.
1. Vaya al carro de compras. El producto debería estar aquí.

#### Configuration Options {#configuration-options}

Puede configurar el aspecto del cuadro de diálogo al hacer clic en el punto interactivo:

1. Haga clic en el componente y en el icono de configuración.

   ![chlimage_1-96](assets/chlimage_1-96.png)

1. Desplazar hacia abajo. Hay una ficha **AGREGAR AL CARRO** .

   ![chlimage_1-97](assets/chlimage_1-97.png)

1. Haga clic en **AGREGAR AL CARRO**. Hay 3 opciones de configuración que puede utilizar.

   ![chlimage_1-98](assets/chlimage_1-98.png)

1. Haga clic en el icono Listo.

## Catálogos {#catalogs}

### Generación de un catálogo {#generating-a-catalog}

#### Generación de un catálogo: IU táctil {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>El catálogo hará referencia a los datos del producto.

Para generar un catálogo:

1.  Abra la consola Sitios (por ejemplo, [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)).
1. Desplácese a la ubicación en la que desee crear la nueva página.
1. Para abrir la lista de opciones, utilice el icono **Crear**:

   ![](do-not-localize/chlimage_1-23.png)

1. From the list select **Create Catalog**, the Create Catalog wizard will open.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Vaya al modelo de catálogo requerido.
1. Toque o haga clic en el botón **Seleccionar** y toque o haga clic en el modelo de catálogo requerido.
1. Tap/click **Next**.

   ![chlimage_1-100](assets/chlimage_1-100.png)

1. Escriba un **Título** y un **Nombre**.
1. Toque o haga clic en el botón **Crear** . Se crea el catálogo y se abre un cuadro de diálogo.

   ![chlimage_1-101](assets/chlimage_1-101.png)

1. Al tocar o hacer clic en el botón **Listo** , volverá a la consola Sitios, donde podrá ver el catálogo.

   Al tocar o hacer clic en el botón **Abrir catálogo** se abre el catálogo (por ejemplo `http://localhost:4502/editor.html/content/test-catalog.html`).

#### Generación de un catálogo: IU clásica {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>El catálogo hará referencia a los datos [del producto](#products-and-product-variants).

1. Con la consola **Sitios** web, vaya al modelo **de catálogo** y, a continuación, al catálogo base.

   Por ejemplo:

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. Cree una nueva página con la plantilla **de modelo de sección** .

   Por ejemplo, `Swimwear`.

1. Abra la nueva `Swimwear` página y haga clic en **Editar modelo** para abrir el cuadro de diálogo **Propiedades** , donde puede configurar la selección de **Productos** .

   Por ejemplo, abra el campo **Etiquetas/Palabras clave** para seleccionar Actividad y, a continuación, Nadar en la sección Geometrixx-Outdoors.

1. Haga clic en **Aceptar** para guardar las propiedades; los productos de ejemplo se mostrarán bajo los criterios **de selección de** productos en la página de modelo.
1. Haga clic en **Desplegar cambios...**, seleccione **Desplegar página y todas las páginas** secundarias y, a continuación, haga clic en **Siguiente** y, a continuación, en **Desplegar**. Una vez que la implementación se haya completado correctamente, el indicador de **estado** se mostrará en verde.
1. Ahora puede hacer clic en **Cerrar** y comprobar la nueva sección del catálogo; por ejemplo, en y debajo:

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. De nuevo, en la página de modelos, haga clic en **Editar modelo** y, en el cuadro de diálogo **Propiedades** , abra la ficha Página **** generada. En el campo Lista de pancartas, seleccione la imagen que desee mostrar; por ejemplo, `summer.jpg`
1. Haga clic en **Aceptar** para guardar las propiedades; la información de la pancarta se mostrará bajo los criterios **de selección de** productos en la página de modelo.
1. Despliegue estos nuevos cambios.

### Despliegue de un catálogo {#rolling-out-a-catalog}

#### Despliegue de un catálogo: IU táctil {#rolling-out-a-catalog-touch-optimized-ui}

Para desplegar un catálogo:

1. Vaya a la consola **Catálogos** , a través de **Comercio**.
1. Vaya al catálogo que desee desplegar.
1. Mediante:

   * [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Modo de selección](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)
   Seleccione el icono **Desplegar cambios** :

   ![](do-not-localize/chlimage_1-24.png)

1. En el asistente, establezca la implementación según sea necesario y toque o haga clic en **Desplegar cambios**.
1. Se abre un cuadro de diálogo. Toque o haga clic en **Hecho** cuando el proceso haya finalizado.

#### Despliegue de un catálogo: IU clásica {#rolling-out-a-catalog-classic-ui}

Para desplegar un catálogo:

1. Vaya al catálogo que desee desplegar. Por ejemplo:

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. Haga clic en **Desplegar cambios...**
1. Configure el despliegue según sea necesario.
1. Haga clic en **Despliegue**.

### Importador de modelo {#blueprint-importer}

#### Importador de modelo: IU táctil {#blueprint-importer-touch-optimized-ui}

1. Vaya a la consola **Catálogos** , a través de **Comercio**.
1. Vaya a la ubicación en la que desea importar el modelo de catálogo.
1. Toque o haga clic en el icono **Importar modelos** .

   ![](do-not-localize/chlimage_1-13.png)

1. En el asistente, seleccione el origen según sea necesario y toque o haga clic en **Siguiente**.

   ![chlimage_1-340](assets/chlimage_1-102.png)

1. Toque o haga clic en **Finalizado** una vez finalizada la importación.

#### Importador de modelo: IU clásica {#blueprint-importer-classic-ui}

1. Con la consola **Herramientas** , vaya a **Comercio**.

   Por ejemplo:

   `http://localhost:4502/miscadmin#/etc/commerce`

1. Abra el Importador **de modelos de** catálogo.
1. Configure la importación según sea necesario.
1. Haga clic en **Importar modelos de catálogo**.

## Promociones {#promotions}

### Creación de una promoción {#creating-a-promotion}

#### Creación de una promoción: IU clásica {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>El siguiente ejemplo trata de una promoción que se lleva a cabo directamente en una [campaña](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md); se utiliza para los cupones.
>
>Una promoción también puede estar en una [experiencia](/help/sites-authoring/personalization.md) dentro de una campaña.
>
>Para obtener más información, consulte [Promociones y Cupones](#promotions-and-vouchers).

1. Abra la consola **Sitios** web de la instancia de creación.
1. En el panel izquierdo, seleccione la **campaña** requerida.
1. Haga clic en **Nuevo**, seleccione la plantilla **Promoción** y luego especifique un **Título** (y **Nombre** si es necesario) para la nueva licencia.
1. Haga clic en **Crear**. La nueva página de promoción se mostrará en el panel derecho.

1. Edite las **propiedades** mediante:

   * abrir la página y, a continuación, hacer clic en el botón Editar para abrir el cuadro de diálogo Propiedades
   * **seleccionando la página en la consola Sitios web, luego utilizando el menú contextual (generalmente el botón secundario del ratón) para seleccionar** Propiedades... y abrir el cuadro de diálogo de propiedades
   Especifique el tipo **de** promoción, el tipo **de** descuento, el valor **de** descuento y cualquier otro campo que sea necesario.

1. Haga clic en **Aceptar** para guardar.

1. Ahora puede activar la promoción para que los compradores la vean en la instancia de publicación.

## Cupones {#vouchers}

### Creación de un cupón {#creating-a-voucher}

#### Creación de un cupón: IU clásica {#creating-a-voucher-classic-ui}

1. Abra la consola **Sitios** web de la instancia de creación.
1. En el panel izquierdo, seleccione la **campaña** requerida.
1. Haga clic en **Nuevo**, seleccione la plantilla **Cupón** y, a continuación, especifique un **Título** (y **Nombre** , si es necesario) para el nuevo cupón.
1. Haga clic en **Crear**. La nueva página de asiento se mostrará en el panel derecho.

1. Abra la nueva página de cupones con un doble clic y luego haga clic en **Editar** para configurar la información según sea necesario.
1. Haga clic en **Aceptar** para guardar.

1. Ahora puede activar la licencia para que los compradores puedan utilizarla en sus carros en la instancia de publicación.

### Eliminando cupones {#removing-vouchers}

#### Eliminación de cupones: IU clásica {#removing-vouchers-classic-ui}

Para que un vale no esté disponible para los clientes, puede:

* Desactive la licencia: permanecerá disponible en el entorno de creación para que pueda reactivarla posteriormente.
* Eliminarlo por completo.

Ambas acciones se pueden realizar desde la consola **Sitios** web.

### Modificación de comprobantes {#modifying-vouchers}

#### Modificación de cupones: IU clásica {#modifying-vouchers-classic-ui}

Para cambiar las propiedades de una licencia o promoción, puede hacer doble clic en ella en la consola **Sitios** web y hacer clic en **Editar**. Después de guardarlo, debe activarlo para que los cambios se inserten en las instancias de publicación.

### Adición de cupones a un carro de compras {#adding-vouchers-to-a-cart}

Para permitir a los usuarios agregar cupones a sus carros, puede utilizar el componente integrado **Cupones** (categoría Comercio). Debe agregarlo a la misma página en la que se muestra el carro de compras (pero no es obligatorio). El componente de cupones es simplemente un formulario en el que el usuario puede introducir un código de asiento, es el componente de carro de compras el que muestra la lista de cupones aplicados y su descuento.

En el sitio de demostración (Geometrixx Outdoors - English) puede ver el formulario de cupones en la página del carro de compras, debajo del carro de compras real.

## Pedidos {#orders}

>[!NOTE]
>
>Debe recordarse que AEM incorporado no tiene acciones necesarias para la funcionalidad estándar relacionada con pedidos, como devolución de mercancías, actualización del estado del pedido, realización de descargas, generación de paquetes. Se trata principalmente de una vista previa de la tecnología.
>
>La gestión genérica de pedidos en AEM se ha mantenido básica; los campos disponibles en el asistente dependen del scaffold:
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>Si crea un scaffold personalizado, puede almacenar más información de pedido.

>[!NOTE]
>
>La consola de pedidos expone la información de pedidos del proveedor, que nunca se publica.
>
>La información del pedido del cliente se guarda en sus directorios principales y se expone en el historial de pedidos de su cuenta. Esta información se publica junto con el resto de su directorio de inicio.

### Creación de la información del pedido {#creating-order-information}

#### Creación de información de pedido: IU táctil {#creating-order-information-touch-optimized-ui}

1. Con la consola **Pedidos** , navegue a la ubicación requerida.
1. Utilice el icono **Crear** para seleccionar **Crear pedido**.

   ![](do-not-localize/chlimage_1-14.png)

1. Se abrirá el asistente. Utilice las fichas **Básico**, **Contenido**, **Pago** y **Cumplimiento** para introducir la [información sobre el nuevo pedido](/help/sites-administering/concepts.md#order-information).

1. Seleccione **Crear** para guardar la información.

### Edición de la información del pedido {#editing-order-information}

#### Edición de la información del pedido: IU táctil {#editing-order-information-touch-optimized-ui}

1. Con la consola **Pedidos** , navegue hasta el orden.
1. Mediante:

   * [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Modo de selección](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)
   Seleccione el icono **Ver datos** de pedido:

   ![](do-not-localize/chlimage_1-15.png)

1. Se mostrará la información [del](/help/sites-administering/concepts.md#order-information) pedido. Utilice **Editar** y **Listo** para realizar cualquier cambio.

