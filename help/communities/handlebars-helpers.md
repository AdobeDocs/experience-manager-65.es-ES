---
title: Ayudantes de manillares SCF
seo-title: Ayudantes de manillares SCF
description: Manillares Métodos de ayuda para facilitar el trabajo con SCF
seo-description: Manillares Métodos de ayuda para facilitar el trabajo con SCF
uuid: 9c514199-871e-4b68-8147-2052d2eeda15
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8b6c1697-d693-41f4-8337-f41658465107
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Ayudantes de manillares SCF {#scf-handlebars-helpers}

| **[Elementos básicos de las funciones de ⇐](essentials.md)** | **[Personalización del lado del servidor](server-customize.md)** |
|---|---|
|  | **[Personalización del cliente](client-customize.md)** |

Handlebars Helpers (ayudantes) son métodos que se pueden llamar desde scripts Handlebars para facilitar el trabajo con componentes SCF.

La implementación incluye una definición de cliente y de servidor. También es posible que los desarrolladores creen asistentes personalizados.

Los asistentes personalizados de SCF entregados con comunidades AEM se definen en la biblioteca [del cliente](../../help/sites-developing/clientlibs.md):

* /etc/clientlibs/social/commons/scf/helpers.js

>[!NOTE]
>
>Asegúrese de instalar el paquete [de funciones de Comunidades](deploy-communities.md#latestfeaturepack)más reciente.

## Abreviar {#abbreviate}

Un asistente para devolver una cadena abreviada que se ajuste a las propiedades maxWords y maxLength.

La cadena que se va a abreviar se proporciona como contexto. Si no se proporciona ningún contexto, se devuelve una cadena vacía.

En primer lugar, el contexto se recorta a maxLength y, a continuación, se divide en palabras y se reduce a maxWords.

Si safeString se establece en true, la cadena devuelta es SafeString.

### Parámetros {#parameters}

* **contexto**: Cadena

   (opcional) El valor predeterminado es la cadena vacía

* **maxLength**: Número

   (opcional) El valor predeterminado es la longitud del contexto.

* **maxWords**: Número

   (opcional) El valor predeterminado es el número de palabras de la cadena recortada.

* **safeString**:Booleano

   (opcional) Devuelve Handlebars.SafeString() si es true. El valor predeterminado es false.

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

Un ayudante para agregar dos grupos debajo de un div, uno para el texto completo y el otro para el menos texto, con la capacidad de alternar entre las dos vistas.

### Parámetros {#parameters-1}

* **contexto**: Cadena

   (opcional) El valor predeterminado es la cadena vacía.

* **numChars**: Número

   (opcional) El número de caracteres que se mostrarán cuando no se muestre texto completo. El valor predeterminado es 100.

* **moreText**: Cadena

   (opcional) El texto que se va a mostrar, que indica que hay más texto que mostrar. El valor predeterminado es &quot;more&quot;.

* **elipsesText**: Cadena

   (opcional) El texto que se va a mostrar y que indica que hay texto oculto. El valor predeterminado es &quot;...&quot;.

* **safeString**:Booleano

   (opcional) Valor booleano que indica si se deben aplicar o no Handlebars.SafeString() antes de devolver el resultado. El valor predeterminado es false.

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

Un asistente para devolver una cadena de fecha con formato.

### Parámetros {#parameters-2}

* **contexto**: Número

   (opcional) un valor de milisegundos compensado con respecto al 1 de enero de 1970 (epoch). El valor predeterminado es la fecha actual.

* **formato**: Cadena

   (opcional) El formato de fecha que se va a aplicar. El valor predeterminado es &quot;AAAA-MM-DDTHH:mm:ss.sssZ&quot; y el resultado aparece como &quot;2015-03-18T18:17:13-07:00&quot;

### Ejemplos {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## Equals {#equals}

Un asistente para devolver contenido según una condición de igualdad.

### Parámetros {#parameters-3}

* **lvalue**: Cadena

   El valor que se va a comparar a la izquierda

* **rvalue**: Cadena

   El valor de la derecha que se va a comparar

### Ejemplo {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
{{else}}
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

Asistente de bloque que prueba el valor actual del modo [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) WCM con una lista de modos separados por cadenas.

### Parámetros {#parameters-4}

* **contexto**: Cadena

   (opcional) La cadena que se va a traducir. Necesario si no se proporciona ningún valor predeterminado.

* **modo**: Cadena

   (opcional) Una lista separada por comas de los modos [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) WCM que se van a probar si están configurados.

### Ejemplo {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{{else}}
 ...
{{/if-wcm-mode}}
```

## i18n {#i-n}

Este asistente anula el asistente de Handlebars &#39;i18n&#39;.

Consulte también [Internacionalización de cadenas en código](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code)JavaScript.

### Parámetros {#parameters-5}

* **contexto**: Cadena

   (opcional) La cadena que se va a traducir. Necesario si no se proporciona ningún valor predeterminado.

* **predeterminado**: Cadena

   (opcional) La cadena predeterminada que se va a traducir. Necesario si no se proporciona ningún contexto.

* **comentario**: Cadena

   (opcional) Una sugerencia de traducción

### Ejemplo {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## Incluir {#include}

Un asistente para incluir un componente como recurso no existente en una plantilla.

Esto permite que el recurso se personalice mediante programación más fácilmente de lo que es posible para un recurso agregado como nodo JCR. Consulte [Agregar o incluir un componente](scf.md#add-or-include-a-communities-component)de comunidades.

Solo se pueden incluir algunos componentes de Comunidades. Para AEM 6.1, los que son incluyentes son [comentarios](essentials-comments.md), [clasificación](rating-basics.md), [revisiones](reviews-basics.md)y [votación](essentials-voting.md).

Este asistente, adecuado solo en el servidor, proporciona una funcionalidad similar a [cq:include](../../help/sites-developing/taglib.md) para scripts JSP.

### Parámetros {#parameters-6}

* **contexto**: Cadena u objeto

   (opcional, a menos que se proporcione una ruta relativa)

   usar `this`para pasar el contexto actual

   se utiliza `this.id` para obtener el recurso en `id` para procesar el resourceType solicitado

* **resourceType**: Cadena

   (opcional) el tipo de recurso predeterminado será el tipo de recurso del contexto

* **plantilla**: Cadena

   path to component script

* **path**: Cadena

   (obligatorio) La ruta al recurso. Si la ruta es relativa, se debe proporcionar un contexto; de lo contrario, se devuelve la cadena vacía.

* **authoringDisabled**:Booleano

   (opcional) El valor predeterminado es false. Solo para uso interno.

### Ejemplo {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

Esto incluirá un nuevo componente de comentarios en `this.id` + /comments

## IncludeClientLib {#includeclientlib}

Un asistente que incluye una biblioteca de cliente HTML de AEM, que puede ser un js, un css o una biblioteca de temas. Para varias inclusiones de diferentes tipos, por ejemplo js y css, esta etiqueta debe usarse varias veces en la secuencia de comandos Handlebars.

Este asistente, adecuado solo en el servidor, proporciona una funcionalidad similar a las secuencias de comandos [ui:includeClientLib](../../help/sites-developing/taglib.md) para JSP.

### Parámetros {#parameters-7}

* **categorías**: Cadena

   (opcional) Una lista de categorías de bibliotecas de cliente separadas por coma. Esto incluirá todas las bibliotecas Javascript y CSS para las categorías determinadas. El nombre del tema se extrae de la solicitud.

* **tema**: Cadena

   (opcional) Una lista de categorías de bibliotecas de cliente separadas por coma. Esto incluirá todas las bibliotecas relacionadas con temas (CSS y JS) para las categorías determinadas. El nombre del tema se extrae de la solicitud.

* **js**: Cadena

   (opcional) Una lista de categorías de bibliotecas de cliente separadas por coma. Esto incluirá todas las bibliotecas Javascript para las categorías determinadas.

* **css**: Cadena

   (opcional) Una lista de categorías de bibliotecas de cliente separadas por coma. Esto incluirá todas las bibliotecas CSS para las categorías determinadas.

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

Un asistente para mostrar cuánto tiempo ha pasado a un punto de corte, después del cual se muestra un formato de fecha normal.

Por ejemplo:

* Hace 12 horas
* 7 días antes

### Parámetros {#parameters-8}

* **contexto**: Número

   Un tiempo en el pasado para comparar con &#39;ahora&#39;. El tiempo se expresa como un valor de milisegundos compensado con respecto al 1 de enero de 1970 (epoch).

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

Un asistente que codifica una cadena de origen para contenido de elementos HTML para ayudar a protegerse de XSS.

NOTA: no es un validador y no se utiliza para escribir valores de atributos.

### Parámetros {#parameters-9}

* **contexto**: object

   HTML que codificar

### Ejemplo {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

Un asistente que codifica una cadena de origen para escribir en un valor de atributo HTML para ayudar a protegerse de XSS.

NOTA: no es un validador y no se utiliza para escribir atributos procesables (href, src, controladores de eventos).

### Parámetros {#parameters-10}

* **contexto**: Objeto

   El HTML que se va a codificar

### Ejemplo {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

Un asistente que codifica una cadena de origen para escribir en contenido de cadena JavaScript para ayudar a protegerse de XSS.

NOTA: no es un validador y no se utiliza para escribir en JavaScript arbitrario.

### Parámetros {#parameters-11}

* **contexto**: Objeto

   El HTML que se va a codificar

### Ejemplo {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

Un asistente que lisa una URL para escribir como href HTML o valor de atributo de origen para ayudar a proteger contra XSS.

NOTA: esto puede devolver una cadena vacía

### Parámetros {#parameters-12}

* **contexto**: Objeto

   La dirección URL que se va a sanear

### Ejemplo {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Información general básica de Handlebars.js {#handlebars-js-basic-overview}

Información general rápida sobre las funciones de ayuda de la documentación [de](https://handlebarsjs.com/expressions.html)Handlebars.js:

* Una llamada de ayuda de Handlebars es un identificador simple (el *nombre *del asistente), seguido de cero o más parámetros separados por espacios.
* Los parámetros pueden ser un objeto String, number, booleano o JSON sencillo, así como una secuencia opcional de pares de clave-valor (argumentos hash) como los últimos parámetros.
* Las claves de los argumentos hash deben ser identificadores simples.
* Los valores de los argumentos hash son expresiones Handlebars: identificadores simples, rutas o cadenas.
* El contexto actual, `this`, siempre está disponible para los ayudantes de Handlebars.
* El contexto puede ser un objeto de datos String, number, booleano o JSON.
* Es posible pasar un objeto anidado dentro del contexto actual como contexto, como `this.url` o `this.id` (vea los siguientes ejemplos de asistentes simples y de bloques).

* Los asistentes de bloque son funciones a las que se puede llamar desde cualquier lugar de la plantilla. Pueden invocar un bloque de la plantilla cero o más veces con un contexto diferente cada vez. Contienen un contexto entre {{#*name*}} y {{/*name*}}.

* Handlebars proporciona un parámetro final a los asistentes llamados &#39;options&#39;. El objeto especial &#39;options&#39; incluye

   * Datos privados opcionales (options.data)
   * Propiedades de clave-valor opcionales de la llamada (options.hash)
   * Capacidad para invocarse (options.fn())
   * Capacidad de invocar lo contrario de sí mismo (options.inverse())

* Se recomienda que el contenido de cadena HTML devuelto por un asistente sea SafeString.

### Ejemplo de un asistente sencillo de la documentación de Handlebars.js: {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

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

Se procesaría:

&lt;ul>&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>Publicación!&lt;/a>&lt;/li>&lt;/ul>

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

Se procesaría:
&lt;ul>&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>&lt;li>&lt;a href=&quot;/people/2&quot;>Yehuda&lt;/a>&lt;/li>&lt;/ul>

## Ayuda personalizada de SCF {#custom-scf-helpers}

Los asistentes personalizados deben implementarse en el lado del servidor y en el lado del cliente, especialmente al pasar datos. Para SCF, la mayoría de las plantillas se compilan y procesan en el servidor, ya que el servidor genera el código HTML para un componente determinado cuando se solicita la página.

### Ayudantes personalizados del lado del servidor {#server-side-custom-helpers}

Para implementar y registrar un asistente personalizado de SCF en el servidor, simplemente implemente la interfaz de Java [TemplateHelper](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html), conviértala en un servicio [](../../help/sites-developing/the-basics.md#osgi) OSGi e instálelo como parte de un paquete OSGi.

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

Los ayudantes del lado del cliente son scripts Handlebars registrados mediante invocación `Handlebars.registerHelper()`.
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

Los asistentes personalizados del lado del cliente deben agregarse a una biblioteca de cliente personalizada.
La clientlib debe:

* Incluir una dependencia de `cq.social.scf`
* Cargar después de cargar las barras de controladores
* Se [incluye](clientlibs.md)

Nota: los ayudantes de SCF están definidos en `/etc/clientlibs/social/commons/scf/helpers.js`.

| **[Elementos básicos de las funciones de ⇐](essentials.md)** | **[Personalización del lado del servidor](server-customize.md)** |
|---|---|
|  | **[Personalización del cliente](client-customize.md)** |

