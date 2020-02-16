---
title: Desarrollo de SPA para AEM
seo-title: Desarrollo de SPA para AEM
description: En este artículo se presentan importantes cuestiones que hay que tener en cuenta a la hora de contratar a un desarrollador front-end para que desarrolle un SPA para AEM, así como una descripción general de la arquitectura de AEM con respecto a los SPA que hay que tener en cuenta al implementar un SPA desarrollado en AEM.
seo-description: En este artículo se presentan importantes cuestiones que hay que tener en cuenta a la hora de contratar a un desarrollador front-end para que desarrolle un SPA para AEM, así como una descripción general de la arquitectura de AEM con respecto a los SPA que hay que tener en cuenta al implementar un SPA desarrollado en AEM.
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# Desarrollo de SPA para AEM{#developing-spas-for-aem}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios del sitio web. Los desarrolladores quieren poder crear sitios con marcos de SPA y los autores quieren editar contenido dentro de AEM sin problemas para un sitio creado con dichos marcos.

En este artículo se presentan importantes cuestiones que hay que tener en cuenta al contratar a un desarrollador front-end para que desarrolle un SPA para AEM y se ofrece una visión general de la arquitectura de AEM con respecto a la implementación de SPA en AEM.

>[!NOTE]
>
>El Editor de SPA es la solución recomendada para proyectos que requieren procesamiento del cliente basado en el marco de SPA (por ejemplo, React o Angular).

## Principios de desarrollo de SPA para AEM {#spa-development-principles-for-aem}

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador front-end observa las optimizaciones estándar al crear un SPA. Si, como desarrollador front-end, sigue estas prácticas recomendadas generales, así como algunos principios específicos de AEM, su SPA funcionará con [AEM y sus funciones](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa)de creación de contenido.

* **[Portabilidad](/help/sites-developing/spa-architecture.md#portability)-**Como con cualquier componente, los componentes se deben crear para que sean lo más portátiles posible. El SPA debe construirse con componentes transferibles y reutilizables.
* **[AEM impulsa la estructura](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)**del sitio: el desarrollador front-end crea componentes y posee su estructura interna, pero depende de AEM para definir la estructura de contenido del sitio.
* **[Procesamiento](/help/sites-developing/spa-architecture.md#dynamic-rendering)**dinámico: todo el procesamiento debe ser dinámico.
* **[Enrutamiento](#dynamic-routing)dinámico:**el SPA es responsable del enrutamiento y AEM lo escucha y obtiene basándose en él. Cualquier enrutamiento también debe ser dinámico.

Si tiene en cuenta estos principios a medida que desarrolla su SPA, será lo más flexible y seguro posible en el futuro, al tiempo que se habilitará toda la funcionalidad de creación de AEM admitida.

Si no necesita admitir funciones de creación de AEM, puede que tenga que considerar un modelo [de diseño de](/help/sites-developing/spa-architecture.md#spa-design-models)SPA diferente.

### Portabilidad {#portability}

Al igual que al desarrollar cualquier componente, los componentes deben diseñarse de manera que se maximice su portabilidad. Cualquier patrón que funcione en contra de la portabilidad o reutilización de los componentes debe evitarse para garantizar la compatibilidad, la flexibilidad y la sostenibilidad a partir de ahora.

El SPA resultante debe construirse con componentes muy portátiles y reutilizables.

### AEM impulsa la estructura del sitio {#aem-drives-site-structure}

El desarrollador de front-end debe considerarse responsable de crear una biblioteca de componentes de SPA que se utilizan para crear la aplicación. El desarrollador front-end tiene control total de la estructura interna de los componentes. [Sin embargo, AEM siempre es propietario de la estructura del sitio.](/help/sites-developing/spa-overview.md)

Esto significa que el desarrollador front-end puede añadir contenido de cliente antes o después del punto de entrada de los componentes y también puede realizar llamadas de terceros dentro del componente. Sin embargo, el desarrollador de front-end no tiene el control absoluto de cómo se anidan los componentes, por ejemplo.

### Procesamiento dinámico {#dynamic-rendering}

El SPA solo debe basarse en la representación dinámica del contenido. Esta es la expectativa predeterminada de que AEM recupere y procese todos los elementos secundarios de la estructura de contenido. [](/help/sites-developing/spa-architecture.md#portability)

Cualquier representación explícita que apunte a contenido específico se considera representación estática y, aunque compatible, no será compatible con las funciones de creación de contenido de AEM. Esto también va en contra del principio de [portabilidad](/help/sites-developing/spa-architecture.md#portability).

### Enrutamiento dinámico {#dynamic-routing}

Al igual que en el procesamiento, todas las rutas también deben ser dinámicas. En AEM, [el SPA siempre debe ser propietario de la ruta](/help/sites-developing/spa-routing.md) y AEM la escucha y captura contenido basado en ella.

Cualquier enrutamiento estático va en contra del [principio de portabilidad](/help/sites-developing/spa-architecture.md#portability) y limita al autor al no ser compatible con las funciones de creación de contenido de AEM. Por ejemplo, con el enrutamiento estático, si el autor del contenido desea cambiar una ruta o cambiar una página, deberá pedir al desarrollador del front-end que lo haga.

## Kit de arranque de Maven Archetype para SPA {#maven-archetype-for-spa-starter-kit}

Adobe recomienda aprovechar el [Arquetipo de Maven para SPA Starter Kit](https://github.com/adobe/aem-spa-project-archetype) para ayudarle a iniciar su propio proyecto de SPA para AEM.

## Modelos de diseño de SPA {#spa-design-models}

Si se siguen [los principios de desarrollo de SPA en AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem) , el SPA funcionará con todas las funciones de creación de contenido de AEM admitidas. [](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

Sin embargo, puede haber casos en los que esto no es totalmente necesario. La siguiente tabla ofrece una visión general de los distintos modelos de diseño, sus ventajas y sus desventajas.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de diseño<br /> </strong></th>
   <th><strong>Ventajas</strong></th>
   <th><strong>Desventajas</strong></th>
  </tr>
  <tr>
   <td>AEM se utiliza como un CMS sin encabezado sin utilizar el marco del SDK del Editor de <a href="/help/sites-developing/spa-reference-materials.md">SPA.</a></td>
   <td>El desarrollador front-end tiene control total sobre la aplicación.</td>
   <td><p>Los autores de contenido no pueden aprovechar la experiencia de creación de contenido de AEM.</p> <p>El código no es portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables mediante el JCR.</p> </td>
  </tr>
  <tr>
   <td>El desarrollador front-end utiliza el marco SDK del Editor de SPA, pero solo abre algunas áreas para el autor del contenido.</td>
   <td>El desarrollador mantiene el control sobre la aplicación al habilitar únicamente la creación en áreas restringidas de la aplicación.</td>
   <td><p>Los autores de contenido están restringidos a un conjunto limitado de experiencias de creación de contenido de AEM.</p> <p>El código no puede ser portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables mediante el JCR.</p> </td>
  </tr>
  <tr>
   <td>El proyecto aprovecha completamente el SDK del Editor de SPA y los componentes principales se desarrollan como una biblioteca y la estructura de contenido de la aplicación se delega a AEM.</td>
   <td><p>La aplicación es reutilizable y portátil.</p> <p>El autor del contenido puede editar la aplicación con la experiencia de creación de contenido de AEM.<br /> </p> <p>El SPA es compatible con el editor de plantillas.</p> </td>
   <td><p>El desarrollador no controla la estructura de la aplicación ni la parte del contenido delegada a AEM.</p> <p>El desarrollador aún puede reservar áreas de la aplicación para el contenido que no está pensado para crearse con AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Aunque todos los modelos son compatibles con AEM, solo implementando el tercero (y siguiendo así los principios de desarrollo de [SPA recomendados en AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)) los autores de contenido podrán interactuar con el contenido de SPA y editarlo en AEM tal como están acostumbrados.
>[](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

## Migración de SPA existentes a AEM {#migrating-existing-spas-to-aem}

Normalmente, si su SPA sigue los principios de desarrollo de [SPA para AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem), su SPA funcionará en AEM y se podrá editar con el editor de AEM SPA.

Siga estos pasos para que el SPA existente esté listo para trabajar con AEM.

1. **Haga que los componentes de JS sean modulares.**

   Hacerlos capaces de procesarse en cualquier orden, posición y tamaño.
1. **Utilice los contenedores proporcionados por nuestro SDK para colocar sus componentes en la pantalla.**

   AEM proporciona un componente de sistema de páginas y párrafos para que pueda utilizarlo.
1. **Cree un componente de AEM para cada componente de JS.**

   Los componentes de AEM definen el cuadro de diálogo y la salida JSON.

## Instrucciones para desarrolladores de front-end {#instructions-for-front-end-developers}

La tarea principal de conseguir que un desarrollador front-end cree un SPA para AEM es acordar los componentes y sus modelos JSON.

A continuación se describen los pasos que debe seguir un desarrollador front-end al desarrollar un SPA para AEM.

1. **Aceptar los componentes y su modelo JSON**

   Los desarrolladores front-end y los desarrolladores de AEM back-end deben ponerse de acuerdo sobre qué componentes son necesarios y un modelo para que exista una coincidencia individual entre los componentes de SPA y los componentes back-end.

   Los componentes de AEM siguen siendo necesarios principalmente para proporcionar cuadros de diálogo de edición y para exportar el modelo de componentes.

1. **En componentes React, acceda al modelo mediante`this.props.cqModel`**

   Una vez que se han acordado los componentes y se ha implantado el modelo JSON, el desarrollador front-end puede desarrollar el SPA y simplemente acceder al modelo JSON a través de `this.props.cqModel`.

1. **Implementar el método`render()`del componente**

   El desarrollador de front-end implementa el `render()` método según lo considere necesario y puede utilizar los campos de la `cqModel` propiedad. Esto genera los fragmentos DOM y HTML que se insertarán en la página. Esta es la forma estándar de crear una aplicación en React.

1. **Asigne el componente al tipo de recurso de AEM mediante`MapTo()`**

   La asignación almacena clases de componente y el componente proporcionado la utiliza internamente para recuperar y crear instancias dinámicas de componentes en función del tipo de recurso determinado. `Container`

   Esto sirve como &quot;pegamento&quot; entre el front-end y el back-end, de modo que el editor sabe a qué componentes de reacción corresponden.

   Los `Page` y `ResponsiveGrid` son buenos ejemplos de clases que extienden la base `Container`.

1. **Defina el parámetro del componente`EditConfig`como`MapTo()`**

   Este parámetro es necesario para indicar al editor cómo se debe nombrar el componente mientras no se procese o no tenga contenido para procesar.

1. **Extender la`Container`clase proporcionada para páginas y contenedores**

   Los sistemas de páginas y párrafos deben ampliar esta clase para que la delegación a los componentes internos funcione según lo previsto.

1. **Implemente una solución de enrutamiento que utilice la API de HTML5`History`.**

   Cuando `ModelRouter` está activado, la llamada a las funciones `pushState` y `replaceState` activará una solicitud al `PageModelManager` para recuperar un fragmento que falta del modelo.

   La versión actual del modelo `ModelRouter` solo admite el uso de direcciones URL que apunten a la ruta de recursos real de los puntos de entrada del modelo de Sling. No admite el uso de direcciones URL personales o alias.

   El `ModelRouter` se puede deshabilitar o configurar para ignorar una lista de expresiones regulares.

## AEM-Agnostic {#aem-agnostic}

Estos bloques de código ilustran cómo los componentes React y Angular no necesitan nada específico de Adobe o AEM.

* Todo lo que se encuentra dentro del componente JavaScript no depende de AEM.
* Sin embargo, lo específico de AEM es que el componente JS debe asignarse a un componente AEM con el asistente MapTo.

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

El `MapTo` ayudante es el &quot;pegamento&quot; que permite que los componentes del back-end y del front-end se comparen entre sí:

* Indica al contenedor JS (o sistema de párrafos JS) qué componente JS es responsable de procesar cada uno de los componentes presentes en el JSON.
* Agrega un atributo de datos HTML al HTML que representa el componente JS, de modo que el Editor de SPA sepa qué cuadro de diálogo mostrar al autor al editar el componente.

Para obtener más información sobre el uso `MapTo` y la creación de SPA para AEM en general, consulte la Guía de introducción para el marco seleccionado.

* [Introducción a los SPA en AEM: reaccionar](/help/sites-developing/spa-getting-started-react.md)
* [Introducción a los SPA en AEM: Angular](/help/sites-developing/spa-getting-started-angular.md)

## Arquitectura de AEM y SPA {#aem-architecture-and-spas}

La arquitectura general de AEM, incluidos los entornos de desarrollo, creación y publicación, no cambia al utilizar SPA. Sin embargo, es útil comprender cómo encaja el desarrollo de SPA en esta arquitectura.

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **Entorno de compilación**

   Aquí es donde el origen de la aplicación SPA y el origen de componentes están desprotegidos.

   * El generador clientlib de NPM crea una biblioteca de cliente del proyecto SPA.
   * Maven se encargará de la utilización de esa biblioteca y la implementará el complemento Maven Build junto con el componente en AEM Author.

* **AEM Author**

   El contenido se crea en el autor de AEM, incluida la creación de SPA.

   Cuando se edita un SPA con el Editor de SPA en el entorno de creación:

   1. El SPA solicita el HTML externo.
   1. Se carga la CSS.
   1. Se carga el Javascript de la aplicación SPA.
   1. Cuando se ejecuta la aplicación SPA, se solicita el JSON, lo que permite a la aplicación crear el DOM de la página, incluidos los `cq-data` atributos.
   1. Estos `cq-data` atributos permiten al editor cargar información de página adicional para saber qué configuraciones de edición están disponibles para los componentes.

* **AEM Publish**

   Aquí es donde el contenido creado y las bibliotecas compiladas, incluidos los artefactos de la aplicación SPA, clientlibs y componentes, se publican para consumo público.

* **Dispatcher/CDN**

   El despachante sirve como capa de almacenamiento en caché de AEM para los visitantes del sitio.

   * Las solicitudes se procesan de forma similar a como se encuentran en AEM Author; sin embargo, no hay ninguna solicitud de la información de la página, ya que solo lo necesita el editor.
   * Javascript, CSS, JSON y HTML se almacenan en caché, lo que optimiza la página para una entrega rápida.

>[!NOTE]
>
>Dentro de AEM no hay necesidad de ejecutar los mecanismos de compilación de Javascript ni de ejecutar el propio Javascript. AEM solo aloja los artefactos compilados desde la aplicación SPA.

## Próximos pasos {#next-steps}

Para obtener información general sobre cómo se estructura un SPA sencillo en AEM y cómo funciona, consulte la guía de introducción para [React](/help/sites-developing/spa-getting-started-react.md) y [Angular](/help/sites-developing/spa-getting-started-angular.md).

Para obtener una guía paso a paso sobre la creación de su propio SPA, consulte el tutorial [](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)Introducción al Editor de AEM SPA - Eventos WKND.

Para obtener más información sobre la asignación de modelos dinámicos a componentes y cómo funciona en SPA en AEM, consulte el artículo Asignación de modelos [dinámicos a componentes para SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Si desea implementar SPA en AEM para un entorno distinto de React o Angular o simplemente desea profundizar en el funcionamiento del SDK de SPA para AEM, consulte el artículo [SPA Blueprint](/help/sites-developing/spa-blueprint.md) .
