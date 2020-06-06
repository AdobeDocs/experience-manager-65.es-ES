---
title: Puntuación y distintivos avanzados
seo-title: Puntuación y distintivos avanzados
description: Configuración de puntuación avanzada
seo-description: Configuración de puntuación avanzada
uuid: 48caca57-43d3-4f2f-adf3-257428ba54d5
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: eb3d5c37-8097-46de-8c4f-804ea723f1c5
docset: aem65
translation-type: tm+mt
source-git-commit: fb7d2a3cebda86fa4d91d2ea89ae459fa4b86fa0
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---


# Puntuación y distintivos avanzados{#advanced-scoring-and-badges}

## Información general {#overview}

La puntuación avanzada permite la concesión de insignias para identificar a los miembros como expertos. La puntuación avanzada asigna puntos en función de la cantidad *y la calidad del* contenido creado por un miembro, mientras que la puntuación básica asigna puntos simplemente en función de la cantidad de contenido creado.

Esta diferencia se debe al motor de puntuación utilizado para calcular las puntuaciones. El motor de puntuación básico aplica matemáticas sencillas. El motor de puntuación avanzado es un algoritmo adaptable que recompensa a los miembros activos que contribuyen con contenido valioso y relevante, deducido a través del procesamiento del lenguaje natural (PNL) de un tema.

Además de la relevancia del contenido, los algoritmos de puntuación tienen en cuenta las actividades de los miembros, como la votación y el porcentaje de respuestas. Aunque la puntuación básica los incluye cuantitativamente, la puntuación avanzada los utiliza algorítmicamente.

Por lo tanto, el motor de puntuación avanzado requiere datos suficientes para que la análisis tenga sentido. El umbral de logro para convertirse en un experto se reevalúa constantemente a medida que el algoritmo se ajusta continuamente al volumen y la calidad del contenido creado. También hay un concepto de *decadencia* de los puestos más antiguos de un miembro. Si un miembro experto deja de participar en el tema en el que adquirió la condición de experto, en algún momento determinado (véase la configuración [del motor de](#configurable-scoring-engine)puntuación) podría perder su condición de experto.

Configurar la puntuación avanzada es prácticamente lo mismo que la puntuación básica:

* Las reglas de puntuación y de identificación básicas y avanzadas se [aplican al contenido](/help/communities/implementing-scoring.md#apply-rules-to-content) de la misma manera

   * Las reglas de puntuación y de identificación básicas y avanzadas pueden aplicarse al mismo contenido

* [La habilitación de distintivos para componentes](/help/communities/implementing-scoring.md#enable-badges-for-component) es genérica

Las diferencias en la configuración de las reglas de puntuación y de identificación son:

* Motor de puntuación avanzado configurable
* Reglas de puntuación avanzadas:

   * `scoringType` definir en `advanced`
   * requires `stopwords`

* Reglas de distintivo avanzadas:

   * `badgingType` definir en `advanced`
   * `badgingLevels` se establece en **número de niveles de expertos para adjudicar**
   * requiere `badgingPaths` una matriz de distintivos en lugar de umbrales, la asignación de matrices señala a los distintivos

>[!NOTE]
>
>Para utilizar las capacidades avanzadas de puntuación y de identificación, instale el paquete [Identificación de](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/social/cq-social-expert-identification-pkg)expertos.

## Motor de puntuación configurable {#configurable-scoring-engine}

El motor de puntuación avanzado proporciona una configuración OSGi con parámetros que afectan al algoritmo de puntuación avanzado.

![chlimage_1-139](assets/chlimage_1-139.png)

* **pesos de puntuación**

   Para un tema, especifique el verbo al que se debe dar la prioridad más alta al calcular la puntuación. Se pueden escribir uno o más temas, pero se pueden limitar a **un verbo por tema**. Consulte [Temas y Verbos](/help/communities/implementing-scoring.md#topics-and-verbs).
Introducido como `topic,verb` con la coma de escape. Por ejemplo:
   `/social/forum/hbs/social/forum\,ADD`
El valor predeterminado se establece en el verbo AÑADIR para los componentes QnA y forum.

* **Rango de puntuación**

   El rango de las puntuaciones avanzadas se define por este valor (máxima puntuación posible) y 0 (menor puntuación posible).

   El valor predeterminado es 100, por lo que el intervalo de puntuación es 0-100.

* **Intervalo de tiempo de decadencia de entidad**

   Este parámetro representa el número de horas después de las cuales todas las puntuaciones de entidad están desactivadas. Esto es necesario para no incluir contenido antiguo en las puntuaciones de un sitio de comunidad.

   El valor predeterminado es 216000 horas (~24 años).

* **Puntuación de la tasa** de crecimientoEspecifica la puntuación entre 0 y el rango de puntuación, más allá de la cual el crecimiento se desacelera para limitar el número de expertos.

   El valor predeterminado es 50.

## Reglas de puntuación avanzadas {#advanced-scoring-rules}

En la puntuación básica, se conoce la cantidad necesaria para obtener una insignia.

En la puntuación avanzada, la cantidad necesaria se ajusta constantemente en función de la cantidad de datos de calidad dentro del sistema. La puntuación se calcula continuamente de forma similar a una curva de campana.

Si un miembro obtuvo una insignia de experto en un tema que ya no está activo, existe la posibilidad de que pierda su insignia debido a la decadencia a lo largo del tiempo.

### scoringType {#scoringtype}

Una regla de puntuación es un conjunto de subreglas de puntuación, cada una de las cuales declara el `scoringType`.

Para invocar el motor de puntuación avanzado, el valor `scoringType`debe establecerse en `advanced`.

Consulte Subreglas [de puntuación](/help/communities/implementing-scoring.md#scoring-sub-rules).

![chlimage_1-140](assets/chlimage_1-140.png)

### Palabras clave {#stopwords}

El paquete de puntuación avanzada instala una carpeta de configuración que contiene un archivo de palabras clave:

* `/libs/settings/community/scoring/configuration/stopwords`

El algoritmo de puntuación avanzada utiliza la lista de palabras contenidas en el archivo de palabras clave para identificar las palabras comunes en inglés que se omiten durante el procesamiento del contenido.

No se espera que este archivo se modifique.

Si falta el archivo de palabras clave, el motor de puntuación avanzado generará un error.

## Reglas de distintivo avanzadas {#advanced-badging-rules}

Las propiedades avanzadas de la regla de identificación difieren de las propiedades [](/help/communities/implementing-scoring.md#badging-rules)básicas de la regla de identificación.

En lugar de asociar puntos con una imagen de insignia, solo es necesario identificar el número de expertos permitidos y la imagen de insignia que se va a otorgar.

![chlimage_1-141](assets/chlimage_1-141.png)

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Tipo</th>
   <th>Value Descripción</th>
  </tr>
  <tr>
   <td>badgingPath</td>
   <td>Cadena[]</td>
   <td><em>(Requerido)</em> Una cadena de varios valores de imágenes de distintivo hasta el número de badgingLevels. Las rutas de imagen de la insignia deben solicitarse para que la primera se conceda al experto más alto. Si hay menos distintivos de los indicados por badgingLevels, el último distintivo de la matriz rellena el resto de la matriz. Ejemplo de entrada:<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>Largo</td>
   <td><em>(Opcional)</em> Especifica los niveles de experiencia que se van a otorgar. Por ejemplo, si debe haber un <code>expert </code>y un <code>almost expert</code> (dos distintivos), el valor debe establecerse en 2. El badgingLevel debe coincidir con el número de imágenes de distintivo relacionadas con expertos que se muestran para la propiedad badgingPath. El valor predeterminado es 1.</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Cadena</td>
   <td><em>(Requerido)</em> Identifica el motor de puntuación como "básico" o "avanzado". Establecido en "avanzado", de lo contrario el valor predeterminado es "básico".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Cadena[]</td>
   <td><em>(Opcional)</em> Una cadena de varios valores para restringir la regla de identificación a eventos de puntuación identificados por las reglas de puntuación enumeradas.<br /> Ejemplo de entrada:<br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> El valor predeterminado no es una restricción.</td>
  </tr>
 </tbody>
</table>

## Reglas y distintivo incluidos {#included-rules-and-badge}

### Distintivo incluido {#included-badge}

En esta versión beta se incluye una insignia de experto basada en premios:

* `expert`

   `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![chlimage_1-142](assets/chlimage_1-142.png)

Para que la insignia de experto aparezca como recompensa por la actividad, asegúrese de:

* `Badges` están activadas para la función, como un foro o un componente QnA.

* Las reglas de puntuación y de identificación avanzadas se aplican a la página (o antecesor) en la que se coloca el componente

Consulte la información básica para:

* [Activación de la marca para un componente](/help/communities/implementing-scoring.md#enableforcomponent)
* [Aplicación de reglas](/help/communities/implementing-scoring.md#applytopage)

### Reglas y subreglas de puntuación incluidas {#included-scoring-rules-and-sub-rules}

En la versión beta se incluyen dos reglas de puntuación avanzadas para la función [de](/help/communities/functions.md#forum-function) foro (una para los componentes de foro y comentarios de la función de foro):

1. `/libs/settings/community/scoring/rules/adv-comments-scoring`

   * `subRules[] =
/libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule`

1. `/libs/settings/community/scoring/rules/adv-forums-scoring`

   * `subRules[] =
/libs/settings/community/scoring/rules/sub-rules/adv-forums-rule
/libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner`

**Notas:**

* Ambos `rules`y `sub-rules` los nodos son del tipo `cq:Page`

* `subRules`es un atributo de tipo String[] en el nodo `jcr:content` de la regla

* `sub-rules` pueden compartirse entre varias reglas de puntuación

* `rules`debe ubicarse en una ubicación de repositorio con permiso de lectura para todos

   * Los nombres de las reglas deben ser únicos independientemente de la ubicación

### Reglas de identificación incluidas {#included-badging-rules}

En la versión se incluyen dos reglas de identificación avanzadas que corresponden a los foros [avanzados y a las reglas](#included-scoring-rules-and-sub-rules)de puntuación de comentarios.

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**Notas:**

* `rules` los nodos son del tipo cq:Page
* `rules` debe ubicarse en una ubicación de repositorio con permiso de lectura para todos

   * Los nombres de las reglas deben ser únicos independientemente de la ubicación

