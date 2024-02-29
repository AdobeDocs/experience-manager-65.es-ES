---
title: Solución de problemas de consultas lentas
description: Aprenda a solucionar problemas de consultas lentas en Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 3405cdd3-3d1b-414d-9931-b7d7b63f0a6f
source-git-commit: 4289c68feb51842b5649f7cff73c5c4bc38add6c
workflow-type: tm+mt
source-wordcount: '2236'
ht-degree: 0%

---

# Solución de problemas de consultas lentas{#troubleshooting-slow-queries}

## Clasificaciones de consulta lenta {#slow-query-classifications}

AEM Existen tres clasificaciones principales de consultas lentas en la, enumeradas por gravedad:

1. **Consultas sin índice**

   * Consultas que lo hacen **no** resolver en un índice y recorrer el contenido de JCR para recopilar resultados

1. **Consultas mal restringidas (o con ámbitos)**

   * Consultas que se resuelven en un índice, pero que deben atravesar todas las entradas de índice para recopilar resultados

1. **Consultas de conjunto de resultados grandes**

   * Consultas que devuelven grandes cantidades de resultados

Las dos primeras clasificaciones de consultas (sin índice y mal restringidas) son lentas. Son lentos porque obligan al motor de consultas de Oak a inspeccionar cada uno **potencial** result (nodo de contenido o entrada de índice) para identificar qué pertenecen a la **real** conjunto de resultados.

El acto de inspeccionar cada resultado potencial es lo que se conoce como Traversing.

Dado que cada resultado potencial debe inspeccionarse, el coste para determinar el conjunto de resultados reales aumenta linealmente con el número de resultados potenciales.

Añadir restricciones de consulta e índices de ajuste permite almacenar los datos del índice en un formato optimizado, lo que permite una recuperación rápida de los resultados y reduce o elimina la necesidad de realizar una inspección lineal de los conjuntos de resultados potenciales.

AEM De forma predeterminada, en la versión 6.3, cuando se alcanza un recorrido de 100 000, la consulta falla y genera una excepción. AEM AEM Este límite no existe de forma predeterminada en versiones de la versión de la aplicación anteriores a la 6.3, pero se puede establecer mediante la configuración OSGi de la configuración del motor de consultas de Apache Jackrabbit y el bean JMX de QueryEngineSettings (propiedad LimitReads).

### Detección de consultas sin índice {#detecting-index-less-queries}

#### Durante el desarrollo {#during-development}

Explicar **todo** consultas y asegurarse de que sus planes de consultas no contienen el **/&amp;ast; travesía** explicación en ellos. Ejemplo de plan de consulta de recorrido:

* **PLAN:** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### Posterior a la implementación {#post-deployment}

* Monitorización de `error.log` para consultas de recorrido sin índice:

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * Este mensaje solo se registra si no hay ningún índice disponible y si la consulta atraviesa potencialmente muchos nodos. Los mensajes no se registran si hay un índice disponible, pero la cantidad a recorrer es pequeña y, por lo tanto, rápida.

* AEM Visitar el sitio web de [Rendimiento de consultas](/help/sites-administering/operations-dashboard.md#query-performance) consola de operaciones y [Explicar](/help/sites-administering/operations-dashboard.md#explain-query) consultas lentas que buscan explicaciones de consulta de recorrido o sin índice.

### Detección de consultas mal restringidas {#detecting-poorly-restricted-queries}

#### Durante el desarrollo {#during-development-1}

Explique todas las consultas y asegúrese de que se resuelven en un índice ajustado para que coincida con las restricciones de propiedad de la consulta.

* La cobertura ideal del plan de consulta tiene `indexRules` para todas las restricciones de propiedad y, como mínimo, para las restricciones de propiedad más estrictas de la consulta.
* Las consultas que ordenan resultados deben resolverse en un índice de propiedades de Lucene con reglas de índice para las propiedades ordenadas por que establecen `orderable=true.`

#### Por ejemplo, la opción predeterminada `cqPageLucene` no tiene una regla de índice para `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

Antes de añadir la regla de índice cq:tags

* **cq:etiquetas Regla de índice**

   * No existe de forma predeterminada

* **Consulta del Generador de consultas**

  ```js
  type=cq:Page
  property=jcr:content/cq:tags
  property.value=my:tag
  ```

* **Plan de consulta**

  `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

Esta consulta se resuelve en `cqPageLucene` índice, pero como no existe ninguna regla de índice de propiedad para `jcr:content` o `cq:tags`, cuando se evalúe esta restricción, todos los registros de `cqPageLucene` el índice se comprueba para determinar una coincidencia. Como tal, si el índice contiene 1 millón `cq:Page` , se comprueban 1 millón de registros para determinar el conjunto de resultados.

Después de agregar la regla de índice cq:tags

* **cq:etiquetas Regla de índice**

  ```js
  /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
  @name=jcr:content/cq:tags
  @propertyIndex=true
  ```

* **Consulta del Generador de consultas**

  ```js
  type=cq:Page
  property=jcr:content/cq:tags
  property.value=myTagNamespace:myTag
  ```

* **Plan de consulta**

  `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

Adición de indexRule para `jcr:content/cq:tags` en el `cqPageLucene` index permite `cq:tags` datos que se van a almacenar de forma optimizada.

Cuando una consulta con `jcr:content/cq:tags` Si se realiza la restricción, el índice puede buscar los resultados por valor. Eso significa que si 100 `cq:Page` los nodos tienen `myTagNamespace:myTag` como valor, solo se devuelven esos 100 resultados, y los otros 999.000 se excluyen de las comprobaciones de restricción, mejorando el rendimiento en un factor de 10.000.

Más restricciones de consulta reducen los conjuntos de resultados aptos y optimizan aún más la optimización de la consulta.

Del mismo modo, sin una regla de índice adicional para `cq:tags` , incluso una consulta de texto completo con una restricción en `cq:tags` tendría un mal rendimiento, ya que los resultados del índice devolverían todas las coincidencias de texto completo. La restricción de cq:tags se filtraría después de ella.

Otra causa del filtrado posterior a los índices son las Listas de control de acceso, que a menudo se pierden durante el desarrollo. Intente asegurarse de que la consulta no devuelva rutas que puedan ser inaccesibles para el usuario. Esto se puede hacer mediante una mejor estructura de contenido y proporcionando restricciones de ruta relevantes en la consulta.

Una forma útil de identificar si el índice Lucene devuelve muchos resultados para devolver un pequeño subconjunto como resultado de la consulta es habilitar los registros de DEPURACIÓN para `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex`. Al hacerlo, puede ver cuántos documentos se cargan desde el índice. La cantidad de resultados posibles frente a la cantidad de documentos cargados no debería ser desproporcionada. Para obtener más información, consulte [Registro](/help/sites-deploying/configure-logging.md).

#### Posterior a la implementación {#post-deployment-1}

* Monitorización de `error.log` para consultas de recorrido:

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* AEM Visitar el sitio web de [Rendimiento de consultas](/help/sites-administering/operations-dashboard.md#query-performance) consola de operaciones y [Explicar](/help/sites-administering/operations-dashboard.md#explain-query) consultas lentas que buscan planes de consulta que no resuelven las restricciones de propiedad de consulta en reglas de propiedad de índice.

### Detección de consultas de conjuntos de resultados grandes {#detecting-large-result-set-queries}

#### Durante el desarrollo {#during-development-2}

Establezca umbrales bajos para oak.queryLimitInMemory (por ejemplo, 10000) y oak.queryLimitReads (por ejemplo, 5000) y optimice la consulta costosa al alcanzar una excepción UnsupportedOperationException que dice &quot;La consulta lee más de x nodos...&quot;

La configuración de umbrales bajos ayuda a evitar consultas que consuman muchos recursos (es decir, que no estén respaldadas por ningún índice o que estén respaldadas por un índice que cubra menos). Por ejemplo, una consulta que lee un millón de nodos produciría una gran cantidad de E/S y afectaría negativamente al rendimiento general de la aplicación. Por lo tanto, cualquier consulta que falle debido a límites superiores debe analizarse y optimizarse.

#### Posterior a la implementación {#post-deployment-2}

* Monitorice los registros para consultas que activen un recorrido de nodos grande o un gran consumo de memoria de montón: &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Optimice la consulta para reducir el número de nodos atravesados.

* Monitorice los registros para consultas que activen un gran consumo de memoria:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Optimice la consulta para reducir el consumo de memoria.

AEM AEM Para las versiones 6.0 - 6.2, puede ajustar el umbral para el recorrido de nodos a través de los parámetros JVM en el script de inicio de la para evitar que las consultas grandes se sobrecarguen en el entorno. Los valores recomendados son:

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

AEM En 6.3, los dos parámetros anteriores están preconfigurados de forma predeterminada y se pueden modificar mediante OSGi QueryEngineSettings.

Encontrará más información en : [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Ajuste del rendimiento de consultas {#query-performance-tuning}

AEM El lema de la optimización del rendimiento de las consultas en la es:

**&quot;Cuantas más restricciones, mejor&quot;.**

A continuación se describen los ajustes recomendados para garantizar el rendimiento de la consulta. En primer lugar, ajuste la consulta, una actividad menos intrusiva, y luego, si es necesario, ajuste las definiciones de índice.

### Ajuste de la instrucción de consulta {#adjusting-the-query-statement}

AEM Compatibilidad con los siguientes idiomas de consulta:

* Query Builder
* JCR-SQL2
* XPath

AEM El siguiente ejemplo utiliza Query Builder porque es el lenguaje de consulta más común utilizado por los desarrolladores de, aunque los mismos principios se aplican a JCR-SQL2 y XPath.

1. Añada una restricción nodetype para que la consulta se resuelva en un índice de propiedades de Lucene existente.

* **Consulta no optimizada**

  ```js
  property=jcr:content/contentType
  property.value=article-page
  ```

* **Consulta optimizada**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.value=article-page
  ```

  AEM Las consultas que carecen de una restricción de tipo de nodo obligan a los usuarios a asumir el valor de `nt:base` AEM nodetype, del que todos los nodos de la son un subtipo, no da como resultado ninguna restricción nodetype.

  Configuración `type=cq:Page` restringe esta consulta únicamente a `cq:Page` AEM , y resuelve la consulta para que se resuelva en el elemento cqPageLucene, limitando los resultados a un subconjunto de nodos (solo `cq:Page` AEM nodes) en la.

1. Ajuste la restricción nodetype de la consulta para que la consulta se resuelva en un índice de propiedades de Lucene existente.

* **Consulta no optimizada**

  ```js
  type=nt:hierarchyNode
  property=jcr:content/contentType
  property.value=article-page
  ```

* **Consulta optimizada**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.value=article-page
  ```

  `nt:hierarchyNode` es el tipo de nodo principal de `cq:Page`. Suponiendo `jcr:content/contentType=article-page` solo se aplica a `cq:Page` nodos mediante la aplicación personalizada de Adobe, esta consulta solo devuelve `cq:Page` nodos donde `jcr:content/contentType=article-page`. Sin embargo, este flujo es una restricción subóptima, ya que:

   * Otros nodos heredan de `nt:hierarchyNode` (por ejemplo, `dam:Asset`) añadiendo innecesariamente al conjunto de resultados potenciales.
   * AEM No existe ningún índice proporcionado por el usuario para `nt:hierarchyNode`, sin embargo, ya que hay un índice proporcionado para `cq:Page`.

  Configuración `type=cq:Page` restringe esta consulta únicamente a `cq:Page` AEM AEM , y resuelve la consulta para que se ejecute en cqPageLucene, limitando los resultados a un subconjunto de nodos (solo nodos cq:Page) en la.

1. O bien, ajuste las restricciones de propiedades para que la consulta se resuelva en un índice de propiedades existente.

* **Consulta no optimizada**

  ```js
  property=jcr:content/contentType
  property.value=article-page
  ```

* **Consulta optimizada**

  ```js
  property=jcr:content/sling:resourceType
  property.value=my-site/components/structure/article-page
  ```

  Cambiar la restricción de propiedad de `jcr:content/contentType` (un valor personalizado) a la propiedad conocida `sling:resourceType` permite que la consulta se resuelva en el índice de propiedades `slingResourceType` que indexa todo el contenido por `sling:resourceType`.

  Los índices de propiedades (a diferencia de los Índices de propiedades de Lucene) se utilizan mejor cuando la consulta no distingue por tipo de nodo y una sola restricción de propiedad domina el conjunto de resultados.

1. Añada a la consulta la restricción de ruta más estricta posible. Por ejemplo, prefiera `/content/my-site/us/en` sobre `/content/my-site`, o `/content/dam` sobre `/`.

* **Consulta no optimizada**

  ```js
  type=cq:Page
  path=/content
  property=jcr:content/contentType
  property.value=article-page
  ```

* **Consulta optimizada**

  ```js
  type=cq:Page
  path=/content/my-site/us/en
  property=jcr:content/contentType
  property.value=article-page
  ```

  Alcance de la restricción de ruta desde `path=/content`hasta `path=/content/my-site/us/en` permite que los índices reduzcan el número de entradas de índice que deben inspeccionarse. Cuando la consulta puede restringir bien la ruta, más allá de lo siguiente `/content` o `/content/dam`, asegúrese de que el índice tenga `evaluatePathRestrictions=true`.

  Nota con `evaluatePathRestrictions` aumenta el tamaño del índice.

1. Cuando sea posible, evite las funciones de consulta y las operaciones de consulta como: `LIKE` y `fn:XXXX` a medida que sus costes se escalan con el número de resultados basados en restricciones.

* **Consulta no optimizada**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.operation=like
  property.value=%article%
  ```

* **Consulta optimizada**

  ```js
  type=cq:Page
  fulltext=article
  fulltext.relPath=jcr:content/contentType
  ```

  La condición LIKE es lenta de evaluar porque no se puede utilizar ningún índice si el texto comienza con un comodín (&quot;%...&#39;). La condición jcr:contains permite utilizar un índice de texto completo y, por lo tanto, se prefiere. Requiere que el índice de propiedades de Lucene resuelto tenga indexRule para `jcr:content/contentType` con `analayzed=true`.

  Uso de funciones de consulta como `fn:lowercase(..)` puede ser más difícil de optimizar, ya que no hay equivalentes más rápidos (fuera de configuraciones del analizador de índices más complejas y molestas). Es mejor identificar otras restricciones de ámbito para mejorar el rendimiento general de la consulta, lo que requiere que las funciones funcionen con el menor conjunto posible de resultados potenciales.

1. ***Este ajuste es específico del Generador de consultas y no se aplica a JCR-SQL2 o XPath.***

   Uso [Supuesto total de Query Builder](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) cuando el conjunto completo de resultados es **no** inmediatamente necesario.

   * **Consulta no optimizada**

     ```js
     type=cq:Page
     path=/content
     ```

   * **Consulta optimizada**

     ```js
     type=cq:Page
     path=/content
     p.guessTotal=100
     ```

   En los casos en los que la ejecución de la consulta es rápida pero el número de resultados es grande, p. `guessTotal` es una optimización crítica para las consultas del Generador de consultas.

   `p.guessTotal=100` indica a Query Builder que solo recopile los primeros 100 resultados. Y, para establecer un indicador booleano que indique si existe al menos un resultado más (pero no cuántos más, ya que el recuento de este número resulta en lentitud). Esta optimización sobresale en los casos de uso de paginación o carga infinita, donde solo se muestra un subconjunto de resultados de forma incremental.

## Ajuste de índice existente {#existing-index-tuning}

1. Si la consulta óptima se resuelve en un índice de propiedades, no queda nada por hacer, ya que los índices de propiedades son mínimamente ajustables.
1. De lo contrario, la consulta debe resolverse en un índice de propiedades de Lucene. Si no se puede resolver ningún índice, vaya a Creación de un índice.
1. Si es necesario, convierta la consulta a XPath o JCR-SQL2.

   * **Consulta del Generador de consultas**

     ```js
     query type=cq:Page
     path=/content/my-site/us/en
     property=jcr:content/contentType
     property.value=article-page
     orderby=@jcr:content/publishDate
     orderby.sort=desc
     ```

   * **XPath generado a partir de la consulta del Generador de consultas**

     ```js
     /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
     ```

1. Proporcione el XPath (o JCR-SQL2) al generador de definiciones de índice de Oak en `https://oakutils.appspot.com/generate/index` para poder generar la definición del índice de propiedades de Lucene optimizada. <!-- The above URL is 404 as of April 24, 2023 -->

   **Definición del índice de propiedades Lucene generada**

   ```xml
   - evaluatePathRestrictions = true
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules
       + cq:Page
           + properties
           + contentType
               - name = "jcr:content/contentType"
               - propertyIndex = true
           + publishDate
               - ordered = true
               - name = "jcr:content/publishDate"
   ```

1. Combine manualmente la definición generada en el índice de propiedades de Lucene existente de forma aditiva. Tenga cuidado de no eliminar las configuraciones existentes, ya que pueden utilizarse para satisfacer otras consultas.

   1. Busque el índice de propiedades de Lucene existente que cubre cq:Page (mediante el Administrador de índices). En este caso, `/oak:index/cqPageLucene`.
   1. Identifique el delta de configuración entre la definición de índice optimizada (Paso #4) y el índice existente (/oak:index/cqPageLucene), y agregue las configuraciones que faltan del índice optimizado a la definición de índice existente.
   1. AEM Prácticas recomendadas de indexación por reindexación, se debe realizar una actualización o reindexación en función de si el contenido existente podría verse afectado por este cambio de configuración de índice.

## Crear un nuevo índice {#create-a-new-index}

1. Compruebe que la consulta no se resuelve en un índice de propiedades de Lucene existente. Si es así, consulte la sección anterior sobre ajuste y índice existente.
1. Si es necesario, convierta la consulta a XPath o JCR-SQL2.

   * **Consulta del Generador de consultas**

     ```js
     type=myApp:Author
     property=firstName
     property.value=ira
     ```

   * **XPath generado a partir de la consulta del Generador de consultas**

     ```js
     //element(*, myApp:Page)[@firstName = 'ira']
     ```

1. Proporcione el XPath (o JCR-SQL2) al generador de definiciones de índice de Oak en `https://oakutils.appspot.com/generate/index` para poder generar la definición del índice de propiedades de Lucene optimizada. <!-- The above URL is 404 as of April 24, 2023 -->

   **Definición del índice de propiedades Lucene generada**

   ```xml
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules
       + myApp:AuthorModel
           + properties
           + firstName
               - name = "firstName"
               - propertyIndex = true
   ```

1. Implemente la definición de índice de propiedades de Lucene generada.

   AEM Agregue la definición XML proporcionada por el Generador de definiciones de índice de Oak para el nuevo índice al proyecto de que administra las definiciones de índice de Oak (recuerde, trate las definiciones de índice de Oak como código, ya que el código depende de ellas).

   AEM Implemente y pruebe el nuevo índice siguiendo el ciclo de vida habitual de desarrollo de software de la aplicación, y compruebe que la consulta se resuelve en el índice y que la consulta es eficaz.

   AEM En la implementación inicial de este índice, se rellena con los datos necesarios para que se rellene de manera correcta.

## ¿Cuándo son correctas las consultas sin índice y las consultas de recorrido? {#when-index-less-and-traversal-queries-are-ok}

AEM Debido a la arquitectura de contenido altamente flexible, es difícil predecir y garantizar que las transiciones de las estructuras de contenido no evolucionen con el tiempo para ser inaceptablemente grandes.

Por lo tanto, asegúrese de que los índices satisfacen las consultas, excepto si la combinación de restricción de ruta y restricción de tipo de nodo garantiza que **nunca se atraviesan menos de 20 nodos.**

## Herramientas de desarrollo de consultas {#query-development-tools}

### Adobe compatible {#adobe-supported}

* **Query Builder Debugger**

   * Interfaz de usuario web para ejecutar consultas del Generador de consultas y generar el XPath de compatibilidad (para su uso en Explicar consulta o Generador de definiciones de índice de Oak).
   * AEM En el [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite - Herramienta de consulta**

   * Interfaz de usuario web para ejecutar consultas XPath y JCR-SQL2.
   * AEM En el [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) > Herramientas > Consulta...

* **[Explicar consulta](/help/sites-administering/operations-dashboard.md#explain-query)**

   * AEM Panel de operaciones de la que proporciona una explicación detallada (plan de consulta, tiempo de consulta y número de resultados) para cualquier consulta XPATH o JCR-SQL2 determinada.

* **[Consultas lentas/populares](/help/sites-administering/operations-dashboard.md#query-performance)**

   * AEM AEM Un panel de operaciones de la lista de las operaciones lentas y populares recientes ejecutadas en el.

* **[Administrador de índices](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * AEM AEM Interfaz de usuario web de operaciones de que muestra los índices de la instancia de la aplicación; facilita la comprensión de qué índices existen; se puede dirigir o aumentar.

* **[Registro](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Registro de Query Builder

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`

   * Registro de ejecución de consulta de Oak

      * `DEBUG @ org.apache.jackrabbit.oak.query`

* **Configuración del motor de consultas de Apache Jackrabbit Configuración OSGi**

   * Configuración de OSGi que configura el comportamiento de error para consultas de recorrido.
   * AEM En el [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **MBean JMX de NodeCounter**

   * AEM MBean de JMX utilizado para estimar el número de nodos en árboles de contenido en la.
   * AEM En el [/system/console/jmx/org.apache.jackrabbit.oak%3Nombre%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### Admitido por la comunidad {#community-supported}

* **Generador de definiciones de índice de Oak en`https://oakutils.appspot.com/generate/index`** <!-- The above URL is 404 as of April 24, 2023 -->

   * Genere un índice de propiedades de Lucence óptimo a partir de instrucciones de consulta XPath o JCR-SQL2.

* **_AEM Complemento de Chrome de_** <!-- For whatever reason, the URL to this extension was causing too many redirects when doing the request so it was removed entirely to get rid of the error; users can easily look up the extension in Google instead. DO NOT ADD THE URL AGAIN!-->

   * El _AEM Complemento de Chrome de_ es una extensión del explorador web Google Chrome que expone los datos de registro por solicitud, incluidas las consultas de ejecución y sus planes de consulta, en la consola de herramientas de desarrollo del explorador.
   * Requiere que instale y habilite [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) AEM en la.
