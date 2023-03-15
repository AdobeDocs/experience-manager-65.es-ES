---
title: Usar HSM para firmar o certificar documentos digitalmente
seo-title: Use HSM to certify eSigned documents
description: Uso de dispositivos HSM o de token electrónico para certificar documentos firmados electrónicamente
seo-description: Use HSM or etoken devices to certify eSigned documents
uuid: bbe057c1-6150-41f9-9c82-4979d31d305d
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 536bcba4-b754-4799-b0d2-88960cc4c44a
exl-id: 4d423881-18e0-430a-849d-e1762366a849
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 100%

---

# Usar HSM para firmar o certificar documentos digitalmente {#use-hsm-to-digitally-sign-or-certify-documents}

Los módulos de seguridad de hardware (HSM) y los tokens electrónicos son dispositivos informáticos dedicados, protegidos y resistentes a la manipulación diseñados para administrar, procesar y almacenar claves digitales de forma segura. Estos dispositivos están conectados directamente a un equipo o a un servidor de red.

Adobe Experience Manager Forms puede utilizar las credenciales almacenadas en un HSM o un token electrónico para firmar electrónicamente o aplicar firmas digitales del lado del servidor a un documento. Para utilizar un dispositivo HSM o de token electrónico con AEM Forms:

1. Habilite el servicio DocAssurance.
1. Configure los certificados para la extensión de Reader.
1. Cree un alias para el dispositivo HSM o de token electrónico en la consola web de AEM.
1. Utilice las API del servicio DocAssurance para firmar o certificar los documentos con las claves digitales almacenadas en el dispositivo.

## Antes de configurar los dispositivos HSM o de token electrónico con AEM Forms {#configurehsmetoken}

* Instale el paquete [de complementos de AEM Forms](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html).
* Instale y configure el software cliente de HSM o de token electrónico en el mismo equipo que el servidor de AEM El software cliente es necesario para comunicarse con los dispositivos HSM y los dispositivos de token electrónico.
* (Solo Microsoft Windows) Establezca la variable de entorno JAVA_HOME_32 para que apunte al directorio en el que está instalada la versión de 32 bits de Java 8 Development Kit (JDK 8). La ruta predeterminada del directorio es C:\Program Files(x86)\Java\jdk&lt;version>.
* (Solo AEM Forms en OSGi) Instale el certificado raíz en el almacén de confianza. Es necesario verificar el PDF firmado

>[!NOTE]
>
>En Microsoft Windows, solo se admiten clientes LunaSA o EToken de 32 bits.

## Habilitar el servicio DocAssurance {#configuredocassurance}

El servicio DocAssurance no está habilitado de forma predeterminada. Siga los siguientes pasos para habilitar el servicio:

1. Detenga la instancia de autor del entorno de AEM Forms.

1. Abra el archivo [AEM_root]\crx-quickstart\conf\sling.properties para editarlo.

   >[!NOTE]
   >
   >Si ha utilizado el archivo [AEM_root]\crx-quickstart\bin\start.bat para iniciar la instancia de AEM, abra el archivo [AEM_root]\crx-quickstart\sling.properties para editarlo.

1. Agregue las siguientes propiedades al archivo sling.properties o reemplácelas:

   ```shell
   sling.bootdelegation.sun=sun.*,com.sun.*,sun.misc.*
   sling.bootdelegation.ibm=com.ibm.xml.*,com.ibm.*
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. Guarde y cierre el archivo sling.properties.
1. Reinicie la instancia de AEM.

## Configuración de certificados para Extensiones de Reader {#set-up-certificates-for-reader-extensions}

Siga los siguientes pasos para configurar los certificados:

1. Inicie sesión en la instancia de autor de AEM como administrador.

1. Haga clic en **Adobe Experience Manager** en la barra de navegación global. Vaya a **Herramientas** >  **Seguridad** >  **Usuarios**.
1. Haga clic en el campo **Nombre** de la cuenta de usuario. Se abrirá la página **Editar configuración de usuario**.
1. En la instancia de autor de AEM, los certificados residen en un almacén de claves. Si no ha creado ningún almacén de claves anteriormente, haga clic en **Crear almacén de claves** y establezca una nueva contraseña para el almacén. Si el servidor ya contiene un almacén de claves, omita este paso.

1. En la página **Editar configuración de usuario**, haga clic en **Administrar almacén de claves**.

1. En el cuadro de diálogo Administración de almacén de claves, expanda la opción **Añadir clave privada del archivo del almacén de claves** y proporcione un alias. El alias se utiliza para realizar la operación de las Extensiones de Reader.
1. Para cargar el archivo del certificado, haga clic en **Seleccionar archivo de almacén de claves** y cargue un archivo `.pfx`.
1. Agregue la **Contraseña del almacén de claves**, la **Contraseña de la clave privada** y el **Alias de la clave privada** asociados con el certificado a los campos respectivos. Haga clic en **Enviar**.

   >[!NOTE]
   >
   >Para determinar el **Alias de la clave privada** de un certificado, puede utilizar el comando keytool de Java: `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

   >[!NOTE]
   >
   >En los campos **Contraseña del almacén de claves** y **Contraseña de la clave privada**, especifique la contraseña proporcionada con el archivo de certificado.

>[!NOTE]
>
>En el caso de AEM Forms en OSGi, para verificar el PDF firmado, utilice el certificado raíz instalado en el almacén de confianza.

>[!NOTE]
>
>Al pasar al entorno de producción, sustituya las credenciales de evaluación por las credenciales de producción. Asegúrese de eliminar las credenciales antiguas de las Extensiones de Reader antes de actualizar una credencial caducada o de evaluaciones.

## Crear un alias para el dispositivo {#configuredeviceinaemconsole}

El alias contiene todos los parámetros que requiere un HSM o un token electrónico. Siga las instrucciones que se indican a continuación para crear un alias para cada credencial HSM o de token electrónico que utilice para realizar firmas electrónicas o firmas digitales:

1. Abra la consola de AEM. La URL predeterminada de la consola de AEM consola es https://&lt;host>:&lt;port>/system/console/configMgr.
1. Abra el **Servicio de configuración de credenciales de HSM** y especifique los valores de los siguientes campos:

   * **Alias de credencial**: especifique una cadena utilizada para identificar el alias. Este valor se utiliza como propiedad en algunas operaciones de firmas digitales, como la operación Firmar campo de firma.
   * **Ruta de DLL**: especifique la ruta de acceso completa de la biblioteca de cliente HSM o de token electrónico en el servidor. Por ejemplo, C:\Program Files\LunaSA\cryptoki.dll. En un entorno en clúster, esta ruta debe ser idéntica para todos los servidores del clúster.
   * **Pin de HSM**: especifique la contraseña necesaria para acceder a la clave del dispositivo.
   * **ID de ranura HSM**: especifique un identificador de ranura de tipo entero. El ID de ranura se establece cliente por cliente. Si registra una segunda máquina en una partición diferente (por ejemplo, HSMPART2 en el mismo dispositivo HSM), entonces la ranura 1 está asociada con la partición HSMPART2 del cliente.

   >[!NOTE]
   >
   >Al configurar el token electrónico, especifique un valor numérico para el campo ID de ranura HSM. Se requiere un valor numérico para que las operaciones de Firmas funcionen.

   * **Certificado SHA1**: especifique el valor SHA1 (huella digital) del archivo de clave pública (.cer) de las credenciales que está utilizando. Asegúrese de que no haya espacios utilizados en el valor SHA1. Si utiliza un certificado físico, no es obligatorio.
   * **Tipo de dispositivo HSM**: seleccione el fabricante del dispositivo HSM (Luna u otro) o del token electrónico.

   Haga clic en **Guardar**. El módulo de seguridad de hardware está configurado para AEM Forms. Ahora puede utilizar el módulo de seguridad de hardware con AEM Forms para firmar o certificar documentos.

## Utilice las API del servicio DocAssurance para firmar o certificar un documento con las claves digitales almacenadas en el dispositivo  {#programatically}

El siguiente código de ejemplo utiliza un HSM o un token electrónico para firmar o certificar un documento.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.ByteArrayInputStream;
import java.io.IOException;
import java.io.InputStream;

import javax.jcr.Binary;
import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 * Digital signatures can be applied to PDF documents to provide a level of security. Digital signatures, like handwritten signatures, provide a means by which signers
 * identify themselves and make statements about a document. The technology used to digitally sign documents helps to ensure that both the signer and recipients are clear
 * about what was signed and confident that the document was not altered since it was signed.
 *
 * PDF documents are signed by means of public-key technology. A signer has two keys: a public key and a private key. The private key is stored in a user's credential that
 * must be available at the time of signing. The public key is stored in the user's certificate that must be available to recipients to validate the signature. Information
 * about revoked certificates is found in certificate revocation lists (CRLs) and Online Certificate Status Protocol (OCSP) responses distributed by Certificate Authorities (CAs).
 * The time of signing can be obtained from a trusted source known as a Timestamping Authority.
 *
 * The following Java code example digitally signs a PDF document that is based on a PDF file.
 * The alias that is specified for the security credential is secure, and revocation checking is performed.
 * Because no CRL or OCSP server information is specified, the server information is obtained from the certificate used to
 * digitally sign the PDF document
 *
 * PreRequisites - Digital certificate for signing the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=Sign.class)
public class Sign{
 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at JCR node
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void signExtend(String inputFile, String outputFile, String alias) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  Document inDoc = new Document(inputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you don't want to use that service
             //as we don't want encryption in this case, passing null for Encryption Options
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, null, getSignatureOptions(alias,resourceResolver),null,null);
        }
  catch(Exception e){
   e.printStackTrace();
  }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        //flush the output document contents to JCR Node
  flush(outDoc, outputFile);

 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getSignatureOptions(String alias, ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.SIGN);

  //field to sign
  String fieldName = "Signature1" ;

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA384;

        //Reason for signing/certifying
        String reason = "Test Reason";

        //location of the signer
        String location = "Test Location";

        //contact info of the signer
        String contactInfo = "Test Contact";

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, true, true, true, TextDirection.AUTO);

        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr, true));
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
    /**
     * This method copies the data from {@code Document}, to the specified file at the given resourcePath.
     * @param doc
     * @param resourcePath
     * @throws IOException
     */
    private void flush(Document doc, String resourcePath) throws IOException {
   //extracts the byte data from Document
   byte[] output = doc.getInlineData();
   Binary opBin;
   Session adminSession = null;
      try {
         adminSession = slingRepository.loginAdministrative(null);

         //get access to the specific node
         //here we are assuming that node exists
           Node node = adminSession.getNode(resourcePath);

           //convert byte[] to Binary
           opBin = adminSession.getValueFactory().createBinary((InputStream)new ByteArrayInputStream(output));

           //set the Binary data value to node's jcr:data
           node.getNode("jcr:content").getProperty("jcr:data").setValue(opBin);
      } catch (RepositoryException e) {

      }
      finally{

       if(adminSession != null && adminSession.isLive()){
        try {
      adminSession.save();
      adminSession.logout();
     } catch (RepositoryException e) {

     }

             }
      }

  }
}
```

Si ha actualizado desde AEM 6.0 Form o AEM 6.1 Forms y estaba utilizando el servicio DocAssurance en la versión anterior:

* Para utilizar el servicio DocAssurance sin un dispositivo HSM o de token electrónico, continúe utilizando el código existente.
* Para utilizar el servicio DocAssurance con un dispositivo HSM o de token electrónico, sustituya el código de objeto CredentialContext existente por la API que se indica a continuación.

```java
/**
  *
  * @param credentialAlias alias of the PKI Credential stored in CQ Key Store or
  * the alias of the HSM Credential configured using HSM Credentials Configuration Service.
  * @param resourceResolver corresponding to the user with the access to the key store and trust store.
  * @param isHSMCredential if the alias is corresponding to HSM Credential.
  */
 public CredentialContext(String credentialAlias, ResourceResolver resourceResolver, boolean isHSMCredential);
```

Para obtener información detallada sobre las API y el código de ejemplo del servicio DocAssurance, consulte [Uso de AEM Document Services mediante programación](/help/forms/using/aem-document-services-programmatically.md).
