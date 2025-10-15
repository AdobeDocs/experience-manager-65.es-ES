---
title: Notas de la versión generales de  [!DNL Adobe Experience Manager]  6.5
description: Notas de la versión de [!DNL Adobe Experience Manager] 6.5 que describen la información de la versión, las novedades, la instalación y las listas de cambios detalladas.
exl-id: b3d4a527-44ca-4eb6-b393-f3e8117cf1a6
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: ht
source-wordcount: '4477'
ht-degree: 100%

---

# Notas de la versión generales de [!DNL Adobe Experience Manager] 6.5{#general-release-notes-for-adobe-experience-manager}

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] |
|---|---|
| Versión | 6.5 |
| Tipo | Versión principal |
| Fecha de disponibilidad general | 8 de abril de 2019 |
| Actualizaciones recomendadas | Consulte las [actualizaciones recientes de AEM](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=es). |

### Datos curiosos {#trivia}

El ciclo de lanzamiento de esta versión de [!DNL Adobe Experience Manager] comenzó el 4 de abril de 2018, pasó 23 iteraciones de control de calidad y corrección de errores y finalizó el 28 de marzo de 2019. El número total de problemas relacionados con los clientes corregidos en esta versión es de 1345, incluidas las mejoras y las nuevas funciones.

[!DNL Adobe Experience Manager] 6.5 está disponible de forma general desde el 8 de abril de 2019.

![Pantalla de inicio de sesión de AEM 6.5](/help/assets/assets/aem65-login-v4.png)

## Novedades {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 es una versión de actualización de la base de código de [!DNL Adobe Experience Manager] 6.4. Proporciona funcionalidades nuevas y mejoradas, correcciones importantes para los clientes, mejoras de alta prioridad y correcciones generales de errores orientadas a la estabilidad del producto. También incluye versiones de [!DNL Adobe Experience Manager] 6.4 Service Pack hasta el SP4.

La lista siguiente proporciona información general, mientras que las páginas siguientes enumeran todos los detalles.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

La plataforma de [!DNL Adobe Experience Manager] 6.5 se basa en versiones actualizadas del marco de trabajo basado en OSGi (Apache Sling y Apache Felix) y el repositorio de contenido de Java™: Apache Jackrabbit Oak 1.10.2.

Quickstart utiliza Eclipse Jetty 9.4.15 como motor de servlet.

#### Compatibilidad con Java™  {#java-support}

* Nueva compatibilidad con Java™ 11, así como para Java™ 8, ya compatible.
* Para obtener un rendimiento óptimo, reemplace los valores de GC predeterminados por otros valores. Para obtener más información, consulte la sección de [instalación y actualización](/help/sites-deploying/custom-standalone-install.md).
* Adobe distribuye las actualizaciones de mantenimiento de Java™ 11 y Java™ 8 para que las utilicen los clientes en proyectos relacionados con AEM cuando estos no están disponibles de manera pública desde Oracle.

#### Desarrollo de Java™ {#java-development}

* Ahora existen [dos versiones de UberJar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies), una versión recomendada con interfaces públicas que no están en desuso y una versión que incluye interfaces que sí están en desuso.

#### Interfaz de usuario {#user-interface}

Se han realizado varias mejoras en la IU para que sea más productiva y fácil de usar.

* Nueva IU de administración de permisos para usuarios y grupos.
* Ahora, las vistas de columnas solo cargan entradas visibles en la pantalla, y solo cargarán más cuando el usuario empiece a desplazarse. Las vistas de lista y tarjeta ya lo hacían desde la versión 6.0 (mejorada en la 6.4).
* Las vistas de columnas ahora incluyen el estado del flujo de trabajo para páginas o recursos cuando corresponda.
* La acción [Seleccionar todo](/help/sites-authoring/basic-handling.md#select-all) es una forma rápida de ejecutar una acción con todas las páginas o recursos de la misma carpeta.
* La acción [Seleccionar todo](/help/sites-authoring/basic-handling.md#select-all) intenta realizar la acción en todas las páginas o recursos, no solo en los que se han cargado. Se muestra un cuadro de diálogo de advertencia si la acción no se actualiza para administrar acciones masivas.

>[!CAUTION]
>
>Adobe no tiene previsto realizar más mejoras en la IU clásica. AEM 6.5 incluye la IU clásica, y los clientes que actualicen desde versiones anteriores pueden seguir utilizándola. La IU clásica sigue siendo totalmente compatible mientras está en desuso. [Más información](/help/sites-deploying/ui-recommendations.md).

#### Búsqueda e indexación {#indexing-and-search}

* La búsqueda en Oak ahora admite facetas dinámicas. Por ejemplo, el carril de filtro en la búsqueda de recursos muestra el número estimado de resultados.
* QueryBuilder se ha ampliado para proporcionar resultados con facetas dinámicas.

#### Actualizar {#upgrade}

* La actualización directa local a AEM 6.5 es compatible con los clientes que ejecutan AEM 6.2, 6.3 y 6.4. Los clientes que usan 5.x o 6.0/6.1 y quieren aprovechar la actualización local deben actualizar primero a 6.4. A continuación, actualice a 6.5 o mediante la transferencia del contenido entre las instancias directamente a AEM 6.5.
* El procedimiento de actualización sigue siendo en gran medida el mismo en 6.5.
* Seguimos admitiendo las funciones Compatibilidad con versiones anteriores, Evaluación de la complejidad de la actualización y Actualizaciones sostenibles introducidas en la versión 6.4. Se han realizado actualizaciones específicas de la versión en aquellas áreas en las que era necesario.
* Se ha simplificado el paquete del detector de patrones. Hay un paquete que evalúa las actualizaciones a 6.5 para las versiones de origen disponibles.
* Para obtener detalles acerca del procedimiento de actualización, consulte la [documentación de actualización](/help/sites-deploying/upgrade.md).

#### Proyectos y flujos de trabajo {#projects-and-workflows}

* El nuevo editor del modelo de flujo de trabajo introducido en la versión 6.4 se ha mejorado para incluir más operaciones, como copiar y publicar, la compatibilidad con variables en los pasos del flujo de trabajo y las mejoras en las divisiones `OR` y `AND`.

#### Repositorio {#repository}

* La base de Adobe Experience Manager 6.5 son las versiones actualizadas del marco de trabajo basado en OSGi (Apache Sling y Apache Felix) y el repositorio de contenido Java™: Apache Jackrabbit Oak 1.10.2.
* Para obtener información general sobre los problemas corregidos, consulte [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) y [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>La nueva versión de Oak Segment Tar, disponible desde AEM 6.3, requiere una migración del repositorio. Este paso es obligatorio si está actualizando desde una versión anterior de TarMK o desea cambiar el nuevo Segment Tar desde otro tipo de persistencia. Para obtener más información sobre cuáles son las ventajas del nuevo Segment Tar, consulte las [Preguntas frecuentes sobre la migración a Oak Segment Tar](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

#### OSGi {#osgi}

* Se han añadido las bibliotecas de utilidades OSGi Promises y Converter.

#### Seguridad {#security}

* Se ha añadido la caducidad de la contraseña para el usuario administrador.

#### Servidor web {#web-server}

* La distribución de Quickstart utiliza Eclipse Jetty 9.4.15 como motor de servlet (AEM 6.4 suministrado con 9.3.22).

### [!DNL Experience Manager] Sites {#experience-manager-sites}

#### Aplicaciones de una sola página administradas {#managed-single-page-apps}

El editor de páginas añade la capacidad de editar contenido en contexto y componer/diseñar dentro de las experiencias procesadas del lado del cliente (también conocido [como editor de SPA](/help/sites-developing/spa-architecture.md)). Las aplicaciones de una sola página existentes creadas con el marco React de JavaScript o Angular se pueden ampliar con el SDK para SJ de AEM, de modo que los profesionales puedan editarlas.

Suministrado por primera vez como parte de AEM 6.4 SP2, con AEM 6.5 la compatibilidad con SPA adquiere las siguientes funciones:

* Utilice el editor de plantillas para editar y configurar las partes editables de AEM de la SPA
* Utilice la administración de varios sitios para crear experiencias de SPA de país, franquicia o marca blanca

#### Administración de contenido headless {#headless-content-management}

AEM puede entregar el contenido en diversos formatos y desde varios niveles de la pila. Algunos han existido desde 2008 con [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) y [POST Servlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html). Los servicios de contenido ([Sling Model Exporter](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=es)) se introdujeron en AEM 6.3 y son el método que utiliza el SDK para SJ de AEM para poblar las aplicaciones de una sola página (SPA). La [API HTTP para Assets](/help/assets/mac-api-assets.md) es una API CRUD que se amplió para AEM 6.5.

Nuevas funciones de la API HTTP:

* Se ha añadido [compatibilidad con fragmentos de contenido a la API HTTP para Assets](/help/assets/assets-api-content-fragments.md) con el fin de crear, actualizar, leer y eliminar fragmentos.
* Exponer listas de fragmentos de contenido a través de los servicios de contenido con el [componente principal Lista de fragmentos de contenido](https://www.aemcomponents.dev).
* Una [biblioteca de componentes principales](https://www.aemcomponents.dev) que muestra la salida JSON predeterminada de los servicios de contenido para cada componente

#### Complemento de Screens {#screens-add-on}

Diseñe, distribuya y optimice experiencias en todas las pantallas digitales, desde quioscos interactivos hasta señalización digital.

* Unificar experiencias y contenido en el sitio web y en las tiendas gracias a la reutilización mejorada del contenido
* Flujos de trabajo de creación y aprobación o publicación simplificados con compatibilidad para lanzamientos
* Editar y ofrecer experiencias interactivas enriquecidas con el editor de SPA
* Usar los lanzamientos para planificar futuros cambios en el contenido de señalización
* Reproducción limitada en un canal de secuencias
* Crear automáticamente una estructura de proyecto utilizando un archivo de origen, como una hoja de Excel
* Compatibilidad ampliada con reproductores multimedia con un sólido funcionamiento en línea y sin conexión (Smart Sync) capaz de escalar incluso a las redes de señalización más amplias.
* Personalizar el contenido que generan los datos en función de la ubicación o la configuración, mediante marcadores de posición dinámicos.
* Datos unificados impulsados por la integración de Adobe Analytics en el reproductor de AEM Screens

Para obtener más información sobre los cambios en AEM Screens, consulte las notas de la versión en la [Guía del usuario de AEM Screens](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=es).

#### Desarrollo de componentes y plantillas {#component-amp-template-development}

* Arquetipo de proyecto Maven 18 (o superior) para proyectos nuevos; consulte [Github para ver las notas de la versión](https://github.com/adobe/aem-project-archetype/releases).
* Arquetipo de proyecto Maven 1.0.6 (o superior) de aplicaciones de una sola página para proyectos nuevos; consulte [Github para ver las notas de la versión](https://github.com/adobe/aem-spa-project-archetype/releases).
* HTL versión 1.4; consulte [GitHub para ver las notas de la versión](https://github.com/adobe/htl-spec/releases/tag/1.4).

   * Operador “in” para cadenas, matrices y objetos:

     ```html
     ${'a' in 'abc'}
     ${100 in myArray}
     ${'a' in myObject}
     ```

   * Declaraciones de variables con data-sly-set:
     `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * Parámetros de control de lista y repetición; inicio, paso, fin:
     `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * Identificadores para data-sly-unwrap:

     ```html
     <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
     text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
     </div>
     ```

   * Compatibilidad con números negativos

* Componentes principales 2.3.2 (o superior); consulte [Github para ver las notas de la versión](https://github.com/adobe/aem-core-wcm-components/releases).
* Sistema de cuadrícula para el contenedor de diseño; consulte [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* Clientlib Manager: se ha configurado Google Closure Compiler de forma predeterminada para la minificación de clientlibs de JavaScript (el valor predeterminado antiguo era Yahoo YUI) y se ha actualizado Google Closure Compiler a la versión v20190121
* Editor de plantillas y directivas

   * Crear y editar plantillas para aplicaciones de una sola página que utilicen el SDK de JS (también denominado Editor de SPA)

* Sitio de referencia We.Retail 4.0; consulte [GitHub para ver las notas de la versión](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* Kit de herramientas para actualizar los sitios existentes y utilizar las funciones del editor más recientes; consulte el [repositorio de GitHub](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM incluye la versión 1.12.4 de la biblioteca jQuery para proporcionar la máxima compatibilidad con el código personalizado existente. Adobe ha realizado modificaciones para solucionar problemas de seguridad conocidos.

#### Administración de sitios {#site-administration}

* El carril [Referencia](/help/sites-authoring/author-environment-tools.md#references) tiene una nueva sección para enumerar los vínculos internos que apuntan a la página seleccionada. Esto es útil cuando se planea dejar una página sin conexión o eliminarla, para ver qué páginas necesitan ajustarse antes de hacerlo.
* La [vista de lista](/help/sites-authoring/basic-handling.md#list-view) tiene una nueva columna de flujo de trabajo que muestra el estado cuando la página se encuentra en un flujo de trabajo.
* En las [propiedades de la página](/help/sites-authoring/editing-page-properties.md), ahora es posible examinar los recursos existentes al asignar una miniatura a la página (pestaña Miniatura).

#### Editor de páginas {#page-editor}

* Permitir la edición y composición en contexto de experiencias de aplicaciones de una sola página generadas con componentes de cliente de React y Angular que utilizan el SDK de JS (también denominado Editor de SPA)
* El modo Andamiaje solo se muestra si la página tiene una página de andamiaje configurada.

#### Fragmentos de contenido y editor {#content-fragments-amp-editor}

* Nuevo carril [Anotaciones](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) en el editor de fragmentos de contenido para hacer comentarios generales y ver los comentarios realizados dentro del texto (también se muestran en el carril Cronología)
* Capacidad para establecer el tipo de contenido predeterminado de un elemento de texto multilínea en un [modelo de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md) en texto simple, texto enriquecido o markdown
* Añadir [comentario/anotaciones](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) seleccionando texto en el RTE (vista de pantalla completa)
* [Comparar versiones](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) de un fragmento de contenido en paralelo mediante el carril Referencia
* El informe de descarga de recursos ahora muestra los fragmentos de contenido correspondientes
* Añadir [compatibilidad con fragmentos de contenido a la API HTTP de Assets](/help/assets/assets-api-content-fragments.md) a través de /api.json. Existen API para crear, actualizar, leer y eliminar fragmentos de contenido.

#### Fragmentos de experiencias {#experience-fragments}

* Se ha mejorado la indexación de los [fragmentos de experiencias](/help/sites-authoring/experience-fragments.md) para que su contenido se encuentre al buscar las páginas donde estos se utilizan.
* La opción [Exportar a Target](/help/sites-administering/experience-fragments-target.md) ahora permite enviar el fragmento de experiencia como JSON (el valor predeterminado es HTML) o ambos.

#### Traducción {#translation}

* Simplificar la creación de proyectos de traducción utilizando Project Masters.
* Simplificar la ejecución de proyectos de traducción estableciendo los trabajos de traducción en el estado aprobado de forma predeterminada.
* Permitir la actualización de páginas traducidas con cambios en la memoria de traducción de terceros.
* Permitir exportar trabajos de traducción en formato JSON.
* Actualizar la integración de traducciones de Microsoft® para utilizar la API V3.

#### Administración de varios sitios (MSM) {#multi-site-management-msm}

* Para las configuraciones de despliegue que utilizan PushOnModify, un proceso de gestión mejorado de la operación de movimiento de página para evitar un estado incoherente.
* Al crear una página dentro de la estructura de Live Copy, se crea una página independiente de forma predeterminada.
* Usar funciones de MSM en aplicaciones de una sola página que utilicen el SDK de JS (también denominado Editor de SPA)

#### Lanzamientos {#launches}

* Nuevo flujo de trabajo de revisión y aprobación para lanzamientos y capacidad de promocionar solo las páginas de lanzamiento aprobadas
* Se ha añadido la [opción en la IU para elegir eliminar el lanzamiento justo después del paso de promoción](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

#### Simulación y segmentación de contenido {#content-targeting-simulation}

* La capa de datos de ContextHub y el motor de reglas del lado del cliente de JavaScript se han actualizado para utilizar jQuery 3 de forma predeterminada.

#### AEM y Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>En la actualidad:
>
>* Solo se admite `at.js 1.x` si usa Adobe Target como motor de segmentación en la consola de actividades de AEM.
>
>* Tanto `at.js. 1.x` como `at.js 2.x` son compatibles si utiliza la exportación de fragmentos de experiencias a Target y ejecuta actividades en la consola de Target.

* La integración de Adobe Target ahora utiliza la API de Target Standard. Las versiones anteriores de AEM emplean la API HTTP de Target Classic, que ahora está en desuso.
* Se ha incluido la versión 63 de Adobe Target `mbox.js`. Adobe recomienda cambiar la implementación a `at.js` v1.x.
* Ahora se ha incluido la versión 1.5.0 de `at.js`. Adobe recomienda usar [Adobe Experience Platform Launch](https://business.adobe.com/es/products/experience-platform/launch.html?lang=es) para aprovisionar `at.js` v1.x en el sitio.

#### AEM y Adobe Analytics {#aem-amp-adobe-analytics}

* Se ha incluido `s_code.js` H.27.5. Adobe recomienda cambiar la implementación a `AppMeasurement.js`
* Se ha incluido `AppMeasurement.js` v1.8.0. Adobe recomienda usar [Adobe Experience Platform Launch](https://business.adobe.com/es/products/experience-platform/launch.html?lang=es) para aprovisionar AppMeasurement.js en el sitio.

#### AEM y Commerce {#aem-commerce}

Las mejoras realizadas en Commerce Integration Framework se encuentran en un ciclo de lanzamiento más rápido desde AEM 6.4. Obtenga más información en [Integración de AEM y Adobe Commerce con Commerce Integration Framework](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/magento.html?lang=es).

#### Complemento de Communities {#communities-add-on}

Para obtener la versión más reciente, consulte la sección [Implementación de Communities](/help/communities/deploy-communities.md) de la documentación.

##### Mejoras en la participación de la comunidad {#enhancements-to-community-engagement}

**Compatibilidad de @menciones**
AEM Communities ahora permite a los usuarios registrados etiquetar (mencionar) a otros miembros registrados para atraer su atención en el contenido generado por el usuario. Los miembros etiquetados (mencionados) reciben entonces una notificación con un vínculo profundo al contenido generado por el usuario correspondiente. Sin embargo, los usuarios pueden optar por deshabilitar o habilitar las notificaciones del correo electrónico y de la web.

![Compatibilidad con menciones con arroba](/help/release-notes/assets/at-mentions.png)

Los usuarios de la comunidad no necesitan buscar su nombre, apellidos o nombre de usuario para ver si alguien ha contactado con ellos o si necesita su atención. Además, permite a los autores de UGC buscar respuestas de usuarios registrados específicos que puedan abordar mejor el problema y aportar información.

Los administradores de la comunidad deben **habilitar las menciones** en los componentes de la comunidad para permitir que los usuarios registrados usen la funcionalidad en esos componentes.

**Mensajería de grupo**

Los miembros registrados de la comunidad ahora pueden enviar mensajes masivos directos a los grupos mediante una sola composición de correo electrónico, en lugar de enviar el mismo mensaje de forma individual a los miembros del grupo. Para permitir la [mensajería de grupo](/help/communities/configure-messaging.md), habilite ambas instancias desde el [servicio de operaciones de mensajería](/help/communities/messaging.md#group-messaging).

![Mensaje de grupo](/help/release-notes/assets/group-messaging.png)

##### Mejoras en la moderación masiva {#enhancements-to-bulk-moderation}

Filtros personalizados en la moderación masiva

Ahora se pueden desarrollar [filtros personalizados](/help/communities/moderation.md#custom-filters) y añadirlos a la IU de moderación masiva.

Un [proyecto de ejemplo](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) que muestra que el filtrado mediante etiquetas está disponible en [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter). Este proyecto puede utilizarse como base para desarrollar filtros personalizados análogos.

![Filtros personalizados](/help/release-notes/assets/custom-tag-filter.png)

**Vista de lista en moderación masiva**

Se ha proporcionado una nueva vista de lista con una IU mejorada en la moderación masiva para mostrar las entradas de contenido generado por el usuario.

![Moderación masiva en la vista de lista](/help/release-notes/assets/list-view-moderation.png)

##### Mejoras en la administración de sitios y grupos {#enhancements-to-site-and-group-management}

**Administradores de sitios y grupos del lado del autor**

Communities, desde AEM 6.5, permite la administración (y gestión) descentralizada de diferentes sitios de la comunidad y grupos/grupos anidados. Las organizaciones que alojan varios sitios de comunidad y grupos anidados ahora pueden seleccionar miembros para funciones de administrador del lado de autor en el momento de la creación del sitio (y del grupo).

![Administrador del sitio](/help/release-notes/assets/site-admin.png)

Los administradores del sitio pueden crear un grupo en cualquier nivel de jerarquía y convertirse en los administradores predeterminados. Asimismo, otros administradores del grupo pueden eliminarlos más tarde. Los administradores del grupo pueden administrar su grupo G1 y crear un subgrupo anidado en G1.

##### Mejoras en la habilitación {#enhancements-to-enablement}

**Compatibilidad con SCORM 2017.1**

La funcionalidad de habilitación de las comunidades de AEM 6.5 admite el motor Modelo de referencia de objetos de contenido compartido [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/).

* Compatibilidad con la navegación por teclado en componentes de habilitación
* Los componentes de habilitación (por ejemplo, Reproducción de catálogos y cursos, Asignaciones, Biblioteca de archivos) en AEM Communities admiten la navegación mediante el teclado para mejorar la accesibilidad.

##### Otras mejoras {#other-enhancements}

* Compatibilidad con Solr 7
* Las comunidades de AEM 6.5 admiten la versión Apache Solr 7.0 de la plataforma de búsqueda al configurar MSRP y DSRP.

### [!DNL Experience Manager Assets] {#experience-manager-assets}

AEM 6.5 presenta las siguientes funciones y mejoras para impulsar la productividad de los usuarios de AEM, las funciones de DAM y las funciones creativas y de marketing asociadas.

#### Integración con [!DNL Adobe Creative Cloud] y flujos de trabajo creativos {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] ofrece varias formas de integrarse con [!DNL Adobe Creative Cloud] y compartir recursos para usarlos en flujos de trabajo en los que los equipos creativos y de marketing o empresariales colaboran estrechamente. [!DNL Experience Manager] 6.5 sigue mejorando la integración y la optimiza para exponer más oportunidades y optimizar los métodos existentes.

Siga leyendo para conocer las capacidades e integraciones específicas de [!DNL Experience Manager] 6.5 que puede utilizar para admitir mejor sus casos de uso de velocidad de contenido.

##### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] refuerza la colaboración entre creativos y especialistas en marketing en el proceso de creación de contenido. Los creativos pueden tener acceso al contenido almacenado en [!DNL Experience Manager Assets], sin salir de las aplicaciones con las que están más familiarizados. Los creativos pueden examinar, buscar, extraer y registrar recursos sin problemas mediante el panel in-app en las aplicaciones [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] y [!DNL Adobe InDesign].

[!DNL Adobe Asset Link] es parte de la oferta [Creative Cloud para empresas](https://www.adobe.com/es/creativecloud/business/enterprise.html). Para obtener más información al respecto, incluida la configuración necesaria de su implementación de [!DNL Experience Manager], consulte [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html?lang=es).

![Buscar recursos en Adobe Photoshop](/help/release-notes/assets/asset_search_photoshop.png)

##### Integración de [!DNL Adobe Stock] {#stock}

Su organización puede usar su plan para empresas [!DNL Adobe Stock] en [!DNL Experience Manager Assets] para asegurarse de que los recursos con licencia estén disponibles para sus proyectos creativos y de marketing. Puede encontrar y previsualizar recursos de [!DNL Adobe Stock] guardados en Experience Manager, así como concederles licencias rápidamente,  mediante las eficaces capacidades de DAM de [!DNL Experience Manager].

El servicio [!DNL Adobe Stock] proporciona a diseñadores y empresas acceso a millones de fotos, vectores, ilustraciones, vídeos, plantillas y recursos 3D de alta calidad, depurados y libres de derechos para todos sus proyectos creativos.

Para obtener más información, consulte [Uso de recursos de Adobe Stock en Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md).

![Previsualizar la imagen y la licencia de Adobe Stock en Experience Manager Assets](/help/release-notes/assets/stock_image_preview_license_options.png)

*Figura: Vista previa de la imagen [!DNL Adobe Stock] y la licencia desde [!DNL Experience Manager Assets].*

![Buscar y filtrar las imágenes de Adobe Stock con licencia en Experience Manager](/help/release-notes/assets/aem-search-filters2.jpg)

*Figura: Buscar y filtrar las imágenes de [!DNL Adobe Stock] con licencia en [!DNL Experience Manager].*

##### Referencias dinámicas en [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] utilizados en [!DNL Adobe InDesign] archivos son dinámicos. Las referencias se actualizan automáticamente si los recursos a los que se hace referencia se mueven en el repositorio. Para obtener más información, consulte [cómo administrar los recursos compuestos](/help/assets/managing-linked-subassets.md).

#### Funcionalidades de Brand Portal {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] le ayuda a adquirir, controlar y distribuir de forma fácil y segura los recursos aprobados a proveedores y agencias externos, así como a usuarios internos de la empresa entre dispositivos. Asimismo, le permite mejorar la eficiencia del uso compartido de recursos, acelera el tiempo de salida al mercado de esos recursos y elimina el riesgo de uso indebido y los accesos no autorizados.

Para obtener más información, consulte [Novedades de Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=es).

#### Recursos de red {#connectedassets}

En las grandes empresas se puede distribuir la infraestructura necesaria para crear sitios web. A veces, las capacidades de creación de sitios web y los recursos digitales necesarios residen en diferentes silos.

[!DNL Experience Manager Sites] ofrece capacidades de crear páginas web y [!DNL Experience Manager Assets] es el sistema de gestión de recursos digitales (DAM) que proporciona los recursos necesarios para los sitios web. [!DNL Experience Manager] ahora admite el caso de uso anterior mediante la integración de [!DNL Sites] y [!DNL Assets]. Consulte [cómo configurar y utilizar la característica Recursos conectados](/help/assets/use-assets-across-connected-assets-instances.md).

![Arrastrar un recurso desde una implementación de [!DNL Experience Manager] en una página de [!DNL Sites] de una implementación de [!DNL Experience Manager] diferente](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*Figura: Arrastrar un recurso desde una implementación de [!DNL Experience Manager] en una página de [!DNL Sites] en una implementación de [!DNL Experience Manager] diferente.*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] ofrece la creación y entrega mejoradas de medios enriquecidos en [!DNL Experience Manager Assets] para impulsar experiencias de vanguardia que sean inmersivas y estén personalizadas. Al cargar un único recurso principal de alta calidad y utilizar el procesamiento y los visores avanzados en la nube de Adobe, puede ofrecer cualquier combinación de representaciones sobre la marcha para admitir la estrategia de medios de su organización.

Para obtener más información sobre las nuevas características de [!DNL Dynamic Media], consulte [Notas de la versión de Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html?lang=es).

##### Compatibilidad con vídeo 360 {#video-support}

Administre sus archivos de vídeo 360 directamente en [!DNL Experience Manager] mediante los visores de última generación para ofrecer experiencias de realidad virtual en escritorios, dispositivos móviles y auriculares de realidad virtual. Para obtener más información, consulte [Uso de vídeos 360](/help/assets/360-video.md).

##### Miniaturas de vídeo personalizadas {#custom-video-thumbnails}

Ahora puede personalizar las miniaturas de los recursos de vídeo mediante fotogramas del propio vídeo u otro contenido almacenado en DAM. Para obtener instrucciones adicionales, consulte [Acerca de las miniaturas de vídeo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

##### Mejoras de accesibilidad {#accessibility-enhancements}

Los visores de [!DNL Dynamic Media] ahora admiten funciones de accesibilidad mejoradas, como compatibilidad con Aria, lectores de pantalla y texto alternativo. Para obtener más información, consulte la [Guía de referencia de visores](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html?lang=es).

#### Mejoras en la experiencia de búsqueda {#experience-enhancement-for-searching}

A partir de [!DNL Experience Manager] 6.5, los especialistas en marketing podrán descubrir los recursos deseados con mayor rapidez desde la página de resultados de búsqueda. Las facetas de búsqueda se actualizan con el número de recursos incluso antes de aplicar el filtro de búsqueda. Ver el recuento esperado en el filtro ayuda a los usuarios a navegar por los resultados de búsqueda de forma eficaz. Para obtener más información, consulte [Búsqueda de recursos en Experience Manager](/help/assets/search-assets.md).

![Ver el número de recursos sin filtrar los resultados de búsqueda en las facetas de búsqueda](/help/assets/assets/asset_search_results_in_facets_filters.png)

*Imagen: ver el número de recursos sin filtrar los resultados de búsqueda en las facetas de búsqueda.*

#### Mejora de usabilidad {#usability-enhancement}

Ahora puede seleccionar todos los recursos cargados dentro de una carpeta o desde un resultado de búsqueda de una sola vez. Esto ayuda a administrar varios recursos con rapidez. La casilla de verificación selecciona todos los recursos que se ajustan al escenario, como un resultado de búsqueda, y no solo los visibles en la interfaz de [!DNL Experience Manager].

![Usar la opción Seleccionar todo para seleccionar todos los recursos cargados con un solo clic.](/help/release-notes/assets/select-all-in-aem-assets.gif)

*Imagen: usar la opción Seleccionar todo para seleccionar todos los recursos cargados con un solo clic.*

#### Mejoras de metadatos {#metadata-enhancements}

[!DNL Assets] le permite crear esquemas de metadatos para carpetas de recursos, que definen el diseño y los metadatos mostrados en las páginas de propiedades de la carpeta. Ahora puede asignar un esquema de metadatos de carpeta a una carpeta existente o hacerlo al crear una. Para obtener más información, consulte [Esquema de metadatos de carpeta](/help/assets/metadata-config.md#folder-metadata-schema).

Al especificar metadatos en cascada, las opciones se pueden cargar desde un archivo JSON en tiempo de ejecución, por ejemplo, en lugar de escribir manualmente en el formulario. Para obtener más información, vea los [metadatos en cascada](/help/assets/metadata-schemas.md#cascading-metadata).

#### Mejoras en la creación de informes {#reporting-enhancements}

Los fragmentos de contenido y los vínculos compartidos ahora se incluyen en el informe descargado. Para obtener más información, consulte [Informes de Assets](/help/assets/asset-reports.md).

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM 6.5 Forms incorpora varias funciones y mejoras nuevas. Los aspectos más destacados incluyen lo siguiente:

* Informes de transacciones para realizar un seguimiento de la cantidad de formularios enviados, documentos tratados y documentos entregados
* Mejoras de usabilidad en las comunicaciones interactivas
* Firmas digitales basadas en la nube en formularios adaptables
* Incrustar formularios adaptables y comunicaciones interactivas en una aplicación de una sola página (SPA) de AEM Sites.
* Compatibilidad con variables en flujos de trabajo de AEM
* Compatibilidad con patrones de visualización de datos en comunicaciones interactivas
* Ordenar formularios adaptables y tablas de comunicaciones interactivas
* Validación automatizada de los datos de entrada en los modelos de datos de formulario

Consulte el [Resumen de las nuevas funciones y mejoras de AEM 6.5 Forms](/help/forms/using/whats-new.md) para obtener información sobre las funciones nuevas y mejoradas y los recursos de documentación.

### Uso del desarrollo centrado en el cliente {#use-customer-focused-development}

Adobe utiliza un modelo de desarrollo centrado en el cliente que permite a los clientes contribuir en todas las etapas del proceso, durante la especificación, el desarrollo y las pruebas. Agradecemos a todos los clientes y socios que hayan contribuido en este proceso.

Adobe dispone de los procedimientos y procesos para permitir la recopilación, la priorización y el seguimiento de la resolución de errores centrada en el cliente y el desarrollo de solicitudes de mejora. El [Portal de asistencia de Experience Manager](https://experienceleague.adobe.com/es?support-solution=Experience+Manager?lang=es#support) está integrado con el sistema de seguimiento de defectos y mejoras de Adobe. El equipo de Asistencia al cliente identifica y resuelve las preguntas del cliente siempre que es posible. Cuando se pasa a I+D, toda la información del cliente se recopila y se utiliza con fines de priorización y creación de informes. En el desarrollo, se da prioridad a la asistencia de pago, los problemas de garantía y las mejoras financiadas por el cliente.

Este proceso de priorización ha dado lugar a más de 750 cambios centrados en el cliente corregidos en AEM 6.5.

## Lista de archivos que forman parte de la versión {#list-of-files-that-are-part-of-the-release}

**Foundation**

* Inicio rápido independiente: `cq-quickstart-6.5.0.jar`.
* Inicio rápido del servidor de aplicaciones: `cq-quickstart-6.5.0.war`.
* Dispatcher 4.3.2 o posteriores para los distintos servidores y plataformas web. Vea el [vínculo de descarga](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=es)
* Complemento para Eclipse IDE ([leer más y descargar](/help/sites-developing/aem-eclipse.md))

* Extensión del editor de código Brackets ([leer más y descargar](/help/sites-developing/aem-brackets.md))
* Dependencias Maven/Gradle ([vínculo de descarga](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/))

**Sites**

* Componentes principales ([proyecto de GitHub](https://github.com/adobe/aem-core-wcm-components))
* Implementación de referencia de We.Retail ([leer más](/help/sites-developing/we-retail.md))
* Arquetipos de proyecto de Maven:

   * para sitios de pila completa: [proyecto de GitHub](https://github.com/adobe/aem-project-archetype)
   * para aplicaciones de una sola página con React/Angular: [proyecto de GitHub](https://github.com/adobe/aem-spa-project-archetype)

* Reproductores de AEM Screens para varias plataformas de destino ([descargar](https://download.macromedia.com/screens/))

* Modelos de idioma de contenido inteligente. El inglés está preinstalado: se pueden descargar más idiomas

   * [Alemán](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [Español](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [Italiano](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [Francés](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* Conjunto de herramientas de modernización de AEM, como la herramienta de conversión de cuadros de diálogo. ([proyecto de GitHub](https://github.com/adobe/aem-modernize-tools))

**Recursos**

* Paquete para añadir un rasterizador PDF mejorado ([leer más](/help/assets/aem-pdf-rasterizer.md))
* Paquete para añadir compatibilidad ampliada con imágenes RAW ([leer más](/help/assets/camera-raw.md))

**Formularios**

* [Paquetes para funciones de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es)
* [SDK de cliente OSGi de AEM Forms](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

## Idiomas {#languages}

La interfaz de usuario está disponible en los siguientes idiomas:

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

[!DNL Experience Manager] 6.5 se ha certificado para GB18030-2005 CITS para usar el estándar de codificación chino.

## Instalación y actualización {#install-update}

Para conocer los requisitos de configuración, consulte las [instrucciones de instalación](/help/sites-deploying/custom-standalone-install.md).

Para obtener instrucciones detalladas, consulte la [documentación de actualización](/help/sites-deploying/upgrade.md).

## Plataformas compatibles {#supported-platforms}

Encuentre la matriz completa de plataformas compatibles, incluido el nivel de compatibilidad, en [Requisitos técnicos de AEM 6.5](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Oracle se ha trasladado a un modelo de soporte a largo plazo (LTS) para los productos de Oracle Java™ SE. Java™ 9 y 10 son versiones que no son LTS de Oracle. Consulte la [hoja de ruta de asistencia de Oracle Java™ SE](https://www.oracle.com/technetwork/java/eol-135779.html). Adobe admite versiones LTS de Java™ para ejecutar AEM solo en producción. Java™ 11 es la versión recomendada para su uso con AEM 6.5.

## Funciones en desuso y eliminadas {#deprecated-and-removed-features}

Adobe evalúa sin cesar las funcionalidades del producto y, con el tiempo, planea reemplazarlas por versiones más potentes o reimplementar partes seleccionadas para mejorarlas de cara a futuras expectativas o extensiones.

Para [!DNL Adobe Experience Manager] 6.5, [lea la lista de funciones obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md). La página también incluye un anuncio previo de los cambios que se producirán en el futuro y un aviso importante para los clientes que actualicen sus datos con respecto a las versiones anteriores.

## Problemas conocidos {#known-issues}

### Plataforma {#platform}

* Se informa de un problema en el que se elimina CRX-Quickstart y su contenido.

  En cada una de estas acciones, asegúrese de que la propiedad `htmllibmanager.fileSystemOutputCacheLocation` no sea una cadena vacía siguiendo estos pasos:

   1. Llamando a `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. Actualizando a AEM 6.5.
   3. Ejecución de la “migración de contenido diferida” en AEM 6.5.

* Si utiliza JDK 11 con la instancia de AEM 6.5, ciertas páginas podrían mostrarse en blanco después de implementar algunos paquetes. El siguiente mensaje de error aparece en el archivo de registro:

  ```java
  *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
  java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
  ```

Para solucionar este error, siga estos pasos:

1. Detenga la instancia de AEM. Vaya a `<aem_server_path_on_server>crx-quickstart\conf` y abra el archivo `sling.properties`. Adobe recomienda realizar una copia de seguridad de este archivo.

1. Busque `org.osgi.framework.bootdelegation=`. Añade propiedades `jdk.internal.reflect,jdk.internal.reflect.*` para mostrar el resultado.

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. Guarde el archivo y reinicie la instancia de AEM.

### Sites {#sites}

* **Uso de versiones de página**: [si se ha movido una página, ya no podrá previsualizar ninguna versión realizada antes del movimiento](/help/sites-authoring/working-with-page-versions.md#previewing-a-version).

### Recursos {#assets}

* **Búsqueda:** la búsqueda no devuelve ningún resultado si la cadena de búsqueda contiene espacios iniciales ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Esquema de metadatos de carpeta**: después de añadir un botón de opción, el campo de ID y Valor no se procesan según lo esperado y la funcionalidad de eliminación no funciona. (CQ-4261144)
* Al cambiar el nombre de un recurso, no es posible utilizar un espacio en blanco en el nombre del recurso. (CQ-4266403)

### Formularios {#forms}

* Cuando AEM Forms está instalado en el sistema operativo Linux®, la firma digital con el módulo de seguridad de hardware no funciona. (CQ-4266721)
* (Solo AEM Forms en WebSphere®) La opción **Forms Workflow** > **Búsqueda de tareas** no devuelve ningún resultado si busca un **administrador** con el **nombre de usuario** como criterio de búsqueda. (CQ-4266457)

* AEM Forms no puede convertir archivos TIF y TIFF con compresión JPEG a documentos PDF. (CQ-4265972)
* Las opciones **AEM Forms Assets Scanner** y **Migración de carta a comunicación interactiva** no funcionan en la página **Migración de AEM Forms**. (CQ-4266572)

* (Solo JBoss® 7) Cuando actualiza desde una versión anterior a AEM 6.5 Forms y la versión anterior tenía procesos (.lca) que creaban y utilizaban una copia del proceso de envío o procesamiento predeterminado, los formularios HTML5 que utilizan estos procesos (.lca) no realiza las acciones necesarias. (CQ-4243928)
* En un formulario adaptable, cuando se invoca un servicio de modelo de datos de formulario desde el editor de reglas para actualizar dinámicamente los valores del componente de opción de imagen, los valores del componente de opción de imagen no se actualizan. (CQ-4254754)
* El programa de instalación de AEM Forms Designer requiere la versión de 32 bits del [paquete de ejecución redistribuible de Visual C++ 2012](https://docs.microsoft.com/es-ES/cpp/windows/latest-supported-vc-redist?view=msvc-170) y los [paquetes de ejecución redistribuibles de Visual C++ 2013](https://support.microsoft.com/es-es/topic/update-for-visual-c-2013-and-visual-c-redistributable-package-5b2ac5ab-4139-8acc-08e2-9578ec9b2cf1). Asegúrese de que los paquetes de ejecución redistribuibles anteriores estén instalados antes de iniciar la instalación. (CQ-4265668)

* PDF Generator no es compatible con la autenticación basada en tarjetas inteligentes. Cuando un administrador habilita la directiva de grupo `Interactive Logon: Require Smart card` en un servidor de Windows, se invalidan todos los usuarios de PDF Generator existentes.

* Cuando se configura un formulario adaptable para actualizar de forma dinámica los valores de un componente y se accede a la instancia de publicación que aloja el formulario a través de Dispatcher, la funcionalidad para actualizar de forma dinámica los valores de un campo deja de funcionar. Para resolver el problema, en la instancia de publicación, abra CRXDE, vaya a `/libs/fd/af/runtime/clientlibs/guideChartReducer` y cree la propiedad que se muestra a continuación.

   * Nombre: allowProxy
   * Tipo: booleano
   * Valor: true
   * Protegido: False
   * Obligatorio: False
   * Múltiple: False
   * Creado automáticamente: False

  La propiedad permite a las bibliotecas de cliente de la carpeta de tiempo de ejecución acceder a los proxies. (CQ-4268679)

* Cuando se inicia AEM Forms, aparece la advertencia `SAX Security Manager could not be setup`.
* Al abrir un PDF protegido con AEM Forms Document Security en un Apple iOS o iPadOS que ejecute la versión 20.10.00 de Adobe Acrobat Reader
* Cuando envía un formulario que contiene un campo de carga de HTML estándar desde un dispositivo iOS de Apple, a veces, el contenido del archivo no se envía y se recibe un archivo de 0 bytes en el otro extremo. Apple iOS 15.1 proporciona una solución para el problema.

## Descarga de productos y asistencia (sitios restringidos) {#product-download-and-support-restricted-sites}

Los siguientes sitios solo están disponibles para clientes. Si es cliente y necesita acceso, póngase en contacto con el administrador de cuentas de Adobe.

* [Descarga del producto en licensing.adobe.com](https://licensing.adobe.com/)

* Actualizaciones de productos, parches y paquetes para obtener funcionalidad adicional en [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html).

* [Asistencia al cliente a través de Admin Console](https://adminconsole.adobe.com/). Para obtener más información, consulte [Nueva experiencia de Asistencia al cliente de Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=es).
