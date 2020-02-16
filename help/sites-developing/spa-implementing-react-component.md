---
title: Implementación de un componente React para SPA
seo-title: Implementación de un componente React para SPA
description: En este artículo se muestra un ejemplo de cómo adaptar un componente de React simple y existente para que funcione con el Editor de SPA de AEM.
seo-description: En este artículo se muestra un ejemplo de cómo adaptar un componente de React simple y existente para que funcione con el Editor de SPA de AEM.
uuid: ae6a0a6f-0c3c-4820-9b58-c2a85a9f5291
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6ed15763-02cc-45d1-adf6-cf9e5e8ebdb0
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# Implementación de un componente React para SPA{#implementing-a-react-component-for-spa}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios del sitio web. Los desarrolladores quieren poder crear sitios con marcos de SPA y los autores quieren editar contenido sin problemas dentro de AEM para un sitio creado con marcos de SPA.

La función de creación de SPA ofrece una solución completa para admitir SPA en AEM. En este artículo se muestra un ejemplo de cómo adaptar un componente de React simple y existente para que funcione con el Editor de SPA de AEM.

>[!NOTE]
>
>El Editor de SPA es la solución recomendada para proyectos que requieren procesamiento del cliente basado en el marco de SPA (por ejemplo, React o Angular).

## Introducción {#introduction}

Gracias al sencillo y ligero contrato que requiere AEM y que se ha establecido entre el SPA y el Editor de SPA, tomar una aplicación de Javascript existente y adaptarla para su uso con un SPA en AEM es un asunto sencillo.

Este artículo ilustra el ejemplo del componente meteorológico en el SPA de muestra de We.Retail Journal.

Debe estar familiarizado con la [estructura de una aplicación SPA para AEM](/help/sites-developing/spa-getting-started-react.md) antes de leer este artículo.

## El componente meteorológico {#the-weather-component}

El componente meteorológico se encuentra en la parte superior izquierda de la aplicación We.Retail Journal. Muestra el clima actual de una ubicación definida, extrayendo datos del tiempo dinámicamente.

### Uso de la utilidad del tiempo {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

Al crear contenido de SPA en el Editor de SPA, el componente meteorológico aparece como cualquier otro componente de AEM, con una barra de herramientas y es editable.

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

La ciudad se puede actualizar en un cuadro de diálogo como cualquier otro componente de AEM.

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

El cambio se mantiene y el componente se actualiza automáticamente con nuevos datos meteorológicos.

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### Implementación de componentes meteorológicos {#weather-component-implementation}

El componente meteorológico se basa en realidad en un componente de React disponible al público, llamado [React Open Weather](https://www.npmjs.com/package/react-open-weather), que se ha adaptado para funcionar como un componente dentro de la aplicación SPA de muestra de We.Retail Journal.

Los siguientes son fragmentos de la documentación de NPM sobre el uso del componente React Open Weather.

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

Revisión del código del componente meteorológico personalizado ( `Weather.js`) en la aplicación We.Retail Journal:

* **Línea 16**: El widget Reaccionar tiempo abierto se carga según sea necesario.
* **Línea 46**: La `MapTo` función relaciona este componente de Reacción con un componente de AEM correspondiente para que se pueda editar en el Editor de SPA.

* **Líneas 22-29**: El `EditConfig` se define, comprobando si la ciudad se ha llenado y definiendo el valor si está vacía.

* **Líneas 31-44**: El componente Tiempo amplía la `Component` clase y proporciona los datos requeridos, tal como se definen en la documentación de uso de NPM para el componente React Open Weather y procesa el componente.

```
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
import {MapTo} from '@adobe/cq-react-editable-components';

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

Aunque ya debe existir un componente back-end, el desarrollador front-end puede aprovechar el componente React Open Weather en We.Retail Journal SPA con muy poca codificación.

## Etapa siguiente {#next-step}

Para obtener más información sobre el desarrollo de SPA para AEM, consulte el artículo [Desarrollo de SPA para AEM](/help/sites-developing/spa-architecture.md).
