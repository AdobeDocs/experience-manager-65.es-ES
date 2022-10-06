---
title: Utilice el modo Diseño para cambiar el tamaño de los componentes de los formularios adaptables
description: Defina la posición de los componentes mediante la cuadrícula adaptable disponible en el modo Diseño
feature: Adaptive Forms
exl-id: 5cf76cb1-c92c-4aed-9945-37494fef2d29
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 73%

---

# Usar el modo Diseño para cambiar el tamaño de los componentes {#use-layout-mode-to-resize-components}

La interfaz de creación de formularios adaptables permite cambiar el tamaño de los componentes mediante el modo Diseño . Arrastre y suelte los puntos azules dentro de las columnas para definir los puntos iniciales y finales en los componentes de posición. Aparecen puntos azules tras pulsar el componente en la cuadrícula adaptable. La cuadrícula adaptable consta de 12 columnas iguales. El sombreado de color blanco y azul en las columnas alternativas diferencia una columna de la otra.

Puede utilizar el modo Diseño para cambiar el tamaño de los componentes de todos los tipos de dispositivos, como escritorio, tableta, teléfono y otros dispositivos más pequeños. La tableta deriva automáticamente la configuración del diseño de la versión de escritorio y los dispositivos más pequeños derivan la configuración del diseño del teléfono. Con todo, puede anular las configuraciones derivadas automáticamente para definir una configuración diferente para cada tipo de dispositivo.

## Acceder al modo Diseño {#access-layout-mode}

Select **Diseño** en la lista desplegable que aparece en la parte superior de la interfaz de creación de formularios adaptables junto a la **Vista previa** . El formulario se muestra en el modo Diseño.

1. Inicie sesión en la instancia de autor de AEM y vaya a **Adobe Experience Manager** > **Forms** > **Forms y documentos**.
1. Crear una nueva o abrir una [formulario adaptable](../../forms/using/creating-adaptive-form.md).
1. Seleccione **Diseño** en la lista desplegable que aparece en la parte superior junto a la opción **Vista previa**. El formulario se muestra en el modo Diseño.

   ![Modo Diseño](assets/layout_mode_ic_new.png)

## Cambiar el tamaño de los componentes {#resize-components}

1. En el modo Diseño, pulse en el componente para cambiar su tamaño. Los puntos azules se muestran al principio y al final de la cuadrícula adaptable.
1. Arrastre y suelte los puntos azules para definir la posición del componente en la cuadrícula adaptable.

   ![Cambiar el tamaño mediante el modo Diseño](assets/layout_mode_resize_new_updated1.png)

   La barra de herramientas que se muestra después de pulsar los componentes consta de las siguientes opciones:

   * **[!UICONTROL Principal]**: Seleccione el elemento principal de un componente.
   * **[!UICONTROL Revertir diseño de punto de interrupción]**: Deshacer todos los cambios de tamaño y aplicar el diseño predeterminado al componente.
   * **[!UICONTROL Flotar a una línea nueva]**: Mover el componente a la línea siguiente si hay varios componentes dentro de la misma línea.

   También puede usar la opción **[!UICONTROL Revertir diseño de punto de interrupción]** (![Revertir punto de interrupción](assets/reverttopreviouslypublishedversion.png)) en el nivel de panel para deshacer todos los cambios de tamaño.

   >[!NOTE]
   >
   >No puede cambiar el tamaño de los componentes de la columna de tabla, barra de herramientas, botón de barra de herramientas y área de destino con el modo Diseño. Utilice el modo Estilo para cambiar el tamaño de estos componentes.

### Ejemplo {#example}

**Objetivo:** Desea insertar un componente de tabla y un componente de imagen y colocarlos en paralelo entre sí en un formulario adaptable.

1. Inserte los componentes de tabla e imagen mediante el modo de edición en el formulario adaptable. El componente de imagen se muestra después del componente de tabla.
1. Cambie al modo Diseño y pulse el componente Tabla. Los puntos azules para cambiar el tamaño del componente se muestran en las columnas 1 y 12.
1. Arrastre y suelte el punto azul en la columna 12 a la columna 6 de la cuadrícula interactiva.

   ![Definir el punto final de la tabla](assets/layout_mode_end_point_table_new.png)

1. Del mismo modo, seleccione el componente Imagen y arrastre y suelte el punto azul en la columna 1 a la columna 7 de la cuadrícula interactiva. Los componentes de tabla e imagen se muestran paralelos entre sí.

   ![Tabla e imagen en paralelo en el modo Diseño](assets/table_image_parallel_new.png)

   Puede seleccionar el componente Imagen y pulsar la opción **Flotar a una línea nueva**, disponible en la barra de herramientas para cambiar el componente Imagen a la línea siguiente.

## Cambiar el tamaño de los paneles {#resize-panels-layout-mode}

Ejecute los siguientes pasos si desea cambiar el tamaño de todo el panel en lugar de componentes individuales:

1. Pulse cualquiera de los componentes del panel cuyo tamaño desee cambiar, elija ![Seleccionar principal](assets/select_parent_icon.svg) y seleccione la primera opción de la lista desplegable, si el panel es el elemento principal inmediato del componente.

   Los puntos azules se muestran al principio y al final de la cuadrícula adaptable.

1. Arrastre y suelte los puntos azules para definir la posición del panel en la cuadrícula adaptable. Puede repetir los pasos 1 y 2 y seleccionar ![Seleccionar principal](assets/float_to_new_line_icon.svg) para desplazar el panel cuyo tamaño se ha cambiado a la línea siguiente.

## Definición del diseño de varias columnas para un panel

Ejecute los siguientes pasos para definir el número de columnas para un panel:

1. En el modo **[!UICONTROL Editar]**, pulse el panel, seleccione ![Configurar](assets/configure_icon.png) luego la opción **[!UICONTROL Adaptable: Todo lo que hay en la página sin navegación]** de la lista desplegable **[!UICONTROL Diseño del panel]**.

1. Pulse ![Guardar](assets/save_icon.svg) para guardar las propiedades.

1. En el modo **[!UICONTROL Diseño]**, pulse cualquiera de los componentes del panel y elija ![Seleccionar principal](assets/select_parent_icon.svg) y seleccione el panel.

1. Pulse ![varias columnas](assets/multi-column.svg) y seleccione el número de columnas de la lista desplegable. El número de columnas puede oscilar entre 1 y 12. El panel se divide en un diseño de varias columnas.

![varias columnas en el modo Diseño](assets/multi-column-layout.png)

## Habilitar la nueva cuadrícula adaptable para los diseños adaptables antiguos {#enableresponsivegrid}

Active la nueva cuadrícula adaptable para los formularios creados con AEM Forms 6.4 o una versión anterior para cambiar el tamaño de los componentes.

>[!NOTE]
>
>Al cambiar a la nueva cuadrícula adaptable, se descartarán las propiedades de diseño ya definidas para los componentes utilizados en el formulario.

Realice los siguientes pasos para habilitar la nueva cuadrícula adaptable:

1. Seleccione **Diseño** en la lista desplegable que aparece en la parte superior junto a la opción **Vista previa**. Aparece una confirmación para habilitar el modo Diseño.
1. Pulse **Sí** para habilitar el modo **Diseño** para el formulario.

### Incrustar un fragmento antiguo en un formulario adaptable con una nueva presentación adaptable {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

El nuevo diseño adaptable para el formulario adaptable le permite agregar un fragmento de formulario adaptable con el antiguo diseño adaptable al formulario. Con todo, el nuevo diseño descarta las propiedades de diseño ya definidas para los componentes utilizados en el fragmento. Puede cambiar al modo Diseño para definir las propiedades de diseño de los componentes utilizados en el fragmento.

### Incrustar un fragmento con un nuevo diseño interactivo en un antiguo formulario adaptable {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

Si incrusta un fragmento con la nueva presentación adaptable en un formulario adaptable con una presentación interactiva antigua, el sistema le indicará que active el modo Diseño para el formulario y vuelva a incrustar el fragmento.

Para habilitar el modo Diseño, seleccione **Diseño** en la lista desplegable que aparece en la parte superior junto a la opción **Vista previa** y pulse **Sí** para confirmar. Seleccione el modo **Editar** para volver a integrar el fragmento.

## Desactivar el modo Diseño para formularios con un diseño adaptable antiguo {#disable-layout-mode-for-forms-with-old-responsive-layout}

Puede desactivar el modo Diseño para formularios con un diseño adaptable antiguo editando las propiedades de la plantilla utilizada en el formulario.

Siga estos pasos para desactivar el modo Diseño:

1. Seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL Plantillas]** y abra la plantilla utilizada en el formulario en el modo **[!UICONTROL Editar]**.
1. Seleccione el contenedor de documentos en el panel izquierdo y pulse **[!UICONTROL Política.]**

   ![Desactivar el modo Diseño](assets/policy_disable_layout_mode.png)

1. Pulse la pestaña **[!UICONTROL Configuración de diseño]** y seleccione **[!UICONTROL Desactivar el modo Diseño]**.
1. Pulse ![Guardar cambios](assets/save_icon.png) para guardar las propiedades de la plantilla.
