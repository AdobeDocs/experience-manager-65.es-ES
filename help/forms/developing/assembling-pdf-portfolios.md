---
title: Compilación de Portfolio PDF
seo-title: Compilación de Portfolio PDF
description: Monte un portafolio PDF para combinar varios documentos de distintos tipos, incluidos archivos de palabras, archivos de imágenes y documentos PDF. Puede montar un portafolio PDF mediante una API de Java y una API de servicio Web.
seo-description: Monte un portafolio PDF para combinar varios documentos de distintos tipos, incluidos archivos de palabras, archivos de imágenes y documentos PDF. Puede montar un portafolio PDF mediante una API de Java y una API de servicio Web.
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1851'
ht-degree: 0%

---


# Compilación de Portfolio PDF {#assembling-pdf-portfolios}

Puede montar un Portfolio PDF mediante el JRE del ensamblador y la API de servicio Web. Un portafolio puede combinar varios documentos de distintos tipos, incluidos archivos de palabras, archivos de imágenes (por ejemplo, un archivo jpeg) y documentos PDF. El diseño del portafolio puede configurarse en diferentes estilos, como la *cuadrícula con Previsualización*, el diseño *En una imagen* o incluso *Girar*.

La siguiente ilustración es una captura de pantalla de un portafolio con *diseño de estilo de imagen*.

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

Crear un Portfolio PDF es una alternativa sin papel a pasar una colección de documentos. Con AEM Forms puede crear carteras invocando el servicio Ensamblador con un documento DDX estructurado. El siguiente documento DDX es un ejemplo de un documento DDX que crea un Portfolio PDF.

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

El documento DXX debe contener una etiqueta `Portfolio` con una etiqueta `Navigator` anidada. Tenga en cuenta que la etiqueta `<Resource name="navigator/image.xxx" source="myImage.png"/>` sólo es necesaria si `myNavigator` está asignada como el navegador de diseño onImage: `AdobeOnImage.nav`. Esta etiqueta permite al servicio Compilador seleccionar la imagen que se va a utilizar como fondo de portafolio. Incluya las etiquetas `PackageFiles` y `File` para definir el nombre de archivo y el tipo MIME del archivo empaquetado.

>[!NOTE]
>
>Para obtener más información sobre el servicio de ensamblador, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y Referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para crear un Portfolio PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Haga referencia a un documento DDX existente.
1. Haga referencia a los documentos necesarios.
1. Configure las opciones de tiempo de ejecución.
1. Monte el portafolio.
1. Guarde el portafolio montado.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requerido si AEM Forms se implementa en JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss)

**Crear un cliente de ensamblador de PDF**

Antes de realizar una operación de ensamblador mediante programación, cree un cliente de servicio de ensamblador.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para montar un Portfolio PDF. Este documento DDX debe contener los elementos `Portfolio`, `Navigator` y `PackageFiles`.

**Hacer referencia a los documentos requeridos**

Para montar un Portfolio PDF, haga referencia a todos los archivos que representan los documentos que se van a ensamblar. Por ejemplo, pase todos los archivos de imagen especificados en el documento DDX al servicio Ensamblador. Tenga en cuenta que se hace referencia a estos archivos en el documento DDX especificado en esta sección: *myImage.png* y *saint_bernard.jpg*.

Al montar un Portfolio PDF, pase un archivo NAV (un archivo de navegador) al servicio del ensamblador. El archivo NAV que se pasa al servicio de ensamblador depende del tipo de Portfolio PDF que se cree. Por ejemplo, para crear un diseño *En una imagen*, pase el archivo AdobeOnImage.nav. Puede localizar archivos NAV en la siguiente carpeta:

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Copie el archivo NAV del directorio de instalación de Acrobat 9 (o posterior). Coloque el archivo NAV en una ubicación en la que la aplicación cliente pueda acceder a él. Todos los archivos se pasan al servicio del ensamblador dentro de un objeto de colección Map.

>[!NOTE]
>
>Los inicios rápidos asociados a la agrupación de Portfolio PDF utilizan AdobeOnImage.nav.

**Definición de opciones de tiempo de ejecución**

Puede definir opciones en tiempo de ejecución que controlen el comportamiento del servicio de ensamblador mientras realiza un trabajo. Por ejemplo, puede definir una opción que indique al servicio Ensamblador que continúe procesando un trabajo si se produce un error.

**Compilación de la cartera**

Para montar un Portfolio PDF, debe llamar a la operación `invokeDDX`. El servicio Ensamblador devuelve el Portfolio PDF dentro de un objeto de colección.

**Guardar el portafolio ensamblado**

Se devuelve un Portfolio PDF dentro de un objeto de colección. Repita el objeto de colección y guarde el Portfolio PDF como archivo PDF.

**Consulte también**

[Compilación de un Portfolio PDF mediante la API de Java](#assemble-a-pdf-portfolio-using-the-java-api)

[Compilación de un Portfolio PDF mediante la API de servicio Web](#assemble-a-pdf-portfolio-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Compilación programada de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Compilación de un Portfolio PDF mediante la API de Java {#assemble-a-pdf-portfolio-using-the-java-api}

Monte un Portfolio PDF mediante la API de servicio de ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Haga referencia a un documento DDX existente.

   * Cree un objeto `java.io.FileInputStream` que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Haga referencia a los documentos necesarios.

   * Cree un objeto `java.util.Map` que se utilice para almacenar documentos PDF de entrada mediante un constructor `HashMap`.
   * Cree un objeto `java.io.FileInputStream` utilizando su constructor. Pase la ubicación del archivo NAV requerido (repita esta tarea para cada archivo necesario para crear una cartera).
   * Cree un objeto `com.adobe.idp.Document` y pase el objeto `java.io.FileInputStream` que contiene el archivo NAV (repita esta tarea para cada archivo necesario para crear un portafolio).
   * Añada una entrada al objeto `java.util.Map` invocando su método `put` y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen especificado en el documento DDX. (repita esta tarea para cada archivo necesario para crear un portafolio).
      * Un objeto `com.adobe.idp.Document` que contiene el documento PDF. (repita esta tarea para cada archivo necesario para crear un portafolio).

1. Configure las opciones de tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene las opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para satisfacer los requisitos comerciales invocando un método que pertenece al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, invoque el método `AssemblerOptionSpec` del objeto `setFailOnError` y pase `false`.

1. Monte el portafolio.

   Invoque el método `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores obligatorios:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX que se va a utilizar
   * Un objeto `java.util.Map` que contiene los archivos necesarios para crear un Portfolio PDF.
   * Un objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones de tiempo de ejecución, incluyendo la fuente predeterminada y el nivel de registro de trabajos

   El método `invokeDDX` devuelve un objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene el Portfolio PDF ensamblado y las excepciones que se hayan producido.

1. Guarde el portafolio montado.

   Para obtener el Portfolio PDF, realice las siguientes acciones:

   * Invocar el método `AssemblerResult` del objeto `getDocuments`. Este método devuelve un objeto `java.util.Map`.
   * Repita el objeto `java.util.Map` hasta que encuentre el objeto `com.adobe.idp.Document` resultante.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para extraer el Portfolio PDF.

**Consulte también**

[Inicio rápido (modo SOAP): Compilación de Portfolio PDF mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Compilación de un Portfolio PDF mediante la API de servicio Web {#assemble-a-pdf-portfolio-using-the-web-service-api}

Monte un Portfolio PDF mediante la API de servicio de ensamblador (servicio Web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL al configurar una referencia de servicio: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de ensamblador de PDF.

   * Cree un objeto `AssemblerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `AssemblerServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `AssemblerServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un documento DDX existente.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento DDX.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento DDX y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia a los documentos necesarios.

   * Para cada archivo de entrada, cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el archivo de entrada.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.
   * Cree un objeto `MyMapOf_xsd_string_To_xsd_anyType`. Este objeto de colección se utiliza para almacenar los archivos de entrada necesarios para crear un Portfolio PDF.
   * Para cada archivo de entrada, cree un objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Asigne un valor de cadena que represente el nombre clave al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key`. Este valor debe coincidir con el valor del elemento especificado en el documento DDX. (Realice esta tarea para cada archivo de entrada).
   * Asigne el objeto `BLOB` que almacena el archivo de entrada en el campo `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value`. (Realice esta tarea para cada documento PDF de entrada).
   * Añada el objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` al objeto `MyMapOf_xsd_string_To_xsd_anyType`. Invoque el método `MyMapOf_xsd_string_To_xsd_anyType` del objeto `Add` y pase el objeto `MyMapOf_xsd_string_To_xsd_anyType`. (Realice esta tarea para cada documento PDF de entrada).

1. Configure las opciones de tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene las opciones de tiempo de ejecución mediante su constructor.
   * Configure las opciones de tiempo de ejecución para satisfacer los requisitos comerciales asignando un valor a un miembro de datos que pertenece al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Ensamblador que continúe procesando un trabajo cuando se produzca un error, asigne `false` al miembro de datos `AssemblerOptionSpec` del objeto `failOnError`.

1. Monte el portafolio.

   Invoque el método `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX
   * El objeto `MyMapOf_xsd_string_To_xsd_anyType` que contiene los archivos necesarios
   * Un objeto `AssemblerOptionSpec` que especifica opciones de tiempo de ejecución

   El método `invokeDDX` devuelve un objeto `AssemblerResult` que contiene los resultados del trabajo y las excepciones que se hayan producido.

1. Guarde el portafolio montado.

   Para obtener el Portfolio PDF recién creado, realice las siguientes acciones:

   * Acceda al campo `AssemblerResult` del objeto `documents`, que es un objeto `Map` que contiene los documentos PDF resultantes.
   * Repita el objeto `Map` para obtener cada documento resultante. A continuación, convierta el `value` miembro del arreglo de discos en un `BLOB`.
   * Extraiga los datos binarios que representan el documento PDF accediendo a la propiedad `BLOB` del objeto `MTOM`. Esto devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
