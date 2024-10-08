---
title: Messaging Essentials
description: Obtenga información sobre los detalles de trabajar con el componente Mensajería y utilizarlo para incluir una función de mensajería en un sitio web.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: b941b5e0-f768-4393-9a9d-ded2cd7d10c4
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 2%

---

# Messaging Essentials {#messaging-essentials}

Esta página documenta los detalles de cómo trabajar con utilizando el componente Mensajería para incluir una función de mensajería en un sitio web.

## Essentials para el lado del cliente {#essentials-for-client-side}

**Escribir mensaje**

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaging/components/hbs/composemessage</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientlibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>plantillas</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/composemessage.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/clientlibs/composemessage.css</td>
  </tr>
  <tr>
   <td><strong>propiedades</strong></td>
   <td>Ver <a href="/help/communities/configure-messaging.md" target="_blank">Configurar mensajes</a></td>
  </tr>
  <tr>
   <td><strong>configuración de administración</strong></td>
   <td><a href="/help/communities/messaging.md">Configurar la mensajería</a></td>
  </tr>
 </tbody>
</table>

**Lista de mensajes**

(Para Bandeja de entrada, Enviado y Papelera)

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaging/components/hbs/messagebox</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientlibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>plantillas</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/messagebox.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/clientlibs/messagebox.css</td>
  </tr>
  <tr>
   <td><strong>propiedades</strong></td>
   <td>Ver <a href="/help/communities/configure-messaging.md" target="_blank">Configurar mensajes</a></td>
  </tr>
  <tr>
   <td><strong>configuración de administración</strong></td>
   <td><a href="/help/communities/messaging.md" target="_blank">Configurar la mensajería</a></td>
  </tr>
 </tbody>
</table>

Vea también [Personalizaciones del lado del cliente](/help/communities/client-customize.md)

## Essentials para servidor {#essentials-for-server-side}

* [Configuración de mensajería](/help/communities/configure-messaging.md)
* [API de cliente de mensajería](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/messaging/client/api/package-summary.html) para componentes SCF
* [API de mensajería](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/messaging/api/package-summary.html) para el servicio
* [Puntos finales de mensajería](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/messaging/client/endpoints/package-summary.html)
* [Personalizaciones del lado del servidor](/help/communities/server-customize.md)

>[!CAUTION]
>
>El parámetro String debe *not* contener una barra diagonal &quot;/&quot; para los siguientes métodos de MessageBuilder:
>
>* `setInboxPath`()
>* `setSentItemsPath`()
>
>Por ejemplo:
>
>```
>valid: mb.setInboxPath( "/mail/inbox" );
> not valid: mb.setInboxPath( "/mail/inbox/" );
>```

### Sitio de la comunidad {#community-site}

Una estructura de sitio de comunidad, creada con el asistente, incluye la función de mensajería cuando se selecciona. Ver la configuración de `User Management` de [Consola de sitios de la comunidad](/help/communities/sites-console.md#user-management).

### Código de ejemplo: Mensaje recibido notificación {#sample-code-message-received-notification}

La característica Mensajería social desencadena eventos para operaciones como `send`, `marking read`, `marking delete`. Estos eventos se pueden capturar y se pueden realizar acciones con los datos contenidos en el evento.

El siguiente ejemplo es de un controlador de eventos que escucha el evento `message sent` y envía un mensaje de correo electrónico a todos los destinatarios de mensajes utilizando `Day CQ Mail Service`.

Para probar el script de ejemplo del lado del servidor, necesita un entorno de desarrollo y la capacidad de crear un paquete OSGi:

1. Inicie sesión como administrador en ` [CRXDE|Lite](https://localhost:4502/crx/de)`.
1. Crear un `bundle node` en `/apps/engage/install` con nombres arbitrarios, como:

   * Nombre simbólico: `com.engage.media.social.messaging.MessagingNotification`
   * Nombre: Notificación de mensaje del tutorial de introducción
   * Descripción: Servicio de ejemplo para enviar una notificación por correo electrónico a los usuarios cuando reciben un mensaje
   * Paquete: `com.engage.media.social.messaging.notification`

1. Vaya a `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/src/main/java/com/engage/media/social/messaging/notification` y, a continuación:

   1. Eliminar la clase `Activator.java` creada automáticamente.
   1. Crear clase `MessageEventHandler.java`.
   1. Copie y pegue el código siguiente en `MessageEventHandler.java`.

1. Haga clic en **Guardar todo**.
1. Vaya a `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/com.engage.media.social.messaging.MessagingNotification.bnd` y agregue todas las instrucciones de importación tal como se escribieron en el código `MessageEventHandler.java`.
1. Genere el paquete.
1. Asegúrese de que el servicio `Day CQ Mail Service`OSGi esté configurado.
1. Inicie sesión como usuario de demostración y envíe un correo electrónico a otro usuario.
1. El destinatario recibe un correo electrónico con respecto a un nuevo mensaje.

#### MessageEventHandler.java {#messageeventhandler-java}

```java
package com.engage.media.social.messaging.notification;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.api.resource.Resource;
import org.apache.commons.mail.Email;
import org.apache.commons.mail.EmailException;
import org.apache.commons.mail.SimpleEmail;
import org.apache.commons.mail.HtmlEmail;
import java.util.List;
import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import com.adobe.cq.social.messaging.api.Message;
import com.adobe.cq.social.messaging.api.MessagingEvent;
import com.day.cq.mailer.MessageGatewayService;
import com.day.cq.mailer.MessageGateway;

@Component(immediate=true)
@Service(EventHandler.class)
@Properties({
        @Property(name = "event.topics", value = "com/adobe/cq/social/message")
})
public class MessagingEventHandler implements EventHandler {
    private Logger logger = LoggerFactory.getLogger(MessagingEventHandler.class);

    @Reference
    ResourceResolverFactory resourceResolverFactory;

    @Reference
    private MessageGatewayService messageGatewayService;

    ResourceResolver resourceResolver=null;
    MessageGateway messageGateway=null;

    public void sendMail(String from, String to,String subject, String content){
        Email email = new SimpleEmail();
        messageGateway = messageGatewayService.getGateway(SimpleEmail.class);
        try {
         email.addTo(to);
            email.addReplyTo(from);
            email.setFrom(from);
            email.setMsg(content);
            email.setSubject(subject);
         messageGateway.send(email);
        } catch(EmailException ex) {
            logger.error("MessageNotificaiton : Error sending email : "+ex.getMessage());
        }
        logger.info("**** MessageNotification **** Mail sent to " + to);
    }

    public void handleEvent(Event event) {
        //Get Message Path and originator User's ID from event
        String messagePath = (String) event.getProperty("path");
        String senderId = (String) event.getProperty("userId");
        MessagingEvent.MessagingActions action = (MessagingEvent.MessagingActions) event.getProperty("action");
        try{
            if(MessagingEvent.MessagingActions.MessageSent.equals(action)){
                resourceResolver = resourceResolverFactory.getAdministrativeResourceResolver(null);

                //Read message
                Resource resource = resourceResolver.getResource(messagePath);
                Message msg = resource.adaptTo(Message.class);

                //Get list of recipient Ids from message
                //For Getting Started Tutorial, Id is same as email. If that is not the case in your site,
                //an additional step is needed to retrieve the email for the Id
                List<String> reclist = msg.getRecipientIdList();
                for(int i=0;i<reclist.size();i++){
                    //Send Email using Mailing Service
                    sendMail("admin@cqadmin.qqq",reclist.get(i),"New message on Getting Started Tutorial", "Hi\nYou have received a new message from  " +  senderId + ". To read it, sign in to Getting Started Tutorial.\n\n-Engage Admin");
                }
            }
        } catch(Exception ex){
            logger.error("Error getting message info : " + ex.getMessage());
        } finally {
            resourceResolver.close();
        }

    }
}
```
