---
title: Rellenado previo de formularios con diseños de posición variable
seo-title: Rellenado previo de formularios con diseños de posición variable
description: nulo
seo-description: nulo
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Rellenado previo de formularios con diseños de posición variable {#prepopulating-forms-with-flowable-layouts1}

## Rellenado previo de formularios con diseños de posición variable {#prepopulating-forms-with-flowable-layouts2}

Al rellenar previamente los formularios, se muestran datos a los usuarios de un formulario procesado. Por ejemplo, supongamos que un usuario inicia sesión en un sitio web con un nombre de usuario y una contraseña. Si la autenticación se realiza correctamente, la aplicación cliente consulta una base de datos para obtener información del usuario. Los datos se combinan en el formulario y luego se procesa al usuario. Como resultado, el usuario puede ver datos personalizados dentro del formulario.

Rellenar un formulario de antemano tiene las siguientes ventajas:

* Permite al usuario ver datos personalizados en un formulario.
* Reduce la cantidad de escritura que el usuario realiza para rellenar un formulario.
* Asegura la integridad de los datos teniendo control sobre dónde se colocan los datos.

Los dos orígenes de datos XML siguientes pueden rellenar previamente un formulario:

* Origen de datos XDP, que es XML que se ajusta a la sintaxis XFA (o datos XFDF para rellenar previamente un formulario creado con Acrobat).
* Un origen de datos XML arbitrario que contiene pares nombre/valor que coinciden con los nombres de campo del formulario (los ejemplos de esta sección utilizan un origen de datos XML arbitrario).

Debe existir un elemento XML para cada campo de formulario que desee rellenar previamente. El nombre del elemento XML debe coincidir con el nombre del campo. Un elemento XML se omite si no se corresponde con un campo de formulario o si el nombre del elemento XML no coincide con el nombre del campo. No es necesario coincidir con el orden en que se muestran los elementos XML, siempre que se especifiquen todos los elementos XML.

Cuando se rellena previamente un formulario que ya contiene datos, se deben especificar los datos que ya se muestran en el origen de datos XML. Supongamos que un formulario que contiene 10 campos tiene datos en cuatro campos. A continuación, supongamos que desea rellenar previamente los seis campos restantes. En este caso, debe especificar 10 elementos XML en el origen de datos XML que se utiliza para rellenar previamente el formulario. Si sólo especifica seis elementos, los cuatro campos originales están vacíos.

Por ejemplo, puede rellenar previamente un formulario, como el formulario de confirmación de ejemplo. (Consulte &quot;Formulario de confirmación&quot; en [Representación de formularios]PDF interactivos(/help/forms/develop/procesing-forms-procesing-forms-interactive-pdf-forms-renderizado.md#procesado-interactivo-pdf-formularios).)

Para rellenar previamente el formulario de confirmación de ejemplo, debe crear un origen de datos XML que contenga tres elementos XML que coincidan con los tres campos del formulario. Este formulario contiene los tres campos siguientes: `FirstName`, `LastName`, y `Amount`. El primer paso es crear un origen de datos XML que contenga elementos XML que coincidan con los campos ubicados en el diseño de formulario. El paso siguiente es asignar valores de datos a los elementos XML, como se muestra en el siguiente código XML.

```as3
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

Después de rellenar previamente el formulario de confirmación con este origen de datos XML y, a continuación, procesar el formulario, se muestran los valores de datos asignados a los elementos XML, como se muestra en el diagrama siguiente.

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### Rellenado previo de formularios con diseños flexibles {#prepopulating_forms_with_flowable_layouts-1}

Los formularios con diseños flexibles son útiles para mostrar una cantidad indeterminada de datos a los usuarios. Dado que la presentación del formulario se ajusta automáticamente a la cantidad de datos que se combina, no es necesario predeterminar una presentación fija ni un número de páginas para el formulario, como se debe hacer con un formulario con presentación fija.

Un formulario suele rellenarse con datos obtenidos durante la ejecución. Como resultado, puede rellenar previamente un formulario creando un origen de datos XML en memoria y colocando los datos directamente en el origen de datos XML en memoria.

Considere una aplicación basada en la Web, como una tienda en línea. Una vez que un comprador en línea finaliza la compra de artículos, todos los artículos comprados se colocan en un origen de datos XML en memoria que se utiliza para rellenar previamente un formulario. El siguiente diagrama muestra este proceso, que se explica en la tabla que sigue al diagrama.

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
   <td><p>Una vez que el usuario termina de comprar elementos y hace clic en el botón Enviar, se crea un origen de datos XML en memoria. Los elementos comprados y la información del usuario se colocan en el origen de datos XML en memoria. </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>El origen de datos XML se utiliza para rellenar previamente un formulario de orden de compra (se muestra un ejemplo de este formulario después de esta tabla). </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>El formulario de orden de compra se procesa en el navegador web del cliente. </p></td>
  </tr>
 </tbody>
</table>

El diagrama siguiente muestra un ejemplo de un formulario de orden de compra. La información de la tabla se puede ajustar al número de registros de los datos XML.

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>Un formulario se puede rellenar previamente con datos de otras fuentes, como una base de datos de empresa o aplicaciones externas.

### Consideraciones sobre el diseño de formularios {#form-design-considerations}

Los formularios con diseños flexibles se basan en diseños de formulario creados en Designer. Un diseño de formulario especifica un conjunto de reglas de presentación, presentación y captura de datos, incluido el cálculo de valores en función de los datos introducidos por el usuario. Las reglas se aplican cuando se introducen datos en un formulario. Los campos que se agregan a un formulario son subformularios que están dentro del diseño de formulario. Por ejemplo, en el formulario de orden de compra que se muestra en el diagrama anterior, cada línea es un subformulario. Para obtener información sobre la creación de un diseño de formulario que contenga subformularios, consulte [Creación de un formulario de orden de compra con presentación](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9)flexible.

### Explicación de los subgrupos de datos {#understanding-data-subgroups}

Un origen de datos XML se utiliza para rellenar previamente formularios con diseños fijos y diseños flexibles. Sin embargo, la diferencia es que un origen de datos XML que rellena previamente un formulario con una presentación flexible contiene elementos XML repetitivos que se utilizan para rellenar previamente subformularios que se repiten dentro del formulario. Estos elementos XML de repetición se denominan subgrupos de datos.

Un origen de datos XML que se utiliza para rellenar previamente el formulario de orden de compra que se muestra en el diagrama anterior contiene cuatro subgrupos de datos de repetición. Cada subgrupo de datos corresponde a un artículo comprado. Los artículos comprados son un monitor, una lámpara de escritorio, un teléfono y una libreta de direcciones.

El siguiente origen de datos XML se utiliza para rellenar previamente el formulario de orden de compra.

```as3
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

* Número de artículo de elementos
* Descripción de elementos
* Cantidad de artículos
* Precio unitario

El nombre del elemento XML principal de un subgrupo de datos debe coincidir con el nombre del subformulario ubicado en el diseño de formulario. Por ejemplo, en el diagrama anterior, observe que el nombre del elemento XML principal del subgrupo de datos es `detail`. Corresponde al nombre del subformulario ubicado en el diseño de formulario en el que se basa el formulario de orden de compra. Si el nombre del elemento XML principal del subgrupo de datos y el subformulario no coinciden, no se rellena previamente un formulario del lado del servidor.

Cada subgrupo de datos debe contener elementos XML que coincidan con los nombres de campo del subformulario. El `detail` subformulario ubicado en el diseño de formulario contiene los campos siguientes:

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>Si intenta rellenar previamente un formulario con un origen de datos que contenga elementos XML de repetición y establece la `RenderAtClient` opción en `No`, solo se combinará el primer registro de datos en el formulario. Para asegurarse de que todos los registros de datos se combinan en el formulario, establezca el valor `RenderAtClient` en `Yes`. Para obtener información sobre la `RenderAtClient` opción, consulte [Representación de formularios en el cliente](/help/forms/developing/rendering-forms-client.md).

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para rellenar previamente un formulario con una presentación flexible, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un origen de datos XML en memoria.
1. Convierta el origen de datos XML.
1. Representar un formulario rellenado previamente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Crear un origen de datos XML en memoria**

Puede utilizar `org.w3c.dom` clases para crear un origen de datos XML en memoria para rellenar previamente un formulario con una presentación flexible. Debe colocar los datos en un origen de datos XML que se ajuste al formulario. Para obtener información sobre la relación entre un formulario con presentación flexible y el origen de datos XML, consulte [Explicación de los subgrupos]de datos (/help/forms/develop/procesing-forms-renderizado-formularios cumplimentados previamente-formularios-presentación-formularios-rellenados-formularios-variable-presentación-presentación-prerellenado.md#Understanding-data-subgrupos).

**Convertir el origen de datos XML**

Un origen de datos XML en memoria que se crea mediante `org.w3c.dom` clases se puede convertir en un `com.adobe.idp.Document` objeto antes de que se pueda utilizar para rellenar previamente un formulario. Un origen de datos XML en memoria se puede convertir mediante clases de transformación XML de Java.

>[!NOTE]
>
>Si utiliza el WSDL del servicio Forms para rellenar previamente un formulario, debe convertir un `org.w3c.dom.Document` objeto en un `BLOB` objeto.

**Representar un formulario rellenado previamente**

Un formulario precumplimentado se procesa como cualquier otro formulario. La única diferencia es que se utiliza el `com.adobe.idp.Document` objeto que contiene el origen de datos XML para rellenar previamente el formulario.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de formularios](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Representación de formularios PDF interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Creación de aplicaciones Web que procesan formularios](/help/forms/developing/creating-web-applications-renders-forms.md)

### Rellenado previo de formularios mediante la API de Java {#prepopulating-forms-using-the-java-api}

Para rellenar previamente un formulario con una presentación flexible mediante la API de formularios (Java), lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clases del proyecto Java. Para obtener información sobre la ubicación de estos archivos, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.

1. Crear un origen de datos XML en memoria

   * Cree un objeto Java `DocumentBuilderFactory` llamando al `DocumentBuilderFactory` método de la `newInstance` clase.
   * Cree un objeto Java `DocumentBuilder` llamando al `DocumentBuilderFactory` método `newDocumentBuilder` del objeto.
   * Llame al `DocumentBuilder` método del `newDocument` objeto para crear una instancia de un `org.w3c.dom.Document` objeto.
   * Cree el elemento raíz del origen de datos XML invocando el `org.w3c.dom.Document` método `createElement` del objeto. Esto crea un `Element` objeto que representa el elemento raíz. Pase un valor de cadena que represente el nombre del elemento al `createElement` método. Convierta el valor devuelto a `Element`. A continuación, anexe el elemento raíz al documento llamando al `Document` método `appendChild` del objeto y pase el objeto de elemento raíz como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Cree el elemento de encabezado del origen de datos XML llamando al `Document` método del `createElement` objeto. Pase un valor de cadena que represente el nombre del elemento al `createElement` método. Convierta el valor devuelto a `Element`. A continuación, anexe el elemento de encabezado al elemento raíz llamando al `root` método `appendChild` del objeto y pase el objeto de elemento de encabezado como argumento. Los elementos XML que se anexan al elemento de encabezado corresponden a la parte estática del formulario. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Cree un elemento secundario que pertenezca al elemento de encabezado llamando al `Document` método `createElement` del objeto y pase un valor de cadena que represente el nombre del elemento. Convierta el valor devuelto a `Element`. A continuación, establezca un valor para el elemento secundario llamando a su `appendChild` método y pase el `Document` método del `createTextNode` objeto como argumento. Especifique un valor de cadena que aparezca como el valor del elemento secundario. Finalmente, anexe el elemento secundario al elemento de encabezado llamando al método `appendChild` del elemento de encabezado y pase el objeto de elemento secundario como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * Agregue todos los elementos restantes al elemento de encabezado repitiendo el último subpaso de cada campo que aparezca en la parte estática del formulario (en el diagrama de origen de datos XML, estos campos se muestran en la sección A. (Consulte [Explicación de los subgrupos](#understanding-data-subgroups)de datos).
   * Cree el elemento detalle del origen de datos XML llamando al `Document` método del `createElement` objeto. Pase un valor de cadena que represente el nombre del elemento al `createElement` método. Convierta el valor devuelto a `Element`. A continuación, anexe el elemento detalle al elemento raíz llamando al `root` método `appendChild` del objeto y pase el objeto de elemento detalle como argumento. Los elementos XML que se anexan al elemento detalle corresponden a la parte dinámica del formulario. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Cree un elemento secundario que pertenezca al elemento detalle llamando al `Document` método `createElement` del objeto y pase un valor de cadena que represente el nombre del elemento. Convierta el valor devuelto a `Element`. A continuación, establezca un valor para el elemento secundario llamando a su `appendChild` método y pase el `Document` método del `createTextNode` objeto como argumento. Especifique un valor de cadena que aparezca como el valor del elemento secundario. Finalmente, anexe el elemento secundario al elemento detalle llamando al método `appendChild` del elemento detalle y pase el objeto secundario como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Repita el último subpaso para que todos los elementos XML se adjunten al elemento detalle. Para crear correctamente el origen de datos XML utilizado para rellenar el formulario de orden de compra, debe anexar los siguientes elementos XML al elemento detalle: `txtDescription`, `numQty`, y `numUnitPrice`.
   * Repita los dos últimos subpasos para todos los elementos de datos utilizados para rellenar previamente el formulario.

1. Convertir el origen de datos XML

   * Cree un `javax.xml.transform.Transformer` objeto invocando el `javax.xml.transform.Transformer` método estático `newInstance` del objeto.
   * Cree un `Transformer` objeto invocando el `TransformerFactory` método `newTransformer` del objeto.
   * Cree un `ByteArrayOutputStream` objeto con su constructor.
   * Cree un `javax.xml.transform.dom.DOMSource` objeto utilizando su constructor y pasando el `org.w3c.dom.Document` objeto que se creó en el paso 1.
   * Cree un `javax.xml.transform.dom.DOMSource` objeto utilizando su constructor y pasando el `ByteArrayOutputStream` objeto.
   * Rellene el objeto Java `ByteArrayOutputStream` invocando el método del `javax.xml.transform.Transformer` objeto y pasando los `transform` objetos `javax.xml.transform.dom.DOMSource` y `javax.xml.transform.stream.StreamResult` .
   * Cree una matriz de bytes y asigne el tamaño del `ByteArrayOutputStream` objeto a la matriz de bytes.
   * Rellene la matriz de bytes invocando el `ByteArrayOutputStream` método `toByteArray` del objeto.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando la matriz de bytes.

1. Representar un formulario rellenado previamente

   Invoque el `FormsServiceClient` método del `renderPDFForm` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo.
   * Un `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario. Asegúrese de utilizar el `com.adobe.idp.Document` objeto creado en los pasos uno y dos.
   * Un `PDFFormRenderSpec` objeto que almacena opciones de tiempo de ejecución.
   * Un `URLSpec` objeto que contiene valores de URI necesarios para el servicio Forms.
   * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   El `renderPDFForm` método devuelve un `FormsResult` objeto que contiene una secuencia de datos de formulario que se debe escribir en el explorador Web del cliente.

   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para enviar una secuencia de datos de formulario al navegador web del cliente.
   * Cree un `com.adobe.idp.Document` objeto invocando el `FormsResult` método ‘s `getOutputContent` .
   * Cree un `java.io.InputStream` objeto invocando el `com.adobe.idp.Document` método `getInputStream` del objeto.
   * Cree una matriz de bytes para rellenarla con la secuencia de datos del formulario invocando el `InputStream` método `read` del objeto y pasando la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .


**Consulte también**

[Inicio rápido (modo SOAP): Rellenado previo de formularios con diseños de posición variable mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rellenado previo de formularios mediante la API de servicio web {#prepopulating-forms-using-the-web-service-api}

Para rellenar previamente un formulario con una presentación flexible mediante la API de Forms (servicio Web), lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto

   * Cree clases proxy de Java que consuman el WSDL del servicio Forms. (Consulte [Creación de clases proxy de Java mediante Apache Axis](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis)).
   * Incluya las clases proxy de Java en la ruta de clases.

1. Crear un origen de datos XML en memoria

   * Cree un objeto Java `DocumentBuilderFactory` llamando al `DocumentBuilderFactory` método de la `newInstance` clase.
   * Cree un objeto Java `DocumentBuilder` llamando al `DocumentBuilderFactory` método `newDocumentBuilder` del objeto.
   * Llame al `DocumentBuilder` método del `newDocument` objeto para crear una instancia de un `org.w3c.dom.Document` objeto.
   * Cree el elemento raíz del origen de datos XML invocando el `org.w3c.dom.Document` método `createElement` del objeto. Esto crea un `Element` objeto que representa el elemento raíz. Pase un valor de cadena que represente el nombre del elemento al `createElement` método. Convierta el valor devuelto a `Element`. A continuación, anexe el elemento raíz al documento llamando al `Document` método `appendChild` del objeto y pase el objeto de elemento raíz como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Cree el elemento de encabezado del origen de datos XML llamando al `Document` método del `createElement` objeto. Pase un valor de cadena que represente el nombre del elemento al `createElement` método. Convierta el valor devuelto a `Element`. A continuación, anexe el elemento de encabezado al elemento raíz llamando al `root` método `appendChild` del objeto y pase el objeto de elemento de encabezado como argumento. Los elementos XML que se anexan al elemento de encabezado corresponden a la parte estática del formulario. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Cree un elemento secundario que pertenezca al elemento de encabezado llamando al `Document` método `createElement` del objeto y pase un valor de cadena que represente el nombre del elemento. Convierta el valor devuelto a `Element`. A continuación, establezca un valor para el elemento secundario llamando a su `appendChild` método y pase el `Document` método del `createTextNode` objeto como argumento. Especifique un valor de cadena que aparezca como el valor del elemento secundario. Finalmente, anexe el elemento secundario al elemento de encabezado llamando al método `appendChild` del elemento de encabezado y pase el objeto de elemento secundario como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * Agregue todos los elementos restantes al elemento de encabezado repitiendo el último subpaso de cada campo que aparezca en la parte estática del formulario (en el diagrama de origen de datos XML, estos campos se muestran en la sección A. (Consulte [Explicación de los subgrupos](#understanding-data-subgroups)de datos).
   * Cree el elemento detalle del origen de datos XML llamando al `Document` método del `createElement` objeto. Pase un valor de cadena que represente el nombre del elemento al `createElement` método. Convierta el valor devuelto a `Element`. A continuación, anexe el elemento detalle al elemento raíz llamando al `root` método `appendChild` del objeto y pase el objeto de elemento detalle como argumento. Los elementos XML que se anexan al elemento detalle corresponden a la parte dinámica del formulario. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Cree un elemento secundario que pertenezca al elemento detalle llamando al `Document` método `createElement` del objeto y pase un valor de cadena que represente el nombre del elemento. Convierta el valor devuelto a `Element`. A continuación, establezca un valor para el elemento secundario llamando a su `appendChild` método y pase el `Document` método del `createTextNode` objeto como argumento. Especifique un valor de cadena que aparezca como el valor del elemento secundario. Finalmente, anexe el elemento secundario al elemento detalle llamando al método `appendChild` del elemento detalle y pase el objeto secundario como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Repita el último subpaso para que todos los elementos XML se adjunten al elemento detalle. Para crear correctamente el origen de datos XML utilizado para rellenar el formulario de orden de compra, debe anexar los siguientes elementos XML al elemento detalle: `txtDescription`, `numQty`, y `numUnitPrice`.
   * Repita los dos últimos subpasos para todos los elementos de datos utilizados para rellenar previamente el formulario.

1. Convertir el origen de datos XML

   * Cree un `javax.xml.transform.Transformer` objeto invocando el `javax.xml.transform.Transformer` método estático `newInstance` del objeto.
   * Cree un `Transformer` objeto invocando el `TransformerFactory` método `newTransformer` del objeto.
   * Cree un `ByteArrayOutputStream` objeto con su constructor.
   * Cree un `javax.xml.transform.dom.DOMSource` objeto utilizando su constructor y pasando el `org.w3c.dom.Document` objeto que se creó en el paso 1.
   * Cree un `javax.xml.transform.dom.DOMSource` objeto utilizando su constructor y pasando el `ByteArrayOutputStream` objeto.
   * Rellene el objeto Java `ByteArrayOutputStream` invocando el método del `javax.xml.transform.Transformer` objeto y pasando los `transform` objetos `javax.xml.transform.dom.DOMSource` y `javax.xml.transform.stream.StreamResult` .
   * Cree una matriz de bytes y asigne el tamaño del `ByteArrayOutputStream` objeto a la matriz de bytes.
   * Rellene la matriz de bytes invocando el `ByteArrayOutputStream` método `toByteArray` del objeto.
   * Cree un `BLOB` objeto utilizando su constructor e invoque su `setBinaryData` método y pase la matriz de bytes.

1. Representar un formulario rellenado previamente

   Invoque el `FormsService` método del `renderPDFForm` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo.
   * Un `BLOB` objeto que contiene datos para combinar con el formulario. Asegúrese de utilizar el `BLOB` objeto que se creó en los pasos uno y dos.
   * Un `PDFFormRenderSpecc` objeto que almacena opciones de tiempo de ejecución. Para obtener más información, consulte [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Un `URLSpec` objeto que contiene valores de URI necesarios para el servicio Forms.
   * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el método . Se utiliza para almacenar el formulario PDF procesado.
   * Objeto vacío `javax.xml.rpc.holders.LongHolder` que se rellena con el método . (Este argumento almacenará el número de páginas del formulario).
   * Objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el método . (Este argumento almacenará el valor de configuración regional).
   * Un `com.adobe.idp.services.holders.FormsResultHolder` objeto vacío que contendrá los resultados de esta operación.
   El `renderPDFForm` método rellena el `com.adobe.idp.services.holders.FormsResultHolder` objeto que se pasa como el último valor de argumento con una secuencia de datos de formulario que se debe escribir en el explorador Web del cliente.

   * Cree un `FormResult` objeto obteniendo el valor del `com.adobe.idp.services.holders.FormsResultHolder` miembro de `value` datos del objeto.
   * Cree un `BLOB` objeto que contenga datos de formulario invocando el `FormsResult` método `getOutputContent` del objeto.
   * Obtenga el tipo de contenido del `BLOB` objeto invocando su `getContentType` método.
   * Defina el tipo de contenido del `javax.servlet.http.HttpServletResponse` objeto invocando su `setContentType` método y pasando el tipo de contenido del `BLOB` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el `javax.servlet.http.HttpServletResponse` método `getOutputStream` del objeto.
   * Cree una matriz de bytes y rellénela invocando el `BLOB` método `getBinaryData` del objeto. Esta tarea asigna el contenido del `FormsResult` objeto a la matriz de bytes.
   * Invoque el `javax.servlet.http.HttpServletResponse` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .
   >[!NOTE]
   >
   >El `renderPDFForm` método rellena el `com.adobe.idp.services.holders.FormsResultHolder` objeto que se pasa como el último valor de argumento con una secuencia de datos de formulario que se debe escribir en el explorador Web del cliente.

**Consulte también**

[Invocación de formularios AEM con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

