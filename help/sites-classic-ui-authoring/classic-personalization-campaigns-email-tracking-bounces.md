---
title: Seguimiento de correos electrónicos rechazados
seo-title: Tracking Bounced Emails
description: Cuando envía una newsletter a muchos usuarios, suele haber algunas direcciones de correo electrónico no válidas en la lista. El envío de boletines a esas direcciones se recupera. AEM Puede administrar esas devoluciones y puede dejar de enviar boletines informativos a esas direcciones después de que se exceda el contador de devoluciones configurado.
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

# Seguimiento de correos electrónicos rechazados{#tracking-bounced-emails}

>[!NOTE]
>
>El Adobe AEM de no planea mejorar aún más el seguimiento de los correos electrónicos abiertos/rechazados enviados por el servicio SMTP de la.
>
>La recomendación es [Uso de Adobe Campaign AEM y su integración con el](/help/sites-administering/campaign.md).

Cuando envía una newsletter a muchos usuarios, suele haber algunas direcciones de correo electrónico no válidas en la lista. El envío de boletines a esas direcciones se recupera. AEM Puede administrar esas devoluciones y puede dejar de enviar boletines informativos a esas direcciones después de que se exceda el contador de devoluciones configurado. De forma predeterminada, la tasa de salida hacia otro sitio se establece en 3, pero se puede configurar.

AEM AEM Para configurar el seguimiento de correos electrónicos rechazados, configure la configuración de la opción para sondear un buzón de correo existente en el que se reciban los correos electrónicos rechazados. Normalmente, esta ubicación es la dirección de correo electrónico de origen que especifica dónde envía la newsletter. AEM sondea esta bandeja de entrada e importa todos los correos electrónicos por debajo de la ruta especificada en la configuración de sondeo. A continuación, se activa un flujo de trabajo para buscar las direcciones de correo electrónico rechazadas dentro de los usuarios y se actualiza el valor de la propiedad bounceCounter del usuario en consecuencia. Una vez superados los rebotes máximos configurados, el usuario se elimina de la lista del boletín informativo.

## Configuración del importador de fuentes {#configuring-the-feed-importer}

El importador de fuentes le permite importar repetidamente contenido de fuentes externas al repositorio. AEM Con esta configuración del importador de fuentes, comprueba en el buzón del remitente si hay correos electrónicos devueltos.

Para configurar el importador de fuentes para el seguimiento de correos electrónicos rechazados, haga lo siguiente:

1. Entrada **Herramientas**, seleccione el Importador de fuentes.

1. Clic **Añadir** para crear una configuración.

   ![chlimage_1](assets/chlimage_1a.png)

1. Añada una configuración seleccionando el tipo y añadiendo información a la URL de sondeo para que pueda configurar el host y el puerto. Además, agregue algunos parámetros de correo electrónico y específicos del protocolo a la consulta de URL. Establezca la configuración para sondear al menos una vez al día.

   Todas las configuraciones necesitan información sobre lo siguiente en la dirección URL de sondeo:

   `username`: El nombre de usuario que se utiliza para la conexión

   `password`: La contraseña utilizada para conectarse

   Además, según el protocolo, puede configurar ciertas opciones.

   **Propiedades de configuración POP3:**

   `pop3.leave.on.server`: define si se deben dejar los mensajes en el servidor o no. Si se establece en true, los mensajes se dejarán en el servidor; en caso contrario, en false. El valor predeterminado es True.

   **Ejemplos POP3:**

   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret | Uso de pop3 sobre SSL para conectarse a GMail en el puerto 995 con usuario/secreto, dejando los mensajes en el servidor de forma predeterminada |
   |---|---|
   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false |

   **Propiedades de configuración de IMAP:**

   Permite establecer marcas para buscar.

   `imap.flag.SEEN`:Establezca false para los mensajes nuevos o no vistos, true para los mensajes ya leídos

   Consulte [https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html](https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html) para obtener la lista completa de indicadores.

   **Ejemplos de IMAP:**

   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret | Uso de IMAP sobre SSL para conectarse a GMail en el puerto 993 con usuario/secreto. Recibir mensajes nuevos solo de forma predeterminada. |
   |---|---|
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true | Utilizando IMAP sobre SSL para conectarse a GMail 993 con usuario/secreto, solo recibiendo mensaje ya visto. |
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true&amp;imap.flag.SEEN=false | Utilizando IMAP sobre SSL para conectarse a GMail 993 con usuario/secreto, recibiendo mensajes leídos o nuevos. |

1. Guarde la configuración.

## Configuración del componente de servicio de newsletter {#configuring-the-newsletter-service-component}

Después de configurar el importador de fuentes, configure la Dirección de origen y el contador de devoluciones.

Para configurar el servicio del boletín informativo:

1. En la consola OSGi, en `<host>:<port>/system/console/configMgr`, vaya a **Newsletter de MCM**.

1. Configure el servicio y guarde los cambios cuando termine.

   ![chlimage_1-1](assets/chlimage_1-1a.png)

   Se pueden configurar las siguientes configuraciones para ajustar el comportamiento:

   | Contador de rechazos máximo (max.bounce.count) | Define el número de devoluciones hasta que se omite un usuario al enviar un boletín informativo. Si este valor se establece en 0, la comprobación de devoluciones se desactiva por completo. |
   |---|---|
   | Actividad sin caché (sent.activity.nocache) | Define la configuración de caché que se utilizará para la actividad de envío de newsletter |

   Una vez guardado, el servicio MCM del boletín informativo realiza las siguientes acciones:

   * Escribe una actividad en el flujo oculto de usuarios tras el envío correcto de un boletín informativo.
   * Escribe una actividad si se detecta una devolución y cambia el contador de devoluciones de los usuarios.
