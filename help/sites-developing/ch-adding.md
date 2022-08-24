---
title: Agregar ContextHub a páginas y acceder a tiendas
description: Agregue ContextHub a sus páginas para habilitar las funciones de ContextHub y vincular a las bibliotecas JavaScript de ContextHub
exl-id: ae745af9-b49f-46b9-ab48-2fd256e9a681
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# Agregar ContextHub a páginas y acceder a tiendas {#adding-contexthub-to-pages-and-accessing-stores}

Agregue ContextHub a sus páginas para habilitar las funciones de ContextHub y vincular a las bibliotecas JavaScript de ContextHub.

La API de JavaScript de ContextHub proporciona acceso a los datos de contexto que administra ContextHub. En esta página se describen brevemente las principales funciones de la API para acceder y manipular los datos de contexto. Siga los vínculos a la documentación de referencia de la API para ver información detallada y ejemplos de código.

## Adición de ContextHub a un componente de página {#adding-contexthub-to-a-page-component}

Para habilitar las funciones de ContextHub y vincular a las bibliotecas JavaScript de ContextHub, incluya la variable `contexthub` en el `head` de su página. El código HTL del componente de página debe parecerse al siguiente ejemplo:

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

Tenga en cuenta que también debe configurar si la barra de herramientas de ContextHub aparece en el modo de vista previa. Consulte [Mostrar y ocultar la interfaz de usuario de ContextHub](ch-configuring.md#showing-and-hiding-the-contexthub-ui).

## Acerca de las tiendas de ContextHub {#about-contexthub-stores}

Utilice los almacenes de ContextHub para conservar los datos de contexto. ContextHub proporciona los siguientes tipos de tiendas que forman la base de todos los tipos de tiendas:

* [PersistedStore](contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersistedJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

Todos los tipos de tienda son extensiones de [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) Clase . Para obtener información sobre la creación de un nuevo tipo de almacén, consulte [Creación de tiendas personalizadas](ch-extend.md#creating-custom-store-candidates). Para obtener información sobre los tipos de almacén de muestra, consulte [Ejemplos de candidatos a la tienda de ContextHub](ch-samplestores.md).

### Modos de persistencia {#persistence-modes}

Los almacenes de ContextHub utilizan uno de los siguientes modos de persistencia:

* **Local:** Utiliza HTML5 localStorage para mantener los datos. El almacenamiento local se mantiene en el explorador en todas las sesiones.
* **Sesión:** Utiliza sessionStorage de HTML5 para mantener los datos. El almacenamiento de sesión se mantiene durante la sesión del explorador y está disponible para todas las ventanas del explorador.
* **Cookie:** Utiliza la compatibilidad nativa de cookies del explorador para el almacenamiento de datos. Los datos de cookies se envían desde y hacia el servidor en solicitudes HTTP.
* **Window.name:** Utiliza la propiedad window.name para mantener los datos.
* **Memoria:** Utiliza un objeto Javascript para mantener los datos.

De forma predeterminada, ContextHub utiliza el modo de persistencia local. Si el explorador no admite o no permite HTML5 localStorage, se utiliza la persistencia de sesión. Si el explorador no admite o no permite HTML5 sessionStorage, se utiliza la persistencia Window.name.

### Almacenar datos {#store-data}

Internamente, el almacenamiento de datos forma una estructura de árbol, que permite agregar valores como tipos primarios u objetos complejos. Cuando se agregan objetos complejos a los almacenes, las propiedades de objeto forman ramas en el árbol de datos. Por ejemplo, el siguiente objeto complejo se agrega a una ubicación de almacén vacía denominada:

```javascript
Object {
   number: 321,
   data: {
      city: "Basel",
      country: "Switzerland",
      details: {
         population: 173330,
         elevation: 260
      }
   }
}
```

La estructura de árbol de los datos del almacén se puede conceptualizar de la siguiente manera:

```text
/
|- number
|- data
      |- city
      |- country
      |- details
            |- population
            |- elevation
```

La estructura de árbol define los elementos de datos del almacén como pares clave/valor. En el ejemplo anterior, la clave `/number` corresponde al valor `321`y la clave `/data/country` corresponde al valor `Switzerland`.

### Manipulación de objetos {#manipulating-objects}

ContextHub proporciona [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) para manipular objetos de JavaScript. Utilice las funciones de esta clase para manipular objetos de JavaScript antes de agregarlos a una tienda o después de obtenerlos de una tienda.

Además, la variable [`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) proporciona funciones para serializar objetos en cadenas y deserializar cadenas en objetos. Utilice esta clase para gestionar datos JSON para admitir exploradores que no incluyan de forma nativa el `JSON.parse` y `JSON.stringify` funciones.

## Interactuar con las tiendas de ContextHub {#interacting-with-contexthub-stores}

Utilice la variable [`ContextHub`](contexthub-api.md#ui-event-constants) Objeto Javascript para obtener un almacén como objeto Javascript. Una vez obtenido el objeto de almacén, puede manipular los datos que contiene. Utilice la variable [`getAllStores`](contexthub-api.md#getallstores) o [`getStore`](contexthub-api.md#getstore-name) para obtener el almacén.

### Acceso a los datos del almacén {#accessing-store-data}

La variable [`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) La clase Javascript define varias funciones para interactuar con datos de almacenamiento. Las siguientes funciones almacenan y recuperan varios elementos de datos contenidos en objetos:

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

Los elementos de datos individuales se almacenan como un conjunto de pares clave/valor. Para almacenar y recuperar valores, especifique la clave correspondiente:

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

Tenga en cuenta que los candidatos de tiendas personalizadas pueden definir funciones adicionales que proporcionan acceso a los datos de almacenamiento.

>[!NOTE]
>
>De forma predeterminada, ContextHub no tiene en cuenta el inicio de sesión que se está utilizando en los servidores de publicación y ContextHub considera a estos usuarios como &quot;anónimos&quot;.
>
>Puede hacer que ContextHub sepa de los usuarios que iniciaron sesión cargando el almacén de perfiles. Consulte [código de muestra en GitHub aquí](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js).

### Eventos de ContextHub {#contexthub-eventing}

ContextHub incluye un marco de eventos que le permite reaccionar automáticamente al almacenar eventos. Cada objeto de almacén contiene un [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) objeto que está disponible como [`eventing`](contexthub-api.md#eventing) propiedad. Utilice la variable [`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) o [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) para enlazar una función de JavaScript a un evento de tienda.

## Uso de ContextHub para manipular cookies {#using-context-hub-to-manipulate-cookies}

La API de JavaScript de Context Hub proporciona compatibilidad con exploradores múltiples para administrar cookies de exploradores. La variable [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) namespace define varias funciones para crear, manipular y eliminar cookies.

## Determinación de segmentos de ContextHub resueltos {#determining-resolved-contexthub-segments}

El motor de segmentos de ContextHub permite determinar cuál de los segmentos registrados se resuelve en el contexto actual. Utilice la función getResolvedSegments de la función [`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) para recuperar segmentos resueltos. A continuación, utilice el `getName` o `getPath` de la función [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) para probar un segmento.

### Segmentos de ContextHub {#contexthub-segments}

Los segmentos de ContextHub se instalan debajo de `/conf/<site>/settings/wcm/segments` nodo .

Los siguientes segmentos se instalan con la variable [Sitio del tutorial de WKND.](getting-started.md)

* verano
* invierno

Las reglas que se utilizan para resolver estos segmentos se resumen de la siguiente manera:

* Primero, la función [geolocalización](ch-samplestores.md#contexthub-geolocation-sample-store-candidate) store se utiliza para determinar la latitud del usuario.
* A continuación, el elemento de datos del mes de la variable [surferinfo store](ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) determina en qué temporada se encuentra en esa latitud.

>[!WARNING]
>
>Los segmentos instalados se proporcionan como configuraciones de referencia para ayudarle a crear su propia configuración dedicada para su proyecto y, como tal, no debe utilizarse directamente.

## Depuración de ContextHub {#debugging-contexthub}

Existen varias opciones para depurar ContextHub, incluida la generación de registros. Consulte [Configuración de ContextHub para obtener más información.](ch-configuring.md#logging-debug-messages-for-contexthub)

## Consulte Información general sobre el marco de ContextHub {#see-an-overview-of-the-contexthub-framework}

ContextHub proporciona un [página de diagnóstico](ch-diagnostics.md) donde puede ver información general del marco de ContextHub.
