---
title: Diseño de plantillas de formulario para formularios HTML5
seo-title: Designing form templates for HTML5 forms
description: AEM Forms ofrece el procesamiento de plantillas de formulario XFA en formato HTML5. Los diseñadores de formularios pueden diseñar plantillas de formulario con Designer y utilizar la capacidad de representación de HTML5.
seo-description: AEM Forms offers rendering XFA form template to HTML5 format. Form designers can design form templates using Designer and use the HTML5 rendition capability.
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
feature: Mobile Forms
exl-id: 7c8d501f-c953-495e-8bac-1f66fd99c783
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# Diseño de plantillas de formulario para formularios HTML5{#designing-form-templates-for-html-forms}

El componente de formularios de HTML5 en AEM ofrece la renderización de la plantilla de formulario XFA al formato HTML5. Los diseñadores de formularios pueden diseñar plantillas de formulario utilizando [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) y utilice la capacidad de representación de HTML5. Estas plantillas de formulario, junto con sus recursos, pueden residir en AEM repositorio, sistema de archivos o exponerse a través de http. Sin embargo, si planea administrar los formularios con Forms Manager, las plantillas y los recursos deben residir en el repositorio de AEM.

Aunque los formularios HTML5 coinciden en buena medida con el comportamiento de los PDF forms, hay algunas funciones en ambos formatos que no se pueden aplicar al otro formato. Por ejemplo, la forma en que se aplican los códigos de barras en un formulario de PDF en Adobe Reader varía según el formulario de Mobile o la forma en que el formulario se firma digitalmente también varía según el formato. Para obtener más información sobre estas variaciones, consulte [Diferenciación de características entre formularios HTML5 y PDF forms](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

Para ver las funciones comunes de XFA, consulte las siguientes prácticas recomendadas y directrices para diseñar un formulario que funcione en ambos formatos.

## Prácticas recomendadas {#best-practices}

La mayoría de los pasos para diseñar una plantilla de formulario, como enlaces de esquema o escribir lógica de formulario, son los mismos. Sin embargo, debido a las diferencias inherentes entre el procesamiento y el motor de secuencias de comandos de un cliente grueso como Adobe Reader y los formularios basados en el explorador, hay algunas recomendaciones que se describen en la sección [prácticas recomendadas](/help/forms/using/design-accessible-html5-forms.md) artículo. Estas prácticas recomendadas le ayudan a diseñar plantillas de formulario para que funcionen según lo esperado en ambos formatos.

### Funciones en AEM Forms Designer para HTML5 Forms {#capabilities-in-aem-forms-designer-for-html-forms}

#### HTML de vista previa {#preview-html}

La ficha HTML de vista previa se agrega en el modo Diseño para que los diseñadores de formularios obtengan una vista previa de los formularios en formato HTML5 durante el proceso de diseño. Para obtener más información sobre cómo habilitar y configurar esta capacidad en AEM Forms Designer, consulte [HTML de vista previa](../../forms/using/preview-xdp-forms-html.md).

#### Firma manuscrita {#scribble-signature}

El objetivo principal de los formularios HTML5 son los dispositivos táctiles. Por lo tanto, se agrega un nuevo control de firma de anotaciones en AEM Forms Designer. Puede hacer clic o arrastrar y soltar el control de firma de anotaciones en la plantilla de formulario y configurarlo. Se representa como un campo de anotaciones en la representación de HTML5 y se puede utilizar para garabatear la firma en dispositivos táctiles. En equipos de escritorio, se puede utilizar como campo de secuencia de comandos utilizando el control del ratón. Para obtener más información sobre cómo utilizar esta función, consulte [Campo de secuencia de comandos XFA](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### Formato de texto enriquecido {#rich-text-format}

Puede convertir un campo de texto en un campo de texto enriquecido. Añade una lista de opciones de formato al campo de texto. Para convertir, abra el Diseñador de Forms y pulse el campo de texto en **[!UICONTROL Vista diseño]**. En el **[!UICONTROL Campo]** , seleccione **[!UICONTROL Texto enriquecido]** de la variable **[!UICONTROL Formato de campo]** lista desplegable. Ahora, cuando el formulario XFA se representa como un formulario HTML5, el campo se procesa como un campo de texto enriquecido. Toque ![Maximizar](assets/maximize_icon.svg) para ver opciones de formato adicionales.
