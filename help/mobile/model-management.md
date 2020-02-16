---
title: Información general de modelos
seo-title: Información general de modelos
description: nulo
seo-description: nulo
uuid: e09dac52-9515-43f7-9d3b-6637e2283d59
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: c8281f98-9811-42f7-9a31-f82dd0f09319
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Información general de modelos{#models-overview}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

La administración de modelos implica la creación y administración de modelos con el fin de asociarlos a objetos de datos eventuales. Cada modelo incluirá todas las propiedades y definiciones de campo necesarias para facilitar la creación y representación de objetos.

La administración de modelos implica la creación de **modelos**, **entidades** y **espacios**. El diagrama siguiente ilustra la relación entre el contenido de AEM y los modelos.

![chlimage_1-81](assets/chlimage_1-81.png)

## El modelo de contenido {#the-content-model}

Un modelo describe el tipo de contenido y indica qué información estará disponible para la aplicación nativa. Es una descripción de lo que conforma un contenido. Un modelo de contenido son las reglas para crear un fragmento de contenido. El modelo de contenido incluye los datos disponibles, los recursos que se pueden utilizar, la relación entre los recursos y los datos, la relación con otros modelos de contenido y los metadatos disponibles.

Los modelos también sirven para transformar el contenido existente de AEM en objetos que las aplicaciones móviles nativas pueden utilizar fácilmente.

Content Services proporcionará algunos modelos predeterminados para objetos comunes como recursos, colecciones de recursos, páginas HTML, configuraciones de aplicaciones y páginas independientes de canales. Se podrán configurar para que satisfagan las necesidades específicas de los clientes sin necesidad de un esfuerzo de desarrollo de AEM.

El usuario puede crear sus propios modelos. Esto permite la creación de nuevos tipos de contenido que AEM aún no administra. La creación de modelos se realiza mediante una interfaz de usuario que utiliza tipos primitivos existentes.

El diagrama siguiente ilustra el modelo de contenido de las aplicaciones de AEM Mobile y cómo se asignan entidades, carpetas y espacios a una aplicación.

![chlimage_1-82](assets/chlimage_1-82.png)

### Modelos {#the-models}

Los modelos se utilizan para determinar cómo se crean las entidades. Definen lo que está disponible en una entidad y cómo se generan los datos a partir del contenido de AEM. Antes de empezar a trabajar con espacios, carpetas y entidades, debe estar familiarizado con la creación y administración de modelos.

>[!NOTE]
>
>Existe un modelo fuera de una aplicación, ya que más de una aplicación puede utilizarlo.


Consulte **[Modelos](/help/mobile/administer-mobile-apps.md)**para crear y administrar modelos en el tablero y el repositorio.

### Entidades en el modelo de contenido {#entities-in-content-model}

Una entidad es una instancia de un modelo de contenido. Una entidad se expone a través de la Content Services API a la biblioteca del cliente y proporciona una forma de que una aplicación nativa acceda al contenido de forma independiente del canal.

En el caso de contenido existente de AEM, se genera una entidad mediante un modelo y el origen de contenido de AEM. Por ejemplo, una entidad de página es un objeto independiente de canal y diseño que se genera a partir de una página de AEM y del modelo de página.

Los cambios en el contenido al que se hace referencia de una entidad provocarán un cambio en la misma. Por ejemplo, si se actualiza una *cq:page* , también se actualizarán todas las entidades basadas en esa página.

Consulte **[Uso de entidades](/help/mobile/spaces-and-entities.md)**para crear entidades personalizadas a partir de modelos.

>[!NOTE]
>
>Si el modelo no corresponde a un contenido de AEM existente, como el cliente ha creado un modelo nuevo, entonces habrá una interfaz de usuario para que un cliente pueda crear una entidad nueva.


### Espacios en el modelo de contenido {#spaces-in-content-model}

Se utiliza un espacio para organizar entidades para facilitar el acceso. Un espacio puede contener uno o varios tipos de entidades y subcarpetas.

En el lado de AEM, un espacio es una forma práctica de administrar entidades relacionadas. También puede utilizarse para asignar permisos de autorización. La autorización puede realizarse en un espacio, que protegerá las entidades que se encuentren en ese espacio.

*Por ejemplo*,

Un usuario tiene tres clasificaciones generales de entidades. Una es solo para uso interno, otra está aprobada para uso público y la tercera es para entidades comunes que son utilizadas por muchas aplicaciones. Para facilitar la gestión, el usuario crea tres espacios: *interno*, *público* (con contenido en inglés y en francés) y *común* para la gestión de las entidades adecuadas, como se indica a continuación:

* /content/entity/internal
* /content/entity/public/es
* /content/entity/public/fr
* /content/entity/common

Se proporcionará un punto final de servicio al espacio para que la biblioteca cliente nativa pueda solicitar una lista del contenido de un espacio. Este &quot;listado&quot; se devolverá como un objeto JSON.

Consulte **[Espacios y entidades](/help/mobile/spaces-and-entities.md)**para crear y publicar espacios.

>[!NOTE]
>
>Muchas aplicaciones pueden utilizar un espacio y una aplicación puede utilizar muchos espacios.

### Carpetas en el modelo de contenido {#folders-in-content-model}

Las carpetas permiten a los usuarios organizar las entidades según sea necesario y facilitan un control ACL más preciso. Los espacios pueden incluir carpetas para ayudar a organizar mejor el contenido y los recursos del espacio. Un usuario puede crear su propia jerarquía en un espacio.

Consulte **[Uso de carpetas en un espacio](/help/mobile/spaces-and-entities.md)**para crear y administrar carpetas dentro de un espacio.
