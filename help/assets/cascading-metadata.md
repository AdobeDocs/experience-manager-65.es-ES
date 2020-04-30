---
title: Metadatos en cascada en [!DNL Adobe Experience Manager Assets].
description: En este artículo se describe cómo definir metadatos en cascada para los recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Metadatos en cascada {#cascading-metadata}

Al capturar la información de metadatos de un recurso, los usuarios proporcionan información en los distintos campos disponibles. Puede mostrar campos de metadatos específicos o valores de campo que dependen de las opciones seleccionadas en los demás campos. Esta visualización condicional de metadatos se denomina metadatos en cascada. En otras palabras, puede crear una dependencia entre un valor o campo de metadatos concreto y uno o más campos y/o sus valores.

Utilice esquemas de metadatos para definir reglas para mostrar metadatos en cascada. Por ejemplo, si el esquema de metadatos incluye un campo de tipo de recurso, puede definir un conjunto pertinente de campos para mostrar en función del tipo de recurso seleccionado por el usuario.

A continuación se indican algunos casos de uso para los que puede definir metadatos en cascada:

* Cuando se requiera la ubicación del usuario, se mostrarán los nombres de ciudades relevantes en función de la elección de país y estado del usuario.
* Cargue nombres de marcas pertinentes en una lista en función de la elección de categoría del producto por parte del usuario.
* Alternar la visibilidad de un campo concreto en función del valor especificado en otro campo. Por ejemplo, muestre campos de dirección de envío separados si el usuario desea que el envío se envíe en una dirección diferente.
* Designar un campo como obligatorio según el valor especificado en otro campo.
* Cambiar las opciones mostradas para un campo concreto en función del valor especificado en otro campo.
* Establezca el valor de metadatos predeterminado en un campo concreto en función del valor especificado en otro campo.

## Configurar metadatos en cascada en [!DNL Experience Manager]{#configure-cascading-metadata-in-aem}

Imagine un escenario en el que desee mostrar metadatos en cascada en función del tipo de recurso seleccionado. Algunos ejemplos

* Para un vídeo, muestre los campos aplicables como formato, códec, duración, etc.
* Para un documento de Word o PDF, muestre campos como, por ejemplo, recuento de páginas, autor, etc.

Independientemente del tipo de recurso elegido, muestre la información de copyright como campo requerido.

1. En [!DNL Experience Manager] la interfaz, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > Esquemas **** de metadatos.
1. In the **[!UICONTROL Schema Forms]** page, select a schema form and then click **[!UICONTROL Edit]** from the toolbar to edit the schema.

   ![select_form](assets/select_form.png)

1. (Opcional) En el editor de esquemas de metadatos, cree un nuevo campo para condicionalizar. Especifique un nombre y una ruta de acceso a la propiedad en la ficha **[!UICONTROL Configuración]** .

   Para crear una nueva ficha, haga clic en `+` para agregar una ficha y, a continuación, agregue un campo de metadatos.

   ![add_tab](assets/add_tab.png)

1. Añada un campo desplegable para el tipo de recurso. Especifique un nombre y una ruta de acceso a la propiedad en la ficha **[!UICONTROL Configuración]** . Añada una descripción opcional.

   ![asset_type_field](assets/asset_type_field.png)

1. Los pares de clave-valor son las opciones proporcionadas a un usuario del formulario. Puede proporcionar los pares clave-valor manualmente o desde un archivo JSON.

   * Para especificar los valores manualmente, seleccione **[!UICONTROL Añadir manualmente]**, haga clic en **[!UICONTROL Añadir opción]** y especifique el texto y el valor de la opción. Por ejemplo, especifique los tipos de recursos de vídeo, PDF, Word e imagen.

   * Para recuperar los valores de un archivo JSON de forma dinámica, seleccione **[!UICONTROL Añadir a través de ruta]** JSON y proporcione la ruta del archivo JSON. [!DNL Experience Manager] Obtiene los pares clave-valor en tiempo real cuando se presenta el formulario al usuario.
   Ambas opciones son mutuamente excluyentes. No puede importar las opciones de un archivo JSON y editarlas manualmente.

   ![add_choice](assets/add_choice.png)

   >[!NOTE]
   >
   >Al agregar un archivo JSON, los pares clave-valor no se muestran en el editor de esquema de metadatos, sino que están disponibles en el formulario publicado.

   >[!NOTE]
   >
   >Al agregar opciones, si hace clic en el campo Desplegable, la interfaz se distorsiona y el icono Eliminar de las opciones deja de funcionar. No haga clic en el menú desplegable hasta que guarde los cambios. Si tiene este problema, guarde el esquema y ábralo de nuevo para continuar con la edición.

1. (Opcional) Añada los demás campos obligatorios. Por ejemplo, formato, códec y duración para el vídeo de tipo de recurso.

   Del mismo modo, agregue campos dependientes para otros tipos de recursos. Por ejemplo, agregue campos de recuento de páginas y autor para recursos de documento, como archivos PDF y Word.

   ![video_dependiente_fields](assets/video_dependent_fields.png)

1. Para crear una dependencia entre el campo de tipo de recurso y otros campos, elija el campo dependiente y abra la ficha **[!UICONTROL Reglas]** .

   ![select_Depenentfield](assets/select_dependentfield.png)

1. Under **[!UICONTROL Requirement]**, choose the **[!UICONTROL Required, based on new rule]** option.
1. Click **[!UICONTROL Add Rule]** and choose the **[!UICONTROL Asset Type]** field to create a dependency. También elija el valor del campo en el que desea crear la dependencia. En este caso, seleccione **[!UICONTROL Vídeo]**. Click **[!UICONTROL Done]** to save the changes.

   ![define_rule](assets/define_rule.png)

   >[!NOTE]
   >
   >La lista desplegable con valores predefinidos manualmente se puede utilizar con las reglas. Los menús desplegables con una ruta JSON configurada no se pueden utilizar con reglas que utilicen valores predefinidos para aplicar condiciones. Si los valores se cargan desde JSON en tiempo de ejecución, no es posible aplicar una regla predefinida.

1. En **[!UICONTROL Visibilidad]**, seleccione la opción **[!UICONTROL Visible, según la nueva regla]**.

1. Click **[!UICONTROL Add Rule]** and choose the **[!UICONTROL Asset Type]** field to create a dependency. También elija el valor del campo en el que desea crear la dependencia. En este caso, seleccione **[!UICONTROL Vídeo]**. Click **[!UICONTROL Done]** to save the changes.

   ![define_visibilityrule](assets/define_visibilityrule.png)

   >[!NOTE]
   >
   >Al hacer clic en un espacio en blanco (o en cualquier lugar que no sea el valor) se restablecen los valores. Si sucede, vuelva a seleccionar los valores.

   >[!NOTE]
   >
   >Puede aplicar condiciones de **[!UICONTROL requisito]** y **[!UICONTROL visibilidad]** independientes entre sí.

1. Del mismo modo, cree una dependencia entre el valor Vídeo en el campo Tipo de recurso y otros campos, como Códec y Duración.
1. Repita los pasos para crear dependencia entre recursos de documento (PDF y Word) en el campo Tipo [!UICONTROL de] recurso y campos como Recuento [!UICONTROL de] páginas y [!UICONTROL Autor].
1. Haga clic en **[!UICONTROL Guardar.]** Aplique el esquema de metadatos a una carpeta.

1. Vaya a la carpeta a la que ha aplicado el Esquema Metadatos y abra la página de propiedades de un recurso. Según lo que elija en el campo Tipo de recurso, se muestran los campos de metadatos correspondientes en cascada.

   ![Metadatos en cascada para un recurso de vídeo](assets/video_asset.png)

   *Figura: Metadatos en cascada para un vídeo.*

   ![Metadatos en cascada para el recurso de documento](assets/doc_type_fields.png)

   *Figura: Metadatos en cascada para un documento.*
