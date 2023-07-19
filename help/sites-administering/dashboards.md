---
title: Tableros
seo-title: Dashboards
description: AEM Aprenda a crear, configurar y desarrollar nuevos paneles de datos de.
seo-description: Learn how to create, configure and develop new AEM dashboards.
uuid: 3eadbba2-0ce1-41be-a9f8-e6cafa109893
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 40560e06-2508-45a4-a648-39629ed54f28
exl-id: 5b934e3a-f554-46ec-a913-8d570abb1503
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 3%

---

# Tableros{#dashboards}

AEM Al utilizar la opción, puede administrar una gran cantidad de contenido de diferentes tipos (por ejemplo, páginas o recursos). AEM Los paneles de DTM ofrecen una forma fácil de usar y personalizable de definir páginas que muestren datos consolidados.

>[!NOTE]
>
>AEM Los paneles de datos se crean por usuario, de modo que el usuario solo puede acceder a su propio panel.
>
>Sin embargo, [Plantillas de panel](#creating-a-dashboard-template) se puede utilizar para compartir la configuración común y el diseño del panel.

![chlimage_1-22](assets/chlimage_1-22.jpeg)

## Administración de tableros {#administering-dashboards}

### Creación De Un Tablero {#creating-a-dashboard}

Para crear un nuevo panel, siga estos pasos:

1. En el **Herramientas** , haga clic en **Consola de configuración**.
1. En el árbol, haga doble clic **Tablero**.
1. Clic **Nuevo panel**.
1. Escriba el **Título** (por ejemplo, Mi tablero) y **Nombre**.
1. Haga clic en **Crear**.

### Clonación De Un Tablero {#cloning-a-dashboard}

Es posible que desee tener varios paneles para ver rápidamente información sobre el contenido de diferentes vistas. AEM Para ayudarle a crear un nuevo tablero, proporciona una función de clonado que puede utilizar para duplicar un tablero existente. Para clonar un tablero, siga estos pasos:

1. En el **Herramientas** , haga clic en **Consola de configuración**.

1. En el árbol, haga clic en **Tablero**.
1. Haga clic en el tablero que desee clonar.

1. Clic **Clonar**.

1. Escriba el **Nombre** del nuevo tablero.

### Eliminación De Un Tablero {#removing-a-dashboard}

1. En el **Herramientas** , haga clic en **Consola de configuración**.

1. En el árbol, haga clic en **Tablero**.
1. Haga clic en el tablero que desee eliminar.

1. Haga clic en **Quitar**.

1. Haga clic en **Sí** para confirmar.

## Componentes del panel {#dashboard-components}

### Información general {#overview}

Los componentes del panel no son más que normales [AEM componentes de](/help/sites-developing/developing-components-samples.md). AEM En esta sección se describen los componentes de sistema de informes que se envían con.

### Componentes de informes de análisis web {#web-analytics-reporting-components}

AEM se envía con un conjunto de componentes que procesan varias métricas de su [SiteCatalyst](/help/sites-administering/adobeanalytics.md) datos. Estos componentes se enumeran en el Sidekick en la **Tablero** sección.

Cada componente del sistema de informes proporciona al menos tres pestañas:

* **Básico**: contiene la configuración principal.

* **Informe:** contiene la configuración específica de cada informe.
* **Estilo**: contiene la configuración de estilo como el tamaño y el margen del gráfico.

Los componentes de creación de informes se inicializan con una configuración predeterminada que le ayuda a configurar rápidamente el panel.

#### Configuración básica {#basic-configuration}

El **Básico** proporciona acceso a las siguientes entradas de configuración:

**Título** El título se muestra en el panel.

**Tipo de solicitud** La forma en que se solicitan los datos.

**Configuración de SiteCatalyst (opcional)** La configuración que desea utilizar para conectarse al SiteCatalyst. Si no se proporciona, se supone que la configuración está configurada en la página Tablero (a través de las propiedades de página).

**ID del grupo de informes (opcional)** El grupo de informes de SiteCatalyst que desea utilizar para generar el gráfico.

#### Configuración del informe {#report-configuration}

Para mostrar las estadísticas web, debe definir el intervalo de fechas de los datos que desea recuperar. El **Informe** proporciona dos campos para definir ese intervalo.

>[!NOTE]
>
>La configuración de un intervalo de fechas grande puede disminuir la capacidad de respuesta del panel.

**Fecha desde** Fecha absoluta o relativa desde la que se recuperan los datos.

**Fecha de finalización** Fecha absoluta o relativa en la que se recuperan los datos.

Cada componente también define configuraciones específicas.

#### Informe de tiempo extra {#overtime-report}

![chlimage_1-26](assets/chlimage_1-26a.png)

**Granularidad de fecha** Unidad de tiempo del eje X (por ejemplo, día, hora).

**Métricas** La lista de eventos que desea mostrar.

**Elementos** La lista de elementos que desglosa los datos de las métricas en el gráfico.

#### Informe de lista clasificada {#ranked-list-report}

![chlimage_1-27](assets/chlimage_1-27a.png)

**Elementos** Elemento que desglosa los datos de las métricas en el gráfico.

**Métricas** El evento que desea mostrar.

**No. de elementos principales** Número de elementos mostrados por el informe.

#### Informe clasificado {#ranked-report}

![chlimage_1-28](assets/chlimage_1-28a.png)

**Métricas** El evento que desea mostrar.

**Elementos** Elemento que desglosa los datos de las métricas en el gráfico.

#### Informe de sección de sitio principal {#top-site-section-report}

Este componente muestra un gráfico con la sección más visitada de un sitio web según la siguiente configuración.

![chlimage_1-29](assets/chlimage_1-29a.png)

**No. de elementos principales** Número de secciones mostradas por en el informe.

#### Informe de tendencias {#trended-report}

![chlimage_1-30](assets/chlimage_1-30a.png)

**Granularidad de fecha** Unidad de tiempo del eje X (por ejemplo, día, hora).

**Métricas** El evento que desea mostrar.

**Elementos** Elemento que desglosa los datos de las métricas en el gráfico.

## Ampliación del panel {#extending-dashboard}

### Información general {#overview-1}

Los paneles son páginas normales ( `cq:Page`), por lo tanto, cualquier componente se puede utilizar para montar paneles.

Hay un grupo de componentes predeterminado `Dashboard` que contiene los componentes de informes de analytics habilitados en la plantilla de forma predeterminada.

### Creación De Una Plantilla De Tablero {#creating-a-dashboard-template}

Una plantilla define el contenido predeterminado de un nuevo panel. Puede utilizar varias plantillas para crear diferentes tipos de paneles.

Las plantillas de tablero se crean como otras plantillas de página, excepto que se almacenan en `/libs/cq/dashboards/templates/`. Consulte la [Creando plantilla de página de contenido](/help/sites-developing/website.md#creating-the-contentpage-template) sección.

>[!NOTE]
>
>Las plantillas de panel se comparten entre los usuarios.

### Desarrollo de un componente de panel {#developing-a-dashboard-component}

AEM El desarrollo de un componente Panel consiste en crear un componente de normal. En esta sección se describe un ejemplo de un componente que muestra los 10 principales colaboradores.

![chlimage_1-31](assets/chlimage_1-31a.png)

Los componentes de autor principales se almacenan en el repositorio en `/apps/geometrixx-outdoors/components/reporting` y se compone de :

1. a `jsp` que lee datos jcr y define el `html` marcador.

1. una biblioteca del lado del cliente que contiene una `js` que recupera y ordena los datos y, a continuación, rellena el `html` marcador.

![chlimage_1-32](assets/chlimage_1-32a.png)

El siguiente archivo JavaScript se define en la variable `geout.reporting.topauthors` [Biblioteca de cliente](/help/sites-developing/clientlibs.md) como elemento secundario del propio componente.

El [QueryBuilder](/help/sites-developing/querybuilder-api.md) se utiliza para consultar el repositorio para leer `cq:AuditEvent` nodos. El resultado de la consulta es un objeto JSON del que se extraen las contribuciones de los autores.

#### top_authors.js {#top-authors-js}

```
$.ajax({
  url: "/bin/querybuilder.json",
  cache: false,
  data: {
       "orderby": "cq:time",
       "orderby.sort": "desc",
       "p.hits": "full",
       "p.limit": 100,
       "path": "/var/audit/com.day.cq.wcm.core.page/",
       "type": "cq:AuditEvent"
   },
  dataType: "json"
}).done(function( res ) {
    var authors = {};
    // from JSON to Object
    for(var r in res.hits) {
        var userId = res.hits[r].userId;
        if(userId == undefined) {
            continue;
        }
        var auth = authors[userId] || {userId : userId};
        auth.contrib = (auth.contrib || 0) +1;

        authors[userId] = auth;
    }

    // order by contribution
    var orderedByContrib = [];
    for(var a in authors) {
        orderedByContrib.push(authors[a]);
    }
    orderedByContrib.sort(function(a,b){return b.contrib - a.contrib});

    // produce the list
    for (var i=0, tot=orderedByContrib.length; i < tot; i++) {
        var current = orderedByContrib[i];
        $("<div> #" + (i + 1) +" "+ current.userId + " (" + current.contrib +" contrib.)</div>").appendTo("#authors-list");

    }
});
```

El `JSP` incluye ambos `global.jsp` y `clientlib`.

#### top_authors.jsp {#top-authors-jsp}

```java
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%
%><%@include file="/libs/foundation/global.jsp" %><%
%>
<ui:includeClientLib categories="geout.reporting.topauthors" />
<%
String reportletTitle = properties.get("title", "Top Authors");
%>
<html>
     <h3><%=xssAPI.encodeForHTML(reportletTitle) %></h3>
     <div id="authors-list"></div>
</html>
```
