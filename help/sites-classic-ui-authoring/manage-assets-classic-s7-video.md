---
title: El vídeo
seo-title: Vídeo
description: Assets proporciona un sistema de administración de recursos de vídeo centralizada en que puede cargar vídeos directamente en Assets para autocodificarlos en Scene7 y acceder directamente a los vídeos de Scene7 desde Assets para la creación de páginas.
seo-description: Assets proporciona un sistema de administración de recursos de vídeo centralizada en que puede cargar vídeos directamente en Assets para autocodificarlos en Scene7 y acceder directamente a los vídeos de Scene7 desde Assets para la creación de páginas.
uuid: 46da7a0d-d17b-4716-a304-ce5496421b5a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dfaa4b3f-f65a-4fe3-87a7-f3bc71015e56
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Vídeo{#video}

Assets permite gestionar recursos de vídeo centralizados, donde puede cargar vídeos directamente en Recursos para codificarlos automáticamente en Dynamic Media Classic y acceder a vídeos de Dynamic Media Classic directamente desde Recursos para la creación de páginas.

La integración de vídeo de Dynamic Media Classic amplía el alcance del vídeo optimizado a todas las pantallas (detección de ancho de banda y dispositivo automático).

* El componente de vídeo de Dynamic Media Classic (Scene7) realiza automáticamente la detección del ancho de banda y el dispositivo para reproducir el formato correcto y el vídeo de calidad correcta en equipos de escritorio, tabletas y dispositivos móviles.
* Assets: puede incluir conjuntos de vídeos adaptables en lugar de solo recursos de vídeo únicos. Un conjunto de vídeos adaptables es un contenedor para todas las representaciones de vídeo necesarias para reproducir vídeo sin problemas en varias pantallas. Un conjunto de vídeos adaptable agrupa versiones del mismo vídeo codificadas con diferentes velocidades de bits y formatos, como 400 kbps, 800 kbps y 1000 kbps. Un conjunto de vídeos adaptables, junto con el componente de vídeo de S7, se utiliza para trasmitir vídeo adaptable en varias pantallas, incluidos equipos de escritorio, iOS, Android, Blackberry y dispositivos móviles de Windows. Consulte [Documentación de Scene7 sobre los conjuntos de vídeos adaptables](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html) para obtener más información.

## Acerca de FFMPEG y Dynamic Media Classic {#about-ffmpeg-and-scene}

El proceso de codificación de vídeo predeterminado se basa en el uso de la integración basada en FFMPEG con los perfiles de vídeo. Por tanto, el flujo de trabajo de Actualizar recurso de DAM listo para usar contiene los dos pasos siguientes de flujo de trabajo basados en FFMPEG:

* Miniaturas de FFMPEG
* Codificación de FFMPEG

Tenga en cuenta que al habilitar y configurar la integración de Dynamic Media Classic no se eliminan ni se desactivan automáticamente estos dos pasos del flujo de trabajo de inserción de recursos de actualización de DAM incorporado. Si ya utiliza codificación de vídeo basada en FFMPEG en AEM, es probable que tenga FFMPEG instalado en sus entornos de creación. En este caso, un nuevo vídeo ingestado con Recursos se codificaría dos veces: una vez desde el codificador FFMPEG y otra desde la integración de Dynamic Media Classic.

Si tiene la codificación de vídeo basada en FFMPEG configurada en AEM y FFMPEG instalado, Adobe recomienda quitar los dos flujos de trabajo de FFMPEG de los flujos de trabajo de Actualizar recurso de DAM.

### Formatos admitidos {#supported-formats}

El componente Vídeo de Dynamic Media Classic admite los siguientes formatos:

* F4V H.264
* MP4 H.264

### Decidir dónde cargar el vídeo {#deciding-where-to-upload-your-video}

Decidir dónde cargar los recursos de vídeo depende de las acciones siguientes:

* ¿Necesita un flujo de trabajo para el recurso de vídeo?
* ¿Necesita un control de versión para el recurso de vídeo?

Si la respuesta es “sí” a una o ambas preguntas, cargue el vídeo directamente en Adobe DAM. Si la respuesta es &quot;no&quot; a ambas preguntas, cargue el vídeo directamente en Dynamic Media Classic. El flujo de trabajo de cada escenario se describe en la sección siguiente.

#### Si está cargando el vídeo directamente en Adobe Assets {#if-you-are-uploading-your-video-directly-to-adobe-assets}

Si necesita un flujo de trabajo o crear versiones de sus recursos, primero debe cargar en Adobe Assets. El flujo de trabajo siguiente es el recomendado:

1. Cargue el recurso de vídeo en Adobe Assets y codifique y publique automáticamente en Dynamic Media Classic.
1. En AEM, acceda a los recursos de vídeo de WCM en la pestaña **[!UICONTROL Películas]** del buscador de contenido.
1. Autor con vídeo de Dynamic Media Classic o componente de vídeo de base.

#### Si va a cargar el vídeo en Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Si no necesita un flujo de trabajo o una versión para los recursos, debe cargar los recursos a Dynamic Media Classic. El flujo de trabajo siguiente es el recomendado:

1. En Dynamic Media Classic, [configure una carga y codificación de FTP programadas en Dynamic Media Classic (sistema automatizado)](https://help.adobe.com/en_US/scene7/using/WS70B173EC-4CAD-4b4c-BF9C-43A11F3A5950.html).
1. In AEM, access video assets in WCM in the **[!UICONTROL Dynamic Media Classic]** tab of the Content Finder.
1. Autor con el componente de vídeo de Dynamic Media Classic.

### Configuración de la integración con vídeo de Dynamic Media Classic {#configuring-integration-with-scene-video}

**Para configurar los ajustes preestablecidos universales**:

1. In **[!UICONTROL Cloud Services]**, navigate to your **[!UICONTROL Dynamic Media Classic]** configuration and click **[!UICONTROL Edit]**.
1. Seleccione la pestaña **[!UICONTROL Vídeo]**.

   >[!NOTE]
   >
   >La pestaña **[!UICONTROL Vídeo]** no aparece si la página no tiene una configuración de nube. Consulte [Activación de Dynamic Media Classic para WCM](#enablingscene7forwcm).

1. Seleccione el perfil de codificación de vídeo adaptable, un perfil de codificación de vídeo único listo para usar o un perfil de codificación de vídeo personalizado.

   >[!NOTE]
   >
   >For more information about what the video presets mean, see the [Dynamic Media Classic documentation](https://help.adobe.com/en_US/scene7/using/WSE86ACF2B-BD50-4c48-A1D7-9CD4405B62D0.html).
   >
   >Adobe recomienda que seleccione ambos conjuntos de vídeos adaptables al configurar los ajustes preestablecidos universales o que seleccione la opción **[!UICONTROL Codificación de vídeo adaptable]**.

1. Los perfiles de codificación seleccionados se aplican automáticamente a todos los vídeos cargados en la carpeta de destino de CQ DAM configurada para esta configuración de nube de Dynamic Media Classic. Puede configurar varias configuraciones de nube de Dynamic Media Classic con distintas carpetas de destino para aplicar distintos perfiles de codificación según sea necesario.

### Actualizar los ajustes preestablecidos del visor y de codificación {#updating-viewer-and-encoding-presets}

If you need to update the viewer and encoding presets for video in AEM because the presets have been updated in Dynamic Media Classic, navigate to the Dynamic Media Classic configuration in the cloud configuration and click **Update the viewer and encoding presets**.

![chlimage_1-135](assets/chlimage_1-131.png)

### Cargar el vídeo maestro {#uploading-your-master-video}

Para cargar el vídeo principal en Dynamic Media Classic desde Adobe DAM:

1. Vaya a la carpeta de destino de CQ DAM donde ha configurado la configuración de nube con perfiles de codificación de Dynamic Media Classic.
1. Haga clic en **[!UICONTROL Cargar]** para cargar el vídeo maestro. Video uploading and encoding is complete after the [!UICONTROL DAM Update Asset] workflow is complete and **[!UICONTROL Publish to Dynamic Media Classic]** has a checkmark.

   >[!NOTE]
   >
   >Puede que pase un tiempo hasta que las miniaturas de vídeo se generen.

   Dragging the DAM master video on to the video component accesses *all* of the Dynamic Media Classic encoded proxy renditions for delivery.

### Componente de vídeo de base frente a componente de vídeo de Dynamic Media Classic {#foundation-video-component-versus-scene-video-component}

Al utilizar AEM, tiene acceso al componente Vídeo disponible en Sitios y al componente de vídeo de Dynamic Media Classic (Scene7). Dichos componentes no son intercambiables.

El componente de vídeo de Dynamic Media Classic solo funciona para vídeos de Dynamic Media Classic. El componente de base funciona con vídeos almacenados desde AEM (mediante ffmpeg) y vídeos de Dynamic Media Classic.

En la matriz siguiente se explica cuándo debe utilizar el componente:

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>De forma predeterminada, el componente de vídeo de Dynamic Media Classic utiliza el perfil de vídeo universal. Sin embargo, puede obtener el reproductor de vídeo basado en HTML5 para que lo utilice AEM. En Dynamic Media Classic, copie el código incrustado del reproductor de vídeo HTML5 incorporado y colóquelo en su página de AEM.


## Componente de vídeo de AEM {#aem-video-component}

Incluso si se recomienda utilizar el componente de vídeo de Dynamic Media Classic para ver vídeos de Dynamic Media Classic, en esta sección se describe el uso de vídeos de Dynamic Media Classic con el componente [!UICONTROL de vídeo] Foundation en AEM, en aras de la integridad.

### Comparación de vídeo de AEM Video y Dynamic Media Classic {#aem-video-and-scene-video-comparison}

En la tabla siguiente se proporciona una comparación de alto nivel de capacidades admitidas entre el componente de vídeo base de AEM y el componente de vídeo de Scene7:

|  | Vídeo base de AEM | Vídeo de Dynamic Media Classic |
|---|---|---|
| Enfoque | Primer enfoque de HTML5. Flash solo se utiliza para la alternativa no HTML5. | Flash en la mayoría de los equipos de escritorio. HTML5 se utiliza para móviles y tabletas. |
| Entrega | Progresivo | Transmisión adaptable |
| Seguimiento | Sí | Sí |
| Capacidad de ampliación | Sí | Sí (con el SDK de visor de Dynamic Media Classic) |
| Vídeo móvil | Sí | Sí |

### Configuración {#setting-up}

#### Creación de perfiles de vídeo {#creating-video-profiles}

Las distintas codificaciones de vídeo se crean según los ajustes preestablecidos de codificación de Dynamic Media Classic seleccionados en la configuración de nube de Dynamic Media Classic. Para que el componente de vídeo de base pueda utilizarlos, se debe crear un perfil de vídeo para cada ajuste preestablecido de codificación de Dynamic Media Classic seleccionado. Esto permite que el componente de vídeo seleccione las representaciones de DAM según corresponda.

>[!NOTE]
>
>Los perfiles de vídeo nuevos, así como los cambios que se realicen en ellos, deben activarse para publicarse.

1. En AEM, vaya a **[!UICONTROL Herramientas]** y seleccione **[!UICONTROL Consola de configuración]**. In the Configuration Console navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Video Profiles]** in the navigation tree.
1. Cree un nuevo perfil de vídeo de Dynamic Media Classic. **[!UICONTROL En el]** Nuevo... , seleccione **[!UICONTROL Crear página]** y, a continuación, la plantilla Perfil de vídeo de Dynamic Media Classic. Asigne un nombre a la página nueva del perfil de vídeo y haga clic en **[!UICONTROL Crear]**.

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. Edite el nuevo perfil de vídeo. Seleccione primero la configuración de nube. A continuación, seleccione el mismo ajuste preestablecido de codificación que el que se ha seleccionado en la configuración de nube.

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | Propiedad | Descripción |
   |---|---|
   | Configuración de nube de Dynamic Media Classic (Scene7) | La configuración de nube que se va a utilizar para los ajustes preestablecidos de codificación. |
   | Ajuste preestablecido de codificación de Dynamic Media Classic (Scene7) | El ajuste preestablecido de codificación con el que se asignará este perfil de vídeo. |
   | Tipo de vídeo HTML5 | Esta propiedad permite establecer el valor de la propiedad type del elemento de origen de vídeo HTML5. Esta información no se proporciona en los ajustes preestablecidos de codificación de Dynamic Media Classic, sino que se requiere para procesar correctamente los vídeos con el elemento de vídeo HTML5. Se proporciona una lista de los formatos comunes, pero se pueden sobrescribir por otros formatos. |

   Repita este paso para todos los ajustes preestablecidos de codificación seleccionados en la configuración de nube que desea utilizar en el componente de vídeo.

#### Configuración del diseño {#configuring-design}

El componente de vídeo base debe saber qué perfiles de vídeo se van a utilizar para crear la lista de orígenes de vídeo. Debe abrir el cuadro de diálogo de diseño de los componentes de vídeo y configurar el diseño de los componentes para utilizar los perfiles de vídeo nuevos.

>[!NOTE]
>
>Si utiliza el componente de vídeo base en una página móvil, es posible que deba repetir estos pasos en el diseño de la página móvil.

>[!NOTE]
>
>Los cambios realizados en el diseño requieren la activación del diseño para que surtan efecto en la publicación.

1. Abra el cuadro de diálogo de diseño del componente de vídeo base y cambie a la pestaña **[!UICONTROL Perfiles]**. A continuación, elimine los perfiles predeterminados y agregue los nuevos perfiles de vídeo de Dynamic Media Classic. El orden de la lista de perfiles en el cuadro de diálogo de diseño también define el orden del elemento de orígenes de vídeo al realizar el procesamiento.
1. Para los navegadores que no admiten HTML5, el componente de vídeo permite configurar una alternativa flash. Abra el cuadro de diálogo de diseño de los componentes de vídeo y cambie a la pestaña **[!UICONTROL Flash]**. Configure las opciones de configuración de Flash Player y asigne un perfil alternativo para Flash Player.

#### Lista de comprobación {#checklist}

1. Cree una configuración de nube de Dynamic Media Classic (Scene7). Asegúrese de que los ajustes preestablecidos de codificación de vídeo se hayan establecido y de que el importador se esté ejecutando.
1. Cree un perfil de vídeo de Dynamic Media Classic para cada ajuste preestablecido de codificación de vídeo seleccionado en la configuración de nube.
1. Los perfiles de vídeo deben estar activados.
1. Configure el diseño del componente de vídeo base en la página.
1. Active el diseño cuando haya terminado con los cambios de diseño.

