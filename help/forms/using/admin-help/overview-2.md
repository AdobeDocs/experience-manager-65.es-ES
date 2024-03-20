---
title: Aspectos básicos de la administración de certificados y credenciales
description: Obtenga información acerca de los conceptos básicos de la administración de certificados y credenciales.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 74bf0e77-f47b-475a-b2a7-52cfb3baaa22
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 3%

---

# Aspectos básicos de la administración de certificados y credenciales {#basics-of-managing-certificates-and-credentials}

A *credencial* contiene la información de clave privada necesaria para firmar o identificar documentos. A *certificado* es información de clave pública que se configura para confianza. AEM Los formularios de datos utilizan certificados y credenciales para varios fines:

* Las extensiones de Acrobat Reader DC utilizan una credencial para habilitar los derechos de uso de Adobe Reader en documentos de PDF. (Consulte [Configuración de credenciales para usarlas con extensiones de Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).)
* Puede configurar Rights Management para que muestre las credenciales de uso en Acrobat únicamente de emisores de confianza. (Consulte [Configuración de visualización del Rights Management](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings).) El nombre común (CN) debe estar presente en el certificado.
* El servicio Signature accede a los certificados y credenciales. Para obtener más información sobre el servicio Signature, consulte [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_65).

**Generación de una clave de par**

AEM Forms utiliza su almacén de confianza para almacenar y administrar certificados, credenciales y listas de revocación de certificados (CRL). Además, puede utilizar un dispositivo HSM (Hardware Security Module) independiente para almacenar claves privadas.

AEM Los formularios no proporcionan ninguna opción para generar un par de claves. AEM Sin embargo, puede generarla con herramientas como Java keytool e importarla en el almacén de confianza de formularios de la red de herramientas de la red de formularios de la organización de formularios de la. Para obtener más información sobre la herramienta clave de Java, consulte lo siguiente:

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL](https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL)

AEM Se admiten los siguientes tipos de firma, que se pueden importar en formularios:

* Firma XML
* XMLTimeStampToken
* RFC 3161: TimeStampToken
* PKCS#7
* PKCS#1
* Firmas DSA

**Gestión de claves perdidas o comprometidas**

Si sospecha que la clave se ha perdido o se ha visto comprometida, realice las siguientes acciones:

1. Informe a la autoridad de certificación para que agregue la clave comprometida a la lista de revocación de certificados para revocarla.
1. Obtenga una clave nueva y sus certificados de la autoridad de certificación.
1. Vuelva a firmar los documentos firmados con la clave comprometida con la nueva clave.
