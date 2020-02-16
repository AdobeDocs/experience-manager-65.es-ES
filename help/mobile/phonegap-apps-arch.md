---
title: La anatomía de una aplicación
seo-title: La anatomía de una aplicación
description: Esta página proporciona una descripción de los componentes de página que se crean para la aplicación basados en el componente /libs/mobileapps/components/angular/ng-page (CRXDE Lite en un servidor local).
seo-description: Esta página proporciona una descripción de los componentes de página que se crean para la aplicación basados en el componente /libs/mobileapps/components/angular/ng-page (CRXDE Lite en un servidor local).
uuid: 4c1a74c1-85af-4a79-b723-e9fbfc661d35
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 55667e62-a61b-4794-b292-8d54929c41ac
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# La anatomía de una aplicación{#the-anatomy-of-an-app}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

## Plantillas de página para aplicaciones móviles {#page-templates-for-mobile-apps}

Los componentes de página que cree para su aplicación se basan en el componente /libs/mobileapps/components/angular/ng-page ([abierto en CRXDE Lite en un servidor](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)local). Este componente contiene las siguientes secuencias de comandos JSP que el componente hereda o anula:

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
* pie de página.jsp
* js_clientlibs.jsp
* css_clientlibs.jsp

### ng-page.jsp {#ng-page-jsp}

Determina el nombre de la aplicación mediante la `applicationName` propiedad y lo expone mediante pageContext.

Incluye head.jsp y body.jsp.

### head.jsp {#head-jsp}

Escribe el `<head>` elemento de la página de la aplicación.

Si desea omitir la meta propiedad viewport de la aplicación, este es el archivo que anula.

Siguiendo las prácticas recomendadas, la aplicación incluye la parte css de las bibliotecas cliente en el encabezado, mientras que el JS se incluye en el elemento &lt; `body>` final.

### body.jsp {#body-jsp}

El cuerpo de una página angular se procesa de forma diferente en función de si se detecta wcmMode (!= WCMMode.DISABLED) para determinar si la página se abre para la creación o como una página publicada.

**Modo de creación**

En el modo de creación, cada página individual se representa por separado. Angular no gestiona el enrutamiento entre páginas ni se utiliza una vista ng para cargar una plantilla parcial que contenga los componentes de la página. En su lugar, el contenido de la plantilla de página (template.jsp) se incluye en el servidor mediante la `cq:include` etiqueta .

Esta estrategia habilita las funciones del autor (como agregar y editar componentes en el sistema de párrafos, la barra de tareas, el modo de diseño, etc.) para funcionar sin modificaciones. Las páginas que dependen del procesamiento del cliente, como las de las aplicaciones, no funcionan bien en el modo de creación de AEM.

Tenga en cuenta que la inclusión template.jsp se envuelve en un `div` elemento que contiene la `ng-controller` directiva. Esta estructura permite la vinculación del contenido DOM con el controlador. Por lo tanto, aunque las páginas que se representan en el lado del cliente fallan, los componentes individuales que lo hacen funcionan bien (consulte la sección sobre componentes más abajo).

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**Modo de publicación**

En el modo de publicación (como cuando la aplicación se exporta mediante la sincronización de contenido), todas las páginas se convierten en una aplicación de una sola página (SPA). (Para obtener más información sobre SPA, utilice el tutorial de Angular, en concreto [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07)).

Solo hay una página HTML en un SPA (una página que contiene el `<html>` elemento). Esta página se denomina &quot;plantilla de diseño&quot;. En terminología angular, es &quot;...una plantilla que es común para todas las vistas de nuestra aplicación.&quot; Considere esta página como la &#39;página de aplicación de nivel superior&#39;. Por convención, la página de aplicación de nivel superior es el `cq:Page` nodo de la aplicación más cercano a la raíz (y no es una redirección).

Dado que el URI real de la aplicación no cambia en el modo de publicación, las referencias a recursos externos de esta página deben utilizar rutas relativas. Por lo tanto, se proporciona un componente de imagen especial que tiene en cuenta esta página de nivel superior al procesar imágenes para la exportación.

Como SPA, esta página de plantilla de diseño simplemente genera un elemento div con una directiva de vista ng.

```xml
 <div ng-view ng-class="transition"></div>
```

El servicio de ruta angular utiliza este elemento para mostrar el contenido de todas las páginas de la aplicación, incluido el contenido de creación de la página actual (contenido en template.jsp).

El archivo body.jsp incluye header.jsp y pie.jsp, que están vacíos. Si desea proporcionar contenido estático en todas las páginas, puede anular estos scripts en la aplicación.

Por último, los clientlibs de javascript se incluyen en la parte inferior del elemento &lt;body>, incluidos dos archivos JS especiales que se generan en el servidor: *&lt;nombre de página>*.angular-app-module.js y *&lt;nombre de página>*.angular-app-controller.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

Esta secuencia de comandos define el módulo angular de la aplicación. El resultado de esta secuencia de comandos está vinculado al marcado que genera el resto del componente de la plantilla mediante el `html` elemento ng-page.jsp, que contiene el atributo siguiente:

```xml
ng-app="<c:out value='${applicationName}'/>"
```

Este atributo indica a Angular que el contenido de este elemento DOM debe estar vinculado al siguiente módulo. Este módulo vincula las vistas (en AEM estos serían recursos cq:Page) con los controladores correspondientes.

Este módulo también define un controlador de nivel superior denominado `AppController` que expone la `wcmMode` variable al ámbito y configura el URI desde el que se recuperan las cargas de actualización de Content Sync.

Por último, este módulo se repite a través de cada página descendiente (incluso a sí mismo) y procesa el contenido del límite de ruta de cada página (mediante el selector y extensión angular-route-fragment.js), incluida como una entrada de configuración en $routeProvider de Angular. En otras palabras, $routeProvider indica a la aplicación qué contenido se debe procesar cuando se solicita una ruta determinada.

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

Esta secuencia de comandos genera un fragmento de JavaScript que debe adoptar la siguiente forma:

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

Este código indica a $routeProvider (definido en angular-app-module.js.jsp) que &#39;/&lt;ruta>&#39; debe ser administrado por el recurso en `templateUrl`y cableado por `controller` (al que se accede a continuación).

Si es necesario, puede anular esta secuencia de comandos para gestionar rutas más complejas, incluidas las que tienen variables. Puede ver un ejemplo de esto en el script /apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp que se instala con AEM:

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

En Angular, los controladores agrupan las variables en el ámbito $scope, exponiéndolas a la vista. La secuencia de comandos angular-app-controllers.js.jsp sigue el patrón ilustrado por angular-app-module.js.jsp en el sentido de que se repite a través de cada página de descendientes (incluida la propia página) y genera el fragmento de controlador que cada página define (a través de controller.js.jsp). Se llama al módulo que define `cqAppControllers` y debe aparecer como una dependencia del módulo de aplicación de nivel superior para que los controladores de página estén disponibles.

### controller.js.jsp {#controller-js-jsp}

La secuencia de comandos controller.js.jsp genera el fragmento de controlador para cada página. Este fragmento de controlador adopta la forma siguiente:

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

Tenga en cuenta que a la `data` variable se le asigna la promesa devuelta por el `$http.get` método Angular. Cada componente incluido en esta página puede, si lo desea, hacer que algún contenido .json esté disponible (mediante su script angular.json.jsp) y actuar en función del contenido de esta solicitud cuando se resuelva. La solicitud es muy rápida en dispositivos móviles porque simplemente accede al sistema de archivos.

Para que un componente forme parte del controlador de esta forma, debe ampliar el componente /libs/mobileapps/components/angular/ng-component e incluir la `frameworkType: angular` propiedad.

### template.jsp {#template-jsp}

Presentado por primera vez en la sección body.jsp, template.jsp simplemente contiene el parámetro de la página. En el modo de publicación, se hace referencia a este contenido directamente (en &lt;page-path>.template.html) y se carga en el SPA a través de templateUrl configurado en $routeProvider.

El parsys de esta secuencia de comandos se puede configurar para aceptar cualquier tipo de componente. Sin embargo, se debe tener cuidado cuando se trata de componentes creados para un sitio web tradicional (en lugar de un SPA). Por ejemplo, el componente de imagen base funciona correctamente solo en la página de aplicación de nivel superior, ya que no está diseñado para hacer referencia a recursos que se encuentran dentro de una aplicación.

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

Esta secuencia de comandos simplemente genera las dependencias angulares del módulo de la aplicación Angular de nivel superior. angular-app-module.js.jsp hace referencia a él.

### header.jsp {#header-jsp}

Secuencia de comandos para colocar contenido estático en la parte superior de la aplicación. Este contenido se incluye en la página de nivel superior, fuera del ámbito de la vista ng.

### pie de página.jsp {#footer-jsp}

Secuencia de comandos para colocar contenido estático en la parte inferior de la aplicación. Este contenido se incluye en la página de nivel superior, fuera del ámbito de la vista ng.

### js_clientlibs.jsp {#js-clientlibs-jsp}

Anule esta secuencia de comandos para incluir sus clientlibs de JavaScript.

### css_clientlibs.jsp {#css-clientlibs-jsp}

Anule esta secuencia de comandos para incluir sus clientlibs de CSS.

## Componentes de la aplicación {#app-components}

Los componentes de la aplicación no solo deben funcionar en una instancia de AEM (publicación o creación), sino también cuando el contenido de la aplicación se exporta al sistema de archivos mediante la sincronización de contenido. Por consiguiente, el componente deberá incluir las siguientes características:

* Se debe hacer referencia a todos los recursos, plantillas y secuencias de comandos de una aplicación PhoneGap de forma relativa.
* La gestión de vínculos difiere si la instancia de AEM funciona en modo de autor o publicación.

### Recursos relativos {#relative-assets}

El URI de un recurso determinado en una aplicación PhoneGap difiere no sólo en cada plataforma, sino que es único en cada instalación de la aplicación. Por ejemplo, observe el siguiente URI de una aplicación que se ejecuta en el simulador de iOS:

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

Observe el GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39; en la ruta.

Como desarrollador de PhoneGap, el contenido que le preocupa se encuentra debajo del directorio www. Para acceder a los recursos de la aplicación, utilice rutas relativas.

Para agravar el problema, la aplicación PhoneGap utiliza el patrón de aplicación de una sola página (SPA) para que el URI base (excluido el hash) nunca cambie. Por lo tanto, cada recurso, plantilla o secuencia de comandos a los que haga referencia **debe ser relativo a la página de nivel superior. **La página de nivel superior inicializa el enrutamiento angular y los controladores en virtud de `*<name>*.angular-app-module.js` y `*<name>*.angular-app-controllers.js`. Esta página debe ser la página más cercana a la raíz del repositorio que *no *extienda un sling:redirect.

Existen varios métodos de ayuda disponibles para tratar las rutas relativas:

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

Para ver ejemplos de su uso, abra el origen mobileapps ubicado en /libs/mobileapps/components/angular.

### Vínculos {#links}

Los vínculos deben utilizar la `ng-click="go('/path')"` función para admitir todos los modos WCM. Esta función depende del valor de una variable de ámbito para determinar correctamente la acción del vínculo:

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

Cuando `$scope.wcmMode == true` administramos cada evento de navegación de la manera habitual, de modo que el resultado sea un cambio en la ruta o en la porción de página de la dirección URL.

Como alternativa, si `$scope.wcmMode == false`cada evento de navegación resulta en un cambio en la parte hash de la dirección URL que resuelve internamente el módulo ngRoute de Angular.

### Detalles del script de componente {#component-script-details}

![chlimage_1-144](assets/chlimage_1-144.png)

#### ng-component.jsp {#ng-component-jsp}

Esta secuencia de comandos muestra el contenido del componente o un marcador de posición adecuado cuando se detecta el modo de edición.

#### template.jsp {#template-jsp-1}

La secuencia de comandos template.jsp procesa el marcado del componente. Si el componente en cuestión está dirigido por datos JSON extraídos de AEM (como &#39;ng-text&#39;: /libs/mobileapps/components/angular/ng-text/template.jsp), esta secuencia de comandos será responsable de cablear el marcado con datos expuestos por el ámbito del controlador de la página.

Sin embargo, los requisitos de rendimiento a veces dictan que no se debe realizar ninguna plantilla del lado del cliente (es decir, enlace de datos). En este caso, simplemente procese el marcado del componente en el servidor y se incluirá en el contenido de la plantilla de página.

#### overhead.jsp {#overhead-jsp}

En componentes impulsados por datos JSON (como &#39;ng-text&#39;: /libs/mobileapps/components/angular/ng-text), se puede usar overhead.jsp para eliminar todo el código Java de template.jsp. Luego se hace referencia a él desde template.jsp y todas las variables que expone en la solicitud están disponibles para su uso. Esta estrategia fomenta la separación de la lógica de la presentación y limita la cantidad de código que se debe copiar y pegar cuando un nuevo componente se deriva de uno existente.

#### controller.js.jsp {#controller-js-jsp-1}

Como se describe en Plantillas de página de AEM, cada componente puede generar un fragmento de JavaScript para consumir el contenido JSON expuesto por la `data` promesa. Siguiendo convenciones angulares, un controlador solo debe utilizarse para asignar variables al ámbito.

#### angular.json.jsp {#angular-json-jsp}

Esta secuencia de comandos se incluye como un fragmento en el archivo &#39;&lt;page-name>.angular.json&#39; de toda la página que se exporta para cada página que extienda ng-page. En este archivo, el desarrollador de componentes puede exponer cualquier estructura JSON que requiera el componente. En el ejemplo &#39;ng-text&#39;, esta estructura simplemente incluye el contenido de texto del componente y un indicador que indica si el componente incluye o no texto enriquecido.

El componente de producto de la aplicación Geometrixx Outdoors es un ejemplo más complejo (/apps/geometrixx-outdoors-app/components/angular/ng-product):

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

Descargue recursos de CLI desde la consola Aplicaciones para optimizarlos para una plataforma específica y luego compilar la aplicación usando la API de integración de línea de comandos (CLI) de PhoneGap. El contenido del archivo ZIP que se guarda en el sistema de archivos local tiene la siguiente estructura:

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

Es un directorio oculto que puede que no vea en función de la configuración actual del sistema operativo. Debe configurar el sistema operativo para que este directorio sea visible si tiene pensado modificar los enlaces de la aplicación que contiene.

#### .cordova/ganchos/ {#cordova-hooks}

Este directorio contiene los enlaces [CLI](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/). Las carpetas del directorio de ganchos contienen secuencias de comandos node.js que se ejecutan en puntos exactos durante la compilación.

#### .cordova/ganchos/after-platform_add/ {#cordova-hooks-after-platform-add}

El directorio after-platform_add contiene el `copy_AMS_Conifg.js` archivo. Esta secuencia de comandos copia un archivo de configuración para admitir la recopilación de análisis de Adobe Mobile Services.

#### .cordova/ganchos/post-preparación/ {#cordova-hooks-after-prepare}

El directorio posterior a la preparación contiene el `copy_resource_files.js` archivo. Esta secuencia de comandos copia una serie de imágenes de icono y de pantalla de bienvenida en ubicaciones específicas de la plataforma.

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

El directorio before_platform_add contiene el `install_plugins.js` archivo. Esta secuencia de comandos se repite a través de una lista de identificadores de complemento de Cordova, instalando aquellos que detecta que no están disponibles.

Esta estrategia no requiere que agrupe e e instale los complementos en AEM cada vez que se ejecute el comando Maven `content-package:install` . La estrategia alternativa de comprobar los archivos en el sistema SCM requiere actividades repetitivas de compilación e instalación.

#### .cordova/ganchos/otros ganchos {#cordova-hooks-other-hooks}

Incluya otros ganchos según sea necesario. Los siguientes ganchos están disponibles (como proporciona la aplicación mundial de saludo de muestra de Phonegap):

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

#### platforms/ {#platforms}

Este directorio está vacío hasta que ejecute el `phonegap run <platform>` comando en el proyecto. Actualmente, `<platform>` puede ser `ios` o `android`.

Después de compilar la aplicación para una plataforma específica, se crea el directorio correspondiente y contiene el código de la aplicación específico de la plataforma.

#### plugins/ {#plugins}

El directorio de complementos se rellena con cada complemento enumerado en el `.cordova/hooks/before_platform_add/install_plugins.js` archivo después de ejecutar el `phonegap run <platform>` comando. El directorio está vacío inicialmente.

#### www/ {#www}

El directorio www contiene todo el contenido web (archivos HTML, JS y CSS) que implementa el aspecto y el comportamiento de la aplicación. Salvo las excepciones que se describen a continuación, este contenido se origina en AEM y se exporta a su formulario estático mediante la sincronización de contenido.

#### www/config.xml {#www-config-xml}

La documentación [de](https://docs.phonegap.com) PhoneGap hace referencia a este archivo como un &quot;archivo de configuración global&quot;. El archivo config.xml contiene muchas propiedades de la aplicación, como el nombre de la aplicación, las &quot;preferencias&quot; de la aplicación (por ejemplo, si una vista web de iOS permite el desplazamiento excesivo o no) y las dependencias de los complementos que *solo* utiliza PhoneGap build.

El archivo config.xml es un archivo estático en AEM y se exporta tal cual mediante la sincronización de contenido.

#### www/index.html {#www-index-html}

El archivo index.html redirige a la página de inicio de la aplicación.

El archivo config.xml contiene el `content` elemento:

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

En [la documentación](https://docs.phonegap.com)de PhoneGap, este elemento se describe como &quot;El elemento opcional &lt;content> define la página de inicio de la aplicación en el directorio de recursos web de nivel superior. El valor predeterminado es index.html, que normalmente aparece en el directorio www de nivel superior de un proyecto.&quot;

La compilación de PhoneGap falla si no hay un archivo index.html. Por lo tanto, se incluye este archivo.

#### www/res {#www-res}

El directorio res contiene imágenes e iconos de la pantalla de bienvenida. La `copy_resource_files.js` secuencia de comandos copia los archivos en sus ubicaciones específicas de la plataforma durante la fase de `after_prepare` compilación.

#### www/etc {#www-etc}

Por convención, en AEM el nodo /etc contiene contenido clientlib estático. El directorio etc contiene las bibliotecas Topcover, AngularJS y Geometrixx ng-clientlibstodas.

#### www/apps {#www-apps}

El directorio de aplicaciones contiene código relacionado con la página de bienvenida. La característica exclusiva de la página de bienvenida de una aplicación de AEM es que inicializa la aplicación sin interacción del usuario. El contenido clientlib (tanto CSS como JS) de la aplicación es, por lo tanto, mínimo para maximizar el rendimiento.

#### www/content {#www-content}

El directorio de contenido contiene el resto del contenido web de la aplicación. El contenido puede incluir, entre otros, los siguientes archivos:

* Contenido de página HTML, que se crea directamente en AEM
* Recursos de imagen asociados a componentes de AEM
* Contenido de JavaScript que generan las secuencias de comandos del lado del servidor
* Archivos JSON que describen el contenido de la página o del componente

#### www/package.json {#www-package-json}

El archivo package.json es un archivo de manifiesto que enumera los archivos que incluye una descarga **completa** de sincronización de contenido. Este archivo también contiene la marca de tiempo en la que se generó la carga útil de sincronización de contenido ( `lastModified`). Esta propiedad se utiliza al solicitar actualizaciones parciales de la aplicación desde AEM.

#### www/package-update.json {#www-package-update-json}

Si esta carga útil es una descarga de toda la aplicación, este manifiesto contiene la lista exacta de archivos como `package.json`.

Sin embargo, si esta carga útil es parcial, `package-update.json` contiene solo los archivos que se incluyen en esta carga útil concreta.

### Pasos siguientes {#the-next-steps}

Una vez que haya aprendido sobre la Anatomía de una aplicación, consulte Aplicaciones [de una](/help/mobile/phonegap-single-page-applications.md)sola página.
