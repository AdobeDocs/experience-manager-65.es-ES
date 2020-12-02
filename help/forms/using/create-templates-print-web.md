---
title: '"Tutorial: Crear plantillas"'
seo-title: Creación de plantillas de impresión y Web para comunicación interactiva
description: Creación de plantillas de impresión y Web para comunicación interactiva
seo-description: Creación de plantillas de impresión y Web para comunicación interactiva
uuid: 22256a61-bcf6-4b02-9ee6-0ffb1cc20a6e
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 879ff6ca-e5f3-451d-acc2-f75142101ddd
docset: aem65
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '1812'
ht-degree: 0%

---


# Tutorial: Crear plantillas{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Este tutorial es un paso en la serie [Crear su primera comunicación interactiva](/help/forms/using/create-your-first-interactive-communication.md). Se recomienda seguir la serie en secuencia cronológica para comprender, realizar y demostrar el caso de uso completo del tutorial.

Para crear una comunicación interactiva, debe tener plantillas disponibles en el servidor de AEM para Canales impresos y Web.

Las plantillas para el canal de impresión se crean en Adobe Forms Designer y se cargan en el servidor de AEM. Estas plantillas están disponibles para su uso durante la creación de una comunicación interactiva.

Las plantillas para el canal Web se crean en AEM. Los creadores y administradores de plantillas pueden crear, editar y habilitar plantillas web. Una vez creadas y habilitadas, estas plantillas están disponibles para su uso durante la creación de una comunicación interactiva.

Este tutorial le guiará por los pasos para crear plantillas para canales impresos y Web de modo que estén disponibles para su uso durante la creación de comunicaciones interactivas. Al final de este tutorial, podrá:

* Creación de plantillas XDP para canal de impresión mediante Adobe Forms Designer
* Cargar las plantillas XDP en AEM Forms Server
* Crear y habilitar plantillas para el canal Web

## Crear plantilla para el canal de impresión {#create-template-for-print-channel}

Cree y gestione una plantilla para el canal de impresión de la comunicación interactiva mediante las siguientes tareas:

* [Creación de una plantilla XDP con Forms Designer](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [Cargar plantilla XDP en el servidor de AEM Forms](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [Creación de una plantilla XDP para fragmentos de diseño](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### Crear una plantilla XDP con Forms Designer {#create-xdp-template-using-forms-designer}

En función del [caso de uso](/help/forms/using/create-your-first-interactive-communication.md) y [anatomía](/help/forms/using/planning-interactive-communications.md), cree los siguientes subformularios en la plantilla XDP:

* Detalles de la factura: Incluye un fragmento de documento
* Detalles del cliente: Incluye un fragmento de documento
* Resumen de facturación: Incluye un fragmento de documento
* Resumen: Incluye un fragmento de documento (subformulario Cargos) y un gráfico (subformulario Gráficos)
* Llamadas por elementos: Incluye una tabla (fragmento de diseño)
* Pagar ahora: Incluye una imagen
* Servicios Añadidos de valor: Incluye una imagen

![create_print_template](assets/create_print_template.gif)

Estos subformularios se muestran como áreas de destinatario en la plantilla Imprimir después de cargar el archivo XDP al servidor de Forms. Todas las entidades, como fragmentos de documento, gráficos, fragmentos de diseño e imágenes, se agregan a las áreas de destinatario al crear la comunicación interactiva.

Siga los pasos siguientes para crear una plantilla XDP para el canal de impresión:

1. Abra Forms Designer, seleccione **Archivo** > **Nuevo** > **Usar un formulario en blanco,** toque **Siguiente** y luego toque **Finalizar** para abrir el formulario para la creación de plantillas.

   Asegúrese de que las opciones **Biblioteca de objetos** y **Objeto** están seleccionadas en el menú **Ventana**.

1. Arrastre y suelte el componente **Subformulario** desde la **Biblioteca de objetos** al formulario.
1. Seleccione el subformulario para mostrar las opciones del subformulario en la ventana **Objeto** del panel derecho.
1. Seleccione la ficha **Subformulario** y seleccione **De posición variable** en la lista desplegable **Contenido**. Arrastre el extremo izquierdo del subformulario para ajustar la longitud.
1. En la ficha **Enlaces**:

   1. Especifique **BillDetails** en el campo **Nombre**.

   1. Seleccione **Ningún enlace de datos** en la lista desplegable **Enlace de datos**.

   ![Subformulario de Designer](assets/forms_designer_subform_new.png)

1. Del mismo modo, seleccione el subformulario raíz, seleccione la ficha **Subformulario** y seleccione **De posición variable** en la lista desplegable **Contenido**. En la ficha **Enlaces**:

   1. Especifique **TelecaBill** en el campo **Nombre**.

   1. Seleccione **Ningún enlace de datos** en la lista desplegable **Enlace de datos**.

   ![Subformulario para plantilla Imprimir](assets/root_subform_print_template_new.png)

1. Repita los pasos 2 a 5 para crear los subformularios siguientes:

   * Detalles de la factura
   * Detalles del cliente
   * Resumen de factura
   * Resumen: seleccione la ficha **Subformulario** y seleccione **Colocado** en la lista desplegable **Contenido** para este subformulario. Inserte los subformularios siguientes en el subformulario **Resumen**.

      * Cargos
      * Gráficos
   * ItemizedCalls
   * PayNow
   * ValueAddedServices

   Para ahorrar tiempo, también puede copiar y pegar subformularios existentes para crear nuevos subformularios.

   Para cambiar el subformulario **Gráficos** a la derecha del subformulario Cargos, seleccione el subformulario **Gráficos** en el panel izquierdo, seleccione la ficha **Presentación** y especifique un valor para el campo **AnclajeX**. El valor debe ser bueno que el valor del campo **Ancho** del subformulario **Cargos**. Seleccione el subformulario **Cargos** y seleccione la ficha **Presentación** para vista del valor del campo **Ancho**.

1. Arrastre y suelte el objeto **Text** de la **Biblioteca de objetos** en el formulario e introduzca el texto **Marque XXXX para suscribirse** en el cuadro.
1. Haga clic con el botón derecho en el objeto de texto del panel izquierdo, seleccione **Cambiar el nombre del objeto** e introduzca el nombre del objeto de texto como **Suscribirse**.

   ![Plantilla XDP](assets/print_xdp_template_subform_new.png)

1. Seleccione **Archivo** > **Guardar como** para guardar el archivo en el sistema de archivos local:

   1. Vaya a la ubicación para guardar el archivo y especifique el nombre como **create_first_ic_print_template**.
   1. Seleccione **.xdp** en la lista desplegable **Guardar como tipo**.

   1. Toque **Guardar**.

### Cargar plantilla XDP en el servidor de AEM Forms {#upload-xdp-template-to-the-aem-forms-server}

Una vez creada una plantilla XDP con Forms Designer, debe cargarla en el servidor de AEM Forms para que la plantilla esté disponible para su uso durante la creación de la comunicación interactiva.

1. Seleccione **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documentos]**.
1. Toque **Crear** > **Carga de archivo**.

   Navegue y seleccione la plantilla **create_first_ic_print_template** (XDP) y toque **Abrir** para importar la plantilla XDP al servidor de AEM Forms.

### Crear una plantilla XDP para fragmentos de diseño {#create-xdp-template-for-layout-fragments}

Para crear un fragmento de diseño para el canal de impresión de la comunicación interactiva, cree un XDP con Forms Designer y cárguelo en el servidor de AEM Forms.

1. Abra Forms Designer, seleccione **Archivo** > **Nuevo** > **Usar un formulario en blanco,** toque **Siguiente** y luego toque **Finalizar** para abrir el formulario para la creación de plantillas.

   Asegúrese de que las opciones **Biblioteca de objetos** y **Objeto** están seleccionadas en el menú **Ventana**.

1. Arrastre y suelte el componente **Tabla** desde la **Biblioteca de objetos** al formulario.
1. En el cuadro de diálogo Insertar tabla:

   1. Especifique el número de columnas como **5**.
   1. Especifique el número de filas de trabajo como **1**.
   1. Seleccione la casilla **Incluir fila de encabezado en tabla**.
   1. Tab **Aceptar**.

1. Puntee **+** en el panel izquierdo junto a **Tabla** 1 y haga clic con el botón derecho en **Celda1** y seleccione **Cambiar el nombre del objeto** a **Fecha**.

   Del mismo modo, cambie el nombre de **Cell2**, **Cell3**, **Cell4** y **Cell5** por **Time**, **Number**, **Duration&lt;a11. 3/> y** Cargos **respectivamente.**

1. Haga clic en los campos de texto Encabezado de la **Vista de Designer** y cámbieles el nombre **Tiempo**, **Número**, **Duración** y **Cargos**.

   ![Fragmento de diseño](assets/layout_fragment_print_new.png)

1. Seleccione **Fila 1** en el panel izquierdo y seleccione **Objeto** > **Enlace** > **Repetir fila para cada elemento de datos**.

   ![Repetir propiedades para el fragmento de diseño](assets/layout_fragment_print_repeat_new.png)

1. Arrastre y suelte el componente **Campo de texto** desde la **Biblioteca de objetos** a la **Vista de Designer**.

   ![Campo de texto para fragmento de diseño](assets/layout_fragment_print_text_field_new.png)

   Del mismo modo, arrastre y suelte el componente **Campo de texto** en las filas **Tiempo**, **Número**, **Duración** y **Cargos**.

1. Seleccione **Archivo** > **Guardar como** para guardar el archivo en el sistema de archivos local:

   1. Vaya a la ubicación para guardar el archivo y especifique el nombre como **table_lf**.
   1. Seleccione **.xdp** en la lista desplegable **Guardar como tipo**.

   1. Toque **Guardar**.
   Una vez que haya creado una plantilla XDP para el fragmento de diseño con Forms Designer, debe [cargarla](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server) en el servidor de AEM Forms para que la plantilla esté disponible para su uso durante la creación de fragmentos de diseño.

## Crear plantilla para canal Web {#create-template-for-web-channel}

Cree y administre una plantilla para el canal Web de comunicación interactiva mediante las siguientes tareas:

* [Crear carpeta para plantillas](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [Crear la plantilla](../../forms/using/create-templates-print-web.md#create-the-template)
* [Habilitar la plantilla](../../forms/using/create-templates-print-web.md#enable-the-template)
* [Activación de botones en Interactive Communications](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### Crear carpeta para plantillas {#create-folder-for-templates}

Para crear una plantilla de canal web, defina una carpeta en la que puede guardar las plantillas creadas. Una vez que haya creado una plantilla dentro de esa carpeta, habilite la plantilla para permitir que los usuarios de los formularios creen un canal web de una comunicación interactiva basada en la plantilla.

Siga los pasos siguientes para crear una carpeta para las plantillas editables:

1. Toque **Herramientas** ![martillo-icono](assets/hammer-icon.svg) > **Navegador de configuración**.
   * Consulte la documentación de [Configuration Browser](/help/sites-administering/configurations.md) para obtener más información.
1. En la página Navegador de configuración, toque **Crear**.
1. En el cuadro de diálogo **Crear configuración**, especifique **Create_First_IC_templates** como título para la carpeta, marque **Plantillas editables** y toque **Crear**.

   ![Configuración de plantillas web](assets/create_first_ic_web_template_new.png)

   La carpeta **Create_First_IC_templates** se crea y se enumera en la página **Configuration Browser**.

### Crear la plantilla {#create-the-template}

En función del [caso de uso](/help/forms/using/create-your-first-interactive-communication.md) y [anatomía](/help/forms/using/planning-interactive-communications.md), cree los paneles siguientes en la plantilla Web:

* Detalles de la factura: Incluye un fragmento de documento
* Detalles del cliente: Incluye un fragmento de documento
* Resumen de facturación: Incluye un fragmento de documento
* Resumen de cargos: Incluye un fragmento de documento y un gráfico (diseño de dos columnas)
* Llamadas por elementos: Incluye una tabla
* Pagar ahora: Incluye un botón **Pagar ahora** y una imagen
* Servicios Añadidos de valor: Incluye una imagen y un botón **Suscribirse**.

![create_web_template](assets/create_web_template.gif)

Todas las entidades, como fragmentos de documento, gráficos, tablas, imágenes y botones, se agregan al crear la comunicación interactiva.

Ejecute los siguientes pasos para crear una plantilla para el canal Web en la carpeta **Create_First_IC_templates**:

1. Vaya a la carpeta de plantillas adecuada seleccionando la carpeta **Herramientas** > **Plantillas** > **Crear_plantillas_IC_iniciales**.
1. Toque **Crear**.
1. En el asistente de configuración **Elija un tipo de plantilla**, seleccione **Comunicación interactiva - Canal Web** y toque **Siguiente**.
1. En el asistente de configuración **Detalles de plantilla**, especifique **Create_First_IC_Web_Template** como título de plantilla. Especifique una descripción opcional y toque **Crear**.

   Se muestra un mensaje de confirmación de que **Create_First_IC_Web_Template**.

1. Toque **Abrir** para abrir la plantilla en el editor de plantillas.
1. Seleccione **Contenido inicial** en la lista desplegable al lado de la opción **Previsualización**.

   ![Editor de plantillas](assets/template_editor_initial_content_new.png)

1. Toque **Panel raíz** y luego toque **+** para vista de la lista de componentes que puede agregar a la plantilla.
1. Seleccione **Panel** en la lista para agregar un panel sobre el **Panel raíz**.
1. Seleccione la ficha **Contenido** en el panel izquierdo. El nuevo panel agregado en el paso 8 se muestra en el **Panel raíz** en el árbol de contenido.

   ![Árbol de contenido](assets/content_tree_root_panel_new.png)

1. Seleccione el panel y toque ![configure_icon](assets/configure_icon.png) (Configurar).
1. En el panel Propiedades:

   1. Especifique **detalles de facturación** en el campo Nombre.
   1. Especifique **Detalles de la factura** en el campo Título.
   1. Seleccione **1** en la lista desplegable **Número de columnas**.

   1. Toque ![](/help/forms/using/assets/done_icon.png) para guardar las propiedades.

   El nombre del panel se actualiza a **Detalles de la factura** en el árbol de contenido.

1. Repita los pasos 7 a 11 para agregar paneles con las siguientes propiedades a la plantilla:

   | Nombre | Título | Número de columnas |
   |---|---|---|
   | detalles del cliente | Detalles del cliente | 1 |
   | resumen de facturación | Resumen de facturación | 3 |
   | summaryfees | Resumen de cargos | 2 |
   | itemisedcall | Llamadas por elementos | 1 |
   | paynow | Pagar ahora | 2 |
   | lienzo | Servicios Añadidos de valor | 1 |

   La siguiente imagen muestra el árbol de contenido después de agregar todos los paneles a la plantilla:

   ![Árbol de contenido para todos los paneles](assets/content_tree_all_panels_new.png)

### Habilitar la plantilla {#enable-the-template}

Una vez que haya creado la plantilla Web, debe habilitarla para utilizar la plantilla mientras crea la Comunicación interactiva.

Ejecute los siguientes pasos para habilitar la plantilla Web:

1. Puntee **Herramientas** ![icono de martillo](assets/hammer-icon.svg) > **Plantillas**.
1. Vaya a la plantilla **Create_First_IC_Web_Template**, selecciónela y toque **Habilitar**.
1. Tab **Active** nuevamente para confirmar.

   La plantilla está habilitada y su estado se muestra como Habilitada. Puede utilizar esta plantilla al crear Comunicación interactiva para el canal Web.

### Activación de botones en Interactive Communications {#enabling-buttons-in-interactive-communications}

En función del caso de uso, debe incluir los botones **Pagar ahora** y **Suscribirse** (componentes de formularios adaptables) en Comunicación interactiva. Para habilitar el uso de estos botones en la comunicación interactiva, ejecute los siguientes pasos:

1. Seleccione **Estructura** en la lista desplegable al lado de la opción **Previsualización**.
1. Seleccione el panel raíz **Contenedor de Documento** mediante el árbol de contenido y toque **Directiva** para seleccionar los componentes que se pueden usar en la Comunicación interactiva.

   ![Configurar directiva](assets/structure_configure_policy_new.png)

1. En la ficha **Componentes permitidos** de la sección **Propiedades**, seleccione **Botón** en los componentes **Formulario adaptable**.

   ![Componentes permitidos](assets/allowed_components_af_new.png)

1. Toque ![done_icon](assets/done_icon.png) para guardar las propiedades.