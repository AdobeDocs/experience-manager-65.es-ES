---
title: FFmpeg para comunidades
seo-title: FFmpeg para comunidades
description: Cómo instalar y configurar FFmpeg para comunidades
seo-description: Cómo instalar y configurar FFmpeg para comunidades
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
translation-type: tm+mt
source-git-commit: 871c42ee000eb250c1c6159d9a0c752e8ed4d7b8
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 1%

---


# FFmpeg para comunidades {#ffmpeg-for-communities}

## Información general {#overview}

FFmpeg es una solución para convertir y transmitir audio y vídeo y, cuando se instala, se utiliza para la transcodificación correcta de [recursos de vídeo](../../help/sites-authoring/default-components-foundation.md#video), así como para la función de habilitación de Comunidades AEM.

FFmpeg se utiliza en el entorno del autor para obtener metadatos de los recursos de activación cargados, así como para generar una miniatura que se mostrará al enumerar el recurso de activación.

## Instalación de FFmpeg {#installing-ffmpeg}

FFmpeg debe estar instalado en los servidores que alojan las instancias de AEM *autor*.

1. Vaya a [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. Descargue la versión más reciente de FFmpeg para su entorno específico (Macintosh, Windows o Linux).

   * Es importante mantener FFmpeg actualizado debido a las vulnerabilidades de seguridad en versiones anteriores.

1. Instale FFmpeg siguiendo las instrucciones para el sistema operativo.

1. Asegúrese de que el ejecutable FFmpeg está establecido en la ruta del sistema.

   Debería poder ejecutar FFmpeg desde cualquier directorio del sistema.

   * Por ejemplo, `ffmpeg -version`.

## Configurar el servicio de transcodificación FFmpeg {#configure-ffmpeg-transcoding-service}

De forma predeterminada, cuando se instala FFmpeg, se configuran varias representaciones (transcodificaciones) según la definición del flujo de trabajo [!UICONTROL Recurso de actualización de DAM].

Dado que las transcodificaciones requieren un uso intensivo de CPU, se recomienda modificar la lista de las representaciones de destinatario. En la mayoría de los casos, la transcodificación no es necesaria.

Para modificar el flujo de trabajo [!UICONTROL Recurso de actualización de DAM] y, en este ejemplo, desactivar la transcodificación:

* Inicie sesión en la instancia de autor con privilegios administrativos.
* Desde la navegación global, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
* Busque **[!UICONTROL Recurso de actualización de DAM]**.
* Haga clic con el botón doble para abrir el flujo de trabajo y editarlo en la IU clásica.

   Ubicación resultante: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Haga clic con el botón doble en el paso **[!UICONTROL Transcodificación de FFmpeg]** para acceder al cuadro de diálogo Propiedades del paso.
* En la ficha **[!UICONTROL Proceso]**:

   * **[!UICONTROL Arumentos]**: Borre todas las entradas para desactivar la transcodificación Valores predeterminados:  `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![configure-ffmpeg](assets/configure-ffmpeg.png)

* Seleccione **[!UICONTROL Aceptar]** para cerrar el cuadro de diálogo `Step Properties`.

* Seleccione **[!UICONTROL Guardar]** para guardar el flujo de trabajo `DAM Update Asset`.



