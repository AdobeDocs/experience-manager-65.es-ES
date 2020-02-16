---
title: Servicio de administración de usuarios y usuarios por usuario en comunidades de AEM
seo-title: Servicio de administración de usuarios y usuarios por usuario en comunidades de AEM
description: Utilice las API para eliminar de forma masiva y exportar de forma masiva contenido generado por el usuario, y para deshabilitar la cuenta de usuario.
seo-description: Utilice las API para eliminar de forma masiva y exportar de forma masiva contenido generado por el usuario, y para deshabilitar la cuenta de usuario.
uuid: 91180659-617d-4f6c-9a07-e680770d0d8f
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
discoiquuid: d305821d-1371-4e4a-8b28-8eee8fafa43b
docset: aem65
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780

---


# Servicio de administración de usuarios y usuarios por usuario en comunidades de AEM{#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>El RGPD se utiliza como ejemplo en las secciones que figuran a continuación, pero los detalles abarcados son aplicables a todas las normas de protección de datos y privacidad; como el RGPD, la CCPA, etc.

AEM Communities expone las API integradas para gestionar perfiles de usuario y gestionar de forma masiva el contenido generado por el usuario (UGC). Una vez activado, el servicio **UserUgcManagement** permite a los usuarios privilegiados (administradores de la comunidad y moderadores) desactivar perfiles de usuario y eliminar o exportar de forma masiva UGC para usuarios específicos. Estas API también permiten a los controladores y procesadores de datos de clientes cumplir con las normas generales de protección de datos (RGPD) de la Unión Europea y otros mandatos de privacidad inspirados en el RGPD.

Para obtener más información, consulte la página del [RGPD en el Centro](https://www.adobe.com/privacy/general-data-protection-regulation.html)de privacidad de Adobe.

>[!NOTE]
>
>Si ha configurado [Adobe Analytics en el sitio de Comunidades](/help/communities/analytics.md) AEM, los datos de usuario capturados se envían al servidor de Adobe Analytics. Adobe Analytics proporciona API que le permiten acceder, exportar y eliminar datos de usuario y cumplir con el RGPD. Para obtener más información, consulte [Enviar solicitudes](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/gdpr_submit_access_delete.html)de acceso y eliminación.

Para poner estas API en uso, debe habilitar el extremo **/services/social/ugcmanagement** activando el servicio UserUgcManagement. Para activar este servicio, instale el servlet de [muestra](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-ugc-management-servlet) disponible en [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-ugc-management-servlet). A continuación, toque el extremo en la instancia de publicación del sitio de comunidades con los parámetros adecuados mediante una solicitud http, similar a

**https://localhost:port/services/social/ugcmanagement?user=&lt;ID autorizable>&amp;operation=&lt;getUgc>**. Sin embargo, también puede crear una interfaz de usuario (interfaz de usuario) para administrar los perfiles de usuario y el contenido generado por el usuario en el sistema.

Estas API permiten realizar las siguientes funciones.

## Recuperar el UGC de un usuario {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String user, OutputStream outputStream) **ayuda a exportar todo el UGC de un usuario desde el sistema.

* **usuario**: ID autorizable de un usuario.
* **outputStream**: el resultado se devuelve como flujo de salida, que es un archivo zip que incluye el contenido generado por el usuario (como archivo json) y los archivos adjuntos (que incluyen imágenes o vídeos cargados por el usuario).

Por ejemplo, para exportar el UGC de un usuario llamado Weston McCall, que utiliza weston.mccall@dodgit.com como ID autorizada para iniciar sesión en el sitio de comunidades, puede enviar una solicitud http GET similar a la siguiente:

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## Eliminar el UGC de un usuario {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, usuario de cadena) **ayuda a eliminar todo el UGC de un usuario del sistema.

* **usuario**: ID autorizable del usuario.

Por ejemplo, para eliminar el UGC de un usuario con un ID autorizado weston.mccall@dodgit.com mediante una solicitud http-POST, utilice los parámetros siguientes:

* user= weston.mccall@dodgit.com
* operation= deleteUgc

### Eliminar UGC de Adobe Analytics {#delete-ugc-from-adobe-analytics}

Para eliminar datos de usuario de Adobe Analytics, siga el flujo de trabajo [de](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/an_gdpr_workflow.html)GDPR Analytics; ya que la API no elimina datos de usuario de Adobe Analytics.

Para las asignaciones de variables de Adobe Analytics utilizadas por AEM Communities, consulte la siguiente imagen:

![Asignación de variables de comunidades AEM para Adobe Analytics](assets/analytics-communities-mapping.png)

## Deshabilitar una cuenta de usuario {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, usuario de cadena) **ayuda a deshabilitar una cuenta de usuario.

* **usuario**: ID autorizable del usuario.

>[!NOTE]
>
>Al deshabilitar un usuario, se elimina todo el contenido generado por el usuario que tiene en el servidor.

Por ejemplo, para eliminar el perfil de un usuario con un ID autorizado weston.mccall@dodgit.com mediante una solicitud http-POST, utilice los parámetros siguientes:

* user= weston.mccall@dodgit.com
* operation= deleteUser

>[!NOTE]
>
>la API deleteUserAccount() solo deshabilita un perfil de usuario en el sistema y elimina el UGC. Sin embargo, para eliminar un perfil de usuario del sistema, vaya a **CRXDE Lite**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de), busque el nodo de usuario y elimínelo.

