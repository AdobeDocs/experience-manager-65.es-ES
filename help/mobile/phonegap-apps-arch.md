---
title: La anatomía de una aplicación
seo-title: The Anatomy of an App
description: Esta página proporciona una descripción de los componentes de página que crea para su aplicación y se basan en el componente /libs/mobileapps/components/angular/ng-page (CRXDE Lite en un servidor local).
seo-description: This page provides description of the page components that you create for your app are based on the /libs/mobileapps/components/angular/ng-page component (CRXDE Lite on a local server).
uuid: 4c1a74c1-85af-4a79-b723-e9fbfc661d35
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 55667e62-a61b-4794-b292-8d54929c41ac
exl-id: ab4f1c61-be83-420e-a339-02cf1f33efed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2686'
ht-degree: 0%

---

# La anatomía de una aplicación{#the-anatomy-of-an-app}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

## Plantillas de página para aplicaciones móviles {#page-templates-for-mobile-apps}

Los componentes de página que crea para su aplicación se basan en el componente /libs/mobileapps/components/angular/ng-page ([abrir en CRXDE Lite en un servidor local](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)). Este componente contiene los siguientes scripts JSP que su componente hereda o anula:

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

Determina el nombre de la aplicación utilizando la variable `applicationName` y la expone a través de pageContext.

Incluye head.jsp y body.jsp.

### head.jsp {#head-jsp}

Escribe el `<head>` elemento de la página de la aplicación.

Si desea anular la metapropiedad viewport de la aplicación, este es el archivo que anula.

Siguiendo las prácticas recomendadas, la aplicación incluye la parte css de las bibliotecas de cliente en el encabezado, mientras que el JS se incluye en la sección de cierre &lt; `body>` elemento.

### body.jsp {#body-jsp}

El cuerpo de una página de Angular se procesa de forma diferente en función de si se detecta wcmMode (!= WCMMode.DISABLED) para determinar si la página se abre para la creación o como una página publicada.

**Modo Autor**

En el modo de creación, cada página individual se procesa por separado. Angular no gestiona el enrutamiento entre páginas ni se utiliza una vista ng para cargar una plantilla parcial que contenga los componentes de la página. En su lugar, el contenido de la plantilla de página (template.jsp) se incluye en el servidor a través del `cq:include` etiqueta.

Esta estrategia permite las funciones del autor (como la adición y edición de componentes en el sistema de párrafos, la barra de tareas, el modo de diseño, etc.) para funcionar sin modificaciones. Las páginas que dependen de la renderización del lado del cliente, como las de las aplicaciones, no funcionan bien en AEM modo de autor.

Tenga en cuenta que la inclusión template.jsp se envuelve en un `div` elemento que contiene el `ng-controller` directiva. Esta estructura permite la vinculación del contenido DOM con el controlador. Por lo tanto, aunque las páginas que se renderizan a sí mismas en el lado del cliente fallan, los componentes individuales que lo hacen funcionan bien (consulte la sección sobre Componentes más abajo).

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**Modo de publicación**

En el modo de publicación (como cuando la aplicación se exporta mediante la sincronización de contenido), todas las páginas se convierten en una aplicación de una sola página (SPA). (Para obtener más información sobre SPA, utilice el tutorial de Angular, específicamente [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07).)

Solo hay una página HTML en un SPA (una página que contiene la variable `<html>` elemento). Esta página se conoce como &quot;plantilla de diseño&quot;. En terminología de Angular, es &quot;...una plantilla que es común para todas las vistas de nuestra aplicación.&quot; Considere esta página como la &quot;página de aplicación de nivel superior&quot;. Por norma, la página de aplicación de nivel superior es la `cq:Page` nodo de la aplicación que esté más cerca de la raíz (y no es un redireccionamiento).

Dado que el URI real de la aplicación no cambia en el modo de publicación, las referencias a recursos externos de esta página deben utilizar rutas relativas. Por lo tanto, se proporciona un componente de imagen especial que tiene en cuenta esta página de nivel superior al procesar imágenes para su exportación.

Como SPA, esta página de plantilla de diseño simplemente genera un elemento div con una directiva ng-view.

```xml
 <div ng-view ng-class="transition"></div>
```

El servicio de ruta de Angular utiliza este elemento para mostrar el contenido de todas las páginas de la aplicación, incluido el contenido legible de la página actual (contenido en template.jsp).

El archivo body.jsp incluye header.jsp y footer.jsp, que están vacíos. Si desea proporcionar contenido estático en todas las páginas, puede anular estos scripts en la aplicación.

Por último, los clientlibs de javascript se incluyen en la parte inferior del &lt;body> que incluye dos archivos JS especiales que se generan en el servidor: *&lt;page name=&quot;&quot;>*.angular-app-module.js y *&lt;page name=&quot;&quot;>*.angular-app-controls.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

Esta secuencia de comandos define el módulo de Angular de la aplicación. El resultado de esta secuencia de comandos está vinculado al marcado que genera el resto del componente de la plantilla a través del `html` en ng-page.jsp, que contiene el siguiente atributo:

```xml
ng-app="<c:out value='${applicationName}'/>"
```

Este atributo indica a Angular que el contenido de este elemento DOM debe estar vinculado al siguiente módulo. Este módulo vincula las vistas (en AEM serían recursos cq:Page) con los controladores correspondientes.

Este módulo también define un controlador de nivel superior denominado `AppController` que expone el `wcmMode` al ámbito y configura el URI desde el que se recuperan las cargas de actualización de Content Sync.

Por último, este módulo se repite a través de cada página descendiente (incluido el que se está usando) y procesa el contenido del trazado de cada página (a través del selector y extensión angular-route-fragment.js ), incluida como una entrada de configuración para $routeProvider de Angular. En otras palabras, $routeProvider indica a la aplicación qué contenido procesar cuando se solicita una ruta determinada.

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

Esta secuencia de comandos genera un fragmento de JavaScript que debe adoptar la siguiente forma:

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

Este código indica a $routeProvider (definido en angular-app-module.js.jsp) que &#39;/&lt;path>&#39; lo gestionará el recurso en `templateUrl`y cableado por `controller` (a lo que vamos a llegar después).

Si es necesario, puede anular esta secuencia de comandos para controlar rutas más complejas, incluidas las que tengan variables. Puede verse un ejemplo de esto en el script /apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp que se instala con AEM:

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

En Angular, los controladores agrupan variables en el ámbito $scope, exponiéndolas a la vista. La secuencia de comandos angular-app-controllers.js.jsp sigue el patrón ilustrado por angular-app-module.js.jsp en el sentido de que se repite a través de cada página descendiente (incluida la propia página) y genera el fragmento de controlador que cada página define (a través de controller.js.jsp). El módulo que define se llama `cqAppControllers` y deben aparecer como una dependencia del módulo de aplicación de nivel superior para que los controladores de página estén disponibles.

### controller.js.jsp {#controller-js-jsp}

La secuencia de comandos controller.js.jsp genera el fragmento de controlador para cada página. Este fragmento de controlador adopta la siguiente forma:

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

Tenga en cuenta que `data` se asigna a la promesa devuelta por el Angular `$http.get` método. Cada componente incluido en esta página puede, si lo desea, hacer que algún contenido .json esté disponible (a través de su script angular.json.jsp) y actuar sobre el contenido de esta solicitud cuando se resuelva. La solicitud es muy rápida en dispositivos móviles porque simplemente accede al sistema de archivos.

Para que un componente forme parte del controlador de esta manera, debe ampliar el componente /libs/mobileapps/components/angular/ng-component e incluir el `frameworkType: angular` propiedad.

### template.jsp {#template-jsp}

Presentado por primera vez en la sección body.jsp, template.jsp simplemente contiene el parsys de la página. En el modo de publicación, se hace referencia a este contenido directamente (en &lt;page-path>.template.html) y se carga en la SPA a través de la templateUrl configurada en $routeProvider.

El parsys de este script se puede configurar para aceptar cualquier tipo de componente. Sin embargo, se debe tener cuidado cuando se trata de componentes creados para un sitio web tradicional (en lugar de un SPA). Por ejemplo, el componente de imagen base funciona correctamente solo en la página de aplicación de nivel superior, ya que no está diseñado para hacer referencia a recursos que están dentro de una aplicación.

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

Esta secuencia de comandos simplemente genera las dependencias de Angular del módulo superior de la aplicación de Angular. angular-app-module.js.jsp hace referencia a él.

### header.jsp {#header-jsp}

Secuencia de comandos para colocar contenido estático en la parte superior de la aplicación. Este contenido lo incluye la página de nivel superior, fuera del ámbito de vista ng.

### footer.jsp {#footer-jsp}

Secuencia de comandos para colocar contenido estático en la parte inferior de la aplicación. Este contenido lo incluye la página de nivel superior, fuera del ámbito de vista ng.

### js_clientlibs.jsp {#js-clientlibs-jsp}

Anule esta secuencia de comandos para incluir sus clientlibs de JavaScript.

### css_clientlibs.jsp {#css-clientlibs-jsp}

Anule esta secuencia de comandos para incluir sus clientlibs de CSS.

## Componentes de la aplicación {#app-components}

Los componentes de la aplicación no solo deben funcionar en una instancia de AEM (publicación o autor), sino también cuando el contenido de la aplicación se exporta al sistema de archivos a través de la sincronización de contenido. Por lo tanto, el componente debe incluir las siguientes características:

* Se debe hacer referencia relativa a todos los recursos, plantillas y secuencias de comandos de una aplicación PhoneGap.
* El manejo de los vínculos difiere si la instancia de AEM funciona en modo de autor o publicación.

### Recursos relativos {#relative-assets}

El URI de cualquier recurso determinado en una aplicación PhoneGap no solo difiere en función de cada plataforma, sino que es único en cada instalación de la aplicación. Por ejemplo, observe el siguiente URI de una aplicación que se ejecuta en el simulador de iOS:

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

Observe el GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39; en la ruta.

Como desarrollador de PhoneGap, el contenido que le preocupa se encuentra debajo del directorio www. Para acceder a los recursos de la aplicación, utilice rutas relativas.

Para agravar el problema, la aplicación PhoneGap utiliza el patrón de aplicación de una sola página (SPA) para que el URI base (excluido el hash) nunca cambie. Por lo tanto, cada recurso, plantilla o secuencia de comandos a los que haga referencia **debe ser relativo a la página de nivel superior. **La página de nivel superior inicializa el enrutamiento de Angular y los controladores en virtud de `*<name>*.angular-app-module.js` y `*<name>*.angular-app-controllers.js`. Esta página debe ser la página más cercana a la raíz del repositorio que *no *extiende un sling:redirect.

Hay varios métodos de ayuda disponibles para tratar con rutas relativas:

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

Para ver ejemplos de su uso, abra la fuente mobileapps ubicada en /libs/mobileapps/components/angular.

### Vínculos {#links}

Los vínculos deben utilizar la variable `ng-click="go('/path')"` para admitir todos los modos WCM. Esta función depende del valor de una variable de ámbito para determinar correctamente la acción del vínculo:

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

When `$scope.wcmMode == true` gestionamos cada evento de navegación de la forma habitual, de modo que el resultado sea un cambio en la ruta o en la parte de página de la dirección URL.

Alternativamente, si `$scope.wcmMode == false`, cada evento de navegación produce un cambio en la parte hash de la dirección URL que se resuelve internamente mediante el módulo ngRoute de Angular.

### Detalles del script de componente {#component-script-details}

![chlimage_1-144](assets/chlimage_1-144.png)

#### ng-component.jsp {#ng-component-jsp}

Esta secuencia de comandos muestra el contenido del componente o un marcador de posición adecuado cuando se detecta el modo de edición.

#### template.jsp {#template-jsp-1}

La secuencia de comandos template.jsp representa el marcado del componente. Si el componente en cuestión está impulsado por datos JSON extraídos de AEM (como &quot;ng-text&quot;): /libs/mobileapps/components/angular/ng-text/template.jsp), esta secuencia de comandos será responsable de cablear el marcado con datos expuestos por el ámbito del controlador de la página.

Sin embargo, los requisitos de rendimiento a veces dictan que no se debe realizar ninguna plantilla del lado del cliente (también conocido como enlace de datos). En este caso, simplemente procese el marcado del componente en el servidor y se incluye en el contenido de la plantilla de página.

#### overhead.jsp {#overhead-jsp}

En componentes impulsados por datos JSON (como &quot;ng-text&quot;): /libs/mobileapps/components/angular/ng-text), sobrecarga.jsp se puede usar para eliminar todo el código Java de template.jsp. A continuación, se hace referencia a él desde template.jsp y todas las variables que expone en la solicitud están disponibles para su uso. Esta estrategia promueve la separación de la lógica de la presentación y limita la cantidad de código que debe copiarse y pegarse cuando se deriva un componente nuevo de uno existente.

#### controller.js.jsp {#controller-js-jsp-1}

Como se describe en AEM plantillas de página, cada componente puede generar un fragmento de JavaScript para consumir el contenido JSON expuesto por el `data` promesa. Siguiendo las convenciones de Angular, un controlador solo debe utilizarse para asignar variables al ámbito.

#### angular.json.jsp {#angular-json-jsp}

Esta secuencia de comandos se incluye como fragmento en la página &quot;&lt;page-name>Archivo .angular.json&#39; que se exporta para cada página que extiende ng-page. En este archivo, el desarrollador de componentes puede exponer cualquier estructura JSON que requiera el componente. En el ejemplo &quot;ng-text&quot;, esta estructura simplemente incluye el contenido de texto del componente y un indicador que indica si el componente incluye o no texto enriquecido.

El componente de producto de la aplicación de Geometrixx al aire libre es un ejemplo más complejo (/apps/geometrixx-outdoors-app/components/angular/ng-product):

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

## Contenido de la descarga de recursos CLI {#contents-of-the-cli-assets-download}

Descargue recursos CLI de la consola Aplicaciones para optimizarlos para una plataforma específica y luego cree la aplicación utilizando la API de integración de línea de comandos (CLI) de PhoneGap. El contenido del archivo ZIP que guarda en el sistema de archivos local tiene la siguiente estructura:

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

Este directorio contiene la variable [Enlaces CLI](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/). Las carpetas del directorio de enlaces contienen secuencias de comandos node.js que se ejecutan en puntos exactos durante la compilación.

#### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

El directorio after-platform_add contiene la variable `copy_AMS_Conifg.js` archivo. Esta secuencia de comandos copia un archivo de configuración para admitir la recopilación de análisis de Adobe Mobile Services.

#### .cordova/ganchos/pospreparación/ {#cordova-hooks-after-prepare}

El directorio después de la preparación contiene la variable `copy_resource_files.js` archivo. Esta secuencia de comandos copia varias imágenes de iconos y pantallas de inicio en ubicaciones específicas de la plataforma.

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

El directorio before_platform_add contiene la variable `install_plugins.js` archivo. Esta secuencia de comandos se repite a través de una lista de identificadores de complemento de Cordova, instalando los que detecta no están disponibles.

Esta estrategia no requiere que agrupe e e instale los complementos para AEM cada vez que Maven `content-package:install` se ejecuta. La estrategia alternativa de comprobar los archivos en su sistema SCM requiere un agrupamiento repetitivo e instalación de actividades.

#### .cordova/ganchos/otros ganchos {#cordova-hooks-other-hooks}

Incluya otros vínculos según sea necesario. Los siguientes vínculos están disponibles (tal y como proporciona la aplicación mundial de saludo de ejemplo de Phonegap):

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

#### plataformas/ {#platforms}

Este directorio está vacío hasta que ejecute el `phonegap run <platform>` en el proyecto. Actualmente, `<platform>` puede `ios` o `android`.

Después de compilar la aplicación para una plataforma específica, se crea el directorio correspondiente y contiene el código de aplicación específico de la plataforma.

#### plugins/ {#plugins}

El directorio de complementos se rellena con cada complemento enumerado en la variable `.cordova/hooks/before_platform_add/install_plugins.js` después de ejecutar el `phonegap run <platform>` comando. El directorio está inicialmente vacío.

#### www/ {#www}

El directorio www contiene todo el contenido web (archivos HTML, JS y CSS) que implementa el aspecto y el comportamiento de la aplicación. Salvo las excepciones que se describen a continuación, este contenido se origina en AEM y se exporta a su formulario estático a través de la sincronización de contenido.

#### www/config.xml {#www-config-xml}

La variable [Documentación de PhoneGap](https://docs.phonegap.com) hace referencia a este archivo como un &quot;archivo de configuración global&quot;. El archivo config.xml contiene muchas propiedades de la aplicación, como el nombre de la aplicación, las preferencias de la aplicación (por ejemplo, si una vista web de iOS permite el desplazamiento excesivo) y las dependencias de los complementos que son *only* consumido por la compilación de PhoneGap.

El archivo config.xml es un archivo estático en AEM y se exporta tal cual a través de la sincronización de contenido.

#### www/index.html {#www-index-html}

El archivo index.html redirige a la página de inicio de la aplicación.

El archivo config.xml contiene la variable `content` elemento:

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

En [la documentación de PhoneGap](https://docs.phonegap.com), este elemento se describe como &quot;El &lt;content> define la página de inicio de la aplicación en el directorio de recursos web de nivel superior. El valor predeterminado es index.html, que normalmente aparece en el directorio www de nivel superior de un proyecto.&quot;

La compilación de PhoneGap falla si no está presente un archivo index.html. Por lo tanto, se incluye este archivo.

#### www/res {#www-res}

El directorio res contiene imágenes e iconos de pantalla de inicio. La variable `copy_resource_files.js` la secuencia de comandos copia los archivos en ubicaciones específicas de la plataforma durante el `after_prepare` fase de compilación.

#### www/etc {#www-etc}

Por convención, en AEM el nodo /etc contiene contenido clientlib estático. El directorio etc contiene las bibliotecas Topcover, AngularJS y Geometrixx-clientlibsall.

#### www/apps {#www-apps}

El directorio de aplicaciones contiene código relacionado con la página de inicio. La característica exclusiva de la página de inicio de una aplicación AEM es que inicializa la aplicación sin interacción del usuario. Por lo tanto, el contenido clientlib (tanto CSS como JS) de la aplicación es mínimo para maximizar el rendimiento.

#### www/content {#www-content}

El directorio de contenido contiene el resto del contenido web de la aplicación. El contenido puede incluir, entre otros, los siguientes archivos:

* contenido de la página HTML, que se crea directamente en AEM
* Recursos de imagen asociados a componentes de AEM
* Contenido de JavaScript que generan las secuencias de comandos del lado del servidor
* Archivos JSON que describen contenido de página o componente

#### www/package.json {#www-package-json}

El archivo package.json es un archivo de manifiesto que enumera los archivos que **full** La descarga de la sincronización de contenido incluye . Este archivo también contiene la marca de tiempo en la que se generó la carga de la sincronización de contenido ( `lastModified`). Esta propiedad se utiliza al solicitar actualizaciones parciales de la aplicación desde AEM.

#### www/package-update.json {#www-package-update-json}

Si esta carga es una descarga de toda la aplicación, este manifiesto contiene la lista exacta de archivos como `package.json`.

Sin embargo, si esta carga es una actualización parcial, `package-update.json` contiene solo los archivos que se incluyen en esta carga útil concreta.

### Pasos siguientes {#the-next-steps}

Una vez que conozca la Anatomía de una aplicación, consulte [Aplicaciones de una sola página](/help/mobile/phonegap-single-page-applications.md).
