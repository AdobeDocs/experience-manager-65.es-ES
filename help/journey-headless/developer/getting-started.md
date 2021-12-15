---
title: Introducción a AEM sin encabezado
description: En esta parte del Recorrido para desarrolladores sin encabezado de AEM, obtenga información sobre AEM requisitos previos sin encabezado.
source-git-commit: 919cef01470dd930884e97b15f2d40a38872c0d0
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 1%

---

# Introducción a AEM sin encabezado {#getting-started}

En esta parte del [AEM Recorrido para desarrolladores sin encabezado,](overview.md) obtenga información sobre lo que se necesita para comenzar su propio proyecto con AEM sin encabezado.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido sin AEM, [Obtenga Información Sobre El Desarrollo Sin Cabeza De CMS](learn-about.md) aprendió la teoría básica de lo que es un CMS sin cabeza y ahora debería:

* Comprender los conceptos básicos y la terminología de la entrega de contenido sin encabezado
* Comprender por qué y cuándo se requiere un proceso sin encabezado
* Conocer en un nivel superior cómo se utilizan los conceptos sin encabezado y cómo se interrelacionan

Este artículo se basa en estos fundamentos para que entienda cómo puede utilizar AEM para implementar una solución sin encabezado.

## Objetivo {#objective}

Este documento le ayuda a comprender AEM sin encabezado en el contexto de su propio proyecto. Después de leer, debe:

* Comprender los conceptos básicos de AEM funciones sin encabezado.
* Conozca los requisitos previos para utilizar AEM funciones sin encabezado.
* Tenga en cuenta AEM niveles de integración sin objetivos.
* Puede definir el proyecto en términos de ámbito.

## Conceptos básicos de AEM {#aem-basics}

Para poder definir el proyecto sin encabezado dentro de AEM, es importante comprender algunos conceptos básicos de AEM.

### Instancia de autor {#author}

En su versión más sencilla, AEM consta de una instancia de autor y una [instancia de publicación](#publish) que trabajan juntos para crear, administrar y publicar el contenido.

El contenido comienza en la instancia de autor. Aquí es donde los autores de contenido crean su contenido. El entorno de creación ofrece varias herramientas para que los autores creen, organicen y reutilicen su contenido.

### Instancia de publicación {#publish}

Una vez creado el contenido en la instancia de autor, debe publicarse para que esté disponible para otros servicios que lo consuman. Una instancia de publicación contiene todo el contenido que se ha publicado.

### Replicación {#replication}

La replicación es el acto de transferir contenido de la instancia de autor a la instancia de publicación. Esto se hace automáticamente AEM cuando un autor u otro usuario con los derechos adecuados publica contenido.

### Resumen de fundamentos de AEM {#aem-basics-summary}

En su nivel más sencillo, la creación de experiencias digitales en AEM requiere los siguientes pasos:

1. Los autores de contenido crean su contenido sin encabezado en la instancia de autor.
1. Cuando este contenido está listo, se replica en la instancia de publicación.
1. Luego se puede llamar a las API para recuperar este contenido.

AEM sin objetivos crea esta base técnica al ofrecer herramientas potentes para administrar el contenido sin objetivos [se describe en la siguiente sección.](#aem-headless-basics)

## Conceptos básicos AEM sin encabezado {#aem-headless-basics}

Las capacidades sin objetivos de AEM se basan en algunas funciones clave. Estos se explican en detalle en partes posteriores del recorrido. Ahora sólo es importante conocer los conceptos básicos de lo que hacen y cómo se llaman.

### Modelos de fragmento de contenido {#content-fragment-models}

Los modelos de fragmento de contenido definen la estructura de los datos y el contenido que se crean y administran en AEM. Sirven como un tipo de andamiaje para el contenido. Al elegir crear contenido, los autores seleccionan entre los modelos de fragmento de contenido que defina, que los guían en la creación de contenido.

### Fragmentos de contenido {#content-fragments}

Los fragmentos de contenido le permiten diseñar, crear, depurar y publicar contenido independiente de las páginas. Permiten preparar contenido listo para usar en varias ubicaciones y en varios canales.

Los fragmentos de contenido contienen contenido estructurado y se pueden entregar en formato JSON.

### API de GraphQL y REST {#apis}

Para modificar el contenido sin problemas, AEM ofrece dos API sólidas.

* La API de GraphQL permite crear solicitudes para acceder a los fragmentos de contenido y enviarlos.
* La API de REST de recursos permite crear y modificar fragmentos de contenido (y otros recursos).

Aprenderá a utilizar estas API en una parte posterior del recorrido sin AEM encabezado. O consulte la [recursos adicionales](#additional-resources) para obtener más documentación.

## Niveles de integración sin encabezado {#integration-levels}

AEM admite todos los modelos sin encabezado y los modelos tradicionales de pila completa o de cabeza de un CMS. Sin embargo, AEM ofrece no solo estas dos opciones exclusivas, sino también la capacidad de soportar modelos híbridos que combinan las ventajas de ambos, ofreciendo una flexibilidad única para su proyecto sin objetivos.

Con el fin de garantizar su comprensión de los conceptos sin objetivos, este Recorrido para desarrolladores AEM sin objetivos se centra en el modelo sin objetivos para ponerle en marcha lo antes posible sin necesidad de utilizar código en AEM.

Sin embargo, hay que tener en cuenta las posibilidades híbridas adicionales que se abren una vez que entienda AEM características sin periféricos. Estos casos se detallan a continuación para su sensibilización. Al final del recorrido, se le introducirán estos conceptos con más detalle en caso de que se requiera dicha flexibilidad para su proyecto.

### Ya tiene un consumo externo de contenido sin encabezado, como una aplicación de una sola página (SPA). {#already-have-a-spa}

Supongamos que su requisito básico es, como mínimo, entregar contenido de AEM a un servicio externo existente.

#### Nivel 1: Integración de fragmentos de contenido: modelo tradicional sin encabezado {#level-1}

Este nivel de integración es el modelo tradicional sin encabezado y permite a los autores de contenido crear contenido en AEM y ofrecerlo sin preocuparse por cualquier número de servicios externos mediante GraphQL o editarlos desde servicios externos mediante la API de Assets. No se requiere código en AEM.

En este modelo, AEM solo se utiliza para crear y servir el contenido mediante AEM fragmentos de contenido. El procesamiento y la interacción con el contenido se delegan en la aplicación externa consumidora, a menudo en una aplicación de una sola página (SPA).

#### Nivel 2: Incrustar el SPA en AEM - Modelo híbrido {#level-2}

Este nivel de integración se basa en el primer nivel, pero también permite que la aplicación externa (SPA) se incruste en AEM para que los autores de contenido puedan ver el contenido en el contexto de la aplicación externa dentro de AEM. La aplicación también puede admitir una edición limitada de la aplicación externa dentro de AEM.

Este nivel tiene la ventaja de permitir que los autores de contenido creen contenido de forma flexible de AEM de forma progresiva, con su contenido presentado en contexto con una SPA externa integrada, a la vez que siguen entregando el contenido sin problemas.

#### Nivel 3: Incrustar y activar completamente SPA en AEM - Modelo híbrido {#level-3}

Este nivel de integración se basa en el nivel dos al permitir que la mayoría del contenido de la SPA externa se pueda editar dentro de AEM.

### Todavía no tiene un consumidor externo del contenido sin encabezado, como una aplicación de una sola página (SPA). {#do-not-have-a-spa}

Si su objetivo es crear un nuevo SPA que consuma contenido sin encabezado desde AEM, puede utilizar funciones como Fragmentos de contenido para administrar el contenido sin encabezado y también generar un SPA con AEM marco de Editor SPA.

Con el Editor de SPA, el SPA no solo consume contenido de AEM, sino que también es totalmente editable dentro de AEM por los autores de contenido, lo que le ofrece la flexibilidad de envío sin periféricos y de edición en contexto dentro de AEM.

## Requisitos y requisitos previos {#requirements-prerequisites}

Hay varios requisitos antes de comenzar su proyecto de AEM sin encabezado.

### Conocimiento {#knowledge}

* GraphQL
* Experiencia de desarrollo crear SPA con marcos de React o Angular
* Capacidades básicas AEM crear fragmentos de contenido y utilizar el editor

### Herramientas {#tools}

* Acceso a espacio aislado para probar la implementación de su proyecto
* Instancia de desarrollo local para modelado y prueba de datos
* SPA externa existente u otro consumidor de su contenido AEM sin encabezado

## Definición del proyecto {#defining-your-project}

Para que cualquier proyecto tenga éxito, es importante definir claramente no sólo los requisitos del proyecto, sino también las funciones y responsabilidades.

### Ámbito {#scope}

Es importante tener un ámbito claramente definido para el proyecto. El ámbito informa los criterios de aceptación y le permite establecer una definición de hecho.

La primera pregunta que deben hacer es &quot;¿Qué estoy tratando de lograr con AEM sin cabeza?&quot; La respuesta debe ser, en general, que tiene o tendrá en el futuro una aplicación de experiencia que ha creado con sus propias herramientas de desarrollo, no con AEM. Esta aplicación de experiencia puede ser una aplicación móvil, un sitio web o cualquier otra aplicación de experiencia de cara al cliente del usuario final. El objetivo de utilizar AEM sin encabezado es alimentar su aplicación de experiencia con contenido creado, almacenado y administrado en AEM con API de última generación que llamarían a AEM sin encabezado para recuperar contenido o incluso contenido completamente CRUD directamente desde su aplicación de experiencia. Si esto no es lo que está buscando hacer, probablemente desee [vuelva a la documentación de AEM](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es) y busque la sección que mejor se adapte a lo que desea lograr.

### Funciones y responsabilidades {#roles-responsibilities}

Las funciones de cualquier proyecto individual varían, pero las importantes que se deben tener en cuenta en el contenido de AEM desarrollo sin objetivos son:

* [Administrador](#administrator)
* [Autor de contenido](#content-author)
* [Arquitecto de contenido](#content-architect)
* [Desarrollador](#developer)

#### Administrador {#administrator}

El administrador es responsable de la configuración y configuración base de su sistema. Por ejemplo, el administrador configura su organización dentro del sistema de administración de usuarios de Adobe, denominado Sistema Identity Management (IMS). El administrador es el primer usuario de la organización que recibe una invitación por correo electrónico de Adobe una vez que su organización ha sido creada por el Adobe dentro de IMS. El administrador puede iniciar sesión en IMS y agregar usuarios de otras personas.

Una vez que el administrador ha configurado los usuarios, se les conceden los permisos para acceder a todos los recursos de AEM para realizar su trabajo como contribuyentes a la entrega de la aplicación de experiencia mediante AEM sin encabezado.

El administrador debe ser el usuario que configure AEM y prepare el entorno de tiempo de ejecución para habilitar [autores de contenido](#content-author) para crear y actualizar contenido y [desarrolladores](#developer) para utilizar API que recuperen o modifiquen contenido para sus aplicaciones de experiencia.

#### Autor de contenido {#content-author}

Los autores de contenido crean y administran el contenido que AEM entrega sin encabezado. Los autores de contenido utilizan funciones AEM, como los fragmentos de contenido y la consola Recursos, para administrar su contenido.

Los autores de contenido deben tener en cuenta las siguientes prácticas recomendadas.

#### Plan de traducción {#translation}

Planifique la traducción al inicio del proyecto. Considere a &quot;especialista en traducción&quot; como una persona independiente cuya responsabilidad es definir qué contenido debe traducirse y qué no debe traducirse, y qué contenido traducido pueden modificar los productores de contenido regionales o locales.

Cree un plan sobre la traducción de contenido que necesita.

* ¿Necesita idiomas diferentes o también un idioma para adoptar los detalles regionales?
* ¿Necesita contenido multimedia enriquecido como imágenes o vídeos para que sea diferente en diferentes configuraciones regionales?

Obtenga información clara sobre el flujo de trabajo de actualización de contenido. ¿Cuál es el proceso de aprobación que debe admitir el sistema? ¿Se pueden aprovechar AEM flujos de trabajo para automatizar este proceso?

Tenga en cuenta que [jerarquía de contenido](#content-hierarchy) se puede aprovechar para facilitar la traducción.

Consulte la [recursos adicionales](#additional-resources) para obtener documentación adicional sobre AEM flujos de trabajo y herramientas de traducción, incluidos vínculos al Recorrido de traducción sin encabezado de AEM.

##### Aprovechar la jerarquía de contenido {#content-hierarchy}

La jerarquía de carpetas puede abordar dos preocupaciones principales con respecto a la administración de contenido:

* [Traducción](#translation) : AEM administra la traducción del contenido manteniendo copias del contenido en carpetas específicas de la configuración regional.
* Organización: las carpetas se utilizan para definir una jerarquía de contenido necesaria para satisfacer las necesidades de traducción, así como para administrar lógicamente los fragmentos de contenido.

AEM permite una estructura de contenido flexible y una jerarquía puede ser arbitrariamente grande. Sin embargo, es importante darse cuenta de que cualquier cambio en la estructura de carpetas puede tener consecuencias no deseadas para las consultas existentes que [confíe en la ruta de contenido.](#developer) Por lo tanto, una jerarquía bien definida y claramente establecida por adelantado, puede ser útil para los autores de contenido.

Las carpetas también se pueden restringir para permitir solo ciertos tipos de contenido (según los modelos de fragmento de contenido). Se recomienda especificar siempre explícitamente qué modelos se permiten para todas las carpetas de la jerarquía. Especificación del contenido permitido para una carpeta determinada:

* Evita que los autores de contenido creen contenido que no pertenece a la carpeta.
* Optimiza el proceso de creación de contenido filtrando los tipos de contenido permitidos en la carpeta durante la creación para mostrar solo tipos de contenido válidos.

Al crear una estructura de contenido adecuada, resulta más fácil coordinar la creación de contenido sin encabezado en todos los canales para maximizar la reutilización de contenido. El aprovechamiento del contenido en varios canales mejora considerablemente la eficacia de la producción de contenido y la administración de cambios.

##### Establecer convenciones de nombres adecuados {#naming-conventions}

Los nombres de los fragmentos de contenido deben ser descriptivos para los autores de contenido. AEM gestiona de forma transparente la omisión o el truncamiento de los nombres que usan los ID en el nivel del repositorio. Por lo tanto, los nombres lógicos proporcionados por los autores de contenido siempre deben ser legibles y representar el contenido.

* Nombre incorrecto: `cta_btn_1`
* Nombre correcto: `Call To Action Button`

Consulte la [recursos adicionales](#additional-resources) para obtener documentación adicional sobre AEM convenciones de nomenclatura de páginas.

##### No extender el anidado de contenido {#content-nesting}

[Fragmentos de contenido](#content-fragments) se utilizan en AEM para crear contenido sin encabezado. AEM admite hasta diez niveles de anidación de contenido para fragmentos de contenido. Sin embargo, es importante tener en cuenta que AEM debe resolver de forma iterativa cada referencia definida en el fragmento de contenido principal y, a continuación, comprobar si hay alguna referencia secundaria en todos los elementos del mismo nivel. Estas operaciones pueden sumarse rápidamente y convertirse en un problema de rendimiento.

Como regla general, las referencias de fragmento de contenido no deben anidarse más allá de cinco niveles.

#### Arquitecto de contenido {#content-architect}

Los arquitectos de contenido analizan los requisitos de los datos que deben entregarse sin interrupciones y definen la estructura de estos datos. Estas estructuras se denominan [Modelos de fragmento de contenido](#content-fragment-models) en AEM. Los modelos de fragmento de contenido se utilizan como base para los fragmentos de contenido que crean los autores de contenido.

Un enfoque útil a la hora de definir modelos de fragmento de contenido es crear modelos que se asignen a los componentes UX de las aplicaciones que consumen el contenido.

Dado que los autores de contenido interactúan con los modelos de forma continua a medida que crean contenido nuevo, alinear los modelos con el usuario les ayuda a visualizar la experiencia digital resultante. Siguiendo con esta alineación, puede asignar iconos a los modelos de fragmento de contenido que representan el elemento UX para que los autores puedan seleccionar de forma intuitiva el modelo correcto en función de las indicaciones visuales.

#### Desarrollador {#developer}

Los desarrolladores son responsables de unir el contenido que se crea sin problemas en AEM al consumidor de ese contenido, que a menudo puede ser una aplicación de una sola página (SPA), una aplicación web progresiva (PWA), una tienda web u otro servicio externo a AEM.

GraphQL sirve de &quot;pegamento&quot; entre AEM y los consumidores de contenido sin encabezado. GraphQL es el idioma que consulta AEM el contenido necesario.

Los desarrolladores deben tener en cuenta algunas recomendaciones básicas al planificar sus consultas:

* Las consultas no deben depender de una ruta fija (`ByPath`) para recuperar fragmentos de contenido.
   * [Los autores de contenido tienen control total sobre la jerarquía de fragmentos de contenido](#content-hierarchy) y podría realizar cambios que podrían romper dicha consulta.
   * Las consultas deben optar por referencias del modelo de fragmento de contenido con parámetros de consulta dinámicos para filtrar los resultados y generar la carga útil deseada.
* Para obtener el mejor rendimiento de las consultas, utilice siempre consultas persistentes en AEM. Estos se discuten más adelante en el recorrido.
* GraphQL es declarativo siguiendo el lema &quot;Pide exactamente lo que necesitas, y consigue exactamente eso&quot;. Esto significa que, al crear consultas de GraphQL, siempre evite `select *`consultas de tipo -que puede crear en una base de datos relacional.

Para un [implementación típica sin encabezado mediante AEM,](#level-1) el desarrollador no necesita tener conocimientos de codificación de AEM.

### Requisitos de rendimiento {#performance-requirements}

Para que cualquier proyecto sea un éxito, el rendimiento debe tenerse en cuenta antes de crear cualquier contenido.

Debe comprender las expectativas de los usuarios/visitantes y diseñar para ellos. Establezca objetivos de nivel de servicio (SLO) y mida para comprender si cumple con las expectativas del usuario.

#### Patrones de tráfico {#traffic-patterns}

Para comprender los patrones de tráfico y tráfico, comience por reunir lo que sabe del pasado y luego proyectar el crecimiento esperado en los próximos años. Algunas de las variables más importantes a tener en cuenta:

* ¿Cuántas llamadas a la API por hora/día/mes espera y hay potencial para picos y temporalidad?
* ¿Cuántos autores de contenido diferentes hay?
* ¿Cuántos autores de contenido espera que trabajen simultáneamente?
* ¿Cuál es la frecuencia de las actualizaciones de contenido?
* ¿Cuántos modelos de contenido se necesitan?
* ¿Cuántas instancias de modelos se necesitan?

#### Frecuencia de actualización {#update-frequency}

A menudo, las diferentes secciones de experiencias tienen distintas frecuencias de actualizaciones de contenido. Comprender esto es importante para poder ajustar las configuraciones de CDN y caché. Esto también es importante para la [Arquitectos de contenido](#content-architects) a medida que diseñan modelos para representar su contenido. Tenga en cuenta lo siguiente:

* ¿Deben caducar algunos tipos de contenido después de un período determinado?
* ¿Hay elementos específicos del usuario que no se pueden almacenar en caché?

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del Recorrido para desarrolladores sin encabezado de AEM, debe:

* Comprender los conceptos básicos de AEM funciones sin encabezado.
* Conozca los requisitos previos para utilizar AEM funciones sin encabezado.
* Tenga en cuenta AEM niveles de integración sin objetivos.
* Puede definir el proyecto en términos de ámbito.

Debe continuar con su recorrido sin AEM para la próxima revisión del documento [Ruta a la primera experiencia usando AEM sin encabezado](path-to-first-experience.md) donde aprenderá a configurar las herramientas necesarias y a empezar a pensar en modelar los datos en AEM.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de desarrollo remoto revisando el documento [Ruta a la primera experiencia usando AEM sin encabezado,](path-to-first-experience.md) los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no son necesarios para continuar en el recorrido sin encabezado.

* [recorrido de traducción AEM sin encabezado](/help/journey-headless/translation/overview.md) - Este recorrido de documentación le ofrece una amplia comprensión de la tecnología sin objetivos, AEM sirve contenido sin objetivos y cómo puede traducirlo.
* [Tutorials AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - Utilice estos tutoriales prácticos para explorar cómo utilizar las distintas opciones para enviar contenido a puntos de conexión sin periféricos con AEM y elegir lo que es adecuado para usted.
* [Administración de contenido sin encabezado mediante las API de GraphQL](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses) - Siga este curso para obtener una descripción general de la API de GraphQL implementada en AEM. Se requiere autenticación mediante Adobe ID.
* [AEM Guías WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql) - Este proyecto de GitHub incluye aplicaciones de ejemplo que destacan AEM API de GraphQL.
* [Conceptos sobre la creación](/help/sites-authoring/author.md) : Documentación técnica para el entorno de creación de AEM que incluye detalles sobre la configuración de creación y publicación
* [Publicación de páginas](/help/sites-authoring/publishing-pages.md) - Documentación técnica para la publicación de contenido en AEM
* [Convenciones de nomenclatura](/help/sites-developing/naming-conventions.md) - Documentación técnica de las restricciones de nomenclatura de páginas en AEM
* [Traducción y administrador de varios sitios](/help/sites-administering/msm-and-translation.md) - Documentación técnica sobre AEM potentes funciones de traducción
* [AEM flujos de trabajo](/help/sites-authoring/workflows.md) : Documentación técnica sobre cómo automatizar flujos de trabajo en AEM
* [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) : Documentación técnica para fragmentos de contenido.
* [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md) : Documentación técnica para modelos de fragmento de contenido.
* [Documentación técnica de GraphQL](https://graphql.org) - La definición de GraphQL (vínculo externo)
* [API de GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) : Documentación técnica que explica cómo crear solicitudes para acceder y enviar fragmentos de contenido
* [API de REST de recursos](/help/assets/assets-api-content-fragments.md) : Documentación técnica que explica cómo crear y modificar fragmentos de contenido (y otros recursos)
* [Consultas persistentes](/help/assets/content-fragments/graphql-api-content-fragments.md#persisted-queries-caching) - Documentación técnica sobre consultas persistentes en AEM
* [Encabezado y sin cabeza en AEM](/help/sites-developing/headful-headless.md) - Un análisis completo de los niveles de integración sin objetivos disponibles en AEM
