---
title: Conexión de AEM Forms con el LiveCycle de Adobe
seo-title: Conexión de AEM Forms con el LiveCycle de Adobe
description: AEM conector de LiveCycle le permite inicio de los servicios de Documento de LiveCycle ES4 desde AEM aplicaciones y flujos de trabajo.
seo-description: AEM conector de LiveCycle le permite inicio de los servicios de Documento de LiveCycle ES4 desde AEM aplicaciones y flujos de trabajo.
uuid: 7dc9d5ec-7b19-4d93-936d-81ceb45dfffa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 7e404b45-1302-4dd1-b3c9-3f47fedb5f94
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 0%

---


# Conexión de AEM Forms con el LiveCycle de Adobe {#connecting-aem-forms-with-adobe-livecycle}

El conector de LiveCycle de Adobe Experience Manager (AEM) permite la invocación sin fisuras de los servicios de Documento de Adobe LiveCycle ES4 desde AEM aplicaciones web y flujos de trabajo. LiveCycle proporciona un SDK de cliente enriquecido que permite a las aplicaciones cliente inicio servicios de LiveCycle mediante API de Java. AEM conector de LiveCycle simplifica el uso de estas API dentro del entorno OSGi.

## Conexión de AEM servidor al LiveCycle de Adobe {#connecting-aem-server-to-adobe-livecycle}

AEM conector de LiveCycle forma parte del [paquete de complemento de AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md). Después de instalar el paquete del complemento AEM Forms, realice los siguientes pasos para agregar detalles del servidor de LiveCycle a AEM consola web.

1. En AEM administrador de configuración de consola web, busque el componente de configuración del SDK de cliente de Adobe LiveCycle.
1. Haga clic en el componente para editar la dirección URL, el nombre de usuario y la contraseña del servidor de configuración.
1. Revise la configuración y haga clic en **Guardar**.

Aunque las propiedades son autoexplicativas, las importantes son las siguientes:

* **URL**  del servidor: especifica la URL del servidor de LiveCycle. Si desea que LiveCycle y AEM se comuniquen a través de https, AEM inicio con la siguiente JVM

   ```java
   argument
    -Djavax.net.ssl.trustStore=<<em>path to LC keystore</em>>
   ```

   , seleccione una opción.

* **Nombre de usuario**: especifica el nombre de usuario de la cuenta que se utiliza para establecer la comunicación entre AEM y LiveCycle. La cuenta es una cuenta de usuario de LiveCycle que tiene permisos para inicio Documento Services.
* **Contraseña**: especifica la contraseña.
* **Nombre**  del servicio: especifica los servicios que se inician con las credenciales de usuario proporcionadas en los campos Nombre de usuario y Contraseña. De forma predeterminada, no se pasan credenciales al iniciar LiveCycle services.

## Iniciando servicios de documento {#starting-document-services}

Las aplicaciones cliente pueden inicio mediante programación servicios de LiveCycle mediante una API de Java, servicios Web, Remoting y REST. Para los clientes de Java, la aplicación puede utilizar el SDK de LiveCycle. El SDK de LiveCycle proporciona una API de Java para iniciar estos servicios de forma remota. Por ejemplo, para convertir un Documento de Microsoft Word a PDF, el cliente inicio GeneratePDFService. El flujo de invocación consta de los siguientes pasos:

1. Cree una instancia de ServiceClientFactory.
1. Cada servicio proporciona una clase de cliente. Para inicio de un servicio, cree una instancia de cliente del servicio.
1. Inicio el servicio y procese el resultado.

AEM conector de LiveCycle simplifica el flujo al exponer estas instancias de cliente como servicios de OSGi a los que se puede acceder con medios OSGi estándar. El conector del LiveCycle ofrece las siguientes características:

* Instancias de cliente como servicio OSGi: Los clientes empaquetados como paquetes OSGI se enumeran en la sección [lista de Documento Services](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p). Cada jar cliente registra la instancia de cliente como servicio OSGi con el Registro de servicio OSGi.
* Propagación de credenciales de usuario: Los detalles de conexión necesarios para conectarse al servidor de LiveCycle se administran en un lugar central.
* Servicio ServiceClientFactory: Para inicio de los procesos, la aplicación cliente puede acceder a la instancia de ServiceClientFactory.

### Comenzar a través de Referencias de Servicio desde el Registro de Servicios de OSGi {#starting-via-service-references-from-osgi-service-registry}

Para inicio de un servicio expuesto desde dentro de AEM, lleve a cabo los siguientes pasos:

1. Determinar las dependencias múltiples. Añada la dependencia al archivo jar cliente requerido en el archivo pom.xml. Como mínimo, agregue dependencia a las taras adobe-livecycle-client y adobe-usermanager-client.

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-livecycle-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-usermanager-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-cq-integration-api</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

   Para inicio de un servicio, agregue la dependencia Maven correspondiente para el servicio. Para ver la lista de las dependencias, consulte [Lista del servicio de Documento](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p). Por ejemplo, para el servicio Generar PDF, agregue la dependencia siguiente:

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-generatepdf-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

1. Obtenga la referencia del servicio. Obtenga un identificador para la instancia de servicio. Si está escribiendo una clase de Java, puede utilizar las anotaciones de los servicios declarativos.

   ```java
   import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
   import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
   import com.adobe.idp.Document;
   
   @Reference
   GeneratePdfServiceClient generatePDF;
   ...
   
   Resource r = resourceResolver.getResource("/path/tp/docx");
   Document sourceDoc = new Document(r.adaptTo(InputStream.class));
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

   El fragmento de código anterior inicio la API createPDF de GeneratePdfServiceClient para convertir un documento a PDF. Puede realizar una invocación similar en un JSP utilizando el siguiente código. La diferencia principal es que el código siguiente utiliza Sling ScriptHelper para acceder a GeneratePdfServiceClient.

   ```jsp
   <%@ page import="com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient" %>
   <%@ page import="com.adobe.livecycle.generatepdf.client.CreatePDFResult" %>
   <%@ page import="com.adobe.idp.Document" %>
   
   GeneratePdfServiceClient generatePDF = sling.getService(GeneratePdfServiceClient.class);
   Document sourceDoc = ...
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

### Comenzar a través de ServiceClientFactory {#starting-via-serviceclientfactory}

En algunos casos se requiere la clase ServiceClientFactory. Por ejemplo, se requiere que ServiceClientFactory llame a los procesos.

```java
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;

@Reference
ServiceClientFactoryProvider scfProvider;

...
ServiceClientFactory scf = scfProvider.getDefaultServiceClientFactory();
...
```

## Soporte de RunAs {#runas-support}

Casi todos los servicios de Documento en LiveCycle requieren autenticación. Puede utilizar cualquiera de las siguientes opciones para el inicio de estos servicios sin proporcionar credenciales explícitas en el código:

### Configuración de lista de permitidos {#allowlist-configuration}

La configuración del SDK del cliente de LiveCycle contiene una configuración sobre los nombres de servicio. Esta configuración es una lista de servicios para los que la lógica de invocación utiliza credenciales de administrador de forma predeterminada. Por ejemplo, si agrega servicios de DirectoryManager (parte de la API de administración de usuarios) a esta lista, cualquier código de cliente puede utilizar directamente el servicio y la capa de invocación pasa automáticamente las credenciales configuradas como parte de la solicitud enviada al servidor de LiveCycle

### RunAsManager {#runasmanager}

Como parte de la integración, se proporciona un nuevo servicio RunAsManager. Le permite controlar mediante programación las credenciales que se utilizarán al realizar llamadas al servidor de LiveCycle.

```java
import com.adobe.livecycle.dsc.clientsdk.security.PasswordCredential;
import com.adobe.livecycle.dsc.clientsdk.security.PrivilegedAction;
import com.adobe.livecycle.dsc.clientsdk.security.RunAsManager;
import com.adobe.idp.dsc.registry.component.ComponentRegistry;

@Reference
private RunAsManager runAsManager;

List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
            public List<Component> run() {
                return componentRegistry.getComponents();
            }
        });
assertNotNull(components);
```

Si desea pasar credenciales diferentes, puede utilizar el método sobrecargado que toma una instancia PasswordCredential.

```java
PasswordCredential credential = new PasswordCredential("administrator","password");
List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
    public List<Component> run() {
        return componentRegistry.getComponents();
    }
},credential);
```

### Propiedad InvocationRequest {#invocationrequest-property}

Si llama a un proceso o utiliza directamente la clase ServiceClientFactory y crea una InvocationRequest, puede especificar una propiedad para indicar que la capa de invocación debe utilizar las credenciales configuradas.

```java
import com.adobe.idp.dsc.InvocationResponse
import com.adobe.idp.dsc.InvocationRequest
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory
import com.adobe.livecycle.dsc.clientsdk.InvocationProperties

ServiceClientFactoryProvider scfp = sling.getService(ServiceClientFactoryProvider.class)
ServiceClientFactory serviceClientFactory = scfp.getDefaultServiceClientFactory()
InvocationRequest ir = serviceClientFactory.createInvocationRequest("sample/LetterSubmissionProcess", "invoke", new HashMap(), true);

//Here we are invoking the request with system user
ir.setProperty(InvocationProperties.INVOKER_TYPE,InvocationProperties.INVOKER_TYPE_SYSTEM)

InvocationResponse response = serviceClientFactory.getServiceClient().invoke(ir);
```

## Lista de servicios de documento {#document-services-list}

### Paquete de API de SDK de cliente de Adobe LiveCycle {#adobe-livecycle-client-sdk-api-bundle}

Están disponibles los siguientes servicios:

* com.adobe.idp.um.api.AuthenticationManager
* com.adobe.idp.um.api.DirectoryManager
* com.adobe.idp.um.api.AuthorizationManager
* com.adobe.idp.dsc.registry.service.ServiceRegistry
* com.adobe.idp.dsc.registry.component.ComponentRegistry

#### Dependencias de maven {#maven-dependencies}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-client</artifactId>
  <version>11.0.0</version>
</dependency>
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-usermanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete de SDK de cliente de Adobe LiveCycle {#adobe-livecycle-client-sdk-bundle}

Están disponibles los siguientes servicios:

* com.adobe.livecycle.dsc.clientsdk.security.RunAsManager
* com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider

#### Dependencias de maven {#maven-dependencies-1}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-cq-integration-api</artifactId>
  <version>1.1.10</version>
</dependency>
```

### Paquete de cliente de Adobe LiveCycle TaskManager {#adobe-livecycle-taskmanager-client-bundle}

Están disponibles los siguientes servicios:

* com.adobe.idp.taskmanager.dsc.client.task.TaskManager
* com.adobe.idp.taskmanager.dsc.client.TaskManagerQueryService
* com.adobe.idp.taskmanager.dsc.client.queuemanager.QueueManager
* com.adobe.idp.taskmanager.dsc.client.emailsettings.EmailSettingService
* com.adobe.idp.taskmanager.dsc.client.endpoint.TaskManagerEndpointClient
* com.adobe.idp.taskmanager.dsc.client.userlist.UserlistService

#### Dependencias de maven {#maven-dependencies-2}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-taskmanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete de cliente de LiveCycle Workflow de Adobe {#adobe-livecycle-workflow-client-bundle}

El siguiente servicio está disponible:

* com.adobe.idp.workflow.client.WorkflowServiceClient

#### Dependencias de maven {#maven-dependencies-3}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-workflow-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete de cliente de Adobe LiveCycle PDF Generator {#adobe-livecycle-pdf-generator-client-bundle}

El siguiente servicio está disponible:

* com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient

#### Dependencias de maven {#maven-dependencies-4}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-generatepdf-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete de cliente de Adobe LiveCycle Application Manager {#adobe-livecycle-application-manager-client-bundle}

Están disponibles los siguientes servicios:

* com.adobe.idp.applicationmanager.service.ApplicationManager
* com.adobe.livecycle.applicationmanager.client.ApplicationManager
* com.adobe.livecycle.design.service.DesigntimeService

#### Dependencias de maven {#maven-dependencies-5}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-applicationmanager-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete de cliente de ensamblador de LiveCycles de Adobe {#adobe-livecycle-assembler-client-bundle}

El siguiente servicio está disponible:

* com.adobe.livecycle.assembler.client.AssemblerServiceClient

#### Dependencias de maven {#maven-dependencies-6}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-assembler-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete del cliente de integración de datos de formulario de LiveCycle de Adobe {#adobe-livecycle-form-data-integration-client-bundle}

El siguiente servicio está disponible:

* com.adobe.livecycle.formdataintegration.client.FormDataIntegrationClient

#### Dependencias de maven {#maven-dependencies-7}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-formdataintegration-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete de cliente de Adobe LiveCycle Forms {#adobe-livecycle-forms-client-bundle}

El siguiente servicio está disponible:

* com.adobe.livecycle.formsservice.client.FormsServiceClient

#### Dependencias de maven {#maven-dependencies-8}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-forms-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete de cliente de Adobe LiveCycle Output {#adobe-livecycle-output-client-bundle}

El siguiente servicio está disponible:

* com.adobe.livecycle.output.client.OutputClient

#### Dependencias de maven {#maven-dependencies-9}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-output-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete de cliente de Adobe LiveCycle Reader Extensions {#adobe-livecycle-reader-extensions-client-bundle}

El siguiente servicio está disponible:

* com.adobe.livecycle.readerextensions.client.ReaderExtensionsServiceClient

#### Dependencias de maven {#maven-dependencies-10}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-reader-extensions-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete de cliente de Adobe LiveCycle Rights Manager {#adobe-livecycle-rights-manager-client-bundle}

Están disponibles los siguientes servicios:

* com.adobe.livecycle.rightsmanagement.client.DocumentManager
* com.adobe.livecycle.rightsmanagement.client.EventManager
* com.adobe.livecycle.rightsmanagement.client.ExternalUserManager
* com.adobe.livecycle.rightsmanagement.client.LicenseManager
* com.adobe.livecycle.rightsmanagement.client.WatermarkManager
* com.adobe.livecycle.rightsmanagement.client.PolicyManager
* com.adobe.livecycle.rightsmanagement.client.AbstractPolicyManager

#### Dependencias de maven {#maven-dependencies-11}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-rightsmanagement-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete del cliente de firmas de LiveCycle de Adobe {#adobe-livecycle-signatures-client-bundle}

El siguiente servicio está disponible:

* com.adobe.livecycle.signatures.client.SignatureServiceClientInterface

#### Dependencias de maven {#maven-dependencies-12}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-signatures-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete cliente de Adobe LiveCycle Truststore {#adobe-livecycle-truststore-client-bundle}

Están disponibles los siguientes servicios:

* com.adobe.truststore.dsc.TrustConfigurationService
* com.adobe.truststore.dsc.CRLService
* com.adobe.truststore.dsc.CredentialService
* com.adobe.truststore.dsc.CertificateService

#### Dependencias de maven {#maven-dependencies-13}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-truststore-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete de cliente de repositorio de LiveCycle de Adobe {#adobe-livecycle-repository-client-bundle}

Están disponibles los siguientes servicios:

* com.adobe.repository.bindings.ResourceRepository
* com.adobe.repository.bindings.ResourceSynchronizer

#### Dependencias de maven {#maven-dependencies-14}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-repository-client</artifactId>
  <version>11.0.0</version>
</dependency>
```
