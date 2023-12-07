---
title: Desagrupar de un documento de PDF mediante la API de servicio web
description: Desmontar un documento de PDF mediante la API del servicio Assembler
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/programmatically_disassembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Developer
exl-id: de2f90ad-5dea-40a0-8c6d-d6b08228310d
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---

# Desagrupar de un documento PDF mediante la API de servicio web {#disassemble-a-pdf-document-usingthe-web-service-api}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Desmontar un documento de PDF mediante la API del servicio Assembler (servicio web):

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
   * Crear un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación de archivo del documento DDX y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Hacer referencia a un documento de PDF para desmontar.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el documento del PDF de entrada. Esta `BLOB` El objeto se pasa a `invokeOneDocument` como argumento.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento del PDF de entrada y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `MTOM` el contenido de la matriz de bytes.
   * Crear un `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de colección se utiliza para almacenar el PDF que se va a desmontar.
   * Crear un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Asigne un valor de cadena que represente el nombre de clave al `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` field. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
   * Asigne el `BLOB` que almacena el documento del PDF en `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` field.
   * Añada el `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto a `MyMapOf_xsd_string_To_xsd_anyType` objeto. Invoque el `MyMapOf_xsd_string_To_xsd_anyType` objeto&quot; `Add` y pase el `MyMapOf_xsd_string_To_xsd_anyType` objeto.

1. Establecer opciones en tiempo de ejecución.

   * Crear un `AssemblerOptionSpec` que almacena las opciones en tiempo de ejecución mediante su constructor.
   * Establezca las opciones en tiempo de ejecución para satisfacer sus necesidades empresariales asignando un valor a un miembro de datos que pertenezca a `AssemblerOptionSpec` objeto. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne a `false` a la `AssemblerOptionSpec` del objeto `failOnError` field.

1. Desmontar el documento del PDF.

   Invoque el `AssemblerServiceClient` del objeto `invokeDDX` y pasar los siguientes valores:

   * A `BLOB` que representa el documento DDX que desmonta el documento de PDF
   * El `MyMapOf_xsd_string_To_xsd_anyType` que contiene el documento de PDF que se va a desmontar
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución

   El `invokeDDX` El método devuelve un `AssemblerResult` que contiene los resultados del trabajo y las excepciones que se han producido.

1. Guarde los documentos del PDF desmontados.

   Para obtener los documentos del PDF recién creados, realice las siguientes acciones:

   * Acceda a la `AssemblerResult` del objeto `documents` , que es un `Map` que contiene los documentos de PDF desensamblados.
   * Itere a través de `Map` para obtener cada documento resultante. A continuación, convierta el de ese miembro de la matriz `value` a un `BLOB`.
   * Extraiga los datos binarios que representan el documento PDF accediendo a su `BLOB` del objeto `MTOM` propiedad. Devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Desmontaje programático de documentos PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
