---
title: Recorrido por FOIA del sitio de referencia We.Gov
seo-title: Recorrido por FOIA del sitio de referencia We.Gov
description: Vea el tutorial en el sitio de referencia We.Gov para entender cómo AEM Forms ayuda a los gobiernos a recibir e impartir la información solicitada por individuos bajo la Ley de Libertad de Información.
seo-description: Vea el tutorial en el sitio de referencia We.Gov para entender cómo AEM Forms ayuda a los gobiernos a recibir e impartir la información solicitada por individuos bajo la Ley de Libertad de Información.
uuid: 65d4233c-8dad-4e5e-8e39-22eb4f145adc
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cef8f597-7935-4d98-aacf-9981470ab620
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---


# Recorrido FOIA del sitio de referencia We.Gov {#we-gov-reference-site-foia-walkthrough}

## Situación de la Ley de libertad de información del sitio de referencia {#reference-site-freedom-of-information-act-scenario}

We.Gov es una organización estatal que permite a los padres adoptivos inscribirse para recibir apoyo infantil si adoptan a un niño. We.Gov también permite a los padres solicitar información de los siguientes departamentos gubernamentales bajo la ley de libertad de información:

* Organismo de Logística de Defensa
* Departamento de Defensa Oficina del Inspector General
* Departamento de Justicia - Oficina de Política de la Información
* Departamento de la Marina
* Organismo de Protección del Medio Ambiente

Para obtener más información sobre la Ley de libertad de información, véase [www.foia.gov](https://www.foia.gov).

El escenario incluye las siguientes personas:

* Sarah Rose, la persona que solicita información en
* John Jacobs, la persona que maneja la solicitud, la envía al departamento correspondiente
* Gloria Rios, la empleada del gobierno que facilita la información según la solicitud

## Sarah inicia la solicitud de información en FOIA {#sarah-initiates-request-for-information-under-foia}

Según la Ley de Libertad de Información, Sarah solicita copia de los registros de casos de la Administración para Niños y Familias durante años (año fiscal) 2013 a 2016. Sarah presenta esta solicitud al Departamento de Justicia - Oficina de Política de Información y también significa que está dispuesta a pagar hasta 100 dólares de los EE.UU. por los gastos de impresión y franqueo.

### Cómo funciona {#how-it-works}

### Véalo usted mismo {#see-it-yourself}

En el explorador, abra `https://<hostname>:<PublishPort>/wegov`. En el sitio Web We.Gov, toque Aplicaciones > Todas las aplicaciones. En la página Todas las aplicaciones, toque Aplicar en Aplicación para Solicitud FOIA.

## Sarah inicio su solicitud de información en FOIA {#sarah-starts-her-application-for-information-under-foia}

Sarah hace clic en **Aplicar** y en la página de Solicitud de Ley de Libertad de Información, Sarah ingresa información que incluye lo siguiente:

* **Agencia:** Sarah especifica la agencia a la que se dirigió la solicitud como Departamento de Justicia - Oficina de Política de Información.

* **Pagará Hasta**: Sarah especifica que está dispuesta a pagar hasta 100 USD por gastos de impresión y envío.
* **Describa la solicitud en detalle**: Sarah especifica &quot;Solicitud de copia de los registros de casos de la Administración para Niños y Familias para los años fiscales 2013 a 2016&quot;.

![Solicitud de copia de los registros de casos de la Administración para la Infancia y la Familia correspondientes a los ejercicios económicos 2013 a 2016](assets/sarahfiosform.png)

Solicitud de copia de los registros de casos de la Administración para la Infancia y la Familia correspondientes a los ejercicios económicos 2013 a 2016

En cualquier momento, Sarah puede tocar save (guardar) para guardar el borrador del formulario y volver más tarde para rellenar el formulario y enviarlo. Sarah presenta el formulario.

>[!NOTE]
>
>El flujo de trabajo de reanudación del correo electrónico funciona únicamente con los usuarios que han iniciado sesión. En el escenario del sitio de referencia, asegúrese de añadir al usuario Sarah Rose. Las credenciales de inicio de sesión de Sarah son `srose/password`.

## John Jacobs recibe y aprueba la solicitud {#john-jacobs-receives-and-approves-the-application}

John Jacobs recibe las solicitudes y las envía a la persona adecuada. AEM Bandeja de entrada le permite ver todas las aplicaciones enviadas en un solo lugar.

### Cómo funciona {#how-it-works-1}

Cuando Sarah rellena y envía la solicitud FOIA, se envía un registro de la solicitud a la bandeja de entrada de John Jacobs. John Jacobs puede vista de la solicitud presentada y aceptarla o rechazarla.

### Véalo usted mismo {#see-it-yourself-1}

Puede acceder a la bandeja de entrada AEM en https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Inicie sesión en la bandeja de entrada AEM, utilizando jjacobs/password como nombre de usuario/contraseña para John Jacobs, y consulte la aplicación FOIA. Para obtener información sobre el uso de AEM Bandeja de entrada para tareas de flujo de trabajo centradas en formularios, consulte [Administración de aplicaciones y tareas de Forms en AEM Bandeja de entrada](/help/forms/using/manage-applications-inbox.md).

![johnjacobs](assets/johnjacobs.png)

John Jacobs puede ver, aprobar o rechazar la solicitud desde el panel de la aplicación. John Jacobs selecciona y abre los detalles de la solicitud y luego de revisarla, la aprueba.

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah recibe un correo electrónico de confirmación</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

Después de que John Jacobs apruebe la solicitud, Sarah recibe un correo electrónico de acuse de recibo del sitio Web We.Gov. Sarah está informada sobre las tarifas y el tiempo necesario para procesar su solicitud. El correo electrónico también incluye detalles de correo electrónico y teléfono con los que sarah puede ponerse en contacto para recibir actualizaciones en su aplicación.

![sarahroseemail](assets/sarahroseemail.png)

## Gloria recibe la solicitud FOIA de aprobación de segundo nivel {#gloria-receives-the-foia-request-for-second-level-approval}

Después de que John Jacobs rellene la información requerida y apruebe la solicitud de Sarah, las solicitudes van a Gloria Rios para la aprobación final. Gloria revisa el documento adjunto del registro y aprueba la solicitud.

![gloriariosinbox](assets/gloriariosinbox.png)

### Cómo funciona {#how-it-works-2}

Cuando John Jacobs aprueba la solicitud FOIA, se crea un PDF o Documento de registro de la aplicación y se envía a la bandeja de entrada de Gloria Rios. Gloria puede vista de la solicitud enviada y aprobarla o rechazarla.

### Consulte usted mismo {#see-for-yourself}

Puede acceder a la bandeja de entrada AEM en https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Inicie sesión en la bandeja de entrada AEM con grios/password como nombre de usuario/contraseña para Gloria Rios, y consulte la solicitud FOIS.

Gloria abre la solicitud y examina los detalles de la solicitud FOIA. Después de revisar los detalles de la solicitud y comprobar la viabilidad de proporcionar los documentos requeridos, Gloria aprueba la solicitud.

![gloriariosaprueba](assets/gloriariosapproves.png)

## Sarah recibe la notificación de que su solicitud ha sido aprobada {#sarah-receives-notification-that-her-request-is-approved}

Después de que Gloria apruebe la solicitud de FOIA, Sarah recibe un correo electrónico que le notifica que su solicitud ha sido aprobada. El correo electrónico también incluye la información sobre la cronología provisional para proporcionar el documento y los detalles de contacto para el seguimiento de la solicitud.

![sarahroseemail, aprobación](assets/sarahroseemailapproval.png)

