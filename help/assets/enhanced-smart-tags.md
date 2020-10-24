---
title: Etiquetas inteligentes mejoradas
description: Etiquetas inteligentes mejoradas
contentOwner: AG
translation-type: tm+mt
source-git-commit: e124025295f29d6f3999dc52467301d48bceee75
workflow-type: tm+mt
source-wordcount: '1525'
ht-degree: 1%

---


# Comprender, aplicar y conservar etiquetas inteligentes {#enhanced-smart-tags}

Las organizaciones que se ocupan de los activos digitales utilizan cada vez más el vocabulario controlado por taxonomía en los metadatos de los recursos. Básicamente, incluye una lista de palabras clave que los empleados, socios y clientes utilizan comúnmente para referirse a los recursos digitales de una clase en particular y buscarlos. Etiquetar recursos con vocabulario controlado por taxonomía garantiza que se puedan identificar y recuperar fácilmente mediante búsquedas basadas en etiquetas.

En comparación con los vocabularios del lenguaje natural, etiquetar los activos digitales en función de la taxonomía empresarial ayuda a alinearlos con el negocio de una compañía y garantiza que los activos más relevantes aparezcan en las búsquedas.

Por ejemplo, un fabricante de automóviles puede etiquetar imágenes de automóviles con nombres de modelos para que solo aparezcan imágenes relevantes cuando se buscan imágenes de varios modelos para diseñar una campaña de promoción.

Para que el servicio de contenido inteligente aplique las etiquetas correctas, debe formarlo para que reconozca su taxonomía. Para entrenar el servicio, seleccione primero un conjunto de recursos y etiquetas que describan mejor estos recursos. Aplique estas etiquetas a los recursos y ejecute un flujo de trabajo de formación para ayudar al servicio a aprender.

Una vez preparada y preparada la etiqueta, el servicio ahora puede aplicarla a los recursos mediante un flujo de trabajo de etiquetado.

En segundo plano, Smart Content Service utiliza el marco de trabajo de Adobe Sensei AI para entrenar su algoritmo de reconocimiento de imágenes en la estructura de etiquetas y la taxonomía empresarial. Esta inteligencia de contenido se utiliza para aplicar etiquetas relevantes a un conjunto diferente de recursos.

Smart Content Service es un servicio en la nube alojado en E/S de Adobe. Para utilizarlo en [!DNL Adobe Experience Manager], el administrador del sistema debe integrar su [!DNL Experience Manager] implementación con E/S de Adobe.

En resumen, estos son los pasos principales para utilizar el servicio de contenido inteligente:

* Incorporación
* Revisión de recursos y etiquetas (definición de taxonomía)
* Formación del servicio de contenido inteligente
* Etiquetado automático

![diagrama de flujo](assets/flowchart.gif)

## Requisitos previos {#prerequisites}

Antes de utilizar el servicio de contenido inteligente, asegúrese de lo siguiente para crear una integración en E/S de Adobe:

* Cuenta de Adobe ID que tiene privilegios de administrador para la organización.
* El servicio de Smart Content Service está habilitado para su organización.
* El paquete base de servicios de contenido inteligente solo se puede agregar a una implementación en la que se haya otorgado licencia a un paquete [!DNL Sites] base y a un complemento [!DNL Assets] .

## Incorporación {#onboarding}

The Smart Content Service is available for purchase as an add-on to [!DNL Experience Manager]. Después de realizar la compra, se envía un correo electrónico al administrador de la organización con un vínculo a E/S de Adobe.

El administrador puede seguir el vínculo para integrar el servicio de contenido inteligente con [!DNL Experience Manager]. Para integrar el servicio con [!DNL Experience Manager Assets], consulte [Configuración de etiquetas](config-smart-tagging.md)inteligentes.

El proceso de integración se completa cuando el administrador configura el servicio y agrega usuarios en [!DNL Experience Manager].

>[!NOTE]
>
>Si utiliza [!DNL Experience Manager] 6.3 o una versión anterior y necesita un servicio de etiquetado para sus recursos, consulte Etiquetas [inteligentes](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html). Las etiquetas inteligentes no utilizan las últimas funciones de AI y, por tanto, son menos precisas que el servicio de etiquetado inteligente mejorado.

## Revisar recursos y etiquetas {#reviewing-assets-and-tags}

Una vez que esté a bordo, lo primero que desea hacer es identificar un conjunto de etiquetas que describan mejor estas imágenes en el contexto de su negocio.

A continuación, revise las imágenes para identificar un conjunto de imágenes que mejor representen el producto para un requerimiento comercial determinado. Asegúrese de que los recursos del conjunto depurado cumplen las directrices [de formación del servicio de contenido](/help/assets/config-smart-tagging.md#training-the-smart-content-service)inteligente.

Añada los recursos a una carpeta y aplique las etiquetas a cada recurso desde la página de propiedades. A continuación, ejecute el flujo de trabajo de formación en esta carpeta. El conjunto depurado de recursos permite que el servicio de contenido inteligente imparta formación eficaz a más recursos mediante las definiciones de taxonomía.

>[!NOTE]
>
>1. La formación es un proceso irrevocable. Adobe recomienda revisar las etiquetas del conjunto depurado de recursos antes de formarlo con las etiquetas.
>1. Antes de la formación para una etiqueta, consulte las directrices [de formación del servicio de contenido](/help/assets/config-smart-tagging.md#training-the-smart-content-service)inteligente.
>1. Cuando entrena el servicio de contenido inteligente por primera vez, Adobe recomienda que lo imparta en al menos dos etiquetas diferentes.


## Comprender los resultados [!DNL Experience Manager] de búsqueda con etiquetas inteligentes {#understandsearch}

De forma predeterminada, [!DNL Experience Manager] la búsqueda combina los términos de búsqueda con una `AND` cláusula. El uso de etiquetas inteligentes no cambia este comportamiento predeterminado. El uso de etiquetas inteligentes agrega una `OR` cláusula adicional para encontrar cualquiera de los términos de búsqueda en las etiquetas inteligentes de aplicación. For example, consider searching for `woman running`. Los recursos con solo `woman` o solamente `running` palabra clave en los metadatos no aparecen en los resultados de búsqueda de forma predeterminada. Sin embargo, en una consulta de búsqueda de este tipo aparece un recurso etiquetado con etiquetas inteligentes `woman` o con `running` etiquetas inteligentes. Los resultados de la búsqueda son una combinación de:

* recursos con `woman` y `running` palabras clave en los metadatos.

* los recursos se etiquetaron de forma inteligente con cualquiera de las palabras clave.

Los resultados de búsqueda que coinciden con todos los términos de búsqueda en los campos de metadatos se muestran primero, seguidos de los resultados de búsqueda que coinciden con cualquiera de los términos de búsqueda en las etiquetas inteligentes. En el ejemplo anterior, el orden aproximado de visualización de los resultados de búsqueda es:

1. coincidencias de en `woman running` los distintos campos de metadatos.
1. coincidencias de `woman running` en etiquetas inteligentes.
1. coincidencias de `woman` o de `running` en etiquetas inteligentes.

>[!CAUTION]
>
>Si la indexación de Lucene se realiza fuera de [!DNL Adobe Experience Manager] este parámetro, la búsqueda basada en etiquetas inteligentes no funciona de la forma esperada.

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

Puede activar el flujo de trabajo de etiquetado desde la consola de flujo de trabajo o desde la línea de tiempo para etiquetar los recursos al instante.

>[!NOTE]
>
>Si ejecuta el flujo de trabajo de etiquetado desde la línea de tiempo, puede aplicar etiquetas a un máximo de 15 recursos a la vez.

#### Etiquetado de recursos desde la consola de flujo de trabajo {#tagging-assets-from-the-workflow-console}

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. En el cuadro de diálogo **[!UICONTROL Ejecutar flujo de trabajo]** , vaya a la carpeta de carga útil que contiene los recursos en los que desea aplicar las etiquetas automáticamente.
1. Especifique un título para el flujo de trabajo y un comentario opcional. Haga clic en **[!UICONTROL Ejecutar]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Vaya a la carpeta de recursos y revise las etiquetas para comprobar si el servicio de contenido inteligente ha etiquetado los recursos correctamente.

#### Etiquetar recursos de la línea de tiempo {#tagging-assets-from-the-timeline}

1. En la interfaz de usuario, seleccione la carpeta que contenga recursos o recursos específicos a los que desee aplicar etiquetas inteligentes. [!DNL Assets]
1. En la esquina superior izquierda, abra la **[!UICONTROL línea de tiempo]**.
1. Abra acciones desde la parte inferior de la barra lateral izquierda y haga clic en Flujo de trabajo **[!UICONTROL de Inicio]**.

   ![inicio_workflow](assets/start_workflow.png)

1. Seleccione el flujo de trabajo Recursos **[!UICONTROL de etiquetas inteligentes]** DAM y especifique un título para el flujo de trabajo.
1. Haga clic en **[!UICONTROL Inicio]**. El flujo de trabajo aplica las etiquetas a los recursos. Vaya a la carpeta de recursos y revise las etiquetas para comprobar si el servicio de contenido inteligente ha etiquetado los recursos correctamente.

>[!NOTE]
>
>En los ciclos de etiquetado posteriores, solo los recursos modificados se etiquetan de nuevo con etiquetas recién formadas.Sin embargo, incluso los recursos sin modificar se etiquetan si el espacio entre los últimos y los actuales ciclos de etiquetado del flujo de trabajo de etiquetado supera las 24 horas. Para los flujos de trabajo de etiquetado periódicos, los recursos sin modificar se etiquetan cuando el lapso de tiempo supera los 6 meses.

## Depurar o moderar las etiquetas inteligentes aplicadas {#manage-smart-tags}

Puede depurar las etiquetas inteligentes para eliminar cualquier etiqueta incorrecta que se haya asignado a las imágenes de su marca, de modo que solo se muestren las etiquetas más relevantes.

La moderación de las etiquetas inteligentes también ayuda a restringir las búsquedas de imágenes basadas en etiquetas, ya que garantiza que la imagen aparezca en los resultados de búsqueda de las etiquetas más relevantes. Básicamente, ayuda a eliminar las posibilidades de que las imágenes no relacionadas aparezcan en los resultados de búsqueda.

También puede asignar una clasificación superior a una etiqueta para aumentar su relevancia con respecto a una imagen. La promoción de una etiqueta para una imagen aumenta las posibilidades de que la imagen aparezca en los resultados de búsqueda cuando se realiza una búsqueda en función de la etiqueta en particular.

1. En el cuadro Omniture, busque recursos basados en una etiqueta.
1. Inspect muestra los resultados de la búsqueda para identificar una imagen que no le parece relevante para la búsqueda.
1. Seleccione la imagen y haga clic en **[!UICONTROL Administrar etiquetas]** en la barra de herramientas.
1. En la página **[!UICONTROL Administrar etiquetas]** , inspeccione las etiquetas. Si no desea que la imagen se busque en función de una etiqueta específica, seleccione la etiqueta y haga clic en **[!UICONTROL Eliminar]** en la barra de herramientas. También puede hacer clic en `x` símbolo que aparece junto a una etiqueta.
1. De forma opcional, para asignar una clasificación superior a una etiqueta, seleccione la etiqueta y haga clic en **[!UICONTROL Promocionar]** en la barra de herramientas. La etiqueta promocionada se mueve a la sección **[!UICONTROL Etiquetas]** .
1. Click **[!UICONTROL Save]** and then click **[!UICONTROL OK]**
1. Vaya a la página **[!UICONTROL Propiedades]** de la imagen. Observe que la etiqueta que promocionó tiene más relevancia y aparece antes en los resultados de búsqueda.

## Sugerencias y limitaciones {#tips-best-practices-limitations}

* El uso de Smart Content Services está limitado a hasta 2 millones de imágenes etiquetadas por año. Todas las imágenes de duplicado procesadas y etiquetadas se cuentan como imágenes etiquetadas.
* Si ejecuta el flujo de trabajo de etiquetado desde la línea de tiempo, puede aplicar etiquetas a un máximo de 15 recursos a la vez.
