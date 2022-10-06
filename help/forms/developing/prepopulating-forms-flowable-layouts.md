---
title: Rellenado previo de Forms con diseños flexibles
seo-title: Prepopulating Forms with Flowable Layouts
description: Rellene previamente los formularios con una presentación flexible para mostrar los datos a los usuarios de un formulario procesado con la API de Java y la API de servicio web.
seo-description: Prepopulate forms with flowable layout to display data to users within a rendered form using the Java API and the Web Service API.
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
role: Developer
exl-id: ff087084-fb1c-43a4-ae54-cc77eb862493
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '3505'
ht-degree: 1%

---

# Rellenado previo de Forms con diseños flexibles {#prepopulating-forms-with-flowable-layouts1}

## Rellenado previo de Forms con diseños flexibles {#prepopulating-forms-with-flowable-layouts2}

Al cumplimentar los formularios de antemano, se muestran datos a los usuarios de un formulario procesado. Por ejemplo, supongamos que un usuario inicia sesión en un sitio web con un nombre de usuario y una contraseña. Si la autenticación se realiza correctamente, la aplicación cliente consulta una base de datos para obtener información del usuario. Los datos se combinan en el formulario y se procesan para el usuario. Como resultado, el usuario puede ver datos personalizados dentro del formulario.

Cumplimentar previamente un formulario tiene las siguientes ventajas:

* Permite al usuario ver datos personalizados en un formulario.
* Reduce la cantidad de escritura que el usuario hace para rellenar un formulario.
* Asegura la integridad de los datos teniendo control sobre dónde se colocan los datos.

Los dos orígenes de datos XML siguientes pueden rellenar previamente un formulario:

* Un origen de datos XDP, que es XML que se ajusta a la sintaxis XFA (o datos XFDF para rellenar previamente un formulario creado con Acrobat).
* Un origen de datos XML arbitrario que contiene pares de nombre/valor que coinciden con los nombres de campo del formulario (los ejemplos de esta sección utilizan un origen de datos XML arbitrario).

Debe existir un elemento XML para cada campo de formulario que desee rellenar previamente. El nombre del elemento XML debe coincidir con el nombre del campo. Se ignora un elemento XML si no se corresponde con un campo de formulario o si el nombre del elemento XML no coincide con el nombre del campo. No es necesario coincidir con el orden en que se muestran los elementos XML, siempre y cuando se especifiquen todos los elementos XML.

Cuando rellene previamente un formulario que ya contenga datos, debe especificar los datos que ya se muestran en el origen de datos XML. Supongamos que un formulario que contiene 10 campos tiene datos en cuatro campos. A continuación, suponga que desea rellenar previamente los seis campos restantes. En este caso, debe especificar 10 elementos XML en el origen de datos XML que se utiliza para rellenar previamente el formulario. Si especifica solo seis elementos, los cuatro campos originales están vacíos.

Por ejemplo, puede rellenar previamente un formulario, como el formulario de confirmación de ejemplo. (Consulte &quot;Formulario de confirmación&quot; en [Renderización de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md).)

Para rellenar previamente el formulario de confirmación de ejemplo, debe crear un origen de datos XML que contenga tres elementos XML que coincidan con los tres campos del formulario. Este formulario contiene los tres campos siguientes: `FirstName`, `LastName`y `Amount`. El primer paso es crear un origen de datos XML que contenga elementos XML que coincidan con los campos ubicados en el diseño de formulario. El siguiente paso es asignar valores de datos a los elementos XML, como se muestra en el siguiente código XML.

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

Después de rellenar previamente el formulario de confirmación con este origen de datos XML y después procesar el formulario, se muestran los valores de datos que asignó a los elementos XML, como se muestra en el diagrama siguiente.

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### Rellenado previo de formularios con diseños flexibles {#prepopulating_forms_with_flowable_layouts-1}

Forms con diseños flexibles es útil para mostrar una cantidad indeterminada de datos a los usuarios. Dado que la presentación del formulario se ajusta automáticamente a la cantidad de datos combinados, no es necesario predeterminar una presentación fija ni un número de páginas para el formulario, como se debe hacer con un formulario con una presentación fija.

Un formulario suele rellenarse con datos obtenidos durante la ejecución. Como resultado, puede rellenar previamente un formulario creando un origen de datos XML en memoria y colocando los datos directamente en el origen de datos XML en memoria.

Considere una aplicación basada en la Web, como una tienda en línea. Una vez que un comprador en línea termina de comprar artículos, todos los artículos adquiridos se colocan en un origen de datos XML en memoria que se utiliza para rellenar previamente un formulario. El diagrama siguiente muestra este proceso, que se explica en la tabla siguiente al diagrama.

![pf_pf_finsrv_webapp_v1](assets/pf_pf_finsrv_webapp_v1.png)

En la tabla siguiente se describen los pasos de este diagrama.

<table>
 <thead>
  <tr>
   <th><p>Etapa</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Un usuario compra artículos en una tienda en línea basada en la web. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Cuando el usuario termina de comprar artículos y hace clic en el botón Enviar, se crea un origen de datos XML en memoria. Los elementos comprados y la información del usuario se colocan en el origen de datos XML en memoria. </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>El origen de datos XML se utiliza para rellenar previamente un formulario de orden de compra (se muestra un ejemplo de este formulario después de esta tabla). </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>El formulario de orden de compra se representa en el explorador web del cliente. </p></td>
  </tr>
 </tbody>
</table>

En el diagrama siguiente se muestra un ejemplo de un formulario de orden de compra. La información de la tabla se puede ajustar al número de registros de los datos XML.

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>Un formulario puede rellenarse previamente con datos de otras fuentes, como una base de datos empresarial o aplicaciones externas.

### Consideraciones sobre el diseño de formularios {#form-design-considerations}

Forms con diseños flexibles se basa en diseños de formulario creados en Designer. Un diseño de formulario especifica un conjunto de reglas de presentación, presentación y captura de datos, incluido el cálculo de valores en función de los datos introducidos por el usuario. Las reglas se aplican cuando se introducen datos en un formulario. Los campos que se agregan a un formulario son subformularios que se encuentran dentro del diseño de formulario. Por ejemplo, en el formulario de orden de compra que se muestra en el diagrama anterior, cada línea es un subformulario. Para obtener información sobre la creación de un diseño de formulario que contenga subformularios, consulte [Creación de un formulario de orden de compra con una presentación flexible](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9).

### Explicación de los subgrupos de datos {#understanding-data-subgroups}

Un origen de datos XML se utiliza para rellenar previamente los formularios con diseños fijos y presentaciones flexibles. Sin embargo, la diferencia es que un origen de datos XML que rellena previamente un formulario con una presentación flexible contiene elementos XML de repetición que se utilizan para rellenar previamente subformularios que se repiten dentro del formulario. Estos elementos XML repetitivos se denominan subgrupos de datos.

Un origen de datos XML que se utiliza para rellenar previamente el formulario de orden de compra que se muestra en el diagrama anterior contiene cuatro subgrupos de datos de repetición. Cada subgrupo de datos corresponde a un artículo comprado. Los artículos comprados son un monitor, una lámpara de escritorio, un teléfono y una libreta de direcciones.

El siguiente origen de datos XML se utiliza para rellenar previamente el formulario de orden de compra.

```xml
     <header>
         <!-- XML elements used to prepopulate non-repeating fields such as address
         <!and city
         <txtPONum>8745236985</txtPONum>
         <dtmDate>2004-02-08</dtmDate>
         <txtOrderedByCompanyName>Any Company Name</txtOrderedByCompanyName>
         <txtOrderedByAddress>555, Any Blvd.</txtOrderedByAddress>
         <txtOrderedByCity>Any City</txtOrderedByCity>
         <txtOrderedByStateProv>ST</txtOrderedByStateProv>
         <txtOrderedByZipCode>12345</txtOrderedByZipCode>
         <txtOrderedByCountry>Any Country</txtOrderedByCountry>
         <txtOrderedByPhone>(123) 456-7890</txtOrderedByPhone>
         <txtOrderedByFax>(123) 456-7899</txtOrderedByFax>
         <txtOrderedByContactName>Contact Name</txtOrderedByContactName>
         <txtDeliverToCompanyName>Any Company Name</txtDeliverToCompanyName>
         <txtDeliverToAddress>7895, Any Street</txtDeliverToAddress>
         <txtDeliverToCity>Any City</txtDeliverToCity>
         <txtDeliverToStateProv>ST</txtDeliverToStateProv>
         <txtDeliverToZipCode>12346</txtDeliverToZipCode>
         <txtDeliverToCountry>Any Country</txtDeliverToCountry>
         <txtDeliverToPhone>(123) 456-7891</txtDeliverToPhone>
         <txtDeliverToFax>(123) 456-7899</txtDeliverToFax>
         <txtDeliverToContactName>Contact Name</txtDeliverToContactName>
     </header>
     <detail>
         <!-- A data subgroup that contains information about the monitor>
         <txtPartNum>00010-100</txtPartNum>
         <txtDescription>Monitor</txtDescription>
         <numQty>1</numQty>
         <numUnitPrice>350.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the desk lamp>
         <txtPartNum>00010-200</txtPartNum>
         <txtDescription>Desk lamps</txtDescription>
         <numQty>3</numQty>
         <numUnitPrice>55.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the Phone>
             <txtPartNum>00025-275</txtPartNum>
             <txtDescription>Phone</txtDescription>
             <numQty>5</numQty>
             <numUnitPrice>85.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the address book>
         <txtPartNum>00300-896</txtPartNum>
         <txtDescription>Address book</txtDescription>
         <numQty>2</numQty>
         <numUnitPrice>15.00</numUnitPrice>
     </detail>
```

Observe que cada subgrupo de datos contiene cuatro elementos XML que corresponden a esta información:

* Número de pieza de elementos
* Descripción de elementos
* Cantidad de artículos
* Precio unitario

El nombre del elemento XML principal de un subgrupo de datos debe coincidir con el nombre del subformulario ubicado en el diseño de formulario. Por ejemplo, en el diagrama anterior, observe que el nombre del elemento XML principal del subgrupo de datos es `detail`. Esto corresponde al nombre del subformulario ubicado en el diseño de formulario en el que se basa el formulario de orden de compra. Si el nombre del elemento XML principal del subgrupo de datos y el subformulario no coinciden, no se rellena previamente un formulario del lado del servidor.

Cada subgrupo de datos debe contener elementos XML que coincidan con los nombres de campo del subformulario. La variable `detail` subformulario ubicado en el diseño de formulario contiene los siguientes campos:

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>Si intenta rellenar previamente un formulario con un origen de datos que contenga elementos XML de repetición y establece la variable `RenderAtClient` a `No`, solo el primer registro de datos se combina en el formulario. Para asegurarse de que todos los registros de datos se combinan en el formulario, establezca la variable `RenderAtClient` a `Yes`. Para obtener información sobre la variable `RenderAtClient` , consulte [Representación de Forms en el cliente](/help/forms/developing/rendering-forms-client.md).

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para rellenar previamente un formulario con una presentación flexible, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un origen de datos XML en memoria.
1. Convierta el origen de datos XML.
1. Representar un formulario rellenado previamente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un origen de datos XML en memoria**

Puede usar `org.w3c.dom` clases para crear un origen de datos XML en memoria para cumplimentar previamente un formulario con una presentación flexible. Debe colocar los datos en un origen de datos XML que se ajuste al formulario. Para obtener información sobre la relación entre un formulario con presentación flexible y el origen de datos XML, consulte [Explicación de los subgrupos de datos](#understanding-data-subgroups).

**Convertir el origen de datos XML**

Un origen de datos XML en memoria que se crea mediante `org.w3c.dom` se pueden convertir en `com.adobe.idp.Document` antes de que se pueda utilizar para rellenar previamente un formulario. Se puede convertir un origen de datos XML en memoria mediante clases de transformación XML de Java.

>[!NOTE]
>
>Si utiliza el WSDL del servicio Forms para rellenar previamente un formulario, debe convertir un `org.w3c.dom.Document` en un `BLOB` objeto.

**Representar un formulario rellenado previamente**

Los formularios rellenados previamente se representan del mismo modo que los demás formularios. La única diferencia es que usa la variable `com.adobe.idp.Document` objeto que contiene el origen de datos XML para rellenar previamente el formulario.

**Consulte también lo siguiente**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderización de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Creación de aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Rellenado previo de formularios mediante la API de Java {#prepopulating-forms-using-the-java-api}

Para rellenar previamente un formulario con una presentación flexible mediante la API de Forms (Java), siga estos pasos:

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-forms-client.jar, en la ruta de clase de su proyecto Java. Para obtener información sobre la ubicación de estos archivos, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Crear un origen de datos XML en memoria

   * Creación de un Java `DocumentBuilderFactory` llamando al `DocumentBuilderFactory` class&quot; `newInstance` método.
   * Creación de un Java `DocumentBuilder` llamando al `DocumentBuilderFactory` del objeto `newDocumentBuilder` método.
   * Llame a la función `DocumentBuilder` del objeto `newDocument` para crear una instancia de `org.w3c.dom.Document` objeto.
   * Cree el elemento raíz del origen de datos XML invocando la variable `org.w3c.dom.Document` del objeto `createElement` método. Esto crea un `Element` objeto que representa el elemento raíz. Pase un valor de cadena que represente el nombre del elemento a la variable `createElement` método. Conversión del valor devuelto a `Element`. A continuación, anexe el elemento raíz al documento llamando a la función `Document` del objeto `appendChild` y pase el objeto de elemento raíz como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Cree el elemento de encabezado de la fuente de datos XML llamando a la función `Document` del objeto `createElement` método. Pase un valor de cadena que represente el nombre del elemento a la variable `createElement` método. Conversión del valor devuelto a `Element`. A continuación, anexe el elemento de encabezado al elemento raíz llamando a la función `root` del objeto `appendChild` y pase el objeto de elemento de encabezado como un argumento. Los elementos XML que se adjuntan al elemento de encabezado corresponden a la parte estática del formulario. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Cree un elemento secundario que pertenezca al elemento del encabezado llamando a la función `Document` del objeto `createElement` y pase un valor de cadena que represente el nombre del elemento. Conversión del valor devuelto a `Element`. A continuación, establezca un valor para el elemento secundario llamando a su `appendChild` y pase el `Document` del objeto `createTextNode` como argumento. Especifique un valor de cadena que aparezca como el valor del elemento secundario. Finalmente, anexe el elemento secundario al elemento del encabezado llamando al elemento del encabezado `appendChild` y pase el objeto de elemento secundario como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * Agregue todos los elementos restantes al elemento del encabezado repitiendo el último subpaso para cada campo que aparezca en la parte estática del formulario (en el diagrama de origen de datos XML, estos campos se muestran en la sección A. (Consulte [Explicación de los subgrupos de datos](#understanding-data-subgroups).)
   * Cree el elemento de detalle de la fuente de datos XML llamando a la función `Document` del objeto `createElement` método. Pase un valor de cadena que represente el nombre del elemento a la variable `createElement` método. Conversión del valor devuelto a `Element`. A continuación, anexe el elemento de detalle al elemento raíz llamando a la función `root` del objeto `appendChild` y pase el objeto detail element como argumento. Los elementos XML que se adjuntan al elemento detalle corresponden a la parte dinámica del formulario. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Cree un elemento secundario que pertenezca al elemento de detalle llamando a la función `Document` del objeto `createElement` y pase un valor de cadena que represente el nombre del elemento. Conversión del valor devuelto a `Element`. A continuación, establezca un valor para el elemento secundario llamando a su `appendChild` y pase el `Document` del objeto `createTextNode` como argumento. Especifique un valor de cadena que aparezca como el valor del elemento secundario. Finalmente, anexe el elemento secundario al elemento de detalle llamando al elemento de detalle `appendChild` y pase el objeto de elemento secundario como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Repita el último subpaso para todos los elementos XML que desee anexar al elemento detalle. Para crear correctamente el origen de datos XML utilizado para rellenar el formulario de orden de compra, debe añadir los siguientes elementos XML al elemento detalle: `txtDescription`, `numQty`y `numUnitPrice`.
   * Repita los dos últimos subpasos para todos los elementos de datos utilizados para rellenar previamente el formulario.

1. Convertir el origen de datos XML

   * Cree un `javax.xml.transform.Transformer` invocando el objeto `javax.xml.transform.Transformer` estático del objeto `newInstance` método.
   * Cree un `Transformer` invocando el objeto `TransformerFactory` del objeto `newTransformer` método.
   * Cree un `ByteArrayOutputStream` usando su constructor.
   * Cree un `javax.xml.transform.dom.DOMSource` usando su constructor y pasando el `org.w3c.dom.Document` objeto creado en el paso 1.
   * Cree un `javax.xml.transform.dom.DOMSource` usando su constructor y pasando el `ByteArrayOutputStream` objeto.
   * Rellenar el Java `ByteArrayOutputStream` invocando el objeto `javax.xml.transform.Transformer` del objeto `transform` y pasando el `javax.xml.transform.dom.DOMSource` y `javax.xml.transform.stream.StreamResult` objetos.
   * Cree una matriz de bytes y asigne el tamaño de la variable `ByteArrayOutputStream` a la matriz de bytes.
   * Rellene la matriz de bytes invocando la variable `ByteArrayOutputStream` del objeto `toByteArray` método.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando la matriz de bytes.

1. Representar un formulario rellenado previamente

   Invocar el `FormsServiceClient` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo.
   * A `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario. Asegúrese de usar la variable `com.adobe.idp.Document` objeto creado en los pasos uno y dos.
   * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución.
   * A `URLSpec` que contiene valores de URI necesarios para el servicio Forms.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   La variable `renderPDFForm` el método devuelve un `FormsResult` objeto que contiene un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

   * Cree un `javax.servlet.ServletOutputStream` objeto utilizado para enviar una secuencia de datos de formulario al explorador web del cliente.
   * Cree un `com.adobe.idp.Document` invocando el objeto `FormsResult` objeto ‘s `getOutputContent` método.
   * Cree un `java.io.InputStream` invocando el objeto `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Crear una matriz de bytes rellenarla con la secuencia de datos del formulario invocando la variable `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invocar el `javax.servlet.ServletOutputStream` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.


**Consulte también lo siguiente**

[Inicio rápido (modo SOAP): Rellenado previo de Forms con diseños flexibles mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rellenado previo de formularios mediante la API de servicio web {#prepopulating-forms-using-the-web-service-api}

Para rellenar previamente un formulario con una presentación flexible mediante la API de Forms (servicio web), siga estos pasos:

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms. (Consulte [Creación de clases de proxy Java mediante el eje Apache](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis).)
   * Incluya las clases proxy de Java en la ruta de clase.

1. Crear un origen de datos XML en memoria

   * Creación de un Java `DocumentBuilderFactory` llamando al `DocumentBuilderFactory` class&quot; `newInstance` método.
   * Creación de un Java `DocumentBuilder` llamando al `DocumentBuilderFactory` del objeto `newDocumentBuilder` método.
   * Llame a la función `DocumentBuilder` del objeto `newDocument` para crear una instancia de `org.w3c.dom.Document` objeto.
   * Cree el elemento raíz del origen de datos XML invocando la variable `org.w3c.dom.Document` del objeto `createElement` método. Esto crea un `Element` objeto que representa el elemento raíz. Pase un valor de cadena que represente el nombre del elemento a la variable `createElement` método. Conversión del valor devuelto a `Element`. A continuación, anexe el elemento raíz al documento llamando a la función `Document` del objeto `appendChild` y pase el objeto de elemento raíz como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Cree el elemento de encabezado de la fuente de datos XML llamando a la función `Document` del objeto `createElement` método. Pase un valor de cadena que represente el nombre del elemento a la variable `createElement` método. Conversión del valor devuelto a `Element`. A continuación, anexe el elemento de encabezado al elemento raíz llamando a la función `root` del objeto `appendChild` y pase el objeto de elemento de encabezado como un argumento. Los elementos XML que se adjuntan al elemento de encabezado corresponden a la parte estática del formulario. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Cree un elemento secundario que pertenezca al elemento del encabezado llamando a la función `Document` del objeto `createElement` y pase un valor de cadena que represente el nombre del elemento. Conversión del valor devuelto a `Element`. A continuación, establezca un valor para el elemento secundario llamando a su `appendChild` y pase el `Document` del objeto `createTextNode` como argumento. Especifique un valor de cadena que aparezca como el valor del elemento secundario. Finalmente, anexe el elemento secundario al elemento del encabezado llamando al elemento del encabezado `appendChild` y pase el objeto de elemento secundario como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * Agregue todos los elementos restantes al elemento del encabezado repitiendo el último subpaso para cada campo que aparezca en la parte estática del formulario (en el diagrama de origen de datos XML, estos campos se muestran en la sección A. (Consulte [Explicación de los subgrupos de datos](#understanding-data-subgroups).)
   * Cree el elemento de detalle de la fuente de datos XML llamando a la función `Document` del objeto `createElement` método. Pase un valor de cadena que represente el nombre del elemento a la variable `createElement` método. Conversión del valor devuelto a `Element`. A continuación, anexe el elemento de detalle al elemento raíz llamando a la función `root` del objeto `appendChild` y pase el objeto detail element como argumento. Los elementos XML que se adjuntan al elemento detalle corresponden a la parte dinámica del formulario. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Cree un elemento secundario que pertenezca al elemento de detalle llamando a la función `Document` del objeto `createElement` y pase un valor de cadena que represente el nombre del elemento. Conversión del valor devuelto a `Element`. A continuación, establezca un valor para el elemento secundario llamando a su `appendChild` y pase el `Document` del objeto `createTextNode` como argumento. Especifique un valor de cadena que aparezca como el valor del elemento secundario. Finalmente, anexe el elemento secundario al elemento de detalle llamando al elemento de detalle `appendChild` y pase el objeto de elemento secundario como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Repita el último subpaso para todos los elementos XML que desee anexar al elemento detalle. Para crear correctamente el origen de datos XML utilizado para rellenar el formulario de orden de compra, debe añadir los siguientes elementos XML al elemento detalle: `txtDescription`, `numQty`y `numUnitPrice`.
   * Repita los dos últimos subpasos para todos los elementos de datos utilizados para rellenar previamente el formulario.

1. Convertir el origen de datos XML

   * Cree un `javax.xml.transform.Transformer` invocando el objeto `javax.xml.transform.Transformer` estático del objeto `newInstance` método.
   * Cree un `Transformer` invocando el objeto `TransformerFactory` del objeto `newTransformer` método.
   * Cree un `ByteArrayOutputStream` usando su constructor.
   * Cree un `javax.xml.transform.dom.DOMSource` usando su constructor y pasando el `org.w3c.dom.Document` objeto creado en el paso 1.
   * Cree un `javax.xml.transform.dom.DOMSource` usando su constructor y pasando el `ByteArrayOutputStream` objeto.
   * Rellenar el Java `ByteArrayOutputStream` invocando el objeto `javax.xml.transform.Transformer` del objeto `transform` y pasando el `javax.xml.transform.dom.DOMSource` y `javax.xml.transform.stream.StreamResult` objetos.
   * Cree una matriz de bytes y asigne el tamaño de la variable `ByteArrayOutputStream` a la matriz de bytes.
   * Rellene la matriz de bytes invocando la variable `ByteArrayOutputStream` del objeto `toByteArray` método.
   * Cree un `BLOB` usando su constructor e invocando su `setBinaryData` y pase la matriz de bytes.

1. Representar un formulario rellenado previamente

   Invocar el `FormsService` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo.
   * A `BLOB` objeto que contiene datos para combinar con el formulario. Asegúrese de usar la variable `BLOB` objeto creado en los pasos uno y dos.
   * A `PDFFormRenderSpecc` que almacena opciones en tiempo de ejecución. Para obtener más información, consulte [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `URLSpec` que contiene valores de URI necesarios para el servicio Forms.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que rellena el método . Se utiliza para almacenar el formulario de PDF procesado.
   * Un vacío `javax.xml.rpc.holders.LongHolder` objeto que rellena el método . (Este argumento almacenará el número de páginas del formulario).
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el método . (Este argumento almacenará el valor de configuración regional).
   * Un vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   La variable `renderPDFForm` rellena el `com.adobe.idp.services.holders.FormsResultHolder` objeto que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

   * Cree un `FormResult` obteniendo el valor de `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value` miembro de datos.
   * Cree un `BLOB` objeto que contiene datos de formulario invocando la variable `FormsResult` del objeto `getOutputContent` método.
   * Obtenga el tipo de contenido de la variable `BLOB` invocando su `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasar el tipo de contenido de la variable `BLOB` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos del formulario en el explorador web del cliente invocando la variable `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree una matriz de bytes y rellénela invocando la variable `BLOB` del objeto `getBinaryData` método. Esta tarea asigna el contenido de la variable `FormsResult` a la matriz de bytes.
   * Invocar el `javax.servlet.http.HttpServletResponse` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.

   >[!NOTE]
   >
   >La variable `renderPDFForm` rellena el `com.adobe.idp.services.holders.FormsResultHolder` objeto que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
