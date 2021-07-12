---
title: Conexión de AEM Forms con el LiveCycle de Adobe
seo-title: Conexión de AEM Forms con el LiveCycle de Adobe
description: AEM conector de LiveCycle le permite iniciar LiveCycle ES4 Document Services desde AEM aplicaciones y flujos de trabajo.
seo-description: AEM conector de LiveCycle le permite iniciar LiveCycle ES4 Document Services desde AEM aplicaciones y flujos de trabajo.
uuid: 7dc9d5ec-7b19-4d93-936d-81ceb45dfffa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 7e404b45-1302-4dd1-b3c9-3f47fedb5f94
role: Admin
exl-id: 562f8a22-cbab-4915-bc0d-da9bea7d18fa
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 0%

---

# Conexión de AEM Forms con el LiveCycle de Adobe {#connecting-aem-forms-with-adobe-livecycle}

El conector de LiveCycle de Adobe Experience Manager (AEM) permite la invocación perfecta de los servicios de documentos de LiveCycle de Adobe ES4 desde AEM aplicaciones web y flujos de trabajo. LiveCycle proporciona un SDK de cliente enriquecido, que permite a las aplicaciones cliente iniciar servicios de LiveCycle mediante API de Java. AEM conector de LiveCycle simplifica el uso de estas API dentro del entorno OSGi.

## Conexión de AEM servidor al LiveCycle de Adobe {#connecting-aem-server-to-adobe-livecycle}

AEM conector de LiveCycle forma parte del [paquete de complementos de AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md). Después de instalar el paquete de complementos de AEM Forms, realice los siguientes pasos para agregar detalles del servidor de LiveCycle a AEM consola web.

1. En AEM administrador de configuración de la consola web, busque el componente de configuración del SDK del cliente de Adobe LiveCycle.
1. Haga clic en el componente para editar la URL, el nombre de usuario y la contraseña del servidor de configuración.
1. Revise la configuración y haga clic en **Guardar**.

Aunque las propiedades se explican por sí solas, las importantes son las siguientes:

* **URL del servidor** : especifica la URL del servidor de LiveCycle. Si desea que el LiveCycle y el AEM se comuniquen a través de https, comience AEM con la siguiente JVM

   ```java
   argument
    -Djavax.net.ssl.trustStore=<<em>path to LC keystore</em>>
   ```

   .

* **Nombre de usuario**: especifica el nombre de usuario de la cuenta que se utiliza para establecer la comunicación entre AEM y LiveCycle. La cuenta es una cuenta de usuario de LiveCycle que tiene los permisos para iniciar Document Services.
* **Contraseña**: especifica la contraseña.
* **Nombre de servicio** : especifica los servicios que se inician utilizando las credenciales de usuario proporcionadas en los campos Nombre de usuario y Contraseña. De forma predeterminada, no se transfieren credenciales al iniciar los servicios de LiveCycle.

## Inicio de document services {#starting-document-services}

Las aplicaciones cliente pueden iniciar servicios de LiveCycle mediante programación utilizando una API de Java, Servicios Web, Remoting y REST. Para clientes Java, la aplicación puede utilizar el SDK de LiveCycle. El SDK de LiveCycle proporciona una API de Java para iniciar estos servicios de forma remota. Por ejemplo, para convertir un documento de Microsoft Word a PDF, el cliente inicia GeneratePDFService. El flujo de invocación consta de los siguientes pasos:

1. Cree una instancia de ServiceClientFactory .
1. Cada servicio proporciona una clase cliente. Para iniciar un servicio, cree una instancia de cliente del servicio.
1. Inicie el servicio y procese el resultado.

AEM conector de LiveCycle simplifica el flujo al exponer estas instancias de cliente como servicios OSGi a los que se puede acceder mediante OSGi estándar. El conector del LiveCycle ofrece las siguientes funciones:

* Instancias de cliente como OSGi Service: Los clientes empaquetados como paquetes OSGI se enumeran en la sección [Lista de servicios de documentos](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p). Cada jar cliente registra la instancia del cliente como servicio OSGi con el Registro de servicios OSGi.
* Propagación de la Credencial de Usuario: Los detalles de conexión necesarios para conectarse al servidor de LiveCycle se administran en un lugar central.
* Servicio ServiceClientFactory: Para iniciar los procesos, la aplicación cliente puede acceder a la instancia de ServiceClientFactory .

### Inicio mediante Referencias de Servicio desde el Registro de Servicios de OSGi {#starting-via-service-references-from-osgi-service-registry}

Para iniciar un servicio expuesto desde AEM, realice los siguientes pasos:

1. Determine las dependencias maven. Agregue dependencia al jar cliente requerido en su archivo maven pom.xml. Como mínimo, agregue dependencia a las jars adobe-livecycle-client y adobe-usermanager-client.

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

   Para iniciar un servicio, agregue la dependencia Maven correspondiente al servicio. Para ver la lista de dependencias, consulte [Document Service List](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p). Por ejemplo, para el servicio Generate PDF agregue la siguiente dependencia:

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-generatepdf-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

1. Obtenga la referencia del servicio. Obtenga un identificador para la instancia de servicio. Si está escribiendo una clase Java, puede utilizar las anotaciones de los servicios declarativos.

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

   El fragmento de código anterior inicia la API createPDF de GeneratePdfServiceClient para convertir un documento a PDF. Puede realizar una invocación similar en un JSP utilizando el siguiente código. La diferencia principal es que el siguiente código utiliza Sling ScriptHelper para acceder a GeneratePdfServiceClient.

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

### Inicio mediante ServiceClientFactory {#starting-via-serviceclientfactory}

La clase ServiceClientFactory es necesaria en algunos casos. Por ejemplo, se requiere ServiceClientFactory para llamar a procesos.

```java
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;

@Reference
ServiceClientFactoryProvider scfProvider;

...
ServiceClientFactory scf = scfProvider.getDefaultServiceClientFactory();
...
```

## Compatibilidad con RunAs {#runas-support}

Casi todos los servicios de documentos de LiveCycle requieren autenticación. Puede utilizar cualquiera de las siguientes opciones para iniciar estos servicios sin proporcionar credenciales explícitas en el código:

### configuración de lista de permitidos {#allowlist-configuration}

La configuración del SDK del cliente de LiveCycle contiene una configuración sobre los nombres de servicio. Esta configuración es una lista de servicios para los que la lógica de invocación utiliza credenciales de administrador listas para usar. Por ejemplo, si agrega los servicios de DirectoryManager (parte de la API de administración de usuarios) a esta lista, cualquier código de cliente puede utilizar directamente el servicio y la capa de invocación pasa automáticamente las credenciales configuradas como parte de la solicitud enviada al servidor de LiveCycle

### RunAsManager {#runasmanager}

Como parte de la integración, se proporciona un nuevo servicio RunAsManager. Permite controlar mediante programación las credenciales que se utilizarán al realizar llamadas al servidor de LiveCycle.

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

Si desea pasar credenciales diferentes, puede utilizar el método de sobrecarga que toma una instancia de PasswordCredential.

```java
PasswordCredential credential = new PasswordCredential("administrator","password");
List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
    public List<Component> run() {
        return componentRegistry.getComponents();
    }
},credential);
```

### InvocationRequest, propiedad {#invocationrequest-property}

Si llama a un proceso o utiliza directamente la clase ServiceClientFactory y crea una InvocationRequest, puede especificar una propiedad para indicar que la capa de invocación debe utilizar credenciales configuradas.

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

## Lista de servicios de documentos {#document-services-list}

### Paquete de API del SDK del cliente de LiveCycle de Adobe {#adobe-livecycle-client-sdk-api-bundle}

Los siguientes servicios están disponibles:

* com.adobe.idp.um.api.AuthenticationManager
* com.adobe.idp.um.api.DirectoryManager
* com.adobe.idp.um.api.AuthorizationManager
* com.adobe.idp.dsc.registry.service.ServiceRegistry
* com.adobe.idp.dsc.registry.component.ComponentRegistry

#### Dependencias de Maven {#maven-dependencies}

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

### Paquete de SDK de cliente de LiveCycle de Adobe {#adobe-livecycle-client-sdk-bundle}

Los siguientes servicios están disponibles:

* com.adobe.livecycle.dsc.clientsdk.security.RunAsManager
* com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider

#### Dependencias de Maven {#maven-dependencies-1}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-cq-integration-api</artifactId>
  <version>1.1.10</version>
</dependency>
```

### LiveCycle de Adobe Paquete de cliente de TaskManager {#adobe-livecycle-taskmanager-client-bundle}

Los siguientes servicios están disponibles:

* com.adobe.idp.taskmanager.dsc.client.task.TaskManager
* com.adobe.idp.taskmanager.dsc.client.TaskManagerQueryService
* com.adobe.idp.taskmanager.dsc.client.queuemanager.QueueManager
* com.adobe.idp.taskmanager.dsc.client.emailsettings.EmailSettingService
* com.adobe.idp.taskmanager.dsc.client.endpoint.TaskManagerEndpointClient
* com.adobe.idp.taskmanager.dsc.client.userlist.UserlistService

#### Dependencias de Maven {#maven-dependencies-2}

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

#### Dependencias de Maven {#maven-dependencies-3}

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

#### Dependencias de Maven {#maven-dependencies-4}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-generatepdf-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### LiveCycle de Adobe Application Manager Paquete de cliente {#adobe-livecycle-application-manager-client-bundle}

Los siguientes servicios están disponibles:

* com.adobe.idp.applicationmanager.service.ApplicationManager
* com.adobe.livecycle.applicationmanager.client.ApplicationManager
* com.adobe.livecycle.design.service.DesigntimeService

#### Dependencias de Maven {#maven-dependencies-5}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-applicationmanager-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete de cliente del ensamblador de LiveCycle de Adobe {#adobe-livecycle-assembler-client-bundle}

El siguiente servicio está disponible:

* com.adobe.livecycle.assembler.client.AssemblerServiceClient

#### Dependencias de Maven {#maven-dependencies-6}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-assembler-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete de cliente de integración de datos de formulario de LiveCycle de Adobe {#adobe-livecycle-form-data-integration-client-bundle}

El siguiente servicio está disponible:

* com.adobe.livecycle.formdataintegration.client.FormDataIntegrationClient

#### Dependencias de Maven {#maven-dependencies-7}

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

#### Dependencias de Maven {#maven-dependencies-8}

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

#### Dependencias de Maven {#maven-dependencies-9}

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

#### Dependencias de Maven {#maven-dependencies-10}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-reader-extensions-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete de cliente de Adobe LiveCycle Rights Manager {#adobe-livecycle-rights-manager-client-bundle}

Los siguientes servicios están disponibles:

* com.adobe.livecycle.rightsmanagement.client.DocumentManager
* com.adobe.livecycle.rightsmanagement.client.EventManager
* com.adobe.livecycle.rightsmanagement.client.ExternalUserManager
* com.adobe.livecycle.rightsmanagement.client.LicenseManager
* com.adobe.livecycle.rightsmanagement.client.WatermarkManager
* com.adobe.livecycle.rightsmanagement.client.PolicyManager
* com.adobe.livecycle.rightsmanagement.client.AbstractPolicyManager

#### Dependencias de Maven {#maven-dependencies-11}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-rightsmanagement-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete de cliente de firmas de LiveCycle de Adobe {#adobe-livecycle-signatures-client-bundle}

El siguiente servicio está disponible:

* com.adobe.livecycle.signatures.client.SignatureServiceClientInterface

#### Dependencias de Maven {#maven-dependencies-12}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-signatures-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete de cliente Truststore de LiveCycle de Adobe {#adobe-livecycle-truststore-client-bundle}

Los siguientes servicios están disponibles:

* com.adobe.truststore.dsc.TrustConfigurationService
* com.adobe.truststore.dsc.CRLService
* com.adobe.truststore.dsc.CredentialService
* com.adobe.truststore.dsc.CertificateService

#### Dependencias de Maven {#maven-dependencies-13}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-truststore-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Paquete de cliente del repositorio de LiveCycle de Adobe {#adobe-livecycle-repository-client-bundle}

Los siguientes servicios están disponibles:

* com.adobe.repository.bindings.ResourceRepository
* com.adobe.repository.bindings.ResourceSynchronizer

#### Dependencias de Maven {#maven-dependencies-14}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-repository-client</artifactId>
  <version>11.0.0</version>
</dependency>
```
