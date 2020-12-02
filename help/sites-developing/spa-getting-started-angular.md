---
title: 'Introducción a SPA en AEM: Angular'
seo-title: 'Introducción a SPA en AEM: Angular'
description: Este artículo presenta una aplicación de SPA de muestra, explica cómo se organiza y le permite ponerse en marcha con sus propios SPA rápidamente usando el marco Angular.
seo-description: Este artículo presenta una aplicación de SPA de muestra, explica cómo se organiza y le permite ponerse en marcha con sus propios SPA rápidamente usando el marco Angular.
uuid: d3d2fa63-68c8-4a48-8c8d-045f4f8db937
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9cdd7648-d67e-414d-aedf-a5687da39326
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 1%

---


# Introducción a SPA en AEM - Angular{#getting-started-with-spas-in-aem-angular}

Las aplicaciones de una sola página (SPA) pueden oferta de experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios con marcos de SPA y los autores quieren editar contenido dentro de AEM sin problemas para un sitio creado con marcos de SPA.

La función de creación de SPA oferta una solución completa para admitir SPA dentro de AEM. Este artículo presenta una aplicación de SPA simplificada en el marco Angular, explica cómo se ha creado, permitiéndole ponerse en marcha con su propia SPA rápidamente.

>[!NOTE]
>
>Este artículo se basa en el marco angular. Para consultar el documento correspondiente del esquema de React, consulte [Introducción a SPA en AEM - Reacción](/help/sites-developing/spa-getting-started-react.md).

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

Este documento recorrerá la estructura de un SPA simplificado e ilustrará cómo funciona para que pueda aplicar este entendimiento a sus propios SPA.

## Dependencias, configuración y generación {#dependencies-configuration-and-building}

Además de la dependencia Angular esperada, el SPA de muestra puede aprovechar bibliotecas adicionales para hacer que la creación del SPA sea más eficiente.

### Dependencias {#dependencies}

El archivo `package.json` define los requisitos del paquete de SPA general. Aquí se enumeran las dependencias de AEM mínimas requeridas.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
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
    clientLibRoot: "./../content/jcr_root/apps/my-angular-app/clientlibs",

    libs: {
        name: "my-angular-app",
        allowProxy: true,
        categories: ["my-angular-app"],
        embed: ["my-angular-app.responsivegrid"],
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

`"build": "ng build --build-optimizer=false && clientlib",`

Una vez creado, el paquete se puede cargar en una instancia de AEM.

### Tipo de archivo del proyecto AEM {#aem-project-archetype}

Cualquier proyecto AEM debe aprovechar el [AEM Arquetipo de proyecto](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype/overview.html), que admite SPA proyectos usando React o Angular y aprovecha el SDK SPA.

## Estructura de la aplicación {#application-structure}

Si se incluyen las dependencias y se crea la aplicación tal como se ha descrito anteriormente, dispondrá de un paquete de SPA que podrá cargar en la instancia de AEM.

La siguiente sección de este documento le explicará cómo se estructura un SPA en AEM, los archivos importantes que dirigen la aplicación y cómo funcionan juntos.

Un componente de imagen simplificado se utiliza como ejemplo, pero todos los componentes de la aplicación se basan en el mismo concepto.

### app.module.ts {#app-module-ts}

El punto de entrada en el SPA es el archivo `app.module.ts` mostrado aquí simplificado para centrarse en el contenido importante.

```
// app.module.ts
import { BrowserModule, BrowserTransferStateModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { SpaAngularEditableComponentsModule } from '@adobe/aem-angular-editable-components';
import { AppRoutingModule } from './app-routing.module';

@NgModule({
  imports: [ BrowserModule.withServerTransition({ appId: 'my-angular-app' }),
    SpaAngularEditableComponentsModule,
    AppRoutingModule,
    BrowserTransferStateModule ],
  providers: ...,
  declarations: [ ... ],
  entryComponents: [ ... ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

El archivo `app.module.ts` es el punto de partida de la aplicación y contiene la configuración inicial del proyecto y utiliza `AppComponent` para arrancar la aplicación.

#### Creación de instancias estáticas {#static-instantiation}

Cuando se crea una instancia del componente mediante una plantilla de componente, el valor debe pasarse del modelo a las propiedades del componente. Los valores del modelo se pasan como atributos para luego estar disponibles como propiedades de componente.

### app.component.ts {#app-component-ts}

Una vez `app.module.ts` bootstraps `AppComponent`, puede luego inicializar la aplicación, que se muestra aquí en una versión simplificada para centrarse en el contenido importante.

```
// app.component.ts
import { Component } from '@angular/core';
import { ModelManager } from '@adobe/aem-spa-page-model-manager';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-root',
  template: `
    <router-outlet></router-outlet>
  `
})

export class AppComponent {
  items;
  itemsOrder;
  path;

  constructor() {
    ModelManager.initialize().then(this.updateData.bind(this));
  }

  private updateData(model) {
    this.path = model[Constants.PATH_PROP];
    this.items = model[Constants.ITEMS_PROP];
    this.itemsOrder = model[Constants.ITEMS_ORDER_PROP];
  }
}
```

### main-content.component.ts {#main-content-component-ts}

Al procesar la página, `app.component.ts` llama a `main-content.component.ts` en una versión simplificada.

```
import { Component } from '@angular/core';
import { ModelManagerService }     from '../model-manager.service';
import { ActivatedRoute } from '@angular/router';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-main',
  template: `
    <aem-page class="structure-page" [attr.data-cq-page-path]="path" [cqPath]="path" [cqItems]="items" [cqItemsOrder]="itemsOrder" ></aem-page>
  `
})

export class MainContentComponent {
  items;
  itemsOrder;
  path;

  constructor( private route: ActivatedRoute,
    private modelManagerService: ModelManagerService) {
    this.modelManagerService.getData({ path: this.route.snapshot.data.path }).then((data) => {
      this.path = data[Constants.PATH_PROP];
      this.items = data[Constants.ITEMS_PROP];
      this.itemsOrder = data[Constants.ITEMS_ORDER_PROP];
    });
  }
}
```

El `MainComponent` ingesta la representación JSON del modelo de página y procesa el contenido para ajustar/decorar cada elemento de la página. Puede encontrar más detalles sobre el `Page` en el documento [Modelo de SPA](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### image.component.ts {#image-component-ts}

El `Page` está compuesto por componentes. Con el JSON ingerido, el `Page` puede procesar los componentes como `image.component.ts` como se muestra aquí.

```
/// image.component.ts
import { Component, Input } from '@angular/core';

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function(cqModel) {
        return !cqModel || !cqModel.src || cqModel.src.trim().length < 1;
    }
};

@Component({
  selector: 'app-image',
  templateUrl: './image.component.html',
})

export class ImageComponent {
  @Input() src: string;
  @Input() alt: string;
  @Input() title: string;
}

MapTo('my-angular-app/components/image')(ImageComponent, ImageEditConfig);
```

La idea central de SPA en AEM es la idea de asignar SPA componentes a AEM componentes y actualizar el componente cuando se modifica el contenido (y viceversa). Consulte el documento [Información general del editor de SPA](/help/sites-developing/spa-overview.md) para obtener un resumen de este modelo de comunicación.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

El método `MapTo` asigna el componente de SPA al componente de AEM. Admite el uso de una sola cadena o una matriz de cadenas.

`ImageEditConfig` es un objeto de configuración que contribuye a habilitar las capacidades de creación de un componente proporcionando los metadatos necesarios para que el editor genere marcadores de posición

Si no hay contenido, las etiquetas se proporcionan como marcadores de posición para representar el contenido vacío.

#### Propiedades pasadas dinámicamente {#dynamically-passed-properties}

Los datos procedentes del modelo se pasan dinámicamente como propiedades del componente.

### image.component.html {#image-component-html}

Finalmente, la imagen se puede procesar en `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## Compartir información entre componentes SPA {#sharing-information-between-spa-components}

Es necesario que los componentes de una aplicación de una sola página compartan información con regularidad. Existen varias formas recomendadas de hacerlo, enumeradas a continuación en orden creciente de complejidad.

* **Opción 1:** Centralice la lógica y difunda a los componentes necesarios, por ejemplo, utilizando una clase util como solución pura orientada a objetos.
* **Opción 2:** Compartir estados de componentes mediante una biblioteca de estados como NgRx.
* **Opción 3:** aproveche la jerarquía de objetos personalizando y ampliando el componente contenedor.

## Próximos pasos {#next-steps}

Para obtener una guía paso a paso sobre cómo crear su propia SPA, consulte el tutorial [Introducción al Editor de AEM SPA - Eventos WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

Para obtener más información sobre cómo organizarse para desarrollar SPA para AEM, consulte el artículo [Desarrollar SPA para AEM](/help/sites-developing/spa-architecture.md).

Para obtener más información sobre la asignación de modelo dinámico a componente y cómo funciona en SPA en AEM, consulte el artículo [Asignación de modelo dinámico a componente para SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Si desea implementar SPA en AEM para un marco que no sea React o Angular o simplemente desea profundizar en el funcionamiento del SDK de SPA para AEM, consulte el artículo [SPA Blueprint](/help/sites-developing/spa-blueprint.md).
