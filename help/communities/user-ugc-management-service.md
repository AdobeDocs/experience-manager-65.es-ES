---
title: Servicio de administración de usuarios y UGC en AEM Communities
seo-title: User and UGC Management Service in AEM Communities
description: Utilice las API para eliminar de forma masiva y exportar de forma masiva contenido generado por el usuario, y para deshabilitar la cuenta de usuario.
seo-description: Use APIs to bulk delete and bulk export user generated content, and disable user account.
uuid: 91180659-617d-4f6c-9a07-e680770d0d8f
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
discoiquuid: d305821d-1371-4e4a-8b28-8eee8fafa43b
docset: aem65
role: Admin
exl-id: 526ef0fa-3f20-4de4-8bc5-f435c60df0d0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# Servicio de administración de usuarios y UGC en AEM Communities {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>El RGPD se utiliza como ejemplo en las secciones siguientes, pero los detalles cubiertos son aplicables a todas las normas de protección de datos y privacidad; como el RGPD, la CCPA, etc.

AEM Communities expone las API listas para usar para administrar perfiles de usuario y administrar de forma masiva el contenido generado por el usuario (UGC). Una vez activada, la variable **UserUgcManagement** permite a los usuarios privilegiados (administradores de la comunidad y moderadores) desactivar perfiles de usuario, y eliminar o exportar UGC de forma masiva para usuarios específicos. Estas API también permiten que los controladores y procesadores de datos de clientes cumplan con las normas generales de protección de datos (RGPD) de la Unión Europea y otros mandatos de privacidad inspirados en el RGPD.

Para obtener más información, consulte [Página del RGPD en el Centro de privacidad de Adobe](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Si ha configurado [Adobe Analytics en AEM Communities](/help/communities/analytics.md) sitio, los datos de usuario capturados se envían al servidor de Adobe Analytics. Adobe Analytics proporciona API que le permiten acceder, exportar y eliminar datos de usuario y cumplir con el RGPD. Para obtener más información, consulte [Envío de solicitudes de acceso y eliminación](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html).

Para que estas API se utilicen, debe habilitar la variable `/services/social/ugcmanagement` al activar el servicio UserUgcManagement. Para activar este servicio, instale la variable [servlet de ejemplo](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) disponible en [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet). A continuación, pulse el punto final en la instancia de publicación del sitio de comunidades con los parámetros apropiados mediante una solicitud http, similar a:

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. Sin embargo, también puede crear una interfaz de usuario (interfaz de usuario) para administrar los perfiles de usuario y el contenido generado por el usuario en el sistema.

Estas API permiten realizar las siguientes funciones.

## Recuperar el UGC de un usuario {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, usuario de cadena, OutputStream outputStream)** ayuda a exportar todo el UGC de un usuario desde el sistema.

* **usuario**: ID autorizado de un usuario.
* **outputStream**: El resultado se devuelve como flujo de salida, que es un archivo zip que incluye el contenido generado por el usuario (como archivo json) y archivos adjuntos (que incluyen imágenes o vídeos cargados por el usuario).

Por ejemplo, para exportar el UGC de un usuario llamado Weston McCall, que utiliza weston.mccall@dodgit.com como ID autorizado para iniciar sesión en el sitio de Communities, puede enviar una solicitud de GET http similar a la siguiente:

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## Eliminar el UGC de un usuario {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, usuario de cadena)** ayuda a eliminar todo el UGC de un usuario del sistema.

* **usuario**: ID autorizado del usuario.

Por ejemplo, para eliminar el UGC de un usuario que tenga un ID autorizado weston.mccall@dodgit.com a través de una solicitud http-POST, utilice los parámetros siguientes:

* user = `weston.mccall@dodgit.com`
* operation = `deleteUgc`

### Eliminar UGC de Adobe Analytics {#delete-ugc-from-adobe-analytics}

Para eliminar datos de usuario de Adobe Analytics, siga la [Flujo de trabajo de RGPD Analytics](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html); ya que la API no elimina los datos de usuario de Adobe Analytics.

Para las asignaciones de variables de Adobe Analytics que utiliza AEM Communities, consulte la siguiente imagen:

![Asignación de variables de comunidades AEM para Adobe Analytics](assets/analytics-communities-mapping.png)

## Deshabilitar una cuenta de usuario {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, usuario de cadena)** ayuda a deshabilitar una cuenta de usuario.

* **usuario**: ID autorizado del usuario.

>[!NOTE]
>
>Al deshabilitar un usuario, se elimina todo el contenido generado por el usuario que tenga en el servidor.

Por ejemplo, para eliminar el perfil de un usuario que tenga un ID autorizado `weston.mccall@dodgit.com` a través de la solicitud http-POST, utilice los siguientes parámetros:

* user = `weston.mccall@dodgit.com`
* operation = `deleteUser`

>[!NOTE]
>
>deleteUserAccount() API solo deshabilita un perfil de usuario en el sistema y elimina el UGC. Sin embargo, para eliminar un perfil de usuario del sistema, vaya a **CRXDE Lite**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de), busque el nodo de usuario y elimínelo.
