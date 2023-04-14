---
title: Uso y ampliación de utilidades (IU clásica)
description: La interfaz basada en la web de Adobe Experience Manager utiliza AJAX y otras tecnologías modernas de navegador para permitir a los autores editar y formatear el contenido WYSIWYG directamente en la página web
uuid: eb3da415-cbef-4766-a28e-837e238a4156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 7b234f1f-4470-4de1-a3c3-ab19e5e001ad
docset: aem65
exl-id: 56a9591c-cd78-42e8-a5d7-6b48581d6af6
source-git-commit: af60428255fb883265ade7b2d9f363aacb84b9ad
workflow-type: tm+mt
source-wordcount: '4926'
ht-degree: 0%

---

# Uso y ampliación de utilidades (IU clásica){#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>Esta página describe el uso de las utilidades dentro de la IU clásica, que quedó obsoleta en la AEM 6.4.
>
>El Adobe recomienda utilizar el [IU táctil](/help/sites-developing/touch-ui-concepts.md) basado en [Interfaz de usuario de Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui) y [Interfaz de usuario de Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

La interfaz basada en web (AEM) de Adobe Experience Manager utiliza AJAX y otras tecnologías modernas de navegador para permitir a los autores editar y dar formato al contenido WYSIWYG directamente en la página web.

AEM usa la variable [ExtJS](https://www.sencha.com/) biblioteca de widgets, que proporciona los elementos de interfaz de usuario altamente pulidos que funcionan en todos los exploradores más importantes y permiten la creación de experiencias de IU de escritorio.

Estos widgets se incluyen en AEM y, además de ser utilizados por AEM mismo, pueden ser utilizados por cualquier sitio web creado con AEM.

Para obtener una referencia completa de todos los widgets disponibles en AEM, consulte la [documentación de la API del widget](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) o [lista de xtype existentes](/help/sites-developing/xtypes.md). Además, hay muchos ejemplos que muestran cómo utilizar el marco de ExtJS disponibles en el [Sencha](https://examples.sencha.com/extjs/7.6.0/) sitio, el propietario de la infraestructura.

Esta página proporciona información sobre cómo utilizar y ampliar las utilidades. En primer lugar, se describe cómo [incluir código de cliente en una página](#including-the-client-sided-code-in-a-page). A continuación, se describen algunos componentes de muestra que se han creado para ilustrar el uso básico y la extensión. Estos componentes están disponibles en la **Uso de las utilidades de ExtJS** paquete en **Uso compartido de paquetes**.

El paquete incluye ejemplos de:

* [Diálogos básicos](#basic-dialogs) creado con utilidades integradas.
* [Diálogos dinámicos](#dynamic-dialogs) se ha creado con utilidades integradas y lógica personalizada de JavaScript.
* Cuadros de diálogo basados en [widgets personalizados](#custom-widgets).
* A [panel de árbol](#tree-overview) mostrar un árbol JCR debajo de una ruta determinada.
* A [panel cuadrícula](#grid-overview) visualización de datos en formato de tabla.

>[!NOTE]
>
>La IU clásica de Adobe Experience Manager se basa en [ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/).

## Inclusión del código de cliente en una página {#including-the-client-sided-code-in-a-page}

JavaScript del lado del cliente y el código de hoja de estilo deben colocarse en una biblioteca de cliente.

Para crear una biblioteca de cliente:

1. Cree un nodo a continuación `/apps/<project>` con las siguientes propiedades:

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[mezcla:bloqueable]&quot;
   * jcr:primaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * categories=&quot;[&lt;category-name>]&quot;
   * dependencias=&quot;[cq.widgets]&quot;

   `Note: <category-name> is the name of the custom library (e.g. "cq.extjstraining") and is used to include the library on the page.`

1. Abajo `clientlib` cree el `css` y `js` carpetas (nt:folder).

1. Abajo `clientlib` cree el `css.txt` y `js.txt` archivos (nt:files). Estos archivos .txt enumeran los archivos que se incluyen en la biblioteca.

1. Editar `js.txt`: debe comenzar con &#39; `#base=js`&#39; seguido de la lista de los archivos agregados por el servicio de biblioteca del cliente de CQ, por ejemplo:

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. Editar `css.txt`: debe comenzar con &#39; `#base=css`&#39; seguido de la lista de los archivos agregados por el servicio de biblioteca del cliente de CQ, por ejemplo:

   ```
   #base=css
    components.css
   ```

1. Debajo de `js` , coloque los archivos JavaScript que pertenecen a la biblioteca.

1. Debajo de `css` carpeta, coloque la variable `.css` y los recursos utilizados por los archivos css (por ejemplo, `my_icon.png`).

>[!NOTE]
>
>El manejo de las hojas de estilo descritas anteriormente es opcional.

Para incluir la biblioteca del cliente en el componente de página jsp:

* para incluir tanto el código JavaScript como las hojas de estilo:
   `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
donde 
`<category-nameX>` es el nombre de la biblioteca del lado del cliente.

* para incluir solo código JavaScript:
   `<ui:includeClientLib js="<category-name>"/>`

Para obtener más información, consulte la descripción del [&lt;ui:includeclientlib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib) etiqueta.

A veces, una biblioteca de cliente solo debería estar disponible en modo de autor y excluirse en modo de publicación. Puede lograrse de la siguiente manera:

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### Introducción a los ejemplos {#getting-started-with-the-samples}

Para seguir los tutoriales de esta página, instale el paquete **Uso de las utilidades de ExtJS** en una instancia de AEM local y cree una página de muestra en la que se incluyan los componentes. Para ello, haga lo siguiente:

1. En la instancia de AEM, descargue el paquete llamado **Uso de utilidades de ExtJS (v01)** desde Package Share e instale el paquete. Crea el proyecto `extjstraining` below `/apps` en el repositorio.
1. Incluya la biblioteca de cliente que contiene las secuencias de comandos (js) y la hoja de estilo (css) en la etiqueta head de la página jsp de Geometrixx. Incluirá los componentes de muestra en una nueva página del **Geometrixx** rama: en **CRXDE Lite** abra el archivo `/apps/geometrixx/components/page/headlibs.jsp` y añada `cq.extjstraining` a la `<ui:includeClientLib>` de la siguiente manera:
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. Cree una página en el **Geometrixx** rama inferior `/content/geometrixx/en/products` y llamémoslo **Uso de las utilidades de ExtJS**.
1. Vaya al modo de diseño y añada todos los componentes del grupo llamado **Uso de las utilidades de ExtJS** al diseño de la Geometrixx
1. Vuelva al modo de edición: los componentes del grupo **Uso de las utilidades de ExtJS** están disponibles en la barra de tareas.

>[!NOTE]
>
>Los ejemplos de esta página se basan en el contenido de muestra de Geometrixx, que ya no se envía con AEM, y que ha sido reemplazado por We.Retail. Consulte la [Implementación de referencia de We.Retail](/help/sites-developing/we-retail.md#we-retail-geometrixx) para obtener información sobre cómo descargar e instalar Geometrixx.

### Cuadros de diálogo básicos {#basic-dialogs}

Los cuadros de diálogo suelen utilizarse para editar contenido, pero también pueden mostrar información. Una manera fácil de ver un cuadro de diálogo completo es acceder a su representación en formato json. Para ello, dirija el navegador a:

`https://localhost:4502/<path-to-dialog>.-1.json`

El primer componente de la variable **Uso de las utilidades de ExtJS** en la barra de tareas se llama **1. Conceptos básicos del cuadro de diálogo** e incluye cuatro cuadros de diálogo básicos creados con utilidades integradas y sin lógica JavaScript personalizada. Los cuadros de diálogo se almacenan a continuación `/apps/extjstraining/components/dialogbasics`. Los diálogos básicos son:

* el cuadro de diálogo Completo ( `full` nodo): muestra una ventana con tres pestañas, cada una con dos campos de texto.
* el cuadro de diálogo Panel único( `singlepanel` nodo): muestra una ventana con una ficha que tiene dos campos de texto.
* el cuadro de diálogo Panel múltiple( `multipanel` nodo): su visualización es la misma que el cuadro de diálogo Completo pero está diseñada de forma diferente.
* Cuadro de diálogo Diseño( `design` nodo): muestra una ventana con dos pestañas. La primera ficha tiene un campo de texto, un menú desplegable y un área de texto contraíble. La segunda ficha tiene un conjunto de campos con cuatro campos de texto y un conjunto de campos contraíble con dos campos de texto.

Incluya la variable **1. Conceptos básicos del cuadro de diálogo** en la página de muestra:

1. Agregue la variable **1. Conceptos básicos del cuadro de diálogo** a la página de muestra desde el **Uso de las utilidades de ExtJS** en la ficha **Barra de tareas**.
1. El componente muestra un título, texto y un **PROPIEDADES** vínculo. Al seleccionar el vínculo, se muestran las propiedades del párrafo almacenado en el repositorio. Vuelva a seleccionar el vínculo para ocultar las propiedades.

El componente se muestra de la siguiente manera:

![imagen_1-60](assets/chlimage_1-60.png)

#### Ejemplo 1: Diálogo completo {#example-full-dialog}

La variable **Completa** muestra una ventana con tres pestañas, cada una con dos campos de texto. Es el cuadro de diálogo predeterminado de la variable **Conceptos básicos del cuadro de diálogo** componente. Sus características son:

* Está definido por un nodo: tipo de nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`.
* Muestra tres pestañas (tipo de nodo = `cq:Panel`).
* Cada ficha tiene dos campos de texto (tipo de nodo = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* Se define mediante el nodo :
   `/apps/extjstraining/components/dialogbasics/full`
* Se procesa en formato JSON solicitando:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

El cuadro de diálogo se muestra de la siguiente manera:

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### Ejemplo 2: Cuadro de diálogo de panel único {#example-single-panel-dialog}

La variable **Panel único** muestra una ventana con una ficha que tiene dos campos de texto. Sus características son:

* Muestra una ficha (tipo de nodo = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)
* La pestaña tiene dos campos de texto (tipo de nodo = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)
* Se define mediante el nodo :
   `/apps/extjstraining/components/dialogbasics/singlepanel`
* Se procesa en formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* Una ventaja sobre **Diálogo completo** es que se necesita menos configuración.
* Uso recomendado: para cuadros de diálogo simples que muestran información o que solo tienen unos pocos campos.

Para utilizar el cuadro de diálogo Panel único:

1. Reemplace el cuadro de diálogo del **Conceptos básicos del cuadro de diálogo** con el **Panel único** diálogo:
   1. En **CRXDE Lite**, elimine el nodo : `/apps/extjstraining/components/dialogbasics/dialog`
   1. Haga clic en **Guardar todo** para guardar los cambios.
   1. Copie el nodo : `/apps/extjstraining/components/dialogbasics/singlepanel`
   1. Pegue el nodo copiado a continuación: `/apps/extjstraining/components/dialogbasics`
   1. Seleccione el nodo : `/apps/extjstraining/components/dialogbasics/Copy of singlepanel`y renómbrelo `dialog`.
1. Edite el componente: el cuadro de diálogo se muestra de la siguiente manera:

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### Ejemplo 3: Diálogo de varios paneles {#example-multi-panel-dialog}

La variable **Varios paneles** tiene la misma visualización que la **Completa** pero se crea de forma diferente. Sus características son:

* Está definido por un nodo (tipo de nodo = `cq:Dialog`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`).
* Muestra tres pestañas (tipo de nodo = `cq:Panel`).
* Cada ficha tiene dos campos de texto (tipo de nodo = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* Se define mediante el nodo :
   `/apps/extjstraining/components/dialogbasics/multipanel`
* Se procesa en formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* Una ventaja sobre **Diálogo completo** es que tiene una estructura simplificada.
* Uso recomendado: para los cuadros de diálogo multipestaña.

Para utilizar el cuadro de diálogo Panel múltiple:

1. Reemplace el cuadro de diálogo del **Conceptos básicos del cuadro de diálogo** con el **Varios paneles** diálogo: siga los pasos descritos para la variable [Ejemplo 2: Cuadro de diálogo de panel único](#example-single-panel-dialog)
1. Edite el componente: el cuadro de diálogo se muestra de la siguiente manera:

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### Ejemplo 4: Diálogo enriquecido {#example-rich-dialog}

La variable **Enriquecido** muestra una ventana con dos pestañas. La primera ficha tiene un campo de texto, un menú desplegable y un área de texto contraíble. La segunda ficha tiene un conjunto de campos con cuatro campos de texto y un conjunto de campos contraíble con dos campos de texto. Sus características son:

* Está definido por un nodo (tipo de nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Muestra dos pestañas (tipo de nodo = `cq:Panel`).
* La primera pestaña tiene un ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` widget con un ` [textfield](/help/sites-developing/xtypes.md#textfield)` y ` [selection](/help/sites-developing/xtypes.md#selection)` utilidad con tres opciones y contraíble ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` con un ` [textarea](/help/sites-developing/xtypes.md#textarea)` para abrir el Navegador.
* La segunda pestaña tiene un ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` widget con cuatro ` [textfield](/help/sites-developing/xtypes.md#textfield)` widgets y un contraíble `dialogfieldset` con dos ` [textfield](/help/sites-developing/xtypes.md#textfield)` widgets.
* Se define mediante el nodo :
   `/apps/extjstraining/components/dialogbasics/rich`
* Se procesa en formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

Para usar la variable **Enriquecido** diálogo:

1. Reemplace el cuadro de diálogo del **Conceptos básicos del cuadro de diálogo** con el **Enriquecido** diálogo: siga los pasos descritos para la variable [Ejemplo 2: Cuadro de diálogo de panel único](#example-single-panel-dialog)
1. Edite el componente: el cuadro de diálogo se muestra de la siguiente manera:

![screen_shot_2012-01-31at50429pm](assets/screen_shot_2012-01-31at50429pm.png) ![screen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### Cuadros de diálogo dinámicos {#dynamic-dialogs}

El segundo componente de la variable **Uso de las utilidades de ExtJS** en la barra de tareas se llama **2. Cuadros de diálogo dinámicos** e incluye tres cuadros de diálogo dinámicos que se crean con utilidades integradas y **con lógica personalizada de JavaScript**. Los cuadros de diálogo se almacenan a continuación `/apps/extjstraining/components/dynamicdialogs`. Los cuadros de diálogo dinámicos son:

* el cuadro de diálogo Cambiar fichas ( `switchtabs` nodo): muestra una ventana con dos pestañas. La primera pestaña tiene una selección de radio con tres opciones: cuando se selecciona una opción, se muestra una pestaña relacionada con la opción. La segunda ficha tiene dos campos de texto.
* el cuadro de diálogo Arbitrario ( `arbitrary` nodo): muestra una ventana con una pestaña. La pestaña tiene un campo para soltar o cargar un recurso y un campo que muestra información sobre la página contenedora y sobre el recurso si se hace referencia a uno.
* el cuadro de diálogo Alternar campos ( `togglefield` nodo): muestra una ventana con una pestaña. La pestaña tiene una casilla de verificación: cuando se marca, se muestra un conjunto de campos con dos campos de texto.

Para incluir el **2. Cuadros de diálogo dinámicos** en la página de muestra:

1. Agregue la variable **2. Cuadros de diálogo dinámicos** a la página de muestra desde el **Uso de las utilidades de ExtJS** en la ficha **Barra de tareas**.
1. El componente muestra un título, texto y un **PROPIEDADES** vínculo. Al seleccionar el vínculo, se muestran las propiedades del párrafo almacenado en el repositorio. Vuelva a seleccionar el vínculo para ocultar las propiedades.

El componente se muestra de la siguiente manera:

![climage_1-61](assets/chlimage_1-61.png)

#### Ejemplo 1: Cuadro de diálogo Cambiar fichas {#example-switch-tabs-dialog}

La variable **Cambiar fichas** muestra una ventana con dos pestañas. La primera pestaña tiene una selección de radio con tres opciones: cuando se selecciona una opción, se muestra una pestaña relacionada con la opción. La segunda ficha tiene dos campos de texto.

Sus principales características son:

* Está definido por un nodo (tipo de nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Muestra dos pestañas (tipo de nodo = `cq:Panel`): una pestaña de selección, la segunda pestaña depende de la selección de la primera pestaña (tres opciones).
* Tiene tres pestañas opcionales (tipo de nodo = `cq:Panel`), cada uno tiene dos campos de texto (tipo de nodo = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`). Solo se muestra una pestaña opcional a la vez.
* Se define mediante la variable `switchtabs` en:
   `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* Se procesa en formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

La lógica se implementa mediante detectores de eventos y código JavaScript de la siguiente manera:

* El nodo de diálogo tiene un &quot; `beforeshow`&quot; oyente que oculta todas las pestañas opcionales antes de que se muestre el cuadro de diálogo:
   `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`

   `dialog.items.get(0)` obtiene la variable `tabpanel` que contiene el panel de selección y los tres paneles opcionales.
* La variable `Ejst.x2` se define en la variable `exercises.js` en:
   `/apps/extjstraining/clientlib/js/exercises.js`
* En el `Ejst.x2.manageTabs()` como el valor de `index` es -1, todas las pestañas opcionales están ocultas (i va del 1 al 3).
* La pestaña de selección tiene dos oyentes: uno que muestra la ficha seleccionada cuando se carga el cuadro de diálogo (&quot; `loadcontent`&quot;) y una que muestre la ficha seleccionada cuando se cambia la selección (&quot; `selectionchanged`&quot;):
   `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* Para la variable `Ejst.x2.showTab()` método,
   `field.findParentByType('tabpanel')` obtiene la variable `tabpanel` que contiene todas las pestañas ( `field` representa el widget de selección)
   `field.getValue()` obtiene el valor de la selección, por ejemplo, tab2
   `Ejst.x2.manageTabs()` muestra la ficha seleccionada.
* Cada ficha opcional tiene un oyente que oculta la pestaña en &quot; `render`&quot; evento:
   `render="function(tab){Ejst.x2.hideTab(tab);}"`
* Para la variable `Ejst.x2.hideTab()` método,
   `tabPanel` es la variable `tabpanel` que contiene todas las pestañas
   `index` es el índice de la pestaña opcional
   `tabPanel.hideTabStripItem(index)` oculta la pestaña

Se muestra de la siguiente manera:

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### Ejemplo 2: Diálogo arbitrario {#example-arbitrary-dialog}

A menudo, un cuadro de diálogo muestra el contenido del componente subyacente. El diálogo descrito aquí, llamado **Arbitrario** , extrae contenido de un componente diferente.

La variable **Arbitrario** muestra una ventana con una ficha. La pestaña tiene dos campos: una para soltar o cargar un recurso y otra que muestre información sobre la página contenedora y sobre el recurso si se ha hecho referencia a uno.

Sus principales características son:

* Está definido por un nodo (tipo de nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Muestra una `tabpanel` widget (tipo de nodo = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) con un panel (tipo de nodo = `cq:Panel`)
* El panel tiene un widget de archivos inteligentes (tipo de nodo = `cq:Widget`, xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`) y un widget de dibujo del propietario (tipo de nodo = `cq:Widget`, xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`)
* Se define mediante la variable `arbitrary` en:
   `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* Se procesa en formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

La lógica se implementa mediante detectores de eventos y código JavaScript de la siguiente manera:

* La variable `ownerdraw` La utilidad tiene un &quot; `loadcontent`&quot; oyente que muestra información sobre la página que contiene el componente. Es decir, el recurso al que hace referencia el widget de archivos inteligentes cuando se carga el contenido:
   `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`

   `field` se configura con la variable `ownerdraw` object
   `path` se configura con la ruta de contenido del componente (por ejemplo, `/content/geometrixx/en/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs`)
* La variable `Ejst.x2` se define en la variable `exercises.js` en:
   `/apps/extjstraining/clientlib/js/exercises.js`
* Para la variable `Ejst.x2.showInfo()` método,
   `pagePath` es la ruta de la página que contiene el componente;
   `pageInfo` representa las propiedades de página en formato json;
   `reference` es la ruta del recurso al que se hace referencia;
   `metadata` representa los metadatos del recurso en formato json;
   `ownerdraw.getEl().update(html);` muestra el html creado en el cuadro de diálogo

Para usar la variable **Arbitrario** diálogo:

1. Reemplace el cuadro de diálogo del **Diálogo dinámico** con el **Arbitrario** diálogo: siga los pasos descritos para la variable [Ejemplo 2: Cuadro de diálogo de panel único](#example-single-panel-dialog)
1. Edit the component: the dialog displays as follows:

![](assets/screen_shot_2012-02-01at115300am.png)

#### Example 3: Toggle Fields Dialog {#example-toggle-fields-dialog}

La variable **Alternar campos** muestra una ventana con una ficha. La pestaña tiene una casilla de verificación: cuando se marca, se muestra un conjunto de campos con dos campos de texto.

Sus principales características son:

* Está definido por un nodo (tipo de nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Muestra una `tabpanel` widget (tipo de nodo = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`) con un panel (tipo de nodo = `cq:Panel`).
* El panel tiene un widget de selección/casilla de verificación (tipo de nodo = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, tipo = ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`) y un widget de conjunto de cuadros de diálogo contraíble (tipo de nodo = `cq:Widget`, xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`) que está oculto de forma predeterminada, con dos widgets de campo de texto (tipo de nodo = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* Se define mediante la variable `togglefields` en:
   `/apps/extjstraining/components/dynamicdialogs/togglefields`
* Se procesa en formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

La lógica se implementa mediante detectores de eventos y código JavaScript de la siguiente manera:

* la pestaña selección tiene dos oyentes: uno que muestra el conjunto de campos de diálogo cuando se carga el contenido (&quot; `loadcontent`&quot;) y una que muestre el conjunto de campos de diálogo cuando se cambia la selección (&quot; `selectionchanged`&quot;):
   `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* La variable `Ejst.x2` se define en la variable `exercises.js` en:
   `/apps/extjstraining/clientlib/js/exercises.js`
* Para la variable `Ejst.x2.toggleFieldSet()` método,
   `box` es el objeto de selección;
   `panel` es el panel que contiene la selección y los widgets dialogfieldset;
   `fieldSet` es el objeto dialogfieldset;
   `show` es el valor de la selección (true o false); basado en &#39; `show`&#39; el cuadro de diálogo se muestra o no

Para usar la variable **Alternar campos** , haga lo siguiente:

1. Reemplace el cuadro de diálogo del **Diálogo dinámico** con el **Alternar campos** diálogo: siga los pasos descritos para la variable [Ejemplo 2: Cuadro de diálogo de panel único](#example-single-panel-dialog)
1. Edite el componente: el cuadro de diálogo se muestra de la siguiente manera:

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### Widgets personalizados {#custom-widgets}

Los widgets listos para usar que se incluyen con AEM deben cubrir la mayoría de los casos de uso. Sin embargo, a veces puede ser necesario crear un widget personalizado para cubrir un requisito específico del proyecto. Los widgets personalizados se pueden crear ampliando los existentes. Para ayudarle a empezar con esta personalización, la variable **`Using ExtJS Widgets`** incluye tres cuadros de diálogo que utilizan tres widgets personalizados diferentes:

* el cuadro de diálogo Campos múltiples ( `multifield` ) muestra una ventana con una pestaña. La pestaña tiene un widget de varios campos personalizado que tiene dos campos: un menú desplegable con dos opciones y un campo de texto. Ya que se basa en la configuración predeterminada `multifield` (que solo tiene un campo de texto), tiene todas las características de la `multifield` para abrir el Navegador.
* el cuadro de diálogo Examinar árbol ( `treebrowse` ) muestra una ventana con una ficha que contiene un widget de exploración de rutas: al hacer clic en la flecha, se abre una ventana en la que puede examinar una jerarquía y seleccionar un elemento. A continuación, la ruta del elemento se agrega al campo de ruta y se mantiene cuando se cierra el cuadro de diálogo.
* un cuadro de diálogo basado en el complemento Editor de texto enriquecido ( `rteplugin` ) que agrega un botón personalizado al Editor de texto enriquecido para insertar texto personalizado en el texto principal. Consiste en un `richtext` y de una función personalizada que se agrega a través del mecanismo de complementos RTE.

Los widgets personalizados y el complemento se incluyen en el componente llamado **3. Widgets personalizados** del **Uso de las utilidades de ExtJS** paquete. Para incluir este componente en la página de muestra:

1. Agregue la variable **3. Widgets personalizados** a la página de muestra desde el **Uso de las utilidades de ExtJS** en la ficha **Barra de tareas**.
1. El componente muestra un título, texto y, al hacer clic en el botón **PROPIEDADES** , las propiedades del párrafo almacenadas en el repositorio. Al hacer clic de nuevo, se ocultan las propiedades.
El componente se muestra de la siguiente manera:

![imagen_1-62](assets/chlimage_1-62.png)

#### Ejemplo 1: Widget de varios campos personalizado {#example-custom-multifield-widget}

La variable **Multicampo personalizado** el cuadro de diálogo basado en widgets muestra una ventana con una ficha. La pestaña tiene un widget multicampo personalizado que, a diferencia del estándar que tiene un campo, tiene dos campos: un menú desplegable con dos opciones y un campo de texto.

La variable **Multicampo personalizado** cuadro de diálogo basado en widgets:

* Está definido por un nodo (tipo de nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Muestra una `tabpanel` widget (tipo de nodo = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) que contiene un panel (tipo de nodo = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* El panel tiene un `multifield` widget (tipo de nodo = `cq:Widget`, xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`).
* La variable `multifield` El widget tiene un campo dconfig (tipo de nodo = `nt:unstructured`, xtype = `ejstcustom`, optionsProvider = `Ejst.x3.provideOptions`) que se basa en el xtype personalizado &#39; `ejstcustom`&#39;:
   * &#39; `fieldconfig`&#39; es una opción de configuración de la variable ` [CQ.form.MultiField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.MultiField)` objeto.
   * &#39; `optionsProvider`&#39; es una configuración de la variable `ejstcustom` para abrir el Navegador. Se configura con la variable `Ejst.x3.provideOptions` método definido en `exercises.js` en:
      `/apps/extjstraining/clientlib/js/exercises.js`
y devuelve dos opciones.
* Se define mediante la variable `multifield` en:
   `/apps/extjstraining/components/customwidgets/multifield`
* Se procesa en formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

El `multifield` widget (xtype = `ejstcustom`):

* Es un objeto JavaScript llamado `Ejst.CustomWidget`
* Se define en la variable `CustomWidget.js` Archivo JavaScript en:
   `/apps/extjstraining/clientlib/js/CustomWidget.js`
* Amplía el ` [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField)` para abrir el Navegador.
* Tiene tres campos: `hiddenField` (Campo de texto), `allowField` (ComboBox) y `otherField` (Campo de texto)
* Anulaciones `CQ.Ext.Component#initComponent` para añadir los tres campos:
   * `allowField` es [CQ.form.Selection](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.Selection) objeto de tipo &quot;select&quot;. optionsProvider es una configuración del objeto Selection a la que se crea una instancia con la configuración optionsProvider del widget personalizado definido en el cuadro de diálogo
   * `otherField` es [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField) object
* Anula los métodos `setValue`, `getValue` y `getRawValue` de [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField) para establecer y recuperar el valor de CustomWidget con el formato :
   `<allowField value>/<otherField value>, for example: 'Bla1/hello'`.
* Se registra a sí mismo como &#39; `ejstcustom`&#39; xtype:
   `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

El cuadro de diálogo basado en widgets **Campo múltiple personalizado** se muestra de la siguiente manera:

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### Ejemplo 2: Personalizado `Treebrowse` Widget {#example-custom-treebrowse-widget}

El **`Treebrowse`** el cuadro de diálogo basado en widgets muestra una ventana con una ficha que contiene un widget de exploración de rutas personalizado. Cuando selecciona la flecha, se abre una ventana en la que puede examinar una jerarquía y seleccionar un elemento. A continuación, la ruta del elemento se agrega al campo de ruta y se mantiene cuando se cierra el cuadro de diálogo.

El `treebrowse` diálogo:

* Está definido por un nodo (tipo de nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Muestra una `tabpanel` widget (tipo de nodo = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) que contiene un panel (tipo de nodo = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* El panel tiene un widget personalizado (tipo de nodo = `cq:Widget`, xtype = `ejstbrowse`)
* Se define mediante la variable `treebrowse` en:
   `/apps/extjstraining/components/customwidgets/treebrowse`
* Se procesa en formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

El widget de árbol personalizado (xtype = `ejstbrowse`):

* Es un objeto JavaScript llamado `Ejst.CustomWidget`
* Se define en la variable `CustomBrowseField.js` Archivo JavaScript en:
   `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* Extensiones ` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`.
* Define una ventana de navegación llamada `browseWindow`.
* Anulaciones ` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick` para mostrar la ventana de navegación cuando se hace clic en la flecha.
* Define un [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel) objeto:
   * Obtiene sus datos llamando al servlet registrado en `/bin/wcm/siteadmin/tree.json`.
   * Su raíz es &quot; `apps/extjstraining`&quot;.
* Define un `window` objeto ( ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`):
   * Basado en el panel predefinido.
   * Tiene un **OK** que define el valor de la ruta seleccionada y oculta el panel.
* La ventana está anclada debajo del **Ruta** campo .
* La ruta seleccionada se pasa del campo Examinar a la ventana de `show` evento.
* Se registra como &#39; `ejstbrowse`&#39; xtype:
   `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

Para usar la variable **Pantallas de árbol personalizadas** cuadro de diálogo basado en widgets:

1. Reemplace el cuadro de diálogo del **Widgets personalizados** con el **Pantallas de árbol personalizadas** diálogo: siga los pasos descritos para la variable [Ejemplo 2: Cuadro de diálogo de panel único](#example-single-panel-dialog)
1. Edite el componente: el cuadro de diálogo se muestra de la siguiente manera:

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### Ejemplo 3: Complemento Editor de texto enriquecido (RTE) {#example-rich-text-editor-rte-plug-in}

La variable **Complemento Editor de texto enriquecido (RTE)** el cuadro de diálogo basado en editor de texto enriquecido es un cuadro de diálogo basado en editor de texto enriquecido que tiene un botón personalizado para insertar texto personalizado entre corchetes. El texto personalizado se puede analizar mediante alguna lógica del lado del servidor (no implementada en este ejemplo), por ejemplo para agregar texto definido en la ruta dada:

La variable **Complemento RTE** diálogo basado en:

* Se define mediante el nodo replugin en:
   `/apps/extjstraining/components/customwidgets/rteplugin`
* Se procesa en formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* La variable `rtePlugins` el nodo tiene un nodo secundario `inserttext` (tipo de nodo = `nt:unstructured`) que recibe el nombre del complemento. Tiene una propiedad denominada `features` que define qué características del complemento están disponibles para RTE.

El complemento RTE:

* Es un objeto JavaScript llamado `Ejst.InsertTextPlugin`
* Se define en la variable `InsertTextPlugin.js` Archivo JavaScript en:
   `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* Amplía el ` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` objeto.
* Los siguientes métodos definen la variable ` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` y se anulan en el complemento de implementación:
   * `getFeatures()` devuelve una matriz de todas las funciones que pone a disposición el complemento.
   * `initializeUI()` agrega el nuevo botón a la barra de herramientas de RTE.
   * `notifyPluginConfig()` muestra título y texto cuando se sitúa el botón sobre él.
   * `execute()` cuando se hace clic en el botón y realiza la acción del complemento: muestra una ventana que se utiliza para definir el texto que se va a incluir.
* `insertText()` inserta un texto utilizando el objeto de diálogo correspondiente `Ejst.InsertTextPlugin.Dialog` (ver más adelante).
* `executeInsertText()` es invocado por el `apply()` método del cuadro de diálogo, que se activa cuando se activa la variable **OK** se hace clic en el botón .
* Se registra como &#39; `inserttext`&#39; plugin:
   `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* el `Ejst.InsertTextPlugin.Dialog` define el cuadro de diálogo que se abre cuando se hace clic en el botón del complemento. El cuadro de diálogo consta de un panel, un formulario, un campo de texto y dos botones (**OK** y **Cancelar**).

Para usar la variable **Complemento Editor de texto enriquecido (RTE)** diálogo basado en:

1. Reemplace el cuadro de diálogo del **Widgets personalizados** con el **Complemento Editor de texto enriquecido (RTE)** diálogo basado en: siga los pasos descritos para la variable [Ejemplo 2: Cuadro de diálogo de panel único](#example-single-panel-dialog)
1. Edite el componente.
1. Haga clic en el último icono de la derecha (el que tiene cuatro flechas). Introduzca una ruta y haga clic en **OK**: La ruta se muestra entre corchetes ([ ]).
1. Haga clic en **OK** por lo tanto, se cierra el Editor de texto enriquecido.

La variable **Complemento Editor de texto enriquecido (RTE)** el cuadro de diálogo basado se muestra de la siguiente manera:

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>Este ejemplo solo muestra cómo implementar la parte del lado del cliente de la lógica: los marcadores de posición (*[text]*) deben analizarse explícitamente en el lado del servidor (por ejemplo, en el componente JSP).

### Tree Overview {#tree-overview}

La solución predeterminada ` [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)` proporciona representación de IU estructurada en árbol de datos estructurados en árbol. El componente Información general de árbol incluido en la variable **Uso de las utilidades de ExtJS** muestra cómo usar el `TreePanel` para mostrar un árbol JCR debajo de una ruta determinada. La ventana en sí puede acoplarse o desacoplarse. En este ejemplo, la lógica de ventana está incrustada en el jsp del componente entre &lt;script>&lt;/script> etiquetas.

Para incluir el **Información general de árbol** a la página de muestra:

1. Agregue la variable **4. Información general de árbol** a la página de muestra desde el **Uso de las utilidades de ExtJS** en la ficha **Barra de tareas**.
1. El componente muestra:
   * un título, con texto
   * a **PROPIEDADES** vínculo: haga clic en para mostrar las propiedades del párrafo almacenado en el repositorio. Haga clic de nuevo para ocultar las propiedades.
   * una ventana flotante con una representación de árbol del repositorio que se puede expandir.

El componente se muestra de la siguiente manera:

![screen_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

El componente Información general de árbol:

* Se define en:
   `/apps/extjstraining/components/treeoverview`

* El cuadro de diálogo permite definir el tamaño de la ventana y acoplar o desacoplar la ventana (consulte los detalles a continuación).

El componente jsp:

* Recupera las propiedades de ancho, alto y acoplado del repositorio.
* Muestra texto sobre el formato de datos de descripción general del árbol.
* Incrusta la lógica de ventana en el jsp del componente entre las etiquetas JavaScript.
* Se define en:
   `apps/extjstraining/components/treeoverview/content.jsp`

El código JavaScript incrustado en el componente jsp:

* Define un `tree` intentando recuperar una ventana de árbol de la página.
* Si la ventana que muestra el árbol no existe, `treePanel` ([CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)):
   * `treePanel` contiene los datos que se utilizan para crear la ventana.
   * Los datos se recuperan llamando al servlet registrado en:
      `/bin/wcm/siteadmin/tree.json`
* La variable `beforeload` listener se asegura de que se carga el nodo seleccionado.
* La variable `root` el objeto define la ruta `apps/extjstraining` como raíz de árbol.
* `tree` ( ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`) se configura en función del `treePanel`y se muestra con:
   `tree.show();`
* Si la ventana existe, se muestra en función de la anchura, la altura y las propiedades acopladas recuperadas del repositorio.

El cuadro de diálogo del componente:

* Muestra una ficha con dos campos para definir el tamaño (anchura y altura) de la ventana de información general del árbol y un campo para acoplar/desacoplar la ventana
* Está definido por un nodo (tipo de nodo = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* El panel tiene un widget de campo de tamaño (tipo de nodo = `cq:Widget`, xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`) y un widget de selección (tipo de nodo = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, tipo = `radio`) con dos opciones (true/false)
* Se define mediante el nodo de diálogo en:
   `/apps/extjstraining/components/treeoverview/dialog`
* Se procesa en formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* Se muestra de la siguiente manera:

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### Información general de cuadrícula {#grid-overview}

Un panel de cuadrícula representa los datos en un formato de tabla de filas y columnas. Se compone de lo siguiente:

* Tienda : el modelo que contiene los registros de datos (filas).
* Modelo de columna : la composición de la columna.
* Ver : encapsula la interfaz de usuario.
* Modelo de selección : el comportamiento de selección.

El componente Información general de cuadrícula incluido en la variable **Uso de las utilidades de ExtJS** paquete muestra cómo mostrar los datos en formato de tabla:

* El ejemplo 1 utiliza datos estáticos.
* El ejemplo 2 utiliza datos recuperados del repositorio.

Para incluir el componente Información general de cuadrícula en la página de muestra:

1. Agregue la variable **5. Información general de cuadrícula** a la página de muestra desde el **Uso de las utilidades de ExtJS** en la ficha **Barra de tareas**.
1. El componente muestra:
   * un título con texto
   * a **PROPIEDADES** vínculo: haga clic en para mostrar las propiedades del párrafo almacenado en el repositorio. Haga clic de nuevo para ocultar las propiedades.
   * una ventana flotante que contiene datos en formato de tabla.

El componente se muestra de la siguiente manera:

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### Ejemplo 1: Cuadrícula predeterminada {#example-default-grid}

En su versión predeterminada, la variable **Información general de cuadrícula** muestra una ventana con datos estáticos en formato de tabla. En este ejemplo, la lógica está incrustada en el jsp del componente de dos maneras:

* la lógica genérica se define entre &lt;script>&lt;/script> etiquetas
* the specific logic is available in a separate .js file and is linked to in the jsp. This setup lets you switch between the two logic (static/dynamic) by commenting the desired &lt;script> tags.

El componente Información general de cuadrícula :

* Se define en:
   `/apps/extjstraining/components/gridoverview`
* El cuadro de diálogo permite definir el tamaño de la ventana y acoplar o desacoplar la ventana.

El componente jsp:

* Recupera las propiedades de ancho, alto y acoplado del repositorio.
* Muestra texto como introducción al formato de datos de información general de la cuadrícula.
* Hace referencia al código JavaScript que define el objeto GridPanel:
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`

   `defaultgrid.js` define algunos datos estáticos como una base para el objeto GridPanel.
* Incrusta código JavaScript entre etiquetas JavaScript que define el objeto Window que consume el objeto GridPanel.
* Se define en:
   `apps/extjstraining/components/gridoverview/content.jsp`

El código JavaScript incrustado en el componente jsp:

* Define el `grid` intentando recuperar el componente de ventana de la página:
   `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* If `grid` no existe, un [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) objeto ( `gridPanel`) se define llamando a la función `getGridPanel()` método (consulte a continuación). Este método se define en `defaultgrid.js`.
* `grid` es ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)` basado en el panel de cuadrícula predefinido y se muestra: `grid.show();`
* If `grid` existe, se muestra en función de la anchura, la altura y las propiedades acopladas recuperadas del repositorio.

El archivo JavaScript ( `defaultgrid.js`) al que se hace referencia en el componente jsp define la variable `getGridPanel()` método al que llama el script incrustado en el JSP y devuelve un ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` basado en datos estáticos. La lógica es la siguiente:

* `myData` es una matriz de datos estáticos con formato de tabla de cinco columnas y cuatro filas.
* `store` es `CQ.Ext.data.Store` objeto que consume `myData`.
* `store` se carga en la memoria:
   `store.load();`
* `gridPanel` es ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` objeto que consume `store`:
   * los anchos de columna siempre se reasignan:
      `forceFit: true`
   * solo se puede seleccionar una fila a la vez:
      `singleSelect:true`

#### Ejemplo 2: Cuadrícula de búsqueda de referencia {#example-reference-search-grid}

Al instalar el paquete, la variable `content.jsp` del **Información general de cuadrícula** muestra una cuadrícula basada en datos estáticos. Es posible modificar el componente para mostrar una cuadrícula con las siguientes características:

* Tiene tres columnas.
* Se basa en los datos recuperados del repositorio llamando a un servlet.
* Las celdas de la última columna se pueden editar. El valor se mantiene en un `test` debajo del nodo definido por la ruta que se muestra en la primera columna.

Como se explica en la sección anterior, el objeto window obtiene su ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` llamando al `getGridPanel()` método definido en la variable `defaultgrid.js` file at `/apps/extjstraining/components/gridoverview/defaultgrid.js`. El componente **Información general de cuadrícula **proporciona una implementación diferente para la `getGridPanel()` método, definido en la variable `referencesearch.js` file at `/apps/extjstraining/components/gridoverview/referencesearch.js`. Al cambiar el archivo .js al que se hace referencia en el jsp del componente, la cuadrícula se basa en los datos recuperados del repositorio.

Cambie el archivo .js al que se hace referencia en el componente jsp:

1. En **CRXDE Lite**, en el `content.jsp` del componente, comente la línea que incluye el `defaultgrid.js` para que tenga el siguiente aspecto:
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. Elimine el comentario de la línea que incluye la variable `referencesearch.js` para que tenga el siguiente aspecto:
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. Guarde los cambios.
1. Actualice la página de muestra.

El componente se muestra de la siguiente manera:

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

Código JavaScript al que se hace referencia en el componente jsp ( `referencesearch.js`) define el `getGridPanel()` método llamado desde el componente jsp y devuelve un ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` , en función de los datos que se recuperan dinámicamente del repositorio. La lógica de `referencesearch.js` define algunos datos dinámicos como una base para el panel de cuadrícula:

* `reader` es ` [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.JsonReader)`objeto que lee la respuesta del servlet en formato json para tres columnas.
* `cm` es ` [CQ.Ext.grid.ColumnModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` para tres columnas.
Las celdas de la columna &quot;Prueba&quot; se pueden editar tal como se definen con un editor:
   `editor: new [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* las columnas se pueden ordenar:
   `cm.defaultSortable = true;`
* `store` es ` [CQ.Ext.data.GroupingStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)` objeto:
   * obtiene sus datos llamando al servlet registrado en &quot; `/bin/querybuilder.json`&quot; con algunos parámetros utilizados para filtrar la consulta
   * se basa en `reader`, definido previamente
   * la tabla se ordena según el &#39;**jcr:path**&#39; en orden ascendente
* `gridPanel` es ` [CQ.Ext.grid.EditorGridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` objeto que se puede editar:
   * se basa en el `store` y en el modelo de columna `cm`
   * solo se puede seleccionar una fila a la vez:
      `sm: new [CQ.Ext.grid.RowSelectionModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * el `afteredit` el listener se asegura de que, después de una celda de la sección **Prueba**&quot; se ha editado la columna:
      * la propiedad &#39; `test`&#39; del nodo en la ruta definida por el **jcr:path**&quot; se configura en el repositorio con el valor de la celda
      * si el POST se realiza correctamente, el valor se agrega al `store` objeto, de lo contrario, se rechaza
