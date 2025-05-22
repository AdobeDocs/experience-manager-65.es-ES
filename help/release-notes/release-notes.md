---
title: Notas de la versión para [!DNL Adobe Experience Manager] 6.5
description: Encuentra información de la versión, novedades, instrucciones de instalación y una lista detallada de cambios para  [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 122b5f1f76bd5c338b18102aff15b84ff3fbf0c6
workflow-type: tm+mt
source-wordcount: '5208'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] 6.5 Últimas notas de la versión del paquete de servicio {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.23.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versión del paquete de servicio |
| Fecha | Jueves, 22 de mayo de 2025 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Qué se incluye en [!DNL Experience Manager] 6.5.23.0 {#what-is-included-in-aem-6523}

[!DNL Experience Manager] 6.5.23.0 incluye nuevas características, mejoras clave solicitadas por el cliente y correcciones de errores. También incluye mejoras de rendimiento, estabilidad y seguridad publicadas desde el lanzamiento inicial de la versión 6.5 en abril de 2019. [Instalar este Service Pack](#install) en [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!--
## Key features and enhancements

### Sites {#sites}

* A () -->

<!--
### [!DNL Assets]

* A ()
-->

<!--
### Forms {#forms-sp23}

Key features and enhancements in this release include the following:

#### New GA features in AEM Forms {#ga-aem-forms-sp23}

* A ()

#### New Beta features in AEM Forms {#beta-aem-forms-sp23}
-->

## Se han corregido problemas en el Service Pack 23 {#fixed-issues}

<!-- 6.5.23.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-6523}

#### Accesibilidad {#sites-accessibility-6523}

* Las secciones de lienzo de las páginas del Editor de AEM ahora admiten la accesibilidad total del teclado. Los usuarios pueden activar los títulos de sección y los botones de edición utilizando únicamente el teclado, sin depender del desplazamiento del ratón. Esta actualización garantiza el cumplimiento de WCAG 2.1.1 y mejora la facilidad de uso entre componentes como Teaser, Imagen, Carrusel, Diseño, Deformación de tiempo y Modelos de anotación. (SITES-25256) <!-- 6.5 LTS SP1 -->
* Se ha corregido un problema de accesibilidad en el Editor de páginas de AEM por el que el foco del teclado se restablece de forma inesperada al principio de la barra de herramientas Demográfica después de activar botones como Persona, Carro de compras o Abandonado. Ahora, el enfoque permanece en el botón activado para admitir flujos de trabajo coherentes de navegación mediante el teclado y lector de pantalla. (SITES-25306)
* Se ha corregido un problema crítico de accesibilidad en el Editor de páginas de AEM en el que los elementos de lienzo de varios cuadros de diálogo y modelos (por ejemplo, el carril de recursos o la vista previa de diseño) no se podían utilizar únicamente con un teclado. Todos los elementos de lienzo interactivos ahora admiten la navegación solo mediante el teclado, lo que garantiza el cumplimiento del criterio de éxito 2.1.1 de WCAG 2.1 (SITE-25256)
* Se ha corregido un problema de accesibilidad en la IU del administrador de sitios en el que los elementos de lista interactivos de la ventana emergente Crear usaban funciones ARIA incorrectas. A los elementos que se comportaban como vínculos se les asignaba `role="listitem"` en lugar de `role="menuitem"`, lo que infringía los patrones de diseño de ARIA y confundía a los lectores de pantalla. Las actualizaciones garantizan que todos los componentes de la lista sigan funciones semánticas adecuadas para mejorar la compatibilidad con la tecnología de teclado y asistencia. (SITES-24493)
* Se ha corregido un problema de asociación de etiquetas de accesibilidad para el título de página y los campos de etiquetas. La interfaz de AEM ahora asocia correctamente las etiquetas de accesibilidad con los campos &quot;Título&quot; y &quot;Título de página&quot; al utilizar lectores de pantalla como JAWS. La corrección garantiza una lectura de etiquetas adecuada y mejora el cumplimiento de la ADA en la creación de páginas, las propiedades y los flujos de trabajo de movimiento. (SITES-27149)
* Se ha corregido un problema de accesibilidad con la identificación de tablas en el cuadro de diálogo de permisos. La tabla de permisos de AEM ahora utiliza funciones y atributos ARIA correctos para garantizar que lectores de pantalla como JAWS lo identifiquen correctamente como una tabla. La corrección mejora el cumplimiento de la accesibilidad y garantiza que los usuarios reciban anuncios de contenido y navegación precisos. (SITES-27140)
* Se ha corregido la falta de una etiqueta visual para los campos de entrada de comentarios en la cronología. Se han corregido las etiquetas visuales que faltaban para los campos de entrada de &quot;comentario&quot; en la sección de cronología para mejorar la accesibilidad. La actualización garantiza que los lectores de pantalla puedan anunciar con precisión las etiquetas de campo. Esta experiencia mejora la navegación y el envío de formularios para todos los usuarios, especialmente las personas que dependen de las tecnologías de asistencia. (SITES-26903)
* Se ha corregido la accesibilidad del teclado para el botón de puntos suspensivos en comentarios de cronología. Se ha habilitado la navegación mediante el teclado para el botón de puntos suspensivos (tres puntos) junto a los comentarios en la sección de cronología. Los usuarios ahora pueden acceder al botón e interactuar con él mediante la tecla de tabulación, lo que mejora la accesibilidad para los usuarios que dependen de la navegación solo mediante teclado. (SITES-26891)
* Se han mejorado los anuncios de NVDA/Narrador para resultados de búsqueda en cuadros de diálogo de selección. Se ha actualizado el cuadro de diálogo Abrir selección para anunciar si se encuentran o no resultados de búsqueda al utilizar lectores de pantalla, como NVDA o Narrador. Esta mejora ayuda a los usuarios que dependen de tecnologías de asistencia a comprender el resultado de sus acciones de búsqueda sin necesidad de confirmación visual. (SITES-26883)
* Se ha corregido la función ARIA del icono de puntos suspensivos junto al campo de entrada de comentarios. Se ha actualizado el icono de puntos suspensivos (tres puntos) junto al campo de entrada del comentario para utilizar la función ARIA correcta, lo que garantiza que los lectores de pantalla puedan identificar el elemento con precisión. Esta mejora mejora mejora el cumplimiento de la accesibilidad y la experiencia de los usuarios que dependen de las tecnologías de asistencia. (SITES-26881)
* Se han corregido atributos ARIA no válidos en los componentes de Coral UI. Se han actualizado los componentes de la interfaz de usuario de Coral para garantizar que todos los atributos ARIA utilicen valores válidos, mejorando la accesibilidad y el cumplimiento. En particular, se abordaron casos en los que valores no válidos como `aria-modal="dialog"` se asignaron incorrectamente. Esta mejora permite a los lectores de pantalla interpretar correctamente los elementos del cuadro de diálogo, lo que mejora la accesibilidad para los usuarios que dependen de tecnologías de asistencia. (SITES-26873)
* Se ha mejorado la visibilidad y la información de herramientas de los iconos en escenarios de flujo. Se ha mejorado el comportamiento de reflujo para garantizar que la información sobre herramientas se muestre correctamente en los iconos **Descargar**, **Volver a procesar recursos** y **Finalizar compra**. Se centró en un problema de accesibilidad en el que los iconos y sus etiquetas se volvían invisibles cuando cambiaba el tamaño de la ventanilla móvil o la configuración de zoom del explorador. Esta corrección admite usuarios con visión reducida al mantener la visibilidad y proporcionar descripciones de iconos adecuadas durante el reflujo. (SITES-26871)

#### Interfaz de usuario de administrador{#sites-adminui-6523}

Se ha corregido la excepción del servicio URL del editor universal con extremos del externalizador faltantes. El servicio URL del editor universal ahora administra los extremos del externalizador local, de publicación o de autor que faltan sin producir excepciones. Los usuarios administradores pueden abrir el Editor de páginas correctamente incluso cuando algunas configuraciones de Externalizer están incompletas. (SITES-28877) <!-- LTS -->

#### IU clásica{#sites-classicui-6523}

* Problema en los cuadros de diálogo de la IU clásica en el que, al cambiar un botón, se ocultaba un área de texto y no se volvía a mostrar en los clics posteriores. La corrección garantiza que el área de texto vuelva a aparecer correctamente cuando se activa, restaurando el comportamiento esperado y evitando interrupciones en los flujos de trabajo del cuadro de diálogo dinámico. (SITES-30230)
* Se ha corregido la funcionalidad del buscador de recursos de imagen de la IU clásica dañada después de la actualización del Service Pack 22. El buscador de recursos de imagen de la IU clásica ahora gestiona correctamente los nombres de recursos que contienen espacios o caracteres especiales. Esta actualización garantiza que el buscador de recursos codifique los nombres de archivo correctamente, lo que evita errores de búsqueda y permite a los autores localizar y seleccionar recursos de imagen sin errores. (SITES-29151)

#### [!DNL Content Fragments]{#sites-contentfragments-6523}

* Se corrigió un error en la prueba de validación de `DeleteVariationIT.testUpdateBasic`. La prueba `DeleteVariationIT.testUpdateBasic` ya no falla durante las ejecuciones de validación del Service Pack. La corrección corrige un problema de asignación de texto que falta en la lógica de administración de JSON, lo que garantiza la estabilidad de la prueba y evita interrupciones de prueba innecesarias. (SITES-28022)
* AEM ahora evita la degradación del rendimiento causada por el formato incorrecto de los metadatos de XMP en los recursos de imagen. Los Assets que contienen nombres de propiedad de XMP no válidos o no compatibles, como los que tienen segmentos numéricos o estructuras no calificadas, ya no almacenan en déclencheur los registros de advertencia repetidos durante el procesamiento. El sistema filtra los metadatos problemáticos para garantizar que la ingesta y validación de recursos se complete sin errores. (SITES-30683) &lt;!— AEM 6.5 LTS SP1>


<!-- #### [!DNL Content Fragments] - Admin{#sites-admin-6523}

* A () -->


#### [!DNL Content Fragments]: editor de fragmentos{#sites-fragments-editor-6523}

Otros autores aún pueden publicar fragmentos de contenido incluso cuando otro autor los desproteja, lo que es contrario al comportamiento deseado de la función de cierre de compra. Esta corrección evita que otros usuarios vean o utilicen los botones de publicación en la interfaz de creación cuando se retira un fragmento de contenido. (SITES-30578) <!-- LTS -->

#### [!DNL Content Fragments] - API de GraphQL {#sites-graphql-api-6523}

Se ha corregido un error QueryValidationError de GraphQL con esquemas de fragmentos de contenido. Al actualizar el paquete `cq-dam-cfm-graphql` se corrigen los errores de validación de esquema al utilizar referencias a fragmentos de contenido. La corrección garantiza que las consultas de GraphQL funcionen correctamente sin requerir la realineación manual del esquema o la republicación después de las implementaciones de paquetes. (SITES-27001) <!-- LTS -->


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6523}

* A () -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6523}

* A () -->


#### Consola de componente{#sites-component-console-6523}

Mejoras en la carga de la página Uso del componente Live. Optimiza la página &quot;Uso activo de componentes&quot; en AEM para evitar que aparezcan filas vacías al desplazarse por conjuntos de datos grandes. Los usuarios que cargan componentes con referencias de uso extensas ahora pueden experimentar una carga de datos continua sin espacios innecesarios ni entradas vacías. Esta experiencia mejora la navegación de páginas, la precisión del seguimiento y la eficacia de la administración en la creación de informes de uso de componentes. (SITES-26454)

#### Servidor principal{#sites-core-backend-6523}

* Se ha corregido un error en la lista de recursos del Buscador de contenido debido a nombres de recursos no válidos. El buscador de contenido ahora gestiona correctamente los nombres de los recursos con caracteres no codificables. La lista de recursos en el Editor de páginas ya no falla ni genera excepciones al encontrar recursos con nombres problemáticos. (SITES-28722)
* Problema en el cual el componente `SearchPathLimiter` generaba entradas de registro excesivas al imprimir mensajes en el nivel de ERROR para cada invocación. Este comportamiento comenzó después del Service Pack 17 y provocó problemas de rendimiento debido a los volúmenes de registro extremadamente altos. La corrección reduce el nivel de registro a DEPURACIÓN, lo que reduce significativamente el ruido de registro y mejora la supervisión del sistema y la eficacia del diagnóstico. (SITES-29835)
* Los metadatos de XMP con formato incorrecto desencadenaron un error durante el procesamiento de los recursos de imagen en `ValidationDataServlet`. La corrección garantiza la administración de metadatos compatible y evita el análisis repetido de propiedades no válidas. (SITIO-30683) <!-- LTS -->


<!-- #### Core Components{#sites-core-components-6523}

* A () -->

<!-- #### Campaign integration{#sites-campaign-integration-6523}

* A () -->

<!-- #### Experience Fragments{#sites-experiencefragments-6523}

* A () -->

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6523}

* A () -->


#### Lanzamientos{#sites-launches-6523}

* Se ha corregido una visualización de fecha de lanzamiento incorrecta entre el 25 de diciembre y el 31 de diciembre. La interfaz de usuario de Lanzamientos ahora muestra fechas entre el 25 de diciembre y el 31 de diciembre con el año correcto. La corrección garantiza que las fechas ya no muestren incorrectamente el año siguiente, lo que evita confusiones durante la planificación y programación de la campaña. (SITES-28706)
* Se han corregido las plantillas de AEM Launch rotas después de la actualización del Service Pack 22. Las plantillas de AEM Launch ahora se cargan correctamente después de una actualización de Service Pack 22. La corrección corrige los datos no válidos en las configuraciones de lanzamiento internas, lo que permite a los usuarios ver, editar y crear Lanzamientos sin errores ni campos que falten. (SITES-28504)


<!-- #### Link Checker{#sites-link-checker-6523}

* A () -->

<!-- #### MSM - Live Copies{#sites-msm-live-copies-6523}

* A () -->


#### Editor de página{#sites-pageeditor-6523}

* Se ha corregido un problema de carga de AssetPicker en resoluciones de pantalla más bajas. El Selector de recursos ahora carga los recursos correctamente cuando los usuarios se desplazan a resoluciones de pantalla más bajas (1728×1117 o menos). Los usuarios ya no experimentan la falta de recursos al desplazarse, lo que mejora la administración de recursos en diferentes puntos de interrupción del dispositivo. (SITES-28065)
* Se ha corregido el anuncio del lector de pantalla que faltaba para las acciones de bloqueo y desbloqueo de página. El editor de páginas ahora anuncia correctamente el mensaje &quot;Información: La página se ha bloqueado/desbloqueado&quot; cuando los usuarios activan el botón de bloqueo/desbloqueo. La corrección mejora el cumplimiento de la accesibilidad y garantiza que los usuarios del lector de pantalla reciban actualizaciones dinámicas durante la edición de páginas. (SITES-27143)
* Se ha mejorado el comportamiento de enfoque de teclado para las acciones de componentes en AEM Authoring. Se ha mejorado la navegación mediante el teclado en la herramienta de creación de AEM para garantizar que el enfoque permanezca en el componente recién creado o seleccionado después de acciones como Configurar, Eliminar o Convertir. Anteriormente, el enfoque cambiaba a la parte superior de la página, lo que provocaba problemas de cumplimiento de la accesibilidad. Esta actualización mejora la experiencia del usuario para los usuarios de tecnología de teclado y asistencia. Para ello, mantiene la progresión del enfoque lógico dentro del flujo de trabajo de edición. (SITES-26549)
* Se ha mejorado la navegación por pestañas en los cuadros de diálogo de Autor. Mejora la navegación mediante el teclado en los cuadros de diálogo de AEM Author, ya que permite a los usuarios seguir presionando la tabulación hacia delante después de alcanzar el cuadro de edición Descripción. Anteriormente, el reventado de foco en el campo Descripción bloqueaba una navegación adicional sin utilizar combinaciones de teclas especiales. La actualización garantiza que los usuarios puedan desplazarse por los campos sin problemas utilizando solo el tabulador, lo que mejora el cumplimiento de la accesibilidad y la experiencia del usuario. (SITES-26524)
* Se introdujo una regresión en el paquete de servicio 22 de AEM 6.5 que impedía a los usuarios incluir espacios en los títulos de Launch. La corrección restaura la capacidad de usar espacios, lo que permite a los equipos definir y organizar los nombres de Launch de forma más flexible, en línea con el comportamiento esperado. (SITES-29414)
* Se ha corregido el problema de cambio de tamaño de los componentes dentro de Contenedores de diseño después de ocultar o mostrar acciones. El editor de páginas ahora calcula correctamente los valores de columna después de ocultar y mostrar un contenedor de diseño. Los usuarios pueden cambiar el tamaño de los componentes sin errores y las columnas se muestran correctamente durante las acciones de cambio de tamaño. (SITES-28463)
* Se ha corregido un error de colocación del botón Árbol de contenido en el Editor de páginas. Ahora, el editor de páginas coloca correctamente el botón de configuración del árbol de contenido en el cuadro de diálogo &quot;Encabezado Teaser&quot; deseado, en lugar de en la sección incorrecta. La corrección actualiza el CSS para el cuadro de diálogo Árbol de contenido para que utilice `top:0` en lugar de `bottom:0`, lo que garantiza la correcta ubicación del botón. (SITES-28448)


<!-- #### Replication{#sites-replication-6523}

* A () -->


#### Editor de texto enriquecido{#sites-rte-6523}

Corregir etiquetas `<br>` inesperadas en el Editor de texto enriquecido con el modo de pegado de texto sin formato. El Editor de texto enriquecido ahora administra correctamente las operaciones de cortar y pegar al utilizar texto sin formato `defaultPasteMode`. La corrección evita la inserción de etiquetas `<br>` inesperadas cuando los usuarios cortan y pegan texto dentro de campos RTE, lo que garantiza un formato limpio durante la edición de contenido. (SITES-27780)

#### Editor universal {#sites-universal-editor-6523}

* Cuando se envían varias solicitudes que contienen el parámetro query a AEM, es posible que la cookie del token de inicio de sesión no se devuelva a tiempo, lo que puede provocar un inicio de sesión fallido. (SITES-30659) <!-- LTS -->
* Para garantizar la compatibilidad y compatibilidad con los controladores SAML, debe configurar la propiedad `service.ranking` para que el controlador `Query Token Auth` ejecute *antes* del controlador `SAML Auth`. (SITES-29684)

### [!DNL Assets]{#assets-6523}

* Los siguientes problemas se producen en la página de navegación local de [!DNL AEM] (6.5.22.0) después de seleccionar ![Assets](/help/assets/assets/Smock_Asset_18_N.svg)**[!UICONTROL Assets ]**, ir a la carpeta**[!UICONTROL  Buscar Adobe Stock ]**y seleccionar una imagen de archivo:
   * La imagen de archivo seleccionada no se puede autorizar y guardar porque al hacer clic en **[!UICONTROL Licencia y guardar]** se muestra una lista desplegable vacía.
   * Si se selecciona la imagen de Stock o se vuelve a introducir la URL de la página de stock, se redirige a la página principal de [!DNL AEM], lo que impide el acceso a la imagen de Adobe Stock. (ASSETS-48687)
* Problemas al administrar carpetas si el nombre de la carpeta incluye un `/` en su nombre en la página de navegación local (6.5.22.0) de [!DNL AEM]. (ASSETS-46740)
* En [!DNL AEM] 6.5, la página de detalles del recurso no se carga desde la vista ![Colección](/help/assets/assets/Smock_Collection_18_N.svg)**[!UICONTROL Colecciones ]**debido a un uso elevado de la memoria. (ASSETS-46738)
* Problemas de integración con [!DNL InDesign] como el servicio `Day CQ DAM Mime Type OSGI` identifica incorrectamente [!DNL InDesign] archivos como `x-adobe-indesign` en lugar de `x-indesign`. (ASSETS-45953)
* La fuga de sesión de [!DNL AEM 6.5.21] se remonta al paso de flujo de trabajo de **[!UICONTROL Publicación programada en Brand Portal]** listo para usar. (ASSETS-44104)
* **[!UICONTROL Memoria insuficiente (OOM)]** errores que se muestran en [!DNL AEM] al procesar y publicar imágenes. Este problema se debió a métodos obsoletos en flujos de trabajo, como **[!DNL Dam Asset update]** y **[!DNL Dynamic Media: Reprocess assets]**. (ASSETS-43343)
* Después de realizar un cambio menor, como actualizar el título, vuelva a abrir y guardar **[!DNL Connected Assets configuration]** en la instancia local de Sites. A continuación, la instancia remota pierde su conexión con la instancia local. Como resultado, no puede establecer comunicación con la instancia local de Sites. (ASSETS-44484)
* En [!DNL AEM 6.5.21], cuando se cancela la carga de un recurso en la vista de lista y se realiza una segunda carga, [!DNL AEM] muestra un error **[!UICONTROL 0 de recursos NaN cargados]**. (ASSETS-44124)

#### [!DNL Dynamic Media]{#assets-dm-6523}

Se ha agregado una propiedad de metadatos (`jcr:content/metadata/dam:scene7SmartCropStatus`) a los recursos para identificar las generaciones de recortes inteligentes con errores. Permite la búsqueda, el filtrado y el reprocesamiento eficientes de recursos con problemas de recorte inteligente mediante flujos de trabajo manuales o automatizados. (ASSETS-46237)

#### [!DNL Dynamic Media] - Modo híbrido {#assets-dm-hybrid-6523}

##### Dynamic Media: paquete de complemento híbrido (AEM 6.5.23 y posterior)

A partir del paquete de servicio 23 de AEM 6.5, hay un nuevo paquete de complemento disponible para el modo híbrido de Dynamic Media. Este paquete incluye el paquete `cq-scene7-imaging` específicamente compatible con el modo de ejecución híbrido de Dynamic Media.

**Corrección de clave incluida**

Se ha corregido un problema en las implementaciones híbridas de Dynamic Media en las que las actualizaciones del parámetro `catalog.expiration` en `/conf/global/settings/dam/dm/imageserver` no se reflejaban en las direcciones URL del servidor o del autor, a pesar de que la replicación se realizaba correctamente sin errores. La actualización garantiza valores de caducidad coherentes entre CRX/DE, la respuesta del servidor y las direcciones URL de envío público. A su vez, mejora el comportamiento de la caché y la fiabilidad de las transformaciones de imagen. (ASSETS-44837)

**Consideraciones importantes**

* El paquete `cq-scene7-imaging` de la instalación base de AEM 6.5.23 (y versiones posteriores) es *no compatible* con el modo de ejecución híbrido de Dynamic Media.
* La instalación del Service Pack 23 (y versiones posteriores) por sí sola *no actualiza automáticamente* el paquete `cq-scene7-imaging` existente en las instancias de AEM configuradas para Dynamic Media - Híbrido (modo de ejecución `-r dynamicmedia`).

**Cuándo instalar el paquete de complementos híbridos**

* Al actualizar directamente a AEM 6.5.23 (y posterior) desde AEM 6.5.19 o anterior.
* Cuando necesite correcciones específicas de la funcionalidad híbrida de Dynamic Media.
* Al implementar una nueva instancia de Dynamic Media híbrida directamente desde AEM 6.5 GA (disponibilidad general) a Service Pack 23 (y posterior).

**Descargar paquete híbrido de complementos**

El paquete de complementos híbrido está disponible en Distribución de software y es de acceso público cuando se lanza AEM 6.5.23 oficialmente el jueves, 22 de mayo de 2025.

[Descargar paquete de complementos híbridos de Dynamic Media](https://author-p11553-e21065.adobeaemcloud.com/ui#/aem/assetdetails.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cq-dam-delivery-65-hybrid-addon-1.0.zip).


### [!DNL Forms]{#forms-6523}

Las correcciones de [!DNL Experience Manager] Forms se entregan mediante un paquete de complementos independiente una semana después de la fecha de lanzamiento programada del paquete de servicio [!DNL Experience Manager]. En este caso, el lanzamiento del paquete de complementos de Forms de AEM 6.5.23.0 está programado para el jueves 29 de mayo de 2025. Se ha añadido una lista de correcciones y mejoras de Forms a esta sección después de la versión.

#### Captcha de Forms {#forms-captcha-6523}

* Se ha mejorado las alertas reCAPTCHA en el Forms adaptable al actualizar los códigos de error de envío a 400. Además, se han refinado las alertas de registro para distinguir entre tiempos de espera, caducidades y errores de detección de bots, lo que mejora la precisión de la resolución de problemas y la observabilidad del sistema. (FORMS-19240)
* Se cerró una instancia de `ResourceResolver` sin cerrar en `ReCaptchaConfigurationServiceImpl` para evitar posibles fugas de recursos y mejorar la estabilidad del sistema al utilizar integraciones reCAPTCHA en AEM Forms. (FORMS-19242)
* Se ha mejorado la administración de la configuración de CAPTCHA para AEM Forms, al garantizar que la configuración correcta se vincula a cada formulario cuando existen varias entradas en la carpeta `/conf/global`. Evita el uso no intencionado de configuraciones de CAPTCHA incorrectas cuando el contenedor de configuración no está seleccionado explícitamente. (FORMS-19239)


<!--
#### XMLFM {#forms-xmlfm-6523}

* A () -->

<!--
#### [!DNL Adaptive Forms] {#adaptive-forms-6523}

* A () -->

<!--
#### [!DNL Forms Designer] {#forms-designer-6523}

* A () -->


### Foundation {#foundation-6523}

* Se ha corregido un problema en los titulares de alertas de Coral por el que el color del texto aparecía en blanco en lugar de negro después de actualizar al Service Pack 21. Garantiza que se aplique un estilo correcto para mantener el contraste y la legibilidad adecuados de los mensajes de alerta en toda la interfaz. (NPR-42359)
* Se ha agregado compatibilidad con la integración de OAuth en la configuración de etiquetas inteligentes para alinearla con la obsolescencia de JWT (token web JSON). Garantiza la funcionalidad continua de las funciones de etiquetas inteligentes mediante métodos de autenticación actualizados. (NPR-42296)

#### Apache Felix {#foundation-apachefelix-6523}

Se ha corregido una NullPointerException que se producía al cargar archivos de clave privada en un campo de propiedad de tipo binario en CRX, restaurando la compatibilidad presente a través del Service Pack 16. Permite flujos de trabajo seguros de carga de archivos clave en AEM Managed Services sin errores del servidor ni interrupciones en los procesos de renovación de certificados. (CQ-4359178)


<!--
#### Campaign{#foundation-campaign-6523}

* A () -->

<!--
#### Cloud Services{#foundation-cloudservices-6523}

* A () -->

<!--
#### Communities {#foundation-communities-6523}

* A () -->

<!--
#### Content distribution{#foundation-content-distribution-6523}

* A () -->

<!--
#### CRX {#foundation-crx-6523}

* A () -->


#### Granite{#foundation-granite-6523}

* Se han resuelto ciclos de dependencia OSGi entre servicios de scripts de Apache Sling que causaban retrasos o errores al cargar páginas de HTML después de actualizar a Service Pack 21. Se han actualizado las referencias de servicio interno para eliminar las dependencias cíclicas que involucran a `SightlyScriptingEngineFactory` y los componentes relacionados, lo que mejora la confiabilidad y el comportamiento de inicio del motor de scripts. (GRANITE-56808)
* Se han actualizado los scripts de uso de JS en Apache Sling para cargar solo bajo demanda en lugar de al inicio con ansiedad, lo que elimina el contenido de subprocesos y reduce el riesgo de que los servidores de publicación no respondan durante la carga. Este cambio mejora la estabilidad del servidor y los tiempos de respuesta durante situaciones de alto tráfico al evitar el bloqueo de recursos provocado por la resolución anticipada de scripts. (GRANITE-56611)
* Se ha corregido un problema en AEM Omnisearch por el cual los marcadores de posición de los campos de entrada se muestran incorrectamente como etiquetas, lo que provoca confusión visual. Garantiza la correcta representación de los marcadores de posición en los campos de filtro, manteniendo un comportamiento de formulario coherente y accesible. (GRANITE-51791)
* Se ha resuelto un error de servidor que se activaba al seleccionar más de 30 CFM (modelos de fragmentos de contenido) con referencias de varios campos en el editor de modelos de fragmentos de contenido. Se ha mejorado el componente de sugerencia de filtros para admitir operaciones POST. Esta capacidad permite el manejo adecuado de grandes conjuntos de referencias durante la creación de fragmentos de contenido y mejorar la estabilidad para configuraciones de modelos de gran volumen. (GRANITE-57164)
* Se ha resuelto un problema en CFM en el cual al hacer clic en cerca de una casilla de verificación se alternaba su estado de forma involuntaria. Se han actualizado los estilos para restringir la activación de clics estrictamente al elemento checkbox, lo que evita interacciones accidentales del usuario y mejora la facilidad de uso y accesibilidad del formulario. (GRANITE-52384)


<!--
#### Integrations{#foundation-integrations-6523}

* A () -->


#### Jetty{#foundation-jetty-6523}

Se ha resuelto un problema en el cual la validación SNI bloqueaba las llamadas de API a través de HTTPS para clientes de AEM que usaban configuraciones SSL de Dispatcher con encabezados de host personalizados. Presenta una opción para deshabilitar la validación de SNI como parte de la configuración de Jetty, habilitando la compatibilidad con configuraciones específicas de proxy inverso donde `mod_proxy` no es factible. (NPR-42614)


<!--
#### Localization{#foundation-localization-6523}

* A () -->

<!--
#### Oak {#foundation-oak-6523}

* A () -->


#### Plataforma{#foundation-platform-6523}

* Se ha corregido un comportamiento incoherente de combinación de etiquetas asegurándose de que el valor de etiqueta combinado siempre se muestre correctamente en los recursos, independientemente de si las etiquetas se crean en línea o mediante el método de creación de etiquetas estándar. Evita que los valores residuales de `EN:title` campos anulen la visualización de la etiqueta combinada. (CQ-4358812)
* Se ha corregido la codificación repetida de caracteres ampersand en los valores de etiqueta dentro del cuadro de diálogo de edición de etiquetas. Evita que se añadan entidades &quot;&amp;&quot; adicionales en cada guardado, lo que garantiza que los valores de las etiquetas permanezcan limpios y coherentes en todas las ediciones y evita errores de visualización en el contenido creado. (CQ-4359048)
* Se ha resuelto un error `ClassCastException` que impide la entrega de correo electrónico en el envío de formularios adaptables en AEM 6.5, que se ejecuta en WebSphere®. La corrección habilita la transmisión de correo electrónico correcta al garantizar la compatibilidad entre `com.sun.mail.handlers.text_plain` y `java.activation.DataContentHandler`, alineándose con la configuración del controlador de correo esperada por los entornos de WebSphere®. (NPR-42500)
* Se ha mejorado la gestión de errores en el Administrador de paquetes asegurándose de que AEM muestre un mensaje claro cuando falle la instalación y de que la respuesta de error esté vacía. Esta corrección evita errores silenciosos y ayuda a una depuración más rápida durante la implementación de paquetes. (NPR-42375)

<!--
#### Security{#foundation-security-6523}

* A -->

<!--
#### Sling{#foundation-sling-6523}

* A () -->


#### Traducción{#foundation-translation-6523}

Se ha corregido un problema de NullPointerException (NPE) que se activaba al actualizar fragmentos de contenido en flujos de trabajo mediante **Actualizar copia de idioma**. Esta corrección garantiza que los flujos de trabajo no entren en un estado de error ni permanezcan atascados en un estado de ejecución al editar contenido vinculado a referencias de traducción. (NPR-42115)

#### Interfaz de usuario{#foundation-ui-6523}

Agrega los atributos `title` que faltan a los botones del cuadro de diálogo de la interfaz de usuario de Coral, como **Listo** y **Cancelar** en los cuadros de diálogo de edición de componentes para mejorar la accesibilidad y habilitar la validación automatizada. Garantiza que los botones conserven los atributos esperados en el procesamiento de marcado, lo que evita errores en las pruebas de IU basadas en Selenium. (NPR-42412)

#### WCM{#foundation-wcm-6523}

Se ha corregido un problema que impedía que se agregaran páginas a trabajos de traducción al usar **Actualizar copia de idioma** en entornos con Service Pack 19 o posterior. Garantiza que los flujos de trabajo de traducción se desarrollen según lo esperado, lo que permite una transferencia de página adecuada entre copias de idioma sin intervención manual. (CQ-4357929)

#### Flujo de trabajo{#foundation-workflow-6523}

Se ha resuelto un problema en `EmailNotificationServiceProcessor` en el cual el método `getSegmentId` devolvía `null` después de la implementación de la revisión, lo que provocaba que los déclencheur de correo electrónico fallaran durante el procesamiento del flujo de trabajo. Restaura la lógica de resolución de ID de segmento correcta asegurándose de que el procesador recupera los valores `SegmentInfo` necesarios para admitir flujos de trabajo de notificaciones de correo electrónico en las instancias de AEM. (CQ-4359755)


## Instalar [!DNL Experience Manager] 6.5.23.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.23.0 requiere [!DNL Experience Manager] 6.5. Consulte [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas. <!-- UPDATE FOR EACH NEW RELEASE -->
* La descarga del Service Pack está disponible en Adobe [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip).
* En una implementación con MongoDB y varias instancias, instale [!DNL Experience Manager] 6.5.23.0 en una de las instancias de creación mediante el Administrador de paquetes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe no recomienda quitar ni desinstalar el paquete [!DNL Experience Manager] 6.5.23.0. Como tal, antes de instalar el paquete, debe crear una copia de seguridad de `crx-repository` en caso de que deba revertirla. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Instalar el Service Pack en [!DNL Experience Manager] 6.5{#install-service-pack}

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (cuando la instancia se haya actualizado desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de realizar la instalación, realice una instantánea o una copia de seguridad nueva de la instancia de [!DNL Experience Manager].

1. Descargar el Service Sack de [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra el Administrador de paquetes y seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y luego seleccione **[!UICONTROL Instalar]**.

1. Para actualizar el conector S3, detenga la instancia después de la instalación del Service Pack, sustituya el conector existente por un nuevo archivo binario proporcionado en la carpeta de instalación y reinicie la instancia. Consulte [Almacén de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo de la interfaz de usuario del administrador de paquetes a veces se cierra durante la instalación del paquete de servicio. Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete actualizador antes de asegurarse de que la instalación se haya realizado correctamente. Normalmente, este problema se produce en el explorador [!DNL Safari], pero puede ocurrir de forma intermitente en cualquier explorador.

**Instalación automática**

Existen dos métodos diferentes que puede utilizar para instalar [!DNL Experience Manager] 6.5.23.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en la carpeta `../crx-quickstart/install` cuando el servidor esté disponible en línea. El paquete se instala automáticamente.
* Use la API [HTTP del Administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que se instalen los paquetes anidados.

>[!NOTE]
>
>Experience Manager 6.5.23.0 no admite la instalación de Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar la instalación**

Para conocer las plataformas que están certificadas para funcionar con esta versión, consulte los [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.23.0)` en [!UICONTROL Productos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos los paquetes OSGi están **[!UICONTROL ACTIVOS]** o **[!UICONTROL FRAGMENTOS]** en la consola OSGi (use la consola web: `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es de la versión 1.22.20 o posterior (utilice la consola web: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### Instalar Service Pack para [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Para obtener instrucciones para instalar el Service Pack en Experience Manager Forms, consulte [Instrucciones de instalación del Service Pack de Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La funcionalidad Formularios adaptables, disponible en [AEM 6.5 Inicio rápido](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), está diseñada únicamente para la exploración y la evaluación. Para su uso en producción, es esencial obtener una licencia válida para AEM Forms, ya que la funcionalidad Formularios adaptables requiere una licencia adecuada.

### Instalación del paquete de índice de GraphQL para fragmentos de contenido de Experience Manager{#install-aem-graphql-index-add-on-package}

Los clientes que usen GraphQL deben instalar el [fragmento de contenido de Experience Manager con el paquete de índice 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip) de GraphQL.

Al hacerlo, puede añadir la definición de índice necesaria en función de las funciones que utilizan realmente.

Si no se instala este paquete, las consultas de GraphQL pueden ser lentas o dar error.

>[!NOTE]
>
>Instale este paquete solo una vez por instancia; no es necesario reinstalarlo con cada Service Pack.

### UberJar{#uber-jar}

UberJar para [!DNL Experience Manager] 6.5.23.0 está disponible en el [repositorio de Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.22/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para usar UberJar en un proyecto de Maven, consulta [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluye la siguiente dependencia en el POM de tu proyecto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.23</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar y los demás artefactos relacionados están disponibles en el repositorio de Maven Central en lugar del repositorio Maven público de Adobe (`repo.adobe.com`). Se cambió el nombre del archivo principal de UberJar a `uber-jar-<version>.jar`. Por lo tanto, no hay `classifier`, con `apis` como valor, para la etiqueta `dependency`.



## Funciones en desuso y eliminadas{#removed-deprecated-features}

Consulte [Funciones obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md/) para obtener una lista detallada de todas las funciones obsoletas o eliminadas de AEM 6.5.

### Editor de SPA  {#spa-editor}

[El editor de SPA](/help/sites-developing/spa-overview.md) ha quedado obsoleto para nuevos proyectos a partir de la versión 6.5.23 de AEM 6.5. El Editor SPA sigue siendo compatible con los proyectos existentes, pero no debe utilizarse para nuevos proyectos.

Los editores preferidos para administrar contenido sin encabezado en AEM ahora son:

* [El editor universal](/help/sites-developing/universal-editor/introduction.md) para la edición visual.
* [El editor de fragmentos de contenido](/help/sites-developing/universal-editor/introduction.md) para la edición de contenido sin encabezado basada en formularios.

## Problemas conocidos{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **Relacionado con Oak**
En Service Pack 13 y versiones posteriores, ha comenzado a aparecer el siguiente registro de errores que afecta a la caché de persistencia:

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  O bien

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  Para resolver esta excepción, haga lo siguiente:

   1. Eliminar las dos carpetas siguientes de `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. Instale el Service Pack o reinicie Experience Manager as a Cloud Service.
Las nuevas carpetas de `cache` y `diff-cache` se crean automáticamente y ya no experimenta una excepción relacionada con `mvstore` en `error.log`.

* Actualice las consultas de GraphQL que puedan haber utilizado un nombre de API personalizado para el modelo de contenido para utilizar el nombre predeterminado del modelo de contenido en su lugar.

* Una consulta GraphQL puede utilizar el índice `damAssetLucene` en lugar del índice `fragments`. Esta acción puede dar como resultado consultas de GraphQL que fallan o que tardan mucho tiempo en ejecutarse.

  Para corregir el problema, `damAssetLucene` debe estar configurado para incluir las dos propiedades siguientes en `/indexRules/dam:Asset/properties`:

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  Una vez modificada la definición del índice, se requiere una reindexación (`reindex` = `true`).

  Después de estos pasos, las consultas de GraphQL deberían funcionar más rápido.

* Al intentar mover, eliminar o publicar fragmentos de contenido, sitios o páginas, hay un problema cuando se recuperan las referencias de fragmentos de contenido. La consulta en segundo plano falla. Es decir, la funcionalidad no funciona.
Para garantizar el funcionamiento correcto, debe agregar las siguientes propiedades al nodo de definición de índice `/oak:index/damAssetLucene` (no se requiere la reindexación):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Si actualiza la instancia de [!DNL Experience Manager] de la versión 6.5.0 a la 6.5.4 al Service Pack más reciente de Java™ 11, verá `RRD4JReporter` excepciones en el archivo `error.log`. Para detener las excepciones, reinicie la instancia de [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Los usuarios pueden cambiar el nombre de una carpeta en una jerarquía de [!DNL Assets] y publicar una carpeta anidada en [!DNL Brand Portal]. Sin embargo, el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Durante la instalación de [!DNL Experience Manager] 6.5.x.x se pueden mostrar los siguientes errores y mensajes de advertencia:
   * &quot;Cuando la integración de Adobe Target se configura en [!DNL Experience Manager] mediante la API de Target Standard (autenticación IMS) y, a continuación, se exportan fragmentos de experiencias a Target, se crean tipos de ofertas incorrectos. En lugar de &quot;Fragmento de experiencia&quot;/fuente &quot;Adobe Experience Manager&quot;, Target crea varias ofertas con el tipo &quot;HTML&quot;/fuente &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en `granite/operations/maintenance`.
   * La validación del lado del servidor de formularios adaptables falla cuando se utilizan funciones de agregado como SUM, MAX y MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : no se encontraron ventanas de mantenimiento en `granite/operations/maintenance`.
   * El punto interactivo de una imagen interactiva de Dynamic Media no está visible al obtener una vista previa del recurso a través del visor de titulares de ventas.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : tiempo de espera agotado para completar el cambio de registro sin registrar.

* A partir de AEM 6.5.15, el motor Rhino JavaScript proporcionado por el paquete ```org.apache.servicemix.bundles.rhino``` presenta un nuevo comportamiento de elevación. Los scripts que utilizan el modo estricto (```use strict;```) deben declarar sus variables correctas. De lo contrario, no se ejecutan y terminan generando un error de tiempo de ejecución.

* La instalación del contenido listo para usar relacionado con el etiquetado mediante un paquete de actualización oficial restablece la propiedad de idiomas del nodo `/content/cq:tags` de forma predeterminada. Esta acción se aplica a los paquetes de servicio, los paquetes de servicio de seguridad, los paquetes de funciones ampliadas, los paquetes de funciones acumulativas, los parches, etc. Por lo tanto, es necesario agregarlo desde las propiedades antes de la instalación.

### Problema conocido de AEM Sites {#known-issues-aem-sites-6523}

* Fragmentos de contenido: la previsualización falla debido a la protección DoS para un gran árbol de fragmentos. Consulte el artículo de [KB sobre las opciones de configuración predeterminadas de GraphQL Query Executor](https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)



### Problemas conocidos de AEM Forms {#known-issues-aem-forms-6523}

* Si la conversión de HTML a PDF falla en un servidor SUSE® Linux® (SLES 15 SP6 en adelante) con el siguiente error:

  ```Auto configuration failed 4143511872:error:0E079065:configuration file routines:DEF_LOAD_BIO:missing equal sign:conf_def.c:362:line 57```
a continuación, configure la siguiente variable de entorno y reinicie el servidor:
  `OPENSSL_CONF=/etc/ssl`

* Después de instalar AEM Forms JEE Service Pack 21 (6.5.21.0), si encuentra entradas duplicadas de Jars Geode `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` en la carpeta `<AEM_Forms_Installation>/lib/caching/lib` (FORMS-14926), realice los siguientes pasos para resolver el problema:

   1. Detenga los localizadores, si están en funcionamiento.
   1. Detenga el servidor de AEM.
   1. Vaya a `<AEM_Forms_Installation>/lib/caching/lib`.
   1. Quite todos los archivos de revisión de Geode excepto `geode-*-1.15.1.2.jar`. Confirme que solo están presentes los jars Geode con `version 1.15.1.2`.
   1. Abra el símbolo del sistema en modo de administrador.
   1. Instale el parche de Geode mediante el archivo `geode-*-1.15.1.2.jar`.

* Si un usuario intenta obtener una vista previa de un borrador de carta con datos XML guardados, se queda atascado en el estado `Loading` para algunas cartas específicas. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (FORMS-14521)

* Después de actualizar a AEM Forms Service Pack 6.5.21.0, el servicio `PaperCapture` no puede realizar operaciones de OCR (reconocimiento óptico de caracteres) en archivos PDF. El servicio no genera resultados en forma de PDF o de archivo de registro. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (CQDOC-21680)

* Cuando los usuarios actualizaban de AEM 6.5 Forms Service Pack 18 o 19 a Service Pack 20 o 21, encontraban un error de compilación de JSP. Este error les impedía abrir o crear formularios adaptables. También causó problemas con otras interfaces de AEM. Estas interfaces incluían el Editor de páginas, la IU de AEM Forms, el Editor de flujos de trabajo y la IU de Información general del sistema. (FORMS-15256)

  Si tiene un problema de este tipo, realice los siguientes pasos para resolverlo:
   1. Vaya al directorio `/libs/fd/aemforms/install/` en CRXDE.
   1. Elimine el paquete con el nombre `com.adobe.granite.ui.commons-5.10.26.jar`.
   1. Reinicie el servidor de AEM.

* Después de actualizar al paquete de servicio 20 de AEM Forms (6.5.20.0) con el complemento de Forms, las configuraciones que dependen del servicio de Adobe Analytics Cloud heredado mediante autenticación basada en credenciales dejan de funcionar. Este problema impedía que las reglas de Analytics se ejecutaran correctamente. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (FORMS-15428)

* Cuando un usuario actualiza al Service Pack 20 de AEM Forms (6.5.20.0) en el servidor JEE y genera archivos PDF mediante los servicios de salida, los archivos PDF se representan con problemas de accesibilidad. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3922112)
* Cuando un usuario genera archivos PDF etiquetados mediante el servicio de salida en JEE, muestra la &quot;Advertencia de estructura inadecuada&quot;. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3922038)
* Cuando se envía un formulario en AEM Forms JEE, las instancias de un elemento XML repetitivo se eliminan de los datos. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3922017)
* Cuando un usuario en un entorno Linux® procesa un formulario adaptable (en JEE) en HTML, no se procesa correctamente. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3921957)
* Cuando un usuario convierte un archivo XTG al formato PostScript mediante el servicio Output en AEM Forms JEE, se produce el siguiente error: `AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE`. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3921720)
* Después de actualizar al paquete de servicio 18 de AEM Forms (6.5.18.0) en el servidor JEE, cuando un usuario envía un formulario, no se puede procesar HTML5 o PDF forms y XMLFM se bloquea. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3921718)
* En la Vista previa de impresión de la interfaz de usuario de Interactive Communications Agent, el símbolo de moneda (como el signo de dólar $) se muestra de forma incoherente para todos los valores de campo. Aparece para valores de hasta 999, pero falta para valores de 1000 y superiores. (FORMS-16557)
* Las modificaciones realizadas en el XDP de los fragmentos de diseño anidados en una comunicación interactiva no se reflejan en el editor de CI. (FORMS-16575)
* En la Vista preliminar de la interfaz de usuario de Interactive Communications Agent, algunos valores calculados no se muestran correctamente. (FORMS-16603)
* Cuando la carta se ve en la Vista previa de impresión, el contenido cambia. Es decir, algunos espacios desaparecen y ciertas letras se reemplazan por `x`. (FORMS-15681)
* Cuando un usuario configura una instancia de WebLogic 14c, el servicio PDFG en AEM Forms Service Pack 21 (6.5.21.0) en JEE que se ejecuta en JBoss® falla debido a conflictos del cargador de clases que implican la biblioteca SLF4J. El error se muestra de la siguiente manera (CQDOC-22178):

  ```java
  Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
  the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
  @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
  (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
  have different Class objects for the type org/slf4j/ILoggerFactory used in the signature
  ```



## Paquetes de contenido y paquetes OSGi incluidos{#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en esta versión del paquete de servicio [!DNL Experience Manager] 6.5:

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.23.0](/help/release-notes/assets/65230-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.23.0](/help/release-notes/assets/65230-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->



## Sitios web restringidos{#restricted-sites}

Estos sitios web solo están disponibles para los clientes de. Si es cliente de y necesita acceso, póngase en contacto con el administrador de cuentas de Adobe.

* [Descarga de producto en Licensing.adobe.com](https://licensing.adobe.com/)
* [Póngase en contacto con Atención al cliente de Adobe](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página de producto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html?lang=es)
>* [[!DNL Experience Manager] Documentación de 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [Suscribirse a las actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html)
