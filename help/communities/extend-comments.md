---
title: Ampliar componente de comentarios
seo-title: Ampliar componente de comentarios
description: Amplíe el componente Comentarios para modificar su apariencia o comportamiento para usos específicos
seo-description: Amplíe el componente Comentarios para modificar su apariencia o comportamiento para usos específicos
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Ampliar componente de comentarios {#extend-comments-component}

La intención de [ampliar](client-customize.md#extensions) un componente predeterminado es alterar el aspecto o el comportamiento de un componente para usos específicos.

La ruta al componente es única y hace referencia al componente predeterminado como un tipo de recurso superior. Hay menos riesgo, ya que el ámbito es limitado en comparación con el ámbito global de una superposición de componentes.

>[!NOTE]
>
>No se admite la extensión de un componente [superpuesto](client-customize.md#overlays).

## Ejemplo {#example}

Supongamos que el encabezado del componente de comentario debe mostrarse con un aspecto alternativo en un sitio de la instancia de AEM, mientras aparece con la visualización predeterminada en otro sitio. En lugar de superponer el comentario predeterminado, que cambia el componente de comentarios para todas las instancias, una mejor solución es asegurarse de que hay varios componentes de comentarios disponibles para su uso en varios sitios.

Para implementar esta solución, cree un nuevo componente que extienda (anule) el existente y modifique la secuencia de comandos Handlebars. El área del sitio que utiliza los nuevos comentarios puede utilizar la extendida, mientras que los sitios que utilizan la apariencia predeterminada no se verán afectados.

El componente de comentarios es en realidad uno de los dos componentes que componen el sistema de comentarios. Por lo tanto, hay dos componentes que ampliar: *comentarios* y *comentario*. La secuencia de comandos que se va a editar se encuentra en el archivo *comment* del componente `header.hbs`, mientras que el componente principal *comments* (el sistema de comentarios) es lo que un autor realmente agrega a la página.

Para ampliar los comentarios deberá:

1. [Crear los componentes](extend-create-components.md)
1. [Añadir comentario a página de muestra](extend-sample-page.md)
1. [Modificar el aspecto](extend-alter-appearance.md)

