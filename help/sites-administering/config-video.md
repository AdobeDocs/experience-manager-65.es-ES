---
title: Configuración del componente de vídeo
seo-title: Configure the Video component
description: Obtenga información sobre cómo configurar el componente de vídeo.
seo-description: Learn how to configure the Video Component.
uuid: f4755a13-08ea-4096-a951-46a590f8d766
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: a1efef3c-0e4b-4a17-bcad-e3cc17adbbf7
exl-id: 9c97f99e-d6ef-4817-8b2a-201ab22f2b38
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# Configuración del componente de vídeo {#configure-the-video-component}

El [Componente de vídeo](/help/sites-authoring/default-components-foundation.md#video) le permite colocar un recurso de vídeo predefinido y listo para usar (OOTB) en la página.

Para que se produzca la transcodificación adecuada, un administrador instala FFmpeg por separado. Consulte [AEM Instalación de FFmpeg y configuración de la](#install-ffmpeg). Los administradores también [Configuración de perfiles de vídeo](#configure-video-profiles) para su uso con elementos de HTML5.

>[!CAUTION]
>
>Este componente de base se ha desaprobado. Adobe recomienda aprovechar el [Componente incrustado de componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/embed.html) en su lugar.

>[!CAUTION]
>
>Ya no se espera que este componente funcione de forma predeterminada sin una amplia personalización en el nivel de proyecto.

## Configuración de perfiles de vídeo {#configure-video-profiles}

Para utilizar los elementos de HTML5, defina los perfiles de vídeo. Los elegidos aquí se utilizan por orden. Para acceder a, utilice [Modo de diseño](/help/sites-authoring/default-components-designmode.md) (Solo IU clásica) y seleccione la **[!UICONTROL Perfiles]** pestaña:

![chlimage_1-317](assets/chlimage_1-317.png)

En este cuadro de diálogo, también puede configurar el diseño del componente de vídeo y los parámetros para [!UICONTROL Reproducción], [!UICONTROL Flash], y [!UICONTROL Avanzadas].

## AEM Instalación de FFmpeg y configuración de la {#install-ffmpeg}

El componente de vídeo se basa en el producto de código abierto de terceros FFmpeg para transcodificar vídeos. Descargado de [https://ffmpeg.org/](https://ffmpeg.org/). AEM Después de instalar FFmpeg, configure la configuración para utilizar un códec de audio específico y opciones específicas de tiempo de ejecución.

Para instalar FFmpeg en **Windows**, siga estos pasos:

1. Descargue el binario compilado como `ffmpeg.zip`.
1. Desarchivar en una carpeta.
1. Establecer la variable de entorno del sistema `PATH` hasta &lt;*your-ffmpeg-location*>`\bin`.
1. AEM Reinicie la sesión.

Para instalar FFmpeg en **MAC OS X**, siga estos pasos:

1. Instalar Xcode disponible en [developer.apple.com/xcode](https://developer.apple.com/xcode/).
1. Instalación disponible en [XQuartz](https://www.xquartz.org) para obtener [X11](https://support.apple.com/es-es/HT201341).
1. Instale MacPorts disponibles en [www.macports.org](https://www.macports.org/).
1. En la consola, ejecute `sudo port install ffmpeg` y siga las instrucciones que aparecen en la pantalla. Asegúrese de que la ruta del `FFmpeg` El ejecutable de se agrega a `PATH` variable del sistema.

Para instalar FFmpeg en **Mac OS X 10.6**, utilizando la versión precompilada, siga estos pasos:

1. Descargue la versión precompilada.
1. Desarchivarlo en el `/usr/local` directorio.
1. En la consola, ejecute `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`. Cambie las rutas según corresponda.

Hasta **AEM configurar la**, siga estos pasos:

>[!NOTE]
>
>Estos pasos solo son necesarios si se requiere una mayor personalización de los códecs.

1. Abrir [!UICONTROL CRXDE Lite] en el explorador web. Acceso [http://localhost:4502/crx/de](http://localhost:4502/crx/de).
2. Seleccione el `/libs/settings/dam/video/format_aac/jcr:content` y asegúrese de que las propiedades del nodo son las siguientes:

   * `audioCodec` es `aac`.
   * `customArgs` es `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. Para personalizar la configuración, cree una superposición en `/apps/settings/` y mueva la misma estructura debajo de `/conf/global/settings/` nodo. No se puede editar en `/libs` nodo. Por ejemplo, para superponer una ruta `/libs/settings/dam/video/fullhd-bp`, créela en `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >Superponga y edite todo el nodo de perfil y no solo la propiedad que necesita modificación. Estos recursos no se resuelven mediante SlingResourceMerger.

4. Si ha cambiado alguna de las propiedades, haga clic en **[!UICONTROL Guardar todo]**.

>[!NOTE]
>
>AEM Los cambios en los modelos de flujo de trabajo predeterminados (OOTB) no se conservan al actualizar la instancia de. El Adobe recomienda copiar los modelos de flujo de trabajo modificados antes de editarlos. Por ejemplo, copie el OOTB [!UICONTROL Recurso de actualización DAM] antes de editar el paso FFmpeg Transcoding en el [!UICONTROL Recurso de actualización DAM] modelo para elegir nombres de perfil de vídeo que existían antes de la actualización. A continuación, puede superponer la variable `/apps` AEM para permitir a los usuarios recuperar los cambios personalizados del modelo de OOTB, de manera que puedan recuperarlos.
