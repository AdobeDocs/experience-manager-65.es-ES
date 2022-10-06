---
title: Habilitar AEM para buscar documentos PDF protegido de seguridad de documentos y documentos de Microsoft Office
seo-title: Enable AEM to search document security protected PDF and Microsoft Office documents
description: Aprenda a habilitar la búsqueda nativa de AEM para realizar búsquedas de texto completo en documentos de PDF protegidos por DRM.
seo-description: Learn how to enable native AEM search to perform full-text search on DRM protected PDF documents.
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
feature: Document Security
exl-id: 91cbd1f1-d53d-455b-8d2c-6918b521db81
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 1%

---

# Habilitar AEM para buscar documentos PDF protegido de seguridad de documentos y documentos de Microsoft Office{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager proporciona una interfaz de usuario para buscar y localizar varios recursos almacenados en AEM. La búsqueda nativa es capaz de buscar y localizar AEM recursos y realizar búsquedas de texto en varios formatos de documento de uso común, como archivos de texto sin formato, documentos de Microsoft Office y documentos de PDF. También puede ampliar y habilitar la búsqueda nativa para realizar búsquedas de texto completo en documentos de Microsoft Office y PDF protegidos por DRM.

Realice los siguientes pasos para permitir que AEM busque documentos protegidos por seguridad de documentos PDF y documentos de Microsoft Office:

## Antes de comenzar {#before-you-start}

* Instale y configure la seguridad de documentos de AEM Forms.
* Añada el paquete sun.util.calendar a la lista de permitidos del **Deserialización de la configuración del cortafuegos.** La configuración se enumera en `https://'[server]:[port]'/system/console/configMgr`.
* Asegúrese de que todos los paquetes de AEM estén en funcionamiento. Los paquetes se enumeran en `https://'[server]:[port]'/system/console/bundles`. Si todos los paquetes no están activos, espere y compruebe el estado de los paquetes después durante unos minutos.

## Establecer una conexión segura dentro del flujo de trabajo de AEM Forms (AEM Forms en JEE) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

Una conexión segura permite un flujo de información fluido entre AEM Forms en JEE y los servicios OSGi que se ejecutan en el mismo servidor. Utilice uno de los siguientes métodos para establecer una conexión segura:

* Configurar el paquete del SDK del cliente de AEM Forms con AEM Forms en credenciales de administrador de JEE
* Configuración del paquete del SDK del cliente de AEM Forms mediante autenticación mutua

### Configurar el paquete del SDK del cliente de AEM Forms con AEM Forms en credenciales de administrador de JEE {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Abra AEM administrador de configuración e inicie sesión como administrador. La dirección URL predeterminada es https://&lt;servername>:&lt;port>/lc/system/console/configMgr.
1. Busque y abra el paquete del SDK del cliente de AEM Forms. Especifique un valor para las siguientes propiedades:

   * **URL del servidor:** Especifique la URL HTTP de AEM Forms en el servidor JEE. Para habilitar la comunicación sobre https, reinicie AEM Forms en el servidor JEE con -Djavax.net.ssl.trustStore=&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> parámetro.
   * **Nombre del servicio**: Agregue RightsManagementService a la lista de servicios especificados.
   * **Nombre de usuario:** Especifique el nombre de usuario de AEM Forms en la cuenta JEE que se utilizará para iniciar llamadas desde AEM Forms en el servidor JEE. La cuenta especificada debe tener permisos para invocar Document Services en AEM Forms en el servidor JEE.
   * **Contraseña**: Especifique la contraseña de AEM Forms en la cuenta JEE mencionada en el campo Nombre de usuario .

   Haga clic en **Guardar**. AEM está habilitado para buscar documentos PDF protegidos de seguridad de documentos y documentos de Microsoft Office.

### Configuración del paquete del SDK del cliente de AEM Forms mediante autenticación mutua {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. Habilite la autenticación mutua para AEM Forms en JEE. Para obtener información detallada, consulte [CAC y autenticación mutua](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Abra AEM administrador de configuración e inicie sesión como administrador. La dirección URL predeterminada es https://&lt;servername>:&lt;port>/lc/system/console/configMgr.
1. Busque y abra el paquete del SDK del cliente de AEM Forms. Especifique un valor para las siguientes propiedades:

   * **URL del servidor:** Especifique la URL HTTPS de AEM Forms en el servidor JEE. Para habilitar la comunicación sobre https, reinicie AEM Forms en el servidor JEE con -Djavax.net.ssl.trustStore=&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> parámetro.
   * **Habilitar SSL bidireccional**: Active la opción Enable 2-way SSL .
   * **URL del archivo KeyStore**: Especifique la dirección URL del archivo del almacén de claves.
   * **URL de la interfaz de TrustStore**: Especifique la dirección URL del archivo del almacén de confianza.
   * **Contraseña de KeyStore**: Especifique la contraseña del archivo del almacén de claves.
   * **TrustStorePassword**: Especifique la contraseña del archivo de almacén de confianza.
   * **Nombre del servicio**: Agregue RightsManagementService a la lista de servicios especificados.

   Haga clic en **Guardar**. AEM está habilitado para buscar documentos PDF protegidos de seguridad de documentos y documentos de Microsoft Office

## Indexar un PDF de ejemplo protegido por políticas o un documento de Microsoft Office {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. Inicie sesión en AEM Assets como administrador.
1. Cree una carpeta en AEM Digital Asset Manager y cargue un PDF protegido por políticas o un documento de Microsoft Office en la carpeta recién creada. Ahora, busque el contenido de los documentos protegidos por políticas utilizando AEM búsqueda. Debe devolver el documento que contiene el texto buscado.
