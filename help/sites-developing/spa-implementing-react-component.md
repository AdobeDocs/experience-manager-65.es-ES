---
title: Implementación de un componente de React para SPA
seo-title: Implementing a React Component for SPA
description: Este artículo presenta un ejemplo de cómo adaptar un componente React simple y existente para trabajar con el AEM SPA Editor.
seo-description: This article presents an example of how to adapt a simple, existing React component to work with the AEM SPA Editor.
uuid: ae6a0a6f-0c3c-4820-9b58-c2a85a9f5291
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6ed15763-02cc-45d1-adf6-cf9e5e8ebdb0
docset: aem65
exl-id: f4959c12-54c5-403a-9973-7a4ab5f16bed
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 6%

---

# Implementación de un componente de React para SPA{#implementing-a-react-component-for-spa}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios mediante marcos de SPA y los autores quieren editar contenido sin problemas dentro de AEM para un sitio creado mediante marcos de SPA.

La función de creación de SPA ofrece una solución completa para admitir SPA dentro de AEM. Este artículo presenta un ejemplo de cómo adaptar un componente React simple y existente para trabajar con el AEM SPA Editor.

>[!NOTE]
>
>El Editor de SPA es la solución recomendada para proyectos que requieren SPA procesamiento del lado del cliente basado en el marco de trabajo (por ejemplo, React o Angular).

## Introducción {#introduction}

Gracias al sencillo y ligero contrato que requiere AEM y establece entre el SPA y el Editor de SPA, tomar una aplicación de Javascript existente y adaptarla para su uso con un SPA en AEM es un asunto directo.

Este artículo ilustra el ejemplo del componente meteorológico en el SPA de muestra de We.Retail Journal.

Debe estar familiarizado con el [estructura de una solicitud SPA para AEM](/help/sites-developing/spa-getting-started-react.md) antes de leer este artículo.

>[!CAUTION]
>Este documento utiliza la variable [Aplicación de diario We.Retail](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) únicamente con fines de demostración. No debe utilizarse para ningún trabajo de proyecto.
>
>Cualquier proyecto AEM debería aprovechar el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es), que admite SPA proyectos que utilizan React o Angular y aprovecha el SDK de SPA.

## El componente meteorológico {#the-weather-component}

El componente meteorológico se encuentra en la parte superior izquierda de la aplicación We.Retail Journal. Muestra el clima actual de una ubicación definida, obteniendo datos del tiempo de forma dinámica.

### Uso del widget meteorológico {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

Al crear contenido del SPA en el Editor de SPA, el componente meteorológico aparece como cualquier otro componente de AEM, se completa con una barra de herramientas y se puede editar.

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

La ciudad se puede actualizar en un cuadro de diálogo como cualquier otro componente AEM.

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

El cambio se mantiene y el componente se actualiza automáticamente con nuevos datos meteorológicos.

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### Implementación de componentes meteorológicos {#weather-component-implementation}

El componente meteorológico se basa en un componente React disponible públicamente, llamado [React Open Weather](https://www.npmjs.com/package/react-open-weather), que se ha adaptado para funcionar como componente dentro de la aplicación de SPA de muestra de We.Retail Journal.

A continuación se muestran algunos fragmentos de la documentación de NPM sobre el uso del componente React Open Weather.

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

Revisión del código del componente meteorológico personalizado ( `Weather.js`) en la aplicación We.Retail Journal:

* **Línea 16**: El widget React Open Weather se carga según sea necesario.
* **Línea 46**: La variable `MapTo` relaciona este componente React con un componente AEM correspondiente para que se pueda editar en el Editor de SPA.

* **Líneas 22-29**: La variable `EditConfig` está definida, comprobando si la ciudad se ha rellenado y definiendo el valor si está vacío.

* **Líneas 31-44**: El componente Tiempo extiende el `Component` y proporciona los datos requeridos tal como se definen en la documentación de uso de NPM para el componente React Open Weather y procesa el componente.

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

Aunque ya debe existir un componente back-end, el desarrollador front-end puede aprovechar el componente React Open Weather en la SPA We.Retail Journal con muy poca codificación.

## Siguiente paso {#next-step}

Para obtener más información sobre el desarrollo de SPA para AEM, consulte el artículo [Desarrollo de SPA para AEM](/help/sites-developing/spa-architecture.md).
