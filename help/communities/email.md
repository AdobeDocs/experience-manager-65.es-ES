---
title: Configuración del correo electrónico
seo-title: Configuración del correo electrónico
description: Configuración de correo electrónico para comunidades
seo-description: Configuración de correo electrónico para comunidades
uuid: e8422cc2-1594-43b0-b587-82825636cec1
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: b4d38e45-eaa0-4ace-a885-a2e84fdfd5a1
pagetitle: Configuring Email
translation-type: tm+mt
source-git-commit: 097109edcf66cc06460c9d962037e49613e3405b
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 3%

---


# Configuración del correo electrónico {#configuring-email}

Los AEM Communities utilizan el correo electrónico para:

* [Notificaciones de comunidades](notifications.md)
* [Suscripciones de comunidades](subscriptions.md)

De forma predeterminada, la función de correo electrónico no funciona, ya que requiere la especificación de un servidor SMTP y un usuario SMTP.

>[!CAUTION]
>
>El correo electrónico para las notificaciones y suscripciones solo debe configurarse en el editor [principal](deploy-communities.md#primary-publisher).


## Configuración predeterminada del servicio de correo {#default-mail-service-configuration}

El servicio de correo predeterminado es necesario tanto para las notificaciones como para las suscripciones.

* Inicie sesión en el editor principal con privilegios de administrador y acceda a la consola [web](../../help/sites-deploying/configuring-osgi.md):

   * Por ejemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Busque el `Day CQ Mail Service`.
* Seleccione el icono de edición.

Esto se basa en la documentación de [Configuración de notificaciones](../../help/sites-administering/notification.md)por correo electrónico, pero con una diferencia en que el campo `"From" address` ** no es obligatorio y debe dejarse vacío.

Por ejemplo (rellenado con valores únicamente para fines ilustrativos):

![chlimage_1-98](assets/chlimage_1-98.png)

* **[!UICONTROL Nombre de host del servidor SMTP]**

   *(Requerido)* El servidor SMTP que se va a utilizar.

* **[!UICONTROL Puerto del servidor SMTP]**

   *(Requerido)* El puerto del servidor SMTP debe ser 25 o superior.

* **[!UICONTROL Usuario SMTP]**

   *(Requerido)* El usuario SMTP.

* **[!UICONTROL Contraseña SMTP]**

   *(Requerido)* La contraseña del usuario SMTP.

* **[!UICONTROL Dirección &quot;De&quot;]**

   Dejar vacío
* **[!UICONTROL SMTP utiliza SSL]**

   Si se selecciona, se enviará un correo electrónico seguro. Asegúrese de que el puerto esté establecido en 465 o según sea necesario para el servidor SMTP.
* **[!UICONTROL Depurar correo electrónico]**

   Si se selecciona, habilita el registro de interacciones del servidor SMTP.

## Configuración de correo electrónico de AEM Communities {#aem-communities-email-configuration}

Una vez configurado el servicio [de correo](#default-mail-service-configuration) predeterminado, las dos instancias existentes de la configuración de `AEM Communities Email Reply Configuration` OSGi, incluidas en la versión, funcionan.

Solo la instancia de suscripciones debe configurarse más al permitir la respuesta por correo electrónico.

1. [Instancia de correo electrónico](#configuration-for-notifications) :

   En el caso de las notificaciones, que no admiten correo electrónico de respuesta y no deben modificarse.

1. [Suscripciones-instancia de correo electrónico](#configuration-for-subscriptions) :

   Requiere configuración para habilitar completamente la creación de publicaciones a partir del correo electrónico de respuesta.

Para llegar a las instancias de configuración de correo electrónico de Comunidades:

* Inicie sesión en el editor principal con privilegios de administrador y acceda a la consola [web](../../help/sites-deploying/configuring-osgi.md)

   * Por ejemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localizar `AEM Communities Email Reply Configuration`.

![chlimage_1-99](assets/chlimage_1-99.png)

### Configuración de notificaciones {#configuration-for-notifications}

La instancia de configuración de `AEM Communities Email Reply Configuration` OSGi con el correo electrónico Nombre es la función de notificaciones. Esta función no incluye la respuesta por correo electrónico.

Esta configuración no debe modificarse.

* Busque el `AEM Communities Email Reply Configuration`.
* Seleccione el icono de edición.
* Verifique que el **nombre** sea `email`.

* Verifique que **Crear anuncio desde correo electrónico** de respuesta sea `unchecked`.

![chlimage_1-100](assets/chlimage_1-100.png)

### Configuración de Suscripciones {#configuration-for-subscriptions}

En el caso de suscripciones de comunidades, es posible activar o desactivar la capacidad de un miembro para publicar contenido respondiendo a un mensaje de correo electrónico.

* Busque el `AEM Communities Email Reply Configuration`.
* Seleccione el icono de edición.
* Verifique que el **nombre** sea `subscriptions-email`.

![chlimage_1-101](assets/chlimage_1-101.png)

* **[!UICONTROL Nombre]**

   *(Requerido)* `subscriptions-email`. No editar.

* **[!UICONTROL Crear anuncio desde correo electrónico de respuesta]**

   Si se selecciona, el destinatario de correo electrónico de suscripción puede publicar contenido enviando una respuesta. El valor predeterminado está marcado.
* **[!UICONTROL Añadir la identificación rastreada en el encabezado]**

   El valor predeterminado es `Reply-To`.

* **[!UICONTROL Longitud máxima del asunto]**

   Si se agrega la identificación del rastreador a la línea de asunto, ésta es la longitud máxima del sujeto, excluyendo la identificación rastreada, tras la cual se recortará. Tenga en cuenta que esto debe ser lo más pequeño posible para evitar que la información de identificación rastreada se pierda. El valor predeterminado es 200.
* **[!UICONTROL Dirección de correo electrónico &quot;De&quot;]**

   *(Requerido)* Dirección desde la que se enviaría el correo electrónico de notificación. Es probable que el mismo usuario **** SMTP especificado para el servicio [de correo](#configuredefaultmailservice)predeterminado. El valor predeterminado es `no-reply@example.com`.

* **[!UICONTROL Respuesta al delimitador]**

   Si se agrega la identificación del rastreador al encabezado Responder a, se utilizará este delimitador. El valor predeterminado es `+` (signo más).

* **[!UICONTROL Prefijo de identificación del rastreador en el asunto]**

   Si se agrega la identificación del rastreador a la línea de asunto, se utilizará este prefijo. El valor predeterminado es `post#`.

* **[!UICONTROL Prefijo de identificación del rastreador en el cuerpo del mensaje]**

   Si se agrega la identificación del rastreador al cuerpo del mensaje, se utilizará este prefijo. El valor predeterminado es `Please do not remove this:`.

* **[!UICONTROL Correo electrónico como HTML]**: Si se selecciona, el tipo de contenido del correo electrónico se establecerá como `"text/html;charset=utf-8"`. El valor predeterminado está marcado.

* **[!UICONTROL Nombre de usuario predeterminado]**

   Este nombre no se usará para usuarios con nombre. El valor predeterminado es `no-reply@example.com`.

* **[!UICONTROL Ruta raíz de plantillas]**

   El correo electrónico se genera mediante la plantilla almacenada en esta ruta raíz. El valor predeterminado es `/etc/community/templates/subscriptions-email`.

## Configurar importador de encuestas {#configure-polling-importer}

Para que el correo electrónico se introduzca en el repositorio, es necesario configurar un importador de encuestas y configurar sus propiedades en el repositorio de forma manual.

### Añadir nuevo importador de encuestas {#add-new-polling-importer}

* Inicie sesión en el editor principal con privilegios de administrador y vaya a la consola del importador de encuestas:

   Por ejemplo, [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* Seleccionar **[!UICONTROL Añadir]**

   ![chlimage_1-102](assets/chlimage_1-102.png)

* **[!UICONTROL Tipo]**

   *(Requerido)* Despliegue para seleccionar `POP3 (over SSL)`.

* **[!UICONTROL URL]**

   *(Requerido)* El servidor de correo saliente. Por ejemplo, `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`.

* **[!UICONTROL Importar a ruta]**&amp;ast;

   *(Requerido)* Configure en `/content/usergenerated/mailFolder/postEmails`buscando en la `postEmails`carpeta y seleccione **Aceptar**.

* **[!UICONTROL Actualizar intervalo en segundos]**

   *(Opcional)* El servidor de correo configurado para el servicio de correo predeterminado puede tener requisitos con respecto al valor del intervalo de actualización. Por ejemplo, Gmail puede requerir un intervalo de `300`.

* **[!UICONTROL Inicio de sesión]**

   *(Opcional)*

* **[!UICONTROL Contraseña]**

   *(Opcional)*

* Seleccione **[!UICONTROL Aceptar]**.

### Ajustar protocolo para nuevo importador de encuestas {#adjust-protocol-for-new-polling-importer}

Una vez guardada la nueva configuración de sondeo, es necesario modificar las propiedades del importador de correo electrónico de suscripción para cambiar el protocolo de `POP3` a `emailreply`

Uso de [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Inicie sesión en el editor principal con privilegios de administrador y vaya a [https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importadores/encuestas](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling).
* Seleccione la configuración recién creada y modifique las siguientes propiedades:

   * **feedType**: Reemplazar `pop3s` por **`emailreply`**
   * **source**: Reemplazar el protocolo del origen `pop3s://` por **`emailreply://`**

![chlimage_1-103](assets/chlimage_1-103.png)

Los triángulos rojos indican las propiedades modificadas. Asegúrese de guardar los cambios:

* Seleccione **[!UICONTROL Guardar todo]**.

