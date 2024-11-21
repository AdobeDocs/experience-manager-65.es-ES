---
title: Notas de la versión para [!DNL Adobe Experience Manager] 6.5
description: Encuentra información de la versión, novedades, instrucciones de instalación y una lista detallada de cambios para  [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 9026b6777e4c3f030eae37491c823a68afe61270
workflow-type: tm+mt
source-wordcount: '5027'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager] 6.5 Últimas notas de la versión del paquete de servicio {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.22.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versión del paquete de servicio |
| Fecha | Jueves, 21 de noviembre de 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Qué se incluye en [!DNL Experience Manager] 6.5.22.0 {#what-is-included-in-aem-6522}

[!DNL Experience Manager] 6.5.22.0 incluye nuevas funciones, mejoras clave solicitadas por el cliente y correcciones de errores. También incluye mejoras de rendimiento, estabilidad y seguridad publicadas desde el lanzamiento inicial de la versión 6.5 en abril de 2019. [Instalar este Service Pack](#install) en [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Funciones principales y mejoras

Las funciones y mejoras clave de esta versión son las siguientes:

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

### Sites {#sites}

AEM [El editor universal](/help/sites-developing/universal-editor/introduction.md) ya está disponible en la versión 6.5 para casos de uso sin encabezado con la aplicación de un paquete de funciones.

### [!DNL Assets]

La pestaña IPTC ahora admite los campos de texto [!UICONTROL Texto alternativo] y [!UICONTROL Descripción extendida]. (ASSETS-34918)

### [!DNL Forms]

* **Compatibilidad con credenciales de OAuth**: Una credencial nueva y más fácil de usar para la autenticación de servidor a servidor, que reemplaza la credencial de cuenta de servicio (JWT) existente. (NPR-41994)
* [Mejoras del editor de reglas en AEM Forms](/help/forms/using/rule-editor-core-components.md):
   * Compatibilidad para implementar condiciones anidadas con la funcionalidad `When-then-else`.
   * Validar o restablecer paneles y formularios, incluidos campos.
   * Compatibilidad con funciones modernas de JavaScript, como las funciones izquierda y flecha (compatibilidad con ES10) dentro de las funciones personalizadas.
* [API de AutoTag para la accesibilidad del PDF](/help/forms/using/aem-document-services-programmatically.md#doc-utility-services-doc-utility-services): AEM Forms en OSGi ahora admite la nueva API de AutoTag para mejorar el PDF para los estándares de accesibilidad al agregar etiquetas: párrafos y listas. Hace que los PDF sean más accesibles para los usuarios con tecnología de asistencia.
* **Compatibilidad con PNG de 16 bits**: El servicio ImageToPdf de PDF Generator ahora admite la conversión de PNG con una profundidad de color de 16 bits.
* **Aplicar artefactos a bloques de texto individuales en XDP**: Forms Designer ahora permite a los usuarios establecer la configuración en bloques de texto individuales en archivos XDP. Esta capacidad permite controlar los elementos que se tratan como artefactos en los PDF resultantes. Estos elementos, como encabezados y pies de página, están disponibles para las tecnologías de asistencia. Las funciones principales incluyen marcar bloques de texto como artefactos e incrustar esta configuración en los metadatos XDP. El servicio de salida de Forms aplica esta configuración durante la generación de PDF, lo que garantiza el etiquetado adecuado de PDF/UA.
* **AEM Forms Designer está certificado con `GB18030:2022` estándar**: con la certificación `GB18030:2022`, ahora Forms Designer admite el conjunto de caracteres Unicode chino que le permite introducir caracteres chinos en todos los campos editables y cuadros de diálogo.
* El servicio PDF Generator en el servidor JEE ahora [admite WebToPDF route](/help/forms/using/admin-help/configure-service-settings.md#generate-pdf-service-settings-generate-pdf-service-settings) para convertir HTML en PDF, junto con las rutas WebKit y WebCapture sólo de Windows. Mientras que la ruta WebToPDF ya está disponible en OSGi y se amplía a JEE. Ahora, tanto en plataformas JEE como OSGi, el servicio de PDF Generator admite las siguientes rutas en diferentes sistemas operativos:
   * **Windows**: WebKit, WebCapture, WebToPDF
   * **Linux®**: WebKit, WebToPDF

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Se han corregido problemas en el Service Pack 22 {#fixed-issues}


### [!DNL Sites]{#sites-6522}


#### Accesibilidad {#sites-accessibility-6522}

* Faltaba un nombre accesible en el botón del selector de muestras de anotación. Es decir, con un lector de pantalla, no hay ningún nombre comprensible para que el botón seleccione después de introducir un nuevo valor hexadecimal. (SITES-11992)
* Los siguientes elementos del menú del carril izquierdo aparecen como una lista, pero no están marcados como tales en el lector de pantalla:

   * Sitio
   * Live Copy
   * Iniciar
   * Copia de idioma
   * Carpeta
   * Informe CSV (SITES-2874)

* AEM La Administración de contenido web principal requiere una etiqueta de accesibilidad para los hipervínculos en el Editor de texto enriquecido. Cuando se utiliza un hipervínculo en el componente de texto, la etiqueta de anclaje debe incluir el atributo `aria-label` para garantizar que los lectores de pantalla puedan leer y transmitir el texto del vínculo con precisión por motivos de accesibilidad. (SITES-11511)
* AEM En la vista de lista, los elementos interactivos del encabezado de tabla no tienen la función de &quot;botón&quot; requerida. Como tal, el lector de pantalla NVDA no anuncia las funciones de botón esperadas para los siguientes encabezados de tabla: Título, Nombre, Modificado, Publicado, Vista previa, Plantilla, Operación, Flujo de trabajo. A cada elemento interactivo del encabezado de la tabla se le debe asignar una función de &quot;botón&quot; para garantizar la compatibilidad con tecnologías de asistencia como NVDA. (SITES-10962)


#### Interfaz de usuario de administrador{#sites-adminui-6522}

* AEM En algunos casos, las funcionalidades de comparación y previsualización de versiones no funcionaban según lo esperado en varias páginas. Específicamente:

   * **Problema de vista previa:** Al intentar obtener una vista previa de la versión de una página, aparece inicialmente un error. Después de volver a intentarlo, la vista previa genera una página en blanco.
   * **Problema de comparación de versiones:** La característica &quot;Comparar con actual&quot; sólo mostraba la versión actual, sin resaltar las diferencias entre versiones. (SITES-23988)

* Aparece una etiqueta `<br>` inesperada en el campo Editor de texto enriquecido (RTE) al utilizar `defaultPasteMode` establecido en `plaintext` durante una acción de copiar y pegar. Este problema causa un marcado diferente para el mismo contenido, lo que da como resultado que el mismo contenido de texto se traduzca dos veces en la memoria de traducción de un cliente. (SITES-23606)
* AEM En la versión 6.5.20.0, se encontró un problema de funcionalidad con la característica **Administrar publicación**. Al seleccionar un nodo y programarlo para su publicación futura, podría aparecer un mensaje de error (&quot;Error al recuperar los recursos secundarios de los elementos seleccionados&quot;) al intentar incluir nodos secundarios. Este problema bloqueaba el uso de la opción **Incluir elementos secundarios**, lo que impedía la publicación completa de la jerarquía de contenido deseada. (SITES-23000)
* La marca de tiempo &quot;Publicado&quot; de una plantilla no se actualizaba en el entorno de creación, aunque la plantilla se replicara correctamente en las instancias de publicación. El comportamiento esperado era que la marca de tiempo de la instancia de autor reflejara la última publicación, pero esta actualización no se estaba produciendo según lo previsto. (SITES-21585)
* AEM Se ha producido una discrepancia en el recuento de vínculos entrantes en el entorno de creación de la. El carril izquierdo mostraba menos vínculos en comparación con la IU clásica. Además, algunos vínculos entrantes legítimos no funcionan. (SITES-24837)
* AEM Se indicaban tiempos de carga extremadamente largos al ver las versiones de la página en la vista Cronología de la vista de la página de la página de la vista de la página de la página de la página de la página de la página de la página de la página de la vista de la página de la. Se tardaba hasta 19 minutos en mostrar las versiones. AEM Este problema estaba en curso desde la actualización de la versión 6.4.8 a la versión 6.5.18 de, lo que afectó significativamente a la eficacia del flujo de trabajo. (SITES-22468 Y SITES-22467)

<!-- #### Classic UI{#sites-classicui-6522} 

* A -->


#### [!DNL Content Fragments]{#sites-contentfragments-6522}

* AEM En la versión actualizada de 6.5.17, guardar fragmentos de contenido generó el siguiente error: *ERROR: No se pudo guardar el fragmento de contenido.* (SITES-22993)
* AEM Se identificó un problema con un solucionador de recursos sin cerrar en `ContentFragmentModelOmniSearchHandler` en el editor de la página de inicio de la página de la página de. (SITES-24903)


#### [!DNL Content Fragments] - Administrador{#sites-admin-6522}

Al hacer clic en el vínculo en la notificación por correo electrónico, se dirige al usuario al visor o editor de recursos predeterminado. Lo hace en lugar del editor de fragmentos de contenido, incluso cuando el recurso del flujo de trabajo está determinado como un fragmento de contenido. (SITES-24338)


#### [!DNL Content Fragments] - API de GraphQL {#sites-graphql-api-6522}

Al utilizar fragmentos de contenido con elementos de campo de texto multilínea, el marcado generado al consultar con GraphQL no conservaba el formato especificado en el HTML. Por ejemplo, faltaba una nueva línea después de la lista. Esto tuvo como consecuencia que el último párrafo pasara a formar parte de la lista. (SITES-23233)


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6522}

* A


#### [!DNL Content Fragments] - REST API{#sites-restapi-6522}

* A -->

#### Servidor principal{#sites-core-backend-6522}

* AEM Se notificaron `SegmentNotFoundException` errores recurrentes en una instancia de autor de la. Al reiniciar el autor, se resolvió temporalmente el problema, pero se necesitaba una corrección a largo plazo para evitar que se produjeran más casos. (SITES-22573)
* Se planteó un problema con respecto a la funcionalidad de la cronología en AEM Sites, específicamente en relación con la administración de las propiedades de `cq:lastModified` que faltan en las anotaciones. AEM Después de aplicar la versión 6.5.20, había incertidumbre sobre si el contenido existente necesitaba una corrección para la propiedad que faltaba o si la cronología se actualizaba para funcionar correctamente sin ella. (SITES-21861)


#### Componentes principales{#sites-core-components-6522}

* AEM Después de una actualización de la versión 6.5.18 a la versión 6.5.21, se identificó un problema con la funcionalidad que comprueba el uso activo de los componentes. Al intentar desplazarse para obtener elementos adicionales en la página Uso de Live, la tabla no cargaba más resultados a pesar de que se veía &quot;Cargando más elementos&quot; en la interfaz de usuario. (SITES-23919)
* AEM Se ha informado de un problema con la validación de los campos obligatorios en un cuadro de diálogo de componente de la que contiene dos pestañas. La pestaña 1 incluía un Editor de texto enriquecido (RTE) y campos de texto, mientras que la pestaña 2 tenía campos de ruta y campos de texto. Aunque todos los campos están marcados como obligatorios (`required=true`), las notificaciones de error persisten incorrectamente en la ficha 1, incluso después de rellenar todos los campos obligatorios. Por el contrario, los errores de la pestaña 2 se borran según lo esperado. (SITES-23243)
* AEM Después de migrar a la versión 6.5.21 del lenguaje de plantilla de HTML `data-sly-include`, la instrucción ya no funcionaba como se esperaba, específicamente no admitía expresiones `appendPath` y `prependPath`. Como resultado, el resultado del recurso incluido no se representó correctamente, aunque funcionaba correctamente antes de la migración. Este problema provocaba errores de procesamiento en los recursos que dependen de estas expresiones para la manipulación de rutas. (GRANITE-52970)


<!-- #### Campaign integration{#sites-campaign-integration-6522}

* A -->


#### Fragmentos de experiencias{#sites-experiencefragments-6522}

* Los fragmentos de experiencias no se ordenan por título como se esperaba cuando se hace clic en el encabezado de columna **Title** en la vista de lista. Se observa un parpadeo rápido en la pantalla, pero no se ordena. (SITES-23706)

* AEM En la versión 6.5.17, se ha producido un problema al convertir un componente de página en un fragmento de experiencia con la función predeterminada. Después de la conversión, el fragmento de experiencia aparecía vacío durante la edición, a pesar de mostrarse correctamente en la página en la que se utilizó. El problema se debía a una creación de nodo incorrecta: el nodo de componente se colocaba fuera del nodo raíz/contenedor, violando la estructura de la plantilla. Necesitaba mover manualmente el nodo de componente al nodo raíz/contenedor correcto para restaurar la editabilidad del fragmento. (SITES-22974)

* AEM Después de migrar de la versión 6.5.11 a la versión 6.5.20, las configuraciones en la nube en los fragmentos de experiencias no se guardaban correctamente. Aunque las configuraciones parecían guardarse en `crx/de`, no se mostraban al volver a abrir la consola de configuraciones, lo que indica un problema de persistencia. (SITES-22287)


<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6522}

* A -->


#### Lanzamientos{#sites-launches-6522}

AEM Al agregar recursos del fragmento de experiencia usando el filtro de etiquetado en la producción de, el usuario podía seleccionarlo, pero luego encontró un error después de seleccionar **Crear copia de idioma**. El comportamiento esperado era que el recurso de fragmento de experiencia seleccionado del filtro de etiquetado se suponía que se agregaría al proyecto de traducción. (SITES-24152)

#### Verificador de vínculos{#sites-link-checker-6522}

LinkCheckerTask no puede autenticarse porque el cliente HTTP intenta NTLM antes de la autenticación básica, lo que provoca que el proxy bloquee a los usuarios después de varios intentos fallidos. En su lugar, el sistema debe utilizar la autenticación básica para autenticarse con el proxy, lo que permite que los servicios LinkCheckerTask funcionen correctamente. (SITES-25034)


#### MSM: Live Copies{#sites-msm-live-copies-6522}

* Cuando se aplican etiquetas SEO Robots a la copia principal y se despliegan en páginas de Live Copy, los valores aparecían correctamente en `crx/de`. Sin embargo, los valores no se reflejaban en la interfaz de usuario en Propiedades de página de las páginas de Live Copy. (SITES-23475)
* Los errores relacionados con los lanzamientos aparecían cuando se intentaba promocionar un lanzamiento a través de la interfaz de usuario. El asistente Promocionar lanzamiento permanecía vacío, lo que impedía completar el proceso de promoción. (SITES-19718)
* AEM Se han producido problemas con los fragmentos de experiencias en los siguientes intentos de crear Live Copies y realizar despliegues en el sistema de informes de la comunidad de experiencias. El problema se produjo cuando los usuarios encontraron un error de `NotFound` al intentar volver a la pantalla de administración de Fragmentos de experiencias desde la pantalla de Despliegue. (SITES-21933)


#### Editor de página{#sites-pageeditor-6522}

* El botón Deshacer cambió la posición del componente además de cambiar el texto a la última versión. (SITES-17465)
* Cuando se pegaba un componente de contenedor copiado, aparecía visualmente dos veces, lo que daba como resultado tres instancias en la página. Sin embargo, después de actualizar la página, el duplicado desapareció, lo que sugiere que el problema era probablemente un error visual temporal. (SITES-21890)
* Al navegar por el panel izquierdo Componentes con las teclas Tab o Mayús+Tab del teclado, varios elementos de texto no estaban claramente visibles, tanto visualmente como en el modo de pestaña. Este problema afectaba a la accesibilidad, lo que dificultaba la identificación o interacción con estos componentes durante la navegación mediante el teclado. (SITES-2266)

#### Replicación{#sites-replication-6522}

AEM En las versiones 6.5.18 y 6.5.19, al desactivar una página principal, se generaron varias solicitudes de desactivación para cada página secundaria. Este problema también provocó la cancelación masiva de la publicación de los extremos de GraphQL. (NPR-42075 Y NPR42010)


### [!DNL Assets]{#assets-6522}

* Al utilizar la función Assets conectado, las actualizaciones realizadas en AEM Assets no se reflejan en el entorno de AEM Sites. (ASSETS-42344)
* Problemas con el estado de publicación del recurso al mover recursos de una ubicación a otra dentro del Experience Manager. (ASSETS-41158)
* La carga de recursos mediante la API genera `unclosed resource resolver` mensaje de error. (ASSETS-41049)
* Problemas con la consulta de referencia `AssetReferenceResolverImpl` después de actualizar a Adobe Experience Manager, Service Pack 21. (ASSETS-40384)
* AEM En la versión 6.5.19 de la aplicación, aunque se elimina una opción de los resultados del panel de búsqueda, también se desmarcan todas las demás casillas de verificación disponibles. (ASSETS-37335)
* Los valores no deseados se muestran en la salida de Excel mientras se realiza la operación de exportación masiva de metadatos. (ASSETS-37260)
* AEM En la versión 6.5.19 de, cuando se carga un archivo de SVG en formato UTF-8, el resultado es borroso. (ASSETS-36616)
* Falta la opción `Fetch original rendition for Dynamic Media Connected Assets` en la configuración de Assets conectado. (ASSETS-41726)
* Las propiedades de recurso se guardan incluso si no se define un valor para los campos obligatorios. (ASSETS-37914)
* Si el estado de procesamiento de un recurso es Error o Error de metadatos, la IU de los subtítulos y las pistas de audio no funciona correctamente. (ASSETS-37281)
* Al guardar los metadatos de un recurso e intentar editarlos, no se muestra el nombre del idioma. (ASSETS-37281)

#### [!DNL Dynamic Media]{#assets-dm-6522}

Un problema de producción interrumpió el proceso de migración cuando se producía un error en la carga de vídeo en Dynamic Media, que mostraba un error de error de proceso en la interfaz de usuario. (ASSETS-36038)


### [!DNL Forms]{#forms-6522}

Las correcciones de [!DNL Experience Manager] Forms se entregan mediante un paquete de complementos independiente una semana después de la fecha de lanzamiento programada del paquete de servicio [!DNL Experience Manager]. AEM En este caso, el lanzamiento del paquete de complementos de Forms de la versión 6.5.22.0 está programado para el jueves, 28 de noviembre de 2024. Se ha añadido una lista de correcciones y mejoras de Forms a esta sección después de la versión.


<!-- #### [!DNL Adaptive Forms] {#forms-6522}

* A


#### [!DNL Forms Designer] {#forms-designer-6522}

* A -->


### Foundation {#foundation-6522}

En la consola de AEM Assets, se ha producido un problema al intentar reordenar documentos DITA. La ruta de exploración situada en la parte superior del cuadro de diálogo del explorador de rutas muestra incorrectamente el nombre del nodo en lugar del título del nodo para el nodo principal raíz. El título del nodo correcto solo aparece después de seleccionar un elemento dentro de la ruta de exploración, lo que indica un error de visualización temporal. (NPR-42106)


<!-- #### Apache Felix {#foundation-apachefelix-6522}


* A

#### Campaign{#foundation-campaign-6522}

* A


#### Cloud Services{#foundation-cloudservices-6522}

* A -->


#### Comunidades {#foundation-communities-6522}

AEM Después de actualizar de la versión 6.5.19 a la versión 6.5.20, surgió un problema en el cual `Connection evic` subprocesos no se cerraron correctamente después de las llamadas a `UgcSearch`. Este problema, observado en el entorno de producción, hace que estos subprocesos persistan y se acumulen con el tiempo, lo que podría afectar al rendimiento. (NPR-42019)


<!-- #### Content distribution{#foundation-content-distribution-6522}

* A -->


#### CRX {#foundation-crx-6522}

* La ordenación no funcionaba de acuerdo con **Grupos** del menú del lado izquierdo del Administrador de paquetes de CRX. (GRANITE-53277)
* AEM El Administrador de paquetes en la restringe la instalación de versiones de paquetes más bajas de forma predeterminada, pero permite instalaciones potentes de versiones anteriores. Sin embargo, el uso de la opción de instalación forzada puede interferir con futuras instalaciones a través de la canalización estándar. Por ejemplo, si está instalada la versión 1.21 de y se agrega la versión 1.24, la instalación se realiza correctamente e incluye ambas versiones. Sin embargo, al intentar instalar la versión 1.22 sobre 1.24, se produce un error en la canalización, pero funciona si se instala a la fuerza, enumerando todas las versiones. Del mismo modo, la instalación de la versión 1.23 se bloquea si la versión 1.24 ya está presente, ya que la canalización no permite las actualizaciones posteriores. (GRANITE-53263)


#### Granite{#foundation-granite-6522}

* AEM Los paquetes de instantáneas se estaban instalando en mediante comandos CURL. Durante la instalación, el instalador JCR analizó los paquetes mediante el instalador OSGI para asegurarse de que no se requieran paquetes o configuraciones OSGI adicionales. Si la versión de un paquete contenía &quot;SNAPSHOT&quot;, el instalador de OSGI activaba VLT para crear un paquete de instantáneas correspondiente. AEM Sin embargo, dado que cada instancia de autor de ejecuta su propio instalador OSGI, ambas instancias pueden intentar generar la instantánea simultáneamente, lo que provoca conflictos de sesión dentro del repositorio. (NPR-42003)
* AEM Existía una contención de bloqueo en `ScriptDependencyResolver` con la versión 6.5.21 de la aplicación de la versión de la aplicación de seguridad de. (GRANITE-53181)
* AEM Después de actualizar a la versión 6.5.21, surgieron problemas cuando se usaban rutas relativas en la sintaxis de Sightly (HTL), como `data-sly-use`. (GRANITE-53080)


#### Integraciones{#foundation-integrations-6522}

* Se ha añadido una declaración de atribución legal para la interfaz de usuario de Cloud Service. (FORMS-16373)
* Adición de permisos de lectura para que el usuario **fd-cloudservice** acceda a las configuraciones de hCaptcha y Turnstile, lo que le permite recuperar el ID de cliente y el secreto de cliente necesarios para la validación y el procesamiento de captcha. Además, se implementó un modelo de Lista de control de acceso para administrar el acceso a estas configuraciones. (FORMS-16360)


#### Localización{#foundation-localization-6522}

En ![Icono de martillo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) Herramientas > **Seguridad** > ![Icono de usuario](https://spectrum.adobe.com/static/icons/workflow_18/Smock_User_18_N.svg) **Usuarios**, en la página Administración de usuarios, los datos de la columna **Estado** de la tabla se mostraban verticalmente. (GRANITE-48304)


<!-- #### Oak {#foundation-oak-6522}

* A -->


#### Plataforma{#foundation-platform-6522}

* AEM El seguimiento de Enterprise Information Management introducido en la versión 6.5.18 de ha producido anomalías en el cálculo de las puntuaciones de adopción del producto. La biblioteca de métricas de Adobe provocó este problema al sobrescribir los datos de usuario proporcionados por la biblioteca de seguimiento de Omega. Como resultado, las puntuaciones de adopción de muchos clientes de AEM Sites y AEM Assets cayeron a cero a partir de febrero de 2024. (CQ-4358438)
* Se ha identificado un problema crítico en el entorno de producción en el que el recolector de elementos no utilizados gestionaba las etiquetas de forma incorrecta. Específicamente, cuando se movió una etiqueta o se le cambió el nombre, el recolector de elementos no utilizados no pudo actualizar la propiedad `cq:MovedTo`, lo que provocó que la etiqueta desapareciera de las páginas. (CQ-4358293)
* AEM AEM Un problema con ContextHub en la versión 6.5.19 hacía que los segmentos se resolvieran incorrectamente cuando se agregaba una ruta de contexto a una instancia de. El problema afectaba específicamente al campo URL dentro de los objetos de JavaScript generados por el componente de página, donde faltaba el prefijo de ruta de contexto requerido. Esta omisión impedía que los segmentos funcionaran según lo esperado. (SITES-21852)
* AEM Se actualizó el Inicio rápido de la para utilizar la biblioteca `commons-collections-3.2.2-adobe-2`. La actualización garantiza que la aplicación se pueda seguir ejecutando sin problemas. (NPR-42150)
* AEM La configuración de OAuth2 de SMTP en la versión 6.5 de difiere considerablemente de la que se utiliza en AEM as a Cloud Service. AEM Para agilizar la configuración y garantizar la coherencia, la configuración de la versión 6.5 de la aplicación de seguridad debía ajustarse a los estándares utilizados en AEM as a Cloud Service. (GRANITE-53273)
* Se encontró un problema al hacer clic en ![Icono de brújula](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Compass_18_N.svg) > ![Icono del proyecto](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Project_18_N.svg) Proyectos y, a continuación, al pasar el puntero del ratón sobre ![Icono de carril izquierdo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) ![Icono de cheurón hacia abajo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg), apareció un acento grave antes de la información sobre herramientas &quot;Solo contenido&quot;. (CQ-4356633)

#### Seguridad{#foundation-security-6522}

* AEM Se han encontrado problemas con una biblioteca criptográfica JSAFE obsoleta (versión 6.0.0) en la. AEM En la versión 6.5.22 se incluye un paquete parcheado con la versión 6.2.5 de JSAFE. (NPR-42006)
* Al validar los protocolos permitidos durante las comprobaciones XSS, los controladores se comparan con &quot;http&quot; y &quot;https&quot;. Sin embargo, la propiedad `protocol` de un objeto URL devolvió estos valores con dos puntos finales, como `http:` y `https:`. Esta discrepancia causó problemas de validación. Para garantizar un análisis preciso, la comprobación de protocolo necesaria para tener en cuenta los dos puntos o ajustar la lógica de comparación en consecuencia.  (NPR-42119)
* AEM AEM Después de instalar la versión 6.5.21 (la versión anterior era la 6.5.19) en IBM® WebSphere® Liberty Profile y Semeru Java 8.0, no se pudo abrir ninguna página. Los registros de errores indicaron problemas relacionados con las versiones de servlet que requerían diferentes paquetes. Para solucionar este problema, se tuvo que revertir la dependencia de `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar` porque estaba relacionada con el problema. (NPR-42116)
* Varios exploradores están eliminando gradualmente la compatibilidad con las cookies **SameSite=None**, que se utilizan para permitir el acceso entre sitios a las cookies. Como alternativa, se están introduciendo **cookies particionadas**. Estas cookies aíslan el almacenamiento según el contexto en el que se utilizan, lo que mejora la privacidad y seguridad al impedir el seguimiento entre sitios, al tiempo que permite que las cookies funcionen dentro de particiones específicas, como contenido de terceros incrustado. (GRANITE-51953)


<!-- #### Sling{#foundation-sling-6522}

* A -->


#### Traducción{#foundation-translation-6522}

* Se ha agregado compatibilidad con los cambios recientes en los componentes principales en las reglas de traducción predeterminadas. (NPR-42029)
* Se ha identificado un problema con la exportación de archivos XLIFF en AEM Forms. Al usar la opción **Exportar selección como XLIFF (solo cadenas)**, la secuencia de componentes no se mantenía de forma coherente. Sin embargo, la secuencia sigue siendo correcta al exportar XLIFF para un idioma específico. Se proporcionaron dos archivos para demostrar el problema: **DE-CH_Export.xliff** (secuencia correcta) y **String_Export.xliff** (secuencia incorrecta). (NPR-42118)


#### Interfaz de usuario{#foundation-ui-6522}

* AEM `coralui-component-dialog` estaba alterando la ubicación de `cq-dialog-actions`, lo que podría afectar el diseño o el comportamiento de los botones de acción en los cuadros de diálogo de la. (NPR-42294)
* AEM La funcionalidad del selector de color en la no funcionaba correctamente. Cuando se accede a él, muestra un modal en blanco, lo que impide la selección de color. AEM Este problema comenzó después de instalar la versión 6.5.20 de en el entorno de ensayo. El selector de color funcionó correctamente *antes* de la actualización. (NPR-42163)
* En ![Icono de martillo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) **Herramientas** > **Flujo de trabajo** > **Modelos** > seleccione cualquier modelo > **Iniciar flujo de trabajo**, faltaba el icono Examinar en el campo Carga útil del cuadro de diálogo **Ejecutar flujo de trabajo**. (NPR-42162)


<!-- #### WCM{#foundation-wcm-6522}

* A


#### Workflow{#foundation-workflow-6522}

* A -->


## Instalar [!DNL Experience Manager] 6.5.22.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.22.0 requiere [!DNL Experience Manager] 6.5. Consulte [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas. <!-- UPDATE FOR EACH NEW RELEASE -->
* La descarga del Service Pack está disponible en el Adobe [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip).
* En una implementación con MongoDB y varias instancias, instale [!DNL Experience Manager] 6.5.22.0 en una de las instancias de creación mediante el Administrador de paquetes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> El Adobe no recomienda quitar ni desinstalar el paquete [!DNL Experience Manager] 6.5.22.0. Como tal, antes de instalar el paquete, debe crear una copia de seguridad de `crx-repository` en caso de que deba revertirla. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Instalar el Service Pack en [!DNL Experience Manager] 6.5{#install-service-pack}

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (cuando la instancia se haya actualizado desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de realizar la instalación, realice una instantánea o una copia de seguridad nueva de la instancia de [!DNL Experience Manager].

1. Descargar el Service Sack de [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra el Administrador de paquetes y seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y luego seleccione **[!UICONTROL Instalar]**.

1. Para actualizar el conector S3, detenga la instancia después de la instalación del Service Pack, sustituya el conector existente por un nuevo archivo binario proporcionado en la carpeta de instalación y reinicie la instancia. Consulte [Almacén de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo de la interfaz de usuario del administrador de paquetes a veces se cierra durante la instalación del paquete de servicio. El Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete actualizador antes de asegurarse de que la instalación se haya realizado correctamente. Normalmente, este problema se produce en el explorador [!DNL Safari], pero puede ocurrir de forma intermitente en cualquier explorador.

**Instalación automática**

Puede usar dos métodos diferentes para instalar [!DNL Experience Manager] 6.5.22.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en la carpeta `../crx-quickstart/install` cuando el servidor esté disponible en línea. El paquete se instala automáticamente.
* Use la API [HTTP del Administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que se instalen los paquetes anidados.

>[!NOTE]
>
>Experience Manager 6.5.22.0 no admite la instalación de Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar la instalación**

Para conocer las plataformas que están certificadas para funcionar con esta versión, consulte los [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.22.0)` en [!UICONTROL Productos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos los paquetes OSGi están **[!UICONTROL ACTIVOS]** o **[!UICONTROL FRAGMENTOS]** en la consola OSGi (use la consola web: `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es de la versión 1.22.20 o posterior (utilice la consola web: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### Instalar Service Pack para [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Para obtener instrucciones para instalar el Service Pack en Experience Manager Forms, consulte [Instrucciones de instalación del Service Pack de Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La funcionalidad Formularios adaptables, disponible en [AEM 6.5 Inicio rápido](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), está diseñada únicamente para la exploración y la evaluación. Para su uso en producción, es esencial obtener una licencia válida para AEM Forms, ya que la funcionalidad Formularios adaptables requiere una licencia adecuada.

### Instalación del paquete de índice de GraphQL para fragmentos de contenido de Experience Manager{#install-aem-graphql-index-add-on-package}

Los clientes que usan GraphQL deben instalar el [fragmento de contenido de Experience Manager con el paquete de índice 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip) de GraphQL.

Al hacerlo, puede añadir la definición de índice necesaria en función de las funciones que utilizan realmente.

Si no se instala este paquete, las consultas de GraphQL pueden ser lentas o dar error.

>[!NOTE]
>
>Instale este paquete solo una vez por instancia; no es necesario reinstalarlo con cada Service Pack.

### UberJar{#uber-jar}

UberJar para [!DNL Experience Manager] 6.5.22.0 está disponible en el [repositorio de Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.21/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para usar UberJar en un proyecto de Maven, consulta [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluye la siguiente dependencia en el POM de tu proyecto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.22</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar y los demás artefactos relacionados están disponibles en el repositorio de Maven Central en lugar del repositorio Maven público de Adobe (`repo.adobe.com`). Se cambió el nombre del archivo principal de UberJar a `uber-jar-<version>.jar`. Por lo tanto, no hay `classifier`, con `apis` como valor, para la etiqueta `dependency`.


## Funciones en desuso y eliminadas{#removed-deprecated-features}

Ver [funciones obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md/).

## Problemas conocidos{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->


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

   1. Instale el Service Pack o reinicie el Experience Manager as a Cloud Service.
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

* AEM A partir de la versión 6.5.15 de, el motor Rhino JavaScript proporcionado por el paquete ```org.apache.servicemix.bundles.rhino``` presenta un nuevo comportamiento de elevación. Los scripts que utilizan el modo estricto (```use strict;```) deben declarar sus variables correctas. De lo contrario, no se ejecutan y terminan generando un error de tiempo de ejecución.

* La instalación del contenido listo para usar relacionado con el etiquetado mediante un paquete de actualización oficial restablece la propiedad de idiomas del nodo `/content/cq:tags` de forma predeterminada. Esta acción se aplica a los paquetes de servicio, los paquetes de servicio de seguridad, los paquetes de funciones ampliadas, los paquetes de funciones acumulativas, los parches, etc. Por lo tanto, es necesario agregarlo desde las propiedades antes de la instalación.

### Problema conocido de AEM Sites {#known-issues-aem-sites-6522}

* Fragmentos de contenido: la previsualización falla debido a la protección DoS para un gran árbol de fragmentos. Consulte el artículo de [KB sobre las opciones de configuración predeterminadas de GraphQL Query Executor](https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)


### Problemas conocidos de AEM Forms {#known-issues-aem-forms-6522}

* Después de instalar AEM Forms JEE Service Pack 21 (6.5.21.0), si encuentra entradas duplicadas de Jars Geode `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` en la carpeta `<AEM_Forms_Installation>/lib/caching/lib` (FORMS-14926), realice los siguientes pasos para resolver el problema:

   1. Detenga los localizadores, si están en funcionamiento.
   1. AEM Detenga el servidor de la.
   1. Vaya a `<AEM_Forms_Installation>/lib/caching/lib`.
   1. Quite todos los archivos de revisión de Geode excepto `geode-*-1.15.1.2.jar`. Confirme que solo están presentes los jars Geode con `version 1.15.1.2`.
   1. Abra el símbolo del sistema en modo de administrador.
   1. Instale el parche de Geode mediante el archivo `geode-*-1.15.1.2.jar`.

* Si un usuario intenta obtener una vista previa de un borrador de carta con datos XML guardados, se queda atascado en el estado `Loading` para algunas cartas específicas. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (FORMS-14521)

* Después de actualizar a AEM Forms Service Pack 6.5.21.0, el servicio `PaperCapture` no puede realizar operaciones de reconocimiento óptico de caracteres (OCR) en los PDF. El servicio no genera resultados en forma de PDF o archivo de registro. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (CQDOC-21680)

* AEM Cuando los usuarios actualizaban de 6.5 Forms Service Pack 18 o 19 a Service Pack 20 o 21, se topaban con un error de compilación de JSP. Este error les impedía abrir o crear formularios adaptables. AEM También causó problemas con otras interfaces de la. Estas interfaces incluían el editor de páginas, la interfaz de usuario de AEM Forms, el editor de flujos de trabajo y la interfaz de usuario de Información general del sistema. (FORMS-15256)

  Si tiene un problema de este tipo, realice los siguientes pasos para resolverlo:
   1. Vaya al directorio `/libs/fd/aemforms/install/` en CRXDE.
   1. Elimine el paquete con el nombre `com.adobe.granite.ui.commons-5.10.26.jar`.
   1. AEM Reinicie el servidor de.

* Después de actualizar al paquete de servicio 20 de AEM Forms (6.5.20.0) con el complemento de Forms, las configuraciones que dependen del servicio de Adobe Analytics Cloud heredado mediante autenticación basada en credenciales dejan de funcionar. Este problema impedía que las reglas de Analytics se ejecutaran correctamente. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (FORMS-15428)

* Cuando un usuario actualiza al paquete de servicio 20 de AEM Forms (6.5.20.0) en el servidor JEE y genera PDF mediante servicios de salida, los PDF se representan con problemas de accesibilidad. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3922112)
* Cuando un usuario genera PDF etiquetados mediante el servicio de salida en JEE, muestra &quot;Advertencia de estructura inadecuada&quot;. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3922038)
* Cuando se envía un formulario en AEM Forms JEE, las instancias de un elemento XML repetitivo se eliminan de los datos. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3922017)
* Cuando un usuario en un entorno Linux® procesa un formulario adaptable (en JEE) en HTML, no se procesa correctamente. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3921957)
* Cuando un usuario convierte un archivo XTG al formato PostScript mediante el servicio Output en AEM Forms JEE, se produce el siguiente error: `AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE`. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3921720)
* Después de actualizar al paquete de servicio 18 de AEM Forms (6.5.18.0) en el servidor JEE, cuando un usuario envía un formulario, no puede procesar PDF forms HTML5 o y se bloquea XMLFM. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3921718)
* En la Vista previa de impresión de la interfaz de usuario de Interactive Communications Agent, el símbolo de moneda (como el signo de dólar $) se muestra de forma incoherente para todos los valores de campo. Aparece para valores de hasta 999, pero falta para valores de 1000 y superiores. (FORMS-16557)
* Las modificaciones realizadas en el XDP de los fragmentos de diseño anidados en una comunicación interactiva no se reflejan en el editor de CI. (FORMS-16575)
* En la Vista preliminar de la interfaz de usuario de Interactive Communications Agent, algunos valores calculados no se muestran correctamente. (FORMS-16603)
* Cuando la carta se ve en la Vista previa de impresión, el contenido cambia. Es decir, algunos espacios desaparecen y ciertas letras se sustituyen por &quot;x&quot; (FORMS-15681)

## Paquetes de contenido y paquetes OSGi incluidos{#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en esta versión del paquete de servicio [!DNL Experience Manager] 6.5:

* [Lista de paquetes OSGi incluidos en el Experience Manager 6.5.22.0](/help/release-notes/assets/65220-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de paquetes de contenido incluidos en el Experience Manager 6.5.22.0](/help/release-notes/assets/65220-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sitios web restringidos{#restricted-sites}

Estos sitios web solo están disponibles para los clientes de. Si es cliente de y necesita acceso, póngase en contacto con el administrador de cuentas de Adobe de.

* [Descarga de producto en Licensing.adobe.com](https://licensing.adobe.com/)
* [Póngase en contacto con Atención al cliente de Adobe](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página de producto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html?lang=es)
>* [[!DNL Experience Manager] Documentación de 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [Suscribirse a las actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html)
