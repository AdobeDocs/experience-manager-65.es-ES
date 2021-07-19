---
title: Vídeo
seo-title: Vídeo
description: Los recursos permiten la administración centralizada de recursos de vídeo, donde puede cargar vídeos directamente en Assets para la codificación automática en Dynamic Media Classic y acceder a los vídeos de Dy directamente desde Assets para la creación de páginas.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dfaa4b3f-f65a-4fe3-87a7-f3bc71015e56
exl-id: c540aa49-9981-4e8c-97df-972085b26490
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 26%

---

# Vídeo{#video}

Los recursos permiten la administración centralizada de recursos de vídeo, donde puede cargar vídeos directamente en Assets para la codificación automática en Dynamic Media Classic y acceder a los vídeos de Dynamic Media Classic directamente desde Assets para la creación de páginas.

La integración de vídeo de Dynamic Media Classic amplía el alcance del vídeo optimizado a todas las pantallas (detección automática de dispositivos y ancho de banda).

* El componente de vídeo Dynamic Media Classic realiza automáticamente la detección de dispositivos y ancho de banda para reproducir el formato y la calidad de vídeo correctos en equipos de escritorio, tabletas y dispositivos móviles.
* Assets: puede incluir conjuntos de vídeos adaptables en lugar de solo recursos de vídeo únicos. Un conjunto de vídeos adaptables es un contenedor para todas las representaciones de vídeo necesarias para reproducir vídeo sin problemas en varias pantallas. Un conjunto de vídeos adaptables agrupa versiones del mismo vídeo codificadas a diferentes velocidades de bits y formatos, como 400 kbps, 800 kbps y 1000 kbps. Utiliza un conjunto de vídeos adaptables, junto con el componente de vídeo S7, para el flujo de vídeo adaptable en varias pantallas, incluidos los dispositivos móviles de escritorio, iOS, Android™, BlackBerry® y Windows. Consulte la [documentación de Dynamic Media Classic sobre los conjuntos de vídeos adaptables para obtener más información](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html#video).

## Acerca de FFMPEG y Dynamic Media Classic {#about-ffmpeg-and-scene}

El proceso de codificación de vídeo predeterminado se basa en el uso de la integración basada en FFMPEG con los perfiles de vídeo. Por lo tanto, el flujo de trabajo [!UICONTROL Activo de actualización de DAM] listo para usar contiene los dos pasos de flujo de trabajo basados en FFMP siguientes:

* Miniaturas de FFMPEG
* Codificación de FFMPEG

Al habilitar y configurar la integración de Dynamic Media Classic, no se eliminan ni se desactivan automáticamente estos dos pasos de flujo de trabajo del flujo de trabajo de ingesta de [!UICONTROL Activo de actualización de DAM] listo para usar. Si ya utiliza codificación de vídeo basada en FFMPEG en Adobe Experience Manager, es probable que tenga FFMPEG instalado en sus entornos de creación. En este caso, un nuevo vídeo grabado con Recursos de Experience Manager se codifica dos veces: una desde el codificador FFMPEG y otra desde la integración con Dynamic Media Classic.

Si tiene configurada la codificación de vídeo basada en FFMPEG en el Experience Manager y FFMPEG instalado, Adobe recomienda eliminar los dos flujos de trabajo FFMPEG de los flujos de trabajo [!UICONTROL DAM Update Asset].

### Formatos admitidos {#supported-formats}

El componente de vídeo Dynamic Media Classic admite los siguientes formatos:

* F4V H.264
* MP4 H.264

### Decida dónde cargar el vídeo {#deciding-where-to-upload-your-video}

Decidir dónde cargar los recursos de vídeo depende de las acciones siguientes:

* ¿Necesita un flujo de trabajo para el recurso de vídeo?
* ¿Necesita un control de versión para el recurso de vídeo?

Si la respuesta es “sí” a una o ambas preguntas, cargue el vídeo directamente en Adobe DAM. Si la respuesta a ambas preguntas es &quot;no&quot;, cargue el vídeo directamente en Dynamic Media Classic. El flujo de trabajo de cada escenario se describe en la sección siguiente.

#### Si está cargando el vídeo directamente en Adobe Assets {#if-you-are-uploading-your-video-directly-to-adobe-assets}

Si necesita un flujo de trabajo o crear versiones de sus recursos, primero debe cargar en Adobe Assets. El flujo de trabajo siguiente es el recomendado:

1. Cargue el recurso de vídeo en Recursos de Adobe y codifique y publique automáticamente en Dynamic Media Classic.
1. En el Experience Manager, acceda a los recursos de vídeo de WCM en la pestaña **[!UICONTROL Películas]** del Buscador de contenido.
1. Autor con vídeo de Dynamic Media Classic o componente de vídeo base.

#### Si está cargando el vídeo en Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Si no necesita un flujo de trabajo o crear versiones de los recursos, debe cargarlos en Dynamic Media Classic. El flujo de trabajo siguiente es el recomendado:

1. En la aplicación de escritorio de Dynamic Media Classic, [configure una carga y codificación de FTP programadas en Dynamic Media Classic (sistema automatizado)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html?lang=en#upload-options).
1. En el Experience Manager, acceda a los recursos de vídeo de WCM en la pestaña **[!UICONTROL Dynamic Media Classic]** del Buscador de contenido.
1. Autor con el componente de vídeo de Dynamic Media Classic.

### Configurar la integración con Dynamic Media Classic Video {#configuring-integration-with-scene-video}

1. En **[!UICONTROL Cloud Services]**, vaya a la configuración de **[!UICONTROL Dynamic Media Classic]** y seleccione **[!UICONTROL Editar]**.
1. Seleccione la pestaña **[!UICONTROL Vídeo]**.

   >[!NOTE]
   >
   >La pestaña **[!UICONTROL Vídeo]** no aparece si la página no tiene una configuración de nube. Consulte [Habilitar Dynamic Media Classic para WCM](#enablingscene7forwcm).

1. Seleccione el perfil de codificación de vídeo adaptable, un perfil de codificación de vídeo único listo para usar o un perfil de codificación de vídeo personalizado.

   >[!NOTE]
   >
   >Para obtener más información sobre el significado de los ajustes preestablecidos de vídeo, consulte [Ajustes preestablecidos de vídeo para codificar archivos de vídeo](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html?lang=en#video-presets-for-encoding-video-files).
   >
   >Adobe recomienda que seleccione ambos conjuntos de vídeos adaptables al configurar los ajustes preestablecidos universales o que seleccione la opción **[!UICONTROL Codificación de vídeo adaptable]**.

1. Los perfiles de codificación seleccionados se aplican automáticamente a todos los vídeos cargados en la carpeta de destino de CQ DAM configurada para esta configuración de nube de Dynamic Media Classic. Puede configurar varias configuraciones de nube de Dynamic Media Classic con diferentes carpetas de destino para aplicar distintos perfiles de codificación según sea necesario.

### Actualizar los ajustes preestablecidos del visor y de codificación {#updating-viewer-and-encoding-presets}

Actualice el visor y los ajustes preestablecidos de codificación para vídeo en Experience Manager si los ajustes preestablecidos se actualizaron en Dynamic Media Classic. En este caso, vaya a la configuración de Dynamic Media Classic en la configuración de nube y seleccione **Actualizar los ajustes preestablecidos de visor y codificación**.

![chlimage_1-131](assets/chlimage_1-131.png)

### Cargar el vídeo de origen principal {#uploading-your-master-video}

Para cargar el vídeo de origen principal en Dynamic Media Classic desde Adobe DAM:

1. Vaya a la carpeta de destino de CQ DAM donde ha configurado la configuración de nube con perfiles de codificación de Dynamic Media Classic.
1. Seleccione **[!UICONTROL Upload]** para cargar el vídeo de origen principal. La carga y codificación de vídeo se completan después de que el flujo de trabajo [!UICONTROL DAM Update Asset] se haya completado y **[!UICONTROL Publish to Dynamic Media Classic]** tenga una marca de verificación.

   >[!NOTE]
   >
   >Puede que pase un tiempo hasta que las miniaturas de vídeo se generen.

   Cuando arrastra el vídeo de origen principal de DAM al componente de vídeo, accede a *todas* las representaciones proxy codificadas de Dynamic Media Classic para su envío.

### Componente de vídeo base frente al componente de vídeo de Dynamic Media Classic {#foundation-video-component-versus-scene-video-component}

Al utilizar Experience Manager, tiene acceso al componente Vídeo disponible en Sitios y al componente de vídeo de Dynamic Media Classic. Dichos componentes no son intercambiables.

El componente de vídeo de Dynamic Media Classic solo funciona para vídeos de Dynamic Media Classic. El componente base funciona con vídeos almacenados desde el Experience Manager (con ffmpeg) y con vídeos de Dynamic Media Classic.

En la matriz siguiente se explica cuándo debe utilizar el componente:

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>De serie, el componente de vídeo de Dynamic Media Classic utiliza el perfil de vídeo universal. Sin embargo, puede obtener el reproductor de vídeo basado en HTML5 para utilizarlo el Experience Manager. En Dynamic Media Classic, copie el código incrustado del reproductor de vídeo HTML5 incorporado y colóquelo en la página Experience Manager.


## Experience Manager Componente de vídeo {#aem-video-component}

Aunque se recomiende utilizar el componente de vídeo de Dynamic Media Classic para ver vídeos de Dynamic Media Classic, en esta sección se describe el uso de vídeos de Dynamic Media Classic con el [!UICONTROL componente de vídeo base] en Experience Manager para que sea más completo.

### Comparación de vídeo Experience Manager y Dynamic Media Classic {#aem-video-and-scene-video-comparison}

La siguiente tabla ofrece una comparación de alto nivel de las funciones admitidas entre el componente de vídeo base de Experience Manager y el componente de vídeo de Dynamic Media Classic:

|  | Vídeo de base de Experience Manager | Vídeo de Dynamic Media Classic |
|---|---|---|
| Enfoque | Primer enfoque de HTML5. Flash solo se utiliza para la alternativa no HTML5. | Flash en la mayoría de los equipos de escritorio. HTML5 se utiliza para móviles y tabletas. |
| Entrega | Progresivo | Transmisión adaptable |
| Seguimiento | Sí | Sí |
| Capacidad de ampliación | Sí | No |
| Vídeo móvil | Sí | Sí |

### Configurar {#setting-up}

#### Creación de perfiles de vídeo {#creating-video-profiles}

Las distintas codificaciones de vídeo se crean según los ajustes preestablecidos de codificación de Dynamic Media Classic seleccionados en la Configuración de nube de Dynamic Media Classic. Para que el componente de vídeo base los utilice, debe crear un perfil de vídeo para cada ajuste preestablecido de codificación de Dynamic Media Classic seleccionado. Permite que el componente de vídeo seleccione las representaciones de DAM según corresponda.

>[!NOTE]
>
>Los perfiles de vídeo nuevos, así como los cambios que se realicen en ellos, deben activarse para publicarse.

1. En el Experience Manager, vaya a **[!UICONTROL Tools]** y, a continuación, seleccione **[!UICONTROL Configuration Console]**.
1. En la consola de configuración, vaya a **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Video Profiles]** en el árbol de navegación.
1. Cree un perfil de vídeo de Dynamic Media Classic. En el menú **[!UICONTROL Nuevo]**, seleccione **[!UICONTROL Crear página]**.
1. Seleccione la plantilla de perfil de vídeo de Dynamic Media Classic . Asigne un nombre a la nueva página de perfil de vídeo y seleccione **[!UICONTROL Crear]**.

   ![chlimage_1-135](assets/chlimage_1-133.png)

1. Edite el nuevo perfil de vídeo. Seleccione primero la configuración de nube. A continuación, seleccione el mismo ajuste preestablecido de codificación que el que se ha seleccionado en la configuración de nube.

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | Propiedad | Descripción |
   |---|---|
   | Configuración de nube de Dynamic Media Classic | La configuración de nube que se utilizará para los ajustes preestablecidos de codificación. |
   | Ajuste preestablecido de codificación de Dynamic Media Classic | El ajuste preestablecido de codificación con el que asignar este perfil de vídeo. |
   | Tipo de vídeo HTML5 | Esta propiedad permite establecer el valor de la propiedad type del elemento de origen de vídeo HTML5. Esta información no la proporcionan los ajustes preestablecidos de codificación de Dynamic Media Classic, pero es necesaria para procesar correctamente los vídeos mediante el elemento de vídeo HTML5. Se proporciona una lista de los formatos comunes, pero se pueden sobrescribir por otros formatos. |

   Repita este paso para todos los ajustes preestablecidos de codificación seleccionados en la configuración de nube que desea utilizar en el componente de vídeo.

#### Configurar diseño {#configuring-design}

El componente de vídeo base debe saber qué perfiles de vídeo se van a utilizar para crear la lista de orígenes de vídeo. Abra el cuadro de diálogo de diseño de componentes de vídeo y configure el diseño de componentes para utilizar los nuevos perfiles de vídeo.

>[!NOTE]
>
>Si utiliza el componente de base Vídeo en una página móvil, repita estos pasos en el diseño de la página móvil.

>[!NOTE]
>
>Los cambios realizados en el diseño requieren la activación del diseño para que surtan efecto en la publicación.

1. Abra el cuadro de diálogo de diseño del componente de vídeo base y cambie a la pestaña **[!UICONTROL Perfiles]**. A continuación, elimine los perfiles predeterminados y añada los nuevos perfiles de vídeo de Dynamic Media Classic. El orden de la lista de perfiles en el cuadro de diálogo de diseño también define el orden del elemento de orígenes de vídeo al realizar la representación.
1. En los navegadores que no admiten HTML5, el componente Vídeo permite configurar una alternativa flash. Abra el cuadro de diálogo de diseño de los componentes de vídeo y cambie a la pestaña **[!UICONTROL Flash]**. Configure las opciones de configuración de Flash Player y asigne un perfil alternativo para Flash Player.

#### Lista de comprobación {#checklist}

1. Cree una configuración de nube de Dynamic Media Classic. Asegúrese de que los ajustes preestablecidos de codificación de vídeo estén configurados y de que el importador se esté ejecutando.
1. Cree un perfil de vídeo de Dynamic Media Classic para cada ajuste preestablecido de codificación de vídeo seleccionado en la configuración de nube.
1. Los perfiles de vídeo deben estar activados.
1. Configure el diseño del componente de vídeo base en la página.
1. Active el diseño cuando haya terminado con los cambios de diseño.
