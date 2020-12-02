---
title: Añadir acción personalizada en elementos de lista de formularios
seo-title: Añadir acción personalizada en elementos de lista de formularios
description: Los desarrolladores de formularios pueden agregar más acciones a la lista de formularios en la página del portal de formularios. De forma predeterminada, la lista de formularios permite acceder al formulario, rellenarlo y enviarlo.
seo-description: Los desarrolladores de formularios pueden agregar más acciones a la lista de formularios en la página del portal de formularios. De forma predeterminada, la lista de formularios permite acceder al formulario, rellenarlo y enviarlo.
uuid: 5703ba27-7fb8-482e-b933-a060574165dc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: c34dd4c2-5fff-4355-b86d-cc8a956dd8af
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Añadir acción personalizada en elementos de lista de formularios{#adding-custom-action-on-form-lister-items}

En AEM Forms, puede crear una página de portal con los formularios disponibles. De forma predeterminada, puede buscar y lista de formularios en una página de portal. Puede abrir formularios para rellenar y enviar la información. Solo se proporcionan acciones de representación de forma predeterminada para los formularios enumerados en una página de portal. Para obtener más información sobre las acciones disponibles en una página de portal, consulte [Creación de una página de portal de formularios](../../forms/using/creating-form-portal-page.md).

Puede agregar otras opciones a la página del portal. Estas opciones o acciones se pueden personalizar personalizando la plantilla del portal de formularios.

Este artículo muestra cómo crear un botón para enviar el vínculo de un formulario, directamente desde una página del portal de formularios. Esta personalización requiere actualizar la plantilla para el componente Búsqueda y listado.

El código requerido para agregar la acción a la plantilla está disponible a continuación. El atributo `onclick` del fragmento de código tiene una secuencia de comandos para enviar un vínculo de un formulario por correo electrónico.

```html
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
  <div class="__FP_boxes-thumbnail">
            <img src ="${contextPath}${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png">
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">Apply</a>
                <a class="__FP_button" title="Email a friend" href="#" onclick="javascript:window.location=&apos;mailto:?subject=Interesting information&body=I thought you might find {name} form helpful :  &apos;+window.location.protocol+window.location.host+&apos;${formUrl}&apos; ;">Email</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">Download</a>
            </div>
        </div>
    </div>
</div>
```

Puede agregar acciones similares en la plantilla personalizada. Para definir una función de JavaScript, agregue la función en una secuencia de comandos de nivel de página y vincúlela con el elemento HTML necesario. En el ejemplo anterior, la expresión `onclick` es la función vinculada.

Después de realizar las modificaciones en la plantilla, la página del portal de muestra contiene un botón para enviar el vínculo del formulario por correo electrónico, como se muestra a continuación.

![email](assets/email.png)

