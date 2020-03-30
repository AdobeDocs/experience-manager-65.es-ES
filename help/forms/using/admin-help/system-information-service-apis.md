---
title: API de servicio informativo del sistema
seo-title: API de servicio informativo del sistema
description: Este documento proporciona información detallada sobre las API proporcionadas por el servicio informativo del sistema.
seo-description: Este documento proporciona información detallada sobre las API proporcionadas por el servicio informativo del sistema.
uuid: 7f624216-56e6-4d49-b9a1-3c9af045dabe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 79fccce2-d090-4b50-9c58-3f2a00e651b2
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# API de servicio informativo del sistema {#system-information-service-apis}

El servicio informativo del sistema proporciona un conjunto de API de REST para recuperar información. La siguiente tabla proporciona información detallada sobre las API:

<table>
 <thead>
  <tr>
   <th><p>Nombre</p></th>
   <th><p>URL</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>SystemInfo.properties</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.properties`</p></td>
   <td><p>Esta API es un envoltorio para la API <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()">de Java system.getProperties</a> . Recupera la configuración del entorno de trabajo actual. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.envVar</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.envVar</p></td>
   <td><p>Recupera todas las variables de entorno del sistema operativo del host. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.logs</p></td>
   <td><p>https://'[servidor]:[puerto]'/rest/services/ SystemInfo.logs</p></td>
   <td><p>Descarga un archivo zip que contiene registros del servidor de aplicaciones. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.config</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.config</p></td>
   <td><p>Recupera todo el contenido del archivo config.xml. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.services</p></td>
   <td><p>https://'[servidor]:[puerto]'/rest/services/ SystemInfo.services</p></td>
   <td><p>Recupera el estado y los parámetros de configuración de los servicios de formularios AEM.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.vitalDetails</p></td>
   <td><p>Recupera tiempo activo del servidor, argumentos JVM, memoria del sistema, tamaño del montón, nombre del sistema operativo, número de subprocesos activos y recuento de subprocesos. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.coreSettings</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.coreSettings</p></td>
   <td><p>Recupera valores de las siguientes propiedades:</p>
    <ul>
     <li><p>AdobeTempDir</p></li>
     <li><p>AdobeServerFontDir</p></li>
     <li><p>CustomerFontDir</p></li>
     <li><p>GlobalDocumentStorageRootDir</p></li>
     <li><p>DefaultDocumentMaxInlineSize</p></li>
     <li><p>DefaultDocumentDisposeTimeout</p></li>
     <li><p>EnableDocumentDBStorage</p></li>
     <li><p>GlobalDocumentStorageUseNetworkShare</p></li>
     <li><p>EnableFIPS</p></li>
     <li><p>EnableWSDL</p></li>
     <li><p>DataServicesConfigFile </p></li>
     <li><p>EnableRDS</p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.database</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.database</p></td>
   <td><p>Recupera información detallada sobre la base de datos.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.licenseInfo</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.licenseInfo</p></td>
   <td><p>Recupera la información de versión y licencia de los componentes de formularios AEM instalados. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.serverConfig</p></td>
   <td><p>Descarga los archivos de configuración del servidor de aplicaciones host. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.thread?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.thread?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>Recupera el recuento y el seguimiento de pila de subprocesos activos. Acepta los siguientes parámetros:</p>
    <ul>
     <li><p>iteraciones= [n]: Especifica el recuento de iteraciones. Sustituya n por un número. </p></li>
     <li><p>Retraso= [n]: Especifica el número de milisegundos que hay que esperar antes de iniciar la siguiente iteración. </p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.info</p></td>
   <td><p>https://'[servidor]:[puerto]'/rest/services/ SystemInfo.info</p></td>
   <td><p>Esta API es un envoltorio para todas las API de servicio informativo del sistema. Internamente, ejecuta todas las API de información del sistema y descarga información en formato zip. </p><p><i><strong>nota</strong>: SystemInfo.info no proporciona el seguimiento de recuento y pila de subprocesos activos. </i></p></td>
  </tr>
 </tbody>
</table>

