---
title: Información general de modelos
description: Aprenda a utilizar la administración de modelos, que implica la creación y administración de modelos para asociarlos con objetos de datos posibles.
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 50785534-5784-4354-b123-5e640b7c0242
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---

# Información general de modelos{#models-overview}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

La administración de modelos implica la creación y administración de modelos para asociarlos con objetos de datos posibles. Cada modelo incluye todas las propiedades y definiciones de campo necesarias para facilitar la creación y la renderización de objetos.

Administración de modelos implica la creación de **modelos**, **entidades**, y **espacios**. AEM El diagrama siguiente ilustra la relación entre el contenido de la y los modelos.

![chlimage_1-81](assets/chlimage_1-81.png)

## El modelo de contenido {#the-content-model}

Un modelo describe el tipo de contenido y denota qué información está disponible para la aplicación nativa. Es una descripción de lo que constituye un fragmento de contenido. Un modelo de contenido son las reglas para crear un fragmento de contenido. El modelo de contenido incluye qué datos están disponibles, qué recursos se pueden utilizar, la relación entre recursos y datos, la relación con otros modelos de contenido y los metadatos disponibles.

AEM Los modelos también sirven como una forma de transformar el contenido existente de la en objetos que las aplicaciones móviles nativas pueden utilizar fácilmente.

Content Services proporciona algunos modelos predeterminados para objetos comunes como recursos, colecciones de recursos, páginas de HTML, configuraciones de aplicación y páginas independientes del canal. AEM Se pueden configurar para que puedan satisfacer las necesidades específicas de los clientes sin requerir un esfuerzo de desarrollo de la.

Los usuarios pueden crear sus propios modelos. AEM Esto permite la creación de nuevos tipos de contenido que aún no son administrados por los usuarios de la aplicación de la manera de hacer un seguimiento de la segmentación de datos La creación del modelo se realiza mediante una interfaz de usuario que utiliza tipos primitivos existentes.

El diagrama siguiente ilustra el modelo de contenido para aplicaciones AEM Mobile y cómo se asignan las entidades, carpetas y espacios a una aplicación.

![chlimage_1-82](assets/chlimage_1-82.png)

### Los modelos {#the-models}

Los modelos se utilizan para determinar cómo se crean las entidades. AEM Definen qué está disponible en una entidad y cómo se generan esos datos a partir del contenido de la. Antes de empezar a trabajar con espacios, carpetas y entidades, debe estar familiarizado con la creación y administración de modelos.

>[!NOTE]
>
>Existe un modelo fuera de una aplicación, ya que más de una aplicación puede utilizarlo.
>

Para crear y administrar modelos en el tablero y el repositorio, consulte **[Modelos](/help/mobile/administer-mobile-apps.md)**.

### Entidades en el modelo de contenido {#entities-in-content-model}

Una entidad es una instancia de un modelo de contenido. Una entidad se expone a través de la API de servicios de contenido a la biblioteca del lado del cliente y proporciona una forma para que una aplicación nativa acceda al contenido de forma independiente del canal.

AEM AEM Si hay contenido de existente, se genera una entidad mediante un modelo y la fuente de contenido de la. AEM Por ejemplo, una entidad de página es un objeto independiente del canal y del diseño que se genera a partir de una página de la página y del modelo de página de la página de la página de la página de la aplicación.

Los cambios en el contenido referenciado de una entidad dan como resultado un cambio en la entidad. Por ejemplo, si *cq:page* se actualiza, entonces también se actualiza cualquier entidad basada en esa página.

Para crear entidades personalizadas a partir de modelos, consulte **[Uso de entidades](/help/mobile/spaces-and-entities.md)**.

>[!NOTE]
>
>AEM Si el modelo no se corresponde con un contenido de la interfaz de usuario existente, como el cliente ha creado un modelo, hay una interfaz de usuario para que un cliente pueda crear una entidad.
>

### Espacios en el modelo de contenido {#spaces-in-content-model}

Se utiliza un espacio para organizar entidades para facilitar el acceso. Un espacio puede contener uno o más tipos de entidad y puede contener subcarpetas.

AEM Por el lado de la, un espacio es una forma cómoda de administrar las entidades relacionadas. También se puede utilizar para asignar permisos de autorización. La autorización se puede realizar en un espacio, que protege las entidades que se encuentran en ese espacio.

*Por ejemplo*,

Un usuario tiene tres clasificaciones generales de entidades. Una es solo para uso interno, otra está aprobada para uso público y una tercera es para entidades comunes que son utilizadas por muchas aplicaciones. Para facilitar la administración, el usuario crea tres espacios, a saber: *interno*, *público* (con contenido en inglés y francés), y *común* para gestionar las entidades adecuadas como se indica a continuación:

* /content/entities/internal
* /content/entities/public/es
* /content/entities/public/fr
* /content/entities/common

Se proporciona un punto final de servicio al espacio para que la biblioteca de cliente nativa pueda solicitar una lista del contenido de un espacio. Este &quot;listado&quot; se devuelve como un objeto JSON.

Consulte **[Espacios y entidades](/help/mobile/spaces-and-entities.md)** para crear y publicar espacios.

>[!NOTE]
>
>Muchas aplicaciones pueden utilizar un espacio, mientras que una aplicación puede utilizar muchos espacios.

### Carpetas en el modelo de contenido {#folders-in-content-model}

Las carpetas permiten a los usuarios organizar las entidades según sea necesario y facilitan un control ACL más preciso. Los espacios pueden incluir carpetas para ayudar a organizar aún más el contenido y los recursos del espacio. Un usuario puede crear su propia jerarquía bajo un espacio.

Para crear y administrar carpetas dentro de un espacio, consulte **[Trabajar con carpetas en un espacio](/help/mobile/spaces-and-entities.md)**.
