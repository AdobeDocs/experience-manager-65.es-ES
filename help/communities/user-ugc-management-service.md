---
title: Servicio de administración de usuarios y UGC en AEM Communities
description: Utilice las API para eliminar de forma masiva y exportar de forma masiva el contenido generado por el usuario, así como desactivar la cuenta de usuario.
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
docset: aem65
role: Admin
exl-id: 526ef0fa-3f20-4de4-8bc5-f435c60df0d0
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---

# Servicio de administración de usuarios y UGC en AEM Communities {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>El RGPD se utiliza como ejemplo en las secciones siguientes, pero los detalles cubiertos son aplicables a todas las regulaciones de protección de datos y privacidad; como el RGPD, la CCPA, etc.

AEM Communities expone las API listas para usarse para administrar perfiles de usuario y contenido generado por el usuario (UGC). Una vez habilitado, el servicio **UserUgcManagement** permite a los usuarios privilegiados (administradores y moderadores de la comunidad) deshabilitar perfiles de usuario y eliminar de forma masiva o exportar de forma masiva UGC para usuarios específicos. Estas API también permiten a los responsables y procesadores de los datos de los clientes cumplir con el Reglamento General de Protección de Datos (RGPD) de la Unión Europea y otros mandatos de privacidad inspirados en el RGPD.

Para obtener más información, consulte la página [RGPD en el Centro de privacidad de Adobe](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Si configuró [Adobe Analytics en el sitio AEM Communities](/help/communities/analytics.md), los datos de usuario capturados se enviarán al servidor de Adobe Analytics. Adobe Analytics proporciona API que le permiten acceder, exportar y eliminar datos de usuario y cumplir con el RGPD. Para obtener más información, consulte [Enviar solicitudes de acceso y eliminación](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-submit-access-delete.html?lang=es).

Para utilizar estas API, debe habilitar el extremo `/services/social/ugcmanagement` activando el servicio UserUgcManagement. Para activar este servicio, instale el [servlet de ejemplo](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) disponible en [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet). A continuación, visite el punto final de la instancia de publicación del sitio de comunidades con los parámetros adecuados mediante una solicitud http, similar a:

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. Sin embargo, también puede crear una interfaz de usuario (interfaz de usuario) para administrar los perfiles de usuario y el contenido generado por el usuario en el sistema.

Estas API permiten realizar las siguientes funciones.

## Recuperar el UGC de un usuario {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String user, OutputStream outputStream)** ayuda a exportar todos los UGC de un usuario desde el sistema.

* **usuario**: ID con autorización de un usuario.
* **outputStream**: el resultado se devuelve como flujo de salida, que es un archivo zip con contenido generado por el usuario (como archivo json) y archivos adjuntos (que incluyen imágenes o vídeos cargados por el usuario).

Por ejemplo, para exportar el UGC de un usuario llamado Weston McCall, que utiliza weston.mccall@dodgit.com como ID autorizado para iniciar sesión en el sitio de comunidades, puede enviar una solicitud de GET http similar a la siguiente:

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## Eliminar el UGC de un usuario {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, usuario de cadena)** ayuda a eliminar del sistema todos los UGC para un usuario.

* **usuario**: ID con autorización del usuario.

Por ejemplo, para eliminar el UGC de un usuario con un ID autorizable weston.mccall@dodgit.com a través de una solicitud http-POST, utilice los siguientes parámetros:

* usuario = `weston.mccall@dodgit.com`
* operación = `deleteUgc`

### Eliminar UGC de Adobe Analytics {#delete-ugc-from-adobe-analytics}

Para eliminar datos de usuario de Adobe Analytics, siga el [flujo de trabajo de análisis del RGPD](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html?lang=es); ya que la API no elimina datos de usuario de Adobe Analytics.

Para las asignaciones de variables de Adobe Analytics utilizadas por AEM Communities, consulte la siguiente imagen:

AEM ![Asignación de variables de comunidades de destino para Adobe Analytics](assets/analytics-communities-mapping.png)

## Deshabilitar una cuenta de usuario {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, usuario de cadena)** ayuda a deshabilitar una cuenta de usuario.

* **usuario**: ID con autorización del usuario.

>[!NOTE]
>
>Al deshabilitar un usuario, se elimina todo el contenido generado por el usuario en el servidor.

Por ejemplo, para eliminar el perfil de un usuario que tiene el identificador autorizado `weston.mccall@dodgit.com` mediante una solicitud http-POST, utilice los parámetros siguientes:

* usuario = `weston.mccall@dodgit.com`
* operación = `deleteUser`

>[!NOTE]
>
>La API deleteUserAccount() solo desactiva un perfil de usuario en el sistema y elimina el UGC. Sin embargo, para eliminar un perfil de usuario del sistema, vaya a **CRXDE Lite**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de), busque el nodo de usuario y elimínelo.
