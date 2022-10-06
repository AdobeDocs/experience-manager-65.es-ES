---
title: Información general del editor de SPA
seo-title: SPA Editor Overview
description: Este artículo ofrece una descripción general completa del Editor de SPA y cómo funciona, e incluye flujos de trabajo detallados de interacción del Editor de SPA dentro de AEM.
seo-description: This article gives a comprehensive overview of the SPA Editor and how it works included detailed workflows of interaction of the SPA Editor within AEM.
uuid: c283abab-f5bc-414a-bc81-bf3bdce38534
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 06b8c0be-4362-4bd1-ad57-ea5503616b17
docset: aem65
exl-id: 7b34be66-bb61-4697-8cc8-428f7c63a887
source-git-commit: a547b2e24205c63284a0e77f2e7f5678ae24968b
workflow-type: tm+mt
source-wordcount: '1657'
ht-degree: 1%

---

# Información general del editor de SPA{#spa-editor-overview}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios mediante marcos de SPA y los autores quieren editar contenido sin problemas dentro de AEM para un sitio creado con dichos marcos.

El SPA Editor ofrece una solución completa para admitir SPA dentro de AEM. Esta página proporciona información general sobre cómo se estructura SPA soporte en AEM, cómo funciona el Editor de SPA y cómo el marco de SPA y la AEM se mantienen sincronizados.

>[!NOTE]
>
>El Editor de SPA es la solución recomendada para proyectos que requieren SPA procesamiento del lado del cliente basado en el marco de trabajo (por ejemplo, React o Angular).

## Introducción {#introduction}

Los sitios creados con marcos de SPA comunes, como React y Angular, cargan su contenido a través de JSON dinámico y no proporcionan la estructura de HTML necesaria para que el Editor de páginas de AEM pueda colocar controles de edición.

Para permitir la edición de SPA dentro de AEM, se necesita una asignación entre la salida JSON del SPA y el modelo de contenido en el repositorio AEM para guardar los cambios en el contenido.

SPA compatibilidad con en AEM introduce una capa de JS fina que interactúa con el código JS de SPA cuando se carga en el Editor de páginas con el que se pueden enviar eventos y se puede activar la ubicación de los controles de edición para permitir la edición en contexto. Esta función se basa en el concepto de extremo de la API de servicios de contenido, ya que el contenido de la SPA debe cargarse a través de los servicios de contenido.

Para obtener más información sobre SPA en AEM, consulte los siguientes documentos:

* [Modelo SPA](/help/sites-developing/spa-blueprint.md) para los requisitos técnicos de una SPA
* [Introducción a SPA en AEM](/help/sites-developing/spa-getting-started-react.md) para un rápido recorrido por un SPA simple

## Diseño {#design}

El componente de página de una SPA no proporciona los elementos HTML de sus componentes secundarios a través del archivo JSP o HTL. Esta operación se delega en el marco SPA. La representación de componentes o modelos secundarios se obtiene como una estructura de datos JSON del JCR. A continuación, los componentes SPA se añaden a la página según esa estructura. Este comportamiento diferencia la composición inicial del cuerpo del componente de página de las contrapartes que no son SPA.

### Administración de modelos de página {#page-model-management}

La resolución y la administración del modelo de página se delegan a un `PageModel` biblioteca. El SPA debe utilizar la biblioteca del modelo de página para que el Editor de SPA pueda inicializarlo y crearlo. La biblioteca Modelo de página que se proporciona indirectamente al componente Página AEM a través del `aem-react-editable-components` npm. El modelo de página es un intérprete entre AEM y la SPA y, por lo tanto, siempre debe estar presente. Cuando se crea la página, se crea una biblioteca adicional `cq.authoring.pagemodel.messaging` debe añadirse para habilitar la comunicación con el editor de páginas.

Si el componente de página SPA hereda del componente principal de página, hay dos opciones para realizar la variable `cq.authoring.pagemodel.messaging` categoría biblioteca de cliente disponible:

* Si la plantilla es editable, agréguela a la directiva de página.
* O agregue las categorías utilizando la variable `customfooterlibs.html`.

Para cada recurso del modelo exportado, el SPA asignará un componente real que realizará la renderización. El modelo, representado como JSON, se representa mediante las asignaciones de componentes dentro de un contenedor.
![screen_shot_2018-08-20at144152](assets/screen_shot_2018-08-20at144152.png)

>[!CAUTION]
>
>La inclusión de la variable `cq.authoring.pagemodel.messaging` debe limitarse al contexto del Editor de SPA.

### Tipo de datos de comunicación {#communication-data-type}

Cuando la variable `cq.authoring.pagemodel.messaging` se añade a la página, enviará un mensaje al Editor de páginas para establecer el tipo de datos de comunicación JSON. Cuando el tipo de datos de comunicación se establece en JSON, las solicitudes de GET se comunican con los puntos finales del modelo Sling de un componente. Una vez que se produce una actualización en el editor de páginas, la representación JSON del componente actualizado se envía a la biblioteca del modelo de página. A continuación, la biblioteca del modelo de página informa al SPA de las actualizaciones.

![screen_shot_2018-08-20at143628](assets/screen_shot_2018-08-20at143628.png)

## Flujo de trabajo {#workflow}

Puede comprender el flujo de la interacción entre el SPA y el AEM pensando en el Editor de SPA como un mediador entre ambos.

* La comunicación entre el editor de páginas y el SPA se realiza mediante JSON en lugar de HTML.
* El editor de páginas proporciona la versión más reciente del modelo de página al SPA mediante el iframe y la API de mensajería.
* El administrador de modelos de página notifica al editor que está listo para la edición y pasa el modelo de página como una estructura JSON.
* El editor no modifica ni siquiera accede a la estructura DOM de la página que se está creando, sino que proporciona el último modelo de página.

![screen_shot_2018-08-20at144324](assets/screen_shot_2018-08-20at144324.png)

### Flujo de trabajo del Editor de SPA básico {#basic-spa-editor-workflow}

Teniendo en cuenta los elementos clave del Editor de SPA, el flujo de trabajo de alto nivel de edición de un SPA dentro de AEM aparece para el autor de la siguiente manera.

![sin título1](assets/untitled1.gif)

1. SPA Editor se carga.
1. SPA se carga en un fotograma independiente.
1. SPA solicita contenido JSON y procesa componentes en el lado del cliente.
1. SPA Editor detecta los componentes procesados y genera superposiciones.
1. El autor hace clic en la superposición y muestra la barra de herramientas de edición del componente.
1. SPA Editor mantiene las ediciones con una solicitud de POST al servidor.
1. SPA Editor solicita JSON actualizado al Editor de SPA, que se envía al SPA con un evento DOM.
1. SPA vuelve a procesar el componente correspondiente, actualizando su DOM.

>[!NOTE]
>
>Tenga en cuenta:
>
>* El SPA siempre está a cargo de su visualización.
>* El SPA Editor está aislado del propio SPA.
>* En producción (publicación), el editor de SPA nunca se carga.
>


### Flujo de trabajo de edición de páginas del servidor de cliente {#client-server-page-editing-workflow}

Esta es una descripción más detallada de la interacción cliente-servidor al editar un SPA.

![page_editor_spa_authoringmediator-2](assets/page_editor_spa_authoringmediator-2.png)

1. El SPA se inicializa y solicita el modelo de página al Exportador del modelo de Sling.
1. El Exportador del modelo de Sling solicita los recursos que componen la página desde el repositorio.
1. El repositorio devuelve los recursos.
1. El Exportador del modelo de Sling devuelve el modelo de la página.
1. El SPA crea una instancia de sus componentes basada en el modelo de página.
1. **6 bis** El contenido informa al editor de que está listo para la creación.

   **6b** El editor de páginas solicita las configuraciones de creación de componentes.

   **6c** El editor de páginas recibe las configuraciones de componentes.
1. Cuando el autor edita un componente, el editor de páginas publica una solicitud de modificación en el servlet de POST predeterminado.
1. El recurso se actualiza en el repositorio.
1. El recurso actualizado se proporciona al servlet del POST.
1. El servlet de POST predeterminado informa al editor de páginas de que el recurso se ha actualizado.
1. El editor de páginas solicita el nuevo modelo de página.
1. Los recursos que componen la página se solicitan al repositorio.
1. El repositorio proporciona los recursos que componen la página al exportador del modelo de Sling.
1. El modelo de página actualizado se devuelve al editor.
1. El editor de páginas actualiza la referencia del modelo de página del SPA.
1. La SPA actualiza sus componentes en función de la nueva referencia del modelo de página.
1. Se actualizan las configuraciones de componentes de los editores de páginas.

   **17 bis** El SPA indica al editor de páginas que el contenido está listo.

   **17b** El editor de páginas proporciona a la SPA configuraciones de componentes.

   **17c** El SPA proporciona configuraciones de componentes actualizadas.

### Flujo de trabajo de creación {#authoring-workflow}

Esta es una descripción más detallada que se centra en la experiencia de creación.

![spa_content_authoringmodel](assets/spa_content_authoringmodel.png)

1. El SPA busca el modelo de página.
1. **2 bis** El modelo de página proporciona al editor los datos necesarios para la creación.

   **2b** Cuando se le notifica, el organizador de componentes actualiza la estructura de contenido de la página.
1. El orquestador de componentes consulta la asignación entre un tipo de recurso AEM y un componente SPA.
1. El organizador de componentes crea una instancia dinámica del componente SPA en función del modelo de página y la asignación de componentes.
1. El editor de páginas actualiza el modelo de página.
1. **6 bis** El modelo de página proporciona datos de creación actualizados al editor de páginas.

   **6b** El modelo de página envía cambios al organizador de componentes.
1. El orquestador de componentes recupera la asignación de componentes.
1. El organizador de componentes actualiza el contenido de la página.
1. Cuando el SPA termina de actualizar el contenido de la página, el editor de páginas carga el entorno de creación.

## Requisitos y limitaciones {#requirements-limitations}

Para permitir que el autor utilice el editor de páginas para editar el contenido de una SPA, la aplicación de SPA debe implementarse para interactuar con el SDK SPA Editor de AEM. Consulte la [Introducción a SPA en AEM](/help/sites-developing/spa-getting-started-react.md) documento para el mínimo que necesita saber para que el suyo funcione.

### Marcos admitidos {#supported-frameworks}

El SDK SPA Editor admite las siguientes versiones mínimas:

* React 16.x y posteriores
* Angular 6.x y superior

Las versiones anteriores de estos marcos pueden funcionar con el SDK AEM Editor SPA, pero no son compatibles.

### Marcos adicionales {#additional-frameworks}

Se pueden implementar marcos de SPA adicionales para trabajar con el SDK de AEM SPA Editor. Consulte la [Modelo SPA](/help/sites-developing/spa-blueprint.md) documento de los requisitos que debe cumplir un marco de trabajo para crear una capa específica del marco compuesta por módulos, componentes y servicios que funcionen con el AEM SPA Editor.

### Uso de varios selectores {#multiple-selectors}

Se pueden definir y utilizar selectores personalizados adicionales como parte de un SPA desarrollado para el SDK de SPA de AEM. Sin embargo, esta compatibilidad requiere que `model` sea el primer selector y la extensión sea `.json` como [requerido por el exportador JSON.](json-exporter-components.md#multiple-selectors)

### Requisitos del editor de texto {#text-editor-requirements}

Si desea utilizar el editor in situ de un componente de texto creado en SPA se requiere una configuración adicional.

1. Establezca un atributo (puede ser cualquiera) en el elemento contenedor contenedor que contenga el HTML de texto. En el caso del contenido de muestra del WKND Journal, es un `<div>` y el selector que se ha utilizado es `data-rte-editelement`.
1. Establezca la configuración `editElementQuery` en el componente de texto de AEM correspondiente `cq:InplaceEditingConfig` que apunten a ese selector, por ejemplo `data-rte-editelement`. Esto permite al editor saber qué elemento de HTML ajusta el texto del HTML.

Para ver un ejemplo de cómo se hace esto, consulte la [Contenido de muestra de WKND Journal.](https://github.com/adobe/aem-sample-we-retail-journal/pull/16/files)

Para obtener información adicional sobre la variable `editElementQuery` y la configuración del editor de texto enriquecido, consulte [Configure el Editor de texto enriquecido.](/help/sites-administering/rich-text-editor.md)

### Restricciones {#limitations}

El SDK de AEM SPA Editor se ha introducido con AEM 6.4 service pack 2. Cuenta con el pleno apoyo del Adobe, que sigue ampliándose y ampliándose. El Editor de SPA aún no admite las siguientes funciones de AEM:

* Modo Target
* ContextHub
* Edición de imágenes en línea
* Editar configuraciones (p. ej. oyentes)
* Deshacer/Rehacer
* Diferencias de página y Deformación de tiempo
* Funciones que realizan la reescritura de HTML en el servidor, como Verificador de vínculos, servicio de reescritura de CDN, acortamiento de URL, etc.
* Modo de desarrollador
* AEM lanzamientos
