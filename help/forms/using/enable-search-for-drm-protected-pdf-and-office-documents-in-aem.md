---
title: Permitir que AEM busque en PDF protegidos por seguridad de documento y en documentos de Microsoft Office
seo-title: Permitir que AEM busque en PDF protegidos por seguridad de documento y en documentos de Microsoft Office
description: Obtenga información sobre cómo activar la búsqueda nativa de AEM para realizar búsquedas de texto completo en documentos PDF protegidos por DRM.
seo-description: Obtenga información sobre cómo activar la búsqueda nativa de AEM para realizar búsquedas de texto completo en documentos PDF protegidos por DRM.
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Permitir que AEM busque en PDF protegidos por seguridad de documento y en documentos de Microsoft Office{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager proporciona una interfaz de usuario para buscar y localizar varios recursos almacenados en AEM. La búsqueda nativa permite buscar y localizar recursos de AEM y realizar búsquedas de texto en varios formatos de documento de uso común, como archivos de texto sin formato, documentos de Microsoft Office y documentos PDF. También puede ampliar y habilitar la búsqueda nativa para realizar búsquedas de texto completo en archivos PDF protegidos con DRM y documentos de Microsoft Office.

Realice los siguientes pasos para permitir que AEM busque en PDF y documentos de Microsoft Office protegidos por seguridad de documento:

## Antes de comenzar {#before-you-start}

* Instale y configure la seguridad de documento de AEM Forms.
* Añada el paquete sun.util.calendar a la lista blanca de la Configuración del cortafuegos de **deserialización.** La configuración se muestra en `https://'[server]:[port]'/system/console/configMgr`.
* Asegúrese de que todos los paquetes de AEM estén en funcionamiento. Los paquetes están enumerados en `https://'[server]:[port]'/system/console/bundles`. Si todos los paquetes no están activos, espere y compruebe el estado de los paquetes después de unos minutos.

## Establecimiento de una conexión segura en el flujo de trabajo de AEM Forms (AEM Forms en JEE) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

Una conexión segura permite un flujo perfecto de información entre AEM Forms en JEE y los servicios OSGi que se ejecutan en el mismo servidor. Utilice uno de los siguientes métodos para establecer una conexión segura:

* Configuración del paquete de SDK de AEM Forms Client con AEM Forms en credenciales de administrador de JEE
* Configuración del paquete SDK de AEM Forms Client mediante autenticación mutua

### Configuración del paquete de SDK de AEM Forms Client con AEM Forms en credenciales de administrador de JEE {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Abra el administrador de configuración de AEM e inicie sesión como administrador. La dirección URL predeterminada es https://&lt;serverName>:&lt;port>/lc/system/console/configMgr.
1. Busque y abra el paquete del SDK del cliente de AEM Forms. Especifique un valor para las siguientes propiedades:

   * **URL del servidor:** Especifique la URL HTTP de AEM Forms en el servidor JEE. Para habilitar la comunicación a través de https, reinicie AEM Forms en el servidor JEE con el parámetro -Djavax.net.ssl.trustStore=&lt;ruta de AEM Forms en el archivo de almacén de claves JEE>.
   * **Nombre** del servicio: Añada RightsManagementService a la lista de los servicios especificados.
   * **Nombre de usuario:** Especifique el nombre de usuario de AEM Forms en la cuenta JEE para iniciar llamadas desde AEM Forms en el servidor JEE. La cuenta especificada debe tener permisos para invocar servicios de Documento en AEM Forms en el servidor JEE.
   * **Contraseña**: Especifique la contraseña de AEM Forms en la cuenta JEE mencionada en el campo Nombre de usuario.
   Haga clic en **Guardar.** AEM está habilitado para buscar documentos PDF y de Microsoft Office protegidos contra la seguridad de documento.

### Configuración del paquete SDK de AEM Forms Client mediante autenticación mutua {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. Habilite la autenticación mutua para AEM Forms en JEE. Para obtener información detallada, consulte [CAC y Autenticación](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)mutua.
1. Abra el administrador de configuración de AEM e inicie sesión como administrador. La dirección URL predeterminada es https://&lt;serverName>:&lt;port>/lc/system/console/configMgr.
1. Busque y abra el paquete del SDK del cliente de AEM Forms. Especifique un valor para las siguientes propiedades:

   * **URL del servidor:** Especifique la URL HTTPS de AEM Forms en el servidor JEE. Para habilitar la comunicación a través de https, reinicie AEM Forms en el servidor JEE con el parámetro -Djavax.net.ssl.trustStore=&lt;ruta de AEM Forms en el archivo de almacén de claves JEE>.
   * **Habilitar SSL** bidireccional: Active la opción Activar SSL bidireccional.
   * **URL** del archivo KeyStore: Especifique la dirección URL del archivo de almacén de claves.
   * **URL** de la carpeta TrustStore: Especifique la dirección URL del archivo de almacén de confianza.
   * **Contraseña** de KeyStore: Especifique la contraseña del archivo de almacén de claves.
   * **TrustStorePassword**: Especifique la contraseña del archivo de almacén de confianza.
   * **Nombre** del servicio: Añada RightsManagementService a la lista de los servicios especificados.
   Haga clic en **Guardar.** AEM está habilitado para buscar archivos PDF protegidos por seguridad de documento y documentos de Microsoft Office

## Indique un PDF de muestra protegido por una política o un documento de Microsoft Office {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. Inicie sesión en Recursos AEM como administrador.
1. Cree una carpeta en AEM Digital Asset Manager y cargue un PDF protegido por una política o un documento de Microsoft Office en la carpeta recién creada. Ahora, busque el contenido de los documentos protegidos por políticas mediante la búsqueda de AEM. Debe devolver el documento que contiene el texto buscado.

