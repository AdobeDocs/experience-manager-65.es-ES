---
title: Notas de la versión para [!DNL Adobe Experience Manager] 6,5
description: Encuentre información de la versión, novedades, instrucciones de instalación y una lista de cambios detallada para [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
exl-id: cac14ac1-9cda-46ae-8aa3-94674bb79157
source-git-commit: 8d06457241919095fd9802f69df426a1cc6851da
workflow-type: tm+mt
source-wordcount: '3675'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] Notas de la versión del paquete de servicio más reciente de 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.19.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versión del paquete de servicio |
| Fecha | Jueves, 30 de noviembre de 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.19.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## ¿Qué incluye? [!DNL Experience Manager] 6.5.19.0 {#what-is-included-in-aem-6519}

[!DNL Experience Manager] 6.5.19.0 incluye nuevas funciones, mejoras clave solicitadas por el cliente, correcciones de errores y mejoras de rendimiento, estabilidad y seguridad que se han publicado desde la publicación inicial de 6.5 en abril de 2019. [Instalar este Service Pack](#install) el [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Algunas de las funciones y mejoras clave de esta versión son las siguientes:

**Funciones principales**

* Recursos, Dynamic Media - [Compatibilidad con subtítulos múltiples y pistas de audio múltiple para vídeos en Dynamic Media](/help/assets/video.md#about-msma): ahora se pueden añadir fácilmente varios subtítulos y varias pistas de audio a un vídeo principal. Esta capacidad significa que los vídeos son accesibles para toda la audiencia global. Puede personalizar un solo vídeo principal publicado a una audiencia global en varios idiomas y adherirse a las directrices de accesibilidad para diferentes regiones geográficas. Los autores también pueden administrar los subtítulos y las pistas de audio desde una sola pestaña en la interfaz de usuario.

* Recursos: desde los resultados de búsqueda, ahora puede navegar a la ubicación de la carpeta que contiene un recurso para permitirle realizar varias tareas de administración de recursos. (ASSETS-23182)

**Mejoras clave**

* El Selector de estrella de Sites en Fragmentos de contenido ha mejorado el rendimiento. (SITES-14092)

* Se habilitó al usuario del Editor de páginas de sitios/Componente de imagen para hacer referencia a los recursos desde el Cloud Service de recursos remoto. (SITES-13448, SITES-13433)

* Para encontrar rápidamente un proyecto en la Vista de lista, donde puede tener muchos proyectos en el sistema, el Adobe ahora admite la ordenación del lado del servidor. Los nodos del proyecto se ordenan en el servidor en función de la columna seleccionada por el usuario antes de procesarlos en la interfaz de usuario. (NPR-41027)

* AEM 6.5.19.0 es compatible con MongoDB 5.0 a 6.0.

**Función en desuso**

* AEM ActiveMQ en el caso de que la aplicación esté en desuso. AEM ActiveMQ se utilizaba para la comunicación entre dos instancias de publicación de. Adobe recomienda que los clientes ahora utilicen un equilibrador de carga.

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Se han corregido problemas en Service Pack 19 {#fixed-issues}

### [!DNL Sites]{#sites-6519}

#### Accesibilidad{#sites-accessibility-6519}

* En una página de AEM Sites, cuando amplía un 200 % la página, los vínculos **[!UICONTROL Copia de idioma]** y **[!UICONTROL Informe CSV]** en el carril Referencias desaparecen. (SITES-11011)

#### Interfaz de usuario de administrador{#sites-adminui-6519}

* Canal de AEM Screens **[!UICONTROL Previsualizar]** La funcionalidad de no funciona ni se muestra en el panel. (SITES-15730)
* Durante una operación de movimiento de página, si la interfaz de usuario no puede mostrar las referencias pero indica que se vuelven a publicar automáticamente, se muestran *no* republicado. (SITES-16435)
* AEM En la versión 6.5 con Service Pack 16 o 17, cuando en la vista de lista de sitios con la columna &quot;Flujo de trabajo&quot; habilitada, no se puede ordenar la lista en función de los elementos de esa columna. No se realiza ninguna ordenación. (SITES-15385)
* Para una plantilla de página de redireccionamiento, el campo de redireccionamiento se ha hecho obligatorio. Sin embargo, la validación del campo requerido no se está aplicando ni funciona en estos dos casos: cuando se crea una página sin un valor de redirección obligatorio; no se puede crear una página de redirección. La validación no funciona al navegar mediante métodos abreviados de teclado y cuando el campo se marca como no válido, no continúa. (SITES-15903)
* Algunos **Vínculos entrantes** no se incluían en el recuento mostrado en la **Referencias** panel. Por ejemplo, el panel mostraba lo siguiente **Enlaces entrantes (6)** pero en realidad había nueve enlaces entrantes. (SITES-14816)

#### IU clásica{#sites-classicui-6519}

* Después de instalar la revisión en SITES-15827, los títulos de los cuadros de diálogo que tenían espacios en blanco entre palabras se reemplazaban por `" "`. También se eliminaban los saltos de línea. (SITES-16089)
* Los títulos de los cuadros de diálogo codificados ahora dan como resultado una doble codificación del título. (SITES-15841)
* AEM La actualización de los servidores del servicio de 6.5.16 a 6.5.17 dio como resultado una doble codificación de los títulos de los cuadros de diálogo de la IU clásica. (SITES-15634)

#### [!DNL Content Fragments]{#sites-contentfragments-6519}

* Aparecerá un mensaje de error de servidor interno en el Editor de fragmentos de contenido. (SITES-13550)
* La actualización de la `org.json` La biblioteca de mediante NPR-41291 ha provocado conversiones de error de datos en la `DefaultDataTypeConverter` de la `cfm-impl` paquete. La conversión de tipos de datos debe ser más flexible. (SITES-16473)
* Aparece el mensaje emergente de error &quot;Esta versión del fragmento de contenido no se puede comparar con la versión actual porque hay contenido incompatible&quot;. Los fragmentos de contenido deben ser comparables, pero no lo es. (SITES-16317)
* Se ha cambiado la URL de JS de selector de recursos de
  `https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js`
hasta
  `https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js` (SITES-16068)
* Adapte el nuevo esquema de respuesta de la API de metadatos Polaris para la integración CFM-Polaris. (SITES-15166)
* Todos los fragmentos de contenido deben enumerarse donde se hace referencia al fragmento de contenido seleccionado. En su lugar, las referencias de recursos en el panel de referencia de fragmentos de contenido muestran referencias 0 (cero). (SITES-15036)

#### Servidor principal{#sites-core-backend-6519}

* Mejorar `StyleImpl`. (SITES-15164)
* Mejore la rama versión/650 de la canalización WCM para poder ejecutar pruebas de integración para sus módulos. (SITES-12938)

<!--#### Core Components{#sites-core-components-6519}

* A -->

#### Integración de Campaign{#sites-campaign-integration-6519}

* En el componente de firma (`/apps/fpl/components/campaign/signature`), el vínculo Externalizer no funcionaba. El dominio no se añadía al origen de la imagen si se eliminaba el comentario del HTML sobre la etiqueta de imagen. Este problema solo se encontró con el componente de firma en el entorno de producción, no en el entorno de ensayo. (SITES-16120)

<!--#### Experience Fragments{#sites-experiencefragments-6519}

* A -->

#### Componentes de base (heredados){#sites-foundation-components-legacy-6519}

* El componente de búsqueda de sitios de Adobe Experience Manager AEM () rompe la interfaz de usuario. (SITES-15087)

#### Editor de consultas de GraphQL{#sites-graphql-query-editor-6519}

* La interfaz de usuario del Editor de GraphQL no permite desplazarse por todas las consultas persistentes cuando hay un número elevado de consultas (por ejemplo, más de 25). (SITES-16008)
* El editor de GraphQL no guarda el estado de publicación de las consultas persistentes. El botón Cancelar la publicación aparece en el Editor de GraphQL, pero no aparece el icono que indica que se ha publicado la consulta persistente. Al actualizar la página, se muestra que la consulta persistente ni siquiera se ha publicado. (SITES-15858)

#### Lanzamientos{#sites-launches-6519}

* Los cambios en el repositorio no se guardan debido a `Oak0001` entra en conflicto cuando se editan varias páginas o se crea contenido. Es normal realizar un reintento en un evento de este tipo, pero esto no ocurre. (SITES-14840)

#### MSM: Live Copies{#sites-msm-live-copies-6519}

* El botón Despliegue de MSM no funciona en la interfaz gráfica de usuario táctil. (SITES-16991)
* La referencia de vínculo no se actualiza dentro del fragmento de experiencia al crear una Live Copy o al desplegar un fragmento de experiencia. (SITES-15460)

#### Editor de página{#sites-pageeditor-6519}

* En Forms > Temáticas, si abrió una temática en el editor de temáticas, realizó algunos cambios y guardó y, a continuación, hizo clic en Previsualizar, se ve un icono de carga, pero la previsualización real no se carga. (SITES-17164)
* La selección de varios tipos de archivo de documento en el filtro de tipo de recurso no funciona en la consola de página. No se encuentran resultados aunque estén disponibles los resultados de un tipo de archivo en particular. Como resultado, los autores no pueden filtrar varios documentos. Deben utilizar varios tipos de documento y tienen que filtrarlos de uno en uno. (SITES-14047)
* AEM AEM Después de actualizar una instancia desde la versión 6.5.17 y la versión 6.5.18, desde el Editor de páginas, si ha seleccionado, haga lo siguiente: **[!UICONTROL Publicar página]**, se le redirigirá a una dirección URL que no existe. Se debe redirigir al usuario al Asistente para publicación. (SITES-15856)
* AEM Copia redundante desde el portapapeles durante una operación de pegado desde el portapapeles del sistema operativo. (SITES-15704)
* En Assets, seleccione **[!UICONTROL Documentos]**, luego en **[!UICONTROL Filtertype]**, seleccionando **[!UICONTROL Microsoft® Word]** o **[!UICONTROL Microsoft® Excel]** no muestra ningún resultado aunque existan archivos de ambos tipos. (SITES-14837)

### [!DNL Assets]{#assets-6519}

* Al crear o guardar una carpeta pública, se crean tres grupos en un panel de administración. (ASSETS-26700)
* No se pueden diferenciar los recursos de publicación en Experience Manager o Brand Portal. (NPR-41320)
* En el panel de búsqueda, cuando selecciona casillas de verificación y anula la selección de cualquiera de ellas, se desactivan todas las casillas de verificación. (ASSETS-26377)

#### [!DNL Dynamic Media]{#assets-dm-6519}

* AEM Una vez cargado un recurso en la interfaz de usuario de, el elemento de configuración de la interfaz de usuario `update_asset` flujo de trabajo activado. El flujo de trabajo nunca termina. En las instancias de flujo de trabajo, el flujo de trabajo termina en el paso de carga del producto. El siguiente paso es cargar Scene7 por lotes. El usuario puede ver que el recurso se encuentra en Scene7 desde la aplicación de Dynamic Media Classic. (ASSETS-30443)
* Un servlet personalizado (extremo de API) devuelve un nombre de archivo de Dynamic Media (Scene7) incorrecto. Se produce cuando se elimina un recurso y se reemplaza por un recurso del mismo nombre. El servlet personalizado devuelve el nombre de archivo antiguo de Dynamic Media (Scene7), mientras que una llamada de API &quot;jcr&quot; devuelve el nombre de archivo correcto. (ASSETS-29476)
* Incluso después de desactivar la sincronización en el nivel de carpeta, los registros muestran el déclencheur de Scene7 ReplicateOnModifyListener. El `ReplicateOnModifyListener/Worker` debe omitir el procesamiento en recursos de carpeta que no sean de Dynamic Media y fragmentos de contenido. (ASSETS-26705)
* Las personas con visión reducida se ven afectadas si el Enfoque no es visible en los elementos desplegables (Solo contenido, Ver, Más opciones) en los modos blanco y negro de alto contraste. (ASSETS-25759)
* Las personas con visión reducida se ven afectadas si la proporción de contraste de luminosidad del texto de una página es inferior a 4,5:1. (ASSETS-25756)
* Los lectores de pantalla no narran el mensaje emergente mostrado después de enviar los datos. (ASSETS-25755)
* Los lectores de pantalla no reconocen los puntos de referencia en la página (Dynamic Media; creación de un perfil de codificación de vídeo) cuando se navega mediante la tecla de método abreviado de referencia o región `D/R`. (ASSETS-25752)
* Los lectores de pantalla no reconocen varios puntos de referencia en la página (Dynamic Media; creación de vídeo interactivo) cuando se navega mediante la tecla de método abreviado de referencia o región `D/R`. (ASSETS-25750)
* Los lectores de pantalla (NVDA/JAWS/Narrator) no reconocen los puntos de referencia de **Editar recurso** mientras se navega con las teclas de método abreviado `D/R`. (ASSETS-25744)
* El usuario recibe un mensaje de trabajo asincrónico vacío/falso, pero el recurso conectado se ha publicado correctamente. (ASSETS-29342)

### [!DNL Forms]{#forms-6519}

Correcciones en [!DNL Experience Manager] Forms se entregan mediante un paquete de complementos independiente una semana después de lo programado [!DNL Experience Manager] Fecha de lanzamiento del paquete de servicio. AEM En este caso, el lanzamiento del paquete de complementos de Forms de la versión 6.5.19.0 está programado para el jueves, 30 de noviembre de 2023. Se agregaría una lista de correcciones y mejoras de Forms a esta sección después de la versión.

* Agregar la lista de control de acceso para `fd-cloudservice` para poder leer o actualizar las configuraciones de Microsoft® en `cloudconfigs/microsoftoffice`. (FORMS-11142)

<!--LEFT BULLET LIST HERE IN CASE OF REUSE BY FORMS IN THE FUTURE 
* **Document Services**
  * text
* **Adaptive Forms** 
  * text
* **Accessibility**
  * text
* **Interactive Communications**
  * text -->

<!--### Commerce{#commerce-6519}

* A -->

### Foundation{#foundation-6519}

* La creación de una copia de idioma en el nivel raíz del idioma no ajusta las rutas en la página. En el caso de que se creara la copia de idioma, no para la raíz del idioma, sino para las páginas debajo de ella, la ruta cambió correctamente. (NPR-41364)
* La información del objeto &quot;Presentación de fecha relativa&quot; solo se puede cerrar pulsando Escape (ESC) en el teclado. La información del objeto debe cerrarse cuando el usuario selecciona cualquier parte de la interfaz de usuario. (NPR-41394)
* Cadena no localizada `Something went wrong while adding the private key.` al añadir un archivo de clave privada incorrecto en **Editar usuario** > **Keystore**. (NPR-41366)
* Los iconos son necesarios para Microsoft® SharePoint y MicrosoftAEM ® One Drive en el entorno de la versión 6.5 de. (NPR-41354)
* &quot;El ID de usuario y la contraseña no coinciden&quot; sin localizar. cadena en **Seguridad** > **Usuario** > **Crear** Cuadro de diálogo. (NPR-41245)
* El código emergente y los controladores de eventos se cargan dos veces, lo que rompe las interfaces de usuario basadas en Coral3 creadas por el usuario. (NPR-41171)
* La selección no funciona correctamente después de utilizar &quot;Seleccionar todo&quot; en la consola de AEM Sites. (NPR-41304)

<!--#### Content distribution{#foundation-content-distribution-6519}

* T -->

#### Integraciones{#integrations-6519}

* AEM Los vínculos SMS de una campaña de correo electrónico de no se escriben correctamente; contienen un elemento de anclaje de HTML. (NPR-41211)
* El texto utilizado en la pantalla de configuración de la cuenta no debe utilizar un nuevo tipo de credencial. (NPR-41210)
* Desplazamiento del programador de importación de informes de Analytics desde `ManagedPollConfig` a trabajos de sling. Cuando se adjuntaban dos marcos de análisis diferentes con grupos de informes diferentes en dos sitios diferentes, `ManagedPollConfig` encuesta solo a uno de ellos. (NPR-41209)
* Cuando el valor se restablece al valor predeterminado, el botón de periodo de tiempo seleccionado anteriormente permanece habilitado. AEM En el panel de información de contenido de la página de, de forma predeterminada, el lapso de tiempo se establece en la semana y muestra las perspectivas de contenido como datos semanales. Ahora, si el usuario selecciona otras opciones del lapso de tiempo, como hora, día, mes y año, los datos cambian según el valor seleccionado. Sin embargo, si los valores se restablecen, de forma predeterminada, el lapso de tiempo visible es de una semana, pero aun así la opción de lapso de tiempo seleccionada anteriormente está seleccionada. (NPR-41246)

#### Oak{#oak-6519}

* AEM Utilidad de Backport para establecer las escrituras de límite de tasa en caso de que se retrase la indexación asíncrona. (NPR-40985)

#### Plataforma{#foundation-platform-6519}

* Las consultas de QueryBuilder con corchetes se traducen erróneamente a xpath (NPR-41298)

<!--#### Replication{#foundation-replication-6519}

* R -->

<!--#### Sling{#foundation-sling-6519}

* W -->

#### Proyectos de traducción{#foundation-translation-6519}

* Al crear la copia de idioma de la página &quot;A&quot;, debe crear automáticamente las copias de idioma de las páginas, fragmentos de experiencias, fragmentos de contenido y recursos a los que se hace referencia. Además, la copia de idioma recién creada de la página &quot;A&quot; en la nueva ruta debe tener sus referencias actualizadas a las respectivas copias de idioma recién creadas de las páginas, los fragmentos de experiencias, los fragmentos de contenido y los recursos. (NPR-41076)

<!--#### User interface{#foundation-ui-6519}

* A -->

<!--#### WCM{#wcm-6519}

* A -->

#### Flujo de trabajo{#foundation-workflow-6519}

* No se puede completar una tarea en la bandeja de entrada. Solo se observa un valor &quot;indefinido&quot; en el menú desplegable al intentar completar la tarea y seleccionar una acción. AEM Esto significa que los usuarios no pueden aplicar el paquete de servicio 6.5.18 de la versión de. (NPR-41402 y NPR-41473)
* No se pueden completar las tareas en la bandeja de entrada. No hay ningún valor (solo &quot;indefinido&quot;) en la lista desplegable al intentar completar la tarea para archivos zip, informes de recursos, movimiento (éxito o error) o caducidad del recurso. (NPR-41305)
* Cuando un usuario selecciona **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > instancias, luego selecciona el flujo de trabajo en ejecución y, a continuación, selecciona **[!UICONTROL Ver carga útil]**, genera una página de error 500. (NPR-41325)

## Instalar [!DNL Experience Manager] 6.5.19.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.19.0 requiere [!DNL Experience Manager] 6.5. Véase [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas. <!-- UPDATE FOR EACH NEW RELEASE -->
* La descarga del Service Pack está disponible en el Adobe [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.19.0.zip).
* En una implementación con MongoDB y varias instancias, instale [!DNL Experience Manager] 6.5.19.0 en una de las instancias de autor mediante el Administrador de paquetes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> El Adobe no recomienda quitar ni desinstalar el [!DNL Experience Manager] Paquete 6.5.19.0. Como tal, antes de instalar el paquete, debe crear una copia de seguridad del `crx-repository` en caso de que deba revertirlo. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Instalación del Service Pack en [!DNL Experience Manager] 6,5{#install-service-pack}

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (cuando la instancia se haya actualizado desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de realizar la instalación, tome una instantánea o realice una copia de seguridad nueva de su [!DNL Experience Manager] ejemplo.

1. Descargue el Service Pack desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.19.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra el Administrador de paquetes y seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y luego seleccione **[!UICONTROL Instalar]**.

1. Para actualizar el conector S3, detenga la instancia después de la instalación del Service Pack, sustituya el conector existente por un nuevo archivo binario proporcionado en la carpeta de instalación y reinicie la instancia. Consulte [Almacén de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo en la interfaz de usuario del Administrador de paquetes a veces existe durante la instalación del Service Pack. El Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete actualizador antes de asegurarse de que la instalación se haya realizado correctamente. Normalmente, este problema se produce en el [!DNL Safari] explorador, pero puede producirse de forma intermitente en cualquier explorador.

**Instalación automática**

Existen dos métodos diferentes que puede utilizar para instalar automáticamente [!DNL Experience Manager] 6.5.19.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en `../crx-quickstart/install` cuando el servidor está disponible en línea. El paquete se instala automáticamente.
* Utilice el [API HTTP del Administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Uso `cmd=install&recursive=true` para instalar los paquetes anidados.

>[!NOTE]
>
>Experience Manager 6.5.19.0 no admite la instalación de Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validación de la instalación**

Para conocer las plataformas certificadas para trabajar con esta versión, consulte la [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.19.0)` bajo [!UICONTROL Productos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos los paquetes OSGi son **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web): `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.17 o posterior de (utilice la consola web: `/system/console/bundles`). <!-- NPR-41292 for 6.5.19.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Instalar Service Pack para [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Para obtener instrucciones para instalar el Service Pack en Experience Manager Forms, consulte [Instrucciones de instalación del Service Pack de Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La funcionalidad Formularios adaptables, disponible en [AEM 6.5 Inicio rápido](https://experienceleague.corp.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=es), está diseñada únicamente para la exploración y la evaluación. Para su uso en producción, es esencial obtener una licencia válida para AEM Forms, ya que la funcionalidad Formularios adaptables requiere una licencia adecuada.

### Instalación del paquete de índice de GraphQL para fragmentos de contenido de Experience Manager{#install-aem-graphql-index-add-on-package}

Los clientes que utilicen GraphQL deben instalar [Fragmento de contenido de Experience Manager con el paquete de índice 1.1.1 de GraphQL](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Al hacerlo, puede añadir la definición de índice necesaria en función de las funciones que utilizan realmente.

Si no se instala este paquete, las consultas de GraphQL pueden ser lentas o dar error.

>[!NOTE]
>
>Instale este paquete solo una vez por instancia; no es necesario reinstalarlo con cada Service Pack.

### UberJar{#uber-jar}

UberJar para [!DNL Experience Manager] 6.5.19.0 está disponible en la [Repositorio de Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.19/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para usar UberJar en un proyecto de Maven, consulte [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.19</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar y los demás artefactos relacionados están disponibles en el Repositorio de Maven Central en lugar del Repositorio de Maven público de Adobe (`repo.adobe.com`). El nombre del archivo principal de UberJar cambia a `uber-jar-<version>.jar`. Así que no hay `classifier`, con `apis` como el valor, para el `dependency` etiqueta.

## Funciones en desuso y eliminadas{#removed-deprecated-features}

Consulte [Funciones en desuso y eliminadas](/help/release-notes/deprecated-removed-features.md/).

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

   1. Elimine las dos carpetas siguientes de `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. Instale el Service Pack o reinicie el Experience Manager as a Cloud Service.
Nuevas carpetas de `cache` y `diff-cache` se crean automáticamente y ya no experimenta una excepción relacionada con lo siguiente `mvstore` en el `error.log`.

* Actualice las consultas de GraphQL que puedan haber utilizado un nombre de API personalizado para el modelo de contenido para utilizar el nombre predeterminado del modelo de contenido en su lugar.

* Una consulta de GraphQL puede utilizar el complemento `damAssetLucene` índice en lugar de `fragments` índice. Esta acción puede dar como resultado consultas de GraphQL que fallan o que tardan mucho tiempo en ejecutarse.

  Para corregir el problema, `damAssetLucene` debe configurarse para incluir las dos propiedades siguientes en `/indexRules/dam:Asset/properties`:

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

  Una vez cambiada la definición del índice, es necesario volver a indexar (`reindex` = `true`).

  Después de estos pasos, las consultas de GraphQL deberían funcionar más rápido.

* Al intentar mover, eliminar o publicar fragmentos de contenido, sitios o páginas, hay un problema cuando se recuperan las referencias de fragmentos de contenido, ya que la consulta en segundo plano falla. Es decir, la funcionalidad no funciona.
Para garantizar un funcionamiento correcto, debe agregar las siguientes propiedades al nodo de definición del índice `/oak:index/damAssetLucene` (no se requiere reindexación):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Si actualiza su [!DNL Experience Manager] instancia de 6.5.0 a 6.5.4 al Service Pack más reciente de Java™ 11, verá lo siguiente `RRD4JReporter` excepciones en la `error.log` archivo. Para detener las excepciones, reinicie la instancia de [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Los usuarios pueden cambiar el nombre de una carpeta en una jerarquía en [!DNL Assets] y publicar una carpeta anidada en [!DNL Brand Portal]. Sin embargo, el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Durante la instalación de, se pueden mostrar los siguientes errores y mensajes de advertencia [!DNL Experience Manager] 6.5.x.x:
   * &quot;Cuando la integración de Adobe Target está configurada en [!DNL Experience Manager] Si se utiliza la API de Target Standard (autenticación IMS) y se exportan los fragmentos de experiencias a Target, se crean tipos de ofertas incorrectos. En lugar de &quot;Fragmento de experiencia&quot;/fuente &quot;Adobe Experience Manager&quot;, Target crea varias ofertas con el tipo &quot;HTML&quot;/fuente &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: No se han encontrado ventanas de mantenimiento en granite/operations/maintenance.
   * La validación del lado del servidor de formularios adaptables falla cuando se utilizan funciones de agregado como SUM, MAX y MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - No hay ventanas de mantenimiento en granite/operations/maintenance.
   * El punto interactivo de una imagen interactiva de Dynamic Media no está visible al obtener una vista previa del recurso a través del visor de titulares de ventas.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : tiempo de espera hasta que se completó el cambio de registro sin registrar.

* AEM A partir de la versión 6.5.15, el motor JavaScript de Rhino proporcionado por el ```org.apache.servicemix.bundles.rhino``` El paquete tiene un nuevo comportamiento de elevación. Scripts que utilizan el modo estricto (```use strict;```) deben declarar correctamente sus variables; de lo contrario, no se ejecutan, lo que genera un error de tiempo de ejecución.

### Problemas conocidos de AEM Forms

#### Plataformas compatibles

* Las versiones de JDK superiores a 1.8.0_281 no son compatibles con el servidor JEE de WebLogic. (FORMS-8498, CQDOC-20383)
* Como [!DNL Microsoft® Windows Server 2019] no admite [!DNL MySQL 5.7] y [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] no admite instalaciones llave en mano para [!DNL Experience Manager Forms 6.5.10.0]. (CQDOC-18312)
* No se admite JDK 11.0.20 para instalar AEM Forms en el instalador JEE. Solo se admite JDK 11.0.19 o versiones anteriores para instalar AEM Forms en el instalador JEE. (FORMS-10659)

#### Instalación

* En la plataforma JBoss® 7.1.4, cuando el usuario instala el Service Pack de Experience Manager 6.5.16.0 o posterior, `adobe-livecycle-jboss.ear` la implementación falla. (CQ-4351522, CQDOC-20159)
* Después de actualizar al entorno del instalador completo llave en mano de AEM Forms 6.5.18.0 JBoss® en Windows Server 2022, al compilar el código de la aplicación cliente de salida mediante Java™ 11, puede producirse el siguiente error de compilación:

  ```
  error: error reading [AEM_Forms_Installation_dir]\sdk\client-libs\common\adobe-output-client.jar; java.net.URISyntaxException: 
  Illegal character in path at index 70: file:/[AEM_Forms_Installation_dir]/sdk/client-libs/common/${clover.jar.name} 1 error
  ```

  Para resolver el problema, realice los siguientes pasos:
   1. Vaya a `[AEM_Forms_Installation_dir]\sdk\client-libs\common\` y descomprima `adobe-output-client.jar` para extraer el `Manifest.mf` archivo.
   1. Actualice el `Manifest.mf` eliminando la entrada de `${clover.jar.name}` del atributo class-path.

      >[!NOTE]
      >
      > También puede utilizar una herramienta de edición in situ, por ejemplo, 7-zip, para actualizar el `Manifest.mf` archivo.

   1. Guarde el actualizado en `Manifest.mf` en el `adobe-output-client.jar` archive.
   1. Guardar el modificado `adobe-output-client.jar` y vuelva a ejecutar el programa de instalación. (CQDOC-20878)
* AEM Después de instalar el programa de instalación completo del paquete de servicio 6.5.19.0 de, la implementación de EAR falla en JEE mediante JBoss® Turnkey.
Para resolver el problema, busque `<AEM_Forms_Installation_dir>\jboss\bin\standalone.bat` archivar y actualizar `Adobe_Adobe_JAVA_HOME` hasta `Adobe_JAVA_HOME` para todas las ocurrencias antes de ejecutar el administrador de configuración. (CQDOC-20803)

#### AEM Instale el fragmento del servlet (paquete de servicio 6.5.14.0 o anterior de)

* AEM AEM Si está actualizando a Service Pack 6.5.15.0 o cualquier versión superior y la instancia de la instancia de la aplicación está funcionando en Tomcat 8.5.88, es obligatorio que instale el fragmento de servlet *antes* continúe con la instalación del paquete de servicio 6.5.15.0 o de cualquier versión superior.
* Es obligatorio instalar el fragmento de servlet para todos los servidores de aplicaciones excepto los que se ejecutan en JBoss® EAP 7.4.0.

**Para instalar el fragmento de servlet:**

1. Descargue el fragmento de servlet de [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).
1. Inicie el servidor de aplicaciones.
1. Espere a que se estabilicen los registros y compruebe el estado del paquete.
1. Abra los paquetes de la consola web. La URL predeterminada es `http://[Server]:[Port]/system/console/bundles`.
1. Seleccionar **[!UICONTROL Instalar]** o **[!UICONTROL Actualizar]**.
1. Seleccionar el fragmento descargado
   `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`
1. Seleccionar **[!UICONTROL Instalar]** o **[!UICONTROL Actualizar]**.
1. Espere a que se estabilice el servidor de aplicaciones.
1. Detenga el servidor de aplicaciones.

#### Formularios adaptables

* Cuando se publica un formulario adaptable, todas sus dependencias, incluidas las directivas, se vuelven a publicar, aunque no se hayan realizado modificaciones en ellas. (FORMS-10454)
* Cuando un usuario selecciona configurar un campo por primera vez en un formulario adaptable, la opción para guardar una configuración no se muestra en el Explorador de propiedades. El problema se resuelve seleccionando la configuración de otro campo del formulario adaptable en el mismo editor.
* Cuando se establece una URL de redireccionamiento en el contenedor de guía de un formulario adaptable, la firma en línea deja de funcionar. (FORMS-10493) Para resolver el problema, descargue e instale el [revisión para 6.5.18.0](/help/release-notes/aem-forms-hotfix.md).
* No se pueden publicar todas las plantillas de documento de registro (DoR). Solo se publican las plantillas de DoR basadas en la configuración regional en inglés y sus plantillas de DoR asociadas basadas en Forms. (FORMS-10535) Para resolver el problema, descargue e instale el [revisión para 6.5.18.0](/help/release-notes/aem-forms-hotfix.md).


#### Comunicaciones interactivas

* AEM Después de actualizar al paquete de servicio 18 de, no es posible abrir la comunicación interactiva con imágenes en línea grandes en el modo de edición. (FORMS-10578) Para resolver el problema, descargue e instale [revisión para 6.5.18.0](/help/release-notes/aem-forms-hotfix.md).

## Paquetes de contenido y paquetes OSGi incluidos{#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en [!DNL Experience Manager] 6.5.19.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.19.0](/help/release-notes/assets/65190_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.19.0](/help/release-notes/assets/65190_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sitios web restringidos{#restricted-sites}

Estos sitios web solo están disponibles para los clientes de. Si es cliente de y necesita acceso, póngase en contacto con el administrador de cuentas de Adobe de.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/)
* [Contactar con Atención al cliente de Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página de producto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentación de 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es)
>* [Suscripción a las actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html)
