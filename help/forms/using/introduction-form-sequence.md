---
title: Introducción a la secuencia de formulario de varios pasos
seo-title: Introduction to multi-step form sequence
description: Con AEM Forms, puede definir una secuencia de panel de formulario en la que desea que los usuarios naveguen y rellenen un formulario adaptable.
seo-description: With AEM Forms, you can define a sequence of form panel in which you want users to navigate and fill an adaptive form.
uuid: db1aac25-fe69-4e43-88d1-4a15389b507f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0f335ea0-504f-4cc0-b97b-c3fc715bcc2e
docset: aem65
feature: Adaptive Forms
exl-id: 1333c6cb-15cc-429b-a13e-5d23afdee69a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 54%

---

# Introducción a la secuencia de formulario de varios pasos{#introduction-to-multi-step-form-sequence}

Los formularios adaptables permiten a los autores de formularios crear experiencias de captura de datos en varios pasos con buena facilidad. Estos formularios incluyen compatibilidad para crear varios paneles y asociar cada uno con diferentes patrones de navegación. Los autores de formularios pueden agrupar los campos de formulario en secciones lógicas y representar un grupo como un panel. La navegación general entre los paneles se controla mediante el diseño del panel. Los autores pueden elegir organizar los paneles en diferentes diseños, por ejemplo, colocándolos secuencialmente utilizando el diseño del asistente o de forma ad hoc utilizando el diseño en Pestaña. Para obtener información sobre los diseños de panel, consulte [Funciones de diseño de formularios adaptables](../../forms/using/layout-capabilities-adaptive-forms.md).

Normalmente, durante la experiencia de rellenado de un formulario, hay que seguir más pasos además de capturar los datos. Un envío de formulario completo puede incluir otros pasos, como firmar el formulario de forma digital, verificar la información con la que se ha rellenado el formulario, procesar pagos, etc. Cada caso es diferente.

Si el caso de uso requiere un conjunto de pasos para la captura de datos o hay regulaciones que necesitan seguir ciertos pasos, AEM Forms proporciona una forma de aplicar esa estructura común en todos los formularios. La implementación planificada de la estructura del formulario define la secuencia de pasos de ese formulario. ![Ejemplo de secuencia de formulario de varios pasos](assets/formpipeline.png)

Ejemplo de secuencia de formulario de varios pasos

Veamos un caso de uso en el que necesita crear una secuencia para rellenar, verificar, firmar y pasos de confirmación de un formulario. Los pasos para crear una secuencia de este tipo son los siguientes:

1. Defina una plantilla de formulario y añádale el panel requerido. Tenga en cuenta que debe haber un panel para cada paso de la secuencia. Sin embargo, puede incluir subpaneles dentro de un panel.

   En este ejemplo, podemos añadir los siguientes paneles:

   * **Rellenado**: contiene campos de formulario para capturar datos. Aquí puede incluir subpaneles anidados para crear secciones para distintos tipos de información, como personal, familia, finanzas, etc.

   * **Verificar**: Contiene el **Verificar** que se puede utilizar en un formulario adaptable basado en XFA. Muestra la información capturada en el panel Relleno en modo de solo lectura para la verificación.

   * **Signo electrónico**: Contiene el **Sign** que se puede utilizar en un formulario adaptable basado en XFA. proporciona los siguientes servicios de firma:

      * Servicios de firma electrónica de Adobe Document Cloud
      * Firma manuscrita
   * **Confirmación**: contiene el componente **Resumen** que muestra un mensaje que confirma el envío del formulario una vez que el usuario lo ha firmado y llega al paso Confirmación (Resumen) de la secuencia. Los autores pueden configurar el texto del componente Resumen, mostrar un mensaje de agradecimiento, mostrar un vínculo al PDF generado, etc.


1. Seleccione el diseño del panel raíz como **[!UICONTROL Asistente]**.
1. Complete los pasos restantes para crear la plantilla de formulario. Para obtener más información, consulte [Creación de una plantilla de formulario adaptable personalizada](../../forms/using/custom-adaptive-forms-templates.md).

Después de definir la secuencia del formulario en la plantilla de formulario, puede utilizarla para crear formularios que tengan la estructura básica definida como dicha secuencia, aunque siempre puede personalizar el formulario para adaptarlo a sus necesidades.
