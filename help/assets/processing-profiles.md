---
title: Perfiles para procesar metadatos, imágenes y vídeos
description: Un perfil contiene un conjunto de reglas en torno a las opciones que se van a aplicar a los recursos cargados en una carpeta. Especifique el perfil de metadatos y el perfil de codificación de vídeo que se aplicarán a los recursos de vídeo que cargue. Para los recursos de imagen, también puede especificar el perfil de imagen que se aplicará a los recursos de imagen para que se recorten correctamente.
uuid: 6ded2a2f-a0d3-4f43-af97-02fbc0902c25
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: b555bf0c-44cb-4fbf-abc4-15971663904d
docset: aem65
translation-type: tm+mt
source-git-commit: 141a1783f275c0b3587ebc374bde19a21e107409
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 1%

---


# Perfiles para procesar metadatos, imágenes y vídeos{#profiles-for-processing-metadata-images-and-videos}

Un perfil es una fórmula para determinar las opciones que se aplican a los recursos que se cargan en una carpeta. Por ejemplo, puede especificar el perfil de metadatos y el perfil de codificación de vídeo que se aplicarán a los recursos de vídeo que cargue. O bien, qué perfil de imagen aplicar a los recursos de imagen para recortarlos correctamente.

Estas reglas pueden incluir la adición de metadatos, el recorte inteligente de imágenes o el establecimiento de perfiles de codificación de vídeo. En AEM, puede crear tres tipos de perfiles, que se tratan en detalle en los vínculos siguientes:

* [Perfiles de metadatos](/help/assets/metadata-config.md#metadata-profiles)
* [Perfiles de imagen](/help/assets/image-profiles.md)
* [Perfiles de vídeo](/help/assets/video-profiles.md)

Debe tener derechos de administrador para crear, editar y eliminar metadatos, imágenes o perfiles de vídeo.

Después de crear los metadatos, las imágenes o el perfil de vídeo, se asignan a una o varias carpetas que se utilizan como destino para los recursos recién cargados.

Un concepto importante con respecto al uso de perfiles en AEM Assets es que están asignados a carpetas. Dentro de un perfil hay ajustes en forma de perfiles de metadatos, junto con perfiles de vídeo o perfiles de imagen. Esta configuración procesa el contenido de una carpeta junto con cualquiera de sus subcarpetas. Por lo tanto, la forma en que se asignan nombres a los archivos y las carpetas, la forma en que se organizan las subcarpetas y la forma en que se gestionan los archivos de estas carpetas influye considerablemente en la forma en que un perfil procesa dichos recursos.
Al utilizar estrategias de asignación de nombres de archivos y carpetas coherentes y adecuadas, junto con una buena práctica de metadatos, puede sacar el máximo partido de la colección de recursos digitales y asegurarse de que el perfil correcto procesa los archivos adecuados.

>[!NOTE]
>
>Los recursos que se mueven de una carpeta a otra no se vuelven a procesar. Por ejemplo, supongamos que tiene la carpeta 1 con el perfil A asignado y la carpeta 2 con el perfil B asignado. Si mueve recursos de la carpeta 1 a la carpeta 2, los recursos movidos conservarán su procesamiento original desde la carpeta 1.
>
>Lo mismo sucede incluso cuando se mueven recursos entre dos carpetas que tienen el mismo perfil asignado.

## Reprocesamiento de recursos en una carpeta {#reprocessing-assets}

>[!NOTE]
>
>Se aplica a *Dynamic Media - modo Scene7* solo en AEM 6.4.6.0 o posterior.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de procesamiento existente que haya cambiado posteriormente.

Por ejemplo, supongamos que ha creado un perfil de imagen y lo ha asignado a una carpeta. Los recursos de imagen que haya cargado en la carpeta se aplicarán automáticamente al perfil de imagen. Sin embargo, posteriormente se decide agregar una nueva proporción de recorte inteligente al perfil. Ahora, en lugar de volver a seleccionar y cargar los recursos en la carpeta, simplemente ejecute el *Scene7: Volver a procesar el flujo de trabajo de Assets*.

Puede ejecutar el flujo de trabajo de reprocesamiento en un recurso cuyo procesamiento haya fallado por primera vez. Por lo tanto, aunque no haya editado un perfil de procesamiento o aplicado un perfil de procesamiento, podrá seguir ejecutando el flujo de trabajo de reprocesamiento en una carpeta de recursos en cualquier momento.

Opcionalmente, puede ajustar el tamaño del lote del flujo de trabajo de reprocesamiento de un valor predeterminado de 50 recursos a 1000. Al ejecutar el _Scene7: Volver a procesar el flujo de trabajo de Assets_ en una carpeta, los recursos se agrupan en lotes y luego se envían al servidor de Dynamic Media para su procesamiento. Tras el procesamiento, los metadatos de cada recurso en todo el conjunto de lotes se actualizan en AEM. Si el tamaño del lote es muy grande, puede experimentar un retraso en el procesamiento. O bien, si el tamaño del lote es demasiado pequeño, puede causar demasiados viajes de ida y vuelta al servidor de Dynamic Media.

Consulte [Ajuste del tamaño de lote del flujo de trabajo de reprocesamiento](#adjusting-load).

>[!NOTE]
>
>Si está realizando una migración masiva de recursos de Dynamic Media Classic a AEM, debe habilitar el agente de replicación de migración en el servidor Dynamic Media. Una vez completada la migración, asegúrese de desactivar el agente.
>
>El agente de publicación de migración debe estar deshabilitado en el servidor de Dynamic Media para que el flujo de trabajo de reprocesamiento funcione según lo esperado.

<!-- Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. -->

**Para volver a procesar los recursos de una carpeta**:
1. En AEM, en la página Recursos, navegue a una carpeta de recursos que tenga un perfil de procesamiento asignado y para la que desee aplicar el **Scene7: Flujo de trabajo de reprocesamiento de recursos**,

   Las carpetas que ya tienen un perfil de procesamiento asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta en la Vista de tarjetas.

1. Seleccione una carpeta.

   * El flujo de trabajo tiene en cuenta todos los archivos de la carpeta seleccionada de forma recursiva.
   * Si hay una o varias subcarpetas con recursos en la carpeta principal seleccionada, el flujo de trabajo volverá a procesar todos los recursos en la jerarquía de carpetas.
   * Se recomienda evitar ejecutar este flujo de trabajo en una jerarquía de carpetas con más de 1000 recursos.

1. Cerca de la esquina superior izquierda de la página, en la lista desplegable, haga clic en **[!UICONTROL Cronología.]**
1. Cerca de la esquina inferior izquierda de la página, a la derecha del campo Comentario, haga clic en el icono del carro ( **^** ) .

   ![Flujo de trabajo de reprocesamiento de recursos 1](/help/assets/assets/reprocess-assets1.png)

1. Haga clic en **[!UICONTROL Flujo de trabajo de Inicio.]**
1. En la lista desplegable **[!UICONTROL Flujo de trabajo de Inicio]**, elija **[!UICONTROL Scene7: Volver a procesar los recursos.]**
1. (Opcional) En el campo de texto **Escriba el título del flujo de trabajo**, escriba un nombre para el flujo de trabajo. Puede utilizar el nombre para hacer referencia a la instancia de flujo de trabajo, si es necesario.

   ![Volver a procesar los recursos 2](/help/assets/assets/reprocess-assets2.png)

1. Haga clic en **[!UICONTROL Inicio]** y luego haga clic en **[!UICONTROL Confirmar.]**

   Para supervisar el flujo de trabajo o comprobar su progreso, en la página de la consola principal de AEM, haga clic en **[!UICONTROL Herramientas > Flujo de trabajo.]** En la página Instancias de flujo de trabajo, seleccione un flujo de trabajo. En la barra de menús, haga clic en **[!UICONTROL Abrir historial.]** También puede finalizar, suspender o cambiar el nombre de un flujo de trabajo seleccionado desde la misma página Instancias de flujo de trabajo.

### Ajuste del tamaño del lote del flujo de trabajo de reprocesamiento {#adjusting-load}

(Opcional) El tamaño de lote predeterminado en el flujo de trabajo de reprocesamiento es de 50 recursos por trabajo. Este tamaño óptimo de lote se rige por el tamaño medio del recurso y los tipos MIME de los recursos en los que se ejecuta el reprocesamiento. Un valor más alto significa que tendrá muchos archivos en un solo trabajo de reprocesamiento. En consecuencia, la pancarta de procesamiento permanece en AEM recursos durante más tiempo. Sin embargo, si el tamaño medio del archivo es pequeño-1 MB o menos-Adobe, se recomienda aumentar el valor a varios cientos, pero nunca más de 1000. Si el tamaño medio de archivo es de cientos de megabytes de Adobe, se recomienda reducir el tamaño del lote hasta 10.

**Ajuste opcional del tamaño del lote del flujo de trabajo de reprocesamiento**

1. En Experience Manager, haga clic en **[!UICONTROL Adobe Experience Manager]** para acceder a la consola de navegación global y, a continuación, haga clic en el icono **[!UICONTROL Herramientas]** (martillo) > **[!UICONTROL Flujo de trabajo > Modelos.]**
1. En la página Modelos de flujo de trabajo, en Vista de tarjeta o Vista de Lista, seleccione **[!UICONTROL Scene7: Volver a procesar los recursos]**.

   ![Página Modelos de Flujo de Trabajo con Scene7: Volver a procesar los recursos seleccionados en la Vista de tarjetas](/help/assets/assets-dm/reprocess-assets7.png)

1. En la barra de herramientas, haga clic en **[!UICONTROL Editar.]** Una nueva ficha de explorador abre el Scene7: Volver a procesar la página del modelo de flujo de trabajo de Recursos.
1. En el Scene7: Volver a procesar la página de flujo de trabajo Recursos, cerca de la esquina superior derecha, haga clic en **[!UICONTROL Editar]** para &quot;desbloquear&quot; el flujo de trabajo.
1. En el flujo de trabajo, seleccione el componente Carga por lotes de Scene7 para abrir la barra de herramientas y, a continuación, haga clic en **[!UICONTROL Configurar]** en la barra de herramientas.

   ![Componente de carga por lotes de Scene7](/help/assets/assets-dm/reprocess-assets8.png)

1. En el cuadro de diálogo **[!UICONTROL Carga por lotes en Scene7—Step Properties]**, establezca lo siguiente:
   * En los campos de texto **[!UICONTROL Título]** y **[!UICONTROL Descripción]**, introduzca un nuevo título y una descripción para el trabajo, si lo desea.
   * Seleccione **[!UICONTROL Avance del controlador]** si el controlador avanzará al paso siguiente.
   * En el campo **[!UICONTROL Tiempo de espera]**, introduzca el tiempo de espera del proceso externo (segundos).
   * En el campo **[!UICONTROL Período]**, introduzca un intervalo de sondeo (segundos) para probar la finalización del proceso externo.
   * En el campo **[!UICONTROL Lote]**, introduzca el número máximo de recursos (50-1000) que se procesarán en un trabajo de carga de procesamiento por lotes de Dynamic Media Server.
   * Seleccione **[!UICONTROL Avanzar al tiempo de espera]** si desea avanzar cuando se alcance el tiempo de espera. Anule la selección si desea continuar con la bandeja de entrada cuando se alcance el tiempo de espera.

   ![Cuadro de diálogo Propiedades](/help/assets/assets-dm/reprocess-assets3.png)

1. En la esquina superior derecha del cuadro de diálogo **[!UICONTROL Carga por lotes en Scene7 - Propiedades del paso]**, haga clic en **[!UICONTROL Listo]**.

1. En la esquina superior derecha del Scene7: Volver a procesar la página del modelo de flujo de trabajo de Recursos, haga clic en **[!UICONTROL Sincronizar]**. Cuando ve **[!UICONTROL Sincronizado]**, el modelo de tiempo de ejecución del flujo de trabajo se sincroniza correctamente y está listo para volver a procesar los recursos en una carpeta.

   ![Sincronización del modelo de flujo de trabajo](/help/assets/assets-dm/reprocess-assets1.png)

1. Cierre la ficha del explorador que muestra el Scene7: Volver a procesar el modelo de flujo de trabajo de Recursos.

<!--1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, click **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then click the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite.]**
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/assets/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, click **[!UICONTROL Add.]** The new property appears as the following:

    ![Saving the new property](/help/assets/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, click **[!UICONTROL Save All.]**
1. In the upper-left corner of the page, click **[!UICONTROL CRXDE Lite]** to return to the main AEM console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.-->
