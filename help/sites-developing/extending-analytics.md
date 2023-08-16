---
title: Ampliación del seguimiento de eventos
seo-title: Extending Event Tracking
description: AEM Analytics permite rastrear la interacción del usuario en el sitio web
seo-description: AEM Analytics lets you track user interaction on your website
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
exl-id: a71d20e6-0321-4afb-95fe-6de8b7b37245
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# Ampliación del seguimiento de eventos{#extending-event-tracking}

AEM Analytics le permite realizar un seguimiento de la interacción del usuario con el sitio web. Como desarrollador, es posible que tenga que:

* Rastree cómo los visitantes interactúan con los componentes. Esto se puede hacer con [Eventos personalizados.](#custom-events)
* [Acceder a valores en ContextHub](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).
* [Añadir llamadas de retorno de registro](#adding-record-callbacks).

>[!NOTE]
>
>Esta información es básicamente genérica, pero utiliza [Adobe Analytics](/help/sites-administering/adobeanalytics.md) para ver ejemplos específicos.
>
>Para obtener información general sobre el desarrollo de componentes y cuadros de diálogo, consulte [Desarrollo de componentes](/help/sites-developing/components.md).

## Eventos personalizados {#custom-events}

Los eventos personalizados hacen un seguimiento de cualquier elemento que dependa de la disponibilidad de un componente específico en la página. Esto también incluye eventos específicos de la plantilla, ya que el componente de página se trata como otro componente.

### Seguimiento De Eventos Personalizados Al Cargar La Página {#tracking-custom-events-on-page-load}

Esto se puede hacer con el pseudoatributo `data-tracking` (el atributo de registro anterior sigue siendo compatible con la compatibilidad con versiones anteriores). Puede añadir esto a cualquier etiqueta de HTML.

La sintaxis para `data-tracking` es

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

Puede pasar cualquier número de pares clave-valor como segundo parámetro, que se denomina carga útil.

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

Al cargar la página, todos `data-tracking` Los atributos se recopilan y agregan al almacén de eventos de ContextHub, donde se pueden asignar a eventos de Adobe Analytics. Adobe Analytics no rastreará los eventos que no estén asignados. Consulte [Conexión a Adobe Analytics](/help/sites-administering/adobeanalytics.md) para obtener más información sobre la asignación de eventos.

### Seguimiento de eventos personalizados después de cargar la página {#tracking-custom-events-after-page-load}

Para realizar un seguimiento de los eventos que se producen después de cargar una página (como las interacciones del usuario), utilice el `CQ_Analytics.record` Función JavaScript:

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

Donde

* `events` es una cadena o una matriz de cadenas (para varios eventos).

* `values` contiene todos los valores que se van a rastrear
* `collect` es opcional y devuelve una matriz que contiene el evento y el objeto de datos.
* `options` es opcional y contiene opciones de seguimiento de vínculos como un elemento HTML `obj` y ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`.

* `componentPath` es un atributo necesario y se recomienda establecerlo en `<%=resource.getResourceType()%>`

Por ejemplo, con la siguiente definición, un usuario hace clic en **Saltar al principio** el vínculo provocará los dos eventos, `jumptop` y `headlineclick`, que se activará:

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## Acceso a los valores en ContextHub {#accessing-values-in-the-contexthub}

La API de JavaScript de ContextHub tiene un `getStore(name)` función que devuelve el almacén especificado, si está disponible. La tienda tiene un `getItem(key)` función que devuelve el valor de la clave especificada, si está disponible. Uso del `getKeys()` función es posible recuperar una matriz de claves definidas para el almacén específico.

Se le pueden notificar los cambios de valor en un almacén enlazando una función utilizando `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)` función.

La mejor manera de recibir notificaciones sobre la disponibilidad inicial de ContextHub es utilizar `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);` función.

**Eventos adicionales para ContextHub:**

Todas las tiendas listas:

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

Específico de la tienda:

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>Consulte también la información completa [Referencia de API de ContextHub](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## Adición de devoluciones de llamada de registro {#adding-record-callbacks}

Antes y después de registrar las llamadas de retorno mediante las funciones `CQ_Analytics.registerBeforeCallback(callback,rank)` y `CQ_Analytics.registerAfterCallback(callback,rank)`.

Ambas funciones toman una función como primer argumento y una clasificación como segundo argumento, lo que dicta el orden en que se ejecutan las llamadas de retorno.

Si la llamada de retorno devuelve el valor &quot;False&quot;, no se ejecutarán las llamadas de retorno siguientes en la cadena de ejecución.
