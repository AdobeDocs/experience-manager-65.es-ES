---
title: Estrategia de copia de seguridad y restauración en un entorno en clúster
description: AEM AEM Si la implementación de los formularios de la almacena datos personalizados adicionales en una base de datos diferente, debe implementar una estrategia para realizar una copia de seguridad de estos datos, asegurándose de que permanezcan sincronizados con los datos de los formularios de la forma de la aplicación.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 98c96349-f253-475f-b646-352269814a38
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1396'
ht-degree: 1%

---

# Estrategia de copia de seguridad y restauración en un entorno en clúster {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>AEM AEM Si la implementación de los formularios de la almacena datos personalizados adicionales en una base de datos diferente, debe implementar una estrategia para realizar una copia de seguridad de estos datos, asegurándose de que permanezcan sincronizados con los datos de los formularios de la forma de la aplicación. Además, la aplicación debe diseñarse para que sea lo suficientemente sólida como para gestionar un escenario en el que las bases de datos adicionales no estén sincronizadas. Se recomienda encarecidamente que cualquier operación de base de datos que se realice se realice en el contexto de una transacción para mantener un estado coherente.

AEM Debe realizar una copia de seguridad de las siguientes partes del sistema de formularios de la para recuperarse de cualquier error:

* AEM Base de datos utilizada por formularios de
* GDS con datos de larga duración y otros documentos persistentes
* AEM base de datos de (repositorio crx)

>[!NOTE]
>
>AEM Debe realizar una copia de seguridad de cualquier otro dato que esté utilizando la configuración de los formularios de la aplicación, como las fuentes de los clientes, los datos de los conectores, etc.

## Copia de seguridad de un entorno agrupado {#back-up-a-clustered-environment}

AEM En este tema se describen las siguientes estrategias para realizar una copia de seguridad de cualquier entorno agrupado de formularios en la aplicación de la:

* Copia de seguridad sin conexión con tiempo de inactividad
* Copia de seguridad sin conexión sin tiempo de inactividad (copia de seguridad de un nodo secundario que se cierra)
* Backup en línea sin tiempo de inactividad pero con retraso en la respuesta
* Copia de seguridad del archivo de propiedades del Bootstrap

### Copia de seguridad sin conexión con tiempo de inactividad {#offline-backup-with-downtime}

1. Apague todo el clúster y los servicios relacionados. (consulte [Iniciar y detener servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. En cualquier nodo, haga una copia de seguridad de la base de datos, GDS y Connectors. (vea [Archivos para realizar copias de seguridad y recuperar](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. AEM Para realizar una copia de seguridad sin conexión del repositorio de, realice los siguientes pasos:

   1. Para cada nodo de clúster, haga una copia de seguridad del archivo que contiene el identificador del nodo de clúster.
   1. Haga una copia de seguridad de todos los archivos de cualquier nodo de clúster secundario, incluidos los subdirectorios.
   1. Haga una copia de seguridad del ID de sistema/repositorio de cada nodo del clúster por separado.

   Para ver los pasos detallados, consulte [Copia de seguridad y restauración](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. Haga una copia de seguridad de cualquier otro dato, como las fuentes del cliente.
1. Inicie de nuevo el clúster.

### Copia de seguridad sin conexión sin tiempo de inactividad {#offline-backup-with-no-downtime}

1. Introduzca el modo de copia de seguridad móvil. (consulte [Introducción de los modos de copia de seguridad](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   Deje el modo de copia de seguridad móvil después de una recuperación.

1. AEM Cierre cualquiera de los nodos secundarios del clúster en lo que respecta a la. (consulte [Iniciar y detener servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. En cualquier nodo, haga una copia de seguridad de la base de datos, GDS y Connectors. (vea [Archivos para realizar copias de seguridad y recuperar](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. AEM Para realizar una copia de seguridad sin conexión del repositorio de, realice los siguientes pasos:

   1. Para cada nodo de clúster, haga una copia de seguridad del archivo que contiene el identificador del nodo de clúster.
   1. Haga una copia de seguridad de todos los archivos de cualquier nodo de clúster secundario, incluidos los subdirectorios.
   1. Haga una copia de seguridad de repository/system.id de cada nodo de clúster por separado.

   Para ver los pasos detallados, consulte [Copia de seguridad y restauración](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. Haga una copia de seguridad de cualquier otro dato, como las fuentes del cliente.
1. Inicie de nuevo el clúster.

### Backup en línea sin tiempo de inactividad pero con retraso en la respuesta {#online-backup-with-no-downtime-but-delay-in-response}

1. Introduzca el modo de copia de seguridad móvil. (consulte [Introducción de los modos de copia de seguridad](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   Deje el modo de copia de seguridad móvil después de una recuperación.

1. AEM Cierre cualquiera de los nodos secundarios del clúster en lo que respecta a la. (consulte [Iniciar y detener servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. En cualquier nodo, haga una copia de seguridad de la base de datos, GDS y Connectors. (vea [Archivos para realizar copias de seguridad y recuperar](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. AEM Para realizar una copia de seguridad en línea del repositorio de, realice los siguientes pasos:

   1. Para cada nodo de clúster, haga una copia de seguridad del archivo que contiene cluster_node.id.
   1. Haga una copia de seguridad de repository/system.id de cada nodo de clúster por separado.
   1. En cualquier nodo secundario, realice una copia de seguridad en línea del repositorio para ver los pasos detallados, consulte Copia de seguridad en línea.

1. Haga una copia de seguridad de cualquier otro dato, como las fuentes del cliente.
1. Inicie de nuevo el clúster.

### Copia de seguridad del archivo de propiedades del Bootstrap {#back-up-the-bootstrap-properties-file}

AEM Cuando creamos un clúster de, se crea un archivo de propiedades en el servidor de aplicaciones para todos los nodos secundarios. Se recomienda realizar una copia de seguridad del archivo de propiedades del Bootstrap. Puede encontrar el archivo en la siguiente ubicación del servidor de aplicaciones:

* JBoss®: en el directorio BIN
* WebLogic: en el directorio de dominio
* WebSphere®: en el directorio de perfil

AEM Haga una copia de seguridad del archivo para el escenario de recuperación ante desastres de nodo secundario y reemplácelo en la ubicación especificada en el servidor de aplicaciones, si se restaura.

## Recuperación en un entorno agrupado {#recovery-in-a-clustered-environment}

Si se produce algún error en todo el clúster o en un solo nodo, restáurelo mediante la copia de seguridad.

Para una recuperación de nodo único, cierre el nodo único y ejecute el procedimiento de recuperación de nodo único.

Si todo el clúster falla debido a errores como el bloqueo de la base de datos, realice los siguientes pasos. La restauración depende del método de copia de seguridad utilizado.

### Restauración de un solo nodo {#restoring-a-single-node}

1. Detenga el nodo dañado.

   >[!NOTE]
   >
   >AEM Si el nodo dañado es un nodo principal de la red, cierre todo el nodo del clúster.

1. Vuelva a crear el sistema físico a partir de una imagen del sistema.
1. AEM Aplique parches o actualizaciones a los formularios de la aplicación desde que se creó la imagen. Esta información se registró durante el procedimiento de copia de seguridad. AEM Los formularios se deben recuperar al mismo nivel de parche que cuando se realizó la copia de seguridad del sistema.
1. AEM (*Opcional*) Si todos los demás nodos funcionan bien, es posible que el repositorio de la también esté dañado. AEM En este caso, verá un mensaje de desincronización del repositorio en el archivo error.log del repositorio de la.

   Para restaurar el repositorio, realice los siguientes pasos.

   >[!NOTE]
   >
   >Si se ha realizado una copia de seguridad en línea del repositorio crx comprimido, descomprímalo en cualquier ubicación y siga el proceso de restauración sin conexión.

   1. Elimine los directorios del repositorio, compartidos, de versión y de espacios de trabajo en el directorio clusterNode del nodo.
   1. Restaure la copia de seguridad del nodo de clúster (incluidos los subdirectorios) en el nodo.
   1. Elimine el archivo clusterNode/revision.log en el nodo.
   1. Elimine el .lock en el nodo, si existe.
   1. Elimine el repository/system.id en el nodo, si existe.
   1. Elimine los archivos &ast;&ast;/listener.properties en el nodo, si existe.
   1. Restaure repository/cluster_node.id para nodos de clúster individuales.

>[!NOTE]
>
>Tenga en cuenta los siguientes puntos:

* AEM Si el nodo con error era un nodo principal, copie todo el contenido de la carpeta del repositorio secundario (crx-repository\crx.0000, donde 0000 puede ser cualquier dígito) en la carpeta del repositorio crx\ y elimine la carpeta del repositorio secundario.
* Antes de reiniciar cualquier nodo de clúster, asegúrese de eliminar el repositorio /clustered.txt del nodo principal.
* Asegúrese de que el nodo principal se inicia primero y, después de iniciarlo, inicie otros nodos.

### Restauración de todo el clúster {#restoring-the-entire-cluster}

1. Detenga todos los nodos del clúster.
1. Vuelva a crear el sistema físico a partir de una imagen del sistema.
1. AEM Aplique parches o actualizaciones a los formularios de AEM que se han aplicado desde que se creó la imagen. Esta información se registró en el paso 1 del procedimiento de copia de seguridad. AEM Los formularios se deben recuperar al mismo nivel de parche que cuando se realizó la copia de seguridad del sistema.
1. Restaure la base de datos, GDS y los conectores.
1. AEM Haga lo siguiente para recuperar el repositorio sin conexión de la:

   >[!NOTE]
   >
   >Si se ha realizado una copia de seguridad en línea del repositorio crx comprimido, descomprímalo en cualquier ubicación y siga el proceso de restauración sin conexión.

   1. En todos los nodos del clúster, elimine los directorios del repositorio, compartido, versión y espacios de trabajo del directorio clusterNode.
   1. Eliminar todos los archivos y directorios del directorio compartido.
   1. Restaure la copia de seguridad del nodo de clúster (incluidos los subdirectorios) en un nodo de clúster.
   1. Copie todos los archivos del nodo de clúster restaurado en todos los demás nodos de clúster. Una vez finalizado, cada nodo de clúster contiene los mismos datos.
   1. Elimine el archivo clusterNode/revision.log en todos los nodos del clúster.
   1. Elimine el .lock en todos los nodos del clúster, si existe.
   1. Elimine todos los nodos de clúster de repository/system.id, si existen.
   1. Elimine los archivos &ast;&ast;/listener.properties en todos los nodos del clúster, si los hay.
   1. Restaure repository/cluster_node.id para nodos de clúster individuales.

>[!NOTE]
>
>Tenga en cuenta los siguientes puntos:

* AEM Si el nodo con error era un nodo principal, copie todo el contenido de la carpeta del repositorio secundario (se parece a crx-repository\crx.0000, donde 0000 puede ser cualquier dígito) en la carpeta del repositorio crx\.
* Antes de reiniciar cualquier nodo de clúster, asegúrese de eliminar el repositorio /clustered.txt del nodo principal.
* Asegúrese de que el nodo principal se inicia primero y, después de iniciarlo, inicie otros nodos.

## Realizar una copia de seguridad y restaurar el nodo de publicación de Administración de correspondencia {#back-up-and-restore-correspondence-management-solution-publish-node}

El nodo del editor no tiene ninguna relación principal-secundaria en un entorno agrupado. Puede realizar una copia de seguridad de cualquier nodo de Publisher siguiendo [Copia de seguridad y restauración](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### Recuperación de un solo nodo de editor {#recover-a-single-publisher-node}

1. Cierre el nodo que debe recuperarse y no realice ninguna actividad de publicación hasta que el nodo vuelva a estar activo.
1. Restaure el nodo Publish mediante [Restaurando la copia de seguridad](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### Recuperar un clúster {#recover-a-cluster}

1. Cierre el clúster.
1. Restaure el nodo Publish mediante [Restaurando la copia de seguridad](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).
1. Inicie el nodo principal seguido del nodo secundario del clúster de creación.
