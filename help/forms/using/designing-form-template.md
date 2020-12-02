---
title: Diseño de plantillas de formulario para formularios HTML5
seo-title: Diseño de plantillas de formulario para formularios HTML5
description: AEM Forms oferta la representación de una plantilla de formulario XFA en formato HTML5. Los diseñadores de formularios pueden diseñar plantillas de formulario con Designer y utilizar la capacidad de representación HTML5.
seo-description: AEM Forms oferta la representación de una plantilla de formulario XFA en formato HTML5. Los diseñadores de formularios pueden diseñar plantillas de formulario con Designer y utilizar la capacidad de representación HTML5.
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# Diseño de plantillas de formulario para formularios HTML5{#designing-form-templates-for-html-forms}

Componente de formularios HTML5 en ofertas de AEM que procesa la plantilla de formulario XFA en formato HTML5. Los diseñadores de formularios pueden diseñar plantillas de formulario mediante [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) y utilizar la capacidad de representación HTML5. Estas plantillas de formulario, junto con sus recursos, pueden residir en AEM repositorio, sistema de archivos o expuestas mediante http. Sin embargo, si planea administrar los formularios con Forms Manager, las plantillas y los recursos deben residir en el repositorio de AEM.

Aunque los formularios HTML5 coinciden en buena medida con el comportamiento de los PDF forms, hay algunas funciones en ambos formatos que no se pueden aplicar al otro. Por ejemplo, la forma en que se aplican los códigos de barras en un formulario PDF en Adobe Reader varía según el formulario móvil o la forma en que se firma digitalmente un formulario también varía según el formato. Para obtener más información sobre estas variaciones, consulte [Diferenciación de funciones entre formularios HTML5 y PDF forms](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

Para ver las funciones XFA comunes, consulte las siguientes optimizaciones y directrices para diseñar un formulario que funcione en ambos formatos.

## Prácticas recomendadas {#best-practices}

La mayoría de los pasos para diseñar una plantilla de formulario, como enlaces de esquema o escritura de lógica de formulario, son los mismos. Sin embargo, debido a las diferencias inherentes entre el motor de procesamiento y de secuencias de comandos de un cliente grueso como Adobe Reader y los formularios basados en explorador, hay algunas recomendaciones que se describen en el artículo [prácticas recomendadas](/help/forms/using/design-accessible-html5-forms.md). Estas prácticas recomendadas le ayudan a diseñar plantillas de formulario para que funcionen correctamente en ambos formatos.

### Capacidades de AEM Forms Designer para HTML5 Forms {#capabilities-in-aem-forms-designer-for-html-forms}

#### HTML de previsualización {#preview-html}

La ficha HTML de Previsualización se agrega en el modo de diseño para que los diseñadores de formularios previsualización formularios en formato HTML5 durante el proceso de diseño. Para obtener más información sobre cómo habilitar y configurar esta capacidad en AEM Forms Designer, consulte [Previsualización HTML](../../forms/using/preview-xdp-forms-html.md).

#### Firma manuscrita {#scribble-signature}

El destinatario clave para los formularios HTML5 son los dispositivos táctiles. Por lo tanto, se agrega un nuevo control de firma de garabatos en AEM Forms Designer. Puede hacer clic o arrastrar y soltar el control de firma de garabatos en la plantilla de formulario y configurarlo. Se procesa como un campo de garabatos en la representación HTML5 y se puede utilizar para garabatear la firma en dispositivos táctiles. En equipos de escritorio, se puede utilizar como campo de garabateo mediante el control del ratón. Para obtener más información sobre cómo utilizar esta función, consulte [Campo de garabatos XFA](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### Formato de texto enriquecido {#rich-text-format}

Puede convertir un campo de texto en un campo de texto enriquecido. Agrega una lista de opciones de formato al campo de texto. Para convertir, abra Forms Designer, toque el campo de texto en **[!UICONTROL Vista de diseño]**. En la ficha **[!UICONTROL Campo]**, seleccione **[!UICONTROL Texto enriquecido]** en la lista desplegable **[!UICONTROL Formato del campo]**. Ahora, cuando el formulario XFA se procesa como un formulario HTML5, el campo se procesa como un campo de texto enriquecido. Toque ![Maximizar](assets/maximize_icon.svg) para vista de opciones de formato adicionales.
