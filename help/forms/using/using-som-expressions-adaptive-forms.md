---
title: Uso de expresiones SOM en formularios adaptables
seo-title: Uso de expresiones SOM en formularios adaptables
description: Obtenga información sobre cómo extraer expresiones SOM de un panel de un formulario adaptable.
seo-description: Obtenga información sobre cómo extraer expresiones SOM de un panel de un formulario adaptable.
uuid: c5d55aff-fb69-4a1c-96ea-fb3f9322cbb0
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 13f00bb2-561f-4d64-8829-292c663abeab
docset: aem65
translation-type: tm+mt
source-git-commit: e5c2385c29e2d20d453e2d1496f7d459d1c55876
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Uso de expresiones SOM en formularios adaptables{#using-som-expressions-in-adaptive-forms}

Los formularios adaptables se modelan como AEM página, que se representa como estructura de contenido JCR en AEM repositorio. El elemento clave de la estructura de contenido es el nodo guideContainer. Debajo de guideContainer, hay un rootPanel que puede contener paneles y campos anidados.

Puede utilizar un modelo de objetos de secuencias de comandos (SOM) para hacer referencia a valores, propiedades y métodos dentro de un modelo de objetos de documento (DOM) concreto. Un DOM organiza los objetos de memoria y las propiedades en una jerarquía de árbol. Una expresión SOM hace referencia a los elementos Campos/Dibujar y a los paneles.

La siguiente imagen muestra una estructura de nodos a la que se traduce un formulario adaptable cuando se agregan componentes a un formulario. Por ejemplo, puede añadir un panel al panel raíz y un botón de radio en el panel que se transforma en DOM durante la ejecución. La Expresión SOM para el campo de botón de radio en formato adaptable se especifica como `guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]`.

![Árbol DOM](assets/hierarchy.png)

Árbol DOM

Una expresión SOM para cualquier elemento de un formulario adaptable lleva el prefijo `guide[0].guide1[0]`. La posición de un componente en la jerarquía de estructura de nodos se utiliza para derivar su expresión SOM.

![Árbol DOM con dos botones de radio](assets/hierarchy_radio_button.png)

Árbol DOM con dos botones de radio

La expresión SOM cambia al cambiar la posición de los botones de radio en el formulario adaptable. En el modo de creación, puede realizar la vista de la expresión SOM de un campo o elemento dentro de AEM Forms mediante la opción de Expresión SOM de Vista. La opción aparece en el panel y al hacer clic con el botón derecho en el campo o elemento.

![Extracción de Expresiones SOM en un formulario adaptable](assets/som-expressions.png)

Extracción de Expresiones SOM en un formulario adaptable

En los paneles, puede acceder a la función desde la barra de herramientas del panel. La función facilita la creación de secuencias de comandos por parte de autores de formularios adaptables.

![Extracción de Expresiones SOM mediante la barra de herramientas del panel](assets/som-expression.png)

Extracción de Expresiones SOM mediante la barra de herramientas del panel

Algunas API enumeradas en [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) utilizan la expresión SOM de un elemento. Por ejemplo, para enfocar un campo concreto en un formulario adaptable, pase la expresión SOM correspondiente a la `getFocus`API en `guideBridge`.
