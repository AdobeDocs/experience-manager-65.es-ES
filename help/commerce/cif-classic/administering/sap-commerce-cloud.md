---
title: Commerce Cloud SAP
seo-title: Commerce Cloud SAP
description: Aprenda a utilizar AEM con el Commerce Cloud SAP.
seo-description: Aprenda a utilizar AEM con el Commerce Cloud SAP.
uuid: cee1a781-fcba-461e-a0a4-c561a1dbcbf3
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 1%

---

# Commerce Cloud SAP{#sap-commerce-cloud}

Después de la instalación, puede configurar la instancia:

1. [Configure la Búsqueda facetada de Geometrixx Outdoors](#configure-the-facetted-search-for-geometrixx-outdoors).
1. [Configurar la versión del catálogo](#configure-the-catalog-version).
1. [Configurar la estructura de importación](#configure-the-import-structure).
1. [Configure los Atributos de producto para cargar](#configure-the-product-attributes-to-load).
1. [Importación de datos del producto](#importing-the-product-data).
1. [Configurar el importador de catálogos](#configure-the-catalog-importer).
1. Utilice el [importador para importar el catálogo](#catalog-import) en una ubicación específica de AEM.

## Configurar la búsqueda por facetas de Geometrixx Outdoors {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>Esto no es necesario para hybris 5.3.0.1 y posteriores.

1. En el explorador, vaya a la **consola de administración de híbridos** en:

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. En la barra lateral, seleccione **System**, luego **Facet search** y, a continuación, **Facet Search Config**.
1. **Abra** Editor para la  **configuración de muestras de solr para clothescatalog**.

1. En **Catalog versions** utilice **Add Catalog version** para agregar `outdoors-Staged` y `outdoors-Online` a la lista.
1. **Guarde la configuración.**
1. Abra **Tipos de elementos SOLR** para agregar **Clasificaciones SOLR** a `ClothesVariantProduct`:

   * relevancia (&quot;Relevancia&quot;, puntuación)
   * name-asc (&quot;Nombre (ascendente)&quot;, name)
   * name-desc (&quot;Nombre (descendente)&quot;, name)
   * price-asc (&quot;Precio (ascendente)&quot;, priceValue)
   * price-desc (&quot;Price (descending)&quot;, priceValue)

   >[!NOTE]
   >
   >Utilice el menú contextual (generalmente el botón derecho del ratón) para seleccionar `Create Solr sort`.
   >
   >Para Hybris 5.0.0 abra la pestaña `Indexed Types`, haga doble clic en `ClothesVariantProduct` y luego en la pestaña `SOLR Sort`.

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. En la pestaña **Tipos indexados** establezca el **Tipo compuesto** en:

   `Product - Product`

1. En la pestaña **Indexed Types** , ajuste las **Indexer queries** para `full`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. En la pestaña **Indexed Types** , ajuste las **Indexer queries** para `incremental`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. En la pestaña **Tipos indexados**, ajuste la faceta `category`. Haga doble clic en la última entrada de la lista de categorías para abrir la pestaña **Indexed property**:

   >[!NOTE]
   >
   >Para hybris 5.2, asegúrese de que el atributo `Facet` de la tabla Propiedades está seleccionado según la captura de pantalla siguiente:

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. Abra la pestaña **Configuración de faceta** y ajuste los valores de campo:

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. **Guarde los cambios.**
1. De nuevo, desde **tipos de elementos SOLR**, ajuste la faceta `price` según las siguientes capturas de pantalla. Al igual que con `category`, haga doble clic en `price` para abrir la pestaña **Indexed property**:

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. Abra la pestaña **Configuración de faceta** y ajuste los valores de campo:

   ![imagen_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. **Guarde los cambios.**
1. Abra **System**, **Facet search** y, a continuación, **Indexer operation wizard**. Iniciar un trabajo de secuencia:

   * **Operación** del indexador:  `full`
   * **Configuración** de Solr:  `Sample Solr Config for Clothes`

## Configurar la versión del catálogo {#configure-the-catalog-version}

La **Versión del catálogo** ( `hybris.catalog.version`) importada se puede configurar para el servicio OSGi:

**Configuración de Day CQ Commerce Hybris**
(  `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**Las** versiones del catálogo se suelen establecer en  `Online` o  `Staged` (valor predeterminado).

>[!NOTE]
>
>Al trabajar con AEM hay varios métodos para administrar los ajustes de configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información. Consulte también la consola para obtener una lista completa de los parámetros configurables y sus valores predeterminados.

El resultado del registro proporciona comentarios sobre las páginas y los componentes creados e informa de posibles errores.

## Configurar la estructura de importación {#configure-the-import-structure}

El siguiente listado muestra una estructura de muestra (de recursos, páginas y componentes) creada de forma predeterminada:

```shell
+ /content/dam/path/to/images
  + 12345.jpg (dam:Asset)
    + ...
  + ...
+ /content/site/en
  - cq:commerceProvider = "hybris"
  - cq:hybrisBaseStore = "basestore"
  - cq:hybrisCatalogId = "catalog"
  + category1 (cq:Page)
    + jcr:content (cq:PageContent)
      - jcr:title = "Category 1"
    + category11 (cq:Page)
      + jcr:content (cq:PageContent)
        - jcr:title = "Category 1.1"
      + 12345 (cq:Page)
        + jcr:content (cq:PageContent)
          + par
            + product (nt:unstructured)
              - cq:hybrisProductId = "12345"
              - sling:resourceType = "commerce/components/product"
              + image (nt:unstructured)
                - sling:resourceType = "commerce/components/product/image"
                - fileReference = "/content/dam/path/to/images/12345.jpg"
              + 12345.1-S (nt:unstructured)
                - cq:hybrisProductId = "12345.1-S"
                - sling:resourceType = "commerce/components/product"
                + image (nt:unstructured)
                  - sling:resourceType = "commerce/components/product/image"
                  - fileReference = "/content/dam/path/to/images/12345.1-S.jpg"
              + ...
```

Dicha estructura la crea el servicio OSGi `DefaultImportHandler` que implementa la interfaz `ImportHandler`. El importador real llama a un controlador de importación para crear productos, variaciones de productos, categorías, recursos, etc.

>[!NOTE]
>
>Puede [personalizar este proceso implementando su propio controlador de importación](#configure-the-import-structure).

La estructura que se genera al importar se puede configurar para:

&quot;**Controlador de importación predeterminado de Day CQ Commerce Hybris**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

Al trabajar con AEM hay varios métodos para administrar los ajustes de configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información. Consulte también la consola para obtener una lista completa de los parámetros configurables y sus valores predeterminados.

## Configure los Atributos del producto para que se carguen {#configure-the-product-attributes-to-load}

El analizador de respuestas se puede configurar para definir las propiedades y los atributos que se van a cargar para los productos (variante):

1. Configure el paquete OSGi:

   **Analizador de respuestas predeterminado de Day CQ Commerce Hybris**
 (`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   Aquí puede definir varias opciones y atributos necesarios para la carga y la asignación.

   >[!NOTE]
   >
   >Al trabajar con AEM hay varios métodos para administrar los ajustes de configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información. Consulte también la consola para obtener una lista completa de los parámetros configurables y sus valores predeterminados.

## Importación de los datos del producto {#importing-the-product-data}

Existen varias formas de importar los datos del producto. Los datos del producto se pueden importar al configurar inicialmente el entorno o después de realizar cambios en los datos de híbridos:

* [Importación completa](#full-import)
* [Importación incremental](#incremental-import)
* [Actualización Express](#express-update)

La información real del producto importada de hybris se guarda en el repositorio en:

`/etc/commerce/products`

Las siguientes propiedades indican el vínculo con hybris:

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>La implementación de hybris (p. ej. `geometrixx-outdoors/en_US`) solo almacena los ID de producto y otra información básica en `/etc/commerce`.
>
>Se hace referencia al servidor híbrido cada vez que se solicita información sobre un producto.

### Importación completa {#full-import}

1. Si es necesario, elimine todos los datos de producto existentes mediante el CRXDE Lite .

   1. Vaya al subárbol que contiene los datos del producto:

      `/etc/commerce/products`

      Por ejemplo:

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. Elimine el nodo que contiene los datos del producto; por ejemplo, `outdoors`.
   1. **Guarde** Allen para mantener el cambio.

1. Abra el importador de híbridos en AEM:

   `/etc/importers/hybris.html`

   Por ejemplo:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Configure los parámetros necesarios; por ejemplo:

   ![imagen_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. Haga clic en **Importar catálogo** para iniciar la importación.

   Cuando se complete, puede verificar los datos importados en:

   ```
       /etc/commerce/products/outdoors
   ```

   Puede abrirlo en CRXDE Lite; por ejemplo:

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### Importación incremental {#incremental-import}

1. Compruebe la información contenida en AEM para los productos correspondientes, en el subárbol apropiado, en:

   `/etc/commerce/products`

   Puede abrirlo en CRXDE Lite; por ejemplo:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. En hybris, actualice la información contenida en el producto(s) revelante(s).

1. Abra el importador de híbridos en AEM:

   `/etc/importers/hybris.html`

   Por ejemplo:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Seleccione la casilla **Incremental Import**.
1. Haga clic en **Importar catálogo** para iniciar la importación.

   Una vez finalizados, puede verificar los datos actualizados en AEM en:

   ```
       /etc/commerce/products
   ```


### Actualización exprés {#express-update}

El proceso de importación puede tardar mucho tiempo, por lo que como extensión de la sincronización de productos puede seleccionar áreas específicas del catálogo para una actualización rápida que se activa manualmente. Esto utiliza la fuente de exportación junto con la configuración de atributos estándar.

1. Compruebe la información contenida en AEM para los productos correspondientes, en el subárbol apropiado, en:

   `/etc/commerce/products`

   Puede abrirlo en CRXDE Lite; por ejemplo:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. En hybris, actualice la información contenida en el producto(s) revelante(s).

1. En hybris, añada los productos a la cola Express; por ejemplo:

   ![imagen_1-43](/help/sites-administering/assets/chlimage_1-43a.png)

1. Abra el importador de híbridos en AEM:

   `/etc/importers/hybris.html`

   Por ejemplo:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Seleccione la casilla de verificación **Express Update**.
1. Haga clic en **Importar catálogo** para iniciar la importación.

   Una vez finalizados, puede verificar los datos actualizados en AEM en:

   ```
       /etc/commerce/products
   ```

   ` [](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

## Configurar el importador de catálogos {#configure-the-catalog-importer}

El catálogo de híbris se puede importar en AEM, utilizando el importador de lotes para catálogos, categorías y productos de híbridos.

Los parámetros utilizados por el importador se pueden configurar para:

**Importador de catálogos de Day CQ Commerce Hybris**
(  `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

Al trabajar con AEM hay varios métodos para administrar los ajustes de configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información. Consulte también la consola para obtener una lista completa de los parámetros configurables y sus valores predeterminados.

## Importación del catálogo {#catalog-import}

El paquete hybris incluye un importador de catálogos para configurar la estructura de página inicial.

Esta opción está disponible en:

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](/help/sites-administering/assets/ecommerceimportconsole.png)

Debe proporcionarse la siguiente información:

* **Almacén**
baseIdentificador del almacén base configurado en híbrido.

* ****
CatálogoIdentificador del catálogo que se va a importar.

* **Ruta**
raízRuta en la que se debe importar el catálogo.

## Eliminación de un producto del catálogo {#removing-a-product-from-the-catalog}

Para eliminar uno o más productos del catálogo:

1. [Configure el para OSGi ](/help/sites-deploying/configuring-osgi.md) **serviceDay CQ Commerce Hybris Catalog Importer**; consulte también  [Configuración del importador de catálogos](#configure-the-catalog-importer).

   Active las siguientes propiedades:

   * **Habilitar la eliminación de productos**
   * **Habilitar la eliminación de recursos del producto**

   >[!NOTE]
   >
   >Al trabajar con AEM hay varios métodos para administrar los ajustes de configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información. Consulte también la consola para obtener una lista completa de los parámetros configurables y sus valores predeterminados.

1. Inicialice el importador realizando dos actualizaciones incrementales (consulte [Importación del catálogo](#catalog-import)):

   * El resultado de la primera ejecución es un conjunto de productos modificados, que se indican en la lista de registros.
   * Por segunda vez, no se debe actualizar ningún producto.

   >[!NOTE]
   >
   >La primera importación es inicializar la información del producto. La segunda importación verifica que todo funcionó y que el conjunto de productos está listo.

1. Compruebe la página de categoría que contiene el producto que desea eliminar. Los detalles del producto deben estar visibles.

   Por ejemplo, la siguiente categoría muestra detalles del producto Cajamara:

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. Extraiga el producto en la consola híbrida. Utilice la opción **Change approval status** para establecer el estado en `unapproved`. El producto se eliminará de la fuente en directo.

   Por ejemplo:

   * Abra la página [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit)
   * Seleccione el catálogo `Outdoors Staged`
   * Buscar `Cajamara`
   * Seleccione este producto y cambie el estado de aprobación a `unapproved`

1. Realice otra actualización incremental (consulte [Importación de catálogo](#catalog-import)). El registro enumerará el producto eliminado.
1. [](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) Despliegue el catálogo correspondiente. La página de producto y producto se habrá eliminado de AEM.

   Por ejemplo:

   * Abra:

      [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * Despliegue el catálogo `Hybris Base`
   * Abra:

      [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * El producto `Cajamara` se habrá eliminado de la categoría `Bike`

1. Para volver a instalar el producto:

   1. En hybris, vuelva a establecer el estado de aprobación en **approved**
   1. En AEM:

      1. realizar una actualización incremental
      1. despliegue de nuevo el catálogo correspondiente
      1. actualizar la página de categoría adecuada

## Agregar la característica Historial de pedidos al contexto de cliente {#add-order-history-trait-to-the-client-context}

Para agregar el historial de pedidos a [Client Context](/help/sites-developing/client-context.md):

1. Abra la [página de diseño de contexto de cliente](/help/sites-administering/client-context.md) mediante:

   * Abra una página para editarla y, a continuación, abra ClientContext utilizando **Ctrl-Alt-c** (windows) o **control-option-c** (Mac). Utilice el icono de lápiz en la esquina superior izquierda de ClientContext para **Abrir la página de diseño de ClientContext**.
   * Vaya directamente a [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [Agregue el componente  **Historial de** ](/help/sites-administering/client-context.md#adding-a-property-component) pedidos al componente  **Carro de** compras del contexto de cliente.
1. Puede confirmar que ClientContext muestra detalles del historial de pedidos. Por ejemplo:

   1. Abra [client context](/help/sites-administering/client-context.md).
   1. Agregue un elemento al carro de compras.
   1. Complete el cierre de compra.
   1. Compruebe el contexto del cliente.
   1. Agregue otro artículo al carro de compras.
   1. Vaya a la página de cierre de compra:

      * El contexto del cliente muestra un resumen del historial de pedidos.
      * Se muestra el mensaje &quot;Usted es un cliente que regresa&quot;.

   >[!NOTE]
   >
   >El mensaje se obtiene mediante:
   >
   >* Vaya a [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  La campaña consiste en una experiencia.
   >
   >* Haga clic en el segmento ([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))
      >
      >
   * El segmento se crea con el rasgo **Order History Property**.

