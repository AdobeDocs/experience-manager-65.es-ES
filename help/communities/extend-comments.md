---
title: Componente Ampliar comentarios
description: Amplíe el componente Comentarios para modificar su apariencia o comportamiento para usos específicos
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%
---
# Componente Ampliar comentarios  {#extend-comments-component}

La intención de [ampliar](client-customize.md#extensions) un componente predeterminado es modificar el aspecto o el comportamiento de un componente para usos específicos.

La ruta al componente es única y hace referencia al componente predeterminado como un supertipo de recurso. Hay menos riesgo, ya que el ámbito es limitado en comparación con el ámbito global de una superposición de componentes.

>[!NOTE]
>
>No se admite la ampliación de un componente [overlay](client-customize.md#overlays).

## Ejemplo {#example}

Supongamos que el encabezado del componente Comentario debe mostrarse con una apariencia alternativa en un sitio de la instancia de AEM, mientras que aparece con la visualización predeterminada en otro sitio. En lugar de superponer el comentario predeterminado, que cambia el componente de comentario para todas las instancias, una mejor solución es garantizar que haya varios componentes de comentario disponibles para su uso en varios sitios.

Para implementar esta solución, cree un componente que amplíe (anule) el existente y modifique el script Handlebars. El área del sitio que utiliza los nuevos comentarios puede utilizar la ampliada, mientras que los sitios que utilizan la apariencia predeterminada no se ven afectados.

El componente de comentario es en realidad uno de los dos componentes que componen el sistema de comentarios. Por lo tanto, hay dos componentes que ampliar: *comments* y *comment*. El script que se va a editar se encuentra en el archivo `header.hbs` del componente *comment*, mientras que el componente principal *comments* (el sistema de comentarios) es lo que un autor agrega a la página.

Para ampliar los comentarios, debe:

1. [Creación de componentes](extend-create-components.md)
1. [Agregar comentario a página de muestra](extend-sample-page.md)
1. [Modificar el aspecto](extend-alter-appearance.md)
