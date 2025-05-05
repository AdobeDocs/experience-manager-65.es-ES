---
title: Funciones obsoletas y eliminadas en la versión 6.5 de Adobe Experience Manager.
description: Notas de versión específicas de las funciones en desuso y eliminadas de Adobe Experience Manager 6.5.
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 191c4b02274ca7e3e9d4622b72cd585870581f47
workflow-type: tm+mt
source-wordcount: '1747'
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
| Sites | El servicio **Configuración de encuestas administradas por el Adobe AEM de trabajo**: `com.day.cq.polling.importer.impl.ManagedPollConfigImpl` | El servicio **Importador de Sling de informes de Adobe AEM Analytics**. Consulte Conectarse a Adobe Analytics y crear marcos de trabajo: [Configuración del intervalo de importación](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval) | 6.5.19.0 |
| Screens | ActiveMQ en Adobe Experience Manager AEM (). AEM Se utilizó ActiveMQ para la comunicación entre dos instancias de Publish de la misma clase. | Adobe recomienda que los clientes ahora utilicen un equilibrador de carga. | 6.5.18.0 |
| Propiedades de Fragmentos de experiencias para **Estado de los medios sociales**. |   | 6.5.11.0 |
| [!DNL Sites] | Plantillas de fragmentos de contenido, para crear fragmentos de contenido simples. | [Fragmentos de contenido estructurados basados en modelos](/help/assets/content-fragments/content-fragments-models.md) ahora. | 6.5.11.0 |
| Integración de Creative Cloud | AEM En la versión 6.2 se introdujo Uso compartido de carpetas de Creative Cloud AEM de. AEM AEM Proporciona una forma de proporcionar a los usuarios creativos acceso a los recursos de para que puedan abrirlos en [!DNL Creative Cloud] aplicaciones, cargar nuevos archivos o guardar cambios en los recursos de manera que puedan acceder a los recursos de manera que puedan acceder a los recursos desde cualquier parte de los recursos de manera que se puedan abrir en  aplicaciones y se puedan guardar los cambios en los recursos de los que se dispone en la. Una nueva funcionalidad lanzada en la aplicación de Creative Cloud, Adobe AEM Asset Link, ofrece una mejor experiencia de usuario y un acceso más potente a los recursos desde la directamente desde Photoshop, InDesign y Illustrator. Adobe AEM no tiene previsto realizar más mejoras en la integración de la integración de uso compartido de carpetas de Creative Cloud de la página de inicio de sesión. AEM Aunque la función está incluida en el servicio de asistencia, se recomienda a los clientes que utilicen soluciones de reemplazo. | Se aconseja a los clientes que cambien a nuevas funciones de integración de Creative Cloud, como Adobe AEM Asset Link o aplicación de escritorio para la aplicación de escritorio de la aplicación de escritorio de la. |  |
| Recursos | `AssetDownloadServlet` está deshabilitado de manera predeterminada para las instancias de publicación. AEM Para obtener más información, consulte [Lista de comprobación de seguridad de la](/help/sites-administering/security-checklist.md). | AEM Configuración descrita en [Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md). |  |
| Integraciones | La pantalla **[!UICONTROL Inclusión de Experience Manager Cloud Service]** está obsoleta desde que la integración de [!DNL Experience Manager] y [!DNL Adobe Target] se actualizó en [!DNL Experience Manager] 6.5. La integración es compatible con la API de Adobe Target Standard. La API utiliza la autenticación mediante Adobe IMS y [!DNL Adobe I/O Runtime]. Admite la función cada vez mayor de Adobe Launch de instrumentar las páginas de [!DNL Experience Manager] para el análisis y la personalización; el asistente de inclusión es irrelevante desde el punto de vista funcional. | Configure conexiones del sistema, autenticación IMS de Adobe e integraciones de [!DNL Adobe I/O Runtime] a través de los respectivos servicios en la nube [!DNL Experience Manager]. | 6.5.7.0 |
| Conectores | El conector JCR de Adobe para Microsoft® SharePoint 2010 y Microsoft® SharePoint 2013 está obsoleto para [!DNL Experience Manager] 6.5. | N/D |  |
| Administrador dinámico de etiquetas (DTM) | La integración con DTM está en desuso. | Cambie a para utilizar Adobe Experience Platform Launch como administrador de etiquetas. |   |
| Adobe Target | AEM Al agregar la capacidad para que los se conecten al servicio Adobe Target mediante la API estándar de Adobe Target AEM (API de REST) basada en [!DNL Adobe I/O] en la versión 6.5, la forma de la API de Target Classic (XML) queda obsoleta. | Vuelva a configurar la integración para [usar la nueva API](/help/sites-administering/target.md). |  |
| Adobe Target | El uso de la integración basada en `mbox.js` con Adobe Target AEM en el caso de los está obsoleto. | Cambiar para usar `at.js` 1.x. |  |
| Comercio | CIF AEM [REST](https://github.com/adobe/commerce-cif-api) se proporcionó en 2018 como un conjunto de microservicios para permitir integraciones entre motores de comercio y de comercio de la red de distribución de datos (MCID) de la red de comercio internacional (MCIDs). Después de que Adobe adquirió Adobe Commerce (anteriormente Magento) a mediados de 2018, Adobe decidió cambiar su enfoque por dos razones. Commerce tiene su propio conjunto de API de Commerce (REST y GraphQL) y no es recomendable mantener dos conjuntos de API. Las tendencias del mercado indicaban que los clientes se estaban acercando a GraphQL, ya que es una forma más eficiente de consultar los datos. En 2019, Adobe ha lanzado el nuevo Commerce integration framework utilizando las API de GraphQL de Commerce como fuente fiable. El Adobe CIF no tiene previsto realizar ninguna inversión adicional en REST en el sector de la. Se aconseja a los clientes que utilicen la solución de sustitución. | AEM Para las integraciones de Commerce AEM CIF AEM CIF de la, cambie a [Arquetipo de archivo](https://github.com/adobe/aem-cif-project-archetype) y [Componentes principales de la](https://github.com/adobe/aem-core-cif-components). AEM Vea la integración de Adobe Commerce [con el Commerce integration framework ](/help/commerce/cif/integrating/magento.md) y el usuario de la vista de datos. La compatibilidad con integraciones de terceros (distintas de Commerce) con el nuevo método está en la hoja de ruta del Adobe. |  |
| Componentes (AEM Sites) | El Adobe no planea realizar más mejoras en la mayoría de los componentes de base almacenados en `/libs/foundation/components`. Busque las propiedades `cq:deprecated` y `cq:deprecatedReason` en la carpeta de componentes. AEM En 6.5 se han incluido los componentes de base, y los clientes que actualicen desde versiones anteriores podrán seguir utilizándolos tal cual. Además, los componentes de base son compatibles aunque estén obsoletos. | El Adobe recomienda utilizar los componentes principales para proyectos futuros. AEM Los sitios existentes pueden permanecer tal cual o usar el [Conjunto de herramientas de modernización de la](https://github.com/adobe/aem-modernize-tools) para refactorizar el sitio y usar los componentes principales. |  |
| Componentes (AEM Sites) | Los componentes del importador de diseños `/libs/wcm/designimporter/components` se han marcado como obsoletos a partir de 6.5. El Adobe no tiene previsto realizar más mejoras en esa implementación del importador de diseños. | Adobe tiene previsto proporcionar una implementación alternativa del caso de uso en futuras versiones. |  |
| Foundation | Marco de descarga de Granite. Adobe no planea realizar más mejoras en la plataforma de descarga introducida en CQ 5.6.1 para externalizar el procesamiento de recursos. | Adobe está trabajando en un módulo de descarga nativo de la nube de próxima generación. |  |
| Desarrolladores | `Hobbes.js`. El Adobe no planea realizar más mejoras en el marco de pruebas de la interfaz de usuario de `hobbes.js`. | El Adobe recomienda que los clientes utilicen la automatización de Selenium. |  |
| Desarrolladores | Biblioteca de cliente de IU de jQuery. Adobe no planea mantener y actualizar más la biblioteca de cliente de la interfaz de usuario de jQuery que se envía como parte de la distribución (inicio rápido). | Adobe recomienda a los clientes que aún requieran la interfaz de usuario de jQuery para su código que lo añadan a su base de código de proyecto. |  |
| Desarrolladores | Biblioteca de cliente de jQuery Animation (`granite.jquery.animation`). Adobe no planea mantener y actualizar la biblioteca de cliente de jQuery Animation que se envía como parte de la distribución (inicio rápido). | Adobe recomienda a los clientes que aún necesiten animaciones jQuery para su código que lo añadan a su base de código de proyecto. |  |
| Desarrolladores | Biblioteca de cliente Handlebars. Adobe no planea mantener y actualizar más la biblioteca de cliente de Handlebar que se envía como parte de la distribución (inicio rápido). | El Adobe recomienda a los clientes que aún necesiten `Handlebars` para su código que lo agreguen a su base de código de proyecto. |  |
| Desarrolladores | Biblioteca cliente de sillas de jardín. Adobe no tiene previsto mantener y actualizar la biblioteca de cliente de Lawnchair que se envía como parte de la distribución (Quickstart). | Adobe recomienda a los clientes que aún necesiten Lawnchair para su código que lo añadan a su base de código de proyecto. |  |
| Desarrolladores | `Granite.Sling.js` biblioteca de cliente. Adobe no planea mejorar más la biblioteca de cliente Granite.Sling.js que se envía como parte de la distribución (Quickstart). | Adobe recomienda a los clientes que dependan de la capacidad de la biblioteca de refactorizar su código para que ya no lo utilicen. |  |
| Desarrolladores | Usar la interfaz de usuario de para comprimir o minimizar las bibliotecas de cliente de JavaScript. El Adobe no tiene previsto actualizar la biblioteca YUI. AEM Hasta la versión 6.4, YUI era la opción predeterminada para minimizar JavaScript con la opción de cambiar a Google Closure Compiler (GCC). AEM A partir de la versión 6.5, GCC es la predeterminada. | El Adobe AEM recomienda a los clientes que actualicen a la versión 6.5 de la versión para cambiar a la versión GCC para su implementación de |  |
| Desarrolladores | Editor de cuadros de diálogo de IU clásica en CRXDE Lite. Adobe no planea mejorar aún más el Editor de cuadros de diálogo de la IU clásica que se incluye como parte de la distribución (inicio rápido) | No hay reemplazo disponible. |  |
| Formularios | La integración de AEM Forms con AEM Mobile está en desuso. | No hay disponible ningún reemplazo. |
| Desarrolladores | Editor de cuadros de diálogo de IU clásica en CRXDE Lite. Adobe no planea mejorar aún más el Editor de cuadros de diálogo de la IU clásica que se incluye como parte de la distribución (inicio rápido) | No hay reemplazo disponible. |  |
| Desarrolladores | Biblioteca de cliente lodash/underscore. Adobe no planea mantener y actualizar la biblioteca de cliente Lodash/underscore que se envía como parte de la distribución (inicio rápido). | Adobe recomienda a los clientes que aún requieran Lodash/guion bajo para que su código lo añada a su base de código de proyecto. |  |

## Funciones eliminadas {#removed-features}

AEM Esta sección enumera las funciones y capacidades que se han eliminado de la versión 6.5 de. Las versiones anteriores tenían estas funciones marcadas como obsoletas.

| Área | Funcionalidad | Reemplazo | Versión (SP) |
|--- |--- |--- |--- |
| Comercio | AEM CIF Se ha eliminado el clásico de la. | AEM CIF Debe migrar a [&#128279;](/help/commerce/cif/migration.md). CIF Si todavía necesita el servicio de asistencia al cliente Classic, se ha creado un paquete de compatibilidad, [póngase en contacto con el servicio de atención al cliente de Adobe](https://experienceleague.adobe.com/es?support-solution=General#support). | 6.5.22.0 |
| Integración con [!DNL Experience Cloud] | Puede sincronizar sus recursos con [!DNL Experience Cloud] mediante una configuración a través de [!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] se llamaba anteriormente [!DNL Adobe Experience Cloud]. | Si tiene alguna pregunta, [póngase en contacto con el Servicio de atención al cliente de Adobe](https://experienceleague.adobe.com/es?support-solution=General#support). |  |
| Activity Map de Analytics | La versión del Activity Map AEM que se incluye dentro de la lista de distribución de. | Debido a los cambios de seguridad de la API de Adobe Analytics, ya no es posible utilizar la versión de Activity Map incluida en AEM. Use el complemento [ActivityMap proporcionado por Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=es). |  |
| Integraciones | La integración de ExactTarget se ha eliminado de la distribución predeterminada (inicio rápido) y ya no está disponible. | No hay reemplazo. |  |
| Integraciones | La integración de la API Salesforce Force se ha eliminado de la distribución predeterminada (Quickstart) y ahora es un paquete adicional que se debe instalar desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html). | La función aún está disponible. |
| Formularios | Se ha eliminado la compatibilidad con el servicio Bridge de migración central de Adobe porque el producto Adobe Central ya no es compatible. | No hay reemplazo. |  |
| Formularios | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | No hay reemplazo. |  |
| Formularios | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Sin reemplazo |  |
| Formularios | La actualización de un solo salto del LiveCycle AEM ES4 SP1 a.5 Forms en JEE no está disponible | Consulte [rutas de actualización disponibles](../forms/using/upgrade.md) en la documentación de actualización de AEM Forms. |  |
| Formularios | Se ha eliminado la compatibilidad con clústeres basados en UPD de AEM Forms en JEE | En AEM Forms, solo se puede utilizar la agrupación en clúster basada en TCP en JEE. AEM Si actualiza un servidor de multidifusión UDP de una versión anterior a la versión 5.5 de Forms en JEE, realice configuraciones manuales para cambiar a clústeres de gemfire basados en TCP. AEM Para obtener instrucciones detalladas, consulte [Actualizar a formularios de 6.5 en JEE](../forms/using/upgrade-forms-jee.md) |  |
| Desarrolladores | Firebug Lite se ha eliminado de la distribución predeterminada (inicio rápido) | Uso de las consolas de desarrollador integradas del explorador |
| Desarrolladores | Quitar la compatibilidad con `customJavaScriptPath` en el Administrador de bibliotecas de cliente de HTML. | Sin reemplazo |  |
| [!DNL Assets] | La característica de descarga de recursos se ha eliminado en [!DNL Adobe Experience Manager] 6.5. | No hay reemplazo disponible. |  |
| Caché | AEM `system/console/slingjsp` se ha eliminado y ya no está disponible en la versión 6.5 de. | Las clases y la caché de Slightly se almacenan en el paquete Apache Sling Commons FileSystem ClassLoader. AEM Puede comprobar el número de paquete en la consola web de la y quitar la carpeta de caché directamente del sistema de archivos (`crx-quickstart/launchpad/felix/bundle<ID>`). |  |
| Screens | Se ha eliminado la compatibilidad con el paquete activemq y sus configuraciones relacionadas. |  |  |

<!-- ## Pre-announcement for next release {#pre-announcement-for-next-release}

This section is used to pre-announce the upcoming changes in the future releases. The announced changes are not yet effective but will impact customers. For example, the features are not yet deprecated but impacts the users after deprecation. These updates are provided for planning purpose.

|Area|Feature|Announcement|
|--- |--- |--- |
|Foundation|UI Framework|Adobe is planning to deprecate the Coral UI 2 components in 2019. Coral UI 3 was introduced with AEM 6.2, and AEM 6.5 is fully based on Coral 3. Adobe recommends customers and partners that have build custom UIs with Coral 2 to refactored them to Coral 3. Adobe is providing a tool to convert Coral 2 dialogs to Coral 3 - [Read more](/help/sites-developing/modernization-tools.md).|
-->
