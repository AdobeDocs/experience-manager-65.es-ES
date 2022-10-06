---
title: Enviar una confirmación de envío de formulario por correo electrónico
seo-title: Sending a form submission acknowledgement via email
description: AEM Forms permite configurar la acción de envío por correo electrónico que envía un acuse de recibo a un usuario al enviar el formulario.
seo-description: AEM Forms allows you to configure the email submit action that sends an acknowledgement to a user on submitting the form.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
exl-id: bca4044a-18a9-4b97-92de-eff1e9a840f9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 40%

---

# Enviar una confirmación de envío de formulario por correo electrónico {#sending-a-form-submission-acknowledgement-via-email}

## Envío de datos de formulario adaptable {#adaptive-form-data-submission}

Los formularios adaptables ofrecen varios [enviar acciones](../../forms/using/configuring-submit-actions.md) flujos de trabajo para enviar los datos del formulario a diferentes extremos.

Por ejemplo, la variable **[!UICONTROL Enviar correo electrónico]** la acción enviar envía un correo electrónico cuando se envía correctamente un formulario adaptable. También se puede configurar el envío de los datos del formulario y el PDF en el correo electrónico.

Este artículo detalla los pasos para habilitar la acción Correo electrónico en un formulario adaptable y las diferentes configuraciones que proporciona.

>[!NOTE]
>
>También puede usar la opción **[!UICONTROL Enviar PDF por correo electrónico]** para enviar el formulario completado por correo electrónico como archivo adjunto PDF. Las opciones de configuración disponibles para esta acción son las mismas que las disponibles para la acción **[!UICONTROL Enviar correo electrónico]**. La acción PDF de correo electrónico solo está disponible para formularios adaptables basados en XFA

## Acción Enviar correo electrónico {#email-action}

La acción Send email permite a un autor enviar correos electrónicos automáticamente a uno o varios destinatarios cuando se envía correctamente un formulario adaptable.

>[!NOTE]
>
>Para utilizar la acción Send email , debe configurar el servicio de correo AEM como se describe en [Configuración del servicio de correo](/help/sites-administering/notification.md#configuring-the-mail-service).

### Activación de la acción Enviar correo electrónico en un formulario adaptable {#enabling-email-action-on-an-adaptive-form}

1. Abra un formulario adaptable en **[!UICONTROL editar]** en el menú contextual.

1. En el **[!UICONTROL Contenido]** ficha, toque **[!UICONTROL Contenedor de formulario]** y toque ![configure](assets/configure-icon.svg) para ver las propiedades del formulario adaptable.

1. En el **[!UICONTROL Envío]** , seleccione **[!UICONTROL Enviar correo electrónico]** de la variable **[!UICONTROL Enviar acción]** lista desplegable.

   ![Acciones de envío](assets/submission-actions.png)

1. Especifique ID de correo electrónico válidos en la **[!UICONTROL Hasta]**, **[!UICONTROL CC]** y **[!UICONTROL CCO]** campos.

   Especifique el asunto y el cuerpo del correo electrónico en la **[!UICONTROL Asunto]** y **[!UICONTROL Plantilla de correo electrónico]** , respectivamente.

   También puede especificar marcadores de posición de variables en los campos, en cuyo caso, los valores de los campos se procesan cuando un usuario final envía correctamente el formulario. Para obtener más información, consulte [Uso de nombres de campos de formulario adaptables para crear contenido de correo electrónico de forma dinámica](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Select **[!UICONTROL Incluir archivos adjuntos]** si el formulario incluye archivos adjuntos y desea adjuntarlos en el correo electrónico.

   >[!NOTE]
   >
   >Si elige la opción **[!UICONTROL Enviar PDF por correo electrónico]** , debe seleccionar la opción Include attachment .

1. Haga clic en ![guardar](assets/save_icon.svg) para guardar los cambios.

### Uso de nombres de campos de formulario adaptables para crear contenido de correo electrónico de forma dinámica {#using-adaptive-form-field-names-to-dynamically-create-email-content}

Los nombres de campo de un formulario adaptable se denominan marcadores de posición que se sustituyen por el valor de ese campo después de que un usuario envíe el formulario.

En la acción **[!UICONTROL Enviar correo electrónico]**, puede utilizar marcadores de posición que se procesan cuando se realiza la acción. Eso significa que los encabezados del correo electrónico (como **[!UICONTROL Para]**, **[!UICONTROL CC]**, **[!UICONTROL CCO]** y **[!UICONTROL Asunto]**) se generan cuando el usuario envía el formulario.

Para definir un marcador de posición, especifique `${<field name>}` en un campo después de seleccionar **[!UICONTROL Enviar correo electrónico]** como acción de envío.

Por ejemplo, si el formulario contiene el campo **[!UICONTROL Dirección de correo electrónico]**, denominado `email_addr`, para capturar el ID de correo electrónico de un usuario, puede especificar lo siguiente en los campos **[!UICONTROL Para]**, **[!UICONTROL CC]** o **[!UICONTROL CCO]**.

`${email_addr}`

Cuando un usuario envía el formulario, se envía un correo electrónico al ID de correo electrónico introducido en el campo `email_addr` del formulario.

>[!NOTE]
>
>Puede encontrar el nombre de un campo en el cuadro de diálogo **[!UICONTROL Editar]** del campo.

Los marcadores de posición de variables también se pueden usar en los campos **[!UICONTROL Asunto]** y **[!UICONTROL Plantilla de correo electrónico]**.

Por ejemplo:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>Los campos de los paneles repetibles no se pueden usar como marcadores de posición variables.
