---
title: Funciones obsoletas y eliminadas en la versión 6.5 de Adobe Experience Manager.
description: Notas de versión específicas de las funciones en desuso y eliminadas de Adobe Experience Manager 6.5.
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: 3443d331815ffb462890282a49e658693f157af0
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 10%

---

# Funciones en desuso y eliminadas {#deprecated-and-removed-features}

<!-- Search&Promote is end-of-life September 1, 2022 | Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Honor the access control setup of user and ensure appropriate permissions. ||
|Adobe Search & Promote|The integration with Adobe Search & Promote is deprecated. Adobe does not plan to make further enhancements to the Search & Promote integration. Adobe Search & Promote integration remains fully supported while being deprecated.||| -->

Adobe evalúa constantemente las capacidades de los productos para renovar o sustituir las funciones más antiguas con alternativas modernas que mejoren el valor general del cliente, siempre teniendo en cuenta la compatibilidad con versiones anteriores.

Para comunicar la inminente eliminación o sustitución de las funciones de Adobe Experience Manager AEM (), se aplican las siguientes reglas:

1. Primero se anuncia el desuso. Aunque están en desuso, las funciones siguen estando disponibles, pero no se siguen mejorando.
1. La eliminación de las funciones obsoletas se produce en la siguiente versión principal como pronto. La fecha objetivo real para la eliminación se anunciará más adelante.

Este proceso proporciona a los clientes un ciclo de lanzamiento para adaptar su implementación a una nueva versión o a la siguiente versión de una capacidad en desuso, antes de eliminarla.

## Funciones obsoletas {#deprecated-features}

AEM Esta sección enumera las funciones que se han marcado como obsoletas con la versión 6.5 de la. Por lo general, las funciones que se planea eliminar en una versión futura se establecen en primer lugar como obsoletas, con una alternativa que las sustituye.

Se recomienda a los clientes que comprueben si utilizan la función o capacidad en su implementación actual, y que planifiquen el cambio de la implementación y usen la alternativa proporcionada.

| Área | Funcionalidad | Reemplazo | Versión (SP) |
|---|---|---|---|
|   |   |   |   |
| Sites | El **Configuración de encuestas administradas de Adobe AEM** servicio: `com.day.cq.polling.importer.impl.ManagedPollConfigImpl` | El **Importador de informes de Sling de Adobe AEM Analytics** servicio. Consulte Conexión a Adobe Analytics y Creación de marcos: [Configuración del intervalo de importación](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval) | 6.5.19.0 |
| Screens | ActiveMQ en Adobe Experience Manager AEM (). AEM ActiveMQ se utilizaba para la comunicación entre dos instancias de publicación de. | Adobe recomienda que los clientes ahora utilicen un equilibrador de carga. | 6.5.18.0 |
| Propiedades de Fragmentos de experiencias para **Estado de los medios sociales**. |   | 6.5.11.0 |
| [!DNL Sites] | Plantillas de fragmentos de contenido, para crear fragmentos de contenido simples. | [Fragmentos de contenido estructurados basados en modelos](/help/assets/content-fragments/content-fragments-models.md) ahora. | 6.5.11.0 |
| Integración de Creative Cloud | AEM En la versión 6.2 se introdujo Uso compartido de carpetas de Creative Cloud AEM de. AEM Proporciona una forma de proporcionar a los usuarios creativos acceso a los recursos de para que puedan abrirlos en los recursos de la aplicación y, de este modo, acceder a los recursos de la manera más rápida posible. [!DNL Creative Cloud] AEM y cargar nuevos archivos o guardar cambios en los archivos de la aplicación de forma que se puedan guardar en la. Una nueva funcionalidad lanzada en la aplicación de Creative Cloud, Adobe AEM Asset Link, ofrece una mejor experiencia de usuario y un acceso más potente a los recursos desde la directamente desde Photoshop, InDesign y Illustrator. Adobe AEM no tiene previsto realizar más mejoras en la integración de la integración de uso compartido de carpetas de Creative Cloud de la página de inicio de sesión. AEM Aunque la función está incluida en el servicio de asistencia, se recomienda a los clientes que utilicen soluciones de reemplazo. | Se aconseja a los clientes que cambien a nuevas funciones de integración de Creative Cloud, como Adobe AEM Asset Link o aplicación de escritorio para la aplicación de escritorio de la aplicación de escritorio de la. |  |
| Assets | `AssetDownloadServlet` está desactivado de forma predeterminada para las instancias de publicación. Para obtener más información, consulte [AEM Lista de comprobación de seguridad de](/help/sites-administering/security-checklist.md). | Configuración descrita en [AEM Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md). |  |
| Integraciones | La pantalla **[!UICONTROL Inclusión de Experience Manager Cloud Service]** está obsoleto debido a que [!DNL Experience Manager] y [!DNL Adobe Target] La integración de se actualiza en [!DNL Experience Manager] 6.5. La integración es compatible con la API de Adobe Target Standard. La API utiliza la autenticación mediante Adobe IMS y [!DNL Adobe I/O Runtime]. Apoya el creciente papel de Adobe Launch en instrumentación [!DNL Experience Manager] en el caso de las páginas de analytics y personalización, el asistente de inclusión es irrelevante desde el punto de vista funcional. | Configurar conexiones del sistema, autenticación IMS de Adobe y [!DNL Adobe I/O Runtime] integraciones a través de las respectivas [!DNL Experience Manager] cloud services. | 6.5.7.0 |
| Conectores | El conector JCR de Adobe para Microsoft® SharePoint 2010 y Microsoft® SharePoint 2013 está obsoleto para [!DNL Experience Manager] 6.5. | N/D |  |
| Administrador dinámico de etiquetas (DTM) | La integración con DTM está en desuso. | Cambie a para utilizar Adobe Experience Platform Launch como administrador de etiquetas. |   |
| Adobe Target | AEM Con la adición de la capacidad para que los usuarios se conecten a un servicio de Adobe Target mediante el uso de la opción de conexión de [!DNL Adobe I/O] La API estándar de Adobe Target AEM (API de REST) basada en la versión 6.5 de, la forma de la API de Target Classic (XML), ya no se utiliza. | Vuelva a configurar la integración en [usar la nueva API](/help/sites-administering/target.md). |  |
| Adobe Target | Uso del `mbox.js` La integración basada en con Adobe Target AEM en la está obsoleta. | Cambiar a uso `at.js` 1.x. |  |
| Comercio | [CIF REST DE](https://github.com/adobe/commerce-cif-api) AEM fue provisto en 2018 como un conjunto de microservicios para permitir integraciones entre motores de comercio y de comercio de la industria de la industria de la construcción de la industria de la construcción. Después de que Adobe adquirió Adobe Commerce (anteriormente Magento) a mediados de 2018, Adobe decidió cambiar su enfoque por dos razones. Commerce tiene su propio conjunto de API de Commerce (REST y GraphQL) y no es recomendable mantener dos conjuntos de API. Las tendencias del mercado indicaban que los clientes se estaban acercando a GraphQL, ya que es una forma más eficiente de consultar los datos. En 2019, Adobe ha lanzado el nuevo Commerce integration framework utilizando las API de GraphQL de Commerce como fuente fiable. El Adobe CIF no planea hacer ninguna inversión adicional en REST de la. Se aconseja a los clientes que utilicen la solución de sustitución. | AEM Para las integraciones de comercio de la plataforma de datos de, cambie a [AEM CIF Tipo de archivo de](https://github.com/adobe/aem-cif-project-archetype) y [AEM CIF Componentes principales de](https://github.com/adobe/aem-core-cif-components). AEM Consulte Integración de y Adobe Commerce [uso del Commerce integration framework](/help/commerce/cif/integrating/magento.md). La compatibilidad con integraciones de terceros (distintas de Commerce) con el nuevo método está en la hoja de ruta del Adobe. |  |
| Componentes (AEM Sites) | Adobe no tiene previsto realizar más mejoras en la mayoría de los componentes de base almacenados en `/libs/foundation/components`. Busque la variable `cq:deprecated` y `cq:deprecatedReason` en la carpeta de componentes. AEM En 6.5 se han incluido los componentes de base, y los clientes que actualicen desde versiones anteriores podrán seguir utilizándolos tal cual. Además, los componentes de base son compatibles aunque estén obsoletos. | El Adobe recomienda utilizar los componentes principales para proyectos futuros. Los sitios existentes pueden permanecer tal cual o utilizar el [AEM Conjunto de herramientas de modernización de](https://github.com/adobe/aem-modernize-tools) para refactorizar el sitio y utilizar los componentes principales. |  |
| Componentes (AEM Sites) | Componentes del importador de diseños `/libs/wcm/designimporter/components` se han marcado como obsoletas a partir de la versión 6.5. El Adobe no tiene previsto realizar más mejoras en esa implementación del importador de diseños. | Adobe tiene previsto proporcionar una implementación alternativa del caso de uso en futuras versiones. |  |
| Foundation | Marco de descarga de Granite. Adobe no planea realizar más mejoras en la plataforma de descarga introducida en CQ 5.6.1 para externalizar el procesamiento de recursos. | Adobe está trabajando en un módulo de descarga nativo de la nube de próxima generación. |  |
| Desarrolladores | `Hobbes.js`. El Adobe no tiene previsto realizar más mejoras en el `hobbes.js` marco de pruebas de interfaz de usuario. | El Adobe recomienda que los clientes utilicen la automatización de Selenium. |  |
| Desarrolladores | Biblioteca de cliente de IU de jQuery. Adobe no planea mantener y actualizar más la biblioteca de cliente de la interfaz de usuario de jQuery que se envía como parte de la distribución (inicio rápido). | Adobe recomienda a los clientes que aún requieran la interfaz de usuario de jQuery para su código que lo añadan a su base de código de proyecto. |  |
| Desarrolladores | Biblioteca de cliente de jQuery Animation (`granite.jquery.animation`). Adobe no planea mantener y actualizar la biblioteca de cliente de jQuery Animation que se envía como parte de la distribución (inicio rápido). | Adobe recomienda a los clientes que aún necesiten animaciones jQuery para su código que lo añadan a su base de código de proyecto. |  |
| Desarrolladores | Biblioteca de cliente Handlebars. Adobe no planea mantener y actualizar más la biblioteca de cliente de Handlebar que se envía como parte de la distribución (inicio rápido). | El Adobe recomienda a los clientes que aún necesiten `Handlebars` para que su código lo añada a su base de código de proyecto. |  |
| Desarrolladores | Biblioteca cliente de sillas de jardín. Adobe no tiene previsto mantener y actualizar la biblioteca de cliente de Lawnchair que se envía como parte de la distribución (Quickstart). | Adobe recomienda a los clientes que aún necesiten Lawnchair para su código que lo añadan a su base de código de proyecto. |  |
| Desarrolladores | `Granite.Sling.js` biblioteca de cliente. Adobe no planea mejorar más la biblioteca de cliente Granite.Sling.js que se envía como parte de la distribución (Quickstart). | Adobe recomienda a los clientes que dependan de la capacidad de la biblioteca de refactorizar su código para que ya no lo utilicen. |  |
| Desarrolladores | Uso de la IU de para comprimir/minimizar las bibliotecas de cliente de JavaScript. El Adobe no tiene previsto actualizar la biblioteca YUI. AEM Hasta la versión 6.4, YUI era la opción predeterminada para minimizar JavaScript con la opción de cambiar a Google Closure Compiler (GCC). AEM A partir de la versión 6.5, GCC es la predeterminada. | El Adobe AEM recomienda a los clientes que actualicen a la versión 6.5 de la versión para cambiar a la versión GCC para su implementación de |  |
| Desarrolladores | Editor de cuadros de diálogo de IU clásica en CRXDE Lite. Adobe no planea mejorar aún más el Editor de cuadros de diálogo de la IU clásica que se incluye como parte de la distribución (inicio rápido) | No hay reemplazo disponible. |  |
| Forms | La integración de AEM Forms con AEM Mobile está en desuso. | No hay disponible ningún reemplazo. |  | Desarrolladores | Editor de cuadros de diálogo de IU clásica en CRXDE Lite. Adobe no planea mejorar aún más el Editor de cuadros de diálogo de la IU clásica que se incluye como parte de la distribución (inicio rápido) | No hay reemplazo disponible. |  |
| Desarrolladores | Biblioteca de cliente lodash/underscore. Adobe no planea mantener y actualizar la biblioteca de cliente Lodash/underscore que se envía como parte de la distribución (inicio rápido). | Adobe recomienda a los clientes que aún requieran Lodash/guion bajo para que su código lo añada a su base de código de proyecto. |  |

## Funciones eliminadas {#removed-features}

AEM Esta sección enumera las funciones y capacidades que se han eliminado de la versión 6.5 de. Las versiones anteriores tenían estas funciones marcadas como obsoletas.

| Área | Funcionalidad | Reemplazo | Versión (SP) |
|--- |--- |--- |--- |
| Integración con [!DNL Experience Cloud] | Puede sincronizar sus recursos con [!DNL Experience Cloud] uso de una configuración de mediante [!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] se llamaba anteriormente [!DNL Adobe Experience Cloud]. | Si tiene alguna consulta, [Contactar con Adobe Atención al cliente](https://experienceleague.adobe.com/?support-solution=General&amp;lang=es#support). |  |
| Activity Map de Analytics | La versión del Activity Map AEM que se incluye dentro de la lista de distribución de. | Debido a los cambios de seguridad de la API de Adobe Analytics, ya no es posible utilizar la versión de Activity Map incluida en AEM. Utilice el [El complemento Activity Map proporcionado por Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=es). |  |
| Integraciones | La integración de ExactTarget se ha eliminado de la distribución predeterminada (inicio rápido) y ya no está disponible. | No hay reemplazo. |  |
| Integraciones | La integración de la API de Salesforce Force se ha eliminado de la distribución predeterminada (Quickstart) y ahora es un paquete adicional para instalar desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html). | La función aún está disponible. |
| Forms | Se ha eliminado la compatibilidad con el servicio de puente de migración de Adobe central, ya que el producto de Adobe central ya no es compatible. | No hay reemplazo. |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | No hay reemplazo. |  |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Sin reemplazo |  |
| Forms | La actualización de un solo salto del LiveCycle AEM ES4 SP1 a.5 Forms en JEE no está disponible | Consulte [rutas de actualización disponibles](../forms/using/upgrade.md) en la documentación de actualización de AEM Forms. |  |
| Forms | Se ha eliminado la compatibilidad con clústeres basados en UPD de AEM Forms en JEE | En AEM Forms, solo se puede utilizar la agrupación en clúster basada en TCP en JEE. AEM Si actualiza un servidor de multidifusión UDP de una versión anterior a la versión 5.5 de Forms en JEE, realice configuraciones manuales para cambiar a clústeres de gemfire basados en TCP. Para obtener instrucciones detalladas, consulte [AEM Actualizar a formularios 6.5 en JEE](../forms/using/upgrade-forms-jee.md) |  |
| Desarrolladores | Firebug Lite se ha eliminado de la distribución predeterminada (inicio rápido) | Uso de las consolas de desarrollador integradas del explorador |
| Desarrolladores | Eliminar `customJavaScriptPath` compatibilidad con en el Administrador de bibliotecas de cliente de HTML. | Sin reemplazo |  |
| [!DNL Assets] | La función de descarga de recursos se ha eliminado de [!DNL Adobe Experience Manager] 6.5. | No hay reemplazo disponible. |  |
| Caché | `system/console/slingjsp` AEM se ha eliminado y ya no está disponible en la versión 6.5 de. | Las clases y la caché de Slightly se almacenan en el paquete Apache Sling Commons FileSystem ClassLoader. AEM Puede comprobar el número de paquete en la consola web de y quitar la carpeta de caché directamente del sistema de archivos (`crx-quickstart/launchpad/felix/bundle<ID>`). |  |
| Screens | Se ha eliminado la compatibilidad con el paquete activemq y sus configuraciones relacionadas. |  |  |

<!-- ## Pre-announcement for next release {#pre-announcement-for-next-release}

This section is used to pre-announce the upcoming changes in the future releases. The announced changes are not yet effective but will impact customers. For example, the features are not yet deprecated but impacts the users after deprecation. These updates are provided for planning purpose.

|Area|Feature|Announcement|
|--- |--- |--- |
|Foundation|UI Framework|Adobe is planning to deprecate the Coral UI 2 components in 2019. Coral UI 3 was introduced with AEM 6.2, and AEM 6.5 is fully based on Coral 3. Adobe recommends customers and partners that have build custom UIs with Coral 2 to refactored them to Coral 3. Adobe is providing a tool to convert Coral 2 dialogs to Coral 3 - [Read more](/help/sites-developing/modernization-tools.md).|
-->
