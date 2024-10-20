---
title: Aspectos básicos de componentes, funciones y funciones
description: Funcionamiento de los sitios, plantillas y grupos de la comunidad
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 15%

---

# Aspectos básicos de componentes, funciones y funciones  {#component-function-and-feature-essentials}

Las características de las comunidades Adobe Experience Manager AEM () requieren que los visitantes del sitio se conviertan en miembros e inicien sesión en el [sitio de la comunidad](overview.md#communitiessites) antes de poder publicar contenido. Por lo tanto, las [plantillas de sitio de la comunidad](sites.md), desde las cuales se [crea un sitio de la comunidad](sites-console.md), están diseñadas para incluir una característica de inicio de sesión y perfiles de usuario, mensajería, búsqueda, moderación y traducción.

Un sitio de comunidad admite miembros que crean grupos de comunidad cuando la función [grupos de comunidad](functions.md#groups-function) se incluye en la plantilla de sitio de comunidad seleccionada.

A continuación se muestran vínculos a información esencial para los componentes, las funciones y las características de las comunidades.

## Componentes básicos {#base-components}

* [Comentarios](essentials-comments.md)
* [Repasos](reviews-basics.md)
* [Tally](tally.md)

   * [Me está gustando](essentials-liking.md)
   * [Clasificación](rating-basics.md)
   * [Votación](essentials-voting.md)
   * *Sondeo (ya no disponible)*

## Componentes con funciones {#components-with-functions}

* [Flujos de actividad](essentials-activities.md)
* [Blog](blog-developer-basics.md) (`Journal`)

* [Calendario](calendar-basics-for-developers.md)
* [Contenido destacado](essentials-featured.md)
* [Biblioteca de archivos](essentials-file-library.md)
* [Foro](essentials-forum.md)
* [Grupos](essentials-groups.md)
* [Ideación](ideation.md)
* [Tabla de clasificación](leaderboard.md)
* [Preguntas y respuestas](qna-essentials.md) `(QnA)`

## Características {#features}

* [Bibliotecas de cliente](clientlibs.md)
* [Sitios de la comunidad](sites-for-developers.md)
* [Eventos OSGi de componente](events.md)
* [Descarga de componentes](sideloading.md)
* [Mensajes](essentials-messaging.md)
* [Editor de texto enriquecido](rte.md)
* [Puntuación y distintivos](configure-scoring.md)
* [Búsqueda](search-implementation.md)
* [Gráfico social](essentials-socialgraph.md)
* [Proveedor de recursos de almacenamiento](srp-and-ugc.md) `(SRP)`

* [Etiquetado](tag.md)

## Javadocs {#javadocs}

AEM Los [javadocs en línea](../../help/sites-developing/reference-materials.md) reflejan las API disponibles en la versión 6.3 de la versión en línea de la versión 6.3.
Las API de Communities están en `com.adobe.cq.social.*` paquetes.

Para cada [paquete de funciones](deploy-communities.md#latestfeaturepack), hay disponible un jar de javadoc. Para obtener más información, visite [Usar Maven para las comunidades](maven.md#javadocs).

## Información adicional {#additional-information}

* [Marco de componentes sociales (SCF)](scf.md)

   * [Personalizaciones del lado del cliente](client-customize.md)
   * [Personalizaciones del lado del servidor](server-customize.md)
   * [Resumen del proveedor de recursos de almacenamiento](srp.md)

* [Directrices de codificación](code-guide.md)
* [Tutoriales](tutorials.md)
* [Resolución de problemas](troubleshooting.md)
