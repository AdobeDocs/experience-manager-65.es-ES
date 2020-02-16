---
title: Selección de un tipo de persistencia para una instalación de AEM Forms
seo-title: Selección de un tipo de persistencia para una instalación de AEM Forms
description: Elija sabiamente un tipo de persistencia. Le ayuda a crear un entorno de AEM Forms eficaz y escalable.
seo-description: Elija sabiamente un tipo de persistencia. Esto le ayuda a crear un entorno de AEM Forms eficiente y escalable.
uuid: 1c692502-5039-4757-9358-1772772b3904
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: a972fb35-38a7-4b83-99bd-6a6dddf8043b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Selección de un tipo de persistencia para una instalación de AEM Forms {#choosing-a-persistence-type-for-an-aem-forms-installation}

Elija sabiamente un tipo de persistencia. Le ayuda a crear un entorno de AEM Forms eficaz y escalable.

La persistencia es el método para almacenar contenido en las tiendas físicas. Define la estructura de datos real y el mecanismo de almacenamiento de los datos. Los microkernels actúan como administradores de persistencia en AEM Forms. AEM Forms admite persistencia (MicroKernals) de tipo TarMK, MongoMK y RDBMK. Puede elegir un tipo de persistencia para AEM Forms en función del propósito y el tipo de implementación (un solo servidor, granja o clúster) de una instancia de AEM Forms.

>[!NOTE]
>
>LiveCycle ES4 SP1 utiliza la persistencia TarPM para almacenar contenido.

En la tabla siguiente se muestran todos los tipos de persistencia admitidos junto con varios parámetros para ayudarle a elegir un tipo de persistencia para su entorno:

<table>
 <tbody>
  <tr>
   <th><strong>Tipo/costo de instalación</strong></th>
   <th><strong>TarMK</strong></th>
   <th><strong>MongoMk</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>Configuración independiente</strong></th>
   <td>Admitido<br /> </td>
   <td>Admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <th><strong>Configuración de clúster</strong></th>
   <td>No admitido</td>
   <td>Admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <th><strong>Costo de licencia</strong></th>
   <td>Incluido con AEM </td>
   <td>Se requiere una licencia separada</td>
   <td>Se requiere una licencia separada</td>
  </tr>
 </tbody>
</table>

TarMK está diseñado para el rendimiento, mientras que MongoMK y RDBMK están diseñados para la escalabilidad. Adobe recomienda encarecidamente TarMK como tecnología de persistencia predeterminada para todos los escenarios de implementación de AEM Forms, tanto para instancias de creación como de publicación, excepto en los casos de uso descritos en la sección [Selección de mongo o de un microkernel de base de datos relacional sobre TarMK](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p).

Para obtener una lista de los microkernels admitidos, consulte los artículos sobre los requisitos [técnicos de](/help/sites-deploying/technical-requirements.md) AEM Forms en OSGi o sobre las combinaciones [de plataformas compatibles con](/help/forms/using/aem-forms-jee-supported-platforms.md) AEM Forms en JEE.

## Elección de Mongo o un Microkernel de Base de Datos Relacional sobre TarMK {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

Un entorno de AEM Forms escalable (agrupado) es un conjunto de dos o más instancias de autor activas configuradas horizontalmente. Puede elegir ejecutar más de una instancia de autor si un único servidor, que admite todas las actividades de creación concurrentes, ya no es sostenible.

Solo se admiten los tipos de persistencia MongoMK y RDBMK para los formularios AEM escalables (agrupados) en entornos JEE. El número de servidores o el tamaño del entorno escalable varía según la instalación. Para obtener una lista de consideraciones y ejemplos, consulte el artículo Implementaciones [](/help/sites-deploying/recommended-deploys.md) recomendadas o las topologías de [arquitectura e implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md) . También puede ponerse en contacto con la asistencia de AEM Forms para obtener información detallada sobre la planificación de la capacidad de AEM Forms con RDBMK y TarMK.
