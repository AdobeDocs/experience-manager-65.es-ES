---
title: Introducción a la secuencia de formularios de varios pasos
seo-title: Introducción a la secuencia de formularios de varios pasos
description: Con AEM Forms, puede definir una secuencia de panel de formularios en la que desee que los usuarios naveguen y rellenen un formulario adaptable.
seo-description: Con AEM Forms, puede definir una secuencia de panel de formularios en la que desee que los usuarios naveguen y rellenen un formulario adaptable.
uuid: db1aac25-fe69-4e43-88d1-4a15389b507f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0f335ea0-504f-4cc0-b97b-c3fc715bcc2e
docset: aem65
translation-type: tm+mt
source-git-commit: 68ea2335a8466c3c23b766efb1a04b6a38d7f670
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---


# Introducción a la secuencia de formularios de varios pasos{#introduction-to-multi-step-form-sequence}

Los formularios adaptables permiten a los autores crear una experiencia de captura de datos de varios pasos con buena facilidad. Incluye compatibilidad integrada para crear varios paneles y asociar cada panel con diferentes patrones de navegación. Los autores de formularios pueden agrupar campos de formulario en secciones lógicas y representar un grupo como un panel. La navegación general entre paneles se controla mediante la presentación del panel. Los autores pueden elegir organizar los paneles en diferentes diseños, por ejemplo, colocándolos secuencialmente mediante el diseño Asistente o de forma ad-hoc mediante el diseño Con fichas. Para obtener información sobre los diseños de panel, consulte [Funciones de diseño de formularios adaptables](../../forms/using/layout-capabilities-adaptive-forms.md).

En una experiencia típica de cumplimentación de formularios, hay más pasos involucrados que simplemente capturar datos. Un envío de formulario completo puede incluir otros pasos, como firmar digitalmente el formulario, verificar la información rellenada en el formulario, procesar pagos, etc. Difiere de un caso a otro.

Si el caso de uso requiere un conjunto de pasos para la captura de datos o existen regulaciones que necesitan seguir determinados pasos, AEM Forms proporciona una manera de aplicar esa estructura común en todos los formularios. La implementación premeditada de la estructura del formulario define la secuencia de pasos para un formulario. ![Ejemplo de secuencia de formularios de varios pasos](assets/formpipeline.png)

Ejemplo de secuencia de formularios de varios pasos

Veamos un caso de uso en el que necesita crear una secuencia para rellenar, verificar, firmar y confirmar un formulario. Los pasos para crear una secuencia de este tipo son los siguientes:

1. Defina una plantilla de formulario y añádala el panel requerido. Tenga en cuenta que debe haber un panel para cada paso de la secuencia. Sin embargo, puede incluir subpaneles dentro de un panel.

   En este ejemplo, podemos agregar los paneles siguientes:

   * **Relleno**: Contiene campos de formulario para capturar datos. Aquí puede incluir subpaneles anidados para crear secciones para distintos tipos de información, como personal, familiar, financiera, etc.

   * **Verificar**: Contiene el  **** componente Verifyque se puede utilizar en un formulario adaptable basado en XFA. Muestra la información capturada en el panel Relleno en modo de solo lectura para verificación.

   * **Firma** electrónica: Contiene el  **** componente Signcomponent que se puede utilizar en un formulario adaptable basado en XFA. proporciona los siguientes servicios de firma:

      * Servicios de Adobe Document Cloud eSign
      * Firma manuscrita
   * **Confirmación**: Contiene el  **** componente Resumen que muestra un mensaje que confirma el envío del formulario después de que un usuario firme el formulario y llegue al paso Confirmación (Resumen) de la secuencia. Los autores pueden configurar el texto del componente Resumen, mostrar un mensaje de agradecimiento, mostrar un vínculo al PDF generado, etc.


1. Seleccione el diseño del panel raíz como **[!UICONTROL Asistente]**.
1. Complete los pasos restantes para crear la plantilla de formulario. Para obtener más información, consulte [Creación de una plantilla de formulario adaptable personalizada](../../forms/using/custom-adaptive-forms-templates.md).

Después de definir la secuencia de formularios en la plantilla de formulario, puede utilizarla para crear formularios que tengan la estructura básica definida como la secuencia en su lugar, aunque siempre puede personalizar el formulario para que se ajuste a sus necesidades.

