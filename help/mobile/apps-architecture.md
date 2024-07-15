---
title: Plantillas de página para aplicaciones móviles
description: Siga esta página para obtener más información sobre las plantillas de página. Los componentes de página que cree para su aplicación se basan en el componente /libs/mobileapps/components/angular/ng-page.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 397def36-45b2-47a7-b103-99ca22b6dae1
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2587'
ht-degree: 0%

---

# Plantillas de página para aplicaciones móviles {#page-templates-for-mobile-apps}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

## Plantillas de página para aplicaciones móviles {#page-templates-for-mobile-apps-1}

Los componentes de página que cree para su aplicación se basan en el componente /libs/mobileapps/components/angular/ng-page ([abrir en el CRXDE Lite en un servidor local](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)). Este componente contiene los siguientes scripts JSP que el componente hereda o anula:

* ng-page.jsp
* head.jsp
* body.jsp
* angular-app-module.js.jsp
* angular-route-fragment.js.jsp
* angular-app-controllers.js.jsp
* controller.js.jsp
* template.jsp
* angular-module-list.js.jsp
* header.jsp
* footer.jsp
* js_clientlibs.jsp
* css_clientlibs.jsp

### ng-page.jsp {#ng-page-jsp}

Determina el nombre de la aplicación que usa la propiedad `applicationName` y la expone a través de pageContext.

Incluye head.jsp y body.jsp.

### head.jsp {#head-jsp}

Escribe el elemento `<head>` de la página de la aplicación.

Si desea anular la metapropiedad de la ventanilla móvil de la aplicación, este es el archivo que debe anular.

Siguiendo las prácticas recomendadas, la aplicación incluye la parte css de las bibliotecas de cliente en el encabezado, mientras que el JS se incluye en el elemento de cierre &lt; `body>`.

### body.jsp {#body-jsp}

El cuerpo de una página Angular se representa de forma diferente en función de si se detecta wcmMode (!)= WCMode.DISABLED) para determinar si la página se abre para la creación o como una página publicada.

**Modo de autor**

En el modo Autor, cada página individual se procesa por separado. El angular no gestiona el enrutamiento entre páginas ni se utiliza una vista ng para cargar una plantilla parcial que contenga los componentes de la página. En su lugar, el contenido de la plantilla de página (template.jsp) se incluye en el servidor mediante la etiqueta `cq:include`.

Esta estrategia permite al autor funciones (como añadir y editar componentes en el sistema de párrafos, Sidekick, modo de diseño, etc.) funcionar sin modificaciones. AEM Las páginas que dependen del procesamiento del lado del cliente, como las de las aplicaciones, no funcionan bien en el modo de autor de la.

La inclusión template.jsp está envuelta en un elemento `div` que contiene la directiva `ng-controller`. Esta estructura permite vincular el contenido DOM con el controlador. Por lo tanto, aunque las páginas que se representan en el lado del cliente fallan, los componentes individuales que lo hacen funcionan bien (consulte la sección sobre Componentes a continuación).

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**Modo Publish**

SPA En el modo Publicación (por ejemplo, cuando la aplicación se exporta mediante Sincronización de contenido), todas las páginas se convierten en una aplicación de una sola página (). SPA (Para obtener más información acerca de la, use el tutorial de Angular, específicamente [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07).)

Solo hay una página de HTML SPA en un elemento (una página que contiene el elemento `<html>`) de la. Esta página se conoce como &quot;plantilla de diseño&quot;. En la terminología de Angular, se trata de &quot;...una plantilla que es común para todas las vistas de la aplicación&quot;. Considere esta página como la &quot;página de aplicación de nivel superior&quot;. Por convención, la página de aplicación de nivel superior es el nodo `cq:Page` de la aplicación que está más cerca de la raíz (y no es una redirección).

Dado que el URI real de la aplicación no cambia en el modo de publicación, las referencias a recursos externos desde esta página deben utilizar rutas relativas. Por lo tanto, se proporciona un componente de imagen especial que tiene en cuenta esta página de nivel superior al procesar imágenes para exportarlas.

SPA Como un elemento de diseño, esta página de plantilla de diseño simplemente genera un elemento div con una directiva ng-view.

```xml
 <div ng-view ng-class="transition"></div>
```

El servicio de ruta de Angular utiliza este elemento para mostrar el contenido de todas las páginas de la aplicación, incluido el contenido legible de la página actual (contenido en template.jsp).

El archivo body.jsp incluye header.jsp y footer.jsp, que están vacíos. Si desea proporcionar contenido estático en cada página, puede anular estos scripts en la aplicación.

Por último, los clientlibs de javascript se incluyen en la parte inferior del elemento &lt;body> , incluidos dos archivos JS especiales que se generan en el servidor: *&lt;page name>*.angular-app-module.js y *&lt;page name>*.angular-app-controladores.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

Esta secuencia de comandos define el módulo de Angular de la aplicación. La salida de este script está vinculada al marcado que genera el resto del componente de la plantilla a través del elemento `html` en ng-page.jsp, que contiene el siguiente atributo:

```xml
ng-app="<c:out value='${applicationName}'/>"
```

Este atributo indica a Angular que el contenido de este elemento DOM debe vincularse al módulo siguiente. AEM Este módulo vincula las vistas (en el caso de los recursos cq:Page) con los controladores correspondientes.

Este módulo también define un controlador de nivel superior denominado `AppController` que expone la variable `wcmMode` al ámbito y configura el URI desde el cual se recuperarán las cargas de actualización de sincronización de contenido.

Por último, este módulo recorre en iteración cada página descendiente (incluida ella misma) y procesa el contenido del fragmento de ruta de cada página (a través del selector y la extensión angular-route-fragment.js), incluyéndolo como una entrada de configuración al \$routeProvider de Angular. En otras palabras, \$routeProvider indica a la aplicación qué contenido se debe representar cuando se solicita una ruta determinada.

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

Este script genera un fragmento de JavaScript que debe tener la siguiente forma:

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

Este código indica a $routeProvider (definido en angular-app-module.js.jsp) que &#39;/&lt;path>&#39; debe ser administrado por el recurso en `templateUrl`, y cableado por `controller` (que llegaremos a continuación).

Si es necesario, puede anular esta secuencia de comandos para gestionar rutas más complejas, incluidas aquellas con variables. AEM Un ejemplo de esto se puede ver en la secuencia de comandos /apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp que se instala con el siguiente comando:

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

En Angular, los controladores conectan variables en el ámbito \$y las exponen a la vista. El script angular-app-controllers.js.jsp sigue el patrón ilustrado por angular-app-module.js.jsp en el sentido de que se repite en cada página descendiente (incluida ella misma) y genera el fragmento de controlador que define cada página (a través de controller.js.jsp). El módulo que define se llama `cqAppControllers` y debe aparecer como una dependencia del módulo de aplicación de nivel superior para que los controladores de página estén disponibles.

### controller.js.jsp {#controller-js-jsp}

El script controller.js.jsp genera el fragmento de controlador para cada página. Este fragmento de controlador tiene la siguiente forma:

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

A la variable `data` se le asigna la promesa devuelta por el método de Angular `$http.get`. Si lo desea, cada componente incluido en esta página puede poner a disposición contenido .json (mediante su script angular.json.jsp) y actuar sobre el contenido de esta solicitud cuando se resuelva. La solicitud es muy rápida en dispositivos móviles porque simplemente accede al sistema de archivos.

Para que un componente forme parte del controlador de esta manera, debe extender el componente /libs/mobileapps/components/angular/ng-component e incluir la propiedad `frameworkType: angular`.

### template.jsp {#template-jsp}

Introducido por primera vez en la sección body.jsp, template.jsp simplemente contiene el parsys de la página. SPA En el modo de publicación, se hace referencia a este contenido directamente (en &lt;page-path>.template.html) y se carga en la interfaz de usuario a través de la URL de la plantilla configurada en la interfaz de usuario \$routeProvider.

El parsys de esta secuencia de comandos se puede configurar para aceptar cualquier tipo de componente. SPA Sin embargo, se debe tener cuidado al tratar con componentes creados para un sitio web tradicional (en lugar de un sitio web en el que se crea un sitio web en el que se puede acceder a un sitio web en el que se puede acceder a una página web en el que se puede acceder a un sitio web tradicional). Por ejemplo, el componente de imagen de base funciona correctamente solo en la página de aplicación de nivel superior, ya que no está diseñado para hacer referencia a los recursos que están dentro de una aplicación.

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

Este script simplemente genera las dependencias de Angular del módulo de aplicación de Angular de nivel superior. angular-app-module.js.jsp hace referencia a él.

### header.jsp {#header-jsp}

Scripts para colocar contenido estático en la parte superior de la aplicación. Este contenido se incluye en la página de nivel superior, fuera del ámbito de ng-view.

### footer.jsp {#footer-jsp}

Scripts para colocar contenido estático en la parte inferior de la aplicación. Este contenido se incluye en la página de nivel superior, fuera del ámbito de ng-view.

### js_clientlibs.jsp {#js-clientlibs-jsp}

Anule este script para incluir sus clientlibs de JavaScript.

### css_clientlibs.jsp {#css-clientlibs-jsp}

Anule este script para incluir los clientlibs de CSS.

## Componentes de aplicación {#app-components}

AEM Los componentes de la aplicación no solo deben funcionar en una instancia de (publicación o autor), sino también cuando el contenido de la aplicación se exporta al sistema de archivos mediante Sincronización de contenido. Por lo tanto, el componente debe incluir las siguientes características:

* Se debe hacer referencia relativa a todos los recursos, plantillas y scripts de una aplicación PhoneGap.
* AEM La administración de los vínculos difiere si la instancia de la funciona en el modo Autor o Publicación.

### Assets relativo {#relative-assets}

El URI de cualquier recurso determinado en una aplicación de PhoneGap difiere no solo por plataforma, sino que es único en cada instalación de la aplicación. Por ejemplo, observe el siguiente URI de una aplicación que se ejecuta en el simulador de iOS:

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

Observe el GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39; en la ruta.

Como desarrollador de PhoneGap, el contenido que le preocupa se encuentra debajo del directorio www. Para acceder a los recursos de la aplicación, utilice rutas relativas.

SPA Para agravar el problema, la aplicación PhoneGap utiliza el patrón de aplicación de una sola página (aplicación de una sola página), de modo que el URI base (excluido el hash) nunca cambie. Por lo tanto, cada recurso, plantilla o script al que haga referencia **debe ser relativo a la página de nivel superior.** La página de nivel superior inicializa el enrutamiento de Angular y los controladores en virtud de `*<name>*.angular-app-module.js` y `*<name>*.angular-app-controllers.js`. Esta página debe ser la página más cercana a la raíz del repositorio que *no *extienda un sling:redirect.

Hay varios métodos de ayuda disponibles para tratar con rutas relativas:

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

Para ver ejemplos de su uso, abra la fuente mobileapps ubicada en /libs/mobileapps/components/angular.

### Vínculos {#links}

Los vínculos deben utilizar la función `ng-click="go('/path')"` para admitir todos los modos WCM. Esta función depende del valor de una variable de ámbito para determinar correctamente la acción del vínculo:

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

Cuando `$scope.wcmMode == true` administramos cada evento de navegación de la manera habitual, de manera que el resultado es un cambio en la ruta y/o en la parte de página de la URL.

Alternativamente, si `$scope.wcmMode == false`, cada evento de navegación produce un cambio en la parte hash de la URL que se resuelve internamente mediante el módulo ngRoute de Angular.

### Detalles del script de componente {#component-script-details}

![chlimage_1-36](assets/chlimage_1-36.png)

#### ng-component.jsp {#ng-component-jsp}

Esta secuencia de comandos muestra el contenido del componente o un marcador de posición adecuado cuando se detecta el modo de edición.

#### template.jsp {#template-jsp-1}

El script template.jsp procesa el marcado del componente. AEM Si el componente en cuestión está impulsado por datos JSON extraídos de los datos (como &quot;ng-text&quot;: /libs/mobileapps/components/angular/ng-text/template.jsp), este script será responsable de cablear el marcado con datos expuestos por el ámbito del controlador de la página.

Sin embargo, los requisitos de rendimiento a veces dictan que no se realice ninguna plantilla del lado del cliente (también conocido como enlace de datos). En este caso, simplemente procese el marcado del componente en el servidor y se incluirá en el contenido de la plantilla de página.

#### overhead.jsp {#overhead-jsp}

En componentes impulsados por datos JSON (como &quot;ng-text&quot;: /libs/mobileapps/components/angular/ng-text), se puede utilizar head.jsp para eliminar todo el código Java de template.jsp. A continuación, se hace referencia a él desde template.jsp y cualquier variable que exponga en la solicitud estará disponible para su uso. Esta estrategia promueve la separación de la lógica de la presentación y limita la cantidad de código que debe copiarse y pegarse cuando se deriva un nuevo componente de uno existente.

#### controller.js.jsp {#controller-js-jsp-1}

AEM Como se describe en Plantillas de página de, cada componente puede generar un fragmento de JavaScript para consumir el contenido JSON expuesto por la promesa `data`. Siguiendo las convenciones de Angular, un controlador solo debe utilizarse para asignar variables al ámbito.

#### angular.json.jsp {#angular-json-jsp}

Este script se incluye como un fragmento en el archivo &#39;&lt;page-name>.angular.json&#39; de toda la página que se exporta para cada página que extiende ng-page. En este archivo, el desarrollador de componentes puede exponer cualquier estructura JSON que requiera el componente. En el ejemplo &quot;ng-text&quot;, esta estructura simplemente incluye el contenido de texto del componente y un indicador que indica si el componente incluye o no texto enriquecido.

El componente de producto de la aplicación de Geometrixx outdoors es un ejemplo más complejo (/apps/geometrixx-outdoors-app/components/angular/ng-product):

```xml
{
    "content-par/ng-product": {
        "items": [{
            "name": "Cajamara",
            "description": "Bike",
            "summaryHTML": "",
            "price": "$610.00",
            "SKU": "eqsmcj",
            "numberOfLikes": "0",
            "numberOfComments": "0"
        }]
    },
    "content-par/ng-product/ng-image": {
        "items": [{
            "hasContent": true,
            "imgSrc": "home/products/eq/eqsm/eqsmcj/jcr_content/content-par/ng-product/ng-image.img.jpg/1377771306985.jpg",
            "description": "",
            "alt": "Cajamara",
            "title": "Cajamara",
            "hasLink": false,
            "linkPath": "",
            "attributes": [{
                "attributeName": "class",
                "attributeValue": "cq-dd-image"
            }]
        }]
    }
}
```

## Contenido de la descarga de CLI de Assets {#contents-of-the-cli-assets-download}

Descargue los recursos CLI de la consola de aplicaciones para optimizarlos para una plataforma específica y, a continuación, cree la aplicación mediante la API de integración de línea de comandos (CLI) de PhoneGap. El contenido del archivo ZIP guardado en el sistema de archivos local tiene la siguiente estructura:

```xml
.cordova/
  |- hooks/
     |- after_prepare/
     |- before_platform_add/
     |- Other Hooks
plugins/
www/
  |- config.xml
  |- index.html
  |- res/
  |- etc/
  |- apps/
  |- content/
  |- package.json
  |- package-update.json
```

### .cordova {#cordova}

Este es un directorio oculto que puede que no vea en función de la configuración actual del sistema operativo. Debe configurar el sistema operativo para que este directorio sea visible si planea modificar los enlaces de la aplicación que contiene.

#### .cordova/hooks/ {#cordova-hooks}

Este directorio contiene los [enlaces CLI](https://cordova.apache.org/docs/en/10.x/guide/appdev/hooks/). Las carpetas del directorio hooks contienen scripts node.js que se ejecutan en puntos exactos durante la compilación.

#### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

El directorio after-platform_add contiene el archivo `copy_AMS_Conifg.js`. Este script copia un archivo de configuración para admitir la recopilación de análisis de Adobe Mobile Services.

#### .cordova/hooks/after-prepare/ {#cordova-hooks-after-prepare}

El directorio after-prepare contiene el archivo `copy_resource_files.js`. Este script copia varias imágenes de icono y de pantalla de inicio en ubicaciones específicas de la plataforma.

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

El directorio before_platform_add contiene el archivo `install_plugins.js`. Este script se repite a través de una lista de identificadores de complementos de Cordova, instalando aquellos que detecta que no están disponibles.

AEM Esta estrategia no requiere que agrupe e e instale los complementos para que se instalen cada vez que se ejecute el comando Maven `content-package:install`. La estrategia alternativa de registrar los archivos en el sistema SCM requiere actividades de agrupamiento e instalación repetitivas.

#### .cordova/hooks/Other Hooks {#cordova-hooks-other-hooks}

Incluya otros ganchos según sea necesario. Los siguientes vínculos están disponibles (tal como los proporciona la aplicación Hello World de ejemplo de PhoneGap):

* after_build
* before_build
* after_compile
* before_compile
* after_docs
* before_docs
* after_emulate
* before_emulate
* after_platform_add
* before_platform_add
* after_platform_ls
* before_platform_ls
* after_platform_rm
* before_platform_rm
* after_plugin_add
* before_plugin_add
* after_plugin_ls
* before_plugin_ls
* after_plugin_rm
* before_plugin_rm
* after_prepare
* before_prepare
* after_run
* before_run

#### platform/ {#platforms}

Este directorio está vacío hasta que ejecute el comando `phonegap run <platform>` en el proyecto. Actualmente, `<platform>` puede ser `ios` o `android`.

Después de crear la aplicación para una plataforma específica, se crea el directorio correspondiente y contiene el código de aplicación específico de la plataforma.

#### plugins/ {#plugins}

El directorio de complementos se rellena con cada complemento enumerado en el archivo `.cordova/hooks/before_platform_add/install_plugins.js` después de ejecutar el comando `phonegap run <platform>`. El directorio está inicialmente vacío.

#### www/ {#www}

El directorio www contiene todo el contenido web (archivos HTML, JS y CSS) que implementa el aspecto y el funcionamiento de la aplicación. AEM Excepto por las excepciones que se describen a continuación, este contenido se origina desde la sincronización de contenido y se exporta a su forma estática mediante la sincronización de contenido.

#### www/config.xml {#www-config-xml}

La documentación de PhoneGap (`https://docs.phonegap.com`) hace referencia a este archivo como un &quot;archivo de configuración global&quot;. El archivo config.xml contiene muchas propiedades de aplicación, como el nombre de la aplicación, las &quot;preferencias&quot; de la aplicación (por ejemplo, si una vista web de iOS permite el overscroll o no) y las dependencias del complemento que PhoneGap Build solo consume *1}.*

AEM El archivo config.xml es un archivo estático en el que se puede exportar el contenido tal cual, y se exporta tal cual mediante la sincronización de contenido.

#### www/index.html {#www-index-html}

El archivo index.html redirige a la página de inicio de la aplicación.

El archivo config.xml contiene el elemento `content`:

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

En la documentación de PhoneGap (`https://docs.phonegap.com`), este elemento se describe como &quot;El elemento opcional &lt;content> define la página de inicio de la aplicación en el directorio de recursos web de nivel superior. El valor predeterminado es index.html, que suele aparecer en el directorio www de nivel superior de un proyecto.&quot;

PhoneGap Build falla si no hay un archivo index.html. Por lo tanto, se incluye este archivo.

#### www/res {#www-res}

El directorio res contiene imágenes e iconos de pantalla de bienvenida. El script `copy_resource_files.js` copia los archivos en sus ubicaciones específicas de la plataforma durante la fase de compilación de `after_prepare`.

#### www/etc {#www-etc}

AEM De forma predeterminada, en el nodo /etc, el contenido clientlib es estático. El directorio etc contiene las bibliotecas Topcoat, AngularJS y Geometrixx-clientlibsall.

#### www/apps {#www-apps}

El directorio de aplicaciones contiene código relacionado con la página de inicio. AEM La característica única de la página de bienvenida de una aplicación de es que inicializa la aplicación sin interacción del usuario. Por lo tanto, el contenido clientlib (tanto CSS como JS) de la aplicación es mínimo para maximizar el rendimiento.

#### www/content {#www-content}

El directorio de contenido incluye el resto del contenido web de la aplicación. El contenido puede incluir, entre otros, los siguientes archivos:

* Contenido de la página del HTML AEM, creado directamente en el sitio de trabajo de la
* AEM Recursos de imagen asociados a componentes de la
* Contenido de JavaScript que generan los scripts del lado del servidor
* Archivos JSON que describen el contenido de una página o componente

#### www/package.json {#www-package-json}

El archivo package.json es un archivo de manifiesto que enumera los archivos que incluye una descarga de sincronización de contenido de **full**. Este archivo también contiene la marca de tiempo a la que se generó la carga útil de sincronización de contenido (`lastModified`). AEM Esta propiedad se utiliza al solicitar actualizaciones parciales de la aplicación desde el punto de vista de la aplicación

#### www/package-update.json {#www-package-update-json}

Si esta carga es una descarga de toda la aplicación, este manifiesto contiene la lista exacta de archivos como `package.json`.

Sin embargo, si esta carga útil es una actualización parcial, `package-update.json` contiene solamente los archivos que se incluyen en esta carga útil en particular.
