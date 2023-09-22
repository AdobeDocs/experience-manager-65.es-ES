---
title: Consultas e indexación de Oak
description: Obtenga información sobre cómo configurar índices en Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
exl-id: d9ec7728-84f7-42c8-9c80-e59e029840da
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '3033'
ht-degree: 2%

---

# Consultas e indexación de Oak{#oak-queries-and-indexing}

>[!NOTE]
>
>AEM Este artículo trata sobre la configuración de índices en la 6. Para conocer las prácticas recomendadas sobre la optimización del rendimiento de consultas e indexación, consulte [Prácticas recomendadas para consultas e indexación](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

## Introducción {#introduction}

A diferencia de Jackrabbit 2, Oak no indexa el contenido de forma predeterminada. Se deben crear índices personalizados cuando sea necesario, como con las bases de datos relacionales tradicionales. Si no hay ningún índice para una consulta específica, es posible que se atraviesen muchos nodos. La consulta puede seguir funcionando, pero es probable que sea lenta.

Si Oak encuentra una consulta sin índice, se imprime un mensaje de registro de nivel WARN:

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## Idiomas de consulta admitidos {#supported-query-languages}

El motor de consultas de Oak es compatible con los siguientes idiomas:

* XPath (recomendado)
* SQL-2
* SQL (obsoleto)
* JQOM

## Tipos de indexador y cálculo de costes {#indexer-types-and-cost-calculation}

El back-end basado en Apache Oak permite que diferentes indexadores se conecten al repositorio.

Un indexador es el **Índice de propiedades**, para la cual la definición del índice se almacena en el propio repositorio.

Implementaciones para **Apache Lucene** y **Solr** también están disponibles de forma predeterminada, ya que ambos admiten la indexación de texto completo.

El **Índice de recorrido** se utiliza si no hay ningún otro indizador disponible. Esto significa que el contenido no está indexado y que los nodos de contenido se atraviesan para encontrar coincidencias con la consulta.

Si hay varios indexadores disponibles para una consulta, cada indexador disponible calcula el coste de ejecución de la consulta. A continuación, Oak elige el indexador con el coste estimado más bajo.

![chlimage_1-148](assets/chlimage_1-148.png)

El diagrama anterior es una representación de alto nivel del mecanismo de ejecución de consultas de Apache Oak.

En primer lugar, la consulta se analiza en un árbol de sintaxis abstracta. A continuación, se comprueba la consulta y se transforma en SQL-2, que es el idioma nativo para las consultas Oak.

A continuación, se consulta cada índice para estimar el coste de la consulta. Una vez completado este paso, se recuperan los resultados del índice más barato. Finalmente, los resultados se filtran, tanto para garantizar que el usuario actual tenga acceso de lectura al resultado como para que el resultado coincida con la consulta completa.

## Configuración de los índices {#configuring-the-indexes}

>[!NOTE]
>
>Para un repositorio grande, crear un índice es una operación que requiere mucho tiempo. Esto es así tanto para la creación inicial de un índice como para la reindexación (reconstrucción de un índice después de cambiar la definición). Consulte también [Solución de problemas de índices Oak](/help/sites-deploying/troubleshooting-oak-indexes.md) y [Prevención de la reindexación lenta](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing).

Si es necesario reindexar en repositorios grandes, especialmente cuando se utiliza MongoDB y para índices de texto completo, considere la preextracción de texto y el uso de oak-run para crear el índice inicial y reindexar.

Los índices se configuran como nodos en el repositorio en la variable **Oak:index** nodo.

El tipo del nodo de índice debe ser **oak:QueryIndexDefinition.** Hay varias opciones de configuración disponibles para cada indexador como propiedades de nodo. Para obtener más información, consulte los detalles de configuración de cada tipo de indizador a continuación.

### El índice de propiedades {#the-property-index}

El índice de propiedades es útil para consultas que tienen restricciones de propiedad pero no son de texto completo. Se puede configurar siguiendo el siguiente procedimiento:

1. Abra CRXDE yendo a `http://localhost:4502/crx/de/index.jsp`
1. Cree un nodo en **oak:index**
1. Asigne un nombre al nodo **PropertyIndex** y establezca el tipo de nodo en **oak:QueryIndexDefinition**
1. Establezca las siguientes propiedades para el nuevo nodo:

   * **tipo:**  `property` (de tipo cadena)
   * **propertyNames:**  `jcr:uuid` (de tipo Nombre)

   Este ejemplo en particular indexa el `jcr:uuid` , cuyo trabajo es exponer el identificador único universal (UUID) del nodo al que está asociado.

1. Guarde los cambios.

El índice de propiedades tiene las siguientes opciones de configuración:

* El **type** especifica el tipo de índice y, en este caso, se debe establecer en **propiedad**

* El **propertyNames** indica la lista de las propiedades almacenadas en el índice. En caso de que falte, el nombre del nodo se utiliza como valor de referencia del nombre de propiedad. En este ejemplo, la variable **jcr:uuid** La propiedad de cuyo trabajo es exponer el identificador único (UUID) de su nodo se agrega al índice.

* El **único** indicador que, si se establece en **true** agrega una restricción de unicidad al índice de propiedades.

* El **declaringNodeTypes** La propiedad permite especificar un tipo de nodo determinado al que el índice solo se aplica.
* El **reindexar** indicador que si se establece en **true**, déclencheur un reíndice de contenido completo.

### El índice ordenado {#the-ordered-index}

El índice ordenado es una extensión del índice de propiedad. Sin embargo, ha quedado obsoleto. Los índices de este tipo deben reemplazarse por el [Índice de propiedades de Lucene](#the-lucene-property-index).

### Índice de texto completo de Lucene {#the-lucene-full-text-index}

AEM En la versión 6 de está disponible un indexador de texto completo basado en Apache Lucene.

Si se configura un índice de texto completo, todas las consultas que tienen una condición de texto completo utilizan el índice de texto completo, independientemente de si hay otras condiciones que están indizadas y de si hay una restricción de ruta.

Si no se configura ningún índice de texto completo, las consultas con condiciones de texto completo no funcionan según lo esperado.

Dado que el índice se actualiza mediante un subproceso en segundo plano asincrónico, algunas búsquedas de texto completo no están disponibles durante un período de tiempo breve hasta que finalizan los procesos en segundo plano.

Puede configurar un índice de texto completo de Lucene siguiendo el siguiente procedimiento:

1. Abra CRXDE y cree un nodo en **oak:index**.
1. Asigne un nombre al nodo **LuceneIndex** y establezca el tipo de nodo en **oak:QueryIndexDefinition**
1. Agregue las siguientes propiedades al nodo:

   * **tipo:**  `lucene` (de tipo cadena)
   * **asíncrona:**  `async` (de tipo cadena)

1. Guarde los cambios.

El índice Lucene tiene las siguientes opciones de configuración:

* El **type** propiedad que especifica el tipo de índice debe establecerse en **lucene**
* El **asíncrona** propiedad que debe establecerse en **asíncrona**. Esto envía el proceso de actualización del índice a un subproceso en segundo plano.
* El **includePropertyTypes** propiedad, que define qué subconjunto de tipos de propiedad se incluye en el índice.
* El **excludePropertyNames** propiedad que define una lista de nombres de propiedades: propiedades que deben excluirse del índice.
* El **reindexar** indicador que, cuando se establece en **true**, déclencheur un reíndice de contenido completo.

### Explicación de la búsqueda de texto completo {#understanding-fulltext-search}

La documentación de esta sección se aplica a Apache Lucene, Elasticsearch e índices de texto completo de PostgreSQL, SQLite y MySQL, por ejemplo. AEM El siguiente ejemplo es para el caso de la aplicación de la combinación de: Oak / Lucene.

<b>Datos que indexar</b>

El punto de partida son los datos que deben indexarse. Veamos los siguientes documentos, por ejemplo:

| <b>ID de documento</b> | <b>Ruta</b> | <b>Texto completo</b> |
| --- | --- | --- |
| 100 | /content/rubik | &quot;Rubik es una marca finlandesa&quot;. |
| 200 | /content/rubiksCube | &quot;El cubo de Rubik fue inventado en 1974&quot;. |
| 300 | /content/cube | &quot;Un cubo es un objeto tridimensional.&quot; |


<b>Índice invertido</b>

El mecanismo de indexación divide el texto completo en palabras denominadas &quot;tokens&quot; y crea un índice denominado &quot;índice invertido&quot;. Este índice contiene la lista de documentos donde aparece para cada palabra.

Las palabras cortas y comunes (también denominadas &quot;palabras de parada&quot;) no se indexan. Todos los tokens se convierten a minúsculas y se aplica la derivación.

Caracteres especiales como *&quot;-&quot;* no están indexados.

| <b>Token</b> | <b>Identificadores de documento</b> |
| --- | --- |
| 194 | ..., 200,... |
| marca | ..., 100,... |
| cubo | ..., 200, 300,... |
| dimensión | 300 |
| terminar | ..., 100,... |
| inventar | 200 |
| objeto | ..., 300,... |
| rubí | ..., 100, 200,... |

La lista de documentos está ordenada. Esto resulta útil cuando se realiza una consulta.

<b>Buscando</b>

A continuación se muestra un ejemplo de consulta. Tenga en cuenta que todos los caracteres especiales (como *&#39;*) se han reemplazado por un espacio:

```
/jcr:root/content//element(\*; cq:Page)`[` jcr:contains('Rubik s Cube')`]`
```

Las palabras se identifican mediante token y se filtran del mismo modo que al indexar (por ejemplo, se eliminan las palabras de un solo carácter). Por lo tanto, en este caso, la búsqueda es para:

```
+:fulltext:rubik +:fulltext:cube
```

El índice consulta la lista de documentos para esas palabras. Si hay muchos documentos, la lista puede ser grande. A modo de ejemplo, supongamos que contienen lo siguiente:


| <b>Token</b> | <b>Identificadores de documento</b> |
| --- | --- |
| rubí | 10, 100, 200, 1000 |
| cubo | 30, 200, 300, 2000 |


Lucene gira hacia atrás y hacia adelante entre las dos listas (o round-robin) `n` listas, al buscar `n` palabras):

* Leído en el &quot;rubik&quot; obtiene la primera entrada: encuentra 10
* Leído en el &quot;cubo&quot; obtiene la primera entrada `>` = 10. 10 no se encuentra, el siguiente es 30.
* Leer en el &quot;rubik&quot; obtiene la primera entrada `>` = 30: encuentra 100.
* Leído en el &quot;cubo&quot; obtiene la primera entrada `>` = 100: encuentra 200.
* Leer en el &quot;rubik&quot; obtiene la primera entrada `>` = 200. 200 se ha encontrado. Así que el documento 200 coincide para ambos términos. Esto se recuerda.
* Leer en el &quot;rubik&quot; obtiene la siguiente entrada: 1000.
* Leído en el &quot;cubo&quot; obtiene la primera entrada `>` = 1000: encuentra 2000.
* Leer en el &quot;rubik&quot; obtiene la primera entrada `>` = 2000: final de la lista.
* Por último, puede detener la búsqueda.

El único documento encontrado que contiene ambos términos es 200, como en el ejemplo siguiente:

| 200 | /content/rubiksCube | &quot;El cubo de Rubik fue inventado en 1974&quot;. |
| --- | --- | --- |

Cuando se encuentran varias entradas, se ordenan por puntuación.

### Índice de propiedades de Lucene {#the-lucene-property-index}

Desde **Oak 1.0.8**, Lucene se puede utilizar para crear índices que impliquen restricciones de propiedad que no sean de texto completo.

Para obtener un índice de propiedades de Lucene, la variable **fulltextEnabled** La propiedad siempre debe establecerse en False.

Consulte el siguiente ejemplo de consulta:

```xml
select * from [nt:base] where [alias] = '/admin'
```

Para definir un índice de propiedades de Lucene para la consulta anterior, puede agregar la siguiente definición creando un nodo en **roble:index:**

* **Nombre:** `LucenePropertyIndex`
* **Tipo:** `oak:QueryIndexDefinition`

Una vez creado el nodo, agregue las siguientes propiedades:

* **tipo:**

  ```xml
  lucene (of type String)
  ```

* **asíncrona:**

  ```xml
  async (of type String)
  ```

* **fulltextEnabled:**

  ```xml
  false (of type Boolean)
  ```

* **includePropertyNames:** `["alias"] (of type String)`

>[!NOTE]
>
>En comparación con el Índice de propiedades normal, el Índice de propiedades de Lucene siempre se configura en modo asincrónico. Por lo tanto, es posible que los resultados devueltos por el índice no siempre reflejen el estado más actualizado del repositorio.

>[!NOTE]
>
>Para obtener información más específica sobre el índice de propiedades de Lucene, consulte la [Página de documentación de Apache Jackrabbit Oak Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### Analizadores Lucene {#lucene-analyzers}

Desde la versión 1.2.0, Oak admite analizadores Lucene.

Los analizadores se utilizan tanto cuando se indexa un documento como en el momento de la consulta. Un analizador examina el texto de los campos y genera un flujo de tokens. Los analizadores Lucene están compuestos por una serie de clases de tokenizer y filtro.

Los analizadores se pueden configurar mediante el `analyzers` nodo (de tipo `nt:unstructured`) dentro de `oak:index` definición.

El analizador predeterminado para un índice se configura en la variable `default` secundario del nodo de analizadores.

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>Para obtener una lista de los analizadores disponibles, consulte la documentación de la API de la versión de Lucene que está utilizando.

#### Especificar la clase de analizador directamente {#specifying-the-analyzer-class-directly}

Si desea utilizar cualquier analizador predeterminado, puede configurarlo siguiendo el siguiente procedimiento:

1. Busque el índice con el que desea utilizar el analizador en `oak:index` nodo.

1. En el índice, cree un nodo secundario llamado `default` de tipo `nt:unstructured`.

1. Agregue una propiedad al nodo predeterminado con las siguientes propiedades:

   * **Nombre:** `class`
   * **Tipo:** `String`
   * **Valor:** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   El valor es el nombre de la clase de analizador que desea utilizar.

   También puede configurar el analizador para que se utilice con una versión de Lucene específica utilizando el `luceneMatchVersion` propiedad de cadena. Una sintaxis válida para utilizarla con Lucene 4.7 sería:

   * **Nombre:** `luceneMatchVersion`
   * **Tipo:** `String`
   * **Valor:** `LUCENE_47`

   If `luceneMatchVersion` no se proporciona, Oak utiliza la versión de Lucene con la que se envía.

1. Si desea añadir un archivo de palabras de detención a las configuraciones del analizador, puede crear un nodo en el `default` uno con las siguientes propiedades:

   * **Nombre:** `stopwords`
   * **Tipo:** `nt:file`

#### Creación de analizadores mediante composición {#creating-analyzers-via-composition}

Los analizadores también pueden estar compuestos por `Tokenizers`, `TokenFilters`, y `CharFilters`. Para ello, especifique un analizador y cree nodos secundarios de sus tokenizers y filtros opcionales que se apliquen en el orden indicado. Consulte también [https://cwiki.apache.org/confluence/display/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://cwiki.apache.org/confluence/display/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

Consideremos esta estructura de nodos como un ejemplo:

* **Nombre:** `analyzers`

   * **Nombre:** `default`

      * **Nombre:** `charFilters`
      * **Tipo:** `nt:unstructured`

         * **Nombre:** `HTMLStrip`
         * **Nombre:** `Mapping`

      * **Nombre:** `tokenizer`

         * **Nombre de la propiedad:** `name`

            * **Tipo:** `String`
            * **Valor:** `Standard`

      * **Nombre:** `filters`
      * **Tipo:** `nt:unstructured`

         * **Nombre:** `LowerCase`
         * **Nombre:** `Stop`

            * **Nombre de la propiedad:** `words`

               * **Tipo:** `String`
               * **Valor:** `stop1.txt, stop2.txt`

            * **Nombre:** `stop1.txt`

               * **Tipo:** `nt:file`

            * **Nombre:** `stop2.txt`

               * **Tipo:** `nt:file`

El nombre de los filtros, charFilters y tokenizers se forman eliminando los sufijos de fábrica. Así:

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` pasa a `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` pasa a `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` pasa a `Stop`

Cualquier parámetro de configuración necesario para la fábrica se especifica como propiedad del nodo en cuestión.

En casos como la carga de palabras de detención en las que se debe cargar contenido de archivos externos, el contenido se puede proporcionar creando un nodo secundario de `nt:file` escriba para el archivo en cuestión.

### El Índice Solr {#the-solr-index}

El propósito del índice Solr es la búsqueda de texto completo, pero también se puede utilizar para indexar la búsqueda por ruta, restricciones de propiedad y restricciones de tipo principal. Esto significa que el índice Solr en Oak puede utilizarse para cualquier tipo de consulta JCR.

AEM AEM La integración en la se produce en el nivel de repositorio, por lo que Solr es uno de los posibles índices que se pueden utilizar en Oak, la nueva implementación de repositorio que se envía con la.

AEM Se puede configurar para que funcione como un servidor remoto con la instancia de.

### AEM Configuración con un único servidor Solr remoto {#configuring-aem-with-a-single-remote-solr-server}

AEM También se puede configurar para que funcione con una instancia remota del servidor Solr:

1. Descargue y extraiga la última versión de Solr. Para obtener más información sobre cómo hacerlo, consulte la [Documentación de instalación de Apache Solr](https://solr.apache.org/guide/6_6/installing-solr.html).
1. Ahora, cree dos fragmentos de Solr. Para ello, cree carpetas para cada uso compartido de la carpeta en la que se ha desempaquetado Solr:

   * Para el primer uso compartido, cree la carpeta:

   `<solrunpackdirectory>\aemsolr1\node1`

   * Para el segundo uso compartido, cree la carpeta:

   `<solrunpackdirectory>\aemsolr2\node2`

1. Busque la instancia de ejemplo en el paquete Solr. Se encuentra en una carpeta llamada &quot; `example`&quot; en la raíz del paquete.
1. Copie las siguientes carpetas de la instancia de ejemplo en las dos carpetas compartidas ( `aemsolr1\node1` y `aemsolr2\node2`):

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. Cree una carpeta llamada &quot; `cfg`&quot; en cada una de las dos carpetas compartidas.
1. Coloque los archivos de configuración de Solr y Zookeeper en el recién creado `cfg` carpetas.

   >[!NOTE]
   >
   >Para obtener más información sobre la configuración de Solr y ZooKeeper, consulte la [Documentación de configuración de Solr](https://cwiki.apache.org/confluence/display/solr/ConfiguringSolr) y el [Guía de introducción de ZooKeeper](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html).

1. Inicie el primer uso compartido con la asistencia de ZooKeeper yendo a `aemsolr1\node1` y ejecutar el siguiente comando:

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. Inicie el segundo uso compartido accediendo a `aemsolr2\node2` y ejecutar el siguiente comando:

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. Una vez iniciados ambos fragmentos, compruebe que todo está en funcionamiento conectándose a la interfaz de Solr en `http://localhost:8983/solr/#/`
1. AEM Inicie sesión y vaya a la consola web en `http://localhost:4502/system/console/configMgr`
1. Establezca la siguiente configuración en **Configuración del servidor remoto Oak Solr**:

   * URL HTTP de Solr: `http://localhost:8983/solr/`

1. Elegir **Solr remoto** en la lista desplegable debajo de **Oak Solr** proveedor de servidor.

1. Vaya a CRXDE e inicie sesión como administrador.
1. Cree un nodo llamado **solrIndex** bajo **oak:index** y establezca las siguientes propiedades:

   * **tipo:** solr (de tipo cadena)
   * **asíncrona:** async (de tipo cadena)
   * **reindexar:** true (de tipo booleano)

1. Guarde los cambios.

#### Configuración recomendada para Solr {#recommended-configuration-for-solr}

A continuación se muestra un ejemplo de una configuración base que se puede utilizar con las tres implementaciones de Solr descritas en este artículo. AEM Se adapta a los índices de propiedades dedicados que ya están presentes en la propiedad y que no deben usarse con otras aplicaciones.

Para utilizarlo correctamente, debe colocar el contenido del archivo directamente en el Directorio principal de Solr. Si hay implementaciones de varios nodos, debe ir directamente a la carpeta raíz de cada nodo.

Archivos de configuración de Solr recomendados

[Obtener archivo](assets/recommended-conf.zip)

### AEM Herramientas de indexación de {#aem-indexing-tools}

AEM AEM La versión 6.1 también integra dos herramientas de indexación presentes en la versión 6.0 de la aplicación de herramientas de Adobe Consulting Services Commons:

1. **Explicar consulta**, una herramienta diseñada para ayudar a los administradores a comprender cómo se ejecutan las consultas;
1. **Administrador de índices Oak**, una interfaz de usuario web para mantener los índices existentes.

Ahora puede acceder a ellas desde el vínculo a **Herramientas - Operaciones - Panel de control - Diagnóstico** AEM en la pantalla de bienvenida de la.

Para obtener más información sobre cómo utilizarlos, consulte la [Documentación del Operations Dashboard](/help/sites-administering/operations-dashboard.md).

#### Creación de índices de propiedades mediante OSGi {#creating-property-indexes-via-osgi}

El paquete ACS Commons también expone las configuraciones OSGi que se pueden utilizar para crear índices de propiedades.

Puede acceder a él desde la consola web buscando &quot;**Asegurar el índice de propiedades de Oak**&quot;.

![chlimage_1-150](assets/chlimage_1-150.png)

### Solución de problemas de indexación {#troubleshooting-indexing-issues}

Pueden surgir situaciones en las que las consultas tardan mucho tiempo en ejecutarse y el tiempo de respuesta general del sistema es lento.

Esta sección presenta un conjunto de recomendaciones sobre lo que se debe hacer para rastrear la causa de estos problemas y consejos sobre cómo resolverlos.

#### Preparar información de depuración para análisis {#preparing-debugging-info-for-analysis}

La forma más sencilla de obtener la información necesaria para la consulta que se está ejecutando es mediante el [Herramienta Explicar consulta](/help/sites-administering/operations-dashboard.md#explain-query). Esto permite recopilar la información precisa necesaria para depurar una consulta lenta sin necesidad de consultar la información de nivel de registro. Esto es deseable si conoce la consulta que se está depurando.

Si no es posible por cualquier motivo, puede recopilar los registros de indexación en un solo archivo y utilizarlo para solucionar su problema concreto.

#### Activar registro {#enable-logging}

Para habilitar el registro, debe habilitar **DEPURAR** registros de nivel para las categorías pertenecientes a la indexación y consultas de Oak. Estas categorías son:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

El **com.day.cq.search** AEM La categoría solo es aplicable si utiliza la utilidad QueryBuilder proporcionada por el usuario.

>[!NOTE]
>
>Es importante que los registros solo estén configurados en DEPURACIÓN mientras se esté ejecutando la consulta que desea solucionar. De lo contrario, se generan muchos eventos en los registros a lo largo del tiempo. Debido a esto, una vez recopilados los registros necesarios, vuelva al registro de nivel INFO para las categorías mencionadas anteriormente.

Puede habilitar el registro siguiendo este procedimiento:

1. Dirija el explorador a `https://serveraddress:port/system/console/slinglog`
1. Haga clic en **Añadir nuevo registrador** en la parte inferior de la consola.
1. En la fila recién creada, añada las categorías mencionadas anteriormente. Puede usar el complemento **+** para agregar más de una categoría a un solo registrador.
1. Elegir **DEPURAR** desde el **Nivel de registro** lista desplegable.
1. Establezca el archivo de salida en `logs/queryDebug.log`. Esto correlaciona todos los eventos de DEPURACIÓN en un solo archivo de registro.
1. Ejecute la consulta o procese la página que está utilizando la consulta que desea depurar.
1. Una vez ejecutada la consulta, vuelva a la consola de registro y cambie el nivel de registro del registrador recién creado a **INFORMACIÓN**.

#### Configuración del índice {#index-configuration}

La forma en que se evalúa la consulta se ve afectada en gran medida por la configuración del índice. Es importante analizar la configuración del índice o enviarla al servicio de asistencia. Puede obtener la configuración como paquete de contenido u obtener una representación JSON.

Normalmente, la configuración de indexación se almacena en `/oak:index` en CRXDE, puede obtener la versión JSON en:

`https://serveraddress:port/oak:index.tidy.-1.json`

Si el índice está configurado en una ubicación diferente, cambie la ruta según corresponda.

#### Salida de MBean {#mbean-output}

A veces resulta útil proporcionar el resultado de los MBeans relacionados con índices para la depuración. Para ello:

1. Vaya a la consola JMX en:
   `https://serveraddress:port/system/console/jmx`

1. Busque los siguientes MBeans:

   * Estadísticas de índice de Lucene
   * Estadísticas de compatibilidad con CopyOnRead
   * Estadísticas de consulta de Oak
   * IndexStats

1. Haga clic en cada uno de los MBean para obtener estadísticas de rendimiento. Cree una captura de pantalla o anótelas en caso de que sea necesario un envío de asistencia.

También puede obtener la variante JSON de estas estadísticas en las siguientes URL:

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

También puede proporcionar una salida JMX consolidada mediante `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`. Esto incluiría todos los detalles de MBean relacionados con Oak en formato JSON.

#### Otros detalles {#other-details}

Puede recopilar más detalles para solucionar el problema, como los siguientes:

1. La versión de Oak en la que se está ejecutando la instancia. Puede verlo abriendo CRXDE y mirando la versión en la esquina inferior derecha de la página de bienvenida, o comprobando la versión de `org.apache.jackrabbit.oak-core` paquete.
1. Resultado de QueryBuilder Debugger de la consulta problemática. Se puede acceder al depurador en: `https://serveraddress:port/libs/cq/search/content/querydebug.html`
