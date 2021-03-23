---
title: Recolección de papelera del almacén de datos
seo-title: Recolección de papelera del almacén de datos
description: Obtenga información sobre cómo configurar la colección de residuos del almacén de datos para liberar espacio en disco.
seo-description: Obtenga información sobre cómo configurar la colección de residuos del almacén de datos para liberar espacio en disco.
uuid: 49488a81-986a-4d1a-96c8-aeb6595fc094
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5b1e46c5-7e56-433e-b62e-2a76ea7be0fd
docset: aem65
translation-type: tm+mt
source-git-commit: 7035c19a109ff67655ee0419aa37d1723e2189cc
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 0%

---


# Recolección de papelera del almacén de datos {#data-store-garbage-collection}

Cuando se elimina un recurso de WCM convencional, la referencia al registro de almacén de datos subyacente se puede eliminar de la jerarquía de nodos, pero el registro de almacén de datos en sí permanece. A continuación, este registro de almacén de datos sin referencia se convierte en &quot;basura&quot; que no es necesario conservar. En los casos en que existen varios activos basura, es beneficioso deshacerse de ellos para conservar el espacio y optimizar el performance del backup y mantenimiento del filesystem.

En su mayor parte, una aplicación WCM tiende a recopilar información, pero no a eliminarla casi con la misma frecuencia. Aunque se añaden nuevas imágenes, incluso las versiones antiguas que se reemplazan, el sistema de control de versiones conserva la anterior y admite la reversión si es necesario. Por lo tanto, la mayor parte del contenido que pensamos como añadido al sistema se almacena de forma permanente. Entonces, ¿cuál es la fuente típica de &quot;basura&quot; en el repositorio que tal vez queramos limpiar?

AEM utiliza el repositorio como almacenamiento para una serie de actividades internas y de mantenimiento de la página:

* Paquetes creados y descargados
* Archivos temporales creados para la replicación de publicación
* Cargas del flujo de trabajo
* Recursos creados temporalmente durante la renderización DAM

Cuando alguno de estos objetos temporales es lo suficientemente grande como para requerir almacenamiento en el almacén de datos, y cuando el objeto termina de usarse, el propio registro del almacén de datos permanece como &quot;basura&quot;. En una aplicación de autor/publicación WCM típica, la fuente más grande de basura de este tipo suele ser el proceso de activación de la publicación. Cuando los datos se replican en Publicar, se recopilan primero en colecciones con un formato de datos eficiente denominado &quot;Durbo&quot; y se almacenan en el repositorio en `/var/replication/data`. Los paquetes de datos suelen superar el umbral de tamaño crítico para el almacén de datos y, por lo tanto, terminan almacenados como registros del almacén de datos. Cuando se completa la replicación, se elimina el nodo de `/var/replication/data`, pero el registro del almacén de datos permanece como &quot;basura&quot;.

Otra fuente de basura recuperable son los paquetes. Los datos del paquete, como todo lo demás, se almacenan en el repositorio y, por lo tanto, para paquetes de más de 4 KB, en el almacén de datos. En el curso de un proyecto de desarrollo o con el paso del tiempo mientras se mantiene un sistema, los paquetes se pueden crear y reconstruir muchas veces, cada compilación resulta en un nuevo registro de almacén de datos, lo que orfiere el registro de la compilación anterior.

## ¿Cómo funciona la colección de residuos del almacén de datos? {#how-does-data-store-garbage-collection-work}

Si el repositorio se ha configurado con un almacén de datos externo, la [colección de residuos del almacén de datos se ejecutará automáticamente](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) como parte de la ventana de mantenimiento semanal. El administrador del sistema también puede [ejecutar manualmente la colección de residuos del almacén de datos](#running-data-store-garbage-collection) según sea necesario. En general, se recomienda que la colección de basura del almacén de datos se realice periódicamente, pero que se tengan en cuenta los siguientes factores al planificar la recogida de residuos en el almacén de datos:

* Las colecciones de residuos del almacén de datos tardan un tiempo y pueden afectar al rendimiento, por lo que deben planificarse en consecuencia.
* La eliminación de los registros de residuos del almacén de datos no afecta al rendimiento normal, por lo que no se trata de una optimización del rendimiento.
* Si la utilización del almacenamiento de información y factores relacionados como los tiempos de backup no son un problema, entonces la recolección de basura del almacén de datos podría diferirse de forma segura.

El recolector de residuos del almacén de datos realiza primero una nota de la marca de tiempo actual cuando comienza el proceso. A continuación, la colección se lleva a cabo mediante un algoritmo de patrón de marca/barrido de varios pasos.

En la primera fase, el recolector de basura del almacén de datos realiza una travesía completa de todo el contenido del repositorio. Para cada objeto de contenido que tiene una referencia a un registro de almacén de datos, localizó el archivo en el sistema de archivos, realizando una actualización de metadatos — modificando el atributo &quot;última modificación&quot; o MTIME. En este punto, los archivos a los que se accede mediante esta fase pasan a ser más recientes que la marca de tiempo de la línea de base inicial.

En la segunda fase, el recolector de residuos del almacén de datos atraviesa la estructura de directorios físicos del almacén de datos de la misma manera que una &quot;búsqueda&quot;. Examinó el atributo &quot;last modified&quot; o MTIME del archivo y realiza la siguiente determinación:

* Si el MTIME es más reciente que la marca de tiempo de la línea de base inicial, entonces el archivo se encontró en la primera fase o es un archivo completamente nuevo que se agregó al repositorio mientras el proceso de recopilación estaba en curso. En cualquiera de estos casos se considerará que el registro está activo y no se eliminará el expediente.
* Si el MTIME es anterior a la marca de tiempo de la línea de base inicial, entonces el archivo no es un archivo al que se hace referencia activamente y se considera un residuo extraíble.

Este método funciona bien para un nodo único con un almacén de datos privado. Sin embargo, el almacén de datos puede compartirse. Si es así, las referencias activas potenciales a los registros del almacén de datos de otros repositorios no se comprueban y los archivos de referencia activos pueden eliminarse por error. Es imperativo que el administrador del sistema comprenda la naturaleza compartida del almacén de datos antes de planificar cualquier colección de residuos y utilice únicamente el proceso de recopilación de residuos del almacén de datos integrado cuando se sepa que el almacén de datos no se comparte.

>[!NOTE]
>
>Al realizar la colección de residuos en una configuración de almacén de datos agrupada o compartida (con Mongo o Segment Tar), el registro puede mostrar advertencias sobre la incapacidad de eliminar ciertos ID de blob. Esto sucede porque otros clústeres o nodos compartidos a los que no hay información sobre las eliminaciones de ID hacen referencia incorrectamente a los ID de blob eliminados en una colección de residuos anterior. Como resultado, cuando se realiza la colección de residuos, registra una advertencia cuando intenta eliminar un ID que ya se ha eliminado en la última ejecución. Este comportamiento no afecta al rendimiento ni a la funcionalidad.

## Ejecución de la colección de residuos del almacén de datos {#running-data-store-garbage-collection}

Existen tres maneras de ejecutar la colección de residuos del almacén de datos, según la configuración del almacén de datos en la que AEM se esté ejecutando:

1. A través de [Revision Cleanup](/help/sites-deploying/revision-cleanup.md) - un mecanismo de colección de residuos que normalmente se utiliza para la limpieza del almacén de nodos.

1. A través de [Data Store Garbage Collection](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-operations-dashboard) : un mecanismo de recopilación de residuos específico para almacenes de datos externos, disponible en el Tablero de operaciones.
1. A través de la [Consola JMX](/help/sites-administering/jmx-console.md).

Si TarMK se está utilizando como almacén de nodos y como almacén de datos, la limpieza de revisión se puede utilizar para la colección de residuos tanto del almacén de nodos como del almacén de datos. Sin embargo, si se configura un almacén de datos externo, como el almacén de datos del sistema de archivos, la colección de residuos del almacén de datos debe activarse de forma explícita y separada de la limpieza de revisión. La colección de residuos del almacén de datos se puede activar mediante el panel Operaciones o la consola JMX.

La tabla siguiente muestra el tipo de colección de residuos del almacén de datos que debe utilizarse para todas las implementaciones de almacén de datos admitidas en el AEM 6:

<table>
 <tbody>
  <tr>
   <td><strong>Almacenamiento de nodos</strong><br /> </td>
   <td><strong>Almacén de datos</strong></td>
   <td><strong>Mecanismo de colección de residuos</strong><br /> </td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>TarMK</td>
   <td>Limpieza de revisión (los binarios están en línea con el Almacenamiento de segmentos)</td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>Sistema de archivos externos</td>
   <td><p>Tarea de colección de residuos del almacén de datos a través del panel de operaciones</p> <p>Consola JMX</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>MongoDB</td>
   <td><p>Tarea de colección de residuos del almacén de datos a través del panel de operaciones</p> <p>Consola JMX</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>Sistema de archivos externos</td>
   <td><p>Tarea de colección de residuos del almacén de datos a través del panel de operaciones</p> <p>Consola JMX</p> </td>
  </tr>
 </tbody>
</table>

### Ejecución de la colección de residuos del almacén de datos mediante el panel de operaciones {#running-data-store-garbage-collection-via-the-operations-dashboard}

La ventana de mantenimiento semanal integrada, disponible a través del [Tablero de operaciones](/help/sites-administering/operations-dashboard.md), contiene una tarea integrada para almacenar en déclencheur la colección de residuos del almacén de datos a la 1 a. m. los domingos.

Si necesita ejecutar la colección de residuos del almacén de datos fuera de este tiempo, se puede activar manualmente mediante el panel de operaciones.

Antes de ejecutar la colección de residuos del almacén de datos, debe comprobar que no se estén ejecutando copias de seguridad en ese momento.

1. Abra el Tablero de operaciones **Navegación** -> **Herramientas** -> **Operaciones** -> **Mantenimiento**.
1. Toque o haga clic en la **Ventana de mantenimiento semanal**.

   ![imagen_1-64](assets/chlimage_1-64.png)

1. Seleccione la tarea **Colección de residuos del almacén de datos** y, a continuación, toque o haga clic en el icono **Ejecutar**.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. La colección de residuos del almacén de datos se ejecuta y su estado se muestra en el panel.

   ![imagen_1-66](assets/chlimage_1-66.png)

>[!NOTE]
>
>La tarea de colección de residuos del almacén de datos solo estará visible si ha configurado un almacén de datos de archivos externos. Consulte [Configuración de almacenes de nodos y almacenes de datos en AEM 6](/help/sites-deploying/data-store-config.md#file-data-store) para obtener información sobre cómo configurar un almacén de datos de archivos.

### Ejecución de la colección de residuos del almacén de datos a través de la consola JMX {#running-data-store-garbage-collection-via-the-jmx-console}

Esta sección trata sobre la ejecución manual de la colección de residuos del almacén de datos a través de la consola JMX. Si la instalación está configurada sin un almacén de datos externo, esto no se aplica a la instalación. En su lugar, consulte las instrucciones sobre cómo ejecutar Revision cleanup en [Mantenimiento del repositorio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).

>[!NOTE]
>
>Si está ejecutando TarMK con un almacén de datos externo, primero debe ejecutar la limpieza de revisión para que la colección de residuos sea efectiva.

Para ejecutar la colección de residuos:

1. En la Consola de administración Apache Felix OSGi, resalte la pestaña **Main** y seleccione **JMX** en el siguiente menú.
1. A continuación, busque y haga clic en **Repository Manager** MBean (o vaya a `https://<host>:<port>/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Drepository+manager%2Ctype%3DRepositoryManagement`).
1. Haga clic en **startDataStoreGC(boolean markOnly)**.
1. introduzca &quot;`true`&quot; para el parámetro `markOnly` si es necesario:

   | **Opción** | **Descripción** |
   |---|---|
   | boolean markOnly | Configúrelo en true para marcar únicamente las referencias y no barrer en la operación de marcar y barrer. Este modo se utilizará cuando el BlobStore subyacente se comparta entre varios repositorios diferentes. Para todos los demás casos, configúrelo en false para realizar la colección de residuos completa. |

1. Haga clic en **Invocar**. CRX ejecuta la colección de residuos e indica cuándo se ha completado.

>[!NOTE]
>
>La colección de residuos del almacén de datos no recopilará los archivos que se hayan eliminado en las últimas 24 horas.

>[!NOTE]
>
>La tarea de colección de residuos del almacén de datos solo se iniciará si ha configurado un almacén de datos de archivos externos. Si no se ha configurado un almacén de datos de archivo externo, la tarea devolverá el mensaje `Cannot perform operation: no service of type BlobGCMBean found` después de invocar. Consulte [Configuración de almacenes de nodos y almacenes de datos en AEM 6](/help/sites-deploying/data-store-config.md#file-data-store) para obtener información sobre cómo configurar un almacén de datos de archivos.

## Automatización de la colección de residuos del almacén de datos {#automating-data-store-garbage-collection}

Si es posible, la colección de residuos del almacén de datos debe ejecutarse cuando haya poca carga en el sistema, por ejemplo por la mañana.

La ventana de mantenimiento semanal integrada, disponible a través del [Tablero de operaciones](/help/sites-administering/operations-dashboard.md), contiene una tarea integrada para almacenar en déclencheur la colección de residuos del almacén de datos a la 1 a. m. los domingos. También debe comprobar que no hay copias de seguridad en ejecución en este momento. El inicio de la ventana de mantenimiento se puede personalizar mediante el panel de control según sea necesario.

>[!NOTE]
>
>El motivo para no ejecutarlo simultáneamente es que los archivos antiguos (y no utilizados) del almacén de datos también reciban una copia de seguridad, de modo que si es necesario volver a una revisión anterior, los binarios aún se encuentren en la copia de seguridad.

Si no desea ejecutar la colección de residuos del almacén de datos con la ventana de mantenimiento semanal en el panel de operaciones, también se puede automatizar mediante los clientes HTTP wget o curl. A continuación se muestra un ejemplo de cómo automatizar la copia de seguridad mediante curl:

>[!CAUTION]
>
>En el siguiente ejemplo comandos `curl` puede que sea necesario configurar varios parámetros para la instancia; por ejemplo, el nombre de host ( `localhost`), el puerto ( `4502`), la contraseña de administrador ( `xyz`) y varios parámetros para la colección de residuos del almacén de datos real.

Este es un ejemplo de comando curl para invocar la colección de residuos del almacén de datos a través de la línea de comandos:

```shell
curl -u admin:admin -X POST --data markOnly=true  https://localhost:4503/system/console/jmx/org.apache.jackrabbit.oak"%"3Aname"%"3Drepository+manager"%"2Ctype"%"3DRepositoryManagement/op/startDataStoreGC/boolean
```

El comando curl devuelve inmediatamente.

## Comprobación de la coherencia del almacén de datos {#checking-data-store-consistency}

La comprobación de coherencia del almacén de datos informará de cualquier binario del almacén de datos que falte pero al que se siga haciendo referencia. Para iniciar una comprobación de coherencia, siga estos pasos:

1. Vaya a la consola JMX. Para obtener información sobre cómo utilizar la consola JMX, consulte [este artículo](/help/sites-administering/jmx-console.md#using-the-jmx-console).
1. Busque el **BlobGarbageCollection** Mbean y haga clic en él.
1. Haga clic en el enlace `checkConsistency()`.

Una vez completada la comprobación de coherencia, un mensaje mostrará el número de binarios que se han notificado como faltantes. Si el número es bueno a 0, compruebe `error.log` para obtener más información sobre los binarios que faltan.

A continuación encontrará un ejemplo de cómo se informan los binarios que faltan en los registros:

```xml
11:32:39.673 INFO [main] MarkSweepGarbageCollector.java:600 Consistency check found [1] missing blobs
```

```xml
11:32:39.673 WARN [main] MarkSweepGarbageCollector.java:602 Consistency check failure intheblob store : DataStore backed BlobStore [org.apache.jackrabbit.oak.plugins.blob.datastore.OakFileDataStore], check missing candidates in file /tmp/gcworkdir-1467352959243/gccand-1467352959243
```

