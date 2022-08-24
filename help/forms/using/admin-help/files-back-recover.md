---
title: Archivos para realizar copias de seguridad y recuperar
seo-title: Files to back up and recover
description: Este documento describe la aplicación y los archivos de datos de los que se debe realizar una copia de seguridad.
seo-description: This document describes the application and data files that must be backed up.
uuid: ba04adb9-675a-48f2-ad52-39c1266e423b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f9a294d-24bd-4e4b-b929-2809f5e6cef9
exl-id: d2dd381d-a7d2-4fec-a8ba-7ca037fd9dc1
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 0%

---

# Archivos para realizar copias de seguridad y recuperar {#files-to-back-up-and-recover}

La aplicación y los archivos de datos de los que se debe realizar una copia de seguridad se describen con más detalle en las secciones siguientes.

Tenga en cuenta los siguientes puntos con respecto al backup y la recuperación:

* Se debe realizar una copia de seguridad de la base de datos antes de GDS y AEM repositorio.
* Si necesita desplegar los nodos en un entorno agrupado para backup, asegúrese de que los nodos secundarios estén apagados antes del nodo principal. De lo contrario, puede provocar incoherencia en el clúster o el servidor. Además, el nodo principal debe activarse antes que cualquier nodo secundario.
* Para la operación de restauración de un clúster, el servidor de aplicaciones debe detenerse para cada nodo del clúster.

## Directorio global de almacenamiento de documentos {#global-document-storage-directory}

El GDS es un directorio utilizado para almacenar archivos de larga duración que se utilizan en un proceso. La duración de los archivos de larga duración está pensada para abarcar uno o más lanzamientos de un sistema de formularios AEM, y puede abarcar días e incluso años. Estos archivos de larga duración pueden incluir PDF, políticas y plantillas de formulario. Los archivos de larga duración son una parte fundamental del estado general de muchas implementaciones de formularios AEM. Si se pierden o dañan algunos o todos los documentos de larga duración, el servidor de formularios puede volverse inestable.

Los documentos de entrada para la invocación asincrónica de trabajos también se almacenan en el GDS y deben estar disponibles para procesar solicitudes. Por lo tanto, es importante que considere la fiabilidad del sistema de archivos que aloja el GDS y que emplee una matriz redundante de discos independientes (RAID) u otra tecnología adecuada para sus requisitos de calidad y nivel de servicio.

La ubicación del GDS se determina durante el proceso de instalación de los formularios de AEM o más tarde mediante la consola de administración. Además de mantener una ubicación de alta disponibilidad para GDS, también puede habilitar el almacenamiento de bases de datos para documentos. Consulte [Opciones de copia de seguridad cuando se utiliza la base de datos para el almacenamiento de documentos](files-back-recover.md#backup-options-when-database-is-used-for-document-storage).

### Ubicación de GDS {#gds-location}

Si deja vacío el ajuste de ubicación durante la instalación, el valor predeterminado de la ubicación es un directorio en la instalación del servidor de aplicaciones. Debe realizar una copia de seguridad del siguiente directorio para el servidor de aplicaciones:

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

Si ha cambiado la ubicación de GDS a una ubicación no predeterminada, puede determinarla de la siguiente manera:

* Inicie sesión en la consola de administración y haga clic en Configuración > Configuración del sistema principal > Configuraciones.
* Registre la ubicación especificada en el cuadro Directorio global de almacenamiento de documentos.

En un entorno agrupado, el GDS suele apuntar a un directorio que se comparte en la red y al que se puede acceder de lectura y escritura para cada nodo del clúster.

La ubicación del GDS puede cambiarse durante una recuperación si la ubicación original ya no está disponible. (Consulte [Cambio de la ubicación de GDS durante la recuperación](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).)

### Opciones de copia de seguridad cuando se utiliza la base de datos para el almacenamiento de documentos {#backup-options-when-database-is-used-for-document-storage}

Puede habilitar AEM almacenamiento de documentos de formularios en la base de datos de formularios de AEM mediante la consola de administración. Aunque esta opción mantiene todos los documentos persistentes en la base de datos, AEM formularios siguen requiriendo el directorio GDS basado en el sistema de archivos porque se utiliza para almacenar archivos permanentes y temporales y recursos relacionados con sesiones e invocaciones de formularios AEM.

Cuando selecciona la opción &quot;Habilitar el almacenamiento de documentos en la base de datos&quot; en la configuración del sistema principal de la consola de administración o mediante Configuration Manager, AEM formularios no permiten el modo de copia de seguridad de instantáneas ni el modo de copia de seguridad móvil. Por lo tanto, no es necesario administrar los modos de copia de seguridad mediante AEM formularios. Si utiliza esta opción, debe realizar una copia de seguridad del GDS solo una vez después de habilitar la opción. Cuando se recuperan AEM formularios de una copia de seguridad, no es necesario cambiar el nombre del directorio de copia de seguridad para el GDS ni restaurar el GDS.

## repositorio AEM {#aem-repository}

AEM repositorio (crx-repository) se crea si crx-repository está configurado al instalar AEM formularios. La ubicación del directorio crx-repository se determina durante el proceso de instalación de formularios AEM. Se requiere AEM copia de seguridad y restauración del repositorio junto con la base de datos y GDS para obtener datos de formularios AEM coherentes en AEM formularios. AEM repositorio contiene datos para la solución de gestión de correspondencia, Forms Manager y AEM Forms Workspace.

### Solución de administración de correspondencia {#correspondence-management-solution}

Correspondence Management Solution centraliza y administra la creación, el ensamblaje y la entrega de correspondencia segura, personalizada e interactiva. Le permite ensamblar rápidamente la correspondencia de contenido preaprobado y creado a medida en un proceso optimizado, desde la creación hasta el archivado. Como resultado, sus clientes obtienen comunicación oportuna, precisa, conveniente, segura y relevante. Su empresa maximiza el valor de las interacciones con los clientes y minimiza los costos y los riesgos con un proceso optimizado para facilitar, acelerar y aumentar la productividad.

Una sencilla configuración de la solución de gestión de correspondencia incluye una instancia de autor y una instancia de publicación en el mismo equipo o en diferentes equipos

### administrador de formularios {#forms-manager}

forms manager optimiza el proceso de actualización, administración y retirada de formularios.

### AEM Forms Workspace {#html-workspace}

AEM Forms Workspace coincide con las capacidades de Flex Workspace (obsoleto para AEM formularios en JEE) y agrega nuevas funciones para ampliar e integrar Workspace y facilitar el uso.

>[!NOTE]
>
>Flex Workspace está en desuso para AEM versión de formularios.

Permite la administración de tareas en clientes sin Flash Player ni Adobe Reader. Facilita la representación de Forms HTML, además de los PDF forms y los formularios de Flex.

## base de datos de AEM forms {#aem-forms-database}

La base de datos de AEM forms almacena contenido como artefactos de formulario, configuraciones de servicio, estado de proceso y referencias de base de datos a archivos del GDS y del directorio raíz de almacenamiento de contenido (para Content Services). Los backups de bases de datos se pueden realizar en tiempo real sin interrupciones en el servicio, y la recuperación puede ser hasta un punto específico en el tiempo o a un cambio en particular. En esta sección se describe cómo configurar la base de datos para que se pueda realizar una copia de seguridad en tiempo real.

En un sistema de formularios AEM correctamente configurado, el administrador del sistema y el administrador de la base de datos pueden colaborar fácilmente para recuperar el sistema a un estado coherente y conocido.

Para realizar una copia de seguridad de la base de datos en tiempo real, debe utilizar el modo de instantánea o configurar la base de datos para que se ejecute en el modo de registro especificado. Esto permite realizar una copia de seguridad de los archivos de la base de datos mientras la base de datos está abierta y disponible para su uso. Además, la base de datos conserva sus registros de reversión y transacciones cuando se ejecuta en estos modos.

>[!NOTE]
>
>Adobe® Content Services ES (obsoleto) es un sistema de administración de contenido instalado con LiveCycle. Permite a los usuarios diseñar, administrar, monitorear y optimizar procesos centrados en el ser humano. La compatibilidad con los servicios de contenido (obsoletos) finaliza el 31/12/2014. Consulte [Documento de ciclo de vida del producto de Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

### DB2 {#db2}

Configure la base de datos DB2 para que se ejecute en el modo de registro de archivos.

>[!NOTE]
>
>Si el entorno de AEM forms se actualizó desde una versión anterior de AEM formularios y utiliza DB2, no se admite la copia de seguridad en línea. En este caso, debe cerrar AEM formularios y realizar una copia de seguridad sin conexión. Las futuras versiones de AEM formularios admitirán la copia de seguridad en línea para los clientes de actualización.

IBM tiene un conjunto de herramientas y sistemas de ayuda para ayudar a los administradores de bases de datos a administrar sus tareas de backup y recuperación:

* Acelerador de registro de archivos IBM DB2
* Experto en el archivo de datos de IBM DB2

DB2 tiene funcionalidades incorporadas para hacer backup de una base de datos en Tivoli Storage Manager. Mediante Tivoli Storage Manager, los backups DB2 se pueden almacenar en otros medios o en el disco duro local.

### Oracle {#oracle}

Utilice copias de seguridad instantáneas o configure la base de datos de Oracle para que se ejecute en el modo de registro de archivos. (Consulte [Copia de seguridad de oracle: Introducción](https://www.databasedesign-resource.com/oracle-backup.md).) Para obtener más información sobre la copia de seguridad y la recuperación de la base de datos de Oracle, visite estos sitios:

[Backup y Recuperación de oracle:](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) Explica los conceptos de backup y recuperación y las técnicas más comunes para usar Recovery Manager (RMAN) para backup, recuperación y reporting en forma más detallada, así como para proporcionar más información sobre cómo planificar una estrategia de backup y recuperación.

[Guía del Usuario de Backup y Recuperación de la Base de Datos oracle:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) Proporciona información detallada sobre la arquitectura RMAN, conceptos y mecanismos de backup y recuperación, técnicas de recuperación avanzadas como funcionalidades de recuperación puntual y flashback de bases de datos, y ajuste del performance de backup y recuperación. También abarca el backup y la recuperación administrados por el usuario, usando instalaciones de sistemas operativos host en lugar de RMAN. Este volumen es esencial para el backup y la recuperación de implementaciones de bases de datos más sofisticadas y para escenarios de recuperación avanzados.

[Referencia de Backup y Recuperación de la Base de Datos de oracle:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) Proporciona información completa sobre sintaxis y semántica para todos los comandos RMAN, y describe las vistas de la base de datos que están disponibles para generar informes sobre actividades de backup y recuperación.

### SQL Server {#sql-server}

Utilice copias de seguridad instantáneas o configure la base de datos de SQL Server para que se ejecute en el modo de registro de transacciones.

SQL Server también proporciona dos herramientas de backup y recuperación:

* SQL Server Management Studio (GUI)
* T-SQL (línea de comandos)

Para obtener más información, consulte [Copia de seguridad y restauración](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx).

### MySQL {#mysql}

Utilice MySQLAdmin o modifique los archivos INI en Windows para configurar la base de datos MySQL para que se ejecute en modo de registro binario. (Consulte [Registro binario de MySQL](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html).) Una herramienta de copia de seguridad para MySQL también está disponible en el software InnoBase. (Consulte [Copia de seguridad en caliente de Innobase](https://www.innodb.com/hot-backup/features.md).)

>[!NOTE]
>
>El modo de registro binario predeterminado para MySQL es &quot;Declaración&quot;, que es incompatible con las tablas utilizadas por Content Services (Obsoleto). El uso del registro binario en este modo predeterminado provoca que los servicios de contenido (obsoletos) fallen. Si su sistema incluye servicios de contenido (obsoleto), utilice el modo de registro &quot;mixto&quot;. Para habilitar el registro &quot;mixto&quot;, agregue el siguiente argumento al archivo my.ini: `binlog_format=mixed log-bin=logname`

Puede utilizar la utilidad mysqldump para obtener la copia de seguridad completa de la base de datos. Es necesario realizar backups completos, pero no siempre resultan convenientes. Producen archivos de backup grandes y tardan tiempo en generarse. Para realizar una copia de seguridad incremental, asegúrese de iniciar el servidor con - `log-bin` como se describe en la sección anterior. Cada vez que el servidor MySQL se reinicia, deja de escribir en el registro binario actual, crea uno nuevo y, a partir de entonces, el nuevo se convierte en el actual. Puede forzar un conmutador manualmente con la variable `FLUSH LOGS SQL` comando. Después de la primera copia de seguridad completa, las siguientes copias de seguridad incrementales se realizan utilizando la utilidad mysqladmin con el `flush-logs` que crea el siguiente archivo de registro.

Consulte [Resumen de Estrategia de Copia de Seguridad](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html).

```text
binlog_format=mixed
log-bin=logname
```

## Directorio raíz del almacenamiento de contenido (solo servicios de contenido) {#content-storage-root-directory-content-services-only}

El directorio raíz del almacenamiento de contenido contiene el repositorio de Content Services (obsoleto) donde se almacenan todos los documentos, artefactos e índices. Se debe realizar una copia de seguridad del árbol del directorio raíz del almacenamiento de contenido. En esta sección se describe cómo determinar la ubicación del directorio raíz del almacenamiento de contenido para entornos independientes y en clúster.

### Ubicación raíz del almacenamiento de contenido (entorno independiente) {#content-storage-root-location-stand-alone-environment}

El directorio raíz del almacenamiento de contenido se crea cuando se instalan los servicios de contenido (obsoletos). La ubicación del directorio raíz del almacenamiento de contenido se determina durante el proceso de instalación de los formularios de AEM.

La ubicación predeterminada para el directorio raíz del almacenamiento de contenido es `[aem-forms root]/lccs_data`.

Haga una copia de seguridad de los siguientes directorios ubicados en el directorio raíz del almacenamiento de contenido:

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Si el directorio /backup-lucene-indexes no está presente, haga una copia de seguridad del directorio /lucene-indexes, también ubicado en el directorio raíz del almacenamiento de contenido. Si el directorio /backup-lucene-indexes está presente, no realice una copia de seguridad del directorio /lucene-indexes porque puede causar errores.

### Ubicación raíz del almacenamiento de contenido (entorno agrupado) {#content-storage-root-location-clustered-environment}

Cuando instala Content Services (Desaprobada) en un entorno agrupado, el directorio raíz del almacenamiento de contenido se divide en dos directorios separados:

**Directorio raíz del almacenamiento de contenido:** Normalmente, un directorio de red compartido accesible de lectura y escritura para todos los nodos del clúster

**Directorio raíz de índice:** Un directorio que se crea en cada nodo del clúster, que siempre tiene la misma ruta y nombre de directorio

La ubicación predeterminada para el directorio raíz del almacenamiento de contenido es `[GDS root]/lccs_data`, donde `[GDS root]` es la ubicación descrita en [Ubicación de GDS](files-back-recover.md#gds-location). Haga una copia de seguridad de los siguientes directorios ubicados en el directorio raíz del almacenamiento de contenido:

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Si el directorio /backup-lucene-indexes no está presente, haga una copia de seguridad del directorio /lucene-indexes, también ubicado en el directorio raíz del almacenamiento de contenido. Si el directorio /backup-lucene-indexes está presente, no realice una copia de seguridad del directorio /lucene-indexes porque puede causar errores.

La ubicación predeterminada para el directorio raíz del índice es `[aem-forms root]/lucene-indexes` en cada nodo.

## Fuentes instaladas por el cliente {#customer-installed-fonts}

Si ha instalado fuentes adicionales en el entorno de formularios AEM, debe realizar una copia de seguridad por separado. Haga una copia de seguridad de todos los directorios de fuentes de Adobe y cliente especificados en la consola de administración en Configuración > Sistema principal > Configuraciones. Asegúrese de realizar una copia de seguridad de todo el directorio de fuentes.

>[!NOTE]
>
>De forma predeterminada, las fuentes de Adobe instaladas con AEM formularios se encuentran en la variable `[aem-forms root]/fonts` directorio.

Si está reinicializando el sistema operativo en el equipo host y desea utilizar fuentes del sistema operativo anterior, también debe realizar una copia de seguridad del contenido del directorio de fuentes del sistema. (Para obtener instrucciones específicas, consulte la documentación de su sistema operativo).
