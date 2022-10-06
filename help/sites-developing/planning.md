---
title: Planificación
seo-title: Planning
description: Lo que debe saber para planificar la prueba
seo-description: What you need to know to plan for your test
uuid: 29b1127a-da85-46ed-98e7-1c983eb40cfe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 12268c43-93f9-42c1-8dd7-f17f9ae2219b
exl-id: ed662279-0679-4ba3-b744-6649fb8dda17
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---

# Planificación{#planning}

Este documento describe lo que debe saber para planificar la prueba. Además, debe responder a estas preguntas antes de realizar las pruebas:

* [¿Qué entornos de prueba se necesitarán?](/help/sites-developing/test-environments.md)
* [Definición de los casos de prueba](/help/sites-developing/test-cases.md)
* [Pruebas: ¿cuándo y con quién?](/help/sites-developing/when-who.md)

## Antes de comenzar {#before-you-start}

Antes de comenzar con el análisis real y la definición de pruebas, revise la siguiente información:

**Arquitectura AEM** - Consulte Conceptos básicos para presentarse a la arquitectura y los principios básicos de AEM.

**Documentación** - Para obtener más información, consulte cualquiera de las secciones de documentación o los artículos Instrucciones de uso.

**Principios básicos de las pruebas** - Debe conocer los principios básicos del Software Testing y Quality Assurance. Preferentemente, debería tener experiencia en proyectos de prueba.

Hay muchos sitios web, libros y cursos que tratan de esos principios y por lo tanto no se tratarán en detalle en este documento.

**Supuestos que se deben evitar** - El mayor supuesto (hecho regularmente) es que su sitio web necesitará atender millones de solicitudes cada día. En determinadas circunstancias, esto puede ser cierto, pero no puede suponerse.

Aunque los números futuros no se pueden predecir con una precisión del 100 %, observar el sitio existente y el tráfico experimentado dará una buena indicación. A continuación, puede hacer que las estimaciones dependan del factor por el que espera / espera que aumente el tráfico.

**Compromiso con la calidad** - Es de suma importancia que cualquiera que realice pruebas permanezca neutral e informe simplemente de los resultados de las pruebas realizadas.

El Administrador de proyectos es responsable de decidir e iniciar acciones en función de los resultados.

**Involucrarse** - Aunque es responsabilidad del director del proyecto garantizar que todas las partes participen plenamente en cualquier reunión (estado, talleres, etc.), también debe tratar de participar lo antes posible en el ciclo del proyecto, incluidos los procesos de recopilación de información y análisis de requisitos.

**Involucrar al cliente** - En un tema similar, intente involucrar al cliente (cuando sea posible) al definir sus casos de prueba y su plan.

## Tipos de pruebas {#types-of-tests}

Existen varias clasificaciones estándar de pruebas que son adecuadas para su uso al probar un proyecto AEM. Debe estar familiarizado con estos para decidir cuál usará:

>[!NOTE]
>
>Se enumeran en orden cronológico de aplicación.

**Pruebas de unidades** - Pruebas (normalmente) realizadas por el equipo de desarrollo para garantizar que los elementos individuales se comporten correctamente, aunque de forma aislada.

**Pruebas de integración** : Módulos de pruebas cuando se combinan. Estas pruebas se realizan después de la prueba de unidad, pero antes de la prueba del sistema.

**Pruebas de humo** - Son pruebas rápidas y sucias que se utilizan para probar que el software se está ejecutando y que la funcionalidad de alto nivel está disponible. Los detalles no se prueban.

**Pruebas funcionales** - Se utilizan para probar la funcionalidad del software. Se diseñará una serie de pruebas para cubrir todos los detalles funcionales, con entradas esperadas e inesperadas y/o erróneas.

Las pruebas en caja negra son pruebas funcionales de una unidad completa/componente/módulo, realizadas sin conocer el funcionamiento interno del elemento en cuestión.

**Pruebas del sistema** - Ensayan todo el sistema una vez que se ha integrado e instalado completamente en una plataforma adecuada.

Proban la funcionalidad en un cuadro negro.

**Pruebas de rendimiento** - Las pruebas de rendimiento son cruciales cuando se realiza la prueba AEM.

Se utilizan para ilustrar el rendimiento en condiciones diferentes:

* Normal

   Condiciones que experimentará el sitio durante, por ejemplo, el 90% de las veces. Por ejemplo, cuando solo una proporción de los autores utiliza el sistema.

* Pico

   Condiciones que se experimentarán durante un tiempo proporcionalmente breve debido a circunstancias especiales; por ejemplo, cuando todos los autores utilizan el sistema de forma simultánea o cuando se publica contenido nuevo y aumenta el número de visitantes que ven el sitio.

* Extremo

   Se puede utilizar para emular el pronóstico de rendimiento cuando se publica contenido nuevo y extremadamente interesante en su sitio web. Entonces se puede ver un pico extremo -aunque esto puede no ser siempre totalmente predecible.

   Estas circunstancias a veces se ven cuando se ponen a disposición entradas para eventos específicos, o cuando se publica por primera vez un muy esperado sitio web.

Los resultados se utilizan para ajustar la aplicación.

**Pruebas de estrés** - Se realizan pruebas de estrés para confirmar el comportamiento de un componente o aplicación en condiciones extremas. En concreto, estas pruebas se utilizan para mostrar cómo se deteriora el comportamiento, cuándo falla el elemento y cómo.

**Pruebas de regresión** - Las pruebas de regresión se utilizan para confirmar que la funcionalidad ya probada en una versión anterior del software sigue funcionando correctamente.

Las pruebas de regresión son buenas candidatas para la automatización (si es posible) para garantizar que se puedan repetir de forma rápida y coherente.

**Pruebas de aceptación** - Las pruebas de aceptación son una categoría especial, ya que se utilizan para indicar la aceptación del cliente del proyecto.

La lista de pruebas de aceptación puede contener una combinación de pruebas de las distintas categorías anteriores y se seleccionan para verificar que el proyecto cumple los requisitos del cliente

Consulte [Aceptación y desactivación](/help/sites-developing/acceptance-signoff.md) para obtener más información.

## Introducción {#getting-started}

Antes de comenzar con los casos de prueba y el plan de pruebas detallados, puede:

**Definir los objetivos** - Defina sus objetivos de alto nivel para que actúen como punto de partida para el ajuste a medida que avancen las pruebas. Desea:

* Pruebe la funcionalidad de acuerdo con la Especificación de requisitos detallada.
* Rendimiento de la prueba según el [Métricas de Target](/help/managing/best-practices-further-reference.md#key-performance-indicators-and-target-metrics).

entre otros.

**Recopilar estadísticas de tráfico del sitio web existente** : Esta información se puede extraer de los archivos de registro. Consulte Supervisión del rendimiento para obtener más información.

Estas cifras darán una indicación del tráfico actual (volumen y difusión) en el sitio web existente y pueden utilizarse para formar un punto de base para el nuevo sitio web.

**Recopilar estadísticas de tráfico de sitios web externos** - Si es posible, puede intentar recopilar estadísticas de tráfico de otros sitios web para compararlas, pero estas cifras no siempre se publican.

**Confirmar métricas de Target** - Las métricas se utilizan para definir mediciones cuantitativas de la calidad del sitio web, ya que representan los objetivos de rendimiento que se deben alcanzar.

Deben definirse al principio del proyecto, junto con el cliente. Consulte [Métricas de Target](/help/sites-developing/planning.md) para obtener más información.
