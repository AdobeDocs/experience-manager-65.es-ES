---
title: Moderar contenido de la comunidad
seo-title: Moderating Community Content
description: Conceptos y acciones de moderación
seo-description: Moderation concepts and actions
uuid: 5c991d3a-0037-4d78-8f91-bb62e44441fa
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6866d209-5789-4ef9-bc3c-d644d4fb4b1c
docset: aem65
role: Admin
exl-id: 22276580-e6bc-41c5-9ac3-e8f291f676b7
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 3%

---

# Moderar contenido de la comunidad {#moderating-community-content}

## Información general {#overview}

El contenido de la comunidad, también conocido como contenido generado por el usuario (UGC), se crea cuando un miembro (visitante del sitio conectado) publica contenido de un sitio de comunidad publicado mediante la interacción con uno de los siguientes componentes de la comunidad:

* [Blog](/help/communities/blog-feature.md): los miembros publican un artículo o comentario en el blog.
* [Calendario](/help/communities/calendar.md): los miembros publican un evento de calendario o un comentario.
* [Comentarios](/help/communities/comments.md): los miembros publican un comentario o responden a un comentario.

* [Foro](/help/communities/forum.md): los miembros publican un nuevo tema o responden a un tema.
* [Ideación](/help/communities/ideation-feature.md): los miembros publican una idea o comentario.
* [QnA](/help/communities/working-with-qna.md): los miembros crean una pregunta o responden a una pregunta.
* [Críticas](/help/communities/reviews.md): los miembros publican un comentario al clasificar un elemento.

La moderación de UGC es útil para reconocer las contribuciones positivas y limitar las negativas (como el spam y el lenguaje abusivo). UGC se puede moderar desde varios entornos:

* [Almacenamiento de contenido de comunidad](working-with-srp.md)

* [Consola de moderación masiva](moderation.md)

   Los administradores y pueden acceder a la consola de moderación [moderadores de la comunidad](/help/communities/users.md) en el entorno público, así como por los administradores del entorno de creación. Esto es posible cuando el contenido de la comunidad se almacena en una [almacén común](/help/communities/working-with-srp.md).

* [Moderación en contexto](in-context.md)

   La moderación en el entorno de publicación la pueden realizar los administradores y los moderadores de la comunidad directamente en la página en la que se publicó el contenido.

## Acciones de moderación {#moderation-actions}

Las acciones que se pueden realizar en el contenido publicado (UGC) varían según la identidad del usuario y el entorno. La siguiente tabla utiliza la siguiente terminología para describir las distintas funciones según la identidad del usuario:

* `Admin`

   Un usuario que es miembro de [community-administrators](users.md) grupo.

* `Moderator`

   Un miembro de un [moderadores de la comunidad](users.md#publishenvironmentusersandgroups) grupo (tiene [permisos de moderador](in-context.md#moderatorpermissions)).

* `Creator`

   El usuario que publicó el contenido.

* `Member`

   Un usuario que ha iniciado sesión sin permisos especiales.

* `Visitor`

   Un usuario anónimo.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Administrador</strong></td>
   <td><strong>Moderador</strong></td>
   <td><strong>Creador</strong></td>
   <td><strong>Miembro</strong></td>
   <td><strong>Visitante</strong></td>
   <td><strong>Evento<br /> Activado</strong></td>
   <td><strong>Premoderado</strong></td>
  </tr>
  <tr>
   <td><strong>Editar/<br /> Eliminar</strong></td>
   <td>X</td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cortar</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Denegar</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cerrar/<br /> Reabrir</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X<br /> </td>
  </tr>
  <tr>
   <td><strong>Indicador/<br /> Desmarcar</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Permitir</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X</td>
  </tr>
 </tbody>
</table>

### Editar/eliminar {#edit-delete}

Una vez realizada una publicación, el creador, un administrador o un moderador de la comunidad pueden editarla o eliminarla.

Cuando se elimina UGC, se elimina del repositorio y es posible que no se recupere.

### Cortar {#cut}

Un administrador o un moderador de la comunidad pueden mover uno o más temas de foro o preguntas de control de calidad de una ubicación a otra. Esto incluye de un sitio de comunidad a otro sitio de comunidad, siempre que el mismo miembro tenga privilegios de moderación en ambos sitios.

Al seleccionar la acción Cortar, el contenido se copia en un portapapeles. Se pueden copiar varias publicaciones y moverlas como un grupo a la nueva ubicación.

![cutugc](assets/cutugc.png)

![putbackugc](assets/putbackugc.png)

En la otra ubicación, cuando el contenido está presente en el portapapeles, se ve un botón Pegar junto a Nueva publicación con un número que identifica el número de publicaciones que se pegarán. El botón Pegar incluye una opción para borrar el portapapeles en lugar de pegarlo.

![pasteugc](assets/pasteugc.png)

![pasteugc1](assets/pasteugc1.png)

### Denegar {#deny}

Un moderador puede impedir que UGC permanezca visible en el sitio publicado. Para los administradores y moderadores de la comunidad, la publicación sigue disponible y se anota como correo no deseado.

### Cerrar/volver a abrir {#close-reopen}

La acción Cerrar funciona en todo el hilo de conversación (un tema de foro o el comentario inicial) e incluye todas las publicaciones o respuestas posteriores.

Cuando se cierra, no solo no son posibles más respuestas, sino que tampoco se permiten acciones de moderación.

Para realizar cualquier operación, el tema o comentario debe volver a abrirse.

La acción Cerrar/Volver a abrir puede ser realizada por administradores o moderadores de la comunidad.

### Marcar/Anular marca {#flag-unflag}

Marcar es un medio para que cualquier miembro que haya iniciado sesión, excepto el creador del contenido, indique que hay un problema con el contenido de una publicación. Una vez marcado, aparecerá un icono de desmarcar que permitirá al mismo miembro desmarcar el contenido.

La moderación en contexto se puede configurar para permitir que los miembros seleccionen un motivo al marcar una publicación. La lista de motivos de marca seleccionables se puede configurar, incluido si se puede introducir o no un motivo personalizado. El motivo del indicador se guarda con el UGC, pero el motivo no almacena en déclencheur ninguna acción en particular. Solo el número de indicadores déclencheur una notificación. El contenido marcado se anota como tal para que los moderadores puedan actuar en consecuencia.

El sistema realiza un seguimiento de todas las marcas, quién las marcó y el motivo de la marca, y envía un evento cuando se alcanza el umbral. Si un moderador de la comunidad permite el UGC, estos indicadores se archivan. Después de permitir y archivar, si hay marcas posteriores, se archivan como si no hubiera habido marcas anteriores.

### Permitir {#allow}

La acción Permitir es una opción para UGC que se ha marcado, denegado o no se ha aprobado en un sistema con moderación previa. La acción Permitir borrará cualquier estado marcado o denegado/spam presente y archivará cualquier dato marcado.

## Conceptos comunes de moderación {#common-moderation-concepts}

### Premoderación {#premoderation}

Cuando UGC está premoderado, la publicación no aparecerá en el sitio publicado hasta que sea aprobada por una acción de moderación. Durante la creación de un [sitio comunitario](/help/communities/sites-console.md), marcando la casilla [Contenido con moderación previa](sites-console.md#moderation) habilitará la moderación previa en todo el sitio. Una vez que los componentes se colocan en una página, los que admiten la moderación se pueden configurar para la moderación previa mediante una configuración en el cuadro de diálogo de edición:

* [Comentarios](comments.md) y [críticas](reviews.md)
in **[!UICONTROL Moderación de usuario]** > **[!UICONTROL Premoderación]**.

* [Foro](/help/communities/forum.md), [ideación](/help/communities/ideation-feature.md), [QnA](/help/communities/working-with-qna.md), y [calendario](/help/communities/calendar.md)
in **[!UICONTROL Configuración]** > **[!UICONTROL Moderado]**.

### Detección de spam {#spam-detection}

La detección de correo no deseado es una funcionalidad de moderación automática que filtra los fragmentos no deseados del contenido generado por el usuario al marcarlos como correo no deseado. Una vez habilitado, identifica si el contenido generado por un usuario es correo no deseado o no en función de una colección preconfigurada de palabras no deseadas. Las palabras de correo no deseado predeterminadas se proporcionan en

`/libs/settings/community/sites/moderation/spamdetector-conf/profiles/spam_words.txt`.

Sin embargo, para personalizar o ampliar las palabras de correo no deseado predeterminadas, cree un conjunto de palabras en el directorio /apps siguiendo la estructura de las palabras de correo no deseado predeterminadas mediante [superposición](/help/communities/overlay-comments.md).

Una publicación generada por el usuario (en todos los tipos de contenido, por ejemplo, blogs, foros y comentarios) que contenga palabras no deseadas se marca con el texto &quot;Esta publicación se clasificó como no deseada&quot; encima de la publicación.

El moderador puede ver una publicación de este tipo y marcar la misma para permitir o denegar la aparición en el sitio. Las acciones de moderación de estas publicaciones se pueden realizar en contexto o a través de la interfaz de usuario de moderación masiva.

![detección de spam](assets/spamdetection.png)

Para activar el motor de detección de correo no deseado, siga estos pasos:

1. Abrir [Consola web](https://localhost:4502/system/console/configMgr), accediendo a `/system/console/configMgr`.

1. Localizar **Moderación automática de AEM Communities** y editarla.
1. Añada el **[!UICONTROL SpamProcess]** entrada.

![proceso spam](assets/spamprocess.png)

>[!NOTE]
>
>La detección de correo no deseado solo se implementa en la configuración regional en inglés.

### Opinión {#sentiment}

La opinión se calcula según el número de palabras clave positivas y negativas ([palabras clave](#configuringwatchwords)) presente en una publicación (UGC).

El análisis de opinión utiliza un conjunto de reglas preconfiguradas y calcula la opinión del UGC. Las reglas predeterminadas se encuentran en: `/libs/cq/workflow/components/workflow/social/sentiments/rules.`

El valor que generan las reglas es de 1 (todas negativas, sin palabras positivas) a 10 (todas positivas, sin palabras negativas). Un valor de opinión de 5 es un sentimiento neutro y es el valor predeterminado.

Las reglas definidas en el componente /libs son las siguientes:

* Regla 1: establezca el valor en 1 si no hay palabras positivas y al menos una palabra negativa.
* Regla 2: establezca el valor en 10 si no hay palabras negativas y al menos una palabra positiva.
* Regla 3: establezca el valor en 3 si hay más palabras negativas que positivas.
* Regla 4: establezca el valor en 8 si hay más palabras positivas que negativas.

Para sobrescribir o agregar reglas, cree un conjunto de reglas en el directorio /apps siguiendo la estructura de las reglas predeterminadas. Edite la configuración de opinión para identificar la ubicación de las reglas.

Una vez analizado, la opinión se almacena con el UGC.

Desde el [consola de moderación masiva](/help/communities/moderation.md)Sin embargo, es posible filtrar y ver UGC en función de si la opinión es negativa, neutral o positiva.

#### Watchwords {#watchwords}

AEM Las comunidades de proporcionan un *analizador de palabras clave* como paso en el proceso de evaluación [opinión](#sentiment). La contribución al valor de opinión proporcionado por las palabras clave se debe a una comparación de palabras clave negativas y positivas utilizadas en el contenido publicado, así como palabras prohibidas.

#### Configuración de opiniones y palabras de inspección {#configure-sentiment-and-watchwords}

La lista de palabras observadas positivas y negativas se puede personalizar, al igual que las reglas de opinión.

La lista predeterminada de palabras observadas se puede introducir como propiedades de un nodo en el repositorio, de forma similar a la predeterminada, o anulando la predeterminada configurando el servicio OSGi `sentimentprocess.name` con la lista de palabras.

El **sentimentprocess.name** también se puede modificar para hacer referencia a la ubicación de un conjunto personalizado de reglas de opinión.

Para configurar opiniones y palabras observadas:

* Inicie sesión en la instancia de autor de como administrador.
* Abrir [Consola web](https://localhost:4502/system/console/configMgr).
* Localizar `sentimentprocess.name`.
* Seleccione la configuración que desea abrir en el modo de edición.

![sentimentprocess](assets/sentimentprocess.png)

* **Observaciones positivas**

   Una lista separada por comas de palabras que contribuyen a un sentimiento positivo que anula los valores predeterminados. La lista predeterminada está vacía.

* **Observaciones negativas**

   Una lista separada por comas de palabras que contribuyen a un sentimiento negativo que anula los valores predeterminados. La lista predeterminada está vacía.

* **Ruta explícita al nodo Watchwords**

   Ubicación del repositorio de un nodo que contiene el valor predeterminado `positive` y `negative` propiedades especificar palabras observadas predeterminadas. El valor predeterminado es `/libs/settings/community/watchwords/default`.

* **Reglas de opinión**

   Ubicación del repositorio de las reglas para calcular la opinión basada en palabras observadas positivas y negativas. El valor predeterminado es `/libs/cq/workflow/components/workflow/social/sentiments/rules` (sin embargo, ya no hay ningún flujo de trabajo involucrado).

A continuación se muestra un ejemplo de una entrada personalizada para las palabras clave predeterminadas, cuando `Explicit Path to Watchwords Node` se establece en `/libs/settings/community/watchwords/default`.

![crxde](assets/crxde.png)

### Permisos del moderador {#moderator-permissions}

Los siguientes permisos, cuando se asignan al mismo recurso, se denominan colectivamente `moderator permissions`:

* `Read`
* `Modify`
* `Create`
* `Delete`
* `Replicate`
