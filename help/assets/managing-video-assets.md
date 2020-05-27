---
title: Administrar recursos de vídeo
description: Obtenga información sobre cómo cargar, previsualización, realizar anotaciones y publicar recursos de vídeo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 11%

---


# Administrar recursos de vídeo {#manage-video-assets}

Obtenga información sobre cómo administrar y editar los recursos de vídeo en Recursos Adobe Experience Manager. Además, si tiene licencia para usar Dynamic Media, consulte la documentación [de vídeo de](/help/assets/video.md)Dynamic Media.

## Carga y previsualización de recursos de vídeo {#upload-and-preview-video-assets}

Recursos Adobe Experience Manager genera previsualizaciones para recursos de vídeo con la extensión MP4. Si el formato del recurso no es MP4, instale el paquete FFmpeg para generar una previsualización. FFmpeg crea representaciones de vídeo de tipo OGG y MP4. Puede realizar la previsualización de estas representaciones en la interfaz de usuario de Recursos.

1. En la carpeta o subcarpetas de recursos digitales, navegue a la ubicación donde desee agregar recursos digitales.
1. Para cargar el recurso, haga clic en **[!UICONTROL Crear]** en la barra de herramientas y, a continuación, elija **[!UICONTROL Archivos]**. Como alternativa, suéltela directamente en el área de recursos. Consulte [Carga de recursos](managing-assets-touch-ui.md#uploading-assets) para obtener más información sobre la operación de carga.
1. Para previsualización de un vídeo en la vista de tarjeta, haga clic en el botón **[!UICONTROL Reproducir]** del recurso de vídeo.

   ![chlimage_1-65](assets/chlimage_1-201.png)

   Puede pausar o reproducir vídeo solo en la vista de la tarjeta. Los botones [!UICONTROL Reproducir] y [!UICONTROL Pausa] no están disponibles en la vista de lista.

1. Para previsualización del vídeo en la página de detalles del recurso, haga clic en el icono **[!UICONTROL Editar]** de la tarjeta.

   El vídeo se reproduce en el reproductor de vídeo nativo del navegador. Puede reproducir, pausar, controlar el volumen y aplicar zoom en el vídeo a pantalla completa.

   ![chlimage_1-66](assets/chlimage_1-202.png)

## Configuración para cargar recursos de más de 2 GB {#configuration-to-upload-assets-that-are-larger-than-gb}

De forma predeterminada, Experience Manager Assets no permite cargar recursos que superen los 2 GB debido a un límite de tamaño de archivo. Sin embargo, puede sobrescribir este límite si ingresa a CRXDE Lite y crea un nodo en el `/apps` directorio. El nodo debe tener el mismo nombre de nodo, estructura de directorio y propiedades de nodo comparables de order.

Además de la configuración de Experience Manager Assets, cambie las configuraciones siguientes para cargar recursos de gran tamaño:

* Aumente el tiempo de caducidad del token. Consulte [!UICONTROL Adobe Granite CSRF Servlet] en la consola web en `https://[aem_server]:[port]/system/console/configMgr`. Para obtener más información, consulte Protección [de](/help/sites-developing/csrf-protection.md)CSRF.
* Aumente la `receiveTimeout` configuración de Dispatcher. Para obtener más información, consulte Configuración [de](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options)Experience Manager Dispatcher.

>[!NOTE]
>
>La interfaz de usuario de Experience Manager Classic no tiene una restricción de tamaño de archivo de 2 GB. Además, el flujo de trabajo de extremo a extremo para vídeos de gran tamaño no es totalmente compatible.

Para configurar un límite de tamaño de archivo mayor, realice los siguientes pasos en el `/apps` directorio.

1. En Experience Manager, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. En CRXDE Lite, vaya a `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. Para ver la ventana del directorio, toque el `>>` icono .
1. From the toolbar, click the **[!UICONTROL Overlay Node]**. También puede seleccionar **[!UICONTROL Nodo de superposición]** en el menú contextual.
1. In the **[!UICONTROL Overlay Node]** dialog, click **[!UICONTROL OK]**.

   ![chlimage_1-67](assets/chlimage_1-203.png)

1. Actualice el explorador. El nodo de superposición `/jcr_root/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` está seleccionado.
1. En la ficha **[!UICONTROL Propiedades]** , introduzca el valor apropiado en bytes para aumentar el límite de tamaño al tamaño deseado. Por ejemplo, para aumentar el límite de tamaño a 30 GB, escriba `{sizeLimit : "32212254720"}` value.

1. En la barra de herramientas, toque **[!UICONTROL Guardar todo]**.
1. En Experience Manager, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > Consola **** web.
1. En la página Paquetes de la consola web de Adobe Experience Manager, en la columna Nombre de la tabla, busque y haga clic en **[!UICONTROL Adobe Granite Workflow External Process Job Handler]**.
1. En la página Controlador de trabajos de proceso externo de Adobe Granite Workflow, establezca los segundos para los campos **[!UICONTROL Tiempo de espera predeterminado]** y **[!UICONTROL Tiempo de espera máximo]** en `18000` (cinco horas).
1. Haga clic en **[!UICONTROL Guardar]**.
1. En Experience Manager, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página Modelos de flujo de trabajo, seleccione **[!UICONTROL Dynamic Media Encode Video]** y, a continuación, haga clic en **[!UICONTROL Editar]**.
1. En la página de flujo de trabajo, haga clic con el botón doble en el componente Proceso **[!UICONTROL del servicio de vídeo de medios]** dinámicos.
1. En el cuadro de diálogo [!UICONTROL Propiedades del paso], en la pestaña **[!UICONTROL Común]**, expanda **Configuración avanzada**.
1. In the **[!UICONTROL Timeout]** field, specify a value of `18000`, then click **[!UICONTROL OK]** to return to the **[!UICONTROL Dynamic Media Encode Video]** workflow page.
1. Cerca de la parte superior de la página, debajo del título de la página de codificación de vídeo de Dynamic Media, haga clic en **[!UICONTROL Guardar]**.

## Publicación de recursos de vídeo {#publish-video-assets}

Una vez publicados los recursos de vídeo, estarán disponibles para incluirlos en una página web mediante una URL o incrustarlos en una página web. Consulte [Publicación de recursos](/help/assets/publishing-dynamicmedia-assets.md).

## Anotación de recursos de vídeo {#annotate-video-assets}

1. En la consola Recursos, haga clic en el icono [!UICONTROL Editar] de la tarjeta de recursos para mostrar la página de detalles de recursos.
1. Para reproducir el vídeo, haga clic en el icono de [!UICONTROL Previsualización] .
1. Para realizar anotaciones en el vídeo, haga clic en el botón **[!UICONTROL Anotar]** . Se agrega una anotación en el punto de tiempo (fotograma) concreto del vídeo. Al realizar anotaciones, puede dibujar en el lienzo e incluir un comentario con el dibujo. Los comentarios se guardan automáticamente.

   ![chlimage_1-68](assets/chlimage_1-204.png)

   Para salir del asistente para anotaciones, haga clic en **[!UICONTROL Cerrar]**.

1. Busque un punto específico en el vídeo, establezca el tiempo en segundos en el campo de **texto** y haga clic en **Saltar**. Por ejemplo, para omitir los primeros 10 segundos de vídeo, introduzca 20 en el campo de texto.

   ![chlimage_1-69](assets/chlimage_1-205.png)

1. Para vista en la línea de tiempo, haga clic en una anotación. Para eliminar la anotación de la línea de tiempo, haga clic en **[!UICONTROL Eliminar]**.

   ![chlimage_1-70](assets/chlimage_1-206.png)
