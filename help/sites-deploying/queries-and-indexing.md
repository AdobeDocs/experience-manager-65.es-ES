---
title: Consultas e indexación de Oak
seo-title: Consultas e indexación de Oak
description: Aprenda a configurar índices en AEM.
seo-description: Aprenda a configurar índices en AEM.
uuid: a1233d2e-1320-43e0-9b18-cd6d1eeaad59
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 492741d5-8d2b-4a81-8f21-e621ef3ee685
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2881'
ht-degree: 1%

---


# Consultas e indexación de Oak{#oak-queries-and-indexing}

>[!NOTE]
>
>Este artículo trata sobre la configuración de índices en AEM 6. Para conocer las prácticas recomendadas sobre optimización del rendimiento de indexación y consultas, consulte [Prácticas recomendadas para consultas e indexación](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

## Introducción {#introduction}

A diferencia de Jackrabbit 2, Oak no indexa el contenido de forma predeterminada. Los índices personalizados deben crearse cuando sea necesario, al igual que con las bases de datos relacionales tradicionales. Si no hay índice para una consulta específica, posiblemente se atraviesen muchos nodos. La consulta puede seguir funcionando, pero probablemente sea muy lenta.

Si Oak encuentra una consulta sin un índice, se imprime un mensaje de registro de nivel WARN:

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## Lenguajes de consulta admitidos {#supported-query-languages}

El motor de consulta Oak admite los siguientes idiomas:

* XPath (recomendado)
* SQL-2
* SQL (obsoleto)
* JQOM

## Tipos de indexador y cálculo de costes {#indexer-types-and-cost-calculation}

El back-end basado en Apache Oak permite conectar diferentes indexadores al repositorio.

Un indizador es el **Property Index**, para el cual la definición del índice se almacena en el propio repositorio.

Las implementaciones para **Apache Lucene** y **Solr** también están disponibles de forma predeterminada, ambas admiten la indexación de texto completo.

Se utiliza el **Traversal Index** si no hay ningún otro indizador disponible. Esto significa que el contenido no está indexado y los nodos de contenido se atraviesan para encontrar coincidencias con la consulta.

Si hay varios indexadores disponibles para una consulta, cada indizador disponible calcula el coste de ejecución de la consulta. A continuación, Oak elige al indizador con el costo estimado más bajo.

![chlimage_1-148](assets/chlimage_1-148.png)

El diagrama anterior es una representación de alto nivel del mecanismo de ejecución de consultas de Apache Oak.

En primer lugar, la consulta se analiza en un árbol de sintaxis abstracta. A continuación, la consulta se comprueba y transforma en SQL-2, que es el idioma nativo para las consultas Oak.

A continuación, se consulta cada índice para estimar el coste de la consulta. Una vez finalizado, se recuperan los resultados del índice más barato. Por último, los resultados se filtran para garantizar que el usuario actual tenga acceso de lectura al resultado y que el resultado coincida con la consulta completa.

## Configuración de los índices {#configuring-the-indexes}

>[!NOTE]
>
>Para un repositorio grande, la creación de un índice es una operación que lleva mucho tiempo. Esto se aplica tanto a la creación inicial de un índice como a la reindexación (reconstrucción de un índice después de cambiar la definición). Consulte también [Resolución de problemas de los índices Oak](/help/sites-deploying/troubleshooting-oak-indexes.md) y [Prevención de la reindexación lenta](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing).

Si es necesario reindexar en repositorios muy grandes, especialmente cuando se utiliza MongoDB y para índices de texto completo, considere la preextracción de texto y el uso de oak-run para crear el índice inicial y reindexar.

Los índices se configuran como nodos en el repositorio bajo el nodo **oak:index**.

El tipo del nodo de índice debe ser **oak:QueryIndexDefinition.** Hay varias opciones de configuración disponibles para cada indizador como propiedades de nodo. Para obtener más información, consulte los detalles de configuración de cada tipo de indexador a continuación.

### Índice de propiedades {#the-property-index}

El índice de propiedades suele ser útil para consultas que tienen restricciones de propiedad pero no son de texto completo. Se puede configurar siguiendo el siguiente procedimiento:

1. Abra CRXDE yendo a `http://localhost:4502/crx/de/index.jsp`
1. Cree un nuevo nodo en **oak:index**
1. Asigne un nombre al nodo **PropertyIndex** y establezca el tipo de nodo en **oak:QueryIndexDefinition**
1. Establezca las siguientes propiedades para el nuevo nodo:

   * **type:**  `property`  (de tipo String)
   * **propertyNames:**  `jcr:uuid`  (de tipo Nombre)

   Este ejemplo en particular indexará la propiedad `jcr:uuid`, cuyo trabajo es exponer el identificador único universal (UUID) del nodo al que está asociado.

1. Guarde los cambios.

El índice de propiedades tiene las siguientes opciones de configuración:

* La propiedad **type** especificará el tipo de índice y, en este caso, debe establecerse en **property**

* La propiedad **propertyNames** indica la lista de propiedades que se almacenarán en el índice. En caso de que falte, el nombre del nodo se utilizará como valor de referencia del nombre de propiedad. En este ejemplo, la propiedad **jcr:uuid** cuyo trabajo es exponer el identificador único (UUID) de su nodo se agrega al índice.

* El indicador **único** que, si se establece en **true** agrega una restricción de exclusividad en el índice de propiedades.

* La propiedad **declaringNodeTypes** permite especificar un determinado tipo de nodo al que solo se aplicará el índice.
* El indicador **reindex**, que si se establece en **true**, déclencheur un reíndice de contenido completo.

### Índice solicitado {#the-ordered-index}

El índice Pedido es una extensión del índice Propiedad. Sin embargo, ha quedado obsoleto. Los índices de este tipo deben reemplazarse por el [Índice de propiedades de Lucene](#the-lucene-property-index).

### Índice de texto completo de Lucene {#the-lucene-full-text-index}

Un indexador de texto completo basado en Apache Lucene está disponible en AEM 6.

Si se configura un índice de texto completo, todas las consultas que tengan una condición de texto completo utilizarán el índice de texto completo, independientemente de si hay otras condiciones que estén indexadas y no importa si hay una restricción de ruta.

Si no se configura ningún índice de texto completo, las consultas con condiciones de texto completo no funcionarán como se espera.

Dado que el índice se actualiza mediante un subproceso en segundo plano asincrónico, algunas búsquedas de texto completo no estarán disponibles durante un breve periodo de tiempo hasta que los procesos en segundo plano hayan finalizado.

Puede configurar un índice de texto completo de Lucene siguiendo el siguiente procedimiento:

1. Abra CRXDE y cree un nuevo nodo en **oak:index**.
1. Asigne un nombre al nodo **LuceneIndex** y establezca el tipo de nodo en **oak:QueryIndexDefinition**
1. Agregue las siguientes propiedades al nodo :

   * **type:**  `lucene`  (de tipo String)
   * **async:**  `async`  (de tipo String)

1. Guarde los cambios.

El índice de Lucene tiene las siguientes opciones de configuración:

* La propiedad **type** que especificará el tipo de índice debe establecerse en **lucene**
* La propiedad **async** que debe establecerse en **async**. Esto enviará el proceso de actualización del índice a un subproceso en segundo plano.
* La propiedad **includePropertyTypes**, que define qué subconjunto de tipos de propiedad se incluirá en el índice.
* La propiedad **excludePropertyNames** que definirá una lista de nombres de propiedades: propiedades que deben excluirse del índice.
* El indicador **reindex**, que cuando se establece en **true**, déclencheur un reindexado de contenido completo.

### Índice de propiedades de Lucene {#the-lucene-property-index}

Desde **Oak 1.0.8**, Lucene puede utilizarse para crear índices que impliquen restricciones de propiedad que no sean de texto completo.

Para obtener un índice de propiedad de Lucene, la propiedad **fulltextEnabled** siempre debe estar definida como falsa.

Veamos el siguiente ejemplo de consulta:

```xml
select * from [nt:base] where [alias] = '/admin'
```

Para definir un Índice de propiedades de Lucene para la consulta anterior, puede añadir la siguiente definición creando un nuevo nodo en **oak:index:**

* **Nombre:** `LucenePropertyIndex`
* **Tipo:** `oak:QueryIndexDefinition`

Una vez creado el nodo, añada las siguientes propiedades:

* **tipo:**

   ```
   lucene (of type String)
   ```

* **asíncrona:**

   ```
   async (of type String)
   ```

* **fulltextEnabled:**

   ```
   false (of type Boolean)
   ```

* **includePropertyNames:** `["alias"] (of type String)`

>[!NOTE]
>
>En comparación con el índice de propiedades normal, el índice de propiedades de Lucene siempre se configura en modo asíncrono. Por lo tanto, es posible que los resultados devueltos por índice no reflejen siempre el estado más actualizado del repositorio.

>[!NOTE]
>
>Para obtener información más específica sobre el índice de propiedades de Lucene, consulte la [página de documentación de Apache Jackrabbit Oak Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### Analizadores de Lucene {#lucene-analyzers}

Desde la versión 1.2.0, Oak admite analizadores de Lucene.

Los analizadores se utilizan tanto cuando se indexa un documento como en el momento de la consulta. Un analizador examina el texto de los campos y genera un flujo de token. Los analizadores de Lucene están compuestos por una serie de clases de tokenizer y filter.

Los analizadores se pueden configurar mediante el nodo `analyzers` (de tipo `nt:unstructured`) dentro de la definición `oak:index`.

El analizador predeterminado de un índice se configura en el elemento secundario `default` del nodo analizadores.

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>Para obtener una lista de analizadores disponibles, consulte la documentación de la API de la versión de Lucene que está utilizando.

#### Especificación directa de la clase Analyzer {#specifying-the-analyzer-class-directly}

Si desea utilizar algún analizador listo para usar, puede configurarlo siguiendo el siguiente procedimiento:

1. Busque el índice con el que desea utilizar el analizador en el nodo `oak:index`.

1. En el índice, cree un nodo secundario llamado `default` de tipo `nt:unstructured`.

1. Agregue una propiedad al nodo predeterminado con las siguientes propiedades:

   * **Nombre:** `class`
   * **Tipo:** `String`
   * **Valor:** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   El valor es el nombre de la clase de analizador que desea utilizar.

   También puede configurar el analizador para que se utilice con una versión de lucene específica mediante la propiedad opcional de cadena `luceneMatchVersion`. Un sintax válido para utilizarlo con Lucene 4.7 sería:

   * **Nombre:** `luceneMatchVersion`
   * **Tipo:** `String`
   * **Valor:** `LUCENE_47`

   Si no se proporciona `luceneMatchVersion`, Oak utilizará la versión de Lucene con la que se envía.

1. Si desea agregar un archivo de palabras clave a las configuraciones del analizador, puede crear un nuevo nodo en el `default` con las siguientes propiedades:

   * **Nombre:** `stopwords`
   * **Tipo:** `nt:file`

#### Creación de analizadores mediante la composición {#creating-analyzers-via-composition}

Los analizadores también se pueden componer en función de `Tokenizers`, `TokenFilters` y `CharFilters`. Puede hacerlo especificando un analizador y creando nodos secundarios de sus tokenizadores y filtros opcionales que se aplicarán en el orden indicado. Consulte también [https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

Considere esta estructura de nodos como ejemplo:

* **Nombre:** `analyzers`

   * **Nombre:** `default`

      * **Nombre:** `charFilters`
      * **Tipo:** `nt:unstructured`

         * **Nombre:** `HTMLStrip`
         * **Nombre:** `Mapping`
      * **Nombre:** `tokenizer`

         * **Nombre de propiedad:** `name`

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





El nombre de los filtros, charFilters y los tokenizadores se forman eliminando los sufijos de fábrica. Por lo tanto:

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` se convierte  `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` se convierte  `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` se convierte  `Stop`

Cualquier parámetro de configuración requerido para la fábrica se especifica como propiedad del nodo en cuestión.

En casos como la carga de palabras de parada en las que es necesario cargar contenido de archivos externos, el contenido se puede proporcionar creando un nodo secundario de tipo `nt:file` para el archivo en cuestión.

### El índice Solr {#the-solr-index}

El propósito del índice Solr es principalmente la búsqueda de texto completo, pero también puede utilizarse para indexar la búsqueda por ruta, restricciones de propiedad y restricciones de tipo principal. Esto significa que el índice Solr en Oak puede utilizarse para cualquier tipo de consulta JCR.

La integración en AEM ocurre a nivel del repositorio, de modo que Solr es uno de los índices posibles que se puede usar en Oak, la nueva implementación del repositorio enviada con AEM.

Se puede configurar para que funcione como servidor incrustado con la instancia de AEM o como servidor remoto.

### Configuración de AEM con un servidor Solr integrado {#configuring-aem-with-an-embedded-solr-server}

>[!CAUTION]
>
>No utilice un servidor Solr incrustado en un entorno de producción. Solo debe utilizarse en un entorno de desarrollo.

AEM se puede utilizar con un servidor Solr incrustado que se puede configurar mediante la consola web. En este caso, el servidor Solr se ejecutará en la misma JVM que la instancia de AEM a la que está incrustado.

Puede configurar el servidor Solr incrustado de:

1. Accediendo a la consola web en `https://serveraddress:4502/system/console/configMgr`
1. Busque &quot;**Oak Solr server provider**&quot;.
1. Pulse el botón de edición y, en la siguiente ventana, establezca el tipo de servidor en **Embedded Solr** en la lista desplegable.

1. A continuación, edite &quot;**Oak Solr incrustado server configuration**&quot; y cree una configuración. Para obtener más información sobre las opciones de configuración, visite el [sitio web de Apache Solr](https://lucene.apache.org/solr/documentation.html).

   >[!NOTE]
   >
   >La configuración de Solr home directory (solr.home.path) buscará una carpeta con el mismo nombre en la carpeta de instalación de AEM.

1. Abra CRXDE e inicie sesión como administrador.
1. Agregue un nodo llamado **solrlndex** de tipo **oak:QueryIndexDefinition** en **oak:index** con las siguientes propiedades:

   * **type:** `solr` (de tipo String)
   * **async:** `async` (de tipo String)
   * **reindex:** `true` (de tipo booleano)

1. Guarde los cambios.

### Configuración de AEM con un único servidor Solr remoto {#configuring-aem-with-a-single-remote-solr-server}

También se AEM configurar para que funcione con una instancia de servidor Solr remoto:

1. Descargue y extraiga la última versión de Solr. Para obtener más información sobre cómo hacerlo, consulte la [documentación de instalación de Apache Solr](https://cwiki.apache.org/confluence/display/solr/Installing+Solr).
1. Ahora, cree dos fragmentos de Solr. Para ello, puede crear carpetas para cada elemento compartido en la carpeta en la que se ha realizado el seguimiento de Solr:

   * Para el primer uso compartido, cree la carpeta :

   `<solrunpackdirectory>\aemsolr1\node1`

   * Para el segundo compartido, cree la carpeta :

   `<solrunpackdirectory>\aemsolr2\node2`

1. Busque la instancia de ejemplo en el paquete Solr. Normalmente se encuentra en una carpeta denominada &quot; `example`&quot; en la raíz del paquete.
1. Copie las siguientes carpetas de la instancia de ejemplo a las dos carpetas compartidas ( `aemsolr1\node1` y `aemsolr2\node2`):

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. Cree una nueva carpeta denominada &quot; `cfg`&quot; en cada una de las dos carpetas compartidas.
1. Coloque los archivos de configuración Solr y Zookeeper en las carpetas `cfg` recién creadas.

   >[!NOTE]
   >
   >Para obtener más información sobre la configuración de Solr y ZooKeeper, consulte la [Documentación de configuración de Solr](https://wiki.apache.org/solr/ConfiguringSolr) y la [Guía de introducción de ZooKeeper](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html).

1. Inicie el primer uso compartido con soporte de ZooKeeper yendo a `aemsolr1\node1` y ejecutando el siguiente comando:

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. Inicie el segundo uso compartido yendo a `aemsolr2\node2` y ejecutando el siguiente comando:

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. Una vez que se hayan iniciado ambos shards, pruebe que todo está en funcionamiento conectándose a la interfaz Solr en `http://localhost:8983/solr/#/`
1. Inicie AEM y vaya a la consola web en `http://localhost:4502/system/console/configMgr`
1. Establezca la siguiente configuración en **Configuración del servidor remoto Oak Solr**:

   * Solr URL HTTP: `http://localhost:8983/solr/`

1. Elija **Remote Solr** en la lista desplegable de **Oak Solr** server provider.

1. Vaya a CRXDE e inicie sesión como administrador.
1. Cree un nuevo nodo llamado **solrIndex** en **oak:index** y establezca las siguientes propiedades:

   * **type:** solr (de tipo String)
   * **async:** async (de tipo String)
   * **reindex:** true (de tipo booleano)

1. Guarde los cambios.

#### Configuración recomendada para Solr {#recommended-configuration-for-solr}

A continuación se muestra un ejemplo de una configuración base que se puede utilizar con las tres implementaciones de Solr descritas en este artículo. Aloja los índices de propiedades dedicados que ya están presentes en AEM y no deben usarse con otras aplicaciones.

Para utilizarlo correctamente, debe colocar el contenido del archivo directamente en Solr Home Directory. En el caso de implementaciones de varios nodos, debe ir directamente debajo de la carpeta raíz de cada nodo.

Archivos de configuración de Solr recomendados

[Obtener archivo](assets/recommended-conf.zip)

### Herramientas de indexación de AEM {#aem-indexing-tools}

AEM 6.1 también integra dos herramientas de indexación presentes en AEM 6.0 como parte del conjunto de herramientas de Adobe Consulting Services Commons:

1. **Explicar consulta**, una herramienta diseñada para ayudar a los administradores a comprender cómo se ejecutan las consultas;
1. **Oak Index Manager**, una interfaz de usuario web para mantener índices existentes.

Ahora puede acceder a ellas accediendo a **Herramientas - Operaciones - Tablero - Diagnóstico** desde la pantalla de bienvenida de AEM.

Para obtener más información sobre cómo utilizarlos, consulte la [Documentación del panel de operaciones](/help/sites-administering/operations-dashboard.md).

#### Creación de índices de propiedades mediante OSGi {#creating-property-indexes-via-osgi}

El paquete ACS Commons también expone las configuraciones de OSGi que pueden utilizarse para crear índices de propiedades.

Puede acceder a él desde la consola web buscando &quot;**Asegúrese de que el índice de propiedades de Oak**&quot;.

![chlimage_1-150](assets/chlimage_1-150.png)

### Solución de problemas de indexación {#troubleshooting-indexing-issues}

Pueden surgir situaciones en las que las consultas tardan mucho en ejecutarse y el tiempo de respuesta general del sistema es lento.

En esta sección se presenta un conjunto de recomendaciones sobre lo que hay que hacer para determinar la causa de esas cuestiones y asesorar sobre cómo resolverlas.

#### Preparación de información de depuración para análisis {#preparing-debugging-info-for-analysis}

La forma más sencilla de obtener la información necesaria para la consulta que se está ejecutando es mediante la [Explicar herramienta de consulta](/help/sites-administering/operations-dashboard.md#explain-query). Esto le permite recopilar la información precisa necesaria para depurar una consulta lenta sin necesidad de consultar la información de nivel de registro. Esto es deseable si conoce la consulta que se está depurando.

Si esto no es posible por ningún motivo, puede recopilar los registros de indexación en un solo archivo y utilizarlos para solucionar su problema en particular.

#### Habilitar el registro {#enable-logging}

Para habilitar el registro, debe habilitar los registros de nivel **DEBUG** para las categorías pertenecientes a la indexación y las consultas de Oak. Estas categorías son:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

La categoría **com.day.cq.search** solo es aplicable si utiliza la utilidad QueryBuilder proporcionada por el AEM.

>[!NOTE]
>
>Es importante que los registros solo se configuren en DEBUG durante la ejecución de la consulta que desea solucionar los problemas; de lo contrario, se generará una gran cantidad de eventos en los registros a lo largo del tiempo. Por este motivo, una vez recopilados los registros necesarios, vuelva al registro de nivel INFO para las categorías mencionadas anteriormente.

Puede habilitar el registro siguiendo este procedimiento:

1. Apunte el navegador a `https://serveraddress:port/system/console/slinglog`
1. Haga clic en el botón **Add new Logger** en la parte inferior de la consola.
1. En la fila recién creada, añada las categorías mencionadas anteriormente. Puede utilizar el signo **+** para agregar más de una categoría a un único registrador.
1. Elija **DEBUG** en la lista desplegable **Log level**.
1. Establezca el archivo de salida en `logs/queryDebug.log`. Esto correlacionará todos los eventos de depuración en un solo archivo de registro.
1. Ejecute la consulta o procese la página que está utilizando la consulta que desea depurar.
1. Una vez que haya ejecutado la consulta, vuelva a la consola de registro y cambie el nivel de registro del registrador recién creado a **INFO**.

#### Configuración de índice {#index-configuration}

La forma en que se evalúa la consulta se ve afectada en gran medida por la configuración del índice. Es importante obtener la configuración del índice para poder analizarlo o enviarlo para que sea compatible. Puede obtener la configuración como paquete de contenido o una representación JSON.

Como en la mayoría de los casos, la configuración de indexación se almacena en el nodo `/oak:index` en CRXDE, puede obtener la versión JSON en:

`https://serveraddress:port/oak:index.tidy.-1.json`

Si el índice está configurado en una ubicación diferente, cambie la ruta en consecuencia.

#### MBean output {#mbean-output}

En algunos casos, es útil proporcionar el resultado de MBeans relacionados con el índice para la depuración. Para ello:

1. Accediendo a la consola JMX en:
   `https://serveraddress:port/system/console/jmx`

1. Busque los siguientes MBeans:

   * Estadísticas del índice Lucene
   * Estadísticas de compatibilidad con CopyOnRead
   * Estadísticas de consulta de Oak
   * IndexStats

1. Haga clic en cada MBeans para obtener las estadísticas de rendimiento. Cree una captura de pantalla o anójelos en caso de que sea necesario enviar un mensaje para que sea compatible.

También puede obtener la variante JSON de estas estadísticas en las siguientes direcciones URL:

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

También puede proporcionar una salida JMX consolidada a través de `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`. Esto incluiría todos los detalles de MBean relacionados con Oak en formato JSON.

#### Otros detalles {#other-details}

Puede recopilar detalles adicionales para ayudar a solucionar el problema, como por ejemplo:

1. La versión Oak en la que se está ejecutando la instancia. Para verlo, abra CRXDE y observe la versión en la esquina inferior derecha de la página de bienvenida o compruebe la versión del paquete `org.apache.jackrabbit.oak-core`.
1. El resultado de QueryBuilder Debugger de la consulta problemática. Se puede acceder al depurador en: `https://serveraddress:port/libs/cq/search/content/querydebug.html`

