---
title: Etiquetas inteligentes mejoradas
description: Etiquetas inteligentes mejoradas
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0560eb8e3c127964920827609a9982acf07b515f
workflow-type: tm+mt
source-wordcount: '1514'
ht-degree: 2%

---


# Comprender, aplicar y conservar etiquetas inteligentes {#enhanced-smart-tags}

Las organizaciones que se ocupan de los activos digitales utilizan cada vez más el vocabulario controlado por taxonomía en los metadatos de los recursos. Básicamente, incluye una lista de palabras clave que los empleados, socios y clientes utilizan comúnmente para referirse a los recursos digitales de una clase en particular y buscarlos. El etiquetado de activos con vocabulario controlado por taxonomía garantiza que los activos se puedan identificar y recuperar fácilmente.

En comparación con los vocabularios del lenguaje natural, etiquetar los activos digitales en función de la taxonomía empresarial ayuda a alinearlos con el negocio de una compañía y garantiza que los activos más relevantes aparezcan en las búsquedas.

Por ejemplo, un fabricante de automóviles puede etiquetar imágenes de automóviles con nombres de modelos para que solo aparezcan imágenes relevantes cuando se buscan imágenes de varios modelos para diseñar una campaña de promoción.

Para que el servicio de contenido inteligente aplique las etiquetas correctas, debe formarlo para que reconozca su taxonomía. Para entrenar el servicio, seleccione primero un conjunto de recursos y etiquetas que describan mejor estos recursos. Aplique estas etiquetas a los recursos y ejecute un flujo de trabajo de formación para ayudar al servicio a aprender.

Una vez preparada y preparada la etiqueta, el servicio ahora puede aplicarla a los recursos mediante un flujo de trabajo de etiquetado.

En segundo plano, Smart Content Service utiliza el marco de trabajo de Adobe Sensei AI para entrenar su algoritmo de reconocimiento de imágenes en la estructura de etiquetas y la taxonomía empresarial. Esta inteligencia de contenido se utiliza para aplicar etiquetas relevantes a un conjunto diferente de recursos.

Smart Content Service es un servicio en la nube alojado en [!DNL Adobe I/O]. Para utilizarlo en [!DNL Adobe Experience Manager], el administrador del sistema debe integrar su implementación [!DNL Experience Manager] con [!DNL Adobe I/O].

En resumen, estos son los pasos principales para utilizar el servicio de contenido inteligente:

* Incorporación
* Revisión de recursos y etiquetas (definición de taxonomía)
* Formación del servicio de contenido inteligente
* Etiquetado automático

![Diagrama de flujo](assets/flowchart.gif)

## Requisitos previos {#prerequisites}

Antes de utilizar el servicio de contenido inteligente, asegúrese de lo siguiente para crear una integración en [!DNL Adobe I/O]:

* Cuenta de Adobe ID que tiene privilegios de administrador para la organización.
* El servicio de Smart Content Service está habilitado para su organización.
* El paquete base de servicios de contenido inteligente solo se puede agregar a una implementación en la que se hayan otorgado licencias para un paquete base [!DNL Adobe Experience Manager Sites] y un complemento [!DNL Assets].

## Incorporación {#onboarding}

El servicio de contenido inteligente está disponible para su compra como complemento de [!DNL Experience Manager]. Después de realizar la compra, se envía un correo electrónico al administrador de la organización con un vínculo a [!DNL Adobe I/O].

El administrador puede seguir el vínculo para integrar el servicio de contenido inteligente con [!DNL Experience Manager]. Para integrar el servicio con [!DNL Experience Manager Assets], consulte [Configuración de etiquetas inteligentes](config-smart-tagging.md).

El proceso de integración se completa cuando el administrador configura el servicio y agrega usuarios en [!DNL Experience Manager].

>[!NOTE]
>
>Si está utilizando [!DNL Experience Manager] 6.3 o una versión anterior y necesita un servicio de etiquetado para sus recursos, consulte [Etiquetas inteligentes](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html). Las etiquetas inteligentes no utilizan las últimas funciones de AI y, por tanto, son menos precisas que el servicio de etiquetado inteligente mejorado.

## Revisar recursos y etiquetas {#reviewing-assets-and-tags}

Una vez que esté a bordo, lo primero que desea hacer es identificar un conjunto de etiquetas que describan mejor estas imágenes en el contexto de su negocio.

A continuación, revise las imágenes para identificar un conjunto de imágenes que mejor representen el producto para un requerimiento comercial determinado. Asegúrese de que los recursos del conjunto depurado cumplen las [pautas de capacitación del servicio de contenido inteligente](/help/assets/config-smart-tagging.md#training-the-smart-content-service).

Añada los recursos a una carpeta y aplique las etiquetas a cada recurso desde la página de propiedades. A continuación, ejecute el flujo de trabajo de formación en esta carpeta. El conjunto depurado de recursos permite que el servicio de contenido inteligente imparta formación eficaz a más recursos mediante las definiciones de taxonomía.

>[!NOTE]
>
>1. La formación es un proceso irrevocable. Adobe recomienda revisar las etiquetas del conjunto depurado de recursos antes de formarlo con las etiquetas.
>1. Antes de la formación para una etiqueta, consulte [Directrices de capacitación del servicio de contenido inteligente](/help/assets/config-smart-tagging.md#training-the-smart-content-service).
>1. Cuando entrena el servicio de contenido inteligente por primera vez, Adobe recomienda que lo imparta en al menos dos etiquetas diferentes.


## Comprender los resultados de la búsqueda [!DNL Experience Manager] con las etiquetas inteligentes {#understandsearch}

De manera predeterminada, la búsqueda [!DNL Experience Manager] combina los términos de búsqueda con una cláusula `AND`. El uso de etiquetas inteligentes no cambia este comportamiento predeterminado. El uso de etiquetas inteligentes agrega una cláusula `OR` adicional para encontrar cualquiera de los términos de búsqueda relacionados con las etiquetas inteligentes. Por ejemplo: considere buscar `woman running`. Los recursos con sólo `woman` o `running` palabra clave en los metadatos no aparecen en los resultados de búsqueda de forma predeterminada. Sin embargo, un recurso etiquetado con `woman` o `running` mediante etiquetas inteligentes aparece en una consulta de búsqueda de este tipo. Los resultados de la búsqueda son una combinación de:

* Recursos con palabras clave `woman` y `running` en los metadatos.

* Recursos etiquetados de forma inteligente con cualquiera de las palabras clave.

Los resultados de búsqueda que coinciden con todos los términos de búsqueda en los campos de metadatos se muestran primero, seguidos de los resultados de búsqueda que coinciden con cualquiera de los términos de búsqueda en las etiquetas inteligentes. En el ejemplo anterior, el orden aproximado de visualización de los resultados de búsqueda es:

1. Coincide con `woman running` en los distintos campos de metadatos.
1. Coincide con `woman running` en las etiquetas inteligentes.
1. Coincide con `woman` o con `running` en las etiquetas inteligentes.

>[!CAUTION]
>
>Si la indexación de Lucene se realiza a partir de [!DNL Adobe Experience Manager], la búsqueda basada en etiquetas inteligentes no funciona de la manera esperada.

## Etiquetar recursos automáticamente {#tagging-assets-automatically}

Una vez que haya formado el servicio de contenido inteligente, puede aplicar el déclencheur del flujo de trabajo de etiquetado para aplicar automáticamente las etiquetas correspondientes a un conjunto diferente de recursos similares.

Puede ejecutar el flujo de trabajo de etiquetado de forma periódica o siempre que sea necesario.

>[!NOTE]
>
>El flujo de trabajo de etiquetado se ejecuta tanto en los recursos como en las carpetas.

### Etiquetado periódico {#periodic-tagging}

Puede activar el servicio de contenido inteligente para etiquetar recursos periódicamente dentro de una carpeta. Abra la página de propiedades de la carpeta de recursos, seleccione **[!UICONTROL Habilitar etiquetas inteligentes]** en la ficha **[!UICONTROL Detalles]** y guarde los cambios.

Una vez seleccionada esta opción para una carpeta, el servicio de contenido inteligente etiqueta automáticamente los recursos de la carpeta. De forma predeterminada, el flujo de trabajo de etiquetado se ejecuta todos los días a las 12:00 AM.

### Etiquetado a petición {#on-demand-tagging}

Puede déclencheur del flujo de trabajo de etiquetado desde la consola de flujo de trabajo o desde la línea de tiempo para etiquetar los recursos al instante.

>[!NOTE]
>
>Si ejecuta el flujo de trabajo de etiquetado desde la línea de tiempo, puede aplicar etiquetas a un máximo de 15 recursos a la vez.

#### Etiquetar recursos desde la consola de flujo de trabajo {#tagging-assets-from-the-workflow-console}

1. En la interfaz [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página **[!UICONTROL Modelos de flujo de trabajo]**, seleccione el flujo de trabajo **[!UICONTROL Recursos de etiquetas inteligentes DAM]** y haga clic en **[!UICONTROL Flujo de trabajo de Inicio]** en la barra de herramientas.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. En el cuadro de diálogo **[!UICONTROL Ejecutar flujo de trabajo]**, busque la carpeta de carga útil que contiene los recursos en los que desea aplicar las etiquetas automáticamente.
1. Especifique un título para el flujo de trabajo y un comentario opcional. Haga clic en **[!UICONTROL Ejecutar]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Vaya a la carpeta de recursos y revise las etiquetas para comprobar si el servicio de contenido inteligente ha etiquetado los recursos correctamente.

#### Etiquetar recursos de la línea de tiempo {#tagging-assets-from-the-timeline}

1. En la interfaz de usuario [!DNL Assets], seleccione la carpeta que contenga recursos o recursos específicos a los que desee aplicar etiquetas inteligentes.
1. En la esquina superior izquierda, abra la **[!UICONTROL Línea de tiempo]**.
1. Abra acciones desde la parte inferior de la barra lateral izquierda y haga clic en **[!UICONTROL Flujo de trabajo de Inicio]**.

   ![inicio_workflow](assets/start_workflow.png)

1. Seleccione el flujo de trabajo **[!UICONTROL Recursos de etiquetas inteligentes DAM]** y especifique un título para el flujo de trabajo.
1. Haga clic en **[!UICONTROL Inicio]**. El flujo de trabajo aplica las etiquetas a los recursos. Vaya a la carpeta de recursos y revise las etiquetas para comprobar si el servicio de contenido inteligente ha etiquetado los recursos correctamente.

>[!NOTE]
>
>En los ciclos de etiquetado posteriores, solo los recursos modificados se etiquetan de nuevo con etiquetas recién formadas. Sin embargo, incluso los recursos sin modificar se etiquetan si el espacio entre los ciclos de etiquetado más recientes y más recientes para el flujo de trabajo de etiquetado supera las 24 horas. Para los flujos de trabajo de etiquetado periódicos, los recursos sin modificar se etiquetan cuando el lapso de tiempo supera los seis meses.

## Depurar o moderar las etiquetas inteligentes aplicadas {#manage-smart-tags}

Puede depurar las etiquetas inteligentes para eliminar cualquier etiqueta incorrecta que se haya asignado a las imágenes de su marca, de modo que solo se muestren las etiquetas más relevantes.

La moderación de las etiquetas inteligentes también ayuda a restringir las búsquedas de imágenes basadas en etiquetas, ya que garantiza que la imagen aparezca en los resultados de búsqueda de las etiquetas más relevantes. Básicamente, ayuda a eliminar las posibilidades de que las imágenes no relacionadas aparezcan en los resultados de búsqueda.

También puede asignar una clasificación superior a una etiqueta para aumentar su relevancia con respecto a una imagen. La promoción de una etiqueta para una imagen aumenta las posibilidades de que la imagen aparezca en los resultados de búsqueda cuando se realiza una búsqueda en función de la etiqueta en particular.

1. En el cuadro Omniture, busque recursos basados en una etiqueta.
1. Inspect muestra los resultados de la búsqueda para identificar una imagen que no le parece relevante para la búsqueda.
1. Seleccione la imagen y haga clic en **[!UICONTROL Administrar etiquetas]** en la barra de herramientas.
1. En la página **[!UICONTROL Administrar etiquetas]**, inspeccione las etiquetas. Si no desea buscar la imagen en función de una etiqueta específica, seleccione la etiqueta y haga clic en **[!UICONTROL Eliminar]** en la barra de herramientas. También puede hacer clic en el símbolo `x` que aparece junto a una etiqueta.
1. Opcionalmente, para asignar una clasificación superior a una etiqueta, seleccione la etiqueta y haga clic en **[!UICONTROL Promocionar]** en la barra de herramientas. La etiqueta que promocione se moverá a la sección **[!UICONTROL Etiquetas]**.
1. Haga clic en **[!UICONTROL Guardar]** y luego en **[!UICONTROL Aceptar]**
1. Vaya a la página **[!UICONTROL Propiedades]** de la imagen. Observe que la etiqueta que promocionó tiene más relevancia y aparece antes en los resultados de búsqueda.

## Sugerencias y limitaciones {#tips-best-practices-limitations}

* El uso de Smart Content Services está limitado a hasta 2 millones de imágenes etiquetadas por año. Todas las imágenes de duplicado procesadas y etiquetadas se cuentan como imágenes etiquetadas.
* Si ejecuta el flujo de trabajo de etiquetado desde la línea de tiempo, puede aplicar etiquetas a un máximo de 15 recursos a la vez.
