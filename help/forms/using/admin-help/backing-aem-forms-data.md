---
title: Copia de seguridad de los datos de AEM formularios
seo-title: Backing up the AEM forms data
description: En este documento se describen los pasos necesarios para completar una copia de seguridad en línea o en caliente de la base de datos de formularios AEM, los directorios raíz de GDS y de almacenamiento de contenido.
seo-description: This document describes the steps that are required to complete a hot, or online, backup of the AEM forms database, the GDS, and Content Storage Root directories.
uuid: ac7856be-e3b7-4b81-b8b9-fc909b5907b4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 52187196-b091-4683-85ae-cc7c250dee54
exl-id: 536615a4-ab42-4b72-83b1-fad110b011ee
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 0%

---

# Copia de seguridad de los datos de AEM formularios {#backing-up-the-aem-forms-data}

En esta sección se describen los pasos necesarios para completar una copia de seguridad en línea o en caliente de la base de datos de formularios AEM, los directorios raíz de GDS y de almacenamiento de contenido.

Una vez instalados e implementados AEM formularios en las áreas de producción, el administrador de la base de datos debe realizar una copia de seguridad inicial completa o en frío de la base de datos. La base de datos debe cerrarse para esta copia de seguridad. A continuación, las copias de seguridad diferenciales o incrementales (o en caliente) de la base de datos deben realizarse regularmente.

Para garantizar una copia de seguridad y recuperación exitosa, debe estar disponible una copia de seguridad de imagen del sistema en todo momento. A continuación, si se produce una pérdida, puede recuperar todo el entorno a un estado coherente.

La copia de seguridad de la base de datos al mismo tiempo que los backups de GDS, AEM repositorio y el directorio raíz de almacenamiento de contenido ayuda a mantener estos sistemas sincronizados si alguna vez se requiere recuperación.

El procedimiento de copia de seguridad descrito en esta sección requiere que introduzca el modo de copia de seguridad segura antes de realizar la copia de seguridad de la base de datos de formularios AEM, AEM repositorio, GDS y los directorios raíz de almacenamiento de contenido. Cuando se completa la copia de seguridad, debe salir del modo de copia de seguridad segura. El modo de copia de seguridad segura se utiliza para marcar los documentos persistentes y de larga duración que residen en el GDS. Este modo garantiza que el mecanismo automatizado de limpieza de archivos (el recolector de archivos) no elimine los archivos caducados hasta que se libere el modo seguro de copia de seguridad. Es necesario mantener una copia de seguridad de GDS en sincronización con una copia de seguridad de la base de datos.

La frecuencia con la que se debe realizar una copia de seguridad de la ubicación de GDS depende de cómo se utilicen AEM formularios y de las ventanas de copia de seguridad disponibles. La ventana de copia de seguridad puede verse afectada por procesos de larga duración porque pueden ejecutarse durante varios días. Si cambia, agrega y elimina archivos continuamente en este directorio, debería realizar una copia de seguridad de la ubicación GDS con más frecuencia.

Si la base de datos se está ejecutando en modo de registro, como se describe en la sección anterior, también se debe realizar una copia de seguridad de los registros de la base de datos con frecuencia para que se puedan utilizar para restaurar la base de datos en caso de que se produzca un error en el contenido.

>[!NOTE]
>
>Los archivos a los que no se hace referencia pueden persistir en el directorio GDS después del proceso de recuperación. Esta es una limitación conocida en este momento.

## Haga una copia de seguridad de la base de datos, GDS, AEM repositorio y los directorios raíz de almacenamiento de contenido {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

Debe colocar AEM formularios en el modo de copia de seguridad segura (instantánea) o en el modo de copia de seguridad móvil (cobertura continua). Antes de configurar AEM formularios para que introduzcan cualquiera de los modos de copia de seguridad, asegúrese de lo siguiente:

* Compruebe la versión del sistema y registre los parches o actualizaciones que se aplicaron desde que se realizó la última copia de seguridad completa de la imagen del sistema.
* Si utiliza copias de seguridad móviles o en modo de instantánea, asegúrese de que la base de datos esté configurada con la configuración de registro correcta para permitir copias de seguridad en caliente de la base de datos. (Consulte [base de datos de AEM forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

Además de esto, observe las siguientes pautas para el proceso de backup/restore.

* Haga una copia de seguridad del directorio GDS utilizando un sistema operativo disponible o una utilidad de copia de seguridad de terceros. (Consulte [Ubicación de GDS](/help/forms/using/admin-help/files-back-recover.md#gds-location).)
* (Opcional) Haga una copia de seguridad del directorio raíz del almacenamiento de contenido utilizando un sistema operativo disponible o una utilidad de copia de seguridad y de terceros. (Consulte [Ubicación raíz del almacenamiento de contenido (entorno independiente)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) o [Ubicación raíz del almacenamiento de contenido (entorno agrupado)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* Haga una copia de seguridad de las instancias de autor y publicación (copia de seguridad del repositorio crx).

   Para realizar una copia de seguridad del entorno de la solución de administración de correspondencia, realice los pasos en las instancias de autor y publicación tal como se describe en [Copia de seguridad y restauración](/help/sites-administering/backup-and-restore.md).

   Tenga en cuenta los siguientes puntos al realizar una copia de seguridad de las instancias de autor y publicación:

   * Asegúrese de que la copia de seguridad de las instancias de autor y publicación esté sincronizada para que se inicie al mismo tiempo. Aunque puede seguir utilizando instancias de autor y publicación mientras se realiza la copia de seguridad, se recomienda no publicar ningún recurso durante la copia de seguridad para evitar cualquier cambio no capturado. Espere a que finalice la copia de seguridad de las instancias de autor y publicación antes de publicar nuevos recursos.
   * La copia de seguridad completa del nodo Autor incluye una copia de seguridad de los datos de Forms Manager y AEM Forms Workspace.
   * Los desarrolladores de Workbench pueden seguir trabajando en sus procesos localmente. No deben implementar ningún proceso nuevo durante la fase de backup.
   * La decisión sobre la duración de cada sesión de copia de seguridad (para el modo de copia de seguridad móvil) debe basarse en el tiempo total que se tarda en realizar una copia de seguridad de todos los datos de AEM formularios (DB, GDS, repositorio AEM y cualquier otro dato personalizado adicional).

Debe realizar una copia de seguridad de la base de datos de formularios AEM, incluidos los registros de transacciones. (Consulte [base de datos de AEM forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Para obtener más información, consulte el artículo correspondiente de la base de conocimientos de la base de datos:

* [Copia de seguridad y recuperación de oracle para formularios AEM](https://www.adobe.com/go/kb403624)
* [Copia de seguridad y recuperación de MySQL para formularios AEM](https://www.adobe.com/go/kb403625)
* [Copia de seguridad y recuperación de Microsoft SQL Server para formularios AEM](https://www.adobe.com/go/kb403623)
* [Copia de seguridad y recuperación de DB2 para formularios AEM](https://www.adobe.com/go/kb403626)

Estos artículos proporcionan directrices para las funciones básicas de la base de datos para el backup y la recuperación de datos. No están pensadas como guías técnicas integradoras de la función específica de backup y recuperación de la base de datos de un proveedor. Describen los comandos necesarios para crear una estrategia de copia de seguridad de base de datos fiable para los datos de aplicaciones de formularios AEM.

>[!NOTE]
>
>La copia de seguridad de la base de datos debe completarse antes de comenzar a realizar la copia de seguridad del GDS. Si no se completa la copia de seguridad de la base de datos, los datos no estarán sincronizados.

### Introducción de los modos de copia de seguridad {#entering-the-backup-modes}

Puede utilizar la consola de administración, el comando LCBackupMode o la API disponible con la instalación de formularios AEM para entrar y salir de los modos de copia de seguridad. Tenga en cuenta que para la copia de seguridad móvil (cobertura continua), la opción de la consola de administración no está disponible; debe utilizar la opción de línea de comandos o la API . <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>Si ha configurado SSL en el servidor de formularios, no puede colocar el servidor de formularios en modo de copia de seguridad mediante la secuencia de comandos LCBackupMode.CMD.

**Uso de la consola de administración para entrar en el modo de copia de seguridad segura**

1. Inicie sesión en la consola de administración.
1. Haga clic en Configuración > Configuración del sistema principal > Utilidades de copia de seguridad.
1. Seleccione Operar en modo de copia de seguridad segura y haga clic en Aceptar.

   Este método coloca AEM formularios en modo de copia de seguridad indefinidamente (sin tiempo de espera) y accede al modo de instantánea en lugar del modo de copia de seguridad móvil.

**Uso de la opción de línea de comandos para entrar al modo de copia de seguridad segura**

Puede utilizar la interfaz de la línea de comandos `LCBackupMode` secuencias de comandos para colocar AEM formularios en modo de copia de seguridad segura.

1. Establezca ADOBE_LIVECYCLE e inicie el servidor de aplicaciones.
1. Vaya a la `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` carpeta.
1. Según el sistema operativo, edite la variable `LCBackupMode.cmd` o `LCBackupMode.sh` para proporcionar valores predeterminados adecuados para su sistema.
1. En el símbolo del sistema, ejecute el siguiente comando en una sola línea:

   * (Windows) `LCBackupMode.cmd enter [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `] [-label=`*labelname* `] [-timeout=`*seconds* `]`
   * (Linux, UNIX) `LCBackupMode.sh enter [-host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `] [-label=`*labelname* `]`

   En los comandos anteriores, los marcadores de posición se definen de la siguiente manera:

   `Host` es el nombre del host en el que se ejecutan AEM formularios.

   `port` es el puerto WebServices del servidor de aplicaciones en el que se ejecutan AEM formularios.

   `user` es el nombre de usuario del administrador de AEM formularios.

   `password` es la contraseña del administrador de AEM formularios.

   `label` es la etiqueta de texto, que puede ser cualquier cadena, para esta copia de seguridad.

   `timeout` es el número de segundos después de los cuales se deja automáticamente el modo de copia de seguridad. Puede ser de 0 a 10.080. Si es 0, que es el valor predeterminado, el modo de copia de seguridad nunca se agota.

   Para obtener más información acerca de la interfaz de la línea de comandos al modo de copia de seguridad, vea el archivo Léame en el directorio BackupRestoreCommand.

### Abandono de los modos de copia de seguridad {#leaving-backup-modes}

Puede utilizar la consola de administración o la opción de línea de comandos para dejar los modos de copia de seguridad.

**Deje el modo de copia de seguridad segura (modo de instantánea)**

Para utilizar la Consola de administración para sacar AEM formularios del modo de copia de seguridad segura (modo de instantánea), realice las siguientes tareas.

1. Inicie sesión en la Consola de administración.
1. Haga clic en Configuración > Configuración del sistema principal > Utilidades de copia de seguridad.
1. Desmarque Operar en modo de copia de seguridad segura y haga clic en Aceptar.

**Deje todos los modos de copia de seguridad**

Puede utilizar la interfaz de la línea de comandos para quitar AEM formularios del modo de copia de seguridad segura (modo de instantánea) o para finalizar la sesión actual del modo de copia de seguridad (modo móvil). Tenga en cuenta que no puede utilizar la consola de administración para salir del modo de copia de seguridad móvil. En el modo de copia de seguridad móvil, los controles de las Utilidades de copia de seguridad de la Consola de administración están desactivados. Debe utilizar una llamada API o utilizar el comando LCBackupMode.

1. Vaya a la `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` carpeta.
1. Según el sistema operativo, edite la variable `LCBackupMode.cmd` o `LCBackupMode.sh` para proporcionar valores predeterminados adecuados para su sistema.

   >[!NOTE]
   >
   >Debe configurar el directorio JAVA_HOME como se describe en el capítulo correspondiente para su servidor de aplicaciones en [Preparación para la instalación de AEM formularios](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*.*

1. Ejecute el siguiente comando en una sola línea:

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `]`
   * (Linux, UNIX) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `]`

      En los comandos anteriores, los marcadores de posición se definen de la siguiente manera:

      `Host` es el nombre del host en el que se ejecutan AEM formularios.

      `port` es el puerto en el que se ejecutan AEM formularios en el servidor de aplicaciones.

      `user` es el nombre de usuario del administrador de AEM formularios.

      `password` es la contraseña del administrador de AEM formularios.

      `leaveContinuousCoverage` Utilice esta opción para desactivar completamente el modo de copia de seguridad móvil.
   >[!NOTE]
   >
   >Durante el tiempo en que el modo de copia de seguridad está desactivado, no se puede restablecer la cobertura continua. No se protegen los cambios que se produzcan durante ese tiempo.

   >[!NOTE]
   >
   >Si ha habilitado el almacenamiento de documentos en la base de datos, el modo de copia de seguridad instantánea y los modos de copia de seguridad móvil no son aplicables.

   Para obtener más información acerca de la interfaz de la línea de comandos al modo de copia de seguridad, vea el archivo Léame en el directorio BackupRestoreCommand.
