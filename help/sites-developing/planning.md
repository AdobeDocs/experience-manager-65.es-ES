---
title: Planificación
seo-title: Planning
description: Aprenda lo que necesita saber para planificar las pruebas de Adobe Experience Manager.
seo-description: What you need to know to plan for your test
uuid: 29b1127a-da85-46ed-98e7-1c983eb40cfe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 12268c43-93f9-42c1-8dd7-f17f9ae2219b
exl-id: ed662279-0679-4ba3-b744-6649fb8dda17
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 0%

---

# Planificación{#planning}

En este documento se describe lo que necesita saber para planificar la prueba. Además, debe responder a estas preguntas antes de realizar las pruebas:

* [¿Qué entornos de prueba se necesitarán?](/help/sites-developing/test-environments.md)
* [Definición de los casos de prueba](/help/sites-developing/test-cases.md)
* [Pruebas: ¿cuándo y con quién?](/help/sites-developing/when-who.md)

## Antes de comenzar {#before-you-start}

Antes de comenzar con el análisis real y la definición de pruebas, revise la siguiente información:

**AEM Arquitectura de** AEM - Consulte Conceptos Básicos para conocer la arquitectura y los principios básicos de la.

**Documentación** : Consulte cualquiera de las secciones de documentación o los artículos Cómo, para obtener más información.

**Principios básicos de las pruebas** - Debe tener en cuenta los principios básicos de las pruebas de software y la garantía de calidad. Preferiblemente, debería tener experiencia en proyectos de prueba.

Existen muchos sitios web, libros y cursos que tratan sobre tales principios y por lo tanto no serán tratados en detalle en este documento.

**Suposiciones que se deben evitar** - La mayor suposición (hecha regularmente) es que su sitio web necesitará atender millones de solicitudes cada día. En ciertas circunstancias esto puede ser cierto, pero no se puede suponer.

Aunque los números futuros no se pueden predecir con una precisión del 100%, observar el sitio existente y el tráfico experimentado dará una buena indicación. A continuación, puede hacer que las estimaciones dependan del factor por el que espera / espera que aumente el tráfico.

**Compromiso con la calidad** - Es de suma importancia que cualquier persona que pruebe permanezca neutral y simplemente informe de los resultados de las pruebas realizadas.

Es responsabilidad del administrador del proyecto decidir e iniciar acciones en función de los resultados.

**Participar** - Aunque es responsabilidad del gestor del proyecto garantizar que todas las partes participen plenamente en cualquier reunión (estado, talleres, etc.), también debe intentar participar lo antes posible en el ciclo del proyecto, incluidos los procesos de recopilación de información y análisis de requisitos.

**Involucrar al cliente** : En un tema similar, intente involucrar al cliente (cuando sea posible) al definir los casos y el plan de prueba.

## Tipos de pruebas {#types-of-tests}

AEM Existen varias clasificaciones estándar de pruebas que son adecuadas para su uso al probar un proyecto de. Debe estar familiarizado con estos elementos para decidir cuál utilizar:

>[!NOTE]
>
>Se enumeran en su orden cronológico de aplicación.

**Pruebas de unidades** - Pruebas (por lo general) realizadas por el equipo de desarrollo para garantizar que los elementos individuales se comportan correctamente, aunque de forma aislada.

**Pruebas de integración** - Pruebe los módulos cuando se combinan. Estas pruebas se realizan después de la prueba unitaria, pero antes de la prueba del sistema.

**Pruebas de humo** - Se trata de pruebas rápidas y sucias que se utilizan para probar que el software se está ejecutando y que la funcionalidad de alto nivel está disponible. Los detalles no se prueban.

**Pruebas funcionales** - Se utilizan para probar la funcionalidad del software. Se diseñará una serie de pruebas para cubrir todos los detalles funcionales, con entradas esperadas e inesperadas o erróneas.

Las pruebas de caja negra son pruebas funcionales de una unidad/componente/módulo completo, realizadas sin conocimiento del funcionamiento interno del elemento en cuestión.

**Pruebas del sistema** - Estos equipos prueban todo el sistema una vez que ha sido completamente integrado e instalado en una plataforma adecuada.

Prueban la funcionalidad en base a una caja negra.

**Pruebas de rendimiento** AEM - Las pruebas de rendimiento son cruciales cuando se realiza la prueba de la.

Se utilizan para ilustrar el rendimiento en condiciones diferentes:

* Normal

  Condiciones que el sitio experimentará por ejemplo el 90% del tiempo. Por ejemplo, cuando solo una proporción de los autores utiliza el sistema.

* Pico

  Condiciones que se experimentarán durante un tiempo proporcionalmente corto debido a circunstancias especiales; por ejemplo, cuando todos los autores utilicen el sistema simultáneamente o cuando se publique nuevo contenido y un número mayor de visitantes vea el sitio.

* Extremo

  Se puede utilizar para emular la previsión de rendimiento cuando se publica contenido nuevo y extremadamente interesante en el sitio web. Entonces se puede ver un pico extremo, aunque esto no siempre es totalmente predecible.

  Estas circunstancias se ven a veces cuando se ponen a disposición entradas para eventos específicos, o cuando se publica por primera vez un sitio web muy esperado.

A continuación, los resultados se utilizan para ajustar la aplicación.

**Pruebas de esfuerzo** - Se realizan pruebas de esfuerzo para confirmar cómo se comporta un componente o aplicación en condiciones extremas. En particular, estas pruebas se utilizan para mostrar cómo se deteriora el comportamiento, cuándo falla el elemento y cómo.

**Pruebas de regresión** - Se utilizan pruebas de regresión para confirmar que la funcionalidad ya probada en una versión anterior del software sigue funcionando correctamente.

Las pruebas de regresión son buenos candidatos para la automatización (si es posible) para garantizar que se puedan repetir de forma rápida y coherente.

**Pruebas de aceptación** - Las pruebas de aceptación son una categoría especial, ya que se utilizan para indicar la aceptación del cliente del proyecto.

La lista de pruebas de aceptación puede contener una combinación de pruebas de las distintas categorías anteriores y se seleccionan para comprobar que el proyecto cumple los requisitos del cliente

Consulte [Aceptación y desactivación](/help/sites-developing/acceptance-signoff.md) para obtener más información.

## Introducción {#getting-started}

Antes de comenzar con los casos de prueba y el plan de prueba detallados, puede hacer lo siguiente:

**Definir los objetivos** - Defina sus objetivos de alto nivel para que actúen como punto de partida para el ajuste a medida que avanza la prueba. Tendrá lo siguiente:

* Pruebe la funcionalidad según la Especificación detallada de requisitos.
* Rendimiento de la prueba según el [Métricas de Target](/help/managing/best-practices-further-reference.md#key-performance-indicators-and-target-metrics).

entre otros.

**Recopilar estadísticas de tráfico del sitio web existente** : esta información se puede extraer de los archivos de registro . Consulte Monitorización del rendimiento para obtener más información.

Estas cifras darán una indicación del tráfico actual (volumen y difusión) en el sitio web existente y se pueden utilizar para formar un punto de base para el nuevo sitio web.

**Recopilar estadísticas de tráfico de sitios web externos** - Si es posible, puede intentar recopilar estadísticas de tráfico de otros sitios web para comparar, pero estas cifras no siempre se publican.

**Confirmar métricas de Target** - Las métricas se utilizan para definir mediciones cuantitativas de la calidad del sitio web, ya que representan los objetivos de rendimiento que deben alcanzarse.

Deben definirse al principio del proyecto, junto con el cliente. Consulte [Métricas de Target](/help/sites-developing/planning.md) para obtener más información.
