---
title: Agrupar portfolios PDF
description: Montar un portafolio de PDF para combinar varios documentos de varios tipos, incluidos archivos de Word, archivos de imagen y documentos de PDF. Puede combinar un catálogo de productos de PDF mediante una API de Java y una API de servicio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d2bd7c3e-4f75-4234-a7aa-ee8524430493
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1815'
ht-degree: 0%

---

# Agrupar portfolios PDF {#assembling-pdf-portfolios}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Puede ensamblar un Portfolio de PDF mediante la API de servicio web y Java del ensamblador. Un portafolio puede combinar varios documentos de varios tipos, incluidos archivos de Word, archivos de imagen (por ejemplo, un archivo JPEG) y documentos de PDF. El diseño del portafolio se puede establecer en diferentes estilos, como el *Cuadrícula con vista previa*, el *En una imagen* diseño o evento *Revolver*.

La siguiente ilustración es una captura de pantalla de un portafolio con *En una imagen* diseño de estilo.

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

La creación de un Portfolio PDF sirve como una alternativa sin papel a pasar una colección de documentos. Con AEM Forms puede crear portafolios invocando el servicio Assembler con un documento DDX estructurado. El siguiente documento DDX es un ejemplo de documento DDX que crea un Portfolio PDF.

```xml
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="portfolio1.pdf">
         <Portfolio>
             <Navigator source="myNavigator">
                 <Resource name="navigator/image.xxx" source="myImage.png"/>
             </Navigator>
         </Portfolio>
         <PackageFiles source="dog1"  >
              <FieldData name="X">72</FieldData>
             <FieldData name="Y">72</FieldData>
             <File filename="saint_bernard.jpg" mimetype="image/jpeg"/>
         </PackageFiles>
         <PackageFiles source="dog2"  >
             <FieldData name="X">120</FieldData>
             <FieldData name="Y">216</FieldData>
             <File filename="greyhound.pdf"/>
         </PackageFiles>
     </PDF>
 </DDX>
```

El documento DXX debe contener un `Portfolio` con una etiqueta anidada `Navigator` etiqueta. Observe la etiqueta `<Resource name="navigator/image.xxx" source="myImage.png"/>` solo es necesario si `myNavigator` se asigna como navegador de diseño onImage: `AdobeOnImage.nav`. Esta etiqueta permite al servicio Assembler seleccionar la imagen que se utilizará como fondo del portafolio. Incluir `PackageFiles` y `File` para definir el nombre de archivo y el tipo MIME del archivo empaquetado.

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para crear un Portfolio PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDF Assembler.
1. Hacer referencia a un documento DDX existente.
1. Consulte los documentos necesarios.
1. Establecer opciones en tiempo de ejecución.
1. Organice el portafolio.
1. Guarde el portafolio ensamblado.

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

Se debe hacer referencia a un documento DDX para ensamblar un Portfolio PDF. Este documento DDX debe contener la variable `Portfolio`, `Navigator` y, `PackageFiles` elementos.

**Hacer referencia a los documentos requeridos**

Para montar un Portfolio de PDF, haga referencia a todos los archivos que representan los documentos que se van a montar. Por ejemplo, pase todos los archivos de imagen especificados en el documento DDX al servicio Assembler. Observe que se hace referencia a estos archivos en el documento DDX especificado en esta sección: *myImage.png* y *saint_bernard.jpg*.

Al combinar un Portfolio de PDF, pase un archivo NAV (un archivo del navegador) al servicio Assembler. El archivo NAV que pasa al servicio Assembler depende del tipo de Portfolio de PDF que se va a crear. Por ejemplo, para crear un *En una imagen* , pase el archivo AdobeOnImage.nav. Puede localizar archivos NAV en la siguiente carpeta:

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Copie el archivo NAV del directorio de instalación de Acrobat 9 (o posterior). Coloque el archivo NAV en una ubicación donde la aplicación cliente pueda acceder a él. Todos los archivos se pasan al servicio Assembler dentro de un objeto de la colección Map.

>[!NOTE]
>
>Los inicios rápidos asociados con los Portfolio del PDF Assembling utilizan AdobeOnImage.nav.

**Establecer opciones en tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlen el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede establecer una opción que indique al servicio Assembler que continúe procesando un trabajo si se produce un error.

**Montar el portafolio**

Para montar un Portfolio PDF, llame al método `invokeDDX` operación. El servicio Assembler devuelve el Portfolio PDF dentro de un objeto de colección.

**Guardar el portafolio ensamblado**

Se devuelve un Portfolio PDF dentro de un objeto de colección. Itere por el objeto de colección y guarde el Portfolio de PDF como un archivo de PDF.

**Consulte también**

[Montar un Portfolio PDF mediante la API de Java](#assemble-a-pdf-portfolio-using-the-java-api)

[Montar un Portfolio PDF mediante la API de servicio web](#assemble-a-pdf-portfolio-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montar un Portfolio PDF mediante la API de Java {#assemble-a-pdf-portfolio-using-the-java-api}

Ensamble un Portfolio PDF mediante la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de PDF Assembler.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `AssemblerServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Hacer referencia a un documento DDX existente.

   * Crear un `java.io.FileInputStream` que representa el documento DDX utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo DDX.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Consulte los documentos necesarios.

   * Crear un `java.util.Map` objeto que se utiliza para almacenar documentos del PDF de entrada mediante un `HashMap` constructor.
   * Crear un `java.io.FileInputStream` mediante su constructor. Pase la ubicación del archivo NAV requerido (repita esta tarea con cada archivo necesario para crear un portafolio).
   * Crear un `com.adobe.idp.Document` y pase el `java.io.FileInputStream` que contiene el archivo NAV (repita esta tarea para cada archivo necesario para crear un portafolio).
   * Añada una entrada a `java.util.Map` invocando su objeto `put` y pasando los siguientes argumentos:

      * Valor de cadena que representa el nombre de clave. Este valor debe coincidir con el valor del elemento de origen especificado en el documento DDX. (repita esta tarea para cada archivo necesario para crear un portafolio).
      * A `com.adobe.idp.Document` que contiene el documento de PDF. (repita esta tarea para cada archivo necesario para crear un portafolio).

1. Establecer opciones en tiempo de ejecución.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca opciones en tiempo de ejecución para satisfacer sus necesidades empresariales invocando un método que pertenezca a `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque el `AssemblerOptionSpec` del objeto `setFailOnError` método y pase `false`.

1. Organice el portafolio.

   Invoque el `AssemblerServiceClient` del objeto `invokeDDX` y pasar los siguientes valores obligatorios:

   * A `com.adobe.idp.Document` que representa el documento DDX a utilizar
   * A `java.util.Map` que contiene los archivos necesarios para generar un Portfolio de PDF.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones de tiempo de ejecución, incluida la fuente predeterminada y el nivel de registro de trabajo

   El `invokeDDX` El método devuelve un valor `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene el Portfolio PDF ensamblado y las excepciones que se han producido.

1. Guarde el portafolio ensamblado.

   Para obtener el Portfolio PDF, realice las siguientes acciones:

   * Invoque el `AssemblerResult` del objeto `getDocuments` método. Este método devuelve un `java.util.Map` objeto.
   * Itere a través de `java.util.Map` hasta que encuentre el resultado `com.adobe.idp.Document` objeto.
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para extraer el Portfolio de PDF.

**Consulte también**

[SOAP Inicio rápido (modo de): Agrupación de Portfolio de PDF mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montar un Portfolio PDF mediante la API de servicio web {#assemble-a-pdf-portfolio-using-the-web-service-api}

Ensamble un Portfolio PDF mediante la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL al configurar una referencia de servicio: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de PDF Assembler.

   * Crear un `AssemblerServiceClient` mediante su constructor predeterminado.
   * Crear un `AssemblerServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio.
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `AssemblerServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Hacer referencia a un documento DDX existente.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el documento DDX.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento DDX y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` método. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Consulte los documentos necesarios.

   * Para cada archivo de entrada, cree un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el archivo de entrada.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` método. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.
   * Crear un `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de colección se utiliza para almacenar los archivos de entrada necesarios para crear un Portfolio de PDF.
   * Para cada archivo de entrada, cree un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Asigne un valor de cadena que represente el nombre de clave al `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` field. Este valor debe coincidir con el valor del elemento especificado en el documento DDX. (Realice esta tarea para cada archivo de entrada).
   * Asigne el `BLOB` que almacena el archivo de entrada en el `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` field. (Realice esta tarea para cada documento de PDF de entrada).
   * Añada el `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto a `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invoque el `MyMapOf_xsd_string_To_xsd_anyType` del objeto `Add` y pase el `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Realice esta tarea para cada documento de PDF de entrada).

1. Establecer opciones en tiempo de ejecución.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca las opciones en tiempo de ejecución para satisfacer sus necesidades empresariales asignando un valor a un miembro de datos que pertenezca a `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne a `false` a la `AssemblerOptionSpec` del objeto `failOnError` miembro de datos.

1. Organice el portafolio.

   Invoque el `AssemblerServiceClient` del objeto `invokeDDX` y pasar los siguientes valores:

   * A `BLOB` que representa el documento DDX
   * El `MyMapOf_xsd_string_To_xsd_anyType` que contiene los archivos necesarios
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución

   El `invokeDDX` El método devuelve un `AssemblerResult` que contiene los resultados del trabajo y las excepciones que se han producido.

1. Guarde el portafolio ensamblado.

   Para obtener el Portfolio PDF recién creado, realice las siguientes acciones:

   * Acceda a la `AssemblerResult` del objeto `documents` , que es un `Map` que contiene los documentos de PDF resultantes.
   * Itere a través de `Map` para obtener cada documento resultante. A continuación, convierta el de ese miembro de la matriz `value` a un `BLOB`.
   * Extraiga los datos binarios que representan el documento PDF accediendo a su `BLOB` del objeto `MTOM` propiedad. Devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
