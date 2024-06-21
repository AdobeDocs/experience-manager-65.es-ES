---
title: Agrupar varios fragmentos XDP
description: Ensamble varios fragmentos XDP en un único documento XDP mediante la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
docset: aem65
role: Developer
exl-id: 54d98c69-2b2e-46cb-9f6a-7e9bdbe5c378
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,  Document Services
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1859'
ht-degree: 0%

---

# Agrupar varios fragmentos XDP{#assembling-multiple-xdp-fragments}

Puede combinar varios fragmentos XDP en un único documento XDP. Por ejemplo, considere los fragmentos XDP en los que cada archivo XDP contiene uno o más subformularios utilizados para crear un formulario de mantenimiento. La siguiente ilustración muestra la vista Esquema (representa el archivo tuc018_template_flowed.xdp utilizado en el *Agrupar varios fragmentos XDP* inicio rápido):

![am_am_formato](assets/am_am_forma.png)

La siguiente ilustración muestra la sección del paciente (representa el archivo tuc018_contact.xdp utilizado en el *Agrupar varios fragmentos XDP* inicio rápido):

![am_am_form](assets/am_am_formb.png)

La siguiente ilustración muestra la sección de mantenimiento del paciente (representa el archivo tuc018_paciente.xdp utilizado en el *Agrupar varios fragmentos XDP* inicio rápido):

![am_am_formc](assets/am_am_formc.png)

Este fragmento contiene dos subformularios llamados *subPatientPhysical* y *subPatientHealth*. Se hace referencia a ambos subformularios en el documento DDX que se pasa al servicio Assembler. Con el servicio Assembler, puede combinar todos estos fragmentos XDP en un único documento XDP, como se muestra en la siguiente ilustración.

![am_am_form](assets/am_am_formd.png)

El siguiente documento DDX combina varios fragmentos XDP en un documento XDP.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <XDP result="tuc018result.xdp">
            <XDP source="tuc018_template_flowed.xdp">
             <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientPhysical" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientHealth" required="false"/>
            </XDP>
         </XDP>
 </DDX>
```

El documento DDX contiene un XDP `result` que especifica el nombre del resultado. En esta situación, el valor es `tuc018result.xdp`. Se hace referencia a este valor en la lógica de la aplicación que se utiliza para recuperar el documento XDP después de que el servicio Assembler devuelva el resultado. Por ejemplo, considere la siguiente lógica de aplicación Java que se utiliza para recuperar el documento XDP ensamblado (observe que el valor está en negrita):

```java
 //Iterate through the map object to retrieve the result XDP document
 for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
     // Retrieve the Map object’s value
     Map.Entry e = (Map.Entry)i.next();
     //Get the key name as specified in the
     //DDX document
     String keyName = (String)e.getKey();
     if (keyName.equalsIgnoreCase("tuc018result.xdp"))
                 {
         Object o = e.getValue();
         outDoc = (Document)o;
         //Save the result PDF file
         File myOutFile = new File("C:\\AssemblerResultXDP.xdp");
         outDoc.copyToFile(myOutFile);
     }
 }
```

El `XDP source` especifica el archivo XDP que representa un documento XDP completo que se puede utilizar como contenedor para agregar fragmentos XDP o como uno de varios documentos que se anexan juntos en orden. En este caso, el documento XDP se utiliza solo como contenedor (la primera ilustración se muestra en *Agrupar varios fragmentos XDP*). Es decir, los demás archivos XDP se colocan dentro del contenedor XDP.

Para cada subformulario, se puede agregar un `XDPContent` (este elemento es opcional). En el ejemplo anterior, observe que hay tres subformularios: `subPatientContact`, `subPatientPhysical`, y `subPatientHealth`. Tanto la `subPatientPhysical` subformulario y el `subPatientHealth` Los subformularios se encuentran en el mismo archivo XDP, tuc018_paciente.xdp. El elemento de fragmento especifica el nombre del subformulario, tal como se define en Designer.

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para montar varios fragmentos XDP, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDF Assembler.
1. Hacer referencia a un documento DDX existente.
1. Hacer referencia a los documentos XDP.
1. Establecer opciones en tiempo de ejecución.
1. Monte los distintos documentos XDP.
1. Recupere el documento XDP ensamblado.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

**Crear un cliente de PDF Assembler**

Para poder realizar mediante programación una operación de Assembler, cree un cliente de servicio Assembler.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para combinar varios documentos XDP. Este documento DDX debe contener `XDP result`, `XDP source`, y `XDPContent` elementos.

**Hacer referencia a los documentos XDP**

Para montar varios documentos XDP, haga referencia a todos los archivos XDP que se utilizan para montar el documento XDP resultante. Asegúrese de que el nombre del subformulario que contiene el documento XDP al que hace referencia el `source` se especifica en la variable `fragment` atributo. Se define un subformulario en Designer. Por ejemplo, considere el siguiente XML.

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

El subformulario denominado *subPatientContact* debe estar en el archivo XDP llamado *tuc018_contact.xdp*.

**Establecer opciones en tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlen el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede establecer una opción que indique al servicio Assembler que continúe procesando un trabajo si se produce un error.

**Montar los varios documentos XDP**

Para montar varios archivos XDP, llame al método `invokeDDX` operación. El servicio Assembler devuelve el documento XDP ensamblado dentro de un objeto de colección.

**Recuperar el documento XDP ensamblado**

Se devuelve un documento XDP ensamblado dentro de un objeto de colección. Itere por el objeto de colección y guarde el documento XDP como un archivo XDP. También puede pasar el documento XDP a otro servicio de AEM Forms, como Output.

**Consulte también**

[Combinar varios fragmentos XDP mediante la API de Java](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[Combinar varios fragmentos XDP mediante la API de servicio web](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[Creación de documentos de PDF mediante fragmentos](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Combinar varios fragmentos XDP mediante la API de Java {#assemble-multiple-xdp-fragments-using-the-java-api}

Ensamble varios fragmentos XDP utilizando la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de PDF Assembler.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `AssemblerServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Hacer referencia a un documento DDX existente.

   * Crear un `java.io.FileInputStream` que representa el documento DDX utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo DDX.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Hacer referencia a los documentos XDP.

   * Crear un `java.util.Map` que se utiliza para almacenar documentos XDP de entrada mediante una `HashMap` constructor.
   * Crear un `com.adobe.idp.Document` y pase el `java.io.FileInputStream` que contiene el archivo XDP de entrada (repita esta tarea para cada archivo XDP).
   * Añada una entrada a `java.util.Map` invocando su objeto `put` y pasando los siguientes argumentos:

      * Valor de cadena que representa el nombre de clave. Este valor debe coincidir con el de `source` valor de elemento especificado en el documento DDX (repita esta tarea para cada archivo XDP).
      * A `com.adobe.idp.Document` que contiene el documento XDP que corresponde a la variable `source` (repita esta tarea para cada archivo XDP).

1. Establecer las opciones en tiempo de ejecución.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca opciones en tiempo de ejecución para satisfacer sus necesidades empresariales invocando un método que pertenezca a `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque el `AssemblerOptionSpec` del objeto `setFailOnError` método y pase `false`.

1. Monte los distintos documentos XDP.

   Invoque el `AssemblerServiceClient` del objeto `invokeDDX` y pasar los siguientes valores obligatorios:

   * A `com.adobe.idp.Document` que representa el documento DDX a utilizar
   * A `java.util.Map` que contiene los archivos XDP de entrada
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución, incluida la fuente predeterminada y el nivel de registro de trabajo

   El `invokeDDX` El método devuelve un valor `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene el documento XDP ensamblado.

1. Recupere el documento XDP ensamblado.

   Para obtener el documento XDP ensamblado, realice las siguientes acciones:

   * Invoque el `AssemblerResult` del objeto `getDocuments` método. Este método devuelve un `java.util.Map` objeto.
   * Itere a través de `java.util.Map` hasta que encuentre el resultado `com.adobe.idp.Document` objeto.
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento XDP ensamblado.

**Consulte también**

[Agrupar varios fragmentos XDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[SOAP Inicio rápido (modo de): Agrupar varios fragmentos XDP mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Combinar varios fragmentos XDP mediante la API de servicio web {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Ensamble varios fragmentos XDP utilizando la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL al configurar una referencia de servicio:

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de PDF Assembler.

   * Crear un `AssemblerServiceClient` mediante su constructor predeterminado.
   * Crear un `AssemblerServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms, como `https://localhost:8080/soap/services/AssemblerService?blob=mtom`). No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio.
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `AssemblerServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario de los formularios de la a `AssemblerServiceClient.ClientCredentials.UserName.UserName` field.
      * Asigne el valor de contraseña correspondiente al `AssemblerServiceClient.ClientCredentials.UserName.Password`field.
      * Asigne el `HttpClientCredentialType.Basic` valor constante para `BasicHttpBindingSecurity.Transport.ClientCredentialType`field.
      * Asigne el `BasicHttpSecurityMode.TransportCredentialOnly` valor constante para `BasicHttpBindingSecurity.Security.Mode`field.

1. Hacer referencia a un documento DDX existente.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el documento DDX.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento DDX y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición inicial y la longitud de la secuencia a leer.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Hacer referencia a los documentos XDP.

   * Para cada archivo XDP de entrada, cree un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el archivo de entrada.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición inicial y la longitud de la secuencia a leer.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.
   * Crear un `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de colección se utiliza para almacenar los archivos de entrada necesarios para crear un documento XDP ensamblado.
   * Para cada archivo de entrada, cree un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Asigne un valor de cadena que represente el nombre de clave al `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` field. Este valor debe coincidir con el valor del elemento especificado en el documento DDX. (Realice esta tarea para cada archivo XDP de entrada).
   * Asigne el `BLOB` que almacena el archivo de entrada en el `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` field. (Realice esta tarea para cada archivo XDP de entrada).
   * Añada el `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto a `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invoque el `MyMapOf_xsd_string_To_xsd_anyType` del objeto `Add` y pase el `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Realice esta tarea para cada documento XDP de entrada).

1. Establecer opciones en tiempo de ejecución.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca las opciones en tiempo de ejecución para satisfacer sus necesidades empresariales asignando un valor a un miembro de datos que pertenezca a `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne a `false` a la `AssemblerOptionSpec` del objeto `failOnError` miembro de datos.

1. Monte los distintos documentos XDP.

   Invoque el `AssemblerServiceClient` del objeto `invokeDDX` y pasar los siguientes valores:

   * A `BLOB` que representa el documento DDX
   * El `MyMapOf_xsd_string_To_xsd_anyType` que contiene los archivos necesarios
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución

   El `invokeDDX` El método devuelve un `AssemblerResult` que contiene los resultados del trabajo y las excepciones que se han producido.

1. Recupere el documento XDP ensamblado.

   Para obtener el documento XDP recién creado, realice las siguientes acciones:

   * Acceda a la `AssemblerResult` del objeto `documents` , que es un `Map` que contiene los documentos de PDF resultantes.
   * Itere a través de `Map` para obtener cada documento resultante. A continuación, convierta el de ese miembro de la matriz `value` a un `BLOB`.
   * Extraiga los datos binarios que representan el documento PDF accediendo a su `BLOB` del objeto `MTOM` propiedad. Esto devuelve una matriz de bytes que puede escribir en un archivo XDP.

**Consulte también**

[Agrupar varios fragmentos XDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
