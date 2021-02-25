---
title: Validación de un documento DDX mediante la API de servicio web
seo-title: Validación de un documento DDX mediante la API de servicio web
description: Utilice la API de servicio de ensamblador para validar un documento DDX.
seo-description: Utilice la API de servicio de ensamblador para validar un documento DDX.
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---


# Validar un documento DDX mediante la API de servicio Web {#validate-a-ddx-document-using-theweb-service-api}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en el entorno JEE.**

Valide un documento DDX mediante la API de servicio de ensamblador (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar localhost con la dirección IP del servidor de formularios.

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
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Configure las opciones de tiempo de ejecución para validar el documento DDX.

   * Cree un objeto `AssemblerOptionSpec` que almacene las opciones de tiempo de ejecución mediante su constructor.
   * Establezca la opción de tiempo de ejecución que indica al servicio Ensamblador que valide el documento DDX asignando el valor true al miembro de datos `AssemblerOptionSpec` del objeto `validateOnly`.
   * Configure la cantidad de información que el servicio Ensamblador escribe en el archivo de registro asignando un valor de cadena al miembro de datos `AssemblerOptionSpec` del objeto `logLevel`. al validar un documento DDX, desea que se escriba más información en el archivo de registro que le ayudará en el proceso de validación. Como resultado, puede especificar el valor `FINE` o `FINER`. Para obtener información sobre las opciones de tiempo de ejecución que puede establecer, consulte la referencia de clase `AssemblerOptionSpec` en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Realice la validación.

   Invoque el método `AssemblerServiceClient` del objeto `invokeDDX` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX.
   * El valor `null` del objeto `Map` que generalmente almacena documentos PDF.
   * Un objeto `AssemblerOptionSpec` que especifica opciones de tiempo de ejecución.

   El método `invokeDDX` devuelve un objeto `AssemblerResult` que contiene información que especifica si el documento DDX es válido.

1. Guarde los resultados de validación en un archivo de registro.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo de registro y el modo en el que se abrirá el archivo. Asegúrese de que la extensión del nombre de archivo sea .xml.
   * Cree un objeto `BLOB` que almacene información de registro obteniendo el valor del miembro de datos `AssemblerResult` del objeto `jobLog`.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB`. Rellene la matriz de bytes obteniendo el valor del campo `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

   >[!NOTE]
   >
   >Si el documento DDX no es válido, se genera un `OperationException`. Dentro de la sentencia catch, puede obtener el valor del miembro `OperationException` del objeto `jobLog`.

**Consulte también**

[Validación de Documentos DDX](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
