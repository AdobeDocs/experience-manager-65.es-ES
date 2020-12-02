---
title: Estrategia para backup y restore en un entorno agrupado
seo-title: Estrategia para backup y restore en un entorno agrupado
description: Si la implementación de formularios AEM almacena datos personalizados adicionales en una base de datos diferente, debe implementar una estrategia para realizar una copia de seguridad de estos datos, asegurándose de que se mantengan sincronizados con los datos de formularios AEM.
seo-description: Si la implementación de formularios AEM almacena datos personalizados adicionales en una base de datos diferente, debe implementar una estrategia para realizar una copia de seguridad de estos datos, asegurándose de que se mantengan sincronizados con los datos de formularios AEM.
uuid: c29b989c-30ed-4a8e-bab8-9b7746291a33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c332985b-4556-4056-961a-fce2356da88d
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 0%

---


# Estrategia para backup y restore en un entorno en clúster {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>Si la implementación de formularios AEM almacena datos personalizados adicionales en una base de datos diferente, debe implementar una estrategia para realizar una copia de seguridad de estos datos, asegurándose de que se mantengan sincronizados con los datos de formularios AEM. Además, la aplicación debe diseñarse de modo que sea lo suficientemente robusta como para gestionar un escenario en el que las bases de datos adicionales no estén sincronizadas. Se recomienda encarecidamente que cualquier operación de base de datos que se realice se realice en el contexto de una transacción para ayudar a mantener un estado coherente.

Debe realizar una copia de seguridad de las siguientes partes del sistema de formularios AEM para recuperarse de cualquier error:

* Base de datos utilizada por AEM formularios
* GDS con datos de larga duración y otros documentos persistentes
* Base de datos AEM (crx-repositorio)

>[!NOTE]
>
>Debe realizar una copia de seguridad de cualquier otro dato que esté utilizando la configuración de formularios AEM, como fuentes de cliente, datos de conectores, etc.

## Realice una copia de seguridad de un entorno en clúster {#back-up-a-clustered-environment}

En este tema se analizan las siguientes estrategias para realizar copias de seguridad de cualquier entorno agrupado de formularios AEM:

* Backup sin conexión con tiempo de inactividad
* Backup sin conexión sin tiempo de inactividad (copia de seguridad de un nodo secundario que está apagado)
* Backup en línea sin downtime pero con retraso en la respuesta
* Realizar una copia de seguridad del archivo de propiedades del Bootstrap

### Backup sin conexión con tiempo de inactividad {#offline-backup-with-downtime}

1. Cierre todo el clúster y los servicios relacionados. (consulte [Inicio y parada de servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. En cualquier nodo, realice una copia de seguridad de la base de datos, GDS y Conectores. (consulte [Archivos para realizar copias de seguridad y recuperar](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Realice los siguientes pasos para realizar copias de seguridad AEM repositorio sin conexión:

   1. Para cada nodo de clúster, haga una copia de seguridad del archivo que contiene el identificador del nodo de clúster.
   1. Realice una copia de seguridad de todos los archivos de cualquier nodo de clúster secundario, incluidos los subdirectorios.
   1. Haga una copia de seguridad del identificador del sistema/repositorio de cada nodo de clúster por separado.

   Para ver los pasos detallados, consulte [Backup y restauración](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html).

1. Realice una copia de seguridad de cualquier otro dato, como las fuentes del cliente.
1. Vuelva a poner en inicio el clúster.

### Backup sin conexión sin downtime {#offline-backup-with-no-downtime}

1. Introduzca el modo de copia de seguridad móvil. (consulte [Introducción de los modos de copia de seguridad](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   Tenga en cuenta que tenemos que dejar el modo de copia de seguridad móvil después de una recuperación.

1. Cierre cualquiera de los nodos secundarios del clúster con respecto a AEM. (consulte [Inicio y parada de servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. En cualquier nodo, realice una copia de seguridad de la base de datos, GDS y Conectores. (consulte [Archivos para realizar copias de seguridad y recuperar](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Realice los siguientes pasos para realizar copias de seguridad AEM repositorio sin conexión:

   1. Para cada nodo de clúster, haga una copia de seguridad del archivo que contiene el identificador del nodo de clúster.
   1. Realice una copia de seguridad de todos los archivos de cualquier nodo de clúster secundario, incluidos los subdirectorios.
   1. Realice una copia de seguridad de repository/system.id de cada nodo de clúster por separado.

   Para ver los pasos detallados, consulte [Backup y restauración](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html).

1. Realice una copia de seguridad de cualquier otro dato, como las fuentes del cliente.
1. Vuelva a poner en inicio el clúster.

### Backup en línea sin downtime pero con retraso en la respuesta {#online-backup-with-no-downtime-but-delay-in-response}

1. Introduzca el modo de copia de seguridad móvil. (consulte [Introducción de los modos de copia de seguridad](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   Tenga en cuenta que debe dejar el modo de copia de seguridad móvil después de una recuperación.

1. Cierre cualquiera de los nodos secundarios del clúster con respecto a AEM. (consulte [Inicio y parada de servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. En cualquier nodo, realice una copia de seguridad de la base de datos, GDS y Conectores. (consulte [Archivos para realizar copias de seguridad y recuperar](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Realice los siguientes pasos para realizar copias de seguridad AEM repositorio en línea:

   1. Para cada nodo de clúster, realice una copia de seguridad del archivo que contiene el cluster_node.id.
   1. Realice una copia de seguridad de repository/system.id de cada nodo de clúster por separado.
   1. En cualquier nodo secundario, realice una copia de seguridad en línea del repositorio para ver los pasos detallados en Copia de seguridad en línea.

1. Realice una copia de seguridad de cualquier otro dato, como las fuentes del cliente.
1. Vuelva a poner en inicio el clúster.

### Realice una copia de seguridad del archivo de propiedades del Bootstrap {#back-up-the-bootstrap-properties-file}

Cuando se crea un clúster de AEM, se crea un archivo de propiedades en el servidor de aplicaciones para todos los nodos secundarios. Se recomienda realizar una copia de seguridad del archivo de propiedades del Bootstrap. Puede encontrar el archivo en la siguiente ubicación del servidor de aplicaciones:

* JBoss: en el directorio BIN
* WebLogic: en el directorio de dominios
* WebSphere: en el directorio de perfil

Debe realizar una copia de seguridad del archivo para el escenario de recuperación ante desastres de AEM nodo secundario y reemplazarlo en la ubicación especificada en el servidor de aplicaciones, si se restaura.

## Recuperación en un entorno en clúster {#recovery-in-a-clustered-environment}

En caso de que se produzca un error en todo el clúster o en un solo nodo, deberá restaurarlo mediante la copia de seguridad.

Para una recuperación de un solo nodo, solo tiene que cerrar el nodo único y ejecutar el procedimiento de recuperación de un solo nodo.

Si todo el clúster falla debido a errores como el bloqueo de la base de datos, debe realizar los siguientes pasos. La restauración depende del método de backup utilizado.

### Restauración de un solo nodo {#restoring-a-single-node}

1. Detenga el nodo dañado.

   >[!NOTE]
   >
   >Si el nodo dañado es un nodo primario AEM, cierre todo el nodo del clúster.

1. Vuelva a crear el sistema físico a partir de una imagen del sistema.
1. Aplique parches o actualizaciones a AEM formularios que se aplicaron desde que se creó la imagen. Esta información se registró durante el procedimiento de copia de seguridad. AEM formularios deben recuperarse al mismo nivel de parche que cuando se realizó la copia de seguridad del sistema.
1. (*Opcional*) Si todos los demás nodos funcionan correctamente, es posible que el repositorio de AEM también esté dañado. En este caso, verá un mensaje unsync del repositorio en el archivo error.log del repositorio de AEM.

   Para restaurar el repositorio, realice los siguientes pasos.

   >[!NOTE]
   >
   >Si una copia de seguridad compactada del repositorio crx se puso en línea, descomprímalo en cualquier ubicación y siga el proceso de restauración sin conexión.

   1. Elimine los directorios de repositorio, compartido, versión y espacios de trabajo en el directorio clusterNode del nodo.
   1. Restaure la copia de seguridad del nodo del clúster (incluidos los subdirectorios) en el nodo.
   1. Elimine el archivo clusterNode/revision.log en el nodo.
   1. Elimine el .lock en el nodo, si existe.
   1. Elimine el repository/system.id del nodo, si existe.
   1. Elimine los archivos &amp;ast;&amp;ast;/listener.properties en el nodo, si existe.
   1. Restaure repository/cluster_node.id para nodos de clúster individuales.

>[!NOTE]
>
>Considere los siguientes puntos:

* Si el nodo con error era un nodo primario AEM, copie todo el contenido de la carpeta del repositorio secundario (crx-repository\crx.0000 donde 0000 puede ser cualquier dígito) en la carpeta crx-repository\ repositorio y elimine la carpeta del repositorio secundario.
* Antes de reiniciar cualquier nodo de clúster, asegúrese de eliminar el repositorio /clustered.txt del nodo principal.
* Asegúrese de que el nodo principal se inicia primero y, una vez que se ha activado completamente, inicio otros nodos.

### Restaurando todo el clúster {#restoring-the-entire-cluster}

1. Detenga todos los nodos del clúster.
1. Volver a crear el sistema físico a partir de una imagen del sistema.
1. Aplicar parches o actualizaciones a formularios AEMFormularios AEM aplicados desde que se creó la imagen. Esta información se registró en el paso 1 del procedimiento de copia de seguridad. AEM formularios deben recuperarse al mismo nivel de parche que cuando se realizó la copia de seguridad del sistema.
1. Restaure la base de datos, GDS y Conectores.
1. Haga lo siguiente para recuperar el repositorio de AEM sin conexión:

   >[!NOTE]
   >
   >Si una copia de seguridad compactada del repositorio crx se puso en línea, descomprímalo en cualquier ubicación y siga el proceso de restauración sin conexión.

   1. En todos los nodos de clúster, elimine los directorios de repositorio, compartido, versión y espacios de trabajo en el directorio clusterNode.
   1. Elimine todos los archivos y directorios del directorio compartido.
   1. Restaure la copia de seguridad del nodo de clúster (incluidos los subdirectorios) en un nodo de clúster.
   1. Copie todos los archivos del nodo de clúster restaurado en todos los demás nodos de clúster. Una vez finalizado, cada nodo de clúster contiene los mismos datos.
   1. Elimine el archivo clusterNode/revision.log en todos los nodos del clúster.
   1. Elimine el .lock en todos los nodos del clúster, si existe.
   1. Elimine repository/system.id todos los nodos de clúster, si existe.
   1. Elimine los archivos &amp;ast;&amp;ast;/listener.properties en todos los nodos del clúster, si existen.
   1. Restaure repository/cluster_node.id para nodos de clúster individuales.

>[!NOTE]
>
>Considere los siguientes puntos:

* Si el nodo con error era un nodo primario AEM, copie todo el contenido de la carpeta del repositorio secundario (parece crx-repository\crx.0000, donde 0000 puede ser cualquier dígito) en la carpeta crx-Repository\.
* Antes de reiniciar cualquier nodo de clúster, asegúrese de eliminar el repositorio /clustered.txt del nodo principal.
* Asegúrese de que el nodo principal se inicia primero y, una vez que se ha activado completamente, inicio otros nodos.

## Haga una copia de seguridad y restaure el nodo de publicación {#back-up-and-restore-correspondence-management-solution-publish-node} de Correspondence Management Solution

El nodo editor no tiene ninguna relación primaria-secundaria en un entorno agrupado. Puede realizar una copia de seguridad de cualquier nodo de Publisher siguiendo [Backup y Restore](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html).

### Recuperar un solo nodo de editor {#recover-a-single-publisher-node}

1. Cierre el nodo que debe recuperarse y no realice ninguna actividad de publicación hasta que el nodo vuelva a activarse.
1. Restaure el nodo Publicar mediante [Restauración de la copia de seguridad](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring de la copia de seguridad).

### Recuperar un clúster {#recover-a-cluster}

1. Cierre el clúster.
1. Restaure el nodo Publicar mediante [Restauración de la copia de seguridad](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring de la copia de seguridad).
1. Inicio el nodo principal seguido del nodo secundario del clúster de creación.

