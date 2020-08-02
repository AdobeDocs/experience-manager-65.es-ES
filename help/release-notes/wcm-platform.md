---
title: Base de AEM y repositorio
description: Notas de la versión para la plataforma y el repositorio de Adobe Experience Manager.
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 56%

---


# Base de AEM y repositorio {#aem-foundation-repository}

## Lista de cambios {#list-of-changes}

### Repositorio {#repository}

* Adobe Experience Manager 6.5 se basa en versiones actualizadas de la arquitectura creada a partir de OSGi (Apache Sling y Apache Felix) y el repositorio de contenido Java: Apache Jackrabbit Oak 1.10.2.
* Para obtener información general sobre los problemas solucionados, consulte [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) y [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>La nueva versión de Oak Segment Tar disponible a partir de la versión 6.3 de AEM requiere realizar una migración del repositorio. Este paso es obligatorio si está actualizando desde una versión anterior de TarMK o desea cambiar la nueva barra de segmentos de otro tipo de persistencia. For more information on what the benefits of the new Segment Tar are, see the [Migrating to Oak Segment Tar FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

### Compatibilidad con Java {#java-support}

* Nueva compatibilidad con Java 11, así como para Java 8.
* Para obtener un rendimiento óptimo, anule los valores GC predeterminados con otros valores. Para obtener más información, consulte la sección [Instalar y actualizar](/help/sites-deploying/custom-standalone-install.md).
* Las actualizaciones de mantenimiento de Java 11 y Java 8 se distribuyen por Adobe para el uso del cliente en proyectos relacionados con AEM, cuando no están disponibles públicamente desde Oracle.

### OSGI {#osgi}

* Bibliotecas de utilidades Añadidas OSGi Promises y Converter.

### Proyectos y flujos de trabajo {#projects-and-workflows}

* New Workflow Model editor introduced in 6.4 has been improved to include more operations like Copy and Publish, Variable support in Workflow steps and enhanced `OR` and `AND` splits.

### Búsqueda {#searching}

* La búsqueda en Oak ahora admite facetas dinámicas. Por ejemplo: el carril de filtro en la búsqueda de recursos muestra la cantidad estimada de resultados.
* QueryBuilder se ha ampliado para proporcionar resultados con facetas dinámicas.

### Seguridad {#security}

* Se agregó la caducidad de la contraseña para el usuario administrador.

### Interfaz de usuario {#user-interface}

Se han realizado varias mejoras en la interfaz de usuario para que sea más productiva y fácil de usar.

* AEM 6.5 presenta una nueva interfaz de usuario de administración de permisos para usuarios y grupos que facilita la visualización y configuración de todo el conjunto de privilegios y restricciones sin tener que acceder a CRXDE.
* Las vistas de columna ahora solo cargan las entradas que son visibles en la pantalla y solo cargarán más cuando el usuario comience a desplazarse por el documento. Las vistas de lista y de tarjeta se incluyen a partir de la versión 6.0 (mejoradas en la versión 6.4).
* Las vistas de columna ahora incluyen el estado del flujo de trabajo para las páginas y recursos, cuando corresponda.
* La acción Seleccionar todo es una forma rápida de ejecutar una acción en todas las páginas o recursos de la misma carpeta.
* La acción Seleccionar todo intenta realizar la acción en todas las páginas o recursos, no solo en el contenido cargado. Si la acción no se actualiza para gestionar acciones masivas, se muestra una advertencia.

>[!CAUTION]
>
>Adobe no realizará más mejoras en la IU clásica. Experience Manager 6.5 incluye la IU clásica para la compatibilidad con versiones anteriores. Classic UI remains fully supported while being deprecated [Read more](/help/sites-deploying/ui-recommendations.md).

### Actualización {#upgrade}

* El procedimiento de actualización es el mismo en la versión 6.5.
* Adobe admite las funciones de compatibilidad retroactiva, de evaluación de la complejidad de las actualizaciones y las actualizaciones sostenibles introducidas en la versión 6.4. Se han realizado actualizaciones específicas de la versión en las áreas en las que era necesario.
* Se ha simplificado el paquete del detector de patrones y habrá un paquete que evaluará las actualizaciones a la versión 6.5 para las versiones de origen disponibles.
* Para obtener más información sobre el procedimiento de actualización, consulte la documentación [de](/help/sites-deploying/upgrade.md)actualización.

### Servidor web {#web-server}

* La distribución Quickstart utiliza Eclipse Jetty 9.4.15 como motor servlet (AEM 6.4 enviado con 9.3.22).
