---
title: Agrupación de varios fragmentos XDP
seo-title: Assembling Multiple XDP Fragments
description: Ensamble varios fragmentos XDP en un único documento XDP con la API de Java y la API de servicio web.
seo-description: Assemble multiple XDP fragments into a single XDP document using the Java API and Web Service API.
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
role: Developer
exl-id: 54d98c69-2b2e-46cb-9f6a-7e9bdbe5c378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 0%

---

# Agrupación de varios fragmentos XDP{#assembling-multiple-xdp-fragments}

Puede ensamblar varios fragmentos XDP en un solo documento XDP. Por ejemplo, considere los fragmentos XDP donde cada archivo XDP contiene uno o más subformularios utilizados para crear un formulario de mantenimiento. La siguiente ilustración muestra la vista Esquema (representa el archivo tuc018_template_flowed.xdp utilizado en la *Agrupación de varios fragmentos XDP* inicio rápido):

![am_am_forma](assets/am_am_forma.png)

La siguiente ilustración muestra la sección del paciente (representa el archivo tuc018_contact.xdp utilizado en la variable *Agrupación de varios fragmentos XDP* inicio rápido):

![am_am_formb](assets/am_am_formb.png)

La siguiente ilustración muestra la sección de salud del paciente (representa el archivo tuc018_paciente.xdp utilizado en la variable *Agrupación de varios fragmentos XDP* inicio rápido):

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

El documento DDX contiene un XDP `result` que especifica el nombre del resultado. En esta situación, el valor es `tuc018result.xdp`. Se hace referencia a este valor en la lógica de aplicación que se utiliza para recuperar el documento XDP después de que el servicio Assembler devuelva el resultado. Por ejemplo, considere la siguiente lógica de aplicación Java que se utiliza para recuperar el documento XDP ensamblado (observe que el valor está en negrita):

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

La variable `XDP source` especifica el archivo XDP que representa un documento XDP completo que puede utilizarse como contenedor para añadir fragmentos XDP o como uno de varios documentos que se anexan juntos en orden. En este caso, el documento XDP se utiliza solo como contenedor (la primera ilustración que se muestra en *Agrupación de varios fragmentos XDP*). Es decir, los otros archivos XDP se colocan dentro del contenedor XDP.

Para cada subformulario, puede agregar una `XDPContent` (este elemento es opcional). En el ejemplo anterior, observe que hay tres subformularios: `subPatientContact`, `subPatientPhysical`y `subPatientHealth`. Ambas `subPatientPhysical` subformulario y `subPatientHealth` el subformulario se encuentra en el mismo archivo XDP, tuc018_holder.xdp. El elemento de fragmento especifica el nombre del subformulario, tal como se define en Designer.

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para ensamblar varios fragmentos XDP, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
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

**Creación de un cliente de ensamblador de PDF**

Antes de realizar una operación Assembler mediante programación, cree un cliente de servicio Assembler.

**Referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para ensamblar varios documentos XDP. Este documento DDX debe contener `XDP result`, `XDP source`y `XDPContent` elementos.

**Referencia a los documentos XDP**

Para ensamblar varios documentos XDP, haga referencia a todos los archivos XDP que se utilizan para ensamblar el documento XDP resultante. Asegúrese de que el nombre del subformulario contenido en el documento XDP al que hace referencia el `source` se especifica en la variable `fragment` atributo. En Designer se define un subformulario. Por ejemplo, considere el siguiente XML.

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

El subformulario denominado *subPatientContact* debe estar ubicado en el archivo XDP llamado *tuc018_contact.xdp*.

**Establecer opciones de tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlan el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Assembler que continúe procesando un trabajo si se encuentra un error.

**Montaje de varios documentos XDP**

Para ensamblar varios archivos XDP, llame a la función `invokeDDX` operación. El servicio Assembler devuelve el documento XDP montado dentro de un objeto de colección.

**Recupere el documento XDP montado**

Un documento XDP montado se devuelve dentro de un objeto de colección. Iterar a través del objeto de colección y guardar el documento XDP como un archivo XDP. También puede pasar el documento XDP a otro servicio de AEM Forms, como Output.

**Consulte también lo siguiente**

[Agrupación de varios fragmentos XDP mediante la API de Java](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[Agrupar varios fragmentos XDP mediante la API de servicio web](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[Creación de documentos del PDF mediante fragmentos](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Agrupación de varios fragmentos XDP mediante la API de Java {#assemble-multiple-xdp-fragments-using-the-java-api}

Ensamble varios fragmentos XDP utilizando la API de servicio de Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-assembler-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `AssemblerServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un documento DDX existente.

   * Cree un `java.io.FileInputStream` objeto que representa el documento DDX utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo DDX.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Haga referencia a los documentos XDP.

   * Cree un `java.util.Map` objeto que se utiliza para almacenar documentos XDP de entrada utilizando un `HashMap` constructor.
   * Cree un `com.adobe.idp.Document` y pase el `java.io.FileInputStream` que contiene el archivo XDP de entrada (repita esta tarea con cada archivo XDP).
   * Agregue una entrada al `java.util.Map` invocando su `put` y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con la variable `source` valor de elemento especificado en el documento DDX (repita esta tarea para cada archivo XDP).
      * A `com.adobe.idp.Document` objeto que contiene el documento XDP que corresponde al `source` (repita esta tarea para cada archivo XDP).

1. Establezca las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Configure las opciones en tiempo de ejecución para satisfacer los requisitos empresariales invocando un método que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque la función `AssemblerOptionSpec` del objeto `setFailOnError` método y pase `false`.

1. Ensamble los varios documentos XDP.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores obligatorios:

   * A `com.adobe.idp.Document` objeto que representa el documento DDX que se va a utilizar
   * A `java.util.Map` objeto que contiene los archivos XDP de entrada
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones de tiempo de ejecución, incluyendo la fuente predeterminada y el nivel de registro de trabajo

   La variable `invokeDDX` el método devuelve un `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene el documento XDP montado.

1. Recupere el documento XDP montado.

   Para obtener el documento XDP montado, realice las siguientes acciones:

   * Invocar el `AssemblerResult` del objeto `getDocuments` método. Este método devuelve un `java.util.Map` objeto.
   * Iterar a través de la variable `java.util.Map` hasta que encuentre el resultado `com.adobe.idp.Document` objeto.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` método para extraer el documento XDP ensamblado.

**Consulte también lo siguiente**

[Agrupación de varios fragmentos XDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[Inicio rápido (modo SOAP): Agrupación de varios fragmentos XDP mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Agrupar varios fragmentos XDP mediante la API de servicio web {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Ensamble varios fragmentos XDP utilizando la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL al configurar una referencia de servicio:

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `AssemblerServiceClient` usando su constructor predeterminado.
   * Cree un `AssemblerServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms, como `https://localhost:8080/soap/services/AssemblerService?blob=mtom`). No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio.
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `AssemblerServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al `AssemblerServiceClient.ClientCredentials.UserName.UserName` campo .
      * Asigne el valor de contraseña correspondiente a la variable `AssemblerServiceClient.ClientCredentials.UserName.Password`campo .
      * Asigne la variable `HttpClientCredentialType.Basic` valor constante de la variable `BasicHttpBindingSecurity.Transport.ClientCredentialType`campo .
      * Asigne la variable `BasicHttpSecurityMode.TransportCredentialOnly` valor constante de la variable `BasicHttpBindingSecurity.Security.Mode`campo .

1. Haga referencia a un documento DDX existente.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento DDX.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento DDX y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia a los documentos XDP.

   * Para cada archivo XDP de entrada, cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el archivo de entrada.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.
   * Cree un `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de colección se utiliza para almacenar los archivos de entrada necesarios para crear un documento XDP ensamblado.
   * Para cada archivo de entrada, cree un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Asigne un valor de cadena que represente el nombre de clave a la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` campo . Este valor debe coincidir con el valor del elemento especificado en el documento DDX. (Realice esta tarea para cada archivo XDP de entrada).
   * Asigne la variable `BLOB` objeto que almacena el archivo de entrada en el `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` campo . (Realice esta tarea para cada archivo XDP de entrada).
   * Agregue la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` al `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invocar el `MyMapOf_xsd_string_To_xsd_anyType` del objeto `Add` y pase el `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Realice esta tarea para cada documento XDP de entrada).

1. Establezca las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Configure las opciones en tiempo de ejecución para satisfacer los requisitos empresariales asignando un valor a un miembro de datos que pertenezca al grupo `AssemblerOptionSpec` objeto. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` a `AssemblerOptionSpec` del objeto `failOnError` miembro de datos.

1. Ensamble los varios documentos XDP.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * A `BLOB` objeto que representa el documento DDX
   * La variable `MyMapOf_xsd_string_To_xsd_anyType` objeto que contiene los archivos necesarios
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución

   La variable `invokeDDX` devuelve un valor `AssemblerResult` que contiene los resultados del trabajo y cualquier excepción que se haya producido.

1. Recupere el documento XDP montado.

   Para obtener el documento XDP recién creado, realice las siguientes acciones:

   * Acceda a la `AssemblerResult` del objeto `documents` , que es un `Map` que contiene los documentos de PDF resultantes.
   * Iterar a través de la variable `Map` para obtener cada documento resultante. A continuación, cree el `value` a `BLOB`.
   * Extraiga los datos binarios que representan el documento del PDF accediendo a su `BLOB` del objeto `MTOM` propiedad. Esto devuelve una matriz de bytes que puede escribir en un archivo XDP.

**Consulte también lo siguiente**

[Agrupación de varios fragmentos XDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
