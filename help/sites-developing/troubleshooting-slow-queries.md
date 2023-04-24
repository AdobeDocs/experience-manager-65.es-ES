---
title: Solución de problemas de consultas lentas
seo-title: Troubleshooting Slow Queries
description: Solución de problemas de consultas lentas
seo-description: null
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
exl-id: 3405cdd3-3d1b-414d-9931-b7d7b63f0a6f
source-git-commit: a296e459461973fc2dbd0641c6fdda1d89d8d524
workflow-type: tm+mt
source-wordcount: '2262'
ht-degree: 0%

---

# Solución de problemas de consultas lentas{#troubleshooting-slow-queries}

## Clasificaciones de consultas lentas {#slow-query-classifications}

Hay tres clasificaciones principales de consultas lentas en AEM, enumeradas por gravedad:

1. **Consultas sin índice**

   * Consultas que sí **not** resolver en un índice y recorrer el contenido de JCR para recopilar resultados

1. **Consultas poco restringidas (o con ámbitos)**

   * Consultas que se resuelven en un índice, pero que deben recorrer todas las entradas de índice para recopilar resultados

1. **Consultas de conjuntos de resultados grandes**

   * Consultas que devuelven un gran número de resultados

Las dos primeras clasificaciones de consultas (sin índice y mal restringidas) son lentas. Son lentos porque obligan al motor de consulta Oak a inspeccionar cada **potencial** resultado (nodo de contenido o entrada de índice) para identificar qué pertenece a la variable **real** conjunto de resultados.

El acto de inspeccionar cada posible resultado es lo que se conoce como Traversing.

Dado que es necesario inspeccionar cada posible resultado, el costo para determinar el conjunto de resultados real aumenta linealmente con el número de posibles resultados.

La adición de restricciones de consulta e índices de ajuste permite almacenar los datos de índice en un formato optimizado que permite una rápida recuperación de resultados y, además, reduce o elimina la necesidad de la inspección lineal de posibles conjuntos de resultados.

En AEM 6.3, de forma predeterminada, cuando se alcanza una travesía de 100 000, la consulta falla y genera una excepción. Este límite no existe de forma predeterminada en versiones AEM anteriores a AEM 6.3, pero se puede establecer a través de la configuración OSGi de Apache Jackrabbit Query Engine y QueryEngineSettings JMX bean (propiedad LimitReads).

### Detección de consultas sin índice {#detecting-index-less-queries}

#### Durante el desarrollo {#during-development}

Explicar **all** consultas y asegúrese de que sus planes de consulta no contengan **/&amp;ast; traverse** en ellos. Ejemplo de plan de consulta de recorrido:

* **PLAN:** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### Posterior a la implementación {#post-deployment}

* Monitorice el `error.log` para consultas transversales sin índice:

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * Este mensaje solo se registra si no hay ningún índice disponible y si la consulta potencialmente atraviesa muchos nodos. Los mensajes no se registran si hay un índice disponible, pero la cantidad a recorrer es pequeña y, por lo tanto, rápida.

* Visite la AEM [Rendimiento de la consulta](/help/sites-administering/operations-dashboard.md#query-performance) consola operaciones y [Explicar](/help/sites-administering/operations-dashboard.md#explain-query) consultas lentas que buscan explicaciones de consulta transversal o sin índice.

### Detección de consultas mal restringidas {#detecting-poorly-restricted-queries}

#### Durante el desarrollo {#during-development-1}

Explique todas las consultas y asegúrese de que se resuelven en un índice ajustado para coincidir con las restricciones de propiedad de la consulta.

* La cobertura del plan de consulta ideal tiene `indexRules` para todas las restricciones de propiedad y como mínimo para las restricciones de propiedad más estrictas de la consulta.
* Las consultas que ordenan los resultados deben resolverse en un índice de propiedades de Lucene con reglas de índice para las propiedades ordenadas por propiedades establecidas `orderable=true.`

#### Por ejemplo, el valor predeterminado `cqPageLucene` no tiene una regla de índice para `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

Antes de añadir la regla de índice cq:tags

* **cq:tags Regla de índice**

   * No existe de forma predeterminada

* **Consulta del generador de consultas**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=my:tag
   ```

* **Plan de consulta**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

Esta consulta se resuelve en el `cqPageLucene` index, pero porque no existe ninguna regla de índice de propiedad para `jcr:content` o `cq:tags`, cuando se evalúa esta restricción, todos los registros de la variable `cqPageLucene` se comprueba el índice para determinar una coincidencia. Como tal, si el índice contiene 1 millón `cq:Page` , se comprueban 1 millón de registros para determinar el conjunto de resultados.

Después de añadir la regla de índice cq:tags

* **cq:tags Regla de índice**

   ```js
   /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
   @name=jcr:content/cq:tags
   @propertyIndex=true
   ```

* **Consulta del generador de consultas**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=myTagNamespace:myTag
   ```

* **Plan de consulta**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

La adición de indexRule para `jcr:content/cq:tags` en el `cqPageLucene` index permite `cq:tags` datos que se van a almacenar de forma optimizada.

Cuando una consulta con la variable `jcr:content/cq:tags` la restricción se realiza, el índice puede buscar los resultados por valor. Eso significa que si 100 `cq:Page` los nodos tienen `myTagNamespace:myTag` como valor, sólo se devuelven esos 100 resultados y los otros 999.000 se excluyen de las comprobaciones de restricciones, lo que mejora el rendimiento en un factor de 10.000.

Más restricciones de consulta reducen los conjuntos de resultados aptos y optimizan aún más la optimización de la consulta.

Del mismo modo, sin una regla de índice adicional para la variable `cq:tags` , incluso una consulta de texto completo con una restricción de `cq:tags` tendría un rendimiento pobre, ya que los resultados del índice devolverían todas las coincidencias de texto completo. La restricción en cq:tags se filtraría después de ella.

Otra causa del filtrado posterior al índice es las Listas de control de acceso, que a menudo se pierden durante el desarrollo. Intente asegurarse de que la consulta no devuelva rutas que podrían no ser accesibles para el usuario. Para ello, se puede mejorar la estructura de contenido y proporcionar una restricción de ruta relevante en la consulta.

Una forma útil de identificar si el índice de Lucene devuelve muchos resultados para devolver un pequeño subconjunto como resultado de la consulta, es habilitar los registros de DEBUG para `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex`. Al hacerlo, puede ver cuántos documentos se están cargando desde el índice. El número de resultados finales frente al número de documentos cargados no debería ser desproporcionado. Para obtener más información, consulte [Registro](/help/sites-deploying/configure-logging.md).

#### Posterior a la implementación {#post-deployment-1}

* Monitorice el `error.log` para consultas transversales:

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* Visite la AEM [Rendimiento de la consulta](/help/sites-administering/operations-dashboard.md#query-performance) consola operaciones y [Explicar](/help/sites-administering/operations-dashboard.md#explain-query) consultas lentas que buscan planes de consulta que no resuelvan restricciones de propiedad de consulta a reglas de propiedad de índice.

### Detección de consultas de conjuntos de resultados grandes {#detecting-large-result-set-queries}

#### Durante el desarrollo {#during-development-2}

Establezca umbrales bajos para oak.queryLimitInMemory (por ejemplo, 10000) y oak.queryLimitReads (por ejemplo, 5000) y optimice la consulta costosa al visitar una excepción UnsupportedOperationException que dice &quot;La consulta lee más de x nodos...&quot;.

La configuración de umbrales bajos ayuda a evitar consultas intensivas en recursos (es decir, que no estén respaldadas por ningún índice o que estén respaldadas por un índice menos abarcador). Por ejemplo, una consulta que lee un millón de nodos produciría muchas IO y tendría un impacto negativo en el rendimiento general de la aplicación. Por lo tanto, cualquier consulta que falle debido a límites superiores debe analizarse y optimizarse.

#### Posterior a la implementación {#post-deployment-2}

* Monitorice los registros para las consultas que activan el consumo de memoria de gran nodo transversal o de gran pila: &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Optimice la consulta para reducir el número de nodos recorridos.

* Monitorice los registros de las consultas que activan el consumo de memoria de pila grande:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Optimice la consulta para reducir el consumo de memoria acumulada.

Para AEM versiones 6.0 - 6.2, puede ajustar el umbral para la travesía de nodos a través de parámetros JVM en el script de inicio de AEM para evitar que las consultas grandes sobrecarguen el entorno. Los valores recomendados son:

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

En AEM 6.3, los dos parámetros anteriores están preconfigurados de forma predeterminada y se pueden modificar a través de OSGi QueryEngineSettings.

Más información disponible en : [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Ajuste del rendimiento de la consulta {#query-performance-tuning}

El lema de la optimización del rendimiento de las consultas en AEM es:

**&quot;Cuantas más restricciones, mejor&quot;.**

A continuación se describen los ajustes recomendados para garantizar el rendimiento de las consultas. Ajuste primero la consulta, una actividad menos intrusiva y, si es necesario, ajuste las definiciones de índice.

### Ajuste de la instrucción de consulta {#adjusting-the-query-statement}

AEM admite los siguientes idiomas de consulta:

* Query Builder
* JCR-SQL2
* XPath

El siguiente ejemplo utiliza Query Builder ya que es el lenguaje de consulta más común utilizado por los desarrolladores de AEM, sin embargo, los mismos principios se aplican a JCR-SQL2 y XPath.

1. Agregue una restricción nodetype para que la consulta se resuelva en un índice de propiedades de Lucene existente.

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

   Las consultas que no tienen una restricción de tipo de nodo obligan a AEM a asumir la `nt:base` nodetype, que cada nodo de AEM es un subtipo de , lo que no produce ninguna restricción de tipo de nodo.

   Configuración `type=cq:Page` restringe esta consulta solo a `cq:Page` y resuelve la consulta en AEM cqPageLucene, limitando los resultados a un subconjunto de nodos (solo `cq:Page` nodos) en AEM.

1. Ajuste la restricción de tipo de nodo de la consulta para que la consulta se resuelva en un índice de propiedades de Lucene existente.

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

   `nt:hierarchyNode` es el nodo principal de `cq:Page`. Asumiendo `jcr:content/contentType=article-page` solo se aplica a `cq:Page` nodos a través de la aplicación personalizada de Adobe, esta consulta solo devuelve `cq:Page` nodos donde `jcr:content/contentType=article-page`. Sin embargo, este flujo es una restricción subóptima porque:

   * Otros nodos heredan de `nt:hierarchyNode` (por ejemplo, `dam:Asset`) añadiendo innecesariamente al conjunto de posibles resultados.
   * No existe ningún índice proporcionado AEM para `nt:hierarchyNode`, sin embargo, ya que hay un índice proporcionado para `cq:Page`.
   Configuración `type=cq:Page` restringe esta consulta solo a `cq:Page` y resuelve la consulta en AEM cqPageLucene, limitando los resultados a un subconjunto de nodos (solo nodos cq:Page) en AEM.

1. O bien, ajuste las restricciones de propiedad para que la consulta se resuelva en un índice de propiedad existente.

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

   Cambio de la restricción de propiedad de `jcr:content/contentType` (un valor personalizado) a la propiedad conocida `sling:resourceType` permite que la consulta se resuelva en el índice de propiedad `slingResourceType` que indexa todo el contenido por `sling:resourceType`.

   Los índices de propiedades (a diferencia de los índices de propiedades de Lucene) se utilizan mejor cuando la consulta no se distingue por tipo de nodo y una sola restricción de propiedad domina el conjunto de resultados.

1. Agregue la restricción de ruta más estricta posible a la consulta. Por ejemplo, prefiera `/content/my-site/us/en` over `/content/my-site`o `/content/dam` over `/`.

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

   Creación de ámbitos de la restricción de rutas desde `path=/content`a `path=/content/my-site/us/en` permite que los índices reduzcan el número de entradas de índice que deben inspeccionarse. Cuando la consulta puede restringir bien la ruta, más allá de `/content` o `/content/dam`, asegúrese de que el índice tiene `evaluatePathRestrictions=true`.

   Tenga en cuenta que `evaluatePathRestrictions` aumenta el tamaño del índice.

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

   La condición LIKE es lenta de evaluar porque no se puede usar ningún índice si el texto comienza con un comodín (&quot;%...&quot;). La condición jcr:contains permite usar un índice de texto completo, y por lo tanto se prefiere. Requiere que el índice de propiedades de Lucene resuelto tenga indexRule para `jcr:content/contentType` con `analayzed=true`.

   Uso de funciones de consulta como `fn:lowercase(..)` puede ser más difícil de optimizar, ya que no hay equivalentes más rápidos (fuera de configuraciones de analizador de índices más complejas y obtrusivas). Es mejor identificar otras restricciones de alcance para mejorar el rendimiento general de la consulta, lo que requiere que las funciones funcionen en el conjunto más pequeño posible de resultados potenciales.

1. ***Este ajuste es específico de Query Builder y no se aplica a JCR-SQL2 o XPath.***

   Uso [Adivinación del Generador de consultas](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) cuando el conjunto completo de resultados es **not** inmediatamente necesario.

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
   En los casos en los que la ejecución de la consulta sea rápida pero el número de resultados sea grande, p. `guessTotal` es una optimización crítica para las consultas de Query Builder.

   `p.guessTotal=100` indica a Query Builder que solo recopile los 100 primeros resultados. Y, para establecer un indicador booleano que indique si existe al menos un resultado más (pero no cuántos más, ya que contar este número resulta en lentitud). Esta optimización destaca para casos de uso de paginación o carga infinita, donde solo se muestra un subconjunto de resultados de forma incremental.

## Ajuste de índice existente {#existing-index-tuning}

1. Si la consulta óptima se resuelve en un índice de propiedades, no queda nada que hacer, ya que los índices de propiedades se pueden ajustar mínimamente.
1. De lo contrario, la consulta debe resolverse en un índice de propiedades de Lucene. Si no se puede resolver ningún índice, vaya a Creación de un nuevo índice.
1. Si es necesario, convierta la consulta a XPath o JCR-SQL2.

   * **Consulta del generador de consultas**

      ```js
      query type=cq:Page
      path=/content/my-site/us/en
      property=jcr:content/contentType
      property.value=article-page
      orderby=@jcr:content/publishDate
      orderby.sort=desc
      ```

   * **XPath generado a partir de la consulta de Query Builder**

      ```js
      /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
      ```

1. Proporcione XPath (o JCR-SQL2) al Generador de definiciones de índices Oak en `https://oakutils.appspot.com/generate/index` de este modo, puede generar la definición optimizada del índice de propiedades de Lucene. <!-- The above URL is 404 as of April 24, 2023 -->

   **Definición del índice de propiedades de Lucene generado**

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

   1. Busque el Índice de propiedades de Lucene existente que cubre cq:Page (mediante el Administrador de índices). En este caso, `/oak:index/cqPageLucene`.
   1. Identifique el delta de configuración entre la definición del índice optimizado (paso 4) y el índice existente (/oak:index/cqPageLucene) y añada las configuraciones que faltan del índice optimizado a la definición del índice existente.
   1. Por AEM Prácticas recomendadas de reindexación, una actualización o un reíndice están en orden, en función de si el contenido existente puede verse afectado por este cambio en la configuración del índice.

## Crear un nuevo índice {#create-a-new-index}

1. Compruebe que la consulta no se resuelva en un índice de propiedades de Lucene existente. Si es así, consulte la sección anterior sobre ajuste e índice existente.
1. Si es necesario, convierta la consulta a XPath o JCR-SQL2.

   * **Consulta del generador de consultas**

      ```js
      type=myApp:Author
      property=firstName
      property.value=ira
      ```

   * **XPath generado a partir de la consulta de Query Builder**

      ```js
      //element(*, myApp:Page)[@firstName = 'ira']
      ```

1. Proporcione XPath (o JCR-SQL2) al Generador de definiciones de índices Oak en `https://oakutils.appspot.com/generate/index` de este modo, puede generar la definición optimizada del índice de propiedades de Lucene. <!-- The above URL is 404 as of April 24, 2023 -->

   **Definición del índice de propiedades de Lucene generado**

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

   Agregue la definición XML proporcionada por Oak Index Definition Generator para el nuevo índice al proyecto AEM que administra las definiciones de índice Oak (recuerde, trate las definiciones de índice Oak como código, ya que el código depende de ellas).

   Implemente y pruebe el nuevo índice siguiendo el ciclo de vida habitual de desarrollo de software de AEM y verifique que la consulta se resuelva en el índice y que la consulta funcione.

   En la implementación inicial de este índice, AEM rellena el índice con los datos necesarios.

## ¿Cuándo son correctas las consultas sin índice y las consultas transversales? {#when-index-less-and-traversal-queries-are-ok}

Debido a AEM arquitectura de contenido flexible, es difícil predecir y garantizar que los recorridos de las estructuras de contenido no evolucionen con el tiempo para ser inaceptablemente grandes.

Por lo tanto, asegúrese de que los índices satisfacen las consultas, excepto si la combinación de restricción de ruta y restricción de tipo de nodo garantiza que **se atraviesan menos de 20 nodos.**

## Herramientas de desarrollo de consultas {#query-development-tools}

### Adobe admitido {#adobe-supported}

* **Depurador del generador de consultas**

   * Una interfaz de usuario web para ejecutar consultas del Generador de consultas y generar el XPath compatible (para su uso en Explicar consulta u Oak Index Definition Generator).
   * En AEM a [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite - Herramienta Consulta**

   * Una interfaz de usuario web para ejecutar consultas XPath y JCR-SQL2.
   * En AEM a [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) > Herramientas > Consulta...

* **[Explicar la consulta](/help/sites-administering/operations-dashboard.md#explain-query)**

   * Un panel de Operaciones de AEM que proporciona una explicación detallada (plan de consulta, tiempo de consulta y número de resultados) para cualquier consulta XPATH o JCR-SQL2 dada.

* **[Consultas lentas/populares](/help/sites-administering/operations-dashboard.md#query-performance)**

   * Un panel de Operaciones de AEM que enumera las consultas lentas y populares recientes ejecutadas en AEM.

* **[Administrador de índices](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * Una AEM Operations WebUI que muestra los índices de la instancia de AEM; facilita la comprensión de qué índices existen; se pueden segmentar o aumentar.

* **[Registro](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Registro de Query Builder

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Registro de ejecución de consultas Oak

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Configuración OSGi de Apache Jackrabbit Query Engine**

   * Configuración de OSGi que configura el comportamiento de error para recorrer consultas.
   * En AEM a [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **Mbean de NodeCounter JMX**

   * JMX MBean solía estimar el número de nodos en árboles de contenido en AEM.
   * En AEM a [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### Comunidad admitida {#community-supported}

* **Generador de definiciones de índices Oak en`https://oakutils.appspot.com/generate/index`** <!-- The above URL is 404 as of April 24, 2023 -->

   * Genere un índice de propiedades de Lucence óptimo a partir de instrucciones de consulta XPath o JCR-SQL2.

* **[Complemento AEM Chrome](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * Extensión de explorador web de Google Chrome que expone los datos de registro por solicitud, incluidas las consultas ejecutadas y sus planes de consulta, en la consola de herramientas de desarrollo del explorador.
   * Requiere [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) para instalar y habilitar en AEM.
