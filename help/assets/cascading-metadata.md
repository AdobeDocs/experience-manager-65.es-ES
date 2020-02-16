---
title: Metadatos en cascada
description: En este artículo se describe cómo definir metadatos en cascada para los recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Metadatos en cascada {#cascading-metadata}

Al capturar la información de metadatos de un recurso, los usuarios proporcionan información en los distintos campos disponibles. Puede mostrar campos de metadatos específicos o valores de campo que dependen de las opciones seleccionadas en los demás campos. Esta visualización condicional de metadatos se denomina metadatos en cascada. En otras palabras, puede crear una dependencia entre un valor o campo de metadatos concreto y uno o más campos y/o sus valores.

Utilice esquemas de metadatos para definir reglas para mostrar metadatos en cascada. Por ejemplo, si el esquema de metadatos incluye un campo de tipo de recurso, puede definir un conjunto pertinente de campos para mostrar en función del tipo de recurso que seleccione un usuario.

A continuación se indican algunos casos de uso para los que puede definir metadatos en cascada:

* Cuando se requiera la ubicación del usuario, se mostrarán los nombres de ciudades relevantes en función de la elección de país y estado del usuario.
* Cargue los nombres de marcas pertinentes en una lista basada en la selección de categoría de producto del usuario.
* Alternar la visibilidad de un campo concreto en función del valor especificado en otro campo. Por ejemplo, muestre campos de dirección de envío separados si el usuario desea que el envío se envíe en una dirección diferente.
* Designar un campo como obligatorio según el valor especificado en otro campo.
* Cambiar las opciones mostradas para un campo concreto en función del valor especificado en otro campo.
* Establezca el valor de metadatos predeterminado en un campo concreto en función del valor especificado en otro campo.

## Configuración de metadatos en cascada en AEM {#configure-cascading-metadata-in-aem}

Imagine un escenario en el que desee mostrar metadatos en cascada en función del tipo de recurso seleccionado. Algunos ejemplos

* Para un vídeo, muestre los campos aplicables como formato, códec, duración, etc.
* Para un documento de Word o PDF, muestre campos como, por ejemplo, recuento de páginas, autor, etc.

Independientemente del tipo de recurso elegido, muestre la información de copyright como campo requerido.

1. Toque o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > Esquemas **[!UICONTROL de metadatos]**.
1. En la página Formularios **[!UICONTROL de]** esquema, seleccione un formulario de esquema y, a continuación, toque o haga clic en **[!UICONTROL Editar]** en la barra de herramientas para editar el esquema.

   ![select_form](assets/select_form.png)

1. (Opcional) En el editor de esquemas de metadatos, cree un nuevo campo para condicionalizar. Especifique un nombre y una ruta de acceso a la propiedad en la ficha **[!UICONTROL Configuración]** .

   Para crear una nueva ficha, toque o haga clic `+` para agregar una ficha y, a continuación, agregue un campo de metadatos.

   ![add_tab](assets/add_tab.png)

1. Agregue un campo Desplegable para el tipo de recurso. Especifique un nombre y una ruta de acceso a la propiedad en la ficha **[!UICONTROL Configuración]** . Agregue una descripción opcional.

   ![asset_type_field](assets/asset_type_field.png)

1. Los pares de clave-valor son las opciones proporcionadas a un usuario del formulario. Puede proporcionar los pares clave-valor manualmente o desde un archivo JSON.

   * Para especificar los valores manualmente, seleccione **[!UICONTROL Agregar manualmente]**, toque o haga clic en **[!UICONTROL Agregar opción]** y especifique el texto y el valor de la opción. Por ejemplo, especifique los tipos de recursos de vídeo, PDF, Word e imagen.

   * Para recuperar los valores de un archivo JSON de forma dinámica, seleccione **[!UICONTROL Agregar a través de ruta]** JSON y proporcione la ruta del archivo JSON. AEM obtiene los pares clave-valor en tiempo real cuando se presenta el formulario al usuario.
   Ambas opciones son mutuamente excluyentes. No puede importar las opciones de un archivo JSON y editarlas manualmente.

   ![add_choice](assets/add_choice.png)

   >[!NOTE]
   >
   >Al agregar un archivo JSON, los pares clave-valor no se muestran en el editor de esquemas de metadatos, sino que están disponibles en el formulario publicado.

   >[!NOTE]
   >
   >Al agregar opciones, si hace clic en el campo Desplegable, la interfaz se distorsiona y el icono Eliminar de las opciones deja de funcionar. No haga clic en el menú desplegable hasta que guarde los cambios. Si tiene este problema, guarde el esquema y ábralo de nuevo para continuar con la edición.

1. (Opcional) Agregue los demás campos obligatorios. Por ejemplo, formato, códec y duración para el vídeo de tipo de recurso.

   Del mismo modo, agregue campos dependientes para otros tipos de recursos. Por ejemplo, agregue campos de recuento de páginas y autor para los recursos de documentos, como archivos PDF y Word.

   ![video_dependiente_fields](assets/video_dependent_fields.png)

1. Para crear una dependencia entre el campo de tipo de recurso y otros campos, elija el campo dependiente y abra la ficha **[!UICONTROL Reglas]** .

   ![select_Depenentfield](assets/select_dependentfield.png)

1. En **[!UICONTROL Requisito]**, elija la opción **[!UICONTROL Requerido, según la nueva regla]** .
1. Toque o haga clic en **[!UICONTROL Agregar regla]** y elija el campo Tipo **[!UICONTROL de]** recurso para crear una dependencia. También elija el valor del campo en el que desea crear la dependencia. En este caso, elija **[!UICONTROL Vídeo]**. Tap/click **[!UICONTROL Done]** to save the changes.

   ![define_rule](assets/define_rule.png)

   >[!NOTE]
   >
   >La lista desplegable con valores predefinidos manualmente se puede utilizar con las reglas. Los menús desplegables con una ruta JSON configurada no se pueden utilizar con reglas que utilicen valores predefinidos para aplicar condiciones. Si los valores se cargan desde JSON en tiempo de ejecución, no es posible aplicar una regla predefinida.

1. En **[!UICONTROL Visibilidad]**, elija la opción **[!UICONTROL Visible, según la nueva regla]** .

1. Toque o haga clic en **[!UICONTROL Agregar regla]** y elija el campo Tipo **[!UICONTROL de]** recurso para crear una dependencia. También elija el valor del campo en el que desea crear la dependencia. En este caso, elija **[!UICONTROL Vídeo]**. Tap/click **[!UICONTROL Done]** to save the changes.

   ![define_visibilityrule](assets/define_visibilityrule.png)

   >[!NOTE]
   >
   >Al tocar o hacer clic en un espacio en blanco (o en cualquier lugar que no sea el valor) se restablecen los valores. Si sucede, vuelva a seleccionar los valores.

   >[!NOTE]
   >
   >Puede aplicar condiciones de **[!UICONTROL requisito]** y **[!UICONTROL visibilidad]** independientes entre sí.

1. Del mismo modo, cree una dependencia entre el valor Vídeo en el campo Tipo de recurso y otros campos, como Códec y Duración.
1. Repita los pasos para crear dependencia entre los recursos del documento (PDF y Word) en el campo Tipo [!UICONTROL de] recurso y campos como Recuento [!UICONTROL de] páginas y [!UICONTROL Autor].
1. Haga clic en **[!UICONTROL Guardar.]** Aplique el esquema de metadatos a una carpeta.

1. Vaya a la carpeta a la que ha aplicado el esquema de metadatos y abra la página de propiedades de un recurso. Según lo que elija en el campo Tipo de recurso, se muestran los campos de metadatos correspondientes en cascada.

   ![Metadatos en cascada para un recurso de vídeo](assets/video_asset.png)
   *Figura: Metadatos en cascada para un vídeo*

   ![Metadatos en cascada para el recurso de documento](assets/doc_type_fields.png)
   *Figura: Metadatos en cascada para un documento*
