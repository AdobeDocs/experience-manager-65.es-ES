---
title: Marketing por correo electrónico
seo-title: E-mail Marketing
description: El marketing por correo electrónico (por ejemplo, los boletines informativos) es una parte importante de cualquier campaña de marketing, ya que los utiliza para insertar contenido en los posibles clientes. AEM AEM En el caso de los boletines informativos, puede crear boletines informativos a partir de contenido existente, así como añadir contenido nuevo específico a los boletines informativos.
seo-description: E-mail marketing (for example, newsletters) are an important part of any marketing campaign as you use them to push content to your leads. In AEM, you can create newsletters from existing AEM content as well as add new content, specific to the newsletters.
uuid: 565943bf-fe37-4d5c-98c3-7c629c4ba264
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 69ca5acb-83f9-4e1b-9639-ec305779c931
docset: aem65
exl-id: a1d8b74e-67eb-4338-9e8e-fd693b1dbd48
source-git-commit: 75c6bb87bb06c5ac9378ccebf193b5416c080bb1
workflow-type: tm+mt
source-wordcount: '1760'
ht-degree: 1%

---

# Marketing por correo electrónico{#e-mail-marketing}

>[!NOTE]
>
>El Adobe AEM de no planea mejorar aún más el seguimiento por correo electrónico de los envíos abiertos/rechazados (no entregables) por el servicio SMTP de la.
>La recomendación es [Aproveche Adobe Campaign AEM y la integración de para crear un entorno de trabajo con](/help/sites-administering/campaign.md).

El marketing por correo electrónico (por ejemplo, los boletines informativos) es una parte importante de cualquier campaña de marketing, ya que los utiliza para insertar contenido en los posibles clientes. AEM AEM En el caso de los boletines informativos, puede crear boletines informativos a partir de contenido existente, así como añadir contenido nuevo específico a los boletines informativos.

Una vez creados, puede enviar boletines informativos al grupo específico de usuarios inmediatamente o en otra hora programada (mediante un flujo de trabajo). Además, los usuarios pueden suscribirse a los boletines en el formato que elijan.

AEM Además, le permite administrar la funcionalidad de la newsletter, lo que incluye el mantenimiento de los temas, el archivado de los boletines informativos y la visualización de las estadísticas de la newsletter.

>[!NOTE]
>
>En Geometrixx, la plantilla de la newsletter abre automáticamente el editor de correo electrónico. Puede utilizar el editor de correo electrónico en otras plantillas en las que desee enviar correos electrónicos, por ejemplo, invitaciones. El editor de correo electrónico se muestra cada vez que se hereda una página de **mcm/components/newsletter/page**.

AEM En este documento se describen los conceptos básicos para crear boletines informativos en la creación de informes de correo electrónico en la. Para obtener información más detallada sobre cómo trabajar con el marketing por correo electrónico, consulte los siguientes documentos:

* [Creación de una página de aterrizaje de newsletter efectiva](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-landingpage.md)
* [Administración de suscripciones](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-subscriptions.md)
* [Publicación de un correo electrónico para proveedores de servicios de correo electrónico](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-newsletters.md)
* [Seguimiento de correos electrónicos rechazados](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-tracking-bounces.md)

>[!NOTE]
>
>Si actualiza los proveedores de correo electrónico, realiza una prueba de vuelo o envía una newsletter, estas operaciones fallan si la newsletter no se publica primero en la instancia de publicación o si la instancia de publicación no está disponible. Asegúrese de publicar la newsletter y de que la instancia de publicación esté activa y en ejecución.

## Creación de una experiencia de newsletter {#creating-a-newsletter-experience}

>[!NOTE]
>
>Las notificaciones por correo electrónico deben configurarse mediante la configuración de osgi. Consulte [Configuración de notificaciones por correo electrónico.](/help/sites-administering/notification.md)

1. Seleccione la nueva campaña en el panel izquierdo o haga doble clic en ella en el panel derecho.

1. Seleccione la vista de lista con el icono:

   ![Vista de lista](do-not-localize/mcm_icon_listview-1.png)

1. Clic **Nuevo...**

   Puede especificar la variable **Título**, **Nombre** y tipo de experiencia que se va a crear; en este caso, Newsletter.

   ![mcm_createnewsletter](assets/mcm_createnewsletter.png)

1. Haga clic en **Crear**.

1. Se abrirá inmediatamente un nuevo cuadro de diálogo. Aquí puede introducir las propiedades de la newsletter.

   El **Lista de destinatarios predeterminada** es un campo obligatorio, ya que forma el punto de contacto de la newsletter (consulte [Uso de listas](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists) para obtener más información sobre listas).

   ![mcm_newnewsletterdialog](assets/mcm_newnewsletterdialog.png)

   * **Nombre desde**
Nombre que debe aparecer como remitente de la newsletter.

   * **Dirección desde**
Dirección de correo que debe aparecer como remitente de la newsletter.

   * **Asunto**
Asunto de la newsletter.

   * **Responder a**
Dirección de correo que enviará las respuestas de la newsletter enviada.

   * **Descripción**
Descripción de la newsletter.

   * **Tiempo de activación**
El tiempo de activación para enviar la newsletter.

   * **Lista de destinatarios predeterminada**
Lista predeterminada que debe recibir la newsletter.

   Se pueden actualizar en una etapa posterior desde el **Propiedades...** diálogo.

1. Clic **OK** para guardar.

## Añadir contenido a los boletines {#adding-content-to-newsletters}

AEM Puede agregar contenido, incluido contenido dinámico, al boletín informativo como lo haría en cualquier componente de la lista de distribución de contenido de la lista de componentes de la lista de distribución de contenido En Geometrixx, la plantilla Newsletter tiene ciertos componentes disponibles para añadir y modificar contenido en los boletines.

1. En el MCM, haga clic en **Campañas** y haga doble clic en el boletín al que desee agregar contenido o editarlo. Se abre la newsletter.

1. Si los componentes no están visibles, vaya a la vista Diseño y habilite los componentes necesarios (por ejemplo, los componentes Newsletter) antes de empezar a editar.
1. Introduzca texto, imágenes u otros componentes nuevos según corresponda. En el ejemplo de Geometrixx, hay 4 componentes disponibles: texto, imagen, encabezado y 2 columnas. La newsletter puede tener más o menos componentes en función de cómo la configure.

   >[!NOTE]
   >
   >Los boletines se personalizan mediante variables. En el boletín informativo de Geometrixx, las variables están disponibles en el componente Texto. Los valores de las variables se heredan de la información del perfil de usuario.

   ![mcm_newsletter_content](assets/mcm_newsletter_content.png)

1. Para insertar variables, seleccione la variable en la lista y haga clic en **Insertar**. Las variables se rellenan desde el perfil.

## Personalización de boletines {#personalizing-newsletters}

Puede personalizar los boletines insertando variables predefinidas en el componente Texto de los boletines en Geometrixx. Los valores de las variables se heredan de la información del perfil de usuario.

También puede simular cómo se personaliza un boletín utilizando el contexto de cliente y cargando un perfil.

Para personalizar un boletín informativo y simular el aspecto que tendrá:

1. En el MCM, abra el boletín para el que desee personalizar la configuración.

1. Abra el componente Texto que desee personalizar.

1. Coloque el cursor donde desee que aparezca la variable, seleccione una variable de la lista desplegable y haga clic en **Insertar**. Haga esto para tantas variables como sea necesario y haga clic en **OK**.

   ![mcm_newsletter_variables](assets/mcm_newsletter_variables.png)

1. Para simular el aspecto que tendrá la variable cuando se envíe, presione CTRL+ALT+c para abrir el contexto de cliente y seleccione **Cargar**. Seleccione el usuario de la lista cuyo perfil desee cargar y haga clic en **OK**.

   La información del perfil que ha cargado ha rellenado las variables.

   ![mc_newsletter_testvariables](assets/mc_newsletter_testvariables.png)

## Prueba de boletines en diferentes clientes de correo electrónico {#testing-newsletters-in-different-e-mail-clients}

>[!NOTE]
>
>Antes de enviar boletines informativos, compruebe la configuración de OSGi para el Day CQ Link Externalizer en `https://localhost:4502/system/console/configMgr`.
>
>El valor predeterminado del parámetro es `localhost:4502` La operación y no se puede completar si se cambia el puerto de la instancia en ejecución.

Cambiar entre clientes de correo electrónico comunes para ver el aspecto que tendrá la newsletter para los posibles clientes. De forma predeterminada, la newsletter se abre sin seleccionar ninguno de los clientes de correo electrónico.

Actualmente, puede ver los boletines en los siguientes clientes de correo electrónico:

* Yahoo mail
* Gmail
* Hotmail
* Thunderbird
* Microsoft Outlook 2007
* Correo electrónico de Apple

Para cambiar entre clientes, haga clic en el icono correspondiente para ver la newsletter en ese cliente de correo electrónico:

1. En el MCM, abra el boletín para el que desee personalizar la configuración.

1. Haga clic en un cliente de correo electrónico en la barra superior para ver el aspecto que tendría la newsletter en ese cliente.

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Repita este paso para cualquier cliente de correo electrónico adicional que desee ver.

   ![chlimage_1-120](assets/chlimage_1-120.png)

## Personalizar configuración de newsletter {#customizing-newsletter-settings}

Aunque solo los usuarios autorizados pueden enviar una newsletter, debe personalizar lo siguiente:

* La línea de asunto, para que los usuarios quieran abrir su correo electrónico y también para asegurarse de que el boletín informativo no termine marcado como correo no deseado.
* La dirección De, por ejemplo noreply@geometrixx.com, para que los usuarios reciban correo electrónico de una dirección especificada.

Para personalizar la configuración de la newsletter:

1. En el MCM, abra el boletín para el que desee personalizar la configuración.

   ![mcm_newsletter_open](assets/mcm_newsletter_open.png)

1. En la parte superior de la newsletter, haga clic en **Configuración**.

   ![mcm_newsletter_settings](assets/mcm_newsletter_settings.png)
1. Introduzca el **Desde** dirección de correo electrónico

1. Modifique la **Asunto** del correo electrónico, si es necesario.

1. Seleccione una **Lista de destinatarios predeterminada** en la lista desplegable.

1. Haga clic en **Aceptar**.

   Al probar o enviar la newsletter, los destinatarios recibirán correos electrónicos con la dirección de correo electrónico y el asunto especificados.

## Boletines de prueba de vuelo {#flight-testing-newsletters}

Aunque las pruebas de vuelo no son obligatorias, antes de enviar una newsletter, es posible que desee probarla para asegurarse de que tenga el aspecto que desea.

Las pruebas de vuelo le permiten hacer lo siguiente:

* Consulte la newsletter en [todos los clientes previstos](#testing-newsletters-in-different-e-mail-clients).
* Compruebe que el servidor de correo está configurado correctamente.
* Determine si el correo electrónico se marca como correo no deseado. (Asegúrese de incluirse en la lista de destinatarios).

>[!NOTE]
>
>Si actualiza los proveedores de correo electrónico, realiza una prueba de vuelo o envía una newsletter, estas operaciones fallan si la newsletter no se publica primero en la instancia de publicación o si la instancia de publicación no está disponible. Asegúrese de publicar la newsletter y de que la instancia de publicación esté activa y en ejecución.

Para enviar boletines de prueba:

1. En el MCM, abra la newsletter que desea probar y enviar.

1. En la parte superior de la newsletter, haga clic en **Prueba** para probar antes de enviar.

   ![mcm_newsletter_testsettings](assets/mcm_newsletter_testsettings.png)

1. Introduzca la dirección de correo electrónico de prueba a la que desea enviar la newsletter y haga clic en **Enviar**. Si desea cambiar el perfil, se carga otro perfil en el contexto del cliente. Para ello, presione CTRL+ALT+c y seleccione Cargar y cargar un perfil.

## Envío de boletines {#sending-newsletters}

>[!NOTE]
>
>El Adobe AEM de no planea mejorar aún más el seguimiento por correo electrónico de los envíos abiertos/rechazados (no entregables) por el servicio SMTP de la.
>La recomendación es [Aproveche Adobe Campaign AEM y la integración de para crear un entorno de trabajo con](/help/sites-administering/campaign.md).

Puede enviar una newsletter desde la newsletter o desde la lista. Se describen ambos procedimientos.

>[!NOTE]
>
>Antes de enviar boletines informativos, compruebe la configuración de OSGi para el Day CQ Link Externalizer en `https://localhost:4502/system/console/configMgr`.
>
>El valor predeterminado del parámetro es `localhost:4502` La operación y no se puede completar si se cambia el puerto de la instancia en ejecución.

>[!NOTE]
>
>Si actualiza los proveedores de correo electrónico, realiza una prueba de vuelo o envía una newsletter, estas operaciones fallan si la newsletter no se publica primero en la instancia de publicación o si la instancia de publicación no está disponible. Asegúrese de publicar la newsletter y de que la instancia de publicación esté activa y en ejecución.

### Envío de boletines informativos desde una campaña {#sending-newsletters-from-a-campaign}

Para enviar una newsletter desde la campaña:

1. En el MCM, abra la newsletter que desee enviar.

   >[!NOTE]
   >
   >Antes de enviar, asegúrese de haber personalizado el asunto de la newsletter y la dirección de correo electrónico de origen mediante [personalizar su configuración](#customizing-newsletter-settings).
   >
   >
   >[Pruebas de vuelo](#flight-testing-newsletters) se recomienda usar la newsletter antes de enviar.

1. En la parte superior de la newsletter, haga clic en **Enviar**. Se abre el asistente Newsletter.

1. En la lista de destinatarios, seleccione la lista en la que desea recibir la newsletter y haga clic en **Siguiente**.

   ![mcm_newslettersend](assets/mcm_newslettersend.png)

1. Se ha confirmado la instalación. Clic **Enviar** para enviar la newsletter.

   ![mcm_newslettersendconfirm](assets/mcm_newslettersendconfirm.png)

   >[!NOTE]
   >
   >Asegúrese de que es uno de los destinatarios para poder asegurarse de que se recibió la newsletter.

### Envío de boletines informativos desde una lista {#sending-newsletters-from-a-list}

Para enviar una newsletter desde una lista:

1. En el MCM, haga clic en **Listas** en el panel izquierdo.

   >[!NOTE]
   >
   >Antes de enviar, asegúrese de haber personalizado el asunto de la newsletter y la dirección de correo electrónico de origen mediante [personalizar su configuración](#customizing-newsletter-settings). No puede probar una newsletter si la envía desde la lista; puede [prueba vuelo](#flight-testing-newsletters) Seleccione esta opción si lo envía desde el boletín informativo.

1. Seleccione la casilla de verificación situada junto a la lista de posibles clientes a los que desea enviar una newsletter.

1. En el **Herramientas** menú, seleccione **Enviar newsletter**. El **Enviar newsletter** se abre.

   ![mcm_newslettersendfromlist](assets/mcm_newslettersendfromlist.png)

1. En el **Newsletter** , seleccione la newsletter que desee enviar y haga clic en **Siguiente**.

   ![mcm_newslettersenddialog](assets/mcm_newslettersenddialog.png)

1. Se ha confirmado la instalación. Clic **Enviar** para enviar la newsletter seleccionada a la lista especificada de posibles clientes.

   ![mcm_newslettersenddialog_confirmation](assets/mcm_newslettersenddialog_confirmation.png)

   La newsletter se envía a los destinatarios seleccionados.

## Suscripción a una newsletter {#subscribing-to-a-newsletter}

En esta sección se describe cómo suscribirse a un boletín informativo.

### Suscripción a una newsletter {#subscribing-to-a-newsletter-1}

Para suscribirse a una newsletter (utilizando el sitio web del Geometrixx como ejemplo):

1. Clic **Sitios web** y vaya a la Geometrixx **Barra de herramientas** y ábrela.

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. En la Newsletter de Geometrixx **Registrarse** , introduzca su dirección de correo electrónico y haga clic en **Registrarse**. Ahora está suscrito a la newsletter.
