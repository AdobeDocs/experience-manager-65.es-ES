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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración del componente Vídeo {#configure-the-video-component}

El componente [](/help/sites-authoring/default-components-foundation.md#video) Vídeo le permite colocar un elemento de vídeo predefinido y listo para usar (OOTB) en la página.

Para que se produzca una transcodificación adecuada, el administrador debe [instalar FFmpeg y configurar AEM](#install-ffmpeg) por separado. También pueden [Configurar los perfiles de su vídeo](#configure-video-profiles) para utilizarlos con elementos HTML5.

## Configuración de perfiles de vídeo {#configure-video-profiles}

Puede que desee definir perfiles de vídeo para utilizarlos en elementos HTML5. Las que se eligen aquí se utilizan en orden. Para acceder, utilice el modo [](/help/sites-authoring/default-components-designmode.md) Diseño (solo en la IU clásica) y seleccione la ficha **[!UICONTROL Perfiles]** :

![chlimage_1-317](assets/chlimage_1-317.png)

También puede configurar el diseño de los componentes y parámetros de vídeo para [!UICONTROL Reproducción], [!UICONTROL Flash]y [!UICONTROL Avanzado].

## Instalación de FFmpeg y configuración de AEM {#install-ffmpeg}

The Video Component relies on the third-party open-source product FFmpeg for proper transcoding of videos that can be downloaded from [https://ffmpeg.org/](https://ffmpeg.org/). Después de instalar FFmpeg, debe configurar AEM para que utilice un códec de audio específico y opciones de tiempo de ejecución específicas.

**Para instalar FFmpeg para su plataforma**:

* **En Windows:**

   1. Descargar el binario compilado como `ffmpeg.zip`
   1. Descomprima en una carpeta.
   1. Configure la variable de entorno del sistema `PATH` en `<*your-ffmpeg-locatio*n>\bin`
   1. Reinicie AEM.

* **En Mac OS X:**

   1. Instalar Xcode ([https://developer.apple.com/technologies/tools/xcode.html](https://developer.apple.com/technologies/tools/xcode.html))
   1. Instale XQuartz/X11.
   1. Instalación de MacPorts ([https://www.macports.org/](https://www.macports.org/))
   1. En la consola, ejecute el siguiente comando y siga las instrucciones:

      `sudo port install ffmpeg`

      `FFmpeg` debe estar en `PATH` para que AEM pueda recogerlo a través de la línea de comandos.

* **Uso de la versión precompilada para OS X 10.6:**

   1. Descargue la versión precompilada.
   1. Extract it to the `/usr/local` directory.
   1. Desde terminal, ejecute:

      `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`

**Para configurar AEM**:

1. Open [!UICONTROL CRXDE Lite] in your web browser. ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))
1. Seleccione el `/libs/settings/dam/video/format_aac/jcr:content` nodo y asegúrese de que las propiedades del nodo son las siguientes:

   * audioCodec:

      ```
       aac
      ```

   * customArgs:

      ```
       -flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8
      ```

1. Para personalizar la configuración, cree una superposición en el `/apps/settings/` nodo y mueva la misma estructura debajo `/conf/global/settings/` del nodo. No se puede editar en el `/libs` nodo. Por ejemplo, para superponer una ruta `/libs/settings/dam/video/fullhd-bp`, créela en `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >Superponga y edite todo el nodo de perfil y no solo la propiedad que necesita modificación. Estos recursos no se resuelven mediante SlingResourceMerger.

1. If you changed either of the properties, click **[!UICONTROL Save All]**.

>[!NOTE]
>
>Los modelos de flujo de trabajo de OOTB no se conservan al actualizar la instancia de AEM. Adobe recomienda copiar modelos de flujo de trabajo de OOTB antes de editarlos. Por ejemplo, copie el modelo de activos de actualización de DAM de OOTB antes de editar el paso de transcodificación de FFmpeg en el modelo de recursos de actualización de DAM para elegir los nombres de perfil de vídeo que existían antes de la actualización. A continuación, puede superponer el `/apps` nodo para permitir que AEM recupere los cambios personalizados del modelo OOTB.

