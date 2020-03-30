---
title: Recuperación de los datos de formularios de AEM
seo-title: Recuperación de los datos de formularios de AEM
description: En este documento se describen los pasos necesarios para recuperar los datos de formularios de AEM.
seo-description: En este documento se describen los pasos necesarios para recuperar los datos de formularios de AEM.
uuid: b5735196-5a8d-4358-884f-e9b8d8f4f682
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e093114-219b-4018-9530-9002eb665448
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Recuperación de los datos de formularios de AEM {#recovering-the-aem-forms-data}

En esta sección se describen los pasos necesarios para recuperar los datos de formularios de AEM. Consulte también consideraciones [especiales para backup y recuperación](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>Los directorios raíz de la base de datos, GDS, AEM y Almacenamiento de contenido deben restaurarse en un equipo con el mismo nombre DNS que el original.

Los formularios AEM deben recuperarse de forma fiable de los siguientes errores:

**Error de disco:** Se necesita el medio de copia de seguridad más reciente para recuperar el contenido de la base de datos.

**Corrupción de datos:** Los sistemas de archivos no registran transacciones pasadas y es posible que los sistemas sobrescriban accidentalmente los datos de proceso requeridos.

**Error del usuario:** La recuperación se limita a los datos que la base de datos pone a disposición. Si los datos se han almacenado y están disponibles, la recuperación se simplifica.

**Interrupción de alimentación, Bloqueo del sistema:** Las API del sistema de archivos no suelen diseñarse ni utilizarse de forma sólida para evitar fallos inesperados del sistema. Si se produce un corte de alimentación o un bloqueo del sistema, es más probable que el contenido de documento que se almacena en la base de datos esté actualizado que el contenido que se almacena en un sistema de archivos.

Si está utilizando el modo de copia de seguridad móvil, aún se encuentra en el modo de copia de seguridad después de la recuperación. Si está utilizando el modo de copia de seguridad instantánea, no se encuentra en el modo de copia de seguridad después de la recuperación.

Al restaurar desde el backup a un nuevo sistema, las siguientes configuraciones pueden ser diferentes. Esta diferencia no debe afectar a una recuperación correcta de la aplicación de formularios AEM:

* Dirección IP
* Configuración física del sistema (CPU, disco, memoria)
* Ubicación de GDS

>[!NOTE]
>
>La copia de seguridad del directorio raíz de Almacenamiento de contenido debe restaurarse a la ubicación de ese directorio tal como se estableció durante la configuración de Content Services.

Si falla un solo nodo de un clúster de varios nodos y los nodos restantes del clúster funcionan correctamente, ejecute el procedimiento de recuperación de un solo nodo del clúster.

## Recuperar datos de formularios de AEM {#recover-the-aem-forms-data}

1. Detenga los servicios de formularios AEM y el servidor de aplicaciones si se están ejecutando.
1. Si es necesario, vuelva a crear el sistema físico a partir de una imagen del sistema. Por ejemplo, este paso puede no ser necesario si el motivo de la recuperación es un servidor de base de datos defectuoso.
1. Aplique parches o actualizaciones a los formularios AEM que se aplicaron desde que se creó la imagen. Esta información se registró en el procedimiento de copia de seguridad. Los formularios AEM deben parchearse al mismo nivel de parche que cuando se realizó la copia de seguridad del sistema.
1. (Servidor de aplicaciones WebSphere) Si se está recuperando a una nueva instancia de WebSphere Application Server, ejecute el comando restoreConfig.bat/sh.
1. Recupere la base de datos de formularios AEM ejecutando primero una operación de restauración de la base de datos mediante los archivos de copia de seguridad de la base de datos y aplicando los redo logs de transacciones a la base de datos recuperada. (Consulte Base de datos [de formularios de](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)AEM). Para obtener más información, consulte uno de estos artículos de la base de conocimiento:

   * [Formularios de Oracle Backup and Recovery para AEM](https://www.adobe.com/go/kb403624)
   * [Formularios de respaldo y recuperación de MySQL para AEM](https://www.adobe.com/go/kb403625)
   * [Formularios de Backup y Recuperación de Microsoft SQL Server para AEM](https://www.adobe.com/go/kb403623)
   * [Backup y recuperación de DB2 para formularios AEM](https://www.adobe.com/go/kb403626)

1. Recupere el directorio GDS eliminando primero el contenido del directorio GDS en la instalación existente de formularios AEM y copiando el contenido del directorio GDS desde el GDS de copia de seguridad. Si ha cambiado la ubicación del directorio GDS, consulte [Cambio de la ubicación GDS durante la recuperación](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. Cambie el nombre del directorio de copia de seguridad de GDS que se va a restaurar, como se muestra en estos ejemplos:

   >[!NOTE]
   >
   >Si el directorio /restore ya existe, haga una copia de seguridad y luego elimínelo antes de cambiar el nombre del directorio /backup que contiene los datos más recientes.

   * (JBoss) Cambiar el nombre `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` a:

      `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`.

   * (WebLogic) Cambiar el nombre `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` a:

      `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`.

   * (WebSphere) Cambiar el nombre `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` a:

      `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`.

1. Para recuperar el directorio raíz de Almacenamiento de contenido, primero elimine el contenido del directorio raíz de Almacenamiento de contenido en la instalación existente de formularios AEM y, a continuación, recupere el contenido siguiendo las tareas de entornos independientes o agrupados:

   >[!NOTE]
   >
   >La copia de seguridad del directorio Raíz de Almacenamiento de contenido debe restaurarse a la ubicación del directorio Raíz de Almacenamiento de contenido tal como se configuró durante la configuración de Content Services (obsoleto).

   **Independiente:** Durante el proceso de recuperación, restaure todos los directorios de los que se realizó una copia de seguridad. Cuando se restauran estos directorios, si el directorio /backup-lucene-indexes está presente, cámbiele el nombre a /lucene-indexes. De lo contrario, el directorio lucene-indexes ya debería existir y no se requiere ninguna acción.

   **Agrupado:** Durante el proceso de recuperación, restaure todos los directorios de los que se realizó una copia de seguridad. Para restaurar el directorio raíz de índice, realice los siguientes pasos en cada nodo del clúster:

   * Elimine todo el contenido del directorio raíz del índice.
   * Si el directorio /backup-lucene-indexes está presente, copie el contenido del directorio raíz del Almacenamiento de *contenido*/backup-lucene-indexes en el directorio raíz del índice y elimine el directorio raíz del Almacenamiento de *contenido*/directorio de índices de lucene-lucene.
   * Si el directorio /lucene-indexes está presente, copie el contenido del directorio *raíz del Almacenamiento de* contenido/lucene-indexes en el directorio raíz del índice.

1. Restaure/recupere el repositorio de CRX.

   * **Independiente**

      *Restaure instancias* de creación y publicación: Si se produce un desastre, puede restaurar el repositorio al último estado de copia de seguridad realizando los pasos descritos en [Copia de seguridad y restauración.](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)

      La restauración completa del nodo Autor determina también la restauración de datos de Forms Manager y AEM Forms Workspace.

   * **Agrupado**

      Para restaurar en un entorno agrupado, consulte [Estrategia para backup y restore en un entorno](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment)agrupado.

1. Elimine los archivos temporales de formularios AEM que se hayan creado en el directorio java.io.temp o en el directorio temporal de Adobe.
1. Inicio de formularios AEM (consulte [Inicio y parada de servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## Cambio de la ubicación del GDS durante la recuperación {#changing-the-gds-location-during-recovery}

Si el GDS se restaura en una ubicación distinta de la original, ejecute la secuencia de comandos LCSetGDS para establecer el GDS en la nueva ubicación. La secuencia de comandos se encuentra en la `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` carpeta. La secuencia de comandos toma dos parámetros `defaultGDS` y `newGDS`. Consulte el `ReadMe.txt` archivo de la misma carpeta para obtener instrucciones sobre cómo ejecutar la secuencia de comandos.

>[!NOTE]
>
>Si ha activado el almacenamiento de documento en la base de datos, no es necesario cambiar la ubicación de GDS.

>[!NOTE]
>
>Esta circunstancia es la única en la que debe utilizar esta secuencia de comandos para cambiar la ubicación del GDS. Para cambiar la ubicación de GDS mientras se ejecutan formularios AEM, utilice la Consola de administración. (Consulte [Configuración general de la configuración](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)de formularios AEM).

>[!NOTE]
>
>La implementación de componentes fallará en Windows si el directorio GDS está en la raíz de la unidad (por ejemplo, D:\). Para GDS, debe asegurarse de que el directorio no se encuentra en la raíz de la unidad, sino en un subdirectorio. Por ejemplo, el directorio debe ser D:\GDS and not simply D:\.

## Recuperación del SMD en un entorno agrupado {#recovering-the-gds-to-a-clustered-environment}

Para cambiar la ubicación de GDS en un entorno agrupado, cierre todo el clúster y ejecute la secuencia de comandos LCSetGDS en un solo nodo del clúster. (Consulte [Cambio de la ubicación del GDS durante la recuperación](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)). Inicio sólo ese nodo. Cuando ese nodo esté completamente iniciado, es posible que otros nodos del clúster se inicien de forma segura y apunten correctamente al nuevo GDS.

>[!NOTE]
>
>Si no puede asegurarse de iniciar un nodo completamente antes de iniciar otros nodos, debe ejecutar la secuencia de comandos LCSetGDS en todos los nodos del clúster antes de realizar el inicio del clúster.

