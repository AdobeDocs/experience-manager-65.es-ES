---
title: Descarga de componentes
description: La descarga de componentes de Communities es útil cuando una página web está diseñada como una aplicación sencilla de una sola página que modifica dinámicamente lo que se muestra según lo que seleccione el visitante del sitio
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 960e132c-b370-43d1-bd8f-e7d0ded7c0b3
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Descarga de componentes {#component-sideloading}

## Información general {#overview}

La descarga de componentes de Communities es útil cuando una página web está diseñada como una aplicación sencilla de una sola página que modifica dinámicamente lo que se muestra según lo que seleccione el visitante del sitio.

Esto se logra cuando los componentes de Communities no existen en la plantilla de página, sino que se agregan dinámicamente después de la selección de un visitante del sitio.

Dado que el marco de trabajo de componentes sociales (SCF) tiene una presencia ligera, solo se registran los componentes SCF que existen en el momento de la carga inicial de la página. Para que se registre un componente SCF agregado dinámicamente después de la carga de página, se debe invocar SCF para &quot;sideload&quot; el componente.

Cuando se diseña una página para descargar de forma secundaria los componentes de las comunidades, es posible almacenar en caché la página completa.

Los pasos para añadir dinámicamente componentes de SCF son los siguientes:

1. [Añadir el componente al DOM](#dynamically-add-component-to-dom)

1. [Descarga del componente](#sideload-by-invoking-scf) mediante uno de estos dos métodos:

* [Inclusión dinámica](#dynamic-inclusion)
   * Reactivar todos los componentes añadidos dinámicamente
* [Carga dinámica](#dynamic-loading)
   * Añadir un componente específico bajo demanda

>[!NOTE]
>
>Descarga de [recursos no existentes](scf.md#add-or-include-a-communities-component) no es compatible.

## Añadir componente de forma dinámica al DOM {#dynamically-add-component-to-dom}

Tanto si el componente se incluye dinámicamente como si se carga dinámicamente, primero debe agregarse al DOM.

Al añadir el componente SCF, la etiqueta más común que se utiliza es la etiqueta DIV, pero también se pueden utilizar otras etiquetas. Dado que SCF solo examina el DOM cuando la página se carga inicialmente, esta adición al DOM pasará desapercibida hasta que se invoque explícitamente a SCF.

Independientemente de la etiqueta que se utilice, el elemento debe ajustarse, como mínimo, al patrón normal de elemento raíz de SCF, ya que contiene estos dos atributos:

* **data-component-id**

  La ruta efectiva al componente añadido.

* **data-scf-component**

  El resourceType del componente.

A continuación se muestra un ejemplo de un componente de comentarios agregado:

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## Descarga al invocar SCF {#sideload-by-invoking-scf}

### Inclusión dinámica {#dynamic-inclusion}

La inclusión dinámica utiliza una solicitud de bootstrap que hace que SCF examine el DOM y arranque todos los componentes SCF encontrados en la página.

Para inicializar los componentes SCF en cualquier momento después de cargar la página, simplemente active un evento JQuery de esta manera:

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### Carga dinámica {#dynamic-loading}

La carga dinámica proporciona control sobre la carga de componentes SCF.

En lugar de arrancar todos los componentes SCF encontrados en el DOM, es posible especificar un componente SCF específico para cargar mediante este método de JavaScript:

`SCF.addComponent(document.getElementById(*someId*));`

Donde `someId` es el valor de `data-component-id` atributo.
