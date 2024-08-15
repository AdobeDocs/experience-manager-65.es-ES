---
title: SPA AEM Introducción a la administración de la en React
description: SPA SPA Este artículo presenta una aplicación de ejemplo para la creación de informes, explica cómo se crea y le permite ponerse en marcha con su propia aplicación de forma rápida mediante el marco de trabajo React.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: 552649e7-6054-4ae8-b570-5ba7230e6f19
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 4%

---

# SPA AEM Introducción a la administración de la en React{#getting-started-with-spas-in-aem-react}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. SPA AEM SPA Los desarrolladores quieren poder crear sitios utilizando marcos de trabajo de y los autores quieren editar contenido sin problemas en para un sitio creado con marcos de trabajo de la.

SPA SPA AEM La función de creación de ofrece una solución completa para la asistencia de la creación de contenido en el ámbito de la. SPA SPA En este artículo se presenta una aplicación de simplificada sobre el marco de trabajo de React, que explica cómo se crea, lo que le permite ponerse en marcha con su propia aplicación de forma rápida y sencilla, con la que puede trabajar con sus propios recursos de forma más rápida y eficaz.

>[!NOTE]
>
>Este artículo se basa en el marco de React. Para el documento correspondiente para la estructura de Angular SPA AEM, consulte [Introducción a la creación de cuadros de trabajo en la - Angular](/help/sites-developing/spa-getting-started-angular.md).

>[!NOTE]
>
>SPA SPA El Editor de segmentos es la solución recomendada para los proyectos que requieren un procesamiento basado en el cliente basado en el marco de trabajo de la aplicación (por ejemplo, React o Angular) de la aplicación de la aplicación de la manera más sencilla posible.

## Introducción {#introduction}

SPA Este artículo resume el funcionamiento básico de un sencillo y el mínimo que necesita saber para poner en marcha el suyo.

SPA AEM Para obtener más información sobre cómo funcionan los en la, consulte los siguientes documentos:

* [Introducción y tutorial de SPA](/help/sites-developing/spa-walkthrough.md)
* [SPA Introducción a la creación de](/help/sites-developing/spa-overview.md)
* [Modelo SPA](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>SPA AEM Para poder crear contenido dentro de un elemento de contenido, el contenido debe almacenarse en el elemento de contenido y ser expuesto por el modelo de contenido de, lo que hace que el contenido se almacene en el elemento de contenido.
>
>SPA AEM Una desarrollada fuera de la no será legible si no respeta el contrato del modelo de contenido.

SPA SPA Este documento recorrerá la estructura de un documento simplificado creado con el marco de trabajo de React e ilustrará cómo funciona para que pueda aplicar esta comprensión a su propia.

## Dependencias, configuración y generación {#dependencies-configuration-and-building}

SPA SPA Además de la dependencia de React esperada, el ejemplo puede utilizar bibliotecas adicionales para que la creación de la biblioteca de React sea más eficiente. En este ejemplo, se puede usar una biblioteca adicional para hacer que la creación de la biblioteca de React sea más eficiente.

### Dependencias {#dependencies}

SPA El archivo `package.json` define los requisitos del paquete general de. AEM SPA Las dependencias mínimas de la para un grupo de trabajo se enumeran aquí.

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

`aem-clientlib-generator` se usa para hacer que la creación de bibliotecas de cliente sea automática como parte del proceso de compilación.

`"aem-clientlib-generator": "^1.4.1",`

Encontrará más detalles sobre [aem-clientlib-generator en GitHub](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>La versión mínima de `aem-clientlib-generator` requerida es 1.4.1.

`aem-clientlib-generator` está configurado en el archivo `clientlib.config.js` de la siguiente manera.

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

### Generación {#building}

En realidad, al crear la aplicación se usa [Webpack](https://webpack.js.org/) para la transpilación, además de aem-clientlib-generator para la creación automática de bibliotecas de cliente. Por lo tanto, el comando build será similar a:

`"build": "webpack && clientlib --verbose"`

AEM Una vez creado, el paquete se puede cargar en una instancia de.

### Tipo de archivo del proyecto AEM {#aem-project-archetype}

Cualquier proyecto AEM debería utilizar el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es), que admite proyectos de SPA que utilizan React o Angular y aprovecha el SDK de SPA.

## Estructura de aplicación {#application-structure}

SPA AEM Incluir las dependencias y crear la aplicación como se describió anteriormente le dejará con un paquete de trabajo de la aplicación que puede cargar en su instancia de.

SPA AEM En la siguiente sección de este documento se explica cómo se estructura una en el trabajo, los archivos importantes que dirigen la aplicación y cómo funcionan juntos.

Como ejemplo se utiliza un componente de imagen simplificado, pero todos los componentes de la aplicación se basan en el mismo concepto.

### index.js {#index-js}

SPA El punto de entrada en la es el archivo `index.js` que se muestra aquí simplificado para centrarse en el contenido importante.

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

La función principal de `index.js` es utilizar la función `ReactDOM.render` para determinar en qué parte del DOM insertar la aplicación.

Este es un uso estándar de esta función, no exclusivo de esta aplicación de ejemplo.

#### Instanciación estática {#static-instantiation}

Cuando se crea una instancia del componente de forma estática mediante la plantilla del componente (por ejemplo, JSX), el valor debe pasarse del modelo a las propiedades del componente.

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

`App.js` sirve principalmente para envolver los componentes raíz que componen la aplicación. El punto de entrada de cualquier aplicación es la página.

### Page.js {#page-js}

Al procesar la página, `App.js` llamadas `Page.js` se muestran aquí en una versión simplificada.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

En este ejemplo, la clase `AppPage` amplía `Page`, que contiene los métodos de contenido interno que se pueden utilizar posteriormente.

`Page` ingiere la representación JSON del modelo de página y procesa el contenido para envolver o decorar cada elemento de la página. SPA Para obtener más información sobre `Page`, consulte el documento [Modelo de la aplicación de código ](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501) de la aplicación de código abierto .

### Image.js {#image-js}

Con la página representada, se pueden procesar los componentes como `Image.js` que se muestran aquí.

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

SPA AEM SPA AEM La idea central de la en la práctica es la idea de asignar componentes de la a componentes de la y actualizar el componente cuando se modifica el contenido (y a la inversa). SPA Consulte el documento [Información general sobre el editor de](/help/sites-developing/spa-overview.md) para obtener un resumen de este modelo de comunicación.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

SPA AEM El método `MapTo` asigna el componente de la al componente de la. Admite el uso de una sola cadena o matriz de cadenas.

`ImageEditConfig` es un objeto de configuración que contribuye a habilitar las capacidades de creación de un componente al proporcionar los metadatos necesarios para que el editor genere marcadores de posición

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

La función `MapTo` devuelve un `Component` que es el resultado de una composición que extiende el `PageClass` proporcionado con los nombres de clase y atributos que habilitan la creación. Este componente se puede exportar para que se cree una instancia más adelante en el marcado de la aplicación.

Cuando se exporta mediante las funciones `MapTo` o `withModel`, el componente `Page` se ajusta con un componente `ModelProvider` que proporciona acceso a los componentes estándar a la última versión del modelo de página o a una ubicación precisa en ese modelo de página.

SPA Para obtener más información, consulte el [documento de modelo de datos](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743).

>[!NOTE]
>
>De forma predeterminada, recibe todo el modelo del componente al utilizar la función `withModel`.

## SPA Uso Compartido De Información Entre Componentes De La {#sharing-information-between-spa-components}

Normalmente, es necesario que los componentes de una aplicación de una sola página compartan información. Existen varias formas recomendadas de hacerlo, enumeradas de la siguiente manera en orden creciente de complejidad.

* **Opción 1:** Centralice la lógica y difunda a los componentes necesarios, por ejemplo, mediante React Context.
* **Opción 2:** Compartir estados de componentes mediante una biblioteca de estados como Redux.
* **Opción 3:** Aproveche la jerarquía de objetos personalizando y extendiendo el componente contenedor.

## Siguientes pasos {#next-steps}

SPA AEM SPA Para obtener una guía paso a paso sobre cómo crear sus propios, consulte el [Tutorial de introducción al Editor de eventos de WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=es) de la página de inicio de la página de inicio de la página de inicio de la página de inicio de la aplicación Editor de eventos de WKND.

SPA AEM SPA AEM Para obtener más información acerca de cómo organizarse para desarrollar la para la distribución de recursos, vea el artículo [Desarrollo de la distribución de recursos para el desarrollo de recursos para el desarrollo de recursos para el desarrollo de recursos para la distribución de recursos](/help/sites-developing/spa-architecture.md).

SPA AEM SPA Para obtener más información acerca de la asignación de modelos dinámicos a componentes y cómo funciona dentro de la asignación de componentes en el modelo dinámico, vea el artículo [Asignación de modelos dinámicos a componentes para la asignación de componentes para el modelo dinámico para la asignación de componentes para el modelo dinámico para la asignación de componentes para la asignación de componentes para el modelo dinámico para la asignación de componentes para la asignación de componentes para la asignación de componentes para la asignación de componentes para la asignación de componentes para el modelo dinámico para la asignación de componentes para la asignación de componentes10000000000000000001010000000000000000000000000000000000000000010000000000000000000000000000000](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)

SPA AEM Si desea implementar un esquema de trabajo en el que no sea React o Angular SPA AEM SPA, o simplemente desea profundizar en cómo funciona el SDK de la para el trabajo de los usuarios, consulte el artículo de [Modelo de trabajo](/help/sites-developing/spa-blueprint.md) para el usuario de .
