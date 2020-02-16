---
title: 'Introducción a los SPA en AEM: reaccionar'
seo-title: 'Introducción a los SPA en AEM: reaccionar'
description: Este artículo presenta una aplicación SPA de muestra, explica cómo se ha creado y le permite ponerse en marcha rápidamente con su propio SPA utilizando el marco de React.
seo-description: Este artículo presenta una aplicación SPA de muestra, explica cómo se ha creado y le permite ponerse en marcha rápidamente con su propio SPA utilizando el marco de React.
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# Introducción a los SPA en AEM: reaccionar{#getting-started-with-spas-in-aem-react}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios del sitio web. Los desarrolladores quieren poder crear sitios con marcos de SPA y los autores quieren editar contenido sin problemas dentro de AEM para un sitio creado con marcos de SPA.

La función de creación de SPA ofrece una solución completa para admitir SPA en AEM. Este artículo presenta una aplicación SPA simplificada en el marco de React, explica cómo se ha creado, permitiéndole ponerse en marcha rápidamente con su propio SPA.

>[!NOTE]
>
>Este artículo se basa en el marco de React. Para consultar el documento correspondiente del marco angular, consulte [Introducción a SPA en AEM - Angular](/help/sites-developing/spa-getting-started-angular.md).

>[!NOTE]
>
>El Editor de SPA es la solución recomendada para proyectos que requieren procesamiento del cliente basado en el marco de SPA (por ejemplo, React o Angular).

## Introducción {#introduction}

Este artículo resume el funcionamiento básico de un SPA simple y el mínimo que necesita saber para que el suyo funcione.

Para obtener más información sobre cómo funcionan los SPA en AEM, consulte los siguientes documentos:

* [Introducción y tutoriales de SPA](/help/sites-developing/spa-walkthrough.md)
* [Introducción a la creación de SPA](/help/sites-developing/spa-overview.md)
* [Modelo SPA](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>Para poder crear contenido dentro de una SPA, el contenido debe almacenarse en AEM y quedar expuesto por el modelo de contenido.
>
>Una SPA desarrollada fuera de AEM no será autorizada si no respeta el contrato del modelo de contenido.

Este documento recorrerá la estructura de un SPA simplificado creado con el marco React e ilustrará cómo funciona para que pueda aplicar este entendimiento a su propio SPA.

## Dependencias, configuración y creación {#dependencies-configuration-and-building}

Además de la dependencia esperada de React, el SPA de muestra puede aprovechar bibliotecas adicionales para hacer que la creación del SPA sea más eficiente.

### Dependencias {#dependencies}

El `package.json` archivo define los requisitos del paquete completo de SPA. Aquí se enumeran las dependencias mínimas de AEM para un SPA en funcionamiento.

```
  "dependencies": {
    "@adobe/cq-react-editable-components": "~1.0.3",
    "@adobe/cq-spa-component-mapping": "~1.0.3",
    "@adobe/cq-spa-page-model-manager": "~1.0.4"
  }
```

Dado que este ejemplo se basa en el marco de React, hay dos dependencias específicas de React que son obligatorias en el `package.json` archivo:

```
react
 react-dom
```

El `aem-clientlib-generator` se aprovecha para hacer que la creación de bibliotecas de cliente sea automática como parte del proceso de compilación.

`"aem-clientlib-generator": "^1.4.1",`

Puede encontrar más detalles [en GitHub aquí](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>La versión mínima del `aem-clientlib-generator` requerido es 1.4.1.

El `aem-clientlib-generator` se configura en el `clientlib.config.js` archivo como se indica a continuación.

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

### Kit de arranque de Maven Archetype para SPA {#maven-archetype-for-spa-starter-kit}

Adobe recomienda aprovechar el [Arquetipo de Maven para SPA Starter Kit](https://github.com/adobe/aem-spa-project-archetype) para ayudarle a iniciar su propio proyecto de SPA para AEM.

## Estructura de la aplicación {#application-structure}

La inclusión de las dependencias y la creación de la aplicación, tal como se ha descrito anteriormente, le dejarán un paquete SPA que ya está en funcionamiento y que podrá cargar en su instancia de AEM.

La siguiente sección de este documento le explicará cómo se estructura un SPA en AEM, los archivos importantes que dirigen la aplicación y cómo funcionan juntos.

Un componente de imagen simplificado se utiliza como ejemplo, pero todos los componentes de la aplicación se basan en el mismo concepto.

### index.js {#index-js}

El punto de entrada en la SPA es, por supuesto, el archivo mostrado aquí se simplifica para centrarse en el contenido importante. `index.js`

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/cq-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

La función principal de `index.js` es aprovechar la `ReactDOM.render` función para determinar en qué parte del DOM se inyecta la aplicación.

Se trata de un uso estándar de esta función, no exclusivo de esta aplicación de ejemplo.

#### Creación de instancias estáticas {#static-instantiation}

Cuando se crea una instancia del componente mediante una plantilla de componente (por ejemplo, JSX), el valor debe pasarse del modelo a las propiedades del componente.

### App.js {#app-js}

Al procesar la aplicación, realiza llamadas `index.js` `App.js`, que se muestran aquí en una versión simplificada para centrarse en el contenido importante.

```
import {Page, withModel } from '@adobe/cq-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` sirve principalmente para ajustar los componentes raíz que componen la aplicación. El punto de entrada de cualquier aplicación es la página.

### Page.js {#page-js}

Al procesar la página, las llamadas `App.js` `Page.js` se enumeran aquí en una versión simplificada.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/cq-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

En este ejemplo, la `AppPage` clase se extiende `Page`, que contiene los métodos de contenido interno que se pueden utilizar.

La `Page` ingesta la representación JSON del modelo de página y procesa el contenido para ajustar/decorar cada elemento de la página. Para más información sobre el `Page` tema, véase el documento [SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### Image.js {#image-js}

Con la página representada, se pueden procesar los componentes como `Image.js` el que se muestra aquí.

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/cq-react-editable-components';

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

La idea central de las SPA en AEM es la idea de asignar componentes de SPA a componentes de AEM y actualizar el componente cuando se modifica el contenido (y viceversa). Consulte el documento Información general [del editor de](/help/sites-developing/spa-overview.md) SPA para obtener un resumen de este modelo de comunicación.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

El `MapTo` método asigna el componente SPA al componente AEM. Admite el uso de una sola cadena o una matriz de cadenas.

`ImageEditConfig` es un objeto de configuración que contribuye a habilitar las capacidades de creación de un componente proporcionando los metadatos necesarios para que el editor genere marcadores de posición

Si no hay contenido, las etiquetas se proporcionan como marcadores de posición para representar el contenido vacío.

#### Propiedades pasadas dinámicamente {#dynamically-passed-properties}

Los datos procedentes del modelo se pasan dinámicamente como propiedades del componente.

## Exportación de contenido editable {#exporting-editable-content}

Puede exportar un componente y mantenerlo editable.

```
import React, { Component } from 'react';
import { MapTo } from '@cq/cq-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

La `MapTo` función devuelve un `Component` resultado de una composición que amplía los nombres y atributos de clase proporcionados `PageClass` con los que se habilita la creación. Este componente se puede exportar para crear posteriormente instancias en el marcado de la aplicación.

Cuando se exporta con las `MapTo` funciones o `withModel` , el `Page` componente se envuelve con un `ModelProvider` componente que proporciona a los componentes estándar acceso a la versión más reciente del modelo de página o a una ubicación precisa en ese modelo de página.

Para obtener más información, consulte el documento [Modelo de SPA](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743).

>[!NOTE]
>
>De forma predeterminada, recibe todo el modelo del componente cuando utiliza la `withModel` función.

## Uso compartido de información entre componentes de SPA {#sharing-information-between-spa-components}

Es necesario que los componentes de una aplicación de una sola página compartan información con regularidad. Existen varias formas recomendadas de hacerlo, enumeradas a continuación en orden creciente de complejidad.

* **** Opción 1: Centralice la lógica y difunda a los componentes necesarios, por ejemplo, mediante React Context.
* **** Opción 2: Compartir estados de componentes mediante una biblioteca de estados como Redux.
* **** Opción 3: Aproveche la jerarquía de objetos personalizando y ampliando el componente contenedor.

## Próximos pasos {#next-steps}

Para obtener una guía paso a paso sobre la creación de su propio SPA, consulte el tutorial [](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)Introducción al Editor de AEM SPA - Eventos WKND.

Para obtener más información sobre cómo organizarse para desarrollar SPA para AEM, consulte el artículo [Desarrollo de SPA para AEM](/help/sites-developing/spa-architecture.md).

Para obtener más información sobre la asignación de modelos dinámicos a componentes y cómo funciona en SPA en AEM, consulte el artículo Asignación de modelos [dinámicos a componentes para SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Si desea implementar SPA en AEM para un entorno distinto de React o Angular o simplemente desea profundizar en el funcionamiento del SDK de SPA para AEM, consulte el artículo [SPA Blueprint](/help/sites-developing/spa-blueprint.md) .
