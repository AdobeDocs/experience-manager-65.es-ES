---
title: Vídeo
description: Obtenga información sobre la administración centralizada de recursos de vídeo Adobe Experience Manager Assets, donde puede cargar vídeos para su codificación automática en Dynamic Media Classic y acceder a vídeos de Dynamic Media Classic directamente desde Recursos de Experience Manager. La integración de vídeo de Dynamic Media Classic amplía el alcance del vídeo optimizado a todas las pantallas.
uuid: 8b3423f1-d96b-44d9-bdb7-e3b77875b25d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: 2685f9f3-0973-40a9-89b8-e7db0a6a75f2
role: Business Practitioner, Administrator
exl-id: 56009925-1a36-48b5-b96c-ec2e468da106
feature: Vídeo
source-git-commit: 99230f2b9ce8179de4034d8bd739a5535b2cc0da
workflow-type: tm+mt
source-wordcount: '1568'
ht-degree: 34%

---

# Vídeo {#video}

Adobe Experience Manager Assets permite la administración centralizada de recursos de vídeo, desde la que puede cargar vídeos directamente en Assets para la codificación automática en Dynamic Media Classic y acceder a vídeos de Dynamic Media Classic directamente desde Assets para la creación de páginas.

La integración de vídeo de Dynamic Media Classic amplía el alcance del vídeo optimizado a todas las pantallas (detección automática de dispositivos y ancho de banda).

* El componente **[!UICONTROL Scene7 Video]** realiza automáticamente la detección de dispositivos y ancho de banda para reproducir el formato y la calidad de vídeo correctos en equipos de escritorio, tabletas y dispositivos móviles.
* Assets: puede incluir conjuntos de vídeos adaptables en lugar de solo recursos de vídeo únicos. Un conjunto de vídeos adaptables contiene todas las representaciones de vídeo necesarias para reproducir vídeo sin problemas en varias pantallas. Un conjunto de vídeos adaptables agrupa versiones del mismo vídeo codificadas a diferentes velocidades de bits y formatos, como 400 kbps, 800 kbps y 1000 kbps. Utiliza un conjunto de vídeos adaptables, junto con el componente de vídeo S7, para el flujo de vídeo adaptable en varias pantallas, incluidos los dispositivos móviles de escritorio, iOS, Android™, BlackBerry® y Windows.
<!-- See [Scene7 documentation about adaptive video sets for more information](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html). -->

## Acerca de FFMPEG y Dynamic Media Classic {#about-ffmpeg-and-scene}

El proceso de codificación de vídeo predeterminado se basa en el uso de la integración basada en FFMPEG con los perfiles de vídeo. Por lo tanto, el flujo de trabajo de ingesta de DAM incorporado contiene los dos pasos siguientes de flujo de trabajo basados en FFMP:

* Miniaturas de FFMPEG
* Codificación de FFMPEG

Al habilitar y configurar la integración de Dynamic Media Classic, no se eliminan ni se desactivan automáticamente estos dos pasos de flujo de trabajo del flujo de trabajo de ingesta de DAM integrado. Si ya utiliza la codificación de vídeo basada en FFMPEG en Adobe Experience Manager, es probable que tenga FFMPEG instalado en los entornos de creación. En este caso, un nuevo vídeo ingestado con DAM se codificaría dos veces: una desde el codificador FFMPEG y otra desde la integración con Dynamic Media Classic.

Si tiene configurada la codificación de vídeo basada en FFMPEG en el Experience Manager y FFMPEG instalado, Adobe recomienda eliminar los dos flujos de trabajo FFMPEG de los flujos de trabajo de ingesta de DAM.

## Formatos admitidos {#supported-formats}

Los formatos siguientes se admiten para el componente de vídeo de Scene7:

* F4V H.264
* MP4 H.264

## Decidir dónde cargar el vídeo {#deciding-where-to-upload-your-video}

Decidir dónde cargar los recursos de vídeo depende de las acciones siguientes:

* ¿Necesita un flujo de trabajo para el recurso de vídeo?
* ¿Necesita un control de versión para el recurso de vídeo?

Si la respuesta es “sí” a una o ambas preguntas, cargue el vídeo directamente en Adobe DAM. Si la respuesta a ambas preguntas es &quot;no&quot;, cargue el vídeo directamente en Dynamic Media Classic. El flujo de trabajo de cada escenario se describe en la sección siguiente.

### Si está cargando el vídeo directamente en Adobe DAM {#if-you-are-uploading-your-video-directly-to-adobe-dam}

Si necesita un flujo de trabajo o crear versiones de los recursos, primero cargue en Adobe DAM . El flujo de trabajo siguiente es el recomendado:

1. Cargue el recurso de vídeo en DAM de Adobe y codifique y publique automáticamente en Dynamic Media Classic.
1. En el Experience Manager, acceda a los recursos de vídeo de WCM en la pestaña **[!UICONTROL Películas]** del Buscador de contenido.
1. Autor con **[!UICONTROL Scene7 Video]** o componente **[!UICONTROL Foundation Video]**.

### Si está cargando el vídeo en Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Si no necesita un flujo de trabajo o crear versiones de los recursos, cárguelos a Scene7. El flujo de trabajo siguiente es el recomendado:

1. En Dynamic Media Classic, [configure una carga y codificación de FTP programada en Scene7 (sistema automatizado)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-files-using-via-ftp).
1. En el Experience Manager, acceda a los recursos de vídeo de WCM en la pestaña **[!UICONTROL Scene7]** del Buscador de contenido.
1. Autor con el componente **[!UICONTROL Scene7 Video]**.

## Configuración de la integración con vídeo de Scene7 {#configuring-integration-with-scene-video}

Para configurar los ajustes preestablecidos universales:

1. En **[!UICONTROL Servicios de nube]**, vaya a la configuración de **[!UICONTROL Scene7]** y haga clic en **[!UICONTROL Editar]**.
1. Seleccione la pestaña **[!UICONTROL Vídeo]**.

   ![chlimage_1-363](assets/chlimage_1-363.png)

   >[!NOTE]
   >
   >La pestaña **[!UICONTROL Vídeo]** no aparece si la página no tiene una configuración de nube.

1. Seleccione el perfil de codificación de vídeo adaptable, un perfil de codificación de vídeo único listo para usar o un perfil de codificación de vídeo personalizado.

   >[!NOTE]
   >
   >Para obtener más información sobre el significado de los ajustes preestablecidos de vídeo, consulte la [documentación de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).
   >
   >Adobe recomienda que seleccione ambos conjuntos de vídeos adaptables al configurar los ajustes preestablecidos universales o que seleccione la opción **[!UICONTROL Codificación de vídeo adaptable]**.

1. Los perfiles de codificación seleccionados se aplican automáticamente a todos los vídeos cargados en la carpeta de destino de CQ DAM que ha configurado para esta configuración de nube de Scene7. Puede establecer diversas configuraciones de nube de Scene7 con diferentes carpetas de destino para aplicar distintos perfiles de codificación según sea necesario.

## Actualizar los ajustes preestablecidos del visor y de codificación  {#updating-viewer-and-encoding-presets}

Para actualizar los ajustes preestablecidos de visor y codificación para vídeo porque los ajustes preestablecidos se actualizaron en Scene7, vaya a la configuración de Scene7 en la Configuración de nube y pulse **[!UICONTROL Actualizar los ajustes preestablecidos de visor y codificación]**.

![chlimage_1-364](assets/chlimage_1-364.png)

## Carga del vídeo de origen principal a Scene7 desde Adobe DAM {#uploading-your-master-video}

1. Vaya a la carpeta de destino de CQ DAM en que ha establecido la configuración de nube con perfiles de codificación de Scene7.
1. Haga clic en **[!UICONTROL Cargar]** para cargar el vídeo de origen principal. La carga y codificación de vídeo se completan después de que el flujo de trabajo [!UICONTROL DAM Update Asset] se haya completado y **[!UICONTROL Publish to Scene7]** tenga una marca de verificación.

   >[!NOTE]
   >
   >Las miniaturas de vídeo tardan un tiempo en generarse.

   Al arrastrar el vídeo de origen principal de DAM al componente de vídeo, se accede a *all* representaciones proxy codificadas de Scene7 para su envío.

## Componente de vídeo base frente al componente de vídeo de Scene7 {#foundation-video-component-versus-scene-video-component}

Al utilizar Experience Manager, tiene acceso al componente Vídeo disponible en Sitios y al componente de vídeo de Scene7. Dichos componentes no son intercambiables.

El componente de vídeo de Scene7 solo funciona para los vídeos de Scene7. El componente base funciona con vídeos almacenados desde el Experience Manager (mediante ffmpeg) y vídeos de Scene7.

La siguiente matriz explica cuándo utilizar cada componente:

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>El componente de vídeo de S7, listo para usar, utiliza el perfil de vídeo universal. Sin embargo, puede obtener el reproductor de vídeo basado en HTML5 para que lo utilice el Experience Manager. En Scene7, copie el código incrustado del reproductor de vídeo HTML5 incorporado y colóquelo en la página Experience Manager.

## Componente de vídeo de Experience Manager {#aem-video-component}

Incluso si se recomienda utilizar el componente de vídeo de Scene7 para ver vídeos de Scene7, en esta sección se describe el uso de vídeos de Scene7 con el componente de vídeo base en Experience Manager, para que sea más completo.

### Comparación de vídeo de Experience Manager y vídeo de Scene7 {#aem-video-and-scene-video-comparison}

La siguiente tabla ofrece una comparación de alto nivel de las funciones admitidas entre el componente de vídeo base de Experience Manager y el componente de vídeo de Scene7:

|  | Vídeo de base de Experience Manager | Vídeo de Scene7 |
|---|---|---|
| Enfoque | Primer enfoque de HTML5. Flash solo se utiliza para la alternativa no HTML5. | Flash en la mayoría de los equipos de escritorio. HTML5 se utiliza para móviles y tabletas. |
| Entrega | Progresivo | Transmisión adaptable |
| Seguimiento | Sí | Sí |
| Capacidad de ampliación | Sí | No |
| Vídeo móvil | Sí | Sí |

### Configuración  {#setting-up}

#### Creación de perfiles de vídeo {#creating-video-profiles}

Las distintas codificaciones de vídeo se crean de acuerdo con los ajustes preestablecidos de codificación de S7 seleccionados en la configuración de nube de S7. Para que el componente de vídeo base los utilice, se debe crear un perfil de vídeo para cada ajuste preestablecido de codificación de S7 seleccionado. Este método permite que el componente de vídeo seleccione las representaciones de DAM según corresponda.

>[!NOTE]
>
>Los perfiles de vídeo nuevos, así como los cambios que se realicen en ellos, deben activarse para publicarse.

1. En el Experience Manager, pulse **[!UICONTROL Herramientas]** > **[!UICONTROL Consola de configuración]**.
1. En la **[!UICONTROL Consola de configuración]**, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL DAM]** > **[!UICONTROL Perfiles de vídeo]** en el árbol de navegación.
1. Crear un perfil de vídeo de S7. En el menú **[!UICONTROL Nuevo]**., seleccione **[!UICONTROL Crear página]** y, a continuación, seleccione la plantilla Perfil de vídeo de Scene7. Asigne un nombre a la página nueva del perfil de vídeo y haga clic en **[!UICONTROL Crear]**.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Edite el nuevo perfil de vídeo. Seleccione primero la configuración de nube. A continuación, seleccione el mismo ajuste preestablecido de codificación que el que se ha seleccionado en la configuración de nube.

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | Propiedad | Descripción |
   |---|---|
   | Configuración de nube de Scene7 | La configuración de nube que se utilizará para los ajustes preestablecidos de codificación. |
   | Ajuste preestablecido de codificación de Scene7 | El ajuste preestablecido de codificación con el que asignar este perfil de vídeo. |
   | Tipo de vídeo HTML5 | Esta propiedad permite establecer el valor de la propiedad type del elemento de origen de vídeo HTML5. Los ajustes preestablecidos de codificación de S7 no proporcionan esta información, pero es necesaria para procesar correctamente los vídeos mediante el elemento de vídeo HTML5. Se proporciona una lista de los formatos comunes, pero se pueden sobrescribir por otros formatos. |

   Repita este paso para todos los ajustes preestablecidos de codificación seleccionados en la configuración de nube que desea utilizar en el componente de vídeo.

#### Configuración del diseño {#configuring-design}

El componente **[!UICONTROL Vídeo base]** debe saber qué perfiles de vídeo utilizar para crear la lista de fuentes de vídeo. Abra el cuadro de diálogo de diseño de componentes de vídeo y configure el diseño de componentes para utilizar los nuevos perfiles de vídeo.

>[!NOTE]
>
>Si utiliza el componente **[!UICONTROL Vídeo base]** en una página móvil, repita estos pasos en el diseño de la página móvil.

>[!NOTE]
>
>Los cambios realizados en el diseño requieren la activación del diseño para que surtan efecto en la publicación.

1. Abra el cuadro de diálogo de diseño del componente **[!UICONTROL Vídeo base]** y cambie a la pestaña **[!UICONTROL Perfiles]**. A continuación, elimine los perfiles predeterminados y añada los nuevos perfiles de vídeo de S7. El orden de la lista de perfiles en el cuadro de diálogo de diseño define el orden del elemento de orígenes de vídeo al realizar la representación.
1. En los exploradores que no admiten HTML5, el componente de vídeo permite configurar una alternativa de Flash. Abra el cuadro de diálogo de diseño de componentes de vídeo y cambie a la pestaña **[!UICONTROL Flash]**. Configure los ajustes del reproductor de Flash y asigne un perfil de reserva para el reproductor Flash.

#### Lista de comprobación {#checklist}

1. Cree una configuración de nube de S7. Asegúrese de que los ajustes preestablecidos de codificación de vídeo estén configurados y de que el importador se esté ejecutando.
1. Cree un perfil de vídeo de S7 para cada ajuste preestablecido de codificación de vídeo seleccionado en la configuración de nube.
1. Los perfiles de vídeo deben estar activados.
1. Configure el diseño del componente **[!UICONTROL Vídeo base]** en la página.
1. Active el diseño cuando haya terminado con los cambios de diseño.
