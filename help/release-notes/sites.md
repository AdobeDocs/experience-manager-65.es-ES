---
title: Notas de versión de AEM Sites
description: Notas de versión específicas de Adobe Experience Manager 6.5 Sites.
translation-type: tm+mt
source-git-commit: 23656e023a9a0bfc335655f9cfb0530aa917b3ef
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 68%

---


# Notas de la versión de AEM Sites {#aem-sites-release-notes}

Consulte las siguientes mejoras de AEM Sites 6.5 detalladamente:

## Desarrollo de componentes y plantillas {#component-amp-template-development}

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

## Administración de sitios {#site-administration}

* La barra de [Referencia](/help/sites-authoring/author-environment-tools.md#references) tiene una nueva sección para mostrar los vínculos internos que conducen a la página seleccionada. Esto resulta útil cuando se planea utilizar o eliminar una página sin conexión, para ver qué páginas necesitan ajustes antes de desconectarlas.
* La [vista de lista](/help/sites-authoring/basic-handling.md#list-view) tiene una nueva columna de flujo de trabajo que muestra el estado de la página cuando se encuentra en un flujo de trabajo.
* En las [propiedades de la página](/help/sites-authoring/editing-page-properties.md), ahora es posible buscar recursos existentes al asignar una miniatura a la página (pestaña Miniaturas).

## Editor de página {#page-editor}

* Permite la edición y composición en contexto de experiencias de aplicaciones de página única construidas con componentes React y Angular del lado del cliente que aprovechan el SDK de JS (también llamado SPA Editor)
* El modo de scaffolding solo se muestra si la página tiene una página de scaffolding configurada.

## Fragmentos de contenido y editor {#content-fragments-amp-editor}

* La nueva barra de [Anotaciones](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) en el Editor de fragmentos de contenido se puede usar para realizar comentarios generales y ver comentarios en el texto (también se muestra en la barra de cronología)
* Posibilidad de establecer el tipo de contenido predeterminado de un elemento de texto multilínea en un [modelo de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md) en texto simple, texto enriquecido o Markdown
* Agregue [comentarios o anotaciones](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) seleccionando texto en RTE (vista de pantalla completa)
* [Comparar versiones](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) de un fragmento de contenido en paralelo a través de la barra de referencia
* El informe de descarga de recursos ahora muestra los fragmentos de contenido correspondientes
* Agregue la [compatibilidad con fragmentos de contenido a la API HTTP de recursos](/help/assets/assets-api-content-fragments.md) mediante /api.json. Existen API para crear, actualizar, leer y eliminar fragmentos de contenido.

## Fragmentos de experiencias {#experience-fragments}

* Se ha mejorado la indexación de los [fragmentos de experiencias](/help/sites-authoring/experience-fragments.md) para que su contenido se encuentre al buscar las páginas donde estos se utilizan
* La opción [Export to Target](/help/sites-administering/experience-fragments-target.md) (Exportar a destino) ahora permite enviar el fragmento de experiencia como JSON (el valor predeterminado es HTML) o ambos

## Traducción {#translation}

* Simplifique la creación de proyectos de traducción mediante Project Masters
* Simplifique la ejecución de proyectos de traducción estableciendo el estado de los trabajos de traducción en &quot;Aprobado&quot; de forma predeterminada
* Permita la actualización de las páginas traducidas con cambios en la memoria de traducción de terceros
* Permita exportar los trabajos de traducción en formato JSON
* Actualización de la integración de Microsoft Translation para utilizar la API V3

## Administración de varios sitios (MSM) {#multi-site-management-msm}

* Para las configuraciones de lanzamiento que utilizan PushOnModify, obtendrá un proceso de gestión mejorado de la operación de movimiento de página para evitar un estado incoherente
* La creación de una nueva página dentro de la estructura livecopy ahora creará por defecto una página independiente
* Utilice las funciones de MSM en aplicaciones de página única que utilicen el SDK para JS (también denominado SPA Editor)

## Lanzamientos {#launches}

* Nuevo flujo de trabajo de revisión y aprobación de lanzamientos, y la capacidad de promover únicamente las páginas de lanzamiento aprobadas
* Se agregó una [opción en la interfaz de usuario para eliminar el lanzamiento después de realizar el paso de promoción](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

## Simulación y segmentación de contenido  {#content-targeting-simulation}

* Se ha actualizado la capa de datos de ContextHub y el motor de reglas del lado del cliente JavaScript para utilizar jQuery 3 de forma predeterminada.

## AEM y Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>Actualmente:
>
>* Solo se admite `at.js 1.x` si utiliza Adobe Target como motor de targeting en AEM consola de actividades.
   >
   >
* Tanto `at.js. 1.x` como `at.js 2.x` son compatibles si utiliza la exportación de fragmentos de experiencias a Target y ejecuta actividades en la consola de Target.


* La integración de Adobe Target ahora puede utilizar la API de Target Standard. Las versiones anteriores de AEM utilizan la API HTTP de Target Classic, que ahora está en desuso.
* Se incluye la versión 63 de Adobe Target `mbox.js`. Adobe recomienda cambiar la implementación a `at.js` v1.x.
* `at.js` ya se incluye la versión 1.5.0. Adobe recomienda utilizar [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) para aprovisionar `at.js` v1.x en el sitio.

## AEM y Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` Se incluye H.27.5. Adobe recomienda cambiar la implementación a `AppMeasurement.js`
* `AppMeasurement.js` Se incluye la versión 1.8.0. Adobe recomienda utilizar [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) para aprovisionar AppMeasurement.js en el sitio.

## AEM y comercio {#aem-commerce}

Las mejoras en Commerce Integration Framework se encuentran en un ciclo de lanzamiento más rápido desde AEM 6.4. [Más información aquí](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html).

## Complemento de Communities {#communities-add-on}

Consulte la [página de las notas de versión de Communities](../release-notes/communities-release-notes.md)

## Complemento de pantallas  {#screens-add-on}

* Uso de lanzamientos para planificar futuros cambios en el contenido de señalización
* Reproducción limitada en un canal de secuencias
* Crear automáticamente la estructura del proyecto mediante un archivo de origen; por ejemplo, una hoja de Excel

Para obtener más información sobre los cambios en AEM Screens, consulte las Notas de la versión en la [Guía del usuario de AEM Screens](https://docs.adobe.com/content/help/es-ES/experience-manager-screens/user-guide/aem-screens-introduction.html).
