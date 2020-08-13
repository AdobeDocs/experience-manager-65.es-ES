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


# Uso de gráficos sociales {#using-social-graph}

## Introducción {#introduction}

La capacidad de un miembro de la comunidad para seguir [actividades](activities.md) y seguir de cerca se establece mediante dos componentes: `Follow` y `Following`.

El `Follow` componente debe asociarse con otro recurso, y esta asociación ya está establecida para miembros y características de la comunidad.

El `Following` componente simplemente lista a los miembros que siguen al miembro actual o a los que sigue el miembro actual. Este gráfico social de las relaciones entre los miembros se incluye en el perfil de usuario creado para un sitio [de](overview.md#communitiessites)comunidad.

## Añadir lo siguiente en una página {#adding-following-to-a-page}

Si desea agregar un `Following` componente a una página en modo de autor, ubique el componente `Communities / Following` y arrástrelo a su lugar en una página en la que debería aparecer el gráfico social.

Para obtener la información necesaria, visite [Communities Components Basics](basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se incluyen las bibliotecas [del lado del cliente](essentials-socialgraph.md#essentials-for-client-side) necesarias, así es como aparecerá el `Following` componente:

![following](assets/following.png)

## Configuración de lo siguiente {#configuring-following}

Actualmente, es necesario establecer la propiedad para determinar si el componente muestra la `follows` relación o la `following` relación.

## Información adicional {#additional-information}

Puede encontrar más información en la página [Social Graph Essentials](essentials-socialgraph.md) para desarrolladores.
