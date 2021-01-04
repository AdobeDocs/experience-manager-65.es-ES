---
title: Montaje de Documentos con numeración Bates
seo-title: Montaje de Documentos con numeración Bates
description: 'Utilice la numeración Bates para montar documentos PDF mediante la API de Java y de servicio Web. '
seo-description: 'Utilice la numeración Bates para montar documentos PDF mediante la API de Java y de servicio Web. '
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1927'
ht-degree: 0%

---


# Montaje de Documentos con numeración de Bates {#assembling-documents-using-bates-numbering}

Puede montar documentos PDF que contengan identificadores de página únicos mediante la numeración Bates. *La* numeración Bates es un método para aplicar identificaciones únicas a un lote de documentos relacionados. A cada página del documento (o conjunto de documentos) se le asigna un número Bates que identifica de forma exclusiva la página. Por ejemplo, los documentos de fabricación que contienen información sobre listas de materiales y están asociados con la producción de un conjunto pueden contener un identificador. Un número Bates contiene un valor numérico incrementado secuencialmente y un prefijo y sufijo opcionales. El prefijo + sufijo numérico + se denomina patrón *bates*.

La siguiente ilustración muestra un documento PDF que contiene un identificador único ubicado en el encabezado del documento.

![au_au_batesnumber](assets/au_au_batesnumber.png)

A los efectos de este análisis, el identificador de página único se coloca en el encabezado de un documento. Supongamos que se utiliza el siguiente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="out.pdf">
        <Header>
         <Center>
             <StyledText>
                 <p font-size="20pt"><BatesNumber/></p>
             </StyledText>
         </Center>
     </Header>
           <PDF source="map.pdf" />
          <PDF source="directions.pdf" />
          </PDF>
 </DDX>
```

Este documento DDX combina dos documentos PDF con el nombre *map.pdf* y *direccionamientos.pdf* en un único documento PDF. El documento PDF resultante contiene un encabezado que consta de un identificador de página único. Por ejemplo, el documento de la ilustración anterior muestra 000016.

>[!NOTE]
>
>Antes de leer esta sección, se recomienda familiarizarse con el ensamblado de documentos PDF mediante el servicio Ensamblador. En esta sección no se analizan los conceptos, como la creación de un objeto de colección que contenga documentos de entrada o la extracción de los resultados del objeto de colección devuelto. (Consulte [Compilación programada de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)).

>[!NOTE]
>
>Para obtener más información sobre el servicio de ensamblador, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y Referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para montar un documento PDF que contenga un identificador de página único (numeración Bates), realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Haga referencia a un documento DDX existente.
1. Documentos PDF de entrada de referencia.
1. Establezca el valor inicial del número Bates.
1. Monte los documentos PDF de entrada.
1. Extraiga los resultados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requerido si AEM Forms se implementa en JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss)

Si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de ensamblador de PDF**

Antes de realizar una operación de ensamblador mediante programación, debe crear un cliente de servicio de ensamblador.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para montar un documento PDF. Por ejemplo, considere el documento DDX que se introdujo en esta sección. Para montar un documento PDF que contenga identificadores de página únicos, el documento DDX debe contener el elemento `BatesNumber`.

**Documentos PDF de entrada de referencia**

Se debe hacer referencia a los documentos PDF de entrada para montar un documento PDF. Por ejemplo, se debe hacer referencia a los documentos map.pdf y direccionamiento.pdf para agrupar estos documentos PDF en un solo documento PDF.

**Establecer el valor inicial del número Bates**

Puede configurar el valor inicial del número Bates para que cumpla los requisitos comerciales. Por ejemplo, supongamos que es un requisito establecer el valor inicial en 000100. Si no establece el valor inicial, el valor de la primera página es 000000.

**Compilación de los documentos PDF de entrada**

Después de crear el cliente del servicio Ensamblador, haga referencia al documento DDX que contiene `BatesNumber` información del elemento, haga referencia a un documento PDF de entrada y defina las opciones de tiempo de ejecución, puede invocar la operación `invokeDDX` que resulta en que el servicio Ensamblador ensamble un documento PDF que contiene identificadores de página únicos.

**Extraer los resultados**

El servicio Ensamblador devuelve un objeto de colección que contiene los resultados del trabajo. Puede extraer el documento PDF resultante y las excepciones que se generen. En este caso, un documento PDF cifrado se encuentra dentro del objeto de recopilación.

>[!NOTE]
>
>Se devuelve un objeto de colección si invoca la operación `invokeDDX`. Esta operación se utiliza al pasar dos o más documentos PDF de entrada al servicio de ensamblador. Sin embargo, si solo pasa un documento PDF de entrada al servicio Ensamblador, debe invocar la operación `invokeOneDocument`. Para obtener información sobre el uso de esta operación, consulte [Compilación de Documentos PDF cifrados](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Compilación programada de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Compilación de documentos con numeración Bates mediante la API de Java {#assemble-documents-with-bates-numbering-using-the-java-api}

Monte un documento PDF que utilice identificadores de página únicos (numeración Bates) mediante la API de servicio de ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Haga referencia a un documento DDX existente.

   * Cree un objeto `java.io.FileInputStream` que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Documentos PDF de entrada de referencia.

   * Cree un objeto `java.util.Map` utilizado para almacenar documentos PDF de entrada mediante un constructor `HashMap`.
   * Para cada documento PDF de entrada, cree un objeto `java.io.FileInputStream` utilizando su constructor y pasando la ubicación del documento PDF de entrada. En este caso, pase la ubicación de un documento PDF sin seguridad.
   * Para cada documento PDF de entrada, cree un objeto `com.adobe.idp.Document` y pase el objeto `java.io.FileInputStream` que contiene el documento PDF.
   * Añada una entrada al objeto `java.util.Map` invocando su método `put` y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX. Por ejemplo, el nombre del archivo de origen PDF especificado en el documento DDX que se introduce en esta sección es Loan.pdf.
      * Un objeto `com.adobe.idp.Document` que contiene el documento PDF no seguro.

1. Establezca el valor inicial del número Bates.

   * Cree un objeto `AssemblerOptionSpec` que almacene las opciones de tiempo de ejecución mediante su constructor.
   * Establezca el número Bates inicial invocando el `AssemblerOptionSpec` objeto `setFirstBatesNumber` y pasando un valor numérico que especifique el valor inicial.

1. Monte los documentos PDF de entrada.

   Invoque el método `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores obligatorios:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX.
   * Un objeto `java.util.Map` que contiene el archivo PDF no seguro de entrada.
   * Un objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución, incluido el nivel predeterminado de fuente y registro de trabajos.

   El método `invokeDDX` devuelve un objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene un documento PDF con contraseña cifrada.

1. Extraiga los resultados.

   Para obtener el documento PDF recién creado, realice las siguientes acciones:

   * Invocar el método `AssemblerResult` del objeto `getDocuments`. Esta acción devuelve un objeto `java.util.Map`.
   * Repita el objeto `java.util.Map` hasta que encuentre el objeto `com.adobe.idp.Document`.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para extraer el documento PDF.

**Consulte también**

[Inicio rápido (modo SOAP): Compilación de un documento PDF con numeración Bates mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Compilación de documentos con numeración Bates mediante la API de servicio Web {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Monte un documento PDF que utilice identificadores de página únicos (numeración Bates) mediante la API de servicio de ensamblador (servicio Web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento DDX y el modo en el que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Documentos PDF de entrada de referencia.

   * Para cada documento PDF de entrada, cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento PDF de entrada.
   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.
   * Cree un objeto `MyMapOf_xsd_string_To_xsd_anyType`. Este objeto de colección se utiliza para almacenar los documentos PDF de entrada.
   * Para cada documento PDF de entrada, cree un objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Por ejemplo, si se utilizan dos documentos PDF de entrada, cree dos objetos `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Asigne un valor de cadena que represente el nombre clave al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key`. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX. (Realice esta tarea para cada documento PDF de entrada).
   * Asigne el objeto `BLOB` que almacena el documento PDF al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value`. (Realice esta tarea para cada documento PDF de entrada).
   * Añada el objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` al objeto `MyMapOf_xsd_string_To_xsd_anyType`. Invoque el método `MyMapOf_xsd_string_To_xsd_anyType` del objeto `Add` y pase el objeto `MyMapOf_xsd_string_To_xsd_anyType`. (Realice esta tarea para cada documento PDF de entrada).

1. Establezca el valor inicial del número Bates.

   * Cree un objeto `AssemblerOptionSpec` que almacene las opciones de tiempo de ejecución mediante su constructor.
   * Establezca el número Bates inicial asignando un valor numérico al miembro de datos `firstBatesNumber` que pertenece al objeto `AssemblerOptionSpec`.

1. Monte los documentos PDF de entrada.

   Invoque el método `AssemblerServiceClient` del objeto `invoke` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX.
   * El objeto `MyMapOf_xsd_string_To_xsd_anyType` que contiene los documentos PDF de entrada. Sus claves deben coincidir con los nombres de los archivos de origen PDF y sus valores deben ser los objetos `BLOB` que correspondan a esos archivos.
   * Un objeto `AssemblerOptionSpec` que especifica opciones de tiempo de ejecución.

   El método `invoke` devuelve un objeto `AssemblerResult` que contiene los resultados del trabajo y las excepciones que se hayan producido.

1. Extraiga los resultados.

   Para obtener el documento PDF recién creado, realice las siguientes acciones:

   * Acceda al campo `AssemblerResult` del objeto `documents`, que es un objeto `Map` que contiene los documentos PDF resultantes.
   * Repita el objeto `Map` hasta que encuentre la clave que coincida con el nombre del documento resultante. A continuación, convierta el `value` miembro del arreglo de discos en un `BLOB`.
   * Extraiga los datos binarios que representan el documento PDF accediendo a la propiedad `BLOB` del objeto `MTOM`. Esto devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
