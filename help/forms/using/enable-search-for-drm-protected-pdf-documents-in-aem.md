---
title: Habilitar AEM para buscar documentos PDF protegidos por seguridad de documento
seo-title: Habilitar AEM para buscar documentos PDF protegidos por seguridad de documento
description: 'Obtenga información sobre cómo habilitar la búsqueda de AEM nativa para realizar búsquedas de texto completo en documentos PDF protegidos con DRM.  '
seo-description: 'Obtenga información sobre cómo habilitar la búsqueda de AEM nativa para realizar búsquedas de texto completo en documentos PDF protegidos con DRM.  '
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


# Habilitar AEM para buscar documentos PDF protegidos por seguridad de documento{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM búsqueda permite buscar y localizar AEM recursos y realizar búsquedas de texto en diversos formatos de documento utilizados con frecuencia, como archivos de texto sin formato, documentos de Microsoft Office y documentos PDF. También puede ampliar la búsqueda nativa para realizar búsquedas de texto completo en [Documentos PDF protegidos con AEM seguridad de Documento](../../forms/using/admin-help/document-security.md). Para permitir que AEM realice búsquedas de texto completo en dichos documentos, lleve a cabo los siguientes pasos:

1. Establecimiento de una conexión segura
1. Indexar un documento PDF de muestra protegido por una política

## Requisitos previos {#prerequisites}

* Si está utilizando AEM Forms en OSGi:

   * Instale el [paquete del indizador de seguridad de AEM Forms Documento](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html) en el servidor AEM Forms.

   * Asegúrese de que un AEM Forms en el servidor JEE esté activo y en ejecución y de que la seguridad de documento esté instalada en el AEM Forms correspondiente en el servidor JEE. El formulario AEM en el servidor JEE es necesario para indexar el documento protegido.

* Si solo utiliza AEM Forms en el servidor JEE, el paquete de indizador ya está instalado.
* Asegúrese de que todos los paquetes estén en funcionamiento. Si todos los paquetes no están activos, espere hasta que todos los paquetes estén en funcionamiento.

   * Para AEM Forms en OSGi, los paquetes se enumeran en https://&#39;[server]:[port]&#39;/system/console/buncles.
   * Para AEM Forms en JEE, los paquetes se muestran en https://&#39;[server]:[port]&#39;/[context-path]/system/console/buncles. Por ejemplo, https://localhost:8080/lc/system/console/bundles.

* Añada el paquete *sun.util.calendar* a la lista de permitidos. Para agregar el paquete a la lista de permitidos, realice los siguientes pasos:

   1. Abra AEM consola web. La dirección URL es https://&#39;[server]:[port]&#39;/system/console/configMgr.
   1. Busque y abra **Deserialization Firewall Configuration**.

   1. Añada el paquete sun.util.calendar al campo de prefijos de paquetes o clases Incluidas en la lista de permitidos y haga clic en **Guardar**.

### Establezca una conexión segura entre las pilas JEE de AEM Forms y OSGi {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

Puede utilizar uno de los siguientes métodos para establecer la conexión segura:

* Configurar el paquete SDK de Adobe LiveCycle Client con AEM Forms en las credenciales de administrador de JEE
* Configurar el paquete SDK del cliente de Adobe LiveCycle mediante autenticación mutua

#### Configurar el paquete SDK de cliente de Adobe LiveCycle con AEM Forms en las credenciales de administrador de JEE {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Abra AEM consola web. La dirección URL es https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Busque y abra el **paquete del SDK del cliente de Adobe LiveCycle**. Especifique un valor para los campos siguientes:

   * **URL del servidor:** especifique la URL HTTPS de AEM Forms en el servidor JEE. Para habilitar la comunicación sobre https, reinicie el servidor con el parámetro -Djavax.net.ssl.trustStore=&lt;ruta de AEM Forms en el archivo de almacén de claves JEE>.
   * **Nombre** del servicio: Añada RightsManagementService a la lista de los servicios especificados.
   * **Nombre de usuario:** especifique el nombre de usuario de la cuenta AEM Forms en JEE que se va a utilizar para iniciar llamadas desde AEM servidor. La cuenta especificada debe tener permisos para servicios de inicio documento en AEM Forms en el servidor JEE.
   * **Contraseña**: Especifique la contraseña del AEM Forms en la cuenta JEE mencionada en el campo Nombre de usuario.

   Haga clic en **Guardar.** AEM está habilitado para buscar documentos PDF protegidos por seguridad de documento.

#### Configurar el paquete SDK del cliente de Adobe LiveCycle mediante autenticación mutua {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. Habilite la autenticación mutua para AEM Forms en JEE. Para obtener información detallada, consulte [CAC y Autenticación mutua](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Abra AEM consola web. La dirección URL es https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Busque y abra el paquete **SDK del cliente de LiveCycle de Adobe**. Especifique un valor para las siguientes propiedades:

   * **URL** del servidor: Especifique la URL HTTPS de AEM Forms en el servidor JEE. Para habilitar la comunicación sobre https, reinicie el servidor de AEM con el parámetro -Djavax.net.ssl.trustStore=&lt;ruta de AEM Forms en el archivo de almacén de claves JEE>.
   * **Habilitar SSL** bidireccional: Active la opción Activar SSL bidireccional.
   * **URL** del archivo KeyStore: Especifique la dirección URL del archivo de almacén de claves.
   * **URL** de la carpeta TrustStore: Especifique la dirección URL del archivo de almacén de confianza.
   * **Contraseña** de KeyStore: Especifique la contraseña del archivo de almacén de claves.
   * **TrustStorePassword**: Especifique la contraseña del archivo de almacén de confianza.
   * **Nombre** del servicio: Añada RightsManagementService a la lista de los servicios especificados.

   Haga clic en **Guardar.** AEM está habilitado para buscar documentos PDF protegidos por seguridad de documento

### Indique un documento PDF de muestra protegido por una política {#index-a-sample-policy-protected-pdf-document}

1. Inicie sesión en AEM Assets como administrador.
1. Cree una carpeta en AEM Administrador de recursos digitales y cargue los documentos PDF protegidos por políticas en la carpeta recién creada.

   Ahora puede buscar los documentos protegidos por políticas mediante AEM búsqueda.

