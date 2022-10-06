---
title: Herramientas de prueba y seguimiento
seo-title: Testing and Tracking Tools
description: AEM proporciona un marco para probar la interfaz de usuario de los componentes y un mecanismo para probar y depurar componentes
seo-description: AEM provides a framework for testing component UI and a mechanism for testing and debugging components
uuid: 12abedb5-4ee7-4389-9340-e628adbbc053
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 3cf0fd8d-7fc8-468a-bb1e-1debb68a82a5
docset: aem65
exl-id: bb5d1c7c-56ce-4d1e-a3cb-4e74d6922137
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 1%

---

# Herramientas de prueba y seguimiento{#testing-and-tracking-tools}

## Pruebas {#testing}

AEM proporciona lo siguiente:

* [un marco para probar la interfaz de usuario de los componentes](/help/sites-developing/hobbes.md).
* [un mecanismo para probar y depurar componentes](/help/sites-developing/developer-mode.md).

Las siguientes son dos herramientas de prueba de código abierto:

**Selenio**

Selenium se utiliza para pruebas de funciones en un explorador con un usuario por actividad. Registra los pasos de prueba (clics) como tablas de HTML o clases Java.

Para obtener más información, consulte [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**JMeter**

JMeter se utiliza para rastrear solicitudes y puede utilizarse para pruebas funcionales, de rendimiento y de estrés.

Para obtener más información, consulte [https://jakarta.apache.org/jmeter/](https://jakarta.apache.org/jmeter).

También existen muchas herramientas propietarias para automatizar pruebas y administrar planes de prueba.

### Seguimiento {#tracking}

Las siguientes herramientas están fácilmente disponibles. Sin embargo, un problema clave en todos los casos es la disponibilidad de los datos para todos los miembros del equipo del proyecto: socio y cliente.

**Bugzilla**

Un sistema de seguimiento de errores que puede configurarse según sus propios requisitos.

**Hojas de cálculo**

Aunque no se trata específicamente de una herramienta de seguimiento de errores, las hojas de cálculo suelen *mis* se utilizan para este fin, ya que son fáciles de entender y la mayoría de los usuarios tienen experiencia en su funcionalidad.

Si se utilizan para el seguimiento, entonces:

* deben mantenerse simples.
* el número de hojas de cálculo individuales debe reducirse al mínimo.
* deben actualizarse periódicamente.
* solo se debe mantener una copia maestra y todos deben saber dónde está la copia maestra.
* deben ser accesibles para todos los miembros del proyecto.
* si la seguridad es un problema (a menudo ocurre en grandes empresas) y el acceso común no es posible, las copias se pueden distribuir siempre que todos entiendan que se trata de copias y no se puedan actualizar.

De nuevo, existen muchas herramientas propietarias para rastrear errores y requisitos de funciones.
