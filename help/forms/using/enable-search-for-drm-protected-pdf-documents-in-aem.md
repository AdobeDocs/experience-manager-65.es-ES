---
title: Habilitar AEM para buscar documentos PDF protegidos de seguridad de documentos
seo-title: Enable AEM to search document security protected PDF documents
description: Aprenda a habilitar la búsqueda nativa de AEM para realizar búsquedas de texto completo en documentos de PDF protegidos por DRM.
seo-description: Learn how to enable native AEM search to perform full-text search on DRM protected PDF documents.
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
feature: Document Security
exl-id: 7cf17fb6-021a-473e-bc3b-27c317953002
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---

# Habilitar AEM para buscar documentos PDF protegidos de seguridad de documentos{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM búsqueda es capaz de buscar y localizar AEM recursos y realizar búsquedas de texto en varios formatos de documento de uso común, como archivos de texto sin formato, documentos de Microsoft Office y documentos de PDF. También puede ampliar la búsqueda nativa para realizar búsquedas de texto completo en [Documentos de PDF protegidos con seguridad AEM documento](../../forms/using/admin-help/document-security.md). Para permitir que AEM realice búsquedas de texto completo en dichos documentos, realice los siguientes pasos:

1. Establecer una conexión segura
1. Indexar un documento de PDF protegido por políticas de muestra

## Requisitos previos {#prerequisites}

* Si utiliza AEM Forms en OSGi:

   * Instalar [Paquete de AEM Forms Document Security Indexer](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html) en el servidor de AEM Forms.

   * Asegúrese de que haya una AEM Forms en el servidor JEE en funcionamiento y de que la seguridad de los documentos esté instalada en la AEM Forms correspondiente del servidor JEE. El formulario AEM en el servidor JEE es necesario para indexar el documento protegido.

* Si solo utiliza AEM Forms en el servidor JEE, el paquete del indizador ya está instalado.
* Asegúrese de que todos los paquetes estén en funcionamiento. Si todos los paquetes no están activos, espere hasta que todos los paquetes estén en funcionamiento.

   * Para AEM Forms en OSGi, los paquetes se enumeran en https://&#39;[server]:[puerto]&#39;/system/console/bundles.
   * Para AEM Forms en JEE, los paquetes se enumeran en https://&#39;[server]:[puerto]&#39;/[context-path]/system/console/bundles. Por ejemplo, https://localhost:8080/lc/system/console/bundles.

* Agregue la variable *sun.util.calendar* a la lista de permitidos. Para agregar el paquete a la lista de permitidos, realice los siguientes pasos:

   1. Abra AEM consola web. La dirección URL es https://&#39;[server]:[puerto]&#39;/system/console/configMgr.
   1. Localizar y abrir **Deserialización de la configuración de Firewall**.

   1. Agregue el paquete sun.util.calendar al campo de prefijos de paquetes o clases Incluidas en la lista de permitidos y haga clic en **Guardar**.

### Establecer una conexión segura entre las pilas AEM Forms JEE y OSGi {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

Puede utilizar uno de los siguientes métodos para establecer la conexión segura:

* Configurar el paquete del SDK del cliente de LiveCycle de Adobe con AEM Forms en las credenciales de administrador de JEE
* Configuración del paquete del SDK del cliente de LiveCycle de Adobe mediante autenticación mutua

#### Configurar el paquete del SDK del cliente de LiveCycle de Adobe con AEM Forms en las credenciales de administrador de JEE {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Abra AEM consola web. La dirección URL es https://&#39;[server]:[puerto]&#39;/system/console/configMgr.
1. Busque y abra el **Paquete de SDK de cliente de LiveCycle de Adobe**. Especifique un valor para los campos siguientes:

   * **URL del servidor:** Especifique la URL HTTPS de AEM Forms en el servidor JEE. Para habilitar la comunicación sobre https, reinicie el servidor con -Djavax.net.ssl.trustStore=&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> parámetro.
   * **Nombre del servicio**: Agregue RightsManagementService a la lista de servicios especificados.
   * **Nombre de usuario:** Especifique el nombre de usuario de AEM Forms en la cuenta JEE que se utilizará para iniciar llamadas desde AEM servidor. La cuenta especificada debe tener permisos para iniciar document services en AEM Forms en el servidor JEE.
   * **Contraseña**: Especifique la contraseña de AEM Forms en la cuenta JEE mencionada en el campo Nombre de usuario .

   Haga clic en **Guardar**. AEM está habilitado para buscar documentos PDF protegidos por seguridad de documentos.

#### Configuración del paquete del SDK del cliente de LiveCycle de Adobe mediante autenticación mutua {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. Habilite la autenticación mutua para AEM Forms en JEE. Para obtener información detallada, consulte [CAC y autenticación mutua](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Abra AEM consola web. La dirección URL es https://&#39;[server]:[puerto]&#39;/system/console/configMgr.
1. Busque y abra el **SDK de cliente de LiveCycle de Adobe** Paquete. Especifique un valor para las siguientes propiedades:

   * **URL del servidor**: Especifique la URL HTTPS de AEM Forms en el servidor JEE. Para habilitar la comunicación sobre https, reinicie el servidor AEM con -Djavax.net.ssl.trustStore=&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> parámetro.
   * **Habilitar SSL bidireccional**: Active la opción Enable 2-way SSL .
   * **URL del archivo KeyStore**: Especifique la dirección URL del archivo del almacén de claves.
   * **URL de la interfaz de TrustStore**: Especifique la dirección URL del archivo del almacén de confianza.
   * **Contraseña de KeyStore**: Especifique la contraseña del archivo del almacén de claves.
   * **TrustStorePassword**: Especifique la contraseña del archivo de almacén de confianza.
   * **Nombre del servicio**: Agregue RightsManagementService a la lista de servicios especificados.

   Haga clic en **Guardar**. AEM está habilitado para buscar documentos PDF protegidos de seguridad de documentos

### Indexar un documento de PDF protegido por políticas de muestra {#index-a-sample-policy-protected-pdf-document}

1. Inicie sesión en AEM Assets como administrador.
1. Cree una carpeta en AEM Digital Asset Manager y cargue los documentos de PDF protegidos por políticas en la carpeta recién creada.

   Ahora, puede buscar los documentos protegidos por políticas mediante AEM búsqueda.
