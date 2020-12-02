---
title: Planificación
seo-title: Planificación
description: Qué necesita saber para planificar la prueba
seo-description: Qué necesita saber para planificar la prueba
uuid: 29b1127a-da85-46ed-98e7-1c983eb40cfe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 12268c43-93f9-42c1-8dd7-f17f9ae2219b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---


# Planificación{#planning}

Este documento describe lo que debe saber para planificar la prueba. Además, debe responder a estas preguntas antes de realizar las pruebas:

* [¿Qué Entornos de prueba serán necesarios?](/help/sites-developing/test-environments.md)
* [Definición de los casos de prueba](/help/sites-developing/test-cases.md)
* [Pruebas: ¿cuándo y con quién?](/help/sites-developing/when-who.md)

## Antes de comenzar {#before-you-start}

Antes de realizar el inicio con la análisis real y la definición de las pruebas, revise la siguiente información:

**Arquitectura**  de AEM: consulte Conceptos básicos para presentarse a la arquitectura y los principios básicos de AEM.

**Documentación** : consulte cualquiera de las secciones de documentación, o artículos sobre cómo hacerlo, para obtener más información.

**Principios básicos de las pruebas** : debe conocer los principios básicos de las pruebas de software y el aseguramiento de la calidad. Es preferible que tenga experiencia en la prueba de proyectos.

Hay muchos sitios web, libros y cursos que tratan de esos principios y por lo tanto no se tratarán en detalle en este documento.

**Suposiciones para evitar** : el mayor supuesto (hecho regularmente) es que su sitio web tendrá que atender millones de solicitudes cada día. En determinadas circunstancias esto puede ser cierto, pero no puede suponerse.

Aunque los números futuros no se pueden predecir con una precisión del 100 %, observar el sitio existente y el tráfico experimentado dará una buena indicación. Luego puede hacer que las estimaciones dependan del factor por el que espera / espera que el tráfico aumente.

**Compromiso con la calidad** - Es de suma importancia que cualquiera que realice pruebas sea neutral y simplemente informe los resultados de las pruebas realizadas.

El director del proyecto tiene la responsabilidad de decidir e iniciar las acciones que dependan de los resultados.

**Involucrarse** : Aunque es responsabilidad del director del proyecto asegurar que todas las partes participen plenamente en cualquier reunión (estado, talleres, etc.), también debe intentar participar lo antes posible en el ciclo del proyecto, incluidos los procesos de recopilación de información y análisis de requisitos.

**Involucrar al cliente** : en un tema similar, trate de involucrar al cliente (cuando sea posible) al definir los casos de prueba y el plan.

## Tipos de pruebas {#types-of-tests}

Existen varias clasificaciones estándar de pruebas que son apropiadas para su uso al probar un proyecto AEM. Debe estar familiarizado con ellos para decidir qué utilizará:

>[!NOTE]
>
>Estos se enumeran en su orden cronológico de aplicación.

**Pruebas**  de unidades: pruebas (generalmente) realizadas por el equipo de desarrollo para garantizar que los elementos individuales se comportan correctamente, aunque de forma aislada.

**Pruebas**  de integración: módulos de pruebas cuando se combinan. Estas pruebas se realizan después de la prueba unitaria, pero antes de la prueba del sistema.

**Pruebas**  de humo: Son pruebas rápidas y sucias que se utilizan para probar que el software se está ejecutando y que la funcionalidad de alto nivel está disponible. Los detalles no se prueban.

**Pruebas**  funcionales: se utilizan para probar la funcionalidad del software. Se diseñará una serie de pruebas que abarcarán todos los detalles funcionales, con datos esperados e inesperados y/o erróneos.

Las pruebas en caja negra son pruebas funcionales de una unidad completa, componente o módulo, realizadas sin conocer el funcionamiento interno del elemento en cuestión.

**Pruebas**  del sistema: comprueban todo el sistema una vez que se ha integrado e instalado en una plataforma adecuada.

Ellos prueban la funcionalidad en forma de caja negra.

**Pruebas**  de rendimiento: las pruebas de rendimiento son cruciales cuando se realiza una prueba de AEM.

Se utilizan para ilustrar el rendimiento en diferentes condiciones:

* Normal

   Condiciones que el sitio experimentará durante el 90% del tiempo, por ejemplo. Por ejemplo, cuando sólo una proporción de los autores utiliza el sistema.

* Pico

   Condiciones que se experimentarán durante un período proporcionalmente breve debido a circunstancias especiales; por ejemplo, cuando todos los autores utilizan el sistema al mismo tiempo o cuando se publica contenido nuevo y un número mayor de visitantes vista al sitio.

* Extremo

   Se puede utilizar para emular la previsión de rendimiento cuando se publica contenido nuevo y extremadamente interesante en el sitio web. Luego se puede ver un pico extremo -aunque esto puede no ser siempre totalmente predecible.

   Estas circunstancias se ven a veces cuando se ponen a disposición boletos para eventos específicos, o cuando se publica un muy esperado sitio web por primera vez.

Los resultados se utilizan para ajustar la aplicación.

**Pruebas**  de esfuerzo: se realizan pruebas de estrés para confirmar el comportamiento de un componente o una aplicación en condiciones extremas. En particular, estas pruebas se utilizan para mostrar cómo se deteriora el comportamiento, cuándo falla el elemento y cómo.

**Pruebas**  de regresión- Las pruebas de regresión se utilizan para confirmar que la funcionalidad ya probada en una versión anterior del software sigue funcionando correctamente.

Las pruebas de regresión son buenas candidatas para la automatización (si es posible) para garantizar que se puedan repetir de manera rápida y coherente.

**Pruebas**  de aceptación: las pruebas de aceptación son una categoría especial, ya que se utilizan para indicar la aceptación del cliente del proyecto.

La lista de las pruebas de aceptación puede contener una combinación de pruebas de las distintas categorías anteriores y se seleccionan para comprobar que el proyecto cumple los requisitos del cliente

Consulte [Aceptación y desactivación](/help/sites-developing/acceptance-signoff.md) para obtener más detalles.

## Introducción {#getting-started}

Antes de comenzar con los casos de prueba y el plan de pruebas detallados, puede:

**Definir los objetivos** : defina los objetivos de alto nivel para que sirvan de punto de partida para el ajuste a medida que avanza la prueba. Desea:

* Pruebe la funcionalidad según la especificación detallada de requisitos.
* Probar el rendimiento según las [métricas de Destinatario](/help/managing/best-practices-further-reference.md#key-performance-indicators-and-target-metrics).

entre otros.

**Recopilar estadísticas de tráfico del sitio web**  existente: esta información se puede extraer de los archivos de registro; consulte Monitoreo de rendimiento para obtener más detalles.

Estas cifras darán una indicación del tráfico actual (volumen y difusión) en el sitio web existente y pueden utilizarse para formar un punto de base para el nuevo sitio web.

**Recopilar estadísticas de tráfico de sitios web**  externos: Si es posible, puede intentar recopilar estadísticas de tráfico de otros sitios web para compararlas, pero estas cifras no siempre se publican.

**Confirmar métricas**  de Destinatario: las métricas se utilizan para definir mediciones cuantitativas de la calidad del sitio web, ya que representan los objetivos de rendimiento que se deben alcanzar.

Deben definirse en el inicio del proyecto, junto con el cliente. Consulte [Métricas de Destinatario](/help/sites-developing/planning.md) para obtener más información.
