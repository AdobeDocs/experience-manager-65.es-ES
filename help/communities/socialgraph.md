---
title: Uso del gráfico social
seo-title: Using Social Graph
description: Adición de un componente siguiente a una página
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

La capacidad de un miembro de la comunidad para seguir [actividades](activities.md) además de ser seguido, se establece mediante dos componentes: `Follow` y `Following`.

La variable `Follow` debe asociarse con otro recurso, y esta asociación ya está establecida para miembros de la comunidad y características.

La variable `Following` simplemente enumera los miembros que siguen al miembro actual o a los que sigue el miembro actual. Este gráfico social de las relaciones entre miembros se incluye en el perfil de usuario establecido para un [sitio de la comunidad](overview.md#communitiessites).

## Adición de lo siguiente a una página {#adding-following-to-a-page}

Si desea agregar un `Following` a una página en modo de autor, busque el componente `Communities / Following` y arrástrela a su lugar en una página donde debería aparecer el gráfico social.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de Communities](basics.md).

Cuando la variable [bibliotecas requeridas del lado del cliente](essentials-socialgraph.md#essentials-for-client-side) se incluyen, así es como se muestra la variable `Following` aparecerá el componente:

![following](assets/following.png)

## Configuración de lo siguiente {#configuring-following}

Actualmente, es necesario establecer la propiedad para determinar si el componente muestra la variable `follows` o `following` relación.

## Información adicional {#additional-information}

Puede encontrar más información en la [Social Graph Essentials](essentials-socialgraph.md) para desarrolladores.
