---
title: Montaje de Documentos Utilizando Numeración Bates
seo-title: Assembling Documents Using Bates Numbering
description: Utilice la numeración Bates para ensamblar documentos de PDF mediante la API de Java y Web Service.
seo-description: Use Bates numbering to assemble PDF documents using the Java and Web Service API.
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
role: Developer
exl-id: 2a4e21c4-f2f5-44cd-b8ed-7b572782a2f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1922'
ht-degree: 0%

---

# Montaje de Documentos Utilizando Numeración Bates {#assembling-documents-using-bates-numbering}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

Puede ensamblar documentos PDF que contengan identificadores de página únicos mediante la numeración Bates. *Numeración de Bates* es un método para aplicar identificadores únicos a un lote de documentos relacionados. A cada página del documento (o conjunto de documentos) se le asigna un número Bates que identifica de forma exclusiva la página. Por ejemplo, los documentos de fabricación que contienen información de lista de materiales y están asociados con la producción de un conjunto pueden contener un identificador. Un número Bates contiene un valor numérico incrementado secuencialmente y un prefijo y sufijo opcionales. El prefijo + sufijo numérico + se denomina *patrón de barras*.

La siguiente ilustración muestra un documento PDF que contiene un identificador único ubicado en el encabezado del documento.

![au_au_batesnumber](assets/au_au_batesnumber.png)

A los efectos de esta discusión, el identificador de página único se coloca en el encabezado de un documento. Supongamos que se utiliza el siguiente documento DDX.

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

Este documento DDX combina dos documentos PDF llamados *map.pdf* y *addresses.pdf* en un documento de PDF único. El documento de PDF resultante contiene un encabezado que consta de un identificador de página único. Por ejemplo, el documento de la ilustración anterior muestra 000016.

>[!NOTE]
>
>Antes de leer esta sección, se recomienda que esté familiarizado con el ensamblaje de documentos PDF mediante el servicio Assembler. En esta sección no se tratan los conceptos, como la creación de un objeto de colección que contenga documentos de entrada o la extracción de los resultados del objeto de colección devuelto. (Consulte [Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Para obtener más información sobre el servicio Assembler, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio de ensamblador y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para ensamblar un documento de PDF que contenga un identificador de página único (numeración Bates), realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de ensamblador de PDF.
1. Haga referencia a un documento DDX existente.
1. Documentos de PDF de entrada de referencia.
1. Establezca el valor de número de Bates inicial.
1. Ensamble los documentos del PDF de entrada.
1. Extraiga los resultados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-Utilities.jar y jbossall-client.jar con archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creación de un cliente de ensamblador de PDF**

Para poder realizar una operación Assembler mediante programación, debe crear un cliente de servicio Assembler.

**Referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para ensamblar un documento PDF. Por ejemplo, considere el documento DDX que se introdujo en esta sección. Para ensamblar un documento de PDF que contenga identificadores de página únicos, el documento DDX debe contener la variable `BatesNumber` elemento.

**Documentos de PDF de entrada de referencia**

Se debe hacer referencia a los documentos del PDF de entrada para ensamblar un documento del PDF. Por ejemplo, se debe hacer referencia a los documentos map.pdf y addresses.pdf para ensamblar estos documentos de PDF en un solo documento de PDF.

**Establezca el valor de número de Bates inicial**

Puede configurar el valor inicial del número de Bates para satisfacer sus necesidades comerciales. Por ejemplo, supongamos que es un requisito establecer el valor inicial en 000100. Si no establece el valor inicial, el valor de la primera página es 00000.

**Montaje de los documentos del PDF de entrada**

Después de crear el cliente de servicio Assembler, haga referencia al documento DDX que contiene `BatesNumber` información del elemento, referencia a un documento de PDF de entrada y definición de opciones de tiempo de ejecución, puede invocar la variable `invokeDDX` operación que resulta en que el servicio Assembler ensambla un documento PDF que contiene identificadores de página únicos.

**Extraer los resultados**

El servicio Assembler devuelve un objeto de colección que contiene los resultados del trabajo. Puede extraer el documento de PDF resultante y cualquier excepción que se produzca. En este caso, un documento de PDF cifrado se encuentra dentro del objeto de colección.

>[!NOTE]
>
>Si invoca el objeto `invokeDDX` operación. Esta operación se utiliza al pasar dos o más documentos de PDF de entrada al servicio Assembler. Sin embargo, si solo pasa un documento de PDF de entrada al servicio Assembler, debe invocar la variable `invokeOneDocument` operación. Para obtener información sobre el uso de esta operación, consulte [Montaje de documentos de PDF cifrados](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**Consulte también lo siguiente**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montaje de documentos con numeración Bates mediante la API de Java {#assemble-documents-with-bates-numbering-using-the-java-api}

Ensamble un documento de PDF que utilice identificadores de página únicos (numeración Bates) mediante la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-assembler-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de ensamblador de PDF.

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `AssemblerServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Haga referencia a un documento DDX existente.

   * Cree un `java.io.FileInputStream` objeto que representa el documento DDX utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo DDX.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Documentos de PDF de entrada de referencia.

   * Cree un `java.util.Map` objeto utilizado para almacenar documentos del PDF de entrada mediante un `HashMap` constructor.
   * Para cada documento del PDF de entrada, cree un `java.io.FileInputStream` usando su constructor y pasando la ubicación del documento del PDF de entrada. En este caso, pase la ubicación de un documento PDF no protegido.
   * Para cada documento del PDF de entrada, cree un `com.adobe.idp.Document` y pase el `java.io.FileInputStream` objeto que contiene el documento PDF.
   * Agregue una entrada al `java.util.Map` invocando su `put` y pasando los siguientes argumentos:

      * Un valor de cadena que representa el nombre de la clave. Este valor debe coincidir con el valor del elemento de origen del PDF especificado en el documento DDX. Por ejemplo, el nombre del archivo de origen del PDF especificado en el documento DDX que se introduce en esta sección es Loan.pdf.
      * A `com.adobe.idp.Document` objeto que contiene el documento PDF no protegido.

1. Establezca el valor de número de Bates inicial.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Establezca el número de Bates inicial invocando la variable `AssemblerOptionSpec` del objeto `setFirstBatesNumber` y pasando un valor numérico que especifica el valor inicial.

1. Ensamble los documentos del PDF de entrada.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores obligatorios:

   * A `com.adobe.idp.Document` que representa el documento DDX.
   * A `java.util.Map` objeto que contiene el archivo PDF de entrada no protegido.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica las opciones en tiempo de ejecución, incluidos el nivel predeterminado de fuente y registro de trabajos.

   La variable `invokeDDX` el método devuelve un `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contiene un documento de PDF cifrado con contraseña.

1. Extraiga los resultados.

   Para obtener el documento de PDF recién creado, realice las siguientes acciones:

   * Invocar el `AssemblerResult` del objeto `getDocuments` método. Esta acción devuelve un `java.util.Map` objeto.
   * Iterar a través de la variable `java.util.Map` hasta que encuentre la variable `com.adobe.idp.Document` objeto.
   * Invocar el `com.adobe.idp.Document` del objeto `copyToFile` método para extraer el documento PDF.

**Consulte también lo siguiente**

[Inicio rápido (modo SOAP): Montaje de un documento PDF con numeración de fechas mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montaje de documentos con numeración Bates mediante la API de servicio web {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Ensamble un documento de PDF que utilice identificadores de página únicos (numeración Bates) mediante la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento DDX y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Documentos de PDF de entrada de referencia.

   * Para cada documento del PDF de entrada, cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento del PDF de entrada.
   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento del PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.
   * Cree un `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de colección se utiliza para almacenar los documentos del PDF de entrada.
   * Para cada documento del PDF de entrada, cree un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto. Por ejemplo, si se utilizan dos documentos de PDF de entrada, cree dos `MyMapOf_xsd_string_To_xsd_anyType_Item` objetos.
   * Asigne un valor de cadena que represente el nombre de clave a la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` campo . Este valor debe coincidir con el valor del elemento de origen del PDF especificado en el documento DDX. (Realice esta tarea para cada documento del PDF de entrada).
   * Asigne la variable `BLOB` objeto que almacena el documento del PDF en el `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` campo . (Realice esta tarea para cada documento del PDF de entrada).
   * Agregue la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` al `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invocar el `MyMapOf_xsd_string_To_xsd_anyType` del objeto `Add` y pase el `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Realice esta tarea para cada documento del PDF de entrada).

1. Establezca el valor de número de Bates inicial.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Establezca el número de Bates inicial asignando un valor numérico a la variable `firstBatesNumber` miembro de datos que pertenece al grupo `AssemblerOptionSpec` objeto.

1. Ensamble los documentos del PDF de entrada.

   Invocar el `AssemblerServiceClient` del objeto `invoke` y pase los siguientes valores:

   * A `BLOB` que representa el documento DDX.
   * La variable `MyMapOf_xsd_string_To_xsd_anyType` que contiene los documentos del PDF de entrada. Sus claves deben coincidir con los nombres de los archivos de origen del PDF, y sus valores deben ser `BLOB` objetos que correspondan a esos archivos.
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución.

   La variable `invoke` devuelve un valor `AssemblerResult` que contiene los resultados del trabajo y cualquier excepción que se haya producido.

1. Extraiga los resultados.

   Para obtener el documento de PDF recién creado, realice las siguientes acciones:

   * Acceda a la `AssemblerResult` del objeto `documents` , que es un `Map` que contiene los documentos del PDF de resultados.
   * Iterar a través de la variable `Map` hasta que encuentre la clave que coincida con el nombre del documento resultante. A continuación, cree el `value` a `BLOB`.
   * Extraiga los datos binarios que representan el documento del PDF accediendo a su `BLOB` del objeto `MTOM` propiedad. Esto devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
