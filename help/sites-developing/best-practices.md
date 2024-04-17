---
title: AEM Prácticas recomendadas para desarrolladores de
description: Los equipos de ingeniería y consultoría de Adobe AEM han desarrollado un conjunto completo de prácticas recomendadas para los desarrolladores de.
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 0a478e80-c1b2-46c1-a6be-794d78b85d69
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 3%

---

# Prácticas recomendadas{#best-practices}

## Prácticas recomendadas para desarrolladores: Introducción {#best-practices-for-developers-getting-started}

Los equipos de ingeniería y consultoría de Adobe AEM han desarrollado un conjunto completo de prácticas recomendadas para los desarrolladores de. Los desarrolladores de Adobe AEM se adhieren a estas prácticas recomendadas a medida que desarrollan actualizaciones principales de productos y códigos de cliente para implementaciones de clientes.

AEM Antes de iniciar el proyecto de desarrollo de la, revise primero estas prácticas recomendadas:

* [Prácticas de desarrollo](/help/sites-developing/development-practices.md)
* [Arquitectura de contenido](/help/sites-developing/content-architecture.md)
* [Arquitectura de software](/help/sites-developing/software-architecture.md)
* [Sugerencias de codificación](/help/sites-developing/coding-tips.md)
* [Problemas de código](/help/sites-developing/code-pitfalls.md)
* [Interacción JCR](/help/sites-developing/jcr-integration.md)
* [Paquetes OSGi](/help/sites-developing/osgi-bundles.md)
* [Prácticas recomendadas de API de Java](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

### Información adicional sobre prácticas recomendadas {#additional-best-practices-information}

Las siguientes áreas tienen documentación disponible específica para el desarrollo de prácticas recomendadas:

* [Sites](#sites)
* [Communities](/help/sites-developing/best-practices.md#communities)
* [Herramientas/HTL](/help/sites-developing/best-practices.md#tooling-htl)

En las tablas siguientes se describen y vinculan documentos específicos.

Para conocer las prácticas recomendadas sobre la administración, la implementación, el mantenimiento o la creación, consulte una de las siguientes opciones:

* [Prácticas recomendadas de administración](/help/sites-administering/administer-best-practices.md)
* [Prácticas recomendadas de creación](/help/sites-authoring/best-practices.md)
* [Implementación de prácticas recomendadas](/help/sites-deploying/best-practices.md)

## Sites {#sites}

La administración y creación del contenido del sitio web tiene algunas prácticas recomendadas descritas a continuación:

<table>
 <tbody>
  <tr>
   <td>Parte de la teoría detrás de la IU táctil estándar.</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">IU táctil: conceptos</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">IU táctil: estructura</a></p> </td>
   <td>Estos documentos proporcionan información general sobre los conceptos y la estructura de la IU táctil.</td>
  </tr>
  <tr>
   <td>IU táctil: personalización de consolas </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">Personalización de consolas de IU táctiles</a></td>
   <td>Este documento describe la mejor manera de ampliar las consolas para la IU táctil.</td>
  </tr>
  <tr>
   <td>IU táctil: personalizar la creación de páginas</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">Personalizar la creación de páginas de IU táctiles</a></td>
   <td>Describe cómo ampliar la creación de páginas para la IU táctil.</td>
  </tr>
  <tr>
   <td>Flujos de trabajo</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">Desarrollo y ampliación de flujos de trabajo</a></td>
   <td><p>Los flujos de trabajo le permiten automatizar las actividades de Adobe Experience Manager AEM AEM () y pueden representar una gran cantidad del procesamiento que se produce en un entorno de trabajo, por lo que es muy recomendable planificar las implementaciones de flujos de trabajo con cuidado.</p> </td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

[AEM Communities](/help/communities/overview.md) simplifica la creación y administración de comunidades locales.

Algunas prácticas recomendadas para las comunidades se describen aquí:

|  |  |  |
|---|---|---|
| Prácticas recomendadas para trabajar con contenido generado por el usuario (UGC) | [Directrices de codificación](/help/communities/code-guide.md) | Directrices para desarrollar código flexible y portátil para [marco de componentes sociales](/help/communities/scf.md) (SCF). |
| Ejemplo de uso de componentes de Communities | [Guía de componentes de la comunidad](/help/communities/components-guide.md) | Una herramienta de desarrollo interactiva. |

## Herramientas/HTL {#tooling-htl}

El lenguaje de plantilla de HTML (HTL) es un nuevo sistema de plantillas de HTML AEM, incluido en la versión 6.0 de la versión, que se ha introducido con la versión 6.0 de la aplicación. AEM Sustituye a JSP y ESP como sistema de creación de plantillas preferido de los.

|  |  |  |
|---|---|---|
| Información general sobre HTL | [Información general y sintaxis de HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=es) | Este documento describe qué es HTL, cómo pasar a HTL, un proyecto de ejemplo, sintaxis, expresiones e instrucciones |
| Uso de la API en Java | [HTL Java Use-API](https://helpx.adobe.com/experience-manager/htl/using/use-api.html) | La API de uso de Java de HTL permite que un archivo HTL acceda a los métodos de ayuda en una clase Java personalizada. |

>[!NOTE]
>
>AEM Los siguientes tutoriales de varias partes pueden ser de interés para la práctica recomendada de configurar un nuevo proyecto de, que detalla los componentes principales, las plantillas editables, las bibliotecas de clientes y el desarrollo de componentes:
>[Introducción a AEM Sites: Tutorial de WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)
