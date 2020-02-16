---
title: Activación de datos adjuntos para un formulario HTML5
seo-title: Activación de datos adjuntos para un formulario HTML5
description: De forma predeterminada, la compatibilidad con archivos adjuntos para formularios HTML5 está desactivada.
seo-description: De forma predeterminada, la compatibilidad con archivos adjuntos para formularios HTML5 está desactivada.
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
translation-type: tm+mt
source-git-commit: 00e14be8a0775149b3ee7ce8cd781dd7f1e49e4f

---


# Activación de datos adjuntos para un formulario HTML5 {#enabling-attachments-for-an-html-form}

Puede cargar, previsualizar y enviar archivos adjuntos con formularios HTML5. De forma predeterminada, la compatibilidad con datos adjuntos está deshabilitada. Para habilitar la compatibilidad con los datos adjuntos:

1. Cree un perfil [](/help/forms/using/custom-profile.md) personalizado con la propiedad de cadena mutiselect `mfAttachmentOptions`.
1. En el perfil personalizado, especifique las propiedades `fileSizeLimit``multiSelect`y `buttonTex`t para configurar las opciones del widget de datos adjuntos del archivo. Si es necesario, también puede especificar más propiedades personalizadas.

1. En el perfil personalizado, utilice las configuraciones siguientes:

   * **multiSelect** -> true o false (true de forma predeterminada)
   * **fileSizeLimit** -> value_in_mb (digamos 5) (2 MB de forma predeterminada)
   * **buttonText** -> Texto del botón para la ventana emergente (&quot;Adjuntar&quot; de forma predeterminada)
   * **aceptar** -> tipos de archivo para aceptar (&quot;audio/&amp;último;, vídeo/&amp;último;, imagen/&amp;último;, texto/&amp;último;, .pdf&quot; de forma predeterminada)
   >[!NOTE]
   >
   >En Microsoft Internet Explorer 9, los usuarios pueden adjuntar archivos que superen el límite especificado. Se trata de un problema conocido.

1. Utilice el editor [de](/help/forms/using/manage-form-metadata.md) metadatos para seleccionar el perfil personalizado que ha creado anteriormente para los formularios HTML 5.
1. Representar la plantilla de formulario con un perfil personalizado y el icono de archivos adjuntos aparecería en la barra de herramientas de formularios.

   >[!NOTE]
   >
   >De forma predeterminada, el portal de formularios proporciona un perfil personalizado con la capacidad de borradores y archivos adjuntos habilitada. Para obtener más información sobre el perfil **Guardar como borrador** , consulte [Guardar formularios HTML5 como borrador](/help/forms/using/saving-html5-form-draft.md).

1. Haga clic en el icono de datos adjuntos y aparecerá un cuadro de diálogo de selección de datos adjuntos. Busque y seleccione el archivo adjunto y haga clic en **Adjuntar**.

   >[!NOTE]
   >
   >Para obtener una vista previa de un archivo adjunto, haga clic en el nombre del mismo.

   >[!NOTE]
   >
   >La opción de vista previa de archivos no está disponible para usuarios anónimos.

## Formato de envío de datos adjuntos {#attachment-submission-format}

Cuando los archivos adjuntos están activados, el formulario HTML5 envía datos de varias partes. Los datos de envío de varias partes tienen dos partes **dataXml** y **archivos adjuntos**.

>[!NOTE]
>
>Para la compatibilidad con versiones anteriores, si `mfAllowAttachments` la opción está desactivada, los formularios HTML5 no envían los datos de varias partes. Envía datos XML simples en formato **application/xml** .

Si el indicador mfAllowAttachments está activado, el servicio [proxy de servicio de](/help/forms/using/service-proxy.md) envío también publica datos de varias partes con dataXml y datos adjuntos.
