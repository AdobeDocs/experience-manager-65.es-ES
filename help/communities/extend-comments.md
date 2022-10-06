---
title: Componente Ampliar comentarios
seo-title: Extend Comments Component
description: Ampliar el componente Comentarios para modificar su aspecto o comportamiento para usos específicos
seo-description: Extend the Comments component to alter its appearance or behavior for specific uses
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# Componente Ampliar comentarios  {#extend-comments-component}

La intención de [ampliar](client-customize.md#extensions) un componente predeterminado es modificar el aspecto o el comportamiento de un componente para usos específicos.

La ruta al componente es única y hace referencia al componente predeterminado como un tipo de superrecurso. Hay menos riesgo, ya que el ámbito está limitado en comparación con el ámbito global de una superposición de componentes.

>[!NOTE]
>
>Ampliación de un [superpuesto](client-customize.md#overlays) no es compatible.

## Ejemplo {#example}

Supongamos que el encabezado del componente de comentario debe mostrarse con un aspecto alternativo en un sitio de la instancia de AEM, mientras aparece con la visualización predeterminada en otro sitio. En lugar de superponer el comentario predeterminado, que cambia el componente de comentario para todas las instancias, una mejor solución es asegurarse de que haya varios componentes de comentario disponibles para usar en varios sitios.

Para implementar esta solución, cree un nuevo componente que amplíe (reemplace) el existente y modifique la secuencia de comandos Handlebars. El área del sitio que utiliza los nuevos comentarios puede utilizar la extendida, mientras que los sitios que utilizan el aspecto predeterminado no se verán afectados.

El componente de comentarios es en realidad uno de los dos componentes que componen el sistema de comentarios. Por lo tanto, hay dos componentes que se pueden ampliar: *comentarios* y *comment*. La secuencia de comandos que se va a editar se encuentra en la sección *comment* del componente `header.hbs` mientras que el principal *comentarios* (el sistema de comentarios) es lo que un autor agrega a la página.

Para ampliar los comentarios, deberá:

1. [Crear los componentes](extend-create-components.md)
1. [Agregar comentario a una página de muestra](extend-sample-page.md)
1. [Modificar el aspecto](extend-alter-appearance.md)
