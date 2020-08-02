---
title: General Release Notes for [!DNL Adobe Experience Manager] 6.5
description: '[!Adobe Experience Manager DNL] 6.5 notas que describen la información de la versión, las novedades, cómo instalar y las listas de cambio detalladas.'
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 61%

---


# General Release Notes for [!DNL Adobe Experience Manager] 6.5{#general-release-notes-for-adobe-experience-manager}

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] |
|---|---|
| Versión | 6.5 |
| Tipo | Versión principal |
| Fecha de disponibilidad general | 8 de abril de 2019 |
| Actualizaciones recomendadas | Consulte [AEM actualizaciones](https://helpx.adobe.com/es/experience-manager/aem-releases-updates.html)recientes. |

### Trivia {#trivia}

The release cycle for this version of [!DNL Adobe Experience Manager] started April 4, 2018, went through 23 iterations of quality assurance and bug fixing, and ended on March 28th, 2019. La cantidad total de problemas relacionados con los clientes, incluidas las mejoras y nuevas características corregidas en esta versión, es de 1345. 

[!DNL Adobe Experience Manager] 6.5 está disponible en general desde el 8 de abril de 2019.

![Pantalla de inicio de AEM 6.5](/help/assets/assets/aem65-login-v4.png)

## Novedades {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 es una versión de actualización a la base de código [!DNL Adobe Experience Manager] 6.4. Proporciona funciones nuevas y mejoradas, correcciones importantes para los clientes, mejoras de alta prioridad y correcciones generales de errores orientadas a la estabilidad del producto. It also includes [!DNL Adobe Experience Manager] 6.4 Service Pack releases up to SP4.

La lista siguiente proporciona información general, mientras que las páginas subsiguientes lista los detalles completos.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

Lista completa de cambios en [AEM Foundation](/help/release-notes/wcm-platform.md).

The platform of [!DNL Adobe Experience Manager] 6.5 build on top of updated versions of the OSGi-based framework (Apache Sling and Apache Felix) and the Java Content Repository: Apache Jackrabbit Oak 1.10.2.

Quickstart utiliza Eclipse Jetty 9.4.15 como motor de servlet.

#### Compatibilidad con Java  {#java-support}

* Nueva compatibilidad con Java 11, así como para Java 8.
* Para obtener un rendimiento óptimo, anule los valores GC predeterminados con otros valores. For more information, see the [install and update](/help/sites-deploying/custom-standalone-install.md) section.
* Las actualizaciones de mantenimiento de Java 11 y Java 8 se distribuyen por Adobe para el uso del cliente en proyectos relacionados con AEM, cuando no están disponibles públicamente desde Oracle.

#### Desarrollo de Java {#java-development}

* There are now [two versions of the Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies), a recommended version with public interfaces that are not marked for deprecation, as well as a version that includes interfaces marked for deprecation.

#### Interfaz de usuario {#user-interface}

Se han realizado varias mejoras en la interfaz de usuario para que sea más productiva y fácil de usar.

* Nueva interfaz de administración de permisos para usuarios y grupos.
* Las vistas de columna ahora solo cargan las entradas que son visibles en la pantalla y solo cargarán más cuando el usuario comience a desplazarse por el documento. Las vistas de lista y de tarjeta se incluyen a partir de la versión 6.0 (mejoradas en la versión 6.4).
* Las vistas de columna ahora incluyen el estado del flujo de trabajo para las páginas y recursos, cuando corresponda.
* La acción [Seleccionar todo](/help/sites-authoring/basic-handling.md#select-all) es una forma rápida de ejecutar una acción en todas las páginas o recursos de la misma carpeta.
* La acción [Seleccionar todo](/help/sites-authoring/basic-handling.md#select-all) intenta realizar la acción en todas las páginas o recursos, no solo en el contenido cargado. Se muestra un cuadro de diálogo de advertencia si la acción no se actualiza para gestionar acciones masivas.

>[!CAUTION]
>
>Adobe no tiene previsto realizar más mejoras en la interfaz de usuario clásica. AEM 6.5 tiene la interfaz de usuario clásica incluida y los clientes que actualicen desde versiones anteriores pueden seguir utilizándola. Tenga en cuenta que la interfaz de usuario clásica será totalmente compatible mientras esté en desuso. [Obtener más información](/help/sites-deploying/ui-recommendations.md).

#### Búsqueda e indexación {#indexing-and-search}

* La búsqueda en Oak ahora admite facetas dinámicas. Por ejemplo: el carril de filtro en la búsqueda de recursos muestra la cantidad estimada de resultados.
* QueryBuilder se ha ampliado para proporcionar resultados con facetas dinámicas.

#### Actualización {#upgrade}

* La actualización directa a la versión AEM 6.5 es compatible con los clientes que ejecutan AEM 6.2, 6.3 y 6.4. Los clientes que utilizan 5.x o 6.0/6.1 y que quieran utilizar la actualización, primero tienen que actualizar a la versión 6.4 y después a la 6.5, o bien deben realizar la transferencia del contenido entre instancias directamente a AEM 6.5.

#### Proyectos y flujos de trabajo {#projects-and-workflows}

* El nuevo editor del modelo de flujo de trabajo introducido en la versión 6.4 se ha mejorado para incluir más operaciones, como copiar y publicar, la compatibilidad con variables en los pasos de flujo de trabajo y las mejoras en las divisiones OR y AND.

### [!DNL Experience Manager] Sites {#experience-manager-sites}

Full list of changes in [AEM Sites and Add-ons](/help/release-notes/sites.md).

#### Aplicaciones administradas de una sola página {#managed-single-page-apps}

El Editor de página agrega la capacidad de editar contenido en contexto y componer o diseñar las experiencias procesadas del lado de cliente (también conocido [como SPA Editor](/help/sites-developing/spa-architecture.md)). Las aplicaciones existentes de una sola página creadas con el marco React de JavaScript o Angular se pueden ampliar con el SDK para SJ de AEM para que los profesionales puedan editarlas.

Incluida primero como paquete de AEM 6.4 SP2, la compatibilidad SPA adquiere las siguientes capacidades con AEM 6.5:

* Utilice el Editor de plantillas para editar y configurar los elementos editables de AEM de SPA
* Utilice la administración de varios sitios para crear experiencias de SPA con país, franquicia o con etiqueta blanca

#### Administración de contenido sin encabezado {#headless-content-management}

AEM tiene la capacidad de entregar el contenido en diversos formatos y desde varios niveles de la pila. Some have been around since 2008 with the [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) and [POST Servlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html). Content Services ([Sling Model Exporter](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/develop-sling-model-exporter.html)) se ha introducido en AEM 6.3 y es el método que usa el SDK de AEM SJ para completar las aplicaciones de página única. La [API HTTP para recursos](/help/assets/mac-api-assets.md) es una API CRUD, que se amplió para AEM 6.5.

Nuevas funciones de API HTTP:

* Se agregó la [compatibilidad con los fragmentos de contenido a la API HTTP para recursos](/help/assets/assets-api-content-fragments.md) para crear, actualizar, leer y eliminar fragmentos.
* Expose lists of Content Fragments via Content Services with the [Content Fragment List Core Component](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html).
* [Biblioteca](https://opensource.adobe.com/aem-core-wcm-components/library.html) de componentes principal que muestra la salida JSON predeterminada de Content Services para cada componente

#### Complemento de pantallas {#screens-add-on}

Diseñe, distribuya y optimice experiencias en todas las pantallas digitales, desde quioscos interactivos hasta la distribución digital.

**Diseño**

* Unifique experiencias y contenido en el sitio web y en las tiendas gracias a la reutilización mejorada del contenido
* Flujos de trabajo de creación y aprobación o publicación sencillos con compatibilidad para lanzamientos
* Edite y ofrezca experiencias interactivas enriquecidas con SPA Editor

**Entregar**

* Compatibilidad ampliada con reproductores multimedia con un sólido funcionamiento en línea y sin conexión (Smart Sync) capaz de escalar incluso a las redes de señalización más amplias.

**Optimizar**

* Personalice el contenido que generan los datos en función de la ubicación o la configuración, mediante marcadores de posición dinámicos.
* La integración de Adobe Analytics en AEM Screens Player se encarga de unificar los detalles obtenidos

For more details on changes to AEM Screens - see the Release Notes in the [AEM Screens User Guide](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html).

### [!DNL Experience Manager Assets] {#experience-manager-assets}

Full list of changes in [AEM 6.5 Assets release notes](/help/release-notes/assets.md).

AEM 6.5 presenta las siguientes capacidades y mejoras para aumentar la productividad de los usuarios de AEM, los roles DAM y las funciones de marketing y creatividad asociadas.

#### Integración con Adobe Creative Cloud {#integration-with-adobe-creative-cloud}

La introducción de [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html) es una experiencia integrada para los usuarios creativos que trabajan en aplicaciones de Adobe Creative Cloud, incluyendo Photoshop, Illustrator e InDesign; asimismo, agiliza la colaboración entre los expertos creativos y los especialistas en mercadotecnia en el proceso de creación de contenido. AEM aplicación de escritorio sigue siendo compatible con las necesidades de los usuarios que trabajan con recursos desde AEM en el escritorio, utilizando cualquier tipo de archivo y cualquier aplicación de escritorio.

Además, AEM se integra con Adobe Stock para ayudar a encontrar, previsualizar, obtener licencias y guardar los recursos de Adobe Stock directamente desde la interfaz de usuario Web de AEM.

![Panel de Asset Link en Photoshop](/help/assets/assets/aem65-assetlink-photoshop.png)

#### Recursos conectados {#connected-assets}

La funcionalidad Recursos conectados está dirigida a implementaciones más grandes con una serie de implementaciones de AEM Sites que necesitan aprovechar los recursos de una implementación DAM de AEM Assets centrales. Permite mejorar la administración en torno a los recursos gestionados de forma centralizada, además de permitir una alta eficacia en el suministro de recursos a las distintas implementaciones de sitios.

### Dynamic Media {#dynamic-media}

Dynamic Media ofrece la creación y entrega de medios enriquecidos mejorada en AEM Assets para ofrecer experiencias de vanguardia inmersivas y personalizadas. Con un único recurso maestro de alta calidad, puede aprovechar el procesamiento avanzado en la nube y puede usar Smart Crop y los mejores visores de su clase para ofrecer las experiencias más atractivas con un rendimiento líder del sector.

Las nuevas funciones son:

* Compatibilidad con auriculares de vídeo y VR de 360°
* Miniaturas de vídeo personalizadas
* Compatibilidad mejorada con accesibilidad
* Protección con vinculación urgente

#### Experiencia de usuario y búsquedas {#user-experience-and-search}

Las mejoras clave le permiten encontrar los recursos adecuados con mayor rapidez, ya que proporcionan facetas de búsqueda dinámica. Asimismo, puede gestionar varios recursos de forma eficaz, ya que estas mejoras le ofrecen la posibilidad de seleccionar todos los recursos de cualquier carpeta o resultados de búsqueda.

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM 6.5 Forms incorpora varias funciones y mejoras nuevas. Los aspectos más destacados incluyen:

* Informes de transacciones para realizar un seguimiento de la cantidad de formularios enviados y documentos procesados
* Mejoras de uso en las comunicaciones interactivas
* Firmas digitales basadas en la nube en formularios adaptables
* Incorporación de formularios adaptables y comunicaciones interactivas en aplicaciones de página única de AEM Sites (SPA).
* Compatibilidad con variables en flujos de trabajo de AEM
* Compatibilidad con el patrón de visualización de datos en las comunicaciones interactivas
* Clasificación de formularios adaptables y tablas de comunicación interactivas
* Validación automatizada de datos de entrada de modelos de datos de formulario

See the [Summary of new features and enhancements in AEM 6.5 Forms](/help/forms/using/whats-new.md) for information about new and improved features and documentation resources.

### [!DNL Experience Manager Communities] {#communitiesreleasenotes}

AEM 6.5 incorpora nuevas funciones y mejoras a Communities. Lo más destacado de esta versión es lo siguiente:

* Se admite el etiquetado de miembros registrados (@mención) durante la edición del contenido que genera el usuario.
* Ahora se admite la mensajería masiva directa a un grupo de miembros.
* Se han desarrollado y agregado filtros personalizados en la interfaz de usuario de moderación masiva. A [sample project](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) demonstrating filtering by tags can be used as a base to develop analogous custom filters.
* La nueva vista de lista se proporciona con una interfaz de usuario mejorada en la moderación masiva.
* Se pueden asignar administradores separados para diferentes sitios de la comunidad y grupos anidados, en lugar de tener un solo administrador en la comunidad.
* Enablement functionality of AEM 6.5 Communities supports [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) engine.
* Puede usar la navegación con teclado en los componentes de habilitación para mejorar la accesibilidad.
* Apache Solr 7.0 es compatible con la configuración de MSRP y DSRP.

For detailed list of changes, see [AEM 6.5 Communities release notes](/help/release-notes/communities-release-notes.md).

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

Puede integrar Livefyre con su instancia de AEM 6.5. Consulte [cómo integrar Livefyre con AEM](https://docs.adobe.com/content/help/en/experience-manager-64/administering/integration/livefyre.html).

### Aprovechar el desarrollo centrado en el cliente {#leverage-customer-focused-development}

Adobe utiliza un modelo de desarrollo centrado en el cliente que le permite contribuir en todas las etapas del proceso de desarrollo, la especificación, el desarrollo y las pruebas. Agradecemos a todos los clientes y socios que hayan contribuido en este proceso.

Adobe cuenta con los procedimientos y procesos necesarios para permitir la recopilación, priorización y seguimiento de la resolución de errores centrada en el cliente y el desarrollo de solicitudes de mejora. The [Adobe Marketing Cloud Support Portal](https://helpx.adobe.com/es/contact/enterprise-support.ec.html) is integrated with the Adobe Enhancement and Defect Tracking System. Las preguntas de los clientes se identifican y resuelven con el Servicio de atención al cliente siempre que es posible. Cuando estas preguntas se envían al departamento de I+D, se recopila toda la información de los clientes y se utiliza para establecer prioridades y elaborar informes. En el desarrollo se da prioridad al soporte pago, los problemas de garantía y las mejoras pagadas por el cliente.

Este proceso de establecimiento de prioridades creó más de 750 cambios orientados al cliente que se solucionaron en AEM 6.5.

## Lista de archivos que forman parte de la versión {#list-of-files-that-are-part-of-the-release}

**Foundation**

* Inicio rápido independiente: `cq-quickstart-6.5.0.jar`.
* Application Server Quickstart: `cq-quickstart-6.5.0.war`.
* Dispatcher 4.3.2 o posterior para los distintos servidores web y plataformas. Consulte vínculo [de descarga](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/getting-started/release-notes.html)
* Plugin para Eclipse IDE ([más información y descarga](/help/sites-developing/aem-eclipse.md))

* Extensión para el editor de texto Brackets ([más información y descarga](/help/sites-developing/aem-brackets.md))
* Dependencias de Maven/Gradle (vínculo[de](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/aem/uber-jar/6.5.0/)descarga)

**Sites**

* Componentes principales (proyecto[](https://github.com/adobe/aem-core-wcm-components)GitHub)
* Implementación de referencia We.Retail ([más información](/help/sites-developing/we-retail.md))
* Arquetipos de proyecto de Maven:

   * for full-stack sites: [GitHub project](https://github.com/adobe/aem-project-archetype)
   * for single-page apps with React/Angular: [GitHub project](https://github.com/adobe/aem-spa-project-archetype)

* AEM Screens Players for various target platforms ([download](https://download.macromedia.com/screens/))

* Modelos de idioma de contenido inteligente. El idioma inglés está preinstalado, pero se pueden descargar más idiomas

   * [Alemán](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [Español](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [Italiano](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [Francés](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* Conjunto de herramientas de modernización de AEM como, por ejemplo, la herramienta de conversión de diálogos. ([proyecto](https://github.com/adobe/aem-modernize-tools)GitHub)

**Assets**

* Paquete para agregar el rasterizador de PDF mejorado ([más información](/help/assets/aem-pdf-rasterizer.md))
* Paquete para agregar compatibilidad ampliada con imágenes RAW ([más información](/help/assets/camera-raw.md))

**Forms**

* [Paquetes para las funciones de AEM Forms](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html)
* [SDK de cliente OSGi de AEM Forms](https://repo.adobe.com/nexus/content/repositories/public/com/adobe/aemfd/aemfd-client-sdk/6.0.80/)

## Idiomas {#languages}

La interfaz de usuario está disponible en los idiomas siguientes:

* Inglés
* Alemán
* Francés
* Español
* Italiano
* Portugués de Brasil
* Japonés
* Chino simplificado
* Chino tradicional (compatibilidad limitada)
* Coreano

[!DNL Experience Manager] 6.5 se ha certificado para GB18030-2005 CITS para que pueda utilizar el estándar de codificación de caracteres chinos.

## Instalar y actualizar {#install-update}

Para conocer los requisitos de configuración, consulte las instrucciones [de instalación](/help/sites-deploying/custom-standalone-install.md).

Para obtener instrucciones detalladas, consulte la documentación [de](/help/sites-deploying/upgrade.md)actualización.

## Plataformas compatibles {#supported-platforms}

Encuentre la matriz completa de plataformas admitidas, incluido el nivel de soporte, en [AEM requisitos](/help/sites-deploying/technical-requirements.md)técnicos de 6.5.

>[!NOTE]
>
>Oracle se ha trasladado a un modelo de Soporte a Largo Plazo (LTS) para productos de Oracle Java SE. Java 9 y 10 son versiones no LTS de Oracle. Consulte [Oracle Java SE support roadmap](https://www.oracle.com/technetwork/java/eol-135779.html). Adobe proporciona compatibilidad con las versiones LTS de Java para que solo se ejecuten AEM en producción. Java 11 es la versión recomendada para utilizar con AEM 6.5.

## Funciones en desuso y eliminadas {#deprecated-and-removed-features}

Adobe evalúa constantemente las capacidades del producto y, con el tiempo, planea sustituir las capacidades con versiones más potentes o decide volver a implementar los elementos seleccionados y así poder estar mejor preparado para futuras expectativas o extensiones.

For [!DNL Adobe Experience Manager] 6.5, [read the list of deprecated and removed capabilities](/help/release-notes/deprecated-removed-features.md). La página también contiene un anuncio previo de próximos cambios y un aviso importante para los clientes que actualizan versiones anteriores.

## Problemas conocidos {#known-issues}

[Lista de problemas conocidos](/help/release-notes/known-issues.md)

### Descarga de productos y asistencia (sitios restringidos) {#product-download-and-support-restricted-sites}

Los siguientes sitios solo están disponibles para los clientes. Si es un cliente y necesita obtener acceso, póngase en contacto con su administrador de cuentas de Adobe.

* [Descarga de productos en Licensing.adobe.com](https://licensing.adobe.com/).

* Actualizaciones, parches y paquetes de productos para obtener funcionalidad adicional en Distribución [de](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)software.

* [Asistencia al cliente mediante Admin Console](https://adminconsole.adobe.com/). Para obtener más información, consulte [Nueva experiencia](https://docs.adobe.com/content/help/en/customer-one/using/home.html)de asistencia al cliente de Adobe.
