---
title: Activación de archivos adjuntos en un formulario HTML5
seo-title: Enabling attachments for an HTML5 form
description: De forma predeterminada, la compatibilidad con archivos adjuntos de los formularios HTML5 está deshabilitada.
seo-description: By default, the attachment support for HTML5 forms is disabled.
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: Mobile Forms
exl-id: 68912260-179a-4d1b-b944-0a1777c021ac
source-git-commit: 6e2a0f053a1f6989524e9ae2b1dcb001b0397ac6
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 2%

---

# Activación de archivos adjuntos en un formulario HTML5 {#enabling-attachments-for-an-html-form}

Puede cargar, previsualizar y enviar archivos adjuntos con formularios HTML5. De forma predeterminada, la compatibilidad con archivos adjuntos está deshabilitada. Para habilitar el soporte de datos adjuntos:

1. Cree un [perfil personalizado](/help/forms/using/custom-profile.md) con un `mfAttachmentOptions` multiselect string property . Cada cadena de la variable `mfAttachmentOptions` la propiedad debe tener `property=value` para configurar las opciones del widget de archivos adjuntos. La variable `property` y `value` puede tener cualquiera de los siguientes valores:

   | Propiedad | Valor |
   |--- |---|
   | multiSelect | true o false (true de forma predeterminada) |
   | fileSizeLimit | Número en MB (2 MBs de forma predeterminada). Por ejemplo, 5. |
   | buttonText | Texto del botón de la ventana emergente (&quot;Adjuntar&quot; de forma predeterminada) |
   | Aceptar | lista separada por comas de los tipos de archivo que se van a aceptar (&quot;audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf&quot; de forma predeterminada) |

   Por ejemplo:

   ![configurar opciones](assets/mfAttachmentOptions.png)

   Si es necesario, también puede especificar más opciones personalizadas para la variable `mfAttachmentOptions` propiedad.

   >[!NOTE]
   >
   >En Microsoft Internet Explorer 9, los usuarios pueden adjuntar archivos que superen el límite especificado. Es un problema conocido.

1. Utilice la variable [editor de metadatos](/help/forms/using/manage-form-metadata.md) para seleccionar el perfil personalizado que ha creado anteriormente para los formularios de HTML 5.
1. Representar la plantilla de formulario con un perfil personalizado y el icono de archivos adjuntos aparecería en la barra de herramientas de formularios.

   >[!NOTE]
   >
   >De forma predeterminada, el portal de formularios proporciona un perfil personalizado con la capacidad de borradores y archivos adjuntos habilitada. Para obtener más información sobre la variable **Guardar como borrador** perfil, consulte [Guardado de formularios del HTML 5 como borrador](/help/forms/using/saving-html5-form-draft.md).

1. Haga clic en el icono de datos adjuntos y aparecerá un cuadro de diálogo de selección de datos adjuntos. Busque y seleccione el archivo adjunto y haga clic en **Adjuntar**.

   >[!NOTE]
   >
   >Para obtener una vista previa de un archivo adjunto, haga clic en su nombre.

   >[!NOTE]
   >
   >La opción de vista previa del archivo no está disponible para usuarios anónimos.

## Formato de envío de datos adjuntos {#attachment-submission-format}

Cuando los archivos adjuntos están habilitados, el formulario de HTML5 envía datos de varias partes. Los datos de envío en varias partes tienen dos partes **dataXml** y **archivos adjuntos**.

>[!NOTE]
>
>Para la compatibilidad con versiones anteriores, si `mfAllowAttachments` está desactivada, los formularios HTML5 no envían los datos de varias partes. Envía xml de datos simples en **application/xml** formato.

Si el indicador mfAllowAttachments está activado, la variable [enviar servicio proxy](/help/forms/using/service-proxy.md) también publica datos de varias partes con dataXml y archivos adjuntos.
