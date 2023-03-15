---
title: '“Tutorial: Crear plantillas”'
seo-title: Create Print and Web templates for Interactive Communication
description: Crear plantillas Imprimir y Web para comunicaciones interactivas
seo-description: Create Print and Web templates for Interactive Communication
uuid: 22256a61-bcf6-4b02-9ee6-0ffb1cc20a6e
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 879ff6ca-e5f3-451d-acc2-f75142101ddd
docset: aem65
feature: Interactive Communication
exl-id: bef1f05e-aea2-433e-b3d5-0b7ad8163fa7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1796'
ht-degree: 100%

---

# Tutorial: Crear plantillas{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Este tutorial es un paso en la serie [Crear su primera comunicación interactiva](/help/forms/using/create-your-first-interactive-communication.md). Se recomienda seguir la serie en orden cronológico para comprender, realizar y mostrar el caso de uso del tutorial completo.

Para crear una comunicación interactiva, debe tener plantillas disponibles en el servidor de AEM para los canales Imprimir y Web.

Las plantillas del canal Imprimir se crean en Adobe Forms Designer y se cargan en el servidor de AEM. Estas plantillas están disponibles para su uso durante la creación de una comunicación interactiva.

Las plantillas del canal Web se crean en AEM. Los autores y administradores de plantillas pueden crear, editar y habilitar plantillas web. Una vez creadas y habilitadas, estas plantillas están disponibles para usarlas durante la creación de una comunicación interactiva.

Este tutorial mostrará los pasos para crear plantillas para los canales Imprimir y Web para que estén disponibles para usarlas durante la creación de comunicaciones interactivas. Al final de este tutorial, podrá:

* Crear plantillas XDP para el canal Imprimir mediante Adobe Forms Designer
* Cargar las plantillas XDP al servidor de AEM Forms
* Crear y habilitar plantillas para el canal Web

## Crear plantillas para el canal Imprimir {#create-template-for-print-channel}

Crear y administrar una plantilla para el canal Imprimir de una comunicación interactiva mediante las siguientes tareas:

* [Crear una plantilla XDP con Forms Designer](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [Cargar una plantilla XDP en el servidor de AEM Forms](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [Crear una plantilla XDP para fragmentos de diseño](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### Crear una plantilla XDP con Forms Designer {#create-xdp-template-using-forms-designer}

En función del [caso de uso](/help/forms/using/create-your-first-interactive-communication.md) y la [anatomía](/help/forms/using/planning-interactive-communications.md), cree los siguientes subformularios en la plantilla XDP:

* Detalles de la factura: incluye un fragmento de documento
* Detalles del cliente: incluye un fragmento de documento
* Resumen de la factura: incluye un fragmento de documento
* Resumen: incluye un fragmento de documento (subformulario Costes) y un gráfico (subformulario Gráficos)
* Llamadas desglosadas: incluye una tabla (fragmento de diseño)
* Pagar ahora: incluye una imagen
* Servicios de valor agregado: incluye una imagen

![create_print_template](assets/create_print_template.gif)

Estos subformularios se muestran como áreas de destino en la plantilla Imprimir después de cargar el archivo XDP en el servidor de Forms. Todas las entidades, como fragmentos de documento, gráficos, fragmentos de diseño e imágenes, se agregan a las áreas de destino al crear la comunicación interactiva.

Ejecute los siguientes pasos para crear una plantilla XDP para el canal Imprimir:

1. Abra Forms Designer, seleccione **Archivo** > **Nuevo** > **Utilizar un formulario en blanco**, pulse **Siguiente** y, a continuación, pulse **Finalizar** para abrir el formulario para crear plantillas.

   Asegúrese de que las opciones **Biblioteca de objetos** y **Objeto** se seleccionan en el menú **Ventana**.

1. Arrastre y suelte el componente **Subformulario** de la **Biblioteca de objetos** al formulario.
1. Seleccione el subformulario para mostrar sus opciones en la ventana **Objeto** del panel derecho.
1. Seleccione la pestaña **Subformulario** y luego seleccione **De posición variable** en la lista desplegable **Contenido**. Arrastre el extremo izquierdo del subformulario para ajustar la longitud.
1. En la pestaña **Enlaces**:

   1. Especifique **BillDetails** en el campo **Nombre**.

   1. Seleccione **Sin enlace de datos** en la lista desplegable **Enlace de datos**.

   ![Subformulario de Designer](assets/forms_designer_subform_new.png)

1. Del mismo modo, seleccione el subformulario raíz, seleccione la pestaña **Subformulario** y seleccione **Flujo** de la lista desplegable **Contenido**. En la pestaña **Enlaces**:

   1. Especifique **TelecaBill** en el campo **Nombre**.

   1. Seleccione **Sin enlace de datos** en la lista desplegable **Enlace de datos**.

   ![Subformulario para plantilla Imprimir](assets/root_subform_print_template_new.png)

1. Repita del paso 2 al 5 para crear los siguientes subformularios:

   * BillDetails
   * CustomerDetails
   * BillSummary
   * Resumen: seleccione la pestaña **Subformulario** y seleccione **Colocado** de la lista desplegable **Contenido** para este subformulario. Inserte los siguientes subformularios en el subformulario **Resumen**.

      * Gastos
      * Gráficos
   * ItemisedCalls
   * PayNow
   * ValueAddedServices

   Para ahorrar tiempo, también puede copiar y pegar subformularios existentes para crear subformularios nuevos.

   Para cambiar el subformulario **Gráficos** a la derecha del subformulario Gastos, seleccione el subformulario **Gráficos** del panel izquierdo, seleccione la pestaña **Diseño** y especifique un valor para el campo **AnchorX**. El valor debe ser mayor que el valor del campo **Anchura** para el subformulario **Gastos**. Seleccione el subformulario **Gastos** y seleccione la pestaña **Diseño** para ver el valor del campo **Anchura**.

1. Arrastre y suelte el objeto **Texto** desde la **Biblioteca de objetos** hasta el formulario y escriba el texto **Marque XXXX para suscribirse** en el cuadro.
1. Haga clic con el botón derecho en el objeto de texto del panel izquierdo y seleccione **Cambiar nombre de objeto** y escriba el nombre para el objeto de texto como **Suscribirse**.

   ![Plantilla XDP](assets/print_xdp_template_subform_new.png)

1. Seleccione **Archivo** > **Guardar como** para guardar el archivo en el sistema de archivos local:

   1. Navegue hasta la ubicación para guardar el archivo y especifique el nombre como **create_first_ic_print_template**.
   1. Seleccione **.xdp** en la lista desplegable **Guardar como tipo**.

   1. Pulse **Guardar**.

### Cargar una plantilla XDP en el servidor de AEM Forms {#upload-xdp-template-to-the-aem-forms-server}

Una vez creada una plantilla XDP con el Forms Designer, debe cargarla en el servidor de AEM Forms para que la plantilla esté disponible para su uso durante la creación de comunicaciones interactivas.

1. Seleccione **[!UICONTROL Forms]** > **[!UICONTROL Formularios y documentos]**.
1. Pulse **Crear** > **Cargar archivo**.

   Desplácese y seleccione la plantilla **create_first_ic_print_template** (XDP) y pulse **Abrir** para importar la plantilla XDP al servidor de AEM Forms.

### Crear una plantilla XDP para fragmentos de diseño {#create-xdp-template-for-layout-fragments}

Para crear un fragmento de diseño para el canal Imprimir de la comunicación interactiva, cree un XDP con Forms Designer y cárguelo en el servidor de AEM Forms.

1. Abra Forms Designer, seleccione **Archivo** > **Nuevo** > **Utilizar un formulario en blanco**, pulse **Siguiente** y, a continuación, pulse **Finalizar** para abrir el formulario para crear plantillas.

   Asegúrese de que las opciones **Biblioteca de objetos** y **Objeto** se seleccionan en el menú **Ventana**.

1. Arrastre y suelte el componente **Tabla** desde la **Biblioteca de objetos** hasta el formulario.
1. En el cuadro de diálogo Insertar tabla:

   1. Especifique el número de columnas como **5**.
   1. Especifique el número de filas como **1**.
   1. Seleccione la casilla de verificación **Incluir fila de encabezado en la tabla**.
   1. Pulse **Aceptar**.

1. Pulse **+** en el panel izquierdo junto a **Tabla** 1 y haga clic con el botón derecho en **Cell1** y seleccione **Cambiar nombre de objeto** a **Fecha**.

   Del mismo modo, cambie el nombre de **Cell2**, **Cell3**, **Cell4** y **Cell5** a **Hora**, **Número**, **Duración** y **Gastos** respectivamente.

1. Haga clic en los campos de texto del encabezado en la **Vista de Designer** y cambie sus nombres a **Tiempo**, **Número**, **Duración** y **Gastos**.

   ![Fragmento de diseño ](assets/layout_fragment_print_new.png)

1. Seleccione **Fila 1** en el panel izquierdo y seleccione **Objeto** > **Enlace** > **Repetir fila para cada elemento de datos**.

   ![Repetir propiedades para el fragmento de diseño](assets/layout_fragment_print_repeat_new.png)

1. Arrastre y suelte el componente **Campo de texto** desde la **Biblioteca de objetos** hasta la **Vista de Designer**.

   ![Campo de texto para fragmento de diseño](assets/layout_fragment_print_text_field_new.png)

   Del mismo modo, arrastre y suelte el componente **Campo de texto** hasta las filas **Tiempo**, **Número**, **Duración** y **Gastos**.

1. Seleccione **Archivo** > **Guardar como** para guardar el archivo en el sistema de archivos local:

   1. Navegue hasta la ubicación para guardar el archivo y especifique el nombre como **table_lf**.
   1. Seleccione **.xdp** en la lista desplegable **Guardar como tipo**.

   1. Pulse **Guardar**.
   Una vez creada una plantilla XDP para el fragmento de diseño con Forms Designer, debe [cargarla](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server) en el servidor de AEM Forms para que la plantilla esté disponible para usarla durante la creación de fragmentos de diseño.

## Crear una plantilla para el canal Web {#create-template-for-web-channel}

Cree y administre una plantilla para el canal Web de comunicaciones interactivas mediante las siguientes tareas:

* [Crear carpeta para plantillas](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [Crear la plantilla](../../forms/using/create-templates-print-web.md#create-the-template)
* [Habilitar la plantilla](../../forms/using/create-templates-print-web.md#enable-the-template)
* [Activar botones en las comunicaciones interactivas](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### Crear carpeta para plantillas {#create-folder-for-templates}

Para crear una plantilla del canal Web, defina una carpeta en la que pueda guardar las plantillas creadas. Una vez creada una plantilla dentro de esa carpeta, habilítela para permitir a los usuarios de los formularios crear un canal Web de una comunicación interactiva basada en la plantilla.

Ejecute los siguientes pasos para crear una carpeta para las plantillas editables:

1. Pulse **Herramientas** ![hammer-icon](assets/hammer-icon.svg) > **Explorador de configuración**.
   * Consulte la documentación del [Explorador de configuración](/help/sites-administering/configurations.md) para obtener más información.
1. En la página Explorador de configuración, pulse **Crear**.
1. En el cuadro de diálogo **Crear configuración**, especifique **Create_First_IC_templates** como título de la carpeta, marque **Plantillas editables** y pulse **Crear**.

   ![Configurar plantillas web](assets/create_first_ic_web_template_new.png)

   La carpeta **Create_First_IC_templates** se crea y se enumera en la página **Explorador de configuración**.

### Crear la plantilla {#create-the-template}

En función del [caso de uso](/help/forms/using/create-your-first-interactive-communication.md) y la [anatomía](/help/forms/using/planning-interactive-communications.md), cree los siguientes paneles en la plantilla web:

* Detalles de la factura: incluye un fragmento de documento
* Detalles del cliente: incluye un fragmento de documento
* Resumen de la factura: incluye un fragmento de documento
* Resumen de gastos: incluye un fragmento de documento y un gráfico (diseño de dos columnas)
* Llamadas desglosadas: incluye una tabla
* Pagar ahora: Incluye un botón **Pagar ahora** y una imagen
* Servicios de valor agregado: incluye una imagen y un botón **Suscribirse**.

![create_web_template](assets/create_web_template.gif)

Todas las entidades, como fragmentos de documento, gráficos, tablas, imágenes y botones, se agregarán al crear la comunicación interactiva.

Siga estos pasos para crear una plantilla para el canal Web en la carpeta **Create_First_IC_templates**:

1. Navegue hasta la carpeta de plantillas adecuada al seleccionar la carpeta **Herramientas** > **Plantillas** > **Create_First_IC_templates**.
1. Pulse **Crear**.
1. En el asistente de configuración **Elegir un tipo de plantilla**, seleccione **Comunicación interactiva: canal Web** y pulse **Siguiente**.
1. En el asistente de configuración **Detalles de la plantilla**, especifique **Create_First_IC_Web_Template** como título de la plantilla. Especifique una descripción opcional y pulse **Crear**.

   Se mostrará el mensaje de confirmación **Create_First_IC_Web_Template**.

1. Pulse **Abrir** para abrir la plantilla en el editor de plantillas.
1. Seleccione **Contenido inicial** de la lista desplegable junto a la opción **Vista previa**.

   ![Editor de plantillas](assets/template_editor_initial_content_new.png)

1. Pulse **Panel raíz** y, a continuación, pulse **+** para ver la lista de componentes que puede agregar a la plantilla.
1. Seleccione **Panel** de la lista para agregar un panel sobre el **Panel raíz**.
1. Seleccione la pestaña **Contenido** en el panel izquierdo. El panel nuevo agregado en el paso 8 se mostrará en **Panel raíz** en el árbol de contenido.

   ![Árbol de contenido](assets/content_tree_root_panel_new.png)

1. Seleccione el panel y pulse ![configure_icon](assets/configure_icon.png) (Configurar).
1. En el panel Propiedades:

   1. Especifique **billdetails** en el campo Nombre.
   1. Especifique **Detalles de la factura** en el campo Título.
   1. Seleccione **1** de la lista desplegable **Número de columnas**.

   1. Pulse ![](/help/forms/using/assets/done_icon.png) para guardar las propiedades.

   El nombre del panel se actualiza a **Detalles de la factura** en el árbol de contenido.

1. Repita del paso 7 al 11 para agregar paneles con las siguientes propiedades a la plantilla:

   | Nombre | Título | Número de columnas |
   |---|---|---|
   | customerdetails | Detalles del cliente | 1 |
   | billsummary | Resumen de la factura | 1 |
   | summarycharges | Resumen de gastos | 2 |
   | itemisedcalls | Llamadas desglosadas | 1 |
   | paynow | Pagar ahora | 2 |
   | vas | Servicios de valor agregado | 1 |

   La siguiente imagen representa el árbol de contenido después de agregar todos los paneles a la plantilla:

   ![Árbol de contenido para todos los paneles](assets/content_tree_all_panels_new.png)

### Habilitar la plantilla {#enable-the-template}

Una vez creada la plantilla web, debe habilitarla para poder utilizarla al crear la comunicación interactiva.

Ejecute los siguientes pasos para habilitar la plantilla web:

1. Pulse **Herramientas** ![hammer-icon](assets/hammer-icon.svg) > **Plantillas**.
1. Navegue hasta la plantilla **Create_First_IC_Web_Template**, selecciónela y pulse **Habilitar**.
1. Pulse de nuevo **Habilitar** para confirmar.

   La plantilla está habilitada y su estado se muestra como Habilitada. Puede utilizar esta plantilla al crear la comunicación interactiva para el canal Web.

### Activar botones en las comunicaciones interactivas {#enabling-buttons-in-interactive-communications}

En función del caso de uso, debe incluir los botones **Pagar ahora** y **Suscribirse** (componentes de formularios adaptables) en la comunicación interactiva. Para habilitar el uso de estos botones en la comunicación interactiva, ejecute los siguientes pasos:

1. Seleccione **Estructura** de la lista desplegable junto a la opción **Vista previa**.
1. Seleccione el panel raíz **Contenedor de documento** mediante el árbol de contenido y pulse **Directiva** para seleccionar los componentes que se pueden usar en la comunicación interactiva.

   ![Configurar directiva](assets/structure_configure_policy_new.png)

1. En la pestaña **Componentes permitidos** de **Propiedades**, seleccione **Botón** de los componentes de **Formulario adaptable**.

   ![Componentes permitidos](assets/allowed_components_af_new.png)

1. Pulse ![done_icon](assets/done_icon.png) para guardar las propiedades.
