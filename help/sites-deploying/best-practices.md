---
title: Implementación de optimizaciones
seo-title: Implementación de optimizaciones
description: Implementación y mantenimiento de las prácticas recomendadas.
seo-description: Implementación y mantenimiento de las prácticas recomendadas.
uuid: 4546ed2c-43d5-40f3-874f-567b324e78c2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4b5c0677-c630-4fae-867e-4f4583ac8507
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 15%

---


# Implementación de optimizaciones{#deploying-best-practices}

Las prácticas recomendadas de implementación describen cómo implementar o mantener AEM de la manera más eficiente y eficaz posible. Esta lista, cada vez más extensa, incluye una gran variedad de áreas de AEM.

Las siguientes áreas cuentan con documentación sobre la implementación y el mantenimiento de las mejores prácticas y recomendaciones:

* [OAK](#oak)
* [Comunidades](#communities)
* [IU](#ui)
* [Actuación](#performance)

Para ver las prácticas recomendadas sobre administración, desarrollo o creación, consulte una de las siguientes opciones:

* [Prácticas recomendadas sobre administración](/help/sites-administering/administer-best-practices.md)
* [Prácticas recomendadas sobre desarrollo](/help/sites-developing/best-practices.md)
* [Prácticas recomendadas de creación](/help/sites-authoring/best-practices.md)

Las tablas siguientes describen los documentos e incluyen vínculos a ellos.

## OAK {#oak}

[](/help/sites-deploying/platform.md) Oakis es un repositorio de contenido jerárquico escalable y de rendimiento que es la base de AEM.

<table>
 <tbody>
  <tr>
   <td><p>Escalabilidad, performance y recuperación ante desastres</p> </td>
   <td><a href="/help/sites-deploying/performance.md">Rendimiento y escalabilidad</a></td>
   <td>Proporciona un documento técnico en el que se analizan la agilidad técnica, el alto rendimiento y las características de recuperación ante desastres sólidas</td>
  </tr>
  <tr>
   <td>Implementaciones de OAK recomendadas</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Implementaciones recomendadas</a></td>
   <td>Describe situaciones de implementación</td>
  </tr>
  <tr>
   <td>Topología de mongo</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Prácticas recomendadas de topología de mongo</a></td>
   <td>Describe la topología de mongo: cuándo utilizar la topología.</td>
  </tr>
  <tr>
   <td>Opciones del almacén de datos</td>
   <td><a href="/help/sites-deploying/data-store-config.md">Configuración de nodos y almacenes de datos</a></td>
   <td>Este documento explica las prácticas recomendadas para almacenar datos binarios y nodos de contenido. Incluye información sobre el uso del almacén de datos Amazon S3.</td>
  </tr>
  <tr>
   <td>Buscar en OAK</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">Prácticas recomendadas para Consultas e indexación</a><br /> </td>
   <td>Describe las prácticas recomendadas para indexar contenido.</td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

AEM Communities simplifica la creación y gestión de comunidades locales. Las prácticas recomendadas para AEM Communities se describen a continuación:

[Almacenamiento](/help/communities/working-with-srp.md)  de contenido de comunidad: analiza la nueva función de almacenamiento compartido para el contenido generado por el usuario (UGC) y las consideraciones para elegir la  [topología](/help/communities/topologies.md) subyacente.

[Implementaciones recomendadas para comunidades](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities) : describe las implementaciones recomendadas para comunidades. |

## IU {#ui}

A continuación se describen las prácticas recomendadas en la interfaz de usuario:

[Interfaz de usuario de Recommendations para clientes](/help/sites-deploying/ui-recommendations.md)

AEM tiene dos IU actualmente: IU clásica y táctil en la misma versión. Por lo tanto, los clientes deben tomar una decisión sobre qué utilizar durante la implementación del proyecto. Este documento tiene por objeto ayudar a encontrar la opción correcta.

## Actuación {#performance}

A continuación se detallan las prácticas recomendadas sobre el rendimiento:

<table>
 <tbody>
  <tr>
   <td>Prácticas recomendadas para garantizar la calidad</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">Prácticas recomendadas para garantizar la calidad</a></td>
   <td>Una descripción general estandarizada de los problemas relacionados con la definición de un concepto de prueba específicamente para pruebas de rendimiento en el entorno <em>publish</em>. Esto es de interés primordial para los ingenieros de control de calidad, los directores de proyectos y los administradores de sistemas.</td>
  </tr>
  <tr>
   <td>Uso de Dispatcher con una CDN</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">Uso de Dispatcher con una CDN</a></td>
   <td>Una red de entrega de contenido (CDN), como Akamai Edge Delivery o Amazon Cloud Front, ofrece contenido desde una ubicación cercana al usuario final.</td>
  </tr>
  <tr>
   <td>Optimización del rendimiento</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">Optimización del rendimiento</a></td>
   <td>Un problema clave es el tiempo que tarda el sitio web en responder a las solicitudes de visitante.</td>
  </tr>
  <tr>
   <td>Prueba de rendimiento</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">Prácticas recomendadas para pruebas de rendimiento</a></td>
   <td>Describe las prácticas recomendadas para ejecutar pruebas de rendimiento en una implementación AEM.<br /> </td>
  </tr>
 </tbody>
</table>

