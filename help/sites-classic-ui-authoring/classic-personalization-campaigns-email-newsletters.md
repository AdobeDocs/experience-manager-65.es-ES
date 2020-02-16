---
title: Publicar un mensaje de correo electrónico para los proveedores de servicios de correo electrónico
seo-title: Publicar un mensaje de correo electrónico para los proveedores de servicios de correo electrónico
description: Puede publicar boletines en servicios de correo electrónico, como ExactTarget y Silverpop Engage.
seo-description: Puede publicar boletines en servicios de correo electrónico, como ExactTarget y Silverpop Engage.
uuid: 1a7adcfe-8e52-49f4-9a00-99ac99881225
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: b9618913-5433-4baf-9ff6-490a26860505
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# Publicar un mensaje de correo electrónico para los proveedores de servicios de correo electrónico{#publishing-an-email-to-email-service-providers}

Puede publicar boletines en servicios de correo electrónico, como ExactTarget y Silverpop Engage. En este documento se describe la forma de configurar AEM para publicar un boletín en esos servicios de correo electrónico.

>[!NOTE]
>
>Debe configurar el proveedor de servicios antes de crear y publicar un mensaje de correo electrónico. See [Configuring ExactTarget](/help/sites-administering/exacttarget.md) and [Configuring Silverpop Engage](/help/sites-administering/silverpop.md) for more information.

Para publicar el correo electrónico en el proveedor de servicios de correo electrónico, debe realizar los pasos siguientes:

1. Cree un mensaje de correo electrónico.
1. Aplique la configuración del servicio de correo electrónico a la dirección de correo electrónico.
1. Publicar el correo electrónico.

>[!NOTE]
>
>Si actualiza los proveedores de correo electrónico, haga una prueba piloto o envíe un boletín; estas operaciones fallarán si el boletín no está publicado en la instancia Publicar o si esta instancia no está disponible. Asegúrese de publicar el boletín y de que la instancia Publicar funciona correctamente.

## Crear un correo electrónico {#creating-an-email}

An email or newsletter that you want to publish to an e-mail service can be created under a campaign using the **Geometrixx Newsletter** template. También puede usar la plantilla **Correo electrónico de Geometrixx Outdoors**. Sample email/newsletter-based on the **Geometrixx Outdoors E-Mail** template are available at `https://<hostname>:<port>/cf#/content/campaigns/geometrixx-outdoors/e-mails.html`.

Para crear un nuevo correo electrónico que se publique en el servicio de correo electrónico configurado:

1. Go to **Websites** and then **Campaigns**. Seleccione una campaña.
1. Haga clic en **Nuevo** para abrir la ventana **Crear página**.
1. Especifique el título y nombre y seleccione la plantilla **Boletín de Geometrixx** de la lista de plantillas disponibles.
1. Haga clic en **Crear**.
1. Abra el correo electrónico que ha creado.
1. Cambie al modo de diseño para seleccionar los componentes que desee mostrar en la barra de tareas.
1. Cambie al modo de edición y empiece a añadir contenido (texto, imágenes, [herramientas de correo electrónico](#adding-exacttarget-email-tools-to-your-email), [variables de personalización](#adding-text-and-personalization-tool-to-your-e-mail), etc.) al boletín.

### Añadir herramientas de correo electrónico de ExactTarget al correo electrónico {#adding-exacttarget-email-tools-to-your-email}

>[!NOTE]
>
>Esta sección es específica del servicio de ExactTarget.

El componente **Herramientas de correo electrónico** de ExactTarget puede añadir más funcionalidades de correo electrónico al mensaje o al boletín.

1. Abra el correo electrónico que quiera publicar en ExactTarget.
1. Añada el componente **ET: herramientas de correo electrónico** a la página mediante la barra de tareas. Abra el componente en el modo de edición.

   ![chlimage_1](assets/chlimage_1.gif)

1. Seleccione una opción del menú **Opciones**:

<table>
 <tbody>
  <tr>
   <td>Dirección física de envío (obligatoria)</td>
   <td>Este componente inserta la dirección de correo física de su organización en el correo electrónico.</td>
  </tr>
  <tr>
   <td>Centro de perfiles (obligatorio)</td>
   <td>El centro de perfiles es una página web en la que los suscriptores pueden introducir y mantener la información personal que usted retiene sobre ellos.</td>
  </tr>
  <tr>
   <td>Ver correo electrónico como página Web</td>
   <td>Este componente permite al usuario ver el correo electrónico como una página web.</td>
  </tr>
  <tr>
   <td>Política de privacidad</td>
   <td>This component inserts the link to your privacy policy in the email.<br /> </td>
  </tr>
  <tr>
   <td>Centro de cancelación de suscripciones</td>
   <td>Permite al usuario cancelar la suscripción a su lista de correo.</td>
  </tr>
  <tr>
   <td>Centro de suscripciones</td>
   <td>Un centro de suscripción es una página web en la que un suscriptor puede controlar los mensajes que recibe de su organización.</td>
  </tr>
  <tr>
   <td>Seguimiento de aperturas de correo electrónico</td>
   <td>A hidden component that allows you to use ExactTarget tracking feature.<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>El menú desplegable **Opciones** solo se rellenará si se aplica la configuración ExactTarget al correo electrónico. See [Applying Email Service Configuration to Email Settings](#applying-e-mail-service-configuration-to-e-mail-settings) for more information.

1. Publicar el correo electrónico en ExactTarget.

   El mensaje que tiene las herramientas de correo electrónico estará disponible en la cuenta configurada de ExactTarget.

>[!NOTE]
>
>* The URLs within the email tools are replaced (in the received email) by their actual values only when an email is sent using **Simple Send** or **Guided Send** but not **Test Send**.
   >
   >
* Se requieren dos de las herramientas de correo electrónico: **Dirección física de envío (obligatoria)** y **Centro de perfiles (obligatorio)**. Cuando se publica el correo electrónico en ExactTarget, se añaden estas dos herramientas de correo electrónico de forma predeterminada en la parte inferior de cada mensaje.
>



### Añadir la herramienta de texto y personalización al correo electrónico {#adding-text-and-personalization-tool-to-your-e-mail}

Puede añadir campos personalizados en un correo electrónico; para ello, añada el componente **Texto y personalización** a la página:

1. Abra el correo electrónico que se publicará en el servicio de correo electrónico.
1. Para activar el campo personalización del servicio de correo electrónico, añada la configuración del marco mientras configura el servicio de correo electrónico. See [configuring Silverpop Engage](/help/sites-administering/silverpop.md) and [configuring Exact Target](/help/sites-administering/exacttarget.md) for more information.
1. Add the component **Text &amp; Personalization** from the sidekick. Este componente forma parte del grupo del boletín. Abra este componente en el modo de edición.

   ![chlimage_1-110](assets/chlimage_1-110a.png)

1. Añada el campo personalizado requerido al texto; para ello, seleccione el campo en el menú desplegable y haga clic en **Insertar**.
1. Haga clic en **Aceptar** para finalizar.

## Aplicar la configuración del servicio de correo electrónico a los mensajes de correo electrónico {#applying-e-mail-service-configuration-to-e-mail-settings}

Para aplicar la configuración del servicio de correo electrónico a un boletín:

1. Cree una configuración de servicio de correo electrónico.
1. Abra el correo electrónico o el boletín.
1. Open the email/newsletter settings by either clicking **Settings** or by clicking **Page Properties in** the sidekick.
1. Haga clic en **Añadir servicio** en la ficha **Servicios de nube**. Verá la lista de servicios. Seleccione la configuración necesaria (**ExactTarget** o **Silverpop**) de la lista que encontrará en la lista desplegable.

   ![climage_1-5](assets/chlimage_1-5a.jpeg)

1. Haga clic en **Aceptar**.

## Publicar mensajes de correo electrónico en el servicio de correo electrónico {#publishing-emails-to-email-service}

Los mensajes de correo electrónico y los boletines se pueden publicar en el servicio de correo electrónico, si sigue estos pasos:

1. Abra el correo electrónico.
1. Antes de publicar un correo electrónico, compruebe que haya aplicado la configuración correcta al correo.
1. Haga clic en **Publicar**. Esta opción abrirá la ventana **Publicar boletín en el proveedor de servicios de correo electrónico.**
1. Rellene el campo **Nombre del boletín**. El correo electrónico o el boletín se publicó en el proveedor de servicios de correo electrónico con este nombre. Si no se especifica ningún nombre, el correo electrónico se publicará con el nombre de la página del boletín en AEM.
1. Haga clic en **Publicar**.

   ![climage_1-6](assets/chlimage_1-6.jpeg)

   Si la operación es correcta, AEM confirmará que se puede ver el correo electrónico en ExactTarget o Silverpop Engage.

   In the case of ExactTarget the published email can ve viewed by clicking **View Published Email**. This takes you directly to the published newsletter in the ExactTarget ([https://members.exacttarget.com/](https://members.exacttarget.com/).).

>[!NOTE]
>
>Si un boletín se publica con el mismo nombre que un correo electrónico o boletín publicado recientemente, no se reemplazará el correo o boletín anterior. En cambio, se creará un nuevo correo electrónico o boletín con el mismo nombre (aunque los ID de los dos boletines serán diferentes).
>
>Al publicar mensajes de correo electrónico y boletines en el proveedor de servicios de correo electrónico, también se publican en la instancia de publicación de AEM.


### Actualizar un correo electrónico publicado {#updating-a-published-e-mail}

The **Update** button on the Publish dialog box lets you update a newsletter already published to an E-mail Service Provider. Si todavía no se ha publicado el boletín y hace clic en el botón **Actualizar**, se mostrará el mensaje **No se publicó el boletín**.

Para actualizar un correo electrónico publicado:

1. Abra el correo electrónico o el boletín que ya se haya publicado en un proveedor de servicios de correo electrónico, y que quiera volver a publicar después de realizar cambios en él.
1. Haga clic en **Publicar**. The **Publish Newsletter to Email Service Provider** window displays. Click **Update**.

   To check if the email/newsletter has been updated on ExactTarget, click **View Published Email**. Esto le llevará al correo electrónico publicado en ExactTarget.

   Para comprobar si el correo electrónico o el boletín se ha actualizado en el servicio de correo electrónico de Silverpop, consulte el sitio Silverpop Engage.

