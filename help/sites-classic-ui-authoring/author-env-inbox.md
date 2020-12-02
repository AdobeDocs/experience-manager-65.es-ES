---
title: 'Su bandeja de entrada  '
seo-title: 'Su bandeja de entrada  '
description: Puede recibir notificaciones desde varias áreas de AEM, como notificaciones sobre elementos de trabajo o tareas que representan acciones que debe realizar en el contenido de la página.
seo-description: Puede recibir notificaciones desde varias áreas de AEM, como notificaciones sobre elementos de trabajo o tareas que representan acciones que debe realizar en el contenido de la página.
uuid: e7ba9150-957d-4f84-a570-2f3d83792472
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: ce2a1475-49cf-43e6-bfb9-006884ce3881
docset: aem65
translation-type: tm+mt
source-git-commit: bcb1840d23ae538c183eecb0678b6a75d346aa50
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 93%

---


# Su bandeja de entrada   {#your-inbox}

Puede recibir notificaciones desde varias áreas de AEM, como notificaciones sobre elementos de trabajo o tareas que representan acciones que debe realizar en el contenido de la página.

Estas notificaciones se reciben en dos bandejas de entrada, que están separadas por tipo de notificación:

* Una bandeja de entrada donde se ven las notificaciones recibidas en relación con las suscripciones (se describe en la sección siguiente).
* En el documento [Participación en Flujos de trabajo](/help/sites-classic-ui-authoring/classic-workflows-participating.md) se describe una bandeja de entrada especializada para elementos de flujo de trabajo.

## Visualizar notificaciones {#viewing-your-notifications}

Para ver las notificaciones:

1. Abra la bandeja de entrada de notificaciones: en la consola **Sitios web**, haga clic en el botón de usuario ubicado en la esquina superior derecha y seleccione **Bandeja de entrada de notificaciones**.

   ![screen_shot_2012-02-08at105226am](assets/screen_shot_2012-02-08at105226am.png)

   >[!NOTE]
   >
   >También puede acceder a la consola directamente desde el navegador; por ejemplo:
   >
   >
   >` https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. Se enumerarán las notificaciones. Puede realizar las acciones requeridas:

   * [Suscripción a las notificaciones](#subscribing-to-notifications)
   * [Procesamiento de notificaciones](#processing-your-notifications)

   ![climage_1-4](assets/chlimage_1-4.jpeg)

## Suscripción a las notificaciones {#subscribing-to-notifications}

Para suscribirse a notificaciones:

1. Abra la bandeja de entrada de notificaciones: en la consola **Sitios web**, haga clic en el botón de usuario ubicado en la esquina superior derecha y seleccione **Bandeja de entrada de notificaciones**.

   ![screen_shot_2012-02-08at105226am-1](assets/screen_shot_2012-02-08at105226am-1.png)

   >[!NOTE]
   >
   >También puede acceder a la consola directamente desde el navegador; por ejemplo:
   >
   >
   >`https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. Haga clic en **Configurar...** en la esquina superior izquierda para abrir el cuadro de diálogo de configuración.

   ![screen_shot_2012-02-08at111056am](assets/screen_shot_2012-02-08at111056am.png)

1. Seleccione el canal de notificación:

   * **Bandeja de entrada**: las notificaciones se mostrarán en su bandeja de entrada de AEM.
   * **Correo electrónico**: las notificaciones se enviarán a la dirección de correo electrónico definida en su perfil de usuario.

   >[!NOTE]
   >
   >Es necesario configurar unas pocas opciones para recibir notificaciones por correo electrónico. También es posible personalizar la plantilla de correo electrónico o añadir una plantilla de correo electrónico para un nuevo idioma. Consulte [Configuración de notificaciones por correo electrónico](/help/sites-administering/notification.md#configuringemailnotification) para configurar las notificaciones por correo electrónico en AEM.

1. Seleccione las acciones de página para las cuales recibirá notificaciones:

   * Activado: cuando se activa una página.
   * Desactivado: cuando se desactiva una página.
   * Eliminado (distribución): cuando se elimina-replica una página. Es decir, cuando se replica una acción de eliminar realizada en una página.
Cuando se elimina o mueve una página, se replica automáticamente una acción de eliminar: la página se elimina en la instancia de origen donde la acción de eliminar se realizó y en la instancia de destino definida por los agentes de replicación.

   * Modificado: cuando se modifica una página.
   * Creado: cuando se crea una página.
   * Eliminado: cuando se elimina una página mediante la acción de eliminar página.
   * Trasladado: cuando se traslada una página.

1. Defina las rutas de las páginas para las cuales recibirá notificaciones:

   * Haga clic en **Añadir** para añadir una nueva fila a la tabla.
   * Haga clic en la celda de la tabla **Ruta** e introduzca la ruta, por ejemplo: `/content/docs`.

   * Para recibir notificaciones para todas las páginas pertenecientes al subárbol, establezca **¿Exacto?** en **No**.
Para recibir notificaciones únicamente para acciones en la página definida por la ruta, establezca **¿Exacto?** en **Sí**.

   * Para permitir la regla, establezca **Regla** en **Permitir**. Si la establece en **Denegar**, se deniega la regla pero no se quita y se puede permitir después.

   Para quitar una definición, seleccione la fila al hacer clic en una celda de tabla y haga clic en **Eliminar**.

1. Haga clic en **Guardar** para guardar la configuración.

## Procesamiento de notificaciones {#processing-your-notifications}

Si eligió recibir notificaciones en su bandeja de entrada AEM, la bandeja de entrada se llenará de notificaciones. Puede [ver sus notificaciones](#viewing-your-notifications) y, a continuación, seleccionar las notificaciones necesarias para:

* Aprobarla al hacer clic en **Aprobar**: el valor en la columna **Leer** se establece en **true**.

* Eliminarla al hacer clic en **Eliminar**.

![climage_1-5](assets/chlimage_1-5.jpeg)
