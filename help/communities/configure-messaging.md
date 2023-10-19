---
title: Función de mensajería
description: Aprenda a configurar la función Mensajería de AEM Communities para permitir que los miembros de la comunidad interactúen entre sí de forma más privada.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: d121dc05-7d15-44ba-8d2d-b59d6c6480c8
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 5%

---

# Función de mensajería {#messaging-feature}

Además de las interacciones visibles públicamente que se producen en los foros y comentarios, la función de mensajería de AEM Communities permite a los miembros de la comunidad interactuar entre sí de forma más privada.

Esta función se puede incluir cuando se crea un [sitio comunitario](/help/communities/overview.md#communitiessites) se ha creado.

La función de mensajería le permite hacer lo siguiente:

**A** - enviar un mensaje a uno o varios miembros de la comunidad

**B** - enviar mensajes directos en [a grupos de miembros de la comunidad](/help/communities/messaging.md#group-messaging)

**C** - enviar un mensaje con datos adjuntos

**D** - reenviar un mensaje

**E** - responder a un mensaje

**F** - eliminar un mensaje

**G** - restaurar un mensaje eliminado

![messaging-section](assets/messaging-section.png)

![restore-message](assets/restore-message.png)

Para activar y modificar la función de mensajería, consulte:

* [Configurar la mensajería](/help/communities/messaging.md) para administradores
* [Messaging Essentials](/help/communities/essentials-messaging.md) para desarrolladores

>[!NOTE]
>
>No se admite agregar `Compose Message, Message, or Message List` componentes (se encuentran en `Communities`grupo de componentes) a una página en modo de edición de autor.

## Configuración de componentes de mensajería {#configure-messaging-components}

Cuando la mensajería está habilitada para un sitio de la comunidad, se configura sin necesidad de ninguna otra configuración. Se proporciona la información si es necesario cambiar la configuración predeterminada.

### Configuración de la lista de mensajes (cuadro de mensaje) {#configure-message-list-message-box}

Para modificar la configuración de la lista de mensajes de **Bandeja de entrada**, **Elementos enviados**, y **Papelera** páginas de la función de mensajería, abra el sitio en [modo de edición de autor](/help/communities/sites-console.md#authoring-site-content).

1. Entrada `Preview` modo, seleccione la **Mensajes** para abrir la página principal de mensajería. A continuación, seleccione **Bandeja de entrada**, **Elementos enviados** o **Papelera** para configurar el componente para esa lista de mensajes.

1. Entrada `Edit` modo, seleccione el componente en la página.
1. Para acceder al cuadro de diálogo de configuración, cancele la herencia seleccionando `link` icono.
Una vez cancelada la herencia, es posible seleccionar el icono de configuración para abrir el cuadro de diálogo de configuración.

1. Una vez completada la configuración, es necesario restaurar la herencia seleccionando la variable `broken link` icono.

![configure-message-list](assets/configure-message-list.png)

#### Pestaña Básicos {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **Selector de servicio**

  (*Requerido*) Establezca este valor en el valor de la propiedad **`serviceSelector.name`** desde el [Servicio de operaciones de mensajería de AEM Communities](/help/communities/messaging.md#messaging-operations-service).

* **Página de composición**

  (*Requerido*) La página que se abrirá cuando un miembro haga clic en **`Reply`** botón. La página de destino debe contener el **Escribir mensaje** formulario.

* **Responder/Ver como medio**

  Si se selecciona, la URL de respuesta y la URL de visualización hacen referencia a un recurso o, de lo contrario, los datos se pasan como parámetros de consulta en la URL.

* **Formulario de visualización de perfil**

  Formulario de perfil que se utilizará para mostrar el perfil del remitente.

* **Carpeta de papelera**

  Si se selecciona, este componente Lista de mensajes solo muestra los mensajes marcados como eliminados (papelera).

* **Rutas de carpeta**

  (*Requerido*) Referencia a los valores establecidos para **inbox.path.name** y **sentitems.path.name** en el [Servicio de operaciones de mensajería de AEM Communities](/help/communities/messaging.md#messaging-operations-service). Al configurar para un `Inbox`, agregue una entrada con el valor **inbox.path.name**. Al configurar para un `Outbox`, agregue una entrada con el valor **sentitems.path.name**. Al configurar para `Trash`, agregue dos entradas con ambos valores.

#### Pestaña Mostrar {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **Botón Marcar lectura**

  Si se selecciona, muestra un `Read`que permite marcar un mensaje como leído.

* **Botón Marcar como no leído**

  Si se selecciona, muestra un `Mark Unread` que permite marcar un mensaje como leído.

* **Botón Eliminar**

  Si se selecciona, muestra un `Delete` que permite marcar un mensaje como leído. Duplica la funcionalidad de eliminación si **`Message Options`** también está marcada.

* **Opciones de mensaje**

  Si se selecciona, se muestra **`Reply`**, **`Reply All`**, **`Forward`**, y **`Delete`** botones que permiten reenviar o eliminar un mensaje. Duplica la funcionalidad de eliminación si **`Delete Button`** también está marcada.

* **Mensajes por página**

  El número especificado es el número máximo de mensajes mostrados por página en un esquema de paginación. Si no se especifica ningún número (se deja en blanco), se muestran todos los mensajes y no hay paginación.

* **Patrones de marca de hora**

  Proporcione patrones de marca de tiempo para uno o más idiomas. El valor predeterminado es en, de, fr, it, es, ja, zh_CN, ko_KR.

* **Mostrar usuario**

  Elija una de estas opciones **`Sender`** o **`Recipients`** para que pueda determinar si desea mostrar el remitente o los destinatarios.

### Configurar mensaje de redacción {#configure-compose-message}

Para modificar la configuración de la página de redacción del mensaje, abra el sitio en [modo de edición de autor](/help/communities/sites-console.md#authoring-site-content).

* Entrada `Preview` modo, seleccione la **Mensajes** para abrir la página principal de mensajería. A continuación, seleccione el botón Nuevo mensaje para poder abrir `Compose Message` página.

* Entrada `Edit` , seleccione el componente principal en la página que contiene el cuerpo del mensaje.
* Para acceder al cuadro de diálogo de configuración, cancele la herencia seleccionando `link` icono.
Una vez cancelada la herencia, es posible seleccionar el icono de configuración para abrir el cuadro de diálogo de configuración.

* Una vez completada la configuración, es necesario restaurar la herencia seleccionando la variable `broken link` icono.

![config-compose-message](assets/config-compose-message.png)

#### Pestaña Básicos {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **URL de redireccionamiento**

  Introduzca la dirección URL de la página que se muestra después de enviar el mensaje. Por ejemplo, `../messaging.html`.

* **URL de cancelación**

  Introduzca la dirección URL de la página que se muestra si el remitente cancela el mensaje. Por ejemplo, `../messaging.html`.

* **Longitud máxima del asunto del mensaje**

  Número máximo de caracteres permitidos en el campo Asunto. Por ejemplo, 500. El valor predeterminado es sin límite.

* **Longitud máxima del cuerpo del mensaje**

  Número máximo de caracteres permitidos en el campo Contenido. Por ejemplo, 10000. El valor predeterminado es sin límite.

* **Selector de servicio**

  (*Requerido*) Establezca este valor en el valor de la propiedad **`serviceSelector.name`** desde el [Servicio de operaciones de mensajería de AEM Communities](/help/communities/messaging.md#messaging-operations-service).

#### Pestaña Mostrar {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **Mostrar campo de asunto**

  Si se selecciona, se muestra el `Subject` y permiten añadir un asunto al mensaje. El valor predeterminado no está marcado.

* **Etiqueta del asunto**

  Introduzca el texto que desea mostrar junto al `Subject` field. El valor predeterminado es `Subject`.

* **Mostrar el campo Adjuntar archivo**

  Si se selecciona, se muestra el `Attachment` y habilite la adición de archivos adjuntos al mensaje. El valor predeterminado no está marcado.

* **Etiqueta de archivo adjunto**

  Introduzca el texto que desea mostrar junto al `Attachment` field. El valor predeterminado es **`Attach File`**.

* **Mostrar campo de contenido**

  Si se selecciona, se muestra el `Content` y permiten añadir un cuerpo del mensaje. El valor predeterminado no está marcado.

* **Etiqueta de contenido**

  Introduzca el texto que desea mostrar junto al `Content` field. El valor predeterminado es **`Body`**.

* **Con editor de texto enriquecido**

  Si se selecciona esta opción, se indica el uso de un cuadro de texto de contenido personalizado con su propio editor de texto enriquecido. El valor predeterminado no está marcado.

* **Patrones de marca de hora**

  Proporcione patrones de marca de tiempo para uno o más idiomas. El valor predeterminado es en, de, fr, it, es, ja, zh_CN, ko_KR.
