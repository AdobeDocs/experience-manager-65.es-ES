---
title: Configurar mensajería
seo-title: Configuración de mensajes
description: Mensajería de las comunidades
seo-description: Mensajería de las comunidades
uuid: 159dcf9d-7948-4a3d-9f51-a5b4d03e172b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 232a0ec1-8dfc-41ec-84cc-69f9db494ea0
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 1%

---


# Configurar mensajería {#configure-messaging}

## Información general {#overview}

La función de mensajería de AEM Communities permite que los visitantes del sitio (miembros) con sesión iniciada envíen mensajes entre sí a los que se puede acceder al iniciar sesión en el sitio.

La mensajería se habilita para un sitio de comunidad marcando una casilla durante la creación [del sitio de](/help/communities/sites-console.md)comunidad.

Esta página contiene información sobre la configuración predeterminada y los posibles ajustes.

Para obtener información adicional para desarrolladores, consulte [Messaging Essentials](/help/communities/essentials-messaging.md).

## Servicio de operaciones de mensajería {#messaging-operations-service}

La configuración del servicio [de operaciones de mensajería de](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) AEM Communities identifica el punto final que gestiona las solicitudes relacionadas con los mensajes, las carpetas que el servicio debe utilizar para almacenar los mensajes y, si los mensajes pueden incluir archivos adjuntos, qué tipos de archivos están permitidos.

Para los sitios de comunidad creados con el `Communities Sites console`, ya existe una instancia del servicio, con la bandeja de entrada configurada en `/mail/inbox`.

### Servicio de operaciones de mensajería de la comunidad {#community-messaging-operations-service}

Como se muestra a continuación, existe una configuración del servicio para los sitios creados con el asistente [de creación del](/help/communities/sites-console.md)sitio. La configuración se puede ver o editar seleccionando el icono de lápiz junto a la configuración.

![mensajería-operaciones](assets/messaging-operations.png)

### Añadir nueva configuración {#add-new-configuration}

Para agregar una nueva configuración, seleccione el icono más &#39;**+**&#39; junto al nombre del servicio:

* **Lista de permitidos de campos del mensaje**

   Especifica las propiedades del componente Componer mensaje que los usuarios pueden editar y mantener. Si se agregan nuevos elementos de formulario, se deberá agregar la identificación del elemento si se desea almacenar en SRP. El valor predeterminado es dos entradas: *asunto* y *contenido*.

* **Límite de tamaño del cuadro de mensaje**

   Número máximo de bytes en el cuadro de mensaje de cada usuario. El valor predeterminado es *1073741824* (1 GB).

* **Límite de recuento de mensajes**

   Número total de mensajes permitidos por usuario. Un valor de -1 indica que se permite un número ilimitado de mensajes, con sujeción al límite de tamaño del cuadro de mensaje. El valor predeterminado es *10000* (10 k).

* **Error al notificar envío**

   Si está activada, notifique al remitente si el envío de mensajes falla en algunos destinatarios. El valor predeterminado está *marcado*.

* **Id. del remitente de envío de error**

   Nombre del remitente que aparece en el mensaje de error de envío. El valor predeterminado es *failNotifier*.

* **Ruta de la plantilla de mensaje de error**

   La ruta absoluta a la raíz de la plantilla de mensaje de envío falló. El valor predeterminado es */etc/notification/messaging/default*.

* **Número de reintentos**

   Número de veces que se intenta reenviar el mensaje que no se puede entregar. El valor predeterminado es *3*.

* **Esperar entre reintentos**

   Número de segundos que hay que esperar entre los intentos de reenviar el mensaje si no se pudo enviar. El valor predeterminado es *100* (segundos).

* **Contar el tamaño del grupo de actualizaciones**

   Número de subprocesos simultáneos utilizados para la actualización de recuento. El valor predeterminado es *10*.

* **Ruta de la bandeja de entrada**

   (*Requerido*) La ruta, relativa al nodo del usuario (/home/users/*username*), que se usará para la `inbox` carpeta. La ruta NO debe terminar con una barra diagonal final &#39;/&#39;. El valor predeterminado es */mail/inbox*.

* **Ruta de elementos enviados**

   (*Requerido*) La ruta, relativa al nodo del usuario (/home/users/*username*), que se usará para la `sent items` carpeta. La ruta NO debe terminar con una barra diagonal final &#39;/&#39;. El valor predeterminado es */mail/sentiitems* .

* **Admite archivos adjuntos**

   Si se selecciona, los usuarios pueden agregar datos adjuntos a sus mensajes. El valor predeterminado está *marcado*.

* **Habilitar la mensajería de grupo**

   Si se selecciona, los usuarios registrados pueden enviar mensajes masivos a un grupo de miembros. El valor predeterminado *no está seleccionado*.

* **Nº máximo del total de destinatarios**

   Si la mensajería de grupo está habilitada, especifique el número máximo de destinatarios a los que se puede enviar un mensaje de grupo a la vez. El valor predeterminado es *100*.

* **Tamaño del lote**

   Número de mensajes que se van a agrupar para un envío al enviar a un grupo grande de destinatarios. El valor predeterminado es *100*.

* **Tamaño total de datos adjuntos**

   Si se selecciona supportAttachments, este valor especifica el tamaño total máximo permitido (en bytes) de todos los archivos adjuntos. El valor predeterminado es *104857600* (100 MB).

* **Lista de bloqueados de tipo de datos adjuntos**

   Lista de bloqueados de extensiones de nombre de archivo, con el prefijo &#39;**.**&#39;, que será rechazado por el sistema. Si no está incluida en la lista de bloqueados, se permite la extensión. Las extensiones pueden agregarse o eliminarse mediante los iconos &#39;**+**&#39; y &#39;**-**&#39;.

* **Tipos de datos adjuntos permitidos**

   **(*Acción requerida*)** Una lista de permitidos de extensiones de nombre de archivo, lo contrario de la lista de bloqueados. Para permitir todas las extensiones de nombre de archivo, excepto las incluidas en la lista de bloqueados, utilice el icono &#39;**-**&#39; para eliminar la única entrada vacía.

* **Selector de servicio**

   (*Requerido*) Una ruta absoluta (extremo) a través de la cual se llama al servicio (recurso virtual). La raíz de la ruta elegida debe estar incluida en la configuración de rutas *de* ejecución de la configuración de OSGi [`Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver), como `/bin/`, `/apps/`y `/services/`. Para seleccionar esta configuración para la función de mensajería de un sitio, este extremo se proporciona como el **`Service selector`** valor para la `Message List and Compose Message components` (consulte Función [de](/help/communities/configure-messaging.md)mensaje).

   El valor predeterminado es */bin/messaging* .

* **Lista de permitidos de campo**

   Utilice la Lista de permitidos **Campos** de mensaje.

>[!CAUTION]
>
>Cada vez que se abre una `Messaging Operations Service` configuración para editarla, si `allowedAttachmentTypes.name` se ha eliminado, se vuelve a agregar una entrada vacía para que la propiedad se pueda configurar. Una sola entrada vacía deshabilita los archivos adjuntos de forma efectiva.
>
>Para permitir todas las extensiones de nombre de archivo, excepto las incluidas en la lista de bloqueados, utilice el icono &#39;**-**&#39; para (de nuevo) eliminar la única entrada vacía antes de hacer clic en **Guardar**.

## Group Messaging {#group-messaging}

Para permitir que los usuarios registrados envíen mensajes directos de forma masiva a grupos de usuarios, asegúrese de **activar la mensajería** de grupo en las dos instancias siguientes de la configuración de Servicios **de operación de** mensajería:

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**Servicio de operaciones de mensajería: consola social**

![social-console-op-service](assets/social-console-op-service.png)

**Servicio de operaciones de mensajería: mensajería social**

![social-message-op-service](assets/social-message-op-service.png)

## Solución de problemas {#troubleshooting}

Una manera de solucionar problemas es habilitar los mensajes de [depuración en el registro.](/help/sites-administering/troubleshooting.md)

Consulte también [Registros y escritores para servicios](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)individuales.

El paquete que se debe supervisar es `com.adobe.cq.social.messaging`.
