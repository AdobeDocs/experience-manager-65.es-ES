---
title: Notas de la versión generales de [!DNL Adobe Experience Manager] 6,5
description: "[!DNL Adobe Experience Manager] Notas de la versión 6.5 que describen la información de la versión, las novedades, cómo instalar y listas de cambios detalladas."
exl-id: b3d4a527-44ca-4eb6-b393-f3e8117cf1a6
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '4676'
ht-degree: 7%

---

# Notas de la versión generales de [!DNL Adobe Experience Manager] 6,5{#general-release-notes-for-adobe-experience-manager}

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] |
|---|---|
| Versión | 6.5 |
| Tipo | Versión principal |
| Fecha de disponibilidad general | 8 de abril de 2019 |
| Actualizaciones recomendadas | Consulte [AEM Actualizaciones recientes de la](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=es). |

### Trivia {#trivia}

El ciclo de lanzamiento de esta versión de [!DNL Adobe Experience Manager] iniciado el 4 de abril de 2018, pasó por 23 iteraciones de garantía de calidad y corrección de errores, y finalizó el 28 de marzo de 2019. El número total de problemas relacionados con los clientes, incluidas las mejoras y las nuevas funciones, corregidos en esta versión es de 1345.

[!DNL Adobe Experience Manager] 6.5 está disponible en general desde el 8 de abril de 2019.

![AEM Pantalla de inicio de sesión de.5](/help/assets/assets/aem65-login-v4.png)

## Novedades {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 es una actualización de la versión [!DNL Adobe Experience Manager] Código base de 6.4. Proporciona funcionalidades nuevas y mejoradas, correcciones importantes para los clientes, mejoras de alta prioridad y correcciones generales de errores orientadas a la estabilidad del producto. También incluye [!DNL Adobe Experience Manager] Versiones de paquete de servicio de 6.4 hasta SP4.

La lista siguiente proporciona una descripción general, mientras que las páginas siguientes enumeran todos los detalles.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

La plataforma de [!DNL Adobe Experience Manager] 6.5 se basa en las versiones actualizadas del marco basado en OSGi (Apache Sling y Apache Felix) y el repositorio de contenido Java™: Apache Jackrabbit Oak 1.10.2.

Quickstart utiliza Eclipse Jetty 9.4.15 como motor servlet.

#### Compatibilidad con Java™  {#java-support}

* Nueva compatibilidad con Java™ 11 y el ya compatible Java™ 8.
* Para obtener un rendimiento óptimo, reemplace los valores de GC predeterminados por otros valores. Para obtener más información, consulte la [instalar y actualizar](/help/sites-deploying/custom-standalone-install.md) sección.
* Las actualizaciones de mantenimiento de Java™ 11 y Java™ 8 se distribuyen por Adobe AEM para que las utilicen los clientes en proyectos relacionados con el uso de la cuando no están disponibles públicamente desde Oracle.

#### Desarrollo de Java™ {#java-development}

* Ahora hay [dos versiones del Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies), una versión recomendada con interfaces públicas que no están marcadas para desaprobación y una versión que incluye interfaces marcadas para desaprobación.

#### Interfaz de usuario {#user-interface}

Se han realizado varias mejoras en la interfaz de usuario para que sea más productiva y fácil de usar.

* Nueva IU de administración de permisos para usuarios y grupos.
* Ahora, las vistas de columnas solo cargan entradas visibles en la pantalla, y solo cargan más cuando el usuario empieza a desplazarse. La vista de lista y tarjeta ya lo hacía desde la versión 6.0 (mejorada en la 6.4).
* Las vistas de columna ahora incluyen el estado del flujo de trabajo para páginas o recursos cuando corresponde.
* El [Seleccionar todo](/help/sites-authoring/basic-handling.md#select-all) Una acción es una forma rápida de ejecutar una acción con todas las páginas o recursos de la misma carpeta.
* El [Seleccionar todo](/help/sites-authoring/basic-handling.md#select-all) La acción intenta realizar la acción en todas las páginas o recursos, no solo en lo que se ha cargado. Se muestra un cuadro de diálogo de advertencia si la acción no se actualiza para administrar acciones masivas.

>[!CAUTION]
>
>Adobe no tiene previsto realizar más mejoras en la IU clásica. AEM La versión 6.5 de tiene incluida la IU clásica, y los clientes que actualicen desde versiones anteriores pueden seguir utilizándola tal cual. La IU clásica sigue siendo totalmente compatible mientras está en desuso. [Más información](/help/sites-deploying/ui-recommendations.md).

#### Búsqueda e indexación {#indexing-and-search}

* La búsqueda en Oak ahora admite facetas dinámicas. Por ejemplo, el carril de filtro en la búsqueda de recursos muestra el número estimado de resultados.
* QueryBuilder se amplió para proporcionar resultados con facetas dinámicas.

#### Actualizar {#upgrade}

* AEM AEM Se admite la actualización directa in situ a la versión 6.5 de los clientes que ejecutan la versión 6.2, 6.3 y 6.4 de la versión 6.3 de la versión, o la versión 6.5 de la versión, respectivamente. Los clientes que usan 5.x o 6.0/6.1 y desean usar la actualización local deben actualizar primero a 6.4. AEM A continuación, actualice a la versión 6.5 o actualice mediante la transferencia del contenido entre las instancias directamente a la versión 6.5, o bien, actualice la versión a la versión 6.5, o bien actualice el contenido directamente a la versión 6.5.
* El procedimiento de actualización sigue siendo el mismo en 6.5.
* Seguimos admitiendo las funciones de Compatibilidad con versiones anteriores, Evaluación de la complejidad de la actualización y Actualizaciones sostenibles introducidas en la versión 6.4. Se han realizado actualizaciones específicas de la versión en estas áreas donde es necesario.
* El empaquetado Pattern Detector ahora se simplifica. Hay un paquete que evalúa las actualizaciones a 6.5 para las versiones de origen disponibles.
* Para obtener más información sobre el procedimiento de actualización, consulte la [documentación de actualización](/help/sites-deploying/upgrade.md).

#### Proyectos y flujos de trabajo {#projects-and-workflows}

* Se ha mejorado el nuevo editor del Modelo de flujo de trabajo introducido en 6.4 para incluir más operaciones como Copiar y Publicar, Compatibilidad con variables en los pasos del flujo de trabajo y se ha mejorado `OR` y `AND` Particiones.

#### Repositorio {#repository}

* La base de Adobe Experience Manager 6.5 se basa en las versiones actualizadas del marco basado en OSGi (Apache Sling y Apache Felix) y el repositorio de contenido Java™: Apache Jackrabbit Oak 1.10.2.
* Para obtener una descripción general de los problemas corregidos, consulte [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) y [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>AEM La nueva versión de Oak Segment Tar, presente desde la versión 6.3 de la versión, requiere una migración del repositorio. Este paso es obligatorio si está actualizando desde una versión anterior de TarMK o desea cambiar el nuevo Segment Tar de otro tipo de persistencia. Para obtener más información sobre las ventajas del nuevo Segment TAR, consulte la [Preguntas frecuentes sobre la migración a Oak Segment Tar](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

#### OSGI {#osgi}

* Se agregaron las bibliotecas de utilidades Promesas y Convertidor de OSGi.

#### Seguridad {#security}

* Se agregó la caducidad de la contraseña para el usuario administrador.

#### Servidor web {#web-server}

* AEM La distribución de Quickstart utiliza Eclipse Jetty 9.4.15 como motor servlet (6.4 enviado con 9.3.22).

### [!DNL Experience Manager] Sites {#experience-manager-sites}

#### Aplicaciones de una sola página administradas {#managed-single-page-apps}

El editor de páginas añade la capacidad de editar contenido en contexto y componer/diseñar dentro de las experiencias procesadas del lado del cliente (también conocida como [SPA como editor de](/help/sites-developing/spa-architecture.md)). Las aplicaciones de una sola página existentes creadas con React o Angular AEM del marco de JavaScript se pueden ampliar con el SDK de SJ de la aplicación para que los profesionales puedan editar.

AEM AEM SPA Enviado por primera vez como parte de la versión 6.4 SP2, con la versión 6.5 de la versión, la compatibilidad con el servicio de soporte técnico gana las siguientes capacidades:

* AEM SPA Utilice el Editor de plantillas para editar y configurar las partes editables de la que se pueden editar
* SPA Utilice Multi-site Management para crear experiencias de país, franquicia o de marca blanca en el sitio de la comunidad de la comunidad de la marca de la marca de la manera más sencilla

#### Administración de contenido sin encabezado {#headless-content-management}

AEM Puede servir el contenido en varios formatos y desde varios niveles de la pila. Algunos han estado alrededor desde 2008 con el [GET de Sling](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) y [Servlet POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html). Servicios de contenido ([Exportador del modelo Sling](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=en)AEM AEM ) se introdujo en la versión 6.3 de y es el método que usa el SDK de SJ de la aplicación para hidratar las aplicaciones de una sola página. El [API HTTP para Assets](/help/assets/mac-api-assets.md) AEM es una API de CRUD, que se amplió para la versión 6.5 de.

Nuevas funciones de la API HTTP:

* Añadido [Compatibilidad con fragmentos de contenido para la API HTTP para Assets](/help/assets/assets-api-content-fragments.md) para crear, actualizar, leer y eliminar fragmentos.
* Exponer listas de fragmentos de contenido mediante servicios de contenido con [Componente principal de lista de fragmentos de contenido](https://www.aemcomponents.dev).
* [Biblioteca de componentes principales](https://www.aemcomponents.dev) que muestra la salida JSON de Content Services predeterminada para cada componente

#### Complemento de Screens {#screens-add-on}

Diseñe, publique y optimice de forma eficaz las experiencias en todas las pantallas digitales, desde quioscos interactivos hasta anuncios digitales.

* Unifique experiencias y contenido en contenido digital y en tienda con una reutilización de contenido mejorada
* Flujos de trabajo optimizados de creación y aprobación/publicación compatibles con lanzamientos
* SPA Edite y entregue experiencias interactivas enriquecidas con el Editor de experiencias de la interfaz de usuario de
* Uso de lanzamientos para planificar futuros cambios de contenido para el contenido de señalización
* Reproducción medida en un canal de secuencia
* Crear automáticamente una estructura de proyecto utilizando un archivo de origen como una hoja de Excel
* Mayor compatibilidad con reproductores de contenidos gracias a la sólida operación on-line y offline (sincronización inteligente), capaz de ampliarse incluso a las redes de anuncios más grandes.
* Personalice por ubicación o configuración del contenido activado por datos mediante marcadores de posición dinámicos.
* Perspectivas unificadas impulsadas por la integración de Adobe Analytics en el reproductor de AEM Screens

Para obtener más información sobre los cambios en AEM Screens, consulte las Notas de la versión en la [Guía del usuario de AEM Screens](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=es).

#### Desarrollo de componentes y plantillas {#component-amp-template-development}

* Arquetipo de proyecto Maven 18+ para nuevos proyectos, consulte [GitHub para notas de la versión](https://github.com/adobe/aem-project-archetype/releases).
* Arquetipo de proyecto de aplicación Maven de una sola página 1.0.6+ para nuevos proyectos, consulte [GitHub para notas de la versión](https://github.com/adobe/aem-spa-project-archetype/releases).
* HTL versión 1.4, consulte [GitHub para notas de la versión](https://github.com/adobe/htl-spec/releases/tag/1.4).

   * Operador &quot;in&quot; para cadenas, matrices y objetos:

     ```html
     ${'a' in 'abc'}
     ${100 in myArray}
     ${'a' in myObject}
     ```

   * Declaraciones de variables con data-sly-set :
     `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * Parámetros de control de lista y repetición: inicio, paso, fin:
     `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * Identificadores para data-sly-unwrap:

     ```html
     <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
     text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
     </div>
     ```

   * Compatibilidad con números negativos

* Componentes principales 2.3.2+, consulte [GitHub para notas de la versión](https://github.com/adobe/aem-core-wcm-components/releases).
* Sistema de cuadrícula para el contenedor de diseño, consulte [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* Clientlib Manager: ha configurado Google Closure Compiler de forma predeterminada para la minificación de clientlibs JavaScript (el valor predeterminado antiguo era Yahoo YUI) y ha actualizado Google Closure Compiler a la versión v20190121
* Editor de plantillas y directivas

   * SPA Cree y edite plantillas para aplicaciones de una sola página que utilicen el SDK de JS (también denominado Editor de código de tiempo de ejecución (también denominado Editor de código de tiempo de la aplicación)).

* Sitio de referencia We.Retail 4.0; consulte [GitHub para notas de la versión](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* Kit de herramientas para actualizar los sitios existentes y utilizar las últimas funciones del editor, consulte [Repositorio de GitHub](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM incluye la versión 1.12.4 de la biblioteca jQuery para proporcionar la máxima compatibilidad con el código personalizado existente. Se han realizado modificaciones por Adobe para solucionar problemas de seguridad conocidos.

#### Administración del sitio {#site-administration}

* El [Referencia](/help/sites-authoring/author-environment-tools.md#references) el carril tiene una nueva sección para la lista de vínculos internos que apuntan a la página seleccionada. Esto resulta útil cuando se planea desconectar o eliminar una página, para ver qué páginas deben ajustarse antes de desconectarlas.
* El [vista de lista](/help/sites-authoring/basic-handling.md#list-view) tiene una nueva columna de flujo de trabajo que muestra el estado cuando la página está en un flujo de trabajo.
* En el [propiedades de página](/help/sites-authoring/editing-page-properties.md)Ahora, es posible buscar recursos existentes al asignar una miniatura a la página (pestaña Miniatura).

#### Editor de página {#page-editor}

* Permitir la edición y composición en contexto de experiencias de aplicación de una sola página con componentes de cliente de React y Angular SPA que utilizan el SDK de JS (también denominado Editor de)
* El modo Andamiaje solo se muestra si la página tiene una página de andamiaje configurada.

#### Fragmentos de contenido y editor {#content-fragments-amp-editor}

* Nuevo [Anotaciones](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) carril en el Editor de fragmentos de contenido para realizar comentarios generales y ver los realizados dentro del texto (también se muestran en el carril Cronología)
* Capacidad para establecer el tipo de contenido predeterminado de un elemento de texto multilínea en una [Modelo de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md) a texto simple, texto enriquecido o markdown
* Añadir [comentario/anotaciones](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) seleccionando texto en RTE (vista de pantalla completa)
* [Comparar versiones](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) Creación de un fragmento de contenido en paralelo mediante un carril de referencia
* El informe de descarga de recursos ahora muestra los fragmentos de contenido en consecuencia
* Añadir [Compatibilidad con fragmentos de contenido para la API HTTP de Assets](/help/assets/assets-api-content-fragments.md) vía /api.json. Existen API para crear, actualizar, leer y eliminar fragmentos de contenido.

#### Fragmentos de experiencias {#experience-fragments}

* Se ha mejorado la indexación de [Fragmentos de experiencias](/help/sites-authoring/experience-fragments.md), por lo que su contenido se encuentra en la búsqueda de páginas donde se utilizan.
* El [Exportar a Target](/help/sites-administering/experience-fragments-target.md) Ahora, la opción le permite enviar el fragmento de experiencia como JSON (el valor predeterminado es HTML) o ambos.

#### Traducción {#translation}

* Simplifique la creación de proyectos de traducción utilizando Project Masters.
* Simplifique la ejecución de proyectos de traducción estableciendo los trabajos de traducción en el estado aprobado de forma predeterminada.
* Permitir la actualización de páginas traducidas con cambios en la memoria de traducción de terceros.
* Permite exportar trabajos de traducción en formato JSON.
* Actualice la integración de traducción de Microsoft® para utilizar la API V3.

#### Administración de varios sitios (MSM) {#multi-site-management-msm}

* Para las configuraciones de despliegue que utilizan PushOnModify, se debe gestionar mejor la operación de movimiento de página para evitar estados incoherentes.
* Al crear una página dentro de la estructura de Live Copy, se crea una página independiente de forma predeterminada.
* SPA Utilice funciones de MSM en aplicaciones de una sola página que utilicen el SDK de JS (también denominado Editor de)

#### Lanzamientos {#launches}

* Nuevo flujo de trabajo de revisión y aprobación para lanzamientos y capacidad de promocionar solo las páginas de lanzamiento aprobadas
* Añadido [en la interfaz de usuario para elegir eliminar el lanzamiento justo después del paso de promoción](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

#### Segmentación y simulación de contenido {#content-targeting-simulation}

* La capa de datos de ContextHub y el motor de reglas del lado del cliente de JavaScript se han actualizado para utilizar jQuery 3 de forma predeterminada.

#### AEM y ADOBE TARGET {#aem-amp-adobe-target}

>[!CAUTION]
>
>Actualmente:
>
>* Solo `at.js 1.x` es compatible si utiliza Adobe Target AEM como motor de segmentación en la consola Actividades de.
>
>* Ambos `at.js. 1.x` y `at.js 2.x` son compatibles si utiliza la exportación de fragmentos de experiencias a Target y ejecuta actividades en la consola de Target.

* La integración de Adobe Target ahora utiliza la API de Target Standard. AEM Las versiones anteriores de utilizan la API de HTTP de Target Classic, que ya está en desuso.
* Adobe Target `mbox.js` se incluye la versión 63 de. El Adobe recomienda encarecidamente que cambie la implementación a `at.js` v1.x.
* `at.js` ya se incluye la versión 1.5.0 de. El Adobe recomienda que utilice [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html) para aprovisionar `at.js` v1.x en el sitio.

#### AEM y ADOBE ANALYTICS {#aem-amp-adobe-analytics}

* `s_code.js` Se incluye H.27.5. El Adobe recomienda cambiar la implementación a `AppMeasurement.js`
* `AppMeasurement.js` Se incluye la versión 1.8.0. El Adobe recomienda que utilice [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html) para aprovisionar AppMeasurement.js en el sitio.

#### AEM Comercio de {#aem-commerce}

Las mejoras realizadas en el Commerce integration framework AEM se encuentran en un ciclo de liberación más rápido desde la versión 6.4 de la. [Obtenga más información aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/magento.html).

#### Complemento de Communities {#communities-add-on}

Para obtener la última versión, consulte la [Implementación de comunidades](/help/communities/deploy-communities.md) de la documentación.

##### Mejoras en la participación de la comunidad {#enhancements-to-community-engagement}

**@Mentions asistencia**
AEM Communities ahora permite a los usuarios registrados etiquetar (mencionar) a otros miembros registrados para atraer su atención, en el contenido generado por el usuario. A continuación, se notifica a los miembros etiquetados (mencionados), con un vínculo profundo al contenido generado por el usuario correspondiente. Sin embargo, los usuarios pueden optar por deshabilitar o habilitar las notificaciones por correo electrónico y web.

![Soporte de menciones de At](/help/release-notes/assets/at-mentions.png)

Los usuarios de la comunidad no necesitan buscar su nombre, apellidos o nombre de usuario para ver si alguien se ha puesto en contacto con ellos o necesita su atención. Además, permite a los autores de UGC buscar respuestas de usuarios registrados específicos que puedan abordar mejor el problema y agregar entradas.

Los administradores de la comunidad deben **Habilitar la mención** en componentes de la comunidad para permitir que los usuarios registrados utilicen la funcionalidad en esos componentes.

**Mensajería de grupo**

Los miembros de la comunidad registrados ahora pueden enviar mensajes directos de forma masiva a los grupos a través de una sola composición de correo electrónico, en lugar de enviar el mismo mensaje individualmente a los miembros del grupo. Para permitir [mensajería de grupo](/help/communities/configure-messaging.md), habilite ambas instancias de [Servicio de operaciones de mensajería](/help/communities/messaging.md#group-messaging).

![Agrupar mensaje](/help/release-notes/assets/group-messaging.png)

##### Mejoras en la moderación masiva {#enhancements-to-bulk-moderation}

Filtros personalizados en moderación masiva

[Filtros personalizados](/help/communities/moderation.md#custom-filters) ahora se puede desarrollar y agregar a la interfaz de usuario de moderación masiva.

A [proyecto de ejemplo](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) que muestra el filtrado mediante etiquetas está disponible en [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter). Este proyecto puede utilizarse como base para desarrollar filtros personalizados análogos.

![Filtros personalizados](/help/release-notes/assets/custom-tag-filter.png)

**Vista de lista en la moderación masiva**

Se ha proporcionado una nueva vista de lista con una interfaz de usuario mejorada en la moderación masiva para mostrar las entradas de contenido generado por el usuario.

![Moderación masiva en la vista de listas](/help/release-notes/assets/list-view-moderation.png)

##### Mejoras en la administración de sitios y grupos {#enhancements-to-site-and-group-management}

**Administradores de grupos y sitios del lado del autor**

AEM Comunidades, de 6,5 en adelante, permite la administración (y gestión) descentralizada de diferentes sitios y grupos comunitarios/grupos anidados. Las organizaciones que alojan varios sitios de comunidad y grupos anidados ahora pueden seleccionar miembros para roles de administrador en el lado del autor en el momento de la creación del sitio (y del grupo).

![Administrador del sitio](/help/release-notes/assets/site-admin.png)

Los administradores del sitio pueden crear un grupo en cualquier nivel de jerarquía y convertirse en los administradores predeterminados. Estos administradores pueden ser eliminados posteriormente por otros administradores del grupo. Los administradores de grupo pueden administrar su grupo G1 y crear un subgrupo anidado en G1.

##### Mejoras en la habilitación {#enhancements-to-enablement}

**Compatibilidad con SCORM 2017.1**

AEM La funcionalidad de habilitación de las comunidades de 6.5 admite el modelo de referencia de objetos de contenido compartido [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) motor.

* Compatibilidad con la navegación por teclado en componentes de habilitación
* Los componentes de habilitación (por ejemplo, Reproducción de catálogos y cursos, Asignaciones, Biblioteca de archivos) en AEM Communities admiten la navegación mediante el teclado para mejorar la accesibilidad.

##### Otras mejoras {#other-enhancements}

* Compatibilidad con Solr 7
* AEM Las comunidades de 6.5 admiten la versión 7.0 de Apache Solr de la plataforma de búsqueda al configurar MSRP y DSRP.

### [!DNL Experience Manager Assets] {#experience-manager-assets}

AEM AEM.5 presenta las siguientes funciones y mejoras para impulsar la productividad de los usuarios de la aplicación, las funciones de DAM y las funciones creativas y de marketing asociadas de la aplicación.

#### Integración con [!DNL Adobe Creative Cloud] y flujos de trabajo creativos {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] ofrece varias formas de integrar con [!DNL Adobe Creative Cloud] y compartir recursos para utilizarlos en flujos de trabajo en los que los equipos creativos y de marketing o empresariales colaboran estrechamente. [!DNL Experience Manager] 6.5 sigue mejorando la integración y la racionaliza para exponer más oportunidades y racionalizar los métodos existentes.

Siga leyendo para conocer las capacidades e integraciones específicas de [!DNL Experience Manager] 6.5 que puede utilizar para admitir mejor sus casos de uso de velocidad de contenido.

##### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] refuerza la colaboración entre creativos y especialistas en marketing en el proceso de creación de contenido. Los creativos pueden acceder al contenido almacenado en [!DNL Experience Manager Assets], sin salir de las aplicaciones con las que están más familiarizados. Los creativos pueden examinar, buscar, extraer y registrar recursos sin problemas mediante el panel integrado en la aplicación de [!DNL Adobe Photoshop], [!DNL Adobe Illustrator], y [!DNL Adobe InDesign] aplicaciones.

[!DNL Adobe Asset Link] forma parte de [Creative Cloud para empresas](https://www.adobe.com/es/creativecloud/business/enterprise.html) oferta. Para obtener más información al respecto, incluida la configuración necesaria de su [!DNL Experience Manager] implementación, consulte [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html).

![Búsqueda de recursos en Adobe Photoshop](/help/release-notes/assets/asset_search_photoshop.png)

##### [!DNL Adobe Stock] integración {#stock}

Su organización puede utilizar su [!DNL Adobe Stock] plan empresarial en [!DNL Experience Manager Assets] para garantizar que los recursos con licencia estén ampliamente disponibles para sus proyectos creativos y de marketing. Puede buscar, previsualizar y conceder licencias rápidamente [!DNL Adobe Stock] recursos que se guardan en Experience Manager, utilizando las potentes capacidades DAM de [!DNL Experience Manager].

[!DNL Adobe Stock] Este servicio proporciona a diseñadores y empresas acceso a millones de fotografías, vectores, ilustraciones, vídeos, plantillas y recursos 3D de alta calidad, depurados y libres de derechos para todos sus proyectos creativos.

Para obtener más información, consulte [Uso de recursos de Adobe Stock en Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md).

![Previsualización de la imagen y la licencia de Adobe Stock desde Experience Manager Assets](/help/release-notes/assets/stock_image_preview_license_options.png)

*Figura: Vista previa [!DNL Adobe Stock] imagen y licencia desde [!DNL Experience Manager Assets].*

![Buscar y filtrar las imágenes de Adobe Stock con licencia en Experience Manager](/help/release-notes/assets/aem-search-filters2.jpg)

*Imagen: búsqueda y filtrado de la licencia [!DNL Adobe Stock] imágenes en [!DNL Experience Manager].*

##### Referencias dinámicas en [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] se usa en [!DNL Adobe InDesign] Los archivos de son dinámicos. Las referencias se actualizan automáticamente si los recursos a los que se hace referencia se mueven en el repositorio. Para obtener más información, consulte [administración de recursos compuestos](/help/assets/managing-linked-subassets.md).

#### Funciones de Brand Portal {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] le ayuda a adquirir, controlar de forma eficaz y distribuir de forma segura los recursos aprobados a proveedores/agencias externos y usuarios internos del negocio entre dispositivos. Ayuda a mejorar la eficacia del uso compartido de recursos, acelera el tiempo de comercialización de los recursos y elimina el riesgo de uso no conforme y acceso no autorizado.

Para obtener más información, consulte [Novedades de Brand Portal.](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=es).

#### Recursos conectados {#connectedassets}

En las grandes empresas se puede distribuir la infraestructura necesaria para crear sitios web. A veces, las capacidades de creación de sitios web y los recursos digitales necesarios residen en diferentes silos.

[!DNL Experience Manager Sites] ofrece capacidades de crear páginas web y es el sistema de gestión de recursos digitales (DAM) que proporciona los recursos necesarios para los sitios web.[!DNL Experience Manager Assets] [!DNL Experience Manager] ahora admite el caso de uso anterior mediante la integración de [!DNL Sites] y [!DNL Assets]. Consulte [Cómo configurar y utilizar la función Recursos conectados](/help/assets/use-assets-across-connected-assets-instances.md).

![Arrastrar un recurso desde una [!DNL Experience Manager] implementación en un [!DNL Sites] página de otro [!DNL Experience Manager] implementación](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*Imagen: arrastre un recurso desde una [!DNL Experience Manager] implementación en un [!DNL Sites] página en una página diferente [!DNL Experience Manager] implementación.*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] ofrece funciones mejoradas de creación y entrega de medios enriquecidos en [!DNL Experience Manager Assets] para impulsar experiencias de vanguardia que sean inmersivas y personalizadas. Al cargar un único recurso principal de alta calidad y utilizar el procesamiento y los visores avanzados en la nube de Adobe, puede ofrecer cualquier combinación de representaciones sobre la marcha para admitir la estrategia de medios de su organización.

Para obtener más información sobre las nuevas [!DNL Dynamic Media] funciones, consulte [Notas de la versión de Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html).

##### Compatibilidad con vídeo 360 {#video-support}

Administre sus archivos de vídeo 360 directamente en [!DNL Experience Manager] uso de visores de última generación para ofrecer experiencias de realidad virtual en sobremesas, dispositivos móviles y auriculares de realidad virtual. Para obtener más información, consulte [Uso del vídeo 360](/help/assets/360-video.md).

##### Miniaturas de vídeo personalizadas {#custom-video-thumbnails}

Ahora puede personalizar las miniaturas de los recursos de vídeo mediante fotogramas del propio vídeo u otro contenido almacenado en DAM. Para obtener más instrucciones, consulte [Acerca de las miniaturas de vídeo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

##### Mejoras de accesibilidad {#accessibility-enhancements}

[!DNL Dynamic Media] Los visores ahora admiten funciones de accesibilidad mejoradas como compatibilidad con Aria, lectores de pantalla y texto alternativo. Para obtener más información, consulte [Guía de referencia del visor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html).

#### Mejora de la experiencia de búsqueda {#experience-enhancement-for-searching}

[!DNL Experience Manager] 6.5 en adelante, los especialistas en marketing pueden descubrir los recursos deseados más rápido desde la página de resultados de búsqueda. Las facetas de búsqueda se actualizan con el número de recursos incluso antes de aplicar el filtro de búsqueda. Ver el recuento esperado en el filtro ayuda a los usuarios a navegar por los resultados de búsqueda de forma eficaz. Para obtener más información, consulte [Buscar recursos en Experience Manager](/help/assets/search-assets.md).

![Ver el número de recursos sin filtrar los resultados de búsqueda en las facetas de búsqueda](/help/assets/assets/asset_search_results_in_facets_filters.png)

*Imagen: consulte el número de recursos sin filtrar los resultados de búsqueda en las facetas de búsqueda.*

#### Mejora de uso {#usability-enhancement}

Ahora puede seleccionar todos los recursos cargados dentro de una carpeta o desde un resultado de búsqueda de una sola vez. Le ayuda a administrar varios recursos rápidamente. La casilla de verificación selecciona todos los recursos que se ajustan al escenario, por ejemplo, un resultado de búsqueda, y no solo los recursos visibles en la [!DNL Experience Manager] interfaz.

![Utilice la opción Seleccionar todo para seleccionar todos los recursos cargados con un solo clic.](/help/release-notes/assets/select-all-in-aem-assets.gif)

*Imagen: utilice la opción Seleccionar todo para seleccionar todos los recursos cargados con un solo clic.*

#### Mejoras de metadatos {#metadata-enhancements}

[!DNL Assets] permite crear esquemas de metadatos para carpetas de recursos, que definen el diseño y los metadatos mostrados en las páginas de propiedades de la carpeta. Ahora puede asignar un esquema de metadatos de carpeta a una carpeta existente o al crear una carpeta. Para obtener más información, consulte [Carpeta de esquema de metadatos](/help/assets/metadata-config.md#folder-metadata-schema).

Al especificar metadatos en cascada, las opciones se pueden cargar desde un archivo JSON en tiempo de ejecución, por ejemplo, en lugar de escribir manualmente en el formulario. Para obtener más información, consulte [metadatos en cascada](/help/assets/metadata-schemas.md#cascading-metadata).

#### Mejoras de informes {#reporting-enhancements}

Los fragmentos de contenido y los vínculos compartidos ahora se incluyen en el informe descargado. Para obtener más información, consulte [Informes de recursos](/help/assets/asset-reports.md).

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM.5 Forms incorpora varias funciones y mejoras nuevas. Los aspectos destacados incluyen:

* Informes de transacciones para realizar un seguimiento de la cantidad de formularios enviados, documentos procesados y documentos representados
* Mejoras de uso en comunicaciones interactivas
* Firmas digitales basadas en la nube en formularios adaptables
* Incrustar formularios adaptables y comunicaciones interactivas en una aplicación de una sola página de AEM Sites SPA ().
* AEM Compatibilidad con variables en flujos de trabajo de
* Compatibilidad con patrones de visualización de datos en comunicaciones interactivas
* Ordenar formularios adaptables y tablas de comunicaciones interactivas
* Validación automatizada de los datos de entrada en los modelos de datos de formulario

Consulte la [AEM Resumen de las nuevas funciones y mejoras de Forms en la versión 6.5 de la versión de](/help/forms/using/whats-new.md) para obtener información sobre las funciones nuevas y mejoradas y los recursos de documentación.

### Uso del desarrollo centrado en el cliente {#leverage-customer-focused-development}

El Adobe de utiliza un modelo de desarrollo centrado en el cliente que permite a los clientes contribuir en todas las etapas del proceso de desarrollo, durante la especificación, el desarrollo y las pruebas. Damos las gracias a todos los clientes y socios colaboradores en este proceso.

Adobe dispone de los procedimientos y procesos necesarios para permitir la recopilación, la priorización y el seguimiento de la resolución de errores centrada en el cliente y el desarrollo de solicitudes de mejora. El [Portal de asistencia al Experience Manager](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=es#support) está integrado con el sistema de mejora de Adobe y seguimiento de defectos. El equipo de Asistencia al cliente identifica y resuelve las preguntas del cliente siempre que es posible. Cuando se pasa a I+D, toda la información del cliente se captura y se utiliza con fines de priorización e informes. En el desarrollo se da prioridad a la asistencia de pago, los problemas de garantía y las mejoras de pago del cliente.

AEM Este proceso de priorización ha dado como resultado más de 750 cambios centrados en el cliente fijados en la versión 6.5000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000

## Lista de archivos que forman parte de la versión {#list-of-files-that-are-part-of-the-release}

**Foundation**

* Inicio rápido independiente: `cq-quickstart-6.5.0.jar`.
* Inicio rápido del servidor de aplicaciones: `cq-quickstart-6.5.0.war`.
* Dispatcher 4.3.2 o posterior para los distintos servidores web y plataformas. Consulte [vínculo de descarga](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html)
* Complemento para Eclipse IDE ([leer más y descargar](/help/sites-developing/aem-eclipse.md))

* Extensión para el editor de código entre corchetes ([leer más y descargar](/help/sites-developing/aem-brackets.md))
* Dependencias Maven/Gradle ([vínculo de descarga](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/))

**Sites**

* Componentes principales ([Proyecto de GitHub](https://github.com/adobe/aem-core-wcm-components))
* Implementación de referencia de We.Retail ([leer más](/help/sites-developing/we-retail.md))
* Arquetipos del proyecto Maven:

   * para sitios de pila completa: [Proyecto de GitHub](https://github.com/adobe/aem-project-archetype)
   * para aplicaciones de una sola página con React/Angular: [Proyecto de GitHub](https://github.com/adobe/aem-spa-project-archetype)

* AEM Screens Players para varias plataformas de destino ([descargar](https://download.macromedia.com/screens/))

* Modelos de idioma de contenido inteligente. El inglés está preinstalado: se pueden descargar más idiomas

   * [Alemán](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [Español](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [Italiano](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [Francés](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* AEM El grupo de herramientas de modernización, por ejemplo, la herramienta de conversión de diálogos. ([Proyecto de GitHub](https://github.com/adobe/aem-modernize-tools))

**Assets**

* Paquete para añadir un Rasterizador de PDF mejorado ([leer más](/help/assets/aem-pdf-rasterizer.md))
* Paquete para añadir compatibilidad con imágenes RAW extendidas ([leer más](/help/assets/camera-raw.md))

**Forms**

* [Paquetes para funciones de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es)
* [AEM Forms OSGi Client SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

## Idiomas {#languages}

La interfaz de usuario de está disponible en los siguientes idiomas:

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

[!DNL Experience Manager] 6.5 ha sido certificado para GB18030-2005 CITS para usar el Estándar de Codificación Chino.

## Instalar y actualizar {#install-update}

Para conocer los requisitos de configuración, consulte [instrucciones de instalación](/help/sites-deploying/custom-standalone-install.md).

Para obtener instrucciones detalladas, consulte [documentación de actualización](/help/sites-deploying/upgrade.md).

## Plataformas compatibles {#supported-platforms}

Encuentre la matriz completa de plataformas compatibles, incluido el nivel de compatibilidad, en [AEM Requisitos técnicos de la versión 6.5](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Oracle se ha trasladado a un modelo de Soporte a largo plazo (LTS) para productos de Oracle Java™ SE. Java™ 9 y 10 son versiones no LTS por Oracle. Consulte [Oracle Java™ SE: hoja de ruta](https://www.oracle.com/technetwork/java/eol-135779.html). El Adobe AEM admite versiones LTS de Java™ para que solo se ejecuten en la fase de producción de los programas de la. AEM Java™ 11 es la versión recomendada para usar con 6.5.

## Funciones en desuso y eliminadas {#deprecated-and-removed-features}

El Adobe evalúa constantemente las funcionalidades del producto y planea con el tiempo reemplazar las funcionalidades con versiones más potentes o decide reimplementar partes seleccionadas para mejorarlas de cara a futuras expectativas o extensiones.

Para [!DNL Adobe Experience Manager] 6,5, [leer la lista de funciones obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md). La página también incluye un anuncio previo de los cambios que se producirán en el futuro y un aviso importante para los clientes que actualicen sus datos con respecto a las versiones anteriores.

## Problemas conocidos {#known-issues}

### Plataforma {#platform}

* Se informa de un problema en el que se eliminan CRX-Quickstart y su contenido.

  En cada una de estas acciones, asegúrese de que la propiedad `htmllibmanager.fileSystemOutputCacheLocation` no es una cadena vacía:

   1. Llamando `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. AEM Actualización a la versión 6.5 de.
   3. AEM Ejecución de la &quot;migración de contenido diferido&quot; en la versión 6.5 de.

  A [Base de conocimiento](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) Este artículo está disponible con más detalles y la solución alternativa para este problema.

* AEM Si utiliza JDK 11 con instancia de 6.5, algunas de las páginas podrían mostrarse en blanco después de implementar algunos paquetes. El siguiente mensaje de error aparece en el archivo de registro:

  ```java
  *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
  java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
  ```

Para resolver este error:

1. Detenga la instancia de AEM. Ir a `<aem_server_path_on_server>crx-quickstart\conf` y abra el `sling.properties` archivo. El Adobe recomienda realizar una copia de seguridad de este archivo.

1. Buscar `org.osgi.framework.bootdelegation=`. Añadir `jdk.internal.reflect,jdk.internal.reflect.*` propiedades para mostrar el resultado como.

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. AEM Guarde el archivo y reinicie la instancia de.

### Sites {#sites}

* **Uso de versiones de página**: [Si se ha movido una página, ya no puede realizar una previsualización de ninguna versión realizada antes del movimiento](/help/sites-authoring/working-with-page-versions.md#previewing-a-version).

### Assets {#assets}

* **Buscar:** La búsqueda no genera ningún resultado si la cadena de búsqueda contiene espacios iniciales ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Esquema de metadatos de carpeta**: Después de agregar un botón de opción, el campo ID y Value no se representan según lo esperado y la funcionalidad de eliminación no funciona. (CQ-4261144)
* Al cambiar el nombre de un recurso, no es posible utilizar un espacio en blanco en el nombre del recurso. (CQ-4266403)

### Forms {#forms}

* Cuando AEM Forms está instalado en el sistema operativo Linux®, la firma digital con el módulo de seguridad de hardware no funciona. (CQ-4266721)
* (Solo AEM Forms en WebSphere®) La variable **Forms Workflow** > **Búsqueda de tareas** La opción no devuelve ningún resultado si busca un **Administrador** con **Nombre de usuario** como criterio de búsqueda. (CQ-4266457)

* AEM Forms no puede convertir archivos TIF y de TIFF con compresión de JPEG a documentos de PDF. (CQ-4265972)
* El **Escáner de recursos de AEM Forms** y **Migración de carta a comunicación interactiva** Las opciones de no funcionan en **Migración de AEM Forms** página. (CQ-4266572)

* AEM (Solo JBoss® 7) Cuando actualiza desde una versión anterior a la versión 6.5 de Forms y la versión anterior tenía procesos (.lca) que creaban y utilizaban una copia del proceso de envío o procesamiento predeterminado, HTML5 Forms que utiliza estos procesos (.lca) no realiza las acciones necesarias. (CQ-4243928)
* En un formulario adaptable, cuando se invoca un servicio del modelo de datos de formulario desde el editor de reglas para actualizar dinámicamente los valores del componente de opción de imagen, los valores del componente de opción de imagen no se actualizan. (CQ-4254754)
* El instalador de AEM Forms Designer requiere la versión de 32 bits de [Paquete de tiempo de ejecución redistribuible de Visual C++ 2012](https://docs.microsoft.com/en-US/cpp/windows/latest-supported-vc-redist?view=msvc-170) y [Paquetes de tiempo de ejecución redistribuibles de Visual C++ 2013](https://support.microsoft.com/en-us/topic/update-for-visual-c-2013-and-visual-c-redistributable-package-5b2ac5ab-4139-8acc-08e2-9578ec9b2cf1). Asegúrese de que los paquetes de ejecución redistribuibles anteriores estén instalados antes de iniciar la instalación. (CQ-4265668)

* El PDF Generator no admite la autenticación basada en tarjetas inteligentes. Cuando un administrador habilita la directiva de grupo `Interactive Logon: Require Smart card` en un servidor de Windows, se invalidan todos los usuarios de PDF Generator existentes.

* Cuando se configura un formulario adaptable para actualizar dinámicamente los valores de un componente y se accede a la instancia de publicación que aloja el formulario a través de Dispatcher, la funcionalidad para actualizar dinámicamente los valores de un campo deja de funcionar. Para resolver el problema, en la instancia de publicación, abra CRXDE y navegue hasta `/libs/fd/af/runtime/clientlibs/guideChartReducer`y cree la propiedad que se muestra en.

   * Nombre: allowProxy
   * Tipo: booleano
   * Valor: true
   * Protegido: Falso
   * Obligatorio: Falso
   * Múltiple: False
   * Creado automáticamente: Falso

  La propiedad permite a las bibliotecas de cliente de la carpeta de tiempo de ejecución acceder a los proxies. (CQ-4268679)

* Cuando se inicia AEM Forms, la variable `SAX Security Manager could not be setup` aparece una advertencia.
* Al abrir un PDF protegido con AEM Forms Document Security en un Apple iOS o iPadOS que ejecute la versión 20.10.00 de Adobe Acrobat Reader
* Cuando envía un formulario que contiene un campo de carga de HTML estándar desde un dispositivo iOS de Apple, a veces, el contenido del archivo no se envía y se recibe un archivo de 0 bytes en el otro extremo. Apple iOS 15.1 proporciona una solución para el problema.

## Descarga y asistencia de productos (sitios restringidos) {#product-download-and-support-restricted-sites}

Los siguientes sitios solo están disponibles para clientes de. Si es cliente de y necesita acceso, póngase en contacto con el administrador de cuentas de Adobe de.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/).

* Actualizaciones de productos, parches y paquetes para obtener funcionalidad adicional en [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html).

* [Asistencia al cliente mediante Admin Console](https://adminconsole.adobe.com/). Para obtener más información, consulte [Nueva experiencia de asistencia al cliente de Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en).
