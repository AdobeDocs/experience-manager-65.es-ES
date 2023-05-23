---
title: Implementación de prácticas recomendadas
seo-title: Deploying Best Practices
description: Implementación y mantenimiento de prácticas recomendadas.
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
ht-degree: 9%

---

# Implementación de prácticas recomendadas{#deploying-best-practices}

AEM Las prácticas recomendadas sobre la implementación describen cómo implementar o mantener los recursos de la manera más eficiente y eficaz posible. AEM Esta creciente lista de temas incluye una variedad de áreas en el área de la.

Las siguientes áreas tienen documentación disponible sobre la implementación y el mantenimiento de las prácticas recomendadas y recomendaciones:

* [OAK](#oak)
* [Communities](#communities)
* [IU](#ui)
* [Rendimiento](#performance)

Para conocer las prácticas recomendadas sobre la administración, el desarrollo o la creación, consulte una de las siguientes opciones:

* [Prácticas recomendadas de administración](/help/sites-administering/administer-best-practices.md)
* [Desarrollo de prácticas recomendadas](/help/sites-developing/best-practices.md)
* [Prácticas recomendadas de creación](/help/sites-authoring/best-practices.md)

En las tablas siguientes se describen y vinculan documentos específicos.

## OAK {#oak}

[Oak](/help/sites-deploying/platform.md) AEM es un repositorio de contenido jerárquico escalable y con buen rendimiento que es la base de la creación de informes de contenido de tipo

<table>
 <tbody>
  <tr>
   <td><p>Escalabilidad, rendimiento y recuperación ante desastres</p> </td>
   <td><a href="/help/sites-deploying/performance.md">Rendimiento y escalabilidad</a></td>
   <td>Proporciona un documento técnico en el que se describen las características técnicas de agilidad, alto rendimiento y recuperación ante desastres con sonido</td>
  </tr>
  <tr>
   <td>Implementaciones OAK recomendadas</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Implementaciones recomendadas</a></td>
   <td>Describe escenarios de implementación</td>
  </tr>
  <tr>
   <td>Topología Mongo</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Prácticas recomendadas de topología Mongo</a></td>
   <td>Describe la topología mongo: cuándo utilizar qué topología.</td>
  </tr>
  <tr>
   <td>Opciones de almacén de datos</td>
   <td><a href="/help/sites-deploying/data-store-config.md">Configuración de almacenes de datos y nodos</a></td>
   <td>En este documento se explican las prácticas recomendadas sobre el almacenamiento de datos binarios y nodos de contenido. Incluye información sobre el uso del almacén de datos de Amazon S3.</td>
  </tr>
  <tr>
   <td>Buscar en OAK</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">Prácticas recomendadas para consultas e indexación</a><br /> </td>
   <td>Describe las prácticas recomendadas sobre cómo indexar contenido.</td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

AEM Communities simplifica la creación y administración de comunidades locales. Las prácticas recomendadas para AEM Communities se describen aquí:

[Almacenamiento de contenido de comunidad](/help/communities/working-with-srp.md) : analiza la nueva función de almacenamiento compartido para el contenido generado por el usuario (UGC) y las consideraciones para elegir el subyacente [topología](/help/communities/topologies.md).

[Implementaciones recomendadas para comunidades](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities) - Describe las implementaciones recomendadas para Communities. |

## IU {#ui}

Las prácticas recomendadas en la interfaz de usuario se describen aquí:

[Interfaz de usuario de Recommendations para clientes](/help/sites-deploying/ui-recommendations.md)

AEM Actualmente, tiene dos interfaces de usuario: la clásica y la táctil en la misma versión. Por lo tanto, los clientes deben tomar una decisión sobre cuál utilizar durante la implementación del proyecto. El objetivo de este documento es ayudar a encontrar la opción correcta.

## Rendimiento {#performance}

Las prácticas recomendadas en cuanto a rendimiento se enumeran a continuación:

<table>
 <tbody>
  <tr>
   <td>Prácticas recomendadas para el control de calidad</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">Prácticas recomendadas para el control de calidad</a></td>
   <td>Una visión general estandarizada de los problemas relacionados con la definición de un concepto de prueba específicamente para pruebas de rendimiento en su <em>publicar</em> entorno. Esto es principalmente de interés para los ingenieros de control de calidad, gestores de proyectos y administradores de sistemas.</td>
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
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">Prácticas recomendadas para las pruebas de rendimiento</a></td>
   <td>AEM Describe las prácticas recomendadas para ejecutar pruebas de rendimiento en una implementación de.<br /> </td>
  </tr>
 </tbody>
</table>
