---
title: FFmpeg para comunidades
seo-title: FFmpeg for Communities
description: Cómo instalar y configurar FFmpeg para Communities
seo-description: How to install and configure FFmpeg for Communities
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# FFmpeg para comunidades {#ffmpeg-for-communities}

## Información general {#overview}

FFmpeg es una solución para la conversión y transmisión de audio y vídeo y, cuando está instalado, se utiliza para la transcodificación adecuada de [recursos de vídeo](../../help/sites-authoring/default-components-foundation.md#video).

## Instalación de FFmpeg {#installing-ffmpeg}

AEM FFmpeg debe instalarse en los servidores que alojan la red de distribución de la red de distribución de la *autor* instancia(s).

1. Ir a [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. Descargue la última versión de FFmpeg para su entorno específico (Macintosh, Windows o Linux).

   * Es importante mantener FFmpeg actualizado debido a las vulnerabilidades de seguridad de las versiones anteriores.

1. Instale FFmpeg siguiendo las instrucciones para el sistema operativo.

1. Asegúrese de que el ejecutable FFmpeg esté establecido en la ruta del sistema.

   Debe poder ejecutar FFmpeg desde cualquier directorio del sistema.

   * Por ejemplo, `ffmpeg -version`.

## Configurar servicio de transcodificación FFmpeg {#configure-ffmpeg-transcoding-service}

De forma predeterminada, cuando FFmpeg está instalado, se configuran varias representaciones (transcodificaciones) según el [!UICONTROL Recurso de actualización DAM] definición de flujo de trabajo.

Como las transcodificaciones hacen un uso intensivo de la CPU, se recomienda modificar la lista de representaciones de destino. En la mayoría de los casos, la transcodificación no es necesaria.

Para modificar [!UICONTROL Recurso de actualización DAM] flujo de trabajo y, en este ejemplo, para desactivar la transcodificación:

* Inicie sesión en la instancia de autor con privilegios administrativos.
* En la navegación global, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
* Localizar **[!UICONTROL Recurso de actualización DAM]**.
* Haga doble clic para abrir el flujo de trabajo y editarlo en la IU clásica.

   Ubicación resultante: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Haga doble clic en **[!UICONTROL Transcodificación FFmpeg]** para acceder al cuadro de diálogo Propiedades del paso.
* En el **[!UICONTROL Proceso]** pestaña:

   * **[!UICONTROL Argumentos]**: borre todas las entradas para deshabilitar la transcodificación. Valores predeterminados: `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![configure-ffmpeg](assets/configure-ffmpeg.png)

* Seleccionar **[!UICONTROL OK]** para cerrar el `Step Properties` diálogo.

* Seleccionar **[!UICONTROL Guardar]** para guardar `DAM Update Asset` flujo de trabajo.
