---
title: Uso del gráfico social
description: Obtenga información sobre cómo agregar el componente Siguiente a una página que permite a los miembros de la comunidad que iniciaron sesión seguir actividades o ser seguidos.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---

# Uso del gráfico social {#using-social-graph}

## Introducción {#introduction}

La capacidad de un miembro de la comunidad para seguir [actividades](activities.md) y a seguir se establece a través de dos componentes: `Follow` y `Following`.

El `Follow` el componente debe estar asociado a otro recurso y esta asociación ya está establecida para los miembros y características de la comunidad.

El `Following` El componente simplemente enumera los miembros que están siguiendo al miembro actual o que están siendo seguidos por el miembro actual. Este gráfico social de las relaciones entre los miembros se incluye en el perfil de usuario establecido para una [sitio comunitario](overview.md#communitiessites).

## Añadir lo siguiente a una página {#adding-following-to-a-page}

Si se desea añadir un `Following` a una página en modo de autor, busque el componente `Communities / Following` y arrástrelo a su lugar en una página en la que deba aparecer el gráfico social.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](basics.md).

Si la variable [bibliotecas requeridas del lado del cliente](essentials-socialgraph.md#essentials-for-client-side) están incluidos, así es como se `Following` el componente aparece:

![siguiente](assets/following.png)

## Configurar lo siguiente {#configuring-following}

Actualmente, es necesario establecer la propiedad para determinar si el componente muestra la variable `follows` o la variable `following` relación.

## Información adicional {#additional-information}

Puede encontrar más información en la [Social Graph Essentials](essentials-socialgraph.md) para desarrolladores.
