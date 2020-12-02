---
title: Herramientas de prueba y seguimiento
seo-title: Herramientas de prueba y seguimiento
description: AEM proporciona un marco para probar la interfaz de usuario de los componentes y un mecanismo para probar y depurar los componentes
seo-description: AEM proporciona un marco para probar la interfaz de usuario de los componentes y un mecanismo para probar y depurar los componentes
uuid: 12abedb5-4ee7-4389-9340-e628adbbc053
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 3cf0fd8d-7fc8-468a-bb1e-1debb68a82a5
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# Herramientas de prueba y seguimiento{#testing-and-tracking-tools}

## Pruebas {#testing}

AEM proporciona:

* [un marco para probar la interfaz de usuario](/help/sites-developing/hobbes.md) del componente.
* [un mecanismo para probar y depurar componentes](/help/sites-developing/developer-mode.md).

Las siguientes son dos herramientas de prueba de código abierto:

**Selenio**

El selenio se utiliza para probar funciones en un navegador con un usuario por actividad. Registra los pasos de prueba (clics) como tablas HTML o clases Java.

Para obtener más información, consulte [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**JMeter**

JMeter se utiliza para rastrear solicitudes y se puede utilizar para pruebas funcionales, de rendimiento y de estrés.

Para obtener más información, consulte [https://jakarta.apache.org/jmeter/](https://jakarta.apache.org/jmeter).

También hay muchas herramientas propias para automatizar pruebas y administrar planes de pruebas.

### Seguimiento {#tracking}

Las siguientes herramientas están fácilmente disponibles. Sin embargo, un problema clave en todos los casos es la disponibilidad de los datos para todos los miembros del equipo del proyecto: socio y cliente.

**Bugzilla**

Un sistema de seguimiento de errores que puede configurarse según sus propios requisitos.

**Hojas de cálculo**

Aunque no se trata específicamente de una herramienta de seguimiento de errores, las hojas de cálculo suelen *mis* utilizarse para este fin, ya que son fáciles de comprender y la mayoría de los usuarios tienen experiencia en su funcionalidad.

Si se utilizan para el seguimiento, entonces:

* deben ser simples.
* el número de hojas de cálculo individuales debe reducirse al mínimo.
* deben actualizarse periódicamente.
* sólo se debe mantener una copia maestra y todos deben saber dónde está la copia maestra.
* deben ser accesibles para todos los miembros del proyecto.
* si la seguridad es un problema (a menudo ocurre en grandes compañías) y no es posible el acceso común, las copias se pueden distribuir siempre que todos entiendan que se trata de copias y no se puedan actualizar.

Nuevamente, existen muchas herramientas de propiedad para rastrear errores y requisitos de características.
