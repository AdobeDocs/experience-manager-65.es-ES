---
title: Función de mensajería
seo-title: Función de mensajería
description: Configuración de componentes de mensajería
seo-description: Configuración de componentes de mensajería
uuid: 8b99ded1-aec2-40c9-82d5-e2e404f614ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9d952604-f9ef-498f-937b-871817c80226
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 4%

---


# Función de mensajería {#messaging-feature}

Además de las interacciones públicamente visibles que se producen en los foros y comentarios, la función de mensajería de AEM Communities permite a los miembros de la comunidad interactuar entre sí de forma más privada.

Esta función se puede incluir cuando se crea un [sitio de comunidad](/help/communities/overview.md#communitiessites).

La función de mensajería permite:

**A** : enviar un mensaje a uno o varios miembros de la comunidad

**B** : enviar mensajes directos en  [masa a los grupos de miembros de la comunidad](/help/communities/messaging.md#group-messaging)

**C** : enviar un mensaje con datos adjuntos

**D** : reenviar un mensaje

**E** : responder a un mensaje

**F** : eliminar un mensaje

**G** : restaurar un mensaje eliminado

![messaging-section](assets/messaging-section.png)

![restore-message](assets/restore-message.png)

Para habilitar y modificar la función de mensajería, consulte:

* [Configurar ](/help/communities/messaging.md) mensajería para administradores
* [Messaging ](/help/communities/essentials-messaging.md) Essentials para desarrolladores

>[!NOTE]
>
>No se admite la adición de `Compose Message, Message, or Message List` componentes (que se encuentra en `Communities`grupo de componentes) a una página en modo de edición de autor.

## Configurar componentes de mensajería {#configure-messaging-components}

Cuando se habilita la mensajería para un sitio de comunidad, se configura sin necesidad de ninguna configuración adicional. La información se proporciona si es necesario cambiar la configuración predeterminada.

### Configurar la Lista de mensajes (cuadro de mensaje) {#configure-message-list-message-box}

Para modificar la configuración de la lista de mensajes para las páginas **Bandeja de entrada**, **Elementos enviados** y **Papelera** de la función de mensajería, abra el sitio en [modo de edición del autor](/help/communities/sites-console.md#authoring-site-content).

1. En el modo `Preview`, seleccione el vínculo **Mensajes** para abrir la página de mensajería principal. A continuación, seleccione **Bandeja de entrada**, **Elementos enviados** o **Papelera** para configurar el componente para esa lista de mensajes.

1. En el modo `Edit`, seleccione el componente en la página.
1. Para acceder al cuadro de diálogo de configuración, seleccione el icono `link` para cancelar la herencia.
Una vez cancelada la herencia, es posible seleccionar el icono de configuración para abrir el cuadro de diálogo de configuración.

1. Una vez completada la configuración, es necesario restaurar la herencia seleccionando el icono `broken link`.

![configure-message-lista](assets/configure-message-list.png)

#### Ficha básica {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **Selector de servicio**

   (*Requerido*) Establezca esto en el valor de la propiedad **`serviceSelector.name`** del [Servicio de operaciones de mensajería de AEM Communities](/help/communities/messaging.md#messaging-operations-service).

* **Componer página**

   (*Requerido*) La página que se abrirá cuando un miembro haga clic en el botón **`Reply`**. La página de destinatario debe contener el formulario **Redactar mensaje**.

* **Responder/Ver como medio**

   Si se selecciona, la URL de respuesta y la URL de Vista harán referencia a un recurso; de lo contrario, los datos se pasarán como parámetros de consulta en la URL.

* **Formulario para mostrar perfil**

   Formulario de perfil que se va a utilizar para mostrar el perfil de remitentes.

* **Carpeta Papelera**

   Si se selecciona, este componente de Lista de mensajes solo muestra los mensajes marcados como eliminados (papelera).

* **Rutas de carpeta**

   (*Requerido*) Al hacer referencia a los valores establecidos para **inbox.path.name** y **sentiitems.path.name** en el [Servicio de operaciones de mensajería de AEM Communities](/help/communities/messaging.md#messaging-operations-service). Al configurar para un `Inbox`, agregue una entrada usando el valor de **inbox.path.name**. Al configurar para un `Outbox`, agregue una entrada usando el valor de **sentiitems.path.name**. Al configurar para `Trash`, agregue dos entradas con ambos valores.

#### Mostrar ficha {#display-tab}

![display-tab-message-lista](assets/display-tab-message-list.png)

* **Marcar botón de lectura**

   Si se selecciona, muestra un botón `Read`que permite marcar un mensaje como leído.

* **Botón Marcar no leído**

   Si se selecciona, muestra un botón `Mark Unread` que permite marcar un mensaje como leído.

* **Botón Eliminar**

   Si se selecciona, muestra un botón `Delete` que permite marcar un mensaje como leído. Duplicado la funcionalidad de eliminación si también se selecciona **`Message Options`**.

* **Opciones de mensaje**

   Si se selecciona, muestra los botones **`Reply`**, **`Reply All`**, **`Forward`** y **`Delete`**, lo que permite enviar o eliminar un mensaje. Duplicado la funcionalidad de eliminación si también se selecciona **`Delete Button`**.

* **Mensajes por página**

   El número especificado es el número máximo de mensajes que se muestran por página en un esquema de paginación. Si no se especifica ningún número (se deja en blanco), se muestran todos los mensajes y no hay paginación.

* **Patrones de marca de hora**

   Proporcione patrones de marca de hora para uno o más idiomas. El valor predeterminado es en, de, fr, it, es, ja, zh_CN, ko_KR.

* **Mostrar usuario**

   Elija **`Sender`** o **`Recipients`** para determinar si desea mostrar el remitente o los Destinatarios.

### Configurar mensaje de composición {#configure-compose-message}

Para modificar la configuración de la página de mensaje de composición, abra el sitio en [modo de edición del autor](/help/communities/sites-console.md#authoring-site-content).

* En el modo `Preview`, seleccione el vínculo **Mensajes** para abrir la página de mensajería principal. A continuación, seleccione el botón Nuevo mensaje para abrir la página `Compose Message`.

* En el modo `Edit`, seleccione el componente principal en la página que contiene el cuerpo del mensaje.
* Para acceder al cuadro de diálogo de configuración, seleccione el icono `link` para cancelar la herencia.
Una vez cancelada la herencia, es posible seleccionar el icono de configuración para abrir el cuadro de diálogo de configuración.

* Una vez completada la configuración, es necesario restaurar la herencia seleccionando el icono `broken link`.

![config-compose-message](assets/config-compose-message.png)

#### Ficha básica {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **Dirección URL de redireccionamiento**

   Introduzca la dirección URL de la página que se muestra después de enviar el mensaje. Por ejemplo, `../messaging.html`.

* **URL de cancelación**

   Introduzca la dirección URL de la página mostrada si el remitente cancela el mensaje. Por ejemplo, `../messaging.html`.

* **Longitud máxima del asunto del mensaje**

   El número máximo de caracteres permitidos en el campo Asunto. Por ejemplo, 500. El valor predeterminado no es límite.

* **Longitud máxima del cuerpo del mensaje**

   El número máximo de caracteres permitidos en el campo Contenido. Por ejemplo, 10000. El valor predeterminado no es límite.

* **Selector de servicio**

   (*Requerido*) Establezca esto en el valor de la propiedad **`serviceSelector.name`** del [Servicio de operaciones de mensajería de AEM Communities](/help/communities/messaging.md#messaging-operations-service).

#### Mostrar ficha {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **Mostrar campo de asunto**

   Si se selecciona, muestre el campo `Subject` y habilite la adición de un asunto al mensaje. El valor predeterminado no está marcado.

* **Etiqueta de asunto**

   Escriba el texto que desea mostrar junto al campo `Subject`. El valor predeterminado es `Subject`.

* **Mostrar el campo Adjuntar archivo**

   Si se selecciona, muestre el campo `Attachment` y habilite la adición de archivos adjuntos al mensaje. El valor predeterminado no está marcado.

* **Etiqueta de archivo adjunto**

   Escriba el texto que desea mostrar junto al campo `Attachment`. El valor predeterminado es **`Attach File`**.

* **Mostrar campo de contenido**

   Si se selecciona, muestre el campo `Content` y habilite la adición de un cuerpo de mensaje. El valor predeterminado no está marcado.

* **Etiqueta de contenido**

   Escriba el texto que desea mostrar junto al campo `Content`. El valor predeterminado es **`Body`**.

* **Con editor de texto enriquecido**

   Si se selecciona, indica el uso de un cuadro de texto de contenido personalizado con su propio editor de texto enriquecido. El valor predeterminado no está marcado.

* **Patrones de marca de hora**

   Proporcione patrones de marca de hora para uno o más idiomas. El valor predeterminado es en, de, fr, it, es, ja, zh_CN, ko_KR.

