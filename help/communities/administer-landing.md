---
title: Sitios de comunidades
seo-title: Sitios de comunidades
description: Información general sobre la documentación de AEM Communities
seo-description: Información general sobre la documentación de AEM Communities
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Communities Sites {#communities-sites}

Esta sección está dirigida a los que administran comunidades AEM y se familiarizan con las funciones de comunidades AEM.

## Información general {#overview}

Para obtener información general y tutoriales de introducción, visite:

* [Información general sobre comunidades AEM](overview.md)
* [Introducción a Comunidades de AEM](getting-started.md)
* [Introducción a Comunidades de AEM para la habilitación](getting-started-enablement.md)

## Temas de administración y configuración {#administration-and-configuration-topics}

### Creación y administración de sitios de comunidades {#communities-site-creation-and-management}

* Consolas [de comunidades](consoles.md)

   * [Sitios](sites-console.md)

      * [Grupos (subcomunidades)](groups.md)
   * [Moderación](moderation.md)
   * [Administración de miembros y grupos](members.md)
   * [Recursos de habilitación](resources.md)
   * [Informes](reports.md)


* Herramientas [*de comunidades *](tools.md):

   * [Plantillas de sitios](sites.md)
   * [Plantillas de grupos](tools-groups.md)
   * [Funciones de comunidad](functions.md)
   * [Configuración de almacenamiento](srp-config.md)
   * [Guía de componentes](components-guide.md)
   * [Insignias](badges.md)


### Contenido generado por el usuario {#user-generated-content}

Una de las principales características de las comunidades AEM es la generación de contenido generado por el usuario (UGC) por los visitantes del sitio que inician sesión (miembros). Para obtener más información sobre cómo trabajar con UGC, visite:

* [Tienda](working-with-srp.md)UGC común: elección de SRP para almacenamiento compartido de UGC
* [UGC](moderate-ugc.md)de moderación: los miembros de confianza pueden moderar UGC de forma masiva o en contexto
* [Etiquetado de UGC](tag-ugc.md): las funciones se pueden configurar para permitir a los miembros etiquetar contenido
* [Traduciendo UGC](translate-ugc.md): las funciones se pueden configurar para traducir todo el contenido generado por usuarios o permitir que los miembros traduzcan los anuncios seleccionados
* [Configuración](analytics.md)de Analytics: activación de Adobe Analytics para informar sobre distintas métricas en relación con la actividad de los miembros

### Miembros de la comunidad {#community-members}

* [Administración de usuarios y grupos](users.md)de usuarios: detalles de los miembros de la comunidad y de los grupos miembros, incluidos los miembros privilegiados
* [Límites](limits.md)de contribución: capacidad para restringir la publicación por nuevos miembros
* [Servicio](deploy-communities.md#tunnel-service-on-author)de túnel: permite el acceso a los miembros y grupos de miembros del lado de publicación desde el entorno de creación
* [Consolas](members.md)Miembros y Grupos: permite crear y administrar miembros y grupos de miembros del lado de publicación desde el entorno de creación
* [Sincronización](sync.md)del usuario: para sincronizar miembros y grupos de miembros en varias instancias de publicación
* [Inicio de sesión social con Facebook y Twitter](social-login.md): capacidad para que los visitantes del sitio se conviertan en miembros de la comunidad mediante sus credenciales de Facebook o Twitter
* [Puntuación y distintivos](implementing-scoring.md): capacidad de asignar distintivos para identificar las funciones de un miembro y de los miembros para obtener distintivos mediante su participación en la comunidad
* [Notificaciones](notifications.md): capacidad de los miembros para recibir notificaciones de la actividad que siguen
* [Suscripciones](subscriptions.md): capacidad de los miembros para interactuar con la comunidad mediante correo electrónico externo
* [Mensajería](messaging.md): capacidad de los miembros para interactuar con la comunidad mediante mensajes internos

### Funciones de habilitación {#enablement-features}

* [Configuración de la habilitación](enablement.md): información necesaria para configurar correctamente las funciones de habilitación
* [Configuración](analytics.md)de Analytics: información necesaria para activar las funciones de Adobe Analytics para Comunidades
* [Etiquetado de recursos](tag-resources.md)de habilitación: necesarios para crear catálogos de habilitación

### Implementación {#deployment}

La sección de implementación contiene información específica de Comunidades de AEM.

La naturaleza del trabajo con contenido de la comunidad influye en la estructura de la implementación:

* [Topologías recomendadas para las comunidades](topologies.md)

Es importante instalar la versión más reciente de Communities en la plataforma AEM:

* [Paquete de funciones de las últimas comunidades](deploy-communities.md#latestfeaturepack)

Consulte la página de implementación para obtener información específica de otras comunidades, como [Actualización](upgrade.md), [Distribuidor](dispatcher.md) y [Replicación](deploy-communities.md#replication-agents-on-author).

## Documentación de comunidades relacionadas {#related-communities-documentation}

* Visite [Implementar comunidades](deploy-communities.md) para conocer las implementaciones recomendadas.

* Visite [Desarrollar comunidades](communities.md) para conocer el marco de componentes sociales (SCF) y personalizar componentes y características de Comunidades.

* Visite [Creación de componentes](author-communities.md) de comunidades para obtener información sobre cómo crear y configurar componentes de comunidades.
