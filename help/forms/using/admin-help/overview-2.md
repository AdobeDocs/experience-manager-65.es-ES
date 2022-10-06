---
title: Aspectos básicos de la administración de certificados y credenciales
seo-title: Basics of managing certificates and credentials
description: Obtenga información sobre los conceptos básicos de la administración de certificados y credenciales.
seo-description: Learn about the basics of managing certificates and credentials.
uuid: f421e206-e7b5-416c-b9fb-974094f10a66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 986d16fc-4c81-4785-b1f3-fe8bd7ff669e
exl-id: 74bf0e77-f47b-475a-b2a7-52cfb3baaa22
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Aspectos básicos de la administración de certificados y credenciales {#basics-of-managing-certificates-and-credentials}

A *credencial* contiene la información de clave privada necesaria para firmar o identificar documentos. A *certificate* es información de clave pública que se configura para la confianza. AEM formularios utiliza certificados y credenciales para varios fines:

* Las extensiones de Acrobat Reader DC utilizan una credencial para habilitar los derechos de uso de Adobe Reader en documentos de PDF. (Consulte [Configuración de credenciales para usarlas con extensiones de Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).)
* Puede configurar el Rights Management para que muestre las credenciales para usarlas en Acrobat únicamente desde emisores de confianza. (Consulte [Configuración de la visualización del Rights Management](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings).) El nombre común (NC) debe estar presente en el certificado.
* El servicio de firma accede a certificados y credenciales. Para obtener más información sobre el servicio Signature, consulte [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_65).

**Generación de una clave de par**

AEM forms utiliza su almacén de confianza para almacenar y administrar certificados, credenciales y listas de revocación de certificados (CRL). Además, puede utilizar un dispositivo independiente Hardware Security Module (HSM) para almacenar claves privadas.

AEM formularios no proporciona ninguna opción para generar un par de claves. Sin embargo, puede generarla con herramientas, como la herramienta de claves Java, e importarla en AEM almacén de confianza de formularios. Para obtener más información sobre la herramienta de claves Java, consulte lo siguiente:

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL](https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL)

Los siguientes tipos de firma son compatibles y se pueden importar en AEM formularios:

* Firma XML
* XMLTimeStampToken
* RFC 3161 TimeStampToken
* PKCS#7
* PKCS#1
* Firmas DSA

**Gestión de claves perdidas o comprometidas**

Si cree que su clave se ha perdido o se ha visto comprometida, realice las siguientes acciones:

1. Informe a la autoridad de certificación de que debe añadir la clave comprometida en la lista de revocación de certificados para revocar la clave.
1. Obtenga una nueva clave y sus certificados de la autoridad de certificación.
1. Vuelva a firmar los documentos que se firmaron con la clave comprometida mediante la nueva clave.
