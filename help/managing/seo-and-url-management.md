---
title: 'Recomendaciones para la administración de direcciones URL y SEO '
seo-title: 'Recomendaciones para la administración de direcciones URL y SEO '
description: Obtenga información sobre las optimizaciones y recomendaciones de SEO para lograr estos objetivos en una implementación AEM.
seo-description: Obtenga información sobre las optimizaciones y recomendaciones de SEO para lograr estos objetivos en una implementación AEM.
uuid: 943e76c4-bd88-4b52-bb43-db375eb89d23
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 7c8f2cec-870b-41a8-8d98-70e29b495587
docset: aem65
translation-type: tm+mt
source-git-commit: c623724df8d849f4cc01f5dc134c775dc24dafc7
workflow-type: tm+mt
source-wordcount: '3119'
ht-degree: 98%

---


# Recomendaciones para la administración de direcciones URL y SEO{#seo-and-url-management-best-practices} 

La optimización de los motores de búsqueda (SEO) se ha convertido en una preocupación clave para muchos expertos en marketing. En consecuencia, es necesario abordar las preocupaciones de la SEO en muchos proyectos AEM.

En este documento primero se describen algunas [Prácticas recomendadas de SEO](#seo-best-practices) y recomendaciones para lograrlas en una implementación de AEM Luego, se profundiza en algunos de los [pasos de implementación más complejos](#aem-configurations) que se mencionan en la primera sección.

## Prácticas recomendadas de SEO {#seo-best-practices}

Esta sección describe algunas prácticas recomendadas generales de SEO.

### URL {#urls}

Existen algunas prácticas recomendadas generalmente aceptadas en cuanto a las URL.

En el proyecto de AEM, al evaluar las URL, pregúntese lo siguiente:

“Si un usuario viera esta URL y ningún contenido en la página, ¿podría describir de qué se trata?”

Si la respuesta es sí, es probable que la URL funcione bien en un motor de búsqueda.

A continuación se ofrecen algunas sugerencias generales para crear las URL para SEO:

* Utilice guiones para separar palabras.

   * Nombre las páginas utilizando guiones (-) como separadores.
   * Evite utilizar mayúsculas y minúsculas, guiones bajos y espacios.

* Evite el uso de parámetros de consulta siempre que sea posible. Si es necesario, limítelos a dos o menos.

   * Utilice la estructura de directorio para indicar la arquitectura de la información, cuando esté disponible.
   * Si no se puede utilizar una estructura de directorio, utilice selectores de Sling en la URL, en lugar de cadenas de consulta. Además del valor SEO que proporcionan, los selectores de Sling también harán que las páginas sean almacenables en la memoria caché para el despachador.

* Cuanto más fácil de leer sea una URL, mejor. Si las palabras clave están presentes en la URL, aumenta su valor.

   * Si se utilizan selectores en una página, se prefieren los selectores que proporcionan un valor semántico.
   * Si un ser humano no puede leer su URL, un motor de búsqueda tampoco podrá.
   * Por ejemplo:
      `mybrand.com/products/product-detail.product-category.product-name.html`
se prefiere en lugar de 
`mybrand.com/products/product-detail.1234.html`

* Evite los subdominios siempre que sea posible, ya que los motores de búsqueda los tratarán como entidades diferentes y fragmentarán el valor SEO del sitio.

   * En su lugar, utilice subrutas de primer nivel. Por ejemplo, en lugar de `es.mybrand.com/home.html`, utilice `www.mybrand.com/es/home.html`.

   * Planifique la jerarquía de contenido para que coincida con la manera en que se presentará el contenido, según esta guía.

* La eficacia de las palabras clave en las URL disminuye a medida que aumenta la longitud de la URL y la posición de la palabra clave. En otras palabras, cuanto más corto, mejor.

   * Utilice las técnicas y funciones para acortar URL de AEM para eliminar elementos innecesarios en la URL.
   * Por ejemplo, `mybrand.com/en/myPage.html` se prefiere en lugar de `mybrand.com/content/my-brand/en/myPage.html`.

* Utilice URL canónicas.

   * Cuando se puede servir una URL desde diferentes rutas o con diferentes parámetros o selectores, asegúrese de utilizar una `rel=canonical` etiqueta en la página.

   * Esto se puede incluir en el código de la plantilla de AEM.

* Haga coincidir las URL con los títulos de las páginas siempre que sea posible.

   * Se debe alentar a los autores de contenido a que sigan esta práctica.

* Admita la función de no distinguir mayúsculas de minúsculas en las solicitudes de URL.

   * Configure al despachante para que vuelva a escribir todas las solicitudes entrantes en minúsculas.
   * Capacite a los autores de contenido para crear todas las páginas con letras minúsculas.

* Asegúrese de que cada página solo se proporcione desde un protocolo.

   * A veces, los sitios se proporcionan desde `http` hasta que un usuario llega a una página con un formulario de cierre de compra o de inicio de sesión, por ejemplo, cuando cambia a `https`. Al establecer vínculos desde esta página, si el usuario puede regresar a las páginas de `http` y acceder a ellas a través de `https`, el motor de búsqueda las rastreará como dos páginas diferentes.

   * Actualmente, Google prefiere las páginas `https` a las `http`. Por esta razón, a menudo facilita las cosas al servir a todo el sitio `https`.

### Configuración de servidor {#server-configuration}

En cuanto a la configuración del servidor, puede realizar los siguientes pasos para asegurarse de que solo se rastreando el contenido correcto:

* Utilice un archivo `robots.txt` para bloquear el rastreo de cualquier contenido que no se deba indexar.

   * Bloquee **todo** el rastreo en los entornos de prueba.

* Al lanzar un nuevo sitio con URL actualizadas, implemente redirecciones 301 para asegurarse de que no se pierda la clasificación SEO existente.
* Incluya un icono de favoritos para el sitio.
* Implemente un mapa del sitio XML para que los motores de búsqueda rastreen fácilmente el contenido. Asegúrese de incluir un mapa del sitio móvil para sitios móviles o adaptables.

## Configuraciones de AEM {#aem-configurations}

En esta sección se describen los pasos de implementación necesarios para configurar AEM de modo que siga estas recomendaciones de SEO.

### Uso de selectores de Sling {#using-sling-selectors}

Anteriormente, el uso de parámetros de consulta era la práctica generalmente aceptada al crear una aplicación web empresarial.

La tendencia de los últimos años ha sido eliminarlos para facilitar la lectura de las URL. En muchas plataformas, esto implica implementar redirecciones en el servidor web o en la red de distribución de contenido (CDN), pero Sling lo hace sencillo. Selectores de Sling:

* Facilitan la lectura de las URL.
* Permiten almacenar en caché las páginas en el despachante y, a menudo, mejora la seguridad.
* Permiten dirigir el contenido directamente, en lugar de tener un servlet genérico que recupera el contenido. Esto otorga el beneficio de las ACL que aplica al repositorio y a los filtros que aplica en el despachante.

#### Uso de selectores para servlets {#using-selectors-for-servlets}

AEM ofrece dos opciones al escribir servlets:

* **Servlets bin**
* **Sling** servlets

Los siguientes ejemplos ilustran cómo registrar servlets que siguen ambos patrones, así como el beneficio que se obtiene por usar servlets de Sling.

#### Servlets bin (un nivel inferior) {#bin-servlets-one-level-down}

Los **servlets bin** siguen el patrón al que muchos desarrolladores están acostumbrados por la programación J2EE. El servlet se registra en una ruta específica, que en el caso de AEM suele estar debajo de `/bin` y se extraen los parámetros de solicitud necesarios de la cadena de consulta.

La anotación de SCR para este tipo de servlet tendría este aspecto:

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

Luego extrae los parámetros de la cadena de consulta mediante el objeto `SlingHttpServletRequest` incluido en el método `doGet`; por ejemplo:

```
String myParam = req.getParameter("myParam");
```

La URL resultante utilizada tendría este aspecto:

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

Hay algunos puntos que hay que tener en cuenta con este enfoque:

* La propia URL pierde el valor SEO. Los usuarios que acceden al sitio, incluidos los motores de búsqueda, no reciben ningún valor semántico de la URL, ya que esta representa una ruta programática y no la jerarquía de contenido.
* La presencia de parámetros de consulta en la URL significa que el despachante no podrá almacenar la respuesta en caché.
* Si desea proteger este servlet, debe implementar su propia lógica de seguridad personalizada en el servlet.
* El despachante debe configurarse (con cuidado) para que se muestre `/bin/myApp/myServlet`. La simple exposición de `/bin` permitiría el acceso a ciertos servlets que no deberían estar abiertos a los visitantes del sitio.

#### Sling servlets (un nivel más bajo) {#sling-servlets-one-level-down}

Los **servlets Sling** permiten registrar el servlet de manera opuesta. En lugar de dirigirse a un servlet y especificar el contenido que desea que el servlet procese en función de los parámetros de consulta, debe buscar el contenido que desea y especificar el servlet que debe presentar el contenido en función de los selectores de Sling.

La anotación de SCR para este tipo de servlet tendría este aspecto:

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json”, methods=”GET”)
```

En este caso, se puede acceder automáticamente al recurso al que se dirige la dirección URL (una instancia del recurso `myPageType`) en el servlet. Para acceder a él, se llama a:

```
Resource myPage = req.getResource();
```

La URL resultante utilizada tendría este aspecto:

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

Los beneficios de este enfoque son:

* Puede incluir el valor SEO, obtenido por la semántica presente en la jerarquía del sitio y el nombre de la página.
* Dado que no hay parámetros de consulta presentes, el despachante puede almacenar la respuesta en caché. Además, cualquier actualización realizada en la página a la que se dirige anulará esta caché cuando se active la página.
* Todas las ACL aplicadas a `/content/my-brand/my-page` entrarán en vigor cuando un usuario intente acceder a este servlet.
* El despachante ya estará configurado para servir este contenido como una función del sitio web. No se requiere ninguna configuración adicional.

### Reescribir URL {#url-rewriting}

En AEM, todas las páginas web se almacenan en `/content/my-brand/my-content`. Aunque esto puede resultar útil desde la perspectiva de la administración de datos del repositorio, no es necesariamente la forma en que desea que los clientes vean el sitio y puede entrar en conflicto con las directrices de SEO para que las URL sean lo más cortas posible. Además, es posible que sirva varios sitios web desde la misma instancia de AEM y desde diferentes nombres de dominio.

En esta sección se analizan las opciones disponibles en AEM para administrar estas URL y presentarlas a los usuarios de una forma más fácil de leer y compatible con la optimización para motores de búsqueda.

#### URL de vanidad {#vanity-urls}

Si un autor desea que una página sea accesible desde una segunda ubicación con fines promocionales, las URL personales de AEM, definidas página por página, pueden resultar útiles. Para agregar una URL de vanidad para una página, navegue hasta ella en la consola **Sitios** y edite las propiedades de la página. En la parte inferior de la pestaña **Básico**, verá una sección en la que se pueden agregar URL de vanidad. Tenga en cuenta que tener la página accesible a través de más de una URL fragmentará el valor SEO de la página, por lo que se debe agregar una etiqueta de URL canónica a la página para evitar este problema.

#### Nombres de páginas localizados {#localized-page-names}

Es posible que desee mostrar nombres de páginas localizados a los usuarios de contenido traducido. Por ejemplo:

* En lugar de hacer que un usuario que habla en español navegue a:
   `www.mydomain.com/es/home.html`

* Sería mejor que la URL fuera:
   `www.mydomain.com/es/casa.html`.

El desafío que supone la localización del nombre de la página es que muchas de las herramientas de localización disponibles en la plataforma AEM dependen de que los nombres de las páginas coincidan en las distintas configuraciones regionales para mantener el contenido sincronizado.

La propiedad `sling:alias` permite tener nuestro pastel y comerlo también. `sling:alias` se puede agregar como propiedad a cualquier recurso para permitir un nombre de alias para el recurso. En el ejemplo anterior, tendría:

* Una página del JCR en:
   `…/es/home`

* A continuación, agréguele una propiedad:
   `sling:alias` = `casa`

Esto permitiría a las herramientas de traducción de AEM, como el administrador de varios sitios, seguir manteniendo una relación entre:

* `/en/home`

* `/es/home`

También permite a los usuarios finales interactuar con el nombre de la página en sus idiomas nativos.

>[!NOTE]
>
>La propiedad `sling:alias` se puede establecer con la propiedad de Alias [ al editar Propiedades](/help/sites-authoring/editing-page-properties.md#advanced) de página.

#### /etc/map {#etc-map}

En una instalación estándar de AEM:

* para la configuración OSGi
   **Apache Sling Resource Resolver Factory**
( 
`org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* la propiedad
   **Ubicación de asignación** ( `resource.resolver.map.location`)

* va de manera predeterminada a`/etc/map`

En esta ubicación se pueden agregar definiciones de asignación a solicitudes entrantes de asignación, reescribir direcciones URL en páginas de AEM o en ambas.

Para crear una nueva asignación, cree un nuevo `sling:Mapping` nodo en esta ubicación debajo de `/http` o `/https`. En función de las propiedades `sling:match` y `sling:internalRedirect` establecidas en este nodo, AEM redireccionará todo el tráfico de la URL coincidente al valor especificado en la propiedad `internalRedirect` .

Si bien este es el enfoque que se documenta en la documentación oficial de AEM y Sling, el soporte de expresión regular proporcionado por esta implementación es limitado cuando se compara con las opciones disponibles utilizando directamente `SlingResourceResolver` . Además, la implementación de asignaciones de este modo puede provocar problemas con la invalidación de la caché del despachante.

A continuación se muestra un ejemplo de cómo se produce este problema:

1. Un usuario visita su sitio web y solicita `https://www.mydomain.com/my-page.html`
1. El despachante reenvía esta solicitud al servidor de publicación.
1. Con `/etc/map`, el servidor de publicación resuelve esta solicitud en `/content/my-brand/my-page` y produce la página.

1. El despachante almacena en la caché la respuesta en `/my-page.html` y le devuelve la respuesta al usuario.
1. Un autor de contenido hace un cambio en esta página y la activa.
1. El agente de vaciado del despachante envía una solicitud de anulación para `/content/my-brand/my-page`**.** Dado que el despachante no tiene una página en la caché en esta ruta, el contenido antiguo permanece en la caché y estará obsoleto.

Existen maneras de configurar reglas de vaciado de despacho personalizadas que asignarán la URL más corta a la URL más larga para invalidar la caché.

Sin embargo, también hay una forma más sencilla de gestionarlo:

1. **Reglas de SlingResourceResolver**

   Mediante la consola web (por ejemplo, localhost:4502/system/console/configMgr) puede configurar el Sling Resource Resolver:

   * **Apache Sling Resource Resolver Factory**

      `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`.
   Se recomienda crear las asignaciones necesarias para acortar las URL como expresiones regulares y luego definir estas configuraciones en un nodo OsgiConfignode `config.publish`, que se incluye en la creación.

   En lugar de definir las asignaciones en `/etc/map`, se pueden asignar directamente a la propiedad Asignaciones **de** URL ( `resource.resolver.mapping`):

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   En este ejemplo sencillo, se elimina `/content/my-brand/` desde el principio de cualquier URL donde esté presente.

   Esto convertiría una URL:

   * de `/content/my-brand/my-page.html`
   * a solo `/my-page.html`

   Esto concuerda con la práctica recomendada de mantener las URL lo más cortas posible.

1. **Asignación de resultados de URL en páginas**

   Después de haber definido las asignaciones en el Apache Sling Resource Resolver, debe utilizar estas asignaciones en los componentes para asegurarse de que las direcciones URL que se emitan en las páginas sean cortas y ordenadas. Puede hacerlo utilizando la función de asignación del `ResourceResolver`.

   Por ejemplo, si estaba implementando un componente de navegación personalizado que detalla los elementos secundarios de la página actual, puede utilizar el método de asignación de la siguiente manera:

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP Server mod_rewrite {#apache-http-server-mod-rewrite}

Hasta ahora, ha implementado asignaciones junto con la lógica de sus componentes para utilizar estas asignaciones al enviar URL a nuestras páginas.

La parte final es el manejo de estas URL abreviadas cuando llegan al despachante, que es donde `mod_rewrite` comienza a funcionar. La mayor ventaja de usar `mod_rewrite` es que las URL se asignan de nuevo a su formulario largo *antes* de enviarse al módulo del despachante. Esto significa que el despachante solicitará la URL larga del servidor de publicación y la almacenará en la memoria caché correspondiente. Por lo tanto, cualquier despachante que borre solicitudes que vengan del servidor de publicación, podrá invalidar este contenido correctamente.

Para implementar estas reglas, puede agregar elementos `RewriteRule` debajo del host virtual en la configuración de Apache HTTP Server. Si desea expandir las URL abreviadas del ejemplo anterior, puede implementar una regla con este aspecto:

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### Etiquetas de URL canónicas {#canonical-url-tags}

Las etiquetas de URL canónicas son etiquetas de vínculo colocadas en el encabezado de un documento HTML para aclarar cómo los motores de búsqueda deben tratar una página al indexar el contenido. El beneficio que ofrece es garantizar que (versiones diferentes de) una página se indexe como la misma aunque la URL de la página pueda contener diferencias.

Por ejemplo: si un sitio tuviera que ofrecer una versión de una página compatible con una impresora, un motor de búsqueda podría indexar esta página por separado desde la versión normal de la página. La etiqueta canónica le dirá al motor de búsqueda que son iguales.

Ejemplos:

* https://www.mydomain.com/my-brand/my-page.html
* https://www.mydomain.com/my-brand/my-page.print.html

Ambos aplicarían la siguiente etiqueta al encabezado de la página:

```xml
<link rel=”canonical” href=”my-brand/my-page.html”/>
```

El valor `href` puede ser relativo o absoluto. El código debe incluirse en el marcado de la página para determinar la URL canónica de la página y mostrar esta etiqueta.

### Configurar el despachante para la insensibilidad de mayúsculas y minúsculas {#configuring-the-dispatcher-for-case-insensitivity}

La práctica recomendada es utilizar letras minúsculas en todas las páginas. Sin embargo, no desea que un usuario obtenga un error 404 cuando acceda al sitio web con letras mayúsculas en su URL. Por este motivo, Adobe recomienda agregar una regla de reescritura en la configuración de Apache HTTP Server para asignar todas las URL entrantes a minúsculas. Además, los autores de contenido deben recibir formación para crear sus páginas con nombres en minúsculas.

Para configurar Apache para que convierta todo el tráfico entrante a minúsculas, agregue lo siguiente a la configuración `vhost` :

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

Además, agregue lo siguiente a la parte superior del archivo `htaccess` :

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### Implementación de robots.txt para proteger los entornos de desarrollo {#implementing-robots-txt-to-protect-development-environments}

Los motores de búsqueda *deben* comprobar la presencia de un `robots.txt` archivo en la raíz del sitio antes de rastrear el sitio. Debe destacarse aquí porque mientras los principales motores de búsqueda como Google, Yahoo o Bing respetan esto, algunos motores de búsqueda extranjeros no lo hacen.

La manera más sencilla de bloquear el acceso a todo el sitio es colocar un archivo denominado `robots.txt` en la raíz del sitio con el siguiente contenido:

```xml
User-agent: *
Disallow: /
```

De lo contrario, en un entorno activo, puede optar por no permitir determinadas rutas que no desee indexar.

La advertencia de colocar el archivo `robots.txt` en la raíz del sitio es que las solicitudes de vaciar el despachante pueden borrar este archivo, y es probable que las asignaciones de URL coloquen la raíz del sitio en un lugar diferente al definido `DOCROOT` en la configuración del Apache HTTP Server. Por este motivo, es común colocar este archivo en la instancia de autor en la raíz del sitio y replicarlo en la instancia de publicación.

### Crear un mapa del sitio XML en AEM {#building-an-xml-sitemap-on-aem}

Los rastreadores utilizan mapas del sitio XML para comprender mejor la estructura de los sitios web. Si bien no hay garantías de que proporcionar un mapa del sitio conduzca a mejores clasificaciones SEO, se trata de una práctica recomendada acordada. Puede mantener manualmente un archivo XML en el servidor web para utilizarlo como mapa del sitio, pero se recomienda generar el mapa del sitio mediante programación, lo que garantiza que, a medida que los autores creen nuevo contenido, el mapa del sitio reflejará automáticamente sus cambios.

Para generar un mapa del sitio mediante programación, registre un servlet Sling que espere una llamada `sitemap.xml` . A continuación, el servlet puede utilizar el recurso proporcionado mediante la API de servlet para ver la página actual y sus elementos secundarios, con lo que se obtiene XML. El XML se almacenará en la caché en el despachante. Se debe hacer referencia a esta ubicación en la propiedad del mapa del sitio del archivo `robots.txt` . Además, será necesario implementar una regla de vaciado personalizada para asegurarse de vaciar este archivo cada vez que se active una nueva página.

>[!NOTE]
>
>Puede registrar un Sling Servlet para buscar el selector `sitemap` con la extensión `xml`. Esto hará que el servlet procese la solicitud cada vez que se solicite una URL que termine en:
>    `/<path-to>/page.sitemap.xml`
Luego, puede obtener el recurso solicitado de la solicitud y generar un mapa del sitio a partir de ese punto en el árbol de contenido mediante las API de JCR.
El beneficio de un enfoque como este es cuando se proporcionan múltiples sitios desde la misma instancia. Una solicitud para `/content/siteA.sitemap.xml` generaría un mapa del sitio para `siteA` mientras que una solicitud para `/content/siteB.sitemap.xml` generaría un mapa del sitio para `siteB` sin la necesidad de escribir un código adicional.

### Crear redirecciones 301 para URL heredadas {#creating-redirects-for-legacy-urls}

Al lanzar un sitio con una nueva estructura, implementar y probar redirecciones 301 en Apache HTTP Server es importante por dos motivos:

* Las URL heredadas acumularon un valor SEO con el tiempo. Al implementar una redirección, el motor de búsqueda puede aplicar este valor a la nueva URL.
* Es posible que los usuarios del sitio hayan creado marcadores en estas páginas. Al implementar las redirecciones, puede asegurarse de dirigir al usuario a la página del nuevo sitio que más coincida con el lugar en el que intentaba ingresar al sitio antiguo.

Para obtener instrucciones sobre cómo implementar las redirecciones 301, asegúrese de comprobar la sección de recursos adicionales que se muestra a continuación, así como una herramienta para probar que las redirecciones funcionan según lo esperado.

## Recursos adicionales {#additional-resources}

Para obtener más información, consulte los siguientes recursos adicionales:

* [Asignación de recursos](/help/sites-deploying/resource-mapping.md)
* [https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url](https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url)
* [https://moz.com/blog/15-seo-best-practices-for-structuring-urls](https://moz.com/blog/15-seo-best-practices-for-structuring-urls)
* [https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/](https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/)
* [https://sling.apache.org/documentation/the-sling-engine/servlets.html](https://sling.apache.org/documentation/the-sling-engine/servlets.html)
* [https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
* [https://httpd.apache.org/docs/current/mod/mod_rewrite.html](https://httpd.apache.org/docs/current/mod/mod_rewrite.html)
* [https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps](https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps)
* [https://www.robotstxt.org/robotstxt.html](https://www.robotstxt.org/robotstxt.html)
* [https://www.internetmarketingninjas.com/blog/search-engine-optimization/301-redirects/](https://www.internetmarketingninjas.com/blog/search-engine-optimization/301-redirects/)
* [https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester)
* [https://adobe-consulting-services.github.io/](https://adobe-consulting-services.github.io/)

