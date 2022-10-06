---
title: FFmpeg para Comunidades
seo-title: FFmpeg for Communities
description: Instalación y configuración de FFmpeg para Communities
seo-description: How to install and configure FFmpeg for Communities
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 1%

---

# FFmpeg para Comunidades {#ffmpeg-for-communities}

## Información general {#overview}

FFmpeg es una solución para convertir y transmitir audio y vídeo y, cuando se instala, se utiliza para una transcodificación adecuada de [recursos de vídeo](../../help/sites-authoring/default-components-foundation.md#video) así como para la función de habilitación de Comunidades AEM.

FFmpeg se utiliza en el entorno de creación para obtener metadatos para los recursos de habilitación cargados, así como para generar una miniatura que se mostrará al enumerar el recurso de habilitación.

## Instalación de FFmpeg {#installing-ffmpeg}

FFmpeg debe instalarse en los servidores que alojen el AEM *author* instancias.

1. Vaya a [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. Descargue la versión más reciente de FFmpeg para su entorno específico (Macintosh, Windows o Linux).

   * Es importante mantener FFmpeg actualizado debido a las vulnerabilidades de seguridad en versiones anteriores.

1. Instale FFmpeg siguiendo las instrucciones para el sistema operativo.

1. Asegúrese de que el ejecutable de FFmpeg esté configurado en la ruta del sistema.

   Debe poder ejecutar FFmpeg desde cualquier directorio de su sistema.

   * Por ejemplo, `ffmpeg -version`.

## Configurar el servicio de transcodificación FFmpeg {#configure-ffmpeg-transcoding-service}

De forma predeterminada, cuando se instala FFmpeg, se configuran varias representaciones (transcodificaciones) según la variable [!UICONTROL Recurso de actualización DAM] definición del flujo de trabajo.

Como las transcodificaciones requieren gran cantidad de CPU, se recomienda modificar la lista de representaciones de destino. En la mayoría de los casos, la transcodificación no es necesaria.

Para modificar el [!UICONTROL Recurso de actualización DAM] flujo de trabajo y, en este ejemplo, para desactivar la transcodificación:

* Inicie sesión en la instancia de autor con privilegios administrativos.
* Desde la navegación global, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
* Localizar **[!UICONTROL Recurso de actualización DAM]**.
* Haga doble clic para abrir el flujo de trabajo y editarlo en la IU clásica.

   Ubicación resultante: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Haga doble clic en el botón **[!UICONTROL Transcodificación FFmpeg]** para acceder al cuadro de diálogo Propiedades del paso .
* En el **[!UICONTROL Proceso]** pestaña:

   * **[!UICONTROL Arumentos]**: Borre todas las entradas para desactivar la transcodificación Valores predeterminados: `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![configure-ffmpeg](assets/configure-ffmpeg.png)

* Select **[!UICONTROL OK]** para cerrar el `Step Properties` diálogo.

* Select **[!UICONTROL Guardar]** para guardar la variable `DAM Update Asset` flujo de trabajo.
