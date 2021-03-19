---
title: Prueba de aplicaciones móviles
seo-title: Prueba de aplicaciones móviles
description: Prueba de aplicaciones móviles
seo-description: nulo
uuid: 3b402d34-5cab-4280-b8b9-88ad9f8fc5e4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
discoiquuid: 5a98e1bd-f5c1-4f2f-ac02-dbd005dc1de7
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 0%

---


# Prueba de aplicaciones móviles{#testing-mobile-apps}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Dada la amplia gama de dispositivos en el mercado y los dispositivos que se lanzan, probar sus aplicaciones se ha vuelto extremadamente importante. Se trata de un área en la que la funcionalidad y la facilidad de uso pueden obtener críticas bajas en una tienda de aplicaciones, pero un único defecto puede provocar que la aplicación se desinstale. Se debe prestar atención especial a los planes de pruebas y a la garantía de calidad. El siguiente vínculo cubre muchos de los temas que deben abordarse en general, como identificar su entorno, definir casos de prueba, tipos de pruebas, supuestos, participación del cliente, etc. También se discuten herramientas para ayudar en el esfuerzo de prueba. Las herramientas internas, como [Hobbes](/help/sites-developing/hobbes.md), pueden ayudar con las pruebas de IU basadas en la web. [Duro ](/help/sites-developing/tough-day.md) Daycan resaltar sus instancias con una carga simulada. Si su entorno de prueba ya tiene experiencia con herramientas de terceros, como Selenium, estas también se pueden utilizar.

Al desarrollar una aplicación móvil, hay muchas preocupaciones nuevas específicas de los dispositivos que deben abordarse junto con las de las pruebas tradicionales.

* Funcional: ¿su aplicación cumple todos los requisitos?
* Uso: ¿Es la aplicación fácil de usar y comprender por su cliente?
* Rendimiento: ¿Qué sucede durante un pico en el uso? ¿Son los elementos de la aplicación, como los bornes y los carruseles, rápidos y no restan importancia a la experiencia?
* Fallo o interrupciones: ¿Qué sucede cuando hay una llamada o notificación entrante mientras la aplicación se está ejecutando? ¿Qué sucede si hay una interrupción o apagado de la red?
* Instalación y actualizaciones: ¿Cómo es la experiencia de instalación? ¿Cómo se eliminan las actualizaciones?
* Técnico: ¿Su aplicación consume demasiada energía de un dispositivo?
* Localización : ¿todas las áreas de la aplicación están traducidas?
* Certificación: ¿Se ha certificado su aplicación? ¿Pueden los clientes confiar en que cumple todos los requisitos legales de privacidad de datos?

Estas preguntas deben responderse durante las pruebas automatizadas y manuales.

## Pruebas automatizadas {#automated-testing}

Se debe realizar cierto grado de prueba automatizada para cubrir la variedad de tamaños de pantalla, restricciones de memoria, métodos de entrada y sistemas operativos. No solo cubre gran parte de los casos de prueba, sino que puede acelerar las pruebas de regresión cuando se introducen nuevas funciones o dispositivos. Lo ideal es que sus herramientas de automatización reduzcan o limiten la duplicación de esfuerzos. Utilice herramientas o marcos para que su esfuerzo de prueba sea aplicable en todas las plataformas. El gráfico siguiente muestra una estructura simplificada de un entorno de prueba tanto para las pruebas de IU basadas en web como para las pruebas de aplicaciones móviles. El lado izquierdo del gráfico muestra una serie de nodos Selenium con exploradores. SeleniumGrid puede almacenar pruebas de IU comunes basadas en web en cualquiera de estos nodos. El hub de Selenium también puede conectarse a Appium para realizar pruebas de aplicaciones en varias plataformas. Solo se muestran los simuladores, pero puede incorporar las utilidades adb, para Android y Xcode para dispositivos iOS. Los vínculos se proporcionan más adelante en este documento, donde puede encontrar detalles específicos para las herramientas mencionadas.

![imagen_1](assets/chlimage_1.jpeg)

## Pruebas manuales {#manual-testing}

Además de las pruebas automatizadas, la aplicación debe pasar por un ciclo de pruebas manuales. Los clientes que ejecuten la aplicación en un dispositivo real no pueden duplicarse mediante un script. Aquí también tiene muchas opciones. Puede utilizar una plataforma, como HockeyApp, para definir quién tiene acceso y recabar comentarios. O bien, puede subcontratar todo el proceso a un servicio como UTest, ElusiveStars o Testin. Si tiene un grupo de probadores internos, pero no tiene variaciones en los dispositivos, hay servicios en la nube donde puede realizar pruebas manuales en su grupo de dispositivos. Uno de esos servicios que ofrece es SauceLabs. También puede crear aplicaciones de forma remota a PhoneGap Enterprise e instalarlas en dispositivos locales como un nivel de aceptación, prueba o descenso. Consulte el sitio web [PhoneGap](https://phonegap.com/) para conocer las últimas funciones y documentación. Cualquiera que sea el enfoque, las pruebas manuales deben realizarse;

* llegue a un gran destinatario de testers,
* realizar pruebas con un gran grupo de dispositivos (idealmente dispositivos reales, pero simuladores/emuladores si no hay dispositivos reales disponibles),
* proporcionar comentarios informativos:

   * informes de bloqueo,
   * análisis/seguimiento,
   * usabilidad,
   * ámbitos de atención,
   * rendimiento,
   * consumo de datos/energía, etc.

## Herramientas {#tools}

Hay una amplia gama de herramientas disponibles para probar aplicaciones móviles. La elección de los que se van a usar se basará en su situación específica: características, precio, asistencia, cobertura, etc. A continuación se describen brevemente algunas de las herramientas y servicios disponibles.

**Selenio**

* Marco que incluye una API para secuencias de comandos de prueba para alimentar WebDriver y controlar varios navegadores.
* Puede utilizarlo junto con Appium para realizar pruebas en dispositivos reales.
* SeleniumGrid dirige pruebas entre nodos para pruebas paralelas.
* Selenium IDE ayuda a reducir la escritura de mayúsculas y minúsculas en la prueba.

Para obtener más información, consulte [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**Testdroid**

* Servicio de pruebas basado en la nube con vínculos de integración continuos y pruebas de dispositivos reales.
* Incluye un rastreador de aplicaciones que comprueba la compatibilidad del dispositivo, analiza registros, atraviesa vistas, toma capturas de pantalla y supervisa el rendimiento.

Para obtener más información, consulte [https://testdroid.com/](https://testdroid.com/).

**Appium**

* Appium es un popular marco entre plataformas para automatizar pruebas móviles.
* Además, se incluye un inspector con capacidades de registro para ayudar a codificar los casos de prueba.

Para obtener más información, consulte [https://appium.io/](https://appium.io/).

**SauceLabs**

* SauceLabs proporciona pruebas basadas en la nube y se integra con una integración continua.
* Las pruebas se ejecutan en su entorno de nube automáticamente o puede iniciar un dispositivo o plataforma en particular y realizar pruebas manuales para ayudar a depurar problemas.

Para obtener más información, consulte [https://saucelabs.com/](https://saucelabs.com/).

**AppTestNow**

* Servicio de externalización que probará sus aplicaciones móviles.
* Incluye un gran grupo de dispositivos y ofrece una amplia gama de tipos de pruebas: rendimiento, calidad, funcionalidad, certificación, localización, consumo de datos, etc.

Para obtener más información, consulte [https://www.apptestnow.com](https://www.apptestnow.com/).

**Aplicación de hockey**

* HockeyApp se encuentra dentro de la prueba manual, donde la aplicación móvil se envía a una tienda de aplicaciones personal donde los probadores pueden descargarla y probarla.

Para obtener más información, consulte [https://hockeyapp.net/features/](https://hockeyapp.net/features/).

**Jenkins**

* Aunque no es una herramienta de prueba, Jenkins es un marco de integración continua que proporciona la base para pruebas automatizadas. Hay varios complementos de terceros disponibles para ampliar la funcionalidad. Por ejemplo, el complemento SeleniumGrid proporciona una interfaz de usuario para ayudar a administrar el hub y los nodos de Selenium.

Para obtener más información, consulte [https://jenkins-ci.org/](https://jenkins-ci.org/) y [https://wiki.jenkins-ci.org/display/JENKINS/Plugins](https://wiki.jenkins-ci.org/display/JENKINS/Plugins).
