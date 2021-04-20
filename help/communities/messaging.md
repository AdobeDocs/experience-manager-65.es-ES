---
title: Configurar mensajería
seo-title: Configuración de mensajería
description: Mensajería de comunidades
seo-description: Mensajería de comunidades
uuid: 159dcf9d-7948-4a3d-9f51-a5b4d03e172b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 232a0ec1-8dfc-41ec-84cc-69f9db494ea0
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 1%

---


# Configurar la mensajería {#configure-messaging}

## Información general {#overview}

La función de mensajería para AEM Communities permite a los visitantes del sitio (miembros) con sesión iniciada enviar mensajes entre sí a los que se puede acceder desde la sesión iniciada en el sitio.

La mensajería está habilitada para un sitio de la comunidad marcando una casilla durante la [creación del sitio de la comunidad](/help/communities/sites-console.md).

Esta página tiene información sobre la configuración predeterminada y los posibles ajustes.

Para obtener información adicional para desarrolladores, consulte [Messaging Essentials](/help/communities/essentials-messaging.md).

## Servicio de operaciones de mensajería {#messaging-operations-service}

La configuración [AEM Communities Messaging Operations Service](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) identifica el punto final que gestiona las solicitudes relacionadas con la mensajería, las carpetas que el servicio debe utilizar para almacenar mensajes y, si los mensajes pueden incluir archivos adjuntos, qué tipos de archivo están permitidos.

Para los sitios de la comunidad creados con `Communities Sites console`, ya existe una instancia del servicio, con la bandeja de entrada configurada como `/mail/inbox`.

### Servicio de operaciones de mensajería de la comunidad {#community-messaging-operations-service}

Como se muestra a continuación, existe una configuración del servicio para los sitios creados con el [asistente de creación de sitios](/help/communities/sites-console.md). La configuración se puede ver o editar seleccionando el icono de lápiz junto a la configuración.

![operaciones de mensajería](assets/messaging-operations.png)

### Añadir nueva configuración {#add-new-configuration}

Para agregar una nueva configuración, seleccione el icono &quot;**+**&quot; junto al nombre del servicio:

* **Lista de permitidos de campos del mensaje**

   Especifica las propiedades del componente Componer mensaje que los usuarios pueden editar y mantener. Si se añaden nuevos elementos de formulario, sería necesario añadir el id de elemento si se desea almacenar en SRP. El valor predeterminado son dos entradas: *subject* y *content*.

* **Límite de tamaño del cuadro de mensaje**

   Número máximo de bytes en el cuadro de mensaje de cada usuario. El valor predeterminado es *1073741824* (1 GB).

* **Límite de recuento de mensajes**

   El número total de mensajes permitidos por usuario. El valor -1 indica que se permite un número ilimitado de mensajes, sujeto al límite de tamaño del cuadro de mensaje. El valor predeterminado es *10000* (10k).

* **Notificar el error de entrega**

   Si está activado, notifique al remitente si la entrega de mensajes falla en algunos destinatarios. El valor predeterminado es *activado*.

* **Id. del remitente del envío de error**

   Nombre del remitente que aparece en el mensaje de error de entrega. El valor predeterminado es *failureNotifier*.

* **Ruta de la plantilla del mensaje de error**

   La ruta absoluta a la entrega produjo un error en la raíz de la plantilla de mensaje. El valor predeterminado es */etc/notification/messaging/default*.

* **Número de reintentos**

   Número de veces que se intenta reenviar el mensaje que no se puede entregar. El valor predeterminado es *3*.

* **Espera entre reintentos**

   Número de segundos que hay que esperar entre los intentos de reenviar el mensaje si no se ha enviado. El valor predeterminado es *100* (segundos).

* **Recuento del tamaño del grupo de informes de actualización**

   Número de subprocesos simultáneos utilizados para la actualización del recuento. El valor predeterminado es *10*.

* **Ruta de la bandeja de entrada**

   (*Requerido*) La ruta, relativa al nodo del usuario (/home/users/*username*), que se utilizará en la carpeta `inbox`. La ruta NO debe terminar con una barra diagonal final &#39;/&#39;. El valor predeterminado es */mail/inbox*.

* **Ruta de acceso de elementos enviados**

   (*Requerido*) La ruta, relativa al nodo del usuario (/home/users/*username*), que se utilizará en la carpeta `sent items`. La ruta NO debe terminar con una barra diagonal final &#39;/&#39;. El valor predeterminado es */mail/sentiitems* .

* **Admitir archivos adjuntos**

   Si se selecciona, los usuarios pueden añadir archivos adjuntos a sus mensajes. El valor predeterminado es *activado*.

* **Habilitar la mensajería de grupo**

   Si se selecciona, los usuarios registrados pueden enviar mensajes masivos a un grupo de miembros. El valor predeterminado es *deseleccionado*.

* **Nº máximo de destinatarios totales**

   Si la mensajería de grupo está habilitada, especifique el número máximo de destinatarios a los que se puede enviar el mensaje de grupo a la vez. El valor predeterminado es *100*.

* **Tamaño del lote**

   Número de mensajes que se van a agrupar para un envío al enviarlos a un grupo grande de destinatarios. El valor predeterminado es *100*.

* **Tamaño total del archivo adjunto**

   Si se selecciona supportAttachments , este valor especifica el tamaño total máximo permitido (en bytes) de todos los archivos adjuntos. El valor predeterminado es *104857600* (100 MB).

* **Lista de bloqueados de tipo de archivo adjunto**

   Una lista de bloqueados de extensiones de nombre de archivo con el prefijo &#39;**.**&#39;, que será rechazado por el sistema. Si no está incluida en la lista de bloqueados, se permite la extensión. Las extensiones se pueden añadir o eliminar utilizando los iconos &#39;**+**&#39; y &#39;**-**&#39;.

* **Tipos de archivos adjuntos permitidos**

   **(*Acción requerida*)** Una lista de permitidos de extensiones de nombre de archivo, lo contrario de la lista de bloqueados. Para permitir todas las extensiones de nombre de archivo, excepto las incluidas en la lista de bloqueados, utilice el icono &#39;**-**&#39; para eliminar la única entrada vacía.

* **Selector de servicio**

   (*Requerido*) Una ruta absoluta (extremo) a través de la cual se llama al servicio (un recurso virtual). La raíz de la ruta elegida debe estar incluida en la configuración *Rutas de ejecución* de la configuración OSGi [ `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver), como `/bin/`, `/apps/` y `/services/`. Para seleccionar esta configuración para la función de mensajería de un sitio, este extremo se proporciona como el valor **`Service selector`** para `Message List and Compose Message components` (consulte [Función del mensaje](/help/communities/configure-messaging.md)).

   El valor predeterminado es */bin/messaging* .

* **Lista de permitidos de campo**

   Utilice la **Lista de permitidos de campos de mensaje**.

>[!CAUTION]
>
>Cada vez que se abre una configuración `Messaging Operations Service` para su edición, si se ha eliminado `allowedAttachmentTypes.name`, se vuelve a añadir una entrada vacía para que la propiedad se pueda configurar. Una sola entrada vacía deshabilita los archivos adjuntos.
>
>Para permitir todas las extensiones de nombre de archivo, excepto las incluidas en la lista de bloqueados, utilice el icono &#39;**-**&#39; para eliminar (de nuevo) la única entrada vacía antes de hacer clic en **Guardar**.

## Mensajería de grupo {#group-messaging}

Para permitir que los usuarios registrados envíen mensajes directos de forma masiva a los grupos de usuarios, asegúrese de **Habilitar la mensajería de grupo** en las dos instancias siguientes de la configuración **Messaging Operation Services**:

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**Servicio de operaciones de mensajería: consola social**

![social-console-op-service](assets/social-console-op-service.png)

**Servicio de operaciones de mensajería: mensajería social**

![social-message-op-service](assets/social-message-op-service.png)

## Solución de problemas {#troubleshooting}

Una manera de solucionar los problemas es habilitar los [mensajes de depuración en el registro.](/help/sites-administering/troubleshooting.md)

Consulte también [Loggers and Writers for Individual Services](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

El paquete a monitorizar es `com.adobe.cq.social.messaging`.
