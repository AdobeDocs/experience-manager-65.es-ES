---
title: Etiquetas inteligentes mejoradas
description: Etiquetas inteligentes mejoradas
contentOwner: AG
translation-type: tm+mt
source-git-commit: 788a66d5732f0a120de6b80da69e9cf81f998667
workflow-type: tm+mt
source-wordcount: '1597'
ht-degree: 2%

---


# Comprender, aplicar y depurar etiquetas inteligentes {#enhanced-smart-tags}

Las organizaciones que se ocupan de los recursos digitales utilizan cada vez más el vocabulario controlado por taxonomía en los metadatos de los recursos. Básicamente, incluye una lista de palabras clave que los empleados, socios y clientes suelen utilizar para referirse a recursos digitales de una clase en particular y buscar dichos recursos. El etiquetado de activos con vocabulario controlado por taxonomía garantiza que los activos se identifiquen y recuperen fácilmente.

En comparación con los vocabularios de lenguaje natural, etiquetar recursos digitales en función de la taxonomía empresarial ayuda a alinearlos con el negocio de una empresa y garantiza que los activos más relevantes aparezcan en las búsquedas.

Por ejemplo, un fabricante de coches puede etiquetar imágenes de coches con nombres de modelos, de modo que solo aparecen imágenes relevantes cuando se buscan imágenes de varios modelos para diseñar una campaña de promoción.

Para que el servicio de contenido inteligente aplique las etiquetas correctas, entrénelo para que reconozca su taxonomía. Para formar el servicio, primero debe depurar un conjunto de recursos y etiquetas que describan mejor estos recursos. Para ayudar al aprendizaje del servicio, aplique estas etiquetas en los recursos y ejecute un flujo de trabajo de formación.

Una vez que una etiqueta está preparada y lista, el servicio ahora puede aplicar estas etiquetas en los recursos a través de un flujo de trabajo de etiquetado.

En segundo plano, el servicio de contenido inteligente utiliza el marco de IA de Adobe Sensei para entrenar su algoritmo de reconocimiento de imágenes en la estructura de etiquetas y la taxonomía empresarial. A continuación, esta inteligencia de contenido se utiliza para aplicar etiquetas relevantes en un conjunto diferente de recursos.

El servicio de contenido inteligente es un servicio en la nube alojado en [!DNL Adobe Developer Console]. Para utilizarlo en [!DNL Adobe Experience Manager], el administrador del sistema debe integrar su implementación [!DNL Experience Manager] con [!DNL Adobe Developer Console].

En resumen, estos son los pasos principales para utilizar el servicio de contenido inteligente:

* Incorporación
* Revisión de recursos y etiquetas (definición de taxonomía)
* Formación del servicio de contenido inteligente
* Etiquetado automático

![Diagrama de flujo](assets/flowchart.gif)

## Requisitos previos y formatos admitidos {#prerequisites}

Antes de utilizar el servicio de contenido inteligente, asegúrese de lo siguiente para crear una integración en [!DNL Adobe Developer Console]:

* Una cuenta de Adobe ID con privilegios de administrador para la organización.
* Habilite el servicio de Smart Content Service para su organización.
* Para agregar el paquete base de servicios de contenido inteligente a una implementación, licencia [!DNL Adobe Experience Manager Sites] Paquete base y [!DNL Assets] complemento.

El servicio aplica etiquetas inteligentes a los recursos de los siguientes tipos de MIME:

* image/jpeg
* image/tiff
* image/png
* image/bmp
* image/gif
* image/pjpeg
* image/x-portable-anymap
* image/x-portable-bitmap
* image/x-portable-graymap
* image/x-portable-pixmap
* image/x-rgb
* image/x-xbitmap
* image/x-xpixmap
* image/x-icon
* imagen/photoshop
* image/x-photoshop
* image/psd
* image/vnd.adobe.photoshop

El servicio aplica etiquetas inteligentes a las representaciones de recursos de los siguientes tipos MIME:

* image/jpeg
* image/pjpeg
* imagen/png

## Incorporación {#onboarding}

El servicio de contenido inteligente está disponible para su compra como complemento de [!DNL Experience Manager]. Después de realizar la compra, se envía un correo electrónico al administrador de la organización con un vínculo a [!DNL Adobe I/O].

El administrador puede seguir el enlace para integrar el servicio de contenido inteligente con [!DNL Experience Manager]. Para integrar el servicio con [!DNL Experience Manager Assets], consulte [Configuración de etiquetas inteligentes](config-smart-tagging.md).

El proceso de incorporación se completa cuando el administrador configura el servicio y agrega usuarios en [!DNL Experience Manager].

>[!NOTE]
>
>Si utiliza [!DNL Experience Manager] 6.3 o una versión anterior y necesita utilizar el servicio de etiquetado para sus recursos, consulte [Etiquetas inteligentes](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html). Las etiquetas inteligentes no utilizan las capacidades de IA más recientes y, por lo tanto, son menos precisas que el servicio de etiquetado inteligente mejorado.

## Revisar recursos y etiquetas {#reviewing-assets-and-tags}

Una vez que esté integrado, lo primero que desea hacer es identificar un conjunto de etiquetas que describan mejor estas imágenes en el contexto de su negocio.

A continuación, revise las imágenes para identificar un conjunto de imágenes que represente mejor su producto para un requisito comercial determinado. Asegúrese de que los recursos del conjunto depurado cumplen las [directrices de formación del servicio de contenido inteligente](/help/assets/config-smart-tagging.md#training-the-smart-content-service).

Agregue los recursos a una carpeta y aplique las etiquetas a cada recurso desde la página de propiedades. A continuación, ejecute el flujo de trabajo de formación en esta carpeta. El conjunto depurado de recursos permite que el servicio de contenido inteligente imparta formación a más recursos mediante las definiciones de taxonomía.

>[!NOTE]
>
>1. La formación es un proceso irrevocable. Adobe recomienda revisar las etiquetas del conjunto depurado de recursos antes de entrenar el servicio de contenido inteligente en las etiquetas.
>1. Antes de recibir formación para una etiqueta, consulte [Directrices de formación del servicio de contenido inteligente](/help/assets/config-smart-tagging.md#training-the-smart-content-service).
>1. Cuando imparte el servicio de contenido inteligente por primera vez, Adobe recomienda que lo imparta en al menos dos etiquetas diferentes.


## Comprender los [!DNL Experience Manager] resultados de búsqueda con etiquetas inteligentes {#understandsearch}

De forma predeterminada, la búsqueda [!DNL Experience Manager] combina los términos de búsqueda con una cláusula `AND`. El uso de etiquetas inteligentes no cambia este comportamiento predeterminado. El uso de etiquetas inteligentes agrega una cláusula `OR` adicional para encontrar cualquiera de los términos de búsqueda relacionados con las etiquetas inteligentes. Por ejemplo, considere la búsqueda de `woman running`. Los recursos con solo `woman` o con `running` palabra clave en los metadatos no aparecen en los resultados de búsqueda de forma predeterminada. Sin embargo, en una consulta de búsqueda de este tipo aparece un recurso etiquetado con `woman` o `running` etiquetas inteligentes. Así que los resultados de la búsqueda son una combinación de:

* Recursos con palabras clave `woman` y `running` en los metadatos.

* Recursos inteligentes etiquetados con cualquiera de las palabras clave.

Los resultados de búsqueda que coinciden con todos los términos de búsqueda en los campos de metadatos se muestran primero, seguidos de los resultados de búsqueda que coinciden con cualquiera de los términos de búsqueda en las etiquetas inteligentes. En el ejemplo anterior, el orden aproximado de visualización de los resultados de búsqueda es:

1. Coincide con `woman running` en los distintos campos de metadatos.
1. Coincide con `woman running` en las etiquetas inteligentes.
1. Coincide con `woman` o `running` en las etiquetas inteligentes.

>[!CAUTION]
>
>Si la indexación de Lucene se realiza a partir de [!DNL Adobe Experience Manager], la búsqueda basada en etiquetas inteligentes no funciona como se espera.

## Etiquetar recursos automáticamente {#tagging-assets-automatically}

Una vez que haya formado el servicio de contenido inteligente, puede activar el flujo de trabajo de etiquetado para aplicar automáticamente las etiquetas adecuadas en un conjunto diferente de recursos similares.

Puede ejecutar el flujo de trabajo de etiquetado periódicamente o siempre que sea necesario.

>[!NOTE]
>
>El flujo de trabajo de etiquetado se ejecuta tanto en los recursos como en las carpetas.

### Etiquetado periódico {#periodic-tagging}

Puede habilitar el servicio de contenido inteligente para que etiquete periódicamente los recursos de una carpeta. Abra la página de propiedades de la carpeta de recursos, seleccione **[!UICONTROL Habilitar etiquetas inteligentes]** en la pestaña **[!UICONTROL Detalles]** y guarde los cambios.

Una vez seleccionada esta opción para una carpeta, el servicio de contenido inteligente etiqueta automáticamente los recursos de la carpeta. De forma predeterminada, el flujo de trabajo de etiquetado se ejecuta todos los días a las 12:00.

### Etiquetado a petición {#on-demand-tagging}

Puede activar el flujo de trabajo de etiquetado desde la consola de flujo de trabajo o desde la cronología para etiquetar los recursos al instante.

>[!NOTE]
>
>Si ejecuta el flujo de trabajo de etiquetado desde la línea de tiempo, puede aplicar etiquetas en un máximo de 15 recursos a la vez.

#### Etiquetar recursos de la consola de flujo de trabajo {#tagging-assets-from-the-workflow-console}

1. En la interfaz [!DNL Experience Manager], vaya a **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. En la página **[!UICONTROL Modelos de flujo de trabajo]**, seleccione el flujo de trabajo **[!UICONTROL Recursos de etiquetas inteligentes DAM]** y haga clic en **[!UICONTROL Iniciar flujo de trabajo]** en la barra de herramientas.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. En el cuadro de diálogo **[!UICONTROL Ejecutar flujo de trabajo]**, vaya a la carpeta de carga útil que contiene los recursos en los que desea aplicar las etiquetas automáticamente.
1. Especifique un título para el flujo de trabajo y un comentario opcional. Haga clic en **[!UICONTROL Ejecutar]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Para comprobar si el servicio de contenido inteligente ha etiquetado los recursos correctamente, vaya a la carpeta de recursos y revise las etiquetas.

#### Etiquetar recursos de la cronología {#tagging-assets-from-the-timeline}

1. En la interfaz de usuario [!DNL Assets], seleccione la carpeta que contiene los recursos o recursos específicos a los que desea aplicar las etiquetas inteligentes.
1. En la esquina superior izquierda, abra la **[!UICONTROL Línea de tiempo]**.
1. Abra las acciones desde la parte inferior de la barra lateral izquierda y haga clic en **[!UICONTROL Iniciar flujo de trabajo]**.

   ![start_workflow](assets/start_workflow.png)

1. Seleccione el flujo de trabajo **[!UICONTROL DAM Smart Tag Assets]** y especifique un título para el flujo de trabajo.
1. Haga clic en **[!UICONTROL Start]**. El flujo de trabajo aplica etiquetas a los recursos. para comprobar si el servicio de contenido inteligente ha etiquetado los recursos correctamente, vaya a la carpeta de recursos y revise las etiquetas.

>[!NOTE]
>
>En los ciclos de etiquetado posteriores, solo los recursos modificados se etiquetan de nuevo con etiquetas recién formadas. Sin embargo, incluso los recursos sin modificar se etiquetan si el espacio entre los ciclos de etiquetado último y actual para el flujo de trabajo de etiquetado supera las 24 horas. Para los flujos de trabajo de etiquetado periódicos, los recursos sin modificar se etiquetan cuando el lapso de tiempo supera los seis meses.

## Depurar o moderar las etiquetas inteligentes aplicadas {#manage-smart-tags}

Puede depurar las etiquetas inteligentes para eliminar las etiquetas inexactas que se asignen a las imágenes de marca, de modo que solo se muestren las etiquetas más relevantes.

Moderar las etiquetas inteligentes también ayuda a refinar las búsquedas basadas en etiquetas de imágenes, ya que garantiza que la imagen aparezca en los resultados de búsqueda de las etiquetas más relevantes. Esencialmente, ayuda a eliminar las posibilidades de que las imágenes no relacionadas aparezcan en los resultados de búsqueda.

También puede asignar una clasificación superior a una etiqueta para aumentar su relevancia para una imagen. La promoción de una etiqueta para una imagen aumenta las posibilidades de que la imagen aparezca en los resultados de búsqueda cuando se busca la etiqueta en particular.

1. En el cuadro de búsqueda, busque recursos basados en una etiqueta como palabra clave.
1. Para identificar una imagen que no encuentra relevante para la búsqueda, revise los resultados de la búsqueda.
1. Seleccione la imagen y haga clic en **[!UICONTROL Administrar etiquetas]** en la barra de herramientas.
1. En la página **[!UICONTROL Administrar etiquetas]**, revise las etiquetas. Si no desea que se busque la imagen en función de una etiqueta específica, seleccione la etiqueta y, a continuación, haga clic en **[!UICONTROL Eliminar]** en la barra de herramientas. También puede hacer clic en el símbolo `x` que aparece junto a una etiqueta.
1. De forma opcional, para asignar una clasificación superior a una etiqueta, seleccione la etiqueta y haga clic en **[!UICONTROL Promocionar]** en la barra de herramientas. La etiqueta que promocione se moverá a la sección **[!UICONTROL Etiquetas]**.
1. Haga clic en **[!UICONTROL Guardar]** y, a continuación, haga clic en **[!UICONTROL Aceptar]**
1. Vaya a la página **[!UICONTROL Properties]** de la imagen. Observe que la etiqueta que promocionó tiene más relevancia y aparece antes en los resultados de búsqueda.

## Sugerencias y limitaciones {#tips-best-practices-limitations}

* El uso de Smart Content Services está limitado a hasta 2 millones de imágenes etiquetadas al año. Las imágenes duplicadas que se procesan y etiquetan se cuentan como imágenes etiquetadas.
* Si ejecuta el flujo de trabajo de etiquetado desde la línea de tiempo, puede aplicar etiquetas en un máximo de 15 recursos a la vez.
* Las etiquetas inteligentes solo funcionan para los formatos de imagen PNG y JPG. Por lo tanto, los recursos admitidos que tienen representaciones creadas en estos dos formatos se etiquetan con etiquetas inteligentes.
