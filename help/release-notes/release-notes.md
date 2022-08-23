---
title: Notas de la versión para [!DNL Adobe Experience Manager] 6,5
description: '"Encuentre información sobre la versión, novedades, instale procedimientos y una lista de cambios detallada para [!DNL Adobe Experience Manager] 6.5."'
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 3c3efe108b020d9c64e456d409f114c8969f2723
workflow-type: tm+mt
source-wordcount: '3652'
ht-degree: 7%

---

# [!DNL Adobe Experience Manager] 6.5 Últimas notas de la versión de Service Pack {#aem-service-pack-release-notes}

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.13.0 |
| Tipo | Versión de Service Pack |
| Fecha | 26 de mayo de 2022 |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.13.0.zip) |

## ¿Qué incluye [!DNL Experience Manager] 6.5.13.0 {#what-is-included-in-aem}

[!DNL Experience Manager] 6.5.13.0 incluye nuevas funciones, mejoras clave solicitadas por los clientes y mejoras de rendimiento, estabilidad y seguridad, que se han publicado desde la disponibilidad inicial de la versión 6.5 en abril de 2019. [Instalar este Service Pack](#install) en [!DNL Experience Manager] 6.5.

Las principales funciones y mejoras introducidas en [!DNL Adobe Experience Manager] 6.5.13.0 son:

* Utilice CAPTCHA invisible en forma adaptable: Ahora puede utilizar un CAPTCHA invisible para mostrar el desafío CAPTCHA solo en el caso de una actividad sospechosa. Si no se encuentra ninguna actividad sospechosa, no se muestra el desafío CAPTCHA. Ayuda a evaluar la cumplimentación de formularios humanos sin requisitos de casilla de verificación, reducir los esfuerzos de personalización y mejorar la experiencia del usuario final. (NPR-38500)

* Se ha agregado compatibilidad para recuperar encabezados de respuesta en el posprocesador del Modelo de datos de formulario para los extremos REST. (NPR-38275)

* Ahora, al generar un archivo de traducción de formulario adaptable, la misma secuencia de textos que el archivo XLIFF generado es idéntica a la secuencia de componentes del correspondiente formulario adaptable. (NPR-37700)

* Cuando localiza un formulario adaptable y realiza incluso un pequeño cambio en el texto del idioma base, la traducción completa falta para todos los demás idiomas. El problema se ha solucionado en [!DNL Experience Manager] 6.5.13.0. (NPR-37189)

* Mejoras de accesibilidad para Forms:

   * Se ha agregado compatibilidad para que los lectores de pantalla reconozcan el encabezado y el cuerpo de una tabla a medida que continúa y las entidades conectadas. Ayuda a los lectores de pantalla a navegar correctamente por las tablas. (NPR-37139)
   * Se ha agregado compatibilidad para que los lectores de pantalla dejen de navegar por el espacio de trabajo del HTML hasta que se abra un cuadro de diálogo. (NPR-37134)

   <!-- 

    * Added ability to specify Screen Reader Text for Hyperlinks in Forms Designer.(NPR-36221)
  
  -->

Se han introducido las siguientes correcciones de errores, funciones clave y mejoras en [!DNL Experience Manager] 6.5.13.0:

<!-- The following issues are fixed in [!DNL Experience Manager] 6.5.13.0: -->

## [!DNL Assets] {#assets-6513}

* Al intentar editar un campo desplegable de solo lectura, el valor desplegable se restablece a vacío. (NPR-38389)
* El usuario no puede introducir un recurso de vídeo (.mp4) si no hay audio en el archivo de vídeo. El flujo de trabajo de recursos de actualización de DAM falla y refleja un mensaje de error. (NPR-38116)
* Al utilizar el Asistente para mover recursos para mover una carpeta que contenga recursos, el flujo de trabajo falla y refleja un mensaje de error. (NPR-38061)
* Error en el flujo de trabajo de transcodificación de FFmpeg para el perfil de vídeo FLV. (CQ-4343249)
* Después de actualizar a [!DNL Experience Manager] 6.5 SP10, el editor de metadatos de recursos no funciona correctamente. (CQ-4341359)
* Al abrir una colección inteligente guardada con el filtro de búsqueda aplicado como Publicar, el filtro de búsqueda cambia automáticamente a No publicado. (CQ-4341191)
* Al cambiar el idioma en **[!UICONTROL Preferencia de usuario]**, la etiqueta **[!UICONTROL Ordenar por]**, el botón desplegable y otras opciones dentro de las opciones de ordenación de la página principal del recurso no se reflejan en el idioma seleccionado. (CQ-4339306)
* Al añadir una regla a un campo desplegable en **[!UICONTROL Esquema de metadatos]**, el **[!UICONTROL Depender de]** no refleja la etiqueta de campo de la lista desplegable. (ASSETS-9442)
* La lista desplegable de metadatos de recursos deshabilitados no contiene valores. (ASSETS-8918)
* Al ver el recurso mediante **[!UICONTROL Más detalles]** en **[!UICONTROL Columna]** vista, se muestran anotaciones incorrectas. (ASSETS-8851)
* Al crear un recurso duplicado con una versión diferente, no se generan las representaciones. (ASSETS-8607)

* Un usuario no administrador puede publicar un recurso que ya ha sido desprotegido por otro usuario. (NPR-38128)
* El visor dimensional no funciona en Chrome 97. (CQ-4340456)
* El botón de descarga de recursos no muestra el menú completo en la página Detalles del recurso. (CQ-4336703)
* Cuando se usa el uso compartido de vínculos, algunas de las cadenas de la ventana de uso compartido de vínculos no están localizadas. (CQ-4330540)
* Al agregar elementos en Administrar publicación, la cadena que refleja el recuento de elementos seleccionados no se localiza. (CQ-4330491)

### [!DNL Dynamic Media] {#dynamic-media-6513}

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Zero day exploit with the Java™ Spring Core Framework (CVE-2022-22963) impacting Experience Manager 6.5.12. (ASSETS-9031) -->
* Vista previa segura basada en tokens para los recursos de Dynamic Media en AEM Authors. (ASSETS-4995)
* Al crear un ajuste preestablecido de imagen para Dynamic Media en [!DNL Experience Manager], el máximo permitido está limitado a 2000x2000 píxeles en la interfaz de usuario. Cuando el valor se aumenta a 2001 píxeles para la anchura o la altura, la variable **[!UICONTROL Guardar]** está desactivado. (ASSETS-5691)
* El usuario puede impedir que se carguen determinados formatos de archivo en Dynamic Media. (ASSETS-5693)
* Accesibilidad : Los usuarios con problemas de visualización que dependen de lectores de pantalla se ven afectados si el atributo Alt no se implementa en una imagen en la interfaz de usuario de ajustes preestablecidos de imagen. (ASSETS-9817)
* Accesibilidad : los lectores de pantalla se ven afectados a medida que los lectores de pantalla narran imágenes sin etiquetar para las imágenes presentes en el &quot;segmento de línea de tiempo&quot; y en la pestaña &quot;Acciones&quot;, cuando navegan al modo de flecha abajo. (ASSETS-5651)
* Accesibilidad: los lectores de pantalla se ven afectados, ya que los lectores de pantalla (NVDA/JAWS) no narran el nombre descriptivo (Enviar correo electrónico) para el botón &quot;Enviar correo electrónico&quot; en el cuadro de diálogo &quot;EmailLink&quot; del reproductor de vídeo, mientras navegan con los modos (Examinar/Cursor). (ASSETS-5641)
* Accesibilidad: el foco del teclado no se desplaza al botón &quot;Rehacer&quot; que aparece después de invocar el botón &quot;Deshacer&quot; en la página Editor de conjuntos de imágenes, mientras se navega con la tecla TAB del teclado. (ASSETS-5582)
* Accesibilidad: Los usuarios que dependen de lectores de pantalla se ven afectados porque el atributo Alt no se proporciona para una imagen de conjunto de imágenes que está presente en el encabezado Propiedades. (ASSETS-5576)
* Accesibilidad: los lectores de pantalla no están narrando la función de encabezado de `Cannot save this set` en el `Cannot save this set` alerta, mientras navega mediante la tecla de método abreviado de encabezado `H`y la tecla de flecha abajo. (ASSETS-5569)
* Accesibilidad : los usuarios que dependen de lectores de pantalla se ven afectados para navegar por los formularios. Encontrarán dificultades para comprender la información sobre los controles de formulario si NVDA no está narrando la información de etiqueta para los controles de giro &quot;Anchura y altura&quot;. Estos controles están presentes en el encabezado de recorte de imagen interactiva mientras se navega en el modo de formulario NVDA &quot;F&quot;. (ASSETS-5393)
* Después de agregar un componente de Dynamic Media en un sitio y de publicar la página, el recurso de Dynamic Media recién agregado no está visible en la página publicada ni en la página Vista previa. Este problema se producía tanto para los tipos de recursos de imagen como de vídeo. (ASSETS-9467)

## Comercio {#commerce-6513}

* &quot;todos&quot; tiene jcr:write en `/content/usergenerated/etc/commerce/smartlists`. (NPR-35230)
* La clasificación local de productos de comercio ya no funciona. (CQ-4343750)
* No se puede publicar rápidamente un producto desde la página de resultados de búsqueda después de cambiar las propiedades. (CQ-4343318)

## CRX {#crx-6513}

* No es posible descargar un paquete si tiene el carácter especial `+` en el nombre del paquete. (NPR-38102)

## [!DNL Forms] {#forms-65130}

<!-- * When you use the prefill service to fill an adaptive form that contains a fragment and the fragment contains a Text box that supports rich text, the form fails to submit, and the following error occurs:

  `[AF] [AEM-AF-901-004]: Encountered an internal error while submitting the form.` (NPR-38542) -->

* Los componentes Botón de opción, Casilla de verificación y Carga de archivo no se traducen correctamente del alemán al inglés. (NPR-38527)
* La codificación de código de barras PDF417 producida por [!DNL Experience Manager] Forms no es válido para un grupo de botones de radio. (NPR-38525)
* El siguiente error se produce al enviar un formulario adaptable.
   `WARN [10.172.114.236 [1650871578492] POST /lc/content/forms/af/public/DHS-3754-ENG/jcr:content/guideContainer.af.internalsubmit.jsp HTTP/1.1] com.adobe.aemds.guide.internal.impl.utils.SubmitDataCollector TemplateKey not found in merge json:cq:responsive` (NPR-38520)
* La opción Excluir campos ocultos del documento de registro no funciona. (NPR-38512)
* Después de agregar el componente Contenedor de Forms a una página Sitios , los usuarios no pueden navegar a una página Sitios diferente y la página Sitios se bloquea en algunas ocasiones. El problema aparece de forma intermitente. (NPR-38506)
* Los usuarios experimentan texto superpuesto en Adaptive Forms después de aplicar [!DNL Experience Manager] 6.5 Service Pack 11. (NPR-38376, CQ-4342472)
* Los usuarios encuentran una excepción al mover paneles de formulario adaptables al nuevo diseño interactivo. (NPR-38369)
* La compatibilidad con ECMASCRIPT 6 (ES6) no está habilitada para la biblioteca del cliente ` /libs/fd/expeditor/clientlibs/view`. (NPR-38358)
* Cuando utilice un [!DNL Experience Manager] Flujo de trabajo para enviar un correo electrónico en hebreo, el correo electrónico recibido al final del usuario contiene signos de interrogación (??) en lugar del texto en hebreo (NPR-38296).
* Los usuarios se desconectan aleatoriamente de [!DNL Experience Manager] Las instancias de publicación y los formularios adaptables no se envían. El problema aparece en [!DNL Experience Manager] instancias que utilizan Dispatcher. (NPR-38285)
* Cuando se utiliza la opción getFormDataString en una regla de Launch de Adobe para capturar los datos del formulario adaptable, la opción no devuelve los datos de Forms adaptables. (NPR-38283)
* [!DNL Experience Manager] 6.5 La API relacionada con java.acl.Group obsoleta de Forms y los siguientes mensajes de error aparecen en el archivo error.log:
   ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)
* Forms creado en alemán no puede traducir al inglés o a cualquier otro idioma. (NPR-38280)
* Cuando se utiliza una versión localizada de un formulario adaptable, el documento de registro (DoR) correspondiente no se localiza. (NPR-38235)
* Cuando se utiliza el paso Enviar correo electrónico para enviar un archivo adjunto junto con un correo electrónico, el archivo adjunto no conserva el nombre especificado en el paso Flujo de trabajo. (NPR-38216)
* Cuando se publica una nueva versión de la carta, los usuarios no pueden abrir los borradores de letras de versiones anteriores de las cartas. (NPR-38215, CQ-4342515)
* Al invocar un método de servicio de punto final SOAP del servicio JEE de AEM Forms en un botón, haga clic en configurado como regla de formulario adaptable, el servicio SOAP falla con la siguiente excepción:
   `ERROR* [0:0:0:0:0:0:0:1 [1624362360493] POST /content/forms/af/testsoapwsdl/jcr:content/guideContainer.af.dermis HTTP/1.1] com.adobe.aemds.guide.addon expeditor.servlet.ExpEditorServiceManager Error while making web service related call java.lang.Exception: createSOAPParam: JSONException`
* Al utilizar com.adobe.fd.pdfutility.services.PDFUtilityService#convertedPDFtoXDP para convertir un PDF al formato XDP, se devuelve un archivo XDP no válido. (NPR-38140, CQ-4342099)
* Cuando varios usuarios utilizan la gestión de correspondencia para generar cartas diferentes, en la vista previa se muestra una carta incorrecta para algunos usuarios. (NPR-38134)
* El componente AEM Forms incrustado en la página SITES utiliza el atributo width que tiene valor en % y no es válido según la validación del HTML W3C. Los usuarios encuentran un error de análisis incorrecto durante la validación del HTML. (NPR-38124)
* Los elementos de botones de opción y casillas de verificación para la mayoría de los temas de OOTB en formularios adaptables no forman parte del orden de tabulación (NPR-38108)
* Cuando un usuario agrega etiquetas de HTML a la sección de comentarios mientras ejecuta un flujo de trabajo, se representan las etiquetas de HTML. (NPR-37591)
* Al importar y publicar una carta que incluya un nuevo archivo XDP, las letras no se previsualizan en la instancia de publicación. Sin embargo, si las letras se importan y publican por segunda vez utilizando el mismo archivo CMP, las letras se previsualizan correctamente. (CQ-4343599)
* Un formulario con la propiedad Preparar proceso de datos establecida no se puede procesar en HTML Workspace. (CQ-4343294)
<!--
For static PDF forms that are created with Forms 6.5 Designer, PDF accessibility fails with error `Tab order entry in page with annotations not set to "S"`. (CQ-4343117) 
 -->
* No se puede convertir una imagen a PDF mediante el servicio PDFG con OCR, después de aplicar el parche AEMForms-6.5.0-0038 (log4jv2.16). (CQ-4342450)

<!-- 
* Incorrect value is displayed for barcode SSCC-18. Forms servers omit the value on the right part of the barcode. (CQ-4342400)
-->
* No se puede importar un archivo Microsoft® Word a Forms Designer. El usuario encuentra errores `Word (version XP or onwards) could not be found on the machine`. (CQ-4342146)

<!-- 
* In Forms 6.5 Designer, when you open a form created with Forms 6.1 Designer and edit a textbox, paragraph spacing exceeds the specified space. All previous settings to the space are removed and manual reformatting of the text box is required. (CQ-4341899) 
-->
* El usuario no puede establecer el tiempo personalizado en el planificador de purga de trabajos. (CQ-4339192)
* El usuario no puede actualizar ninguna configuración en la interfaz de usuario de administración de puntos finales y encuentra un error ` Uncaught ReferenceError: updateEndpoint_required is not defined`. (CQ-4331523)
* En el caso de las etiquetas no válidas, la gestión correcta del mensaje de error no funciona como se esperaba. (NPR-38106 y CQ-4337173)

>[!NOTE]
>
>* [!DNL Experience Manager Forms] lanza los paquetes de complementos una semana después de la fecha de lanzamiento programada del paquete de servicio de [!DNL Experience Manager].


## Granite {#granite-6513}

* Omnisearch devuelve el resultado para los usuarios sin derechos de lectura. (NPR-38373)
* Habilitar ES6 para `/libs/granite/configurations/clientlibs/confbrowser`. (NPR-38300)

## Integraciones {#integrations-6513}

* Fuga de sesiones de resolución de recursos en el servicio Test and Target desde UserInfoServlet obsoleto. (NPR-38112)

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * AEM‑OP‑13 ‑ HTTP Parameter Pollution in `com.day.cq.searchpromote.impl.servlet`. (NPR-38033) -->
<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Analytics 2.0 IMS support added to Experience Manager 6.5. (NPR-37914) -->

## Oak: indexación y consultas {#oak-6513}

* La versión de Oak para 6.5.13.0 ahora se actualiza a 1.22.11. (NPR-38084) -->

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Create a CFP based on latest 6.5.12 and update Oak-related bundle versions. (NPR-38144) -->

## Plataforma {#platform-6513}

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * RTC : Universal XSS through cq-rewriter HtmlParser. (NPR-38064) -->
* Actualizar la dependencia de `org.apache.httpcomponents.httpclient` en [!DNL Experience Manager] 6.5. (NPR-37999)
* Carga de Autor alta debido a las sugerencias de campo de ruta. (CQ-4341826)
* El usuario debe actualizar la página cuando cambie el proyecto de la vista de tarjeta a la vista de calendario. (CQ-4340368)
* Las etiquetas se pierden debido a las restricciones de permisos. (CQ-4339543)
* Varios problemas notificados con Buscar y filtrar en Selección de rutas no funcionan. (CQ-4339402)
* Dejar de utilizar DTM en 6.5: cambie a Launch para la instrumentación Omega y añada compatibilidad con Gainsight. (CQ-4337809)
* Restringir la función de búsqueda de componentes de campo de ruta en función de la propiedad de filtro de campo de ruta establecida. (CQ-4309556)
* [!DNL Experience Manager] Plataforma 6.5: Correcciones de nombres de configuraciones regionales chinas. (CQ-4308978)
* Cambie a Launch para la instrumentación Omega. (NPR-38377)
* [!DNL Experience Manager] Plataforma 6.5: Correcciones de nombres de configuración regional en chino. (CQ-4308978)

## Replicación {#replication-6513}

* Publicación del nodo de usuario que falla de Autor a Editor. (NPR-38005)

## [!DNL Sites] {#sites-6513}

### Administrador {#sites-admin-6513}

* Se ha introducido una regresión con SP 12 que podría haber causado un problema al mover páginas. (SITES-5298)

### Interfaz de usuario clásica {#sites-classicui-6513}

* RTE: La imagen actualizada no está visible cuando se arrastra una nueva imagen sobre una imagen existente. (NPR-38141)

<!-- version 2 of description above * Updated Image is not visible When a new image is dragged on top of an existing image the updated image is not visible in RTE - Classic UI. (NPR-38141) -->

### Fragmentos de contenido {#sites-contentfragments-6513}

* Compatibilidad con la creación de modelos de fragmento de contenido en subconfiguraciones. (NPR-38054)

<!-- version 2 of description above * The Configuration Manager now allows you to set the Content Fragment Model config on a sub-config folder. (NPR-38054) -->
* Mejore el rendimiento al utilizar la validación &quot;Campo único&quot; en el Modelo de fragmento de contenido. (NPR-38142)

<!-- version 2 of description above * The unique field validation query is now fixed. (NPR-38142) -->
* Mejorar el tiempo de respuesta al abrir el Editor del modelo de fragmento de contenido. Es posible que los clientes con numerosos fragmentos en Assets hayan visto errores al abrir. (SITES-6284)

<!-- version 2 of description above * If the customer is trying to access the editor of the content fragment models, they get a query error because of too many fragments on the dam. (SITES-6284) -->
* Se ha introducido una regresión al actualizar de 6.5.11 a 6.5.12 que podría haber causado errores del Editor del modelo de fragmento de contenido. (SITES-5088 y SITES-4967)

<!-- version 2 of description above * Paths were getting deleted when AEM 6.5.12.0 was installed on existing 6.5.11.0 instance. (SITES-5088)
* Apple 6.5.10 system crashing when using CF model editor, due to erroneous feature toggle check. (SITES-4967) -->
* Mejore la localización de la interfaz de usuario del Editor del modelo de fragmento de contenido. (NPR-38126)

<!-- version 2 of description above * Some strings in the Content Fragment Model editor are not localized. (NPR-38126) -->
* Se ha corregido un problema que, al cerrar el Editor de fragmentos de contenido, podía producirse un error cuando se usaba el servidor Autor con Dispatcher. (NPR-38205)

<!-- version 2 of description above * Update of Content Fragment references is returning an invalid JSON response via Dispatcher. (NPR-38205) -->
* Se ha corregido un problema que impedía guardar un modelo cuando se utilizaba la validación en un campo RTE. (NPR-38210)

<!--version 2 of description above * Content Fragment Model Rich Text Validation Prevents Blocks Saving a Content Fragment Model. (NPR-38210) -->
* Problema con el fragmento de contenido con la propiedad booleana que no muestra Texto de campo en &quot;título&quot; en lugar de mostrar &quot;Nombre de propiedad&quot;. (NPR-38244)
* Error al ejecutar la consulta persistente con la variable de consulta mediante Postman. (NPR-38251, NPR-38057)
<!--version 2 of description above * An unexpected error message is coming in Postman, when executing the graphQL persisted query having query variables. (NPR-38251) -->
* Componente de fragmento de contenido: Se ha corregido la regresión en la opción &quot;gestione encabezados como párrafos&quot; que era 6.5 SP7. (NPR-38055)

<!--version 2 of description above * After applying SP11 to the Publish instance of AEM 6.5.6, the display result of the Content Fragment set in the published page changes. (NPR-38055) -->
* Se ha introducido una regresión de corrección en la versión 6.5.11 que puede haber causado errores de búsqueda de recursos. (SITES-4784)

<!--version 2 of description above * Adapt external index package to use selection Policy (fragment versus asset index). (SITES-4784) -->
* Uso **[!UICONTROL Editar]** de los resultados de búsqueda podrían resultar en un `Not Found` error. (NPR-37810)

<!--version 2 of description above * When editing Content Fragment from the Assets Search Rail results page, it throws 'Not Found' error. (NPR-37810) -->

### ContentHub {#sites-contenthub-6513}

* Los modelos de interfaz de usuario de Context Hub no se representan correctamente sin actualizar la página. (NPR-38212)

### Editor de correo electrónico {#sites-emaileditor-6513}

* Habilite la compatibilidad para la próxima versión de los componentes principales de correo electrónico [https://github.com/adobe/aem-core-email-components](https://github.com/adobe/aem-core-email-components). (NPR-38445 y NPR-38204)

<!-- version 2 of description above * Allow new email templated under campaign and ambit. (NPR-38445) * The "Approve for Adobe Campaign" workflow was only running for pages which are of type or extending the resource types: "mcm/neolane/components/newsletter", "mcm/campaign/components/newsletter" and "mcm/campaign/components/campaign_newsletterpage". (NPR-38204) -->

### Fragmentos de experiencias {#sites-experiencefragments-6513}

* Al utilizar la acción Navegar a página en Referencias para un fragmento de experiencia, se abre la página incorrecta. (NPR-38062)
* Las propiedades de diseño procedentes de una plantilla XF no se observan en un lado de una página. (NPR-38214)
* Se ha mejorado el rendimiento del cálculo de referencia XF. (NPR-38269)

<!-- version 2 of description above * Job queue configuration is incorrect - The OSGi configuration for the reference updater job queue has not been ported back to 6.5. This issue leads to jobs being run in the main queue, which has a higher priority and allows more jobs to run in parallel. This flow can lead to CPU exhaustion. (NPR-38269) -->

### Editor de página {#sites-pageeditor-6513}

* Mejore el deshacer de los componentes que no tienen la función inlineEditing o dropTarget en `cq:editConfig`. (NPR-38361)

<!-- version 2 of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* Es posible que la lista desplegable Sistema de estilos se haya colocado en la parte superior de la página en lugar de en el contexto del componente, para los componentes que utilizan `cq:editConfig` &quot;después de editar: REFRESH_PAGE&quot;. Este problema ya está resuelto. (NPR-38384)

<!-- version 2 of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig “afteredit: REFRESH_PAGE”. (NPR-38384) -->
* El componente de texto está desalineado cuando se agrega a los contenedores de diseño anidados. (NPR-38193)
* Se mostraba una ficha de estilo vacía cuando no había ninguna configuración del sistema de estilos para un componente; la pestaña ahora está oculta cuando no hay ninguna configuración presente. (NPR-38218)
<!-- version 2 of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* La propiedad `useLegacyResponsiveBehaviour` solo funciona cuando se autentica. (NPR-37996)
* La actualización de jquery-ui a la versión más reciente provocaba la ruptura del Editor. (SITES-5647)

### Seguridad {#sites-security-6513}

* A veces, la interfaz de usuario de Administración de grupos de usuarios no eliminaba usuarios, especialmente en grupos con más de 20 usuarios. (NPR-38041)

<!--version 2 of description above * Cannot remove users from user groups. (NPR-38041) -->

### SEO {#sites-seo-6513}

* El Generador de mapas del sitio y la etiqueta canónica añaden compatibilidad para las direcciones URL sin .html. (CIF-2647)
* Añada compatibilidad para eliminar idiomas alternativos utilizando la configuración noindex. (CIF-2496)
* Añada compatibilidad para proporcionar una dirección URL personalizada para sobrescribir la dirección URL canónica predeterminada de las páginas con contenido casi idéntico. (CIF-2747)

### SPA Editor y SDK {#sites-spa-sdk-6513}

* A partir de la versión 6.5.13, ya no debe crear el nodo de componente contenedor en JCR antes de realizar ediciones mediante el Editor de SPA. A `virtual container` se crea antes de guardarlo mediante el SDK. (SITES-5762)

<!-- version 2 of description above * Virtual container support - Adding a child component to a virtual container that is not yet present in the database implies the creation of a node to represent the container in content structure. (SITES-5762) -->

### Editor de plantillas {#sites-templateeditor-6513}

* Se ha corregido la regresión de que la publicación de una plantilla modificada no estaba publicando todas las dependencias. (NPR-38274)

<!-- version 2 of description above * Template changes do not get published until you publish a page that uses that template. (NPR-38274) -->
* TemplatedResource valueMap debe permitir lecturas profundas según la API de ValueMap. (NPR-38439)

## Sling {#sling-6513}

<!-- OBSOLETE BASED ON CQDOC-19400 * Memory leak in `DiscoveryLiteDescriptor`. (NPR-38288) -->
* Actualizar `sling-javax.activation` paquete con corrección de SLING-8777. (NPR-38077)

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Security issues reported under `org.apache.sling.scripting.jst`. (NPR-38067) -->

## Proyectos de traducción {#translation-6513}

* Se crean varios lanzamientos para páginas a las que se hace referencia/xf. (NPR-38263)
* Se ha cambiado el comportamiento de añadir páginas a proyectos de traducción desde Service Pack 10. El proyecto de traducción no contiene una página recién creada [ex: test-page-women-2] en la lista, cuando se selecciona el elemento principal de la página recién creada [no la página recién creada directamente]. (NPR-38256)
* Agregar `cq:isTranslationLaunch` en Lanzamientos creados por Translation Project. (NPR-38224)
* Launch se está creando para una página con un XF al que se hace referencia y que tiene un recurso en ella. (NPR-38199)
* [!DNL Experience Manager] la actualización de la memoria de traducción no funciona. (NPR-38196)
* Habilitar ES6 para `/libs/cq/gui/components/projects/admin/translation/job/addcontent/clientlibs.js`. (NPR-38306)
* Último paquete de 18n para traducciones para [!DNL Experience Manager] 6.5. (CQ-4339505)

## Interfaz de usuario {#ui-6513}

* Actualizar a `favicon.ico` que se utiliza en Experience Manager. (CQ-4315324)
* Cuando se encuentra en la página de inicio > Sección de herramientas y haga clic en el botón [!DNL Experience Manager] el icono [!DNL Experience Manager] La pantalla de navegación debería aparecer. (NPR-38417)
* Habilitar ES6 para `/libs/granite/ui/references/clientlibs/coral/references`. (NPR-38303)
* Habilitar ES6 para `/libs/granite/datavisualization/clientlibs/d3-3.x`. (NPR-38302)
<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * AEM‑OP‑09 ‑ Persistent cross‑site scripting selecting paths in templates. (NPR-38301) -->
* El selector de fechas en la IU táctil se muestra en coreano. (NPR-38079)
* Cuadro de diálogo de creación con varios campos, tras reordenar los campos y perder el valor de selección del botón de radio. (NPR-38063)

## WCM {#wcm-6513}

* [!DNL Experience Manager] MCM (Campaign) 6.5: Correcciones de nombres de configuraciones regionales chinas. (CQ-4308973)
* ResourceResolver no cerrado en com.day.cq.wcm.workflow.impl.WcmWorkflowServiceImpl.autoSubmitPageAfterModification (NPR-38286)

## Instalar [!DNL Experience Manager] 6.5.13.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback -->

* [!DNL Experience Manager] 6.5.13.0 requiere [!DNL Experience Manager] 6.5. Véase [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas.
* La descarga del Service Pack está disponible en Adobe [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html).
* En una implementación con MongoDB y varias instancias, instale [!DNL Experience Manager] 6.5.13.0 en una de las instancias de autor que utiliza el Administrador de paquetes.

>[!NOTE]
>
>El Adobe no recomienda quitar o desinstalar el [!DNL Experience Manager] Paquete 6.5.13.0.

### Instale el Service Pack en [!DNL Experience Manager] 6,5 {#install-service-pack}

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (cuando la instancia se actualizó desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de la instalación, tome una instantánea o una copia de seguridad nueva de su [!DNL Experience Manager] instancia.

1. Descargue el Service Pack desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.13.0.zip).

1. Abra Administrador de paquetes y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

1. Para actualizar el conector S3, detenga la instancia después de instalar el Service Pack, sustituya el conector existente por un nuevo archivo binario proporcionado en la carpeta de instalación y reinicie la instancia. Consulte [Almacenamiento de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo en la interfaz de usuario del Administrador de paquetes a veces se cierra durante la instalación del Service Pack. Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete de actualización antes de asegurarse de que las instalaciones se realizan correctamente. Normalmente, este problema ocurre en [!DNL Safari] pero puede ocurrir de forma intermitente en cualquier explorador.

**Instalación automática**

Hay dos métodos diferentes que puede utilizar para instalar automáticamente [!DNL Experience Manager] 6.5.13.0.

* Coloque el paquete en `../crx-quickstart/install` cuando el servidor esté disponible en línea. El paquete se instala automáticamente.
* Utilice la variable [API HTTP del Administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Uso `cmd=install&recursive=true` para que se instalen los paquetes anidados.

>[!NOTE]
>
>[!DNL Experience Manager] 6.5.13.0 no admite la instalación del Bootstrap.

**Validar la instalación**

Para saber cuáles son las plataformas certificadas para funcionar con esta versión, consulte la [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.13.0)` under [!UICONTROL Productos instalados].

1. Todos los paquetes OSGi son: **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web: `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.3 o posterior (utilice la consola web: `/system/console/bundles`).


### Instalar [!DNL Experience Manager] Paquete de complementos de Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Omitir si no utiliza [!DNL Experience Manager] Forms. Correcciones en [!DNL Experience Manager] Forms se entrega a través de un paquete de complementos independiente una semana después de la programación [!DNL Experience Manager] Versión de Service Pack.

1. Asegúrese de que ha instalado la variable [!DNL Experience Manager] Service Pack.
1. Descargue el paquete de complementos de Forms correspondiente que aparece en las [versiones de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) para su sistema operativo.
1. Instale el paquete de complementos de Forms como se describe en [Instalación de paquetes de complementos de AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).
1. Si utiliza letras en Experience Manager 6.5 Forms, instale la variable [último paquete de compatibilidad de AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates).

### Instalar [!DNL Experience Manager] Forms en JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Omita este paso si no utiliza AEM Forms en JEE. Correcciones en [!DNL Experience Manager] Forms en JEE se entrega a través de un instalador independiente.

Para obtener información acerca de la instalación del instalador acumulativo para [!DNL Experience Manager] Forms en JEE y la configuración posterior a la implementación, consulte la [notas de la versión](jee-patch-installer-65.md).

>[!NOTE]
>
>Después de instalar el instalador acumulativo para [!DNL Experience Manager] Forms en JEE, instale el último paquete de complementos de Forms, elimine el paquete de complementos de Forms del `crx-repository\install` y reinicie el servidor.

### UberJar {#uber-jar}

UberJar para [!DNL Experience Manager] La versión 6.5.13.0 está disponible en la [Repositorio de Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/)(https://).

Para usar UberJar en un proyecto de Maven, consulte [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.13</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar y los otros artefactos relacionados están disponibles en el Repositorio Central de Maven en lugar del Repositorio de Maven Público de Adobe (`repo.adobe.com`). Se cambia el nombre del archivo UberJar principal a `uber-jar-<version>.jar`. Así que no hay `classifier`, con `apis` como valor, para la variable `dependency` etiqueta.

## Funciones en desuso {#removed-deprecated-features}

A continuación se muestra una lista de funciones y capacidades que están marcadas como obsoletas con [!DNL Experience Manager] 6.5.7.0. Las funciones se marcan como obsoletas inicialmente y después se eliminan en una versión futura. Se proporciona una opción alternativa.

Revise si utiliza una función o una capacidad en una implementación. Además, planifique cambiar la implementación para utilizar una opción alternativa.

| Área | Función | Reemplazo |
|---|---|---|
| Integraciones | La variable **[!UICONTROL Inclusión de AEM Cloud Services]** ya que la función [!DNL Experience Manager] y [!DNL Adobe Target] la integración se actualiza en [!DNL Experience Manager] 6.5. La integración es compatible con la API de Adobe Target Standard. La API utiliza la autenticación mediante Adobe IMS y [!DNL Adobe I/O]. Apoya el creciente papel de Adobe Launch como instrumento [!DNL Experience Manager] páginas para analytics y personalización, el asistente de inclusión es funcionalmente irrelevante. | Configure las conexiones del sistema, la autenticación IMS de Adobe y [!DNL Adobe I/O] integraciones a través de las [!DNL Experience Manager] servicios en la nube. |
| Conectores | El conector JCR de Adobe para Microsoft® SharePoint 2010 y Microsoft® SharePoint 2013 está obsoleto para [!DNL Experience Manager] 6.5. | N/D |

## Problemas conocidos {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

<!-- VULNERABILITY ISSUE - REMOVED MAY 23, 2022 AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * If you are using Content Fragments and GraphQL, Adobe recommends that you install the following packages on top of 6.5.12.0:

  * [AEM 6.5.12 Sites HotFix-NPR-38144](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Faem-service-pkg-6.5.12.0-NPR-38144-B0002.zip) (this hot fix replaces SP12, but can be installed on top of SP12) -->

* [AEM fragmento de contenido con el paquete de índice 1.0.3 de GraphQL](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.3.zip)

* Como [!DNL Microsoft® Windows Server 2019] no es compatible [!DNL MySQL 5.7] y [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] no admite instalaciones llave en mano para [!DNL AEM Forms 6.5.10.0].

* Si actualiza su [!DNL Experience Manager] de la versión 6.5 a la versión 6.5.10.0, puede ver `RRD4JReporter` las excepciones de `error.log` archivo. Para resolver el problema, reinicie la instancia.

* Si instala [!DNL Experience Manager] 6.5 Service Pack 10 o un Service Pack anterior en [!DNL Experience Manager] 6.5, la copia en tiempo de ejecución del modelo de flujo de trabajo personalizado de recursos (creado en `/var/workflow/models/dam`).
Para recuperar la copia de tiempo de ejecución, Adobe recomienda sincronizar la copia en tiempo de diseño del modelo de flujo de trabajo personalizado con su copia de tiempo de ejecución mediante la API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Los usuarios pueden cambiar el nombre de una carpeta de una jerarquía [!DNL Assets] y publicar una carpeta anidada en [!DNL Brand Portal]. Sin embargo, el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Cuando un usuario selecciona configurar un campo por primera vez en un formulario adaptable, la opción para guardar una configuración no se muestra en el Explorador de propiedades. Si se selecciona para configurar otro campo del formulario adaptable en el mismo editor, se resuelve el problema.

* Durante la instalación de [!DNL Experience Manager] 6.5.x.x:
   * &quot;Cuando la integración de Adobe Target está configurada en [!DNL Experience Manager] con la API de Target Standard (autenticación IMS) y luego exportar fragmentos de experiencia a Target se crean tipos de oferta incorrectos. En lugar de tener que escribir &quot;Fragmento de experiencias&quot;/origen &quot;Adobe Experience Manager&quot;, Destino, se crean varias ofertas con el tipo &quot;HTML&quot;/origen &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La validación del lado del servidor del formulario adaptable falla cuando se utilizan funciones agregadas como SUM, MAX y MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La zona interactiva de una imagen interactiva de Dynamic Media no está visible al previsualizar el recurso mediante el visor de banners de ventas.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tiempo de espera de que el cambio de registro se complete sin registrar.

* Al intentar mover, eliminar o publicar fragmentos de contenido o sitios o páginas, hay un problema cuando se recuperan referencias de fragmentos de contenido, ya que la consulta en segundo plano falla; es decir, la funcionalidad no funciona.
Para garantizar la operación correcta, debe añadir las siguientes propiedades al nodo de definición de índice `/oak:index/damAssetLucene` (no se requiere reindexación):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## Paquetes de contenido y paquetes OSGi incluidos {#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en [!DNL Experience Manager] 6.5.13.0:

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.13.0](/help/release-notes/assets/65130_bundles.txt)

* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.13.0](/help/release-notes/assets/65130_packages.txt)

## Sitios web restringidos {#restricted-sites}

Estos sitios web solo están disponibles para los clientes. Si es un cliente y necesita obtener acceso, póngase en contacto con su administrador de cuentas de Adobe.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/)
* [Contacto con el servicio de atención al cliente de Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página de producto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentación de 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es)
>* [Suscripción a las actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html)

