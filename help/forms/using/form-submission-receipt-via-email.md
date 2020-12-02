---
title: Envío de un acuse de recibo de envío de formulario por correo electrónico
seo-title: Envío de un acuse de recibo de envío de formulario por correo electrónico
description: AEM Forms permite configurar la acción de envío por correo electrónico que envía una confirmación a un usuario al enviar el formulario.
seo-description: AEM Forms permite configurar la acción de envío por correo electrónico que envía una confirmación a un usuario al enviar el formulario.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
translation-type: tm+mt
source-git-commit: acc2a3977353386d7e1dfd1344a61d78812fe3fc
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---


# Envío de confirmación de envío de formulario por correo electrónico {#sending-a-form-submission-acknowledgement-via-email}

## Envío de datos de formulario adaptable {#adaptive-form-data-submission}

Los formularios adaptables proporcionan varios flujos de trabajo predeterminados [acciones de envío](../../forms/using/configuring-submit-actions.md) para enviar los datos del formulario a diferentes extremos.

Por ejemplo, la acción de envío **[!UICONTROL Enviar correo electrónico]** envía un mensaje de correo electrónico cuando se envía correctamente un formulario adaptable. También se puede configurar para enviar los datos del formulario y el PDF en el correo electrónico.

Este artículo detalla los pasos para habilitar la acción Correo electrónico en un formulario adaptable y las diferentes configuraciones que proporciona.

>[!NOTE]
>
>También puede utilizar la opción **[!UICONTROL Enviar archivo PDF por correo electrónico]** para enviar el formulario completado por correo electrónico como archivo adjunto en PDF. Las opciones de configuración disponibles para esta acción son las mismas que las opciones disponibles para la acción **[!UICONTROL Enviar correo electrónico]**. La acción Enviar un PDF por correo electrónico solo está disponible para formularios adaptables basados en XFA

## Enviar acción de correo electrónico {#email-action}

La acción Enviar correo electrónico permite a un autor enviar correo electrónico automáticamente a uno o varios destinatarios cuando se envía correctamente un formulario adaptable.

>[!NOTE]
>
>Para utilizar la acción Enviar correo electrónico, debe configurar el servicio de correo AEM como se describe en [Configuración del servicio de correo](/help/sites-administering/notification.md#configuring-the-mail-service).

### Activación de la acción Enviar correo electrónico en un formulario adaptable {#enabling-email-action-on-an-adaptive-form}

1. Abra un formulario adaptable en modo **[!UICONTROL editar]**.

1. En la ficha **[!UICONTROL Contenido]**, toque **[!UICONTROL Contenedor de formulario]** y toque ![configurar](assets/configure-icon.svg) para vista de las propiedades del formulario adaptable.

1. En la sección **[!UICONTROL Envío]**, seleccione **[!UICONTROL Enviar correo electrónico]** en la lista desplegable **[!UICONTROL Enviar acción]**.

   ![Enviar acciones](assets/submission-actions.png)

1. Especifique ID de correo electrónico válidos en los campos **[!UICONTROL Para]**, **[!UICONTROL CC]** y **[!UICONTROL BCC]**.

   Especifique el asunto y el cuerpo del correo electrónico en los campos **[!UICONTROL Subject]** y **[!UICONTROL Email Template]**, respectivamente.

   También puede especificar marcadores de posición de variables en los campos, en cuyo caso, los valores de los campos se procesan cuando un usuario final envía correctamente el formulario. Para obtener más información, consulte [Uso de nombres de campo de formulario adaptables para crear dinámicamente contenido de correo electrónico](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Seleccione **[!UICONTROL Incluir archivos adjuntos]** si el formulario incluye archivos adjuntos y desea adjuntarlos en el correo electrónico.

   >[!NOTE]
   >
   >Si elige la opción **[!UICONTROL Enviar archivo PDF por correo electrónico]**, debe seleccionar la opción Incluir archivos adjuntos.

1. Haga clic en ![guardar](assets/save_icon.svg) para guardar los cambios.

### Uso de nombres de campo de formulario adaptables para crear dinámicamente contenido de correo electrónico {#using-adaptive-form-field-names-to-dynamically-create-email-content}

Los nombres de campo de un formulario adaptable se denominan marcadores de posición que se sustituyen por el valor de dicho campo después de que un usuario envía el formulario.

En la acción **[!UICONTROL Enviar correo electrónico]**, puede utilizar marcadores de posición que se procesan cuando se realiza la acción. Significa que los encabezados del correo electrónico (como **[!UICONTROL A]**, **[!UICONTROL CC]**, **[!UICONTROL BCC]**, **[!UICONTROL Subject]**) se generan cuando el usuario envía el formulario.

Para definir un marcador de posición, especifique `${<field name>}` en un campo después de seleccionar **[!UICONTROL Enviar correo electrónico]** como Acción de envío.

Por ejemplo, si el formulario contiene el campo **[!UICONTROL Dirección de correo electrónico]**, denominado `email_addr`, para capturar el ID de correo electrónico de un usuario, puede especificar lo siguiente en los campos **[!UICONTROL Para]**, **[!UICONTROL CC]** o **[!UICONTROL BCC]**.

`${email_addr}`

Cuando un usuario envía el formulario, se envía un correo electrónico al ID de correo electrónico introducido en el campo `email_addr` del formulario.

>[!NOTE]
>
>Puede encontrar el nombre de un campo en el cuadro de diálogo **[!UICONTROL Editar]** del campo.

Los marcadores de posición de variables también se pueden utilizar en los campos **[!UICONTROL Subject]** y **[!UICONTROL Email Template]**.

Por ejemplo:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>Los campos de los paneles repetitivos no se pueden usar como marcadores de posición de variables.

