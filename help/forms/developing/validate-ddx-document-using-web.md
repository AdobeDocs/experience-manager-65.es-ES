---
title: Validación de un documento DDX mediante la API de servicio web
seo-title: Validate a DDX document using theweb service API
description: Utilice la API de servicio del ensamblador para validar un documento DDX.
seo-description: Use the Assembler Service API to validate a DDX document.
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
role: Developer
exl-id: 069e5b10-ab93-4492-a70d-6a0d462105a6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# Validación de un documento DDX mediante la API de servicio web {#validate-a-ddx-document-using-theweb-service-api}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

Valide un documento DDX utilizando la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace localhost por la dirección IP del servidor de formularios.

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
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo para leer.
   * Rellene el `BLOB` asignando su `MTOM` con el contenido de la matriz de bytes.

1. Defina las opciones en tiempo de ejecución para validar el documento DDX.

   * Cree un `AssemblerOptionSpec` que almacena opciones en tiempo de ejecución mediante su constructor.
   * Establezca la opción en tiempo de ejecución que indica al servicio Assembler que valide el documento DDX asignando el valor true al `AssemblerOptionSpec` del objeto `validateOnly` miembro de datos.
   * Establezca la cantidad de información que el servicio Assembler escribe en el archivo de registro asignando un valor de cadena al `AssemblerOptionSpec` del objeto `logLevel` miembro de datos. método Al validar un documento DDX, desea que se escriba más información en el archivo de registro que ayudará en el proceso de validación. Como resultado, puede especificar el valor `FINE` o `FINER`. Para obtener información sobre las opciones de tiempo de ejecución que puede establecer, consulte la `AssemblerOptionSpec` referencia de clase en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Realice la validación.

   Invocar el `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * A `BLOB` que representa el documento DDX.
   * El valor `null` para el `Map` que generalmente almacena documentos PDF.
   * Un `AssemblerOptionSpec` objeto que especifica opciones en tiempo de ejecución.

   La variable `invokeDDX` devuelve un valor `AssemblerResult` objeto que contiene información que especifica si el documento DDX es válido.

1. Guarde los resultados de validación en un archivo de registro.

   * Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo de registro y el modo en el que se abre el archivo. Asegúrese de que la extensión del nombre de archivo es .xml.
   * Cree un `BLOB` objeto que almacena información de registro obteniendo el valor de la variable `AssemblerResult` del objeto `jobLog` miembro de datos.
   * Cree una matriz de bytes que almacene el contenido del `BLOB` objeto. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` campo .
   * Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

   >[!NOTE]
   >
   >Si el documento DDX no es válido, `OperationException` se lanza. Dentro de la sentencia catch, puede obtener el valor de la variable `OperationException` del objeto `jobLog` miembro.

**Consulte también lo siguiente**

[Validación de documentos DDX](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
