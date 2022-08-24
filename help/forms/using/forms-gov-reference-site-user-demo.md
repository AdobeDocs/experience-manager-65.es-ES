---
title: Recorrido por el sitio web de referencia We.Gov y We.Finance
seo-title: We.Gov and We.Finance reference site walkthrough
description: Utilice usuarios y grupos ficticios para realizar tareas de AEM Forms mediante el paquete de demostración We.Gov y We.Finance .
seo-description: Use fictitious users and groups to perform AEM Forms tasks using We.Gov and We.Finance demo package.
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
exl-id: 288d5459-bc69-4328-b6c9-4b4960bf4977
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2526'
ht-degree: 1%

---

# Recorrido por el sitio web de referencia We.Gov y We.Finance {#we-gov-reference-site-walkthrough}

## Requisitos previos {#pre-requisites}

Configure el sitio de referencia tal como se describe en [Configure y configure el sitio de referencia de We.Gov y We.Finance](../../forms/using/forms-install-configure-gov-reference-site.md).

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
* Notificaciones por correo electrónico
* (Opcional) Comunicaciones de los clientes

   * Canal de impresión
   * Canal web

* Adobe Analytics
* Integraciones de fuentes de datos

### Usuarios y grupos ficticios {#fictitious-users-and-groups}

El paquete de demostración de We.Gov viene con los siguientes usuarios ficticios integrados:

* **Aya Tan**: Ciudadano elegible para un servicio de una agencia gubernamental

![Usuario ficticio](/help/forms/using/assets/aya_tan_new.png)

* **George Lang**: Agencia We.Gov Analista Comercial

![Usuario ficticio](/help/forms/using/assets/george_lang.png)

* **Camila Santos**: Líder de We.Gov Agency CX

![Usuario ficticio](/help/forms/using/assets/camila_santos.png)

También se incluyen los siguientes grupos:

* **Usuarios De Forms De We.Gov**

   * George Lang (miembro)
   * Camila Santos (miembro)

* **Usuarios de We.Gov**

   * George Lang (miembro)
   * Camila Santos (miembro)
   * Aya Tan (miembro)

### Leyenda de términos de descripción general de la demostración {#demo-overview-terms-legend}

1. **Suplantar**: Se han definido Usuarios y grupos en AEM demostración.
1. **Botón**: Rectángulo de color o flecha con círculo para desplazarse.
1. **Haga clic en**: Ejecutar una acción en el artículo de usuario.
1. **Vínculos**: Situado en la parte superior del menú principal del sitio de We.Gov.
1. **Instrucciones del usuario**: Un conjunto de pasos numéricos a seguir al navegar por el artículo del usuario.
1. **Portal de Forms**: *https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*
1. **Vista móvil**:Usuario de We.Gov para replicar una vista móvil con un navegador de nuevo tamaño.
1. **Vista de escritorio**: Usuario de We.gov para ver la demostración en un ordenador portátil o de escritorio.
1. **Formulario de prefiltro**: Formulario en la página de inicio del sitio de We.Gov.
1. **Formulario adaptable**: Formulario de solicitud de inscripción para la demostración de We.gov.

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Sitio Web We.Gov De Adobe**: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **Bandeja de entrada de Adobe**: Barra de menús superior [Icono de celda](assets/bell.svg) en AEM backend.

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **Cliente de correo electrónico**: Forma preferida de ver los correos electrónicos (Gmail, Outlook)
1. **CTA**: Llamada a acción
1. **Navegar**: Para localizar un punto de referencia específico en la página del explorador.
1. **AFC**: automated forms conversion

## automated forms conversion (Camila) {#automated-forms-conversion}

**Esta sección**: Camila el CX Lead tiene un formulario basado en PDF existente que se utilizó como parte de un proceso basado en papel. Como parte de un esfuerzo de modernización, quiere utilizar este formulario de PDF para crear automáticamente un nuevo Forms adaptable moderno.

### automated forms conversion - We.Gov (Camila) {#automated-forms-conversion-wegov}

1. Vaya a *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. Inicie sesión con:
   * **Usuario**: camila.santos
   * **Contraseña**: password
1. En la página principal, seleccione Forms > Forms y documentos > AEM Forms We.gov Forms > AFC.
1. Camila carga el PDF en AEM Forms.

   ![Cargar formulario](assets/aftia-upload-form.jpg)

1. A continuación, Camilla selecciona el formulario del PDF y hace clic en **Iniciar conversión automatizada** para iniciar el proceso de conversión. Es posible que tenga que hacer clic en **Sobrescribir conversión** si ha convertido el formulario.

   >[!NOTE]
   >
   >Tenga en cuenta que los ajustes de AFC están preconfigurados para el usuario final, lo que significa que no deben modificarse.

   * **Opcional**: Si desea utilizar el tema Ultramarina accesible, simplemente haga clic en el tema Especificar un formulario adaptable y seleccione el tema Accesible-Ultramarino que aparece en la lista de opciones.

   ![Iniciar conversión](assets/aftia-start-conversion.jpg)

   ![Tema ultramarino](assets/aftia-upload-conversion-settings.jpg)

   El estado de porcentaje completado se muestra durante la conversión. Una vez que se muestra el estado **Convertido**, haga clic en **output** carpeta, seleccione el formulario adaptable y haga clic en **Editar** para abrir el formulario convertido.

1. A continuación, Camilla revisa el formulario y se asegura de que todos los campos estén presentes

   ![Revisar conversión](assets/aftia-review-conversion.jpg)

1. A continuación, Camilla comienza a editar el formulario. Selecciona Panel raíz > Editar (la llave inglesa) > selecciona Pestañas en la parte superior en el menú desplegable Diseño del panel > selecciona la casilla de verificación.

   ![Revisar propiedades](assets/aftia-review-properties.jpg)

1. A continuación, Camilla agrega todas las modificaciones necesarias de CSS y campo para producir el producto final.

   ![Agregar CSS](assets/aftia-add-css.jpg)

### Modelo De Datos De Formulario Y Fuentes De Datos (Camila) {#data-sources}

**Esta sección**: Una vez que el documento se ha convertido y producido un formulario adaptable, Camila debe conectar el formulario adaptable a un origen de datos.

1. Camila abre las Propiedades en el formulario convertido en [automated forms conversion - We.Gov](#automated-forms-conversion-wegov).

1. A continuación, Camila selecciona Modelo de formulario > Selecciona Modelo de datos de formulario en la lista desplegable Seleccionar de > Selecciona FDM de inscripción de We.gov en la lista de opciones.

1. Haga clic en el botón Guardar y cerrar .

   ![Selección de FDM](assets/aftia-select-fdm.jpg)

1. Camila hace clic en **output** , selecciona el formulario adaptable y hace clic en **Editar** para abrir el formulario de We.Gov completado.
1. Camila selecciona un campo de formulario adaptable y hace clic en ![Icono Configurar](assets/configure-icon.svg). Crea enlaces con las entidades del modelo de datos de formulario utilizando la variable **Referencia de enlace** campo . Repite este paso para todos los campos del formulario adaptable.

### Pruebas De Accesibilidad Del Formulario (Camila) {#form-accessibility-testing}

Camila también valida que el contenido creado esté construido de forma correcta y totalmente accesible según los estándares corporativos.

1. Camila hace clic en **output** , selecciona el formulario adaptable y hace clic en **Vista previa** para abrir el formulario de We.Gov completado.

1. Abre la ficha Auditoría en la herramienta para desarrolladores de Chrome.

1. Realiza una comprobación de accesibilidad para validar el formulario adaptable.

   ![Comprobación de accesibilidad](assets/aftia-accessibility.jpg)

## Demostración De Vista Móvil De Formulario Adaptable (Aya) {#mobile-view-demo}

**Esta sección debe realizarse antes de la demostración.**

**Instrucciones del usuario:**

1. Vaya a: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. Inicie sesión con:

   1. **Usuario**: aya.tan
   1. **Contraseña**: password

1. Cambie el tamaño de la ventana del explorador o utilice el emulador del explorador para replicar un tamaño de dispositivo móvil.

### Sitio Web De We.Gov (Aya) {#aya-user-story-we-gov-website}

![Usuario ficticio](/help/forms/using/assets/aya_tan_new-1.png)

**Esta sección**: Aya es ciudadano. Ella escucha de un amigo que puede ser elegible para recibir un Servicio de una agencia gubernamental. Aya navega al sitio web de We.Gov desde su teléfono móvil para obtener más información sobre los servicios para los que es elegible.

### We.Gov Pre-Screener (Aya) {#aya-user-story-we-gov-pre-screener}

Aya responde algunas preguntas para confirmar su elegibilidad rellenando un breve formulario adaptativo en su teléfono móvil.

**Instrucciones del usuario:**

1. Realice una selección en cada campo desplegable.

   >[!NOTE]
   >
   >Si el usuario gana más de 200.000 dólares al año, no es apto.

1. Haga clic en el **¿Soy elegible?**&quot; botón.
1. Haga clic en el **Aplicar ahora**&quot; para continuar.

   ![Aplicar ahora, vínculo](/help/forms/using/assets/apply_now_link.png)

### Formulario Adaptativo We.Gov (Aya) {#aya-user-story-we-gov-adaptive-form}

Aya descubre que es elegible y comienza a llenar su solicitud para solicitar servicio en su dispositivo móvil.

Aya necesita revisar algunos documentos en casa antes de poder completar la solicitud de servicio. Guarda y sale de la aplicación desde su dispositivo móvil.

**Instrucciones del usuario:**

1. Complete los campos Información básica , los siguientes son campos obligatorios y desplegables:

   1. Información básica

      1. Nombre
      1. Apellidos
      1. fecha de nacimiento
      1. Correo electrónico

1. Utilice lo siguiente **lógica dinámica** para demostrar la función dinámica utilizando **Situación familiar** lista desplegable:

   1. **Single**: Mostrar el siguiente panel de kin
   1. **Casado**: Mostrar panel dependiente del matrimonio
   1. **Divorciado**: Mostrar el siguiente panel de kin
   1. **Viudo**: Mostrar el siguiente panel de kin
   1. **¿Tienes hijos?**: (Sí/No) para mostrar el panel dependiente secundario.

      1. (Agregar/quitar) para agregar/quitar varios paneles dependientes secundarios.

1. Haga clic en la flecha derecha de la barra de menús gris.
1. Haga clic en el botón Save en la parte inferior.

   ![Detalles del formulario adaptable](/help/forms/using/assets/adaptive_form.png)

## Demostración del escritorio {#desktop-demo}

**Esta sección:** De vuelta en casa, Aya ha encontrado la información que necesitaba y reanuda la aplicación desde su escritorio. Aya navega al portal de formularios en línea para reanudar su aplicación. Con una simple personalización, las agencias también pueden generar y enviar por correo electrónico automáticamente un vínculo para reanudar la aplicación.

### Formulario Adaptable Continuo (Aya) {#aya-user-story-continued-adaptive-form}

**Instrucciones del usuario:**

1. Vaya a *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. En la barra de navegación, seleccione hacer clic en &quot;**Servicios en línea**&quot;.
1. En el panel &quot;Borrador de Forms&quot;, seleccione la &quot;Solicitud de Inscripción para Beneficios de Salud&quot; existente.

   ![Solicitud de Inscripción en Beneficios de Salud](/help/forms/using/assets/enrollment_application.png)

   El aspecto es el mismo y no necesita volver a introducir ningún dato.

   **Instrucciones del usuario:**

1. Haga clic en CTA del círculo derecho para desplazarse a la siguiente sección.

   ![CTA de círculo derecho](/help/forms/using/assets/right_circle_cta_new.png)

   El formulario se rellena hasta el punto de la última entrada de Aya. Aya ha introducido toda su información y está lista para enviarla.

   ![Enviar el formulario adaptable](/help/forms/using/assets/submit_adaptive_form.png)

   >[!NOTE]
   >
   >Cuando Aya rellena el campo de número de teléfono, debe rellenarlo como un número continuo de 11 dígitos sin guiones, espacios ni guiones.

   Después de enviar Aya recibe una página de agradecimiento. Opcionalmente, también recibirá un correo electrónico que puede abrir para firmar electrónicamente el documento de registro con Adobe Sign.

### Opcional: Adobe Sign (Aya) {#adobe-sign}

**Instrucciones del usuario:**

1. Vaya al cliente de correo electrónico y busque el correo electrónico de Adobe Sign .
1. Haga clic en el vínculo a Adobe Sign.

   ![vínculo de firma de Adobe](/help/forms/using/assets/adobe_sign_link.png)

**Instrucciones del usuario:**

1. Compruebe el **Estoy de acuerdo**&quot;.
1. Haga clic en &quot;**Accept**&quot;.
1. Desplácese hasta la parte inferior del documento revisado.
1. Haga clic en la ficha amarilla resaltada para firmar el documento.

   ![Firmar el documento](/help/forms/using/assets/sign_document_new.png) ![Firmar el documento de prueba](/help/forms/using/assets/sign_test_document.png)

## Agente gubernamental (George) {#government-agent-george}

![Agente gubernamental George](/help/forms/using/assets/george_lang-1.png)

**Esta sección:** George es analista de negocios en la agencia gubernamental Aya es solicitante de un servicio. George tiene un solo tablero donde puede ver todas las solicitudes de servicio que se le han asignado para su revisión.

### Bandeja de entrada AEM (George) {#george-user-story-aem-inbox}

**Instrucciones del usuario:**

1. Vaya a *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Haga clic en el icono de usuario (esquina superior derecha) y utilice el icono &quot;**Cerrar sesión**&quot;, o bien &quot;**Suplantar como**&quot; opción de menú si actualmente ha iniciado sesión con un usuario administrativo.

   1. Inicie sesión con:

      1. **Usuario:** george.lang
      1. **Contraseña:** password
   1. O Suplantar:

      1. Escriba &quot;**George**&quot; en el **Suplantar como**&quot;.

      1. Haga clic en Aceptar para suplantar.


1. En la esquina superior derecha, haga clic en el icono Notification (bell) .
1. Haga clic en &quot;**Ver todo**&quot; para desplazarse a la bandeja de entrada.
1. En la bandeja de entrada, abra la última &quot;**Revisión de la aplicación de beneficios de salud**&quot;.

   ![Revisión de la aplicación de beneficios de salud](/help/forms/using/assets/health_benefits.png)

### Opcional: AEM Inbox &amp; MS Dynamics (George) {#george-user-story-aem-inbox-and-ms-dynamics}

Gracias a las integraciones de datos y a los flujos de trabajo automatizados, aparece la aplicación de Aya junto con un registro CRM que se generó automáticamente cuando se enviaron los datos.

**Instrucciones del usuario:**

1. Abra e inspeccione el formulario adaptable de solo lectura.
1. Haga clic en el &quot;**Abrir MS Dynamics**&quot; para abrir el registro de MS Dynamics en una nueva ventana.
1. En CRM puede ver que toda la información se puede actualizar

   1. Opcionalmente, puede agregar algunas notas de revisión directamente en Dynamics.

1. Cierre y vuelva a AEM Bandeja de entrada.

   ![Registro de MS Dynamics](/help/forms/using/assets/ms_dynamics.png)

### Volver a AEM bandeja de entrada (George) {#george-user-story-back-to-aem-inbox}

George aprueba la aplicación de Aya, y gracias a un flujo de trabajo automatizado existente, también se envía un correo electrónico de confirmación a Aya.

**Instrucciones del usuario:**

1. Vaya a la esquina superior izquierda y haga clic en &quot;**Aprobar**&quot; para aprobar la aplicación.
1. En el modal, puede dejar un mensaje para el posible cliente CX.
1. Haga clic en Finalizado.
1. (Función ciudadana) Abra su cliente de correo electrónico para ver el correo electrónico enviado a Aya.

   ![Ver el correo electrónico enviado a Aya](/help/forms/using/assets/email_client.png)

## Plomo CX (Camila) {#cx-lead-camila}

![Camila (posible cliente CX)](/help/forms/using/assets/camila_santos-1.png)

**Esta sección:** Camila the CX Lead configura una llamada telefónica de bienvenida con Aya para explicar cómo usar los servicios gubernamentales para los que ha sido aprobada.

### (Opcional) AEM Inbox &amp; MS Dynamics {#camila-user-story-aem-inbox-ms-dynamics}

**Instrucciones del usuario:**

1. Vaya a *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Haga clic en el icono de usuario (esquina superior derecha) y utilice el icono &quot;**Cerrar sesión**&quot;, o bien &quot;**Suplantar como**&quot; opción de menú si actualmente ha iniciado sesión con un usuario administrativo.

   1. Inicie sesión con:

      1. **Usuario**: camila.santos
      1. **Contraseña**: password
   1. O Suplantar:

      1. Escriba &quot;**Camila**&quot; en el **Suplantar como**&quot;.

      1. Haga clic en Aceptar para suplantar.


1. En la esquina superior derecha, haga clic en el icono Notification (bell) .
1. Haga clic en &quot;**Ver todo**&quot; para desplazarse a la bandeja de entrada.
1. En la bandeja de entrada, abra la última &quot;**Nueva aprobación de contacto**&quot;.

![Nueva aprobación de contacto](/help/forms/using/assets/new_contact_approval.png)

**(Opcional) Instrucciones del usuario:**

1. Abra e inspeccione el formulario adaptable de solo lectura.
1. Haga clic en el &quot;**Abrir MS Dynamics**&quot; para abrir el registro de MS Dynamics en una nueva ventana.
1. En CRM puede ver que toda la información se puede actualizar

   1. De forma opcional, agregue una nueva actividad de llamada directamente en Dynamics.
   1. Abra el &quot;**Actividades**&quot;.
   1. Haga clic en el &quot;**Nueva llamada telefónica**&quot;.
   1. Agregar detalles de llamadas telefónicas.
   1. Guarde y cierre la ventana.

1. De vuelta en AEM, vaya a la esquina superior izquierda y haga clic en &quot;**Submit**&quot; para enviar la solicitud.
1. En el modal, puede dejar un mensaje.
1. Haga clic en Finalizado.

   ![Pestaña Actividades](/help/forms/using/assets/activities_tab.png) ![Confirmar nuevo contacto](/help/forms/using/assets/confirm_new_contact.png)

## (Opcional) Kit de bienvenida ciudadano (Aya) {#welcome-kit-citizen-aya}

**Esta sección:** Aya recibe un correo electrónico que contiene un enlace a una comunicación interactiva que resume sus ventajas e incluye campos de formulario para rellenar. Con la declaración de beneficios del PDF adjunta y el enlace a la carta de comunicación interactiva en el correo (con el mismo tema/marca que la comunicación interactiva).

### Notificación De Cliente De Correo Electrónico (Aya) {#aya-user-story-email-client}

**Instrucciones del usuario:**

1. Busque y abra el correo electrónico del Kit de bienvenida.
1. Desplácese hasta el archivo adjunto del PDF en la parte inferior de la página.
1. Haga clic en para abrir el archivo adjunto del PDF.
1. Desplácese hacia arriba en su cliente de correo electrónico y haga clic en &quot;**Ver kit de bienvenida en línea**&quot;.

   1. Se abrirá la versión del canal web del mismo documento.

1. Para obtener una referencia rápida al PDF directamente:

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. Para una referencia rápida a IC directamente:

   *https://&lt;aemserver>:&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![Manual de beneficios de bienvenida](/help/forms/using/assets/welcome_benefits_handbook.png) ![Vínculo de comunicación interactiva](/help/forms/using/assets/interactive_communication.png)

## Nuevo Recordatorio Ciudadano (Aya) {#renewal-reminder-citizen-aya}

**Esta sección:** Camila también programa un recordatorio de comunicación un año después. (Paso de flujo de trabajo que automatiza/ejecuta y el correo electrónico).

### Notificación De Cliente De Correo Electrónico (Aya) {#aya-user-story-email-client-updated}

**Instrucciones del usuario:**

1. Vaya a su cliente de correo electrónico.
1. Busque y abra el correo electrónico del recordatorio de renovación .
1. Haga clic en el &quot;**Enviar una nueva aplicación**&quot; para abrir el formulario adaptable.

   1. Esta sección se deja vacía intencionadamente para admitir el rellenado previo de datos en la fase 2.

   ![Correo electrónico del recordatorio de renovación](/help/forms/using/assets/renewal_reminder_email.png)

## (Opcional) Modelo de datos de formulario (Camila) {#form-data-model}

**Esta sección**: Camila se desplaza a Integraciones de datos de AEM Forms, donde puede realizar una prueba rápida para comprobar que la información enviada al origen de datos externo mediante la integración del modelo de datos de formulario está presente.

### Modelo De Datos De Formulario (Camila) {#form-data-model-camila}

**Esta sección**: Camila se desplaza a la página Fuentes de datos para validar los datos que el servidor ha replicado en la base de datos de Derby.

1. Una vez que la experiencia del usuario se haya completado y el envío del usuario se haya completado, Camila accede a la pestaña Fuentes de datos en AEM Forms (**Forms** > **Integraciones de datos**)

1. A continuación, Camila selecciona AEM Forms **FDM de We.gov** y, a continuación, edite el **FDM de inscripción de We.gov**.

1. A continuación, Camila selecciona el **Contacto** > **Leer servicio** que se van a probar.

   ![Servicio de lectura de contacto](assets/aftia-contact-read-service.jpg)

1. A continuación, Camila proporciona al servicio de prueba un id de contacto y, a continuación, hace clic en el botón Test . Por ejemplo, 1 o 2, si envió el formulario. Si no ha enviado el formulario, no se devuelve ningún dato.

   ![Servicio de lectura de contacto](assets/aftia-test-service.jpg)

1. A continuación, Camila puede validar que los datos se hayan insertado correctamente en el origen de datos.

   * Los datos dentro de Derby DS se asemejan al siguiente formato:

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

**Esta sección:** Camila navega a un tablero donde puede ver en los KPI de la agencia como el % de ciudadanos que empiezan a llenar un formulario de solicitud de servicio y abandonan, la cantidad promedio de tiempo desde la presentación de la solicitud hasta la respuesta de aprobación/denegación, y estadísticas de participación para los manuales de beneficios que ha enviado a los ciudadanos.

### Informes De Adobe Analytics Sites (Camila) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. Vaya a *https://&lt;aemserver>:&lt;port>/sites.html/content*
1. Seleccione el **Sitio de AEM Forms We.Gov**&quot; para ver las páginas del sitio.
1. Seleccione una de las páginas del sitio (p. ej. Inicio) y elija &quot;**Analytics y Recommendations**&quot;.

   ![Analytics y recomendaciones](/help/forms/using/assets/analytics_recommendation.jpg)

1. En esta página, verá información recuperada de Adobe Analytics que pertenece a la página de AEM Sites (NOTA: por diseño, esta información se actualiza periódicamente desde Adobe Analytics y no se muestra en tiempo real).

   ![Métricas clave de Adobe Analytics](/help/forms/using/assets/analytics_key_metrics.jpg)

1. De vuelta a la página de vista de página (a la que se accede en el paso 3), también puede ver la información de vista de página cambiando la configuración de visualización para ver los elementos en el **Vista de lista**&quot;.
1. Busque el &quot;**Ver**&quot; menú desplegable y seleccione &quot;**Vista de lista**&quot;.

   ![Vista de lista en el menú desplegable Ver](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. En el mismo menú, seleccione &quot;**Configuración de vista**&quot; y seleccione las columnas que desee mostrar en el **Analytics**&quot;.

   ![Configuración de la visualización de columnas](/help/forms/using/assets/view_setting_analytics.jpg)

1. Haga clic en &quot;**Actualizar**&quot; para que las nuevas columnas estén disponibles.

   ![Hacer que las columnas nuevas estén disponibles](/help/forms/using/assets/new_columns_available.jpg)

### Informes de Adobe Analytics Forms (Camila) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. Vaya a

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. Seleccione el **Solicitud De Inscripción Para Beneficios De Salud**&quot; formulario adaptable y seleccione la **Informe de Analytics**&quot;.

   ![Solicitud de Inscripción en Beneficios de Salud](/help/forms/using/assets/analytics_report_benefits.jpg)

1. Espere a que se cargue la página y vea los datos del informe de Analytics.

   ![Datos de informes de Analytics](/help/forms/using/assets/analytics_report_data_updated.jpg)
