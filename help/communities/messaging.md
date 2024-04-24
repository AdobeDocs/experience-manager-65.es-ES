---
title: Configurar la mensajería
description: Obtenga información acerca de la función de mensajería de AEM Communities que permite a los visitantes (miembros) del sitio que han iniciado sesión enviarse mensajes entre sí.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: ee94f093-fd14-49f2-9990-fbe853d924b1
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# Configurar la mensajería {#configure-messaging}

## Información general {#overview}

La función de mensajería para AEM Communities permite a los visitantes (miembros) del sitio que han iniciado sesión enviarse mensajes que son accesibles una vez que han iniciado sesión en el sitio.

La mensajería está habilitada para un sitio de la comunidad marcando una casilla durante [creación de sitios de la comunidad](/help/communities/sites-console.md).

Esta página contiene información sobre la configuración predeterminada y los posibles ajustes.

Para obtener información adicional para desarrolladores, consulte [Messaging Essentials](/help/communities/essentials-messaging.md).

## Servicio de operaciones de mensajería {#messaging-operations-service}

La configuración [Servicio de operaciones de mensajería de AEM Communities](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) identifica el extremo que administra las solicitudes relacionadas con la mensajería, las carpetas que el servicio debe utilizar para almacenar mensajes y, si los mensajes pueden incluir archivos adjuntos, qué tipos de archivo se permiten.

Para los sitios de la comunidad creados con `Communities Sites console`, existe una instancia del servicio, con la bandeja de entrada configurada como `/mail/inbox`.

### Servicio Community Messaging Operations {#community-messaging-operations-service}

Como se muestra a continuación, existe una configuración del servicio para los sitios creados con [asistente de creación de sitios](/help/communities/sites-console.md). La configuración se puede ver o editar seleccionando el icono de lápiz junto a la configuración.

![messaging-operations](assets/messaging-operations.png)

### Añadir nueva configuración {#add-new-configuration}

Para añadir una configuración, seleccione el signo más &#39;**+**&#39; junto al nombre del servicio:

* **Lista de permitidos Campos de mensaje**

  Especifica las propiedades del componente Componer mensaje que los usuarios pueden editar y conservar. Si se agregan nuevos elementos de formulario, se debe agregar el ID del elemento si se desea almacenar en SRP. El valor predeterminado es dos entradas: *sujeto* y *content*.

* **Límite de tamaño de cuadro de mensaje**

  Número máximo de bytes en el cuadro de mensaje de cada usuario. El valor predeterminado es *1073741824* (1 GB).

* **Límite de recuento de mensajes**

  Número total de mensajes permitidos por usuario. El valor -1 indica que se permite un número ilimitado de mensajes, sujeto al límite de tamaño del cuadro de mensaje. El valor predeterminado es *10000* (10k).

* **Notificar error de envío**

  Si se selecciona, se notifica al remitente si la entrega del mensaje falla a algunos destinatarios. El valor predeterminado es *comprobado*.

* **Error de ID de remitente de entrega**

  Nombre del remitente que aparece en el mensaje de error de entrega. El valor predeterminado es *failureNotifier*.

* **Ruta de plantilla de mensaje de error**

  Ruta absoluta a la raíz de la plantilla de mensaje del envío con error. El valor predeterminado es */etc/notification/messaging/default*.

* **Número de reintentos**

  Número de veces que se intenta reenviar el mensaje que no se puede enviar. El valor predeterminado es *3*.

* **Esperar entre reintentos**

  Número de segundos de espera entre intentos para reenviar el mensaje si no se puede enviar. El valor predeterminado es *100* (segundos).

* **Contar tamaño del grupo de actualización**

  Número máximo de subprocesos simultáneos utilizados para la actualización del recuento. El valor predeterminado es *10*.

* **Ruta de bandeja de entrada**

  (*Requerido*) La ruta relativa al nodo del usuario (/home/users/*nombre de usuario*), que se usará para `inbox` carpeta. La ruta NO debe finalizar con una barra diagonal final &quot;/&quot;. El valor predeterminado es */mail/inbox*.

* **Ruta de elementos enviados**

  (*Requerido*) La ruta relativa al nodo del usuario (/home/users/*nombre de usuario*), que se usará para `sent items` carpeta. La ruta NO debe finalizar con una barra diagonal final &quot;/&quot;. El valor predeterminado es */mail/sentitems* .

* **Admitir archivos adjuntos**

  Si se selecciona, los usuarios pueden agregar archivos adjuntos a sus mensajes. El valor predeterminado es *comprobado*.

* **Habilitar la mensajería de grupo**

  Si se selecciona, los usuarios registrados pueden enviar mensajes masivos a un grupo de miembros. El valor predeterminado es *no seleccionado*.

* **Nº máximo de destinatarios totales**

  Si la mensajería de grupo está habilitada, especifique el número máximo de destinatarios a los que se pueden enviar mensajes de grupo a la vez. El valor predeterminado es *100*.

* **Tamaño del lote**

  Número de mensajes que se van a agrupar para un envío al enviarlos a un grupo grande de destinatarios. El valor predeterminado es *100*.

* **Tamaño total del archivo adjunto**

  Si se activa supportAttachments, este valor especifica el tamaño total máximo permitido (en bytes) de todos los datos adjuntos. El valor predeterminado es *104857600* (100 MB).

* **Lista de bloqueados de tipo de adjunto**

  Una lista de bloqueados de extensiones de nombre de archivo, con el prefijo &#39;**.**&#39;, que es rechazado por el sistema. Si no está incluida en la lista de bloqueados, se permite la extensión. Las extensiones se pueden añadir o eliminar utilizando &#39;**+**&#39; y &#39;**-** Iconos de.

* **Tipos de archivos adjuntos permitidos**

  **(*Acción necesaria*)** Una lista de permitidos de extensiones de nombre de archivo, la opuesta a la lista de bloqueados. Para permitir todas las extensiones de nombre de archivo, excepto las incluidas en la lista de bloqueados, utilice el **-**&#39; para eliminar la única entrada vacía.

* **Selector de servicio**

  (*Requerido*) Una ruta absoluta (extremo) a través de la cual se llama al servicio (recurso virtual). La raíz de la ruta elegida debe ser una incluida en la variable *Rutas de ejecución* Ajuste de configuración de la configuración de OSGi [`Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver), como `/bin/`, `/apps/`, y `/services/`. Para seleccionar esta configuración para la función de mensajería de un sitio, este extremo se proporciona como **`Service selector`** valor para `Message List and Compose Message components` (consulte [Función de mensaje](/help/communities/configure-messaging.md)).

  El valor predeterminado es */bin/messaging* .

* **Lista de permitidos de campo**

  Uso **Lista de permitidos Campos de mensaje**.

>[!CAUTION]
>
>Cada vez que `Messaging Operations Service` La configuración de se abre para su edición, si `allowedAttachmentTypes.name` Si se ha eliminado, se lee una entrada vacía para poder configurar la propiedad. Una sola entrada vacía deshabilita efectivamente los archivos adjuntos.
>
>Para permitir todas las extensiones de nombre de archivo, excepto las incluidas en la lista de bloqueados, utilice el **-**&#39; para eliminar (de nuevo) la única entrada vacía antes de hacer clic en **Guardar**.

## Mensajería grupal {#group-messaging}

Para permitir que los usuarios registrados envíen mensajes directos de forma masiva a grupos de usuarios, asegúrese de lo siguiente **Habilitar la mensajería de grupo** en las dos instancias siguientes de **Servicios de operación de mensajería** configuración:

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**Servicio de operaciones de mensajería: consola social**

![social-console-op-service](assets/social-console-op-service.png)

**Servicio de Operaciones de Mensajería: mensajería social**

![social-message-op-service](assets/social-message-op-service.png)

## Resolución de problemas {#troubleshooting}

Una forma de solucionar los problemas es habilitar [depuración de mensajes en el registro.](/help/sites-administering/troubleshooting.md)

Consulte también [Registradores y escritores para servicios individuales](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

El paquete que se va a supervisar es `com.adobe.cq.social.messaging`.
