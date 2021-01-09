---
title: Uso del modo Diseño para cambiar el tamaño de los componentes en formularios adaptables
description: 'Definir la posición de los componentes mediante la cuadrícula adaptable disponible en el modo Diseño '
translation-type: tm+mt
source-git-commit: 923c31bf67c7ad480ef3c3a1e312b4bd841bac6d
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 0%

---


# Utilice el modo Diseño para cambiar el tamaño de los componentes {#use-layout-mode-to-resize-components}

La interfaz de creación de formularios adaptables permite cambiar el tamaño de los componentes mediante el modo Diseño. Arrastre y suelte puntos azules dentro de las columnas para definir el inicio y los puntos finales para colocar los componentes. Los puntos azules se muestran después de tocar el componente dentro de la cuadrícula adaptable. La cuadrícula adaptable consta de 12 columnas iguales. El sombreado de color blanco y azul en las columnas alternativas diferencia una columna de la otra.

Puede utilizar el modo Diseño para cambiar el tamaño de los componentes de todos los tipos de dispositivos, como el escritorio, la tablet, el teléfono y otros dispositivos más pequeños. La tablet deriva automáticamente la configuración de diseño de la versión de escritorio y los dispositivos más pequeños obtienen la configuración de diseño del teléfono. Sin embargo, puede anular las configuraciones derivadas automáticamente para definir una configuración diferente para cada tipo de dispositivo.

## Modo Diseño de acceso {#access-layout-mode}

Seleccione **Presentación** en la lista desplegable que aparece en la parte superior de la interfaz de creación de formularios adaptables junto a la opción **Previsualización**. El formulario se muestra en el modo Presentación.

1. Inicie sesión en la instancia de creación de AEM y vaya a **Adobe Experience Manager** > **Forms** > **Forms &amp; Documentos**.
1. Cree un formulario adaptable nuevo o abra uno existente [](../../forms/using/creating-adaptive-form.md).
1. Seleccione **Diseño** en la lista desplegable que aparece en la parte superior junto a la opción **Previsualización**. El formulario se muestra en el modo Presentación.

   ![Modo de diseño](assets/layout_mode_ic_new.png)

## Cambiar el tamaño de los componentes {#resize-components}

1. En el modo Diseño, toque el componente para cambiar el tamaño. Los puntos azules se muestran en el inicio y al final de la cuadrícula adaptable.
1. Arrastre y suelte los puntos azules para definir la posición del componente en la cuadrícula interactiva.

   ![Cambio de tamaño mediante el modo Diseño](assets/layout_mode_resize_new_updated1.png)

   La barra de herramientas que se muestra después de tocar componentes consta de las siguientes opciones:

   * **[!UICONTROL Principal]**: Seleccione el elemento principal de un componente.
   * **[!UICONTROL Revertir diseño]** de punto de interrupción: Deshace todos los cambios de tamaño y aplica el diseño predeterminado al componente.
   * **[!UICONTROL Flotar a nueva línea]**: Mueva el componente a la línea siguiente si hay varios componentes dentro de la misma línea.

   También puede utilizar la opción **[!UICONTROL Revertir diseño de punto de interrupción]** ( ![Revertir punto de interrupción](assets/reverttopreviouslypublishedversion.png)) en el nivel de panel para deshacer todos los cambios de tamaño.

   >[!NOTE]
   >
   >No se puede cambiar el tamaño de los componentes de columna de tabla, barra de herramientas, botón de barra de herramientas y área de destinatario mediante el modo Diseño. Utilice el modo Estilo para cambiar el tamaño de estos componentes.

### Ejemplo {#example}

**Objetivo:** desea insertar un componente de tabla y un componente Imagen y colocarlos en paralelo en un formulario adaptable.

1. Inserte los componentes de tabla e imagen mediante el modo de edición en el formulario adaptable. El componente de imagen se muestra después del componente de tabla.
1. Cambie al modo Diseño y toque el componente Tabla. Los puntos azules para cambiar el tamaño del componente se muestran en las columnas 1 y 12.
1. Arrastre y suelte el punto azul de la columna 12 a la columna 6 de la cuadrícula adaptable.

   ![Definir el punto final de la tabla](assets/layout_mode_end_point_table_new.png)

1. Del mismo modo, seleccione el componente Imagen y arrastre y suelte el punto azul en la columna 1 a la columna 7 de la cuadrícula adaptable. Los componentes de tabla e imagen se muestran en paralelo.

   ![Tabla e imagen en paralelo en el modo Diseño](assets/table_image_parallel_new.png)

   Puede seleccionar el componente Imagen y tocar la opción **Flotar a nueva línea** disponible en la barra de herramientas para cambiar el componente Imagen a la siguiente línea.

## Cambiar el tamaño de los paneles {#resize-panels-layout-mode}

Realice los siguientes pasos si desea cambiar el tamaño del panel completo en lugar de componentes individuales:

1. Toque cualquiera de los componentes del panel cuyo tamaño desee cambiar, seleccione ![Seleccionar principal](assets/select_parent_icon.svg) y seleccione la primera opción en la lista desplegable, si el panel es el elemento principal inmediato del componente.

   Los puntos azules se muestran en el inicio y al final de la cuadrícula adaptable.

1. Arrastre y suelte los puntos azules para definir la posición del panel en la cuadrícula interactiva.
Puede repetir los pasos 1 y 2 y seleccionar ![Seleccionar principal](assets/float_to_new_line_icon.svg) para cambiar el panel cuyo tamaño ha cambiado a la línea siguiente.

## Definición del diseño de varias columnas para un panel

Siga los pasos siguientes para definir el número de columnas de un panel:

1. En el modo **[!UICONTROL Editar]**, toque el panel, seleccione ![Configurar](assets/configure_icon.png) y seleccione la opción **[!UICONTROL Responder - todo en la página sin navegación]** en la lista desplegable **[!UICONTROL Diseño del panel]**.

1. Toque ![Guardar](assets/save_icon.svg) para guardar las propiedades.

1. En el modo **[!UICONTROL Presentación]**, toque cualquiera de los componentes del panel, seleccione ![Seleccionar principal](assets/select_parent_icon.svg) y seleccione el panel.

1. Toque ![varias columnas](assets/multi-column.svg) y seleccione el número de columnas en la lista desplegable. El número de columnas puede oscilar entre 1 y 12. El panel se divide en un diseño de varias columnas.

![varias columnas en modo de diseño](assets/multi-column-layout.png)

## Habilitar la nueva cuadrícula adaptable para los diseños interactivos antiguos {#enableresponsivegrid}

Active la nueva cuadrícula adaptable para los formularios que cree con AEM Forms 6.4 o una versión inferior para cambiar el tamaño de los componentes.

>[!NOTE]
>
>Al cambiar a la nueva cuadrícula adaptable se descartan las propiedades de diseño ya definidas para los componentes utilizados en el formulario.

Realice los siguientes pasos para habilitar la nueva cuadrícula adaptable:

1. Seleccione **Diseño** en la lista desplegable que aparece en la parte superior junto a la opción **Previsualización**. Aparece una confirmación para habilitar el modo Diseño.
1. Toque **Sí** para habilitar el modo **Diseño** para el formulario.

### Incrustar un fragmento antiguo en un formulario adaptable con una nueva presentación adaptable {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

La nueva presentación adaptable para formularios adaptables permite agregar un fragmento de formulario adaptable con la presentación adaptable anterior al formulario. Sin embargo, el nuevo diseño descarta las propiedades de diseño ya definidas para los componentes utilizados en el fragmento. Puede cambiar al modo Diseño para definir las propiedades de diseño de los componentes utilizados en el fragmento.

### Incrustar un fragmento con una nueva presentación adaptable en un antiguo formulario adaptable {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

Si incrusta un fragmento con la nueva presentación adaptable en un formulario adaptable con una presentación adaptable antigua, el sistema le pedirá que habilite el modo Diseño para el formulario y vuelva a incrustar el fragmento.

Para habilitar el modo Diseño, seleccione **Diseño** en la lista desplegable que aparece en la parte superior junto a la opción **Previsualización** y toque **Sí** para confirmar. Seleccione el modo **Editar** para volver a incrustar el fragmento.

## Deshabilitar el modo Diseño para formularios con presentación adaptable anterior {#disable-layout-mode-for-forms-with-old-responsive-layout}

Puede desactivar el modo Presentación para formularios con presentación adaptable antigua editando las propiedades de la plantilla utilizada en el formulario.

Realice los siguientes pasos para desactivar el modo Diseño:

1. Seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL Plantillas]** y abra la plantilla utilizada en el formulario en el modo **[!UICONTROL Editar]**.
1. Seleccione el Contenedor de Documento en el panel izquierdo y toque **[!UICONTROL Directiva.]**

   ![Deshabilitar modo Diseño](assets/policy_disable_layout_mode.png)

1. Toque la ficha **[!UICONTROL Configuración de diseño]** y seleccione **[!UICONTROL Deshabilitar modo de diseño]**.
1. Toque ![Guardar cambios](assets/save_icon.png) para guardar las propiedades de la plantilla.

