---
title: Información general sobre modelos
seo-title: Información general sobre modelos
description: Información general sobre modelos
seo-description: nulo
uuid: e09dac52-9515-43f7-9d3b-6637e2283d59
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: c8281f98-9811-42f7-9a31-f82dd0f09319
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 0%

---


# Información general de modelos{#models-overview}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

La administración de modelos implica la creación y administración de modelos con el fin de asociarlos con posibles objetos de datos. Cada modelo incluirá todas las propiedades y definiciones de campo necesarias para facilitar la creación y renderización de objetos.

La administración de modelos implica la creación de **modelos**, **entidades** y **espacios**. En el diagrama siguiente se ilustra la relación entre el contenido de AEM y los modelos.

![chlimage_1-81](assets/chlimage_1-81.png)

## El modelo de contenido {#the-content-model}

Un modelo describe el tipo de contenido y denota qué información estará disponible para la aplicación nativa. Es una descripción de lo que constituye un fragmento de contenido. Un modelo de contenido son las reglas para la creación de contenido. El modelo de contenido incluye qué datos están disponibles, qué recursos se pueden utilizar, la relación entre recursos y datos, la relación con otros modelos de contenido y los metadatos disponibles.

Los modelos también sirven para transformar el contenido de AEM existente en objetos que las aplicaciones móviles nativas puedan utilizar fácilmente.

Los servicios de contenido ofrecerán algunos modelos predeterminados para objetos comunes, como recursos, colecciones de recursos, páginas HTML, configuraciones de aplicaciones y páginas independientes de canales. Se pueden configurar para que satisfagan necesidades específicas del cliente sin necesidad de un esfuerzo de desarrollo AEM.

El usuario puede crear sus propios modelos. Esto permite la creación de nuevos tipos de contenido que no están administrados por AEM. La creación del modelo se realiza mediante una interfaz de usuario que utiliza tipos primitivos existentes.

En el diagrama siguiente se ilustra el modelo de contenido de las aplicaciones de AEM Mobile y cómo se asignan a una aplicación entidades, carpetas y espacios.

![chlimage_1-82](assets/chlimage_1-82.png)

### Los modelos {#the-models}

Los modelos se utilizan para determinar cómo se crean las entidades. Definen qué está disponible en una entidad y cómo se generan esos datos a partir de AEM contenido. Antes de empezar a trabajar con espacios, carpetas y entidades, debe estar familiarizado con la creación y administración de modelos.

>[!NOTE]
>
>Existe un modelo fuera de una aplicación, ya que más de una aplicación puede utilizarlo.


Consulte **[Modelos](/help/mobile/administer-mobile-apps.md)** para crear y administrar modelos en el panel y el repositorio.

### Entidades del modelo de contenido {#entities-in-content-model}

Una entidad es una instancia de un modelo de contenido. Una entidad se expone a través de la API de servicios de contenido a la biblioteca del lado del cliente y proporciona una forma para que una aplicación nativa acceda al contenido de forma independiente del canal.

En el caso de contenido de AEM existente, una entidad se genera mediante un modelo y la fuente de contenido de AEM. Por ejemplo, una entidad de página es un objeto independiente de canal y presentación que se genera a partir de una página AEM y el modelo de página.

Los cambios en el contenido al que se hace referencia en una entidad provocarán un cambio en la entidad. Por ejemplo, si se actualiza un *cq:page*, también se actualizarán las entidades basadas en esa página.

Consulte **[Uso de entidades](/help/mobile/spaces-and-entities.md)** para crear entidades personalizadas a partir de modelos.

>[!NOTE]
>
>Si el modelo no corresponde a un contenido de AEM existente, como que el cliente haya creado un modelo nuevo, entonces habrá una interfaz de usuario para que un cliente pueda crear una entidad nueva.


### Espacios en el modelo de contenido {#spaces-in-content-model}

Un espacio se utiliza para organizar entidades para facilitar el acceso. Un espacio puede contener uno o más tipos de entidades y puede contener subcarpetas.

En el lado AEM, un espacio es una forma cómoda de administrar entidades relacionadas. También se puede utilizar para asignar permisos de autorización. La autorización se puede realizar en un espacio, que protegerá las entidades que se encuentran en ese espacio.

*Por ejemplo*,

Un usuario tiene tres clasificaciones generales de entidades. Una es solo para uso interno, otra está aprobada para uso público y la tercera es para entidades comunes que son utilizadas por muchas aplicaciones. Para facilitar la administración, el usuario crea tres espacios, *internal*, *public* (con contenido en inglés y en francés) y *common* para administrar las entidades adecuadas, como se menciona a continuación:

* /content/entities/internal
* /content/entities/public/en
* /content/entities/public/fr
* /content/entities/common

Se proporcionará un punto final de servicio al espacio para que la biblioteca cliente nativa pueda solicitar una lista del contenido de un espacio. Este &quot;listado&quot; se devolverá como un objeto JSON.

Consulte **[Espacios y entidades](/help/mobile/spaces-and-entities.md)** para crear y publicar espacios.

>[!NOTE]
>
>Muchas aplicaciones pueden utilizar un espacio y una aplicación puede utilizar muchos espacios.

### Carpetas en el modelo de contenido {#folders-in-content-model}

Las carpetas permiten a los usuarios organizar las entidades según sea necesario y facilitan un control ACL más preciso. Los espacios pueden incluir carpetas para ayudar a organizar mejor el contenido y los recursos del espacio. Un usuario puede crear su propia jerarquía en un espacio.

Consulte **[Trabajo con carpetas en un espacio](/help/mobile/spaces-and-entities.md)** para crear y administrar carpetas dentro de un espacio.
