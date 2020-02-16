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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Función de mensajería{#messaging-feature}

Además de las interacciones públicamente visibles que se producen en los foros y comentarios, la función de mensajería de** **Comunidades AEM permite a los miembros de la comunidad interactuar entre sí de forma más privada.

Esta función se puede incluir cuando se crea un sitio [de](/help/communities/overview.md#communitiessites) comunidad.

La función de mensajería permite:

**A** - enviar un mensaje a uno o varios miembros **de la comunidad** - enviar mensajes directos [masivamente a los grupos](/help/communities/messaging.md#group-messaging)miembros de la comunidad **C** - enviar un mensaje con datos adjuntos **D** - enviar un mensaje**E - **responder a un mensaje **** F - eliminar un mensaje**G **- restaurar un mensaje eliminado

![messaging-section](assets/messaging-section.png) ![restore-message](assets/restore-message.png)

Para habilitar y modificar la función de mensajería, consulte:

* [Configuración de la mensajería](/help/communities/messaging.md) para administradores
* [Esenciales](/help/communities/essentials-messaging.md) de mensajería para desarrolladores

>[!NOTE]
>
>No se pueden agregar `Compose Message, Message, or Message List` componentes (que se encuentran en el grupo de `Communities`componentes) a una página en modo de edición de autor.

## Configuración de componentes de mensajería {#configure-messaging-components}

Cuando se habilita la mensajería para un sitio de comunidad, se configura sin necesidad de ninguna configuración adicional. La información se proporciona si es necesario cambiar la configuración predeterminada.

### Configurar lista de mensajes (cuadro de mensaje) {#configure-message-list-message-box}

Para modificar la configuración de la lista de mensajes para la **Bandeja de entrada**, Elementos **** enviados y **Papelera **páginas de la función de mensajería, abra el sitio en modo [de edición de](/help/communities/sites-console.md#authoring-site-content)autor.

1. En `Preview`modo, seleccione el vínculo **Mensajes **para abrir la página de mensajes principal. A continuación, seleccione **Bandeja de entrada**, **Elementos enviados **o **Papelera **para configurar el componente para esa lista de mensajes.

1. En `Edit` modo, seleccione el componente en la página.
1. Para acceder al cuadro de diálogo de configuración, seleccione el `link`icono para cancelar la herencia.
Una vez cancelada la herencia, es posible seleccionar el icono de configuración para abrir el cuadro de diálogo de configuración.

1. Una vez completada la configuración, es necesario restaurar la herencia seleccionando el `broken link` icono .

![configure-message-list](assets/configure-message-list.png)

#### Basic tab {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **Selector** de servicio (*obligatorio*) Establezca este valor en el valor de la propiedad**`serviceSelector.name`*** del servicio [de operaciones de mensajería de comunidades de](/help/communities/messaging.md#messaging-operations-service)AEM.

* **Página** de composición (*obligatoria*) La página que se abrirá cuando un miembro haga clic en el botón **`Reply`**s. La página de destino debe contener el formulario **Redactar mensaje** .

* **Responder/Ver como recurso** Si se selecciona, la URL de respuesta y la URL de vista harán referencia a un recurso; de lo contrario, los datos se pasarán como parámetros de consulta en la URL.

* **Formulario** de visualización de perfilFormulario de perfil que se utiliza para mostrar el perfil de los remitentes.

* **Carpeta** de papelera Si está activada, este componente Lista de mensajes solo muestra los mensajes marcados como eliminados (papelera).

* **Rutas** de carpeta (*obligatorio*) Referencia a los valores configurados para **inbox.path.name** y **sentitems.path.name **en el servicio [de operaciones de mensajería de](/help/communities/messaging.md#messaging-operations-service)AEM Communities. Al configurar para un `Inbox`, agregue una entrada usando el valor de **inbox.path.name**. Al configurar para un `Outbox`, agregue una entrada usando el valor de **sentitómesis.path.name**. Al configurar para `Trash`, agregue dos entradas con ambos valores.

#### Ficha Mostrar {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **Marcar botón** de lectura Si está activado, muestra un `Read`botón que permite marcar un mensaje como leído.

* **Marcar botón** no leído Si está activado, muestra un `Mark Unread` botón que permite marcar un mensaje como leído.

* **Botón** Eliminar Si está activado, muestra un `Delete`botón que permite marcar un mensaje como leído. Se duplicará la funcionalidad de eliminación si también **`Message Options`** está marcada.

* **Opciones** de mensaje Si está activada, muestra **`Reply`**, **`Reply All`**, **`Forward`**y **`Delete`**botones que permiten que un mensaje se vuelva a enviar o se elimine. Se duplicará la funcionalidad de eliminación si también **`Delete Button`** está marcada.

* **Mensajes por página** El número especificado es el número máximo de mensajes que se muestran por página en un esquema de paginación. Si no se especifica ningún número (se deja en blanco), se muestran todos los mensajes y no hay paginación.

* **Patrones** de marca de hora Proporciona patrones de marca de hora para uno o más idiomas. El valor predeterminado es en, de, fr, it, es, ja, zh_CN, ko_KR.

* **Mostrar usuario** Elija **`Sender`**o **`Recipients`**para determinar si desea mostrar el remitente o los destinatarios.

### Configurar mensaje de composición {#configure-compose-message}

Para modificar la configuración de la página de mensaje de composición, abra el sitio en modo [de edición de](/help/communities/sites-console.md#authoring-site-content)autor.

* En `Preview`modo, seleccione el vínculo **Mensajes **para abrir la página de mensajes principal. A continuación, seleccione el botón Nuevo mensaje para abrir la `Compose Message` página.

* En `Edit` modo, seleccione el componente principal en la página que contiene el cuerpo del mensaje.
* Para acceder al cuadro de diálogo de configuración, seleccione el `link`icono para cancelar la herencia.
Una vez cancelada la herencia, es posible seleccionar el icono de configuración para abrir el cuadro de diálogo de configuración.

* Una vez completada la configuración, es necesario restaurar la herencia seleccionando el `broken link`icono.

![config-compose-message](assets/config-compose-message.png)

#### Basic tab {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **Dirección URL** de redirecciónIntroduzca la dirección URL de la página que se muestra después de enviar el mensaje. Por ejemplo, `../messaging.html`.

* **Cancelar URL** Introduzca la dirección URL de la página mostrada si el remitente cancela el mensaje. Por ejemplo, `../messaging.html`.

* **Longitud máxima del asunto** del mensaje El número máximo de caracteres permitidos en el campo Asunto. Por ejemplo, 500. El valor predeterminado no es límite.

* **Longitud máxima del cuerpo** del mensaje El número máximo de caracteres permitidos en el campo Contenido. Por ejemplo, 10000. El valor predeterminado no es límite.

* **Selector** de servicio (*obligatorio*) Establezca este valor en el valor de la propiedad**`serviceSelector.name`*** del servicio [de operaciones de mensajería de comunidades de](/help/communities/messaging.md#messaging-operations-service)AEM.

#### Ficha Mostrar {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **Mostrar campo** de asunto Si está activado, muestre el `Subject` campo y active la adición de un asunto al mensaje. El valor predeterminado no está marcado.

* **Etiqueta** AsuntoEscriba el texto que se mostrará junto al `Subject` campo. El valor predeterminado es `Subject`.

* **Mostrar campo** Adjuntar archivo si está activado, muestre el `Attachment` campo y habilite la adición de archivos adjuntos al mensaje. El valor predeterminado no está marcado.

* **Adjuntar etiqueta** de archivoIntroduzca el texto que desea mostrar junto al `Attachment` campo. El valor predeterminado es **`Attach File`**.

* **Mostrar campo** de contenido Si está activado, muestre el `Content` campo y habilite la adición de un cuerpo de mensaje. El valor predeterminado no está marcado.

* **Etiqueta** de contenidoIntroduzca el texto que desea mostrar junto al `Content` campo. El valor predeterminado es **`Body`**.

* **Con el Editor** de texto enriquecido Si está activado, indica el uso de un cuadro de texto de contenido personalizado con su propio editor de texto enriquecido. El valor predeterminado no está marcado.

* **Patrones** de marca de hora Proporciona patrones de marca de hora para uno o más idiomas. El valor predeterminado es en, de, fr, it, es, ja, zh_CN, ko_KR.

