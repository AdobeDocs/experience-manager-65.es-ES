---
title: Uso del gráfico social
description: Obtenga información sobre cómo agregar el componente Siguiente a una página que permite a los miembros de la comunidad que iniciaron sesión seguir actividades o ser seguidos.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 1%
---
# Uso del gráfico social {#using-social-graph}

## Introducción {#introduction}

La capacidad de un miembro de la comunidad para seguir [actividades](activities.md) y ser seguido se establece mediante dos componentes: `Follow` y `Following`.

El componente `Follow` debe estar asociado con otro recurso y esta asociación ya está establecida para los miembros y características de la comunidad.

El componente `Following` simplemente enumera los miembros que están siguiendo al miembro actual o que están siendo seguidos por el miembro actual. Este gráfico social de las relaciones entre los miembros se incluye en el perfil de usuario establecido para un [sitio de la comunidad](overview.md#communitiessites).

## Añadir lo siguiente a una página {#adding-following-to-a-page}

Si desea agregar un componente `Following` a una página en modo de autor, busque el componente `Communities / Following` y arrástrelo a su lugar en una página en la que debería aparecer el gráfico social.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](essentials-socialgraph.md#essentials-for-client-side), así es como aparece el componente `Following`:

![siguiente](assets/following.png)

## Configurar lo siguiente {#configuring-following}

Actualmente, es necesario establecer la propiedad para determinar si el componente muestra la relación `follows` o la relación `following`.

## Información adicional {#additional-information}

Encontrará más información en la página de [Social Graph Essentials](essentials-socialgraph.md) para desarrolladores.
