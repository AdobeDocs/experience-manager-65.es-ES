---
title: Etiquetas inteligentes mejoradas
description: Etiquetas inteligentes mejoradas
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Etiquetas inteligentes mejoradas {#enhanced-smart-tags}

## Información general sobre las etiquetas inteligentes mejoradas {#overview-of-enhanced-smart-tags}

Las organizaciones que se ocupan de los activos digitales utilizan cada vez más el vocabulario controlado por taxonomía en los metadatos de los recursos. Básicamente, incluye una lista de palabras clave que los empleados, socios y clientes utilizan comúnmente para referirse a los recursos digitales de una clase en particular y buscarlos. Etiquetar recursos con vocabulario controlado por taxonomía garantiza que se puedan identificar y recuperar fácilmente mediante búsquedas basadas en etiquetas.

En comparación con los vocabularios del lenguaje natural, etiquetar los activos digitales en función de la taxonomía empresarial ayuda a alinearlos con el negocio de una empresa y garantiza que los activos más relevantes aparezcan en las búsquedas.

Por ejemplo, un fabricante de automóviles puede etiquetar imágenes de autos con nombres de modelo para que solo aparezcan imágenes relevantes cuando se buscan imágenes de varios modelos para diseñar una campaña de promoción.

Para que el servicio de contenido inteligente aplique las etiquetas correctas, debe formarlo para que reconozca su taxonomía. Para entrenar el servicio, seleccione primero un conjunto de recursos y etiquetas que describan mejor estos recursos. Aplique estas etiquetas a los recursos y ejecute un flujo de trabajo de formación para ayudar al servicio a aprender.

Una vez preparada y preparada la etiqueta, el servicio ahora puede aplicarla a los recursos mediante un flujo de trabajo de etiquetado.

En segundo plano, el servicio de contenido inteligente utiliza el marco de IA de Adobe Sensei para formar su algoritmo de reconocimiento de imágenes en la estructura de etiquetas y la taxonomía empresarial. Esta inteligencia de contenido se utiliza para aplicar etiquetas relevantes a un conjunto diferente de recursos.

Smart Content Service es un servicio en la nube alojado en Adobe I/O. Para utilizarlo en Adobe Experience Manager (AEM), el administrador del sistema debe integrar su instancia de AEM con la E/S de Adobe.

En resumen, estos son los pasos principales para utilizar el servicio de contenido inteligente:

* Incorporación
* Revisión de recursos y etiquetas (definición de taxonomía)
* Formación del servicio de contenido inteligente
* Etiquetado automático

![diagrama de flujo](assets/flowchart.gif)

## Requisitos previos {#prerequisites}

Antes de utilizar el servicio de contenido inteligente, asegúrese de lo siguiente para crear una integración en Adobe I/O:

* Una cuenta de Adobe ID que tiene privilegios de administrador para la organización.
* El servicio de Smart Content Service está habilitado para su organización.

## Incorporación {#onboarding}

El servicio de contenido inteligente está disponible para su compra como complemento de AEM. Después de realizar la compra, se envía un correo electrónico al administrador de la organización con un vínculo a la E/S de Adobe.

El administrador puede seguir el vínculo para integrar el servicio de contenido inteligente con AEM. Para integrar el servicio con Recursos AEM, consulte [Configuración de etiquetas](config-smart-tagging.md)inteligentes.

El proceso de integración se completa cuando el administrador configura el servicio y agrega usuarios en AEM.

>[!NOTE]
>
>Si utiliza AEM 6.3 o una versión anterior y necesita un servicio de etiquetado para sus recursos, consulte Etiquetas [inteligentes](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html). Las etiquetas inteligentes no utilizan las últimas funciones de AI y, por tanto, son menos precisas que el servicio de etiquetado inteligente mejorado.

## Revisar recursos y etiquetas {#reviewing-assets-and-tags}

Una vez que esté integrado, lo primero que desea hacer es identificar un conjunto de etiquetas que describan mejor estas imágenes en el contexto de su negocio.

A continuación, revise las imágenes para identificar un conjunto de imágenes que mejor representen el producto para un requerimiento comercial determinado. Asegúrese de que los recursos del conjunto depurado cumplen las directrices [de formación del servicio de contenido](smart-tags-training-guidelines.md)inteligente.

Agregue los recursos a una carpeta y aplique las etiquetas a cada recurso desde la página de propiedades. A continuación, ejecute el flujo de trabajo de formación en esta carpeta. El conjunto depurado de recursos permite que el servicio de contenido inteligente imparta formación eficaz a más recursos mediante las definiciones de taxonomía.

>[!NOTE]
>
>1. La formación es un proceso irrevocable. Adobe recomienda revisar las etiquetas del conjunto depurado de recursos antes de formarlo con las etiquetas.
>1. Lea las directrices [de formación del servicio de contenido](smart-tags-training-guidelines.md) inteligente antes de iniciar la formación para cualquier etiqueta.
>1. Cuando entrena el servicio de contenido inteligente por primera vez, Adobe recomienda que lo imparta en al menos dos etiquetas diferentes.


## Formación del servicio de contenido inteligente {#training-the-smart-content-service}

Para que Smart Content Service reconozca su taxonomía empresarial, ejecútela en un conjunto de recursos que ya incluyen etiquetas que son relevantes para su negocio. Después de la formación, el servicio puede aplicar la misma taxonomía a un conjunto de activos similar.

Puede entrenar el servicio varias veces para mejorar su capacidad de aplicar etiquetas relevantes. Después de cada ciclo de formación, ejecute un flujo de trabajo de etiquetado y compruebe si los recursos están etiquetados correctamente.

Puede capacitar al servicio de contenido inteligente de forma periódica o según sus necesidades.

>[!NOTE]
>
>El flujo de trabajo de formación solo se ejecuta en carpetas.

### Formación periódica {#periodic-training}

Puede habilitar el servicio de contenido inteligente para que imparta formación periódica sobre los recursos y las etiquetas asociadas dentro de una carpeta. Abra la página de propiedades de la carpeta de recursos, seleccione **[!UICONTROL Activar etiquetas]** inteligentes en la ficha **[!UICONTROL Detalles]** y guarde los cambios.

![enable_smart_tags](assets/enable_smart_tags.png)

Una vez seleccionada esta opción para una carpeta, AEM ejecuta un flujo de trabajo de formación automáticamente para formar el servicio de contenido inteligente en los recursos de la carpeta y sus etiquetas. De forma predeterminada, el flujo de trabajo de formación se ejecuta semanalmente los sábados a las 12:30.

### Capacitación a pedido {#on-demand-training}

Puede entrenar el servicio de contenido inteligente siempre que sea necesario desde la consola Flujo de trabajo.

1. Toque o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Herramientas > Flujo de trabajo > Modelos]**.
1. En la página Modelos **[!UICONTROL de]** flujo de trabajo, seleccione el flujo de trabajo de formación **[!UICONTROL de etiquetas]** inteligentes y, a continuación, toque o haga clic en **[!UICONTROL Iniciar flujo de trabajo]** en la barra de herramientas.
1. En el cuadro de diálogo **[!UICONTROL Ejecutar flujo de trabajo]** , vaya a la carpeta de carga útil que incluye los recursos etiquetados para la formación del servicio.
1. Especifique un título para el flujo de trabajo y un comentario. A continuación, toque o haga clic en **[!UICONTROL Ejecutar]**. Los recursos y las etiquetas se envían para formación.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>Una vez que los recursos de una carpeta se procesan para formación, solo los recursos modificados se procesan en los ciclos de formación posteriores.

### Ver informes de capacitación {#viewing-training-reports}

Para comprobar si el servicio de contenido inteligente ha recibido formación sobre sus etiquetas en el conjunto de recursos de formación, consulte el informe de flujo de trabajo de formación desde la consola Informes.

1. Toque o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Herramientas > Recursos > Informes]**.
1. En la página Informes **[!UICONTROL de]** recursos, toque o haga clic en **[!UICONTROL Crear]**.
1. Seleccione el informe Formación **[!UICONTROL sobre etiquetas]** inteligentes y, a continuación, toque o haga clic en **[!UICONTROL Siguiente]** en la barra de herramientas.
1. Especifique un título y una descripción para el informe. En **[!UICONTROL Programar informe]**, deje seleccionada la opción **[!UICONTROL Ahora]** . Si desea programar el informe para más adelante, seleccione **[!UICONTROL Más adelante]** y especifique una fecha y una hora. A continuación, toque o haga clic en **[!UICONTROL Crear]** desde la barra de herramientas.
1. En la página Informes **[!UICONTROL de]** recursos, seleccione el informe que ha generado. Para ver el informe, toque **[!UICONTROL Ver]** en la barra de herramientas.
1. Revise los detalles del informe.

   El informe muestra el estado de la formación de las etiquetas que ha entrenado. El color verde de la columna Estado **[!UICONTROL de]** formación indica que el servicio de contenido inteligente ha recibido formación para la etiqueta. El color amarillo indica que el servicio no está completamente entrenado para una etiqueta en particular. En este caso, agregue más imágenes con la etiqueta en concreto y ejecute el flujo de trabajo de formación para que el servicio se imparta completamente en la etiqueta .

   Si no ve las etiquetas en este informe, vuelva a ejecutar el flujo de trabajo de formación para estas etiquetas.

1. Para descargar el informe, selecciónelo en la lista y toque **[!UICONTROL Descargar]** en la barra de herramientas. El informe se descarga como archivo de Excel.

## Etiquetado automático de recursos {#tagging-assets-automatically}

Una vez que haya formado el servicio de contenido inteligente, puede activar el flujo de trabajo de etiquetado para aplicar automáticamente las etiquetas adecuadas a un conjunto diferente de recursos similares.

Puede ejecutar el flujo de trabajo de etiquetado de forma periódica o siempre que sea necesario.

>[!NOTE]
>
>El flujo de trabajo de etiquetado se ejecuta tanto en los recursos como en las carpetas.

### Etiquetado periódico {#periodic-tagging}

Puede activar el servicio de contenido inteligente para etiquetar recursos periódicamente dentro de una carpeta. Abra la página de propiedades de la carpeta de recursos, seleccione **[!UICONTROL Activar etiquetas]** inteligentes en la ficha **[!UICONTROL Detalles]** y guarde los cambios.

Una vez seleccionada esta opción para una carpeta, el servicio de contenido inteligente etiqueta automáticamente los recursos de la carpeta. De forma predeterminada, el flujo de trabajo de etiquetado se ejecuta todos los días a las 12:00 AM.

### Etiquetado a petición {#on-demand-tagging}

Puede activar el flujo de trabajo de etiquetado desde lo siguiente para etiquetar los recursos al instante:

* Consola de flujo de trabajo
* Escala de tiempo

>[!NOTE]
>
>Si ejecuta el flujo de trabajo de etiquetado desde la línea de tiempo, puede aplicar etiquetas a un máximo de 15 recursos a la vez.

#### Etiquetado de recursos desde la consola de flujo de trabajo {#tagging-assets-from-the-workflow-console}

1. Toque o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Herramientas > Flujo de trabajo > Modelos]**.
1. En la página Modelos **[!UICONTROL de]** flujo de trabajo, seleccione el flujo de trabajo Recursos **[!UICONTROL de etiquetas inteligentes]** DAM y, a continuación, toque o haga clic en **[!UICONTROL Iniciar flujo de trabajo]** en la barra de herramientas.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. En el cuadro de diálogo **[!UICONTROL Ejecutar flujo de trabajo]** , vaya a la carpeta de carga útil que contiene los recursos en los que desea aplicar las etiquetas automáticamente.
1. Especifique un título para el flujo de trabajo y un comentario opcional. A continuación, toque o haga clic en **[!UICONTROL Ejecutar]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Vaya a la carpeta de recursos y revise las etiquetas para comprobar si el servicio de contenido inteligente ha etiquetado los recursos correctamente. Para obtener más información, consulte [Administración de etiquetas](managing-smart-tags.md)inteligentes.

#### Etiquetar recursos de la línea de tiempo {#tagging-assets-from-the-timeline}

1. En la interfaz de usuario de Recursos, seleccione la carpeta que contenga recursos o recursos específicos a los que desee aplicar etiquetas inteligentes.
1. Toque el logotipo de Experience Manager y abra la línea de tiempo.
1. Puntee en la flecha de la parte inferior y, a continuación, toque o haga clic en **[!UICONTROL Iniciar flujo de trabajo]**.

   ![start_workflow](assets/start_workflow.png)

1. Seleccione el flujo de trabajo Recursos **[!UICONTROL de etiquetas inteligentes]** DAM y especifique un título para el flujo de trabajo.
1. Toque o haga clic en **[!UICONTROL Iniciar]**. El flujo de trabajo aplica las etiquetas a los recursos. Vaya a la carpeta de recursos y revise las etiquetas para comprobar si el servicio de contenido inteligente ha etiquetado los recursos correctamente. Para obtener más información, consulte [Administración de etiquetas](managing-smart-tags.md)inteligentes.

>[!NOTE]
>
>En los ciclos de etiquetado posteriores, solo los recursos modificados se etiquetan de nuevo con etiquetas recién formadas.
>
>Sin embargo, incluso los recursos sin modificar se etiquetan si el espacio entre los ciclos de etiquetado más recientes y más recientes para el flujo de trabajo de etiquetado supera las 24 horas.
>
>Para los flujos de trabajo de etiquetado periódico, los recursos sin modificar se etiquetan cuando el lapso supera los 6 meses.
