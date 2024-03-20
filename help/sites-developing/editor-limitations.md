---
title: Limitaciones del editor
description: El editor de la IU táctil utiliza superposiciones para interactuar con el contenido limitado en un iframe. Esta interacción crea algunas limitaciones en el uso del editor y también para los desarrolladores.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
exl-id: fd64f5dc-dfff-466b-8cdd-3c24ea1a15c8
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 6%

---

# Limitaciones del editor{#editor-limitations}

El editor de la IU táctil utiliza superposiciones para interactuar con el contenido limitado en un iframe. Esta interacción crea algunas limitaciones en el uso del editor y también para los desarrolladores. Esta página resume estas limitaciones y proporciona soluciones o soluciones alternativas siempre que sea posible.

## Limitaciones funcionales {#functional-limitations}

Un autor puede encontrar las siguientes limitaciones funcionales al utilizar el editor para crear páginas.

### Vínculos no activos {#links-not-active}

Cuándo [edición de una página](/help/sites-authoring/editing-content.md), los vínculos no están activos.

* [Cambiar a **Previsualizar** modo](/help/sites-authoring/editing-content.md#preview-mode) para navegar mediante los vínculos del contenido.

### Páginas de estructura {#structure-pages}

Las páginas no pueden tener nombre `structure`. Páginas con nombre `structure` no se pueden editar en el editor de páginas.

## Limitaciones de CSS {#css-limitations}

Un desarrollador puede encontrar las siguientes limitaciones con las interacciones del editor con CSS.

### Elementos en posición absoluta {#absolutely-positioned-elements}

Los elementos con una posición absoluta pueden causar problemas en la posición de su superposición.

* Si esto sucede, asegúrese de que las dimensiones del elemento con una posición absoluta son correctas porque el editor crea una superposición con las mismas dimensiones.

### Unidades vh {#vh-units}

`vh` las unidades no son compatibles porque Adobe Experience Manager AEM (iFrame) debe ajustar automáticamente la altura de los iframes (iFrame) (o la altura de los iframes).

### Imágenes de fondo fijas {#fixed-background-images}

Es posible que las imágenes de fondo fijas no se muestren como fijas al desplazarse, ya que están incrustadas en un iframe.

* Seleccionar **Ver página publicada** en las acciones de la barra de encabezado muestra la página correctamente.

### Altura al 100% {#height}

El 100 % de altura no es compatible con el elemento de cuerpo de una página.

* Una solución alternativa es implementar un cuerpo de pantalla completa &quot;estirando&quot; el elemento de cuerpo de la siguiente manera:

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

Los problemas de contracción del margen se pueden ver si el primer elemento secundario del elemento body tiene un margen.

* La solución consiste en añadir una corrección clara en el nivel de elemento de cuerpo como se indica a continuación:

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
