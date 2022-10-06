---
title: Agrupación de Portfolio PDF
seo-title: Assembling PDF Portfolios
description: Ensamble un portafolio de PDF para combinar varios documentos de varios tipos, incluidos archivos de palabra, archivos de imagen y documentos de PDF. Puede ensamblar un portafolio de PDF mediante una API de Java y una API de servicio web.
seo-description: Assemble a PDF portfolio to combine several documents of various types, including word file, image files, and PDF documents. You can assemble a PDF portfolio using a Java API and a Web Service API.
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
role: Developer
exl-id: d2bd7c3e-4f75-4234-a7aa-ee8524430493
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 0%

---

# Agrupación de Portfolio PDF {#assembling-pdf-portfolios}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

Puede ensamblar un Portfolio PDF mediante el JRE del ensamblador y la API de servicio web. Un portafolio puede combinar varios documentos de distintos tipos, incluidos archivos de palabra, archivos de imagen (por ejemplo, un archivo jpeg) y documentos PDF. El diseño del portafolio se puede establecer en distintos estilos, como el *Cuadrícula con vista previa*, el *En una imagen* diseño o par *Revolver*.

La siguiente ilustración es una captura de pantalla de un portafolio con *En una imagen* diseño de estilo.

![ap_ap_portafolio](assets/ap_ap_portfolio.png)

La creación de un Portfolio PDF es una alternativa sin papel a la transmisión de una colección de documentos. Con AEM Forms puede crear portafolios invocando el servicio Assembler con un documento DDX estructurado. El siguiente documento DDX es un ejemplo de documento DDX que crea un Portfolio de PDF.

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

El documento DXX debe contener un `Portfolio` etiqueta con un anidado `Navigator` etiqueta. Tenga en cuenta la etiqueta `<Resource name="navigator/image.xxx" source="myImage.png"/>` solo es necesario si `myNavigator` se asigna como navegador de diseño onImage: `AdobeOnImage.nav`. Esta etiqueta permite que el servicio Assembler seleccione la imagen que se utilizará como fondo de portafolio. Incluir `PackageFiles` y `File` etiquetas para definir el nombre de archivo y el tipo MIME del archivo empaquetado.

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para crear un Portfolio de PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Haga referencia a un documento DDX existente.
1. Haga referencia a los documentos necesarios.
1. Establezca las opciones de tiempo de ejecución.
1. Ensamble el portafolio.
1. Guarde el portafolio montado.

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

Se debe hacer referencia a un documento DDX para ensamblar un Portfolio de PDF. Este documento DDX debe contener la variable `Portfolio`, `Navigator` y `PackageFiles` elementos.

**Referencia a los documentos requeridos**

Para ensamblar un Portfolio PDF, haga referencia a todos los archivos que representen los documentos que desea ensamblar. Por ejemplo, pase todos los archivos de imagen especificados en el documento DDX al servicio Assembler. Observe que estos archivos están referenciados en el documento DDX especificado en esta sección: *myImage.png* y *saint_bernard.jpg*.

Al ensamblar un Portfolio PDF, pase un archivo NAV (un archivo del navegador) al servicio Assembler. El archivo NAV que se pasa al servicio Assembler depende del tipo de Portfolio del PDF que se cree. Por ejemplo, para crear un *En una imagen* diseño, pase el archivo AdobeOnImage.nav. Puede localizar archivos NAV en la siguiente carpeta:

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Copie el archivo NAV del directorio de instalación de Acrobat 9 (o posterior). Coloque el archivo NAV en una ubicación en la que la aplicación cliente pueda acceder a él. Todos los archivos se pasan al servicio Assembler dentro de un objeto de colección Map.

>[!NOTE]
>
>Los inicios rápidos asociados con los Portfolio del PDF de ensamblaje utilizan AdobeOnImage.nav.

**Establecer opciones de tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlan el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Assembler que continúe procesando un trabajo si se encuentra un error.

**Montaje del portafolio**

Para montar un Portfolio de PDF, llame a la función `invokeDDX` operación. El servicio Assembler devuelve el Portfolio del PDF dentro de un objeto de colección.

**Guarde el portafolio montado**

Se devuelve un Portfolio PDF dentro de un objeto de colección. Itere a través del objeto de colección y guarde el Portfolio del PDF como un archivo del PDF.

**Consulte también lo siguiente**

[Montaje de un Portfolio de PDF mediante la API de Java](#assemble-a-pdf-portfolio-using-the-java-api)

[Montaje de un Portfolio PDF mediante la API de servicio web](#assemble-a-pdf-portfolio-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montaje de un Portfolio de PDF mediante la API de Java {#assemble-a-pdf-portfolio-using-the-java-api}

Ensamble un Portfolio PDF mediante la API de servicio del ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-assembler-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `AssemblerServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un documento DDX existente.

   * Cree un `java.io.FileInputStream` objeto que representa el documento DDX utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo DDX.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Haga referencia a los documentos necesarios.

   * Cree un `java.util.Map` objeto que se utiliza para almacenar documentos del PDF de entrada mediante un `HashMap` constructor.
   * Cree un `java.io.FileInputStream` usando su constructor. Pase la ubicación del archivo NAV requerido (repita esta tarea para cada archivo necesario para crear un portafolio).
   * Cree un `com.adobe.idp.Document` y pase el `java.io.FileInputStream` que contiene el archivo NAV (repita esta tarea con cada archivo necesario para crear un portafolio).
   * Agregue una entrada al `java.util.Map` invocando su `put` y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen especificado en el documento DDX. (repita esta tarea para cada archivo necesario para crear un portafolio).
      * A `com.adobe.idp.Document` objeto que contiene el documento PDF. (repita esta tarea para cada archivo necesario para crear un portafolio).

1. Establezca las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Configure las opciones en tiempo de ejecución para satisfacer los requisitos empresariales invocando un método que pertenece al `AssemblerOptionSpec` objeto. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque la función `AssemblerOptionSpec` del objeto `setFailOnError` método y pase `false`.

1. Ensamble el portafolio.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores obligatorios:

   * A `com.adobe.idp.Document` objeto que representa el documento DDX que se va a utilizar
   * A `java.util.Map` que contiene los archivos necesarios para crear un Portfolio de PDF.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones de tiempo de ejecución, incluida la fuente predeterminada y el nivel de registro de trabajo

   La variable `invokeDDX` el método devuelve un `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contiene el Portfolio del PDF montado y cualquier excepción que se haya producido.

1. Guarde el portafolio montado.

   Para obtener el Portfolio del PDF, realice las siguientes acciones:

   * Invocar el `AssemblerResult` del objeto `getDocuments` método. Este método devuelve un `java.util.Map` objeto.
   * Iterar a través de la variable `java.util.Map` hasta que encuentre el resultado `com.adobe.idp.Document` objeto.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para extraer el Portfolio del PDF.

**Consulte también lo siguiente**

[Inicio rápido (modo SOAP): Agrupación de Portfolio PDF mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montaje de un Portfolio PDF mediante la API de servicio web {#assemble-a-pdf-portfolio-using-the-web-service-api}

Ensamble un Portfolio PDF mediante la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL al configurar una referencia de servicio: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `AssemblerServiceClient` usando su constructor predeterminado.
   * Cree un `AssemblerServiceClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio.
   * Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `AssemblerServiceClient.Endpoint.Binding` campo . Conversión del valor devuelto a `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asignar el nombre de usuario de los formularios AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Asignar el valor de contraseña correspondiente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un documento DDX existente.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento DDX.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento DDX y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia a los documentos necesarios.

   * Para cada archivo de entrada, cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el archivo de entrada.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.
   * Cree un `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de colección se utiliza para almacenar los archivos de entrada necesarios para crear un Portfolio de PDF.
   * Para cada archivo de entrada, cree un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Asigne un valor de cadena que represente el nombre de clave a la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` campo . Este valor debe coincidir con el valor del elemento especificado en el documento DDX. (Realice esta tarea para cada archivo de entrada).
   * Asigne la variable `BLOB` objeto que almacena el archivo de entrada en el `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` campo . (Realice esta tarea para cada documento del PDF de entrada).
   * Agregue la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` al `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invocar el `MyMapOf_xsd_string_To_xsd_anyType` del objeto `Add` y pase el `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Realice esta tarea para cada documento del PDF de entrada).

1. Establezca las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Configure las opciones en tiempo de ejecución para satisfacer los requisitos empresariales asignando un valor a un miembro de datos que pertenezca al grupo `AssemblerOptionSpec` objeto. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` a `AssemblerOptionSpec` del objeto `failOnError` miembro de datos.

1. Ensamble el portafolio.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * A `BLOB` objeto que representa el documento DDX
   * La variable `MyMapOf_xsd_string_To_xsd_anyType` objeto que contiene los archivos necesarios
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución

   La variable `invokeDDX` devuelve un valor `AssemblerResult` que contiene los resultados del trabajo y cualquier excepción que se haya producido.

1. Guarde el portafolio montado.

   Para obtener el Portfolio del PDF recién creado, realice las siguientes acciones:

   * Acceda a la `AssemblerResult` del objeto `documents` , que es un `Map` que contiene los documentos de PDF resultantes.
   * Iterar a través de la variable `Map` para obtener cada documento resultante. A continuación, cree el `value` a `BLOB`.
   * Extraiga los datos binarios que representan el documento del PDF accediendo a su `BLOB` del objeto `MTOM` propiedad. Esto devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
