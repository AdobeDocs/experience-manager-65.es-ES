---
title: Sitios de comunidades
description: Obtenga información acerca de los aspectos básicos de las comunidades de Adobe Experience Manager AEM () para administradores que ya están familiarizados con sus funciones básicas.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 4%

---

# Sitios de comunidades {#communities-sites}

Esta sección es para aquellos que administran AEM Communities y supone que están familiarizados con las funciones de AEM Communities.

## Información general {#overview}

Para obtener información general y tutoriales de introducción, visite:

* [Información general de AEM Communities](overview.md)
* [Introducción a AEM Communities](getting-started.md)

## Temas de administración y configuración {#administration-and-configuration-topics}

### Creación y administración de sitios de comunidades {#communities-site-creation-and-management}

* Comunidades [consolas](consoles.md)

   * [Sites](sites-console.md)

      * [Grupos (subcomunidades)](groups.md)

   * [Moderación](moderation.md)
   * [Administración de miembros y grupos](members.md)
   * [Informes](reports.md)

* Comunidades [*herramientas*](tools.md):

   * [Plantillas de sitios](sites.md)
   * [Plantillas de grupo](tools-groups.md)
   * [Funciones de la comunidad](functions.md)
   * [Configuración de almacenamiento](srp-config.md)
   * [Guía de componentes](components-guide.md)
   * [Insignias](badges.md)


### Contenido generado por el usuario {#user-generated-content}

Una característica principal de AEM Communities es la generación de contenido generado por el usuario (UGC) por parte de los visitantes del sitio (miembros) que han iniciado sesión. Para obtener más información sobre cómo trabajar con UGC, visite:

* [Almacén UGC común](working-with-srp.md): opción de SRP para almacenamiento compartido de UGC
* [Moderar UGC](moderate-ugc.md): los miembros de confianza pueden moderar UGC de forma masiva o en contexto
* [Etiquetado de UGC](tag-ugc.md): las características se pueden configurar para permitir a los miembros etiquetar contenido
* [Traducción de UGC](translate-ugc.md): las características pueden configurarse para traducir todos los UGC o permitir que los miembros traduzcan las publicaciones seleccionadas
* [Configuración de Analytics](analytics.md): permitir que Adobe Analytics informe sobre distintas métricas relativas a la actividad de los miembros

### Miembros de la comunidad {#community-members}

* [Administración de usuarios y grupos de usuarios](users.md): detalles de miembros de la comunidad y grupos de miembros, incluidos los miembros privilegiados.
* [Límites de contribución](limits.md): capacidad para restringir la publicación de nuevos miembros.
* [Servicio de túnel](deploy-communities.md#tunnel-service-on-author): permite el acceso a los miembros y grupos de miembros del lado de publicación desde el entorno de creación.
* [Consolas de miembros y grupos](members.md): permite crear y administrar miembros y grupos de miembros del lado de publicación desde el entorno de creación.
* [Sincronización de usuarios](sync.md): para sincronizar miembros y grupos de miembros en varias instancias de publicación.
* [Iniciar sesión en medios sociales con Facebook y el Twitter](social-login.md): permite que los visitantes del sitio se conviertan en miembros de la comunidad con sus credenciales de Facebook o Twitter.
* [Puntuación e insignias](implementing-scoring.md): capacidad para que se asignen insignias a fin de identificar las funciones de un miembro y para que los miembros obtengan insignias mediante su participación en la comunidad.
* [Notificaciones](notifications.md): capacidad para que se notifique a los miembros la actividad que siguen.
* [Suscripciones](subscriptions.md): capacidad para que los miembros interactúen con la comunidad mediante correo electrónico externo.
* [Mensajería](messaging.md): capacidad para que los miembros interactúen con la comunidad mediante mensajes internos.

### Implementación {#deployment}

La sección de implementación contiene información específica de AEM Communities.

La naturaleza del trabajo con contenido de la comunidad influye en la estructura de la implementación:

* [Topologías recomendadas para comunidades](topologies.md)

AEM Es importante instalar la versión más reciente de Communities en la plataforma de la:

* [Último paquete de funciones de Communities](deploy-communities.md#latestfeaturepack)

Consulte la página de implementación para obtener información específica de otras comunidades, como [Actualización](upgrade.md), [Dispatcher](dispatcher.md) y [Replicación](deploy-communities.md#replication-agents-on-author).

## Documentación de comunidades relacionadas {#related-communities-documentation}

* Visite [Implementación de comunidades](deploy-communities.md), donde podrá obtener información sobre las implementaciones recomendadas.

* Visite [Desarrollo de comunidades](communities.md), donde podrá obtener información acerca del marco de componentes sociales (SCF) y la personalización de componentes y características de las comunidades.

* Visite [Creación de componentes de comunidades](author-communities.md), donde aprenderá a crear y configurar componentes de comunidades.
