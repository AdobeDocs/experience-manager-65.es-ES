---
title: Adición de ContextHub a las páginas y acceso a las tiendas
description: Agregue ContextHub a sus páginas para habilitar las funciones de ContextHub y para vincular a las bibliotecas de JavaScript de ContextHub
exl-id: ae745af9-b49f-46b9-ab48-2fd256e9a681
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Adición de ContextHub a las páginas y acceso a las tiendas {#adding-contexthub-to-pages-and-accessing-stores}

Agregue ContextHub a sus páginas para habilitar las funciones de ContextHub y para vincular a las bibliotecas de JavaScript de ContextHub.

La API de JavaScript de ContextHub proporciona acceso a los datos de contexto que administra ContextHub. Esta página describe brevemente las principales funciones de la API para acceder y manipular los datos de contexto. Siga los vínculos a la documentación de referencia de la API para ver información detallada y ejemplos de código.

## Adición de ContextHub a un componente de página {#adding-contexthub-to-a-page-component}

Para habilitar las funciones de ContextHub y vincular a las bibliotecas de JavaScript de ContextHub, incluya la `contexthub` componente en la `head` de la página. El código HTL del componente de página debe ser similar al siguiente ejemplo:

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

Tenga en cuenta que también debe configurar si la barra de herramientas de ContextHub aparece en el modo de vista previa. Consulte [Mostrar y ocultar la interfaz de usuario de ContextHub](ch-configuring.md#showing-and-hiding-the-contexthub-ui).

## Acerca de las tiendas ContextHub {#about-contexthub-stores}

Utilice los almacenes de ContextHub para mantener los datos de contexto. ContextHub proporciona los siguientes tipos de tiendas que forman la base de todos los tipos de tiendas:

* [PersistedStore](contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersistedJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

Todos los tipos de almacén son extensiones de [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) clase. Para obtener información sobre cómo crear un tipo de almacén, consulte [Crear tiendas personalizadas](ch-extend.md#creating-custom-store-candidates). Para obtener información acerca de los tipos de almacén de ejemplo, consulte [Candidatos de tienda de ContextHub de muestra](ch-samplestores.md).

### Modos de persistencia {#persistence-modes}

Las tiendas de Context Hub utilizan uno de los siguientes modos de persistencia:

* **Local:** Utiliza localStorage de HTML5 para mantener los datos. El almacenamiento local se mantiene en el explorador entre sesiones.
* **Sesión:** Utiliza sessionStorage de HTML5 para mantener los datos. El almacenamiento de sesión se mantiene durante la sesión del explorador y está disponible para todas las ventanas del explorador.
* **Cookie:** Utiliza la compatibilidad nativa del explorador con las cookies para el almacenamiento de datos. Los datos de cookies se envían y reciben del servidor en solicitudes HTTP.
* **Window.name:** Utiliza la propiedad window.name para mantener los datos.
* **Memoria:** Utiliza un objeto JavaScript para mantener los datos.

De forma predeterminada, ContextHub utiliza el modo de persistencia local. Si el explorador no admite ni permite el almacenamiento local de HTML5, se utiliza la persistencia de la sesión. Si el explorador no admite ni permite sessionStorage de HTML5, se utiliza la persistencia Window.name.

### Almacenar datos {#store-data}

Internamente, los datos se almacenan en una estructura de árbol, lo que permite agregar valores como tipos principales u objetos complejos. Cuando se agregan objetos complejos a los almacenes, las propiedades de los objetos forman ramas en el árbol de datos. Por ejemplo, el siguiente objeto complejo se agrega a un almacén vacío denominado ubicación:

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

ContextHub proporciona el [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) para manipular objetos JavaScript. Utilice las funciones de esta clase para manipular los objetos JavaScript antes de agregarlos a un almacén o después de obtenerlos de un almacén.

Además, la variable [`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) proporciona funciones para serializar objetos en cadenas y deserializar cadenas en objetos. Utilice esta clase para administrar datos JSON con el fin de admitir exploradores que no incluyan de forma nativa la variable `JSON.parse` y `JSON.stringify` funciones.

## Interactuar con tiendas de ContextHub {#interacting-with-contexthub-stores}

Utilice el [`ContextHub`](contexthub-api.md#ui-event-constants) Objeto JavaScript para obtener un almacén como objeto JavaScript. Una vez obtenido el objeto de almacén, puede manipular los datos que contiene. Utilice el [`getAllStores`](contexthub-api.md#getallstores) o el [`getStore`](contexthub-api.md#getstore-name) para obtener la tienda.

### Acceso a datos de tienda {#accessing-store-data}

El [`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) La clase JavaScript define varias funciones para interactuar con los datos del almacén. Las siguientes funciones almacenan y recuperan varios elementos de datos contenidos en objetos:

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

Los elementos de datos individuales se almacenan como un conjunto de pares clave/valor. Para almacenar y recuperar valores, especifique la clave correspondiente:

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

Tenga en cuenta que los candidatos de tienda personalizados pueden definir funciones adicionales que proporcionen acceso para almacenar datos.

>[!NOTE]
>
>ContextHub no tiene en cuenta de forma predeterminada la sesión iniciada actualmente en los servidores de publicación y ContextHub considera que estos usuarios son &quot;anónimos&quot;.
>
>Para que ContextHub sepa que los usuarios que han iniciado sesión deben cargar el almacén de perfiles. Consulte [código de muestra en GitHub aquí](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js).

### Eventos de ContextHub {#contexthub-eventing}

ContextHub incluye un marco de trabajo de eventos que le permite reaccionar automáticamente ante los eventos de almacenamiento. Cada objeto de almacén contiene un [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) que está disponible como el de la tienda [`eventing`](contexthub-api.md#eventing) propiedad. Utilice el [`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) o [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) para enlazar una función de JavaScript a un evento de tienda.

## Uso de ContextHub para manipular las cookies {#using-context-hub-to-manipulate-cookies}

La API de JavaScript de ContextHub proporciona compatibilidad entre exploradores para administrar las cookies del explorador. El [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) namespace define varias funciones para crear, manipular y eliminar cookies.

## Determinación de segmentos de ContextHub resueltos {#determining-resolved-contexthub-segments}

El motor de segmentos de ContextHub permite determinar qué segmentos registrados se resuelven en el contexto actual. Utilice la función getResolvedSegments de [`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) para recuperar segmentos resueltos. A continuación, utilice el `getName` o `getPath` función del [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) para probar un segmento.

### Segmentos de ContextHub {#contexthub-segments}

Los segmentos de ContextHub se instalan debajo de `/conf/<site>/settings/wcm/segments` nodo.

Los siguientes segmentos se instalan con [Sitio del tutorial de WKND.](getting-started.md)

* verano
* invierno

Las reglas que se utilizan para resolver estos segmentos se resumen de la siguiente manera:

* Primero, el [geolocation](ch-samplestores.md#contexthub-geolocation-sample-store-candidate) La tienda se utiliza para determinar la latitud del usuario.
* A continuación, el elemento de datos de mes del [tienda surferinfo](ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) determina qué estación se encuentra en esa latitud.

>[!WARNING]
>
>Los segmentos instalados se proporcionan como configuraciones de referencia para ayudarle a crear su propia configuración dedicada para su proyecto. No los utilice directamente.

## Depuración de ContextHub {#debugging-contexthub}

Existen varias opciones para depurar ContextHub, incluida la generación de registros. Consulte [Configuración de ContextHub para obtener más información.](ch-configuring.md#logging-debug-messages-for-contexthub)

## Consulte Información general sobre el marco de trabajo de ContextHub {#see-an-overview-of-the-contexthub-framework}

ContextHub proporciona un [página de diagnósticos](ch-diagnostics.md) donde puede ver una descripción general del marco de trabajo de ContextHub.
