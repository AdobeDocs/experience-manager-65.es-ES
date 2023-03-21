---
title: Recuperación de los datos de AEM Forms
seo-title: Recovering the AEM forms data
description: En este documento se describen los pasos necesarios para recuperar los datos de los formularios AEM.
seo-description: This document describes the steps required to recover the AEM forms data.
uuid: b5735196-5a8d-4358-884f-e9b8d8f4f682
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e093114-219b-4018-9530-9002eb665448
exl-id: 9e648bab-9284-4fda-abb4-8bd7cd085981
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 0%

---

# Recuperación de los datos de AEM Forms {#recovering-the-aem-forms-data}

En esta sección se describen los pasos necesarios para recuperar los datos de los formularios AEM. Consulte también [Consideraciones especiales para backup y recuperación](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>La base de datos, GDS, el repositorio AEM y los directorios raíz de almacenamiento de contenido deben restaurarse en un equipo con el mismo nombre DNS que el original.

AEM formularios deben recuperarse de forma fiable de los siguientes errores:

**Fallo de disco:** Se requiere el soporte de copia de seguridad más reciente para recuperar el contenido de la base de datos.

**Corrupción de datos:** Los sistemas de archivos no registran transacciones anteriores y es posible que los sistemas sobrescriban accidentalmente los datos de proceso necesarios.

**Error del usuario:** La recuperación se limita a los datos disponibles en la base de datos. Si los datos se almacenaron y están disponibles, la recuperación se simplifica.

**Interrupción de alimentación, Bloqueo del sistema:** Las API del sistema de archivos a menudo no se diseñan ni se utilizan de manera sólida para evitar fallos inesperados del sistema. Si se produce una interrupción de la alimentación o un bloqueo del sistema, es más probable que el contenido del documento almacenado en la base de datos esté actualizado que el contenido almacenado en un sistema de archivos.

Si está utilizando el modo de copia de seguridad móvil, sigue en modo de copia de seguridad después de la recuperación. Si está utilizando el modo de copia de seguridad instantánea, no está en modo de copia de seguridad después de la recuperación.

Al restaurar desde la copia de seguridad a un nuevo sistema, las siguientes configuraciones pueden ser diferentes. Esta diferencia no debe afectar a una recuperación correcta de la aplicación de formularios AEM:

* Dirección IP
* Configuración física del sistema (CPUs, disco, memoria)
* Ubicación de GDS

>[!NOTE]
>
>La copia de seguridad del directorio raíz del almacenamiento de contenido debe restaurarse a la ubicación de ese directorio tal como se estableció durante la configuración de Content Services.

Si falla un solo nodo de un clúster de nodos múltiples y los nodos restantes del clúster funcionan correctamente, ejecute el procedimiento de recuperación de nodos únicos del clúster.

## Recuperar los datos de los formularios AEM {#recover-the-aem-forms-data}

1. Detenga los servicios de formularios AEM y el servidor de aplicaciones si se ejecuta.
1. Si es necesario, vuelva a crear el sistema físico a partir de una imagen del sistema. Por ejemplo, este paso puede no ser necesario si el motivo de la recuperación es un servidor de base de datos defectuoso.
1. Aplique parches o actualizaciones a AEM formularios que se aplicaron desde que se hizo la imagen. Esta información se registró en el procedimiento de copia de seguridad. AEM formularios deben parchearse con el mismo nivel de parche que cuando se realizó la copia de seguridad del sistema.
1. (Servidor de aplicaciones WebSphere®) Si está recuperando una nueva instancia de WebSphere® Application Server, ejecute el comando restoreConfig.bat/sh.
1. Recupere la base de datos de formularios AEM ejecutando primero una operación de restauración de la base de datos utilizando los archivos de copia de seguridad de la base de datos y aplicando los redo logs de transacciones a la base de datos recuperada. (Consulte [base de datos de AEM forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Para obtener más información, consulte uno de estos artículos de la base de conocimientos:

   * [Copia de seguridad y recuperación de DB2® para formularios AEM](https://experienceleague.adobe.com/docs/experience-manager-64/forms/administrator-help/aem-forms-backup-recovery/files-back-recover.html?lang=en#db2)
   * [Copia de seguridad y recuperación de oracle para formularios AEM](https://experienceleague.adobe.com/docs/experience-manager-64/forms/administrator-help/aem-forms-backup-recovery/files-back-recover.html?lang=en#oracle)
   * [Copia de seguridad y recuperación de Microsoft® SQL Server para formularios AEM](https://experienceleague.adobe.com/docs/experience-manager-64/forms/administrator-help/aem-forms-backup-recovery/files-back-recover.html?lang=en#sql-server)
   * [Copia de seguridad y recuperación de MySQL para formularios AEM](https://experienceleague.adobe.com/docs/experience-manager-64/forms/administrator-help/aem-forms-backup-recovery/files-back-recover.html?lang=en#mysql)

1. Recupere el directorio GDS eliminando primero el contenido del directorio GDS en la instalación existente de AEM formularios y copiando el contenido del directorio GDS de la copia de seguridad de GDS. Si ha cambiado la ubicación del directorio GDS, consulte [Cambio de la ubicación de GDS durante la recuperación](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. Cambie el nombre del directorio de copia de seguridad GDS que desea restaurar, como se muestra en estos ejemplos:

   >[!NOTE]
   >
   >Si el directorio /restore ya existe, haga una copia de seguridad y luego elimínelo antes de cambiar el nombre del directorio /backup que contiene los datos más recientes.

   * (JBoss®) Cambiar nombre `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` a:

      `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`.

   * (WebLogic) Cambiar el nombre `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` a:

      `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`.

   * (WebSphere®) Cambiar nombre `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` a:

      `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`.

1. Recupere el directorio raíz del almacenamiento de contenido eliminando primero el contenido del directorio raíz del almacenamiento de contenido en la instalación existente de AEM formularios y recuperando el contenido siguiendo las tareas para entornos independientes o en clúster:

   >[!NOTE]
   >
   >La copia de seguridad del directorio raíz del almacenamiento de contenido debe restaurarse a la ubicación del directorio raíz del almacenamiento de contenido, tal como se configuró durante la configuración de Content Services (obsoleto).

   **Independiente:** Durante el proceso de recuperación, restaure todos los directorios de los que se hizo backup. Cuando se restauran estos directorios, si el directorio /backup-lucene-indexes está presente, renómbralo a /lucene-indexes. De lo contrario, el directorio lucene-indexes ya debería existir y no se requiere ninguna acción.

   **Agrupado:** Durante el proceso de recuperación, restaure todos los directorios de los que se hizo backup. Para restaurar el directorio raíz del índice, realice los siguientes pasos en cada nodo del clúster:

   * Elimine todo el contenido del directorio raíz del índice.
   * Si el directorio /backup-lucene-indexes está presente, copie el contenido del *Directorio raíz del almacenamiento de contenido*/backup-lucene-indexes directorio en el directorio raíz del índice y elimine el *Directorio raíz del almacenamiento de contenido*/backup-lucene-indexes.
   * Si el directorio /lucene-indexes está presente, copie el contenido de *Directorio raíz del almacenamiento de contenido*/lucene-indexes directorio raíz del índice.

1. Restaure/recupere el repositorio CRX.

   * **Independiente**

      *Restaurar instancias de autor y publicación*: Si se produce un desastre, puede restaurar el repositorio al último estado de copia de seguridad realizando los pasos descritos en [Copia de seguridad y restauración.](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html)

      La restauración completa del nodo Autor también determina la restauración de los datos de Forms Manager y AEM Forms Workspace.

   * **Agrupado**

      Para restaurar en un entorno agrupado, consulte [Estrategia para backup y restore en un entorno en cluster](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. Elimine los archivos temporales de formularios AEM que se hayan creado en el directorio java.io.temp o en el directorio temporal de Adobe.
1. Inicio AEM formularios (consulte [Inicio y parada de servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## Cambio de la ubicación de GDS durante la recuperación {#changing-the-gds-location-during-recovery}

Si el GDS se restaura a una ubicación distinta a la original, ejecute el script LCSetGDS para establecer el GDS en la nueva ubicación. La secuencia de comandos se encuentra en el `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` carpeta. La secuencia de comandos toma dos parámetros, `defaultGDS` y `newGDS`. Consulte la `ReadMe.txt` en la misma carpeta para obtener instrucciones sobre cómo ejecutar la secuencia de comandos.

>[!NOTE]
>
>Si ha habilitado el almacenamiento de documentos en la base de datos, no es necesario cambiar la ubicación de GDS.

>[!NOTE]
>
>Esta circunstancia es la única en la que debe utilizar esta secuencia de comandos para cambiar la ubicación de GDS. Para cambiar la ubicación de GDS mientras se ejecutan AEM formularios, utilice la Consola de administración. (Consulte [Configuración general de AEM formularios](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).)

>[!NOTE]
>
>La implementación de componentes fallará en Windows si el directorio GDS está en la raíz de la unidad (por ejemplo, D:\). Para GDS, debe asegurarse de que el directorio no está ubicado en la raíz de la unidad, sino en un subdirectorio. Por ejemplo, el directorio debe ser D:\GDS and not simply D:\.

## Recuperación del GDS en un entorno agrupado {#recovering-the-gds-to-a-clustered-environment}

Para cambiar la ubicación de GDS en un entorno agrupado, cierre todo el clúster y ejecute el script LCSetGDS en un solo nodo del clúster. (Consulte [Cambio de la ubicación de GDS durante la recuperación](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).) Inicie solo ese nodo. Cuando ese nodo está completamente iniciado, otros nodos del clúster pueden iniciarse de forma segura y apuntarán correctamente al nuevo GDS.

>[!NOTE]
>
>Si no puede asegurarse de iniciar un nodo completamente antes de iniciar otros nodos, debe ejecutar el script LCSetGDS en cada nodo del clúster antes de iniciar el clúster.
