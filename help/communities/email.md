---
title: Configuración del correo electrónico
seo-title: Configuración del correo electrónico
description: Configuración de correo electrónico para Communities
seo-description: Configuración de correo electrónico para Communities
uuid: e8422cc2-1594-43b0-b587-82825636cec1
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: b4d38e45-eaa0-4ace-a885-a2e84fdfd5a1
pagetitle: Configuring Email
role: Administrador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 3%

---


# Configuración del correo electrónico {#configuring-email}

AEM Communities utiliza el correo electrónico para:

* [Notificaciones de comunidades](notifications.md)
* [Suscripciones de Communities](subscriptions.md)

De forma predeterminada, la función de correo electrónico no funciona, ya que requiere la especificación de un servidor SMTP y un usuario SMTP.

>[!CAUTION]
>
>El correo electrónico para notificaciones y suscripciones solo debe configurarse en el [publicador principal](deploy-communities.md#primary-publisher).

## Configuración predeterminada del servicio de correo {#default-mail-service-configuration}

El servicio de correo predeterminado es necesario tanto para notificaciones como para suscripciones.

* Inicie sesión en el editor principal con privilegios de administrador y acceda a la [Consola Web](../../help/sites-deploying/configuring-osgi.md):

   * Por ejemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Busque `Day CQ Mail Service`.
* Seleccione el icono de edición.

Esto se basa en la documentación de [Configuring Email Notification](../../help/sites-administering/notification.md), pero con una diferencia en que el campo `"From" address` es *no* necesario y debe dejarse vacío.

Por ejemplo (rellenado con valores solo con fines ilustrativos):

![email-config](assets/email-config.png)

* **[!UICONTROL Nombre de host del servidor SMTP]**

   *(Obligatorio)* El servidor SMTP que se va a utilizar.

* **[!UICONTROL Puerto del servidor SMTP]**

   *(Obligatorio)* El puerto del servidor SMTP debe ser de 25 o superior.

* **[!UICONTROL Usuario SMTP]**

   *(Obligatorio)* El usuario SMTP.

* **[!UICONTROL Contraseña SMTP]**

   *(Obligatorio)* La contraseña del usuario SMTP.

* **[!UICONTROL Dirección &quot;De&quot;]**

   Dejar vacío
* **[!UICONTROL SMTP utiliza SSL]**

   Si está marcada esta opción, envía un correo electrónico seguro. Asegúrese de que el puerto está configurado en 465 o como se requiere para el servidor SMTP.
* **[!UICONTROL Depurar correo electrónico]**

   Si se selecciona, habilita el registro de interacciones del servidor SMTP.

## Configuración de correo electrónico de AEM Communities {#aem-communities-email-configuration}

Una vez configurado el [servicio de correo predeterminado](#default-mail-service-configuration), las dos instancias existentes de la configuración `AEM Communities Email Reply Configuration` OSGi, incluidas en la versión, se vuelven funcionales.

Solo es necesario configurar la instancia de las suscripciones al permitir la respuesta por correo electrónico.

1. [](#configuration-for-notifications) Instancia de correo electrónico:

   En el caso de las notificaciones, que no admiten correo electrónico de respuesta y no deben modificarse.

1. [Subscriptions-](#configuration-for-subscriptions) email instance:

   Requiere configuración para habilitar completamente la creación de publicaciones a partir del correo electrónico de respuesta.

Para llegar a las instancias de configuración de correo electrónico de Communities:

* Inicie sesión en el editor principal con privilegios de administrador y acceda a la [Consola Web](../../help/sites-deploying/configuring-osgi.md)

   * Por ejemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Busque `AEM Communities Email Reply Configuration`.

![email-reply-config](assets/email-reply-config.png)

### Configuración de notificaciones {#configuration-for-notifications}

La instancia de `AEM Communities Email Reply Configuration` configuración OSGi con el correo electrónico Nombre es la función de notificaciones. Esta función no incluye la respuesta por correo electrónico.

Esta configuración no debe modificarse.

* Busque `AEM Communities Email Reply Configuration`.
* Seleccione el icono de edición.
* Compruebe que **Name** sea `email`.

* Compruebe que **Crear anuncio a partir del correo electrónico de respuesta** es `unchecked`.

![configure-email-reply](assets/configure-email-reply.png)

### Configuración de suscripciones {#configuration-for-subscriptions}

Para suscripciones de Communities, es posible activar o desactivar la capacidad de un miembro de publicar contenido respondiendo a un correo electrónico.

* Busque `AEM Communities Email Reply Configuration`.
* Seleccione el icono de edición.
* Compruebe que **Name** sea `subscriptions-email`.

   ![configure-email-subscription](assets/configure-email-subscriptions.png)

* **[!UICONTROL Nombre]**

   *(Requerido)* `subscriptions-email`. No Edite.

* **[!UICONTROL Crear publicación a partir del correo electrónico de respuesta]**

   Si se selecciona, el destinatario del correo electrónico de suscripción puede anunciar contenido enviando una respuesta. El valor predeterminado está marcado.
* **[!UICONTROL Agregar id rastreado al encabezado]**

   El valor predeterminado es `Reply-To`.

* **[!UICONTROL Longitud máxima del asunto]**

   Si se agrega el id de rastreador a la línea de asunto, esta es la longitud máxima del asunto, excluyendo el id rastreado, tras lo cual se recortará. Tenga en cuenta que esto debe ser lo más pequeño posible para evitar que se pierda la información de identificación rastreada. El valor predeterminado es 200.

* **[!UICONTROL Dirección de correo electrónico &quot;Responder&quot;]**

   Dirección que se utiliza como dirección de correo electrónico &quot;Responder&quot;. El valor predeterminado es `no-reply@example.com`.

* **[!UICONTROL Responder al delimitador]**

   Si se agrega el id de rastreador al encabezado Responder, se utilizará este delimitador. El valor predeterminado es `+` (signo más).

* **[!UICONTROL Prefijo de ID del rastreador en el asunto]**

   Si se agrega el id de rastreador a la línea de asunto, se utilizará este prefijo. El valor predeterminado es `post#`.

* **[!UICONTROL Prefijo de id del rastreador en el cuerpo del mensaje]**

   Si se agrega el id del rastreador al cuerpo del mensaje, se utilizará este prefijo. El valor predeterminado es `Please do not remove this:`.

* **[!UICONTROL Enviar correo electrónico como HTML]**: Si se selecciona, Content-Type of email se establecerá como  `"text/html;charset=utf-8"`. El valor predeterminado está marcado.

* **[!UICONTROL Nombre de usuario predeterminado]**

   Este nombre no se utilizará para usuarios sin nombre. El valor predeterminado es `no-reply@example.com`.

* **[!UICONTROL Ruta raíz de plantillas]**

   El correo electrónico se genera mediante la plantilla almacenada en esta ruta raíz. El valor predeterminado es `/etc/community/templates/subscriptions-email`.

## Configurar el importador de encuestas {#configure-polling-importer}

Para que el correo electrónico se introduzca en el repositorio, es necesario configurar un importador de encuestas y configurar sus propiedades en el repositorio manualmente.

### Agregar nuevo importador de encuestas {#add-new-polling-importer}

* Inicie sesión en el editor principal con privilegios de administrador y vaya a la consola del importador de encuestas:

   Por ejemplo, [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* Seleccione **[!UICONTROL Add]**

   ![polling-importer](assets/polling-importer.png)

* **[!UICONTROL Tipo]**

   *(Obligatorio)* Desplegable para seleccionar  `POP3 (over SSL)`.

* **[!UICONTROL URL]**

   *(Obligatorio)* El servidor de correo saliente. Por ejemplo, `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`.

* **[!UICONTROL Importar a Path]**&amp;ast;

   *(Obligatorio)* Configúrelo en  `/content/usergenerated/mailFolder/postEmails`
navegando hasta la  `postEmails`carpeta y seleccione  **Aceptar**.

* **[!UICONTROL Actualizar intervalo en segundos]**

   *(Opcional)* El servidor de correo configurado para el servicio de correo predeterminado puede tener requisitos con respecto al valor del intervalo de actualización. Por ejemplo, Gmail puede requerir un intervalo de `300`.

* **[!UICONTROL Inicio de sesión]**

   *(Opcional)*

* **[!UICONTROL Contraseña]**

   *(Opcional)*

* Seleccione **[!UICONTROL OK]**.

### Ajustar protocolo para nuevo importador de encuestas {#adjust-protocol-for-new-polling-importer}

Una vez guardada la nueva configuración de sondeo, es necesario modificar las propiedades del importador de correo electrónico de suscripción para cambiar el protocolo de `POP3` a `emailreply`.

Uso del [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Inicie sesión en el editor principal con privilegios de administrador y vaya a [https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importadores/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling).
* Seleccione la configuración recién creada y modifique las siguientes propiedades:

   * **feedType**: Reemplazar  `pop3s` por  **`emailreply`**
   * **fuente**: Reemplazar el protocolo del origen  `pop3s://` por  **`emailreply://`**

![sonling-protocol](assets/polling-protocol.png)

Los triángulos rojos indican las propiedades modificadas. Asegúrese de guardar los cambios:

* Seleccione **[!UICONTROL Guardar todo]**.

