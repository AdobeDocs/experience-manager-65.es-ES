---
title: Desarrollo (genérico)
seo-title: Desarrollo (genérico)
description: El marco de integración incluye una capa de integración con una API que le permite crear componentes AEM para las capacidades de comercio electrónico
seo-description: El marco de integración incluye una capa de integración con una API que le permite crear componentes AEM para las capacidades de comercio electrónico
uuid: 393bb28a-9744-44f4-9796-09228fcd466f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: d8ee3b57-633a-425e-bf36-646f0e0bad52
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1886'
ht-degree: 0%

---


# Desarrollando (genérico){#developing-generic}

>[!NOTE]
>
>[También hay ](/help/sites-developing/ecommerce.md#api-documentation) documentación de API disponible.

El marco de integración incluye una capa de integración con una API. Esto le permite crear componentes AEM para las capacidades de comercio electrónico (independientemente del motor de comercio electrónico específico). También le permite utilizar la base de datos CRX interna o conectar un sistema de comercio electrónico y extraer datos de productos en AEM.

Se proporcionan varios componentes de AEM listos para usar para utilizar la capa de integración. Actualmente son:

* Un componente de visualización de productos
* Un carro de compras
* Promociones y vales
* Modelos de catálogo y de sección
* Cierre de compra
* Búsqueda  

Para la búsqueda se proporciona un enlace de integración que le permite utilizar la búsqueda AEM, una búsqueda de terceros (como Search&amp;Promote) o una combinación de estos.

## Selección del motor de comercio electrónico {#ecommerce-engine-selection}

El marco de comercio electrónico se puede utilizar con cualquier solución de comercio electrónico; el motor que se utiliza debe identificarse por AEM, incluso cuando se utiliza el motor genérico AEM:

* Los motores de comercio electrónico son servicios OSGi que admiten la interfaz `CommerceService`

   * Los motores se pueden distinguir mediante una propiedad de servicio `commerceProvider`

* AEM admite `Resource.adaptTo()` para `CommerceService` y `Product`

   * La implementación `adaptTo` busca una propiedad `cq:commerceProvider` en la jerarquía del recurso:

      * Si se encuentra, el valor se utiliza para filtrar la búsqueda del servicio de comercio.
      * Si no se encuentra, se utiliza el servicio de comercio de mayor clasificación.
   * Se utiliza una mezcla `cq:Commerce` para que se pueda agregar la `cq:commerceProvider` a los recursos con establecimiento inflexible de tipos.


* La propiedad `cq:commerceProvider` también se utiliza para hacer referencia a la definición de fábrica de comercio adecuada.

   * Por ejemplo, una propiedad `cq:commerceProvider` con el valor geometrixx se correlacionará con la configuración OSGi para **Day CQ Commerce Factory for Geometrixx-Outdoors** (`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`), donde el parámetro `commerceProvider` también tiene el valor `geometrixx`.
   * Aquí se pueden configurar otras propiedades (cuando sea apropiado y esté disponible).

En una instalación AEM estándar se requiere una implementación específica, por ejemplo:

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | ejemplo de geometrixx; esto incluye extensiones mínimas de la API genérica |

### Ejemplo {#example}

```shell
/etc/commerce/products/geometrixx-outdoors
+ cq:commerceProvider = geometrixx
  + adobe-logo-shirt
    + cq:commerceType = product
    + price = 12.50
  + adobe-logo-shirt_S
    + cq:commerceType = variant
    + size = S
  + adobe-logo-shirt_XL
    + cq:commerceType = variant
    + size = XL
    + price = 14.50
```

>[!NOTE]
>
>Con CRXDE Lite puede ver cómo se gestiona esto en el componente de producto para la implementación genérica de AEM:
>
>`/apps/geometrixx-outdoors/components/product`

### Administración de sesiones {#session-handling}

Sesión para almacenar información relacionada con el carro de compras del cliente.

El **CommerceSession**:

* Es propietario del **carro de compras**

   * realiza tareas de adición/eliminación/etc.
   * realiza los distintos cálculos en el carro de compras;

      `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* Persistencia de los datos **order**:

   `CommerceSession.getUserContext()`

* Puede recuperar o actualizar los detalles del envío mediante `updateOrder(Map<String, Object> delta)`
* También posee la conexión de procesamiento **pago**
* También posee la conexión **de despacho**

### Arquitectura {#architecture}

#### Arquitectura del producto y las variantes {#architecture-of-product-and-variants}

Un solo producto puede tener varias variaciones; por ejemplo, puede variar según el color o el tamaño. Un producto debe definir qué propiedades impulsan la variación; denominamos estos *ejes de variante*.

Sin embargo, no todas las propiedades son ejes de variante. Las variaciones también pueden afectar a otras propiedades; por ejemplo, el precio puede depender del tamaño. Estas propiedades no pueden ser seleccionadas por el comprador y, por lo tanto, no se consideran ejes de variante.

Cada producto o variante está representado por un recurso y, por lo tanto, asigna 1:1 a un nodo de repositorio. Es un corolario que un producto específico y/o una variante se puedan identificar de forma única por su trayectoria.

Cualquier recurso de producto puede representarse mediante `Product API`. La mayoría de las llamadas de la API de producto son específicas de la variación (aunque las variaciones pueden heredar valores compartidos de un antecesor), pero también hay llamadas que lista el conjunto de variaciones ( `getVariantAxes()`, `getVariants()`, etc.).

>[!NOTE]
>
>De hecho, los ejes de variante se determinan por el resultado que `Product.getVariantAxes()` devuelve:
>
>* para la implementación genérica AEM leerla desde una propiedad en los datos del producto ( `cq:productVariantAxes`)
>
>
Mientras que los productos (en general) pueden tener muchos ejes de variante, el componente de producto listo para usar solo gestiona dos:
>
>1. `size`
>1. más uno más

>
>   
Esta variante adicional se selecciona mediante la propiedad `variationAxis` de la referencia del producto (generalmente `color` para Geometrixx Outdoors).

#### Referencias del producto y datos PIM {#product-references-and-pim-data}

En general:

* Los datos de PIM se encuentran en `/etc`

* Referencias del producto en `/content`.

Debe haber un mapa 1:1 entre las variaciones del producto y los nodos de datos del producto.

Las referencias de producto también deben tener un nodo para cada variación presentada, pero no es necesario presentar todas las variaciones. Por ejemplo, si un producto tiene variaciones S, M, L, los datos del producto pueden ser:

```shell
etc
  commerce
    products
      shirt
        shirt-s
        shirt-m
        shirt-l
```

Mientras que un catálogo &quot;grande y alto&quot; solo puede tener:

```shell
content
  big-and-tall
    shirt
      shirt-l
```

Por último, no es necesario utilizar los datos del producto. Puede colocar todos los datos del producto debajo de las referencias en el catálogo; pero no puede tener varios catálogos sin duplicar todos los datos del producto.

**API**

#### com.adobe.cq.commerce.api.Interfaz de producto {#com-adobe-cq-commerce-api-product-interface}

```java
public interface Product extends Adaptable {

    public String getPath();            // path to specific variation
    public String getPagePath();        // path to presentation page for all variations
    public String getSKU();             // unique ID of specific variation

    public String getTitle();           // shortcut to getProperty(TITLE)
    public String getDescription();     // shortcut to getProperty(DESCRIPTION)
    public String getImageUrl();        // shortcut to getProperty(IMAGE_URL)
    public String getThumbnailUrl();    // shortcut to getProperty(THUMBNAIL_URL)

    public <T> T getProperty(String name, Class<T> type);

    public Iterator<String> getVariantAxes();
    public boolean axisIsVariant(String axis);
    public Iterator<Product> getVariants(VariantFilter filter) throws CommerceException;
}
```

#### com.adobe.cq.commerce.api.VariantFilter {#com-adobe-cq-commerce-api-variantfilter}

```java
/**
 * Interface for filtering variants and AxisFilter provided as common implementation
 *
 * The <code>VariantFilter</code> is used to filter variants,
 * e.g. when using {@link Product#getVariants(VariantFilter filter)}.
 */
public interface VariantFilter {
    public boolean includes(Product product);
}

/**
 * A {@link VariantFilter} for filtering variants by the given
 * axis and value. The following example returns a list of
 * variant products that have a value of <i>blue</i> on the
 * <i>color</i> axis.
 *
 * <p>
 * <code>product.getVariants(new AxisFilter("color", "blue"));</code>
 */
public class AxisFilter implements VariantFilter {

    private String axis;
    private String value;

    public AxisFilter(String axis, String value) {
        this.axis = axis;
        this.value = value;
    }

    /**
     * {@inheritDoc}
     */
    public boolean includes(Product product) {
        ValueMap values = product.adaptTo(ValueMap.class);

        if(values != null) {
            String v = values.get(axis, String.class);

            return v != null && v == value;
        }

        return false;
    }
}
```

* **Mecanismo general de Almacenamiento**

   * Los nodos de producto no son:no estructurados.
   * Un nodo de producto puede ser:

      * Una referencia, con los datos del producto almacenados en otra parte:

         * Las referencias de producto contienen una propiedad `productData`, que apunta a los datos del producto (generalmente en `/etc/commerce/products`).
         * Los datos del producto son jerárquicos; los atributos de producto se heredan de los antecesores de un nodo de datos de producto.
         * Las referencias de producto también pueden contener propiedades locales, que anulan las especificadas en los datos de producto.
      * Un producto en sí mismo:

         * Sin una propiedad `productData`.
         * Un nodo de producto que contiene todas las propiedades localmente (y no contiene una propiedad productData) hereda los atributos de producto directamente de sus propios antecesores.


* **Estructura de producto AEM-genérica**

   * Cada variante debe tener su propio nodo de hoja.
   * La interfaz de producto representa productos y variantes, pero el nodo de repositorio relacionado es específico sobre cuál es.
   * El nodo product describe los atributos del producto y los ejes de variante.

#### Ejemplo {#example-1}

```shell
+ banyan_shirt
    - cq:commerceType = product
    - cq:productAttributes = [jcr:title, jcr:description, size, price, color]
    - cq:productVariantAxes = [color, size]
    - jcr:title = Banyan Shirt
    - jcr:description = Flowery, all-cotton shirt.
    - price = 14.00
    + banyan_shirt_s
        - cq:commerceType = variant
        - size = S
        + banyan_shirt_s_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_s_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_m
        - cq:commerceType = variant
        - size = M
        + banyan_shirt_m_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_m_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_l
        - cq:commerceType = variant
        - size = L
        + banyan_shirt_l_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_l_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_xl
        - cq:commerceType = variant
        - size = XL
        - price = 18.00
```

#### Arquitectura del carro de compras {#architecture-of-the-shopping-cart}

**Componentes**

* El carro de compras es propiedad del `CommerceSession:`

   * El `CommerceSession` realiza agregar, eliminar, etc.
   * El `CommerceSession` también realiza los diversos cálculos en el carro de compras.
   * El `CommerceSession` también aplica los cupones y las promociones que se activaron en el carro de compras.

* Aunque no está directamente relacionado con el carro de compras, `CommerceSession` también debe proporcionar información de precios de catálogo (ya que posee precios)

   * Los precios pueden tener varios modificadores:

      * Descuentos de cantidad.
      * Diferentes monedas.
      * IVA y libre de IVA.
   * Los modificadores están completamente abiertos con la siguiente interfaz:

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**Almacenamiento**

* Almacenamiento

   * En el caso de los carros de AEM genéricos se almacenan en el [ClientContext](/help/sites-administering/client-context.md)

**Personalización**

* La personalización siempre debe impulsarse a través del [ClientContext](/help/sites-administering/client-context.md).
* Se crea un ClientContext `/version/` del carro de compras en todos los casos:

   * Los productos deben agregarse mediante el método `CommerceSession.addCartEntry()`.

* A continuación se muestra un ejemplo de información del carro de compras en el carro de ClientContexts:

![chlimage_1-33](assets/chlimage_1-33a.png)

#### Arquitectura de cierre de compra {#architecture-of-checkout}

**Datos de pedido y carro de compras**

El `CommerceSession` posee los tres elementos:

1. **Contenido del carro de compras**

   La API corrige el esquema de contenido del carro de compras:

   ```java
       public void addCartEntry(Product product, int quantity);
       public void modifyCartEntry(int entryNumber, int quantity);
       public void deleteCartEntry(int entryNumber);
   ```

1. **Precios**

   La API también fija el esquema de precios:

   ```java
       public String getCartPreTaxPrice();
       public String getCartTax();
       public String getCartTotalPrice();
       public String getOrderShipping();
       public String getOrderTotalTax();
       public String getOrderTotalPrice();
   ```

1. **Detalles del pedido**

   Sin embargo, los detalles del pedido *no* son corregidos por la API:

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**Cálculos de envío**

* Los formularios de pedido suelen necesitar presentar varias opciones de envío (y precios).
* Los precios pueden basarse en artículos y detalles del pedido, como peso o dirección de envío.
* El `CommerceSession` tiene acceso a todas las dependencias, por lo que se puede tratar de manera similar a los precios del producto:

   * El `CommerceSession` tiene precios de envío.
   * Utilice `updateOrder(Map<String, Object> delta)` para recuperar/actualizar los detalles del envío.

### Definición de búsqueda {#search-definition}

Siguiendo el modelo de API de servicio estándar, el proyecto eCommerce proporciona un conjunto de API relacionadas con la búsqueda que pueden ser implementadas por motores de comercio individuales.

>[!NOTE]
>
>Actualmente, sólo el motor de híbris implementa la API de búsqueda lista para usar.
>
>Sin embargo, la API de búsqueda es genérica y cada CommerceService puede implementarla individualmente.
>
>Por lo tanto, aunque la implementación genérica proporcionada de forma predeterminada no implementa esta API, puede ampliarla y agregar la funcionalidad de búsqueda.

El proyecto eCommerce contiene un componente de búsqueda predeterminado, ubicado en:

`/libs/commerce/components/search`

![chlimage_1-34](assets/chlimage_1-34a.png)

Esto hace uso de la API de búsqueda para la consulta del motor de comercio seleccionado (consulte [Selección del motor de comercio electrónico](#ecommerce-engine-selection)):

#### API de búsqueda {#search-api}

Existen varias clases genéricas/de ayuda proporcionadas por el proyecto principal:

1. `CommerceQuery`

   Se utiliza para describir una consulta de búsqueda (contiene información sobre el texto de la consulta, la página actual, el tamaño de la página, la clasificación y las facetas seleccionadas). Todos los servicios de comercio electrónico que implementan la API de búsqueda recibirán instancias de esta clase para realizar la búsqueda. Se puede crear una instancia de `CommerceQuery` a partir de un objeto de solicitud ( `HttpServletRequest`).

1. `FacetParamHelper`

   Es una clase de utilidad que proporciona un método estático - `toParams` - que se utiliza para generar cadenas de parámetro `GET` a partir de una lista de facetas y un valor alternado. Esto resulta útil en la interfaz de usuario, donde debe mostrar un hipervínculo para cada valor de cada faceta, de modo que cuando el usuario haga clic en el hipervínculo, se alternará el valor correspondiente (es decir, si se seleccionó, se eliminará de la consulta; de lo contrario, se agregará). Esto tiene en cuenta toda la lógica de manejo de facetas de varios valores o de un solo valor, valores de anulación, etc.

El punto de entrada para la API de búsqueda es el método `CommerceService#search` que devuelve un objeto `CommerceResult`. Consulte la documentación de la API para obtener más información sobre este tema.

### Desarrollo de promociones y cupones {#developing-promotions-and-vouchers}

* Cupones:

   * Un cupón es un componente basado en páginas que se crea o edita con la consola Sitios web y se almacena en:

      `/content/campaigns`

   * Suministro de cupones:

      * Código de asiento (que el comprador debe escribir en el carro de compras).
      * Una etiqueta de asiento (que se mostrará después de que el comprador la haya introducido en el carro de compras).
      * Una ruta de promoción (que define la acción a la que se aplica la licencia).
   * Los cupones no tienen su propia fecha/hora de inicio y de salida, pero utilizan las de sus campañas principales.
   * Los motores de comercio exterior también pueden suministrar vales; estos requisitos requieren un mínimo de:

      * Código de asiento
      * Un método `isValid()`
   * El componente **Cupón** ( `/libs/commerce/components/voucher`) proporciona:

      * Un procesador para la administración de vales; esto muestra los asientos que hay actualmente en el carro de compras.
      * Los cuadros de diálogo de edición (formulario) para la administración (adición/eliminación) de las licencias.
      * Acciones necesarias para agregar/quitar asientos al carro de compras o para extraerlos de él.



* Promociones:

   * Una promoción es un componente basado en páginas que se crea o edita con la consola Sitios web y se almacena en:

      `/content/campaigns`

   * Oferta de promociones:

      * Una prioridad
      * Una ruta del controlador de promoción
   * Puede conectar las promociones a una campaña para definir su fecha y hora de activación/desactivación.
   * Puede conectar las promociones a una experiencia para definir sus segmentos.
   * Las promociones que no están conectadas a una experiencia no se activan por sí solas, sino que pueden ser activadas por un cupón.
   * El componente Promoción ( `/libs/commerce/components/promotion`) contiene:

      * PROCESADORES y diálogos para la administración de promociones
      * subcomponentes para procesar y editar parámetros de configuración específicos de los controladores de promoción
   * Se suministran dos controladores de promoción de fábrica:

      * `DiscountPromotionHandler`, que aplica un descuento absoluto o porcentual para todo el carro de compras
      * `PerfectPartnerPromotionHandler`, que aplica un descuento absoluto o porcentual del producto si el producto asociado también está en el carro de compras
   * El ClientContext `SegmentMgr` resuelve los segmentos y el ClientContext `CartMgr` resuelve las promociones. Se activarán todas las promociones que estén sujetas a al menos un segmento resuelto.

      * Las promociones activadas se envían nuevamente al servidor mediante una llamada AJAX para volver a calcular el carro de compras.
      * Las promociones activadas (y los cupones añadidos) también se muestran en el panel ClientContext.




La añade/eliminación de un asiento de un carro de compras se realiza mediante la API `CommerceSession`:

```java
/**
 * Apply a voucher to this session's cart.
 *
 * @param code the voucher's code
 * @throws CommerceException
 */
public void addVoucher(String code) throws CommerceException;

/**
 * Remove a voucher that was previously added with {@link #addVoucher(String)}.
 *
 * @param code the voucher's code
 * @throws CommerceException
 */
public void removeVoucher(String code) throws CommerceException;

/**
 * Get a list of vouchers that were added to this cart via {@link #addVoucher(String)}.
 *
 * @throws CommerceException
 */
public List<Voucher> getVouchers() throws CommerceException;
```

De este modo, `CommerceSession` es responsable de comprobar si existe un vale y si se puede aplicar o no. Esto puede ser para vales que solo se pueden aplicar si se cumple una determinada condición; por ejemplo, cuando el precio total del carro es bueno (más de 100 dólares). Si no se puede aplicar un asiento por ningún motivo, el método `addVoucher` generará una excepción. Además, `CommerceSession` es responsable de actualizar los precios del carro después de agregar o eliminar un vale.

La `Voucher` es una clase similar a un grano que contiene campos para:

* Código de cupón
* Una breve descripción
* Hacer referencia a la promoción relacionada que indica el tipo y el valor de descuento

El `AbstractJcrCommerceSession` proporcionado puede aplicar comprobantes. Las licencias devueltas por la clase `getVouchers()` son instancias de `cq:Page` que contienen un nodo jcr:content con las siguientes propiedades (entre otras):

* `sling:resourceType` (Cadena): debe ser  `commerce/components/voucher`

* `jcr:title` (Cadena): para la descripción del asiento
* `code` (Cadena): el código que debe introducir el usuario para aplicar esta licencia
* `promotion` (Cadena) - la promoción que se aplicará; p. ej.  `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

Los controladores de promoción son servicios OSGi que modifican el carro de compras. El carro admitirá varios ganchos que se definirán en la interfaz `PromotionHandler`.

```java
/**
 * Apply promotion to a cart line item. The method returns a discount
 * <code>PriceInfo</code> instance or <code>null</code> if no discount
 * was applied.
 * @param commerceSession The commerce session
 * @param promotion The configured promotion
 * @param cartEntry The cart line item
 * @return A discounted <code>PriceInfo</code> or <code>null</code>
 */
public PriceInfo applyCartEntryPromotion(CommerceSession commerceSession,
                                         Promotion promotion, CartEntry cartEntry)
    throws CommerceException;

/**
 * Apply promotion to an order. The method returns a discount
 * <code>PriceInfo</code> instance or <code>null</code> if no discount
 * was applied.
 * @param commerceSession The commerce session
 * @param promotion The configured promotion
 * @return A discounted <code>PriceInfo</code> or <code>null</code>
 */
public PriceInfo applyOrderPromotion(CommerceSession commerceSession, Promotion promotion)
    throws CommerceException;

public PriceInfo applyShippingPromotion(CommerceSession commerceSession, Promotion promotion)
    throws CommerceException;

/**
 * Allows a promotion handler to define a custom, author-oriented message for a promotion.
 * The {@link com.adobe.cq.commerce.common.promotion.PerfectPartnerPromotionHandler}, for instance,
 * uses this to list the qualifying pairs of products in the current cart.
 * @param commerceSession
 * @param promotion
 * @return A message to display
 * @throws CommerceException
 */
public String getMessage(SlingHttpServletRequest request, CommerceSession commerceSession, Promotion promotion) throws CommerceException;

/**
 * Informs the promotion handler that something under the promotions root has been edited, and the handler
 * should invalidate any caches it might be keeping.
 */
public void invalidateCaches();
```

Se proporcionan tres controladores de promoción predeterminados:

* `DiscountPromotionHandler` aplica un descuento absoluto o porcentual para todo el carro de compras
* `PerfectPartnerPromotionHandler` aplica un descuento de porcentaje o absoluto del producto si el socio del producto también está en el carro de compras
* `FreeShippingPromotionHandler` aplica envío gratuito

