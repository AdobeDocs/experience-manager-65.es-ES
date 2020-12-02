---
title: Limitaciones del editor
seo-title: Limitaciones del editor
description: El editor de la interfaz de usuario táctil utiliza superposiciones para interactuar con contenido limitado en un iframe. Esta interacción crea algunas limitaciones en el uso del editor y también para los desarrolladores.
seo-description: El editor de la interfaz de usuario táctil utiliza superposiciones para interactuar con contenido limitado en un iframe. Esta interacción crea algunas limitaciones en el uso del editor y también para los desarrolladores.
uuid: ff524530-3f3a-4c5b-9f94-4aa9aeb9d461
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: d748decb-a614-4c9e-a502-d6176b720f1a
translation-type: tm+mt
source-git-commit: 844d42ed50da153077423190684aa85265bce12f
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Limitaciones del editor{#editor-limitations}

El editor de la interfaz de usuario táctil utiliza superposiciones para interactuar con contenido limitado en un iframe. Esta interacción crea algunas limitaciones en el uso del editor y también para los desarrolladores. Esta página resume estas limitaciones y proporciona soluciones o soluciones alternativas siempre que sea posible.

## Limitaciones funcionales {#functional-limitations}

Un autor puede encontrar las siguientes limitaciones funcionales al utilizar el editor para crear páginas.

### Vínculos no activos {#links-not-active}

Cuando [edita una página](/help/sites-authoring/editing-content.md), los vínculos no están activos.

* [Cambie a  **** ](/help/sites-authoring/editing-content.md#preview-mode) Vista previa para navegar con los vínculos del contenido.

### Páginas de estructura {#structure-pages}

No se puede asignar un nombre a las páginas `structure`. Las páginas con el nombre `structure` no se podrán editar en el editor de páginas.

## Limitaciones de CSS {#css-limitations}

Un desarrollador puede encontrar las siguientes limitaciones con las interacciones del editor con CSS.

### Elementos con posición absoluta {#absolutely-positioned-elements}

Los elementos con posición absoluta pueden causar problemas en la posición de su superposición.

* Si esto sucede, asegúrese de que las dimensiones del elemento con posición absoluta son correctas porque el editor creará una superposición con las mismas dimensiones.

### unidades de vh {#vh-units}

`vh` no se admiten las unidades porque la altura del iframe debe ajustarse automáticamente por AEM.

### Imágenes de fondo fijas {#fixed-background-images}

Es posible que las imágenes de fondo fijas no se muestren como fijas al desplazarse debido a que se incrustan en un iframe.

* Si selecciona **Página de Vista como Publicada** en las acciones de la barra de encabezado, la página se muestra correctamente.

### Altura del 100% {#height}

El elemento body de una página no admite una altura del 100 %.

* Es posible una solución alternativa para implementar un cuerpo a pantalla completa &quot;estirando&quot; el elemento body de la siguiente manera:

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### Contraer margen {#margin-collapsing}

Se pueden ver problemas de colapso de margen si el primer elemento secundario del elemento body tiene un margen.

* La solución es agregar una corrección clara en el nivel del elemento de cuerpo, como la siguiente:

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```

