---
title: Accesibilidad en Dynamic Media
description: Obtenga información sobre la accesibilidad en Dynamic Media y los visores de Dynamic Media
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: 696aaa54007e4a78fe6b07d8ba65660595286dca
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---


# Accesibilidad en [!DNL Dynamic Media] {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] admite tecnologías de control de teclado y asistencia, como lectores de pantalla JAWS y NVDA, en la interfaz de usuario de creación.

## Compatibilidad con la accesibilidad del teclado en [!DNL Dynamic Media]

Dado que [!DNL Dynamic Media] es un complemento para [!DNL Adobe Experience Manager Assets], la mayoría del comportamiento del control de teclado es exactamente el mismo que en [!DNL Experience Manager Assets]. Por ejemplo, el `Cancel` botón de [!DNL Dynamic Media] tiene el mismo resaltado que en [!DNL Experience Manager Assets]y reacciona a la `Spacebar` tecla como en [!DNL Experience Manager Assets]. Consulte Métodos abreviados [de teclado en Recursos](/help/assets/accessibility.md#keyboard-shortcuts).

Las pulsaciones de teclas admitidas por los elementos individuales de la interfaz de usuario [!DNL Dynamic Media] son, en la mayoría de los casos, obvias y fáciles de detectar. El control de teclado de [!DNL Dynamic Media] es de lo siguiente:

* Posibilidad de utilizar `Tab` y `Shift+Tab` pulsaciones de tecla para desplazarse entre los elementos interactivos de la página.
El uso del enfoque de entrada `Tab` avanza al siguiente elemento de interfaz de usuario en el orden de tabulación; el uso `Shift+Tab` devuelve el enfoque de entrada al elemento de interfaz de usuario anterior.
El recorrido de enfoque sigue la ubicación del elemento de interfaz de usuario natural en la pantalla y se mueve de izquierda a derecha y, a continuación, de arriba abajo. Además, si algún campo tiene un error, puede presionar `Tab` para mover el enfoque a él.
* Posibilidad de utilizar la `Spacebar` tecla y `Enter` para activar elementos de la interfaz de usuario estándar, como botones, lista desplegable, etc.
* Posibilidad de ver el resaltado del enfoque del teclado en el elemento activo. El elemento de interfaz de usuario que tiene foco de entrada puede recibir una indicación de enfoque visual como borde representado alrededor del elemento de interfaz de usuario.
* En el editor de zonas interactivas, puede utilizar algunas pulsaciones de teclas personalizadas, como las teclas de flecha, para interactuar con elementos complejos de la interfaz de usuario y cambiar la posición de las zonas interactivas.
* En el editor de vídeo interactivo, puede utilizar el `Spacebar` para seleccionar una imagen y agregarla a un segmento. Además, puede utilizar la `Backspace` tecla para eliminar el elemento seleccionado de la ficha **[!UICONTROL Contenido]** . Además, si se presionan `Tab` las funciones que se desean, se puede navegar entre los elementos interactivos de la página.
* En el editor Recorte de imagen/Recorte inteligente, puede realizar las siguientes acciones:
   * Utilice las teclas de flecha para recortar el tamaño del marco, o para cambiar la posición de la imagen, o ambas.
   * La primera `Tab` parada resalta todo el marco de la imagen. A continuación, puede utilizar las teclas de flecha del teclado para cambiar la posición del marco.
   * Las cuatro `Tab` paradas siguientes son las cuatro esquinas del marco. Cuando el enfoque se coloca en una esquina de marco, la esquina se resalta. De nuevo, puede utilizar las teclas de flecha del teclado para mover la esquina seleccionada.
Consulte [Edición del recorte inteligente o muestra inteligente de una sola imagen](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Soporte de tecnología de asistencia en [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] los elementos de la interfaz de usuario funcionan con tecnologías de asistencia, como lectores de pantalla. Por ejemplo, reconoce los puntos de referencia en una página cuando se navegan por los puntos de referencia mediante combinaciones de teclas `D` o regiones mediante combinaciones de teclas `R`. También muestra el encabezado al desplazarse mediante el método abreviado de teclado del encabezado `H`.

## Compatibilidad con la accesibilidad del teclado en [!DNL Dynamic Media] los visores {#keyboard-accessibility-for-dm-viewers}

Todos los componentes de [!DNL Dynamic Media] visores integrados admiten la accesibilidad del teclado para sus clientes.

Consulte [Navegación](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) y accesibilidad del teclado en la Guía de referencia de visores de Dynamic Media.

## Compatibilidad con tecnología de asistencia en [!DNL Dynamic Media] visores {#assistive-technology-support-for-dm-viewers}

Todos los componentes [!DNL Dynamic Media] del visor admiten funciones y atributos ARIA (Aplicaciones de Internet enriquecidas accesibles) para mejorar la integración con tecnologías de asistencia como lectores de pantalla.
Consulte el tema de ayuda sobre la compatibilidad con **la tecnología de** asistencia en cualquier tema de personalización del visor de la Guía de referencia de visores de Dynamic Media. Por ejemplo, consulte [Compatibilidad](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) con tecnología de asistencia para el visor de vídeo o Compatibilidad con [tecnología de](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) asistencia para el visor de imágenes interactivo.

>[!MORELIKETHIS]
>
>* [Accesibilidad para las soluciones de Adobe](https://www.adobe.com/accessibility.html)
>* [Accesibilidad en [!DNL Experience Manager Assets]](/help/assets/accessibility.md)

