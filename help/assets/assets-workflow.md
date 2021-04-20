---
title: Procesamiento de recursos mediante flujos de trabajo
description: Procesamiento de recursos para convertir formatos, crear representaciones, administrar recursos, validar recursos y ejecutar flujos de trabajo.
contentOwner: AG
feature: Workflow, Renditions
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 3%

---


# Procesar recursos digitales {#process-assets}

[!DNL Adobe Experience Manager Assets] le permite trabajar en sus recursos digitales de muchas maneras para permitir un procesamiento de recursos robusto. Puede utilizar los métodos de procesamiento predeterminados o personalizados para garantizar la finalización de procesos empresariales integrales, auditorías y cumplimiento de normas, descubrimiento y distribución, y la sanidad básica de sus recursos digitales. Puede realizar las tareas de administración de recursos y lograr la escala y personalización necesarias.

## Comprender los flujos de trabajo {#understand-workflows}

Para el procesamiento de recursos, [!DNL Experience Manager] utiliza flujos de trabajo. Los flujos de trabajo ayudan a automatizar la lógica empresarial o las actividades. De forma predeterminada, se proporcionan pasos granulares para realizar tareas específicas y los desarrolladores pueden crear sus propios pasos personalizados. Estos pasos se pueden combinar en un orden lógico para crear flujos de trabajo. Por ejemplo, un flujo de trabajo puede aplicar una marca de agua en las imágenes cargadas según un criterio específico, como la carpeta a la que se carga, la resolución de la imagen, etc. Otro ejemplo es un flujo de trabajo configurado para marcar con agua y añadir simultáneamente metadatos, crear representaciones, agregar etiquetas inteligentes y publicar en un almacén de datos.

## Flujos de trabajo predeterminados disponibles en [!DNL Experience Manager] {#default-workflows}

De forma predeterminada, todos los recursos cargados se procesan mediante el flujo de trabajo [!UICONTROL DAM Update Asset]. El flujo de trabajo se ejecuta para cada recurso cargado y realiza tareas básicas de administración de recursos, como la generación de representación, la reescritura de metadatos, la extracción de páginas, la extracción de medios y la transcodificación.

Para ver los distintos modelos de flujo de trabajo disponibles de forma predeterminada, consulte **[!UICONTROL Tools > Workflow > Models]** en [!DNL Experience Manager].

![Algunos de los flujos de trabajo predeterminados](assets/aem-default-workflows.png)

*Figura: Algunos de los flujos de trabajo predeterminados disponibles en  [!DNL Experience Manager].*

## Aplicar flujos de trabajo para procesar recursos {#applying-workflows-to-assets}

La aplicación de flujos de trabajo a recursos digitales es la misma que para las páginas de sitios web. Para obtener una guía completa sobre cómo crear y utilizar flujos de trabajo, consulte [iniciar flujos de trabajo](/help/sites-authoring/workflows-participating.md).

Utilice flujos de trabajo en recursos digitales para activar el recurso o crear marcas de agua. Muchos de los flujos de trabajo de los recursos se activan automáticamente. Por ejemplo, el flujo de trabajo que crea automáticamente una representación después de editar una imagen está activado automáticamente.

>[!NOTE]
>
>Si un flujo de trabajo disponible en la IU clásica no está disponible en la IU táctil, como [!UICONTROL Solicitud de activación] y [!UICONTROL Solicitud de desactivación], consulte [Creación de modelos de flujo de trabajo](/help/sites-developing/workflows-models.md#classic2touchui).

## Aplicar un flujo de trabajo a un recurso {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
Para aplicar un flujo de trabajo a un recurso, siga estos pasos:

1. Vaya a la ubicación del recurso para el que desea iniciar un flujo de trabajo y haga clic en el recurso para abrir la página del recurso. Seleccione **[!UICONTROL Línea de tiempo]** en el menú para mostrar la línea de tiempo.

   ![línea de tiempo-1](assets/timeline.png)

1. Haga clic en **[!UICONTROL Actions]** en la parte inferior para abrir la lista de acciones disponibles para el recurso.

1. Haga clic en **[!UICONTROL Iniciar flujo de trabajo]** en la lista.

1. En el cuadro de diálogo **[!UICONTROL Iniciar flujo de trabajo]**, seleccione un modelo de flujo de trabajo de la lista.

1. (Opcional) Especifique un título para el flujo de trabajo que se puede utilizar para hacer referencia a la instancia del flujo de trabajo.

   ![seleccione flujo de trabajo, proporcione un título y haga clic en iniciar](assets/start-workflow.png)

1. Haga clic en **[!UICONTROL Inicio]** y, a continuación, haga clic en **[!UICONTROL Continuar]**. Cada paso del flujo de trabajo se muestra en la cronología como un evento.

   ![chlimage_1-256](assets/chlimage_1-52.png)

## Aplicar un flujo de trabajo a varios recursos {#applying-a-workflow-to-multiple-assets}

1. Desde la consola [!DNL Assets], vaya a la ubicación de los recursos para los que desea iniciar un flujo de trabajo y seleccione los recursos. Seleccione **[!UICONTROL Línea de tiempo]** en el menú para mostrar la línea de tiempo.

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. Haga clic en **[!UICONTROL Actions]** ![cheurón hacia arriba](assets/do-not-localize/chevron-up-icon.png) en la parte inferior.
1. Haga clic en **[!UICONTROL Iniciar flujo de trabajo]**. En el cuadro de diálogo **[!UICONTROL Iniciar flujo de trabajo]**, seleccione un modelo de flujo de trabajo de la lista.

   ![iniciar flujo de trabajo](assets/start-workflow.png)

1. (Opcional) Especifique un título para el flujo de trabajo, que se puede utilizar para hacer referencia a la instancia de flujo de trabajo.
1. Haga clic en **[!UICONTROL Iniciar]** y, a continuación, en **[!UICONTROL Confirmar]** en el cuadro de diálogo. El flujo de trabajo se ejecuta en todos los recursos seleccionados.

## Aplicar un flujo de trabajo a varias carpetas {#applying-a-workflow-to-multiple-folders}

El procedimiento para aplicar un flujo de trabajo a varias carpetas es similar al procedimiento para aplicar un flujo de trabajo a varios recursos. Seleccione las carpetas en la interfaz [!DNL Assets] y realice los pasos 2 a 7 del procedimiento [aplicar un flujo de trabajo a varios recursos](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets).

## Aplicar un flujo de trabajo a una colección {#applying-a-workflow-to-a-collection}

Consulte [aplicar un flujo de trabajo en una colección](/help/assets/manage-collections.md#running-a-workflow-on-a-collection).

## Inicie automáticamente un flujo de trabajo para procesar los recursos de forma condicional {#auto-execute-workflow-on-some-assets}

Los administradores pueden configurar el flujo de trabajo para que ejecuten y procesen automáticamente los recursos en función de condiciones predefinidas. La funcionalidad es útil para los usuarios de la línea de negocios y los especialistas en marketing, por ejemplo, para crear un flujo de trabajo personalizado en carpetas específicas. Digamos que todos los activos de la sesión fotográfica de una agencia pueden estar marcados con agua o que todos los activos cargados por un profesional independiente pueden procesarse para crear representaciones específicas.

Para un modelo de flujo de trabajo, los usuarios pueden crear un iniciador de flujo de trabajo que lo ejecute. Un iniciador de flujo de trabajo supervisa los cambios en el repositorio de contenido y ejecuta el flujo de trabajo cuando se cumplen las condiciones predefinidas. Los administradores pueden proporcionar acceso a los especialistas en marketing para crear los flujos de trabajo y configurar el lanzador. Los usuarios pueden modificar el flujo de trabajo predeterminado [!UICONTROL Activo de actualización de DAM] para añadir los pasos adicionales necesarios para procesar recursos específicos. El flujo de trabajo se ejecuta en todos los recursos cargados recientemente. Utilice uno de los siguientes métodos para limitar la ejecución de los pasos adicionales en recursos específicos:

* Haga una copia del flujo de trabajo [!UICONTROL DAM Update Asset] y modifíquelo para que se ejecute en una jerarquía de carpetas específica. Este método es útil para algunas carpetas.
* Los pasos de procesamiento adicionales se pueden agregar utilizando una [OR división](/help/sites-developing/workflows-step-ref.md#or-split) como se aplica condicionalmente a tantas carpetas como sea necesario.

## Prácticas recomendadas y limitaciones {#best-practices-limitations-tips}

* Tenga en cuenta sus necesidades para todos los tipos de representaciones al diseñar flujos de trabajo. Si no prevé la necesidad de una representación en el futuro, elimine su paso de creación del flujo de trabajo. Las representaciones no se pueden eliminar de forma masiva posteriormente. Las representaciones no deseadas pueden ocupar mucho espacio de almacenamiento después de un uso prolongado de [!DNL Experience Manager]. Para recursos individuales, puede eliminar las representaciones manualmente desde la interfaz de usuario. Para varios recursos, puede personalizar [!DNL Experience Manager] para eliminar representaciones específicas o eliminar los recursos y volver a cargarlos.
* De forma predeterminada, el flujo de trabajo [!UICONTROL Activo de actualización de DAM] incluye algunos pasos para crear miniaturas y representaciones web. Si se eliminan todas las representaciones predeterminadas del flujo de trabajo, la interfaz de usuario de [!DNL Assets] no se procesa correctamente.

>[!MORELIKETHIS]
>
>* [Aplicar y participar en flujos de trabajo](/help/sites-authoring/workflows.md)
>* [Creación de modelos de flujo de trabajo y ampliación de la funcionalidad del flujo de trabajo](/help/sites-developing/workflows.md)
>* [Métodos para ejecutar flujos de trabajo](/help/sites-administering/workflows-starting.md)
>* [Prácticas recomendadas del flujo de trabajo](/help/sites-developing/workflows-best-practices.md)

