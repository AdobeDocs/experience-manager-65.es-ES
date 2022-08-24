---
title: Reader que amplía documentos de PDF protegidos por políticas utilizando la Biblioteca de Protección Portátil
seo-title: Reader extending policy-protected PDF documents using Portable Protection Library
description: Las extensiones de Reader permiten funciones interactivas en documentos de Adobe PDF a través de Acrobat Reader. Puede utilizar la biblioteca de protección portátil (PPL) para que el lector amplíe los documentos de PDF protegidos DRM.
seo-description: Reader extensions enable interactive features in Adobe PDF documents through Acrobat Reader. You can use the Portable Protection Library (PPL) to reader extend the DRM protected PDF documents.
uuid: 0da17641-d24c-43c2-b918-8b5abe1e5473
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 83ca522e-d16e-4196-9aa7-84f85de8dee2
feature: Document Security
exl-id: fe5d83e8-5e36-4146-a20a-dab2213055e2
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Reader que amplía documentos de PDF protegidos por políticas utilizando la Biblioteca de Protección Portátil {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

Debe estar familiarizado con los conceptos de seguridad de documentos, extensión de lectura y lenguaje de programación Java para que el lector amplíe los documentos PDF protegidos por políticas de seguridad de documentos.

Puede utilizar la seguridad de los documentos para restringir el acceso de documentos de PDF específicos únicamente a usuarios autorizados. También puede determinar cómo un destinatario puede utilizar un documento protegido. Por ejemplo, puede especificar si los destinatarios pueden imprimir, copiar o editar texto de un documento protegido por políticas de seguridad de documentos. Para obtener más información sobre la seguridad de los documentos, consulte [acerca de la seguridad del documento](/help/forms/using/admin-help/document-security.md).

Puede utilizar extensiones de lector para habilitar funciones interactivas en documentos de Adobe PDF mediante Acrobat Reader. Estas funciones interactivas normalmente están disponibles solo a través de Adobe Acrobat Professional y Standard. Para obtener más información sobre las funciones interactivas que puede habilitar la extensión de lectura, consulte [Servicio DocAssurance de Adobe Experience Manager Forms ](/help/forms/using/overview-aem-document-services.md)**.**

Puede utilizar la biblioteca de protección portátil para aplicar políticas en el documento sin necesidad de que el documento viaje por la red. Sólo las credenciales de seguridad y los detalles de la política de protección viajan a través de la red. El documento real nunca sale del cliente y las políticas de protección se aplican localmente en el cliente.

## Reader que amplía documentos de PDF protegidos por políticas de seguridad de documentos {#reader-extending-document-security-policy-protected-pdf-documents}

Los documentos protegidos por políticas son documentos cifrados. No puede utilizar API estándar de extensión de lectura para aplicar, quitar y recuperar derechos de uso de documentos de PDF protegidos por políticas. Solo el servicio Reader Extensions de la biblioteca de protección portátil proporciona API para aplicar, quitar y recuperar derechos de uso de documentos PDF protegidos por políticas de seguridad de documentos.

### Servicio de extensiones de Reader {#reader-extensions-service}

El servicio de extensión de lectura agrega derechos de uso a un documento de PDF protegido por políticas, activando características que normalmente no están disponibles cuando se abre un documento de PDF con Adobe Acrobat Reader. También tiene API para eliminar y recuperar los derechos de uso de un documento protegido por políticas.

El servicio Reader Extensions admite totalmente documentos PDF basados en el PDF estándar 1.6 y posteriores. Aparte de Acrobat Reader, los usuarios de terceros no necesitan ningún software o complemento adicional para utilizar los documentos de PDF protegidos por políticas.

Puede realizar las siguientes tareas con el servicio Reader Extensions:

* Aplique derechos de uso a un documento de PDF protegido por políticas.
* Elimine los derechos de uso de un documento de PDF protegido por políticas.
* Recupere los derechos de uso aplicados a un documento de PDF protegido por políticas.

### Aplicar derechos de uso a un documento de PDF protegido por políticas de seguridad de documento {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

Puede usar la variable `applyUsageRights`API de Java para aplicar derechos de uso a documentos de PDF protegidos por políticas. Los derechos de uso pertenecen a funciones que están disponibles de forma predeterminada en Acrobat pero no en Adobe Reader, como la capacidad de agregar comentarios a un formulario o de rellenar los campos del formulario y guardar el formulario. Los documentos del PDF que tienen derechos de uso aplicados se denominan documentos habilitados para derechos. Un usuario que abre un documento con derechos activados en Adobe Reader puede realizar operaciones que estén habilitadas para ese documento específico.

**Sintaxis:** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parámetro</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p>inputFile</p> </td>
   <td><p>Especifique InputStream que representa el documento del PDF al que se deben aplicar los derechos de uso. Puede utilizar el Rights Management de LiveCycle o los documentos protegidos por seguridad de documentos de AEM Forms.</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>Especifique el objeto File que representa un archivo .jks. El archivo .jks es un archivo de almacén de claves. Señala a un certificado que concede derechos de uso.</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>Especifique la contraseña del almacén de claves. </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p>Especifica un objeto de tipo <a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">DerechosDeUso</a>. El objeto usageRights representa derechos individuales que pueden aplicarse a un documento de PDF protegido por políticas.</p> </td>
  </tr>
 </tbody>
</table>

### Recupere los derechos de uso aplicados a un documento de PDF protegido por políticas.   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

Puede usar la variable `getDocumentUsageRights`API de Java para recuperar los derechos de uso de la extensión de lectura aplicados a un documento de PDF protegido por políticas. Al recuperar información sobre los derechos de uso, puede obtener información sobre la extensión del lector de funciones habilitada para el documento de PDF protegido por políticas.

**Sintaxis:** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parámetro</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>Especifique InputStream que representa el documento del PDF desde el que se van a recuperar los derechos de uso. Puede utilizar el Rights Management de LiveCycle o los documentos protegidos por seguridad de documentos de AEM Forms.</p> </td>
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

System.out.println("UsageRights applied successfully to the document. ");
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

### Eliminación de los derechos de uso de un documento de PDF protegido por políticas {#remove-usage-rights-of-a-policy-protected-pdf-document}

Puede usar la variable `removeUsageRights`API de Java para eliminar los derechos de uso de un documento protegido por políticas. La eliminación de los derechos de uso de un documento de PDF protegido por políticas es necesaria para realizar otras operaciones de AEM Forms en el documento. Por ejemplo, debe firmar digitalmente (o certificar) un documento PDF antes de establecer los derechos de uso. Por lo tanto, si desea realizar operaciones en un documento protegido por políticas, debe eliminar los derechos de uso del documento PDF, realizar las demás operaciones, como firmar digitalmente el documento y, a continuación, volver a aplicar los derechos de uso al documento.

**Sintaxis:** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parámetro</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>Especifique InputStream que representa el documento del PDF desde el que se utiliza<br /> se eliminarán. Puede utilizar el Rights Management de LiveCycle o los documentos protegidos por seguridad de documentos de AEM Forms.</td>
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
System.out.println("RE rights removed successfully from the document.");
outputStream.close();
inputFileStream.close();
```
