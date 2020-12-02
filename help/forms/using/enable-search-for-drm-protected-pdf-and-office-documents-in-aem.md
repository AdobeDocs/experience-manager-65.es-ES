---
title: Habilitar AEM para buscar en los documentos PDF y de Microsoft Office protegidos por seguridad de documento
seo-title: Habilitar AEM para buscar en los documentos PDF y de Microsoft Office protegidos por seguridad de documento
description: Obtenga información sobre cómo habilitar la búsqueda de AEM nativa para realizar búsquedas de texto completo en documentos PDF protegidos con DRM.
seo-description: Obtenga información sobre cómo habilitar la búsqueda de AEM nativa para realizar búsquedas de texto completo en documentos PDF protegidos con DRM.
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 1%

---


# Habilitar AEM para buscar en archivos PDF protegidos por seguridad de documento y documentos de Microsoft Office{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager proporciona una interfaz de usuario para buscar y localizar varios recursos almacenados en AEM. La búsqueda nativa permite buscar y localizar recursos AEM y realizar búsquedas de texto en diversos formatos de documento de uso común, como archivos de texto sin formato, documentos de Microsoft Office y documentos PDF. También puede ampliar y habilitar la búsqueda nativa para realizar búsquedas de texto completo en archivos PDF protegidos con DRM y documentos de Microsoft Office.

Realice los siguientes pasos para habilitar AEM para buscar documentos PDF y de Microsoft Office protegidos por seguridad de documento:

## Antes de comenzar {#before-you-start}

* Instale y configure la seguridad de AEM Forms documento.
* Añada el paquete sun.util.calendar a la lista de permitidos de la **Configuración del cortafuegos de deserialización.** La configuración se muestra en  `https://'[server]:[port]'/system/console/configMgr`.
* Asegúrese de que todos los paquetes de AEM estén en funcionamiento. Los paquetes se enumeran en `https://'[server]:[port]'/system/console/bundles`. Si todos los paquetes no están activos, espere y compruebe el estado de los paquetes después de unos minutos.

## Establecer una conexión segura dentro del flujo de trabajo de AEM Forms (AEM Forms en JEE) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

Una conexión segura permite un flujo fluido de información entre AEM Forms en JEE y los servicios OSGi que se ejecutan en el mismo servidor. Utilice uno de los siguientes métodos para establecer una conexión segura:

* Configurar el paquete de SDK de cliente de AEM Forms con AEM Forms en credenciales de administrador de JEE
* Configurar el paquete de SDK del cliente de AEM Forms mediante autenticación mutua

### Configurar el paquete de SDK de cliente de AEM Forms con AEM Forms en credenciales de administrador de JEE {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Abra AEM administrador de configuración e inicie sesión como administrador. La dirección URL predeterminada es https://&lt;serverName>:&lt;port>/lc/system/console/configMgr.
1. Busque y abra el paquete SDK de AEM Forms Client. Especifique un valor para las siguientes propiedades:

   * **URL del servidor:** especifique la URL HTTP de AEM Forms en el servidor JEE. Para habilitar la comunicación a través de https, reinicie el AEM Forms en el servidor JEE con el parámetro -Djavax.net.ssl.trustStore=&lt;ruta de AEM Forms en el archivo de almacén de claves JEE>.
   * **Nombre** del servicio: Añada RightsManagementService a la lista de los servicios especificados.
   * **Nombre de usuario:** especifique el nombre de usuario de AEM Forms en la cuenta JEE para iniciar llamadas desde AEM Forms en el servidor JEE. La cuenta especificada debe tener permisos para invocar servicios de Documento en el AEM Forms en el servidor JEE.
   * **Contraseña**: Especifique la contraseña del AEM Forms en la cuenta JEE mencionada en el campo Nombre de usuario.

   Haga clic en **Guardar.** AEM está habilitado para buscar documentos PDF y de Microsoft Office protegidos por seguridad de documento.

### Configurar el paquete de SDK del cliente de AEM Forms mediante autenticación mutua {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. Habilite la autenticación mutua para AEM Forms en JEE. Para obtener información detallada, consulte [CAC y Autenticación mutua](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Abra AEM administrador de configuración e inicie sesión como administrador. La dirección URL predeterminada es https://&lt;serverName>:&lt;port>/lc/system/console/configMgr.
1. Busque y abra el paquete SDK de AEM Forms Client. Especifique un valor para las siguientes propiedades:

   * **URL del servidor:** especifique la URL HTTPS de AEM Forms en el servidor JEE. Para habilitar la comunicación a través de https, reinicie el AEM Forms en el servidor JEE con el parámetro -Djavax.net.ssl.trustStore=&lt;ruta de AEM Forms en el archivo de almacén de claves JEE>.
   * **Habilitar SSL** bidireccional: Active la opción Activar SSL bidireccional.
   * **URL** del archivo KeyStore: Especifique la dirección URL del archivo de almacén de claves.
   * **URL** de la carpeta TrustStore: Especifique la dirección URL del archivo de almacén de confianza.
   * **Contraseña** de KeyStore: Especifique la contraseña del archivo de almacén de claves.
   * **TrustStorePassword**: Especifique la contraseña del archivo de almacén de confianza.
   * **Nombre** del servicio: Añada RightsManagementService a la lista de los servicios especificados.

   Haga clic en **Guardar.** AEM está habilitado para buscar documentos PDF y de Microsoft Office protegidos por seguridad de documento

## Indique un PDF de muestra protegido por una política o un documento de Microsoft Office {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. Inicie sesión en AEM Assets como administrador.
1. Cree una carpeta en AEM Administrador de recursos digitales y cargue un PDF protegido por una política o un documento de Microsoft Office en la carpeta recién creada. Ahora, busque el contenido de los documentos protegidos por políticas mediante AEM búsqueda. Debe devolver el documento que contiene el texto buscado.

