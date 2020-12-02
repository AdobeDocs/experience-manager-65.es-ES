---
title: Etiqueta decorativa
description: Cuando se procesa un componente de una página web, se puede generar un elemento HTML que ajuste el componente procesado en sí mismo. Para los desarrolladores, AEM ofertas claras y sencillas controlando las etiquetas de decoración que envuelven los componentes incluidos.
translation-type: tm+mt
source-git-commit: be1c0e21216b1014a36f88d13557f6e1d7a87c0a
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 1%

---


# Etiqueta decorativa{#decoration-tag}

Cuando se procesa un componente de una página web, se puede generar un elemento HTML que ajuste el componente procesado en sí mismo. Esto sirve principalmente para dos fines:

* Un componente solo se puede editar cuando se envuelve con un elemento HTML.
* El elemento de ajuste se utiliza para aplicar clases HTML que proporcionan:

   * información del diseño
   * información de estilo

Para los desarrolladores, AEM ofertas claras y sencillas controlando las etiquetas de decoración que envuelven los componentes incluidos. La combinación de dos factores define si se procesa la etiqueta decorativa y cómo se procesa, en lo que esta página se sumergirá:

* El propio componente puede configurar su etiqueta de decoración con un conjunto de propiedades.
* Las secuencias de comandos que incluyen componentes (HTL, JSP, dispatcher, etc.) pueden definir los aspectos de la etiqueta decorativa con parámetros de inclusión.

## Recomendaciones {#recommendations}

A continuación se ofrecen algunas recomendaciones generales sobre cuándo incluir el elemento envolvente que debería ayudar a evitar problemas inesperados:

* La presencia del elemento envolvente no debe diferir entre los códigos WCMM (modo de edición o previsualización), las instancias (autor o publicación) o el entorno (ensayo o producción), de modo que el CSS y los JavaScript de la página funcionen de forma idéntica en todos los casos.
* El elemento wrapper debe agregarse a todos los componentes que sean editables, de modo que el editor de páginas pueda inicializarlos y actualizarlos correctamente.
* En el caso de componentes no editables, el elemento envolvente puede evitarse si no cumple ninguna función determinada, de modo que el marcado resultante no esté inflado innecesariamente.

## Controles de componentes {#component-controls}

Se pueden aplicar las siguientes propiedades y nodos a los componentes para controlar el comportamiento de su etiqueta decorativa:

* **`cq:noDecoration {boolean}`:** Esta propiedad se puede agregar a un componente y un valor verdadero fuerza AEM no generar ningún elemento envolvente sobre el componente.

* **`cq:htmlTag`node:** Este nodo se puede agregar bajo un componente y puede tener las siguientes propiedades:

   * **`cq:tagName {String}`:** Esto se puede usar para especificar una etiqueta HTML personalizada que se utilizará para ajustar los componentes en lugar del elemento DIV predeterminado.
   * **`class {String}`:** Se puede utilizar para especificar los nombres de clase css que se añadirán al contenedor.
   * Otros nombres de propiedad se agregarán como atributos HTML con el mismo valor de cadena que se proporciona.

## Controles de secuencias de comandos {#script-controls}

Sin embargo, el comportamiento del contenedor difiere según si se utiliza [HTL](/help/sites-developing/decoration-tag.md#htl) o [JSP](/help/sites-developing/decoration-tag.md#jsp) para incluir el elemento.

### HTL {#htl}

En general, el comportamiento del envolvente en HTL puede resumirse de la siguiente manera:

* No se procesa ningún DIV de envoltorio de forma predeterminada (solo al hacer `data-sly-resource="foo"`).
* Todos los modos wcm (deshabilitado, previsualización, edición tanto en la creación como en la publicación) se representan de forma idéntica.

El comportamiento del envoltorio también se puede controlar completamente.

* El script HTL tiene control total sobre el comportamiento resultante de la etiqueta wrapper.
* Las propiedades de componente (como `cq:noDecoration` y `cq:tagName`) también pueden definir la etiqueta de envoltorio.

Es posible controlar por completo el comportamiento de las etiquetas wrapper desde scripts HTL y su lógica asociada.

Para obtener más información sobre el desarrollo en HTL, consulte la [documentación de HTL](https://docs.adobe.com/content/help/es-ES/experience-manager-htl/using/overview.html).

#### Árbol de decisiones {#decision-tree}

Este árbol de decisión resume la lógica que determina el comportamiento de las etiquetas de envoltorio.

![chlimage_1-75](assets/chlimage_1-75a.png)

#### Casos de uso {#use-cases}

Los tres casos de uso siguientes proporcionan ejemplos de cómo se manejan las etiquetas de envoltorio y también ilustran lo sencillo que es controlar el comportamiento deseado de las etiquetas de envoltorio.

En todos los ejemplos que se muestran a continuación se asume la siguiente estructura de contenido y componentes:

```
/content/test/
  @resourceType = "test/components/one"
  child/
    @resourceType = "test/components/two"
```

```
/apps/test/components/
  one/
    one.html
  two/
    two.html
    cq:htmlTag/
      @cq:tagName = "article"
      @class = "component-two"
```

#### Caso de uso 1: Incluir un componente para la reutilización del código {#use-case-include-a-component-for-code-reuse}

El caso de uso más típico es cuando un componente incluye otro componente por motivos de reutilización del código. En ese caso, no se desea que el componente incluido sea editable con su propia barra de herramientas y cuadro de diálogo, por lo que no se necesita ningún contenedor y se omitirá el `cq:htmlTag` del componente. Se puede considerar el comportamiento predeterminado.

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

Resultado en `/content/test.html`:

**`Hello World!`**

Un ejemplo sería un componente que incluye un componente de imagen principal para mostrar una imagen, normalmente en ese caso mediante el uso de un recurso sintético, que consiste en incluir un componente secundario virtual pasando a un recurso de datos de modo inteligente un objeto Map que represente todas las propiedades que el componente tendría.

#### Caso de uso 2: Incluir un componente editable {#use-case-include-an-editable-component}

Otro caso de uso común es cuando los componentes de contenedor incluyen componentes secundarios editables, como un Contenedor de diseño. En este caso, cada niño incluido necesita imperativamente un envoltorio para que funcione el editor (a menos que esté explícitamente deshabilitado con la propiedad `cq:noDecoration`).

Dado que el componente incluido es en este caso un componente independiente, necesita un elemento envolvente para que funcione el editor y para definir su diseño y estilo que aplicar. Para activar este comportamiento, está la opción `decoration=true`.

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

Resultado en `/content/test.html`:

**`<article class="component-two">Hello World!</article>`**

#### Caso de uso 3: Comportamiento personalizado {#use-case-custom-behavior}

Puede haber muchos casos complejos, que pueden lograrse fácilmente con la posibilidad de que HTL proporcione explícitamente:

* **`decorationTagName='ELEMENT_NAME'`** Para definir el nombre del elemento del contenedor.
* **`cssClassName='CLASS_NAME'`** Definición de los nombres de clase CSS que se van a definir en él.

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

Resultado `/content/test.html`:

**`<aside class="child">Hello World!</aside>`**

## JSP {#jsp}

Al incluir un componente mediante `cq:includ`e o `sling:include`, el comportamiento predeterminado en AEM es utilizar una DIV para envolver el elemento. Sin embargo, este ajuste se puede personalizar de dos formas:

* Indique explícitamente AEM no ajustar el componente mediante `cq:noDecoration`.
* Utilice una etiqueta HTML personalizada para ajustar el componente mediante `cq:htmlTag`/ `cq:tagName` o `decorationTagName`.

### Árbol de decisiones {#decision-tree-1}

El siguiente árbol de decisiones ilustra cómo `cq:noDecoration`, `cq:htmlTag`, `cq:tagName` y `decorationTagName` afectan el comportamiento del contenedor.

![climage_1-3](assets/chlimage_1-3a.jpeg)

