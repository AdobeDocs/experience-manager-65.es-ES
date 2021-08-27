---
title: 'Aprender a utilizar GraphQL con AEM: contenido de muestra y consultas'
description: Aprenda a utilizar GraphQL con AEM para ofrecer contenido sin problemas explorando contenido de muestra y consultas.
feature: Content Fragments,GraphQL API
source-git-commit: 94145c6428f61e31f6784a3d6ea67aa8d81cedd6
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 6%

---

# Aprender a utilizar GraphQL con AEM: contenido de muestra y consultas {#learn-graphql-with-aem-sample-content-queries}

Aprenda a utilizar GraphQL con AEM para ofrecer contenido sin problemas explorando contenido de muestra y consultas.

>[!NOTE]
>
>Esta página debe leerse junto con:
>
>* [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)
>* [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)
>* [AEM API de GraphQL para su uso con fragmentos de contenido](/help/assets/content-fragments/graphql-api-content-fragments.md)


Para empezar a utilizar las consultas de GraphQL y cómo funcionan con AEM fragmentos de contenido, ayuda a ver algunos ejemplos prácticos.

Para ayudarle con esto, consulte:

* Una [estructura de fragmento de contenido de muestra](#content-fragment-structure-graphql)

* Y algunos [ejemplos de consultas de GraphQL](#graphql-sample-queries), basados en la estructura de fragmento de contenido de ejemplo (modelos de fragmento de contenido y fragmentos de contenido relacionados).


## GraphQL: consultas de ejemplo con la estructura de fragmento de contenido de ejemplo {#graphql-sample-queries-sample-content-fragment-structure}

Consulte estas consultas de ejemplo para ver ilustraciones de la creación de consultas, junto con resultados de ejemplo.

>[!NOTE]
>
>Según su instancia, puede acceder directamente a la interfaz [Graph *i* QL incluida con AEM API de GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface) para enviar y probar consultas.
>
>Por ejemplo: `http://localhost:4502/content/graphiql.html`

>[!NOTE]
>
>Las consultas de ejemplo se basan en la [Estructura de fragmento de contenido de ejemplo para su uso con GraphQL](#content-fragment-structure-graphql)

### Consulta de ejemplo: todos los esquemas y tipos de datos disponibles {#sample-all-schemes-datatypes}

Esto devolverá todos los `types` para todos los esquemas disponibles.

**Consulta de ejemplo**

```xml
{
  __schema {
    types {
      name
      description
    }
  }
}
```

**Resultado de muestra**

```xml
{
  "data": {
    "__schema": {
      "types": [
        {
          "name": "AdventureModel",
          "description": null
        },
        {
          "name": "AdventureModelArrayFilter",
          "description": null
        },
        {
          "name": "AdventureModelFilter",
          "description": null
        },
        {
          "name": "AdventureModelResult",
          "description": null
        },
        {
          "name": "AdventureModelResults",
          "description": null
        },
        {
          "name": "AllFragmentModels",
          "description": null
        },
        {
          "name": "ArchiveRef",
          "description": null
        },
        {
          "name": "ArrayMode",
          "description": null
        },
        {
          "name": "ArticleModel",
          "description": null
        },

...more results...

        {
          "name": "__EnumValue",
          "description": null
        },
        {
          "name": "__Field",
          "description": null
        },
        {
          "name": "__InputValue",
          "description": null
        },
        {
          "name": "__Schema",
          "description": "A GraphQL Introspection defines the capabilities of a GraphQL server. It exposes all available types and directives on the server, the entry points for query, mutation, and subscription operations."
        },
        {
          "name": "__Type",
          "description": null
        },
        {
          "name": "__TypeKind",
          "description": "An enum describing what kind of type a given __Type is"
        }
      ]
    }
  }
}
```

### Consulta de muestra: toda la información sobre todas las ciudades {#sample-all-information-all-cities}

Para recuperar toda la información sobre todas las ciudades, puede utilizar la consulta muy básica:
**Consulta de ejemplo**

```xml
{
  cityList {
    items
  }
}
```

Cuando se ejecuta, el sistema expande automáticamente la consulta para incluir todos los campos:

```xml
{
  cityList {
    items {
      _path
      name
      country
      population
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/basel",
          "name": "Basel",
          "country": "Switzerland",
          "population": 172258
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/bucharest",
          "name": "Bucharest",
          "country": "Romania",
          "population": 1821000
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-francisco",
          "name": "San Francisco",
          "country": "USA",
          "population": 883306
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-jose",
          "name": "San Jose",
          "country": "USA",
          "population": 1026350
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/stuttgart",
          "name": "Stuttgart",
          "country": "Germany",
          "population": 634830
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/zurich",
          "name": "Zurich",
          "country": "Switzerland",
          "population": 415367
        }
      ]
    }
  }
}
```

### Consulta de muestra: nombres de todas las ciudades {#sample-names-all-cities}

Se trata de una consulta directa para devolver el `name`de todas las entradas del esquema `city`.

**Consulta de ejemplo**

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Basel"
        },
        {
          "name": "Berlin"
        },
        {
          "name": "Bucharest"
        },
        {
          "name": "San Francisco"
        },
        {
          "name": "San Jose"
        },
        {
          "name": "Stuttgart"
        },
        {
          "name": "Zurich"
        }
      ]
    }
  }
}
```

### Consulta De Muestra: Un Solo Fragmento De Ciudad Específico {#sample-single-specific-city-fragment}

Esta es una consulta para devolver los detalles de una sola entrada de fragmento en una ubicación específica del repositorio.

**Consulta de ejemplo**

```xml
{
  cityByPath (_path: "/content/dam/sample-content-fragments/cities/berlin") {
    item {
      _path
      name
      country
      population
     categories
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "cityByPath": {
      "item": {
        "_path": "/content/dam/sample-content-fragments/cities/berlin",
        "name": "Berlin",
        "country": "Germany",
        "population": 3669491,
        "categories": [
          "city:capital",
          "city:emea"
        ]
      }
    }
  }
}
```

### Consulta de ejemplo: todas las ciudades con una variación con nombre {#sample-cities-named-variation}

Si crea una nueva variación, denominada &quot;Berlin Center&quot; (`berlin_centre`), para `city` Berlín, puede utilizar una consulta para devolver detalles de la variación.

**Consulta de ejemplo**

```xml
{
  cityList (variation: "berlin_center") {
    items {
      _path
      name
      country
      population
      categories
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491,
          "categories": [
            "city:capital",
            "city:emea"
          ]
        }
      ]
    }
  }
}
```

### Consulta de muestra: Detalles completos del CEO y los empleados de una empresa {#sample-full-details-company-ceos-employees}

Utilizando la estructura de los fragmentos anidados, esta consulta devuelve todos los detalles del CEO de una empresa y de todos sus empleados.

**Consulta de ejemplo**

```xml
query {
  companyList {
    items {
      name
      ceo {
        _path
        name
        firstName
        awards {
        id
          title
        }
      }
      employees {
       name
        firstName
       awards {
         id
          title
        }
      }
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Apple Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Marsh",
              "firstName": "Duke",
              "awards": []
            },
            {
              "name": "Caulfield",
              "firstName": "Max",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                }
              ]
            }
          ]
        },
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/adam-smith",
            "name": "Smith",
            "firstName": "Adam",
            "awards": []
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        },
        {
          "name": "NextStep Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe",
              "awards": []
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham",
              "awards": []
            }
          ]
        }
      ]
    }
  }
}
```

### Consulta de muestra: todas las personas que tienen el nombre &quot;Jobs&quot; o &quot;Smith&quot; {#sample-all-persons-jobs-smith}

Esto filtrará todos los `persons` para aquellos que tengan el nombre `Jobs`o `Smith`.

**Consulta de ejemplo**

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

**Resultados de muestra**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Jobs",
          "firstName": "Steve"
        }
      ]
    }
  }
}
```

### Consulta de muestra: todas las personas que no tienen un nombre de &quot;trabajos&quot; {#sample-all-persons-not-jobs}

Esto filtrará todos los `persons` para aquellos que tengan el nombre `Jobs`o `Smith`.

**Consulta de ejemplo**

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
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

**Resultados de muestra**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Lincoln",
          "firstName": "Abraham"
        },
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Slade",
          "firstName": "Cutter"
        },
        {
          "name": "Marsh",
          "firstName": "Duke"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Croft",
          "firstName": "Lara"
        },
        {
          "name": "Caulfield",
          "firstName": "Max"
        }
      ]
    }
  }
}
```

### Consulta de muestra: todas las aventuras cuyo `_path` comienza con un prefijo específico {#sample-wknd-all-adventures-cycling-path-filter}

Todos los `adventures` donde `_path` comienza con un prefijo específico (`/content/dam/wknd/en/adventures/cycling`).

**Consulta de ejemplo**

```xml
query {
  adventureList(
    filter: {
      _path: {
        _expressions: [
        {
          value: "/content/dam/wknd/en/adventures/cycling"
         _operator: STARTS_WITH
        }]
       }
    })
    {
    items {
      _path
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-southern-utah/cycling-southern-utah"
        },
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-tuscany/cycling-tuscany"
        }
      ]
    }
  }
}
```

### Consulta de muestra - Todas las ciudades situadas en Alemania o Suiza con una población entre 40000 y 999999 {#sample-all-cities-d-ch-population}

Aquí se filtra una combinación de campos. Se utiliza un `AND` (implícito) para seleccionar el rango `population`, mientras que se utiliza un `OR` (explícito) para seleccionar las ciudades requeridas.

**Consulta de ejemplo**

```xml
query {
  cityList(filter: {
    population: {
      _expressions: [
        {
          value: 400000
          _operator: GREATER_EQUAL
        }, {
          value: 1000000
          _operator: LOWER
        }
      ]
    },
    country: {
      _logOp: OR
      _expressions: [
        {
          value: "Germany"
        }, {
          value: "Switzerland"
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Stuttgart",
          "population": 634830,
          "country": "Germany"
        },
        {
          "name": "Zurich",
          "population": 415367,
          "country": "Switzerland"
        }
      ]
    }
  }
}
```

### Consulta de muestra: todas las ciudades con SAN en el nombre, independientemente del caso {#sample-all-cities-san-ignore-case}

Esta consulta interroga para todas las ciudades que tienen `SAN` en el nombre, independientemente del caso.

**Consulta de ejemplo**

```xml
query {
  cityList(filter: {
    name: {
      _expressions: [
        {
          value: "SAN"
          _operator: CONTAINS
          _ignoreCase: true
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA"
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA"
        }
      ]
    }
  }
}
```

### Consulta de muestra: filtre una matriz con un elemento que deba producirse al menos una vez {#sample-array-item-occur-at-least-once}

Esta consulta filtra en una matriz con un elemento (`city:na`) que debe producirse al menos una vez.

**Consulta de ejemplo**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          value: "city:na"
          _apply: AT_LEAST_ONCE
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA",
          "categories": [
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### Consulta de muestra: filtrar por un valor de matriz exacto {#sample-array-exact-value}

Esta consulta filtra con un valor de matriz exacto.

**Consulta de ejemplo**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          values: [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### Consulta de ejemplo para fragmentos de contenido anidados: todas las empresas que tienen al menos un empleado con el nombre &quot;Smith&quot; {#sample-companies-employee-smith}

Esta consulta ilustra el filtrado para cualquier `person` de `name` &quot;Smith&quot;, que devuelve información de entre dos fragmentos anidados: `company` y `employee`.

**Consulta de ejemplo**

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "NextStep Inc.",
          "ceo": {
            "name": "Jobs",
            "firstName": "Steve"
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe"
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham"
            }
          ]
        }
      ]
    }
  }
}
```

### Ejemplo de consulta para fragmentos de contenido anidados - Todas las empresas en las que todos los empleados han ganado el premio &quot;Gamestar&quot; {#sample-all-companies-employee-gamestar-award}

Esta consulta ilustra el filtrado entre tres fragmentos anidados: `company`, `employee` y `award`.

**Consulta de ejemplo**

```xml
query {
  companyList(filter: {
    employees: {
      _apply: ALL
      _match: {
        awards: {
          _match: {
            id: {
              _expressions: [
                {
                  value: "GS"
                  _operator:EQUALS
                }
              ]
            }
          }
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
        awards {
          id
          title
        }
      }
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "name": "Smith",
            "firstName": "Adam"
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        }
      ]
    }
  }
}
```

### Consulta de ejemplo para metadatos: enumera los metadatos de los premios titulados GB {#sample-metadata-awards-gb}

Esta consulta ilustra el filtrado entre tres fragmentos anidados: `company`, `employee` y `award`.

**Consulta de ejemplo**

```xml
query {
  awardList(filter: {
      id: {
        _expressions: [
          {
            value:"GB"
          }
        ]
    }
  }) {
    items {
      _metadata {
        stringMetadata {
          name,
          value
        }
      }
      id
      title
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "awardList": {
      "items": [
        {
          "_metadata": {
            "stringMetadata": [
              {
                "name": "title",
                "value": "Gameblitz Award"
              },
              {
                "name": "description",
                "value": ""
              }
            ]
          },
          "id": "GB",
          "title": "Gameblitz"
        }
      ]
    }
  }
}
```

## Ejemplo de consultas con el proyecto WKND {#sample-queries-using-wknd-project}

Estas consultas de ejemplo se basan en el proyecto WKND. Esto tiene:

* Modelos de fragmento de contenido disponibles en:
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* Fragmentos de contenido (y otro contenido) disponibles en:
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`

>[!NOTE]
>
>Como los resultados pueden ser extensos, no se reproducen aquí.

### Consulta de ejemplo para todos los fragmentos de contenido de un determinado modelo con las propiedades especificadas {#sample-wknd-all-model-properties}

Esta consulta de ejemplo interroga:

* para todos los fragmentos de contenido de tipo `article`
* con las propiedades `path`y `author`.

**Consulta de ejemplo**

```xml
{
  articleList {
    items {
      _path
      author
    }
  }
}
```

### Consulta de ejemplo para metadatos {#sample-wknd-metadata}

Esta consulta interroga:

* para todos los fragmentos de contenido de tipo `adventure`
* metadata

**Consulta de ejemplo**

```xml
{
  adventureList {
    items {
      _path,
      _metadata {
        stringMetadata {
          name,
          value
        }
        stringArrayMetadata {
          name,
          value
        }
        intMetadata {
          name,
          value
        }
        intArrayMetadata {
          name,
          value
        }
        floatMetadata {
          name,
          value
        }
        floatArrayMetadata {
          name,
          value
        }
        booleanMetadata {
          name,
          value
        }
        booleanArrayMetadata {
          name,
          value
        }
        calendarMetadata {
          name,
          value
        }
        calendarArrayMetadata {
          name,
          value
        }
      }
    }
  }
}
```

### Consulta de ejemplo para un solo fragmento de contenido de un modelo determinado {#sample-wknd-single-content-fragment-of-given-model}

Esta consulta de ejemplo interroga:

* para un solo fragmento de contenido de tipo `article` en una ruta específica
   * dentro de él, todos los formatos de contenido:
      * HTML
      * Markdown
      * Texto sin formato
      * JSON

**Consulta de ejemplo**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures") {
    item {
        _path
        author
        main {
          html
          markdown
          plaintext
          json
        }
    }
  }
}
```

### Consulta de ejemplo para un modelo de fragmento de contenido de un modelo {#sample-wknd-content-fragment-model-from-model}

Esta consulta de ejemplo interroga:

* para un solo fragmento de contenido
   * detalles del modelo de fragmento de contenido subyacente

**Consulta de ejemplo**

```xml
{
  adventureByPath(_path: "/content/dam/wknd/en/adventures/riverside-camping-australia/riverside-camping-australia") {
    item {
      _path
      adventureTitle
      _model {
        _path
        title
      }
    }
  }
}
```

### Consulta de ejemplo para un fragmento de contenido anidado: tipo de modelo único{#sample-wknd-nested-fragment-single-model}

Esta consulta interroga:

* para un solo fragmento de contenido de tipo `article` en una ruta específica
   * dentro de él, la ruta y el autor del fragmento al que se hace referencia (anidado)

>[!NOTE]
>
>El campo `referencearticle` tiene el tipo de datos `fragment-reference`.

**Consulta de ejemplo**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/skitouring/skitouring") {
    item {
        _path
        author
        referencearticle {
          _path
          author
      }
    }
  }
}
```

### Consulta de ejemplo para un fragmento de contenido anidado: tipo de modelo múltiple{#sample-wknd-nested-fragment-multiple-model}

Esta consulta interroga:

* para varios fragmentos de contenido de tipo `bookmark`
   * con referencias de fragmento a otros fragmentos de los tipos de modelo específicos `article` y `adventure`

>[!NOTE]
>
>El campo `fragments` tiene el tipo de datos `fragment-reference`, con los modelos `Article`, `Adventure` seleccionados.

```xml
{
  bookmarkList {
    items {
        fragments {
          ... on ArticleModel {
            _path
            author
          }
          ... on AdventureModel {
            _path
            adventureTitle
          }
        }
     }
  }
}
```

### Consulta de ejemplo para un fragmento de contenido de un modelo específico con referencias de contenido{#sample-wknd-fragment-specific-model-content-reference}

Esta consulta tiene dos sabores:

1. Para devolver todas las referencias de contenido.
1. Para devolver las referencias de contenido específicas del tipo `attachments`.

Estas consultas interrogan:

* para varios fragmentos de contenido de tipo `bookmark`
   * con referencias de contenido a otros fragmentos

#### Consulta de ejemplo para varios fragmentos de contenido con referencias de recuperación previa {#sample-wknd-multiple-fragments-prefetched-references}

La siguiente consulta devuelve todas las referencias de contenido utilizando `_references`:

```xml
{
  bookmarkList {
     _references {
         ... on ImageRef {
          _path
          type
          height
        }
        ... on MultimediaRef {
          _path
          type
          size
        }
        ... on DocumentRef {
          _path
          type
          author
        }
        ... on ArchiveRef {
          _path
          type
          format
        }
    }
    items {
        _path
    }
  }
}
```

#### Consulta de ejemplo para varios fragmentos de contenido con archivos adjuntos {#sample-wknd-multiple-fragments-attachments}

La siguiente consulta devuelve todos los `attachments`: un campo específico (subgrupo) de tipo `content-reference`:

>[!NOTE]
>
>El campo `attachments` tiene el tipo de datos `content-reference`, con varios formularios seleccionados.

```xml
{
  bookmarkList {
    items {
      attachments {
        ... on PageRef {
          _path
          type
        }
        ... on ImageRef {
          _path
          width
        }
        ... on MultimediaRef {
          _path
          size
        }
        ... on DocumentRef {
          _path
          author
        }
        ... on ArchiveRef {
          _path
          format
        }
      }
    }
  }
}
```

### Consulta de ejemplo para un solo fragmento de contenido con referencia en línea RTE {#sample-wknd-single-fragment-rte-inline-reference}

Esta consulta interroga:

* para un solo fragmento de contenido de tipo `bookmark` en una ruta específica
   * dentro de eso, referencias en línea RTE

>[!NOTE]
>
>Las referencias en línea RTE se hidratan en `_references`.

**Consulta de ejemplo**

```xml
{
  bookmarkByPath(_path: "/content/dam/wknd/en/bookmarks/skitouring") {
    item {
      _path
      description {
        json
      }
    }
    _references {
      ... on ArticleModel {
        _path
      }
      ... on AdventureModel {
        _path
      }
      ... on ImageRef {
        _path
      }
      ... on MultimediaRef {
        _path
      }
      ... on DocumentRef {
        _path
      }
      ... on ArchiveRef {
        _path
      }
    }
  }
}
```

### Consulta de ejemplo para una única variación de fragmento de contenido de un modelo determinado {#sample-wknd-single-fragment-given-model}

Esta consulta interroga:

* para un solo fragmento de contenido de tipo `article` en una ruta específica
   * dentro de él, los datos relacionados con la variación: `variation1`

**Consulta de ejemplo**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures", variation: "variation1") {
    item {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### Consulta de ejemplo para una variación con nombre de varios fragmentos de contenido de un modelo determinado {#sample-wknd-variation-multiple-fragment-given-model}

Esta consulta interroga:

* para fragmentos de contenido de tipo `article` con una variación específica: `variation1`

**Consulta de ejemplo**

```xml
{
  articleList (variation: "variation1") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### Consulta de ejemplo para varios fragmentos de contenido de una configuración regional determinada {#sample-wknd-multiple-fragments-given-locale}

Esta consulta interroga:

* para fragmentos de contenido de tipo `article` dentro de la configuración regional `fr`

**Consulta de ejemplo**

```xml
{ 
  articleList (_locale: "fr") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

## La estructura de fragmento de contenido de ejemplo (utilizada con GraphQL) {#content-fragment-structure-graphql}

Las consultas de ejemplo se basan en la siguiente estructura, que utiliza:

* Uno o más [Modelos de fragmento de contenido de muestra](#sample-content-fragment-models-schemas): forman la base de los esquemas de GraphQL

* [Ejemplo de ](#sample-content-fragments) fragmentos de contenido basados en los modelos anteriores

### Modelos de fragmento de contenido de muestra (esquemas) {#sample-content-fragment-models-schemas}

Para las consultas de ejemplo, utilizaremos los siguientes modelos de contenido y sus interrelaciones (referencias ->):

* [Empresa](#model-company)
->  [Persona](#model-person)
    ->  [Premio](#model-award)

* [Ciudad](#model-city)

#### Empresa {#model-company}

Los campos básicos que definen a la empresa son:

| Nombre del campo | Tipo de datos | Referencia |
|--- |--- |--- |
| Nombre de la empresa | Texto de línea única |  |
| CEO | Referencia de fragmento (único) | [Person](#model-person) |
| Empleados | Referencia de fragmento (multicampo) | [Persona](#model-person) |

#### Person {#model-person}

Los campos que definen a una persona, que también puede ser empleado:

| Nombre del campo | Tipo de datos | Referencia |
|--- |--- |--- |
| Nombre | Texto de línea única |  |
| Nombre | Texto de línea única |  |
| Premios | Referencia de fragmento (multicampo) | [Premio](#model-award) |

#### Premio {#model-award}

Los campos que definen un premio son:

| Nombre del campo | Tipo de datos | Referencia |
|--- |--- |--- |
| Acceso directo/ID | Texto de línea única |  |
| Título | Texto de línea única |  |

#### Ciudad {#model-city}

Los campos para definir una ciudad son:

| Nombre del campo | Tipo de datos | Referencia |
|--- |--- |--- |
| Nombre | Texto de línea única |  |
| País | Texto de línea única |  |
| Población | Número |  |
| Categorías | Etiquetas |  |

### Fragmentos de contenido de muestra {#sample-content-fragments}

Los siguientes fragmentos se utilizan para el modelo adecuado.

#### Empresa {#fragment-company}

| Nombre de la empresa | CEO | Empleados |
|--- |--- |--- |
| Apple | Steve Jobs | Marsh<br>Max Caulfield |
|  Little Pony Inc. | Adam Smith | Lara Croft<br>Esclavija de corte |
| NextStep Inc. | Steve Jobs | Joe Smith<br>Abe Lincoln |

#### Persona {#fragment-person}

| Nombre | Nombre | Premios |
|--- |--- |--- |
| Lincoln |  Abe |  |
| Smith | Adam |   |
| Enclavado |  Cortador |  Gameblitz<br>Gamestar |
| Marsh |  Duke |   |   |
|  Smith |  Joe |   |
| Recortar |  Lara | Gamestar |
| Caulfield |  Máximo |  Gameblitz |
|  Trabajos |  Steve |   |

#### Premio {#fragment-award}

| Acceso directo/ID | Título |
|--- |--- |
| GB | Gameblitz |
|  GS | Gamestar |
|  OSC | Oscar |

#### Ciudad {#fragment-city}

| Nombre | País | Población | Categorías |
|--- |--- |--- |--- |
| Basilea | Suiza | 172258 | ciudad:emea |
| Berlín | Alemania | 3669491 | city:capital<br>ciudad:emea |
| Bucarest | Rumanía | 1821000 |  city:capital<br>ciudad:emea |
| San Francisco |  EE. UU. |  883306 |  ciudad:playa<br>ciudad:na |
| San José |  EE. UU. |  102635 |  ciudad:na |
| Stuttgart |  Alemania |  634830 |  ciudad:emea |
|  Zúrich |  Suiza |  415367 |  city:capital<br>ciudad:emea |
