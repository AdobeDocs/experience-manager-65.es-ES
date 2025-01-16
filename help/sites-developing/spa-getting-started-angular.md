---
title: SPA AEM Introducción a la administración de la en Angular
description: SPA SPA Este artículo presenta una aplicación de ejemplo para la creación de informes, explica cómo se crea y le permite ponerse en marcha con su propia aplicación de forma rápida mediante el marco de trabajo de Angular de trabajo de.
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: 9528d92b-0989-4e2d-83be-ba6c07c845e2
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 6d961456e0e1f7a26121da9be493308a62c53e04
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 5%

---


# SPA AEM Introducción a la administración de la en Angular{#getting-started-with-spas-in-aem-angular}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. SPA AEM SPA Los desarrolladores quieren poder crear sitios utilizando marcos de trabajo de y los autores quieren editar contenido sin problemas en para un sitio creado con marcos de trabajo de la.

SPA SPA AEM La función de creación de ofrece una solución completa para la asistencia de la creación de contenido en el ámbito de la. SPA En este artículo se presenta una aplicación de simplificada sobre el marco de trabajo de Angular SPA, y se explica cómo se crea, lo que le permite ponerse en marcha con sus propios rápidamente.

>[!NOTE]
>
>Este artículo se basa en el marco de Angular de. SPA AEM Para ver el documento correspondiente del marco de React, consulte [Introducción a la administración de datos en la - React](/help/sites-developing/spa-getting-started-react.md).

{{ue-over-spa}}

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

SPA El archivo `package.json` define los requisitos del paquete general de. AEM Aquí se enumeran las dependencias mínimas requeridas de la.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

`aem-clientlib-generator` se usa para hacer que la creación de bibliotecas de cliente sea automática como parte del proceso de compilación.

`"aem-clientlib-generator": "^1.4.1",`

Más detalles acerca de [aem-clientlib-generator están disponibles en GitHub](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>La versión mínima de `aem-clientlib-generator` requerida es 1.4.1.

`aem-clientlib-generator` está configurado en el archivo `clientlib.config.js` de la siguiente manera.

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

### Generación {#building}

En realidad, al crear la aplicación se usa [Webpack](https://webpack.js.org/) para la transpilación, además de aem-clientlib-generator para la creación automática de bibliotecas de cliente. Por lo tanto, el comando build será similar a:

`"build": "ng build --build-optimizer=false && clientlib",`

AEM Una vez creado, el paquete se puede cargar en una instancia de.

### Tipo de archivo del proyecto AEM {#aem-project-archetype}

Cualquier proyecto AEM debería utilizar el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es), que admite proyectos de SPA que utilizan React o Angular y aprovecha el SDK de SPA.

## Estructura de aplicación {#application-structure}

SPA AEM Incluir las dependencias y crear la aplicación como se describió anteriormente le dejará con un paquete de trabajo de la aplicación que puede cargar en su instancia de.

SPA AEM La siguiente sección de este documento le explicará cómo se estructura una en la, los archivos importantes que impulsan la aplicación y cómo funcionan juntos.

Como ejemplo se utiliza un componente de imagen simplificado, pero todos los componentes de la aplicación se basan en el mismo concepto.

### app.module.ts {#app-module-ts}

SPA El punto de entrada en la es el archivo `app.module.ts` que se muestra aquí simplificado para centrarse en el contenido importante.

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

El archivo `app.module.ts` es el punto de partida de la aplicación, contiene la configuración inicial del proyecto y usa `AppComponent` para arrancar la aplicación.

#### Instanciación estática {#static-instantiation}

Cuando se crea una instancia del componente de forma estática mediante la plantilla de componente, el valor debe pasarse del modelo a las propiedades del componente. Los valores del modelo se pasan como atributos para que estén disponibles posteriormente como propiedades de componente.

### app.component.ts {#app-component-ts}

Una vez que `app.module.ts` arranca `AppComponent`, puede inicializar la aplicación, que se muestra aquí en una versión simplificada para centrarse en el contenido importante.

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

Al procesar la página, `app.component.ts` llamadas `main-content.component.ts` se muestran aquí en una versión simplificada.

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

`MainComponent` ingiere la representación JSON del modelo de página y procesa el contenido para envolver o decorar cada elemento de la página. SPA Para obtener más información sobre `Page`, consulte el documento [Modelo de la aplicación de código ](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501) de la aplicación de código abierto .

### image.component.ts {#image-component-ts}

`Page` está compuesto por componentes. Con el JSON introducido, `Page` puede procesar esos componentes como `image.component.ts`, como se muestra aquí.

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

SPA AEM SPA AEM La idea central de la en la práctica es la idea de asignar componentes de la a componentes de la y actualizar el componente cuando se modifica el contenido (y a la inversa). SPA Consulte el documento [Información general sobre el editor de](/help/sites-developing/spa-overview.md) para obtener un resumen de este modelo de comunicación.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

SPA AEM El método `MapTo` asigna el componente de la al componente de la. Admite el uso de una sola cadena o matriz de cadenas.

`ImageEditConfig` es un objeto de configuración que contribuye a habilitar las capacidades de creación de un componente al proporcionar los metadatos necesarios para que el editor genere marcadores de posición

Si no hay contenido, las etiquetas se proporcionan como marcadores de posición para representar el contenido vacío.

#### Propiedades pasadas dinámicamente {#dynamically-passed-properties}

Los datos procedentes del modelo se pasan dinámicamente como propiedades del componente.

### image.component.html {#image-component-html}

Finalmente, la imagen se puede procesar en `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## SPA Uso Compartido De Información Entre Componentes De La {#sharing-information-between-spa-components}

Normalmente, es necesario que los componentes de una aplicación de una sola página compartan información. Existen varias formas recomendadas de hacerlo, enumeradas de la siguiente manera en orden creciente de complejidad.

* **Opción 1:** Centralice la lógica y difunda a los componentes necesarios, por ejemplo, utilizando una clase util como solución pura orientada a objetos.
* **Opción 2:** Compartir estados de componentes mediante una biblioteca de estado como NgRx.
* **Opción 3:** Aproveche la jerarquía de objetos personalizando y extendiendo el componente contenedor.

## Siguientes pasos {#next-steps}

SPA AEM SPA Para obtener una guía paso a paso sobre cómo crear sus propios, consulte el [Tutorial de introducción al Editor de eventos de WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=es) de la página de inicio de la página de inicio de la página de inicio de la página de inicio de la aplicación Editor de eventos de WKND.

SPA AEM SPA AEM Para obtener más información acerca de cómo organizarse para desarrollar la para la distribución de recursos, vea el artículo [Desarrollo de la distribución de recursos para el desarrollo de recursos para el desarrollo de recursos para el desarrollo de recursos para la distribución de recursos](/help/sites-developing/spa-architecture.md).

SPA AEM SPA Para obtener más información acerca de la asignación de modelos dinámicos a componentes y cómo funciona dentro de la asignación de componentes en el modelo dinámico, vea el artículo [Asignación de modelos dinámicos a componentes para la asignación de componentes para el modelo dinámico para la asignación de componentes para el modelo dinámico para la asignación de componentes para la asignación de componentes para el modelo dinámico para la asignación de componentes para la asignación de componentes para la asignación de componentes para la asignación de componentes para la asignación de componentes para el modelo dinámico para la asignación de componentes para la asignación de componentes10000000000000000001010000000000000000000000000000000000000000010000000000000000000000000000000](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)

Si desea implementar la implementación de la en un Angular SPA de trabajo que no sea React o SPA AEM, o simplemente desea profundizar en cómo funciona el modelo de trabajo de SDK AEM SPA para la, consulte el artículo de [Modelo de trabajo](/help/sites-developing/spa-blueprint.md).
