---
title: Administrar recursos de vídeo
description: Cargar, previsualizar, anotar y publicar recursos de vídeo en [!DNL Adobe Experience Manager].
contentOwner: AG
role: Business Practitioner
feature: Asset Management
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 8%

---


# Administrar recursos de vídeo {#manage-video-assets}

El formato de vídeo es una parte fundamental de los recursos digitales de una organización. [!DNL Adobe Experience Manager] ofrece ofertas y funciones maduras para administrar todo el ciclo de vida de los recursos de vídeo tras su creación.

Obtenga información sobre cómo administrar y editar los recursos de vídeo en [!DNL Adobe Experience Manager Assets]. La codificación y transcodificación de vídeo, por ejemplo, la transcodificación FFmpeg, es posible mediante la integración [!DNL Dynamic Media].

## Cargar y previsualizar recursos de vídeo {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] genera vistas previas para recursos de vídeo con la extensión MP4. Si el formato del recurso no es MP4, instale el paquete FFmpeg para generar una vista previa. FFmpeg crea representaciones de vídeo de tipo OGG y MP4. Puede obtener una vista previa de las representaciones en la interfaz de usuario [!DNL Assets].

1. En la carpeta o subcarpetas de recursos digitales, vaya a la ubicación en la que desee agregar recursos digitales.
1. Para cargar el recurso, haga clic en **[!UICONTROL Create]** en la barra de herramientas y seleccione **[!UICONTROL Files]**. También puede arrastrar un archivo en la interfaz de usuario. Consulte [carga de recursos](manage-assets.md#uploading-assets) para obtener más información.
1. Para obtener una vista previa de un vídeo en la vista de tarjeta, haga clic en la opción **[!UICONTROL Reproducir]** ![reproducir](assets/do-not-localize/play.png) del recurso de vídeo. Puede pausar o reproducir vídeo solo en la vista de tarjeta. Las opciones [!UICONTROL Play] y [!UICONTROL Pause] no están disponibles en la vista de lista.

1. Para obtener una vista previa del vídeo en la página de detalles del recurso, haga clic en **[!UICONTROL Editar]** en la tarjeta. El vídeo se reproduce en el reproductor de vídeo nativo del explorador. Puede reproducir, pausar, controlar el volumen y hacer zoom en el vídeo hasta la pantalla completa.

   ![Controles de reproducción de vídeo](assets/video-playback-controls.png)

## Configuración para cargar recursos de más de 2 GB {#configuration-to-upload-assets-that-are-larger-than-gb}

De forma predeterminada, [!DNL Assets] no permite cargar ningún recurso que supere los 2 GB debido a un límite de tamaño de archivo. Sin embargo, puede sobrescribir este límite entrando en CRXDE Lite y creando un nodo en el directorio `/apps`. El nodo debe tener el mismo nombre de nodo, estructura de directorio y propiedades de nodo comparables de order.

Además de la configuración [!DNL Assets] , cambie las siguientes configuraciones para cargar recursos de gran tamaño:

* Aumente el tiempo de caducidad del token. Consulte [!UICONTROL Adobe Granite CSRF Servlet] en la Consola Web en `https://[aem_server]:[port]/system/console/configMgr`. Para obtener más información, consulte [Protección CSRF](/help/sites-developing/csrf-protection.md).
* Aumente el `receiveTimeout` en la configuración de Dispatcher. Para obtener más información, consulte [Configuración de Dispatcher Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options).

>[!NOTE]
>
>La interfaz de usuario de [!DNL Experience Manager] Classic no tiene una restricción de tamaño de archivo de 2 GB. Además, el flujo de trabajo completo para vídeo de gran tamaño no es totalmente compatible.

Para configurar un límite de tamaño de archivo más alto, realice los siguientes pasos en el directorio `/apps`.

1. En [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. En el CRXDE Lite, vaya a `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. Para ver la ventana del directorio, haga clic en `>>`.
1. En la barra de herramientas, haga clic en el **[!UICONTROL nodo de superposición]**. También puede seleccionar **[!UICONTROL Nodo de superposición]** en el menú contextual.
1. En el cuadro de diálogo **[!UICONTROL Nodo de superposición]**, haga clic en **[!UICONTROL Aceptar]**.

   ![Nodo de superposición](assets/overlay-node-path.png)

1. Actualice el explorador. El nodo de superposición `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` está seleccionado.
1. En la pestaña **[!UICONTROL Properties]**, introduzca el valor apropiado en bytes para aumentar el límite de tamaño al tamaño deseado. Por ejemplo, para aumentar el límite de tamaño a 30 GB, introduzca el valor `32212254720`.

1. En la barra de herramientas, haga clic en **[!UICONTROL Guardar todo]**.
1. En [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
1. En la página [!DNL Adobe Experience Manager] [!UICONTROL Paquetes de consola web], en la columna Nombre de la tabla, busque y haga clic en **[!UICONTROL Controlador de trabajo de proceso externo de Adobe Granite Workflow]**.
1. En la página [!UICONTROL Controlador de trabajo de proceso externo de Adobe Granite Workflow], establezca los segundos para los campos **[!UICONTROL Tiempo de espera predeterminado]** y **[!UICONTROL Tiempo de espera máximo]** en `18000` (cinco horas). Haga clic en **[!UICONTROL Guardar]**.
1. En [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página Modelos de flujo de trabajo , seleccione **[!UICONTROL Dynamic Media Codificar vídeo]** y haga clic en **[!UICONTROL Editar]**.
1. En la página de flujo de trabajo, haga doble clic en el componente **[!UICONTROL Dynamic Media Video Service Process]**.
1. En el cuadro de diálogo [!UICONTROL Propiedades del paso], en la pestaña **[!UICONTROL Común]**, expanda **Configuración avanzada**.
1. En el campo **[!UICONTROL Timeout]**, especifique un valor de `18000` y haga clic en **[!UICONTROL OK]** para volver a la página de flujo de trabajo **[!UICONTROL Dynamic Media Encode Video]**.
1. Cerca de la parte superior de la página, debajo del título de página [!UICONTROL Dynamic Media Encode Video], haga clic en **[!UICONTROL Guardar]**.

## Publicar recursos de vídeo {#publish-video-assets}

Después de la publicación, puede incluir los recursos de vídeo en una página web como URL o incrustar directamente los recursos. Para obtener más información, consulte [Publicar recursos de Dynamic Media](/help/assets/publishing-dynamicmedia-assets.md).

## Anotar recursos de vídeo {#annotate-video-assets}

1. En la consola [!DNL Assets], seleccione **[!UICONTROL Editar]** en la tarjeta de recursos para mostrar la página de detalles del recurso.
1. Para reproducir el vídeo, haga clic en **[!UICONTROL Preview]**.
1. Para realizar anotaciones en el vídeo, haga clic en **[!UICONTROL Anotar]**. Se añade una anotación en el momento (fotograma) concreto del vídeo. Al anotar, puede dibujar en el lienzo e incluir un comentario con el dibujo. Los comentarios se guardan automáticamente. Para salir del asistente de anotaciones, haga clic en **[!UICONTROL Cerrar]**.

   ![Dibujar y anotar en un marco de vídeo](assets/annotate-video.png)

1. Busque un punto específico en el vídeo, establezca el tiempo en segundos en el campo de **texto** y haga clic en **Saltar**. Por ejemplo, para omitir los primeros 20 segundos de vídeo, introduzca 20 en el campo de texto.

   ![Busque un momento en un vídeo para omitir en segundos especificados](assets/seek-in-video.png)

1. Para verla en la línea de tiempo, haga clic en una anotación. Para eliminar la anotación de la cronología, haga clic en **[!UICONTROL Eliminar]**.

   ![Ver anotaciones y los detalles en la cronología](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [Administrar recursos digitales en recursos de Experience Manager](/help/assets/manage-assets.md)
>* [Administrar colecciones en recursos de Experience Manager](/help/assets/manage-collections.md)
>* [Documentación de vídeo de Dynamic Media](/help/assets/video.md).

