---
title: 'Introducción a la SPA en AEM: reaccionar'
seo-title: 'Introducción a la SPA en AEM: reaccionar'
description: Este artículo presenta una aplicación de SPA de muestra, explica cómo se organiza y le permite ponerse en marcha con sus propios SPA rápidamente usando el marco de React.
seo-description: Este artículo presenta una aplicación de SPA de muestra, explica cómo se organiza y le permite ponerse en marcha con sus propios SPA rápidamente usando el marco de React.
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 1%

---


# Introducción a SPA en AEM - Reacción{#getting-started-with-spas-in-aem-react}

Las aplicaciones de una sola página (SPA) pueden oferta de experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios con marcos de SPA y los autores quieren editar contenido dentro de AEM sin problemas para un sitio creado con marcos de SPA.

La función de creación de SPA oferta una solución completa para admitir SPA dentro de AEM. Este artículo presenta una aplicación de SPA simplificada en el marco de React, explica cómo se ha creado, permitiéndole ponerse en marcha con su propia SPA rápidamente.

>[!NOTE]
>
>Este artículo se basa en el marco de React. Para ver el documento correspondiente para Angular framework, consulte [Introducción a SPA en AEM - Angular](/help/sites-developing/spa-getting-started-angular.md).

>[!NOTE]
>
>El Editor de SPA es la solución recomendada para proyectos que requieren SPA procesamiento del lado del cliente basado en el marco de trabajo (por ejemplo, React o Angular).

## Introducción {#introduction}

Este artículo resume el funcionamiento básico de un simple SPA y el mínimo que necesita saber para que el suyo funcione.

Para obtener más información sobre el funcionamiento de SPA en AEM, consulte los siguientes documentos:

* [SPA Introducción y Tutorial](/help/sites-developing/spa-walkthrough.md)
* [Introducción a la creación de SPA](/help/sites-developing/spa-overview.md)
* [SPA modelo](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>Para poder crear contenido dentro de un SPA, el contenido debe almacenarse en AEM y ser expuesto por el modelo de contenido.
>
>Una SPA desarrollada fuera de AEM no será autorizada si no respeta el contrato del modelo de contenido.

Este documento recorrerá la estructura de un SPA simplificado creado con el marco de React e ilustrará cómo funciona para que pueda aplicar este entendimiento a su propia SPA.

## Dependencias, configuración y generación {#dependencies-configuration-and-building}

Además de la dependencia de React esperada, el SPA de muestra puede aprovechar bibliotecas adicionales para hacer que la creación del SPA sea más eficiente.

### Dependencias {#dependencies}

El archivo `package.json` define los requisitos del paquete de SPA general. Las dependencias de AEM mínimas para un SPA en funcionamiento se enumeran aquí.

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

Dado que este ejemplo se basa en el marco de React, hay dos dependencias específicas de React que son obligatorias en el archivo `package.json`:

```
react
 react-dom
```

El `aem-clientlib-generator` se aprovecha para hacer que la creación de bibliotecas de cliente sea automática como parte del proceso de compilación.

`"aem-clientlib-generator": "^1.4.1",`

Puede encontrar más detalles sobre esto [en GitHub aquí](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>La versión mínima del `aem-clientlib-generator` requerido es 1.4.1.

El `aem-clientlib-generator` se configura en el archivo `clientlib.config.js` de la siguiente manera.

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-react-app/clientlibs",

    libs: {
        name: "my-react-app",
        allowProxy: true,
        categories: ["my-react-app"],
        embed: ["my-react-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### Compilando {#building}

En realidad, la creación de la aplicación aprovecha [Webpack](https://webpack.js.org/) para la transpilación, además del generador aem-clientlib-para la creación automática de la biblioteca del cliente. Por lo tanto, el comando build será similar a:

`"build": "webpack && clientlib --verbose"`

Una vez creado, el paquete se puede cargar en una instancia de AEM.

### Tipo de archivo del proyecto AEM {#aem-project-archetype}

Cualquier proyecto AEM debe aprovechar el [AEM Arquetipo de proyecto](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype/overview.html), que admite SPA proyectos usando React o Angular y aprovecha el SDK SPA.

## Estructura de la aplicación {#application-structure}

Si se incluyen las dependencias y se crea la aplicación tal como se ha descrito anteriormente, dispondrá de un paquete de SPA que podrá cargar en la instancia de AEM.

La siguiente sección de este documento le explicará cómo se estructura un SPA en AEM, los archivos importantes que dirigen la aplicación y cómo funcionan juntos.

Un componente de imagen simplificado se utiliza como ejemplo, pero todos los componentes de la aplicación se basan en el mismo concepto.

### index.js {#index-js}

El punto de entrada al SPA es, por supuesto, el archivo `index.js` mostrado aquí simplificado para centrarse en el contenido importante.

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/aem-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

La función principal de `index.js` es aprovechar la función `ReactDOM.render` para determinar en qué parte del DOM se inyecta la aplicación.

Se trata de un uso estándar de esta función, no exclusivo de esta aplicación de ejemplo.

#### Creación de instancias estáticas {#static-instantiation}

Cuando se crea una instancia del componente mediante una plantilla de componente (por ejemplo, JSX), el valor debe pasarse del modelo a las propiedades del componente.

### App.js {#app-js}

Al procesar la aplicación, `index.js` llama a `App.js`, que se muestra aquí en una versión simplificada para centrarse en el contenido importante.

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` sirve principalmente para ajustar los componentes raíz que componen la aplicación. El punto de entrada de cualquier aplicación es la página.

### Page.js {#page-js}

Al procesar la página, `App.js` llama a `Page.js` en una versión simplificada.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

En este ejemplo, la clase `AppPage` amplía `Page`, que contiene los métodos de contenido interno que se pueden utilizar.

El `Page` ingesta la representación JSON del modelo de página y procesa el contenido para ajustar/decorar cada elemento de la página. Puede encontrar más detalles sobre el `Page` en el documento [Modelo de SPA](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### Image.js {#image-js}

Con la página representada, se pueden procesar los componentes como `Image.js`, como se muestra aquí.

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Image.css');

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function() {
        return !this.props || !this.props.src || this.props.src.trim().length < 1;
    }
};

class Image extends Component {

    render() {
        return (<img src={this.props.src}>);
    }
}

MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);
```

La idea central de SPA en AEM es la idea de asignar SPA componentes a AEM componentes y actualizar el componente cuando se modifica el contenido (y viceversa). Consulte el documento [Información general del editor de SPA](/help/sites-developing/spa-overview.md) para obtener un resumen de este modelo de comunicación.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

El método `MapTo` asigna el componente de SPA al componente de AEM. Admite el uso de una sola cadena o una matriz de cadenas.

`ImageEditConfig` es un objeto de configuración que contribuye a habilitar las capacidades de creación de un componente proporcionando los metadatos necesarios para que el editor genere marcadores de posición

Si no hay contenido, las etiquetas se proporcionan como marcadores de posición para representar el contenido vacío.

#### Propiedades pasadas dinámicamente {#dynamically-passed-properties}

Los datos procedentes del modelo se pasan dinámicamente como propiedades del componente.

## Exportación de contenido editable {#exporting-editable-content}

Puede exportar un componente y mantenerlo editable.

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

La función `MapTo` devuelve un `Component` resultado de una composición que extiende el `PageClass` proporcionado con los nombres y atributos de clase que habilitan la creación. Este componente se puede exportar para crear posteriormente instancias en el marcado de la aplicación.

Cuando se exporta con las funciones `MapTo` o `withModel`, el componente `Page` se envuelve con un componente `ModelProvider` que proporciona a los componentes estándar acceso a la versión más reciente del modelo de página o a una ubicación precisa en ese modelo de página.

Para obtener más información, consulte el [documento de modelo de SPA](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743).

>[!NOTE]
>
>De forma predeterminada, recibe todo el modelo del componente al utilizar la función `withModel`.

## Compartir información entre componentes SPA {#sharing-information-between-spa-components}

Es necesario que los componentes de una aplicación de una sola página compartan información con regularidad. Existen varias formas recomendadas de hacerlo, enumeradas a continuación en orden creciente de complejidad.

* **Opción 1:** Centralice la lógica y difunda a los componentes necesarios, por ejemplo, mediante Contexto de reacción.
* **Opción 2:** Compartir estados de componentes mediante una biblioteca de estados como Redux.
* **Opción 3:** aproveche la jerarquía de objetos personalizando y ampliando el componente contenedor.

## Próximos pasos {#next-steps}

Para obtener una guía paso a paso sobre cómo crear su propia SPA, consulte el tutorial [Introducción al Editor de AEM SPA - Eventos WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

Para obtener más información sobre cómo organizarse para desarrollar SPA para AEM, consulte el artículo [Desarrollar SPA para AEM](/help/sites-developing/spa-architecture.md).

Para obtener más información sobre la asignación de modelo dinámico a componente y cómo funciona en SPA en AEM, consulte el artículo [Asignación de modelo dinámico a componente para SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Si desea implementar SPA en AEM para un marco que no sea React o Angular o simplemente desea profundizar en el funcionamiento del SDK de SPA para AEM, consulte el artículo [SPA Blueprint](/help/sites-developing/spa-blueprint.md).
