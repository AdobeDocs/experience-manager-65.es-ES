---
title: Monitoreo de los recursos del servidor mediante la consola JMX
seo-title: Monitoreo de los recursos del servidor mediante la consola JMX
description: Aprenda a supervisar los recursos del servidor mediante la consola JMX.
seo-description: Aprenda a supervisar los recursos del servidor mediante la consola JMX.
uuid: 0a28aafe-61b2-472b-8f8f-2cd6540cbfee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 873ce073-0055-4e1b-b3c6-ae7967700894
docset: aem65
translation-type: tm+mt
source-git-commit: 97c93a95cd7fe63b306d80fe127388a209b727c7
workflow-type: tm+mt
source-wordcount: '4974'
ht-degree: 1%

---


# Monitoreo de los recursos del servidor mediante la consola de JMX{#monitoring-server-resources-using-the-jmx-console}

La consola JMX le permite supervisar y administrar los servicios en el servidor CRX. En las secciones siguientes se resumen los atributos y las operaciones que se exponen a través del marco JMX.

Para obtener información sobre cómo utilizar los controles de consola, consulte [Uso de la consola JMX](#using-the-jmx-console). Para obtener información general sobre JMX, consulte la página [Java Management Extensions (JMX) Technology](https://www.oracle.com/technetwork/java/javase/tech/javamanagement-140525.html) en el sitio Web de Oracle.

Para obtener información sobre la creación de MBeans para administrar los servicios mediante la consola JMX, consulte [Integración de servicios con la consola JMX](/help/sites-developing/jmx-integration.md).

## Mantenimiento de flujo de trabajo {#workflow-maintenance}

Operaciones para administrar instancias de flujo de trabajo en ejecución, finalizadas, obsoletas y con errores.

* Dominio: com.adobe.granite.workflow
* Tipo: Mantenimiento

>[!NOTE]
>
>Consulte la [consola de flujo de trabajo](/help/sites-administering/workflows-administering.md) para obtener herramientas de administración de flujo de trabajo adicionales y descripciones de posibles estados de instancias de flujo de trabajo.

### Operaciones {#operations}

**** listRunningWorkflowsPerModelEnumera el número de instancias de flujo de trabajo que se están ejecutando para cada modelo de flujo de trabajo.

* Argumentos: none
* Valor devuelto: Datos tabulares que contienen las columnas Count y ModelId.

**** listCompletedWorkflowsPerModelEnumera el número de instancias de flujo de trabajo completadas para cada modelo de flujo de trabajo.

* Argumentos: none
* Valor devuelto: Datos tabulares que contienen las columnas Count y ModelId.

**** returnWorkflowQueueInfoEnumera información sobre los elementos de flujo de trabajo que se han procesado y que están en cola para su procesamiento.

* Argumentos: none
* Valor devuelto: Datos tabulares que contienen las siguientes columnas:

   * Trabajos
   * Nombre de la cola
   * Activar tareas
   * Tiempo medio de procesamiento
   * Tiempo promedio de espera
   * Tareas canceladas
   * Tareas con errores
   * Trabajos finalizados
   * Trabajos procesados
   * Trabajos en cola

**** returnWorkflowJobTopicInfoEnumera la información de procesamiento de los trabajos de flujo de trabajo, organizada por tema.

* Argumentos: none
* Valor devuelto: Datos tabulares que contienen las siguientes columnas:

   * Nombre del tema
   * Tiempo medio de procesamiento
   * Tiempo promedio de espera
   * Tareas canceladas
   * Tareas con errores
   * Trabajos finalizados
   * Trabajos procesados

**** returnFailedWorkflowCountMuestra el número de instancias de flujo de trabajo que han fallado. Puede especificar un modelo de flujo de trabajo para la consulta o recuperar información para todos los modelos de flujo de trabajo.

* Argumentos:

   * modelo: ID del modelo que se va a consulta. Para ver un recuento de instancias de flujo de trabajo con errores para todos los modelos de flujo de trabajo, especifique ningún valor. El ID es la ruta al nodo del modelo, por ejemplo:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor devuelto: Número de instancias de flujo de trabajo con errores.

**** returnFailedWorkflowCountPerModelMuestra el número de instancias de flujo de trabajo que han fallado para cada modelo de flujo de trabajo.

* Argumentos: ninguno.
* Valor devuelto: Datos tabulares que contienen las columnas Count e Model ID.

**instancias de flujo de trabajo de** finalizaciónErrorInstancesTerminar que han fallado. Puede finalizar todas las instancias con errores o solo las instancias con errores de un modelo específico. Opcionalmente, puede reiniciar las instancias después de que hayan finalizado. También puede probar la operación para ver los resultados sin realizar la operación.

* Argumentos:

   * Reinicie la instancia: (Opcional) Especifique un valor de `true` para reiniciar las instancias después de que hayan finalizado. El valor predeterminado de `false` no provoca el reinicio de instancias de flujo de trabajo terminadas.
   * Ensayo: (Opcional) Especifique un valor de `true` para ver los resultados de la operación sin realizar la operación. El valor predeterminado de `false` hace que la operación se realice.
   * Modelo: (Opcional) El ID del modelo al que se aplica la operación. No especifique ningún modelo para aplicar la operación a las instancias con errores de todos los modelos de flujo de trabajo. El ID es la ruta al nodo del modelo, por ejemplo:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor devuelto: Datos tabulares sobre las instancias que se terminan, que contienen las siguientes columnas:

   * Iniciador
   * InstanceId
   * ModelId
   * Carga útil
   * StartComment
   * WorkflowTitle

**** vuelva a intentarErrorWorkItemsIntenta ejecutar los pasos del elemento de trabajo que han fallado. Puede reintentar todos los elementos de trabajo con errores o solo los elementos de trabajo con errores para un modelo de flujo de trabajo específico. Opcionalmente, puede probar la operación para ver los resultados sin realizar la operación.

* Argumentos:

   * Ensayo: (Opcional) Especifique un valor de `true` para ver los resultados de la operación sin realizar la operación. El valor predeterminado de `false` hace que la operación se realice.
   * Modelo: (Opcional) El ID del modelo al que se aplica la operación. No especifique ningún modelo para aplicar la operación a los elementos de trabajo fallidos de todos los modelos de flujo de trabajo. El ID es la ruta al nodo del modelo, por ejemplo:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor devuelto: Datos tabulares sobre los elementos de trabajo fallidos que se vuelven a intentar, incluidas las siguientes columnas:

   * Iniciador
   * InstanceId
   * ModelId
   * Carga útil
   * StartComment
   * WorkflowTitle

**** PurgeActiveQuita las instancias de flujo de trabajo activas de una página específica. Puede purgar instancias activas para todos los modelos o solo las instancias para un modelo específico. Opcionalmente, puede probar la operación para ver los resultados sin realizar la operación.

* Argumentos:

   * Modelo: (Opcional) El ID del modelo al que se aplica la operación. No especifique ningún modelo para aplicar la operación a las instancias de flujo de trabajo de todos los modelos de flujo de trabajo. El ID es la ruta al nodo del modelo, por ejemplo:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Número de días transcurridos desde que se inició el flujo de trabajo: La antigüedad de las instancias de flujo de trabajo que se van a purgar, en días.
   * Ensayo: (Opcional) Especifique un valor de `true` para ver los resultados de la operación sin realizar la operación. El valor predeterminado de `false` hace que la operación se realice.

* Valor devuelto: Datos tabulares sobre las instancias de flujo de trabajo activas que se purgan, incluidas las siguientes columnas:

   * Iniciador
   * InstanceId
   * ModelId
   * Carga útil
   * StartComment
   * WorkflowTitle

**** countStaleWorkflowsDevuelve el número de instancias de flujo de trabajo que están obsoletas. Puede recuperar el número de instancias antiguas para todos los modelos de flujo de trabajo o para un modelo específico.

* Argumentos:

   * Modelo: (Opcional) El ID del modelo al que se aplica la operación. No especifique ningún modelo para aplicar la operación a las instancias de flujo de trabajo de todos los modelos de flujo de trabajo. El ID es la ruta al nodo del modelo, por ejemplo:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor devuelto: Número de instancias de flujo de trabajo antiguas.

**** RestartStaleWorkflowsReinicia instancias de flujo de trabajo antiguas. Puede reiniciar todas las instancias antiguas o solo las instancias antiguas de un modelo específico. También puede probar la operación para ver los resultados sin realizar la operación.

* Argumentos:

   * Modelo: (Opcional) El ID del modelo al que se aplica la operación. No especifique ningún modelo para aplicar la operación a las instancias antiguas de todos los modelos de flujo de trabajo. El ID es la ruta al nodo del modelo, por ejemplo:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Ensayo: (Opcional) Especifique un valor de `true` para ver los resultados de la operación sin realizar la operación. El valor predeterminado de `false` hace que la operación se realice.

* Valor devuelto: Lista de instancias de flujo de trabajo que se reinician.

**** fetchModelListEnumera todos los modelos de flujo de trabajo.

* Argumentos: none
* Valor devuelto: Datos tabulares que identifican los modelos de flujo de trabajo, incluidas las columnas ModelId y ModelName.

**** countRunningWorkflowsDevuelve el número de instancias de flujo de trabajo que se están ejecutando. Puede recuperar el número de instancias en ejecución para todos los modelos de flujo de trabajo o para un modelo específico.

* Argumentos:

   * Modelo: (Opcional) El ID del modelo para el que se devuelve el número de instancias en ejecución. No especifique ningún modelo para devolver el número de instancias en ejecución de todos los modelos de flujo de trabajo. El ID es la ruta al nodo del modelo, por ejemplo:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor devuelto: Número de instancias de flujo de trabajo en ejecución.

**** countCompletedWorkflowsDevuelve el número de instancias de flujo de trabajo completadas. Puede recuperar el número de instancias completadas para todos los modelos de flujo de trabajo o para un modelo específico.

* Argumentos:

   * Modelo: (Opcional) El ID del modelo para el que se devuelve el número de instancias completadas. No especifique ningún modelo para devolver el número de instancias completadas de todos los modelos de flujo de trabajo. El ID es la ruta al nodo del modelo, por ejemplo:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valor devuelto: Número de instancias de flujo de trabajo completadas.

**** purgeCompletedQuita del repositorio los registros de flujos de trabajo completados de una página específica. Utilice esta operación periódicamente para minimizar el tamaño del repositorio cuando utilice con frecuencia flujos de trabajo. Puede purgar instancias completadas para todos los modelos o solo las instancias para un modelo específico. Opcionalmente, puede probar la operación para ver los resultados sin realizar la operación.

* Argumentos:

   * Modelo: (Opcional) El ID del modelo al que se aplica la operación. No especifique ningún modelo para aplicar la operación a las instancias de flujo de trabajo de todos los modelos de flujo de trabajo. El ID es la ruta al nodo del modelo, por ejemplo:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Número de días transcurridos desde que se completó el flujo de trabajo: Número de días que las instancias de flujo de trabajo han estado en el estado completado.
   * Ensayo: (Opcional) Especifique un valor de `true` para ver los resultados de la operación sin realizar la operación. El valor predeterminado de `false` hace que la operación se realice.

* Valor devuelto: Datos tabulares sobre las instancias de flujo de trabajo completadas que se purgan, incluidas las siguientes columnas:

   * Iniciador
   * InstanceId
   * ModelId
   * Carga útil
   * StartComment
   * WorkflowTitle

## Repositorio {#repository}

Información sobre el repositorio de CRX

* Dominio: com.adobe.granite
* Tipo: Repositorio

### Atributos {#attributes}

**** NombreNombre de la implementación del repositorio JCR. Solo lectura.

**** VersiónLa versión de implementación del repositorio. Solo lectura.

**** HomeDirEl directorio donde se encuentra el repositorio. La ubicación predeterminada es &lt;QuickStart_Jar_Location>/crx-quickstart/repositorio. Solo lectura.

**Nombre del** clienteNombre del cliente al que se emite la licencia de software. Solo lectura.

**** LicenseKeyClave de licencia única para esta instalación del repositorio. Solo lectura.

**** AvailableDiskSpaceEspacio en disco disponible para esta instancia del repositorio, en Mbytes. Solo lectura.

**** MaximumNumberOfOpenFilesNúmero de archivos que se pueden abrir al mismo tiempo. Solo lectura.

**** SessionTrackerValor de la variable de sistema crx.debug.session. true indica una sesión de depuración. false indica una sesión normal. Lectura y escritura.

**** DescriptoresConjunto de pares de clave-valor que representan las propiedades del repositorio. Todas las propiedades son de solo lectura.

<table>
 <tbody>
  <tr>
   <th>Clave</th>
   <th>Value</th>
  </tr>
  <tr>
   <td>option.node.and.property.with.same.name.supported</td>
   <td>Indica si un nodo y una propiedad del nodo pueden tener el mismo nombre. true indica que se admiten los mismos nombres, false indica que no se admite. </td>
  </tr>
  <tr>
   <td>identifier.stability</td>
   <td>Indica la estabilidad de identificadores de nodo no referenciables. Los valores siguientes son posibles:
    <ul>
     <li>identifier.stable.indefinite.duration: Los identificadores no cambian.</li>
     <li>identifier.stable.method.duration: Los identificadores pueden cambiar entre llamadas de método.</li>
     <li>identifier.stable.save.duration: Los identificadores no cambian dentro de un ciclo de almacenamiento/actualización.</li>
     <li>identifier.stable.session.duration: Los identificadores no cambian durante una sesión.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>query.xpath.pos.index</td>
   <td>Indica si se admite el lenguaje de consulta JCR 1.0 XPath. true indica compatibilidad y false indica no compatibilidad.</td>
  </tr>
  <tr>
   <td>crx.repository.systemid</td>
   <td>El identificador del sistema tal como se encuentra en el archivo system.id.</td>
  </tr>
  <tr>
   <td>option.query.sql.supported</td>
   <td>Indica si se admite el lenguaje de consulta JCR 1.0 XPath. true indica compatibilidad y false indica no compatibilidad.</td>
  </tr>
  <tr>
   <td>jcr.repository.version</td>
   <td>Versión de la implementación del repositorio.</td>
  </tr>
  <tr>
   <td>option.update.primary.node.type.supported</td>
   <td>Indica si se puede cambiar el tipo de nodo principal de un nodo. true indica que se puede cambiar el tipo de nodo principal y false indica que no se admite el cambio.</td>
  </tr>
  <tr>
   <td>option.node.type.management.supported</td>
   <td>Indica si se admite la administración de tipos de nodo. true indica que se admite y false indica que no se admite.</td>
  </tr>
  <tr>
   <td>node.type.management.overrides.supported</td>
   <td>Indica si se puede anular la definición de nodo secundario o propiedad heredada de un tipo de nodo. true indica que se admiten las anulaciones y false indica que no hay anulaciones.</td>
  </tr>
  <tr>
   <td>option.observation.supported</td>
   <td>true indica que se admite la observación asincrónica de los cambios del repositorio. La compatibilidad con la observación asincrónica permite a las aplicaciones recibir y responder a las notificaciones sobre cada cambio a medida que se producen.</td>
  </tr>
  <tr>
   <td>query.jcrscore</td>
   <td><p>true indica que la seudopropiedad jcr:score está disponible en consultas XPath y SQL que incluyen una función jcrfn:contains (en XPath) o CONTAINS (en SQL) para realizar una búsqueda de texto completo.</p> </td>
  </tr>
  <tr>
   <td>option.simple.versioning.supported</td>
   <td>true indica que el repositorio admite versiones simples. Con el control de versiones sencillo, el repositorio mantiene una serie secuencial de versiones de un nodo.</td>
  </tr>
  <tr>
   <td>option.workspace.management.supported</td>
   <td>true indica que el repositorio admite la creación y eliminación de espacios de trabajo mediante API.</td>
  </tr>
  <tr>
   <td>option.update.mixin.node.types.supported</td>
   <td>true indica que el repositorio admite la adición y eliminación de tipos de nodos mixtos de un nodo existente.</td>
  </tr>
  <tr>
   <td>node.type.management.primary.item.name.supported</td>
   <td>true indica que el repositorio permite que las definiciones de nodos contengan un elemento principal como elemento secundario. Se puede acceder a un elemento principal mediante la API sin conocer el nombre del elemento.</td>
  </tr>
  <tr>
   <td>level.2.supported</td>
   <td>true indica que tanto LEVEL_1_SUPPORTED como OPTION_XML_IMPORT_SUPPORTED son verdaderos.</td>
  </tr>
  <tr>
   <td>write.supported</td>
   <td>true indica que el repositorio proporciona acceso de escritura mediante la API. false indica acceso de sólo lectura.</td>
  </tr>
  <tr>
   <td>node.type.management.update.in.use.supported</td>
   <td>true indica que puede cambiar las definiciones de nodos que utilizan los nodos existentes.</td>
  </tr>
  <tr>
   <td>jcr.specification.version</td>
   <td>Versión de la especificación JCR que implementa el repositorio.</td>
  </tr>
  <tr>
   <td>option.journaled.observation.supported</td>
   <td>true indica que las aplicaciones pueden realizar una observación en diario del repositorio. con la observación en diario, se puede obtener un conjunto de notificaciones de cambio para un período de tiempo específico. </td>
  </tr>
  <tr>
   <td>query.languages</td>
   <td>Los idiomas de consulta que admite el repositorio. Ningún valor indica que no se admite la consulta.</td>
  </tr>
  <tr>
   <td>option.xml.export.supported</td>
   <td>true indica que el repositorio admite la exportación de nodos como código XML.</td>
  </tr>
  <tr>
   <td>node.type.management.multiple.binary.properties.supported</td>
   <td>true indica que el repositorio admite el registro de tipos de nodos que tienen varias propiedades binarias. false indica que se admite una sola propiedad binaria para un tipo de nodo.</td>
  </tr>
  <tr>
   <td>option.access.control.supported</td>
   <td>true indica que el repositorio admite control de acceso para configurar y determinar los privilegios de usuario para el acceso a nodos.</td>
  </tr>
  <tr>
   <td>option.baselines.supported</td>
   <td>true indica que el repositorio admite configuraciones y líneas de base.</td>
  </tr>
  <tr>
   <td>option.shareable.nodes.supported</td>
   <td>true indica que el repositorio admite la creación de nodos compartibles.</td>
  </tr>
  <tr>
   <td>crx.cluster.id</td>
   <td>Identificador del clúster de repositorio.</td>
  </tr>
  <tr>
   <td>query.stored.queries.supported</td>
   <td>true indica que el repositorio admite consultas almacenadas.</td>
  </tr>
  <tr>
   <td>query.full.text.search.supported</td>
   <td>true indica que el repositorio admite la búsqueda de texto completo.</td>
  </tr>
  <tr>
   <td>node.type.management.inheritance</td>
   <td><p>Indica el nivel de compatibilidad del repositorio con la herencia de tipo de nodo. Los valores siguientes son posibles:</p> <p>node.type.management.herencia.Minimum: El registro de los tipos de nodos principales está limitado a aquellos que solo tienen nt:base como supertipo. El registro de los tipos de nodos de mezcla está limitado a los que no tienen supertipo.</p> <p>node.type.management.herencia.single: El registro de tipos de nodos principales está limitado a los que tienen un supertipo. El registro de los tipos de nodos de mezcla está limitado a los que tienen como máximo un supertipo.</p> <p><br /> node.type.management.herencia.multiple: Los tipos de nodos primarios se pueden registrar con uno o más supertipos. Los tipos de nodos de mezcla se pueden registrar con cero o más supertipos.</p> </td>
  </tr>
  <tr>
   <td>crx.cluster.preferredMaster</td>
   <td>true indica que este nodo de clúster es el maestro preferido del clúster.</td>
  </tr>
  <tr>
   <td>option.transactions.supported</td>
   <td>true indica que el repositorio admite transacciones.</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor.url</td>
   <td>Dirección URL del proveedor del repositorio.</td>
  </tr>
  <tr>
   <td>node.type.management.value.constraints.supported</td>
   <td>true indica que el repositorio admite restricciones de valor para propiedades de nodo.</td>
  </tr>
  <tr>
   <td>node.type.management.property.types</td>
   <td>matriz de constantes javax.jcr.PropertyType que representan los tipos de propiedad que puede especificar un tipo de nodo registrado. Una matriz de longitud cero indica que los tipos de nodo registrados no pueden especificar definiciones de propiedad. Los tipos de propiedad son STRING, URI, BOOLEAN, LONG, DOBLE, DECIMAL, BINARY, DATE, NAME, PATH, WEAKREFERENCE, REFERENCE y UNDEFINED (si se admite).</td>
  </tr>
  <tr>
   <td>node.type.management.orderable.child.nodes.supported</td>
   <td>true indica que el repositorio admite la preservación del orden de los nodos secundarios.</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor</td>
   <td>Nombre del proveedor del repositorio.</td>
  </tr>
  <tr>
   <td>query.joins</td>
   <td><p>Nivel de asistencia para las uniones en consultas. Los valores siguientes son posibles:</p>
    <ul>
     <li>consulta.joins.none: No se admiten las uniones. Las consultas pueden utilizar un selector.</li>
     <li>consulta.joins.inner: Compatibilidad con las uniones interiores.</li>
     <li>consulta.joins.inner.external: Compatibilidad con las uniones interiores y exteriores.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>org.apache.jackrabbit.spi.commons.AdditionalEventInfo</td>
   <td> </td>
  </tr>
  <tr>
   <td>query.xpath.doc.order</td>
   <td>true indica que el repositorio admite el lenguaje de consulta XPath 1.0.</td>
  </tr>
  <tr>
   <td>query.jcrpath</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.xml.import.supported</td>
   <td>true indica que el repositorio admite la importación de código XML como contenido.</td>
  </tr>
  <tr>
   <td>node.type.management.same.name.siblings.supported</td>
   <td>true indica que el repositorio admite nodos del mismo nivel (nodos con el mismo elemento principal) con los mismos nombres.</td>
  </tr>
  <tr>
   <td>node.type.management.residual.definitions.supported</td>
   <td>true indica que el repositorio admite propiedades de nombre con definiciones residuales. Cuando se admite, el atributo name de una definición de elemento puede ser un asterisco ("*").</td>
  </tr>
  <tr>
   <td>node.type.management.autocreated.definitions.supported</td>
   <td>true indica que el repositorio admite la creación automática de elementos secundarios (nodos o propiedades) de un nodo cuando se crea el nodo.</td>
  </tr>
  <tr>
   <td>crx.cluster.master</td>
   <td>true indica que este nodo de repositorio es el nodo maestro del clúster.</td>
  </tr>
  <tr>
   <td>level.1.supported</td>
   <td>true indica que option.xml.export.support es true y consulta.languages tiene una longitud no nula.</td>
  </tr>
  <tr>
   <td>option.unfiled.content.supported</td>
   <td>true indica que el repositorio admite contenido sin archivar. Los nodos sin archivar no forman parte de la jerarquía del repositorio.</td>
  </tr>
  <tr>
   <td>jcr.specification.name</td>
   <td>Nombre de la especificación JCR que implementa el repositorio.</td>
  </tr>
  <tr>
   <td>option.versioning.supported</td>
   <td>true indica que el repositorio admite versiones completas.</td>
  </tr>
  <tr>
   <td>jcr.repository.name</td>
   <td>Nombre del repositorio.</td>
  </tr>
  <tr>
   <td>option.locking.supported</td>
   <td>true indica que el repositorio admite el bloqueo de nodos. El bloqueo permite al usuario impedir temporalmente que otros usuarios realicen cambios.</td>
  </tr>
  <tr>
   <td>jcr.repository.version.display</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.activities.supported</td>
   <td>true indica que el repositorio admite actividades. Las actividades son un conjunto de cambios que se realizan en un espacio de trabajo y que se combinan en otro espacio de trabajo.</td>
  </tr>
  <tr>
   <td>node.type.management.multivalued.properties.supported</td>
   <td>true indica que el repositorio admite propiedades de nodo que pueden tener cero o más valores.</td>
  </tr>
  <tr>
   <td>option.retention.supported</td>
   <td>true indica que el repositorio admite el uso de aplicaciones de administración de retención externas para aplicar políticas de retención al contenido y admite retención y liberación.</td>
  </tr>
  <tr>
   <td>option.lifecycle.supported</td>
   <td>true indica que el repositorio admite la administración del ciclo vital.</td>
  </tr>
 </tbody>
</table>

**** WorkspaceNamesNombres de los espacios de trabajo del repositorio. Solo lectura.

**** DataStoreGarbageCollectionDelay La cantidad de tiempo, en milisegundos, que la recolección de elementos no utilizados se repite después de analizar cada décimo nodo. Lectura y escritura.

**** BackupDelay La cantidad de tiempo en milisegundos que el proceso de copia de seguridad permanece entre cada paso de la copia de seguridad. Lectura y escritura.

**** BackupInProgressEl valor true indica que se está ejecutando un proceso de copia de seguridad. Solo lectura.

**** BackupProgressPara la copia de seguridad actual, el porcentaje de todos los archivos de los que se ha realizado una copia de seguridad. Solo lectura.

**** CurrentBackupTarget Para la copia de seguridad actual, el archivo ZIP donde se almacenan los archivos de copia de seguridad. Cuando una copia de seguridad no está en curso, no aparece ningún valor. Solo lectura.

**** BackupWasSuccessfulEl valor true indica que no se han producido errores durante la copia de seguridad actual o que no hay ninguna copia de seguridad en curso. false indica un error durante la copia de seguridad actual. Solo lectura.

**** BackupResult El estado de la copia de seguridad actual. Los valores siguientes son posibles:

* Copia de seguridad en curso: Se está ejecutando una copia de seguridad.
* Copia de seguridad cancelada: Se canceló la copia de seguridad.
* Copia de seguridad finalizada con error: Error durante la copia de seguridad. El mensaje de error proporciona información sobre la causa.
* Copia de seguridad completada: La copia de seguridad se realizó correctamente.
* No se ha ejecutado ninguna copia de seguridad hasta ahora: No hay copia de seguridad en curso.

Solo lectura.

**** TarOptimizationRunningSinceLa hora en la que se inició el proceso de optimización de archivos TAR actual. Solo lectura.

**** TarOptimizationDelay La cantidad de tiempo en milisegundos que el proceso de optimización TAR permanece entre cada paso del proceso. Lectura y escritura.

**** ClusterPropertiesConjunto de pares clave-valor que representan las propiedades y los valores del clúster. Cada fila de la tabla representa una propiedad de clúster. Solo lectura.

**** ClusterNodesMiembros del clúster de repositorios.

**** ClusterId El identificador de este clúster de repositorio. Solo lectura.

**** ClusterMasterId El identificador del nodo maestro de este clúster de repositorio. Solo lectura.

**** ClusterNodeId El identificador de este nodo del clúster de repositorio. Solo lectura.

### Operaciones {#operations-1}

**** createWorkspaceCrea un espacio de trabajo en este repositorio.

* Argumentos:

   * name: Un valor de cadena que representa el nombre del nuevo espacio de trabajo.

* Valor devuelto: none

**** runDataStoreGarbageCollectionEjecuta la recopilación de elementos no utilizados en los nodos del repositorio.

* Argumentos:

   * delete: Un valor booleano que indica si se eliminarán los elementos del repositorio que no se utilicen. Un valor de true provoca la eliminación de nodos y propiedades no utilizados. Un valor false hace que se analicen todos los nodos, pero no se elimina ninguno.

* Valor devuelto: none

**** stopDataStoreGarbageCollection Detiene una recopilación de elementos no utilizados del almacén de datos en ejecución.

* Argumentos: none
* Valor devuelto: representación de cadena del estado actual

**** startBackupRealiza una copia de seguridad de los datos del repositorio en un archivo ZIP.

* Argumentos:

   * `target`:: (Opcional) Un  `String` valor que representa el nombre del archivo ZIP o directorio en el que se archivan los datos del repositorio. Para utilizar un archivo ZIP, incluya la extensión del nombre del archivo ZIP. Para utilizar un directorio, no incluya ninguna extensión de nombre de archivo.

      Para realizar una copia de seguridad incremental, especifique el directorio que se utilizó anteriormente para la copia de seguridad.

      Puede especificar una ruta absoluta o relativa. Las rutas relativas son relativas al elemento principal del directorio crx-quickstart.

      Cuando no especifica ningún valor, se utiliza el valor predeterminado de `backup-currentdate.zip`, donde `currentdate` tiene el formato `yyyyMMdd-HHmm`.

* Valor devuelto: none

**** cancelBackupDetiene el proceso de copia de seguridad actual y elimina el archivo temporal que el proceso creó para archivar datos.

* Argumentos: none
* Valor devuelto: none

**** blockRepositoryWritesBlocks cambia los datos del repositorio. Todos los oyentes de copia de seguridad del repositorio reciben una notificación del bloque.

* Argumentos: none
* Valor devuelto: none

**** unblockRepositoryWritesQuita el bloque del repositorio. Todos los oyentes de copia de seguridad del repositorio reciben una notificación de la eliminación del bloque.

* Argumentos: none
* Valor devuelto: none

**** startTarOptimizationInicia el proceso de optimización de archivos TAR utilizando el valor predeterminado para tarOptimizationDelay.

* Argumentos: none
* Valor devuelto: none

**** stopTarOptimizationDetiene la optimización de archivos TAR.

* Argumentos: none
* Valor devuelto: none

**** tarIndexMergeCombina los archivos de índice superiores de todos los conjuntos TAR. Los archivos de índice principales son archivos con distintas versiones principales. Por ejemplo, los siguientes archivos se combinan en el archivo index_3_1.tar: index_1_1.tar, index_2_0.tar, index_3_0.tar. Los archivos que se han combinado se eliminan (en el ejemplo anterior, se eliminan index_1_1.tar, index_2_0.tar e index_3_0.tar).

* Argumentos:

   * `background`:: Valor booleano que indica si se debe ejecutar la operación en segundo plano para que la consola web se pueda utilizar durante la ejecución. Un valor true ejecuta la operación en segundo plano.

* Valor devuelto: none

**** makeClusterMasterEstablece este nodo de repositorio como nodo maestro del clúster. Si aún no es master, este comando detiene el detector de la instancia maestra actual y inicio un detector maestro en el nodo actual. Este nodo se establece como nodo maestro y se reinicia, lo que provoca que todos los demás nodos del clúster (es decir, los que están controlados por el maestro) se conecten a esta instancia.

* Argumentos: none
* Valor devuelto: none

**** joinClusterAgrega este repositorio a un clúster como nodo controlado por el maestro de clúster. Debe proporcionar un nombre de usuario y una contraseña para fines de autenticación. La conexión utiliza autenticación básica. Las credenciales de seguridad se codifican en base-64 antes de enviarse al servidor.

* Argumentos:

   * `master`:: Un valor de cadena que representa la dirección IP o el nombre del equipo del equipo que ejecuta el nodo del repositorio principal.
   * `username`:: Nombre que se va a utilizar para autenticarse con el clúster.
   * `password`:: La contraseña que se usará para la autenticación.

* Valor devuelto: none

**** traversalCheckTraverses y, opcionalmente, corrige incoherencias en un subárbol que comienzan en un nodo específico. Esto se trata en detalle en la documentación sobre los administradores de persistencia.

**** consistenciaCheckChecks y opcionalmente corrige la coherencia en el almacén de datos. Esto se trata en detalle en la documentación del almacén de datos.

## Estadísticas del repositorio (TimeSeries) {#repository-statistics-timeseries}

El valor del campo TimeSeries para cada tipo de estadística que `org.apache.jackrabbit.api.stats.RepositoryStatistics` define.

* Dominio: `com.adobe.granite`
* Tipo: `TimeSeries`
* Nombre: Uno de los siguientes valores de la clase `org.apache.jackrabbit.api.stats.RepositoryStatistics.Type` Enum:

   * BUNDLE_CACHE_ACCESS_COUNTER
   * BUNDLE_CACHE_MISS_AVERAGE
   * BUNDLE_CACHE_MISS_COUNTER
   * BUNDLE_CACHE_MISS_DURATION
   * BUNDLE_CACHE_SIZE_COUNTER
   * BUNDLE_COUNTER
   * BUNDLE_READ_COUNTER
   * BUNDLE_WRITE_AVERAGE
   * BUNDLE_WRITE_COUNTER
   * BUNDLE_WRITE_DURATION
   * BUNDLE_WS_SIZE_COUNTER
   * CONSULTA_PROMEDIO
   * CONSULTA_COUNT
   * CONSULTA_DURACIÓN
   * SESSION_COUNT
   * SESSION_LOGIN_COUNTER
   * SESSION_READ_AVERAGE
   * SESSION_READ_COUNTER
   * SESSION_READ_DURATION
   * SESSION_WRITE_AVERAGE
   * SESSION_WRITE_COUNTER
   * SESSION_WRITE_DURATION

### Atributos {#attributes-1}

Se proporcionan los atributos siguientes para cada tipo de estadística del informe:

* ValuePerSecond: El valor medido por segundo durante el último minuto. Solo lectura.
* ValuePerMinute: El valor medido por minuto durante la última hora. Solo lectura.
* ValuePerHour: El valor medido por hora durante la última semana. Solo lectura.
* ValuePerWeek: El valor medido por semana durante los últimos tres años. Solo lectura.

## Estadísticas de Consulta del repositorio {#repository-query-stats}

Información estadística sobre consultas del repositorio.

* Dominio: com.adobe.granite
* Tipo: QueryStat

### Atributos {#attributes-2}

**** SlowQueriesInformación sobre las consultas del repositorio que han tardado más en completarse. Solo lectura.

**** SlowQueriesQueueSize El número máximo de consultas que se incluirán en la lista SlowQueries. Lectura-escritura.

**** PopularQueriesInformación sobre las consultas del repositorio que más se han producido. Solo lectura.

**** PopularQueriesQueueSize El número máximo de consultas en la lista PopularQueries. Lectura-escritura.

### Operaciones {#operations-2}

**** clearSlowQueriesQueueQuita todas las consultas de la lista SlowQueries.

* Argumentos: none
* Valor devuelto: none

**** clearPopularQueriesQueueQuita todas las consultas de la lista PopularQueries.

* Argumentos: none
* Valor devuelto: none

## Agentes de replicación {#replication-agents}

Monitorear los servicios para cada agente de replicación. Al crear un agente de replicación, el servicio aparece automáticamente en la consola JMX.

* **Dominio:** com.adobe.granite.Replication
* **Tipo:** agente
* **Nombre:** sin valor
* **Propiedades:** {id=&quot;*Name*&quot;}, donde  ** Nombre es el valor de la propiedad Agent Name.

### Atributos {#attributes-3}

**** IdValor de cadena que representa el identificador de la configuración del agente de replicación. Varios agentes pueden utilizar la misma configuración. Solo lectura.

**** VálidoValor booleano que indica si el agente está configurado correctamente:

* `true`:: Configuración válida.
* `false` :: La configuración contiene errores.

Solo lectura.

**** EnabledValor booleano que indica si el agente está habilitado:

* `true`: Activado.
* `false`: Deshabilitado.

**** QueueBlockedValor booleano que indica si la cola existe y está bloqueada:

* `true`: Bloqueado. Está pendiente un reintento automático.
* `false`:: No bloqueada o no existe.

Solo lectura.

**** QueuePausedValor booleano que indica si la cola de trabajos está en pausa:

* `true`:: Pausado (suspendido)
* `false`:: No se ha pausado o no existe.

Lectura-escritura.

**** QueueNumEntriesUn valor int que representa el número de trabajos en la cola del agente. Solo lectura.

**** QueueStatusTimeValor de fecha que indica la hora en que se obtuvieron los valores de estado mostrados en el servidor. El valor corresponde al tiempo en que se cargó la página. Solo lectura.

**colas** bloqueadas QueueNextRetryTimeFor, un valor de fecha que indica cuándo se realiza el siguiente reintento automático. Cuando no aparece tiempo, la cola no se bloquea. Solo lectura.

**** QueueProcessingSinceValor de fecha que indica cuándo se inició el procesamiento del trabajo actual. Cuando no aparece ningún tiempo, la cola se bloquea o está inactiva. Solo lectura.

**** QueueLastProcessTimeValor de fecha que indica cuándo se completó el trabajo anterior. Solo lectura.

### Operaciones {#operations-3}

**** queueForceRetryPara colas bloqueadas, envía el comando de reintento a la cola.

* Argumentos: none
* Valor devuelto: none

**** queueClearQuita todos los trabajos de la cola.

* Argumentos: none
* Valor devuelto: none

## Motor Sling {#sling-engine}

Proporciona estadísticas sobre las solicitudes HTTP para que pueda supervisar el rendimiento del servicio SlingRequestProcessor.

* Dominio: org.apache.sling
* Tipo: motor
* Propiedades: {service=RequestProcessor}

### Atributos {#attributes-4}

**** SolicitudesCount El número de solicitudes que se han producido desde la última vez que se restablecieron las estadísticas.

**** MinRequestDurationMsec La cantidad de tiempo más corta (en milisegundos) necesaria para procesar una solicitud desde que se restablecieron las estadísticas por última vez.

**** MaxRequestDurationMsec La mayor cantidad de tiempo (en milisegundos) necesaria para procesar una solicitud desde la última vez que se restablecieron las estadísticas.

**** StandardDeviationDurationMsec La desviación estándar de la cantidad de tiempo necesaria para procesar solicitudes. La desviación estándar se calcula usando todas las solicitudes desde la última vez que se restablecieron las estadísticas.

**** MeanRequestDurationMsec La cantidad media de tiempo necesaria para procesar una solicitud. La media se calcula usando todas las solicitudes desde la última vez que se restablecieron las estadísticas

### Operaciones {#operations-4}

**** resetStatisticsEstablece todas las estadísticas en cero. Restablezca las estadísticas cuando necesite analizar el rendimiento de procesamiento de solicitudes durante un intervalo de tiempo específico.

* Argumentos: none
* Valor devuelto: none

**** idRepresentación de cadena del ID del paquete.

**** installingValor booleano que indica si el paquete está instalado:

* `true`: Instalado.
* `false`: No está instalado.

**** installByEl ID del usuario que instaló el paquete por última vez.

**** installDate La fecha en que se instaló el paquete por última vez.

**** sizeValor largo que contiene el tamaño del paquete en bytes.


## Iniciador de inicio rápido {#quickstart-launcher}

Información sobre el proceso de inicio y el iniciador de inicio rápido.

* Dominio: com.adobe.granite.quickstart
* Tipo: Iniciador

### Operaciones {#operations-5}

**registro**

Muestra un mensaje en la ventana de inicio rápido.

Argumentos:

* p1: Un valor `String` que representa el mensaje que se va a mostrar.
* Valor devuelto: none

**startupFinished**

Llama al método startupFinished del iniciador del servidor. El método intenta abrir la página de bienvenida en un navegador web.

* Argumentos: none
* Valor devuelto: none

**startupProgress**

Establece el valor de finalización del proceso de inicio del servidor. La barra de progreso de la ventana QuickStart representa el valor de finalización.

* Argumentos:
   * p1: Un valor flotante que representa la cantidad del proceso de inicio que se ha completado, como fracción. El valor debe estar entre cero y uno. Por ejemplo, 0,3 indica que se ha completado el 30 %.
* Valor devuelto: ninguno.

## Servicios de terceros {#third-party-services}

Varios recursos de servidor de terceros instalan MBeans que exponen atributos y operaciones a la consola JMX. La siguiente tabla lista los recursos de terceros y proporciona vínculos a más información.

<table>
 <tbody>
  <tr>
   <th>Dominio</th>
   <th>Tipo</th>
   <th>Clase MBean</th>
  </tr>
  <tr>
   <td>Implementación de JMImation</td>
   <td>MBeanServerDelegate</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/MBeanServerDelegate.html">javax.management.MBeanServerDelegate</a></td>
  </tr>
  <tr>
   <td>com.sun.management</td>
   <td>HotSpotDiagnostic</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/jre/api/management/extension/com/sun/management/HotSpotDiagnosticMXBean.html">com.sun.management.HotSpotDiagnosticMXBean</a></td>
  </tr>
  <tr>
   <td>java.lang</td>
   <td>
    <ul>
     <li>ClassLoading</li>
     <li>Compilación</li>
     <li>GarbageCollector</li>
     <li>Memoria</li>
     <li>MemoryManager</li>
     <li>MemoryPool</li>
     <li>Sistema operativo</li>
     <li>Tiempo de ejecución</li>
     <li>Threading</li>
    </ul> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/package-summary.html">javax.</a> management package</td>
  </tr>
  <tr>
   <td>java.util.logging</td>
   <td> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/java/util/logging/LoggingMXBean.html">java.util.logging.LoggingMXBean</a></td>
  </tr>
  <tr>
   <td>osgi.core</td>
   <td>
    <ul>
     <li>bundleState</li>
     <li>marco</li>
     <li>packageState</li>
     <li>serviceState</li>
    </ul> </td>
   <td><a href="https://osgi.org/specification/osgi.enterprise/7.0.0/service.jmx.html#d0e42567">org.osgi.jmx.</a> frameworkpackage</td>
  </tr>
 </tbody>
</table>

## Uso de la consola de JMX {#using-the-jmx-console}

La consola JMX muestra información sobre varios servicios que se ejecutan en el servidor:

* Atributos: Propiedades de servicio como configuraciones o datos de tiempo de ejecución. Los atributos pueden ser de sólo lectura o de lectura y escritura.
* Operaciones: Comandos que se pueden invocar en el servicio.

Los MBeans que se implementan con un servicio OSGi exponen atributos y operaciones de servicio a la consola. El MBean determina los atributos y las operaciones que se exponen y si los atributos son de sólo lectura o de lectura y escritura.

La página principal de la consola JMX incluye una tabla de servicios. Cada fila de la tabla representa un servicio expuesto por un MBean.

1. Abra la consola web y haga clic en la ficha JMX. ([http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
2. Haga clic en un valor de celda de un servicio para ver los atributos y las operaciones del servicio.
3. Para cambiar un valor de atributo, haga clic en el valor, especifique el valor en el cuadro de diálogo que aparece y haga clic en Guardar.
4. Para invocar una operación de servicio, haga clic en el nombre de la operación, especifique los valores de los argumentos en el cuadro de diálogo que aparece y haga clic en Invocar.

## Uso de Aplicaciones JMX Externas para Monitoreo {#using-external-jmx-applications-for-monitoring}

CRX permite que las aplicaciones externas interactúen con Managed Beans (MBeans) mediante [Java Management Extensions (JMX)](https://docs.oracle.com/javase/6/docs/technotes/guides/management/overview.html). El uso de consolas genéricas como [JConsole](https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html) o aplicaciones de monitoreo específicas del dominio, permite obtener y configurar configuraciones y propiedades de CRX, así como monitorear el rendimiento y el uso de los recursos.

### Uso de JConsole para conectarse a CRX {#using-jconsole-to-connect-to-crx}

Para conectarse a CRX mediante JConsole, siga estos pasos:

1. Abra una ventana de terminal.
1. Introduzca el siguiente comando:

   `jconsole`

JConsole aparecerá en inicio y la ventana de JConsole.

### Conexión a un proceso CRX local {#connecting-to-a-local-crx-process}

JConsole mostrará una lista de los procesos locales de la máquina virtual Java. La lista contendrá dos procesos de inicio rápido. Seleccione el proceso &quot;CHILD&quot; de inicio rápido de la lista de procesos locales (generalmente el que tiene el PID más alto).

![screen_shot_2012-03-26at114557am](assets/screen_shot_2012-03-26at114557am.png)

### Conexión a un proceso CRX remoto {#connecting-to-a-remote-crx-process}

Para conectarse a un proceso CRX remoto, el JVM que aloja el proceso CRX remoto deberá estar habilitado para aceptar conexiones JMX remotas.

Para habilitar conexiones JMX remotas, se debe establecer la siguiente propiedad del sistema al iniciar la JVM:

`com.sun.management.jmxremote.port=portNum`

En la propiedad anterior, `portNum` es el número de puerto a través del cual desea habilitar las conexiones RMI de JMX. Asegúrese de especificar un número de puerto no utilizado. Además de publicar un conector RMI para el acceso local, al configurar esta propiedad se publica un conector RMI adicional en un registro privado de sólo lectura en el puerto especificado con un nombre conocido, &quot;jmxrmi&quot;.

De forma predeterminada, cuando se habilita el agente JMX para la supervisión remota, se utiliza la autenticación por contraseña basada en un archivo de contraseña que debe especificarse con la siguiente propiedad del sistema al iniciar la VM de Java:

`com.sun.management.jmxremote.password.file=pwFilePath`

Consulte la [documentación relevante de JMX](https://docs.oracle.com/javase/6/docs/technotes/guides/management/agent.html) para obtener instrucciones detalladas sobre cómo configurar un archivo de contraseña.

Ejemplo:

```shell
$ java
  -Dcom.sun.management.jmxremote.password.file=pwFilePath
  -Dcom.sun.management.jmxremote.port=8463
  -jar ./cq-quickstart.jar
```

### Uso de los MBeans proporcionados por CRX {#using-the-mbeans-provided-by-crx}

Después de conectarse al proceso de inicio rápido, JConsole proporciona una serie de herramientas generales de monitoreo para el JVM en el que CRX se está ejecutando.

![screen_shot_2012-03-26at115056am](assets/screen_shot_2012-03-26at115056am.png)

Para acceder a las opciones de supervisión y configuración internas de CRX, vaya a la ficha MBeans y, en el árbol de contenido jerárquico de la izquierda, seleccione la sección Atributos o Operaciones en la que esté interesado. Por ejemplo, la sección com.adobe.granite/Repository/Operations.

En esa sección, seleccione el atributo o la operación que desee en el panel izquierdo.

![screen_shot_2012-03-26at115728am](assets/screen_shot_2012-03-26at115728am.png)

