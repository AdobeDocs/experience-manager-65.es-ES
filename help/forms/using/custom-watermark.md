---
title: Marca de agua personalizada en la vista previa del PDF de letras
seo-title: Custom watermark in letter PDF preview
description: Aprenda a crear marcas de agua personalizadas en la vista previa del PDF de letras.
seo-description: Learn how to create custom watermark in letter PDF preview.
uuid: 5adfede3-9b38-4a12-bf14-6d80cfb0a05a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: adc7ec13-0675-4071-9c4c-e238202d9d85
docset: aem65
feature: Correspondence Management
exl-id: 7d90fade-1ca4-41d8-bbf9-45490465784a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 1%

---

# Marca de agua personalizada en la vista previa del PDF de letras{#custom-watermark-in-letter-pdf-preview}

## Información general {#overview}

En la interfaz de usuario Crear correspondencia, los usuarios del agente previsualizan la correspondencia en la forma final en la que se envía al posprocesamiento, por ejemplo para correo electrónico o impresión.

Para evitar el uso no autorizado de estos datos, las organizaciones pueden imponer una marca de agua en el PDF de vista previa. La marca de agua predeterminada es &quot;PREVIEW&quot;, que aparece en el PDF.

Para habilitar la marca de agua en el PDF de vista previa, seleccione la opción **[!UICONTROL Aplicar marca de agua]** Durante la opción Vista previa en **[!UICONTROL Configuraciones de administración de correspondencia]** en https://&#39;[server]:[puerto]&#39;/system/console/configMgr.

![marca de agua predeterminada](assets/default-watermark.png)

Puede seguir los pasos siguientes para personalizar el texto y el aspecto de la marca de agua:

## Personalización de la marca de agua en la vista previa del PDF en la IU Crear correspondencia {#customizewatermark-}

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. En la carpeta de aplicaciones, cree una carpeta denominada **[!UICONTROL previsualizar marca de agua]** con una ruta/estructura similar a la carpeta de marca de agua de la vista previa en la carpeta libs:

   1. Haga clic con el botón derecho en el **previsualizar marca de agua** en la siguiente ruta y seleccione **Nodo de superposición**:

      `/libs/fd/cm/configFiles/previewwatermark`

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tiene los siguientes valores:

      **Ruta:** /libs/fd/cm/configFiles/previewwatermark

      **Ubicación de superposición:** /apps/

      **Coincidir tipos de nodo:** Comprobado

      >[!NOTE]
      >
      >No realice cambios en la rama /libs. Cualquier cambio que realice puede perderse, ya que esta rama puede cambiar siempre que:
      >
      >    
      >    
      >    * Actualice en su instancia
      >    * Aplicar una corrección
      >    * Instalación de un paquete de características


   1. Haga clic en **OK** y haga clic en **Guardar todo**. La variable **[!UICONTROL previsualizar marca de agua]** se crea en la ruta de acceso especificada.

1. Copie y pegue el archivo ddx de la carpeta &quot;/libs/fd/cm/configFiles/previewwatermark&quot; a la carpeta &quot;/apps/fd/cm/configFiles/previewwatermark&quot; y haga clic en **[!UICONTROL Guardar todo]**.
1. Realice los cambios deseados en el archivo ddx en /apps/fd/cm/configFiles/previewwatermark/.

   ```xml
   <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
    <PDF result="output.pdf">
     <PDF source="input.pdf"/>
           <Watermark opacity="15%" rotation="45">
            <StyledText>
                     <p font-family="Georgia" font-size="70pt" color="black" font-weight="bold">
                         PREVIEW
                    </p>
            </StyledText>
           </Watermark>
    </PDF>
   </DDX>
   ```

   Para obtener información sobre la personalización del aspecto, el texto y la alineación de la marca de agua, consulte Adición y eliminación de marcas de agua y fondos en la [Servicio de ensamblador y referencia DDX](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf) documento.

   >[!NOTE]
   >
   >En el archivo dx, las referencias a resultado y origen deben permanecer sin cambiar a output.pdf y input.pdf. El nombre del ddx del archivo tampoco debe cambiarse.

1. Haga clic en **Guardar todo**.
