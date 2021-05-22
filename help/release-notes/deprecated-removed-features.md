---
title: Funciones obsoletas y eliminadas en la versión 6.5 de Adobe Experience Manager.
description: Notas de versión específicas de las funciones en desuso y eliminadas de Adobe Experience Manager 6.5.
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: d19b203ffe75a5628f350113d4d74a2916beffc8
workflow-type: tm+mt
source-wordcount: '1736'
ht-degree: 43%

---

# Funciones en desuso y eliminadas {#deprecated-and-removed-features}

Adobe evalúa constantemente las capacidades de los productos para renovar o sustituir las funciones más antiguas con alternativas modernas que mejoren el valor general del cliente, siempre teniendo en cuenta la compatibilidad con versiones anteriores.

Para comunicar la inminente eliminación o sustitución de las capacidades de AEM, se aplican las siguientes reglas:

1. Primero se anuncia el desuso. Aunque están en desuso, las funcionalidades aún están disponibles, pero no se han mejorado.
1. La eliminación de las funciones obsoletas se produce en la siguiente versión principal como muy pronto. Se anunciará la fecha real de la eliminación.

Este proceso proporciona a los clientes un ciclo de lanzamiento para adaptar su implementación a una nueva versión o a la siguiente versión de una capacidad en desuso, antes de eliminarla.

## Funciones en desuso {#deprecated-features}

Esta sección detalla las funciones y capacidades en desuso de AEM 6.5. Normalmente, las funciones que se quieren eliminar de una versión futura se establecen primero en desuso y, a continuación, se proporciona una alternativa.

Se recomienda a los clientes que comprueben si utilizan la función o capacidad en su implementación actual, y que planifiquen el cambio de la implementación y usen la alternativa proporcionada.

| Área | Función | Reemplazo |
|---|---|---|
| Ingregación de Creative Cloud | AEM al uso compartido de carpetas de Creative Cloud se introdujo en AEM 6.2 como una forma de proporcionar a los usuarios creativos acceso a los recursos de AEM, de modo que puedan abrirlos en aplicaciones CC y cargar nuevos archivos o guardar cambios en AEM. Adobe Asset Link, la nueva capacidad de la aplicación Creative Cloud, proporciona experiencia de usuario mejorada y un acceso más eficaz a los recursos de AEM directamente desde Photoshop, InDesign e Illustrator. Adobe no tiene previsto realizar más mejoras en la integración del uso compartido de carpetas de Creative Cloud en AEM. Aunque la función se incluye en AEM, se recomienda a los clientes utilizar soluciones alternativas. | Se aconseja a los clientes que cambien a las nuevas funciones de integración de Creative Cloud, como Adobe Asset Link o AEM aplicación de escritorio. |
| Assets | `AssetDownloadServlet` está desactivado de forma predeterminada para las instancias publicadas. Para obtener más información, consulte la [AEM security checklist (lista de comprobación de seguridad de AEM)](/help/sites-administering/security-checklist.md). | Configuración descrita en la [AEM Security checklist (lista de comprobación de seguridad de AEM)](/help/sites-administering/security-checklist.md). |
| Recursos | Si un usuario no tiene permisos suficientes (de lectura y escritura) en `/content/dam/collections`, no puede crear una colección. | Coincidir con la configuración de control de acceso del usuario y comprobar los permisos adecuados. |
| Adobe Search &amp; Promote | La integración con Adobe Search &amp; Promote está en desuso. Adobe no tiene previsto realizar más mejoras en la integración de Search &amp; Promote. Tenga en cuenta que la integración de Search &amp; Promote será totalmente compatible mientras esté en desuso. |  |
| Administrador de etiquetas DTM | La integración con DTM (Dynamic Tag Manager) está en desuso. | Utilice Adobe Experience Platform Launch como administrador de etiquetas. |
| Adobe Target | Con la adición de la capacidad de AEM para conectarse al servicio de Adobe Target mediante la API Adobe Target Standard (Rest API) basada en [!DNL Adobe I/O] en AEM 6.5, la API (XML) de Target Classic está en desuso. | Vuelva a configurar la integración para [utilizar la nueva API](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html). |
| Adobe Target | El uso de la integración basada en `mbox.js` con Adobe Target en AEM está en desuso. | Cambie a utilizar `at.js` 1.x. |
| Comercio | [CIF ](https://github.com/adobe/commerce-cif-api) RESTse proporcionó en 2018 como un conjunto de microservicios para permitir integraciones entre motores de comercio y AEM. Después de que el Adobe adquirió su Magento a mediados de 2018, el Adobe decidió cambiar su enfoque por dos razones. Magento tiene su propio conjunto de API de comercio (REST y GraphQL) y no es recomendable mantener dos conjuntos de API. Las tendencias del mercado indicaron que los clientes se dirigían a GraphQL, ya que es una forma más eficaz de consultar los datos. En 2019, Adobe lanzó el nuevo Commerce Integration Framework utilizando las API de GraphQL de Magento como fuente de verdad. Adobe no tiene previsto realizar ninguna inversión en CIF REST. Se recomienda encarecidamente a los clientes que utilicen la solución de reemplazo. | Para integraciones AEM-Magento, cambie a [AEM tipo de archivo CIF](https://github.com/adobe/aem-cif-project-archetype) y [AEM componentes principales del CIF](https://github.com/adobe/aem-core-cif-components). Consulte Integración de AEM y Magento [mediante Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md). La compatibilidad con integraciones de terceros (que no sean Magento) con el nuevo enfoque está en nuestra hoja de ruta. |
| Componentes (AEM Sites) | Adobe no tiene previsto realizar mejoras adicionales en la mayoría de los componentes de base almacenados en `/libs/foundation/components`. Busque las propiedades `cq:deprecated` y `cq:deprecatedReason` en la carpeta de componentes. AEM 6.5 incluye los componentes de base, y los clientes que actualicen desde versiones anteriores pueden seguir utilizándolos tal cual. Además, los componentes de base son totalmente compatibles, aunque estén en desuso. | Adobe recomienda utilizar los componentes principales para futuros proyectos. Los sitios existentes pueden permanecer tal cual o utilizar el [AEM Grupo de herramientas de modernización](https://github.com/adobe/aem-modernize-tools) para refactorizar el sitio y utilizar los componentes principales. |
| Componentes (AEM Sites) | Los componentes del Importador de diseños `/libs/wcm/designimporter/components` se han marcado como obsoletos a partir de la versión 6.5. Adobe no tiene previsto realizar más mejoras en la implementación del Importador de diseños. | Adobe tiene previsto proporcionar una implementación alternativa del caso de uso en futuras versiones. |
| Foundation | Marco de descarga de Granite. Adobe no tiene previsto realizar más mejoras en el marco de descarga que se introdujo en CQ 5.6.1 para externalizar el procesamiento de recursos. | Adobe trabaja en un marco de descarga nativo de la nube de próxima generación. |
| Desarrolladores | `Hobbes.js`. Adobe no tiene previsto realizar más mejoras en el marco de pruebas de la interfaz de usuario `hobbes.js`. | Adobe recomienda que los clientes utilicen la automatización de Selenium. |
| Desarrolladores | Biblioteca de cliente de la interfaz de usuario de jQuery. Adobe no tiene previsto seguir manteniendo ni actualizando la biblioteca de cliente de la interfaz de usuario de jQuery incluida como parte de la distribución (Quickstart) | Adobe recomienda a los clientes que aún necesitan la interfaz de usuario de jQuery para su código que lo añadan a su base de código de proyecto. |
| Desarrolladores | Biblioteca de cliente de animación de jQuery (`granite.jquery.animation`). Adobe no tiene previsto seguir manteniendo ni actualizando la biblioteca de cliente de animación de jQuery incluida como parte de la distribución (Quickstart) | Adobe recomienda a los clientes que aún necesitan jQuery Animations para su código que lo añadan a su base de código de proyecto. |
| Desarrolladores | Biblioteca de cliente de Handlebars. Adobe no tiene previsto seguir manteniendo ni actualizando la biblioteca de cliente de Handlebars incluida como parte de la distribución (Quickstart) | Adobe recomienda a los clientes que aún necesitan Handlebars para su código que lo añadan a su base de código de proyecto. |
| Desarrolladores | Biblioteca de cliente de Lawnchair. Adobe no tiene previsto seguir manteniendo ni actualizando la biblioteca de cliente de Lawnchair incluida como parte de la distribución (Quickstart) | Adobe recomienda a los clientes que aún necesitan Lawnchair para su código que lo añadan a su base de código de proyecto. |
| Desarrolladores | `Granite.Sling.js` biblioteca de cliente. Adobe no tiene previsto mejorar la biblioteca de cliente de Granite.Sling.js incluida como parte de la distribución (Quickstart) | Adobe recomienda a los clientes que dependen de la capacidad de la biblioteca de refactorizar su código que ya no lo utilicen. |
| Desarrolladores | Usar YUI para comprimir o minimizar las bibliotecas de cliente de JavaScript. Adobe no tiene previsto actualizar la biblioteca de YUI. Hasta AEM 6.4, YUI era el valor predeterminado para minimizar JavaScript con la opción de cambiar a Google Closure Compiler (GCC). A partir de AEM 6.5, la opción GCC es la opción predeterminada. | Adobe recomienda a los clientes que actualicen a AEM 6.5 para cambiar a GCC para su implementación |
| Desarrolladores | Editor de diálogos estándar de interfaz de usuario en CRXDE Lite. Adobe no tiene previsto mejorar el editor de diálogos estándar de interfaz de usuario incluido como parte de la distribución (Quickstart) | No hay reemplazo disponible. |
| Forms | La integración de AEM Forms con AEM Mobile está en desuso. | No hay disponible Sustitución. |  | Desarrolladores | Editor de diálogos estándar de interfaz de usuario en CRXDE Lite. Adobe no tiene previsto mejorar el editor de diálogos estándar de interfaz de usuario incluido como parte de la distribución (Quickstart) | No hay reemplazo disponible. |
| Desarrolladores | Biblioteca de cliente guion/guion bajo. El Adobe no tiene previsto seguir manteniendo ni actualizando la biblioteca de cliente de guion/guion bajo incluida como parte de la distribución (Quickstart) | Adobe recomienda a los clientes que aún necesitan Lodash/underscore para su código que lo añadan a su base de código de proyecto. |

## Funciones eliminadas {#removed-features}

Esta sección enumera las funciones y capacidades que se han eliminado de AEM 6.5. Las versiones anteriores indicaban que estas funciones estaban en desuso.

| Área | Función | Reemplazo |
|--- |--- |--- |
| Integración con [!DNL Experience Cloud] | Puede sincronizar los recursos con [!DNL Experience Cloud] mediante una configuración mediante [!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] antes se llamaba  [!DNL Adobe Marketing Cloud]. | Si tiene alguna consulta, [póngase en contacto con el Servicio de atención al cliente de Adobe](https://www.adobe.com/account/sign-in.supportportal.html). |
| Analytics Activity Map | La versión de Activity Map que está incluida en AEM. | Debido a los cambios de seguridad de la API de Adobe Analytics, ya no es posible utilizar la versión de Activity Map incluida en AEM. Utilice el [complemento Activity Map proporcionado por Adobe Analytics](https://docs.adobe.com/content/help/es-ES/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.translate.html). |
| Integraciones | La integración de ExactTarget se ha eliminado de la distribución predeterminada (Quickstart) y ya no está disponible. | Sin reemplazo. |
| Integraciones | La integración de la API de Salesforce Force se ha eliminado de la distribución predeterminada (Quickstart) y ahora es un paquete adicional para instalar desde [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | La función aún está disponible. |
| Forms | Se ha eliminado la compatibilidad con el servicio Adobe Central Migration Bridge, ya que el producto Adobe Central ya no es compatible. | Sin reemplazo. |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Sin reemplazo. |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Sin reemplazo |
| Forms | La actualización de un solo salto de LiveCycle ES4 SP1 a AEM 6.5 Forms en JEE no está disponible | Consulte [rutas de actualización disponibles](../forms/using/upgrade.md) en la documentación de actualización de AEM Forms. |
| Forms | Se ha eliminado la compatibilidad con clústeres basados en UPD de AEM Forms en JEE | Solo puede usar clustering basado en TCP en AEM Forms en JEE. Si actualiza un servidor de multidifusión UDP de una versión anterior a AEM 5.5 Forms en JEE, realice configuraciones manuales para cambiar a clúster de gemfire basado en TCP. Para obtener instrucciones detalladas, consulte [Actualización a AEM formularios 6.5 en JEE](../forms/using/upgrade-forms-jee.md) |
| Desarrolladores | Se ha eliminado Firebug Lite de la distribución predeterminada (Quickstart) | Usar las consolas de desarrollador incorporadas en el navegador |
| Desarrolladores | Elimine la compatibilidad con `customJavaScriptPath` en el Administrador de bibliotecas de clientes HTML. | Sin reemplazo |
| [!DNL Assets] | La función de descarga de recursos se ha eliminado en [!DNL Adobe Experience Manager] 6.5. | No hay reemplazo disponible. |
| Caché | `system/console/slingjsp` elimina ya no está disponible en AEM 6.5. | Classes y Slightly cache se almacenan bajo el paquete Apache Sling Commons FileSystem ClassLoader . Puede comprobar el número de paquete en la consola web de AEM y eliminar la carpeta de caché directamente del sistema de archivos (`crx-quickstart/launchpad/felix/bundle<ID>`). |

## Anuncio previo de la próxima versión {#pre-announcement-for-next-release}

Esta sección se utiliza para anunciar previamente los próximos cambios en las próximas versiones. Los cambios anunciados aún no son efectivos, pero afectarán a los clientes. Por ejemplo, las funciones aún no están en desuso, pero afectan a los usuarios después de su desuso. Estas actualizaciones se proporcionan con fines de planificación.

| Área | Función | Anuncio |
|--- |--- |--- |
| Foundation | Marco de interfaz de usuario | Adobe tiene previsto dejar de utilizar los componentes de Coral UI 2 en 2019. Coral UI 3 se ha introducido con AEM 6.2 y AEM 6.5 se basa completamente en Coral 3. Adobe recomienda a los clientes y socios que hayan creado interfaces de usuario personalizadas con Coral 2 que las actualicen a Coral 3. Adobe proporciona una herramienta para convertir los cuadros de diálogo de Coral 2 a Coral 3 [Más información](/help/sites-developing/modernization-tools.md). |
