---
title: Edición del contenido de una página
seo-title: Editar el contenido de una página
description: Una vez creada la página, puede actualizarla según sus necesidades editando el contenido
seo-description: Una vez creada la página, puede actualizarla según sus necesidades editando el contenido
uuid: 5b4f0a8f-5196-42ea-8413-203783a0b77b
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: f92ed674-5865-4a53-8c3a-369536861f14
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Editar el contenido de una página{#editing-page-content}

Después de crear una página (nueva o como parte de un lanzamiento o Live Copy), puede editar el contenido para realizar las actualizaciones que requiera.

El contenido se añade mediante los [componentes](/help/sites-authoring/default-components-console.md) (adecuados para el tipo de contenido), que se pueden arrastrar hacia la página. Después estos se pueden editar in situ, mover o eliminar.

>[!NOTE]
>
>Su cuenta debe disponer de los [privilegios de acceso](/help/sites-administering/security.md) y los [permisos apropiados](/help/sites-administering/security.md#permissions) para editar páginas.
>
>Si se producen problemas, le sugerimos que se ponga en contacto con el administrador del sistema.

>[!NOTE]
>
>If your page and/or template has been appropriately set up, then you can use [responsive layout](/help/sites-authoring/responsive-layout.md) when editing.

>[!NOTE]
>
>When in **Edit** mode, links in your content are visible, but **not accessible**. Use [Preview mode](#previewingpagestouchoptimizedui) if you want to navigate using the links in your content.

## Barra de herramientas de página {#page-toolbar}

La barra de herramientas de página ofrece acceso a las funciones correspondientes, en función de la configuración de la página.

![screen_shot_2018-03-22at111338](assets/screen_shot_2018-03-22at111338.png)

La barra de herramientas ofrece acceso a numerosas opciones. En función del contexto y la configuración, puede que algunas opciones no estén disponibles.

* **Alternar panel lateral**

   Esta opción abre o cierra el panel lateral, que contiene el [Navegador de recursos](/help/sites-authoring/author-environment-tools.md#assets-browser), el [Navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser) y el [Árbol de contenido](/help/sites-authoring/author-environment-tools.md#content-tree).

   ![](do-not-localize/screen_shot_2018-03-22at111425.png)

* **Información de la página**

   Proporciona acceso al menú [Información de página](/help/sites-authoring/author-environment-tools.md#page-information), que permite ver los detalles de la página y las acciones que es posible realizar en ella, como ver y editar su información, ver sus propiedades y publicarla/cancelar su publicación.

   ![](do-not-localize/screen_shot_2018-03-22at111437.png)

* **Emulador**

   Activa o desactiva la [barra de herramientas del emulador](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate), que se utiliza para simular el aspecto de la página en otro dispositivo. En el modo de diseño se activa automáticamente.

   ![](do-not-localize/screen_shot_2018-03-22at111442.png)

* **Context Hub**

   Abre el [Context Hub](/help/sites-authoring/ch-previewing.md). Solo está disponible en el modo de vista previa.

   ![screen_shot_2018-03-22at111543](assets/screen_shot_2018-03-22at111543.png)

* **Título de página**

   Es meramente informativo.

   ![screen_shot_2018-03-22at111554](assets/screen_shot_2018-03-22at111554.png)

* **Selector de modo** 

   Muestra el [modo](/help/sites-authoring/author-environment-tools.md#page-modes) actual y permite seleccionar otro, como por ejemplo edición, diseño, deformación de tiempo o segmentación.

   ![chlimage_1-120](assets/chlimage_1-120.png)

* **Vista previa**

   Activa el [modo de vista previa](/help/sites-authoring/editing-content.md#preview-mode). Aquí se muestra la página tal y como aparecerá cuando se publique.

   ![chlimage_1-121](assets/chlimage_1-121.png)

* **Anotar**

   Le permite añadir [anotaciones](/help/sites-authoring/annotations.md) a una página al revisarla. Tras añadir la primera anotación, el icono se convertirá en un número que indica la cantidad de anotaciones que tiene la página.

   ![](do-not-localize/screen_shot_2018-03-22at111638.png)

### Notificación de estado {#status-notification}

If a page is part of a [workflow](/help/sites-authoring/workflows.md) or multiple workflows, this information is shown in a notification bar at the top of the screen when editing the page.

![screen_shot_2018-03-22at111739](assets/screen_shot_2018-03-22at111739.png)

>[!NOTE]
>
>La barra de estado solo es visible para las cuentas de usuario con los privilegios apropiados.

La notificación indica el flujo de trabajo que se está ejecutando con la página. Si el usuario participa en el paso actual del flujo de trabajo, también dispondrá de opciones para [afectar al estado del flujo de trabajo](/help/sites-authoring/workflows-participating.md) y obtener más información sobre el mismo, como por ejemplo:

* **Completar** : abre el cuadro de diálogo **Completar elemento** de trabajo

* **Delegar** : abre el cuadro de diálogo **Completar elemento** de trabajo

* **Ver detalles** : abre la ventana **Detalles** del flujo de trabajo

Completing and delegating workflow steps via the notification bar works as it does when [participating in workflows](/help/sites-authoring/workflows-participating.md) from the Notification inbox.

Si la página está sujeta a varios flujos de trabajo, el número de los mismos se muestra en el extremo derecho de la notificación, junto a dos botones de flecha que permiten desplazarse por los flujos de trabajo.

![chlimage_1-122](assets/chlimage_1-122.png)

## Marcador de posición de componente {#component-placeholder}

El marcador de posición de componente es un indicador para mostrar la posición del componente cuando lo coloque (sobre el componente por el que pasa el ratón en ese momento).

* Al añadir un componente nuevo a la página (arrastrándolo desde el navegador de componentes):

   ![screen_shot_2018-03-22at111928](assets/screen_shot_2018-03-22at111928.png)

* Al mover un componente existente:

   ![screen_shot_2018-03-22at112445](assets/screen_shot_2018-03-22at112445.png)

## Insertar un componente {#inserting-a-component}

### Inserción de un componente desde el navegador de componentes {#inserting-a-component-from-the-components-browser}

Puede seleccionar un componente nuevo mediante el [navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser). El [marcador de posición de componente](#component-placeholder) le muestra dónde se colocará el componente:

1. Asegúrese de que la página se encuentra en el modo de [**edición **.](/help/sites-authoring/author-environment-tools.md#page-modes)
1. Abra el [navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser).
1. Arrastre el componente en cuestión hasta la [posición deseada](#component-placeholder).

1. [Edite](#editmovecopypastedelete) el componente.

>[!NOTE]
>
>En un dispositivo móvil, el navegador de componentes ocupará toda la pantalla. Cuando comience a arrastrar un componente, el navegador se cerrará para volver a mostrar la página, de modo que pueda colocarlo.

### Inserción de un componente desde el sistema de párrafos {#inserting-a-component-from-the-paragraph-system}

Puede agregar un componente nuevo mediante el cuadro **Arrastrar componentes aquí** del sistema de párrafos:

1. Asegúrese de que la página se encuentra en el modo de [**edición **.](/help/sites-authoring/author-environment-tools.md#page-modes)
1. Existen dos formas de seleccionar y añadir un nuevo componente desde el sistema de párrafo:

   * Seleccione la opción **Insertar componente** (+) en la barra de herramientas de un componente existente o el cuadro **Arrastrar componentes aquí**.
   ![screen_shot_2018-03-22at112536](assets/screen_shot_2018-03-22at112536.png)

   * If you are on a desktop device you can double-click on the **Drag components here** box.
   Se abrirá el cuadro de diálogo **Insertar nuevo componente** para que pueda seleccionar el componente requerido: 

   ![screen_shot_2018-03-22at112650](assets/screen_shot_2018-03-22at112650.png)

1. El componente seleccionado se agregará a la parte inferior de la página. [Edite](#editmovecopypastedelete) el componente como sea necesario.

### Inserción de un componente mediante el navegador de recursos {#inserting-a-component-using-the-assets-browser}

También puede añadir un componente nuevo a la página arrastrando un recurso desde el [navegador de recursos](/help/sites-authoring/author-environment-tools.md#assets-browser). De este modo se crea automáticamente un componente nuevo del tipo correspondiente (que contiene el recurso).

Esta opción es válida para los siguientes tipos de activo (algunos dependen del sistema de páginas o de párrafos):

<table>
 <tbody>
  <tr>
   <th><strong>Tipo de recurso</strong></th>
   <th><strong>Tipo de componente resultante</strong></th>
  </tr>
  <tr>
   <td>Imagen</td>
   <td>Imagen</td>
  </tr>
  <tr>
   <td>Documento</td>
   <td>Descargar</td>
  </tr>
  <tr>
   <td>Producto</td>
   <td>Producto</td>
  </tr>
  <tr>
   <td>Vídeo</td>
   <td>Flash</td>
  </tr>
  <tr>
   <td>Fragmento de contenido</td>
   <td>Fragmento de contenido<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Puede configurar este comportamiento en su instalación. Para obtener más detalles, consulte [Configurar un sistema de párrafos de manera que, al arrastrar un activo, se cree una instancia de componente](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance).

Para crear un componente arrastrando uno de los tipos de activo anteriores:

1. Asegúrese de que la página se encuentra en el modo de [**edición **.](/help/sites-authoring/author-environment-tools.md#page-modes)
1. Abra el [navegador de recursos](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. Arrastre el recurso hasta la posición necesaria. El [marcador de posición de componente](#component-placeholder) le muestra dónde se colocará este.

   Se creará un componente apropiado para el tipo de activo en la posición requerida: un componente que contendrá el activo seleccionado.

1. Si es necesario, [edite](#editmovecopypastedelete) el componente.

>[!NOTE]
>
>En un dispositivo móvil, el navegador de recursos ocupará toda la pantalla. Cuando comience a arrastrar un recurso, el navegador se cerrará para volver a mostrar la página, de modo que pueda colocarlo.

Si al examinar los recursos descubre que necesita realizar alguna modificación rápida en alguno de ellos, puede iniciar el [editor de recursos](/help/assets/managing-assets-touch-ui.md) directamente desde el navegador haciendo clic en el icono de edición que hay junto al nombre del recurso.

![screen_shot_2018-03-22at112735](assets/screen_shot_2018-03-22at112735.png)

## Editar/Configurar/Copiar/Cortar/Eliminar/Pegar {#edit-configure-copy-cut-delete-paste}

Si se selecciona un componente, se abrirá la barra de herramientas, que proporciona acceso a distintas acciones que se pueden realizar en el componente.

Las acciones disponibles para el usuario se mostrarán según corresponda y es posible que no todas las acciones se describan aquí.

![screen_shot_2018-03-22at112909](assets/screen_shot_2018-03-22at112909.png)

* **Editar**

   [Según el tipo](/help/sites-authoring/default-components.md) de componente, esto le permitirá [editar el contenido del componente](#edit-content). Normalmente se mostrará una barra de herramientas.

   ![](do-not-localize/screen_shot_2018-03-22at112936.png)

* **Configurar**

   [Según el tipo](/help/sites-authoring/default-components.md) de componente, esto le permitirá editar y configurar las propiedades del componente. A menudo, se abrirá un cuadro de diálogo.

   ![](do-not-localize/screen_shot_2018-03-22at112955.png)

* **Copiar**

   Esta opción copiará el componente al portapapeles. Tras la acción de pegado, se conservará el componente original.

   ![](do-not-localize/screen_shot_2018-03-22at113000.png)

* **Cortar**

   Esta opción copiará el componente al portapapeles. Tras la acción de pegado, se eliminará el componente original.

   ![screen_shot_2018-03-22at113007](assets/screen_shot_2018-03-22at113007.png)

* **Eliminar**

   Esta opción eliminará el componente de la página, previa confirmación.

   ![](do-not-localize/screen_shot_2018-03-22at113012.png)

* **Insertar componente**

   Esta opción abre el cuadro de diálogo para [agregar un nuevo componente](/help/sites-authoring/editing-content.md#inserting-a-component-from-the-paragraph-system).

   ![](do-not-localize/screen_shot_2018-03-22at113017.png)

* **Pegar**

   El componente del portapapeles se copiará en la página. Dependiendo de si utilizó copiar o cortar, el original se conservará o no.

   * Puede pegar componentes en la misma página o en otra distinta.
   * El elemento se pegará sobre el elemento en el que seleccione la acción de pegar.
   * La acción Pegar se muestra únicamente si hay contenido en el portapapeles.
   ![screen_shot_2018-03-22at113553](assets/screen_shot_2018-03-22at113553.png)

   >[!NOTE]
   >
   >Si pega contenido en otra página que ya estaba abierta antes de la operación de corte y copia, debe actualizar la página para ver el contenido pegado.

* **Agrupar**

   Esta opción le permite seleccionar varios componentes a la vez. En un dispositivo de escritorio puede conseguir lo mismo haciendo **Control + clic** o **Comando + clic**.

   ![](do-not-localize/screen_shot_2018-03-22at113240.png)

* **Principal**

   Permite seleccionar el componente principal del componente seleccionado.

   ![screen_shot_2018-03-22at113028](assets/screen_shot_2018-03-22at113028.png)

* **Diseño**

   Permite modificar el [diseño](/help/sites-authoring/editing-content.md#edit-component-layout) del componente seleccionado. Esta opción se aplica únicamente al componente seleccionado y no activa el [modo de diseño](/help/sites-authoring/author-environment-tools.md#page-modes) para toda la página.

   ![](do-not-localize/screen_shot_2018-03-22at113044.png)

* **Conversión en una variación de fragmento de experiencias**

   Esto permite crear un nuevo [fragmento de experiencias](/help/sites-authoring/experience-fragments.md) a partir del componente seleccionado o añadirlo a un fragmento de experiencias. 

   ![](do-not-localize/screen_shot_2018-03-22at113033.png)

## Editar (contenido) {#edit-content}

Hay dos métodos para añadir y/o editar contenido en los componentes:

* Abra el [cuadro de diálogo del componente para editarlo](#component-edit-dialog).
* [Arrastre y coloque un recurso](#draganddropintocomponent) desde el navegador de recursos para agregar contenido directamente.

### Cuadro de diálogo de edición de contenido {#component-edit-dialog}

Puede abrir un componente para editar su contenido mediante el icono de [edición (lápiz) de la barra de herramientas de componentes](#edit-configure-copy-cut-delete-paste).

Las opciones exactas de edición dependerán del componente. Para algunos componentes, [solo en el modo de pantalla completa estarán disponibles todas las acciones](#edit-content-full-screen-mode). Por ejemplo:

* [Componente de texto](/help/sites-authoring/rich-text-editor.md#main-pars-title-24)

   ![screen_shot_2018-03-22at120215](assets/screen_shot_2018-03-22at120215.png)

* Componente de imagen

   ![screen_shot_2018-03-22at120252](assets/screen_shot_2018-03-22at120252.png)

   >[!NOTE]
   >
   >La edición no funciona con un componente de imagen vacío.
   >
   >
   >Debe [arrastrar o cargar una imagen (mediante Configurar)](/help/sites-authoring/default-components-foundation.md#image) para poder iniciar la edición.

* Componente de imagen: pantalla completa

   Si [entra en el modo de pantalla completa](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode) para el componente de imagen, tendrá más espacio para editarla y verá opciones de edición adicionales, como **Iniciar mapa** y **Restablecer zoom**. Además, la pantalla completa permite la selección de ajustes preestablecidos de recorte.

   ![screen_shot_2018-03-22at120529](assets/screen_shot_2018-03-22at120529.png)

* Para los componentes creados a partir de más de un componente básico, como el [componente de base de texto e imágenes](/help/sites-authoring/default-components-foundation.md#text-image), primero se debe confirmar qué conjunto de opciones de edición desea utilizar:

   ![chlimage_1-123](assets/chlimage_1-123.png)

### Arrastrar y colocar recursos en un componente {#drag-and-drop-assets-into-component}

Para tipos de componente específicos puede arrastrar y colocar recursos del navegador de recursos directamente en el componente para actualizar el contenido:

| **Tipo de recurso** | **Tipo de componente** |
|---|---|
| Imagen | Imagen |
| Documento | Descargar |
| Producto | Producto |
| Vídeo | Flash |
| Fragmento de contenido | Fragmento de contenido |

## Editar (contenido) en modo de pantalla completa {#edit-content-full-screen-mode}

Se puede acceder y salir del modo de pantalla completa de todos los componentes con la siguiente opción:

![](do-not-localize/chlimage_1-20.png)

Por ejemplo, el componente **Texto**:

![screen_shot_2018-03-22at121616](assets/screen_shot_2018-03-22at121616.png)

>[!NOTE]
>
>Para algunos componentes, el modo de pantalla completa tendrá más opciones disponibles que el editor in-situ básico.

## Mover un componente {#moving-a-component}

Para mover un componente de párrafo:

1. Seleccione el párrafo que desee mover manteniéndolo pulsado o mediante clic y mantener.
1. Arrastre el párrafo a la nueva ubicación. AEM le indicará dónde puede colocarlo. Suéltelo en la ubicación que desee.

   ![screen_shot_2018-03-22at121821](assets/screen_shot_2018-03-22at121821.png)

1. Se mueve el párrafo.

>[!NOTE]
>
>También puede utilizar [Cortar y pegar](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) para mover un componente.

## Editar diseño de componente {#edit-component-layout}

En vez de pasar repetidamente de la edición al [modo de diseño](/help/sites-authoring/responsive-layout.md) para ajustar un componente, puede seleccionar la acción **Diseño** del mismo. Podrá cambiar su diseño sin tener que abandonar el modo de edición, por lo que ahorrará tiempo.

1. When in **Edit** mode of the sites console, selecting a component reveals the component&#39;s toolbar.

   ![screen_shot_2018-03-22at133756](assets/screen_shot_2018-03-22at133756.png)

   Click or tap the **Layout** action to adjust the layout of the component.

   ![](do-not-localize/chlimage_1-21.png)

1. Una vez que se ha seleccionado la acción Diseño:

   * Se muestran los controles de cambio de tamaño del componente.
   * La barra de herramientas del emulador aparece en la parte superior de la pantalla.
   * En la barra de herramientas del componente se muestran las acciones de diseño en vez de las acciones de edición normales.
   ![screen_shot_2018-03-22at133843](assets/screen_shot_2018-03-22at133843.png)

   You can now modify the layout of the component as you would in [layout mode](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode).

1. After making the necessary layout changes, click the **Close** button in the component action menu to stop modifying the layout of the component. La barra de herramientas del componente recuperará su estado de edición normal.

   ![](do-not-localize/screen_shot_2018-03-22at133920.png)

>[!NOTE]
>
>El ámbito de la acción Diseño se reduce al componente seleccionado. Por ejemplo, si está editando el diseño de un componente y, a continuación, hace clic en otro componente, aparecerá la barra de herramientas de edición estándar (no la barra de herramientas de diseño) para el componente recién seleccionado y desaparecerán los controladores de cambio de tamaño, así como la barra de herramientas del emulador.
>
>Si necesita editar el diseño general de la página y modificar múltiples components, cambie al [modo de diseño](/help/sites-authoring/responsive-layout.md).

## Componentes heredados {#inherited-components}

Los componentes heredados pueden ser el producto de distintos escenarios, como por ejemplo:

* [Administración de varios sitios](/help/sites-administering/msm.md)
* [Lanzamientos](/help/sites-authoring/launches.md) (cuando se basan en una Live Copy).
* Componentes específicos, como el sistema de párrafos heredado en Geometrixx.

Puede cancelar (y volver a habilitar) la herencia. En función del componente, esta opción puede estar disponible en:

* **Live Copy**

   La barra de herramientas del componente, siempre que el componente esté en una página que forme parte de una Live Copy o lanzamiento (basado en una Live Copy). Por ejemplo:

   ![screen_shot_2018-03-22at134339](assets/screen_shot_2018-03-22at134339.png)

   La opción Cancelar herencia está disponible:

   ![](do-not-localize/screen_shot_2018-03-22at134406.png)

   O vuelva a activar la herencia si ya se ha cancelado:

   ![](do-not-localize/screen_shot_2018-03-22at134417.png)

   La acción Despliegue también está disponible en el modelo o en el origen de Live Copy:

   ![](do-not-localize/screen_shot_2018-03-22at134516.png)

* **Un sistema de párrafos heredado**

   El cuadro de diálogo de configuración. Por ejemplo, como en el sistema de párrafos heredado:

   ![chlimage_1-124](assets/chlimage_1-124.png)

## Edición de las plantilla de página {#editing-the-page-template}

Si la página se basa en una [plantilla editable](/help/sites-authoring/templates.md#editable-and-static-templates), puede cambiar fácilmente al [editor de plantillas](/help/sites-authoring/templates.md#editing-templates-template-authors) seleccionando **Editar plantilla** en el [menú Información de página](/help/sites-authoring/author-environment-tools.md#page-information).

If the page is based on a [static template](/help/sites-authoring/templates.md#editable-and-static-templates), you can switch to [Design mode](/help/sites-authoring/default-components-designmode.md) using the [page mode selector](/help/sites-authoring/author-environment-tools.md#page-modes) on the toolbar to enable/disable components for use on the page.

Puede ver fácilmente en qué plantilla se basa la página, o cuándo debe seleccionar la página en [vista de columna](/help/sites-authoring/basic-handling.md#column-view) o [vista de lista](/help/sites-authoring/basic-handling.md#list-view).

## Estado de Live Copy {#live-copy-status}

El [modo de la página de estado de Live Copy](/help/sites-authoring/author-environment-tools.md#page-modes) le permite echar un vistazo al estado de la Live Copy y ver los componentes que se han heredado o no:

* Borde verde: heredado
* Borde rosa: se ha cancelado la herencia

Por ejemplo:

![screen_shot_2018-03-22at134820](assets/screen_shot_2018-03-22at134820.png)

## Agregar anotaciones {#adding-annotations}

[Las anotaciones](/help/sites-authoring/annotations.md) permiten que los revisores y otros autores hagan comentarios sobre el contenido. A menudo se utilizan para revisiones y validaciones.

## Previsualizar páginas {#previewing-pages}

Existen dos métodos para visualizar la vista previa de una página:

* [Modo de vista previa](#preview-mode): una vista previa rápida y en el sitio

* [Ver tal y como aparece publicado](#view-as-published): una vista previa completa que abre la página en una nueva pestaña.

>[!NOTE]
>
>* Los vínculos del contenido están visibles en el modo de edición, pero no puede accederse a ellos.
>* Utilice cualquiera de las opciones de vista previa si desea navegar mediante sus vínculos.
>* Use the [keyboard shortcut](/help/sites-authoring/keyboard-shortcuts.md) `Ctrl-Shift-M` to switch between preview and the last selected mode.
>



>[!NOTE]
>
>La cookie del modo WCM está establecida para las dos opciones.

### Modo de vista previa {#preview-mode}

Al editar contenido, puede obtener una vista previa de la página con el [modo de vista previa](/help/sites-authoring/author-environment-tools.md#page-modes). Este modo:

* Oculta los distintos mecanismos de edición para ofrecerle una vista rápida del aspecto que tendrá la página cuando se publique.
* Permite utilizar vínculos para navegar.
* **No** actualiza el contenido de la página.

Al crear proyectos, el modo de vista previa está disponible mediante el icono situado en la parte superior derecha del editor de páginas:

![chlimage_1-125](assets/chlimage_1-125.png)

### Ver tal y como aparece publicado {#view-as-published}

La opción **Ver tal y como aparece publicado** se muestra disponible en el menú [Información de página](/help/sites-authoring/author-environment-tools.md#page-information). Esta opción abre la página en una nueva ficha, actualiza el contenido y muestra la página exactamente como aparecerá en el entorno de publicación.

## Bloquear una página {#locking-a-page}

AEM le permite bloquear páginas para que nadie más pueda modificar su contenido. Esta función es útil cuando realice muchas ediciones en una página concreta o cuando tenga que congelar una página durante un rato.

Las páginas se pueden bloquear desde:

* **Consola Sitios**

   1. Seleccione la página con el [modo de selección](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
   1. Seleccione el icono de bloqueo.
   ![screen_shot_2018-03-22at134928](assets/screen_shot_2018-03-22at134928.png)

* **Editor de página**

   1. Seleccione el icono **Información de página** para abrir el menú.
   1. Seleccione la opción **Bloquear página**.

Una vez bloqueada, se actualiza la información de la vista de la consola y, al editar, se muestra un símbolo de bloqueo en la barra de herramientas.

![screen_shot_2018-03-22at135010](assets/screen_shot_2018-03-22at135010.png)

>[!CAUTION]
>
>El bloqueo de páginas se puede realizar al [suplantar un usuario](/help/sites-administering/security.md#impersonating-another-user). Sin embargo, una página bloqueada de este modo solo la puede desbloquear el usuario que ha suplantado a otro usuario o un usuario con privilegios de administrador.
>
>Las páginas no se pueden bloquear al suplantar al usuario que ha bloqueado la página.

## Desbloquear una página {#unlocking-a-page}

Unlocking a page is very similar to [locking the page](#locking-a-page). Once the page is locked the lock options are replaced by unlock actions.

El menú Información de página muestra la opción **Desbloquear** y el icono Bloquear de la consola Sitios se reemplaza con el icono **Desbloquear**.

![screen_shot_2018-03-22at134942](assets/screen_shot_2018-03-22at134942.png)

>[!CAUTION]
>
>El bloqueo de páginas se puede realizar al [suplantar un usuario](/help/sites-administering/security.md#impersonating-another-user). Sin embargo, una página bloqueada de este modo solo la puede desbloquear el usuario que ha suplantado a otro usuario o un usuario con privilegios de administrador.
>
>Las páginas no se pueden bloquear al suplantar al usuario que ha bloqueado la página.

## Deshacer y rehacer modificaciones de páginas {#undoing-and-redoing-page-edits}

Los iconos siguientes le permiten deshacer o rehacer una acción. Se muestran en la barra de herramientas cuando corresponde:

![](do-not-localize/screen_shot_2018-03-23at093614.png)

>[!NOTE]
>
>The [keyboard shortcut](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) `Ctrl-Z` is also availalbe to undo page edit actions.
>
>The keyboard shortcut `Ctrl-Y` is also availalbe to redo page edit actions.

>[!NOTE]
>
>Consulte [Deshacer y rehacer ediciones de página: la teoría](#undoing-and-redoing-page-edits-the-theory) para ver toda la información sobre las posibilidades de deshacer y rehacer ediciones de página.

## Deshacer y rehacer ediciones de página: la teoría {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>El administrador del sistema puede [configurar varios aspectos de las funciones de Deshacer/Rehacer](/help/sites-administering/config-undo.md) según los requisitos de la instancia.

AEM almacena un historial de las acciones que realiza y la secuencia en que las realizó, de modo que puede deshacer varias acciones en el orden en que se realizaron, y también rehacerlas para volver a aplicar una o más acciones.

Si hay un elemento seleccionado en la página de contenido (por ejemplo, un componente de texto), el comando para deshacer o rehacer se aplica a dicho elemento.

El comportamiento de los comandos Deshacer y Rehacer es similar al de otros programas de software. Use los comandos para restaurar el estado reciente de la página web a medida que toma decisiones sobre el contenido. Por ejemplo, si mueve un párrafo de texto a una ubicación diferente en la página, puede usar el comando Deshacer para mover el párrafo a la posición original. Si más tarde decide que la posición anterior era mejor, use el comando rehacer para “deshacer el deshacer”.

>[!NOTE]
>
>Puede hacer lo siguiente:
>
>* Rehacer acciones siempre y cuando no haya realizado ninguna edición en la página desde que usó el comando Deshacer por última vez.
>* Deshacer un máximo de 20 acciones de edición (configuración predeterminada).
>* Utilizar los [métodos abreviados del teclado](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) para deshacer y rehacer.
>



Puede usar los comandos Deshacer y Rehacer para los siguientes tipos de cambios de página:

* Agregar, editar, quitar y mover párrafos
* Editar contenido de párrafos en el lugar
* Copiar, cortar y pegar elementos en una página

Los campos de formulario procesados por los componentes de formulario no deberían tener valores especificados mientras se crean las páginas. Así pues, los comandos deshacer y rehacer no afectarán a los cambios que realice en los valores de estos tipos de componente. Por ejemplo, no se puede deshacer la selección de un valor en una lista desplegable.

>[!NOTE]
>
>Se necesitan permisos especiales para deshacer y rehacer cambios en archivos e imágenes.

>[!NOTE]
>
>El historial de cambios en archivos e imágenes dura un mínimo de diez horas. No obstante, pasado ese tiempo, no se garantiza que se puedan deshacer los cambios. El administrador puede modificar el plazo predeterminado de diez horas.

