---
title: Preguntas más frecuentes sobre el fin de vida útil del visor DHTML
seo-title: Preguntas más frecuentes sobre el fin de vida útil del visor DHTML
description: A partir del 31 de enero de 2014, la plataforma de visor DHTML de Scene7 dejará de funcionar oficialmente. Esta notificación le proporciona respuestas a las preguntas más frecuentes para que pueda prepararse para esta transición a nuestra nueva plataforma de visor HTML5.
seo-description: A partir del 31 de enero de 2014, la plataforma de visor DHTML de Scene7 dejará de funcionar oficialmente. Esta notificación le proporciona respuestas a las preguntas más frecuentes para que pueda prepararse para esta transición a nuestra nueva plataforma de visor HTML5.
uuid: a78c03b3-6513-42e1-881f-6a9551659769
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d94244ac-a5f6-4c95-ab8c-26b41d25863f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Preguntas más frecuentes sobre el fin de vida útil del visor DHTML{#dhtml-viewer-end-of-life-faqs}

A partir del 31 de enero de 2014, la plataforma de visor DHTML de Scene7 dejará de funcionar oficialmente. Esta notificación le proporciona respuestas a las preguntas más frecuentes para que pueda prepararse para esta transición a nuestra nueva plataforma de visor HTML5.

**¿Cuál es el cambio?**

A partir del 31 de enero de 2014, Scene7 ya no ofrecerá asistencia para la plataforma de visor DHTML.

**¿Qué significa el fin de vida?**

El final de su vida útil significa que Scene7 (1) ya no agregará mejoras en las funciones a la plataforma de visor DHTML (2) ni publicará correcciones de errores en la plataforma de visor DHTML y (3) el servicio de atención al cliente dejará de solucionar problemas o de proporcionar asistencia para cualquier problema o pregunta relacionado con el visor DHTML.

**¿Por qué realiza Scene7 este cambio?**

Los estándares web evolucionan constantemente y DHTML es una tecnología de desarrollo web antigua que se está reemplazando rápidamente por HTML5. La mayor limitación de DHTML como plataforma es que no es capaz de crear la riqueza de experiencia que HTML5 ahora puede admitir de forma consistente y más sencilla en varios navegadores. Por ejemplo, estas limitaciones incluyen la falta de compatibilidad entre exploradores para:

* Cursores personalizados
* Esquinas redondeadas
* Animaciones (como el volteo de página, la flexibilización del zoom)
* Efectos (como sombras, resplandor)
* Compatibilidad total con fuentes
* Reproducción de vídeo sin complementos

Específicamente a la plataforma de visor DHTML de Scene7, tanto la solución basada en JSP como las API de Javascript no se han optimizado para dispositivos móviles para aprovechar las funciones de gestos y multitoque. Y aunque los visores DHTML que se lanzaron en 2011/principios de 2012 están optimizados para dispositivos móviles, eran difíciles de personalizar y mantener debido a la falta de un marco de desarrollo flexible basado en componentes SDK.

Debido a estas limitaciones en DHTML y a la rápida tracción del sector con HTML5 como estándar emergente tanto para equipos de escritorio como móviles, Scene7 ha decidido invertir en una plataforma de visor basada en HTML5. Esta inversión ofrecerá a nuestros clientes una plataforma sólida con la que podrán crear visores interactivos más enriquecidos y atractivos que puedan llegar a los usuarios en varias pantallas, incluidos los dispositivos de escritorio, iOS y Android.

**¿Cómo sé si mi visor está usando la plataforma DHTML?**

Para determinar si el visor que utiliza su empresa es DHTML y, por lo tanto, se ve afectado por este cambio, compruebe si:

1. Su empresa está utilizando un visor de Scene7 incorporado en esta tabla, donde la &quot;Tecnología de visor&quot; se designa como &quot;DHTML&quot;:

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. Su empresa está utilizando un visor que se creó como un nuevo ajuste preestablecido basado en un visor de Scene7 incorporado en esta tabla, donde la &quot;Tecnología del visor&quot; se designa como &quot;DHTML&quot;:

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. Su empresa está utilizando un visor personalizado creado a partir de la solución DHTML basada en JSP:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference)

1. Su empresa está utilizando un visor personalizado creado a partir de la API de JavaScript:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference)

1. Su empresa está utilizando un visor personalizado creado con la API de flotación multipantalla DHTML:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer)

1. Su empresa está utilizando un visor personalizado creado con la API flotante de escritorio DHTML:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer)

1. Su empresa está utilizando una biblioteca de detección de dispositivos que forma parte del paquete de visores DHTML:

   Busque la inclusión de JS de &quot;sj_deviceDetect.js&quot; en el código.

   Esto se ha sustituido por el nuevo código de detección de dispositivos JS aquí: [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers) .

**¿Cuál es la plataforma de visor de sustitución?**

El reemplazo de DHTML es la plataforma de visor HTML5 de Scene7, que consta de:

* Los visores integrados en HTML5 incluyen interacciones optimizadas para dispositivos móviles en varios tipos de visor, incluidos zoom básico, zoom flotante, conjuntos de imágenes, conjuntos de muestras, giro multidimensional y medios mixtos. Para ver ejemplos actualizados de estos visores, consulte: [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
* SDK de visor HTML5 que permite una amplia personalización de los visores de Adobe Scene7 para sitios y dispositivos compatibles con HTML5 (como iOS y Android), lo que ofrece la máxima flexibilidad y creatividad para personalizar el aspecto del visor y la interactividad. Las ventajas de los componentes reutilizables optimizados para el rendimiento reducen el coste total del desarrollo del visor y aceleran el desarrollo personalizado.

**¿Cuándo tendrá la plataforma de visor HTML5 las funciones que necesito para realizar la transición desde la plataforma de visor DHTML?**

Scene7 lanzó el primer SDK de visor HTML5 en otoño de 2011 con el lanzamiento de la versión 5.5. Desde entonces, hemos agregado numerosas funciones a la plataforma y hemos ampliado la compatibilidad para más y más tipos de visores. Para la mayoría de los requisitos habituales del visor, es probable que la plataforma de visor HTML5 ya cuente con las funciones que necesita migrar ahora. Y seguimos invirtiendo agresivamente en esta plataforma de visor con lanzamientos cada trimestre.

Para determinar si los requisitos del visor se pueden satisfacer hoy mismo con la plataforma de visor HTML5, consulte la siguiente documentación:

[https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers) (para funciones de visores originales y funciones de personalización)

[https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html) (para acceder a la documentación de la API de SDK)

Si no está seguro de si el SDK de visor HTML5 puede o no satisfacer sus necesidades, consulte con nuestro equipo de servicios profesionales.

**¿Cómo puedo realizar la transición de mis visores a la plataforma HTML5?**

Para realizar la transición de los visores a la plataforma HTML5, Scene7 ofrece las siguientes opciones:

1. Utilice uno de los visores HTML5 integrados de Scene7, cuyos ejemplos se pueden encontrar aquí: [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
1. Configure uno de los visores HTML5 integrados de Scene7 en la configuración de la aplicación de SPS. Esto le permitirá personalizar cierto comportamiento, como el tamaño del visor, las transiciones, el comportamiento de zoom, etc.: [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html)
1. Personalice el aspecto de los visores HTML5 integrados en Scene7 mediante la modificación de CSS para cambiar el diseño visual, como la ilustración de botones, la colocación, la transparencia, los colores de fondo, etc.: [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers)
1. Cree un visor HTML5 personalizado desde cero con el SDK, que se puede descargar aquí: [https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html). Puede contratar servicios profesionales para crear el visor personalizado o hacer que su propio equipo de desarrollo web lo cree.

**¿Qué sucede con los exploradores que no admiten HTML5?**

HTML5 es compatible con muchos dispositivos móviles y navegadores web, y sigue ganando terreno. Actualmente, aunque HTML5 no es compatible con Internet Explorer 8 o versiones posteriores, Scene7 ha innovado nuestra plataforma de visor HTML5 para ampliar la compatibilidad incluso a IE 7 e IE 8. Con la plataforma de visor HTML5 de Scene7, puede llegar a la mayoría abrumadora de usuarios de escritorio y móviles con una única plataforma de desarrollo.

Los requisitos actuales del sistema a partir de la versión 2.2.1 del SDK para HTML5 son:

* Microsoft® Windows® XP o posterior, Macintosh® OS X 10.6 o posterior
* Firefox 17, Safari 5.1, Chrome 23, Internet Explorer 7 o posterior
* iOS 3.2.2 o posterior
* Certificado en iPhone3 o posterior y iPad1 o posterior (exploradores nativos)
* Android OS 2.2 o posterior

Para comprobar si su navegador es compatible con nuestra plataforma de visor HTML5, inicie el siguiente visor de ejemplo:

[https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image](https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image)

Si ve la imagen ampliada pasando el ratón o arrastrando el dedo sobre la imagen principal, se trata de un navegador o dispositivo compatible.

**¿Qué opciones tengo si quiero seguir en producción con mi visor DHTML existente?**

Aunque todavía puede estar en producción con visores basados en DHTML, es importante tener en cuenta que no habrá mejoras, correcciones de errores ni atención al cliente después del 31 de enero de 2014. Por lo tanto, recomendamos encarecidamente a todos los clientes que migren a nuestra plataforma de visor HTML5 más sólida. . Sin embargo, si su situación comercial impide dicha migración antes de la fecha de EOL, tiene la opción de contratar servicios profesionales para ampliar el período de tiempo de mantenimiento admitido. Para obtener más información, póngase en contacto con su administrador de cuentas.

**¿Con quién puedo contactar para obtener más información?**

Si esta pregunta frecuente no responde a todas sus preguntas, póngase en contacto con el servicio de asistencia técnica ([s7support@adobe.com](mailto:s7support@adobe.com)) o con el administrador de cuentas de Adobe.
