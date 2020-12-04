---
title: Uso de xtypes (IU clásica)
seo-title: Uso de xtypes (IU clásica)
description: Obtenga información sobre todos los tipos de expresiones disponibles con AEM
seo-description: Obtenga información sobre todos los tipos de expresiones disponibles con AEM
uuid: 6497caa4-2f9b-4f21-9023-88d485fd1d78
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: adb70b43-1b0b-4302-905a-c7612675dabb
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '6414'
ht-degree: 0%

---


# Uso de xtypes (IU clásica){#using-xtypes-classic-ui}

Esta página describe todos los tipos de expresiones disponibles con Adobe Experience Manager (AEM).

En el lenguaje ExtJS, un xtype es un nombre simbólico dado a una clase. Puede leer el párrafo &quot;Componente XTypes&quot; de la [Información general de ExtJS 2](https://www.sencha.com/learn/overview-of-extjs-2) para obtener una explicación detallada sobre qué es un xtype y cómo se puede utilizar.

Para obtener información completa sobre todos los widgets disponibles en AEM, consulte la [documentación de API de utilidades](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html).

Para averiguar en qué componentes se utiliza un xtype determinado en AEM, puede utilizar la siguiente consulta Xpath en CRXDE reemplazando &#39;Casilla&#39; por el xtype que le interese:

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>Esta página describe el uso de xtypes de ExtJS dentro de la IU clásica.
>
>Adobe recomienda aprovechar la IU [estándar, moderna y](/help/sites-developing/touch-ui-concepts.md) táctil basada en la IU [](/help/sites-developing/touch-ui-concepts.md#coral-ui) Coral y la IU [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

## xtypes {#xtypes}

A continuación encontrará una lista de los xtype disponibles en Adobe Experience Manager:

* anotación

   [CQ.wcm.AnNotación](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Annotation)

   El cuadro de diálogo es un tipo especial de ventana con un formulario en el cuerpo y un grupo de botones en el pie de página. Normalmente se utiliza para editar contenido, pero también para mostrar información.

* arraystore

   [CQ.Ext.data.ArrayStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayStore)

   Anteriormente conocido como &quot;SimpleStore&quot;.

   Clase auxiliar pequeña para facilitar la creación de [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)s a partir de datos de Array. Un ArrayStore se configurará automáticamente con un [CQ.Ext.data.ArrayReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayReader).

* asseteditor

   [CQ.dam.AssetEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.AssetEditor)

   Editor de recursos utilizado en Administración de DAM.

* assetreferenciesearchdialog

   [CQ.wcm.AssetReferenceSearchDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.AssetReferenceSearchDialog)

   AssetReferenceSearchDialog es un cuadro de diálogo que aparece en caso de que una página haga referencia a recursos o etiquetas.

* blueprintconfig

   [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig)

   BlueprintConfig proporciona un panel para la vista de las Live Copies de un modelo y la edición de estas propiedades de modelo (desencadenamiento de sincronización y acciones de sincronización).

* blueprintstatus

   [CQ.wcm.msm.BlueprintStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus)

   BlueprintStatus proporciona un panel para la vista y edición de un modelo y sus relaciones con Live Copies. La exploración se realiza mediante [CQ.wcm.msm.BlueprintStatus.Tree](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus.Tree), edición a través de [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig) y una [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties).

* box

   [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent)

   Clase base para cualquier [Componente](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component) que se va a cambiar de tamaño como un cuadro, utilizando anchura y altura.

   BoxComponent proporciona ajustes automáticos del modelo de cuadro para cambiar el tamaño y la posición y funcionará correctamente en el modelo de representación de componentes.

* browsedialog

   [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog)

   El cuadro de diálogo Examinar permite al usuario examinar el repositorio para seleccionar una ruta. Generalmente se utiliza a través de un [BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField).

* browsefield

   [CQ.form.BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField)

   **Obsoleto: Utilice  [CQ.form.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) PathField en su lugar**

* editor de bulkeditor

   [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor)

   El Editor masivo proporciona un motor de búsqueda y una cuadrícula para editar los resultados de la búsqueda.

   BulkEditor debe insertarse en un formulario HTML (requerido por la funcionalidad de importación). Esto funciona perfectamente con un [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* bulkeditorform

   [CQ.wcm.BulkEditorForm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditorForm)

   BulkEditorForm proporciona [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor) rodeado por un formulario HTML. Esta es la versión independiente del [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor); se requiere un formulario HTML para el botón de importación.

* botón

   [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)

   Clase Botón simple

* buttongroup

   [CQ.Ext.ButtonGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ButtonGroup)

   Contenedor para un grupo de botones.

* gráfico

   [CQ.Ext.chart.Chart](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart)

   El paquete CQ.Ext.chart proporciona la capacidad de visualizar datos con gráficos basados en flash. Cada gráfico se enlaza directamente a un CQ.Ext.data.Store que habilita las actualizaciones automáticas del gráfico. Para cambiar el aspecto de un gráfico, consulte las opciones de configuración [chartStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) y [extraStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart).

* casilla de verificación

   [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox)

   Campo de casilla de verificación única. Se puede utilizar como reemplazo directo de los campos de casillas de verificación tradicionales.

* checkboxgroup

   [CQ.Ext.form.CheckboxGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.CheckboxGroup)

   Un contenedor de agrupación para los controles [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox).

* clearcombo

   [CQ.form.ClearableComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ClearableComboBox)

   ClearableComboBox es un cuadro combinado no editable con un activador para borrar su valor.

* colorfield

   [CQ.form.ColorField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorField)

   ColorField permite al usuario introducir un valor hexadecimal de color directamente o mediante un [CQ.Ext.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorMenu).

* colorlist

   [CQ.form.ColorList](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorList)

   La Lista de colores permite al usuario elegir un color de una lista editable.

* colormenu

   [CQ.Ext.menu.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.ColorMenu)

   Menú que contiene un componente [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette).

* paleta de colores

   [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette)

   Clase de paleta de colores simple para elegir colores. La paleta se puede procesar en cualquier contenedor.

* combo

   [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)

   Control combinado compatible con autocompletar, carga remota, paginación y muchas otras funciones.

   Un ComboBox funciona de manera similar a un campo HTML tradicional &lt;select>. La diferencia es que para enviar el [valorField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox), debe especificar un [hiddenName](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) para crear una entrada oculta.

* componente

   [CQ.Ext.Component](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)

   Clase base para todos los componentes de Ext. Todas las subclases de Component pueden participar en el ciclo de vida automatizado del componente Ext de creación, procesamiento y destrucción que proporciona la clase [Contenedor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container). Los componentes se pueden agregar a un Contenedor mediante la opción de configuración [items](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) en el momento en que se crea el Contenedor.

* extractor de componentes

   [CQ.wcm.ComponentExtractor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ComponentExtractor)

   ComponentExtractor permite al usuario extraer componentes de un sitio web o una página.

* componentselector

   [CQ.form.ComponentSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentSelector)

   Una selección agrupada y ordenada de componentes disponibles.

* componentestilos

   [CQ.form.ComponentStyles](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentStyles)

* compositefield

   [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)

   Clase base para campos de formulario complejos y basados en panel que incluyen un campo de formulario o un grupo de campos de formulario.

* contenedor

   [CQ.Ext.Contenedor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)

   Clase base para cualquier [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent) que pueda contener otros componentes. Los contenedores se encargan del comportamiento básico de contener elementos, es decir, agregar, insertar y eliminar elementos.

   Las clases de Contenedor más utilizadas son [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel), [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) y [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel).

* contentfinder

   [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder)

   ContentFinder es una columna especializada de dos columnas [Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport) que contiene el Buscador de contenido real a la izquierda y el Marco de contenido a la derecha.

* contentfindertab

   [CQ.wcm.ContentFinderTab](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinderTab)

   ContentFinderTab es un panel especializado que proporciona funciones utilizadas en los paneles de fichas de [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder). Generalmente presenta un formulario de búsqueda (el Cuadro de Consulta) y una vista de datos para mostrar la búsqueda.

* cq.workflow.model.combo

   [CQ.wcm.WorkflowModelCombo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelCombo)

   WorkflowModelCombo es un [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) personalizado que muestra una lista de los modelos de flujo de trabajo disponibles.

* cq.workflow.model.selector

   [CQ.wcm.WorkflowModelSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelSelector)

   WorkflowModelSelector combina un WorkflowModelCombo con una imagen en miniatura del flujo de trabajo y botones para crear y editar modelos de flujo de trabajo.

* createsiteasistente

   [CQ.wcm.CreateSiteWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateSiteWizard)

   CreateSiteWizard es un asistente paso a paso para crear sitios (MSM).

* createversiondialog

   [CQ.wcm.CreateVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateVersionDialog)

   CreateVersionDialog es un cuadro de diálogo que permite crear una nueva versión de una página.

* custom contentpanel

   [CQ.CustomContentPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.CustomContentPanel)

   CustomContentPanel es un tipo de panel especial para su uso en [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog): Su contenido se recupera y se envía a una dirección URL diferente a los demás campos del cuadro de diálogo.

* ciclo

   [CQ.Ext.CycleButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton)

   SplitButton especializado que contiene un menú de elementos [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem). El botón se desplaza automáticamente por cada elemento de menú al hacer clic, elevando el evento [change](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) del botón (o llamando a la función [changeHandler](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) del botón, si se proporciona) para el elemento de menú activo.

* dataview

   [CQ.Ext.DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView)

   Mecanismo para mostrar datos mediante plantillas de diseño y formato personalizados. DataView utiliza una [CQ.Ext.XTemplate](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.XTemplate) como mecanismo de plantilla interna y está enlazada a [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) para que, a medida que cambian los datos del almacén, la vista se actualice automáticamente para reflejar los cambios.

* datefield

   [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField)

   Proporciona un campo de entrada de fecha con una lista desplegable [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) y validación automática de fechas.

* datemenu

   [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu)

   Menú que contiene un componente [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker).

* datepicker

   [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker)

   Selector de fecha emergente. Esta clase la utiliza la clase [DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) para permitir la exploración y selección de fechas válidas.

* datetime

   [CQ.form.DateTime](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DateTime)

   DateTime permite al usuario introducir una fecha y una hora combinando [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) y [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField).

* el cuadro de diálogo

   [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)

   El cuadro de diálogo es un tipo especial de ventana con un formulario en el cuerpo y un grupo de botones en el pie de página. Normalmente se utiliza para editar contenido, pero también para mostrar información.

* cuadro de diálogo

   [CQ.form.DialogFieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DialogFieldSet)

   DialogFieldSet es un [FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet) para su uso en [Diálogos](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* directstore

   [CQ.Ext.data.DirectStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectStore)

   Clase auxiliar pequeña para crear un [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) configurado con un [CQ.Ext.data.DirectProxy](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectProxy) y [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader) para interactuar con un [CQ.Ext.Direct](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Direct) servidor &lt;a4> a8/>Proveedor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.direct.Provider) más fácil.[

* displayfield

   [CQ.Ext.form.DisplayField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DisplayField)

   Campo de texto de solo visualización que no se valida ni se envía.

* editbar

   [CQ.wcm.EditBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar)

   La barra de edición permite al usuario editar el contenido mediante los botones de una barra.

   Aunque no aparece aquí, EditBar tiene todos los miembros de [CQ.wcm.EditBase](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBase).

* editor

   [CQ.Ext.Editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Editor)

   Campo de editor base que gestiona la visualización/ocultación bajo demanda y que tiene una lógica incorporada de tamaño y gestión de eventos.

* editorgrid

   [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)

   Esta clase amplía la [clase GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) para proporcionar la edición de celdas en las [columnas](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column) seleccionadas. Las columnas editables se especifican proporcionando un [editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel) en la [configuración de columna](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column).

* editrollover

   [CQ.wcm.EditRollover](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover)

   El botón Editar (Edit)Rótulo (Rollover) permite al usuario editar contenido mediante doble-clic y proporciona más acciones de edición a través de un menú contextual. El área editable se indica con un marco cuando el ratón se mueve sobre el contenido.

* feedimporter

   [CQ.wcm.FeedImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FeedImporter)

   FeedImporter permite al usuario importar fuentes RSS o Atom y crear páginas para cada entrada de fuente.

* field

   [CQ.Ext.form.Field](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Field)

   Clase base para los campos de formulario que proporcionan la administración de eventos, el ajuste de tamaño, la gestión de valores y otras funciones predeterminadas.

* fieldSet

   [CQ.Ext.form.FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet)

   Contenedor estándar utilizado para agrupar elementos dentro de un [formulario](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FormPanel). ...

* fileupload adialogbutton

   [CQ.form.FileUploadDialogButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadDialogButton)

   FileUploadDialogButton crea un botón que abre un nuevo cuadro de diálogo para cargar un archivo mediante FileUploadField. Se puede utilizar dentro de los cuadros de diálogo de edición en los que la carga debe realizarse en un formulario independiente.

* campo de carga de archivos

   [CQ.form.FileUploadField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadField)

   FileUploadField permite al usuario seleccionar un solo archivo para cargar.

* findreplacedialog

   [CQ.wcm.FindReplaceDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FindReplaceDialog)

   FindReplaceDialog es un cuadro de diálogo para buscar y reemplazar tokens en una página y sus páginas secundarias.

* flash

   [CQ.Ext.FlashComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.FlashComponent)

* cuadrícula

   [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)

   Esta clase representa la interfaz principal de un control de cuadrícula basado en componentes para representar datos en formato de tabla de filas y columnas.

* groupingstore

   [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)

   Implementación de almacén especializada que permite agrupar registros por uno de los campos disponibles. Esto generalmente se utiliza junto con [CQ.Ext.grid.GroupingView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GroupingView) para probar el modelo de datos de un GridPanel agrupado.

* cuadro de diálogo

   [CQ.wcm.HeavyMoveDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.HeavyMoveDialog)

   HeavyMoveDialog es un cuadro de diálogo que permite mover una página y sus páginas secundarias, teniendo en cuenta también la reactivación de páginas activadas previamente (movimiento &quot;pesado&quot;).

* oculto

   [CQ.Ext.form.Hidden](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Hidden)

   Campo oculto básico para almacenar valores ocultos en formularios que deben pasarse en el envío del formulario.

* histórybutton

   [CQ.HistoryButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.HistoryButton)

   HistoryButton es una pequeña clase auxiliar que proporciona fácilmente botones de retroceso y avance. Generalmente se requieren dos instancias relacionadas: La instancia del botón de avance es un botón sencillo vinculado a la instancia del botón de retroceso que controla el historial.

* htmleditor

   [CQ.Ext.form.HtmlEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor)

   Proporciona un componente ligero del Editor HTML. Algunas funciones de la barra de herramientas no son compatibles con Safari y se ocultarán automáticamente cuando sea necesario. Éstos se indican en las opciones de configuración cuando corresponde.

   Los botones de la barra de herramientas del editor tienen información sobre herramientas definida en la propiedad [buttonTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor).

* iframedialog

   [CQ.IframeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframeDialog)

   Cuadro de diálogo sin formato que muestra el contenido de un iframe y permite formularios en iframes.

* iframepanel

   [CQ.IframePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframePanel)

   Panel que contiene un iframe. Proporciona una creación sencilla de iframes, un evento de carga de iframe y un fácil acceso al contenido del iframe.

* inlinetextfield

   [CQ.form.InlineTextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.InlineTextField)

   InlineField es un campo de texto que se muestra como una etiqueta cuando no está activo.

* jsonstore

   [CQ.Ext.data.JsonStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonStore)

   Clase auxiliar pequeña para facilitar la creación de [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)s a partir de datos JSON. Un JsonStore se configurará automáticamente con un [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader).

* label

   [CQ.Ext.form.Label](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Label)

   Etiqueta básica.

* languageEopydialog

   [CQ.wcm.LanguageCopyDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LanguageCopyDialog)

   LanguageCopyDialog es un cuadro de diálogo para copiar árboles de idioma.

* linkchecker

   [CQ.wcm.LinkChecker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LinkChecker)

   LinkChecker es una herramienta para comprobar los vínculos externos en un sitio.

* vista de lista

   [CQ.Ext.lista.ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView)

   CQ.Ext.lista.ListView es una implementación rápida y de peso ligero de una vista similar a [Grid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel).

* livecopyproperties

   [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties)

   LiveCopyProperties proporciona un panel para la vista y edición de las propiedades de Live Copy (herencia de relaciones, desencadenado de sincronización y acciones de sincronización).

* lvbooleancolumn

   [CQ.Ext.lista.BooleanColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.BooleanColumn)

   Clase de definición de columna que procesa campos de datos booleanos. Consulte la opción de configuración [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) de [CQ.Ext.lista.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) para obtener más detalles.

* lvcolumn

   [CQ.Ext.lista.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column)

   Esta clase encapsula los datos de configuración de columna que se utilizarán en la inicialización de [ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView).

* lvdatecolumn

   [CQ.Ext.lista.DateColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn)

   Una clase de definición de columna que procesa una fecha pasada según la configuración regional predeterminada o un formato [configurado](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn). Consulte la opción de configuración [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) de [CQ.Ext.lista.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) para obtener más detalles.

* lvnumercolumn

   [CQ.Ext.lista.NumberColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn)

   Clase de definición de columna que procesa un campo de datos numérico según una cadena [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn). Consulte la opción de configuración [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) de [CQ.Ext.lista.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) para obtener más detalles.

* mediabrowsedialog

   [CQ.MediaBrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.MediaBrowseDialog)

   **Obsoleto: Utilice  [Content ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder) Finder para buscar medios.**

   MediaBrowseDialog es un cuadro de diálogo para explorar la biblioteca de medios.

* menú

   [CQ.Ext.menu.Menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Menu)

   Un objeto de menú. Este es el contenedor al que puede agregar elementos de menú. El menú también puede servir como clase base cuando se desea un menú especializado basado en otro componente (por ejemplo, [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu)).

   Los menús pueden contener [elementos de menú](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item) o [componentes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)s generales.

* menubaseitem

   [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem)

   Clase base para todos los elementos que se procesan en menús. BaseItem proporciona opciones de procesamiento predeterminadas, administración de estado activado y configuración base compartidas por todos los componentes de menú.

* menucheckitem

   [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem)

   Añade un elemento de menú que contiene una casilla de verificación de forma predeterminada, pero que también puede formar parte de un grupo de radio.

* menuitem

   [CQ.Ext.menu.Item](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)

   Una clase base para todos los elementos de menú que requieren funcionalidad relacionada con el menú (como submenús) y no son elementos de visualización estáticos. Item amplía la funcionalidad básica de [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem) agregando activación específica de menú y administración de clics.

* menuseparator

   [CQ.Ext.menu.Separator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Separator)

   Añade una barra separadora en un menú, utilizada para dividir grupos lógicos de elementos de menú. Generalmente agregará uno de estos elementos utilizando &quot;-&quot; en la llamada a add() o en la configuración de elementos en lugar de crear uno directamente.

* menutextitem

   [CQ.Ext.menu.TextItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.TextItem)

   Añade una cadena de texto estática en un menú, que se suele utilizar como encabezado o separador de grupo.

* metadata

   [CQ.dam.form.Metadata](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.form.Metadata)

   Los metadatos proporcionan un conjunto de campos para determinar la información necesaria para un campo de metadatos, tal como se utiliza, por ejemplo, en las páginas del editor de recursos.

   Proporciona los campos siguientes:

* multifield

   [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)

   MultiField es una lista editable de campos de formulario para editar propiedades de varios valores.

* mvt

   [CQ.form.MVT](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MVT)

   El componente Multivariate testing se puede utilizar para definir y editar un conjunto de imágenes que se presentan como pancartas alternativas. Las estadísticas de la tasa de pulsaciones se recopilan por titular.

* notificationinbox

   [CQ.wcm.NotificationInbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.NotificationInbox)

   NotificationInbox permite al usuario suscribirse a acciones de WCM y administrar notificaciones.

* campo numérico

   [CQ.Ext.form.NumberField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.NumberField)

   Campo de texto numérico que proporciona filtrado automático de pulsaciones de teclas y validación numérica.

* offlineimporter

   [CQ.wcm.OfflineImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.OfflineImporter)

   OfflineImporter es una herramienta para importar y convertir documentos de Microsoft Word en páginas AEM. Esta función permite editar el contenido sin conexión mediante un procesador de textos.

* ownerdraw

   [CQ.form.OwnerDraw](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.OwnerDraw)

   OwnerDraw puede contener código HTML personalizado (introducido directamente o recuperado de una URL).

* paginación

   [CQ.Ext.PagingToolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.PagingToolbar)

   A medida que aumenta la cantidad de registros, aumenta el tiempo necesario para que el explorador los procese. La paginación se utiliza para reducir la cantidad de datos intercambiados con el cliente.

* panel

   [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel)

   El panel es un contenedor que tiene una funcionalidad específica y componentes estructurales que lo convierten en el bloque de creación perfecto para interfaces de usuario orientadas a la aplicación.

   Los paneles son, en virtud de su herencia de [CQ.Ext.Contenedor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container).

* referencias de párrafo

   [CQ.form.ParagraphReference](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ParagraphReference)

   El campo de referencia de párrafo permite examinar páginas y seleccionar uno de sus párrafos. Consiste en un campo desencadenador y un cuadro de diálogo de exploración de párrafo asociado.

* password

   [CQ.form.Password](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Password)

   La contraseña es similar a [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) pero mantiene su valor como privado, lo que permite a los usuarios introducir datos confidenciales.

* pathcompletion

   [CQ.form.PathCompletion](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathCompletion)

   **Obsoleto: Utilice  [CQ.form.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) PathField en su lugar**

* pathfield

   [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)

   PathField es un campo de entrada diseñado para rutas con finalización de ruta y un botón para abrir un [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog) para explorar el repositorio del servidor. También puede examinar párrafos de página para generar vínculos avanzados.

* progreso

   [CQ.Ext.ProgressBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)

   Un componente de barra de progreso que se puede actualizar. La barra de progreso admite dos modos diferentes: manual y automático.

   En modo manual, usted es responsable de mostrar, actualizar (a través de [updateProgress](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)) y borrar la barra de progreso según sea necesario de su propio código. Este método es más adecuado cuando desea mostrar el progreso.

* propertygrid

   [CQ.Ext.grid.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyGrid)

   Una implementación de red especializada destinada a imitar la cuadrícula de propiedades tradicional como se suele ver en los IDE de desarrollo. Cada fila de la cuadrícula representa una propiedad de algún objeto y los datos se almacenan como un conjunto de pares nombre/valor en [CQ.Ext.grid.PropertyRecord](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyRecord)s.

* propgrid

   [CQ.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.PropertyGrid)

   PropertyGrid es una cuadrícula genérica que se utiliza para mostrar y editar propiedades de objetos.

* rápido

   [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip)

   @xtype quicktip Clase de información sobre herramientas especializada para información sobre herramientas que se puede especificar en el marcado y administrar automáticamente mediante la instancia global [CQ.Ext.QuickTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTips). Consulte el encabezado de la clase QuickTips para obtener más detalles y ejemplos de uso.

* radio

   [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio)

   Campo de radio único. Igual que la casilla de verificación, pero se proporciona como una comodidad para configurar automáticamente el tipo de entrada. El explorador administra automáticamente la agrupación de radio si se asigna el mismo nombre a cada radio de un grupo.

* radiogroup

   [CQ.Ext.form.RadioGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.RadioGroup)

   Un contenedor de agrupación para controles [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio).

* cuadro de diálogo de referencias

   [CQ.wcm.ReferencesDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ReferencesDialog)

   El cuadro de diálogo Referencias es un cuadro de diálogo para mostrar referencias en una página.

* restoretreedialog

   [CQ.wcm.RestoreTreeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreTreeDialog)

   RestoreTreeDialog es un cuadro de diálogo para restaurar una versión anterior de un árbol.

* restoreversiondialog

   [CQ.wcm.RestoreVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreVersionDialog)

   RestoreVersionDialog es un cuadro de diálogo para restaurar una versión anterior de una página.

* richtext

   [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText)

   RichText proporciona un campo de formulario para editar información de texto con estilo (texto enriquecido).

   El componente RichText proporciona actualmente las siguientes funciones:

* plan de implementación

   [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan)

   El RolloutPlan proporciona un cuadro de diálogo para observar el progreso de la implementación de una página. RolloutPlan se inicia con un [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard).

* rolloutasistente

   [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard)

   El Asistente para despliegue proporciona un asistente para desplegar una página. RolloutWizard inicio un [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan).

* searchfield

   [CQ.form.SearchField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SearchField)

   SearchField proporciona un campo de búsqueda que proporciona los resultados en una lista desplegable que puede utilizarse para buscar en el repositorio.

* selección

   [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection)

   La selección permite al usuario elegir entre varias opciones. Las opciones pueden formar parte de la configuración o cargarse desde una respuesta JSON. La selección se puede procesar como desplegable (seleccionar) o como un cuadro combinado (seleccionar más entrada de texto libre).

* barra de tareas

   [CQ.wcm.Sidekick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Sidekick)

   La barra de tareas es un asistente flotante que proporciona al usuario herramientas comunes para la edición de páginas.

* siteadmin

   [CQ.wcm.SiteAdmin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin)

   SiteAdmin es una consola que proporciona funciones de administración de WCM.

* siteimporter

   [CQ.wcm.SiteImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteImporter)

   SiteImporter permite al usuario importar sitios web completos y crear proyectos iniciales.

* sizefield

   [CQ.form.SizeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SizeField)

   SizeField permite al usuario introducir la anchura y la altura (por ejemplo, para una imagen).

* regulador

   [CQ.Ext.Slider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Slider)

   Control deslizante que admite orientación vertical u horizontal, ajustes de teclado, ajuste configurable, clic en el eje y animación. Se puede agregar como un elemento a cualquier contenedor. Ejemplo de uso: ...

* presentación

   [CQ.form.Slideshow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Slideshow)

   La proyección de diapositivas proporciona un componente que se puede utilizar para definir y editar un conjunto de imágenes y títulos de imágenes que se pueden ver como una proyección de diapositivas.

   El componente Presentación de diapositivas se basa en el componente [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage).

* smartfile

   [CQ.form.SmartFile](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartFile)

   SmartFile es un cargador de archivos inteligente.

   Si hay un complemento de Flash (versión >= 9) instalado, las cargas se ejecutan mediante la biblioteca de carga SWF, que proporciona una forma cómoda de gestionar las cargas.

* smartimage

   [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage)

   SmartImage es un cargador de imágenes inteligente. Proporciona herramientas para procesar una imagen cargada, por ejemplo, una herramienta para definir mapas de imagen y un recorte de imagen.

   Tenga en cuenta que el componente está diseñado principalmente para utilizarse en una ficha de diálogo independiente.

* espaciador

   [CQ.Ext.Spacer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Spacer)

   Se utiliza para proporcionar un espacio considerable en un diseño.

* spinner

   [CQ.form.Spinner](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Spinner)

   El Giro es un campo desencadenador para valores numéricos, de fecha o de hora. El valor se puede aumentar y reducir mediante los activadores de dirección, la rueda de desplazamiento o las teclas proporcionados.

* divitbutton

   [CQ.Ext.SplitButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.SplitButton)

   Botón dividido que proporciona una flecha desplegable integrada que puede activar un evento por separado del evento de clic predeterminado del botón. Generalmente esto se utilizaría para mostrar un menú desplegable que proporciona opciones adicionales a la acción del botón principal, pero cualquier controlador personalizado puede proporcionar la implementación de arrowclick.

* static

   [CQ.Static](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Static)

   El Static puede utilizarse para mostrar texto arbitrario o HTML.

* estadísticas

   [CQ.wcm.Statistics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Statistics)

   Las estadísticas muestran las impresiones de página como un gráfico. La utilidad permite seleccionar un período, las estadísticas deben mostrarse.

* store

   [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)

   La clase Store encapsula una caché del lado del cliente de [objetos Record](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Record) que proporcionan datos de entrada para Componentes como [GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel), el [ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) o el [DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView).

* sugerestfield

   [CQ.form.Suggesfield](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SuggestField)

   Suggetfield proporciona al usuario sugerencias basadas en su entrada.

* conmutador

   [CQ.Switcher](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Switcher)

   El conmutador proporciona un grupo de botones para la barra de encabezado de una consola para cambiar entre sitios web, recursos digitales, herramientas, flujo de trabajo y seguridad.

* tableedit

   [CQ.form.TableEdit](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit)

   **Obsoleto: Utilice  [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2) .**

* tableedit2

   [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2)

   TableEdit2 proporciona una utilidad para crear tablas.

* tabpanel

   [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel)

   Un contenedor de tabulación básico. TabPanels se puede utilizar exactamente como un [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel) estándar para propósitos de diseño, pero también tienen compatibilidad especial para contener componentes secundarios ([`items`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)).

* etiquetas

   [CQ.tagging.TagInputField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tagging.TagInputField)

   ```
   CQ.tagging.TagInputField
   ```

   es un widget de formulario para introducir etiquetas. Tiene un menú emergente para seleccionar etiquetas existentes, incluye la finalización automática y muchas otras funciones.

* textarea

   [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea)

   Campo de texto multilínea. Se puede utilizar como reemplazo directo de los campos de área de texto tradicionales, además de añadir compatibilidad con el ajuste automático de tamaño.

* textbutton

   [CQ.TextButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.TextButton)

   TextButton proporciona un vínculo de texto con las capacidades de [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button).

* textfield

   [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)

   Campo de texto básico. Se puede utilizar como reemplazo directo de entradas de texto tradicionales o como clase base para controles de entrada más sofisticados (como [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea) y [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)).

* thumbnail

   [CQ.form.Thumbnail](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Thumbnail)

* timefield

   [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField)

   Proporciona un campo de entrada de tiempo con una lista desplegable de tiempo y validación automática de tiempo. Ejemplo de uso: ...

* tip

   [CQ.Ext.Tip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tip)

   @xtype sugerencia Esta es la clase base para [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip) y [CQ.Ext.Tooltip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tooltip) que proporciona el diseño y la posición básicos que requieren todas las clases basadas en sugerencias. Esta clase se puede utilizar directamente para sugerencias sencillas con posición estática.

* titleseparator

   [CQ.menu.TitleSeparator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.menu.TitleSeparator)

   Añade una barra separadora en un menú, utilizada para dividir grupos lógicos de elementos de menú. El separador puede además llevar un título.

* toolbar

   [CQ.Ext.Toolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Toolbar)

   Clase de barra de herramientas básica. Aunque [`defaultType`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) para la barra de herramientas es [`button`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button), los elementos de la barra de herramientas (elementos secundarios para el contenedor de la barra de herramientas) pueden ser prácticamente cualquier tipo de componente. Los elementos de la barra de herramientas se pueden crear explícitamente mediante sus constructores.

* tooltip

   [CQ.Ext.ToolTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ToolTip)

   Implementación de información de objeto estándar para proporcionar información adicional al pasar el ratón sobre un elemento de destinatario. @xtype tooltip.

* treegrid

   [CQ.tree.TreeGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tree.TreeGrid)

   @xtype treegrid

* treepanel

   [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)

   El panel Árbol proporciona una representación de interfaz de usuario estructurada en árbol de datos estructurados en árbol.

   [Los ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode)TreeNodes añadidos al TreePanel pueden contener cada uno de ellos metadatos utilizados por la aplicación en su propiedad  [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode) attribute.

* activar

   [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)

   Proporciona un envoltorio práctico para TextFields que agrega un botón desencadenador en el que se puede hacer clic (de forma predeterminada, parece un cuadro combinado). El activador no tiene ninguna acción predeterminada, por lo que debe asignar una función para implementar el controlador de clics del desencadenador anulando [onTriggerClick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField). Puede crear un TriggerField directamente, ya que se representa exactamente como un cuadro combinado.

* upload addialog

   [CQ.UploadDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UploadDialog)

   UploadDialog permite al usuario cargar archivos en el repositorio. Crea un nuevo UploadDialog.

* userinfo

   [CQ.UserInfo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UserInfo)

   Elemento de la barra de herramientas para mostrar el nombre de usuario actual y permitir acciones de usuario como editar propiedades de usuario y suplantación.

* viewport

   [CQ.Ext.Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport)

   Un contenedor especializado que representa el área de la aplicación visible (la ventanilla móvil).

   La ventanilla se procesa a sí misma en el cuerpo del documento, se ajusta automáticamente al tamaño de la ventanilla del navegador y gestiona el cambio de tamaño de la ventana. Solo puede haber una ventanilla.

* ventana

   [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)

   Panel especializado que se utilizará como ventana de la aplicación. Las ventanas están flotadas, [ajustables](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) y [arrastrables](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) de forma predeterminada. Windows puede [maximizarse](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) para llenar la ventanilla, restaurarse a su tamaño anterior y [minimizar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)d.

* xmlstore

   [CQ.Ext.data.XmlStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlStore)

   Clase auxiliar pequeña para facilitar la creación de [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)s a partir de datos XML. Un XmlStore se configurará automáticamente con un [CQ.Ext.data.XmlReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlReader).

   **** cqincludePseudo xtype que incluye definiciones de utilidades de una ruta diferente en el repositorio. Se utiliza con mayor frecuencia en los cuadros de diálogo de página. No hay ninguna clase de widget de JavaScript para este tipo de expresiones. La función formatData() de la clase CQ.Util la procesa. Para obtener más información, consulte este artículo de la base de conocimientos.
