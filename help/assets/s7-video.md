---
title: Vídeo
description: Obtenga información acerca de la administración centralizada de recursos de vídeo en Adobe Experience Manager Assets, donde puede cargar vídeos para su codificación automática en Dynamic Media Classic y acceder a vídeos de Dynamic Media Classic directamente desde Experience Manager Assets. La integración de vídeo de Dynamic Media Classic amplía el alcance del vídeo optimizado a todas las pantallas.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
role: User, Admin
mini-toc-levels: 3
exl-id: 56009925-1a36-48b5-b96c-ec2e468da106
feature: Video
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1551'
ht-degree: 1%

---

# Vídeo {#video}

Adobe Experience Manager Assets proporciona una administración centralizada de recursos de vídeo, donde puede cargar vídeos directamente en Assets para su codificación automática en Dynamic Media Classic y acceder a vídeos de Dynamic Media Classic directamente desde Assets para la creación de páginas.

La integración de vídeo de Dynamic Media Classic amplía el alcance del vídeo optimizado a todas las pantallas (detección automática de dispositivos y ancho de banda).

* El **[!UICONTROL Scene7 Video]** El componente realiza automáticamente la detección de dispositivos y ancho de banda para reproducir el formato y el vídeo de calidad adecuados en equipos de escritorio, tabletas y dispositivos móviles.
* Recursos: puede incluir conjuntos de vídeos adaptables en lugar de recursos de vídeo únicos. Un conjunto de vídeos adaptable contiene todas las representaciones de vídeo necesarias para reproducir vídeo sin problemas en varias pantallas. Un conjunto de vídeos adaptable agrupa versiones del mismo vídeo que se codifican a diferentes velocidades de bits y formatos, como 400 kbps, 800 kbps y 1000 kbps. Puede utilizar un conjunto de vídeos adaptable, junto con el componente de vídeo S7, para la transmisión de vídeo adaptable en varias pantallas, incluidos equipos de escritorio, iOS, Android™, BlackBerry® y dispositivos móviles Windows.
<!-- See [Scene7 documentation about adaptive video sets for more information](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html). -->

## Acerca de FFMPEG y Dynamic Media Classic {#about-ffmpeg-and-scene}

El proceso de codificación de vídeo predeterminado se basa en el uso de la integración basada en FFMPEG con perfiles de vídeo. Por lo tanto, el flujo de trabajo de ingesta de DAM predeterminado contiene los dos pasos siguientes del flujo de trabajo basado en ffmpeg:

* Miniaturas FFMPEG
* Codificación FFMPEG

Al habilitar y configurar la integración de Dynamic Media Classic, no se eliminan ni desactivan automáticamente estos dos pasos del flujo de trabajo de ingesta de DAM predeterminado. Si ya utiliza la codificación de vídeo basada en FFMPEG en Adobe Experience Manager, es probable que tenga FFMPEG instalado en los entornos de creación. En este caso, un nuevo vídeo introducido mediante DAM se codificaría dos veces: una desde el codificador FFMPEG y otra desde la integración de Dynamic Media Classic.

Si tiene configurada la codificación de vídeo basada en FFMPEG en Experience Manager y FFMPEG instalado, Adobe recomienda eliminar los dos flujos de trabajo FFMPEG de los flujos de trabajo de ingesta de DAM.

## Formatos admitidos {#supported-formats}

Los siguientes formatos son compatibles con el componente de vídeo de Scene7:

* F4V H.264
* MP4 H.264

## Decida dónde cargar el vídeo {#deciding-where-to-upload-your-video}

La decisión sobre dónde cargar los recursos de vídeo depende de lo siguiente:

* ¿Necesita un flujo de trabajo para el recurso de vídeo?
* ¿Necesita control de versión para el recurso de vídeo?

Si la respuesta a alguna de estas preguntas es &quot;sí&quot;, cargue el vídeo directamente en Adobe DAM. Si la respuesta a ambas preguntas es &quot;no&quot;, cargue el vídeo directamente en Dynamic Media Classic. El flujo de trabajo para cada escenario se describe en la siguiente sección.

### Si está cargando el vídeo directamente en Adobe DAM {#if-you-are-uploading-your-video-directly-to-adobe-dam}

Si necesita un flujo de trabajo o control de versiones para sus recursos, cárguelos primero en DAM de Adobe. El flujo de trabajo recomendado es el siguiente:

1. Cargue el recurso de vídeo en Adobe DAM y codifique y publique automáticamente en Dynamic Media Classic.
1. En Experience Manager, acceda a los recursos de vídeo en WCM en la **[!UICONTROL Películas]** del Buscador de contenido.
1. Autor con **[!UICONTROL Scene7 Video]** o **[!UICONTROL Vídeo de base]** componente.

### Si carga el vídeo en Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Si no necesita un flujo de trabajo o control de versiones para sus recursos, cárguelos en Scene7. El flujo de trabajo recomendado es el siguiente:

1. En Dynamic Media Classic, [configurar una carga y codificación FTP programadas en Scene7 (sistema automatizado)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-files-using-via-ftp).
1. En Experience Manager, acceda a los recursos de vídeo en WCM en la **[!UICONTROL Scene7]** del Buscador de contenido.
1. Autor con el **[!UICONTROL Scene7 Video]** componente.

## Configuración de la integración con Scene7 Video {#configuring-integration-with-scene-video}

1. Entrada **[!UICONTROL Cloud Service]**, vaya a su **[!UICONTROL Scene7]** y seleccione **[!UICONTROL Editar]**.
1. Seleccione el **[!UICONTROL Vídeo]** pestaña.

   ![chlimage_1-363](assets/chlimage_1-363.png)

   >[!NOTE]
   >
   >El **[!UICONTROL Vídeo]** La pestaña no aparece si la página no tiene una configuración de nube.

1. Seleccione el perfil de codificación de vídeo adaptable, un perfil de codificación de vídeo único predeterminado o un perfil de codificación de vídeo personalizado.

   >[!NOTE]
   >
   >Para obtener más información sobre el significado de los ajustes preestablecidos de vídeo, consulte la [Documentación de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).
   >
   >El Adobe recomienda seleccionar ambos conjuntos de vídeos adaptables al configurar los ajustes preestablecidos universales o seleccionar el **[!UICONTROL Codificación de vídeo adaptable]** opción.

1. Los perfiles de codificación seleccionados se aplican automáticamente a todos los vídeos cargados en la carpeta de destino CQ DAM que haya configurado para esta configuración de nube de Scene7. Puede configurar varias configuraciones de nube de Scene7 con diferentes carpetas de destino para aplicar diferentes perfiles de codificación según sea necesario.

## Actualizar los ajustes preestablecidos del visor y de codificación {#updating-viewer-and-encoding-presets}

Para actualizar los ajustes preestablecidos de visualizador y codificación para vídeo porque se han actualizado en Scene7, vaya a la configuración de Scene7 en la Configuración de nube y seleccione **[!UICONTROL Actualizar el visualizador y los ajustes preestablecidos de codificación]**.

![chlimage_1-364](assets/chlimage_1-364.png)

## Cargue el vídeo de origen principal en Scene7 desde Adobe DAM {#uploading-your-master-video}

1. Vaya a la carpeta de destino de CQ DAM donde ha configurado la configuración de nube con perfiles de codificación de Scene7.
1. Seleccionar **[!UICONTROL Cargar]** para cargar el vídeo de origen principal. La carga y la codificación de vídeo se completan después de [!UICONTROL Recurso de actualización DAM] flujo de trabajo completado y **[!UICONTROL Publicar en Scene7]** tiene una marca de verificación.

   >[!NOTE]
   >
   >Las miniaturas de vídeo tardan un tiempo en generarse.

   Arrastrar el vídeo de origen principal DAM a los accesos de componente de vídeo *todo* Representaciones de proxy codificadas en Scene7 para la entrega.

## Componente de vídeo base frente a componente de vídeo Scene7 {#foundation-video-component-versus-scene-video-component}

Al utilizar Experience Manager, puede acceder al componente de vídeo disponible en Sites y al componente de vídeo de Scene7. Estos componentes no son intercambiables.

El componente de vídeo de Scene7 solo funciona para vídeos de Scene7. El componente de base funciona con vídeos almacenados desde Experience Manager (con ffmpeg) y vídeos de Scene7.

La siguiente matriz explica cuándo utilizar qué componente:

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>De forma predeterminada, el componente de vídeo S7 utiliza el perfil de vídeo universal. Sin embargo, puede obtener el reproductor de vídeo basado en HTML5 para que lo utilice Experience Manager. En Scene7, copie el código incrustado del reproductor de vídeo HTML5 incorporado y colóquelo en la página del Experience Manager.

## Componente de vídeo de Experience Manager {#aem-video-component}

Aunque se recomiende el uso del componente de vídeo de Scene7 para ver vídeos de Scene7, en esta sección se describe el uso de vídeos de Scene7 con el componente de vídeo de Foundation en Experience Manager, en aras de la exhaustividad.

### Comparación entre Experience Manager Video y Scene7 Video {#aem-video-and-scene-video-comparison}

En la tabla siguiente se proporciona una comparación de alto nivel de las funciones compatibles entre el componente de vídeo de Experience Manager Foundation y el componente de vídeo de Scene7:

|   | Vídeo de Experience Manager Foundation | Scene7 Video |
|---|---|---|
| Aproximación | Primer acercamiento de HTML 5. El Flash solo se utiliza para la reserva que no es de HTML 5. | Flash en la mayoría de los sobremesas. HTML5 se utiliza para móviles y tabletas. |
| Entrega | Progresivo | Flujo adaptable |
| Seguimiento | Sí | Sí |
| Extensibilidad | Sí | No |
| Vídeo móvil | Sí | Sí |

### Configuración de {#setting-up}

#### Creación de perfiles de vídeo {#creating-video-profiles}

Las distintas codificaciones de vídeo se crean según los ajustes preestablecidos de codificación de S7 seleccionados en la configuración de nube de S7. Para que el componente de vídeo de base los utilice, se debe crear un perfil de vídeo para cada ajuste preestablecido de codificación S7 seleccionado. Este método permite al componente de vídeo seleccionar las representaciones DAM según corresponda.

>[!NOTE]
>
>Para poder publicar, deben activarse nuevos perfiles de vídeo y cambios en los mismos.

1. En Experience Manager, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Consola de configuración]**.
1. En el **[!UICONTROL Consola de configuración]**, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL DAM]** > **[!UICONTROL Perfiles de vídeo]** en el árbol de navegación.
1. Cree un perfil de vídeo de S7. En el **[!UICONTROL Nuevo]**. menú, seleccione **[!UICONTROL Crear página]** y, a continuación, seleccione la plantilla Scene7 Video Profile. Asigne un nombre a la nueva página de perfil de vídeo y seleccione **[!UICONTROL Crear]**.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Edite el nuevo perfil de vídeo. Seleccione primero la configuración de nube. A continuación, seleccione el mismo ajuste preestablecido de codificación que se seleccionó en la configuración de la nube.

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | Propiedad | Descripción |
   |---|---|
   | Configuración de nube de Scene7 | La configuración de nube que se utilizará para los ajustes preestablecidos de codificación. |
   | Ajuste preestablecido de codificación de Scene7 | Ajuste preestablecido de codificación con el que se asignará este perfil de vídeo. |
   | Tipo de vídeo HTML5 | Esta propiedad permite establecer el valor de la propiedad type del elemento de origen de vídeo HTML 5. Esta información no la proporcionan los ajustes preestablecidos de codificación de S7, pero es necesaria para procesar correctamente los vídeos con el elemento de vídeo de HTML 5. Se proporciona una lista de formatos comunes, pero se puede sobrescribir para otros formatos. |

   Repita este paso para todos los ajustes preestablecidos de codificación seleccionados en la configuración de nube que desee utilizar en el componente de vídeo.

#### Configuración del diseño {#configuring-design}

El **[!UICONTROL Vídeo de base]** El componente debe saber qué perfiles de vídeo utilizar para crear la lista de fuentes de vídeo. Abra el cuadro de diálogo de diseño de componentes de vídeo y configure el diseño de componentes para con los nuevos perfiles de vídeo.

>[!NOTE]
>
>Si usa el **[!UICONTROL Vídeo de base]** en una página móvil, repita estos pasos en el diseño de la página móvil.

>[!NOTE]
>
>Los cambios realizados en el diseño requieren que su activación surta efecto en la publicación.

1. Abra el **[!UICONTROL Vídeo de base]** Cuadro de diálogo de diseño del componente y cambie a **[!UICONTROL Perfiles]** pestaña. A continuación, elimine los perfiles predeterminados y añada los nuevos perfiles de vídeo de S7. El orden de la lista de perfiles en el cuadro de diálogo de diseño define el orden del elemento de orígenes de vídeo al procesarse.
1. En los exploradores que no admiten HTML5, el componente de vídeo permite configurar una reserva de Flash. Abra el cuadro de diálogo de diseño de componentes de vídeo y cambie a **[!UICONTROL Flash]** pestaña. Configure los ajustes del reproductor de Flash y asigne un perfil de reserva para el reproductor Flash.

#### Lista de comprobación {#checklist}

1. Cree una configuración de nube de S7. Asegúrese de que los ajustes preestablecidos de codificación de vídeo estén configurados y de que el importador esté en ejecución.
1. Cree un perfil de vídeo S7 para cada ajuste preestablecido de codificación de vídeo seleccionado en la configuración de la nube.
1. Los perfiles de vídeo deben activarse.
1. Configurar el diseño de **[!UICONTROL Vídeo de base]** en la página.
1. Active el diseño una vez que haya terminado con los cambios de diseño.
