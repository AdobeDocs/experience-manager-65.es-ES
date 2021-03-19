---
title: Uso de Adobe Sign en un formulario adaptable
seo-title: Uso de Adobe Sign en un formulario adaptable
description: Habilite los flujos de trabajo de firma electrónica (Adobe Sign) para un formulario adaptable a fin de automatizar los flujos de trabajo de firma, simplificar los procesos de firma única y múltiple y firmar electrónicamente formularios desde dispositivos móviles.
seo-description: Habilite los flujos de trabajo de firma electrónica (Adobe Sign) para un formulario adaptable a fin de automatizar los flujos de trabajo de firma, simplificar los procesos de firma única y múltiple y firmar electrónicamente formularios desde dispositivos móviles.
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
feature: Forms adaptable, Adobe Sign
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '3863'
ht-degree: 0%

---


# Uso de [!DNL Adobe Sign] en un formulario adaptable{#using-adobe-sign-in-an-adaptive-form}

[!DNL Adobe Sign] activa los flujos de trabajo de firma electrónica para formularios adaptables. Las firmas electrónicas mejoran los flujos de trabajo para procesar documentos para áreas legales, de ventas, de nómina, de gestión de recursos humanos y más.

En un escenario típico de [!DNL Adobe Sign] y formularios adaptables, un usuario rellena un formulario adaptable para solicitar un servicio. Por ejemplo, una solicitud de hipoteca y tarjeta de crédito requiere firmas legales de todos los prestatarios y cosolicitantes. Para habilitar los flujos de trabajo de firma electrónica para escenarios similares, puede integrar [!DNL Adobe Sign] con AEM [!DNL Forms]. Algunos ejemplos más son: puede utilizar [!DNL Adobe Sign] para:

* Cierre las ofertas de cualquier dispositivo con procesos de propuesta, presupuesto y contrato totalmente automatizados.
* Finalice los procesos de Recursos Humanos más rápido y ofrezca a sus empleados las experiencias digitales.
* Reduzca los tiempos de ciclo de contrato e incorpore a sus proveedores más rápido.
* Cree flujos de trabajo digitales que automaticen procesos comunes.

[!DNL Adobe Sign] integración con AEM  [!DNL Forms] admite:

* Flujos de trabajo de firma de usuarios únicos y múltiples
* Flujos de trabajo de firma secuenciales y simultáneos
* Experiencias de firma dentro y fuera de formulario
* Firma de formularios como usuario anónimo o con sesión iniciada
* Procesos de firma dinámica (integración con AEM flujo de trabajo [!DNL Forms])
* Autenticación a través de una base de conocimiento, un teléfono y perfiles sociales

Conozca las [prácticas recomendadas de usar Adobe Sign con formularios adaptables](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684) para crear mejores experiencias de firma.

## Requisitos previos {#prerequisites}

Antes de utilizar [!DNL Adobe Sign] en un formulario adaptable:

* Asegúrese de que AEM [!DNL Forms] servicio en la nube está configurado para utilizar [!DNL Adobe Sign]. Para obtener más información, consulte [Integración de Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).
* Mantenga lista de firmantes lista. Se requiere al menos una dirección de correo electrónico para cada firmante.

## Configurar [!DNL Adobe Sign] para un formulario adaptable {#configure-adobe-sign-for-an-adaptive-form}

Realice los siguientes pasos para configurar [!DNL Adobe Sign] para un formulario adaptable:

1. [Edición de las propiedades de formulario adaptables para el signo de Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [Adición de campos de Adobe Sign a un formulario adaptable](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [Habilitar Adobe Sign para un formulario adaptable](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [Seleccione el Cloud Service de Adobe Sign para un formulario adaptable](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [Agregar firmantes de Adobe Sign a un formulario adaptable](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [Seleccione Enviar acción para un formulario adaptable](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![Datos del signatario](assets/signer_details_new.png)

### Editar propiedades de formulario adaptables para [!DNL Adobe Sign] {#enableadobesign}

Configure las propiedades de formulario adaptables para [!DNL Adobe Sign] para un formulario adaptable existente o nuevo.

[Crear un formulario adaptable para ](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) señales de Adobe describe los pasos para crear un formulario adaptable básico. Consulte [Creación de un formulario adaptable](../../forms/using/creating-adaptive-form.md) para conocer otras opciones disponibles al crear un formulario adaptable.

#### Crear un formulario adaptable para [!DNL Adobe Sign] {#create-an-adaptive-form-for-adobe-sign}

Siga estos pasos para crear un formulario adaptable con firma habilitada:

1. Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Pulse **[!UICONTROL Crear]** y seleccione **[!UICONTROL Formulario adaptable]**. Aparecerá una lista de plantillas. Seleccione la plantilla y pulse **[!UICONTROL Siguiente]**.
1. En la pestaña **[!UICONTROL Basic]**:

   1. Especifique el **[!UICONTROL Nombre]** y el **[!UICONTROL Título]** para el formulario adaptable.

   1. Seleccione el [contenedor de configuración](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creado al configurar [!DNL Adobe Sign] con AEM [!DNL Forms].

      >[!NOTE]
      >
      >La lista desplegable **[!UICONTROL Adobe Sign Cloud Service]** muestra los servicios de nube que se configuran en el contenedor de configuración que seleccione en este campo. La lista desplegable **[!UICONTROL Cloud Service de Adobe Sign]** está disponible en la sección **[!UICONTROL Firma electrónica]** de las propiedades del formulario adaptable cuando selecciona la opción **[!UICONTROL Habilitar Adobe Sign]**.

1. En la ficha **[!UICONTROL Modelo de formulario]**, seleccione una de las siguientes opciones:

   * Seleccione la opción **[!UICONTROL Associate form template como Document of Record template]** y seleccione una plantilla Document of Record . Si utiliza un formulario adaptable basado en una plantilla de formulario, los documentos enviados para firmar sólo mostrarán aquellos campos basados en la plantilla de formulario asociada. No muestra todos los campos del formulario adaptable.

   * Seleccione la opción **[!UICONTROL Generate Document of Record]**. Si utiliza la opción Documento de registro habilitado para el formulario adaptable, el documento enviado para firmar muestra todos los campos del formulario adaptable.

1. Toque **[!UICONTROL Crear.]** Se crea un formulario adaptable con firma habilitada, que se puede utilizar para agregar  [!DNL Adobe Sign] campos.

#### Editar un formulario adaptable para [!DNL Adobe Sign] {#editafsign}

Realice los siguientes pasos para utilizar [!DNL Adobe Sign] en un formulario adaptable existente:

1. Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Seleccione el formulario adaptable y pulse **[!UICONTROL Properties]**.
1. En la pestaña **[!UICONTROL Basic]**, seleccione el [contenedor de configuración](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creado al configurar [!DNL Adobe Sign] con AEM [!DNL Forms].
1. En la ficha **[!UICONTROL Modelo de formulario]**, seleccione una de las siguientes opciones:

   * Seleccione la opción **[!UICONTROL Associate form template como Document of Record template]** y seleccione una plantilla Document of Record . Si utiliza un formulario adaptable basado en una plantilla de formulario, los documentos enviados para firmar sólo mostrarán aquellos campos basados en la plantilla de formulario asociada. No muestra todos los campos del formulario adaptable.

   * Seleccione la opción **[!UICONTROL Generate Document of Record]**. Si utiliza la opción Documento de registro habilitado para el formulario adaptable, el documento enviado para firmar muestra todos los campos del formulario adaptable.

1. Toque **[!UICONTROL Guardar y cerrar]**. El formulario adaptable está habilitado para [!DNL Adobe Sign].

### Agregar campos de Adobe Sign a un formulario adaptable {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] tiene varios campos que se pueden colocar en un formulario adaptable. Estos campos aceptan varios tipos de datos, como firmas, iniciales, empresa o título, y ayudan a recopilar información adicional durante la firma, junto con las firmas. Puede utilizar el componente Bloque [!DNL Adobe Sign] para colocar los campos [!DNL Adobe Sign] en varias ubicaciones en un formulario adaptable.

Siga estos pasos para agregar campos a un formulario adaptable y personalizar diversas opciones relacionadas con estos campos:

1. Arrastre y suelte el componente **[!UICONTROL Bloque de Adobe Sign]** desde el navegador de componentes al formulario adaptable. El componente Bloque [!DNL Adobe Sign] tiene todos los campos [!DNL Adobe Sign] admitidos. De forma predeterminada, agrega un campo **Signature** al formulario adaptable.

   ![Bloque de firma](assets/sign_block_new.png)

   De forma predeterminada, el bloque [!DNL Adobe Sign] no está visible en el formulario adaptable publicado. Solo está visible en los documentos de firma. Puede cambiar la visibilidad del [!DNL Adobe Sign] Bloque desde las propiedades del componente Bloque [!DNL Adobe Sign].

   >[!NOTE]
   >
   >    * El uso del bloque [!DNL Adobe Sign] no es obligatorio para utilizar [!DNL Adobe Sign] en un formulario adaptable. Si no utiliza el bloque [!DNL Adobe Sign] y agrega campos para los firmantes, el campo de firma predeterminado se muestra en la parte inferior de los documentos de firma.
   >    * Utilice el bloque [!DNL Adobe Sign] solo para los formularios adaptables que generan automáticamente el documento de registro. Si utiliza un XDP personalizado para generar un documento de registro o un formulario adaptable basado en una plantilla de formulario, no se admite el bloque [!DNL Adobe Sign].


1. Seleccione el componente **[!UICONTROL Adobe Sign Block]** y pulse el icono **Edit** ![aem_6_3_edit](assets/aem_6_3_edit.png). Muestra las opciones para añadir campos y dar formato al aspecto de un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Seleccione y añada  [!DNL Adobe Sign] campos. **B.** Expanda el  [!DNL Adobe Sign] bloque a la vista de pantalla completa

1. Pulse el icono **[!UICONTROL Adobe Sign] Field** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png). Muestra las opciones para seleccionar y agregar campos [!DNL Adobe Sign].

   Expanda el campo desplegable **[!UICONTROL Type]** para seleccionar un campo [!DNL Adobe Sign] y pulse el icono Listo ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para agregar el campo seleccionado al bloque [!DNL Adobe Sign]. El campo desplegable **[!UICONTROL Type]** incluye los tipos de campo Firma, Información del firmante y Datos. [!DNL Adobe Sign] integración con AEM campos de  [!DNL Forms] compatibilidad enumerados solo en el cuadro   desplegable Tipo . Para obtener información detallada sobre los campos [!DNL Adobe Sign], consulte [Documentación de Adobe Sign](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   Es obligatorio proporcionar un nombre único para un campo. También puede seleccionar la opción necesaria para marcar un campo como obligatorio. Además de las opciones **[!UICONTROL Name]** y **[!UICONTROL Required]**, algunos campos [!DNL Adobe Sign] tienen más opciones. Por ejemplo, máscara y líneas múltiples. Además, especifique un nombre único para cada campo [!DNL Adobe Sign] si los campos residen en bloques iguales o diferentes [!DNL Adobe Sign].

   Si selecciona **[!UICONTROL Firma digital]** en la lista desplegable, puede aplicar firmas digitales al formulario adaptable:

   * En línea, usar firmas de la nube para firmar con un [ID digital](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) alojado por un proveedor de servicios de confianza.
   * Localmente descargando el documento con Adobe Acrobat o Reader usando una tarjeta inteligente, un token USB o un ID digital basado en archivos.

### Habilitar [!DNL Adobe Sign] para un formulario adaptable {#enableadobsignforanadaptiveform}

De serie, [!DNL Adobe Sign] no está habilitado para un formulario adaptable. Siga estos pasos para habilitarlo:

1. En el navegador de contenido, pulse **[!UICONTROL Contenedor de formulario]** y pulse el icono **[!UICONTROL Configurar]** ![configurar](assets/configure.png). Abre el explorador de propiedades y muestra las propiedades del contenedor de formularios adaptables.
1. En el navegador de propiedades, expanda el acordeón **[!UICONTROL Electronic Signature]** y seleccione la opción **[!UICONTROL Enable Adobe Sign]**. Habilita [!DNL Adobe Sign] para un formulario adaptable.

### Seleccione [!DNL Adobe Sign] Cloud Service y orden de firma {#selectadobesigncloudserviceforanadaptiveform}

Puede configurar varios servicios [!DNL Adobe Sign] para una instancia de AEM [!DNL Forms]. Es aconsejable tener un conjunto de servicios separados para cada función (Recursos Humanos, Finanzas, etc.). Facilita el seguimiento y la creación de informes de documentos firmados. Por ejemplo, un banco tiene varios departamentos. Puede tener una configuración separada para cada departamento para un mejor seguimiento de los documentos.

Un documento también puede tener varios firmantes. Por ejemplo, una solicitud de tarjeta de crédito puede tener varios solicitantes. Un banco requiere firmas de todos los solicitantes antes de iniciar la solicitud de procesamiento. En el caso de los casos de multifirmante, puede seleccionar firmar el documento en orden secuencial o simultáneo.

Siga estos pasos para seleccionar un servicio en la nube y el orden de firma:

![cloud-service](assets/cloud-service.png)

1. En el navegador de contenido, pulse **[!UICONTROL Contenedor de formulario]** y pulse el icono **[!UICONTROL Configurar]** ![configurar](assets/configure.png). Abre el explorador de propiedades y muestra las propiedades del contenedor de formularios adaptables.
1. En el navegador de propiedades, expanda el acordeón **[!UICONTROL Electronic Signature]** y seleccione la opción **[!UICONTROL Enable Adobe Sign]**. Habilita [!DNL Adobe Sign] para un formulario adaptable.
1. Seleccione un servicio de nube de la lista ya configurada de Cloud Services [!DNL Adobe Sign].

   Si la lista **[!UICONTROL Cloud Service de Adobe Sign]** está vacía, siga el artículo [Configurar Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) para configurar el servicio.

   La lista desplegable enumera los servicios de nube que existen en la carpeta `global` en Herramientas > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Además, en la lista desplegable también se enumeran los servicios de nube que existen en la carpeta seleccionada en el campo **[!UICONTROL Configuration Container]** al crear un formulario adaptable.

1. Seleccione el orden de firma del cuadro de diálogo **[!UICONTROL Los firmantes pueden firmar]**. [!DNL Adobe Sign] los cantantes pueden firmar un formulario adaptable  **[!UICONTROL secuencialmente]**  (uno tras otro firmante o  **[!UICONTROL simultáneamente]** ) en cualquier orden.

   En orden secuencial, un firmante recibe el formulario para firmar a la vez. Una vez que un firmante completa la firma del documento, el formulario se envía al siguiente firmante, etc.

   En orden simultáneo, varios firmantes pueden firmar un formulario a la vez.

1. [Agregue firmantes a un ](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) formulario adaptable y pulse el icono Listo  ![aem_6_3_forms_](assets/aem_6_3_forms_save.png) saveicon para guardar los cambios.


### Agregar firmantes a un formulario adaptable {#addsignerstoanadaptiveform}

Solo se puede tener un firmante o varios firmantes para un formulario adaptable. Al agregar un firmante, también puede configurar los detalles de autenticación del firmante. También puede seleccionar si el usuario que rellena el formulario y el cantante son la misma persona. Realice los siguientes pasos para agregar y proporcionar varios detalles sobre un firmante:

1. En el navegador de contenido, pulse **[!UICONTROL Contenedor de formulario]** y pulse el icono **[!UICONTROL Configurar]** ![configurar](assets/configure.png). Abre el explorador de propiedades con propiedades del contenedor de formularios adaptables.
1. En el navegador de propiedades, expanda el acordeón **[!UICONTROL Electronic Signature]** y seleccione la opción **[!UICONTROL Enable Adobe Sign]**. Habilita [!DNL Adobe Sign] para un formulario adaptable.
1. Pulse **[!UICONTROL Agregar firmante]** en **[!UICONTROL Configuración del firmante]**. Agrega un firmante al formulario adaptable. Puede agregar varios [!DNL Adobe Sign] firmantes a un formulario adaptable.
   ![detalles telefónicos](assets/phone-details.png)

1. Haga clic en el icono **Edit** ![aem_6_3_edit](assets/aem_6_3_edit.png) para especificar la siguiente información sobre el firmante:

   * **[!UICONTROL Título]:** especifique un título para identificar a un firmante de forma única.

   * **[!UICONTROL ¿El signatario y quien rellena el formulario son la misma persona?]:** seleccione  **Sí** si la persona que rellena el formulario y la que firma primero son la misma persona. Si la opción está establecida en **No,** no utilice el componente del paso de firma en el formulario adaptable. Si el formulario contiene un componente Paso de firma, el campo se establece automáticamente como Sí.

   * **[!UICONTROL Dirección de correo electrónico del firmante]:** especifique la dirección de correo electrónico del firmante. El firmante recibe los documentos o formularios firmados en la dirección de correo electrónico especificada. Puede elegir utilizar una dirección de correo electrónico proporcionada en un campo de formulario, en AEM perfil de usuario del usuario que ha iniciado sesión o escribir manualmente una dirección de correo electrónico. Es un paso obligatorio. Asegúrese de que la dirección de correo electrónico del primer firmante o del único firmante (en el caso de un firmante único) no sea idéntica a la cuenta [!DNL Adobe Sign] utilizada para configurar los servicios en la nube de AEM.

   * **[!UICONTROL Método de autenticación de firmante]:** especifique el método para autenticar a un usuario antes de abrir un formulario para firmar. Puede elegir entre teléfono, base de conocimientos y autenticación social basada en identidad.
   >[!NOTE]
   >
   >    * De forma predeterminada, la autenticación basada en la identidad social proporciona una opción para autenticarse con Facebook, Google y LinkedIn. Puede ponerse en contacto con el soporte técnico de [!DNL Adobe Sign] para habilitar otros proveedores de autenticación social.


   * **[!DNL Adobe Sign]campos para rellenar o firmar:** seleccione los  [!DNL Adobe Sign] campos del firmante. Un formulario adaptable puede tener varios campos [!DNL Adobe Sign]. Puede elegir habilitar campos específicos para un firmante. El campo muestra todos los bloques [!DNL Adobe Sign] disponibles. Al seleccionar un bloque, se seleccionan todos los campos del bloque. Puede utilizar el icono X para anular la selección de un campo.

   ![signer-details](assets/signer-details.png)

   La imagen anterior tiene dos ejemplos de [!DNL Adobe Sign] Bloques: Información personal y detalles de Office

   Pulse el icono Listo ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). Se agrega y configura el firmante.

### Seleccione Enviar acción para un formulario adaptable {#selectsubmitactionforanadaptiveform}

Después de agregar campos [!DNL Adobe Sign] a un formulario adaptable, habilitar [!DNL Adobe Sign] desde el contenedor de formularios, seleccionar el Cloud Service [!DNL Adobe Sign] y agregar [!DNL Adobe Sign] Signers, seleccione una acción de envío adecuada para el formulario adaptable. Para obtener información detallada sobre las acciones de envío de formularios adaptables, consulte [Configuración de la acción de envío](../../forms/using/configuring-submit-actions.md).

Además, un formulario adaptable habilitado para [!DNL Adobe Sign] solo se envía después de que todos los firmantes firmen el formulario. Puede encontrar formularios parcialmente firmados en la sección Firma pendiente del portal de formularios. [!DNL Adobe Sign] El servicio de configuración mantiene el  [!DNL Adobe Sign] servidor de sondeo a intervalos  [regulares ](../../forms/using/adobe-sign-integration-adaptive-forms.md) para verificar el estado de las firmas. Si todos los firmantes completan la firma del formulario, se inicia el servicio de acción de envío y se envía el formulario. Si utiliza una acción de envío personalizada y el formulario utiliza [!DNL Adobe Sign], actualice la acción de envío personalizada para utilizar el servicio de acción de envío.

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

La experiencia de firma de formularios está lista. Puede obtener una vista previa del formulario para comprobar la experiencia de firma. En el formulario publicado, los campos [!DNL Adobe Sign] Bloque se muestran cuando un firmante recibe el formulario para firmar por correo electrónico. Esta experiencia también se conoce como experiencia de firma fuera de formulario. También puede configurar una experiencia de firma en el formulario para el primer firmante; para obtener información detallada, consulte [Crear experiencia de firma en el formulario](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience).

## Configuración de firmas de nube para un formulario adaptable {#configure-cloud-signatures-for-an-adaptive-form}

Las firmas digitales o remotas basadas en la nube son una nueva generación de firmas digitales que funcionan en equipos de escritorio, dispositivos móviles y la web, y cumplen con los niveles más altos de cumplimiento y seguridad para la autenticación de firmantes. Puede firmar un formulario adaptable con firmas digitales basadas en la nube.

Después de [editar las propiedades del formulario adaptable para el signo de Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign), realice los siguientes pasos para agregar el campo de firma de nube a un formulario adaptable:

1. Arrastre y suelte el componente **[!UICONTROL Bloque de Adobe Sign]** desde el navegador de componentes al formulario adaptable. El componente [!UICONTROL Adobe Sign Block] tiene todos los campos [!DNL Adobe Sign] admitidos. De forma predeterminada, agrega un campo **[!UICONTROL Signature]** al formulario adaptable.

   ![Bloque de firma](assets/sign-block-new.png)

1. Seleccione el componente **[!UICONTROL Adobe Sign Block]** y pulse el icono **Edit** ![aem_6_3_edit](assets/aem_6_3_edit.png). Muestra las opciones para añadir campos y dar formato al aspecto de un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Seleccione y añada  [!DNL Adobe Sign] campos. **B.** Expanda el  [!DNL Adobe Sign] bloque a la vista de pantalla completa

1. Pulse el icono **[!UICONTROL Adobe Sign Field]** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png). Muestra las opciones para seleccionar y agregar campos [!DNL Adobe Sign].

   Expanda el campo desplegable **[!UICONTROL Type]** para seleccionar **[!UICONTROL Digital Signature]** y pulse el icono **Listo** para añadir el campo seleccionado al bloque [!DNL Adobe Sign].

   ![Firmas digitales](assets/digital_signatures_new.png)

   Es obligatorio proporcionar un nombre único para un campo.

   Aplique firmas digitales al formulario adaptable utilizando:

   * Firmas en la nube: Firme con un [ID digital](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) alojado por un proveedor de servicios de confianza.
   * Adobe Acrobat o Reader: Descargue y abra el documento con Adobe Acrobat o Reader para firmarlo con una tarjeta inteligente, un token USB o un ID digital basado en archivos.

   Después de agregar el campo de firma de nube al formulario adaptable, realice los siguientes pasos para completar el proceso de configuración:

   * [Habilitar Adobe Sign para un formulario adaptable](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [Seleccione el Cloud Service de Adobe Sign para un formulario adaptable](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [Agregar firmantes de Adobe Sign a un formulario adaptable](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [Seleccione Enviar acción para un formulario adaptable](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## Crear experiencia de firma en formularios {#create-in-form-signing-experience}

Un usuario también puede firmar un formulario adaptable mientras lo rellena. Esta experiencia también se conoce como experiencia de firma en formularios. La experiencia de firma en el formulario solo está disponible para el primer cantante en un entorno de varios firmantes. Siga estos pasos para crear una experiencia de firma en formularios para un formulario adaptable:

1. [Añada y configure el componente](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component) Paso de firma .
1. [Añada el componente](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component) Paso de resumen .

![Experiencia de firma en formulario](assets/in_form_signing_experience_new.png)

### Añadir y configurar el componente Paso de firma {#add-and-configure-the-signature-step-component}

Utilice el componente Paso de firma para proporcionar un área donde firmar electrónicamente el formulario rellenado. Cuando se representa la sección que contiene el componente Paso de firma, muestra una versión en PDF que se puede firmar del formulario rellenado. El componente Paso de firma ocupa el ancho completo disponible para el formulario. Se recomienda no tener ningún otro componente en la sección que contenga el componente Paso de firma.

Realice los siguientes pasos para configurar el componente Paso de firma:

1. Arrastre y suelte el componente **[!UICONTROL Paso de firma]** desde el explorador de componentes al formulario.
1. Seleccione el componente del paso Firma recién agregado y pulse el icono **Configurar** ![configurar](assets/configure.png). Abre el navegador de propiedades y muestra las propiedades del paso Firma. Configure las siguientes propiedades:

   * **[!UICONTROL Nombre]**: Especifique el nombre del componente.

   * **[!UICONTROL Título]:** especifique el título único del componente.
   * **[!UICONTROL Mensaje de plantilla]:** especifique el mensaje que se mostrará mientras se carga el PDF de firma. [!DNL Adobe Sign] los servicios tardan un tiempo en preparar y cargar el PDF de firma.
   * **[!UICONTROL Servicio de firma]:** seleccione la  **[!DNL Adobe Sign]** opción .

   * **[!UICONTROL Utilice el componente]** de firma electrónica heredado: Si utiliza el formulario adaptable respectivo en  [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md), AEM  [!DNL Forms] aplicación o el formulario adaptable subyacente tiene un componente de firma electrónica heredado, seleccione la opción  **Usar** componente de firma electrónica heredado .

   * **[!UICONTROL Configuración]**: Seleccione una configuración ([!DNL Adobe Sign] Cloud Service). El cuadro desplegable solo está disponible si la opción **Use legacy E-sign component** está activada.

   * **[!UICONTROL Clase]** CSS: Especifique la clase CSS para el componente.

   Pulse el icono Listo ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para guardar los cambios.

   ![Paso de firma](assets/signature_step_new.png)

   >[!NOTE]
   >
   > * Cuando arrastra y suelta el componente **[!UICONTROL Paso de firma]** al formulario, el **[!UICONTROL es el firmante y la persona que rellena el formulario el mismo?]** se establece automáticamente en  **Yes**. Es necesario mantener el formulario en funcionamiento.
      >
      > 
   * Utilice el componente Paso de resumen después del componente Paso de firma para obtener la mejor experiencia. El paso Resumen envía el formulario de forma automática e inmediata después de completar la firma de un formulario en el componente Paso de firma. Si no utiliza el paso de resumen, se activa un envío automático solo después del intervalo establecido utilizando el [Servicio de configuración de Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status).
      > Algunas prácticas recomendadas son:
   > * El panel de formulario adaptable que contiene el paso Firma siempre se encuentra en el último o el segundo último panel de un formulario adaptable. Puede ser el segundo último panel solo cuando el último panel contiene el paso Resumen.
   > * El panel que contiene el componente de paso Firma o Resumen no puede contener ningún otro componente.
   > * Los formularios adaptables que contienen Paso de firma no pueden tener botón de envío.
   > * El envío de los formularios adaptables que contienen el paso Firma se gestiona mediante un servicio en segundo plano o el paso Resumen. Si hay un firmante configurado que también esté rellenando el formulario, la ventaja de gestionar el envío del formulario adaptable mediante el paso Resumen es que evalúa inmediatamente que el firmante ha firmado el formulario e invoca la acción de envío. Un servicio en segundo plano tarda más en evaluar si todos los firmantes configurados han firmado el formulario y retrasa la presentación del formulario adaptable.
   > * Diseñe el formulario para que el usuario no pueda volver atrás desde un panel que contenga el paso Firma o Resumen.



### Configurar la página de agradecimiento o el componente de paso de resumen {#configure-the-thank-you-page-or-summary-step-component}

El componente **Paso de resumen** envía automáticamente el formulario, rellena la información dentro de la página de resumen personalizada y muestra el resumen del formulario enviado. También obtiene la información necesaria en el mapa de retorno. El componente Paso de resumen ocupa el ancho completo disponible para el formulario. Se recomienda no tener ningún otro componente en la sección que contenga el componente Paso de resumen.

Ahora, la experiencia de firma de formularios en está lista. Puede obtener una vista previa del formulario para comprobar la experiencia de firma.

## Preguntas frecuentes {#frequently-asked-questions}

**P:** Puede incrustar un formulario adaptable en otro formulario adaptable. ¿Puede habilitarse [!DNL Adobe Sign] el formulario adaptable incrustado?
**Ans:** No, AEM no  [!DNL Forms] admite el uso de un formulario adaptable que incruste un formulario adaptable  [!DNL Adobe Sign] habilitado para firmar

**P:** Cuando creo un formulario adaptable utilizando la plantilla avanzada y lo abro para editarlo, aparece el mensaje de error &quot;Las firmas electrónicas no están configuradas correctamente&quot;. aparece. ¿Cómo se resuelve el mensaje de error?
**Ans:** El formulario adaptable creado con la plantilla avanzada está configurado para utilizarse  [!DNL Adobe Sign]. Para resolver el error, cree y seleccione una configuración de nube [!DNL Adobe Sign] y configure un [!DNL Adobe Sign] firmante para el formulario adaptable.

**P:** ¿Puedo utilizar etiquetas de  [!DNL Adobe Sign] texto en un componente de texto estático de un formulario adaptable?
**Ans:** sí, se pueden utilizar etiquetas de texto en un componente de texto para añadir  [!DNL Adobe Sign] campos a un  [documento de registro](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)  (solo la opción de documento de registro generado automáticamente) activado en forma adaptable. Para obtener más información sobre el procedimiento y las reglas para crear una etiqueta de texto, consulte [Documentación de Adobe Sign](https://helpx.adobe.com/sign/using/text-tag.html). Tenga en cuenta también que los formularios adaptables tienen una compatibilidad limitada con las etiquetas de texto. Puede utilizar las etiquetas de texto para crear solo los campos que admite [Adobe Sign Block](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form).

**P:** AEM  [!DNL Forms] proporciona los componentes de paso Bloque de  [!UICONTROL Adobe Sign ] y Firma. ¿Se pueden utilizar simultáneamente en una forma adaptativa?
**Ans:** puede utilizar ambos componentes simultáneamente en un formulario. Estas son algunas recomendaciones para utilizar estos componentes:

**Bloque de Adobe Sign:** puede utilizar el Bloque de  [!UICONTROL Adobe Sign ] para agregar campos de  [!UICONTROL Adobe ] en cualquier parte del formulario adaptable. También ayuda a asignar campos específicos a los firmantes. De forma predeterminada, cuando se ve una vista previa de un formulario adaptable o se publica [!UICONTROL Adobe Sign] Block no está visible. Estos bloques solo están habilitados en el documento de firma. En el documento de firma, solo se activan los campos asignados a un firmante. [!UICONTROL El ] Signblock de Adobe se puede utilizar con los firmantes primero y siguientes.

**Componente de paso de firma:**  puede utilizar el componente de paso de firma para crear una experiencia de firma en el formulario. Solo permite que el primer firmante firme mientras se rellena el formulario. Cuando se representa la sección que contiene el componente Paso de firma, muestra una versión PDF del formulario que se puede firmar. Generalmente es la última o la penúltima sección seguida del componente de resumen de un formulario.

## Solución de problemas {#troubleshoot}

### [!DNL Adobe Sign] errores de acuerdo  {#adobe-sign-agreement-failures}

****
ProblemaCuando el  [!DNL Adobe Sign] servicio está configurado para un formulario adaptable, el servicio no crea un  [!DNL Adobe Sign] acuerdo para el formulario adaptable subyacente.

**Resolución**

* Compruebe la [configuración del servicio en la nube de Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md) utilizada en el formulario adaptable.
* Asegúrese de que la aplicación de API en el servidor [!DNL Adobe Sign] utilizado para configurar el servicio en la nube [!DNL Adobe Sign] tiene los permisos necesarios.
* Si utiliza varios [!DNL Adobe Sign] servicios en la nube, señale la **[!UICONTROL URL oAuth]** de todos los servicios a la misma **[!UICONTROL Adobe Sign Share]**.

* Utilice direcciones de correo electrónico independientes para configurar la cuenta [!DNL Adobe Sign] y para el primer firmante y el primer firmante. La dirección de correo electrónico del primer firmante o del único firmante (en el caso del firmante único) no puede ser idéntica a la cuenta [!DNL Adobe Sign] utilizada para configurar los servicios en la nube de AEM.

### AEM flujo de trabajo [!DNL Forms] configurado para un formulario adaptable [!DNL Adobe Sign] habilitado no se inicia {#adobe-sign-aem-form-workflow-failures}

****
ProblemaCuando  [!DNL Adobe Sign] se configura para un formulario adaptable, el flujo de trabajo configurado con la opción Invocar  [!DNL Forms] flujo de trabajo no se inicia.

**Resolución**

* Cuando utiliza [!DNL Adobe Sign] sin el paso de firma o el formulario requiere firmas de varias personas, AEM servidor [!DNL Forms] espera a que el programador confirme que todas las personas han firmado el formulario. El planificador envía el formulario adaptable solo después de que todas las personas hayan completado la firma y el flujo de trabajo se inicie solo después de que se haya enviado correctamente el formulario adaptable. Puede acortar el intervalo del [planificador](adobe-sign-integration-adaptive-forms.md) para comprobar el estado de la firma del formulario a intervalos rápidos y el envío rápido del formulario.


## Artículos relacionados {#related-articles}

* [Integración de Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [Prácticas recomendadas para utilizar Adobe Sign con formularios adaptables](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
* [Uso de Adobe Sign con AEM Forms (vídeo)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
