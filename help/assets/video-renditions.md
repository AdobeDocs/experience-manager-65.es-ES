---
title: Representaciones de vídeo
description: Representaciones de vídeo
uuid: a02f9ec1-30d9-4cbb-8746-8391ac614f0a
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 1601b473-7227-4a56-bb7c-289de2987e4b
translation-type: tm+mt
source-git-commit: 66f46a34832254af74c72da16ec8ebe3eb8cd46d

---


# Video renditions {#video-renditions}

Recursos Adobe Experience Manager (AEM) genera representaciones de vídeo para recursos de vídeo de varios formatos, incluidos OGG, FLV, etc.

Recursos AEM admite representaciones estáticas y dinámicas (representaciones con codificación DM) para recursos multimedia.

Las representaciones estáticas se generan de forma nativa utilizando FFMPEG (instalado y disponible en la ruta del sistema) y se almacenan en el repositorio de contenido.

Las representaciones con codificación DM se almacenan en el servidor proxy y se sirven en tiempo de ejecución.

Los recursos de AEM admiten la reproducción de estas representaciones en el lado del cliente.

Para ver las representaciones de un recurso de vídeo concreto, abra su página de recursos y toque el icono de navegación global. A continuación, seleccione **[!UICONTROL Representaciones]** en la lista.

![chlimage_1-478](assets/chlimage_1-478.png)

La lista de representaciones de vídeo se muestra en el panel **[!UICONTROL Representaciones]** .

![chlimage_1-479](assets/chlimage_1-479.png)

Para configurar el servidor proxy para las representaciones con codificación DM, [configure los servicios de Dynamic Media Cloud.](config-dynamic.md)

Para generar representaciones de vídeo con parámetros deseados, [cree un perfil](video-profiles.md)de vídeo correspondiente.

Después de configurar el servidor proxy y crear perfiles de vídeo, puede incluir este ajuste preestablecido de vídeo en un perfil de procesamiento y aplicar el perfil de procesamiento a una carpeta.

>[!NOTE]
>
>La reproducción de audio no funciona para archivos OGG y WAV en Microsoft Internet Explorer 11. Se `Invalid Source` muestra un error en la página de detalles de recursos para los recursos con la extensión OGG o WAV.
>
>En MS Edge y iPad, los archivos OGG no se reproducen y generan un error de formato no admitido.
