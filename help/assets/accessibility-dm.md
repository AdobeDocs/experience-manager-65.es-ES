---
title: Accesibilidad en Dynamic Media
description: Obtenga información acerca de la compatibilidad con la accesibilidad en los visores de Dynamic Media y Dynamic Media.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: User, Admin
exl-id: bbdb800c-b6f8-4506-b8ac-daf64edcd6c0
solution: Experience Manager, Experience Manager Assets
source-git-commit: ed7183efa57db6d97941e3acc99d126c2fc0f6c5
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# Accesibilidad en [!DNL Dynamic Media] {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] admite tecnologías de control de teclado y asistencia, como lectores de pantalla JAWS y NVDA, en la interfaz de usuario de creación.

## Compatibilidad de accesibilidad de teclado en [!DNL Dynamic Media]

Porque [!DNL Dynamic Media] es un complemento de para [!DNL Adobe Experience Manager Assets], la mayoría de los comportamientos de control de teclado son los mismos que en [!DNL Experience Manager Assets]. Por ejemplo, la variable `Cancel` botón en [!DNL Dynamic Media] tiene el mismo resaltado de enfoque que en [!DNL Experience Manager Assets], y reacciona a la `Spacebar` clave como en [!DNL Experience Manager Assets]. Consulte [Métodos abreviados de teclado en Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Pulsaciones de teclas compatibles con elementos de interfaz de usuario individuales en [!DNL Dynamic Media] son claras y fáciles de descubrir. Control de teclado en [!DNL Dynamic Media] es acerca de lo siguiente:

* Capacidad de uso `Tab` y `Shift+Tab` pulse las teclas para desplazarse entre los elementos interactivos de la página.
Uso de `Tab` avanza el enfoque de entrada al siguiente elemento de interfaz de usuario en el orden de tabulación; utilizando `Shift+Tab` vuelve a enfocar la entrada al elemento de interfaz de usuario anterior.
La inversión del enfoque sigue la ubicación natural del elemento de la interfaz de usuario en la pantalla y se mueve de izquierda a derecha y, a continuación, de arriba a abajo. Además, si algún campo tiene un error, puede pulsar `Tab` para desplazar el foco a él.
* Capacidad para utilizar el `Spacebar` y `Enter` para activar elementos estándar de la interfaz de usuario, como botones y listas desplegables.
* Posibilidad de ver el resalte de enfoque del teclado en el elemento activo. El elemento de interfaz de usuario que tiene el enfoque de entrada recibe una indicación de enfoque visual como un borde procesado alrededor del elemento de interfaz de usuario.
* En el editor de puntos interactivos, puede utilizar algunas pulsaciones de teclas personalizadas, como las teclas de flecha, para interactuar con elementos complejos de la interfaz de usuario y cambiar la posición de los puntos interactivos.
* En el editor de vídeo interactivo, puede utilizar el `Spacebar` para seleccionar una imagen y añadirla a un segmento. Además, puede utilizar la variable `Backspace` para eliminar el elemento seleccionado de la **[!UICONTROL Contenido]** pestaña. Además, presionando `Tab` funciona como desee para desplazarse entre los elementos interactivos de la página.
* En el editor de recorte inteligente/recorte inteligente de imágenes, puede hacer lo siguiente:
   * Utilice las teclas de flecha para recortar el tamaño del marco, cambiar la posición de la imagen o ambas cosas.
   * El primero `Tab` stop resalta todo el marco de la imagen. A continuación, puede utilizar las teclas de flecha del teclado para cambiar la posición del marco.
   * Los cuatro próximos `Tab` las paradas son las cuatro esquinas del marco. Cuando el enfoque se coloca en una esquina del marco, la esquina se resalta. De nuevo, puede utilizar las teclas de flecha del teclado para mover la esquina enfocada.
Consulte [Editar el recorte inteligente o la muestra inteligente de una sola imagen](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Soporte de tecnología de asistencia en [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] Los elementos de la interfaz de usuario de trabajan con tecnologías de asistencia como lectores de pantalla. Por ejemplo, reconoce los puntos de referencia de una página cuando se navegan por ellos mediante el método abreviado de teclado `D` o regiones mediante métodos abreviados de teclado `R`. También narra el encabezado al navegar mediante el método abreviado de teclado para encabezados `H`.

## Compatibilidad de accesibilidad de teclado en [!DNL Dynamic Media] visores {#keyboard-accessibility-for-dm-viewers}

Todo listo para usar [!DNL Dynamic Media] los componentes de visores admiten la accesibilidad del teclado para sus clientes.

Consulte [Navegación y accesibilidad del teclado](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) en la Guía de referencia de visores de Dynamic Media.

## Soporte de tecnología de asistencia en [!DNL Dynamic Media] visores {#assistive-technology-support-for-dm-viewers}

Todo [!DNL Dynamic Media] Los componentes del visor admiten funciones y atributos ARIA (Aplicaciones de Internet enriquecidas accesibles) para mejorar la integración con tecnologías de asistencia como lectores de pantalla.
Consulte la **Soporte de tecnología de asistencia** Tema de ayuda de cualquier tema sobre personalización del visor en la Guía de referencia de visores de Dynamic Media. Por ejemplo, consulte [Soporte de tecnología de asistencia](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) para el visualizador de vídeo, o [Soporte de tecnología de asistencia](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) para el visualizador de imágenes interactivo.

## Compatibilidad con subtítulos opcionales en Dynamic Media {#closed-caption-support}

Dynamic Media admite la entrega de vídeos y conjuntos de vídeos adaptables con subtítulos. Los subtítulos deben mostrarse sobre el contenido del vídeo.

Consulte [Vídeo en Dynamic Media: Añadir subtítulos para el vídeo](/help/assets/video.md#adding-captions-to-video).

>[!MORELIKETHIS]
>
>* [Accesibilidad para las soluciones de Adobe](https://www.adobe.com/accessibility.html)
>* [Accesibilidad en [!DNL Experience Manager Assets]](/help/assets/accessibility.md)
