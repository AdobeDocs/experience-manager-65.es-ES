---
title: Accesibilidad en Dynamic Media
description: Obtenga información sobre la compatibilidad con la accesibilidad en los visores de Dynamic Media y Dynamic Media.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: User, Admin
exl-id: bbdb800c-b6f8-4506-b8ac-daf64edcd6c0
source-git-commit: 01de1d5064f5ebf00acd2fe9f138d852f41f7273
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# Accesibilidad en [!DNL Dynamic Media] {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] admite tecnologías de control de teclado y asistencia, como lectores de pantalla JAWS y NVDA, en la interfaz de usuario de creación.

## Compatibilidad con la accesibilidad del teclado en [!DNL Dynamic Media]

Porque [!DNL Dynamic Media] es un complemento para [!DNL Adobe Experience Manager Assets], la mayoría del comportamiento del control de teclado es el mismo que en [!DNL Experience Manager Assets]. Por ejemplo, la variable `Cancel` botón [!DNL Dynamic Media] tiene el mismo enfoque que en [!DNL Experience Manager Assets]y reacciona a la `Spacebar` clave como en [!DNL Experience Manager Assets]. Consulte [Métodos abreviados del teclado en Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Pulsaciones de teclas admitidas por elementos individuales de la interfaz de usuario en [!DNL Dynamic Media] son claras y fáciles de descubrir. Control de teclado en [!DNL Dynamic Media] es acerca de lo siguiente:

* Capacidad de uso `Tab` y `Shift+Tab` pulsaciones de teclas para desplazarse entre los elementos interactivos de la página.
Uso `Tab` avanza el enfoque de entrada al siguiente elemento de interfaz de usuario en el orden de tabulación; using `Shift+Tab` devuelve el enfoque de entrada al elemento de interfaz de usuario anterior.
El enfoque transversal sigue la ubicación del elemento de la interfaz de usuario natural en la pantalla y se mueve de izquierda a derecha y, a continuación, de arriba a abajo. Además, si algún campo presenta un error, puede pulsar `Tab` para mover el enfoque a él.
* Capacidad para usar la variable `Spacebar` y `Enter` para activar elementos estándar de la interfaz de usuario, como botones y listas desplegables.
* Posibilidad de ver el resaltado del foco del teclado en el elemento activo. El elemento de interfaz de usuario que tiene enfoque de entrada recibe una indicación de enfoque visual como borde representado alrededor del elemento de interfaz de usuario.
* En el editor de puntos interactivos, puede utilizar algunas pulsaciones de teclas personalizadas, como teclas de flecha, para interactuar con elementos complejos de la interfaz de usuario con el fin de cambiar la posición de los puntos interactivos.
* En el editor de vídeo interactivo, puede usar la variable `Spacebar` para seleccionar una imagen y añadirla a un segmento. Además, puede usar la variable `Backspace` para eliminar el elemento seleccionado del **[!UICONTROL Contenido]** pestaña . También, presionando `Tab` para desplazarse entre los elementos interactivos de la página.
* En el editor Recorte de imagen/Recorte inteligente, puede hacer lo siguiente:
   * Utilice las teclas de flecha para recortar el tamaño del marco, o para cambiar la posición de la imagen, o ambas.
   * La primera `Tab` stop resalta todo el marco de imagen. A continuación, puede utilizar las teclas de flecha del teclado para cambiar la posición del marco.
   * Las cuatro siguientes `Tab` las paradas son las cuatro esquinas del marco. Cuando el enfoque se coloca en una esquina de marco, la esquina se resalta. De nuevo, puede utilizar las teclas de flecha del teclado para mover la esquina enfocada.
Consulte [Editar el recorte inteligente o la muestra inteligente de una sola imagen](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Soporte técnico de asistencia en [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] los elementos de la interfaz de usuario funcionan con tecnologías de asistencia, como lectores de pantalla. Por ejemplo, reconoce los puntos de referencia en una página cuando se navegan por los puntos de referencia mediante el método abreviado de teclado `D` o regiones que utilicen la combinación de teclas `R`. También narra el encabezado al navegar mediante la combinación de teclas del encabezado `H`.

## Compatibilidad con la accesibilidad del teclado en [!DNL Dynamic Media] visualizadores {#keyboard-accessibility-for-dm-viewers}

Todo listo para usar [!DNL Dynamic Media] los componentes visualizadores admiten la accesibilidad mediante teclado para sus clientes.

Consulte [Navegación y accesibilidad del teclado](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) en la Guía de referencia de visores de Dynamic Media.

## Soporte técnico de asistencia en [!DNL Dynamic Media] visualizadores {#assistive-technology-support-for-dm-viewers}

Todo [!DNL Dynamic Media] los componentes del visor admiten las funciones y atributos de ARIA (Aplicaciones de Internet enriquecidas accesibles) para mejorar la integración con tecnologías de asistencia, como lectores de pantalla.
Consulte la **Soporte técnico de asistencia** Tema de ayuda de cualquier tema de personalización de visores en la Guía de referencia de visores de Dynamic Media. Por ejemplo, consulte [Soporte técnico de asistencia](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) para el visor de vídeo, o [Soporte técnico de asistencia](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) para el visualizador de imagen interactiva.

## Compatibilidad con subtítulos en Dynamic Media {#closed-caption-support}

Dynamic Media admite la entrega de conjuntos de vídeos y vídeos adaptables con subtítulos. Los subtítulos deben mostrarse sobre el contenido del vídeo.

Consulte [Vídeo en Dynamic Media: Agregar subtítulos o subtítulos cerrados a un vídeo](/help/assets/video.md#adding-captions-to-video).

>[!MORELIKETHIS]
>
>* [Accesibilidad para soluciones de Adobe](https://www.adobe.com/accessibility.html)
>* [Accesibilidad en [!DNL Experience Manager Assets]](/help/assets/accessibility.md)

