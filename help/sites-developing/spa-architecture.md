---
title: SPA Desarrollo de la para Adobe Experience Manager
description: SPA Este artículo presenta preguntas importantes que se deben tener en cuenta al contratar a un desarrollador front-end para desarrollar una para Adobe Experience Manager AEM AEM SPA SPA AEM (en inglés) y ofrece una visión general de la arquitectura de los desarrolladores en relación con los aspectos que se deben tener en cuenta a la hora de implementar un desarrollador de soluciones de desarrollo en el entorno de la.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: c1429889-e2ed-4e2f-a45f-33f8a6a52745
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 6d961456e0e1f7a26121da9be493308a62c53e04
workflow-type: tm+mt
source-wordcount: '2018'
ht-degree: 5%

---


# Desarrollo de SPA para AEM{#developing-spas-for-aem}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. SPA Los desarrolladores quieren poder crear sitios utilizando marcos de trabajo de la y los autores quieren editar contenido dentro de Adobe Experience Manager AEM (la opción de la) sin problemas para un sitio creado con esos marcos de trabajo.

SPA AEM AEM SPA AEM Este artículo presenta preguntas importantes que se deben tener en cuenta al contratar a un desarrollador front-end para desarrollar una aplicación para la y ofrece una descripción general de la arquitectura de las soluciones de implementación de la aplicación de la aplicación de la forma de la implementación de la aplicación de la aplicación de la aplicación de la forma de un desarrollador de front-end en la implementación de la implementación de la aplicación de la en la.

{{ue-over-spa}}

## SPA AEM Principios de desarrollo de la {#spa-development-principles-for-aem}

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador front-end sigue las prácticas recomendadas estándar al crear una SPA. AEM SPA AEM Si, como desarrollador front-end, sigue estas prácticas recomendadas generales y algunos principios específicos de la, su equipo funcionará con [y sus capacidades de creación de contenido](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa).

* **[Portabilidad](/help/sites-developing/spa-architecture.md#portability) -** Al igual que con cualquier componente, los componentes deben crearse para que sean lo más portátiles posible. La SPA debe crearse con componentes transferibles y reutilizables.
* **[AEM impulsa la estructura del sitio](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)**: el desarrollador front-end crea componentes y posee su estructura interna, pero depende de AEM para definir la estructura de contenido del sitio.
* **[Procesamiento dinámico](/help/sites-developing/spa-architecture.md#dynamic-rendering)**: todo el procesamiento debe ser dinámico.
* SPA AEM **[Enrutamiento dinámico](#dynamic-routing) -**: El es responsable del enrutamiento, lo escucha y realiza recuperaciones basadas en él. Cualquier enrutamiento también debe ser dinámico.

SPA AEM Si tiene en cuenta estos principios a medida que desarrolle su, será lo más flexible y tendrá la mayor garantía de futuro posible, al tiempo que se habilitan todas las funcionalidades de creación de contenido compatibles.

AEM SPA Si no necesita ser compatible con las características de creación de la, es posible que tenga que considerar un [modelo de diseño](/help/sites-developing/spa-architecture.md#spa-design-models) diferente.

### Portabilidad {#portability}

Al igual que al desarrollar cualquier componente, los componentes deben diseñarse de tal manera que maximice su portabilidad. Debe evitarse cualquier patrón que vaya en contra de la portabilidad o reutilización de los componentes para garantizar la compatibilidad, flexibilidad y capacidad de mantenimiento en el futuro.

SPA El resultado debe ser construido con componentes altamente portátiles y reutilizables.

### AEM Estructura del sitio de {#aem-drives-site-structure}

SPA El desarrollador front-end debe considerarse a sí mismo como responsable de crear una biblioteca de componentes de que se utilizan para crear la aplicación. El desarrollador front-end tiene un control total de la estructura interna de los componentes. AEM [Sin embargo, en todo momento, el usuario es propietario de la estructura del sitio.](/help/sites-developing/spa-overview.md)

Esto significa que el desarrollador front-end puede añadir contenido del cliente antes o después del punto de entrada de los componentes y también puede realizar llamadas de terceros dentro del componente. Sin embargo, el desarrollador front-end no tiene control total sobre cómo se anidan los componentes, por ejemplo.

### Procesamiento dinámico {#dynamic-rendering}

SPA La solo debe depender de la renderización dinámica del contenido. AEM Esta es la expectativa predeterminada en la que la recupera y procesa todos los elementos secundarios de la estructura de contenido.

AEM Cualquier renderización explícita que apunte a contenido específico se considera una renderización estática y, aunque se admite, no es compatible con las funciones de creación de contenido que se estén utilizando para la creación de contenido de la. Esto también va en contra del principio de [portabilidad](/help/sites-developing/spa-architecture.md#portability).

### Enrutamiento dinámico {#dynamic-routing}

Al igual que con el procesamiento, todo el enrutamiento también debe ser dinámico. AEM SPA AEM En, [la siempre debe ser propietaria del enrutamiento](/help/sites-developing/spa-routing.md) y, a la vez, la escucha y recupera el contenido basado en él, de manera que la escucha de manera correcta.

AEM Cualquier enrutamiento estático funciona en contra del [principio de portabilidad](/help/sites-developing/spa-architecture.md#portability) y limita al autor al no ser compatible con las características de creación de contenido de los programas de trabajo de los que se puede crear contenido. Por ejemplo, con el enrutamiento estático, si el autor de contenido desea cambiar una ruta o cambiar una página, tendría que pedirle al desarrollador front-end que lo haga.

## Tipo de archivo del proyecto AEM {#aem-project-archetype}

Cualquier proyecto AEM debería utilizar el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es), que admite proyectos de SPA que utilizan React o Angular y aprovecha el SDK de SPA.

## SPA Modelos de diseño {#spa-design-models}

SPA AEM SPA AEM Si se siguen los [principios de desarrollo de la en el ](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem), entonces el funcionará con todas las características de creación de contenido de la admitidas.

Sin embargo, puede haber casos en los que esto no sea del todo necesario. En la tabla siguiente se ofrece una descripción general de los distintos modelos de diseño, sus ventajas y sus desventajas.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de diseño<br /> </strong></th>
   <th><strong>Ventajas</strong></th>
   <th><strong>Desventajas</strong></th>
  </tr>
  <tr>
   <td>AEM se utiliza como CMS SPA sin encabezado sin usar el marco de trabajo de <a href="/help/sites-developing/spa-reference-materials.md">Editor SDK de.</a></td>
   <td>El desarrollador front-end tiene control total sobre la aplicación.</td>
   <td><p>AEM Los autores de contenido no pueden utilizar la experiencia de creación de contenido de.</p> <p>El código no es portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables a través de JCR.</p> </td>
  </tr>
  <tr>
   <td>SPA El desarrollador front-end utiliza el marco de trabajo de SDK del Editor de, pero solo abre algunas áreas al autor del contenido.</td>
   <td>El desarrollador mantiene el control de la aplicación y solo permite la creación en áreas restringidas de la aplicación.</td>
   <td><p>AEM Los autores de contenido están restringidos a un conjunto limitado de experiencias de creación de contenido que se pueden crear con un contenido de la.</p> <p>El código corre el riesgo de no ser ni portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables a través del JCR.</p> </td>
  </tr>
  <tr>
   <td>SPA El proyecto utiliza completamente el SDK AEM del Editor de, y los componentes de front-end se desarrollan como una biblioteca y la estructura de contenido de la aplicación se delega a los.</td>
   <td><p>La aplicación es reutilizable y portátil.</p> <p>AEM El autor del contenido puede editar la aplicación usando la experiencia de creación de contenido que se está usando para la creación de contenido de la.<br /> </p> <p>SPA La plantilla es compatible con el editor de plantillas de.</p> </td>
   <td><p>AEM El desarrollador no controla la estructura de la aplicación ni la parte de contenido delegada a la que se ha delegado la aplicación en el usuario.</p> <p>AEM El desarrollador puede seguir reservando áreas de la aplicación para el contenido que no vaya a crearse con la ayuda de la herramienta de creación de segmentos de contenido de la aplicación de la aplicación de tipo de.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM SPA AEM SPA AEM Aunque todos los modelos son compatibles con los modelos, solo implementando el tercero (y, por lo tanto, siguiendo los [principios de desarrollo recomendados en el caso de los autores de contenido en el caso de los) los autores de contenido pueden interactuar con el contenido de los modelos y editarlo a medida que se vayan acostumbrando a él, en la medida en que lo hagan.](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

## SPA AEM Migración de recursos existentes a la {#migrating-existing-spas-to-aem}

SPA SPA AEM SPA AEM AEM SPA Por lo general, si el sigue los [Principios de desarrollo de la](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem), el usuario trabajará en el entorno de trabajo y podrá editarlo usando el Editor de la de trabajo de la aplicación .

SPA AEM Siga estos pasos para preparar sus existentes para trabajar con ellos.

1. **Haga que sus componentes JS sean modulares.**

   Permitir que se representen en cualquier orden, posición y tamaño.
1. **Use los contenedores proporcionados por SDK de Adobe para colocar los componentes en la pantalla.**

   AEM proporciona un componente del sistema de páginas y párrafos para que lo utilice.
1. AEM **Crear un componente de la para cada componente de JS.**

   AEM Los componentes de definen el cuadro de diálogo y la salida JSON.

## Instrucciones para desarrolladores de front-end {#instructions-for-front-end-developers}

SPA AEM La tarea principal al involucrar a un desarrollador front-end para crear una para la creación de segmentos es acordar sobre los componentes y sus modelos JSON.

SPA AEM A continuación se describen los pasos que debe seguir un desarrollador front-end al desarrollar una para la creación de segmentos de cliente de la interfaz de usuario de la interfaz de usuario de.

1. **Aceptar componentes y su modelo JSON**

   AEM SPA Los desarrolladores de front-end y de back-end deben ponerse de acuerdo sobre qué componentes son necesarios y un modelo, de modo que haya una coincidencia individualizada entre los componentes de la interfaz de usuario y los componentes de back-end de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario.

   AEM La mayoría de los componentes todavía son necesarios para proporcionar cuadros de diálogo de edición y para exportar el modelo de componente.

1. **En los componentes de React, acceda al modelo a través de`this.props.cqModel`**

   SPA Una vez acordados los componentes y configurado el modelo JSON, el desarrollador front-end es libre de desarrollar el modelo y puede acceder al modelo JSON a través de `this.props.cqModel`.

1. **Implementar el método `render()` del componente**

   El desarrollador front-end implementa el método `render()` como crea conveniente y puede utilizar los campos de la propiedad `cqModel`. Esto genera el DOM y los fragmentos de HTML que se insertan en la página. Esta es la forma estándar de crear una aplicación en React.

1. AEM **Asigne el componente al tipo de recurso de a través de`MapTo()`**

   La asignación almacena clases de componentes y el componente `Container` proporcionado la utiliza internamente para recuperar y crear instancias de componentes de forma dinámica en función del tipo de recurso dado.

   Esto sirve como &quot;pegamento&quot; entre el front-end y el back-end para que el editor sepa a qué componentes corresponden los componentes de react.

   `Page` y `ResponsiveGrid` son buenos ejemplos de clases que amplían la base `Container`.

1. **Defina `EditConfig` del componente como parámetro para`MapTo()`**

   Este parámetro es necesario para indicar al editor cómo se debe asignar un nombre al componente, siempre que no se haya procesado aún o no tenga contenido para procesar.

1. **Extender la clase `Container` proporcionada para páginas y contenedores**

   Los sistemas de páginas y párrafos deben ampliar esta clase para que la delegación a los componentes internos funcione según lo esperado.

1. **Implementar una solución de enrutamiento que use la API HTML5 `History`.**

   Cuando `ModelRouter` está habilitado, al llamar a las funciones `pushState` y `replaceState` se déclencheur una solicitud a `PageModelManager` para recuperar un fragmento que falta del modelo.

   La versión actual de `ModelRouter` solo admite el uso de direcciones URL que apunten a la ruta de recursos real de los puntos de entrada del modelo Sling. No admite el uso de direcciones URL o alias de vanidad.

   `ModelRouter` se puede deshabilitar o configurar para que ignore una lista de expresiones regulares.

## AEM agnóstico {#aem-agnostic}

Estos bloques de código ilustran cómo los componentes de React y Angular no necesitan nada que sea específico o de Adobe AEM de la.

* Todo lo que se encuentra dentro del componente JavaScript AEM no es compatible con el uso de la.
* AEM AEM Sin embargo, lo que es específico de la es que el componente JS debe asignarse a un componente de la aplicación de seguridad de la aplicación de ayuda de MapTo.

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

El asistente de `MapTo` es el &quot;pegado&quot; que permite hacer coincidir los componentes del back-end y del front-end:

* Indica al contenedor de JS (o sistema de párrafos de JS) qué componente de JS es responsable de procesar cada uno de los componentes presentes en el JSON.
* Agrega un atributo de datos de HTML al HTML SPA que procesa el componente JS, de modo que el Editor de datos sepa qué cuadro de diálogo mostrar al autor al editar el componente.

SPA AEM Para obtener más información sobre el uso de `MapTo` y la generación de la para los usuarios en general, consulte la guía de introducción para el marco de trabajo elegido.

* [SPA AEM Introducción a la administración de la en React](/help/sites-developing/spa-getting-started-react.md)
* [SPA AEM Introducción a la administración de la en Angular](/help/sites-developing/spa-getting-started-angular.md)

## AEM SPA Arquitectura de la y la {#aem-architecture-and-spas}

AEM SPA La arquitectura general de los entornos de desarrollo, creación y publicación, entre otros, no cambia al utilizar la. SPA Sin embargo, es útil comprender cómo encaja el desarrollo de la en esta arquitectura.

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **Entorno de compilación**

  SPA Aquí es donde se extrae el origen del origen de la aplicación y del origen del componente de la aplicación de la.

   * SPA El generador clientlib de NPM crea una biblioteca de cliente a partir del proyecto de.
   * AEM Maven se encarga de tomar esa biblioteca e implementarla el complemento de compilación de Maven junto con el componente al autor de la.

* AEM **Autor de**

  AEM SPA El contenido se crea en el autor de la, incluido el autor de la creación

  SPA SPA Cuando se edita una con el Editor de en el entorno de creación:

   1. SPA El HTML externo se lo solicita el.
   1. Se carga el CSS.
   1. Se carga la JavaScript SPA de la aplicación de la.
   1. SPA Cuando se ejecuta la aplicación de, se solicita el JSON, lo que permite a la aplicación crear el DOM de la página, incluidos los atributos `cq-data`.
   1. Estos atributos de `cq-data` permiten al editor cargar información de página adicional para saber qué configuraciones de edición están disponibles para los componentes.

* AEM **Publish**

  SPA Aquí es donde el contenido creado y las bibliotecas compiladas, incluidos los artefactos de aplicación, clientlibs y componentes, se publican para uso público.

* **Dispatcher / CDN**

  Dispatcher AEM sirve como capa de almacenamiento en caché de los recursos para los visitantes del sitio.

   * AEM Las solicitudes se procesan de forma similar a como se encuentran en el autor de la página, pero no hay ninguna solicitud de información de la página porque solo la necesita el editor.
   * JavaScript, CSS, JSON y HTML se almacenan en caché, lo que optimiza la página para una entrega rápida.

>[!NOTE]
>
>AEM Dentro de, no es necesario ejecutar los mecanismos de compilación de JavaScript ni ejecutar el propio JavaScript. AEM SPA solo aloja los artefactos compilados de la aplicación de la.

## Siguientes pasos {#next-steps}

SPA AEM Para obtener una descripción general de cómo está estructurado un sencillo en el trabajo de la, consulte la guía de introducción para [React](/help/sites-developing/spa-getting-started-react.md) y [Angular](/help/sites-developing/spa-getting-started-angular.md).

SPA AEM SPA Para obtener una guía paso a paso sobre cómo crear sus propios, consulte el [Tutorial de introducción al Editor de eventos de WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=es) de la página de inicio de la página de inicio de la página de inicio de la página de inicio de la aplicación Editor de eventos de WKND.

SPA AEM SPA Para obtener más información acerca de la asignación de modelos dinámicos a componentes y cómo funciona dentro de la asignación de componentes en el modelo dinámico, vea el artículo [Asignación de modelos dinámicos a componentes para la asignación de componentes para el modelo dinámico para la asignación de componentes para el modelo dinámico para la asignación de componentes para la asignación de componentes para el modelo dinámico para la asignación de componentes para la asignación de componentes para la asignación de componentes para la asignación de componentes para la asignación de componentes para el modelo dinámico para la asignación de componentes para la asignación de componentes10000000000000000001010000000000000000000000000000000000000000010000000000000000000000000000000](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)

Si desea implementar la implementación de la en un Angular SPA de trabajo que no sea React o SPA AEM, o simplemente desea profundizar en cómo funciona el modelo de trabajo de SDK AEM SPA para la, consulte el artículo de [Modelo de trabajo](/help/sites-developing/spa-blueprint.md).
