---
title: Función de mensajería
description: Aprenda a configurar la función Mensajería de AEM Communities para permitir que los miembros de la comunidad interactúen entre sí de forma más privada.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: d121dc05-7d15-44ba-8d2d-b59d6c6480c8
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---

# Función de mensajería {#messaging-feature}

Además de las interacciones visibles públicamente que se producen en los foros y comentarios, la función de mensajería de AEM Communities permite a los miembros de la comunidad interactuar entre sí de forma más privada.

Esta característica se puede incluir cuando se crea un [sitio de la comunidad](/help/communities/overview.md#communitiessites).

La función de mensajería le permite hacer lo siguiente:

**A** - enviar un mensaje a uno o más miembros de la comunidad

**B** - enviar mensajes directos en [lotes a grupos de miembros de la comunidad](/help/communities/messaging.md#group-messaging)

**C** - enviar un mensaje con datos adjuntos

**D** - reenviar un mensaje

**E** - responder a un mensaje

**F** - eliminar un mensaje

**G** - restaurar un mensaje eliminado

![sección de mensajería](assets/messaging-section.png)

![mensaje de restauración](assets/restore-message.png)

Para activar y modificar la función de mensajería, consulte:

* [Configurar la mensajería](/help/communities/messaging.md) para administradores
* [Messaging Essentials](/help/communities/essentials-messaging.md) para desarrolladores

>[!NOTE]
>
>No se admite agregar componentes de `Compose Message, Message, or Message List` (que se encuentran en el grupo de componentes `Communities`) a una página en modo de edición de autor.

## Configuración de componentes de mensajería {#configure-messaging-components}

Cuando la mensajería está habilitada para un sitio de la comunidad, se configura sin necesidad de ninguna otra configuración. Se proporciona la información si es necesario cambiar la configuración predeterminada.

### Configuración de la lista de mensajes (cuadro de mensaje) {#configure-message-list-message-box}

Para modificar la configuración de la lista de mensajes de **Bandeja de entrada**, **Elementos enviados** y **Papelera** de la función de mensajería, abre el sitio en [modo de edición de autor](/help/communities/sites-console.md#authoring-site-content).

1. En el modo `Preview`, seleccione el vínculo **Mensajes** para abrir la página principal de mensajería. A continuación, seleccione **Bandeja de entrada**, **Elementos enviados** o **Papelera** para configurar el componente de esa lista de mensajes.

1. En el modo `Edit`, seleccione el componente en la página.
1. Para acceder al cuadro de diálogo de configuración, cancele la herencia seleccionando el icono `link`.
Una vez cancelada la herencia, es posible seleccionar el icono de configuración para abrir el cuadro de diálogo de configuración.

1. Una vez completada la configuración, es necesario restaurar la herencia seleccionando el icono `broken link`.

![configure-message-list](assets/configure-message-list.png)

#### Pestaña Básico {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **Selector de servicio**

  (*Obligatorio*) Establezca este valor en el valor de la propiedad **`serviceSelector.name`** del [Servicio de operaciones de mensajería de AEM Communities](/help/communities/messaging.md#messaging-operations-service).

* **Escribir página**

  (*Obligatorio*) La página que se abrirá cuando un miembro haga clic en el botón **`Reply`**. La página de destino debe contener el formulario **Escribir mensaje**.

* **Responder/Ver como medio**

  Si se selecciona, la URL de respuesta y la URL de visualización hacen referencia a un recurso o, de lo contrario, los datos se pasan como parámetros de consulta en la URL.

* **Formulario para mostrar el perfil**

  Formulario de perfil que se utilizará para mostrar el perfil del remitente.

* **Carpeta de papelera**

  Si se selecciona, este componente Lista de mensajes solo muestra los mensajes marcados como eliminados (papelera).

* **Rutas de carpeta**

  (*Obligatorio*) Hacer referencia a los valores establecidos para **inbox.path.name** y **sentitems.path.name** en el [Servicio de operaciones de mensajería de AEM Communities](/help/communities/messaging.md#messaging-operations-service). Al configurar para un `Inbox`, agregue una entrada con el valor de **inbox.path.name**. Al configurar para un `Outbox`, agregue una entrada con el valor de **sentitems.path.name**. Al configurar para `Trash`, agregue dos entradas con ambos valores.

#### Pestaña Mostrar {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **Marcar botón de lectura**

  Si se selecciona esta opción, se muestra un botón `Read` que permite marcar un mensaje como leído.

* **Marcar botón no leído**

  Si se selecciona esta opción, se muestra un botón `Mark Unread` que permite marcar un mensaje como leído.

* **Botón Eliminar**

  Si se selecciona esta opción, se muestra un botón `Delete` que permite marcar un mensaje como leído. Duplica la funcionalidad de eliminación si **`Message Options`** también está marcado.

* **Opciones de mensaje**

  Si se selecciona esta opción, se muestran los botones **`Reply`**, **`Reply All`**, **`Forward`** y **`Delete`** que permiten que un mensaje se reenvíe o elimine. Duplica la funcionalidad de eliminación si **`Delete Button`** también está marcado.

* **Mensajes por página**

  El número especificado es el número máximo de mensajes mostrados por página en un esquema de paginación. Si no se especifica ningún número (se deja en blanco), se muestran todos los mensajes y no hay paginación.

* **Patrones de marca de tiempo**

  Proporcione patrones de marca de tiempo para uno o más idiomas. El valor predeterminado es en, de, fr, it, es, ja, zh_CN, ko_KR.

* **Mostrar usuario**

  Elija **`Sender`** o **`Recipients`** para que pueda determinar si desea mostrar el remitente o los destinatarios.

### Configurar mensaje de redacción {#configure-compose-message}

Para modificar la configuración de la página de redacción del mensaje, abra el sitio en [modo de edición de autor](/help/communities/sites-console.md#authoring-site-content).

* En el modo `Preview`, seleccione el vínculo **Mensajes** para abrir la página principal de mensajería. A continuación, seleccione el botón Nuevo mensaje para poder abrir la página `Compose Message`.

* En el modo `Edit`, seleccione el componente principal de la página que contiene el cuerpo del mensaje.
* Para acceder al cuadro de diálogo de configuración, cancele la herencia seleccionando el icono `link`.
Una vez cancelada la herencia, es posible seleccionar el icono de configuración para abrir el cuadro de diálogo de configuración.

* Una vez completada la configuración, es necesario restaurar la herencia seleccionando el icono `broken link`.

![config-compose-message](assets/config-compose-message.png)

#### Pestaña Básico {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **URL de redireccionamiento**

  Introduzca la dirección URL de la página que se muestra después de enviar el mensaje. Por ejemplo, `../messaging.html`.

* **Cancelar URL**

  Introduzca la dirección URL de la página que se muestra si el remitente cancela el mensaje. Por ejemplo, `../messaging.html`.

* **Longitud máxima del asunto del mensaje**

  Número máximo de caracteres permitidos en el campo Asunto. Por ejemplo, 500. El valor predeterminado es sin límite.

* **Longitud máxima del cuerpo del mensaje**

  Número máximo de caracteres permitidos en el campo Contenido. Por ejemplo, 10000. El valor predeterminado es sin límite.

* **Selector de servicio**

  (*Obligatorio*) Establezca este valor en el valor de la propiedad **`serviceSelector.name`** del [Servicio de operaciones de mensajería de AEM Communities](/help/communities/messaging.md#messaging-operations-service).

#### Pestaña Mostrar {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **Mostrar campo de asunto**

  Si se selecciona, se muestra el campo `Subject` y se habilita la adición de un asunto al mensaje. El valor predeterminado no está marcado.

* **Etiqueta de asunto**

  Escriba el texto que desea mostrar junto al campo `Subject`. El valor predeterminado es `Subject`.

* **Mostrar campo de archivo adjunto**

  Si se selecciona, se muestra el campo `Attachment` y se habilita la adición de archivos adjuntos al mensaje. El valor predeterminado no está marcado.

* **Adjuntar etiqueta de archivo**

  Escriba el texto que desea mostrar junto al campo `Attachment`. El valor predeterminado es **`Attach File`**.

* **Mostrar campo de contenido**

  Si se selecciona, se muestra el campo `Content` y se habilita la adición de un cuerpo de mensaje. El valor predeterminado no está marcado.

* **Etiqueta de contenido**

  Escriba el texto que desea mostrar junto al campo `Content`. El valor predeterminado es **`Body`**.

* **Con Editor De Texto Enriquecido**

  Si se selecciona esta opción, se indica el uso de un cuadro de texto de contenido personalizado con su propio editor de texto enriquecido. El valor predeterminado no está marcado.

* **Patrones de marca de tiempo**

  Proporcione patrones de marca de tiempo para uno o más idiomas. El valor predeterminado es en, de, fr, it, es, ja, zh_CN, ko_KR.
