---
title: Administrar varios recursos y colecciones
description: Descubra cómo editar los metadatos de varios recursos y colecciones simultáneamente para propagar rápidamente los cambios comunes de metadatos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9af0ee0ff9d1089b6cf09c52f7f606cce6775d72

---


# Gestión de recursos y colecciones {#managing-multiple-assets-and-collections}

Recursos Adobe Enterprise Manager (AEM) permite editar simultáneamente los metadatos de varios recursos para que pueda propagar rápidamente cambios comunes de metadatos a los recursos de forma masiva. También puede editar los metadatos de varias colecciones de forma masiva.

Utilice la página de propiedades para realizar cambios en los metadatos de varios recursos o colecciones:

* Cambiar las propiedades de metadatos a un valor común
* Agregar o modificar etiquetas

Para personalizar la página de propiedades de metadatos, incluida la adición, modificación y eliminación de propiedades de metadatos, utilice el editor de esquemas.

>[!NOTE]
>
>Los métodos de edición masiva funcionan para los recursos disponibles en una carpeta o una colección. En el caso de los recursos disponibles en varias carpetas o que cumplen un criterio común, es posible actualizar [masivamente los metadatos después de realizar la búsqueda](search-assets.md#metadataupdates).

## Editar propiedades de metadatos de varios recursos {#editing-metadata-properties-of-multiple-assets}

1. En la interfaz de usuario de Recursos, navegue a la ubicación de los recursos que desee editar.
1. Seleccione los recursos para los que desea editar propiedades comunes.
1. En la barra de herramientas, toque o haga clic en el icono **[!UICONTROL Propiedades]** para abrir la página de propiedades de los recursos seleccionados.

   >[!NOTE]
   >
   >Cuando se seleccionan varios recursos, se selecciona el formulario principal común más bajo para los recursos. En otras palabras, la página de propiedades solo muestra los campos de metadatos comunes en las páginas de propiedades de todos los recursos individuales.

1. Modifique las propiedades de metadatos de los recursos seleccionados en las distintas fichas.
1. Para ver el editor de metadatos de un recurso específico, anule la selección de los recursos restantes de la lista. Los campos del editor de metadatos se rellenan con los metadatos del recurso concreto.

   >[!NOTE]
   >
   >* En la página de propiedades, puede quitar recursos de la lista de recursos desactivándolos. La lista de recursos tiene todos los recursos seleccionados de forma predeterminada. Los metadatos de los recursos que se eliminan de la lista no se actualizan.
   >* En la parte superior de la lista de recursos, active la casilla de verificación situada cerca de **[!UICONTROL Título]** para alternar entre seleccionar los recursos y borrar la lista.


1. Para seleccionar un esquema de metadatos diferente para los recursos, toque o haga clic en el icono **[!UICONTROL Configuración]** de la barra de herramientas y seleccione el esquema deseado.
1. Guarde los cambios.
1. Para anexar los nuevos metadatos con los metadatos existentes en los campos que contienen varios valores, seleccione el **[!UICONTROL modo Anexar]**. Si no selecciona esta opción, los metadatos nuevos sustituirán a los metadatos existentes en los campos. Pulse o haga clic en **[!UICONTROL Enviar]**.

   >[!CAUTION]
   >
   >En el caso de los campos de un solo valor, los nuevos metadatos no se anexan al valor existente en el campo aunque seleccione el modo **[!UICONTROL Anexar]**.

## Configurar límite para la actualización masiva de metadatos {#configlimit}

Para evitar situaciones similares a las de DOS, AEM limita el número de parámetros admitidos en una solicitud de Sling. Al actualizar los metadatos de muchos recursos de una sola vez, es posible que se alcance el límite y que los metadatos no se actualicen para más recursos. AEM genera la siguiente advertencia en los registros:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Para cambiar el límite, acceda a la consola web ( **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**) y cambie el valor de **[!UICONTROL Máximo de parámetros POST]** en la configuración OSGi de la **[!UICONTROL administración de parámetros de solicitud Apache Sling]**.

>[!MORELIKETHIS]
>
>* [Editar propiedades de metadatos de varias colecciones](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)

