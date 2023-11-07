---
title: SPA AEM Introducción a la administración de la en Angular
seo-title: Getting Started with SPAs in AEM - Angular
description: SPA SPA Este artículo presenta una aplicación de ejemplo para la creación de informes, explica cómo se crea y le permite ponerse en marcha con su propia aplicación de forma rápida mediante el marco de trabajo de Angular de trabajo de.
seo-description: This article presents a sample SPA application, explains how it is put together, and lets you get up-and-running with your own SPA quickly using the Angular framework.
uuid: d3d2fa63-68c8-4a48-8c8d-045f4f8db937
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9cdd7648-d67e-414d-aedf-a5687da39326
docset: aem65
exl-id: 9528d92b-0989-4e2d-83be-ba6c07c845e2
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 6%

---

# SPA AEM Introducción a la administración de la en Angular{#getting-started-with-spas-in-aem-angular}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. SPA AEM SPA Los desarrolladores quieren poder crear sitios utilizando marcos de trabajo de y los autores quieren editar contenido sin problemas en para un sitio creado con marcos de trabajo de la.

SPA SPA AEM La función de creación de ofrece una solución completa para la asistencia de la creación de contenido en el ámbito de la. SPA En este artículo se presenta una aplicación de simplificada sobre el marco de trabajo de Angular SPA, y se explica cómo se crea, lo que le permite ponerse en marcha con sus propios rápidamente.

>[!NOTE]
>
>Este artículo se basa en el marco de Angular de. Para ver el documento correspondiente al marco de React, consulte [SPA AEM Introducción a la administración de la en React](/help/sites-developing/spa-getting-started-react.md).

>[!NOTE]
>
>SPA SPA El Editor de es la solución recomendada para proyectos que requieren un procesamiento basado en el marco de trabajo del lado del cliente (por ejemplo, React o Angular).

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

SPA SPA Este documento recorrerá la estructura de un documento simplificado e ilustrará cómo funciona para que pueda aplicar esta comprensión a su propio.

## Dependencias, configuración y generación {#dependencies-configuration-and-building}

Además de la dependencia de Angular SPA SPA esperada, el ejemplo puede utilizar bibliotecas adicionales para que la creación de los recursos de ejemplo sea más eficiente. En este ejemplo, se puede usar una biblioteca de bibliotecas adicionales para hacer que la creación de los recursos sea más eficiente

### Dependencias {#dependencies}

El `package.json` SPA define los requisitos del paquete de trabajo global de la. AEM Aquí se enumeran las dependencias mínimas requeridas de la.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

El `aem-clientlib-generator` se utiliza para hacer que la creación de bibliotecas de cliente sea automática como parte del proceso de compilación.

`"aem-clientlib-generator": "^1.4.1",`

Se pueden encontrar más detalles al respecto [en GitHub aquí](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>La versión mínima del `aem-clientlib-generator` obligatorio es 1.4.1.

El `aem-clientlib-generator` está configurado en la `clientlib.config.js` como se indica a continuación.

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

La creación de la aplicación utiliza [Webpack](https://webpack.js.org/) para la transpilación, además de aem-clientlib-generator para la creación automática de bibliotecas de cliente. Por lo tanto, el comando build será similar a:

`"build": "ng build --build-optimizer=false && clientlib",`

AEM Una vez creado, el paquete se puede cargar en una instancia de.

### Tipo de archivo del proyecto AEM. {#aem-project-archetype}

Cualquier proyecto AEM debería utilizar el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es), que admite proyectos de SPA que utilizan React o Angular y aprovecha el SDK de SPA.

## Estructura de aplicación {#application-structure}

SPA AEM Incluir las dependencias y crear la aplicación como se describió anteriormente le dejará con un paquete de trabajo de la aplicación que puede cargar en su instancia de.

SPA AEM La siguiente sección de este documento le explicará cómo se estructura una en la, los archivos importantes que impulsan la aplicación y cómo funcionan juntos.

Como ejemplo se utiliza un componente de imagen simplificado, pero todos los componentes de la aplicación se basan en el mismo concepto.

### app.module.ts {#app-module-ts}

SPA El punto de entrada en la es el `app.module.ts` archivo que se muestra aquí simplificado para centrarse en el contenido importante.

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

El `app.module.ts` es el punto de partida de la aplicación y contiene la configuración inicial del proyecto y utiliza `AppComponent` para arrancar la aplicación.

#### Instanciación estática {#static-instantiation}

Cuando se crea una instancia del componente de forma estática mediante la plantilla de componente, el valor debe pasarse del modelo a las propiedades del componente. Los valores del modelo se pasan como atributos para que estén disponibles posteriormente como propiedades de componente.

### app.component.ts {#app-component-ts}

Una `app.module.ts` correas `AppComponent`A continuación, puede inicializar la aplicación, que se muestra aquí en una versión simplificada para centrarse en el contenido importante.

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

Al procesar la página, `app.component.ts` llamadas `main-content.component.ts` enumerados aquí en una versión simplificada.

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

El `MainComponent` ingiere la representación JSON del modelo de página y procesa el contenido para envolver o decorar cada elemento de la página. Más información sobre la `Page` se puede encontrar en el documento [SPA Modelo de](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### image.component.ts {#image-component-ts}

El `Page` está compuesto por componentes. Con el JSON introducido, la variable `Page` puede procesar estos componentes, como `image.component.ts` como se muestra aquí.

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

SPA AEM SPA AEM La idea central de la en la práctica es la idea de asignar componentes de la a componentes de la y actualizar el componente cuando se modifica el contenido (y a la inversa). Ver el documento [SPA Resumen del editor de](/help/sites-developing/spa-overview.md) para obtener un resumen de este modelo de comunicación.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

El `MapTo` SPA AEM El método asigna el componente de la al componente de la. Admite el uso de una sola cadena o matriz de cadenas.

`ImageEditConfig` es un objeto de configuración que contribuye a habilitar las capacidades de creación de un componente al proporcionar los metadatos necesarios para que el editor genere marcadores de posición

Si no hay contenido, las etiquetas se proporcionan como marcadores de posición para representar el contenido vacío.

#### Propiedades pasadas dinámicamente {#dynamically-passed-properties}

Los datos procedentes del modelo se pasan dinámicamente como propiedades del componente.

### image.component.html {#image-component-html}

Finalmente, la imagen se puede representar en `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## SPA Uso Compartido De Información Entre Componentes De La {#sharing-information-between-spa-components}

Normalmente, es necesario que los componentes de una aplicación de una sola página compartan información. Existen varias formas recomendadas de hacerlo, enumeradas de la siguiente manera en orden creciente de complejidad.

* **Opción 1:** Centralice la lógica y difunda a los componentes necesarios, por ejemplo, utilizando una clase util como solución pura orientada a objetos.
* **Opción 2:** Compartir estados de componentes mediante una biblioteca de estados como NgRx.
* **Opción 3:** Aproveche la jerarquía de objetos personalizando y ampliando el componente contenedor.

## Pasos siguientes {#next-steps}

SPA Para obtener una guía paso a paso sobre cómo crear sus propios, consulte la [AEM SPA Introducción al Editor de eventos de: Tutorial de eventos de WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=es).

SPA AEM Para obtener más información acerca de cómo organizarse para desarrollar la para obtener más información, consulte el artículo [SPA AEM Desarrollo de la](/help/sites-developing/spa-architecture.md).

SPA AEM Para obtener más información acerca de la asignación de modelos dinámicos a componentes y cómo funciona dentro de la asignación de componentes dentro de la en la aplicación, consulte el artículo [SPA Asignación de modelos dinámicos a componentes para la creación de](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

SPA AEM Si desea implementar un esquema de trabajo en el que se incluya un módulo de trabajo que no sea React o Angular SPA AEM, o simplemente desea profundizar en cómo funciona el SDK de la para la creación de informes, consulte el documento de trabajo de la aplicación de diseño de informes (en inglés) que contiene información detallada sobre cómo funciona el SDK para la creación de informes de. [SPA Modelo de](/help/sites-developing/spa-blueprint.md) artículo.
