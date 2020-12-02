---
title: Uso de gráficos sociales
seo-title: Uso de gráficos sociales
description: Añadir un componente Siguiente en una página
seo-description: Añadir un componente Siguiente en una página
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
translation-type: tm+mt
source-git-commit: 1429a099288f038510cb0a194fb55632297ef371
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---


# Uso de Social Graph {#using-social-graph}

## Introducción {#introduction}

La capacidad de un miembro de la comunidad para seguir [actividades](activities.md) y seguir se establece mediante dos componentes: `Follow` y `Following`.

El componente `Follow` debe asociarse con otro recurso y esta asociación ya está establecida para miembros de la comunidad y funciones.

El componente `Following` simplemente lista los miembros que siguen al miembro actual o que siguen el miembro actual. Este gráfico social de las relaciones entre miembros se incluye en el perfil de usuario establecido para un [sitio de comunidad](overview.md#communitiessites).

## Añadir lo siguiente en una página {#adding-following-to-a-page}

Si desea agregar un componente `Following` a una página en modo de autor, ubique el componente `Communities / Following` y arrástrelo a su lugar en una página donde debería aparecer el gráfico social.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de comunidades](basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](essentials-socialgraph.md#essentials-for-client-side), así es como aparecerá el componente `Following`:

![following](assets/following.png)

## Configurando lo siguiente {#configuring-following}

Actualmente, es necesario establecer la propiedad para determinar si el componente muestra la relación `follows` o la relación `following`.

## Información adicional {#additional-information}

Puede encontrar más información en la página [Social Graph Essentials](essentials-socialgraph.md) para desarrolladores.
