---
title: Novedades de Adobe Experience Manager 6.5 Service Pack 4
description: Novedades de Adobe Experience Manager 6.5 Service Pack 4
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Novedades de Adobe Experience Manager 6.5 Service Pack 4 {#aem-whats-new-service-pack-4}

Adobe Experience Manager (6.5) le permite acceder a nuevas funciones y mejoras continuas mediante las versiones trimestrales de Service Pack. Con este enfoque, se pueden adoptar las innovaciones fácilmente.

Experience Manager Service Pack 4 (6.5.4.0) es una actualización importante. Incluye todas las nuevas funciones, las mejoras clave solicitadas por el cliente, el rendimiento, la estabilidad y las mejoras de seguridad lanzadas desde la versión AEM 6.5 de abril de 2019. Puede instalar el Service Pack en AEM 6.5 y versiones posteriores.

En este artículo se destacan las funciones incluidas en el último Service Pack 6.5, las funciones [clave incluidas en los Service Pack](#key-features-previous-service-packs)6.5 anteriores y algunas de las versiones [clave desde Experience Manager 6.5.3.0](#key-features-sice-sp3).

## AEM Sites {#aem-sites}

### Mejoras del sistema de estilos

Ahora puede seleccionar estilos dentro del cuadro de diálogo de componentes mediante el sistema de estilos mejorado.

### Mejoras en el rendimiento en diversas esferas {#performance-improvements}

* Se ha reducido el tiempo para cargar e inicializar ContextHub en un sitio (`contexthub.kernel.js`). Esto resulta en cargas de página más rápidas durante una visita al sitio.

* Se ha reducido el tiempo para actualizar una página después de arrastrar Fragmentos de experiencia al Editor de páginas de sitios.

* Se ha reducido el tiempo de carga de las entradas en una página Sitios con más de 200 copias activas en **[!UICONTROL Live Copy Overview]**.

* Se mejoró la administración de direcciones URL incompletas o no válidas. Estas direcciones URL pueden ralentizar el Editor de plantillas.

## AEM Assets {#aem-assets}

### Configurar AEM Assets con Brand Portal {#configure-assets-bp}

Se ha cambiado el canal de autorización entre AEM Assets y Brand Portal. Anteriormente, Brand Portal se configuraba en la IU clásica mediante OAuth Gateway heredado, que utiliza el intercambio de tokens JWT para obtener un Token de acceso IMS para la autorización. Recursos AEM ahora se configura con Brand Portal a través de Adobe I/O, que proporciona un distintivo IMS para la autorización del inquilino de Brand Portal.

Los pasos para configurar Recursos AEM con Brand Portal son diferentes en función de la versión de AEM y de si está configurando por primera vez o actualizando las configuraciones existentes. Consulte [Configuración de AEM Assets con Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) para obtener más información.


### Problemas conocidos {#known-issues-bp}

* Los usuarios de Brand Portal no pueden publicar recursos de carpetas de contribución en Recursos AEM al actualizar a Adobe I/O en AEM 6.5.4.

### Accessibility enhancements {#accessibility-enhancements}

Experience Manager Assets incluye las siguientes mejoras de accesibilidad:

* Las teclas de flecha del teclado se pueden utilizar para mover y recorrer áreas dentro de imágenes con zoom. Para obtener más información, consulte Recursos de [previsualización utilizando únicamente](../assets/managing-assets-touch-ui.md#previewing-assets)teclas de teclado.

* Los lectores de pantalla pueden leer las casillas de verificación de estado mixto (en las que, a menos que seleccione todos los predicados anidados, las casillas de verificación de primer nivel no se seleccionan y se rompen) en el panel Filtros.

* Las restricciones de formato de fecha y hora se proporcionan en las etiquetas de campo de los campos de fecha, para permitir que los usuarios introduzcan la fecha en el formato correcto mediante el teclado.

   Por ejemplo, `On Time (MM-DD-YYYY HH:mm)`. Aquí MM es el mes en formato de dos dígitos, AAAA es el año, DD es el día en formato de dos dígitos, HH es la hora en formato militar de 24 horas y mm es el minuto.

* El símbolo `X` del botón para eliminar las etiquetas seleccionadas actualmente lo anuncian los lectores de pantalla junto con el número de etiquetas seleccionadas.

## Formularios AEM {#aem-forms}

### Generar salida imprimible en flujos de trabajo de AEM Forms {#generate-printable-output}

El paso de flujo de trabajo Generar salida imprimible permite integrar un archivo de plantilla de origen con un archivo de datos. Esta integración le permite imprimir o guardar diferentes copias del archivo de plantilla. El paso genera una salida PCL, PostScript, ZPL, IPL, TPCL o DPL. Para obtener más información sobre esta función, consulte Flujo de trabajo centrado en [formularios en OSGi - Referencia](../forms/using/aem-forms-workflow-step-reference.md)de pasos.

![Generar salida imprimible](assets/generate-print-output-step.gif)

### Compatibilidad con varias columnas para formularios adaptables y comunicaciones interactivas en el modo Diseño {#multi-column-adaptive-forms}

Ahora puede definir el número de columnas para un panel en formularios adaptables y comunicaciones interactivas. Cambie al modo de diseño para utilizar la nueva opción de varias columnas. Para obtener más información, consulte [Uso del modo Diseño para cambiar el tamaño de los componentes](../forms/using/resize-using-layout-mode.md).

![Diseño de varias columnas](assets/multi-column-layout.gif)

### Personalizaciones de la bandeja de entrada de AEM {#aem-inbox}

La nueva opción Control de administración permite a los administradores:

* Personalización del texto y logotipo del encabezado

* Controlar la visualización de los vínculos de navegación disponibles en el encabezado

La opción Control de administración solo está visible para los miembros del grupo de administradores o administradores de flujo de trabajo. Para obtener más información sobre esta función, consulte [Su bandeja de entrada](../sites-authoring/inbox.md).

### Compatibilidad con texto enriquecido en formularios HTML5 {#rich-text-support}

Conversión de un campo de texto en un formulario XFA en un campo de texto enriquecido en un formulario HTML5. Para obtener más información, consulte [Diseño de plantillas de formulario para formularios](../forms/using/designing-form-template.md)HTML5.

### Accessibility enhancements {#forms-accessibility-enhancements-6540}

Los formularios de Experience Manager incluyen las siguientes mejoras de accesibilidad:

* Los lectores de pantalla anuncian los campos de casillas de verificación, vínculos, selector de fecha e introducción de fecha correctamente en un formulario adaptable.

* Cada página de un formulario adaptable ahora incluye un título y una etiqueta de punto de referencia principal.

## Funciones principales de los Service Packs anteriores de AEM 6.5 {#key-features-previous-service-packs}

### Imágenes inteligentes para Dynamic Media {#smart-imaging}

Las imágenes inteligentes utilizan las características de visualización únicas de cada usuario para ofrecer automáticamente las imágenes correctas optimizadas para su experiencia, lo que mejora el rendimiento y la participación. Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes y utilizan la inteligencia en el último milisegundo de envío para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión de red o del navegador. Consulte Imágenes [inteligentes](../assets/imaging-faq.md).

### Recorte inteligente en perfiles de vídeo para medios dinámicos (6.5.3.0) {#smart-crop-video}

El recorte inteligente para vídeo, una función opcional disponible en Perfiles de vídeo, es una herramienta que utiliza la potencia de la inteligencia artificial en Adobe Sensei para detectar y recortar automáticamente el punto focal en cualquier vídeo adaptable o vídeo progresivo que haya cargado, independientemente del tamaño. Consulte [Acerca del uso de recortes inteligentes en perfiles](../assets/video-profiles.md)de vídeo.

### Búsqueda visual de AEM Assets (6.5.2.0) {#visual-search}

Los usuarios de recursos pueden buscar imágenes visualmente similares. AEM muestra las imágenes con etiquetas inteligentes del repositorio de DAM similares a una imagen seleccionada por el usuario. See [Visual search](../assets/search-assets.md).

### Uso compartido y solicitud de acceso a elementos de la bandeja de entrada de un usuario de AEM Forms (6.5.3.0) {#share-request-access}

Puede compartir los elementos de la Bandeja de entrada con otro usuario. Una vez que otro usuario obtiene acceso a los elementos de la Bandeja de entrada, el usuario puede reclamar y realizar las acciones correspondientes en los elementos compartidos. Del mismo modo, puede solicitar acceso a los elementos de la Bandeja de entrada a otros usuarios. Consulte [Uso compartido y solicitud de acceso a elementos de la Bandeja de entrada de un usuario](../forms/using/configure-shared-queues-osgi.md).

### Configuración de la configuración externa de los elementos de la Bandeja de entrada de un usuario de AEM Forms (6.5.3.0) {#configure-out-of-office}

Si planea salir de la oficina, puede especificar lo que sucede con los artículos que se le han asignado para ese período.
Tiene la opción de especificar una fecha y hora de inicio y una fecha y hora de finalización para que la configuración fuera de la oficina esté en vigor. Puede establecer una persona predeterminada a la que se enviarán todos los elementos. Consulte [Configuración fuera de la oficina](../forms/using/configure-out-of-office-settings.md).

### Generar varias comunicaciones interactivas mediante la API por lotes para AEM Forms (6.5.3.0) {#generate-multiple-ic}

Puede utilizar la API por lotes para generar varias comunicaciones interactivas a partir de una plantilla. La plantilla es una comunicación interactiva sin datos. La API de lote combina datos con una plantilla para generar una comunicación interactiva. La API es útil en la producción masiva de comunicaciones interactivas. Por ejemplo: facturas telefónicas, extractos de tarjetas de crédito para varios clientes. Consulte [Generación de varias comunicaciones interactivas mediante la API](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)por lotes.

## Versiones clave desde AEM 6.5 SP3 {#key-features-since-sp3}

Entre el 12 de diciembre de 2019 y el 5 de marzo de 2020, Adobe lanzó las siguientes funciones que están fuera del producto principal de AEM:

* AEM Cloud Manager 2020.1.0 y 2020.2.0

   Mejore el estado de la canalización y la capacidad de descargar registros para varios pasos. Consulte:

   * [Cloud Manager 2020.1.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-1-0.html)


   * [Cloud Manager 2020.2.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-2-0.html)


* Actualizaciones de CLI de AEM Cloud Manager

   Automatice las tareas de Cloud Manager con la herramienta de línea de comandos. Consulte [GitHub](https://github.com/adobe/aio-cli-plugin-cloudmanager/releases).

* Sitios AEM: Arquetipo de proyecto 23

   La mejor forma de inicio de un nuevo proyecto de AEM. Archetype 23 combina el arquetipo [del proyecto para SPA y sitios regulares en uno](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-23) y proporciona un tema predeterminado para dar inicio a su desarrollo front-end.

* Sitios AEM: Sitio de referencia WKND

   [Nuevo proyecto](https://www.wknd.site/) de referencia con prácticas recomendadas sobre cómo crear sitios con AEM. Obtenga más información leyendo el tutorial [](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)WKND actualizado. Puede tomar el código más reciente de [GitHub](https://github.com/adobe/aem-guides-wknd/releases).

* Sitios AEM: Componentes principales de Commerce CIF 0.7.0 y 0.9.0

   Integre AEM Sites con Magento Commerce. Consulte [Ampliación de los componentes principales dedicados y del arquetipo de proyecto con enfoque en Comercio](https://github.com/adobe/aem-core-cif-components/releases).

* Recursos AEM: Desktop App 2.0.1.1

   Consulte [Obtener acceso de escritorio a los recursos](https://docs.adobe.com/content/help/es-ES/experience-manager-desktop-app/using/release-notes.html).

* AEM Screens: Feature Pack 202001

   Digital Signage directamente desde AEM. Instale las mejoras con el último Feature Pack para [activar la reproducción sincrónica en varios reproductores](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html)multimedia.

## Recursos útiles

* [Guías de usuario de AEM 6.5](../user-guide/home.md)

* [Notas de versión específicas de Adobe Experience Manager 6.5](release-notes.md)

* [Notas de la versión de Service Pack para Adobe Experience Manager 6.5](sp-release-notes.md)
