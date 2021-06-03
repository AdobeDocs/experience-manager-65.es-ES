---
title: Configuración del componente Vídeo
seo-title: Configuración del componente Vídeo
description: Obtenga información sobre cómo configurar el componente de vídeo.
seo-description: Obtenga información sobre cómo configurar el componente de vídeo.
uuid: f4755a13-08ea-4096-a951-46a590f8d766
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: a1efef3c-0e4b-4a17-bcad-e3cc17adbbf7
exl-id: 9c97f99e-d6ef-4817-8b2a-201ab22f2b38
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 2%

---

# Configuración del componente Vídeo {#configure-the-video-component}

El [componente Vídeo](/help/sites-authoring/default-components-foundation.md#video) permite colocar un recurso de vídeo predefinido y listo para usar (OOTB) en la página.

Para que se produzca la transcodificación adecuada, un administrador instala FFmpeg por separado. Consulte [Instalar FFmpeg y configurar AEM](#install-ffmpeg). Los administradores también [configuran perfiles de vídeo](#configure-video-profiles) para utilizarlos con elementos HTML5.

>[!CAUTION]
>
>Este componente de base ya no se utiliza. Adobe recomienda aprovechar el [Componente incrustado de componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/embed.html) en su lugar.

>[!CAUTION]
>
>Ya no se espera que este componente funcione de forma predeterminada sin una amplia personalización a nivel de proyecto.

## Configuración de perfiles de vídeo {#configure-video-profiles}

Para utilizar elementos HTML5, defina perfiles de vídeo. Los elegidos aquí se utilizan en orden. Para acceder, utilice [Design Mode](/help/sites-authoring/default-components-designmode.md) (solo IU clásica) y seleccione la pestaña **[!UICONTROL Profiles]**:

![chlimage_1-317](assets/chlimage_1-317.png)

Desde este cuadro de diálogo, también puede configurar el diseño del componente Vídeo y los parámetros para [!UICONTROL Reproducción], [!UICONTROL Flash] y [!UICONTROL Avanzadas].

## Instale FFmpeg y configure AEM {#install-ffmpeg}

El componente Vídeo se basa en el producto de terceros de código abierto FFmpeg para la transcodificación de vídeos. Descargado desde [https://ffmpeg.org/](https://ffmpeg.org/). Después de instalar FFmpeg, configure AEM para utilizar un códec de audio específico y opciones específicas de tiempo de ejecución.

Para instalar FFmpeg en **Windows**, siga estos pasos:

1. Descargue el binario compilado como `ffmpeg.zip`.
1. Desarchivar en una carpeta.
1. Establezca la variable de entorno del sistema `PATH` en &lt;*your-ffmpeg-location*>`\bin`.
1. Reinicie AEM.

Para instalar FFmpeg en **Mac OS X**, siga estos pasos:

1. Instale Xcode disponible en [developer.apple.com/xcode](https://developer.apple.com/xcode/).
1. Instale disponible en [XQuartz](https://www.xquartz.org) para obtener [X11](https://support.apple.com/en-us/HT201341).
1. Instale MacPorts disponibles en [www.macports.org](https://www.macports.org/).
1. En la consola, ejecute el comando `sudo port install ffmpeg` y siga las instrucciones que aparecen en la pantalla. Asegúrese de que la ruta del ejecutable `FFmpeg` se agrega a la variable del sistema `PATH`.

Para instalar FFmpeg en **Mac OS X 10.6**, con la versión precompilada, siga estos pasos:

1. Descargue la versión precompilada.
1. Desarchivarlo en el directorio `/usr/local`.
1. En la consola, ejecute `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`. Cambie las rutas según corresponda.

Para **configurar AEM**, siga estos pasos:

>[!NOTE]
>
>Estos pasos solo son necesarios si se requiere una mayor personalización de los códecs.

1. Abra [!UICONTROL CRXDE Lite] en el explorador web. Acceda a [http://localhost:4502/crx/de](http://localhost:4502/crx/de).
2. Seleccione el nodo `/libs/settings/dam/video/format_aac/jcr:content` y asegúrese de que las propiedades del nodo son las siguientes:

   * `audioCodec` es  `aac`.
   * `customArgs` es  `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. Para personalizar la configuración, cree una superposición en el nodo `/apps/settings/` y mueva la misma estructura en el nodo `/conf/global/settings/`. No se puede editar en el nodo `/libs`. Por ejemplo, para superponer la ruta `/libs/settings/dam/video/fullhd-bp`, créela en `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >Superponga y edite todo el nodo de perfil y no solo la propiedad que necesita modificación. Estos recursos no se resuelven mediante SlingResourceMerger.

4. Si ha cambiado cualquiera de las propiedades, haga clic en **[!UICONTROL Guardar todo]**.

>[!NOTE]
>
>Los cambios en los modelos de flujo de trabajo predeterminados (OOTB) no se conservan al actualizar la instancia de AEM. Adobe recomienda copiar los modelos de flujo de trabajo modificados antes de editarlos. Por ejemplo, copie el modelo OOTB [!UICONTROL DAM Update Asset] antes de editar el paso de transcodificación FFmpeg en el modelo [!UICONTROL DAM Update Asset] para elegir los nombres de perfil de vídeo que existían antes de la actualización. A continuación, puede superponer el nodo `/apps` para permitir AEM recupere los cambios personalizados del modelo OOTB.
