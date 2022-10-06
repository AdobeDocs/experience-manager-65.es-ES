---
title: Aplicaciones de una sola página
seo-title: Single Page Applications
description: Siga esta página para obtener más información sobre las aplicaciones de una sola página, es decir, puede crear una aplicación que funcione de forma idéntica a una aplicación de escritorio o móvil.
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
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

[Aplicaciones de una sola página](https://en.wikipedia.org/wiki/Single-page_application) (SPA) han alcanzado una masa crítica, considerada ampliamente como el patrón más eficaz para crear experiencias fluidas con la tecnología web. Si sigue un patrón de SPA, puede crear una aplicación que funcione de forma idéntica a una aplicación de escritorio o móvil, pero que alcance una multitud de plataformas de dispositivos y factores de formulario debido a su fundación en estándares web abiertos.

En términos generales, SPA parecen tener un mayor rendimiento que los sitios web tradicionales basados en páginas porque normalmente cargan una página de HTML completa **solo una vez** (incluidos CSS, JS y contenido de fuente compatible) y, a continuación, cargue solo exactamente lo que sea necesario cada vez que se produzca un cambio de estado en la aplicación. Lo que es necesario para este cambio de estado puede variar en función del conjunto de tecnologías seleccionadas, pero normalmente incluye un solo fragmento de HTML para reemplazar la &quot;vista&quot; existente y la ejecución de un bloque de código JS para conectar la nueva vista y realizar cualquier representación de plantilla del lado del cliente que pueda ser necesaria. La velocidad de este cambio de estado se puede mejorar aún más si se admiten mecanismos de almacenamiento en caché de plantillas o incluso acceso sin conexión al contenido de plantillas si se utiliza Adobe PhoneGap.

AEM 6.1 es compatible con la construcción y administración de SPA a través de AEM Apps. Este artículo proporcionará una introducción a los conceptos subyacentes a la SPA y cómo se aprovechan [AngularJS](https://angularjs.org/) para llevar su marca a App Store y Google Play.

## SPA en aplicaciones AEM {#spa-in-aem-apps}

El marco Aplicación de una sola página de AEM aplicaciones permite un alto rendimiento de una aplicación AngularJS, a la vez que permite a los autores (u otro personal no técnico) crear y administrar el contenido de la aplicación mediante el entorno de editor táctil, de arrastrar y soltar, que tradicionalmente se ha reservado para la gestión de sitios web. ¿Ya tiene un sitio construido con AEM? Encontrará que reutilizar el contenido, los componentes, los flujos de trabajo, los recursos y los permisos es fácil con AEM aplicaciones.

## Módulo de aplicación AngularJS {#angularjs-application-module}

AEM aplicaciones gestiona gran parte de la configuración de AngularJS, incluido el módulo de nivel superior de la aplicación. De forma predeterminada, este módulo se llama &#39;AEMAngularApp&#39; y el script responsable de su generación se puede encontrar (y superponer) en /libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp.

Parte de la inicialización de la aplicación implica especificar de qué módulos AngularJS depende la aplicación. La lista de módulos que utiliza su aplicación la especifica un script ubicado en /libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp, y el componente de página de sus propias aplicaciones puede superponer para incorporar cualquier módulo AngularJS adicional que requiera su aplicación. Por ejemplo, compare el script anterior con la implementación de la Geometrixx (ubicada en /apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp).

Para admitir la navegación entre los distintos estados de la aplicación, el script angular-aplicación-módulo se repite en todas las páginas descendientes de la página de la aplicación de nivel superior para generar un conjunto de &quot;rutas&quot; y configura cada ruta en el servicio $routeProvider del Angular. Para ver un ejemplo de cómo se ve esto en la práctica, eche un vistazo al script del módulo de aplicaciones de angular generado por el ejemplo de la aplicación de Geometrixx Outdoors: (el vínculo requiere una instancia local) [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

Al profundizar en el AEMAngularApp generado, encontrará una serie de rutas especificadas de la siguiente manera:

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

El ejemplo anterior ilustra en particular un ejemplo de cómo pasar un parámetro como parte de la ruta. En este ejemplo indicamos que cuando se solicita una ruta que cumpla el patrón especificado (/content/phonegap/geometrixx-outdoors/en/home/products/:id), debe gestionarse mediante la plantilla home/products.template.html y utilizar el controlador &#39;contentphonegapgeometrixoutdoorsenhomeproducts&#39;.

La plantilla que se carga cuando se solicita esta ruta se especifica en la propiedad templateUrl . Esta plantilla contiene el HTML de AEM componentes que se han incluido en la página, así como cualquier directiva AngularJS necesaria para cablear el lado del cliente de la aplicación. Para ver un ejemplo de una directiva AngularJS en un componente de Geometrixx, eche un vistazo a la línea 45 de template.jsp del carrusel de barrido (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp).

## Controladores de página {#page-controllers}

En palabras del propio Angular, &quot;un controlador es una función constructora de JavaScript que se utiliza para aumentar el ámbito del Angular&quot;. ([source](https://docs.angularjs.org/guide/controller)) Cada página de una aplicación AEM se conecta automáticamente a un controlador que puede ser ampliado por cualquier controlador que especifique un `frameworkType` de `angular`. Eche un vistazo al componente ng-text como ejemplo (/libs/mobileapps/components/angular/ng-text), incluido el nodo cq:template que se asegura de que cada vez que este componente se añada a una página incluya esta importante propiedad.

Para un ejemplo de controlador más complejo, abra el script ng-template-page controller.jsp (ubicado en la página /apps/geometrixx-outdoors-app/components/angular/ng-template-page). De particular interés es el código javascript que genera cuando se ejecuta, que se procesa de la siguiente manera:

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

En el ejemplo anterior, verá que estamos tomando un parámetro de la variable `$routeParams` y luego masajearlo en la estructura de directorio en la que se almacenan nuestros datos JSON. Tratando con el sku `id` de este modo, podemos entregar una sola plantilla de producto que pueda procesar los datos del producto para miles de productos potenciales distintos. Este es un modelo mucho más escalable que requiere una ruta individual para cada elemento en una base de datos de productos masiva (potencialmente).

También hay dos componentes en funcionamiento aquí: ng-product aumenta el ámbito con los datos que extrae de lo anterior `$http` llamada a . También hay una imagen ng en esta página que a su vez también aumenta el ámbito con el valor que recupera de la respuesta. En virtud del Angular `$http` , cada componente esperará pacientemente hasta que la solicitud finalice y se cumpla la promesa que creó.

## Pasos siguientes {#the-next-steps}

Una vez que conozca las Aplicaciones de una sola página, consulte [Desarrollo de aplicaciones con la CLI de PhoneGap](/help/mobile/phonegap-apps-pg-cli.md).
