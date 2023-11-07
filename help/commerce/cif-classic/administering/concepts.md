---
title: Conceptos
description: Conozca los conceptos generales de comercio electrónico con Adobe Experience Manager.
contentOwner: Guillaume Carlino
exl-id: 290b2af6-257f-42f2-b809-1248227a4795
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '4481'
ht-degree: 1%

---

# Conceptos {#concepts}

El marco de integración proporciona los mecanismos y componentes para:

* conexión a un motor de comercio electrónico
* extracción de datos en Adobe Experience Manager AEM ()
* mostrar esos datos y recopilar las respuestas del comprador
* devolución de detalles de transacción
* buscar en los datos de ambos sistemas

Esto significa lo siguiente:

* Los compradores pueden registrarse y comprar sin esperar.
* Los compradores ven sin demora los cambios de precios.
* Los productos se pueden añadir según sea necesario.

>[!NOTE]
>
>El marco de comercio electrónico se puede utilizar con:
>
>* [Adobe Commerce](/help/commerce/cif/integrating/magento.md)
>* [COMMERCE CLOUD SAP](/help/commerce/cif-classic/administering/sap-commerce-cloud.md)
>* [Commerce Cloud de Salesforce](https://github.com/adobe/commerce-salesforce)
>

>[!CAUTION]
>
>El [Marco de integración de eCommerce](https://business.adobe.com/products/experience-manager/sites/ecommerce-integrations.html) AEM es un complemento de.
>
>Su representante de ventas puede proporcionar todos los detalles, según el motor adecuado.

>[!CAUTION]
>
>El marco de trabajo proporciona los requisitos básicos para su propio proyecto.
>
>Siempre se necesita una cierta cantidad de trabajo de desarrollo para adaptar el marco a sus especificaciones.

>[!CAUTION]
>
>AEM AEM La instalación estándar de la incluye la implementación genérica de comercio electrónico de (JCR).
>
>Se ha diseñado con fines de demostración o como base básica para una implementación personalizada según sus necesidades.

AEM Para optimizar la operación, tanto el motor de comercio electrónico como el de los recursos, se concentran en su propia área de experiencia. La información se transfiere entre ambos en tiempo real; por ejemplo:

* AEM Puede:

   * Solicitar:

      * Información del producto del motor de comercio electrónico.

   * Proporcionar:

      * Vistas del usuario para obtener información del producto, el carro de compras y el cierre de compra.
      * Información del carro de compras y del cierre de compra al motor de comercio electrónico.
      * Optimización del motor de búsqueda (SEO).
      * Funcionalidad de la comunidad.
      * Interacciones de marketing no estructuradas.

* El motor de comercio electrónico puede:

   * Proporcionar:

      * Información del producto de la base de datos.
      * Administración de variantes de producto.
      * Order Management.
      * ERP (planificación de recursos empresariales).
      * Buscar en la información del producto.

   * Proceso:

      * El carro de compras.
      * El pago.
      * Cumplimiento del pedido.

>[!NOTE]
>
>Los detalles exactos dependen del motor de comercio electrónico y de la implementación del proyecto.

AEM Se proporcionan varios componentes listos para usar para usar de la capa de integración de. Actualmente, estos incluyen:

* Información del producto
* Carro de compras
* Fecha de salida
* Mi cuenta

También hay varias opciones de búsqueda disponibles.

## Arquitectura {#architecture}

El marco de integración proporciona la API, una serie de componentes para ilustrar la funcionalidad y varias extensiones para proporcionar ejemplos de métodos de conexión:

![chlimage_1-4](/help/sites-administering/assets/chlimage_1-4.png)

El marco de trabajo le permite acceder a funciones como las siguientes:

![chlimage_1-5](/help/sites-administering/assets/chlimage_1-5.png)

### Implementaciones {#implementations}

AEM eCommerce se implementa con un motor de comercio electrónico:

* AEM El marco de trabajo de integración de comercio electrónico se ha creado para permitirle integrar fácilmente un motor de comercio electrónico con las soluciones de comercio electrónico de forma más sencilla y con más de un. AEM El motor de comercio electrónico creado específicamente controla los datos de los productos, los carros de compras, el cierre de compra y el cumplimiento de los pedidos, mientras que el control de la visualización de datos y las campañas de marketing se realiza de forma independiente.


>[!NOTE]
>
>AEM AEM La instalación estándar de la incluye la implementación genérica de comercio electrónico de (JCR).
>
>Se ha diseñado con fines de demostración o como base básica para una implementación personalizada según sus necesidades.
>
>AEM AEM eCommerce implementado en el entorno de desarrollo genérico basado en JCR es:
>
>* AEM Un ejemplo de comercio electrónico independiente y nativo de la comunidad de usuarios de para ilustrar el uso de la API de. Esto se puede utilizar para controlar los datos del producto, los carros de compras y el cierre de compra con la visualización de datos y las campañas de marketing existentes. AEM En este caso, la base de datos de productos se almacena en el repositorio nativo de la implementación de (implementación de Adobe de ), que es el que se utiliza para la creación de informes de producto de [JCR](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html)).
>
>  AEM La instalación estándar de la aplicación contiene los conceptos básicos de la [implementación genérica de eCommerce](/help/commerce/cif-classic/administering/generic.md).

### Proveedores de comercio {#commerce-providers}

AEM Al importar datos desde un motor de comercio al sitio de comercio electrónico de la aplicación, se utiliza un proveedor de comercio para proporcionar datos a los importadores. Un proveedor comercial puede admitir varios importadores.

AEM Un proveedor de comercio es un código de personalizado para lo siguiente:

* interfaz con un motor de comercio back-end
* implementar un sistema de comercio sobre el repositorio JCR.

AEM Actualmente hay disponibles dos proveedores comerciales de ejemplo para la creación de segmentos de mercado:

* uno para geometrixx-hybris
* otro para geometrixx-generic (JCR)

Aunque normalmente un proyecto necesita desarrollar su propio proveedor de comercio personalizado y específico para su PIM y esquema de datos del producto.

>[!NOTE]
>
>Los importadores de Geometrixx utilizan archivos CSV; hay una descripción del esquema aceptado (con propiedades personalizadas permitidas) en los comentarios anteriores a su implementación.

El [ProductServicesManager](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/ProductServicesManager.html) mantiene (mediante [OSGi](/help/sites-deploying/configuring.md#osgi-configuration-settings)) una lista de implementaciones de [ProductImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/ProductImporter.html) y [CatalogBlueprintImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/CatalogBlueprintImporter.html) interfaces. Se enumeran en la **Importador/Proveedor comercial** campo desplegable del asistente del importador (con el `commerceProvider` propiedad como nombre).

Cuando un importador/proveedor comercial específico está disponible en la lista desplegable, los datos suplementarios que necesite se deben definir (según el tipo de importador) en:

* `/apps/commerce/gui/content/catalogs/importblueprintswizard/importers`
* `/apps/commerce/gui/content/products/importproductswizard/importers`

La carpeta bajo el `importers` La carpeta debe coincidir con el nombre del importador. Por ejemplo:

* `.../importproductswizard/importers/geometrixx/.content.xml`

El importador define el formato del archivo de importación de origen. O el importador puede establecer una conexión (por ejemplo, WebDAV o http) con el motor de comercio.

## Funciones {#roles}

El sistema integrado se encarga de las siguientes funciones para mantener los datos:

* Usuario de gestión de información del producto (PIM) que mantiene:

   * Información del producto.
   * Taxonomía, categorización, aprobación.
   * Interactúa con la administración de recursos digitales.
   * Precios: a menudo proviene de un sistema ERP y no se mantiene explícitamente en el sistema comercial.

* Autor/responsable de marketing que mantiene lo siguiente:

   * Contenido de marketing para todos los canales.
   * Promociones.
   * Cupones.
   * Campañas.

* Internauta/comprador que:

   * Consulta la información del producto.
   * Coloca artículos en el carro de compras.
   * Comprueba sus pedidos.
   * Se espera el cumplimiento del pedido.

Aunque la ubicación real puede depender de la implementación; por ejemplo, genérica o con un motor de comercio electrónico:

![chlimage_1-6](/help/sites-administering/assets/chlimage_1-6.png)

## Productos {#products}

### Datos de productos frente a datos de marketing {#product-data-versus-marketing-data}

#### Categorías estructurales frente a categorías de marketing {#structural-versus-marketing-categories}

Si se pueden diferenciar las dos categorías siguientes, esto permite establecer direcciones URL claras con una estructura significativa (árboles de `cq:Page` AEM nodos) y, por lo tanto, muy cerca de la gestión de contenido clásica de la):

* *Estructurales *categorías

  El árbol de categorías que define *¿qué es un producto?*; por ejemplo:

  `/products/mens/shoes/sneakers`

* *Marketing* categorías

  Todas las demás categorías que *el producto puede pertenecer a*; por ejemplo:

  `/special-offers/christmas/shoes`)

### Datos del producto {#product-data}

Para retratar y administrar su producto, querrá tener una amplia gama de información sobre ellos.

Los datos del producto pueden ser:

* AEM se mantiene directamente en el sitio de la aplicación (genérico).
* AEM se mantiene en el motor de comercio electrónico y se pone a disposición de los usuarios en la práctica de la.

  Según el tipo de datos, es [sincronizado](#catalog-maintenance-data-synchronization) si es necesario o se accede directamente; por ejemplo, los datos muy volátiles y críticos, como los precios de los productos, se recuperan del motor de comercio electrónico en cada solicitud de página para garantizar que estén siempre actualizados.

AEM En cualquier caso, cuando los datos del producto se han introducido o importado en la lista de productos, se pueden ver desde la pestaña de la lista de datos. **Productos** consola. Aquí, las vistas de tarjeta y lista de un producto muestran información como:

* la imagen
* el código SKU
* cuando se modificó por última vez

![chlimage_1-7](/help/sites-administering/assets/chlimage_1-7.png)

### Variantes del producto {#product-variants}

Para los productos adecuados, también se puede almacenar información sobre las variantes. Por ejemplo, en el caso de las prendas de vestir, los diferentes colores disponibles se mantienen como variantes:

![ecommerceproductvariants](/help/sites-administering/assets/ecommerceproductvariants.png)

### Atributos del producto {#product-attributes}

AEM Los atributos individuales que se conservan sobre cada producto pueden depender del motor de comercio electrónico que se utilice y de la implementación de la. Están disponibles (según corresponda) cuando visualiza páginas de productos o edita información de productos y pueden incluir lo siguiente:

* **Imagen**

  Una imagen del producto.

* **Título**

  El nombre del producto.

* **Descripción**

  Una descripción textual del producto.

* **Etiquetas**

  Etiquetas utilizadas para agrupar productos relacionados.

* **Categoría de recursos predeterminada**

  Una categoría predeterminada para los recursos.

* **Datos de ERP**

  Información sobre planificación de recursos empresariales (ERP).

   * **SKU**

     Información sobre la unidad de almacén (SKU).

   * **Color**
   * **Tamaño**
   * **Precio**

     El precio unitario del producto.

* **Resumen**

  Resumen de las funciones del producto.

* **Características**

  Más información sobre las características del producto.

### Recursos del producto {#product-assets}

Se puede mantener una selección de activos para productos individuales. Normalmente, incluyen imágenes y vídeos.

## Catálogos {#catalogs}

Un catálogo agrupa los datos de productos para facilitar la administración y la representación al comprador. A menudo, un catálogo está estructurado según atributos como el idioma, el área geográfica, la marca, la temporada, la afición, el deporte, entre muchos otros.

### Estructura del catálogo {#catalog-structure}

#### Catálogos en varios idiomas {#catalogs-in-multiple-languages}

AEM admite contenido de productos de en varios idiomas. Al solicitar datos, el marco de trabajo de integración recupera el idioma del árbol actual (por ejemplo, `en_US` para páginas en `/content/geometrixx-outdoors/en_US`).

En el caso de las tiendas multilingües, puede importar el catálogo para cada árbol de idiomas individualmente (o copiarlo con [MSM](/help/sites-administering/msm.md)).

#### Catálogos para varias marcas {#catalogs-for-multiple-brands}

Al igual que con los idiomas, las grandes empresas multinacionales deben atender a múltiples marcas.

#### Catálogos por etiquetas {#catalogs-by-tags}

Las etiquetas también se pueden utilizar para agrupar productos en un catálogo. Pueden utilizarse para catálogos más dinámicos, como ofertas de temporada.

### Configuración del catálogo (importación inicial) {#catalog-setup-initial-import}

AEM Según la implementación, puede importar los datos de producto necesarios para el catálogo base en desde las siguientes ubicaciones:

* un archivo CSV (para la implementación genérica)
* el motor de comercio electrónico

### Mantenimiento del catálogo (sincronización de datos) {#catalog-maintenance-data-synchronization}

Es inevitable realizar más cambios en los datos del producto:

* para la implementación genérica, se pueden administrar con la variable [editor de productos](/help/commerce/cif-classic/administering/generic.md#editing-product-information)
* al utilizar un [Motor de comercio electrónico: los cambios deben sincronizarse](#data-synchronization-with-an-ecommerce-engine-ongoing)

#### Sincronización de datos con un motor de comercio electrónico (en curso) {#data-synchronization-with-an-ecommerce-engine-ongoing}

Después de la importación inicial, los cambios en los datos del producto son inevitables.

AEM Cuando se utiliza un motor de comercio electrónico, los datos del producto se mantienen allí y deben estar disponibles en el mercado de trabajo de la. Estos datos del producto deben sincronizarse cuando se realicen actualizaciones.

Esto puede depender del tipo de datos:

* A [la sincronización periódica se utiliza junto con una fuente de datos de cambios](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#product-synchronization-and-publishing).

  Además de esto, puede seleccionar actualizaciones específicas para una actualización rápida.

* Se recuperan del motor de comercio datos muy volátiles, como la información de precios, para cada solicitud de página, a fin de garantizar que estén siempre actualizados.

### Catálogos: rendimiento y escala {#catalogs-performance-and-scaling}

La importación de un catálogo grande con un número elevado de productos (más de 100 000) desde un motor de comercio electrónico (PIM) puede afectar al sistema debido al gran número de nodos. También puede ralentizar la instancia de creación si los productos tienen recursos asociados (por ejemplo, imágenes de productos). Esto se debe a que el posprocesamiento de estos recursos consume mucha CPU y memoria.

Hay varias estrategias que puede elegir para solucionar estos problemas:

* [Agrupamiento](#bucketing) - para atender el gran número de nodos
* [Descargar recurso después del procesamiento en una instancia dedicada](#offload-asset-post-processing-to-a-dedicated-instance)
* [Importar solo datos de productos](#only-import-product-data)
* [Importar limitación y guardar por lotes](#import-throttling-and-batch-saves)
* [Pruebas de rendimiento](#performance-testing)
* [Rendimiento - Varios](#performance-miscellaneous)

#### Agrupamiento {#bucketing}

Si un nodo JCR tiene muchos nodos secundarios directos (por ejemplo, 1000 y más), se requieren bloques (carpetas fantasma) para garantizar que el rendimiento no se vea afectado. Se generan según un algoritmo al importar.

Estos contenedores toman la forma de carpetas fantasma que se introducen en la estructura del catálogo, pero se pueden configurar para que no se vean en las direcciones URL públicas.

#### Descargar recurso después del procesamiento en una instancia dedicada {#offload-asset-post-processing-to-a-dedicated-instance}

Este escenario implica la configuración de dos instancias de autor:

1. Instancia de autor maestra

   Importa datos de producto desde PIM, en el que el posprocesamiento de las rutas de recursos está deshabilitado.

1. Instancia de autor DAM dedicada

   Importa y posprocesa recursos de producto del PIM y, a continuación, los replica en la instancia de autor principal para su uso.

![Diagrama de arquitectura](/help/sites-administering/assets/chlimage_1-8.png)

#### Importar solo datos de productos {#only-import-product-data}

En el caso de los productos que no contienen recursos (imágenes) para importar, puede importar los datos del producto sin verse afectado por el posprocesamiento de recursos.

![Diagrama de arquitectura](/help/sites-administering/assets/chlimage_1-9.png)

#### Pruebas de rendimiento {#performance-testing}

AEM Las pruebas de rendimiento deben tenerse en cuenta en las implementaciones de eCommerce de:

* Entorno de creación:

  La actividad en segundo plano (por ejemplo, la importación) puede producirse al mismo tiempo que la actividad normal del usuario (por ejemplo, la edición de páginas) e incluso si el rendimiento del front-end recibe (en general) una prioridad mayor, el mal rendimiento visto por los autores en línea puede provocar frustración y bloquear una decisión de lanzamiento.

* Entorno de publicación:

  La replicación es un proceso esencial para garantizar que el contenido se publique de forma rápida y fiable. Esto puede verse afectado por la forma en que el autor agrupa el contenido que se va a publicar.

* Front-end:

  La combinación de invalidaciones de front-end y caché puede causar sorpresas de rendimiento. Las pruebas ayudan a evitarlos.

Tenga en cuenta que estas pruebas de rendimiento requieren conocer y analizar el destinatario:

* Volúmenes de contenido

   * Assets
   * Productos y SKU de I18ned localizados

* Actividad de usuario:

   * Edición masiva
   * Publicación masiva
   * Solicitudes de búsqueda intensas

* Procesos de fondo

   * Importaciones
   * Actualizaciones de sincronización (por ejemplo, precios)

* Requisitos de mantenimiento (copia de seguridad, optimización de Tar PM, recopilación de residuos del almacén de datos, etc.)

#### Rendimiento - Varios {#performance-miscellaneous}

Para todas las implementaciones, se pueden tener en cuenta los siguientes puntos:

* Como el producto, las unidades y categorías de mantenimiento de existencias pueden ser numerosas, intente utilizar el menor número de nodos posible para modelar el contenido.

  Cuantos más nodos tenga, más flexible será su contenido (por ejemplo, parsys). Sin embargo, todo es un equilibrio y ¿necesita flexibilidad individual (de forma predeterminada) al manipular (por ejemplo) productos de 30 000?

* Evite la duplicación todo lo que pueda (consulte localización) o, cuando lo haga, piense en los nodos a los que conduce la duplicación.
* Intente etiquetar el contenido lo más posible para preparar la optimización de la consulta.

  Por ejemplo:

  `/content/products/france/fr/shoe/reebok/pump/46 SKU`

  debe tener una etiqueta por nivel de contenido (es decir, país, idioma, categoría, marca, producto). Buscando por

  `//element(*,my:Sku)[@country='france' and @language='fr'`

  y

  `@category='shoe' and @brand='reebok' and @product='pump']`

  será drásticamente más rápido que buscar

  `/jcr:root/content/france/fr/shoe/reebok/pump/element(*,my:Sku)`

* En su pila técnica, planifique el modelo y los servicios de acceso a contenido factorizado. Esta es una práctica recomendada general, pero es aún más crucial aquí, ya que puede, en fases de optimización, añadir cachés de aplicación para datos que se leen con frecuencia (y con los que no desea rellenar la caché del paquete).

  Por ejemplo, la administración de atributos suele ser un buen candidato para el almacenamiento en caché, ya que se refiere a los datos que se actualizan mediante la importación de productos.
* Considere el uso de [páginas de proxy](#proxy-pages).

### Páginas de sección de catálogo {#catalog-section-pages}

Las secciones de catálogo proporcionan, por ejemplo, lo siguiente:

* una introducción (imagen o texto) a la categoría; también se puede utilizar para titulares y teasers para promocionar ofertas especiales
* vínculos a los productos individuales de esa categoría
* vínculos a otras categorías

![ecommerce_categoryrunning](/help/sites-administering/assets/ecommerce_categoryrunning.png)

### Páginas de producto {#product-pages}

Las páginas de productos proporcionan información completa sobre productos individuales. Las actualizaciones dinámicas de también se reflejan; por ejemplo, los cambios de precios registrados en el motor de comercio electrónico.

AEM Las páginas de producto son páginas de productos que utilizan la variable **Product** componente; por ejemplo, dentro de **Producto de comercio** plantilla:

![ecommerce_nairobirunnersgreen](/help/sites-administering/assets/ecommerce_nairobirunnersgreen.png)

El componente Producto proporciona lo siguiente:

* Información general del producto, incluidos texto e imágenes.
* Asignación de precios; se recupera del motor de comercio electrónico cada vez que se muestra o actualiza la página.
* Información de variante del producto; por ejemplo, color y tamaño.

Esta información permite al comprador seleccionar lo siguiente al añadir un artículo a su cesta:

* Variantes de color y tamaño
* Cantidad

#### Páginas de aterrizaje del producto {#product-landing-pages}

AEM Se trata de páginas de datos que proporcionan principalmente información estática; por ejemplo, una introducción y descripción general con vínculos a las páginas de productos subyacentes.

### Componente del producto {#product-component}

El **Product** se puede agregar a cualquier página con una página principal que envíe los metadatos necesarios (es decir, las rutas a `cartPage` y `cartObject`). En el sitio de demostración, Geometrixx Outdoors, esto lo proporciona `UserInfo.jsp`.

El **Product** El componente también se puede personalizar según sus necesidades individuales.

### Páginas proxy {#proxy-pages}

Las páginas proxy se utilizan para simplificar la estructura del repositorio y optimizar el almacenamiento para catálogos grandes.

AEM La creación de un catálogo utiliza diez nodos por producto, ya que proporciona componentes individuales para cada producto que puede actualizar y personalizar en el propio. Este gran número de nodos puede convertirse en un problema si el catálogo contiene cientos o incluso miles de productos. Para evitar problemas, puede crear el catálogo mediante páginas proxy.

Las páginas proxy utilizan una estructura de dos nodos ( `cq:Page` y `jcr:content`) que no contiene nada del contenido del producto real. El contenido se genera, a petición del cliente, haciendo referencia a los datos del producto y a la página de la plantilla.

Sin embargo, hay una compensación. AEM No podrá personalizar la información del producto dentro de, ya que se utiliza una plantilla estándar (definida para su sitio).

>[!NOTE]
>
>No tendrá ningún problema si importa un catálogo grande sin páginas proxy.
>
>Puede convertir una metodología a la otra en cualquier momento. También puede convertir una subsección del catálogo.

## Promociones y cupones {#promotions-and-vouchers}

### Cupones {#vouchers}

Los cupones son un método probado y probado de ofrecer descuentos para atraer a los compradores a hacer una compra y / o recompensar la lealtad del cliente.

* Suministro de cupones:

   * Un código de cupón (que el comprador debe escribir en el carro de compras).
   * Una etiqueta de cupón (que se mostrará después de que el comprador la haya introducido en el carro de compras).
   * Una ruta de promoción (que define la acción que aplica el cupón).

* Los motores de comercio externo también pueden proporcionar cupones.

AEM En la:

* Un cupón es un componente basado en páginas que se crea o edita con la consola Sitios web.
* El **Cupón** El componente proporciona:

   * Un procesador para la administración de cupones; muestra todos los cupones que hay actualmente en el carro de compras.
   * Los cuadros de diálogo de edición (formulario) para administrar (añadir/eliminar) los cupones.
   * Las acciones necesarias para agregar o eliminar cupones en el carro de compras.

* Los cupones no tienen sus propias fechas u horas de activación y desactivación, sino que utilizan las de sus campañas principales.

>[!NOTE]
>
>AEM utiliza el término **Cupón**, este es sinónimo del término **Cupón**.

### Promociones {#promotions}

Las promociones, junto con los cupones, le permiten realizar escenarios como:

* Una compañía proporciona precios personalizados para los empleados, que es una lista de usuarios hecha a mano.
* Los clientes a largo plazo reciben descuentos en todos los pedidos.
* Un precio de venta ofrecido durante un periodo de tiempo bien definido.
* Un cliente recibe un cupón cuando su pedido anterior superaba una cantidad específica.
* Un cliente que compra *product-X* se ofrece un descuento el *product-Y* (productos de par).

Las promociones no las mantienen los gestores de información de productos, sino los gestores de marketing:

* Una promoción es un componente basado en páginas que se crea o edita con la consola Sitios web. &quot;
* Oferta de promociones:

   * Una prioridad
   * Una ruta del controlador de promoción

* Puede conectar las promociones a una campaña para definir su fecha/hora de activación/desactivación.
* Puede conectar las promociones a una experiencia para definir sus segmentos.
* Las promociones que no estén conectadas a una experiencia no se activarán por sí solas, sino que se podrán activar mediante un cupón.
* El componente Promoción contiene:

   * procesadores y cuadros de diálogo para la administración de promociones
   * subcomponentes para procesar y editar parámetros de configuración específicos de los controladores de promoción

AEM En las promociones también se integran las promociones en la [Campaign Management](/help/sites-authoring/personalization.md):

* a [campaña](/help/sites-authoring/personalization.md) especifica los tiempos de activación/desactivación
* [experiencias](/help/sites-authoring/personalization.md) *dentro* la campaña se utiliza para agrupar recursos (páginas de teaser, promociones, etc.) según el segmento de audiencia al que correspondan

Una promoción se puede llevar a cabo en una experiencia o directamente en la campaña:

* Si una promoción se celebra en una experiencia, se puede aplicar automáticamente a un segmento de audiencia.

  Por ejemplo, en el sitio de muestra geometrixx-outdoors, la promoción:

  `/content/campaigns/geometrixx-outdoors/big-spender/ordervalueover100/free-shipping`

  está en una experiencia de y se activa automáticamente siempre que el segmento ( `ordervalueover100`) se resuelve.

* Si una promoción no aparece dentro de una experiencia (solo en la campaña), no se puede aplicar automáticamente a una audiencia. Sin embargo, se puede despedir si el comprador introduce un cupón en el carro de compras y ese cupón hace referencia a la promoción.

  Por ejemplo, la promoción:

  `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

  está fuera de una experiencia y, por lo tanto, nunca se activa automáticamente (es decir, según la segmentación). Sin embargo, los cupones hacen referencia a él, que se puede encontrar en varias de las experiencias de la campaña de artículos. Al introducir estos códigos de cupón en el carro de compras, se activa la promoción.

>[!NOTE]
>
>[promociones de hybris](https://www.hybris.com/modules/promotion) y [cupones hybris](https://www.hybris.com/en/modules/voucher) cubrir todo lo que influye en el carro de compras y está relacionado con los precios. Contenido de marketing específico de la promoción (como titulares, etc.). no forma parte de la promoción de hybris.

## Personalización {#personalization}

### Registro de cliente y cuentas {#customer-registration-and-accounts}

AEM Cuando un comprador se registra, los detalles de la cuenta deben sincronizarse entre el motor de comercio electrónico y el sistema de comercio electrónico (eCommerce). Los datos confidenciales se mantienen de forma independiente, pero los perfiles se comparten:

![chlimage_1-10](/help/sites-administering/assets/chlimage_1-10.png)

El mecanismo exacto puede depender del escenario:

1. Las cuentas de usuario existen en ambos sistemas:

   1. No se requiere ninguna acción.

1. AEM La cuenta de usuario solo existe en los siguientes:

   1. AEM El usuario se crea en el motor de comercio electrónico con el mismo ID de cuenta y una contraseña aleatoria que se almacenará en el sistema de acceso a la cuenta de usuario de la que se dispone en el código de acceso de la cuenta de usuario de eCommerce.
   1. AEM La contraseña aleatoria es necesaria, ya que intenta iniciar sesión en el motor de comercio electrónico en la primera llamada (por ejemplo, cuando se solicita una página de producto y se hace referencia al motor de comercio electrónico para el precio). AEM Debido a que esto sucede después del inicio de sesión de la, la contraseña no está disponible.

1. La cuenta de usuario solo existe en el motor de comercio electrónico:

   1. AEM La cuenta se crea en la misma cuenta con el mismo ID de cuenta y la misma contraseña de.

AEM Al utilizar un motor de comercio electrónico, solo almacena el ID y la contraseña de la cuenta (opcionalmente, un grupo de usuarios). El resto de la información se almacena en el motor de comercio electrónico.

>[!NOTE]
>
>AEM AEM Al utilizar un motor de comercio electrónico, debe asegurarse de que las cuentas creadas para los usuarios que inician sesión en una instancia de se replican (por ejemplo, mediante flujos de trabajo) en cualquier otra instancia de la que se comunique con ese motor.
>
>AEM De lo contrario, estas otras instancias de también intentarán crear cuentas para los mismos usuarios en el motor. Estas acciones fallan con un `DuplicateUidException` viene del motor.

### Registro de cliente {#customer-sign-up}

A menudo, es necesario registrarse para que el comprador tenga acceso al carro de compras. Esto requiere registro (Crear cuenta) para poder crear una cuenta específica del cliente.

![chlimage_1-11](/help/sites-administering/assets/chlimage_1-11.png)

>[!NOTE]
>
>También admite un carro de compras y un cierre de compra anónimos.

### Inicio de sesión de cliente {#customer-sign-in}

Después de registrarse, el comprador puede iniciar sesión con su cuenta para que se puedan rastrear sus acciones y cumplir sus pedidos.

![chlimage_1-12](/help/sites-administering/assets/chlimage_1-12.png)

### Inicio de sesión único {#single-sign-on}

AEM Se proporciona el inicio de sesión único (SSO), para que los autores se conozcan tanto en el sistema de comercio electrónico como en el de comercio electrónico sin tener que iniciar sesión dos veces.

### myAccount {#myaccount}

Los datos de transacción del motor de comercio electrónico se combinan con la información personal sobre el comprador. AEM utiliza algunos de estos datos como datos de perfil. AEM La acción de un formulario en la escribe información en el motor de comercio electrónico.

Hay una página que le permite administrar fácilmente la información de su cuenta. Puede acceder a ella haciendo clic en **Mi cuenta** en la parte superior de una página Geometrixx o navegando hasta `/content/geometrixx-outdoors/en/user/account.html`.

![chlimage_1-13](/help/sites-administering/assets/chlimage_1-13.png)

### Libreta de direcciones {#address-book}

El sitio debe almacenar una selección de direcciones, incluidas las direcciones de envío, facturación y alternativas. AEM Esto se puede implementar mediante formularios basados en el formato de dirección predeterminado o puede utilizar el componente Libreta de direcciones proporcionado por el administrador de direcciones de la.

Este componente de Libreta de direcciones le permite:

* editar direcciones en el libro
* seleccionar una dirección de la libreta de direcciones de envío
* seleccionar una dirección de la libreta de direcciones de facturación

Puede elegir la dirección que desee de forma predeterminada.

Se puede acceder al componente de libreta de direcciones desde el **Mi cuenta** haciendo clic en **Libreta de direcciones** o navegando a `/content/geometrixx-outdoors/en/user/account/address-book.html`.

![chlimage_1-14](/help/sites-administering/assets/chlimage_1-14.png)

Puede hacer clic en **Añadir nueva dirección...** para agregar una dirección a su libreta de direcciones. Se abrirá un formulario que puede rellenar y, a continuación, hacer clic en **Añadir dirección**.

>[!NOTE]
>
>Puede escribir varias direcciones en la Libreta de direcciones.

La Libreta de direcciones se utiliza cuando &quot;cierra la compra&quot; del carro de compras:

![chlimage_1-15](/help/sites-administering/assets/chlimage_1-15.png)

Las direcciones se mantienen a continuación `user_home/profile/addresses`.
Por ejemplo, para Alison Parker, estaría en /home/users/geometrixx/aparker@geometrixx.info/profile/addresses

Puede elegir la dirección que desee como predeterminada, ya que esta información se conserva en el perfil del comprador en lugar de en la dirección. La propiedad de perfil `address.default` se establece con la ruta de la dirección seleccionada para el valor.

### Precios específicos del cliente {#customer-specific-pricing}

AEM El motor de comercio electrónico utiliza el contexto (en esencia, la información del comprador) para determinar el precio que mantiene y, a continuación, proporcionar la información correcta de vuelta a la información de los clientes de forma que puedan obtener la información que necesitan los proveedores de servicios de comercio electrónico.

## Carro de compras y pedidos {#shopping-cart-and-orders}

Al realizar compras, el comprador explora las páginas de productos y selecciona artículos para colocarlos en su carro de compras. Cuando se procede al cierre de compra, se puede realizar un pedido.

### Compradores anónimos {#anonymous-shoppers}

Un cliente anónimo puede:

* Ver productos
* Agregar productos al carro de compras
* Realice el cierre de compra para realizar su pedido

>[!NOTE]
>
>Según la configuración de la información de la dirección de la instancia o el registro de cliente, puede ser necesario antes del cierre de compra.

### Compradores registrados {#registered-shoppers}

Un cliente registrado puede:

* Inicie sesión en su cuenta
* Ver productos
* Agregar productos al carro de compras
* Realice el cierre de compra para realizar su pedido
* Ver y rastrear pedidos anteriores

### Resumen del contenido del carro de compras {#shopping-cart-content-overview}

El carro de compras proporciona lo siguiente:

* una descripción general de los elementos seleccionados
* vínculos a las páginas de productos de los elementos seleccionados
* la capacidad de:

   * actualizar el número/cantidad de artículos individuales
   * quitar elementos individuales

![ecommerce_shoppingcart](/help/sites-administering/assets/ecommerce_shoppingcart.png)

El carro de compras se guarda según el motor que se esté utilizando:

* AEM El genérico almacena el carro de compras en una cookie.
* Algunos motores de comercio electrónico pueden almacenar el carro de compras en una sesión.

En cualquier caso, los elementos permanecen en el carro de compras (y se pueden restaurar) durante el inicio de sesión o el cierre de sesión (pero solo en el mismo equipo o explorador). Por ejemplo:

* examinar como `anonymous` y agregar productos al carro de compras
* iniciar sesión como `Allison Parker` - El carrito de Allison está vacío
* Añadir productos al carrito de compras de Allison
* cerrar sesión: el carro muestra los productos de `anonymous`

* iniciar sesión de nuevo como `Allison Parker` - Los productos de Allison están restaurados

>[!NOTE]
>
>Un carro de compras anónimo solo se puede restaurar en el mismo equipo o explorador.

>[!NOTE]
>
>No se recomienda probar la restauración del contenido del carro de compras con `admin` cuenta de, ya que puede entrar en conflicto con la `admin` cuenta del motor de comercio electrónico (por ejemplo, hybris).

>[!NOTE]
>
>hybris se puede configurar para que elimine los carros de compras pendientes después de un período de tiempo definido.

Antes del cierre de compra, los cambios en los precios se reflejan (en ambos sistemas) a medida que se producen.

### Información del pedido {#order-information}

AEM AEM En función de la información de implementación sobre un pedido que se conserva en el motor de comercio electrónico o en el sistema de comercio electrónico, esta información se procesa mediante la función de procesamiento de datos de tipo.

Se almacena diversa información, que puede incluir:

* **ID de pedido**

  Número de referencia del pedido.

* **Realizado**

  La fecha en la que se realizó el pedido.

* **Estado**

  El estado del pedido; por ejemplo, Enviado.

* **Moneda**

  La moneda del pedido.

* **Elementos de contenido**

  Una lista de los elementos pedidos.

* **Subtotal**

  El coste total de los artículos pedidos.

* **Impuestos**

  El importe de los impuestos adeudados en el pedido.

* **Envío**

  Gastos de envío.

* **Total**

  El valor total del pedido; artículos pedidos, impuestos y envío.

* **Dirección de facturación**

  La dirección a la que se debe enviar la factura.

* **Testigo de pago**

  La forma de pago.

* **Estado de pago**

  El estado del pago.

* **Dirección de envío**

  La dirección a la que deben enviarse las mercancías.

* **Método de envío**

  El método de envío; por ejemplo, terrestre, marítimo o aéreo.

* **Número de seguimiento**

  Cualquier número de seguimiento utilizado por la empresa de envío.

* **Vínculo de seguimiento**

  El vínculo utilizado para rastrear el pedido mientras se envía.

>[!NOTE]
>
>Los campos utilizados en el asistente para crear pedidos dependen de que haya un andamiaje táctil optimizado definido para la ubicación. En el ejemplo genérico, se puede encontrar en:
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`

AEM Cuando el pedido se mantiene dentro de la consola Pedidos muestra lo siguiente para cada pedido:

* el número de artículos del carro de compras
* el valor total del pedido
* cuando se realizó el pedido
* el estado

![chlimage_1-16](/help/sites-administering/assets/chlimage_1-16.png)

### Seguimiento de pedidos {#order-tracking}

Después de realizar un pedido, los compradores suelen regresar a:

* Comprobar el estado de su pedido
* Eliminar productos del pedido
* Añadir productos al pedido

Después de recibir la entrega del pedido, es posible que los compradores también deseen ver el historial de pedidos realizados durante un período de tiempo.

El motor de comercio electrónico se encarga de la tramitación y el seguimiento de los pedidos. AEM La información se puede mostrar utilizando el componente Historial de Pedidos, que muestra todos los detalles relevantes, incluidos los cupones y las promociones aplicadas. Por ejemplo:

![chlimage_1-17](/help/sites-administering/assets/chlimage_1-17.png)

## Cierre de compra {#checkout}

AEM El cierre de compra se implementa con los formularios estándar de. Esto permite al administrador de marketing personalizar la experiencia con el contenido de marketing.

AEM A continuación, el departamento de comercio electrónico administra el proceso de cierre de compra con los datos de los formularios de la.

### Seguridad de pago {#payment-security}

Los datos de pago, incluida la información de la tarjeta de crédito, a menudo se administran mediante el motor de comercio electrónico. AEM reenvía dicha información transaccional al motor (desde donde se reenvía a continuación a un servicio de procesamiento de pagos).

Se puede lograr la conformidad con la industria de tarjetas de pago (PCI).

### Confirmación del pedido {#confirmation-of-order}

El pedido se confirma en pantalla y se puede rastrear con la variable [seguimiento de pedidos](#order-tracking).

## Búsqueda {#search-features}

![chlimage_1-18](/help/sites-administering/assets/chlimage_1-18.png)

AEM Dado que utiliza páginas estándar para los productos, puede utilizar el componente de búsqueda estándar para crear una página de búsqueda.

Si necesita una implementación más completa, puede hacer lo siguiente:

* Amplíe el componente de búsqueda predeterminado con la funcionalidad que necesita.
* Implemente el método de búsqueda en su `CommerceService` y, a continuación, utilice el componente de búsqueda eCommerce en la página de búsqueda.

Al utilizar un motor de comercio electrónico, la API de búsqueda de comercio electrónico se puede implementar completamente en la solución del motor de comercio electrónico, por lo que puede utilizar el componente de búsqueda de comercio electrónico que se proporciona de forma predeterminada. La búsqueda con facetas le permite buscar JCR o el motor:
