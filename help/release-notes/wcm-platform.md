---
title: AEM Foundation y repositorio
description: Notas de versión específicas de la plataforma y repositorio de Adobe Experience Manager 6.3 AEM.
uuid: 70626eda-c514-44bd-9f28-ff7abdc22f53
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 66ecf4c5-6d0f-4586-880d-7d1c8a5a5614
docset: aem65
translation-type: tm+mt
source-git-commit: 4dc4a518c212555b7833ac27de02087a403d3517

---


# AEM Foundation y repositorio{#aem-foundation-repository}

## Lista de cambios {#list-of-changes}

### Repositorio {#repository}

* Adobe Experience Manager 6.5 se basa en versiones actualizadas de la arquitectura creada a partir de OSGi (Apache Sling y Apache Felix) y el repositorio de contenido Java: Apache Jackrabbit Oak 1.10.2.
* Please see [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) and [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt) for a full overview of fixed issues.

>[!CAUTION]
>
>* La nueva versión de Oak Segment Tar disponible a partir de la versión 6.3 de AEM requiere realizar una migración del repositorio. Este paso es obligatorio si está actualizando desde una versión anterior de TarMK o desea cambiar la nueva barra de segmentos de otro tipo de persistencia. For more information on what the benefits of the new Segment Tar are, see the [Migrating to Oak Segment Tar FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).
>



### Compatibilidad con Java {#java-support}

* Nueva compatibilidad con Java 11, así como para Java 8
* Para obtener un rendimiento óptimo, anule los valores GC predeterminados con otros valores. Para obtener más información, consulte la sección [Instalar y actualizar](/help/sites-deploying/custom-standalone-install.md).
* Adobe distribuirá las actualizaciones de mantenimiento de Java 11 y Java 8 para que el cliente pueda usarlas en proyectos relacionados con AEM, cuando estas no estén disponibles públicamente en Oracle

### OSGI {#osgi}

* Se agregaron las bibliotecas de utilidades de OSGi Promises y Converter

### Proyectos y flujos de trabajo {#projects-and-workflows}

* El nuevo editor del modelo de flujo de trabajo introducido en la versión 6.4 se ha mejorado para incluir más operaciones, como copiar y publicar, la compatibilidad con variables en los pasos de flujo de trabajo y las mejoras en las divisiones OR y AND.

### Búsqueda {#searching}

* La búsqueda en Oak ahora admite facetas dinámicas. Por ejemplo: el carril de filtro en la búsqueda de recursos muestra la cantidad estimada de resultados.
* QueryBuilder se ha ampliado para proporcionar resultados con facetas dinámicas

### Seguridad {#security}

* Se agregó la caducidad de la contraseña para el usuario administrador.

### Interfaz de usuario {#user-interface}

Se han realizado varias mejoras en la interfaz de usuario para que sea más productiva y fácil de usar.

* AEM 6.5 presenta una nueva interfaz de usuario de administración de permisos para usuarios y grupos que facilita la visualización y configuración de todo el conjunto de privilegios y restricciones sin tener que acceder a CRXDE.
* Las vistas de columna ahora solo cargan las entradas que son visibles en la pantalla y solo cargarán más cuando el usuario comience a desplazarse por el documento. Las vistas de lista y de tarjeta se incluyen a partir de la versión 6.0 (mejoradas en la versión 6.4)
* Las vistas de columna ahora incluyen el estado del flujo de trabajo para las páginas y recursos, cuando corresponda
* La acción Seleccionar todo es una forma rápida de ejecutar una acción en todas las páginas o recursos de la misma carpeta
* La acción Seleccionar todo intenta realizar la acción en todas las páginas o activos, no solo en el contenido cargado. Si la acción no se ha actualizado para administrar acciones en bloque, se mostrará un cuadro de diálogo de advertencia

>[!CAUTION]
>
>* Adobe no tiene previsto realizar más mejoras en la interfaz de usuario clásica. AEM 6.5 tiene la interfaz de usuario clásica incluida y los clientes que actualicen desde versiones anteriores pueden seguir utilizándola. Note that Classic UI remains fully supported while being deprecated [Read more](/help/sites-deploying/ui-recommendations.md).
>



### Actualización {#upgrade}

* El procedimiento de actualización es el mismo en la versión 6.5.
* Adobe admite las funciones de compatibilidad retroactiva, de evaluación de la complejidad de las actualizaciones y las actualizaciones sostenibles introducidas en la versión 6.4. Se han realizado actualizaciones específicas de la versión en las áreas en las que era necesario.
* Se ha simplificado el paquete del detector de patrones y habrá un paquete que evaluará las actualizaciones a la versión 6.5 para las versiones de origen disponibles.
* Please see the [Upgrade documentation](/help/sites-deploying/upgrade.md) for more details on upgrade procedure.

### Servidor web {#web-server}

* La distribución Quickstart utiliza Eclipse Jetty 9.4.15 como motor servlet (AEM 6.4 enviado con 9.3.22)

