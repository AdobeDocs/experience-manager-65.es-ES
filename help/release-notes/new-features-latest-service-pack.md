---
title: Novedades de Adobe Experience Manager 6.5 Service Pack 7
description: Novedades de Adobe Experience Manager 6.5 Service Pack 7
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 55ef8af25887a59d9d13275645c1ec20f0c49380
workflow-type: tm+mt
source-wordcount: '2807'
ht-degree: 1%

---


# Novedades de Adobe Experience Manager 6.5 Service Pack 7 {#aem-whats-new-service-pack}

![Novedades](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] Los Service Packs 6.5 proporcionan nuevas funciones, mejoras solicitadas por el cliente y mejoras de rendimiento, estabilidad y seguridad a intervalos trimestrales. La disponibilidad trimestral facilita el acceso y la adopción de nuevas características e innovaciones.

Este artículo resalta las características incluidas en el Service Pack 6.5 más reciente, [características clave incluidas en los Service Pack 6.5 anteriores](#key-features-previous-service-packs) y las [versiones de AEM clave desde la última versión del Service Pack](#key-releases-since-last-sp).

## Adobe [!DNL Experience Manager Sites] {#aem-sites}

### Ordenar las páginas de Live Copy disponibles para la implementación {#sort-livecopy-pages}

Ahora puede ordenar las páginas de Live Copy disponibles para la implementación con las propiedades [!UICONTROL Name], [!UICONTROL Last modified date] y [!UICONTROL Last rollout date]. La [!UICONTROL última fecha de implementación] de una página es una nueva propiedad introducida en esta versión.

### Disponibilidad de movimientos de página e implementaciones de MSM como operaciones asincrónicas {#page-moves-msm-asynchronous}

Ahora puede realizar los movimientos de página y los despliegues de MSM como operaciones asincrónicas para reducir su impacto en el rendimiento del tiempo de ejecución. Puede programar las operaciones para su ejecución inmediata o posterior. El estado de los trabajos y pasos de proceso asociados se muestra en una consola, lo que resulta útil para supervisar los lanzamientos de MSM a gran escala.

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* [!DNL Assets] y  [!DNL Dynamic Media] proporcionar varias mejoras de accesibilidad. Las mejoras están relacionadas con la navegación mediante el teclado, el uso de lectores de pantalla y mejoras similares para permitir el uso de tecnologías de asistencia (AT). Consulte [[!DNL Assets] mejoras](/help/release-notes/sp-release-notes.md#assets-6570) y [[!DNL Dynamic Media] mejoras](/help/release-notes/sp-release-notes.md#dynamic-media-6570).

* Los usuarios pueden ordenar recursos digitales en vistas de tarjetas y columnas.

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>[!DNL Experience Manager Forms] los paquetes de complementos están disponibles una semana después del lanzamiento programado de  [!DNL Experience Manager] Service Pack.

### Mejoras de rendimiento {#performance-improvements-forms}

[!DNL Experience Manager] 6.5 Service Pack 7 Forms mejora el rendimiento de:

* Validando los valores de campo en el servidor al enviar un formulario adaptable.

* Conversión de un formulario PDF a un formulario adaptable mediante [!DNL Automated Forms Conversion service].

### Modelo de datos de formulario Configuración de cliente HTTP para optimizar el rendimiento {#fdm-http-client-config}

[!DNL Experience Manager Forms] modelo de datos de formulario al integrarse con los servicios web RESTful como origen de datos ahora incluye configuraciones de cliente HTTP para la optimización del rendimiento.

### Disponibilidad de la opción Restablecer para cada componente en el modo Diseño {#reset-option-layout-mode}

Ahora puede utilizar la opción de restablecimiento para cada componente en el modo Diseño de un formulario adaptable. Al definir un diseño de varias columnas para un panel, puede utilizar esta función para restablecer componentes individuales dentro del panel.

## Características clave de los paquetes de servicios [!DNL Experience Manager] 6.5 anteriores {#key-features-previous-service-packs}

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### Disponibilidad de la operación de Movimiento de página en modo asincrónico (6.5.6.0) {#page-move-asynchronous}

La operación de movimiento de página ahora está disponible en modo asincrónico. Además de la ejecución inmediata, también puede programar la operación Movimiento de página para que se ejecute más tarde.

#### Mejoras de accesibilidad (6.5.5.0) {#accessibility-sites}

* Se ha mejorado el sistema de informes de errores al agregar información de texto.

* Se ha mejorado el enfoque de la interfaz de usuario durante la navegación mediante el teclado.

* Se ha mejorado la relación de contraste para varios elementos de la interfaz de usuario.

* Se ha mejorado la coherencia de los atributos alt para las imágenes de página.

* Se ha mejorado la coherencia de las etiquetas de aplicaciones de Internet enriquecidas (ARIA) accesibles.

* Se mejoraron las capacidades de acceso al escritorio no visual (NVDA).

* Se ha mejorado la compatibilidad con el lector de pantalla.

#### Otras mejoras clave (6.5.5.0) {#other-enhancements-sites}

* No se permite el acceso anónimo al CRXDE Lite para aumentar la seguridad. En su lugar, se dirige a los usuarios a la pantalla de inicio de sesión. Consulte [Desarrollo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* Al copiar o pegar un árbol de páginas, ahora tiene la opción de pegar la página raíz o la página raíz con las subpáginas del árbol.

* [!DNL Adobe Experience Manager Experience Fragments] exportados a  [!DNL Adobe Target] espacios de trabajo ahora aparecen como tipos de oferta únicos y fuentes de oferta en  [!DNL Target].

* Administrador de varios sitios: el activador Publicar ahora elimina un componente de la página publicada si se elimina un componente de la página de origen.

* Administrador de múltiples sitios: cuando el nombre de un componente local en una [!UICONTROL Live Copy] es idéntico al nombre de un componente en el modelo y el componente se despliega desde el modelo, el término `_msm_moved` ahora se agrega al nombre del componente local.

#### Mejoras en el sistema de estilos (6.5.4.0) {#style-system-enhancements}

Ahora puede seleccionar estilos dentro del cuadro de diálogo de componentes mediante el sistema de estilos mejorado.

#### Mejoras en el rendimiento en diversas áreas (6.5.4.0) {#performance-improvements}

* Se ha reducido el tiempo para cargar e inicializar ContextHub en un sitio (`contexthub.kernel.js`). Esto resulta en cargas de página más rápidas durante una visita al sitio.

* Se ha reducido el tiempo para actualizar una página después de arrastrar [!DNL Experience Fragments] al [!DNL Sites] Editor de páginas.

* Se ha reducido el tiempo de carga de las entradas en una página [!DNL Sites] con más de 200 copias activas en **[!UICONTROL Live Copy Overview]**.

* Se mejoró la administración de direcciones URL incompletas o no válidas. Estas direcciones URL pueden ralentizar el Editor de plantillas.

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

#### Mejoras de accesibilidad (6.5.6.0) {#accessibility-assets-6560}

* **Se ha mejorado el enfoque de la interfaz de usuario durante la navegación** mediante el teclado, por ejemplo, centrándose en:

   * `x` en el cuadro de diálogo  [!UICONTROL Vista previa de ] versión de un recurso en la  [!UICONTROL línea de tiempo].

   * Opciones de interfaz de usuario procesables.

   * Campo de correo electrónico en el cuadro de diálogo [!UICONTROL Vínculo compartido] y campo para agregar un grupo de usuarios cerrado en la ficha [!UICONTROL Permiso] de la carpeta [!UICONTROL Propiedades].

* **Funcionalidad mejorada con las teclas del teclado**

   Los usuarios pueden utilizar las teclas del teclado para arrastrar los controles en el editor de formularios de Esquema de metadatos en el modo de exploración del lector de pantalla.

* **Se ha mejorado el uso para los usuarios** de lectores de pantalla debido a lo siguiente:

   * Los lectores de pantalla anuncian el propósito de los reproductores de audio y vídeo.

   * Los lectores de pantalla anuncian el propósito de las opciones de la interfaz de usuario para eliminar las etiquetas seleccionadas mediante [!UICONTROL cuadro de diálogo de selección de etiquetas] en el recurso [!UICONTROL Propiedades].

   * Los lectores de pantalla anuncian los encabezados de fila y los elementos de fila de las tablas para que los usuarios sepan qué entradas pertenecen a la misma fila.

   * Título de página descriptivo y significativo de la página de búsqueda.

   * Los lectores de pantalla anuncian las opciones del panel de filtros de búsqueda como acordeones ampliables.

#### Otras mejoras en [!DNL Assets] (6.5.6.0) {#other-enhancements-assets-6560}

* Los grupos de usuarios asociados con carpetas (privadas y no privadas) ahora se eliminan del repositorio al [eliminar dichas carpetas](/help/assets/private-folder.md#delete-private-folder). Sin embargo, los grupos de usuarios redundantes, huérfanos, no utilizados y autogenerados existentes pueden eliminarse del repositorio mediante JMX.

#### Mejoras de accesibilidad en [!DNL Assets] (6.5.5.0) {#assets-accessibility}

[!DNL Experience Manager Assets] ahora es más accesible de conformidad con las directrices de accesibilidad del contenido web (WCAG). La accesibilidad ha mejorado debido a las siguientes mejoras:

* Muchos elementos, controles, páginas y cuadros de diálogo de la interfaz de usuario son fáciles de leer en pantalla.

* Se puede acceder a muchos elementos de interfaz de usuario, controles y campos de formulario de entrada mediante el teclado.

* El color y el contraste de algunos elementos de la interfaz de usuario se actualizan para que los usuarios con visión limitada o los usuarios sin percepción del color puedan distinguir estos elementos de la interfaz de usuario. Por ejemplo, el color de los iconos de clasificación por estrellas (como en la sección [!UICONTROL Clasificación] de la ficha [!UICONTROL Avanzado] del recurso [!UICONTROL Propiedades] o en la vista de la tarjeta) se cambia para obtener el contraste adecuado.

   ![Iconos de clasificación con mejor contraste](assets/star-rating-icons.png)

#### Gestión de excepciones mejorada (6.5.5.0) {#exception-handling}

[!DNL Assets] el flujo de interfaz de usuario tiene una mejor gestión de excepciones. Si un recurso no tiene un tipo para su dimensión, la excepción observada se registra en los archivos de registro.

#### Compatibilidad con activos 3D en [!DNL Dynamic Media] (6.5.5.0) {#support-for-3d}

La compatibilidad con imágenes 3D en [!DNL Dynamic Media] permite a los clientes publicar y agregar contenido 3D a páginas web y aplicaciones. La compatibilidad incluye:

* Publique formatos de recursos 3D comunes y genere una URL de recursos que se pueda utilizar en páginas web y otras aplicaciones.

* Visor web 3D, con tecnología [!DNL Adobe Dimension], para realizar vistas interactivas de los recursos 3D publicados.

* Publique y vista recursos 3D comunes en páginas [!DNL Experience Manager Sites] mediante el componente [!DNL Sites] WCM.

#### Configurar [!DNL Experience Manager Assets] con [!DNL Brand Portal] (6.5.4.0) {#configure-assets-bp}

Se cambia el canal de autorización entre [!DNL Experience Manager Assets] y [!DNL Brand Portal]. Anteriormente, [!DNL Brand Portal] se configuraba en la IU clásica mediante OAuth Gateway heredado, que utiliza el intercambio de tokens JWT para obtener un Token de acceso IMS para la autorización. [!DNL Experience Manager Assets] ahora se configura  [!DNL Brand Portal] mediante Adobe I/O, que obtiene un testigo IMS para la autorización de su  [!DNL Brand Portal] inquilino.

Los pasos para configurar [!DNL Experience Manager Assets] con [!DNL Brand Portal] son diferentes en función de su versión [!DNL Experience Manager] y de si está configurando por primera vez o actualizando las configuraciones existentes. Consulte [Configuración de recursos de Experience Manager con Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) para obtener más información.

#### Mejoras de accesibilidad (6.5.4.0) {#accessibility-enhancements}

[!DNL Experience Manager Assets] incluye las siguientes mejoras de accesibilidad:

* Las teclas de flecha del teclado se pueden utilizar para mover y recorrer áreas dentro de imágenes con zoom. Para obtener más información, consulte [Recursos de previsualización que utilizan únicamente teclas de teclado](../assets/manage-assets.md#previewing-assets).

* Los lectores de pantalla pueden leer las casillas de verificación de estado mixto (en las que, a menos que seleccione todos los predicados anidados, las casillas de verificación de primer nivel no se seleccionan y se rompen) en el panel Filtros.

* Las restricciones de formato de fecha y hora se proporcionan en las etiquetas de campo de los campos de fecha, para permitir que los usuarios introduzcan la fecha en el formato correcto mediante el teclado.
Por ejemplo, `On Time (MM-DD-YYYY HH:mm)`. Aquí MM es el mes en formato de dos dígitos, AAAA es el año, DD es el día en formato de dos dígitos, HH es la hora en formato militar de 24 horas y mm es el minuto.

* Los lectores de pantalla anuncian la opción de eliminar las etiquetas seleccionadas (`X` símbolo) y el número de etiquetas seleccionadas.

#### Columna que se puede ordenar para la fecha de creación de los recursos en la vista de lista (6.5.3.0) {#sortable-date-created-column}

En la vista de lista DAM se agrega una nueva columna que se puede ordenar para la fecha de creación de los recursos y, en la búsqueda de recursos, se genera una vista de listas.

![Columna ordenable para la fecha de creación](assets/asset-created-date.png)

#### Búsqueda visual de [!DNL Adobe Experience Manager Assets] (6.5.2.0) {#visual-search}

[!DNL Assets] los usuarios pueden buscar imágenes visualmente similares. Experience Manager muestra las imágenes con etiquetas inteligentes del repositorio de DAM que son similares a una imagen seleccionada por el usuario. Consulte [Búsqueda visual](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

#### Invalidar contenido en caché de CDN (6.5.6.0) {#invalidate-cdn-cached-content}

Ahora puede utilizar la interfaz de usuario [!DNL Dynamic Media] para invalidar el contenido en caché de la red de Envío de contenido (CDN). Como resultado, los recursos actualizados están disponibles instantáneamente en lugar de esperar a que caduque la caché. Puede invalidar CDN mediante:

* Creación de una plantilla de invalidación de CDN: Selección de recursos y direcciones URL asociadas a plantillas

* Selección de recursos y ajustes preestablecidos asociados mediante el selector de recursos

* Añadir direcciones URL de recursos completas

#### Publicación selectiva de recursos en [!DNL Experience Manager] y [!DNL Dynamic Media] (6.5.6.0) {#selective-publishing}

Ahora puede optar por publicar o cancelar la publicación de recursos en [!DNL Experience Manager] o [!DNL Dynamic Media] mediante [!UICONTROL Asistente para publicación rápida] o [!UICONTROL Administrar publicación]. También puede establecer el modo `Publish` o `Unpublish` en el nivel de carpeta.

#### Imágenes inteligentes para Dynamic Media {#smart-imaging}

Las imágenes inteligentes utilizan las características de visualización únicas de cada usuario para ofrecer automáticamente las imágenes correctas optimizadas para su experiencia, lo que mejora el rendimiento y la participación. Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes y utilizan la inteligencia en el último milisegundo de envío para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión de red o del navegador. Consulte [Imágenes inteligentes](../assets/imaging-faq.md).

#### Recorte inteligente en perfiles de vídeo para Dynamic Media (6.5.3.0) {#smart-crop-video}

El recorte inteligente para vídeo, una función opcional disponible en Perfiles de vídeo, es una herramienta que utiliza la potencia de la inteligencia artificial en Adobe Sensei para detectar y recortar automáticamente el punto focal en cualquier vídeo adaptable o vídeo progresivo que haya cargado, independientemente del tamaño. Consulte [Acerca del uso del recorte inteligente en perfiles de vídeo](../assets/video-profiles.md).

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### Rellene previamente un formulario adaptable en el cliente (6.5.6.0) {#prefill-merge-data-at-client}

Cuando se rellena previamente un formulario adaptable, el servidor [!DNL Experience Manager Forms] combina los datos con un formulario adaptable y le envía el formulario rellenado. De forma predeterminada, la acción de combinación de datos tiene lugar en el servidor.
Ahora puede configurar el servidor [!DNL Experience Manager Forms] para que [realice la acción de combinación de datos en el cliente](../../help/forms/using/prepopulate-adaptive-form-fields.md) en lugar del servidor. Reduce considerablemente el tiempo necesario para rellenar y procesar formularios adaptables.

#### Integración del modelo de datos de formulario con las API de RESTful en un servidor con implementación SSL bidireccional (6.5.6.0) {#fdm-integration-rest-apis-two-way-ssl}

[!DNL Experience Manager Forms] el modelo de datos de formulario ahora puede  [integrarse con las API de RESTful en un servidor que tenga una SSL bidireccional implementada en él](../../help/forms/using/configure-data-sources.md).

#### Compatibilidad añadida para etiquetas de texto [!DNL Adobe Sign] en el servicio de Automated forms conversion (6.5.6.0) {#sign-integration-acroform-afcs}

Si un AcroForm incluye [!DNL Adobe Sign] etiquetas de texto, estos campos ahora se reconocen y representan como campos [!DNL Adobe Sign] en el formulario adaptable convertido mediante [!DNL Automated Forms Conversion service]. Un firmante puede rellenar estos campos al firmar el formulario adaptable.

#### Compatibilidad para convertir PDF forms de color en formularios adaptables (6.5.6.0) {#colored-PDF-forms}

Puede utilizar [!DNL Automated Forms Conversion service] para convertir PDF forms de color en formularios adaptables.

#### Compatibilidad con los protocolos SMB 2 y SMB 3 (6.5.6.0) {#smb-support}

[!DNL Experience Manager Forms] ahora admite los protocolos SMB 2 y SMB 3.

#### Caché mejorada para páginas de formularios adaptables traducidas (6.5.6.0) {#enhanced-caching-translated-adaptive-forms}

Ahora puede especificar [configuración regional como selector en la dirección URL del formulario adaptable en lugar de un argumento en la dirección URL del formulario adaptable](../../help/forms/using/supporting-new-language-localization.md). Ayuda a almacenar en caché formularios adaptables traducidos en [!DNL Experience Manager Dispatcher]. En versiones anteriores no era posible almacenar en caché formularios adaptables traducidos. Para obtener información detallada sobre la configuración del almacenamiento en caché para utilizar la configuración regional como selector en la URL del formulario adaptable, consulte [Configuración de la caché de formularios adaptables en el despachante](../../help/forms/using/configure-adaptive-forms-cache.md).

#### Guardar el resultado del servicio del modelo de datos de formulario en una variable (6.5.6.0) {#save-fdm-service-to-variable}

El modelo de datos de formulario permite guardar el resultado de un servicio de modelo de datos de formulario en una variable. [!DNL Experience Manager Forms] ahora asigna automáticamente el tipo del servicio del modelo de datos de formulario al tipo de variable.

#### Adjuntar varios archivos para el componente Archivo adjunto (6.5.6.0) {#attach-multiple-files}

Ahora puede [adjuntar varios archivos](../../help/forms/using/introduction-forms-authoring.md) al componente [!UICONTROL Archivo adjunto] de formularios adaptables.

#### Personalización de las columnas Bandeja de entrada de Adobe Experience Manager (6.5.5.0) {#customize-aem-inbox-columns}

Puede personalizar una bandeja de entrada [!DNL Experience Manager] para cambiar el título predeterminado de una columna, reordenar la posición de una columna y mostrar columnas adicionales basadas en los datos de un flujo de trabajo. Los miembros del grupo `administrators` o `workflow-administrators` pueden personalizar las columnas. Para obtener más información, consulte [Control de administración](../sites-authoring/inbox.md#inbox-admin-control).

![Personalizar las columnas de la Bandeja de entrada Experience Manager](assets/customize-columns.gif)

#### Guardar comunicaciones interactivas como borrador (6.5.5.0) {#save-as-draft}

Puede utilizar la interfaz de usuario del agente para guardar uno o varios borradores para cada comunicación interactiva y recuperar el borrador más adelante para continuar trabajando en él. Puede especificar un nombre diferente para cada borrador para identificarlo. Para obtener más información, consulte [Guardar comunicaciones interactivas como borrador](../forms/using/prepare-send-interactive-communication.md#save-as-draft).

![Guardar como borrador](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] compatibilidad con el servidor de aplicaciones (6.5.5.0)  {#weblogic-support}

Adobe Experience Manager Forms ha agregado compatibilidad con [!DNL Oracle WebLogic 12] para Adobe Experience Manager Forms en JEE. Puede actualizar desde una versión anterior o configurar un nuevo Forms Experience Manager 6.5 en el servidor JEE en [!DNL Oracle WebLogic] 12.2.1.4 y posterior. Posteriormente corresponde a los cambios menores de la versión, donde x en 12.2.1.x se sustituye por un número de versión.

#### Mejoras de accesibilidad (6.5.5.0) {#accessibility-improvements}

Adobe Experience Manager Forms incluye las siguientes mejoras de accesibilidad:

* Cuando un usuario previsualización un formulario adaptable como un formulario HTML, el campo [!UICONTROL Firma de garabatos] conserva el enfoque de tabulación.

* Los mensajes de error que se muestran al enviar un formulario adaptable ahora contienen el atributo `aria-describedBy`. El atributo se adjunta a los campos a los que se hace referencia en el mensaje de error. El atributo `aria-describedby` indica los ID de los elementos que describen el objeto. Ayuda a establecer una relación entre utilidades o grupos y texto que los describa.

* Si un formulario adaptable tiene algunos campos obligatorios, el atributo obligatorio se establece en `True` para dichos campos en el esquema de accesibilidad de ARIA.

#### Autenticación basada en certificados X-509 para servicios Web basados en SOAP en modelo de datos de formulario (6.5.5.0) {#x509-based-authentication-soap}

El modelo de datos de formulario ahora admite la autenticación basada en certificados X-509 mientras se utilizan servicios Web SOAP como origen de datos. Para obtener más información, consulte [Configuración de servicios Web SOAP](../forms/using/configure-data-sources.md#configure-soap-web-services).

#### Otras mejoras clave (6.5.5.0) {#other-improvements}

* Experience Manager 6.5 Forms en JEE Documento Security ahora se basa en [!DNL Apache Struts 2].

* Compatibilidad añadida para [!DNL Oracle Real Applications Cluster (RAC) 19c].

#### Generar salida imprimible en flujos de trabajo Forms Experience Manager (6.5.4.0) {#generate-printable-output}

El paso de flujo de trabajo Generar salida imprimible permite integrar un archivo de plantilla de origen con un archivo de datos. Esta integración le permite imprimir o guardar diferentes copias del archivo de plantilla. El paso genera una salida PCL, PostScript, ZPL, IPL, TPCL o DPL. Para obtener más información sobre esta función, consulte [Flujo de trabajo centrado en Forms en OSGi - Referencia de pasos](../forms/using/aem-forms-workflow-step-reference.md).

![Generar salida imprimible](assets/generate-print-output-step.gif)

#### Compatibilidad con múltiples columnas para formularios adaptables y comunicaciones interactivas en modo Diseño (6.5.4.0) {#multi-column-adaptive-forms}

Ahora puede definir el número de columnas para un panel en formularios adaptables y comunicaciones interactivas. Cambie al modo de diseño para utilizar la nueva opción de varias columnas. Para obtener más información, consulte [Uso del modo Diseño para cambiar el tamaño de los componentes](../forms/using/resize-using-layout-mode.md).

![Diseño de varias columnas](assets/multi-column-layout.gif)

#### Personalizaciones de la Bandeja de entrada de Experience Manager (6.5.4.0) {#aem-inbox}

La nueva opción Control de administración permite a los administradores:

* Personalice el texto y el logotipo del encabezado.

* Controle la visualización de los vínculos de navegación disponibles en el encabezado.

La opción Control de administración solo está visible para los miembros del grupo `administrators` o `workflow-administrators`. Para obtener más información sobre esta función, consulte [Su bandeja de entrada](../sites-authoring/inbox.md).

#### Compatibilidad con texto enriquecido en formularios HTML5 (6.5.4.0) {#rich-text-support}

Conversión de un campo de texto en un formulario XFA en un campo de texto enriquecido en un formulario HTML5. Para obtener más información, consulte [Diseño de plantillas de formulario para formularios HTML5](../forms/using/designing-form-template.md).

#### Mejoras de accesibilidad (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms incluye las siguientes mejoras de accesibilidad:

* Los lectores de pantalla anuncian los campos de casillas de verificación, vínculos, selector de fecha e introducción de fecha correctamente en un formulario adaptable.

* Cada página de un formulario adaptable ahora incluye un título y una etiqueta de punto de referencia principal.

#### Compartir y solicitar acceso a los elementos de la Bandeja de entrada de un usuario de Forms Experience Manager (6.5.3.0) {#share-request-access}

Puede compartir los elementos de la Bandeja de entrada con otro usuario. Una vez que otro usuario obtiene acceso a los elementos de la Bandeja de entrada, el usuario puede reclamar y realizar las acciones correspondientes en los elementos compartidos. Del mismo modo, puede solicitar acceso a los elementos de la Bandeja de entrada a otros usuarios. Consulte [Compartir y solicitar acceso a los elementos de la Bandeja de entrada de un usuario](../forms/using/configure-shared-queues-osgi.md).

#### Configure las opciones de fuera de la oficina para los elementos de la Bandeja de entrada de un usuario Experience Manager de Forms (6.5.3.0) {#configure-out-of-office}

Si planea salir de la oficina, puede especificar lo que sucede con los artículos que se le han asignado para ese período.
Tiene la opción de especificar una fecha y hora de inicio y una fecha y hora de finalización para que la configuración fuera de la oficina esté en vigor. Puede establecer una persona predeterminada a la que se enviarán todos los elementos. Consulte [Configuración fuera de la oficina](../forms/using/configure-out-of-office-settings.md).

#### Generar varias comunicaciones interactivas mediante la API por lotes para Forms Experience Manager (6.5.3.0) {#generate-multiple-ic}

Puede utilizar la API por lotes para generar varias comunicaciones interactivas a partir de una plantilla. La plantilla es una comunicación interactiva sin datos. La API de lote combina datos con una plantilla para generar una comunicación interactiva. La API es útil en la producción masiva de comunicaciones interactivas. Por ejemplo: facturas telefónicas, extractos de tarjetas de crédito para varios clientes. Consulte [Generación de varias comunicaciones interactivas mediante la API por lotes](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

## Versiones clave desde Adobe Experience Manager 6.5 SP6 {#key-releases-since-last-sp}

Entre el 3 de septiembre de 2020 y el 26 de noviembre de 2020, Adobe lanzó lo siguiente, además de los Service Packs y los paquetes de correcciones acumulativos:

* [!DNL Adobe Experience Manager] como Cloud Service  [2020.9.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-2020-9-0.html?lang=en#release-notes) y  [2020.10.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-2020-10-0.html?lang=en#release-notes).

* [[!DNL Experience Manager] aplicación de escritorio 2.0 (2.0.3.2)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

* [Sitio de referencia WKND - 0.0.6](https://github.com/adobe/aem-guides-wknd/releases/tag/aem-guides-wknd-0.0.6)

* [Experience Manager Screens: Feature Pack 202008](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202008.html)

* [Vínculo de recurso de Adobe v2.2](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html)

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] 6.5 documentación](../user-guide/home.md)
>* [Notas de la versión generales de la versión de la versión  [!DNL Adobe Experience Manager] 6.5](release-notes.md)
>* [Notas de la versión del Service Pack para [!DNL Adobe Experience Manager]  6.5](sp-release-notes.md)

