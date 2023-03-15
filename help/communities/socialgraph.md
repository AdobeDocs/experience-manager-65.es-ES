---
title: Uso del gráfico social
seo-title: Using Social Graph
description: Añadir el siguiente componente a una página
seo-description: Adding a Following component to a page
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---

# Uso del gráfico social {#using-social-graph}

## Introducción {#introduction}

La capacidad de un miembro de la comunidad para seguir [actividades](activities.md) así como a seguirse se establece a través de dos componentes: `Follow` y `Following`.

El `Follow` el componente debe estar asociado a otro recurso y esta asociación ya está establecida para los miembros y características de la comunidad.

El `Following` El componente simplemente enumera los miembros que están siguiendo al miembro actual o que están siendo seguidos por el miembro actual. Este gráfico social de las relaciones entre los miembros se incluye en el perfil de usuario establecido para una [sitio comunitario](overview.md#communitiessites).

## Añadir lo siguiente a una página {#adding-following-to-a-page}

Si se desea añadir un `Following` a una página en modo de autor, busque el componente `Communities / Following` y arrástrelo a su lugar en una página en la que deba aparecer el gráfico social.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](basics.md).

Si la variable [bibliotecas requeridas del lado del cliente](essentials-socialgraph.md#essentials-for-client-side) están incluidos, así es como se `Following` el componente aparecerá:

![siguiente](assets/following.png)

## Configurar lo siguiente {#configuring-following}

Actualmente, es necesario establecer la propiedad para determinar si el componente muestra la variable `follows` o la variable `following` relación.

## Información adicional {#additional-information}

Puede encontrar más información en la [Social Graph Essentials](essentials-socialgraph.md) para desarrolladores.
