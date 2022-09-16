---
title: Notas de la versión para [!DNL Adobe Experience Manager] 6,5
description: Busque información sobre la versión, novedades, procedimientos de instalación y una lista detallada de cambios para [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 48f898a774d2ddd6d2c31f6a4107c71e4032cfc2
workflow-type: tm+mt
source-wordcount: '3281'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager] 6.5 Últimas notas de la versión de Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.14.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versión de Service Pack |
| Fecha | 25 de agosto de 2022 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## ¿Qué incluye [!DNL Experience Manager] 6.5.14.0 {#what-is-included-in-aem-6514}

[!DNL Experience Manager] 6.5.14.0 incluye nuevas funciones, mejoras clave solicitadas por el cliente, correcciones de errores y mejoras de rendimiento, estabilidad y seguridad, que se han publicado desde la disponibilidad inicial de la versión 6.5 en abril de 2019. [Instalar este Service Pack](#install) en [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6514}

* No se pueden agregar ni ver etiquetas para archivos PDF. (NPR-38452)
* Cuando configura los recursos conectados, guarda la configuración, vuelve a abrir la página de configuración y prueba la configuración ya guardada, la conexión de prueba falla. (NPR-38507)
* No se pueden agregar usuarios con ID de usuario numérico a las colecciones. (NPR-38538)
* Experience Manager no procesa el FFmpeg instalado en la instancia de autor. (NPR-38568)
* El procesamiento del PDF falla con un `NoClassDefFoundError` mensaje de error. (NPR-38741)
* El botón Agregar de Columnas personalizadas no se muestra correctamente al crear un informe de recursos para `de_DE` configuración regional. (ASSETS-10641)
* Cuando se carga un recurso duplicado en el repositorio y el Experience Manager de Digital Asset Management detecta y proporciona una opción para eliminarlo, el recurso original también se elimina del repositorio. (ASSETS-10826)
* Experience Manager no guarda correctamente los metadatos de la carpeta cuando especifica caracteres especiales en varios campos. (ASSETS-10721)
* No se pueden guardar las propiedades del recurso hasta que haga clic en **[!UICONTROL Guardar y cerrar]** dos veces. (ASSETS-12040)
* El lector de pantalla solo anuncia el `Relate` botón. Sin embargo, la variable `Relate` también contiene un submenú y se puede expandir y contraer. (ASSETS-6938)
* Atributos ARIA requeridos (Aplicaciones de Internet enriquecidas accesibles) `aria-expanded` para `role="combo box"` falta. (ASSETS-6928)
* En la vista de tarjeta, en el área de navegación principal del archivo, el contenido del texto **[!UICONTROL Ordenar por]** no tiene al menos una relación de contraste de 4,5:1 con respecto a su color de fondo. (ASSETS-6926)
* El Experience Manager no identifica **[!UICONTROL Seleccionar un modelo de flujo de trabajo]** lista desplegable como campo obligatorio al crear un modelo de flujo de trabajo. (ASSETS-6871)

>[!NOTE]
>
>Los servicios de contenido inteligente no estarán disponibles para los nuevos clientes locales de Experience Manager Assets a partir del 1 de septiembre de 2022. No afecta a los clientes locales y de Adobe Managed Services existentes que ya tienen habilitada esta capacidad.

### [!DNL Dynamic Media] {#dynamic-media-6514}

* Añada compatibilidad con el restablecimiento de contraseña para el usuario de Dynamic Media Classic en el Experience Manager. (ASSETS-10298)
* Los recortes inteligentes generados para las imágenes con fondo transparente tienen fondo blanco. (ASSETS-13148)
* Dynamic Media no genera miniaturas para los archivos EPS. (ASSETS-10959)
* Los recursos no se cargan en la cuenta de Dynamic Media debido a la falta de un parámetro de carga. (ASSETS-13165)
* Permita que los recursos con nombres buenos a 127 caracteres se carguen en Dynamic Media. (ASSETS-9991)
* Habilitación de JavaScript ES6 (ECMAScript 6) para visores de Dynamic Media en Experience Manager 6.5.14.0. (NPR-38393)
* Configuración de las opciones en Dynamic Media **[!UICONTROL Configuración general]** y **[!UICONTROL Configuración de publicación]** no deben ser accesibles para los usuarios que no sean administradores. (ASSETS-8628)
* Dynamic Media **[!UICONTROL Configuración general]** no muestra correctamente los parámetros de carga ya configurados. (ASSETS-10245)
* La interfaz de usuario del Experience Manager no muestra ningún mensaje de error en caso de que falle la creación/actualización del conjunto. (ASSETS-10264)
* No se puede aplicar una directiva guardada a uno de los contenedores de una plantilla editable para permitirle agregar componentes de Dynamic Media. (ASSETS-11044)
* Los recursos no se cargan en la cuenta de Dynamic Media después de ejecutar el flujo de trabajo de Recursos de reprocesamiento de Dynamic Media en recursos con un manejo de trabajo incorrecto. (ASSETS-12084, ASSETS-9877)
* Los usuarios del lector de pantalla se ven afectados por el `title` no se proporciona para `<frame>` y `<iframe>` en el **[!UICONTROL Escriba para buscar]** para abrir el Navegador. (ASSETS-5483)
* En los lectores de pantalla, relacionados y significativos `alt=` debe proporcionarse para varias imágenes presentes en **[!UICONTROL Recursos]** en el panel izquierdo. (ASSETS-5644)
* El lector de pantalla no lee **[!UICONTROL Silenciar]** y **[!UICONTROL Anular silenciar]** en vídeo utilizando el componente Dynamic Media. (ASSETS-10169)

## Comercio {#commerce-6514}

* Los productos de comercio no se ordenan mediante el encabezado de columna y está utilizando _remote_ modo de ordenación; en su lugar, los productos de comercio deben ordenarse mediante encabezados de columna con _local_ modo de ordenación. (CQ-4343750, NPR-38498)



## [!DNL Forms] {#forms-6514}

<!--

>[!NOTE]
>
> Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

>[!NOTE]
>
>* [!DNL Experience Manager Forms] releases the add-on packages one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages will release Thursday, September 1, 2022. In addition, a list of Forms fixes and enhancements will also be added to this section.

-->

* Cuando se adjunta un archivo a un formulario adaptable de varios paneles y se guarda un borrador del formulario adaptable, se produce un error. (NPR-38978)
* Cuando un usuario convierte un perfil de RGB a un perfil CMYK mediante la API de Java createPDF2 con la configuración de AdobePDF, la opción no funciona con la API de Java. La opción funciona bien con la aplicación independiente DistillerClient. (NPR-38858, CQ-4346181)
* Después de instalar AEM 6.5 Forms service pack 12 (6.5.12.0), todas las opciones excepto cerrar la tarea dejarán de estar disponibles en el paso Asignar tarea de AEM Flujos de trabajo. (NPR-38743)
* En un documento de registro (DoR), algunos valores de una tabla se truncan. (NPR-38657)
* Al obtener una vista previa de FormSet con Data XML, cuando el XDP contiene un campo flotante, al obtener una vista previa de un FormSet, no se muestran datos, pero se muestran datos cuando se utiliza la opción PDF de vista previa.
* En Forms adaptable, el botón de opción y la casilla de verificación no están en orden de tabulación. (NPR-38645)
* Al usar la variable `Summary Step` para generar el documento de registro (DoR) para un formulario adaptable traducido después del envío, no se traduce al idioma localizado. (NPR-38567)
* La opción Deshabilitar reintento en AEM pasos del flujo de trabajo no funciona como se espera. El problema aparece de forma intermitente. (NPR-38547)
* Cuando el formulario adaptable se envía con el campo de texto enriquecido, la variable `an Internal Error while Submitting a Form` se produce. Cuando el usuario se centra en el campo de texto enriquecido, antes del envío del formulario, el error no se produce. (NPR-38542)
* Un error `sling-default-3-AdobeSignRefreshTokenScheduleJob com.adobe.forms.foundation.oauth.model.OAuthConfigSlingModel Refresh Token not present for: /conf/gws-eform/cashlite/settings/cloudconfigs/fdm/cashlite/jcr:content occurs` se registra. (NPR-38541)
* Cuando un usuario carga un PDF en un formulario adaptable, el servidor de AEM Forms deja de responder. (NPR-38398)
* En un AEM Forms en un servidor OSGi, cuando se utiliza la API del servicio de documentos para certificar el PDF, se produce un error: com.adobe.fd.signatures.truststore.errors.exception.CredentialRetrievalException: AEM-DSS-311. (CQ-4346252)
* Al presentar los proyectos de carta, la variable `Could not upload asset from xml input` se produce un error. No afecta a la funcionalidad. Una vez abierto un borrador, la carta se representa correctamente. (CQ-4345979, CQ-4344418)
* Cuando se introduce una fecha en formato alemán y la variable `Preview with Data` se utiliza para una carta, el campo Fecha no se representa. (CQ-4345783)
* Al crear un portal web y generar los códigos de barras basados en datos, algunos códigos de barras no se descodifican correctamente. (CQ-4345743)
* La conversión postscript al PDF no procesa el documento de salida con los colores esperados. (CQ-4345074)
* La resolución de recursos provoca errores de envío intermitentes y hace que el mismo seguimiento de pila aparezca varias veces para un único envío. (CQ-4344764)
* Los usuarios no pueden abrir los borradores modificados que usan la variable `cmDataUrl` parámetro. Los borradores se abren bien por primera vez. Los problemas empiezan a aparecer en los intentos posteriores. (CQ-4344418)
* Cuando el usuario introduce la variable `&` en una Comunicación interactiva (IC), el borrador de la IC correspondiente no se carga. (CQ-4343969)
* Cuando se utilizan opciones de estilo en AEM Forms Designer para generar archivos PCL, el estilo especificado no se aplica a los archivos generados. (CQ-4339573)
* Cuando el recuento de páginas es superior a 15, la conversión automatizada de formularios XDP dinámicos a formularios adaptables falla. Esto funciona bien cuando el recuento de páginas es inferior a 15. (NPR-35337)
* Cuando se utiliza la opción Agregar a favoritos, no indica el estado del conmutador al lector de pantalla. (NPR-37137)
* En el Modelo de datos de formulario, los valores después del decimal en el Modelo de datos de formulario respaldado por la base de datos se truncan para el dinero y el tipo de datos de dinero pequeño. . (CQDOC-19509)
* Cuando se selecciona un vínculo de navegación para un flujo de trabajo en HTML Workspace, no se indica que el vínculo de navegación esté seleccionado. (NPR-37138)
* La función de firma de guiones no es compatible con las directrices de accesibilidad. (NPR-37596)
* AEM Forms utiliza log4j 1.x. La compatibilidad con log4j 1.x ha llegado al final de su vida útil. (NPR-38273)
* Cuando se utiliza la base de datos MSSQL como origen de datos en un Modelo de datos de formulario y se recuperan valores, se truncan los números después del decimal en los valores recuperados. (CQ-4346190)
* En Forms 6.5 Designer, cuando se abre un formulario creado con Forms 6.1 Designer y se edita un cuadro de texto, el espaciado entre párrafos supera el espacio especificado. Se eliminan todas las configuraciones anteriores al espacio y se requiere el cambio de formato manual del cuadro de texto. (CQ-4341899)
* Se muestra un valor incorrecto para el código de barras SSCC-18. Los servidores de Forms omiten el valor en la parte derecha del código de barras. (CQ-4342400)
* Para los PDF forms estáticos creados con Forms 6.5 Designer, la accesibilidad del PDF falla con un error `Tab order entry in page with annotations not set to "S"`. (CQ-4343117)
* Se ha agregado la capacidad de especificar texto de Reader de pantalla para hipervínculos en Forms Designer.(NPR-36221)
* Cuando se agrega un panel repetible a un formulario adaptable que no es XFA y el recuento de los paneles repetibles en un formulario que no es XFA es superior a 15 segundos, agregar una nueva instancia puede tardar hasta 7-8 segundos. (NPR-37346)

## Integraciones {#integrations-6514}

* Habilite la compatibilidad de compilación de JavaScript ES6 (modo ECMAScript6 o superior) para la minimización de la variable `/libs/cq/analytics/widgets.js` biblioteca. (NPR-38433)
* Habilite la compatibilidad de compilación de JavaScript ES6 (modo ESMAScript6 o superior) para la minimización de la variable `/libs/cq/testandtarget/clientlibs/testandtarget/util.js` biblioteca. (NPR-38435)
* Cuantos más contenidos haya en `/content/campaigns`, mientras más larga sea la llamada a `targeteditor.html` (`/libs/cq/personalization/touch-ui/content/targeteditor.html`) se produce cuando se abre el Editor de páginas. (NPR-38663)

## Plataforma {#platform-6514}

* No se puede iniciar sesión en el Administrador de paquetes para implementar actualizaciones. (NPR-38646)
* En la interfaz de usuario del selector de etiquetas de recursos, las etiquetas aparecen en el orden en que se crearon. Sin embargo, cuando hay muchas etiquetas, es difícil ver y administrar las etiquetas porque no se pueden ordenar. (CQ-4344279)
* Cree una notificación en la interfaz de usuario cuando un usuario esté suplantado por un administrador o cualquier otra persona que utilice el **[!UICONTROL Suplantar como]** campo . (CQ-4345288)
* En una colección inteligente, todos los recursos se mostraban al filtrar con una búsqueda guardada. (CQ-4345326)
* Se muestra un recuento incorrecto de recursos seleccionados para **[!UICONTROL Agregar a colección]** when **[!UICONTROL Seleccionar todo]** está seleccionado. (CQ-4345424)
* Se produjo un mensaje de excepción al usar la variable **[!UICONTROL Suplantar como]** con un grupo o un usuario inexistente. (CQ-4346098)

## [!DNL Sites] {#sites-6514}

* Se produjeron eliminaciones de ruta inesperadas al actualizar el Experience Manager de 6.5.12.0 a 6.5.13.0. (NPR-38532)

### Accesibilidad {#access-6514}

* En Experience Manager Sites, al expandir el **[!UICONTROL Cambiar el formato de visualización y ajustar la configuración de visualización]** y, a continuación, seleccione **[!UICONTROL Vista de lista]**, el **[!UICONTROL Arrastrar y soltar]** falta un nombre accesible. (SITES-2863, NPR-38760)
* El lector de pantalla debe anunciar el nombre accesible como `Show description for Archive` o `Show description for mini shopping cart`. Sin embargo, el nombre accesible actual se anuncia como `Info Circle button show description` para _all_ los botones de información sobre herramientas. (SITES-3104)
* Mejore el deshacer de los componentes que no tienen la función inlineEditing o dropTarget en `cq:editConfig`. (NPR-38361) <!-- version 2 (old) of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* La lista desplegable Sistema de estilos puede haberse colocado en la parte superior de la página en lugar de en el contexto del componente, para los componentes que utilizan `cq:editConfig` &quot;después de editar: REFRESH_PAGE&quot;. (NPR-38384) <!-- version 2 (old) of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig "afteredit: REFRESH_PAGE". (NPR-38384) -->
* El componente de texto está desalineado cuando se agrega a los contenedores de diseño anidados. (NPR-38193)
* Se mostraba una ficha de estilo vacía cuando no había ninguna configuración del sistema de estilos para un componente. La pestaña ahora está oculta cuando no hay ninguna configuración presente. (NPR-38218) <!-- version 2 (old) of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* La propiedad `useLegacyResponsiveBehaviour` solo funciona cuando se autentica. (NPR-37996)

### [!DNL Content Fragments] {#sites-contentfragments-6514}

* Problema de validación del campo de enumeración de fragmentos de contenido la primera vez que se carga el fragmento de contenido. (SITES-7140)
* Debe añadir campos de personalización de Campaign en el Editor de texto enriquecido del editor de fragmentos de contenido. (NPR-38526)
* Al crear o editar un nuevo fragmento de contenido en el editor de fragmentos de contenido, mediante Dispatcher, el modelo de fragmento de contenido no se guarda. Además, el editor de fragmentos de contenido no se cierra y se muestra un error en el registro del explorador. (NPR-38691)
* Error de validación de consulta persistente. (NPR-38523)
* En el cuadro de diálogo Fragmento de contenido, en **[!UICONTROL Propiedades]**, el **[!UICONTROL Fragmento de contenido]** no conserva la ruta guardada en la ventana emergente de selección. (NPR-38632)
* Cuando crea un modelo de fragmento de contenido y agrega un campo de enumeración del tipo desplegable, la validación correcta para _`is required`_falla. (NPR-38237)

### Componentes principales  {#sites-corecomponents-6514}

* El nuevo componente Correo electrónico de página no debería forzarle a la interfaz de usuario clásica durante la edición `/etc`. (NPR-38648)

### Editor de página {#sites-pageeditor-6514}

* El usuario no puede cambiar el tamaño del componente según el número deseado de columnas. (NPR-38688)

### Editor de plantillas {#sites-templateeditor-6514}

* Falta **[!UICONTROL Eliminar]** y **[!UICONTROL Cortar]** botones de la barra de menús de una plantilla editable después de una `cq:actions` se personalizó. (NPR-38521)
* Si un componente incluye otro componente, no es posible eliminarlo dentro de la estructura de la plantilla porque la variable **[!UICONTROL Eliminar]** falta en la barra de menús. (NPR-38585)

## Sling {#sling-6514}

* Se experimentó un aumento en el número de archivos abiertos en producción debido a una fuga de memoria en el módulo `DiscoveryLiteDescriptor` en `org.apache.sling.discovery.commons`, versión 1.0.20. (NPR-38288)
* En Experience Manager, de **[!UICONTROL Operaciones]** > **[!UICONTROL Diagnóstico]**, se produce un error al seleccionar **[!UICONTROL ZIP de estado de descarga]** > **[!UICONTROL Descargar]**. (NPR-38514)

## Proyectos de traducción {#translation-6514}

* El lanzamiento de subpáginas que se agregaron como referencia en una página principal no se promocionaba cuando la variable `isDeep` se ha definido como `false`. (NPR-38531)

## Interfaz de usuario {#ui-6514}

* Al usar **[!UICONTROL Seleccionar todo]** > **[!UICONTROL Publicación rápida]**, el Experience Manager no estaba publicando todos los recursos ni mostrando la cantidad de recursos que se publicarían en **[!UICONTROL Tarjeta]** ver o **[!UICONTROL Lista]** vista. (NPR-38546)
* Se muestra un recuento incorrecto de activos seleccionados para **[!UICONTROL Agregar a colección]** en **[!UICONTROL Seleccionar todo]** caso. (NPR-38633)
* Los usuarios deshabilitados se pueden seguir agregando a Colecciones y proyectos. (NPR-38651)
* Al eliminar un filtro sin guardar el formulario de búsqueda, se crea un error. (NPR-38698)
* La sesión de un usuario no puede obtener una `ModifiableValueMap` para los grupos con el fin de establecer la pertenencia directa al grupo. (NPR-38710)

## Flujo de trabajo {#workflow-6514}

* Habilite la compatibilidad de compilación de JavaScript ES6 (modo ESMAScript6 o superior) para la minimización de la variable `/libs/cq/inbox/gui/components/inbox/clientlibs/commons.js` biblioteca. (NPR-38304)
* Una vez que se ejecuta el flujo de trabajo y se completan los pasos del proceso, el mismo comentario se repite varias veces. (NPR-38364)

## Instalar [!DNL Experience Manager] 6.5.14.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.14.0 requiere [!DNL Experience Manager] 6.5. Véase [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas. <!-- UPDATE FOR EACH NEW RELEASE -->
* La descarga del Service Pack está disponible en Adobe [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html).
* En una implementación con MongoDB y varias instancias, instale [!DNL Experience Manager] 6.5.14.0 en una de las instancias de autor que utiliza el Administrador de paquetes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!NOTE]
>
>El Adobe no recomienda quitar o desinstalar el [!DNL Experience Manager] Paquete 6.5.14.0. <!-- UPDATE FOR EACH NEW RELEASE -->

### Instale el Service Pack en [!DNL Experience Manager] 6,5 {#install-service-pack}

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (cuando la instancia se actualizó desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de la instalación, tome una instantánea o una copia de seguridad nueva de su [!DNL Experience Manager] instancia.

1. Descargue el Service Pack desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra el Administrador de paquetes y, a continuación, seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y, a continuación, seleccione **[!UICONTROL Instalar]**.

1. Para actualizar el conector S3, detenga la instancia después de instalar el Service Pack, sustituya el conector existente por un nuevo archivo binario proporcionado en la carpeta de instalación y reinicie la instancia. Consulte [Almacenamiento de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo en la interfaz de usuario del Administrador de paquetes a veces se cierra durante la instalación del Service Pack. Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete de actualización antes de asegurarse de que las instalaciones se realizan correctamente. Normalmente, este problema ocurre en [!DNL Safari] pero puede ocurrir de forma intermitente en cualquier explorador.

**Instalación automática**

Hay dos métodos diferentes que puede utilizar para instalar automáticamente [!DNL Experience Manager] 6.5.14.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en `../crx-quickstart/install` cuando el servidor esté disponible en línea. El paquete se instala automáticamente.
* Utilice la variable [API HTTP del Administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Uso `cmd=install&recursive=true` para que se instalen los paquetes anidados.

>[!NOTE]
>
>El Experience Manager 6.5.14.0 no admite la instalación del Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar la instalación**

Para saber cuáles son las plataformas certificadas para funcionar con esta versión, consulte la [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.14.0)` under [!UICONTROL Productos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos los paquetes OSGi son: **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web: `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.12 o posterior (utilice la consola web: `/system/console/bundles`). <!-- NPR-38747 -->

### Instalar [!DNL Experience Manager] Paquete de complementos de Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Omitir si no utiliza [!DNL Experience Manager] Forms.

<!-- 

Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

-->

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

UberJar para [!DNL Experience Manager] La versión 6.5.13.0 está disponible en la [Repositorio de Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>En Experience Manager 6.5.14.0, tenga en cuenta que la versión de UberJar (6.5.13.0) sigue siendo la misma que la versión anterior.

Para usar UberJar en un proyecto de Maven, consulte [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

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
| Integraciones | La variable **[!UICONTROL Inclusión de AEM Cloud Services]** ya que la función [!DNL Experience Manager] y [!DNL Adobe Target] la integración se actualiza en [!DNL Experience Manager] 6.5. La integración es compatible con la API de Adobe Target Standard. La API utiliza la autenticación mediante Adobe IMS y [!DNL Adobe I/O Runtime]. Apoya el creciente papel de Adobe Launch como instrumento [!DNL Experience Manager] páginas para analytics y personalización, el asistente de inclusión es funcionalmente irrelevante. | Configure las conexiones del sistema, la autenticación IMS de Adobe y [!DNL Adobe I/O Runtime] integraciones a través de las [!DNL Experience Manager] servicios en la nube. |
| Conectores | El conector JCR de Adobe para Microsoft® SharePoint 2010 y Microsoft® SharePoint 2013 está obsoleto para [!DNL Experience Manager] 6.5. | N/D |

## Problemas conocidos {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

* [AEM fragmento de contenido con el paquete de índice 1.0.5 de GraphQL](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip)
Este paquete es necesario para los clientes que utilizan GraphQL; esto les permite añadir la definición de índice necesaria en función de las funciones que realmente utilizan.

* Como [!DNL Microsoft® Windows Server 2019] no es compatible [!DNL MySQL 5.7] y [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] no admite instalaciones llave en mano para [!DNL AEM Forms 6.5.10.0].

* Si actualiza su [!DNL Experience Manager] de la versión 6.5 a la versión 6.5.10.0, puede ver `RRD4JReporter` las excepciones de `error.log` archivo. Para resolver el problema, reinicie la instancia.

* Si instala [!DNL Experience Manager] 6.5 Service Pack 10 o un Service Pack anterior en [!DNL Experience Manager] 6.5, la copia en tiempo de ejecución del modelo de flujo de trabajo personalizado de recursos (creado en `/var/workflow/models/dam`).
Para recuperar la copia de tiempo de ejecución, Adobe recomienda sincronizar la copia en tiempo de diseño del modelo de flujo de trabajo personalizado con su copia de tiempo de ejecución mediante la API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Los usuarios pueden cambiar el nombre de una carpeta de una jerarquía [!DNL Assets] y publicar una carpeta anidada en [!DNL Brand Portal]. Sin embargo, el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Cuando un usuario selecciona configurar un campo por primera vez en un formulario adaptable, la opción para guardar una configuración no se muestra en el Explorador de propiedades. Si se selecciona para configurar otro campo del formulario adaptable en el mismo editor, se resuelve el problema.

* Durante la instalación de [!DNL Experience Manager] 6.5.x.x:
   * &quot;Cuando la integración de Adobe Target está configurada en [!DNL Experience Manager] con la API de Target Standard (autenticación IMS) y luego exportar fragmentos de experiencia a Target se crean tipos de oferta incorrectos. En lugar de escribir &quot;Fragmento de experiencia&quot;/origen &quot;Adobe Experience Manager&quot;, Target crea varias ofertas con el tipo &quot;HTML&quot;/origen &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La validación del lado del servidor del formulario adaptable falla cuando se utilizan funciones agregadas como SUM, MAX y MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La zona interactiva de una imagen interactiva de Dynamic Media no está visible al previsualizar el recurso mediante el visor de banners de ventas.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tiempo de espera de que el cambio del registro se complete sin registrar.

* Al intentar mover, eliminar o publicar fragmentos de contenido o sitios o páginas, hay un problema cuando se recuperan referencias de fragmentos de contenido, ya que la consulta en segundo plano falla; es decir, la funcionalidad no funciona.
Para garantizar la operación correcta, debe añadir las siguientes propiedades al nodo de definición de índice `/oak:index/damAssetLucene` (no se requiere reindexación):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## Paquetes de contenido y paquetes OSGi incluidos {#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en [!DNL Experience Manager] 6.5.14.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.14.0](/help/release-notes/assets/65140_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.14.0](/help/release-notes/assets/65140_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sitios web restringidos {#restricted-sites}

Estos sitios web solo están disponibles para los clientes. Si es un cliente y necesita obtener acceso, póngase en contacto con su administrador de cuentas de Adobe.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/)
* [Contacto con el servicio de atención al cliente de Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página de producto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentación de 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es)
>* [Suscripción a las actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html)

