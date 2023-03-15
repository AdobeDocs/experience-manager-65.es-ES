---
title: Etiquetas inteligentes mejoradas
description: Etiquetas inteligentes mejoradas
contentOwner: AG
feature: Smart Tags, Search
role: User
exl-id: 5eff4a0f-30b1-4753-ad0b-002656eed972
source-git-commit: dd1e08bee03a6c7b07b32b0fb929d02dad467744
workflow-type: tm+mt
source-wordcount: '1579'
ht-degree: 2%

---

# Explicación, aplicación y depuración de las etiquetas inteligentes {#enhanced-smart-tags}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/smart-tags.html?lang=en) |
| AEM 6.5 | Este artículo |
| AEM 6.4 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/enhanced-smart-tags.html?lang=en) |

Las organizaciones que trabajan con recursos digitales utilizan cada vez más vocabulario controlado por taxonomía en los metadatos de recursos. Básicamente, incluye una lista de palabras clave que los empleados, socios y clientes suelen utilizar para referirse a recursos digitales de una clase determinada y buscarlos. El etiquetado de recursos con vocabulario controlado por taxonomía garantiza que los recursos se identifiquen y recuperen fácilmente.

En comparación con los vocabularios de lenguajes naturales, el etiquetado de recursos digitales basado en la taxonomía empresarial ayuda a alinearlos con el negocio de una empresa y garantiza que los recursos más relevantes aparezcan en las búsquedas.

Por ejemplo, un fabricante de automóviles puede etiquetar imágenes de automóviles con nombres de modelos para que solo aparezcan imágenes relevantes cuando se busquen imágenes de varios modelos para diseñar una campaña de promoción.

Para que el servicio de contenido inteligente aplique las etiquetas correctas, entréguelo para que reconozca su taxonomía. Para entrenar el servicio, primero depure un conjunto de recursos y etiquetas que describan mejor estos recursos. Para ayudar al servicio a aprender, aplique estas etiquetas en los recursos y ejecute un flujo de trabajo de formación.

Una vez que una etiqueta está preparada y lista, el servicio ahora puede aplicar estas etiquetas a los recursos a través de un flujo de trabajo de etiquetado.

En segundo plano, el servicio de contenido inteligente utiliza el marco de trabajo de Adobe Sensei AI para entrenar su algoritmo de reconocimiento de imágenes en la estructura de etiquetas y la taxonomía empresarial. A continuación, esta inteligencia de contenido se utiliza para aplicar las etiquetas relevantes a un conjunto diferente de recursos.

Smart Content Service es un servicio en la nube alojado en [!DNL Adobe Developer Console]. Para usarlo en [!DNL Adobe Experience Manager], el administrador del sistema debe integrar su [!DNL Experience Manager] implementación con [!DNL Adobe Developer Console].

En resumen, estos son los pasos principales para utilizar el servicio de contenido inteligente:

* Incorporación
* Revisión de recursos y etiquetas (definición de taxonomía)
* Formación del servicio de contenido inteligente
* Etiquetado automático

![Diagrama de flujo](assets/flowchart.gif)

## Requisitos previos y formatos admitidos {#prerequisites}

Antes de utilizar el servicio de contenido inteligente, asegúrese de lo siguiente para crear una integración en [!DNL Adobe Developer Console]:

* Una cuenta de Adobe ID con privilegios de administrador para la organización.
* Habilite el servicio de contenido inteligente para su organización.
* Para agregar el paquete base de Smart Content Services a una implementación, otorgue una licencia a [!DNL Adobe Experience Manager Sites] Paquete base y [!DNL Assets] complemento de.

El servicio aplica etiquetas inteligentes a los recursos de los siguientes tipos MIME:

* `image/jpeg`
* `image/tiff`
* `image/png`
* `image/bmp`
* `image/gif`
* `image/pjpeg`
* `image/x-portable-anymap`
* `image/x-portable-bitmap`
* `image/x-portable-graymap`
* `image/x-portable-pixmap`
* `image/x-rgb`
* `image/x-xbitmap`
* `image/x-xpixmap`
* `image/x-icon`
* `image/photoshop`
* `image/x-photoshop`
* `image/psd`
* `image/vnd.adobe.photoshop`

El servicio aplica etiquetas inteligentes a las representaciones de recursos de los siguientes tipos MIME:

* `image/jpeg`
* `image/pjpeg`
* `image/png`

## Incorporación {#onboarding}

El servicio de contenido inteligente está disponible para su compra como complemento de [!DNL Experience Manager]. Después de realizar la compra, se envía un correo electrónico al administrador de la organización con un vínculo a [!DNL Adobe I/O].

El administrador puede seguir el vínculo para integrar el servicio de contenido inteligente con [!DNL Experience Manager]. Para integrar el servicio con [!DNL Experience Manager Assets], consulte [Configuración de etiquetas inteligentes](config-smart-tagging.md).

El proceso de incorporación se completa cuando el administrador configura el servicio y añade usuarios en [!DNL Experience Manager].

## Revisión de recursos y etiquetas {#reviewing-assets-and-tags}

Una vez que se haya incorporado, lo primero que debe hacer es identificar un conjunto de etiquetas que describa mejor estas imágenes en el contexto de su negocio.

A continuación, revise las imágenes para identificar el conjunto de imágenes que mejor represente el producto para un requisito empresarial determinado. Asegúrese de que los recursos del conjunto depurado se ajustan a [Directrices de formación de Smart Content Service](/help/assets/config-smart-tagging.md#training-the-smart-content-service).

Agregue los recursos a una carpeta y aplique las etiquetas a cada recurso desde la página de propiedades. A continuación, ejecute el flujo de trabajo de formación en esta carpeta. El conjunto depurado de recursos permite al servicio de contenido inteligente formar de forma eficaz más recursos mediante las definiciones de taxonomía.

>[!NOTE]
>
>1. La formación es un proceso irrevocable. El Adobe recomienda revisar las etiquetas del conjunto depurado de recursos mucho antes de entrenar al servicio de contenido inteligente en las etiquetas.
>1. Antes de aprender a utilizar una etiqueta, consulte [Directrices de formación de Smart Content Service](/help/assets/config-smart-tagging.md#training-the-smart-content-service).
>1. Cuando entrena el servicio de contenido inteligente por primera vez, Adobe recomienda que lo imparta en al menos dos etiquetas distintas.


## Comprender [!DNL Experience Manager] resultados de búsqueda con etiquetas inteligentes {#understandsearch}

De forma predeterminada, [!DNL Experience Manager] la búsqueda combina los términos de búsqueda con una `AND` Cláusula. El uso de etiquetas inteligentes no cambia este comportamiento predeterminado. El uso de etiquetas inteligentes añade un `OR` para buscar cualquiera de los términos de búsqueda relacionados con las etiquetas inteligentes. Por ejemplo, considere la posibilidad de buscar `woman running`. Recursos con solo `woman` o simplemente `running` palabra clave en los metadatos no aparecen en los resultados de búsqueda de forma predeterminada. Sin embargo, un recurso etiquetado con `woman` o `running` el uso de etiquetas inteligentes aparece en una consulta de búsqueda de este tipo. Por lo tanto, los resultados de búsqueda son una combinación de:

* Recursos con `woman` y `running` palabras clave en los metadatos.

* Recursos etiquetados de forma inteligente con cualquiera de las palabras clave.

Los resultados de búsqueda que coinciden con todos los términos de búsqueda en los campos de metadatos se muestran primero, seguidos de los resultados de búsqueda que coinciden con cualquiera de los términos de búsqueda en las etiquetas inteligentes. En el ejemplo anterior, el orden aproximado de visualización de los resultados de búsqueda es:

1. Coincidencias de `woman running` en los distintos campos de metadatos.
1. Coincidencias de `woman running` en etiquetas inteligentes.
1. Coincidencias de `woman` o de `running` en etiquetas inteligentes.

>[!CAUTION]
>
>Si la indexación de Lucene se realiza fuera de [!DNL Adobe Experience Manager], la búsqueda basada en etiquetas inteligentes no funciona como se espera.

## Etiquetar recursos automáticamente {#tagging-assets-automatically}

Después de haber formado el servicio de contenido inteligente, puede almacenar en déclencheur el flujo de trabajo de etiquetado para aplicar automáticamente las etiquetas adecuadas a un conjunto diferente de recursos similares.

Puede ejecutar el flujo de trabajo de etiquetado periódicamente o siempre que sea necesario.

>[!NOTE]
>
>El flujo de trabajo de etiquetado se ejecuta tanto en recursos como en carpetas.

### Etiquetado periódico {#periodic-tagging}

Puede habilitar el Servicio de contenido inteligente para que etiquete periódicamente recursos de una carpeta. Abra la página de propiedades de la carpeta de recursos y seleccione **[!UICONTROL Habilitar etiquetas inteligentes]** en el **[!UICONTROL Detalles]** y guarde los cambios.

Una vez seleccionada esta opción para una carpeta, el servicio de contenido inteligente etiqueta automáticamente los recursos de la carpeta. De forma predeterminada, el flujo de trabajo de etiquetado se ejecuta todos los días a las 12:00 a.m.

### Etiquetado bajo demanda {#on-demand-tagging}

Puede almacenar en déclencheur el flujo de trabajo de etiquetado desde la consola de flujo de trabajo o desde la cronología para etiquetar instantáneamente los recursos.

>[!NOTE]
>
>Si ejecuta el flujo de trabajo de etiquetado desde la cronología, puede aplicar etiquetas en un máximo de 15 recursos a la vez.

#### Etiquetado de recursos desde la consola de flujo de trabajo {#tagging-assets-from-the-workflow-console}

1. Entrada [!DNL Experience Manager] interfaz, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. Desde el **[!UICONTROL Modelos de flujo de trabajo]** , seleccione la **[!UICONTROL Recursos de etiquetas inteligentes DAM]** flujo de trabajo y haga clic en **[!UICONTROL Iniciar flujo de trabajo]** en la barra de herramientas.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. En el **[!UICONTROL Ejecutar flujo de trabajo]** , vaya a la carpeta de carga útil que contiene los recursos en los que desea aplicar las etiquetas automáticamente.
1. Especifique un título para el flujo de trabajo y un comentario opcional. Clic **[!UICONTROL Ejecutar]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Para comprobar si el servicio de contenido inteligente ha etiquetado correctamente los recursos, vaya a la carpeta de recursos y revise las etiquetas.

#### Etiquetado de recursos de la cronología {#tagging-assets-from-the-timeline}

1. Desde el [!DNL Assets] interfaz de usuario, seleccione la carpeta que contiene los recursos o los recursos específicos a los que desea aplicar las etiquetas inteligentes.
1. En la esquina superior izquierda, abra el **[!UICONTROL Cronología]**.
1. Abra las acciones desde la parte inferior de la barra lateral izquierda y haga clic en **[!UICONTROL Iniciar flujo de trabajo]**.

   ![start_workflow](assets/start_workflow.png)

1. Seleccione el **[!UICONTROL Recursos de etiqueta inteligente DAM]** y especifique un título para el flujo de trabajo.
1. Clic **[!UICONTROL Inicio]**. El flujo de trabajo aplica etiquetas a los recursos. para comprobar si el servicio de contenido inteligente ha etiquetado correctamente los recursos, vaya a la carpeta de recursos y revise las etiquetas.

>[!NOTE]
>
>En los ciclos de etiquetado siguientes, solo los recursos modificados se vuelven a etiquetar con etiquetas recién formadas. Sin embargo, incluso los recursos sin modificar se etiquetan si el espacio entre los ciclos de etiquetado último y actual para el flujo de trabajo de etiquetado supera las 24 horas. Para los flujos de trabajo de etiquetado periódicos, los recursos sin modificar se etiquetan cuando el lapso de tiempo supera los seis meses.

## Depurar o moderar las etiquetas inteligentes aplicadas {#manage-smart-tags}

Puede depurar las etiquetas inteligentes para eliminar cualquier etiqueta inexacta asignada a las imágenes de su marca, de modo que solo se muestren las etiquetas más relevantes.

La moderación de las etiquetas inteligentes también ayuda a refinar las búsquedas de imágenes basadas en etiquetas, ya que garantiza que la imagen aparezca en los resultados de búsqueda de las etiquetas más relevantes. Básicamente, ayuda a eliminar las posibilidades de que las imágenes no relacionadas se muestren en los resultados de búsqueda.

También puede asignar una clasificación más alta a una etiqueta para aumentar su relevancia para una imagen. Promocionar una etiqueta para una imagen aumenta las posibilidades de que la imagen aparezca en los resultados de búsqueda cuando se busca la etiqueta en particular.

1. En el cuadro de búsqueda, busque recursos basados en una etiqueta como palabra clave.
1. Para identificar una imagen que no encuentre relevante para la búsqueda, revise los resultados de la búsqueda.
1. Seleccione la imagen y haga clic en **[!UICONTROL Administrar etiquetas]** en la barra de herramientas.
1. Desde el **[!UICONTROL Administrar etiquetas]** , revise las etiquetas. Si no desea buscar la imagen según una etiqueta específica, seleccione la etiqueta y haga clic en **[!UICONTROL Eliminar]** en la barra de herramientas. También puede hacer clic en `x` símbolo que aparece junto a una etiqueta.
1. De forma opcional, para asignar una clasificación más alta a una etiqueta, seleccione la etiqueta y haga clic en **[!UICONTROL Promocionar]** en la barra de herramientas. La etiqueta que promueva se moverá al **[!UICONTROL Etiquetas]** sección.
1. Clic **[!UICONTROL Guardar]** y luego haga clic en **[!UICONTROL OK]**
1. Vaya a **[!UICONTROL Propiedades]** página para la imagen. Observe que a la etiqueta promocionada se le asigna más relevancia y aparece antes en los resultados de búsqueda.

## Sugerencias y limitaciones {#tips-best-practices-limitations}

* Para entrenar el modelo, utilice las imágenes más adecuadas. El curso de formación no se puede revertir o el modelo de formación no se puede eliminar. La precisión del etiquetado depende de la formación actual, por lo que debe hacerlo con cuidado.
* El uso de los servicios de contenido inteligente está limitado a un máximo de 2 millones de imágenes etiquetadas al año. Todas las imágenes duplicadas que se procesan y etiquetan se cuentan como imágenes etiquetadas.
* Si ejecuta el flujo de trabajo de etiquetado desde la cronología, puede aplicar etiquetas en un máximo de 15 recursos a la vez.
* Las etiquetas inteligentes solo funcionan para formatos de imagen PNG y JPG. Por lo tanto, los recursos compatibles que tengan representaciones creadas en estos dos formatos se etiquetan con etiquetas inteligentes.
