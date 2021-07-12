---
title: Selección de un tipo de persistencia para una instalación de AEM Forms
seo-title: Selección de un tipo de persistencia para una instalación de AEM Forms
description: Elija un tipo de persistencia con sabiduría. Le ayuda a crear un entorno de AEM Forms eficiente y escalable.
seo-description: Elija un tipo de persistencia con sabiduría. Le ayuda a crear un entorno AEM Forms eficiente y escalable.
uuid: 1c692502-5039-4757-9358-1772772b3904
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: a972fb35-38a7-4b83-99bd-6a6dddf8043b
role: Admin
exl-id: 621fe107-f4ac-42b1-8c7b-8abbcaac7380
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---

# Selección de un tipo de persistencia para una instalación de AEM Forms {#choosing-a-persistence-type-for-an-aem-forms-installation}

Elija un tipo de persistencia con sabiduría. Le ayuda a crear un entorno de AEM Forms eficiente y escalable.

La persistencia es el método para almacenar contenido en los almacenes físicos. Define la estructura de datos real y el mecanismo de almacenamiento de los datos. Los microkernels actúan como gestores de persistencia en AEM Forms. AEM Forms admite persistencia (MicroKernals) de tipo TarMK, MongoMK y RDBMK. Puede elegir un tipo de persistencia para AEM Forms según el propósito y el tipo de implementación (un solo servidor, una granja o un clúster) de una instancia de AEM Forms.

>[!NOTE]
>
>LiveCycle ES4 SP1 utiliza la persistencia TarPM para almacenar contenido.

La tabla siguiente muestra todos los tipos de persistencia admitidos, así como varios parámetros que le ayudarán a elegir un tipo de persistencia para su entorno:

<table>
 <tbody>
  <tr>
   <th><strong>Tipo de instalación/costo</strong></th>
   <th><strong>TarMK</strong></th>
   <th><strong>MongoMk</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>Configuración independiente</strong></th>
   <td>Compatible<br /> </td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <th><strong>Configuración del clúster</strong></th>
   <td>No compatible</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <th><strong>Costo de licencia</strong></th>
   <td>Incluido con AEM </td>
   <td>Licencia separada requerida</td>
   <td>Licencia separada requerida</td>
  </tr>
 </tbody>
</table>

TarMK está diseñado para el rendimiento, mientras que MongoMK y RDBMK están diseñados para la escalabilidad. Adobe recomienda encarecidamente TarMK como tecnología de persistencia predeterminada para todos los escenarios de implementación de AEM Forms, tanto para instancias de Autor como de Publicación, excepto en los casos de uso descritos en la sección [Elección de Mongo o de un micronúcleo de base de datos relacional sobre TarMK](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p).

Para obtener la lista de microkernels compatibles, consulte los artículos [AEM Forms on OSGi Technical Requirements](/help/sites-deploying/technical-requirements.md) o [AEM Forms on JEE supported platform grouping](/help/forms/using/aem-forms-jee-supported-platforms.md).

## Elección de Mongo o un Microkernel de Base de Datos Relacional sobre TarMK {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

Un entorno de AEM Forms escalable (agrupado) es un conjunto de dos o más instancias de autor activas configuradas horizontalmente. Puede optar por ejecutar más de una instancia de autor si un solo servidor, que admita todas las actividades de creación concurrentes, ya no es sostenible.

Solo se admite el tipo de persistencia MongoMK y RDBMK para un AEM Forms escalable (agrupado) en un entorno JEE. La cantidad de servidores o el tamaño del entorno escalable varía según la instalación. Para obtener una lista de consideraciones y ejemplos, consulte el artículo [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md) o [Arquitectura y topologías de implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md). También puede ponerse en contacto con el servicio de asistencia de AEM Forms para obtener información detallada sobre la planificación de la capacidad de AEM Forms con RDBMK y TarMK.
