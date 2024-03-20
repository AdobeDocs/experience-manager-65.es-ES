---
title: Representaciones de vídeo
description: Aprenda a utilizar Adobe Experience Manager Assets para generar representaciones de vídeo para recursos de vídeo de varios formatos, incluidos OGG, FLV, etc.
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
exl-id: a644558e-5be9-4ba2-b560-fc300497fbdf
solution: Experience Manager, Experience Manager Assets
feature: Video
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# Representaciones de vídeo {#video-renditions}

Adobe Experience Manager Assets genera representaciones de vídeo para recursos de vídeo de varios formatos, incluidos OGG, FLV, etc.

Experience Manager Assets admite representaciones estáticas y dinámicas (representaciones codificadas en DM) para recursos de medios.

Las representaciones estáticas se generan de forma nativa mediante FFMPEG (instalado y disponible en la ruta del sistema) y se almacenan en el repositorio de contenido.

Las representaciones codificadas en DM se almacenan en el servidor proxy y se proporcionan durante la ejecución.

Experience Manager Assets proporciona compatibilidad de reproducción para estas representaciones en el lado del cliente.

Para ver las representaciones de un recurso de vídeo concreto, abra su página de recursos y seleccione el icono Navegación global. A continuación, elija **[!UICONTROL Representaciones]** de la lista.

![chlimage_1-478](assets/chlimage_1-478.png)

La lista de representaciones de vídeo se muestra en la **[!UICONTROL Representaciones]** panel.

![chlimage_1-479](assets/chlimage_1-479.png)

Para configurar el servidor proxy para representaciones con codificación DM, [configurar Dynamic Media Cloud Services](config-dynamic.md).

Para generar representaciones de vídeo con los parámetros deseados, [crear un perfil de vídeo correspondiente](video-profiles.md).

Después de configurar el servidor proxy y crear perfiles de vídeo, puede incluir este ajuste preestablecido de vídeo en un perfil de procesamiento y aplicar el perfil de procesamiento a una carpeta.

>[!NOTE]
>
>La reproducción de audio no funciona para archivos OGG y WAV en Microsoft® Internet Explorer 11. Un error `Invalid Source` se muestra en la página de detalles del recurso para los recursos con extensión OGG o WAV.
>
>En MS® Edge y iPad, los archivos OGG no se reproducen y generan un error de formato no admitido.
