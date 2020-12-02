---
title: Aspectos básicos de la administración de certificados y credenciales
seo-title: Aspectos básicos de la administración de certificados y credenciales
description: Obtenga información sobre los aspectos básicos de la administración de certificados y credenciales.
seo-description: Obtenga información sobre los aspectos básicos de la administración de certificados y credenciales.
uuid: f421e206-e7b5-416c-b9fb-974094f10a66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 986d16fc-4c81-4785-b1f3-fe8bd7ff669e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---


# Aspectos básicos de la administración de certificados y credenciales {#basics-of-managing-certificates-and-credentials}

Una *credencial* contiene la información de clave privada necesaria para firmar o identificar documentos. Un *certificado* es información de clave pública que se configura para la confianza. AEM formularios utiliza certificados y credenciales para varios fines:

* Las extensiones de Acrobat Reader DC utilizan una credencial para habilitar los derechos de uso de Adobe Reader en documentos PDF. (Consulte [Configuración de credenciales para su uso con extensiones de Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)).
* Puede configurar Rights Management para que muestre las credenciales para usarlas solo en Acrobat desde emisores de confianza. (Consulte [Configuración de la visualización del Rights Management](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings).) El nombre común (NC) debe estar presente en el certificado.
* El servicio Signature accede a los certificados y las credenciales. Para obtener más información sobre el servicio Signature, consulte [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_63).

**Generación de una clave de par**

AEM formularios utiliza su almacén de confianza para almacenar y administrar certificados, credenciales y listas de revocación de certificados (CRL). Además, puede utilizar un dispositivo independiente Hardware Security Module (HSM) para almacenar claves privadas.

AEM formularios no proporciona ninguna opción para generar un par de claves. Sin embargo, puede generarla con herramientas, como la herramienta clave de Java, e importarla en AEM formulario Almacén de confianza. Para obtener más información sobre la herramienta de claves Java, consulte lo siguiente:

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html](https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html)

Los siguientes tipos de firma son compatibles y se pueden importar en AEM formularios:

* Firma XML
* XMLTimeStampToken
* RFC 3161 TimeStampToken
* PKCS#7
* PKCS#1
* Firmas de DSA

**Gestión de claves perdidas o comprometidas**

Si sospecha que la clave se ha perdido o se ha visto comprometida, lleve a cabo las siguientes acciones:

1. Informe a la autoridad de certificación, de modo que agregue la clave comprometida en la lista de revocación de certificados para revocar la clave.
1. Obtenga una nueva clave y sus certificados de la autoridad de certificación.
1. Vuelva a firmar los documentos firmados con la clave comprometida con la nueva clave.

