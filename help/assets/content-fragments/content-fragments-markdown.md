---
title: Markdown
seo-title: Markdown
description: Cuando se está creando, el editor de fragmentos de contenido utiliza la sintaxis de restricción para permitir escribir contenido fácilmente.
seo-description: Cuando se está creando, el editor de fragmentos de contenido utiliza la sintaxis de restricción para permitir escribir contenido fácilmente.
uuid: afcbf82f-3a75-4491-9172-706188db65bb
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: b193f28c-46c2-4eab-bbb8-578530f80ba5
docset: aem65
translation-type: tm+mt
source-git-commit: 08bf8f42898446f2e5cca1fde55ceb84710a1e30
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 4%

---


# Markdown{#markdown}

Cuando se [está creando](content-fragments-variations.md#authoring-your-content), el editor de fragmentos de contenido utiliza la sintaxis *markdown* para permitirle escribir contenido fácilmente:

![editor de marcas](/help/assets/content-fragments/assets/cfm-6420-08.png)

Puede definir:

* [Notación de encabezado](/help/assets/content-fragments/content-fragments-markdown.md#heading-notation)
* [Párrafos y saltos de línea](/help/assets/content-fragments/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [Vínculos](/help/assets/content-fragments/content-fragments-markdown.md#links)
* [Imágenes](/help/assets/content-fragments/content-fragments-markdown.md#images)
* [Bloquear cotizaciones](/help/assets/content-fragments/content-fragments-markdown.md#block-quotes)
* [Listas](/help/assets/content-fragments/content-fragments-markdown.md#lists)
* [Énfasis](/help/assets/content-fragments/content-fragments-markdown.md#emphasis)
* [Bloques de código](/help/assets/content-fragments/content-fragments-markdown.md#code-blocks)
* [Escapadas de barra invertida](/help/assets/content-fragments/content-fragments-markdown.md#backslash-escapes)

## Notación de encabezado {#heading-notation}

Para crear un encabezado, coloque una etiqueta (#) delante del encabezado. Se utiliza una etiqueta (#) para H1, dos etiquetas hash (##) para H2, etc. Se pueden usar hasta 6 etiquetas hash. Por ejemplo:

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

De forma opcional, puede crear una H1 subrayando el texto en signos iguales y crear una H2 subrayando el texto en signos menos. Por ejemplo:

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## Párrafos y saltos de línea {#paragraphs-and-line-breaks}

Un párrafo es simplemente una o varias líneas consecutivas de texto, separadas por una o varias líneas en blanco. Una línea en blanco es una línea que sólo contiene espacios o fichas. Los párrafos normales no se deben aplicar sangría con espacios ni fichas.

Un salto de línea se crea finalizando una línea con dos o más espacios que un retorno.

## Vínculos {#links}

Puede crear vínculos en línea y de referencia.

En ambos estilos, el texto del vínculo se delimita entre corchetes `[]`.

Estos son ejemplos de vínculos en línea:

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

Un vínculo de referencia tiene la sintaxis siguiente:

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## Imágenes {#images}

La sintaxis de las imágenes es similar a la de los vínculos. Puede crear imágenes en línea y referenciadas.

Por ejemplo, una imagen en línea tiene la siguiente sintaxis:

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

La sintaxis incluye:

* Signo de exclamación: !;
* seguido de un conjunto de corchetes que contiene el texto del atributo alt de la imagen;
* seguido de un conjunto de paréntesis, que contiene la dirección URL o la ruta de la imagen, y un atributo de título opcional entre comillas simples o dobles.

Una imagen de estilo de referencia tiene la siguiente sintaxis:

    `![Alt text][id]`

Donde &quot;id&quot; es el nombre de una referencia de imagen definida. Las referencias de imagen se definen con sintaxis idéntica a las referencias de vínculo:

    `[id]: url/to/image "Optional title attribute"`

## Comillas de bloque {#block-quotes}

Puede citar texto agregando el símbolo > delante del texto. Por ejemplo:

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

Puede tener comillas de bloque anidadas. Por ejemplo:

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## Listas {#lists}

Puede crear listas ordenadas y sin ordenar.

Para crear una lista sin orden, utilice &amp;ast; antes de los elementos de la lista. Por ejemplo:

    `* item in list`

    `* item in list`

    `* item in list`

Para crear una lista ordenada, agregue los números, seguidos de un punto, antes de cada elemento de la lista. Por ejemplo:

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## Énfasis {#emphasis}

Puede agregar estilo en cursiva o negrita al texto.

Para agregar cursiva de la siguiente manera:

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

Puede aplicar negrita al texto de la siguiente manera:

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

Para indicar un fragmento de código, envuélvalo con comillas (`). A diferencia de un bloque de código con formato previo, un espacio de código indica código dentro de un párrafo normal.

Por ejemplo:

    ``Use the `printf()` function.``

## Bloques de código {#code-blocks}

Los bloques de código generalmente se utilizan para ilustrar el código fuente. Puede crear bloques de código sangrando el código mediante una ficha o un mínimo de 4 espacios. Por ejemplo:

    `This is a normal paragraph.`

        `This is a code block.`

## Escapadas de barra invertida {#backslash-escapes}

Puede utilizar los escapes de barra invertida para generar caracteres literales con un significado especial en la sintaxis de formato. Por ejemplo, si desea rodear una palabra con asteriscos literales (en lugar de una etiqueta HTML &lt;em>), puede utilizar barras invertidas antes de los asteriscos, como esta:

    `\\*literal asterisks\\*`

Los escapes de barra invertida están disponibles para los siguientes caracteres:

    ` \ backslash`

    `` ` backtick``

    ` * asterisk`

    ` _ underscore`

    ` {} curly braces`

    ` [] square brackets`

    ` () parentheses`

    ` # hash mark`

    ` + plus sign`

    ` - minus sign (hyphen)`

    ` . dot`

