---
title: Carga de componentes
seo-title: Component Sideloading
description: La carga lateral de componentes de Communities resulta útil cuando una página web está diseñada como una aplicación de página simple y única que modifica dinámicamente lo que se muestra en función de lo que seleccione el visitante del sitio
seo-description: Communities component sideloading is useful when a web page is designed as a simple, single page app that dynamically alters what is displayed depending on what is selected by the site visitor
uuid: 8c9a5fde-26a3-4610-bc14-f8b665059015
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a9cb5294-e5ab-445b-b7c2-ffeecda91c50
exl-id: 960e132c-b370-43d1-bd8f-e7d0ded7c0b3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Carga de componentes {#component-sideloading}

## Información general {#overview}

La carga lateral de componentes de Communities resulta útil cuando una página web está diseñada como una aplicación de página simple y única que modifica dinámicamente lo que se muestra en función de lo que seleccione el visitante del sitio.

Esto se logra cuando los componentes de Communities no existen en la plantilla de página, sino que se añaden de forma dinámica tras la selección de un visitante del sitio.

Dado que el marco de componentes sociales (SCF) tiene una presencia ligera, solo se registran los componentes de SCF que existen en el momento de la carga inicial de la página. Para que un componente SCF añadido dinámicamente se registre después de la carga de página, se debe invocar SCF para &quot;cargar&quot; el componente.

Cuando una página está diseñada para cargar componentes de Communities, es posible almacenar en caché toda la página.

Los pasos para agregar componentes SCF de forma dinámica son:

1. [Añadir el componente al DOM](#dynamically-add-component-to-dom)

1. [Carga del componente](#sideload-by-invoking-scf) utilizando uno de estos dos métodos:

* [Inclusión dinámica](#dynamic-inclusion)
   * Agrupar todos los componentes añadidos dinámicamente
* [Carga dinámica](#dynamic-loading)
   * Añadir un componente específico bajo demanda

>[!NOTE]
>
>Carga parcial de [recursos no existentes](scf.md#add-or-include-a-communities-component) no es compatible.

## Añadir dinámicamente un componente a DOM {#dynamically-add-component-to-dom}

Tanto si el componente se incluye dinámicamente como si se carga dinámicamente, primero debe agregarse al DOM.

Al añadir el componente SCF, la etiqueta más común que se debe utilizar es la etiqueta DIV, pero también se pueden utilizar otras etiquetas. Dado que SCF solo examina el DOM cuando la página se carga inicialmente, esta adición al DOM pasa desapercibida hasta que se invoque explícitamente SCF.

Sea cual sea la etiqueta utilizada, como mínimo, el elemento debe cumplir el patrón de elemento raíz SCF normal al contener estos dos atributos:

* **data-component-id**

   Ruta efectiva al componente añadido.

* **data-scf-component**

   El resourceType del componente.

A continuación se muestra un ejemplo de un componente de comentarios añadido:

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## Carga secundaria mediante invocación de SCF {#sideload-by-invoking-scf}

### Inclusión dinámica {#dynamic-inclusion}

La inclusión dinámica utiliza una solicitud de ampliación que hace que SCF examine el DOM y arranque todos los componentes SCF que se encuentran en la página.

Para inicializar los componentes SCF en cualquier momento después de la carga de la página, simplemente active un evento JQuery de esta manera:

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### Carga dinámica {#dynamic-loading}

La carga dinámica proporciona control sobre la carga de componentes SCF.

En lugar de arrancar todos los componentes SCF que se encuentran en el DOM, es posible especificar un componente SCF específico para cargar mediante este método JavaScript:

`SCF.addComponent(document.getElementById(*someId*));`

Donde `someId` es el valor de la variable `data-component-id` atributo.
