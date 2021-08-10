---
title: Representaciones de vídeo
description: Representaciones de vídeo
uuid: a02f9ec1-30d9-4cbb-8746-8391ac614f0a
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 1601b473-7227-4a56-bb7c-289de2987e4b
exl-id: a644558e-5be9-4ba2-b560-fc300497fbdf
source-git-commit: 77687a0674b939460bd34011ee1b94bd4db50ba4
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# Representaciones de vídeo {#video-renditions}

Adobe Experience Manager Assets genera representaciones de vídeo para recursos de vídeo de varios formatos, incluidos OGG, FLV, etc.

Recursos de Experience Manager admite representaciones estáticas y dinámicas (representaciones con codificación DM) para recursos de medios.

Las representaciones estáticas se generan de forma nativa utilizando FFMPEG (instalado y disponible en la ruta del sistema) y se almacenan en el repositorio de contenido.

Las representaciones con codificación DM se almacenan en el servidor proxy y se proporcionan durante la ejecución.

Los recursos de Experience Manager son compatibles con la reproducción de estas representaciones en el lado del cliente.

Para ver las representaciones de un recurso de vídeo concreto, abra su página de recursos y seleccione el icono Navegación global . A continuación, elija **[!UICONTROL Representaciones]** en la lista.

![chlimage_1-478](assets/chlimage_1-478.png)

La lista de representaciones de vídeo se muestra en el panel **[!UICONTROL Representaciones]**.

![chlimage_1-479](assets/chlimage_1-479.png)

Para configurar el servidor proxy para las representaciones con codificación DM, [configure los servicios de Dynamic Media Cloud](config-dynamic.md).

Para generar representaciones de vídeo con los parámetros deseados, [cree un perfil de vídeo correspondiente](video-profiles.md).

Después de configurar el servidor proxy y crear perfiles de vídeo, puede incluir este ajuste preestablecido de vídeo en un perfil de procesamiento y aplicar el perfil de procesamiento a una carpeta.

>[!NOTE]
>
>La reproducción de audio no funciona para archivos OGG y WAV en Microsoft® Internet Explorer 11. Aparece un error `Invalid Source` en la página de detalles del recurso para los recursos con la extensión OGG o WAV.
>
>En MS® Edge y iPad, los archivos OGG no se reproducen y generan un error de formato no admitido.
