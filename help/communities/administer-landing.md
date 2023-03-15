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

Esta sección es para aquellos que administran AEM Communities y supone que están familiarizados con las funciones de AEM Communities.

## Información general {#overview}

Para obtener información general y tutoriales de introducción, visite:

* [Información general de AEM Communities](overview.md)
* [Introducción a Comunidades de AEM](getting-started.md)
* [Introducción a AEM Communities para la habilitación](getting-started-enablement.md)

## Temas de administración y configuración {#administration-and-configuration-topics}

### Creación y administración de sitios de comunidades {#communities-site-creation-and-management}

* Communities [consolas](consoles.md)

   * [Sites](sites-console.md)

      * [Grupos (subcomunidades)](groups.md)
   * [Moderación](moderation.md)
   * [Administración de miembros y grupos](members.md)
   * [Recursos de habilitación](resources.md)
   * [Informes](reports.md)


* Communities [*herramientas*](tools.md):

   * [Plantillas de sitios](sites.md)
   * [Plantillas de grupos](tools-groups.md)
   * [Funciones de comunidad](functions.md)
   * [Configuración de almacenamiento](srp-config.md)
   * [Guía de componentes](components-guide.md)
   * [Insignias](badges.md)


### Contenido generado por el usuario {#user-generated-content}

Una característica principal de AEM Communities es la generación de contenido generado por el usuario (UGC) por parte de los visitantes del sitio (miembros) que han iniciado sesión. Para obtener más información sobre cómo trabajar con UGC, visite:

* [Almacén UGC común](working-with-srp.md): elección del SRP para el almacenamiento compartido de UGC
* [Moderar UGC](moderate-ugc.md): los miembros de confianza pueden moderar el CGU de forma masiva o en contexto
* [Etiquetado de UGC](tag-ugc.md): se pueden configurar funciones para permitir a los miembros etiquetar contenido
* [Traducción de UGC](translate-ugc.md): las funciones se pueden configurar para traducir todos los UGC o permitir que los miembros traduzcan las publicaciones seleccionadas
* [Configuración de Analytics](analytics.md): permite que Adobe Analytics informe sobre distintas métricas relativas a la actividad de los miembros

### Miembros de la comunidad {#community-members}

* [Administración de usuarios y grupos de usuarios](users.md): detalles de miembros de la comunidad y grupos de miembros, incluidos los miembros privilegiados.
* [Límites de contribución](limits.md): capacidad para restringir los mensajes de los nuevos miembros.
* [Servicio de túnel](deploy-communities.md#tunnel-service-on-author): permite acceder a los miembros y grupos de miembros del lado de publicación desde el entorno de creación.
* [Consolas de miembros y grupos](members.md): permite crear y administrar miembros y grupos de miembros del lado de publicación desde el entorno de creación.
* [Sincronización de usuarios](sync.md): para sincronizar miembros y grupos de miembros en varias instancias de publicación.
* [Inicio de sesión social con Facebook y Twitter](social-login.md): capacidad de los visitantes del sitio para convertirse en miembros de la comunidad mediante sus credenciales de Facebook o Twitter.
* [Puntuación y distintivos](implementing-scoring.md): capacidad para asignar insignias a fin de identificar las funciones de un miembro y para que los miembros obtengan insignias mediante su participación en la comunidad.
* [Notificaciones](notifications.md): capacidad para que los miembros reciban notificaciones de la actividad que siguen.
* [Suscripciones](subscriptions.md): capacidad de los miembros para interactuar con la comunidad mediante correo electrónico externo.
* [Mensajes](messaging.md): capacidad de los miembros para interactuar con la comunidad mediante mensajes internos.

### Funciones de habilitación {#enablement-features}

* [Configuración de habilitación](enablement.md): información necesaria para configurar correctamente las funciones de activación.
* [Configuración de Analytics](analytics.md): información necesaria para habilitar las funciones de Adobe Analytics para comunidades.
* [Recursos de habilitación de etiquetas](tag-resources.md): necesario para crear catálogos de habilitación.

### Implementación {#deployment}

La sección de implementación contiene información específica de AEM Communities.

La naturaleza del trabajo con contenido de la comunidad influye en la estructura de la implementación:

* [Topologías recomendadas para comunidades](topologies.md)

AEM Es importante instalar la versión más reciente de Communities en la plataforma de la:

* [Último paquete de funciones de Communities](deploy-communities.md#latestfeaturepack)

Consulte la página de implementación para obtener otra información específica de las comunidades, como para [Actualización](upgrade.md), [Dispatcher](dispatcher.md) y [Replicación](deploy-communities.md#replication-agents-on-author).

## Documentación de comunidades relacionadas {#related-communities-documentation}

* Visita [Implementación de comunidades](deploy-communities.md) para obtener más información sobre las implementaciones recomendadas.

* Visita [Desarrollo de comunidades](communities.md) para obtener más información sobre el marco de trabajo de componentes sociales (SCF) y personalizar los componentes y las funciones de las Comunidades.

* Visita [Componentes de comunidades de creación](author-communities.md) para aprender a crear y configurar componentes de Communities.
