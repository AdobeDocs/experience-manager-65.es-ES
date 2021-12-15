---
title: recorrido para desarrolladores AEM sin encabezado
description: AEM documentación CMS sin objetivos. Comience aquí para obtener un recorrido guiado a través de las potentes y flexibles funciones de AEM, sus capacidades y cómo aprovecharlas en su primer proyecto de desarrollo.
source-git-commit: 0458a811b5bd062abbe8a42ec141bc786491e19e
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 2%

---

# recorrido para desarrolladores AEM sin encabezado {#aem-headless-developer-journey}

Empiece aquí por un recorrido guiado a través de las potentes y flexibles funciones de AEM, sus capacidades y cómo aprovecharlas en su primer proyecto de desarrollo sin objetivos. Este recorrido le proporciona toda la documentación AEM sin encabezado que necesita para desarrollar su primera aplicación sin encabezado.

## Introducción {#introduction}

La implementación sin encabezado renuncia a la administración de páginas y componentes, como es tradicional en las soluciones de pila completas, y se centra en la creación de fragmentos de contenido neutros para el canal y reutilizables y su envío por canales cruzados. Es un patrón de desarrollo moderno y dinámico para implementar experiencias digitales.

Esta guía le guiará por los temas de implementación más importantes de AEM para que, al completarse:

* Comprenda perfectamente qué es la entrega de contenido sin objetivos y sus ventajas.
* Comprender AEM funciones sin objetivos y cómo trabajan juntos para ofrecer una experiencia sin objetivos.
* Tenga la capacidad de realizar los primeros pasos en la implementación de su primer proyecto AEM sin encabezado.

## recorridos de documentación de AEM {#documentation-journeys}

[Un Recorrido de documentación](/help/journey-documentation/home.md) une muchos temas y características diferentes y tal vez complicados al proporcionar una narrativa que ayuda al lector, que puede ser nuevo en AEM, entender y resolver un problema de negocios de principio a fin, mientras asume un mínimo de conocimiento previo o AEM.

Los Recorridos de documentación están diseñados en torno a los principios de las mejores prácticas, basados en las últimas investigaciones del Adobe, la experiencia de implementación comprobada de los consultores de Adobe y los comentarios de los proyectos de los clientes.

Si desea saber cómo el Adobe recomienda resolver casos empresariales sin objetivos con AEM, [recorridos sin AEM](/help/journey-headless/home.md) son el punto de inicio.

>[!TIP]
>
> Si prefiere **aprenda haciendo** y están técnicamente inclinados, visite los tutoriales AEM sin encabezado, que están organizados por API y framework y están disponibles en la [Sección Recursos adicionales](#additional-resources) al final de este documento.

## Audience {#audience}

Este recorrido está diseñado para el desarrollador, que expone los requisitos, pasos y enfoque de un proyecto sin encabezado AEM desde la perspectiva del desarrollador. El recorrido define las personas adicionales con las que el desarrollador debe interactuar para que un proyecto tenga éxito, pero el punto de vista del recorrido es el del desarrollador.

Las siguientes son las personalidades que interactúan en este recorrido.

| Grupo de usuarios | Descripción | Función en este Recorrido |
|---|---|---|
| Desarrollador (audiencia de destino) | Tiene experiencia en el desarrollo de aplicaciones sin periféricos que consumen contenido de diferentes fuentes | Destinatarios objetivo de este recorrido |
| Autor de contenido | Crea y gestiona el contenido que se entrega sin problemas | Los autores de contenido crean contenido que el desarrollador entrega sin problemas. |
| Administrador | Gestiona la configuración y configuración base de AEM | El desarrollador trabaja con el administrador para realizar los cambios de configuración necesarios para el desarrollo. |
| Arquitecto de contenido | Analiza los requisitos de los datos que deben entregarse sin interrupciones y define la estructura de estos datos | Los desarrolladores trabajan con el arquitecto de contenido para comprender la estructura de los datos y los requisitos para ofrecerlos sin problemas. |

Por supuesto, la información de este recorrido puede ser útil para todas las personas, pero parte de la información puede ser superflua para ciertas funciones. Manténgase atento a [recorridos futuros que cubran funciones adicionales.](/help/journey-documentation/home.md#journeys)

## El Recorrido para desarrolladores sin objetivos {#the-journey}

Explorará muchos temas en este recorrido. Los siguientes artículos le proporcionan conocimientos básicos de AEM y le permiten acceder a documentación técnica detallada.

Aunque puede ir directamente a una parte concreta del recorrido, muchos conceptos se basan en los de artículos anteriores. Por lo tanto, si es nuevo en sin encabezado en AEM, le recomendamos que comience al principio y avance secuencialmente.

| # | Artículo | Descripción |
|---|---|---|
| 0 | recorrido para desarrolladores AEM sin encabezado | Este documento |
| 1 | [Obtenga información sobre el desarrollo sin encabezado de CMS](learn-about.md) | Obtenga información sobre la tecnología sin encabezado y cuándo utilizarla. |
| 2 | [Introducción a AEM sin encabezado](getting-started.md) | Obtenga información sobre los requisitos previos sin encabezado de AEM |
| 3 | [Ruta a la primera experiencia usando AEM sin encabezado](path-to-first-experience.md) | Configure su entorno de desarrollo y aprenda a integrar una aplicación sencilla con AEM sin encabezado |
| 4 | [Cómo modelar el contenido](model-your-content.md) | Aprenda a modelar la estructura de contenido. A continuación, observe esa estructura para Adobe Experience Manager (AEM) mediante los modelos de fragmentos de contenido y los fragmentos de contenido, para reutilizarla en todos los canales. |
| 5 | [Cómo acceder al contenido a través de las API de envío de AEM](access-your-content.md) | Aprenda a utilizar las consultas de GraphQL para acceder al contenido de los fragmentos de contenido. |
| 6 | [Actualización del contenido mediante las API de AEM Assets](update-your-content.md) | Aprenda a utilizar la API de REST para acceder y actualizar el contenido de los fragmentos de contenido. |
| 7 | [Cómo ponerlo todo juntos: su aplicación y su contenido en AEM sin encabezado](put-it-all-together.md) | Aprenda a tomar su proyecto AEM y prepararlo para su lanzamiento con el SDK sin encabezado de AEM. |
| 8 | [Opcional: Cómo crear aplicaciones de una sola página (SPA) con AEM](create-spa.md) | Una vez que haya comprendido AEM funciones sin encabezado, explore cómo combinar entregas con encabezado y sin encabezado y aprenda a crear SPA editables con AEM marco SPA Editor. |

<!-- HM-Links
|8|[How to go live with your headless application](go-live.md)|Learn how to deploy application live and take your local code in Git and move it to Cloud Manager Git for CI/CD pipeline.|
|9|[Optional - How to create single page applications (SPAs) with AEM](create-spa.md)|Once you understand AEM's headless features, explore how to combine headful and headless delivery and learn how you can create editable SPAs using AEM's SPA Editor framework.|
-->

## Siguientes pasos {#what-is-next}

Ahora está listo para empezar con su recorrido sin encabezado de Adobe. Le animamos a que continúe con la siguiente parte del recorrido y lea el artículo [Obtenga información sobre el desarrollo sin encabezado de CMS.](learn-about.md)

### Elija su propia aventura {#choose-your-path}

Sin embargo, Adobe quiere que tenga éxito a medida que comienza con el proyecto sin encabezado de AEM, independientemente de su estilo de aprendizaje. Así que por favor consideren estas dos opciones.

* Si prefiere continuar **obtenga información sobre conceptos sin encabezado y AEM tecnologías sin encabezado**, debe continuar con su recorrido sin AEM como se recomienda en la próxima revisión del documento [Modelo del contenido como modelos de contenido AEM](model-your-content.md) donde aprende a modelar la estructura de contenido en AEM.
* Si prefiere **aprenda haciendo**, puede ir al [Tutorial práctico Introducción a AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) donde saltará directamente al desarrollo sin encabezado de AEM implementando un proyecto simple para exponer AEM contenido sin encabezado.

## Recursos adicionales {#additional-resources}

Los recorridos de documentación muestran cómo AEM resuelve un problema comercial al proporcionar una narrativa que lo guía a través de procesos y funciones complejos e interrelacionados. Un recorrido ilustra cómo varias funciones trabajan juntas para satisfacer una sola necesidad empresarial.

Como estos recorridos están diseñados para mantenerse por su cuenta. Sin embargo, varios de ellos pueden relacionarse entre sí. Consulte estos recorridos adicionales para obtener más información sobre cómo funcionan juntas AEM potentes funciones.

* [Tutoriales AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - Si prefiere aprender haciendo y está técnicamente inclinado, tome nuestros tutoriales prácticos organizados por API y framework, que exploran la creación y el uso de aplicaciones creadas sobre AEM sin encabezado.
* [recorrido de traducción AEM sin encabezado](/help/journey-headless/translation/overview.md) - Este recorrido de documentación le ofrece una amplia comprensión de la tecnología sin objetivos, AEM sirve contenido sin objetivos y cómo puede traducirlo.
* [Recorrido de creación sin encabezado](/help/journey-headless/author/overview.md) - Empiece aquí para obtener un recorrido guiado a través de las potentes y flexibles funciones de AEM, sus capacidades y cómo modelar su contenido en su primer proyecto sin objetivos.
* [Recorrido de arquitectos sin encabezado](/help/journey-headless/architect/overview.md) - Empiece aquí para ver una introducción a las potentes y flexibles funciones de Adobe Experience Manager y a cómo modelar el contenido de su proyecto.
* [AEM documentación técnica](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es) - Si ya tiene una comprensión firme de las tecnologías AEM y sin objetivos, puede que desee consultar directamente nuestros documentos técnicos.
