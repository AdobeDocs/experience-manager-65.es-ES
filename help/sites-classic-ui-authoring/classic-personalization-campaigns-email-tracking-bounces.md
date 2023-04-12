---
title: Seguimiento de correos electrónicos devueltos
seo-title: Tracking Bounced Emails
description: Cuando envía una newsletter a muchos usuarios, normalmente hay algunas direcciones de correo electrónico no válidas en la lista. Si se envían newsletters a esas direcciones, se devuelven. AEM administrar esas devoluciones y dejar de enviar newsletters a esas direcciones una vez se haya superado el contador de devoluciones configurado.
seo-description: When you send a newsletter to many users, there are usually some invalid emails addresses in the list. Sending newsletters to those addresses bounce back. AEM is capable of managing those bounces and can stop sending newsletters to those addresses after the configured bounce counter is exceeded.
uuid: 749959f2-e6f8-465f-9675-132464c65f11
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: fde9027b-9057-48c3-ae34-3f3258c5b371
exl-id: 6cda0a68-0df9-44e7-ae4f-9951411af6dd
source-git-commit: e05f6cd7cf17f4420176cf76f28cb469bcee4a0a
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---

# Seguimiento de correos electrónicos devueltos{#tracking-bounced-emails}

>[!NOTE]
>
>Adobe no tiene previsto mejorar aún más el seguimiento de los correos electrónicos abiertos o devueltos enviados por AEM servicio SMTP.
>
>La recomendación es [usar Adobe Campaign y su integración AEM](/help/sites-administering/campaign.md).

Cuando envía una newsletter a muchos usuarios, normalmente hay algunas direcciones de correo electrónico no válidas en la lista. Si se envían newsletters a esas direcciones, se devuelven. AEM administrar esas devoluciones y dejar de enviar newsletters a esas direcciones una vez se haya superado el contador de devoluciones configurado. De forma predeterminada, la tasa de salida hacia otro sitio está definida en 3 pero es configurable.

Para configurar AEM para realizar un seguimiento de los correos electrónicos devueltos, configure AEM para sondear un buzón de correo existente en el que se reciben los correos devueltos. Normalmente, esta ubicación es la dirección de correo electrónico &quot;de&quot; que especifica al enviar la newsletter. AEM sondea esta bandeja de entrada e importa todos los correos electrónicos por debajo de la ruta especificada en la configuración de sondeo. A continuación, se activa un flujo de trabajo para buscar las direcciones de correo electrónico devueltas dentro de los usuarios y actualiza el valor de la propiedad bounceCounter del usuario en consecuencia. Una vez superados los rechazos máximos configurados, el usuario se elimina de la lista del boletín informativo.

## Configuración del importador de fuentes {#configuring-the-feed-importer}

El importador de fuentes le permite importar repetidamente contenido de fuentes externas en su repositorio. Con esta configuración del importador de fuentes, AEM comprueba si hay correos electrónicos devueltos en el buzón del remitente.

Para configurar Feed Importer para que realice el seguimiento de los correos electrónicos devueltos, haga lo siguiente:

1. En **Herramientas**, seleccione Feed Importer.

1. Haga clic en **Agregar** para crear una configuración.

   ![imagen_1](assets/chlimage_1a.png)

1. Para agregar una configuración, seleccione el tipo y añada información a la URL de sondeo para que pueda configurar el host y el puerto. Además, agregue algunos parámetros de correo y protocolo específicos a la consulta de URL. Establezca la configuración para sondear al menos una vez al día.

   Todas las configuraciones necesitan información sobre lo siguiente en la URL de sondeo:

   `username`: El nombre de usuario que se utiliza para la conexión

   `password`: La contraseña que se utiliza para la conexión

   Además, según el protocolo, puede configurar ciertos ajustes.

   **Propiedades de configuración POP3:**

   `pop3.leave.on.server`: Define si los mensajes se dejarán en el servidor o no. Configúrelo en true para dejar mensajes en el servidor; en caso contrario, en false . El valor predeterminado es true.

   **Ejemplos de POP3:**

   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret | Usar pop3 sobre SSL para conectarse a GMail en el puerto 995 con user/secret, dejando mensajes en el servidor de forma predeterminada |
   |---|---|
   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false |

   **Propiedades de configuración de IMAP:**

   Permite establecer indicadores para buscar.

   `imap.flag.SEEN`: establezca false para los mensajes nuevos o no vistos, true para los mensajes ya leídos

   Consulte [https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html](https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html) para la lista completa de indicadores.

   **Ejemplos de IMAP:**

   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret | Usar IMAP sobre SSL para conectarse a GMail en el puerto 993 con user/secret. Solo se obtienen nuevos mensajes de forma predeterminada. |
   |---|---|
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true | Usar IMAP sobre SSL para conectarse a GMail 993 con usuario/secreto, solo obteniendo un mensaje ya visto. |
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true&amp;imap.flag.SEEN=false | Usar IMAP sobre SSL para conectarse a GMail 993 con usuario/secreto, obteniendo mensajes nuevos o ya leídos. |

1. Guarde la configuración.

## Configuración del componente de servicio de boletín informativo {#configuring-the-newsletter-service-component}

Después de configurar Feed Importer, configure la dirección De y el contador de devoluciones.

Para configurar el servicio de boletín informativo:

1. En la consola OSGi, en `<host>:<port>/system/console/configMgr`, vaya a **Newsletter de MCM**.

1. Configure el servicio y guarde los cambios cuando termine.

   ![Chlimage_1-1](assets/chlimage_1-1a.png)

   Se pueden configurar las siguientes configuraciones para ajustar el comportamiento:

   | Contador de devoluciones máximo (max.bounce.count) | Define el número de devoluciones hasta que se omite a un usuario al enviar una newsletter. Si este valor se establece en 0, se desactiva completamente la comprobación de devoluciones. |
   |---|---|
   | Actividad sin caché (sent.activity.nocache) | Define la configuración de caché que se utilizará para la actividad de newsletter enviada |

   Una vez guardado, el servicio MCM newsletter hace lo siguiente:

   * Escribe una actividad en el flujo oculto de los usuarios tras enviar correctamente una newsletter.
   * Escribe una actividad si se detecta una devolución y cambia el contador de devoluciones de los usuarios.
