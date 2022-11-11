---
title: No se pueden abrir PDF forms basados en XFA en Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer o Apple Safari
description: No se pueden abrir PDF forms basados en XFA en Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer o Apple Safari
seo-title: Unable to open XFA-based PDF forms in Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer, or Apple Safari
feature: Adaptive Forms
source-git-commit: f2b76ce0c2f296f81c3748794bf2ab74ccd5bb95
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# No se pueden abrir PDF forms basados en XFA en Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer o Apple Safari{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

Muchas versiones recientes de exploradores han incluido su propia compatibilidad limitada con PDF forms basados en XFA. Aunque estos exploradores pueden abrir PDF forms basados en XFA, las capacidades proporcionadas son limitadas. Si no puede abrir o enviar un formulario de PDF basado en XFA en un explorador moderno, utilice uno de los siguientes métodos:

* Uso [Adobe® Acrobat®](https://www.adobe.com/acrobat.html) o [Reader® Adobe® Adobe®](https://get.adobe.com/reader/), versión 8 o posterior para abrir y enviar PDF forms basados en XFA.
* Acrobat y el Reader, en Microsoft® Windows®, le permiten configurar para abrir PDF en modo de vista protegida, lo que impide que se abran PDF forms basados en XFA. Asegúrese de que el modo de Vista protegida de su Acrobat o Reader esté desactivado. Para obtener más información, consulte [Vista protegida (solo Windows)](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html).
* (Para desarrolladores de Forms) Adobe Experience Manager Forms también ofrece asistencia para:

   * [procesar formularios basados en XFA en HTML5 Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?#key-capabilities-of-html-forms-br) de forma que los formularios se puedan abrir en navegadores compatibles con HTML5, incluidos los que se ejecuten en dispositivos móviles como iPad. La representación HTML5 de los formularios mantiene la presentación del diseño de formulario y admite la mayoría de las lógicas de formulario (como JavaScript, cálculo de formulario y validaciones de formulario) incrustadas en la plantilla de formulario XFA.
   * [convertir formularios basados en XFA en Forms adaptable para móviles](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?#create-an-adaptive-form-based-on-an-xfa-form-template). Estos formularios proporcionan un diseño interactivo, capacidades de personalización y se adaptan dinámicamente a las respuestas del usuario añadiendo o eliminando campos o secciones según sea necesario. También proporcionan conectores listos para usar para diversas fuentes de datos, funciones de Document of Record y fácil conexión con Adobe Analytics para la evaluación del rendimiento. Para obtener más información, consulte [Funciones y capacidades clave](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/key-features.html).

De este modo, las inversiones en tecnología en formularios XFA están protegidas y siguen ofreciendo una experiencia óptima para los usuarios finales. Para obtener más información, consulte [Documentación del producto de Adobe Experience Manager Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html).
