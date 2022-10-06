---
title: Sitios de comunidades
seo-title: Communities Sites
description: Información general sobre la documentación de AEM Communities
seo-description: Overview of the AEM Communities documentation
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 5%

---

# Sitios de comunidades {#communities-sites}

Esta sección es para aquellos que administran AEM Communities y que asumen la familiaridad con las funciones de AEM Communities.

## Información general {#overview}

Para obtener información general y tutoriales de introducción, visite:

* [Información general de AEM Communities](overview.md)
* [Introducción a Comunidades de AEM](getting-started.md)
* [Introducción a AEM Communities para la activación](getting-started-enablement.md)

## Temas de administración y configuración {#administration-and-configuration-topics}

### Creación y administración de sitios de comunidades {#communities-site-creation-and-management}

* Comunidades [consolas](consoles.md)

   * [Sites](sites-console.md)

      * [Grupos (subcomunidades)](groups.md)
   * [Moderación](moderation.md)
   * [Administración de miembros y grupos](members.md)
   * [Recursos de habilitación](resources.md)
   * [Informes](reports.md)


* Comunidades [*herramientas*](tools.md):

   * [Plantillas de sitios](sites.md)
   * [Plantillas de grupos](tools-groups.md)
   * [Funciones de comunidad](functions.md)
   * [Configuración de almacenamiento](srp-config.md)
   * [Guía de componentes](components-guide.md)
   * [Insignias](badges.md)


### Contenido generado por el usuario {#user-generated-content}

Una de las principales características de AEM Communities es la generación de contenido generado por el usuario (UGC, por sus siglas en inglés) por los visitantes del sitio que han iniciado sesión (miembros). Para obtener más información sobre cómo trabajar con UGC, visite:

* [Almacenamiento UGC común](working-with-srp.md): elección de SRP para el almacenamiento compartido de UGC
* [Moderación de UGC](moderate-ugc.md): los miembros de confianza pueden moderar UGC de forma masiva o en contexto
* [Etiquetado UGC](tag-ugc.md): se pueden configurar para permitir que los miembros etiqueten contenido
* [Traducción de UGC](translate-ugc.md): se pueden configurar para traducir todo el UGC o permitir que los miembros traduzcan los anuncios seleccionados
* [Configuración de Analytics](analytics.md): permitir a Adobe Analytics informar sobre diversas métricas relativas a la actividad de los miembros

### Miembros de la comunidad {#community-members}

* [Administración de usuarios y grupos de usuarios](users.md): detalles de los miembros de la comunidad y de los grupos miembros, incluidos los miembros privilegiados.
* [Límites de contribución](limits.md): capacidad para restringir la publicación por nuevos miembros.
* [Servicio de túnel](deploy-communities.md#tunnel-service-on-author): permite acceder a los miembros y grupos de miembros del lado de publicación desde el entorno de creación.
* [Consolas Miembros y Grupos](members.md): permite crear y administrar miembros y grupos de miembros del lado de publicación desde el entorno de creación.
* [Sincronización de usuarios](sync.md): para sincronizar miembros y grupos de miembros en varias instancias de publicación.
* [Inicio de sesión en Social con Facebook y Twitter](social-login.md): capacidad para que los visitantes del sitio se conviertan en miembros de la comunidad mediante sus credenciales de Facebook o Twitter.
* [Puntuación y distintivos](implementing-scoring.md): capacidad para asignar distintivos para identificar las funciones de un miembro y para que los miembros obtengan distintivos mediante su participación en la comunidad.
* [Notificaciones](notifications.md): capacidad para que los miembros sean notificados de la actividad que siguen.
* [Suscripciones](subscriptions.md): capacidad para que los miembros interactúen con la comunidad mediante correo electrónico externo.
* [Mensajería](messaging.md): capacidad para que los miembros interactúen con la comunidad mediante mensajes internos.

### Funciones de habilitación {#enablement-features}

* [Configuración de la habilitación](enablement.md): información necesaria para configurar correctamente las funciones de habilitación.
* [Configuración de Analytics](analytics.md): información necesaria para activar las funciones de Adobe Analytics para Communities.
* [Etiquetado de recursos de habilitación](tag-resources.md): necesario para crear catálogos de habilitación.

### Implementación {#deployment}

La sección de implementación contiene información específica de AEM Communities.

La naturaleza del trabajo con contenido de la comunidad influye en la estructura de la implementación:

* [Topologías recomendadas para comunidades](topologies.md)

Es importante instalar la versión más reciente de Communities en la plataforma AEM:

* [Paquete de funciones de las comunidades más recientes](deploy-communities.md#latestfeaturepack)

Consulte la página de implementación para obtener información específica de otras comunidades, como por ejemplo para [Actualización](upgrade.md), [Dispatcher](dispatcher.md) y [Replicación](deploy-communities.md#replication-agents-on-author).

## Documentación de Communities relacionadas {#related-communities-documentation}

* Visita [Implementación de comunidades](deploy-communities.md) para obtener más información sobre las implementaciones recomendadas.

* Visita [Desarrollo de comunidades](communities.md) para obtener información sobre el marco de componentes sociales (SCF) y la personalización de componentes y funciones de Communities.

* Visita [Creación de componentes de Communities](author-communities.md) para aprender a crear con y configurar componentes de Communities.
