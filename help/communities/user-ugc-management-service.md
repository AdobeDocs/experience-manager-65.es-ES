---
title: Servicio de administración de usuarios y usuarios por usuario en AEM Communities
seo-title: Servicio de administración de usuarios y usuarios por usuario en AEM Communities
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
source-git-commit: 18f401babef4cb2aad47e6e4cbb0500b0f8365e2
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---


# Servicio de administración de usuarios y usuarios por usuario en AEM Communities {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>El RGPD se utiliza como ejemplo en las secciones que figuran a continuación, pero los detalles abarcados son aplicables a todas las normas de protección de datos y privacidad; como el RGPD, la CCPA, etc.


AEM Communities expone las API integradas para administrar los perfiles de los usuarios y el contenido generado por los usuarios (UGC) de forma masiva. Una vez activado, el servicio **UserUgcManagement** permite a los usuarios privilegiados (administradores de la comunidad y moderadores) desactivar los perfiles de usuario y eliminar o exportar de forma masiva UGC para usuarios específicos. Estas API también permiten que los controladores y los procesadores de datos de los clientes cumplan con las Normas Generales de Protección de Datos (RGPD) de la Unión Europea y otros mandatos de privacidad inspirados en el RGPD.

Para obtener más información, consulte la página del [RGPD en el Centro](https://www.adobe.com/privacy/general-data-protection-regulation.html)de Privacidad del Adobe.

>[!NOTE]
>
>Si ha configurado [Adobe Analytics en el sitio de AEM Communities](/help/communities/analytics.md) , los datos de usuario capturados se envían al servidor de Adobe Analytics. Adobe Analytics proporciona API que le permiten acceder, exportar y eliminar datos de usuario y cumplir con el RGPD. Para obtener más información, consulte [Enviar solicitudes](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html)de acceso y eliminación.


Para poner estas API en uso, debe habilitar el extremo activando el servicio UserUgcManagement `/services/social/ugcmanagement` . Para activar este servicio, instale el servlet de [muestra](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) disponible en [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet). A continuación, toque el extremo en la instancia de publicación del sitio de comunidades con los parámetros adecuados mediante una solicitud http, similar a:

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. Sin embargo, también puede crear una interfaz de usuario (interfaz de usuario) para administrar los perfiles de usuario y el contenido generado por el usuario en el sistema.

Estas API permiten realizar las siguientes funciones.

## Recuperar el UGC de un usuario {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String user, OutputStream outputStream)** ayuda a exportar desde el sistema todo el UGC de un usuario.

* **usuario**: ID de un usuario con autorización.
* **outputStream**: El resultado se devuelve como flujo de salida, que es un archivo zip que incluye el contenido generado por el usuario (como archivo json) y los archivos adjuntos (que incluyen imágenes o vídeos cargados por el usuario).

Por ejemplo, para exportar el UGC de un usuario llamado Weston McCall, que utiliza weston.mccall@dodgit.com como ID autorizada para iniciar sesión en el sitio de comunidades, puede enviar una solicitud de GET http similar a la siguiente:

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## Eliminar el UGC de un usuario {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, usuario de cadena)** ayuda a eliminar todo el UGC de un usuario del sistema.

* **usuario**: ID de usuario con autorización.

Por ejemplo, para eliminar el UGC de un usuario con un ID autorizado weston.mccall@dodgit.com mediante una solicitud de http-POST, utilice los parámetros siguientes:

* user = `weston.mccall@dodgit.com`
* operation = `deleteUgc`

### Eliminar UGC de Adobe Analytics {#delete-ugc-from-adobe-analytics}

Para eliminar datos de usuario del Adobe Analytics, siga el flujo de trabajo [de análisis de](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)GDPR; ya que la API no elimina datos de usuario de Adobe Analytics.

Para las asignaciones de variables de Adobe Analytics utilizadas por AEM Communities, consulte la siguiente imagen:

![Asignación de variables de comunidades AEM para Adobe Analytics](assets/analytics-communities-mapping.png)

## Deshabilitar una cuenta de usuario {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, usuario de cadena)** ayuda a deshabilitar una cuenta de usuario.

* **usuario**: ID de usuario con autorización.

>[!NOTE]
>
>Al deshabilitar un usuario, se elimina todo el contenido generado por el usuario que tiene en el servidor.


Por ejemplo, para eliminar el perfil de un usuario con un ID autorizado `weston.mccall@dodgit.com` mediante una solicitud http-POST, utilice los parámetros siguientes:

* user = `weston.mccall@dodgit.com`
* operation = `deleteUser`

>[!NOTE]
>
>la API deleteUserAccount() solo deshabilita un perfil de usuario en el sistema y elimina el UGC. Sin embargo, para eliminar un perfil de usuario del sistema, vaya al **CRXDE Lite**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de), busque el nodo de usuario y elimínelo.


