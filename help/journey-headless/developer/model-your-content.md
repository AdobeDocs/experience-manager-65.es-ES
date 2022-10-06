---
title: Cómo modelar el contenido
description: En esta parte del Recorrido para desarrolladores sin encabezado de AEM, aprenda a modelar el contenido para AEM entrega sin encabezado mediante Modelado de contenido con modelos de fragmentos de contenido y fragmentos de contenido.
exl-id: f75b433f-5a81-4259-a9f5-b58954b87970
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1826'
ht-degree: 5%

---

# Cómo modelar el contenido {#model-your-content}

En esta parte del [recorrido para desarrolladores AEM sin encabezado](overview.md), puede aprender a modelar la estructura de contenido. A continuación, observe esa estructura para Adobe Experience Manager (AEM) mediante los modelos de fragmentos de contenido y los fragmentos de contenido, para reutilizarla en todos los canales.

## La historia hasta ahora {#story-so-far}

Al principio [Obtenga Información Sobre El Desarrollo Sin Cabeza De CMS](learn-about.md) entrega de contenido sin encabezado cubierto y por qué debería usarse. Entonces [Introducción a AEM sin encabezado](getting-started.md) descrita AEM sin encabezado en el contexto de su propio proyecto.

En el documento anterior del recorrido sin AEM, [Ruta a la primera experiencia usando AEM sin encabezado](path-to-first-experience.md), aprendió los pasos necesarios para implementar el primer proyecto. Después de leerlo, debe:

* Comprender las consideraciones de planificación importantes para diseñar el contenido
* Comprender los pasos para implementar sin encabezado según los requisitos de nivel de integración.
* Configure las herramientas y configuraciones de AEM necesarias.
* Conozca las prácticas recomendadas para que su recorrido sin objetivos sea fluido, mantenga la eficiencia de la generación de contenido y asegúrese de que el contenido se entregue rápidamente.

Este artículo se basa en estos fundamentos para que entienda cómo preparar su propio AEM proyecto sin objetivos.

## Objetivo {#objective}

* **Audiencia**: Principiante
* **Objetivo**: Aprenda a modelar la estructura de contenido y luego a comprender esa estructura utilizando AEM modelos de fragmentos de contenido y fragmentos de contenido:
   * Introduzca conceptos y terminología relacionados con el modelado de datos/contenido.
   * Descubra por qué se necesita el modelado de contenido para la entrega de contenido sin encabezado.
   * Aprenda a realizar esta estructura utilizando AEM modelos de fragmento de contenido (y cree contenido con fragmentos de contenido).
   * Aprenda a modelar el contenido; principios con muestras básicas.

>[!NOTE]
>
>El modelado de datos es un campo muy grande, ya que se utiliza al desarrollar bases de datos relacionales. Hay muchos libros, y fuentes de información en línea, disponibles.
>
>Solo se tendrán en cuenta los aspectos que son de interés al modelar datos para su uso con AEM sin encabezado.

## Modelado de contenido {#content-modeling}

*Es un mundo grande, malo*.

Tal vez, tal vez no, pero ciertamente es un gran ***complicado*** el mundo y el modelado de datos se utilizan para definir una representación simplificada de una subsección muy (muy) pequeña, utilizando la información específica necesaria para un determinado fin.

>[!NOTE]
>
>Como AEM trata del contenido, nos referimos a Modelado de datos como Modelado de contenido.

Por ejemplo:

Hay muchas escuelas, pero todas tienen varias cosas en común:

* Una ubicación
* Un profesor jefe
* Muchos profesores
* Muchos miembros del personal no docente
* Muchos alumnos
* Muchos ex profesores
* Muchos ex alumnos
* Muchas aulas
* Muchos (muchos) libros
* Muchos (muchos) equipos
* Muchas actividades extracurriculares
* y así sucesivamente....

Incluso en un ejemplo tan pequeño la lista puede parecer interminable. Pero si simplemente desea que la aplicación realice una tarea sencilla, debe limitar la información a lo esencial.

Por ejemplo, la publicidad de eventos especiales para todas las escuelas de la zona:

* Nombre del colegio
* Ubicación del colegio
* Profesor jefe
* Tipo de evento
* Fecha del evento
* Profesor organizando el evento

### Conceptos  {#concepts}

Se denomina **Entidades** - básicamente las &quot;cosas&quot; de las que queremos almacenar información.

La información que queremos almacenar sobre ellos es la **Atributos** (propiedades), como Nombre y Cualificaciones para los profesores.

Luego hay varias **Relaciones** entre las entidades. Por ejemplo, normalmente una escuela tiene un solo profesor jefe y muchos maestros (y normalmente el profesor jefe también es profesor).

Se llama al proceso de análisis y definición de esta información, junto con las relaciones entre ellos **Modelado de contenido**.

### Datos básicos {#basics}

A menudo es necesario empezar por elaborar un **Esquema conceptual** que describe las entidades y sus relaciones. Normalmente es de alto nivel (conceptual).

Una vez estable, puede convertir los modelos en un **Esquema lógico** que describe las entidades, junto con los atributos y las relaciones. En este nivel, debe examinar detenidamente las definiciones para eliminar la duplicación y optimizar el diseño.

>[!NOTE]
>
>A veces, estos dos pasos se combinan, a menudo según la complejidad del escenario.

Por ejemplo, si necesita entidades independientes para `Head Teacher` y `Teacher`, o simplemente un atributo adicional en la variable `Teacher` modelo?

### Garantizar la integridad de los datos {#data-integrity}

La integridad de los datos es necesaria para garantizar la precisión y coherencia del contenido durante todo su ciclo de vida. Esto incluye garantizar que los autores de contenido puedan comprender fácilmente qué almacenar, por lo que lo siguiente es vital:

* una estructura clara
* una estructura lo más concisa posible (sin sacrificar la precisión)
* validación de campos individuales
* cuando proceda, restringir el contenido de campos específicos a lo que sea significativo

### Eliminación de la redundancia de datos {#data-redundancy}

La redundancia de datos se produce cuando la misma información se almacena dos veces dentro de la estructura de contenido. Esto debe evitarse, ya que puede provocar confusión al crear el contenido y errores al consultar; sin mencionar el uso indebido del espacio de almacenamiento.

### Optimización y rendimiento {#optimization-and-performance}

Al optimizar su estructura, puede mejorar el rendimiento, tanto para la creación de contenido como para las consultas.

Todo es un acto de equilibrio, pero la creación de una estructura demasiado compleja o con demasiados niveles puede:

* Sea confuso para los autores que generan el contenido.

* Afecta gravemente al rendimiento si la consulta tiene que acceder a varios fragmentos de contenido anidados (referenciados) para recuperar el contenido requerido.

## Modelado de contenido para AEM sin encabezado {#content-modeling-for-aem-headless}

El modelado de datos es un conjunto de técnicas establecidas, que a menudo se utilizan cuando se desarrollan bases de datos de relaciones, por lo que ¿qué significa el modelado de contenido para AEM sin encabezado?

### ¿Por qué? {#why}

Para garantizar que su aplicación pueda solicitar y recibir de forma consistente y eficiente el contenido necesario de AEM, este contenido debe estar estructurado.

Esto significa que la aplicación conoce de antemano la forma de respuesta y, por lo tanto, cómo procesarla. Esto es mucho más fácil que recibir contenido de forma libre, que debe analizarse para determinar qué contiene y, por lo tanto, cómo puede utilizarse.

### Introducción a How? {#how}

AEM utiliza los fragmentos de contenido para proporcionar las estructuras necesarias para la entrega sin encabezado de su contenido a sus aplicaciones.

La estructura del modelo de contenido es:

* realizado mediante la definición del modelo de fragmento de contenido,
* se utiliza como base de los fragmentos de contenido utilizados para la generación de contenido.

>[!NOTE]
>
>Los modelos de fragmento de contenido también se utilizan como base de los esquemas AEM de GraphQL, que se utilizan para recuperar contenido; más información al respecto en una sesión posterior.

Las solicitudes de contenido se realizan mediante la API de AEM GraphQL, una implementación personalizada de la API estándar de GraphQL. La API de AEM GraphQL permite realizar consultas (complejas) en los fragmentos de contenido, cada una de las cuales depende de un tipo de modelo específico.

Las aplicaciones pueden utilizar el contenido devuelto.

## Creación de la estructura con modelos de fragmento de contenido {#create-structure-content-fragment-models}

Los modelos de fragmento de contenido proporcionan varios mecanismos que le permiten definir la estructura del contenido.

Un modelo de fragmento de contenido describe una entidad.

>[!NOTE]
>Debe habilitar la funcionalidad Fragmento de contenido en el navegador de configuración para poder crear nuevos modelos.

>[!TIP]
>
>Se debe asignar un nombre al modelo para que el autor del contenido sepa qué modelo seleccionar al crear un fragmento de contenido.

Dentro de un modelo:

1. **Tipos de datos** permite definir los atributos individuales.
Por ejemplo, defina el campo que contiene el nombre de un profesor como **Texto** y sus años de servicio como **Número**.
1. Los tipos de datos **Referencia de contenido** y **Referencia de fragmento** permite crear relaciones con otro contenido dentro de AEM.
1. La variable **Referencia de fragmento** el tipo de datos le permite obtener varios niveles de estructura anidando los fragmentos de contenido (según el tipo de modelo). Esto es vital para el modelado de contenido.

Por ejemplo:
![Modelado de contenido con fragmentos de contenido](assets/headless-modeling-01.png "Modelado de contenido con fragmentos de contenido")

### Tipos de datos {#data-types}

AEM proporciona los siguientes tipos de datos para modelar el contenido:

* Texto de línea única
* Texto multilínea
* Número
* Booleano
* Fecha y hora
* Lista desglosada
* Etiquetas
* Referencia de contenido
* Referencia al fragmento
* Objeto JSON

### Referencias y contenido anidado {#references-nested-content}

Dos tipos de datos proporcionan referencias al contenido fuera de un fragmento específico:

* **Referencia de contenido**
Esto proporciona una sencilla referencia a otro contenido de cualquier tipo.
Por ejemplo, puede hacer referencia a una imagen en una ubicación específica.

* **Referencia de fragmento**
Esto proporciona referencias a otros fragmentos de contenido.
Este tipo de referencia se utiliza para crear contenido anidado y presenta las relaciones necesarias para modelar el contenido.
El tipo de datos se puede configurar para que los autores de fragmentos puedan hacer lo siguiente:
   * Editar directamente el fragmento al que se hace referencia.
   * Crear un nuevo fragmento de contenido basado en el modelo apropiado

### Creación de modelos de fragmento de contenido {#creating-content-fragment-models}

Desde el principio, debe habilitar los modelos de fragmento de contenido para su sitio, esto se hace en el navegador de configuración; en Herramientas -> General -> Explorador de configuración. Puede seleccionar para configurar la entrada global o crear una nueva configuración. Por ejemplo:

![Definir configuración](assets/cfm-configuration.png)

>[!NOTE]
>
>Consulte Recursos adicionales: Fragmentos de contenido en el navegador de configuración

A continuación, se pueden crear los modelos de fragmentos de contenido y definir la estructura. Esto se puede hacer en Herramientas -> Recursos -> Modelos de fragmento de contenido. Por ejemplo:

![Modelo de fragmento de contenido](assets/cfm-model.png)

>[!NOTE]
>
>Consulte Recursos adicionales: Modelos de fragmento de contenido.

## Uso del modelo para crear contenido con fragmentos de contenido {#use-content-to-author-content}

Los fragmentos de contenido siempre se basan en un modelo de fragmento de contenido. El modelo proporciona la estructura, el fragmento alberga el contenido.

### Selección del modelo apropiado {#select-model}

El primer paso para crear el contenido es crear un fragmento de contenido. Esto se realiza mediante Crear -> Fragmento de contenido en la carpeta requerida en Assets -> Archivos. El asistente lo guiará a través de los pasos.

Un fragmento de contenido se basa en un modelo de fragmento de contenido específico que se selecciona como primer paso del proceso de creación.

### Creación y edición de contenido estructurado {#create-edit-structured-content}

Una vez creado el fragmento, puede abrirlo en el Editor de fragmentos de contenido. Aquí puede hacer lo siguiente:

* Edite el contenido en modo normal o de pantalla completa.
* Dé formato al contenido como Texto completo, Texto sin formato o Marcado.
* Cree y administre Variaciones de su contenido.
* Asociar contenido.
* Edite los metadatos.
* Mostrar la estructura de árbol.
* Previsualización de la representación JSON.

### Creación de fragmentos de contenido {#creating-content-fragments}

Después de seleccionar el modelo adecuado, se abre un fragmento de contenido para editarlo en el Editor de fragmentos de contenido:

![Editor de fragmentos de contenido](assets/cfm-editor.png)

>[!NOTE]
>
>Consulte Recursos adicionales: Uso de fragmentos de contenido.

## Introducción a algunos ejemplos {#getting-started-examples}

<!--
tbc...
...and/or see the structures covered for the GraphQL samples...
...will those (ever) be delivered as an official sample package?
-->

Para obtener una estructura básica como ejemplo, consulte La estructura del fragmento de contenido de ejemplo.

## Siguientes pasos {#whats-next}

Ahora que ha aprendido a modelar su estructura y a crear contenido en función de eso, el siguiente paso es [Aprenda a utilizar las consultas de GraphQL para acceder y recuperar el contenido de los fragmentos de contenido](access-your-content.md). Esto presentará y analizará GraphQL, y luego verá algunas consultas de ejemplo para ver cómo funcionan las cosas en la práctica.

## Recursos adicionales {#additional-resources}

* [Uso de fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) : la página de inicio para los fragmentos de contenido
   * [Fragmentos de contenido en el navegador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md) - habilitar la funcionalidad Fragmento de contenido en el navegador de configuración
   * [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md) - crear y editar modelos de fragmento de contenido
   * [Administración de fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md) - crear y crear fragmentos de contenido; esta página le llevará a otras secciones detalladas
* [Esquemas de AEM GraphQL](access-your-content.md) - cómo GraphQL realiza los modelos
* [La estructura de fragmento de contenido de ejemplo](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [Introducción a AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=es) : una breve serie de tutoriales de vídeo que ofrecen información general sobre el uso de AEM funciones sin encabezado, incluidos el modelado de contenido y GraphQL
   * [Conceptos básicos de modelos de GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/video-series/modeling-basics.html) - Aprenda a definir y utilizar fragmentos de contenido en Adobe Experience Manager (AEM) para utilizarlos con GraphQL.
