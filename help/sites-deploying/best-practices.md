---
title: Prácticas Recomendadas De Implementación
seo-title: Deploying Best Practices
description: Implementación y mantenimiento de las prácticas recomendadas.
seo-description: Deploying and maintaining best practices.
uuid: 4546ed2c-43d5-40f3-874f-567b324e78c2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4b5c0677-c630-4fae-867e-4f4583ac8507
exl-id: 4cbc0a30-d5f6-40ff-b7f6-8d64762e1970
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 16%

---

# Prácticas Recomendadas De Implementación{#deploying-best-practices}

Las prácticas recomendadas de implementación describen cómo implementar o mantener AEM de la forma más eficiente y eficaz posible. Esta lista, cada vez más extensa, incluye una gran variedad de áreas de AEM.

Las siguientes áreas tienen documentación disponible sobre la implementación y el mantenimiento de las prácticas recomendadas y recomendaciones:

* [OAK](#oak)
* [Communities](#communities)
* [IU](#ui)
* [Actuación](#performance)

Para conocer las prácticas recomendadas sobre administración, desarrollo o creación, consulte uno de los siguientes temas:

* [Prácticas recomendadas sobre administración](/help/sites-administering/administer-best-practices.md)
* [Prácticas recomendadas sobre desarrollo](/help/sites-developing/best-practices.md)
* [Prácticas recomendadas sobre la creación](/help/sites-authoring/best-practices.md)

Las tablas siguientes describen los documentos e incluyen vínculos a ellos.

## OAK {#oak}

[Oak](/help/sites-deploying/platform.md) es un repositorio de contenido jerárquico escalable y con rendimiento que es la base de AEM.

<table>
 <tbody>
  <tr>
   <td><p>Escalabilidad, Performance y Recuperación ante Desastres</p> </td>
   <td><a href="/help/sites-deploying/performance.md">Rendimiento y escalabilidad</a></td>
   <td>Proporciona un documento técnico en el que se analizan la agilidad técnica, el alto rendimiento y las funciones de recuperación ante desastres sólidas</td>
  </tr>
  <tr>
   <td>Implementaciones de OAK recomendadas</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Implementaciones recomendadas</a></td>
   <td>Describe los escenarios de implementación</td>
  </tr>
  <tr>
   <td>Topología mongo</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Prácticas recomendadas sobre la topología de Mongo</a></td>
   <td>Describe la topología de mongo: cuándo utilizar qué topología.</td>
  </tr>
  <tr>
   <td>Opciones del almacén de datos</td>
   <td><a href="/help/sites-deploying/data-store-config.md">Configuración de nodos y almacenes de datos</a></td>
   <td>En este documento se explican las prácticas recomendadas relacionadas con el almacenamiento de datos binarios y nodos de contenido. Incluye información sobre el uso del almacén de datos de Amazon S3.</td>
  </tr>
  <tr>
   <td>Buscar en OAK</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">Prácticas recomendadas para consultas e indexación</a><br /> </td>
   <td>Describe las prácticas recomendadas sobre cómo indexar contenido.</td>
  </tr>
 </tbody>
</table>

## Comunidades {#communities}

AEM Communities simplifica la creación y gestión de comunidades locales. Las prácticas recomendadas para AEM Communities se describen a continuación:

[Almacenamiento de contenido de la comunidad](/help/communities/working-with-srp.md) - Analiza la nueva función de almacenamiento compartido para el contenido generado por el usuario (UGC) y las consideraciones para elegir el subyacente [topología](/help/communities/topologies.md).

[Implementaciones recomendadas para comunidades](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities) - Describe las implementaciones recomendadas para Communities. |

## IU {#ui}

Las prácticas recomendadas en torno a la interfaz de usuario se describen a continuación:

[Interfaz de usuario de Recommendations para clientes](/help/sites-deploying/ui-recommendations.md)

AEM tiene dos IU actualmente: IU clásica y táctil optimizada en la misma versión. Por lo tanto, los clientes deben tomar una decisión sobre qué utilizar durante la implementación del proyecto. El objetivo de este documento es ayudar a encontrar la opción correcta.

## Actuación {#performance}

Las prácticas recomendadas sobre el rendimiento se enumeran a continuación:

<table>
 <tbody>
  <tr>
   <td>Prácticas recomendadas para garantizar la calidad</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">Prácticas recomendadas para garantizar la calidad</a></td>
   <td>Una visión general estandarizada de los problemas relacionados con la definición de un concepto de prueba específicamente para las pruebas de rendimiento en su <em>publicar</em> entorno. Esto es de interés principalmente para los ingenieros de control de calidad, los directores de proyectos y los administradores de sistemas.</td>
  </tr>
  <tr>
   <td>Utilizar Dispatcher con una CDN</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">Utilizar Dispatcher con una CDN</a></td>
   <td>Una red de entrega de contenido (CDN), como Akamai Edge Delivery o Amazon Cloud Front, ofrece contenido desde una ubicación cercana al usuario final.</td>
  </tr>
  <tr>
   <td>Optimización del rendimiento</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">Optimización del rendimiento</a></td>
   <td>Un problema clave es el tiempo que tarda el sitio web en responder a las solicitudes de los visitantes.</td>
  </tr>
  <tr>
   <td>Pruebas de rendimiento</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">Prácticas recomendadas para pruebas de rendimiento</a></td>
   <td>Describe las prácticas recomendadas para ejecutar pruebas de rendimiento en una implementación AEM.<br /> </td>
  </tr>
 </tbody>
</table>
