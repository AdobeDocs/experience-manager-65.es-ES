---
title: Ampliación del seguimiento de Eventos
seo-title: Ampliación del seguimiento de Eventos
description: AEM Analytics le permite realizar un seguimiento de la interacción del usuario en su sitio web
seo-description: AEM Analytics le permite realizar un seguimiento de la interacción del usuario en su sitio web
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---


# Ampliación del seguimiento de Eventos{#extending-event-tracking}

AEM Analytics permite realizar un seguimiento de la interacción del usuario en el sitio web. Como desarrollador, es posible que necesite:

* Rastree cómo interactúan los visitantes con sus componentes. Esto se puede hacer con [eventos personalizados.](#custom-events)
* [Valores de acceso en ContextHub](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).
* [Añadir rellamadas](#adding-record-callbacks) de registro.

>[!NOTE]
>
>Esta información es básicamente genérica, pero utiliza [Adobe Analytics](/help/sites-administering/adobeanalytics.md) para ejemplos específicos.
>
>Para obtener información general sobre el desarrollo de componentes y cuadros de diálogo, consulte [Desarrollo de componentes](/help/sites-developing/components.md).

## Eventos personalizados {#custom-events}

Los eventos personalizados realizan un seguimiento de todo lo que dependa de la disponibilidad de un componente específico en la página. Esto también incluye eventos específicos de la plantilla, ya que el componente de página se trata como otro componente.

### Seguimiento de Eventos personalizados al cargar la página {#tracking-custom-events-on-page-load}

Esto se puede hacer usando el pseudoatributo `data-tracking` (el atributo de registro anterior aún se admite para compatibilidad con versiones anteriores). Puede agregarlo a cualquier etiqueta HTML.

La sintaxis para `data-tracking` es

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

Puede pasar cualquier número de pares clave-valor como el segundo parámetro, que se denomina carga útil.

Un ejemplo podría tener el siguiente aspecto:

```xml
<span data-tracking="{event:'blogEntryView',
                                values:{
                                   'blogEntryContentType': 'blog',
                                   'blogEntryUniqueID': '<%= xssAPI.encodeForJSString(entry.getId()) %>',
                                   'blogEntryTitle': '<%= xssAPI.encodeForJSString(entry.getTitle()) %>',
                                   'blogEntryAuthor':'<%= xssAPI.encodeForJSString(entry.getAuthor()) %>',
                                   'blogEntryPageLanguage':'<%= currentPage.getLanguage(true) %>'
                                },
                                componentPath:'myapp/component/mycomponent'}">
</span>
```

Al cargar la página, todos los atributos `data-tracking` se recopilarán y agregarán al almacén de eventos de ContextHub, donde se pueden asignar a eventos de Adobe Analytics. Adobe Analytics no rastreará los eventos que no estén asignados. Consulte [Conexión a Adobe Analytics](/help/sites-administering/adobeanalytics.md) para obtener más información sobre la asignación de eventos.

### Seguimiento de Eventos personalizados después de la carga de la página {#tracking-custom-events-after-page-load}

Para rastrear los eventos que se producen después de cargar una página (como las interacciones del usuario), utilice la función `CQ_Analytics.record` JavaScript:

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

Dónde

* `events` es una cadena o una matriz de cadenas (para varios eventos).

* `values` contiene todos los valores para rastrear
* `collect` es opcional y devuelve una matriz que contiene el evento y el objeto de datos.
* `options` es opcional y contiene opciones de seguimiento de vínculos como elemento HTML  `obj` y  ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`.

* `componentPath` es un atributo necesario y se recomienda establecerlo en  `<%=resource.getResourceType()%>`

Por ejemplo, con la siguiente definición, un usuario que haga clic en el vínculo **Saltar a arriba** provocará que se activen los dos eventos, `jumptop` y `headlineclick`:

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## Acceso a los valores en ContextHub {#accessing-values-in-the-contexthub}

La API JavaScript de ContextHub tiene una función `getStore(name)` que devuelve el almacén especificado, si está disponible. El almacén tiene una función `getItem(key)` que devuelve el valor de la clave especificada, si está disponible. Con la función `getKeys()` es posible recuperar una matriz de claves definidas para el almacén específico.

Puede recibir notificaciones de cambios de valor en un almacén enlazando una función mediante la función `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)`.

La mejor manera de recibir notificaciones sobre la disponibilidad inicial de ContextHub es utilizar la función `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`.

**Eventos adicionales para ContextHub:**

Todas las tiendas están listas para:

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

Específico de la tienda:

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>Consulte también la [Referencia completa de la API de ContextHub](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## Añadiendo llamadas de retorno de registros {#adding-record-callbacks}

Antes y después de que las rellamadas se registren usando las funciones `CQ_Analytics.registerBeforeCallback(callback,rank)` y `CQ_Analytics.registerAfterCallback(callback,rank)`.

Ambas funciones toman una función como el primer argumento y una clasificación como el segundo argumento, que dicta el orden en que se ejecutan las rellamadas.

Si la llamada de retorno devuelve false, no se ejecutarán las llamadas de retorno siguientes en la cadena de ejecución.
