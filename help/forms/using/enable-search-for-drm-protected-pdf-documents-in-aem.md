---
title: Habilitar AEM para buscar documentos PDF protegidos por seguridad de documentos
seo-title: Habilitar AEM para buscar documentos PDF protegidos por seguridad de documentos
description: 'Aprenda a habilitar la búsqueda nativa de AEM para realizar búsquedas de texto completo en documentos PDF protegidos por DRM.  '
seo-description: 'Aprenda a habilitar la búsqueda nativa de AEM para realizar búsquedas de texto completo en documentos PDF protegidos por DRM.  '
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 1%

---


# Habilitar AEM para buscar documentos PDF protegidos por seguridad de documentos{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM búsqueda es capaz de buscar y localizar AEM recursos y realizar búsquedas de texto en varios formatos de documento de uso común, como archivos de texto sin formato, documentos de Microsoft Office y documentos PDF. También puede ampliar la búsqueda nativa para realizar búsquedas de texto completo en [documentos PDF protegidos con AEM seguridad de documento](../../forms/using/admin-help/document-security.md). Para permitir que AEM realice búsquedas de texto completo en dichos documentos, realice los siguientes pasos:

1. Establecer una conexión segura
1. Indexar un documento PDF de muestra protegido por políticas

## Requisitos previos {#prerequisites}

* Si utiliza AEM Forms en OSGi:

   * Instale [AEM Forms Document Security Indexer package](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html) en el servidor de AEM Forms.

   * Asegúrese de que haya una AEM Forms en el servidor JEE en funcionamiento y de que la seguridad de los documentos esté instalada en la AEM Forms correspondiente del servidor JEE. El formulario AEM en el servidor JEE es necesario para indexar el documento protegido.

* Si solo utiliza AEM Forms en el servidor JEE, el paquete del indizador ya está instalado.
* Asegúrese de que todos los paquetes estén en funcionamiento. Si todos los paquetes no están activos, espere hasta que todos los paquetes estén en funcionamiento.

   * Para AEM Forms en OSGi, los paquetes se enumeran en https://&#39;[server]:[port]&#39;/system/console/bundles.
   * Para AEM Forms en JEE, los paquetes se enumeran en https://&#39;[server]:[port]&#39;/[context-path]/system/console/bundles. Por ejemplo, https://localhost:8080/lc/system/console/bundles.

* Agregue el paquete *sun.util.calendar* a la lista de permitidos. Para agregar el paquete a la lista de permitidos, realice los siguientes pasos:

   1. Abra AEM consola web. La dirección URL es https://&#39;[server]:[port]&#39;/system/console/configMgr.
   1. Busque y abra **Deserialization Firewall Configuration**.

   1. Agregue el paquete sun.util.calendar al campo de prefijos de paquetes o clases Incluidas en la lista de permitidos y haga clic en **Guardar**.

### Establezca una conexión segura entre AEM Forms JEE y las pilas OSGi {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

Puede utilizar uno de los siguientes métodos para establecer la conexión segura:

* Configurar el paquete del SDK del cliente de LiveCycle de Adobe con AEM Forms en las credenciales de administrador de JEE
* Configuración del paquete del SDK del cliente de LiveCycle de Adobe mediante autenticación mutua

#### Configurar el paquete del SDK del cliente de LiveCycle de Adobe con AEM Forms en las credenciales de administrador de JEE {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Abra AEM consola web. La dirección URL es https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Localice y abra el **paquete del SDK del cliente de LiveCycle de Adobe**. Especifique un valor para los campos siguientes:

   * **URL del servidor:** especifique la URL HTTPS de AEM Forms en el servidor JEE. Para habilitar la comunicación sobre https, reinicie el servidor con el parámetro -Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file> .
   * **Nombre** del servicio: Agregue RightsManagementService a la lista de servicios especificados.
   * **Nombre de usuario:** especifique el nombre de usuario de AEM Forms en la cuenta JEE que se va a usar para iniciar llamadas desde AEM servidor. La cuenta especificada debe tener permisos para iniciar document services en AEM Forms en el servidor JEE.
   * **Contraseña**: Especifique la contraseña de AEM Forms en la cuenta JEE mencionada en el campo Nombre de usuario .

   Haga clic en **Guardar**. AEM está habilitado para buscar documentos PDF protegidos por seguridad de documentos.

#### Configurar el paquete del SDK del cliente de LiveCycle de Adobe mediante autenticación mutua {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. Habilite la autenticación mutua para AEM Forms en JEE. Para obtener información detallada, consulte [CAC y autenticación mutua](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Abra AEM consola web. La dirección URL es https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Busque y abra el paquete **Adobe LiveCycle Client SDK**. Especifique un valor para las siguientes propiedades:

   * **URL** del servidor: Especifique la URL HTTPS de AEM Forms en el servidor JEE. Para habilitar la comunicación sobre https, reinicie el servidor de AEM con el parámetro -Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file> .
   * **Habilitar SSL** bidireccional: Active la opción Enable 2-way SSL .
   * **URL** del archivo KeyStore: Especifique la dirección URL del archivo del almacén de claves.
   * **URL** de archivo de TrustStore: Especifique la dirección URL del archivo del almacén de confianza.
   * **Contraseña de KeyStore**: Especifique la contraseña del archivo del almacén de claves.
   * **TrustStorePassword**: Especifique la contraseña del archivo de almacén de confianza.
   * **Nombre** del servicio: Agregue RightsManagementService a la lista de servicios especificados.

   Haga clic en **Guardar**. AEM está habilitado para buscar documentos PDF protegidos por seguridad de documentos

### Indexar un documento PDF de muestra protegido por políticas {#index-a-sample-policy-protected-pdf-document}

1. Inicie sesión en AEM Assets como administrador.
1. Cree una carpeta en AEM Digital Asset Manager y cargue los documentos PDF protegidos por políticas en la carpeta recién creada.

   Ahora, puede buscar los documentos protegidos por políticas mediante AEM búsqueda.

