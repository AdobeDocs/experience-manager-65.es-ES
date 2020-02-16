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
translation-type: tm+mt
source-git-commit: 56f7db792b340ed6774c54170e9b5d2a52153cd5

---


# Tutorial: Crear comunicación interactiva {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Este tutorial es un paso en la [serie Crear una primera comunicación](/help/forms/using/create-your-first-interactive-communication.md) interactiva. Se recomienda seguir la serie en secuencia cronológica para comprender, realizar y demostrar el caso de uso completo del tutorial.

Una vez creados todos los componentes básicos, como el modelo de datos de formulario, los fragmentos de documento, las plantillas y los temas para la versión web, puede empezar a crear una comunicación interactiva.

Interactive Communications puede entregarse a través de dos canales: Imprimir y Web. También puede crear una comunicación interactiva con el canal de impresión como maestro. La opción Imprimir como principal para el canal Web garantiza que el contenido, la herencia y el enlace de datos del canal Web se deriven del canal Imprimir. También garantiza que los cambios realizados en el canal Imprimir se sincronizan en el canal Web. Sin embargo, los autores de Comunicación interactiva pueden romper la herencia de componentes específicos en el canal Web.

Este tutorial le guiará por los pasos para crear comunicaciones interactivas para los canales de impresión y Web. Al final de este tutorial, podrá:

* Crear comunicación interactiva para el canal de impresión
* Crear comunicación interactiva para el canal Web
* Crear comunicaciones interactivas de impresión y Web con impresión como imagen principal

## Crear comunicaciones interactivas para impresión y Web sin sincronización {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### Crear comunicación interactiva para el canal de impresión {#create-interactive-communication-for-print-channel}

A continuación se muestra la lista de recursos que ya se han creado en este tutorial y que son necesarios al crear la comunicación interactiva para el canal de impresión:

**** Imprimir plantilla: [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**** Modelo de datos de formulario: [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**** Fragmentos de documento: [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_loads_first_ic](../../forms/using/create-document-fragments.md)

**** Fragmentos de diseño: [table_lf](../../forms/using/create-templates-print-web.md)

**** Imágenes: PayNow y ValueAddedServices

1. Inicie sesión en la instancia de creación de AEM y vaya a **Adobe Experience Manager** > **Formularios** > **Formularios y documentos**.
1. Toque **Crear** y seleccione Comunicación **** interactiva. Se muestra el asistente **Crear comunicación** interactiva.
1. Especifique **create_first_ic** en el campo **Título** y **Nombre** . Seleccione **FDM_Create_First_IC** como modelo de datos de formulario y toque **Siguiente**.
1. En el asistente **Canales** :

   1. Especifique **create_first_ic_print_template** como plantilla de impresión y toque **Seleccionar**. Asegúrese de que la casilla de verificación **Usar impresión como principal para canal** web no está seleccionada.

   1. Especifique la carpeta **Create_First_IC_templates** > **Create_First_IC_Web_Template** como plantilla Web y toque **Seleccionar**.

   1. Toque **Crear**.
   Se muestra un mensaje de confirmación de que la comunicación interactiva se ha creado correctamente.

1. Toque **Editar** para abrir la comunicación interactiva en el panel derecho.
1. Vaya a la ficha **Recursos** y aplique el filtro para mostrar solo los fragmentos de documento en el panel izquierdo.
1. Arrastre y suelte los siguientes fragmentos de documento en sus áreas de destino en la Comunicación interactiva:

   | Fragmento de documento | Área de destino |
   |---|---|
   | bill_details_first_ic | Detalles de la factura |
   | customer_details_first_ic | Detalles del cliente |
   | bill_summary_first_ic | Resumen de factura |
   | summary_loads_first_interactive_Communication | Cargos |

   ![Fragmentos de documento para comunicaciones interactivas](assets/create_first_ic_doc_fragments_new.png)

1. Toque **Gráficos** en el área de destino y toque **+** para agregar un componente **Gráfico** .
1. Puntee en el componente Gráfico y seleccione ![](assets/configure_icon.png) (Configurar). Las propiedades del gráfico se muestran en el panel izquierdo:

   1. Especifique un nombre para el gráfico.
   1. Seleccione **Circular** en la lista desplegable Tipo **de** gráfico.
   1. Seleccione la propiedad **calltype** del tipo de objeto del modelo de datos de **llamadas** en la sección del eje **** X. Tocar ![](assets/done_icon.png).
   1. Seleccione **Frecuencia** en la lista desplegable **Función** .
   1. Seleccione la propiedad **calltype** del tipo de objeto del modelo de datos de **llamadas** en la sección eje **** Y. Tocar ![](assets/done_icon.png).
   1. Toque ![](assets/done_icon.png) para guardar las propiedades del gráfico.

1. Vaya a la ficha **Recursos** y aplique el filtro para mostrar solo los fragmentos de diseño en el panel izquierdo. Arrastre y suelte el fragmento de diseño **table_lf** en el área de destino **Llamadas** por elemento.
1. Seleccione el Campo de texto en la columna **Fecha** y toque ![](assets/configure_icon.png) (Configurar).
1. Seleccione Objeto **** del modelo de datos en la lista desplegable Tipo **de** enlace y seleccione **llamadas** > **fecha** de llamada. Toque ![](assets/done_icon.png) dos veces para guardar las propiedades.

   Del mismo modo, cree enlaces con **llamada**, **número** de llamada, duración **de** llamada y **cargas** de llamada para los campos de texto en las columnas **Tiempo************** , Número, Duracióny Gastos.

1. Toque **Pagar ahora** el área de destino y toque **+** para agregar un componente **Imagen** .
1. Puntee en el componente Imagen y seleccione ![](assets/configure_icon.png) (Configurar). Las propiedades de imagen se muestran en el panel izquierdo:

   1. Especifique **PayNow** como nombre de la imagen en el campo **Nombre** .
   1. Toque **Cargar**, seleccione la imagen guardada en el sistema de archivos local y toque **Abrir**.
   1. Toque ![](assets/done_icon.png) para guardar las propiedades de la imagen.

1. Repita los pasos 13 y 14 para agregar la imagen **ValueAddedServices** al área de destino **ValueAddedServices** .

### Create Interactive Communication for Web channel {#create-interactive-communication-for-web-channel}

A continuación se muestra la lista de recursos que ya se han creado en este tutorial y que son necesarios al crear la comunicación interactiva para el canal Web:

**** Plantilla web: [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**** Modelo de datos de formulario: [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**** Fragmentos de documento: [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_loads_first_ic](../../forms/using/create-document-fragments.md)

**** Imágenes: PayNowWeb y ValueAddedServicesWeb

1. Inicie sesión en la instancia de creación de AEM y vaya a **Adobe Experience Manager** > **Formularios** > **Formularios y documentos**.
1. Toque **Crear** y seleccione Comunicación **** interactiva. Se muestra el asistente **Crear comunicación** interactiva.
1. Especifique **create_first_ic** en el campo **Título** y **Nombre** . Seleccione **FDM_Create_First_IC** como modelo de datos de formulario y toque **Siguiente**.
1. En el asistente **Canales** :

   1. Especifique **create_first_ic_print_template** como plantilla de impresión y toque **Seleccionar**. Asegúrese de que la casilla de verificación **Usar impresión como principal para canal** web no está seleccionada.

   1. Especifique la carpeta **Create_First_IC_templates** > **Create_First_IC_Web_Template** como plantilla Web y toque **Seleccionar**.

   1. Toque **Crear**.
   Se muestra un mensaje de confirmación de que la comunicación interactiva se ha creado correctamente.

1. Toque **Editar** para abrir la comunicación interactiva en el panel derecho.
1. Toque la ficha **Canales** del panel izquierdo y toque **Web**.
1. Vaya a la ficha **Recursos** y aplique el filtro para mostrar solo los fragmentos de documento en el panel izquierdo.
1. Arrastre y suelte los siguientes fragmentos de documento en sus áreas de destino en la Comunicación interactiva:

   | Fragmento de documento | Área de destino |
   |---|---|
   | bill_details_first_ic | Detalles de la factura |
   | customer_details_first_ic | Detalles del cliente |
   | bill_summary_first_ic | Resumen de factura |
   | summary_loads_first_interactive_Communication | Cargos |

1. Toque **Resumen de cargos** en el área de destino y toque **+** para agregar un componente de **gráfico** .
1. Puntee en el componente Gráfico y seleccione ![](assets/configure_icon.png) (Configurar). Las propiedades del gráfico se muestran en el panel izquierdo:

   1. Especifique un nombre para el gráfico.
   1. Seleccione **Circular** en la lista desplegable Tipo **de** gráfico.

   1. Seleccione la propiedad **calltype** del tipo de objeto del modelo de datos de **llamadas** en la sección del eje **** X. Tocar ![](assets/done_icon.png).

   1. Seleccione **Frecuencia** en la lista desplegable **Función** .

   1. Seleccione la propiedad **calltype** del tipo de objeto del modelo de datos de **llamadas** en la sección eje **** Y. Tocar ![](assets/done_icon.png).

   1. Toque ![](assets/done_icon.png) para guardar las propiedades del gráfico.

1. Seleccione la ficha Fuentes **de** datos en el panel izquierdo y arrastre y suelte el objeto del modelo de datos de **llamadas** en el área de destino Llamadas **** por elemento. Todas las propiedades del objeto del modelo de datos de **llamadas** se muestran como columnas de tabla en el área de destino Llamadas **** por elemento del panel derecho.

   En función del caso de uso, se requieren las columnas Fecha de llamada, Hora de llamada, Número de llamada, Duración de llamada y Cargos de llamada en la tabla.

   ![Tabla de comunicación interactiva](assets/table_ic_web_new.png)

1. Seleccione el encabezado de la columna de la tabla **Móvil** y seleccione **Más opciones** > **Eliminar columna**. Del mismo modo, elimine la columna **Tipo** de llamada.
1. Seleccione el encabezado de la columna de la tabla **Calldate** y toque ![Editar](assets/edit.png) (Editar) para cambiar el nombre del texto a Fecha **de** llamada. Del mismo modo, cambie el nombre de otros encabezados de columna en la tabla.
1. En función del caso de uso, inserte un botón **Pagar ahora** en la Comunicación interactiva que proporciona al usuario una opción para realizar el pago haciendo clic en el botón. Siga los pasos siguientes para insertar el botón:

   1. Toque **Pagar ahora** el área de destino y toque **+** para agregar un componente de **texto** .

   1. Toque el componente de texto y toque ![Editar](assets/edit.png) (Editar).
   1. Cambie el nombre del texto a **Pagar ahora**.
   1. Seleccione el texto y toque el icono Hipervínculo.
   1. Especifique la URL de pago en el campo **Ruta** .
   1. Seleccione **Nueva ficha** en la lista desplegable **Destino** .

   1. Toque ![](assets/done_icon.png) para guardar las propiedades del hipervínculo.

1. Seleccione **Estilo** en la lista desplegable situada junto a la opción **Vista previa** .

   ![Seleccionar modo de estilo para la comunicación interactiva](assets/select_style_ic_web_new.png)

1. Defina el estilo del texto del hipervínculo para que se muestre como un botón en la Comunicación interactiva siguiendo los pasos siguientes:

   1. Toque el componente de texto y seleccione ![Editar](assets/edit.png) (Editar).
   1. En la sección **Borde** , especifique **1,5 px** como Ancho **** del borde, seleccione **Sólido** como Estilo ******** **** del borde y especifique 46 pxcomo Radio del borde.

   1. Seleccione Rojo como color de fondo para el botón en la sección **Fondo** .
   1. En el campo **Margen** de la sección **Dimensiones y posición** , toque el icono **Editar simultáneamente** y defina el margen **Derecho** como **450 px**. Los campos Superior, Inferior e Izquierda se definen como en blanco.
   ![Insertar hipervínculo en comunicación interactiva](assets/ic_web_hyperlink_new.png)

1. Toque **Pagar ahora** el área de destino y toque **+** para agregar un componente **Imagen** .
1. Puntee en el componente Imagen y seleccione ![](assets/configure_icon.png) (Configurar). Las propiedades de imagen se muestran en el panel izquierdo:

   1. Especifique **PayNow** como nombre de la imagen en el campo **Nombre** .

   1. Toque **Cargar**, seleccione la imagen **PayNowWeb** guardada en el sistema de archivos local y toque **Abrir**.

   1. Toque ![](assets/done_icon.png) para guardar las propiedades de la imagen.

1. En función del caso de uso, inserte un botón **Suscribirse** en la Comunicación interactiva que ofrece al usuario la opción de suscribirse a los servicios de valor añadido haciendo clic en el botón.

   Repita los pasos 13 a 17 para agregar un botón **Suscribirse** al área de destino Servicios **de** valor agregado y agregar la imagen **ValueAddedServicesWeb** .

## Crear comunicaciones interactivas para impresión y Web con sincronización automática {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

También puede crear una comunicación interactiva habilitando la sincronización automática entre los canales Imprimir y Web. Para habilitar la sincronización automática, seleccione la opción Imprimir como formato al crear la comunicación interactiva. Al seleccionar la opción Imprimir como principal, se garantiza que el contenido, la herencia y el enlace de datos del canal Web se deriven del canal Imprimir. También garantiza que los cambios realizados en el canal Imprimir se reflejen en el canal Web.

Ejecute los siguientes pasos para derivar el contenido del canal Web mediante el canal Imprimir:

1. Inicie sesión en la instancia de creación de AEM y vaya a **Adobe Experience Manager** > **Formularios** > **Formularios y documentos**.
1. Toque **Crear** y seleccione Comunicación **** interactiva. Se muestra el asistente **Crear comunicación** interactiva.
1. Especifique **create_first_ic** en el campo **Título** y **Nombre** . Seleccione **FDM_Create_First_IC** como modelo de datos de formulario y toque **Siguiente**.
1. En el asistente **Canales** :

   1. Especifique **create_first_ic_print_template** como plantilla de impresión y toque **Seleccionar**.

   1. Seleccione la casilla de verificación **Usar Imprimir como principal para canal** web.
   1. Especifique la carpeta **Create_First_IC_templates** > **Create_First_IC_Web_Template** como plantilla Web y toque **Seleccionar**.

   1. Toque **Crear**.
   Se muestra un mensaje de confirmación de que la comunicación interactiva se ha creado correctamente.

1. Toque **Editar** para abrir la comunicación interactiva en el panel derecho.
1. Ejecute los pasos 6 a 15 de la sección [Crear comunicación interactiva para el canal](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel) de impresión.
1. Toque la ficha **Canales** del panel izquierdo y toque **Web** para generar automáticamente contenido para el canal Web desde el canal Imprimir.
1. Como la casilla de verificación **Usar impresión como principal para canal** web está seleccionada en el paso 4, el contenido y los enlaces se generan automáticamente para el canal web desde el canal de impresión.

   El contenido del canal de impresión se inserta debajo del contenido de la plantilla de canal Web. Para modificar el contenido del canal Web que se ha generado automáticamente desde el canal Imprimir, puede cancelar la herencia de cualquier área de destino.

   Pase el ratón sobre el área de destino relevante en el canal web, seleccione ![cancelar herencia](assets/cancelinheritance.png) (Cancelar herencia) y, a continuación, en el cuadro de diálogo **Cancelar herencia** , toque **Sí**.

   ![Cancelar herencia](assets/cancel_inheritance_web_channel_new.png)

   Si ha cancelado la herencia de un componente, puede volver a activarlo. Para volver a habilitar la herencia, pase el ratón sobre el límite del área de destino correspondiente, que incluye el componente, y toque ![volver a habilitar la herencia](assets/reenableinheritance.png).

1. Seleccione la ficha **Contenido** en el panel izquierdo.
1. Arrastre y suelte el contenido del canal Web generado automáticamente en los paneles existentes en la plantilla Web mediante el árbol de contenido. A continuación se muestra la lista de componentes que deben reorganizarse:

   * Componente Detalles de la factura al panel Detalles de la factura
   * Componente Detalles del cliente al panel Detalles del cliente
   * Componente Resumen de Facturación al panel Resumen de Facturación
   * Resumen del componente Cargos al panel Resumen de Cargos
   * Fragmento de diseño (tabla) al panel Llamadas por elemento
   ![Árbol de contenido web](assets/ic_web_content_tree_new.png)

1. Repita los pasos 13 a 18 de [Crear comunicación interactiva para el canal](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) Web para insertar los hipervínculos **Pagar ahora** y **Suscribirse** en el canal Web de la comunicación interactiva.

