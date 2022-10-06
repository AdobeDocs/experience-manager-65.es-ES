---
title: Obtenga Información Sobre El Desarrollo Sin Cabeza De CMS
description: En esta parte del Recorrido para desarrolladores AEM sin encabezado, conozca la tecnología sin encabezado y por qué la utilizaría.
exl-id: f0989cea-3102-43cd-976e-9a6b265d9c15
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 1%

---

# Obtenga Información Sobre El Desarrollo Sin Cabeza De CMS {#learn-about}

En esta parte del [AEM Recorrido para desarrolladores sin encabezado,](overview.md) aprenda sobre la tecnología sin encabezado y por qué la utilizaría.

## Objetivo {#objective}

Este documento le ayuda a comprender la entrega de contenido sin encabezado y por qué debería usarse. Después de leer, debería haber logrado lo siguiente:

* Comprender los conceptos básicos y la terminología de la entrega de contenido sin encabezado
* Comprender por qué y cuándo se requiere un proceso sin encabezado
* Conocer en un nivel superior cómo se utilizan los conceptos sin encabezado y cómo se interrelacionan

## Entrega de contenido de pila completa {#full-stack}

Desde el surgimiento de los sistemas de administración de contenido (CMS) a gran escala, fáciles de usar, las organizaciones los han aprovechado como una ubicación central para administrar mensajes, marcas y comunicaciones. El uso del CMS como punto central para la administración de experiencias mejoró la eficiencia al eliminar la necesidad de duplicar tareas en sistemas dispares.

![El clásico CMS de pila completa](assets/full-stack.png)

En un CMS de pila completa, toda la funcionalidad para manipular el contenido está en el CMS. Las características del sistema componen diferentes componentes de la pila de CMS. La solución de pila completa tiene muchas ventajas.

* Tiene un sistema para mantener.
* El contenido se administra de forma centralizada.
* Todos los servicios del sistema están integrados.
* La creación de contenido es perfecta.

Por lo tanto, si desea agregar un canal nuevo o admitir nuevos tipos de experiencias, puede insertar uno o más componentes nuevos en la pila y solo tiene un lugar donde realizar los cambios.

![Adición de un nuevo canal a la pila](assets/adding-channel.png)

La complejidad de las dependencias dentro de la pila se hace evidente rápidamente, ya que puede que sea necesario ajustar otros elementos de la pila para adaptarse a los cambios.

## Límites de entrega de pila completa {#limits}

El método de pila completa crea inherentemente un silo donde todas las experiencias aterrizan en un sistema. Los cambios o adiciones a un componente del silo requieren cambios en otros componentes que pueden hacer que los cambios requieran mucho tiempo y sean costosos.

Esto es particularmente cierto en el caso del sistema de presentación, que en configuraciones tradicionales, a menudo está estrechamente vinculado al CMS. Cualquier canal nuevo generalmente significa una actualización del sistema de presentación, que puede afectar a todos los demás canales.

![La complejidad crece a medida que los canales se añaden a una pila](assets/presentation-complexity.png)

Las limitaciones de este silo natural pueden hacerse evidentes a medida que se dedica más esfuerzo a coordinar los cambios en todos los componentes de la pila.

Los usuarios esperan que haya participación independientemente de la plataforma o el punto de contacto, lo que requiere agilidad en la forma de ofrecer sus experiencias.  Este enfoque multicanal es el estándar de las experiencias digitales y, en determinadas circunstancias, un enfoque de pila completa puede resultar inflexible.

## La cabeza sin cabeza {#the-head}

El jefe de cualquier sistema es generalmente el procesador de salida de ese sistema, normalmente en forma de GUI u otra salida gráfica.

Por ejemplo, es probable que un servidor sin periféricos esté sentado en un rack en una sala de servidores en algún lugar y no tenga un monitor conectado. Para acceder a él, debe conectarse de forma remota. En este caso, el monitor es la cabeza ya que se encarga de procesar la salida del servidor. Usted como consumidor del servicio, proporcione su propio cabezal (el monitor) cuando se conecte de forma remota a él.

Cuando hablamos de un CMS sin objetivos, el CMS administra el contenido y continúa entregándolo a los consumidores. Sin embargo, solo entregando la variable **contenido** de forma estandarizada, un CMS sin periféricos omite el procesamiento de salida final, dejando el **presentación** del contenido al servicio consumidor.

![CMS sin encabezado](assets/headless-cms.png)

Los servicios que consumen, ya sean experiencias de AR, una tienda web, experiencias móviles, aplicaciones web progresivas (PWA), etc., reciben contenido del CMS sin periféricos y proporcionan su propia renderización. Se ocupan de proporcionar sus propias cabezas para su contenido.

Omitir la cabeza simplifica el CMS al eliminar la complejidad. Al hacerlo, también se traslada la responsabilidad de procesar el contenido a los servicios que realmente necesitan el contenido y que a menudo son más adecuados para dicha renderización.

## Desacoplamiento {#decoupling}

La entrega sin objetivos es posible mediante la exposición de un conjunto de interfaces de programación de aplicaciones (API) sólidas y flexibles que todas las experiencias pueden aprovechar. La API sirve como idioma común entre los servicios, y los une a nivel de contenido mediante una entrega de contenido estandarizada, pero permitiéndoles la flexibilidad para implementar sus propias soluciones.

Sin encabezado es un ejemplo de desvinculación del contenido de su presentación. O en un sentido más genérico, desacoplando el front-end del back-end de su pila de servicios. En una configuración sin periféricos, el sistema de presentación (el cabezal) está disociado de la administración de contenido (el tamaño). Los dos únicos interactúan mediante llamadas de API.

Esta disociación significa que cada servicio consumidor (el front-end) puede crear su experiencia en función del mismo contenido que se entrega a través de las API, lo que garantiza la reutilización del contenido y la coherencia. Los servicios de consumo pueden implementar sus propios sistemas de presentación, lo que permite que la pila de administración de contenido (el back end) se escale fácilmente horizontalmente.

## Fundamentos tecnológicos {#technology}

Un enfoque sin objetivos le permite crear un conjunto de tecnologías que se adapte rápida y fácilmente a las futuras exigencias de experiencias digitales.

Las API para CMS en el pasado generalmente se basaban en REST. La transferencia de estado representativo (REST) proporciona recursos como texto de forma apátrida. Esto permite leer y modificar los recursos con un conjunto predefinido de operaciones. El REST permite una buena interoperabilidad entre los servicios de la web al garantizar la representación sin estado del contenido.

Sigue siendo necesario contar con API de REST sólidas. Sin embargo, las solicitudes REST pueden ser grandes y detalladas. Si tiene varios consumidores haciendo llamadas REST para todos sus canales, esta diversidad de compuestos y el rendimiento pueden verse afectados.

La entrega de contenido sin encabezado suele utilizar las API de GraphQL. GraphQL permite una transferencia sin estado similar, pero permite consultas más específicas, reduce el número total de consultas necesarias y mejora el rendimiento. Es común ver que las soluciones utilizan una mezcla de REST y GraphQL, eligiendo esencialmente la mejor herramienta para el trabajo en cuestión.

Independientemente de cuál sea su API elegida, al definir un sistema sin encabezado basado en API comunes, puede aprovechar el explorador más reciente y otras tecnologías web, como aplicaciones web progresivas (PWA). Las API crean una interfaz estándar que es fácilmente ampliable y adaptable.

Normalmente, el contenido se representa en el lado del cliente. Normalmente, esto significa que alguien llama al contenido en un dispositivo móvil, el CMS envía el contenido y, a continuación, el dispositivo móvil (el cliente) es responsable de procesar el contenido que ha servido. Si el dispositivo es antiguo o lento, la experiencia digital también es lenta.

Desvincular contenido de la presentación significa que puede haber más control sobre estas preocupaciones de rendimiento del lado del cliente. El procesamiento del lado del servidor (SSR) transfiere la responsabilidad de procesar el contenido desde el explorador del cliente al servidor. Esto le permite, como proveedor del contenido, ofrecer un nivel de rendimiento garantizado a la audiencia si es necesario.

## Desafíos organizativos {#organization}

Sin objetivos abre un mundo de flexibilidad para ofrecer sus experiencias digitales. Pero esta flexibilidad también puede representar su propio desafío.

Tener muchos canales diferentes puede significar que cada uno tiene sus propios sistemas de presentación. Aunque todas consumen el mismo contenido a través de las mismas API, la experiencia puede ser diferente debido a las diferentes presentaciones. Se debe prestar atención y atención a garantizar la coherencia de la experiencia del cliente.

Al implementar sistemas de diseño cuidadosos, compartir bibliotecas de patrones y aprovechar componentes de diseño reutilizables, así como marcos abiertos y establecidos del lado del cliente, se pueden asegurar experiencias coherentes, pero esto debe planificarse.

## El futuro no tiene rumbo y el futuro está ahora {#future}

Las experiencias digitales seguirán definiendo la forma en que las marcas interactúan con los clientes. Lo que es interesante del diseño sin objetivos es la flexibilidad que nos proporciona para responder a las expectativas de los clientes en evolución.

Es imposible predecir el futuro, pero no hay nadie que te dé la agilidad de reaccionar a lo que traiga el futuro.

## AEM y sin encabezado {#aem-and-headless}

A medida que continúe con este recorrido para desarrolladores, aprenderá cómo AEM admite la entrega sin objetivos junto con sus funciones de entrega de pila completa.

Como líder del sector en la administración de experiencias digitales, el Adobe se da cuenta de que la solución ideal a los desafíos del mundo real que enfrentan los creadores de experiencias rara vez es una opción binaria. Por este motivo, AEM no solo admite ambos modelos, sino que también permite de forma exclusiva la combinación híbrida sin fisuras de los dos, combinando las ventajas de la pila completa y sin periféricos, para ayudarle a servir mejor a los consumidores de su contenido, independientemente del lugar en que se encuentren.

Este recorrido se centra en el modelo de envío de contenido sin periféricos. Sin embargo, una vez que tenga este conocimiento fundacional, puede explorar más a fondo cómo aprovechar el poder de ambos modelos.

## Siguientes pasos {#what-is-next}

¡Gracias por empezar con tu recorrido AEM sin cabeza! Ahora que lee este documento, debe:

* Comprender los conceptos básicos y la terminología de la entrega de contenido sin encabezado.
* Comprenda por qué y cuándo es necesario que no tenga encabezado.
* Conocer en un nivel superior cómo se utilizan los conceptos sin encabezado y cómo se interrelacionan.

Aproveche este conocimiento y continúe su recorrido sin AEM cabeza al revisar el documento [Introducción a AEM sin encabezado](getting-started.md) donde aprenderá a configurar las herramientas necesarias y a empezar a pensar en cómo AEM aborda la entrega de contenido sin encabezado y sus requisitos previos.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de desarrollo remoto revisando el documento [Introducción a AEM sin encabezado](getting-started.md), los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no son necesarios para continuar en el recorrido sin encabezado.

* [Tutorials AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es) - Utilice estos tutoriales prácticos para explorar cómo utilizar las distintas opciones para enviar contenido a puntos de conexión sin periféricos con AEM y elegir lo que es adecuado para usted.
