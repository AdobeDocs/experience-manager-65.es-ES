---
title: Inicio rápido de la API de Java del servicio de credenciales (SOAP)
seo-title: Inicio rápido de la API de Java del servicio de credenciales (SOAP)
description: Inicio rápido de la API de Java del servicio de credenciales (SOAP)
uuid: a00eabfa-3a52-41dd-bcba-c60d00394384
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: b624e255-ae71-4d9c-8554-d48f3e77b799
role: Desarrollador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# Inicio rápido de API de Java (SOAP) de Credential Service {#credential-service-java-api-quickstart-soap}

El inicio rápido de la API de Java (SOAP) está disponible para el servicio Credential.

[Inicio rápido (modo SOAP): Importación de credenciales mediante la API de Java](credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[Inicio rápido (modo SOAP): Eliminación de credenciales mediante la API de Java](credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

Las operaciones de AEM Forms se pueden realizar mediante la API con establecimiento inflexible de tipos de AEM Forms y el modo de conexión se debe establecer en SOAP.

>[!NOTE]
>
>Inicio rápido ubicado en Programación con formularios AEM se basan en FormsServer que se implementa en JBoss y en el sistema operativo Windows. Sin embargo, si está utilizando otro sistema operativo, como Unix, reemplace las rutas específicas de Windows con rutas compatibles con el sistema operativo aplicable. Del mismo modo, si utiliza otro servidor de aplicaciones J2EE, asegúrese de especificar propiedades de conexión válidas. Consulte [Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

>[!NOTE]
>
>No puede realizar operaciones del servicio Credencial mediante servicios web.

## Inicio rápido (modo SOAP): Importación de credenciales mediante la API de Java {#quick-start-soap-mode-importing-credentials-using-the-java-api}

El siguiente ejemplo de código importa una credencial basada en un archivo llamado *cred.p12*. El valor de alias utilizado para importar las credenciales es `Secure`. (Consulte [Importación de credenciales mediante la API del administrador de confianza](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)).

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-truststore-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
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
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.truststore.client.CredentialServiceClient;
 
 public class ImportCredentialSoap {
 
     public static void main(String[] args) {
            try {
 
          //Set connection properties required to invoke AEM Forms using SOAP mode
              Properties connectionProps = new Properties();
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a CredentialServiceClient instance
             CredentialServiceClient certClient = new CredentialServiceClient(myFactory);
 
             //Reference a credential based on a P12 file
             FileInputStream myCred = new FileInputStream("C:\\Adobe\cred.p12");
             Document credential = new Document(myCred);
 
             //Create a string array to store usage values
             String[] usage = new String[1];
             usage[0] = "truststore.usage.type.sign";
 
             //Import the credential
             certClient.importCredential("secure",credential,"password",usage);
             System.out.println("Credential was uploaded");
 
            }catch (Exception e) {
                e.printStackTrace();
            }
 
            }
 }
 
 
 
```

## Inicio rápido (modo SOAP): Eliminación de credenciales mediante la API de Java {#quick-start-soap-mode-deleting-credentials-using-the-java-api}

En el siguiente ejemplo de código se elimina una credencial basada en un valor de alias *secure*. (Consulte [Eliminación de credenciales utilizando la API del administrador de confianza](/help/forms/developing/credentials.md#deleting-credentials-by-using-the-trust-manager-api)).

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-truststore-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
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
 
 import java.util.Properties;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.truststore.client.CredentialServiceClient;
 
 public class DeleteCertificateSoap {
 
 
     public static void main(String[] args)
     {
     try {
 
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a CredentialServiceClient instance
         CredentialServiceClient certClient = new CredentialServiceClient(myFactory);
 
         //Delete the certificate
         certClient.deleteCredential("secure");
         System.out.println("Credential was deleted");
 
        }catch (Exception e) {
            e.printStackTrace();
        }
 
        }
 
 }
 
```

