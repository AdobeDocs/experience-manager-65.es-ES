---
title: '[!DNL Experience Manager] Notas de la versión de service pack 6.5'
description: Notas de versión específicas de [!DNL Adobe Experience Manager] 6.5 service pack 9
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 19dd081674b4954498d6aa62335f6b5a9f2a4146
workflow-type: tm+mt
source-wordcount: '3835'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] Notas de la versión de service pack 6.5 {#aem-service-pack-release-notes}

## Información de la versión {#release-information}

| Productos | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.9.0 |
| Tipo | Versión de Service Pack |
| Fecha | 27 de mayo de 2021 |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9-1.0.zip) |

## Qué incluye [!DNL Adobe Experience Manager] 6.5.9.0 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.9.0 incluye nuevas funciones, mejoras clave solicitadas por los clientes y mejoras de rendimiento, estabilidad y seguridad, que se han publicado desde la publicación de la versión 6.5 en abril de 2019. El Service Pack se instala en [!DNL Adobe Experience Manager] 6.5.

Las funciones y mejoras clave introducidas en [!DNL Adobe Experience Manager] 6.5.9.0 son:

* [!DNL Experience Manager Sites] El componente Dynamic Media Foundation ahora permite activar o desactivar la optimización para dispositivos de mayor resolución al utilizar ajustes preestablecidos de imagen o Recorte inteligente interactivos.

* Para mejorar el rendimiento, la condición `hidden=false` se mueve de la consulta JCR al evaluador [!UICONTROL QueryBuilder]. Para comprobar que un predicado oculto funciona después del cambio, [!DNL Experience Manager] comprueba que no se muestra ninguna carpeta oculta.

* Posibilidad de restaurar páginas y árboles eliminados en una página [!DNL Experience Manager Sites].

* Compatibilidad para que un nuevo usuario actualice el token de acceso mediante un token de actualización para el servicio de configuración de correo.

* [Compatibilidad con el mecanismo SMTP XOAUTH2](/help/sites-administering/notification.md#setting-up-oauth)  para el servicio de configuración de correo.

* Compatibilidad con las versiones [!DNL MongoDB] 4.2 y 4.4.

* Las ocurrencias de nombres relacionados con Hong Kong, Macao y Taiwán se actualizan según las nuevas convenciones de nomenclatura para las regiones y configuraciones regionales chinas.

* Mejoras de accesibilidad en [!DNL Experience Manager] [[!DNL Assets]](#assets-accessibility-6590) y [[!DNL Dynamic Media]](#accessibility-dm-6590).

* El RGPD de imágenes inteligentes (proporción de píxeles de dispositivo) y la optimización del ancho de banda de red le permiten ofrecer imágenes de la mejor calidad de forma eficaz; en dispositivos con pantallas de alta resolución y ancho de banda de red restringido. Para obtener más información y cronología, consulte [preguntas frecuentes sobre imágenes inteligentes](/help/assets/imaging-faq.md).

* [!DNL Dynamic Media] delivery (modificador de `fmt` URL) es compatible con el formato de imagen de próxima generación AVIF (formato de imagen AV1). Para obtener más información y cronología, consulte [servicio de imágenes y renderización de API fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html).

* Capacidad para enviar un correo electrónico de notificación a un grupo mediante el paso de flujo de trabajo [!UICONTROL Asignar tarea].

* Capacidad para recuperar un borrador de comunicación interactiva después de modificar la comunicación interactiva de origen.

* Establezca un nombre de dominio personalizado para cargar, procesar y validar el servicio reCAPTCHA en [!DNL Experience Manager Forms].

* Mejoras en los datos de entrada para el paso de flujo de trabajo [!UICONTROL Invocar el servicio del modelo de datos de formulario].

* Capacidad para utilizar varias páginas de formato en una plantilla Documento de registro en [!DNL Experience Manager Forms].

* Saltos de página de soporte en Documento de registro en [!DNL Experience Manager Forms].

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.22.7.

Para obtener una lista completa de las funciones y mejoras introducidas en [!DNL Experience Manager] 6.5.9.0, consulte [novedades en [!DNL Adobe Experience Manager] 6.5 Service Pack 9](new-features-latest-service-pack.md).

>[!NOTE]
>
>A partir de Service Pack 9, los clientes [!DNL Experience Manager] pueden desarrollar y operar sus [!DNL Experience Manager] aplicaciones con distribuciones de las [!DNL Azul Zulu] compilaciones de OpenJDK, compatibles con los estándares de Java™ SE.
>El Adobe también proporciona soporte para los [!DNL Azul Zulu] JDK a los clientes [!DNL Experience Manager].
>Puede descargar las versiones relevantes de los [!DNL Azul Zulu] JDK desde [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
>Los derechos de uso de la tecnología Java™ de Oracle, tal como se distribuye por Adobe, expirarán a finales de diciembre de 2022. [!DNL Experience Manager] se recomienda a los clientes que planifiquen e implementen el uso de para los  [!DNL Azul Zulu] JDK a más tardar para esta fecha. Para obtener más información sobre el uso de la tecnología [!DNL Oracle Java™] y la tecnología [!DNL Azul Zulu], consulte las [preguntas frecuentes](https://experienceleague.adobe.com/docs/experience-manager-65/assets/adobe-azul-openjdk-license-agreement.pdf) asociadas.

La siguiente es la lista de correcciones que se proporcionan en la versión [!DNL Experience Manager] 6.5.9.0.

### [!DNL Sites] {#sites-6590}

* Las páginas publicadas con la propiedad Requisito de autenticación habilitada no redirigen a la página de inicio de sesión y devuelven el mensaje de error 404 (NPR-36354).

* Al crear un hipervínculo, la opción de buscar un vínculo no funciona en el componente de texto (NPR-35849).

* Se activa una consulta transversal al utilizar la API `com.day.cq.wcm.commons.ReferenceSearch`. Afecta al rendimiento del servidor [!DNL Experience Manager] (NPR-36407).

* El contenedor de diseño anidado dentro de otro contenedor de diseño cambiado de tamaño muestra un número incorrecto de columnas para sus componentes secundarios, lo que hace que estos componentes no se alineen a la cuadrícula (NPR-36359).

* El Comprobador de vínculos externos muestra vínculos externos válidos como vínculos no válidos (NPR-36289).

* Después de mostrar las referencias durante algún tiempo, el panel de referencias comienza a mostrar un mensaje de error (NPR-36167).

* Al mover un componente, el parsys creado automáticamente no tiene el nodo `sling:resourceType` (NPR-36165).

* Cuando se intenta sincronizar una Live Copy (mientras se utilizan configuraciones de implementación [!UICONTROL Activar en modelo] y [!UICONTROL Desactivar en modelo]) si se elimina un componente en el maestro de Live Copy, la sincronización falla y se registra un `NullPointerException` (NPR-36127).

* Cuando un usuario escribe texto improvisado para etiqueta (etiqueta que no existe en el sistema) y pulsa Intro, la etiqueta aparece debajo del campo pero cuando el fragmento de contenido se guarda y vuelve a abrir, la etiqueta improvisada desaparece (NPR-36132).

* La bandeja de entrada no tiene la opción de mostrar el estado de las operaciones asincrónicas (NPR-36104).

* Se crea un componente duplicado después de restaurar la herencia (NPR-36000).

* Al utilizar `RemoteContentRenderingService`, la solicitud al `RemoteContentRendererRequestHandler.getRequest` siempre incluye la página raíz del `ComponentExporter`, pero no incluye la página solicitada si no se incluye con el modelo raíz en función de la profundidad de recorrido y las opciones de filtrado establecidas. La solicitud siempre debe incluir la página solicitada para que el SPA tenga suficiente información para presentar una respuesta (NPR-35961).

* Los elementos onTime/offTime no se activan/desactivan en el onTime/offTime esperado (NPR-35936).

* Cuando publica una página que contiene un fragmento de experiencia que no tiene la propiedad `cq:lastModified` , se produce un `NullPointerException` (NPR-35914).

* Cuando se intenta cambiar el tamaño de un componente dentro de un contenedor, no es posible volver a cambiar el tamaño al tamaño original. Cuando se reduce el tamaño del contenedor de componentes, no es posible volver a establecer el tamaño en el original (NPR-35809).

* En el cuadro de diálogo de lanzamiento, activado en el editor o desde la Información general de Live Copy, los iconos de estado para páginas separadas, suspendidas o no creadas son incorrectos (NPR-35691).

* Despliegue de Multi-Site Manager en propiedades de página de formato ignorar la página de despliegue y las subpáginas de la casilla de verificación (NPR-35634).

* Falta la funcionalidad Restaurar árbol, disponible en la IU clásica en la IU táctil (CQ-4315352, CQ-4309415).

* Problemas al revertir la herencia y desplegar la página en una página [!DNL Experience Manager Sites] (NPR-36033).

### [!DNL Assets] {#assets-6590}

Las siguientes mejoras en la experiencia de usuario se realizan en [!DNL Assets]:

* Para ver los recursos que no están ordenados en función de ninguno de los parámetros [!UICONTROL Create], [!UICONTROL Modify] o [!UICONTROL Name], [!DNL Adobe Experience Manager] ofrece una opción [!UICONTROL None] dentro de las opciones [!UICONTROL Sort by]. La opción [!UICONTROL None] garantiza que los recursos de la interfaz de usuario de Assets (en las vistas Tarjeta, Columna y Perspectivas) estén en el mismo orden en que existen en el nodo JCR (NPR-36356).

* Para convertir el ID de correo electrónico en minúsculas en la respuesta de API ACP de [!DNL Adobe Experience Manager] se introduce un ajuste opcional; ya que los usuarios de [!DNL Adobe Asset Link] no podían registrar recursos si su ID no tenía todos los caracteres en minúsculas. El panel [!DNL Adobe Asset Link] consume la respuesta de API ACP de [!DNL Adobe Experience Manager] (CQ-4317704).

[!DNL Adobe Experience Manager] 6.5.9.0  [!DNL Assets] proporciona las siguientes mejoras de accesibilidad.

Se mejora el contraste (con fondo) del siguiente texto e iconos, de modo que los usuarios con visión y percepción de color limitadas puedan comprender:

* Título del recurso en la página [!UICONTROL Propiedades] (NPR-35967).
* Iconos de clasificación por estrellas en las secciones [!UICONTROL Clasificación] en varios lugares (NPR-36009).
* Texto en la vista de tarjeta del recurso y la carpeta (NPR-35966).
* Texto del marcador de posición en la vista [!UICONTROL Línea de tiempo] (NPR-35965).
* Nombres de recursos en los resultados de búsqueda de recursos (NPR-35964).
* Texto del marcador de posición en el cuadro de diálogo [!UICONTROL Uso compartido de vínculos] (NPR-35963).
* [!UICONTROL Metadatos],  [!UICONTROL estado] y   otro texto en la   lista, en el cuadro de diálogo  [!UICONTROL Ver ] configuración (NPR-35910).
*  Ubicación y  [!UICONTROL tipo para ] buscar textos de marcador de posición en búsqueda global (NPR-35909).
* Expanda y contraiga los iconos en el [!UICONTROL Árbol de contenido] (NPR-35908).
* Texto de [!UICONTROL Assets] en la página donde se muestran las carpetas de recursos (NPR-35905).
* Texto en la opción [!UICONTROL Metadatos de recursos], [!UICONTROL Estadísticas de uso] dentro de la opción [!UICONTROL Información general] en la página de detalles de recursos (NPR-35904).
* Texto para teclas de método abreviado para las opciones [!UICONTROL properties] y [!UICONTROL editar] en la página de detalles del recurso (NPR-35904).

[!DNL Adobe Experience Manager] 6.5.9.0  [!DNL Assets] corrige los siguientes problemas.

* Las etiquetas creadas dentro de un elemento de selección de etiquetas en un formulario [!UICONTROL Folder Metadata Schema] no se guardan (NPR-36119).

* Cuando se utiliza una elipse pequeña para anotar recursos, la elipse se superpone con el número de la anotación en la versión de impresión (NPR-36114).

* En algún momento, en la vista de columna, [!DNL Experience Manager] no solicita conflictos de recursos duplicados cuando se carga un recurso duplicado (NPR-36048).

* El cuadro de diálogo Compartir vínculo no se cierra haciendo clic en el botón Cerrar si se abre y no se realiza ningún cambio (NPR-36030).

* Cuando se seleccionan varios recursos para actualizar las propiedades, a veces se produce un error o se actualizan las propiedades de un recurso no seleccionado (NPR-36002).

* Cuando en la carga de recursos se añaden espacios en blanco al principio o al final de los nombres de los archivos de recursos, con caracteres restantes iguales al nombre de un recurso existente en el repositorio, el recurso existente se reemplaza sin registrar ningún error (NPR-36001).

* Cuando el vídeo se reproduce en la página de detalles del recurso, las opciones de reproducción y pausa no funcionan (NPR-35999).

* Al cancelar la publicación de recursos de forma masiva, Brand Portal genera un error que sugiere que el URI de la solicitud es demasiado largo (NPR-35954).

* Cuando se imprime un recurso con texto de anotación largo, el texto de la anotación se recorta, incluso si hay espacio disponible (NPR-35948).

* La opción para desplazarse a la página siguiente está desactivada al seleccionar la página en la vista Plantillas seleccionada en la página Crear catálogo (CQ-4315462).

* Cuando se inicia el flujo de trabajo de actualización de recursos en el recurso de vídeo, la página se actualiza repetidamente (CQ-4313375).

* Las carpetas DAM no se pueden eliminar ni mover, y se registra una excepción (NPR-35942).

### [!DNL Dynamic Media] {#dynamic-media-6590}

[!DNL Adobe Experience Manager] 6.5.9.0  [!DNL Assets] proporciona las siguientes mejoras de accesibilidad en  [!DNL Dynamic Media].

* Cuando abra el cuadro de diálogo para agregar recursos mediante teclas de teclado en el editor [!UICONTROL Conjunto de imágenes]:
   * Los lectores de pantalla narran que el cuadro de diálogo está abierto.
   * El foco del teclado pasa al cuadro de diálogo cuando se abre.
   * El foco del teclado vuelve a la opción Agregar recurso cuando se cierra el cuadro de diálogo (CQ-4312134).

* Ahora puede agregar y editar puntos interactivos en recursos utilizando teclas de teclado en el editor de puntos interactivos (CQ-4305965).

* Ahora puede colocar hipervínculos en puntos interactivos mediante la administración de puntos interactivos mediante teclas de teclado. El enfoque del lector de pantalla ahora se mueve al campo para editar la ruta de URL y la opción Abrir cuadro de diálogo de selección (CQ-4290735).

* Se mejora el contraste (con fondo) del texto y los controles en la página Editor de conjuntos de imágenes, de modo que los usuarios con visión y percepción limitadas del color puedan comprender (CQ-4290733).

* Ahora puede navegar a las opciones de uso compartido de recursos en el Editor de ajustes preestablecidos de visualizador y contraer la opción de uso compartido expandido mediante teclas de teclado (CQ-4290724).

* Ahora puede navegar y ver las informaciones de objeto en los iconos de información y los iconos de alerta en las pestañas Básico y Avanzado de la página Editar Codificación de Vídeo utilizando las teclas de teclado (CQ-4290722).

* Los lectores de pantalla ahora narran las instrucciones de varios campos en la pestaña Aspecto y Comportamiento del Editor de ajustes preestablecidos de visualizador (CQ-4290721).

* Al navegar por la página Editar ajuste preestablecido de imagen en el modo Formulario , el lector de pantalla narra el propósito y los nombres de varios campos y controles (CQ-4290717).

* Al navegar por la página de detalles de recursos, los lectores de pantalla ahora describen el propósito de varias opciones dentro de Visualizadores (CQ-4290716).

* Contraste (con fondo) del texto del marcador de posición Todas las representaciones en representaciones de la página de detalles del recurso se mejora, de modo que los usuarios con visión y percepción limitadas del color puedan comprenderlo (CQ-4290713).

* Ahora se proporciona un asterisco visual para indicar que el campo es obligatorio en el campo Título del recurso en el Editor de conjuntos de imágenes y los lectores de pantalla anuncian la información necesaria para el campo (CQ-4290712).

* Los lectores de pantalla ahora pueden acceder y narrar el propósito de varias opciones interactivas dentro de Visualizadores en la página de detalles de recursos (CQ-4290708).

Adobe Experience Manager 6.5.9.0 Assets corrige los siguientes problemas en [!DNL Dynamic Media]:

* Los ajustes preestablecidos de visualizador personalizados y CSS no se replican en [!DNL Dynamic Media] cuando [!DNL Dynamic Media] se activa de forma selectiva y se deshabilita por [default](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/config-dm.html#troubleshoot-dm-config) (NPR-36232).

* Cuando se intenta obtener una vista previa de las representaciones de vídeo en la página de detalles del recurso, los vídeos se cargan lentamente (CQ-4320122).

* La página del explorador no responde y se ralentiza al cargar más de 200 activos con Duplicate Asset Detector habilitado (CQ-4319633).

* Cuando se añade un recurso de imagen panorámica en el componente de medios panorámicos de una página, se registra un error de referencia no capturada (CQ-4317666).

* Cuando se implementa un visualizador de medios interactivo con fragmento de experiencia, el fragmento de experiencia no se abre desde el editor y se registra un error (CQ-4317655).

* [!UICONTROL Publicar en Dynamic ] Media no está disponible en las opciones de  [!UICONTROL Publicación ] rápida de la página   Propiedades (CQ-4317199).

* Los autores de sitios con permisos de solo lectura pueden utilizar la funcionalidad de recorte inteligente en los recursos y editar las representaciones recortadas inteligentes (CQ-4316450).

* Las anotaciones de vídeo no funcionan para rutas de carpeta en las que la configuración [!DNL Dynamic Media] no está habilitada, aunque la instancia [!DNL Experience Manager] esté configurada en modo [!DNL Dynamic Media] (CQ-4314950).

* Cuando el título de los recursos tiene caracteres de doble byte, multibyte, ASCII alto, cirílico, par sustituto, hebreo, árabe y GB18030, al publicar en Dynamic Media el título del recurso tiene un signo de interrogación (?) (CQ-4311872).

>Problemas conocidos de reproducción de vídeo en Dynamic Media *solo en el Experience Manager 6.5.9.0*:
>
>* 

   <!-- CQDOC-18116 -->You cannot play video renditions from the asset's Details page on Experience Manager - Dynamic Media running in hybrid mode.
>* 

   <!-- CQDOC-18116 -->You cannot stream videos on Experience Manager - Dynamic Media running in hybrid mode.


### Plataforma {#platform-6590}

* Cuando se genera una miniatura para un modelo y se implementan los cambios en la Live Copy, la herencia de algunos campos no funciona (CQ-4319517).

* Cuando cree una carpeta, seleccione la propiedad Orderable y agregue más de 20 recursos a la carpeta. Al seleccionar todos los recursos de la carpeta, se muestra un recuento incorrecto (CQ-4316243).

* Al actualizar una página, la ordenación de carpetas o recursos no muestra los resultados adecuados (CQ-4316200).

* La biblioteca JavaScript de controladores se actualiza a la versión 4.7.7 (NPR-36375).

* Los paquetes personalizados no se actualizan al instalar un nuevo paquete de código mediante el Administrador de paquetes (NPR-35949).

* Un paquete Sling `resourceresolver` está causando que la consulta `Sling:alias` falle (NPR-35335).

* La ruta de contexto se elimina al configurar SSL en el Experience Manager (NPR-35294).

* La excepción `SegmentNotFound` se devuelve después de una sesión de larga duración (NPR-36405).

### Integraciones {#integrations-6590}

* No se pueden guardar las propiedades de la página con la herencia habilitada para los Cloud Services de fragmentos de experiencias (NPR-36107).

* La paginación de la interfaz de usuario IMS y la carga diferida no muestran los resultados adecuados (NPR-36046).

* Al crear la configuración de A4T Target y seleccionar la fuente de informes como [!DNL Adobe Analytics], no hay grupos de informes habilitados para Adobe Target disponibles en la lista desplegable (NPR-36006).

### Proyectos {#projects-6590}

* No se pueden guardar las propiedades de un proyecto porque la ruta JCR al proyecto no se ha resuelto debido a una barra diagonal adicional (`/`) anexada a la ruta del proyecto (NPR-36191).

### Pantallas {#screens-6590}

* [!DNL Experience Manager Screens] los reproductores no se pueden autenticar si se utiliza un controlador de autenticación personalizado de dos factores (NPR-35854).

### Comercio {#commerce-6590}

* El asistente del [!UICONTROL Catálogo de comercio] no carga más de 40 elementos en la vista de columna (CQ-4318379).

### Proyectos de traducción {#translation-6590}

* Las opciones de actualización o sobrescritura no se muestran al retraducir una `es` a `es_es` página (NPR-36170).

* Cuando se selecciona la opción de aprobación automática para un proyecto con traducción humana, el estado del trabajo se muestra como `Unknown` (NPR-35981).

* Cuando traduce una página, la ruta de referencia de [!DNL Experience Fragments] no se actualiza a la ruta de referencia [!DNL Experience Fragment] de destino (NPR-35911).

* Cuando se realizan cambios en las páginas principal y secundaria y se envía la página principal para su traducción, también se traducen incorrectamente las páginas secundarias (NPR-35896).

* Cuando hay varios proyectos de traducción simultáneos para una página seleccionada, la opción [!UICONTROL Ir a proyectos] no se vincula al último proyecto de traducción (NPR-35454).

* Cuando publica recursos en [!DNL Dynamic Media], [!DNL Experience Manager] muestra un mensaje incorrecto para etiquetas no publicadas (CQ-4315914, CQ-4315913).

* Cuando se abre un trabajo eliminado, [!DNL Experience Manager] muestra un mensaje incorrecto (CQ-4315910).

### Flujo de trabajo {#workflow-6590}

* Al hacer clic en Completar, Delegar o Abrir acciones para elementos disponibles en la Bandeja de entrada, no hay ninguna pista visual para la finalización de estas acciones (NPR-36317).

### [!DNL Communities] {#communities-6590}

* En el filtrado de contenido no deseado, el sistema consume el 100% del espacio de memoria de Java™, lo que hace que el servidor Experience Manager no responda (NPR-36316, NPR-36493).
* En los foros, los datos de las sesiones JCR procedentes de `SearchCommentSocialComponentListProvider` se filtran (NPR-36235).
* La apertura de un mensaje de bandeja de entrada específico refleja todos los mensajes con paginación incorrecta y otros problemas (NPR-35917).

### [!DNL Brand Portal] {#brandportal-6590}

* El indicador de la función de abastecimiento de recursos se habilita automáticamente al configurar [!DNL Experience Manager Assets] con [!DNL Brand Portal] (NPR-36010).

### [!DNL Forms] {#forms-6590}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] lanza los paquetes de complementos una semana después de la fecha de lanzamiento programada del paquete de servicio de [!DNL Experience Manager].
>* Ahora puede desarrollar y operar aplicaciones con [!DNL Azul Zulu] compilaciones de [!DNL OpenJDK] para [!DNL Experience Manager Forms] en implementaciones OSGi.


**Formularios adaptables**

* Problemas de inicialización de idioma en [!DNL Experience Manager Forms] 6.5.7.0 mientras se generan varios diccionarios de traducción (NPR-36439).
* Cuando se añade un archivo adjunto al fragmento de formulario adaptable y se envía el formulario, [!DNL Experience Manager Forms] muestra el siguiente mensaje de error (NPR-36195):

   ```TXT
    POST /content/forms/af/attachmentissue/jcr:content/guideContainer.af.submit.jsp HTTP/1.1] com.adobe.aemds.guide.servlet.GuideSubmitServlet [AF] Invalid file name or mime type for file resulted in submission failure
   ```

* Cuando se utiliza la traducción humana para actualizar un diccionario y después previsualizar un formulario adaptable, no se muestran las modificaciones (NPR-36035).

**Comunicaciones interactivas**

* Cuando se carga una imagen mediante el canal de impresión de comunicaciones interactivas y se edita, la imagen ya no está visible (NPR-36518).

* Al editar un recurso de texto y rellenar un marcador de posición, todos los elementos interactivos se eliminan del panel de navegación (NPR-35991).

**Flujo de trabajo**

* Cuando llama al extremo REST de un servicio [!DNL Experience Manager Forms] en JBoss®, [!DNL Experience Manager] muestra el siguiente mensaje de error (NPR-36305):

   ```TXT
   Invalid input. The maximum length of 2000 characters was exceeded.
   ```

**BackendIntegration**

* No se puede guardar un modelo de datos de formulario mientras se vincula el argumento de servicio de lectura a un valor literal que contiene un guión (NPR-36366).

**Seguridad de los documentos**

* Al establecer la certificación y el HSM para GlobalSign, [!DNL Experience Manager Forms] muestra los mensajes de error `Unsuported Algorithm` y `Invalid TSA Certificate` al agregar una marca de tiempo a LTV (NPR-36026, NPR-36025).

**Servicios de documento**

* Actualizaciones en la biblioteca [!DNL Gibson] para la integración con [!DNL Experience Manager Forms] (NPR-36211).

**Base JEE**

* Cuando selecciona Administración de puntos de conexión en la interfaz de usuario de administración, [!DNL Experience Manager Forms] muestra el mensaje de error `endpoint registry failure` (CQ-4320249).

Para obtener información sobre las actualizaciones de seguridad, consulte la [[!DNL Experience Manager] página de boletines de seguridad](https://helpx.adobe.com/security/products/experience-manager.html).

## Instalar 6.5.9.0 {#install}

**Requisitos de configuración y más información**

* El Experience Manager 6.5.9.0 requiere el Experience Manager 6.5. Consulte [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas.
* La descarga del Service Pack está disponible en el Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* En una implementación con MongoDB y varias instancias, instale el Experience Manager 6.5.9.0 en una de las instancias de autor mediante el Administrador de paquetes.

>[!NOTE]
>
>Adobe no recomienda quitar o desinstalar el paquete [!DNL Adobe Experience Manager] 6.5.9.0.

### Instalación del Service Pack {#install-service-pack}

Para instalar el Service Pack en una instancia [!DNL Adobe Experience Manager] 6.5, siga estos pasos:

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (y este es el caso cuando la instancia se actualizó desde una versión anterior). Adobe también recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de la instalación, tome una instantánea o una copia de seguridad nueva de su instancia [!DNL Experience Manager].

1. Descargue el Service Pack desde [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9-1.0.zip).

1. Abra Administrador de paquetes y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y haga clic en **[!UICONTROL Install]**.

1. Para actualizar el conector S3, detenga la instancia después de instalar el Service Pack, sustituya el conector existente por un nuevo archivo binario proporcionado en la carpeta de instalación y reinicie la instancia. Consulte [Almacenamiento de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo en la interfaz de usuario del Administrador de paquetes a veces se cierra durante la instalación del Service Pack. Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete de actualización antes de asegurarse de que las instalaciones se realizan correctamente. Normalmente, esto sucede en [!DNL Safari] pero puede suceder de forma intermitente en cualquier explorador.

**Instalación automática**

Existen dos maneras de instalar automáticamente [!DNL Experience Manager] 6.5.9.0 en una instancia de trabajo:

A. Coloque el paquete en la carpeta `../crx-quickstart/install` cuando el servidor esté disponible en línea. El paquete se instala automáticamente.

B. Utilice la API [HTTP del Administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Utilice `cmd=install&recursive=true` para instalar los paquetes anidados.

>[!NOTE]
>
>Adobe Experience Manager 6.5.9.0 no es compatible con la instalación del Bootstrap.

**Validar la instalación**

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.9.0)` en [!UICONTROL Installed Products].

1. Todos los paquetes OSGi son **[!UICONTROL ACTIVE]** o **[!UICONTROL FRAGMENT]** en la consola OSGi (utilice la consola web: `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.3 o posterior (utilice la consola web: `/system/console/bundles`).

Para saber cuáles son las plataformas certificadas para funcionar con esta versión, consulte los [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

### Instalación del paquete de complementos de Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Omita este paso si no utiliza Experience Manager Forms. Las correcciones en Experience Manager Forms se entregan mediante un paquete de complementos independiente una semana después de la versión programada del Service Pack [!DNL Experience Manager].

1. Asegúrese de que ha instalado el Service Pack de Adobe Experience Manager.
1. Descargue el paquete de complementos de Forms correspondiente que aparece en las [versiones de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) para su sistema operativo.
1. Instale el paquete de complementos de Forms como se describe en [Instalación de paquetes de complementos de AEM Forms](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager 6.5.9.0 incluye una nueva versión de [Paquete de compatibilidad de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). Si utiliza una versión anterior del paquete de compatibilidad de AEM Forms y la actualiza al Experience Manager 6.5.9.0, instale la versión más reciente del paquete tras la instalación del paquete de complementos de Forms.

### Instalar Adobe Experience Manager Forms en JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Omita este paso si no utiliza AEM Forms en JEE. Las correcciones en Adobe Experience Manager Forms en JEE se entregan mediante un instalador independiente.

Para obtener información sobre la instalación del instalador acumulativo para Forms Experience Manager en JEE y la configuración posterior a la implementación, consulte las [notas de la versión](jee-patch-installer-65.md).

>[!NOTE]
>
>Después de instalar el instalador acumulativo para Experience Manager Forms en JEE, instale el último paquete de complementos de Forms, elimine el paquete de complementos de Forms de la carpeta `crx-repository\install` y reinicie el servidor.

### UberJar {#uber-jar}

UberJar para Experience Manager 6.5.9.0 está disponible en el [repositorio Maven Central](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.9-1.0/).

Para usar UberJar en un proyecto de Maven, consulte [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.9-1.0</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar y los otros artefactos relacionados están disponibles en el Repositorio Central de Maven en lugar del Repositorio de Maven Público de Adobe (`repo.adobe.com`). El nombre del archivo principal de UberJar cambia a `uber-jar-<version>.jar`. Por lo tanto, no hay `classifier`, con `apis` como valor, para la etiqueta `dependency`.

## Funciones en desuso {#removed-deprecated-features}

A continuación se muestra una lista de funciones y capacidades que están marcadas como obsoletas con [!DNL Experience Manager] 6.5.7.0. Las funciones se marcan como obsoletas inicialmente y luego se eliminan en una versión futura. Se proporciona una opción alternativa.

Revise si utiliza una función o una capacidad en una implementación. Además, planifique cambiar la implementación para utilizar una opción alternativa.

| Área | Función | Reemplazo |
|---|---|---|
| Integraciones | La pantalla de inclusión **[!UICONTROL AEM Cloud Services]** está en desuso. Con la integración de Experience Manager y Adobe Target actualizada en Experience Manager 6.5 para admitir la API de Adobe Target Standard, que utiliza la autenticación mediante el Adobe IMS y [!DNL Adobe I/O], y el creciente papel de Launch Adobe para instrumentar páginas de Experience Manager para el análisis y la personalización, el asistente de inclusión se ha vuelto funcionalmente irrelevante. | Configure las conexiones del sistema, la autenticación IMS de Adobe y las integraciones [!DNL Adobe I/O] a través de los respectivos servicios en la nube [!DNL Experience Manager]. |
| Conectores | El conector JCR de Adobe para Microsoft® SharePoint 2010 y Microsoft® SharePoint 2013 está obsoleto para Experience Manager 6.5. | N/D |

## Problemas conocidos {#known-issues}

* Si está actualizando la instancia [!DNL Experience Manager] de la versión 6.5 a la versión 6.5.9.0, puede ver `RRD4JReporter` excepciones en el archivo `error.log`. Reinicie la instancia para resolver el problema.

* Si instala [!DNL Experience Manager] 6.5 Service Pack 5 o un Service Pack anterior en [!DNL Experience Manager] 6.5, se eliminará la copia de tiempo de ejecución del modelo de flujo de trabajo personalizado de recursos (creado en `/var/workflow/models/dam`).
Para recuperar la copia de tiempo de ejecución, Adobe recomienda sincronizar la copia en tiempo de diseño del modelo de flujo de trabajo personalizado con su copia de tiempo de ejecución mediante la API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Si se cambia el nombre de una carpeta de la jerarquía en [!DNL Assets] y se publica en [!DNL Brand Portal] una carpeta anidada que contiene un recurso, el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelve a publicar la carpeta raíz.

* Cuando un usuario selecciona configurar un campo por primera vez en un formulario adaptable, la opción para guardar una configuración no se muestra en el Explorador de propiedades. Si se selecciona para configurar otro campo del formulario adaptable en el mismo editor, se resuelve el problema.

* Durante la instalación del Experience Manager 6.5.x.x pueden aparecer los siguientes errores y mensajes de advertencia:
   * &quot;Cuando la integración de Adobe Target se configura en Experience Manager mediante la API de Target Standard (autenticación IMS), la exportación de fragmentos de experiencias a Target provoca la creación de tipos de ofertas incorrectos. En lugar de tener que escribir &quot;Fragmento de experiencias&quot;/origen &quot;Adobe Experience Manager&quot;, Destino, se crean varias ofertas con el tipo &quot;HTML&quot;/origen &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La validación del lado del servidor del formulario adaptable falla cuando se utilizan funciones agregadas como SUM, MAX y MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La zona interactiva de una imagen interactiva de Dynamic Media no está visible al previsualizar el recurso mediante el visor de banners de ventas.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tiempo de espera de que el cambio de registro se complete sin registrar.

## Paquetes de contenido y paquetes OSGi incluidos {#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en [!DNL Experience Manager] 6.5.9.0:

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.9.0](assets/6590_bundles.txt)

* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.9.0](assets/6590_packages.txt)

## Sitios web restringidos {#restricted-sites}

Estos sitios web solo están disponibles para los clientes. Si es un cliente y necesita obtener acceso, póngase en contacto con su administrador de cuentas de Adobe.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/)
* Consulte [cómo ponerse en contacto con el Servicio de atención al cliente de Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Notas de la versión 6.5](/help/release-notes/release-notes.md)
* [[!DNL Experience Manager] página de producto](https://www.adobe.com/es/marketing/experience-manager.html)
* [[!DNL Experience Manager] Documentación de 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es)
* [Suscripción a las actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html)

