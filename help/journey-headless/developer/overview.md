---
title: Recorrido para desarrolladores de AEM sin encabezado
description: AEM Documentación de CMS sin encabezado de. Comience aquí para obtener un recorrido AEM guiado a través de las potentes y flexibles funciones sin encabezado de los, sus capacidades y cómo aprovecharlas en su primer proyecto de desarrollo.
exl-id: f24fb308-daa7-426f-ba45-37a236b5a500
source-git-commit: 9c517590c2b78eed7c52e33e0a106237a2af3bb7
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 76%

---

# Recorrido para desarrolladores de AEM sin encabezado {#aem-headless-developer-journey}

Comience aquí para obtener un recorrido AEM guiado a través de las potentes y flexibles funciones sin encabezado de los, sus capacidades y cómo aprovecharlas en su primer proyecto de desarrollo sin encabezado. Este recorrido AEM le proporciona toda la documentación sin encabezado de la que necesita para desarrollar su primera aplicación sin encabezado.

## Introducción {#introduction}

La implementación sin encabezado renuncia a la administración de páginas y componentes, ya que es tradicional en soluciones de pila completa y se centra en la creación de fragmentos de contenido neutros y reutilizables para el canal y en su entrega multicanal. Es un patrón de desarrollo moderno y dinámico para implementar experiencias digitales.

AEM Esta guía le guía por los temas de implementación sin encabezado más comunes en la documentación de para que, al completarla, pueda hacer lo siguiente:

* Comprenderá perfectamente qué es la entrega de contenido sin encabezado y sus ventajas.
* Comprenderá las funciones sin encabezado de AEM y cómo trabajan conjuntamente para ofrecer una experiencia sin encabezado.
* Tendrá la posibilidad de realizar los primeros pasos en la implementación de su primer proyecto AEM sin encabezado.

## Recorridos de documentación de AEM {#documentation-journeys}

[Un recorrido de documentación](/help/journey-documentation/home.md) une muchos temas y características diferentes y tal vez complicados. Proporciona una narrativa que ayuda al lector (que puede ser nuevo en AEM) a entender y resolver un problema empresarial de principio a fin, mientras asume un conocimiento previo mínimo de AEM.

Los recorridos de documentación están diseñados en torno a los principios de las prácticas recomendadas, basados en las últimas investigaciones de Adobe, la experiencia de implementación comprobada de los consultores de Adobe y los comentarios sobre los proyectos de los clientes.

Si quiere saber lo recomienda Adobe para resolver los casos empresariales sin encabezado con AEM, [Los recorridos de AEM sin encabezado](/help/journey-headless/home.md) es dónde debe empezar.

>[!TIP]
>
>Si lo prefiere, **aprenda haciendo** AEM y son técnicamente propensos, visite los tutoriales sin encabezado de la, organizados por API y marco de trabajo y disponibles en [Sección Recursos adicionales](#additional-resources) al final de este documento.

## Audiencia {#audience}

Este recorrido está diseñado para el desarrollador y expone los requisitos, pasos y enfoque de un proyecto de AEM sin encabezado desde la perspectiva del desarrollador. El recorrido define las personas adicionales con las que el desarrollador debe interactuar para que un proyecto tenga éxito, pero el punto de vista del recorrido es el del desarrollador.

Los siguientes son los perfiles que interactúan en este recorrido.

| Grupo de usuarios | Descripción | Función en este recorrido |
|---|---|---|
| Desarrollador (audiencia de destino) | Tiene experiencia en el desarrollo de aplicaciones sin encabezado que consumen contenido de diferentes fuentes | Audiencia de destino de este recorrido |
| Autor de contenido | Crea y gestiona contenido que se suministra sin encabezado | Los autores de contenido crean contenido que el desarrollador entrega sin encabezado. |
| Administrador | Gestiona la configuración base de AEM | El desarrollador trabaja con el administrador para realizar los cambios de configuración necesarios para el desarrollo. |
| Arquitecto de contenido | Analiza los requisitos de los datos que deben entregarse sin encabezado y define la estructura de estos datos | Los desarrolladores trabajan con el arquitecto de contenido para comprender la estructura de los datos y los requisitos para ofrecerlos sin encabezado. |

Por supuesto, la información de este recorrido puede ser útil para todas las personas, pero parte de la información puede ser superflua para ciertas funciones. Manténgase atento a [recorridos futuros que cubran funciones adicionales.](/help/journey-documentation/home.md#journeys)

## Recorrido para los desarrolladores de contenido sin encabezado {#the-journey}

Explorará muchos temas en este recorrido. Los siguientes artículos le proporcionan conocimientos básicos sobre los contenidos sin encabezado en AEM y acercan la documentación técnica detallada.

Aunque puede ir directamente a una parte concreta del recorrido, muchos conceptos se basan en los de artículos anteriores. AEM Por lo tanto, si es nuevo en el uso sin encabezado en la, Adobe recomienda comenzar por el principio y avanzar secuencialmente.

| # | Artículo | Descripción |
|---|---|---|
| 0 | Recorrido para desarrolladores de AEM sin encabezado | Este documento |
| 1 | [Obtenga información acerca del desarrollo sin encabezado de CMS](learn-about.md) | Obtenga información sobre la tecnología sin encabezado y cuándo utilizarla. |
| 2 | [Introducción a AEM sin encabezado](getting-started.md) | Aprenda sobre los requisitos previos de AEM sin encabezado |
| 3 | [Ruta hacia la primera experiencia al usar AEM sin encabezado](path-to-first-experience.md) | Configurar su entorno de desarrollo y aprender a integrar una aplicación sencilla con AEM sin encabezado |
| 4 | [Cómo modelar el contenido](model-your-content.md) | Aprenda a modelar la estructura de contenido. A continuación, observe esa estructura para Adobe Experience Manager (AEM) mediante los modelos de fragmentos de contenido y los fragmentos de contenido, para reutilizarla en todos los canales. |
| 5 | [Cómo acceder al contenido a través de las API de entrega de AEM](access-your-content.md) | Aprenda a utilizar las consultas de GraphQL para acceder al contenido de los fragmentos de contenido. |
| 6 | [Actualización del contenido mediante las API de AEM Assets](update-your-content.md) | Descubra cómo utilizar la API de REST para acceder y actualizar el contenido de los fragmentos de contenido. |
| 7 | [Cómo ponerlo todo junto: su aplicación y su contenido en AEM sin encabezado](put-it-all-together.md) | Aprenda a gestionar su proyecto AEM y prepararlo para su lanzamiento con el SDK de AEM sin encabezado. |
| 8 | [Publicación de la aplicación sin encabezado](go-live.md) | Obtenga información sobre cómo implementar la aplicación en directo, tomar el código local en Git y moverlo a Cloud Manager Git para la canalización de CI/CD. |
| 9 | [Opcional: cómo crear aplicaciones de una sola página (SPA) con AEM](create-spa.md) | AEM SPA AEM SPA Una vez que haya comprendido las funciones sin encabezado de la, explore cómo combinar la entrega sin encabezado y la entrega sin encabezado, y descubra cómo puede crear un entorno de trabajo editable con el editor de contenido de la. |

## Siguientes pasos {#what-is-next}

Ya está listo para empezar su recorrido de Adobe sin encabezado. Le animamos a que continúe con la siguiente parte del recorrido y lea el artículo [Obtenga información acerca del desarrollo sin encabezado CMS.](learn-about.md)

### Elija su propia aventura {#choose-your-path}

Sin embargo, Adobe AEM quiere que tenga éxito a medida que empiece a trabajar en su proyecto sin encabezado, independientemente de su estilo de aprendizaje. Así que por favor considere estas dos opciones.

* Si prefiere seguir **obteniendo información sobre conceptos sin encabezado y tecnologías sin encabezado de AEM**, debe continuar con su recorrido de AEM sin encabezado como se recomienda en la próxima revisión del documento [Modelar el contenido como modelos de contenido de AEM](model-your-content.md), donde aprenderá a modelar la estructura de contenido en AEM.
* Si prefiere **aprender de forma práctica**, puede ir al [Tutorial práctico de introducción a AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=es), donde pasará directamente al desarrollo de AEM sin encabezado implementando un proyecto simple para exponer contenido sin encabezado de AEM.

## Recursos adicionales {#additional-resources}

Los recorridos de documentación muestran cómo AEM resuelve un problema empresarial al proporcionar una narrativa que lo guía a través de procesos y características complejas e interrelacionadas. Un recorrido ilustra cómo varias funciones trabajan juntas para satisfacer una sola necesidad empresarial.

Ya que estos recorridos están diseñados para mantenerse por su cuenta. Sin embargo, varios de ellos pueden relacionarse entre sí. Consulte estos recorridos adicionales para obtener más información sobre cómo las potentes funciones de AEM trabajan juntas.

* [Tutoriales Headless de AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es): si prefiere aprender con la práctica y tiene interés por la tecnología, siga nuestros tutoriales prácticos organizados por API y el marco de trabajo, que exploran la creación y el uso de aplicaciones creadas en AEM Headless.
* [Recorrido de traducción de AEM sin encabezado](/help/journey-headless/translation/overview.md): este recorrido de documentación le ofrece un amplio conocimiento sobre la tecnología sin encabezado, cómo proporciona AEM contenido sin encabezado y cómo puede traducirlo.
* [Recorrido de creación sin encabezado](/help/journey-headless/author/overview.md). Empiece aquí para obtener un recorrido guiado a través de las potentes y flexibles funciones sin encabezado de AEM, sus capacidades y cómo modelar su contenido en su primer proyecto sin encabezado.
* [Recorrido de arquitectos Headless](/help/journey-headless/architect/overview.md) : Empiece aquí para ver una introducción a las potentes y flexibles funciones sin encabezado de Adobe Experience Manager y cómo diseñar contenido para su proyecto.
* [Documentación técnica de AEM ](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es): si ya tiene una comprensión firme de las tecnologías AEM y headless, puede que desee consultar directamente nuestros documentos técnicos detallados.

   * Un [AEM Introducción a la como CMS sin encabezado](/help/sites-developing/headless/introduction.md)

* El [AEM Portal para desarrolladores de](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es)
