---
title: Desarrollo de SPA para AEM
seo-title: Desarrollo de SPA para AEM
description: Este artículo presenta importantes cuestiones que deben tenerse en cuenta al contratar a un desarrollador front-end para que desarrolle un SPA para AEM, así como también ofrece una visión general de la arquitectura de AEM con respecto a SPA que debe tener en cuenta al implementar un SPA desarrollado en AEM.
seo-description: Este artículo presenta importantes cuestiones que deben tenerse en cuenta al contratar a un desarrollador front-end para que desarrolle un SPA para AEM, así como también ofrece una visión general de la arquitectura de AEM con respecto a SPA que debe tener en cuenta al implementar un SPA desarrollado en AEM.
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
translation-type: tm+mt
source-git-commit: 590dc4464182d4baf8293e7bb0774ce92971c0af
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 0%

---


# Desarrollo de SPA para AEM{#developing-spas-for-aem}

Las aplicaciones de una sola página (SPA) pueden oferta de experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios con marcos de SPA y los autores quieren editar contenido dentro de AEM sin problemas para un sitio creado con dichos marcos.

Este artículo presenta importantes cuestiones que deben tenerse en cuenta al contratar a un desarrollador front-end para que desarrolle un SPA para AEM y ofrece una visión general de la arquitectura de AEM con respecto a la implementación de SPA en AEM.

>[!NOTE]
>
>El Editor de SPA es la solución recomendada para proyectos que requieren SPA procesamiento del lado del cliente basado en el marco de trabajo (por ejemplo, React o Angular).

## Principios de desarrollo SPA para AEM {#spa-development-principles-for-aem}

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador front-end observa las optimizaciones estándar al crear un SPA. Si como desarrollador front-end sigue estas optimizaciones generales, así como algunos principios específicos de AEM, su SPA funcionará con [AEM y sus capacidades de creación de contenido](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa).

* **[Portabilidad](/help/sites-developing/spa-architecture.md#portability) -** Como con cualquier componente, los componentes se deben crear para que sean lo más portátiles posible. El SPA debe construirse con componentes transferibles y reutilizables.
* **[AEM impulsa la estructura](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)**  del sitio: el desarrollador front-end crea componentes y posee su estructura interna, pero depende de AEM para definir la estructura de contenido del sitio.
* **[Procesamiento](/help/sites-developing/spa-architecture.md#dynamic-rendering)**  dinámico: todo el procesamiento debe ser dinámico.
* **[Enrutamiento](#dynamic-routing)  dinámico:** El SPA es responsable del enrutamiento y AEM lo escucha y obtiene basándose en él. Cualquier enrutamiento también debería ser dinámico.

Si tiene en cuenta estos principios a medida que desarrolla su SPA, será lo más flexible y la prueba más futura posible, al tiempo que se habilitará toda la funcionalidad AEM creación admitida.

Si no necesita admitir AEM funciones de creación, puede que tenga que considerar un modelo de diseño [SPA diferente](/help/sites-developing/spa-architecture.md#spa-design-models).

### Portabilidad {#portability}

Al igual que al desarrollar cualquier componente, los componentes deben diseñarse de manera que se maximice su portabilidad. Cualquier patrón que funcione en contra de la portabilidad o reutilización de los componentes debe evitarse para garantizar la compatibilidad, la flexibilidad y la sostenibilidad a partir de ahora.

El SPA resultante debe construirse con componentes muy portátiles y reutilizables.

### AEM impulsa la estructura del sitio {#aem-drives-site-structure}

El desarrollador de front-end debe considerarse responsable de crear una biblioteca de componentes de SPA que se utilizan para crear la aplicación. El desarrollador front-end tiene control total de la estructura interna de los componentes. [Sin embargo, AEM en todo momento posee la estructura del sitio.](/help/sites-developing/spa-overview.md)

Esto significa que el desarrollador front-end puede añadir contenido de cliente antes o después del punto de entrada de los componentes y también puede realizar llamadas de terceros dentro del componente. Sin embargo, el desarrollador de front-end no tiene el control absoluto de cómo se anidan los componentes, por ejemplo.

### Procesamiento dinámico {#dynamic-rendering}

El SPA solo debe basarse en la representación dinámica del contenido. Es la expectativa predeterminada en la que AEM captura y procesa todos los elementos secundarios de la estructura de contenido. [](/help/sites-developing/spa-architecture.md#portability)

Cualquier representación explícita que apunte a contenido específico se considera representación estática y aunque se admite, no será compatible con las funciones de creación de contenido de AEM. Esto también va en contra del principio de [portabilidad](/help/sites-developing/spa-architecture.md#portability).

### Enrutamiento dinámico {#dynamic-routing}

Al igual que en el procesamiento, todo el enrutamiento también debe ser dinámico. En AEM, [el SPA siempre debe ser propietario del enrutamiento](/help/sites-developing/spa-routing.md) y AEM lo escucha y obtiene contenido basado en él.

Cualquier enrutamiento estático funciona en contra del [principio de portabilidad](/help/sites-developing/spa-architecture.md#portability) y limita al autor al no ser compatible con las características de creación de contenido de AEM. Por ejemplo, con un enrutamiento estático, si el autor del contenido desea cambiar una ruta o una página, deberá pedir al desarrollador del front-end que lo haga.

## Tipo de archivo del proyecto AEM {#aem-project-archetype}

Cualquier proyecto AEM debe aprovechar el [AEM Arquetipo de proyecto](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype/overview.html), que admite SPA proyectos usando React o Angular y aprovecha el SDK SPA.

## Modelos de diseño de SPA {#spa-design-models}

Si se siguen los [principios de desarrollo de SPA en AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem), el SPA funcionará con todas las funciones AEM creación de contenido admitidas. [](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

Sin embargo, puede haber casos en los que esto no es totalmente necesario. La siguiente tabla ofrece una visión general de los distintos modelos de diseño, sus ventajas y sus desventajas.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de diseño<br /> </strong></th>
   <th><strong>Ventajas</strong></th>
   <th><strong>Desventajas</strong></th>
  </tr>
  <tr>
   <td>AEM se utiliza como un CMS sin encabezado sin utilizar el <a href="/help/sites-developing/spa-reference-materials.md">SPA marco del SDK del Editor.</a></td>
   <td>El desarrollador front-end tiene control total sobre la aplicación.</td>
   <td><p>Los autores de contenido no pueden aprovechar AEM experiencia de creación de contenido.</p> <p>El código no es portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables mediante el JCR.</p> </td>
  </tr>
  <tr>
   <td>El desarrollador front-end utiliza el marco del SDK del Editor de SPA, pero solo abre algunas áreas para el autor del contenido.</td>
   <td>El desarrollador mantiene el control sobre la aplicación al habilitar únicamente la creación en áreas restringidas de la aplicación.</td>
   <td><p>Los autores de contenido están restringidos a un conjunto limitado de experiencias de creación de contenido AEM.</p> <p>El código no puede ser portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables mediante el JCR.</p> </td>
  </tr>
  <tr>
   <td>El proyecto aprovecha completamente el SDK SPA Editor y los componentes principales se desarrollan como una biblioteca y la estructura de contenido de la aplicación se delega en AEM.</td>
   <td><p>La aplicación es reutilizable y portátil.</p> <p>El autor del contenido puede editar la aplicación con AEM experiencia de creación de contenido.<br /> </p> <p>El SPA es compatible con el editor de plantillas.</p> </td>
   <td><p>El desarrollador no controla la estructura de la aplicación ni la parte del contenido delegada a AEM.</p> <p>El desarrollador aún puede reservar áreas de la aplicación para el contenido que no está pensado para ser creado con AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Aunque todos los modelos se admiten en AEM, sólo implementando el tercero (y siguiendo así los [principios de desarrollo de SPA recomendados en AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)) los autores de contenido podrán interactuar con el contenido del SPA y editarlo en AEM tal como están acostumbrados.
>[](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

## Migración de SPA existentes a AEM {#migrating-existing-spas-to-aem}

Generalmente, si su SPA sigue los [Principios de desarrollo de SPA para AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem), su SPA trabajará en AEM y será editable mediante el Editor de SPA de AEM.

Siga estos pasos para preparar el SPA existente para trabajar con AEM.

1. **Haga que los componentes de JS sean modulares.**

   Hacerlos capaces de procesarse en cualquier orden, posición y tamaño.
1. **Utilice los contenedores proporcionados por nuestro SDK para colocar sus componentes en la pantalla.**

   AEM proporciona un componente de sistema de páginas y párrafos para que pueda utilizarlo.
1. **Cree un componente de AEM para cada componente de JS.**

   Los componentes AEM definen el cuadro de diálogo y la salida JSON.

## Instrucciones para desarrolladores de front-end {#instructions-for-front-end-developers}

La principal tarea de lograr que un desarrollador front-end cree un SPA para AEM es acordar los componentes y sus modelos JSON.

A continuación se describen los pasos que debe seguir un desarrollador front-end al desarrollar un SPA para AEM.

1. **Aceptar los componentes y su modelo JSON**

   Los desarrolladores de front-end y los desarrolladores de AEM de back-end deben acordar qué componentes son necesarios y qué modelo, de modo que exista una coincidencia individual entre los componentes de SPA y los componentes de back-end.

   AEM componentes siguen siendo necesarios principalmente para proporcionar cuadros de diálogo de edición y para exportar el modelo de componentes.

1. **En componentes React, acceda al modelo mediante`this.props.cqModel`**

   Una vez que se han acordado los componentes y se ha establecido el modelo JSON, el desarrollador front-end puede desarrollar el SPA y simplemente acceder al modelo JSON mediante `this.props.cqModel`.

1. **Implementar el  `render()` método del componente**

   El desarrollador front-end implementa el método `render()` según lo considere necesario y puede utilizar los campos de la propiedad `cqModel`. Esto genera los fragmentos DOM y HTML que se insertarán en la página. Esta es la forma estándar de crear una aplicación en React.

1. **Asigne el componente al tipo de recurso AEM mediante`MapTo()`**

   La asignación almacena clases de componentes y el componente proporcionado `Container` la utiliza internamente para recuperar y crear instancias dinámicas de componentes en función del tipo de recurso determinado.

   Esto sirve como &quot;pegamento&quot; entre el front-end y el back-end, de modo que el editor sabe a qué componentes de reacción corresponden.

   Los `Page` y `ResponsiveGrid` son buenos ejemplos de clases que amplían la base `Container`.

1. **Defina el parámetro del componente  `EditConfig` como`MapTo()`**

   Este parámetro es necesario para indicar al editor cómo se debe nombrar el componente mientras no se procese o no tenga contenido para procesar.

1. **Ampliar la  `Container` clase proporcionada para páginas y contenedores**

   Los sistemas de páginas y párrafos deben ampliar esta clase para que la delegación a los componentes internos funcione según lo previsto.

1. **Implemente una solución de enrutamiento que utilice la  `History` API de HTML5.**

   Cuando `ModelRouter` está habilitado, llamar a las funciones `pushState` y `replaceState` activará una solicitud a `PageModelManager` para recuperar un fragmento que falta del modelo.

   La versión actual de `ModelRouter` solo admite el uso de direcciones URL que apunten a la ruta de recursos real de los puntos de entrada del Modelo Sling. No admite el uso de direcciones URL personales o alias.

   El `ModelRouter` puede deshabilitarse o configurarse para ignorar una lista de expresiones regulares.

## AEM-agnóstico {#aem-agnostic}

Estos bloques de código ilustran cómo los componentes React y Angular no necesitan nada que sea Adobe o AEM específico.

* Todo lo que se encuentra dentro del componente JavaScript no es AEM.
* Sin embargo, lo que es específico de AEM es que el componente JS debe asignarse a un componente AEM con el asistente MapTo.

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

El asistente `MapTo` es el &quot;pegamento&quot; que permite que los componentes del back-end y del front-end se comparen entre sí:

* Indica al contenedor JS (o sistema de párrafos JS) qué componente JS es responsable de procesar cada uno de los componentes presentes en el JSON.
* Agrega un atributo de datos HTML al HTML que representa el componente JS, de modo que el Editor de SPA sepa qué cuadro de diálogo mostrar al autor al editar el componente.

Para obtener más información sobre el uso de `MapTo` y la creación de SPA para AEM en general, consulte la Guía de introducción de su estructura seleccionada.

* [Introducción a la SPA en AEM: reaccionar](/help/sites-developing/spa-getting-started-react.md)
* [Introducción a SPA en AEM: Angular](/help/sites-developing/spa-getting-started-angular.md)

## Arquitectura AEM y SPA {#aem-architecture-and-spas}

La arquitectura general de AEM, incluidos los entornos de desarrollo, creación y publicación, no cambia al utilizar SPA. Sin embargo, es útil comprender cómo SPA desarrollo encaja en esta arquitectura.

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **Generar Entorno**

   Aquí es donde se extrae el origen de la aplicación SPA y el origen del componente.

   * El generador clientlib de NPM crea una biblioteca de cliente del proyecto SPA.
   * Maven se encargará de la utilización de esa biblioteca y la implementará el complemento Maven Build junto con el componente en AEM Author.

* **AEM Author**

   El contenido se crea en el autor AEM, incluido el SPA de creación.

   Cuando se edita un SPA con el Editor de SPA en el entorno de creación:

   1. El SPA solicita el HTML externo.
   1. Se carga la CSS.
   1. Se carga el Javascript de la aplicación SPA.
   1. Cuando se ejecuta la aplicación de SPA, se solicita el JSON, lo que permite que la aplicación genere el DOM de la página, incluidos los atributos `cq-data`.
   1. Estos atributos `cq-data` permiten al editor cargar información de página adicional para que sepa qué configuraciones de edición están disponibles para los componentes.

* **AEM Publish**

   Aquí es donde el contenido creado y las bibliotecas compiladas, incluidos SPA artefactos de aplicación, clientlibs y componentes, se publican para consumo público.

* **Dispatcher/CDN**

   El despachante sirve como capa de almacenamiento en caché de AEM para visitantes al sitio.

   * Las solicitudes se procesan de forma similar a como se encuentran en AEM Author; sin embargo, no hay ninguna solicitud de la información de la página, ya que solo lo necesita el editor.
   * Javascript, CSS, JSON y HTML se almacenan en caché, lo que optimiza la página para un envío rápido.

>[!NOTE]
>
>Dentro de AEM no hay necesidad de ejecutar los mecanismos de compilación de Javascript ni de ejecutar el propio Javascript. AEM solo aloja los artefactos compilados de la aplicación SPA.

## Próximos pasos {#next-steps}

Para obtener información general sobre cómo se estructura un SPA simple en AEM y cómo funciona, consulte la guía de introducción para [React](/help/sites-developing/spa-getting-started-react.md) y [Angular](/help/sites-developing/spa-getting-started-angular.md).

Para obtener una guía paso a paso sobre cómo crear su propia SPA, consulte el tutorial [Introducción al Editor de AEM SPA - Eventos WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

Para obtener más información sobre la asignación de modelo dinámico a componente y cómo funciona en SPA en AEM, consulte el artículo [Asignación de modelo dinámico a componente para SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Si desea implementar SPA en AEM para un marco que no sea React o Angular o simplemente desea profundizar en el funcionamiento del SDK de SPA para AEM, consulte el artículo [SPA Blueprint](/help/sites-developing/spa-blueprint.md).
