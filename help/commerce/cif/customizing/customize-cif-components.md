---
title: Personalice los componentes principales de CIF
description: Aprenda a personalizar AEM componentes principales del CIF. El tutorial explica cómo ampliar de forma segura un componente principal del CIF para satisfacer los requisitos específicos de la empresa. Obtenga información sobre cómo ampliar una consulta de GraphQL para devolver un atributo personalizado y mostrar el nuevo atributo en un componente principal del CIF.
sub-product: Commerce
topics: Development
version: Cloud Service
doc-type: tutorial
activity: develop
audience: developer
feature: Commerce Integration Framework
kt: 4279
thumbnail: customize-aem-cif-core-component.jpg
exl-id: 8933942e-be49-49d3-bf0a-7225257e2803
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '2604'
ht-degree: 24%

---

# Personalización de los componentes principales del CIF de AEM {#customize-cif-components}

La variable [Proyecto de CIF Venia](https://github.com/adobe/aem-cif-guides-venia) es una base de código de referencia para usar [Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components). En este tutorial, ampliará aún más la variable [Teaser de productos](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) para mostrar un atributo personalizado de Adobe Commerce. También obtendrá más información sobre la integración de GraphQL entre AEM y Adobe Commerce y los enlaces de extensión proporcionados por los componentes principales del CIF.

>[!TIP]
>
>Utilice la variable [AEM tipo de archivo del proyecto](https://github.com/adobe/aem-project-archetype) al iniciar su propia implementación de comercio.

## Qué va a generar

La marca Venia comenzó recientemente a fabricar algunos productos utilizando materiales sostenibles y la empresa quiere mostrar un **Compatible con el ecosistema** distintivo como parte del teaser de productos. Se creará un nuevo atributo personalizado en Adobe Commerce para indicar si un producto usa la variable **Eco amigable** material. Este atributo personalizado se agregará como parte de la consulta de GraphQL y se mostrará en el teaser de productos de los productos especificados.

![Implementación Final De Distintivo Compatible Con Eco](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Requisitos previos {#prerequisites}

Se requiere un entorno de desarrollo local para completar este tutorial. Esto incluye una instancia de AEM en ejecución configurada y conectada a una instancia de Adobe Commerce. Consulte los requisitos y pasos para [configuración de un desarrollo local con AEM](../develop.md). Para seguir el tutorial por completo, necesitará permisos para agregar [Atributos a un producto](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) en Adobe Commerce.

También necesitará el IDE de GraphQL como [GraphiQL](https://github.com/graphql/graphiql) o una extensión del explorador para ejecutar ejemplos de código y tutoriales. Si instala una extensión del explorador, asegúrese de que tenga la capacidad de establecer encabezados de solicitud. En Google Chrome, [Cliente Altair GraphQL](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja) es una extensión que puede realizar el trabajo.

## Clonar el proyecto de Venia {#clone-venia-project}

Clonaremos el [Proyecto Venia](https://github.com/adobe/aem-cif-guides-venia) y, a continuación, anule los estilos predeterminados.

>[!NOTE]
>
>**Siéntase libre de usar un proyecto existente** (basado en el tipo de archivo del proyecto AEM con CIF incluido) y omita esta sección.

1. Ejecute el siguiente comando git para clonar el proyecto:

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. Cree e implemente el proyecto en una instancia local de AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Agregue las configuraciones de OSGi necesarias para conectar la instancia de AEM a una instancia de Adobe Commerce o agregue las configuraciones al proyecto recién creado.

1. En este punto, debe tener una versión de trabajo de una tienda conectada a una instancia de Adobe Commerce. Vaya a la `US` > `Home` en: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   Hay que ver que la tienda esté usando actualmente el tema de Venia. Al expandir el menú principal de la tienda, debería ver varias categorías que indican que la conexión a Adobe Commerce está funcionando.

   ![Tienda configurada con tema de Venia](../assets/customize-cif-components/venia-store-configured.png)

## Creación del teaser de productos {#author-product-teaser}

El componente teaser de productos se ampliará a lo largo de este tutorial. Como primer paso, agregue una nueva instancia del teaser de productos a la página principal para comprender la funcionalidad de línea de base.

1. Vaya hasta la **Página de inicio** del sitio: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. Inserte un nuevo componente **teaser de productos** en el contenedor del diseño principal de la página.

   ![Inserción del teaser de productos](../assets/customize-cif-components/product-teaser-add-component.png)

3. Expanda el panel lateral (si no está activado) y cambie desde menú desplegable del buscador de recursos a **Productos**. Esto debería mostrar una lista de los productos disponibles de una instancia de Adobe Commerce conectada. Seleccione un producto y **arrástrelo y suéltelo** en el componente **teaser de productos** de la página.

   ![Arrastrar y soltar teaser de productos](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   >Tenga en cuenta que también puede configurar el producto mostrado configurando el componente con el cuadro de diálogo (haga clic en el icono de _llave inglesa_).

4. Ahora debería ver un producto que muestra el teaser de productos. Se muestran el nombre y el precio del producto ya que son atributos predeterminados.

   ![Teaser de productos: estilo predeterminado](../assets/customize-cif-components/product-teaser-default-style.png)

## Añadir un atributo personalizado en Adobe Commerce {#add-custom-attribute}

Los productos y los datos de productos mostrados en AEM se almacenan en Adobe Commerce. A continuación, añada un nuevo atributo para **Compatible con el ecosistema** como parte del atributo de producto configurado mediante la interfaz de usuario de Adobe Commerce.

>[!TIP]
>
>Ya tiene un **Sí/No** como parte de su conjunto de atributos de producto? Siéntase libre de usarlo y omita esta sección.

1. Inicie sesión en la instancia de Adobe Commerce.
1. Vaya a **Catálogo** > **Productos**.
1. Actualice el filtro de búsqueda para encontrar la variable **Producto configurable** se utiliza cuando se añade al componente Teaser en el ejercicio anterior. Abra el producto en modo de edición.

   ![Buscar el producto Valeria](../assets/customize-cif-components/search-valeria-product.png)

1. En la vista del producto, haga clic en **Añadir atributo** > **Crear nuevo atributo**.
1. Complete el **Nuevo atributo** formulario con los siguientes valores (deje la configuración predeterminada para otros valores)

   | Conjunto de campos | Etiqueta de campo | Valor |
   | ----------------------------- | ------------------ | ---------------- |
   | Propiedades de atributo | Etiqueta de atributo | **Compatible con el ecosistema** |
   | Propiedades de atributo | Tipo de entrada de catálogo | **Sí/No** |
   | Propiedades de atributos avanzadas | Código de atributo | **eco_friendly** |

   ![Nuevo formulario de atributos](../assets/customize-cif-components/attribute-new-form.png)

   Haga clic en **Guardar atributo** cuando termine.

1. Desplácese hasta la parte inferior del producto y amplíe el **Atributos** encabezado. Debería ver el nuevo **Compatible con el ecosistema** campo . Cambie el conmutador a **Sí**.

   ![Cambiar alternancia a sí](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **Guardar** los cambios en el producto.

   >[!TIP]
   >
   >Más detalles sobre la administración [Los atributos de producto se encuentran en la guía del usuario de Adobe Commerce](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html).

1. Vaya a **Sistema** > **Herramientas** > **Administración de caché**. Como se ha realizado una actualización del esquema de datos, es necesario invalidar algunos de los tipos de caché en Adobe Commerce.
1. Marque la casilla situada junto a **Configuración** y envíe el tipo de caché para **Actualizar**

   ![Actualizar tipo de caché de configuración](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   >Más detalles sobre [La Administración de caché se encuentra en la guía del usuario de Adobe Commerce](https://docs.magento.com/user-guide/system/cache-management.html).

## Uso de un IDE de GraphQL para verificar el atributo {#use-graphql-ide}

Antes de saltar a AEM código, es útil explorar el [Adobe Commerce GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) uso de un IDE de GraphQL. La integración de Adobe Commerce con AEM se realiza principalmente mediante una serie de consultas de GraphQL. Comprender y modificar las consultas de GraphQL es una de las formas clave de ampliar los componentes principales del CIF.

A continuación, utilice un IDE de GraphQL para verificar que la variable `eco_friendly` se ha agregado al conjunto de atributos de producto. Las capturas de pantalla de este tutorial utilizan la variable [Cliente Altair GraphQL](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja).

1. Abra el IDE de GraphQL e introduzca la URL `http://<server>/graphql` en la barra URL de su IDE o extensión.
2. Agregue lo siguiente [consulta de productos](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) donde `YOUR_SKU` es la variable **SKU** del producto utilizado en el ejercicio anterior:

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

   Tenga en cuenta que el valor de **Sí** es un entero de **1**. Esto resulta útil cuando escribimos la consulta GraphQL en Java.

   >[!TIP]
   >
   >Documentación más detallada sobre [Adobe Commerce GraphQL se puede encontrar aquí](https://devdocs.magento.com/guides/v2.4/graphql/index.html).

## Actualización del modelo de Sling para el teaser de productos {#updating-sling-model-product-teaser}

A continuación, ampliaremos la lógica empresarial del teaser de productos implementando el modelo Sling. [Los modelos de Sling](https://sling.apache.org/documentation/bundles/models.html) son objetos Java antiguos comunes (&quot;POJO&quot;), impulsados por anotaciones que implementan cualquier lógica comercial necesaria para el componente. Los modelos Sling se utilizan junto con las secuencias de comandos HTL como parte del componente. Seguiremos el patrón de [delegación de modelos Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) para que podamos extender las partes del modelo de teaser de productos existente.

Los modelos Sling se implementan como Java y se pueden encontrar en el módulo **principal** del proyecto generado.

Uso [el IDE que elija](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) para importar el proyecto Venia. Las capturas de pantalla utilizadas son de la [Código IDE de Visual Studio](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code).

1. En su IDE, vaya a la sección **core** para: `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`.

   ![IDE de ubicación principal](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` es una interfaz de Java que amplía el CIF [ProductTeaser](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) interfaz.

   Ya se ha agregado un nuevo método con el nombre `isShowBadge()` para mostrar un distintivo si el producto se considera &quot;nuevo&quot;.

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

   Este es un nuevo método que introduciremos para encapsular la lógica para indicar si el producto tiene la variable `eco_friendly` establecido en **Sí** o **No**.

1. A continuación, revise la `MyProductTeaserImpl.java` at `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`.

   La variable [patrón de delegación para modelos Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) permite `MyProductTeaserImpl` referencia `ProductTeaser` a través del `sling:resourceSuperType` propiedad:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   Para todos los métodos que no queremos anular o cambiar, simplemente podemos devolver el valor de que la variable `ProductTeaser` devuelve. Por ejemplo:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   Esto minimiza la cantidad de código Java que debe escribir una implementación.

1. Uno de los puntos de extensión adicionales que proporcionan AEM componentes principales del CIF es el `AbstractProductRetriever` que proporciona acceso a atributos de producto específicos. Inspect la variable `initModel()` método:

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

   La variable `@PostConstruct` la anotación garantiza que se llame a este método en cuanto se inicialice el modelo Sling.

   Tenga en cuenta que la consulta de producto GraphQL ya se ha ampliado con la variable `extendProductQueryWith` método para recuperar el `created_at` atributo. Este atributo se utiliza más adelante como parte del `isShowBadge()` método.

1. Actualice la consulta de GraphQL para incluir el `eco_friendly` en la consulta parcial:

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p -> p
               .createdAt()
               .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
           );
       }
   }
   ```

   Añadir al método `extendProductQueryWith` es una manera eficaz de garantizar que el resto del modelo disponga de atributos de productos adicionales. También minimiza el número de consultas ejecutadas.

   En el código anterior, la variable`addCustomSimpleField` se utiliza para recuperar la variable `eco_friendly` atributo. Esto ilustra cómo se puede consultar cualquier atributo personalizado que forme parte del esquema de Adobe Commerce.

   >[!NOTE]
   >
   >La variable `createdAt()` se ha implementado como parte de la función [Interfaz de producto](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java). Se han implementado la mayoría de los atributos de esquema encontrados con frecuencia, por lo que solo debe utilizarse `addCustomSimpleField` para atributos verdaderamente personalizados.

1. Agregue un registrador para ayudar a depurar el código Java:

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. A continuación, implemente la variable `isEcoFriendly()` método:

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

   En el método anterior, la variable `productRetriever` se usa para recuperar el producto y la variable `getAsInteger()` para obtener el valor de `eco_friendly` atributo. Basándonos en las consultas de GraphQL que ejecutamos anteriormente sabemos que el valor esperado cuando la variable `eco_friendly` se configura como &quot;**Sí**&quot; es en realidad un entero de **1**.

   Ahora que se ha actualizado el modelo Sling, es necesario actualizar el marcado del componente para que muestre un indicador de **Compatible con el ecosistema** basado en el modelo Sling.

## Personalización del marcado del teaser de productos {#customize-markup-product-teaser}

Una extensión común de los componentes de AEM es modificar el marcado que genera el componente. Esto se realiza anulando la [secuencia de comandos HTL](https://docs.adobe.com/content/help/es-ES/experience-manager-htl/using/overview.html) que utiliza el componente para representar su marcado. La plantilla de idioma HTML (HTL) es un idioma de plantilla ligero que los componentes de AEM utilizan para representar dinámicamente el marcado basado en contenido creado, lo que permite la reutilización de los componentes. El teaser de productos, por ejemplo, se puede reutilizar una y otra vez para mostrar diferentes productos.

En nuestro caso, queremos renderizar un banner sobre el teaser para indicar que el producto es &quot;compatible con el medio ambiente&quot; basado en un atributo personalizado. El patrón de diseño para [personalizar el marcado](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) de un componente es en realidad estándar para todos los componentes AEM, no solo para los componentes principales del CIF de AEM.

>[!NOTE]
>
>Si personaliza un componente mediante los seleccionadores de productos y categorías del CIF como este teaser de productos o el componente de página del CIF, asegúrese de incluir el `cif.shell.picker` clientlib para los cuadros de diálogo de componentes. Consulte [Uso del selector de productos y categorías del CIF](use-cif-pickers.md) para obtener más información.

1. En el IDE, navegue y expanda el `ui.apps` y expanda la jerarquía de carpetas a: `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` e inspeccione el `.content.xml` archivo.

   ![Product Teaser ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   Arriba se encuentra la definición del componente para el componente teaser de productos en nuestro proyecto. Observe la propiedad `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Este es un ejemplo de creación de un [componente Proxy](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/get-started/using.html#create-proxy-components). En lugar de copiar y pegar todas las secuencias de comandos HTL del teaser de productos de los componentes principales del CIF de AEM, podemos usar `sling:resourceSuperType` para heredar todas las funcionalidades.

1. Abra el archivo `productteaser.html`. Esta es una copia de `productteaser.html` del [Teaser del producto CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)

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

   Observe que el modelo Sling para `MyProductTeaser` se utiliza y se asigna a la variable `product` variable.

1. Modificar `productteaser.html` para realizar una llamada a la función `isEcoFriendly` método implementado en el ejercicio anterior:

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

   Al llamar a un método de modelo de Sling en HTL, la variable `get` y `is` parte del método se suelta y la primera letra se escribe en minúsculas. So `isShowBadge()` se convierte `.showBadge` y `isEcoFriendly` se convierte `.ecoFriendly`. Basado en el valor booleano devuelto por `.isEcoFriendly()` determina si la variable `<span>Eco Friendly</span>` se muestra.

   Más información sobre `data-sly-test` y otros [Las instrucciones de bloque HTL se pueden encontrar aquí](https://docs.adobe.com/content/help/en/experience-manager-htl/using/htl/block-statements.html#test).

1. Guarde los cambios e implemente las actualizaciones en AEM con sus habilidades con Maven, desde un terminal de línea de comandos:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Abra una nueva ventana del explorador y vaya a AEM y a la **Consola OSGi** > **Estado** > **Modelos de Sling**: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. Buscar `MyProductTeaserImpl` y debería ver una línea como la siguiente:

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   Esto indica que el modelo Sling se ha implementado correctamente y se ha asignado al componente correcto.

1. Actualice a **Página de inicio de Venia** at [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) donde se ha añadido el teaser de productos.

   ![Se muestra un mensaje ecológico](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   Si el producto tiene la variable `eco_friendly` establecido en **Sí**, debería ver el texto &quot;Eco Friendly&quot; en la página. Intente cambiar a diferentes productos para ver el cambio de comportamiento.

1. A continuación, abra la AEM `error.log` para ver las instrucciones de registro que agregamos. La variable `error.log` se encuentra en `<AEM SDK Install Location>/crx-quickstart/logs/error.log`.

   Busque en los registros de AEM para ver las instrucciones de registro agregadas en el modelo Sling:

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   >También puede ver algunos rastros de pila si el producto utilizado en el teaser no tiene el valor `eco_friendly` como parte de su conjunto de atributos.

## Agregar estilos para el distintivo ecológico {#add-styles}

En este punto, la lógica de cuándo mostrar la variable **Compatible con el ecosistema** está funcionando, sin embargo el texto sin formato podría utilizar algunos estilos. A continuación, agregue un icono y estilos a la variable `ui.frontend` para completar la implementación.

1. Descargue el [eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) archivo. Se utilizará como el **Compatible con el ecosistema** distintivo.
1. Vuelva al IDE y vaya a la `ui.frontend` carpeta.
1. Agregue la variable `eco_friendly.svg` a `ui.frontend/src/main/resources/images` carpeta:

   ![Se agregó un SVG compatible con el ecosistema.](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. Abra el archivo . `productteaser.scss` at `ui.frontend/src/main/styles/commerce/_productteaser.scss`.
1. Añada las siguientes reglas de Sass dentro de la variable `.productteaser` Clase :

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
   >Consulte [Diseño de los componentes principales del CIF](./style-cif-component.md) para obtener más información sobre los flujos de trabajo front-end.

1. Guarde los cambios e implemente las actualizaciones en AEM con sus habilidades con Maven, desde un terminal de línea de comandos:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Actualice a **Página de inicio de Venia** at [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) donde se ha añadido el teaser de productos.

   ![Implementación Final De Distintivo Compatible Con Eco](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Felicitaciones {#congratulations}

Acaba de personalizar su primer componente del CIF de AEM. Descargue el [archivos de solución terminados aquí](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip).

## Desafío para una bonificación {#bonus-challenge}

Revise la funcionalidad de la variable **Nuevo** que ya se ha implementado en el teaser de productos. Intente agregar una casilla de verificación adicional para que los autores controlen cuándo se llama a la función **Compatible con el ecosistema** se debe mostrar el distintivo. Deberá actualizar el cuadro de diálogo del componente en `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`.

![Nuevo desafío para la implementación de distintivos](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## Recursos adicionales {#additional-resources}

- [Tipo de archivo de AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es)
- [Componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components)
- [Personalización de los componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
- [Personalización de componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=es)
- [Introducción a AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es)
- [Uso del selector de productos y categorías del CIF](use-cif-pickers.md)
