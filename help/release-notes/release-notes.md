---
title: Notas de la versión para [!DNL Adobe Experience Manager] 6,5
description: Busque información sobre la versión, novedades, procedimientos de instalación y una lista detallada de cambios para [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
source-git-commit: 3430897fc98aecbcf6cc7bf6bdc9b3df24e92366
workflow-type: tm+mt
source-wordcount: '2986'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] 6.5 Últimas notas de la versión de Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=WRAZ43&nav=MTVfezk2OTJDQTNFLUI4QTQtNDY2RS05NEVCLUQ5QjcyNEVENkJDNn0 -->

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.16.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versión de Service Pack |
| Fecha | Jueves, 23 de febrero de 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]be/packages/cq650/servicepack/aem-service-pkg-6.5.16.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## ¿Qué incluye [!DNL Experience Manager] 6.5.16.0 {#what-is-included-in-aem-6516}

[!DNL Experience Manager] 6.5.16.0 incluye nuevas funciones, mejoras clave solicitadas por el cliente, correcciones de errores y mejoras de rendimiento, estabilidad y seguridad, que se han publicado desde la disponibilidad inicial de la versión 6.5 en abril de 2019. [Instalar este Service Pack](#install) en [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Una mejora clave en Dynamic Media es la siguiente:

Nuevo protocolo DASH (Dynamic Adaptive Streaming over HTTP) compatible con la transmisión de velocidad de bits adaptable en el envío de vídeo de Dynamic Media (con CMAF) [Formato de aplicación de medios común] activada).

* La transmisión adaptativa (DASH/HLS) garantiza una mejor experiencia de visualización de vídeos por parte del usuario final.
* DASH es el protocolo estándar internacional para la transmisión de vídeo adaptable y es ampliamente adoptado en el sector.
* Disponible ahora en Asia-Pacífico y América del Norte (se habilitará mediante un ticket de soporte); próximamente en Europa, Oriente Medio y África.

Consulte [Habilitar DASH en su cuenta](/help/assets/video.md#enable-dash).

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6516}

* Recursos conectados: Cuando activa las opciones de recorte inteligente para imágenes en DAM remoto, carga imágenes en una carpeta y sincroniza la carpeta con sitios locales, la carpeta no se abre en la implementación local de Sites. (NPR-39912)
* Al ordenar una colección por su nombre, la vista de lista no funciona correctamente (ASSETS-19401)
* Cuando se carga un archivo multimedia grande (JPEG) en Colecciones, el Experience Manager deja de responder. (ASSETS-19387)
* En el panel del árbol de contenido, el nombre del recurso mostrado es incorrecto, ya que la ubicación del recurso no se representa correctamente. (ASSETS-18870)
* Al compartir una colección mediante un vínculo, los datos de la dirección URL no coinciden entre la barrido de la vista de tarjeta y la vista de lista. (ASSETS-18758)
* Cuando se realiza una búsqueda de contenido mediante un filtro en el tipo de carpeta, los resultados de la búsqueda son incoherentes. (ASSETS-18227)
* La variable `dam:size` no se actualiza después de XMP reescritura, lo que hace que se devuelva información incorrecta del `/platform/path/to/asset.jpg;resource=metadata` API. (ASSETS-17631)
* Resolución de recursos sin cerrar en todas las instancias de Experience Manager. (ASSETS-16904)
* No se puede crear una versión para un recurso aunque tenga asignado el `create` y `modify` permisos. (ASSETS-15956)
* La variable `move` se desactiva aleatoriamente al mover un recurso de un punto a otro. (ASSETS-14889)
* Los lectores de pantalla no pueden identificar encabezados, ya que el texto no se define dentro de las etiquetas de encabezado sino como texto general. (ASSETS-6924)
* El texto alternativo de la imagen no es obligatorio, pero el texto mostrado debajo de la imagen es repetitivo con un `Type` atributo. (ASSETS-6915)


## [!DNL Assets] - [!DNL Dynamic Media] {#dm-6516}

* El elemento de formulario no contiene una etiqueta. Con lectores de pantalla como NVDA y JAWS, la información de la etiqueta del formulario no se anuncia correctamente. (CQ-4344078)
* Los desplegables no se cierran cuando el `Escape` se utiliza en un teclado. (CQ-4344077)
* El icono Información (la letra &quot;i&quot;) que aparece para la sugerencia de error en línea después de proporcionar una entrada no válida, no es accesible mediante un teclado. (CQ-4344076)
* `getManifestURI` devuelve nulo debido a que una propiedad JCR se está leyendo como `toString` en lugar de `getString`. (ASSETS-18674)
* El componente de vídeo SmartCrop no se está comportando correctamente. El componente está llevando a cabo la reproducción en lugar de la transmisión, y las llamadas VTT están fallando, lo que provoca un error 404. (ASSETS-18468)
* Selección **[!UICONTROL Propiedades]** en la página Visualizador de un recurso, se produce una excepción de puntero nulo. (ASSETS-18420)
* [!DNL Experience Manager] cambios en la interfaz de usuario para el flujo continuo DASH que incluyen lo siguiente:
   * tener un campo CMAF visible (Common Media Application Format) en el editor de perfiles de vídeo.
   * hacer que el proceso de carga de vídeo envíe un indicador de CMAF.
   * las opciones **[!UICONTROL auto]**, **[!UICONTROL hls]** y **[!UICONTROL guión]** ya están disponibles en la lista desplegable de reproducción del editor de ajustes preestablecidos de visor **[!UICONTROL Comportamiento]** pestaña .
(ASSETS-17428)
* En Navegación, al seleccionar **[!UICONTROL Recursos]** > **[!UICONTROL Archivos]** > **[!UICONTROL Crear]** > **[!UICONTROL Conjunto de carrusel]**, el icono de imagen se superpone con la cadena de texto &quot;Diapositiva 1&quot;. (ASSETS-18578)
* Los recursos no publicados se vuelven a publicar. (ASSETS-16428)
* Experience Manager Author se desactiva debido a un problema de carga que solicita la creación de una alerta sintética. (ASSETS-15937)
* En la página Configuración general de Dynamic Media , aparece un mensaje de error sin traducir `Failed to fetch data` aparece. (ASSETS-15617)

## [!DNL Forms] {#forms-6516}

### [!DNL Forms] Características principales {#forms-features-6516}

* [Forms adaptable sin objetivos](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) permite a los desarrolladores crear, publicar y administrar formularios interactivos a los que se puede acceder e interactuar con ellos mediante API, en lugar de a través de una interfaz gráfica de usuario tradicional.

* [Componentes principales adaptables de Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es#features) son un conjunto de 24 componentes de código abierto compatibles con BEM que se basan en los componentes principales de WCM de Adobe Experience Manager. Estos componentes son de código abierto y permiten a los desarrolladores personalizar y ampliar fácilmente estos componentes para adaptarlos a las necesidades específicas de su organización. Cualquiera con habilidades existentes para personalizar [Componentes principales de WCM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html?lang=en) puede personalizar y aplicar estilo fácilmente a estos componentes.

* El servicio de extensión de Reader en OSGi ahora proporciona opciones independientes para habilitar los derechos de uso de importación y exportación en un PDF para importar o exportar datos en Adobe Acrobat Reader. (NPR-39909)

### [!DNL Forms] Correcciones {#forms-fixes-6516}

* Al usar un **Asignar tarea** para enviar una notificación para una tarea asignada, se envían dos correos electrónicos en lugar de uno al individuo asignado. (NPR-40078)
* Cuando un usuario oculta los encabezados de tabla, anula la configuración del ancho de columna establecido anteriormente y todas las columnas mantienen el mismo ancho. (NPR-40063)
* En caso de cambiar la contraseña predeterminada del usuario administrador de `admin`, mientras realiza la `Prepare Adobe Experience Manager Server For DSC deployment` compruebe el paquete de servicio JEE de AEM Forms que falla. (NPR-40062), (NPR-39387)
* Las API de OutputService y AssemblerService no pueden convertir el formulario de PDF a PDF/A. (NPR-39990)
* El servicio del ensamblador no puede convertir el PDF a PDF/A. Cuando un usuario convierte un PDF en PDF/A, se produce el siguiente error: `PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Summary" ignoreUnusedResources="true" allowCertificationSignatures="true"> <Violation count="6" key="PDFA_CS_001_NOT_DEVICE_INDEPENDENT" description="ColorSpace is not device independent`. (NPR-39956)
* Cuando falla la validación del lado del servidor para una llamada a la API GuideSubmitServlet, los errores no se devuelven en la respuesta enviada al cliente. (NPR-39925)
* Después de actualizar a AEM 6.5.15.0 Service Pack en el servidor Windows, el usuario encuentra varios mensajes de error y el servicio de correo electrónico no funciona.(NPR-39919)
* Al actualizar a AEM 6.5.14.0 y utilizar el servicio importData para combinar PDF con XML, se produce el siguiente error: `Caused by: java.lang.NoSuchMethodError: com.adobe.xfa.form.FormModel.isXFABarcode(Lcom/adobe/xfa/Node;)Ljava/lang/Boolean`.(NPR-39807)
* Cuando el usuario instala **Oficina de seguridad de documentos** , se producen los siguientes problemas:
   * Microsoft® Excel se bloquea con frecuencia.
   * Al abrir un documento protegido, la variable **Oficina de seguridad de documentos** no se detecta como instalada en un equipo. Indica al usuario que descargue e instale la extensión de seguridad. (NPR-39768)
* Después de que un usuario actualice a AEM Service Pack 6.5.15.0, la conversión de PostScript a Pdf no funciona. (NPR-39765), (NPR-39764)
* Cuando el usuario intenta abrir la pantalla de presentación después de abrir un formulario adaptable, falla con una excepción NullPointer :`[172.17.0.1[1662032923933]GET/libs/fd/af/content/editors/form/tour/content.htmlHTTP/1.1]com.day.cq.wcm.core.impl.WCMDebugFilterException:org.apache.sling.api.scripting.ScriptEvaluationException:"` (NPR-39654)
* En Windows, cuando el usuario habilita la configuración en negro de alto contraste, el contenido de Forms de HTML5 no queda claro cuando se representa como una vista previa de HTML en el explorador. (NPR-39018)
* Cuando el usuario intenta agregar metadatos, el botón Guardar deja de ser funcional para los componentes Borrador y Envío.(CQ-4349601)
* Después de actualizar a AEM 6.5.15.0 Service Pack, la redirección de las URL relativas ya no funciona en el Editor visual. (NPR-39947)
* Cuando un usuario actualiza a AEM 6.5.15.0 Service Pack, la redirección deja de funcionar con Internet Explorer. (CQ-4351745)
* Después de que un usuario actualice a AEM 6.5.15.0 Service Pack, no se reconoce la etiqueta de encabezado del HTML. El código de HTML de la etiqueta de encabezado se muestra como texto en el formulario de HTML. (NPR-39915)
* Cuando el usuario intenta enviar un formulario adaptable, se produce un error tipast: `ERROR [10.207.64.167 [1668589530607] POST /app/LS4/content/forms/af/revalidate/jcr:content/guideContainer.af.submit.jsp HTTP/1.1]`(NPR-39809)
* Cuando un usuario obtiene una vista previa de un documento de registro mediante la variable **Enviar correo electrónico** Enviar acción, no se muestra correctamente. La plantilla de correo se incrusta en la previsualización del documento de registro. (CQ-4352155)
* Cuando un usuario obtiene una vista previa de un formulario adaptable como HTML en un explorador Microsoft Edge con modo de compatibilidad con IE, no se muestra correctamente.(CQ-4352216)
* El diccionario debe incluir nuevas configuraciones regionales con caracteres especiales, como guiones bajos o guiones, para habilitar la traducción. (NPR-40088)

Después de instalar el paquete de servicio del complemento Forms AEM 6.5.16.0, los clientes se enfrentaban a los problemas que se enumeran a continuación. Por lo tanto, una versión actualizada de [Paquete de servicio de complementos de Forms de AEM 6.5.16.0: 6.0.914](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) está disponible. Adobe recomienda utilizar el Service Pack actualizado:
* Cuando un usuario intenta crear un formulario adaptable con un usuario del grupo de usuarios de formularios, la opción para seleccionar cualquier plantilla no está presente y se produce un error similar al siguiente: error interno del servidor: java.lang.NullPointerException en com.adobe.aem.formsndocuments.servlet.ThemeClientLibraryDataSourceServlet.lambda$getThemeClientLibCategoryList$3(ThemeClientLibraryDataServlet.java:76) en java.base/java.util.stream.ReferencePipeline$2$1.1 (ReferencePipeline.java:176) en java.base/java.util.Iterator.foreachRemaining(Iterator.java:133) (FORMS-7629)
* Los cambios realizados en las reglas del editor de código no se están guardando.(FORMS-7532)

## Integraciones {#integrations-6516}

* Eliminación del código de Search&amp;Promote de Adobe y la dependencia del Experience Manager 6.5. El Search&amp;Promote de Adobe llegó al final del servicio en septiembre de 2022. Consulte [Anuncio de fin de servicio de Search&amp;Promote de Adobe](https://experienceleague.adobe.com/docs/discontinued/using/search-promote.html?lang=en). (NPR-39706)

## [!DNL Sites] {#sites-6516}

* Actual `cq-wcm-core` la versión artificial no tiene el POM. (SITES-10983)
* La acción de vista previa de lanzamiento no debe enumerar la página que se va a crear. (SITES-10355, CQ-4266213)
* Despliegue después de que la desconexión MSM vuelva a crear la página desconectada. (SITES-9841)
* La creación de un lanzamiento está agotando el tiempo de espera; el usuario debe esperar muchos minutos en una pantalla de carga antes de que se agote el tiempo de espera de la solicitud. (SITES-9051)
* La interfaz de usuario de la página de lanzamiento muestra rutas de página principales inexistentes. Puede desplegar la página con un mensaje de éxito, pero la página secundaria no se despliega debido a que la página principal no se despliega nunca. (SITES-8621)

### [!DNL Sites] - Componentes principales {#sites-core-components-6516}

* Centralice el procesamiento de vínculos en páginas de correo electrónico para que ya no se necesiten personalizaciones de modelo. (SITES-9002)

### [!DNL Sites] - Interfaz de usuario del administrador {#sites-adminui-6516}

* La exportación a CSV no exporta todas las páginas de la página seleccionada. (SITES-9390)

### [!DNL Sites] - [!DNL Content Fragments] {#sites-contentfragments-6516}

* No se puede imprimir el JSON de un fragmento de contenido. El motivo es que la consulta de GraphQL no se puede generar al abrir la página Vista previa del fragmento de contenido. (SITES-8619)
* Al volver a abrir el Editor del modelo de fragmento de contenido, todas las **[!UICONTROL Fecha y hora]** los campos se configuran de forma predeterminada en el tipo Fecha y hora . (SITES-8401)

### [!DNL Sites] - [!DNL Experience Fragments] {#sites-experiencefragments-6516}

* No puede mover un fragmento de experiencia a otra carpeta aunque la plantilla aparezca en plantillas permitidas. (SITES-8601)
* (SITES-7989)


### [!DNL Sites] - Editor de página {#sites-pageeditor-6516}

* Actualización de dependencias para la mejora de resolución de recursos realizada en SITES-8464 en la que el procesamiento de páginas en el modo de creación creó un número elevado de `TemplatedResourceImpl` objetos. (SITES-9350)


## Sling {#sling-6516}

* El Experience Manager está bloqueado al inicio. (NPR-39832)
* Cuando hay muchas rutas mnemónicas presentes en el almacenamiento de la versión de Experience Manager, el Experience Manager no se inicia. (NPR-38955)


## Proyectos de traducción {#translation-6516}

* En `MicrosoftTranslationServiceImpl`, el parámetro de cadena de consulta `Category` es incorrecto. (NPR-39828)
* Al crear un proyecto de traducción se muestra el error *El recurso de página de formato no existe*; no se crea el proyecto de traducción. (NPR-39762)
* No se puede establecer una fecha de vencimiento en un proyecto de traducción que utiliza un conector de traducción humana. (NPR-39593)

## Interfaz de usuario {#ui-6516}

* Cuando se cambia a una resolución más pequeña, no se muestra DatePicker y la selección AM/PM no se muestra ni cambia visiblemente. (NPR-39948)
* Cuando se utiliza minify js (minimización de JavaScript), no se procesa la minificación debido a un error de análisis. (NPR-39650)
* Campo de etiqueta (`/libs/cq/gui/components/coral/common/form/tagfield`) entra en conflicto con la cronología. (CQ-4350751)


## WCM {#wcm-6516}

* La acción de vista previa de lanzamiento no debe enumerar la página que se va a crear. (CQ-4266213, SITES-10355)

## Flujo de trabajo {#workflow-6516}

* Eliminar manualmente el modelo de flujo de trabajo editable de `/conf` deja una instancia de modelo de tiempo de ejecución persistente sin un modelo editable. (CQ-4349365)


## Instalar [!DNL Experience Manager] 6.5.16.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.16.0 requiere [!DNL Experience Manager] 6.5. Véase [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas. <!-- UPDATE FOR EACH NEW RELEASE -->
* La descarga del Service Pack está disponible en Adobe [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html).
* En una implementación con MongoDB y varias instancias, instale [!DNL Experience Manager] 6.5.16.0 en una de las instancias de autor que utiliza el Administrador de paquetes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe no recomienda quitar o desinstalar el [!DNL Experience Manager] Paquete 6.5.16.0. Como tal, antes de instalar el paquete, debe crear una copia de seguridad de la variable `crx-repository` en caso de que necesite revertirla. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for AEM Forms, see [AEM Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Instale el Service Pack en [!DNL Experience Manager] 6,5 {#install-service-pack}

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (cuando la instancia se actualizó desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de la instalación, tome una instantánea o una copia de seguridad nueva de su [!DNL Experience Manager] instancia.

1. Descargue el Service Pack desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra el Administrador de paquetes y, a continuación, seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y, a continuación, seleccione **[!UICONTROL Instalar]**.

1. Para actualizar el conector S3, detenga la instancia después de instalar el Service Pack, sustituya el conector existente por un nuevo archivo binario proporcionado en la carpeta de instalación y reinicie la instancia. Consulte [Almacenamiento de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo en la interfaz de usuario del Administrador de paquetes a veces se cierra durante la instalación del Service Pack. Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete de actualización antes de asegurarse de que las instalaciones se realizan correctamente. Normalmente, este problema ocurre en [!DNL Safari] pero puede ocurrir de forma intermitente en cualquier explorador.

**Instalación automática**

Hay dos métodos diferentes que puede utilizar para instalar automáticamente [!DNL Experience Manager] 6.5.16.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en `../crx-quickstart/install` cuando el servidor esté disponible en línea. El paquete se instala automáticamente.
* Utilice la variable [API HTTP del Administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Uso `cmd=install&recursive=true` para que se instalen los paquetes anidados.

>[!NOTE]
>
>El Experience Manager 6.5.16.0 no admite la instalación del Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar la instalación**

Para saber cuáles son las plataformas certificadas para funcionar con esta versión, consulte la [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.16.0)` under [!UICONTROL Productos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos los paquetes OSGi son: **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web: `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.14 o posterior (utilice la consola web: `/system/console/bundles`). <!-- NPR-39939 for 6.5.16.0 --> <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Instalación de Service Pack para [!DNL Experience Manager] Forms {#install-aem-forms-add-on-package}

Para obtener instrucciones para instalar el Service Pack en AEM Forms, consulte [Instrucciones de instalación de AEM Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### Instalación del paquete de índice de GraphQL para fragmentos de contenido de Experience Manager {#install-aem-graphql-index-add-on-package}

Los clientes que utilicen GraphQL deben instalar la variable [AEM fragmento de contenido con el paquete de índice de GraphQL 1.0.5](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip).

Esto le permite añadir la definición de índice necesaria en función de las funciones que realmente utilizan.

Si no se instala este paquete, pueden producirse consultas de GraphQL lentas o fallidas.

>[!NOTE]
>
>Este paquete solo debe instalarse una vez por instancia; no es necesario volver a instalarlo con cada Service Pack.

### UberJar {#uber-jar}

UberJar para [!DNL Experience Manager] La versión 6.5.16.0 está disponible en la [Repositorio de Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>En el Experience Manager 6.5.16.0, la versión de UberJar (6.5.15.0) sigue siendo la misma que la versión anterior.


Para usar UberJar en un proyecto de Maven, consulte [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.15</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar y los otros artefactos relacionados están disponibles en el Repositorio Central de Maven en lugar del Repositorio de Maven Público de Adobe (`repo.adobe.com`). Se cambia el nombre del archivo UberJar principal a `uber-jar-<version>.jar`. Así que no hay `classifier`, con `apis` como valor, para la variable `dependency` etiqueta.

## Funciones en desuso {#removed-deprecated-features}

A continuación se muestra una lista de funciones y capacidades que están marcadas como obsoletas con [!DNL Experience Manager] 6.5.7.0. Las funciones se marcan como obsoletas inicialmente y después se eliminan en una versión futura. Se proporciona una opción alternativa.

Revise si utiliza una función o una capacidad en una implementación. Además, planifique cambiar la implementación para utilizar una opción alternativa.

| Área | Funcionalidad | Reemplazo |
|---|---|---|
| Integraciones | La variable **[!UICONTROL Inclusión de AEM Cloud Services]** ya que la función [!DNL Experience Manager] y [!DNL Adobe Target] la integración se actualiza en [!DNL Experience Manager] 6.5. La integración es compatible con la API de Adobe Target Standard. La API utiliza la autenticación mediante Adobe IMS y [!DNL Adobe I/O Runtime]. Apoya el creciente papel de Adobe Launch como instrumento [!DNL Experience Manager] páginas para analytics y personalización, el asistente de inclusión es funcionalmente irrelevante. | Configure las conexiones del sistema, la autenticación IMS de Adobe y [!DNL Adobe I/O Runtime] integraciones a través de las [!DNL Experience Manager] servicios en la nube. |
| Conectores | El conector JCR de Adobe para Microsoft® SharePoint 2010 y Microsoft® SharePoint 2013 está obsoleto para [!DNL Experience Manager] 6.5. | N/D |

## Problemas conocidos {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* Actualice las consultas de GraphQL que puedan haber utilizado un nombre de API personalizado para el modelo de contenido a para utilizar en su lugar el nombre predeterminado del modelo de contenido.

* Una consulta de GraphQL puede utilizar la variable `damAssetLucene` índice en lugar de `fragments` índice. Esto puede provocar que las consultas de GraphQL fallen o que tarden mucho tiempo en ejecutarse.

   Para corregir el problema, `damAssetLucene` debe configurarse para incluir las dos propiedades siguientes:

   * `contentFragment`
   * `model`

   Después de cambiar la definición del índice, se requiere una reindexación (`reindex` = `true`).

   Después de estos pasos, las consultas de GraphQL deben funcionar más rápido.

* Como [!DNL Microsoft®® Windows Server 2019] no es compatible [!DNL MySQL 5.7] y [!DNL JBoss®® EAP 7.1], [!DNL Microsoft®® Windows Server 2019] no admite instalaciones llave en mano para [!DNL AEM Forms 6.5.10.0].

* Si actualiza su [!DNL Experience Manager] de 6.5.0 a 6.5.4 al último service pack de Java™ 11, verá `RRD4JReporter` las excepciones de `error.log` archivo. Para detener las excepciones, reinicie la instancia de [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Los usuarios pueden cambiar el nombre de una carpeta de una jerarquía [!DNL Assets] y publicar una carpeta anidada en [!DNL Brand Portal]. Sin embargo, el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Cuando un usuario selecciona configurar un campo por primera vez en un formulario adaptable, la opción para guardar una configuración no se muestra en el Explorador de propiedades. Si se selecciona para configurar otro campo del formulario adaptable en el mismo editor, se resuelve el problema.

* Durante la instalación de [!DNL Experience Manager] 6.5.x.x:
   * &quot;Cuando la integración de Adobe Target está configurada en [!DNL Experience Manager] con la API de Target Standard (autenticación IMS) y luego exportar fragmentos de experiencia a Target se crean tipos de oferta incorrectos. En lugar de escribir &quot;Fragmento de experiencia&quot;/origen &quot;Adobe Experience Manager&quot;, Target crea varias ofertas con el tipo &quot;HTML&quot;/origen &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: No se encontraron ventanas de mantenimiento en granito/operaciones/mantenimiento.
   * La validación del lado del servidor del formulario adaptable falla cuando se utilizan funciones agregadas como SUM, MAX y MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - No se encontraron ventanas de mantenimiento en granito/operaciones/mantenimiento.
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

* En AEM Forms, el protocolo POP3 no funciona con los extremos de correo electrónico para Microsoft® Office 365.
* En la plataforma JBoss® 7.1.4, cuando el usuario instala AEM paquete de servicio 6.5.16.0, `adobe-livecycle-jboss.ear` la implementación falla.

## Paquetes de contenido y paquetes OSGi incluidos {#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en [!DNL Experience Manager] 6.5.16.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.16.0](/help/release-notes/assets/65160_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.16.0](/help/release-notes/assets/65160_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sitios web restringidos {#restricted-sites}

Estos sitios web solo están disponibles para los clientes. Si es cliente y necesita acceso, póngase en contacto con el administrador de cuentas de Adobe.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/)
* [Contacto con el servicio de atención al cliente de Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página de producto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentación de 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es)
>* [Suscripción a las actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html)

