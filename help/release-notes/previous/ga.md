---
title: Notas de la versión generales para [!DNL Adobe Experience Manager] 6,5
description: '[!DNL Adobe Experience Manager]Las notas de 6.5 describen la información de la versión, las novedades, la instalación y las listas de cambios detalladas.'
source-git-commit: 9b15215a68495a800e94a58b523e1b7baa0c0203
workflow-type: tm+mt
source-wordcount: '4696'
ht-degree: 53%

---

# Notas de la versión generales para [!DNL Adobe Experience Manager] 6,5{#general-release-notes-for-adobe-experience-manager}

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] |
|---|---|
| Versión | 6.5 |
| Tipo | Versión principal |
| Fecha de disponibilidad general | 8 de abril de 2019 |
| Actualizaciones recomendadas | Consulte [AEM actualizaciones recientes](https://helpx.adobe.com/es/experience-manager/aem-releases-updates.html). |

### Trivia {#trivia}

El ciclo de lanzamiento de esta versión de [!DNL Adobe Experience Manager] a partir del 4 de abril de 2018, pasó por 23 iteraciones de control de calidad y corrección de errores, y finalizó el 28 de marzo de 2019. La cantidad total de problemas relacionados con los clientes, incluidas las mejoras y nuevas características corregidas en esta versión, es de 1345. 

[!DNL Adobe Experience Manager] 6.5 está disponible desde el 8 de abril de 2019.

![Pantalla de inicio de AEM 6.5](/help/assets/assets/aem65-login-v4.png)

## Novedades {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 es una versión de actualización a [!DNL Adobe Experience Manager] base de código 6.4. Proporciona funciones nuevas y mejoradas, correcciones importantes para los clientes, mejoras de alta prioridad y correcciones generales de errores orientadas a la estabilidad del producto. También incluye [!DNL Adobe Experience Manager] Versiones de Service Pack 6.4 hasta SP4.

La lista siguiente proporciona información general, mientras que en las páginas siguientes se incluyen todos los detalles.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

La plataforma de [!DNL Adobe Experience Manager] 6.5 se basa en versiones actualizadas del marco basado en OSGi (Apache Sling y Apache Felix) y el repositorio de contenido Java: Apache Jackrabbit Oak 1.10.2.

Quickstart utiliza Eclipse Jetty 9.4.15 como motor de servlet.

#### Compatibilidad con Java  {#java-support}

* Nueva compatibilidad con Java 11, así como para Java 8.
* Para obtener un rendimiento óptimo, anule los valores GC predeterminados con otros valores. Para obtener más información, consulte la [instalar y actualizar](/help/sites-deploying/custom-standalone-install.md) para obtener más información.
* Las actualizaciones de mantenimiento de Java 11 y Java 8 se distribuyen por Adobe para el uso del cliente en proyectos relacionados con AEM, cuando no están disponibles para el público desde el Oracle.

#### Desarrollo de Java {#java-development}

* Ahora hay [dos versiones de Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies), una versión recomendada con interfaces públicas que no están marcadas para su desaprobación, así como una versión que incluye interfaces marcadas para su desaprobación.

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

#### Buscar e indexar {#indexing-and-search}

* La búsqueda en Oak ahora admite facetas dinámicas. Por ejemplo, el carril de filtro de la búsqueda de recursos muestra la cantidad estimada de resultados.
* QueryBuilder se ha ampliado para proporcionar resultados con facetas dinámicas.

#### Actualización {#upgrade}

* La actualización directa a la versión AEM 6.5 es compatible con los clientes que ejecutan AEM 6.2, 6.3 y 6.4. Los clientes que utilizan 5.x o 6.0/6.1 y que quieran utilizar la actualización, primero tienen que actualizar a la versión 6.4 y después a la 6.5, o bien deben realizar la transferencia del contenido entre instancias directamente a AEM 6.5.
* El procedimiento de actualización es el mismo en la versión 6.5.
* Adobe admite las funciones de compatibilidad retroactiva, de evaluación de la complejidad de las actualizaciones y las actualizaciones sostenibles introducidas en la versión 6.4. Se han realizado actualizaciones específicas de la versión en las áreas en las que era necesario.
* Se ha simplificado el paquete del detector de patrones y habrá un paquete que evaluará las actualizaciones a la versión 6.5 para las versiones de origen disponibles.
* Para obtener más información sobre el procedimiento de actualización, consulte la [documentación de actualización](/help/sites-deploying/upgrade.md).

#### Proyectos y flujos de trabajo {#projects-and-workflows}

* El nuevo editor de modelos de flujo de trabajo introducido en la versión 6.4 se ha mejorado para incluir más operaciones, como copiar y publicar, la compatibilidad con variables en los pasos del flujo de trabajo y se ha mejorado `OR` y `AND` divisiones.

#### Repositorio {#repository}

* Adobe Experience Manager 6.5 se basa en versiones actualizadas de la arquitectura creada a partir de OSGi (Apache Sling y Apache Felix) y el repositorio de contenido Java: Apache Jackrabbit Oak 1.10.2.
* Para obtener una descripción general de los problemas corregidos, consulte [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) y [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>La nueva versión de Oak Segment Tar disponible a partir de la versión 6.3 de AEM requiere realizar una migración del repositorio. Este paso es obligatorio si actualiza desde una versión anterior de TarMK o si desea cambiar la nueva Tar de segmento de otro tipo de persistencia. Para obtener más información sobre las ventajas de la nueva barra de segmentos, consulte la [Preguntas frecuentes sobre la migración a Oak Segment Tar](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

#### OSGI {#osgi}

* Se agregaron las bibliotecas de utilidades OSGi Promises y Converter .

#### Seguridad {#security}

* Se agregó la caducidad de la contraseña para el usuario administrador.

#### Servidor web {#web-server}

* La distribución Quickstart utiliza Eclipse Jetty 9.4.15 como motor servlet (AEM 6.4 incluido con 9.3.22).

### [!DNL Experience Manager] Sites {#experience-manager-sites}

#### Aplicaciones administradas de una sola página {#managed-single-page-apps}

El Editor de página agrega la capacidad de editar contenido en contexto y componer o diseñar las experiencias procesadas del lado de cliente (también conocido [como SPA Editor](/help/sites-developing/spa-architecture.md)). Las aplicaciones existentes de una sola página creadas con el marco React de JavaScript o Angular se pueden ampliar con el SDK para SJ de AEM para que los profesionales puedan editarlas.

Incluida primero como paquete de AEM 6.4 SP2, la compatibilidad SPA adquiere las siguientes capacidades con AEM 6.5:

* Utilice el Editor de plantillas para editar y configurar los elementos editables de AEM de SPA
* Utilice Multi-site Management para crear experiencias de SPA con país, franquicia o marca blanca

#### Administración de contenido sin encabezado {#headless-content-management}

AEM tiene la capacidad de entregar el contenido en diversos formatos y desde varios niveles de la pila. Algunos han existido desde el 2008 con el [GET de Sling](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) y [POST Servlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html). Content Services ([Sling Model Exporter](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=es)) se ha introducido en AEM 6.3 y es el método que usa el SDK de AEM SJ para completar las aplicaciones de página única. La [API HTTP para recursos](/help/assets/mac-api-assets.md) es una API CRUD, que se amplió para AEM 6.5.

Nuevas funciones de API HTTP:

* Se agregó la [compatibilidad con los fragmentos de contenido a la API HTTP para recursos](/help/assets/assets-api-content-fragments.md) para crear, actualizar, leer y eliminar fragmentos.
* Exponga listas de fragmentos de contenido a través de los servicios de contenido con la variable [Componente principal de la lista de fragmentos de contenido](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html).
* [Biblioteca de componentes principales](https://opensource.adobe.com/aem-core-wcm-components/library.html) que muestra la salida JSON de Content Services predeterminada para cada componente

#### Complemento de pantallas {#screens-add-on}

Diseñe, distribuya y optimice experiencias en todas las pantallas digitales, desde quioscos interactivos hasta la distribución digital.

* Unifique experiencias y contenido en el sitio web y en las tiendas gracias a la reutilización mejorada del contenido
* Flujos de trabajo de creación y aprobación o publicación sencillos con compatibilidad para lanzamientos
* Edite y ofrezca experiencias interactivas enriquecidas con SPA Editor
* Uso de lanzamientos para planificar futuros cambios en el contenido de señalización
* Reproducción limitada en un canal de secuencias
* Crear automáticamente una estructura de proyecto utilizando un archivo de origen como una hoja de Excel
* Compatibilidad ampliada con reproductores multimedia con un sólido funcionamiento en línea y sin conexión (Smart Sync) capaz de escalar incluso a las redes de señalización más amplias.
* Personalice el contenido que generan los datos en función de la ubicación o la configuración, mediante marcadores de posición dinámicos.
* La integración de Adobe Analytics en AEM Screens Player se encarga de unificar los detalles obtenidos

Para obtener más información sobre los cambios en AEM Screens, consulte las Notas de la versión en la [Guía del usuario de AEM Screens](https://docs.adobe.com/content/help/es-ES/experience-manager-screens/user-guide/aem-screens-introduction.html).

#### Desarrollo de componentes y plantillas {#component-amp-template-development}

* Arquetipo de proyecto Maven 18 (o superior) para proyectos nuevos; consulte [Github para ver las notas de versión](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases).
* Arquetipo de proyecto Maven 1.0.6 (o superior) de aplicaciones de página única para proyectos nuevos; consulte [Github para ver las notas de versión](https://github.com/adobe/aem-spa-project-archetype/releases).
* Versión 1.4 de HTL; consulte [Github para ver las notas de versión](https://github.com/adobe/htl-spec/releases/tag/1.4).

   * operador &quot;in&quot; para cadenas, matrices y objetos:

      ```html
      ${'a' in 'abc’}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * Declaraciones de variables con data-sly-set :
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * Parámetros de control de lista y repetición: inicio, paso, final:
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * Identificadores para data-sly-unwrap:

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * Compatibilidad con números negativos

* Componentes principales 2.3.2 (o superior); consulte [Github para ver las notas de versión](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases).
* Sistema de cuadrícula para contenedores de diseño; consulte [Github](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* Administrador de Clientlib: se ha hecho que Google Closure Compiler sea predeterminado en la minificación de clientlibs de JavaScript (el valor predeterminado anterior era Yahoo YUI) y se ha actualizado Google Closure Compiler a la versión v20190121
* Editor de plantillas y políticas

   * Cree y edite plantillas para aplicaciones de página única que utilicen el SDK para JS (también denominado SPA Editor)

* Sitio de referencia We.Retail 4.0; consulte [Github para ver las notas de versión](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* Kit de herramientas para actualizar los sitios existentes a fin de aprovechar las últimas funciones del editor, consulte [Repositorio de Github](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM incluye la versión 1.12.4 de la biblioteca jQuery para proporcionar la máxima compatibilidad con el código personalizado existente. Adobe ha realizado varias modificaciones para solucionar problemas de seguridad conocidos.

#### Administración de sitios {#site-administration}

* La barra de [Referencia](/help/sites-authoring/author-environment-tools.md#references) tiene una nueva sección para mostrar los vínculos internos que conducen a la página seleccionada. Esto resulta útil cuando se planea utilizar o eliminar una página sin conexión, para ver qué páginas necesitan ajustes antes de desconectarlas.
* La [vista de lista](/help/sites-authoring/basic-handling.md#list-view) tiene una nueva columna de flujo de trabajo que muestra el estado de la página cuando se encuentra en un flujo de trabajo.
* En las [propiedades de la página](/help/sites-authoring/editing-page-properties.md), ahora es posible buscar recursos existentes al asignar una miniatura a la página (pestaña Miniaturas).

#### Editor de página {#page-editor}

* Permite la edición y composición en contexto de experiencias de aplicaciones de página única construidas con componentes React y Angular del lado del cliente que aprovechan el SDK de JS (también llamado SPA Editor)
* El modo de scaffolding solo se muestra si la página tiene una página de scaffolding configurada.

#### Fragmentos de contenido y editor {#content-fragments-amp-editor}

* La nueva barra de [Anotaciones](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) en el Editor de fragmentos de contenido se puede usar para realizar comentarios generales y ver comentarios en el texto (también se muestra en la barra de cronología)
* Posibilidad de establecer el tipo de contenido predeterminado de un elemento de texto multilínea en un [Modelo de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md) para texto simple, texto enriquecido o Markdown
* Agregue [comentarios o anotaciones](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) seleccionando texto en RTE (vista de pantalla completa)
* [Comparar versiones](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) de un fragmento de contenido en paralelo a través de la barra de referencia
* El informe de descarga de recursos ahora muestra los fragmentos de contenido correspondientes
* Agregue la [compatibilidad con fragmentos de contenido a la API HTTP de recursos](/help/assets/assets-api-content-fragments.md) mediante /api.json. Existen API para crear, actualizar, leer y eliminar fragmentos de contenido.

#### Fragmentos de experiencias {#experience-fragments}

* Se ha mejorado la indexación de los [fragmentos de experiencias](/help/sites-authoring/experience-fragments.md) para que su contenido se encuentre al buscar las páginas donde estos se utilizan
* La opción [Export to Target](/help/sites-administering/experience-fragments-target.md) (Exportar a destino) ahora permite enviar el fragmento de experiencia como JSON (el valor predeterminado es HTML) o ambos

#### Traducción {#translation}

* Simplifique la creación de proyectos de traducción mediante Project Masters
* Simplifique la ejecución de proyectos de traducción estableciendo el estado de los trabajos de traducción en &quot;Aprobado&quot; de forma predeterminada
* Permita la actualización de las páginas traducidas con cambios en la memoria de traducción de terceros
* Permita exportar los trabajos de traducción en formato JSON
* Actualización de la integración de Microsoft Translation para utilizar la API V3

#### Administración de varios sitios (MSM) {#multi-site-management-msm}

* Para las configuraciones de lanzamiento que utilizan PushOnModify, obtendrá un proceso de gestión mejorado de la operación de movimiento de página para evitar un estado incoherente
* La creación de una nueva página dentro de la estructura livecopy ahora creará por defecto una página independiente
* Utilice las funciones de MSM en aplicaciones de página única que utilicen el SDK para JS (también denominado SPA Editor)

#### Lanzamientos {#launches}

* Nuevo flujo de trabajo de revisión y aprobación de lanzamientos, y la capacidad de promover únicamente las páginas de lanzamiento aprobadas
* Se agregó una [opción en la interfaz de usuario para eliminar el lanzamiento después de realizar el paso de promoción](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

#### Simulación y segmentación de contenido {#content-targeting-simulation}

* Se ha actualizado la capa de datos de ContextHub y el motor de reglas del lado del cliente JavaScript para utilizar jQuery 3 de forma predeterminada.

#### AEM y Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>Actualmente:
>
>* Solo `at.js 1.x` es compatible si utiliza Adobe Target como motor de targeting en AEM consola Actividades .
>
>* Ambas `at.js. 1.x` y `at.js 2.x` son compatibles si utiliza la exportación de fragmentos de experiencias a Target y ejecuta actividades en la consola de Target.


* La integración de Adobe Target ahora puede utilizar la API de Target Standard. Las versiones anteriores de AEM utilizan la API HTTP de Target Classic, que ahora está en desuso.
* Adobe Target `mbox.js` se incluye la versión 63. Adobe recomienda cambiar la implementación a `at.js` v1.x.
* `at.js` ya se incluye la versión 1.5.0. Adobe recomienda usar [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) a la provisión `at.js` v1.x en el sitio.

#### AEM y Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` Se incluye H.27.5. Adobe recomienda cambiar la implementación a `AppMeasurement.js`
* `AppMeasurement.js` Se incluye la versión 1.8.0. Adobe recomienda utilizar [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) para aprovisionar AppMeasurement.js en el sitio.

#### AEM y comercio {#aem-commerce}

Las mejoras en Commerce Integration Framework se encuentran en un ciclo de lanzamiento más rápido desde AEM 6.4. [Obtenga más información aquí](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html).

#### Complemento de Communities {#communities-add-on}

Para obtener la última versión, consulte la [Implementación de comunidades](/help/communities/deploy-communities.md) de la documentación.

##### Mejoras en el compromiso de la comunidad {#enhancements-to-community-engagement}

**Compatibilidad con @mentions**
AEM Communities ahora permite a los usuarios registrados etiquetar (mencionar) otros miembros registrados para atraer su atención, en Contenido generado por el usuario. A continuación, se notificará a los miembros etiquetados (mencionados) con una vinculación profunda al contenido que creó el usuario correspondiente. Sin embargo, los usuarios pueden optar por activar o desactivar las notificaciones web y de correo electrónico.

![Compatibilidad con menciones](/help/release-notes/assets/at-mentions.png)

Los usuarios de la comunidad no necesitan buscar su nombre, apellido o nombre de usuario para ver si alguien los ha contactado o si necesita su atención. Además, permite que los autores de UGC busquen respuestas de usuarios específicos registrados que pueden abordar el problema y añadir entradas.

Los administradores de la comunidad deben **Habilitar mención** en componentes de comunidad para permitir que los usuarios registrados utilicen la funcionalidad en esos componentes.

**Mensajería de grupo**

Los miembros registrados de la comunidad ahora pueden enviar mensajes masivos directos a los grupos mediante una sola composición de correo electrónico, en lugar de enviar el mismo mensaje individualmente a los miembros del grupo. Para permitir [mensajería de grupo](/help/communities/configure-messaging.md), habilite ambas instancias de [Servicio de operaciones de mensajería](/help/communities/messaging.md#group-messaging).

![Mensajería de grupo](/help/release-notes/assets/group-messaging.png)

##### Mejoras de la moderación masiva {#enhancements-to-bulk-moderation}

Filtros personalizados en la moderación masiva

[Filtros personalizados](/help/communities/moderation.md#custom-filters) ahora se puede desarrollar y agregar a la interfaz de usuario de Moderación masiva.

En [Github](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) encontrará un [proyecto de muestra](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) del filtrado mediante etiquetas. Este proyecto se puede utilizar como base para desarrollar filtros personalizados similares.

![Filtros personalizados](/help/release-notes/assets/custom-tag-filter.png)

**Vista de lista en la moderación masiva**

Se ha proporcionado una nueva vista de lista con una interfaz de usuario mejorada con la moderación masiva, para mostrar las entradas del contenido que haya creado el usuario.

![Moderación masiva en la vista de lista](/help/release-notes/assets/list-view-moderation.png)

##### Mejoras en la administración del sitio y del grupo {#enhancements-to-site-and-group-management}

**Autor del sitio y administradores del grupo**

Communities, AEM 6.5 y otras versiones posteriores le permiten realizar operaciones con la administración (y gestión) descentralizada de distintos sitios de comunidad y grupos anidados. Las organizaciones que alojan varios sitios de comunidad y grupos anidados ahora pueden seleccionar miembros para funciones de administrador del lado de autor en el momento de la creación del sitio (y del grupo).

![Administrador del sitio](/help/release-notes/assets/site-admin.png)

Los administradores del sitio pueden crear un grupo en cualquier nivel de jerarquía y convertirse en administradores predeterminados. Posteriormente, otros administradores del grupo pueden eliminarlos. Los administradores del grupo pueden administrar su grupo G1 y crear un subgrupo anidado en G1.

##### Mejoras en la activación {#enhancements-to-enablement}

**Compatibilidad con SCORM 2017.1**

La funcionalidad de habilitación de AEM 6.5 Communities es compatible con el modelo de referencia de objetos de contenido compartible [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) motor.

* Compatibilidad con la navegación por teclado en los componentes de habilitación
* Los componentes de habilitación (por ejemplo, Catálogo y Reproducción de cursos, Asignaciones, Biblioteca de archivos) en AEM Communities admiten la navegación mediante el teclado para mejorar la accesibilidad.

##### Otras mejoras {#other-enhancements}

* Compatibilidad con Solr 7
* AEM 6.5 Communities es compatible con la versión Apache Solr 7.0 de la plataforma de búsqueda al configurar MSRP y DSRP.

### [!DNL Experience Manager Assets] {#experience-manager-assets}

AEM 6.5 presenta las siguientes capacidades y mejoras para aumentar la productividad de los usuarios de AEM, los roles DAM y las funciones de marketing y creatividad asociadas.

#### Integración con [!DNL Adobe Creative Cloud] y flujos de trabajo creativos {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] ofrece varias formas de integración con y permite compartir recursos para usarlos en flujos de trabajo en los que los equipos creativos, de marketing o de negocios colaboran estrechamente.[!DNL Adobe Creative Cloud] [!DNL Experience Manager] 6.5 continúa mejorando la integración y la optimiza para ofrecer más oportunidades y agilizar los métodos existentes.

Siga leyendo para conocer las funcionalidades e integraciones específicas de [!DNL Experience Manager] 6.5 que puede utilizar para ofrecer una mejor compatibilidad con los casos de uso de velocidad de contenido.

##### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] fortalece la colaboración entre creativos y especialistas en marketing en el proceso de creación de contenido. Los creativos pueden acceder al contenido almacenado en [!DNL Experience Manager Assets], sin dejar las aplicaciones con las que están más familiarizados. Los creativos pueden examinar, buscar, extraer y registrar recursos sin problemas mediante el panel en la aplicación de [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]y [!DNL Adobe InDesign] aplicaciones.

[!DNL Adobe Asset Link] es parte de [Creative Cloud para empresas](https://www.adobe.com/creativecloud/business/enterprise.html) oferta. Para obtener más información, incluida la configuración necesaria de su [!DNL Experience Manager] implementación, consulte [Vínculo de recurso de Adobe](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html).

![Buscar recursos en Adobe Photoshop](/help/release-notes/assets/asset_search_photoshop.png)

##### [!DNL Adobe Stock] integración {#stock}

Su organización puede utilizar su [!DNL Adobe Stock] plan empresarial dentro de [!DNL Experience Manager Assets] para garantizar que los recursos con licencia estén disponibles en general para sus proyectos creativos y de marketing. Puede encontrar, obtener una vista previa y obtener una licencia rápidamente [!DNL Adobe Stock] recursos que se guardan en Experience Manager, utilizando las potentes funciones DAM de [!DNL Experience Manager].

[!DNL Adobe Stock]El servicio proporciona a diseñadores y empresas acceso a millones de fotos, vectores, ilustraciones, vídeos, plantillas y recursos 3D de alta calidad, verificados y libres de derechos de autor para todos sus proyectos creativos.

Para obtener más información, consulte [Uso de recursos de Adobe Stock en Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md).

![Vista previa de la imagen y la licencia de Adobe Stock desde Experience Manager Assets](/help/release-notes/assets/stock_image_preview_license_options.png)

*Figura: Vista previa [!DNL Adobe Stock] imagen y licencia desde [!DNL Experience Manager Assets].*

![Buscar y filtrar las imágenes de Adobe Stock con licencia en Experience Manager](/help/release-notes/assets/aem-search-filters2.jpg)

*Figura: Busque y filtre la licencia [!DNL Adobe Stock] imágenes en [!DNL Experience Manager].*

##### Referencias dinámicas en [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] se usa en [!DNL Adobe InDesign] los archivos son dinámicos. Las referencias se actualizan automáticamente si los recursos a los que se hace referencia se mueven en el repositorio. Para obtener más información, consulte [administración de recursos compuestos](/help/assets/managing-linked-subassets.md).

#### Capacidades de Brand Portal {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] le ayuda a adquirir, controlar y distribuir de forma eficaz y segura los recursos aprobados a agencias o proveedores externos y a usuarios de negocios internos en todos los dispositivos. Asimismo, le permite mejorar la eficiencia del uso compartido de recursos, acelera el tiempo de comercialización de esos recursos y elimina el riesgo de uso indebido y los accesos no autorizados.

Para obtener más información, consulte [Novedades de Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=es).

#### Recursos conectados {#connectedassets}

En las grandes empresas se puede distribuir la infraestructura necesaria para crear sitios web. A veces, las capacidades de creación de sitios web y los recursos digitales necesarios residen en distintos silos.

[!DNL Experience Manager Sites] ofrece capacidades de crear páginas web y es el sistema de gestión de recursos digitales (DAM) que proporciona los recursos necesarios para los sitios web.[!DNL Experience Manager Assets] [!DNL Experience Manager] ahora es compatible con el caso de uso anterior mediante la integración de [!DNL Sites] y [!DNL Assets]. Consulte [configuración y uso de la función Recursos conectados](/help/assets/use-assets-across-connected-assets-instances.md).

![Arrastrar un recurso desde un [!DNL Experience Manager] implementación en un [!DNL Sites] página de un [!DNL Experience Manager] implementación](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*Figura: Arrastrar un recurso desde un [!DNL Experience Manager] implementación en un [!DNL Sites] en una página diferente [!DNL Experience Manager] implementación.*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] ofrece una creación y entrega de medios enriquecidos mejorada en [!DNL Experience Manager Assets] para impulsar experiencias de vanguardia inmersivas y personalizadas. Al cargar un único recurso principal de alta calidad y usar los visores y el procesamiento avanzado en la nube de Adobe, puede entregar cualquier combinación de representaciones sobre la marcha para respaldar la estrategia de medios de su organización.

Para obtener más información sobre las nuevas [!DNL Dynamic Media] características, consulte [Notas de la versión de Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html).

##### Compatibilidad con vídeo 360 {#video-support}

Administre sus archivos de vídeo de 360 directamente en [!DNL Experience Manager] uso de visores de vanguardia para ofrecer experiencias de VR a equipos de escritorio, dispositivos móviles y auriculares de realidad virtual. Para obtener más información, consulte [Uso del vídeo 360](/help/assets/360-video.md).

##### Miniaturas de vídeo personalizadas {#custom-video-thumbnails}

Ahora puede personalizar las miniaturas de sus recursos de vídeo utilizando fotogramas del propio vídeo u otro contenido almacenado en DAM. Para obtener instrucciones adicionales, consulte [Acerca de las miniaturas de vídeo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

##### Mejoras de accesibilidad {#accessibility-enhancements}

[!DNL Dynamic Media] los visores ahora admiten funciones de accesibilidad mejoradas como compatibilidad con Aria, lectores de pantalla y texto alternativo. Para obtener más información, consulte [Guía de referencia de visores](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html).

#### Mejora de la opción de búsqueda {#experience-enhancement-for-searching}

[!DNL Experience Manager] A partir de la versión 6.5, los especialistas en marketing pueden descubrir los recursos deseados con mayor rapidez desde la página de resultados de búsqueda. Las facetas de búsqueda se actualizan con el número de recursos incluso antes de aplicar el filtro de búsqueda. Ver la cantidad esperada con el filtro ayuda a los usuarios a navegar a través de los resultados de búsqueda de forma eficaz. Para obtener más información, consulte [Buscar recursos en el Experience Manager](/help/assets/search-assets.md).

![Ver el número de recursos sin filtrar los resultados de búsqueda en las facetas de búsqueda](/help/assets/assets/asset_search_results_in_facets_filters.png)

*Figura: Consulte el número de recursos sin filtrar los resultados de búsqueda en las facetas de búsqueda.*

#### Mejora de la capacidad de uso {#usability-enhancement}

Ahora puede seleccionar todos los recursos cargados dentro de una carpeta o desde un resultado de búsqueda en una sola vez. Esto le permite administrar varios recursos rápidamente. La casilla de verificación selecciona todos los recursos que se ajustan al escenario, por ejemplo, un resultado de búsqueda, y no solo los recursos que están visibles en la variable [!DNL Experience Manager] interfaz.

![Utilice la opción Seleccionar todo para seleccionar todos los recursos cargados en un solo clic.](/help/release-notes/assets/select-all-in-aem-assets.gif)

*Figura: Utilice la opción Seleccionar todo para seleccionar todos los recursos cargados en un solo clic.*

#### Mejoras en los metadatos {#metadata-enhancements}

[!DNL Assets] permite crear esquemas de metadatos para carpetas de recursos, que definen el diseño y los metadatos que se muestran en las páginas de propiedades de las carpetas. Ahora puede asignar un esquema de metadatos de carpeta a una carpeta existente o al crear una carpeta. Para obtener más información, consulte [Esquema de metadatos de carpeta](/help/assets/metadata-config.md#folder-metadata-schema).

Al especificar los metadatos en cascada, las opciones se pueden cargar desde un archivo JSON en tiempo de ejecución, en lugar de escribir manualmente en el formulario. Para obtener más información, consulte [metadatos en cascada](/help/assets/metadata-schemas.md#cascading-metadata).

#### Mejoras en los informes {#reporting-enhancements}

Los fragmentos de contenido y los vínculos compartidos se incluyen ahora en el informe descargado. Para obtener más información, consulte los [informes de recursos](/help/assets/asset-reports.md).

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

Consulte la [Resumen de las nuevas funciones y mejoras de AEM 6.5 Forms](/help/forms/using/whats-new.md) para obtener información sobre las funciones nuevas y mejoradas y los recursos de documentación.

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

Puede integrar Livefyre con su instancia de AEM 6.5. Consulte [integración de Livefyre con AEM](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/livefyre.html).

### Aprovechar el desarrollo centrado en el cliente {#leverage-customer-focused-development}

Adobe utiliza un modelo de desarrollo centrado en el cliente que le permite contribuir en todas las etapas del proceso de desarrollo, la especificación, el desarrollo y las pruebas. Agradecemos a todos los clientes y socios que hayan contribuido en este proceso.

Adobe cuenta con los procedimientos y procesos necesarios para permitir la recopilación, priorización y seguimiento de la resolución de errores centrada en el cliente y el desarrollo de solicitudes de mejora. La variable [Portal de asistencia al Experience Manager](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) está integrado con el sistema de seguimiento de defectos y mejora del Adobe. El equipo de asistencia al cliente identifica y resuelve las preguntas de los clientes siempre que es posible. Cuando estas preguntas se envían al departamento de I+D, se recopila toda la información de los clientes y se utiliza para establecer prioridades y elaborar informes. En el desarrollo se da prioridad a la asistencia de pago, los problemas de garantía y las mejoras pagadas por el cliente.

Este proceso de establecimiento de prioridades creó más de 750 cambios orientados al cliente que se solucionaron en AEM 6.5.

## Lista de archivos que forman parte de la versión {#list-of-files-that-are-part-of-the-release}

**Foundation**

* Inicio rápido independiente: `cq-quickstart-6.5.0.jar`.
* Inicio rápido del servidor de aplicaciones: `cq-quickstart-6.5.0.war`.
* Dispatcher 4.3.2 o posterior para los distintos servidores web y plataformas. Consulte [vínculo de descarga](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html)
* Plugin para Eclipse IDE ([más información y descarga](/help/sites-developing/aem-eclipse.md))

* Extensión para el editor de texto Brackets ([más información y descarga](/help/sites-developing/aem-brackets.md))
* Dependencias de Maven/Gradle ([vínculo de descarga](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/))

**Sites**

* Componentes principales ([Proyecto de GitHub](https://github.com/adobe/aem-core-wcm-components))
* Implementación de referencia We.Retail ([más información](/help/sites-developing/we-retail.md))
* Arquetipos de proyecto de Maven:

   * para sitios de pila completa: [Proyecto de GitHub](https://github.com/adobe/aem-project-archetype)
   * para aplicaciones de una sola página con React/Angular: [Proyecto de GitHub](https://github.com/adobe/aem-spa-project-archetype)

* Reproductores de AEM Screens para varias plataformas de destino ([descargar](https://download.macromedia.com/screens/))

* Modelos de idioma de contenido inteligente. El idioma inglés está preinstalado, pero se pueden descargar más idiomas

   * [Alemán](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [Español](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [Italiano](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [Francés](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* Conjunto de herramientas de modernización de AEM como, por ejemplo, la herramienta de conversión de diálogos. ([Proyecto de GitHub](https://github.com/adobe/aem-modernize-tools))

**Assets**

* Paquete para agregar el rasterizador de PDF mejorado ([más información](/help/assets/aem-pdf-rasterizer.md))
* Paquete para agregar compatibilidad ampliada con imágenes RAW ([más información](/help/assets/camera-raw.md))

**Forms**

* [Paquetes para las funciones de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [SDK de cliente AEM Forms OSGi](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

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

Para conocer los requisitos de configuración, consulte [instrucciones de instalación](/help/sites-deploying/custom-standalone-install.md).

Para obtener instrucciones detalladas, consulte [documentación de actualización](/help/sites-deploying/upgrade.md).

## Plataformas compatibles {#supported-platforms}

Encuentre la matriz completa de plataformas compatibles, incluido el nivel de soporte en [AEM 6.5 requisitos técnicos](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Oracle se ha trasladado a un modelo de soporte a largo plazo (LTS) para los productos Oracle Java SE. Java 9 y 10 son versiones no LTS por Oracle. Consulte [Plan de soporte de Oracle Java SE](https://www.oracle.com/technetwork/java/eol-135779.html). Adobe es compatible con las versiones LTS de Java para que solo se ejecuten AEM en producción. Java 11 es la versión recomendada para usar con AEM 6.5.

## Funciones en desuso y eliminadas {#deprecated-and-removed-features}

Adobe evalúa constantemente las capacidades del producto y, con el tiempo, planea sustituir las capacidades con versiones más potentes o decide volver a implementar los elementos seleccionados y así poder estar mejor preparado para futuras expectativas o extensiones.

Para [!DNL Adobe Experience Manager] 6.5, [leer la lista de funcionalidades obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md). La página también contiene un anuncio previo de próximos cambios y un aviso importante para los clientes que actualizan versiones anteriores.

## Problemas conocidos {#known-issues}

### Plataforma {#platform}

* Se informa de un problema en el que CRX-Quickstart y su contenido se eliminan.

   En cada una de estas acciones, asegúrese de que la propiedad `htmllibmanager.fileSystemOutputCacheLocation` no es una cadena vacía:

   1. Llamar a `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. Actualización a AEM 6.5.
   3. Ejecutando &quot;migración de contenido diferido&quot; en AEM 6.5.

   A [Base de conocimientos](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) este artículo está disponible con más detalles y la solución para este problema.

* Si utiliza JDK 11 con AEM instancia 6.5, algunas de las páginas podrían aparecer en blanco después de implementar algunos paquetes. El siguiente mensaje de error aparece en el archivo de registro:

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

Para resolver este error:

1. Detenga la instancia de AEM. Vaya a `<aem_server_path_on_server>crx-quickstart\conf` y abra el `sling.properties` archivo. Adobe recomienda realizar una copia de seguridad de este archivo.

1. Buscar `org.osgi.framework.bootdelegation=`. Agregar `jdk.internal.reflect,jdk.internal.reflect.*` propiedades para mostrar el resultado como.

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. Guarde el archivo y reinicie la instancia de AEM.

## Sites {#sites}

* **Uso de versiones de página**: Si se ha movido una página, ya no puede realizar una vista previa de ninguna versión realizada antes del movimiento.

### Assets {#assets}

* **Buscar:** La búsqueda no devuelve ningún resultado si la cadena de búsqueda contiene espacios iniciales ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Esquema de metadatos de carpeta**: después de añadir un botón de opciones, los campos Id. y Valor no se procesan como se esperaba y la funcionalidad de eliminación no funciona. (CQ-4261144)
* Al cambiar el nombre de un recurso, no se puede utilizar un espacio en blanco en el nombre del recurso. (CQ-4266403)

### Forms {#forms}

* Cuando AEM Forms está instalado en el sistema operativo Linux, la firma digital con el módulo de seguridad de hardware no funciona. (CQ-4266721)
* (AEM Forms solo en WebSphere) La opción **Forms Workflow**> **Task Search** (Búsqueda de tareas) no devuelve ningún resultado si se busca un **administrador** con el **nombre de usuario** como criterio de búsqueda. (CQ-4266457)

* AEM Forms no puede convertir archivos TIF y TIFF con compresión de JPEG a documentos PDF. (CQ-4265972)
* Las opciones **AEM Forms Assets Scanner** (Escáner de recursos de AEM Forms) y **Letter to Interactive Communication Migration** (Carta para la migración de comunicaciones interactiva) no funcionan en la página de **migración de AEM Forms**. (CQ-4266572)

* (Solo JBoss 7) Cuando actualiza de una versión anterior a AEM 6.5 Forms y la versión anterior tenía procesos (.lca) que creaban y utilizaban una copia del proceso de envío predeterminado o del procesamiento predeterminado, HTML5 Forms que utilizaba esos procesos (.lca) no realiza las acciones requeridas. (CQ-4243928)
* En un formulario adaptable, cuando se invoca un servicio de modelo de datos de formulario desde el editor de reglas para actualizar dinámicamente los valores del componente de elección de imágenes, los valores del componente de elección de imágenes no se actualizan. (CQ-4254754)
* El instalador de AEM Forms Designer requiere la versión de 32 bits de [Paquete de tiempo de ejecución redistribuible de Visual C++ 2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads) y [Paquetes de tiempo de ejecución redistribuibles de Visual C++ 2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Asegúrese de que los paquetes de ejecución redistribuibles anteriores estén instalados antes de iniciar la instalación. (CQ-4265668)

* El Generador de PDF no admite la autenticación basada en tarjetas inteligentes.  Cuando un administrador habilita la directiva de grupo `Interactive Logon: Require Smart card` en un servidor de Windows, todos los usuarios existentes del Generador de PDF se invalidan.

* Cuando se configura un formulario adaptable para actualizar dinámicamente los valores de un componente y se accede a la instancia de publicación que aloja el formulario a través del controlador, la funcionalidad para actualizar dinámicamente los valores de un campo deja de funcionar. Para resolver el problema, en la instancia de publicación, abra CRXDE, vaya a `/libs/fd/af/runtime/clientlibs/guideChartReducer`y cree la propiedad que aparece a continuación.

   * Nombre: allowProxy
   * Tipo: Boolean (booleano)
   * Valor: true (verdadero)
   * Protegido: false (falso)
   * Obligatorio: false (falso)
   * Varios: false (falso)
   * Creación automática: False

   La propiedad permite que las bibliotecas de cliente en la carpeta de ejecución accedan a los proxy. (CQ-4268679)

* Cuando se inicia AEM Forms, la variable `SAX Security Manager could not be setup` aparece la advertencia.
* Al abrir un PDF protegido con AEM Forms Document Security en un Apple iOS o iPadOS que ejecute Adobe Acrobat Reader versión 20.10.00.
* Cuando se envía un formulario que contiene un campo de carga de HTML estándar desde un dispositivo iOS de Apple, a veces el contenido del archivo no se envía y se recibe un archivo de 0 bytes en el otro extremo. Apple iOS 15.1 proporciona una solución para el problema.

## Descarga de productos y asistencia (sitios restringidos) {#product-download-and-support-restricted-sites}

Los siguientes sitios solo están disponibles para los clientes. Si es un cliente y necesita obtener acceso, póngase en contacto con su administrador de cuentas de Adobe.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/).

* Actualizaciones, parches y paquetes de productos para obtener funcionalidad adicional en [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html).

* [Asistencia al cliente mediante Admin Console](https://adminconsole.adobe.com/). Para obtener más información, consulte [Nueva experiencia de asistencia al cliente de Adobe](https://docs.adobe.com/content/help/en/customer-one/using/home.html).
