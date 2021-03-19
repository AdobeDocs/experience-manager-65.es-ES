---
title: Activación de archivos adjuntos en un formulario HTML5
seo-title: Activación de archivos adjuntos en un formulario HTML5
description: De forma predeterminada, la compatibilidad con archivos adjuntos de los formularios HTML5 está desactivada.
seo-description: De forma predeterminada, la compatibilidad con archivos adjuntos de los formularios HTML5 está desactivada.
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Activación de archivos adjuntos en un formulario HTML5 {#enabling-attachments-for-an-html-form}

Puede cargar, previsualizar y enviar archivos adjuntos con formularios HTML5. De forma predeterminada, la compatibilidad con archivos adjuntos está deshabilitada. Para habilitar el soporte de datos adjuntos:

1. Cree un [perfil personalizado](/help/forms/using/custom-profile.md) con la propiedad de cadena de selección múltiple `mfAttachmentOptions`.
1. En el perfil personalizado, especifique las propiedades `fileSizeLimit`, `multiSelect` y `buttonTex`t para configurar las opciones del widget de archivos adjuntos. Si es necesario, también puede especificar más propiedades personalizadas.

1. En el perfil personalizado, utilice las siguientes configuraciones:

   * **multiSelect** -> true o false (true de forma predeterminada)
   * **fileSizeLimit** -> value_in_mb (digamos 5) (2 MB de forma predeterminada)
   * **buttonText**  -> Texto del botón de la ventana emergente (&quot;Adjuntar&quot; de forma predeterminada)
   * **aceptar** -> tipos de archivo que aceptar (&quot;audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf&quot; de forma predeterminada)

   >[!NOTE]
   >
   >En Microsoft Internet Explorer 9, los usuarios pueden adjuntar archivos que superen el límite especificado. Es un problema conocido.

1. Utilice el [editor de metadatos](/help/forms/using/manage-form-metadata.md) para seleccionar el perfil personalizado que ha creado anteriormente para los formularios HTML 5.
1. Representar la plantilla de formulario con un perfil personalizado y el icono de archivos adjuntos aparecería en la barra de herramientas de formularios.

   >[!NOTE]
   >
   >De forma predeterminada, el portal de formularios proporciona un perfil personalizado con la capacidad de borradores y archivos adjuntos habilitada. Para obtener más información sobre el perfil **Guardar como borrador**, consulte [Guardar formularios HTML5 como borrador](/help/forms/using/saving-html5-form-draft.md).

1. Haga clic en el icono de datos adjuntos y aparecerá un cuadro de diálogo de selección de datos adjuntos. Examine y seleccione el archivo adjunto y haga clic en **Adjuntar**.

   >[!NOTE]
   >
   >Para obtener una vista previa de un archivo adjunto, haga clic en su nombre.

   >[!NOTE]
   >
   >La opción de vista previa del archivo no está disponible para usuarios anónimos.

## Formato de envío de datos adjuntos {#attachment-submission-format}

Cuando los archivos adjuntos están habilitados, el formulario HTML5 envía datos de varias partes. Los datos de envío de varias partes tienen dos partes **dataXml** y **archivos adjuntos**.

>[!NOTE]
>
>Para la compatibilidad con versiones anteriores, si la opción `mfAllowAttachments` está desactivada, los formularios HTML5 no envían los datos de varias partes. Envía xml de datos simples en formato **application/xml**.

Si el indicador mfAllowAttachments está activado, el [servicio proxy de envío](/help/forms/using/service-proxy.md) también publica datos de varias partes con dataXml y archivos adjuntos.
