---
title: 'Opcional: creación de aplicaciones de una sola página (SPA) con AEM'
description: En esta continuación opcional del Recorrido para desarrolladores de AEM sin encabezado, aprenderá cómo AEM combina la entrega sin encabezado con las funciones tradicionales de CMS de pila completa y cómo puede crear SPA editables con el marco de trabajo del editor SPA de AEM.
exl-id: 91eadda2-b881-4e4a-867f-8c5c54e8f8b4
source-git-commit: a2ababa9dd9115e963b91a7271d204d287557c40
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 100%

---

# Creación de aplicaciones de una sola página (SPA) con AEM {#create-spa}

En esta continuación opcional del [Recorrido para desarrolladores AEM sin encabezado,](overview.md) aprenderá cómo AEM combina la entrega sin encabezado con funciones tradicionales de CMS de pila completa y cómo puede crear SPA editables con el marco de trabajo del editor de SPA de AEM, así como integrar SPA externas, permitiendo la funcionalidad de edición necesaria.

## La historia hasta ahora {#story-so-far}

En este punto, debería haber completado todo el [Recorrido para desarrolladores de AEM sin encabezado](overview.md) y comprender los conceptos básicos de la entrega de contenido sin encabezado en AEM, incluido lo siguiente:

* La diferencia entre la entrega de contenido sin encabezado y con encabezado.
* Las características sin encabezado de AEM.
* Cómo organizar un proyecto sin encabezado en AEM.
* Cómo crear contenido sin encabezado en AEM.
* Cómo recuperar y actualizar contenido sin encabezado en AEM.
* Cómo poner en marcha un proyecto de AEM sin encabezado.

Así que ahora o bien ha puesto en marcha su primer proyecto de AEM sin encabezado o tiene los conocimientos necesarios para hacerlo. Enhorabuena.

Entonces, ¿por qué está leyendo esta continuación adicional y opcional del recorrido? Es probable que recuerde que en la [Introducción](getting-started.md#integration-levels) hemos examinado brevemente cómo AEM no solo admite entregas sin encabezado y modelos de pila completos tradicionales, sino que también puede admitir modelos híbridos que combinan las ventajas de ambos. Aunque no es el modelo tradicional sin encabezado, estos modelos híbridos pueden ofrecer una flexibilidad sin precedentes a ciertos proyectos.

Este artículo se basa en sus conocimientos de AEM sin encabezado para explorar en profundidad cómo puede crear sus propias aplicaciones de una sola página (SPA) que realmente se pueden editar en AEM. De este modo puede crear contenido y enviarlo sin encabezado a una SPA, pero dicha SPA sigue siendo editable en AEM.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo se desarrollan las aplicaciones de una sola página mediante el marco de trabajo del editor de SPA de AEM. Después de leer este documento, debería poder hacer lo siguiente:

* Comprender la función básica del editor de SPA.
* Conocer los requisitos para crear una SPA totalmente editable para AEM.
* Comprender cómo se pueden integrar las SPA externas en AEM.
* Comprender cómo se debe implementar o no la representación del lado del servidor.

## Condiciones y requisitos previos {#requirements-prerequisites}

Antes de empezar a trabajar con las SPA en AEM hay una serie de requisitos.

### Conocimiento {#knowledge}

* Experiencia en desarrollo creando SPA con marcos de trabajo React o Angular.
* Conocimientos básicos de AEM para crear fragmentos de contenido y utilizar el editor.
* Asegúrese de revisar el documento [Con encabezado y sin encabezado en AEM](/help/sites-developing/headful-headless.md) para comprender los distintos niveles de integración de SPA posibles.

### Herramientas {#tools}

* Acceso a la zona protegida para probar la implementación de su proyecto.
* Instancia de desarrollo local para modelado y prueba de datos.
* SPA externa existente (opcional, según el modelo de integración elegido).
* Tipo de archivo del proyecto AEM.

## ¿Qué es una SPA? {#what-is-a-spa}

Una aplicación de una sola página (SPA) difiere de una página convencional en que se procesa en el lado del cliente y principalmente está dirigida por JavaScript, y se basa en llamadas Ajax para cargar datos y actualizar la página de forma dinámica. La mayoría o todo el contenido se recupera una vez en una carga de una sola página con recursos adicionales cargados asincrónicamente según sea necesario en función de la interacción del usuario con la página.

Esto reduce la necesidad de actualizaciones de la página y presenta al usuario una experiencia que es fluida, rápida y se parece más a una experiencia nativa de la aplicación.

El Editor de SPA de AEM permite a los desarrolladores de front-end crear SPA que se pueden integrar en un sitio AEM, lo que permite a los autores de contenido editar el contenido SPA tan fácilmente como cualquier otro contenido de AEM.

## ¿Por qué una SPA? {#why-spa}

Al ser más rápido, fluido y más parecido a una aplicación nativa, una SPA se convierte en una experiencia muy atractiva no solo para el visitante de la página web, sino también para los especialistas en marketing y desarrolladores debido a la naturaleza de cómo funcionan las SPA.

Para obtener una descripción completa de las SPA y por qué las utilizaría, consulte los [recursos adicionales](#additional-resources) para obtener vínculos a más documentación detallada.

## Cómo AEM gestiona las SPA

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador front-end sigue las prácticas recomendadas estándar al crear una SPA. Si como desarrollador front-end sigue estas prácticas recomendadas generales, así como algunos principios específicos de AEM, su SPA funcionará con AEM y su funcionalidad de creación de contenido.

* **Portabilidad**: al igual que con cualquier componente, los componentes de SPA deben estar creados para ser lo más portátiles posible. La SPA debe crearse con componentes transferibles y reutilizables.
* **AEM impulsa la estructura del sitio**: el desarrollador front-end crea componentes y posee su estructura interna, pero depende de AEM para definir la estructura de contenido del sitio.
* **Procesamiento dinámico**: todo el procesamiento debe ser dinámico.
* **Enrutamiento dinámico**: la SPA es responsable del enrutamiento, y AEM la atiende y recupera en función de esta. Cualquier enrutamiento también debe ser dinámico.

Para obtener una descripción completa de cómo AEM gestiona las SPA, consulte los [recursos adicionales](#additional-resources) para obtener vínculos a más documentación detallada.

## El editor de SPA de AEM {#aem-spa-editor}

Los sitios creados con marcos de trabajo de las SPA comunes, como React y Angular, cargan su contenido a través de JSON dinámico y no proporcionan la estructura de HTML necesaria para que el Editor de páginas de AEM pueda colocar controles de edición.

Para permitir la edición de las SPA dentro de AEM, se necesita una asignación entre la salida JSON de las SPA y el modelo de contenido en el repositorio AEM para guardar los cambios en el contenido.

El soporte de las SPA en AEM introduce una capa delgada de JS que interactúa con el código JS de las SPA cuando se carga en el Editor de páginas con el que se pueden enviar eventos y activar la ubicación de los controles de edición para permitir la edición en contexto. Esta función se basa en el concepto de punto final de la API de Servicios de contenido, ya que el contenido de las SPA debe cargarse a través de los Servicios de contenido.

Para obtener una descripción completa del editor de SPA de AEM, consulte el apartado [recursos adicionales](#additional-resources) para obtener los vínculos a documentación más detallada.

## Adaptación de las SPA existentes {#existing-spas}

Si tiene una SPA existente, AEM permite integrarlo en AEM para que sea visible para los autores de contenido en el editor de AEM. Esto puede resultar muy útil para ver el contenido que crean a través de los fragmentos de contenido en el contexto de la aplicación final en la que se consumirá.

Además, con tan solo unos pequeños cambios, puede habilitar una determinada capacidad de edición en la SPA externa dentro del editor de AEM.

El componente RemotePage permite procesar una SPA externa en AEM.

Para obtener una descripción completa de cómo hacer que una SPA externa se pueda editar en AEM, consulte la sección [recursos adicionales](#additional-resources) para obtener vínculos a documentación más detallada.

## Siguientes pasos {#what-is-next}

Para comenzar a desarrollar su propia SPA para AEM, revise los siguientes documentos:

* [Tutorial WKND de SPA](/help/sites-developing/spa-wknd.md)
* [Introducción a React](/help/sites-developing/spa-getting-started-react.md)
* [Introducción a Angular](/help/sites-developing/spa-getting-started-angular.md)

Si necesita adaptar una SPA existente para utilizarla en AEM, revise los documentos siguientes:

* [El componente RemotePage](/help/sites-developing/spa-remote-page.md)
* [Edición de un SPA externo dentro de AEM](/help/sites-developing/spa-edit-external.md)

Consulte los [recursos adicionales](#additional-resources) para profundizar en los temas de las SPA en AEM.

## Recursos adicionales {#additional-resources}

A continuación se muestran algunos recursos adicionales que profundizan en algunos conceptos mencionados en este documento.

* [Con encabezado y sin encabezado en AEM](/help/sites-developing/headful-headless.md): una descripción de los diferentes modelos de entrega disponibles en AEM.
* [Introducción y tutorial de SPA.](/help/sites-developing/spa-walkthrough.md): una buena introducción a las SPA en AEM
* [Desarrollo de las SPA para AEM](/help/sites-developing/spa-architecture.md): directrices sobre cómo desarrollar las SPA para AEM
* [Información general del editor de SPA](/help/sites-developing/spa-overview.md): detalles del funcionamiento del editor de SPA.
* [Procesamiento en el lado del servidor](/help/sites-developing/spa-ssr.md): cómo configurar la renderización del lado del servidor (SSR) para las SPA de AEM
* [Documentos de referencia de la SPA](/help/sites-developing/spa-reference-materials.md): referencias de la API de JavaScript y vínculos a los proyectos de GitHub de SPA en AEM de código abierto
* [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md): cómo crear fragmentos de contenido
* [Arquetipo del proyecto de AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es): plantilla de Maven que crea un proyecto mínimo, basado en las prácticas recomendadas de Adobe Experience Manager (AEM) como punto de partida para su sitio web
