---
title: Puntuación y distintivos de comunidades
seo-title: Puntuación y distintivos de comunidades
description: La puntuación y los distintivos de AEM Communities le permiten identificar y premiar a los miembros de la comunidad
seo-description: La puntuación y los distintivos de AEM Communities le permiten identificar y premiar a los miembros de la comunidad
uuid: d73683df-a413-4b3c-869c-67568bfdfcf6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ea033bb9-cb92-4c93-855f-8c902999378c
docset: aem65
tagskeywords: scoring, badging, badges, gamification
role: Admin
exl-id: 4aa857f7-d111-4548-8f03-f6d6c27acf51
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2884'
ht-degree: 2%

---

# Puntuación y distintivos de comunidades {#communities-scoring-and-badges}

## Información general {#overview}

La función de puntuación y distintivos de AEM Communities permite identificar y premiar a los miembros de la comunidad.

Los principales aspectos de la puntuación y las insignias son:

* [Asigne ](#assign-and-revoke-badges) distintivos para identificar la función de un miembro en la comunidad.

* [Adjudicación básica de ](#enable-scoring) distintivos a los miembros para fomentar su participación (cantidad de contenido creado).

* [Concesión avanzada de ](/help/communities/advanced.md) distintivos para identificar a los miembros como expertos (calidad del contenido creado).

**** Tenga en cuenta que la asignación de distintivos  [no está habilitada de forma predeterminada](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>La estructura de implementación visible en CRXDE Lite está sujeta a cambios una vez que la interfaz de usuario esté disponible.

## Insignias {#badges}

Los distintivos se colocan bajo el nombre de un miembro para indicar su papel o su posición en la comunidad. Los distintivos pueden mostrarse como una imagen o como un nombre. Cuando se muestra como una imagen, el nombre se incluye como texto alternativo para la accesibilidad.

De forma predeterminada, los distintivos se encuentran en el repositorio en

* `/libs/settings/community/badging/images`

Si se almacenan en una ubicación diferente, todos deben poder leerlos.

Los distintivos se diferencian en UGC en cuanto a si fueron asignados o ganados según las reglas. Actualmente, los distintivos asignados aparecen como texto y los distintivos obtenidos aparecen como una imagen.

### Interfaz de usuario de administración de distintivos {#badge-management-ui}

La consola [Distintivos](/help/communities/badges.md) de Communities permite agregar distintivos personalizados que se pueden mostrar para un miembro cuando se ganan (se conceden) o cuando asumen una función específica en la comunidad (se asignan).

### Distintivos asignados {#assigned-badges}

Un administrador asigna los distintivos basados en el rol a los miembros de la comunidad según su rol en la comunidad.

Los distintivos asignados (y adjudicados) se almacenan en el [SRP](/help/communities/srp.md) seleccionado y no son directamente accesibles. Hasta que una GUI esté disponible, el único medio para asignar distintivos basados en funciones es hacerlo con código o cURL. Para obtener instrucciones de cURL, consulte la sección titulada [Asignar y revocar distintivos](#assign-and-revoke-badges).

En la versión se incluyen tres distintivos basados en funciones:

* **moderador**

   `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **administrador de grupos**

   `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **miembro privilegiado**

   `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

   ![distintivos asignados](assets/assigned-badges.png)

### Distintivos asignados {#awarded-badges}

El servicio de puntuación concede distinciones basadas en premios a los miembros de la comunidad en función de las normas aplicadas a su actividad en la comunidad.

Para que los distintivos aparezcan como recompensa por la actividad, hay dos cosas que deben suceder:

* El distintivo debe estar [habilitado](#enableforcomponent) para el componente de la función.
* Las reglas de puntuación y asignación deben [aplicarse](#applytopage) a la página (o antecesor) en la que se coloca el componente.

En la versión se incluyen tres distintivos basados en premios:

* **oro**

   `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **silver**

   `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **bronce**

   `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   ![distintivos premiados](assets/awarded-badges.png)

>[!NOTE]
>
>Las reglas de puntuación se pueden configurar para asignar puntos negativos a los anuncios marcados como inapropiados y, por lo tanto, afectar al valor de puntuación. Sin embargo, una vez obtenido un distintivo, no se eliminará automáticamente debido a la reducción de puntos de puntuación o a los cambios en la regla de puntuación.
>
>Los distintivos otorgados pueden revocarse de la misma manera que los distintivos asignados. Consulte la sección [Asignar y revocar distintivos](#assign-and-revoke-badges). Las futuras mejoras incluirán una interfaz de usuario para administrar los distintivos de los miembros.

### Distintivos personalizados {#custom-badges}

Los distintivos personalizados se pueden instalar mediante la [consola Distintivos](/help/communities/badges.md) y se pueden asignar o especificar en las reglas de distintivo.

Cuando se instalan desde la consola Distintivos, los distintivos personalizados se replican automáticamente en el entorno de publicación.

## Habilitar puntuación {#enable-scoring}

La puntuación no está activada de forma predeterminada. Los pasos básicos para configurar y habilitar la puntuación y la concesión de distintivos son:

* Identificar reglas para ganar puntos ([reglas de puntuación](#scoring-rules)).
* Para los puntos acumulados por reglas de puntuación, asigne [distintivos](#badges) ([reglas de distintivo](#badging-rules)).

* [Aplique las reglas de puntuación e identificación a un sitio](#apply-rules-to-content) de la comunidad.
* [Habilite el distintivo para las funciones de la comunidad](#enable-badges-for-component).

Consulte la sección [Prueba rápida](#quick-test) para habilitar la puntuación para un sitio de la comunidad mediante las reglas de puntuación y distintivo predeterminadas para los foros y comentarios.

### Aplicar reglas al contenido {#apply-rules-to-content}

Para habilitar la puntuación y los distintivos, agregue las propiedades `scoringRules` y `badgingRules` a cualquier nodo del árbol de contenido del sitio.

Si el sitio ya está publicado, después de aplicar todas las reglas y habilitar los componentes, vuelva a publicar el sitio.

Las reglas que se aplican a un componente habilitado para distintivos son las del nodo actual o su antecesor.

Si el nodo es de tipo `cq:Page` (recomendado), usando CRXDE|Lite, agregue las propiedades a su nodo `jcr:content`.

| **Propiedad** | **Tipo** | **Descripción** |
|---|---|---|
| badgingRules | Cadena | una lista de matriz de [reglas de distintivo](#badging-rules) |
| scoringRules | Cadena | una lista de matriz de [reglas de puntuación](#scoring-rules) |

>[!NOTE]
>
>Si parece que una regla de puntuación no tiene ningún efecto en la asignación de distintivos, asegúrese de que la propiedad scoringRules de la regla de distintivo no haya bloqueado la regla de puntuación. Consulte la sección titulada [Reglas de distintivo](#badging-rules).

### Habilitar distintivos para componentes {#enable-badges-for-component}

Las reglas de puntuación y clasificación solo están en vigor para las instancias de componentes que han habilitado el distintivo editando la configuración de componentes en [modo de creación](/help/communities/author-communities.md).

Una propiedad booleana, `allowBadges`, habilita o deshabilita la visualización de distintivos para una instancia de componente. Se puede configurar en el [cuadro de diálogo de edición de componentes](/help/communities/author-communities.md) para componentes de foro, control de calidad y comentarios mediante una casilla de verificación denominada **Display Badges**.

#### Ejemplo : allowBadges para la instancia de componente Foro {#example-allowbadges-for-forum-component-instance}

![enable-badges-component](assets/enable-badges-component.png)

>[!NOTE]
>
>Se puede superponer cualquier componente para mostrar distintivos utilizando el código HBS que se encuentra en foros, control de calidad y comentarios como ejemplo.

## Reglas de puntuación {#scoring-rules}

Las reglas de puntuación son la base de la puntuación para la concesión de distintivos.

Muy simplemente, cada regla de puntuación es una lista de una o más subreglas. Las reglas de puntuación se aplican al contenido del sitio de la comunidad para identificar las reglas que se aplicarán cuando se habiliten los distintivos.

Las reglas de puntuación se heredan pero no son aditivas. Por ejemplo:

* Si la página 2 contiene la regla de puntuación 2 y su página antecesora 1 contiene la regla de puntuación 1.
* Una acción en un componente de página2 invocará tanto la regla1 como la regla2.
* Si ambas reglas contienen subreglas aplicables para el mismo `topic/verb`:

   * Solo la subregla de la regla 2 afectará a la puntuación.
   * Las puntuaciones de ambas subreglas no se suman.

Cuando hay más de una regla de puntuación, las puntuaciones se mantienen por separado para cada regla.

Las reglas de puntuación son nodos de tipo `cq:Page` con propiedades en su nodo `jcr:content` que especifican la lista de subreglas que la definen.

Las puntuaciones se almacenan en SRP.

>[!NOTE]
>
>Práctica recomendada: asigne un nombre único a cada regla de puntuación.
>
>Los nombres de las reglas de puntuación deben ser únicos a nivel global; no deben terminar con el mismo nombre.
>
>Un ejemplo de lo que *no* debe hacer:
>
>/libs/settings/community/scoring/rules/site1/forums-scoring
>/libs/settings/community/scoring/rules/site2/forums-scoring

### Subreglas de puntuación {#scoring-sub-rules}

Las subreglas de puntuación contienen las propiedades que detallan los valores para participar en la comunidad.

Cada subregla de puntuación identifica:

* ¿Qué actividades se están rastreando?
* ¿Qué función de comunidad específica está involucrada?
* ¿Cuántos puntos se conceden?

De forma predeterminada, se otorgan puntos al miembro que realiza la acción, a menos que la subregla especifique el propietario del contenido que recibe los puntos ( `forOwner`).

Cada subregla se puede incluir en una o más reglas de puntuación.

El nombre de la subregla suele seguir el patrón de uso de *subject* , *object* y *verb*. Por ejemplo:

* member-comment-create
* miembro-recibo-voto

Las subreglas son nodos de tipo `cq:Page` con propiedades en su nodo `jcr:content`que especifican los [verbos y temas](#topics-and-verbs) .

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Tipo</th>
   <th> Value Descripción</th>
  </tr>
  <tr>
   <td><i><code>VERB</code></i></td>
   <td>Largo</td>
   <td>
    <ul>
     <li>obligatorio; el verbo corresponde a una acción de evento</li>
     <li>debe haber al menos una propiedad verbo</li>
     <li>el verbo debe introducirse en MAYÚSCULAS</li>
     <li>puede haber varias propiedades de verbo, pero no duplicados</li>
     <li>el valor es la puntuación que se aplicará a este evento</li>
     <li>el valor puede ser positivo o negativo</li>
     <li>una lista de los verbos admitidos en la versión se encuentra en la sección <a href="#topics-and-verbs">Temas y verbos</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>Cadena</td>
   <td>
    <ul>
     <li>opcional; restringe la subregla a los componentes de la comunidad identificados por temas de evento</li>
     <li>si se especifica : es una cadena de varios valores de temas de evento</li>
     <li>una lista de temas de la versión se encuentra en la sección <a href="#topics-and-verbs">Temas y verbos</a></li>
     <li>el valor predeterminado es aplicar a todos los temas asociados con los verbos</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>Booleano</td>
   <td>
    <ul>
     <li>opcional; no es relevante cuando el miembro actúa sobre el contenido que posee</li>
     <li>si es true, aplique puntuación al propietario del contenido sobre el que se va a actuar</li>
     <li>si es false, aplique una puntuación a los miembros que realicen una acción</li>
     <li>el valor predeterminado es false</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>scoringType</code></td>
   <td>Cadena</td>
   <td>
    <ul>
     <li>opcional; identifica el motor de puntuación</li>
     <li>si es "básico", especifica el motor de puntuación en función de la cantidad
      <ul>
       <li>incluido en la versión</li>
      </ul> </li>
     <li>si "avanzado", especifica el motor de puntuación en función de la calidad y la cantidad
      <ul>
       <li>requiere un <a href="/help/communities/advanced.md">paquete adicional</a></li>
      </ul> </li>
     <li>el valor predeterminado es "basic"</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Reglas de puntuación y subreglas incluidas {#included-scoring-rules-and-sub-rules}

En la versión se incluyen dos reglas de puntuación para la [Función de foro](/help/communities/functions.md#forum-function) (una para los componentes Foro y Comentarios de la función Foro):

1. /libs/settings/community/scoring/rules/comments-scoring

   * subRules[] =
/libs/settings/community/scoring/rules/sub-rules/member-comment-create
/libs/settings/community/scoring/rules/sub-rules/member-receive-vote
/libs/settings/community/scoring/rules/sub-rules/member-to-vote
/libs/settings/community/scoring/rules/sub-rules/member-is-moderated

1. /libs/settings/community/scoring/rules/forums-scoring

   * subRules[] =
/libs/settings/community/scoring/rules/sub-rules/member-forum-create
/libs/settings/community/scoring/rules/sub-rules/member-receive-vote
/libs/settings/community/scoring/rules/sub-rules/member-to-vote
/libs/settings/community/scoring/rules/sub-rules/member-is-moderated

**Notas:**

* Los nodos `rules` y `sub-rules` son del tipo cq:Page.

* `subRules` es un atributo del tipo String [] en el  `jcr:content` nodo de la regla.

* `sub-rules` puede compartirse entre distintas reglas de puntuación.
* `rules` debe estar ubicado en una ubicación de repositorio con permiso de lectura para todos.

   * Los nombres de las reglas deben ser únicos independientemente de la ubicación.

### Activación de reglas de puntuación personalizadas {#activating-custom-scoring-rules}

Los cambios o adiciones realizados en las reglas de puntuación o en las subreglas realizadas en el entorno de creación deben instalarse en la publicación.

## Reglas de distintivo {#badging-rules}

Las reglas de distintivo vinculan las reglas de puntuación a los distintivos especificando:

* Regla de puntuación
* Puntuación necesaria para que se le conceda un distintivo específico

Las reglas de distintivo son nodos de tipo `cq:Page` con propiedades en su nodo `jcr:content` que correlacionan las reglas de puntuación con puntuaciones e insignias.

Las reglas para el distintivo constan de una propiedad `thresholds` obligatoria que es una lista ordenada de puntuaciones asignadas a distintivos. Las puntuaciones deben ordenarse en valor creciente. Por ejemplo:

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * Se otorga una insignia de bronce para ganar 1 punto.

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * Se otorga una insignia de plata cuando se acumulan 60 puntos.

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * Se otorga una insignia de oro cuando se acumulan 80 puntos.

Las reglas de distintivo están acompañadas de reglas de puntuación que determinan cómo se acumulan los puntos. Consulte la sección titulada [Aplicar reglas al contenido](#apply-rules-to-content).

La propiedad `scoringRules` de una regla de distintivo simplemente restringe qué reglas de puntuación se pueden emparejar con esa regla de distintivo en particular.

>[!NOTE]
>
>Práctica recomendada : cree imágenes de distintivo únicas para cada sitio AEM.

![badging-rule-configuration](assets/badging-rule-configuration.png)

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Tipo</th>
   <th>Valor Descripción</th>
  </tr>
  <tr>
   <td>umbrales</td>
   <td>Cadena</td>
   <td><em>(obligatorio)</em> Una cadena de varios valores del formulario 'number|path'
    <ul>
     <li>número = puntuación</li>
     <li>| = el gráfico de líneas verticales (U+007C)</li>
     <li>ruta = ruta completa al recurso de imagen de distintivo</li>
    </ul> Las cadenas deben ordenarse para que los números aumenten en valor y no aparezca ningún espacio en blanco entre el número y la ruta.<br /> Ejemplo de entrada :<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Cadena</td>
   <td><em>(opcional)</em> Identifica el motor de puntuación como "básico" o "avanzado". Si desea utilizar el motor de puntuación avanzado, consulte <a href="/help/communities/advanced.md">Puntuación avanzada y distintivos</a>. El valor predeterminado es "básico".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Cadena</td>
   <td>(<em>opcional</em>) Una cadena de varios valores para restringir la regla de distintivo a los eventos de puntuación identificados por las reglas de puntuación</td>
  </tr>
 </tbody>
</table>

### Reglas de distintivo incluidas {#included-badging-rules}

En la versión se incluyen dos reglas de distintivo que corresponden a las [Reglas de puntuación de foros y comentarios](#includedscoringrules).

* `/libs/settings/community/badging/rules/comments-badging`

* `/libs/settings/community/badging/rules/forums-badging`

**Notas:**

* `rules` los nodos son del tipo cq:Page.
* `rules` debe estar ubicado en una ubicación de repositorio con permiso de lectura para todos.

   * Los nombres de las reglas deben ser únicos independientemente de la ubicación.

### Activación de reglas de distintivo personalizadas {#activating-custom-badging-rules}

Los cambios o adiciones realizados en las reglas de distintivo o en las imágenes realizadas en el entorno de creación deben instalarse en la publicación.

## Asignar y revocar distintivos {#assign-and-revoke-badges}

Los distintivos se pueden asignar a miembros mediante la [consola de miembros](/help/communities/members.md#badges-tab) o mediante programación mediante comandos cURL.

Los siguientes comandos cURL muestran lo que es necesario para una solicitud HTTP para asignar y revocar distintivos. El formato básico es:

cURL -i -X POST -H *encabezado* -u *inicio de sesión* -F *operación* -F *distintivo* *perfil de miembro-url*

*header* = &quot;Accept:application/json&quot; encabezado personalizado para pasar al servidor (obligatorio)

*inicio de sesión* = id-administrador:contraseña, por ejemplo: admin:admin

*operation* = &quot;:operation=social:assignBadge&quot; O &quot;:operation=social:deleteBadge&quot;

*badge* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* = la ubicación del archivo de imagen del distintivo en el repositorio, por ejemplo: /libs/settings/community/badging/images/moderator/jcr:content/moderator.png

*member-profile-url* = el punto final del perfil del miembro en la publicación, por ejemplo: https://&lt;server>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>El *miembro-profile-url*:
>
>* Puede hacer referencia a una instancia de autor si el [Servicio de túnel](/help/communities/users.md#tunnel-service) está habilitado.
>* Puede ser un nombre aleatorio y oscuro; consulte [Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) con respecto al ID autorizado.


### Ejemplos: {#examples}

#### Asignar un distintivo de moderador {#assign-a-moderator-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

#### Revocar un distintivo de plata asignado {#revoke-an-assigned-silver-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:deleteBadge" -F "badgeContentPath=/libs/settings/community/badging/images/silver/jcr:content/silver.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

>[!NOTE]
>
>El uso de cURL para asignar y revocar distintivos funciona para cualquier imagen de distintivo, pero cuando se asignan en lugar de ganarse, se marcan como distintivos asignados y se gestionan según corresponda.

## Puntuación y distintivos para componentes personalizados {#scoring-and-badges-for-custom-components}

Se pueden crear reglas de puntuación y de distintivo para componentes personalizados al asociar los temas de evento creados para el componente con verbos.

## Temas y verbos {#topics-and-verbs}

Cuando los miembros interactúan con las funciones de las comunidades, se envían eventos que pueden almacenar en déclencheur a los oyentes asincrónicos, como notificaciones y puntuación.

La instancia SocialEvent de un componente registra los eventos como `actions` que se producen para un `topic`. SocialEvent incluye un método para devolver un `verb` asociado a la acción. Existe una relación *n-1* entre `actions` y `verbs`.

Para los componentes de comunidades entregados, las tablas siguientes describen el `verbs` definido para cada `topic` disponible para usar en [subreglas de puntuación](#scoring-sub-rules).

>[!NOTE]
>
>Una nueva propiedad booleana, `allowBadges`, habilita o deshabilita la visualización de distintivos para una instancia de componente. Se puede configurar en [cuadros de diálogo de edición de componentes](/help/communities/author-communities.md) actualizados mediante una casilla de verificación etiquetada **Mostrar distintivos**.

**[Calendario](/help/communities/calendar.md)**
ComponentSocialEvent  `topic`= com/adobe/cq/social/calendar

| **Verbo** | **Descripción** |
|---|---|
| POST | miembro crea un evento de calendario |
| AÑADIR | comentarios de miembro en un evento de calendario |
| ACTUALIZAR | se edita el evento o comentario de calendario del miembro |
| ELIMINAR | se elimina el evento o comentario del calendario del miembro |

**[Comentarios](/help/communities/comments.md)**
ComponentSocialEvent  `topic`= com/adobe/cq/social/comment

| **Verbo** | **Descripción** |
|---|---|
| POST | member crea un comentario |
| AÑADIR | respuestas de los miembros a comentarios |
| ACTUALIZAR | se edita el comentario del miembro |
| ELIMINAR | se suprime el comentario del miembro |

**[Biblioteca de archivos](/help/communities/file-library.md)**
ComponentSocialEvent  `topic`= com/adobe/cq/social/fileLibrary

| **Verbo** | **Descripción** |
|---|---|
| POST | member crea una carpeta |
| ADJUNTAR | el miembro carga un archivo |
| ACTUALIZAR | el miembro actualiza una carpeta o un archivo |
| ELIMINAR | un miembro elimina una carpeta o un archivo |

**[Forum](/help/communities/forum.md)**
ComponentSocialEvent  `topic`= com/adobe/cq/social/forum

| **Verbo** | **Descripción** |
|---|---|
| POST | miembro crea tema del foro |
| AÑADIR | respuestas de los miembros al tema del foro |
| ACTUALIZAR | se edita el tema o la respuesta del foro del miembro |
| ELIMINAR | se elimina el tema o la respuesta del foro del miembro |

**[Journal](/help/communities/blog-feature.md)**
ComponentSocialEvent  `topic`= com/adobe/cq/social/journal

| **Verbo** | **Descripción** |
|---|---|
| POST | miembro crea un artículo de blog |
| AÑADIR | comentarios de los miembros en un artículo de blog |
| ACTUALIZAR | se edita el artículo o comentario del blog del miembro |
| ELIMINAR | se elimina el artículo o comentario del blog del miembro |

**[QnA ComponentSocialEvent](/help/communities/working-with-qna.md)**
  `topic` = com/adobe/cq/social/qna

| **Verbo** | **Descripción** |
|---|---|
| POST | crea una pregunta QnA |
| AÑADIR | crea una respuesta de control de calidad |
| ACTUALIZAR | se edita la pregunta o respuesta de control de calidad de un miembro |
| SELECT | se selecciona la respuesta del miembro |
| UNSELECT | se anula la selección de la respuesta del miembro |
| ELIMINAR | se elimina la pregunta o respuesta de control de calidad de un miembro |

**[Revisiones de](/help/communities/reviews.md)**
ComponentSocialEvent  `topic`= com/adobe/cq/social/review

| **Verbo** | **Descripción** |
|---|---|
| POST | miembro crea revisión |
| ACTUALIZAR | se edita la revisión de miembro |
| ELIMINAR | se suprime la revisión de miembro |

**[Clasificación](/help/communities/rating.md)**
de ComponentSocialEvent  `topic`= com/adobe/cq/social/tally/rating

| **Verbo** | **Descripción** |
|---|---|
| AGREGAR CLASIFICACIÓN | el contenido del miembro se ha clasificado mejor |
| QUITAR CLASIFICACIÓN | el contenido del miembro se ha clasificado como inferior |

**[Votación](/help/communities/voting.md)**
ComponentSocialEvent  `topic`= com/adobe/cq/social/tally/vote

| **Verbo** | **Descripción** |
|---|---|
| AGREGAR VOTACIÓN | el contenido de los miembros ha sido votado |
| ELIMINAR VOTACIÓN | el contenido de los miembros ha sido rechazado |

**Componentes habilitados para**
moderaciónSocialEvent  `topic`= com/adobe/cq/social/moderation

| **Verbo** | **Descripción** |
|---|---|
| DENEGAR | se deniega el contenido del miembro |
| INDICADOR INAPROPIADO | el contenido del miembro está marcado |
| LAG-AS-INAPROPIADO | el contenido del miembro no está marcado |
| ACEPTAR | el contenido del miembro es aprobado por el moderador |
| CERRAR | el miembro cierra el comentario a ediciones y respuestas |
| ABRIR | el miembro vuelve a abrir el comentario |

### Eventos de componente personalizados {#custom-component-events}

Para un componente personalizado, se crea una instancia de SocialEvent para registrar los eventos del componente como `actions` que se producen para un `topic`.

Para admitir la puntuación, SocialEvent tendría que anular el método `getVerb()` para que se devuelva un `verb` apropiado para cada `action`. El `verb` devuelto para una acción puede ser de uso común (como `POST`) o uno especializado para el componente (como `ADD RATING`). Existe una relación *n-1* entre `actions` y `verbs`.

## Solución de problemas {#troubleshooting}

### Los distintivos no aparecen {#badges-are-not-appearing}

Si se han aplicado reglas de puntuación y de distintivo al contenido del sitio web, pero no se han concedido distintivos para ninguna actividad, asegúrese de que se hayan habilitado distintivos para la instancia de ese componente.

Consulte [Habilitar distintivos para el componente](#enable-badges-for-component).

### La regla de puntuación no tiene efecto {#scoring-rule-has-no-effect}

Si se han aplicado reglas de puntuación y de distintivo al contenido del sitio web y se están concediendo distintivos para algunas acciones, pero no para otras, compruebe que la regla de distintivo no haya restringido las reglas de puntuación a las que se aplica.

Consulte la propiedad `scoringRules` de [Badging Rules](#badging-rules).

### Tipo sensible a mayúsculas y minúsculas {#case-sensitive-typo}

La mayoría de las propiedades y los valores, especialmente los verbos, distinguen entre mayúsculas y minúsculas. Los verbos deben ser MAYÚSCULAS cuando se utilizan en una subregla de puntuación.

Si la función no funciona como se espera, asegúrese de que los datos se han introducido correctamente.

## Prueba rápida {#quick-test}

Es posible probar rápidamente la puntuación y el distintivo mediante el sitio [Tutorial de introducción](/help/communities/getting-started.md) (participación) :

* Acceso al CRXDE Lite en el autor.
* Vaya a la página base:

   * /content/sites/engagement/en/jcr:content

* Agregue la propiedad badgingRules :

   * **Nombre**: `badgingRules`
   * **Tipo**: `String`
   * Seleccione **Multi**
   * Seleccione **Add**
   * Escriba `/libs/settings/community/badging/rules/forums-badging`
   * Seleccione **+**
   * Escriba `/libs/settings/community/badging/rules/comments-badging`
   * Seleccione **OK**

* Agregue la propiedad scoringRules :

   * **Nombre**: `scoringRules`
   * **Tipo**: `String`
   * Seleccione **Multi**
   * Seleccione **Add**
   * Escriba `/libs/settings/community/scoring/rules/forums-scoring`
   * Seleccione **+**
   * Escriba `/libs/settings/community/scoring/rules/comments-scoring`
   * Seleccione **OK**

* Seleccione **Guardar todo**.

![asignación de puntuación de prueba](assets/test-scoring-badging.png)

A continuación, asegúrese de que los componentes de foro y comentarios permitan que se muestren distintivos:

* De nuevo con CRXDE Lite.
* Vaya al componente del foro

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* Agregue la propiedad booleana allowBadges, si es necesario, y asegúrese de que sea verdadera.

   * **Nombre**: `allowBadges`
   * **Tipo**: `Boolean`
   * **Valor**:  `true`

![test-forum-component](assets/test-forum-component.png)

A continuación, [vuelva a publicar](/help/communities/sites-console.md#publishing-the-site) el sitio de la comunidad.

Finalmente,

* Vaya al componente en la instancia de publicación.
* Inicie sesión como miembro de la comunidad (por ejemplo: weston.mccall@dodgit.com / contraseña).
* Publicar un nuevo tema de foro.
* La página debe actualizarse para que se muestre el distintivo.

   * Cierre sesión e inicie sesión como otro miembro de la comunidad (por ejemplo: aaron.mcdonald@mailinator.com/password).

* Seleccione el foro.

Esto debería ganar al miembro de la comunidad una insignia de bronce visible con su publicación en el foro debido a que el primer umbral de la regla de la insignia de foro es una puntuación de 1.

![bronzebadge](assets/bronzebadge.png)

## Información adicional {#additional-information}

Puede encontrar más información en la página [Scoring and Badges Essentials](/help/communities/configure-scoring.md) para desarrolladores.

Para obtener información sobre el motor de puntuación avanzado, consulte [Puntuación avanzada y distintivos](/help/communities/advanced.md).

El panel de control [component](/help/communities/enabling-leaderboard.md) y [function](/help/communities/functions.md#leaderboard-function) configurables simplifica la visualización de los miembros y sus puntuaciones en un sitio de la comunidad.
