---
title: Estrategia de copia de seguridad y restauración en un entorno en clúster
seo-title: Strategy for backup and restore in a clustered environment
description: Si la implementación de AEM forms almacena datos personalizados adicionales en una base de datos diferente, debe implementar una estrategia para realizar una copia de seguridad de estos datos, asegurándose de que se mantengan sincronizados con los datos de AEM forms.
seo-description: If your AEM forms implementation stores additional custom data in a different database, you must implement a strategy to back up this data ensuring that it remains in sync with the AEM forms data.
uuid: c29b989c-30ed-4a8e-bab8-9b7746291a33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c332985b-4556-4056-961a-fce2356da88d
exl-id: 98c96349-f253-475f-b646-352269814a38
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 1%

---

# Estrategia de copia de seguridad y restauración en un entorno en clúster {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>Si la implementación de AEM forms almacena datos personalizados adicionales en una base de datos diferente, debe implementar una estrategia para realizar una copia de seguridad de estos datos, asegurándose de que se mantengan sincronizados con los datos de AEM forms. Además, la aplicación debe diseñarse para que sea lo suficientemente robusta como para gestionar un escenario en el que las bases de datos adicionales no estén sincronizadas. Es muy recomendable que cualquier operación de base de datos que se realice se realice en el contexto de una transacción para ayudar a mantener un estado coherente.

Debe realizar una copia de seguridad de las siguientes partes del sistema de formularios AEM para recuperarse de cualquier error:

* Base de datos utilizada por AEM formularios
* GDS con datos de larga duración y otros documentos persistentes
* AEM base de datos (crx-repository)

>[!NOTE]
>
>Es necesario realizar una copia de seguridad de cualquier otro dato que esté utilizando la configuración de formularios AEM, como fuentes de cliente, datos de conectores, etc.

## Realizar una copia de seguridad de un entorno en clúster {#back-up-a-clustered-environment}

En este tema se tratan las siguientes estrategias para realizar copias de seguridad de cualquier entorno agrupado de AEM formularios:

* Backup sin conexión con tiempo de inactividad
* Copia de seguridad sin conexión sin tiempo de inactividad (copia de seguridad de un nodo secundario que está apagado)
* Copia de seguridad en línea sin downtime pero con retraso en la respuesta
* Haga una copia de seguridad del archivo de propiedades del Bootstrap

### Backup sin conexión con tiempo de inactividad {#offline-backup-with-downtime}

1. Apague todo el clúster y los servicios relacionados. (consulte [Inicio y parada de servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. En cualquier nodo, realice una copia de seguridad de la base de datos, GDS y Conectores. (consulte [Archivos para realizar copias de seguridad y recuperar](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Para realizar copias de seguridad AEM repositorio sin conexión, realice los siguientes pasos:

   1. Para cada nodo de clúster, haga una copia de seguridad del archivo que contiene el identificador del nodo de clúster.
   1. Haga una copia de seguridad de todos los archivos de cualquier nodo de clúster secundario, incluidos los subdirectorios.
   1. Haga una copia de seguridad del id de repositorio/sistema de cada nodo de clúster por separado.

   Para ver los pasos detallados, consulte [Copia de seguridad y restauración](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. Haga una copia de seguridad de cualquier otro dato, como las fuentes del cliente.
1. Inicie el clúster de nuevo.

### Backup sin conexión sin downtime {#offline-backup-with-no-downtime}

1. Introduzca el modo de copia de seguridad móvil. (consulte [Introducción de los modos de copia de seguridad](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   Deje el modo de copia de seguridad móvil después de una recuperación.

1. Apague cualquiera de los nodos secundarios del clúster con respecto a AEM. (consulte [Inicio y parada de servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. En cualquier nodo, realice una copia de seguridad de la base de datos, GDS y Conectores. (consulte [Archivos para realizar copias de seguridad y recuperar](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Para realizar copias de seguridad AEM repositorio sin conexión, realice los siguientes pasos:

   1. Para cada nodo de clúster, haga una copia de seguridad del archivo que contiene el identificador del nodo de clúster.
   1. Haga una copia de seguridad de todos los archivos de cualquier nodo de clúster secundario, incluidos los subdirectorios.
   1. Haga una copia de seguridad de repository/system.id de cada nodo de clúster por separado.

   Para ver los pasos detallados, consulte [Copia de seguridad y restauración](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. Haga una copia de seguridad de cualquier otro dato, como las fuentes del cliente.
1. Inicie el clúster de nuevo.

### Copia de seguridad en línea sin downtime pero con retraso en la respuesta {#online-backup-with-no-downtime-but-delay-in-response}

1. Introduzca el modo de copia de seguridad móvil. (consulte [Introducción de los modos de copia de seguridad](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   Deje el modo de copia de seguridad móvil después de una recuperación.

1. Apague cualquiera de los nodos secundarios del clúster con respecto a AEM. (consulte [Inicio y parada de servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. En cualquier nodo, realice una copia de seguridad de la base de datos, GDS y Conectores. (consulte [Archivos para realizar copias de seguridad y recuperar](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Para realizar copias de seguridad AEM repositorio en línea, realice los siguientes pasos:

   1. Para cada nodo de clúster, haga una copia de seguridad del archivo que contiene el cluster_node.id.
   1. Haga una copia de seguridad de repository/system.id de cada nodo de clúster por separado.
   1. En cualquier nodo secundario, realice una copia de seguridad en línea del repositorio para ver los pasos detallados; consulte Copia de seguridad en línea.

1. Haga una copia de seguridad de cualquier otro dato, como las fuentes del cliente.
1. Inicie el clúster de nuevo.

### Haga una copia de seguridad del archivo de propiedades del Bootstrap {#back-up-the-bootstrap-properties-file}

Cuando creamos un clúster de AEM, se crea un archivo de propiedades en el servidor de aplicaciones para todos los nodos secundarios. Se recomienda realizar una copia de seguridad del archivo de propiedades del Bootstrap. Puede encontrar el archivo en la siguiente ubicación del servidor de aplicaciones:

* JBoss®: en el directorio BIN
* WebLogic: en el directorio de dominio
* WebSphere®: en el directorio de perfiles

Haga una copia de seguridad del archivo para el escenario de recuperación ante desastres de AEM nodo secundario y sustitúyalo en la ubicación especificada en el servidor de aplicaciones, si se restaura.

## Recuperación en un entorno agrupado {#recovery-in-a-clustered-environment}

Si hay algún fallo en todo el clúster o en un solo nodo, restablézcalo usando la copia de seguridad.

Para una recuperación de nodo único, cierre el nodo único y ejecute el procedimiento de recuperación de nodo único.

En caso de que todo el clúster falle debido a errores como el bloqueo de la base de datos, realice los siguientes pasos. La restauración depende del método de copia de seguridad utilizado.

### Restauración de un solo nodo {#restoring-a-single-node}

1. Detenga el nodo dañado.

   >[!NOTE]
   >
   >Si el nodo dañado es un nodo primario AEM, cierre todo el nodo del clúster.

1. Vuelva a crear el sistema físico a partir de una imagen del sistema.
1. Aplique parches o actualizaciones a AEM formularios que se aplicaron desde que se hizo la imagen. Esta información se registró durante el procedimiento de copia de seguridad. AEM formularios deben recuperarse al mismo nivel de parche que cuando se realizó la copia de seguridad del sistema.
1. (*Opcional*) Si todos los demás nodos funcionan bien, es posible que el repositorio de AEM también esté dañado. En este caso, verá un mensaje unsync del repositorio en el archivo error.log del repositorio AEM.

   Para restaurar el repositorio, realice los siguientes pasos.

   >[!NOTE]
   >
   >Si una copia de seguridad comprimida del repositorio crx se ha conectado, descomprima el archivo en cualquier ubicación y siga el proceso de restauración sin conexión.

   1. Elimine los directorios de repositorio, compartido, versión y espacios de trabajo en el directorio clusterNode del nodo .
   1. Restaure la copia de seguridad del nodo del clúster (incluidos los subdirectorios) al nodo .
   1. Elimine el archivo clusterNode/revision.log en el nodo .
   1. Elimine el .lock en el nodo, si existe.
   1. Elimine el repository/system.id en el nodo , si existe.
   1. Elimine los archivos &amp;ast;&amp;ast;/listener.properties del nodo, si existe.
   1. Restaure repository/cluster_node.id para nodos de clúster individuales.

>[!NOTE]
>
>Consideremos los siguientes puntos:

* Si el nodo en el que se produjo el error era un nodo primario AEM, copie todo el contenido de la carpeta del repositorio secundario (crx-repository\crx.0000 donde 000 puede ser cualquier dígito) en la carpeta del repositorio crx-repository\ y elimine la carpeta del repositorio secundario.
* Antes de reiniciar cualquier nodo de clúster, asegúrese de eliminar el repositorio /clustered.txt del nodo principal.
* Asegúrese de que el nodo principal se inicie primero y, después de que esté activo, inicie otros nodos.

### Restauración de todo el clúster {#restoring-the-entire-cluster}

1. Detenga todos los nodos del clúster.
1. Vuelva a crear el sistema físico a partir de una imagen del sistema.
1. Aplique parches o actualizaciones a AEM formularios AEM aplicados desde que se hizo la imagen. Esta información se registró en el paso 1 del procedimiento de copia de seguridad. AEM formularios deben recuperarse al mismo nivel de parche que cuando se realizó la copia de seguridad del sistema.
1. Restaure la base de datos, GDS y conectores.
1. Haga lo siguiente para recuperar el repositorio AEM sin conexión:

   >[!NOTE]
   >
   >Si una copia de seguridad comprimida del repositorio crx se ha conectado, descomprima el archivo en cualquier ubicación y siga el proceso de restauración sin conexión.

   1. En todos los nodos del clúster, elimine los directorios del repositorio, compartido, versión y espacio de trabajo en el directorio clusterNode .
   1. Elimine todos los archivos y directorios del directorio compartido.
   1. Restaure la copia de seguridad del nodo del clúster (incluidos los subdirectorios) en un nodo del clúster.
   1. Copie todos los archivos del nodo de clúster restaurado a todos los demás nodos de clúster. Una vez finalizado, cada nodo de clúster contiene los mismos datos.
   1. Elimine el archivo clusterNode/revision.log en todos los nodos del clúster.
   1. Elimine el .lock en todos los nodos del clúster, si existe.
   1. Elimine repository/system.id todos los nodos del clúster, si existe.
   1. Elimine los archivos &amp;ast;&amp;ast;/listener.properties en todos los nodos del clúster, si existen.
   1. Restaure repository/cluster_node.id para nodos de clúster individuales.

>[!NOTE]
>
>Consideremos los siguientes puntos:

* Si el nodo en el que se produjo el error era un nodo primario AEM, copie todo el contenido de la carpeta del repositorio secundario (se parece a crx-repository\crx.0000 donde 000 puede ser cualquier dígito) en la carpeta del repositorio crx-repository\.
* Antes de reiniciar cualquier nodo de clúster, asegúrese de eliminar el repositorio /clustered.txt del nodo principal.
* Asegúrese de que el nodo principal se inicie primero y, después de que esté activo, inicie otros nodos.

## Hacer una copia de seguridad y restaurar el nodo de publicación de la solución Gestión de correspondencia {#back-up-and-restore-correspondence-management-solution-publish-node}

El nodo editor no tiene ninguna relación principal-secundaria en un entorno agrupado. Puede realizar una copia de seguridad de cualquier nodo de Publisher siguiendo las instrucciones siguientes [Copia de seguridad y restauración](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### Recuperar un solo nodo de editor {#recover-a-single-publisher-node}

1. Cierre el nodo que debe recuperarse y no realice ninguna actividad de publicación hasta que el nodo vuelva a estar activo.
1. Restaure el nodo Publicar mediante [Restauración de la copia de seguridad](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### Recuperar un clúster {#recover-a-cluster}

1. Cierre el clúster.
1. Restaure el nodo Publicar mediante [Restauración de la copia de seguridad](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).
1. Inicie el nodo principal seguido del nodo secundario del clúster de creación.
