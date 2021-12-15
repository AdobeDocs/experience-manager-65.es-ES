---
title: 'Opcional: Cómo crear aplicaciones de una sola página (SPA) con AEM'
description: En esta continuación opcional del Recorrido para desarrolladores sin encabezado de AEM, aprenderá cómo AEM combinar la entrega sin encabezado con las funciones tradicionales de CMS de pila completa y cómo puede crear SPA editables con AEM marco de edición de SPA.
exl-id: d74848f2-683e-49e1-9374-32596ca5d7d7
source-git-commit: 7b97bc0ffb0df6641ae71fa36c459f1368052e12
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 0%

---

# Cómo crear aplicaciones de una sola página (SPA) con AEM {#create-spa}

En esta continuación opcional del [AEM Recorrido para desarrolladores sin encabezado,](overview.md) aprenderá cómo AEM combinar envíos sin encabezado con funciones tradicionales de CMS de pila completa y cómo puede crear SPA editables con AEM marco SPA Editor, así como integrar SPA externas, permitiendo las funciones de edición necesarias.

## La historia hasta ahora {#story-so-far}

En este punto, debería haber completado todo el [recorrido para desarrolladores AEM sin encabezado](overview.md) y comprenda los conceptos básicos de la entrega sin encabezado en AEM, incluida la comprensión de:

* La diferencia entre la entrega de contenido sin encabezado y con encabezado.
* AEM características sin periféricos.
* Organizar y AEM proyecto sin encabezado.
* Cómo crear contenido sin encabezado en AEM.
* Cómo recuperar y actualizar contenido sin encabezado en AEM.
* Cómo poner en marcha un proyecto AEM sin encabezado.

Así que ahora ya sea que usted se ha puesto en marcha con su primer proyecto AEM sin cabeza o tiene todo el conocimiento necesario para hacerlo. Felicitaciones!

Entonces, ¿por qué está leyendo esta continuación adicional y opcional del recorrido? Es probable que recuerde eso en la [Introducción](getting-started.md#integration-levels) analizamos brevemente cómo AEM no solo admite entregas sin periféricos y modelos de pila completa tradicionales, sino que también puede admitir modelos híbridos que combinan las ventajas de ambos. Aunque no es el modelo tradicional sin cabeza, estos modelos híbridos pueden ofrecer una flexibilidad sin precedentes a ciertos proyectos.

Este artículo se basa en su conocimiento de AEM sin encabezado al explorar en profundidad cómo puede crear sus propias aplicaciones de una sola página (SPA) que realmente se pueden editar en AEM. De este modo puede crear contenido y enviarlo sin problemas a un SPA, pero ese SPA sigue siendo editable en AEM.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo se desarrollan las aplicaciones de una sola página mediante el marco AEM SPA Editor. Después de leer este documento, debe:

* Comprender la función básica del SPA Editor.
* Conozca los requisitos para crear una SPA totalmente editable para AEM.
* Comprender cómo se pueden integrar los SPA externos en AEM.
* Comprenda cómo se debe implementar o no la representación del lado del servidor.

## Requisitos y requisitos previos {#requirements-prerequisites}

Hay varios requisitos antes de comenzar a trabajar con SPA en AEM.

### Conocimiento {#knowledge}

* Experiencia de desarrollo crear SPA con marcos de React o Angular
* Capacidades básicas AEM crear fragmentos de contenido y utilizar el editor
* Asegúrese de revisar el documento [Encabezado y sin cabeza en AEM](/help/sites-developing/headful-headless.md) para comprender los distintos niveles de integración SPA posibles.

### Herramientas {#tools}

* Acceso a espacio aislado para probar la implementación de su proyecto
* Instancia de desarrollo local para modelado y prueba de datos
* SPA externa existente (opcional, según el modelo de integración elegido)
* Tipo de archivo del proyecto AEM

## ¿Qué es un SPA? {#what-is-a-spa}

Una aplicación de una sola página (SPA) difiere de una página convencional en que se procesa en el lado del cliente y principalmente está dirigida por JavaScript, y se basa en llamadas Ajax para cargar datos y actualizar la página de forma dinámica. La mayoría o todo el contenido se recupera una vez en una única carga de página con recursos adicionales cargados asincrónicamente según sea necesario en función de la interacción del usuario con la página.

Esto reduce la necesidad de actualizar la página y presenta al usuario una experiencia que es fluida, rápida y se parece más a una experiencia nativa de la aplicación.

El AEM SPA Editor permite a los desarrolladores de front-end crear SPA que se pueden integrar en un sitio AEM, lo que permite a los autores de contenido editar el contenido SPA tan fácilmente como cualquier otro contenido AEM.

## ¿Por qué un SPA? {#why-spa}

Al ser más rápido, fluido y más parecido a una aplicación nativa, una SPA se convierte en una experiencia muy atractiva no solo para el visitante de la página web, sino también para los especialistas en marketing y desarrolladores debido a la naturaleza de cómo SPA funciona.

Para obtener una descripción completa de las SPA y por qué las utilizaría, consulte la [recursos adicionales](#additional-resources) para obtener vínculos a más documentación detallada.

## Cómo AEM gestiona SPA

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador del front-end observa las prácticas recomendadas estándar al crear un SPA. Si como desarrollador de front-end sigue estas prácticas recomendadas generales, así como algunos principios específicos de AEM, su SPA funcionará con AEM y sus funciones de creación de contenido.

* **Portabilidad** - Al igual que con cualquier componente, los componentes SPA deben estar construidos para ser lo más portátiles posible. El SPA debe crearse con componentes transferibles y reutilizables.
* **AEM estructura del sitio** : El desarrollador de front-end crea componentes y posee su estructura interna, pero depende de AEM para definir la estructura de contenido del sitio.
* **Renderización dinámica** - Todas las renderizaciones deben ser dinámicas.
* **Enrutamiento dinámico** - El SPA es responsable del enrutamiento y AEM lo escucha y busca según él. Cualquier enrutamiento también debe ser dinámico.

Para obtener una descripción completa de cómo AEM gestiona los SPA, consulte la [recursos adicionales](#additional-resources) para obtener vínculos a más documentación detallada.

## Editor AEM SPA {#aem-spa-editor}

Los sitios creados con marcos de SPA comunes, como React y Angular, cargan su contenido a través de JSON dinámico y no proporcionan la estructura de HTML necesaria para que el Editor de páginas de AEM pueda colocar controles de edición.

Para permitir la edición de SPA dentro de AEM, se necesita una asignación entre la salida JSON del SPA y el modelo de contenido en el repositorio AEM para guardar los cambios en el contenido.

SPA compatibilidad con en AEM introduce una capa de JS fina que interactúa con el código JS de SPA cuando se carga en el Editor de páginas con el que se pueden enviar eventos y se puede activar la ubicación de los controles de edición para permitir la edición en contexto. Esta función se basa en el concepto de extremo de la API de servicios de contenido, ya que el contenido de la SPA debe cargarse a través de los servicios de contenido.

Para obtener una descripción completa del AEM SPA Editor, consulte la [recursos adicionales](#additional-resources) para obtener vínculos a más documentación detallada.

## Adaptación a SPA existentes {#existing-spas}

Si tiene un SPA existente, AEM puede incrustarlo en AEM para que sea visible para los autores de contenido en el editor de AEM. Esto puede resultar muy útil para ver el contenido que están creando mediante fragmentos de contenido en el contexto de la aplicación final en la que se consumirá.

Además, con solo cambios pequeños, puede habilitar cierta capacidad de edición en el SPA externo dentro del editor de AEM.

El componente RemotePage permite procesar una SPA externa en AEM.

Para obtener una descripción completa de cómo hacer editable un SPA externo en AEM, consulte la [recursos adicionales](#additional-resources) para obtener vínculos a más documentación detallada.

## Siguientes pasos {#what-is-next}

Para comenzar a desarrollar su propio SPA para AEM, revise los siguientes documentos:

* [Tutorial de SPA WKND](/help/sites-developing/spa-wknd.md)
* [Introducción a React](/help/sites-developing/spa-getting-started-react.md)
* [Introducción a Angular](/help/sites-developing/spa-getting-started-angular.md)

Si necesita adaptar un SPA existente para utilizarlo en AEM, revise los siguientes documentos:

* [El componente RemotePage](/help/sites-developing/spa-remote-page.md)
* [Edición de un SPA externo dentro de AEM](/help/sites-developing/spa-edit-external.md)

Consulte a continuación la [recursos adicionales](#additional-resources) que puede profundizar en SPA temas de AEM.

## Recursos adicionales {#additional-resources}

A continuación se muestran algunos recursos adicionales que profundizan en algunos conceptos mencionados en este documento.

* [Encabezado y sin cabeza en AEM](/help/sites-developing/headful-headless.md) - Una descripción de los diferentes modelos de envío disponibles en AEM
* [SPA Introducción y Tutorial.](/help/sites-developing/spa-walkthrough.md) - Una buena introducción a la SPA en AEM
* [Desarrollo de SPA para AEM](/help/sites-developing/spa-architecture.md) - Directrices sobre cómo desarrollar SPA para AEM
* [Información general del Editor de SPA](/help/sites-developing/spa-overview.md) - Detalles del funcionamiento del SPA Editor
* [Renderización del servidor](/help/sites-developing/spa-ssr.md) - Cómo configurar SSR para AEM SPA
* [Documentos de referencia SPA](/help/sites-developing/spa-reference-materials.md) : Referencias de la API de JavaScript y vínculos a los proyectos de código abierto AEM SPA proyectos de GitHub
* [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) - Cómo crear fragmentos de contenido
* [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) - Plantilla Maven que crea un proyecto mínimo de Adobe Experience Manager (AEM) basado en las prácticas recomendadas como punto de partida para su sitio web
