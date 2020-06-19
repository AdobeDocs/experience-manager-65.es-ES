---
title: Permitir que AEM busque documentos PDF protegidos por la seguridad de documento
seo-title: Permitir que AEM busque documentos PDF protegidos por la seguridad de documento
description: 'Obtenga información sobre cómo activar la búsqueda nativa de AEM para realizar búsquedas de texto completo en documentos PDF protegidos por DRM.  '
seo-description: 'Obtenga información sobre cómo activar la búsqueda nativa de AEM para realizar búsquedas de texto completo en documentos PDF protegidos por DRM.  '
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---


# Permitir que AEM busque documentos PDF protegidos por la seguridad de documento{#enable-aem-to-search-document-security-protected-pdf-documents}

La búsqueda de AEM permite buscar y localizar recursos de AEM y realizar búsquedas de texto en varios formatos de documento de uso común, como archivos de texto sin formato, documentos de Microsoft Office y documentos PDF. También puede ampliar la búsqueda nativa para realizar búsquedas de texto completo en Documentos [PDF protegidos con seguridad](../../forms/using/admin-help/document-security.md)de AEM Documento. Para permitir que AEM realice búsquedas de texto completo en dichos documentos, lleve a cabo los siguientes pasos:

1. Establecimiento de una conexión segura
1. Indexar un documento PDF de muestra protegido por una política

## Requisitos previos {#prerequisites}

* Si está utilizando AEM Forms en OSGi:

   * Instale el paquete [](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html) AEM Forms Documento Security Indexer en el servidor de AEM Forms.

   * Asegúrese de que un AEM Forms del servidor JEE esté activo y en funcionamiento y de que la seguridad de documento esté instalada en los AEM Forms correspondientes del servidor JEE. El formulario AEM en el servidor JEE es necesario para indexar el documento protegido.

* Si solo utiliza AEM Forms en el servidor JEE, el paquete de indizador ya está instalado.
* Asegúrese de que todos los paquetes estén en funcionamiento. Si todos los paquetes no están activos, espere hasta que todos los paquetes estén en funcionamiento.

   * Para los AEM Forms en OSGi, los paquetes se muestran en https://&#39;[server]:[port]&#39;/system/console/buncles.
   * Para AEM Forms en JEE, los paquetes se muestran en https://&#39;[server]:[port]&#39;/[context-path]/system/console/buncles. Por ejemplo, https://localhost:8080/lc/system/console/bundles.

* Añada el paquete *sun.util.calendar* a la lista permitida. Para agregar el paquete a la lista de permitidos, realice los siguientes pasos:

   1. Abra la consola web de AEM. La dirección URL es https://&#39;[server]:[port]&#39;/system/console/configMgr.
   1. Localice y abra **Deserialization Firewall Configuration**.

   1. Añada el paquete sun.util.calendar al campo Clases permitidas o prefijos de paquete y haga clic en **Guardar**.

### Establecer una conexión segura entre las pilas JEE y OSGi de AEM Forms {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

Puede utilizar uno de los siguientes métodos para establecer la conexión segura:

* Configurar el paquete de SDK de Adobe LiveCycle Client con AEM Forms en las credenciales de administrador de JEE
* Configurar el paquete de SDK de Adobe LiveCycle Client mediante autenticación mutua

#### Configurar el paquete de SDK de Adobe LiveCycle Client con AEM Forms en las credenciales de administrador de JEE {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Abra la consola web de AEM. La dirección URL es https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Busque y abra el paquete de SDK de **Adobe LiveCycle Client**. Especifique un valor para los campos siguientes:

   * **URL del servidor:** Especifique la URL HTTPS de AEM Forms en el servidor JEE. Para habilitar la comunicación sobre https, reinicie el servidor con el parámetro -Djavax.net.ssl.trustStore=&lt;ruta de AEM Forms en el archivo de almacén de claves JEE>.
   * **Nombre** del servicio: Añada RightsManagementService a la lista de los servicios especificados.
   * **Nombre de usuario:** Especifique el nombre de usuario de los AEM Forms de la cuenta JEE que se utilizarán para iniciar llamadas desde el servidor AEM. La cuenta especificada debe tener permisos para servicios de inicio documento en los AEM Forms del servidor JEE.
   * **Contraseña**: Especifique la contraseña de los AEM Forms de la cuenta JEE que se mencionan en el campo Nombre de usuario.

   Haga clic en **Guardar.** AEM está habilitado para buscar documentos PDF protegidos por seguridad de documento.

#### Configurar el paquete de SDK de Adobe LiveCycle Client mediante autenticación mutua {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. Habilite la autenticación mutua para AEM Forms en JEE. Para obtener información detallada, consulte [CAC y Autenticación](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)mutua.
1. Abra la consola web de AEM. La dirección URL es https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Busque y abra el paquete de SDK **de** Adobe LiveCycle Client. Especifique un valor para las siguientes propiedades:

   * **URL** del servidor: Especifique la URL HTTPS de AEM Forms en el servidor JEE. Para habilitar la comunicación a través de https, reinicie el servidor AEM con el parámetro -Djavax.net.ssl.trustStore=&lt;ruta de AEM Forms en el archivo de almacén de claves JEE>.
   * **Habilitar SSL** bidireccional: Active la opción Activar SSL bidireccional.
   * **URL** del archivo KeyStore: Especifique la dirección URL del archivo de almacén de claves.
   * **URL** de la carpeta TrustStore: Especifique la dirección URL del archivo de almacén de confianza.
   * **Contraseña** de KeyStore: Especifique la contraseña del archivo de almacén de claves.
   * **TrustStorePassword**: Especifique la contraseña del archivo de almacén de confianza.
   * **Nombre** del servicio: Añada RightsManagementService a la lista de los servicios especificados.

   Haga clic en **Guardar.** AEM está habilitado para buscar documentos PDF protegidos por seguridad de documento

### Indexar un documento PDF de muestra protegido por una política {#index-a-sample-policy-protected-pdf-document}

1. Inicie sesión como administrador en AEM Assets.
1. Cree una carpeta en AEM Digital Asset Manager y cargue los documentos PDF protegidos por políticas en la carpeta recién creada.

   Ahora puede buscar en los documentos protegidos por políticas mediante la búsqueda de AEM.

