---
title: Desarrollo con SAP Commerce Cloud
description: El marco de trabajo de integración de Commerce Cloud de SAP incluye un nivel de integración con una API.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: b3de1a4a-f334-44bd-addc-463433204c99
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '2303'
ht-degree: 0%

---

# Desarrollo con SAP Commerce Cloud {#developing-with-sap-commerce-cloud}

>[!NOTE]
>
>El marco de comercio electrónico se puede utilizar con cualquier solución de comercio electrónico. Algunos detalles específicos y ejemplos mencionados aquí pueden verse en el [hybris](https://www.sap.com/products/crm.html) solución.

El marco de integración incluye una capa de integración con una API. Esto le permite:

* conectar un sistema de comercio electrónico y extraer datos de productos en Adobe Experience Manager AEM ()

* AEM crear componentes de para las capacidades de comercio independientemente del motor específico de comercio electrónico

![chlimage_1-11](/help/sites-developing/assets/chlimage_1-11a.png)

>[!NOTE]
>
>[Documentación de API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) también está disponible.

AEM Se proporcionan varios componentes listos para usar para usar de la capa de integración de. Actualmente son:

* un componente de visualización del producto
* un carro de compras
* check-out

AEM Para la búsqueda, se proporciona un gancho de integración que le permite utilizar la búsqueda de la, la búsqueda del sistema de comercio electrónico, una búsqueda de terceros o una combinación de estos.

## Selección de motor de comercio electrónico {#ecommerce-engine-selection}

AEM El marco de comercio electrónico se puede utilizar con cualquier solución de comercio electrónico, el motor que se utilice debe ser identificable por los siguientes puntos:

* Los motores de comercio electrónico son servicios OSGi que admiten el `CommerceService` interfaz

   * Los motores se pueden distinguir mediante una `commerceProvider` propiedad de servicio

* AEM soportes de la `Resource.adaptTo()` para `CommerceService` y `Product`

   * El `adaptTo` la implementación busca un `cq:commerceProvider` en la jerarquía del recurso:

      * Si se encuentra, el valor se utiliza para filtrar la búsqueda del servicio de comercio.

      * Si no se encuentra, se utiliza el servicio de comercio de mayor clasificación.

   * A `cq:Commerce` mixin se usa para que el `cq:commerceProvider` se puede agregar a recursos con establecimiento inflexible de tipos.

* El `cq:commerceProvider` también se utiliza para hacer referencia a la definición de commerce factory adecuada.

   * Por ejemplo, una `cq:commerceProvider` propiedad con el valor `hybris` se correlaciona con la configuración OSGi para **Day CQ Commerce Factory for Hybris** (com.adobe.cq.commerce.hybris.impl.HybrisServiceFactory): donde el parámetro `commerceProvider` también tiene el valor `hybris`.

   * Aquí encontrará más propiedades, como **Versión de catálogo** se puede configurar (cuando corresponda y esté disponible).

Consulte los siguientes ejemplos:

| `cq:commerceProvider = geometrixx` | AEM en una instalación estándar se requiere una implementación específica. Por ejemplo, el ejemplo de Geometrixx, que incluye extensiones mínimas a la API genérica |
|--- |--- |
| `cq:commerceProvider = hybris` | implementación de hybris |

### Ejemplos {#example}

```shell
/content/store
+ cq:commerceProvider = hybris
  + mens
    + polo-shirt-1
    + polo-shirt-2
    + employee
+ cq:commerceProvider = jcr
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
>Con CRXDE Lite, puede ver cómo se gestiona esto en el componente de producto para la implementación de hybris:
>
>`/apps/geometrixx-outdoors/components/hybris/product/product.jsp`

### Desarrollo para hybris 4 {#developing-for-hybris}

La extensión hybris del marco de integración de comercio electrónico se ha actualizado para admitir Hybris 5, manteniendo al mismo tiempo la compatibilidad con versiones anteriores con Hybris 4.

La configuración predeterminada del código está ajustada para Hybris 5.

Para desarrollar Hybris 4, se requiere lo siguiente:

* Al invocar Maven, agregue el siguiente argumento de la línea de comandos al comando

  `-P hybris4`

  Descarga la distribución preconfigurada de Hybris 4 y la incrusta en el paquete `cq-commerce-hybris-server`.

* En el administrador de configuración de OSGi:

   * Deshabilite la compatibilidad con Hybris 5 para el servicio Analizador de respuestas predeterminado.

   * Asegúrese de que el servicio Controlador de autenticación básica de Hybris tenga una clasificación de servicio inferior a la del servicio Controlador de autenticación de Hybris.

### Gestión de sesión {#session-handling}

hybris utiliza una sesión de usuario para almacenar información como el carro de compras del cliente. El ID de sesión se devuelve de hybris en un `JSESSIONID` cookie que debe enviarse en solicitudes posteriores a hybris. Para evitar almacenar el ID de sesión en el repositorio, se codifica en otra cookie que se almacena en el explorador del comprador. Se realizan los siguientes pasos:

* En la primera solicitud, no se establece ninguna cookie en la solicitud del comprador; por lo que se envía una solicitud a la instancia de hybris para crear una sesión.

* Las cookies de sesión se extraen de la respuesta y se codifican en una nueva cookie (por ejemplo, `hybris-session-rest`) y se establece en la respuesta al comprador. La codificación de una nueva cookie es obligatoria, ya que la cookie original solo es válida para una ruta determinada y, de lo contrario, no se devolverá desde el explorador en solicitudes posteriores. La información de la ruta debe añadirse al valor de la cookie.

* En solicitudes posteriores, las cookies se descodifican del `hybris-session-<*xxx*>` y se establecen en el cliente HTTP que se utiliza para solicitar datos de hybris.

>[!NOTE]
>
>Se crea una nueva sesión anónima cuando la sesión original ya no es válida.

#### CommerceSession {#commercesession}

* Esta sesión es &quot;propietaria&quot; de **carro de compras**

   * realiza operaciones add/remove/etc.

   * realiza los distintos cálculos en el carro de compras;

     `commerceSession.getProductPrice(Product product)`

* Posee el *ubicación de almacenamiento* para el **pedido** datos

  `CommerceSession.getUserContext()`

* Posee el **pago** conexión de procesamiento

* Posee el **cumplimiento** conexión

### Sincronización y publicación de productos {#product-synchronization-and-publishing}

AEM Los datos del producto que se mantienen en hybris deben estar disponibles en la práctica de la. Se ha implementado el siguiente mecanismo:

* hybris proporciona una carga inicial de ID como fuente. Puede haber actualizaciones en esta fuente.
* AEM hybris proporciona información actualizada a través de una fuente (que se utiliza para sondear las encuestas de la que se dispone en el caso de los).
* AEM Cuando está utilizando datos de productos de, envía solicitudes de vuelta a hybris para los datos actuales (solicitud de obtención condicional con fecha de última modificación).
* En Hybris, es posible especificar el contenido de las fuentes de forma declarativa.
* AEM AEM La asignación de la estructura de fuente al modelo de contenido de la se produce en el adaptador de fuente del lado del.

![chlimage_1-12](/help/sites-developing/assets/chlimage_1-12a.png)

* AEM El importador (b) se utiliza para la configuración inicial de la estructura del árbol de páginas en los catálogos de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de destino de los catálogos.
* AEM AEM Los cambios de catálogo en los híbridos se indican para que se puedan aplicar a través de una fuente, que luego se propagan a la (b).

   * Producto añadido/eliminado/modificado con respecto a la versión del catálogo.

   * Producto aprobado.

* AEM La extensión hybris proporciona un importador de encuestas (&quot;esquema hybris&quot;), que se puede configurar para importar cambios en un intervalo especificado (por ejemplo, cada 24 horas en las que el intervalo se especifica en segundos):

  ```JavaScript
      http://localhost:4502/content/geometrixx-outdoors/en_US/jcr:content.json
       {
       * "jcr:mixinTypes": ["cq:PollConfig"],
       * "enabled": true,
       * "source": "hybris:outdoors",
       * "jcr:primaryType": "cq:PageContent",
       * "interval": 86400
       }
  ```

* AEM La configuración del catálogo en reconoce de manera **Ensayado** y **En línea** versiones de catálogo.

* AEM La sincronización de productos entre versiones de catálogo requiere la activación o desactivación de la página de la página de la versión correspondiente (a, c).

   * Adición de un producto a un **En línea** la versión del catálogo requiere la activación de la página del producto.

   * La eliminación de un producto requiere la desactivación.

* AEM La activación de una página en el apartado (c) requiere una comprobación (b) y solo es posible si

   * El producto se encuentra en un **En línea** versión del catálogo para páginas de productos.

   * Los productos a los que se hace referencia están disponibles en una **En línea** versión del catálogo para otras páginas (por ejemplo, páginas de campaña).

* Las páginas de productos activadas deben acceder a los datos del producto **En línea** versión (d).

* AEM La instancia Publicación de la requiere acceso a hybris para la recuperación de datos personalizados y del producto (d).

### Arquitectura {#architecture}

#### Arquitectura de producto y variantes {#architecture-of-product-and-variants}

Un solo producto puede tener varias variaciones; por ejemplo, puede variar según el color y/o el tamaño. Un producto debe definir qué propiedades impulsan la variación; términos de Adobe estos *ejes de variante*.

Sin embargo, no todas las propiedades son ejes de variante. Las variaciones también pueden afectar a otras propiedades; por ejemplo, el precio puede depender del tamaño. Estas propiedades no pueden ser seleccionadas por el comprador y, por lo tanto, no se consideran ejes de variante.

Cada producto o variante está representado por un recurso y, por lo tanto, se asigna 1:1 a un nodo de repositorio. Es un corolario que un producto específico o una variante se puedan identificar de forma exclusiva por su ruta.

El recurso de producto/variante no siempre contiene los datos de producto reales. Podría ser una representación de datos almacenados en otro sistema (como hybris). AEM Por ejemplo, las descripciones de los productos y los precios no se almacenan en el sistema de comercio electrónico, sino que se recuperan en tiempo real del motor de comercio electrónico.

Cualquier recurso de producto puede representarse mediante una `Product API`. La mayoría de las llamadas de la API de producto son específicas de la variación (aunque las variaciones pueden heredar valores compartidos de un antecesor), pero también hay llamadas que enumeran el conjunto de variaciones ( `getVariantAxes()`, `getVariants()`, etc.).

>[!NOTE]
>
>De hecho, los ejes de variante están determinados por lo que sea `Product.getVariantAxes()` devuelve:
>* hybris lo define para la implementación de hybris
>
>Aunque los productos (en general) pueden tener muchos ejes de variante, el componente de producto listo para usar solo gestiona dos:
>
>1. `size`
>
>1. más uno más
>
>Esta variante adicional se selecciona mediante la variable `variationAxis` propiedad de la referencia del producto (normalmente `color` para Geometrixx Outdoors).

#### Referencias y datos del producto {#product-references-and-product-data}

En general, los datos del producto se encuentran en `/etc`, y referencias de producto en `/content`.

Debe haber una asignación individual entre las variaciones de productos y los nodos de datos de productos.

Las referencias de producto también deben tener un nodo para cada variación presentada, pero no es necesario presentar todas las variaciones. Por ejemplo, si un producto tiene variaciones de S, M y L, los datos del producto podrían ser:

```shell
etc
|──commerce
|  |──products
|     |──shirt
|       |──shirt-s
|       |──shirt-m
|       |──shirt-l
```

Mientras que un catálogo &quot;Grande y Alto&quot; podría tener solo:

```shell
content
|──big-and-tall
|  |──shirt
|     |──shirt-l
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

   * Los nodos de producto son `nt:unstructured`.

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

   * El `CommerceSession` realiza operaciones de agregar o quitar, etc.
   * El `CommerceSession` también realiza los distintos cálculos en el carro de compras. &quot;

* Aunque no está directamente relacionado con el carro de compras, la variable `CommerceSession` también debe proporcionar información sobre los precios del catálogo (ya que posee precios)

   * Los precios pueden tener varios modificadores:

      * Descuentos por cantidad.
      * Diferentes monedas.
      * Deudor de IVA y exento de IVA.

   * Los modificadores están abiertos con la siguiente interfaz:

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`

**Almacenamiento**

* Almacenamiento

   * En el caso de hybris, el servidor de hybris es propietario del carro de compras.
   * AEM En el caso de los carros de compras no genéricos, los carros de compras se almacenan en el [ClientContext](/help/sites-administering/client-context.md).

**Personalización**

* Impulse siempre la personalización a través de [ClientContext](/help/sites-administering/client-context.md).
* Un ClientContext `/version/` del carro de compras se crea en todos los casos:

   * Los productos deben añadirse utilizando `CommerceSession.addCartEntry()` método.

* A continuación se muestra un ejemplo de información del carro de compras en el carro de ClientContexts:

![chlimage_1-13](/help/sites-developing/assets/chlimage_1-13a.png)

#### Arquitectura del cierre de compra {#architecture-of-checkout}

**Datos de pedido y carrito**

El `CommerceSession` posee los tres elementos:

1. Contenido del carro
1. Precio
1. Los detalles del pedido

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

* Los formularios de pedido suelen presentar varias opciones de envío (y precios).
* Los precios pueden estar basados en artículos y detalles del pedido, como el peso y/o la dirección de entrega.
* El `CommerceSession` tiene acceso a todas las dependencias, por lo que se puede tratar de manera similar a los precios de productos:

   * El `CommerceSession` posee precios de envío.
   * Puede recuperar o actualizar los detalles de envío utilizando `updateOrder(Map<String, Object> delta)`

>[!NOTE]
>
>Se puede implementar un selector de envío; por ejemplo:
>
>`yourProject/commerce/components/shippingpicker`:
>
>* Básicamente, podría ser una copia de `foundation/components/form/radio`, pero con llamadas de retorno a `CommerceSession` para:
>
>* Comprobación de si el método está disponible
>* Adición de información de precios
>* AEM Para permitir que los compradores actualicen la página de pedidos en el mercado (incluido el superconjunto de métodos de envío y el texto que los describe), sin dejar de tener el control para exponer los datos relevantes `CommerceSession` información.

**Procesamiento de pagos**

* El `CommerceSession` también posee la conexión de procesamiento de pagos.

* Los implementadores deben añadir llamadas específicas (al servicio de procesamiento de pagos que hayan elegido) al `CommerceSession` implementación.

**Satisfacción de pedidos**

* El `CommerceSession` también es propietario de la conexión de cumplimiento.
* Los implementadores deben añadir llamadas específicas (al servicio de procesamiento de pagos que hayan elegido) al `CommerceSession` implementación.

### Definición de búsqueda {#search-definition}

Siguiendo el modelo de API de servicio estándar, el proyecto de comercio electrónico proporciona un conjunto de API relacionadas con la búsqueda que pueden implementar los motores de comercio individuales.

>[!NOTE]
>
>Actualmente, solo el motor hybris implementa la API de búsqueda de forma predeterminada.
>
>Sin embargo, la API de búsqueda es genérica y cada CommerceService la puede implementar individualmente.

El proyecto de comercio electrónico contiene un componente de búsqueda predeterminado en:

`/libs/commerce/components/search`

![chlimage_1-14](/help/sites-developing/assets/chlimage_1-14a.png)

Utiliza la API de búsqueda para consultar el motor de comercio seleccionado (consulte [Selección de motor de comercio electrónico](#ecommerce-engine-selection)):

#### API de búsqueda {#search-api}

El proyecto principal proporciona varias clases genéricas/de ayuda:

1. `CommerceQuery`

   Describe una consulta de búsqueda (contiene información sobre el texto de la consulta, la página actual, el tamaño de página, el orden y las facetas seleccionadas). Todos los servicios de comercio electrónico que implementan la API de búsqueda reciben instancias de esta clase para realizar su búsqueda. A `CommerceQuery` se puede crear una instancia desde un objeto de solicitud ( `HttpServletRequest`).

1. `FacetParamHelper`

   Es una clase de utilidad que proporciona un método estático: `toParams` - que se utiliza para generar `GET` cadenas de parámetros de una lista de facetas y un valor alternado. Esto resulta útil en la interfaz de usuario, donde debe mostrar un hipervínculo para cada valor de cada faceta, de modo que cuando el usuario haga clic en el hipervínculo, se alterne el valor respectivo. Es decir, si se seleccionó, se elimina de la consulta; de lo contrario, se agrega. Esto se encarga de toda la lógica de administrar facetas múltiples o de un solo valor, anular valores, etc.

El punto de entrada para la API de búsqueda es `CommerceService#search` método que devuelve un valor `CommerceResult` objeto. Consulte la [Documentación de API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) para obtener más información sobre este tema.

### Integración de usuarios {#user-integration}

AEM La integración se proporciona entre los sistemas de comercio electrónico de los distintos sistemas de comercio electrónico y de los que se puede acceder. AEM AEM Esto requiere una estrategia para sincronizar a los compradores entre los distintos sistemas, de modo que el código específico de los clientes solo tenga que saber sobre los puntos de venta y, a la inversa, solo tenga que saber sobre los puntos de venta:

* Autenticación

  AEM Se presume que el es el... *solamente* front-end web y, por lo tanto, funciona *todo* autenticación.

* Cuentas en Hybris

  AEM crea una cuenta correspondiente (subordinada) en hybris para cada comprador. AEM El nombre de usuario de esta cuenta es el mismo que el nombre de usuario de la. AEM Una contraseña criptográficamente aleatoria se genera automáticamente y se almacena (codifica) en el código de acceso de los usuarios de la red de servicios de Internet ().

#### Usuarios preexistentes {#pre-existing-users}

AEM Un front-end se puede colocar delante de una implementación de hybris existente. AEM Además, se puede añadir un motor hybris a una instalación existente de la. Para ello, los sistemas deben poder gestionar correctamente los usuarios existentes en cualquiera de ellos:

* AEM > hybris

   * AEM Al iniciar sesión en hybris, si no existe el usuario de la:

      * crear un usuario de hybris con una contraseña criptográficamente aleatoria
      * AEM almacene el nombre de usuario de hybris en el directorio de usuario del usuario de la

   * Consulte: `com.adobe.cq.commerce.hybris.impl.HybrisSessionImpl#login()`

* AEM hybris >

   * AEM Al iniciar sesión en, si el sistema reconoce al usuario, haga lo siguiente:

      * intente iniciar sesión en hybris con el nombre de usuario/pwd proporcionado
      * AEM AEM AEM si se ejecuta correctamente, cree el usuario en la cuenta de usuario con la misma contraseña (los resultados de sal específicos de la en el hash específico de la cuenta de usuario).

   * El algoritmo anterior se implementa en un Sling `AuthenticationInfoPostProcessor`

      * Consulte: `com.adobe.cq.commerce.hybris.impl.user.LazyUserImporter.java`

### Personalización del proceso de importación {#customizing-the-import-process}

Para crear a partir de la funcionalidad existente su controlador de importación personalizado:

* tiene que implementar el `ImportHandler` interfaz

* puede ampliar el `DefaultImportHandler`.

```java
/**
 * Services implementing the <code>ImportHandler</code> interface are
 * called by the {@link HybrisImporter} to create actual commerce entities
 * such as products.
 */
public interface ImportHandler {

  /**
  * Not used.
  */
  public void createTaxonomie(ImporterContext ctx);

  /**
  * Creates a catalog with the given name.
  * @param ctx   The importer context
  * @param name  The catalog's name
  * @return Path of created catalog
  */
  public String createCatalog(ImporterContext ctx, String name) throws Exception;

  /**
  * Creates a product from the given values.
  * @param ctx                The importer context
  * @param values             The product's properties
  * @param parentCategoryPath The containing category's path
  * @return Path of created product
  */
  public String createProduct(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;

  /**
  * Creates a variant product from the given values.
  * @param ctx             The importer context
  * @param values          The product's properties
  * @param baseProductPath The base product's path
  * @return Path of created product
  */
  public String createVariantProduct(ImporterContext ctx, ValueMap values, String baseProductPath) throws Exception;

  /**
  * Creates an asset for a product. This is usually a product
  * image.
  * @param ctx             The importer context
  * @param values          The product's properties
  * @param baseProductPath The product's path
  * @return Path of created asset
  */
  public String createAsset(ImporterContext ctx, ValueMap values, String productPath) throws Exception;

  /**
  * Creates a category from the given values.
  * @param ctx           The importer context
  * @param values        The category's properties
  * @param parentPath    Path of parent category or base path of import if there is a root category
  * @return Path of created category
  */
  public String createCategory(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;
}
```

Para que el importador reconozca el controlador personalizado, debe especificar el `service.ranking`con un valor superior a 0, por ejemplo.

```java
@Component
@Service
@Property(name = "service.ranking", value = 100)
public class MyImportHandler extends DefaultImportHandler
{
...
}
```
