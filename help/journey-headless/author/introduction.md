---
title: recorrido de autor de contenido sin encabezado de AEM
description: Introducción a las funciones potentes, flexibles y sin encabezado de Adobe Experience Manager y a cómo crear contenido para su proyecto.
source-git-commit: 38525b6cc14e9f6025564c060b8cfb4f9e0ea473
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# Creación para usuarios sin encabezado con AEM: una introducción {#author-headless-introduction}

En esta parte del [recorrido de autor de contenido sin encabezado de AEM](overview.md), puede conocer los conceptos (básicos) y la terminología necesarios para comprender la creación de contenido para la entrega de contenido sin encabezado con Adobe Experience Manager (AEM).

## Objetivo {#objective}

* **Audiencia**: Principiante
* **Objetivo**: Introduzca los conceptos y la terminología relevantes para la creación sin encabezado.

## Sistema de gestión de contenido (CMS) {#content-management-system}

¿Qué es un sistema de administración de contenido?

Un sistema de gestión de contenido (CMS) es exactamente lo que dice: un sistema informático utilizado para administrar contenido. Es un poco general, por lo que para ser más preciso, se utiliza (normalmente) para administrar el contenido que desea poner a disposición en los sitios web.

## CMS sin encabezado {#headless-cms}

Sin encabezado es un término utilizado para describir sistemas que efectivamente desasocian el contenido de la forma en que se muestra ese contenido en la web.

Tradicionalmente, administraría su contenido en un CMS, y el mismo CMS sería responsable de procesar ese contenido en sus páginas web.

Ahora, sin encabezado significa que el conjunto de contenido se puede administrar en el CMS y luego acceder a él mediante una o más aplicaciones (independientes).

Esto significa que el contenido se puede entregar a cualquier dispositivo, en una amplia gama de formatos. Esto hace que todo el proceso sea mucho más flexible y también significa que no necesita preocuparse por el diseño y el formato.

>[!NOTE]
>
>Si desea obtener más información sobre los detalles técnicos de CMS sin encabezado, puede leer más en Información sobre el desarrollo sin encabezado de CMS.

## Adobe Experience Manager {#aem-cms}

Entonces, ¿qué es AEM?

En primer lugar, AEM es un sistema de gestión de contenido con una amplia gama de funciones que también se pueden personalizar para satisfacer sus necesidades.

Esto significa que se puede utilizar como:

* CMS sin encabezado
   * Para que no tenga encabezado, el contenido se puede crear como **Fragmentos de contenido**.
Son elementos de contenido independientes a los que se puede acceder directamente desde una amplia gama de aplicaciones, ya que tienen una estructura predefinida basada en **Modelos de fragmento de contenido**.
Esto significa que el contenido puede llegar a una amplia gama de dispositivos, en una amplia gama de formatos y con una amplia selección de funcionalidades.
(Y como doble golpe, estos fragmentos también se pueden utilizar al construir páginas web AEM, si lo desea).

* CMS &quot;tradicional&quot;
   * El contenido se crea para páginas web mediante una serie de componentes que definen cómo se representará el contenido en el sitio web. Incluso aquí AEM es extremadamente flexible, ya que el equipo del proyecto puede desarrollar componentes personalizados.

## Modelado de contenido {#content-modeling}

Por lo tanto, el modelado de contenido (también conocido como modelado de datos) es otro término técnico. ¿Por qué debería interesarle como autor?

Para que las aplicaciones sin encabezado puedan acceder a su contenido y hacer algo con él, su contenido realmente necesita tener una estructura predefinida. Sería posible tener tu contenido como forma libre, pero haría vida *very* complicada para las aplicaciones.

Básicamente, el proceso de definición de la estructura a la que se adhiere el contenido implica diseñar un modelo, que se denomina modelado de datos.

Para AEM la función de arquitecto de contenido (normalmente una persona diferente), realizará el modelado de datos para diseñar una serie de **Modelos de fragmento de contenido** - que luego utiliza como base para el contenido mediante **Fragmentos de contenido**.

>[!NOTE]
>
>Si desea obtener más información sobre el modelado de datos, puede leer más en el Recorrido AEM Arquitecto de contenido sin encabezado .

## Siguientes pasos {#whats-next}

Ahora que ha aprendido los conceptos y la terminología, el siguiente paso es [Descubra los conceptos básicos de la creación de fragmentos de contenido](basics.md). Esto introducirá la gestión básica de AEM junto con cómo crear fragmentos de contenido.

## Recursos adicionales {#additional-resources}

* recorrido para desarrolladores AEM sin encabezado
   * [Obtenga Información Sobre El Desarrollo Sin Cabeza De CMS](/help/journey-headless/developer/learn-about.md)

* [recorrido de arquitecto de contenido sin encabezado de AEM](/help/journey-headless/architect/overview.md)

* [AEM Recorrido de traducción de contenido sin encabezado](/help/journey-headless/translation/overview.md)
