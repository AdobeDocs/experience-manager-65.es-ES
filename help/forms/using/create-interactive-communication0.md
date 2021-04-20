---
title: '"Tutorial: Crear comunicación interactiva "'
seo-title: Crear una comunicación interactiva para la impresión y la Web
description: Crear una comunicación interactiva con todos los componentes básicos
seo-description: Crear una comunicación interactiva con todos los componentes básicos
uuid: 5ffaa86f-87c7-4673-8b41-63ec61421be2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ac5d8d4f-fc13-4e8d-819c-c5db07fa6870
docset: aem65
feature: Interactive Communication
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 0%

---


# Tutorial: Crear comunicación interactiva {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Este tutorial es un paso de la serie [Create your first Interactive Communication](/help/forms/using/create-your-first-interactive-communication.md) . Se recomienda seguir la serie en secuencia cronológica para comprender, realizar y demostrar el caso de uso completo del tutorial.

Una vez creados todos los componentes básicos, como el modelo de datos de formulario, los fragmentos de documento, las plantillas y los temas para la versión web, puede empezar a crear una comunicación interactiva.

Las comunicaciones interactivas se pueden entregar a través de dos canales: Imprimir y Web. También puede crear una comunicación interactiva con el canal de impresión como maestro. La opción Imprimir como principal para el canal web garantiza que el contenido, la herencia y el enlace de datos del canal web se deriven del canal de impresión. También garantiza que los cambios realizados en el canal Imprimir se sincronicen en el canal Web. Sin embargo, los autores de la comunicación interactiva pueden romper la herencia de componentes específicos del canal web.

Este tutorial lo acompaña durante los pasos para crear comunicaciones interactivas para los canales web e impresos. Al final de este tutorial, podrá:

* Crear comunicación interactiva para el canal de impresión
* Crear comunicación interactiva para el canal web
* Crear comunicaciones interactivas de impresión y web con Imprimir como maestro

## Crear comunicaciones interactivas para impresión y web sin sincronización {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### Crear comunicación interactiva para el canal de impresión {#create-interactive-communication-for-print-channel}

A continuación se muestra la lista de recursos que ya se han creado en este tutorial y que son necesarios al crear la comunicación interactiva para el canal de impresión:

**Imprimir plantilla:** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**Modelo de datos de formulario:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Fragmentos de documento:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_first_ic](../../forms/using/create-document-fragments.md)

**Fragmentos de diseño:** [table_lf](../../forms/using/create-templates-print-web.md)

**Imágenes:** PayNow y ValueAddedServices

1. Inicie sesión en la instancia de autor de AEM y vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Pulse **Crear** y seleccione **Comunicación interactiva**. Se muestra el asistente **Crear comunicación interactiva**.
1. Especifique **create_first_ic** en el **Título** y en el campo **Nombre**. Seleccione **FDM_Create_First_IC** como Modelo de datos de formulario y pulse **Siguiente**.
1. En el asistente **Channels**:

   1. Especifique **create_first_ic_print_template** como plantilla de impresión y pulse **Seleccionar**. Asegúrese de que la casilla de verificación **Usar impresión como maestro para canal web** no esté seleccionada.

   1. Especifique **Create_First_IC_templates** folder > **Create_First_IC_Web_Template** como plantilla web y pulse **Select**.

   1. Toque **Crear**.

   Se muestra un mensaje de confirmación de que la comunicación interactiva se ha creado correctamente.

1. Pulse **Editar** para abrir la comunicación interactiva en el panel derecho.
1. Vaya a la pestaña **Assets** y aplique el filtro para mostrar solo los fragmentos del documento en el panel izquierdo.
1. Arrastre y suelte los siguientes fragmentos de documento en sus áreas de destino en la Comunicación interactiva:

   | Fragmento de documento | Área de destino |
   |---|---|
   | bill_details_first_ic | Detalles de la factura |
   | customer_details_first_ic | Detalles del cliente |
   | bill_summary_first_ic | Resumen de facturación |
   | summary_charge_first_interactivo_communication | Cargos |

   ![Fragmentos de documento para comunicaciones interactivas](assets/create_first_ic_doc_fragments_new.png)

1. Pulse **Charts** área de destino y pulse **+** para añadir un componente **Chart**.
1. Pulse el componente Gráfico y seleccione ![configure_icon](assets/configure_icon.png) (Configurar). Las propiedades del gráfico se muestran en el panel izquierdo:

   1. Especifique un nombre para el gráfico.
   1. Seleccione **Pie** en la lista desplegable **Tipo de gráfico**.
   1. Seleccione la propiedad **calltype** del tipo de objeto del modelo de datos **calls** en la sección **X-axis**. Pulse ![done_icon](assets/done_icon.png).
   1. Seleccione **Frequency** en la lista desplegable **Function**.
   1. Seleccione la propiedad **calltype** del tipo de objeto del modelo de datos **calls** en la sección **Y-axis**. Pulse ![done_icon](assets/done_icon.png).
   1. Toque ![done_icon](assets/done_icon.png) para guardar las propiedades del gráfico.

1. Vaya a la pestaña **Assets** y aplique el filtro para mostrar solo los fragmentos de diseño en el panel izquierdo. Arrastre y suelte el fragmento de diseño **table_lf** en el área de destino **Llamadas desglosadas**.
1. Seleccione el campo de texto en la columna **Date** y pulse ![configure_icon](assets/configure_icon.png) (Configurar).
1. Seleccione **Objeto del modelo de datos** en la lista desplegable **Tipo de enlace** y seleccione **llamadas** > **fecha de llamada**. Toque ![done_icon](assets/done_icon.png) dos veces para guardar las propiedades.

   Del mismo modo, cree un enlace con **calltime**, **callnumber**, **callduration** y **callloads** para los campos de texto de los campos **Time**, **Number**, **Duración** y **Cargos** columnas respectivamente.

1. Pulse **PayNow** área de destino y pulse **+** para añadir un componente **Image**.
1. Pulse el componente Imagen y seleccione ![configure_icon](assets/configure_icon.png) (Configurar). Las propiedades de la imagen se muestran en el panel izquierdo:

   1. Especifique **PayNow** como nombre de la imagen en el campo **Name**.
   1. Pulse **Cargar**, seleccione la imagen guardada en el sistema de archivos local y pulse **Abrir**.
   1. Toque ![done_icon](assets/done_icon.png) para guardar las propiedades de la imagen.

1. Repita los pasos 13 y 14 para agregar la imagen **ValueAddedServices** al área de destino **ValueAddedServices**.

### Crear comunicación interactiva para el canal web {#create-interactive-communication-for-web-channel}

A continuación se muestra la lista de recursos que ya se han creado en este tutorial y que son necesarios al crear la comunicación interactiva para el canal web:

**Plantilla web:** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**Modelo de datos de formulario:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Fragmentos de documento:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_first_ic](../../forms/using/create-document-fragments.md)

**Imágenes:** PayNowWeb y ValueAddedServicesWeb

1. Inicie sesión en la instancia de autor de AEM y vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Pulse **Crear** y seleccione **Comunicación interactiva**. Se muestra el asistente **Crear comunicación interactiva**.
1. Especifique **create_first_ic** en el **Título** y en el campo **Nombre**. Seleccione **FDM_Create_First_IC** como Modelo de datos de formulario y pulse **Siguiente**.
1. En el asistente **Channels**:

   1. Especifique **create_first_ic_print_template** como plantilla de impresión y pulse **Seleccionar**. Asegúrese de que la casilla de verificación **Usar impresión como maestro para canal web** no esté seleccionada.

   1. Especifique **Create_First_IC_templates** folder > **Create_First_IC_Web_Template** como plantilla web y pulse **Select**.

   1. Toque **Crear**.

   Se muestra un mensaje de confirmación de que la comunicación interactiva se ha creado correctamente.

1. Pulse **Editar** para abrir la comunicación interactiva en el panel derecho.
1. Pulse la pestaña **Channels** del panel izquierdo y pulse **Web**.
1. Vaya a la pestaña **Assets** y aplique el filtro para mostrar solo los fragmentos del documento en el panel izquierdo.
1. Arrastre y suelte los siguientes fragmentos de documento en sus áreas de destino en la Comunicación interactiva:

   | Fragmento de documento | Área de destino |
   |---|---|
   | bill_details_first_ic | Detalles de la factura |
   | customer_details_first_ic | Detalles del cliente |
   | bill_summary_first_ic | Resumen de facturación |
   | summary_charge_first_interactivo_communication | Cargos |

1. Pulse **Resumen de cargos** y pulse **+** para añadir un componente **Chart**.
1. Pulse el componente Gráfico y seleccione ![configure_icon](assets/configure_icon.png) (Configurar). Las propiedades del gráfico se muestran en el panel izquierdo:

   1. Especifique un nombre para el gráfico.
   1. Seleccione **Pie** en la lista desplegable **Tipo de gráfico**.

   1. Seleccione la propiedad **calltype** del tipo de objeto del modelo de datos **calls** en la sección **X-axis**. Pulse ![done_icon](assets/done_icon.png).

   1. Seleccione **Frequency** en la lista desplegable **Function**.

   1. Seleccione la propiedad **calltype** del tipo de objeto del modelo de datos **calls** en la sección **Y-axis**. Pulse ![done_icon](assets/done_icon.png).

   1. Toque ![done_icon](assets/done_icon.png) para guardar las propiedades del gráfico.

1. Seleccione la pestaña **Fuentes de datos** en el panel izquierdo y arrastre y suelte el objeto del modelo de datos **llamadas** en el área de destino **Llamadas desglosadas**. Todas las propiedades del objeto del modelo de datos **Calls** se muestran como columnas de tabla en el área de destino **Llamadas desglosadas** del panel derecho.

   En función del caso de uso, se requieren las columnas Fecha de llamada, Hora de llamada, Número de llamada, Duración de llamada y Cargos de llamada en la tabla.

   ![Tabla de comunicación interactiva](assets/table_ic_web_new.png)

1. Seleccione **Mobilenum** encabezado de columna de tabla y seleccione **Más opciones** > **Eliminar columna**. Del mismo modo, elimine la columna **Calltype**.
1. Seleccione el encabezado de columna de la tabla **Calldate** y pulse ![edit](assets/edit.png) (Editar) para cambiar el nombre del texto a **Fecha de llamada**. Del mismo modo, cambie el nombre de otros encabezados de columna de la tabla.
1. En función del caso de uso, inserte un botón **Pagar ahora** en la Comunicación interactiva que proporcione al usuario una opción para realizar el pago haciendo clic en el botón. Siga estos pasos para insertar el botón :

   1. Pulse **Pagar ahora** área de destino y pulse **+** para añadir un componente **Texto**.

   1. Pulse el componente de texto y pulse ![editar](assets/edit.png) (Editar).
   1. Cambie el nombre del texto a **Pagar ahora**.
   1. Seleccione el texto y pulse el icono Hipervínculo .
   1. Especifique la URL de pago en el campo **Path**.
   1. Seleccione **Nueva pestaña** en la lista desplegable **Objetivo**.

   1. Toque ![done_icon](assets/done_icon.png) para guardar las propiedades del hipervínculo.

1. Seleccione **Estilo** en la lista desplegable junto a la opción **Vista previa**.

   ![Seleccione el modo Estilo para la comunicación interactiva](assets/select_style_ic_web_new.png)

1. Defina un estilo para el texto del hipervínculo para mostrarlo como un botón en la Comunicación interactiva siguiendo los pasos siguientes:

   1. Pulse el componente de texto y seleccione ![editar](assets/edit.png) (Editar).
   1. En la sección **Borde**, especifique **1,5px** como **Ancho del borde**, seleccione **Sólido** como **Estilo del borde** y especifique **46px** como **2/>Radio del borde**.

   1. Seleccione Rojo como color de fondo para el botón en la sección **Fondo**.
   1. En el campo **Margen** de la sección **Dimension y posición**, pulse el icono **Editar simultáneamente** y establezca el margen **Derecho** como **450px**. Los campos Superior, Inferior e Izquierda se definen como en blanco.

   ![Insertar hipervínculo en comunicación interactiva](assets/ic_web_hyperlink_new.png)

1. Pulse **Pagar ahora** área de destino y pulse **+** para añadir un componente **Imagen**.
1. Pulse el componente Imagen y seleccione ![configure_icon](assets/configure_icon.png) (Configurar). Las propiedades de la imagen se muestran en el panel izquierdo:

   1. Especifique **PayNow** como nombre de la imagen en el campo **Name**.

   1. Toque **Upload**, seleccione la imagen **PayNowWeb** guardada en el sistema de archivos local y pulse **Abrir**.

   1. Toque ![done_icon](assets/done_icon.png) para guardar las propiedades de la imagen.

1. En función del caso de uso, inserte un botón **Subscribe** en la Comunicación interactiva que proporcione al usuario una opción para suscribirse a los servicios de valor agregado haciendo clic en el botón .

   Repita los pasos 13-17 para agregar un botón **Suscribirse** al área de destino **Servicios de valor agregado** y añada la imagen **ValueAddedServicesWeb**.

## Crear comunicaciones interactivas para impresión y web con sincronización automática {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

También puede crear una comunicación interactiva habilitando la sincronización automática entre los canales Imprimir y Web. Para habilitar la sincronización automática, seleccione la opción Imprimir como maestro al crear la comunicación interactiva. Al seleccionar la opción Imprimir como formato, se garantiza que el contenido, la herencia y el enlace de datos del canal web se deriven del canal Imprimir. También garantiza que los cambios realizados en el canal Imprimir se reflejen en el canal Web.

Siga estos pasos para derivar el contenido del canal web mediante el canal de impresión:

1. Inicie sesión en la instancia de autor de AEM y vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Pulse **Crear** y seleccione **Comunicación interactiva**. Se muestra el asistente **Crear comunicación interactiva**.
1. Especifique **create_first_ic** en el **Título** y en el campo **Nombre**. Seleccione **FDM_Create_First_IC** como Modelo de datos de formulario y pulse **Siguiente**.
1. En el asistente **Channels**:

   1. Especifique **create_first_ic_print_template** como plantilla de impresión y pulse **Seleccionar**.

   1. Active la casilla **Usar Imprimir como maestro para el canal web**.
   1. Especifique **Create_First_IC_templates** folder > **Create_First_IC_Web_Template** como plantilla web y pulse **Select**.

   1. Toque **Crear**.

   Se muestra un mensaje de confirmación de que la comunicación interactiva se ha creado correctamente.

1. Pulse **Editar** para abrir la comunicación interactiva en el panel derecho.
1. Ejecute los pasos 6 a 15 de la sección [Crear comunicación interactiva para el canal de impresión](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel).
1. Pulse la pestaña **Channels** del panel izquierdo y pulse **Web** para generar automáticamente contenido para el canal web desde el canal de impresión.
1. Como la casilla **Use Print as Master for Web Channel** está seleccionada en el paso 4, el contenido y los enlaces se generan automáticamente para el canal Web desde el canal Print.

   El contenido del canal de impresión se inserta debajo del contenido de la plantilla de canal web. Para modificar el contenido del canal web que se ha generado automáticamente desde el canal de impresión, puede cancelar la herencia de cualquier área de destino.

   Pase el ratón sobre el área de destino relevante en el canal web y seleccione ![cancelar herencia](assets/cancelinheritance.png) (Cancelar herencia) y, a continuación, en el cuadro de diálogo **Cancelar herencia**, pulse **Sí**.

   ![Cancelar herencia](assets/cancel_inheritance_web_channel_new.png)

   Si ha cancelado la herencia de un componente, puede volver a activarlo. Para volver a habilitar la herencia, pase el ratón sobre el límite del área de destino correspondiente, que incluye el componente, y pulse ![volver a habilitar herencia](assets/reenableinheritance.png).

1. Seleccione la pestaña **Content** en el panel izquierdo.
1. Arrastre y suelte el contenido del canal web generado automáticamente en los paneles existentes de la plantilla web mediante el árbol de contenido. A continuación se muestra la lista de componentes que deben reorganizarse:

   * Componente Detalles de la factura al panel Detalles de la factura
   * Componente Detalles del cliente al panel Detalles del cliente
   * Componente Resumen de facturación al panel Resumen de facturación
   * Componente Resumen de Cargos al panel Resumen de Cargos
   * Fragmento de diseño (tabla) al panel Llamadas desglosadas

   ![Árbol de contenido web](assets/ic_web_content_tree_new.png)

1. Repita los pasos 13-18 de [Crear comunicación interactiva para el canal web](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) para insertar los hipervínculos **Pay Now** y **Subscribe** en el canal web de la comunicación interactiva.

