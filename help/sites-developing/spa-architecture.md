---
title: Desarrollo de SPA para AEM
seo-title: Desarrollo de SPA para AEM
description: Este artículo presenta preguntas importantes que se deben tener en cuenta al contratar a un desarrollador de front-end para que desarrolle un SPA para AEM, así como una visión general de la arquitectura de AEM con respecto a SPA tener en cuenta al implementar un SPA desarrollado en AEM.
seo-description: Este artículo presenta preguntas importantes que se deben tener en cuenta al contratar a un desarrollador de front-end para que desarrolle un SPA para AEM, así como una visión general de la arquitectura de AEM con respecto a SPA tener en cuenta al implementar un SPA desarrollado en AEM.
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
exl-id: c1429889-e2ed-4e2f-a45f-33f8a6a52745
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 1%

---

# Desarrollo de SPA para AEM{#developing-spas-for-aem}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios mediante marcos de SPA y los autores quieren editar contenido sin problemas dentro de AEM para un sitio creado con dichos marcos.

Este artículo presenta preguntas importantes que se deben tener en cuenta al contratar a un desarrollador de front-end para que desarrolle un SPA para AEM y ofrece una visión general de la arquitectura de AEM con respecto a la implementación de SPA en AEM.

>[!NOTE]
>
>El Editor de SPA es la solución recomendada para proyectos que requieren SPA procesamiento del lado del cliente basado en el marco de trabajo (por ejemplo, React o Angular).

## Principios de desarrollo SPA para AEM {#spa-development-principles-for-aem}

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador del front-end observa las prácticas recomendadas estándar al crear un SPA. Si como desarrollador de front-end sigue estas prácticas recomendadas generales, así como algunos principios específicos de AEM, su SPA funcionará con [AEM y sus capacidades de creación de contenido](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa).

* **[Portabilidad](/help/sites-developing/spa-architecture.md#portability) :** Al igual que con cualquier componente, los componentes deben crearse para que sean lo más portátiles posible. El SPA debe crearse con componentes transferibles y reutilizables.
* **[AEM estructura del sitio](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)** : el desarrollador de front-end crea componentes y posee su estructura interna, pero depende de la AEM para definir la estructura de contenido del sitio.
* **[Renderización dinámica](/help/sites-developing/spa-architecture.md#dynamic-rendering)** : todas las renderizaciones deben ser dinámicas.
* **[Enrutamiento dinámico](#dynamic-routing) :** el SPA es responsable del enrutamiento y AEM lo escucha y obtiene según él. Cualquier enrutamiento también debe ser dinámico.

Si tiene en cuenta estos principios al desarrollar su SPA, será lo más flexible y la prueba más futura posible, al mismo tiempo que habilita todas las funciones de creación AEM compatibles.

Si no necesita admitir AEM funciones de creación, puede que tenga que considerar un [SPA modelo de diseño](/help/sites-developing/spa-architecture.md#spa-design-models) diferente.

### Portabilidad {#portability}

Al igual que cuando se desarrolla cualquier componente, los componentes deben diseñarse de manera que se maximice su portabilidad. Cualquier patrón que funcione en contra de la portabilidad o reutilización de los componentes debe evitarse para garantizar la compatibilidad, flexibilidad y mantenimiento en el futuro.

El SPA resultante debe crearse con componentes altamente portátiles y reutilizables.

### AEM estructura del sitio {#aem-drives-site-structure}

El desarrollador principal debe considerarse a sí mismo como responsable de crear una biblioteca de componentes de SPA que se utilizan para crear la aplicación. El desarrollador de front-end tiene control total de la estructura interna de los componentes. [Sin embargo, AEM en todo momento posee la estructura del sitio.](/help/sites-developing/spa-overview.md)

Esto significa que el desarrollador del front-end puede añadir contenido del cliente antes o después del punto de entrada de los componentes y también puede realizar llamadas de terceros dentro del componente. Sin embargo, el desarrollador de front-end no tiene control absoluto sobre cómo se anidan los componentes, por ejemplo.

### Renderización dinámica {#dynamic-rendering}

El SPA solo debe depender de la representación dinámica del contenido. Esta es la expectativa predeterminada en la que AEM recupera y procesa todos los elementos secundarios de la estructura de contenido.

Cualquier renderización explícita que señale a contenido específico se considera una renderización estática y aunque compatible, no será compatible con AEM funciones de creación de contenido. Esto también va en contra del principio de [portabilidad](/help/sites-developing/spa-architecture.md#portability).

### Enrutamiento dinámico {#dynamic-routing}

Al igual que con la renderización, todo el enrutamiento también debe ser dinámico. En AEM, [el SPA siempre debe ser propietario del enrutamiento](/help/sites-developing/spa-routing.md) y AEM lo escucha y busca contenido basado en él.

Cualquier enrutamiento estático funciona en contra del [principio de portabilidad](/help/sites-developing/spa-architecture.md#portability) y limita al autor al no ser compatible con las funciones de creación de contenido de AEM. Por ejemplo, con el enrutamiento estático, si el autor de contenido desea cambiar una ruta o cambiar una página, tendría que pedirle al desarrollador del front-end que lo hiciera.

## Tipo de archivo del proyecto AEM {#aem-project-archetype}

Cualquier proyecto AEM debe aprovechar el [AEM tipo de archivo del proyecto](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype/overview.html), que admite SPA proyectos con React o Angular y aprovecha el SDK de SPA.

## SPA modelos de diseño {#spa-design-models}

Si se siguen los [principios de desarrollo de SPA en AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem) , el SPA funcionará con todas las funciones AEM creación de contenido admitidas.

Sin embargo, puede haber casos en que esto no sea completamente necesario. La siguiente tabla ofrece una descripción general de los distintos modelos de diseño, sus ventajas y sus desventajas.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de diseño<br /> </strong></th>
   <th><strong>Ventajas</strong></th>
   <th><strong>Desventajas</strong></th>
  </tr>
  <tr>
   <td>AEM se utiliza como un CMS sin encabezado sin utilizar el <a href="/help/sites-developing/spa-reference-materials.md">SPA marco del SDK del Editor.</a></td>
   <td>El desarrollador del front-end tiene control total sobre la aplicación.</td>
   <td><p>Los autores de contenido no pueden aprovechar AEM experiencia de creación de contenido.</p> <p>El código no es portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador del front-end debe mantener plantillas editables a través de JCR.</p> </td>
  </tr>
  <tr>
   <td>El desarrollador de front-end utiliza el marco del SDK del Editor de SPA, pero solo abre algunas áreas al autor del contenido.</td>
   <td>El desarrollador mantiene el control sobre la aplicación habilitando la creación solo en áreas restringidas de la aplicación.</td>
   <td><p>Los autores de contenido están restringidos a un conjunto limitado de AEM experiencia de creación de contenido.</p> <p>El código corre el riesgo de no ser portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador del front-end debe mantener plantillas editables a través de JCR.</p> </td>
  </tr>
  <tr>
   <td>El proyecto aprovecha completamente el SDK del Editor de SPA y los componentes de front-end se desarrollan como una biblioteca y la estructura de contenido de la aplicación se delega en AEM.</td>
   <td><p>La aplicación es reutilizable y portátil.</p> <p>El autor del contenido puede editar la aplicación mediante AEM experiencia de creación de contenido.<br /> </p> <p>El SPA es compatible con el editor de plantillas.</p> </td>
   <td><p>El desarrollador no controla la estructura de la aplicación ni la parte del contenido delegada a AEM.</p> <p>El desarrollador aún puede reservar áreas de la aplicación para el contenido que no está pensado para su creación mediante AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Aunque todos los modelos se admiten en AEM, solo implementando el tercero (y siguiendo así los [SPA principios de desarrollo recomendados en AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)) los autores de contenido podrán interactuar con el contenido del SPA y editarlo en AEM a medida que estén acostumbrados.

## Migración de SPA existentes a AEM {#migrating-existing-spas-to-aem}

Por lo general, si la SPA sigue los [SPA Principios de desarrollo para AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem), la SPA funcionará en AEM y se podrá editar con el AEM Editor de SPA.

Siga estos pasos para preparar su SPA existente para trabajar con AEM.

1. **Haga que los componentes de JS sean modulares.**

   Permiten procesarlos en cualquier orden, posición y tamaño.
1. **Utilice los contenedores proporcionados por nuestro SDK para colocar sus componentes en la pantalla .**

   AEM proporciona un componente de sistema de páginas y párrafos para que lo utilice.
1. **Cree un componente AEM para cada componente JS.**

   Los componentes AEM definen el cuadro de diálogo y la salida JSON.

## Instrucciones para desarrolladores de front-end {#instructions-for-front-end-developers}

La tarea principal de hacer que un desarrollador front-end cree un SPA para AEM es acordar los componentes y sus modelos JSON.

A continuación se describen los pasos que debe seguir un desarrollador de front-end al desarrollar un SPA para AEM.

1. **Aceptar componentes y su modelo JSON**

   Los desarrolladores de front-end y los desarrolladores de AEM de back-end deben ponerse de acuerdo sobre qué componentes son necesarios y un modelo, de modo que exista una coincidencia individual entre los componentes de SPA y los componentes del back-end.

   AEM componentes siguen siendo necesarios principalmente para proporcionar cuadros de diálogo de edición y exportar el modelo de componentes.

1. **En Componentes de React, acceda al modelo a través de`this.props.cqModel`**

   Una vez que los componentes están acordados y el modelo JSON está en su lugar, el desarrollador front-end puede desarrollar el SPA y simplemente acceder al modelo JSON a través de `this.props.cqModel`.

1. **Implementar el  `render()` método del componente**

   El desarrollador del front-end implementa el método `render()` como considere adecuado y puede utilizar los campos de la propiedad `cqModel` . Esto genera los fragmentos DOM y HTML que se insertan en la página. Esta es la forma estándar de crear una aplicación en React.

1. **Asigne el componente al tipo de recurso AEM mediante`MapTo()`**

   La asignación almacena clases de componentes y la utiliza internamente el componente proporcionado `Container` para recuperar y crear instancias de componentes de forma dinámica en función del tipo de recurso dado.

   Esto sirve como &quot;pegamento&quot; entre el front-end y el back-end para que el editor sepa a qué componentes corresponden los componentes de reacción.

   Los `Page` y `ResponsiveGrid` son buenos ejemplos de clases que amplían la base `Container`.

1. **Defina el parámetro del componente  `EditConfig` como`MapTo()`**

   Este parámetro es necesario para indicar al editor cómo se debe nombrar el componente mientras no se haya procesado aún o no haya contenido para procesar.

1. **Ampliar la  `Container` clase proporcionada para páginas y contenedores**

   Los sistemas de páginas y párrafos deben ampliar esta clase para que la delegación a componentes internos funcione según lo esperado.

1. **Implemente una solución de enrutamiento que utilice la  `History` API de HTML5.**

   Cuando `ModelRouter` está habilitado, la llamada a las funciones `pushState` y `replaceState` envía una solicitud a `PageModelManager` para recuperar un fragmento que falta en el modelo.

   La versión actual de `ModelRouter` solo admite el uso de direcciones URL que apunten a la ruta de recurso real de los puntos de entrada del modelo Sling. No admite el uso de direcciones URL o alias personales.

   El `ModelRouter` se puede deshabilitar o configurar para ignorar una lista de expresiones regulares.

## AEM-agnóstico {#aem-agnostic}

Estos bloques de código ilustran cómo los componentes React y Angular no necesitan nada que sea Adobe o AEM específico.

* Todo lo que se encuentra dentro del componente JavaScript no es AEM.
* Sin embargo, lo que es específico de AEM es que el componente JS debe asignarse a un componente AEM con el asistente de MapTo.

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

El asistente `MapTo` es el &quot;pegamento&quot; que permite que los componentes del back-end y del front-end se comparen entre sí:

* Indica al contenedor de JS (o sistema de párrafos JS) qué componente JS es responsable de procesar cada uno de los componentes presentes en el JSON.
* Añade un atributo de datos HTML al HTML que procesa el componente JS, de modo que el Editor de SPA sepa qué cuadro de diálogo mostrar al autor al editar el componente.

Para obtener más información sobre el uso de `MapTo` y la creación de SPA para AEM en general, consulte la guía de introducción para el marco seleccionado.

* [Introducción a SPA en AEM: React](/help/sites-developing/spa-getting-started-react.md)
* [Introducción a SPA en AEM: Angular](/help/sites-developing/spa-getting-started-angular.md)

## Arquitectura AEM y SPA {#aem-architecture-and-spas}

La arquitectura general de AEM, incluidos los entornos de desarrollo, creación y publicación, no cambia al utilizar SPA. Sin embargo, es útil comprender cómo SPA desarrollo encaja en esta arquitectura.

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **Entorno de compilación**

   Aquí es donde se extrae el origen de la aplicación SPA y el origen de componentes.

   * El generador clientlib de NPM crea una biblioteca de cliente del proyecto SPA.
   * Maven la tomará y la implementará el complemento de compilación de Maven junto con el componente en AEM Author.

* **AEM Author**

   El contenido se crea en el autor AEM, incluido el SPA de creación.

   Cuando se edita una SPA con el Editor de SPA en el entorno de creación:

   1. El SPA solicita el HTML externo.
   1. Se carga el CSS.
   1. Se carga el JavaScript de la aplicación SPA.
   1. Cuando se ejecuta la aplicación SPA, se solicita el JSON, lo que permite que la aplicación cree el DOM de la página, incluidos los atributos `cq-data`.
   1. Estos atributos `cq-data` permiten al editor cargar información de página adicional para que sepa qué configuraciones de edición están disponibles para los componentes.

* **AEM Publish**

   Aquí es donde el contenido creado y las bibliotecas compiladas, incluidos los artefactos de SPA aplicación, clientlibs y componentes, se publican para el consumo público.

* **Dispatcher/CDN**

   Dispatcher sirve como capa de AEM de almacenamiento en caché para los visitantes del sitio.

   * Las solicitudes se procesan de forma similar a como se encuentran en AEM Author; sin embargo, no hay solicitud de la información de la página, ya que el editor solo lo necesita.
   * Javascript, CSS, JSON y HTML se almacenan en caché, lo que optimiza la página para una entrega rápida.

>[!NOTE]
>
>Dentro de AEM no hay necesidad de ejecutar mecanismos de compilación de Javascript ni de ejecutar el propio Javascript. AEM solo aloja los artefactos compilados desde la aplicación SPA.

## Pasos siguientes {#next-steps}

Para obtener información general sobre cómo se estructura un SPA simple en AEM y cómo funciona, consulte la guía de introducción para [React](/help/sites-developing/spa-getting-started-react.md) y [Angular](/help/sites-developing/spa-getting-started-angular.md).

Para obtener una guía paso a paso sobre la creación de su propia SPA, consulte el [Introducción al Editor de SPA de AEM - Tutorial de eventos WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

Para obtener más información sobre el modelo dinámico para la asignación de componentes y cómo funciona dentro de SPA en AEM, consulte el artículo [Asignación de modelos dinámicos a componentes para SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Si desea implementar SPA en AEM para un marco que no sea React o Angular o simplemente desea profundizar en el funcionamiento del SDK de SPA para AEM, consulte el artículo [SPA modelo](/help/sites-developing/spa-blueprint.md) .
