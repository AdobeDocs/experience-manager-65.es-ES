---
title: Configurar correo electrónico
description: Obtenga información sobre cómo configurar notificaciones y suscripciones por correo electrónico para las comunidades de Adobe Experience Manager.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
pagetitle: Configuring Email
role: Admin
exl-id: bf97d388-f8ca-4e37-88e2-0c536834311e
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Configurar correo electrónico {#configuring-email}

AEM Communities utiliza el correo electrónico para:

* [Notificaciones de Communities](notifications.md)
* [Suscripciones de Communities](subscriptions.md)

De forma predeterminada, la función de correo electrónico no funciona, ya que requiere la especificación de un servidor SMTP y un usuario SMTP.

>[!CAUTION]
>
>El correo electrónico para notificaciones y suscripciones solo debe configurarse en la [editor principal](deploy-communities.md#primary-publisher).

## Configuración predeterminada del servicio de correo {#default-mail-service-configuration}

El servicio de correo predeterminado es necesario tanto para las notificaciones como para las suscripciones.

* Inicie sesión en el editor principal con privilegios de administrador y acceda al [Consola web](../../help/sites-deploying/configuring-osgi.md):

   * Por ejemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Busque el `Day CQ Mail Service`.
* Seleccione el icono de edición.

Se basa en la documentación de [Configuración de notificaciones por correo electrónico](../../help/sites-administering/notification.md), pero con una diferencia en que el campo `"From" address` es *no* obligatorio y debe dejarse vacío.

Por ejemplo, (rellenado con valores solo con fines ilustrativos):

![email-config](assets/email-config.png)

* **[!UICONTROL Nombre de host del servidor SMTP]**

  *(Obligatorio)* Servidor SMTP que se va a utilizar.

* **[!UICONTROL Puerto del servidor SMTP]**

  *(Obligatorio)* El puerto del servidor SMTP debe ser 25 o superior.

* **[!UICONTROL usuario de SMTP]**

  *(Obligatorio)* El usuario SMTP.

* **[!UICONTROL Contraseña SMTP]**

  *(Obligatorio)* La contraseña del usuario SMTP.

* **[!UICONTROL Dirección &quot;De&quot;]**

  Dejar vacío
* **[!UICONTROL SMTP: usar SSL]**

  Si se selecciona, envía un correo electrónico seguro. Asegúrese de que el puerto está establecido en 465 o como se requiere para un servidor SMTP.
* **[!UICONTROL Depurar correo electrónico]**

  Si se selecciona, se habilita el registro de interacciones del servidor SMTP.

## Configuración de correo electrónico de AEM Communities {#aem-communities-email-configuration}

Una vez que [servicio de correo predeterminado](#default-mail-service-configuration) está configurada, las dos instancias existentes del `AEM Communities Email Reply Configuration` La configuración OSGi, incluida en la versión, se vuelve funcional.

Solo la instancia de las suscripciones debe configurarse aún más al permitir la respuesta por correo electrónico.

1. [Correo electrónico](#configuration-for-notifications) instancia:

   Para las notificaciones, que no admite la respuesta por correo electrónico y no debe modificarse.

1. [Subscriptions-email](#configuration-for-subscriptions) instancia:

   Se requiere una configuración para habilitar completamente la creación de entradas a partir del correo electrónico de respuesta.

Para llegar a las instancias de configuración de correo electrónico de Communities:

* Inicie sesión en el editor principal con privilegios de administrador y acceda al [Consola web](../../help/sites-deploying/configuring-osgi.md)

   * Por ejemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localizar `AEM Communities Email Reply Configuration`.

![email-reply-config](assets/email-reply-config.png)

### Configuración para notificaciones {#configuration-for-notifications}

La instancia de `AEM Communities Email Reply Configuration` La configuración OSGi con el nombre de correo electrónico es la función de notificaciones. Esta función no incluye respuesta de correo electrónico.

No modifique esta configuración.

* Busque el `AEM Communities Email Reply Configuration`.
* Seleccione el icono de edición.
* Compruebe que la variable **Nombre** es `email`.

* Compruebe que **Crear entrada a partir del correo electrónico de respuesta** es `unchecked`.

![configure-email-reply](assets/configure-email-reply.png)

### Configuración para suscripciones {#configuration-for-subscriptions}

Para las suscripciones de Communities, es posible habilitar o deshabilitar la capacidad para que un miembro publique contenido al responder a un correo electrónico.

* Busque el `AEM Communities Email Reply Configuration`.
* Seleccione el icono de edición.
* Compruebe que la variable **Nombre** es `subscriptions-email`.

  ![configure-email-subscription](assets/configure-email-subscriptions.png)

* **[!UICONTROL Nombre]**

  *(Obligatorio)* `subscriptions-email`. No Editar.

* **[!UICONTROL Crear entrada a partir del correo electrónico de respuesta]**

  Si se selecciona, el destinatario de un correo electrónico de suscripción puede publicar contenido enviando una respuesta. La opción predeterminada está activada.
* **[!UICONTROL Añadir ID de seguimiento al encabezado]**

  El valor predeterminado es `Reply-To`.

* **[!UICONTROL Longitud máxima del asunto]**

  Si se añade un ID de rastreador a la línea de asunto, esta es la longitud máxima del asunto, excluido el ID rastreado, tras la cual se recorta. Debe ser lo más pequeño posible para evitar que se pierda la información del ID rastreado. El valor predeterminado es 200.

* **[!UICONTROL Dirección de correo electrónico de respuesta]**

  Dirección que se utiliza como dirección de correo electrónico de &quot;respuesta&quot;. El valor predeterminado es `no-reply@example.com`.

* **[!UICONTROL Responder a delimitador]**

  Si se añade un ID de rastreador al encabezado Responder a, se utiliza este delimitador. El valor predeterminado es `+` (signo más).

* **[!UICONTROL Prefijo de ID de rastreador en el asunto]**

  Si se añade un ID de rastreador a la línea de asunto, se utiliza este prefijo. El valor predeterminado es `post#`.

* **[!UICONTROL Prefijo de ID de rastreador en el cuerpo del mensaje]**

  Si se añade un ID de rastreador al cuerpo del mensaje, se utiliza este prefijo. El valor predeterminado es `Please do not remove this:`.

* **[!UICONTROL Correo electrónico como HTML]**: si se selecciona, el tipo de contenido de correo electrónico se establece como `"text/html;charset=utf-8"`. La opción predeterminada está activada.

* **[!UICONTROL Nombre de usuario predeterminado]**

  Este nombre se utiliza para los usuarios sin nombre. El valor predeterminado es `no-reply@example.com`.

* **[!UICONTROL Ruta raíz de plantillas]**

  El correo electrónico se crea mediante una plantilla almacenada en esta ruta raíz. El valor predeterminado es `/etc/community/templates/subscriptions-email`.

## Configurar el importador de encuestas {#configure-polling-importer}

Para que el correo electrónico se introduzca en el repositorio, es necesario configurar un importador de encuestas y configurar sus propiedades en el repositorio manualmente.

### Agregar nuevo importador de encuestas {#add-new-polling-importer}

* Inicie sesión en el editor principal con privilegios de administrador y vaya a la consola del importador de encuestas:

  Por ejemplo, [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* Seleccionar **[!UICONTROL Añadir]**

  ![importador de encuestas](assets/polling-importer.png)

* **[!UICONTROL Tipo]**

  *(Obligatorio)* Tire hacia abajo para seleccionar `POP3 (over SSL)`.

* **[!UICONTROL URL]**

  *(Obligatorio)* El servidor de correo saliente. Por ejemplo, `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`.

* **[!UICONTROL Importar a ruta]**&amp;ast;

  *(Obligatorio)* Configure como. `/content/usergenerated/mailFolder/postEmails`
navegando hasta la `postEmails`carpeta y seleccione **OK**.

* **[!UICONTROL Actualizar intervalo en segundos]**

  *(Opcional)* El servidor de correo configurado para el servicio de correo predeterminado puede tener requisitos relativos al valor del intervalo de actualización. Por ejemplo, Gmail puede requerir un intervalo de `300`.

* **[!UICONTROL Iniciar sesión]**

  *(Opcional)*

* **[!UICONTROL Contraseña]**

  *(Opcional)*

* Seleccionar **[!UICONTROL OK]**.

### Ajustar protocolo para nuevo importador de encuestas {#adjust-protocol-for-new-polling-importer}

Una vez guardada la nueva configuración de sondeo, es necesario modificar aún más las propiedades del importador de correo electrónico de suscripción para cambiar el protocolo de `POP3` hasta `emailreply`.

Uso de [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Inicie sesión en el editor principal con privilegios de administrador y vaya a [https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importadores/sondeo](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling).
* Seleccione la configuración recién creada y modifique las siguientes propiedades:

   * **feedType**: Reemplazar `pop3s` con **`emailreply`**
   * **origen**: Reemplace el protocolo del origen `pop3s://` con **`emailreply://`**

![protocolo de sondeo](assets/polling-protocol.png)

Los triángulos rojos indican las propiedades modificadas. Asegúrese de guardar los cambios:

* Seleccionar **[!UICONTROL Guardar todo]**.
