---
title: Ruta a la primera experiencia usando AEM sin encabezado
description: En esta parte del Recorrido para desarrolladores sin encabezado de AEM, comprenderá los pasos para implementar su primera experiencia sin objetivos en AEM, incluidas las consideraciones de planificación, y también aprenderá las prácticas recomendadas para que su ruta sea lo más fluida posible.
source-git-commit: 0458a811b5bd062abbe8a42ec141bc786491e19e
workflow-type: tm+mt
source-wordcount: '1982'
ht-degree: 0%

---

# Ruta a la primera experiencia usando AEM sin encabezado {#path-to-first-experience}

En esta parte del [AEM Recorrido para desarrolladores sin encabezado,](overview.md) comprenderá los pasos para implementar su primera experiencia sin objetivos en AEM, incluidas consideraciones de planificación, y también aprenderá prácticas recomendadas para que su ruta sea lo más fluida posible.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido sin AEM, [Introducción a AEM sin encabezado](getting-started.md) aprendió la teoría básica de lo que es un CMS sin cabeza y ahora debería:

* Comprender los conceptos básicos de AEM funciones sin encabezado.
* Conozca los requisitos previos para utilizar AEM funciones sin encabezado.
* Tenga en cuenta AEM niveles de integración sin objetivos.
* Puede definir el proyecto en términos de ámbito.

Este artículo se basa en estos fundamentos para que entienda cómo preparar su propio AEM proyecto sin objetivos.

## Objetivo {#objective}

Este documento le ayuda a comprender los pasos necesarios para implementar su primer proyecto. Después de leerlo, debe:

* Comprenda las consideraciones de planificación importantes para diseñar su contenido.
* Comprender los pasos para implementar sin encabezado en AEM.
* Conozca qué herramientas y configuraciones de AEM necesarias son necesarias.
* Conozca las prácticas recomendadas para que su recorrido sin objetivos sea fluido, mantenga la eficiencia de la generación de contenido y asegúrese de que el contenido se entregue rápidamente.

## Requisitos {#requirements}

Antes de continuar con este documento, asegúrese de haber revisado el documento anterior en el Recorrido para desarrolladores sin encabezado de AEM, [Introducción a AEM sin encabezado](getting-started.md) asegurarse de que:

* Cumplir los requisitos enumerados.
* Tenga en cuenta su propia definición de proyecto, que incluye ámbito, funciones y rendimiento.

## Planificación para el éxito {#planning-for-success}

Para iniciar su primer proyecto sin encabezado AEM debe asegurarse de que dispone de un modelo de contenido que admita la personalización y las actualizaciones que desee realizar en todos los canales.

Independientemente de AEM, también debe asegurarse de que tiene configurado un entorno de desarrollo adecuado si está creando una aplicación del lado del cliente para poder probar el cliente frente a las llamadas de API a AEM.

### Definición de modelos de contenido y API {#defining-models}

Desea impulsar una experiencia coherente y administrar campañas personalizadas en todos los canales, de modo que pueda ver cada canal individual y cada superficie como su propia estructura de contenido distinta a la que enviar. Sin embargo, tener cada canal con su propio modelo de contenido será difícil de mantener.

En su lugar, debe tener en cuenta cómo se relaciona el contenido en diferentes superficies basándose en principios de organización, como jerarquías de productos y marcas, categorías de bienes o superficies o pasos en el recorrido del cliente. Por ejemplo, si tiene un conjunto de superficies que admiten una marca específica de automóviles que fabrica, puede que desee comenzar con un modelo de contenido para obtener información general que sea verdadera para todo el coche y que luego tenga elementos más específicos, como el contenido necesario, cuando el coche comience a funcionar cuando haya problemas de servicio. Este modelo aplicará la herencia del contenido general de la marca de un automóvil, al tiempo que permitirá cambios basados en el contexto específico necesario. También le ayudará a administrar en el futuro las actualizaciones de este contenido, ya que puede aplicar el control en función de funciones como el especialista en marketing general o el gestor de productos para toda la marca de automóvil, frente a un autor responsable de la experiencia de &quot;inicio de coche&quot;.

Una vez que tenga el modelo de contenido y una vista clara de los distintos clientes a los que debe mostrarse el contenido, debe asegurarse de que GraphQL/API asociadas con el acceso a varios modelos de contenido se publiquen para todos los clientes que necesiten este contenido. Existen diferentes opciones para acceder a cierto contenido. Puede solicitar un contenido específico que sea estático y que permita el almacenamiento en caché del contenido y un rendimiento superior. También puede solicitar contenido que se genere dinámicamente y que requiera más procesamiento. Asegúrese de que los clientes aprovechan las API más eficientes para sus necesidades comerciales.

## Explicación de los entornos {#understanding-environments}

Dentro de AEM hay tres tipos de entornos: desarrollo, ensayo y producción.

Los entornos de desarrollo (puede tener varios) son un lugar seguro para experimentar y probar ideas. Durante la fase inicial del proyecto, el Adobe recomienda utilizar los entornos de desarrollo para probar variaciones de modelos de contenido y ver cuáles proporcionan la salida deseada para las superficies.

El entorno de ensayo de los proyectos sin periféricos se utiliza para validar las nuevas versiones de productos de AEM antes de que se implementen en producción. Mantenga una lista actualizada de los modelos de contenido de producción allí y un subconjunto del contenido, de modo que pueda tener archivos JSON procesados para comparar si siguen proporcionando la misma salida, a medida que realiza cambios o que la versión de AEM introduce cambios

La producción es donde los autores de contenido crean y administran su contenido real. Los cambios de modelo en la producción deben llevarse a cabo con cuidado y teniendo en cuenta la compatibilidad con versiones anteriores.

Durante la fase de desarrollo, se recomienda trabajar con un entorno de desarrollo y ensayo. A medida que vaya a probar el rendimiento, querrá pasar al entorno de producción.

### Cooperación de desarrolladores y autores de contenido {#cooperation}

Los desarrolladores necesitan un entorno de desarrollo de AEM configurado con los modelos de contenido rellenados. El desarrollador desarrolla el cliente que consumirá contenido desde AEM sin encabezado, ya que los autores de contenido siguen creando el contenido. Por eso las definiciones de API son muy importantes. Al aprovechar el SDK de AEM, el desarrollador puede crear un enlace de prueba para que se puedan crear pruebas cliente y unidad a fin de garantizar que el cliente pueda procesar el contenido correctamente.

Los autores de contenido crean contenido en función de los modelos de contenido que se han definido en el entorno de ensayo. Con la herramienta de creación de fragmentos de contenido, el autor crearía un nuevo fragmento de contenido o editaría un fragmento de contenido existente. Antes de publicarlo, el autor puede obtener una vista previa del aspecto que tendrá en el cliente si trabaja con el desarrollador para impulsar el modelo de contenido al desarrollo o configurar un entorno de desarrollador solo para que los autores puedan obtener una vista previa del aspecto que tendría en el cliente.

## Configuración {#setup}

Antes de comenzar con sin encabezado en AEM, debe asegurarse de que todas las funciones necesarias estén habilitadas. Esta sección describe lo que se requiere. Los pasos reales para realizar estos pasos se detallan más adelante en la sección [AEM Recorrido para desarrolladores sin objetivos.](#overview.md)

También puede consultar la [recursos adicionales](#additional-resources) para obtener más información sobre los temas individuales.

### Configuración {#configuration}

1. Habilitar fragmentos de contenido
1. Habilitar GraphQL
1. Configuración del SDK sin encabezado

## Implementación de la primera aplicación AEM sin encabezado

Se trata de una descripción general de lo que necesita para implementar su primera aplicación sin encabezado mediante AEM para entregar su contenido. La forma de llevar a cabo estos pasos se describirá en detalle en partes posteriores del Recorrido para desarrolladores sin encabezado.

1. Crear modelos de fragmento de contenido
1. Crear fragmentos de contenido
1. Consulta de contenido con GraphQL

## Prácticas recomendadas   {#best-practices}

Un proyecto sin objetivos no sólo es exitoso debido a la tecnología implementada, sino también debido a la buena planificación y a la buena gobernanza de los proyectos. A continuación se indican algunas prácticas recomendadas para que los autores y desarrolladores de contenido tengan en cuenta al planificar el proyecto.

### Organización del contenido {#organizing-content}

* Haga su estructura tan compleja como sea necesario pero manténgala lo más simple posible. Las estructuras de contenido más sencillas ayudan a optimizar la administración del contenido y a mejorar el rendimiento del sistema.
* Priorice la reutilización del contenido en su estrategia. Cree submodelos y referencias de contenido que se puedan reutilizar en varios modelos y canales de nivel superior.
* Haga que las estructuras de contenido se expliquen lo más posible para que los autores de contenido puedan aprender y adaptarse rápidamente a las tareas de creación.
* Si tiene restricciones de acceso, intente alinear su modelo de contenido con los requisitos de acceso.
* Cuando tiene requisitos de acceso, deben dirigir la jerarquía de contenido. Agrupe el contenido que edita el mismo grupo de personas.
* Agrupe contenido similar en una carpeta.
   * Es más probable que un autor de contenido copie y pegue el contenido existente para crear contenido nuevo. Por lo tanto, hacer esto en la misma carpeta lo hace más eficiente.
   * AEM permite establecer los modelos permitidos por carpeta, de modo que la variable **Crear nuevo** solo mostrará los modelos compatibles con esa ubicación.
* La creación del editor de fragmentos de contenido en línea de nuevos fragmentos de contenido se puede simplificar si la carpeta raíz está configurada en el modelo. Entonces el profesional no tiene que elegir una ubicación, pero solo necesita proporcionar un nombre y puede comenzar a editar la nueva referencia.

### Creación de contenido {#authoring}

* Para versiones específicas del canal de su contenido, considere la posibilidad de utilizar variaciones de fragmento de contenido. Las variaciones se sincronizan con el patrón de contenido para optimizar la administración del cambio de contenido.
* Invite a otros productores de contenido a revisar contenido y proporcionar comentarios con anotaciones y comentarios, que están disponibles en el editor de fragmentos de contenido y globalmente en el Admin Console de fragmentos de contenido.
* Mantenga las cosas en movimiento con el menor número posible de elementos obligatorios. Los elementos obligatorios pueden bloquear el flujo de trabajo.

### Creación de contenido global {#localization}

* Establezca reglas y gobierno para la traducción de contenido. Para reducir la carga del sistema, establezca la traducción como un proceso asincrónico que se puede ejecutar en intervalos más largos. Espere un tiempo para el control de calidad de la localización y la corrección de errores.
* Aproveche todas las funcionalidades proporcionadas por su sistema de tecnología de traducción que puede integrar con AEM, como la memoria de traducción.
* Comprenda si el contenido multimedia enriquecido, como imágenes y vídeos, necesita localización.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del Recorrido para desarrolladores sin encabezado de AEM, debe:

* Comprenda las consideraciones de planificación importantes para diseñar su contenido.
* Comprender los pasos para implementar sin encabezado en AEM.
* Conozca qué herramientas y configuraciones de AEM necesarias son necesarias.
* Conozca las prácticas recomendadas para que su recorrido sin objetivos sea fluido, mantenga la eficiencia de la generación de contenido y asegúrese de que el contenido se entregue rápidamente.

Queremos que aproveche este conocimiento fundacional para comprender completamente el poder y la flexibilidad de AEM sin cabeza para que pueda aprovecharlo para sus propios proyectos. Para ello, tiene opciones.

### Elija su propia aventura {#choose-your-path}

Independientemente del estilo de aprendizaje que tenga, Adobe quiere que tenga éxito a medida que comience con su proyecto sin objetivos AEM.

* Si prefiere continuar **obtenga información sobre conceptos sin encabezado y AEM tecnologías sin encabezado**, debe continuar con su recorrido AEM sin encabezado revisando el documento [Modelo del contenido como modelos de contenido AEM](model-your-content.md) donde aprende a modelar la estructura de contenido en AEM.
* Si prefiere **aprenda haciendo**, puede ir al [Tutorial práctico Introducción a AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) donde saltará directamente al desarrollo sin encabezado de AEM implementando un proyecto simple para exponer AEM contenido sin encabezado.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de desarrollo remoto revisando el documento [Cómo modelar el contenido como modelos AEM contenido,](model-your-content.md) los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no son necesarios para continuar en el recorrido sin encabezado.

* [recorrido de traducción AEM sin encabezado](/help/journey-headless/translation/overview.md) - Este recorrido de documentación le ofrece una amplia comprensión de la tecnología sin objetivos, AEM sirve contenido sin objetivos y cómo puede traducirlo.
* [Desarrollo sin objetivos para AEM Sites](/help/sites-developing/headless/introduction.md) - Una introducción rápida para orientar al desarrollador AEM sin encabezado con las funciones necesarias
* [Tutorials AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - Utilice estos tutoriales prácticos para explorar cómo utilizar las distintas opciones para enviar contenido a puntos de conexión sin periféricos con AEM y elegir lo que es adecuado para usted.
* [Administración de contenido sin encabezado mediante las API de GraphQL](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses) - Siga este curso para obtener una descripción general de la API de GraphQL implementada en AEM. Se requiere autenticación mediante Adobe ID.
* [AEM Guías WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql) - Este proyecto de GitHub incluye aplicaciones de ejemplo que destacan AEM API de GraphQL.
* [Guía de introducción sin encabezado](/help/sites-developing/headless/introduction.md#getting-started) - Una introducción rápida a AEM funciones sin periféricos para usuarios que ya conocen AEM.
* [Crear modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md) - Documentación técnica sobre modelos de fragmentos de contenido
* [Crear fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) - Documentación técnica sobre fragmentos de contenido
* [Consulta de contenido con GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) - Documentación técnica sobre la API de GraphQL

<!-- HM-Links
* [Introduction to the Architecture of Adobe Experience Manager as a Cloud Service](/help/overview/architecture.md) - A complete overview of AEM's architecture
* [Headless Getting Started Guide](/help/implementing/developing/headless/introduction.md#getting-started) - A quick introduction to AEM's headless features for users already knowledgeable of AEM.
* [Create Content Fragment Models](/help/assets/content-fragments/content-fragments-models.md) - Technical documentation on Content Fragment Models
* [Create Content Fragments](/help/assets/content-fragments/content-fragments.md) - Technical documentation on Content Fragments
* [Query content with GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) - Technical documentation on the GraphQL API

-->