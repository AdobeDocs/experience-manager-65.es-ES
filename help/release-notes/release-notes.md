---
title: Notas de la versión para [!DNL Adobe Experience Manager] 6,5
description: Encuentre información de la versión, novedades, instrucciones de instalación y una lista de cambios detallada para [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
source-git-commit: 210299acf9f853a19bd513c84c1678e44ba81729
workflow-type: tm+mt
source-wordcount: '2456'
ht-degree: 2%

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
| Versión | 6.5.20.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versión del paquete de servicio |
| Fecha | Jueves, 22 de febrero de 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## ¿Qué incluye? [!DNL Experience Manager] 6.5.20.0 {#what-is-included-in-aem-6520}

[!DNL Experience Manager] 6.5.20.0 incluye nuevas funciones, mejoras clave solicitadas por el cliente, correcciones de errores y mejoras de rendimiento, estabilidad y seguridad que se han publicado desde la publicación inicial de 6.5 en abril de 2019. [Instalar este Service Pack](#install) el [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Funciones principales y mejoras

<!-- * _6.5.20.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Algunas de las funciones y mejoras clave de esta versión son las siguientes:

* Dynamic Media ahora es compatible con el formato de imagen HEIC sin pérdidas para Apple iOS/iPadOS. Consulte [fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html?lang=en) en la API de servicio y procesamiento de imágenes de Dynamic Media.

* El Administrador de varios sitios (MSM) ahora es compatible con estructuras de fragmentos de experiencias, incluidas carpetas y subcarpetas, para un despliegue masivo eficaz de fragmentos de experiencias en Live Copies.

<!-- ### [!DNL Forms]

* text -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Se han corregido problemas en el Service Pack 20 {#fixed-issues}

### [!DNL Sites]{#sites-6520}

<!--#### Accessibility{#sites-accessibility-6520}

* text -->

#### Interfaz de usuario de administrador{#sites-adminui-6520}

* El `Workflow Title` el campo está marcado con `*` según sea necesario, pero no hay validación. (SITES-16491)

<!--#### Classic UI{#sites-classicui-6520}

* text -->

#### [!DNL Content Fragments]{#sites-contentfragments-6520}

* AEM AEM Ya no se admitían carpetas de configuración anidadas y las carpetas del modelo de fragmento de contenido dejaron de ser visibles después de actualizar a la versión 6.5.18 o a la versión 6.5.19 de la versión 6.18 o la versión 6.5.19 de la versión. (SITES-18110)
* Algunas subcarpetas no pueden elegir entre los modelos de fragmento de contenido heredados. Debe admitir carpetas sin tener un `jcr:content` , incluso si las carpetas DAM creadas mediante la interfaz de usuario tienen un nodo de este tipo. (SITES-17943)

#### [!DNL Content Fragments] - API de GraphQL {#sites-graphql-api-6520}

<!-- REMOVED AS PER EMAIL FROM SAMEER DHAWAN FEBRUARY 19, 2024 * When upgrading AEM from 6.5.19.0 to 6.5.20.0, the path `/libs/cq/graphql/sites/graphiql` was getting deleted. (SITES-19530) CRITICAL -->
* Al ejecutar una consulta de GraphQL en [filtrar resultados](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#filtering) mediante variables opcionales, si un valor específico es **no** Cuando se proporciona para la variable opcional, la variable se omite en la evaluación de filtros. (SITES-17051)

<!--#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6520}

* text -->

#### [!DNL Content Fragments] - API DE REST{#sites-restapi-6520}

* Con la actualización del `org.json` biblioteca, se ha producido un cambio en la forma en que se deserializaban los números decimales. Antes se convertían &quot;por defecto&quot; en Dobles y ahora en BigDecimals. En su lugar, los valores de las propiedades de metadatos, almacenados mediante la API de REST, deben convertirse a Double a partir de BigDecimal. (SITES-16857)

#### Servidor principal{#sites-core-backend-6520}

* Cuando se utiliza la publicación rápida de un fragmento de contenido, continúa cargándose y no se publica. AEM AEM Es decir, Publicación rápida no funciona para los fragmentos de contenido después de una actualización de Service Pack de la versión 6.5.7 a la versión 6.5.17 de la versión de. Cuando el usuario intentó la publicación administrada, funcionó. Sin embargo, cuando intentaron Publicación rápida, no se estaba publicando. Específicamente, `com.day.cq.wcm.core.impl.reference.ActivationReferenceSearchBuilder` causó que el sistema se golpeara. (SITES-17311)
* Los fragmentos de contenido no se pueden serializar con el exportador Jackson: La carga de la página se interrumpe cuando hay un fragmento de contenido al que se hace referencia en una página (utiliza el código del exportador Jackson) y cualquier etiqueta agregada a un fragmento de contenido. (SITES-18096)

#### Componentes principales{#sites-core-components-6520}

* CIF AEM Instalación del paquete de componentes principales en las causas de la `:type` Valor de los componentes existentes que se van a cambiar. El cambio significa que ya no se representan en las páginas a las que se han agregado. (SITES-17601)

#### Integración de Campaign{#sites-campaign-integration-6520}

* AEM estaba usando una lista de permitidos, también conocida como `whitelist`- debido a un informe de vulnerabilidad. La lista de permitidos impedía a los clientes utilizar la funcionalidad necesaria. (SITES-16822)

#### Fragmentos de experiencias{#sites-experiencefragments-6520}

* MSM para fragmentos de experiencias ahora admite el despliegue masivo a estructuras de contenido de fragmentos de experiencias, incluidas carpetas y subcarpetas. (SITES-16004)

<!--#### Foundation Components (Legacy){#sites-foundation-components-legacy-6520}

* text

#### Launches{#sites-launches-6520}

* text -->

#### MSM: Live Copies{#sites-msm-live-copies-6520}

* Un &quot;`Is not modifiable`Se produce una excepción &quot; al desplegar el componente. Específicamente, una `org.apache.sling.servlets.post.impl.operations.ModifyOperation` se experimenta una excepción durante el procesamiento de respuestas. (SITES-18809)
* No se pueden desplegar cambios en Live Copies específicas de fragmentos de experiencias. (SITES-17930)
* Cuando un usuario agrega una anotación a un componente en una página de modelo y luego la despliega, el recuento de anotaciones en Live Copy se muestra incorrectamente. (SITES-17099)
* El botón Despliegue de MSM de la página principal a la página secundaria se interrumpe en la interfaz gráfica de usuario táctil; cuando se selecciona, se muestra el siguiente error: `Uncaught TypeError: _g.shared is undefined`. (SITES-16991)

#### Editor de página{#sites-pageeditor-6520}

* La vista previa del editor de temáticas Forms está dañada. Cuando se selecciona Vista previa, solo está visible un icono de carga. (SITES-17164)

### [!DNL Assets]{#assets-6520}

* No se pueden validar los campos basados en reglas en el asistente del editor de metadatos. Aparece el mensaje de error &quot;Faltan campos obligatorios&quot;. (ASSETS-31396)
* Después de mover un PDF a otra ubicación, la variable **[!UICONTROL Ver página]** La opción desaparece. (ASSETS-30538)
* No se puede seleccionar una imagen con permisos de lectura. (ASSETS-32199)
* No se puede cambiar el tamaño de la tarjeta en la configuración de vista. (ASSETS-31667)
* Se produce un error al cargar el tipo de archivo .oft. (ASSETS-30109)
* Cuando intenta agregar un campo de metadatos personalizado como una columna adicional al informe, las casillas de verificación no están seleccionadas. (ASSETS-31671)
* La operación de movimiento de recursos no funciona correctamente en el paquete de servicio 16 de Experience Manager. (ASSETS-30598)

#### [!DNL Dynamic Media]{#assets-dm-6520}

* AEM Cuando se carga un recurso en la interfaz de usuario de, la variable `Update_asset` flujo de trabajo activado. Sin embargo, el flujo de trabajo nunca termina. El flujo de trabajo solo finaliza hasta el paso de carga del producto. El siguiente paso es la carga por lotes de Scene7 AEM, pero ese proceso no se está incorporando a la fase de carga por lotes de los recursos de la red de distribución de datos de. (ASSETS-30443)
* Necesita una forma mejor de gestionar correctamente los vídeos que no son de Dynamic Media en el componente Dynamic Media. Este problema creaba una excepción al crear una instancia de `dynamicmedia_sly.js`. (ASSETS-31301)
* La vista previa funciona para todos los recursos, conjuntos de vídeos adaptables y vídeos. Sin embargo, genera un error 403 para `.m3u8` archivos (que, por cierto, siguen funcionando mediante vínculos públicos). (ASSETS-31882)
* El `scene7SmartCropProcessingStatus` estado corregido. Los metadatos de vídeo de recorte inteligente se utilizaban para mostrar errores incluso si se habían realizado correctamente. (ASSETS-31255)

### [!DNL Forms]{#forms-6520}

Correcciones en [!DNL Experience Manager] Forms se entregan mediante un paquete de complementos independiente una semana después de lo programado [!DNL Experience Manager] Fecha de lanzamiento del paquete de servicio. AEM En este caso, el lanzamiento del paquete de complementos de Forms de la versión 6.5.20.0 está programado para el jueves, 29 de febrero de 2024. Se ha añadido una lista de correcciones y mejoras de Forms a esta sección después de la versión.

<!-- #### [!DNL Adaptive Forms] -->

<!--LEFT BULLET LIST HERE IN CASE OF REUSE BY FORMS IN THE FUTURE 
* **Document Services**
  * text
* **Adaptive Forms** 
  * text
* **Accessibility**
  * text
* **Interactive Communications**
  * text -->

<!--### Commerce{#commerce-6520}

* text -->

### Foundation {#foundation-6520}

#### Communities {#communities-6520}

* Los diagnósticos de sincronización de usuarios fallan después de configurar correctamente la sincronización de usuarios. (NPR-41693)

<!-- #### Content distribution{#foundation-content-distribution-6520}

* text -->

#### Integraciones{#integrations-6520}

* Elimine todo el código y las dependencias de la Search&amp;Promote AEM de Adobe de la versión 6.5 de. (NPR-40856)

#### Localización{#localization-6520}

* La etiqueta Aria &quot;close&quot; no está localizada en **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**, seleccione una carpeta y, en la barra de herramientas, seleccione **[!UICONTROL Propiedades]** > **[!UICONTROL Permisos]** pestaña > nombre del miembro. (NPR-41705)
* Hay una información de objeto truncada para **[!UICONTROL Contraseña de almacén de claves]** en la página Configuración SSL para las configuraciones regionales ENG, FRA, KOR, DEU y PTB. (NPR-41367)

#### Plataforma{#foundation-platform-6520}

* AEM Problema con la integración de Campaign con los recursos causados por el servlet /api, que no devuelven el esquema correcto en el json href. AEM El motivo era que no estaba recibiendo el encabezado X-Forward-Proto, lo que obligaba a que la solicitud respondiera con un esquema HTTP en lugar de HTTPS. Como tal, se debe añadir la capacidad de alternar la selección de esquemas en función de una configuración OSGI. (GRANITE-48454)

#### Sling{#foundation-sling-6520}

* El `org.apache.sling.resourceMerger` AEM el paquete 1.4.2 genera una excepción con respecto a la versión 6.5, el paquete de servicio 17 y posteriores de. La fusión de recursos de Sling 1.4.4 debe incluirse en el paquete de servicio 20. (NPR-41630)

#### Traducción{#foundation-translation-6520}

* AEM Después de la implementación del paquete de servicio 18 de 6.5, se produjo un problema con la pestaña Filtros en el Editor de reglas de traducción. Cuando se selecciona un Contexto, al hacer clic en Editar > Guardar, la próxima vez que abra el mismo Contexto aparecerá un carácter de comillas dobles como HTML. Básicamente, las reglas de traducción no se guardaban correctamente. (NPR-41624)
* AEM Problemas relacionados con las traducciones de fragmentos de contenido, en las que las cadenas traducidas se envían de vuelta del proveedor de traducción a la, pero se quedan en el `/content/projects` y no actualizar los fragmentos de contenido. (NPR-41516)
* Se muestra un mensaje de error al crear una copia de idioma. Se produce en una página que tiene un fragmento de contenido referenciado en una propiedad de página mediante modelos de fragmento de contenido. (NPR-41441)
* Los vínculos de los fragmentos de experiencias no se ajustan al idioma correcto durante la copia de idioma. En su lugar, el fragmento de experiencia apunta a la configuración regional principal. (NPR-41343)

#### Interfaz de usuario{#foundation-ui-6520}

* AEM El error de la consola se experimenta después de una actualización al paquete de servicio 18 de la versión 6.5 de la. El error se encuentra en `coralUI3.js` AEM y se produce al seleccionar cualquier lista desplegable en la lista de elementos de la lista de elementos de la lista de archivos. Específicamente, sucede con un `onOverlayToggle` evento. El error `Uncaught TypeError: Cannot read properties of null (reading 'innerText')` se muestra. (NPR-41467)
* AEM En el **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL Etiquetado]** > **[!UICONTROL Crear]** > **[!UICONTROL Crear etiqueta]**, introduciendo caracteres no latinos en **Título** El campo causa el **Nombre** campo que se va a rellenar solo con el carácter de guión ( `-` ). (NPR-41623)
* El año de copyright es incorrecto en `About Adobe Experience Manager` Cuadro de diálogo. (NPR-41526)
* Hay elementos sin traducir **[!UICONTROL Propiedades de perfil]** cadenas al editar la configuración de usuario. Ocurre en todas las configuraciones regionales. (NPR-41365)

<!-- #### WCM{#wcm-6520}

* text

#### Workflow{#foundation-workflow-6520}

* text -->

## Instalar [!DNL Experience Manager] 6.5.20.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.20.0 requiere [!DNL Experience Manager] 6.5. Véase [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas. <!-- UPDATE FOR EACH NEW RELEASE -->
* La descarga del Service Pack está disponible en el Adobe [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip).
* En una implementación con MongoDB y varias instancias, instale [!DNL Experience Manager] 6.5.20.0 en una de las instancias de autor mediante el Administrador de paquetes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> El Adobe no recomienda quitar ni desinstalar el [!DNL Experience Manager] Paquete de 6.5.20.0. Como tal, antes de instalar el paquete, debe crear una copia de seguridad del `crx-repository` en caso de que deba revertirlo. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Instalación del Service Pack en [!DNL Experience Manager] 6,5{#install-service-pack}

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (cuando la instancia se haya actualizado desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de realizar la instalación, tome una instantánea o realice una copia de seguridad nueva de su [!DNL Experience Manager] ejemplo.

1. Descargue el Service Pack desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra el Administrador de paquetes y seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y luego seleccione **[!UICONTROL Instalar]**.

1. Para actualizar el conector S3, detenga la instancia después de la instalación del Service Pack, sustituya el conector existente por un nuevo archivo binario proporcionado en la carpeta de instalación y reinicie la instancia. Consulte [Almacén de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo en la interfaz de usuario del Administrador de paquetes a veces existe durante la instalación del Service Pack. El Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete actualizador antes de asegurarse de que la instalación se haya realizado correctamente. Normalmente, este problema se produce en el [!DNL Safari] explorador, pero puede producirse de forma intermitente en cualquier explorador.

**Instalación automática**

Existen dos métodos diferentes que puede utilizar para instalar automáticamente [!DNL Experience Manager] 6.5.20.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en `../crx-quickstart/install` cuando el servidor está disponible en línea. El paquete se instala automáticamente.
* Utilice el [API HTTP del Administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Uso `cmd=install&recursive=true` para instalar los paquetes anidados.

>[!NOTE]
>
>Experience Manager 6.5.20.0 no admite la instalación de Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validación de la instalación**

Para conocer las plataformas certificadas para trabajar con esta versión, consulte la [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.20.0)` bajo [!UICONTROL Productos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos los paquetes OSGi son **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web): `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.18 o posterior de (utilice la consola web: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Instalar Service Pack para [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Para obtener instrucciones para instalar el Service Pack en Experience Manager Forms, consulte [Instrucciones de instalación del Service Pack de Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La funcionalidad Formularios adaptables, disponible en [AEM 6.5 Inicio rápido](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/deploying/deploy.html), está diseñada únicamente para la exploración y la evaluación. Para su uso en producción, es esencial obtener una licencia válida para AEM Forms, ya que la funcionalidad Formularios adaptables requiere una licencia adecuada.

### Instalación del paquete de índice de GraphQL para fragmentos de contenido de Experience Manager{#install-aem-graphql-index-add-on-package}

Los clientes que utilicen GraphQL deben instalar [Fragmento de contenido de Experience Manager con el paquete de índice 1.1.1 de GraphQL](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Al hacerlo, puede añadir la definición de índice necesaria en función de las funciones que utilizan realmente.

Si no se instala este paquete, las consultas de GraphQL pueden ser lentas o dar error.

>[!NOTE]
>
>Instale este paquete solo una vez por instancia; no es necesario reinstalarlo con cada Service Pack.

### UberJar{#uber-jar}

UberJar para [!DNL Experience Manager] 6.5.20.0 está disponible en la [Repositorio de Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.20/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para usar UberJar en un proyecto de Maven, consulte [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.20</version>
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

Problemas conocidos de [!DNL Experience Manager] Forms se entregan mediante un paquete de complementos independiente una semana después de lo programado [!DNL Experience Manager] Fecha de lanzamiento del paquete de servicio. AEM En este caso, el lanzamiento del paquete de complementos de Forms de la versión 6.5.20.0 está programado para el jueves, 29 de febrero de 2024. Se ha añadido una lista de problemas conocidos de los formularios a esta sección después de la versión.

<!--

#### Supported platforms 

* JDK 11.0.20 is not supported to install AEM Forms on JEE Installer. Only JDK 11.0.19 or earlier versions are supported to install AEM Forms on JEE Installer. (FORMS-10659)

#### Installation 

* On JBoss&reg; 7.1.4 platform, when user installs Experience Manager 6.5.16.0 or later service pack, `adobe-livecycle-jboss.ear` deployment fails. (CQ-4351522, CQDOC-20159)

<!-- 
* After upgrading to AEM Forms 6.5.18.0 JBoss&reg; Turnkey full installer environment on Windows Server 2022, when compiling Output client application code using Java&trade; 11, the following compilation error may occur:
  
  ```
  error: error reading [AEM_Forms_Installation_dir]\sdk\client-libs\common\adobe-output-client.jar; java.net.URISyntaxException: 
  Illegal character in path at index 70: file:/[AEM_Forms_Installation_dir]/sdk/client-libs/common/${clover.jar.name} 1 error
  
  ```
  
  To resolve the issue, perform the following steps:
    1. Navigate to `[AEM_Forms_Installation_dir]\sdk\client-libs\common\` and unzip `adobe-output-client.jar` to extract the `Manifest.mf` file.
    1. Update the `Manifest.mf` file by removing the entry `${clover.jar.name}` from the class-path attribute. 

        >[!NOTE]
        >
        > You can also use an in-place editing tool, for example, 7-zip, to update the `Manifest.mf` file.  

    1. Save the updated the `Manifest.mf` in the `adobe-output-client.jar` archive. 
    1. Save the modified `adobe-output-client.jar` file and rerun the setup. (CQDOC-20878) 

* After installing AEM Service Pack 6.5.20.0 full installer, the EAR deployment fails on JEE using JBoss&reg; Turnkey. UPDATE FOR EACH NEW RELEASE To resolve the issue, locate the AEM_Forms_Installation_dir\jboss\bin\standalone.bat file and update `Adobe_Adobe_JAVA_HOME` to `Adobe_JAVA_HOME` for all occurrences before running the configuration manager. (CQDOC-20803).

#### Install the servlet fragment (AEM Service Pack 6.5.14.0 or earlier)

* If you are upgrading to AEM Service Pack 6.5.15.0 or higher, and your AEM instance is operating on Tomcat 8.5.88, it is mandatory that you install the servlet fragment. Do this install *before* you proceed with the installation of Service Pack 6.5.15.0 or higher.
* It is mandatory that you install the servlet fragment for all application servers except those running on JBoss&reg; EAP 7.4.0.

**To install the servlet fragment:**

1. Download the servlet fragment from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).
1. Start the application server. 
1. Wait for the logs to stabilize and check the bundle state.
1. Open Web Console Bundles. The default URL is `http://[Server]:[Port]/system/console/bundles`.
1. Select **[!UICONTROL Install]** or **[!UICONTROL Update]**. 
1. Select the downloaded fragment 
`org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar` 
1. Select **[!UICONTROL Install]** or **[!UICONTROL Update]**. 
1. Wait for the application server to stabilize.
1. Stop the application server.

#### Adaptive Forms

* When an Adaptive Form is published, all its dependencies, including policies, get republished, even if no modifications have been made to them. (FORMS-10454)
* When a user selects to configure a field for the first time in an adaptive form, the option to save a configuration does not display in Properties Browser. Selecting to configure some other field of the Adaptive Form in the same editor resolves the issue. 
* When users perform the submit action, the submission fails with an error: 
`javax.servlet.ServletException: java.lang.NoSuchMethodError`
To resolve the issue, [recompile the Sling scripts such as JSP, Java&trade;, and Sightly](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html#resolution). (FORMS-8542)
* After installing AEM Service Pack 6.5.14.0 and onwards, users are unable to select a font from the JEE Admin UI for PDF documents when navigating to `Home` > `Services` > `PDF Generator` > `Adobe PDF Settings`, as the font list appears empty. (FORMS-12095)
 When a form is signed using the OOTB Scribble Signature component, it appears in the image dialogue but does not preview and appears blank when you click on it. (FORMS-12073). A hotfix is available for this issue. To download and install the hotfix, see [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md) 
* On AEM Forms on JEE, the HTML5 Forms that use the context path, fail to render. (FORMS-12485, FORMS-12691). A hotfix is available for this issue. To download and install the hotfix, see [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md).
* Adaptive Forms let you use custom functions with ECMAScript version 5 or earlier. When a custom function uses ECMAScript version 6 or later, like 'let', 'const', or arrow functions, the rule editor might not open properly.

#### AEM Forms on JEE 

* Critical security vulnerabilities have been reported for Struts 2 RCE, a popular and open-source web application framework for developing Java&trade; EE web applications. Adobe has released [AEM 6.5 Service Pack 19.1 (6.5.19.1)](/help/forms/using/mitigating-struts-2-rce-vulnerabilities-for-experience-manager-manager-form.md) to address the vulnerability in AEM Forms on JEE. 

The font enumeration fails due to the missing Ps2Pdf service file.-->

## Paquetes de contenido y paquetes OSGi incluidos{#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en esta [!DNL Experience Manager] Versión del paquete de servicio 6.5:

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.20.0](/help/release-notes/assets/65200-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.20.0](/help/release-notes/assets/65200-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sitios web restringidos{#restricted-sites}

Estos sitios web solo están disponibles para los clientes de. Si es cliente de y necesita acceso, póngase en contacto con el administrador de cuentas de Adobe de.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/)
* [Contactar con Atención al cliente de Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página de producto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentación de 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es)
>* [Suscribirse a las actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html)
