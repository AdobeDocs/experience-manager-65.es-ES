---
title: Mostrar problemas para documentos protegidos por directivas y PDF forms basados en XFA
description: Mostrar problemas para documentos protegidos por directivas y PDF forms basados en XFA
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ebb61f2c5056a780e829e64031f8eba69a8ae25b
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Mostrar problemas para documentos protegidos por directivas y PDF forms basados en XFA

Consulte por los siguientes motivos si no puede abrir un formulario de PDF basado en XFA o un documento protegido por una directiva mediante Adobe LiveCycle Rights Management:

* Los documentos protegidos por directivas y PDF forms basados en XFA requieren Adobe® Acrobat® o Adobe® Reader®, versión 8 y posteriores. Consulte [Descargas de Adobe](https://www.adobe.com/downloads.html) para descargar la última versión de Reader o Acrobat.
* Navegadores como Mozilla Firefox y Google Chrome ofrecen un visor de PDF integrado que no admite PDF forms basado en XFA. Para ver PDF forms basado en XFA en estos exploradores, debe configurar para abrir archivos PDF con Acrobat o Reader. Para obtener más información, consulte PDF forms basado en XFA en Mozilla Firefox y Google Chrome.
* Acrobat y Reader, en Microsoft® Windows®, le permiten configurar para abrir archivos PDF en modo de Vista protegida, lo que impide que se abran documentos protegidos por directivas y PDF forms basados en XFA. Asegúrese de que el modo Vista protegida de su Acrobat o Reader esté deshabilitado. Para obtener más información, consulte [Vista protegida (solo Windows)](https://helpx.adobe.com/acrobat/kb/end-of-support-acrobat-x-reader-x.html).
* Si intenta acceder a documentos protegidos por directivas o PDF forms basados en XFA en su dispositivo móvil, tenga en cuenta lo siguiente:

   * La apertura de documentos protegidos por directivas en dispositivos móviles requiere Adobe Reader para dispositivos móviles. Para obtener más información, consulte [Aplicación móvil de Adobe Reader](https://www.adobe.com/in/acrobat/mobile/acrobat-reader.html).
   * Los dispositivos móviles y smartphones iOS, Android y Blackberry no son compatibles con el complemento Adobe Reader de los formularios XFA. LiveCycle ES4 proporciona un servicio que se dirige a dispositivos móviles que utilizan HTML5; el creador del formulario debe utilizar ese servicio para permitir que los formularios se utilicen en estos dispositivos.
   * Si utiliza el estilo Metro en un dispositivo móvil con Windows 8, cambie a la vista estándar o aproveche HTML5 con LiveCycle ES4.

>[!NOTE]
>
>LiveCycle ES4 proporciona compatibilidad para procesar formularios basados en XFA en HTML5, de modo que los formularios se puedan abrir en exploradores compatibles con HTML5, incluidos los que se ejecutan en dispositivos móviles como iPad. La representación HTML5 de los formularios mantiene la presentación del diseño de formulario y admite la mayoría de las lógicas de formulario (como JavaScript, cálculo de formulario y validaciones de formulario) incrustadas en la plantilla de formulario XFA. De este modo, sus inversiones en tecnología en formularios XFA se transfieren fácilmente a los dispositivos donde no es posible ejecutar el complemento Adobe Reader.
>Para obtener más información, consulte Actualizar a [documentación del producto de LiveCycle](https://business.adobe.com/products/experience-manager/forms/aem-forms.html).

[Avisos legales](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [Política de privacidad en línea](https://www.adobe.com/es/privacy.html)