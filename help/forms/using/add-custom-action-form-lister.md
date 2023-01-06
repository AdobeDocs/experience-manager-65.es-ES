---
title: Agregar acciones personalizadas a elementos de lista de formularios
seo-title: Adding custom action on form lister items
description: Los desarrolladores de formularios pueden agregar más acciones a la lista de formularios de la página del portal de formularios. De forma predeterminada, la lista de formularios le permite acceder al formulario, rellenarlo y enviarlo.
seo-description: Form developers can add more actions to the listing of forms on the forms portal page. By default, the form listing allows you to access the form, fill it, and submit it.
uuid: 5703ba27-7fb8-482e-b933-a060574165dc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: c34dd4c2-5fff-4355-b86d-cc8a956dd8af
docset: aem65
exl-id: 7c2a91c8-9b68-4491-88e2-f7ea68f5a79f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '265'
ht-degree: 100%

---

# Agregar acciones personalizadas a elementos de lista de formularios{#adding-custom-action-on-form-lister-items}

En AEM Forms, puede crear una página del portal que enumere los formularios disponibles. De forma predeterminada, puede buscar y mostrar formularios en una página del portal. Puede abrir formularios para rellenar y enviar la información. Solo se proporcionan las acciones de procesamiento predeterminadas para los formularios enumerados en una página del portal. Para obtener más información sobre las acciones disponibles en una página del portal, consulte [Crear una página de portal de formularios](../../forms/using/creating-form-portal-page.md).

Puede agregar otras opciones a la página del portal. Estas opciones o acciones se pueden personalizar si personaliza la plantilla del portal de formularios.

Este artículo muestra cómo crear un botón para enviar el vínculo de un formulario, directamente desde una página del portal de formularios. Esta personalización requiere la actualización de la plantilla para el componente Buscar y listar.

El código requerido para agregar la acción a la plantilla está disponible a continuación. El atributo `onclick` del fragmento de código tiene un script para enviar un vínculo de un formulario por correo electrónico.

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

Puede agregar acciones similares en la plantilla personalizada. Para definir una función de JavaScript, agregue la función en un script de nivel de página y vincúlelo con el elemento HTML requerido. En el ejemplo anterior, la expresión `onclick` es la función vinculada.

Después de realizar las ediciones en la plantilla, la página del portal de muestra contiene un botón para enviar el vínculo del formulario por correo electrónico, como se muestra a continuación.

![correo electrónico](assets/email.png)
