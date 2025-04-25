---
title: Cómo abrir PDF forms basado en XFA en Firefox y Chrome
description: Cómo abrir PDF forms basado en XFA en Firefox y Chrome
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ebb61f2c5056a780e829e64031f8eba69a8ae25b
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---

# Cómo abrir PDF forms basado en XFA en Firefox y Chrome

## Problema

El visor integrado de PDF incluido con Mozilla Firefox y Google Chrome no es compatible con PDF forms basados en XFA. Por lo tanto, los PDF forms basados en XFA no se abren en versiones posteriores de Firefox y Chrome.

## Solución

Para utilizar PDF forms basado en XFA en Firefox y Chrome, realice los siguientes pasos para configurar Firefox y Chrome para abrir archivos PDF con Adobe Reader o Adobe Acrobat.

>[!NOTE]
> 
> Asegúrese de que tiene Adobe Reader o Adobe Acrobat instalados en el equipo.

### Configuración de Firefox

1. En Firefox, elija **Herramientas > Opciones**.

1. En el diálogo Opciones, haga clic en **Aplicaciones**.

1. En la pestaña Aplicaciones, escriba PDF en el campo de búsqueda.

1. Para el tipo de contenido Formato de documento portátil (PDF) en el resultado de búsqueda, seleccione **Usar Adobe Acrobat (en Firefox)** en la lista desplegable Acción.
   ![use-adobe-acrobat](/help/forms/using/assets/use-adobe-acrobat.png)
1. Haga clic en Aceptar.

1. Reinicie Firefox.

### Configuración de Chrome

1. En Chrome, vaya a chrome://plugins/.

1. Haga clic en Deshabilitar en el Visor de Chrome PDF y, a continuación, en Habilitar en el complemento de Adobe PDF.
   ![chrome-pdf-viewer](/help/forms/using/assets/chrome-image.png)
Para obtener más información, consulte la documentación de [Adobe PDF plug-in](https://support.google.com/chrome/?hl=en&amp;visit_id=638803785294106945-2276548125&amp;rd=4&amp;topic=3421431#topic=7439538) de Google.

>[!NOTE]
> 
> LiveCycle ES4 proporciona compatibilidad para procesar formularios basados en XFA en HTML5, de modo que los formularios se puedan abrir en exploradores compatibles con HTML5, incluidos los que se ejecutan en dispositivos móviles como iPad. La representación HTML5 de los formularios mantiene la presentación del diseño de formulario y admite la mayoría de las lógicas de formulario (como JavaScript, cálculo de formulario y validaciones de formulario) incrustadas en la plantilla de formulario XFA. De este modo, sus inversiones en tecnología en formularios XFA se transfieren fácilmente a dispositivos en los que no es posible ejecutar el complemento Adobe Reader.
>Para obtener más información, consulte [Documentación del producto de LiveCycle](https://business.adobe.com/products/experience-manager/forms/aem-forms.html).

[Avisos legales](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [Política de privacidad en línea](https://www.adobe.com/es/privacy.html)