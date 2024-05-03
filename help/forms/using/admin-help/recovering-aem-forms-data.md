---
title: Recuperación de los datos de AEM Forms
description: AEM En este documento se describen los pasos necesarios para recuperar los datos de los formularios de la.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9e648bab-9284-4fda-abb4-8bd7cd085981
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 1%

---

# Recuperación de los datos de AEM Forms {#recovering-the-aem-forms-data}

AEM En esta sección se describen los pasos necesarios para recuperar los datos de los formularios de la. Consulte también [Consideraciones especiales para el backup y la recuperación](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>AEM Los directorios de base de datos, GDS, repositorio de y raíz de almacenamiento de contenido deben restaurarse en un equipo con el mismo nombre DNS que el original.

AEM Los formularios de datos deben recuperarse de forma fiable de los siguientes errores:

**Error de disco:** Se necesita el medio de copia de seguridad más reciente para recuperar el contenido de la base de datos.

**Datos dañados:** Los sistemas de archivos no registran las transacciones anteriores y pueden sobrescribir accidentalmente los datos de proceso necesarios.

**Error de usuario:** La recuperación se limita a los datos que la base de datos pone a disposición. Si los datos se almacenaron y están disponibles, la recuperación se simplifica.

**Cortes de alimentación, bloqueo del sistema:** Las API del sistema de archivos no suelen diseñarse ni utilizarse de manera sólida que proteja contra errores inesperados del sistema. Si se produce un corte de alimentación o un bloqueo del sistema, es más probable que el contenido del documento almacenado en la base de datos esté actualizado que el contenido almacenado en un sistema de archivos.

Si está utilizando el modo de copia de seguridad móvil, aún está en modo de copia de seguridad después de la recuperación. Si está utilizando el modo de copia de seguridad de instantánea, no estará en modo de copia de seguridad después de la recuperación.

Al restaurar desde la copia de seguridad en un sistema nuevo, las siguientes configuraciones pueden ser diferentes. AEM Esta diferencia no debería afectar a la recuperación correcta de la aplicación de formularios en la que se ha realizado el:

* Dirección IP
* Configuración del sistema físico (CPU, disco, memoria)
* Ubicación de GDS

>[!NOTE]
>
>La copia de seguridad del directorio raíz de almacenamiento de contenido debe restaurarse a la ubicación de ese directorio tal como se estableció durante la configuración de Content Services.

Si un nodo único de un clúster de varios nodos ha fallado y los nodos restantes del clúster funcionan correctamente, realice el procedimiento de recuperación de nodo único del clúster.

## AEM Recuperar los datos de los formularios {#recover-the-aem-forms-data}

1. AEM Detenga los servicios de formularios y el servidor de aplicaciones de la si se ejecuta.
1. Si es necesario, vuelva a crear el sistema físico a partir de una imagen del sistema. Por ejemplo, este paso puede no ser necesario si el motivo de la recuperación es un servidor de base de datos defectuoso.
1. AEM Aplique parches o actualizaciones a los formularios de la aplicación desde que se creó la imagen. Esta información se registró en el procedimiento de copia de seguridad. AEM Se debe aplicar un parche a los formularios en el mismo nivel de parche que se aplicaba cuando se hizo una copia de seguridad del sistema.
1. (Servidor de aplicaciones WebSphere®) Si se recupera en una nueva instancia de WebSphere®, ejecute el comando restoreConfig.bat/sh.
1. AEM Recupere la base de datos de formularios de la base de datos de la aplicación ejecutando primero una operación de restauración de la base de datos utilizando los archivos de copia de seguridad de la base de datos y, a continuación, aplicando los redo logs de transacción a la base de datos recuperada. (Consulte [AEM base de datos de formularios](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Para obtener más información, consulte uno de estos artículos de la base de conocimiento:

   * [DB2](/help/forms/using/admin-help/files-back-recover.md#db2)
   * [Copia de seguridad y recuperación de oracle AEM para formularios de](/help/forms/using/admin-help/files-back-recover.md#oracle)
   * [Microsoft](/help/forms/using/admin-help/files-back-recover.md#sql-server)
   * [AEM Copia de seguridad y recuperación de MySQL para formularios de](/help/forms/using/admin-help/files-back-recover.md#mysql)

1. AEM Recupere el directorio GDS eliminando primero el contenido del directorio GDS en la instalación existente de formularios de GDS y, a continuación, copiando el contenido del directorio GDS desde el GDS de copia de seguridad. Si ha cambiado la ubicación del directorio GDS, consulte [Cambio de la ubicación de GDS durante la recuperación](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. Cambie el nombre del directorio de copia de seguridad de GDS que desea restaurar, como se muestra en estos ejemplos:

   >[!NOTE]
   >
   >Si el directorio /restore ya existe, haga una copia de seguridad del mismo y elimínelo antes de cambiar el nombre del directorio /backup que contiene los datos más recientes.

   * (JBoss®) Cambiar nombre `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` hasta:

     `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`.

   * (WebLogic) Cambiar nombre `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` hasta:

     `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`.

   * (WebSphere®) Cambiar nombre `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` hasta:

     `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`.

1. AEM Recupere el directorio raíz de almacenamiento de contenido eliminando primero el contenido del directorio raíz de almacenamiento de contenido en la instalación existente de formularios en la que ya existen y, a continuación, recuperando el contenido siguiendo las tareas de los entornos independientes o agrupados:

   >[!NOTE]
   >
   >La copia de seguridad del directorio raíz de almacenamiento de contenido debe restaurarse a la ubicación del directorio raíz de almacenamiento de contenido tal como se estableció durante la configuración de Content Services (obsoleto).

   **Independiente:** Durante el proceso de recuperación, restaure todos los directorios de los que se hizo una copia de seguridad. Cuando se restauren estos directorios, si el directorio /backup-lucene-indexes está presente, renómbrelo a /lucene-indexes. De lo contrario, el directorio lucene-indexes ya debería existir y no se requiere ninguna acción.

   **Agrupado:** Durante el proceso de recuperación, restaure todos los directorios de los que se hizo una copia de seguridad. Para restaurar el directorio raíz del índice, realice los siguientes pasos en cada nodo del clúster:

   * Elimine todo el contenido del directorio raíz del índice.
   * Si el directorio /backup-lucene-indexes está presente, copie el contenido del *Directorio raíz de almacenamiento de contenido*/backup-lucene-indexes al directorio raíz del índice y elimine el *Directorio raíz de almacenamiento de contenido* directorio /backup-lucene-indexes.
   * Si el directorio /lucene-indexes está presente, copie el contenido del *Directorio raíz de almacenamiento de contenido* directorio /lucene-indexes al directorio raíz del índice.

1. Restaurar/recuperar el repositorio CRX.

   * **Independiente**

     *Restaurar instancias de autor y publicación*: Si se produce un desastre, puede restaurar el repositorio al último estado de copia de seguridad realizando los pasos descritos en [Copia de seguridad y restauración](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html)

     La restauración completa del nodo Autor también determina la restauración de los datos de Forms Manager y AEM Forms Workspace.

   * **Agrupado**

     Para la restauración en un entorno agrupado, consulte [Estrategia de copia de seguridad y restauración en un entorno en clúster](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. AEM Elimine cualquier archivo temporal de formularios de la forma de la aplicación que se haya creado en el directorio java.io.temp o en el directorio temporal del Adobe.
1. AEM Inicio de formularios (consulte ) [Iniciar y detener servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## Cambio de la ubicación de GDS durante la recuperación {#changing-the-gds-location-during-recovery}

Si el GDS se restaura en una ubicación distinta a la original, ejecute el script LCSetGDS para establecer el GDS en la nueva ubicación. La secuencia de comandos se encuentra en `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` carpeta. La secuencia de comandos toma dos parámetros, `defaultGDS` y `newGDS`. Consulte la `ReadMe.txt` en la misma carpeta para obtener instrucciones sobre cómo ejecutar la secuencia de comandos.

>[!NOTE]
>
>Si ha habilitado el almacenamiento de documentos en la base de datos, no es necesario cambiar la ubicación de GDS.

>[!NOTE]
>
>Esta circunstancia es la única en la que debería usar esta secuencia de comandos para cambiar la ubicación de GDS. AEM Para cambiar la ubicación de GDS mientras se está ejecutando el formulario de GDS, utilice la consola de administración. (Consulte [AEM Configurar opciones generales de formularios](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).)

>[!NOTE]
>
>La implementación de componentes fallará en Windows si el directorio GDS se encuentra en la raíz de la unidad (por ejemplo, D:\). Para GDS, debe asegurarse de que el directorio no se encuentra en la raíz de la unidad, sino en un subdirectorio. Por ejemplo, el directorio debe ser D:\GDS y no simplemente D:\.

## Recuperación del GDS en un entorno agrupado {#recovering-the-gds-to-a-clustered-environment}

Para cambiar la ubicación de GDS en un entorno agrupado, apague todo el clúster y ejecute el script LCSetGDS en un solo nodo del clúster. (Consulte [Cambio de la ubicación de GDS durante la recuperación](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).) Inicie solo ese nodo. Cuando ese nodo esté completamente iniciado, es posible que otros nodos del clúster se inicien de forma segura y apunten correctamente al nuevo GDS.

>[!NOTE]
>
>Si no puede asegurarse de que se inicia un nodo completamente antes de iniciar otros nodos, debe ejecutar el script LCSetGDS en todos los nodos del clúster antes de iniciar el clúster.
