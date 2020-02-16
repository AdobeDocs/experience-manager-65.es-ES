---
title: Consultas de Oak e indización
seo-title: Consultas de Oak e indización
description: Obtenga información sobre cómo configurar índices en AEM.
seo-description: Obtenga información sobre cómo configurar índices en AEM.
uuid: a1233d2e-1320-43e0-9b18-cd6d1eeaad59
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 492741d5-8d2b-4a81-8f21-e621ef3ee685
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
translation-type: tm+mt
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306

---


# Consultas de Oak e indización{#oak-queries-and-indexing}

>[!NOTE]
>
>Este artículo trata sobre la configuración de índices en AEM 6. Para obtener información sobre las prácticas recomendadas para optimizar el rendimiento de la consulta y la indexación, consulte [Prácticas recomendadas para consultas e indexación](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

## Introducción {#introduction}

A diferencia de Jackrabbit 2, Oak no índice el contenido de forma predeterminada. Los índices personalizados deben crearse cuando sea necesario, al igual que con las bases de datos relacionales tradicionales. Si no hay un índice para una consulta específica, es posible que se atraviesen muchos nodos. La consulta puede seguir funcionando pero probablemente sea muy lenta.

Si Oak encuentra una consulta sin un índice, se imprime un mensaje de registro de nivel WARN:

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## Idiomas de consulta admitidos {#supported-query-languages}

El motor de consulta Oak admite los siguientes idiomas:

* XPath (recomendado)
* SQL-2
* SQL (desaprobado)
* JQOM

## Tipos de indexador y cálculo de costes {#indexer-types-and-cost-calculation}

El back-end basado en Apache Oak permite conectar diferentes indexadores al repositorio.

Un indizador es el **índice** de propiedades, para el que la definición de índice se almacena en el propio repositorio.

Las implementaciones para **Apache Lucene** y **Solr** también están disponibles de forma predeterminada, lo que permite indexar texto completo.

El **Índice** Traversal se utiliza si no hay ningún otro indizador disponible. Esto significa que el contenido no está indizado y que los nodos de contenido se atraviesan para encontrar coincidencias con la consulta.

Si hay varios indexadores disponibles para una consulta, cada indizador disponible calcula el costo de ejecución de la consulta. Oak luego elige al indizador con el costo estimado más bajo.

![chlimage_1-148](assets/chlimage_1-148.png)

El diagrama anterior es una representación de alto nivel del mecanismo de ejecución de consultas de Apache Oak.

En primer lugar, la consulta se analiza en un árbol de sintaxis abstracta. A continuación, la consulta se comprueba y se transforma en SQL-2, que es el idioma nativo de las consultas Oak.

A continuación, se consulta cada índice para estimar el costo de la consulta. Una vez finalizado, se recuperan los resultados del índice más barato. Por último, los resultados se filtran para garantizar que el usuario actual tenga acceso de lectura al resultado y que el resultado coincida con la consulta completa.

## Configuración de los índices {#configuring-the-indexes}

>[!NOTE]
>
>Para un repositorio grande, la creación de un índice es una operación lenta. Esto se aplica tanto a la creación inicial de un índice como al reindexado (reconstrucción de un índice después de cambiar la definición). Consulte también [Resolución de problemas con los índices](/help/sites-deploying/troubleshooting-oak-indexes.md) Oak y [Prevención de la reindexación](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing)lenta.

Si es necesario volver a indexar en repositorios muy grandes, especialmente cuando se utiliza MongoDB y para índices de texto completo, considere la extracción previa de texto y el uso de la función de roble para crear el índice inicial y reindexar.

Los índices se configuran como nodos en el repositorio bajo el nodo **oak:index** .

El tipo del nodo de índice debe ser **oak:QueryIndexDefinition.** Hay varias opciones de configuración disponibles para cada indizador como propiedades de nodo. Para obtener más información, consulte los detalles de configuración de cada tipo de indizador a continuación.

### Índice de propiedades {#the-property-index}

El índice de propiedades suele ser útil para las consultas que tienen restricciones de propiedad pero no son de texto completo. Se puede configurar siguiendo el procedimiento siguiente:

1. Abra CRXDE yendo a `http://localhost:4502/crx/de/index.jsp`
1. Crear un nuevo nodo en **roak:index**
1. Asigne un nombre al nodo **PropertyIndex** y defina el tipo de nodo en **oak:QueryIndexDefinition**
1. Defina las siguientes propiedades para el nuevo nodo:

   * **** type:  `property` (de tipo String)
   * **** propertyNames:  `jcr:uuid` (de tipo Nombre)
   En este ejemplo en particular se indexará la `jcr:uuid` propiedad, cuyo trabajo consiste en exponer el identificador único universal (UUID) del nodo al que está conectado.

1. Guarde los cambios.

El índice de propiedades tiene las siguientes opciones de configuración:

* La propiedad **type** especificará el tipo de índice y, en este caso, debe establecerse en **property**

* La propiedad **propertyNames** indica la lista de las propiedades que se almacenarán en el índice. Si falta, el nombre del nodo se utilizará como valor de referencia del nombre de propiedad. En este ejemplo, se agrega al índice la propiedad **jcr:uuid** cuyo trabajo es exponer el identificador único (UUID) de su nodo.

* El indicador **único** que, si se define como **true** , agrega una restricción de unicidad en el índice de propiedad.

* La propiedad **declaringNodeTypes** permite especificar un tipo de nodo determinado al que solo se aplicará el índice.
* El indicador de **reindexación** que, si se establece en **true**, activará un reíndice de contenido completo.

### Índice ordenado {#the-ordered-index}

El índice Pedido es una extensión del índice Propiedad. Sin embargo, ha quedado obsoleto. Los índices de este tipo deben reemplazarse por el [índice](#the-lucene-property-index)de propiedades de Lucene.

### Índice de texto completo de Lucene {#the-lucene-full-text-index}

Un indizador de texto completo basado en Apache Lucene está disponible en AEM 6.

Si se configura un índice de texto completo, todas las consultas que tengan una condición de texto completo utilizarán el índice de texto completo, sin importar si hay otras condiciones indizadas y sin importar si hay una restricción de ruta.

Si no hay ningún índice de texto completo configurado, las consultas con condiciones de texto completo no funcionarán según lo esperado.

Dado que el índice se actualiza mediante un subproceso en segundo plano asincrónico, algunas búsquedas de texto completo no estarán disponibles durante un período de tiempo reducido hasta que se hayan finalizado los procesos en segundo plano.

Puede configurar un índice de texto completo de Lucene siguiendo el procedimiento siguiente:

1. Abra CRXDE y cree un nuevo nodo en **roak:index**.
1. Asigne un nombre al nodo **LuceneIndex** y defina el tipo de nodo en **oak:QueryIndexDefinition**
1. Agregue las siguientes propiedades al nodo:

   * **** type:  `lucene` (de tipo String)
   * **** asíncrono:  `async` (de tipo String)

1. Guarde los cambios.

El índice Lucene tiene las siguientes opciones de configuración:

* La propiedad **type** que especificará el tipo de índice debe establecerse en **lucene**
* La propiedad **async** que debe establecerse en **async**. Esto enviará el proceso de actualización del índice a un subproceso en segundo plano.
* La propiedad **includePropertyTypes** , que definirá qué subconjunto de tipos de propiedad se incluirá en el índice.
* La propiedad **excludePropertyNames** que definirá una lista negra de nombres de propiedad: propiedades que deben excluirse del índice.
* El indicador de **reindexación** que, cuando se establece en **true**, activa un reíndice de contenido completo.

### Índice de propiedades de Lucene {#the-lucene-property-index}

Desde **Oak 1.0.8**, Lucene puede utilizarse para crear índices que impliquen restricciones de propiedad que no sean de texto completo.

Para obtener un índice de propiedades de Lucene, la propiedad **fulltextEnabled** siempre debe establecerse en false.

Observe la siguiente consulta de ejemplo:

```xml
select * from [nt:base] where [alias] = '/admin'
```

Para definir un índice de propiedades de Lucene para la consulta anterior, puede agregar la siguiente definición creando un nuevo nodo en **roak:index:**

* **Nombre:** `LucenePropertyIndex`
* **Tipo:** `oak:QueryIndexDefinition`

Una vez creado el nodo, agregue las siguientes propiedades:

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

* **** includePropertyNames: `["alias"] (of type String)`

>[!NOTE]
>
>En comparación con el índice de propiedades normal, el índice de propiedades de Lucene siempre se configura en modo asíncrono. Por lo tanto, es posible que los resultados devueltos por índice no siempre reflejen el estado más actualizado del repositorio.

>[!NOTE]
>
>Para obtener información más específica sobre el índice de propiedades de Lucene, consulte la página [](https://jackrabbit.apache.org/oak/docs/query/lucene.html)de documentación de Apache Jackrabbit Oak Lucene.

### Análisis de Lucene {#lucene-analyzers}

Desde la versión 1.2.0, Oak admite analizadores Lucene.

Los analizadores se utilizan tanto cuando un documento está indexado como en el momento de la consulta. Un analizador examina el texto de los campos y genera un flujo de token. Los analizadores de Lucene se componen de una serie de clases de tokenizer y de filtro.

Los analizadores se pueden configurar mediante el `analyzers` nodo (de tipo `nt:unstructured`) dentro de la `oak:index` definición.

El analizador predeterminado de un índice se configura en el elemento secundario del nodo de analizadores `default` .

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>Para obtener una lista de los analizadores disponibles, consulte la documentación de la API de la versión de Lucene que está utilizando.

#### Especificación de la clase Analyzer directamente {#specifying-the-analyzer-class-directly}

Si desea utilizar algún analizador de fuera de la caja, puede configurarlo siguiendo el procedimiento siguiente:

1. Busque el índice con el que desea utilizar el analizador en el `oak:index` nodo.

1. En el índice, cree un nodo secundario llamado `default` de tipo `nt:unstructured`.

1. Agregue una propiedad al nodo predeterminado con las siguientes propiedades:

   * **Nombre:** `class`
   * **Tipo:** `String`
   * **** Valor: `org.apache.lucene.analysis.standard.StandardAnalyzer`
   El valor es el nombre de la clase de analizador que desea utilizar.

   También puede configurar el analizador para que se utilice con una versión lucene específica mediante la propiedad `luceneMatchVersion` string opcional. Un sintax válido para utilizarlo con Lucene 4.7 sería:

   * **Nombre:** `luceneMatchVersion`
   * **Tipo:** `String`
   * **** Valor: `LUCENE_47`
   Si no `luceneMatchVersion` se proporciona, Oak utilizará la versión de Lucene con la que se envía.

1. Si desea agregar un archivo de palabras clave a las configuraciones del analizador, puede crear un nuevo nodo debajo del `default` que tenga las siguientes propiedades:

   * **Nombre:** `stopwords`
   * **Tipo:** `nt:file`

#### Creación de analizadores mediante la composición {#creating-analyzers-via-composition}

Los analizadores también se pueden componer según `Tokenizers`, `TokenFilters` y `CharFilters`. Puede hacerlo especificando un analizador y creando nodos secundarios de sus tokenizadores y filtros opcionales que se aplicarán en orden de lista. Consulte también [https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

Considere esta estructura de nodos como un ejemplo:

* **Nombre:** `analyzers`

   * **Nombre:** `default`

      * **Nombre:** `charFilters`
      * **Tipo:** `nt:unstructured`

         * **Nombre:** `HTMLStrip`
         * **Nombre:** `Mapping`
      * **Nombre:** `tokenizer`

         * **Nombre de propiedad:** `name`

            * **Tipo:** `String`
            * **** Valor: `Standard`
      * **Nombre:** `filters`
      * **Tipo:** `nt:unstructured`

         * **Nombre:** `LowerCase`
         * **Nombre:** `Stop`

            * **** Nombre de propiedad: `words`

               * **Tipo:** `String`
               * **** Valor: `stop1.txt, stop2.txt`
            * **Nombre:** `stop1.txt`

               * **Tipo:** `nt:file`
            * **Nombre:** `stop2.txt`

               * **Tipo:** `nt:file`





El nombre de los filtros, charFilters y los tokenizadores se forman eliminando los sufijos de fábrica. Así:

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` se convierte `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` se convierte `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` se convierte `Stop`

Cualquier parámetro de configuración requerido para la fábrica se especifica como propiedad del código en cuestión.

En casos como cargar palabras de detención en las que es necesario cargar contenido de archivos externos, el contenido se puede proporcionar creando un nodo secundario de `nt:file` tipo para el archivo en cuestión.

### El índice Solr {#the-solr-index}

El propósito del índice Solr es principalmente la búsqueda de texto completo, pero también puede utilizarse para indexar la búsqueda por ruta, restricciones de propiedad y restricciones de tipo principal. Esto significa que el índice Solr en Oak puede utilizarse para cualquier tipo de consulta JCR.

La integración en AEM se produce a nivel de repositorio, de modo que Solr es uno de los índices posibles que se puede utilizar en Oak, la nueva implementación de repositorio enviada con AEM.

Se puede configurar para que funcione como servidor incrustado con la instancia de AEM o como servidor remoto.

### Configuración de AEM con un servidor Solr incrustado {#configuring-aem-with-an-embedded-solr-server}

>[!CAUTION]
>
>No utilice un servidor Solr incrustado en un entorno de producción. Sólo debe utilizarse en un entorno de desarrollo.

AEM se puede utilizar con un servidor Solr incrustado que se puede configurar mediante la consola web. En este caso, el servidor Solr se ejecutará en el mismo JVM que la instancia de AEM a la que está incrustado.

Puede configurar el servidor Solr incrustado mediante:

1. Ir a la consola web en `https://serveraddress:4502/system/console/configMgr`
1. Busque &quot;**Oak Solr server provider**&quot;.
1. Pulse el botón de edición y, en la siguiente ventana, defina el tipo de servidor como Solar **incrustado** en la lista desplegable.

1. A continuación, edite &quot;**Oak Solr incrustado configuración** del servidor&quot; y cree una configuración. Para obtener más información sobre las opciones de configuración, visite el sitio web [de](https://lucene.apache.org/solr/documentation.html)Apache Solr.

   >[!NOTE]
   >
   >La configuración del directorio de inicio de Solr (solr.home.path) buscará una carpeta con el mismo nombre en la carpeta de instalación de AEM.

1. Abra CRXDE e inicie sesión como administrador.
1. Agregue un nodo llamado **solrlndex** de tipo **oak:QueryIndexDefinition** en **oak:index** con las siguientes propiedades:

   * **** type: `solr`(de tipo String)
   * **** asíncrono: `async`(de tipo String)
   * **** reindexar: `true`(de tipo booleano)

1. Guarde los cambios.

### Configuración de AEM con un único servidor remoto Solr {#configuring-aem-with-a-single-remote-solr-server}

AEM también se puede configurar para que funcione con una instancia de servidor remoto de Solr:

1. Descargue y extraiga la última versión de Solr. Para obtener más información sobre cómo hacerlo, consulte la documentación [de instalación de](https://cwiki.apache.org/confluence/display/solr/Installing+Solr)Apache Solr.
1. Ahora, cree dos fragmentos de Solr. Para ello, cree carpetas para cada elemento compartido en la carpeta en la que se ha realizado la copia de seguridad de Solr:

   * Para el primer uso compartido, cree la carpeta:
   `<solrunpackdirectory>\aemsolr1\node1`

   * Para el segundo tablero, cree la carpeta:
   `<solrunpackdirectory>\aemsolr2\node2`

1. Busque la instancia de ejemplo en el paquete Solr. Generalmente se encuentra en una carpeta llamada &quot; `example`&quot; en la raíz del paquete.
1. Copie las siguientes carpetas de la instancia de ejemplo en las dos carpetas compartidas ( `aemsolr1\node1` y `aemsolr2\node2`):

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. Cree una nueva carpeta llamada &quot; `cfg`&quot; en cada una de las dos carpetas compartidas.
1. Coloque los archivos de configuración Solr y Zookeeper en las `cfg` carpetas recién creadas.

   >[!NOTE]
   >
   >Para obtener más información sobre la configuración de Solr y ZooKeeper, consulte la documentación [de Configuración de](https://wiki.apache.org/solr/ConfiguringSolr) Solr y la Guía [de introducción de](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html)ZooKeeper.

1. Inicie el primer uso compartido con la compatibilidad con ZooKeeper. Para ello, vaya a `aemsolr1\node1` y ejecute el siguiente comando:

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. Para iniciar el segundo uso compartido, vaya a `aemsolr2\node2` y ejecute el siguiente comando:

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. Una vez iniciados los dos shards, compruebe que todo esté activo y en funcionamiento conectándose a la interfaz de Solr en `http://localhost:8983/solr/#/`
1. Inicie AEM y vaya a la consola web en `http://localhost:4502/system/console/configMgr`
1. Defina la siguiente configuración en Configuración **del servidor remoto** Oak Solr:

   * Solr HTTP URL: `http://localhost:8983/solr/`

1. Elija **Solar** remoto en la lista desplegable en Proveedor del servidor **Oak Solr** .

1. Vaya a CRXDE e inicie sesión como administrador.
1. Cree un nuevo nodo denominado **solrIndex** en **roak:index** y defina las siguientes propiedades:

   * **** type: solr (de tipo String)
   * **** asíncrono: async (de tipo String)
   * **** reindexar: true (de tipo Boolean)

1. Guarde los cambios.

#### Configuración recomendada para Solr {#recommended-configuration-for-solr}

A continuación se muestra un ejemplo de una configuración base que puede utilizarse con las tres implementaciones de Solr descritas en este artículo. Aloja los índices de propiedades dedicados que ya están presentes en AEM y no deben usarse con otras aplicaciones.

Para utilizarla correctamente, debe colocar el contenido del archivo directamente en Solr Home Directory. En el caso de implementaciones de varios nodos, debe ir directamente a la carpeta raíz de cada nodo.

Archivos de configuración de Solr recomendados

[Obtener archivo](assets/recommended-conf.zip)

### Herramientas de indexación de AEM {#aem-indexing-tools}

AEM 6.1 también integra dos herramientas de indexación presentes en AEM 6.0 como parte del conjunto de herramientas de Adobe Consulting Services Commons:

1. **Explicar Query**, una herramienta diseñada para ayudar a los administradores a comprender cómo se ejecutan las consultas;
1. **Oak Index Manager**, una interfaz de usuario web para mantener índices existentes.

Ahora puede ponerse en contacto con ellos en **Herramientas - Operaciones - Tablero - Diagnóstico** desde la pantalla de bienvenida de AEM.

Para obtener más información sobre cómo utilizarlos, consulte la documentación [del panel de](/help/sites-administering/operations-dashboard.md)operaciones.

#### Creación de índices de propiedades mediante OSGi {#creating-property-indexes-via-osgi}

El paquete ACS Commons también expone configuraciones OSGi que pueden utilizarse para crear índices de propiedades.

Puede acceder a ella desde la consola web buscando &quot;**Asegúrese de que el índice** de propiedades Oak&quot;.

![chlimage_1-150](assets/chlimage_1-150.png)

### Solución de problemas de indexación {#troubleshooting-indexing-issues}

Pueden surgir situaciones en las que las consultas tardan mucho tiempo en ejecutarse y el tiempo de respuesta general del sistema es lento.

En esta sección se presenta un conjunto de recomendaciones sobre lo que debe hacerse para determinar la causa de esas cuestiones y asesorar sobre cómo resolverlas.

#### Preparación de la información de depuración para el análisis {#preparing-debugging-info-for-analysis}

La forma más sencilla de obtener la información requerida para la consulta que se está ejecutando es mediante la herramienta [](/help/sites-administering/operations-dashboard.md#explain-query)Explicar consulta. Esto le permitirá recopilar la información precisa necesaria para depurar una consulta lenta sin necesidad de consultar la información de nivel de registro. Esto es deseable si conoce la consulta que se está depurando.

Si esto no es posible por ningún motivo, puede recopilar los registros de indexación en un solo archivo y utilizarlos para solucionar un problema concreto.

#### Habilitar registro {#enable-logging}

Para habilitar el registro, debe habilitar los registros de nivel **DEBUG** para las categorías pertenecientes a la indexación y las consultas Oak. Estas categorías son:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

La categoría **com.day.cq.search** solo se aplica si utiliza la utilidad QueryBuilder proporcionada por AEM.

>[!NOTE]
>
>Es importante que los registros sólo estén configurados en DEBUG mientras se ejecute la consulta que desea solucionar los problemas; de lo contrario, se generará una gran cantidad de eventos en los registros con el paso del tiempo. Debido a esto, una vez recopilados los registros necesarios, vuelva al registro de nivel INFO para las categorías mencionadas anteriormente.

Puede habilitar el registro siguiendo este procedimiento:

1. Elija el explorador para `https://serveraddress:port/system/console/slinglog`
1. Haga clic en el botón **Agregar nuevo registrador** en la parte inferior de la consola.
1. En la fila recién creada, agregue las categorías mencionadas arriba. Puede utilizar el signo **+** para agregar más de una categoría a un único registrador.
1. Seleccione **DEBUG** en la lista desplegable **Nivel** de registro.
1. Establezca el archivo de salida en `logs/queryDebug.log`. Esto correlacionará todos los eventos DEBUG en un solo archivo de registro.
1. Ejecute la consulta o represente la página que utiliza la consulta que desea depurar.
1. Una vez ejecutada la consulta, vuelva a la consola de registro y cambie el nivel de registro del nuevo registrador creado a **INFO**.

#### Configuración de índice {#index-configuration}

La forma en que se evalúa la consulta se ve afectada en gran medida por la configuración del índice. Es importante obtener la configuración del índice para poder analizarla o enviarla a soporte técnico. Puede obtener la configuración como un paquete de contenido o una representación JSON.

Como en la mayoría de los casos, la configuración de indización se almacena bajo el `/oak:index` nodo en CRXDE, puede obtener la versión JSON en:

`https://serveraddress:port/oak:index.tidy.-1.json`

Si el índice está configurado en una ubicación diferente, cambie la ruta en consecuencia.

#### Salida MBean {#mbean-output}

En algunos casos, resulta útil proporcionar el resultado de MBeans relacionados con el índice para la depuración. Puede hacerlo mediante:

1. Ir a la consola JMX en:
   `https://serveraddress:port/system/console/jmx`

1. Busque los siguientes MBeans:

   * Estadísticas del índice Lucene
   * Estadísticas de soporte de CopyOnRead
   * Estadísticas de consulta Oak
   * IndexStats

1. Haga clic en cada MBeans para obtener las estadísticas de rendimiento. Cree una captura de pantalla o anótela en caso de que sea necesario enviar la información para que sea compatible.

También puede obtener la variante JSON de estas estadísticas en las siguientes direcciones URL:

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

También puede proporcionar una salida JMX consolidada mediante `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`. Esto incluiría todos los detalles de MBean relacionados con Oak en formato JSON.

#### Otros detalles {#other-details}

Puede recopilar detalles adicionales para ayudar a solucionar el problema, como:

1. La versión Oak en la que se está ejecutando su instancia. Puede ver esto abriendo CRXDE y mirando la versión en la esquina inferior derecha de la página de bienvenida, o comprobando la versión del `org.apache.jackrabbit.oak-core` paquete.
1. El resultado del depurador QueryBuilder de la consulta problemática. Se puede acceder al depurador en: `https://serveraddress:port/libs/cq/search/content/querydebug.html`

