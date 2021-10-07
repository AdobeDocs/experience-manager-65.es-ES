---
title: 'Conceptos '
description: Conceptos generales de comercio electrónico con AEM.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: 290b2af6-257f-42f2-b809-1248227a4795
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '4524'
ht-degree: 1%

---

# Conceptos {#concepts}

El marco de integración ofrece mecanismos y componentes para:

* conexión a un motor de comercio electrónico
* extracción de datos en AEM
* visualización de esos datos y recopilación de las respuestas del comprador
* devolver detalles de transacciones
* buscar en los datos de ambos sistemas

Esto significa que:

* Los compradores pueden registrarse y comprar sin esperar.
* Los compradores verán los cambios de precios sin demora.
* Los productos se pueden agregar según sea necesario.

>[!NOTE]
>
>El marco de comercio electrónico se puede utilizar con:
>
>* [Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)
>* [SAP Commerce Cloud](/help/commerce/cif-classic/administering/sap-commerce-cloud.md)
>* [Commerce Cloud de Salesforce](https://github.com/adobe/commerce-salesforce)

>


>[!CAUTION]
>
>El [marco de integración de comercio electrónico](https://www.adobe.com/solutions/web-experience-management/commerce.html) es un complemento AEM.
>
>Su representante de ventas podrá dar todos los detalles, según el motor apropiado.

>[!CAUTION]
>
>El marco proporciona los requisitos básicos para su propio proyecto.
>
>Siempre se necesita una cierta cantidad de trabajo de desarrollo para adaptar el marco a sus especificaciones.

>[!CAUTION]
>
>La instalación de AEM estándar incluye la implementación de comercio electrónico de AEM genérica (JCR).
>
>Actualmente está pensado para fines de demostración o como base básica de una implementación personalizada según sus necesidades.

Para optimizar el funcionamiento, tanto AEM como el motor de comercio electrónico se concentran en su propio área de experiencia. La información se transfiere entre ambos en tiempo real; por ejemplo:

* AEM puede:

   * Solicitar:

      * Información del producto del motor de comercio electrónico.
   * Proporcione:

      * Vistas del usuario para obtener información del producto, el carro de compras y el cierre de compra.
      * Carro de compras e información de cierre de compra al motor de comercio electrónico.
      * Optimización del motor de búsqueda (SEO).
      * Funcionalidad de la comunidad.
      * Interacciones de marketing no estructuradas.


* El motor de comercio electrónico puede:

   * Proporcione:

      * Información del producto de la base de datos.
      * Administración de variantes de producto.
      * Gestión de pedidos.
      * ERP (planificación de recursos institucionales).
      * Busque dentro de la información del producto.
   * Proceso:

      * El carro de compras.
      * El cierre de compra.
      * Cumplimiento de pedidos.


>[!NOTE]
>
>Los detalles exactos dependerán del motor de comercio electrónico y de la implementación del proyecto.

Se proporcionan varios componentes de AEM listos para usar para utilizar la capa de integración. Actualmente, estos incluyen:

* Información del producto
* Carro de compras
* Extracción
* Mi cuenta

También hay varias opciones de búsqueda disponibles.

## Arquitectura {#architecture}

El marco de integración proporciona la API, una serie de componentes para ilustrar la funcionalidad y varias extensiones para proporcionar ejemplos de métodos de conexión:

![Chlimage_1-4](/help/sites-administering/assets/chlimage_1-4.png)

El marco le permite acceder a funcionalidades como:

![Chlimage_1-5](/help/sites-administering/assets/chlimage_1-5.png)

### Implementaciones {#implementations}

AEM comercio electrónico se implementa con un motor de comercio electrónico:

* El marco de integración de eCommerce se ha creado para permitirle integrar fácilmente un motor de comercio electrónico con AEM. El motor de comercio electrónico creado con el propósito controla los datos del producto, los carros de compras, el cierre de compra y el cumplimiento de los pedidos, mientras que AEM controla la visualización de los datos y las campañas de marketing.


>[!NOTE]
>
>La instalación de AEM estándar incluye la implementación de comercio electrónico de AEM genérica (JCR).
>
>Actualmente está pensado para fines de demostración o como base básica de una implementación personalizada según sus necesidades.
>
>AEM comercio electrónico implementado dentro de AEM usando desarrollo genérico basado en JCR es:
>
>* Un ejemplo de comercio electrónico independiente y AEM para ilustrar el uso de la API. Esto se puede usar para controlar los datos del producto, los carros de compras y el cierre de compra en conjunto con la visualización de datos y las campañas de marketing existentes. En este caso, la base de datos del producto se almacena en el repositorio nativo de AEM (implementación de [JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html) por parte del Adobe).
>
>  La instalación de AEM estándar contiene los conceptos básicos de la [implementación genérica de comercio electrónico](/help/commerce/cif-classic/administering/generic.md).

### Proveedores de comercio {#commerce-providers}

Al importar datos de un motor de comercio a su sitio de comercio electrónico de AEM, se utiliza un proveedor de comercio para proporcionar datos a los importadores. Un proveedor de comercio puede admitir varios importadores.

Un proveedor de comercio es AEM código personalizado para:

* interfaz con un motor de comercio back-end
* implementar un sistema de comercio sobre el repositorio JCR

Actualmente hay dos proveedores de comercio de ejemplo disponibles para AEM:

* one for geometrixx-hybris
* another for geometrixx-generic (JCR)

Aunque normalmente un proyecto tendrá que desarrollar su propio proveedor de comercio personalizado específico para su PIM y esquema de datos del producto.

>[!NOTE]
>
>Los importadores de geometrixx utilizan archivos CSV; hay una descripción del esquema aceptado (con propiedades personalizadas permitidas) en los comentarios sobre su implementación.

El [ProductServicesManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductServicesManager.html) mantiene (a través de [OSGi](/help/sites-deploying/configuring.md#osgi-configuration-settings)) una lista de implementaciones de las interfaces [ProductImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductImporter.html) y [CatalogBlueprintImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/CatalogBlueprintImporter.html). Se enumeran en el campo desplegable **Importador/Proveedor de comercio** del asistente del importador (con la propiedad `commerceProvider` como nombre).

Cuando un importador o proveedor de comercio específico está disponible en la lista desplegable, cualquier dato suplementario que necesite debe definirse (según el tipo de importador) en:

* `/apps/commerce/gui/content/catalogs/importblueprintswizard/importers`
* `/apps/commerce/gui/content/products/importproductswizard/importers`

La carpeta de la carpeta `importers` adecuada debe coincidir con el nombre del importador; por ejemplo:

* `.../importproductswizard/importers/geometrixx/.content.xml`

El importador define el formato del archivo de importación de origen. O el importador puede establecer una conexión (por ejemplo, WebDAV o http) con el motor de comercio.

## Funciones {#roles}

El sistema integrado se ocupa de las siguientes funciones para mantener los datos:

* Usuario de administración de la información del producto (PIM) que mantiene:

   * Información del producto.
   * taxonomía, categorización, aprobación.
   * Interactúa con la administración de recursos digitales.
   * Precios - a menudo esto viene de un sistema ERP y no se mantiene explícitamente en el sistema comercial.

* Autor/administrador de marketing que mantiene:

   * Contenido de marketing para todos los canales.
   * Promociones.
   * Cupones.
   * Campañas.

* Surfer / Shopper quien:

   * Muestra la información del producto.
   * Coloca artículos en el carro de compras.
   * Comprueba sus pedidos.
   * Se espera el cumplimiento del pedido.

Aunque la ubicación real puede depender de la implementación; por ejemplo, genérico o con un motor de comercio electrónico:

![Chlimage_1-6](/help/sites-administering/assets/chlimage_1-6.png)

## Productos {#products}

### Datos de producto versus datos de marketing {#product-data-versus-marketing-data}

#### Categorías estructurales y de marketing {#structural-versus-marketing-categories}

Si se pueden diferenciar las dos categorías siguientes, esto le permite aclarar las direcciones URL con una estructura significativa (árboles de `cq:Page` nodos) y, por lo tanto, muy cerca de la administración clásica de contenido de AEM):

* *Categorías *estructurales

   El árbol de categorías que define *qué es un producto*; por ejemplo:

   `/products/mens/shoes/sneakers`

* ** Categorías de marketing

   Todas las demás categorías de un *producto pueden pertenecer a*; por ejemplo:

   `/special-offers/christmas/shoes`)

### Datos del producto {#product-data}

Para presentar y administrar su producto, querrá incluir una amplia gama de información sobre ellos.

Los datos del producto pueden ser:

* mantenido directamente en AEM (genérico).
* mantenido en el motor de comercio electrónico y disponible en AEM.

   Según el tipo de datos, se [sincroniza](#catalog-maintenance-data-synchronization) según sea necesario o se accede directamente a él; por ejemplo, los datos críticos y altamente volátiles, como los precios de los productos, se recuperan del motor de comercio electrónico en cada solicitud de página para garantizar que estén siempre actualizados.

En cualquier caso, cuando los datos del producto se han introducido o importado en AEM, se pueden ver desde la consola **Products**. En este caso, las vistas de tarjeta y lista de un producto muestran información como:

* la imagen
* el código SKU
* cuando se haya modificado por última vez

![Chlimage_1-7](/help/sites-administering/assets/chlimage_1-7.png)

### Variantes del producto {#product-variants}

Para los productos adecuados, también se puede obtener información sobre las variantes. Por ejemplo, para los artículos de ropa, los diferentes colores disponibles se mantienen como variantes:

![ecommerceproductvariants](/help/sites-administering/assets/ecommerceproductvariants.png)

### Atributos del producto {#product-attributes}

Los atributos individuales que se mantienen sobre cada producto pueden depender del motor de comercio electrónico que se utilice y de la implementación de AEM. Están disponibles (según corresponda) al ver páginas de productos o al editar información del producto y pueden incluir:

* **Imagen**

   Una imagen del producto.

* **Título**

   El nombre del producto.

* **Descripción**

   Descripción textual del producto.

* **Etiquetas**

   Tags used to group related products.

* **Categoría de recursos predeterminada**

   Una categoría predeterminada para los recursos.

* **Datos de ERP**

   Información sobre planificación de los recursos institucionales.

   * **SKU**

      Información de la unidad de almacenamiento (SKU).

   * **Color**
   * **Tamaño**
   * **Precio**

      El precio unitario del producto.

* **Resumen**

   Resumen de las funciones del producto.

* **Características**

   Más información sobre las características del producto.

### Recursos de producto {#product-assets}

Se puede mantener una selección de recursos para productos individuales. Normalmente incluyen imágenes y vídeos.

## Catálogos {#catalogs}

Un catálogo agrupa los datos del producto para facilitar la administración y la representación al comprador. A menudo, un catálogo está estructurado según atributos como idioma, área geográfica, marca, temporada, pasatiempo, deporte, entre muchos otros.

### Estructura del catálogo {#catalog-structure}

#### Catálogos en varios idiomas {#catalogs-in-multiple-languages}

AEM admite contenido de productos en varios idiomas. Al solicitar datos, el marco de integración recupera el idioma del árbol actual (por ejemplo, `en_US` para las páginas en `/content/geometrixx-outdoors/en_US`).

Para una tienda multilingüe, puede importar el catálogo para cada árbol de idiomas individualmente (o copiarlo mediante [MSM](/help/sites-administering/msm.md)).

#### Catálogos para marcas múltiples {#catalogs-for-multiple-brands}

Al igual que con los idiomas, las grandes empresas multinacionales pueden necesitar atender a múltiples marcas.

#### Catálogos por etiquetas {#catalogs-by-tags}

Las etiquetas también se pueden usar para agrupar productos en un catálogo. Pueden utilizarse para catálogos más dinámicos, como ofertas de temporada.

### Configuración del catálogo (importación inicial) {#catalog-setup-initial-import}

Según la implementación, puede importar los datos de producto necesarios para el catálogo base en AEM desde:

* un archivo CSV (para la implementación genérica)
* el motor de comercio electrónico

### Mantenimiento del catálogo (Sincronización de datos) {#catalog-maintenance-data-synchronization}

Será inevitable realizar más cambios en los datos del producto:

* para la implementación genérica , se pueden administrar con el [editor de productos](/help/commerce/cif-classic/administering/generic.md#editing-product-information)
* cuando se utiliza un motor de [eCommerce , los cambios deben sincronizarse](#data-synchronization-with-an-ecommerce-engine-ongoing)

#### Sincronización de datos con un motor de comercio electrónico (en curso) {#data-synchronization-with-an-ecommerce-engine-ongoing}

Después de la importación inicial, los cambios en los datos del producto son inevitables.

Al utilizar un motor de comercio electrónico, los datos del producto se mantienen allí y deben estar disponibles en AEM. Los datos de este producto deben sincronizarse cuando se realicen actualizaciones.

Esto puede depender del tipo de datos:

* Se utiliza una [sincronización periódica junto con una fuente de datos de cambios](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#product-synchronization-and-publishing).

   Además de esto, puede seleccionar actualizaciones específicas para una actualización rápida.

* Los datos muy volátiles, como la información de precios, se recuperan del motor de comercio para cada solicitud de página para garantizar que siempre estén actualizados.

### Catálogos: rendimiento y escala {#catalogs-performance-and-scaling}

La importación de un catálogo grande con un número elevado de productos (normalmente más de 100.000) desde un motor de comercio electrónico (PIM) puede afectar al sistema debido al gran número de nodos. También puede ralentizar la instancia de creación si los productos tienen recursos asociados (p. ej., imágenes de producto). Esto se debe al hecho de que el posprocesamiento de estos recursos requiere gran cantidad de CPU y memoria.

Existen varias estrategias que puede elegir para solucionar estos problemas:

* [Agrupación](#bucketing) : para satisfacer el gran número de nodos
* [Descargar el posprocesamiento de recursos en una instancia dedicada](#offload-asset-post-processing-to-a-dedicated-instance)
* [Importar solo datos de productos](#only-import-product-data)
* [Importar restricciones y guardar lotes](#import-throttling-and-batch-saves)
* [Pruebas de rendimiento](#performance-testing)
* [Rendimiento - Varios](#performance-miscellaneous)

#### Agrupamiento {#bucketing}

Si un nodo JCR tiene muchos nodos secundarios directos (por ejemplo, 1000 o más), se necesitan bloques (carpetas fantasma) para garantizar que el rendimiento no se vea afectado. Se generan según un algoritmo al importar.

Estos bloques toman la forma de carpetas fantasma que se introducen en la estructura del catálogo, pero que pueden configurarse para que no aparezcan en las direcciones URL públicas.

#### Descargar el posprocesamiento de recursos en una instancia dedicada {#offload-asset-post-processing-to-a-dedicated-instance}

Este escenario implica la configuración de dos instancias de autor:

1. Instancia del autor maestro

   Importa datos de producto de PIM, en los que se desactiva el posprocesamiento de las rutas de recursos.

1. Instancia de autor de DAM dedicada

   Importa y posprocesa recursos de producto desde el PIM y, a continuación, los replica en la instancia de autor maestra para su uso.

![Diagrama de arquitectura](/help/sites-administering/assets/chlimage_1-8.png)

#### Importar solo datos de productos {#only-import-product-data}

For cases when products do not contain assets (images) to be imported, you can import the product data without being affected by asset post-processing.

![Diagrama de arquitectura](/help/sites-administering/assets/chlimage_1-9.png)

#### Pruebas de rendimiento {#performance-testing}

Performance testing must be taken into consideration on AEM eCommerce implementations:

* Author environment:

   La actividad en segundo plano (por ejemplo, importar) puede producirse al mismo tiempo que la actividad normal del usuario (por ejemplo, la edición de páginas) e incluso si el rendimiento del front-end tiene (en general) una prioridad mayor, el mal rendimiento que ven los autores en línea puede provocar frustraciones que puedan bloquear una decisión de activación.

* Entorno de publicación:

   La replicación es un proceso crítico para garantizar que el contenido se publique de forma rápida y fiable. Esto puede verse afectado por el modo en que el autor agrupa el contenido que se va a publicar.

* Front-end:

   La mezcla de invalidaciones de front-end y de caché puede potencialmente causar sorpresas en el rendimiento. Las pruebas ayudan a evitarlas.

Tenga en cuenta que esta prueba de rendimiento requiere conocimientos y análisis del objetivo:

* Volúmenes de contenido

   * Assets
   * Productos y SKU localizados con i18ned

* Actividad del usuario:

   * Edición masiva
   * Publicación masiva
   * Solicitudes de búsqueda intensivas

* Procesos en segundo plano

   * Importaciones
   * Actualizaciones de sincronización (p. ej., precios)

* Requisitos de mantenimiento (copia de seguridad, optimización de Tar PM, colección de residuos del almacén de datos, etc.)

#### Rendimiento - Varios {#performance-miscellaneous}

Para todas las implementaciones se pueden tener en cuenta los siguientes puntos:

* Como el producto, las unidades de almacenamiento y las categorías pueden ser numerosas, intente utilizar el menor número posible de nodos para modelar el contenido.

   Cuantos más nodos tenga, más flexible será su contenido (por ejemplo, parsys). Sin embargo, todo es una compensación y ¿necesita flexibilidad individual (de forma predeterminada) al manipular (por ejemplo) productos de 30K?

* Evite la duplicación tanto como pueda (consulte localización) o, cuando lo haga, piense en cuántos nodos conducirá la duplicación.
* Intente etiquetar el contenido tanto como pueda para preparar la optimización de la consulta.

   Por ejemplo:

   `/content/products/france/fr/shoe/reebok/pump/46 SKU`

   debe tener una etiqueta por nivel de contenido (es decir, país, idioma, categoría, marca, producto). Buscando

   `//element(*,my:Sku)[@country=’france’ and @language=’fr’`

   y

   `@category=’shoe’ and @brand=’reebok’ and @product=’pump’]`

   será mucho más rápido que buscar

   `/jcr:root/content/france/fr/shoe/reebok/pump/element(*,my:Sku)`

* En su pila técnica, planifique un modelo y servicios de acceso a contenido muy factorizado. Esta es una práctica recomendada general, pero es aún más crucial para ella, ya que puede, en las fases de optimización, añadir cachés de aplicación para datos que se leen muy a menudo (y que no desea rellenar la caché del paquete con).

   Por ejemplo, la administración de atributos suele ser un buen candidato para el almacenamiento en caché, ya que afecta a los datos que se actualizan a través de la importación de productos.
* Considere el uso de [páginas proxy](#proxy-pages).

### Páginas de sección del catálogo {#catalog-section-pages}

Las secciones del catálogo le proporcionan, por ejemplo:

* una introducción (imagen o texto) a la categoría; esto también se puede utilizar para letreros y teasers para promocionar ofertas especiales
* vínculos a productos individuales de esa categoría
* vínculos a las otras categorías

![ecommerce_categoryrunning](/help/sites-administering/assets/ecommerce_categoryrunning.png)

### Páginas de producto {#product-pages}

Las páginas de productos proporcionan información completa sobre productos individuales. También se reflejan las actualizaciones dinámicas de . por ejemplo, los cambios de precios registrados en el motor de comercio electrónico.

Las páginas de producto son páginas AEM que utilizan el componente **Product**; por ejemplo, dentro de la plantilla **Commerce Product**:

![ecommerce_nairobirunnersgreen](/help/sites-administering/assets/ecommerce_nairobirunnersgreen.png)

El componente Producto proporciona:

* Información general del producto; incluyendo texto e imágenes.
* Precios; esto generalmente se recupera del motor de comercio electrónico cada vez que se muestra/actualiza la página.
* Información sobre la variante del producto; por ejemplo, color y tamaño.

Esta información permite al comprador seleccionar lo siguiente al añadir un elemento a su cesta:

* Variables de color y tamaño
* Cantidad

#### Páginas de aterrizaje del producto {#product-landing-pages}

Son páginas AEM que proporcionan información principalmente estática; por ejemplo, una introducción y una descripción general con vínculos a las páginas de producto subyacentes.

### Componente del producto {#product-component}

El componente **Product** se puede añadir a cualquier página con una página principal que envíe los metadatos necesarios (es decir, las rutas a `cartPage` y `cartObject`). En el sitio de demostración, Geometrixx Outdoors, esto lo suministra `UserInfo.jsp`.

The **Product** component can also be customized according to your individual requirements.

### Proxy Pages {#proxy-pages}

Las páginas proxy se utilizan para simplificar la estructura del repositorio y optimizar el almacenamiento para catálogos grandes.

Creating a catalog will use ten nodes per product as it provides individual components for each product that you can update and customise within AEM. Este gran número de nodos puede convertirse en un problema si el catálogo contiene cientos o incluso miles de productos. Para evitar cualquier problema, puede crear su catálogo utilizando páginas proxy.

Proxy pages use a two-node structure ( `cq:Page` and `jcr:content`) that does not contain any of the actual product content. El contenido se genera, en el momento de la solicitud, haciendo referencia a los datos del producto y a la página de plantilla.

Sin embargo, hay una compensación. No podrá personalizar la información del producto dentro de AEM, se utilizará una plantilla estándar (definida para el sitio).

>[!NOTE]
>
>No tendrá ningún problema si importa un catálogo grande sin páginas proxy.
>
>Puede convertir de una metodología a otra en cualquier momento. También puede convertir una subsección del catálogo.

## Promociones y cupones {#promotions-and-vouchers}

### Cupones {#vouchers}

Los cupones son un método probado y probado de ofrecer descuentos para atraer compradores a realizar una compra o premiar la lealtad del cliente.

* Suministro de cupones:

   * Código de cupón (que el comprador escribirá en el carro de compras).
   * Una etiqueta de cupón (que se mostrará después de que el comprador la haya introducido en el carro de compras).
   * Una ruta de promoción (que define la acción que aplica el cupón).

* Los motores de comercio exterior también pueden proporcionar vales.

En AEM:

* Un vale es un componente basado en páginas que se crea o edita con la consola Sitios web .
* El componente **Cupón** proporciona:

   * Un procesador para la administración de vales; esto muestra cualquier comprobante que se encuentre en el carro de compras.
   * Los cuadros de diálogo de edición (formulario) para administrar (añadir/quitar) los comprobantes.
   * Las acciones necesarias para agregar/quitar cupones al carro de compras o desde él.

* Los cupones no tienen su propio valor en la fecha/hora y fuera de ella, pero utilizan los de sus campañas principales.

>[!NOTE]
>
>AEM utiliza el término **Cupón**, es sinónimo del término **Cupón**.

### Promociones {#promotions}

Las promociones, junto con los vales, permiten realizar escenarios como:

* Una empresa proporciona precios personalizados para empleados, que es una lista de usuarios diseñada a mano.
* Los clientes a largo plazo reciben descuentos en todos los pedidos.
* Precio de venta ofrecido durante un período de tiempo bien definido.
* Un cliente recibe un asiento cuando su pedido anterior excede una cantidad específica.
* A los clientes que compran *product-X* se les ofrece un descuento en *product-Y* (productos de pareja).

Normalmente, los administradores de información de productos no se encargan de mantener las promociones, pero sí de los administradores de marketing:

* Una promoción es un componente basado en páginas que se crea o edita con la consola Sitios web . &quot;
* Oferta de promociones:

   * Una prioridad
   * Una ruta del controlador de promoción

* Puede conectar promociones a una campaña para definir la fecha y las horas de activación y desactivación.
* Puede conectar promociones a una experiencia para definir sus segmentos.
* Las promociones que no estén conectadas a una experiencia no se activarán por sí solas, pero aún pueden ser activadas por un Cupón.
* El componente Promoción contiene:

   * renderizadores y diálogos para la administración de promociones
   * subcomponentes para procesar y editar parámetros de configuración específicos de los controladores de promoción

En AEM, las promociones también están integradas en la [Administración de campañas](/help/sites-authoring/personalization.md):

* una [campaña](/help/sites-authoring/personalization.md) especifica los tiempos de activación/desactivación
* [](/help/sites-authoring/personalization.md) ** las experiencias de la campaña se utilizan para agrupar recursos (teaserpages, promociones, etc.) según el segmento de audiencia al que corresponden

Una promoción puede realizarse en una experiencia o directamente en la campaña:

* Si una promoción se realiza en una experiencia, se puede aplicar automáticamente a un segmento de audiencia.

   Por ejemplo, en el sitio de muestra de geometrixx-outdoors, la promoción:

   `/content/campaigns/geometrixx-outdoors/big-spender/ordervalueover100/free-shipping`

   está en una experiencia, por lo que se activa automáticamente cada vez que se resuelve el segmento ( `ordervalueover100`).

* Si una promoción no aparece dentro de una experiencia (solo en la campaña), no se puede aplicar automáticamente a una audiencia. Sin embargo, se puede activar si el comprador introduce un vale en el carro y ese vale hace referencia a la promoción.

   Por ejemplo, la promoción:

   `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

   está fuera de una experiencia y, por lo tanto, nunca se activa automáticamente (es decir: en función de la segmentación). Sin embargo, los vales hacen referencia a él, que se puede encontrar en varias de las experiencias de la campaña de artículos. Si se introducen esos códigos de cupón en el carro de compras, la promoción se activará.

>[!NOTE]
>
>[híbris ](https://www.hybris.com/modules/promotion) promotions and  [hybris ](https://www.hybris.com/en/modules/voucher) voucherscover cubren todo lo que influye en el carro de compras y está relacionado con los precios. El contenido de marketing específico de promoción (como banners, etc.) no forma parte de la promoción de híbridos.

## Personalización {#personalization}

### Registro de clientes y cuentas {#customer-registration-and-accounts}

Cuando se registra un comprador, los detalles de la cuenta deben sincronizarse entre AEM y el motor de comercio electrónico. Sensitive data is held independently, but profiles are shared:

![imagen_1-10](/help/sites-administering/assets/chlimage_1-10.png)

El mecanismo exacto puede depender del escenario:

1. Las cuentas de usuario existen en ambos sistemas:

   1. No se requiere ninguna acción.

1. La cuenta de usuario solo existe en AEM:

   1. El usuario se creará en el motor de comercio electrónico con el mismo ID de cuenta y una contraseña aleatoria que se almacenarán en AEM.
   1. La contraseña aleatoria es necesaria, ya que AEM intenta iniciar sesión en el motor de comercio electrónico en la primera llamada (por ejemplo, cuando se solicita una página de producto y se hace referencia al motor de comercio electrónico para el precio). Como esto sucede después del inicio de sesión AEM, la contraseña no está disponible.

1. The user account only exists in the eCommerce engine:

   1. La cuenta se creará en AEM con el mismo ID de cuenta y contraseña.

Al utilizar un motor de comercio electrónico, AEM solo almacena el ID de cuenta y la contraseña (opcionalmente, un grupo de usuarios). El resto de la información se almacena en el motor de comercio electrónico.

>[!NOTE]
>
>Al utilizar un motor de comercio electrónico, debe asegurarse de que las cuentas creadas para los usuarios que inician sesión en una instancia de AEM se dupliquen (por ejemplo, mediante flujos de trabajo) en cualquier otra instancia de AEM que se comunique con ese motor.
>
>De lo contrario, estas otras instancias de AEM también intentarán crear cuentas para los mismos usuarios en el motor. Estas acciones fallarán con un `DuplicateUidException` proveniente del motor.

### Registro de clientes {#customer-sign-up}

A menudo, es necesario registrarse para que el comprador tenga acceso al carro de compras. Esto requiere registrarse (Crear cuenta) para poder crear una cuenta específica del cliente.

![imagen_1-11](/help/sites-administering/assets/chlimage_1-11.png)

>[!NOTE]
>
>También se admite un carro de compras y un cierre de compra anónimos.

### Inicio de sesión de cliente {#customer-sign-in}

Después de registrarse, el comprador puede iniciar sesión con su cuenta para que se pueda realizar un seguimiento de sus acciones y cumplir sus pedidos.

![imagen_1-12](/help/sites-administering/assets/chlimage_1-12.png)

### Inicio de sesión único {#single-sign-on}

Se proporciona el inicio de sesión único (SSO), de modo que los autores sean conocidos tanto en AEM como en el sistema de comercio electrónico sin tener que iniciar sesión dos veces.

### myAccount {#myaccount}

Los datos de transacción del motor de comercio electrónico se combinan con información personal sobre el comprador. AEM utiliza algunos de estos datos como datos de perfil. La acción de un formulario en AEM escribe información de nuevo en el motor de comercio electrónico.

Hay una página que le permite administrar fácilmente la información de su cuenta. Puede acceder a él haciendo clic en **My Account** en la parte superior de una página de geometrixx o navegando a `/content/geometrixx-outdoors/en/user/account.html`.

![imagen_1-13](/help/sites-administering/assets/chlimage_1-13.png)

### Libreta de direcciones {#address-book}

El sitio deberá almacenar una selección de direcciones; incluida la entrega, la facturación y las direcciones alternativas. Esto se puede implementar utilizando formularios basados en el formato de dirección predeterminado o puede utilizar el componente Libreta de direcciones proporcionado por AEM.

Este componente de Libreta de direcciones le permite:

* editar direcciones en el libro
* seleccionar una dirección de la libreta para la dirección de envío
* seleccionar una dirección de la libreta para la dirección de facturación

Puede elegir la dirección que desee de forma predeterminada.

Se puede acceder al componente Libreta de direcciones desde la página **Mi cuenta** haciendo clic en **Libreta de direcciones** o navegando a `/content/geometrixx-outdoors/en/user/account/address-book.html`.

![imagen_1-14](/help/sites-administering/assets/chlimage_1-14.png)

Puede hacer clic en **Add new address...** para agregar una nueva dirección en la libreta de direcciones. Se abre un formulario que se puede rellenar y, a continuación, se hace clic en **Agregar dirección**.

>[!NOTE]
>
>Puede introducir varias direcciones en la Libreta de direcciones.

La Libreta de direcciones se utiliza cuando se cierra la compra:

![imagen_1-15](/help/sites-administering/assets/chlimage_1-15.png)

Las direcciones se mantienen debajo de `user_home/profile/addresses`.
Por ejemplo, para Alison Parker, estaría en /home/users/geometrixx/aparker@geometrixx.info/profile/addresses

Puede elegir la dirección que desea de forma predeterminada; esta información se mantiene en el perfil del comprador en lugar de en la dirección. La propiedad de perfil `address.default` se establece con la ruta de la dirección seleccionada para el valor.

### Precios específicos del cliente {#customer-specific-pricing}

El motor de comercio electrónico utiliza el contexto (básicamente la información del comprador) para determinar el precio que tiene y, a continuación, AEM la información correcta.

## Carro de compras y pedidos {#shopping-cart-and-orders}

Cuando realice la compra, el comprador examinará las páginas del producto y seleccionará los artículos para colocarlos en su carro de compras. Cuando proceden al cierre de compra, se puede realizar un pedido.

### Compradores anónimos {#anonymous-shoppers}

Un cliente anónimo puede:

* Ver productos
* Agregar productos al carro de compras
* Realizar cierre de compra para realizar el pedido

>[!NOTE]
>
>Dependiendo de la configuración de la información de dirección de su instancia, o del registro de clientes, podría ser necesario antes del cierre de compra.

### Compradores registrados {#registered-shoppers}

Un cliente registrado puede:

* Inicie sesión en su cuenta
* View products
* Agregar productos al carro de compras
* Realizar cierre de compra para realizar el pedido
* View and track previous orders

### Shopping Cart Content Overview {#shopping-cart-content-overview}

The shopping cart provides:

* una descripción general de los elementos seleccionados
* links to the product pages for the selected items
* la capacidad para:

   * actualizar el número/cantidad de los artículos individuales
   * quitar elementos individuales

![ecommerce_shoppingcart](/help/sites-administering/assets/ecommerce_shoppingcart.png)

El carro de compras se guarda de acuerdo con el motor utilizado:

* AEM genérico almacena el carro de compras en una cookie.
* Ciertos motores de comercio electrónico pueden almacenar el carro de compras en una sesión.

En cualquier caso, los artículos permanecen en el carro (y se pueden restaurar) durante el inicio de sesión o cierre de sesión (pero solo en el mismo equipo o explorador). Por ejemplo:

* busque `anonymous` y añada productos al carro de compras
* iniciar sesión como `Allison Parker` - su carro está vacío
* agregar productos a su carro de compras
* cierre de sesión: el carro mostrará los productos para `anonymous`

* vuelva a iniciar sesión como `Allison Parker`: sus productos se restauran

>[!NOTE]
>
>Un carro de compras anónimo solo se puede restaurar en el mismo equipo o explorador.

>[!NOTE]
>
>No se recomienda probar la restauración del contenido del carro de compras con la cuenta `admin` , ya que esto puede entrar en conflicto con la cuenta `admin` del motor de comercio electrónico (p. ej., hybris).

>[!NOTE]
>
>se puede configurar hybris para eliminar los carros de compras pendientes después de un período de tiempo definido.

Antes del cierre de compra, se reflejan los cambios de precio (en ambos sistemas) a medida que se producen.

### Información del pedido {#order-information}

En función de la información de implementación sobre un pedido se mantenga en el motor de comercio electrónico o en el AEM, esta información se procesa mediante AEM.

Se almacena una variedad de información, que puede incluir:

* **ID de pedido**

   El número de referencia del pedido.

* **Realizado**

   La fecha en la que se realizó el pedido.

* **Estado**

   El estado de la orden; por ejemplo, Enviado.

* **Moneda**

   La moneda del pedido.

* **Elementos de contenido**

   Lista de elementos ordenados.

* **Subtotal**

   El coste total de los artículos pedidos.

* **Impuestos**

   El importe de los impuestos adeudados en el pedido.

* **Envío**

   Gastos de envío.

* **Total**

   El valor total del pedido; artículos pedidos, impuestos y compras.

* **Dirección de facturación**

   La dirección a la que se debe enviar la factura.

* **Testigo de pago**

   El método de pago.

* **Estado de pago**

   El estado del pago.

* **Dirección de envío**

   Dirección a la que deben enviarse las mercancías.

* **Método de envío**

   El método de envío; por ejemplo, tierra, mar o aire.

* **Número de seguimiento**

   Cualquier número de seguimiento utilizado por la compañía de envío.

* **Vínculo de seguimiento**

   Vínculo utilizado para realizar el seguimiento del pedido mientras se envía.

>[!NOTE]
>
>Los campos utilizados en el asistente para crear orden dependen de que haya un andamiaje táctil definido para la ubicación. En el ejemplo genérico, se puede encontrar en:
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`

Cuando el pedido se mantiene en AEM consola Pedidos muestra lo siguiente para cada pedido:

* el número de elementos del carro de compras
* el valor total del pedido
* cuando se realizó el pedido
* el estado

![imagen_1-16](/help/sites-administering/assets/chlimage_1-16.png)

### Seguimiento de pedidos {#order-tracking}

Después de realizar un pedido, los compradores suelen regresar a:

* Comprobar el estado de su pedido
* Eliminar productos del pedido
* Añadir productos al pedido

Después de recibir la entrega del pedido, es posible que los compradores también deseen ver el historial de pedidos realizados durante un período de tiempo.

El cumplimiento y seguimiento de los pedidos suele ser administrado por el motor de comercio electrónico. La información se puede mostrar AEM el componente Historial de pedidos , que muestra todos los detalles relevantes, incluidos los comprobantes y las promociones aplicadas. Por ejemplo:

![chlimage_1-17](/help/sites-administering/assets/chlimage_1-17.png)

## Cierre de compra {#checkout}

El cierre de compra se implementa con formularios AEM estándar. Esto permite al administrador de marketing personalizar la experiencia con contenido de marketing.

A continuación, eCommerce administra el proceso de cierre de compra con los datos introducidos desde los formularios AEM.

### Seguridad de pago {#payment-security}

Los detalles de pago, incluida la información de la tarjeta de crédito, suelen ser administrados por el motor de comercio electrónico. AEM reenvía dicha información transaccional al motor (desde donde se reenvía a un servicio de procesamiento de pagos).

Se puede lograr el cumplimiento de la normativa de la industria de tarjetas de pago (PCI).

### Confirmación del pedido {#confirmation-of-order}

El pedido se confirma en pantalla y se puede rastrear con el [seguimiento de pedidos](#order-tracking).

## Búsqueda {#search-features}

![chlimage_1-18](/help/sites-administering/assets/chlimage_1-18.png)

Dado que AEM utiliza páginas estándar para los productos, puede utilizar el componente de búsqueda estándar para crear una página de búsqueda.

Si necesita una implementación más detallada, puede:

* Amplíe el componente de búsqueda predeterminado con la funcionalidad que necesite.
* Implemente el método de búsqueda en `CommerceService` y, a continuación, utilice el componente de búsqueda de comercio electrónico en la página de búsqueda.

Al utilizar un motor de comercio electrónico, la API de búsqueda de comercio electrónico se puede implementar completamente en la solución del motor de comercio electrónico, de modo que puede utilizar el componente de búsqueda de comercio electrónico que se proporciona de forma predeterminada. La búsqueda por facetas le permite buscar en JCR o en el motor:
