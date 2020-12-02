---
title: Reader ampliando documentos PDF protegidos por políticas mediante la biblioteca de protección portátil
seo-title: Reader ampliando documentos PDF protegidos por políticas mediante la biblioteca de protección portátil
description: Las extensiones de Reader habilitan funciones interactivas en los documentos de Adobe PDF a través de Acrobat Reader. Puede utilizar la biblioteca de protección portátil (PPL) para que el lector extienda los documentos PDF protegidos con DRM.
seo-description: Las extensiones de Reader habilitan funciones interactivas en los documentos de Adobe PDF a través de Acrobat Reader. Puede utilizar la biblioteca de protección portátil (PPL) para que el lector extienda los documentos PDF protegidos con DRM.
uuid: 0da17641-d24c-43c2-b918-8b5abe1e5473
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 83ca522e-d16e-4196-9aa7-84f85de8dee2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---


# Reader extendiendo documentos PDF protegidos por políticas mediante la biblioteca de protección portátil {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

Debe estar familiarizado con los conceptos de seguridad de documento, extensión de lector y lenguaje de programación Java para que el lector pueda ampliar los documentos PDF protegidos por políticas de seguridad de documento.

Puede utilizar la seguridad de documento para restringir el acceso de documentos PDF específicos solo a usuarios autorizados. También puede determinar cómo un destinatario puede utilizar un documento protegido. Por ejemplo, puede especificar si los destinatarios pueden imprimir, copiar o editar texto de un documento protegido por una política de seguridad de documento. Para obtener más información sobre la seguridad de documento, consulte [acerca de la seguridad de documento](/help/forms/using/admin-help/document-security.md).

Puede utilizar extensiones de lector para activar funciones interactivas en Adobe PDF documento a través de Acrobat Reader. Estas funciones interactivas normalmente solo están disponibles a través de Adobe Acrobat Professional y Standard. Para obtener más información sobre las funciones interactivas que la extensión de lector puede habilitar, consulte [Servicio de Adobe Experience Manager Forms DocAssurance ](/help/forms/using/overview-aem-document-services.md)**.**

Puede utilizar la biblioteca de protección portátil para aplicar políticas en el documento sin necesidad de documentos que viajen por la red. Sólo las credenciales de seguridad y los detalles de la política de protección viajan por la red. El documento real nunca sale del cliente y las políticas de protección se aplican localmente en el cliente.

## Reader extendiendo documentos PDF protegidos por políticas de seguridad de documento {#reader-extending-document-security-policy-protected-pdf-documents}

Los documentos protegidos por políticas son documentos cifrados. No se pueden usar API de extensión de lector estándar para aplicar, quitar y recuperar derechos de uso de documentos PDF protegidos por políticas. Solo el servicio Extensiones de Reader de la biblioteca de protección portátil proporciona API para aplicar, quitar y recuperar derechos de uso de documentos PDF protegidos por políticas de seguridad de documento.

### Servicio Extensiones de Reader {#reader-extensions-service}

El servicio de extensión de lector agrega derechos de uso a un documento PDF protegido por una política, activando funciones que normalmente no están disponibles cuando se abre un documento PDF con Adobe Acrobat Reader. También tiene API para eliminar y recuperar los derechos de uso de un documento protegido por una política.

El servicio Reader Extensions admite totalmente documentos PDF basados en el estándar PDF 1.6 y posterior. Aparte de Acrobat Reader, los usuarios de terceros no necesitan ningún software o complemento adicional para utilizar los documentos PDF protegidos por políticas.

Puede realizar las siguientes tareas con el servicio Reader Extensions:

* Aplique derechos de uso a un documento PDF protegido por una política.
* Elimine los derechos de uso de un documento PDF protegido por una política.
* Recupere los derechos de uso aplicados a un documento PDF protegido por una política.

### Aplicar derechos de uso a un documento PDF protegido por una política de seguridad de documento {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

Puede utilizar la API de `applyUsageRights`Java para aplicar derechos de uso a documentos PDF protegidos por políticas. Los derechos de uso se refieren a la funcionalidad que está disponible de forma predeterminada en Acrobat pero no en Adobe Reader, como la capacidad de agregar comentarios a un formulario o de rellenar los campos del formulario y guardar el formulario. Los documentos PDF que tienen derechos de uso aplicados se denominan documentos habilitados para derechos. Un usuario que abre un documento con derechos activados en Adobe Reader puede realizar operaciones habilitadas para ese documento específico.

**Sintaxis:** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parámetro</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p>inputFile</p> </td>
   <td><p>Especifique InputStream que represente el documento PDF al que se van a aplicar los derechos de uso. Puede utilizar documentos protegidos por seguridad de LiveCycle Rights Management o AEM Forms documento.</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>Especifique el objeto File que representa un archivo .jks. El archivo .jks es un archivo de almacén de claves. Apunta a un certificado que concede derechos de uso.</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>Especifique la contraseña del almacén de claves. </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p>Especifica un objeto de tipo <a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">UsageRights</a>. El objeto usageRights representa derechos individuales que se pueden aplicar a un documento PDF protegido por una política.</p> </td>
  </tr>
 </tbody>
</table>

### Recupere los derechos de uso aplicados a un documento PDF protegido por una política.   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

Puede utilizar la API de `getDocumentUsageRights`Java para recuperar los derechos de uso de la extensión de lectura aplicados a un documento PDF protegido por una política. Al recuperar información sobre los derechos de uso, puede obtener información sobre las características que la extensión del lector ha habilitado para el documento PDF protegido por políticas.

**Sintaxis:** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parámetro</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>Especifique InputStream que represente el documento PDF desde el que se van a recuperar los derechos de uso. Puede utilizar documentos protegidos por seguridad de LiveCycle Rights Management o AEM Forms documento.</p> </td>
  </tr>
 </tbody>
</table>

#### Ejemplo de código {#code-sample}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\protected.pdf"; //Input file can be RM protected or unprotected pdf file
File certFile = new File("C:\\Sample\\cert.jks"); //RE certificate file
String password = "password"; //password for RE certificate
UsageRights usageRights = getUsageRights(true,true,false,false,true,true,false,false,false,false,true);

//RE rights to be applied on the file : FormFillIn, FormDataImportExport, SubmitStandalone, OnlineForms, DynamicFormField, DynamicFormPages, BarcodeDecoding, DigitalSignatures, Comments, CommentsOnline, EmbeddedFiles

InputStream inputFileStream = new FileInputStream(inputFileName);
InputStream output = rmClient2.getRightsManagementReaderExtensionService().applyUsageRights(inputFileStream, certFile, credentialPassword, rights);

String outputFileName = "C:\\Sample\\ReAdded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = output.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}

System.out.println("UsageRights applied successfully to the document. ”);
 outputStream.close();
inputFileStream.close();

//Get Usage Rights for the output pdf document
InputStream fileWithRe = new FileInputStream(myFile);

GetUsageRightsResult usageRights = rmClient2.getRightsManagementReaderExtensionService().getDocumentUsageRights(fileWithRe);

UsageRights rights = usageRights.getRights();
String right1 = rights1.toString();
System.out.println("RE rights for the file are :\n"+right1);
 fileWithRe.close();
```

### Eliminar los derechos de uso de un documento PDF protegido por una política {#remove-usage-rights-of-a-policy-protected-pdf-document}

Puede utilizar la API de `removeUsageRights`Java para eliminar los derechos de uso de un documento protegido por una política. La eliminación de los derechos de uso de un documento PDF protegido por una política es necesaria para realizar otras operaciones de AEM Forms en el documento. Por ejemplo, debe firmar digitalmente (o certificar) un documento PDF antes de definir los derechos de uso. Por lo tanto, si desea realizar operaciones en un documento protegido por una política, debe quitar los derechos de uso del documento PDF, realizar las demás operaciones, como firmar digitalmente el documento y, a continuación, volver a aplicar los derechos de uso al documento.

**Sintaxis:** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parámetro</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>Especifique InputStream que represente el documento PDF del que se eliminarán los derechos de uso<br />. Puede utilizar documentos protegidos por seguridad de LiveCycle Rights Management o AEM Forms documento.</td>
  </tr>
 </tbody>
</table>

#### Ejemplo de código {#code-sample-1}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\fileWithRe.pdf"; //Input file can be RM protected or unprotected pdf file
InputStream inputFileStream = new FileInputStream(inputFileName);

InputStream fileStream = rmClient2.getRightsManagementReaderExtensionService().removeUsageRights(inputFileStream);

String outputFileName = "C:\\Sample\\ReRemoveded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = fileStream.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}
System.out.println("RE rights removed successfully from the document.”);
outputStream.close();
inputFileStream.close();
```

