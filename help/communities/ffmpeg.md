---
title: FFmpeg para comunidades
description: Cómo instalar y configurar FFmpeg para Communities
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
solution: Experience Manager
feature: Communities
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 1%
---
# FFmpeg para comunidades {#ffmpeg-for-communities}

## Información general {#overview}

FFmpeg es una solución para convertir y transmitir audio y vídeo y, cuando se instala, se usa para transcodificar correctamente [recursos de vídeo](../../help/sites-authoring/default-components-foundation.md#video).

## Instalación de FFmpeg {#installing-ffmpeg}

FFmpeg debe instalarse en los servidores que hospedan las instancias de AEM *author*.

1. Vaya a [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. Descargue la última versión de FFmpeg para su entorno específico (Macintosh, Windows o Linux).

   * Es importante mantener FFmpeg actualizado debido a las vulnerabilidades de seguridad de las versiones anteriores.

1. Instale FFmpeg siguiendo las instrucciones para el sistema operativo.

1. Asegúrese de que el ejecutable FFmpeg esté establecido en la ruta del sistema.

   Debe poder ejecutar FFmpeg desde cualquier directorio del sistema.

   * Por ejemplo, `ffmpeg -version`.

## Configurar servicio de transcodificación FFmpeg {#configure-ffmpeg-transcoding-service}

De forma predeterminada, cuando FFmpeg está instalado, se configuran varias representaciones (transcodificaciones) según la definición del flujo de trabajo [!UICONTROL DAM Update Asset].

Como las transcodificaciones hacen un uso intensivo de CPU, se recomienda modificar la lista de representaciones de destinatario. En la mayoría de los casos, la transcodificación no es necesaria.

Para modificar el flujo de trabajo [!UICONTROL DAM Update Asset] y, en este ejemplo, para desactivar la transcodificación:

* Inicie sesión en la instancia de autor con privilegios administrativos.
* En la navegación global, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
* Busque **[!UICONTROL recurso de actualización DAM]**.
* Haga doble clic para abrir el flujo de trabajo y editarlo en la IU clásica.

  Ubicación resultante: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Haga doble clic en el paso **[!UICONTROL FFmpeg transcoding]** para acceder al cuadro de diálogo Propiedades del paso.
* En la ficha **[!UICONTROL Proceso]**:

  * **[!UICONTROL Argumentos]**: borre todas las entradas para deshabilitar la transcodificación Valores predeterminados: `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

  ![configure-ffmpeg](assets/configure-ffmpeg.png)

* Seleccione **[!UICONTROL Aceptar]** para cerrar el cuadro de diálogo `Step Properties`.

* Seleccione **[!UICONTROL Guardar]** para guardar el flujo de trabajo `DAM Update Asset`.
