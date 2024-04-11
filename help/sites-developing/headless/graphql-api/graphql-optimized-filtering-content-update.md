---
title: Actualización de los fragmentos de contenido para el filtrado optimizado de GraphQL
description: Obtenga información sobre cómo actualizar los fragmentos de contenido para el filtrado optimizado de GraphQL en Adobe Experience Manager para la entrega de contenido sin encabezado.
exl-id: d78ec052-c091-49ca-9f36-a3d24eb9edd5
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 37%

---

# Actualización de los fragmentos de contenido para el filtrado optimizado de GraphQL {#updating-content-fragments-for-optimized-graphql-filtering}

Para optimizar el rendimiento de los filtros de GraphQL, ejecute un procedimiento para actualizar los fragmentos de contenido.

>[!NOTE]
>
>Después de actualizar los fragmentos de contenido, puede seguir las recomendaciones de [Optimización de consultas de GraphQL](/help/sites-developing/headless/graphql-api/graphql-optimization.md).

## Requisitos previos {#prerequisites}

AEM Asegúrese de que tiene un mínimo de 6.5.17.0 de la versión de.

## Actualización de los fragmentos de contenido {#updating-content-fragments}

Para ejecutar el procedimiento, siga estos pasos:

1. [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para el **Configuración del trabajo de migración de fragmentos de contenido**:

   ![Configuración del trabajo de migración de fragmentos de contenido OSGi](assets/cfm-graphql-update-01.png "Configuración del trabajo de migración de fragmentos de contenido OSGi")

1. En el cuadro de diálogo, establezca estos dos parámetros de la siguiente manera:

   * **ContentFragmentMigration:Enabled** : `1`
   * **ContentFragmentMigration:Aplicar** : `1`

1. **Guardar** las especificaciones: se inicia el procedimiento de actualización.

1. Espere hasta que se complete el procedimiento. El procedimiento se completa cuando la propiedad `cfGlobalVersion` aparece en `/content/dam` y se establece en `1`.

1. Vuelva a la configuración de OSGi para desactivar el procedimiento.

   En el cuadro de diálogo de **Configuración del trabajo de migración de fragmentos de contenido** establezca estos dos parámetros de la siguiente manera:

   * **ContentFragmentMigration:Enabled** : `0`
   * **ContentFragmentMigration:Aplicar** : `0`

## Restricciones {#limitations}

Tenga en cuenta las siguientes limitaciones:

* Optimizar el rendimiento de los filtros de GraphQL solo será posible después de una actualización completa de todos los fragmentos de contenido (indicada por la presencia de la propiedad `cfGlobalVersion` para el nodo JCR `/content/dam`).

* Si los fragmentos de contenido se importan desde un paquete de contenido (mediante `crx/de`) después de ejecutar el procedimiento de actualización, esos fragmentos de contenido no se tendrán en cuenta en los resultados de la consulta de GraphQL hasta que se vuelva a ejecutar el procedimiento de actualización.
