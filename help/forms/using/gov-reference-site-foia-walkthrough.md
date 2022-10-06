---
title: Recorrido por FOIA del sitio de referencia We.Gov
seo-title: We.Gov reference site FOIA walkthrough
description: Consulte la guía del sitio de referencia de We.Gov para comprender cómo AEM Forms ayuda a los gobiernos a recibir e impartir la información solicitada por individuos bajo la Ley de Libertad de Información.
seo-description: See the We.Gov reference site walkthrough to understand how AEM Forms helps governments receive and impart information requested by individuals under the Freedom of Information Act.
uuid: 65d4233c-8dad-4e5e-8e39-22eb4f145adc
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cef8f597-7935-4d98-aacf-9981470ab620
exl-id: 57b5ce89-6b01-4087-a485-6d9696f06378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# Recorrido por FOIA del sitio de referencia We.Gov {#we-gov-reference-site-foia-walkthrough}

## Situación de la Ley de libertad de información del sitio de referencia {#reference-site-freedom-of-information-act-scenario}

We.Gov es una organización estatal que permite a los padres adoptivos inscribirse para recibir apoyo infantil si adoptan a un niño. We.Gov también permite a los padres solicitar información de los siguientes departamentos gubernamentales bajo la ley de libertad de información:

* Organismo de Logística de Defensa
* Departamento de Defensa Oficina del Inspector General
* Departamento de Justicia - Oficina de Política de la Información
* Departamento de la Marina
* Organismo de Protección del Medio Ambiente

Para obtener más información sobre la Ley de Libertad de Información, consulte [www.foia.gov](https://www.foia.gov).

El escenario incluye las siguientes personas:

* Sarah Rose, la persona que solicita información bajo
* John Jacobs, la persona que gestiona la solicitud, la reenvía al departamento correspondiente
* Gloria Rios, la empleada del gobierno que facilita la información según la solicitud

## Sarah inicia la solicitud de información bajo FOIA {#sarah-initiates-request-for-information-under-foia}

Según la Ley de Libertad de Información, Sarah solicita copia de los registros de casos de la Administración para Niños y Familias durante años (año fiscal) 2013-2016. Sarah presenta esta solicitud al Departamento de Justicia - Oficina de Política de Información y también significa que está dispuesta a pagar hasta 100 dólares por los costos de impresión y franqueo.

### Funcionamiento {#how-it-works}

### Véalo usted mismo {#see-it-yourself}

En el explorador, abra `https://<hostname>:<PublishPort>/wegov`. En el sitio de We.Gov, pulse Aplicaciones > Todas las aplicaciones. En la página Todas las aplicaciones, pulse Aplicar en Solicitud para solicitud FOIA.

## Sarah comienza su solicitud de información bajo FOIA {#sarah-starts-her-application-for-information-under-foia}

Sarah hace clic **Aplicar** y en la página del formulario de solicitud de la Ley de Libertad de Información, Sarah introduce información que incluye lo siguiente:

* **Agencia:** Sarah especifica la agencia a la que se dirigió la solicitud como Departamento de Justicia - Oficina de Política de Información.

* **Pagará Hasta**: Sarah especifica que está dispuesta a pagar hasta USD 100 por gastos de impresión y franqueo.
* **Describir la solicitud en detalle**: Sarah especifica &quot;Solicitando copia de los registros de casos de la Administración para Niños y Familias para los años fiscales 2013 a 2016&quot;.

![Solicitud de una copia de los registros de casos de la Administración para la Infancia y la Familia correspondientes a los ejercicios económicos 2013 a 2016](assets/sarahfiosform.png)

Solicitud de una copia de los registros de casos de la Administración para la Infancia y la Familia correspondientes a los ejercicios económicos 2013 a 2016

En cualquier momento, Sarah puede pulsar Guardar para Guardar el borrador del formulario y volver más tarde para rellenar el formulario y enviarlo. Sarah presenta el formulario.

>[!NOTE]
>
>El flujo de trabajo de reanudación por correo electrónico solo funciona con usuarios que iniciaron sesión. En el escenario del sitio de referencia, asegúrese de que se añade la usuaria Sarah Rose. Las credenciales de inicio de sesión de Sarah son `srose/password`.

## John Jacobs recibe y aprueba la solicitud {#john-jacobs-receives-and-approves-the-application}

John Jacobs recibe las peticiones y las redirige a la persona correcta. AEM Bandeja de entrada le permite ver todas las solicitudes enviadas en un solo lugar.

### Funcionamiento {#how-it-works-1}

Cuando Sarah rellena y envía la solicitud FOIA, se envía un registro de la solicitud a la bandeja de entrada de John Jacobs. John Jacobs puede consultar la solicitud presentada y aceptarla o rechazarla.

### Véalo usted mismo {#see-it-yourself-1}

Puede acceder a la bandeja de entrada de AEM en https://&lt;***hostname***>:&lt;***Puerto de publicación***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Inicie sesión en la bandeja de entrada AEM, utilizando jjacobs/contraseña como nombre de usuario/contraseña para John Jacobs, y vea la aplicación FOIA. Para obtener información sobre el uso de AEM Bandeja de entrada para tareas de flujo de trabajo centradas en formularios, consulte [Administrar aplicaciones y tareas de Forms en AEM bandeja de entrada](/help/forms/using/manage-applications-inbox.md).

![johnjacobs](assets/johnjacobs.png)

John Jacobs puede ver, aprobar o rechazar la solicitud desde el panel de aplicaciones. John Jacobs selecciona y abre los detalles de la solicitud y, después de revisarla, la aprueba.

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah recibe un correo electrónico de reconocimiento</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

Después de que John Jacobs apruebe la solicitud, Sarah recibe un correo electrónico de reconocimiento del sitio de We.Gov. Sarah es informada sobre las tarifas y el tiempo necesario para procesar su solicitud. El correo electrónico también incluye detalles de correo electrónico y teléfono que sarah puede contactar para recibir actualizaciones en su aplicación.

![sarahroseemail](assets/sarahroseemail.png)

## Gloria recibe la solicitud de FOIA para la aprobación de segundo nivel {#gloria-receives-the-foia-request-for-second-level-approval}

Después de que John Jacobs rellene la información requerida y apruebe la solicitud de Sarah, las solicitudes van a Gloria Rios para la aprobación final. Gloria revisa el documento de registro adjunto y aprueba la solicitud.

![gloriosinbox](assets/gloriariosinbox.png)

### Funcionamiento {#how-it-works-2}

Cuando John Jacobs aprueba la solicitud FOIA, se crea un PDF o documento de registro de la aplicación y se envía a la bandeja de entrada de Gloria Rios. Gloria puede ver la solicitud enviada y aprobarla o rechazarla.

### Véalo usted mismo {#see-for-yourself}

Puede acceder a la bandeja de entrada de AEM en https://&lt;***hostname***>:&lt;***Puerto de publicación***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Inicie sesión en la bandeja de entrada AEM utilizando grios/password como nombre de usuario/contraseña para Gloria Rios, y vea la solicitud FOIS.

Gloria abre la solicitud y examina los detalles de la solicitud FOIA. Después de revisar los detalles de la solicitud y comprobar la viabilidad de proporcionar los documentos requeridos, Gloria aprueba la solicitud.

![gloriariosaprobaciones](assets/gloriariosapproves.png)

## Sarah recibe la notificación de que su solicitud está aprobada {#sarah-receives-notification-that-her-request-is-approved}

Después de que Gloria apruebe la solicitud de FOIA, Sarah recibe un correo electrónico que le notifica que su solicitud está aprobada. El correo electrónico también incluye información sobre el calendario provisional para proporcionar el documento y los detalles de contacto para el seguimiento de la solicitud.

![sarahroseemailapproval](assets/sarahroseemailapproval.png)
