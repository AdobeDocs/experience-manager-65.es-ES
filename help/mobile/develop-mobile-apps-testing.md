---
title: Prueba de aplicaciones móviles
seo-title: Prueba de aplicaciones móviles
description: nulo
seo-description: nulo
uuid: 3b402d34-5cab-4280-b8b9-88ad9f8fc5e4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
discoiquuid: 5a98e1bd-f5c1-4f2f-ac02-dbd005dc1de7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Prueba de aplicaciones móviles{#testing-mobile-apps}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Dada la amplia variedad de dispositivos en el mercado y los que se lanzan, probar sus aplicaciones se ha vuelto extremadamente importante. Este es un área en la que la funcionalidad y la facilidad de uso pueden obtener críticas bajas en una tienda de aplicaciones, pero un único defecto puede provocar la desinstalación de la aplicación. Se debe prestar atención especial a los planes de pruebas y al control de calidad. El siguiente vínculo abarca muchos de los temas que deben tratarse en general, como identificar su entorno, definir casos de prueba, tipos de pruebas, supuestos, participación del cliente, etc. También se analizan las herramientas para ayudar en el esfuerzo de prueba. Las herramientas internas, como [Hobbes](/help/sites-developing/hobbes.md), pueden ayudarle con las pruebas de IU basadas en la web. [El día](/help/sites-developing/tough-day.md) duro puede resaltar las instancias con una carga simulada. Si su entorno de prueba ya tiene experiencia con herramientas de terceros, como Selenium, estas también se pueden usar.

Al desarrollar una aplicación móvil, hay muchas nuevas preocupaciones específicas de los dispositivos que deben abordarse junto con las de las pruebas tradicionales.

* Funcional: ¿Su aplicación cumple todos los requisitos?
* Facilidad de uso: ¿Su cliente puede utilizar y comprender la aplicación fácilmente?
* Rendimiento: ¿Qué ocurre durante un pico de uso? ¿Los elementos de la aplicación, como los barridos y los carruseles, son rápidos y no reducen la experiencia?
* Error o interrupciones: ¿Qué sucede cuando hay una llamada o notificación entrante mientras la aplicación se está ejecutando? ¿Qué sucede si se produce una interrupción de la red o una interrupción de la alimentación?
* Instalación y actualizaciones: ¿Cómo se lleva a cabo la instalación? ¿Cómo se eliminan las actualizaciones?
* Técnico: ¿La aplicación consume demasiada energía de un dispositivo?
* Localización: ¿Se traducen todas las áreas de la aplicación?
* Certificación: ¿Se ha certificado su aplicación? ¿Pueden los clientes confiar en que cumple todos los requisitos legales de privacidad de datos?

Estas preguntas deben responderse durante las pruebas automáticas y manuales.

## Pruebas automatizadas {#automated-testing}

Se debe realizar cierto grado de pruebas automatizadas para abarcar la variedad de tamaños de pantalla, limitaciones de memoria, métodos de entrada y sistemas operativos. No sólo cubre gran parte de los casos de prueba, sino que puede acelerar las pruebas de regresión cuando se introducen nuevas funciones o dispositivos. Idealmente, las herramientas de automatización deberían reducir o limitar la duplicación de esfuerzos. Utilice herramientas o marcos para que su esfuerzo de prueba sea aplicable en todas las plataformas. En el siguiente gráfico se muestra una estructura simplificada de un entorno de prueba tanto para las pruebas de IU basadas en la web como para las pruebas de aplicaciones móviles. El lado izquierdo del gráfico muestra una serie de nodos Selenium con exploradores. SeleniumGrid puede crear pruebas de IU comunes basadas en web para cualquiera de estos nodos. El concentrador Selenium también se puede conectar a Appium para realizar pruebas de aplicaciones entre plataformas. Solo se muestran los simuladores, pero puede incorporar las utilidades adb, para Android y Xcode para dispositivos iOS. Los vínculos se proporcionan más adelante en este documento, donde podrá encontrar detalles específicos de las herramientas mencionadas.

![chlimage_1](assets/chlimage_1.jpeg)

## Pruebas manuales {#manual-testing}

Además de las pruebas automatizadas, la aplicación debe pasar por un ciclo de pruebas manuales. Los clientes que ejecutan la aplicación en un dispositivo real no pueden duplicarse con un script. Aquí también tienes muchas opciones. Puede utilizar una plataforma, como HockeyApp, para definir quién tiene acceso y recopilar comentarios. O bien, puede subcontratar todo el proceso a un servicio como UTest, ElusiveStars o Testin. Si tiene un grupo de probadores internos, pero carece de variaciones de dispositivos, hay servicios en la nube donde puede realizar pruebas manuales en su grupo de dispositivos. Uno de esos servicios que ofrece es SauceLabs. También puede crear aplicaciones de forma remota en PhoneGap Enterprise e instalarlas en dispositivos locales como un nivel de aceptación de pruebas o de degradación. Consulte el sitio web de [PhoneGap](https://phonegap.com/) para conocer sus últimas funciones y documentación. Cualquiera que sea el método, las pruebas manuales deben realizarse;

* alcanza un gran objetivo de testers,
* realizar pruebas con un gran grupo de dispositivos (idealmente dispositivos reales, pero simuladores/emuladores si no hay dispositivos reales disponibles),
* proporcione comentarios informativos:

   * informes de bloqueo,
   * análisis/seguimiento,
   * usabilidad,
   * ámbitos de atención,
   * rendimiento,
   * consumo de datos/energía, etc.

## Herramientas {#tools}

Hay una amplia gama de herramientas disponibles para probar aplicaciones móviles. La elección de los que se usarán se basará en su situación específica: características, precio, asistencia, cobertura, etc. La siguiente es sólo una pequeña descripción de algunas de las herramientas y servicios disponibles.

**Selenio**

* Marco que incluye una API para secuencias de comandos de prueba para alimentar WebDriver y controlar varios exploradores.
* Puede utilizarlo junto con Appium para realizar pruebas en dispositivos reales.
* SeleniumGrid dirige las pruebas entre nodos para pruebas paralelas.
* El IDE selenio ayuda a reducir la escritura de los casos de prueba.

Para obtener más información, consulte [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**Testdroid**

* Servicio de pruebas basado en la nube con ganchos de integración continuos y pruebas de dispositivos reales.
* Incluye un App Crawler que comprueba la compatibilidad del dispositivo, analiza registros, recorre vistas, toma capturas de pantalla y monitorea el rendimiento.

Para obtener más información, consulte [https://testdroid.com/](https://testdroid.com/).

**Appio**

* Appium es un popular marco multiplataforma para automatizar pruebas móviles.
* Además, se incluye un inspector con capacidades de registro para ayudar a codificar los casos de prueba.

Para obtener más información, consulte [https://appium.io/](https://appium.io/).

**SauceLabs**

* SauceLabs ofrece pruebas basadas en la nube y se integra con una integración continua.
* Las pruebas se ejecutan automáticamente en su entorno de nube o puede iniciar un dispositivo o plataforma en particular y realizar pruebas manuales para ayudar a depurar problemas.

Para obtener más información, consulte [https://saucelabs.com/](https://saucelabs.com/).

**AppTestNow**

* Servicio de externalización que probará las aplicaciones móviles.
* Incluye un gran grupo de dispositivos y ofrece una amplia gama de tipos de pruebas: rendimiento, calidad, funcionalidad, certificación, localización, consumo de datos, etc.

Para obtener más información, consulte [https://www.apptestnow.com](https://www.apptestnow.com/).

**HockeyApp**

* HockeyApp cae dentro de la prueba manual, donde la aplicación móvil se envía a una tienda de aplicaciones personal donde los probadores pueden descargarla y probarla.

Para obtener más información, consulte [https://hockeyapp.net/features/](https://hockeyapp.net/features/).

**Jenkins**

* Aunque no es una herramienta de prueba, Jenkins es un marco de integración continua que proporciona la columna vertebral de las pruebas automatizadas. Existen numerosos complementos de terceros disponibles para ampliar la funcionalidad. Por ejemplo, el complemento SeleniumGrid proporciona una interfaz de usuario para administrar el hub y los nodos de Selenium.

Para obtener más información, consulte [https://jenkins-ci.org/](https://jenkins-ci.org/) y [https://wiki.jenkins-ci.org/display/JENKINS/Plugins](https://wiki.jenkins-ci.org/display/JENKINS/Plugins).
