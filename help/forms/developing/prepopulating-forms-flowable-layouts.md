---
title: Rellenado previo de Forms con diseños flexibles
seo-title: Rellenado previo de Forms con diseños flexibles
description: Rellene previamente los formularios con una presentación flexible para mostrar los datos a los usuarios de un formulario procesado con la API de Java y la API de servicio web.
seo-description: Rellene previamente los formularios con una presentación flexible para mostrar los datos a los usuarios de un formulario procesado con la API de Java y la API de servicio web.
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
role: Desarrollador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3534'
ht-degree: 0%

---


# Rellenado previo de Forms con diseños de posición variable {#prepopulating-forms-with-flowable-layouts1}

## Rellenado previo de Forms con diseños de posición variable {#prepopulating-forms-with-flowable-layouts2}

Al cumplimentar los formularios de antemano, se muestran datos a los usuarios de un formulario procesado. Por ejemplo, supongamos que un usuario inicia sesión en un sitio web con un nombre de usuario y una contraseña. Si la autenticación se realiza correctamente, la aplicación cliente consulta una base de datos para obtener información del usuario. Los datos se combinan en el formulario y se procesan para el usuario. Como resultado, el usuario puede ver datos personalizados dentro del formulario.

Cumplimentar previamente un formulario tiene las siguientes ventajas:

* Permite al usuario ver datos personalizados en un formulario.
* Reduce la cantidad de escritura que el usuario hace para rellenar un formulario.
* Asegura la integridad de los datos teniendo control sobre dónde se colocan los datos.

Los dos orígenes de datos XML siguientes pueden rellenar previamente un formulario:

* Un origen de datos XDP, que es XML que se ajusta a la sintaxis XFA (o datos XFDF para rellenar previamente un formulario creado con Acrobat).
* Un origen de datos XML arbitrario que contiene pares de nombre/valor que coinciden con los nombres de campo del formulario (los ejemplos de esta sección utilizan un origen de datos XML arbitrario).

Debe existir un elemento XML para cada campo de formulario que desee rellenar previamente. El nombre del elemento XML debe coincidir con el nombre del campo. Se omite un elemento XML si no se corresponde con un campo de formulario o si el nombre del elemento XML no coincide con el nombre del campo. No es necesario coincidir con el orden en que se muestran los elementos XML, siempre y cuando se especifiquen todos los elementos XML.

Cuando rellene previamente un formulario que ya contenga datos, debe especificar los datos que ya se muestran en el origen de datos XML. Supongamos que un formulario que contiene 10 campos tiene datos en cuatro campos. A continuación, suponga que desea rellenar previamente los seis campos restantes. En este caso, debe especificar 10 elementos XML en el origen de datos XML que se utiliza para rellenar previamente el formulario. Si especifica solo seis elementos, los cuatro campos originales están vacíos.

Por ejemplo, puede rellenar previamente un formulario, como el formulario de confirmación de ejemplo. (Consulte &quot;Formulario de confirmación&quot; en [Representación de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)).

Para rellenar previamente el formulario de confirmación de ejemplo, debe crear un origen de datos XML que contenga tres elementos XML que coincidan con los tres campos del formulario. Este formulario contiene los tres campos siguientes: `FirstName`, `LastName` y `Amount`. El primer paso es crear un origen de datos XML que contenga elementos XML que coincidan con los campos ubicados en el diseño de formulario. El siguiente paso es asignar valores de datos a los elementos XML, como se muestra en el siguiente código XML.

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

### Consideraciones sobre el diseño de formulario {#form-design-considerations}

Forms con diseños flexibles se basa en diseños de formulario creados en Designer. Un diseño de formulario especifica un conjunto de reglas de presentación, presentación y captura de datos, incluido el cálculo de valores en función de los datos introducidos por el usuario. Las reglas se aplican cuando se introducen datos en un formulario. Los campos que se agregan a un formulario son subformularios que se encuentran dentro del diseño de formulario. Por ejemplo, en el formulario de orden de compra que se muestra en el diagrama anterior, cada línea es un subformulario. Para obtener información sobre la creación de un diseño de formulario que contenga subformularios, consulte [Creación de un formulario de orden de compra con presentación flexible](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9).

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

Cada subgrupo de datos debe contener elementos XML que coincidan con los nombres de campo del subformulario. El subformulario `detail` ubicado en el diseño de formulario contiene los siguientes campos:

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>Si intenta rellenar previamente un formulario con un origen de datos que contenga elementos XML de repetición y establece la opción `RenderAtClient` en `No`, solo se combinará el primer registro de datos en el formulario. Para asegurarse de que todos los registros de datos se combinan en el formulario, establezca `RenderAtClient` en `Yes`. Para obtener información sobre la opción `RenderAtClient`, consulte [Rendering Forms at the Client](/help/forms/developing/rendering-forms-client.md).

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

Puede utilizar clases `org.w3c.dom` para crear un origen de datos XML en memoria para rellenar previamente un formulario con una presentación flexible. Debe colocar los datos en un origen de datos XML que se ajuste al formulario. Para obtener información sobre la relación entre un formulario con presentación flexible y el origen de datos XML, consulte [Explicación de los subgrupos de datos](#understanding-data-subgroups).

**Convertir el origen de datos XML**

Un origen de datos XML en memoria que se crea mediante clases `org.w3c.dom` se puede convertir en un objeto `com.adobe.idp.Document` antes de que se pueda utilizar para rellenar previamente un formulario. Se puede convertir un origen de datos XML en memoria mediante clases de transformación XML de Java.

>[!NOTE]
>
>Si utiliza el WSDL del servicio Forms para rellenar previamente un formulario, debe convertir un objeto `org.w3c.dom.Document` en un objeto `BLOB`.

**Representar un formulario rellenado previamente**

Los formularios rellenados previamente se representan del mismo modo que los demás formularios. La única diferencia es que se utiliza el objeto `com.adobe.idp.Document` que contiene el origen de datos XML para rellenar previamente el formulario.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderización de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Creación de aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Rellenado previo de formularios con la API de Java {#prepopulating-forms-using-the-java-api}

Para rellenar previamente un formulario con una presentación flexible mediante la API de Forms (Java), siga estos pasos:

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-forms-client.jar, en la ruta de clase de su proyecto Java. Para obtener información sobre la ubicación de estos archivos, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Crear un origen de datos XML en memoria

   * Cree un objeto Java `DocumentBuilderFactory` llamando al método `DocumentBuilderFactory` class’ `newInstance` .
   * Cree un objeto Java `DocumentBuilder` llamando al método `DocumentBuilderFactory` del objeto `newDocumentBuilder` .
   * Llame al método `DocumentBuilder` del objeto `newDocument` para crear una instancia de un objeto `org.w3c.dom.Document`.
   * Cree el elemento raíz del origen de datos XML invocando el método `org.w3c.dom.Document` del objeto `createElement` . Esto crea un objeto `Element` que representa el elemento raíz. Pase un valor de cadena que represente el nombre del elemento al método `createElement` . Establezca el valor devuelto en `Element`. A continuación, anexe el elemento raíz al documento llamando al método `Document` del objeto `appendChild` y pase el objeto raíz del elemento como un argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Cree el elemento de encabezado del origen de datos XML llamando al método `Document` del objeto `createElement` . Pase un valor de cadena que represente el nombre del elemento al método `createElement` . Establezca el valor devuelto en `Element`. A continuación, anexe el elemento del encabezado al elemento raíz llamando al método `root` del objeto `appendChild` y pase el objeto del elemento del encabezado como un argumento. Los elementos XML que se adjuntan al elemento de encabezado corresponden a la parte estática del formulario. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Cree un elemento secundario que pertenezca al elemento del encabezado llamando al método `Document` del objeto `createElement` y pase un valor de cadena que represente el nombre del elemento. Establezca el valor devuelto en `Element`. A continuación, establezca un valor para el elemento secundario llamando a su método `appendChild` y pasando el método `Document` del objeto `createTextNode` como argumento. Especifique un valor de cadena que aparezca como el valor del elemento secundario. Finalmente, anexe el elemento secundario al elemento del encabezado llamando al método `appendChild` del elemento del encabezado y pase el objeto del elemento secundario como un argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * Agregue todos los elementos restantes al elemento del encabezado repitiendo el último subpaso para cada campo que aparezca en la parte estática del formulario (en el diagrama de origen de datos XML, estos campos se muestran en la sección A. (Consulte [Explicación de los subgrupos de datos](#understanding-data-subgroups)).
   * Cree el elemento detalle del origen de datos XML llamando al método `Document` del objeto `createElement` . Pase un valor de cadena que represente el nombre del elemento al método `createElement` . Establezca el valor devuelto en `Element`. A continuación, anexe el elemento de detalle al elemento raíz llamando al método `root` del objeto `appendChild` y pase el objeto de elemento de detalle como un argumento. Los elementos XML que se adjuntan al elemento detalle corresponden a la parte dinámica del formulario. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Cree un elemento secundario que pertenezca al elemento de detalle llamando al método `Document` del objeto `createElement` y pase un valor de cadena que represente el nombre del elemento. Establezca el valor devuelto en `Element`. A continuación, establezca un valor para el elemento secundario llamando a su método `appendChild` y pasando el método `Document` del objeto `createTextNode` como argumento. Especifique un valor de cadena que aparezca como el valor del elemento secundario. Finalmente, anexe el elemento secundario al elemento detalle llamando al método `appendChild` del elemento de detalle y pase el objeto del elemento secundario como un argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Repita el último subpaso para todos los elementos XML que desee anexar al elemento detalle. Para crear correctamente el origen de datos XML utilizado para rellenar el formulario de orden de compra, debe añadir los siguientes elementos XML al elemento detalle: `txtDescription`, `numQty` y `numUnitPrice`.
   * Repita los dos últimos subpasos para todos los elementos de datos utilizados para rellenar previamente el formulario.

1. Convertir el origen de datos XML

   * Cree un objeto `javax.xml.transform.Transformer` invocando el método estático `javax.xml.transform.Transformer` del objeto `newInstance`.
   * Cree un objeto `Transformer` invocando el método `TransformerFactory` del objeto `newTransformer`.
   * Cree un objeto `ByteArrayOutputStream` utilizando su constructor.
   * Cree un objeto `javax.xml.transform.dom.DOMSource` utilizando su constructor y pasando el objeto `org.w3c.dom.Document` creado en el paso 1.
   * Cree un objeto `javax.xml.transform.dom.DOMSource` utilizando su constructor y pasando el objeto `ByteArrayOutputStream`.
   * Rellene el objeto Java `ByteArrayOutputStream` invocando el método `javax.xml.transform.Transformer` del objeto `transform` y pasando los objetos `javax.xml.transform.dom.DOMSource` y `javax.xml.transform.stream.StreamResult`.
   * Cree una matriz de bytes y asigne el tamaño del objeto `ByteArrayOutputStream` a la matriz de bytes.
   * Rellene la matriz de bytes invocando el método `ByteArrayOutputStream` del objeto `toByteArray`.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando la matriz de bytes.

1. Representar un formulario rellenado previamente

   Invoque el método `FormsServiceClient` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo.
   * Un objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Asegúrese de utilizar el objeto `com.adobe.idp.Document` creado en los pasos uno y dos.
   * Un objeto `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución.
   * Un objeto `URLSpec` que contiene valores de URI necesarios para el servicio Forms.
   * Un objeto `java.util.HashMap` que almacena archivos adjuntos. Se trata de un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `renderPDFForm` devuelve un objeto `FormsResult` que contiene un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para enviar una secuencia de datos de formulario al explorador web del cliente.
   * Cree un objeto `com.adobe.idp.Document` invocando el método `FormsResult` del objeto ‘s `getOutputContent`.
   * Cree un objeto `java.io.InputStream` invocando el método `com.adobe.idp.Document` del objeto `getInputStream`.
   * Cree una matriz de bytes rellénela con la secuencia de datos del formulario invocando el método `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invoque el método `javax.servlet.ServletOutputStream` del objeto `write` para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.


**Consulte también**

[Inicio rápido (modo SOAP): Rellenado previo de Forms con diseños flexibles mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rellenado previo de formularios mediante la API de servicio web {#prepopulating-forms-using-the-web-service-api}

Para rellenar previamente un formulario con una presentación flexible mediante la API de Forms (servicio web), siga estos pasos:

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms. (Consulte [Creación de clases de proxy Java mediante el eje Apache](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis)).
   * Incluya las clases proxy de Java en la ruta de clase.

1. Crear un origen de datos XML en memoria

   * Cree un objeto Java `DocumentBuilderFactory` llamando al método `DocumentBuilderFactory` class’ `newInstance` .
   * Cree un objeto Java `DocumentBuilder` llamando al método `DocumentBuilderFactory` del objeto `newDocumentBuilder` .
   * Llame al método `DocumentBuilder` del objeto `newDocument` para crear una instancia de un objeto `org.w3c.dom.Document`.
   * Cree el elemento raíz del origen de datos XML invocando el método `org.w3c.dom.Document` del objeto `createElement` . Esto crea un objeto `Element` que representa el elemento raíz. Pase un valor de cadena que represente el nombre del elemento al método `createElement` . Establezca el valor devuelto en `Element`. A continuación, anexe el elemento raíz al documento llamando al método `Document` del objeto `appendChild` y pase el objeto raíz del elemento como un argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Cree el elemento de encabezado del origen de datos XML llamando al método `Document` del objeto `createElement` . Pase un valor de cadena que represente el nombre del elemento al método `createElement` . Establezca el valor devuelto en `Element`. A continuación, anexe el elemento del encabezado al elemento raíz llamando al método `root` del objeto `appendChild` y pase el objeto del elemento del encabezado como un argumento. Los elementos XML que se adjuntan al elemento de encabezado corresponden a la parte estática del formulario. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Cree un elemento secundario que pertenezca al elemento del encabezado llamando al método `Document` del objeto `createElement` y pase un valor de cadena que represente el nombre del elemento. Establezca el valor devuelto en `Element`. A continuación, establezca un valor para el elemento secundario llamando a su método `appendChild` y pasando el método `Document` del objeto `createTextNode` como argumento. Especifique un valor de cadena que aparezca como el valor del elemento secundario. Finalmente, anexe el elemento secundario al elemento del encabezado llamando al método `appendChild` del elemento del encabezado y pase el objeto del elemento secundario como un argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * Agregue todos los elementos restantes al elemento del encabezado repitiendo el último subpaso para cada campo que aparezca en la parte estática del formulario (en el diagrama de origen de datos XML, estos campos se muestran en la sección A. (Consulte [Explicación de los subgrupos de datos](#understanding-data-subgroups)).
   * Cree el elemento detalle del origen de datos XML llamando al método `Document` del objeto `createElement` . Pase un valor de cadena que represente el nombre del elemento al método `createElement` . Establezca el valor devuelto en `Element`. A continuación, anexe el elemento de detalle al elemento raíz llamando al método `root` del objeto `appendChild` y pase el objeto de elemento de detalle como un argumento. Los elementos XML que se adjuntan al elemento detalle corresponden a la parte dinámica del formulario. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Cree un elemento secundario que pertenezca al elemento de detalle llamando al método `Document` del objeto `createElement` y pase un valor de cadena que represente el nombre del elemento. Establezca el valor devuelto en `Element`. A continuación, establezca un valor para el elemento secundario llamando a su método `appendChild` y pasando el método `Document` del objeto `createTextNode` como argumento. Especifique un valor de cadena que aparezca como el valor del elemento secundario. Finalmente, anexe el elemento secundario al elemento detalle llamando al método `appendChild` del elemento de detalle y pase el objeto del elemento secundario como un argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Repita el último subpaso para todos los elementos XML que desee anexar al elemento detalle. Para crear correctamente el origen de datos XML utilizado para rellenar el formulario de orden de compra, debe añadir los siguientes elementos XML al elemento detalle: `txtDescription`, `numQty` y `numUnitPrice`.
   * Repita los dos últimos subpasos para todos los elementos de datos utilizados para rellenar previamente el formulario.

1. Convertir el origen de datos XML

   * Cree un objeto `javax.xml.transform.Transformer` invocando el método estático `javax.xml.transform.Transformer` del objeto `newInstance`.
   * Cree un objeto `Transformer` invocando el método `TransformerFactory` del objeto `newTransformer`.
   * Cree un objeto `ByteArrayOutputStream` utilizando su constructor.
   * Cree un objeto `javax.xml.transform.dom.DOMSource` utilizando su constructor y pasando el objeto `org.w3c.dom.Document` creado en el paso 1.
   * Cree un objeto `javax.xml.transform.dom.DOMSource` utilizando su constructor y pasando el objeto `ByteArrayOutputStream`.
   * Rellene el objeto Java `ByteArrayOutputStream` invocando el método `javax.xml.transform.Transformer` del objeto `transform` y pasando los objetos `javax.xml.transform.dom.DOMSource` y `javax.xml.transform.stream.StreamResult`.
   * Cree una matriz de bytes y asigne el tamaño del objeto `ByteArrayOutputStream` a la matriz de bytes.
   * Rellene la matriz de bytes invocando el método `ByteArrayOutputStream` del objeto `toByteArray`.
   * Cree un objeto `BLOB` utilizando su constructor, invoque su método `setBinaryData` y pase la matriz de bytes.

1. Representar un formulario rellenado previamente

   Invoque el método `FormsService` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo.
   * Un objeto `BLOB` que contiene datos para combinar con el formulario. Asegúrese de utilizar el objeto `BLOB` que se creó en los pasos uno y dos.
   * Un objeto `PDFFormRenderSpecc` que almacena opciones en tiempo de ejecución. Para obtener más información, consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Un objeto `URLSpec` que contiene valores de URI necesarios para el servicio Forms.
   * Un objeto `java.util.HashMap` que almacena archivos adjuntos. Se trata de un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un objeto `com.adobe.idp.services.holders.BLOBHolder` vacío que se rellena con el método . Se utiliza para almacenar el formulario PDF procesado.
   * Un objeto `javax.xml.rpc.holders.LongHolder` vacío que se rellena con el método . (Este argumento almacenará el número de páginas del formulario).
   * Un objeto `javax.xml.rpc.holders.StringHolder` vacío que se rellena con el método . (Este argumento almacenará el valor de configuración regional).
   * Un objeto `com.adobe.idp.services.holders.FormsResultHolder` vacío que contendrá los resultados de esta operación.

   El método `renderPDFForm` rellena el objeto `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

   * Cree un objeto `FormResult` obteniendo el valor del miembro de datos `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value`.
   * Cree un objeto `BLOB` que contenga datos de formulario invocando el método `FormsResult` del objeto `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `BLOB` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `BLOB`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir el flujo de datos del formulario en el explorador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData`. Esta tarea asigna el contenido del objeto `FormsResult` a la matriz de bytes.
   * Invoque el método `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

   >[!NOTE]
   >
   >El método `renderPDFForm` rellena el objeto `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

**Consulte también**

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

