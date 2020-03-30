---
title: Recorrido por el sitio de referencia We.Gov
seo-title: Recorrido por el sitio de referencia We.Gov
description: Use usuarios y grupos ficticios para realizar tareas de formularios AEM mediante el paquete de demostración We.Gov.
seo-description: Use usuarios y grupos ficticios para realizar tareas de formularios AEM mediante el paquete de demostración We.Gov.
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
translation-type: tm+mt
source-git-commit: f323b490c37effc3cbb36c793b62fa788eca9545

---


# Recorrido por el sitio de referencia We.Gov{#we-gov-reference-site-walkthrough}

## Requisitos previos {#pre-requisites}

Configure el sitio de referencia tal como se describe en [Configurar y configurar el sitio](../../forms/using/forms-install-configure-gov-reference-site.md)de referencia de We.Gov.

## Artículo del usuario {#user-story}

* Formularios AEM

   * Captura de datos
   * Integración de datos (MS Dynamics)
   * Adobe Sign

* Flujo de trabajo
* Comunicaciones de clientes

   * Canal de impresión
   * Canal web

* Adobe Analytics

### Fictitious users and groups {#fictitious-users-and-groups}

El paquete de demostración de We.Gov incluye los siguientes usuarios ficticios integrados:

* **Aya Tan**: Ciudadano con derecho a un servicio de un organismo público

![Usuario ficticio](/help/forms/using/assets/aya_tan_new.png)

* **George Lang**: Analista comercial de la agencia We.Gov

![Usuario ficticio](/help/forms/using/assets/george_lang.png)

* **Camila Santos**: Líder del CX de la agencia We.Gov

![Usuario ficticio](/help/forms/using/assets/camila_santos.png)

También se incluyen los siguientes grupos:

* **Usuarios de formularios We.Gov**

   * George Lang (miembro)
   * Camila Santos (miembro)

* **Usuarios de We.Gov**

   * George Lang (miembro)
   * Camila Santos (miembro)
   * Aya Tan (miembro)

### Leyenda de términos de información general de demostración {#demo-overview-terms-legend}

1. **Suplantar**: Se han definido Usuarios y grupos en la demostración de AEM.
1. **Botón**: Rectángulo de color o flecha con círculo para desplazarse.
1. **Haga clic**: Para ejecutar una acción en el artículo del usuario.
1. **Vínculos**: Ubicado en la parte superior del menú principal en el sitio Web We.Gov.
1. **Instrucciones** del usuario: Un conjunto de pasos numéricos a seguir al navegar por el artículo del usuario.
1. **Forms Portal**: *https://&lt;aemserver>:&lt;puerto>/content/we-gov/formsportal.html*
1. **Vista** móvil: usuario de We.Gov para replicar una vista móvil con un navegador de nuevo tamaño.
1. **Vista** de escritorio: Demostración de usuario de We.gov a vista en un ordenador portátil o de escritorio.
1. **Formulario** de prefiltro: Formulario en la Página de inicio del sitio Web We.Gov.
1. **Formulario** adaptable: Formulario de solicitud de inscripción para la demostración de We.gov.

   *https://&lt;aemserver>:&lt;puerto>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Sitio** Adobe We.Gov: *https://&lt;aemserver>:&lt;puerto>/content/we-gov/home.html*
1. **Bandeja de entrada** de Adobe: Se encuentra el icono [de](assets/bell.svg) celda de la barra de menús superior en el servidor AEM.

   *https://&lt;aemserver>:&lt;puerto>/aem/start.html*

1. **Cliente** de correo electrónico: Forma preferida de vista de los correos electrónicos (Gmail, Outlook)
1. **CTA**: Llamada a acción
1. **Navegar**: Para localizar un punto de referencia específico en la página del explorador.

## Demostración de vista móvil {#mobile-view-demo}

**Esta sección debe realizarse antes de la demostración.**

**Instrucciones del usuario:**

1. Vaya a: *https://&lt;aemserver>:&lt;puerto>/content/we-gov/home.html*
1. Iniciar sesión con:

   1. **Usuario**: aya.tan
   1. **Contraseña**: password

1. Cambie el tamaño de la ventana del explorador o utilice el emulador del explorador para replicar un tamaño de dispositivo móvil.

### Historia del usuario de Aya (sitio web We.Gov) {#aya-user-story-we-gov-website}

![Usuario ficticio](/help/forms/using/assets/aya_tan_new-1.png)

**Esta sección**: Aya es un ciudadano. Ella escucha de un amigo que podría ser elegible para recibir un Servicio de una agencia gubernamental. Aya navega al sitio web We.Gov desde su teléfono móvil para conocer más sobre los servicios a los que puede acceder.

### Historia del usuario de Aya (Antecedentes de We.Gov) {#aya-user-story-we-gov-pre-screener}

Aya responde algunas preguntas para confirmar su elegibilidad rellenando un breve formulario adaptable en su teléfono móvil.

**Instrucciones del usuario:**

1. Realice una selección en cada campo desplegable.

   1. Nota: Si el usuario gana más de $200.000 al año, no es elegible.

1. Haga clic en &quot;¿**Soy elegible?**” botón.
1. Haga clic en el botón &quot;**Aplicar ahora**&quot; para continuar.

   ![Aplicar ahora vínculo](/help/forms/using/assets/apply_now_link.png)

### Aya User Story (Formulario adaptable We.Gov) {#aya-user-story-we-gov-adaptive-form}

Aya descubre que es elegible y comienza a completar su solicitud para solicitar servicio en su dispositivo móvil.

Aya necesita revisar algunos documentos en casa antes de completar la solicitud de servicio. Ella guarda y sale de la aplicación.

**Instrucciones del usuario:**

1. Rellene los campos de información Básica, los siguientes son campos y desplegables obligatorios:

   1. Información básica

      1. Nombre
      1. Segundo nombre
      1. Apellidos
      1. Nombre preferido
      1. DOB
      1. Sexo
   1. Información de contacto

      1. Dirección
      1. Ciudad
      1. Número de teléfono
      1. Código postal
      1. Correo electrónico
      1. Estado
   1. Estado marcial

      1. Estado de familia



1. Utilice la siguiente lógica **** dinámica para mostrar la función dinámica mediante el menú desplegable Estado **de la** familia:

   1. **Único**: Mostrar el siguiente panel de parentesco
   1. **Casado**: Mostrar panel dependiente del matrimonio
   1. **Divorciado**: Mostrar el siguiente panel de parentesco
   1. **Viudo**: Mostrar el siguiente panel de parentesco
   1. **¿Tienes hijos?**:: (Sí/No) para mostrar el panel dependiente del niño.

      1. (Añadir/Eliminar) para agregar/quitar varios paneles dependientes secundarios.

1. Haga clic en la flecha derecha en la barra de menús gris.
1. Haga clic en el botón Guardar en la parte inferior.

   ![Detalles del formulario adaptable](/help/forms/using/assets/adaptive_form.png)

## Demostración de escritorio {#desktop-demo}

**Esta sección:** De vuelta en casa, Aya ha encontrado la información que necesitaba y reanuda la aplicación desde su escritorio. Aya navega al portal de formularios en línea para reanudar su solicitud. Con una simple personalización, las agencias también pueden generar y enviar por correo electrónico automáticamente un vínculo para reanudar la aplicación.

### Aya User Story (formulario adaptable continuado) {#aya-user-story-continued-adaptive-form}

**Instrucciones del usuario:**

1. Vaya a *https://&lt;aemserver>:&lt;puerto>/content/we-gov/home.html*
1. En la barra de navegación, seleccione &quot;**Online Services**&quot;.
1. En el panel &quot;Borradores de formularios&quot;, seleccione la &quot;Solicitud de inscripción para beneficios de salud&quot; existente.

   ![Solicitud de inscripción para beneficios de salud](/help/forms/using/assets/enrollment_application.png)

   El aspecto es el mismo y no necesita volver a introducir ningún dato.

   **Instrucciones del usuario:**

1. Haga clic en CTA del círculo derecho para desplazarse a la siguiente sección.

   ![CTA circular de RI](/help/forms/using/assets/right_circle_cta_new.png)

   El formulario se rellena hasta el punto de la última entrada de Aya. Aya ha ingresado toda su información y está lista para enviarla.

   ![Envío del formulario adaptable](/help/forms/using/assets/submit_adaptive_form.png)

   Después de enviar Aya recibe un correo electrónico que abre y está lista para firmar electrónicamente con Adobe Sign.

**Instrucciones del usuario:**

1. Después del envío se mostrará una página de agradecimiento.
1. Vaya al cliente de correo electrónico y busque el correo electrónico de Adobe Sign.
1. Haga clic en el vínculo a Adobe Sign.

   ![Vínculo de firma de Adobe](/help/forms/using/assets/adobe_sign_link.png)

**Instrucciones del usuario:**

1. Marque la casilla &quot;**Estoy de acuerdo**&quot;.
1. Haga clic en &quot;**Aceptar**&quot;.
1. Desplácese hasta la parte inferior del documento revisado.
1. Haga clic en la ficha amarilla resaltada para firmar el documento.

   ![Firmar el documento](/help/forms/using/assets/sign_document_new.png) ![Firmar el documento de prueba](/help/forms/using/assets/sign_test_document.png)

## Agente gubernamental (George) {#government-agent-george}

![Agente de gobierno George](/help/forms/using/assets/george_lang-1.png)

**Esta sección:** George es analista de negocios en la agencia gubernamental de la que Aya solicita un servicio. George tiene un solo panel donde puede ver todas las solicitudes de solicitud de servicio que le han sido asignadas para su revisión.

### George User Story (bandeja de entrada de AEM) {#george-user-story-aem-inbox}

**Instrucciones del usuario:**

1. Vaya a *https://&lt;aemserver>:&lt;puerto>/aem/start.html*
1. Haga clic en el icono de usuario (esquina superior derecha) y utilice la opción de menú &quot;**Cerrar sesión**&quot; o &quot;**Suplantar como**&quot; si ha iniciado sesión con un usuario administrativo.

   1. Iniciar sesión con:

      1. **Usuario:** george.lang
      1. **Contraseña:** password
   1. O Suplantar:

      1. Escriba &quot;**George**&quot; en el campo &quot;**Suplantar como**&quot;.

      1. Haga clic en Aceptar para suplantar.


1. En la esquina superior derecha, haga clic en el icono Notificación (campana).
1. Haga clic en &quot;**Vista de todo**&quot; para desplazarse a la Bandeja de entrada.
1. En la Bandeja de entrada, abra la tarea más reciente &quot;Revisión **de la aplicación de beneficios** sanitarios&quot;.

   ![Revisión de la aplicación de beneficios de salud](/help/forms/using/assets/health_benefits.png)

### George User Story (bandeja de entrada de AEM y MS Dynamics) {#george-user-story-aem-inbox-and-ms-dynamics}

Gracias a las integraciones de datos y a los flujos de trabajo automatizados, aparece la aplicación de Aya, junto con un registro CRM que se generó automáticamente al enviar los datos.

**Instrucciones del usuario:**

1. Abra e inspeccione el formulario adaptable de solo lectura.
1. Haga clic en el botón &quot;**Abrir dinámica de MS**&quot; para abrir el registro de MS Dynamics en una ventana nueva.
1. En CRM puede ver toda la información que se puede actualizar

   1. De forma opcional, agregue algunas notas de revisión directamente en Dynamics.

1. Cierre y vuelva a la Bandeja de entrada de AEM.

   ![Registro de MS Dynamics](/help/forms/using/assets/ms_dynamics.png)

### George User Story (de vuelta a la bandeja de entrada de AEM) {#george-user-story-back-to-aem-inbox}

George aprueba la aplicación de Aya, y gracias a un flujo de trabajo automatizado existente también se envía un correo electrónico de confirmación a Aya.

**Instrucciones del usuario:**

1. Vaya a la esquina superior izquierda y haga clic en &quot;**Aprobar**&quot; para aprobar la aplicación.
1. En el modal, puede dejar un mensaje para el posible cliente CX.
1. Haga clic en Finalizado.
1. (Función ciudadana) Abra su cliente de correo electrónico para la vista del correo electrónico enviado a Aya.

   ![Vista del correo electrónico enviado a Aya](/help/forms/using/assets/email_client.png)

## Líder CX (Camila) {#cx-lead-camila}

![Camila (posible cliente de CX)](/help/forms/using/assets/camila_santos-1.png)

**Esta sección:** Camila the CX Lead configura una llamada de bienvenida con Aya para explicar cómo hacer uso de los servicios gubernamentales para los que ha sido aprobada.

### Artículo del usuario de Camila (bandeja de entrada de AEM y MS Dynamics) {#camila-user-story-aem-inbox-ms-dynamics}

**Instrucciones del usuario:**

1. Vaya a *https://&lt;aemserver>:&lt;puerto>/aem/start.html*
1. Haga clic en el icono de usuario (esquina superior derecha) y utilice la opción de menú &quot;**Cerrar sesión**&quot; o &quot;**Suplantar como**&quot; si ha iniciado sesión con un usuario administrativo.

   1. Iniciar sesión con:

      1. **Usuario**: camila.santos
      1. **Contraseña**: password
   1. O Suplantar:

      1. Escriba &quot;**Camila**&quot; en el campo &quot;**Suplantar como**&quot;.

      1. Haga clic en Aceptar para suplantar.


1. En la esquina superior derecha, haga clic en el icono Notificación (campana).
1. Haga clic en &quot;**Vista de todo**&quot; para desplazarse a la Bandeja de entrada.
1. En la Bandeja de entrada, abra la última tarea &quot;**Nueva aprobación** de contacto&quot;.

   ![Nueva aprobación de contacto](/help/forms/using/assets/new_contact_approval.png)

   **Instrucciones del usuario:**

1. Abra e inspeccione el formulario adaptable de solo lectura.
1. Haga clic en el botón &quot;**Abrir dinámica de MS**&quot; para abrir el registro de MS Dynamics en una ventana nueva.
1. En CRM puede ver toda la información que se puede actualizar

   1. De forma opcional, agregue una nueva actividad de llamada directamente en Dynamics.
   1. Abra la sección &quot;**Actividades**&quot;.
   1. Haga clic en la opción &quot;**Nueva llamada** telefónica&quot;.
   1. Añada los detalles de la llamada telefónica.
   1. Guarde y cierre la ventana.

1. De nuevo en AEM, vaya a la esquina superior izquierda y haga clic en &quot;**Enviar**&quot; para enviar la aplicación.
1. En el modal, puede dejar un mensaje.
1. Haga clic en Finalizado.

   ![Ficha](/help/forms/using/assets/activities_tab.png) Actividades ![Confirmar nuevo contacto](/help/forms/using/assets/confirm_new_contact.png)

## Bienvenido Kit ciudadano (Aya) {#welcome-kit-citizen-aya}

**Esta sección:** Aya recibe un correo electrónico que contiene un enlace a una comunicación interactiva que resume sus beneficios e incluye también campos de formulario para rellenar. Con la declaración de beneficios en PDF adjunta y el enlace a la carta de comunicación interactiva en el correo (con el mismo tema/marca que la comunicación interactiva).

### Aya User Story (cliente de correo electrónico) {#aya-user-story-email-client}

**Instrucciones del usuario:**

1. Busque y abra el correo electrónico del Kit de bienvenida.
1. Desplácese hasta archivos PDF adjuntos en la parte inferior de la página.
1. Haga clic para abrir el archivo adjunto PDF.
1. Desplácese hacia arriba en su cliente de correo electrónico y haga clic en &quot;Kit de bienvenida de **Vista en línea**&quot;.

   1. Esto abrirá la versión de canal web del mismo documento.

1. Para obtener una referencia rápida a PDF directamente:

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-Handbook*

1. Para una rápida referencia a IC directamente:

   *https://&lt;aemserver>:&lt;puerto>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?canal=web&amp;mode=previsualización&amp;wcmmode=disabled*

   ![Vínculo de comunicación](/help/forms/using/assets/welcome_benefits_handbook.png) interactiva del Manual ![de beneficios de bienvenida](/help/forms/using/assets/interactive_communication.png)

## Ciudadano Que Recuerda La Renovación (Aya) {#renewal-reminder-citizen-aya}

**Esta sección:** Camila también programa un recordatorio de comunicación un año después. (Paso del flujo de trabajo que automatiza/ejecuta y envía un correo electrónico).

### Aya User Story (cliente de correo electrónico) {#aya-user-story-email-client-1}

**Instrucciones del usuario:**

1. Navegue hasta el cliente de correo electrónico.
1. Busque y abra el correo electrónico del recordatorio de renovación.
1. Haga clic en el botón &quot;**Enviar una nueva aplicación**&quot; para abrir el formulario adaptable.

   1. Esta sección se deja en blanco intencionalmente para admitir datos previamente rellenados en la fase 2.
   ![Correo electrónico del recordatorio de renovación](/help/forms/using/assets/renewal_reminder_email.png)

## Líder de Analytics CX (Camila) {#analytics-cx-lead-camila}

**Esta sección:** Camila navega a un panel donde puede ver en todos los KPI de la agencia como el porcentaje de ciudadanos que inicio llenar un formulario de solicitud de servicio y abandonarlo, el tiempo promedio desde el envío de la solicitud hasta la respuesta de aprobación/denegación, y estadísticas de participación para los manuales de beneficios que ha enviado a los ciudadanos.

### Camila revisa el sistema de informes de sitios (Adobe Analytics de We.Gov) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. Vaya a *https://&lt;aemserver>:&lt;puerto>/sites.html/content*
1. Seleccione el &quot;**AEM Forms We.Gov Site**&quot; para la vista de las páginas del sitio.
1. Seleccione una de las páginas del sitio (p. ej. Inicio) y elija &quot;**Analytics y recomendaciones**&quot;.

   ![Analytics y Recomendaciones](/help/forms/using/assets/analytics_recommendation.jpg)

1. En esta página, verá información recuperada de Adobe Analytics que se refiere a la página Sitios de AEM (NOTA: por diseño, esta información se actualiza periódicamente desde Adobe Analytics y no se muestra en tiempo real).

   ![Métricas clave de Adobe Analytics](/help/forms/using/assets/analytics_key_metrics.jpg)

1. De nuevo en la página de vista de página (a la que se accede en el paso 3), también puede realizar la vista de la información de vista de página cambiando la configuración de visualización a elementos de vista en la &quot;Vista **de** Lista&quot;.
1. Busque el menú desplegable &quot;**Vista**&quot; y seleccione &quot;Vista **de** Lista&quot;.

   ![vista de Lista en el menú desplegable Vista](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. En el mismo menú, seleccione &quot;Configuración **de** Vista&quot; y seleccione las columnas que desee mostrar en la sección &quot;**Análisis**&quot;.

   ![Configurar la visualización de columnas](/help/forms/using/assets/view_setting_analytics.jpg)

1. Haga clic en &quot;**Actualizar**&quot; para que las nuevas columnas estén disponibles.

   ![Hacer que las columnas nuevas estén disponibles](/help/forms/using/assets/new_columns_available.jpg)

### Camila revisa el sistema de informes de formularios (Adobe Analytics de We.Gov) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. Ir a

   *https://&lt;aemserver>:&lt;puerto>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. Seleccione el formulario adaptable &quot;**Solicitud de inscripción para beneficios** de salud&quot; y seleccione la opción &quot;Informe **de análisis**&quot;.

   ![Solicitud de inscripción para beneficios de salud](/help/forms/using/assets/analytics_report_benefits.jpg)

1. Espere a que se cargue la página y vista los datos del informe de Analytics.

   ![Datos de informes de Analytics](/help/forms/using/assets/analytics_report_data_updated.jpg)

