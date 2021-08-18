---
title: SCF Handlebars Helpers
seo-title: SCF Handlebars Helpers
description: Métodos de ayuda de manillares para facilitar el trabajo con SCF
seo-description: Métodos de ayuda de manillares para facilitar el trabajo con SCF
uuid: 9c514199-871e-4b68-8147-2052d2eeda15
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8b6c1697-d693-41f4-8337-f41658465107
exl-id: bfb95cae-4b0f-4521-a113-042dc4005a63
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 2%

---

# SCF Handlebars Helpers {#scf-handlebars-helpers}

| **[⇐ de características esenciales](essentials.md)** | **[Criterios de personalización del lado del servidor](server-customize.md)** |
|---|---|
|  | **[Criterios de personalización del lado del cliente](client-customize.md)** |

Handlebars Helpers (ayudantes) son métodos a los que se puede llamar desde scripts Handlebars para facilitar el trabajo con componentes SCF.

La implementación incluye una definición del lado del cliente y del lado del servidor. También es posible que los desarrolladores creen ayudantes personalizados.

Los ayudantes personalizados de SCF que se entregan con AEM Communities se definen en la [biblioteca de cliente](../../help/sites-developing/clientlibs.md):

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>Asegúrese de instalar el [paquete de funciones más reciente de Communities](deploy-communities.md#latestfeaturepack).

## Abreviar {#abbreviate}

Un ayudante para devolver una cadena abreviada que se ajuste a las propiedades maxWords y maxLength .

La cadena que se va a abreviar se proporciona como contexto. Si no se proporciona ningún contexto, se devuelve una cadena vacía.

En primer lugar, el contexto se recorta a maxLength y, a continuación, el contexto se divide en palabras y se reduce a maxWords.

Si safeString se establece en true, la cadena devuelta es SafeString.

### Parámetros {#parameters}

* **contexto**: Cadena

   (Opcional) El valor predeterminado es la cadena vacía

* **maxLength**: Número

   (Opcional) El valor predeterminado es la longitud del contexto.

* **maxWords**: Número

   (Opcional) El valor predeterminado es el número de palabras de la cadena recortada.

* **safeString**: Booleano

   (Opcional) Devuelve un Handlebars.SafeString() si es verdadero. El valor predeterminado es false.

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

Un ayudante a añadir dos espacios bajo un div, uno para el texto completo y el otro para el menos texto, con la capacidad de alternar entre las dos vistas.

### Parámetros {#parameters-1}

* **contexto**: Cadena

   (Opcional) El valor predeterminado es la cadena vacía.

* **numChars**: Número

   (Opcional) El número de caracteres que se mostrarán cuando no se muestre texto completo. El valor predeterminado es 100.

* **moreText**: Cadena

   (Opcional) Texto que se mostrará indicando que hay más texto que mostrar. El valor predeterminado es &quot;more&quot;.

* **elipsesText**: Cadena

   (Opcional) Texto que se mostrará indicando que hay texto oculto. El valor predeterminado es &quot;...&quot;.

* **safeString**: Booleano

   (Opcional) Valor booleano que indica si se deben aplicar o no Handlebars.SafeString() antes de devolver el resultado. El valor predeterminado es false.

### Ejemplo {#example}

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

Un ayudante para devolver una cadena de fecha con formato.

### Parámetros {#parameters-2}

* **contexto**: Número

   (Opcional) un valor de milisegundos compensado con respecto al 1 de enero de 1970 (epoch). El valor predeterminado es la fecha actual.

* **formato**: Cadena

   (Opcional) El formato de fecha que se va a aplicar. El valor predeterminado es &quot;AAAA-MM-DDTHH:mm:ss.sssZ&quot; y el resultado aparece como &quot;2015-03-18T18:17:13-07:00&quot;

### Ejemplos {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## Es igual a {#equals}

Un ayudante a devolver contenido en función de una condición de igualdad.

### Parámetros {#parameters-3}

* **lvalue**: Cadena

   El valor izquierdo que se va a comparar.

* **rvalue**: Cadena

   El valor a la derecha que se va a comparar.

### Ejemplo {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
{{else}}
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

Un asistente de bloque que prueba el valor actual de [WCM mode](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) con una lista de modos separados por cadenas.

### Parámetros {#parameters-4}

* **contexto**: Cadena

   (Opcional) La cadena que se va a traducir. Obligatorio si no se proporciona ningún valor predeterminado.

* **modo**: Cadena

   (Opcional) Una lista separada por comas de [modos WCM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) para probar si está configurada.

### Ejemplo {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{{else}}
 ...
{{/if-wcm-mode}}
```

## i18n {#i-n}

Este ayudante anula el Handlebars Helper &#39;i18n&#39;.

Consulte también [Internacionalización de cadenas en JavaScript Code](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code).

### Parámetros {#parameters-5}

* **contexto**: Cadena

   (Opcional) La cadena que se va a traducir. Obligatorio si no se proporciona ningún valor predeterminado.

* **predeterminado**: Cadena

   (Opcional) La cadena predeterminada que se va a traducir. Obligatorio si no se proporciona ningún contexto.

* **comentario**: Cadena

   (Opcional) Una sugerencia de traducción

### Ejemplo {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## Incluir {#include}

Un ayudante para incluir un componente como recurso no existente en una plantilla.

Esto permite que el recurso se personalice mediante programación con más facilidad de lo que es posible para un recurso añadido como nodo JCR. Consulte [Agregar o incluir un componente de comunidades](scf.md#add-or-include-a-communities-component).

Solo se pueden incluir algunos componentes de Communities. Para AEM 6.1, los que son inclusibles son [comentarios](essentials-comments.md), [clasificación](rating-basics.md), [revisiones](reviews-basics.md) y [votación](essentials-voting.md).

Este asistente, apropiado solo en el lado del servidor, proporciona una funcionalidad similar a [cq:include](../../help/sites-developing/taglib.md) para scripts JSP.

### Parámetros {#parameters-6}

* **contexto**: Cadena u objeto

   (Opcional, a menos que proporcione una ruta relativa)

   Utilice `this` para pasar el contexto actual.

   Utilice `this.id` para obtener el recurso en `id` para procesar el resourceType solicitado.

* **resourceType**: Cadena

   (Opcional) el tipo de recurso pasará de forma predeterminada al tipo de recurso desde el contexto.

* **plantilla**: Cadena

   Ruta al script de componente.

* **ruta**: Cadena

   (Obligatorio) Ruta al recurso. Si la ruta es relativa, se debe proporcionar un contexto; de lo contrario, se devuelve la cadena vacía.

* **authoringDisabled**: Booleano

   (Opcional) El valor predeterminado es false. Solo para uso interno.

### Ejemplo {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

Esto incluirá un nuevo componente de comentarios en `this.id` + /comments.

## IncludeClientLib {#includeclientlib}

Un asistente que incluye una biblioteca de cliente html AEM, que puede ser un js, un css o una biblioteca de temas. Para varias inclusiones de diferentes tipos, por ejemplo js y css, esta etiqueta debe utilizarse varias veces en el script Handlebars.

Este asistente, apropiado solo en el lado del servidor, proporciona una funcionalidad similar a [ui:includeClientLib](../../help/sites-developing/taglib.md) para scripts JSP.

### Parámetros {#parameters-7}

* **categorías**: Cadena

   (Opcional) Una lista de categorías de biblioteca de cliente separadas por coma. Esto incluirá todas las bibliotecas Javascript y CSS para las categorías dadas. El nombre del tema se extrae de la solicitud.

* **tema**: Cadena

   (Opcional) Una lista de categorías de biblioteca de cliente separadas por coma. Esto incluirá todas las bibliotecas relacionadas con temas (CSS y JS) para las categorías dadas. El nombre del tema se extrae de la solicitud.

* **js**: Cadena

   (Opcional) Una lista de categorías de biblioteca de cliente separadas por coma. Esto incluirá todas las bibliotecas JavaScript de las categorías dadas.

* **css**: Cadena

   (Opcional) Una lista de categorías de biblioteca de cliente separadas por coma. Esto incluirá todas las bibliotecas CSS de las categorías dadas.

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

## Pretty-time {#pretty-time}

Ayuda para mostrar cuánto tiempo ha pasado hasta un punto límite, después del cual se muestra un formato de fecha normal.

Por ejemplo:

* Hace 12 horas
* Hace 7 días

### Parámetros {#parameters-8}

* **contexto**: Número

   Un momento en el pasado para compararlo con &quot;ahora&quot;. El tiempo se expresa como un valor de milisegundos compensado con respecto al 1 de enero de 1970 (epoch).

* **daysCutoff**: Número

   El número de días antes de cambiar a una fecha real. El valor predeterminado es 60.

### Ejemplo {#example-5}

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

Un ayudante que codifica una cadena de origen para contenido de elementos HTML para ayudar a protegerse contra XSS.

NOTA: no es un validador y no se va a utilizar para escribir valores de atributo.

### Parámetros {#parameters-9}

* **contexto**: object

   El HTML que se va a codificar.

### Ejemplo {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

Un ayudante que codifica una cadena de origen para escribir en un valor de atributo HTML para ayudar a protegerse contra XSS.

NOTA: no es un validador y no se va a usar para escribir atributos procesables (href, src, controladores de eventos).

### Parámetros {#parameters-10}

* **contexto**: Objeto

   El HTML que se va a codificar.

### Ejemplo {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

Un ayudante que codifica una cadena de origen para escribir en contenido de cadena JavaScript para ayudar a protegerse contra XSS.

NOTA: no es un validador y no debe utilizarse para escribir en JavaScript arbitrario.

### Parámetros {#parameters-11}

* **contexto**: Objeto

   El HTML que se va a codificar.

### Ejemplo {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

Un ayudante que corrige una dirección URL para escribir como href HTML o valor de atributo srce para ayudar a protegerse contra XSS.

NOTA: esto puede devolver una cadena vacía

### Parámetros {#parameters-12}

* **contexto**: Objeto

   La URL para sanear.

### Ejemplo {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Información general básica de Handlebars.js {#handlebars-js-basic-overview}

* Una llamada de ayuda de Handlebars es un identificador simple (el *nombre* del ayudante), seguido de cero o más parámetros separados por espacio.
* Los parámetros pueden ser un objeto String, number, booleano o JSON simple, así como una secuencia opcional de pares clave-valor (argumentos hash) como los últimos parámetros.
* Las claves en los argumentos hash deben ser identificadores simples.
* Los valores de los argumentos hash son expresiones Handlebars: identificadores simples, rutas o cadenas.
* El contexto actual, `this`, siempre está disponible para los ayudantes de Handlebars.
* El contexto puede ser un objeto de datos String, number, booleano o JSON.
* Es posible pasar un objeto anidado dentro del contexto actual como contexto, como `this.url` o `this.id` (ver los siguientes ejemplos de asistentes simples y de bloque).

* Los ayudantes de bloque son funciones a las que se puede llamar desde cualquier lugar de la plantilla. Cada vez pueden invocar un bloque de la plantilla cero o más veces con un contexto diferente. Contienen un contexto entre {{#*name*}} y {{/*name*}.

* Handlebars proporciona un parámetro final para los ayudantes llamados &quot;opciones&quot;. El objeto especial &quot;options&quot; incluye

   * Datos privados opcionales (options.data)
   * Propiedades de clave-valor opcionales de la llamada (options.hash)
   * Capacidad de invocar (options.fn())
   * Capacidad de invocar lo contrario de sí mismo (options.inverse())

* Se recomienda que el contenido de cadena HTML devuelto por un ayudante sea SafeString.

### Un ejemplo de ayuda sencilla de la documentación de Handlebars.js: {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link_to', function(title, options) {
    return new Handlebars.SafeString('<a href="/posts' + this.url + '">' + title + "!</a>");
});

var context = {posts: [
    {url: "/hello-world",
      body: "Hello World!"}
  ] };

// when link_to is called, posts is the current context
var source = '<ul>{{#posts}}<li>{{{link_to "Post"}}}</li>{{/posts}}</ul>'

var template = Handlebars.compile(source);

template(context);
```

Renderizaría:

&lt;ul>
&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>¡Publicación!&lt;/a>&lt;/li>
&lt;/ul>

### Ejemplo de un asistente de bloque de la documentación de Handlebars.js: {#an-example-of-a-block-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link', function(options) {
    return new Handlebars.SafeString('<a href="/people/' + this.id + '">' + options.fn(this) + '</a>');
});

var data = { "people": [
  { "name": "Alan", "id": 1 },
  { "name": "Yehuda", "id": 2 }
]};

// when link is called, people is the current context
var source = "<ul>{{#people}}<li>{{#link}}{{name}}{{/link}}</li>{{/people}}</ul>";

var template = Handlebars.compile(source);

template(data);
```

Renderizaría:
&lt;ul>
&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>
&lt;li>&lt;a href=&quot;/people/2&quot;>Yehuda&lt;/a>&lt;/li>
&lt;/ul>

## Ayuda personalizada de SCF {#custom-scf-helpers}

Los ayudantes personalizados deben implementarse en el lado del servidor y del cliente, especialmente al pasar datos. Para SCF, la mayoría de las plantillas se compilan y procesan en el servidor, ya que el servidor genera el HTML para un componente determinado cuando se solicita la página.

### Ayudas personalizadas del lado del servidor {#server-side-custom-helpers}

Para implementar y registrar un asistente personalizado de SCF en el lado del servidor, simplemente implemente la interfaz Java [TemplateHelper](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html), conviértala en un [Servicio OSGi](../../help/sites-developing/the-basics.md#osgi) e instálelo como parte de un paquete OSGi.

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
>También se debe crear un asistente creado para el lado del servidor para el lado del cliente.
>
>El componente se vuelve a procesar en el lado del cliente para el usuario que ha iniciado sesión y, si no se encuentra el asistente del lado del cliente, el componente desaparece.

### Ayudantes personalizados del lado del cliente {#client-side-custom-helpers}

Los ayudantes del lado del cliente son secuencias de comandos Handlebars registradas invocando `Handlebars.registerHelper()`.
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

* Incluya una dependencia de `cq.social.scf`.
* Cargue después de cargar los controladores.
* Ser [incluido](clientlibs.md).

Nota: los ayudantes de SCF se definen en `/etc/clientlibs/social/commons/scf/helpers.js`.

| **[⇐ de características esenciales](essentials.md)** | **[Criterios de personalización del lado del servidor](server-customize.md)** |
|---|---|
|  | **[Criterios de personalización del lado del cliente](client-customize.md)** |
