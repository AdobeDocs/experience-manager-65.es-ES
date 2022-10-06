---
title: Procedimiento de actualización
seo-title: Upgrade Procedure
description: Obtenga información sobre el procedimiento que debe seguir para actualizar AEM.
seo-description: Learn about the procedure you need to follow in order to upgrade AEM.
uuid: 81126a70-c082-4f01-a1ad-7152182da88b
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 5c035d4c-6e03-48b6-8404-800b52d659b8
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: 5242600c-2281-46f9-a347-d985b4e319b3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# Procedimiento de actualización {#upgrade-procedure}

>[!NOTE]
>
>La actualización requerirá tiempo de inactividad para el nivel de Author, ya que la mayoría de las actualizaciones de AEM se realizan in situ. Siguiendo estas prácticas recomendadas, el tiempo de inactividad del nivel de publicación se puede minimizar o eliminar.

Al actualizar los entornos de AEM, debe tener en cuenta las diferencias de enfoque entre la actualización de entornos de autor o los entornos de publicación para minimizar el tiempo de inactividad tanto para los autores como para los usuarios finales. Esta página describe el procedimiento de alto nivel para actualizar una topología de AEM que actualmente se ejecuta en una versión de AEM 6.x. Dado que el proceso difiere entre los niveles de autor y publicación, así como las implementaciones basadas en Mongo y TarMK, cada nivel y micronúcleo se ha incluido en una sección separada. Al ejecutar la implementación, se recomienda primero actualizar el entorno de creación, determinar el éxito y, a continuación, avanzar a los entornos de publicación.

<!--
>[!IMPORTANT]
>
>The downtime during the upgrade can be significally reduced by indexing the repository before performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)
-->

## Nivel de Author de TarMK {#tarmk-author-tier}

### Topología de inicio {#starting-topology}

La topología asumida para esta sección consiste en un servidor Autor que se ejecuta en TarMK con un modo de espera pasiva. La replicación se produce desde el servidor Autor al conjunto de servidores de publicación TarMK. Aunque no se ilustra aquí, este enfoque también se puede aprovechar para implementaciones que utilizan descarga. Asegúrese de actualizar o reconstruir la instancia de descarga en la nueva versión después de deshabilitar los agentes de replicación en la instancia de autor y antes de volver a activarlos.

![tarmk_started_topología](assets/tarmk_starting_topology.jpg)

### Preparación de la actualización {#upgrade-preparation}

![upgrade-preparation-author](assets/upgrade-preparation-author.png)

1. Detener la creación de contenido

1. Detener la instancia de espera

1. Deshabilitar agentes de replicación en el autor

1. Ejecute el [tareas de mantenimiento previas a la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md).

### Ejecución de la actualización {#upgrade-execution}

![execute_upgrade](assets/execute_upgrade.jpg)

1. Ejecute el [actualización in situ](/help/sites-deploying/in-place-upgrade.md)
1. Actualización del módulo de Dispatcher *si es necesario*

1. El control de calidad valida la actualización

1. Cierre la instancia de autor.

### Si se realiza correctamente {#if-successful}

![if_success](assets/if_successful.jpg)

1. Copie la instancia actualizada para crear un nuevo modo de espera pasiva

1. Iniciar la instancia de autor

1. Inicie la instancia de espera.

### Si No Se Ha Realizado Correctamente (Reversión) {#if-unsuccessful-rollback}

![rollback](assets/rollback.jpg)

1. Inicie la instancia de espera pasiva como el nuevo primario

1. Reconstruya el entorno Autor desde el modo de espera pasiva.

## Clúster de autor de MongoMK {#mongomk-author-cluster}

### Topología de inicio {#starting-topology-1}

La topología asumida para esta sección consiste en un clúster de Autor MongoMK con al menos dos instancias de Autor AEM, respaldadas por al menos dos bases de datos MongoMK. Todas las instancias de Autor comparten un almacén de datos. Estos pasos deben aplicarse a los almacenes de datos S3 y File. La replicación se produce desde los servidores Author al conjunto de servidores de publicación TarMK.

![mongo-topología](assets/mongo-topology.jpg)

### Preparación de la actualización {#upgrade-preparation-1}

![mongo-upgrade_prep](assets/mongo-upgrade_prep.jpg)

1. Detener la creación de contenido
1. Clonar el almacén de datos para la copia de seguridad
1. Detenga todas las instancias excepto una de AEM Author, su Autor principal
1. Elimine todos los nodos MongoDB excepto uno del conjunto de réplicas, su instancia principal de Mongo
1. Actualice el `DocumentNodeStoreService.cfg` en el Autor principal para reflejar su conjunto de réplicas de miembro único
1. Reinicie el Autor principal para asegurarse de que se reinicia correctamente
1. Deshabilitar agentes de replicación en el Autor principal
1. Ejecutar [tareas de mantenimiento previas a la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) en la instancia principal de Autor
1. Si es necesario, actualice MongoDB en la instancia principal de Mongo a la versión 3.2 con WiredTiger

### Ejecución de la actualización {#Upgrade-execution-1}

![mongo-execution](assets/mongo-execution.jpg)

1. Ejecute un [actualización in situ](/help/sites-deploying/in-place-upgrade.md) en el Autor principal
1. Actualizar el Dispatcher o el módulo web *si es necesario*
1. El control de calidad valida la actualización

### Si se realiza correctamente {#if-successful-1}

![mongo-secundario](assets/mongo-secondaries.jpg)

1. Crear nuevas instancias de autor 6.5, conectadas a la instancia actualizada de Mongo

1. Reconstruya los nodos MongoDB que se eliminaron del clúster

1. Actualice el `DocumentNodeStoreService.cfg` archivos para reflejar el conjunto completo de réplicas

1. Reinicie las instancias de autor de una en una

1. Elimine el almacén de datos clonado.

### Si No Se Ha Realizado Correctamente (Reversión)  {#if-unsuccessful-rollback-2}

![mongo-rollback](assets/mongo-rollback.jpg)

1. Vuelva a configurar las instancias secundarias de Autor para conectarse al almacén de datos clonado

1. Apague la instancia principal de Author actualizada

1. Cierre la instancia principal actualizada de Mongo.

1. Inicie las instancias secundarias de Mongo con una de ellas como la nueva instancia principal

1. Configure las variables `DocumentNodeStoreService.cfg` archivos en las instancias de autor secundarias para señalar al conjunto de réplicas de instancias de Mongo aún no actualizadas

1. Inicie las instancias secundarias de Autor

1. Limpie las instancias de autor actualizadas, el nodo Mongo y el almacén de datos.

## Granja de publicación TarMK {#tarmk-publish-farm}

### Granja de publicación TarMK {#tarmk-publish-farm-1}

La topología asumida para esta sección consiste en dos instancias de publicación de TarMK, frontadas por Dispatchers que a su vez están frontadas por un equilibrador de carga. La replicación se produce desde el servidor Autor al conjunto de servidores de publicación TarMK.

![tarmk-pub-Farmv5](assets/tarmk-pub-farmv5.png)

### Ejecución de la actualización {#upgrade-execution-2}

![upgrade-publish2](assets/upgrade-publish2.png)

1. Detenga el tráfico a la instancia Publicar 2 en el equilibrador de carga
1. Ejecutar [mantenimiento previo a la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) en Publish 2
1. Ejecute un [actualización in situ](/help/sites-deploying/in-place-upgrade.md) en Publish 2
1. Actualizar el Dispatcher o el módulo web *si es necesario*
1. Vaciar la caché de Dispatcher
1. El control de calidad valida la publicación 2 a través de Dispatcher, detrás del cortafuegos
1. Cerrar publicación 2
1. Copiar la instancia de Publish 2
1. Iniciar publicación 2

### Si se realiza correctamente {#if-successful-2}

![upgrade-publish1](assets/upgrade-publish1.png)

1. Habilitar el tráfico en Publish 2
1. Detener el tráfico en la publicación 1
1. Detenga la instancia Publish 1
1. Reemplace la instancia Publish 1 con una copia de Publish 2
1. Actualizar el Dispatcher o el módulo web *si es necesario*
1. Vaciar la caché de Dispatcher para la publicación 1
1. Iniciar publicación 1
1. El control de calidad valida la publicación 1 a través de Dispatcher, detrás del cortafuegos

### Si No Se Ha Realizado Correctamente (Reversión) {#if-unsuccessful-rollback-1}

![pub_rollback](assets/pub_rollback.jpg)

1. Crear una copia de Publish 1
1. Reemplace la instancia Publish 2 con una copia de Publish 1
1. Vaciar la caché de Dispatcher para la publicación 2
1. Iniciar publicación 2
1. El control de calidad valida la publicación 2 a través de Dispatcher, detrás del cortafuegos
1. Habilitar el tráfico en Publish 2

## Pasos finales de la actualización {#final-upgrade-steps}

1. Habilitar el tráfico para la publicación 1
1. El control de calidad realiza la validación final desde una dirección URL pública
1. Habilitar agentes de replicación desde el entorno de Author
1. Reanudar la creación de contenido
1. Realizar [comprobaciones posteriores a la actualización](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).

![final](assets/final.jpg)
