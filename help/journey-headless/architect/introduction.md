---
title: Recorrido de arquitecto de contenido de AEM Headless
description: Introducción a las funciones potentes, flexibles y sin encabezado de Adobe Experience Manager y cómo modelar el contenido de su proyecto.
exl-id: 49ba0d6d-dde4-42e2-92fd-c7655c0eebc0
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 3%

---

# Modelado de contenido para Headless con AEM: introducción {#architect-headless-introduction}

En esta parte del [recorrido de arquitecto de contenido sin encabezado de AEM](overview.md), puede conocer los conceptos (básicos) y la terminología necesarios para comprender el modelado de contenido para la entrega de contenido sin encabezado con Adobe Experience Manager (AEM).

Este documento le ayuda a comprender la entrega de contenido sin encabezado, cómo AEM admite sin encabezado y cómo se modela el contenido para que no tenga encabezado. Después de leer, debería haber logrado lo siguiente:

* Comprender los conceptos básicos de la entrega de contenido sin encabezado.
* Familiarícese con cómo AEM admite el modelado de contenido y sin encabezado.

## Objetivo {#objective}

* **Audiencia**: Principiante
* **Objetivo**: Introduzca los conceptos y la terminología relevantes para el Modelado de contenido sin encabezado.

## Entrega de contenido de pila completa {#full-stack}

Desde el surgimiento de los sistemas de administración de contenido (CMS) a gran escala, fáciles de usar, las organizaciones los han aprovechado como una ubicación central para administrar mensajes, marcas y comunicaciones. El uso del CMS como punto central para la administración de experiencias mejoró la eficiencia al eliminar la necesidad de duplicar tareas en sistemas dispares.

![El clásico CMS de pila completa](/help/journey-headless/developer/assets/full-stack.png)

En un CMS de pila completa, toda la funcionalidad para manipular contenido está en el CMS. Las características del sistema componen diferentes componentes de la pila de CMS. La solución de pila completa tiene muchas ventajas.

* Hay un sistema para mantener.
* El contenido se administra de forma centralizada.
* Todos los servicios del sistema están integrados.
* La creación de contenido es perfecta.

Por lo tanto, si se necesita añadir un nuevo canal o admitir nuevos tipos de experiencias, se pueden insertar uno o más componentes nuevos en la pila y solo hay un lugar donde realizar cambios.

![Adición de un nuevo canal a la pila](/help/journey-headless/developer/assets/adding-channel.png)

Sin embargo, la complejidad de las dependencias dentro de la pila se hace evidente rápidamente, ya que otros elementos de la pila deben ajustarse para adaptarse a los cambios.

## La cabeza sin cabeza {#the-head}

El jefe de cualquier sistema es generalmente el procesador de salida de ese sistema, normalmente en forma de GUI u otra salida gráfica.

Cuando hablamos de un CMS sin objetivos, el CMS administra el contenido y continúa entregándolo a los consumidores. Sin embargo, solo entregando la variable **contenido** de forma estandarizada, un CMS sin periféricos omite el procesamiento de salida final, dejando el **presentación** del contenido al servicio consumidor.

![CMS sin encabezado](/help/journey-headless/developer/assets/headless-cms.png)

Los servicios que consumen, ya sean experiencias de AR, una tienda web, experiencias móviles, aplicaciones web progresivas (PWA), etc., reciben contenido del CMS sin periféricos y proporcionan su propia renderización. Se ocupan de proporcionar sus propias cabezas para su contenido.

Omitir la cabeza simplifica el CMS al eliminar la complejidad. Al hacerlo, también se traslada la responsabilidad de procesar el contenido a los servicios que realmente necesitan el contenido y que a menudo son más adecuados para dicha renderización.

## Modelado de contenido {#content-modeling}

El modelado de contenido (también conocido como modelado de datos) es su especialidad, por lo que ¿qué debe tenerse en cuenta al modelar para trabajar sin encabezado?

Para que las aplicaciones sin encabezado puedan acceder a su contenido y hacer algo con él, el contenido realmente necesita tener una estructura predefinida. Sería posible tener tu contenido como forma libre, pero haría vida *very* complicada para las aplicaciones.

Para AEM usted, como arquitecto de contenido, realizará el modelado de contenido para diseñar una gama de **Modelos de fragmento de contenido**. Definen la estructura utilizada cuando los autores de contenido crean la variable **Fragmentos de contenido** que contienen el contenido.

### Acceso al contenido {#access-content}

Esto es más un detalle de desarrollo - pero puede que le interese, sólo para completar la historia.

Una vez que haya creado los modelos de fragmento de contenido y que los autores los hayan utilizado para generar el contenido, las aplicaciones sin encabezado tendrán que acceder a este contenido.

Adobe Experience Manager (AEM) puede acceder selectivamente a sus fragmentos de contenido mediante la API de GraphQL de AEM para devolver solo el contenido necesario. Con la API un desarrollador puede formular consultas que seleccionen contenido específico. Este proceso de selección se basa en *your* Modelos de fragmento de contenido.

Esto significa que el proyecto puede realizar una entrega sin objetivos de contenido estructurado para su uso en las aplicaciones.

## Siguientes pasos {#whats-next}

Ahora que ha aprendido los conceptos y la terminología, el siguiente paso es [Conozca los conceptos básicos del modelado con modelos de fragmentos de contenido](basics.md).

## Recursos adicionales {#additional-resources}

* recorrido para desarrolladores AEM sin encabezado
   * [Obtenga Información Sobre El Desarrollo Sin Cabeza De CMS](/help/journey-headless/developer/learn-about.md)
   * [Aprenda a modelar el contenido](/help/journey-headless/developer/model-your-content.md)
