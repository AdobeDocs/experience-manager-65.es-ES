---
title: Archivos para realizar copias de seguridad y recuperar
seo-title: Archivos para realizar copias de seguridad y recuperar
description: Este documento describe la aplicación y los archivos de datos de los que se debe realizar una copia de seguridad.
seo-description: Este documento describe la aplicación y los archivos de datos de los que se debe realizar una copia de seguridad.
uuid: ba04adb9-675a-48f2-ad52-39c1266e423b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f9a294d-24bd-4e4b-b929-2809f5e6cef9
translation-type: tm+mt
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec

---


# Archivos para realizar copias de seguridad y recuperar {#files-to-back-up-and-recover}

La aplicación y los archivos de datos de los que se debe realizar una copia de seguridad se describen con más detalle en las siguientes secciones.

Considere los siguientes puntos con respecto al backup y la recuperación:

* Se debe realizar una copia de seguridad de la base de datos antes del repositorio GDS y AEM.
* Si necesita desglosar los nodos en un entorno en clúster para realizar copias de seguridad, asegúrese de que los nodos esclavos se cierren antes que el nodo maestro. De lo contrario, puede provocar incoherencias en el clúster o en el servidor. Además, el nodo maestro debe activarse antes que cualquier nodo esclavo.
* Para la operación de restauración de un clúster, el servidor de aplicaciones debe detenerse para cada nodo del clúster.

## Directorio global de almacenamiento de documentos {#global-document-storage-directory}

El GDS es un directorio que se utiliza para almacenar archivos de larga duración que se utilizan en un proceso. La duración de los archivos de larga duración está pensada para abarcar uno o varios lanzamientos de un sistema de formularios AEM y puede abarcar días e incluso años. Estos archivos de larga duración pueden incluir archivos PDF, políticas y plantillas de formulario. Los archivos de larga duración son una parte fundamental del estado general de muchas implementaciones de formularios AEM. Si se pierden o dañan algunos o todos los documentos de larga duración, el servidor de formularios puede volverse inestable.

Los documentos de entrada para la invocación asíncrona de trabajos también se almacenan en el GDS y deben estar disponibles para procesar solicitudes. Por lo tanto, es importante que considere la fiabilidad del sistema de archivos que aloja el GDS y utilice una matriz redundante de discos independientes (RAID) u otra tecnología, según corresponda, según sus necesidades de calidad y nivel de servicio.

La ubicación del GDS se determina durante el proceso de instalación de formularios AEM o posteriormente mediante la consola de administración. Además de mantener una ubicación de alta disponibilidad para GDS, también puede habilitar el almacenamiento de bases de datos para documentos. Consulte Opciones [de copia de seguridad cuando se utiliza la base de datos para el almacenamiento](files-back-recover.md#backup-options-when-database-is-used-for-document-storage)de documentos.

### Ubicación de GDS {#gds-location}

Si deja la configuración de ubicación vacía durante la instalación, la ubicación predeterminada es un directorio en la instalación del servidor de aplicaciones. Debe realizar una copia de seguridad del siguiente directorio para el servidor de aplicaciones:

* (JBoss) `[appserver root]/server/[server]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/[server]/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/[server]/DocumentStorage`

Si ha cambiado la ubicación de GDS a una ubicación no predeterminada, puede determinarla de la siguiente manera:

* Inicie sesión en la consola de administración y haga clic en Configuración > Configuración del sistema principal > Configuraciones.
* Registre la ubicación especificada en el cuadro Directorio global de almacenamiento de documentos.

En un entorno agrupado, el GDS suele apuntar a un directorio que se comparte en la red y que es accesible de lectura y escritura para cada nodo de clúster.

La ubicación del GDS puede cambiarse durante una recuperación si la ubicación original ya no está disponible. (Consulte [Cambio de la ubicación del GDS durante la recuperación](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)).

### Opciones de copia de seguridad cuando se utiliza la base de datos para el almacenamiento de documentos {#backup-options-when-database-is-used-for-document-storage}

Puede activar el almacenamiento de documentos de formularios AEM en la base de datos de formularios AEM mediante la consola de administración. Aunque esta opción mantiene todos los documentos persistentes en la base de datos, los formularios AEM siguen requiriendo el directorio GDS basado en el sistema de archivos, ya que se utiliza para almacenar archivos permanentes y temporales y recursos relacionados con sesiones e invocaciones de formularios AEM.

Al seleccionar la opción &quot;Activar almacenamiento de documentos en la base de datos&quot; en Configuración básica del sistema en la consola de administración o mediante Configuration Manager, los formularios AEM no permiten el modo de copia de seguridad de instantáneas ni el modo de copia de seguridad móvil. Por lo tanto, no es necesario administrar los modos de copia de seguridad mediante formularios AEM. Si utiliza esta opción, debe realizar una copia de seguridad del GDS una sola vez después de activar la opción. Cuando se recuperan formularios AEM de una copia de seguridad, no es necesario cambiar el nombre del directorio de copia de seguridad del GDS ni restaurar GDS.

## Repositorio de AEM {#aem-repository}

El repositorio de AEM (crx-repository) se crea si crx-repository está configurado durante la instalación de formularios AEM. La ubicación del directorio crx-repository se determina durante el proceso de instalación de formularios AEM. Se requiere la copia de seguridad y restauración del repositorio de AEM, junto con la base de datos y GDS, para obtener datos coherentes de formularios AEM en formularios AEM. El repositorio de AEM contiene datos para Correspondence Management Solution, Forms Manager y AEM Forms Workspace.

### Solución de administración de correspondencia {#correspondence-management-solution}

Correspondence Management Solution centraliza y administra la creación, el ensamblaje y la entrega de correspondencia segura, personalizada e interactiva. Le permite reunir rápidamente la correspondencia de contenido preaprobado y de creación personalizada en un proceso optimizado, desde la creación hasta el archivado. Como resultado, sus clientes obtienen una comunicación oportuna, precisa, conveniente, segura y relevante. Su empresa maximiza el valor de las interacciones con los clientes y minimiza los costos y los riesgos con un proceso optimizado para facilitar, acelerar y aumentar la productividad.

Una configuración de solución de administración de correspondencia simple incluye una instancia de autor y una instancia de publicación en el mismo equipo o en diferentes equipos

### forms manager {#forms-manager}

el administrador de formularios optimiza el proceso de actualización, administración y retirada de formularios.

### Espacio de trabajo de AEM Forms {#html-workspace}

AEM Forms Workspace se ajusta a las funciones del espacio de trabajo de Flex (obsoleto para formularios AEM en JEE) y agrega nuevas funciones para ampliar e integrar Workspace y hacerlo más sencillo de usar.

>[!NOTE]
>
>Flex Workspace está en desuso para la versión de formularios AEM.

Permite la administración de tareas en clientes sin Flash Player ni Adobe Reader. Facilita la representación de formularios HTML, además de formularios PDF y formularios Flex.

## Base de datos de formularios AEM {#aem-forms-database}

La base de datos de formularios AEM almacena contenido como artefactos de formularios, configuraciones de servicio, estado de proceso y referencias de base de datos a archivos del GDS y del directorio raíz de almacenamiento de contenido (para Content Services). Las copias de seguridad de la base de datos se pueden realizar en tiempo real sin interrupción del servicio y la recuperación puede realizarse en un punto específico en el tiempo o a un cambio concreto. En esta sección se describe cómo configurar la base de datos para que se pueda realizar una copia de seguridad en tiempo real.

En un sistema de formularios AEM configurado correctamente, el administrador del sistema y el administrador de la base de datos pueden colaborar fácilmente para recuperar el sistema a un estado coherente y conocido.

Para realizar una copia de seguridad de la base de datos en tiempo real, debe utilizar el modo de instantánea o configurar la base de datos para que se ejecute en el modo de registro especificado. Esto permite realizar copias de seguridad de los archivos de base de datos mientras la base de datos está abierta y disponible para su uso. Además, la base de datos conserva sus registros de transacciones y reversión cuando se ejecuta en estos modos.

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (obsoleto) es un sistema de administración de contenido instalado con LiveCycle. Permite a los usuarios diseñar, administrar, monitorear y optimizar procesos centrados en el ser humano. La compatibilidad con Content Services (obsoleto) finaliza el 31/12/2014. Consulte el documento [de ciclo vital del producto de](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)Adobe. Para obtener información sobre la configuración de Content Services (obsoleto), consulte [Administración de Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).

### DB2 {#db2}

Configure la base de datos de DB2 para que se ejecute en modo de registro de archivos.

>[!NOTE]
>
>Si el entorno de formularios AEM se actualizó desde una versión anterior de formularios AEM y utiliza DB2, no se admite la copia de seguridad en línea. En este caso, debe cerrar los formularios de AEM y realizar una copia de seguridad sin conexión. Las versiones futuras de los formularios AEM admitirán la copia de seguridad en línea para los clientes que realicen la actualización.

IBM cuenta con un conjunto de herramientas y sistemas de ayuda para ayudar a los administradores de bases de datos a administrar sus tareas de backup y recuperación:

* Acelerador de Log de Archiving DB2 de IBM (consulte la Guía [del Usuario del Acelerador de Log de Archiving DB2 de](https://publib.boulder.ibm.com/infocenter/dzichelp/v2r2/topic/com.ibm.db2tools.alc.doc.ug/alcugb20.pdf?noframes=true)IBM para z/OS).
* Experto en el Archiving de Datos de IBM DB2 (consulte Guía y Referencia [del Usuario Experto en Archiving de Datos de](https://publib.boulder.ibm.com/infocenter/mptoolic/v1r0/topic/com.ibm.db2tools.aeu.doc.ug/ahxugb13.pdf?noframes=true)IBM DB2).

DB2 cuenta con capacidades integradas para realizar copias de seguridad de una base de datos en Tivoli Storage Manager. Mediante el uso de Tivoli Storage Manager, las copias de seguridad de DB2 se pueden almacenar en otros medios o en el disco duro local.

Para obtener más información sobre el backup y la recuperación de bases de datos DB2, consulte [Desarrollo de una estrategia de backup y recuperación para DB2](https://publib.boulder.ibm.com/infocenter/db2luw/v9/index.jsp?topic=/com.ibm.db2.udb.admin.doc/doc/c0005945.htm).

### Oracle {#oracle}

Utilice copias de seguridad de instantáneas o configure la base de datos Oracle para que se ejecute en modo de registro de archivos. (Consulte [Oracle Backup: Introducción](https://www.databasedesign-resource.com/oracle-backup.md)). Para obtener más información sobre cómo realizar copias de seguridad y recuperar la base de datos Oracle, vaya a estas ubicaciones:

[](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) Backup y Recuperación de Oracle: Explica los conceptos de backup y recuperación y las técnicas más comunes para utilizar Recovery Manager (RMAN) para backup, recuperación e informes en forma más detallada, así como para proporcionar más información sobre cómo planificar una estrategia de backup y recuperación.

[](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) Guía del Usuario de Oracle Database Backup and Recovery: Proporciona información detallada sobre la arquitectura RMAN, los conceptos y mecanismos de backup y recuperación, las técnicas de recuperación avanzadas como las funciones de recuperación puntual y flashback de bases de datos, y el ajuste del performance de backup y recuperación. También abarca el backup y la recuperación administrados por el usuario, utilizando instalaciones del sistema operativo del host en lugar de RMAN. Este volumen es esencial para el backup y la recuperación de implementaciones de bases de datos más sofisticadas y para situaciones de recuperación avanzadas.

[](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) Referencia de Backup y Recuperación de Base de Datos Oracle: Proporciona información completa sobre sintaxis y semántica para todos los comandos RMAN, y describe las vistas de base de datos disponibles para generar informes sobre las actividades de backup y recuperación.

### SQL Server {#sql-server}

Utilice copias de seguridad instantáneas o configure la base de datos de SQL Server para que se ejecute en el modo de registro de transacciones.

SQL Server también proporciona dos herramientas de backup y recuperación:

* SQL Server Management Studio (GUI)
* T-SQL (línea de comandos)

Consulte [Estrategias](https://articles.techrepublic.com.com/5100-1035_61-1043671.md)de Backup y [Backup y Restore](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx).

### MySQL {#mysql}

Utilice MySQLAdmin o modifique los archivos INI en Windows para configurar su base de datos MySQL para que se ejecute en modo de registro binario. (Consulte Registro [binario](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html)MySQL). Una herramienta de backup en caliente para MySQL también está disponible desde el software InnoBase. (Consulte [Copia de seguridad](https://www.innodb.com/hot-backup/features.md)en caliente de Innobase).

**Nota**: *El modo de registro binario predeterminado para MySQL es &quot;Statement&quot;, que es incompatible con las tablas utilizadas por Content Services (obsoleto). El uso del inicio de sesión binario en este modo predeterminado provoca errores en Content Services (obsoleto). Si el sistema incluye Content Services (obsoleto), utilice el modo de registro &quot;Mixto&quot;.*Para habilitar el registro &quot;Mixto&quot;, agregue el siguiente argumento al archivo my.ini:
`binlog_format=mixed log-bin=logname`

Puede utilizar la utilidad mysqldump para obtener la copia de seguridad completa de la base de datos. Se requieren backups completos, pero no siempre son convenientes. Producen grandes archivos de backup y tardan tiempo en generarse. Para realizar una copia de seguridad incremental, asegúrese de iniciar el servidor con la opción - `log-bin` como se describe en la sección anterior. Cada vez que el servidor MySQL se reinicia, deja de escribir en el registro binario actual, crea uno nuevo y, a partir de entonces, el nuevo se convierte en el actual. Puede forzar un conmutador manualmente con el `FLUSH LOGS SQL` comando. Después de la primera copia de seguridad completa, las posteriores copias de seguridad incrementales se realizan utilizando la utilidad mysqladmin con el `flush-logs` comando, que crea el siguiente archivo de registro.

Consulte Resumen [de estrategia de copia de seguridad](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html).

```as3
binlog_format=mixed
log-bin=logname
```

## Directorio raíz de almacenamiento de contenido (solo Content Services) {#content-storage-root-directory-content-services-only}

El directorio raíz de almacenamiento de contenido contiene el repositorio de Content Services (obsoleto) donde se almacenan todos los documentos, artefactos e índices. Se debe realizar una copia de seguridad del árbol del directorio raíz del almacenamiento de contenido. Esta sección describe cómo determinar la ubicación del directorio raíz de almacenamiento de contenido para entornos independientes y en clúster.

### Ubicación raíz del almacenamiento de contenido (entorno independiente) {#content-storage-root-location-stand-alone-environment}

El directorio raíz del almacenamiento de contenido se crea cuando se instala Content Services (obsoleto). La ubicación del directorio raíz de almacenamiento de contenido se determina durante el proceso de instalación de formularios de AEM.

La ubicación predeterminada para el directorio raíz de almacenamiento de contenido es `[aem-forms root]/lccs_data`.

Realice una copia de seguridad de los siguientes directorios ubicados en el directorio raíz de almacenamiento de contenido:

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Si el directorio /backup-lucene-indexes no está presente, haga una copia de seguridad del directorio /lucene-indexes, también ubicado en el directorio Raíz de almacenamiento de contenido. Si el directorio /backup-lucene-indexes está presente, no realice una copia de seguridad del directorio /lucene-indexes porque puede causar errores.

### Ubicación raíz del almacenamiento de contenido (entorno en clúster) {#content-storage-root-location-clustered-environment}

Al instalar Content Services (obsoleto) en un entorno en clúster, el directorio raíz de almacenamiento de contenido se divide en dos directorios distintos:

**** Directorio raíz de almacenamiento de contenido: Normalmente, un directorio de red compartido accesible de lectura y escritura para todos los nodos del clúster

**** Directorio raíz de índice: Directorio que se crea en cada nodo del clúster, siempre con la misma ruta y nombre de directorio

La ubicación predeterminada para el directorio raíz de almacenamiento de contenido es `[GDS root]/lccs_data`, donde `[GDS root]` es la ubicación descrita en la ubicación [de](files-back-recover.md#gds-location)GDS. Realice una copia de seguridad de los siguientes directorios ubicados en el directorio raíz de almacenamiento de contenido:

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Si el directorio /backup-lucene-indexes no está presente, haga una copia de seguridad del directorio /lucene-indexes, también ubicado en el directorio Raíz de almacenamiento de contenido. Si el directorio /backup-lucene-indexes está presente, no realice una copia de seguridad del directorio /lucene-indexes porque puede causar errores.

La ubicación predeterminada para el directorio raíz de índice está `[aem-forms root]/lucene-indexes` en cada nodo.

## Fuentes instaladas por el cliente {#customer-installed-fonts}

Si ha instalado fuentes adicionales en el entorno de formularios AEM, debe realizar una copia de seguridad por separado. Realice una copia de seguridad de todos los directorios de fuentes de Adobe y del cliente que se especifican en la consola de administración en Configuración > Sistema principal > Configuraciones. Asegúrese de realizar una copia de seguridad del directorio de fuentes completo.

>[!NOTE]
>
>De forma predeterminada, las fuentes de Adobe instaladas con los formularios AEM se encuentran en el `[aem-forms root]/fonts` directorio.

Si está reinicializando el sistema operativo en el equipo host y desea utilizar fuentes del sistema operativo anterior, también se debe realizar una copia de seguridad del contenido del directorio de fuentes del sistema. (Para obtener instrucciones específicas, consulte la documentación del sistema operativo).
