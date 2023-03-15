---
title: Implementación de un componente de React para SPA
seo-title: Implementing a React Component for SPA
description: AEM SPA En este artículo se presenta un ejemplo de cómo adaptar un componente React simple y existente para trabajar con el Editor de.
seo-description: This article presents an example of how to adapt a simple, existing React component to work with the AEM SPA Editor.
uuid: ae6a0a6f-0c3c-4820-9b58-c2a85a9f5291
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6ed15763-02cc-45d1-adf6-cf9e5e8ebdb0
docset: aem65
exl-id: f4959c12-54c5-403a-9973-7a4ab5f16bed
source-git-commit: afd2afe182d65e64c0ad851b86021886078a9dd5
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 12%

---

# Implementación de un componente de React para SPA{#implementing-a-react-component-for-spa}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. SPA AEM SPA Los desarrolladores quieren poder crear sitios utilizando marcos de trabajo de y los autores quieren editar contenido sin problemas en para un sitio creado con marcos de trabajo de la.

SPA SPA AEM La función de creación de ofrece una solución completa para la asistencia de la creación de contenido en el ámbito de la. AEM SPA En este artículo se presenta un ejemplo de cómo adaptar un componente React simple y existente para trabajar con el Editor de.

>[!NOTE]
>
>SPA SPA El editor de segmentos es la solución recomendada para los proyectos que requieren un procesamiento basado en el marco de trabajo del cliente basado en el marco de trabajo de la aplicación (por ejemplo, React o Angular).

## Introducción {#introduction}

AEM SPA SPA SPA AEM Gracias al contrato sencillo y ligero que requiere la aplicación y que se establece entre el Editor de Javascript y el Editor de Javascript, la adopción de una aplicación JavaScript existente y su adaptación para su uso con una aplicación de Javascript en el Editor de Javascript es un asunto sencillo y directo.

SPA Este artículo ilustra el ejemplo del componente meteorológico en la muestra de We.Retail Journal.

Debe estar familiarizado con las [SPA AEM estructura de una aplicación de para la](/help/sites-developing/spa-getting-started-react.md) antes de leer este artículo.

>[!CAUTION]
>Este documento usa el [Aplicación de diario We.Retail](https://github.com/adobe/aem-sample-we-retail-journal) únicamente con fines de demostración. No debe utilizarse para ningún trabajo de proyecto.
>
>Cualquier proyecto AEM debería aprovechar el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es), que admite proyectos de SPA que utilizan React o Angular y aprovecha el SDK de SPA.

## El componente Meteorológico {#the-weather-component}

El componente meteorológico se encuentra en la parte superior izquierda de la aplicación We.Retail Journal. Muestra el tiempo actual de una ubicación definida, extrayendo datos meteorológicos de forma dinámica.

### Uso del widget del tiempo {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

SPA SPA AEM Al crear contenido de la en el Editor de, el componente meteorológico aparece como cualquier otro componente de la, se completa con una barra de herramientas y se puede editar.

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

AEM La ciudad se puede actualizar en un cuadro de diálogo como cualquier otro componente de la.

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

El cambio se mantiene y el componente se actualiza automáticamente con nuevos datos meteorológicos.

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### Implementación del componente meteorológico {#weather-component-implementation}

El componente meteorológico en realidad se basa en un componente React disponible públicamente, llamado [Tiempo abierto en React](https://www.npmjs.com/package/react-open-weather)SPA , que se ha adaptado para que funcione como un componente dentro de la aplicación de ejemplo de We.Retail Journal.

Los siguientes son fragmentos de la documentación de NPM del uso del componente React Open Weather.

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

Revisión del código del componente meteorológico personalizado ( `Weather.js`) en la aplicación We.Retail Journal:

* **Línea 16**: El widget React Open Weather se carga según sea necesario.
* **Línea 46**: La `MapTo` AEM SPA relaciona este componente de React con un componente correspondiente de manera que se pueda editar en el Editor de la.

* **Líneas 22-29**: La `EditConfig` está definida, comprobando si la ciudad se ha rellenado y definiendo el valor si está vacío.

* **Líneas 31-44**: El componente Tiempo amplía la variable `Component` y proporciona los datos necesarios tal como se definen en la documentación de uso de NPM para el componente React Open Weather y procesa el componente.

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

SPA Aunque ya debe existir un componente back-end, el desarrollador front-end puede aprovechar el componente React Open Weather en la publicación de We.Retail Journal con muy poca codificación.

## Siguiente paso {#next-step}

SPA AEM Para obtener más información sobre el desarrollo de la para obtener más información, consulte el artículo [SPA AEM Desarrollo de la](/help/sites-developing/spa-architecture.md).
