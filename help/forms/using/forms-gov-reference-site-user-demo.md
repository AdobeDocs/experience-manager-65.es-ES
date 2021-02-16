---
title: Recorrido por el sitio de referencia de We.Gov y We.Finance
seo-title: Recorrido por el sitio de referencia de We.Gov y We.Finance
description: Use usuarios y grupos ficticios para realizar tareas de AEM Forms con el paquete de demostración We.Gov y We.Finance.
seo-description: Use usuarios y grupos ficticios para realizar tareas de AEM Forms con el paquete de demostración We.Gov y We.Finance.
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
translation-type: tm+mt
source-git-commit: c6b8e184042394d99ceb099c918b81e2cce49497
workflow-type: tm+mt
source-wordcount: '2548'
ht-degree: 1%

---


# Recorrido del sitio de referencia de We.Gov y We.Finance {#we-gov-reference-site-walkthrough}

## Requisitos previos {#pre-requisites}

Configure el sitio de referencia tal como se describe en [Configure y configure el sitio de referencia We.Gov y We.Finance](../../forms/using/forms-install-configure-gov-reference-site.md).

## Artículo del usuario {#user-story}

* AEM Forms

   * Conversión automatizada de formularios
   * Creación  
   * Modelos de datos de formulario/Fuentes de datos

* AEM Forms

   * Captura de datos
   * (Opcional) Integración de datos (MS Dynamics)
   * (Opcional) Adobe Sign

* Flujo de trabajo
* Notificaciones de correo electrónico
* (Opcional) Comunicaciones con los clientes

   * Canal de impresión
   * Canal web

* Adobe Analytics
* Integraciones de fuentes de datos

### Usuarios y grupos ficticios {#fictitious-users-and-groups}

El paquete de demostración de We.Gov incluye los siguientes usuarios ficticios integrados:

* **Aya Tan**: Ciudadano con derecho a un servicio de un organismo público

![Usuario ficticio](/help/forms/using/assets/aya_tan_new.png)

* **George Lang**: Analista comercial de la agencia We.Gov

![Usuario ficticio](/help/forms/using/assets/george_lang.png)

* **Camila Santos**: Líder del CX de la agencia We.Gov

![Usuario ficticio](/help/forms/using/assets/camila_santos.png)

También se incluyen los siguientes grupos:

* **Usuarios de Forms de We.Gov**

   * George Lang (miembro)
   * Camila Santos (miembro)

* **Usuarios de We.Gov**

   * George Lang (miembro)
   * Camila Santos (miembro)
   * Aya Tan (miembro)

### Leyenda de términos generales de demostración {#demo-overview-terms-legend}

1. **Suplantar**: Se definieron Usuarios y grupos en AEM demostración.
1. **Botón**: Rectángulo de color o flecha con círculo para desplazarse.
1. **Haga clic**: Para ejecutar una acción en el artículo del usuario.
1. **Vínculos**: Ubicado en la parte superior del menú principal en el sitio Web We.Gov.
1. **Instrucciones** del usuario: Un conjunto de pasos numéricos a seguir al navegar por el artículo del usuario.
1. **Forms Portal**:  *https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*
1. **Vista** móvil: usuario de We.Gov para replicar una vista móvil con un navegador de nuevo tamaño.
1. **Vista** de escritorio: Demostración de usuario de We.gov a vista en un ordenador portátil o de escritorio.
1. **Formulario** de prefiltro: Formulario en la Página de inicio del sitio Web We.Gov.
1. **Formulario** adaptable: Formulario de solicitud de inscripción para la demostración de We.gov.

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Sitio** We.Gov de Adobe:  *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **Bandeja de entrada** de Adobe: Se encuentra en la barra de menús superior  [Icono ](assets/bell.svg) Bell en AEM back-end.

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **Cliente** de correo electrónico: Forma preferida de vista de los correos electrónicos (Gmail, Outlook)
1. **CTA**: Llamada a acción
1. **Navegar**: Para localizar un punto de referencia específico en la página del explorador.
1. **AFC**: automated forms conversion

## automated forms conversion (Camila) {#automated-forms-conversion}

**Esta sección**: Camila el posible cliente de CX tiene un formulario basado en PDF que se utilizó como parte de un proceso basado en papel. Como parte de un esfuerzo de modernización, quiere utilizar este formulario PDF para crear automáticamente un nuevo Forms adaptable moderno.

### automated forms conversion: We.Gov (Camila) {#automated-forms-conversion-wegov}

1. Vaya a *https://&lt;aemserver>:&lt;puerto>/aem/start.html*

1. Iniciar sesión con:
   * **Usuario**: camila.santos
   * **Contraseña**: password
1. En la página principal, seleccione Forms > Forms y Documentos > AEM Forms We.gov Forms > AFC.
1. Camila carga el PDF en AEM Forms.

   ![Cargar formulario](assets/aftia-upload-form.jpg)

1. Luego, Camilla selecciona el formulario PDF y hace clic **Conversión automatizada de Inicio** para inicio del proceso de conversión. Es posible que deba hacer clic en **Sobrescribir conversión** si ha convertido el formulario.

   >[!NOTE]
   >
   >Tenga en cuenta que los ajustes de AFC están preconfigurados para el usuario final, lo que significa que no deben modificarse.

   * **Opcional**: Si desea utilizar el tema Ultramarino accesible, simplemente haga clic en el tema Especificar un formulario adaptable y seleccione el tema Accesible-Ultramarino que aparece en la lista de opciones.

   ![Conversión de inicios](assets/aftia-start-conversion.jpg)

   ![Tema ultramarino](assets/aftia-upload-conversion-settings.jpg)

   El estado de porcentaje completado se muestra durante la conversión. Una vez que se muestre el estado **Convertido**, haga clic en la carpeta **salida**, seleccione el formulario adaptable y haga clic en **Editar** para abrir el formulario convertido.

1. A continuación, Camilla revisa el formulario y se asegura de que todos los campos están presentes

   ![Revisar conversión](assets/aftia-review-conversion.jpg)

1. Después, Camilla inicio para editar el formulario. Ella selecciona Panel raíz > Editar (la llave inglesa) > selecciona Fichas arriba en el menú desplegable Diseño del panel > selecciona la casilla de verificación.

   ![Revisar propiedades](assets/aftia-review-properties.jpg)

1. Luego, Camilla agrega todas las modificaciones necesarias de CSS y campo para producir el producto final.

   ![Añadir CSS](assets/aftia-add-css.jpg)

### Modelo de datos de formulario y fuentes de datos (Camila) {#data-sources}

**Esta sección**: Una vez que el documento se ha convertido y producido un formulario adaptable, Camila debe conectar el formulario adaptable a un origen de datos.

1. Camila abre las Propiedades en el formulario convertido en [Automated forms conversion - We.Gov](#automated-forms-conversion-wegov).

1. A continuación, Camila selecciona Modelo de formulario > Selecciona Modelo de datos de formulario en el menú desplegable Seleccionar de > Selecciona FDM de matriculación de We.gov en la opción lista de.

1. Haga clic en el botón Guardar y cerrar.

   ![Selección de FDM](assets/aftia-select-fdm.jpg)

1. Camila hace clic en la carpeta **output**, selecciona el formulario adaptable y hace clic **Editar** para abrir el formulario We.Gov completado.
1. Camila selecciona un campo de formulario adaptable y hace clic en ![Configurar icono](assets/configure-icon.svg). Crea enlaces con las entidades del modelo de datos de formulario mediante el campo **Referencia de enlace**. Repite este paso en todos los campos del formulario adaptable.

### Prueba de accesibilidad del formulario (Camila) {#form-accessibility-testing}

Camila también valida que el contenido creado se haya creado correctamente y sea totalmente accesible según los estándares corporativos.

1. Camila hace clic en la carpeta **output**, selecciona el formulario adaptable y hace clic **Previsualización** para abrir el formulario We.Gov completado.

1. Abre la ficha Auditoría en la herramienta para desarrolladores de Chrome.

1. Realiza una comprobación de accesibilidad para validar el formulario adaptable.

   ![Comprobación de accesibilidad](assets/aftia-accessibility.jpg)

## Demostración De Vista Móvil De Formulario Adaptable (Aya) {#mobile-view-demo}

**Esta sección debe realizarse antes de la demostración.**

**Instrucciones del usuario:**

1. Vaya a: *https://&lt;aemserver>:&lt;puerto>/content/we-gov/home.html*
1. Iniciar sesión con:

   1. **Usuario**: aya.tan
   1. **Contraseña**: password

1. Cambie el tamaño de la ventana del explorador o utilice el emulador del explorador para replicar un tamaño de dispositivo móvil.

### Sitio Web We.Gov (Aya) {#aya-user-story-we-gov-website}

![Usuario ficticio](/help/forms/using/assets/aya_tan_new-1.png)

**Esta sección**: Aya es un ciudadano. Ella escucha de un amigo que podría ser elegible para recibir un Servicio de una agencia gubernamental. Aya navega al sitio web We.Gov desde su teléfono móvil para conocer más sobre los servicios a los que puede acceder.

### Pre-Screener de We.Gov (Aya) {#aya-user-story-we-gov-pre-screener}

Aya responde algunas preguntas para confirmar su elegibilidad rellenando un breve formulario adaptable en su teléfono móvil.

**Instrucciones del usuario:**

1. Realice una selección en cada campo desplegable.

   >[!NOTE]
   >
   >Si el usuario gana más de $200.000 al año, no es elegible.

1. Haga clic en &quot;**¿Cumplo los requisitos?**” botón.
1. Haga clic en el botón &quot;**Aplicar ahora**&quot; para continuar.

   ![Aplicar ahora vínculo](/help/forms/using/assets/apply_now_link.png)

### Formulario adaptable We.Gov (Aya) {#aya-user-story-we-gov-adaptive-form}

Aya descubre que es elegible y comienza a completar su solicitud para solicitar servicio en su dispositivo móvil.

Aya necesita revisar algunos documentos en casa antes de completar la solicitud de servicio. Guarda y sale de la aplicación desde su dispositivo móvil.

**Instrucciones del usuario:**

1. Rellene los campos de información Básica, los siguientes son campos y desplegables obligatorios:

   1. Información básica

      1. Nombre
      1. Apellidos
      1. DOB
      1. Correo electrónico

1. Utilice la siguiente **lógica dinámica** para mostrar la función dinámica mediante la lista desplegable **Estado de la familia**:

   1. **Único**: Mostrar el siguiente panel de parentesco
   1. **Casado**: Mostrar panel dependiente del matrimonio
   1. **Divorciado**: Mostrar el siguiente panel de parentesco
   1. **Viudo**: Mostrar el siguiente panel de parentesco
   1. **¿Tienes hijos?**:: (Sí/No) para mostrar el panel dependiente del niño.

      1. (Añadir/Eliminar) para agregar/quitar varios paneles dependientes secundarios.

1. Haga clic en la flecha derecha en la barra de menús gris.
1. Haga clic en el botón Guardar en la parte inferior.

   ![Detalles del formulario adaptable](/help/forms/using/assets/adaptive_form.png)

## Demostración en escritorio {#desktop-demo}

**Esta sección:** De vuelta en casa, Aya ha encontrado la información que necesitaba y reanuda la aplicación desde su escritorio. Aya navega al portal de formularios en línea para reanudar su solicitud. Con una simple personalización, las agencias también pueden generar y enviar por correo electrónico automáticamente un vínculo para reanudar la aplicación.

### Formulario Adaptable Continuo (Aya) {#aya-user-story-continued-adaptive-form}

**Instrucciones del usuario:**

1. Vaya a *https://&lt;aemserver>:&lt;puerto>/content/we-gov/home.html*
1. En la barra de navegación, seleccione hacer clic en &quot;**Servicios en línea**&quot;.
1. En el panel &quot;Borrador de Forms&quot;, seleccione la &quot;Solicitud de inscripción para beneficios de salud&quot; existente.

   ![Solicitud de inscripción para beneficios de salud](/help/forms/using/assets/enrollment_application.png)

   El aspecto es el mismo y no necesita volver a introducir ningún dato.

   **Instrucciones del usuario:**

1. Haga clic en CTA del círculo derecho para desplazarse a la siguiente sección.

   ![CTA circular de RI](/help/forms/using/assets/right_circle_cta_new.png)

   El formulario se rellena hasta el punto de la última entrada de Aya. Aya ha ingresado toda su información y está lista para enviarla.

   ![Envío del formulario adaptable](/help/forms/using/assets/submit_adaptive_form.png)

   >[!NOTE]
   >
   >Cuando Aya rellena el campo del número de teléfono, debe rellenarlo como un número continuo de 11 dígitos sin guiones, espacios ni guiones.

   Después de enviar Aya recibe una página de agradecimiento. Opcionalmente, también recibirá un correo electrónico que podrá abrir para firmar electrónicamente el documento del registro con Adobe Sign.

### Opcional: Adobe Sign (Aya) {#adobe-sign}

**Instrucciones del usuario:**

1. Vaya al cliente de correo electrónico y busque el correo electrónico de Adobe Sign.
1. Haga clic en el vínculo a Adobe Sign.

   ![Vínculo de firma de Adobe](/help/forms/using/assets/adobe_sign_link.png)

**Instrucciones del usuario:**

1. Marque la casilla &quot;**Acepto**&quot;.
1. Haga clic en &quot;**Aceptar**&quot;.
1. Desplácese hasta la parte inferior del documento revisado.
1. Haga clic en la ficha amarilla resaltada para firmar el documento.

   ![Firmar el ](/help/forms/using/assets/sign_document_new.png) ![documento Firmar el documento de prueba](/help/forms/using/assets/sign_test_document.png)

## Agente gubernamental (George) {#government-agent-george}

![Agente de gobierno George](/help/forms/using/assets/george_lang-1.png)

**Esta sección:** George es un analista de negocios de la agencia gubernamental de la que Aya solicita un servicio. George tiene un solo panel donde puede ver todas las solicitudes de solicitud de servicio que le han sido asignadas para su revisión.

### Bandeja de entrada AEM (George) {#george-user-story-aem-inbox}

**Instrucciones del usuario:**

1. Vaya a *https://&lt;aemserver>:&lt;puerto>/aem/start.html*
1. Haga clic en el icono de usuario (esquina superior derecha) y utilice la opción de menú &quot;**Cerrar sesión**&quot; o la opción de menú &quot;**Suplantar como**&quot; si ha iniciado sesión con un usuario administrativo.

   1. Iniciar sesión con:

      1. **Usuario:** george.lang
      1. **Contraseña:** contraseña
   1. O Suplantar:

      1. Escriba &quot;**George**&quot; en el campo &quot;**Suplantar como**&quot;.

      1. Haga clic en Aceptar para suplantar.


1. En la esquina superior derecha, haga clic en el icono Notificación (campana).
1. Haga clic en &quot;**Vista de todo**&quot; para navegar a la Bandeja de entrada.
1. En la Bandeja de entrada, abra la última tarea &quot;**Health Benefits Application Review**&quot;.

   ![Revisión de la aplicación de beneficios de salud](/help/forms/using/assets/health_benefits.png)

### Opcional: Bandeja de entrada AEM y MS Dynamics (George) {#george-user-story-aem-inbox-and-ms-dynamics}

Gracias a las integraciones de datos y a los flujos de trabajo automatizados, aparece la aplicación de Aya, junto con un registro CRM que se generó automáticamente al enviar los datos.

**Instrucciones del usuario:**

1. Abra e inspeccione el formulario adaptable de solo lectura.
1. Haga clic en el botón &quot;**Abrir MS Dynamics**&quot; para abrir el registro de MS Dynamics en una ventana nueva.
1. En CRM puede ver toda la información que se puede actualizar

   1. De forma opcional, agregue algunas notas de revisión directamente en Dynamics.

1. Cierre y vuelva a AEM Bandeja de entrada.

   ![Registro de MS Dynamics](/help/forms/using/assets/ms_dynamics.png)

### Volver a AEM bandeja de entrada (George) {#george-user-story-back-to-aem-inbox}

George aprueba la aplicación de Aya, y gracias a un flujo de trabajo automatizado existente también se envía un correo electrónico de confirmación a Aya.

**Instrucciones del usuario:**

1. Vaya a la esquina superior izquierda y haga clic en &quot;**Aprobar**&quot; para aprobar la aplicación.
1. En el modal, puede dejar un mensaje para el posible cliente CX.
1. Haga clic en Finalizado.
1. (Función ciudadana) Abra su cliente de correo electrónico para la vista del correo electrónico enviado a Aya.

   ![Vista del correo electrónico enviado a Aya](/help/forms/using/assets/email_client.png)

## Líder CX (Camila) {#cx-lead-camila}

![Camila (posible cliente de CX)](/help/forms/using/assets/camila_santos-1.png)

**Esta sección:** Camila el posible cliente de CX configura una llamada telefónica de bienvenida con Aya para explicar cómo hacer uso de los servicios gubernamentales para los que ha sido aprobada.

### (Opcional) AEM Bandeja de entrada y MS Dynamics {#camila-user-story-aem-inbox-ms-dynamics}

**Instrucciones del usuario:**

1. Vaya a *https://&lt;aemserver>:&lt;puerto>/aem/start.html*
1. Haga clic en el icono de usuario (esquina superior derecha) y utilice la opción de menú &quot;**Cerrar sesión**&quot; o la opción de menú &quot;**Suplantar como**&quot; si ha iniciado sesión con un usuario administrativo.

   1. Iniciar sesión con:

      1. **Usuario**: camila.santos
      1. **Contraseña**: password
   1. O Suplantar:

      1. Escriba &quot;**Camila**&quot; en el campo &quot;**Suplantar como**&quot;.

      1. Haga clic en Aceptar para suplantar.


1. En la esquina superior derecha, haga clic en el icono Notificación (campana).
1. Haga clic en &quot;**Vista de todo**&quot; para navegar a la Bandeja de entrada.
1. En la Bandeja de entrada, abra la última tarea &quot;**Nueva aprobación de contacto**&quot;.

![Nueva aprobación de contacto](/help/forms/using/assets/new_contact_approval.png)

**(Opcional) Instrucciones del usuario:**

1. Abra e inspeccione el formulario adaptable de solo lectura.
1. Haga clic en el botón &quot;**Abrir MS Dynamics**&quot; para abrir el registro de MS Dynamics en una ventana nueva.
1. En CRM puede ver toda la información que se puede actualizar

   1. De forma opcional, agregue una nueva actividad de llamada directamente en Dynamics.
   1. Abra la sección &quot;**Actividades**&quot;.
   1. Haga clic en la opción &quot;**Nueva llamada de teléfono**&quot;.
   1. Añada los detalles de la llamada telefónica.
   1. Guarde y cierre la ventana.

1. Vuelva a AEM, desplácese hasta la esquina superior izquierda y haga clic en &quot;**Enviar**&quot; para enviar la aplicación.
1. En el modal, puede dejar un mensaje.
1. Haga clic en Finalizado.

   ![Ficha actividades ](/help/forms/using/assets/activities_tab.png) ![Confirmar nuevo contacto](/help/forms/using/assets/confirm_new_contact.png)

## (Opcional) Kit De Bienvenida Ciudadano (Aya) {#welcome-kit-citizen-aya}

**Esta sección:** Aya recibe un correo electrónico que contiene un enlace a una comunicación interactiva que resume sus beneficios e incluye también campos de formulario para rellenar. Con la declaración de beneficios en PDF adjunta y el enlace a la carta de comunicación interactiva en el correo (con el mismo tema/marca que la comunicación interactiva).

### Notificación de cliente de correo electrónico (Aya) {#aya-user-story-email-client}

**Instrucciones del usuario:**

1. Busque y abra el correo electrónico del Kit de bienvenida.
1. Desplácese hasta archivos PDF adjuntos en la parte inferior de la página.
1. Haga clic para abrir el archivo adjunto PDF.
1. Desplácese hacia arriba en el cliente de correo electrónico y haga clic en &quot;**kit de bienvenida de Vista en línea**&quot;.

   1. Esto abrirá la versión de canal web del mismo documento.

1. Para obtener una referencia rápida a PDF directamente:

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-Handbook/we-gov-welcome-Handbook*

1. Para una rápida referencia a IC directamente:

   *https://&lt;aemserver>:&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?canal=web&amp;mode=previsualización&amp;wcmmode=disabled*

   ![Manual ](/help/forms/using/assets/welcome_benefits_handbook.png) ![de beneficios de bienvenidaVínculo de comunicación interactiva](/help/forms/using/assets/interactive_communication.png)

## Ciudadano del recordatorio de renovación (Aya) {#renewal-reminder-citizen-aya}

**Esta sección:** Camila también programa un recordatorio de comunicación un año después. (Paso del flujo de trabajo que automatiza/ejecuta y envía un correo electrónico).

### Notificación de cliente de correo electrónico (Aya) {#aya-user-story-email-client-updated}

**Instrucciones del usuario:**

1. Navegue hasta el cliente de correo electrónico.
1. Busque y abra el correo electrónico del recordatorio de renovación.
1. Haga clic en el botón &quot;**Enviar una nueva aplicación**&quot; para abrir el formulario adaptable.

   1. Esta sección se deja en blanco intencionadamente para admitir los datos que se rellenan previamente en la fase 2.

   ![Correo electrónico del recordatorio de renovación](/help/forms/using/assets/renewal_reminder_email.png)

## (Opcional) Modelo de datos de formulario (Camila) {#form-data-model}

**Esta sección**: Camila se desplaza a Integraciones de datos de AEM Forms, donde puede realizar una prueba rápida para comprobar que la información enviada al origen de datos externo mediante la integración del modelo de datos de formulario está realmente presente.

### Modelo de datos de formulario (Camila) {#form-data-model-camila}

**Esta sección**: Camila navega a la página Fuentes de datos para validar los datos que el servidor ha replicado en la base de datos de Derby.

1. Una vez completada la experiencia del usuario y que se ha completado el envío del usuario, Camila se desplaza a la ficha Fuentes de datos de AEM Forms (**Forms** > **Integraciones de datos**)

1. Luego, Camila selecciona AEM Forms **We.gov FDM** y luego edita el **FDM de inscripción de We.gov**.

1. A continuación, Camila selecciona el **Contacto** > **Servicio de lectura** que se va a probar.

   ![Servicio de lectura de contacto](assets/aftia-contact-read-service.jpg)

1. A continuación, Camila proporciona al servicio de prueba una identificación de contacto y, a continuación, hace clic en el botón Prueba. Por ejemplo, 1 o 2, si ha enviado el formulario. Si no ha enviado el formulario, no se devuelve ningún dato.

   ![Servicio de lectura de contacto](assets/aftia-test-service.jpg)

1. Luego, Camila puede validar que los datos se hayan insertado correctamente en el origen de datos.

   * Los datos dentro de Derby DS tienen el siguiente formato:

   ```xml
      [
         {
         "ADDRESS_COUNTRY": "USA",
         "LAST_NAME": "Tan",
         "ADDRESS_CITY": "New York",
         "FIRST_NAME": "Aya",
         "ADDRESS_STATE": "AL",
         "ADDRESS_LINE1": "123 Street crescent",
         "GENDER_CODE": "2",
         "ADDRESS_LINE2": "123 Street crescent",
         "ADDRESS_POSTAL_CODE": "90210",
         "BIRTH_DATE": "1991-12-12",
         "CONTACT_ID": 1,
         "MIDDLE_NAME": "M",
         "HAS_CHILDREN_CODE": "0"
         }
   ]
   ```

## (Opcional) Analytics (Camila) {#analytics-cx-lead-camila}

**Esta sección:** Camila navega a un panel donde puede ver los KPI de la agencia como el porcentaje de ciudadanos que inicio rellenar un formulario de solicitud de servicio y abandonarlo, el tiempo promedio desde el envío de la solicitud hasta la respuesta de aprobación/denegación, y las estadísticas de participación para los manuales de beneficios que ha enviado a los ciudadanos.

### sistema de informes de sitios de Adobe Analytics (Camila) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. Vaya a *https://&lt;aemserver>:&lt;puerto>/sites.html/content*
1. Seleccione el &quot;**Sitio Web de AEM Forms.Gov**&quot; para realizar la vista de las páginas del sitio.
1. Seleccione una de las páginas del sitio (por ejemplo: Inicio) y elija &quot;**Analytics y Recommendations**&quot;.

   ![Analytics y Recomendaciones](/help/forms/using/assets/analytics_recommendation.jpg)

1. En esta página, verá la información recuperada de Adobe Analytics que se refiere a la página de AEM Sites (NOTA: por diseño, esta información se actualiza periódicamente desde Adobe Analytics y no se muestra en tiempo real).

   ![Métricas clave de Adobe Analytics](/help/forms/using/assets/analytics_key_metrics.jpg)

1. De nuevo en la página de vista de página (a la que se accede en el paso 3.1), también puede realizar la vista de la información de vista de página cambiando la configuración de visualización a elementos de vista en la Vista de Lista &quot;**a1/>&quot;.**
1. Busque el menú desplegable &quot;**Vista**&quot; y seleccione &quot;**Vista de Lista**&quot;.

   ![Vista de lista en el menú desplegable Vista](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. En el mismo menú, seleccione &quot;**Configuración de Vista**&quot; y seleccione las columnas que desee mostrar en la sección &quot;**Análisis**&quot;.

   ![Configurar la visualización de columnas](/help/forms/using/assets/view_setting_analytics.jpg)

1. Haga clic en &quot;**Actualizar**&quot; para que las nuevas columnas estén disponibles.

   ![Hacer que las columnas nuevas estén disponibles](/help/forms/using/assets/new_columns_available.jpg)

### Adobe Analytics Forms Sistema de informes (Camila) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. Ir a

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. Seleccione el formulario adaptable &quot;**Solicitud de inscripción para beneficios de salud**&quot; y seleccione la opción &quot;**Informe de Analytics**&quot;.

   ![Solicitud de inscripción para beneficios de salud](/help/forms/using/assets/analytics_report_benefits.jpg)

1. Espere a que se cargue la página y vista los datos del informe de Analytics.

   ![Datos de informes de Analytics](/help/forms/using/assets/analytics_report_data_updated.jpg)

