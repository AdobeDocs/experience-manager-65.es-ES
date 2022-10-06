---
title: Copia de seguridad y restauración
seo-title: Backup and Restore
description: Aprenda a realizar copias de seguridad y restaurar el contenido de AEM.
seo-description: Learn how to backup and restore your AEM content.
uuid: 446a466f-f508-4430-9e50-42cd4463760e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: eb8bbb85-ca2f-4877-8ee0-bb1ee8b7d8de
exl-id: dd26dade-b769-483e-bc11-dcfa5ed1f87e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2283'
ht-degree: 0%

---

# Copia de seguridad y restauración{#backup-and-restore}

Hay dos maneras de hacer backup y restaurar el contenido del repositorio en AEM:

* Puede crear una copia de seguridad externa del repositorio y almacenarla en una ubicación segura. Si el repositorio se desglosa, puede restaurarlo al estado anterior.
* Puede crear versiones internas del contenido del repositorio. Estas versiones se almacenan en el repositorio junto con el contenido, por lo que puede restaurar rápidamente los nodos y árboles que haya cambiado o eliminado.

## General {#general}

El enfoque descrito aquí se aplica para backup y recuperación del sistema.

Si necesita realizar una copia de seguridad o recuperar una pequeña cantidad de contenido, que se pierde, no es necesario que recupere el sistema:

* Puede recuperar los datos de otro sistema a través de un paquete
* o restaura la copia de seguridad en un sistema temporal, cree un paquete de contenido e impleméntelo en el sistema, donde falta este contenido.

Para obtener más información, consulte [Copia de seguridad de paquetes](/help/sites-administering/backup-and-restore.md#package-backup) más abajo.

## Temporización {#timing}

No ejecute la copia de seguridad en paralelo con la colección de residuos del almacén de datos, ya que podría dañar los resultados de ambos procesos.

## Copia de seguridad sin conexión {#offline-backup}

Siempre puede realizar una copia de seguridad sin conexión. Esto requiere un tiempo de inactividad de AEM, pero puede ser bastante eficiente en términos de tiempo necesario en comparación con un backup en línea.

En la mayoría de los casos, utilizará una instantánea del sistema de archivos para crear una copia de sólo lectura del almacenamiento en ese momento. Para crear una copia de seguridad sin conexión, siga estos pasos:

* detener la aplicación
* hacer una copia de seguridad de instantánea
* iniciar la aplicación

Como la copia de seguridad de la instantánea suele tardar sólo unos segundos, todo el tiempo de inactividad es inferior a unos minutos.

## Copia de seguridad en línea {#online-backup}

Este método de copia de seguridad crea una copia de seguridad de todo el repositorio, incluidas las aplicaciones implementadas bajo él, como AEM. La copia de seguridad incluye contenido, historial de versiones, configuración, software, revisiones, aplicaciones personalizadas, archivos de registro, índices de búsqueda, etc. Si utiliza clústeres y si la carpeta compartida es un subdirectorio de `crx-quickstart` (físicamente o utilizando un enlace de software), también se realiza una copia de seguridad del directorio compartido.

Puede restaurar todo el repositorio (y cualquier aplicación) más adelante.

Este método funciona como una copia de seguridad &quot;en caliente&quot; o &quot;en línea&quot; para que se pueda realizar mientras se ejecuta el repositorio. Por lo tanto, el repositorio se puede utilizar mientras se ejecuta la copia de seguridad. Este método funciona para las instancias de repositorio predeterminadas, basadas en almacenamiento de Tar.

Al crear una copia de seguridad, tiene las siguientes opciones:

* Copia de seguridad a un directorio mediante AEM herramienta de copia de seguridad integrada.
* Copia de seguridad a un directorio mediante una instantánea de filesystem

En cualquier caso, la copia de seguridad crea una imagen (o instantánea) del repositorio. Luego, el agente de backup de sistemas debe tener cuidado de transferir esta imagen a un sistema de backup dedicado (unidad de cinta).

>[!NOTE]
>
>Si AEM función Copia de seguridad en línea se utiliza en una instancia de AEM que tiene una configuración de blobstore personalizada, se recomienda configurar la ruta del almacén de datos para que esté fuera del &quot; `crx-quickstart`&quot; y haga una copia de seguridad del almacén de datos por separado.

>[!CAUTION]
>
>La copia de seguridad en línea solo realiza una copia de seguridad del sistema de archivos. Si almacena el contenido del repositorio o los archivos del repositorio en una base de datos, dicha base de datos debe realizar una copia de seguridad por separado. Si está utilizando AEM con MongoDB, consulte la documentación sobre cómo usar la variable [Herramientas de copia de seguridad nativas de MongoDB](https://docs.mongodb.org/manual/tutorial/backup-with-mongodump/).

### AEM copia de seguridad en línea {#aem-online-backup}

Una copia de seguridad en línea del repositorio le permite crear, descargar y eliminar archivos de copia de seguridad. Es una función de copia de seguridad &quot;en caliente&quot; o &quot;en línea&quot;, por lo que se puede ejecutar mientras el repositorio se esté utilizando normalmente en modo de lectura-escritura.

>[!CAUTION]
>
>No ejecutar AEM copia de seguridad en línea simultáneamente con [Colección de residuos del almacén de datos](/help/sites-administering/data-store-garbage-collection.md) o [Limpieza de revisión](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup). Afectará negativamente al rendimiento del sistema.

Al iniciar una copia de seguridad, puede especificar una **Ruta de destino** y/o **Retraso**.

**Ruta de destino** Los archivos de copia de seguridad generalmente se guardan en la carpeta principal de la carpeta que contiene el archivo jar de inicio rápido (.jar). Por ejemplo, si tiene el archivo jar AEM ubicado en /InstallationKits/AEM, la copia de seguridad se generará en /InstallationKits. También puede especificar un objetivo para una ubicación de su elección.

Si la variable **TargetPath** es un directorio, la imagen del repositorio se crea en este directorio. Si el mismo directorio se utiliza varias veces (o siempre) para almacenar la copia de seguridad,

* los archivos modificados en el repositorio se modifican según corresponda en TargetPath
* Los archivos eliminados en el repositorio se eliminan en TargetPath
* los archivos creados en el repositorio se crean en TargetPath

>[!NOTE]
>
>If **TargetPath** se establece en nombre de archivo con la extensión **.zip**, el repositorio se copia de seguridad en un directorio temporal y, a continuación, el contenido de este directorio temporal se comprime y se almacena en el archivo ZIP.
>
>Se desaconseja este enfoque, porque
>
>* requiere almacenamiento de disco adicional durante el proceso de copia de seguridad (directorio temporal más el archivo zip)
>* el proceso de compresión lo realiza el repositorio y puede influir en su rendimiento.
>* Retrasa el proceso de copia de seguridad.
>* Hasta Java 1.6 Java solo puede crear archivos ZIP de hasta un tamaño de 4 gigabytes.
>
>Si necesita crear un ZIP como formato de copia de seguridad, debe realizar una copia de seguridad en un directorio y, a continuación, utilizar un programa de compresión para crear el archivo zip.

**Retraso** Indica un retraso de tiempo (en milisegundos), para que el rendimiento del repositorio no se vea afectado. De forma predeterminada, la copia de seguridad del repositorio se ejecuta a toda velocidad. Puede ralentizar la creación de una copia de seguridad en línea para que no ralentice otras tareas.

Cuando utilice un retraso muy grande, asegúrese de que la copia de seguridad en línea no tarde más de 24 horas. Si lo hizo, descarte esta copia de seguridad, ya que puede que no contenga todos los binarios.
Un retraso de 1 milisegundo suele dar como resultado un uso de CPU del 10%, y un retraso de 10 milisegundos normalmente da como resultado menos del 3% de uso de CPU. El retraso total en segundos se puede calcular de la siguiente manera: El tamaño del repositorio en MB, multiplicado por el retraso en milisegundos, dividido por 2 (si se utiliza la opción zip) o dividido por 4 (cuando se realiza la copia de seguridad en un directorio). Esto significa que una copia de seguridad en un directorio de un repositorio de 200 MB con una demora de 1 ms aumenta el tiempo de backup en unos 50 segundos.

>[!NOTE]
>
>Consulte [Cómo funciona AEM copia de seguridad en línea](#how-aem-online-backup-works) para obtener detalles internos del proceso.

Para crear una copia de seguridad:

1. Inicie sesión en AEM como administrador.

1. Vaya a **Herramientas - Operaciones - Copia de seguridad.**
1. Haga clic en **Crear**. Se abrirá la consola de copia de seguridad.

   ![Chlimage_1-1](assets/chlimage_1-1a.png)

1. En la consola de copia de seguridad, especifique la variable **[Ruta de destino](#aem-online-backup)** y **[Retraso](#aem-online-backup)**.

   ![Chlimage_1-2](assets/chlimage_1-2a.png)

   >[!NOTE]
   >
   >La consola de copia de seguridad también está disponible mediante:
   >
   >
   >` https://<*hostname*>:<*port-number*>/libs/granite/backup/content/admin.html`

1. Haga clic en **Guardar**, una barra de progreso indicará el progreso de la copia de seguridad.

   >[!NOTE]
   >
   >Puede **Cancelar** una copia de seguridad en ejecución en cualquier momento.

1. Cuando se completa la copia de seguridad, los archivos zip se enumeran en la ventana de copia de seguridad.

   ![Chlimage_1-3](assets/chlimage_1-3a.png)

   >[!NOTE]
   >
   >Los archivos de copia de seguridad que ya no son necesarios se pueden eliminar mediante la consola. Seleccione el archivo de copia de seguridad en el panel izquierdo y haga clic en **Eliminar**.

   >[!NOTE]
   >
   >Si ha realizado una copia de seguridad en un directorio: una vez finalizado el proceso de copia de seguridad, AEM no escribirá en el directorio de destino.

### Automatización AEM Backup en Línea {#automating-aem-online-backup}

Si es posible, la copia de seguridad en línea debe ejecutarse cuando haya poca carga en el sistema, por ejemplo por la mañana.

Las copias de seguridad se pueden automatizar mediante la `wget` o `curl` Clientes HTTP. A continuación se muestran ejemplos de cómo automatizar la copia de seguridad mediante curl.

#### Copia de seguridad hasta el directorio de destino predeterminado {#backing-up-to-the-default-target-directory}

>[!CAUTION]
>
>En el siguiente ejemplo, varios parámetros de la variable `curl` puede que sea necesario configurar el comando para su instancia; por ejemplo, el nombre de host ( `localhost`), puerto ( `4502`), contraseña de administrador ( `xyz`) y nombre de archivo ( `backup.zip`).

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=backup.zip
```

El archivo o directorio de copia de seguridad se crea en el servidor en la carpeta principal de la carpeta que contiene la variable `crx-quickstart` (igual que si creara la copia de seguridad con el explorador). Por ejemplo, si ha instalado AEM en el directorio `/InstallationKits/crx-quickstart/`y, a continuación, la copia de seguridad se crea en la variable `/InstallationKits` directorio.

El comando curl se devuelve inmediatamente, por lo que debe controlar este directorio para ver cuándo el archivo zip está listo. Mientras se crea la copia de seguridad, se puede ver un directorio temporal (con el nombre basado en el del archivo zip final), al final se comprimirá. Por ejemplo:

* nombre del archivo zip resultante: `backup.zip`
* nombre del directorio temporal: `backup.f4d5.temp`

#### Copia de seguridad a un directorio de destino no predeterminado {#backing-up-to-a-non-default-target-directory}

Normalmente, el archivo o directorio de copia de seguridad se crea en el servidor en la carpeta principal de la carpeta que contiene la variable `crx-quickstart` carpeta.

Si desea guardar la copia de seguridad (de cualquier tipo) en una ubicación diferente, puede establecer una ruta absoluta &quot;al `target` en el `curl` comando.

Por ejemplo, para generar `backupJune.zip` en el directorio `/Backups/2012`:

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=/Backups/2012/backupJune.zip"
```

>[!CAUTION]
>
>Cuando se usa un servidor de aplicaciones diferente (como JBoss), es posible que la copia de seguridad en línea no funcione según lo esperado, ya que el directorio de destino no se puede escribir. En este caso, póngase en contacto con el servicio de asistencia técnica.

>[!NOTE]
>
>También se puede activar una copia de seguridad [uso de los MBeans proporcionados por AEM](/help/sites-administering/jmx-console.md).

### Copia de seguridad de instantánea del sistema de archivos {#filesystem-snapshot-backup}

El proceso descrito aquí es especialmente apropiado para repositorios grandes.

>[!NOTE]
>
>Si desea utilizar este método de backup, su sistema debe admitir instantáneas de filesystem. Por ejemplo, para Linux esto significa que sus filesystems deberían colocarse en un volumen lógico.

1. Haga una instantánea del sistema de archivos AEM está implementado en.

1. Monte la instantánea del sistema de archivos.
1. Realice una copia de seguridad y desinstale la instantánea.

### Cómo funciona AEM copia de seguridad en línea {#how-aem-online-backup-works}

AEM copia de seguridad en línea consta de una serie de acciones internas para garantizar la integridad de los datos de los que se hace backup y los archivos de copia de seguridad que se están creando. A continuación se enumeran para los interesados.

La copia de seguridad en línea utiliza el siguiente algoritmo:

1. Al crear un archivo zip, el primer paso es crear o localizar el directorio de destino.

   * Si se realiza la copia de seguridad en un archivo zip, se crea un directorio temporal. El nombre del directorio empieza por `backup.` y termina con `.temp`; por ejemplo `backup.f4d3.temp`.
   * Si se realiza una copia de seguridad en un directorio, se utiliza el nombre especificado en la ruta de destino. Se puede utilizar un directorio existente; de lo contrario, se creará un directorio nuevo.

      Un archivo vacío llamado `backupInProgress.txt` se crea en el directorio de destino cuando se inicia la copia de seguridad. Este archivo se elimina cuando finaliza la copia de seguridad.

1. Los archivos se copian del directorio de origen al directorio de destino (o al directorio temporal al crear un archivo zip). El almacén de segmentos se copia antes del almacén de datos para evitar que se dañe el repositorio. Los datos de índice y caché se omiten al crear la copia de seguridad. Como resultado, los datos de `crx-quickstart/repository/cache` y `crx-quickstart/repository/index` no se incluye en la copia de seguridad. El indicador de barra de progreso del proceso está entre 0% - 70% al crear un archivo zip, o entre 0% - 100% si no se crea ningún archivo zip.

1. Si la copia de seguridad se está realizando en un directorio preexistente, se eliminan los archivos &quot;antiguos&quot; del directorio de destino. Los archivos antiguos son archivos que no existen en el directorio de origen.

Los archivos se copian en el directorio de destino en cuatro etapas:

1. En la primera etapa de copia (indicador de progreso 0% - 63% al crear un archivo zip o 0% - 90% si no se crea ningún archivo zip), todos los archivos se copian mientras el repositorio se ejecuta normalmente. El proceso consta de dos fases:

   * Fase A: todo se copia excepto para el almacén de datos (con retraso).
   * Fase B: solo se copia el almacén de datos (con retraso).

1. En la segunda etapa de copia (indicador de progreso 63% - 65,8% al crear un archivo zip o 90% - 94% si no se crea ningún archivo zip) solo se copian los archivos creados o modificados en el directorio de origen desde que se inició la primera etapa de copia. Dependiendo de la actividad del repositorio, esto puede variar desde ningún archivo hasta un número significativo de archivos (porque la primera etapa de copia de archivos suele tardar mucho tiempo). El proceso de copia es similar a la primera etapa (Fase A y Fase B con retraso).
1. En la tercera etapa de copia (indicador de progreso 65,8% - 68,6% al crear un archivo zip o 94% - 98% si no se crea ningún archivo zip) solo se copian los archivos creados o modificados en el directorio de origen desde que se inició la segunda etapa de copia. Según la actividad del repositorio, es posible que no haya archivos para copiar o que haya un número muy pequeño de archivos (porque la segunda etapa de copia de archivos suele ser rápida). El proceso de copia es similar a la segunda etapa: Fase A y Fase B, pero sin demora.
1. Las etapas de copia de archivos de una a tres se realizan simultáneamente mientras se ejecuta el repositorio. Solo se copian los archivos creados o modificados en el directorio de origen desde que se inició la tercera etapa de copia. Dependiendo de la actividad del repositorio, puede que no haya archivos para copiar, o que haya un número muy, muy pequeño de archivos (porque la segunda etapa de copia de archivos suele ser muy rápida). Indicador de progreso 68,6% - 70% al crear un archivo zip o 98% - 100% si no se crea ningún archivo zip. El proceso de copia es similar a la tercera etapa.
1. Según el objetivo:

   * Si se especificó un archivo zip, ahora se crea desde el directorio temporal. Indicador de progreso 70% - 100%. A continuación, se elimina el directorio temporal.
   * Si el destino era un directorio, el archivo vacío llamado `backupInProgress.txt` se elimina para indicar que la copia de seguridad ha finalizado.

## Restauración de la copia de seguridad {#restoring-the-backup}

Puede restaurar una copia de seguridad de la siguiente manera:

* En caso de que realice una copia de seguridad de instantánea del sistema de archivos, simplemente puede restaurar una imagen del sistema.
* En caso de que haya creado la copia de seguridad como archivo zip, solo tiene que descomprimir el contenido en una carpeta nueva e iniciar AEM desde esa ubicación.

## Copia de seguridad de paquetes {#package-backup}

Para realizar copias de seguridad y restaurar contenido, puede utilizar uno de los administradores de paquetes, que utiliza el formato de paquete de contenido para realizar copias de seguridad y restaurar contenido. El Administrador de paquetes proporciona más flexibilidad para definir y administrar paquetes.

Para obtener más información sobre las características y las compensaciones de cada uno de estos formatos de paquete de contenido, consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md).

### Alcance del backup {#scope-of-backup}

Al realizar copias de seguridad de nodos mediante el Administrador de paquetes o el Zipper de contenido, CRX guarda la siguiente información:

* El contenido del repositorio debajo del árbol que ha seleccionado.
* Las definiciones de tipo Node que se utilizan para el contenido del que realiza la copia de seguridad.
* Las definiciones de área de nombres que se utilizan para el contenido del que realiza la copia de seguridad.

Al realizar una copia de seguridad, AEM pierde la siguiente información:

* El historial de versiones.
