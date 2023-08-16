---
title: Desarrollo (genérico)
seo-title: Developing (generic)
description: AEM El marco de trabajo de integración incluye una capa de integración con una API, lo que le permite crear componentes de para las capacidades de comercio electrónico
seo-description: The integration framework includes an integration layer with an API, allowing you to build AEM components for eCommerce capabilities
uuid: 393bb28a-9744-44f4-9796-09228fcd466f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: 1138a548-d112-4446-b0e1-b7a9ea7c7604
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1860'
ht-degree: 0%

---

# Desarrollo (genérico){#developing-generic}

>[!NOTE]
>
>[Documentación de API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) también está disponible.

El marco de integración incluye una capa de integración con una API. AEM Esto le permite crear componentes de para las capacidades de comercio electrónico (independientemente del motor específico de comercio electrónico). AEM También le permite utilizar la base de datos CRX interna o conectar un sistema de comercio electrónico y extraer datos de productos en la base de datos de.

AEM Se proporcionan una serie de componentes listos para usar para usar de la capa de integración de, que son: Actualmente son:

* Un componente de visualización de producto
* Un carro de compras
* Promociones y cupones
* Modelos de catálogo y sección
* Fecha de salida
* Búsqueda

AEM Para la búsqueda se proporciona un gancho de integración que le permite utilizar la búsqueda de la, una búsqueda de terceros o una combinación de estos.

## Selección de motor de comercio electrónico {#ecommerce-engine-selection}

AEM AEM El marco de comercio electrónico se puede utilizar con cualquier solución de comercio electrónico, el motor que se utiliza debe ser identificado por los usuarios, incluso cuando se utiliza el motor genérico, que es el siguiente:

* Los motores de comercio electrónico son servicios OSGi que admiten el `CommerceService` interfaz

   * Los motores se pueden distinguir mediante una `commerceProvider` propiedad de servicio

* AEM soportes de la `Resource.adaptTo()` para `CommerceService` y `Product`

   * El `adaptTo` la implementación busca un `cq:commerceProvider` en la jerarquía del recurso:

      * Si se encuentra, el valor se utiliza para filtrar la búsqueda del servicio de comercio.
      * Si no se encuentra, se utiliza el servicio de comercio de mayor clasificación.

   * A `cq:Commerce` mixin se usa para que el `cq:commerceProvider` se puede agregar a recursos con establecimiento inflexible de tipos.

* El `cq:commerceProvider` también se utiliza para hacer referencia a la definición de commerce factory adecuada.

   * Por ejemplo, una `cq:commerceProvider` la propiedad con el valor geometrixx se correlacionará con la configuración OSGi para **Day CQ Commerce Factory for Geometrixx-Outdoors** (`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`): donde el parámetro `commerceProvider` también tiene el valor `geometrixx`.
   * Aquí se pueden configurar más propiedades (cuando corresponda y estén disponibles).

AEM En una instalación estándar se requiere una implementación específica, por ejemplo:

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | ejemplo de geometrixx; incluye extensiones mínimas a la API genérica |

### Ejemplos {#example}

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
>Con CRXDE Lite AEM puede ver cómo se gestiona esto en el componente de producto para la implementación genérica de la:
>
>`/apps/geometrixx-outdoors/components/product`

### Gestión de sesión {#session-handling}

Una sesión para almacenar información relacionada con el carro de compras del cliente.

El **CommerceSession**:

* Posee el **carro de compras**

   * realiza operaciones add/remove/etc.
   * realiza los distintos cálculos en el carro de compras;

     `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* Posee persistencia de **pedido** datos:

  `CommerceSession.getUserContext()`

* Puede recuperar o actualizar los detalles de envío utilizando `updateOrder(Map<String, Object> delta)`
* También posee el **pago** conexión de procesamiento
* También posee el **cumplimiento** conexión

### Arquitectura {#architecture}

#### Arquitectura de producto y variantes {#architecture-of-product-and-variants}

Un solo producto puede tener varias variaciones; por ejemplo, puede variar según el color y/o el tamaño. Un producto debe definir qué propiedades impulsan la variación; llamamos a estas *ejes de variante*.

Sin embargo, no todas las propiedades son ejes de variante. Las variaciones también pueden afectar a otras propiedades; por ejemplo, el precio puede depender del tamaño. Estas propiedades no pueden ser seleccionadas por el comprador y, por lo tanto, no se consideran ejes de variante.

Cada producto o variante está representado por un recurso y, por lo tanto, se asigna 1:1 a un nodo de repositorio. Es un corolario que un producto específico o una variante se puedan identificar de forma exclusiva por su ruta.

Cualquier recurso de producto puede representarse mediante una `Product API`. La mayoría de las llamadas que se realizan en la API de producto son específicas de cada variación (aunque las variaciones pueden heredar valores compartidos de un antecesor), pero también hay llamadas que enumeran el conjunto de variaciones ( `getVariantAxes()`, `getVariants()`, etc.).

>[!NOTE]
>
>En efecto, un eje variante está determinado por lo que sea `Product.getVariantAxes()` devuelve:
>
>* AEM para la implementación genérica, lo lee de una propiedad en los datos del producto ( `cq:productVariantAxes`)
>
>Aunque los productos (en general) pueden tener muchos ejes de variante, el componente de producto listo para usar solo gestiona dos:
>
>1. `size`
>1. más uno más
>
>   Esta variante adicional se selecciona mediante la variable `variationAxis` propiedad de la referencia del producto (normalmente `color` para Geometrixx Outdoors).

#### Referencias del producto y datos de PIM {#product-references-and-pim-data}

En general:

* Los datos de PIM se encuentran en `/etc`

* Referencias de producto en `/content`.

Debe haber una asignación individual entre las variaciones de productos y los nodos de datos de productos.

Las referencias de producto también deben tener un nodo para cada variación presentada, pero no es necesario presentar todas las variaciones. Por ejemplo, si un producto tiene variaciones de S, M y L, los datos del producto podrían ser:

```shell
etc
  commerce
    products
      shirt
        shirt-s
        shirt-m
        shirt-l
```

Mientras que un catálogo &quot;Grande y Alto&quot; podría tener solo:

```shell
content
  big-and-tall
    shirt
      shirt-l
```

Por último, no es necesario utilizar datos de productos. Puede colocar todos los datos del producto debajo de las referencias en el catálogo; pero, en realidad, no puede tener varios catálogos sin duplicar todos los datos del producto.

**API**

#### Interfaz de com.adobe.cq.commerce.api.Product {#com-adobe-cq-commerce-api-product-interface}

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

#### com.adobe.cq.commerce.api.VariantFilter  {#com-adobe-cq-commerce-api-variantfilter}

```java
/**
 * Interface for filtering variants and AxisFilter provided as common implementation
 *
 * The <code>VariantFilter</code> is used to filter variants,
 * for example, when using {@link Product#getVariants(VariantFilter filter)}.
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

* **Mecanismo general de almacenamiento**

   * Los nodos de producto no son: desestructurados.
   * Un nodo de producto puede ser:

      * Una referencia, con los datos del producto almacenados en otra parte:

         * Las referencias de producto contienen un `productData` , que apunta a los datos del producto (normalmente en `/etc/commerce/products`).
         * Los datos del producto son jerárquicos; los atributos del producto se heredan de los antecesores de un nodo de datos del producto.
         * Las referencias de producto también pueden contener propiedades locales, que anulan las especificadas en sus datos de producto.

      * Un producto en sí:

         * Sin un `productData` propiedad.
         * Un nodo de producto que contiene todas las propiedades localmente (y no contiene una propiedad productData) hereda directamente los atributos de producto de sus propios antecesores.

* **AEM Estructura de producto genérica de**

   * Cada variante debe tener su propio nodo de hoja.
   * La interfaz de producto representa productos y variantes, pero el nodo de repositorio relacionado es específico sobre cuál es.
   * El nodo de producto describe los atributos de producto y los ejes de variante.

#### Ejemplos {#example-1}

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

* El carro de compras es propiedad de `CommerceSession:`

   * El `CommerceSession` realiza operaciones de añadir, quitar, etc.
   * El `CommerceSession` también realiza los distintos cálculos en el carro de compras.
   * El `CommerceSession` también aplica cupones y promociones que se han activado en el carro de compras.

* Aunque no está directamente relacionado con el carro de compras, la variable `CommerceSession` también debe proporcionar información sobre los precios del catálogo (ya que posee precios)

   * Los precios pueden tener varios modificadores:

      * Descuentos por cantidad.
      * Diferentes monedas.
      * Deudor de IVA y exento de IVA.

   * Los modificadores son completamente abiertos con la siguiente interfaz:

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`

**Almacenamiento**

* Almacenamiento

   * AEM En el caso de los carros de compras no genéricos de la se almacenan en la variable [ClientContext](/help/sites-administering/client-context.md)

**Personalización**

* La personalización siempre debe realizarse a través de [ClientContext](/help/sites-administering/client-context.md).
* Un ClientContext `/version/` del carro de compras se crea en todos los casos:

   * Los productos deben añadirse utilizando `CommerceSession.addCartEntry()` método.

* A continuación se muestra un ejemplo de información del carro de compras en el carro de ClientContexts:

![chlimage_1-33](/help/sites-developing/assets/chlimage_1-33a.png)

#### Arquitectura del cierre de compra {#architecture-of-checkout}

**Datos de pedido y carrito**

El `CommerceSession` posee los tres elementos:

1. **Contenido del carro**

   La API corrige el esquema de contenido del carro de compras:

   ```java
       public void addCartEntry(Product product, int quantity);
       public void modifyCartEntry(int entryNumber, int quantity);
       public void deleteCartEntry(int entryNumber);
   ```

1. **Precio**

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

   Sin embargo, los detalles del pedido son *no* corregido por la API:

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**Cálculos de Envío**

* Los formularios de pedido a menudo necesitan presentar varias opciones de envío (y precios).
* Los precios pueden estar basados en artículos y detalles del pedido, como el peso y/o la dirección de entrega.
* El `CommerceSession` tiene acceso a todas las dependencias, por lo que se puede tratar de manera similar a los precios de productos:

   * El `CommerceSession` posee precios de envío.
   * Uso `updateOrder(Map<String, Object> delta)` para recuperar o actualizar los detalles del envío.

### Definición de búsqueda {#search-definition}

Siguiendo el modelo de API de servicio estándar, el proyecto de comercio electrónico proporciona un conjunto de API relacionadas con la búsqueda que pueden implementar los motores de comercio individuales.

>[!NOTE]
>
>Actualmente, solo el motor hybris implementa la API de búsqueda de forma predeterminada.
>
>Sin embargo, la API de búsqueda es genérica y cada CommerceService la puede implementar individualmente.
>
>Por lo tanto, aunque la implementación genérica proporcionada de forma predeterminada no implementa esta API, puede ampliarla y añadir la funcionalidad de búsqueda.

El proyecto de comercio electrónico contiene un componente de búsqueda predeterminado, ubicado en:

`/libs/commerce/components/search`

![chlimage_1-34](/help/sites-developing/assets/chlimage_1-34a.png)

Utiliza la API de búsqueda para consultar el motor de comercio seleccionado (consulte ) [Selección de motor de comercio electrónico](#ecommerce-engine-selection)):

#### API de búsqueda {#search-api}

El proyecto principal proporciona varias clases genéricas/de ayuda:

1. `CommerceQuery`

   Se utiliza para describir una consulta de búsqueda (contiene información sobre el texto de la consulta, la página actual, el tamaño de página, el orden y las facetas seleccionadas). Todos los servicios de comercio electrónico que implementen la API de búsqueda recibirán instancias de esta clase para realizar su búsqueda. A `CommerceQuery` se puede crear una instancia desde un objeto de solicitud ( `HttpServletRequest`).

1. `FacetParamHelper`

   Es una clase de utilidad que proporciona un método estático: `toParams` - que se utiliza para generar `GET` cadenas de parámetros de una lista de facetas y un valor alternado. Esto resulta útil en la interfaz de usuario, donde debe mostrar un hipervínculo para cada valor de cada faceta, de modo que cuando el usuario haga clic en el hipervínculo, se alterne el valor respectivo (es decir, si se seleccionó, se elimine de la consulta; de lo contrario, se agregue). Esto se encarga de toda la lógica de administrar facetas múltiples o de un solo valor, anular valores, etc.

El punto de entrada para la API de búsqueda es `CommerceService#search` método que devuelve un valor `CommerceResult` objeto. Consulte la Documentación de la API para obtener más información sobre este tema.

### Desarrollo de promociones y cupones {#developing-promotions-and-vouchers}

* Cupones:

   * Un cupón es un componente basado en páginas que se crea/edita con la consola Sitios web y se almacena en:

     `/content/campaigns`

   * Suministro de cupones:

      * Un código de cupón (que el comprador debe escribir en el carro de compras).
      * Una etiqueta de cupón (que se mostrará después de que el comprador la haya introducido en el carro de compras).
      * Una ruta de promoción (que define la acción que aplica el cupón).

   * Los cupones no tienen sus propias fechas u horas de activación y desactivación, sino que utilizan las de sus campañas principales.
   * Los motores de comercio externo también pueden proporcionar cupones, que requieren un mínimo de:

      * Un código de cupón
      * Un `isValid()` método

   * El **Cupón** componente ( `/libs/commerce/components/voucher`) proporciona:

      * Un procesador para la administración de cupones; muestra todos los cupones que hay actualmente en el carro de compras.
      * Los cuadros de diálogo de edición (formulario) para administrar (añadir/eliminar) los cupones.
      * Las acciones necesarias para agregar o eliminar cupones en el carro de compras.

* Promociones:

   * Una promoción es un componente basado en páginas que se crea/edita con la consola Sitios web y se almacena en:

     `/content/campaigns`

   * Oferta de promociones:

      * Una prioridad
      * Una ruta del controlador de promoción

   * Puede conectar las promociones a una campaña para definir su fecha/hora de activación/desactivación.
   * Puede conectar las promociones a una experiencia para definir sus segmentos.
   * Las promociones que no estén conectadas a una experiencia no se activarán por sí solas, sino que se podrán activar mediante un cupón.
   * El componente Promoción ( `/libs/commerce/components/promotion`) contiene:

      * procesadores y cuadros de diálogo para la administración de promociones
      * subcomponentes para procesar y editar parámetros de configuración específicos de los controladores de promoción

   * Se proporcionan dos controladores de promoción predeterminados:

      * `DiscountPromotionHandler`, que aplica un descuento absoluto o porcentual a todo el carro de compras
      * `PerfectPartnerPromotionHandler`, que aplica un descuento absoluto o porcentual del producto si el producto del socio también está en el carro de compras

   * El ClientContext `SegmentMgr` resuelve los segmentos y el ClientContext `CartMgr` resuelve las promociones. Se activará cada promoción sujeta al menos a un segmento resuelto.

      * AJAX Las promociones activadas se envían de vuelta al servidor a través de una llamada de para volver a calcular el carro de compras.
      * Las promociones activadas (y los cupones añadidos) también se muestran en el panel ClientContext.

La adición o eliminación de un cupón de un carro de compras se realiza mediante las `CommerceSession` API:

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

Por aquí, el `CommerceSession` es responsable de comprobar si existe un cupón y si se puede aplicar o no. Esto podría aplicarse a los cupones que solo se pueden aplicar si se cumple una determinada condición; por ejemplo, cuando el precio total del carro de compras es mayor de 100 dólares). Si no se puede aplicar un cupón por cualquier motivo, la `addVoucher` El método generará una excepción. Además, la variable `CommerceSession` es responsable de actualizar los precios del carro de compras después de añadir o eliminar un cupón.

El `Voucher` es una clase similar a un bean que contiene campos para:

* Código de cupón
* Breve descripción
* Referencia a la promoción relacionada que indica el tipo y valor de descuento

El `AbstractJcrCommerceSession` siempre que pueda aplicar cupones. Los cupones devueltos por la clase `getVouchers()` son instancias de `cq:Page` que contenga un nodo jcr:content con las siguientes propiedades (entre otras):

* `sling:resourceType` (Cadena): esto debe ser `commerce/components/voucher`

* `jcr:title` (Cadena): para la descripción del cupón
* `code` (Cadena): el código que el usuario debe introducir para aplicar este cupón
* `promotion` (Cadena): la promoción que se va a aplicar; por ejemplo, `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

Los controladores de promociones son servicios OSGi que modifican el carro de compras. El carro de compras admitirá varios enlaces que se definirán en la `PromotionHandler` interfaz.

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

* `DiscountPromotionHandler` aplica un descuento absoluto o porcentual en todo el carro de compras
* `PerfectPartnerPromotionHandler` aplica un descuento absoluto o porcentual del producto si el socio de producto también está en el carro de compras
* `FreeShippingPromotionHandler` se aplica envío gratuito
