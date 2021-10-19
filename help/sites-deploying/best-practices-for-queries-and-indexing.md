---
title: Prácticas recomendadas para consultas e indexación
seo-title: Best Practices for Queries and Indexing
description: Este artículo proporciona directrices sobre cómo optimizar los índices y las consultas.
seo-description: This article provides guidelines on how to optimize your indexes and queries.
uuid: 0609935a-4a72-4b8e-a28e-daede9fc05f4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3f06f7a1-bdf0-4700-8a7f-1d73151893ba
exl-id: 6dfaa14d-5dcf-4e89-993a-8d476a36d668
source-git-commit: 52c8d4c425213718678543e9e9e8e5a4c2af4f95
workflow-type: tm+mt
source-wordcount: '4684'
ht-degree: 0%

---

# Prácticas recomendadas para consultas e indexación{#best-practices-for-queries-and-indexing}

Junto con la transición a Oak en el AEM 6, se hicieron algunos cambios importantes en la forma en que se administran las consultas y los índices. En Jackrabbit 2, todo el contenido se indexaba de forma predeterminada y se podía consultar libremente. En Oak, los índices deben crearse manualmente en el `oak:index` nodo . Una consulta se puede ejecutar sin un índice, pero para conjuntos de datos grandes, se ejecutará muy lentamente o incluso se anulará.

Este artículo describe cuándo crear índices y cuándo no se necesitan, los trucos para evitar usar consultas cuando no son necesarias y las sugerencias para optimizar sus índices y consultas para que rindan del modo más óptimo posible.

Además, asegúrese de leer el [Documentación de Oak sobre la escritura de consultas e índices](/help/sites-deploying/queries-and-indexing.md). Además de que los índices son un nuevo concepto en el AEM 6, hay diferencias sintácticas en las consultas Oak que deben tenerse en cuenta al migrar código de una instalación AEM anterior.

## Cuándo usar consultas {#when-to-use-queries}

### Diseño de Repositorio y Taxonomía {#repository-and-taxonomy-design}

Al diseñar la taxonomía de un repositorio, es necesario tener en cuenta varios factores. Estos incluyen controles de acceso, localización, herencia de propiedades de componentes y páginas, entre otros.

Al diseñar una taxonomía que aborde estas preocupaciones, también es importante considerar la &quot;transferibilidad&quot; del diseño de indexación. En este contexto, la transferibilidad es la capacidad de una taxonomía que permite acceder al contenido de forma predecible en función de su ruta. Esto hará que el sistema sea más eficaz y fácil de mantener que uno que requiera ejecutar muchas consultas.

Además, al diseñar una taxonomía, es importante considerar si el orden es importante. En los casos en los que no se requiere orden explícito y se espera un gran número de nodos del mismo nivel, se prefiere utilizar un tipo de nodo no ordenado como `sling:Folder` o `oak:Unstructured`. En los casos en que se requiera la orden, `nt:unstructured` y `sling:OrderedFolder` sería más apropiado.

### Consultas en componentes {#queries-in-components}

Dado que las consultas pueden ser una de las operaciones más gravosas realizadas en un sistema AEM, es aconsejable evitarlas en los componentes. A menudo, hacer que se ejecuten varias consultas cada vez que se procesa una página puede degradar el rendimiento del sistema. Existen dos estrategias que se pueden utilizar para evitar ejecutar consultas al procesar componentes: **atravesar nodos** y **recuperación previa de resultados**.

#### Recorrer nodos {#traversing-nodes}

Si el repositorio está diseñado de tal manera que permita un conocimiento previo de la ubicación de los datos requeridos, el código que recupera estos datos de las rutas necesarias se puede implementar sin tener que ejecutar consultas para encontrarlos.

Un ejemplo de esto sería la representación de contenido que se ajuste a una determinada categoría. Un método sería organizar el contenido con una propiedad de categoría que se pueda consultar para rellenar un componente que muestre elementos en una categoría.

Un mejor enfoque sería estructurar este contenido en una taxonomía por categoría para que se pueda recuperar manualmente.

Por ejemplo, si el contenido se almacena en una taxonomía similar a:

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

el `/content/myUnstructuredContent/parentCategory/childCategory` simplemente se puede recuperar, sus elementos secundarios se pueden analizar y utilizar para procesar el componente.

Además, cuando se trata de un conjunto de resultados pequeño o homogéneo, puede ser más rápido atravesar el repositorio y recopilar los nodos necesarios, en lugar de crear una consulta para devolver el mismo conjunto de resultados. Como consideración general, deben evitarse las consultas siempre que sea posible.

#### Recuperación previa de resultados {#prefetching-results}

A veces, el contenido o los requisitos relacionados con el componente no permiten el uso de la transversal de nodos como método para recuperar los datos necesarios. En estos casos, es necesario ejecutar las consultas necesarias antes de procesar el componente para garantizar un rendimiento óptimo para el usuario final.

Si los resultados necesarios para el componente se pueden calcular en el momento en que se crea y no hay expectativa de que el contenido cambie, la consulta se puede ejecutar cuando el autor aplique la configuración en el cuadro de diálogo.

Si los datos o el contenido cambian con regularidad, la consulta se puede ejecutar en una programación o a través de un oyente para buscar actualizaciones de los datos subyacentes. A continuación, los resultados se pueden escribir en una ubicación compartida del repositorio. Cualquier componente que necesite estos datos puede extraer los valores de este nodo único sin necesidad de ejecutar una consulta en tiempo de ejecución.

## Optimización de la consulta {#query-optimization}

Cuando se ejecuta una consulta que no utiliza un índice, se registrarán advertencias relativas a la travesía del nodo. Si se trata de una consulta que se va a ejecutar con frecuencia, se debe crear un índice. Para determinar qué índice utiliza una consulta determinada, la variable [Explicar la herramienta Consulta](/help/sites-administering/operations-dashboard.md#explain-query) se recomienda. Para obtener información adicional, el registro de depuración se puede habilitar para las API de búsqueda relevantes.

>[!NOTE]
>
>Después de modificar una definición de índice, es necesario volver a crear el índice (reindexado). Dependiendo del tamaño del índice, esto puede tardar algún tiempo en completarse.

Al ejecutar consultas complejas, puede haber casos en los que se desglose la consulta en varias consultas más pequeñas y se unirán los datos a través del código después de que el hecho tenga un mayor rendimiento. La recomendación para estos casos es comparar el rendimiento de los dos enfoques para determinar qué opción sería mejor para el caso de uso en cuestión.

AEM permite escribir consultas de una de las tres maneras siguientes:

* A través de la función [API de QueryBuilder](/help/sites-developing/querybuilder-api.md) (recomendado)
* Uso de XPath (recomendado)
* Uso de SQL2

Aunque todas las consultas se convierten a SQL2 antes de ejecutarse, la sobrecarga de la conversión de consultas es mínima y, por lo tanto, la preocupación buena al elegir un idioma de consulta será la legibilidad y el nivel de comodidad del equipo de desarrollo.

>[!NOTE]
>
>Al utilizar QueryBuilder, determinará el recuento de resultados de forma predeterminada, que es más lento en Oak en comparación con las versiones anteriores de Jackrabbit. Para compensarlo, puede usar la variable [Parámetro de adivinenTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results).

### La herramienta Explicar consulta {#the-explain-query-tool}

Como con cualquier idioma de consulta, el primer paso para optimizar una consulta es comprender cómo se ejecutará. Para habilitar esta actividad, puede usar la variable [Explicar la herramienta Consulta](/help/sites-administering/operations-dashboard.md#explain-query) que forma parte del panel de operaciones. Con esta herramienta, se puede conectar y explicar una consulta. Se mostrará una advertencia si la consulta causará problemas con un repositorio grande, así como con el tiempo de ejecución y los índices que se utilizarán. La herramienta también puede cargar una lista de consultas lentas y populares que luego se pueden explicar y optimizar.

### DEBUG Logging para consultas {#debug-logging-for-queries}

Para obtener información adicional sobre cómo Oak elige qué índice utilizar y cómo el motor de consulta está ejecutando realmente una consulta, una **DEBUG** la configuración de registro se puede agregar para los siguientes paquetes:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

Asegúrese de eliminar este registrador cuando haya terminado de depurar la consulta, ya que generará mucha actividad y eventualmente podrá rellenar el disco con archivos de registro.

Para obtener más información sobre cómo hacerlo, consulte la [Documentación de registro](/help/sites-deploying/configure-logging.md).

### Estadísticas de índice {#index-statistics}

Lucene registra un bean JMX que proporcionará detalles sobre contenido indexado, incluido el tamaño y número de documentos presentes en cada uno de los índices.

Puede acceder a ella accediendo a la consola JMX en `https://server:port/system/console/jmx`

Una vez que haya iniciado sesión en la consola JMX, realice una búsqueda de **Estadísticas del índice Lucene** para encontrarlo. Otras estadísticas de índice se pueden encontrar en la **IndexStats** MBean.

Para obtener estadísticas de consulta, eche un vistazo al MBean llamado **Estadísticas de consulta de Oak**.

Si desea profundizar en los índices utilizando una herramienta como [Luke](https://code.google.com/p/luke/), deberá utilizar la consola Oak para volcar el índice desde la `NodeStore` a un directorio del sistema de archivos. Para obtener instrucciones sobre cómo hacerlo, lea la [Documentación de Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

También puede extraer los índices en su sistema en formato JSON. Para ello, debe acceder a `https://server:port/oak:index.tidy.-1.json`

### Límites de la consulta {#query-limits}

**Durante el desarrollo**

Establecer umbrales bajos para `oak.queryLimitInMemory` (p. ej. 10000) y roble. `queryLimitReads` (p. ej. 5000) y optimice la costosa consulta al visitar una excepción UnsupportedOperationException que dice &quot;La consulta lee más de x nodos...&quot;.

Esto ayuda a evitar consultas intensivas en recursos (por ejemplo, no está respaldado por ningún índice o está respaldado por un índice menos abarcador). Por ejemplo, una consulta que lee un millón de nodos produciría un aumento de E/S y afectaría negativamente al rendimiento general de la aplicación. Cualquier consulta que falle debido a límites superiores debe analizarse y optimizarse.

#### **Posterior a la implementación** {#post-deployment}

* Monitorice los registros para las consultas que activan el consumo de memoria de gran nodo transversal o de gran pila: &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Optimizar la consulta para reducir el número de nodos recorridos

* Monitorice los registros de las consultas que activan el consumo de memoria de pila grande :

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Optimizar la consulta para reducir el consumo de memoria acumulada

Para AEM versiones 6.0 - 6.2, puede ajustar el umbral para la travesía de nodos a través de parámetros JVM en el script de inicio de AEM para evitar que las consultas grandes sobrecarguen el entorno.

Los valores recomendados son:

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

En AEM 6.3, los dos parámetros anteriores están preconfigurados en OOTB y pueden persistir a través de OSGi QueryEngineSettings.

Más información disponible en : [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Sugerencias para crear índices eficientes {#tips-for-creating-efficient-indexes}

### ¿Debería crear un índice? {#should-i-create-an-index}

La primera pregunta que se debe hacer al crear o optimizar índices es si realmente son necesarios para una situación determinada. Si sólo va a ejecutar la consulta en cuestión una vez o sólo ocasionalmente y en un momento de menor actividad para el sistema a través de un proceso por lotes, puede ser mejor no crear un índice en absoluto.

Después de crear un índice, cada vez que se actualizan los datos indexados, también se debe actualizar el índice. Dado que esto conlleva implicaciones de rendimiento para el sistema, los índices solo deben crearse cuando son realmente necesarios.

Además, los índices solo son útiles si los datos contenidos en el índice son lo suficientemente únicos como para garantizarlos. Consideremos un índice en un libro y los temas que abarca. Al indexar un conjunto de temas en un texto, normalmente habrá cientos o miles de entradas, lo que le permite saltar rápidamente a un subconjunto de páginas para encontrar rápidamente la información que está buscando. Si ese índice solo tuviera dos o tres entradas, cada una señalando varios cientos de páginas, el índice no sería muy útil. Este mismo concepto se aplica a los índices de base de datos. Si solo hay un par de valores únicos, el índice no será muy útil. Dicho esto, un índice también puede llegar a ser demasiado grande para ser útil. Para consultar las estadísticas de índices, consulte [Estadísticas de índice](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics) arriba.

### ¿Índices de Lucene o de Propiedad? {#lucene-or-property-indexes}

Los índices de Lucene se introdujeron en Oak 1.0.9 y ofrecen algunas optimizaciones poderosas sobre los índices de propiedades que se introdujeron en el primer lanzamiento de AEM 6. Cuando decida si desea utilizar índices de Lucene o índices de propiedades, tenga en cuenta lo siguiente:

* Los índices de Lucene ofrecen muchas más funciones que los índices de propiedades. Por ejemplo, un índice de propiedad solo puede indexar una sola propiedad mientras que un índice de Lucene puede incluir muchas. Para obtener más información sobre todas las funciones disponibles en los índices de Lucene, consulte la [documentación](https://jackrabbit.apache.org/oak/docs/query/lucene.html).
* Los índices de Lucene son asíncronos. Aunque esto ofrece un aumento considerable del rendimiento, también puede provocar un retraso entre el momento en que los datos se escriben en el repositorio y el momento en que se actualiza el índice. Si es vital que las consultas devuelvan resultados 100% precisos, se necesitaría un índice de propiedad.
* Al ser asíncronos, los índices de Lucene no pueden imponer restricciones de exclusividad. Si esto es necesario, deberá establecerse un índice de propiedad.

En general, se recomienda utilizar los índices de Lucene a menos que exista una necesidad imperiosa de usar índices de propiedades para poder obtener los beneficios de un mayor rendimiento y flexibilidad.

### Indexación de Solr {#solr-indexing}

AEM también es compatible con la indexación de Solr de forma predeterminada. Esto se aprovecha principalmente para admitir la búsqueda de texto completo, pero también se puede utilizar para admitir cualquier tipo de consulta JCR. Se debe tener en cuenta Solr cuando las instancias de AEM no tienen la capacidad de CPU para gestionar el número de consultas necesarias en implementaciones intensivas de búsqueda, como sitios web impulsados por búsquedas con un número elevado de usuarios simultáneos. Alternativamente, Solr se puede implementar en un enfoque basado en rastreadores para aprovechar algunas de las características más avanzadas de la plataforma.

Los índices Solr se pueden configurar para ejecutar integrados en el servidor de AEM para entornos de desarrollo o se pueden descargar a una instancia remota para mejorar la escalabilidad de búsqueda en los entornos de producción y ensayo. Aunque la descarga de la búsqueda mejora la escalabilidad, introduce latencia y, por ello, no se recomienda a menos que sea necesario. Para obtener más información sobre cómo configurar la integración de Solr y cómo crear índices de Solr, consulte la [Documentación de Consultas e Indexación de Oak](/help/sites-deploying/queries-and-indexing.md#the-solr-index).

>[!NOTE]
>
>Mientras toma el enfoque de búsqueda de Solr integrado, permitiría descargar la indexación a un servidor Solr. Si se utilizan las características más avanzadas del servidor Solr mediante un método basado en rastreadores, será necesario realizar un trabajo de configuración adicional. El alambre de techo ha creado un [conector de código abierto](https://www.aemsolrsearch.com/#/) para acelerar estos tipos de implementaciones.

La desventaja de este enfoque es que, aunque de forma predeterminada, las consultas de AEM respetarán las ACL y, por lo tanto, ocultarán los resultados a los que un usuario no tiene acceso, la externalización de la búsqueda a un servidor Solr no admitirá esta función. Si la búsqueda se va a externalizar de esta manera, se debe tener cuidado adicional para garantizar que los usuarios no reciban resultados que no deban ver.

Los casos de uso potenciales en los que este método puede ser adecuado son los casos en los que puede ser necesario acumular datos de búsqueda de múltiples fuentes. Por ejemplo, puede tener un sitio alojado en AEM, así como un segundo sitio alojado en una plataforma de terceros. Solr se puede configurar para rastrear el contenido de ambos sitios y almacenarlo en un índice agregado. Esto permitiría realizar búsquedas entre sitios.

### Consideraciones sobre el diseño {#design-considerations}

La documentación de Oak para los índices de Lucene enumera varias consideraciones que deben tenerse en cuenta al diseñar los índices:

* Si la consulta utiliza diferentes restricciones de ruta, utilice `evaluatePathRestrictions`. Esto permitirá que la consulta devuelva el subconjunto de resultados bajo la ruta especificada y luego los filtre según la consulta. De lo contrario, la consulta buscará todos los resultados que coincidan con los parámetros de consulta en el repositorio y los filtrará según la ruta.
* Si la consulta utiliza la ordenación, tenga una definición de propiedad explícita para la propiedad ordenada y establezca `ordered` a `true` para ello. Esto permitirá que los resultados se ordenen como tales en el índice y que se guarden en costosas operaciones de ordenación en el momento de la ejecución de la consulta.

* Solo ponga lo que se necesita en el índice. La adición de características o propiedades innecesarias hará que el índice crezca y ralentice el rendimiento.
* En un índice de propiedad, tener un nombre de propiedad único ayudaría a reducir el tamaño de un índice, pero para los índices de Lucene, el uso de `nodeTypes` y `mixins` debe hacerse para lograr índices coherentes. Consulta de un `nodeType` o `mixin` será más funcional que consultar `nt:base`. Al utilizar este método, defina `indexRules` para el `nodeTypes` en cuestión.

* Si las consultas solo se están ejecutando bajo ciertas rutas, cree esos índices bajo esas rutas. Los índices no son necesarios para vivir en la raíz del repositorio.
* Se recomienda utilizar un único índice cuando todas las propiedades que se indexen estén relacionadas para permitir que Lucene evalúe tantas restricciones de propiedad como sea posible de forma nativa. Además, una consulta solo usará un índice, incluso al realizar una unión.

### CopyOnRead {#copyonread}

En los casos en que la variable `NodeStore` se almacena de forma remota, una opción denominada `CopyOnRead` se puede activar. La opción hará que el índice remoto se escriba en el sistema de archivos local cuando se lea. Esto puede ayudar a mejorar el rendimiento de las consultas que a menudo se ejecutan con estos índices remotos.

Esto se puede configurar en la consola OSGi en el **LuceneIndexProvider** y está habilitado de forma predeterminada a partir de Oak 1.0.13.

### Eliminación de índices {#removing-indexes}

Cuando se elimina un índice, siempre se recomienda desactivarlo temporalmente configurando la variable `type` propiedad a `disabled` y realice pruebas para asegurarse de que la aplicación funciona correctamente antes de eliminarla. Tenga en cuenta que un índice no se actualiza mientras está deshabilitado, por lo que puede que no tenga el contenido correcto si se vuelve a habilitar y puede que sea necesario reindexarlo.

Después de eliminar un índice de propiedad en una instancia de TarMK, será necesario ejecutar la compactación para recuperar cualquier espacio en disco que estuviera en uso. Para los índices de Lucene, el contenido del índice real reside en BlobStore, por lo que se necesitaría una colección de residuos del almacén de datos.

Al eliminar un índice en una instancia de MongoDB, el coste de eliminación es proporcional al número de nodos en el índice. Dado que la eliminación de un índice grande puede causar problemas, el método recomendado es deshabilitar el índice y eliminarlo solo durante una ventana de mantenimiento, utilizando una herramienta como **oak-mongo.js**. Tenga en cuenta que este método no debe emplearse para contenido de nodo normal, ya que puede introducir incoherencias en los datos.

>[!NOTE]
>
>Para obtener más información sobre oak-mongo.js, consulte la [Sección Herramientas de la línea de comandos](https://jackrabbit.apache.org/oak/docs/command_line.html) de la documentación de Oak.

### Hoja de referencia de consultas JCR {#jcrquerycheatsheet}

Para apoyar la creación de consultas JCR eficientes y definiciones de índices, la variable [Hoja de referencia de consultas JCR|assets/JCR_query_cheatsheet-v1.0.pdf] está disponible para su descarga y uso como referencia durante el desarrollo. Contiene consultas de ejemplo para QueryBuilder, XPath y SQL-2, que abarcan varios escenarios que se comportan de forma diferente en términos del rendimiento de la consulta. También proporciona recomendaciones sobre cómo crear o personalizar índices Oak. El contenido de esta hoja de referencia se aplica a AEM 6.5 y AEM as a Cloud Service.

## Reindexación {#re-indexing}

Esta sección describe **only** razones aceptables para volver a indexar los índices de Oak.

Fuera de las razones descritas a continuación, el inicio de los reíndices de los índices Oak **not** cambie el comportamiento o resuelva los problemas, y aumente la carga innecesariamente en AEM.

La reindexación de los índices Oak debe evitarse a menos que se indique lo contrario en las tablas siguientes.

>[!NOTE]
>
>Antes de consultar las tablas siguientes para determinar si la reindexación es útil,** siempre **verificar:
>
>* la consulta es correcta
>* la consulta responde al índice esperado (mediante [Explicar consulta](/help/sites-administering/operations-dashboard.md#diagnosis-tools))
>* el proceso de indexación ha finalizado

>


### Cambios en la configuración del índice Oak {#oak-index-configuration-changes}

La única condición aceptable de no errar para la reindexación de índices Oak, es si la configuración de un índice Oak ha cambiado.

*La reindexación siempre debe abordarse teniendo debidamente en cuenta su impacto en AEM rendimiento general y realizarse durante períodos de baja actividad o períodos de mantenimiento.*

A continuación se detallan los posibles problemas, junto con las resoluciones:

* [Cambio en la definición del índice de propiedades](#property-index-definition-change)
* [Cambio de definición de índice de Lucene](#lucene-index-definition-change)

#### Cambio en la definición del índice de propiedades {#property-index-definition-change}

* Se aplica para/si:

   * Todas las versiones de Oak
   * Solo [índices de propiedades](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* Síntomas:

   * Los nodos existentes antes de la actualización de definición del índice de propiedad no aparecen en los resultados

* Cómo verificar:

   * Determine si los nodos que faltan se crearon o modificaron antes de la implementación de la definición de índice actualizada.
   * Compruebe el `jcr:created` o `jcr:lastModified` propiedades de cualquier nodo que falte con respecto al tiempo modificado del índice

* Cómo resolver:

   * [Volver a indexar](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) el índice de lucene
   * Alternativamente, toque (realice una operación de escritura benigna) a los nodos que faltan

      * Requiere toques manuales o código personalizado
      * Requiere que se conozca el conjunto de nodos que faltan
      * Requiere cambiar cualquier propiedad en el nodo

#### Cambio de definición de índice de Lucene {#lucene-index-definition-change}

* Se aplica para/si:

   * Todas las versiones de Oak
   * Solo [índices de lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Síntomas:

   * El índice Lucene no contiene los resultados esperados
   * Los resultados de la consulta no reflejan el comportamiento esperado de la definición del índice
   * El plan de consulta no informa de los resultados esperados en función de la definición del índice

* Cómo verificar:

   * Verifique que la definición del índice se haya cambiado utilizando el método JMX Mbean (LuceneIndex), estadísticas del índice de Lucene `diffStoredIndexDefinition`.

* Cómo resolver:

   * Versiones de Oak anteriores a la 1.6:

      * [Volver a indexar](#how-to-re-index) el índice de lucene
   * Versiones de Oak 1.6+

      * Si el contenido existente no se ve afectado por los cambios, entonces solo se necesita una actualización

         * [Actualizar](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) el índice de lucene estableciendo [oak:queryIndexDefinition]@refresh=true
      * Si no, [re-index](#how-to-re-index) el índice de lucene

         * Nota: El estado de índice desde la última reindexación correcta (o indexación inicial) se utilizará hasta que se active una nueva reindexación



### Situaciones de error y excepcionales {#erring-and-exceptional-situations}

En la siguiente tabla se describen las únicas situaciones de error aceptables y excepcionales en las que la reindexación de índices Oak resolverá el problema.

Si se produce un problema en AEM que no coincide con los criterios descritos a continuación, haga lo siguiente **not** vuelva a indexar los índices, ya que no resolverá el problema.

A continuación se detallan los posibles problemas, junto con las resoluciones:

* [Falta el binario del índice Lucene](#lucene-index-binary-is-missing)
* [El binario del índice Lucene está dañado](#lucene-index-binary-is-corrupt)

#### Falta el binario del índice Lucene {#lucene-index-binary-is-missing}

* Se aplica para/si:

   * Todas las versiones de Oak
   * Solo [índices de lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Síntomas:

   * El índice Lucene no contiene los resultados esperados

* Cómo verificar:

   * El archivo de registro de errores contiene una excepción que indica que falta un binario del índice Lucene

* Cómo resolver:

   * Realizar una comprobación de repositorios a través de; por ejemplo:

      [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

      atravesar el repositorio determina si faltan otros binarios (además de los archivos Lucene)

   * Si faltan binarios que no sean índices de lucene, restaure desde la copia de seguridad
   * De lo contrario, [re-index](#how-to-re-index) *all* índices de lucene
   * Nota:

      Esta condición indica un almacén de datos mal configurado que puede resultar en CUALQUIER binario (p. ej. recursos binarios) para que desaparezcan.

      En este caso, restaure a la última versión correcta conocida del repositorio para recuperar todos los binarios que faltan.

#### El binario del índice Lucene está dañado {#lucene-index-binary-is-corrupt}

* Se aplica para/si:

   * Todas las versiones de Oak
   * Solo [índices de lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Síntomas:

   * El índice Lucene no contiene los resultados esperados

* Cómo verificar:

   * La variable `AsyncIndexUpdate` (cada 5 segundos) fallará con una excepción en el archivo error.log:

      `...a Lucene index file is corrupt...`

* Cómo resolver:

   * Eliminar la copia local del índice de lucene

      1. Detener AEM
      1. Eliminar la copia local del índice de Lucene en `crx-quickstart/repository/index`
      1. Reiniciar AEM
   * Si esto no resuelve el problema, y la variable `AsyncIndexUpdate` las excepciones persisten entonces:

      1. [Volver a indexar](#how-to-re-index) el índice de erring
      1. Archivo también un [Compatibilidad con Adobe](https://helpx.adobe.com/support.html) ticket


### Cómo reindexar {#how-to-re-index}

>[!NOTE]
>
>En el AEM 6.5, [oak-run.jar es el ÚNICO método admitido](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree) para volver a indexar en repositorios MongoMK o RDBMK.

#### Reindexación de índices de propiedades {#re-indexing-property-indexes}

* Uso [oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) para volver a indexar el índice de propiedades
* Establezca la propiedad async-reindex en true en el índice de propiedades

   * `[oak:queryIndexDefinition]@reindex-async=true`

* Volver a indexar el índice de propiedades de forma asíncrona mediante la Consola web a través de la **PropertyIndexAsyncReindex** MBean;

   por ejemplo,

   [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### Reindexación de los índices de propiedades de Lucene {#re-indexing-lucene-property-indexes}

* Uso [oak-run.jar para volver a indexar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) el índice de propiedad de Lucene.
* Establezca la propiedad async-reindex en true en el índice de propiedad de lucene

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>La sección anterior resume y enmarca la guía de reindexación de Oak de la [Documentación de Apache Oak](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing) en el contexto de AEM.

### Texto Pre-extracción de binarios {#text-pre-extraction-of-binaries}

La preextracción de texto es el proceso de extraer y procesar texto de binarios, directamente desde el almacén de datos a través de un proceso aislado, y exponer directamente el texto extraído a posteriores reindexaciones de los índices Oak.

* Se recomienda la extracción previa de texto Oak para volver a indexar los índices de Lucene en repositorios con grandes volúmenes de archivos (binarios) que contienen texto extraíble (p. ej. PDF, documentos de Word, PPT, TXT, etc.) que cumplen los requisitos para la búsqueda de texto completo mediante índices Oak implementados; por ejemplo `/oak:index/damAssetLucene`.
* La preextracción de texto solo beneficiará a la reindexación de los índices de Lucene, y NO a los índices de propiedades de Oak, ya que los índices de propiedades no extraen texto de los binarios.
* La preextracción de texto tiene un gran impacto positivo cuando la reindexación de texto completo de binarios con gran cantidad de texto (PDF, Doc, TXT, etc.), donde como repositorio de imágenes no disfrutará de las mismas eficiencias ya que las imágenes no contienen texto extraíble.
* La preextracción de texto realiza la extracción de texto relacionado con la búsqueda de texto completo de una manera extra eficiente y lo expone al proceso de reindexación/indexación de Oak de una manera que es extra eficiente de consumir.

#### ¿Cuándo se puede utilizar la preextracción de texto? {#when-can-text-pre-extraction-be-used}

Reindexación de una **existente** índice lucene con extracción binaria habilitada

* Reindexación del procesamiento **all** contenido candidato en el repositorio; cuando los binarios de los que extraer texto completo son numerosos o complejos, una mayor carga de cálculo para realizar la extracción de texto completo se coloca en AEM. La preextracción de texto desplaza el &quot;trabajo costoso desde el punto de vista computacional&quot; de la extracción de texto a un proceso aislado que accede directamente a AEM Data Store, evitando así sobrecargas y contención de recursos en AEM.

Soporte para la implementación de un **new** índice lucene para AEM con extracción binaria habilitada

* Cuando se implementa un nuevo índice (con la extracción binaria habilitada) en AEM, Oak indexa automáticamente todo el contenido candidato en la siguiente ejecución del índice de texto completo asíncrono. Por las mismas razones descritas en la reindexación anterior, esto puede resultar en una carga indebida en AEM.

#### ¿Cuándo se puede utilizar la preextracción de texto NOT? {#when-can-text-pre-extraction-not-be-used}

La extracción previa de texto no se puede utilizar para contenido nuevo agregado al repositorio, ni tampoco es necesario.

El nuevo contenido se añade al repositorio de forma natural e incremental se indexará mediante el proceso de indexación de texto completo asincrónico (de forma predeterminada, cada 5 segundos).

En el funcionamiento normal de AEM, por ejemplo, cargando recursos a través de la interfaz de usuario web o mediante la ingesta programática de recursos, AEM indexará automática e incrementalmente el nuevo contenido binario. Dado que la cantidad de datos es incremental y relativamente pequeña (aproximadamente la cantidad de datos que se puede mantener en el repositorio en 5 segundos), AEM realizar la extracción de texto completo de los binarios durante la indexación sin afectar al rendimiento general del sistema.

#### Requisitos previos para utilizar la preextracción de texto {#prerequisites-to-using-text-pre-extraction}

* Se reindexará un índice de lucene que realice una extracción binaria de texto completo o implemente un nuevo índice que incluya binarios de índice de texto completo de contenido existente
* El contenido (binarios) desde el que se extrae texto previamente debe estar en el repositorio
* Una ventana de mantenimiento para generar el archivo CSV Y para realizar la reindexación final
* Versión de Oak: 1.0.18+, 1.2.3+
* [oak-run.jar](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)versión 1.7.4+
* Una carpeta o un recurso compartido del sistema de archivos para almacenar el texto extraído accesible desde las instancias de AEM de indexación

   * La configuración OSGi de preextracción de texto requiere una ruta del sistema de archivos a los archivos de texto extraídos, por lo que debe ser accesible directamente desde la instancia de AEM (unidad local o montaje de uso compartido de archivos)

#### Cómo realizar la extracción previa de texto {#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***Los comandos oak-run.jar descritos a continuación se enumeran completamente en [https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>El diagrama y los pasos anteriores sirven para explicar y complementar los pasos técnicos de preextracción de texto descritos en la documentación de Apache Oak.

![Flujo del proceso de preextracción de texto](assets/chlimage_1-139.png)

**Generar lista de contenido para extraer previamente**

*Ejecute el paso 1(a-b) durante una ventana de mantenimiento/período de bajo uso, ya que el almacén de nodos se atraviesa durante esta operación, lo que puede conllevar una carga significativa en el sistema.*

1 bis. Ejecutar `oak-run.jar --generate` para crear una lista de nodos de los que se extraerá previamente su texto.

1 ter. La lista de nodos (1a) se almacena en el sistema de archivos como un archivo CSV

Tenga en cuenta que todo el almacén de nodos se atraviesa (según lo especificado por las rutas en el comando oak-run) cada vez `--generate` se ejecuta y se ejecuta una **new** Se crea el archivo CSV. El archivo CSV es **not** se reutiliza entre ejecuciones discretas del proceso de preextracción de texto (pasos 1 a 2).

**Extraer texto previamente al sistema de archivos**

*El paso 2(a-c) se puede ejecutar durante el funcionamiento normal de AEM si solo interactúa con el almacén de datos.*

2 bis. Ejecutar `oak-run.jar --tika` para extraer previamente texto para los nodos binarios enumerados en el archivo CSV generado en (1b)

2 ter. El proceso iniciado en (2a) accede a los nodos binarios definidos en el CSV en el Almacén de datos directamente y extrae texto.

2 quáter.  El texto extraído se almacena en el sistema de archivos en un formato que no se puede utilizar en el proceso de reindexación de Oak (3a)

El texto extraído previamente se identifica en el CSV mediante la huella digital binaria. Si el archivo binario es el mismo, se puede utilizar el mismo texto extraído previamente en AEM instancias. Dado que AEM Publish suele ser un subconjunto de AEM Author, el texto extraído previamente de AEM Author también se puede utilizar para volver a indexar AEM Publish (suponiendo que AEM Publish tenga acceso al sistema de archivos a los archivos de texto extraídos).

El texto extraído previamente se puede añadir gradualmente a con el tiempo. La preextracción de texto omitirá la extracción para binarios extraídos anteriormente, por lo que se recomienda mantener el texto extraído previamente en caso de que la reindexación deba ocurrir en el futuro (suponiendo que el contenido extraído no sea prohibitivamente grande. Si es así, evalúe comprimiendo el contenido en el interín, ya que el texto se comprime bien).

**Reindexar índices Oak, obtener texto completo de archivos de texto extraído**

*Ejecute la reindexación (pasos 3a-b) durante un período de mantenimiento/bajo uso, ya que el almacén de nodos se atraviesa durante esta operación, lo que puede conllevar una carga significativa en el sistema.*

3 bis. [Volver a indexar](#how-to-re-index) de índices de Lucene se invoca en AEM

3 ter. La configuración OSGi de Apache Jackrabbit Oak DataStore PreExtractingTextProvider (configurada para apuntar el texto extraído a través de una ruta del sistema de archivos) ordena a Oak que obtenga texto completo de los archivos extraídos y evita directamente pulsar y procesar los datos almacenados en el repositorio.
