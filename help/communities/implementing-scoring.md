---
title: Puntuación y distintivos de comunidades
seo-title: Puntuación y distintivos de comunidades
description: La puntuación y las insignias de AEM Communities le permiten identificar y premiar a los miembros de la comunidad
seo-description: La puntuación y las insignias de AEM Communities le permiten identificar y premiar a los miembros de la comunidad
uuid: d73683df-a413-4b3c-869c-67568bfdfcf6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ea033bb9-cb92-4c93-855f-8c902999378c
docset: aem65
tagskeywords: scoring, badging, badges, gamification
translation-type: tm+mt
source-git-commit: 2daf00f17058de8b901848fcf1128a5ee9770368
workflow-type: tm+mt
source-wordcount: '2884'
ht-degree: 2%

---


# Puntuación y distintivos de comunidades {#communities-scoring-and-badges}

## Información general {#overview}

La función de puntuación y distintivos de AEM Communities permite identificar y premiar a los miembros de la comunidad.

Los principales aspectos de la puntuación y las insignias son:

* [Asigne ](#assign-and-revoke-badges) distintivos para identificar la función de un miembro en la comunidad.

* [Concesión básica de ](#enable-scoring) distintivos a los miembros para fomentar su participación (cantidad de contenido creado).

* [Concesión avanzada de ](/help/communities/advanced.md) distintivos para identificar a los miembros como expertos (calidad del contenido creado).

**** Tenga en cuenta que la concesión de distintivos  [no está habilitada de forma predeterminada](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>La estructura de implementación visible en CRXDE Lite está sujeta a cambios una vez que la interfaz de usuario esté disponible.

## Insignias {#badges}

Las insignias se colocan bajo el nombre de un miembro para indicar su rol o su posición en la comunidad. Los distintivos pueden mostrarse como una imagen o como un nombre. Cuando se muestra como una imagen, el nombre se incluye como texto alternativo para la accesibilidad.

De forma predeterminada, los distintivos se encuentran en el repositorio en

* `/libs/settings/community/badging/images`

Si se almacenan en una ubicación diferente, todos deben leerlos accesibles.

Los distintivos se diferencian en UGC en cuanto a si fueron asignados o ganados según las reglas. Actualmente, las insignias asignadas aparecen como texto y las insignias obtenidas aparecen como imágenes.

### Interfaz de usuario de administración de distintivos {#badge-management-ui}

La consola Communities [Badges](/help/communities/badges.md) permite agregar distintivos personalizados que se pueden mostrar para un miembro cuando se ganan (se otorgan) o cuando asumen un rol específico en la comunidad (se asignan).

### Distintivos asignados {#assigned-badges}

Un administrador asigna las insignias basadas en roles a los miembros de la comunidad según su función en la comunidad.

Los distintivos asignados (y adjudicados) se almacenan en el [SRP](/help/communities/srp.md) seleccionado y no son directamente accesibles. Hasta que haya una GUI disponible, el único medio para asignar distintivos basados en roles es hacerlo con código o cURL. Para obtener instrucciones sobre cURL, consulte la sección titulada [Asignar y revocar distintivos](#assign-and-revoke-badges).

En la versión se incluyen tres distintivos basados en funciones:

* **moderador**

   `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **administrador de grupos**

   `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **miembro privilegiado**

   `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

   ![distintivos asignados](assets/assigned-badges.png)

### Distintivos otorgados {#awarded-badges}

El servicio de puntaje otorga insignias basadas en premios a los miembros de la comunidad según las reglas aplicadas a su actividad en la comunidad.

Para que las insignias aparezcan como recompensa por la actividad, hay dos cosas que deben suceder:

* La identificación debe estar [habilitada](#enableforcomponent) para el componente de la función.
* Las reglas de puntuación y de identificación deben [aplicarse](#applytopage) a la página (o antecesor) en la que se coloca el componente.

En la versión se incluyen tres distintivos basados en premios:

* **oro**

   `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **silver**

   `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **bronce**

   `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   ![galardonadas](assets/awarded-badges.png)

>[!NOTE]
>
>Las reglas de puntuación se pueden configurar para asignar puntos negativos para anuncios marcados como inapropiados y, por lo tanto, afectar al valor de puntuación. Sin embargo, una vez obtenido un distintivo, no se eliminará automáticamente debido a la reducción de puntos de puntuación o a los cambios en las reglas de puntuación.
>
>Las insignias otorgadas pueden ser revocadas de la misma manera que las insignias asignadas. Consulte la sección [Asignar y revocar distintivos](#assign-and-revoke-badges). Las futuras mejoras incluirán una interfaz de usuario para administrar las insignias de los miembros.

### Distintivos personalizados {#custom-badges}

Los distintivos personalizados se pueden instalar mediante la consola [Badges](/help/communities/badges.md) y se pueden asignar o especificar en las reglas de distintivo.

Cuando se instalan desde la consola Insignias, los distintivos personalizados se replican automáticamente en el entorno de publicación.

## Habilitar puntuación {#enable-scoring}

La puntuación no está habilitada de forma predeterminada. Los pasos básicos para configurar y habilitar la puntuación y la concesión de insignias son:

* Identifique las reglas para obtener puntos ([reglas de puntuación](#scoring-rules)).
* Para los puntos acumulados por reglas de puntuación, asigne [distintivos](#badges) ([reglas de identificación](#badging-rules)).

* [Aplique las reglas de puntuación y de identificación a un sitio](#apply-rules-to-content) de la comunidad.
* [Habilite el distintivo para las funciones](#enable-badges-for-component) de la comunidad.

Consulte la sección [Prueba rápida](#quick-test) para habilitar la puntuación para un sitio de la comunidad mediante las reglas de puntuación y marca predeterminadas para los foros y comentarios.

### Aplicar reglas al contenido {#apply-rules-to-content}

Para habilitar la puntuación y los distintivos, agregue las propiedades `scoringRules` y `badgingRules` a cualquier nodo del árbol de contenido del sitio.

Si el sitio ya está publicado, después de aplicar todas las reglas y activar los componentes, vuelva a publicar el sitio.

Las reglas que se aplican a un componente habilitado para distintivos son las del nodo actual o su antecesor.

Si el nodo es de tipo `cq:Page` (recomendado), con CRXDE|Lite, agregue las propiedades a su nodo `jcr:content`.

| **Propiedad** | **Tipo** | **Descripción** |
|---|---|---|
| badgingRules | Cadena | una lista de matriz de [reglas de identificación](#badging-rules) |
| scoringRules | Cadena | una lista de matriz de [reglas de puntuación](#scoring-rules) |

>[!NOTE]
>
>Si una regla de puntuación parece no tener ningún efecto en la concesión de distintivos, asegúrese de que la propiedad scoringRules de la regla de puntuación no haya bloqueado la regla de puntuación. Consulte la sección titulada [Reglas de Badging](#badging-rules).

### Habilitar distintivos para el componente {#enable-badges-for-component}

Las reglas de puntuación y de clasificación solo se aplican a las instancias de componentes que han habilitado la identificación mediante la edición de la configuración de componentes en [modo de creación](/help/communities/author-communities.md).

Una propiedad booleana, `allowBadges`, habilita o deshabilita la visualización de distintivos para una instancia de componente. Se puede configurar en el [cuadro de diálogo de edición de componentes](/help/communities/author-communities.md) para los componentes forum, QnA y comment mediante una casilla de verificación rotulada **Display Badges**.

#### Ejemplo: allowBadges para la instancia del componente Foro {#example-allowbadges-for-forum-component-instance}

![enable-badges-component](assets/enable-badges-component.png)

>[!NOTE]
>
>Cualquier componente se puede superponer para mostrar distintivos mediante el código HBS que se encuentra en los foros, el control de calidad y los comentarios como ejemplo.

## Reglas de puntuación {#scoring-rules}

Las reglas de puntuación son la base de la puntuación con el fin de otorgar distintivos.

Muy sencillamente, cada regla de puntuación es una lista de una o más subreglas. Las reglas de puntuación se aplican al contenido del sitio de la comunidad para identificar las reglas que se aplicarán cuando los distintivos estén habilitados.

Las reglas de puntuación se heredan pero no son aditivas. Por ejemplo:

* Si page2 contiene la regla de puntuación2 y su antecesor page1 contiene la regla de puntuación1.
* Una acción en un componente page2 invocará tanto rule1 como rule2.
* Si ambas reglas contienen subreglas aplicables para el mismo `topic/verb`:

   * Solo la subregla de la regla 2 afectará la puntuación.
   * Las puntuaciones de ambas subreglas no se suman.

Cuando hay más de una regla de puntuación, las puntuaciones se mantienen por separado para cada regla.

Las reglas de puntuación son nodos de tipo `cq:Page` con propiedades en su nodo `jcr:content` que especifican la lista de subreglas que la definen.

Las puntuaciones se almacenan en SRP.

>[!NOTE]
>
>Práctica recomendada: asigne un nombre exclusivo a cada regla de puntuación.
>
>Los nombres de las reglas de puntuación deben ser únicos globalmente; no deben terminar con el mismo nombre.
>
>Un ejemplo de lo que *no* debe hacer:
>
>/libs/settings/community/scoring/rules/site1/forums-scoring
>/libs/settings/community/scoring/rules/site2/forums-scoring

### Subreglas de puntuación {#scoring-sub-rules}

Las subreglas de puntuación contienen las propiedades que detallan los valores para participar en la comunidad.

Cada subregla de puntuación identifica:

* ¿Qué actividades se rastrean?
* ¿Qué función de comunidad específica está involucrada?
* ¿Cuántos puntos se conceden?

De forma predeterminada, los puntos se otorgan al miembro que realiza la acción, a menos que la subregla especifique el propietario del contenido como receptor de los puntos ( `forOwner`).

Cada subregla puede incluirse en una o varias reglas de puntuación.

El nombre de la subregla suele seguir el patrón de utilizar un *sujeto*, *objeto* y *verbo*. Por ejemplo:

* miembro-comentario-crear
* miembro-recibo-voto

Las subreglas son nodos de tipo `cq:Page` con propiedades en su nodo `jcr:content`que especifican los [verbos y temas](#topics-and-verbs).

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
     <li>requerido; el verbo corresponde a una acción de evento</li>
     <li>debe haber al menos una propiedad verbo</li>
     <li>el verbo debe introducirse en MAYÚSCULAS</li>
     <li>puede haber varias propiedades de verbo, pero no duplicados</li>
     <li>el valor es la puntuación que se aplicará a este evento</li>
     <li>el valor puede ser positivo o negativo</li>
     <li>una lista de verbos admitidos en la versión se encuentra en la sección <a href="#topics-and-verbs">Temas y verbos</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>Cadena</td>
   <td>
    <ul>
     <li>opcional; restringe la subregla a los componentes de la comunidad identificados por los temas de evento</li>
     <li>si se especifica : el valor es una cadena de varios valores de temas de evento</li>
     <li>una lista de los temas de la versión se encuentra en la sección <a href="#topics-and-verbs">Temas y verbos</a></li>
     <li>el valor predeterminado es aplicar a todos los temas asociados con los verbos</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>Booleano</td>
   <td>
    <ul>
     <li>opcional; no es relevante cuando el miembro actúa con el contenido que posee</li>
     <li>si es true, aplique una puntuación al propietario del contenido en el que se actúa</li>
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

### Se incluyeron reglas de puntuación y subreglas {#included-scoring-rules-and-sub-rules}

En la versión se incluyen dos reglas de puntuación para la [Función de foro](/help/communities/functions.md#forum-function) (una para los componentes Foro y Comentarios de la función Foro):

1. /libs/settings/community/scoring/rules/comments-scoring

   * subRules[] =
/libs/settings/community/scoring/rules/sub-rules/miembro-comment-create
/libs/settings/community/scoring/rules/sub-rules/miembro-recibo-voto
/libs/settings/community/scoring/rules/sub-rules/miembro-dar-voto
/libs/settings/community/scoring/rules/sub-rules/miembro-es-moderado

1. /libs/settings/community/scoring/rules/forums-scoring

   * subRules[] =
/libs/settings/community/scoring/rules/sub-rules/miembro-forum-create
/libs/settings/community/scoring/rules/sub-rules/miembro-recibo-voto
/libs/settings/community/scoring/rules/sub-rules/miembro-dar-voto
/libs/settings/community/scoring/rules/sub-rules/miembro-es-moderado

**Notas:**

* Los nodos `rules` y `sub-rules` son de tipo cq:Page.

* `subRules` es un atributo de tipo [] Cadena en el  `jcr:content` nodo de la regla.

* `sub-rules` puede compartirse entre varias reglas de puntuación.
* `rules` debe estar ubicado en una ubicación de repositorio con permiso de lectura para todos.

   * Los nombres de las reglas deben ser únicos independientemente de la ubicación.

### Activación de reglas de puntuación personalizadas {#activating-custom-scoring-rules}

Los cambios o adiciones realizados en las reglas de puntuación o subreglas realizados en el entorno de creación deben instalarse en la publicación.

## Reglas de insignia {#badging-rules}

Las reglas de asignación de distintivos vinculan las reglas de puntuación a los distintivos especificando:

* Regla de puntuación
* Puntuación necesaria para que se le conceda una insignia específica

Las reglas de asignación de distintivos son nodos de tipo `cq:Page` con propiedades en su nodo `jcr:content` que correlacionan las reglas de puntuación con puntuaciones y distintivos.

Las reglas para el marcado consisten en una propiedad `thresholds` obligatoria que es una lista ordenada de puntuaciones asignadas a distintivos. Las puntuaciones deben ordenarse en valor creciente. Por ejemplo:

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * Se concede una insignia de bronce para ganar 1 punto.

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * Se otorga una insignia de plata cuando se acumulan 60 puntos.

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * Se otorga una insignia de oro cuando se acumulan 80 puntos.

Las reglas de asignación de distintivos están emparejadas con reglas de puntuación que determinan la acumulación de puntos. Consulte la sección titulada [Aplicar reglas al contenido](#apply-rules-to-content).

La propiedad `scoringRules` de una regla de marcado simplemente restringe qué reglas de puntuación se pueden emparejar con esa regla de marcado en particular.

>[!NOTE]
>
>Práctica recomendada: cree imágenes de distintivo únicas para cada sitio AEM.

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
   <td><em>(requerido)</em> Una cadena de varios valores del formulario 'number|path'
    <ul>
     <li>number = score</li>
     <li>| = el carácter de línea vertical (U+007C)</li>
     <li>path = ruta completa al recurso de imagen de distintivo</li>
    </ul> Las cadenas deben ordenarse de modo que los números aumenten en valor y no debería aparecer espacio en blanco entre el número y la ruta.<br /> Ejemplo de entrada:<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Cadena</td>
   <td><em>(opcional)</em> Identifica el motor de puntuación como "básico" o "avanzado". Si desea el motor de puntuación avanzado, consulte <a href="/help/communities/advanced.md">Puntuación avanzada y distintivos</a>. El valor predeterminado es "basic".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Cadena</td>
   <td>(<em>opcional</em>) Una cadena de varios valores para restringir la regla de identificación a los eventos de puntuación identificados por las reglas de puntuación</td>
  </tr>
 </tbody>
</table>

### Reglas de identificación incluidas {#included-badging-rules}

En la versión se incluyen dos reglas de identificación que corresponden a las [reglas de puntuación de los foros y comentarios](#includedscoringrules).

* `/libs/settings/community/badging/rules/comments-badging`

* `/libs/settings/community/badging/rules/forums-badging`

**Notas:**

* `rules` los nodos son del tipo cq:Page.
* `rules` debe estar ubicado en una ubicación de repositorio con permiso de lectura para todos.

   * Los nombres de las reglas deben ser únicos independientemente de la ubicación.

### Activación de reglas de identificación personalizadas {#activating-custom-badging-rules}

Cualquier cambio o adición que se realice en las reglas de marcado o en las imágenes realizadas en el entorno del autor debe instalarse en la publicación.

## Asignar y revocar distintivos {#assign-and-revoke-badges}

Los distintivos pueden asignarse a miembros mediante la consola [miembros](/help/communities/members.md#badges-tab) o mediante programación mediante comandos cURL.

Los siguientes comandos cURL muestran lo que es necesario para una solicitud HTTP para asignar y revocar distintivos. El formato básico es:

cURL -i -X POST -H *encabezado* -u *inicio de sesión* -F *operación* -F *distintivo* *miembro-perfil-url*

*header* = &quot;Accept:application/json&quot; encabezado personalizado para pasar al servidor (requerido)

*sign* = admin-id:password, por ejemplo: admin:admin

*operation* = &quot;:operation=social:assignBadge&quot; OR &quot;:operation=social:deleteBadge&quot;

*badge* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* = la ubicación del archivo de imagen del distintivo en el repositorio, por ejemplo: /libs/settings/community/badging/images/moderator/jcr:content/moderator.png

*miembro-perfil-url* = el punto final del perfil del miembro al publicar, por ejemplo: https://&lt;server>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>El *miembro-perfil-url*:
>
>* Puede hacer referencia a una instancia de autor si el [servicio de túnel](/help/communities/users.md#tunnel-service) está habilitado.
>* Puede ser un nombre oscuro y aleatorio; consulte [Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) con respecto al ID autorizado.


### Ejemplos: {#examples}

#### Asignar una insignia de moderador {#assign-a-moderator-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

#### Revocar una insignia de plata asignada {#revoke-an-assigned-silver-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:deleteBadge" -F "badgeContentPath=/libs/settings/community/badging/images/silver/jcr:content/silver.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

>[!NOTE]
>
>El uso de cURL para asignar y revocar insignias funciona para cualquier imagen de insignia, pero cuando se asignan en lugar de ganarse, se marcan como insignias asignadas y se gestionan en consecuencia.

## Puntuación y distintivos para componentes personalizados {#scoring-and-badges-for-custom-components}

Las reglas de puntuación y de distintivo se pueden crear para componentes personalizados asociando los temas de evento creados para el componente con verbos.

## Temas y verbos {#topics-and-verbs}

Cuando los miembros interactúan con las funciones de la comunidad, se envían eventos que pueden dar déclencheur a los oyentes asincrónicos, como las notificaciones y la puntuación.

La instancia de SocialEvent de un componente registra los eventos como `actions` que se producen para un `topic`. SocialEvent incluye un método para devolver un `verb` asociado a la acción. Existe una relación *n-1* entre `actions` y `verbs`.

Para los componentes de comunidades entregados, las tablas siguientes describen el `verbs` definido para cada `topic` disponible para su uso en [subreglas de puntuación](#scoring-sub-rules).

>[!NOTE]
>
>Una nueva propiedad booleana, `allowBadges`, habilita o deshabilita la visualización de distintivos para una instancia de componente. Se puede configurar en [cuadros de diálogo de edición de componentes](/help/communities/author-communities.md) actualizados mediante una casilla de verificación rotulada **Insignias de visualización**.

**[Calendario](/help/communities/calendar.md)**
ComponenteSocialEvent  `topic`= com/adobe/cq/social/calendar

| **Verbo** | **Descripción** |
|---|---|
| POST | miembro crea un evento de calendario |
| AÑADIR | comentarios de miembros en un evento de calendario |
| ACTUALIZAR | se edita el evento o comentario del calendario del miembro |
| ELIMINAR | se elimina el evento o comentario del calendario del miembro |

**[Comments](/help/communities/comments.md)**
ComponentSocialEvent  `topic`= com/adobe/cq/social/comment

| **Verbo** | **Descripción** |
|---|---|
| POST | miembro crea un comentario |
| AÑADIR | respuestas de los miembros al comentario |
| ACTUALIZAR | se edita el comentario del miembro |
| ELIMINAR | se elimina el comentario del miembro |

**[File Library](/help/communities/file-library.md)**
ComponentSocialEvent  `topic`= com/adobe/cq/social/fileLibrary

| **Verbo** | **Descripción** |
|---|---|
| POST | miembro crea una carpeta |
| ATTACH | miembro carga un archivo |
| ACTUALIZAR | Un miembro actualiza una carpeta o un archivo |
| ELIMINAR | elimina una carpeta o un archivo |

**[Foro](/help/communities/forum.md)**
ComponenteSocialEvent  `topic`= com/adobe/cq/social/forum

| **Verbo** | **Descripción** |
|---|---|
| POST | miembro crea un tema del foro |
| AÑADIR | respuestas de los miembros al tema del foro |
| ACTUALIZAR | se edita el tema o la respuesta del foro del miembro |
| ELIMINAR | se elimina el tema o la respuesta del foro del miembro |

**[Historial](/help/communities/blog-feature.md)**
ComponentSocialEvent  `topic`= com/adobe/cq/social/historial

| **Verbo** | **Descripción** |
|---|---|
| POST | miembro crea un artículo de blog |
| AÑADIR | comentarios de miembros en un artículo de blog |
| ACTUALIZAR | se edita el artículo o comentario del blog del miembro |
| ELIMINAR | se elimina el artículo o comentario del blog del miembro |

**[QnA](/help/communities/working-with-qna.md)**
ComponentSocialEvent  `topic` = com/adobe/cq/social/qna

| **Verbo** | **Descripción** |
|---|---|
| POST | miembro crea una pregunta QnA |
| AÑADIR | miembro crea una respuesta de QnA |
| ACTUALIZAR | se edita la pregunta o la respuesta de control de calidad del miembro |
| SELECCIONAR | la respuesta del miembro está seleccionada |
| DESSELECCIONAR | se anula la selección de la respuesta del miembro |
| ELIMINAR | se elimina la pregunta o la respuesta de control de calidad del miembro |

**[Revisa](/help/communities/reviews.md)**
ComponentSocialEvent  `topic`= com/adobe/cq/social/review

| **Verbo** | **Descripción** |
|---|---|
| POST | miembro crea revisión |
| ACTUALIZAR | se edita la revisión del miembro |
| ELIMINAR | se elimina la revisión del miembro |

**[Rating](/help/communities/rating.md)**
ComponentSocialEvent  `topic`= com/adobe/cq/social/tally/rating

| **Verbo** | **Descripción** |
|---|---|
| AÑADIR CLASIFICACIÓN | el contenido del miembro se ha valorado |
| QUITAR CLASIFICACIÓN | el contenido del miembro se ha reducido |

**[Votación](/help/communities/voting.md)**
ComponentSocialEvent  `topic`= com/adobe/cq/social/tally/vote

| **Verbo** | **Descripción** |
|---|---|
| AÑADIR VOTACIÓN | el contenido de los miembros ha sido votado |
| ELIMINAR VOTACIÓN | el contenido de los miembros ha sido rechazado |

**Componentes habilitados para moderación**
SocialEvent  `topic`= com/adobe/cq/social/moderation

| **Verbo** | **Descripción** |
|---|---|
| DENEGAR | se deniega el contenido del miembro |
| INDICADOR COMO INAPROPIADO | se marca el contenido del miembro |
| DESALOG-AS-INAPROPIADO | el contenido del miembro no está marcado |
| ACEPTAR | el moderador aprueba el contenido del miembro |
| CERRAR | el miembro cierra los comentarios a las ediciones y las respuestas |
| ABRIR | miembro vuelve a abrir el comentario |

### Eventos de componentes personalizados {#custom-component-events}

Para un componente personalizado, se crea una instancia de SocialEvent para registrar los eventos del componente como `actions` que se producen para un `topic`.

Para admitir la puntuación, el evento de SocialEvent tendría que anular el método `getVerb()` para que se devuelva un `verb` apropiado para cada `action`. El `verb` devuelto para una acción puede ser uno de uso común (como `POST`) o uno especializado para el componente (como `ADD RATING`). Existe una relación *n-1* entre `actions` y `verbs`.

## Solución de problemas {#troubleshooting}

### Los distintivos no aparecen {#badges-are-not-appearing}

Si se han aplicado reglas de puntuación y de distintivo al contenido del sitio web, pero no se han otorgado distintivos para ninguna actividad, asegúrese de que se hayan habilitado las insignias para la instancia del componente.

Consulte [Habilitar distintivos para el componente](#enable-badges-for-component).

### La regla de puntuación no tiene efecto {#scoring-rule-has-no-effect}

Si se han aplicado reglas de puntuación y de identificación al contenido del sitio web, y se están adjudicando insignias para algunas acciones, pero no para otras, compruebe que la regla de insignia no haya restringido las reglas de puntuación a las que se aplica.

Consulte la propiedad `scoringRules` de [Reglas de identificación](#badging-rules).

### Tipo con distinción entre mayúsculas y minúsculas {#case-sensitive-typo}

La mayoría de las propiedades y los valores, especialmente los verbos, distinguen entre mayúsculas y minúsculas. Los verbos deben ser todos MAYÚSCULAS cuando se utilizan en una subregla de puntuación.

Si la función no funciona correctamente, asegúrese de que los datos se hayan introducido correctamente.

## Prueba rápida {#quick-test}

Es posible probar rápidamente la puntuación y la identificación mediante el sitio [Tutorial de introducción](/help/communities/getting-started.md) (participación):

* CRXDE Lite de acceso al autor.
* Vaya a la página base:

   * /content/sites/engagement/es/jcr:content

* Añada la propiedad badgingRules:

   * **Nombre**: `badgingRules`
   * **Tipo**: `String`
   * Seleccione **Multi**
   * Seleccione **Añadir**
   * Escriba `/libs/settings/community/badging/rules/forums-badging`
   * Seleccione **+**
   * Escriba `/libs/settings/community/badging/rules/comments-badging`
   * Seleccione **Aceptar**

* Añada la propiedad scoringRules:

   * **Nombre**: `scoringRules`
   * **Tipo**: `String`
   * Seleccione **Multi**
   * Seleccione **Añadir**
   * Escriba `/libs/settings/community/scoring/rules/forums-scoring`
   * Seleccione **+**
   * Escriba `/libs/settings/community/scoring/rules/comments-scoring`
   * Seleccione **Aceptar**

* Seleccione **Guardar todo**.

![test-scoring-badging](assets/test-scoring-badging.png)

A continuación, asegúrese de que los componentes de foro y comentarios permiten que se muestren distintivos:

* De nuevo con CRXDE Lite.
* Vaya al componente de foro

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* Añada la propiedad booleana allowBadges, si es necesario, y asegúrese de que es verdadera.

   * **Nombre**: `allowBadges`
   * **Tipo**: `Boolean`
   * **Valor**:  `true`

![test-forum-component](assets/test-forum-component.png)

A continuación, [vuelva a publicar](/help/communities/sites-console.md#publishing-the-site) el sitio de comunidad.

Finalmente,

* Vaya al componente en la instancia de publicación.
* Inicie sesión como miembro de la comunidad (por ejemplo: weston.mccall@dodgit.com / contraseña).
* Publicar un nuevo tema del foro.
* La página debe actualizarse para que se muestre el distintivo.

   * Cierre la sesión e inicie sesión como otro miembro de la comunidad (por ejemplo: aaron.mcdonald@mailinator.com/password).

* Seleccione el foro.

Esto debería ganar al miembro de la comunidad una insignia de bronce visible con su publicación en el foro debido a que el primer umbral de la regla de identificación de foros es una puntuación de 1.

![bronzebadge](assets/bronzebadge.png)

## Información adicional {#additional-information}

Puede encontrar más información en la página [Esenciales de puntuación y distintivos](/help/communities/configure-scoring.md) para desarrolladores.

Para obtener información sobre el motor de puntuación avanzado, consulte [Puntuación avanzada y distintivos](/help/communities/advanced.md).

El Leaderboard configurable [component](/help/communities/enabling-leaderboard.md) y [function](/help/communities/functions.md#leaderboard-function) simplifica la visualización de los miembros y sus puntuaciones en un sitio de la comunidad.
