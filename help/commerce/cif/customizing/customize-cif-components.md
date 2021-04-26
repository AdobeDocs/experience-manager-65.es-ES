---
title: Personalice los componentes principales de CIF
description: Aprenda a personalizar AEM componentes principales del CIF. El tutorial explica cómo ampliar de forma segura un componente principal del CIF para satisfacer los requisitos específicos de la empresa. Obtenga información sobre cómo ampliar una consulta de GraphQL para devolver un atributo personalizado y mostrar el nuevo atributo en un componente principal del CIF.
sub-product: Comercio
topics: Development
version: cloud-service
doc-type: tutorial
activity: develop
audience: developer
feature: Marco de integración de Commerce
kt: 4279
thumbnail: customize-aem-cif-core-component.jpg
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '2549'
ht-degree: 29%

---

# Personalización de los componentes principales del CIF de AEM {#customize-cif-components}

El [proyecto Venia del CIF](https://github.com/adobe/aem-cif-guides-venia) es una base de código de referencia para el uso de [componentes principales del CIF](https://github.com/adobe/aem-core-cif-components). En este tutorial, ampliará aún más el componente [teaser de productos](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) para mostrar un atributo personalizado del Magento. También obtendrá más información sobre la integración de GraphQL entre AEM y Magento y los enlaces de extensión proporcionados por los componentes principales del CIF.

>[!TIP]
>
> Utilice el [AEM tipo de archivo del proyecto](https://github.com/adobe/aem-project-archetype) al iniciar su propia implementación de comercio.

## Qué va a generar

La marca Venia comenzó recientemente a fabricar algunos productos utilizando materiales sostenibles y la empresa desea mostrar un distintivo **Eco Friendly** como parte del teaser de productos. Se creará un nuevo atributo personalizado en Magento para indicar si un producto utiliza el material **Eco friendly**. Este atributo personalizado se agregará como parte de la consulta de GraphQL y se mostrará en el teaser de productos de los productos especificados.

![Implementación Final De Distintivo Compatible Con Eco](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Requisitos previos {#prerequisites}

Se requiere un entorno de desarrollo local para completar este tutorial. Esto incluye una instancia de AEM en ejecución configurada y conectada a una instancia de Magento. Revise los requisitos y pasos para [configurar un desarrollo local con AEM](../develop.md). Para seguir el tutorial por completo, necesitará permisos para agregar [Atributos a un Producto](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) en el Magento.

También necesitará el IDE de GraphQL como [GraphiQL](https://github.com/graphql/graphiql) o una extensión del explorador para ejecutar los ejemplos de código y tutoriales. Si instala una extensión del explorador, asegúrese de que tenga la capacidad de establecer encabezados de solicitud. En Google Chrome, [Altair GraphQL Client](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja) es una extensión que puede hacer el trabajo.

## Clonar el proyecto Venia {#clone-venia-project}

Clonaremos el [Proyecto Venia](https://github.com/adobe/aem-cif-guides-venia) y luego anularemos los estilos predeterminados.

>[!NOTE]
>
> **Siéntase libre de usar un proyecto existente**  (basado en el tipo de archivo del proyecto AEM con CIF incluido) y omita esta sección.

1. Ejecute el siguiente comando git para clonar el proyecto:

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. Cree e implemente el proyecto en una instancia local de AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. Añada las configuraciones de OSGi necesarias para conectar la instancia de AEM a una instancia de Magento o añadir las configuraciones al proyecto recién creado.

1. En este punto, debería tener una versión de trabajo de una tienda conectada a una instancia de Magento. Vaya a la página `US` > `Home` en: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   Hay que ver que la tienda esté usando actualmente el tema de Venia. Al expandir el menú principal de la tienda, verá varias categorías que indican que la conexión con Magento está funcionando.

   ![Tienda configurada con tema de Venia](../assets/customize-cif-components/venia-store-configured.png)

## Creación del teaser de productos {#author-product-teaser}

El componente teaser de productos se ampliará a lo largo de este tutorial. Como primer paso, agregue una nueva instancia del teaser de productos a la página principal para comprender la funcionalidad de línea de base.

1. Vaya hasta la **Página de inicio** del sitio: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. Inserte un nuevo componente **teaser de productos** en el contenedor del diseño principal de la página.

   ![Inserción del teaser de productos](../assets/customize-cif-components/product-teaser-add-component.png)

3. Expanda el panel lateral (si no está activado) y cambie desde menú desplegable del buscador de recursos a **Productos**. Esto debería mostrar una lista de los productos disponibles de una instancia conectada a Magento. Seleccione un producto y **arrástrelo y suéltelo** en el componente **teaser de productos** de la página.

   ![Arrastrar y soltar teaser de productos](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   > Tenga en cuenta que también puede configurar el producto mostrado configurando el componente con el cuadro de diálogo (haga clic en el icono de _llave inglesa_).

4. Ahora debería ver un producto que muestra el teaser de productos. Se muestran el nombre y el precio del producto ya que son atributos predeterminados.

   ![Teaser de productos: estilo predeterminado](../assets/customize-cif-components/product-teaser-default-style.png)

## Agregar un atributo personalizado en el Magento {#add-custom-attribute}

Los productos y los datos de producto mostrados en AEM se almacenan en el Magento . A continuación, añada un nuevo atributo para **Eco Friendly** como parte del atributo de producto definido mediante la interfaz de usuario del Magento.

>[!TIP]
>
> ¿Ya tiene un atributo personalizado **Yes/No** como parte de su conjunto de atributos del producto? Siéntase libre de usarlo y omita esta sección.

1. Inicie sesión en la instancia de Magento.
1. Vaya a **Catálogo** > **Productos**.
1. Actualice el filtro de búsqueda para encontrar el **Producto configurable** utilizado cuando se agregó al componente teaser en el ejercicio anterior. Abra el producto en modo de edición.

   ![Buscar el producto Valeria](../assets/customize-cif-components/search-valeria-product.png)

1. En la vista del producto, haga clic en **Agregar atributo** > **Crear nuevo atributo**.
1. Rellene el formulario **Nuevo atributo** con los siguientes valores (deje la configuración predeterminada para otros valores)

   | Conjunto de campos | Etiqueta de campo | Value |
   | ----------------------------- | ------------------ | ---------------- |
   | Propiedades de atributo | Etiqueta de atributo | **Compatible con el ecosistema** |
   | Propiedades de atributo | Tipo de entrada de catálogo | **Sí/No** |
   | Propiedades de atributos avanzadas | Código de atributo | **eco_friendly** |

   ![Nuevo formulario de atributos](../assets/customize-cif-components/attribute-new-form.png)

   Haga clic en **Guardar atributo** cuando termine.

1. Desplácese hasta la parte inferior del producto y amplíe el encabezado **Atributos**. Debería ver el nuevo campo **Eco Friendly**. Cambie el conmutador a **Yes**.

   ![Cambiar alternancia a sí](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **** Guarde los cambios en el producto.

   >[!TIP]
   >
   > Puede encontrar más información sobre la administración de [Atributos de producto en la guía del usuario del Magento](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html).

1. Vaya a **System** > **Tools** > **Cache Management**. Dado que se ha realizado una actualización en el esquema de datos, es necesario invalidar algunos de los tipos de caché en el Magento.
1. Marque la casilla junto a **Configuration** y envíe el tipo de caché para **Refresh**

   ![Actualizar tipo de caché de configuración](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   > Puede encontrar más información sobre [Cache Management en la guía del usuario del Magento](https://docs.magento.com/user-guide/system/cache-management.html).

## Usar un IDE de GraphQL para verificar el atributo {#use-graphql-ide}

Antes de saltar a AEM código, es útil explorar el [Magento GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) mediante un IDE de GraphQL. La integración del Magento con AEM se realiza principalmente mediante una serie de consultas de GraphQL. Comprender y modificar las consultas de GraphQL es una de las formas clave de ampliar los componentes principales del CIF.

A continuación, utilice un IDE de GraphQL para verificar que el atributo `eco_friendly` se ha agregado al conjunto de atributos del producto. Las capturas de pantalla de este tutorial utilizan [Altair GraphQL Client](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja).

1. Abra el IDE de GraphQL e introduzca la URL `http://<magento-server>/graphql` en la barra URL de su IDE o extensión.
2. Añada la siguiente [consulta de productos](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) donde `YOUR_SKU` es el **SKU** del producto utilizado en el ejercicio anterior:

   ```json
     {
       products(
       filter: { sku: { eq: "YOUR_SKU" } }
       ) {
           items {
           name
           sku
           eco_friendly
           }
       }
   }
   ```

3. Ejecute la consulta y debe obtener una respuesta como la siguiente:

   ```json
   {
     "data": {
       "products": {
         "items": [
           {
             "name": "Valeria Two-Layer Tank",
             "sku": "VT11",
             "eco_friendly": 1
           }
         ]
       }
     }
   }
   ```

   ![Ejemplo de respuesta de GraphQL](../assets/customize-cif-components/sample-graphql-query.png)

   Tenga en cuenta que el valor de **Yes** es un número entero de **1**. Esto resulta útil cuando escribimos la consulta GraphQL en Java.

   >[!TIP]
   >
   > Puede encontrar documentación más detallada sobre [Magento GraphQL aquí](https://devdocs.magento.com/guides/v2.4/graphql/index.html).

## Actualizar el modelo de Sling para el teaser de productos {#updating-sling-model-product-teaser}

A continuación, ampliaremos la lógica empresarial del teaser de productos implementando el modelo Sling. [Los modelos de Sling](https://sling.apache.org/documentation/bundles/models.html) son objetos Java antiguos comunes (&quot;POJO&quot;), impulsados por anotaciones que implementan cualquier lógica comercial necesaria para el componente. Los modelos Sling se utilizan junto con las secuencias de comandos HTL como parte del componente. Seguiremos el patrón de [delegación de modelos Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) para que podamos extender las partes del modelo de teaser de productos existente.

Los modelos Sling se implementan como Java y se pueden encontrar en el módulo **principal** del proyecto generado.

Utilice [el IDE de su elección](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) para importar el proyecto de Venia. Las capturas de pantalla utilizadas son de [Visual Studio Code IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code).

1. En su IDE, navegue bajo el módulo **core** para: `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`.

   ![IDE de ubicación principal](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` es una interfaz de Java que amplía la interfaz  [](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) ProductTeaserinterface del CIF.

   Ya se ha agregado un nuevo método denominado `isShowBadge()` para mostrar un distintivo si el producto se considera &quot;Nuevo&quot;.

1. Añada un nuevo método `isEcoFriendly()` en la interfaz:

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   Este es un nuevo método que introduciremos para encapsular la lógica para indicar si el producto tiene el atributo `eco_friendly` establecido en **Yes** o **No**.

1. A continuación, revise `MyProductTeaserImpl.java` en `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`.

   El patrón de delegación [para modelos Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) permite que `MyProductTeaserImpl` haga referencia al modelo `ProductTeaser` a través de la propiedad `sling:resourceSuperType`:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   Para todos los métodos que no queremos anular o cambiar, simplemente podemos devolver el valor que devuelve el `ProductTeaser`. Por ejemplo:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   Esto minimiza la cantidad de código Java que debe escribir una implementación.

1. Uno de los puntos de extensión adicionales que proporcionan AEM componentes principales del CIF es el `AbstractProductRetriever` que proporciona acceso a atributos de producto específicos. Inspect utiliza el método `initModel()` :

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to intialize the proudctRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
           if (productRetriever != null) {
               productRetriever.extendProductQueryWith(p -> p.createdAt());
           }
   
       }
   ...
   ```

   La anotación `@PostConstruct` garantiza que se llame a este método en cuanto se inicialice el modelo Sling.

   Observe que la consulta de producto GraphQL ya se ha ampliado con el método `extendProductQueryWith` para recuperar el atributo `created_at` adicional. Este atributo se utiliza posteriormente como parte del método `isShowBadge()`.

1. Actualice la consulta de GraphQL para incluir el atributo `eco_friendly` en la consulta parcial:

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p ->
                productRetriever.extendProductQueryWith(p -> p
                   .createdAt()
                   .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
               );
           );
       }
   }
   ```

   Añadir al método `extendProductQueryWith` es una manera eficaz de garantizar que el resto del modelo disponga de atributos de productos adicionales. También minimiza el número de consultas ejecutadas.

   En el código anterior, se utiliza el`addCustomSimpleField` para recuperar el atributo `eco_friendly`. Esto ilustra cómo se puede realizar la consulta de cualquier atributo personalizado que forme parte del esquema del Magento.

   >[!NOTE]
   >
   > El método `createdAt()` se ha implementado como parte de la [Interfaz de producto](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java). Se han implementado la mayoría de los atributos de esquema encontrados con frecuencia, por lo que solo debe utilizarse `addCustomSimpleField` para atributos verdaderamente personalizados.

1. Agregue un registrador para ayudar a depurar el código Java:

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. A continuación, implemente el método `isEcoFriendly()`:

   ```java
   @Override
   public Boolean isEcoFriendly() {
   
       Integer ecoFriendlyValue;
       try {
           ecoFriendlyValue = productRetriever.fetchProduct().getAsInteger(ECO_FRIENDLY_ATTRIBUTE);
           if(ecoFriendlyValue != null && ecoFriendlyValue.equals(Integer.valueOf(1))) {
               LOGGER.info("*** Product is Eco Friendly**");
               return true;
           }
       } catch (SchemaViolationError e) {
           LOGGER.error("Error retrieving eco friendly attribute");
       }
       LOGGER.info("*** Product is not Eco Friendly**");
       return false;
   }
   ```

   En el método anterior, se utiliza `productRetriever` para recuperar el producto y el método `getAsInteger()` se utiliza para obtener el valor del atributo `eco_friendly`. Basándonos en las consultas de GraphQL que ejecutamos anteriormente sabemos que el valor esperado cuando el atributo `eco_friendly` se establece en &quot;**Yes**&quot; es en realidad un número entero de **1**.

   Ahora que se ha actualizado el modelo Sling, es necesario actualizar el marcado del componente para que muestre un indicador **Eco Friendly** basado en el modelo Sling.

## Personalización del marcado del teaser de productos {#customize-markup-product-teaser}

Una extensión común de los componentes de AEM es modificar el marcado que genera el componente. Esto se realiza anulando la [secuencia de comandos HTL](https://docs.adobe.com/content/help/es-ES/experience-manager-htl/using/overview.html) que utiliza el componente para representar su marcado. La plantilla de idioma HTML (HTL) es un idioma de plantilla ligero que los componentes de AEM utilizan para representar dinámicamente el marcado basado en contenido creado, lo que permite la reutilización de los componentes. El teaser de productos, por ejemplo, se puede reutilizar una y otra vez para mostrar diferentes productos.

En nuestro caso, queremos renderizar un banner sobre el teaser para indicar que el producto es &quot;compatible con el medio ambiente&quot; basado en un atributo personalizado. El patrón de diseño para [personalizar el marcado](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) de un componente es en realidad estándar para todos los componentes AEM, no solo para los componentes principales del CIF de AEM.

1. En el IDE, navegue y expanda el módulo `ui.apps` y expanda la jerarquía de carpetas a: `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` e inspeccione el archivo `.content.xml`.

   ![Product Teaser ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   Arriba se encuentra la definición del componente para el componente teaser de productos en nuestro proyecto. Observe la propiedad `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Este es un ejemplo de creación de un [componente Proxy](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/get-started/using.html#create-proxy-components). En lugar de copiar y pegar todas las secuencias de comandos HTL del teaser de productos de los componentes principales del CIF de AEM, podemos usar `sling:resourceSuperType` para heredar todas las funcionalidades.

1. Abra el archivo `productteaser.html`. Esta es una copia del archivo `productteaser.html` desde el [teaser de productos CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)

   ```html
   <!--/* productteaser.html */-->
   <sly
     data-sly-use.product="com.venia.core.models.commerce.MyProductTeaser"
     data-sly-use.templates="core/wcm/components/commons/v1/templates.html"
     data-sly-use.actionsTpl="actions.html"
     data-sly-test.isConfigured="${properties.selection}"
     data-sly-test.hasProduct="${product.url}"
   ></sly>
   ```

   Observe que se utiliza el modelo de Sling para `MyProductTeaser` y se asigna a la variable `product`.

1. Modifique `productteaser.html` para realizar una llamada al método `isEcoFriendly` implementado en el ejercicio anterior:

   ```html
   ...
   <div
     data-sly-test="${isConfigured && hasProduct}"
     class="item__root"
     data-cmp-is="productteaser"
     data-virtual="${product.virtualProduct}"
   >
     <div data-sly-test="${product.showBadge}" class="item__badge">
       <span>${properties.text || 'New'}</span>
     </div>
     <!--/* Insert call to Eco Friendly here */-->
     <div data-sly-test="${product.ecoFriendly}" class="item__eco">
       <span>Eco Friendly</span>
     </div>
     ...
   </div>
   ```

   Al llamar a un método del modelo de Sling en HTL, se suelta la porción `get` y `is` del método y se escribe la primera letra en minúsculas. Por lo tanto, `isShowBadge()` se convierte en `.showBadge` y `isEcoFriendly` en `.ecoFriendly`. En función del valor booleano devuelto por `.isEcoFriendly()` determina si se muestra `<span>Eco Friendly</span>`.

   Puede encontrar más información sobre `data-sly-test` y otras [instrucciones de bloque HTL aquí](https://docs.adobe.com/content/help/en/experience-manager-htl/using/htl/block-statements.html#test).

1. Guarde los cambios e implemente las actualizaciones en AEM con sus habilidades con Maven, desde un terminal de línea de comandos:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. Abra una nueva ventana del explorador y vaya a AEM y a la **consola OSGi** > **Estado** > **Modelos Sling**: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. Busque `MyProductTeaserImpl` y debería ver una línea como la siguiente:

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   Esto indica que el modelo Sling se ha implementado correctamente y se ha asignado al componente correcto.

1. Actualice a la **Página principal de Venia** en [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) donde se ha agregado el teaser de productos.

   ![Se muestra un mensaje ecológico](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   Si el producto tiene el atributo `eco_friendly` establecido en **Yes**, debería ver el texto &quot;Eco Friendly&quot; en la página. Intente cambiar a diferentes productos para ver el cambio de comportamiento.

1. A continuación, abra el AEM `error.log` para ver las instrucciones de registro que agregamos. El `error.log` se encuentra en `<AEM SDK Install Location>/crx-quickstart/logs/error.log`.

   Busque en los registros de AEM para ver las instrucciones de registro agregadas en el modelo Sling:

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   > También puede ver algunos rastros de pila si el producto utilizado en el teaser no tiene el atributo `eco_friendly` como parte de su conjunto de atributos.

## Agregar estilos para el distintivo compatible con Eco {#add-styles}

En este punto, la lógica para cuándo mostrar el distintivo **Eco Friendly** está funcionando, aunque el texto sin formato podría utilizar algunos estilos. A continuación, agregue un icono y estilos al módulo `ui.frontend` para completar la implementación.

1. Descargue el archivo [eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg). Se utilizará como distintivo **Eco Friendly**.
1. Vuelva al IDE y vaya a la carpeta `ui.frontend` .
1. Añada el archivo `eco_friendly.svg` a la carpeta `ui.frontend/src/main/resources/images`:

   ![Se agregó SVG compatible con el ecosistema](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. Abra el archivo `productteaser.scss` en `ui.frontend/src/main/styles/commerce/_productteaser.scss`.
1. Añada las siguientes reglas de Sass dentro de la clase `.productteaser` :

   ```scss
   .productteaser {
       ...
       .item__eco {
           width: 60px;
           height: 60px;
           left: 0px;
           overflow: hidden;
           position: absolute;
           padding: 5px;
   
       span {
           display: block;
           position: absolute;
           width: 45px;
           height: 45px;
           text-indent: -9999px;
           background: no-repeat center center url('../resources/images/eco_friendly.svg');
           }
       }
   ...
   }
   ```

   >[!NOTE]
   >
   > Consulte [Diseño de componentes principales del CIF](./style-cif-component.md) para obtener más información sobre los flujos de trabajo front-end.

1. Guarde los cambios e implemente las actualizaciones en AEM con sus habilidades con Maven, desde un terminal de línea de comandos:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. Actualice a la **Página principal de Venia** en [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) donde se ha agregado el teaser de productos.

   ![Implementación Final De Distintivo Compatible Con Eco](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Felicitaciones {#congratulations}

Acaba de personalizar su primer componente del CIF de AEM. Descargue los [archivos de solución terminados aquí](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip).

## Desafío para una bonificación {#bonus-challenge}

Revise la funcionalidad del distintivo **New** que ya se ha implementado en el teaser de productos. Intente agregar una casilla de verificación adicional para que los autores controlen cuándo se debe mostrar el distintivo **Eco Friendly**. Deberá actualizar el cuadro de diálogo del componente en `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`.

![Nuevo desafío para la implementación de distintivos](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## Recursos adicionales {#additional-resources}

- [Tipo de archivo de AEM](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype/overview.html)
- [Componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components)
- [Personalización de los componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
- [Personalización de componentes principales](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/customizing.html)
- [Introducción a AEM Sites](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
