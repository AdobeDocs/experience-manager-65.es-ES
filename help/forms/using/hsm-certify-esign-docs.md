---
title: Utilice HSM para firmar digitalmente o certificar documentos
seo-title: Utilizar HSM para certificar documentos firmados electrónicamente
description: Utilizar HSM o dispositivos de activación para certificar documentos firmados electrónicamente
seo-description: Utilizar HSM o dispositivos de activación para certificar documentos firmados electrónicamente
uuid: bbe057c1-6150-41f9-9c82-4979d31d305d
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 536bcba4-b754-4799-b0d2-88960cc4c44a
translation-type: tm+mt
source-git-commit: 35b2c9c8c79b3cc3d81e0b92ea17cd7d599fa7ee
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---


# Utilice HSM para firmar digitalmente o certificar documentos {#use-hsm-to-digitally-sign-or-certify-documents}

Los módulos de seguridad de hardware (HSM) y las cookies son dispositivos informáticos dedicados, reforzados y resistentes a las manipulaciones diseñados para administrar, procesar y almacenar claves digitales de forma segura. Estos dispositivos están conectados directamente a un equipo o a un servidor de red.

Adobe Experience Manager Forms puede utilizar las credenciales almacenadas en un HSM o grabadas para firmar electrónicamente o aplicar firmas digitales de servidor a un documento. Para utilizar un HSM o un dispositivo de activación con AEM Forms:

1. Habilite el servicio DocAssurance.
1. Configure los certificados para la extensión de Reader.
1. Cree un alias para el HSM o dispositivo de activación en AEM consola web.
1. Utilice las API de servicio DocAssurance para firmar o certificar los documentos con claves digitales almacenadas en el dispositivo.

## Antes de configurar el HSM o los dispositivos de activación con AEM Forms {#configurehsmetoken}

* Instale el paquete [AEM Forms Add-on](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html).
* Instale y configure el software de cliente HSM o Token en el mismo equipo que AEM servidor. El software cliente es necesario para comunicarse con el HSM y los dispositivos de activación.
* (Solo Microsoft Windows) Configure la variable de entorno JAVA_HOME_32 para que señale al directorio en el que está instalada la versión de 32 bits de Java 8 Development Kit (JDK 8). La ruta predeterminada del directorio es C:\Program Files(x86)\Java\jdk&lt;version>
* (Solo AEM Forms en OSGi) Instale el certificado raíz en el almacén de confianza. Es necesario verificar el PDF firmado

>[!NOTE]
>
>En Microsoft Windows, solo se admiten clientes LunaSA o EToken de 32 bits.

## Habilite el servicio DocAssurance {#configuredocassurance}

De forma predeterminada, el servicio DocAssurance no está habilitado. Realice los siguientes pasos para habilitar el servicio:

1. Detenga la instancia de autor de su entorno de AEM Forms.

1. Abra el archivo [AEM_root]\crx-quickstart\conf\sling.properties para editarlo.

   >[!NOTE]
   >
   >Si ha utilizado el archivo [AEM_root]\crx-quickstart\bin\start.bat para inicio de la instancia de AEM, abra el archivo [AEM_root]\crx-quickstart\sling.properties para editarlo.

1. Añada o reemplace las siguientes propiedades en el archivo sling.properties:

   ```shell
   sling.bootdelegation.sun=sun.*,com.sun.*,sun.misc.*
   sling.bootdelegation.ibm=com.ibm.xml.*,com.ibm.*
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. Guarde y cierre el archivo sling.properties.
1. Reinicie la instancia de AEM.

## Configurar certificados para extensiones de Reader {#set-up-certificates-for-reader-extensions}

Realice los siguientes pasos para configurar los certificados:

1. Inicie sesión en la instancia de AEM Author como administrador.

1. Haga clic **Adobe Experience Manager** en la barra de navegación global. Vaya a **Herramientas** > **Seguridad** > **Usuarios**.
1. Haga clic en el campo **nombre** de la cuenta de usuario. Se abre la página **Editar configuración de usuario**.
1. En la instancia de AEM Author, los certificados residen en un KeyStore. Si no ha creado un KeyStore anteriormente, haga clic en **Crear KeyStore** y defina una nueva contraseña para el KeyStore. Si el servidor ya contiene un KeyStore, omita este paso.

1. En la página **Editar configuración de usuario**, haga clic en **Administrar KeyStore**.

1. En el cuadro de diálogo Administración de KeyStore, expanda la opción **Añadir clave privada del archivo de almacén de claves** y proporcione un alias. El alias se utiliza para realizar la operación Extensiones de Reader.
1. Para cargar el archivo de certificado, haga clic en **Seleccionar archivo de almacén de claves** y cargue un archivo `.pfx`.
1. Añada la **Contraseña del almacén de claves**,**Contraseña de clave privada** y **Alias de clave privada** que está asociado con el certificado en los campos respectivos. Haga clic en **Enviar**.

   >[!NOTE]
   >
   >Para determinar el alias P **de clave privada** de un certificado, puede utilizar el comando de la herramienta clave de Java: `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

   >[!NOTE]
   >
   >En los campos **Contraseña del almacén de claves** y **Contraseña de clave privada**, especifique la contraseña proporcionada con el archivo de certificado.

>[!NOTE]
>
>Para AEM Forms en OSGi, para comprobar el PDF firmado, el certificado raíz instalado en el almacén de confianza.

>[!NOTE]
>
>Al pasar al entorno de producción, reemplace las credenciales de evaluación por las credenciales de producción. Asegúrese de eliminar las credenciales antiguas de las extensiones de Reader antes de actualizar una credencial de evaluación o caducada.

## Crear un alias para el dispositivo {#configuredeviceinaemconsole}

El alias contiene todos los parámetros que requiere un HSM o una cookie. Siga las instrucciones que se indican a continuación para crear un alias para cada credencial de HSM o de activación que utilice eSign o Digital Signatures:

1. Abra AEM consola. La dirección URL predeterminada de AEM consola es https://&lt;host>:&lt;puerto>/system/console/configMgr
1. Abra el **servicio de configuración de credenciales de HSM** y especifique los valores para los siguientes campos:

   * **Alias** de credencial: Especifique una cadena utilizada para identificar el alias. Este valor se utiliza como propiedad para algunas operaciones de firmas digitales, como la operación Firmar campo de firma.
   * **Ruta** de DLL: Especifique la ruta completa de su HSM o biblioteca de cliente activada en el servidor. Por ejemplo, C:\Program Files\LunaSA\cryptoki.dll. En un entorno agrupado, esta ruta debe ser idéntica para todos los servidores del clúster.
   * **Pin** HSM: Especifique la contraseña necesaria para acceder a la clave del dispositivo.
   * **Id** de ranura HSM: Especifique un identificador de ranura de tipo entero. El ID de ranura se establece cliente por cliente. Si registra una segunda máquina en una partición diferente (por ejemplo, HSMPART2 en el mismo dispositivo HSM), entonces la ranura 1 se asocia con la partición HSMPART2 para el cliente.

   >[!NOTE]
   >
   >Durante la configuración de Etoken, especifique un valor numérico para el campo Id. de ranura HSM. Se requiere un valor numérico para que funcionen las operaciones Firmas.

   * **Certificado SHA1**: Especifique el valor SHA1 (huella digital) del archivo de clave pública (.cer) para las credenciales que está utilizando. Asegúrese de que no hay espacios utilizados en el valor SHA1. Si utiliza un certificado físico, no es obligatorio.
   * **Tipo** de dispositivo HSM: Seleccione el fabricante del HSM (Luna u otro) o dispositivo eToken.

   Haga clic en **Guardar.** El módulo de seguridad de hardware está configurado para AEM Forms. Ahora puede utilizar el módulo de seguridad de hardware con AEM Forms para firmar o certificar documentos.

## Utilice las API del servicio DocAssurance para firmar o certificar un documento con claves digitales almacenadas en el dispositivo  {#programatically}

El siguiente código de muestra utiliza un HSM o un token para firmar o certificar un documento.

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

Si ha actualizado desde AEM 6.0 Form o AEM 6.1 Forms y estaba utilizando el servicio DocAssurance en la versión anterior, entonces:

* Para utilizar el servicio DocAssurance sin un HSM o dispositivo de activación, siga utilizando el código existente.
* Para utilizar el servicio DocAssurance con un HSM o dispositivo de activación, sustituya el código de objeto CredentialContext existente por la API que se indica a continuación.

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

Para obtener información detallada sobre las API y el código de muestra del servicio DocAssurance, consulte [Uso de AEM servicios de Documento mediante programación](/help/forms/using/aem-document-services-programmatically.md).
