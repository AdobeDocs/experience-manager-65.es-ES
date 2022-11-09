---
title: Prácticas recomendadas
seo-title: Best Practices
description: Los equipos de ingeniería y consultoría de Adobe han desarrollado un conjunto completo de prácticas recomendadas para los desarrolladores de AEM
seo-description: Adobe Engineering and Consulting teams have developed a comprehensive set of best practices for AEM developers
uuid: f962c31f-8140-482f-b189-16376e23bfed
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 99678c1a-81f3-4fb3-bf73-98f0691c3fb6
exl-id: 0a478e80-c1b2-46c1-a6be-794d78b85d69
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 19%

---

# Prácticas recomendadas{#best-practices}

## Prácticas recomendadas para desarrolladores: introducción {#best-practices-for-developers-getting-started}

Los equipos de ingeniería y consultoría de Adobe han desarrollado un conjunto completo de prácticas recomendadas para los desarrolladores de AEM. Los desarrolladores de Adobe siguen estas prácticas recomendadas a medida que desarrollan actualizaciones de productos AEM principales y código de cliente para implementaciones de clientes.

Antes de comenzar el proyecto de desarrollo de AEM, revise primero estas prácticas recomendadas:

* [Prácticas de desarrollo](/help/sites-developing/development-practices.md)
* [Arquitectura de contenido](/help/sites-developing/content-architecture.md)
* [Arquitectura de software](/help/sites-developing/software-architecture.md)
* [Consejos de codificación](/help/sites-developing/coding-tips.md)
* [Problemas de código](/help/sites-developing/code-pitfalls.md)
* [Interacción de JCR](/help/sites-developing/jcr-integration.md)
* [Paquetes OSGi](/help/sites-developing/osgi-bundles.md)
* [Prácticas recomendadas de API de Java](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

### Información adicional sobre prácticas recomendadas {#additional-best-practices-information}

Las siguientes áreas tienen documentación disponible específica para el desarrollo de prácticas recomendadas:

* [Sites](#sites)
* [Communities](/help/sites-developing/best-practices.md#communities)
* [Herramientas/HTL](/help/sites-developing/best-practices.md#tooling-htl)

Las tablas siguientes describen los documentos e incluyen vínculos a ellos.

Para conocer las prácticas recomendadas sobre administración, implementación y mantenimiento, o creación, consulte uno de los siguientes temas:

* [Prácticas recomendadas sobre administración](/help/sites-administering/administer-best-practices.md)
* [Prácticas recomendadas sobre la creación](/help/sites-authoring/best-practices.md)
* [Prácticas recomendadas sobre implementación](/help/sites-deploying/best-practices.md)

## Sitios {#sites}

Para administrar y crear contenido en un sitio web, hay que seguir estas prácticas recomendadas:

<table>
 <tbody>
  <tr>
   <td>Parte de la teoría que sustenta la IU táctil estándar.</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">IU táctil: Conceptos</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">IU táctil: Estructura</a></p> </td>
   <td>Estos documentos proporcionan información general sobre los conceptos y la estructura de la IU táctil.</td>
  </tr>
  <tr>
   <td>IU táctil: Personalización de consolas </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">Personalización de consolas de IU con capacidad táctil</a></td>
   <td>Este documento describe la mejor manera de ampliar las consolas para la IU táctil.</td>
  </tr>
  <tr>
   <td>IU táctil: Personalización de la creación de páginas</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">Personalización de la creación de páginas con IU táctil</a></td>
   <td>Describe cómo ampliar la creación de páginas para la IU táctil.</td>
  </tr>
  <tr>
   <td>Flujos de trabajo</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">Desarrollo y ampliación de flujos de trabajo</a></td>
   <td><p>Los flujos de trabajo permiten automatizar las actividades de Adobe Experience Manager (AEM) y pueden representar una gran cantidad del procesamiento que se produce en un entorno de AEM, por lo que se recomienda planificar cuidadosamente las implementaciones de flujos de trabajo.</p> </td>
  </tr>
 </tbody>
</table>

## Comunidades {#communities}

[AEM Communities](/help/communities/overview.md) simplifica la creación y gestión de comunidades locales.

A continuación se describen algunas prácticas recomendadas para las comunidades:

|  |  |  |
|---|---|---|
| Prácticas recomendadas para trabajar con contenido generado por el usuario (UGC) | [Directrices de codificación](/help/communities/code-guide.md) | Directrices para el desarrollo de código flexible y portátil para [marco de componentes sociales](/help/communities/scf.md) (SCF). |
| Ejemplo de uso de componentes de Communities | [Guía de componentes de comunidad](/help/communities/components-guide.md) | Una herramienta de desarrollo interactiva. |

## Herramientas/HTL {#tooling-htl}

El lenguaje de plantilla de HTML (HTL) es un nuevo sistema de plantilla de HTML, introducido con AEM 6.0. Sustituye a JSP y ESP como sistema de plantilla preferido de AEM.

|  |  |  |
|---|---|---|
| Información general sobre HTL | [Información general y sintaxis de HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) | Este documento describe qué es HTL, cómo se mueve a HTL, un proyecto de ejemplo, sintaxis, expresiones y afirmaciones |
| Uso de API en java | [HTL Java Use-API](https://helpx.adobe.com/experience-manager/htl/using/use-api.html) | La HTL Java Use-API permite que un archivo HTL acceda a los métodos de ayuda en una clase Java personalizada. |

>[!NOTE]
>
>El siguiente tutorial en varias partes puede ser de interés para la práctica recomendada para configurar un nuevo proyecto de AEM, que detalla los componentes principales, las plantillas editables, las bibliotecas de clientes y el desarrollo de componentes:
>[Introducción a AEM Sites: Tutorial de WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)
