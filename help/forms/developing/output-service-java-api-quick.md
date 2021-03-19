---
title: Inicio rápido de la API de Java del servicio de salida (SOAP)
seo-title: Inicio rápido de la API de Java del servicio de salida (SOAP)
description: Utilice el servicio de salida Inicio rápido de la API de Java (SOAP) para crear un documento PDF, crear un documento PDF basado en un archivo XDP de aplicación, crear un documento PDF/A, pasar documentos al servicio de salida, pasar un documento ubicado en el repositorio de AEM Forms al servicio de salida, crear un documento PDF basado en fragmentos, imprimir en un archivo, enviar un flujo de impresión a una impresora de red, crear varios archivos PDF, crear reglas de búsqueda, transformar un documento PDF.
seo-description: Utilice el servicio de salida Inicio rápido de la API de Java (SOAP) para crear un documento PDF, crear un documento PDF basado en un archivo XDP de aplicación, crear un documento PDF/A, pasar documentos al servicio de salida, pasar un documento ubicado en el repositorio de AEM Forms al servicio de salida, crear un documento PDF basado en fragmentos, imprimir en un archivo, enviar un flujo de impresión a una impresora de red, crear varios archivos PDF, crear reglas de búsqueda, transformar un documento PDF.
uuid: 34cb1fc7-50a9-4db8-aed1-dbd3480d1323
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f4415aeb-5c1b-4087-b60f-b2ea952c52b5
role: Desarrollador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1406'
ht-degree: 0%

---


# Inicio rápido de la API Java del servicio de salida (SOAP) {#output-service-java-api-quick-start-soap}

El inicio rápido de la API de Java (SOAP) está disponible para el servicio de salida.

[Inicio rápido (modo SOAP): Creación de un documento PDF mediante la API de Java](output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Inicio rápido (modo SOAP): Creación de un documento PDF basado en un archivo XDP de aplicación mediante la API de Java](output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api)

[Inicio rápido (modo SOAP): Creación de un documento PDF/A mediante la API de Java](output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[Inicio rápido (modo SOAP): Pasar documentos al servicio de salida mediante la API de Java](output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Inicio rápido (modo SOAP): Pasar un documento ubicado en el repositorio de AEM Forms al servicio de salida mediante la API de Java](output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inicio rápido (modo SOAP): Creación de un documento PDF basado en fragmentos mediante la API de Java](#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Inicio rápido (modo SOAP): Impresión en un archivo mediante la API de Java](#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[Inicio rápido (modo SOAP): Envío de un flujo de impresión a una impresora de red mediante la API de Java](output-service-java-api-quick.md#quick-start-soap-mode-sending-a-print-stream-to-a-network-printer-using-the-java-api)

[Inicio rápido (modo SOAP): Creación de varios archivos PDF mediante la API de Java](output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[Inicio rápido (modo SOAP): Creación de reglas de búsqueda mediante la API de Java](output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Inicio rápido (modo SOAP): Transformación de un documento PDF mediante la API de Java](output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

Las operaciones de AEM Forms se pueden realizar mediante la API con establecimiento inflexible de tipos de AEM Forms y el modo de conexión se debe establecer en SOAP.

>[!NOTE]
>
>Quick Starts ubicado en Programación con formularios AEM se basan en el sistema operativo Forms Server. Sin embargo, si está utilizando otro sistema operativo, como UNIX, reemplace las rutas específicas de Windows por rutas compatibles con el sistema operativo aplicable. Del mismo modo, si utiliza otro servidor de aplicaciones J2EE, asegúrese de especificar propiedades de conexión válidas. Consulte [Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## Inicio rápido (modo SOAP): Creación de un documento PDF mediante la API de Java {#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api}

El siguiente ejemplo de código Java crea un documento PDF llamado *Loan.pdf*. Este documento PDF se basa en un diseño de formulario denominado *Loan.xdp* y en un archivo de datos XML denominado *Loan.xml*. El *Loan.pdf* está escrito en C:\Adobe folder located on the J2EE application server hosting AEM Forms, no en el equipo cliente. (Consulte [Creación de documentos PDF](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents)).

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import com.adobe.livecycle.output.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
 public class CreatePDFDocument {
 
     public static void main(String[] args) {
 
         try{
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create an OutputClient object
         OutputClient outClient = new OutputClient(myFactory);
 
         //Reference form data
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
         Document inXMData = new Document (fileInputStream);
 
         //Set PDF run-time options
         PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
         outputOptions.setFileURI("C:\\Adobe\Loan.pdf");
 
         //Set rendering run-time options
         RenderOptionsSpec pdfOptions = new RenderOptionsSpec();
         pdfOptions.setLinearizedPDF(true);
         pdfOptions.setAcrobatVersion(AcrobatVersion.Acrobat_9);
 
         //Create a PDF document
         OutputResult outputDocument = outClient.generatePDFOutput(
             TransformationFormat.PDF,
             "Loan.xdp",
             "C:\\Adobe",
             outputOptions,
             pdfOptions,
             inXMData
         );
 
         //Retrieve the results of the operation
         Document metaData = outputDocument.getStatusDoc();
         File myFile = new File("C:\\Adobe\Output.xml");
         metaData.copyToFile(myFile);
         }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
     }
 }
 
```

## Inicio rápido (modo SOAP): Creación de un documento PDF basado en un archivo XDP de aplicación mediante la API de Java {#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api}

El siguiente ejemplo de código Java crea un documento PDF llamado *Loan.pdf*. Este documento PDF se basa en un diseño de formulario denominado *Loan.xdp* y en un archivo de datos XML denominado *Loan.xml*. El archivo XDP se implementa como parte de una aplicación de AEM Forms llamada `Applications/FormsApplication`. Observe que la ruta URI es `repository:///Applications/FormsApplication/1.0/FormsFolder/`. El *Loan.pdf* está escrito en C:\Adobe folder located on the J2EE application server hosting AEM Forms, no en el equipo cliente. (Consulte [Creación de documentos PDF](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents)).

>[!NOTE]
>
>Antes de ejecutar este inicio rápido, asegúrese de crear una aplicación de AEM Forms denominada Applications/FormsApplication. Cree una carpeta dentro de la aplicación denominada FormsFolder y coloque el archivo XDP en la carpeta . Para obtener más información, consulte [Generación de un documento PDF ](/help/forms/developing/creating-document-output-streams.md)*.*

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/Adobe/adobe_experience_manager_forms/SDK/client-libs/common
     *
     * <install directory>/Adobe/adobe_experience_manager_forms/SDK/client-libs/jboss
     *
     * <install directory>/Adobe/adobe_experience_manager_forms/jboss/bin/client
     *
     * If you want to invoke a remote AEM Forms instance and there is a
     * firewall between the client application and AEM Forms, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/Adobe/adobe_experience_manager_forms/SDK/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms library files" in Programming
     * with AEM Forms
     */
 import com.adobe.livecycle.output.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
 public class CreatePDFDocumentFromLCApp {
 
     public static void main(String[] args) {
 
         try{
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create an OutputClient object
         OutputClient outClient = new OutputClient(myFactory);
 
         //Reference form data
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
         Document inXMData = new Document (fileInputStream);
 
         //Set PDF run-time options
         PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
         outputOptions.setFileURI("C:\\Adobe\Loan.pdf");
 
         //Set rendering run-time options
         RenderOptionsSpec pdfOptions = new RenderOptionsSpec();
         pdfOptions.setLinearizedPDF(true);
         pdfOptions.setAcrobatVersion(AcrobatVersion.Acrobat_9);
 
         //Create a PDF document -- reference an XDP file named Loan.xdp that is deployed as part of
         //a AEM Forms application named Applications/FormsApplication. The XDP file is located
         //in a folder named FormsFolder
         OutputResult outputDocument = outClient.generatePDFOutput(
             TransformationFormat.PDF,
             "Loan.xdp",
             "repository:///Applications/FormsApplication/1.0/FormsFolder/",
             outputOptions,
             pdfOptions,
             inXMData
         );
 
         //Retrieve the results of the operation
         Document metaData = outputDocument.getStatusDoc();
         File myFile = new File("C:\\Adobe\Output.xml");
         metaData.copyToFile(myFile);
         }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
     }
 }
 
 
```

## Inicio rápido (modo SOAP): Pasar un documento ubicado en el Repositorio al servicio Output utilizando la API de Java {#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api}

El siguiente código Java recupera un archivo XDP del Repositorio y lo pasa al servicio Output dentro de la instancia `com.adobe.idp.Document` . El archivo XDP se implementa como parte de una aplicación de AEM Forms llamada `Applications/FormsApplication`. Observe que la ruta URI es `repository:///Applications/FormsApplication/1.0/FormsFolder/`.

>[!NOTE]
>
>La API del repositorio se utiliza para recuperar el archivo XDP de esta ubicación. (Consulte [Lectura de recursos](/help/forms/developing/aem-forms-repository.md#reading-resources)).

Fíjese también en que el valor raíz del contenido `repository:///Applications/FormsApplication/1.0/FormsFolder/` se pasa al método `OutputClient` del objeto `generatePDFOutput2` (el segundo parámetro). Este valor se pasa al servicio Output para informar al servicio Output de que el material colateral, como las imágenes, se almacena en esta ubicación.

>[!NOTE]
>
>Puede establecer el valor raíz del contenido del mismo modo que al invocar el método `generatePrintedOutput2`.

El *Loan.pdf* está escrito en C:\Adobe folder located on the J2EE application server hosting AEM Forms. (Consulte [Pasar documentos ubicados en el repositorio al servicio de salida](/help/forms/developing/creating-document-output-streams.md#passing-documents-located-in-the-repository-to-the-output-service)).

>[!NOTE]
>
>Antes de ejecutar este inicio rápido, asegúrese de crear una aplicación de AEM Forms denominada Applications/FormsApplication. Cree una carpeta dentro de la aplicación denominada FormsFolder y coloque el archivo XDP en la carpeta .

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe-repository-client.jar
     * 3. adobe-livecycle-client.jar
     * 4. adobe-usermanager-client.jar
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import com.adobe.livecycle.output.client.*;
 import com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient;
 
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
 public class CreatePDFFFromRepository {
 
     public static void main(String[] args) {
 
         try{
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create an OutputClient object
         OutputClient outClient = new OutputClient(myFactory);
 
         //Reference form data
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
         Document inXMData = new Document (fileInputStream);
 
         //Set PDF run-time options
         PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
         outputOptions.setFileURI("C:\\Adobe\Loan.pdf"); // this PDF form is saved on the server
 
         //Get the form design from the AEM Forms Repository
         Document formDesign =  GetFormDesign(myFactory);
 
         //Set rendering run-time options
         RenderOptionsSpec pdfOptions = new RenderOptionsSpec();
         pdfOptions.setLinearizedPDF(true);
         pdfOptions.setAcrobatVersion(AcrobatVersion.Acrobat_9);
 
         //Create a non-interactive PDF document
         OutputResult outputDocument = outClient.generatePDFOutput2(
             TransformationFormat.PDF,
             "repository:///Applications/FormsApplication/1.0/FormsFolder/",
             formDesign,
             outputOptions,
             pdfOptions,
             inXMData
         );
 
         //Save the non-interactive PDF form as a PDF file on the client computer
         Document pdfForm = outputDocument.getGeneratedDoc();
         File myFile = new File("C:\\Adobe\Loan.pdf");
         pdfForm.copyToFile(myFile);
         }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
     }
 
     // Retrieve the form design from the following Repository path:
     // /Applications/FormsApplication/1.0/FormsFolder/Loan.xdp
     private static Document GetFormDesign(ServiceClientFactory myFactory)
     {
     try{
 
         // Create a ResourceRepositoryClient object using the service client factory
         ResourceRepositoryClient repositoryClient = new ResourceRepositoryClient(myFactory);
 
         // Specify the path in the Repository to Loan.xdp
         String resourceUri =  "/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
 
         // Retrieve the XDP file
         Document doc = repositoryClient.readResourceContent(resourceUri);
 
            //Return the Document instance
            return  doc;
          }
 
         catch(Exception e)
         {
             e.printStackTrace();
         }
         return null;
     }
 }
 
 
 
```

## Inicio rápido (modo SOAP): Creación de un documento PDF mediante la API de Java {#quick_start_soap_mode_creating_a_pdf_document_using_the_java_api-1}

El siguiente ejemplo de código Java crea un documento PDF llamado *Loan.pdf*. Este documento PDF se basa en un diseño de formulario denominado *Loan.xdp* y en un archivo de datos XML denominado *Loan.xml*. El *Loan.pdf* está escrito en C:\Adobe folder located on the J2EE application server hosting AEM Forms, no en el equipo cliente. (Consulte [Creación de documentos PDF](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents)).

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import com.adobe.livecycle.output.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
 public class CreatePDFDocumentSOAP {
 
     public static void main(String[] args) {
 
     try{
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create an OutputClient object
         OutputClient outClient = new OutputClient(myFactory);
 
         //Reference form data
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
         Document inXMData = new Document (fileInputStream);
 
         //Set PDF run-time options
         PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
         outputOptions.setFileURI("C:\\Adobe\Loan.pdf");
 
         //Set rendering run-time options
         RenderOptionsSpec pdfOptions = new RenderOptionsSpec();
         pdfOptions.setLinearizedPDF(true);
         pdfOptions.setAcrobatVersion(AcrobatVersion.Acrobat_9);
 
         //Create a PDF document
         OutputResult outputDocument = outClient.generatePDFOutput(
             TransformationFormat.PDF,
             "Loan.xdp",
             "C:\\Adobe",
             outputOptions,
             pdfOptions,
             inXMData
         );
 
         //Retrieve the results of the operation
         Document metaData = outputDocument.getStatusDoc();
         File myFile = new File("C:\\Adobe\Output.xml");
         metaData.copyToFile(myFile);
         }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
     }
 }
```

## Inicio rápido (modo SOAP): Creación de un documento PDF/A mediante la API de Java {#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api}

El siguiente ejemplo de código Java crea un documento PDF/A llamado *LoanArchive.pdf*. Este documento PDF se basa en un diseño de formulario denominado *Loan.xdp* y en un archivo de datos XML denominado *Loan.xml*. El *LoanArchive.pdf* está escrito en C:\Adobe folder located on the J2EE application server hosting AEM Forms, no en el equipo cliente. (Consulte [Creación de documentos PDF/A](/help/forms/developing/creating-document-output-streams.md#creating-pdf-a-documents)).

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import com.adobe.livecycle.output.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class CreatePDFADocument {
 
     public static void main(String[] args) {
 
     try{
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create an OutputClient object
         OutputClient outClient = new OutputClient(myFactory);
 
         //Reference an XML data source to merge with the form design
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
         Document inXMData = new Document (fileInputStream);
 
         //Set PDF run-time options
         PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
         outputOptions.setFileURI("C:\\Adobe\LoanArchive.pdf");
 
         //Set rendering run-time options
         RenderOptionsSpec pdfAOptions = new RenderOptionsSpec();
         pdfAOptions.setPDFAConformance(PDFAConformance.A);
         pdfAOptions.setPDFARevisionNumber(PDFARevisionNumber.Revision_1);
 
 
         //Create a PDF/A document
         OutputResult outputDocument = outClient.generatePDFOutput(
             TransformationFormat.PDFA,
             "Loan.xdp",
             "C:\\Adobe",
             outputOptions,
             pdfAOptions,
             inXMData
         );
 
         //Write the results of the operation to OutputLog.xml
         Document resultData = outputDocument.getStatusDoc();
         File myFile = new File("C:\\Adobe\OutputLog.xml");
         resultData.copyToFile(myFile);
 
         }catch (Exception ee)
         {
             ee.printStackTrace();
         }
     }
 }
 
```

## Inicio rápido (modo SOAP): Pasar documentos al servicio de salida mediante la API de Java {#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api}

El siguiente inicio rápido de Java recupera el archivo *Loan.xdp* desde Content Services. Este archivo XDP se encuentra en `space /Company Home/Form Designs`. El archivo XDP se devuelve en una instancia `com.adobe.idp.Document`. La instancia `com.adobe.idp.Document` se pasa al servicio Output . El formulario no interactivo se guarda como un archivo PDF llamado *Loan.pdf *en el equipo cliente. Como la opción URI de archivo está establecida, el archivo PDF *Loan.pdf *también se guarda en el servidor de aplicaciones J2EE que aloja AEM Forms. (Consulte [Pasar documentos ubicados en Content Services ES2 al Output Service](/help/forms/developing/creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)).

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe-contentservices-client.jar
     * 3. adobe-livecycle-client.jar
     * 4. adobe-usermanager-client.jar
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import com.adobe.livecycle.contentservices.client.CRCResult;
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl;
 import com.adobe.livecycle.output.client.*;
 
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
 public class CreatePDFFFromContentServices {
 
     public static void main(String[] args) {
 
         try{
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create an OutputClient object
         OutputClient outClient = new OutputClient(myFactory);
 
         //Reference form data
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
         Document inXMData = new Document (fileInputStream);
 
         //Set PDF run-time options
         PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
         outputOptions.setFileURI("C:\\Adobe\Loan.pdf"); // this PDF form is saved on the server
 
         //Get the form design from Content Services
         Document formDesign =  GetFormDesign(myFactory);
 
         //Set rendering run-time options
         RenderOptionsSpec pdfOptions = new RenderOptionsSpec();
         pdfOptions.setLinearizedPDF(true);
         pdfOptions.setAcrobatVersion(AcrobatVersion.Acrobat_9);
 
         //Create a non-interactive PDF document
         OutputResult outputDocument = outClient.generatePDFOutput2(
             TransformationFormat.PDF,
             "C:\\Adobe",
             formDesign,
             outputOptions,
             pdfOptions,
             inXMData
         );
 
         //Save the non-interactive PDF form as a PDF file on the client computer
         Document pdfForm = outputDocument.getGeneratedDoc();
         File myFile = new File("C:\\Adobe\Loan.pdf");
         pdfForm.copyToFile(myFile);
         }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
     }
 
     //Retrieve the form design from Content Services ES2
     private static Document GetFormDesign(ServiceClientFactory myFactory)
     {
         try{
 
         //Create a DocumentManagementServiceClientImpl object
         DocumentManagementServiceClientImpl    docManager = new DocumentManagementServiceClientImpl(myFactory);
 
         //Specify the name of the store and the content to retrieve
            String storeName = "SpacesStore";
            String nodeName  = "/Company Home/Form Designs/Loan.xdp";
 
            //Retrieve /Company Home/Form Designs/Loan.xdp
            CRCResult content = docManager.retrieveContent(
                      storeName,
                      nodeName,
                      "");
 
            //Return the Document instance
             Document doc =content.getDocument();
             return  doc;
          }
 
         catch(Exception e)
         {
             e.printStackTrace();
         }
         return null;
     }
 }
 
```

## Inicio rápido (modo SOAP): Creación de un documento PDF basado en fragmentos utilizando la API de Java {#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api}

En el siguiente ejemplo de código Java se crea un documento PDF basado en un diseño de formulario ensamblado por el servicio Assembler. El servicio Assembler monta fragmentos ubicados en varios archivos XDP en un único diseño de formulario. La lógica de aplicación que invoca el servicio Assembler se encuentra en un método definido por el usuario llamado `GetFormDesign`. El formulario no interactivo se guarda como un archivo PDF llamado *Loan.pdf *en el equipo cliente. (Consulte [Creación de documentos PDF utilizando fragmentos](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)).

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     * 20. adobe-assembler-client.jar
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     *
     * This is the DDX file is used to assemble multiple XDP documents:
     * <?xml version="1.0" encoding="UTF-8"?>
     * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <XDP result="tuc018result.xdp">
     * <XDP source="tuc018_template_flowed.xdp">
     * <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
     * <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientPhysical" required="false"/>
     * <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientHealth" required="false"/>
     * </XDP>
     * </XDP>
     * </DDX>
     */
 import com.adobe.livecycle.assembler.client.AssemblerOptionSpec;
 import com.adobe.livecycle.assembler.client.AssemblerResult;
 import com.adobe.livecycle.assembler.client.AssemblerServiceClient;
 import com.adobe.livecycle.output.client.*;
 
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
 public class CreatePDFFromFragments {
 
     public static void main(String[] args) {
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an OutputClient object
             OutputClient outClient = new OutputClient(myFactory);
 
             //Reference form data
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
             Document inXMData = new Document (fileInputStream);
 
             //Set PDF run-time options
             PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
             outputOptions.setFileURI("C:\\Adobe\Loan.pdf"); // this PDF form is saved on the server
 
             //Get the form design from Assembler service
             Document formDesign =  GetFormDesign(myFactory);
 
             //Set rendering run-time options
             RenderOptionsSpec pdfOptions = new RenderOptionsSpec();
             pdfOptions.setLinearizedPDF(true);
             pdfOptions.setAcrobatVersion(AcrobatVersion.Acrobat_9);
 
             //Create a non-interactive PDF document
             OutputResult outputDocument = outClient.generatePDFOutput2(
                 TransformationFormat.PDF,
                 "C:\\Adobe",
                 formDesign,
                 outputOptions,
                 pdfOptions,
                 inXMData
             );
 
             //Save the non-interactive PDF form as a PDF file on the client computer
             Document pdfForm = outputDocument.getGeneratedDoc();
             File myFile = new File("C:\\Adobe\Loan.pdf");
             pdfForm.copyToFile(myFile);
             }
             catch (Exception ee)
             {
                 ee.printStackTrace();
             }
         }
 
         //Retrieve the form design from Assembler service
         private static Document GetFormDesign(ServiceClientFactory myFactory)
         {
             try{
 
                 //Create an AssemblerServiceClient object
                 AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
                 //Create a FileInputStream object based on an existing DDX file
                 FileInputStream myDDXFile = new FileInputStream("C:\\Adobe\fragmentDDX.xml");
 
                 //Create a Document object based on the DDX file
                 Document myDDX = new Document(myDDXFile);
 
                 //Create a Map object to store the input XDP files
                 Map inputs = new HashMap();
                 FileInputStream inSource = new FileInputStream("C:\\Adobe\tuc018_template_flowed.xdp");
                 FileInputStream inFragment1 = new FileInputStream("C:\\Adobe\tuc018_contact.xdp");
                 FileInputStream inFragment2 = new FileInputStream("C:\\Adobe\tuc018_patient.xdp");
 
                 //Create a Document object
                 Document myMapSource = new Document(inSource);
 
                 //Create a Document object
                 Document inFragment1Doc = new Document(inFragment1);
 
                 //Create a Document object
                 Document inFragment2Doc = new Document(inFragment2);
 
                 //Place all of the XDP files into the MAP
                 inputs.put("tuc018_template_flowed.xdp",myMapSource);
                 inputs.put("tuc018_contact.xdp",inFragment1Doc);
                 inputs.put("tuc018_patient.xdp",inFragment2Doc);
 
 
                 //Create an AssemblerOptionsSpec object
                 AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
                 assemblerSpec.setFailOnError(false);
 
                 //Submit the job to Assembler service
                 AssemblerResult jobResult = assemblerClient.invokeDDX(myDDX,inputs,assemblerSpec);
                 java.util.Map allDocs = jobResult.getDocuments();
 
                 //Retrieve the result PDF document from the Map object
                 Document outDoc = null;
 
                 //Iterate through the map object to retrieve the result XDP document
                 for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
                     // Retrieve the Map object?s value
                     Map.Entry e = (Map.Entry)i.next();
 
                     //Get the key name as specified in the
                     //DDX document
                     String keyName = (String)e.getKey();
                     if (keyName.equalsIgnoreCase("tuc018result.xdp"))
                     {
                         Object o = e.getValue();
                         outDoc = (Document)o;
 
                     }
                 }
 
             return outDoc;
             }catch (Exception e) {
                 e.printStackTrace();
             }
             return null;
         }
     }
 
 
```

## Inicio rápido (modo SOAP): Impresión en un archivo mediante la API de Java {#quick-start-soap-mode-printing-to-a-file-using-the-java-api}

El siguiente ejemplo de código Java imprime un flujo de salida en un archivo PostScript denominado *MortgageForm.ps*. (Consulte [Impresión en archivos](/help/forms/developing/creating-document-output-streams.md#printing-to-files)).

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import com.adobe.livecycle.output.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class PrintToFile {
 
     public static void main(String[] args) {
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an OutputClient object
             OutputClient outClient = new OutputClient(myFactory);
 
             //Reference XML data that represents form data
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
             Document inputXML = new Document(fileInputStream);
 
             //Set print run-time options required to print to a file
             PrintedOutputOptionsSpec printOptions = new PrintedOutputOptionsSpec();
             printOptions.setFileURI("C:\\Adobe\MortgageForm.ps");
 
             //Print the print stream to a PostScript file
             OutputResult outputDocument = outClient.generatePrintedOutput(
                     PrintFormat.PostScript,
                     "Loan.xdp",
                     "C:\\Adobe",
                     null,
                     printOptions,
                     inputXML);
 
             //Write the results of the operation to OutputLog.xml
             Document resultData = outputDocument.getStatusDoc();
             File myFile = new File("C:\\Adobe\OutputLog.xml");
             resultData.copyToFile(myFile);
             System.out.println("AEM Forms printed to MortgageForm.ps");
         }
     catch (Exception ee)
             {
             ee.printStackTrace();
         }
     }
 }
 
```

## Inicio rápido (modo SOAP): Envío de un flujo de impresión a una impresora de red mediante la API de Java {#quick-start-soap-mode-sending-a-print-stream-to-a-network-printer-using-the-java-api}

El siguiente ejemplo de código Java envía un flujo de impresión PostScript a una impresora de red denominada *\\Printer1\Printer*. Se envían dos copias a la impresora. (Consulte [Envío de emisiones de impresión a impresoras](/help/forms/developing/creating-document-output-streams.md#sending-print-streams-to-printers)).

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.output.client.*;
 
 public class SendToPrinter {
 
     public static void main(String[] args) {
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an OutputClient object
             OutputClient outClient = new OutputClient(myFactory);
 
             //Reference XML data that represents form data
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
             Document inputXML = new Document(fileInputStream);
 
             //Set print run-time options required to print to a file
             PrintedOutputOptionsSpec printOptions = new PrintedOutputOptionsSpec();
 
             //Set the number of copies to print
             printOptions.setCopies(2);
 
             //Turn on the Staple option
             printOptions.setStaple(Staple.on);
 
             //Create a PostScript output stream based on the form design named Loan.xdp and
             //the data located in the XML file
             OutputResult outputDocument = outClient.generatePrintedOutput(
                     PrintFormat.PostScript,
                     "Loan.xdp",
                     "C:\\Adobe",
                     "C:\\Adobe",
                     printOptions,
                     inputXML);
 
             //Get a Document object that stores the PostScript print stream
             Document psPrintStream = outputDocument.getGeneratedDoc();
 
             //Specify the print server and the printer name
             String printServer = "\\\ottprint";
             String printerName = "\\\ottprint\Balsom";
 
             //Send the PostScript print stream to the printer
             outClient.sendToPrinter(
                     psPrintStream,
                     PrinterProtocol.SharedPrinter,
                     printServer,
                     printerName);
             }
         catch (Exception ee)
             {
             ee.printStackTrace();
             }
     }
 }
 
```

## Inicio rápido (modo SOAP): Creación de varios archivos PDF mediante la API de Java {#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api}

El siguiente código Java crea varios archivos PDF para cada registro de datos ubicado en un archivo de datos XML denominado *Loan_data_batch.xml*. Los archivos se escriben en C:\Adobe directory. Los archivos PDF se escriben en C:\Adobe folder located on the J2EE application server hosting AEM Forms, no en el equipo cliente. (Consulte [Creación de varios archivos de salida](/help/forms/developing/creating-document-output-streams.md#creating-multiple-output-files)).

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.output.client.*;
 
 public class CreateBatchFiles {
 
     public static void main(String[] args) {
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an OutputClient object
             OutputClient outClient = new OutputClient(myFactory);
 
             //Reference form data that contains multiple records
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan_data_batch.xml");
             Document inXMData = new Document (fileInputStream);
 
             //Set run-time options to generate many PDF files
             PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
             outputOptions.setFileURI("C:\\Adobe\Loan.pdf");
             outputOptions.setGenerateManyFiles(true);
             outputOptions.setRecordName("LoanRecord");
 
 
             //Set rendering run-time options
             RenderOptionsSpec pdfOptions = new RenderOptionsSpec();
             pdfOptions.setCacheEnabled(new Boolean(true));
 
 
             //Create multiple PDF files
             OutputResult outputDocument = outClient.generatePDFOutput(
                 TransformationFormat.PDF,
                 "Loan.xdp",
                 "C:\\Adobe",
                 outputOptions,
                 pdfOptions,
                 inXMData
                 );
 
             //Retrieve the results of the operation
             Document metaData = outputDocument.getStatusDoc();
             File myFile = new File("C:\\Adobe\Output.xml");
             metaData.copyToFile(myFile);
             }
             catch (Exception ee)
             {
                 ee.printStackTrace();
             }
     }
 }
 
 
```

## Inicio rápido (modo SOAP): Creación de reglas de búsqueda mediante la API de Java {#quick-start-soap-mode-creating-search-rules-using-the-java-api}

El siguiente ejemplo de código Java crea dos patrones de texto que el servicio Output busca. El primer patrón de texto es Hipoteca. Si se encuentra, el servicio Output utiliza el diseño de formulario denominado *Mortgage.xdp*. El segundo patrón de texto es Automobile. Si se encuentra, el servicio Output utiliza el diseño de formulario denominado *AutomobileLoan.xdp*. Si no se encuentra ningún patrón de texto, el servicio Output utiliza el diseño de formulario predeterminado denominado* Loan.xdp. *(Consulte [Creación de reglas de búsqueda](/help/forms/developing/creating-document-output-streams.md#creating-search-rules)).

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import com.adobe.livecycle.output.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class CreateSearchRules {
 
     public static void main(String[] args) {
         try{
 
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an OutputClient object
             OutputClient outClient = new OutputClient(myFactory);
 
             //Reference form data
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
             Document inXMData = new Document (fileInputStream);
 
             //Define two text patterns
             Rule mortageRule = new Rule();
             mortageRule.setPattern("Mortgage");
             mortageRule.setForm("Mortgage.xdp");
 
             Rule automobileRule = new Rule();
             automobileRule.setPattern("Automobile");
             automobileRule.setForm("AutomobileLoan.xdp");
 
             //Add the Rules to a List object
             List<Rule> myList = new ArrayList<Rule>();
             myList.add(mortageRule);
             myList.add(automobileRule);
 
             //Define PDF run-time options which includes Search Rules
             PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
             outputOptions.setFileURI("C:\\Adobe\Loan.pdf");
             outputOptions.setRules(myList);
             outputOptions.setLookAhead(900);
 
             //Define rendering run-time options
             RenderOptionsSpec pdfOptions = new RenderOptionsSpec();
             pdfOptions.setCacheEnabled(new Boolean(true));
 
             //Create a PDF document based on multiple form designs
             OutputResult outputDocument = outClient.generatePDFOutput(
                 TransformationFormat.PDF,
                 "Loan.xdp",
                 "C:\\Adobe",
                 outputOptions,
                 pdfOptions,
                 inXMData
             );
 
             //Write the results of the operation to OutputLog.xml
             Document resultData = outputDocument.getStatusDoc();
             File myFile = new File("C:\\Adobe\OutputLog.xml");
             resultData.copyToFile(myFile);
             }
         catch (Exception ee)
                 {
                     ee.printStackTrace();
                 }
         }
 }
 
```

## Inicio rápido (modo SOAP): Transformación de un documento PDF mediante la API de Java {#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api}

El siguiente ejemplo de código Java transforma un documento PDF interactivo llamado *Loan.pdf* en un documento PDF no interactivo llamado *NonInteractiveLoan.pdf*. (Consulte [Acoplamiento de documentos PDF](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents)).

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import com.adobe.livecycle.output.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class TransformPDF {
 
     public static void main(String[] args) {
 
     try{
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create an OutputClient object
         OutputClient outClient = new OutputClient(myFactory);
 
         //Reference an interactive PDF document to transform
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.pdf");
         Document inPDFDoc = new Document (fileInputStream);
 
         //Transform the PDF document to a non-interactive PDF document
         Document transformedDocument = outClient.transformPDF(
                 inPDFDoc,
                 TransformationFormat.PDF,
                 null,
                 null,
                 null);
 
         //Save the non-interactive PDF document
         File myFile = new File("C:\\Adobe\NonInteractiveLoan.pdf");
         transformedDocument.copyToFile(myFile);
 
     }catch (Exception ee)
         {
             ee.printStackTrace();
         }
     }
 }
 
```

