---
title: No se pueden abrir PDF forms basados en XFA en Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer o Apple Safari
description: No se pueden abrir PDF forms basados en XFA en Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer o Apple Safari
seo-title: Unable to open XFA-based PDF forms in Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer, or Apple Safari
feature: Adaptive Forms
exl-id: fdd15315-e0d6-4d80-acb4-2e0ecec716c4
source-git-commit: 2f1e6eb5451e76b9688401b32d4866ed74cca84e
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# No se pueden abrir PDF forms basados en XFA en Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer o Apple Safari{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

Muchas versiones recientes de exploradores han incluido su propia compatibilidad limitada con PDF forms basados en XFA. Aunque estos exploradores pueden abrir PDF forms basados en XFA, las capacidades proporcionadas son limitadas. Si no puede abrir o enviar un formulario de PDF basado en XFA en un explorador moderno, utilice uno de los siguientes métodos:

* Uso [Adobe ® Acrobat®](https://www.adobe.com/acrobat.html) o [Adobe ® Adobe ® Reader ®](https://get.adobe.com/es/reader/), versión 8 o posterior para abrir y enviar PDF forms basados en XFA.
* Acrobat y Reader, en Microsoft® Windows®, permiten configurar para abrir PDF en modo Vista protegida, lo que impide que se abran PDF forms basados en XFA. Asegúrese de que el modo Vista protegida del Acrobat o del Reader esté deshabilitado. Para obtener más información, consulte [Vista protegida (solo Windows)](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html).
* (Para desarrolladores de Forms) Adobe Experience Manager Forms también proporciona asistencia para lo siguiente:

   * [procesar formularios basados en XFA en HTML5 Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?#key-capabilities-of-html-forms-br) de forma que los formularios se puedan abrir en exploradores compatibles con HTML5, incluidos los que se ejecuten en dispositivos móviles como iPad. La representación de los formularios de HTML5 mantiene la presentación del diseño de formulario y admite la mayoría de las lógicas de formulario (como JavaScript, cálculo de formulario y validaciones de formulario) incrustadas en la plantilla de formulario XFA.
   * [Conversión de formularios basados en XFA a Forms adaptable móvil adaptable](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?#create-an-adaptive-form-based-on-an-xfa-form-template). Estos formularios proporcionan un diseño interactivo, funciones de personalización y se adaptan de forma dinámica a las respuestas del usuario añadiendo o eliminando campos o secciones según sea necesario. También proporcionan conectores predeterminados para varias fuentes de datos, funciones de documento de registro y una conexión sencilla a Adobe Analytics para evaluar el rendimiento. Para obtener más información, consulte [Funciones y capacidades clave](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/key-features.html).

De este modo, sus inversiones en tecnología en formularios XFA están protegidas y siguen proporcionando una experiencia óptima a los usuarios finales. Para obtener más información, consulte [Documentación del producto de Adobe Experience Manager Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html).
