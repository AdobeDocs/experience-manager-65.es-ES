---
title: Ejemplos de candidatos de la tienda ContextHub
seo-title: Ejemplos de candidatos de la tienda ContextHub
description: ContextHub proporciona varios candidatos de almacén de muestra que puede utilizar en sus soluciones
seo-description: ContextHub proporciona varios candidatos de almacén de muestra que puede utilizar en sus soluciones
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
translation-type: tm+mt
source-git-commit: e37ff1c9e657c580c607f2656adca01a2b39f81f

---


# Ejemplos de candidatos de la tienda ContextHub{#sample-contexthub-store-candidates}

ContextHub proporciona varios candidatos de almacén de muestra que puede utilizar en sus soluciones. Se proporciona la siguiente información para cada muestra:

* Dónde encontrar el código fuente para poder abrirlo con fines de aprendizaje.
* Cómo configurar las tiendas que se crean a partir de los candidatos de la tienda.
* Cómo se estructuran los datos del almacén para que pueda acceder a ellos.

>[!WARNING]
>
>Los candidatos del almacén de muestra se proporcionan como configuraciones de referencia para ayudarle a crear su propia configuración dedicada para su proyecto y, como tal, no debe utilizarse directamente.

## ejemplo de aem.segmentation, candidato a almacén {#aem-segmentation-sample-store-candidate}

Almacenar para segmentos de ContextHub resueltos y sin resolver. Recupera automáticamente segmentos desde el Administrador de segmentos de ContextHub.

### Ubicación de origen {#source-location-segmentation}

`/libs/settings/cloudsettings/legacy/contexthub/segmentation`

### Implementación de base {#base-implementation-segmentation}

El candidato de almacén de segmentación de aem se extiende [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configuración {#configuration-segmentation}

Al crear una tienda aem.segmentation, no es necesario proporcionar una configuración detallada. La configuración predeterminada especifica la ubicación de las definiciones de segmentos de ContextHub.

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"/etc/segmentation/contexthub.segment.js"
   }
}
```

## contexthub.geolocation Ejemplo de candidato a tienda {#contexthub-geolocation-sample-store-candidate}

El candidato al almacén de muestras de contexthub.geolocation utiliza Google Maps para obtener y almacenar información sobre la ubicación del cliente.

### Ubicación de origen {#source-location-geolocation}

`/libs/settings/cloudsettings/legacy/contexthub/geolocation`

### Implementación de base {#base-implementation-geolocation}

Se extiende el candidato del almacén contexthub.geolocation [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configuración {#configuration-geolocation}

La configuración predeterminada especifica información sobre el servicio Google y las coordenadas iniciales de latitud y longitud.

```xml
{
        "service": {
            "jsonp": false,
            "timeout": 1000,
            "ttl": 1800000,
            "secure": false,
            "host": "maps.googleapis.com",
            "port": 80,
            "path": "/maps/api/geocode/json"
        },

        "eventDeferring": 16,

        "html5coordinatesDiscoveryAPI": {
            "timeout": 30000,
            "ttl": 900000,
            "highAccuracy": false
        },

        "initialValues": {
            "latitude": 37.331375,
            "longitude": -121.893992
        }
    }
```

### Elementos de datos {#data-items-geolocation}

El almacén utiliza un árbol de datos similar al siguiente ejemplo:

```xml
{
   "latitude":"37.331375",
   "longitude":"-121.893992"
}
```

>[!NOTE]
>
>Una política de seguridad introducida en Chrome 50.x requiere que todas las llamadas relacionadas con la geolocalización se realicen a través de una conexión segura. Por lo tanto, AEM fuerza el uso de https para llamadas a la API de geolocalización si AEM también se está ejecutando sobre https. De lo contrario, se utiliza http para cumplir con la política del mismo origen. Consulte [esta entrada](https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only) del blog de Google para obtener más información sobre el cambio en Chrome.

## contexthub.surferinfo Ejemplo de candidato a tienda {#contexthub-surferinfo-sample-store-candidate}

Almacena información sobre el entorno de cliente actual, como el dispositivo, la ventana, el explorador, la fecha y la hora.

### Ubicación de origen {#source-location-surferinfo

`/libs/settings/cloudsettings/legacy/contexthub/surferinfo`

### Implementación de base {#base-implementation-surferinfo}

Se extiende el candidato del almacén contexthub.datetime [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore).

### Configuración {#configuration-surferinfo}

La configuración predeterminada se hereda de `ContextHub.Store.PersistedStore`.

### Elementos de datos {#data-items-surferinfo}

Las tiendas que utilizan este candidato de almacén tienen un árbol de datos similar al siguiente ejemplo:

```xml
{
   "display":{
      "resolution":{
         "width":1440,
         "height":900
      },
      "devicePixelRatio":1,
      "colorDepth":24,
      "nrOfColors":16777216,
      "pixelsPerInch":96,
      "orientation":{
         "mode":"landscape",
         "direction":"normal"
      }
   },
   "window":{
      "dimension":{
         "width":1395,
         "height":652
      },
      "percentageUsage":0.7
   },
   "browser":{
      "version":"39.0",
      "family":"Firefox",
      "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:39.0) Gecko/20100101 Firefox/39.0"
   },
   "device":{
      "category":"Desktop",
      "type":"Desktop",
      "model":"PC",
      "version":""
   },
   "isMobile":true,
   "os":{
      "name":"Mac OS X",
      "version":"10"
   },
   "year":2015,
   "month":7,
   "day":22,
   "hour":14,
   "minutes":1
}
```

## granite.emulators Ejemplo de Candidato a tienda {#granite-emulators-sample-store-candidate}

El candidato de almacén de muestras granite.emulators almacena información sobre los dispositivos cliente.

### Ubicación de origen {#source-location-emulators}

`/libs/settings/cloudsettings/legacy/contexthub/emulators`

### Implementación de base {#base-implementation-emulators}

Se extiende el candidato del almacén contexthub.geolocation [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore).

### Configuración {#configuration-emulators}

La configuración predeterminada incluye una matriz denominada `defaultEmulators` que contiene información sobre distintos dispositivos. Cuando cree una tienda, proporcione distintos perfiles de dispositivo en la propiedad Configuración de detalles según sea necesario, utilizando el formato que se ilustra en el siguiente ejemplo:

```xml
{
   "defaultEmulators":[
        {
            "id": "iphone-6",
            "title": "iPhone 6",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 750,
            "height": 1334,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 2
        },
        {
            "id": "iphone-6-plus",
            "title": "iPhone 6 Plus",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        },
        {
            "id": "galaxy-s4",
            "title": "Samsung Galaxy S4",
            "type": "mobile",
            "platform": "Android",
            "platformVersion": "4.4.2 KitKat",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        }
    ]
}
```

### Elementos de datos {#data-items-emulators}

El árbol de datos del almacén es similar al siguiente ejemplo:

```xml
{
   "devices":[
      {"id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
      },
      {"id":"ipad-3",
      "title":"iPad 3 / 4 / Air",
      "type":"tablet",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":1536,
      "height":2048,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"iphone-6",
      "title":"iPhone 6",
      "type":"mobile",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":750,
      "height":1334,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"galaxy-s4",
      "title":"Samsung Galaxy S4",
      "type":"mobile",
      "platform":"Android",
      "platformVersion":"4.4.2 KitKat",
      "width":1080,
      "height":1920,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":3
      }
   ],
   "currentDeviceId":"native",
   "orientations":[
      {"id":"landscape",
      "title":"Landscape"
      },
      {"id":"portrait",
       "title":"Portrait"
      }
   ],
   "currentDevice":{
      "id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
   }
}
```

## granite.profile Ejemplo de candidato de tienda {#granite-profile-sample-store-candidate}

Almacena información sobre el usuario actual.

### Ubicación de origen {#source-location-profile}

`/libs/settings/cloudsettings/legacy/contexthub/profile`

### Implementación de base {#base-implementation-profile}

Se extiende el candidato del almacén contexthub.datetime [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configuración {#configuration-profile}

Se utiliza la siguiente configuración predeterminada. No debe cambiar esta configuración.

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"${contexthub:/store/profile/path}.infinity.json"
   },
   "initialValues":{"path":"/home/users/a/anonymous"}
}
```

### Elementos de datos {#data-items-profile}

Las tiendas que utilizan este candidato de almacén tienen un árbol de datos similar al siguiente ejemplo:

```xml
{
   "displayName":"anonymous",
   "path":"/home/users/6/6zavE_DGre6Ad9Y5E0Ba",
   "avatar":"/etc/designs/default/images/social/avatar.png",
   "authorizableId":"anonymous"
}
```
