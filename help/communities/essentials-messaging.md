---
title: Esenciales de mensajería
seo-title: Esenciales de mensajería
description: Descripción general del componente Mensajería
seo-description: Descripción general del componente Mensajería
uuid: e0dad45e-d84d-4b28-b357-aded1c5d2605
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 98f70093-e786-4555-8aaa-d0df4c977dc0
docset: aem65
translation-type: tm+mt
source-git-commit: a3ccb1ffe2b2e24c453afac8cf3efc098f393030

---


# Esenciales de mensajería{#messaging-essentials}

Esta página documenta los detalles del trabajo con el componente Mensajería para incluir una función de mensajería en un sitio web.

## Esenciales para el cliente {#essentials-for-client-side}

**Componer mensaje**

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/mensajería/componentes/hbs/composemess</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientllibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/composemessage.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/clientlibs/composemessage.css</td>
  </tr>
  <tr>
   <td><strong>propiedades</strong></td>
   <td>consulte <a href="/help/communities/configure-messaging.md" target="_blank">Configurar mensajería</a></td>
  </tr>
  <tr>
   <td><strong>configuración de administración</strong></td>
   <td><a href="/help/communities/messaging.md">Configurar mensajería</a></td>
  </tr>
 </tbody>
</table>

**Lista de mensajes**

(para Bandeja de entrada, Enviado y Papelera)

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaging/components/hbs/messagebox</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientllibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/messagebox.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/clientlibs/messagebox.css</td>
  </tr>
  <tr>
   <td><strong>propiedades</strong></td>
   <td>consulte <a href="/help/communities/configure-messaging.md" target="_blank">Configurar mensajería</a></td>
  </tr>
  <tr>
   <td><strong>configuración de administración</strong></td>
   <td><a href="/help/communities/messaging.md" target="_blank">Configurar mensajería</a></td>
  </tr>
 </tbody>
</table>

Consulte también Personalizaciones del lado del [cliente](/help/communities/client-customize.md)

## Esenciales para servidor {#essentials-for-server-side}

* [Configuración de mensajes](/help/communities/configure-messaging.md)
* [APIs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/api/package-summary.html) de cliente de mensajería para componentes SCF
* [API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/api/package-summary.html) de mensajería para el servicio
* [Extremos de mensajería](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/endpoints/package-summary.html)
* [Personalizaciones del lado del servidor](/help/communities/server-customize.md)

>[!CAUTION]
>
>El parámetro String *no debe *contener una barra diagonal final &quot;/&quot; para los siguientes métodos de MessageBuilder:
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
>

### Sitio de la comunidad {#community-site}

Una estructura de sitio de comunidad, creada con el asistente, incluye la función de mensajería cuando se selecciona. Consulte `User Management` Configuración de la consola [Sitios de](/help/communities/sites-console.md#user-management)comunidad.

### Código de muestra: Notificación de mensaje recibido {#sample-code-message-received-notification}

La función Mensajería social genera eventos para operaciones, por ejemplo `send`, `marking read``marking delete`. Estos eventos se pueden capturar y realizar acciones en los datos contenidos en el evento.

El ejemplo siguiente es el de un controlador de eventos que escucha el `message sent` evento y envía un correo electrónico a todos los destinatarios del mensaje mediante el `Day CQ Mail Service`.

Para probar la secuencia de comandos de ejemplo del lado del servidor, necesita un entorno de desarrollo y la capacidad de crear un paquete OSGi:

1. Inicie sesión como administrador para ` [CRXDE|Lite](https://localhost:4502/crx/de).`
1. Cree una `bundle node`entrada `/apps/engage/install` con nombres arbitrarios, como:

   * Nombre simbólico: com.engagement.media.social.messaging.MessagingNotification
   * Nombre: Notificación de mensajes de tutoriales de introducción
   * Descripción: un servicio de muestra para enviar una notificación por correo electrónico a los usuarios cuando reciben un mensaje
   * Paquete: com.engagement.media.social.messaging.notification

1. Vaya a /apps/engage/install/com.engage.media.social.messaging.MessagingNotification/src/main/java/com/engagement/media/social/messaging/notification y, a continuación:

   1. Elimine la clase Activator.java creada automáticamente.
   1. Cree la clase MessageEventHandler.java.
   1. Copie y pegue el código siguiente en MessageEventHandler.java.

1. Haga clic en **Guardar todo.**
1. Vaya a /apps/engage/install/com.engage.media.social.messaging.MessagingNotification/com.engage.media.social.messaging.MessagingNotification.bnd y agregue todas las sentencias de importación tal como están escritas en el código MessageEventHandler.java.
1. Cree el paquete.
1. Asegúrese de que el servicio `Day CQ Mail Service`OSGi está configurado.
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

