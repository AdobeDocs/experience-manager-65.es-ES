---
title: Gestión de colecciones de recursos digitales
description: Obtenga información sobre tareas para administrar colecciones de recursos, como crear, vista, eliminar, editar y descargar colecciones.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: cedefb58919d7d215040e72b4cc41159161938a8
workflow-type: tm+mt
source-wordcount: '2178'
ht-degree: 11%

---


# Administrar colecciones {#managing-collections}

Una colección es un conjunto de recursos dentro de [!DNL Adobe Experience Manager Assets]. Utilice colecciones para compartir recursos entre usuarios. El conjunto puede ser una colección estática o una colección dinámica basada en los resultados de la búsqueda.

A diferencia de las carpetas, una colección puede incluir recursos de distintas ubicaciones. Puede compartir colecciones con varios usuarios a los que se han asignado diferentes niveles de privilegios, como ver, editar, etc.

Puede compartir varias colecciones con un usuario. Cada colección contiene referencias a recursos. La integridad referencial de los recursos se mantiene en todas las colecciones.

Las colecciones son de los siguientes tipos, según la forma en que recopilan los recursos:

* Colección que contiene una lista de referencia estática de recursos, carpetas y otras colecciones.

* Colección inteligente que incluye de forma dinámica recursos basados en criterios de búsqueda.

## Acceso a la consola de colecciones {#navigating-the-collections-console}

Para abrir las **[!UICONTROL colecciones]**, en la [!DNL Experience Manager] interfaz, vaya a **[!UICONTROL Recursos]** > **[!UICONTROL Colecciones]**.

## Creación de una colección {#creating-a-collection}

Puede crear una colección con referencias [](#creating-a-collection-with-static-references) estáticas o basada en un filtro [basado en criterios de](#creating-a-smart-collection)búsqueda. También puede crear una colección a partir de una caja de iluminación.

### Creación de una colección con referencias estáticas {#creating-a-collection-with-static-references}

Puede crear una colección con referencias estáticas, por ejemplo, una colección con referencias a recursos, carpetas, colecciones, conjuntos de giros y conjuntos de imágenes.

1. Vaya a la consola **[!UICONTROL Colecciones]** .
1. En la barra de herramientas, haga clic en **[!UICONTROL Crear]**.
1. En la página **[!UICONTROL Crear colección]** , introduzca un título y una descripción opcional para la colección.
1. Agregue miembros a la colección y asigne los permisos correspondientes. Como alternativa, seleccione **[!UICONTROL Colección pública]** para permitir que todos los usuarios tengan acceso a la colección.

   >[!NOTE]
   >
   >Para permitir que los miembros compartan colecciones con otros usuarios, proporcione los permisos de lectura del `dam-users` grupo en la ruta `home/users`. Otorgue permiso a los usuarios en la `/content/dam/collections` ubicación para permitir que los usuarios realicen la vista de las colecciones en listas emergentes. Como alternativa, haga que el usuario forme parte del `dam-users` grupo.

1. (Opcional) Añada una imagen en miniatura para la colección.
1. Click **[!UICONTROL Create]**, and then click **[!UICONTROL OK]** to close the dialog. En la consola Colecciones se abre una colección con el título y las propiedades especificados.

   >[!NOTE]
   >
   >[!DNL Experience Manager Assets] le permite crear tareas de revisión para una colección de forma similar a como crea tareas de revisión para una carpeta de recursos.

   Para añadir recursos a la colección, vaya a la interfaz de usuario [!DNL Assets] . Para obtener más información, consulte [Añadir recursos en una colección](#adding-assets-to-a-collection).

### Creación de colecciones mediante dropzone {#create-collections-using-dropzone}

Puede arrastrar recursos de la interfaz de usuario a una colección [!DNL Assets] . También puede crear una copia de una colección y arrastrar los recursos allí.

1. En la interfaz de usuario, seleccione los recursos que desee agregar a una colección. [!DNL Assets]
1. Arrastre los recursos a la zona **[!UICONTROL Colocar en colección]** . Como alternativa, haga clic en **[!UICONTROL A colección]** en la barra de herramientas.

   ![drop_in_collection](assets/drop_in_collection.png)

1. In the **[!UICONTROL Add To Collection]** page, click **[!UICONTROL Create Collection]** from the toolbar.

   If you want to add the assets to an existing collection, select it from the page, and click **[!UICONTROL Add]**. De forma predeterminada, se selecciona la colección con la fecha de actualización más reciente.

1. En el cuadro de diálogo **[!UICONTROL Crear nueva colección]**, indique un nombre para la colección. Si desea que todos los usuarios tengan acceso a la colección, seleccione **[!UICONTROL Colección pública]**.
1. Haga clic en **[!UICONTROL Continuar]** para crear la colección.

### Creación de una colección inteligente {#creating-a-smart-collection}

Una colección inteligente utiliza criterios de búsqueda para rellenar recursos de forma dinámica. Puede crear una colección inteligente utilizando solo archivos y no carpetas o archivos y carpetas.

Para crear una colección inteligente, siga los pasos:

1. Vaya a la interfaz de usuario y haga clic en [!DNL Assets] Buscar.

1. Escriba la palabra clave de búsqueda en el cuadro Omniture y presione `Enter`. Abra el panel Filtros y aplique un filtro de búsqueda.

1. En la lista **[!UICONTROL Archivos y carpetas]** , seleccione **[!UICONTROL Archivos]**.

   ![files_option](assets/files_option.png)

1. Haga clic en **[!UICONTROL Guardar colección]** inteligente.

1. Especifique un nombre para la colección. Seleccione **[!UICONTROL Público]** para agregar el grupo Usuarios de DAM con la función Visor a la colección inteligente.

   ![save_collection](assets/save_collection.png)

   >[!NOTE]
   >
   >Si selecciona **[!UICONTROL Público]**, la colección inteligente estará disponible para todos los usuarios con la función de propietario después de crearla. Si anula la selección de la opción **[!UICONTROL Público]** , el grupo de usuarios DAM ya no estará asociado a la colección inteligente.

1. Click **[!UICONTROL Save]** to create the smart collection, and then close the message box to complete the process.

   The new smart collection is also added to the **[!UICONTROL Saved Searches]** list.

   ![collection_lists](assets/collection_listing.png)

   The label of the **[!UICONTROL Create Smart Selection]** option changes to **[!UICONTROL Edit Smart Selection]**. Para editar la configuración de la colección inteligente, seleccione **[!UICONTROL Archivos]** en la lista **[!UICONTROL Archivos y carpetas]**. Haga clic en la opción **[!UICONTROL Editar selección]** inteligente para ![editar la colección](assets/do-not-localize/edit-smart-collection.png) inteligente.

## Añadir recursos en una colección {#adding-assets-to-a-collection}

Puede agregar recursos a una colección que contenga una lista de los recursos o carpetas a los que se hace referencia. Las colecciones inteligentes utilizan una consulta de búsqueda para rellenar los recursos. Por lo tanto, las referencias estáticas a recursos y carpetas no son aplicables a ellos.

1. En la interfaz de usuario de [!DNL A]recursos, seleccione el recurso y haga clic en **[!UICONTROL To Collection]** ![add to collection](assets/do-not-localize/add-to-collection.png) (Añadir a colección) en la barra de herramientas.
También puede arrastrar el recurso al área **[!UICONTROL Colocar en colección]** de la interfaz. Añada los recursos cuando la etiqueta de la región cambie a **[!UICONTROL Colocar para Añadir]**.

1. En la página **[!UICONTROL Añadir a colección]** , seleccione la colección a la que desea agregar el recurso.

1. Haga clic en **[!UICONTROL Añadir]** y, a continuación, cierre el mensaje de confirmación. El recurso se agrega a la colección.

## Edición de una colección inteligente {#editing-a-smart-collection}

Las colecciones inteligentes se crean al guardar una búsqueda para que pueda modificar su contenido modificando los parámetros de búsqueda de la búsqueda [](#saved-searches)guardada.

1. En la interfaz de usuario, haga clic en la opción de [!DNL Assets] búsqueda ![](assets/do-not-localize/search_icon.png) de la barra de herramientas.
1. Con el cursor en el cuadro Omniture search, presione la tecla Retorno.
1. En la [!DNL Experience Manager] interfaz, abra el panel Filtros.
1. En la lista **[!UICONTROL Búsquedas guardadas]**, seleccione la colección inteligente que desee modificar. El panel Buscar aparecen los filtros configurados para la búsqueda guardada.

   ![select_smart_collection](assets/select_smart_collection.png)

1. En la lista **[!UICONTROL Archivos y carpetas]** , seleccione **[!UICONTROL Archivos]**.
1. Modifique uno o varios filtros, según sea necesario. Haga clic en **[!UICONTROL Editar colección]** inteligente.

   También puede editar el nombre de la colección inteligente.

   ![edit_smart_collection_dialog](assets/edit_smart_collectiondialog.png)

1. Haga clic en **[!UICONTROL Guardar.]** Aparecerá el cuadro de diálogo **[!UICONTROL Editar colección]** inteligente.
1. Haga clic en **[!UICONTROL Sobrescribir]** para reemplazar la colección inteligente original por la colección editada. También puede seleccionar **[!UICONTROL Guardar como]** para guardar la colección editada por separado.
1. En el cuadro de diálogo de confirmación, haga clic en **[!UICONTROL Guardar]** para completar el proceso.

## Vista y edición de metadatos de la colección {#view-edit-collection-metadata}

Los metadatos de la colección incluyen datos sobre la colección, incluidas las etiquetas que se agreguen.

1. En la consola [!UICONTROL Colecciones] , seleccione una colección y haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas.
1. En la página **[!UICONTROL Metadatos de la colección]**, consulte los metadatos de la colección desde las pestañas **[!UICONTROL Básico]** y **[!UICONTROL Avanzado]**.
1. Modifique los metadatos según sea necesario. Para guardar los cambios, haga clic en **[!UICONTROL Guardar y cerrar]** en la barra de herramientas.

## Editar metadatos de varias colecciones de forma masiva {#editing-collection-metadata-in-bulk}

Puede editar los metadatos de varias colecciones simultáneamente. Esta funcionalidad le ayuda a replicar rápidamente metadatos comunes en varias colecciones.

1. En la consola Colecciones, seleccione dos o más colecciones.
1. En la barra de herramientas, haga clic en **[!UICONTROL Propiedades]**.
1. En la página **[!UICONTROL Metadatos de la colección]**, edite los metadatos en las pestañas **[!UICONTROL Básico]** y **[!UICONTROL Avanzado]**, según sea necesario.
1. Para vista de las propiedades de metadatos de una colección específica, anule la selección de las colecciones restantes de la lista de colecciones. Los campos del editor de metadatos se rellenan con los metadatos de la colección en particular.

   >[!NOTE]
   >
   >* En la página [!UICONTROL Propiedades] , puede quitar colecciones de la lista de colecciones anulando su selección. La lista de colecciones tiene todas las colecciones seleccionadas de forma predeterminada. [!DNL Experience Manager] no actualiza los metadatos de las colecciones que elimina.
   >* En la parte superior de la lista, active la casilla de verificación situada junto a **[!UICONTROL Título]** para alternar entre seleccionar las colecciones y borrar la lista.


1. Haga clic en **[!UICONTROL Guardar y cerrar]** en la barra de herramientas y, a continuación, cierre el cuadro de diálogo de confirmación.
1. To append the new metadata with the existing metadata, select **[!UICONTROL Append mode]**. Si no selecciona esta opción, los metadatos nuevos sustituirán a los metadatos existentes en los campos. Haga clic en **[!UICONTROL Enviar]**.

   >[!NOTE]
   >
   >Los metadatos que se agregan para las colecciones seleccionadas sobrescriben los metadatos anteriores para estas colecciones. Utilice el modo  Anexar para agregar nuevos valores a los metadatos existentes en los campos que pueden contener varios valores. Los campos de un solo valor siempre se sobrescriben. Las etiquetas que agregue al campo [!UICONTROL Etiquetas] se anexan a la lista de etiquetas existente en los metadatos.

Para personalizar la página de [!UICONTROL propiedades] de metadatos, incluida la adición, modificación y eliminación de propiedades de metadatos, utilice el editor de Esquema.

>[!TIP]
>
>El método de edición masiva funciona para los recursos disponibles en una colección. En el caso de los recursos disponibles en varias carpetas o que cumplen un criterio común, es posible actualizar [masivamente los metadatos después de realizar la búsqueda](/help/assets/search-assets.md#metadataupdates).

## Buscar colecciones {#searching-collections}

Puede buscar colecciones desde la consola Colecciones. Cuando realiza una búsqueda con palabras clave en el cuadro Omniture, busca los nombres de la colección, los metadatos y las etiquetas agregadas a las colecciones. [!DNL Assets]

Si busca colecciones desde el nivel superior, solo se devuelven colecciones individuales en los resultados de búsqueda. [!DNL Assets] o las carpetas de las colecciones se excluyen. En todos los demás casos (por ejemplo, dentro de una colección individual o en una jerarquía de carpetas), se devuelven todos los recursos, carpetas y colecciones relevantes.

## Buscar dentro de las colecciones {#searching-within-collections}

En la consola Colecciones, haga clic en una colección para abrirla.

Dentro de una colección, la búsqueda está restringida a los recursos (y sus etiquetas y metadatos) dentro de la colección que está viendo. [!DNL Experience Manager] Al buscar dentro de una carpeta, se devuelven todos los recursos y las carpetas secundarias que coinciden con la carpeta actual. Al buscar dentro de una colección, solo se devuelven los recursos, las carpetas y otras colecciones que coinciden con los miembros directos de la colección.

## Editar la configuración de la colección {#editing-collection-settings}

Puede editar la configuración de la colección, como título y descripción, o bien añadir miembros a una colección.

1. Seleccione una colección y haga clic en **[!UICONTROL Configuración]** en la barra de herramientas. También puede utilizar la acción rápida **[!UICONTROL Configuración]** de la miniatura de la colección.
1. Modifique la configuración de la colección en la página **[!UICONTROL Configuración de la colección]**. For example, modify the collection title, descriptions, members, and permissions as discussed in [Adding Collections](#creating-a-collection).

1. Para guardar los cambios, haga clic en **[!UICONTROL Guardar]**.

## Eliminar una colección {#deleting-a-collection}

1. En la consola Colecciones, seleccione una o varias colecciones y haga clic en Eliminar en la barra de herramientas.

1. En el cuadro de diálogo, haga clic en **[!UICONTROL Eliminar]** para confirmar la acción de eliminar.

   >[!NOTE]
   >
   >También puede eliminar colecciones inteligentes [eliminando las búsquedas](#saved-searches)guardadas.

## Descargar una colección {#downloading-a-collection}

Al descargar una colección, se descarga toda la jerarquía de recursos de la colección, incluidas las carpetas y las colecciones secundarias.

1. En la consola Colecciones, seleccione una o varias colecciones para descargar.
1. En la barra de herramientas, haga clic en **[!UICONTROL Descargar]**.
1. En el cuadro de diálogo **[!UICONTROL Descargar]** , haga clic en **[!UICONTROL Descargar]**. Si desea descargar las representaciones de los recursos de la colección, seleccione **[!UICONTROL Representaciones]**. Seleccione la opción **[!UICONTROL Correo electrónico]** para enviar una notificación por correo electrónico al propietario de la colección.

   Cuando selecciona una colección para descargar, se descarga la jerarquía completa de carpetas bajo la colección. Para incluir cada colección que descargue (incluidos los recursos de las colecciones secundarias anidadas en la colección principal) en una carpeta individual, seleccione **[!UICONTROL Crear una carpeta independiente para cada recurso]**.

## Crear colecciones anidadas {#creating-nested-collections}

Puede agregar una colección a otra colección, creando así una colección anidada.

1. En la consola Colecciones, seleccione la colección o el grupo de colecciones que desee y haga clic en **[!UICONTROL A colección]** en la barra de herramientas.

1. En la página **[!UICONTROL Añadir a colección]** , seleccione la colección en la que desea agregar la colección.

   >[!NOTE]
   >
   >La colección actualizada más recientemente se selecciona de forma predeterminada en la página **[!UICONTROL Añadir a colección]** .

1. Haga clic en **[!UICONTROL Agregar]**. Un mensaje confirma que la colección se agrega a la colección de destinatarios en la página **[!UICONTROL Seleccionar destino]** . Cierre el mensaje para completar el proceso.

>[!NOTE]
>
>Las colecciones inteligentes no se pueden anidar. En otras palabras, las colecciones inteligentes no pueden contener ninguna otra colección.

## Búsquedas guardadas {#saved-searches}

In the [!DNL Assets] user interface, you can search or filter assets based on certain rules, search criteria, or custom search facets. Si los guarda como **[!UICONTROL Búsquedas guardadas]**, puede acceder a ellos más adelante desde la lista **[!UICONTROL Búsquedas guardadas]** del panel Filtro. Al crear una búsqueda guardada también se crea una colección inteligente.

![saved_searches_lista](assets/saved_searches_list.png)

Las búsquedas guardadas se crean al crear una colección inteligente. Las colecciones inteligentes se agregan automáticamente a la lista **[!UICONTROL Búsquedas guardadas]**. The [!UICONTROL Saved Searches] query for the collection is saved in the `dam:query` property in CRXDE at the relative location `/content/dam/collections/`. No hay límites para las búsquedas que puede guardar ni para las búsquedas guardadas que se muestran en la lista.

>[!NOTE]
>
>Puede compartir colecciones inteligentes del mismo modo que comparte colecciones estáticas.

Editar búsquedas guardadas es lo mismo que editar colecciones inteligentes. Para obtener más información, consulte [Edición de una colección](#editing-a-smart-collection)inteligente.

Para eliminar las búsquedas guardadas, siga estos pasos:

1. En la interfaz de usuario, haga clic en la opción [!DNL Assets] de ![](assets/do-not-localize/search_icon.png)búsqueda.
1. Con el cursor en el campo Omniture search, presione la tecla Retorno.
1. En la [!DNL Experience Manager] interfaz, abra el panel Filtros.
1. From the **[!UICONTROL Saved Searches]** list, click **[!UICONTROL Delete]** next to the smart collection that you want to delete.

   ![select_smart_collection](assets/select_smart_collection.png)

1. En el cuadro de diálogo, haga clic en **[!UICONTROL Eliminar]** para eliminar la búsqueda guardada.

## Ejecución de un flujo de trabajo en una colección {#running-a-workflow-on-a-collection}

Puede ejecutar un flujo de trabajo para los recursos de una colección. Si la colección contiene colecciones anidadas, el flujo de trabajo también se ejecuta en los recursos de las colecciones anidadas. Sin embargo, si la colección y la colección anidada contienen recursos de duplicado, el flujo de trabajo solo se ejecuta una vez para dichos recursos.

1. Abra **[!UICONTROL Recursos]** > **[!UICONTROL Colecciones]**. Para ejecutar un flujo de trabajo en una colección específica, selecciónela.
1. Open **[!UICONTROL Timeline]** rail. Haga clic en ![Chevron hacia arriba](assets/do-not-localize/chevron-up-icon.png) y haga clic en Flujo de trabajo **[!UICONTROL de Inicio]**.
1. En la sección **[!UICONTROL Iniciar flujo de trabajo]**, seleccione un modelo de flujo de trabajo de la lista. Por ejemplo, seleccione el modelo **[!UICONTROL Recurso de actualización DAM]**.
1. Introduzca un título para el flujo de trabajo y haga clic en **[!UICONTROL Inicio]**.
1. In the dialog, click **[!UICONTROL Proceed]**. El flujo de trabajo procesa todos los recursos de la colección seleccionada.

>[!MORELIKETHIS]
>
>* [Configuración de las notificaciones por correo electrónico de Recursos Experience Manager](/help/sites-administering/notification.md#assetsconfig)
>* [Crear una tarea de revisión para colecciones](bulk-approval.md)

