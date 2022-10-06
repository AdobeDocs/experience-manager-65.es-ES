---
title: Función Flujos de actividad
seo-title: Activity Streams Feature
description: Actividades de un miembro de la comunidad que ha iniciado sesión
seo-description: Activities of a signed-in community member
uuid: decd2d6c-4d4b-4698-a92c-2b5b441458cf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 89f3630f-c01a-4dc0-9ff5-169785f22c01
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 4%

---

# Función Flujos de actividad {#activity-streams-feature}

## Introducción {#introduction}

Las actividades de un miembro de la comunidad que ha firmado, como la publicación en un foro o blog, se recopilan en un flujo que puede filtrarse y mostrarse de varias maneras a través de la configuración de la `Activity Streams` componente.

La capacidad de seguir agrega otra visión de las actividades cuando los miembros de la comunidad siguen publicaciones de interés o siguen las actividades de otros miembros de la comunidad.

El documento describe:

* Adición del componente Flujos de actividad a un sitio AEM
* Ajustes de configuración del componente Flujos de actividad

### Adición de flujos de actividad a una página {#adding-activity-streams-to-a-page}

Si desea agregar un `Activity Streams` a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Activity Streams`

y arrástrela a su lugar en una página en la que deberían aparecer las emisiones de actividad.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de Communities](/help/communities/basics.md).

Cuando la variable [bibliotecas requeridas del lado del cliente](/help/communities/essentials-activities.md#essentials-for-client-side) se incluyen, así es como se muestra la variable `Activity Streams` aparecerá el componente :

![flujos de actividad](assets/activity-component.png)

### Configuración de flujos de actividad {#configuring-activity-streams}

Seleccione la colocación `Activity Streams` para acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configure](assets/configure-new.png)

En el **Actividades del usuario** especifique qué actividades mostrar :

![user-activities](assets/user-activities.png)

* **Número máximo de actividades**

   El número de actividades que se van a mostrar

* **Ruta de medio de flujo**

   Déjelo en blanco para acceder de forma predeterminada al sitio de la comunidad o al grupo de la comunidad. La ruta del recurso de flujo identifica el origen de las actividades. El valor predeterminado es en blanco.

* **Mostrar vista de actividades de usuario**

   Si se selecciona, la página actividades incluirá una pestaña que filtra las actividades en función de las generadas dentro de la comunidad por el miembro actual. El valor predeterminado está marcado.

* **Mostrar vista de todas las actividades**

   Si se selecciona, la página actividades incluirá una pestaña que incluye todas las actividades generadas dentro de la comunidad a la que tiene acceso el miembro actual. El valor predeterminado está marcado.

* **Mostrar la vista siguiente**

   Si se selecciona, la página actividades incluirá una pestaña que filtra las actividades en función de las que sigue el miembro actual. El valor predeterminado está marcado.

### Vista siguiente {#following-view}

Los componentes deben configurarse para habilitar lo siguiente. Las funciones que permiten lo siguiente son: [blog](/help/communities/blog-feature.md), [foro](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendario](/help/communities/calendar.md), [filelibrary](/help/communities/file-library.md)y [comentarios](/help/communities/comments.md).

![vista posterior](assets/following-activities.png)

La variable **Seguir** proporciona un medio para seguir entradas como actividades, [notificaciones](/help/communities/notifications.md)o [suscripciones](/help/communities/subscriptions.md). Cada vez que se usa la variable **Seguir** está seleccionado, es posible activar o desactivar una selección. La variable `Email Subscriptions` La selección solo está presente cuando está configurada.

Si se selecciona cualquier método de seguimiento, el texto del botón cambia a **A continuación**. Para mayor comodidad, es posible seleccionar `Unfollow All` para desactivar todos los métodos.

La variable **Seguir** aparecerá:

* Al ver el perfil de otro miembro.
* En una página de características principales, como foros, QnA y blogs.

   * Sigue toda la actividad de esa función general.

* Para una entrada específica, como un tema de foro, una pregunta de control de calidad o un artículo de blog.

   * Sigue toda la actividad de esa entrada específica.

### Información adicional {#additional-information}

Puede encontrar más información en la [Elementos esenciales de flujos de actividad](/help/communities/essentials-activities.md) para desarrolladores.
