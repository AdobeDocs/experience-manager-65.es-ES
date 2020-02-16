---
title: Lectores de pantalla para formularios HTML5
seo-title: Lectores de pantalla para formularios HTML5
description: Enumera los lectores de pantalla admitidos en los formularios HTML5.
seo-description: Enumera los lectores de pantalla admitidos en los formularios HTML5.
uuid: 035354e2-957f-4eb6-bc16-4ca96ec7ac74
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Lectores de pantalla para formularios HTML5 {#screen-readers-for-html-forms}

Los componentes de formularios HTML5 representan la plantilla de formulario XFA en un formato HTML5. Todos los navegadores estándar compatibles con HTML5 pueden procesar estos formularios. Para admitir una experiencia de captura de datos similar en formularios PDF y HTML5, la presentación de los formularios PDF se conserva en formularios HTML5.

Los formularios HTML5 utilizan construcciones HTML estándar que permiten utilizar herramientas de accesibilidad regulares para HTML con estos formularios. Si un formulario está diseñado según las prácticas recomendadas para formularios accesibles, funciona con cualquier lector de pantalla admitido. Además, estos formularios están activados para la navegación mediante el teclado.

## Normas de accesibilidad {#accessibility-standards}

Los formularios HTML5 cumplen con la sección 508 para accesibilidad con excepciones conocidas. Consulte [VPAT para formularios](https://www.adobe.com/mena_en/accessibility/compliance/livecycle-mobile-forms-es4-section-508-vpat.html) HTML5 para obtener más información.

## Lectores de pantalla certificados para formularios HTML5 {#certified-screen-readers-for-html-forms}

* JAWS 14.0 en Microsoft Windows
* VoiceOver en Mac OS X y iPad

### JAWS {#jaws}

Todas las pulsaciones de teclas y los métodos abreviados predeterminados funcionan en formularios HTML5. Para obtener más información sobre el uso de JAWS, visite [https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp).

### VoiceOver {#voiceover}

Los formularios HTML5 admiten todas las pulsaciones de teclas y gestos predeterminados de Voz sobre. Para obtener más información sobre la configuración y el uso de VoiceOver, consulte [https://www.apple.com/accessibility/voiceover/](https://www.apple.com/accessibility/voiceover/).

## Problemas conocidos {#known-issues}

* **(Solo en el Explorador interno 9)** En los formularios HTML5, las páginas se cargan a petición (dinámicamente). La carga de página a petición causa problemas con el funcionamiento de los lectores de pantalla. Cuando el enfoque del lector de pantalla está en el último campo de la página y el usuario pulsa la ficha, en lugar de definir el enfoque en el primer campo de la página siguiente, el lector de pantalla vuelve a centrarse en el primer campo de la primera página del formulario.
* **(Solo en el Explorador interno 9)** El control Selector de fecha de los formularios HTML5 no es totalmente accesible con el teclado. En el control Selector de fecha, si presiona varias veces las teclas de dirección Subir/Bajar, el control Selector de fecha se cierra y el enfoque se mueve al campo siguiente/último.

* VoiceOver no puede detectar las teclas de flecha en la utilidad de fecha en iPad safari.

**[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)**
