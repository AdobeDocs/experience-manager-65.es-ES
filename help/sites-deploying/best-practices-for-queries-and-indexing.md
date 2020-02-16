---
title: Prácticas recomendadas para consultas e indexación
seo-title: Prácticas recomendadas para consultas e indexación
description: Este artículo proporciona directrices sobre cómo optimizar los índices y las consultas.
seo-description: Este artículo proporciona directrices sobre cómo optimizar los índices y las consultas.
uuid: 0609935a-4a72-4b8e-a28e-daede9fc05f4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3f06f7a1-bdf0-4700-8a7f-1d73151893ba
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Prácticas recomendadas para consultas e indexación{#best-practices-for-queries-and-indexing}

Junto con la transición a Oak en AEM 6, se han realizado algunos cambios importantes en la forma en que se administran las consultas y los índices. En Jackrabbit 2, todo el contenido se indexaba de forma predeterminada y se podía consultar libremente. En Oak, los índices se deben crear manualmente bajo el `oak:index` nodo. Una consulta se puede ejecutar sin índice, pero para conjuntos de datos grandes, se ejecutará muy lentamente o incluso se anulará.

En este artículo se describe cuándo crear índices y cuándo no se necesitan, los trucos para evitar el uso de consultas cuando no son necesarias y las sugerencias para optimizar los índices y las consultas a fin de que funcionen lo mejor posible.

Además, asegúrese de leer la documentación de [Oak sobre la escritura de consultas e índices](/help/sites-deploying/queries-and-indexing.md). Además de que los índices son un nuevo concepto en AEM 6, existen diferencias sintácticas en las consultas Oak que deben tenerse en cuenta al migrar código desde una instalación anterior de AEM.

## Cuándo utilizar las consultas {#when-to-use-queries}

### Diseño de Taxonomía y Repositorio {#repository-and-taxonomy-design}

Al diseñar la taxonomía de un repositorio, es necesario tener en cuenta varios factores. Estos incluyen controles de acceso, localización, herencia de propiedades de componente y página, entre otros.

Al diseñar una taxonomía que aborde estas preocupaciones, también es importante considerar la &quot;transferibilidad&quot; del diseño de indexación. En este contexto, la transferibilidad es la capacidad de una taxonomía que permite acceder al contenido de forma predecible en función de su ruta. Esto hará que sea más fácil mantener un sistema de mayor rendimiento que uno que requiera la ejecución de muchas consultas.

Además, al diseñar una taxonomía, es importante tener en cuenta si el pedido es importante. En los casos en los que no se requiere orden explícito y se espera un gran número de nodos del mismo nivel, es preferible utilizar un tipo de nodo no ordenado como `sling:Folder` o `oak:Unstructured`. En los casos en que se requiera la orden, `nt:unstructured` y `sling:OrderedFolder` sería más apropiado.

### Consultas en componentes {#queries-in-components}

Dado que las consultas pueden ser una de las operaciones más gravosas que se realizan en un sistema AEM, es recomendable evitarlas en los componentes. Hacer que se ejecuten varias consultas cada vez que se procesa una página puede degradar el rendimiento del sistema. Existen dos estrategias que pueden utilizarse para evitar la ejecución de consultas al procesar componentes: **atravesando nodos** y **recuperando previamente resultados**.

#### Nodos de recorrido {#traversing-nodes}

Si el repositorio está diseñado de tal manera que permite conocer previamente la ubicación de los datos requeridos, se puede implementar el código que recupera estos datos de las rutas necesarias sin tener que ejecutar consultas para encontrarlos.

Un ejemplo de esto sería la representación de contenido que se ajusta a una determinada categoría. Un método sería organizar el contenido con una propiedad de categoría que se pueda consultar para rellenar un componente que muestre los elementos de una categoría.

Un mejor método sería estructurar este contenido en una taxonomía por categoría para que se pueda recuperar manualmente.

Por ejemplo, si el contenido se almacena en una taxonomía similar a:

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

El `/content/myUnstructuredContent/parentCategory/childCategory` nodo simplemente se puede recuperar, sus elementos secundarios se pueden analizar y utilizar para procesar el componente.

Además, cuando se trata de un conjunto de resultados pequeño o homogéneo, puede ser más rápido recorrer el repositorio y recopilar los nodos necesarios, en lugar de crear una consulta para devolver el mismo conjunto de resultados. Como consideración general, deben evitarse las consultas cuando sea posible.

#### Recuperación previa de resultados {#prefetching-results}

A veces, el contenido o los requisitos que rodean al componente no permiten el uso de la transversal de nodos como método para recuperar los datos requeridos. En estos casos, es necesario ejecutar las consultas necesarias antes de que se represente el componente, de modo que se garantice un rendimiento óptimo para el usuario final.

Si los resultados necesarios para el componente se pueden calcular en el momento de su creación y no se espera que el contenido cambie, la consulta se puede ejecutar cuando el autor aplique la configuración en el cuadro de diálogo.

Si los datos o el contenido cambian con regularidad, la consulta se puede ejecutar según una programación o mediante un detector para actualizaciones de los datos subyacentes. A continuación, los resultados se pueden escribir en una ubicación compartida del repositorio. Cualquier componente que necesite estos datos puede extraer los valores de este nodo único sin necesidad de ejecutar una consulta en tiempo de ejecución.

## Optimización de consultas {#query-optimization}

Al ejecutar una consulta que no utiliza un índice, se registrarán advertencias relativas a la transversal de nodos. Si se trata de una consulta que se va a ejecutar con frecuencia, se debe crear un índice. Para determinar qué índice utiliza una consulta determinada, se recomienda la herramienta [](/help/sites-administering/operations-dashboard.md#explain-query) Explicar consulta. Para obtener más información, el registro DEBUG puede habilitarse para las API de búsqueda relevantes.

>[!NOTE]
>
>Después de modificar una definición de índice, es necesario volver a crear el índice (reindexado). Dependiendo del tamaño del índice, esto puede tardar algún tiempo en completarse.

Al ejecutar consultas complejas, puede haber casos en los que se desglose la consulta en varias consultas más pequeñas y se unan los datos a través del código después de que el hecho tenga un mayor rendimiento. La recomendación para estos casos es comparar el rendimiento de los dos enfoques para determinar qué opción sería mejor para el caso de uso en cuestión.

AEM permite escribir consultas de una de las tres maneras siguientes:

* Mediante las API de [QueryBuilder](/help/sites-developing/querybuilder-api.md) (recomendado)
* Uso de XPath (recomendado)
* Uso de SQL2

Aunque todas las consultas se convierten a SQL2 antes de ejecutarse, la sobrecarga de la conversión de consultas es mínima y, por lo tanto, la mayor preocupación al elegir un idioma de consulta será la legibilidad y el nivel de comodidad del equipo de desarrollo.

>[!NOTE]
>
>Al utilizar QueryBuilder, determinará el recuento de resultados de forma predeterminada, que es más lento en Oak en comparación con las versiones anteriores de Jackrabbit. Para compensarlo, puede utilizar el parámetro [](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results)adivinarTotal.

### La herramienta Explicar consulta {#the-explain-query-tool}

Como con cualquier lenguaje de consulta, el primer paso para optimizar una consulta es comprender cómo se ejecutará. Para habilitar esta actividad, puede utilizar la herramienta [](/help/sites-administering/operations-dashboard.md#explain-query) Explicar consulta que forma parte del Tablero de operaciones. Con esta herramienta se puede conectar y explicar una consulta. Se mostrará una advertencia si la consulta causará problemas con un repositorio grande, así como con el tiempo de ejecución y los índices que se utilizarán. La herramienta también puede cargar una lista de consultas lentas y populares que se pueden explicar y optimizar.

### Registro DEBUG para consultas {#debug-logging-for-queries}

Para obtener información adicional sobre cómo Oak está eligiendo qué índice utilizar y cómo el motor de consulta está ejecutando una consulta, se puede agregar una configuración de registro **DEBUG** para los siguientes paquetes:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

Asegúrese de eliminar este registrador cuando haya terminado de depurar la consulta, ya que generará mucha actividad y, finalmente, podrá rellenar el disco con archivos de registro.

Para obtener más información sobre cómo hacerlo, consulte la documentación sobre [registro](/help/sites-deploying/configure-logging.md).

### Estadísticas de índice {#index-statistics}

Lucene registra un frijol JMX que proporciona detalles sobre el contenido indexado, incluyendo el tamaño y el número de documentos presentes en cada uno de los índices.

Puede acceder a ella accediendo a la consola de JMX en `https://server:port/system/console/jmx`

Una vez que haya iniciado sesión en la consola JMX, realice una búsqueda de **Lucene Index Statistics** para encontrarla. Puede encontrar otras estadísticas de índice en el MBean de **IndexStats** .

Para obtener estadísticas de consulta, consulte el MBean llamado **Oak Query Statistics**.

Si desea explorar los índices usando una herramienta como [Luke](https://code.google.com/p/luke/), necesitará usar la consola Oak para volcar el índice desde el directorio del sistema de archivos `NodeStore` a un directorio del sistema de archivos. Para obtener instrucciones sobre cómo hacerlo, lea la documentación [de](https://jackrabbit.apache.org/oak/docs/query/lucene.html)Lucene.

También puede extraer los índices del sistema en formato JSON. Para ello, debe acceder a `https://server:port/oak:index.tidy.-1.json`

### Límites de la consulta {#query-limits}

**Durante el desarrollo**

Configure umbrales bajos para `oak.queryLimitInMemory` (p. ej. 10000) y roble. `queryLimitReads` (p. ej. 5000) y optimice la costosa consulta al visitar una excepción UnsupportedOperationException que dice &quot;La consulta lee más de nodos x...&quot;.

Esto ayuda a evitar consultas con muchos recursos (por ejemplo: no está respaldada por ningún índice o está respaldada por un índice de cobertura menos elevado). Por ejemplo: una consulta que lee 1 millón de nodos provocaría un aumento de la E/S y tendría un impacto negativo en el rendimiento general de la aplicación. Cualquier consulta que falle debido a los límites superiores debe analizarse y optimizarse.

#### **Post-implementación**{#post-deployment}

* Monitoree los registros de las consultas que activan el consumo de memoria de grandes nodos transversal o de gran consumo de memoria de pila: &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Optimice la consulta para reducir el número de nodos a través de los cuales se realiza la transferencia

* Monitoree los registros de las consultas que activan el consumo de memoria de montón grande:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Optimice la consulta para reducir el consumo de memoria de pila

En las versiones de AEM 6.0 - 6.2, puede ajustar el umbral para el recorrido de nodos mediante parámetros JVM en la secuencia de comandos de inicio de AEM para evitar que las consultas de gran tamaño sobrecarguen el entorno.

Los valores recomendados son:

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

En AEM 6.3, los dos parámetros anteriores están preconfigurados OTB y pueden persistir mediante OSGi QueryEngineSettings.

Más información disponible en : [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Sugerencias para crear índices eficientes {#tips-for-creating-efficient-indexes}

### ¿Debería crear un índice? {#should-i-create-an-index}

La primera pregunta que se debe hacer al crear o optimizar índices es si realmente son necesarios para una situación determinada. Si sólo va a ejecutar la consulta en cuestión una vez o sólo ocasionalmente y en un momento de poca actividad para el sistema a través de un proceso por lotes, puede que sea mejor no crear un índice en absoluto.

Después de crear un índice, cada vez que se actualicen los datos indexados, también se debe actualizar el índice. Dado que esto conlleva implicaciones de rendimiento para el sistema, los índices solo deben crearse cuando son realmente necesarios.

Además, los índices solo son útiles si los datos contenidos en el índice son lo suficientemente únicos como para garantizarlos. Considere un índice en un libro y los temas que abarca. Al indexar un conjunto de temas en un texto, normalmente habrá cientos o miles de entradas, lo que le permite saltar rápidamente a un subconjunto de páginas para encontrar rápidamente la información que busca. Si ese índice sólo tuviera dos o tres entradas, cada una de las cuales apunte a varios cientos de páginas, el índice no sería muy útil. Este mismo concepto se aplica a los índices de base de datos. Si solo hay un par de valores únicos, el índice no será muy útil. Dicho esto, un índice también puede llegar a ser demasiado grande para ser útil. Para ver las estadísticas de índice, consulte Estadísticas [de índice](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics) más arriba.

### ¿Índices de Lucene o Propiedad? {#lucene-or-property-indexes}

Los índices de Lucene se introdujeron en Oak 1.0.9 y ofrecen algunas optimizaciones poderosas sobre los índices de propiedades que se introdujeron en el lanzamiento inicial de AEM 6. Cuando decida si desea utilizar índices de Lucene o índices de propiedades, tenga en cuenta lo siguiente:

* Los índices de Lucene ofrecen muchas más funciones que los índices de propiedades. Por ejemplo, un índice de propiedades solo puede indexar una propiedad única, mientras que un índice de Lucene puede incluir muchas. Para obtener más información sobre todas las funciones disponibles en los índices de Lucene, consulte la [documentación](https://jackrabbit.apache.org/oak/docs/query/lucene.html).
* Los índices de Lucene son asincrónicos. Aunque esto ofrece un considerable aumento del rendimiento, también puede provocar un retraso entre el momento en que se escriben los datos en el repositorio y el momento en que se actualiza el índice. Si es vital que las consultas demuestren resultados 100% precisos, se requiere un índice de propiedades.
* Al ser asincrónicos, los índices de Lucene no pueden imponer restricciones de exclusividad. Si esto es necesario, deberá establecerse un índice de propiedades.

En general, se recomienda utilizar los índices de Lucene a menos que haya una necesidad imperiosa de utilizar los índices de propiedades para que pueda obtener los beneficios de un mayor rendimiento y flexibilidad.

### Indexación de solr {#solr-indexing}

AEM también es compatible con la indexación Solr de forma predeterminada. Esto se aprovecha principalmente para admitir la búsqueda de texto completo, pero también puede utilizarse para admitir cualquier tipo de consulta JCR. Se debe tener en cuenta Solr cuando las instancias de AEM no tienen la capacidad de CPU para gestionar el número de consultas necesarias en implementaciones intensivas de búsqueda, como los sitios web impulsados por la búsqueda con un número elevado de usuarios simultáneos. De lo contrario, Solr se puede implementar en un enfoque basado en bots para aprovechar algunas de las características más avanzadas de la plataforma.

Los índices de Solr se pueden configurar para ejecutarse integrados en el servidor AEM para entornos de desarrollo o pueden descargarse en una instancia remota para mejorar la escalabilidad de búsqueda en los entornos de producción y ensayo. Aunque la descarga de la búsqueda mejorará la escalabilidad, introducirá latencia y por ello no se recomienda a menos que sea necesario. Para obtener más información acerca de cómo configurar la integración de Solr y cómo crear índices de Solr, consulte la documentación [Consultas de](/help/sites-deploying/queries-and-indexing.md#the-solr-index)Oak e Indexación.

>[!NOTE]
>
>Si se toma el enfoque de búsqueda integrada de Solr, se podría descargar la indización en un servidor Solr. Si se utilizan las características más avanzadas del servidor Solr mediante un método basado en el explorador, será necesario realizar un trabajo de configuración adicional. Headwire ha creado un conector [de código](https://www.aemsolrsearch.com/#/) abierto para acelerar estos tipos de implementaciones.

La desventaja de este enfoque es que, aunque de forma predeterminada, las consultas AEM respetarán las ACL y, por tanto, ocultarán los resultados a los que un usuario no tiene acceso, la externalización de la búsqueda en un servidor Solr no admitirá esta función. Si la búsqueda se va a externalizar de esta manera, se debe tener especial cuidado en garantizar que los usuarios no reciban los resultados que no deben ver.

En los casos de uso potencial en que este enfoque pueda ser adecuado se dan casos en que es posible que sea necesario agregar datos de búsqueda de múltiples fuentes. Por ejemplo, es posible que un sitio esté alojado en AEM, así como un segundo sitio en una plataforma de terceros. Solr se puede configurar para rastrear el contenido de ambos sitios y almacenarlo en un índice agregado. Esto permitiría realizar búsquedas entre sitios.

### Design Considerations {#design-considerations}

La documentación de Oak para los índices de Lucene enumera varias consideraciones que deben tenerse en cuenta al diseñar los índices:

* Si la consulta utiliza diferentes restricciones de ruta, utilice `evaluatePathRestrictions`. Esto permitirá que la consulta devuelva el subconjunto de resultados bajo la ruta especificada y luego los filtre según la consulta. De lo contrario, la consulta buscará todos los resultados que coincidan con los parámetros de consulta en el repositorio y luego los filtrará según la ruta.
* Si la consulta utiliza la ordenación, tenga una definición de propiedad explícita para la propiedad ordenada y defina `ordered` en `true` para ella. Esto permitirá que los resultados se ordenen como tales en el índice y se ahorren en costosas operaciones de ordenación en tiempo de ejecución de la consulta.

* Ponga lo que se necesita en el índice. La adición de características o propiedades innecesarias hará que el índice crezca y ralentice el rendimiento.
* En un índice de propiedades, tener un nombre de propiedad único ayudaría a reducir el tamaño de un índice, pero en el caso de los índices de Lucene, el uso de `nodeTypes` y `mixins` debería hacerse para lograr índices coherentes. Consultar un elemento específico `nodeType` o `mixin` será más eficaz que consultar `nt:base`. Al utilizar este método, defina `indexRules` para el `nodeTypes` objeto en cuestión.

* Si las consultas solo se ejecutan bajo ciertas rutas, cree esos índices debajo de dichas rutas. No es necesario que los índices estén activos en la raíz del repositorio.
* Se recomienda utilizar un único índice cuando todas las propiedades indizadas estén relacionadas para permitir que Lucene evalúe tantas restricciones de propiedad como sea posible de forma nativa. Además, una consulta solo usará un índice, aunque se realice una combinación.

### CopyOnRead {#copyonread}

En los casos en que el `NodeStore` se almacena de forma remota, se puede activar una opción llamada `CopyOnRead` . La opción hará que el índice remoto se escriba en el sistema de archivos local cuando se lea. Esto puede ayudar a mejorar el rendimiento de las consultas que a menudo se ejecutan con estos índices remotos.

Esto se puede configurar en la consola OSGi bajo el servicio **LuceneIndexProvider** y se habilita de forma predeterminada a partir de Oak 1.0.13.

### Eliminación de índices {#removing-indexes}

Al eliminar un índice, siempre se recomienda deshabilitar temporalmente el índice estableciendo la propiedad en `type` `disabled` y realizando pruebas para asegurarse de que la aplicación funciona correctamente antes de eliminarla. Tenga en cuenta que un índice no se actualiza mientras está deshabilitado, por lo que es posible que no tenga el contenido correcto si se vuelve a activar y que sea necesario volver a indexarlo.

Después de quitar un índice de propiedad en una instancia de TarMK, será necesario ejecutar la compactación para recuperar cualquier espacio en disco que se estuviera utilizando. En el caso de los índices de Lucene, el contenido del índice real permanece en BlobStore, por lo que se requiere una recopilación de elementos no utilizados del almacén de datos.

Al eliminar un índice en una instancia de MongoDB, el costo de eliminación es proporcional al número de nodos en el índice. Dado que la eliminación de un índice grande puede causar problemas, el método recomendado es deshabilitar el índice y eliminarlo únicamente durante una ventana de mantenimiento, utilizando una herramienta como **oak-mongo.js**. Tenga en cuenta que este método no debe emplearse para el contenido normal de nodos, ya que puede introducir incoherencias de datos.

>[!NOTE]
>
>Para obtener más información sobre oak-mongo.js, consulte la sección [Herramientas de la línea de](https://jackrabbit.apache.org/oak/docs/command_line.html) comandos de la documentación de Oak.

## Volver a indexar {#re-indexing}

Esta sección describe los **únicos** motivos aceptables para volver a indexar los índices Oak.

Fuera de los motivos que se describen a continuación, iniciar los reíndices de Oak **no cambiará** el comportamiento ni resolverá los problemas, y aumentará innecesariamente la carga en AEM.

Se evitará la reindexación de los índices de roble, a menos que se trate de una de las razones que figuran en los cuadros siguientes.

>[!NOTE]
>
>Antes de consultar las tablas siguientes para determinar si es útil volver a indexar,** siempre **verificar:
>
>* la consulta es correcta
>* la consulta se resuelve en el índice esperado (mediante [Explicar consulta](/help/sites-administering/operations-dashboard.md#diagnosis-tools))
>* el proceso de indexación ha finalizado
>



### Cambios en la configuración del índice Oak {#oak-index-configuration-changes}

Las únicas condiciones no aceptables para volver a indexar los índices de roble son si la configuración de un índice de roble ha cambiado.

*La reindexación siempre debe abordarse teniendo debidamente en cuenta su impacto en el rendimiento general de AEM y realizarse durante períodos de baja actividad o ventanas de mantenimiento.*

A continuación se detallan los posibles problemas, junto con las resoluciones:

* [Cambio de definición de índice de propiedades](#property-index-definition-change)
* [Cambio de definición de índice de Lucene](#lucene-index-definition-change)

#### Cambio de definición de índice de propiedades {#property-index-definition-change}

* Se aplica para/si:

   * Todas las versiones Oak
   * Sólo índices [de propiedades](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* Síntomas:

   * Los nodos existentes antes de la actualización de definición del índice de propiedades no aparecen en los resultados

* Cómo verificar:

   * Determine si los nodos que faltan se crearon o modificaron antes de la implementación de la definición de índice actualizada.
   * Verificar las propiedades `jcr:created` o `jcr:lastModified` de cualquier nodo que falte con respecto al tiempo de modificación del índice

* Cómo resolver:

   * [Volver a indexar](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) el índice de luminosidad
   * Alternativamente, toque (realice una operación de escritura benigna) a los nodos que faltan

      * Requiere toques manuales o código personalizado
      * Requiere que se conozca el conjunto de nodos que faltan
      * Requiere cambiar cualquier propiedad del nodo

#### Cambio de definición de índice de Lucene {#lucene-index-definition-change}

* Se aplica para/si:

   * Todas las versiones Oak
   * Sólo índices [de lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Síntomas:

   * El índice Lucene no contiene los resultados esperados
   * Los resultados de la consulta no reflejan el comportamiento esperado de la definición del índice
   * El plan de consulta no informa de la salida esperada según la definición del índice

* Cómo verificar:

   * Verifique que la definición del índice se haya cambiado usando el método JMX Mbean (LuceneIndex), estadísticas del índice de Lucene `diffStoredIndexDefinition`.

* Cómo resolver:

   * Versiones Oak anteriores a la versión 1.6:

      * [Volver a indexar](#how-to-re-index) el índice de luminosidad
   * Versiones Oak 1.6+

      * Si los cambios no afectan al contenido existente, solo se necesita una actualización

         * [Actualice](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) el índice de luminancia estableciendo [oak:queryIndexDefinition]@refresh=true
      * De lo contrario, [vuelva a indexar](#how-to-re-index) el índice de luminosidad

         * Nota: El estado de índice desde la última reindexación correcta (o indexación inicial) se utilizará hasta que se active una nueva reindexación



### Situaciones de error y excepcionales {#erring-and-exceptional-situations}

En la siguiente tabla se describen las únicas situaciones de error aceptables y excepcionales en las que la reindexación de índices de roble resolverá el problema.

Si se produce un problema en AEM que no coincide con los criterios descritos a continuación, **no vuelva** a indexar ningún índice, ya que no resolverá el problema.

A continuación se detallan los posibles problemas, junto con las resoluciones:

* [Falta el binario del índice Lucene](#lucene-index-binary-is-missing)
* [El binario del índice Lucene está dañado](#lucene-index-binary-is-corrupt)

#### Falta el binario del índice Lucene {#lucene-index-binary-is-missing}

* Se aplica para/si:

   * Todas las versiones Oak
   * Sólo índices [de lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Síntomas:

   * El índice Lucene no contiene los resultados esperados

* Cómo verificar:

   * El archivo de registro de errores contiene una excepción que indica que falta un binario del índice Lucene

* Cómo resolver:

   * Realizar una comprobación de repositorio de travesía; por ejemplo:

      [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

      recorrer el repositorio determina si faltan otros binarios (además de los archivos de lucene)

   * Si faltan archivos binarios que no sean índices de lucene, restaure desde la copia de seguridad
   * De lo contrario, [vuelva a indexar](#how-to-re-index) *todos los* índices de lucene
   * Nota:

      Esta condición indica un almacén de datos mal configurado que puede resultar en CUALQUIER binario (p. ej. recursos binarios) para desaparecer.

      En este caso, restaure a la última versión correcta conocida del repositorio para recuperar todos los binarios que faltan.

#### El binario del índice Lucene está dañado {#lucene-index-binary-is-corrupt}

* Se aplica para/si:

   * Todas las versiones Oak
   * Sólo índices [de lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Síntomas:

   * El índice Lucene no contiene los resultados esperados

* Cómo verificar:

   * El error `AsyncIndexUpdate` (cada 5 s) fallará con una excepción en error.log:

      `...a Lucene index file is corrupt...`

* Cómo resolver:

   * Eliminar la copia local del índice de lucene

      1. Detener AEM
      1. Eliminar la copia local del índice de lucene en `crx-quickstart/repository/index`
      1. Reiniciar AEM
   * Si esto no resuelve el problema y las `AsyncIndexUpdate` excepciones persisten:

      1. [Volver a indexar](#how-to-re-index) el índice de error
      1. Presente también un ticket de asistencia técnica [de](https://helpx.adobe.com/support.html) Adobe


### Cómo volver a indexar {#how-to-re-index}

>[!NOTE]
>
>En AEM 6.5, [oak-run.jar es el ÚNICO método](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree) admitido para volver a indexar en repositorios MongoMK o RDBMK.

#### Volver a indexar índices de propiedades {#re-indexing-property-indexes}

* Use [oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) para volver a indexar el índice de propiedades
* Establezca la propiedad async-reindex en true en el índice de propiedades

   * `[oak:queryIndexDefinition]@reindex-async=true`

* Volver a indexar el índice de propiedades de forma asíncrona mediante la consola web mediante **PropertyIndexAsyncReindex** MBean;

   por ejemplo,

   [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### Reindexación de los índices de propiedades de Lucene {#re-indexing-lucene-property-indexes}

* Use [oak-run.jar para volver a indexar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) el índice de la propiedad Lucene.
* Establezca la propiedad async-reindex en true en el índice de la propiedad lucene

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>La sección anterior resume y enmarca la guía de reindexación Oak de la documentación [de](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing) Apache Oak en el contexto de AEM.

### Texto Pre-extracción de binarios {#text-pre-extraction-of-binaries}

La pre-extracción de texto es el proceso de extraer y procesar texto de los binarios, directamente desde el almacén de datos a través de un proceso aislado, y exponer directamente el texto extraído a los posteriores re/indexados de los índices Oak.

* Se recomienda la extracción previa de texto oak para volver a indexar los índices Lucene en repositorios con grandes volúmenes de archivos (binarios) que contienen texto extraíble (p. ej. PDF, documentos de Word, PPT, TXT, etc.) que cumplen los requisitos para la búsqueda de texto completo mediante índices Oak implementados; por ejemplo `/oak:index/damAssetLucene`.
* La pre-extracción de texto sólo beneficiará la re-indexación de los índices Lucene, y NO de los índices de propiedades Oak, ya que los índices de propiedades no extraen texto de los binarios.
* La preextracción de texto tiene un gran impacto positivo cuando la reindexación de texto completo de binarios con mucho texto (PDF, Doc, TXT, etc.), donde como repositorio de imágenes no disfrutará de la misma eficacia, ya que las imágenes no contienen texto extraíble.
* La extracción previa de texto realiza la extracción de texto relacionado con la búsqueda de texto completo de una manera excesivamente eficiente, y la expone al proceso de indexación/re de Oak de una manera que es excesivamente eficiente de consumir.

#### ¿Cuándo se puede utilizar la preextracción de texto? {#when-can-text-pre-extraction-be-used}

Reindexación de un índice de lucene **existente** con extracción binaria habilitada

* Volver a indexar el procesamiento de **todo** el contenido candidato en el repositorio; cuando los binarios de los que se va a extraer texto completo son numerosos o complejos, se coloca en AEM una mayor carga computacional para realizar la extracción de texto completo. La extracción previa de texto mueve el &quot;trabajo costoso de la computación&quot; de la extracción de texto a un proceso aislado que accede directamente al almacén de datos de AEM, evitando así la sobrecarga y la contención de recursos en AEM.

Compatibilidad con la implementación de un **nuevo** índice lucene en AEM con extracción binaria habilitada

* Cuando se implementa un nuevo índice (con la extracción binaria habilitada) en AEM, Oak indexa automáticamente todo el contenido candidato en la siguiente ejecución asincrónica de índice de texto completo. Por los mismos motivos descritos en la reindexación anterior, esto puede resultar en una carga indebida en AEM.

#### ¿Cuándo se puede utilizar la preextracción de texto NO? {#when-can-text-pre-extraction-not-be-used}

La extracción previa de texto no se puede utilizar para el nuevo contenido agregado al repositorio, ni tampoco es necesario.

El nuevo contenido se agrega al repositorio de forma natural e incremental mediante el proceso de indexación de texto completo asincrónico (de forma predeterminada, cada 5 segundos).

Bajo el funcionamiento normal de AEM, por ejemplo, al cargar recursos a través de la interfaz de usuario web o mediante la ingesta programática de recursos, AEM indexará automáticamente e incrementalmente el nuevo contenido binario. Dado que la cantidad de datos es incremental y relativamente pequeña (aproximadamente la cantidad de datos que se puede mantener en el repositorio en 5 segundos), AEM puede realizar la extracción de texto completo de los binarios durante la indexación sin afectar al rendimiento general del sistema.

#### Requisitos previos para utilizar la preextracción de texto {#prerequisites-to-using-text-pre-extraction}

* Se volverá a indexar un índice de lucene que realiza una extracción binaria de texto completo o implementa un nuevo índice que incluirá binarios de índice de texto completo de contenido existente
* El contenido (binarios) del que se debe extraer texto previamente debe estar en el repositorio
* Ventana de mantenimiento para generar el archivo CSV Y para realizar la reindexación final
* Versión Oak: 1.0.18+, 1.2.3+
* [oak-run.](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)jarversion 1.7.4+
* Una carpeta o un recurso compartido del sistema de archivos para almacenar el texto extraído al que se puede acceder desde las instancias de AEM de indexación

   * La configuración OSGi de preextracción de texto requiere una ruta de acceso del sistema de archivos a los archivos de texto extraídos, por lo que se debe acceder a ellos directamente desde la instancia de AEM (unidad local o montaje de uso compartido de archivos)

#### Cómo realizar la preextracción de texto {#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***Los comandos oak-run.jar que se describen a continuación están totalmente enumerados en[https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>El diagrama y los pasos anteriores sirven para explicar y complementar los pasos de preextracción de texto técnico descritos en la documentación de Apache Oak.

![Flujo del proceso de preextracción de texto](assets/chlimage_1-139.png)

**Generar lista de contenido para extraer previamente**

*Ejecute el paso 1(a-b) durante una ventana de mantenimiento/período de bajo uso a medida que se atraviesa el almacén de nodos durante esta operación, lo que puede suponer una carga significativa en el sistema.*

1 bis. Ejecutar `oak-run.jar --generate` para crear una lista de nodos que tendrán su texto previamente extraído.

1 ter. La lista de nodos (1a) se almacena en el sistema de archivos como archivo CSV

Tenga en cuenta que todo el almacén de nodos se recorre (según lo especificado por las rutas en el comando oak-run) cada vez que `--generate` se ejecuta y se crea un **nuevo** archivo CSV. El archivo CSV **no se reutiliza** entre ejecuciones discretas del proceso de preextracción de texto (pasos 1 a 2).

**Extraer texto previamente al sistema de archivos**

*El paso 2(a-c) se puede ejecutar durante el funcionamiento normal de AEM si solo interactúa con el almacén de datos.*

2 bis. Ejecutar `oak-run.jar --tika` para extraer previamente texto para los nodos binarios enumerados en el archivo CSV generado en (1b)

2 ter. El proceso iniciado en (2a) accede directamente a los nodos binarios definidos en el CSV en el Almacén de datos y extrae texto.

2 quater.  El texto extraído se almacena en el sistema de archivos en un formato que el proceso de reindexación Oak no permite (3a)

El texto extraído previamente se identifica en el CSV mediante la huella digital binaria. Si el archivo binario es el mismo, se puede utilizar el mismo texto preextraído en todas las instancias de AEM. Dado que AEM Publish suele ser un subconjunto de AEM Author, el texto extraído previamente de AEM Author también se puede utilizar para volver a indexar AEM Publish (suponiendo que AEM Publish tiene acceso al sistema de archivos a los archivos de texto extraídos).

El texto extraído previamente se puede añadir de forma incremental a lo largo del tiempo. La preextracción de texto omitirá la extracción de archivos binarios extraídos anteriormente, por lo que es recomendable mantener el texto extraído previamente en caso de que la reindexación deba volver a producirse en el futuro (suponiendo que el contenido extraído no sea demasiado grande. Si es así, evalúe el compactado del contenido en el interín, ya que el texto se comprime bien).

**Volver a indexar índices Oak, abastecimiento de texto completo a partir de archivos de texto extraído**

*Ejecute la reindexación (pasos 3a-b) durante un período de mantenimiento/bajo uso, ya que durante esta operación se atraviesa el almacén de nodos, lo que puede suponer una carga significativa en el sistema.*

3 bis. [La reindexación](#how-to-re-index) de los índices de Lucene se invoca en AEM

3 ter. La configuración OSGi de Apache Jackrabbit Oak DataStore PreExtractTextProvider (configurada para apuntar el texto extraído a través de una ruta de sistema de archivos) indica a Oak que debe buscar texto completo a partir de los Archivos extraídos y evita directamente ingresar y procesar los datos almacenados en el repositorio.

