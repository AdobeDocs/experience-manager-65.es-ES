---
title: Componente de página SPA
seo-title: SPA Page Component
description: En un SPA, el componente de página no proporciona los elementos HTML de sus componentes secundarios, sino que lo delega en el marco de SPA. Este documento explica cómo esto hace que el componente de página sea único de un SPA.
seo-description: In an SPA the page component doesn't provide the HTML elements of its child components, but instead delegates this to the SPA framework. This document explains how this makes the page component of an SPA unique.
uuid: d444527a-e883-4873-a55b-c2bc140d8d7f
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6329301c-1a26-4a46-99ae-1b7cc15b08be
docset: aem65
exl-id: 0e9e2350-67ef-45c3-991f-6c1cd98fe93d
source-git-commit: 17c198c744111753ffffcc0758f98859524c964e
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---

# Componente de página SPA{#spa-page-component}

En un SPA, el componente de página no proporciona los elementos HTML de sus componentes secundarios, sino que lo delega en el marco de SPA. Este documento explica cómo esto hace que el componente de página sea único de un SPA.

>[!NOTE]
>
>El Editor de SPA es la solución recomendada para proyectos que requieren SPA procesamiento del lado del cliente basado en el marco de trabajo (por ejemplo, React o Angular).

## Introducción {#introduction}

El componente de página de una SPA no proporciona los elementos HTML de sus componentes secundarios a través de un archivo JSP o HTL y objetos de recurso. Esta operación se delega en el marco SPA. La representación de los componentes secundarios se obtiene como una estructura de datos JSON (es decir, el modelo). A continuación, los componentes SPA se añaden a la página según el modelo JSON proporcionado. Como tal, la composición del cuerpo inicial del componente de página difiere de sus homólogos HTML procesados previamente.

## Administración de modelos de página {#page-model-management}

La resolución y la administración del modelo de página se delegan a un módulo [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) proporcionado. El SPA debe interactuar con el módulo `PageModelManager` cuando se inicializa para recuperar el modelo de página inicial y registrarse para actualizaciones del modelo, que principalmente se producen cuando el autor edita la página mediante el Editor de páginas. SPA proyecto puede acceder a `PageModelManager` como paquete npm. Como intérprete entre AEM y el SPA, el `PageModelManager` está pensado para acompañar al SPA.

Para permitir la creación de la página, se debe agregar una biblioteca de cliente denominada `cq.authoring.pagemodel.messaging` para proporcionar un canal de comunicación entre el SPA y el editor de páginas. Si el componente de página SPA hereda del componente wcm/core de la página, hay las siguientes opciones para que la categoría `cq.authoring.pagemodel.messaging` biblioteca de cliente esté disponible:

* Si la plantilla es editable, agregue la categoría biblioteca de cliente a la directiva de página.
* Añada la categoría biblioteca de cliente utilizando el `customfooterlibs.html` del componente de página.

No olvide limitar la inclusión de la categoría `cq.authoring.pagemodel.messaging` al contexto del editor de páginas.

## Tipo de datos de comunicación {#communication-data-type}

El tipo de datos de comunicación se establece como un elemento HTML dentro del componente Página AEM mediante el atributo `data-cq-datatype`. Cuando el tipo de datos de comunicación se establece en JSON, las solicitudes de GET llegan a los extremos del modelo Sling de un componente. Una vez que se produce una actualización en el editor de páginas, la representación JSON del componente actualizado se envía a la biblioteca del modelo de página. A continuación, la biblioteca del modelo de página advierte del SPA de las actualizaciones.

**Componente de página SPA -`body.html`**

```
<div id="page"></div>
```

Además de ser una buena práctica para no retrasar la generación del DOM, el marco SPA requiere que los scripts se añadan al final del cuerpo.

**Componente de página SPA -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

Las propiedades del metarecurso que describen el contenido SPA:

**Componente de página SPA -`customheaderlibs.html`**

```
<meta property="cq:datatype" data-sly-test="${wcmmode.edit || wcmmode.preview}" content="JSON"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.edit}" content="edit"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.preview}" content="preview"/>
<meta property="cq:pagemodel_root_url" data-sly-use.page="com.adobe.cq.sample.spa.journal.models.AppPage" content="${page.rootUrl}"/>
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
    <sly data-sly-call="${clientlib.css @ categories='we-retail-journal-react'}"/>
</sly>
```

>[!NOTE]
>
>El selector de modelo predeterminado se establece de forma estática al solicitar la representación del modelo de Sling de un componente.

## Metapropiedades {#meta-properties}

* `cq:wcmmode`: Modo WCM de los editores (p. ej. página, plantilla)
* `cq:pagemodel_root_url`: URL del modelo raíz de la aplicación. Importante al acceder directamente a una página secundaria, ya que el modelo de página secundaria es un fragmento del modelo raíz de la aplicación. A continuación, ` [PageModelManager](/help/sites-developing/spa-page-component.md)` vuelve a componer sistemáticamente el modelo inicial de la aplicación al entrar en la aplicación desde su punto de entrada raíz.

* `cq:pagemodel_router`: Habilitar o deshabilitar el  ` [ModelRouter](/help/sites-developing/spa-routing.md)` de la  `PageModelManager` biblioteca

* `cq:pagemodel_route_filters`: Lista separada por comas o expresiones regulares para proporcionar rutas que  ` [ModelRouter](/help/sites-developing/spa-routing.md)` deben ignorarse.

>[!CAUTION]
>
>Este documento utiliza la aplicación We.Retail Journal solo con fines de demostración. No debe utilizarse para ningún trabajo de proyecto.
>
>Cualquier proyecto AEM debe aprovechar el [AEM tipo de archivo del proyecto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html), que admite SPA proyectos mediante React o Angular y aprovecha el SDK de SPA.Todos los proyectos SPA en AEM deben basarse en el tipo de archivo Maven para SPA Starter Kit.

## Sincronización de superposiciones del editor de páginas {#page-editor-overlay-synchronization}

La sincronización de las superposiciones está garantizada por el mismo Observador de mutación proporcionado por la categoría `cq.authoring.page`.

## Configuración de estructura exportada JSON del modelo Sling {#sling-model-json-exported-structure-configuration}

Cuando las capacidades de enrutamiento están habilitadas, se supone que la exportación JSON de la SPA contiene las diferentes rutas de la aplicación gracias a la exportación JSON del componente de navegación AEM. La salida JSON del componente de navegación de AEM se puede configurar en la directiva de contenido de la página raíz de SPA mediante las dos propiedades siguientes:

* `structureDepth`: Número correspondiente a la profundidad del árbol exportado
* `structurePatterns`: Regex de la matriz de anexos correspondiente a la página que se va a exportar

Esto se puede mostrar en el contenido de muestra de SPA en `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`.
