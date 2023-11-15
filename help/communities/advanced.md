---
title: Puntuación avanzada y distintivos
description: Aprenda a configurar la puntuación avanzada para que pueda permitir la concesión de insignias e identificar a los miembros como expertos.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: d3bb6664-6c01-4bcf-840c-072fc491fc99
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 1%

---

# Puntuación avanzada y distintivos{#advanced-scoring-and-badges}

## Información general {#overview}

La puntuación avanzada permite la concesión de insignias para identificar a los miembros como expertos. La puntuación avanzada asigna puntos según la cantidad *y* calidad del contenido creado por un miembro, mientras que la puntuación básica asigna puntos en función de la cantidad de contenido creado.

Esta diferencia se debe al motor de puntuación utilizado para calcular las puntuaciones. El motor de puntuación básico aplica matemáticas simples. El motor de puntuación avanzado es un algoritmo adaptable que recompensa a los miembros activos que contribuyen con contenido relevante y valorado, deducido a través del procesamiento de lenguaje natural (PNL) de un tema.

Además de la relevancia del contenido, los algoritmos de puntuación tienen en cuenta las actividades de los miembros, como la votación y el porcentaje de respuestas. Aunque la puntuación básica los incluye cuantitativamente, la puntuación avanzada los utiliza de forma algorítmica.

Por lo tanto, el motor de puntuación avanzado requiere datos suficientes para que el análisis sea significativo. El umbral de logro para convertirse en un experto se reevalúa constantemente a medida que el algoritmo se ajusta continuamente al volumen y la calidad del contenido creado. También existe el concepto de *pudrirse* de los puestos más antiguos de un miembro. Si un miembro experto deja de participar en la materia en la que haya obtenido la condición de experto, en algún momento predeterminado (véase [configuración del motor de puntuación](#configurable-scoring-engine)) podrían perder su condición de expertos.

La configuración de la puntuación avanzada es prácticamente la misma que la puntuación básica:

* Las reglas básicas y avanzadas de puntuación e identificación son [aplicado al contenido](/help/communities/implementing-scoring.md#apply-rules-to-content) de la misma manera.

   * Se pueden aplicar reglas básicas y avanzadas de puntuación e insignias al mismo contenido.

* [Activación de distintivos para componentes](/help/communities/implementing-scoring.md#enable-badges-for-component) es genérico.

Las diferencias al configurar las reglas de puntuación e insignias son las siguientes:

* Motor de puntuación avanzado configurable
* Reglas de puntuación avanzadas:

   * `scoringType` establezca en `advanced`
   * Requiere `stopwords`

* Reglas avanzadas de distintivo:

   * `badgingType` establezca en `advanced`
   * `badgingLevels` establezca en **número de niveles de expertos que se van a otorgar**
   * Requiere `badgingPaths` matriz de distintivos en lugar de umbrales: la matriz asigna puntos a distintivos.

>[!NOTE]
>
>Para utilizar las funcionalidades avanzadas de puntuación e insignias, instale [Paquete de identificación de experto](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq610%2Fsocial%2Ffeaturepack%2Fcq-social-expert-identification-pkg).

## Motor de puntuación configurable {#configurable-scoring-engine}

El motor de puntuación avanzada proporciona una configuración OSGi con parámetros que afectan al algoritmo de puntuación avanzada.

![advanced-scoring-engine](assets/advanced-scoring-engine.png)

* **Ponderaciones de puntuación**

  Para un tema, especifique el verbo que debe tener la prioridad más alta al calcular la puntuación. Se pueden introducir uno o más temas, pero limitados a **un verbo por tema**. Consulte [Temas y verbos](/help/communities/implementing-scoring.md#topics-and-verbs).
Ingresado como `topic,verb` con la coma escapada. Por ejemplo:
  `/social/forum/hbs/social/forum\,ADD`
De forma predeterminada, se establece el verbo ADD para los componentes de foro y control de calidad.

* **Rango de puntuación**

  El rango de puntuaciones avanzadas se define con este valor (puntuación máxima) y 0 (puntuación más baja posible).

  El valor predeterminado es 100, de modo que el intervalo de puntuación es de 0 a 100.

* **Intervalo de tiempo de deterioro de entidad**

  Este parámetro representa el número de horas después de las cuales se deterioran todas las puntuaciones de entidad. Esto es necesario para no incluir contenido antiguo en las puntuaciones de un sitio de la comunidad.

  El valor predeterminado es de 216000 horas (~24 años).

* **Tasa de crecimiento de puntuación**
Esto especifica la puntuación entre el intervalo de puntuación 0, más allá del cual el crecimiento se ralentiza para limitar el número de expertos.

  El valor predeterminado es 50.

## Reglas de puntuación avanzadas {#advanced-scoring-rules}

En la puntuación básica, se conoce la cantidad necesaria para obtener una insignia.

En la puntuación avanzada, la cantidad necesaria se ajusta constantemente en función de la cantidad de datos de calidad dentro del sistema. La puntuación se calcula continuamente de forma similar a una curva de campana.

Si un miembro obtuvo una insignia de experto en un tema que ya no está activo, existe la posibilidad de que pierda su insignia debido a la decadencia con el tiempo.

### scoringType {#scoringtype}

Una regla de puntuación es un conjunto de subreglas de puntuación, cada una de las cuales declara el `scoringType`.

Para invocar el motor de puntuación avanzada, la variable `scoringType`debe establecerse en `advanced`.

Consulte [Subreglas de puntuación](/help/communities/implementing-scoring.md#scoring-sub-rules).

![advanced-scoring-type](assets/advanced-scoring-type.png)

### Palabras de parada {#stopwords}

El paquete de puntuación avanzada instala una carpeta de configuración que contiene un archivo de palabras de parada:

* `/libs/settings/community/scoring/configuration/stopwords`

El algoritmo de puntuación avanzada utiliza la lista de palabras del archivo de palabras de parada para identificar palabras comunes en inglés que se omiten durante el procesamiento de contenido.

No se espera que este archivo se modifique.

Si falta el archivo de palabras de parada, el motor de puntuación avanzada genera un error.

## Reglas de distintivos avanzadas {#advanced-badging-rules}

Las propiedades avanzadas de la regla de distintivos difieren de las siguientes [propiedades básicas de reglas de identificación](/help/communities/implementing-scoring.md#badging-rules).

En lugar de asociar puntos con una imagen de distintivo, solo es necesario identificar el número de expertos permitidos y la imagen de distintivo que se va a otorgar.

![advanced-badging-rules](assets/advanced-badging-rules.png)

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Tipo</th>
   <th>Valor  Descripción</th>
  </tr>
  <tr>
   <td>badgingPath</td>
   <td>Cadena[]</td>
   <td><em>(Obligatorio)</em> Una cadena de varios valores de imágenes de distintivo hasta el número de badgingLevels. Las rutas de imagen del distintivo deben ordenarse para que la primera se asigne al experto más alto. Si hay menos distintivos de los indicados por badgingLevels, el último distintivo de la matriz rellena el resto de la matriz. Ejemplo de entrada:<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>Largo</td>
   <td><em>(Opcional)</em> Especifica los niveles de experiencia que se van a otorgar. Por ejemplo, si debe haber un <code>expert </code>y un <code>almost expert</code> (dos distintivos), el valor debe establecerse en 2. badgingLevel debe corresponder al número de imágenes de distintivo relacionadas con expertos que aparecen en la propiedad badgingPath. El valor predeterminado es 1.</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Cadena</td>
   <td><em>(Obligatorio)</em> Identifica el motor de puntuación como "básico" o "avanzado". Configúrelo como "avanzado"; de lo contrario, el valor predeterminado es "básico".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Cadena[]</td>
   <td><em>(Opcional)</em> Una cadena de varios valores para restringir la regla de identificación a los eventos de puntuación identificados por una o más reglas de puntuación enumeradas.<br /> Ejemplo de entrada:<br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> El valor predeterminado es sin restricciones.</td>
  </tr>
 </tbody>
</table>

## Reglas incluidas e insignias {#included-rules-and-badge}

### Insignia incluida {#included-badge}

Esta versión beta incluye una insignia de experto basada en recompensas:

* `expert`

  `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![insignia de experto](assets/included-badge.png)

Para que el distintivo de experto aparezca como una recompensa por la actividad, asegúrese de que:

* `Badges` están habilitados para la función, como un componente de foro o control de calidad.

* Las reglas avanzadas de puntuación e identificación se aplican a la página (o antecesor) en la que se coloca el componente

Consulte la información básica de:

* [Activación de la insignia para un componente](/help/communities/implementing-scoring.md#enableforcomponent)
* [Aplicación de reglas](/help/communities/implementing-scoring.md#applytopage)

### Reglas y subreglas de puntuación incluidas {#included-scoring-rules-and-sub-rules}

La versión beta incluye dos reglas de puntuación avanzadas para [función de foro](/help/communities/functions.md#forum-function) (uno para los componentes foro y comentarios de la función foro):

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

* Ambos `rules` y `sub-rules` los nodos son del tipo `cq:Page`.
* `subRules` es un atributo de tipo cadena`[]` en la regla de `jcr:content` nodo.
* `sub-rules` pueden compartirse entre varias reglas de puntuación.
* `rules` debe estar en una ubicación de repositorio con permiso de lectura para todos.
* Los nombres de las reglas deben ser únicos independientemente de la ubicación.

### Reglas de distintivos incluidas {#included-badging-rules}

En la versión de se incluyen dos reglas de distintivo avanzadas que corresponden a las siguientes [reglas de puntuación de foros y comentarios avanzados](#included-scoring-rules-and-sub-rules).

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**Notas:**

* `rules` Los nodos son de tipo cq:Page.
* `rules` debe estar en una ubicación de repositorio con permiso de lectura para todos.
* Los nombres de las reglas deben ser únicos independientemente de la ubicación.
