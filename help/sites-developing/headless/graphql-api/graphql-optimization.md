---
title: Optimización de consultas de GraphQL
description: Aprenda a optimizar las consultas de GraphQL al filtrar, paginar y ordenar los fragmentos de contenido en Adobe Experience Manager as a Cloud Service para la entrega de contenido sin encabezado.
source-git-commit: 1481d613783089046b44d4652d38f7b4b16acc4d
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 58%

---


# Optimización de consultas de GraphQL {#optimizing-graphql-queries}

>[!NOTE]
>
>Antes de aplicar estas recomendaciones de optimización, considere lo siguiente [Actualización de los fragmentos de contenido para paginación y ordenación en el filtrado de GraphQL](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md) para obtener el mejor rendimiento.

AEM En una instancia de con un número elevado de fragmentos de contenido que comparte el mismo modelo, las consultas de listas de GraphQL pueden resultar costosas (en términos de recursos).

La razón es porque *todo* los fragmentos que comparten un modelo que se utiliza en la consulta de GraphQL deben cargarse en la memoria. Hacerlo consume tiempo y memoria. El filtrado, que puede reducir el número de elementos en el conjunto de resultados (final), solo se puede aplicar **después** cargando todo el conjunto de resultados en la memoria.

Este proceso puede dar la impresión de que incluso los conjuntos de resultados pequeños (pueden) dar lugar a un mal rendimiento. Sin embargo, en realidad, la lentitud está causada por el tamaño del conjunto de resultados inicial, ya que debe manejarse internamente antes de aplicar el filtrado.

Para reducir los problemas de rendimiento y memoria, este conjunto de resultados inicial debe mantenerse lo más pequeño posible.

AEM proporciona dos métodos para optimizar las consultas de GraphQL:

* [Filtrado híbrido](#hybrid-filtering)
* [Paginación](#paging)

   * [Ordenación](#sorting) no está directamente relacionada con la optimización, pero sí con la paginación

Cada método tiene sus propios casos de uso y limitaciones. Este documento proporciona información sobre el filtrado y la paginación híbridos, con algunas [prácticas recomendadas](#best-practices) para optimizar las consultas de GraphQL.

## Filtrado híbrido {#hybrid-filtering}

El filtrado híbrido combina el filtrado de JCR con el filtrado de AEM.

Aplica un filtro de JCR (en forma de restricción de consulta) antes de cargar el conjunto de resultados en la memoria para el filtrado de AEM. Este proceso sirve para reducir el conjunto de resultados cargado en la memoria, ya que el filtro JCR elimina los resultados superfluos de antemano.

>[!NOTE]
>
>AEM Por motivos técnicos (por ejemplo, flexibilidad, anidación de fragmentos), no se puede delegar todo el filtrado a JCR.

Esta técnica mantiene la flexibilidad que proporcionan los filtros de GraphQL, al tiempo que delega la mayor parte posible del filtrado a JCR.

## Paginación {#paging}

GraphQL AEM en la admite dos tipos de paginación:

* [paginación basada en límite/desplazamiento](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#list-offset-limit)
Este tipo de paginación se utiliza para consultas de lista; estas consultas terminan con 
`List`; por ejemplo, `articleList`.
Para utilizarlo, debe proporcionar la posición del primer elemento que se va a devolver (la variable `offset`) y el número de elementos que se van a devolver (la variable `limit`, o tamaño de página).

* [paginación basada en cursor](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#paginated-first-after) (representado por `first`y `after`) Este tipo de paginación proporciona un ID único para cada elemento; también conocido como cursor.
En la consulta, se especifica el cursor del último elemento de la página anterior, además del tamaño de página (el número máximo de elementos que se van a devolver).

   Como la paginación basada en cursor no se ajusta a las estructuras de datos de las consultas basadas en listas, AEM ha introducido el tipo de consulta `Paginated`; por ejemplo, `articlePaginated`. Las estructuras de datos y los parámetros utilizados siguen la [Especificación de conexión del cursor de GraphQL](https://relay.dev/graphql/connections.htm).

   >[!NOTE]
   >
   >Actualmente, AEM admite la paginación de reenvío (utilizando los parámetros `after`/`first`).
   >
   >La paginación hacia atrás (utilizando los parámetros `before`/`last`) no es compatible.

## Ordenación {#sorting}

La ordenación solo puede ser eficaz si todos los criterios de ordenación están relacionados con fragmentos de nivel superior.

Si el orden de clasificación incluye uno o más campos que se encuentran en un fragmento anidado, todos los fragmentos que compartan el modelo de nivel superior deben cargarse en la memoria. Este flujo causa un impacto negativo en el rendimiento.

>[!NOTE]
>
>La ordenación en campos de nivel superior también tiene un impacto (aunque pequeño) en el rendimiento.

## Prácticas recomendadas {#best-practices}

El objetivo principal de todas las optimizaciones es reducir el conjunto de resultados inicial. Las prácticas recomendadas enumeradas aquí proporcionan formas de hacerlo. Pueden (y deben) combinarse.

### Filtrar solo por propiedades de nivel superior {#filter-top-level-properties-only}

Actualmente, el filtrado en el nivel JCR solo funciona para fragmentos de nivel superior.

Si un filtro se dirige a los campos de un fragmento anidado, AEM tiene que volver a cargar (en memoria) todos los fragmentos que comparten el modelo subyacente.

Aún puede optimizar estas consultas de GraphQL combinando expresiones de filtro en campos de fragmentos de nivel superior y en campos de fragmentos anidados con la variable [Operador AND](#logical-operations-in-filter-expressions).

### Uso de la estructura de contenido {#use-content-structure}

AEM En la práctica, se considera una buena práctica utilizar la estructura del repositorio para reducir el ámbito del contenido que se va a procesar.

Aplique este enfoque a las consultas de GraphQL aplicando un filtro en la variable `_path` del fragmento de nivel superior:

```graphql
{
  someList(filter: {
    _path: {
      _expressions: [ 
        {
          value: "/content/dam/some/sub/path/",
          _operator: STARTS_WITH
        }
      ]
    }
  }) {
    items {
      # ...
    }
  }
}
```

>[!NOTE]
>
>El final `/` en `value` es obligatorio para lograr el mejor rendimiento.

### Usar paginación {#use-paging}

También puede utilizar la paginación para reducir el conjunto de resultados inicial, sobre todo si las solicitudes no utilizan ningún filtro ni ordenación.

AEM Si filtra u ordena por fragmentos anidados, las consultas paginadas pueden seguir siendo lentas, ya que aún deben cargar cantidades mayores de fragmentos en la memoria. Por lo tanto, si combina filtrado y paginación, tenga en cuenta las reglas de filtrado (como se ha mencionado anteriormente).

Para la paginación, la ordenación es igualmente importante, ya que los resultados paginados siempre se ordenan, ya sea de forma explícita o implícita.

Si le interesa principalmente recuperar solo las primeras páginas, no hay ninguna diferencia significativa entre el uso de consultas `...List` o `...Paginated`. Sin embargo, si a la aplicación le interesa leer más de una o dos páginas, debe tener en cuenta la consulta `...Paginated`, ya que tiene un rendimiento notablemente mejor con las páginas posteriores.

### Operaciones lógicas en expresiones de filtro {#logical-operations-in-filter-expressions}

Si está filtrando por fragmentos anidados, aún puede aplicar el filtrado JCR proporcionando un filtro complementario en un campo de nivel superior que se combina con `AND` operador.

Un caso de uso típico es restringir el ámbito de la consulta utilizando un filtro en `_path` del fragmento de nivel superior. A continuación, filtre por campos adicionales que puedan estar en el nivel superior o en un fragmento anidado.

En este caso, las diferentes expresiones de filtro se combinarían con `AND`. Por lo tanto, el filtro de `_path` puede limitar de forma efectiva el conjunto de resultados inicial. El resto de filtros de los campos de nivel superior también pueden ayudar a reducir el conjunto de resultados inicial, siempre y cuando se combinen con `AND`.

Filtrar expresiones combinadas con `OR` no se puede optimizar si hay fragmentos anidados implicados. Tales `OR` las expresiones solo se pueden optimizar si *no* están implicados fragmentos anidados.

### Evitar filtrar los campos de texto multilínea {#avoid-filtering-multiline-textfields}

Los campos de un campo de texto multilínea (html, markdown, plaintext, json) no se pueden filtrar a través de una consulta JCR, ya que el contenido de estos campos debe calcularse sobre la marcha.

Si todavía debe filtrar en un campo de texto multilínea, considere la posibilidad de limitar el tamaño del conjunto de resultados inicial añadiendo expresiones de filtro adicionales y combinándolas con `AND`. Limitar el ámbito mediante el filtrado en el campo `_path` también es un buen enfoque.

### Evitar el filtrado en campos virtuales {#avoid-filtering-virtual-fields}

Los campos virtuales (la mayoría de los campos que comienzan por `_`) se calculan mientras se ejecuta una consulta de GraphQL y, por lo tanto, están fuera del ámbito del filtrado basado en JCR.

Una excepción importante es el campo `_path`, que se puede utilizar de forma eficaz para reducir el tamaño del conjunto de resultados inicial: si el contenido está estructurado en consecuencia (consulte [Uso de la estructura de contenido](#use-content-structure)).

### Filtrado: exclusiones {#filtering-exclusions}

Hay otras varias situaciones en las que una expresión de filtro no se puede evaluar en el nivel JCR (y, por lo tanto, debe evitarse para lograr el mejor rendimiento):

* Filtrado de expresiones en un valor `Float` que usa la opción de filtro `_sensitiveness`, y donde `_sensitiveness` se establece en cualquier elemento que no sea `0.0`.

* Filtrado de expresiones en un valor `String` mediante la opción de filtro `_ignoreCase`.

* Filtrado en valores `null`.

* Filtros en matrices con `_apply: ALL_OR_EMPTY`.

* Filtros en matrices con `_apply: INSTANCES`, `_instances: 0`.

* Filtrado de expresiones mediante el operador `CONTAINS_NOT`.

* Filtrado de expresiones en una `Calendar`, `Date`, o `Time` que utilizan la variable `NOT_AT` operador.
