---
title: Función de flujo de Actividad
seo-title: Función de flujo de Actividad
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
source-git-commit: 10c17fc199c476ec66059cc6bf4cbb4a0ff1af40
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 4%

---


# Función de flujo de Actividad {#activity-streams-feature}

## Introducción {#introduction}

Las actividades de un miembro de la comunidad firmado, como publicar en un foro o blog, se recopilan en un flujo que puede filtrarse y mostrarse de diversas maneras a través de la configuración del `Activity Streams` componente.

La capacidad de seguir agrega otra vista de actividades cuando los miembros de la comunidad siguen publicaciones de interés o siguen las actividades de otros miembros de la comunidad.

El documento describe:

* Añadir el componente Flujos de Actividad en un sitio de AEM
* Configuración del componente Flujos de Actividad

### Añadir flujos de Actividad en una página {#adding-activity-streams-to-a-page}

Si desea agregar un `Activity Streams` componente a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Activity Streams`

y arrástrelo a su lugar en una página donde deberían aparecer los flujos de actividad.

Para obtener la información necesaria, visite [Communities Components Basics](/help/communities/basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se incluyen las bibliotecas [del lado del cliente](/help/communities/essentials-activities.md#essentials-for-client-side) necesarias, así es como aparecerá el `Activity Streams` componente:

![chlimage_1-195](assets/chlimage_1-195.png)

### Configuración de flujos de Actividad {#configuring-activity-streams}

Seleccione el componente colocado al que desea acceder y seleccione el `Activity Streams` `Configure` icono que abre el cuadro de diálogo de edición.

![chlimage_1-494](assets/chlimage_1-494.png)

En la ficha Actividades **** del usuario, especifique qué actividades mostrar:

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

Los componentes deben configurarse para habilitar lo siguiente. Las funciones que permiten lo siguiente son [blog](/help/communities/blog-feature.md), [foro](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendario](/help/communities/calendar.md), [biblioteca](/help/communities/file-library.md)[](/help/communities/comments.md)de archivos y comentarios.

![climage_1-5](assets/chlimage_1-5.png)

El botón **Seguir** proporciona un medio para seguir las entradas como actividades, [notificaciones](/help/communities/notifications.md)o [suscripciones](/help/communities/subscriptions.md). Cada vez que se selecciona el botón **Seguir** , es posible activar o desactivar una selección. La `Email Subscriptions` selección solo está presente cuando está configurada.

Si se selecciona cualquier método de seguimiento, el texto del botón cambia a **Siguiente**. Para mayor comodidad, es posible seleccionar `Unfollow All` desactivar todos los métodos.

Aparecerá el botón **Seguir** :

* Al ver el perfil de otro miembro.
* En una página de características principal, como foros, QnA y blogs.

   * Sigue toda la actividad de esa función general.

* Para una entrada específica, como un tema del foro, una pregunta de QnA o un artículo del blog.

   * Sigue toda la actividad de esa entrada específica.

### Información adicional {#additional-information}

Puede encontrar más información en la página [Actividad Streams Essentials](/help/communities/essentials-activities.md) para desarrolladores.
