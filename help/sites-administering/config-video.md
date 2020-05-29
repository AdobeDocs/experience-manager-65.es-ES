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
translation-type: tm+mt
source-git-commit: 071f4a292343f0ad52ca3700c95bf60f03c307cc
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Configuración del componente Vídeo {#configure-the-video-component}

El componente [](/help/sites-authoring/default-components-foundation.md#video) Vídeo le permite colocar un recurso de vídeo predefinido y listo para usar (OOTB) en la página.

Para que se produzca una transcodificación adecuada, un administrador instala FFmpeg por separado. Consulte [Instalación de FFmpeg y configuración de AEM](#install-ffmpeg). Administrators also [Configure Video Profiles](#configure-video-profiles) for use with HTML5 elements.

## Configuración de perfiles de vídeo {#configure-video-profiles}

Para utilizar elementos HTML5, defina definir perfiles de vídeo. Las que se eligen aquí se utilizan en orden. Para acceder, utilice el modo [](/help/sites-authoring/default-components-designmode.md) Diseño (solo en la IU clásica) y seleccione la ficha **[!UICONTROL Perfiles]** :

![chlimage_1-317](assets/chlimage_1-317.png)

Desde este cuadro de diálogo, también puede configurar el diseño del componente Vídeo y los parámetros para [!UICONTROL Reproducción], [!UICONTROL Flash]y [!UICONTROL Avanzado].

## Instalación de FFmpeg y configuración de AEM {#install-ffmpeg}

El componente Vídeo depende del producto de código abierto de terceros FFmpeg para la transcodificación de vídeos. Descargado desde [https://ffmpeg.org/](https://ffmpeg.org/). Después de instalar FFmpeg, configure AEM para que utilice un códec de audio específico y opciones de tiempo de ejecución específicas.

Para instalar FFmpeg en **Windows**, siga estos pasos:

1. Descargue el binario compilado como `ffmpeg.zip`.
1. Desarchivar en una carpeta.
1. Configure la variable de entorno del sistema `PATH` como &lt;*your-ffmpeg-location*>`\bin`.
1. Reinicie AEM.

Para instalar FFmpeg en **Mac OS X**, siga estos pasos:

1. Instale Xcode disponible en [developer.apple.com/xcode](hhttps://developer.apple.com/xcode/).
1. Instale en [XQuartz](https://www.xquartz.org) para obtener [X11](https://support.apple.com/en-us/HT201341).
1. Instale MacPorts en [www.macports.org](https://www.macports.org/).
1. En la consola, ejecute `sudo port install ffmpeg` y siga las instrucciones que aparecen en pantalla. Asegúrese de que la ruta del `FFmpeg` ejecutable se agrega a la variable `PATH` del sistema.

Para instalar FFmpeg en **Mac OS X 10.6**, con la versión precompilada, siga estos pasos:

1. Descargue la versión precompilada.
1. Desarchivarla en el `/usr/local` directorio.
1. En la consola, ejecute `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`. Cambie las rutas según corresponda.

Para **configurar AEM**, siga estos pasos:

>[!NOTE]
>
>Estos pasos sólo son necesarios si se requiere una mayor personalización de los códecs.

1. Open [!UICONTROL CRXDE Lite] in your web browser. Acceda a [http://localhost:4502/crx/de](http://localhost:4502/crx/de).
2. Seleccione el `/libs/settings/dam/video/format_aac/jcr:content` nodo y asegúrese de que las propiedades del nodo son las siguientes:

   * `audioCodec` es `aac`.
   * `customArgs` es `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. Para personalizar la configuración, cree una superposición en el `/apps/settings/` nodo y mueva la misma estructura debajo `/conf/global/settings/` del nodo. No se puede editar en el `/libs` nodo. Por ejemplo, para superponer una ruta `/libs/settings/dam/video/fullhd-bp`, créela en `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >Superponga y edite todo el nodo de perfil y no sólo la propiedad que necesita modificación. Estos recursos no se resuelven mediante SlingResourceMerger.

4. If you changed either of the properties, click **[!UICONTROL Save All]**.

>[!NOTE]
>
>Los cambios en los modelos de flujo de trabajo predeterminados (OOTB) no se conservan al actualizar la instancia de AEM. Adobe recomienda copiar los modelos de flujo de trabajo modificados antes de editarlos. Por ejemplo, copie el modelo [!UICONTROL DAM Update Asset] OOTB antes de editar el paso Transcodificación FFmpeg en el modelo [!UICONTROL DAM Update Asset] para elegir los nombres de perfiles de vídeo que existían antes de la actualización. A continuación, puede superponer el `/apps` nodo para permitir que AEM recupere los cambios personalizados del modelo OOTB.
