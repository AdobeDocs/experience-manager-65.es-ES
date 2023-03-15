---
title: Aplicaciones de una sola página
seo-title: Single Page Applications
description: Siga esta página para obtener más información sobre las aplicaciones de una sola página; es decir, puede crear una aplicación que funcione de forma idéntica a una aplicación de escritorio o móvil.
seo-description: Follow this page to learn about single page applications, that is, you can create an application that performs identically to a desktop or mobile application.
uuid: d1865e79-6e7c-4149-95c0-556e61478b01
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: a5b5e40e-2457-45fe-9632-baf5008fe8bf
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 1%

---

# Aplicaciones de una sola página{#single-page-applications}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran procesamiento del lado del cliente basado en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

[Aplicaciones de una sola página](https://en.wikipedia.org/wiki/Single-page_application) SPA () han alcanzado una masa crítica, ampliamente considerada como el patrón más efectivo para construir experiencias sin fisuras con la tecnología web. SPA Al seguir un patrón de, puede crear una aplicación que funcione de forma idéntica a una aplicación de escritorio o móvil, pero que alcance una multitud de plataformas de dispositivo y factores de formulario debido a su base en los estándares web abiertos.

SPA En términos generales, los sitios web basados en páginas suelen tener un rendimiento mayor que los tradicionales, ya que suelen cargar una página completa del HTML **solo una vez** (incluido CSS, JS y contenido de fuentes de compatibilidad) y, a continuación, cargue solo exactamente lo que sea necesario cada vez que se produzca un cambio de estado en la aplicación. Lo que se necesita para este cambio de estado puede variar en función del conjunto de tecnologías elegidas, pero normalmente incluye un solo fragmento de HTML para reemplazar la &quot;vista&quot; existente y la ejecución de un bloque de código JS para cablear la nueva vista y realizar cualquier procesamiento de plantillas del lado del cliente que sea necesario. La velocidad de este cambio de estado se puede mejorar aún más si se admiten mecanismos de almacenamiento en caché de plantillas o incluso si se utiliza Adobe PhoneGap, se puede acceder sin conexión al contenido de las plantillas.

AEM SPA AEM.1 1 soporta la construcción y gestión de los recursos de las aplicaciones de la red a través de las aplicaciones de la. SPA Este artículo proporciona una introducción a los conceptos subyacentes a la y a cómo se aprovechan [AngularJS](https://angularjs.org/) para llevar su marca al App Store y al Google Play.

## SPA AEM en aplicaciones de {#spa-in-aem-apps}

AEM El marco de aplicación de una sola página en las aplicaciones de permite el alto rendimiento de una aplicación AngularJS, a la vez que permite a los autores (u otro personal no técnico) crear y administrar el contenido de la aplicación mediante el entorno de editor de arrastrar y soltar optimizado para el contacto que tradicionalmente se ha reservado para administrar sitios web. AEM ¿Ya tiene un sitio creado con la opción de creación de la? AEM Verá que reutilizar el contenido, los componentes, los flujos de trabajo, los recursos y los permisos es fácil con las aplicaciones de la red de aplicaciones de Adobe (App) de Adobe (App).

## Módulo de aplicación AngularJS {#angularjs-application-module}

AEM Las aplicaciones de AppMeasurement administran gran parte de la configuración de AngularJS por usted, incluida la creación del módulo de nivel superior de su aplicación. De forma predeterminada, este módulo se denomina &quot;AEMAngularApp&quot; y el script responsable de su generación se puede encontrar (y superponer) en /libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp.

Parte de la inicialización de la aplicación implica especificar de qué módulos AngularJS depende la aplicación. La lista de módulos que utiliza la aplicación está especificada por un script ubicado en /libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp y la puede superponer el componente de página de la aplicación para extraer los módulos AngularJS adicionales que requiera la aplicación. Por ejemplo, compare la secuencia de comandos anterior con la implementación de Geometrixx (ubicada en /apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp).

Para admitir la navegación entre los distintos estados de la aplicación, el script angular-app-module se repite en todas las páginas descendientes de la página de la aplicación de nivel superior para generar un conjunto de &quot;rutas&quot; y configura cada ruta en el servicio $routeProvider de Angular. Para ver un ejemplo del aspecto que tiene en la práctica, consulte el script angular-app-module generado por el ejemplo de la aplicación para Geometrixx Outdoors: (el vínculo requiere una instancia local). [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

Al profundizar en la AEMngularApp generada, encontrará una serie de rutas especificadas de la siguiente manera:

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

La muestra anterior ilustra, en particular, un ejemplo de paso de un parámetro como parte de la ruta. En este ejemplo indicamos que cuando se solicita una ruta que cumple el patrón especificado (/content/phonegap/geometrixx-outdoors/en/home/products/:id), debe gestionarse mediante la plantilla home/products.template.html y utilizar el controlador &quot;contentphonegapgeometrixxoutdoorsenhomeproducts&quot;.

La propiedad templateUrl especifica la plantilla que se cargará cuando se solicite esta ruta. Esta plantilla contendrá el HTML AEM de componentes de la aplicación que se han incluido en la página, así como cualquier directiva de AngularJS necesaria para conectar el lado del cliente de la aplicación. Para ver un ejemplo de una directiva AngularJS en un componente de Geometrixx, consulte la línea 45 de template.jsp del carrusel de barrido (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp).

## Controladores de página {#page-controllers}

En palabras del propio Angular, &quot;un controlador es una función constructora de JavaScript que se utiliza para aumentar el ámbito del Angular&quot;. ([origen](https://docs.angularjs.org/guide/controller)AEM ) Cada página de una aplicación de se conecta automáticamente a un controlador que se puede aumentar con cualquier controlador que especifique un `frameworkType` de `angular`. Eche un vistazo al componente ng-text como ejemplo (/libs/mobileapps/components/angular/ng-text), incluido el nodo cq:template, que se asegura de que cada vez que se añada este componente a una página, incluya esta propiedad importante.

Para ver un ejemplo de controlador más complejo, abra el script ng-template-page controller.jsp (ubicado en /apps/geometrixx-outdoors-app/components/angular/ng-template-page). De particular interés es el código JavaScript que genera cuando se ejecuta, que se procesa de la siguiente manera:

```xml
// Controller for page 'products'
.controller('contentphonegapgeometrixxoutdoorsenhomeproducts', ['$scope', '$http', '$routeParams',
    function($scope, $http, $routeParams) {
        var sku = $routeParams.id;
        var productPath = '/' + sku.substring(0, 2) + '/' + sku.substring(0, 4) + '/' + sku;
        var data = $http.get('home/products' + productPath + '.angular.json' + cacheKiller);

        /* ng-product component controller (path: content-par/ng-product) */
        data.then(function(response) {
            $scope.contentparngproduct = response.data["content-par/ng-product"].items;
        });

        /* ng-image component controller (path: content-par/ng-product/ng-image) */
        data.then(function(response) {
            $scope.contentparngproductngimage = response.data["content-par/ng-product/ng-image"].items;
        });
    }
])
```

En el ejemplo anterior, observará que estamos tomando un parámetro de la variable `$routeParams` y, a continuación, redistribuirlo en la estructura de directorios en la que se almacenan nuestros datos JSON. Al tratar con el sku `id` de esta manera, podemos ofrecer una sola plantilla de producto que pueda procesar los datos del producto para miles de productos diferentes. Este es un modelo mucho más escalable que requiere una ruta individual para cada elemento en una base de datos de productos (potencialmente) masiva.

Aquí también hay dos componentes: ng-product aumenta el ámbito con los datos que extrae de lo anterior `$http` llamada. También hay una imagen ng en esta página que a su vez aumenta el ámbito con el valor que recupera de la respuesta. En virtud de las disposiciones del Angular `$http` , cada componente esperará pacientemente hasta que la solicitud haya finalizado y se cumpla la promesa que ha creado.

## Pasos siguientes {#the-next-steps}

Una vez que conozca las aplicaciones de una sola página, consulte [Desarrollo de aplicaciones con CLI de PhoneGap](/help/mobile/phonegap-apps-pg-cli.md).
