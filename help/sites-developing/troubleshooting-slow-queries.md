---
title: Resolución de problemas de Consultas lentas
seo-title: Resolución de problemas de Consultas lentas
description: nulo
seo-description: nulo
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
translation-type: tm+mt
source-git-commit: 6d8680bcfb03197ac33bc7efb0e40796e38fef20
workflow-type: tm+mt
source-wordcount: '2267'
ht-degree: 0%

---


# Resolución de problemas de Consultas lentas{#troubleshooting-slow-queries}

## Clasificaciones de Consultas lentas {#slow-query-classifications}

Existen tres clasificaciones principales de consultas lentas en AEM, enumeradas por gravedad:

1. **Consultas sin índice**

   * Consultas que **no** se resuelven en un índice y atraviesan el contenido del JCR para recopilar resultados

1. **Consultas poco restringidas (o con ámbito)**

   * Consultas que se resuelven en un índice, pero que deben recorrer todas las entradas de índice para recopilar resultados

1. **Consultas de conjuntos de resultados grandes**

   * Consultas que devuelven un gran número de resultados

Las dos primeras clasificaciones de consultas (sin índice y mal restringidas) son lentas, porque obligan al motor de consulta Oak a inspeccionar cada **resultado potencial** (nodo de contenido o entrada de índice) para identificar qué pertenece al conjunto de resultados **real**.

El acto de inspeccionar cada posible resultado es lo que se conoce como Traversing.

Dado que debe inspeccionarse cada posible resultado, el costo para determinar el resultado real crece de manera lineal con el número de posibles resultados.

Añadir las restricciones de consulta y los índices de ajuste permite almacenar los datos del índice en un formato optimizado que permite una rápida recuperación de los resultados y reduce o elimina la necesidad de realizar una inspección lineal de los posibles conjuntos de resultados.

En AEM 6.3, de forma predeterminada, cuando se alcanza un recorrido de 100.000, la consulta falla y emite una excepción. Este límite no existe de forma predeterminada en las versiones AEM anteriores a AEM 6.3, pero se puede establecer mediante la configuración OSGi de Apache Jackrabbit Engine y el grano JMX QueryEngineSettings (propiedad LimitReads).

### Detección de Consultas sin índice {#detecting-index-less-queries}

#### Durante el desarrollo {#during-development}

Explicar **todas** consultas y asegurarse de que sus planes de consulta no contengan la **/&amp;ast; explicación de traverse** en ellos. Ejemplo de plan de consulta de recorrido:

* **PLAN:** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### Post-implementación {#post-deployment}

* Monitoree el `error.log` para consultas de recorrido sin índice:

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * Este mensaje solo se registra si no hay ningún índice disponible y si la consulta potencialmente atraviesa muchos nodos. Los mensajes no se registran si hay un índice disponible, pero la cantidad que se va a recorrer es pequeña y, por lo tanto, rápida.

* Visite la consola de operaciones [Rendimiento de Consulta](/help/sites-administering/operations-dashboard.md#query-performance) de AEM y [Explicar](/help/sites-administering/operations-dashboard.md#explain-query) consultas lentas que buscan explicaciones de consulta de índice o de recorrido.

### Detección de Consultas mal restringidas {#detecting-poorly-restricted-queries}

#### Durante el desarrollo {#during-development-1}

Explicar todas las consultas y asegurarse de que se resuelven en un índice ajustado para coincidir con las restricciones de propiedad de la consulta.

* La cobertura del plan de consulta ideal tiene `indexRules` para todas las restricciones de propiedad y, como mínimo, para las restricciones de propiedad más estrictas de la consulta.
* Las consultas que ordenan los resultados deben resolverse en un Índice de propiedades de Lucene con reglas de índice para las propiedades ordenadas por propiedades que establecen `orderable=true.`

#### Por ejemplo: el `cqPageLucene` predeterminado no tiene una regla de índice para `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

Antes de agregar la regla de índice cq:tags

* **cq:regla de índice de etiquetas**

   * No existe de forma predeterminada

* **Consulta consulta Builder**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=my:tag
   ```

* **Plan de consulta**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

Esta consulta se resuelve en el índice `cqPageLucene`, pero como no existe ninguna regla de índice de propiedad para `jcr:content` o `cq:tags`, cuando se evalúa esta restricción, todos los registros del índice `cqPageLucene` se comprueban para determinar una coincidencia. Esto significa que si el índice contiene 1 millón de nodos `cq:Page`, entonces se verifican 1 millón de registros para determinar el conjunto de resultados.

Después de agregar la regla de índice cq:tags

* **cq:regla de índice de etiquetas**

   ```js
   /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
   @name=jcr:content/cq:tags
   @propertyIndex=true
   ```

* **Consulta consulta Builder**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=myTagNamespace:myTag
   ```

* **Plan de consulta**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

La adición de indexRule para `jcr:content/cq:tags` en el índice `cqPageLucene` permite que los datos `cq:tags` se almacenen de manera optimizada.

Cuando se realiza una consulta con la restricción `jcr:content/cq:tags`, el índice puede buscar los resultados por valor. Esto significa que si 100 `cq:Page` nodos tienen `myTagNamespace:myTag` como valor, sólo se devuelven esos 100 resultados y los otros 999.000 se excluyen de las comprobaciones de restricción, lo que mejora el rendimiento en un factor de 10.000.

Por supuesto, las restricciones de consulta adicionales reducen los conjuntos de resultados elegibles y optimizan aún más la optimización de la consulta.

De manera similar, sin una regla de índice adicional para la propiedad `cq:tags`, incluso una consulta de texto completo con una restricción en `cq:tags` tendría un mal rendimiento, ya que los resultados del índice devolverían todas las coincidencias de texto completo. La restricción de las etiquetas cq:se filtraría después.

Otra causa del filtrado posterior al índice son las Listas de Control de acceso, que a menudo se pierden durante el desarrollo. Intente asegurarse de que la consulta no devuelve rutas de acceso inaccesibles para el usuario. Esto generalmente se puede hacer mediante una mejor estructura de contenido y proporcionando una restricción de ruta relevante en la consulta.

Una manera útil de identificar si el índice Lucene devuelve muchos resultados para devolver un subconjunto muy pequeño como resultado de la consulta es habilitar los registros DEBUG para `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex` y ver cuántos documentos se cargan desde el índice. El número de resultados finales frente al número de documentos cargados no debería ser desproporcionado. Para obtener más información, consulte [Registro](/help/sites-deploying/configure-logging.md).

#### Post-implementación {#post-deployment-1}

* Monitoree el `error.log` para consultas transversales:

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* Visite la consola de operaciones [Rendimiento de Consulta](/help/sites-administering/operations-dashboard.md#query-performance) de AEM y [Explicar](/help/sites-administering/operations-dashboard.md#explain-query) consultas lentas que buscan planes de consulta que no resuelvan las restricciones de propiedades de consulta a las reglas de propiedades de índice.

### Detección de Consultas de conjuntos de resultados grandes {#detecting-large-result-set-queries}

#### Durante el desarrollo {#during-development-2}

Establezca umbrales bajos para oak.queryLimitInMemory (p. ej. 10000) y oak.queryLimitReads (p. ej. 5000) y optimice la consulta costosa al visitar una excepción UnsupportedOperationException que dice &quot;La consulta lee más de nodos x...&quot;.

Esto ayuda a evitar consultas que requieren muchos recursos (por ejemplo: no está respaldada por ningún índice o está respaldada por un índice de cobertura menos elevado). Por ejemplo, una consulta que lee nodos 1M produciría muchas E/S y tendría un impacto negativo en el rendimiento general de la aplicación. Por lo tanto, cualquier consulta que falle debido a los límites superiores debe analizarse y optimizarse.

#### Post-implementación {#post-deployment-2}

* Monitoree los registros de consultas que activan el consumo de memoria traversal de nodos grandes o de gran consumo de memoria de pila: &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Optimice la consulta para reducir el número de nodos a través de los cuales se realiza el desplazamiento

* Monitoree los registros de consultas que activan el consumo de memoria de gran pila:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Optimice la consulta para reducir el consumo de memoria del montón

Para las versiones de AEM 6.0 a 6.2, puede ajustar el umbral para el recorrido de nodos mediante parámetros JVM en la secuencia de comandos de inicio de AEM para evitar que grandes consultas sobrecarguen el entorno. Los valores recomendados son:

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

En AEM 6.3, los 2 parámetros anteriores están preconfigurados de forma predeterminada y se pueden modificar mediante OSGi QueryEngineSettings.

Más información disponible en : [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Ajuste del rendimiento de la consulta {#query-performance-tuning}

El lema de la optimización del rendimiento de consulta en AEM es:

**&quot;Cuantas más restricciones, mejor&quot;.**

A continuación se describen los ajustes recomendados para garantizar el rendimiento de la consulta. Ajuste primero la consulta, una actividad menos complicada y, si es necesario, ajuste las definiciones de índice.

### Ajuste de la instrucción de Consulta {#adjusting-the-query-statement}

AEM admite los siguientes idiomas de consulta:

* Query Builder
* JCR-SQL2
* XPath

En el siguiente ejemplo se utiliza Consulta Builder ya que es el lenguaje de consulta más común utilizado por los desarrolladores de AEM; sin embargo, los mismos principios se aplican a JCR-SQL2 y XPath.

1. Añada una restricción nodetype para que la consulta se resuelva en un índice de propiedades Lucene existente.

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

   Las consultas que carecen de una restricción de tipo de nodo obligan a AEM a asumir el tipo de nodo `nt:base`, que cada nodo de AEM es un subtipo de, lo que resulta en una restricción de tipo de nodo.

   La configuración `type=cq:Page` restringe esta consulta sólo a `cq:Page` nodos y resuelve la consulta a AEM cqPageLucene, limitando los resultados a un subconjunto de nodos (sólo `cq:Page` nodos) en AEM.

1. Ajuste la restricción nodetype de la consulta para que la consulta se resuelva en un índice de propiedades Lucene existente.

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

   `nt:hierarchyNode` es el tipo de nodo principal de  `cq:Page`y, suponiendo que solo  `jcr:content/contentType=article-page` se aplique a  `cq:Page` los nodos a través de nuestra aplicación personalizada, esta consulta sólo devolverá  `cq:Page` nodos donde  `jcr:content/contentType=article-page`. Sin embargo, esta es una restricción subóptima porque:

   * Otros nodos heredan de `nt:hierarchyNode` (p. ej. `dam:Asset`) añadiendo innecesariamente al conjunto de posibles resultados.
   * No existe un índice proporcionado por AEM para `nt:hierarchyNode`, pero sí un índice proporcionado para `cq:Page`.
   La configuración `type=cq:Page` restringe esta consulta a sólo nodos `cq:Page` y resuelve la consulta a AEM cqPageLucene, limitando los resultados a un subconjunto de nodos (sólo nodos cq:Page) en AEM.

1. O bien, ajuste las restricciones de propiedad para que la consulta se resuelva en un índice de propiedades existente.

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

   Si se cambia la restricción de propiedad de `jcr:content/contentType` (un valor personalizado) a la propiedad conocida `sling:resourceType`, la consulta puede resolver el índice de propiedad `slingResourceType` que indexa todo el contenido por `sling:resourceType`.

   Los índices de propiedades (a diferencia de los índices de propiedades de Lucene) se utilizan mejor cuando la consulta no se detecta por tipo de nodo y una única restricción de propiedad domina el conjunto de resultados.

1. Añada la restricción de ruta más estricta posible para la consulta. Por ejemplo, prefiera `/content/my-site/us/en` por encima de `/content/my-site` o `/content/dam` por encima de `/`.

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

   Al establecer la restricción de ruta de `path=/content`a `path=/content/my-site/us/en`, los índices pueden reducir el número de entradas de índice que se deben inspeccionar. Cuando la consulta puede restringir la ruta muy bien, más allá de `/content` o `/content/dam`, asegúrese de que el índice tenga `evaluatePathRestrictions=true`.

   Tenga en cuenta que el uso de `evaluatePathRestrictions` aumenta el tamaño del índice.

1. Cuando sea posible, evite las funciones y operaciones de consulta, como: `LIKE` y `fn:XXXX` a medida que sus costos escalan con el número de resultados basados en restricciones.

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

   La condición LIKE es lenta de evaluar porque no se puede utilizar ningún índice si el texto está inicio con un comodín (&quot;%...&#39;). La condición jcr:contains permite utilizar un índice de texto completo y, por lo tanto, es preferible. Esto requiere que el Índice de propiedades de Lucene resuelto tenga indexRule para `jcr:content/contentType` con `analayzed=true`.

   El uso de funciones de consulta como `fn:lowercase(..)` puede resultar más difícil de optimizar, ya que no hay equivalentes más rápidos (fuera de configuraciones de analizador de índices más complejas y obtrusivas). Lo mejor es identificar otras restricciones de creación de ámbitos para mejorar el rendimiento general de la consulta, lo que requiere que las funciones funcionen en el conjunto más pequeño posible de resultados potenciales.

1. ***Este ajuste es específico del Generador de Consultas y no se aplica a JCR-SQL2 o XPath.***

   Utilice [generador de Consultas&#39; adivinenTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) cuando el conjunto completo de resultados sea **no** inmediatamente necesario.

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
   En los casos en los que la ejecución de la consulta es rápida pero el número de resultados es grande, p. `guessTotal` es una optimización crítica para las consultas del Generador de Consultas.

   `p.guessTotal=100` indica a Consulta Builder que solo recopile los primeros 100 resultados y defina un indicador booleano que indique si existen al menos otros resultados (pero no cuántos más, ya que contar este número sería lento). Esta optimización destaca para los casos de uso de paginación o carga infinita, donde sólo se muestra un subconjunto de resultados de forma incremental.

## Ajuste de índice existente {#existing-index-tuning}

1. Si la consulta óptima se resuelve en un índice de propiedades, no queda nada por hacer, ya que los índices de propiedades pueden ajustarse de forma mínima.
1. De lo contrario, la consulta debería resolver en un índice de propiedades de Lucene. Si no se puede resolver ningún índice, vaya a Creación de un nuevo índice.
1. Si es necesario, convierta la consulta a XPath o JCR-SQL2.

   * **Consulta consulta Builder**

      ```js
      query type=cq:Page
      path=/content/my-site/us/en
      property=jcr:content/contentType
      property.value=article-page
      orderby=@jcr:content/publishDate
      orderby.sort=desc
      ```

   * **XPath generado a partir de la consulta del Generador de Consultas**

      ```js
      /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
      ```

1. Proporcione XPath (o JCR-SQL2) a [Generador de definiciones de índices Oak](https://oakutils.appspot.com/generate/index) para generar la definición optimizada del índice de propiedades de Lucene.

   **Definición del índice de propiedades de Lucene generada**

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

1. Combine manualmente la definición generada con el Índice de propiedades de Lucene existente de forma aditiva. Tenga cuidado de no eliminar las configuraciones existentes, ya que pueden utilizarse para satisfacer otras consultas.

   1. Busque el índice de propiedades de Lucene existente que cubre cq:Page (mediante el Administrador de índices). En este caso, `/oak:index/cqPageLucene`.
   1. Identifique el delta de configuración entre la definición de índice optimizada (paso 4) y el índice existente (/oak:index/cqPageLucene), y agregue las configuraciones que faltan del Índice optimizado a la definición de índice existente.
   1. Por AEM Optimizaciones para volver a indexar, se debe actualizar o reindexar en función de si el contenido existente se verá afectado por este cambio de configuración de índice.

## Crear un nuevo índice {#create-a-new-index}

1. Compruebe que la consulta no se resuelve en un índice de propiedades de Lucene existente. Si es así, consulte la sección anterior sobre ajuste e índice existente.
1. Si es necesario, convierta la consulta a XPath o JCR-SQL2.

   * **Consulta consulta Builder**

      ```js
      type=myApp:Author
      property=firstName
      property.value=ira
      ```

   * **XPath generado a partir de la consulta del Generador de Consultas**

      ```js
      //element(*, myApp:Page)[@firstName = 'ira']
      ```

1. Proporcione XPath (o JCR-SQL2) a [Generador de definiciones de índices Oak](https://oakutils.appspot.com/generate/index) para generar la definición optimizada del índice de propiedades de Lucene.

   **Definición del índice de propiedades de Lucene generada**

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

1. Implemente la definición generada del índice de propiedades de Lucene.

   Añada la definición XML proporcionada por Oak Index Definition Generator para el nuevo índice al proyecto de AEM que administra las definiciones de índice Oak (recuerde, trate las definiciones de índice Oak como código, ya que el código depende de ellas).

   Implemente y pruebe el nuevo índice siguiendo el ciclo de vida habitual de desarrollo de software de AEM y verifique que la consulta se resuelva en el índice y que la consulta funcione.

   Tras la implementación inicial de este índice, AEM rellenará el índice con los datos necesarios.

## ¿Cuándo son correctas las consultas sin índice y de recorrido? {#when-index-less-and-traversal-queries-are-ok}

Debido a AEM arquitectura de contenido flexible, es difícil predecir y asegurar que las transversales de las estructuras de contenido no evolucionen con el tiempo para ser inaceptablemente grandes.

Por lo tanto, asegúrese de que los índices cumplen las consultas, excepto si la combinación de restricción de ruta y restricción de tipo de nodo garantiza que **menos de 20 nodos se hayan recorrido nunca.**

## Herramientas de desarrollo de consulta {#query-development-tools}

### Adobe admitido {#adobe-supported}

* **Consulta Builder Debugger**

   * Una WebUI para ejecutar consultas del Generador de Consultas y generar el XPath compatible (para su uso en Explicar Consulta o en el Generador de definiciones de índices Oak).
   * Ubicado en AEM en [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite - Herramienta Consulta**

   * Una WebUI para ejecutar consultas XPath y JCR-SQL2.
   * Ubicado en AEM en [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) > Herramientas > Consulta...

* **[Explicar la consulta](/help/sites-administering/operations-dashboard.md#explain-query)**

   * Un panel de operaciones de AEM que proporciona una explicación detallada (plan de Consulta, tiempo de consulta y cantidad de resultados) para cualquier consulta XPATH o JCR-SQL2 dada.

* **[Consultas lentas/populares](/help/sites-administering/operations-dashboard.md#query-performance)**

   * Un panel de Operaciones AEM que enumera las consultas lentas y populares recientes ejecutadas en AEM.

* **[Administrador de índices](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * Una WebUI de operaciones de AEM que muestra los índices en la instancia de AEM; facilita la comprensión de los índices que ya existen, que se pueden segmentar o aumentar.

* **[Registro](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Registro de consulta Builder

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Registro de ejecución de consultas Oak

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Configuración del motor de Consulta Apache Jackrabbit Configuración OSGi**

   * Configuración de OSGi que configura el comportamiento de error para recorrer consultas.
   * Ubicado en AEM en [/system/console/configMgr#org.apache.jackrabbit.oak.consulta.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodoContador de granos JMX**

   * MBean de JMX utilizado para estimar el número de nodos en los árboles de contenido de AEM.
   * Ubicado en AEM en [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### Comunidad admitida {#community-supported}

* **[Generador de definiciones de índice Oak](https://oakutils.appspot.com/generate/index)**

   * Genere un índice de propiedades de luminancia óptimo a partir de las sentencias de consulta XPath o JCR-SQL2.

* **[Complemento AEM Chrome](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * Extensión del navegador web de Google Chrome que expone los datos del registro por solicitud, incluidas las consultas ejecutadas y sus planes de consulta, en la consola de herramientas de desarrollo del navegador.
   * Requiere que [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) esté instalado y habilitado en AEM.
