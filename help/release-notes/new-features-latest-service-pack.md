---
title: Novedades de [!DNL Experience Manager] 6.5 Service Pack 9
description: Novedades de [!DNL Experience Manager] 6.5 Service Pack 9
contentOwner: AK
mini-toc-levels: 1
exl-id: 32470e6e-8a66-4670-82da-2259f6e001c3
source-git-commit: 557615a019fedee1863e4d1970445fbfa17736cb
workflow-type: tm+mt
source-wordcount: '3680'
ht-degree: 1%

---

# Novedades de [!DNL Adobe Experience Manager] 6.5 Service Pack 9 {#aem-whats-new-service-pack}

![Novedades](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] 6.5 Los Service Packs proporcionan nuevas funciones, mejoras solicitadas por el cliente y mejoras de rendimiento, estabilidad y seguridad a intervalos trimestrales. La disponibilidad trimestral facilita el acceso y la adopción de nuevas características e innovaciones.

Este artículo resalta las funciones incluidas en el Service Pack más reciente, las [características clave incluidas en los Service Pack 6.5 anteriores](#key-features-previous-service-packs) y las [versiones clave desde la última versión del Service Pack](#key-releases-since-last-sp).

>[!NOTE]
>
>A partir de [!DNL Experience Manager] Service Pack 9, los clientes [!DNL Experience Manager] pueden desarrollar y operar sus [!DNL Experience Manager] aplicaciones con distribuciones de las [!DNL Azul Zulu] compilaciones de OpenJDK, compatibles con Java SE.
>El Adobe también proporciona soporte para los [!DNL Azul Zulu] JDK a los clientes [!DNL Experience Manager].
>Puede descargar las versiones relevantes de los [!DNL Azul Zulu] JDK desde [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
>Los derechos de uso de la tecnología Java de Oracle, tal como se distribuyen por Adobe, expirarán a finales de diciembre de 2022. [!DNL Experience Manager] se recomienda a los clientes que planifiquen e implementen el uso de para los  [!DNL Azul Zulu] JDK a más tardar para esta fecha. Para obtener más información sobre el uso de la tecnología [!DNL Oracle Java] y la tecnología [!DNL Azul Zulu], consulte las [preguntas frecuentes](https://experienceleague.adobe.com/docs/experience-manager-65/assets/adobe-azul-openjdk-license-agreement.pdf?lang=en) asociadas.

## [!DNL Adobe Experience Manager Sites] {#aem-sites}

### Capacidad de restaurar páginas y árboles eliminados {#ability-to-restore-pages-tree}

Ahora puede restaurar las páginas eliminadas y toda la vista de árbol en una página [!DNL Experience Manager Sites].

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* Se ha actualizado el nombre de las regiones y escenarios chinos relacionados con Hong Kong, Macao y Taiwán, para hacerlos coherentes con las opiniones políticas y sociales chinas.

* Se introduce una configuración opcional para cambiar la cadena en los ID de correo electrónico en la respuesta de API ACP de [!DNL Adobe Experience Manager].

   ![configuración para cambiar los ID de correo electrónico a minúsculas en la respuesta ACP de  [!DNL Experience Manager]](assets/email-lowcase-config.png)

* El contraste del texto y los iconos en el fondo se mejora para diversas funciones. Esta implementación de las directrices WCAG hace que [!DNL Assets] sea más accesible para los usuarios con visión y percepción limitadas del color. Consulte [mejoras de accesibilidad en [!DNL Assets]](sp-release-notes.md#assets-accessibility-6590).

### [!DNL Dynamic Media] {#assets-dynamic-media}

* [[!DNL Dynamic Media] es más ](sp-release-notes.md#assets-accessibility-6590) accesible en términos de:

   * Facilidad de uso con teclas de teclado.
   * Contraste (con fondo) de texto, texto de marcador de posición y controles en varios editores.
   * Accesibilidad y narración por parte de los lectores de pantalla.

* El RGPD de imágenes inteligentes (proporción de píxeles de dispositivo) y la optimización del ancho de banda de la red le permiten ofrecer imágenes de la mejor calidad de forma eficaz; en dispositivos con pantallas de alta resolución y ancho de banda de red restringido. Para obtener más información y cronología, consulte [preguntas frecuentes sobre imágenes inteligentes](/help/assets/imaging-faq.md).

* [!DNL Dynamic Media] delivery (modificador de `fmt` URL) ahora es compatible con el formato de imagen de próxima generación AVIF (formato de imagen AV1). Para obtener más información y cronología, consulte [servicio de imágenes y renderización de API fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html).

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>El paquete de complementos de [!DNL Experience Manager Forms] está disponible una semana después del lanzamiento programado del [!DNL Experience Manager] Service Pack.

### Compatibilidad con [!DNL Azul Zulu OpenJDK] {#support-azul-zulu}

Ahora puede desarrollar y operar aplicaciones con [!DNL Azul Zulu] compilaciones de [!DNL OpenJDK] para [!DNL Experience Manager Forms] en implementaciones OSGi. Para obtener más información, consulte [Experience Manager 6.5 Service Pack 9 Notas de la versión](sp-release-notes.md) y [Requisitos técnicos](../sites-deploying/technical-requirements.md).

### Capacidad para enviar un correo electrónico de notificación a un grupo mediante [!UICONTROL Asignar tarea] {#group-notification-email}

Ahora puede enviar un correo electrónico de notificación a una dirección de correo electrónico de grupo mediante el paso Asignar tarea del flujo de trabajo.

### Capacidad para recuperar un borrador de comunicación interactiva después de modificar la comunicación interactiva de origen {#retrieve-draft-after-source-modifications}

Ahora puede recuperar una comunicación interactiva guardada como borrador después de realizar cambios en la comunicación interactiva de origen.

### Configure un nombre de dominio personalizado para cargar, procesar y validar el servicio reCAPTCHA {#set-custom-domain-name-recaptcha}

El servicio reCAPTCHA utiliza `https://www.recaptcha.net/` como dominio predeterminado. Ahora puede modificar la configuración para establecer `https://www.google.com/` o cualquier nombre de dominio personalizado para cargar, procesar y validar el servicio reCAPTCHA.

### Mejoras en los datos de entrada para el paso del flujo de trabajo [!UICONTROL Invocar el servicio del modelo de datos de formulario] {#input-data-enhancements-fdm}

Cuando se selecciona un modelo de datos de formulario y un servicio en el paso de flujo de trabajo [!UICONTROL Invocar el servicio del modelo de datos de formulario], se especifican argumentos de servicio para los datos de entrada.

Si selecciona la opción [!UICONTROL Relative to Payload] para adjuntar un archivo como argumento de servicio, ahora puede especificar la ruta de la carpeta que contiene el archivo en lugar del nombre real del archivo. La definición del nombre de la carpeta, en lugar del nombre del archivo adjunto, permite reutilizar modelos de flujo de trabajo. No se limita el modelo de flujo de trabajo a un único nombre de archivo adjunto.

### Capacidad para utilizar varias páginas de formato en una plantilla Documento de registro {#use-multiple-master-pages-dor-template}

Ahora puede utilizar varias páginas de formato en una plantilla Documento de registro . Como resultado, ahora puede tener diferentes encabezados, pies de página, fuentes, información de logotipo en la página de título y otras páginas de la plantilla.

### Saltos de página de asistencia en el documento de registro {#support-page-breaks-dor}

Ahora puede agregar saltos de página a un documento de registro. Como resultado, si un panel se rompe en las páginas, puede agregar un salto de página para mover el panel a una nueva página de un Documento de registro.

## Funciones principales en paquetes de servicios anteriores de [!DNL Experience Manager] 6.5 {#key-features-previous-service-packs}

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### Ordenar las páginas de Live Copy disponibles para el lanzamiento (6.5.8.0) {#sort-livecopy-pages}

Ahora puede ordenar las páginas de Live Copy disponibles para la implementación mediante las propiedades [!UICONTROL Name], [!UICONTROL Last modified date] y [!UICONTROL Last rollout date]. La [!UICONTROL Última fecha de lanzamiento] para una página es una nueva propiedad introducida en esta versión.

#### Disponibilidad de movimientos de página y lanzamientos de MSM como operaciones asincrónicas (6.5.7.0) {#page-moves-msm-asynchronous}

Ahora puede realizar los movimientos de página y los despliegues de MSM como operaciones asincrónicas para reducir su impacto en el rendimiento del tiempo de ejecución. Puede programar las operaciones para su ejecución inmediata o posterior. El estado de los trabajos asociados y los pasos del proceso se muestran en una consola, lo que resulta útil para supervisar las implementaciones de MSM a gran escala.

#### Disponibilidad de la operación Mover página en modo asincrónico (6.5.6.0) {#page-move-asynchronous}

La operación de movimiento de página ya está disponible en modo asíncrono. Además de la ejecución inmediata, también puede programar la operación Mover página para una ejecución posterior.

#### Mejoras de accesibilidad (6.5.5.0) {#accessibility-sites}

* Se mejoraron los informes de errores añadiendo información de texto.

* Se ha mejorado el enfoque de la interfaz de usuario durante la navegación mediante el teclado.

* Se ha mejorado la relación de contraste para varios elementos de la interfaz de usuario.

* Se ha mejorado la coherencia de los atributos alternativos para las imágenes de página.

* Se ha mejorado la coherencia de las etiquetas de las aplicaciones de Internet enriquecidas accesibles (ARIA).

* Se han mejorado las capacidades de acceso al escritorio no visual (NVDA).

* Se ha mejorado la compatibilidad con lectores de pantalla.

#### Otras mejoras clave (6.5.5.0) {#other-enhancements-sites}

* No se permite el acceso anónimo al CRXDE Lite para mejorar la seguridad. En su lugar, se dirige a los usuarios a la pantalla de inicio de sesión. Consulte [Desarrollo con el CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* Al copiar o pegar un árbol de páginas, ahora tiene la opción de pegar la página raíz o la página raíz con las subpáginas del árbol.

* [!DNL Adobe Experience Manager Experience Fragments] exportados a  [!DNL Adobe Target] espacios de trabajo ahora aparecen como tipos de oferta únicos y fuentes de oferta en  [!DNL Target].

* Administrador de varios sitios : el déclencheur Publicar ahora elimina un componente de la página publicada si un componente se elimina de la página de origen.

* Administrador de varios sitios : cuando el nombre de un componente local en una [!UICONTROL Live Copy] es idéntico al nombre de un componente en el modelo y el componente se despliega desde el modelo, el término `_msm_moved` se agrega ahora al nombre del componente local.

#### Mejoras en el sistema de estilos (6.5.4.0) {#style-system-enhancements}

Ahora puede seleccionar estilos en el cuadro de diálogo de componentes mediante el sistema de estilos mejorado.

#### Mejoras de rendimiento en diversas áreas (6.5.4.0) {#performance-improvements}

* Se ha reducido el tiempo para cargar e inicializar ContextHub en un sitio (`contexthub.kernel.js`). El resultado es una carga de página más rápida durante una visita al sitio.

* Se ha reducido el tiempo para actualizar una página después de arrastrar [!DNL Experience Fragments] al [!DNL Sites] Editor de páginas.

* Se ha reducido el tiempo de carga de las entradas de una página [!DNL Sites] con más de 200 Live Copy en **[!UICONTROL Información general de Live Copy]**.

* Se ha mejorado el manejo de direcciones URL incompletas o no válidas. Estas direcciones URL pueden ralentizar el Editor de plantillas.

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

* Al utilizar la funcionalidad [Recursos conectados](/help/assets/use-assets-across-connected-assets-instances.md), ahora puede ver una lista de todas las páginas [!DNL Sites] que utilizan el recurso. Estas referencias a un recurso están disponibles en la página [!UICONTROL Propiedades] de un recurso. Esto permite a los administradores, especialistas en marketing y bibliotecarios obtener una vista completa del uso de los recursos, lo que permite un mejor seguimiento, administración y coherencia de marca (6.5.8.0).

* Al eliminar un recurso al que se hace referencia en una página web, [!DNL Experience Manager] muestra una advertencia. Puede forzar la eliminación de un recurso al que se hace referencia o comprobar y modificar las referencias que se muestran en la página [!DNL Properties] del recurso. Al hacer clic en las referencias se abren las páginas locales y remotas [!DNL Sites] (6.5.8.0).

* [!DNL Assets] y  [!DNL Dynamic Media] proporcionan varias mejoras de accesibilidad. Las mejoras están relacionadas con la navegación mediante el teclado, el uso de lectores de pantalla y mejoras similares para permitir el uso de tecnologías de asistencia (AT). Consulte [[!DNL Assets] mejoras](/help/release-notes/sp-release-notes.md#assets-6570) y [[!DNL Dynamic Media] mejoras](/help/release-notes/sp-release-notes.md#dynamic-media-6570) (6.5.7.0)

* Los usuarios pueden ordenar los recursos digitales en las vistas de tarjeta y columna (6.5.7.0).

#### Mejoras de accesibilidad (6.5.6.0) {#accessibility-assets-6560}

* **Se ha mejorado el enfoque de la interfaz de usuario durante la navegación** mediante el teclado, por ejemplo, centrándose en:

   * `x` en el cuadro de diálogo  [!UICONTROL Vista previa ] de versión de un recurso en la  [!UICONTROL línea de tiempo].

   * Opciones de interfaz de usuario procesables.

   * Campo de correo electrónico en el cuadro de diálogo [!UICONTROL Compartir enlace] y campo para agregar grupo de usuarios cerrado en la pestaña [!UICONTROL Permiso] de la carpeta [!UICONTROL Propiedades].

* **Funcionalidad mejorada con teclas de teclado**

   Los usuarios pueden utilizar teclas de teclado para arrastrar controles en el editor de formularios de esquemas de metadatos en el modo Examinar del lector de pantalla.

* **Se ha mejorado la capacidad de uso de los usuarios** de lectores de pantalla debido a lo siguiente:

   * Los lectores de pantalla anuncian el propósito de los reproductores de vídeo y audio.

   * Los lectores de pantalla anuncian el propósito de las opciones de la interfaz de usuario para eliminar las etiquetas seleccionadas mediante el cuadro de diálogo [!UICONTROL Selección de etiquetas] en el recurso [!UICONTROL Propiedades].

   * Los lectores de pantalla anuncian los encabezados de fila y los elementos de fila de las tablas, de modo que los usuarios sepan qué entradas pertenecen a la misma fila.

   * Título de página descriptivo y significativo de la página de búsqueda.

   * Los lectores de pantalla anuncian las opciones del panel de filtro de búsqueda como acordeones ampliables.

#### Otras mejoras en [!DNL Assets] (6.5.6.0) {#other-enhancements-assets-6560}

* Los grupos de usuarios asociados con carpetas (privadas y no privadas) ahora se eliminan del repositorio al [eliminar esas carpetas](/help/assets/private-folder.md#delete-private-folder). Sin embargo, los grupos de usuarios redundantes, huérfanos, no utilizados y autogenerados se pueden eliminar del repositorio utilizando JMX.

#### Mejoras de accesibilidad en [!DNL Assets] (6.5.5.0) {#assets-accessibility}

[!DNL Experience Manager Assets] ahora es más accesible de acuerdo con las directrices de accesibilidad del contenido web (WCAG). La accesibilidad ha mejorado debido a las siguientes mejoras:

* Muchos elementos, controles, páginas y cuadros de diálogo de la interfaz de usuario son fáciles de leer en pantalla.

* Se puede acceder a muchos elementos de interfaz de usuario, controles y campos de formulario de entrada mediante el teclado.

* El color y el contraste de algunos elementos de la interfaz de usuario se actualizan para que los usuarios con visión limitada o los usuarios sin percepción del color puedan distinguir estos elementos de la interfaz de usuario. Por ejemplo, el color de los iconos de clasificación por estrellas (como en la sección [!UICONTROL Clasificación] de la pestaña [!UICONTROL Avanzadas] del recurso [!UICONTROL Propiedades] o en la vista de tarjeta) se cambia para obtener el contraste adecuado.

   ![Iconos de clasificación con contraste mejorado](assets/star-rating-icons.png)

#### Tratamiento de excepciones mejorado (6.5.5.0) {#exception-handling}

[!DNL Assets] el flujo de la interfaz de usuario de tiene una mejor gestión de excepciones. Si un recurso no tiene un tipo para su dimensión, la excepción observada se registra en los archivos de registro.

#### Compatibilidad con recursos 3D en [!DNL Dynamic Media] (6.5.5.0) {#support-for-3d}

La compatibilidad con imágenes 3D en [!DNL Dynamic Media] permite a los clientes publicar y agregar contenido 3D a páginas web y aplicaciones. La compatibilidad incluye:

* Publique formatos de recursos 3D comunes y genere una URL de recursos que se pueda usar en páginas web y otras aplicaciones.

* Un visualizador web 3D, con tecnología [!DNL Adobe Dimension], para ver de forma interactiva los recursos 3D publicados.

* Publique y vea recursos 3D comunes en páginas [!DNL Experience Manager Sites] mediante el componente [!DNL Sites] WCM.

#### Configurar [!DNL Experience Manager Assets] con [!DNL Brand Portal] (6.5.4.0) {#configure-assets-bp}

Se cambia el canal de autorización entre [!DNL Experience Manager Assets] y [!DNL Brand Portal]. Anteriormente, [!DNL Brand Portal] se configuraba en la interfaz de usuario clásica a través de la puerta de enlace OAuth heredada, que utiliza el intercambio de tokens de JWT para obtener un token de acceso de IMS para la autorización. [!DNL Experience Manager Assets] ahora se configura con  [!DNL Brand Portal] mediante  [!DNL Adobe I/O], que obtiene un testigo IMS para la autorización del  [!DNL Brand Portal] inquilino.

Los pasos para configurar [!DNL Experience Manager Assets] con [!DNL Brand Portal] son diferentes según la versión [!DNL Experience Manager] y si está configurando por primera vez o actualizando las configuraciones existentes. Consulte [Configuración de recursos de Experience Manager con Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) para obtener más información.

#### Mejoras de accesibilidad (6.5.4.0) {#accessibility-enhancements-6540}

[!DNL Experience Manager Assets] incluye las siguientes mejoras de accesibilidad:

* Las teclas de flecha del teclado se pueden utilizar para mover y recorrer áreas dentro de imágenes con zoom. Para obtener más información, consulte [vista previa de recursos utilizando claves de teclado únicamente](../assets/manage-assets.md#previewing-assets).

* Los lectores de pantalla pueden leer las casillas de verificación de estado mixto (en las que, a menos que seleccione todos los predicados anidados, no se seleccionan las casillas de verificación de primer nivel y aparecen marcadas) del panel Filtros.

* Las restricciones de formato de fecha y hora se proporcionan en las etiquetas de campo de los campos de fecha, para permitir a los usuarios introducir la fecha en el formato correcto mediante el teclado.
Por ejemplo, `On Time (MM-DD-YYYY HH:mm)`. Aquí MM es el mes en formato de dos dígitos, AAAA es el año, DD es el día en formato de dos dígitos, HH es la hora en formato militar de 24 horas y mm es el minuto.

* Los lectores de pantalla anuncian la opción de eliminar las etiquetas seleccionadas (símbolo `X`) y el número de etiquetas seleccionadas.

#### Columna que se puede ordenar para Fecha de creación de recursos en la vista de lista (6.5.3.0) {#sortable-date-created-column}

Se añade una nueva columna clasificable para la fecha de creación de los recursos en la vista de lista DAM y en los resultados de búsqueda de recursos en la vista de lista.

![Columna ordenable para la fecha creada](assets/asset-created-date.png)

#### Búsqueda visual para [!DNL Adobe Experience Manager Assets] (6.5.2.0) {#visual-search}

[!DNL Assets] los usuarios pueden buscar imágenes visualmente similares. Experience Manager muestra las imágenes con etiquetas inteligentes del repositorio de DAM similares a una imagen seleccionada por el usuario. Consulte [Búsqueda visual](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

#### Invalidar contenido en caché de CDN (6.5.6.0) {#invalidate-cdn-cached-content}

Ahora puede utilizar la interfaz de usuario [!DNL Dynamic Media] para invalidar el contenido almacenado en caché de la red de entrega de contenido (CDN). Como resultado, los recursos actualizados están disponibles instantáneamente en lugar de esperar a que caduque la caché. Puede invalidar la CDN:

* Creación de una plantilla de invalidación de CDN: Selección de recursos y direcciones URL asociadas a formularios basados en plantillas

* Selección de recursos y ajustes preestablecidos asociados mediante el selector de recursos

* Adición de direcciones URL de recursos completas

#### Publicación selectiva de recursos en [!DNL Experience Manager] y [!DNL Dynamic Media] (6.5.6.0) {#selective-publishing}

Ahora puede elegir publicar o cancelar la publicación de recursos de forma selectiva en [!DNL Experience Manager] o [!DNL Dynamic Media] mediante el asistente [!UICONTROL Publicación rápida] o [!UICONTROL Administrar publicación]. También puede establecer el modo `Publish` o `Unpublish` en el nivel de carpeta.

#### Imágenes inteligentes para Dynamic Media {#smart-imaging}

Las imágenes inteligentes utilizan las características de visualización únicas de cada usuario para ofrecer automáticamente las imágenes adecuadas optimizadas para su experiencia, lo que resulta en un mejor rendimiento y participación. Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes y utilizan la inteligencia en el último milisegundo de envío para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión de red o del explorador. Consulte [Imágenes inteligentes](../assets/imaging-faq.md).

#### Recorte inteligente en perfiles de vídeo para Dynamic Media (6.5.3.0) {#smart-crop-video}

El recorte inteligente para vídeo (una función opcional disponible en Perfiles de vídeo) es una herramienta que utiliza el poder de la inteligencia artificial en Adobe Sensei para detectar y recortar automáticamente el punto focal en cualquier vídeo adaptable o vídeo progresivo que haya cargado, independientemente del tamaño. Consulte [Acerca del uso del recorte inteligente en perfiles de vídeo](../assets/video-profiles.md).

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### Mostrar u ocultar el componente CAPTCHA en una forma adaptable basada en reglas (6.5.8.0) {#show-hide-captcha}

Ahora puede validar CAPTCHA en el envío de formularios adaptables o en la acción del usuario. También puede agregar condiciones para validar CAPTCHA en una acción del usuario y mostrar u ocultar el componente CAPTCHA en un formulario adaptable basado en reglas.

#### Añadir servicios CAPTCHA personalizados (6.5.8.0) {#add-custom-captcha-services}

[!DNL Experience Manager Forms] proporciona compatibilidad para utilizar Google reCAPTCHA (se requiere una licencia independiente de las API de Google reCAPTCHA) como servicio de validación de CAPTCHA. También puede utilizar un servicio CAPTCHA personalizado para validar CAPTCHA.

#### Otras mejoras (6.5.8.0) {#other-enhancements-forms-6580}

* Se ha mejorado la accesibilidad del componente Selector de fecha [!DNL Experience Manager Forms].

* Se ha agregado compatibilidad para generar una comunicación interactiva en formato PCL mediante la API PrintChannel.

* Al realizar una conversión PDFG, ahora puede habilitar o deshabilitar los cambios del Registro [!DNL Experience Manager Forms] para la generación de marcadores personalizados.

#### Mejoras de rendimiento (6.5.7.0) {#performance-improvements-forms}

[!DNL Experience Manager] 6.5 Service Pack 7 Forms mejora el rendimiento para:

* Validación de los valores de campo en el servidor al enviar un formulario adaptable.

* Conversión de un formulario PDF en un formulario adaptable mediante [!DNL Automated Forms Conversion service].

#### Compatibilidad con grupos de disponibilidad Always On de Microsoft SQL Server 2016 para alta disponibilidad (6.5.7.0) {#always-on-availability-groups}

[!DNL Experience Manager Forms] ahora es compatible con los grupos de disponibilidad Always On de  [!DNL Microsoft] SQL Server 2016 para una alta disponibilidad en implementaciones de OSGi.

#### Modelo de datos de formulario Configuración del cliente HTTP para optimizar el rendimiento (6.5.7.0) {#fdm-http-client-config}

[!DNL Experience Manager Forms] modelo de datos de formulario al integrarse con los servicios web RESTful, ya que el origen de datos ahora incluye configuraciones de cliente HTTP para la optimización del rendimiento. Consulte [Configuración de fuentes de datos](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration).

#### Disponibilidad de la opción Restablecer para cada componente en el modo Diseño (6.5.7.0) {#reset-option-layout-mode}

Ahora puede utilizar la opción restablecer para cada componente en el modo Diseño de un formulario adaptable. Cuando define un diseño de varias columnas para un panel, puede utilizar esta función para restablecer componentes individuales dentro del panel. Consulte [Uso del modo de diseño para cambiar el tamaño de los componentes](../../help/forms/using/resize-using-layout-mode.md#resize-components).

#### Rellene previamente un formulario adaptable en el cliente (6.5.6.0) {#prefill-merge-data-at-client}

Cuando se rellena previamente un formulario adaptable, el servidor [!DNL Experience Manager Forms] combina los datos con un formulario adaptable y le envía el formulario rellenado. De forma predeterminada, la acción de combinación de datos se realiza en el servidor.
Ahora puede configurar el servidor [!DNL Experience Manager Forms] para que [realice la acción de combinación de datos en el cliente](../../help/forms/using/prepopulate-adaptive-form-fields.md) en lugar del servidor. Reduce considerablemente el tiempo necesario para rellenar y procesar formularios adaptables.

#### Integración del modelo de datos de formulario con las API de RESTful en un servidor con implementación de SSL bidireccional (6.5.6.0) {#fdm-integration-rest-apis-two-way-ssl}

[!DNL Experience Manager Forms] el modelo de datos de formulario ahora se puede  [integrar con las API de RESTful en un servidor que tenga implementado](../../help/forms/using/configure-data-sources.md) un SSL bidireccional.

#### Se ha agregado compatibilidad con [!DNL Adobe Sign] Etiquetas de texto en el servicio de Automated forms conversion (6.5.6.0) {#sign-integration-acroform-afcs}

Si un AcroForm incluye [!DNL Adobe Sign] Etiquetas de texto, esos campos ahora se reconocen y representan como campos [!DNL Adobe Sign] en el formulario adaptable convertido mediante [!DNL Automated Forms Conversion service]. Un firmante puede rellenar estos campos al firmar el formulario adaptable.

#### Compatibilidad para convertir PDF forms de color en formularios adaptables (6.5.6.0) {#colored-PDF-forms}

Puede utilizar [!DNL Automated Forms Conversion service] para convertir los PDF forms de color en formularios adaptables.

#### Compatibilidad con los protocolos SMB 2 y SMB 3 (6.5.6.0) {#smb-support}

[!DNL Experience Manager Forms] ahora es compatible con los protocolos SMB 2 y SMB 3.

#### Almacenamiento en caché mejorado para páginas de formularios adaptables traducidas (6.5.6.0) {#enhanced-caching-translated-adaptive-forms}

Ahora puede especificar [configuración regional como selector en la URL del formulario adaptable en lugar de como argumento en la URL del formulario adaptable](../../help/forms/using/supporting-new-language-localization.md). Ayuda a almacenar en caché formularios adaptables traducidos en [!DNL Experience Manager Dispatcher]. En versiones anteriores no se podía almacenar en caché el formulario adaptable traducido. Para obtener información detallada sobre la configuración del almacenamiento en caché para utilizar la configuración regional como selector en la URL del formulario adaptable, consulte [Configuración de la caché del formulario adaptable en Dispatcher](../../help/forms/using/configure-adaptive-forms-cache.md).

#### Guardar el resultado del servicio del modelo de datos de formulario en una variable (6.5.6.0) {#save-fdm-service-to-variable}

El modelo de datos de formulario permite guardar el resultado de un servicio del modelo de datos de formulario en una variable. [!DNL Experience Manager Forms] ahora asigna automáticamente el tipo del servicio del modelo de datos de formulario al tipo de variable.

#### Adjuntar varios archivos para el componente Archivo adjunto (6.5.6.0) {#attach-multiple-files}

Ahora puede [adjuntar varios archivos](../../help/forms/using/introduction-forms-authoring.md) al componente [!UICONTROL Archivo adjunto] de los formularios adaptables.

#### Personalizar las columnas Bandeja de entrada de Adobe Experience Manager (6.5.5.0) {#customize-aem-inbox-columns}

Puede personalizar una bandeja de entrada [!DNL Experience Manager] para cambiar el título predeterminado de una columna, reordenar la posición de una columna y mostrar columnas adicionales basadas en los datos de un flujo de trabajo. Los miembros del grupo `administrators` o `workflow-administrators` pueden personalizar las columnas. Para obtener más información, consulte [Control de administración](../sites-authoring/inbox.md#inbox-admin-control).

![Personalizar columnas de la bandeja de entrada del Experience Manager](assets/customize-columns.gif)

#### Guardar comunicaciones interactivas como borrador (6.5.5.0) {#save-as-draft}

Puede utilizar la interfaz de usuario del agente para guardar uno o más borradores para cada comunicación interactiva y recuperar el borrador más adelante para seguir trabajando en él. Puede especificar un nombre diferente para cada borrador para identificarlo. Para obtener más información, consulte [Guardar comunicaciones interactivas como borrador](../forms/using/prepare-send-interactive-communication.md#save-as-draft).

![Guardar como borrador](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] compatibilidad con el servidor de aplicaciones (6.5.5.0) {#weblogic-support}

Adobe Experience Manager Forms ha agregado compatibilidad con [!DNL Oracle WebLogic 12] para Adobe Experience Manager Forms en JEE. Puede actualizar desde una versión anterior o configurar un nuevo Experience Manager 6.5 Forms en el servidor JEE en [!DNL Oracle WebLogic] 12.2.1.4 y posterior. Posteriormente corresponde a los cambios menores de la versión, donde x en 12.2.1.x se sustituye por un número de versión.

#### Mejoras de accesibilidad (6.5.5.0) {#accessibility-improvements}

Adobe Experience Manager Forms incluye las siguientes mejoras de accesibilidad:

* Cuando un usuario obtiene una vista previa de un formulario adaptable como un formulario HTML, el campo [!UICONTROL Scribble Signature] mantiene el enfoque de tabulación.

* Los mensajes de error mostrados al enviar un formulario adaptable ahora contienen el atributo `aria-describedBy`. El atributo se adjunta a los campos a los que se hace referencia en el mensaje de error. El atributo `aria-describedby` indica las ID de los elementos que describen el objeto. Ayuda a establecer una relación entre las utilidades o los grupos y el texto que los describe.

* Si un formulario adaptable tiene algunos campos obligatorios, el atributo obligatorio se establece en `True` para dichos campos en el esquema de accesibilidad de ARIA.

#### Autenticación basada en certificados X-509 para servicios web basados en SOAP en el modelo de datos de formulario (6.5.5.0) {#x509-based-authentication-soap}

El modelo de datos de formulario ahora es compatible con la autenticación basada en certificados X-509 mientras se utilizan servicios web SOAP como origen de datos. Para obtener más información, consulte [Configuración de servicios web SOAP](../forms/using/configure-data-sources.md#configure-soap-web-services).

#### Otras mejoras clave (6.5.5.0) {#other-improvements}

* Experience Manager 6.5 Forms en JEE Document Security ahora se basa en [!DNL Apache Struts 2].

* Se ha agregado compatibilidad con [!DNL Oracle Real Applications Cluster (RAC) 19c].

#### Generar resultados imprimibles en flujos de trabajo de Experience Manager Forms (6.5.4.0) {#generate-printable-output}

El paso Generar flujo de trabajo de salida imprimible permite integrar un archivo de plantilla de origen con un archivo de datos. Esta integración permite imprimir o guardar diferentes copias del archivo de plantilla. El paso genera una salida PCL, PostScript, ZPL, IPL, TPCL o DPL. Para obtener más información sobre esta función, consulte [Flujo de trabajo centrado en Forms en OSGi - Referencia de pasos](../forms/using/aem-forms-workflow-step-reference.md).

![Generar salida imprimible](assets/generate-print-output-step.gif)

#### Compatibilidad con varias columnas para formularios adaptables y comunicaciones interactivas en el modo Diseño (6.5.4.0) {#multi-column-adaptive-forms}

Ahora puede definir el número de columnas de un panel en formularios adaptables y comunicaciones interactivas. Cambie al modo de diseño para utilizar la nueva opción de varias columnas. Para obtener más información, consulte [Uso del modo Diseño para cambiar el tamaño de los componentes](../forms/using/resize-using-layout-mode.md).

![Diseño de varias columnas](assets/multi-column-layout.gif)

#### Personalizaciones de la bandeja de entrada de Experience Manager (6.5.4.0) {#aem-inbox}

La nueva opción Control de administración permite a los administradores:

* Personalice el texto y el logotipo del encabezado.

* Controle la visualización de los vínculos de navegación disponibles en el encabezado.

La opción Control de administración solo está visible para los miembros del grupo `administrators` o `workflow-administrators` . Para obtener más información sobre esta función, consulte [Su bandeja de entrada](../sites-authoring/inbox.md).

#### Compatibilidad con texto enriquecido en formularios HTML5 (6.5.4.0) {#rich-text-support}

Convierta un campo de texto de un formulario XFA en un campo de texto enriquecido de un formulario HTML5. Para obtener más información, consulte [Diseño de plantillas de formulario para formularios HTML5](../forms/using/designing-form-template.md).

#### Mejoras de accesibilidad (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms incluye las siguientes mejoras de accesibilidad:

* Los lectores de pantalla anuncian correctamente las casillas de verificación, los vínculos, el selector de fechas y los campos de entrada de fecha en un formulario adaptable.

* Cada página de un formulario adaptable ahora incluye un título y una etiqueta de referencia principal.

#### Compartir y solicitar acceso a elementos de la bandeja de entrada de un usuario de Forms Experience Manager (6.5.3.0) {#share-request-access}

Puede compartir los elementos de la bandeja de entrada con otro usuario. Una vez que otro usuario obtiene acceso a los elementos de la bandeja de entrada, el usuario puede reclamar y tomar las medidas adecuadas sobre los elementos compartidos. Del mismo modo, puede solicitar acceso a los elementos de la Bandeja de entrada a otros usuarios. Consulte [Compartir y solicitar acceso a los elementos de la bandeja de entrada de un usuario](../forms/using/configure-shared-queues-osgi.md).

#### Configurar las opciones fuera de la oficina para los elementos de la Bandeja de entrada de un usuario de Forms Experience Manager (6.5.3.0) {#configure-out-of-office}

Si planea estar fuera de la oficina, puede especificar qué sucede con los artículos que se le han asignado durante ese período.
Tiene la opción de especificar una fecha y hora de inicio y una fecha y hora de finalización para que la configuración fuera de la oficina esté en vigor. Puede establecer una persona predeterminada a la que se envían todos los elementos. Consulte [Configuración fuera de Office](../forms/using/configure-out-of-office-settings.md).

#### Generación de varias comunicaciones interactivas mediante la API por lotes para Experience Manager Forms (6.5.3.0) {#generate-multiple-ic}

Puede utilizar la API por lotes para producir varias comunicaciones interactivas a partir de una plantilla. La plantilla es una comunicación interactiva sin datos. La API por lotes combina datos con una plantilla para producir una comunicación interactiva. La API es útil en la producción masiva de comunicaciones interactivas. Por ejemplo, facturas telefónicas, extractos de tarjetas de crédito para varios clientes. Consulte [Generación de varias comunicaciones interactivas mediante la API por lotes](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

<!-- TBD: Check if the wider team released anything in FY21.
-->

## Versiones clave desde [!DNL Adobe Experience Manager] 6.5 SP8 {#key-releases-since-last-sp}

Entre el 25 de febrero de 2021 y el 27 de mayo de 2021, Adobe lanzó lo siguiente, además de los Service Packs:

* [!DNL Adobe Experience Manager] como Cloud Service  [2021.2.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-2-0.html),  [2021.3.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-3-0.html) y  [2021.4.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=en#release-date).

* [[!DNL Experience Manager] aplicación de escritorio 2.1 (2.1.2.0)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

* [Experience Manager Screens: Paquete de funciones 202103](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202103.html?lang=en)

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] Documentación de 6.5](../user-guide/home.md)
* [Notas de la versión generales de [!DNL Adobe Experience Manager] 6.5](release-notes.md)
* [Notas de la versión del Service Pack para [!DNL Adobe Experience Manager] 6.5](sp-release-notes.md)

