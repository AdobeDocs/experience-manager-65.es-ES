---
title: Prácticas recomendadas
seo-title: Prácticas recomendadas
description: Los equipos de ingeniería y consultoría de Adobe han desarrollado un completo conjunto de prácticas recomendadas para los desarrolladores de AEM
seo-description: Los equipos de ingeniería y consultoría de Adobe han desarrollado un completo conjunto de prácticas recomendadas para los desarrolladores de AEM
uuid: f962c31f-8140-482f-b189-16376e23bfed
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 99678c1a-81f3-4fb3-bf73-98f0691c3fb6
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c

---


# Prácticas recomendadas{#best-practices}

## Prácticas recomendadas para desarrolladores: Introducción {#best-practices-for-developers-getting-started}

Los equipos de ingeniería y consultoría de Adobe han desarrollado un completo conjunto de prácticas recomendadas para los desarrolladores de AEM. Los desarrolladores de Adobe siguen estas prácticas recomendadas a medida que desarrollan actualizaciones de productos principales de AEM y código de cliente para implementaciones de clientes.

Antes de iniciar el proyecto de desarrollo de AEM, consulte estas prácticas recomendadas:

* [Prácticas de desarrollo](/help/sites-developing/development-practices.md)
* [Arquitectura del contenido](/help/sites-developing/content-architecture.md)
* [Arquitectura de software](/help/sites-developing/software-architecture.md)
* [Consejos de codificación](/help/sites-developing/coding-tips.md)
* [Problemas de código](/help/sites-developing/code-pitfalls.md)
* [Interacción de JCR](/help/sites-developing/jcr-integration.md)
* [Paquetes OSGi](/help/sites-developing/osgi-bundles.md)

### Información adicional sobre prácticas recomendadas {#additional-best-practices-information}

Las siguientes áreas tienen documentación disponible específica para desarrollar las mejores prácticas:

* [Sitios](#sites)
* [Comunidades](/help/sites-developing/best-practices.md#communities)
* [Tooling/HTL](/help/sites-developing/best-practices.md#tooling-htl)

Las tablas siguientes describen los documentos e incluyen vínculos a ellos.

Para ver las prácticas recomendadas sobre administración, implementación, mantenimiento o creación, consulte una de las siguientes opciones:

* [Prácticas recomendadas sobre administración](/help/sites-administering/administer-best-practices.md)
* [Prácticas recomendadas de creación](/help/sites-authoring/best-practices.md)
* [Prácticas recomendadas sobre implementación](/help/sites-deploying/best-practices.md)

## Sitios {#sites}

Para administrar y crear contenido en un sitio web, hay que seguir estas prácticas recomendadas:

<table>
 <tbody>
  <tr>
   <td>Algunas de las teorías detrás de la IU estándar con capacidad táctil.</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">IU táctil: Conceptos</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">IU táctil:Estructura</a></p> </td>
   <td>Estos documentos proporcionan información general sobre los conceptos y la estructura de la IU táctil.</td>
  </tr>
  <tr>
   <td>IU táctil: Personalización de consolas </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">Personalización de consolas de IU táctiles</a></td>
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
   <td><p>Los flujos de trabajo le permiten automatizar las actividades de Adobe Experience Manager (AEM) y pueden representar una gran parte del procesamiento que se produce en un entorno AEM, por lo que se recomienda planificar cuidadosamente las implementaciones de flujos de trabajo.</p> </td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

[AEM Communities](/help/communities/overview.md) simplifica la creación y gestión de comunidades locales.

A continuación se describen algunas prácticas recomendadas para las comunidades:

|  |  |  |
|---|---|---|
| Prácticas recomendadas para trabajar con contenido generado por usuarios (UGC) | [Directrices de codificación](/help/communities/code-guide.md) | Directrices para desarrollar un código flexible y portátil para el marco [de componentes](/help/communities/scf.md) sociales (SCF). |
| Ejemplo de uso de componentes de Communities | [Guía de componentes de comunidad](/help/communities/components-guide.md) | Una herramienta de desarrollo interactiva. |

## Tooling/HTL {#tooling-htl}

HTML Template Language (HTL) es un nuevo sistema de plantillas HTML, introducido con AEM 6.0. Reemplaza JSP y ESP como el sistema de plantillas preferido de AEM.

|  |  |  |
|---|---|---|
| Visión general de HTL | [Información general y sintaxis de HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) | Este documento describe qué es HTL, cómo moverse a HTL, un proyecto de muestra, sintaxis, expresiones y afirmaciones |
| Uso de API en java | [HTL Java Use-API](https://helpx.adobe.com/experience-manager/htl/using/use-api.html) | La Use-API de HTL Java permite que un archivo HTL acceda a los métodos de ayuda en una clase Java personalizada. |

>[!NOTE]
>
>El siguiente tutorial en varias partes puede ser de interés para la práctica recomendada para configurar un nuevo proyecto de AEM, en el que se detallan los componentes principales, las plantillas editables, las bibliotecas de clientes y el desarrollo de componentes:
>[Introducción a los sitios de AEM: Tutorial de WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)

