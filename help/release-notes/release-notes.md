---
title: Notas de la versión para [!DNL Adobe Experience Manager] 6,5
description: Encuentre información de la versión, novedades, instrucciones de instalación y una lista de cambios detallada para [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 6bf2d6409a15be02a247fab84caa743e8542da13
workflow-type: tm+mt
source-wordcount: '3032'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] Notas de la versión del paquete de servicio más reciente de 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.21.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versión del paquete de servicio |
| Fecha | jueves, 6 de junio de 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## ¿Qué incluye? [!DNL Experience Manager] 6.5.21.0 {#what-is-included-in-aem-6521}

[!DNL Experience Manager] 6.5.21.0 incluye nuevas funciones, mejoras clave solicitadas por el cliente y correcciones de errores. También incluye mejoras de rendimiento, estabilidad y seguridad publicadas desde el lanzamiento inicial de la versión 6.5 en abril de 2019. [Instalar este paquete de servicio](#install) el [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Funciones principales y mejoras

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Algunas de las funciones y mejoras clave de esta versión son las siguientes:

* Una credencial nueva y más fácil de usar para la autenticación de servidor a servidor, que reemplaza la credencial de cuenta de servicio (JWT) existente. (NPR-41994)

### [!DNL Assets]

#### Mejoras

A continuación se muestra la lista de mejoras incluidas en esta versión:

* La pestaña IPTC ahora es compatible con [!UICONTROL Texto alternativo] y [!UICONTROL Descripción extendida] campos de texto. (ASSETS-34918)

#### Correcciones de accesibilidad

A continuación se muestra la lista de correcciones de accesibilidad incluidas en esta versión:

* Si el estado de procesamiento de un recurso es Error o Error de metadatos, la IU de los subtítulos y las pistas de audio no funciona correctamente. (ASSETS-37281)
* Al guardar los metadatos de un recurso e intentar editarlos, no se muestra el nombre del idioma. (ASSETS-37281)

<!-- ### [!DNL Forms]
* A -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Se han corregido problemas en Service Pack 21 {#fixed-issues}

### [!DNL Sites]{#sites-6521}

#### Accesibilidad {#sites-accessibility-6521}

* El **[!UICONTROL Búsquedas guardadas]** la etiqueta no es persistente. El marcador de posición se utiliza como la única etiqueta visual para un campo de texto. (SITES-3050)

#### Interfaz de usuario de administrador{#sites-adminui-6521}

* Al hacer clic en **[!UICONTROL Sites]** > **[!UICONTROL Componentes principales]** > **[!UICONTROL Propiedades]** > **[!UICONTROL Permisos]** pestaña > **[!UICONTROL Permiso efectivo]**, el **Permisos efectivos** el cuadro de diálogo no se abre en. (SITES-17378)

<!-- #### Classic UI{#sites-classicui-6521} 

* A -->

#### [!DNL Content Fragments]{#sites-contentfragments-6521}

* Se ha corregido la doble inclusión de los elementos del formulario. (SITES-21109)
* Al crear un fragmento de contenido, el botón Cerrar a veces no responde, lo que provoca que toda la página se congele y requiera una actualización de página para cerrar el fragmento de contenido. En cuanto al problema de creación de versiones, el sistema está creando una nueva versión de un fragmento de contenido. Este problema se produce incluso cuando el usuario no ha realizado ningún cambio, simplemente interactuando con el RTE o un campo de texto. (SITES-21187)

#### [!DNL Content Fragments] - API de GraphQL {#sites-graphql-api-6521}

* Al actualizar Adobe Experience Manager de 6.5.19.0 a 6.5.20.0, la ruta `/libs/cq/graphql/sites/graphiql` se estaba eliminando. (SITES-20098)

<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6521}

* W -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6521}

* W -->

<!-- #### Core Backend{#sites-core-backend-6521}

* W -->

<!-- #### Core Components{#sites-core-components-6521}

* I -->

<!-- #### Campaign integration{#sites-campaign-integration-6521}

* A -->

#### Fragmentos de experiencias{#sites-experiencefragments-6521}

* Despliegue de fragmentos de experiencias de `masters/language` hasta `country/language` no actualiza las referencias cruzadas. (SITES-21172)
* Plantillas no solo especificadas en `cq:allowedTemplates`, pero plantillas que tienen `allowedPaths` configuradas en el nivel de plantilla, aparecen como opciones al crear un nuevo Fragmento de experiencia. (SITES-20855)

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6521}

* T -->

<!-- #### Launches{#sites-launches-6521} -->

<!-- DELETED MAY 22, 2024 FROM TOTAL RELEASE CANDIDATE ISSUES * The `sourceRootResource` configured in the Launch configuration within CRXDE Lite points to content that no longer exists, leading to a malfunction when attempts are made to delete launches. Delete launches even if the page is deleted or if the path is not the same. (SITES-20750) -->

#### MSM: Live Copies{#sites-msm-live-copies-6521}

* Superponer el componente Página para agregar pestañas en las propiedades de página. Uno de ellos es la configuración de página y tiene una propiedad para agregar una URL de fragmento de experiencia. El vínculo configurado en las propiedades de página para el fragmento de experiencia no cambia para ninguna copia de idioma creada para esa página. El vínculo configurado debe cambiar con la URL de copia de idioma. (SITES-19580)

#### Editor de página{#sites-pageeditor-6521}

* El modo de edición aplica un fondo gris de forma incoherente, que no cumple con los estándares de contraste de color WCAG (Directrices de accesibilidad al contenido web). (SITES-20060)

### [!DNL Assets]{#assets-6521}

* Si se publica un recurso en Brand Portal, el estado de publicación sigue siendo incoherente. (ASSETS-36807)
* Los recursos no se eliminan al eliminarlos de una instancia mediante una llamada de API. (ASSETS-35131)
* Cuando intente importar metadatos, `question mark (?)` reemplaza la inserción de caracteres en cualquier idioma que no sea inglés.  (ASSETS-35091)
* Cuándo `dc:title` se utiliza con la cadena de tipo de datos, el árbol de contenido de recursos no funciona correctamente después de la instalación del Service Pack 6.5.19. (ASSETS-34684)
* Se muestra un error si hay algún carácter especial en el nombre de un recurso. (ASSETS-33248)

#### [!DNL Dynamic Media]{#assets-dm-6521}

* AEM En la versión 6.5.18, no muestra todas las zonas interactivas agregadas a un recurso al editar las zonas interactivas. Sin embargo, todos los puntos interactivos funcionan en un recurso publicado, pero no puede editarlos más adelante si es necesario. (ASSETS-33609)
* Los archivos EPS más recientes que se cargan no generan miniaturas después del reprocesamiento. (ASSETS-32617)
* En la pestaña Herramientas > Assets > Configuración de publicación de Dynamic Media > Atributos de solicitud, las entradas `Width(px)` y `Height(px)` tienen un aspecto diferente en español, italiano y portugués. No están alineadas entre sí en estas ubicaciones. (ASSETS-31896)
* A partir del 1 de mayo de 2024, Adobe Dynamic Media dejará de ofrecer asistencia para lo siguiente:
   * SSL (Secure Socket Layer) 2.0
   * SSL 3.0
   * TLS (Transport Layer Security) 1.0 y 1.1
   * Los siguientes cifrados débiles en TLS 1.2:
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

### [!DNL Forms]{#forms-6521}

Correcciones en [!DNL Experience Manager] Forms se entregan mediante un paquete de complementos independiente una semana después de lo programado [!DNL Experience Manager] Fecha de lanzamiento del paquete de servicio. AEM En este caso, el lanzamiento del paquete de complementos de Forms de la versión 6.5.21.0 está programado para el jueves, 13 de junio de 2024. Se ha añadido una lista de correcciones y mejoras de Forms a esta sección después de la versión.

<!-- #### [!DNL Adaptive Forms]

* THIS BUG WAS ALREADY REPORTED IN THE 6.5.20.0 RELEASE NOTES. IS IT NEEDED AGAIN IN THE 6.5.21.0 RELEASE NOTES? (AEM Forms on JEE Only) The PDF Generator service fails to enumerate the fonts available on the server. Consequently, the font selection panel on the Adobe PDF Settings page in the PDFG Admin UI remains empty, effectively preventing (un)embedding of chosen fonts. (FORMS-12095) -->


<!-- #### [!DNL Forms Designer] {#forms-designer-6521}

* W -->

### Foundation {#foundation-6521}

#### Apache Felix {#foundation-apachefelix-6521}

* AEM Problema de actualización con el paquete de servicio 19 (SP19) de 6.5 en el que falta la ruta raíz de contexto del servidor de aplicaciones para las solicitudes no autorizadas a Apache Felix después de la instalación de SP19. Actualización a la consola de administración web de Apache Felix 4.9.8. (NPR-41933)

#### Campaign{#foundation-campaign-6521}

* AEM El paquete de servicio 15 de.5 produce registros de errores continuos con entradas significativas. Se notificaron los siguientes problemas:

   * Error 404 INFO por falta de recurso en ruta `/libs/granite/ui/content/shell/start.html`
   * Entrada de registro de error para una excepción SlingException no detectada debido a `NullPointerException` en `CampaignsDataSourceServlet.java:147`

  AEM Los registros de errores no deben rellenarse con entradas de error frecuentes y voluminosas, y la instancia de error debe funcionar sin problemas relacionados con la falta de recursos o excepciones. (CQ-4357064)

#### Cloud Services{#foundation-cloudservices-6521}

* Quitar Google AEM Guava de los Cloud Service de la. (CQ-4356436)

<!-- #### Communities {#foundation-communities-6521}

* U -->

<!-- #### Content distribution{#foundation-content-distribution-6521}

* T -->

#### Granite{#foundation-granite-6521}

* No puede seleccionar **Eliminar** o **Modificar** sin **Examinar** en el Explorador de configuración. (GRANITE-51002)

#### Integraciones{#foundation-integrations-6521}

* Referente a `cq-target-integration`, debe eliminar el uso que no sea de prueba de Google Guava. (CQ-4357101)
* Reemplazo de credenciales de cuenta de servicio (token web JSON o JWT) con credenciales de servidor a servidor OAuth2 (también conocidas como entidades de seguridad de servicio). (NPR-41994)
* La creación de una solicitud de audiencia falla con la configuración de IMS (Identity Management System). (NPR-41888)
* Cuando un cliente intenta ver la página Carga útil, el contenido no se muestra correctamente debido a una dirección URL mal formada; se muestra un error 404. El error se debe a la falta de un signo de interrogación en la dirección URL, antes de los parámetros de la consulta. Este problema requiere que el cliente inserte el signo de interrogación para ver correctamente la página Carga útil. (NPR-41957)
* Elimine el código y la dependencia de la Search&amp;Promote AEM de Adobe de la versión 6.5 de, que llegó al final de su vida útil en la versión 6.5 de, que estaba en uso desde la versión 6.5. [Septiembre de 2022 según aviso](https://experienceleague.adobe.com/en/docs/discontinued/using/search-promote). (NPR-41855)

#### Localización{#foundation-localization-6521}

* En el editor Plantillas, la cadena de texto *`No video available.`* no está localizado. (SITES-13190)
* La cadena después de activar o desactivar un usuario no está localizada en **Herramientas** > **Seguridad** > **Usuarios** > *any_user_name* > **Activar** > **OK** y seleccione *any_user_name* > **Desactivar** > **OK**. (NPR-41737)

#### Plataforma{#foundation-platform-6521}

* El `Unclosed resource resolver` se está experimentando un error para `com.day.cq.mailer.impl.DefaultMailService`. El `MessageGatewayService` La clase, que está lista para usarse, se estaba utilizando sin un solucionador de recursos. El problema se producía en cualquier página con un botón de envío de formulario que envíe un correo electrónico con esta clase. (NPR-41853)
* En el **Acerca de Adobe Experience Manager** , el año de copyright sigue siendo 2023. (CQ-4356349)


<!-- #### Sling{#foundation-sling-6521}

* T -->

#### Traducción{#foundation-translation-6521}

* AEM Se ha producido un problema con el estado de la traducción predeterminada de la versión 6.5.19 de que no se actualizaba según lo esperado para un lanzamiento. AEM Después de importar un archivo traducido a un trabajo de traducción asociado con un lanzamiento de la, se esperaba que el estado cambiara a `Approved`. En su lugar, el estado cambió a `Ready for Review`, que no es el comportamiento esperado. (NPR-41756)
* Al crear varias configuraciones y acceder a las configuraciones de Cloud Service de traducción, no todos los elementos se muestran en la interfaz de usuario. Solo se muestran los 40 primeros elementos/carpeta; se activa la carga diferida, pero no se añade más contenido. (NPR-41829)
* Los caracteres ilegibles se producen si hay japonés en la página Permisos de la interfaz de usuario táctil. (NPR-41794)
* AEM Las versiones 6.5.14 y 6.5.9 no envían un emoji para su traducción. (CQ-4357000)

#### Interfaz de usuario{#foundation-ui-6521}

* En Herramientas > Seguridad > Usuarios > &lt;user_name> > Perfiles, en la **Editar configuración de usuario** , al hacer clic en Cancelar no se sale del cuadro de diálogo. (NPR-41793)
* El Granito `pathfield` componente en `/libs/granite/ui/components/coral/foundation/form/pathfield` no se puede habilitar el **[!UICONTROL Seleccionar]** cuando se selecciona un recurso. Una vez que aparece el campo de ruta y el usuario selecciona la casilla de verificación del recurso, la variable **[!UICONTROL Seleccionar]** El botón no está habilitado; no cambia de gris a azul. (NPR-41970)
* AEM Existe un problema con el campo de referencia del Modelo de fragmento de contenido (CFM) en la aplicación de la versión de la aplicación de la versión de la aplicación de la versión de. A pesar de que el campo de referencia CFM se ha establecido como obligatorio, el sistema permite a los usuarios hacer clic en Guardar para guardar contenido con valores que no sean CFM en determinados escenarios. El botón Guardar debe estar atenuado (no disponible). (NPR-41894)
* Los cuadros de diálogo estándar de la interfaz de usuario de Coral que utilizan la variable `successresponse` La acción debe almacenar en déclencheur una respuesta de éxito después de la acción. AEM Sin embargo, en el paquete de servicio 19 de 6.5, la acción de recarga no se invoca y no se muestra ningún mensaje. (NPR-41797)
* AEM AEM Los vínculos de notificaciones de no funcionan en el paquete de servicio 18 de la versión 6.5 de la versión. AEM Al actualizar a Service Pack 18, los vínculos de notificaciones de la no funcionan al seleccionar los mensajes mediante el botón de notificaciones. (NPR-41792)

<!-- #### WCM{#foundation-wcm-6521}

* T -->

#### Flujo de trabajo{#foundation-workflow-6521}

* AEM En la versión 6.5.18, se han repetido errores al eliminar de la caché de metadatos del usuario durante la depuración. (NPR-41762)

## Instalar [!DNL Experience Manager] 6.5.21.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.21.0 requiere [!DNL Experience Manager] 6.5. Véase [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas. <!-- UPDATE FOR EACH NEW RELEASE -->
* La descarga del paquete de servicio está disponible en el Adobe [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip).
* En una implementación con MongoDB y varias instancias, instale [!DNL Experience Manager] 6.5.21.0 en una de las instancias de autor mediante el Administrador de paquetes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> El Adobe no recomienda quitar ni desinstalar el [!DNL Experience Manager] Paquete de 6.5.21.0. Como tal, antes de instalar el paquete, debe crear una copia de seguridad del `crx-repository` en caso de que deba revertirlo. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Instalación del paquete de servicio en [!DNL Experience Manager] 6,5{#install-service-pack}

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (cuando la instancia se haya actualizado desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de realizar la instalación, tome una instantánea o realice una copia de seguridad nueva de su [!DNL Experience Manager] ejemplo.

1. Descargue el Service Sack de [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra el Administrador de paquetes y seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y luego seleccione **[!UICONTROL Instalar]**.

1. Para actualizar el conector S3, detenga la instancia después de la instalación del Service Pack, sustituya el conector existente por un nuevo archivo binario proporcionado en la carpeta de instalación y reinicie la instancia. Consulte [Almacén de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo en la interfaz de usuario del administrador de paquetes a veces existe durante la instalación del paquete de servicio. El Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete actualizador antes de asegurarse de que la instalación se haya realizado correctamente. Normalmente, este problema se produce en el [!DNL Safari] explorador, pero puede producirse de forma intermitente en cualquier explorador.

**Instalación automática**

Existen dos métodos diferentes que puede utilizar para instalar [!DNL Experience Manager] 6.5.21.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en `../crx-quickstart/install` cuando el servidor está disponible en línea. El paquete se instala automáticamente.
* Utilice el [API HTTP del Administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Uso `cmd=install&recursive=true` para instalar los paquetes anidados.

>[!NOTE]
>
>Experience Manager 6.5.21.0 no admite la instalación de Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validación de la instalación**

Para conocer las plataformas certificadas para trabajar con esta versión, consulte la [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.21.0)` bajo [!UICONTROL Productos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos los paquetes OSGi son **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web): `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.20 o posterior de (utilice la consola web: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Instalar Service Pack para [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Para obtener instrucciones para instalar el Service Pack en Experience Manager Forms, consulte [Instrucciones de instalación del Service Pack de Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La funcionalidad Formularios adaptables, disponible en [AEM 6.5 Inicio rápido](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), está diseñada únicamente para la exploración y la evaluación. Para su uso en producción, es esencial obtener una licencia válida para AEM Forms, ya que la funcionalidad Formularios adaptables requiere una licencia adecuada.

### Instalación del paquete de índice de GraphQL para fragmentos de contenido de Experience Manager{#install-aem-graphql-index-add-on-package}

Los clientes que utilicen GraphQL deben instalar [Fragmento de contenido de Experience Manager con el paquete de índice 1.1.1 de GraphQL](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Al hacerlo, puede añadir la definición de índice necesaria en función de las funciones que utilizan realmente.

Si no se instala este paquete, las consultas de GraphQL pueden ser lentas o dar error.

>[!NOTE]
>
>Instale este paquete solo una vez por instancia; no es necesario reinstalarlo con cada Service Pack.

### UberJar{#uber-jar}

UberJar para [!DNL Experience Manager] 6.5.21.0 está disponible en la [Repositorio de Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.21/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para usar UberJar en un proyecto de Maven, consulte [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.21</version>
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

* Al intentar mover, eliminar o publicar fragmentos de contenido, sitios o páginas, hay un problema cuando se recuperan las referencias de fragmentos de contenido. La consulta en segundo plano falla. Es decir, la funcionalidad no funciona.
Para garantizar un funcionamiento correcto, debe agregar las siguientes propiedades al nodo de definición del índice `/oak:index/damAssetLucene` (no se requiere reindexación):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Si actualiza su [!DNL Experience Manager] instancia de 6.5.0 a 6.5.4 con el último Service Pack en Java™ 11, verá lo siguiente `RRD4JReporter` excepciones en la `error.log` archivo. Para detener las excepciones, reinicie la instancia de [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Los usuarios pueden cambiar el nombre de una carpeta en una jerarquía en [!DNL Assets] y publicar una carpeta anidada en [!DNL Brand Portal]. Sin embargo, el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Durante la instalación de, se pueden mostrar los siguientes errores y mensajes de advertencia [!DNL Experience Manager] 6.5.x.x:
   * &quot;Cuando la integración de Adobe Target está configurada en [!DNL Experience Manager] Si se utiliza la API de Target Standard (autenticación IMS) y se exportan los fragmentos de experiencias a Target, se crean tipos de ofertas incorrectos. En lugar de &quot;Fragmento de experiencia&quot;/fuente &quot;Adobe Experience Manager&quot;, Target crea varias ofertas con el tipo &quot;HTML&quot;/fuente &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: No se han encontrado ventanas de mantenimiento en granite/operations/maintenance.
   * La validación del lado del servidor de formularios adaptables falla cuando se utilizan funciones de agregado como SUM, MAX y MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : No se han encontrado ventanas de mantenimiento en granite/operations/maintenance.
   * El punto interactivo de una imagen interactiva de Dynamic Media no está visible al obtener una vista previa del recurso a través del visor de titulares de ventas.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : tiempo de espera hasta que se completó el cambio de registro sin registrar.

* AEM A partir de la versión 6.5.15, el motor JavaScript de Rhino proporcionado por el ```org.apache.servicemix.bundles.rhino``` El paquete tiene un nuevo comportamiento de elevación. Scripts que utilizan el modo estricto (```use strict;```) deben declarar sus variables correctas. De lo contrario, no se ejecutan y terminan generando un error de tiempo de ejecución.

* La instalación del etiquetado del contenido relacionado listo para usar mediante un paquete de actualización oficial restablece la propiedad de idiomas del `/content/cq:tags` de forma predeterminada. Esta acción se aplica a los paquetes de servicio, los paquetes de servicio de seguridad, los paquetes de funciones ampliadas, los paquetes de funciones acumulativas, los parches, etc. Por lo tanto, es necesario agregarlo desde las propiedades antes de la instalación.

### Problema conocido de AEM Sites {#known-issues-aem-sites-6521}

* SITES-17934 - Fragmentos de contenido - La vista previa falla debido a la protección DoS para un árbol grande de fragmentos. Consulte la [Artículo de KB sobre las opciones de configuración predeterminadas del ejecutor de consultas de GraphQL](https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-23945)

### Problemas conocidos de AEM Forms {#known-issues-aem-forms-6521}

* En un formulario adaptable basado en un XDP con scripts incrustados en casillas de verificación, los scripts no se ejecutan para elementos después de esas casillas de verificación. (FORMS-14244)
* Los usuarios no pueden crear una carta de Administración de correspondencia. Cuando un usuario crea una carta, aparece un error con la descripción &quot;`Object Object`&quot; y no se crea la carta. Las miniaturas de los diseños tampoco se pueden cargar en la pantalla de creación de cartas. Puede instalar el [AEM Paquete de servicio de formulario 20 más reciente de 6.5 (6.5.20.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) para resolver el problema. (FORMS-13496)
* El servicio de comunicaciones interactivas crea el documento del PDF, pero los datos del usuario no se rellenan automáticamente en los campos del formulario. El servicio de relleno previo no funciona como se esperaba. Puede instalar el [AEM Paquete de servicio de formulario 20 más reciente de 6.5 (6.5.20.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) para resolver el problema. (FORMS-13413, FORMS-13493)
* El editor de revisión y corrección (RnC) de un servicio de automated forms conversion no se puede cargar. Puede instalar el [AEM Paquete de servicio de formulario 20 más reciente de 6.5 (6.5.20.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) para resolver el problema. (FORMS-13491)
* AEM Forms AEM Después de actualizar del paquete de servicio 18 (6.5.18.0) o el paquete de servicio 19 (6.5.19.0) de Forms AEM 6.5 a paquete de servicio 20 (6.5.20.0) de Forms 6.5, los usuarios se toparán con un error de compilación de JSP. AEM No pueden abrir ni crear formularios adaptables y están experimentando errores con otras interfaces de usuario, como el editor de páginas, la interfaz de usuario de AEM Forms AEM y el editor de flujo de trabajo de la. Puede instalar el [AEM Paquete de servicio de formulario 20 más reciente de 6.5 (6.5.20.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) para resolver el problema. (FORMS-13492)
* Las filas del widget selector de fechas se truncan al recorrer meses en el widget emergente de los campos con el patrón Editar/Mostrar. (FORMS-13620)
* Los envíos de formularios fallan al intentar utilizar el servicio DOR (documento de registro) en el backend. El mensaje de error encontrado es: &quot;No se pudo completar la acción de envío porque el recurso de formulario no se ha asignado correctamente&quot;. (FORMS-13798)
* Cuando se envía un formulario adaptable desde una instancia de publicación de Adobe Experience Manager a un flujo de trabajo de Adobe Experience Manager, el flujo de trabajo no puede guardar los archivos adjuntos. (FORMS-14209)
* AEM Al instalar el paquete de servicio 20 de Forms 6.5 de la interfaz de usuario (IU) de AEM Sites (paquete de complemento de AEM Forms para SP20), se produce una degradación significativa del rendimiento. (FORMS-13791)
* El servicio de relleno previo falla con una excepción de puntero nulo en las comunicaciones interactivas. (CQDOC-21355)
* Las Forms adaptables permiten utilizar funciones personalizadas con ECMAScript versión 5 o anteriores. Cuando una función personalizada utiliza ECMAScript versión 6 o posterior, como `let`, `const`, o funciones de flecha, es posible que el editor de reglas no se abra correctamente.

## Paquetes de contenido y paquetes OSGi incluidos{#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en esta [!DNL Experience Manager] Versión del paquete de servicio 6.5:

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.21.0](/help/release-notes/assets/65210-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.21.0](/help/release-notes/assets/65210-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sitios web restringidos{#restricted-sites}

Estos sitios web solo están disponibles para los clientes de. Si es cliente de y necesita acceso, póngase en contacto con el administrador de cuentas de Adobe de.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/)
* [Contactar con Atención al cliente de Adobe](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página de producto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html?lang=es)
>* [[!DNL Experience Manager] Documentación de 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [Suscribirse a las actualizaciones de productos prioritarias de Adobe](https://www.adobe.com/subscription/priority-product-update.html)

