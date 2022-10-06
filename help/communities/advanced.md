---
title: Puntuación avanzada y distintivos
seo-title: Advanced Scoring and Badges
description: Configuración de puntuación avanzada
seo-description: Setting up advanced scoring
uuid: 48caca57-43d3-4f2f-adf3-257428ba54d5
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: eb3d5c37-8097-46de-8c4f-804ea723f1c5
docset: aem65
role: Admin
exl-id: d3bb6664-6c01-4bcf-840c-072fc491fc99
source-git-commit: 07f8a9f629122102d30676926b225d57e542147d
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---

# Puntuación avanzada y distintivos{#advanced-scoring-and-badges}

## Información general {#overview}

La puntuación avanzada permite la asignación de distintivos para identificar a los miembros como expertos. La puntuación avanzada asigna puntos según la cantidad *y* calidad del contenido creado por un miembro, mientras que la puntuación básica asigna puntos basándose simplemente en la cantidad de contenido creado.

Esta diferencia se debe al motor de puntuación utilizado para calcular las puntuaciones. El motor de puntuación básico aplica matemáticas sencillas. El motor de puntuación avanzado es un algoritmo adaptable que premia a los miembros activos que contribuyen con contenido valioso y relevante, deducido a través del procesamiento de lenguajes naturales (NLP) de un tema.

Además de la relevancia del contenido, los algoritmos de puntuación tienen en cuenta las actividades de los miembros, como la votación y el porcentaje de respuestas. Aunque la puntuación básica los incluye cuantitativamente, la puntuación avanzada los utiliza de forma algorítmica.

Por lo tanto, el motor de puntuación avanzado requiere datos suficientes para que el análisis sea significativo. El umbral de logros para convertirse en un experto se reevalúa constantemente a medida que el algoritmo se ajusta continuamente al volumen y la calidad del contenido creado. También hay un concepto de *desintegración* de las publicaciones anteriores de un miembro. Si un miembro experto deja de participar en el asunto en el que ha adquirido la condición de experto, en algún punto predeterminado (véase [configuración del motor de puntuación](#configurable-scoring-engine)) podrían perder su condición de expertos.

La configuración de puntuación avanzada es prácticamente la misma que la puntuación básica:

* Las reglas básicas y avanzadas de puntuación y distintivo son [aplicado al contenido](/help/communities/implementing-scoring.md#apply-rules-to-content) de la misma manera.

   * Las reglas básicas y avanzadas de puntuación e insignia pueden aplicarse al mismo contenido.

* [Activación de distintivos para componentes](/help/communities/implementing-scoring.md#enable-badges-for-component) es genérico.

Las diferencias en la configuración de las reglas de puntuación y de distintivo son:

* Motor de puntuación avanzado configurable
* Reglas de puntuación avanzadas:

   * `scoringType` configure como `advanced`
   * Requiere `stopwords`

* Reglas de distintivo avanzadas:

   * `badgingType` configure como `advanced`
   * `badgingLevels` configure como **número de niveles de expertos a adjudicar**
   * Requiere `badgingPaths` matriz de distintivos en lugar de umbrales de asignación de matrices apunta a distintivos.

>[!NOTE]
>
>Para utilizar capacidades avanzadas de puntuación y distintivo, instale la variable [Paquete de identificación de expertos](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq610%2Fsocial%2Ffeaturepack%2Fcq-social-expert-identification-pkg).

## Motor de puntuación configurable {#configurable-scoring-engine}

El motor de puntuación avanzado proporciona una configuración OSGi con parámetros que afectan al algoritmo de puntuación avanzado.

![motor de puntuación avanzada](assets/advanced-scoring-engine.png)

* **Ponderaciones de valoración**

   Para un tema, especifique el verbo al que se le debe dar la prioridad más alta al calcular la puntuación. Se pueden introducir uno o más temas, pero limitados a **un verbo por tema**. Consulte [Temas y verbos](/help/communities/implementing-scoring.md#topics-and-verbs).
Introducido como `topic,verb` con la coma de escape. Por ejemplo:
   `/social/forum/hbs/social/forum\,ADD`
El valor predeterminado es el verbo ADD para los componentes QnA y forum .

* **Rango de puntuación**

   El rango de las puntuaciones avanzadas se define mediante este valor (máxima puntuación posible) y 0 (menor puntuación posible).

   El valor predeterminado es 100, por lo que el intervalo de puntuación es 0-100.

* **Intervalo de tiempo de descomposición de entidades**

   Este parámetro representa el número de horas después de las cuales todas las puntuaciones de entidad están atenuadas. Esto es necesario para no incluir contenido antiguo en las puntuaciones de un sitio de la comunidad.

   El valor predeterminado es 216000 horas (~24 años).

* **Tasa de crecimiento de la puntuación**
Esto especifica la puntuación entre 0 y el rango de puntuación, más allá del cual el crecimiento se ralentiza para limitar el número de expertos.

   El valor predeterminado es 50.

## Reglas de puntuación avanzadas {#advanced-scoring-rules}

En la puntuación básica, se conoce la cantidad necesaria para obtener un distintivo.

En la puntuación avanzada, la cantidad necesaria se ajusta constantemente en función de la cantidad de datos de calidad dentro del sistema. La puntuación se calcula continuamente de forma similar a una curva de campana.

Si un miembro obtuvo un distintivo de experto en un tema que ya no está activo, existe la posibilidad de que pierda su distintivo debido a la decadencia a lo largo del tiempo.

### scoringType {#scoringtype}

Una regla de puntuación es un conjunto de subreglas de puntuación, cada una de las cuales declara la variable `scoringType`.

Para invocar el motor de puntuación avanzado, la variable `scoringType`debe configurarse como `advanced`.

Consulte [Subreglas de puntuación](/help/communities/implementing-scoring.md#scoring-sub-rules).

![tipo de puntuación avanzada](assets/advanced-scoring-type.png)

### Palabras clave {#stopwords}

El paquete de puntuación avanzada instala una carpeta de configuración que contiene un archivo de palabras clave:

* `/libs/settings/community/scoring/configuration/stopwords`

El algoritmo de puntuación avanzado utiliza la lista de palabras incluidas en el archivo de palabras clave para identificar las palabras comunes en inglés que se omiten durante el procesamiento del contenido.

No se espera que este archivo se modifique.

Si falta el archivo de palabras clave, el motor de puntuación avanzado generará un error.

## Reglas de distintivo avanzadas {#advanced-badging-rules}

Las propiedades avanzadas de la regla de distintivo difieren de la variable [propiedades básicas de reglas de distintivo](/help/communities/implementing-scoring.md#badging-rules).

En lugar de asociar puntos con una imagen de distintivo, solo es necesario identificar el número de expertos permitidos y la imagen de distintivo a premiar.

![advanced-badging-rules](assets/advanced-badging-rules.png)

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Tipo</th>
   <th>Valor Descripción</th>
  </tr>
  <tr>
   <td>badgingPath</td>
   <td>Cadena[]</td>
   <td><em>(Obligatorio)</em> Una cadena de varios valores de imágenes de distintivo hasta el número de badgingLevels. Las rutas de la imagen del distintivo deben ordenarse para que la primera se conceda al experto más alto. Si hay menos distintivos de los indicados por badgingLevels, el último distintivo de la matriz rellena el resto de la matriz. Ejemplo de entrada:<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>Largo</td>
   <td><em>(Opcional)</em> Especifica los niveles de experiencia que se van a adjudicar. Por ejemplo, si debería haber un <code>expert </code>y <code>almost expert</code> (dos distintivos), el valor debe establecerse en 2. El badgingLevel debe corresponder con el número de imágenes de distintivo relacionadas con expertos que se enumeran para la propiedad badgingPath. El valor predeterminado es 1.</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Cadena</td>
   <td><em>(Obligatorio)</em> Identifica el motor de puntuación como "básico" o "avanzado". Establézcalo en "avanzado" de lo contrario el valor predeterminado es "básico".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Cadena[]</td>
   <td><em>(Opcional)</em> Una cadena de varios valores para restringir la regla de distintivo a los eventos de puntuación identificados por las reglas de puntuación enumeradas.<br /> Ejemplo de entrada:<br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> El valor predeterminado no es una restricción.</td>
  </tr>
 </tbody>
</table>

## Reglas y distintivo incluidos {#included-rules-and-badge}

### Distintivo incluido {#included-badge}

Esta versión beta incluye un distintivo de experto basado en premios:

* `expert`

   `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![licencia de experto](assets/included-badge.png)

Para que el distintivo de experto aparezca como una recompensa por la actividad, asegúrese de:

* `Badges` están activados para la función, como un foro o un componente QnA.

* Las reglas avanzadas de puntuación y distintivo se aplican a la página (o antecesor) en la que se coloca el componente

Consulte la información básica para:

* [Activación del distintivo para un componente](/help/communities/implementing-scoring.md#enableforcomponent)
* [Aplicación de reglas](/help/communities/implementing-scoring.md#applytopage)

### Reglas de puntuación y subreglas incluidas {#included-scoring-rules-and-sub-rules}

En la versión beta se incluyen dos reglas de puntuación avanzadas para la variable [función del foro](/help/communities/functions.md#forum-function) (una para los componentes de foro y comentarios de la función de foro):

1. `/libs/settings/community/scoring/rules/adv-comments-scoring`

   ```
   subRules[] =
   /libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
   /libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
   /libs/settings/community/scoring/rules/sub-rules/adv-voting-rule
   ```

1. `/libs/settings/community/scoring/rules/adv-forums-scoring`

   ```
   subRules[] =
   /libs/settings/community/scoring/rules/sub-rules/adv-forums-rule
   /libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
   /libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
   ```

**Notas:**

* Ambas `rules` y `sub-rules` los nodos son de tipo `cq:Page`.
* `subRules` es un atributo de tipo String`[]` en la regla `jcr:content` nodo .
* `sub-rules` puede compartirse entre distintas reglas de puntuación.
* `rules` debe estar ubicado en una ubicación de repositorio con permiso de lectura para todos.
* Los nombres de las reglas deben ser únicos independientemente de la ubicación.

### Reglas de distintivo incluidas {#included-badging-rules}

En la versión se incluyen dos reglas de distintivo avanzadas que corresponden a la variable [foros avanzados y reglas de puntuación de comentarios](#included-scoring-rules-and-sub-rules).

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**Notas:**

* `rules` los nodos son del tipo cq:Page.
* `rules` debe estar ubicado en una ubicación de repositorio con permiso de lectura para todos.
* Los nombres de las reglas deben ser únicos independientemente de la ubicación.
