---
title: SPA Desarrollo de la para Adobe Experience Manager
description: SPA Este artículo presenta preguntas importantes que se deben tener en cuenta al contratar a un desarrollador front-end para desarrollar una para Adobe Experience Manager AEM AEM SPA SPA AEM (en inglés) y ofrece una visión general de la arquitectura de los desarrolladores en relación con los aspectos que se deben tener en cuenta a la hora de implementar un desarrollador de soluciones de desarrollo en el entorno de la.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: c1429889-e2ed-4e2f-a45f-33f8a6a52745
source-git-commit: 69346a710708ee659ee97e9fdc193c8ea2658fe6
workflow-type: tm+mt
source-wordcount: '2056'
ht-degree: 4%

---

# Desarrollo de SPA para AEM{#developing-spas-for-aem}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. SPA Los desarrolladores quieren poder crear sitios utilizando marcos de trabajo de la y los autores quieren editar contenido dentro de Adobe Experience Manager AEM (la opción de la) sin problemas para un sitio creado con esos marcos de trabajo.

SPA AEM AEM SPA AEM Este artículo presenta preguntas importantes que se deben tener en cuenta al contratar a un desarrollador front-end para desarrollar una aplicación para la y ofrece una descripción general de la arquitectura de las soluciones de implementación de la aplicación de la aplicación de la forma de la implementación de la aplicación de la aplicación de la aplicación de la forma de un desarrollador de front-end en la implementación de la implementación de la aplicación de la en la.

>[!NOTE]
>
>SPA SPA El Editor de es la solución recomendada para proyectos que requieren un procesamiento basado en el marco de trabajo del lado del cliente (por ejemplo, React o Angular).

## SPA AEM Principios de desarrollo de la {#spa-development-principles-for-aem}

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador front-end sigue las prácticas recomendadas estándar al crear una SPA. AEM SPA Si, como desarrollador front-end, sigue estas prácticas recomendadas generales y algunos principios específicos de la interfaz de usuario de la aplicación, el administrador de la aplicación de la aplicación de la interfaz de usuario de su cuenta de usuario de la aplicación de, el administrador de la aplicación de la aplicación de la configuración de usuario de la aplicación estará funcionando con la siguiente: [AEM y sus capacidades de creación de contenido](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa).

* **[Portabilidad](/help/sites-developing/spa-architecture.md#portability) -** Al igual que con cualquier otro componente, los componentes deben crearse para que sean lo más portátiles posible. La SPA debe crearse con componentes transferibles y reutilizables.
* **[AEM Estructura del sitio de](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)** AEM : el desarrollador front-end crea componentes y es propietario de su estructura interna, pero depende de la definición de la estructura de contenido del sitio en la que se basa para definir el contenido.
* **[Procesamiento dinámico](/help/sites-developing/spa-architecture.md#dynamic-rendering)**: todo el procesamiento debe ser dinámico.
* **[Enrutamiento dinámico](#dynamic-routing) -** SPA AEM El usuario es responsable del enrutamiento, lo escucha y lo recupera en función de lo que se haya hecho en la base de datos de, y el usuario es responsable de la. Cualquier enrutamiento también debe ser dinámico.

SPA AEM Si tiene en cuenta estos principios a medida que desarrolle su, será lo más flexible y tendrá la mayor garantía de futuro posible, al tiempo que se habilitan todas las funcionalidades de creación de contenido compatibles.

AEM Si no necesita admitir características de creación de la, es posible que tenga que considerar una opción diferente [SPA modelo de diseño de](/help/sites-developing/spa-architecture.md#spa-design-models).

### Portabilidad {#portability}

Al igual que al desarrollar cualquier componente, los componentes deben diseñarse de tal manera que maximice su portabilidad. Debe evitarse cualquier patrón que vaya en contra de la portabilidad o reutilización de los componentes para garantizar la compatibilidad, flexibilidad y capacidad de mantenimiento en el futuro.

SPA El resultado debe ser construido con componentes altamente portátiles y reutilizables.

### AEM Estructura del sitio de {#aem-drives-site-structure}

SPA El desarrollador front-end debe considerarse a sí mismo como responsable de crear una biblioteca de componentes de que se utilizan para crear la aplicación. El desarrollador front-end tiene un control total de la estructura interna de los componentes. [AEM Sin embargo, en todo momento, es propietario de la estructura del sitio.](/help/sites-developing/spa-overview.md)

Esto significa que el desarrollador front-end puede añadir contenido del cliente antes o después del punto de entrada de los componentes y también puede realizar llamadas de terceros dentro del componente. Sin embargo, el desarrollador front-end no tiene control total sobre cómo se anidan los componentes, por ejemplo.

### Procesamiento dinámico {#dynamic-rendering}

SPA La solo debe depender de la renderización dinámica del contenido. AEM Esta es la expectativa predeterminada en la que la recupera y procesa todos los elementos secundarios de la estructura de contenido.

AEM Cualquier renderización explícita que apunte a contenido específico se considera una renderización estática y, aunque se admite, no es compatible con las funciones de creación de contenido. Esto también va en contra del principio de [portabilidad](/help/sites-developing/spa-architecture.md#portability).

### Enrutamiento dinámico {#dynamic-routing}

Al igual que con el procesamiento, todo el enrutamiento también debe ser dinámico. AEM En el [SPA la ruta siempre debe pertenecer a la dirección](/help/sites-developing/spa-routing.md) AEM y lo escucha, y recupera contenido basado en él.

Cualquier enrutamiento estático funciona con la variable [principio de portabilidad](/help/sites-developing/spa-architecture.md#portability) AEM y limita al autor al no ser compatible con las funciones de creación de contenido de la aplicación de la creación de contenido de la. Por ejemplo, con el enrutamiento estático, si el autor de contenido desea cambiar una ruta o cambiar una página, tendría que pedirle al desarrollador front-end que lo haga.

## Tipo de archivo del proyecto AEM. {#aem-project-archetype}

AEM Cualquier proyecto debe utilizar la variable [AEM Tipo de archivo del proyecto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es)SPA , que es compatible con proyectos de que utilizan React o Angular SPA y utiliza el SDK de.

## SPA Modelos de diseño {#spa-design-models}

Si la variable [SPA AEM Principios de desarrollo de la](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem) SPA AEM son seguidos, entonces sus funcionarán con todas las funciones de creación de contenido de admitidas.

Sin embargo, puede haber casos en los que esto no sea del todo necesario. En la tabla siguiente se ofrece una descripción general de los distintos modelos de diseño, sus ventajas y sus desventajas.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de diseño<br /> </strong></th>
   <th><strong>Ventajas</strong></th>
   <th><strong>Desventajas</strong></th>
  </tr>
  <tr>
   <td>AEM se utiliza como CMS sin encabezado sin usar el <a href="/help/sites-developing/spa-reference-materials.md">SPA Marco del SDK del editor de.</a></td>
   <td>El desarrollador front-end tiene control total sobre la aplicación.</td>
   <td><p>AEM Los autores de contenido no pueden utilizar la experiencia de creación de contenido de.</p> <p>El código no es portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables a través de JCR.</p> </td>
  </tr>
  <tr>
   <td>SPA El desarrollador front-end utiliza el marco de trabajo del SDK del Editor de, pero solo abre algunas áreas al autor del contenido.</td>
   <td>El desarrollador mantiene el control de la aplicación y solo permite la creación en áreas restringidas de la aplicación.</td>
   <td><p>AEM Los autores de contenido están restringidos a un conjunto limitado de experiencias de creación de contenido de la.</p> <p>El código corre el riesgo de no ser ni portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables a través del JCR.</p> </td>
  </tr>
  <tr>
   <td>SPA AEM El proyecto aprovecha completamente el SDK del Editor de, y los componentes de front-end se desarrollan como una biblioteca y la estructura de contenido de la aplicación se delega a los usuarios de la aplicación de forma que puedan acceder a la interfaz de usuario de la aplicación en un solo paso.</td>
   <td><p>La aplicación es reutilizable y portátil.</p> <p>AEM El autor del contenido puede editar la aplicación mediante la experiencia de creación de contenido de la.<br /> </p> <p>SPA La plantilla es compatible con el editor de plantillas de.</p> </td>
   <td><p>AEM El desarrollador no controla la estructura de la aplicación ni la parte de contenido delegada a la que se ha delegado la aplicación en el usuario.</p> <p>AEM El desarrollador puede seguir reservando áreas de la aplicación para el contenido que no vaya a crearse con la ayuda de la herramienta de creación de segmentos de contenido de la aplicación de la aplicación de tipo de.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM Aunque todos los modelos son compatibles con los modelos de, solo mediante la implementación de la tercera (y, por lo tanto, siguiendo el recomendado) [SPA AEM Principios de desarrollo de la en](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)SPA AEM ), los autores de contenido podrán interactuar con el contenido de la página de contenido y editarlo en la forma en la que están acostumbrados a la creación de la página de contenido de la página de la página de la página de la página de inicio de la página de la página de inicio de la página de inicio de la página de inicio.

## SPA AEM Migración de recursos existentes a la {#migrating-existing-spas-to-aem}

SPA Por lo general, si el usuario sigue el procedimiento de [SPA AEM Principios de desarrollo de la](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)SPA AEM AEM SPA , el funcionará en el modo de trabajo y se podrá editar con el Editor de la de trabajo de la aplicación de.

SPA AEM Siga estos pasos para preparar sus existentes para trabajar con ellos.

1. **Haga que los componentes JS sean modulares.**

   Permitir que se representen en cualquier orden, posición y tamaño.
1. **Utilice los contenedores proporcionados por el SDK de Adobe para colocar los componentes en la pantalla.**

   AEM proporciona un componente del sistema de páginas y párrafos para que lo utilice.
1. **AEM Cree un componente de para cada componente JS.**

   AEM Los componentes de definen el cuadro de diálogo y la salida JSON.

## Instrucciones para desarrolladores de front-end {#instructions-for-front-end-developers}

SPA AEM La tarea principal al involucrar a un desarrollador front-end para crear una para la creación de segmentos es acordar sobre los componentes y sus modelos JSON.

SPA AEM A continuación se describen los pasos que debe seguir un desarrollador front-end al desarrollar una para la creación de segmentos de cliente de la interfaz de usuario de la interfaz de usuario de.

1. **Acordar componentes y su modelo JSON**

   AEM SPA Los desarrolladores de front-end y de back-end deben ponerse de acuerdo sobre qué componentes son necesarios y un modelo, de modo que haya una coincidencia individualizada entre los componentes de la interfaz de usuario y los componentes de back-end de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario.

   AEM La mayoría de los componentes todavía son necesarios para proporcionar cuadros de diálogo de edición y para exportar el modelo de componente.

1. **En Componentes de React, acceda al modelo mediante`this.props.cqModel`**

   SPA Una vez acordados los componentes y que el modelo JSON esté listo, el desarrollador front-end es libre de desarrollar el modelo de JSON y puede acceder a él simplemente a través de la interfaz de usuario de JSON. El desarrollador de JSON puede desarrollar el modelo de JSON de una manera sencilla y sencilla. `this.props.cqModel`.

1. **Implementar el del componente `render()` método**

   El desarrollador front-end implementa las `render()` y pueden utilizar los campos de la variable. `cqModel` propiedad. Esto genera el DOM y los fragmentos de HTML que se insertan en la página. Esta es la forma estándar de crear una aplicación en React.

1. **AEM Asigne el componente al tipo de recurso de mediante`MapTo()`**

   La asignación almacena clases de componentes y la utiliza internamente el proporcionado `Container` para recuperar y crear instancias de componentes de forma dinámica en función del tipo de recurso dado.

   Esto sirve como &quot;pegamento&quot; entre el front-end y el back-end para que el editor sepa a qué componentes corresponden los componentes de react.

   El `Page` y `ResponsiveGrid` son buenos ejemplos de clases que amplían la base `Container`.

1. **Defina el del componente `EditConfig` como parámetro a`MapTo()`**

   Este parámetro es necesario para indicar al editor cómo se debe asignar un nombre al componente, siempre que no se haya procesado aún o no tenga contenido para procesar.

1. **Ampliar el proporcionado `Container` clase para páginas y contenedores**

   Los sistemas de páginas y párrafos deben ampliar esta clase para que la delegación a los componentes internos funcione según lo esperado.

1. **Implementar una solución de enrutamiento que use el HTML 5 `History` API.**

   Si la variable `ModelRouter` está habilitado, llamando a la función `pushState` y `replaceState` funciones déclencheur una solicitud a `PageModelManager` para recuperar un fragmento que falta del modelo.

   La versión actual de `ModelRouter` solo admite el uso de direcciones URL que apunten a la ruta de recurso real de los puntos de entrada del modelo Sling. No admite el uso de direcciones URL o alias de vanidad.

   El `ModelRouter` se puede deshabilitar o configurar para que ignore una lista de expresiones regulares.

## AEM agnóstico {#aem-agnostic}

Estos bloques de código ilustran cómo los componentes de React y Angular no necesitan nada que sea específico o de Adobe AEM de la.

* AEM Todo lo que se encuentra dentro del componente JavaScript no es independiente de la aplicación de la aplicación de la aplicación de.
* AEM AEM Sin embargo, lo que es específico de la es que el componente JS debe asignarse a un componente de la aplicación de seguridad de la aplicación de ayuda de MapTo.

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

El `MapTo` Helper es el &quot;pegamento&quot; que permite hacer coincidir los componentes del back-end y del front-end:

* Indica al contenedor de JS (o sistema de párrafos de JS) qué componente de JS es responsable de procesar cada uno de los componentes presentes en el JSON.
* Agrega un atributo de datos de HTML al HTML SPA que procesa el componente JS, de modo que el Editor de datos sepa qué cuadro de diálogo mostrar al autor al editar el componente.

Para obtener más información sobre el uso de `MapTo` SPA AEM y crear una lista de componentes para la creación de informes de manera general, consulte la guía de introducción para obtener información sobre el marco de trabajo seleccionado.

* [SPA AEM Introducción a la administración de la en React](/help/sites-developing/spa-getting-started-react.md)
* [SPA AEM Introducción a la administración de la en Angular](/help/sites-developing/spa-getting-started-angular.md)

## AEM SPA Arquitectura de la y la {#aem-architecture-and-spas}

AEM SPA La arquitectura general de los entornos de desarrollo, creación y publicación, entre otros, no cambia al utilizar la. SPA Sin embargo, es útil comprender cómo encaja el desarrollo de la en esta arquitectura.

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **Entorno de compilación**

  SPA Aquí es donde se extrae el origen del origen de la aplicación y del origen del componente de la aplicación de la.

   * SPA El generador clientlib de NPM crea una biblioteca de cliente a partir del proyecto de.
   * Esa biblioteca la toma Maven y la implementa el complemento de compilación de Maven junto con el componente al autor de AEM.

* **AEM Author**

  AEM SPA El contenido se crea en el autor de la, incluido el autor de la creación

  SPA SPA Cuando se edita una con el Editor de en el entorno de creación:

   1. SPA El HTML externo se lo solicita el.
   1. Se carga el CSS.
   1. SPA Se carga el JavaScript de la aplicación de.
   1. SPA Cuando se ejecuta la aplicación de la, se solicita el JSON, lo que permite a la aplicación crear el DOM de la página, incluido el `cq-data` atributos.
   1. Esta `cq-data` Los atributos de permiten al editor cargar información de página adicional para saber qué configuraciones de edición están disponibles para los componentes.

* **AEM Publish**

  SPA Aquí es donde el contenido creado y las bibliotecas compiladas, incluidos los artefactos de aplicación, clientlibs y componentes, se publican para uso público.

* **Dispatcher/CDN**

  AEM Dispatcher sirve como la capa de almacenamiento en caché de los recursos para los visitantes del sitio.

   * Las solicitudes se procesan de forma similar a como se encuentran en el Autor de AEM, pero no hay ninguna solicitud de información de página porque solo la necesita el editor.
   * JavaScript, CSS, JSON y HTML se almacenan en caché, lo que optimiza la página para una entrega rápida.

>[!NOTE]
>
>AEM Dentro de, no es necesario ejecutar los mecanismos de compilación de JavaScript ni ejecutar el propio JavaScript. AEM SPA solo aloja los artefactos compilados de la aplicación de la.

## Pasos siguientes {#next-steps}

SPA AEM Para obtener una descripción general de cómo se estructura un simple en la y cómo funciona, consulte la guía de introducción para ambos [Reaccionar](/help/sites-developing/spa-getting-started-react.md) y [Angular](/help/sites-developing/spa-getting-started-angular.md).

SPA Para obtener una guía paso a paso sobre cómo crear sus propios, consulte la [AEM SPA Introducción al Editor de eventos de: Tutorial de eventos de WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=es).

SPA AEM Para obtener más información acerca de la asignación de modelos dinámicos a componentes y cómo funciona dentro de la asignación de componentes dentro de la en la aplicación, consulte el artículo [SPA Asignación de modelos dinámicos a componentes para la creación de](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

SPA AEM Si desea implementar la implementación de la en un entorno de trabajo distinto de React o Angular SPA AEM, o simplemente desea profundizar en cómo funciona el SDK de la para la creación de informes, consulte la [SPA Modelo de](/help/sites-developing/spa-blueprint.md) artículo.
