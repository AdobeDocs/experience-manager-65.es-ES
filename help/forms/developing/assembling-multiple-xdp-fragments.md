---
title: Agrupación de varios fragmentos XDP
seo-title: Agrupación de varios fragmentos XDP
description: Ensamble varios fragmentos XDP en un único documento XDP mediante la API de Java y la API de servicio web.
seo-description: Ensamble varios fragmentos XDP en un único documento XDP mediante la API de Java y la API de servicio web.
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 0%

---


# Montaje de varios fragmentos XDP{#assembling-multiple-xdp-fragments}

Puede ensamblar varios fragmentos XDP en un solo documento XDP. Por ejemplo, considere los fragmentos XDP donde cada archivo XDP contiene uno o más subformularios utilizados para crear un formulario de mantenimiento. La siguiente ilustración muestra la vista de esquema (representa el archivo tuc018_template_flowed.xdp utilizado en el *ensamblaje de varios fragmentos XDP* inicio rápido):

![am_am_forma](assets/am_am_forma.png)

La siguiente ilustración muestra la sección del paciente (representa el archivo tuc018_contact.xdp utilizado en el *ensamblaje de varios fragmentos XDP* inicio rápido):

![am_am_formb](assets/am_am_formb.png)

La siguiente ilustración muestra la sección de estado del paciente (representa el archivo tuc018_paciente.xdp utilizado en el *Ensamblado de varios fragmentos XDP* inicio rápido):

![am_am_formc](assets/am_am_formc.png)

Este fragmento contiene dos subformularios llamados *subPatientPhysical* y *subPatientHealth*. Se hace referencia a ambos subformularios en el documento DDX que se pasa al servicio Assembler. Con el servicio Assembler, puede combinar todos estos fragmentos XDP en un único documento XDP, como se muestra en la siguiente ilustración.

![am_am_formd](assets/am_am_formd.png)

El siguiente documento DDX integra varios fragmentos XDP en un documento XDP.

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

El documento DDX contiene una etiqueta XDP `result` que especifica el nombre del resultado. En esta situación, el valor es `tuc018result.xdp`. Se hace referencia a este valor en la lógica de aplicación que se utiliza para recuperar el documento XDP después de que el servicio Assembler devuelva el resultado. Por ejemplo, considere la siguiente lógica de aplicación Java que se utiliza para recuperar el documento XDP ensamblado (observe que el valor está en negrita):

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

La etiqueta `XDP source` especifica el archivo XDP que representa un documento XDP completo que puede utilizarse como contenedor para añadir fragmentos XDP o como uno de varios documentos que se anexan juntos en orden. En esta situación, el documento XDP solo se utiliza como contenedor (la primera ilustración que se muestra en *Agrupación de varios fragmentos XDP*). Es decir, los otros archivos XDP se colocan dentro del contenedor XDP.

Para cada subformulario, se puede añadir un elemento `XDPContent` (este elemento es opcional). En el ejemplo anterior, observe que hay tres subformularios: `subPatientContact`, `subPatientPhysical` y `subPatientHealth`. Tanto el subformulario `subPatientPhysical` como el subformulario `subPatientHealth` se encuentran en el mismo archivo XDP, tuc018_holder.xdp. El elemento de fragmento especifica el nombre del subformulario, tal como se define en Designer.

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para ensamblar varios fragmentos XDP, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente del ensamblador PDF.
1. Haga referencia a un documento DDX existente.
1. Haga referencia a los documentos XDP.
1. Establezca las opciones de tiempo de ejecución.
1. Ensamble los varios documentos XDP.
1. Recupere el documento XDP montado.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

**Crear un cliente de ensamblador PDF**

Antes de realizar una operación Assembler mediante programación, cree un cliente de servicio Assembler.

**Referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para ensamblar varios documentos XDP. Este documento DDX debe contener elementos `XDP result`, `XDP source` y `XDPContent`.

**Referencia a los documentos XDP**

Para ensamblar varios documentos XDP, haga referencia a todos los archivos XDP que se utilizan para ensamblar el documento XDP resultante. Asegúrese de que el nombre del subformulario contenido en el documento XDP al que hace referencia el atributo `source` se especifica en el atributo `fragment`. En Designer se define un subformulario. Por ejemplo, considere el siguiente XML.

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

El subformulario denominado *subPatientContact* debe encontrarse en el archivo XDP denominado *tuc018_contact.xdp*.

**Establecer opciones de tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlan el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Assembler que continúe procesando un trabajo si se encuentra un error.

**Montaje de varios documentos XDP**

Para ensamblar varios archivos XDP, llame a la operación `invokeDDX`. El servicio Assembler devuelve el documento XDP montado dentro de un objeto de colección.

**Recupere el documento XDP montado**

Un documento XDP montado se devuelve dentro de un objeto de colección. Iterar a través del objeto de colección y guardar el documento XDP como un archivo XDP. También puede pasar el documento XDP a otro servicio de AEM Forms, como Output.

**Consulte también**

[Agrupación de varios fragmentos XDP mediante la API de Java](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[Agrupar varios fragmentos XDP mediante la API de servicio web](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montaje programático de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[Creación de documentos PDF mediante fragmentos](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Ensamble varios fragmentos XDP con la API de Java {#assemble-multiple-xdp-fragments-using-the-java-api}

Ensamble varios fragmentos XDP utilizando la API de servicio de Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-assembler-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente del ensamblador PDF.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Haga referencia a un documento DDX existente.

   * Cree un objeto `java.io.FileInputStream` que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Haga referencia a los documentos XDP.

   * Cree un objeto `java.util.Map` que se utilice para almacenar documentos XDP de entrada mediante un constructor `HashMap`.
   * Cree un objeto `com.adobe.idp.Document` y pase el objeto `java.io.FileInputStream` que contiene el archivo XDP de entrada (repita esta tarea con cada archivo XDP).
   * Agregue una entrada al objeto `java.util.Map` invocando su método `put` y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento `source` especificado en el documento DDX (repita esta tarea con cada archivo XDP).
      * Un objeto `com.adobe.idp.Document` que contiene el documento XDP que corresponde al elemento `source` (repita esta tarea con cada archivo XDP).

1. Establezca las opciones de tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución empleando su constructor.
   * Defina las opciones en tiempo de ejecución para satisfacer los requisitos empresariales invocando un método que pertenece al objeto `AssemblerOptionSpec` . Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produce un error, invoque el método `AssemblerOptionSpec` del objeto `setFailOnError` y pase `false`.

1. Ensamble los varios documentos XDP.

   Invoque el método `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores obligatorios:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX que se va a utilizar
   * Un objeto `java.util.Map` que contiene los archivos XDP de entrada
   * Un objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones de tiempo de ejecución, incluidas la fuente predeterminada y el nivel de registro de trabajo

   El método `invokeDDX` devuelve un objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene el documento XDP ensamblado.

1. Recupere el documento XDP montado.

   Para obtener el documento XDP montado, realice las siguientes acciones:

   * Invoque el método `AssemblerResult` del objeto `getDocuments`. Este método devuelve un objeto `java.util.Map`.
   * Repita el objeto `java.util.Map` hasta que encuentre el objeto `com.adobe.idp.Document` resultante.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento XDP ensamblado.

**Consulte también**

[Montaje de varios ](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[fragmentos XDPInicio rápido (modo SOAP): Agrupación de varios fragmentos XDP mediante la ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[API de Java, incluidos los ](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[archivos de biblioteca Java de AEM FormsConfiguración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Agrupar varios fragmentos XDP mediante la API de servicio web {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Ensamble varios fragmentos XDP utilizando la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL al configurar una referencia de servicio:

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente del ensamblador PDF.

   * Cree un objeto `AssemblerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `AssemblerServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms, como `https://localhost:8080/soap/services/AssemblerService?blob=mtom`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `AssemblerServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName` .
      * Asigne el valor de contraseña correspondiente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor de constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor de constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un documento DDX existente.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento DDX.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento DDX y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia a los documentos XDP.

   * Para cada archivo XDP de entrada, cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el archivo de entrada.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.
   * Cree un objeto `MyMapOf_xsd_string_To_xsd_anyType`. Este objeto de colección se utiliza para almacenar los archivos de entrada necesarios para crear un documento XDP ensamblado.
   * Para cada archivo de entrada, cree un objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Asigne un valor de cadena que represente el nombre clave al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key`. Este valor debe coincidir con el valor del elemento especificado en el documento DDX. (Realice esta tarea para cada archivo XDP de entrada).
   * Asigne el objeto `BLOB` que almacena el archivo de entrada al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value`. (Realice esta tarea para cada archivo XDP de entrada).
   * Agregue el objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` al objeto `MyMapOf_xsd_string_To_xsd_anyType`. Invoque el método `MyMapOf_xsd_string_To_xsd_anyType` del objeto `Add` y pase el objeto `MyMapOf_xsd_string_To_xsd_anyType`. (Realice esta tarea para cada documento XDP de entrada).

1. Establezca las opciones de tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución empleando su constructor.
   * Defina las opciones en tiempo de ejecución para satisfacer los requisitos empresariales asignando un valor a un miembro de datos que pertenece al objeto `AssemblerOptionSpec`. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` al miembro de datos `AssemblerOptionSpec` del objeto `failOnError`.

1. Ensamble los varios documentos XDP.

   Invoque el método `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX
   * El objeto `MyMapOf_xsd_string_To_xsd_anyType` que contiene los archivos necesarios
   * Un objeto `AssemblerOptionSpec` que especifica opciones en tiempo de ejecución

   El método `invokeDDX` devuelve un objeto `AssemblerResult` que contiene los resultados del trabajo y cualquier excepción que se haya producido.

1. Recupere el documento XDP montado.

   Para obtener el documento XDP recién creado, realice las siguientes acciones:

   * Acceda al campo `AssemblerResult` del objeto `documents`, que es un objeto `Map` que contiene los documentos PDF resultantes.
   * Repita el objeto `Map` para obtener cada documento resultante. A continuación, convierta el `value` del miembro de la matriz en un `BLOB`.
   * Extraiga los datos binarios que representan el documento PDF accediendo a la propiedad `BLOB` del objeto `MTOM`. Esto devuelve una matriz de bytes que puede escribir en un archivo XDP.

**Consulte también**

[Agrupación de varios ](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[fragmentos XDPInvocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)