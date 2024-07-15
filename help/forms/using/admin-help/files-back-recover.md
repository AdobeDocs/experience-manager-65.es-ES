---
title: Archivos para realizar copias de seguridad y recuperar
description: Este documento describe la aplicación y los archivos de datos de los que se debe realizar una copia de seguridad.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d2dd381d-a7d2-4fec-a8ba-7ca037fd9dc1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '2017'
ht-degree: 3%

---

# Archivos para realizar copias de seguridad y recuperar {#files-to-back-up-and-recover}

La aplicación y los archivos de datos de los que se debe realizar una copia de seguridad se describen con más detalle en las secciones siguientes.

Tenga en cuenta los siguientes puntos con respecto a la copia de seguridad y la recuperación:

* AEM Se debe hacer una copia de seguridad de la base de datos antes de GDS y repositorio de.
* Si necesita reducir los nodos en un entorno agrupado en clúster para realizar una copia de seguridad, asegúrese de que los nodos secundarios se cierran antes que el nodo principal. De lo contrario, puede provocar incoherencia en el clúster o en el servidor. Además, el nodo principal debe activarse antes que cualquier nodo secundario.
* Para la operación de restauración de un clúster, el servidor de aplicaciones debe detenerse para cada nodo del clúster.

## Directorio global de almacenamiento de documentos {#global-document-storage-directory}

El GDS es un directorio que se utiliza para almacenar archivos de larga duración que se utilizan dentro de un proceso. AEM La duración de los archivos de larga duración está pensada para abarcar uno o más inicios de un sistema de formularios de la serie de formularios, y puede abarcar días e incluso años. Estos archivos de larga duración pueden incluir PDF, directivas y plantillas de formulario. AEM Los archivos de larga duración son una parte esencial del estado general de muchas implementaciones de formularios en la forma de un formulario en el que se puede ejecutar un proceso de trabajo. Si se pierden o dañan algunos o todos los documentos de larga duración, el servidor de Forms puede volverse inestable.

Los documentos de entrada para la invocación asincrónica de trabajos también se almacenan en el GDS y deben estar disponibles para procesar solicitudes. Por lo tanto, es importante que tenga en cuenta la fiabilidad del sistema de archivos que aloja el GDS y que emplee una matriz redundante de discos independientes (RAID) u otra tecnología adecuada para sus requisitos de calidad y nivel de servicio.

AEM La ubicación del GDS se determina durante el proceso de instalación de los formularios de la o más tarde mediante la consola de administración. Además de mantener una ubicación de alta disponibilidad para GDS, también puede habilitar el almacenamiento de documentos en la base de datos. Ver [Opciones de copia de seguridad cuando se usa la base de datos para el almacenamiento de documentos](files-back-recover.md#backup-options-when-database-is-used-for-document-storage).

### Ubicación de GDS {#gds-location}

Si deja vacía la configuración de ubicación durante la instalación, la ubicación predeterminada es un directorio en la instalación del servidor de aplicaciones. Haga una copia de seguridad del siguiente directorio para su servidor de aplicaciones:

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

Si ha cambiado la ubicación de GDS a una ubicación no predeterminada, puede determinarla de la siguiente manera:

* Inicie sesión en la consola de administración y haga clic en Configuración > Configuración del sistema principal > Configuraciones.
* Registre la ubicación especificada en el cuadro Directorio global de almacenamiento de documentos.

En un entorno agrupado, el GDS normalmente señala a un directorio compartido en la red y es de lectura y escritura accesible para cada nodo de clúster.

La ubicación del GDS puede cambiarse durante una recuperación si la ubicación original ya no está disponible. (Consulte [Cambio de la ubicación de GDS durante la recuperación](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).)

### Opciones de copia de seguridad cuando se utiliza la base de datos para el almacenamiento de documentos {#backup-options-when-database-is-used-for-document-storage}

AEM AEM Puede habilitar el almacenamiento de documentos de formularios en la base de datos de formularios en la que se utiliza la consola de administración. AEM AEM Aunque esta opción mantiene todos los documentos persistentes en la base de datos, los formularios de la aplicación aún requieren el directorio GDS basado en el sistema de archivos porque se utiliza para almacenar archivos y recursos permanentes y temporales relacionados con las sesiones e invocaciones de formularios de la aplicación de formularios de la.

AEM Al seleccionar la opción &quot;Habilitar el almacenamiento de documentos en la base de datos&quot; en la Configuración del sistema principal de la consola de administración o al utilizar el Administrador de configuración, los formularios no permiten el modo de copia de seguridad de instantáneas ni el modo de copia de seguridad móvil. AEM Por lo tanto, no es necesario administrar los modos de copia de seguridad mediante los formularios de. Si utiliza esta opción, debe realizar una copia de seguridad del GDS solo una vez después de habilitar la opción. AEM Al recuperar formularios de la copia de seguridad, no es necesario cambiar el nombre del directorio de la copia de seguridad para el GDS o restaurar el GDS.

## Repositorio de AEM {#aem-repository}

AEM AEM El repositorio de crx (crx-repository) se crea si el repositorio crx está configurado al instalar formularios de la. AEM La ubicación del directorio crx-repository se determina durante el proceso de instalación de los formularios de la. AEM AEM AEM Es necesario realizar una copia de seguridad y una restauración del repositorio de datos junto con la base de datos y el GDS para obtener datos de formularios en forma de coherentes. AEM El repositorio de contiene datos para la solución de Administración de correspondencia, Forms Manager y AEM Forms Workspace.

### Solución de Administración de correspondencia {#correspondence-management-solution}

Administración de correspondencia centraliza y administra la creación, la combinación y la entrega de correspondencia segura, personalizada e interactiva. Le permite combinar rápidamente la correspondencia de contenido preaprobado y creado a medida en un proceso optimizado, desde la creación hasta el archivado. Como resultado, sus clientes recibirán una comunicación oportuna, precisa, conveniente, segura y relevante. Su empresa maximiza el valor de las interacciones con los clientes y minimiza los costes y los riesgos con un proceso optimizado para facilitar, acelerar y aumentar la productividad.

Una configuración sencilla de la solución de Administración de correspondencia incluye una instancia de autor y una instancia de publicación en el mismo equipo o en equipos diferentes

### administrador de formularios {#forms-manager}

forms manager optimiza el proceso de actualización, administración y retirada de formularios.

### AEM Forms Workspace {#html-workspace}

AEM Forms Workspace AEM coincide con las capacidades del Workspace de Flex (obsoleto para formularios de en JEE) y agrega nuevas funciones para ampliar e integrar Workspace y hacerlo más fácil de usar.

>[!NOTE]
>
>Flex AEM Workspace está en desuso para la versión de formularios en la que se ha realizado un.

Permite la administración de tareas en clientes sin Flash Player ni Adobe Reader. Facilita la representación de HTML Forms, además de PDF forms y formularios Flex.

## AEM base de datos de formularios {#aem-forms-database}

AEM La base de datos de formularios almacena contenido, como artefactos de formulario, configuraciones de servicio, estados de proceso y referencias de base de datos a archivos en el GDS y en el directorio raíz de almacenamiento de contenido (para Content Services). Las copias de seguridad de la base de datos se pueden realizar en tiempo real sin interrupciones en el servicio y la recuperación se puede realizar en un momento específico o en un cambio concreto. En esta sección se describe cómo configurar la base de datos para que se pueda realizar una copia de seguridad de la misma en tiempo real.

AEM En un sistema de formularios correctamente configurado, el administrador del sistema y el administrador de la base de datos pueden colaborar fácilmente para recuperar el sistema a un estado coherente y conocido.

Para realizar una copia de seguridad de la base de datos en tiempo real, debe utilizar el modo de instantánea o configurar la base de datos para que se ejecute en el modo de registro especificado. Esto permite hacer una copia de seguridad de los archivos de la base de datos mientras ésta está abierta y disponible para su uso. Además, la base de datos conserva sus registros de reversión y transacciones cuando se ejecuta en estos modos.

>[!NOTE]
>
>Adobe LiveCycle® ® Content Services ES (obsoleto) es un sistema de administración de contenido instalado con LiveCycle. Permite a los usuarios diseñar, administrar, supervisar y optimizar procesos centrados en las personas. La compatibilidad con los servicios de contenido (obsoleto) finaliza el 31/12/2014. Ver [documento de ciclo de vida del producto de Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

### DB2 {#db2}

Configure la base de datos DB2 para que se ejecute en el modo de registro de archivo.

>[!NOTE]
>
>AEM AEM Si el entorno de formularios en la que se ha realizado la actualización se ha realizado desde una versión anterior de formularios en la que se utiliza DB2, no se admite la copia de seguridad en línea. AEM En este caso, debe cerrar los formularios de la y realizar una copia de seguridad sin conexión. AEM Las versiones futuras de los formularios de la admitirán el backup en línea para los clientes de actualización.

IBM tiene un conjunto de herramientas y sistemas de ayuda para ayudar a los administradores de bases de datos a administrar sus tareas de copia de seguridad y recuperación:

* Acelerador de registros de archivo de IBM DB2
* Experto en archivos de datos de IBM DB2

DB2 tiene funcionalidades integradas para realizar copias de seguridad de una base de datos en Tivoli Storage Manager. Mediante Tivoli Storage Manager, las copias de seguridad DB2 se pueden almacenar en otros soportes o en el disco duro local.

### Oracle {#oracle}

Utilice las copias de seguridad instantáneas o configure la base de datos de Oracle para que se ejecute en el modo de registro de archivos. (Consulte Copia De Seguridad De [Oracle: Introducción](https://www.databasedesign-resource.com/oracle-backup.md).) Para obtener más información sobre la copia de seguridad y recuperación de la base de datos de Oracle, visite estos sitios:

[Copia de seguridad y recuperación en Oracle:](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) Explica los conceptos de copia de seguridad y recuperación, así como las técnicas más comunes para usar Recovery Manager (RMAN) para realizar copias de seguridad, recuperar y generar informes con más detalle, y proporciona más información acerca de cómo planear una copia de seguridad y una estrategia de recuperación.

[Guía del usuario de backup y recuperación de la base de datos de Oracle:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) Proporciona información detallada sobre la arquitectura de RMAN, los conceptos y mecanismos de backup y recuperación, las técnicas avanzadas de recuperación, como las funciones de flashback de la base de datos y de recuperación puntual, y la optimización del rendimiento de backup y recuperación. También cubre la copia de seguridad y recuperación gestionadas por el usuario, utilizando instalaciones del sistema operativo del host en lugar de RMAN. Este volumen es esencial para la copia de seguridad y recuperación de implementaciones de bases de datos más sofisticadas y para escenarios de recuperación avanzados.

[Referencia de copia de seguridad y recuperación de la base de datos de Oracle:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) Proporciona información completa acerca de la sintaxis y la semántica de todos los comandos de RMAN, y describe las vistas de la base de datos disponibles para la creación de informes sobre las actividades de copia de seguridad y recuperación.

### SQL Server {#sql-server}

Utilice las copias de seguridad instantáneas o configure la base de datos de SQL Server para que se ejecute en el modo de registro de transacciones.

SQL Server también proporciona dos herramientas de copia de seguridad y recuperación:

* SQL Server Management Studio (GUI)
* T-SQL (línea de comandos)

Para obtener más información, consulte [Copia de seguridad y restauración](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx).

### MySQL {#mysql}

Utilice MySQLAdmin o modifique los archivos INI en Windows para configurar la base de datos MySQL para que se ejecute en modo de registro binario. (Consulte [Registro binario de MySQL](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html).) Una herramienta de copia de seguridad en caliente para MySQL también está disponible en el software InnoBase. (Consulte [Copia de seguridad en caliente de Innobase](https://www.innodb.com/hot-backup/features.md).)

>[!NOTE]
>
>El modo de registro binario predeterminado para MySQL es &quot;Statement&quot;, que es incompatible con tablas utilizadas por Content Services (obsoleto). El uso del registro binario en este modo predeterminado provoca que Content Services (Obsoleto) falle. Si su sistema incluye Content Services (obsoleto), utilice el modo de registro &quot;Mixto&quot;. Para habilitar el registro &quot;Mixto&quot;, agregue el siguiente argumento al archivo my.ini: `binlog_format=mixed log-bin=logname`

Puede utilizar la utilidad mysqldump para obtener la copia de seguridad completa de la base de datos. Se requieren copias de seguridad completas, pero no siempre son convenientes. Producen archivos de copia de seguridad grandes y tardan tiempo en generarse. Para realizar una copia de seguridad incremental, asegúrese de iniciar el servidor con la opción - `log-bin`, tal como se describe en la sección anterior. Cada vez que el servidor MySQL se reinicia, deja de escribir en el registro binario actual, crea uno nuevo y, a partir de entonces, el nuevo se convierte en el actual. Puede forzar un cambio manualmente con el comando `FLUSH LOGS SQL`. Después de la primera copia de seguridad completa, las copias de seguridad incrementales posteriores se realizan mediante la utilidad mysqladmin con el comando `flush-logs`, que crea el siguiente archivo de registro.

Ver [Resumen de estrategia de copia de seguridad](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html).

```text
binlog_format=mixed
log-bin=logname
```

## Directorio raíz de almacenamiento de contenido (solo servicios de contenido) {#content-storage-root-directory-content-services-only}

El directorio raíz del almacenamiento de contenido contiene el repositorio de Content Services (obsoleto) donde se almacenan todos los documentos, artefactos e índices. Se debe realizar una copia de seguridad del árbol del directorio raíz de almacenamiento de contenido. En esta sección se describe cómo determinar la ubicación del directorio raíz de almacenamiento de contenido para los entornos independientes y en clúster.

### Ubicación raíz del almacenamiento de contenido (entorno independiente) {#content-storage-root-location-stand-alone-environment}

El directorio raíz de almacenamiento de contenido se crea cuando se instala Content Services (obsoleto). AEM La ubicación del directorio raíz del almacenamiento de contenido se determina durante el proceso de instalación de los formularios de la.

La ubicación predeterminada del directorio raíz de almacenamiento de contenido es `[aem-forms root]/lccs_data`.

Haga una copia de seguridad de los siguientes directorios en el directorio raíz de almacenamiento de contenido:

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Si el directorio /backup-lucene-indexes no está presente, haga una copia de seguridad del directorio /lucene-indexes, también en el directorio raíz del almacenamiento de contenido. Si el directorio /backup-lucene-indexes está presente, no realice una copia de seguridad del directorio /lucene-indexes porque podría provocar errores.

### Ubicación raíz del almacenamiento de contenido (entorno en clúster) {#content-storage-root-location-clustered-environment}

Al instalar Content Services (obsoleto) en un entorno agrupado, el directorio raíz del almacenamiento de contenido se divide en dos directorios independientes:

**Directorio raíz de almacenamiento de contenido:** Normalmente, un directorio de red compartido que es de lectura y escritura accesible para todos los nodos del clúster

**Directorio raíz de índice:** Un directorio que se crea en cada nodo del clúster, siempre con la misma ruta de acceso y el mismo nombre de directorio

La ubicación predeterminada del directorio raíz de almacenamiento de contenido es `[GDS root]/lccs_data`, donde `[GDS root]` es la ubicación descrita en [ubicación GDS](files-back-recover.md#gds-location). Haga una copia de seguridad de los siguientes directorios en el directorio raíz de almacenamiento de contenido:

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Si el directorio /backup-lucene-indexes no está presente, haga una copia de seguridad del directorio /lucene-indexes, también en el directorio raíz del almacenamiento de contenido. Si el directorio /backup-lucene-indexes está presente, no realice una copia de seguridad del directorio /lucene-indexes porque podría provocar errores.

La ubicación predeterminada del directorio raíz del índice es `[aem-forms root]/lucene-indexes` en cada nodo.

## Fuentes instaladas por el cliente {#customer-installed-fonts}

AEM Si ha instalado fuentes adicionales en el entorno de formularios de la, debe hacer una copia de seguridad de ellas por separado. Haga una copia de seguridad de todos los directorios de fuentes de Adobe y cliente especificados en la consola de administración en Configuración > Sistema principal > Configuraciones. Asegúrese de hacer una copia de seguridad de todo el directorio de fuentes.

>[!NOTE]
>
>De forma predeterminada, las fuentes de Adobe AEM instaladas con los formularios de la aplicación se encuentran en el directorio `[aem-forms root]/fonts`.

Si está reinicializando el sistema operativo en el equipo host y desea utilizar fuentes del sistema operativo anterior, también se debe realizar una copia de seguridad del contenido del directorio de fuentes del sistema. (Para obtener instrucciones específicas, consulte la documentación del sistema operativo).
