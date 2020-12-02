---
title: Aplicaciones de una sola página
seo-title: Aplicaciones de una sola página
description: Siga esta página para conocer las aplicaciones de una sola página, es decir, puede crear una aplicación que funcione de forma idéntica a una aplicación de escritorio o móvil.
seo-description: Siga esta página para conocer las aplicaciones de una sola página, es decir, puede crear una aplicación que funcione de forma idéntica a una aplicación de escritorio o móvil.
uuid: d1865e79-6e7c-4149-95c0-556e61478b01
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: a5b5e40e-2457-45fe-9632-baf5008fe8bf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 0%

---


# Aplicaciones de una sola página{#single-page-applications}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

[Las Aplicaciones](https://en.wikipedia.org/wiki/Single-page_application)  de una sola página (SPA) han alcanzado una masa crítica, generalmente consideradas como el patrón más efectivo para crear experiencias sin fisuras con la tecnología Web. Si sigue un patrón de SPA, puede crear una aplicación que funcione de forma idéntica a una aplicación de escritorio o móvil, pero que alcance una multitud de plataformas de dispositivos y factores de formulario debido a su base en estándares web abiertos.

En términos generales, SPA más rendimiento que los sitios web basados en páginas tradicionales porque normalmente cargan una página HTML completa **sólo una vez** (incluyendo CSS, JS y contenido de fuente compatible) y luego cargan sólo exactamente lo que es necesario cada vez que se produce un cambio de estado en la aplicación. Lo que se necesita para este cambio de estado puede variar en función del conjunto de tecnologías elegidas, pero generalmente incluye un solo fragmento HTML para reemplazar la &#39;vista&#39; existente y la ejecución de un bloque de código JS para conectar la nueva vista y realizar cualquier representación de plantilla de cliente que sea necesaria. La velocidad de este cambio de estado se puede mejorar aún más si se admiten mecanismos de almacenamiento en caché de plantillas o incluso acceso sin conexión al contenido de la plantilla si se utiliza Adobe PhoneGap.

AEM 6.1 apoya la construcción y gestión de SPA a través de AEM Apps. Este artículo proporciona una introducción a los conceptos subyacentes a la SPA y a cómo aprovechan [AngularJS](https://angularjs.org/) para llevar su marca a App Store y Google Play.

## SPA en aplicaciones de AEM {#spa-in-aem-apps}

El marco de aplicación de una sola página de AEM aplicaciones permite el alto rendimiento de una aplicación de AngularJS, al tiempo que permite a los autores (u otro personal no técnico) crear y administrar el contenido de la aplicación mediante el entorno de editor de arrastrar y soltar optimizado para el tacto, que tradicionalmente se ha reservado para administrar sitios web. ¿Ya tiene un sitio construido con AEM? Encontrará que reutilizar el contenido, los componentes, los flujos de trabajo, los recursos y los permisos es sencillo con AEM aplicaciones.

## Módulo de aplicación AngularJS {#angularjs-application-module}

AEM aplicaciones gestiona gran parte de la configuración de AngularJS, incluida la compilación del módulo de nivel superior de la aplicación. De forma predeterminada, este módulo se denomina &#39;AEMAngularApp&#39; y el script responsable de su generación se puede encontrar (y superponer) en /libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp.

Parte de la inicialización de la aplicación implica especificar de qué módulos AngularJS depende la aplicación. La lista de módulos que utiliza su aplicación se especifica mediante un script ubicado en /libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp, y el componente de página de sus propias aplicaciones puede superponerlos para obtener los módulos AngularJS adicionales que su aplicación necesite. Por ejemplo, compare la secuencia de comandos anterior con la implementación de Geometrixx (ubicada en /apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp).

Para admitir la navegación entre los distintos estados de la aplicación, el script angular-app-module se repite en todas las páginas descendientes de la página de la aplicación de nivel superior para generar un conjunto de &#39;rutas&#39; y configura cada ruta en el servicio $routeProvider de Angular. Para ver un ejemplo de cómo se ve esto en la práctica, eche un vistazo al script angular-app-module generado por el ejemplo de la aplicación Geometrixx Outdoors: (el vínculo requiere una instancia local) [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

Al buscar en la AEMAngularApp generada, encontrará una serie de rutas especificadas de la siguiente manera:

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

El ejemplo anterior ilustra en particular un ejemplo de cómo pasar un parámetro como parte de la ruta. En este ejemplo indicamos que cuando se solicita una ruta que cumpla el patrón especificado (/content/phonegap/geometrixx-outdoors/en/home/products/:id), debe gestionarse mediante la plantilla home/products.template.html y utilizar el controlador &#39;contentphonegapgeometrixoutdoorsenhomeproducts&#39;.

La plantilla que se cargará cuando se solicite esta ruta se especifica en la propiedad templateUrl. Esta plantilla contendrá el código HTML de AEM componentes que se han incluido en la página, así como las directivas AngularJS necesarias para cablear el lado del cliente de la aplicación. Para ver un ejemplo de una directiva AngularJS en un componente de Geometrixx, consulte la línea 45 de template.jsp (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp) del carrusel de barrido.

## Controladores de página {#page-controllers}

En palabras propias de Angular, &quot;un controlador es una función constructora de JavaScript que se utiliza para aumentar el ámbito angular&quot;. ([source](https://docs.angularjs.org/guide/controller)) Cada página de una aplicación AEM se conecta automáticamente a un controlador que puede ser aumentado por cualquier controlador que especifique un `frameworkType` de `angular`. Observe el componente ng-text como ejemplo (/libs/mobileapps/components/angular/ng-text), incluido el nodo cq:template que se asegura de que cada vez que se agrega este componente a una página incluya esta importante propiedad.

Para obtener un ejemplo de controlador más complejo, abra el script ng-template-page controller.jsp (ubicado en /apps/geometrixx-outdoors-app/components/angular/ng-template-page). De particular interés es el código javascript que genera cuando se ejecuta, que se procesa de la siguiente manera:

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

En el ejemplo anterior, observará que tomamos un parámetro del servicio `$routeParams` y luego lo analizamos en la estructura de directorio en la que se almacenan nuestros datos JSON. Al abordar el sku `id` de esta manera, podemos entregar una única plantilla de producto que puede procesar los datos del producto para miles potenciales de productos distintos. Se trata de un modelo mucho más escalable que requiere una ruta individual para cada elemento en una base de datos de productos masiva (potencialmente).

Aquí también hay dos componentes: ng-product aumenta el ámbito con los datos que extrae de la llamada `$http` anterior. También hay una imagen ng en esta página que, a su vez, también aumenta el ámbito con el valor que recupera de la respuesta. En virtud del servicio `$http` de Angular, cada componente esperará pacientemente hasta que la solicitud haya terminado y se cumpla la promesa que ha creado.

## Pasos siguientes {#the-next-steps}

Una vez que conozca las Aplicaciones de una sola página, consulte [Desarrollo de aplicaciones con la CLI de PhoneGap](/help/mobile/phonegap-apps-pg-cli.md).
