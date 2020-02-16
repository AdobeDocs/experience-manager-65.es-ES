---
title: Backup y Restore
seo-title: Backup y Restore
description: Obtenga información sobre cómo realizar copias de seguridad y restaurar el contenido de AEM.
seo-description: Obtenga información sobre cómo realizar copias de seguridad y restaurar el contenido de AEM.
uuid: 446a466f-f508-4430-9e50-42cd4463760e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: eb8bbb85-ca2f-4877-8ee0-bb1ee8b7d8de
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# Backup y Restore{#backup-and-restore}

Existen dos formas de realizar copias de seguridad y restaurar el contenido del repositorio en AEM:

* Puede crear una copia de seguridad externa del repositorio y almacenarla en una ubicación segura. Si el repositorio se desglosa, puede restaurarlo al estado anterior.
* Puede crear versiones internas del contenido del repositorio. Estas versiones se almacenan en el repositorio junto con el contenido, para que pueda restaurar rápidamente los nodos y los árboles que haya cambiado o eliminado.

## General {#general}

El enfoque descrito aquí se aplica para el backup y la recuperación del sistema.

Si necesita realizar una copia de seguridad o recuperar una pequeña cantidad de contenido, que se pierde, no necesariamente se requiere una recuperación del sistema:

* Puede recuperar los datos de otro sistema mediante un paquete
* o restaura la copia de seguridad en un sistema temporal, cree un paquete de contenido e impleméntelo en el sistema, donde falta este contenido.

Para obtener más información, consulte [Copia de seguridad](/help/sites-administering/backup-and-restore.md#package-backup) del paquete más abajo.

## Temporización {#timing}

No ejecute la copia de seguridad en paralelo con la recolección de elementos no utilizados del almacén de datos, ya que podría dañar los resultados de ambos procesos.

## Backup sin conexión {#offline-backup}

Siempre puede realizar una copia de seguridad sin conexión. Esto requiere un tiempo de inactividad de AEM, pero puede ser bastante eficiente en cuanto al tiempo necesario en comparación con un respaldo en línea.

En la mayoría de los casos, utilizará una instantánea del filesystem para crear una copia de sólo lectura del almacenamiento de información en ese momento. Para crear una copia de seguridad sin conexión, siga estos pasos:

* detener la aplicación
* hacer una copia de seguridad de instantánea
* iniciar la aplicación

Dado que el backup de copias instantáneas generalmente tarda sólo unos segundos, el tiempo de inactividad completo es de menos de unos minutos.

## Backup en línea {#online-backup}

Este método de copia de seguridad crea una copia de seguridad de todo el repositorio, incluidas las aplicaciones implementadas en él, como AEM. La copia de seguridad incluye contenido, historial de versiones, configuración, software, revisiones, aplicaciones personalizadas, archivos de registro, índices de búsqueda, etc. Si utiliza la agrupación en clúster y si la carpeta compartida es un subdirectorio de `crx-quickstart` (físicamente o mediante un vínculo de software), también se realiza una copia de seguridad del directorio compartido.

Puede restaurar todo el repositorio (y cualquier aplicación) más adelante.

Este método funciona como una copia de seguridad &quot;en caliente&quot; o &quot;en línea&quot; para que se pueda realizar mientras se ejecuta el repositorio. Por lo tanto, el repositorio se puede utilizar mientras se ejecuta la copia de seguridad. Este método funciona para las instancias de repositorio predeterminadas basadas en almacenamiento de etiquetas.

Al crear una copia de seguridad, tiene las siguientes opciones:

* Realizar una copia de seguridad en un directorio mediante la herramienta de copia de seguridad integrada de AEM.
* Realizar una copia de seguridad en un directorio mediante una instantánea del sistema de archivos

En cualquier caso, la copia de seguridad crea una imagen (o instantánea) del repositorio. Luego, el agente de backup de sistemas debe tener cuidado de transferir esta imagen a un sistema de backup dedicado (unidad de cinta).

>[!NOTE]
>
>Si la función de copia de seguridad en línea de AEM se utiliza en una instancia de AEM que tiene una configuración de tipo bogavante personalizada, se recomienda configurar la ruta del almacén de datos para que esté fuera del directorio &quot; `crx-quickstart`&quot; y realizar una copia de seguridad del almacén de datos por separado.

>[!CAUTION]
>
>La copia de seguridad en línea sólo realiza una copia de seguridad del sistema de archivos. Si almacena el contenido del repositorio y/o los archivos del repositorio en una base de datos, dicha base de datos debe realizarse de forma independiente. Si utiliza AEM con MongoDB, consulte la documentación sobre cómo utilizar las herramientas [de copia de seguridad nativas de](https://docs.mongodb.org/manual/tutorial/backup-with-mongodump/)MongoDB.

### Backup en línea de AEM {#aem-online-backup}

Una copia de seguridad en línea del repositorio le permite crear, descargar y eliminar archivos de copia de seguridad. Se trata de una función de copia de seguridad &quot;en caliente&quot; o &quot;en línea&quot;, por lo que se puede ejecutar mientras el repositorio se utiliza normalmente en modo de lectura y escritura.

>[!CAUTION]
>
>No ejecute AEM Online Backup al mismo tiempo que [Datastore Garbage Collection](/help/sites-administering/data-store-garbage-collection.md) o [Revision Cleanup](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup). Afectará negativamente el rendimiento del sistema.

Al iniciar una copia de seguridad, puede especificar una ruta **de** destino y/o un **retraso**.

**Ruta** de destino Los archivos de copia de seguridad generalmente se guardan en la carpeta principal de la carpeta que contiene el archivo jar de inicio rápido (.jar). Por ejemplo, si el archivo AEM jar se encuentra en /InstallationKits/AEM, la copia de seguridad se generará en /InstallationKits. También puede especificar un objetivo para una ubicación de su elección.

Si **TargetPath** es un directorio, la imagen del repositorio se crea en este directorio. Si el mismo directorio se utiliza varias veces (o siempre) para almacenar la copia de seguridad,

* los archivos modificados del repositorio se modifican en consecuencia en TargetPath
* los archivos eliminados del repositorio se eliminan en TargetPath
* los archivos creados en el repositorio se crean en TargetPath

>[!NOTE]
>
>Si **TargetPath** se establece en filename con la extensión **.zip**, se realiza una copia de seguridad del repositorio en un directorio temporal y, a continuación, el contenido de este directorio temporal se comprime y almacena en el archivo ZIP.
>
>Este enfoque se desalienta, porque
>
>* requiere almacenamiento de disco adicional durante el proceso de copia de seguridad (directorio temporal más el archivo zip)
>* el proceso de compresión lo realiza el repositorio y puede influir en su rendimiento.
>* Retrasa el proceso de backup.
>* Hasta Java 1.6 Java sólo puede crear archivos ZIP de hasta 4 gigabytes.
>
>
Si necesita crear un ZIP como formato de copia de seguridad, debe realizar una copia de seguridad en un directorio y luego utilizar un programa de compresión para crear el archivo zip.

**Retraso** Indica un retraso de tiempo (en milisegundos) para que el rendimiento del repositorio no se vea afectado. De forma predeterminada, la copia de seguridad del repositorio se ejecuta a toda velocidad. Puede ralentizar la creación de una copia de seguridad en línea para que no ralentice otras tareas.

Cuando utilice un retraso muy grande, asegúrese de que el backup en línea no dure más de 24 horas. Si lo hizo, descarte esta copia de seguridad, ya que podría no contener todos los binarios.
Un retraso de 1 milisegundo suele dar como resultado un uso del 10% de la CPU y un retraso de 10 milisegundos suele dar como resultado un uso de menos del 3% de la CPU. El retraso total en segundos se puede calcular de la siguiente manera: Tamaño del repositorio en MB, multiplicado por retraso en milisegundos, dividido por 2 (si se utiliza la opción zip) o dividido por 4 (al realizar una copia de seguridad en un directorio). Esto significa que una copia de seguridad en un directorio de un repositorio de 200 MB con una demora de 1 ms aumenta el tiempo de backup en unos 50 segundos.

>[!NOTE]
>
>Consulte [Cómo funciona](#how-aem-online-backup-works) AEM Online Backup para obtener detalles internos del proceso.

Para crear una copia de seguridad:

1. Inicie sesión en AEM como administrador.

1. Vaya a **Herramientas - Operaciones - Copia de seguridad.**
1. Haga clic en **Crear**. Se abrirá la consola de respaldo.

   ![chlimage_1-1](assets/chlimage_1-1a.png)

1. En la consola de copia de seguridad, especifique la ruta **[de](#aem-online-backup)**destino y el**[ retraso](#aem-online-backup)**.

   ![chlimage_1-2](assets/chlimage_1-2a.png)

   >[!NOTE]
   >
   >La consola de copia de seguridad también está disponible mediante:
   >
   >
   >` https://<*hostname*>:<*port-number*>/libs/granite/backup/content/admin.html`

1. Haga clic en **Guardar**, una barra de progreso indicará el progreso de la copia de seguridad.

   >[!NOTE]
   >
   >Puede **cancelar** una copia de seguridad en ejecución en cualquier momento.

1. Una vez finalizada la copia de seguridad, los archivos zip aparecen en la ventana de copia de seguridad.

   ![climage_1-3](assets/chlimage_1-3a.png)

   >[!NOTE]
   >
   >Los archivos de copia de seguridad que ya no se necesitan se pueden eliminar con la consola. Seleccione el archivo de copia de seguridad en el panel izquierdo y haga clic en **Eliminar**.

   >[!NOTE]
   >
   >Si ha realizado una copia de seguridad en un directorio: una vez finalizado el proceso de copia de seguridad, AEM no escribirá en el directorio de destino.

### Automatización del backup en línea de AEM {#automating-aem-online-backup}

Si es posible, la copia de seguridad en línea debe ejecutarse cuando haya poca carga en el sistema, por ejemplo por la mañana.

Las copias de seguridad se pueden automatizar mediante los clientes `wget` o `curl` HTTP. A continuación se muestran ejemplos de cómo automatizar el backup mediante curl.

#### Realizar una copia de seguridad del directorio de Target predeterminado {#backing-up-to-the-default-target-directory}

>[!CAUTION]
>
>En el siguiente ejemplo, es posible que sea necesario configurar varios parámetros del `curl` comando para la instancia; por ejemplo, el nombre de host ( `localhost`), el puerto ( `4502`), la contraseña de administrador ( `xyz`) y el nombre de archivo ( `backup.zip`).

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=backup.zip
```

El archivo o directorio de copia de seguridad se crea en el servidor en la carpeta principal de la carpeta que contiene la `crx-quickstart` carpeta (igual que si se creara la copia de seguridad mediante el navegador). Por ejemplo, si ha instalado AEM en el directorio `/InstallationKits/crx-quickstart/`, la copia de seguridad se crea en el `/InstallationKits` directorio.

El comando curl se devuelve inmediatamente, por lo que debe controlar este directorio para ver cuándo está listo el archivo zip. Mientras se crea la copia de seguridad, se puede ver un directorio temporal (con el nombre basado en el del archivo zip final), al final se comprimirá. Por ejemplo:

* nombre del archivo zip resultante: `backup.zip`
* nombre del directorio temporal: `backup.f4d5.temp`

#### Realizar una copia de seguridad de un directorio de Target no predeterminado {#backing-up-to-a-non-default-target-directory}

Normalmente, el archivo o directorio de copia de seguridad se crea en el servidor en la carpeta principal de la carpeta que contiene la `crx-quickstart` carpeta.

Si desea guardar la copia de seguridad (de cualquier tipo) en una ubicación diferente, puede establecer una ruta absoluta &quot;al `target` parámetro en el `curl` comando.

Por ejemplo, para generar `backupJune.zip` en el directorio `/Backups/2012`:

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=/Backups/2012/backupJune.zip"
```

>[!CAUTION]
>
>Al utilizar un servidor de aplicaciones diferente (como JBoss), es posible que la copia de seguridad en línea no funcione según lo esperado, ya que el directorio de destino no se puede escribir. En este caso, póngase en contacto con la asistencia técnica.

>[!NOTE]
>
>También se puede activar una copia de seguridad [con los MBeans proporcionados por AEM](/help/sites-administering/jmx-console.md).

### Backup de Instantánea del Sistema de Archivos {#filesystem-snapshot-backup}

El proceso descrito aquí es especialmente adecuado para repositorios grandes.

>[!NOTE]
>
>Si desea utilizar este método de copia de seguridad, su sistema debe admitir copias instantáneas del filesystem. Por ejemplo, para Linux esto significa que sus sistemas de ficheros deben colocarse en un volumen lógico.

1. Realice una instantánea del sistema de archivos en el que se implementa AEM.

1. Monte la instantánea del sistema de archivos.
1. Realice una copia de seguridad y desmonte la instantánea.

### Cómo funciona AEM Online Backup {#how-aem-online-backup-works}

El respaldo en línea de AEM consta de una serie de acciones internas para garantizar la integridad de los datos a los que se realiza una copia de seguridad y la creación de los archivos de copia de seguridad. Éstos se enumeran a continuación para los interesados.

La copia de seguridad en línea utiliza el siguiente algoritmo:

1. Al crear un archivo zip, el primer paso es crear o localizar el directorio de destino.

   * Si realiza una copia de seguridad en un archivo zip, se crea un directorio temporal. El nombre del directorio comienza por `backup.` y termina por `.temp`; por ejemplo `backup.f4d3.temp`.
   * Si realiza una copia de seguridad en un directorio, se utiliza el nombre especificado en la ruta de destino. Se puede utilizar un directorio existente; de lo contrario, se creará un nuevo directorio.

      Cuando se inicia la copia de seguridad, se crea un archivo vacío denominado `backupInProgress.txt` en el directorio de destino. Este archivo se elimina cuando la copia de seguridad finaliza.

1. Los archivos se copian del directorio de origen al directorio de destino (o directorio temporal al crear un archivo zip). El almacén de segmentos se copia antes del almacén de datos para evitar daños en el repositorio. Los datos de índice y caché se omiten al crear la copia de seguridad. Como resultado, los datos de `crx-quickstart/repository/cache` y no `crx-quickstart/repository/index` se incluyen en la copia de seguridad. El indicador de la barra de progreso del proceso se encuentra entre 0% y 70% al crear un archivo zip, o entre 0% y 100% si no se crea ningún archivo zip.

1. Si la copia de seguridad se está realizando en un directorio preexistente, se eliminarán los archivos &quot;antiguos&quot; del directorio de destino. Los archivos antiguos son archivos que no existen en el directorio de origen.

Los archivos se copian en el directorio de destino en cuatro etapas:

1. En la primera etapa de la copia (indicador de progreso 0% - 63% al crear un archivo zip o 0% - 90% si no se crea ningún archivo zip), todos los archivos se copian mientras el repositorio se ejecuta normalmente. El proceso consta de dos fases:

   * Fase A: todo se copia excepto el almacén de datos (con retraso).
   * Fase B: solo se copia el almacén de datos (con retraso).

1. En la segunda etapa de la copia (indicador de progreso 63% - 65,8% al crear un archivo zip o 90% - 94% si no se crea ningún archivo zip), solo se copian los archivos creados o modificados en el directorio de origen desde que se inició la primera etapa de la copia. En función de la actividad del repositorio, esto puede variar desde ningún archivo hasta un número significativo de archivos (ya que la primera etapa de copia de archivos suele tardar mucho tiempo). El proceso de copia es similar a la primera etapa (fase A y fase B con retraso).
1. En la tercera etapa de copia (indicador de progreso 65,8% - 68,6% al crear un archivo zip o 94% - 98% si no se crea ningún archivo zip), solo se copian los archivos que se crearon o modificaron en el directorio de origen desde que se inició la segunda etapa de copia. Según la actividad del repositorio, es posible que no haya archivos para copiar o que haya un número muy pequeño de archivos (ya que la segunda etapa de copia de archivos suele ser rápida). El proceso de copia es similar a la segunda etapa: Fase A y Fase B, pero sin demora.
1. Las etapas de copia de archivos de uno a tres se realizan al mismo tiempo que se ejecuta el repositorio. Solo se copian los archivos creados o modificados en el directorio de origen desde que se inició la tercera etapa de copia. Según la actividad del repositorio, es posible que no haya archivos para copiar, o que haya un número muy, muy pequeño de archivos (porque la segunda etapa de copia de archivos suele ser muy rápida). Indicador de progreso 68,6% - 70% al crear un archivo zip o 98% - 100% si no se crea ningún archivo zip. El proceso de copia es similar a la tercera etapa.
1. Según el objetivo:

   * Si se ha especificado un archivo zip, ahora se crea desde el directorio temporal. Indicador de progreso 70% - 100%. A continuación, se elimina el directorio temporal.
   * Si el destino era un directorio, el archivo vacío llamado `backupInProgress.txt` se elimina para indicar que la copia de seguridad ha finalizado.

## Restauración de la copia de seguridad {#restoring-the-backup}

Puede restaurar una copia de seguridad de la siguiente manera:

* En caso de que realice una copia de seguridad de instantáneas del sistema de archivos, puede simplemente restaurar una imagen del sistema.
* En caso de que haya creado la copia de seguridad como archivo zip, solo tiene que descomprimir el contenido en una nueva carpeta e iniciar AEM desde esa ubicación.

## Copia de seguridad de paquetes {#package-backup}

Para realizar copias de seguridad y restaurar contenido, puede utilizar uno de los administradores de paquetes, que utiliza el formato de paquete de contenido para realizar copias de seguridad y restaurar contenido. El Administrador de paquetes proporciona más flexibilidad para definir y administrar paquetes.

Para obtener más información sobre las características y los sacrificios de cada uno de estos formatos de paquete de contenido individual, consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md).

### Alcance del backup {#scope-of-backup}

Cuando realiza una copia de seguridad de nodos mediante el Administrador de paquetes o el Zipper de contenido, CRX guarda la siguiente información:

* El contenido del repositorio debajo del árbol seleccionado.
* Definiciones de tipo de nodo que se utilizan para el contenido del que realiza una copia de seguridad.
* Definiciones de espacio de nombres que se utilizan para el contenido del que realiza una copia de seguridad.

Al realizar la copia de seguridad, AEM pierde la siguiente información:

* Historial de versiones.

