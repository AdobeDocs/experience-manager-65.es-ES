---
title: Desarrollo de comunidades
seo-title: Developing Communities
description: Cree y personalice funciones de la comunidad como foros, grupos de usuarios y mucho más
seo-description: Create and customize community features such as forums, user groups, and more
uuid: 51dc54da-9090-4d36-adf9-72d5479062a5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: fbfe8097-3c3f-4a05-97ad-1ce526362a26
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 5%

---

# Desarrollo de comunidades  {#developing-communities}

## Información general {#overview}

AEM Communities simplifica la creación y personalización de funciones de la comunidad como foros, grupos de usuarios, blogs, preguntas y respuestas, calendarios, comentarios, revisiones, votaciones, clasificaciones y asignaciones. Estas funciones hacen que el contenido generado por el usuario (UGC) se introduzca en el entorno de publicación.

La base de una [sitio comunitario](overview.md#communitiessites) es el [marco de componentes sociales](scf.md) (SCF). La creación de un sitio de la comunidad comienza con la selección de un [plantilla del sitio de la comunidad](sites-console.md) que se compone de [funciones de comunidad](functions.md).

Para obtener información general y tutoriales de introducción, visite:

* [Información general de AEM Communities](overview.md)
* [Introducción a AEM Communities](getting-started.md)

>[!NOTE]
> 
>Se recomienda encarecidamente mantenerse al día con el [últimas versiones](deploy-communities.md#latest-releases).

## Implementaciones recomendadas {#recommended-deployments}

* [Almacenamiento de contenido de comunidad](working-with-srp.md): analiza las opciones de SRP disponibles para un almacén común de UGC
* [Topologías recomendadas para comunidades](topologies.md): analiza topologías basadas en casos de uso y opciones de SRP

## Marco del componente social {#social-component-framework}

* [Marco del componente social](scf.md): información general sobre el marco de trabajo y las API.
* [SCF Handlebars Helpers](handlebars-helpers.md): ayudantes predeterminados y cómo escribir ayudantes personalizados.
* [Personalización del lado del cliente](client-customize.md): personalizar el código que se ejecuta en el explorador.
* [Personalización del lado del servidor](server-customize.md): personalizar el código que se ejecuta en el servidor.
* [Proveedor de recursos de almacenamiento (SRP)](srp.md): información general sobre el almacenamiento de contenido de la comunidad.
* [Directrices de codificación](code-guide.md): directrices, sugerencias y trucos.
* [Guía de componentes de la comunidad](components-guide.md): herramienta de desarrollo interactiva.

## Aspectos básicos de componentes, funciones y funciones {#component-function-and-feature-essentials}

Los componentes, las funciones y las funciones de AEM Communities proporcionan los componentes básicos para [sitios de la comunidad](sites-console.md).

* [Aspectos básicos de componentes, funciones y funciones](essentials.md)
* [Componentes de Clientlibs para Communities](clientlibs.md)
* [Funciones de la comunidad](functions.md)
* [Plantillas de grupo de comunidad](tools-groups.md)
* [Plantillas de sitio de la comunidad](sites.md)

## Miembros de la comunidad {#community-members}

* [Administración de usuarios y grupos de usuarios](users.md)
* [Inicio de sesión social con Facebook y Twitter](social-login.md)

## Grupos de la comunidad {#community-groups}

[Grupos de comunidad](overview.md#communitygroups) es el concepto de permitir que los miembros de la comunidad formen subcomunidades dentro del sitio de la comunidad. La creación de un grupo de comunidad puede producirse en el entorno de publicación o creación.

* [Elementos esenciales del grupo de comunidad](essentials-groups.md)
* [Función Grupos](functions.md#groups-function)
* [Plantillas de grupo de comunidad](tools-groups.md)
* [Administración de usuarios y grupos de usuarios](users.md)
* [Grupos de la comunidad para autores](creating-groups.md)

## Administración de datos {#managing-data}

* [SRP y UGC Essentials](srp-and-ugc.md) - Métodos y ejemplos de la utilidad API de SRP
* [Tag Essentials](tag.md) - capacidad de los miembros de la comunidad de etiquetar recursos de habilitación catalogados o UGC

## Tutoriales {#tutorials}

* [Tutoriales de cliente](tutorials.md#client-side-customization)
* [Tutoriales del lado del servidor](tutorials.md#server-side-customization)
* [Instrucciones sobre procedimientos](tutorials.md#how-to-instructions)

## Solución de problemas {#troubleshooting}

* [Solución de problemas](troubleshooting.md)
* [Problemas conocidos](/help/release-notes/release-notes.md)

## Documentación de comunidades relacionadas {#related-communities-documentation}

* Visita [Implementación de comunidades](deploy-communities.md) para obtener más información sobre las implementaciones recomendadas y la configuración de dispatcher.

* Visita [Administración de sitios de Communities](administer-landing.md) para obtener más información sobre la creación de un sitio de la comunidad, la configuración de las plantillas de sitio de la comunidad, la moderación del contenido de la comunidad, la administración de miembros y la configuración de la mensajería.

* Visita [Componentes de comunidades de creación](author-communities.md) para aprender a crear y configurar componentes de Communities.
