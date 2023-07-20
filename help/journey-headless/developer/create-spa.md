---
title: 'SPA Opcional: cómo crear aplicaciones de una sola página () con Adobe Experience Manager'
description: En esta continuación opcional del Recorrido AEM SPA AEM SPA para desarrolladores de Adobe Experience Manager () sin encabezado, aprenderá a combinar la entrega sin encabezado con las funciones tradicionales de CMS de pila completa y cómo puede crear plantillas editables utilizando el AEM de trabajo de Editor de.
exl-id: 91eadda2-b881-4e4a-867f-8c5c54e8f8b4
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 60%

---

# Creación de aplicaciones de una sola página (SPA) con AEM {#create-spa}

En esta continuación opcional de la [AEM Recorrido de desarrollador sin encabezado,](overview.md) aprenderá cómo Adobe Experience Manager AEM SPA AEM SPA SPA () puede combinar la entrega sin encabezado con las funciones tradicionales de CMS full-stack y cómo puede crear plantillas editables mediante el módulo Editor de e integrar plantillas externas, lo que permite crear funcionalidades de edición según sea necesario.

## La historia hasta ahora {#story-so-far}

En este punto, debería haber completado todo el [Recorrido para desarrolladores de AEM sin encabezado](overview.md) y comprender los conceptos básicos de la entrega de contenido sin encabezado en AEM, incluido lo siguiente:

* La diferencia entre la entrega de contenido sin encabezado y con encabezado.
* Las características sin encabezado de AEM.
* Cómo organizar un proyecto sin encabezado en AEM.
* Cómo crear contenido sin encabezado en AEM.
* Cómo recuperar y actualizar contenido sin encabezado en AEM.
* Cómo poner en marcha un proyecto de AEM sin encabezado.

AEM Por lo tanto, ahora ya está en funcionamiento con su primer proyecto sin encabezado de la red de trabajo o tiene el conocimiento necesario para hacerlo. Enhorabuena.

Entonces, ¿por qué está leyendo esta continuación adicional y opcional del recorrido? Es probable que lo recuerde en el [Primeros pasos](getting-started.md#integration-levels)AEM Sin embargo, hubo una breve discusión sobre cómo no solo admite la entrega sin encabezado y los modelos full-stack tradicionales, sino que también puede admitir modelos híbridos que combinen las ventajas de ambos. Aunque no es el modelo tradicional sin encabezado, estos modelos híbridos pueden ofrecer una flexibilidad sin precedentes a ciertos proyectos.

AEM SPA AEM Este artículo se basa en su conocimiento de las aplicaciones sin encabezado de explorando en profundidad cómo puede crear sus propias aplicaciones de una sola página () que se pueden editar en los entornos de trabajo de la interfaz de usuario de la aplicación de la interfaz de usuario de. SPA SPA AEM De este modo, puede crear contenido y enviarlo sin encabezado a un, pero ese contenido sigue siendo editable en los entornos de trabajo de los que se puede hacer una.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo se desarrollan las aplicaciones de una sola página mediante el marco de trabajo del editor de SPA de AEM. Después de leer este documento, debería poder hacer lo siguiente:

* Comprender la función básica del editor de SPA.
* Conocer los requisitos para crear una SPA totalmente editable para AEM.
* Comprender cómo se pueden integrar las SPA externas en AEM.
* Comprender cómo se debe implementar o no el procesamiento en el lado del servidor.

## Condiciones y requisitos previos {#requirements-prerequisites}

SPA AEM Antes de comenzar a trabajar con los recursos de la, deben cumplirse varios requisitos.

### Conocimiento {#knowledge}

* Experiencia en desarrollo creando SPA con marcos de trabajo React o Angular.
* Conocimientos básicos de AEM para crear fragmentos de contenido y utilizar el editor.
* Asegúrese de revisar el documento [AEM Encabezado y sin encabezado en el](/help/sites-developing/headful-headless.md) SPA para comprender los distintos niveles de integración de la posibles.

### Herramientas {#tools}

* Acceso a la zona protegida para probar la implementación de su proyecto.
* Instancia de desarrollo local para modelado y prueba de datos.
* SPA externa existente (opcional, según el modelo de integración elegido).
* Tipo de archivo del proyecto AEM.

## ¿Qué es una SPA? {#what-is-a-spa}

SPA Una aplicación de una sola página () se diferencia de una página convencional en que se procesa en el lado del cliente y se basa principalmente en JavaScript, y depende de llamadas de Ajax para cargar datos y actualizar la página de forma dinámica. La mayoría o todo el contenido se recupera una vez en una carga de una sola página con recursos adicionales cargados asincrónicamente según sea necesario en función de la interacción del usuario con la página.

Esto reduce la necesidad de actualizaciones de la página y presenta al usuario una experiencia que es fluida, rápida y se parece más a una experiencia nativa de la aplicación.

El Editor de SPA de AEM permite a los desarrolladores de front-end crear SPA que se pueden integrar en un sitio AEM, lo que permite a los autores de contenido editar el contenido SPA tan fácilmente como cualquier otro contenido de AEM.

## ¿Por qué una SPA? {#why-spa}

SPA SPA Al ser más rápido, fluido y más parecido a una aplicación nativa, una aplicación se convierte en una experiencia atractiva no solo para el visitante de la página web, sino también para los especialistas en marketing y desarrolladores debido a la naturaleza de cómo funcionan los.

Para obtener una descripción completa de las SPA y por qué las utilizaría, consulte los [recursos adicionales](#additional-resources) para obtener vínculos a más documentación detallada.

## Cómo AEM gestiona las SPA

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador front-end sigue las prácticas recomendadas estándar al crear una SPA. AEM SPA AEM Como desarrollador front-end, si sigue estas prácticas recomendadas generales y algunos principios específicos de la, su equipo de trabajo funcionará con las capacidades de creación de contenido y de las que se utilizan para la creación de contenido de la interfaz de usuario de.

* **Portabilidad**: al igual que con cualquier componente, los componentes de SPA deben estar creados para ser lo más portátiles posible. La SPA debe crearse con componentes transferibles y reutilizables.
* **AEM Estructura del sitio de** AEM : el desarrollador front-end crea componentes y es propietario de su estructura interna, pero depende de la definición de la estructura de contenido del sitio en la que se basa para definir el contenido.
* **Procesamiento dinámico**: todo el procesamiento debe ser dinámico.
* **Enrutamiento dinámico**: la SPA es responsable del enrutamiento, y AEM la atiende y recupera en función de esta. Cualquier enrutamiento también debe ser dinámico.

Para obtener una descripción completa de cómo AEM gestiona las SPA, consulte los [recursos adicionales](#additional-resources) para obtener vínculos a más documentación detallada.

## El editor de SPA de AEM {#aem-spa-editor}

Los sitios creados con marcos de trabajo de las SPA comunes, como React y Angular, cargan su contenido a través de JSON dinámico y no proporcionan la estructura de HTML necesaria para que el Editor de páginas de AEM pueda colocar controles de edición.

Para permitir la edición de las SPA dentro de AEM, se necesita una asignación entre la salida JSON de las SPA y el modelo de contenido en el repositorio AEM para guardar los cambios en el contenido.

El soporte de las SPA en AEM introduce una capa delgada de JS que interactúa con el código JS de las SPA cuando se carga en el Editor de páginas con el que se pueden enviar eventos y activar la ubicación de los controles de edición para permitir la edición en contexto. SPA Esta función se basa en el concepto de extremo de API de servicios de contenido porque el contenido de la debe cargarse mediante servicios de contenido.

Para obtener una descripción completa del editor de SPA de AEM, consulte el apartado [recursos adicionales](#additional-resources) para obtener los vínculos a documentación más detallada.

## Adaptación de las SPA existentes {#existing-spas}

SPA AEM AEM AEM Si tiene un recurso existente, es compatible con la incrustación en el editor de contenido, por lo que es visible para los autores de contenido en el editor de contenido. En el editor de contenido, el editor de contenido se puede insertar en el editor de contenido, en el que se muestra a los usuarios de manera que no se puede acceder a él Esto puede resultar útil para ver el contenido que están creando a través de fragmentos de contenido en el contexto de la aplicación final en la que se consumirá.

SPA AEM Además, con solo pequeños cambios, puede habilitar cierta capacidad de edición en el editor de externo en el propio editor de contenido.

El componente RemotePage permite procesar una SPA externa en AEM.

Para obtener una descripción completa de cómo hacer que una SPA externa se pueda editar en AEM, consulte la sección [recursos adicionales](#additional-resources) para obtener vínculos a documentación más detallada.

## Siguientes pasos {#what-is-next}

Para comenzar a desarrollar su propia SPA para AEM, revise los siguientes documentos:

* [Tutorial WKND de SPA](/help/sites-developing/spa-wknd.md)
* [Introducción a React](/help/sites-developing/spa-getting-started-react.md)
* [Introducción a Angular](/help/sites-developing/spa-getting-started-angular.md)

SPA AEM Si debe adaptar un documento existente para utilizarlo en la, revise los siguientes documentos:

* [El componente RemotePage](/help/sites-developing/spa-remote-page.md)
* [Edición de un SPA externo dentro de AEM](/help/sites-developing/spa-edit-external.md)

Consulte los [recursos adicionales](#additional-resources) para profundizar en los temas de las SPA en AEM.

## Recursos adicionales {#additional-resources}

A continuación se muestran algunos recursos adicionales que profundizan en algunos conceptos mencionados en este documento.

* [Con encabezado y sin encabezado en AEM](/help/sites-developing/headful-headless.md): una descripción de los diferentes modelos de entrega disponibles en AEM.
* [Introducción y tutorial de SPA.](/help/sites-developing/spa-walkthrough.md): una buena introducción a las SPA en AEM
* [Desarrollo de las SPA para AEM](/help/sites-developing/spa-architecture.md): directrices sobre cómo desarrollar las SPA para AEM
* [Información general del editor de SPA](/help/sites-developing/spa-overview.md): detalles del funcionamiento del editor de SPA.
* [Procesamiento del lado del servidor](/help/sites-developing/spa-ssr.md) AEM SPA - Cómo configurar SSR para la de la
* [SPA Documentos de referencia](/help/sites-developing/spa-reference-materials.md) AEM SPA - Referencias de la API de JavaScript y vínculos a proyectos de código abierto de GitHub de
* [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md): cómo crear fragmentos de contenido
* [Arquetipo del proyecto de AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es): plantilla de Maven que crea un proyecto mínimo, basado en las prácticas recomendadas de Adobe Experience Manager (AEM) como punto de partida para su sitio web
