---
title: Diseño de plantillas de formulario para formularios HTML5
seo-title: Diseño de plantillas de formulario para formularios HTML5
description: AEM Forms ofrece la renderización de plantillas de formulario XFA en formato HTML5. Los diseñadores de formularios pueden diseñar plantillas de formulario con Designer y utilizar la capacidad de representación HTML5.
seo-description: AEM Forms ofrece la renderización de plantillas de formulario XFA en formato HTML5. Los diseñadores de formularios pueden diseñar plantillas de formulario con Designer y utilizar la capacidad de representación HTML5.
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---


# Diseño de plantillas de formulario para formularios HTML5{#designing-form-templates-for-html-forms}

El componente de formularios HTML5 de AEM ofrece la renderización de una plantilla de formulario XFA al formato HTML5. Los diseñadores de formularios pueden diseñar plantillas de formulario utilizando [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) y utilizar la capacidad de representación HTML5. Estas plantillas de formulario, junto con sus recursos, pueden residir en AEM repositorio, sistema de archivos o exponerse a través de http. Sin embargo, si planea administrar los formularios con Forms Manager, las plantillas y los recursos deben residir en el repositorio de AEM.

Aunque los formularios HTML5 coinciden en buena medida con el comportamiento de los PDF forms, hay algunas funciones en ambos formatos que no se pueden aplicar al otro formato. Por ejemplo, la forma en que se aplican los códigos de barras en un formulario PDF en Adobe Reader varía según el formulario móvil o la forma en que se firma digitalmente un formulario también varía según el formato. Para obtener más información sobre estas variaciones, consulte [Distinción de características entre formularios HTML5 y PDF forms](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

Para ver las funciones comunes de XFA, consulte las siguientes prácticas recomendadas y directrices para diseñar un formulario que funcione en ambos formatos.

## Prácticas recomendadas {#best-practices}

La mayoría de los pasos para diseñar una plantilla de formulario, como enlaces de esquema o escribir lógica de formulario, son los mismos. Sin embargo, debido a las diferencias inherentes entre el procesamiento y el motor de secuencias de comandos de un cliente grueso como Adobe Reader y los formularios basados en el explorador, hay algunas recomendaciones que se describen en el artículo [prácticas recomendadas](/help/forms/using/design-accessible-html5-forms.md). Estas prácticas recomendadas le ayudan a diseñar plantillas de formulario para que funcionen según lo esperado en ambos formatos.

### Funciones en AEM Forms Designer para HTML5 Forms {#capabilities-in-aem-forms-designer-for-html-forms}

#### Vista previa de HTML {#preview-html}

La ficha Vista previa de HTML se agrega en el modo Diseño para que los diseñadores de formularios obtengan una vista previa de los formularios en formato HTML5 durante el proceso de diseño. Para obtener más información sobre cómo habilitar y configurar esta capacidad en AEM Forms Designer, consulte [Vista previa de HTML](../../forms/using/preview-xdp-forms-html.md).

#### Firma manuscrita {#scribble-signature}

El destino principal de los formularios HTML5 son los dispositivos táctiles. Por lo tanto, se agrega un nuevo control de firma de anotaciones en AEM Forms Designer. Puede hacer clic o arrastrar y soltar el control de firma de anotaciones en la plantilla de formulario y configurarlo. Se representa como un campo de anotaciones en una representación HTML5 y se puede utilizar para garabatear firmas en dispositivos táctiles. En equipos de escritorio, se puede utilizar como campo de secuencia de comandos utilizando el control del ratón. Para obtener más información sobre cómo utilizar esta función, consulte [Campo de análisis XFA](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### Formato de texto enriquecido {#rich-text-format}

Puede convertir un campo de texto en un campo de texto enriquecido. Añade una lista de opciones de formato al campo de texto. Para convertir, abra Forms Designer, pulse el campo de texto en **[!UICONTROL Vista diseño]**. En la pestaña **[!UICONTROL Field]**, seleccione **[!UICONTROL Rich Text]** en la lista desplegable **[!UICONTROL Field Format]**. Ahora, cuando el formulario XFA se representa como un formulario HTML5, el campo se procesa como un campo de texto enriquecido. Toque ![Maximizar](assets/maximize_icon.svg) para ver opciones de formato adicionales.
