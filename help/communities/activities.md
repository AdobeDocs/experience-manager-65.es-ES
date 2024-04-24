---
title: Función Flujos de actividad
description: Descubra cómo se recopilan las actividades de un miembro de la comunidad conectado en un flujo que puede filtrar y mostrar a través del componente Flujos de actividad.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Función Flujos de actividad {#activity-streams-feature}

## Introducción {#introduction}

Las actividades de un miembro de la comunidad que ha iniciado sesión, como publicar en un foro o blog, se recopilan en un flujo que puede filtrarse y mostrarse de varias formas mediante la configuración del `Activity Streams` componente.

La capacidad de seguir agrega otra vista de las actividades cuando los miembros de la comunidad siguen publicaciones de interés o siguen las actividades de otros miembros de la comunidad.

El documento describe:

* AEM Adición del componente Flujos de actividad a un sitio de
* Ajustes de configuración del componente Flujos de actividad

### Adición de flujos de actividad a una página {#adding-activity-streams-to-a-page}

Si se desea añadir un `Activity Streams` a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Activity Streams`

Y arrástrela a su lugar en una página en la que deban aparecer flujos de actividad.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](/help/communities/basics.md).

Si la variable [bibliotecas requeridas del lado del cliente](/help/communities/essentials-activities.md#essentials-for-client-side) están incluidos, así es como se `Activity Streams` el componente aparece:

![activity-streams](assets/activity-component.png)

### Configuración de flujos de actividad {#configuring-activity-streams}

Seleccione el colocado `Activity Streams` para que pueda acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configurar](assets/configure-new.png)

En el **Actividades de usuario** , especifique qué actividades mostrar :

![user-activities](assets/user-activities.png)

* **Número máximo de actividades**

  Número de actividades que se van a mostrar

* **Ruta de medio de flujo**

  Déjelo en blanco para establecer de forma predeterminada el sitio o el grupo de la comunidad. La ruta del recurso de flujo identifica el origen de las actividades. El valor predeterminado está en blanco.

* **Mostrar vista de actividades de usuario**

  Si se selecciona, la página Actividades incluye una pestaña que filtra las actividades en función de las que genera el miembro actual dentro de la comunidad. La opción predeterminada está activada.

* **Mostrar vista de todas las actividades**

  Si se selecciona, la página de actividades incluye una pestaña que incluye todas las actividades generadas dentro de la comunidad a la que tiene acceso el miembro actual. La opción predeterminada está activada.

* **Mostrar la vista siguiente**

  Si se selecciona, la página Actividades incluye una pestaña que filtra las actividades en función de las que sigue el miembro actual. La opción predeterminada está activada.

### Vista siguiente {#following-view}

Los componentes deben configurarse para habilitar lo siguiente. Las funciones que permiten lo siguiente son [blog](/help/communities/blog-feature.md), [foro](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendario](/help/communities/calendar.md), [biblioteca de archivos](/help/communities/file-library.md), y [comentarios](/help/communities/comments.md).

![vista siguiente](assets/following-activities.png)

El **Seguir** proporciona un medio para seguir las entradas como actividades, [notificaciones](/help/communities/notifications.md), o [suscripciones](/help/communities/subscriptions.md). Cada vez que **Seguir** botón está seleccionado, es posible activar o desactivar una selección. El `Email Subscriptions` la selección solo está presente cuando está configurada.

Si se selecciona cualquier método de seguimiento, el texto del botón cambia a **Siguientes**. Para su comodidad, es posible seleccionar `Unfollow All` para desactivar todos los métodos.

El **Seguir** aparece el botón:

* Al ver el perfil de otro usuario.
* En una página de características principal, como foros, control de calidad y blogs.

   * Sigue toda la actividad de para esa función general.

* Para una entrada específica, como un tema de foro, una pregunta de control de calidad o un artículo de blog.

   * Sigue todas las actividades de esa entrada específica.

### Información adicional {#additional-information}

Puede encontrar más información en la [Activity Streams Essentials](/help/communities/essentials-activities.md) para desarrolladores.
