---
title: Novedades de Adobe Experience Manager 6.5 Service Pack 5
description: Novedades de Adobe Experience Manager 6.5 Service Pack 5
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 71c0d0263e1d0da7e33762a3b22773f38db3ba52
workflow-type: tm+mt
source-wordcount: '1873'
ht-degree: 3%

---


# Novedades de Adobe Experience Manager 6.5 Service Pack 5 {#aem-whats-new-service-pack-5}

Los Service Packs de Adobe Experience Manager 6.5 proporcionan nuevas funciones, mejoras solicitadas por el cliente y mejoras de rendimiento, estabilidad y seguridad a intervalos trimestrales. La disponibilidad trimestral facilita el acceso y la adopción de nuevas características e innovaciones.

Este artículo destaca las funciones incluidas en el último Service Pack 6.5, las funciones [clave incluidas en los Service Pack](#key-features-previous-service-packs)6.5 anteriores y algunas de las versiones [clave desde la versión Experience Manager 6.5.4.0](#key-releases-since-last-sp) .

## Adobe Experience Manager Sites {#aem-sites}

### Mejoras de accesibilidad {#accessibility-sites}

* Se ha mejorado el sistema de informes de errores al agregar información de texto.

* Se ha mejorado el enfoque de la interfaz de usuario durante la navegación mediante el teclado.

* Se ha mejorado la relación de contraste para varios elementos de la interfaz de usuario.

* Se ha mejorado la coherencia de los atributos alt para las imágenes de página.

* Se ha mejorado la coherencia de las etiquetas de aplicaciones de Internet enriquecidas (ARIA) accesibles.

* Se mejoraron las capacidades de acceso al escritorio no visual (NVDA).

* Se ha mejorado la compatibilidad con el lector de pantalla.

### Otras mejoras clave {#other-enhancements-sites}

* Al copiar o pegar un árbol de páginas, ahora tiene la opción de pegar la página raíz o la página raíz con las subpáginas del árbol.

* [!DNL Adobe Experience Manager Experience Fragments] exportados a [!DNL Adobe Target] espacios de trabajo ahora aparecen como tipos de oferta únicos y fuentes de oferta en [!DNL Target].

* Administrador de varios sitios: el activador Publicar ahora elimina un componente de la página publicada si se elimina un componente de la página de origen.

* Administrador de varios sitios: cuando el nombre de un componente local en una [!UICONTROL Live Copy] es idéntico al nombre de un componente en el modelo y el componente se despliega desde el modelo, el término `_msm_moved` se agrega ahora al nombre del componente local.

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

### Mejoras de accesibilidad en [!DNL Assets] {#assets-accessibility}

[!DNL Experience Manager Assets] ahora es más accesible de conformidad con las directrices de accesibilidad del contenido web (WCAG). La accesibilidad ha mejorado debido a las siguientes mejoras:

* Muchos elementos, controles, páginas y cuadros de diálogo de la interfaz de usuario son fáciles de leer en pantalla.

* Se puede acceder a muchos elementos de interfaz de usuario, controles y campos de formulario de entrada mediante el teclado.

* El color y el contraste de algunos elementos de la interfaz de usuario se actualizan para que los usuarios con visión limitada o los usuarios sin percepción del color puedan distinguir estos elementos de la interfaz de usuario. For example, the color of star rating icons (such as in [!UICONTROL Rating] section of [!UICONTROL Advanced] tab in asset [!UICONTROL Properties] or in card view) is changed for appropriate contrast.

   ![Iconos de clasificación con mejor contraste](assets/star-rating-icons.png)

### Gestión de excepciones mejorada {#exception-handling}

[!DNL Assets] el flujo de interfaz de usuario tiene una mejor gestión de excepciones. Si un recurso no tiene un tipo para su dimensión, la excepción observada se registra en los archivos de registro.

### Compatibilidad con recursos 3D en [!DNL Dynamic Media] {#support-for-3d}

La compatibilidad con imágenes 3D en [!DNL Dynamic Media] permite a los clientes publicar y añadir contenido 3D a páginas web y aplicaciones. La compatibilidad incluye:

* Publique formatos de recursos 3D comunes y genere una URL de recursos que se pueda utilizar en páginas web y otras aplicaciones.

* Un visor web 3D, con tecnología [!DNL Adobe Dimension], para realizar vistas interactivas de los recursos 3D publicados.

* Publique y vista recursos 3D comunes en [!DNL Experience Manager Sites] páginas mediante el componente [!DNL Sites] WCM.

## Adobe Experience Manager Forms {#aem-forms}

### Personalización de las columnas de la Bandeja de entrada de Adobe Experience Manager {#customize-aem-inbox-columns}

Puede personalizar una [!DNL Experience Manager] Bandeja de entrada para cambiar el título predeterminado de una columna, reordenar la posición de una columna y mostrar columnas adicionales basadas en los datos de un flujo de trabajo. Los miembros del `administrators` grupo o del `workflow-administrators` grupo pueden personalizar las columnas. Para obtener más información, consulte Control [de administración](../sites-authoring/inbox.md#inbox-admin-control).

![Personalizar las columnas de la Bandeja de entrada Experience Manager](assets/customize-columns.gif)

### Guardar comunicaciones interactivas como borrador {#save-as-draft}

Puede utilizar la interfaz de usuario del agente para guardar uno o varios borradores para cada comunicación interactiva y recuperar el borrador más adelante para continuar trabajando en él. Puede especificar un nombre diferente para cada borrador para identificarlo. Para obtener más información, consulte [Guardar comunicaciones interactivas como borrador](../forms/using/prepare-send-interactive-communication.md#save-as-draft).

![Guardar como borrador](assets/save-as-draft.gif)

### [!DNL Oracle WebLogic] compatibilidad con el servidor de aplicaciones {#weblogic-support}

Adobe Experience Manager Forms ha agregado compatibilidad con [!DNL Oracle WebLogic 12] formularios Adobe Experience Manager en JEE. Puede actualizar desde una versión anterior o configurar un nuevo Experience Manager 6.5 Forms en el servidor JEE en [!DNL Oracle WebLogic] 12.2.1.4 y versiones posteriores. Posteriormente corresponde a los cambios menores de la versión, donde x en 12.2.1.x se sustituye por un número de versión.

### Mejoras de accesibilidad {#accessibility-improvements}

Adobe Experience Manager Forms incluye las siguientes mejoras de accesibilidad:

* Cuando un usuario previsualización un formulario adaptable como un formulario HTML, el campo Firma [!UICONTROL de] garabatos conserva el enfoque de tabulación.

* Los mensajes de error que se muestran al enviar un formulario adaptable ahora contienen el `aria-describedBy` atributo. El atributo se adjunta a los campos a los que se hace referencia en el mensaje de error. El `aria-describedby` atributo indica los identificadores de los elementos que describen el objeto. Ayuda a establecer una relación entre utilidades o grupos y texto que los describa.

* Si un formulario adaptable tiene algunos campos obligatorios, el atributo obligatorio se define como `True` para dichos campos en el esquema de accesibilidad de ARIA.

### Autenticación basada en certificados X-509 para servicios Web basados en SOAP en modelo de datos de formulario {#x509-based-authentication-soap}

El modelo de datos de formulario ahora admite la autenticación basada en certificados X-509 mientras se utilizan servicios Web SOAP como origen de datos. Para obtener más información, consulte [Configuración de servicios](../forms/using/configure-data-sources.md#configure-soap-web-services)web SOAP.

### Otras mejoras clave {#other-improvements}

* Experience Manager 6.5 Forms on JEE Documento Security se basa ahora en [!DNL Apache Struts 2].

* Se Añadió la compatibilidad con [!DNL Oracle Real Applications Cluster (RAC) 19c].

## Características principales de los Service Packs anteriores de Experience Manager 6.5 {#key-features-previous-service-packs}

### Experience Manager Sites {#aem-sites-previous-service-packs}

#### Mejoras en el sistema de estilos (6.5.4.0) {#style-system-enhancements}

Ahora puede seleccionar estilos dentro del cuadro de diálogo de componentes mediante el sistema de estilos mejorado.

#### Mejoras de rendimiento en diversas áreas (6.5.4.0) {#performance-improvements}

* Se ha reducido el tiempo para cargar e inicializar ContextHub dentro de un sitio (`contexthub.kernel.js`). Esto resulta en cargas de página más rápidas durante una visita al sitio.

* Se ha reducido el tiempo para actualizar una página después de arrastrarla [!DNL Experience Fragments] al Editor [!DNL Sites] de páginas.

* Se ha reducido el tiempo de carga de las entradas de una [!DNL Sites] página con más de 200 copias activas en **[!UICONTROL Live Copy Overview]**.

* Se mejoró la administración de direcciones URL incompletas o no válidas. Estas direcciones URL pueden ralentizar el Editor de plantillas.

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

#### Configurar [!DNL Experience Manager Assets] con [!DNL Brand Portal] (6.5.4.0) {#configure-assets-bp}

Se cambia el canal de autorización entre [!DNL Experience Manager Assets] y [!DNL Brand Portal] . Anteriormente, [!DNL Brand Portal] se configuraba en la IU clásica mediante OAuth Gateway heredado, que utiliza el intercambio de tokens JWT para obtener un Token de acceso IMS para la autorización. [!DNL Experience Manager Assets] ahora se configura con [!DNL Brand Portal] mediante Adobe I/O, que obtiene un testigo IMS para la autorización de su [!DNL Brand Portal] inquilino.

Los pasos para configurar [!DNL Experience Manager Assets] con [!DNL Brand Portal] son diferentes en función de su [!DNL Experience Manager] versión, y de si está configurando por primera vez o actualizando las configuraciones existentes. Consulte [Configuración de recursos de Experience Manager con Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) para obtener más información.

#### Accessibility enhancements (6.5.4.0) {#accessibility-enhancements}

[!DNL Experience Manager Assets] incluye las siguientes mejoras de accesibilidad:

* Las teclas de flecha del teclado se pueden utilizar para mover y recorrer áreas dentro de imágenes con zoom. Para obtener más información, consulte Recursos de [previsualización utilizando únicamente](../assets/managing-assets-touch-ui.md#previewing-assets)teclas de teclado.

* Los lectores de pantalla pueden leer las casillas de verificación de estado mixto (en las que, a menos que seleccione todos los predicados anidados, las casillas de verificación de primer nivel no se seleccionan y se rompen) en el panel Filtros.

* Las restricciones de formato de fecha y hora se proporcionan en las etiquetas de campo de los campos de fecha, para permitir que los usuarios introduzcan la fecha en el formato correcto mediante el teclado.
Por ejemplo, `On Time (MM-DD-YYYY HH:mm)`. Aquí MM es el mes en formato de dos dígitos, AAAA es el año, DD es el día en formato de dos dígitos, HH es la hora en formato militar de 24 horas y mm es el minuto.

* Los lectores de pantalla ahora anuncian el `X` símbolo para eliminar las etiquetas seleccionadas junto con el número de etiquetas seleccionadas.

#### Búsqueda visual [!DNL Adobe Experience Manager Assets] (6.5.2.0) {#visual-search}

[!DNL Assets] los usuarios pueden buscar imágenes visualmente similares. Experience Manager muestra las imágenes con etiquetas inteligentes del repositorio de DAM que son similares a una imagen seleccionada por el usuario. See [Visual search](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

#### Imágenes inteligentes para Dynamic Media {#smart-imaging}

Las imágenes inteligentes utilizan las características de visualización únicas de cada usuario para ofrecer automáticamente las imágenes correctas optimizadas para su experiencia, lo que mejora el rendimiento y la participación. Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes y utilizan la inteligencia en el último milisegundo de envío para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión de red o del navegador. Consulte Imágenes [inteligentes](../assets/imaging-faq.md).

#### Recorte inteligente en perfiles de vídeo para Dynamic Media (6.5.3.0) {#smart-crop-video}

El recorte inteligente para vídeo, una función opcional disponible en Perfiles de vídeo, es una herramienta que utiliza la potencia de la inteligencia artificial en Adobe Sensei para detectar y recortar automáticamente el punto focal en cualquier vídeo adaptable o vídeo progresivo que haya cargado, independientemente del tamaño. Consulte [Acerca del uso de recortes inteligentes en perfiles](../assets/video-profiles.md)de vídeo.

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### Generar salida imprimible en flujos de trabajo de formularios Experience Manager (6.5.4.0) {#generate-printable-output}

El paso de flujo de trabajo Generar salida imprimible permite integrar un archivo de plantilla de origen con un archivo de datos. Esta integración le permite imprimir o guardar diferentes copias del archivo de plantilla. El paso genera una salida PCL, PostScript, ZPL, IPL, TPCL o DPL. Para obtener más información sobre esta función, consulte Flujo de trabajo centrado en [formularios en OSGi - Referencia](../forms/using/aem-forms-workflow-step-reference.md)de pasos.

![Generar salida imprimible](assets/generate-print-output-step.gif)

#### Compatibilidad con múltiples columnas para formularios adaptables y comunicaciones interactivas en modo Diseño (6.5.4.0) {#multi-column-adaptive-forms}

Ahora puede definir el número de columnas para un panel en formularios adaptables y comunicaciones interactivas. Cambie al modo de diseño para utilizar la nueva opción de varias columnas. Para obtener más información, consulte [Uso del modo Diseño para cambiar el tamaño de los componentes](../forms/using/resize-using-layout-mode.md).

![Diseño de varias columnas](assets/multi-column-layout.gif)

#### Personalizaciones de la bandeja de entrada de Experience Manager (6.5.4.0) {#aem-inbox}

La nueva opción Control de administración permite a los administradores:

* Personalice el texto y el logotipo del encabezado.

* Controle la visualización de los vínculos de navegación disponibles en el encabezado.

La opción Control de administración solo está visible para los miembros del `administrators` grupo o `workflow-administrators` grupo. Para obtener más información sobre esta función, consulte [Su bandeja de entrada](../sites-authoring/inbox.md).

#### Compatibilidad con texto enriquecido en formularios HTML5 (6.5.4.0) {#rich-text-support}

Conversión de un campo de texto en un formulario XFA en un campo de texto enriquecido en un formulario HTML5. Para obtener más información, consulte [Diseño de plantillas de formulario para formularios](../forms/using/designing-form-template.md)HTML5.

#### Accessibility enhancements (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms incluye las siguientes mejoras de accesibilidad:

* Los lectores de pantalla anuncian los campos de casillas de verificación, vínculos, selector de fecha e introducción de fecha correctamente en un formulario adaptable.

* Cada página de un formulario adaptable ahora incluye un título y una etiqueta de punto de referencia principal.

#### Compartir y solicitar acceso a elementos de la Bandeja de entrada de un usuario de formularios Experience Manager (6.5.3.0) {#share-request-access}

Puede compartir los elementos de la Bandeja de entrada con otro usuario. Una vez que otro usuario obtiene acceso a los elementos de la Bandeja de entrada, el usuario puede reclamar y realizar las acciones correspondientes en los elementos compartidos. Del mismo modo, puede solicitar acceso a los elementos de la Bandeja de entrada a otros usuarios. Consulte [Uso compartido y solicitud de acceso a elementos de la Bandeja de entrada de un usuario](../forms/using/configure-shared-queues-osgi.md).

#### Configuración de la configuración externa de los elementos de la Bandeja de entrada de un usuario AEM Forms (6.5.3.0) {#configure-out-of-office}

Si planea salir de la oficina, puede especificar lo que sucede con los artículos que se le han asignado para ese período.
Tiene la opción de especificar una fecha y hora de inicio y una fecha y hora de finalización para que la configuración fuera de la oficina esté en vigor. Puede establecer una persona predeterminada a la que se enviarán todos los elementos. Consulte [Configuración fuera de la oficina](../forms/using/configure-out-of-office-settings.md).

#### Generar varias comunicaciones interactivas mediante la API por lotes para AEM Forms (6.5.3.0) {#generate-multiple-ic}

Puede utilizar la API por lotes para generar varias comunicaciones interactivas a partir de una plantilla. La plantilla es una comunicación interactiva sin datos. La API de lote combina datos con una plantilla para generar una comunicación interactiva. La API es útil en la producción masiva de comunicaciones interactivas. Por ejemplo: facturas telefónicas, extractos de tarjetas de crédito para varios clientes. Consulte [Generación de varias comunicaciones interactivas mediante la API](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)por lotes.

## Versiones clave desde Adobe Experience Manager 6.5 SP4 {#key-releases-since-last-sp}

Entre el 5 de marzo de 2020 y el 4 de junio de 2020, Adobe lanzó lo siguiente, además de los Service Packs y los paquetes de correcciones acumulativos:

* [El portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) de distribución de software está disponible para descargar paquetes de servicios de Experience Manager, paquetes de correcciones acumulativos, correcciones rápidas y paquetes de funciones.

* [!DNL Adobe Experience Manager Cloud Manager] [2020.3.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-3-0.html), [2020.4.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-4-0.html)y [2020.5.0](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-manager/using/release-notes/release-notes-current.translate.html).

* [Aplicación de escritorio Experience Manager 2.0.2.0](https://docs.adobe.com/content/help/es-ES/experience-manager-desktop-app/using/release-notes.html).

* [Pantallas de Experience Manager: Feature Pack 202004](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202004.html).

>[!MORELIKETHIS]
>
>* [Documentación de Adobe Experience Manager 6.5](../user-guide/home.md)
>* [Notas generales de la versión de Adobe Experience Manager 6.5](release-notes.md)
>* [Notas de la versión del Service Pack para Adobe Experience Manager 6.5](sp-release-notes.md)

