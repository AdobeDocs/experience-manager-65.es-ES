---
title: Referencia de predicados del generador de consultas
seo-title: Query Builder Predicate Reference
description: Referencia de predicado completa para la API de Query Builder.
seo-description: Complete predicate reference for the Query Builder API.
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
exl-id: 54b942f9-5dd9-4826-9a0a-028f2d7b8e41
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '2310'
ht-degree: 3%

---

# Referencia de predicados del generador de consultas{#query-builder-predicate-reference}

## General {#general}

* [root](#root)
* [grupo ](#group)
* [orderby](#orderby)

## Predicados {#predicates}

* [boolproperty](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [daterange](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [excludepaths](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [texto completo](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [language](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [mainasset](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [memberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodename](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [notexpired](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [path](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [propiedad](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangeproperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [relativedaterange](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [similar](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [etiqueta](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [type](/help/sites-developing/querybuilder-predicate-reference.md#type)

### boolproperty {#boolproperty}

Coincide con las propiedades BOOLEAN de JCR. Solo acepta los valores &quot; `true`&quot; y &quot; `false`&quot;. En el caso de &quot; `false`&quot;, coincidirá si la propiedad tiene el valor &quot; `false`&quot; o si no existe en absoluto. Esto puede resultar útil para comprobar los indicadores booleanos que solo se establecen cuando están activados.

El &quot; heredado `operation`&quot; no tiene significado.

Admite la extracción de facetas. Proporcionará bloques para cada `true` o `false` , pero solo para propiedades existentes.

#### Propiedades {#properties}

* **boolproperty**
ruta relativa a la propiedad, por ejemplo 
`myFeatureEnabled` o `jcr:content/myFeatureEnabled`

* **value**
valor para comprobar la propiedad, &quot; 
`true`&quot; o &quot; `false`&quot;

### contentfragment {#contentfragment}

Restringe el resultado a fragmentos de contenido.

No admite el filtrado.

No admite la extracción de facetas.

#### Propiedades {#properties-1}

* **contentfragment**
Se puede utilizar con cualquier valor para comprobar si hay fragmentos de contenido.

### dateComparison {#datecomparison}

Compara dos propiedades JCR DATE entre sí. Puede comprobar si son iguales, desiguales, buenos o buenos que o iguales.

Se trata de un predicado de solo filtrado y no puede aprovechar un índice de búsqueda.

#### Propiedades {#properties-2}

* **property1**

   ruta a la propiedad first date

* **property2**

   ruta a la propiedad de segunda fecha

* **operation**

   &quot; `equals`&quot; para coincidencia exacta, &quot; `!=`&quot; para la comparación de desigualdad, &quot; `greater`&quot; para la propiedad1 buena que la propiedad2, &quot; `>=`&quot; para la propiedad1 buena o igual a la propiedad2. El valor predeterminado es &quot; `equals`&quot;.

### daterange {#daterange}

Coincide con las propiedades de FECHA JCR con un intervalo de fecha y hora. Utiliza el formato ISO8601 para fechas y horas ( `YYYY-MM-DDTHH:mm:ss.SSSZ`) y permite también representaciones parciales, como `YYYY-MM-DD`. Alternativamente, la marca de tiempo se puede proporcionar como número de milisegundos desde 1970 en la zona horaria UTC, el formato de tiempo unix.

Puede buscar cualquier cosa entre dos marcas de tiempo, cualquier cosa más reciente o anterior que una fecha determinada, y también elegir entre intervalos abiertos e inclusivos.

Admite la extracción de facetas. Proporcionará bloques &quot;hoy&quot;, &quot;esta semana&quot;, &quot;este mes&quot;, &quot;últimos 3 meses&quot;, &quot;este año&quot;, &quot;el año pasado&quot; y &quot;anteriores al año pasado&quot;.

No admite el filtrado.

#### Propiedades {#properties-3}

* **propiedad**

   ruta relativa a un `DATE` propiedad, por ejemplo `jcr:lastModified`

* **lowerBound**

   fecha inferior enlazada para comprobar la propiedad, por ejemplo `2014-10-01`

* **lowerOperation**

   &quot; `>`&quot; (más reciente) o &quot; `>=`&quot; (en o más reciente), se aplica al `lowerBound`. El valor predeterminado es &quot; `>`&quot;.

* **upperBound**

   límite superior para comprobar la propiedad, por ejemplo `2014-10-01T12:15:00`

* **upperOperation**

   &quot; `<`&quot; (más antiguo) o &quot; `<=`&quot; (en o más años), se aplica al `upperBound`. El valor predeterminado es &quot; `<`&quot;.

* **timeZone**

   ID de la zona horaria que se debe usar cuando no se proporcione como cadena de fecha ISO-8601. El valor predeterminado es la zona horaria predeterminada del sistema.

### excludepaths {#excludepaths}

Excluye los nodos del resultado donde su ruta coincide con una expresión regular.

Se trata de un predicado de solo filtrado y no puede aprovechar un índice de búsqueda.

No admite la extracción de facetas.

#### Propiedades {#properties-4}

* **excludepaths**

   la expresión regular coincide con las rutas de resultados, excluyendo las coincidentes del resultado.

### texto completo {#fulltext}

Busca términos en el índice de texto completo.

No admite el filtrado.

No admite la extracción de facetas.

#### Propiedades {#properties-5}

* **texto completo**

   los términos de búsqueda de texto completo

* **relPath**

   la ruta relativa para buscar en la propiedad o subnodo. Esta propiedad es opcional.

### grupo  {#group}

Permite crear condiciones anidadas. Los grupos pueden contener grupos anidados. Todo en una consulta querybuilder está implícito en un grupo raíz, que puede tener `p.or` y `p.not` también.

Ejemplo para hacer coincidir una de las dos propiedades con un valor:

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Conceptualmente `(1_property` O `2_property)`.

Ejemplo para grupos anidados:

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

Esto busca el término &quot;**Administración**&quot; dentro de las páginas en `/content/geometrixx/en` o en activos en `/content/dam/geometrixx`.

Conceptualmente `fulltext AND ( (path AND type) OR (path AND type) )`. Tenga en cuenta que estas uniones O necesitan buenos índices para el rendimiento.

#### Propiedades {#properties-6}

* **p.o**

   si está configurado como &quot; `true`&quot;, solo debe coincidir un predicado del grupo. El valor predeterminado es &quot; `false`&quot;, lo que significa que todos deben coincidir

* **p.not**

   si está configurado como &quot; `true`&quot;, anula al grupo (el valor predeterminado es &quot; `false`&quot;)

* **&lt;predicate>**

   agrega predicados anidados

* **N_&lt;predicate>**

   agrega varios predicados anidados del mismo tiempo, como `1_property, 2_property, ...`

### hasPermission {#haspermission}

Restringe el resultado a elementos en los que la sesión actual tiene el valor especificado [Privilegios JCR.](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Se trata de un predicado de solo filtrado y no puede aprovechar un índice de búsqueda. No admite la extracción de facetas.

#### Propiedades {#properties-7}

* **hasPermission**

   privilegios JCR separados por comas que la sesión de usuario actual debe tener ALL para el nodo en cuestión; por ejemplo `jcr:write`, `jcr:modifyAccessControl`

### language {#language}

Busca páginas de CQ en un idioma específico. Esto examina tanto la propiedad idioma de la página como la ruta de la página, que a menudo incluye el idioma o la configuración regional en una estructura de sitio de nivel superior.

Se trata de un predicado de solo filtrado y no puede aprovechar un índice de búsqueda.

Admite la extracción de facetas. Proporcionará bloques para cada código de idioma único.

#### Propiedades {#properties-8}

* **language**

   Código de idioma ISO, por ejemplo &quot; `de`&quot;

### mainasset {#mainasset}

Comprueba si un nodo es un recurso principal DAM y no un subrecurso. Básicamente se trata de todos los nodos que no están dentro de un nodo de &quot;subactivos&quot;. Tenga en cuenta que esto no comprueba la existencia de `dam:Asset` tipo de nodo. Para usar este predicado, simplemente configure &quot; `mainasset=true`&quot; o &quot; `mainasset=false`&quot;, no hay más propiedades.

Se trata de un predicado de solo filtrado y no puede aprovechar un índice de búsqueda.

Admite la extracción de facetas. Proporcionará 2 bloques para los recursos principales y subactivos.

#### Propiedades {#properties-9}

* **mainasset**

   booleano, &quot; `true`&quot; para los activos principales, &quot; `false`&quot; para los subactivos

### memberOf {#memberof}

Busca elementos que son miembros de un [colección de recursos de sling](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Se trata de un predicado de solo filtrado y no puede aprovechar un índice de búsqueda. No admite la extracción de facetas.

#### Propiedades {#properties-10}

* **memberOf**

   ruta de la recopilación de recursos de Sling

### nodename {#nodename}

Coincide con los nombres de nodo de JCR.

Admite la extracción de facetas. Proporcionará bloques para cada nombre de nodo único (nombre de archivo).

#### Propiedades {#properties-11}

* **nodename**

   patrón de nombre de nodo que permite comodines: `*` = cualquier carácter o no, `?` = cualquier char, `[abc]` = solo caracteres entre corchetes

### notexpired {#notexpired}

Coincide con elementos comprobando si una propiedad JCR DATE es buena o igual a la hora del servidor actual. Se puede utilizar para comprobar un &quot; `expiresAt`&quot; como la propiedad date y limite solo a los que aún no han caducado ( `notexpired=true`) o que ya han caducado ( `notexpired=false`).

No admite el filtrado.

Admite la extracción de facetas del mismo modo que el predicado de intervalo de fechas.

#### Propiedades {#properties-12}

* **notexpired**

   booleano, &quot; `true`&quot; para no caducar todavía (fecha futura o igual), &quot; `false`&quot; para caducado (fecha en el pasado) (obligatorio)

* **propiedad**

   ruta relativa al `DATE` propiedad que se va a comprobar (obligatorio)

### orderby {#orderby}

Permite ordenar el resultado. Si se requiere ordenar por varias propiedades, este predicado debe agregarse varias veces utilizando el prefijo numérico, como `1_orderby=first`, `2_oderby=second`.

#### Propiedades {#properties-13}

* **orderby**

   o bien el nombre de la propiedad JCR indicado por un @ inicial, por ejemplo `@jcr:lastModified` o `@jcr:content/jcr:title`, u otro predicado de la consulta, por ejemplo `2_property`, sobre el que ordenar

* **ordenar**

   dirección de clasificación, ya sea &quot; `desc`&quot; para descendiente o &quot; `asc`&quot; para ascendente (predeterminado)

* **case**

   si está configurado como &quot; `ignore`&quot; hará que la clasificación no distinga mayúsculas de minúsculas, lo que significa que &quot;a&quot; viene antes que &quot;B&quot;; si está vacío o no se tiene en cuenta, la ordenación distingue entre mayúsculas y minúsculas, lo que significa que &quot;B&quot; viene antes que &quot;a&quot;.

### ruta {#path}

Búsquedas dentro de una ruta determinada.

No admite la extracción de facetas.

#### Propiedades {#properties-14}

* **path**

   patrón de ruta; según el valor exacto, el subárbol completo coincidirá (como anexar `//*` en xpath, pero tenga en cuenta que esto no incluye la ruta base) (exacto=false, predeterminado) o solo coincide una ruta exacta, que puede incluir caracteres comodín ( `*`); si se establece self, se buscará en todo el subárbol, incluido el nodo base

* **exacto**

   if `exact` tiene el valor true/on, la ruta exacta debe coincidir, pero puede contener caracteres comodín simples ( `*`), que coinciden con los nombres, pero no con &quot; `/`&quot;; si es false (predeterminado), se incluyen todos los descendientes (opcional)

* **plano**

   busca solo los elementos secundarios directos (como anexar &quot; `/*`&quot; en xpath) (solo se usa si &#39; `exact`&#39; no es verdadero, opcional)

* **self**

   busca en el subárbol pero incluye el nodo base dado como ruta (sin comodines)

### propiedad {#property}

Coincide con las propiedades JCR y sus valores.

Admite la extracción de facetas. Proporcionará bloques para cada valor de propiedad único en los resultados.

#### Propiedades {#properties-15}

* **propiedad**

   ruta relativa a la propiedad, por ejemplo `jcr:title`

* **value**

   valor para comprobar la propiedad; sigue al tipo de propiedad JCR a las conversiones de cadena

* **N_value**

   use `1_value`, `2_value`, ... para comprobar si hay varios valores (combinados con `OR` de forma predeterminada, con `AND` if and=true) (desde 5.3)

* **y**

   se establece en true para combinar varios valores ( `N_value`) con AND (desde 5.3)

* **operation**

   &quot;`equals`&quot; para coincidencia exacta (predeterminado), &quot; `unequals`&quot; para la comparación de desigualdad, &quot; `like`&quot; para usar la variable `jcr:like` función xpath (opcional), &quot; `not`&quot; sin coincidencia (p. ej. &quot;`not(@prop)`&quot; en xpath, se ignorará el valor param) o &quot; `exists`&quot; para la comprobación de existencia (el valor puede ser true - la propiedad debe existir, el valor predeterminado - o false - igual que &quot; `not`&quot;)

* **depth**

   número de niveles comodín debajo de los cuales puede existir la propiedad/ruta relativa (por ejemplo, `property=size depth=2` comprobará el nodo/tamaño, nodo/&amp;ast;/size y nodo/&amp;ast;/&amp;ast;/size)

### rangeproperty {#rangeproperty}

Coincide con una propiedad JCR con un intervalo. Esto se aplica a propiedades con tipos lineales como `LONG`, `DOUBLE` y `DECIMAL`. Para `DATE` consulte el predicado de intervalo de fechas que ha optimizado la entrada de formato de fecha.

Puede definir un límite inferior y un límite superior o solo uno de ellos. La operación (p. ej. &quot;menor que&quot; o &quot;menor o igual que&quot;) también se pueden especificar individualmente para los límites inferior y superior.

No admite la extracción de facetas.

#### Propiedades {#properties-16}

* **propiedad**

   ruta relativa a la propiedad

* **lowerBound**

   límite inferior para comprobar la propiedad

* **lowerOperation**

   &quot; `>`&quot; (predeterminado) o &quot; `>=`&quot;, se aplica al `lowerValue`

* **upperBound**

   límite superior para comprobar la propiedad

* **upperOperation**

   &quot; `<`&quot; (predeterminado) o &quot; `<=`&quot;, se aplica al `lowerValue`

* **decimal**

   &quot; `true`&quot; si la propiedad marcada es del tipo Decimal

### relativedaterange {#relativedaterange}

Coincide `JCR DATE` propiedades frente a un intervalo de fecha y hora utilizando desplazamientos de tiempo relativos a la hora actual del servidor. Puede especificar `lowerBound` y `upperBound` uso de un valor milisegundo o de la sintaxis bugzilla `1s 2m 3h 4d 5w 6M 7y` (un segundo, dos minutos, tres horas, cuatro días, cinco semanas, seis meses, siete años). Prefijo con &quot; `-`&quot; para indicar un desplazamiento negativo antes de la hora actual. Si solo especifica `lowerBound` o `upperBound`, el otro tendrá el valor predeterminado 0, es decir, la hora actual.

Por ejemplo:

* `upperBound=1h` (y no `lowerBound`) seleccionaría cualquier cosa en la siguiente hora
* `lowerBound=-1d` (y no `upperBound`) seleccionaría cualquier cosa en las últimas 24 horas
* `lowerBound=-6M` y `upperBound=-3M` seleccionaría cualquier cosa de 6 meses a 3 meses de edad
* `lowerBound=-1500` y `upperBound=5500` seleccionaría cualquier cosa entre 1500 milisegundos en el pasado y 5500 milisegundos en el futuro
* `lowerBound=1d` y `upperBound=2d` seleccionaría cualquier cosa en el día siguiente a mañana

Tenga en cuenta que no toma años bisiestos en consideración y que todos los meses son 30 días.

No admite el filtrado.

Admite la extracción de facetas del mismo modo que el predicado de intervalo de fechas.

#### Propiedades {#properties-17}

* **upperBound**

   límite de fecha superior en milisegundos o `1s 2m 3h 4d 5w 6M 7y` (un segundo, dos minutos, tres horas, cuatro días, cinco semanas, seis meses, siete años) en relación con la hora del servidor actual, utilice &quot;-&quot; para obtener una compensación negativa

* **lowerBound**

   límite de fecha inferior en milisegundos o `1s 2m 3h 4d 5w 6M 7y` (un segundo, dos minutos, tres horas, cuatro días, cinco semanas, seis meses, siete años) en relación con la hora del servidor actual, utilice &quot;-&quot; para obtener una compensación negativa

### root {#root}

Grupo de predicados raíz. Admite todas las funciones de un grupo y permite establecer parámetros de consulta globales.

El nombre &quot;root&quot; nunca se utiliza en una consulta, está implícito.

#### Propiedades {#properties-18}

* **p.offset**

   número que indica el inicio de la página de resultados, es decir, cuántos elementos se deben omitir

* **p.limit**

   número que indica el tamaño de la página

* **p.supongoTotal**

   recomendado: evite calcular el total del resultado completo, que puede resultar costoso; o bien un número que indica el total máximo que se va a contar (por ejemplo, 1000, un número que proporciona a los usuarios suficientes comentarios sobre el tamaño aproximado y los números exactos para obtener resultados más pequeños) o &quot; `true`&quot; para contar solamente hasta el mínimo necesario `p.offset` + `p.limit`

* **p.excerpt**

   si está configurado como &quot; `true`&quot;, incluir extracto de texto completo en el resultado

* **p.hits**

   (solo para el servlet JSON) seleccione la forma en que se escriben las visitas como JSON, con estas visitas estándar (ampliables mediante el servicio ResultHitWriter):

   * **simple**:

      elementos mínimos como `path`, `title`, `lastmodified`, `excerpt` (si está configurado)

   * **completa**:

      renderización JSON de sling del nodo, con `jcr:path` indicando la ruta de la visita: de forma predeterminada, solo enumera las propiedades directas del nodo, incluya un árbol más profundo con `p.nodedepth=N`, con 0 que significa todo el subárbol infinito; add `p.acls=true` para incluir los permisos JCR de la sesión actual en el elemento de resultado dado (asignaciones: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)

   * **selectivo**:

      solo las propiedades especificadas en `p.properties`, que es una lista de rutas relativas separadas por espacios (utilice &quot;+&quot; en las direcciones URL); si la ruta relativa tiene una profundidad > 1, se representarán como objetos secundarios; la propiedad especial jcr:path incluye la ruta de la visita

### savedquery {#savedquery}

Incluye todos los predicados de una consulta de querybuilder persistente en la consulta actual como un predicado de subgrupo.

Tenga en cuenta que esto no ejecutará una consulta adicional sino que extenderá la consulta actual.

Las consultas se pueden mantener mediante programación mediante `QueryBuilder#storeQuery()`. El formato puede ser una propiedad String de varias líneas o una `nt:file` que contiene la consulta como archivo de texto en formato de propiedades de Java.

No admite la extracción de facetas para los predicados de la consulta guardada.

#### Propiedades {#properties-19}

* **savedquery**

   ruta a la consulta guardada (propiedad String o `nt:file` node)

### similar {#similar}

Búsqueda por similitudes usando JCR XPath&#39;s `rep:similar()`.

No admite el filtrado. No admite la extracción de facetas.

#### Propiedades {#properties-20}

* **similar**
ruta absoluta al nodo para el cual encontrar nodos similares

* **local**
una ruta relativa a un nodo descendiente o 
`.` para el nodo actual (opcional, el valor predeterminado es &quot; `.`&quot;)

### etiqueta {#tag}

Busca contenido etiquetado con una o más etiquetas, especificando las rutas de título de las etiquetas.

Admite la extracción de facetas. Proporcionará bloques para cada etiqueta única, utilizando la ruta de título de la etiqueta actual.

#### Propiedades {#properties-21}

* **etiqueta**

   ruta de título de etiqueta que se va a buscar, por ejemplo &quot;Propiedades de los recursos : Orientación / Horizontal&quot;

* **N_value**

   use `1_value`, `2_value`, ... para comprobar si hay varias etiquetas (combinadas con `OR` de forma predeterminada, con `AND` if and=true) (desde 5.6)

* **propiedad**

   propiedad (o ruta relativa a la propiedad) que se va a ver (valor predeterminado) `cq:tags`&quot;)

### tagid {#tagid}

Busca contenido etiquetado con una o más etiquetas, especificando los ID de las etiquetas.

Admite la extracción de facetas. Proporcionará bloques para cada etiqueta única, utilizando su ID de etiqueta actual.

#### Propiedades {#properties-22}

* **tagid**

   id de etiqueta que se va a buscar, por ejemplo &quot; `properties:orientation/landscape`&quot;

* **N_value**

   use `1_value`, `2_value`, ... para comprobar si hay varios identificadores (combinados con `OR` de forma predeterminada, con `AND` if and=true) (desde 5.6)

* **propiedad**

   propiedad (o ruta relativa a la propiedad) que se va a ver (valor predeterminado) `cq:tags`&quot;)

### tagsearch {#tagsearch}

Busca contenido etiquetado con una o más etiquetas, especificando palabras clave. Primero buscará las etiquetas que contengan estas palabras clave en sus títulos y luego restringirá el resultado a solo los elementos etiquetados con ellas.

No admite la extracción de facetas.

#### Propiedades {#Properties-1}

* **tagsearch**

   palabra clave que se busca en los títulos de etiquetas

* **propiedad**

   propiedad (o ruta relativa a la propiedad) que se va a ver (valor predeterminado) `cq:tags`&quot;)

* **lang**

   para buscar solo en un título de etiqueta localizado determinado (p. ej. &quot; `de`&quot;)

* **all**

   (bool) buscar todo el texto completo de la etiqueta, es decir, todos los títulos, descripción, etc. (tiene prioridad sobre &quot;l&quot; `ang`&quot;)

### type {#type}

Restringe los resultados a un tipo de nodo JCR específico, tanto del tipo de nodo principal como del tipo de mezcla. Esto también encontrará subtipos de ese tipo de nodo. Tenga en cuenta que los índices de búsqueda del repositorio deben cubrir los tipos de nodos para una ejecución eficiente.

Admite la extracción de facetas. Proporcionará bloques para cada tipo único en los resultados.

#### Propiedades {#Properties-2}

* **type**

   tipo de nodo o nombre de mezcla que se va a buscar, por ejemplo `cq:Page`
