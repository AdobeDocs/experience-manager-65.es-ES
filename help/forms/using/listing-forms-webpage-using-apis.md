---
title: Lista de formularios en una página web mediante API
seo-title: Lista de formularios en una página web mediante API
description: Consulte mediante programación Forms Manager para recuperar una lista filtrada de formularios y mostrarla en sus propias páginas Web.
seo-description: Consulte mediante programación Forms Manager para recuperar una lista filtrada de formularios y mostrarla en sus propias páginas Web.
uuid: e51cb2d4-816f-4e6d-a081-51e4999b00ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 515ceaf6-c132-4e1a-b3c6-5d2c1ccffa7c
translation-type: tm+mt
source-git-commit: db69c393fc44ca2fcb30f9fcb0c5ca456ba35ed5

---


# Lista de formularios en una página web mediante API {#listing-forms-on-a-web-page-using-apis}

AEM Forms proporciona una API de búsqueda basada en REST que los desarrolladores web pueden utilizar para consultar y recuperar un conjunto de formularios que cumplen los criterios de búsqueda. Las API se pueden utilizar para buscar formularios basados en distintos filtros. El objeto response contiene atributos de formulario, propiedades y puntos finales de procesamiento de los formularios.

Para buscar formularios con la API de REST, envíe una solicitud GET al servidor en `https://[server]:[port]/libs/fd/fm/content/manage.json` los parámetros de consulta que se describen a continuación.

## Query parameters {#query-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>Nombre del atributo<br /> </strong></td>
   <td><strong>Descripción<br /> </strong></td>
  </tr>
  <tr>
   <td>func<br /> </td>
   <td><p>Especifica la función que se va a llamar. Para buscar formularios, establezca el valor del <code>func </code>atributo en <code>searchForms</code>.</p> <p>Por ejemplo, <code class="code">
       URLParameterBuilder entityBuilder=new URLParameterBuilder ();
       entityBuilder.add("func", "searchForms");</code></p> <p><strong></strong> Nota: <em>Este parámetro es obligatorio.</em><br /> </p> </td>
  </tr>
  <tr>
   <td>appPath<br /> </td>
   <td><p>Especifica la ruta de la aplicación para buscar formularios. De forma predeterminada, el atributo appPath busca en todas las aplicaciones disponibles en el nivel de nodo raíz.<br /> </p> <p>Puede especificar varias rutas de aplicación en una sola consulta de búsqueda. Separe las distintas rutas con el carácter de barra vertical (|). </p> </td>
  </tr>
  <tr>
   <td>cutPoints<br /> </td>
   <td><p>Especifica las propiedades que se van a recuperar con los recursos. Puede utilizar el asterisco (*) para recuperar todas las propiedades a la vez. Utilice el operador de barra vertical (|) para especificar varias propiedades. </p> <p>Por ejemplo, <code>cutPoints=propertyName1|propertyName2|propertyName3</code></p> <p><strong>Nota</strong>: </p>
    <ul>
     <li><em>Siempre se buscan propiedades como id, path y name. </em></li>
     <li><em>Cada recurso tiene un conjunto diferente de propiedades. Las propiedades como formUrl, pdfUrl y guideUrl no dependen del atributo cutpoints. Estas propiedades dependen del tipo de recurso y se recuperan en consecuencia. </em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>relation<br /> </td>
   <td>Especifica los recursos relacionados que se van a recuperar junto con los resultados de la búsqueda. Puede elegir una de las siguientes opciones para recuperar recursos relacionados:
    <ul>
     <li><strong>NO_RELATION</strong>: No busque recursos relacionados.</li>
     <li><strong>INMEDIATO</strong>: Recoge recursos directamente relacionados con los resultados de búsqueda.</li>
     <li><strong>ALL</strong>: Buscar directa e indirectamente recursos relacionados.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>maxSize</td>
   <td>Especifica el número máximo de formularios que se van a recuperar.</td>
  </tr>
  <tr>
   <td>desplazamiento</td>
   <td>Especifica el número de formularios que se omitirán desde el inicio.</td>
  </tr>
  <tr>
   <td>returnCount</td>
   <td>Especifica si se devuelven o no los resultados de búsqueda que coinciden con los criterios dados. </td>
  </tr>
  <tr>
   <td>sentencias</td>
   <td><p>Especifica la lista de instrucciones. Las consultas se ejecutan en la lista de instrucciones especificadas en el formato JSON. </p> <p>Por ejemplo,</p> <p><code class="code">JSONArray statementArray=new JSONArray();
       JSONObject statement=new JSONObject();
       statement.put("name", "title");
       statement.put("value", "SimpleSurveyAF");
       statement.put("operator", "EQ"); statementArray.put(statement);</code></p> <p>En el ejemplo anterior, </p>
    <ul>
     <li><strong>name</strong>: especifica el nombre de la propiedad que se va a buscar.</li>
     <li><strong>value</strong>: especifica el valor de la propiedad que se va a buscar.</li>
     <li><strong>operador</strong>: especifica el operador que se aplicará durante la búsqueda. Se admiten los siguientes operadores:
      <ul>
       <li>EQ: igual a </li>
       <li>NEQ - No es igual a</li>
       <li>GT - Mayor que</li>
       <li>LT - Menor que</li>
       <li>GTEQ: mayor o igual que</li>
       <li>LTEQ: menor o igual que</li>
       <li>CONTIENE: A contiene B si B es parte de A</li>
       <li>FULLTEXT: búsqueda de texto completo</li>
       <li>INTERRUPTOR DE ESTANQUEIDAD: A empieza por B si B es la parte inicial de A</li>
       <li>INTERRUPTOR DE ENCENDIDO: A termina con B si B es la parte final de A</li>
       <li>LIKE - Implementa el operador LIKE</li>
       <li>AND - Combinar varias afirmaciones</li>
      </ul> <p><strong></strong> Nota: Los operadores <em>GT, LT, GTEQ y LTEQ son aplicables a propiedades de tipo lineal como LONG, DOUBLE y DATE.</em></p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>pedidos<br /> </td>
   <td><p>Especifica los criterios de pedido para los resultados de búsqueda. Los criterios se definen en el formato JSON. Puede ordenar los resultados de búsqueda en más de un campo. Los resultados se ordenan en el orden en que aparecen los campos en la consulta.</p> <p>Por ejemplo,</p> <p>Para recuperar los resultados de consulta ordenados por propiedad title en orden ascendente, agregue el siguiente parámetro: </p> <p><code class="code">JSONArray orderingsArray=new JSONArray();
       JSONObject orderings=new JSONObject();
       orderings.put("name", "title");
       orderings.put("criteria", "ASC");
       orderingsArray.put(orderings);
       entityBuilder.add("orderings", orderingsArray.toString());</code></p>
    <ul>
     <li><strong>name</strong>: Especifica el nombre de la propiedad que se va a utilizar para ordenar los resultados de búsqueda.</li>
     <li><strong>criterios</strong>: Especifica el orden de los resultados. El atributo order acepta los siguientes valores:
      <ul>
       <li>ASC: utilice ASC para organizar los resultados en orden ascendente.<br /> </li>
       <li>DES: utilice DES para organizar los resultados en orden descendente.</li>
      </ul> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>includeXdp</td>
   <td>Especifica si se recupera el contenido binario o no. El <code>includeXdp</code> atributo es aplicable a recursos de tipo <code>FORM</code>, <code>PDFFORM</code>y <code>PRINTFORM</code>.</td>
  </tr>
  <tr>
   <td>assetType</td>
   <td>Especifica los tipos de recursos que se van a recuperar de todos los recursos publicados. Utilice el operador de barra vertical (|) para especificar varios tipos de recursos. Los tipos de recursos válidos son FORM, PDFFORM, PRINTFORM, RESOURCE y GUIDE.</td>
  </tr>
 </tbody>
</table>

## Solicitud de muestra {#sample-request}

```
func : searchForms
appPath : /content/dam/formsanddocuments/MyApplication23
cutPoints : title|description|author|status|creationDate|lastModifiedDate|activationDate|expiryDate|tags|allowedRenderFormat|formmodel
relation : NO_RELATION
includeXdp : false
maxSize : 10
offset : 0
returnCount : true
statements: [{"name":"name","value":"*Claim.xdp","operator":"CONTAINS"},
                {"name":"","value":"Expense","operator":"FULLTEXT"},
                {"name":"description","value":"ABCD*","operator":"CONTAINS"},
                {"name":"status","value":"false","operator":"EQ"},
                {"name":"lastModifiedDate","value":"01/09/2013","operator":"GTEQ"},
                {"name":"lastModifiedDate","value":"01/18/2013","operator":"LTEQ"}]
orderings:[{"name" :“lastModifiedDate“:”order”:”ASC”}]
```

## Respuesta de muestra {#sample-response}

```
[
{"resultCount":2},
    {"assetType":"FORM","name":"ExpenseClaim.xdp","id":"509fa2d5-e3c9-407b-b8dc-fa0ba08eb0ce",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDEFGIJK","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"5477a127-8bbf-4cec-8f81-2689e5cb4a15",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/Image.gif","resourceSize":0}],
       "status":false,"creationDate":1358429845623,"lastModifiedDate":1358429846771},
{"assetType":"FORM","name":"ExpenseClaim.xdp","id":"4312239b-b666-4d36-95bc-641b3a39ddd4",
       "path":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDefghijklm","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"118a2e3f-7097-4d8c-85d1-651306de284a",
       "path":"/content/dam/formsanddocuments/MyApplication23/Image.gif","resourceSize":0}],"status":false,
       "creationDate":1358429856690,"lastModifiedDate":1358430109023}
]
```

## Artículos relacionados

* [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* [Crear página del portal de formularios](/help/forms/using/creating-form-portal-page.md)
* [Lista de formularios en una página web mediante API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Uso del componente Borradores y envíos](/help/forms/using/draft-submission-component.md)
* [Personalización del almacenamiento de borradores y formularios enviados](/help/forms/using/draft-submission-component.md)
* [Ejemplo para integrar el componente de borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md)
* [Personalización de plantillas para componentes del portal de formularios](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introducción a la publicación de formularios en un portal](/help/forms/using/introduction-publishing-forms.md)