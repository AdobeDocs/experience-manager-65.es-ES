---
title: Función Flujos de actividad
seo-title: Función Flujos de actividad
description: Actividades de un miembro de la comunidad que ha iniciado sesión
seo-description: Actividades de un miembro de la comunidad que ha iniciado sesión
uuid: decd2d6c-4d4b-4698-a92c-2b5b441458cf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 89f3630f-c01a-4dc0-9ff5-169785f22c01
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Función Flujos de actividad{#activity-streams-feature}

## Introducción {#introduction}

Las actividades de un miembro de la comunidad que ha firmado, como publicar en un foro o blog, se recopilan en un flujo que puede filtrarse y mostrarse de diversas maneras a través de la configuración del `Activity Streams` componente.

La capacidad de seguir agrega otra visión de las actividades cuando los miembros de la comunidad siguen publicaciones de interés o siguen las actividades de otros miembros de la comunidad.

El documento describe:

* adición del componente Flujos de actividad a un sitio de AEM
* configuración del componente Flujos de actividad

### Adición de flujos de actividad a una página {#adding-activity-streams-to-a-page}

Si desea agregar un `Activity Streams` componente a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Activity Streams`

y arrástrelo a su lugar en una página donde deberían aparecer los flujos de actividad.

Para obtener la información necesaria, visite [Communities Components Basics](/help/communities/basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se incluyen las bibliotecas [del lado del cliente](/help/communities/essentials-activities.md#essentials-for-client-side) necesarias, así es como aparecerá el `Activity Streams` componente:

![chlimage_1-24](assets/chlimage_1-24.png)

### Configuración de flujos de actividad {#configuring-activity-streams}

Seleccione el componente colocado al que desea acceder y seleccione el `Activity Streams` `Configure` icono que abre el cuadro de diálogo de edición.

![chlimage_1-25](assets/chlimage_1-25.png)

En la ficha Actividades **** del usuario, especifique qué actividades mostrar:

![chlimage_1-26](assets/chlimage_1-26.png)

* **Número máximo de actividades** Número máximo de actividades para mostrar

* **Ruta** de recursos de flujo Deje en blanco para establecer de forma predeterminada el sitio de comunidad o el grupo de comunidad. La ruta del recurso de flujo identifica el origen de las actividades. El valor predeterminado está en blanco.

* **Mostrar vista** de actividades del usuario si está activada, la página de actividades incluirá una ficha que filtra las actividades en función de las generadas en la comunidad por el miembro actual. El valor predeterminado está marcado.

* **Mostrar todas las actividades** si se activa, la página de actividades incluirá una ficha que incluye todas las actividades generadas dentro de la comunidad a la que tiene acceso el miembro actual. El valor predeterminado está marcado.

* **Mostrar vista** siguiente si está activada, la página de actividades incluirá una ficha que filtra las actividades en función de las que sigue el miembro actual. El valor predeterminado está marcado.

### Vista siguiente {#following-view}

Los componentes deben configurarse para habilitar lo siguiente. Las funciones que permiten lo siguiente son [blog](/help/communities/blog-feature.md), [foro](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendario](/help/communities/calendar.md), [biblioteca](/help/communities/file-library.md)[](/help/communities/comments.md)de archivos y comentarios.

![chlimage_1-27](assets/chlimage_1-27.png)

El botón **Seguir **proporciona un medio para seguir las entradas como actividades, [notificaciones](/help/communities/notifications.md)o [suscripciones](/help/communities/subscriptions.md). Cada vez que se selecciona el botón **Seguir **se puede activar o desactivar una selección. La `Email Subscriptions` selección solo está presente cuando está configurada.

Si se selecciona cualquier método de seguimiento, el texto del botón cambia a **Siguiente**. Para mayor comodidad, es posible seleccionar `Unfollow All` desactivar todos los métodos.

Aparecerá el botón **Seguir **

* al ver el perfil de otro miembro
* en una página de características principal, como foros, QnA y blogs

   * sigue toda la actividad de esa función general

* para una entrada específica, como un tema del foro, una pregunta de preguntas y respuestas o un artículo del blog

   * sigue toda la actividad de esa entrada específica

### Información adicional {#additional-information}

Puede encontrar más información en la página [Flujos de actividad esenciales](/help/communities/essentials-activities.md) para desarrolladores.
