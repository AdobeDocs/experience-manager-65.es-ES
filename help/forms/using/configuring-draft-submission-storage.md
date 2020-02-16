---
title: Configuración de los servicios de almacenamiento para borradores y envíos
seo-title: Configuración de los servicios de almacenamiento para borradores y envíos
description: Obtenga información sobre cómo configurar el almacenamiento para borradores y envíos
seo-description: Obtenga información sobre cómo configurar el almacenamiento para borradores y envíos
uuid: 2f4efc07-312c-4908-8c91-84f4e6c5ad25
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6ebb6420-68b6-4abc-b298-c252db038416
translation-type: tm+mt
source-git-commit: f9ed171c188a4dfb71f12ae9c98105a4c1895542

---


# Configuración de los servicios de almacenamiento para borradores y envíos {#configuring-storage-services-for-drafts-and-submissions}

## Información general {#overview}

Con AEM Forms, puede almacenar:

* **Borradores**: Formulario de trabajo en curso que los usuarios finales rellenan y guardan para después y envían después.

* **Envíos**: Se han enviado formularios que contienen datos proporcionados por el usuario.

Los servicios de metadatos y datos de AEM Forms Portal permiten crear borradores y envíos. De forma predeterminada, los datos se almacenan en la instancia de publicación, que luego se replican de forma inversa en la instancia de autor configurada para que estén disponibles para la percolación en otras instancias de publicación.

La preocupación con el enfoque ya existente es que almacena todos los datos en la instancia de publicación, incluidos los datos que pueden ser Información personal identificable (PII).

Además del método predeterminado mencionado anteriormente, también hay una implementación alternativa disponible para insertar directamente los datos del formulario en el procesamiento en lugar de guardarlos localmente. Los clientes que tengan problemas con el almacenamiento de datos potencialmente confidenciales en una instancia de publicación pueden elegir la implementación alternativa en la que los datos se envían a un servidor de procesamiento. Dado que el procesamiento ocurre en la instancia de autor, suele permanecer en una zona segura.

>[!NOTE]
>
>Cuando se utiliza la acción de envío de Forms Portal o se activa la opción Almacenar datos en el portal de formularios en un formulario adaptable, los datos del formulario se almacenan en el repositorio de AEM. En un entorno de producción, se recomienda no almacenar datos de formulario enviados o borrador en el repositorio de AEM. En su lugar, debe integrar los borradores y el componente de envío con un almacenamiento seguro como la base de datos empresarial para almacenar borradores y datos de formularios enviados.
>
>Para obtener más información, consulte [Ejemplo para integrar el componente de borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md).

## Configuración de los servicios de borradores y envíos de Forms Portal {#configuring-forms-portal-drafts-and-submissions-services}

En Configuración de la consola web de AEM ( `https://[host]:[port]/system/console/configMgr`), haga clic para abrir el borrador del portal de **formularios y la configuración** de envío en modo de edición.

Especifique los valores de las propiedades en función de sus requisitos, tal como se describe a continuación:

### Servicios predeterminados para almacenar datos en una instancia de publicación {#out-of-the-box-services-to-store-data-on-publish-instance}

Los datos se replican de forma inversa en la instancia de autor configurada.

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Value</th>
  </tr>
  <tr>
   <td>Servicio de datos de borrador de Forms Portal(Identificador para el servicio de datos de borrador (<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Servicio de metadatos de borrador de Forms Portal (identificador para el servicio de metadatos de borrador (<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Servicio de envío de datos de Forms Portal (identificador para el servicio de envío de datos (<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Servicio de envío de metadatos de Forms Portal (identificador para el servicio de envío de metadatos (<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### Servicios predeterminados para almacenar datos en instancias de procesamiento remoto {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

Los datos se insertan directamente en la instancia remota configurada

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Value</th>
  </tr>
  <tr>
   <td>Servicio de datos de borrador de Forms Portal(Identificador para el servicio de datos de borrador (<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Servicio de metadatos de borrador de Forms Portal (identificador para el servicio de metadatos de borrador (<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Servicio de envío de datos de Forms Portal (identificador para el servicio de envío de datos (<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Servicio de envío de metadatos de Forms Portal (identificador para el servicio de envío de metadatos (<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

Aparte de la configuración especificada arriba, proporcione información sobre la instancia de procesamiento remoto configurada.

En Configuración de la consola web de AEM ( `https://[host]:[port]/system/console/configMgr`), haga clic para abrir el servicio **de configuración de** AEM DS en modo de edición. En el cuadro de diálogo Servicio de configuración de AEM DS, proporcione información sobre el procesamiento de la URL del servidor, el nombre de usuario del servidor de procesamiento y la contraseña.

>[!NOTE]
>
>También se proporciona una implementación de muestra para almacenar datos de usuario en una base de datos. Para comprender cómo configurar los servicios de datos y metadatos para almacenar datos de usuario en una base de datos externa, consulte [Ejemplo para integrar componentes de borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md).

