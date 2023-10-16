---
title: AEM Uso con el Commerce Cloud de SAP
description: Aprenda a utilizar Adobe Experience Manager con SAP Commerce Cloud.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: c342f789-2ff7-4802-99c7-c3699218fe47
source-git-commit: 3400df1ecd545aa0fb0e3fcdcc24f629ce4c99ba
workflow-type: tm+mt
source-wordcount: '1704'
ht-degree: 1%

---

# COMMERCE CLOUD SAP{#sap-commerce-cloud}

Después de la instalación puede configurar la instancia:

1. [Configuración de la búsqueda con facetas para Geometrixx Outdoors](#configure-the-facetted-search-for-geometrixx-outdoors).
1. [Configurar la versión del catálogo](#configure-the-catalog-version).
1. [Configuración de la estructura de importación](#configure-the-import-structure).
1. [Configurar los atributos del producto para cargar](#configure-the-product-attributes-to-load).
1. [Importación de los datos del producto](#importing-the-product-data).
1. [Configuración del importador de catálogos](#configure-the-catalog-importer).
1. Utilice el [importador para importar el catálogo](#catalog-import) AEM a una ubicación específica en el área de trabajo de la.

## Configuración de la búsqueda con facetas para Geometrixx Outdoors {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>No es necesario para hybris 5.3.0.1 y versiones posteriores.

1. En el explorador, vaya a **consola de administración de hybris** a las:

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. En la barra lateral, seleccione **Sistema**, entonces **Búsqueda de facetas**, entonces **Configuración de búsqueda de facetas**.
1. **Abrir editor** para el **Ejemplo de configuración de Solr para el catálogo de ropa**.

1. En **Versiones de catálogo** use **Añadir versión del catálogo** para agregar `outdoors-Staged` y `outdoors-Online` a la lista.
1. **Guarde la configuración.**
1. Abrir **Tipos de artículos de SOLR** para agregar **Clasificaciones de SOLR** hasta `ClothesVariantProduct`:

   * relevancia (&quot;Relevancia&quot;, puntuación)
   * name-asc (&quot;Nombre (ascendente)&quot;, nombre)
   * name-desc (&quot;Nombre (descendente)&quot;, nombre)
   * price-asc (&quot;Precio (ascendente)&quot;, priceValue)
   * price-desc (&quot;Precio (descendente)&quot;, priceValue)

   >[!NOTE]
   >
   >Utilice el menú contextual (normalmente clic con el botón derecho) para seleccionar `Create Solr sort`.
   >
   >Para Hybris 5.0.0, abra el `Indexed Types` pestaña, haga doble clic en `ClothesVariantProduct`, luego la pestaña `SOLR Sort`.

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. En el **Tipos indexados** pestaña, configure el **Tipo compuesto** hasta:

   `Product - Product`

1. En el **Tipos indexados** pestaña, ajuste el **Consultas del indexador** para `full`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. En el **Tipos indexados** pestaña, ajuste el **Consultas del indexador** para `incremental`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. En el **Tipos indexados** pestaña, ajuste el `category` faceta. Haga doble clic en la última entrada de la lista de categorías para abrir **Propiedad indizada** pestaña:

   >[!NOTE]
   >
   >Para hybris 5.2, asegúrese de que la variable `Facet` en la tabla Propiedades se selecciona de acuerdo con la siguiente captura de pantalla:

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. Abra el **Configuración de faceta** y ajuste los valores de los campos:

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. **Guarde los cambios.**
1. Otra vez desde **Tipos de artículos de SOLR**, ajuste el `price` faceta de acuerdo con las siguientes capturas de pantalla. Al igual que con `category`, haga doble clic en `price` para abrir **Propiedad indizada** pestaña:

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. Abra el **Configuración de faceta** y ajuste los valores de los campos:

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. **Guarde los cambios.**
1. Abrir **Sistema**, **Búsqueda de facetas**, entonces **Asistente de operaciones del indizador**. Iniciar un cronjob:

   * **Operación de indizador**: `full`
   * **Configuración de Solr**: `Sample Solr Config for Clothes`

## Configurar la versión del catálogo {#configure-the-catalog-version}

El **Versión de catálogo** ( `hybris.catalog.version`) que se importa se puede configurar para el servicio OSGi:

**Configuración de Day CQ Commerce Hybris**
( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**Versión de catálogo** se establece en `Online` o `Staged` (el valor predeterminado).

>[!NOTE]
>
>AEM Al trabajar con los servicios de configuración, existen varios métodos para administrar los parámetros de configuración de dichos servicios; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obtener información detallada. Consulte también la consola para obtener una lista completa de los parámetros configurables y sus valores predeterminados.

El resultado del registro proporciona comentarios sobre las páginas y los componentes creados e informa de posibles errores.

## Configuración de la estructura de importación {#configure-the-import-structure}

La siguiente lista muestra una estructura de muestra (de recursos, páginas y componentes) que se crea de forma predeterminada:

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

El servicio OSGi crea una estructura de este tipo `DefaultImportHandler` que implementa la `ImportHandler` interfaz. El importador real llama a un controlador de importación para crear productos, variaciones de productos, categorías, recursos, etc.

>[!NOTE]
>
>Puede [personalice este proceso implementando su propio controlador de importación](#configure-the-import-structure).

La estructura que se generará al importar se puede configurar para lo siguiente:

&quot;**Controlador de importación predeterminado de Day CQ Commerce Hybris**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

AEM Al trabajar con los servicios de configuración, existen varios métodos para administrar los parámetros de configuración de dichos servicios; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obtener información detallada. Consulte también la consola para obtener una lista completa de los parámetros configurables y sus valores predeterminados.

## Configurar los atributos del producto para cargar {#configure-the-product-attributes-to-load}

El analizador de respuestas se puede configurar para definir las propiedades y los atributos que se van a cargar para los productos (variante):

1. Configure el paquete OSGi:

   **Analizador de respuestas predeterminado de Day CQ Commerce Hybris**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   Aquí puede definir varias opciones y atributos necesarios para la carga y la asignación.

   >[!NOTE]
   >
   >AEM Al trabajar con los servicios de configuración, existen varios métodos para administrar los parámetros de configuración de dichos servicios; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obtener información detallada. Consulte también la consola para obtener una lista completa de los parámetros configurables y sus valores predeterminados.

## Importación de los datos del producto {#importing-the-product-data}

Existen varias formas de importar los datos del producto. Los datos del producto se pueden importar al configurar el entorno por primera vez o después de realizar cambios en los datos de hybris:

* [Importación completa](#full-import)
* [Importación incremental](#incremental-import)
* [Actualización rápida](#express-update)

La información real del producto importado de hybris se almacena en el repositorio en:

`/etc/commerce/products`

Las siguientes propiedades indican el vínculo con hybris:

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>La implementación de hybris (es decir, `geometrixx-outdoors/en_US`) solo almacena los ID de producto y otra información básica en `/etc/commerce`.
>
>Se hace referencia al servidor hybris cada vez que se solicita información sobre un producto.

### Importación completa {#full-import}

1. Si es necesario, elimine todos los datos de producto existentes mediante CRXDE Lite.

   1. Navegue hasta el subárbol que contiene los datos del producto:

      `/etc/commerce/products`

      Por ejemplo:

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. Elimine el nodo que contiene los datos del producto; por ejemplo, `outdoors`.
   1. **Guardar todo** para continuar con el cambio.

1. AEM Abra el importador de hybris en la siguiente ubicación:

   `/etc/importers/hybris.html`

   Por ejemplo:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Configure los parámetros necesarios; por ejemplo:

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. Clic **Importar catálogo** para iniciar la importación.

   Una vez finalizado, puede comprobar los datos importados en:

   ```
       /etc/commerce/products/outdoors
   ```

   Puede abrirlo en CRXDE Lite; por ejemplo:

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### Importación incremental {#incremental-import}

1. AEM Compruebe la información contenida en la documentación de los productos relevantes, en el subárbol correspondiente debajo de:

   `/etc/commerce/products`

   Puede abrirlo en CRXDE Lite; por ejemplo:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. En hybris, actualice la información contenida en los productos relevantes.

1. AEM Abra el importador de hybris en la siguiente ubicación:

   `/etc/importers/hybris.html`

   Por ejemplo:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Seleccione la casilla de verificación **Importación incremental**.
1. Clic **Importar catálogo** para iniciar la importación.

   AEM Una vez finalizado, puede comprobar los datos actualizados en la sección de datos, en la sección de:

   ```
       /etc/commerce/products
   ```


### Actualización rápida {#express-update}

El proceso de importación puede llevar mucho tiempo, por lo que como extensión de la sincronización de productos puede seleccionar áreas específicas del catálogo para una actualización rápida que se activa manualmente. Utiliza la fuente de exportación junto con la configuración de atributos estándar.

1. AEM Compruebe la información contenida en la documentación de los productos relevantes, en el subárbol correspondiente debajo de:

   `/etc/commerce/products`

   Puede abrirlo en CRXDE Lite; por ejemplo:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. En hybris, actualice la información contenida en los productos relevantes.

1. En hybris, agregue uno o más productos a la cola rápida; por ejemplo:

   ![chlimage_1-43](/help/sites-administering/assets/chlimage_1-43a.png)

1. AEM Abra el importador de hybris en la siguiente ubicación:

   `/etc/importers/hybris.html`

   Por ejemplo:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Seleccione la casilla de verificación **Actualización rápida**.
1. Clic **Importar catálogo** para iniciar la importación.

   AEM Una vez finalizado, puede comprobar los datos actualizados en la sección de datos, en la sección de:

   ```
       /etc/commerce/products
   ```

## Configuración del importador de catálogos {#configure-the-catalog-importer}

AEM El catálogo de hybris se puede importar a la lista de productos, utilizando el importador de lotes para catálogos de hybris, categorías y productos.

Los parámetros utilizados por el importador se pueden configurar para:

**Importador de catálogos de Day CQ Commerce Hybris**
( `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

AEM Al trabajar con los servicios de configuración, existen varios métodos para administrar los parámetros de configuración de dichos servicios; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obtener información detallada. Consulte también la consola para obtener una lista completa de los parámetros configurables y sus valores predeterminados.

## Importación de catálogo {#catalog-import}

El paquete hybris viene con un importador de catálogos para configurar la estructura inicial de la página.

Esta opción está disponible en:

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](/help/sites-administering/assets/ecommerceimportconsole.png)

Deberá facilitarse la siguiente información:

* **Almacén base**
El identificador del almacén base configurado en hybris.

* **Catálogo**
El identificador del catálogo que se va a importar.

* **Ruta raíz**
Ruta de acceso en la que se debe importar el catálogo.

## Eliminación de un producto del catálogo {#removing-a-product-from-the-catalog}

Para eliminar uno o más productos del catálogo:

1. [Configure para el servicio OSGi](/help/sites-deploying/configuring-osgi.md) **Importador de catálogos de Day CQ Commerce Hybris**; consulte también [Configuración del importador de catálogos](#configure-the-catalog-importer).

   Active las siguientes propiedades:

   * **Habilitar eliminación del producto**
   * **Habilitar eliminación de recursos del producto**

   >[!NOTE]
   >
   >AEM Al trabajar con los servicios de configuración, existen varios métodos para administrar los parámetros de configuración de dichos servicios; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obtener información detallada. Consulte también la consola para obtener una lista completa de los parámetros configurables y sus valores predeterminados.

1. Inicialice el importador realizando dos actualizaciones incrementales (consulte [Importación de catálogo](#catalog-import)):

   * El resultado de la primera ejecución en un conjunto de productos modificados: se indica en la lista de registros.
   * Por segunda vez, no se debe actualizar ningún producto.

   >[!NOTE]
   >
   >La primera importación es para inicializar la información del producto. La segunda importación comprueba que todo funcionó y que el conjunto de productos está listo.

1. Consulte la página de categoría que contiene el producto que desea eliminar. Los detalles del producto deben estar visibles.

   Por ejemplo, la siguiente categoría muestra detalles del producto Cajamara:

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. Elimine el producto en la consola de hybris. Utilice la opción **Cambiar estado de aprobación** para establecer el estado en `unapproved`. El producto se elimina de la fuente activa.

   Por ejemplo:

   * Abra la página. [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit)
   * Selección del catálogo `Outdoors Staged`
   * Buscar `Cajamara`
   * Seleccione este producto y cambie el estado de aprobación a `unapproved`

1. Realice otra actualización incremental (consulte [Importación de catálogo](#catalog-import)). El registro enumera el producto eliminado.
1. [Despliegue](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) el catálogo adecuado. AEM Se han eliminado el producto y la página del producto de la lista de productos de la red de distribución de productos de.

   Por ejemplo:

   * Abra:

     [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * Desplegar el `Hybris Base` catalogar
   * Abra:

     [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * El `Cajamara` El producto se ha eliminado de `Bike` categoría

1. Para restablecer el producto:

   1. En hybris, vuelva a establecer el estado de aprobación en **aprobado**
   1. AEM En la:

      1. realizar una actualización incremental
      1. despliegue de nuevo el catálogo apropiado
      1. actualice la página de categoría adecuada

## Añadir el rasgo Historial de pedidos al Client Context {#add-order-history-trait-to-the-client-context}

Para agregar el historial de pedidos a [Client Context](/help/sites-developing/client-context.md):

1. Abra el [página de diseño de Client Context](/help/sites-administering/client-context.md), mediante:

   * Abra una página para editarla y, a continuación, abra el contexto de cliente con **Ctrl-Alt-c** (Windows) o **control-option-c** (Mac). Utilice el icono de lápiz de la esquina superior izquierda del contexto del cliente para lo siguiente **Abrir la página de diseño del ClientContext**.
   * Vaya directamente a [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [Añada el **Historial de pedidos** componente](/help/sites-administering/client-context.md#adding-a-property-component) a la **Coche de compras** Componente t del contexto del cliente.
1. Puede confirmar que el contexto del cliente muestra detalles del historial de pedidos. Por ejemplo:

   1. Abra el [Client Context](/help/sites-administering/client-context.md).
   1. Agregar un elemento al carro de compras.
   1. Complete el cierre de compra.
   1. Compruebe el contexto del cliente.
   1. Agregar otro elemento al carro de compras.
   1. Vaya a la página de cierre de compra:

      * El contexto del cliente muestra un resumen del historial de pedidos.
      * Se muestra el mensaje &quot;Es cliente habitual&quot;.

   >[!NOTE]
   >
   >El mensaje se obtiene de la siguiente manera:
   >
   >* Vaya a [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  La campaña consiste en una experiencia.
   >
   >* Haga clic en el segmento ([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))
   >
   >* El segmento se crea con la variable **Propiedad Historial de pedidos** rasgo.
