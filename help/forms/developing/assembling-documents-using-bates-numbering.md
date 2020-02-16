---
title: Montaje de documentos con numeración Bates
seo-title: Montaje de documentos con numeración Bates
description: nulo
seo-description: nulo
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Montaje de documentos con numeración Bates {#assembling-documents-using-bates-numbering}

Puede montar documentos PDF que contengan identificadores de página únicos mediante la numeración Bates. *La numeración* de Bates es un método para aplicar identificaciones únicas a un lote de documentos relacionados. A cada página del documento (o conjunto de documentos) se le asigna un número Bates que identifica de forma exclusiva la página. Por ejemplo, los documentos de fabricación que contienen información sobre la lista de materiales y que están asociados con la producción de un conjunto pueden contener un identificador. Un número Bates contiene un valor numérico incrementado secuencialmente y un prefijo y sufijo opcionales. El prefijo + numérico + sufijo se denomina patrón *bates*.

La siguiente ilustración muestra un documento PDF que contiene un identificador único ubicado en el encabezado del documento.

![au_au_batesnumber](assets/au_au_batesnumber.png)

A los efectos de este análisis, el identificador de página único se coloca en el encabezado de un documento. Supongamos que se utiliza el siguiente documento DDX.

```as3
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

Este documento DDX combina dos documentos PDF denominados *map.pdf* y *direcciones.pdf* en un solo documento PDF. El documento PDF resultante contiene un encabezado que consta de un identificador de página único. Por ejemplo, el documento de la ilustración anterior muestra 000016.

>[!NOTE]
>
>Antes de leer esta sección, se recomienda familiarizarse con el ensamblado de documentos PDF mediante el servicio Ensamblador. En esta sección no se analizan los conceptos, como la creación de un objeto de colección que contenga documentos de entrada o la extracción de los resultados del objeto de recopilación devuelto. (Consulte Compilación [programada de documentos](/help/forms/developing/programmatically-assembling-pdf-documents.md)PDF).

>[!NOTE]
>
>Para obtener más información sobre el servicio Compilador, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y Referencia](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Resumen de los pasos {#summary-of-steps}

Para montar un documento PDF que contenga un identificador de página único (numeración Bates), realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Haga referencia a un documento DDX existente.
1. Consulte documentos PDF de entrada.
1. Establezca el valor inicial del número Bates.
1. Monte los documentos PDF de entrada.
1. Extraiga los resultados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

Si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.

**Crear un cliente de ensamblador de PDF**

Antes de realizar una operación de ensamblador mediante programación, debe crear un cliente de servicio de ensamblador.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para ensamblar un documento PDF. Por ejemplo, considere el documento DDX que se introdujo en esta sección. Para montar un documento PDF que contenga identificadores de página únicos, el documento DDX debe contener el `BatesNumber` elemento .

**Documentos PDF de entrada de referencia**

Se debe hacer referencia a los documentos PDF de entrada para montar un documento PDF. Por ejemplo, se debe hacer referencia a los documentos map.pdf y direccionamiento.pdf para agrupar estos documentos PDF en un solo documento PDF.

**Establecer el valor inicial del número Bates**

Puede configurar el valor inicial del número Bates para que cumpla los requisitos comerciales. Por ejemplo, supongamos que es un requisito establecer el valor inicial en 000100. Si no establece el valor inicial, el valor de la primera página es 000000.

**Compilación de documentos PDF de entrada**

Después de crear el cliente del servicio Ensamblador, hacer referencia al documento DDX que contiene información de `BatesNumber` elementos, hacer referencia a un documento PDF de entrada y establecer opciones de tiempo de ejecución, puede invocar la `invokeDDX` operación que resulta en que el servicio Ensamblador ensamble un documento PDF que contiene identificadores de página únicos.

**Extraer los resultados**

El servicio Ensamblador devuelve un objeto de colección que contiene los resultados del trabajo. Puede extraer el documento PDF resultante y las excepciones que se generen. En este caso, un documento PDF cifrado se encuentra dentro del objeto de recopilación.

>[!NOTE]
>
>Se devuelve un objeto de colección si se invoca la `invokeDDX` operación. Esta operación se utiliza al pasar dos o más documentos PDF de entrada al servicio de ensamblador. Sin embargo, si solo pasa un documento PDF de entrada al servicio Ensamblador, debe invocar la `invokeOneDocument` operación. Para obtener información sobre el uso de esta operación, consulte [Compilación de documentos](/help/forms/developing/assembling-encrypted-pdf-documents.md)PDF cifrados.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Compilación de documentos PDF mediante programación](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Compilación de documentos con numeración Bates mediante la API de Java {#assemble-documents-with-bates-numbering-using-the-java-api}

Monte un documento PDF que utilice identificadores de página únicos (numeración Bates) mediante la API de servicio de ensamblador (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `AssemblerServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un documento DDX existente.

   * Cree un `java.io.FileInputStream` objeto que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Consulte documentos PDF de entrada.

   * Cree un `java.util.Map` objeto que se utilice para almacenar documentos PDF de entrada mediante un `HashMap` constructor.
   * Para cada documento PDF de entrada, cree un `java.io.FileInputStream` objeto utilizando su constructor y pasando la ubicación del documento PDF de entrada. En este caso, pase la ubicación de un documento PDF sin seguridad.
   * Para cada documento PDF de entrada, cree un `com.adobe.idp.Document` objeto y pase el `java.io.FileInputStream` objeto que contiene el documento PDF.
   * Agregue una entrada al `java.util.Map` objeto invocando su `put` método y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX. Por ejemplo, el nombre del archivo de origen PDF especificado en el documento DDX que se introduce en esta sección es Loan.pdf.
      * Un `com.adobe.idp.Document` objeto que contiene el documento PDF no seguro.

1. Establezca el valor inicial del número Bates.

   * Cree un `AssemblerOptionSpec` objeto que almacene opciones de tiempo de ejecución mediante su constructor.
   * Establezca el número Bates inicial invocando el `AssemblerOptionSpec` objeto `setFirstBatesNumber` y pasando un valor numérico que especifique el valor inicial.

1. Monte los documentos PDF de entrada.

   Invoque el `AssemblerServiceClient` método del `invokeDDX` objeto y pase los siguientes valores obligatorios:

   * Un `com.adobe.idp.Document` objeto que representa el documento DDX.
   * Un `java.util.Map` objeto que contiene el archivo PDF no seguro de entrada.
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones en tiempo de ejecución, incluidos el nivel predeterminado de fuente y registro de trabajos.
   El `invokeDDX` método devuelve un `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contiene un documento PDF con contraseña cifrada.

1. Extraiga los resultados.

   Para obtener el documento PDF recién creado, realice las siguientes acciones:

   * Invocar el `AssemblerResult` método del `getDocuments` objeto. Esta acción devuelve un `java.util.Map` objeto.
   * Repita el `java.util.Map` objeto hasta que encuentre el `com.adobe.idp.Document` objeto.
   * Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto para extraer el documento PDF.

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
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `AssemblerServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `AssemblerServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio.
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `AssemblerServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia a un documento DDX existente.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el documento DDX.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento DDX y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Consulte documentos PDF de entrada.

   * Para cada documento PDF de entrada, cree un `BLOB` objeto utilizando su constructor. El `BLOB` objeto se utiliza para almacenar el documento PDF de entrada.
   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el `BLOB` objeto asignando su `MTOM` propiedad con el contenido de la matriz de bytes.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Este objeto de colección se utiliza para almacenar los documentos PDF de entrada.
   * Para cada documento PDF de entrada, cree un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto. Por ejemplo, si se utilizan dos documentos PDF de entrada, cree dos `MyMapOf_xsd_string_To_xsd_anyType_Item` objetos.
   * Asigne un valor de cadena que represente el nombre clave al `MyMapOf_xsd_string_To_xsd_anyType_Item` campo del `key` objeto. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX. (Realice esta tarea para cada documento PDF de entrada).
   * Asigne el `BLOB` objeto que almacena el documento PDF al `MyMapOf_xsd_string_To_xsd_anyType_Item` campo del `value` objeto. (Realice esta tarea para cada documento PDF de entrada).
   * Agregue el `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto al `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invoque el `MyMapOf_xsd_string_To_xsd_anyType` método del `Add` objeto y pase el `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Realice esta tarea para cada documento PDF de entrada).

1. Establezca el valor inicial del número Bates.

   * Cree un `AssemblerOptionSpec` objeto que almacene opciones de tiempo de ejecución mediante su constructor.
   * Establezca el número Bates inicial asignando un valor numérico al miembro de datos que `firstBatesNumber` pertenece al `AssemblerOptionSpec` objeto.

1. Monte los documentos PDF de entrada.

   Invoque el `AssemblerServiceClient` método del `invoke` objeto y pase los valores siguientes:

   * Un `BLOB` objeto que representa el documento DDX.
   * El `MyMapOf_xsd_string_To_xsd_anyType` objeto que contiene los documentos PDF de entrada. Sus claves deben coincidir con los nombres de los archivos de origen PDF y sus valores deben ser los `BLOB` objetos que correspondan a dichos archivos.
   * Un `AssemblerOptionSpec` objeto que especifica opciones de tiempo de ejecución.
   El `invoke` método devuelve un `AssemblerResult` objeto que contiene los resultados del trabajo y las excepciones que se hayan producido.

1. Extraiga los resultados.

   Para obtener el documento PDF recién creado, realice las siguientes acciones:

   * Acceda al `AssemblerResult` campo del `documents` objeto, que es un `Map` objeto que contiene los documentos PDF resultantes.
   * Repita el `Map` objeto hasta que encuentre la clave que coincida con el nombre del documento resultante. A continuación, convierta los elementos del miembro `value` de la matriz en un `BLOB`.
   * Extraiga los datos binarios que representan el documento PDF accediendo a la propiedad del `BLOB` objeto `MTOM` . Esto devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
