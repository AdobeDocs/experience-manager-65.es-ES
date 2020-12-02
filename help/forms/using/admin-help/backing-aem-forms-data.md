---
title: Copia de seguridad de los datos de formularios AEM
seo-title: Copia de seguridad de los datos de formularios AEM
description: Este documento describe los pasos necesarios para completar una copia de seguridad en caliente o en línea de la base de datos de formularios AEM, los directorios GDS y Raíz de Almacenamiento de contenido.
seo-description: Este documento describe los pasos necesarios para completar una copia de seguridad en caliente o en línea de la base de datos de formularios AEM, los directorios GDS y Raíz de Almacenamiento de contenido.
uuid: ac7856be-e3b7-4b81-b8b9-fc909b5907b4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 52187196-b091-4683-85ae-cc7c250dee54
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---


# Copia de seguridad de los datos de formularios AEM {#backing-up-the-aem-forms-data}

En esta sección se describen los pasos necesarios para completar una copia de seguridad en caliente o en línea de la base de datos de formularios AEM, los directorios raíz de Almacenamiento de contenido y GDS.

Una vez que AEM formularios se instalan e implementan en áreas de producción, el administrador de la base de datos debe realizar una copia de seguridad inicial completa o en frío de la base de datos. La base de datos debe cerrarse para esta copia de seguridad. A continuación, las copias de seguridad diferenciales o incrementales (o en caliente) de la base de datos deben realizarse regularmente.

Para garantizar una copia de seguridad y recuperación exitosa, debe estar disponible en todo momento una copia de seguridad de imagen del sistema. Luego, si se produce una pérdida, puede recuperar todo el entorno a un estado consistente.

Realizar una copia de seguridad de la base de datos al mismo tiempo que las copias de seguridad del directorio raíz de GDS, AEM repositorio y Almacenamiento de contenido ayuda a mantener sincronizados estos sistemas si alguna vez se requiere la recuperación.

El procedimiento de copia de seguridad descrito en esta sección requiere que introduzca el modo de copia de seguridad segura antes de realizar una copia de seguridad de la base de datos de formularios AEM, AEM repositorio, GDS y los directorios raíz de Almacenamiento de contenido. Cuando se complete la copia de seguridad, debe salir del modo de copia de seguridad segura. El modo de respaldo seguro se utiliza para marcar documentos de larga duración y persistentes que residen en el GDS. Este modo garantiza que el mecanismo de limpieza de archivos automatizado (el recopilador de archivos) no elimine los archivos caducados hasta que se libere el modo de copia de seguridad segura. Es necesario mantener una copia de seguridad de GDS en sincronización con una copia de seguridad de la base de datos.

La frecuencia con la que se debe realizar una copia de seguridad de la ubicación de GDS depende de cómo se utilicen AEM formularios y de las ventanas de copia de seguridad disponibles. La ventana de backup puede verse afectada por procesos de larga duración, ya que pueden ejecutarse durante varios días. Si cambia, agrega y elimina archivos de este directorio continuamente, debe realizar una copia de seguridad de la ubicación de GDS con más frecuencia.

Si la base de datos se está ejecutando en modo de registro, como se describe en la sección anterior, también se debe realizar una copia de seguridad de los registros de la base de datos con frecuencia para que se puedan utilizar para restaurar la base de datos en caso de fallo de medios.

>[!NOTE]
>
>Los archivos a los que no se hace referencia pueden persistir en el directorio GDS después del proceso de recuperación. Esta es una limitación conocida en este momento.

## Realice una copia de seguridad de la base de datos, GDS, el repositorio de AEM y los directorios raíz del Almacenamiento de contenido {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

Debe colocar AEM formularios en el modo de copia de seguridad segura (instantánea) o en el modo de copia de seguridad móvil (cobertura continua). Antes de definir AEM formularios para introducir cualquiera de los modos de copia de seguridad, asegúrese de lo siguiente:

* Compruebe la versión del sistema y registre los parches o actualizaciones que se aplicaron desde la última copia de seguridad de la imagen del sistema completa.
* Si utiliza copias de seguridad móviles o en modo de instantánea, asegúrese de que la base de datos está configurada con la configuración de registro correcta para permitir las copias de seguridad en caliente de la base de datos. (Consulte [AEM base de datos de formularios](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

Además de esto, observe las siguientes pautas para el proceso de backup/restore.

* Realice una copia de seguridad del directorio GDS mediante un sistema operativo disponible o una utilidad de copia de seguridad de terceros. (Consulte [Ubicación de GDS](/help/forms/using/admin-help/files-back-recover.md#gds-location)).
* (Opcional) Realice una copia de seguridad del directorio raíz de Almacenamiento de contenido mediante un sistema operativo disponible o una herramienta de respaldo y de terceros. (Consulte [Ubicación raíz del Almacenamiento de contenido (entorno independiente)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) o [Ubicación raíz del Almacenamiento de contenido (entorno agrupado)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* Realizar copia de seguridad   instancias de creación y publicación (copia de seguridad de crx -repositorio).

   Para realizar una copia de seguridad del entorno de la solución de administración de correspondencia, realice los pasos en las instancias de creación y publicación como se describe en [Backup y Restore](/help/sites-administering/backup-and-restore.md).

   Tenga en cuenta los siguientes puntos al realizar una copia de seguridad de las instancias de autor y publicación:

   * Asegúrese de que la copia de seguridad de las instancias de autor y publicación se sincroniza con inicio al mismo tiempo. Aunque puede seguir utilizando instancias de autor y publicación mientras se realiza la copia de seguridad, se recomienda no publicar ningún recurso durante la copia de seguridad para evitar cambios no capturados. Espere a que la copia de seguridad de las instancias de creación y publicación finalice antes de publicar nuevos recursos.
   * La copia de seguridad completa del nodo Autor incluye copia de seguridad de los datos de Forms Manager y AEM Forms Workspace.
   * Los desarrolladores de Workbench pueden seguir trabajando en sus procesos de forma local. No deben implementar ningún proceso nuevo durante la fase de backup.
   * La decisión sobre la duración de cada sesión de copia de seguridad (para el modo de copia de seguridad móvil) debe basarse en el tiempo total que se tarda en realizar una copia de seguridad de todos los datos en formularios AEM (DB, GDS, repositorio AEM y cualquier otro dato personalizado adicional).

Debe realizar una copia de seguridad de la base de datos de formularios AEM, incluidos los registros de transacciones. (Consulte [AEM base de datos de formularios](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Para obtener más información, consulte el artículo correspondiente de la base de datos:

* [Backup y recuperación de oracle para formularios AEM](https://www.adobe.com/go/kb403624)
* [Respaldo y recuperación de MySQL para formularios AEM](https://www.adobe.com/go/kb403625)
* [Copias de seguridad y recuperación de Microsoft SQL Server para formularios AEM](https://www.adobe.com/go/kb403623)
* [Backup y recuperación de DB2 para formularios AEM](https://www.adobe.com/go/kb403626)

Estos artículos proporcionan orientación sobre las funciones básicas de la base de datos para el backup y la recuperación de datos. No están pensadas como guías técnicas integradoras de la función de backup y recuperación de bases de datos de un proveedor específico. Describen comandos que son necesarios para crear una estrategia de copia de seguridad de base de datos confiable para los datos de la aplicación de formularios AEM.

>[!NOTE]
>
>La copia de seguridad de la base de datos debe estar completa antes de comenzar a realizar la copia de seguridad del GDS. Si no se completa la copia de seguridad de la base de datos, los datos no estarán sincronizados.

### Introducción de los modos de backup {#entering-the-backup-modes}

Puede utilizar la consola de administración, el comando LCBackupMode o la API disponible con la instalación de formularios AEM para entrar y salir de los modos de copia de seguridad. Tenga en cuenta que para el respaldo móvil (cobertura continua), la opción de la consola de administración no está disponible; debe utilizar la opción de línea de comandos o la API. <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>Si ha configurado SSL en el servidor de formularios, no podrá colocar el servidor de formularios en modo de copia de seguridad mediante la secuencia de comandos LCBackupMode.CMD.

**Uso de la consola de administración para acceder al modo de copia de seguridad segura**

1. Inicie sesión en la consola de administración.
1. Haga clic en Configuración > Configuración del sistema principal > Utilidades de copia de seguridad.
1. Seleccione Operar en modo de copia de seguridad segura y haga clic en Aceptar.

   Este método coloca AEM formularios en modo de copia de seguridad indefinidamente (sin tiempo de espera) y entra en modo de instantánea en lugar de en modo de copia de seguridad móvil.

**Uso de la opción de línea de comandos para entrar en el modo de copia de seguridad segura**

Puede utilizar las secuencias de comandos `LCBackupMode` de la interfaz de la línea de comandos para colocar AEM formularios en modo de copia de seguridad seguro.

1. Establezca ADOBE_LIVECYCLE y inicio en el servidor de aplicaciones.
1. Vaya a la carpeta `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline`.
1. Según el sistema operativo, edite la secuencia de comandos `LCBackupMode.cmd` o `LCBackupMode.sh` para proporcionar valores predeterminados que sean adecuados para el sistema.
1. En el símbolo del sistema, ejecute el siguiente comando en una sola línea:

   * (Windows) `LCBackupMode.cmd enter [-Host=`*nombre de host* `] [-port=`*número de puerto* `] [-user=`*nombre de usuario* `] [-password=`*contraseña* `] [-label=`*nombre de etiqueta* `] [-timeout=`*segundos* `]`
   * (Linux, UNIX) `LCBackupMode.sh enter [-host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `] [-label=`*labelname* &lt;a 10/>`]`

   En los comandos anteriores, los marcadores de posición se definen de la siguiente manera:

   `Host` es el nombre del host en el que se ejecutan AEM formularios.

   `port` es el puerto de WebServices del servidor de aplicaciones en el que se ejecutan AEM formularios.

   `user` es el nombre de usuario del administrador de formularios AEM.

   `password` es la contraseña del administrador de formularios AEM.

   `label` es la etiqueta de texto, que puede ser cualquier cadena, para esta copia de seguridad.

   `timeout` es el número de segundos después de los cuales se deja automáticamente el modo de copia de seguridad. Puede ser de 0 a 10.080. Si es 0, que es el valor predeterminado, el modo de copia de seguridad nunca se agota el tiempo de espera.

   Para obtener más información sobre la interfaz de la línea de comandos al modo de copia de seguridad, consulte el archivo Léame en el directorio BackupRestoreCommand.

### Abandonar modos de backup {#leaving-backup-modes}

Puede utilizar la consola de administración o la opción de línea de comandos para dejar los modos de copia de seguridad.

**Salir del modo de copia de seguridad segura (modo de instantánea)**

Para utilizar la Consola de administración para quitar AEM formularios del modo de copia de seguridad segura (modo de instantánea), realice las siguientes tareas.

1. Inicie sesión en la Consola de administración.
1. Haga clic en Configuración > Configuración del sistema principal > Utilidades de copia de seguridad.
1. Anule la selección de Operar en modo de copia de seguridad segura y haga clic en Aceptar.

**Deje todos los modos de copia de seguridad**

Puede utilizar la interfaz de la línea de comandos para quitar AEM formularios del modo de copia de seguridad segura (modo de instantánea) o para finalizar la sesión actual del modo de copia de seguridad (modo móvil). Tenga en cuenta que no puede utilizar la consola de administración para salir del modo de copia de seguridad móvil. En el modo de copia de seguridad móvil, los controles Utilidades de copia de seguridad de la Consola de administración están desactivados. Debe utilizar la llamada de API o el comando LCBackupMode.

1. Vaya a la carpeta `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline`.
1. Según el sistema operativo, edite la secuencia de comandos `LCBackupMode.cmd` o `LCBackupMode.sh` para proporcionar valores predeterminados que sean adecuados para el sistema.

   >[!NOTE]
   >
   >Debe configurar el directorio JAVA_HOME como se describe en el capítulo correspondiente para el servidor de aplicaciones en [Preparación de la instalación de AEM formularios](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*.*

1. Ejecute el siguiente comando en una sola línea:

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `]`
   * (Linux, UNIX) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `]`

      En los comandos anteriores, los marcadores de posición se definen de la siguiente manera:

      `Host` es el nombre del host en el que se ejecutan AEM formularios.

      `port` es el puerto en el que se ejecutan AEM formularios en el servidor de aplicaciones.

      `user` es el nombre de usuario del administrador de formularios AEM.

      `password` es la contraseña del administrador de formularios AEM.

      `leaveContinuousCoverage` Utilice esta opción para desactivar completamente el modo de copia de seguridad móvil.
   >[!NOTE]
   >
   >Durante el tiempo en que el modo de copia de seguridad está desactivado, no se puede restablecer la cobertura continua. No se protegen los cambios que se produzcan durante ese tiempo.

   >[!NOTE]
   >
   >Si ha activado el almacenamiento de documento en la base de datos, no se aplican el modo de copia de seguridad instantánea ni los modos de copia de seguridad móvil.

   Para obtener más información sobre la interfaz de la línea de comandos al modo de copia de seguridad, consulte el archivo léame en el directorio BackupRestoreCommand.

