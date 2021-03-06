---
title: Función de flujo de actividad
seo-title: Función de flujo de actividad
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
source-git-commit: fcdae5363e7a0070b5d6b76227e5c65efb71bc03
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 4%

---


# Función de flujo de actividad {#activity-streams-feature}

## Introducción {#introduction}

Las actividades de un miembro de la comunidad firmado, como publicar en un foro o blog, se recopilan en un flujo que puede filtrarse y mostrarse de diversas maneras a través de la configuración del componente `Activity Streams`.

La capacidad de seguir agrega otra vista de actividades cuando los miembros de la comunidad siguen publicaciones de interés o siguen las actividades de otros miembros de la comunidad.

El documento describe:

* Añadir el componente Flujos de Actividad en un sitio AEM
* Configuración del componente Flujos de Actividad

### Añadir flujos de Actividad a una página {#adding-activity-streams-to-a-page}

Si desea agregar un componente `Activity Streams` a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Activity Streams`

y arrástrelo a su lugar en una página donde deberían aparecer los flujos de actividad.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de comunidades](/help/communities/basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](/help/communities/essentials-activities.md#essentials-for-client-side), así es como aparecerá el componente `Activity Streams`:

![Flujos de actividad](assets/activity-component.png)

### Configuración de flujos de Actividad {#configuring-activity-streams}

Seleccione el componente `Activity Streams` colocado para acceder y seleccione el icono `Configure` que abre el cuadro de diálogo de edición.

![configurar](assets/configure-new.png)

En la ficha **Actividades de usuario**, especifique qué actividades mostrar:

![actividades de usuario](assets/user-activities.png)

* **Número máximo de actividades**

   El número de actividades que se mostrarán

* **Ruta de medio de flujo**

   Déjelo en blanco para acceder de forma predeterminada al sitio de comunidad o al grupo de comunidad. La ruta del recurso de flujo identifica el origen de las actividades. El valor predeterminado está en blanco.

* **Mostrar vista de actividades de usuario**

   Si se selecciona, la página actividades incluirá una ficha que filtros actividades en función de las generadas dentro de la comunidad por el miembro actual. El valor predeterminado está marcado.

* **Mostrar vista de todas las actividades**

   Si se selecciona, la página actividades incluirá una ficha que incluirá todas las actividades generadas dentro de la comunidad a la que tiene acceso el miembro actual. El valor predeterminado está marcado.

* **Mostrar la vista siguiente**

   Si se selecciona, la página actividades incluirá una ficha que filtros actividades en función de las que sigue el miembro actual. El valor predeterminado está marcado.

### Vista siguiente {#following-view}

Los componentes deben configurarse para habilitar lo siguiente. Las funciones que permiten lo siguiente son [blog](/help/communities/blog-feature.md), [foro](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendario](/help/communities/calendar.md), [biblioteca de archivos](/help/communities/file-library.md) y [comentarios](/help/communities/comments.md).

![vista siguiente](assets/following-activities.png)

El botón **Seguir** proporciona un medio para seguir las entradas como actividades, [notificaciones](/help/communities/notifications.md) o [suscripciones](/help/communities/subscriptions.md). Cada vez que se selecciona el botón **Seguir**, es posible activar o desactivar una selección. La selección `Email Subscriptions` sólo está presente cuando está configurada.

Si se selecciona cualquier método de seguimiento, el texto del botón cambia a **Siguiente**. Para mayor comodidad, es posible seleccionar `Unfollow All` para desactivar todos los métodos.

Aparecerá el botón **Seguir**:

* Al ver el perfil de otro miembro.
* En una página de características principal, como foros, QnA y blogs.

   * Sigue toda la actividad de esa función general.

* Para una entrada específica, como un tema del foro, una pregunta de QnA o un artículo del blog.

   * Sigue toda la actividad de esa entrada específica.

### Información adicional {#additional-information}

Puede encontrar más información en la página [Actividad Streams Essentials](/help/communities/essentials-activities.md) para desarrolladores.
