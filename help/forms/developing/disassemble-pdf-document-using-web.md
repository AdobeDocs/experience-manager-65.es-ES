---
title: Desmontaje de un documento de PDF mediante la API de servicio Web
seo-title: Disassemble a PDF document usingthe web service API
description: Desmontaje de un documento de PDF mediante la API de servicio del ensamblador
seo-description: Disassemble a PDF document using the Assembler Service API
uuid: d6283dc5-e333-49d0-abde-1d390662f4fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/programmatically_disassembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 49584fb4-8c3a-4d73-acd6-0879a67f6093
role: Developer
exl-id: de2f90ad-5dea-40a0-8c6d-d6b08228310d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---

# Desmontaje de un documento de PDF mediante la API de servicio web {#disassemble-a-pdf-document-usingthe-web-service-api}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

Desmonte un documento del PDF utilizando la API del servicio Assembler (servicio Web):

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
   * Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento DDX y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia a un documento del PDF para desmontarlo.

   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar el documento del PDF de entrada. Esta `BLOB` se pasa al `invokeOneDocument` como argumento.
   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` campo el contenido de la matriz de bytes.
   * Cree un `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de colección se utiliza para almacenar el PDF que se va a desmontar.
   * Cree un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Asigne un valor de cadena que represente el nombre de clave a la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` campo . Este valor debe coincidir con el valor del elemento de origen del PDF especificado en el documento DDX.
   * Asigne la variable `BLOB` objeto que almacena el documento del PDF en el `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` campo .
   * Agregue la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` al `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invocar el `MyMapOf_xsd_string_To_xsd_anyType` object’ `Add` y pase el `MyMapOf_xsd_string_To_xsd_anyType` objeto.

1. Establezca las opciones de tiempo de ejecución.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Configure las opciones en tiempo de ejecución para satisfacer los requisitos empresariales asignando un valor a un miembro de datos que pertenezca al grupo `AssemblerOptionSpec` objeto. Por ejemplo, para solicitar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` a `AssemblerOptionSpec` del objeto `failOnError` campo .

1. Desmonte el documento del PDF.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * A `BLOB` objeto que representa el documento DDX que desmonta el documento PDF
   * La variable `MyMapOf_xsd_string_To_xsd_anyType` objeto que contiene el documento del PDF que se va a desmontar
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución

   La variable `invokeDDX` devuelve un valor `AssemblerResult` objeto que contiene los resultados del trabajo y cualquier excepción que se haya producido.

1. Guarde los documentos de PDF desmontados.

   Para obtener los documentos de PDF recién creados, realice las siguientes acciones:

   * Acceda a la `AssemblerResult` del objeto `documents` , que es un `Map` que contiene los documentos de PDF desmontados.
   * Iterar a través de la variable `Map` para obtener cada documento resultante. A continuación, cree el `value` a `BLOB`.
   * Extraiga los datos binarios que representan el documento del PDF accediendo a su `BLOB` del objeto `MTOM` propiedad. Esto devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también lo siguiente**

[Desmontaje programático de documentos PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
