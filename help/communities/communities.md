---
title: Desarrollo de comunidades
description: Cree y personalice funciones de la comunidad como foros, grupos de usuarios y mucho más.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 5%

---

# Desarrollo de comunidades  {#developing-communities}

## Información general {#overview}

Las comunidades de Adobe Experience Manager AEM () simplifican la creación y personalización de funciones de la comunidad, como foros, grupos de usuarios, blogs, preguntas y respuestas, calendarios, comentarios, revisiones, votaciones, clasificaciones y asignaciones. Estas funciones hacen que el contenido generado por el usuario (UGC) se introduzca en el entorno de publicación.

La base de un [sitio de comunidad](overview.md#communitiessites) es el [marco de trabajo de componente social](scf.md) (SCF). La creación de un sitio de la comunidad comienza con la selección de una [plantilla del sitio de la comunidad](sites-console.md) compuesta por [funciones de la comunidad](functions.md).

Para obtener información general y tutoriales de introducción, visite:

* [Información general de AEM Communities](overview.md)
* [Introducción a AEM Communities](getting-started.md)

>[!NOTE]
> 
>Se recomienda encarecidamente mantenerse actualizado con las [últimas versiones](deploy-communities.md#latest-releases).

## Implementaciones recomendadas {#recommended-deployments}

* [Almacenamiento de contenido de la comunidad](working-with-srp.md): analiza las opciones disponibles del proveedor de recursos sociales (SRP) para un almacén común de UGC
* [Topologías recomendadas para comunidades](topologies.md): analiza las topologías en función del caso de uso y la opción de SRP

## Marco del componente social {#social-component-framework}

* [Marco de componente social](scf.md): información general sobre el marco de trabajo y las API.
* [SCF Handlebars Helpers](handlebars-helpers.md): ayudantes predeterminados y cómo escribir ayudantes personalizados.
* [Personalización del lado del cliente](client-customize.md): personalizando el código que se ejecuta en el explorador.
* [Personalización del lado del servidor](server-customize.md): personalizando el código que se ejecuta en el servidor.
* [Proveedor de recursos de almacenamiento (SRP)](srp.md): información general sobre el almacenamiento de contenido de la comunidad.
* [Directrices de codificación](code-guide.md): directrices, sugerencias y trucos.
* [Guía de componentes de la comunidad](components-guide.md): herramienta de desarrollo interactiva.

## Aspectos básicos de componentes, funciones y funciones {#component-function-and-feature-essentials}

Los componentes, las funciones y las características de AEM Communities constituyen los componentes básicos de [sitios de la comunidad](sites-console.md).

* [Aspectos básicos de componentes, funciones y funciones](essentials.md)
* [Componentes de Clientlibs para Communities](clientlibs.md)
* [Funciones de la comunidad](functions.md)
* [Plantillas de grupo de comunidad](tools-groups.md)
* [Plantillas de sitio de la comunidad](sites.md)

## Miembros de la comunidad {#community-members}

* [Administración de usuarios y grupos de usuarios](users.md)
* [Social Inicie sesión con Facebook y Twitter](social-login.md)

## Grupos de la comunidad {#community-groups}

[Los grupos de la comunidad](overview.md#communitygroups) son el concepto de permitir que los miembros de la comunidad formen subcomunidades dentro del sitio de la comunidad. La creación de un grupo de comunidad puede producirse en el entorno de publicación o creación.

* [Elementos esenciales del grupo de comunidad](essentials-groups.md)
* [Función Grupos](functions.md#groups-function)
* [Plantillas de grupo de comunidad](tools-groups.md)
* [Administración de usuarios y grupos de usuarios](users.md)
* [Grupos de la comunidad para autores](creating-groups.md)

## Administración de datos {#managing-data}

* [SRP y UGC Essentials](srp-and-ugc.md): métodos y ejemplos de la utilidad API de SRP
* [Elementos esenciales de la etiqueta](tag.md): capacidad de los miembros de la comunidad para etiquetar recursos de habilitación catalogados o UGC

## Tutoriales {#tutorials}

* [Tutoriales de cliente](tutorials.md#client-side-customization)
* [Tutoriales del lado del servidor](tutorials.md#server-side-customization)
* [Instrucciones sobre procedimientos](tutorials.md#how-to-instructions)

## Resolución de problemas {#troubleshooting}

* [Resolución de problemas](troubleshooting.md)
* [Problemas conocidos](/help/release-notes/release-notes.md)

## Documentación de comunidades relacionadas {#related-communities-documentation}

* Visite [Implementación de comunidades](deploy-communities.md) para obtener más información sobre las implementaciones recomendadas y la configuración de Dispatcher.

* Visite [Administración de sitios de comunidades](administer-landing.md) para obtener información sobre cómo crear un sitio de comunidad, configurar plantillas de sitios de comunidad, moderar el contenido de la comunidad, administrar miembros y configurar mensajes.

* Visite [Creación de componentes de comunidades](author-communities.md) para aprender a crear y configurar componentes de comunidades.
