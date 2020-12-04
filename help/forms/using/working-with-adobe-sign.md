---
title: Uso de Adobe Sign en un formulario adaptable
seo-title: Uso de Adobe Sign en un formulario adaptable
description: Habilite flujos de trabajo de firma electrónica (Adobe Sign) para un formulario adaptable a fin de automatizar los flujos de trabajo de firma, simplificar los procesos de firma única y múltiple y firmar electrónicamente formularios desde dispositivos móviles.
seo-description: Habilite flujos de trabajo de firma electrónica (Adobe Sign) para un formulario adaptable a fin de automatizar los flujos de trabajo de firma, simplificar los procesos de firma única y múltiple y firmar electrónicamente formularios desde dispositivos móviles.
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
translation-type: tm+mt
source-git-commit: 4abfda568fc15f225510c79635387142aefddc72
workflow-type: tm+mt
source-wordcount: '3949'
ht-degree: 0%

---


# Uso de Adobe Sign en un formulario adaptable{#using-adobe-sign-in-an-adaptive-form}

Adobe Sign permite flujos de trabajo de firma electrónica para formularios adaptables. Las firmas electrónicas mejoran los flujos de trabajo para procesar documentos para áreas legales, de ventas, de nómina, de gestión de recursos humanos y más.

En un escenario típico de Adobe Sign y formularios adaptables, un usuario rellena un formulario adaptable para aplicar a un servicio. Por ejemplo, una solicitud de hipoteca y tarjeta de crédito requiere firmas legales de todos los prestatarios y cosolicitantes. Para habilitar flujos de trabajo de firma electrónica para situaciones similares, puede integrar Adobe Sign con AEM Forms. Algunos ejemplos más son: puede usar Adobe Sign para:

* Cierre las operaciones desde cualquier dispositivo con procesos de propuesta, presupuesto y contrato completamente automatizados.
* Finalice los procesos de Recursos Humanos más rápido y dé a sus empleados las experiencias digitales.
* Recorte los tiempos del ciclo de contratos y encargue a sus proveedores más rápido.
* Cree flujos de trabajo digitales que automaticen procesos comunes.

La integración de Adobe Sign con AEM Forms es compatible con:

* Flujos de trabajo de firma de un solo usuario y de varios usuarios
* Flujos de trabajo de firma secuenciales y simultáneas
* Experiencias de firma dentro y fuera de formulario
* Firma de formularios como un usuario anónimo o que ha iniciado sesión
* Procesos de firma dinámica (integración con el flujo de trabajo de AEM Forms)
* Autenticación a través de una base de conocimiento, un teléfono y perfiles sociales

## Requisitos previos {#prerequisites}

Antes de usar Adobe Sign en un formulario adaptable:

* Asegúrese de que el servicio en la nube de AEM Forms esté configurado para usar Adobe Sign. Para obtener más información, consulte [Integración de Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).
* Mantenga la lista de firmantes lista. Se requiere al menos una dirección de correo electrónico para cada firmante.

## Configurar Adobe Sign para un formulario adaptable {#configure-adobe-sign-for-an-adaptive-form}

Realice los siguientes pasos para configurar Adobe Sign para un formulario adaptable:

1. [Editar propiedades de formulario adaptable para el signo de Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [Añadir campos de Adobe Sign en un formulario adaptable](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [Habilitar Adobe Sign para un formulario adaptable](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [Seleccionar Cloud Service de Adobe Sign para un formulario adaptable](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [Añadir firmantes de Adobe Sign a un formulario adaptable](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [Seleccionar acción de envío para un formulario adaptable](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![Datos del signatario](assets/signer_details_new.png)

### Editar propiedades de formularios adaptables para Adobe Sign {#enableadobesign}

Configure propiedades de formulario adaptables para Adobe Sign para un formulario adaptable existente o nuevo.

[Crear un formulario adaptable para ](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) señales de Adobe describe los pasos para crear un formulario adaptable básico. Consulte [Creación de un formulario adaptable](../../forms/using/creating-adaptive-form.md) para ver otras opciones disponibles al crear un formulario adaptable.

#### Crear un formulario adaptable para Adobe Sign {#create-an-adaptive-form-for-adobe-sign}

Realice los siguientes pasos para crear un formulario adaptable con firma:

1. Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms y Documentos]**.
1. Toque **[!UICONTROL Crear]** y seleccione **[!UICONTROL Formulario adaptable]**. Aparece una lista de plantillas. Seleccione la plantilla y toque **[!UICONTROL Siguiente]**.
1. En la ficha **[!UICONTROL Basic]**:

   1. Especifique el **Nombre** y **Título** para el formulario adaptable.

   1. Seleccione el [contenedor de configuración](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creado al configurar Adobe Sign con AEM Forms.

      >[!NOTE]
      >
      >La lista desplegable **[!UICONTROL Cloud Service de Adobe Sign]** muestra los servicios en la nube configurados en el contenedor de configuración que seleccione en este campo. La lista desplegable **[!UICONTROL Cloud Service de Adobe Sign]** está disponible en la sección **[!UICONTROL Firma electrónica]** de las propiedades del formulario adaptable al seleccionar la opción **[!UICONTROL Habilitar Adobe Sign]**.

1. En la ficha **[!UICONTROL Modelo de formulario]**, seleccione una de las siguientes opciones:

   * Seleccione la opción **[!UICONTROL Asociar plantilla de formulario como Documento de plantilla de registro]** y seleccione un Documento de plantilla de registro. Si utiliza un formulario adaptable basado en una plantilla de formulario, las documentos enviadas para firmar solo mostrarán los campos basados en la plantilla de formulario asociada. No muestra todos los campos del formulario adaptable.

   * Seleccione la opción **[!UICONTROL Generar Documento de registro]**. Si utiliza una opción Documento de registro activado en un formulario adaptable, el documento enviado para firmar muestra todos los campos del formulario adaptable.

1. Toque **[!UICONTROL Crear.]** Se crea un formulario adaptable con firma, que puede utilizarse para agregar campos de Adobe Sign.

#### Editar un formulario adaptable para Adobe Sign {#editafsign}

Siga estos pasos para utilizar Adobe Sign en un formulario adaptable existente:

1. Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms y Documentos]**.
1. Seleccione el formulario adaptable y toque **[!UICONTROL Propiedades]**.
1. En la ficha **[!UICONTROL Básico]**, seleccione el [contenedor de configuración](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creado al configurar Adobe Sign con AEM Forms.
1. En la ficha **[!UICONTROL Modo de formulario]**, seleccione una de las siguientes opciones:

   * Seleccione la opción **[!UICONTROL Asociar plantilla de formulario como Documento de plantilla de registro]** y seleccione un Documento de plantilla de registro. Si utiliza un formulario adaptable basado en una plantilla de formulario, las documentos enviadas para firmar solo mostrarán los campos basados en la plantilla de formulario asociada. No muestra todos los campos del formulario adaptable.

   * Seleccione la opción **[!UICONTROL Generar Documento de registro]**. Si utiliza una opción Documento de registro activado en un formulario adaptable, el documento enviado para firmar muestra todos los campos del formulario adaptable.

1. Toque **[!UICONTROL Guardar y cerrar]**. El formulario adaptable está habilitado para Adobe Sign.

### Añadir campos de Adobe Sign a un formulario adaptable {#addadobesignfieldstoanadaptiveform}

Adobe Sign tiene varios campos que se pueden colocar en un formulario adaptable. Estos campos aceptan varios tipos de datos, como firmas, iniciales, compañía o título, y ayudan a recopilar información adicional durante la firma, junto con las firmas. Puede utilizar el componente Bloque de Adobe Sign para colocar los campos de Adobe Sign en varias ubicaciones en un formulario adaptable.

Siga estos pasos para agregar campos a un formulario adaptable y personalizar diversas opciones relacionadas con estos campos:

1. Arrastre y suelte el componente **Bloque de Adobe Sign** desde el navegador de componentes al formulario adaptable. El componente Bloque de Adobe Sign tiene todos los campos de Adobe Sign admitidos. De forma predeterminada, agrega un campo **Signature** al formulario adaptable.

   ![Bloque de firma](assets/sign_block_new.png)

   De forma predeterminada, el bloque de Adobe Sign no está visible en el formulario adaptable publicado. Solo está visible en los documentos de firma. Puede cambiar la visibilidad de Adobe Sign Block desde las propiedades del componente Adobe Sign Block.

   >[!NOTE]
   >
   >    * El uso del bloque Adobe Sign no es obligatorio para utilizar Adobe Sign en un formulario adaptable. Si no utiliza el bloque Adobe Sign y agrega campos para los firmantes, el campo de firma predeterminado se muestra en la parte inferior de los documentos de firma.
   >    * Utilice el bloque Adobe Sign solo para aquellos formularios adaptables que generen automáticamente Documento de registro. Si utiliza un XDP personalizado para generar Documentos de registro o un formulario adaptable basado en plantillas de formulario, no es necesario el bloque Adobe Sign.


1. Seleccione el componente **Bloque de Adobe Sign** y toque el icono **Editar** ![aem_6_3_edit](assets/aem_6_3_edit.png). Muestra opciones para agregar campos y dar formato al aspecto de un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **R.** Seleccione y agregue campos de Adobe Sign. **B.** Expanda el bloque Adobe Sign a la vista de pantalla completa

1. Toque el icono **Campo de Adobe Sign** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png). Muestra las opciones para seleccionar y agregar campos de Adobe Sign.

   Expanda el campo desplegable **Tipo** para seleccionar un campo de Adobe Sign y toque el icono Listo ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para agregar el campo seleccionado al bloque de Adobe Sign. El campo desplegable **Tipo** incluye los tipos de campo Firma, Información del firmante y Datos. La integración de Adobe Sign con AEM Forms solo aparece en el cuadro desplegable Tipo. Para obtener información detallada sobre los campos de Adobe Sign, consulte [Documentación de Adobe Sign](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   Es obligatorio proporcionar un nombre único para un campo. También puede seleccionar la opción necesaria para marcar un campo como obligatorio. Además de la opción **Nombre** y **Requerido**, algunos campos de Adobe Sign tienen más opciones. Por ejemplo, máscara y líneas múltiples. Además, especifique un nombre único para cada campo de Adobe Sign, ya sea que los campos residan en bloques de Adobe Sign iguales o diferentes.

   Si selecciona **Firma digital** en la lista desplegable, puede aplicar firmas digitales al formulario adaptable:

   * En línea, se utilizan firmas en la nube para firmar con un [ID digital](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) alojado por un proveedor de servicio de confianza.
   * Localmente, descargando el documento con Adobe Acrobat o Reader mediante una tarjeta inteligente, un token USB o un ID digital basado en archivos.

### Habilitar Adobe Sign para un formulario adaptable {#enableadobsignforanadaptiveform}

De forma predeterminada, Adobe Sign no está habilitado para un formulario adaptable. Realice los siguientes pasos para habilitarlo:

1. En el navegador de contenido, toque **Contenedor de formulario** y el icono **Configurar** ![configurar](assets/configure.png). Abre el navegador de propiedades y muestra las propiedades del contenedor de formulario adaptable.
1. En el navegador de propiedades, expanda el acordeón **Firma electrónica** y seleccione la opción **Habilitar Adobe Sign**. Habilita Adobe Sign para un formulario adaptable.

### Seleccione el Cloud Service de Adobe Sign y el orden de firma {#selectadobesigncloudserviceforanadaptiveform}

Puede configurar varios servicios de Adobe Sign para una instancia de AEM Forms. Es aconsejable contar con un conjunto de servicios separados para cada función (Recursos Humanos, Finanzas, etc.). Facilita el seguimiento y el sistema de informes de documentos firmados. Por ejemplo, un banco tiene múltiples departamentos. Puede tener una configuración separada para cada departamento para un mejor seguimiento de los documentos.

Un documento también puede tener varios firmantes. Por ejemplo, una solicitud de tarjeta de crédito puede tener varios solicitantes. Un banco requiere la firma de todos los solicitantes antes de iniciar la solicitud de procesamiento. En los escenarios con varios firmantes, puede seleccionar firmar el documento en orden secuencial o simultáneo.

Realice los siguientes pasos para seleccionar un servicio en la nube y el orden de firma:

![cloud-service](assets/cloud-service.png)

1. En el navegador de contenido, toque **Contenedor de formulario** y el icono **Configurar** ![configurar](assets/configure.png). Abre el navegador de propiedades y muestra las propiedades del contenedor de formulario adaptable.
1. En el navegador de propiedades, expanda el acordeón **Firma electrónica** y seleccione la opción **Habilitar Adobe Sign**. Habilita Adobe Sign para un formulario adaptable.
1. Seleccione un servicio en la nube de la lista ya configurada de Cloud Services de Adobe Sign.

   Si la lista **Adobe Sign Cloud Service** está vacía, siga el artículo [Configurar Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) para configurar el servicio.

   La lista desplegable lista los servicios en la nube que existen en la carpeta `global` en Herramientas > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Además, el menú desplegable también lista los servicios en la nube que existen en la carpeta seleccionada en el campo **[!UICONTROL Contenedor de configuración]** al crear un formulario adaptable.

1. Seleccione el orden de firma en el cuadro de diálogo **Los firmantes pueden firmar**. Los cantantes de Adobe Sign pueden firmar un formulario adaptable **Secuencialmente** - uno tras otro firmante o **Simultáneamente** - en cualquier orden.

   En orden secuencial, un firmante recibe el formulario para firmar por vez. Una vez que un firmante completa la firma del documento, el formulario se envía al siguiente firmante, etc.

   En orden simultáneo, varios firmantes pueden firmar un formulario a la vez.

1. [Añada Firmantes en un ](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) formulario adaptable y toque el icono  [Listo_6_3_forms_](assets/aem_6_3_forms_save.png) saveicon para guardar los cambios.


### Añadir firmantes a un formulario adaptable {#addsignerstoanadaptiveform}

Solo puede tener un firmante o varios para un formulario adaptable. Al agregar un firmante, también puede configurar los detalles de autenticación para el firmante. También puede seleccionar si la persona que rellena el formulario y la cantante son la misma. Realice los siguientes pasos para agregar y proporcionar varios detalles sobre un firmante:

1. En el navegador de contenido, toque **Contenedor de formulario** y el icono **Configurar** ![configurar](assets/configure.png). Abre el navegador de propiedades con propiedades de contenedor de formulario adaptable.
1. En el navegador de propiedades, expanda el acordeón **Firma electrónica** y seleccione la opción **Habilitar Adobe Sign**. Habilita Adobe Sign para un formulario adaptable.
1. Toque **Añadir firmante** en **Configuración del firmante**. Agrega un firmante al formulario adaptable. Puede agregar varios firmantes de Adobe Sign a un formulario adaptable.
1. ![detalles de teléfono](assets/phone-details.png)

   Haga clic en el icono **Editar** ![aem_6_3_edit](assets/aem_6_3_edit.png) para especificar la siguiente información sobre el firmante:

   * **Título:** especifique un título para identificar exclusivamente a un firmante.

   * **¿Son iguales el firmante y la persona que rellena el formulario?:** Seleccione  **Sí**, si el usuario que rellena el formulario y el primer firmante son la misma persona. Si la opción está establecida en **No,** no utilice el componente de paso de firma en el formulario adaptable. Si el formulario contiene un componente Paso de firma, el campo se establece automáticamente en Sí.

   * **Dirección de correo electrónico del firmante:** especifique la dirección de correo electrónico del firmante. El firmante recibe documentos/formulario firmados en la dirección de correo electrónico especificada. Puede elegir utilizar una dirección de correo electrónico proporcionada en un campo de formulario, en AEM perfil de usuario del usuario que ha iniciado sesión o introducir manualmente una dirección de correo electrónico. Es un paso obligatorio. Asegúrese de que la dirección de correo electrónico del primer firmante o del único firmante (en el caso de un solo firmante) no es idéntica a la cuenta de Adobe Sign utilizada para configurar los servicios de nube de AEM.

   * **Método de autenticación del firmante:** especifique el método para autenticar a un usuario antes de abrir un formulario para firmar. Puede elegir entre teléfono, base de conocimientos y autenticación social basada en la identidad.
   >[!NOTE]
   >
   >    * De forma predeterminada, la autenticación social basada en la identidad proporciona una opción para autenticarse con Facebook, Google y LinkedIn. Puede ponerse en contacto con la asistencia de Adobe Sign para habilitar otros proveedores de autenticación social.


   * **Campos de Adobe Sign para rellenar o firmar:** seleccione los campos de Adobe Sign para el firmante. Un formulario adaptable puede tener varios campos de Adobe Sign. Puede elegir habilitar campos específicos para un firmante. El campo muestra todos los bloques de Adobe Sign disponibles. Cuando se selecciona un bloque, se seleccionan todos los campos del bloque. Puede utilizar el icono X para anular la selección de un campo.

   ![signer-details](assets/signer-details.png)

   La imagen anterior tiene dos ejemplos de Bloques de Adobe Sign: Información personal y detalles de Office

   Toque el icono Listo ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). Se agrega y configura el firmante.

### Seleccione Enviar acción para un formulario adaptable {#selectsubmitactionforanadaptiveform}

Después de agregar campos de Adobe Sign a un formulario adaptable, activar Adobe Sign desde el contenedor del formulario, seleccionar Cloud Service de Adobe Sign y agregar firmantes de Adobe Sign, seleccionar una acción de envío adecuada para el formulario adaptable. Para obtener información detallada sobre las acciones de envío de formularios adaptables, consulte [Configuración de la acción Enviar](../../forms/using/configuring-submit-actions.md).

Además, un formulario adaptable habilitado para Adobe Sign se envía solamente después de que todos los firmantes firmen el formulario. Puede encontrar un formulario parcialmente firmado en la sección Firma pendiente del portal de formularios. El servicio de configuración de Adobe Sign sigue sondeando el servidor de Adobe Sign a [intervalos regulares](../../forms/using/adobe-sign-integration-adaptive-forms.md) para verificar el estado de las firmas. Si todos los firmantes completan la firma del formulario, se inicia el servicio de acción de envío y se envía el formulario. Si está utilizando una acción de envío personalizada y el formulario utiliza Adobe Sign, actualice la acción de envío personalizada para utilizar el servicio de acción de envío.

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

La experiencia de firma de formularios está lista. Puede previsualización del formulario para comprobar la experiencia de firma. En el formulario publicado, los campos Bloque de Adobe Sign se muestran cuando un firmante recibe el formulario para firmar por correo electrónico. Esta experiencia también se conoce como experiencia de firma fuera de formulario. También puede configurar una experiencia de firma en el formulario para el primer firmante; para obtener más información, consulte [Creación de una experiencia de firma en el formulario](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience).

## Configurar firmas de nube para un formulario adaptable {#configure-cloud-signatures-for-an-adaptive-form}

Las firmas digitales basadas en la nube o las firmas remotas son una nueva generación de firmas digitales que funcionan en el escritorio, los dispositivos móviles y la web: y cumplir los niveles más altos de cumplimiento y seguridad para la autenticación de firmantes. Puede firmar un formulario adaptable con firmas digitales basadas en la nube.

Después de [editar las propiedades del formulario adaptable para el signo de Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign), lleve a cabo los siguientes pasos para agregar el campo de firma en la nube a un formulario adaptable:

1. Arrastre y suelte el componente **Bloque de Adobe Sign** desde el navegador de componentes al formulario adaptable. El componente Bloque de Adobe Sign tiene todos los campos de Adobe Sign admitidos. De forma predeterminada, agrega un campo **Signature** al formulario adaptable.

   ![Bloque de firma](assets/sign-block-new.png)

1. Seleccione el componente **Bloque de Adobe Sign** y toque el icono **Editar** ![aem_6_3_edit](assets/aem_6_3_edit.png). Muestra opciones para agregar campos y dar formato al aspecto de un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **R.** Seleccione y agregue campos de Adobe Sign. **B.** Expanda el bloque Adobe Sign a la vista de pantalla completa

1. Toque el icono **Campo de Adobe Sign** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png). Muestra las opciones para seleccionar y agregar campos de Adobe Sign.

   Expanda el campo desplegable **Tipo** para seleccionar **Firma digital** y toque el icono Listo para agregar el campo seleccionado al bloque Adobe Sign.

   ![Firmas digitales](assets/digital_signatures_new.png)

   Es obligatorio proporcionar un nombre único para un campo.

   Aplicar firmas digitales al formulario adaptable mediante:

   * Firmas de nube: Firme con un [ID digital](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) alojado por un proveedor de servicio de confianza.
   * Adobe Acrobat o Reader: Descargue y abra el documento con Adobe Acrobat o Reader para firmar con una tarjeta inteligente, un token USB o un ID digital basado en archivos.

   Después de agregar el campo de firma en la nube al formulario adaptable, realice los siguientes pasos para completar el proceso de configuración:

   * [Habilitar Adobe Sign para un formulario adaptable](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [Seleccionar Cloud Service de Adobe Sign para un formulario adaptable](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [Añadir firmantes de Adobe Sign a un formulario adaptable](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [Seleccionar acción de envío para un formulario adaptable](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## Crear experiencia de firma en el formulario {#create-in-form-signing-experience}

Un usuario también puede firmar un formulario adaptable mientras lo rellena. Esta experiencia también se conoce como experiencia de firma en el formulario. La experiencia de firma en el formulario solo está disponible para el primer cantante en un entorno de varios firmantes. Realice los siguientes pasos para crear una experiencia de firma en formularios para un formulario adaptable:

1. [Añada y configure el componente](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component) Paso de firma.
1. [Añada el componente](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component) Paso de resumen.

![Experiencia de firma en el formulario](assets/in_form_signing_experience_new.png)

### Añadir y configurar el componente Paso de firma {#add-and-configure-the-signature-step-component}

Utilice el componente Paso de firma para proporcionar un área donde firmar electrónicamente el formulario rellenado. Cuando se representa la sección que contiene el componente Paso de firma, muestra una versión en PDF que se puede firmar del formulario rellenado. El componente Paso de firma ocupa toda la anchura disponible para el formulario. Se recomienda no tener ningún otro componente en la sección que contenga el componente Paso de firma.

Realice los siguientes pasos para configurar el componente Paso de firma:

1. Arrastre y suelte el componente **Paso de firma** desde el navegador de componentes al formulario.
1. Seleccione el componente de paso Firma recién agregado y toque el icono **Configurar** ![configurar](assets/configure.png). Abre el navegador de propiedades y muestra las propiedades del paso Firma. Configure las siguientes propiedades:

   * **Nombre** del elemento: Especifique el nombre del componente.

   * **Título:** especifique el título exclusivo del componente.
   * **Mensaje de plantilla:** especifique el mensaje que se mostrará mientras se carga el PDF de firma. Los servicios de Adobe Sign tardan algún tiempo en preparar y cargar archivos PDF de firma.
   * **Servicio de firma:** seleccione la opción  **Adobe** Signoption.

   * **Usar componente** de firma electrónica heredado: Si está utilizando el formulario adaptable correspondiente en  [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md), la aplicación de AEM Forms o el formulario adaptable subyacente tiene un componente de firma electrónica heredado, seleccione la opción  **Usar** componente de firma electrónica heredado.

   * **Configuración**: Seleccione una configuración (Cloud Service de Adobe Sign). El cuadro desplegable solo está disponible si la opción **Usar componente de firma electrónica heredado** está habilitada.

   Toque el icono Listo ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para guardar los cambios.

   ![Paso de firma](assets/signature_step_new.png)

   >[!NOTE]
   >
   > * Cuando arrastra y suelta el componente **[!UICONTROL Paso de firma]** en el formulario, el **[!UICONTROL ¿Son iguales el firmante y la persona que rellena el formulario?]** se establece automáticamente en  **Sí**. Es necesario mantener el formulario en funcionamiento.
      >
      > 
   * Utilice el componente Paso de resumen después del paso de firma para disfrutar de una experiencia óptima. El paso Resumen envía el formulario automáticamente e inmediatamente después de haber completado la firma de un formulario en el componente Paso de firma. Si no utiliza el paso de resumen, un envío automático se activa solamente después del intervalo establecido mediante el [servicio de configuración de Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status).
   > * Algunas prácticas recomendadas son:
   > * El panel Formulario adaptable que contiene el paso Firma siempre se encuentra en el último o segundo panel de un formulario adaptable. Puede ser el segundo último panel solo cuando el último panel contiene el paso Resumen.
   > * El panel que contiene el componente de paso Firma o Resumen no puede contener ningún otro componente.
   > * Los formularios adaptables que contengan Paso de firma no pueden tener botón de envío. El envío se realiza mediante un servicio en segundo plano o el paso Resumen.
   > * Diseñe el formulario para que un usuario no pueda desplazarse hacia atrás desde un panel que contenga el paso Firma o Resumen.



### Configurar la página de agradecimiento o el componente de paso de resumen {#configure-the-thank-you-page-or-summary-step-component}

El componente **Paso de resumen** envía automáticamente el formulario, rellena la información dentro de la página de resumen personalizada y muestra el resumen del formulario enviado. También obtiene la información requerida en el mapa de retorno. El componente Paso de resumen ocupa toda la anchura disponible para el formulario. Se recomienda no tener ningún otro componente en la sección que contenga el componente Paso de resumen.

Ahora, la experiencia de firma de formularios en curso está lista. Puede previsualización del formulario para comprobar la experiencia de firma.

## Preguntas frecuentes {#frequently-asked-questions}

**P:** Puede incrustar un formulario adaptable en otro formulario adaptable. ¿Se puede habilitar Adobe Sign en el formulario adaptable incrustado?
**Ans:** No, AEM Forms no admite el uso de un formulario adaptable que incruste un formulario adaptable Adobe Sign habilitado para firmar

**P:** Cuando se crea un formulario adaptable con la plantilla avanzada y se abre para su edición, aparece un mensaje de error &quot;Firma electrónica o Firmantes no están configurados correctamente&quot;. aparece. ¿Cómo resolver el mensaje de error?
**Ans:El formulario** adaptable creado con la plantilla avanzada está configurado para utilizar Adobe Sign. Para resolver el error, cree y seleccione una configuración de nube de Adobe Sign y configure un firmante de Adobe Sign para el formulario adaptable.

**P:** ¿Puedo utilizar etiquetas de texto de Adobe Sign en un componente de texto estático de un formulario adaptable?
**Ans:** Sí, se pueden utilizar etiquetas de texto en un componente de texto para agregar campos de Adobe Sign a un  [Documento de registro](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)  (solo opción de documento de registro generado automáticamente) de un formulario adaptable habilitado. Para obtener más información sobre el procedimiento y las reglas para crear una etiqueta de texto, consulte [Documentación de Adobe Sign](https://helpx.adobe.com/sign/using/text-tag.html). Además, los formularios adaptables tienen una compatibilidad limitada con las etiquetas de texto. Puede utilizar las etiquetas de texto para crear solo los campos que admite [Bloque de Adobe Sign](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form).

**P:** AEM Forms proporciona componentes de paso Bloque Adobe Sign y Firma. ¿Pueden utilizarse simultáneamente en forma adaptable?
**Ans:** puede utilizar ambos componentes simultáneamente en un formulario. Estas son algunas recomendaciones para usar estos componentes:

**Bloque de Adobe Sign:** puede usar el Bloque de Adobe Sign para agregar campos de Adobe Sign en cualquier parte del formulario adaptable. También ayuda a asignar campos específicos a los firmantes. De forma predeterminada, cuando se realiza una vista previa de un formulario adaptable o se publica un bloque de Adobe Sign no está visible. Estos bloques solo se activan en el documento de firma. En el documento de firma, solo se activan los campos asignados a un firmante. El bloque Adobe Sign se puede utilizar con los firmantes primero y posteriores.

**Componente de paso de firma:** puede utilizar el componente de paso de firma para crear una experiencia de firma en el formulario. Solo permite que el primer firmante firme mientras se rellena el formulario. Cuando se representa la sección que contiene el componente Paso de firma, muestra una versión en PDF del formulario que se puede firmar. Generalmente es la última o penúltima sección seguida de un componente de resumen de un formulario.

## Solución de problemas {#troubleshoot}

### Fallos del acuerdo de Adobe Sign {#adobe-sign-agreement-failures}

****
ProblemaCuando el servicio de Adobe Sign está configurado para un formulario adaptable, el servicio no puede crear un acuerdo de Adobe Sign para el formulario adaptable subyacente.

**Resolución**

* Compruebe la configuración [del servicio en la nube de Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md) utilizada en el formulario adaptable.
* Asegúrese de que la aplicación API del servidor de Adobe Sign utilizada para configurar el servicio de Adobe Sign Cloud tiene los permisos necesarios.
* Si utiliza varios servicios de Adobe Sign Cloud, señale la **[!UICONTROL URL de autenticación]** de todos los servicios a la misma **[!UICONTROL Adobe Sign Share]**.

* Utilice direcciones de correo electrónico independientes para configurar la cuenta de Adobe Sign y para el primer firmante y el primer firmante. La dirección de correo electrónico del primer firmante o del único firmante (en el caso del firmante único) no puede ser idéntica a la cuenta de Adobe Sign utilizada para configurar los servicios de nube de AEM.

### El flujo de trabajo de AEM Forms configurado para un formulario adaptable habilitado para Adobe Sign no inicio {#adobe-sign-aem-form-workflow-failures}

****
ProblemaCuando Adobe Sign está configurado para un formulario adaptable, el flujo de trabajo configurado con la opción Invocar Forms Workflow no tiene inicios.

**Resolución**

* Cuando se utiliza Adobe Sign sin el paso Firma o el formulario requiere firmas de varias personas, el servidor de AEM Forms espera a que el Planificador confirme que todas las personas han firmado el formulario. El Planificador envía el formulario adaptable solo después de que toda la persona complete los inicios de firma y flujo de trabajo después de enviar correctamente el formulario adaptable. Puede acortar el intervalo del [Planificador](adobe-sign-integration-adaptive-forms.md) para comprobar el estado de la firma del formulario a intervalos rápidos y acelerar el envío del formulario.


## Artículos relacionados {#related-articles}

* [Integrar Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [Uso de Adobe Sign en un formulario adaptable](../../forms/using/working-with-adobe-sign.md)
* [Uso de Adobe Sign con AEM Forms (vídeo)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
