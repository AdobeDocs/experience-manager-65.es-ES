---
title: Implementación de un componente de React para SPA
seo-title: Implementación de un componente de React para SPA
description: Este artículo presenta un ejemplo de cómo adaptar un componente React simple y existente para trabajar con el Editor SPA de AEM.
seo-description: Este artículo presenta un ejemplo de cómo adaptar un componente React simple y existente para trabajar con el Editor SPA de AEM.
uuid: ae6a0a6f-0c3c-4820-9b58-c2a85a9f5291
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6ed15763-02cc-45d1-adf6-cf9e5e8ebdb0
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 2%

---


# Implementación de un componente de React para SPA{#implementing-a-react-component-for-spa}

Las aplicaciones de una sola página (SPA) pueden oferta de experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios con marcos de SPA y los autores quieren editar contenido dentro de AEM sin problemas para un sitio creado con marcos de SPA.

La función de creación de SPA oferta una solución completa para admitir SPA dentro de AEM. Este artículo presenta un ejemplo de cómo adaptar un componente React simple y existente para trabajar con el Editor SPA de AEM.

>[!NOTE]
>
>El Editor de SPA es la solución recomendada para proyectos que requieren SPA procesamiento del lado del cliente basado en el marco de trabajo (por ejemplo, React o Angular).

## Introducción {#introduction}

Gracias al sencillo y ligero contrato que requiere AEM y establecido entre el SPA y el Editor SPA, tomar una aplicación de Javascript existente y adaptarla para su uso con un SPA en AEM es un asunto sencillo.

Este artículo ilustra el ejemplo del componente meteorológico en el SPA de muestra de Historial We.Retail.

Debe estar familiarizado con la [estructura de una aplicación SPA para AEM](/help/sites-developing/spa-getting-started-react.md) antes de leer este artículo.

>[!CAUTION]
>Este documento utiliza la aplicación de Historial [We.Retail](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) únicamente con fines de demostración. No debe utilizarse para ningún trabajo de proyecto.
>
>Cualquier proyecto AEM debe aprovechar el [AEM Arquetipo de proyecto](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype/overview.html), que admite SPA proyectos usando React o Angular y aprovecha el SDK SPA.

## El componente meteorológico {#the-weather-component}

El componente meteorológico se encuentra en la parte superior izquierda de la aplicación de Historial We.Retail. Muestra el clima actual de una ubicación definida, extrayendo datos del tiempo dinámicamente.

### Uso de la utilidad del tiempo {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

Al crear contenido del SPA en el Editor de SPA, el componente meteorológico aparece como cualquier otro componente AEM, con una barra de herramientas y es editable.

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

La ciudad se puede actualizar en un cuadro de diálogo como cualquier otro componente AEM.

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

El cambio se mantiene y el componente se actualiza automáticamente con nuevos datos meteorológicos.

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### Implementación de componentes meteorológicos {#weather-component-implementation}

El componente meteorológico se basa en realidad en un componente de React disponible públicamente, llamado [React Open Weather](https://www.npmjs.com/package/react-open-weather), que se ha adaptado para funcionar como un componente dentro de la aplicación SPA de muestra de We.Retail Historial.

Los siguientes son fragmentos de la documentación de NPM sobre el uso del componente React Open Weather.

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

Revisión del código del componente meteorológico personalizado ( `Weather.js`) en la aplicación de Historial We.Retail:

* **Línea 16**: El widget Reaccionar tiempo abierto se carga según sea necesario.
* **Línea 46**: La  `MapTo` función relaciona este componente de Reacción con un componente de AEM correspondiente para que se pueda editar en el Editor de SPA.

* **Líneas 22-29**: El  `EditConfig` se define, comprobando si la ciudad se ha llenado y definiendo el valor si está vacía.

* **Líneas 31-44**: El componente Tiempo amplía la  `Component` clase y proporciona los datos requeridos, tal como se definen en la documentación de uso de NPM para el componente React Open Weather (Reacción del tiempo de apertura) y procesa el componente.

```javascript
/*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 ~ Copyright 2018 Adobe Systems Incorporated
 ~
 ~ Licensed under the Apache License, Version 2.0 (the "License");
 ~ you may not use this file except in compliance with the License.
 ~ You may obtain a copy of the License at
 ~
 ~     https://www.apache.org/licenses/LICENSE-2.0
 ~
 ~ Unless required by applicable law or agreed to in writing, software
 ~ distributed under the License is distributed on an "AS IS" BASIS,
 ~ WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 ~ See the License for the specific language governing permissions and
 ~ limitations under the License.
 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*/
import React, {Component} from 'react';
import ReactWeather from 'react-open-weather';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Weather.css');

const WeatherEditConfig = {

    emptyLabel: 'Weather',

    isEmpty: function() {
        return !this.props || !this.props.cq_model || !this.props.cq_model.city || this.props.cq_model.city.trim().length < 1;
    }
};

class Weather extends Component {

    render() {
        let apiKey = "12345678901234567890";
        let city;

        if (this.props.cq_model) {
            city = this.props.cq_model.city;
            return <ReactWeather key={'react-weather' + Date.now()} forecast="today" apikey={apiKey} type="city" city={city} />
        }

        return null;
    }
}

MapTo('we-retail-journal/global/components/weather')(Weather, WeatherEditConfig);
```

Aunque ya debe existir un componente back-end, el desarrollador front-end puede aprovechar el componente React Open Weather en la SPA de Historial We.Retail con muy poca codificación.

## Etapa siguiente {#next-step}

Para obtener más información sobre cómo desarrollar SPA para AEM, consulte el artículo [Desarrollar SPA para AEM](/help/sites-developing/spa-architecture.md).
