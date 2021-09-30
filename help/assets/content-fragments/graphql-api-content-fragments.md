---
title: AEM API de GraphQL para su uso con fragmentos de contenido
description: Aprenda a utilizar los fragmentos de contenido en Adobe Experience Manager (AEM) con la API de AEM GraphQL para la entrega de contenido sin encabezado.
feature: Content Fragments,GraphQL API
exl-id: beae1f1f-0a76-4186-9e58-9cab8de4236d
source-git-commit: 67e145e250bbe386168ab2c0f8967f91aa9d8a36
workflow-type: tm+mt
source-wordcount: '3919'
ht-degree: 1%

---

# AEM API de GraphQL para su uso con fragmentos de contenido {#graphql-api-for-use-with-content-fragments}

Aprenda a utilizar los fragmentos de contenido en Adobe Experience Manager (AEM) con la API de AEM GraphQL para la entrega de contenido sin encabezado.

AEM API de GraphQL utilizada con los fragmentos de contenido se basa principalmente en la API estándar de código abierto de GraphQL.

El uso de la API de GraphQL en AEM permite la entrega eficiente de fragmentos de contenido a clientes JavaScript en implementaciones CMS sin encabezado:

* Evitar solicitudes de API iterativas como con REST,
* Garantizar que la entrega se limite a los requisitos específicos,
* Permitir el envío masivo de exactamente lo que se necesita para procesar como respuesta a una sola consulta de API.

>[!NOTE]
>
>GraphQL se utiliza actualmente en dos escenarios (independientes) en Adobe Experience Manager (AEM):
>
>* [AEM Commerce consume datos de una plataforma de comercio a través de GraphQL](/help/commerce/cif/integrating/magento.md).
>* AEM fragmentos de contenido trabajan junto con la API de GraphQL de AEM (una implementación personalizada, basada en GraphQL estándar) para ofrecer contenido estructurado para su uso en aplicaciones.


## La API de GraphQL {#graphql-api}

GraphQL es:

* &quot;*...un idioma de consulta para API y un tiempo de ejecución para cumplir esas consultas con los datos existentes. GraphQL proporciona una descripción completa y comprensible de los datos de su API, da a los clientes la capacidad de preguntar exactamente lo que necesitan y nada más, facilita la evolución de las API con el tiempo y permite potentes herramientas para desarrolladores.*&quot;.

   Consulte [GraphQL.org](https://graphql.org)

* &quot;*...una especificación abierta para una capa de API flexible. Coloque GraphQL sobre los backends existentes para crear productos más rápido que nunca....*&quot;.

   Consulte [Explorar GraphQL](https://www.graphql.com).

* *&quot;...especificación y lenguaje de consulta de datos desarrollados internamente por Facebook en 2012 antes de ser de código abierto público en 2015. Proporciona una alternativa a las arquitecturas basadas en REST con el propósito de aumentar la productividad del desarrollador y minimizar las cantidades de datos transferidos. GraphQL se utiliza en la producción por cientos de organizaciones de todos los tamaños...&quot;*

   Consulte [GraphQL Foundation](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

Para obtener más información sobre la API de GraphQL, consulte las siguientes secciones (entre muchos otros recursos):

* En [graphql.org](https://graphql.org):

   * [Introducción a GraphQL](https://graphql.org/learn)

   * [Especificación de GraphQL](https://spec.graphql.org/)

* En [graphql.com](https://graphql.com):

   * [Guías](https://www.graphql.com/guides/)

   * [Tutoriales](https://www.graphql.com/tutorials/)

   * [Casos prácticos](https://www.graphql.com/case-studies/)

La implementación de GraphQL para AEM se basa en la biblioteca Java estándar de GraphQL. Consulte:

* [graphQL.org: Java](https://graphql.org/code/#java)

* [GraphQL Java en GitHub](https://github.com/graphql-java)

### Terminología de GraphQL {#graphql-terminology}

GraphQL utiliza lo siguiente:

* **[Consultas](https://graphql.org/learn/queries/)**

* **[Esquemas y tipos](https://graphql.org/learn/schema/)**:

   * Los esquemas se generan mediante AEM basados en los modelos de fragmento de contenido.
   * Con sus esquemas, GraphQL presenta los tipos y operaciones permitidos para la implementación de GraphQL AEM.

* **[Campos](https://graphql.org/learn/queries/#fields)**

* **[Extremo de GraphQL](#graphql-aem-endpoint)**
   * Ruta en AEM que responde a consultas de GraphQL y proporciona acceso a los esquemas de GraphQL.

   * Consulte [Activación del punto final de GraphQL](#enabling-graphql-endpoint) para obtener más información.

Consulte la [(GraphQL.org) Introducción a GraphQL](https://graphql.org/learn/) para obtener información detallada, incluidas las [Prácticas recomendadas](https://graphql.org/learn/best-practices/).

### Tipos de consulta de GraphQL {#graphql-query-types}

Con GraphQL puede realizar consultas para devolver:

* Una **entrada única**

* Una **[lista de entradas](https://graphql.org/learn/schema/#lists-and-non-null)**

También puede realizar:

* [Consultas persistentes, que se almacenan en caché](#persisted-queries-caching)

>[!NOTE]
>Puede probar y depurar consultas de GraphQL mediante el [GraphiQL IDE](#graphiql-interface).

## GraphQL para AEM extremo {#graphql-aem-endpoint}

El punto final es la ruta utilizada para acceder a GraphQL para AEM. Al utilizar esta ruta, usted (o su aplicación) pueden:

* acceder al esquema de GraphQL,
* envíe sus consultas de GraphQL,
* reciba las respuestas (a sus consultas de GraphQL).

Hay dos tipos de extremos en AEM:

* Global
   * Disponible para su uso en todos los sitios.
   * Este extremo puede utilizar todos los modelos de fragmento de contenido de todas las configuraciones de sitios (definidas en el [Explorador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)).
   * Si hay algún modelo de fragmento de contenido que debería compartirse entre las configuraciones de Sitios, estos deberían crearse en las configuraciones globales de Sitios.
* Configuraciones de sitios:
   * Corresponde a una configuración de Sites, tal como se define en el [Explorador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
   * Específico de un sitio o proyecto especificado.
   * Un extremo específico de la configuración de Sitios usará los modelos de fragmento de contenido de esa configuración de Sitios específica junto con los de la configuración de Sitios global.

>[!CAUTION]
>
>El editor de fragmentos de contenido puede permitir que un fragmento de contenido de una configuración de sitios haga referencia a un fragmento de contenido de otra configuración de sitios (a través de políticas).
>
>En tal caso, no todo el contenido se podrá recuperar mediante un punto final específico de configuración de Sites.
>
>El autor del contenido debe controlar este escenario; por ejemplo, puede resultar útil considerar la posibilidad de colocar los modelos de fragmento de contenido compartido en la configuración de sitios globales.

La ruta del repositorio de GraphQL para AEM punto final global es:

`/content/cq:graphql/global/endpoint`

Para el cual su aplicación puede utilizar la siguiente ruta en la dirección URL de la solicitud:

`/content/_cq_graphql/global/endpoint.json`

Para habilitar un punto final para GraphQL para AEM, debe:

* [Habilitar el extremo de GraphQL](#enabling-graphql-endpoint)
* [Publicar el extremo de GraphQL](#publishing-graphql-endpoint)

### Activación del extremo de GraphQL {#enabling-graphql-endpoint}

Para habilitar un extremo de GraphQL, primero debe tener una configuración adecuada. Consulte [Fragmentos de contenido - Navegador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md).

>[!CAUTION]
>
>Si el [uso de modelos de fragmento de contenido no se ha habilitado](/help/assets/content-fragments/content-fragments-configuration-browser.md), la opción **Crear** no estará disponible.

Para habilitar el punto final correspondiente:

1. Vaya a **Tools**, **Assets** y seleccione **GraphQL**.
1. Seleccione **Crear**.
1. Se abrirá el cuadro de diálogo **Crear nuevo extremo de GraphQL**. Aquí puede especificar:
   * **Nombre**: nombre del extremo; puede escribir cualquier texto.
   * **Utilice el esquema GraphQL proporcionado por**: utilice la lista desplegable para seleccionar el sitio o proyecto requerido.

   >[!NOTE]
   >
   >La siguiente advertencia se muestra en el cuadro de diálogo:
   >
   >* *Los extremos de GraphQL pueden introducir problemas de rendimiento y seguridad de datos si no se administran con cuidado. Asegúrese de definir los permisos adecuados después de crear un extremo.*


1. Confirme con **Crear**.
1. El cuadro de diálogo **Próximos pasos** proporciona un vínculo directo a la consola de seguridad para que pueda asegurarse de que el punto final recién creado tenga los permisos adecuados.

   >[!CAUTION]
   >
   >El punto final es accesible para todos. Esto puede suponer un problema de seguridad, especialmente en las instancias de publicación, ya que las consultas de GraphQL pueden imponer una carga pesada en el servidor.
   >
   >Puede configurar ACL, según su caso de uso, en el punto final.

### Publicación del extremo de GraphQL {#publishing-graphql-endpoint}

Seleccione el nuevo extremo y **Publish** para que esté disponible en todos los entornos.

>[!CAUTION]
>
>El punto final es accesible para todos.
>
>En instancias de publicación esto puede suponer un problema de seguridad, ya que las consultas de GraphQL pueden imponer una carga pesada en el servidor.
>
>Debe configurar las ACL adecuadas para su caso de uso en el punto final.

## Interfaz de GraphiQL {#graphiql-interface}

La implementación de la interfaz estándar [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) está disponible para su uso con AEM GraphQL. Esto se puede [instalar con AEM](#installing-graphiql-interface).

>[!NOTE]
>
>GraphiQL está enlazado al extremo global (y no funciona con otros extremos para configuraciones de sitios específicas).

Esta interfaz le permite introducir y probar directamente consultas.

Por ejemplo:

* `http://localhost:4502/content/graphiql.html`

Esto proporciona funciones como resaltado de sintaxis, autocompletado, autosugerencia, junto con un historial y documentación en línea:

![Interfaz ](assets/cfm-graphiql-interface.png "GraphiQL de GraphiQL")

### Instalación de la interfaz AEM GraphiQL {#installing-graphiql-interface}

<!-- 6.5.10.0??? -->

La interfaz de usuario de GraphiQL se puede instalar en AEM con un paquete dedicado: el paquete [GraphiQL Content Package v0.0.6 (2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip).

>[!NOTE]
>
>El paquete disponible es totalmente compatible con AEM 6.5.10.0 y AEM como Cloud Service.

## Casos de uso para entornos de creación y publicación {#use-cases-author-publish-environments}

Los casos de uso pueden depender del tipo de entorno AEM:

* Entorno de publicación; se usa para:
   * Datos de consulta para la aplicación JS (caso de uso estándar)

* Entorno de creación; se usa para:
   * Datos de consulta para &quot;fines de administración de contenido&quot;:
      * GraphQL en AEM es actualmente una API de solo lectura.
      * La API de REST se puede utilizar para operaciones CR(u)D.

## Permisos {#permission}

Los permisos son los necesarios para acceder a Assets.

## Generación de esquemas {#schema-generation}

GraphQL es una API con establecimiento inflexible de tipos, lo que significa que los datos deben estar claramente estructurados y organizados por tipo.

La especificación de GraphQL proporciona una serie de directrices sobre cómo crear una API robusta para interrogar datos en una instancia determinada. Para ello, un cliente debe recuperar el [Schema](#schema-generation), que contiene todos los tipos necesarios para una consulta.

Para los fragmentos de contenido, los esquemas (estructura y tipos) de GraphQL se basan en **Modelos de fragmento de contenido** [Habilitados](/help/assets/content-fragments/content-fragments-models.md) y en sus tipos de datos.

>[!CAUTION]
>
>Todos los esquemas de GraphQL (derivados de los modelos de fragmento de contenido que han sido **Enabled**) se pueden leer a través del extremo de GraphQL.
>
>Esto significa que debe asegurarse de que no hay datos confidenciales disponibles, ya que podrían filtrarse de esta manera; por ejemplo, esto incluye información que podría estar presente como nombres de campo en la definición del modelo.

Por ejemplo, si un usuario creó un Modelo de fragmento de contenido denominado `Article`, AEM genera el objeto `article` que es de un tipo `ArticleModel`. Los campos dentro de este tipo corresponden a los campos y tipos de datos definidos en el modelo.

1. Un modelo de fragmento de contenido:

   ![Modelo de fragmento de contenido para usar con el Modelo de fragmento de ](assets/cfm-graphqlapi-01.png "GraphQLContent para usar con GraphQL")

1. El esquema correspondiente de GraphQL (salida de la documentación automática de GraphiQL):
   ![Esquema GraphQL basado en el ](assets/cfm-graphqlapi-02.png "modelo de fragmento de contenidoEsquema de GraphQL basado en el modelo de fragmento de contenido")

   Esto muestra que el tipo generado `ArticleModel` contiene varios [campos](#fields).

   * Tres de ellos han sido controlados por el usuario: `author`, `main` y `referencearticle`.

   * Los demás campos los agregó automáticamente AEM y representan métodos útiles para proporcionar información sobre un determinado fragmento de contenido; en este ejemplo, `_path`, `_metadata`, `_variations`. Estos [campos de ayuda](#helper-fields) están marcados con un `_` anterior para distinguir entre lo que ha definido el usuario y lo que se ha generado automáticamente.

1. Después de que un usuario crea un fragmento de contenido basado en el modelo de artículo, se puede interrogar a través de GraphQL. Para ver ejemplos, consulte [Sample Queries](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries) (basado en una [estructura de fragmento de contenido de ejemplo para usar con GraphQL](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)).

En GraphQL para AEM, el esquema es flexible. Esto significa que se genera automáticamente cada vez que se crea, actualiza o elimina un modelo de fragmento de contenido. Las cachés del esquema de datos también se actualizan al actualizar el modelo de fragmento de contenido.

El servicio Sites GraphQL escucha (en segundo plano) cualquier modificación realizada en un modelo de fragmento de contenido. Cuando se detectan actualizaciones, solo se regenera esa parte del esquema. Esta optimización ahorra tiempo y proporciona estabilidad.

Por ejemplo, si:

1. Instale un paquete que contenga `Content-Fragment-Model-1` y `Content-Fragment-Model-2`:

   1. Se generarán los tipos de GraphQL para `Model-1` y `Model-2`.

1. A continuación, modifique `Content-Fragment-Model-2`:

   1. Solo se actualizará el tipo `Model-2` GraphQL.

   1. Mientras que `Model-1` permanecerá igual.

>[!NOTE]
>
>Esto es importante tener en cuenta en caso de que desee realizar actualizaciones masivas en los modelos de fragmento de contenido a través de la api de REST o de otro modo.

El esquema se sirve a través del mismo extremo que las consultas de GraphQL, con el cliente manejando el hecho de que se llama al esquema con la extensión `GQLschema`. Por ejemplo, si se realiza una solicitud `GET` simple en `/content/cq:graphql/global/endpoint.GQLschema`, el resultado del esquema será el tipo Content: `text/x-graphql-schema;charset=iso-8859-1`.

### Generación de esquemas: modelos no publicados {#schema-generation-unpublished-models}

Cuando los fragmentos de contenido están anidados, puede ocurrir que se publique un modelo de fragmento de contenido principal, pero no un modelo al que se hace referencia.

>[!NOTE]
>
>La interfaz de usuario de AEM evita que esto ocurra, pero si la publicación se realiza mediante programación o con paquetes de contenido, puede ocurrir.

Cuando esto sucede, AEM genera un esquema *incompleto* para el modelo de fragmento de contenido principal. Esto significa que la referencia de fragmento, que depende del modelo no publicado, se elimina del esquema.

## Fields {#fields}

Dentro del esquema hay campos individuales, de dos categorías básicas:

* Campos que se generan.

   Se utiliza una selección de [Tipos de campo](#field-types) para crear campos en función de cómo configure el modelo de fragmento de contenido. Los nombres de los campos se toman del campo **Property Name** del **Data Type**.

   * También está la propiedad **Render As** que se debe tener en cuenta, ya que los usuarios pueden configurar ciertos tipos de datos; por ejemplo, como texto de una sola línea o como campo múltiple.

* GraphQL para AEM también genera varios [campos de ayuda](#helper-fields).

   Se utilizan para identificar un fragmento de contenido o para obtener más información sobre un fragmento de contenido.

### Tipos de campo {#field-types}

GraphQL para AEM admite una lista de tipos. Se representan todos los tipos de datos del modelo de fragmento de contenido compatibles y los tipos de GraphQL correspondientes:

| Modelo de fragmento de contenido: tipo de datos | Tipo de GraphQL | Descripción |
|--- |--- |--- |
| Texto de una sola línea | Cadena, [Cadena] |  Se utiliza para cadenas simples como nombres de autor, nombres de ubicación, etc. |
| Texto de varias líneas | String |  Se utiliza para generar texto como el cuerpo de un artículo |
| Número |  Flotante, [Flotante] | Se utiliza para mostrar números de coma flotante y números regulares |
| Booleano |  Booleano |  Se utiliza para mostrar casillas de verificación → instrucciones simples true/false |
| Fecha Y Hora | Calendario |  Se utiliza para mostrar la fecha y la hora en formato ISO 8086. Según el tipo seleccionado, hay tres sabores disponibles para usar en AEM GraphQL: `onlyDate`, `onlyTime`, `dateTime` |
| Enumeración |  String |  Se utiliza para mostrar una opción de una lista de opciones definidas en la creación del modelo. |
|  Etiquetas |  [String] |  Se utiliza para mostrar una lista de cadenas que representan las etiquetas utilizadas en AEM |
| Referencia de contenido |  Cadena |  Se utiliza para mostrar la ruta hacia otro recurso en AEM |
| Referencia al fragmento |  *Un tipo de modelo* |  Se utiliza para hacer referencia a otro fragmento de contenido de un tipo de modelo determinado, definido cuando se creó el modelo |

### Campos de ayuda {#helper-fields}

Además de los tipos de datos de los campos generados por el usuario, GraphQL para AEM también genera varios campos *helper* para ayudar a identificar un fragmento de contenido o para proporcionar información adicional sobre un fragmento de contenido.

#### Ruta {#path}

El campo de ruta se utiliza como identificador en GraphQL. Representa la ruta del recurso de fragmento de contenido dentro del repositorio de AEM. Se ha elegido como identificador de un fragmento de contenido, ya que:

* es único dentro de AEM,
* se pueden recuperar fácilmente.

El siguiente código muestra las rutas de todos los fragmentos de contenido que se crearon en función del modelo de fragmento de contenido `Person`.

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

Para recuperar un solo fragmento de contenido de un tipo específico, también debe determinar primero su ruta. por ejemplo:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

Consulte [Consulta de muestra: un solo fragmento de ciudad específico](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment).

#### Metadatos {#metadata}

A través de GraphQL, AEM también expone los metadatos de un fragmento de contenido. Los metadatos son la información que describe un fragmento de contenido, como el título de un fragmento de contenido, la ruta de vista en miniatura, la descripción de un fragmento de contenido, la fecha en que se creó, entre otros.

Como los metadatos se generan mediante el Editor de esquemas y, como no tienen una estructura específica, el tipo `TypedMetaData` GraphQL se implementó para exponer los metadatos de un fragmento de contenido. `TypedMetaData` expone la información agrupada por los siguientes tipos escalares:

| Campo |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!`  |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

Cada tipo escalar representa un único par nombre-valor o una matriz de pares nombre-valor, donde el valor de ese par es del tipo en el que se agrupó.

Por ejemplo, si desea recuperar el título de un fragmento de contenido, sabemos que esta propiedad es una propiedad de cadena, por lo que consultaremos todos los metadatos de cadena:

Para consultar metadatos:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      _metadata {
        stringMetadata {
          name
          value
        }
      }
    }
  }
}
```

Puede ver todos los tipos de metadatos de GraphQL si ve el esquema de Generated GraphQL. Todos los tipos de modelo tienen el mismo `TypedMetaData`.

>[!NOTE]
>
>**Diferencia entre metadatos normales y de matriz**
>Tenga en cuenta que tanto `StringMetadata` como `StringArrayMetadata` hacen referencia a lo que se almacena en el repositorio, no a cómo se recuperan.
>
>Por ejemplo, si llama al campo `stringMetadata`, recibirá una matriz de todos los metadatos almacenados en el repositorio como `String` y, si llama a `stringArrayMetadata`, recibirá una matriz de todos los metadatos almacenados en el repositorio como `String[]`.

Consulte [Muestra de consulta para metadatos: enumera los metadatos de los premios titulados GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb).

#### Variaciones {#variations}

El campo `_variations` se ha implementado para simplificar la consulta de las variaciones que tiene un fragmento de contenido. Por ejemplo:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

Consulte [Consulta de muestra: todas las ciudades con una variación denominada](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation).

<!--
## Security Considerations {#security-considerations}
-->

## Variables de GraphQL {#graphql-variables}

GraphQL permite colocar variables en la consulta. Para obtener más información, consulte la documentación de [GraphQL para las variables](https://graphql.org/learn/queries/#variables).

Por ejemplo, para obtener todos los fragmentos de contenido de tipo `Article` que tengan una variación específica, puede especificar la variable `variation` en GraphiQL.

![Variables ](assets/cfm-graphqlapi-03.png "GraphQL")

```xml
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
        items {
            _path
            author
        }
    }
}
 
### in query variables
{
    "variation": "uk"
}
```

## Directivas de GraphQL {#graphql-directives}

En GraphQL existe la posibilidad de cambiar la consulta en función de variables, denominadas Directivas de GraphQL.

Por ejemplo, puede incluir el campo `adventurePrice` en una consulta para todos los `AdventureModels`, en función de una variable `includePrice`.

![Directivas de GraphQL ](assets/cfm-graphqlapi-04.png "Directivas de GraphQL")

```xml
### query
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      adventureTitle
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

## Filtrado {#filtering}

También puede utilizar el filtrado en las consultas de GraphQL para devolver datos específicos.

El filtrado utiliza una sintaxis basada en operadores lógicos y expresiones.

Por ejemplo, la siguiente consulta (básica) filtra todas las personas que tienen un nombre de `Jobs` o `Smith`:

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

Para ver más ejemplos, consulte:

* detalles de [GraphQL para AEM extensiones](#graphql-extensions)

* [Ejemplos de consultas que utilizan este contenido y estructura de ejemplo](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * Y el [Contenido de muestra y estructura](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql) preparados para su uso en consultas de ejemplo

* [Consultas de muestra basadas en el proyecto WKND](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## GraphQL para AEM: Resumen de extensiones {#graphql-extensions}

El funcionamiento básico de las consultas con GraphQL para AEM se adhiera a la especificación estándar de GraphQL. Para las consultas de GraphQL con AEM hay algunas extensiones:

* Si necesita un solo resultado:
   * utilizar el nombre del modelo; ciudad del ejemplo

* Si espera una lista de resultados:
   * añada `List` al nombre del modelo; por ejemplo, `cityList`
   * Consulte [Consulta de muestra: toda la información sobre todas las ciudades](#sample-all-information-all-cities)

* Si desea utilizar un OR lógico:
   * use ` _logOp: OR`
   * Consulte [Consulta de muestra: todas las personas que tienen el nombre &quot;Trabajos&quot; o &quot;Smith&quot;](#sample-all-persons-jobs-smith)

* AND lógico también existe, pero (a menudo) está implícito

* Puede consultar los nombres de campo que se correspondan con los campos del modelo de fragmento de contenido
   * Consulte [Consulta de muestra: detalles completos del CEO y los empleados de una empresa](#sample-full-details-company-ceos-employees)

* Además de los campos del modelo, hay algunos campos generados por el sistema (precedidos de guiones bajos):

   * Para el contenido:

      * `_locale` : revelar el idioma; basado en el Administrador de idiomas
         * Consulte [Consulta de ejemplo para varios fragmentos de contenido de una configuración regional determinada](#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` : para mostrar metadatos del fragmento
         * Consulte [Consulta de muestra para metadatos: enumere los metadatos de los premios titulados GB](#sample-metadata-awards-gb)
      * `_model` : permitir la consulta de un modelo de fragmento de contenido (ruta y título)
         * Consulte [Consulta de ejemplo para un modelo de fragmento de contenido de un modelo](#sample-wknd-content-fragment-model-from-model)
      * `_path` : la ruta al fragmento de contenido dentro del repositorio
         * Consulte [Consulta de muestra: un solo fragmento de ciudad específico](#sample-single-specific-city-fragment)
      * `_reference` : para revelar referencias; incluir referencias en línea en el Editor de texto enriquecido
         * Consulte [Consulta de ejemplo para varios fragmentos de contenido con referencias de recuperación previa](#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` : para mostrar variaciones específicas dentro del fragmento de contenido
         * Consulte [Consulta de muestra: todas las ciudades con una variación con nombre](#sample-cities-named-variation)
   * Y operaciones:

      * `_operator` : aplicar operadores específicos;  `EQUALS`,  `EQUALS_NOT`,  `GREATER_EQUAL`,  `LOWER`,  `CONTAINS`,  `STARTS_WITH`
         * Consulte [Consulta de muestra: todas las personas que no tienen un nombre de &quot;Trabajos&quot;](#sample-all-persons-not-jobs)
         * Consulte [Consulta de muestra: todas las aventuras en las que el `_path` comienza con un prefijo específico](#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply` : aplicar condiciones específicas; por ejemplo,   `AT_LEAST_ONCE`
         * Consulte [Muestra de consulta - Filtrar en una matriz con un elemento que debe producirse al menos una vez](#sample-array-item-occur-at-least-once)
      * `_ignoreCase` : para ignorar el caso al consultar
         * Consulte [Consulta de muestra: todas las ciudades con SAN en el nombre, independientemente del caso](#sample-all-cities-san-ignore-case)









* Se admiten los tipos de unión de GraphQL:

   * use `... on`
      * Consulte [Consulta de ejemplo para un fragmento de contenido de un modelo específico con una referencia de contenido](#sample-wknd-fragment-specific-model-content-reference)

## Consultas persistentes (almacenamiento en caché) {#persisted-queries-caching}

Después de preparar una consulta con una solicitud de POST, esta se puede ejecutar con una solicitud de GET que se puede almacenar en caché mediante cachés HTTP o una CDN.

Esto es necesario, ya que las consultas de POST generalmente no se almacenan en caché y si se utiliza la GET con la consulta como parámetro, existe un riesgo significativo de que el parámetro sea demasiado grande para los servicios HTTP e intermediarios.

Las consultas persistentes siempre deben utilizar el extremo relacionado con la [configuración de sitios adecuada](#graphql-aem-endpoint); para que puedan usar una o ambas:

* La configuración global y el punto final
La consulta tiene acceso a todos los modelos de fragmento de contenido.
* Configuraciones de sitios específicas y puntos de conexión
La creación de una consulta persistente para una configuración de sitios específica requiere un punto final específico para la configuración de sitios (para proporcionar acceso a los modelos de fragmentos de contenido relacionados).
Por ejemplo, para crear una consulta persistente específica para la configuración de WKND Sites, se debe crear de antemano una configuración de sitios específica de WKND y un extremo específico de WKND.

>[!NOTE]
>
>Consulte [Habilitar la funcionalidad de fragmento de contenido en el navegador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) para obtener más información.
>
>Las **Consultas de persistencia de GraphQL** deben habilitarse para la configuración de sitios adecuada.

Por ejemplo, si hay una consulta concreta llamada `my-query`, que utiliza un modelo `my-model` de la configuración de Sites `my-conf`:

* Puede crear una consulta utilizando el extremo específico `my-conf` y luego la consulta se guardará de la siguiente manera:
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* Puede crear la misma consulta utilizando el extremo `global` , pero la consulta se guardará de la siguiente manera:
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>Estas son dos consultas diferentes: se guardan en rutas diferentes.
>
>Simplemente utilizan el mismo modelo, pero a través de puntos de conexión diferentes.


Estos son los pasos necesarios para mantener una consulta determinada:

1. Prepare la consulta colocándola en la nueva dirección URL de extremo `/graphql/persist.json/<config>/<persisted-label>`.

   Por ejemplo, cree una consulta persistente:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. En este punto, compruebe la respuesta.

   Por ejemplo, compruebe si se ha realizado correctamente:

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. A continuación, puede reproducir la consulta persistente obteniendo la dirección URL `/graphql/execute.json/<shortPath>`.

   Por ejemplo, utilice la consulta persistente:

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Actualice una consulta persistente mediante POST a una ruta de consulta ya existente.

   Por ejemplo, utilice la consulta persistente:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. Cree una consulta sin formato ajustada.

   Por ejemplo:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Cree una consulta sencilla envolvente con control de caché.

   Por ejemplo:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Cree una consulta persistente con parámetros:

   Por ejemplo:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```

1. Ejecución de una consulta con parámetros.

   Por ejemplo:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

1. Para ejecutar la consulta en la publicación, es necesario replicar el árbol persistente relacionado

   * Uso de un POST para la replicación:

      ```xml
      $curl -X POST   http://localhost:4502/bin/replicate.json \
        -H 'authorization: Basic YWRtaW46YWRtaW4=' \
        -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
        -F cmd=activate
      ```

   * Uso de un paquete:
      1. Cree una nueva definición de paquete.
      1. Incluya la configuración (por ejemplo, `/conf/wknd/settings/graphql/persistentQueries`).
      1. Cree el paquete.
      1. Repita el paquete.
   * Uso de la herramienta de replicación/distribución.
      1. Vaya a la herramienta Distribución.
      1. Seleccione la activación del árbol para la configuración (por ejemplo, `/conf/wknd/settings/graphql/persistentQueries`).
   * Uso de un flujo de trabajo (mediante la configuración del iniciador del flujo de trabajo):
      1. Defina una regla de lanzador de flujo de trabajo para ejecutar un modelo de flujo de trabajo que duplique la configuración en diferentes eventos (por ejemplo, crear, modificar, entre otros).



1. Una vez que la configuración de la consulta está en la publicación, se aplican los mismos principios, solo con el extremo de publicación.

   >[!NOTE]
   >
   >Para el acceso anónimo, el sistema supone que la ACL permite que &quot;todos&quot; tengan acceso a la configuración de la consulta.
   >
   >Si no es así, no podrá ejecutarse.

   >[!NOTE]
   >
   >Debe codificarse cualquier punto y coma (&quot;;&quot;) en las direcciones URL.
   >
   >Por ejemplo, como en la solicitud para ejecutar una consulta persistente:
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

## Consulta del extremo de GraphQL desde un sitio web externo {#query-graphql-endpoint-from-external-website}

Para acceder al extremo de GraphQL desde un sitio web externo, debe configurar:

* [Filtro CORS](#cors-filter)
* [Filtro de referente](#referrer-filter)

### Filtro CORS {#cors-filter}

>[!NOTE]
>
>Para obtener una descripción detallada de la política de uso compartido de recursos CORS en AEM, consulte [Comprender el uso compartido de recursos de origen cruzado (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors)).

Para acceder al extremo de GraphQL, se debe configurar una directiva CORS en el repositorio Git del cliente. Para ello, agregue un archivo de configuración OSGi CORS apropiado para los puntos de conexión deseados.

Esta configuración debe especificar un origen de sitio web de confianza `alloworigin` o `alloworiginregexp` para el que se debe conceder acceso.

Por ejemplo, para conceder acceso al extremo de GraphQL y al extremo de consultas persistentes para `https://my.domain` puede utilizar:

```xml
{
  "supportscredentials":true,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/_cq_graphql/global/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

Si ha configurado una ruta mnemónica para el extremo, también puede utilizarla en `allowedpaths`.

### Filtro de referente {#referrer-filter}

Además de la configuración de CORS, se debe configurar un filtro de referente para permitir el acceso desde hosts de terceros.

Para ello, agregue un archivo de configuración de OSGi Referrer Filter apropiado que:

* especifica un nombre de host de sitio web de confianza; `allow.hosts` o `allow.hosts.regexp`,
* concede acceso a este nombre de host.

Por ejemplo, para conceder acceso a solicitudes con el referente `my.domain` puede:

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>Sigue siendo responsabilidad del cliente:
>
>* solo conceder acceso a dominios de confianza
>* asegúrese de que no se expone ninguna información confidencial
>* no utilice una sintaxis comodín [*]; esto deshabilitará el acceso autenticado al extremo de GraphQL y también lo expondrá a todo el mundo.


>[!CAUTION]
>
>Todos los esquemas de GraphQL [](#schema-generation) (derivados de modelos de fragmento de contenido que han sido **Enabled**) se pueden leer a través del extremo de GraphQL.
>
>Esto significa que debe asegurarse de que no hay datos confidenciales disponibles, ya que podrían filtrarse de esta manera; por ejemplo, esto incluye información que podría estar presente como nombres de campo en la definición del modelo.

## Autenticación {#authentication}

Consulte [Autenticación para consultas de GraphQL remotas AEM fragmentos de contenido](/help/assets/content-fragments/graphql-authentication-content-fragments.md).

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## Preguntas frecuentes {#faqs}

Preguntas que han surgido:

1. **P**: &quot;*¿En qué se diferencia la API de GraphQL de la API de Query Builder AEM?*&quot;

   * **A**: &quot;*La API de AEM GraphQL ofrece control total sobre la salida JSON y es un estándar del sector para consultar contenido.
En adelante, AEM tiene previsto invertir en la API de AEM GraphQL.*&quot;

## Tutorial: Introducción a AEM sin encabezado y GraphQL {#tutorial}

¿Busca un tutorial práctico? Consulte el tutorial completo [Introducción a AEM sin encabezado y GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) que ilustra cómo crear y exponer contenido mediante las API de GraphQL de AEM y consumido por una aplicación externa, en un escenario de CMS sin encabezado.
