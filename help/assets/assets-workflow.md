---
title: Procesar recursos para llevar a cabo procesos de negocios, realizar auditorías, lograr cumplimiento de normas y mantener la solidez básica
description: Procesamiento de recursos para convertir formatos, crear representaciones, administrar recursos, validar recursos y ejecutar flujos de trabajo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: f6c770e8830bd2fe7c436c4bfe9725564c49a08f
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 3%

---


# Procesar recursos digitales {#process-assets}

[!DNL Adobe Experience Manager Assets] le permite trabajar en sus recursos digitales de muchas maneras para permitir un procesamiento sólido de los recursos. Puede utilizar los métodos de procesamiento predeterminados o personalizados para garantizar la finalización completa de los procesos empresariales, las auditorías y el cumplimiento de normas, el descubrimiento y la distribución, y la solidez básica de sus activos digitales. Puede realizar las tareas de administración de recursos y, al mismo tiempo, lograr la escala y personalización necesarias.

## Comprender los flujos de trabajo {#understand-workflows}

Para el procesamiento de recursos, [!DNL Experience Manager] utiliza flujos de trabajo. Los Flujos de trabajo ayudan a automatizar las actividades o la lógica empresarial. De forma predeterminada, se proporcionan pasos granulares para realizar tareas específicas y los desarrolladores pueden crear sus propios pasos personalizados. Estos pasos se pueden combinar en un orden lógico para crear flujos de trabajo. Por ejemplo, un flujo de trabajo puede aplicar una marca de agua a las imágenes cargadas según criterios específicos, como la carpeta en la que se carga, la resolución de la imagen, etc. Otro ejemplo es un flujo de trabajo configurado para marcar con agua y agregar metadatos simultáneamente, crear representaciones, agregar etiquetas inteligentes y publicar en un almacén de datos.

## flujos de trabajo predeterminados disponibles en [!DNL Experience Manager] {#default-workflows}

De forma predeterminada, todos los recursos cargados se procesan mediante el flujo de trabajo Actualizar recursos  DAM. El flujo de trabajo se ejecuta para cada recurso cargado y lleva a cabo tareas básicas de administración de recursos, como la generación de representaciones, la reescritura de metadatos, la extracción de páginas, la extracción de medios y la transcodificación.

Para ver los distintos modelos de flujo de trabajo disponibles de forma predeterminada, consulte **[!UICONTROL Herramientas > Flujo de trabajo > Modelos]** en [!DNL Experience Manager].

![Parte del flujo de trabajo predeterminado](assets/aem-default-workflows.png)

*Figura: Algunos de los flujos de trabajo predeterminados disponibles en[!DNL Experience Manager].*

## Aplicar flujos de trabajo para procesar recursos {#applying-workflows-to-assets}

La aplicación de flujos de trabajo a los recursos digitales es la misma que para las páginas del sitio web. Para obtener una guía completa sobre cómo crear y utilizar flujos de trabajo, consulte flujos de trabajo [de inicio](/help/sites-authoring/workflows-participating.md).

Utilice flujos de trabajo en recursos digitales para activar el recurso o crear marcas de agua. Muchos de los flujos de trabajo de los recursos se activan automáticamente. Por ejemplo, el flujo de trabajo que crea automáticamente una representación después de editar una imagen se activa automáticamente.

>[!NOTE]
>
>Si un flujo de trabajo disponible en la IU clásica no está disponible en la IU táctil, como [!UICONTROL Solicitud de activación] y [!UICONTROL Solicitud de desactivación], consulte [Creación de modelos](/help/sites-developing/workflows-models.md#classic2touchui)de flujo de trabajo.

## Aplicación de un flujo de trabajo a un recurso {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
Para aplicar un flujo de trabajo a un recurso, siga estos pasos:

1. Vaya a la ubicación del recurso para el que desea realizar el inicio de un flujo de trabajo y haga clic en el recurso para abrir la página de recursos. Seleccione **[!UICONTROL Línea de tiempo]** en el menú para mostrar la línea de tiempo.

   ![línea de tiempo-1](assets/timeline.png)

1. Haga clic en **[!UICONTROL Acciones]** en la parte inferior para abrir la lista de acciones disponibles para el recurso.

1. Haga clic en Flujo de trabajo **[!UICONTROL Inicio]** desde la lista.

1. In the **[!UICONTROL Start Workflow]** dialog, select a workflow model from the list.

   ![chlimage_1-254](assets/chlimage_1-50.png)

1. (Opcional) Especifique un título para el flujo de trabajo que pueda utilizarse para hacer referencia a la instancia del flujo de trabajo.

   ![chlimage_1-255](assets/chlimage_1-51.png)

1. Haga clic en **[!UICONTROL Inicio]** y, a continuación, en **[!UICONTROL Continuar]**. Cada paso del flujo de trabajo se muestra en la cronología como un evento.

   ![chlimage_1-256](assets/chlimage_1-52.png)

## Aplicación de un flujo de trabajo a varios recursos {#applying-a-workflow-to-multiple-assets}

1. Desde la consola Recursos, desplácese hasta la ubicación de los recursos para los que desea realizar el inicio en un flujo de trabajo y seleccione los recursos. Seleccione **[!UICONTROL Línea de tiempo]** en el menú para mostrar la línea de tiempo.

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. Haga clic en **[!UICONTROL Acciones]** en la parte inferior.

   ![chlimage_1-30](assets/chlimage_1-137.png)

1. Haga clic en Flujo de trabajo **[!UICONTROL de Inicio]**. In the **[!UICONTROL Start Workflow]** dialog, select a workflow model from the list.

   ![chlimage_1-31](assets/chlimage_1-138.png)

1. (Opcional) Especifique un título para el flujo de trabajo, que se puede utilizar para hacer referencia a la instancia de flujo de trabajo.
1. Haga clic en **[!UICONTROL Iniciar]** y, a continuación, en **[!UICONTROL Confirmar]** en el cuadro de diálogo. El flujo de trabajo se ejecuta en todos los recursos seleccionados.

## Aplicar un flujo de trabajo a varias carpetas {#applying-a-workflow-to-multiple-folders}

El procedimiento para aplicar un flujo de trabajo a varias carpetas es similar al procedimiento para aplicar un flujo de trabajo a varios recursos. Seleccione las carpetas de la [!DNL Assets] interfaz y realice los pasos 2 a 7 del procedimiento para [aplicar un flujo de trabajo a varios recursos](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets).

## Aplicación de un flujo de trabajo a una colección {#applying-a-workflow-to-a-collection}

Consulte [Aplicación de un flujo de trabajo a una colección](/help/assets/managing-collections-touch-ui.md#running-a-workflow-on-a-collection).

## inicio automático de un flujo de trabajo para procesar los recursos de forma condicional {#auto-execute-workflow-on-some-assets}

Los administradores pueden configurar el flujo de trabajo para ejecutar y procesar automáticamente recursos en función de condiciones predefinidas. La funcionalidad es útil para usuarios de la línea de negocios y especialistas en mercadotecnia, por ejemplo, para crear un flujo de trabajo personalizado en carpetas específicas. Supongamos que todos los activos de la sesión fotográfica de una agencia se pueden marcar con agua o que todos los recursos cargados por un operador independiente se pueden procesar para crear representaciones específicas.

Para un modelo de flujo de trabajo, los usuarios pueden crear un iniciador de flujo de trabajo que lo ejecute. Un iniciador de flujo de trabajo supervisa los cambios en el repositorio de contenido y ejecuta el flujo de trabajo cuando se cumplen las condiciones predefinidas. Los administradores pueden proporcionar acceso a los especialistas en marketing para crear flujos de trabajo y configurar el iniciador. Los usuarios pueden modificar el flujo de trabajo predeterminado de recursos [!UICONTROL de actualización de] DAM para agregar los pasos adicionales necesarios para procesar recursos específicos. El flujo de trabajo se ejecuta en todos los recursos cargados recientemente. Utilice uno de los siguientes métodos para limitar la ejecución de los pasos adicionales en recursos específicos:

* Realice una copia del flujo de trabajo de [!UICONTROL DAM Update Asset] y modifíquelo para que se ejecute en una jerarquía de carpetas específica. Este método resulta útil para algunas carpetas.
* Los pasos de procesamiento adicionales se pueden agregar mediante una división [](/help/sites-developing/workflows-step-ref.md#or-split) O, según se requiera, para tantas carpetas como se necesiten.

## Prácticas recomendadas y limitaciones {#best-practices-limitations-tips}

* Tenga en cuenta sus necesidades para todos los tipos de representaciones al diseñar flujos de trabajo. Si no prevé la necesidad de una representación en el futuro, elimine el paso de creación del flujo de trabajo. Las representaciones no se pueden eliminar de forma masiva posteriormente. Las representaciones no deseadas pueden ocupar mucho espacio en almacenamiento después de un uso prolongado de [!DNL Experience Manager]. Para recursos individuales, puede quitar las representaciones manualmente de la interfaz de usuario. En el caso de varios recursos, puede personalizar [!DNL Experience Manager] para eliminar representaciones específicas o eliminar los recursos y cargarlos de nuevo.
* De forma predeterminada, el flujo de trabajo de recursos [!UICONTROL de actualización de] DAM incluye algunos pasos para crear miniaturas y representaciones web. Si se eliminan del flujo de trabajo las representaciones predeterminadas, la interfaz de usuario de [!DNL Assets] no se procesa correctamente.

>[!MORELIKETHIS]
>
>* [Aplicar y participar en flujos de trabajo](/help/sites-authoring/workflows.md)
>* [Creación de modelos de flujo de trabajo y ampliación de la funcionalidad de flujo de trabajo](/help/sites-developing/workflows.md)
>* [Métodos para ejecutar flujos de trabajo](/help/sites-administering/workflows-starting.md)
>* [Prácticas recomendadas del flujo de trabajo](/help/sites-developing/workflows-best-practices.md)
>* [Artículo de comunidad sobre la modificación de recursos mediante flujo de trabajo](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)

