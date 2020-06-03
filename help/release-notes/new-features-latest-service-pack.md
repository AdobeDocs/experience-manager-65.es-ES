---
title: Novedades de Adobe Experience Manager 6.5 Service Pack 5
description: Novedades de Adobe Experience Manager 6.5 Service Pack 5
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: cc423a199e860429e85895690f6c1a81c20d1a19
workflow-type: tm+mt
source-wordcount: '1853'
ht-degree: 4%

---


# Novedades de AEM 6.5 Service Pack 5 {#aem-whats-new-service-pack-5}

Los Service Packs de Adobe Experience Manager 6.5 le proporcionan nuevas funciones, mejoras solicitadas por el cliente, mejoras relacionadas con el rendimiento y la estabilidad a intervalos trimestrales. El modelo de envío trimestral facilita el acceso y la adopción de nuevas características e innovaciones.

En este artículo se destacan las funciones incluidas en el último Service Pack 6.5, las funciones [clave incluidas en los Service Pack](#key-features-previous-service-packs)6.5 anteriores y algunas de las versiones [clave desde la versión 6.5.4.0](#key-features-sice-sp3) de Experience Manager.

## AEM Sites {#aem-sites}

### Mejoras de accesibilidad {#accessibility-sites}

* Se ha mejorado el sistema de informes de errores al agregar información de texto

* Se ha mejorado el enfoque de la interfaz de usuario durante la navegación mediante el teclado

* Se ha mejorado el contraste del texto (proporción de luminosidad)

* Se ha mejorado la coherencia de los atributos alt para las imágenes de página

* Se ha mejorado la coherencia de las etiquetas de aplicaciones de Internet enriquecidas (ARIA) accesibles

* Funciones mejoradas de acceso al escritorio no visual (NVDA)

* Compatibilidad con lectores de pantalla mejorada

### Otras mejoras clave {#other-enhancements-sites}

* Al copiar o pegar un árbol de páginas, ahora tiene la opción de pegar la página raíz o la página raíz con las subpáginas del árbol.

* AEM Experience Fragments exported to Adobe Target workspaces now appear as unique offer types and offer sources in [!DNL Target].

* Administrador de varios sitios: el activador Publicar ahora elimina correctamente un componente de la página publicada si se elimina un componente de la página de origen.

* Administrador de varios sitios: cuando el nombre de un componente local en un LiveCopy es idéntico al nombre de un componente en el modelo y el componente se despliega desde el modelo, el término _msm_move se agrega ahora correctamente al nombre del componente local.

## AEM Assets {#aem-assets}

### Mejoras de accesibilidad en los recursos {#assets-accessibility}

[!DNL Adobe Experience Manager] Las funcionalidades de los recursos ahora son más accesibles de acuerdo con las Pautas de Accesibilidad al Contenido Web (WCAG). La accesibilidad ha mejorado en las siguientes áreas:

* Los elementos, controles, páginas y cuadros de diálogo de la interfaz de usuario son fáciles de leer en pantalla.

* Los elementos de la interfaz de usuario, los controles y los campos del formulario de entrada son accesibles mediante el teclado.

* Cambio de color y contraste de algunos gráficos para distinguirlos los usuarios con visión limitada y sin percepción de color. Por ejemplo, el color de los iconos de clasificación por estrellas (como en la sección [!UICONTROL Clasificación] de la ficha [!UICONTROL Avanzado] de [!UICONTROL Propiedades] del recurso o en la vista de la tarjeta) se cambia para obtener el contraste adecuado.

![se cambió el color de los iconos de clasificación por estrellas para mejorar el contraste](assets/star-rating-icons.png)

### Gestión de excepciones mejorada {#exception-handling}

El flujo de la interfaz de usuario de recursos tiene una mejor gestión de excepciones. Anteriormente, si un recurso no tenía el tipo adecuado para su dimensión, se observaba una excepción que se capturaba en silencio sin ningún seguimiento en los registros. Este comportamiento ha cambiado y todas las excepciones se capturan en registros.

## [!DNL Dynamic Media] {#dynamic-media}

### Compatibilidad con 3D en [!DNL Dynamic Media] {#support-for-3d}

La compatibilidad con 3D [!DNL Dynamic Media] ahora permite a los clientes publicar y añadir contenido 3D a páginas web y aplicaciones. Incluye:

* Publicación de formatos de recursos 3D comunes para generar una URL de recursos.

* Visualización interactiva de recursos 3D publicados mediante un nuevo visor web 3D disponible en la biblioteca [!DNL Dynamic Media] del visor, con tecnología Adobe Dimension.

* Publicación y visualización en 3D en [!DNL Experience Manager Sites] página mediante el componente [!DNL Sites] WCM.

## Formularios AEM {#aem-forms}

### Personalización de las columnas de la Bandeja de entrada de AEM {#customize-aem-inbox-columns}

Puede personalizar una bandeja de entrada de AEM para cambiar el título predeterminado de una columna, reordenar la posición de una columna y mostrar columnas adicionales basadas en los datos de un flujo de trabajo. Debe ser miembro `administrators` o `workflow-administrators` grupo para personalizar las columnas.

![Personalización de las columnas de AEM Inbox](assets/customize-columns.gif)

### Guardar comunicaciones interactivas como borrador {#save-as-draft}

Puede utilizar la interfaz de usuario del agente para guardar uno o varios borradores para cada comunicación interactiva y recuperar el borrador más adelante para continuar trabajando en él. Puede especificar un nombre diferente para cada borrador para facilitar la identificación.

![Guardar como borrador](assets/save-as-draft.gif)

### [!DNL Oracle WebLogic] compatibilidad con el servidor de aplicaciones {#weblogic-support}

AEM Forms ha añadido compatibilidad con AEM Forms [!DNL Oracle WebLogic 12] en JEE. Puede actualizar desde una versión anterior o configurar un nuevo AEM 6.5 Forms en el servidor JEE en [!DNL Oracle WebLogic] 12.2.1.4 y versiones posteriores. Posteriormente corresponde a los cambios menores de la versión, donde x en 12.2.1.x se sustituye por un número de versión.

### Mejoras de accesibilidad {#accessibility-improvements}

AEM Forms incluye las siguientes mejoras de accesibilidad:

* Cuando un usuario previsualización un formulario adaptable como un formulario HTML, el campo Firma [!UICONTROL de] garabatos conserva el enfoque de tabulación.

* Los mensajes de error que se muestran al enviar un formulario adaptable ahora contienen el `aria-describedBy` atributo. El atributo se adjunta a los campos a los que se hace referencia en el mensaje de error. El `aria-describedby` atributo indica los identificadores de los elementos que describen el objeto. Ayuda a establecer una relación entre utilidades o grupos y texto que los describa.

* Si un formulario adaptable tiene algunos campos obligatorios, el atributo obligatorio se define como `True` para dichos campos en el esquema de accesibilidad de ARIA.

### Autenticación basada en certificados X-509 para servicios Web basados en SOAP en modelo de datos de formulario {#x509-based-authentication-soap}

El modelo de datos de formulario ahora admite la autenticación basada en certificados X-509 mientras se utilizan servicios Web SOAP como origen de datos.

### Otras mejoras clave {#other-improvements}

* AEM 6.5 Forms on JEE Documento Security ahora se basa en [!DNL Apache Struts 2].

* Se Añadió la compatibilidad con [!DNL Oracle Real Applications Cluster (RAC) 19c].

## Funciones principales de los Service Packs anteriores de AEM 6.5 {#key-features-previous-service-packs}

### AEM Sites {#aem-sites-previous-service-packs}

#### Mejoras en el sistema de estilos (6.5.4.0) {#style-system-enhancements}

Ahora puede seleccionar estilos dentro del cuadro de diálogo de componentes mediante el sistema de estilos mejorado.

#### Mejoras de rendimiento en diversas áreas (6.5.4.0) {#performance-improvements}

* Se ha reducido el tiempo para cargar e inicializar ContextHub en un sitio (`contexthub.kernel.js`). Esto resulta en cargas de página más rápidas durante una visita al sitio.

* Se ha reducido el tiempo para actualizar una página después de arrastrar Fragmentos de experiencia al Editor de páginas de sitios.

* Se ha reducido el tiempo de carga de las entradas en una página Sitios con más de 200 copias activas en **[!UICONTROL Live Copy Overview]**.

* Se mejoró la administración de direcciones URL incompletas o no válidas. Estas direcciones URL pueden ralentizar el Editor de plantillas.

### AEM Assets {#aem-assets-previous-service-packs}

#### Configure AEM Assets with Brand Portal (6.5.4.0) {#configure-assets-bp}

Se ha cambiado el canal de autorización entre AEM Assets y Brand Portal. Anteriormente, Brand Portal se configuraba en la IU clásica mediante OAuth Gateway heredado, que utiliza el intercambio de tokens JWT para obtener un Token de acceso IMS para la autorización. Recursos AEM ahora se configura con Brand Portal a través de Adobe I/O, que proporciona un distintivo IMS para la autorización del inquilino de Brand Portal.

Los pasos para configurar Recursos AEM con Brand Portal son diferentes en función de la versión de AEM y de si está configurando por primera vez o actualizando las configuraciones existentes. Consulte [Configuración de AEM Assets con Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) para obtener más información.

#### Accessibility enhancements (6.5.4.0) {#accessibility-enhancements}

Experience Manager Assets incluye las siguientes mejoras de accesibilidad:

* Las teclas de flecha del teclado se pueden utilizar para mover y recorrer áreas dentro de imágenes con zoom. Para obtener más información, consulte Recursos de [previsualización utilizando únicamente](../assets/managing-assets-touch-ui.md#previewing-assets)teclas de teclado.

* Los lectores de pantalla pueden leer las casillas de verificación de estado mixto (en las que, a menos que seleccione todos los predicados anidados, las casillas de verificación de primer nivel no se seleccionan y se rompen) en el panel Filtros.

* Las restricciones de formato de fecha y hora se proporcionan en las etiquetas de campo de los campos de fecha, para permitir que los usuarios introduzcan la fecha en el formato correcto mediante el teclado.

   Por ejemplo, `On Time (MM-DD-YYYY HH:mm)`. Aquí MM es el mes en formato de dos dígitos, AAAA es el año, DD es el día en formato de dos dígitos, HH es la hora en formato militar de 24 horas y mm es el minuto.

* El símbolo `X` del botón para eliminar las etiquetas seleccionadas actualmente lo anuncian los lectores de pantalla junto con el número de etiquetas seleccionadas.

#### Búsqueda visual de AEM Assets (6.5.2.0) {#visual-search}

Los usuarios de recursos pueden buscar imágenes visualmente similares. AEM muestra las imágenes con etiquetas inteligentes del repositorio de DAM similares a una imagen seleccionada por el usuario. See [Visual search](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

#### Imágenes inteligentes para Dynamic Media {#smart-imaging}

Las imágenes inteligentes utilizan las características de visualización únicas de cada usuario para ofrecer automáticamente las imágenes correctas optimizadas para su experiencia, lo que mejora el rendimiento y la participación. Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes y utilizan la inteligencia en el último milisegundo de envío para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión de red o del navegador. Consulte Imágenes [inteligentes](../assets/imaging-faq.md).

#### Recorte inteligente en perfiles de vídeo para medios dinámicos (6.5.3.0) {#smart-crop-video}

El recorte inteligente para vídeo, una función opcional disponible en Perfiles de vídeo, es una herramienta que utiliza la potencia de la inteligencia artificial en Adobe Sensei para detectar y recortar automáticamente el punto focal en cualquier vídeo adaptable o vídeo progresivo que haya cargado, independientemente del tamaño. Consulte [Acerca del uso de recortes inteligentes en perfiles](../assets/video-profiles.md)de vídeo.

### Formularios AEM {#aem-forms-previous-service-packs}

#### Generar salida imprimible en flujos de trabajo de AEM Forms (6.5.4.0) {#generate-printable-output}

El paso de flujo de trabajo Generar salida imprimible permite integrar un archivo de plantilla de origen con un archivo de datos. Esta integración le permite imprimir o guardar diferentes copias del archivo de plantilla. El paso genera una salida PCL, PostScript, ZPL, IPL, TPCL o DPL. Para obtener más información sobre esta función, consulte Flujo de trabajo centrado en [formularios en OSGi - Referencia](../forms/using/aem-forms-workflow-step-reference.md)de pasos.

![Generar salida imprimible](assets/generate-print-output-step.gif)

#### Compatibilidad con varias columnas para formularios adaptables y comunicaciones interactivas en modo Diseño (6.5.4.0) {#multi-column-adaptive-forms}

Ahora puede definir el número de columnas para un panel en formularios adaptables y comunicaciones interactivas. Cambie al modo de diseño para utilizar la nueva opción de varias columnas. Para obtener más información, consulte [Uso del modo Diseño para cambiar el tamaño de los componentes](../forms/using/resize-using-layout-mode.md).

![Diseño de varias columnas](assets/multi-column-layout.gif)

#### Personalizaciones de la bandeja de entrada de AEM (6.5.4.0) {#aem-inbox}

La nueva opción Control de administración permite a los administradores:

* Personalización del texto y logotipo del encabezado

* Controlar la visualización de los vínculos de navegación disponibles en el encabezado

La opción Control de administración solo está visible para los miembros del grupo de administradores o administradores de flujo de trabajo. Para obtener más información sobre esta función, consulte [Su bandeja de entrada](../sites-authoring/inbox.md).

#### Compatibilidad con texto enriquecido en formularios HTML5 (6.5.4.0) {#rich-text-support}

Conversión de un campo de texto en un formulario XFA en un campo de texto enriquecido en un formulario HTML5. Para obtener más información, consulte [Diseño de plantillas de formulario para formularios](../forms/using/designing-form-template.md)HTML5.

#### Accessibility enhancements (6.5.4.0) {#forms-accessibility-enhancements-6540}

Los formularios de Experience Manager incluyen las siguientes mejoras de accesibilidad:

* Los lectores de pantalla anuncian los campos de casillas de verificación, vínculos, selector de fecha e introducción de fecha correctamente en un formulario adaptable.

* Cada página de un formulario adaptable ahora incluye un título y una etiqueta de punto de referencia principal.

#### Uso compartido y solicitud de acceso a elementos de la bandeja de entrada de un usuario de AEM Forms (6.5.3.0) {#share-request-access}

Puede compartir los elementos de la Bandeja de entrada con otro usuario. Una vez que otro usuario obtiene acceso a los elementos de la Bandeja de entrada, el usuario puede reclamar y realizar las acciones correspondientes en los elementos compartidos. Del mismo modo, puede solicitar acceso a los elementos de la Bandeja de entrada a otros usuarios. Consulte [Uso compartido y solicitud de acceso a elementos de la Bandeja de entrada de un usuario](../forms/using/configure-shared-queues-osgi.md).

#### Configuración de la configuración externa de los elementos de la Bandeja de entrada de un usuario de AEM Forms (6.5.3.0) {#configure-out-of-office}

Si planea salir de la oficina, puede especificar lo que sucede con los artículos que se le han asignado para ese período.
Tiene la opción de especificar una fecha y hora de inicio y una fecha y hora de finalización para que la configuración fuera de la oficina esté en vigor. Puede establecer una persona predeterminada a la que se enviarán todos los elementos. Consulte [Configuración fuera de la oficina](../forms/using/configure-out-of-office-settings.md).

#### Generar varias comunicaciones interactivas mediante la API por lotes para AEM Forms (6.5.3.0) {#generate-multiple-ic}

Puede utilizar la API por lotes para generar varias comunicaciones interactivas a partir de una plantilla. La plantilla es una comunicación interactiva sin datos. La API de lote combina datos con una plantilla para generar una comunicación interactiva. La API es útil en la producción masiva de comunicaciones interactivas. Por ejemplo: facturas telefónicas, extractos de tarjetas de crédito para varios clientes. Consulte [Generación de varias comunicaciones interactivas mediante la API](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)por lotes.

## Versiones clave desde AEM 6.5 SP4 {#key-releases-since-last-sp}

Entre el 05 de marzo de 2020 y el 4 de junio de 2020, Adobe lanzó las siguientes funciones que están fuera del producto principal de AEM:

* AEM Cloud Manager [2020.3.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-3-0.html), [2020.4.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-4-0.html)y [2020.5.0](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-manager/using/release-notes/release-notes-current.translate.html)

* [Recursos AEM: Desktop App 2.0.2.0](https://docs.adobe.com/content/help/es-ES/experience-manager-desktop-app/using/release-notes.html)

* [AEM Screens: Feature Pack 202004](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202004.html)

## Recursos útiles

* [Guías de usuario de AEM 6.5](../user-guide/home.md)

* [Notas de versión específicas de Adobe Experience Manager 6.5](release-notes.md)

* [Notas de la versión de Service Pack para Adobe Experience Manager 6.5](sp-release-notes.md)
