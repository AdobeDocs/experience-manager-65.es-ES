---
title: Personalice los componentes principales de CIF
description: Obtenga información sobre cómo personalizar los componentes principales de Adobe Experience Manager CIF. CIF El tutorial explica cómo ampliar de forma segura un componente principal de la para satisfacer los requisitos específicos de la empresa. Obtenga información sobre cómo ampliar una consulta de GraphQL CIF para devolver un atributo personalizado y mostrar el nuevo atributo en un componente principal de la.
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
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '2567'
ht-degree: 15%

---

# Personalización de componentes principales de Adobe Experience Manager CIF {#customize-cif-components}

El [CIF Proyecto Venia en la](https://github.com/adobe/aem-cif-guides-venia) es una base de código de referencia para utilizar [Componentes principales del CIF](https://github.com/adobe/aem-core-cif-components). En este tutorial, se amplía aún más la variable [Teaser de productos](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) para mostrar un atributo personalizado de Adobe Commerce. También obtendrá más información sobre la integración de GraphQL entre Adobe Experience Manager AEM () y Adobe Commerce CIF y los enlaces de extensión que proporcionan los componentes principales de la.

>[!TIP]
>
>Utilice el [AEM Arquetipo de proyecto](https://github.com/adobe/aem-project-archetype) al iniciar su propia implementación de commerce.

## Qué va a generar

La marca Venia ha empezado recientemente a fabricar algunos productos con materiales sostenibles y la empresa desea mostrar un **Respetuoso con el medio ambiente** como parte del teaser de productos. Se crea un nuevo atributo personalizado en Adobe Commerce para indicar si un producto utiliza el **Respetuoso con el medio ambiente** material. Este atributo personalizado se agrega como parte de la consulta de GraphQL y se muestra en el teaser de productos para productos especificados.

![Implementación final de distintivo ecológico](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Requisitos previos {#prerequisites}

Se requiere un entorno de desarrollo local para completar este tutorial. AEM Esto incluye una instancia de ejecución de la instancia de que está configurada y conectada a una instancia de Adobe Commerce. Revise los requisitos y pasos para [AEM configuración de un desarrollo local con](../develop.md). Para seguir el tutorial por completo, necesita permisos para agregar [Atributos para un producto](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) en Adobe Commerce.

También necesita el IDE de GraphQL, como [GraphiQL](https://github.com/graphql/graphiql) o una extensión del explorador para ejecutar los ejemplos de código y los tutoriales. Si instala una extensión de explorador, asegúrese de que pueda establecer encabezados de solicitud. En Google Chrome, [Cliente de Altair GraphQL](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja) es una extensión que puede realizar el trabajo.

## Clonar el proyecto Venia {#clone-venia-project}

Se clonará el [Proyecto Venia](https://github.com/adobe/aem-cif-guides-venia) y, a continuación, invalide los estilos predeterminados.

>[!NOTE]
>
>**Siéntase libre de usar un proyecto existente** AEM CIF (en función del Tipo de archivo del proyecto de la con el que se incluye la) y omita esta sección.

1. Ejecute el siguiente comando de Git para clonar el proyecto:

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. Cree e implemente el proyecto en una instancia local de AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. AEM Añada las configuraciones de OSGi necesarias para conectar la instancia de a una instancia de Adobe Commerce o añadir las configuraciones al proyecto recién creado.

1. En este punto, debería tener una versión de trabajo de una tienda conectada a una instancia de Adobe Commerce. Vaya a `US` > `Home` página en: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   Hay que ver que la tienda esté usando actualmente el tema de Venia. Al expandir el menú principal de la tienda, verá varias categorías que indican que la conexión con Adobe Commerce está funcionando.

   ![Tienda configurada con tema de Venia](../assets/customize-cif-components/venia-store-configured.png)

## Creación del teaser de productos {#author-product-teaser}

El componente teaser de productos se amplía a través de este tutorial. Como primer paso, añada una instancia del teaser de productos a la página de inicio para comprender la funcionalidad de línea de base.

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

AEM Los productos y los datos de productos que se muestran en la lista de productos se almacenan en Adobe Commerce. A continuación, añada un nuevo atributo para **Respetuoso con el medio ambiente** como parte del conjunto de atributos del producto mediante la interfaz de usuario de Adobe Commerce.

>[!TIP]
>
>Ya tiene un personalizado **Sí/No** como parte de su conjunto de atributos del producto? No dude en usarlo y saltarse esta sección.

1. Inicie sesión en la instancia de Adobe Commerce.
1. Vaya a **Catálogo** > **Productos**.
1. Actualice el filtro de búsqueda para encontrar el **Producto configurable** se utiliza cuando se añade al componente Teaser en el ejercicio anterior. Abra el producto en modo de edición.

   ![Buscar el producto Valeria](../assets/customize-cif-components/search-valeria-product.png)

1. En la vista del producto, haga clic en **Añadir atributo** > **Crear nuevo atributo**.
1. Rellene el **Nuevo atributo** formulario con los siguientes valores (dejar la configuración predeterminada para otros valores)

   | Conjunto de campos | Etiqueta de campo | Valor |
   | ----------------------------- | ------------------ | ---------------- |
   | Propiedades de atributo | Etiqueta de atributo | **Respetuoso con el medio ambiente** |
   | Propiedades de atributo | Tipo de entrada de catálogo | **Sí/No** |
   | Propiedades de atributo avanzadas | Código de atributo | **eco_friendly** |

   ![Formulario de nuevo atributo](../assets/customize-cif-components/attribute-new-form.png)

   Clic **Guardar atributo** cuando termine.

1. Desplácese hasta la parte inferior del producto y expanda **Atributos** encabezado. Debería ver el nuevo **Respetuoso con el medio ambiente** field. Cambie la opción a **Sí**.

   ![Cambiar a sí](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **Guardar** los cambios en el producto.

   >[!TIP]
   >
   >Más detalles acerca de la administración de [Los atributos del producto se encuentran en la guía del usuario de Adobe Commerce](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html).

1. Vaya a **Sistema** > **Herramientas** > **Administración de caché**. Dado que se ha realizado una actualización del esquema de datos, debe invalidar algunos de los tipos de caché en Adobe Commerce.
1. Marque la casilla junto a **Configuración** y envíe el tipo de caché para **Actualizar**

   ![Actualizar tipo de caché de configuración](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   >Más detalles acerca de [La administración de caché se encuentra en la guía del usuario de Adobe Commerce](https://docs.magento.com/user-guide/system/cache-management.html).

## Utilizar un IDE de GraphQL para comprobar el atributo {#use-graphql-ide}

AEM Antes de saltar al código de la, es útil explorar la [Adobe Commerce GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) usar un IDE de GraphQL. La integración de Adobe Commerce AEM con se realiza principalmente mediante una serie de consultas de GraphQL. Comprender y modificar las consultas de GraphQL CIF es una de las formas clave en que se pueden ampliar los componentes principales de la.

A continuación, utilice un IDE de GraphQL para comprobar que la variable `eco_friendly` se ha añadido el atributo al conjunto de atributos del producto. Las capturas de pantalla de este tutorial utilizan la variable [Cliente de Altair GraphQL](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja).

1. Abra el IDE de GraphQL e introduzca la dirección URL `http://<server>/graphql` en la barra URL del IDE o de la extensión.
2. Añada lo siguiente [consulta de productos](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) donde `YOUR_SKU` es el **SKU** del producto utilizado en el ejercicio anterior:

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

3. Ejecute la consulta y debería obtener una respuesta como la siguiente:

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

El valor de **Sí** es un número entero de **1**. Será útil cuando escriba la consulta de GraphQL en Java™.

>[!TIP]
>
>Documentación más detallada sobre [Adobe Commerce GraphQL se puede encontrar aquí](https://devdocs.magento.com/guides/v2.4/graphql/index.html).

## Actualización del modelo de Sling para el teaser de productos {#updating-sling-model-product-teaser}

A continuación, ampliará la lógica empresarial del teaser de productos implementando un modelo Sling. [Modelos Sling](https://sling.apache.org/documentation/bundles/models.html), son objetos Java™ antiguos comunes (&quot;POJO&quot;) impulsados por anotaciones que implementan cualquier lógica empresarial necesaria para el componente. Los modelos Sling se utilizan con scripts HTL como parte del componente. Usted seguirá el [patrón de delegación para modelos Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) para poder ampliar partes del modelo de teaser de productos existente.

Los modelos Sling se implementan como Java™ y se pueden encontrar en la **núcleo** módulo del proyecto generado.

Uso [el IDE de su elección](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#set-up-the-development-ide) para importar el proyecto Venia. Las capturas de pantalla utilizadas son de [IDE de código de Visual Studio](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?#microsoft-visual-studio-code).

1. En el IDE, vaya a **núcleo** módulo a: `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`.

   ![IDE de ubicación principal](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` CIF es una interfaz de Java™ que amplía la interfaz de [ProductTeaser](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) interfaz.

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

Este es un nuevo método para encapsular la lógica e indicar si el producto tiene el `eco_friendly` atributo establecido en **Sí** o **No**.

1. A continuación, inspeccione el `MyProductTeaserImpl.java` en `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`.

   El [patrón de delegación para modelos Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) permite `MyProductTeaserImpl` para referencia `ProductTeaser` modelo a través de `sling:resourceSuperType` propiedad:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   Para todos los métodos que no se anulan ni cambian, puede devolver el valor que `ProductTeaser` devuelve. Por ejemplo:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   Esto minimiza la cantidad de código Java™ que debe escribir una implementación.

1. AEM CIF Uno de los puntos de extensión adicionales que proporcionan los componentes principales de la es el `AbstractProductRetriever` que proporciona acceso a atributos de producto específicos. Inspect el `initModel()` método:

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

   El `@PostConstruct` Esta anotación garantiza que se llame a este método cuando se inicialice el modelo Sling.

   Tenga en cuenta que la consulta de GraphQL del producto ya se ha ampliado con la variable `extendProductQueryWith` método para recuperar el `created_at` atributo. Este atributo se utiliza posteriormente como parte de la variable `isShowBadge()` método.

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

   Añadir a `extendProductQueryWith` es una forma eficaz de garantizar que el resto del modelo disponga de atributos de producto adicionales. También minimiza el número de consultas ejecutadas.

   En el código anterior, la variable`addCustomSimpleField` se utiliza para recuperar la variable `eco_friendly` atributo. Esto ilustra cómo se puede consultar cualquier atributo personalizado que forme parte del esquema de Adobe Commerce.

   >[!NOTE]
   >
   >El `createdAt()` El método se ha implementado como parte de [Interfaz de producto](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java). Se han implementado la mayoría de los atributos de esquema encontrados con frecuencia, por lo que solo debe utilizarse `addCustomSimpleField` para atributos verdaderamente personalizados.

1. Añada un registrador para depurar el código Java™:

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. A continuación, implemente la `isEcoFriendly()` método:

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

   En el método anterior, la variable `productRetriever` se utiliza para recuperar el producto y la `getAsInteger()` se utiliza para obtener el valor del `eco_friendly` atributo. Según las consultas de GraphQL que ejecutó anteriormente, sabe que el valor esperado cuando `eco_friendly` el atributo se establece en &quot;**Sí**&quot; es en realidad un número entero de **1**.

   Ahora que se ha actualizado el modelo Sling, el marcado del componente debe actualizarse para mostrar realmente un indicador de **Respetuoso con el medio ambiente** se basa en el modelo Sling.

## Personalización del marcado del teaser de productos {#customize-markup-product-teaser}

Una extensión común de los componentes de AEM es modificar el marcado que genera el componente. Esto se realiza anulando la [secuencia de comandos HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=es) que utiliza el componente para representar su marcado. El lenguaje de plantilla de HTML AEM (HTL) es un lenguaje de plantilla ligero que los componentes de la plantilla utilizan para representar dinámicamente el marcado basado en contenido creado, lo que permite reutilizar los componentes. El teaser de productos, por ejemplo, se puede reutilizar una y otra vez para mostrar diferentes productos.

En este caso, desea renderizar un titular sobre el teaser para indicar que el producto es &quot;Respetuoso con el medio ambiente&quot; basado en un atributo personalizado. El patrón de diseño para [personalizar el marcado](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) de un componente es en realidad estándar para todos los componentes AEM, no solo para los componentes principales del CIF de AEM.

>[!NOTE]
>
>CIF CIF Si personaliza un componente mediante los selectores de producto y categoría de como este teaser de productos o el componente de página de la página, asegúrese de incluir los necesarios `cif.shell.picker` clientlib para los cuadros de diálogo de componentes. Consulte [CIF Uso del selector de productos y categorías de la](use-cif-pickers.md) para obtener más información.

1. En el IDE, navegue y expanda `ui.apps` y expanda la jerarquía de carpetas a: `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` e inspeccione el `.content.xml` archivo.

   ![teaser de productos ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   La definición del componente para el componente teaser de productos en este proyecto está arriba. Observe la propiedad `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Este es un ejemplo de creación de un [componente Proxy](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html#create-proxy-components). AEM CIF En lugar de copiar y pegar todas las secuencias de comandos HTL del teaser de productos de los componentes principales de la, puede utilizar el complemento `sling:resourceSuperType` para heredar todas las funciones.

1. Abra el archivo `productteaser.html`. Esta es una copia del `productteaser.html` desde el [CIF Teaser de productos](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)

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

   Observe que el modelo Sling de `MyProductTeaser` se utiliza y se asigna a `product` variable.

1. Modificar `productteaser.html` para realizar una llamada al `isEcoFriendly` método implementado en el ejercicio anterior:

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

   Al llamar a un método del modelo Sling en HTL, la variable `get` y `is` del método se borra y la primera letra se convierte en minúsculas. Entonces `isShowBadge()` pasa a `.showBadge` y `isEcoFriendly` pasa a `.ecoFriendly`. Basado en el valor booleano devuelto desde `.isEcoFriendly()` determina si la variable `<span>Eco Friendly</span>` se muestra.

   Más información sobre `data-sly-test` y otros [Puede encontrar instrucciones de bloque HTL aquí](https://experienceleague.adobe.com/docs/experience-manager-htl/content/specification.html).

1. AEM Guarde los cambios e implemente las actualizaciones para que se puedan usar con sus habilidades con Maven, desde un terminal de línea de comandos:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. AEM Abra una nueva ventana del explorador y vaya a la página de y a la página de inicio de la barra de herramientas de **Consola OSGi** > **Estado** > **Modelos Sling**: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. Buscar por `MyProductTeaserImpl` y debería ver una línea como la siguiente:

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   Esto indica que el modelo Sling se ha implementado y asignado correctamente al componente correcto.

1. Actualice a la **Página principal de Venia** en [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) donde se ha agregado el teaser de productos.

   ![Se muestra un mensaje ecológico](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   Si el producto tiene el `eco_friendly` atributo establecido en **Sí**, debería ver el texto &quot;Eco Friendly&quot; en la página. Intente cambiar a diferentes productos para ver el cambio de comportamiento.

1. AEM A continuación, abra la `error.log` para ver las instrucciones de registro agregadas. El `error.log` es el `<AEM SDK Install Location>/crx-quickstart/logs/error.log`.

   AEM Busque los registros de la para ver las instrucciones de registro agregadas en el modelo Sling:

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   >También puede ver algunos seguimientos de pila si el producto utilizado en el teaser no tiene el `eco_friendly` como parte de su conjunto de atributos.

## Añadir estilos para la insignia ecológica {#add-styles}

En este punto, la lógica de cuándo mostrar la variable **Respetuoso con el medio ambiente** El distintivo funciona, pero el texto sin formato podría utilizar algunos estilos. A continuación, añada un icono y estilos a `ui.frontend` para completar la implementación.

1. Descargue la [eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) archivo. Se usa como. **Respetuoso con el medio ambiente** insignia.
1. Vuelva al IDE y vaya al `ui.frontend` carpeta.
1. Añada el `eco_friendly.svg` archivo a la `ui.frontend/src/main/resources/images` carpeta:

   ![Se agregó un SVG ecológico](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. Abra el archivo `productteaser.scss` en `ui.frontend/src/main/styles/commerce/_productteaser.scss`.
1. Agregue las siguientes reglas Sass dentro de la variable `.productteaser` clase:

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
   >Desproteger [CIF Estilo de componentes principales de](./style-cif-component.md) para obtener más información sobre los flujos de trabajo front-end.

1. AEM Guarde los cambios e implemente las actualizaciones para que se puedan usar con sus habilidades con Maven, desde un terminal de línea de comandos:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Actualice a la **Página principal de Venia** en [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) donde se ha agregado el teaser de productos.

   ![Implementación final de distintivo ecológico](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Felicitaciones {#congratulations}

AEM CIF Ha personalizado su primer componente de la. Descargue la [archivos de solución finalizados aquí](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip).

## Desafío para una bonificación {#bonus-challenge}

Revise la funcionalidad de **Nuevo** que ya se ha implementado en el teaser de productos. Intente añadir una casilla de verificación adicional para que los autores controlen cuándo se **Respetuoso con el medio ambiente** debe mostrarse el distintivo. Debe actualizar el cuadro de diálogo del componente en `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`.

![Nuevo desafío de implementación de distintivos](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## Recursos adicionales {#additional-resources}

- [Tipo de archivo de AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es)
- [Componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components)
- [Personalización de los componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components)
- [Personalización de componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=es)
- [Introducción a AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es)
- [CIF Uso del selector de productos y categorías de la](use-cif-pickers.md)
