---
title: SCF Handlebars Helpers
description: Métodos de ayuda para facilitar el trabajo con SCF
topic-tags: developing
content-type: reference
exl-id: bfb95cae-4b0f-4521-a113-042dc4005a63
source-git-commit: 787e5a87f13498006e2ce897e85ee12704b58f09
workflow-type: tm+mt
source-wordcount: '1453'
ht-degree: 2%

---

# SCF Handlebars Helpers {#scf-handlebars-helpers}

| **[⇐ aspectos básicos de funciones](essentials.md)** | **[⇒ de personalización del lado del servidor](server-customize.md)** |
|---|---|
|   | **[⇒ de personalización de cliente](client-customize.md)** |

Handlebars Helpers (ayudantes) son métodos a los que se puede llamar desde scripts Handlebars para facilitar el trabajo con componentes SCF.

La implementación incluye una definición del lado del cliente y una definición del lado del servidor. También es posible que los desarrolladores creen ayudantes personalizados.

Los ayudantes de SCF personalizados que se entregan con AEM Communities se definen en la [biblioteca de cliente](../../help/sites-developing/clientlibs.md):

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>Asegúrese de instalar el [último paquete de funciones de Communities](deploy-communities.md#latestfeaturepack).

## Abreviar {#abbreviate}

Un asistente para devolver una cadena abreviada que se ajuste a las propiedades maxWords y maxLength.

La cadena que se va a abreviar se proporciona como contexto. Si no se proporciona ningún contexto, se devuelve una cadena vacía.

En primer lugar, el contexto se recorta a maxLength y, a continuación, se divide en palabras y se reduce a maxWords.

Si safeString se establece en true, la cadena devuelta es SafeString.

### Parámetros {#parameters}

* **contexto**: cadena

  (Opcional) La cadena predeterminada está vacía

* **maxLength**: número

  (Opcional) El valor predeterminado es la longitud del contexto.

* **maxWords**: número

  (Opcional) El valor por defecto es el número de palabras de la cadena recortada.

* **safeString**: booleano

  (Opcional) Devuelve un valor Handlebars.SafeString() si es true. El valor predeterminado es false.

### Ejemplos {#examples}

```
{{abbreviate subject maxWords=2}}

/*
If subject =
    "AEM Communities - Site Creation Wizard"

Then abbreviate would return
    "AEM Communities".
*/
```

```
{{{abbreviate message safeString=true maxLength=30}}}

/*
If message =
    "The goal of AEM Communities is to quickly create a community engagement site."

Then abbreviate would return
    "The goal of AEM Communities is"
*/
```

## Content-loadmore {#content-loadmore}

Un asistente puede agregar dos espacios bajo un div, uno para el texto completo y otro para el texto menos, con la capacidad de alternar entre las dos vistas.

### Parámetros {#parameters-1}

* **contexto**: cadena

  (Opcional) El valor predeterminado es la cadena vacía.

* **numChars**: número

  (Opcional) El número de caracteres que se mostrarán cuando no se muestre texto completo. El valor predeterminado es 100.

* **moreText**: cadena

  (Opcional) Texto que se mostrará para indicar que hay más texto que mostrar. El valor predeterminado es &quot;más&quot;.

* **ellipsesText**: cadena

  (Opcional) Texto que se mostrará para indicar que hay texto oculto. El valor predeterminado es &quot;...&quot;.

* **safeString**: booleano

  (Opcional) Valor booleano que indica si se debe aplicar Handlebars.SafeString() antes de devolver el resultado. El valor predeterminado es false.

### Ejemplos {#example}

```
{{content-loadmore  context numChars=32  moreText="go on"  ellipsesText="..." }}

/*
If context =
    "Here is the initial less content and this is more content."

Then content-loadmore would return
    "Here is the initial less content<span class="moreelipses">...</span> <span class="scf-morecontent"><span>and this is more content.</span>  <a href="" class="scf-morelink" evt="click=toggleContent">go on</a></span>"
*/
```

## DateUtil {#dateutil}

Un asistente para devolver una cadena de fecha con formato.

### Parámetros {#parameters-2}

* **contexto**: número

  (Opcional) un valor de milisegundos de desplazamiento desde el 1 de enero de 1970 (epoch). El valor predeterminado es la fecha actual.

* **formato**: cadena

  (Opcional) Formato de fecha que se aplicará. El valor predeterminado es AAAA-MM-DDTHH:mm:ss.sssZ&quot; y el resultado será &quot;2015-03-18T18:17:13-07:00&quot;

### Ejemplos {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## Igual a {#equals}

Un asistente para devolver contenido en función de un condicional de igualdad.

### Parámetros {#parameters-3}

* **lvalue**: cadena

  El valor de la izquierda que se va a comparar.

* **rvalue**: cadena

  El valor de la derecha que se va a comparar.

### Ejemplos {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
`{{else}}`
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

Un asistente de bloque que prueba el valor actual de [Modo WCM](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) con una lista de modos separados por cadenas.

### Parámetros {#parameters-4}

* **contexto**: cadena

  (Opcional) La cadena que se va a traducir. Obligatorio si no se proporciona ningún valor predeterminado.

* **modo**: cadena

  (Opcional) Una lista separada por comas de [Modos WCM](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) para comprobar si está configurado.

### Ejemplos {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{else}}
 ...
`{{/if-wcm-mode}}`
```

## i18n {#i-n}

Este asistente anula el asistente Handlebars &#39;i18n&#39;.

Consulte también [Internacionalización de cadenas en código JavaScript](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code).

### Parámetros {#parameters-5}

* **contexto**: cadena

  (Opcional) La cadena que se va a traducir. Obligatorio si no se proporciona ningún valor predeterminado.

* **predeterminado**: cadena

  (Opcional) La cadena predeterminada que se va a traducir. Obligatorio si no se proporciona ningún contexto.

* **comentario**: cadena

  (Opcional) Una sugerencia de traducción

### Ejemplos {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## Incluir {#include}

Un asistente para incluir un componente como recurso no existente en una plantilla.

Este método permite personalizar el recurso mediante programación con mayor facilidad de lo que es posible para un recurso agregado como nodo JCR. Consulte [Agregar o incluir un componente de Communities](scf.md#add-or-include-a-communities-component).

Solo se pueden incluir algunos de los componentes de las comunidades que se han seleccionado. <!-- OBSOLETE/OLD  NEED TO UPDATE FOR 6.5  For AEM 6.1, those that are includable are [comments](essentials-comments.md), [rating](rating-basics.md), [reviews](reviews-basics.md), and [voting](essentials-voting.md). -->

Este asistente, que solo es adecuado en el lado del servidor, proporciona una funcionalidad similar a [cq:include](../../help/sites-developing/taglib.md) para scripts JSP.

### Parámetros {#parameters-6}

* **contexto**: cadena u objeto

  (Opcional, a menos que se proporcione una ruta relativa)

  Uso `this` para pasar el contexto actual.

  Uso `this.id` para obtener el recurso en `id` para procesar el resourceType solicitado.

* **resourceType**: cadena

  (Opcional) El tipo de recurso toma por defecto el tipo de recurso del contexto.

* **plantilla**: cadena

  Ruta al script de componente.

* **ruta**: cadena

  (Obligatorio) La ruta al recurso. Si la ruta es relativa, se debe proporcionar un contexto; de lo contrario, se devuelve la cadena vacía.

* **authoringDisabled**: booleano

  (Opcional) El valor predeterminado es falso. Solo para uso interno.

### Ejemplos {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

Incluye un nuevo componente de comentarios en `this.id` + /comments.

## IncludeClientLib {#includeclientlib}

AEM Un asistente que incluye una biblioteca de cliente de HTML de, que puede ser una biblioteca js, css o de temáticas. Para varias inclusiones de diferentes tipos, por ejemplo, js y css, esta etiqueta debe utilizarse varias veces en el script Handlebars.

Este asistente, que solo es adecuado en el lado del servidor, proporciona una funcionalidad similar a [ui:includeClientLib](../../help/sites-developing/taglib.md) para scripts JSP.

### Parámetros {#parameters-7}

* **categorías**: cadena

  (Opcional) Una lista de categorías de biblioteca de cliente separadas por comas. Incluya todas las bibliotecas JavaScript y CSS para las categorías dadas. El nombre de la temática se extrae de la solicitud.

* **tema**: cadena

  (Opcional) Una lista de categorías de biblioteca de cliente separadas por comas. Incluya todas las bibliotecas relacionadas con temas (tanto CSS como JS) para las categorías dadas. El nombre de la temática se extrae de la solicitud.

* **js**: cadena

  (Opcional) Una lista de categorías de biblioteca de cliente separadas por comas. Incluye todas las bibliotecas JavaScript para las categorías dadas.

* **css**: cadena

  (Opcional) Una lista de categorías de biblioteca de cliente separadas por comas. Incluye todas las bibliotecas CSS de las categorías dadas.

### Ejemplos {#examples-2}

```
// all: js + theme (theme-js + css)
{{includeClientLib categories="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/socialgraph.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/socialgraph.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// only js libs
{{includeClientLib js="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/socialgraph.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// theme only (theme-js + css)
{{includeClientLib theme="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// css only
{{includeClientLib css="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/socialgraph.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
```

## Tiempo bonito {#pretty-time}

Un asistente para mostrar cuánto tiempo ha pasado hasta un punto de corte, después del cual se muestra un formato de fecha normal.

Por ejemplo:

* Hace 12 horas
* Hace 7 días

### Parámetros {#parameters-8}

* **contexto**: número

  Un tiempo en el pasado para compararlo con el &#39;ahora&#39;. El tiempo se expresa como un desplazamiento de valor de milisegundos desde el 1 de enero de 1970 (época).

* **daysCutoff**: número

  Número de días transcurridos antes de cambiar a una fecha real. El valor predeterminado es 60.

### Ejemplos {#example-5}

```
{{pretty-time this.published daysCutoff=7}}

/*
Depending on how long in the past, may return

  "3 minutes ago"

  "3 hours ago"

  "3 days ago"
*/
```

## Xss-html {#xss-html}

Un asistente que codifica una cadena de origen para el contenido de elementos HTML para ayudar a protegerse contra XSS.

NOTA: Este asistente no es un validador y no debe utilizarse para escribir valores de atributo.

### Parámetros {#parameters-9}

* **contexto**: objeto

  HTML que se va a codificar.

### Ejemplos {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

Un asistente que codifica una cadena de origen para escribir en un valor de atributo de HTML para ayudar a protegerse contra XSS.

NOTA: Este asistente no es un validador y no debe utilizarse para escribir atributos procesables (href, src, controladores de eventos).

### Parámetros {#parameters-10}

* **contexto**: objeto

  HTML que se va a codificar.

### Ejemplos {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

Un asistente que codifica una cadena de origen para escribir en el contenido de la cadena JavaScript para ayudar a protegerse contra XSS.

NOTA: Este asistente no es un validador y no debe utilizarse para escribir en JavaScript arbitrario.

### Parámetros {#parameters-11}

* **contexto**: objeto

  HTML que se va a codificar.

### Ejemplos {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

Un asistente que sanea una dirección URL para escribir como un valor de atributo HTML href o srce para ayudar a protegerse contra XSS.

NOTA: Este asistente puede devolver una cadena vacía.

### Parámetros {#parameters-12}

* **contexto**: objeto

  Dirección URL para sanear.

### Ejemplos {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Información general básica de Handlebars.js {#handlebars-js-basic-overview}

* Una llamada de ayuda de Handlebars es un identificador simple (la variable *name* del asistente), seguido de cero o más parámetros separados por espacios.
* Los parámetros pueden ser un objeto simple String, number, boolean o JSON y una secuencia opcional de pares clave-valor (argumentos hash) como últimos parámetros.
* Las claves de los argumentos hash deben ser identificadores simples.
* Los valores de los argumentos hash son expresiones Handlebars: identificadores simples, rutas o cadenas.
* El contexto actual, `this`, siempre está disponible para los ayudantes de Handlebars.
* El contexto puede ser una cadena, un número, un booleano o un objeto de datos JSON.
* Es posible pasar un objeto anidado en el contexto actual como contexto, como `this.url` o `this.id` (consulte los siguientes ejemplos de ayudantes simples y de bloque).

* Los ayudantes de bloque son funciones a las que se puede llamar desde cualquier lugar de la plantilla. Pueden invocar un bloque de la plantilla cero o más veces con un contexto diferente cada vez. Contienen un contexto entre `{{#*name*}}` y `{{/*name*}}`.

* Los Handlebars proporcionan un parámetro final a los ayudantes llamados &quot;options&quot;. El objeto especial &quot;options&quot; incluye

   * Datos privados opcionales (options.data)
   * Propiedades clave-valor opcionales de la llamada (options.hash)
   * Capacidad para invocarse a sí mismo (options.fn())
   * Capacidad para invocar lo contrario a sí mismo (options.inverse())

* Se recomienda que el contenido de la cadena HTML devuelto por un asistente sea SafeString.

### Un ejemplo de un asistente simple de la documentación de Handlebars.js: {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link_to', function(title, options) {
    return new Handlebars.SafeString('<a href="/posts' + this.url + '">' + title + "!</a>");
});

var context = {posts: [
    {url: "/hello-world",
      body: "Hello World!"}
  ] };

// when link_to is called, posts is the current context
var source = '<ul>`{{#posts}}`<li>{{{link_to "Post"}}}</li>`{{/posts}}`</ul>'

var template = Handlebars.compile(source);

template(context);
```

Se renderizaría:

&lt;ul>
&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>¡Publica!&lt;/a>&lt;/li>
&lt;/ul>

### Un ejemplo de un asistente de bloque de la documentación de Handlebars.js: {#an-example-of-a-block-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link', function(options) {
    return new Handlebars.SafeString('<a href="/people/' + this.id + '">' + options.fn(this) + '</a>');
});

var data = { "people": [
  { "name": "Alan", "id": 1 },
  { "name": "Yehuda", "id": 2 }
]};

// when link is called, people is the current context
var source = "<ul>`{{#people}}`<li>`{{#link}}``{{name}}``{{/link}}`</li>`{{/people}}`</ul>";

var template = Handlebars.compile(source);

template(data);
```

Se renderizaría:
&lt;ul>
&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>
&lt;li>&lt;a href=&quot;/people/2&quot;>Yehuda&lt;/a>&lt;/li>
&lt;/ul>

## Ayudantes de SCF personalizados {#custom-scf-helpers}

Los asistentes personalizados deben implementarse en el lado del servidor y del cliente, especialmente al pasar datos. Para SCF, la mayoría de las plantillas se compilan y se representan en el servidor, ya que el servidor genera el HTML de un componente determinado cuando se solicita la página.

### Ayudantes personalizados del lado del servidor {#server-side-custom-helpers}

Para implementar y registrar un asistente SCF personalizado en el lado del servidor, simplemente implemente la interfaz Java™ [TemplateHelper](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html), conviértalo en un [Servicio OSGi](../../help/sites-developing/the-basics.md#osgi) e instálelo como parte de un paquete OSGi.

Por ejemplo:

### FooTextHelper.java {#footexthelper-java}

```java
/** Custom Handlebars Helper */

package com.my.helpers;

import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

import com.adobe.cq.social.handlebars.api.TemplateHelper;
import com.github.jknack.handlebars.Options;

@Service
@Component
public class FooTextHelper implements TemplateHelper<String>{

    @Override
    public CharSequence apply(String context, Options options) throws IOException {
        return "foo-" + context;
    }

    @Override
    public String getHelperName() {
        return "foo-text";
    }

    @Override
    public Class<String> getContextType() {
        return String.class;
    }
}
```

>[!NOTE]
>
>También se debe crear un asistente creado del lado del servidor para el lado del cliente.
>
>El componente se vuelve a procesar en el lado del cliente para el usuario que ha iniciado sesión y, si no se encuentra el asistente del lado del cliente, el componente desaparece.

### Ayudantes personalizados del lado del cliente {#client-side-custom-helpers}

Los ayudantes del lado del cliente son scripts Handlebars registrados invocando `Handlebars.registerHelper()`.
Por ejemplo:

### custom-helpers.js {#custom-helpers-js}

```
function(Handlebars, SCF, $CQ) {

    Handlebars.registerHelper('foo-text', function(context, options) {
        if (!context) {
            return "";
        }
        return "foo-" + context;
    });

})(Handlebars, SCF, $CQ);
```

Los ayudantes personalizados del lado del cliente deben agregarse a una biblioteca de cliente personalizada.
La clientlib debe:

* Incluir una dependencia en `cq.social.scf`.
* Cargar después de cargar Handlebars.
* Be [incluido](clientlibs.md).

Nota: Los ayudantes de SCF se definen en `/etc/clientlibs/social/commons/scf/helpers.js`.

| **[⇐ aspectos básicos de funciones](essentials.md)** | **[⇒ de personalización del lado del servidor](server-customize.md)** |
|---|---|
|   | **[⇒ de personalización de cliente](client-customize.md)** |
