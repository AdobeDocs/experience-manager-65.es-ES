---
title: Uso de gráficos sociales
seo-title: Uso de gráficos sociales
description: Adición de un componente Siguiente a una página
seo-description: Adición de un componente Siguiente a una página
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Uso de gráficos sociales {#using-social-graph}

## Introducción {#introduction}

La capacidad de un miembro de la comunidad para seguir y seguir [las actividades](activities.md) se establece mediante dos componentes: `Follow`y `Following`.

El `Follow`componente debe asociarse con otro recurso, y esta asociación ya está establecida para miembros y características de la comunidad.

El `Following`componente simplemente enumera los miembros que están siguiendo al miembro actual o que están siendo seguidos por el miembro actual. Este gráfico social de las relaciones entre miembros se incluye en el perfil de usuario establecido para un sitio [de](overview.md#communitiessites)comunidad.

## Adición de lo siguiente a una página {#adding-following-to-a-page}

Si desea agregar un `Following`componente a una página en modo de autor, ubique el componente `Communities / Following` y arrástrelo a su lugar en una página en la que debería aparecer el gráfico social.

Para obtener la información necesaria, visite [Communities Components Basics](basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se incluyen las bibliotecas [del lado del cliente](essentials-socialgraph.md#essentials-for-client-side) necesarias, así es como aparecerá el `Following` componente:

![chlimage_1-447](assets/chlimage_1-447.png)

## Configuración de lo siguiente {#configuring-following}

Actualmente, es necesario establecer la propiedad para determinar si el componente muestra la `follows`relación o la `following`relación.

## Información adicional {#additional-information}

Puede encontrar más información en la página [Social Graph Essentials](essentials-socialgraph.md) para desarrolladores.
