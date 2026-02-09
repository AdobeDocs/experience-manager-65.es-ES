---
title: Funciones obsoletas y eliminadas en la versión 6.5 de Adobe Experience Manager.
description: Notas de la versión específicas de las funciones en desuso y eliminadas de Adobe Experience Manager 6.5.
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
source-git-commit: 30137e36b60c3ada70240e1442390f9fdd26f3b9
workflow-type: tm+mt
source-wordcount: '1771'
ht-degree: 100%

---

# Funciones en desuso y eliminadas {#deprecated-and-removed-features}

<!-- Search&Promote is end-of-life September 1, 2022 | Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Honor the access control setup of user and ensure appropriate permissions. ||
|Adobe Search & Promote|The integration with Adobe Search & Promote is deprecated. Adobe does not plan to make further enhancements to the Search & Promote integration. Adobe Search & Promote integration remains fully supported while being deprecated.||| -->

Adobe evalúa constantemente las capacidades de los productos para renovar o sustituir las funciones más antiguas con alternativas modernas que mejoren el valor general del cliente, siempre teniendo en cuenta la compatibilidad con versiones anteriores.

Para comunicar la inminente eliminación o sustitución de las funciones de Adobe Experience Manager (AEM), se aplican las siguientes reglas:

1. Primero se anuncia el desuso. Aunque están en desuso, las funciones siguen estando disponibles, pero no se siguen mejorando.
1. La eliminación de las funciones en desuso se produce en la siguiente versión principal como pronto. La fecha objetivo real para la eliminación se anunciará más adelante.

Este proceso proporciona a los clientes un ciclo de lanzamiento para adaptar su implementación a una nueva versión o a la siguiente versión de una capacidad en desuso, antes de eliminarla.

## Funciones en desuso {#deprecated-features}

Esta sección enumera las funciones que se han marcado como en desuso con AEM 6.5. Por lo general, las funciones que se planea eliminar en una versión futura se establecen en primer lugar como en desuso, con una alternativa que las sustituye.

Se recomienda a los clientes que comprueben si utilizan la función o capacidad en su implementación actual, y que planifiquen el cambio de la implementación y usen la alternativa proporcionada.

| Área | Característica | Reemplazo | Versión (SP) |
|---|---|---|---|
| Sites | [Editor de SPA](/help/sites-developing/spa-editor-deprecation.md) | Para casos de uso sin encabezado, utilice el [Editor universal](/help/sites-developing/universal-editor/introduction.md) para la edición visual o el [Editor de fragmentos de contenido](/help/sites-developing/universal-editor/introduction.md) para la edición basada en formularios. | 6.5.23 |
| Sites | El servicio **Configuración de encuestas administradas por Adobe AEM**: `com.day.cq.polling.importer.impl.ManagedPollConfigImpl` | El servicio **Importador de Sling de informes de AEM Analytics de Adobe**. Consulte Conectarse a Adobe Analytics y crear marcos de trabajo: [Configuración del intervalo de importación](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval) | 6.5.19.0 |
| Screens | ActiveMQ en Adobe Experience Manager (AEM). ActiveMQ se utilizaba para la comunicación entre dos instancias de publicación de AEM. | Adobe recomienda que los clientes ahora utilicen un equilibrador de carga. | 6.5.18.0 |
| Propiedades de Fragmentos de experiencias para **Estado de los medios sociales**. | |  | 6.5.11.0 |
| [!DNL Sites] | Plantillas de fragmentos de contenido, para crear fragmentos de contenido simples. | [Fragmentos de contenido estructurados basados en modelos](/help/assets/content-fragments/content-fragments-models.md) ahora. | 6.5.11.0 |
| Integración de Creative Cloud | AEM para uso compartido de carpetas de Creative Cloud se introdujo en AEM 6.2. Ofrece una forma de proporcionar a los usuarios creativos acceso a los recursos de AEM para que puedan abrirlos en aplicaciones de [!DNL Creative Cloud], cargar nuevos archivos o guardar cambios en AEM. Adobe Asset Link, una nueva función lanzada en la aplicación Creative Cloud, proporciona una mejor experiencia del usuario y un acceso más potente a los recursos de AEM directamente desde Photoshop, InDesign e Illustrator. Adobe no tiene previsto realizar más mejoras en la integración del uso compartido de carpetas de Creative Cloud en AEM. Aunque la función está incluida en AEM, se recomienda a los clientes utilizar el remplazo. | Se recomienda a los clientes cambiar a nuevas funciones de integración de Creative Cloud, como Adobe Asset Link o la aplicación de escritorio de AEM. |  |
| Recursos | `AssetDownloadServlet` está deshabilitado de manera predeterminada para las instancias de publicación. Para obtener más información, consulte [Lista de comprobación de seguridad de AEM](/help/sites-administering/security-checklist.md). | Configuración descrita en [Lista de comprobación de seguridad de AEM](/help/sites-administering/security-checklist.md). |  |
| Integraciones | La pantalla **[!UICONTROL Inclusión de Experience Manager Cloud Services]** está en desuso desde que la integración de [!DNL Experience Manager] y [!DNL Adobe Target] se actualizó en [!DNL Experience Manager] 6.5. La integración es compatible con la API de Adobe Target Standard. La API utiliza la autenticación mediante Adobe IMS y [!DNL Adobe I/O Runtime]. Admite la creciente función de Adobe Launch de instrumentar páginas de [!DNL Experience Manager] para el análisis y la personalización; el asistente de inclusión es irrelevante desde el punto de vista funcional. | Configure conexiones del sistema, autenticación IMS de Adobe e integraciones de [!DNL Adobe I/O Runtime] a través de los respectivos servicios en la nube de [!DNL Experience Manager]. | 6.5.7.0 |
| Conectores | El conector JCR de Adobe para Microsoft® SharePoint 2010 y Microsoft® SharePoint 2013 está obsoleto para [!DNL Experience Manager] 6.5. | N/A |  |
| Administrador dinámico de etiquetas (DTM) | La integración con DTM está en desuso. | Cambie a Adobe Experience Platform Launch como administrador de etiquetas. |   |
| Adobe Target | Al añadir la capacidad para que AEM se conecte al servicio de Adobe Target mediante la API estándar de Adobe Target (API de REST) basada en [!DNL Adobe I/O] en AEM 6.5, la forma de la API de Target Classic (XML) queda en desuso. | Vuelva a configurar la integración para [usar la nueva API](/help/sites-administering/target.md). |  |
| Adobe Target | El uso de la integración basada en `mbox.js` con Adobe Target en AEM está en desuso. | Cambiar para usar `at.js` 1.x. |  |
| Comercio | [CIF REST](https://github.com/adobe/commerce-cif-api) se proporcionó en 2018 como un conjunto de microservicios para habilitar integraciones entre AEM y motores de comercio. Después de que Adobe adquiriera Adobe Commerce (anteriormente Magento) a mediados de 2018, Adobe decidió cambiar su enfoque por dos razones. Commerce tiene su propio conjunto de API de Commerce (REST y GraphQL) y no es recomendable mantener dos conjuntos de API. Las tendencias del mercado indicaban que los clientes se estaban acercando a GraphQL, ya que es una forma más eficiente de consultar los datos. En 2019, Adobe lanzó el nuevo Commerce Integration Framework con las API de GraphQL de Commerce como fuente fiable. Adobe no tiene previsto realizar ninguna inversión adicional en CIF REST. Se aconseja a los clientes que utilicen la solución de sustitución. | Para las integraciones de AEM y Commerce, cambie a [AEM CIF Archetype](https://github.com/adobe/aem-cif-project-archetype) y [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components). Vea la integración de AEM con Adobe Commerce [mediante Commerce Integration Framework](/help/commerce/cif/integrating/magento.md). La compatibilidad con integraciones de terceros (distintas de Commerce) con el nuevo método está en la hoja de ruta de Adobe. |  |
| Componentes (AEM Sites) | Adobe no tiene previsto realizar más mejoras en la mayoría de los componentes de base almacenados en `/libs/foundation/components`. Busque las propiedades `cq:deprecated` y `cq:deprecatedReason` en la carpeta de componentes. AEM 6.5 incluye los componentes de base y los clientes que actualicen desde versiones anteriores pueden seguir utilizándolos tal cual. Además, los componentes de base son compatibles aunque estén obsoletos. | Adobe recomienda utilizar los componentes principales para proyectos futuros. Los sitios existentes pueden permanecer tal cual o usar el [Conjunto de herramientas de modernización de AEM](https://github.com/adobe/aem-modernize-tools) para refactorizar el sitio y usar los componentes principales. |  |
| Componentes (AEM Sites) | Los componentes del importador de diseños `/libs/wcm/designimporter/components` se han marcado como obsoletos a partir de 6.5. Adobe no tiene previsto realizar más mejoras en esa implementación del importador de diseños. | Adobe tiene previsto proporcionar una implementación alternativa del caso de uso en futuras versiones. |  |
| Foundation | Marco de descarga de Granite. Adobe no tiene previsto realizar más mejoras en la plataforma de descarga introducida en CQ 5.6.1 para externalizar el procesamiento de recursos. | Adobe está trabajando en un marco de descarga nativo de la nube de próxima generación. |  |
| Desarrolladores | `Hobbes.js`. Adobe no tiene previsto realizar más mejoras en el marco de prueba de la interfaz de usuario de `hobbes.js`. | Adobe recomienda que los clientes utilicen la automatización de Selenium. |  |
| Desarrolladores | Biblioteca de cliente de IU de jQuery. Adobe no tiene previsto seguir manteniendo ni actualizando la biblioteca de cliente de la interfaz de usuario de jQuery incluida como parte de la distribución (inicio rápido). | Adobe recomienda a los clientes que aún requieran la interfaz de usuario de jQuery para su código que lo añadan a su base de código de proyecto. |  |
| Desarrolladores | Biblioteca de cliente de jQuery Animation (`granite.jquery.animation`). Adobe no tiene previsto seguir manteniendo ni actualizando la biblioteca de cliente de animación de jQuery incluida como parte de la distribución (inicio rápido). | Adobe recomienda a los clientes que aún necesiten animaciones de jQuery para su código que lo añadan a su base de código de proyecto. |  |
| Desarrolladores | Biblioteca de cliente de Handlebars. Adobe no tiene previsto seguir manteniendo ni actualizando la biblioteca de cliente de Handlebars incluida como parte de la distribución (inicio rápido). | Adobe recomienda a los clientes que aún necesiten `Handlebars` para su código que lo añadan a su base de código de proyecto. |  |
| Desarrolladores | Biblioteca de cliente de Lawnchair. Adobe no tiene previsto seguir manteniendo ni actualizando la biblioteca de cliente de Lawnchair incluida como parte de la distribución (inicio rápido). | Adobe recomienda a los clientes que aún necesiten Lawnchair para su código que lo añadan a su base de código de proyecto. |  |
| Desarrolladores | Biblioteca de cliente de `Granite.Sling.js`. Adobe no tiene previsto mejorar la biblioteca de cliente de Granite.Sling.js incluida como parte de la distribución (inicio rápido). | Adobe recomienda a los clientes que dependan de la capacidad de la biblioteca de refactorizar su código para que ya no la utilicen. |  |
| Desarrolladores | Usar YUI para comprimir o minimizar las bibliotecas de cliente de JavaScript. Adobe no tiene previsto actualizar ya más la biblioteca de YUI. Hasta AEM 6.4, YUI era la opción predeterminada para minimizar JavaScript con la opción de cambiar a Google Closure Compiler (GCC). A partir de AEM 6.5, GCC es la opción predeterminada. | Adobe recomienda a los clientes que actualicen a AEM 6.5 cambiar a GCC para su implementación |  |
| Desarrolladores | Editor de cuadros de diálogo de IU clásica en CRXDE Lite. Adobe no tiene previsto mejorar el editor de diálogos estándar de interfaz de usuario incluido como parte de la distribución (Quickstart) | No hay ningún reemplazo disponible. |  |
| Formularios | La integración de AEM Forms con AEM Mobile está en desuso. | No hay ningún reemplazo disponible. |  |
| Desarrolladores | Editor de cuadros de diálogo de IU clásica en CRXDE Lite. Adobe no tiene previsto mejorar el editor de diálogos estándar de interfaz de usuario incluido como parte de la distribución (Quickstart) | No hay ningún reemplazo disponible. |  |
| Desarrolladores | Biblioteca de cliente lodash/underscore. Adobe no tiene previsto mantener y actualizar la biblioteca de cliente Lodash/underscore que se envía como parte de la distribución (inicio rápido). | Adobe recomienda a los clientes que aún requieran Lodash/underscore para su código que lo añadan a su base de código de proyecto. |  |
| [!DNL Foundation] | Compatibilidad con com.adobe.granite.oauth.server | Integración de IMS de Adobe |  |

## Funciones eliminadas {#removed-features}

Esta sección enumera las funciones que se han eliminado de AEM 6.5. Las versiones anteriores tenían estas funciones marcadas como en desuso.

| Área | Característica | Reemplazo | Versión (SP) |
|--- |--- |--- |--- |
| Comercio | Se ha eliminado AEM CIF Classic. | Debe migrar a [AEM CIF](/help/commerce/cif/migration.md). Si todavía necesita CIF Classic, se ha creado un paquete de compatibilidad, [comuníquese con atención al cliente de Adobe](https://experienceleague.adobe.com/es/home?support-solution=General#support). | 6.5.22.0 |
| Integración con [!DNL Experience Cloud] | Puede sincronizar sus recursos con [!DNL Experience Cloud] mediante una configuración a través de [!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] se llamaba anteriormente [!DNL Adobe Experience Cloud]. | Si tiene alguna pregunta, [póngase en contacto con Atención al cliente de Adobe](https://experienceleague.adobe.com/es/home?support-solution=General#support). |  |
| Analytics Activity Map | La versión de Activity Map que se incluye en AEM. | Debido a los cambios de seguridad de la API de Adobe Analytics, ya no es posible utilizar la versión de Activity Map incluida en AEM. Use el [complemento ActivityMap proporcionado por Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=es). |  |
| Integraciones | La integración de ExactTarget se ha quitado de la distribución predeterminada (inicio rápido) y ya no está disponible. | No hay reemplazo. |  |
| Integraciones | La integración de la API Salesforce Force se ha quitado de la distribución predeterminada (inicio rápido) y ahora es un paquete adicional que se debe instalar desde la [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html). | La función aún está disponible. |  |
| Formularios | Se ha quitado la compatibilidad con el servicio Adobe Central Migration Bridge, ya que el producto Adobe Central ya no es compatible. | No hay reemplazo. |  |
| Formularios | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | No hay reemplazo. |  |
| Formularios | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | No hay reemplazo |  |
| Formularios | La actualización de un solo salto de LiveCycle ES4 SP1 a AEM 6.5 Forms en JEE no está disponible | Consulte [rutas de actualización disponibles](../forms/using/upgrade.md) en la documentación de actualización de AEM Forms. |  |
| Formularios | Se ha quitado la compatibilidad con clústeres basados en UPD de AEM Forms en JEE | En AEM Forms en JEE, solo se pueden utilizar clústeres basados en TCP. Si actualiza un servidor multidifusión UDP de una versión anterior a AEM 5.5 Forms en JEE, realice configuraciones manuales para cambiar a clústeres de gemfire basados en TCP. Para obtener instrucciones detalladas, consulte [Actualizar a AEM 6.5 Forms en JEE](../forms/using/upgrade-forms-jee.md) |  |
| Desarrolladores | Firebug Lite se ha quitado de la distribución predeterminada (inicio rápido) | Uso de las consolas de desarrollador integradas del explorador |  |
| Desarrolladores | Quitar la compatibilidad con `customJavaScriptPath` en el Administrador de bibliotecas de cliente HTML. | No hay reemplazo |  |
| [!DNL Assets] | La característica de descarga de recursos se ha quitado en [!DNL Adobe Experience Manager] 6.5. | No hay ningún reemplazo disponible. |  |
| Caché | `system/console/slingjsp` se ha quitado y ya no está disponible en AEM 6.5. | La caché ligera y de clases se almacena en el paquete Apache Sling Commons FileSystem ClassLoader. Puede comprobar el número de paquete en la consola web de AEM y quitar la carpeta de caché directamente del sistema de archivos (`crx-quickstart/launchpad/felix/bundle<ID>`). |  |
| Screens | Se ha quitado la compatibilidad con el paquete activemq y sus configuraciones relacionadas. |  |  |

<!-- ## Pre-announcement for next release {#pre-announcement-for-next-release}

This section is used to pre-announce the upcoming changes in the future releases. The announced changes are not yet effective but will impact customers. For example, the features are not yet deprecated but impacts the users after deprecation. These updates are provided for planning purpose.

|Area|Feature|Announcement|
|--- |--- |--- |
|Foundation|UI Framework|Adobe is planning to deprecate the Coral UI 2 components in 2019. Coral UI 3 was introduced with AEM 6.2, and AEM 6.5 is fully based on Coral 3. Adobe recommends customers and partners that have build custom UIs with Coral 2 to refactored them to Coral 3. Adobe is providing a tool to convert Coral 2 dialogs to Coral 3 - [Read more](/help/sites-developing/modernization-tools.md).|
-->
