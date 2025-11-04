---
title: Notas de la versión para  [!DNL Adobe Experience Manager]  6.5
description: Encuentre información de la versión, novedades, instrucciones de instalación y una lista de cambios detallada para  [!DNL Adobe Experience Manager]  6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 9d5ad43703d2fb3c1d40e10578f5289510a18230
workflow-type: tm+mt
source-wordcount: '6746'
ht-degree: 99%

---

# Notas de la versión del Service Pack de [!DNL Adobe Experience Manager] 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.23.0, Revisión para GRANITE-61551 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versión del Service Pack |
| Fecha | 9 de septiembre de 2025 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fcq-6.5.0-hotfix-GRANITE-61551-SP23-1.2.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

<!-- OLD DOWNLOAD URL
(https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) -->

## Qué se incluye en [!DNL Experience Manager] 6.5.23.0 {#what-is-included-in-aem-6523}

[!DNL Experience Manager] 6.5.23.0 incluye nuevas funciones, mejoras clave solicitadas por el cliente y correcciones de errores. También incluye mejoras de rendimiento, estabilidad y seguridad publicadas desde la disponibilidad inicial de la versión 6.5 en abril de 2019. [Instalar este Service Pack](#install) en [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Funciones y mejoras clave

<!--### Sites {#sites}

* A () -->

<!--
### [!DNL Assets]

* A ()
-->

### Formularios {#forms-sp23}

Las funciones y mejoras clave de esta versión son las siguientes:

* [Hipervínculos accesibles con estilo de texto mixto en PDF estáticos](https://helpx.adobe.com/content/dam/help/es/experience-manager/6-5/forms/pdf/using-designer.pdf): los hipervínculos que contienen estilos de texto mixtos en PDF estáticos ahora están etiquetados como un solo elemento accesible. Esta mejora simplifica la estructura del árbol de etiquetas, optimiza la navegación del lector de pantalla y admite un mejor cumplimiento de la accesibilidad.

* [Se ha actualizado la matriz de plataformas compatible](/help/forms/using/aem-forms-jee-supported-platforms.md)

  La versión más reciente introduce actualizaciones en la matriz de plataformas admitidas, lo que garantiza la compatibilidad con las tecnologías más recientes.

   * Cliente de IBM® Content Manager 8.7

   * MongoDB Enterprise 7.0

   * MySQL 8.4

   * Microsoft® SQL Server 2022

   * Controlador JDBC 12.8 de Microsoft® SQL Server

   * Red Hat® Enterprise Linux® 9 (Kernel 4.x, 64 bits) 

* [Componente de archivo adjunto protegido](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment): como medida de seguridad, el componente ahora evita el envío de archivos con extensiones modificadas que intentan omitir las comprobaciones de tipo de archivo permitido. Estos archivos se bloquean durante el envío para garantizar que solo se aceptan tipos de archivo válidos.

* FORMS-20533, FORMS-20532: AEM Forms ahora incluye una actualización de la versión de Struts de 2.5.33 a 6.x. Se añadió la compatibilidad a través de una [revisión](/help/release-notes/aem-forms-hotfix.md) que puede [descargar e instalar](/help/release-notes/aem-forms-hotfix.md) para que sea compatible con la última versión de Struts.

* **LC-3922769**: algunas funciones de AEM Forms ahora requieren OpenSSL 3 para funcionar de forma correcta. El sistema debe tener OpenSSL 3 instalado, con las bibliotecas `libcrypto.so.3` y `libssl.so.3`.  Dado que las actualizaciones de seguridad solo están disponibles en las versiones 3.0.14 y posteriores y que la compatibilidad con SafeLogic finaliza en febrero de 2025, BSAFE se ha eliminado y OpenSSL 3 ahora se utiliza para el cumplimiento de la seguridad.  Para conocer la compatibilidad de la plataforma y los requisitos detallados, consulte [Plataformas compatibles con AEM Forms en JEE](/help/forms/using/aem-forms-jee-supported-platforms.md) y [Requisitos técnicos](/help/sites-deploying/technical-requirements.md).


  **Para comprobar la instalación de OpenSSL 3:**

   * **RHEL/CentOS/Fedora-based systems**: `rpm -qa | grep   openssl3`
   * **Ubuntu/Debian-based systems**: `dpkg -l | grep openssl3`
   * **Verificación alternativa**: `ldd /path/to/XMLForm |   grep -E 'libcrypto.so.3|libssl.so.3'` (si las bibliotecas están en LD_LIBRARY_PATH)





<!--* **Two-Factor authentication with SAML for AdminUI** 

  AdminUI in AEM Forms JEE now supports two-factor authentication using Security Assertion Markup Language (SAML) single sign-on (SSO), providing stronger security and a seamless login experience for administrators, similar to what is available in HTML Workspace. 

#### New GA features in AEM Forms {#ga-aem-forms-sp23}

* A ()

#### New Beta features in AEM Forms {#beta-aem-forms-sp23}
-->

## Problemas corregidos en el Service Pack 23 {#fixed-issues}

<!-- 6.5.23.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-6523}

#### Accesibilidad {#sites-accessibility-6523}

* Las secciones de lienzo de las páginas del Editor de AEM ahora admiten la accesibilidad total del teclado. Los usuarios pueden activar los títulos de sección y los botones de edición utilizando únicamente el teclado, sin depender del desplazamiento del ratón. Esta actualización garantiza el cumplimiento de WCAG 2.1.1 y mejora la capacidad de uso entre componentes (como los modales Teaser, Imagen, Carrusel, Diseño, Deformación de tiempo y Anotación). (SITES-25256) <!-- 6.5 LTS SP1 -->
* Se ha corregido un problema de accesibilidad en el editor de páginas de AEM por el que el enfoque del teclado se restablece de forma inesperada al principio de la barra de herramientas demográficas después de activar botones como Persona, Carro de compras o Abandonado. Ahora, el enfoque permanece en el botón activado para admitir flujos de trabajo coherentes de navegación mediante el teclado y lector de pantalla. (SITES-25306)
* Se ha corregido un problema crítico de accesibilidad en el editor de páginas de AEM por el que los elementos de lienzo de varios cuadros de diálogo y modelos (por ejemplo, el carril de recursos o la vista previa de diseño) no se podían utilizar solo con un teclado. Todos los elementos de lienzo interactivos ahora admiten la navegación solo mediante el teclado, lo que garantiza el cumplimiento del criterio de éxito 2.1.1 de WCAG 2.1 (SITE-25256)
* Se ha corregido un problema de accesibilidad en la IU de administración de Sites por el que los elementos de lista interactivos del elemento emergente Crear usaban funciones ARIA incorrectas. A los elementos que se comportaban como vínculos se les asignaba `role="listitem"`, en lugar de `role="menuitem"`, lo que infringía los patrones de diseño de ARIA y confundía a los lectores de pantalla. Las actualizaciones garantizan que todos los componentes de la lista sigan funciones semánticas adecuadas para mejorar la compatibilidad con la tecnología de teclado y asistencia. (SITES-24493)
* Se ha corregido un problema de asociación de etiquetas de accesibilidad para el título de página y los campos de etiquetas. La interfaz de AEM ahora asocia correctamente las etiquetas de accesibilidad con los campos “Título” y “Título de página” al utilizar lectores de pantalla como JAWS. La corrección garantiza una lectura de etiquetas adecuada y mejora el cumplimiento de la ADA en la creación de páginas, las propiedades y los flujos de trabajo de movimiento. (SITES-27149)
* Se ha corregido un problema de accesibilidad con la identificación de tablas en el cuadro de diálogo de permisos. La tabla de permisos de AEM ahora utiliza funciones y atributos de ARIA correctos para garantizar que lectores de pantalla como JAWS la identifiquen correctamente como una tabla. La corrección mejora el cumplimiento de la accesibilidad y garantiza que los usuarios reciban anuncios de contenido y navegación precisos. (SITES-27140)
* Se ha corregido la falta de una etiqueta visual para los campos de entrada de comentarios en la cronología. Se han corregido las etiquetas visuales que faltaban para los campos de entrada de “comentario” en la sección de cronología para mejorar la accesibilidad. La actualización garantiza que los lectores de pantalla puedan anunciar con precisión las etiquetas de campo. Esta experiencia mejora la navegación y el envío de formularios para todos los usuarios, y sobre todo para las personas que dependen de las tecnologías de asistencia. (SITES-26903)
* Se ha corregido la accesibilidad del teclado para el botón de puntos suspensivos en comentarios de la cronología. Se ha habilitado la navegación mediante el teclado para el botón de puntos suspensivos (tres puntos) junto a los comentarios en la sección de cronología. Los usuarios ahora pueden acceder al botón e interactuar con él mediante la tecla de tabulación, lo que mejora la accesibilidad para los usuarios que dependen de la navegación solo mediante teclado. (SITES-26891)
* Se han mejorado los anuncios de NVDA/Narrator para resultados de búsqueda en los cuadros de diálogo de selección. Se ha actualizado el cuadro de diálogo Abrir selección para anunciar si se encuentran o no resultados de búsqueda al utilizar lectores de pantalla, como NVDA o Narrator. Esta mejora ayuda a los usuarios que dependen de las tecnologías de asistencia a comprender el resultado de sus acciones de búsqueda sin necesidad de confirmación visual. (SITES-26883)
* Se ha corregido la función ARIA del icono de puntos suspensivos junto al campo de entrada de comentarios. Se ha actualizado el icono de puntos suspensivos (tres puntos) junto al campo de entrada del comentario para utilizar la función ARIA correcta, lo que garantiza que los lectores de pantalla puedan identificar el elemento con precisión. Esta mejora optimiza el cumplimiento de la accesibilidad y la experiencia de los usuarios que dependen de las tecnologías de asistencia. (SITES-26881)
* Se han corregido atributos ARIA no válidos en los componentes de Coral UI. Se han actualizado los componentes de Coral UI para garantizar que todos los atributos ARIA utilicen valores válidos, lo que mejora la accesibilidad y el cumplimiento. En particular, se han abordado los casos en los que valores no válidos como `aria-modal="dialog"` se asignaban de forma incorrecta. Esta mejora permite a los lectores de pantalla interpretar correctamente los elementos del cuadro de diálogo, lo que mejora la accesibilidad para los usuarios que dependen de las tecnologías de asistencia. (SITES-26873)
* Visibilidad mejorada e información sobre herramientas para iconos en escenarios de reflujo. Se ha mejorado el comportamiento de reflujo para garantizar que la información sobre herramientas se muestre correctamente en los iconos **Descargar**, **Volver a procesar recursos** y **Finalizar compra**. Se centró en un problema de accesibilidad en el que los iconos y sus etiquetas se volvían invisibles cuando cambiaba el tamaño de la ventanilla móvil o la configuración de zoom del explorador. Esta corrección admite usuarios con visión reducida al mantener la visibilidad y proporcionar descripciones de iconos adecuadas durante el reflujo. (SITES-26871)

#### Interfaz de usuario de administración{#sites-adminui-6523}

Se ha corregido la excepción del servicio URL del editor universal con puntos finales del externalizador faltantes. El servicio URL del editor universal ahora administra los puntos finales del externalizador local, de publicación o de autor que faltan sin producir excepciones. Los usuarios administradores pueden abrir el Editor de páginas correctamente incluso cuando algunas configuraciones del externalizador están incompletas. (SITES-28877) <!-- LTS -->

#### IU clásica{#sites-classicui-6523}

* Problema en los cuadros de diálogo de la IU clásica en el que, al cambiar un botón, se ocultaba un área de texto y no se volvía a mostrar en los clics posteriores. La corrección garantiza que el área de texto vuelva a aparecer correctamente cuando se activa, restaurando el comportamiento esperado y evitando interrupciones en los flujos de trabajo del cuadro de diálogo dinámico. (SITES-30230)
* Se ha corregido la funcionalidad del buscador de recursos de imagen de la IU clásica dañada después de la actualización del Service Pack 22. El buscador de recursos de imagen de la IU clásica ahora gestiona correctamente los nombres de recursos que contienen espacios o caracteres especiales. Esta actualización garantiza que el buscador de recursos codifique los nombres de archivo correctamente, lo que evita errores de búsqueda y permite a los autores localizar y seleccionar recursos de imagen sin errores. (SITES-29151)

#### [!DNL Content Fragments]{#sites-contentfragments-6523}

* Se corrigió un error en la prueba de validación de `DeleteVariationIT.testUpdateBasic`. La prueba `DeleteVariationIT.testUpdateBasic` ya no falla durante las ejecuciones de validación del Service Pack. La corrección corrige un problema de asignación de texto que falta en la lógica de administración de JSON, lo que garantiza la estabilidad de la prueba y evita interrupciones de prueba innecesarias. (SITES-28022)
* AEM ahora evita la degradación del rendimiento causada por el formato incorrecto de los metadatos de XMP en los recursos de imagen. Los recursos que contienen nombres de propiedad de XMP no válidos o no compatibles, como los que tienen segmentos numéricos o estructuras no calificadas, ya no activan los registros de advertencia repetidos durante el procesamiento. El sistema filtra los metadatos problemáticos para garantizar que la ingesta y validación de recursos se complete sin errores. (SITES-30683) <!-- AEM 6.5 LTS SP1 -->


<!-- #### [!DNL Content Fragments] - Admin{#sites-admin-6523}

* A () -->


#### [!DNL Content Fragments]: editor de fragmentos{#sites-fragments-editor-6523}

Otros autores aún pueden publicar fragmentos de contenido incluso cuando otro autor los desprotege lo que es contrario al comportamiento deseado de la función de desprotección. Esta corrección evita que otros usuarios vean o utilicen los botones de publicación en la interfaz de creación cuando se desprotege un fragmento de contenido. (SITES-30578) <!-- LTS -->

#### [!DNL Content Fragments]: API de GraphQL {#sites-graphql-api-6523}

Se ha corregido un error QueryValidationError de GraphQL con esquemas de fragmentos de contenido. Al actualizar el paquete `cq-dam-cfm-graphql` se corrigen los errores de validación de esquema al utilizar referencias a fragmentos de contenido. La corrección garantiza que las consultas de GraphQL funcionen correctamente sin requerir la realineación manual del esquema o la republicación después de las implementaciones de paquetes. (SITES-27001) <!-- LTS -->


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6523}

* A () -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6523}

* A () -->


#### Consola de componente{#sites-component-console-6523}

Mejoras en la carga de la página “Uso del componente Live”. Optimiza la página “Uso activo de componentes” en AEM para evitar que aparezcan filas vacías al desplazarse por conjuntos de datos grandes. Los usuarios que cargan componentes con referencias de uso extensas ahora pueden experimentar una carga de datos continua sin pausas innecesarias ni entradas vacías. Esta experiencia mejora la navegación de páginas, la precisión del seguimiento y la eficacia de la administración en la creación de informes de uso de componentes. (SITES-26454)

#### Backend principal{#sites-core-backend-6523}

* Se ha corregido un error en la lista de recursos del Buscador de contenido debido a nombres de recursos no válidos. El buscador de contenido ahora gestiona correctamente los nombres de los recursos con caracteres no codificables. La lista de recursos en el Editor de páginas ya no falla ni genera excepciones al encontrar recursos con nombres problemáticos. (SITES-28722)
* Problema en el cual el componente `SearchPathLimiter` generaba entradas de registro excesivas al imprimir mensajes en el nivel de ERROR para cada invocación. Este comportamiento comenzó después del Service Pack 17 y provocó problemas de rendimiento debido a los volúmenes de registro extremadamente altos. La corrección reduce el nivel de registro a DEPURACIÓN, lo que reduce significativamente el ruido de registro y mejora la monitorización del sistema y la eficacia del diagnóstico. (SITES-29835)
* Los metadatos de XMP con formato incorrecto activaron un error durante el procesamiento de los recursos de imagen en `ValidationDataServlet`. La corrección garantiza la administración de metadatos compatible y evita el análisis repetido de propiedades no válidas. (SITE-30683)  <!-- LTS -->


<!-- #### Core Components{#sites-core-components-6523}

* A () -->

<!-- #### Campaign integration{#sites-campaign-integration-6523}

* A () -->

<!-- #### Experience Fragments{#sites-experiencefragments-6523}

* A () -->

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6523}

* A () -->


#### Lanzamientos{#sites-launches-6523}

* Se ha corregido una incorrecta visualización de fecha de lanzamiento entre el 25 y el 31 de diciembre. La IU de los lanzamientos ahora muestra fechas entre el 25 y el 31 de diciembre con el año correcto. La corrección garantiza que las fechas ya no muestren incorrectamente el año siguiente, lo que evita confusiones durante la planificación y programación de la campaña. (SITES-28706)
* Se han corregido las plantillas de AEM Launch que no funcionaban tras la actualización Service Pack 22. Las plantillas de AEM Launch ahora se cargan correctamente después de una actualización de Service Pack 22. La corrección corrige los datos no válidos en las configuraciones de lanzamiento internas, lo que permite a los usuarios ver, editar y crear lanzamientos sin errores ni campos que falten. (SITES-28504)


<!-- #### Link Checker{#sites-link-checker-6523}

* A () -->

<!-- #### MSM - Live Copies{#sites-msm-live-copies-6523}

* A () -->


#### Editor de páginas{#sites-pageeditor-6523}

* Se ha corregido un problema de carga de AssetPicker en resoluciones de pantalla más bajas. AssetPicker ahora carga los recursos correctamente cuando los usuarios se desplazan a resoluciones de pantalla más bajas (1728 ×1117 o menos). Los usuarios ya no experimentan la falta de recursos al desplazarse, lo que mejora la administración de recursos en diferentes puntos de interrupción del dispositivo. (SITES-28065)
* Se ha corregido la falta de anuncios del lector de pantalla para las acciones de bloqueo y desbloqueo de página. El editor de páginas ahora anuncia correctamente el mensaje “Información: La página se ha bloqueado/desbloqueado” cuando los usuarios activan el botón de bloqueo/desbloqueo. La corrección mejora el cumplimiento de la accesibilidad y garantiza que los usuarios del lector de pantalla reciban actualizaciones dinámicas durante la edición de páginas. (SITES-27143)
* Se ha mejorado el comportamiento de enfoque de teclado para las acciones de componentes en la creación de AEM. Se ha mejorado la navegación mediante el teclado en la herramienta de autor de AEM para garantizar que el enfoque permanezca en el componente recién creado o seleccionado después de acciones como Configurar, Eliminar o Convertir. Anteriormente, el enfoque cambiaba a la parte superior de la página, lo que provocaba problemas de cumplimiento de la accesibilidad. Esta actualización mejora la experiencia del usuario para los usuarios de teclado y tecnología de asistencia. Lo hace manteniendo una progresión del enfoque lógico dentro del flujo de trabajo de edición. (SITES-26549)
* Se ha mejorado la navegación por pestañas en los cuadros de diálogo de creación. Mejora la navegación mediante el teclado en los cuadros de diálogo de autor de AEM permitiendo a los usuarios avanzar mediante el tabulador después de alcanzar el cuadro de edición Descripción. Anteriormente, la retención del foco en el campo Descripción impedía que se pudiese seguir navegando sin utilizar combinaciones de teclas especiales. La actualización garantiza que los usuarios puedan desplazarse por los campos sin problemas utilizando solo el tabulador, lo que mejora el cumplimiento de la accesibilidad y la experiencia del usuario. (SITES-26524)
* Se introdujo una regresión en AEM 6.5 Service Pack 22 que impedía a los usuarios incluir espacios en los títulos de lanzamiento. La corrección restaura la capacidad de usar espacios, lo que permite a los equipos definir y organizar los nombres de lanzamiento de forma más flexible, en línea con el comportamiento esperado. (SITES-29414)
* Se ha corregido el problema de cambio de tamaño de los componentes dentro de los contenedores de diseño después de ocultar o mostrar acciones. El editor de páginas ahora calcula correctamente los valores de columna después de ocultar y mostrar un contenedor de diseño. Los usuarios pueden cambiar el tamaño de los componentes sin errores y las columnas se muestran correctamente durante las acciones de cambio de tamaño. (SITES-28463)
* Se ha corregido un error de colocación del botón de árbol de contenido en el editor de páginas. Ahora, el editor de páginas coloca correctamente el botón de configuración del árbol de contenido en el cuadro de diálogo “Encabezado Teaser” deseado, en lugar de en la sección incorrecta. La corrección actualiza el CSS para el cuadro de diálogo del árbol de contenido para que utilice `top:0` en lugar de `bottom:0`, lo que garantiza la correcta ubicación del botón. (SITES-28448)


<!-- #### Replication{#sites-replication-6523}

* A () -->


#### Editor de texto enriquecido{#sites-rte-6523}

Corregir etiquetas `<br>` inesperadas en el editor de texto enriquecido con el modo de pegado de texto sin formato. El editor de texto enriquecido ahora administra correctamente las operaciones de cortar y pegar al utilizar texto sin formato `defaultPasteMode`. La corrección evita la inserción de etiquetas `<br>` inesperadas cuando los usuarios cortan y pegan texto dentro de campos RTE, lo que garantiza un formato limpio durante la edición de contenido. (SITES-27780)

#### Editor universal {#sites-universal-editor-6523}

* Cuando se envían varias solicitudes que contienen el parámetro de consulta a AEM, es posible que la cookie del token de inicio de sesión no se devuelva a tiempo, lo que puede provocar un fallo en el inicio de sesión. (SITES-30659) <!-- LTS -->
* Para garantizar la compatibilidad con los controladores SAML, debe configurar la propiedad `service.ranking` para que el controlador `Query Token Auth` ejecute *antes* del controlador `SAML Auth`. (SITES-29684)

### [!DNL Assets]{#assets-6523}

* Los siguientes problemas se producen en la página de navegación On-Premise de [!DNL AEM] (6.5.22.0) después de seleccionar ![Assets](/help/assets/assets/Smock_Asset_18_N.svg)**[!UICONTROL Assets &#x200B;]**, ir a la carpeta&#x200B;**[!UICONTROL &#x200B; Buscar Adobe Stock &#x200B;]**&#x200B;y seleccionar una imagen de archivo:
   * La imagen de archivo seleccionada no se puede autorizar y guardar porque al hacer clic en **[!UICONTROL Licencia y guardar]** se muestra una lista desplegable vacía.
   * Si se selecciona la imagen de archivo o se vuelve a introducir la URL de la página de archivo, se redirige a la página principal de [!DNL AEM], lo que impide el acceso a la imagen de Adobe Stock. (ASSETS-48687)
* Problemas al administrar carpetas si el nombre de la carpeta incluye un `/` en su nombre en la página de navegación On-Premise (6.5.22.0) de [!DNL AEM]. (ASSETS-46740)
* En [!DNL AEM] 6.5, la página de detalles del recurso no se carga desde la vista ![Colección](/help/assets/assets/Smock_Collection_18_N.svg)**[!UICONTROL Colecciones &#x200B;]**&#x200B;debido a un uso elevado de la memoria. (ASSETS-46738)
* Problemas de integración con [!DNL InDesign] dado que el servicio `Day CQ DAM Mime Type OSGI` identifica incorrectamente [!DNL InDesign] archivos como `x-adobe-indesign` en lugar de `x-indesign`. (ASSETS-45953)
* La fuga de sesión de [!DNL AEM 6.5.21] se remonta al paso de flujo de trabajo de **[!UICONTROL Publicación programada en Brand Portal]** listo para usar. (ASSETS-44104)
* Errores de **[!UICONTROL memoria insuficiente (OOM)]** que se muestran en [!DNL AEM] al procesar y publicar imágenes. Este problema se debió a métodos obsoletos en flujos de trabajo, como **[!DNL Dam Asset update]** y **[!DNL Dynamic Media: Reprocess assets]**. (ASSETS-43343)
* Después de realizar un cambio menor, como actualizar el título, vuelva a abrir y guardar **[!DNL Connected Assets configuration]** en la instancia local de Sites. A continuación, la instancia remota pierde su conexión con la instancia local. Como resultado, no puede establecer comunicación con la instancia local de Sites. (ASSETS-44484)
* En [!DNL AEM 6.5.21], cuando se cancela la carga de un recurso en la vista de lista y se realiza una segunda carga, [!DNL AEM] muestra un error **[!UICONTROL 0 de NaN recursos cargados]**. (ASSETS-44124)

#### [!DNL Dynamic Media]{#assets-dm-6523}

Se ha añadido una propiedad de metadatos (`jcr:content/metadata/dam:scene7SmartCropStatus`) a los recursos para identificar las generaciones de recortes inteligentes con errores. Permite la búsqueda, el filtrado y el reprocesamiento eficientes de recursos con problemas de recorte inteligente mediante flujos de trabajo manuales o automatizados. (ASSETS-46237)

#### [!DNL Dynamic Media] - Modo híbrido {#assets-dm-hybrid-6523}

##### Dynamic Media: paquete de complemento híbrido (AEM 6.5.23 y posterior)

A partir del Service Pack 23 de AEM 6.5, hay un nuevo paquete de complemento disponible para el modo híbrido de Dynamic Media. Este paquete incluye el paquete `cq-scene7-imaging` específicamente compatible con el modo de ejecución híbrido de Dynamic Media.

**Corrección clave incluida**

Se ha corregido un problema en las implementaciones híbridas de Dynamic Media en las que las actualizaciones del parámetro `catalog.expiration` en `/conf/global/settings/dam/dm/imageserver` no se reflejaban en las direcciones URL del servidor o del autor, a pesar de que la replicación se realizaba correctamente sin errores. La actualización garantiza valores de caducidad coherentes entre CRX/DE, la respuesta del servidor y las direcciones URL de envío público. A su vez, mejora el comportamiento de la caché y la fiabilidad de las transformaciones de imagen. (ASSETS-44837)

**Consideraciones importantes**

* El paquete `cq-scene7-imaging` de la instalación base de AEM 6.5.23 (y versiones posteriores) *no es compatible* con el modo de ejecución híbrido de Dynamic Media.
* La instalación del Service Pack 23 (y versiones posteriores) por sí sola *no actualiza automáticamente* el paquete `cq-scene7-imaging` existente en las instancias de AEM configuradas para Dynamic Media - Híbrido (modo de ejecución `-r dynamicmedia`).

**Cuándo instalar el paquete del complemento híbrido**

* Al actualizar directamente a AEM 6.5.23 (y posterior) desde AEM 6.5.19 o anterior.
* Cuando necesite correcciones específicas de la funcionalidad híbrida de Dynamic Media.
* Al implementar una nueva instancia híbrida de Dynamic Media directamente desde AEM 6.5 GA (disponibilidad general) a Service Pack 23 (y posterior).

**Descargar el paquete del complemento híbrido**

El paquete del complemento híbrido está disponible públicamente en Adobe Software Distribution a partir del jueves, 22 de mayo de 2025, con la versión oficial de AEM 6.5.23. Los usuarios pueden encontrarlo si buscan **Paquete del complemento híbrido de Dynamic Media de AEM 6.5** en Distribución de software.


### [!DNL Forms]{#forms-6523}

#### Forms Designer

* Cuando un usuario exporta los datos de un PDF basado en XFA mediante exportDataAPI, el XML resultante muestra discrepancias cuando se compara con los datos XML exportados manualmente mediante Acrobat Reader. Faltaban valores de algunos campos en la salida en comparación con la salida generada desde Acrobat Reader. (LC-3922791)

* En AEM Forms 6.5.22.0, la generación de una etiqueta de PDF etiquetada con el servicio Output en Workbench añade una etiqueta inesperada bajo la etiqueta de referencia en un elemento de tabla de contenido. (LC-3922756)

* Cuando un usuario coloca pies de ilustración de campo con alineación inferior o derecha en AEM Forms Designer, el árbol de etiquetas incluye solo el pie de ilustración sin el valor correspondiente, lo que provoca un etiquetado de accesibilidad incompleto. (LC-3922619)

* Al actualizar del Service Pack 6 de AEM Forms 6.5 al Service Pack 20 de AEM Forms, los códigos QR de los PDF generados se vuelven ilegibles. El texto alternativo para los códigos QR también falla en las pruebas de accesibilidad, lo que afecta a la compatibilidad con los lectores de pantalla. (LC-3922551)

* Cuando un usuario procesa una carta en la interfaz de usuario de Agent en AEM Forms Service Pack 18, el contenido no se muestra correctamente debido a la API FormService.render(). (LC-3922461)

#### Formularios

* En AEM Forms, la habilitación de “Permitir texto enriquecido para el título” en el panel raíz hará que “Excluir título del documento de registro” en un panel anidado oculte el título del panel raíz de forma incorrecta. Lo hace así en el documento de registro generado. (FORMS-19696)

* El sistema ignora los `sling:resourceType` personalizados asignados mediante `aem:afProperties` en un esquema JSON en AEM 6.5. El tipo de recurso personalizado se omite durante el procesamiento. (FORMS-19691)

* Cuando un usuario envía un formulario adaptable con archivos adjuntos rellenados previamente mediante URI, el envío del formulario falla con una NullPointerException debido a la falta de datos binarios. (FORMS-19371) (FORMS-19486)

* Cuando un usuario carga un PDF en la sección “Formularios y documentos” de AEM 6.5 Forms, la función de cronología deja de funcionar. (FORMS-19407) (FORMS-19234)

* Cuando un usuario carga archivos mediante el componente de archivos adjuntos listo para usar (OOTB) en AEM Forms, se identifican vulnerabilidades de seguridad. Este problema lleva a una posible interceptación del proceso de envío por entidades no autorizadas. (FORMS-19271)

* Cuando un usuario configura un formulario adaptable listo para usar en AEM Forms para generar un documento de registro (DoR) automáticamente, el campo “Título” de las propiedades del documento de Acrobat Reader no muestra el título del documento de registro capturado. De forma predeterminada, el título del formulario no aparece en lugar del nombre del archivo. (FORMS-19263)

* Cuando un usuario abre una comunicación interactiva en la interfaz de usuario de Agent, los datos rellenados previamente no se pueden borrar por completo; al eliminarlos, se rellenan automáticamente con los mismos datos. (FORMS-19151)

* Cuando un usuario previsualiza un campo de fecha en la interfaz de usuario de Agent, la fecha cambia inesperadamente. Este problema se produce debido a discrepancias de las zonas horarias entre la configuración UTC de VM y la interpretación de la fecha por parte del sistema. (FORMS-19115)

* Cuando un usuario envía un formulario, los archivos adjuntos pueden duplicarse, lo que provoca varias cargas del mismo archivo. (FORMS-19045) (FORMS-19051)

* La adición de coordinadores a los conjuntos de políticas en la seguridad de documentos de AEM 6.5 falla tanto en la producción como en los entornos inferiores. (FORMS-18603, FORMS-18212, FORMS-19697)

* Cuando un usuario hace clic en el “datepicker-calendar-icon” en modo escritorio con un campo vacío en AEM Forms Service Pack 22, se produce un error debido a la variable _$focusedDate no definida, lo que interrumpe los scripts personalizados asociados. (FORMS-18483) (FORMS-18268)

* En AEM Forms Service Pack 19 (6.5.19.0), cuando un cliente previsualiza una carta, el campo “Cantidad de palabras” no muestra o actualiza los valores numéricos incorrectamente, lo que provoca una desalineación y que falten espacios en el contenido. (FORMS-18437, FORMS-17330, FORMS-18209, FORMS-18557, CTG-4150848, FORMS-19614, LC-3922004)

* Cuando un cliente previsualiza una carta guardada en AEM Forms 6.5 SP19 en RHEL, el contenido no se alinea correctamente, faltan espacios y aparecen caracteres inesperados como “x”. (FORMS-18422) (FORMS-17641)

* Cuando un usuario navega entre las pestañas de AEM Forms, la selección de componentes en la primera pestaña deja de responder. (FORMS-18345)

* En AEM Forms 6.5.21.0, cuando un usuario convierte un archivo HTML a PDF mediante la opción WebToPDF, el PDF de salida no incluye la sección de encabezado, incluidas las etiquetas de título y los metadatos. (FORMS-18223, FORMS-17835, FORMS-19642, FORMS-18224)

* En AEM JEE Process Manager SDK, cuando un usuario invoca el método retryAction(long actionOid), el sistema reintenta incorrectamente la primera acción encontrada en la tabla tb_action_instance. Este flujo de trabajo se produce incluso cuando se proporciona un ID de acción específico o cuando el ID es nulo, lo que da lugar a un comportamiento no deseado. (FORMS-18187)

* Después de actualizar a SP22, el usuario encuentra problemas en los que las funcionalidades de borrador guardado y envío fallan sin mostrar ningún mensaje de error. (FORMS-18069)

* En AEM 6.5.21.0, la transición de componentes base basados en XSD a componentes principales impide la implementación de referencias entre archivos en los esquemas JSON, lo que afecta a la migración de formularios adaptables. (FORMS-18065)

* Cuando un usuario obtiene una vista previa de una carta en la IU del agente, el campo de fecha muestra un valor incorrecto debido a problemas de conversión de tiempo CI. Estas discrepancias surgen de las diferencias de huso horario entre el entorno de la VM y la interpretación del tiempo por parte del sistema (horario UTC frente a hora local). (FORMS-17988) (FORMS-17248)

* Cuando un usuario obtiene una vista previa de las cartas mediante plantillas de notificación CI en AEM Forms, los tiempos de generación del PDF varían significativamente, de 1,5 segundos a más de 10 segundos, incluso en el mismo servidor. Esta incoherencia afecta a los flujos de trabajo críticos para el negocio. (FORMS-17951)

* Cuando un usuario enlaza un objeto de firma manuscrita en un formulario adaptable a un XDP mediante la opción “Fuentes de datos”, los cambios no se pueden guardar. El motivo se debe a errores persistentes de validación de la relación de aspecto, incluso cuando se utilizan valores válidos. (FORMS-17587)

* Cuando un usuario utiliza un XDP específico con muchos campos ocultos para fragmentos de documento, AEM crea nodos de CRX con la propiedad `cm:optional` establecida en falso, lo que provoca que falle el envío de la comunicación interactiva (CI). (FORMS-17538)

* En AEM Forms 6.5.19.0, cuando un cliente obtiene una vista previa de una carta, el campo de cuadro numérico no gestiona correctamente los valores negativos cuando se definen los límites de dígitos para el posible cliente y el valor de fragmento. Este problema se produce debido al uso de parseFloat, que trata el signo menos como parte del número. (FORMS-17451)

* En AEM Forms 6.5, cuando se obtiene una vista previa de una carta, se observa el uso del comodín “*” en el archivo Adobe.json, lo que genera inquietudes sobre su finalidad y su posible modificación. (FORMS-17317)

* Cuando un usuario usa un lector de pantalla en `Apply for a Fixed Rate Saver joint account`, los encabezados se anuncian incorrectamente como `clickable`, lo que provoca problemas de accesibilidad. (FORMS-17038)

* Cuando se incrusta un formulario, al iframe generado le falta un atributo de título, lo que provoca un problema de cumplimiento de la accesibilidad. (FORMS-17010)

* La descarga de un formulario mediante la IU del administrador de Forms siempre incluye dependencias asociadas, como temáticas y fragmentos. (FORMS-15811)

* Cuando un usuario accede al formulario en dispositivos móviles (iOS y Android™), los botones “siguiente” y “anterior” de la primera página están desactivados. Sin embargo, el lector de pantalla no los identifica como deshabilitados. (FORMS-15773)

* Cuando un usuario guarda un formulario grande con fragmentos y carga diferida habilitados, no puede recuperar borradores, lo que interrumpe el flujo de trabajo. (FORMS-19890, FORMS-19808)

#### Forms JEE

* Cuando un usuario reconfigura la base de datos en AEM Forms, la conexión falla debido a parámetros codificados. (FORMS-19568, FORMS-17621)

* Cuando un usuario configura AEM 6.5 con MySQL 8.4 utilizando el método llave en mano parcial, el administrador de configuración de LiveCycle (LCM) no reconoce el controlador de conector MySQL requerido. Esto provoca que la prueba y la configuración de la conexión a la base de datos fallen. (FORMS-19442)

* Cuando un usuario ejecuta LCM con JDBC 12.8.1 en JRE 11 en un entorno JEE, la configuración falla debido a problemas de incompatibilidad. (FORMS-19276)

* Cuando un usuario abre una tarea en AEM local, el sistema ejecuta el Perfil de acción de inicio de Workspace en lugar de AssignedUserProfile. (FORMS-19065)

* Cuando un usuario utiliza el método retryAction(long actionOid) en el administrador de procesos de AEM JEE, se produce un comportamiento inesperado. (FORMS-18357)(FORMS-18187)

* En AEM Forms 6.5.21.0, la conversión de PDFG da el siguiente error: (FORMS-16851)(FORMS-14613)

* En AEM Forms 6.5.23.0 con revisión 2, (PDFG) error de conversiones de PS a PDF y de HTML a PDF (WebKit). (FORMS-21721)

* En AEM Forms 6.5.23.0 con revisión 3, (PDFG) la conversión de imagen a PDF falla. (FORMS-22029)

#### Captcha de Forms {#forms-captcha-6523}

* Se ha mejorado las alertas reCAPTCHA en los formularios adaptables al actualizar los códigos de error de envío a 400. Además, se han refinado las alertas de registro para distinguir entre tiempos de espera, caducidades y errores de detección de bots, lo que mejora la precisión de la resolución de problemas y la observabilidad del sistema. (FORMS-19240)
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

* Se ha corregido un problema en los titulares de alertas de Coral por el que el color del texto aparecía en blanco, en lugar de negro, después de actualizar al Service Pack 21. Garantiza que se aplique un estilo correcto para mantener el contraste y la legibilidad adecuados de los mensajes de alerta en toda la interfaz. (NPR-42359)
* Se ha añadido compatibilidad con la integración de OAuth en la configuración de etiquetas inteligentes para alinearla con la obsolescencia de JWT (token web JSON). Garantiza la funcionalidad continua de las funciones de etiquetas inteligentes mediante métodos de autenticación actualizados. (NPR-42296)

#### Apache Felix {#foundation-apachefelix-6523}

Se ha corregido una NullPointerException que se producía al cargar archivos de clave privada en un campo de propiedad de tipo binario en CRX, lo que restaura la compatibilidad presente a través del Service Pack 16. Permite flujos de trabajo seguros de carga de archivos clave en AEM Managed Services sin errores del servidor ni interrupciones en los procesos de renovación de certificados. (CQ-4359178)


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

* Se han resuelto ciclos de dependencia OSGi entre servicios de scripts de Apache Sling que causaban retrasos o errores al cargar páginas HTML tras actualizar al Service Pack 21. Se han actualizado las referencias de servicio interno para eliminar las dependencias cíclicas que involucran a `SightlyScriptingEngineFactory` y los componentes relacionados, lo que mejora la fiabilidad y el comportamiento de inicio del motor de scripts. (GRANITE-56808)
* Se han actualizado los scripts de uso de JS en Apache Sling para cargar solo bajo demanda en lugar de hacerlo de forma anticipada al inicio, lo que elimina la contención de subprocesos y reduce el riesgo de que los servidores de publicación no respondan durante la carga. Este cambio mejora la estabilidad del servidor y los tiempos de respuesta durante situaciones de alto tráfico al evitar el bloqueo de recursos provocado por la resolución anticipada de scripts. (GRANITE-56611)
* Se ha corregido un problema en AEM OmniSearch por el cual los marcadores de posición de los campos de entrada se muestran de forma incorrecta como etiquetas, lo que provoca confusión visual. Garantiza el correcto procesado de los marcadores de posición en los campos de filtro, con lo que se mantiene un comportamiento coherente y accesible del formulario. (GRANITE-51791)
* Se ha resuelto un error de servidor que se activaba al seleccionar más de 30 CFM (modelos de fragmentos de contenido) con referencias de varios campos en el editor de modelos de fragmentos de contenido. Se ha mejorado el componente de sugerencia de filtros para admitir operaciones POST. Esta capacidad permite el manejo adecuado de grandes conjuntos de referencias durante la creación de fragmentos de contenido y mejora la estabilidad para configuraciones de modelos de gran volumen. (GRANITE-57164)
* Se ha resuelto un problema en los CFM por el cual, al hacer clic cerca de una casilla de verificación, se alternaba su estado de forma involuntaria. Se han actualizado los estilos para restringir la activación de clics estrictamente al elemento de casilla de verificación, lo que evita interacciones accidentales del usuario y mejora la facilidad de uso y accesibilidad del formulario. (GRANITE-52384)


<!--
#### Integrations{#foundation-integrations-6523}

* A () -->


#### Jetty{#foundation-jetty-6523}

Se ha resuelto un problema por el cual la validación SNI bloqueaba las llamadas de API a través de HTTPS para clientes de AEM que usaban configuraciones SSL de Dispatcher con encabezados de host personalizados. Presenta una opción para deshabilitar la validación de SNI como parte de la configuración de Jetty, lo que habilita la compatibilidad con configuraciones específicas de proxy inverso donde `mod_proxy` no es factible. (NPR-42614)


<!--
#### Localization{#foundation-localization-6523}

* A () -->

<!--
#### Oak {#foundation-oak-6523}

* A () -->


#### Plataforma{#foundation-platform-6523}

* Se ha corregido un comportamiento incoherente de la combinación de etiquetas al garantizar que el valor de etiqueta combinado siempre se muestre de forma correcta en los recursos, con independencia de si las etiquetas se crean en línea o mediante el método estándar. Evita que los valores residuales de los campos `EN:title` anulen la visualización de la etiqueta combinada. (CQ-4358812)
* Se ha corregido la codificación repetida de caracteres et en los valores de etiqueta dentro del cuadro de diálogo de edición de etiquetas. Evita que se añadan entidades “&amp;” adicionales en cada guardado, lo que garantiza que los valores de las etiquetas permanezcan limpios y coherentes en todas las ediciones y evita errores de visualización en el contenido creado. (CQ-4359048)
* Se ha resuelto un error `ClassCastException` que impide la entrega de correo electrónico en el envío de formularios adaptables en AEM 6.5, que se ejecuta en WebSphere®. La corrección habilita la transmisión de correo electrónico correcta al garantizar la compatibilidad entre `com.sun.mail.handlers.text_plain` y `java.activation.DataContentHandler`, en consonancia con la configuración del gestor de correo esperada por los entornos WebSphere®. (NPR-42500)
* Se ha mejorado la gestión de errores en el administrador de paquetes al asegurar que AEM muestre un mensaje claro cuando falle la instalación y la respuesta de error esté vacía. Esta corrección evita errores silenciosos y ayuda a una depuración más rápida durante la implementación de paquetes. (NPR-42375)

<!--
#### Security{#foundation-security-6523}

* A -->

<!--
#### Sling{#foundation-sling-6523}

* A () -->


#### Traducción{#foundation-translation-6523}

Se ha corregido un problema de NullPointerException (NPE) que se activaba al actualizar fragmentos de contenido en flujos de trabajo mediante **Actualizar copia de idioma**. Esta corrección garantiza que los flujos de trabajo no entren en un estado de error ni permanezcan atascados en un estado de ejecución al editar contenido vinculado a referencias de traducción. (NPR-42115)

#### Interfaz de usuario{#foundation-ui-6523}

Añade los atributos `title` que faltan a los botones del cuadro de diálogo de Coral UI, como **Listo** y **Cancelar**, en los cuadros de diálogo de edición de componentes para mejorar la accesibilidad y habilitar la validación automatizada. Garantiza que los botones conserven los atributos esperados en el procesamiento de marcado, lo que evita errores en las pruebas de IU basadas en Selenium. (NPR-42412)

#### WCM{#foundation-wcm-6523}

Se ha corregido un problema que impedía que se añadieran páginas a trabajos de traducción al usar **Actualizar copia de idioma** en entornos con Service Pack 19 o posterior. Garantiza que los flujos de trabajo de traducción se desarrollen según lo esperado, lo que permite una transferencia de página adecuada entre copias de idioma sin intervención manual. (CQ-4357929)

#### Flujo de trabajo{#foundation-workflow-6523}

Se ha resuelto un problema en `EmailNotificationServiceProcessor` en el cual el método `getSegmentId` devolvía `null` después de la implementación de la revisión, lo que provocaba que los activadores de correo electrónico fallaran durante el procesamiento del flujo de trabajo. Restaura la lógica de resolución de ID de segmento correcta asegurándose de que el procesador recupera los valores `SegmentInfo` necesarios para admitir flujos de trabajo de notificaciones de correo electrónico en las instancias de AEM. (CQ-4359755)


## Instalar [!DNL Experience Manager] 6.5.23.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.23.0 requiere [!DNL Experience Manager] 6.5. Consulte la [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas. <!-- UPDATE FOR EACH NEW RELEASE -->
* La descarga del Service Pack está disponible en [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) de Adobe.
* En una implementación con MongoDB y varias instancias, instale [!DNL Experience Manager] 6.5.23.0 en una de las instancias de creación mediante el Administrador de paquetes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe no recomienda quitar ni desinstalar el paquete [!DNL Experience Manager] 6.5.23.0. Como tal, antes de instalar el paquete, debe crear una copia de seguridad de `crx-repository` en caso de que deba revertirla. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Instalar el Service Pack en [!DNL Experience Manager] 6.5{#install-service-pack}

1. Reinicie la instancia antes de la instalación si está en modo de actualización (cuando la instancia se haya actualizado desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de realizar la instalación, realice una instantánea o una copia de seguridad nueva de la instancia de [!DNL Experience Manager].

1. Descargue el Service Sack desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra el Administrador de paquetes y seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

1. Para actualizar el conector S3, detenga la instancia después de la instalación del Service Pack, sustituya el conector existente por un nuevo archivo binario, proporcionado en la carpeta de instalación, y reinicie la instancia. Consulte [Almacén de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo de la IU del administrador de paquetes a veces se cierra durante la instalación del Service Pack. Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete actualizador para asegurarse de que la instalación es correcta. Normalmente, este problema se produce en el explorador [!DNL Safari], pero puede ocurrir de forma intermitente en cualquier explorador.

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

1. Todos los paquetes OSGi tienen el valor **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web: `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es de la versión 1.22.20 o posterior (utilice la consola web: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### Instalar Service Pack para [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Para obtener instrucciones para instalar el Service Pack en Experience Manager Forms, consulte [Instrucciones de instalación del Service Pack de Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La funcionalidad Formularios adaptables, disponible en [AEM 6.5 Inicio rápido](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), está diseñada únicamente para la exploración y la evaluación. Para su uso en producción, es esencial obtener una licencia válida para AEM Forms, ya que la funcionalidad Formularios adaptables requiere una licencia adecuada.

### Instalación del paquete de índice de GraphQL para fragmentos de contenido de Experience Manager{#install-aem-graphql-index-add-on-package}

Los clientes que usen GraphQL deben instalar el [fragmento de contenido de Experience Manager con el paquete de índice 1.1.1 de GraphQL](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Al hacerlo, puede añadir la definición de índice necesaria según las funciones que utilizan realmente.

Si no se instala este paquete, las consultas de GraphQL pueden ser lentas o dar error.

>[!NOTE]
>
>Instale este paquete solo una vez por instancia; no es necesario reinstalarlo con cada Service Pack.

### UberJar{#uber-jar}

UberJar para [!DNL Experience Manager] 6.5.23.0 está disponible en el [repositorio de Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.22/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para utilizar UberJar en un proyecto de Maven, consulte [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

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
>UberJar y los demás artefactos relacionados están disponibles en el repositorio de Maven Central, en lugar del repositorio Maven público de Adobe (`repo.adobe.com`). Se ha cambiado el nombre del archivo principal de UberJar a `uber-jar-<version>.jar`. Por lo tanto, no hay `classifier`, con `apis` como valor, para la etiqueta `dependency`.



## Funciones en desuso y eliminadas{#removed-deprecated-features}

Consulte [Funciones obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md/) para obtener una lista detallada de todas las funciones obsoletas o eliminadas de AEM 6.5.

### Editor de SPA {#spa-editor}

[El Editor de SPA](/help/sites-developing/spa-overview.md) ha quedado obsoleto para nuevos proyectos a partir de la versión 6.5.23 de AEM 6.5. El editor de SPA sigue siendo compatible con los proyectos existentes, pero no debe utilizarse en nuevos proyectos.

Los editores preferidos para administrar contenido sin encabezado en AEM ahora son:

* [El editor universal](/help/sites-developing/universal-editor/introduction.md) para la edición visual.
* [El editor de fragmentos de contenido](/help/sites-developing/universal-editor/introduction.md) para la edición de contenido sin encabezado basada en formularios.

## Problemas conocidos{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **Problema con el paquete de scripts JSP en AEM 6.5.21-6.5.23 y AEM 6.5 LTS GA**
AEM 6.5.21, 6.5.22, 6.5.23 y AEM 6.5 LTS GA se envían con el paquete `org.apache.sling.scripting.jsp:2.6.0`, que contiene un problema conocido. El problema suele producirse con una carga alta cuando la instancia de AEM administra muchas solicitudes simultáneas.

  Cuando se produce este problema, puede aparecer una de las siguientes excepciones en los registros de errores junto con las referencias a `org.apache.sling.scripting.jsp:2.6.0`:

   * `java.io.IOException: classFile.delete() failed`
   * `java.io.IOException: tmpFile.renameTo(classFile) failed`
   * `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
   * `java.io.FileNotFoundException`

  Cuando se produce este error, el único método de recuperación es reiniciar la instancia de AEM.

  Póngase en contacto con Asistencia al cliente de Adobe y consulte esta nota de la versión para obtener una solución.

* **Relacionado con Oak**
A partir del Service Pack 13, ha comenzado a aparecer el siguiente registro de errores que afecta a la caché de persistencia:

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

   1. Instalar el Service Pack o reiniciar Experience Manager as a Cloud Service.
Las nuevas carpetas de `cache` y `diff-cache` se crean automáticamente y ya no experimentará una excepción relacionada con `mvstore` en `error.log`.

* Actualice las consultas de GraphQL que puedan haber usado un nombre de API personalizado para el modelo de contenido y utilizará el nombre predeterminado del modelo de contenido en su lugar.

* Una consulta de GraphQL puede emplear el índice `damAssetLucene`, en lugar del índice `fragments`. Esta acción podría provocar que las consultas de GraphQL fallen o tarden mucho en ejecutarse.

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
Para garantizar el funcionamiento correcto, debe añadir las siguientes propiedades al nodo de definición de índice `/oak:index/damAssetLucene` (no se requiere la reindexación):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Si actualiza la instancia de [!DNL Experience Manager] de la versión 6.5.0-6.5.4 al Service Pack más reciente de Java™ 11, verá excepciones `RRD4JReporter` en el archivo `error.log`. Para detener las excepciones, reinicie la instancia de [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Los usuarios pueden cambiar el nombre de una carpeta en una jerarquía de [!DNL Assets] y publicar una carpeta anidada en [!DNL Brand Portal]. Sin embargo, el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Durante la instalación de [!DNL Experience Manager] 6.5.x.x se pueden mostrar los siguientes errores y mensajes de advertencia:
   * “Cuando la integración de Adobe Target se configura en [!DNL Experience Manager] mediante la API de Target Standard (autenticación IMS) y, a continuación, se exportan fragmentos de experiencias a Target, se crean tipos de ofertas incorrectos. En lugar de “Experience Fragment”/source “Adobe Experience Manager”, Target crea varias ofertas con el tipo “HTML”/source “Adobe Target Classic”.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en `granite/operations/maintenance`.
   * La validación del lado del servidor de formularios adaptables falla cuando se utilizan funciones de agregado como SUM, MAX y MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en `granite/operations/maintenance`.
   * La zona interactiva de una imagen interactiva de Dynamic Media no está visible al previsualizar el recurso a través del visor de banners a la venta.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]`: tiempo de espera agotado para completar el cambio de registro sin registrar.

* A partir de AEM 6.5.15, el motor Rhino JavaScript proporcionado por el paquete ```org.apache.servicemix.bundles.rhino``` presenta un nuevo comportamiento de hoisting. Los scripts que utilizan el modo estricto (```use strict;```) deben declarar sus variables correctas. De lo contrario, no se ejecutan y terminan generando un error de tiempo de ejecución.

* La instalación del contenido listo para usar relacionado con el etiquetado mediante un paquete de actualización oficial restablece la propiedad de idiomas del nodo `/content/cq:tags` a su valor predeterminado. Esta acción se aplica a los paquetes de servicio, los paquetes de servicio de seguridad, los paquetes de funciones ampliadas, los paquetes de funciones acumulativas, los parches, etc. Por lo tanto, es necesario añadirlo desde las propiedades antes de la instalación.

### Problema conocido de AEM Sites {#known-issues-aem-sites-6523}

Fragmentos de contenido: la previsualización falla debido a la protección DoS para un gran árbol de fragmentos. Consulte el [artículo de KB sobre las opciones de configuración predeterminadas del ejecutor de consultas de GraphQL](https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)

### Problemas conocidos de AEM Forms {#known-issues-aem-forms-6523}

>[!NOTE]
>
> No actualice al Service Pack 6.5.23.0 por problemas que no tengan revisiones disponibles, ya que podría provocar errores inesperados. Actualice al Service Pack 6.5.23.0 solo después de que se publiquen las revisiones necesarias.

#### Problemas con revisiones disponibles {#aem-forms-issues-with-hotfixes}

Los siguientes problemas incluyen una revisión disponible para su descarga e instalación. Puede [descargar e instalar la revisión](/help/release-notes/aem-forms-hotfix.md) para resolver los siguientes problemas:

* **FORMS-20203**: cuando un usuario actualiza el marco de Struts de la versión 2.5.x a la 6.x, la interfaz de usuario de directivas de AEM Forms no muestra todas las configuraciones, como la opción de añadir una marca de agua.

* **FORMS-20360**: después de actualizar al Service Pack 6.5.23.0 de AEM Forms, el servicio de conversión ImageToPDF falla con el siguiente error:
  ```17:15:44,468 ERROR [com.adobe.pdfg.GeneratePDFImpl] (default task-49) ALC-PDG-001-000-ALC-PDG-011-028-Error occurred while converting the input image file to PDF. com/adobe/internal/pdftoolkit/core/encryption/EncryptionImp```

* **FORMS-20478**: Al intentar convertir archivos TIFF de tipo 7/8 a PDF, el proceso de conversión falla con el error “Error de conversión ALC-PDG-001-000-Image2Pdf, causado por: com/sun/image/codec/jpeg/JPEGCodec” y “ALC-PDG-016-003-Se produjo un error desconocido o inesperado durante el posprocesamiento de PDF”. El sistema intenta volver a intentarlo con el decodificador TIFF ImageIO de TM, pero finalmente no consigue completar el trabajo.

* **FORMS-14521**: si un usuario intenta obtener una vista previa de un borrador de carta con datos XML guardados, se queda atascado en el estado `Loading` para algunas cartas específicas.

* AEM Forms ahora incluye una actualización de la versión de Struts de la 2.5.33 a la 6.x para el componente de formularios. Esto proporciona cambios, anteriormente omitidos, de Struts que no se han incluido en el SP23. La compatibilidad se añadió a través de una [revisión](/help/release-notes/aem-forms-hotfix.md) que puede descargar e instalar para añadir compatibilidad con la última versión de Struts.

#### Otros problemas conocidos {#aem-forms-other-known-issues}

* Después de instalar AEM Forms JEE Service Pack 21 (6.5.21.0), si encuentra entradas duplicadas de Jars Geode `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` en la carpeta `<AEM_Forms_Installation>/lib/caching/lib` (FORMS-14926), siga estos pasos para resolver el problema:

   1. Detenga los localizadores, si están en funcionamiento.
   2. Detenga el servidor de AEM.
   3. Ir a `<AEM_Forms_Installation>/lib/caching/lib`.
   4. Quite todos los archivos de parche de Geode, excepto `geode-*-1.15.1.2.jar`. Confirme que solo están presentes los Jars Geode con `version 1.15.1.2`.
   5. Abra el símbolo del sistema en modo de administrador.
   6. Instale el parche de Geode mediante el archivo `geode-*-1.15.1.2.jar`.

* Cuando los usuarios actualizaban de AEM 6.5 Forms Service Pack 18 o 19 al Service Pack 20 o 21, encontraban un error de compilación de JSP. Este error les impedía abrir o crear formularios adaptables. También causó problemas con otras interfaces de AEM. Estas interfaces incluían el editor de páginas, la IU de AEM Forms, el editor de flujos de trabajo y la IU de información general del sistema. (FORMS-15256)

  Si tiene un problema de este tipo, siga estos pasos para resolverlo:
   1. Vaya al directorio `/libs/fd/aemforms/install/` en CRXDE.
   2. Elimine el paquete con el nombre `com.adobe.granite.ui.commons-5.10.26.jar`.
   3. Reinicie el servidor de AEM.

* En la Vista previa de impresión de la IU de Interactive Communications Agent, el símbolo de moneda (como el signo de dólar $) se muestra de forma incoherente para todos los valores de campo. Aparece para valores de hasta 999, pero falta para valores de 1000 y superiores. (FORMS-16557)
* Las modificaciones realizadas en el XDP de los fragmentos de diseño anidados en una comunicación interactiva no se reflejan en el editor de CI. (FORMS-16575)
* En la Vista previa de impresión de la IU de Interactive Communications Agent,  algunos valores calculados no se muestran correctamente. (FORMS-16603)
* Cuando la carta se ve en la Vista previa de impresión, el contenido cambia. Es decir, algunos espacios desaparecen y ciertas letras se reemplazan por `x`. (FORMS-15681)
* **FORMS-15428**: Después de actualizar al paquete de servicio 20 de AEM Forms (6.5.20.0) con el complemento de Forms, las configuraciones que dependen del servicio de Adobe Analytics Cloud heredado mediante autenticación basada en credenciales dejan de funcionar. Este problema impedía que las reglas de análisis se ejecutaran de forma correcta.

* Cuando un usuario configura una instancia de WebLogic 14c, el servicio PDFG en AEM Forms Service Pack 21 (6.5.21.0) en JEE que se ejecuta en JBoss® falla debido a conflictos del cargador de clases que implican la biblioteca SLF4J. El error se muestra de la siguiente manera (CQDOC-22178):

  ```java
  Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
  the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
  @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
  (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
  have different Class objects for the type org/slf4j/ILoggerFactory used in the signature.
  ```

* FORMS-21378: cuando la validación del lado del servidor (SSV) está habilitada, los envíos de formularios pueden fallar. Si tiene este problema, póngase en contacto con el Soporte técnico de Adobe para obtener ayuda.



## Paquetes de contenido y paquetes OSGi incluidos{#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en esta versión de [!DNL Experience Manager] 6.5 Service Pack:

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.23.0](/help/release-notes/assets/65230-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.23.0](/help/release-notes/assets/65230-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sitios web restringidos{#restricted-sites}

Estos sitios web solo están disponibles para los clientes. Si es cliente y necesita acceso, póngase en contacto con el administrador de cuentas de Adobe.

* [Descarga de producto en licensing.adobe.com](https://licensing.adobe.com/)
* [Contacte con el servicio de atención al cliente de Adobe](https://experienceleague.adobe.com/es/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página de productos](https://business.adobe.com/es/products/experience-manager/adobe-experience-manager.html?lang=es)
>* Documentación de[[!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/es/docs/experience-manager-65)
>* [Suscripción a las actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html)
