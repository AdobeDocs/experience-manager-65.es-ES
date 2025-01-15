---
title: Prueba de aplicaciones móviles
description: Obtenga información sobre cómo automatizar o probar manualmente sus aplicaciones móviles con varias herramientas.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
exl-id: e10e1904-7016-4eb0-9408-36297285f378
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 0%

---

# Prueba de aplicaciones móviles{#testing-mobile-apps}

{{ue-over-mobile}}

Dada la amplia gama de dispositivos en el mercado y los dispositivos que se están lanzando, la prueba de sus aplicaciones se ha vuelto imprescindible. Esta es un área en la que la funcionalidad y la facilidad de uso pueden recibir pocas críticas en una tienda de aplicaciones, pero un solo defecto puede provocar que se desinstale la aplicación. Se debe prestar mucha atención a sus planes de pruebas y a la garantía de calidad. El siguiente vínculo abarca muchos de los temas que se deben abordar en general, como la identificación del entorno, la definición de casos de prueba, los tipos de pruebas, las suposiciones y la participación del cliente. También se analizan las herramientas que ayudan en el esfuerzo de prueba. Las herramientas internas, como [Hobbes](/help/sites-developing/hobbes.md), pueden ayudar con las pruebas de IU basadas en la web. [Día difícil](/help/sites-developing/tough-day.md) puede sobrecargar las instancias con una carga simulada. Si el entorno de prueba ya tiene experiencia con herramientas de terceros, como Selenium, también se pueden utilizar.

Al desarrollar una aplicación móvil, hay muchas preocupaciones nuevas específicas de los dispositivos que deben abordarse junto con las de las pruebas tradicionales.

* Funcional: ¿su aplicación cumple todos los requisitos?
* Usabilidad: ¿Es su cliente fácil de usar y entender la aplicación?
* Rendimiento: ¿Qué sucede durante un pico en el uso? ¿Los elementos de la aplicación, como los deslizamientos y los carruseles, son rápidos y no le restan importancia a la experiencia?
* Fallo o interrupciones: ¿Qué sucede cuando hay una llamada o una notificación entrantes mientras la aplicación se está ejecutando? ¿Qué sucede si hay una interrupción de la red o una desconexión?
* Instalación y actualizaciones. ¿Cómo es la experiencia de instalación? ¿Cómo se eliminan las actualizaciones?
* Técnico: ¿Su aplicación consume demasiada energía de un dispositivo?
* Localización: ¿Se traducen todas las áreas de la aplicación?
* Certificación: ¿Se ha certificado su aplicación? ¿Pueden los clientes confiar en que sigue todos los requisitos legales de privacidad de datos?

Estas preguntas deben responderse durante las pruebas automatizadas y manuales.

## Pruebas automatizadas {#automated-testing}

Se debe realizar cierto grado de pruebas automatizadas para cubrir la variedad de tamaños de pantalla, restricciones de memoria, métodos de entrada y sistemas operativos. No solo cubre muchos de los casos de prueba, sino que puede acelerar las pruebas de regresión cuando se introducen nuevas funciones o dispositivos. Lo ideal es que sus herramientas de automatización reduzcan o limiten la duplicación de esfuerzos. Utilice herramientas o marcos de trabajo para que el esfuerzo de prueba sea aplicable a todas las plataformas. El siguiente gráfico muestra una estructura simplificada de un entorno de prueba tanto para las pruebas de interfaz de usuario basadas en la web como para las pruebas de aplicaciones móviles. La parte izquierda del gráfico muestra una serie de nodos de Selenium con exploradores. SeleniumGrid puede agrupar pruebas de IU comunes basadas en la web para cualquiera de estos nodos. Selenium hub también se puede conectar a Appium para realizar pruebas de aplicaciones en varias plataformas. Solo se muestran los simuladores, pero puede incorporar las utilidades adb, para Android™ y Xcode para dispositivos iOS. Los vínculos se proporcionan más adelante en este documento, donde puede encontrar detalles específicos para las herramientas mencionadas.

![chlimage_1](assets/chlimage_1.jpeg)

## Pruebas manuales {#manual-testing}

Además de las pruebas automatizadas, la aplicación debe pasar por un ciclo de pruebas manuales. Los clientes que ejecuten la aplicación en un dispositivo real no se pueden duplicar mediante una secuencia de comandos. Aquí también tiene muchas opciones. Puede utilizar una plataforma, como HockeyApp, para definir quién tiene acceso y recopilar comentarios. O bien, puede subcontratar todo el proceso a un servicio como UTest, ElusiveStars o Testin. Si tiene un grupo de probadores internos, pero le falta variación de dispositivos, hay servicios en la nube donde puede realizar pruebas manuales en su grupo de dispositivos. Uno de estos servicios que proporciona esto es SauceLabs. También puede crear aplicaciones de forma remota en PhoneGap Enterprise e instalarlas en dispositivos locales como nivel de aceptación, prueba o degradación. Consulte el sitio web de PhoneGap (`https://phonegap.com/`) para conocer las últimas funciones y documentación. Sea cual sea el enfoque, las pruebas manuales deben hacer lo siguiente:

* alcanzó un gran objetivo de probadores,
* realizar pruebas con un gran grupo de dispositivos (idealmente, dispositivos reales, pero simuladores/emuladores si no hay dispositivos reales disponibles),
* proporcione comentarios informativos:

   * informes de bloqueo,
   * análisis/seguimiento,
   * facilidad de uso,
   * áreas de atención,
   * rendimiento,
   * consumo de datos/energía, etc.

## Herramientas {#tools}

Hay una amplia gama de herramientas disponibles para probar aplicaciones móviles. La elección de los que se van a utilizar debe basarse en su situación específica: características, precio, asistencia, cobertura, etc. A continuación se ofrece una breve descripción de algunas de las herramientas y servicios disponibles.

**Selenio**

* Marco de trabajo que incluye una API para scripts de prueba para alimentar WebDriver y controlar varios exploradores.
* Puede utilizar esto con Appium para probar en dispositivos reales.
* SeleniumGrid dirige las pruebas entre nodos para pruebas paralelas.
* Selenium IDE ayuda a reducir la escritura de casos de prueba.

Para obtener más información, consulte [https://www.selenium.dev/](https://www.selenium.dev/).

**Testdroid**

* Un servicio de pruebas basado en la nube con enlaces de integración continua y pruebas reales de dispositivos.
* Se incluye un rastreador de aplicaciones que comprueba la compatibilidad del dispositivo, analiza los registros, atraviesa las vistas, toma capturas de pantalla y supervisa el rendimiento.

Para obtener más información, consulte [https://testdroid.com/](https://testdroid.com/).

**Apio**

* Appium es un popular marco multiplataforma para automatizar pruebas móviles.
* Además, se incluye un inspector con capacidades de registro para ayudar a codificar casos de prueba.

Para obtener más información, consulte [https://appium.io/](https://appium.io/).

**SauceLabs**

* SauceLabs proporciona pruebas basadas en la nube e integra con una integración continua.
* Las pruebas se ejecutan en su entorno de nube automáticamente o puede iniciar un dispositivo o plataforma en particular y realizar pruebas manuales para depurar los problemas.

Para obtener más información, consulte [https://saucelabs.com/](https://saucelabs.com/).

<!-- **AppTestNow**

* An outsourcing service that tests your mobile apps.
* Included is a large pool of devices and offers a wide range of types of testing: performance, quality, functional, certification, localization, data consumption, and so on.

For more information, see [https://apptestnow.com/](https://apptestnow.com/). -->

**Aplicación de hockey**

* HockeyApp entra dentro de las pruebas manuales en las que la aplicación móvil se envía a una tienda de aplicaciones personal en la que los probadores pueden descargarla y probarla.

Para obtener más información, consulte [https://hockeyapp.net/features/](https://hockeyapp.net/features/).

**Jenkins**

* Aunque no es una herramienta de prueba, Jenkins es un marco de integración continua que proporciona la base para las pruebas automatizadas. Hay numerosos complementos de terceros disponibles para ampliar la funcionalidad. Por ejemplo, el complemento SeleniumGrid proporciona una interfaz de usuario para ayudar a administrar el concentrador y los nodos de Selenium.

Para obtener más información, consulte [https://www.jenkins.io/](https://www.jenkins.io/) y [https://plugins.jenkins.io/](https://plugins.jenkins.io/).
