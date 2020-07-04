---
title: Funciones obsoletas y eliminadas en la versión Adobe Experience Manager 6.5.
description: Notas de versión específicas de las funciones en desuso y eliminadas de Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 29f8e59e3fc9d3c089ee3b78c24638cd3cd2e96b
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 45%

---


# Funciones en desuso y eliminadas {#deprecated-and-removed-features}

Adobe evalúa constantemente las capacidades de los productos para renovar o sustituir las funciones más antiguas con alternativas modernas que mejoren el valor general del cliente, siempre teniendo en cuenta la compatibilidad con versiones anteriores.

Para comunicar la inminente eliminación o sustitución de las funciones de AEM, se aplican las siguientes reglas:

1. Primero se anuncia el desuso. Aunque están en desuso, las capacidades siguen estando disponibles, pero no se han mejorado.
1. La eliminación de funciones obsoletas se produce en la siguiente versión principal como muy pronto. Se anunciará la fecha real de la eliminación.

Este proceso proporciona a los clientes un ciclo de lanzamiento para adaptar su implementación a una nueva versión o a la siguiente versión de una capacidad en desuso, antes de eliminarla.

## Funciones en desuso {#deprecated-features}

Esta sección detalla las funciones y capacidades en desuso de AEM 6.5. Normalmente, las funciones que se quieren eliminar de una versión futura se establecen primero en desuso y, a continuación, se proporciona una alternativa.

Se recomienda a los clientes que comprueben si utilizan la función o capacidad en su implementación actual, y que planifiquen el cambio de la implementación y usen la alternativa proporcionada.

| Área | Función | Reemplazo |
|---|---|---|
| Ingregación de Creative Cloud | AEM to Creative Cloud Folder Sharing se introdujo en AEM 6.2 como forma de proporcionar a los usuarios creativos acceso a los recursos de AEM, de modo que puedan abrirlos en aplicaciones CC y cargar nuevos archivos o guardar cambios en AEM. Adobe Asset Link, la nueva capacidad de la aplicación Creative Cloud, proporciona experiencia de usuario mejorada y un acceso más eficaz a los recursos de AEM directamente desde Photoshop, InDesign e Illustrator. Adobe no tiene previsto realizar más mejoras en la integración del uso compartido de carpetas de Creative Cloud en AEM. Aunque la función se incluye en AEM, se recomienda a los clientes utilizar soluciones alternativas. | Se recomienda a los clientes que cambien a las nuevas funciones de integración de Creative Cloud, incluidas Adobe Asset Link o la aplicación de escritorio AEM. Consulte Prácticas recomendadas de integración de AEM y Creative Cloud para obtener más información. |
| Assets | `AssetDownloadServlet` está desactivado de forma predeterminada para las instancias publicadas. Para obtener más información, consulte la [AEM security checklist (lista de comprobación de seguridad de AEM)](/help/sites-administering/security-checklist.md). | Configuración descrita en la [AEM Security checklist (lista de comprobación de seguridad de AEM)](/help/sites-administering/security-checklist.md). |
| Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Coincidir con la configuración de control de acceso del usuario y comprobar los permisos adecuados. |
| Adobe Search &amp; Promote | La integración con Adobe Search &amp; Promote está en desuso. Adobe no tiene previsto realizar más mejoras en la integración de Search &amp; Promote. Tenga en cuenta que la integración de Search &amp; Promote será totalmente compatible mientras esté en desuso. |  |
| Administrador de etiquetas DTM | La integración con DTM (Dynamic Tag Manager) está en desuso. | Utilice Adobe Experience Platform Launch como administrador de etiquetas. |
| Adobe Target | Al añadir la capacidad de AEM para conectarse al servicio de Adobe Target mediante la API Adobe Target Standard basada en Adobe E/S (API de Rest) en AEM 6.5, el método de la API de Target Classic (XML) quedará en desuso. | Reconfigure the integration to [use the new API](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html). |
| Adobe Target | Using the `mbox.js` based integration with Adobe Target in AEM is deprecated. | Switch to use `at.js` 1.x. |
| Comercio | [CIF REST](https://github.com/adobe/commerce-cif-api) se proporcionó en 2018 como un conjunto de microservicios para permitir integraciones entre AEM y motores de comercio. Después de que Adobe adquirió Magento a mediados de 2018, Adobe decidió cambiar su enfoque por dos razones. Magento tiene su propio conjunto de API de comercio (REST y GraphQL) y no es recomendable mantener dos conjuntos de API. Las tendencias del mercado indicaban que los clientes avanzaban hacia GraphQL, ya que es una forma más eficiente de consultar datos. En 2019, Adobe lanzó el nuevo Commerce Integration Framework utilizando las API GraphQL de Magento como fuente de verdad. Adobe no planea realizar ninguna inversión adicional en CIF REST. Se recomienda encarecidamente a los clientes que utilicen la solución de reemplazo. | Para las integraciones de AEM-Magento, cambie a [AEM CIF Archetype](https://github.com/adobe/aem-cif-project-archetype) y [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components). See AEM and Magento integration [using Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md). El apoyo a integraciones de terceros (distintas de Magento) con el nuevo enfoque está en nuestra hoja de ruta. |
| Componentes (AEM Sites) | Adobe no tiene previsto realizar mejoras adicionales en la mayoría de los componentes de base almacenados en `/libs/foundation/components`. Look for the `cq:deprecated` and `cq:deprecatedReason` property in the component folder. AEM 6.5 incluye los componentes de base y los clientes que actualicen desde versiones anteriores pueden seguir utilizándolos tal cual. Además, los componentes de base son totalmente compatibles aunque estén en desuso. | Adobe recomienda utilizar los componentes principales para futuros proyectos. Existing sites can remain as is or use the [AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools) to refactor the site to use Core Components. |
| Componentes (AEM Sites) | Design Importer Components `/libs/wcm/designimporter/components` have been marked as deprecated starting 6.5. Adobe does not plan to make further enhancements to that implementation of the design importer. | Adobe planea ofrecer una implementación alternativa del caso de uso en futuras versiones. |
| Foundation | Marco de descarga de Granite. Adobe no planea realizar más mejoras en el marco de descarga que se introdujo en CQ 5.6.1 para externalizar el procesamiento de recursos. | Adobe trabaja en un marco de descarga nativo de la nube de próxima generación. |
| Desarrolladores | `Hobbes.js`. Adobe does not plan to make further enhancements to the `hobbes.js` user interface testing framework. | Adobe recomienda que los clientes utilicen la automatización Selenium. |
| Desarrolladores | Biblioteca de cliente de la interfaz de usuario de jQuery. Adobe no tiene previsto seguir manteniendo ni actualizando la biblioteca de cliente de la interfaz de usuario de jQuery incluida como parte de la distribución (Quickstart) | Adobe recomienda a los clientes que aún necesitan la IU de jQuery para que su código se añada a su base de código de proyecto. |
| Desarrolladores | Biblioteca de cliente de jQuery Animation (`granite.jquery.animation`). Adobe no tiene previsto seguir manteniendo ni actualizando la biblioteca de cliente de animación de jQuery incluida como parte de la distribución (Quickstart) | Adobe recomienda a los clientes que aún necesitan jQuery Animations para que su código se añada a su base de código de proyecto. |
| Desarrolladores | Biblioteca de cliente de Handlebars. Adobe no tiene previsto seguir manteniendo ni actualizando la biblioteca de cliente de Handlebars incluida como parte de la distribución (Quickstart) | Adobe recomienda a los clientes que aún necesitan Handlebars para su código que lo añadan a su base de código de proyecto. |
| Desarrolladores | Biblioteca de cliente de Lawnchair. Adobe no tiene previsto seguir manteniendo ni actualizando la biblioteca de cliente de Lawnchair incluida como parte de la distribución (Quickstart) | Adobe recomienda a los clientes que aún necesitan Lawnsilla para su código que lo añadan a su base de código de proyecto. |
| Desarrolladores | `Granite.Sling.js` biblioteca de cliente. Adobe no tiene previsto mejorar la biblioteca de cliente de Granite.Sling.js incluida como parte de la distribución (Quickstart) | Adobe recomienda a los clientes que dependen de la capacidad de la biblioteca para cambiar el factor de su código y dejar de utilizarlo. |
| Desarrolladores | Usar YUI para comprimir o minimizar las bibliotecas de cliente de JavaScript. Adobe no tiene previsto actualizar la biblioteca de YUI. Hasta AEM 6.4, la IU era la predeterminada para reducir el código JavaScript con la opción de cambiar a Google Closure Compiler (GCC). A partir de AEM 6.5, la opción GCC es la opción predeterminada. | Adobe recomienda a los clientes que actualicen a AEM 6.5 para cambiar a GCC para su implementación |
| Desarrolladores | Editor de diálogos estándar de interfaz de usuario en CRXDE Lite. Adobe no tiene previsto mejorar el editor de diálogos estándar de interfaz de usuario incluido como parte de la distribución (Quickstart) | No hay reemplazo disponible. |
| Forms | La integración de AEM Forms con AEM Mobile ya no se utiliza. | No hay sustitutos disponibles. |

## Funciones eliminadas {#removed-features}

Esta sección lista las funciones y funciones que se han eliminado de AEM 6.5. Las versiones anteriores tenían estas capacidades marcadas como obsoletas.

| Área | Función | Reemplazo |
|--- |--- |--- |
| Analytics Activity Map | La versión de Activity Map que está incluida en AEM. | Debido a los cambios de seguridad de la API de Adobe Analytics, ya no es posible utilizar la versión de Activity Map incluida en AEM. Utilice el complemento [Activity Map proporcionado por Adobe Analytics](https://docs.adobe.com/content/help/es-ES/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.translate.html). |
| Integraciones | La integración de ExactTarget se ha eliminado de la distribución predeterminada (QuickStart) y ya no está disponible. | Sin reemplazo. |
| Integraciones | Salesforce Force API integration has been removed from the default distribution (Quickstart) and is now an extra package to install from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | La función aún está disponible. |
| Forms | Se ha eliminado la compatibilidad con el servicio Adobe Central Migration Bridge, ya que el producto Adobe Central ya no es compatible. | Sin reemplazo. |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Sin reemplazo. |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Sin reemplazo |
| Forms | La actualización de un solo salto de LiveCycle ES4 SP1 a AEM 6.5 Forms en JEE no está disponible | Consulte las rutas [de actualización](../forms/using/upgrade.md) disponibles en la documentación de actualización de AEM Forms. |
| Forms | Se ha eliminado la compatibilidad con clústeres basados en UPD de los AEM Forms en JEE | Solo se puede usar clustering basado en TCP en AEM Forms en JEE. Si actualiza un servidor de multidifusión UDP de una versión anterior a AEM 5.5 Forms en JEE, realice configuraciones manuales para cambiar a la agrupación de gemfire basada en TCP. Para obtener instrucciones detalladas, consulte [Actualización a formularios AEM 6.5 en JEE](../forms/using/upgrade-forms-jee.md) |
| Desarrolladores | Se ha eliminado Firebug Lite de la distribución predeterminada (Quickstart) | Usar las consolas de desarrollador incorporadas en el navegador |
| Desarrolladores | Remove `customJavaScriptPath` support in HTML Client Library Manager. | Sin reemplazo |
| [!DNL Assets] | La función de descarga de recursos se elimina en [!DNL Adobe Experience Manager] 6.5. | No hay reemplazo disponible. |
| Caché | `system/console/slingjsp` ya no está disponible en AEM 6.5. | Clases y ligero caché se almacena en el paquete Apache Sling Commons FileSystem ClassLoader. Puede comprobar el número de paquete en la consola web de AEM y quitar la carpeta de caché directamente del sistema de archivos (`crx-quickstart/launchpad/felix/bundle<ID>`). |

## Anuncio previo para la siguiente versión {#pre-announcement-for-next-release}

Esta sección se utiliza para anunciar los próximos cambios en las próximas versiones. Los cambios anunciados aún no son efectivos, pero afectarán a los clientes. Por ejemplo, las funciones aún no están en desuso, pero afectan a los usuarios después de su desaprobación. Estas actualizaciones se proporcionan con fines de planificación.

| Área | Función | Anuncio |
|--- |--- |--- |
| Foundation | Marco de interfaz de usuario | Adobe tiene previsto dejar de utilizar los componentes de Coral UI 2 en 2019. Coral UI 3 se ha introducido con AEM 6.2 y AEM 6.5 se basa completamente en Coral 3. Adobe recomienda a los clientes y socios que hayan creado interfaces de usuario personalizadas con Coral 2 que las actualicen a Coral 3. Adobe proporciona una herramienta para convertir los cuadros de diálogo de Coral 2 a Coral 3 [Más información](/help/sites-developing/dialog-conversion.md). |
