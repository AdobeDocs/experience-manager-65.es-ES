---
title: Edición del contenido de páginas
description: Una vez creada la página, puede editar el contenido para realizar las actualizaciones que necesite.
uuid: 5b4f0a8f-5196-42ea-8413-203783a0b77b
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: f92ed674-5865-4a53-8c3a-369536861f14
docset: aem65
exl-id: d5cf4478-51e4-4ca8-b3f8-6d7caed7d515
source-git-commit: d9155cdac183acbdd190da552512a1e9bcc43d64
workflow-type: tm+mt
source-wordcount: '3082'
ht-degree: 42%

---

# Edición del contenido de una página{#editing-page-content}

Después de crear una página (nueva o como parte de un lanzamiento o Live Copy), puede editar el contenido para realizar las actualizaciones que requiera.

El contenido se añade mediante [componentes](/help/sites-authoring/default-components-console.md) (apropiado para el tipo de contenido) que se puede arrastrar hasta la página. Después estos se pueden editar local, mover o eliminar.

>[!NOTE]
>
>Su cuenta necesita el [derechos de acceso adecuados](/help/sites-administering/security.md) y [permissions](/help/sites-administering/security.md#permissions) para editar páginas.
>
>Si se producen problemas, le sugerimos que se ponga en contacto con el administrador del sistema.

>[!NOTE]
>
>Si la página o plantilla se han configurado correctamente, podrá utilizar el [diseño interactivo](/help/sites-authoring/responsive-layout.md) cuando esté editando.

>[!NOTE]
>
>En el modo de **edición** puede ver los vínculos en el contenido, pero no puede **acceder** a ellos. Utilice el [modo de vista previa](#previewingpagestouchoptimizedui) si desea navegar utilizando los vínculos del contenido.

## Barra de herramientas de página {#page-toolbar}

La barra de herramientas de página ofrece acceso a las funciones correspondientes, en función de la configuración de la página.

![screen_shot_2018-03-22at111338](assets/screen_shot_2018-03-22at111338.png)

La barra de herramientas ofrece acceso a numerosas opciones. Según el contexto y la configuración actuales, algunas opciones pueden no estar disponibles.

* **Alternar panel lateral**

  Esto abre o cierra el panel lateral, que contiene el [Explorador de recursos](/help/sites-authoring/author-environment-tools.md#assets-browser), [Navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser), y [Árbol de contenido](/help/sites-authoring/author-environment-tools.md#content-tree).

  ![Alternar panel lateral](do-not-localize/screen_shot_2018-03-22at111425.png)

* **Información de la página**

  Proporciona acceso al [Información de página](/help/sites-authoring/author-environment-tools.md#page-information) menú que incluye detalles de página y acciones que se pueden realizar en la página, incluida la visualización y edición de información de página, la visualización de propiedades de página y la publicación/cancelación de publicación de la página.

  ![Información de la página](do-not-localize/screen_shot_2018-03-22at111437.png)

* **Emulador**

  Alterna el [barra de herramientas del emulador](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate), que se utiliza para emular el aspecto de la página en otro dispositivo. Esto se activa automáticamente en el modo de diseño.

  ![Emulador](do-not-localize/screen_shot_2018-03-22at111442.png)

* **ContextHub**

  Abre el [Context Hub](/help/sites-authoring/ch-previewing.md). Solo está disponible en el modo de vista previa.

  ![screen_shot_2018-03-22at111543](assets/screen_shot_2018-03-22at111543.png)

* **Título de página**

  Esto es puramente informativo.

  ![screen_shot_2018-03-22at111554](assets/screen_shot_2018-03-22at111554.png)

* **Selector de modo**

  Muestra el actual [modo](/help/sites-authoring/author-environment-tools.md#page-modes) y permite seleccionar otro modo, como edición, diseño, deformación de tiempo o segmentación.

  ![chlimage_1-120](assets/chlimage_1-120.png)

* **Vista previa**

  Habilita [modo de previsualización](/help/sites-authoring/editing-content.md#preview-mode). Esto muestra la página tal como aparecerá cuando se publique.

  ![chlimage_1-121](assets/chlimage_1-121.png)

* **Anotar**

  Permite agregar [anotaciones](/help/sites-authoring/annotations.md) a la página cuando revise una página. Después de la primera anotación, el icono cambia a un número que indica el número de anotaciones en la página.

  ![Anotar](do-not-localize/screen_shot_2018-03-22at111638.png)

### Notificación de estado {#status-notification}

Si una página es parte de uno o varios [flujos de trabajo](/help/sites-authoring/workflows.md), esta información se muestra en una barra de notificación situada en la parte superior de la pantalla cuando edita la página.

![screen_shot_2018-03-22at111739](assets/screen_shot_2018-03-22at111739.png)

>[!NOTE]
>
>La barra de estado solo es visible para las cuentas de usuario con los privilegios adecuados.

La notificación enumera el flujo de trabajo que se ejecuta en la página. Si el usuario está implicado en el paso del flujo de trabajo actual, las opciones son [afectar al estado del flujo de trabajo](/help/sites-authoring/workflows-participating.md) y también dispone de más información sobre el flujo de trabajo, como:

* **Completar** - Abre el **Completar elemento de trabajo** diálogo

* **Delegar** - Abre el **Completar elemento de trabajo** diálogo

* **Ver detalles**: abre la ventana **Detalles** del flujo de trabajo.

Completar y delegar los pasos del flujo de trabajo mediante la barra de notificaciones funciona igual que al [participar en flujos de trabajo](/help/sites-authoring/workflows-participating.md) desde la bandeja de entrada de notificaciones.

Si la página está sujeta a varios flujos de trabajo, el número de los mismos se muestra en el extremo derecho de la notificación, junto a dos botones de flecha que permiten desplazarse por los flujos de trabajo.

![chlimage_1-122](assets/chlimage_1-122.png)

## Marcador de posición de componente {#component-placeholder}

El marcador de posición de componente es un indicador que muestra dónde se colocará un componente cuando lo suelte, sobre el componente que está pasando el ratón por encima.

* Al añadir un componente nuevo a la página (arrastrando desde el explorador de componentes):

  ![screen_shot_2018-03-22at111928](assets/screen_shot_2018-03-22at111928.png)

* Al mover un componente existente:

  ![screen_shot_2018-03-22at112445](assets/screen_shot_2018-03-22at112445.png)

## Insertar un componente {#inserting-a-component}

### Inserción de un componente desde el navegador de componentes {#inserting-a-component-from-the-components-browser}

Puede seleccionar un componente nuevo mediante el [navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser). El [marcador de posición de componente](#component-placeholder) le muestra dónde se colocará el componente:

1. Asegúrese de que la página se encuentra en el modo de [**edición**.](/help/sites-authoring/author-environment-tools.md#page-modes)
1. Abra el [navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser).
1. Arrastre el componente en cuestión hasta la [posición deseada](#component-placeholder).

1. [Editar](#editmovecopypastedelete) el componente.

>[!NOTE]
>
>En un dispositivo móvil, el navegador de componentes llenará toda la pantalla. Una vez que comience a arrastrar un componente, el explorador se cerrará para mostrar de nuevo la página y así poder colocar el componente.

### Inserción de un componente desde el sistema de párrafos {#inserting-a-component-from-the-paragraph-system}

Puede agregar un componente nuevo mediante el cuadro **Arrastrar componentes aquí** del sistema de párrafos:

1. Asegúrese de que la página se encuentra en el modo de [**edición**.](/help/sites-authoring/author-environment-tools.md#page-modes)
1. Existen dos formas de seleccionar y agregar un componente nuevo desde el sistema de párrafos:

   * Seleccione el **Insertar componente** opción (+) de la barra de herramientas de un componente existente o de la **Arrastre los componentes aquí** cuadro.

   ![screen_shot_2018-03-22at112536](assets/screen_shot_2018-03-22at112536.png)

   * En un dispositivo de escritorio puede hacer doble clic en el cuadro **Arrastrar componentes aquí**.

   Se abrirá el cuadro de diálogo **Insertar nuevo componente** para que pueda seleccionar el componente requerido: 

   ![screen_shot_2018-03-22at112650](assets/screen_shot_2018-03-22at112650.png)

1. El componente seleccionado se agregará a la parte inferior de la página. [Editar](#editmovecopypastedelete) Seleccione el componente según sea necesario.

### Inserción de un componente mediante el navegador de recursos   {#inserting-a-component-using-the-assets-browser}

También puede agregar un componente nuevo a la página arrastrando un recurso desde el [explorador de recursos](/help/sites-authoring/author-environment-tools.md#assets-browser). Esto creará automáticamente un nuevo componente del tipo adecuado (y que contenga el recurso).

Esto es válido para los siguientes tipos de recursos (algunos dependerán del sistema de páginas o párrafos):

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
>Puede configurar este comportamiento en su instalación. Consulte [Configuración de un sistema de párrafos para que, al arrastrar un recurso, se cree una instancia de componente](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) para obtener más información.

Para crear un componente arrastrando uno de los tipos de activo anteriores:

1. Asegúrese de que la página se encuentra en el modo de [**edición**.](/help/sites-authoring/author-environment-tools.md#page-modes)
1. Abra el [explorador de recursos](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. Arrastre el recurso en cuestión a la posición deseada. El [marcador de posición de componente](#component-placeholder) le muestra dónde se colocará el componente.

   Se creará un componente, adecuado para el tipo de recurso, en la ubicación requerida; contendrá el recurso seleccionado.

1. [Editar](#editmovecopypastedelete) el componente, si es necesario.

>[!NOTE]
>
>En un dispositivo móvil, el explorador de recursos rellenará toda la pantalla. Una vez que comience a arrastrar un recurso, el explorador se cerrará para mostrar de nuevo la página y poder colocarlo.

Si al examinar los recursos descubre que necesita realizar algún cambio rápido en alguno de ellos, puede iniciar el [editor de recursos](/help/assets/manage-assets.md) directamente desde el explorador, haciendo clic en el icono de edición situado junto al nombre del recurso.

![screen_shot_2018-03-22at112735](assets/screen_shot_2018-03-22at112735.png)

## Editar/Configurar/Copiar/Cortar/Eliminar/Pegar {#edit-configure-copy-cut-delete-paste}

Si se selecciona un componente, se abrirá la barra de herramientas, que proporciona acceso a distintas acciones que se pueden realizar en el componente.

Las acciones disponibles para el usuario se mostrarán según corresponda y es posible que no todas las acciones se describan aquí.

![screen_shot_2018-03-22at112909](assets/screen_shot_2018-03-22at112909.png)

* **Editar**

  [En función del tipo de componente](/help/sites-authoring/default-components.md), esta opción le permite [editar el contenido del componente](#edit-content). Normalmente se mostrará una barra de herramientas.

  ![Editar](do-not-localize/screen_shot_2018-03-22at112936.png)

* **Configurar**

  [En función del tipo de componente](/help/sites-authoring/default-components.md), esta opción le permite editar y configurar las propiedades del componente. A menudo, se abrirá un cuadro de diálogo.

  ![Configurar](do-not-localize/screen_shot_2018-03-22at112955.png)

* **Copiar**

  Esto copiará el componente en el portapapeles. Después de la acción de pegar, el componente original se mantiene.

  ![Copiar](do-not-localize/screen_shot_2018-03-22at113000.png)

* **Cortar**

  Esto copiará el componente en el portapapeles. Después de la acción de pegar, se eliminará el componente original.

  ![screen_shot_2018-03-22at113007](assets/screen_shot_2018-03-22at113007.png)

* **Eliminar**

  Esto eliminará el componente de la página con su confirmación.

  ![Eliminar](do-not-localize/screen_shot_2018-03-22at113012.png)

* **Insertar componente**

  Esto abre el cuadro de diálogo a [añadir un componente nuevo](/help/sites-authoring/editing-content.md#inserting-a-component-from-the-paragraph-system).

  ![Insertar componente](do-not-localize/screen_shot_2018-03-22at113017.png)

* **Pegar**

  Esto pegará el componente del portapapeles en la página. Si el original permanece, depende de si ha utilizado copiar o cortar.

   * Puede pegar en la misma página o en otra página.
   * El elemento pegado se pegará encima del elemento donde seleccione la acción de pegado.
   * La acción Pegar solo se mostrará si hay contenido en el portapapeles.

  ![screen_shot_2018-03-22at113553](assets/screen_shot_2018-03-22at113553.png)

  >[!NOTE]
  >
  >Si pega en una página diferente que ya estaba abierta antes de la operación de cortar o copiar, debe actualizar la página para ver el contenido pegado.

* **Grupo**

  Esto le permite seleccionar varios componentes a la vez. En un dispositivo de escritorio puede conseguir lo mismo haciendo **Control + clic** o **Comando + clic**.

  ![Grupo](do-not-localize/screen_shot_2018-03-22at113240.png)

* **Principal**

  Permite seleccionar el componente principal del componente seleccionado.

  ![screen_shot_2018-03-22at113028](assets/screen_shot_2018-03-22at113028.png)

* **Diseño**

  Esto le permite modificar el [layout](/help/sites-authoring/editing-content.md#edit-component-layout) del componente seleccionado. Esto solo se aplica al componente seleccionado y no activa el [Modo Diseño](/help/sites-authoring/author-environment-tools.md#page-modes) para toda la página.

  ![Diseño](do-not-localize/screen_shot_2018-03-22at113044.png)

* **Conversión en una variación de fragmento de experiencia**

  Esto permite crear un nuevo [fragmento de experiencia](/help/sites-authoring/experience-fragments.md) a partir del componente seleccionado o añadirlo a un fragmento de experiencia. 

  ![Convertir en variación de fragmento de experiencia](do-not-localize/screen_shot_2018-03-22at113033.png)

## Editar (contenido) {#edit-content}

Hay dos métodos para añadir y/o editar contenido en los componentes:

* Abra el [cuadro de diálogo de componentes para editar](#component-edit-dialog).
* [Arrastrar y soltar un recurso](#draganddropintocomponent) desde el explorador de recursos para añadir contenido directamente.

### Cuadro de diálogo de edición de contenido   {#component-edit-dialog}

Puede abrir un componente para editar el contenido mediante el icono [Editar (lápiz) de la barra de herramientas](#edit-configure-copy-cut-delete-paste) del componente.

Las opciones de edición exactas dependerán del componente. Para algunos componentes [todas las acciones solo estarán disponibles en modo de pantalla completa](#edit-content-full-screen-mode). Por ejemplo:

* [Componente de texto](/help/sites-authoring/rich-text-editor.md#main-pars-title-24)

  ![screen_shot_2018-03-22at120215](assets/screen_shot_2018-03-22at120215.png)

* Componente de imagen

  ![screen_shot_2018-03-22at120252](assets/screen_shot_2018-03-22at120252.png)

  >[!NOTE]
  >
  >La edición no funciona con un componente de imagen vacío.
  >
  >
  >Usted debe [arrastrar o cargar una imagen (con Configurar)](/help/sites-authoring/default-components-foundation.md#image) antes de empezar a editarlo.

* Componente de imagen: pantalla completa

  [La introducción del modo de pantalla completa](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode) para el componente de imagen permite disponer de más espacio para editar la imagen y mostrar opciones de edición adicionales como **Iniciar mapa** y **Restablecer zoom**. Además, la pantalla completa permite seleccionar ajustes preestablecidos de recorte.

  ![screen_shot_2018-03-22at120529](assets/screen_shot_2018-03-22at120529.png)

* Componentes construidos a partir de más de un componente básico, como [Componente de base Texto e imagen](/help/sites-authoring/default-components-foundation.md#text-image), primero pídale que confirme qué conjunto de opciones de edición desea utilizar:

  ![chlimage_1-123](assets/chlimage_1-123.png)

### Arrastrar y colocar recursos en un componente {#drag-and-drop-assets-into-component}

Para tipos de componentes específicos puede arrastrar y soltar recursos desde el explorador de recursos directamente en el componente para actualizar el contenido:

| **Tipo de recurso** | **Tipo de componente** |
|---|---|
| Imagen | Imagen |
| Documento | Descargar |
| Producto | Producto |
| Vídeo | Flash |
| Fragmento de contenido | Fragmento de contenido |

## Editar (Contenido) Modo De Pantalla Completa {#edit-content-full-screen-mode}

Se puede acceder y salir del modo de pantalla completa de todos los componentes con la siguiente opción:

![Editar modo de pantalla completa](do-not-localize/chlimage_1-20.png)

Por ejemplo, el componente **Texto**:

![screen_shot_2018-03-22at121616](assets/screen_shot_2018-03-22at121616.png)

>[!NOTE]
>
>Para algunos componentes, el modo de pantalla completa tendrá más opciones disponibles que el editor local básico.

## Mover un componente {#moving-a-component}

Para mover un componente de párrafo:

1. Seleccione el párrafo que desea mover pulsando y manteniendo pulsado o pulsando y manteniendo pulsado.
1. Arrastre el párrafo a la nueva ubicación. AEM Indica dónde se puede depositar el párrafo. Colóquelo en la ubicación que desee.

   ![screen_shot_2018-03-22at121821](assets/screen_shot_2018-03-22at121821.png)

1. Se mueve el párrafo.

>[!NOTE]
>
>También puede utilizar [Cortar y pegar](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) para mover un componente.

## Editar diseño de componente {#edit-component-layout}

En vez de pasar repetidamente de la edición al [modo de diseño](/help/sites-authoring/responsive-layout.md) para ajustar un componente, puede seleccionar la acción **Diseño** del mismo. Podrá cambiar su diseño sin tener que abandonar el modo de edición, por lo que ahorrará tiempo.

1. En el modo de **edición** de la consola del sitio, si se selecciona un componente, aparece su barra de herramientas.

   ![screen_shot_2018-03-22at133756](assets/screen_shot_2018-03-22at133756.png)

   Pulse o haga clic en la acción **Diseño** para ajustar el diseño del componente.

   ![Barra de herramientas de los componentes](do-not-localize/chlimage_1-21.png)

1. Una vez seleccionada la acción Diseño:

   * Se muestran los controladores de tamaño del componente.
   * La barra de herramientas del emulador se muestra en la parte superior de la pantalla.
   * Las acciones de diseño en lugar de las acciones de edición estándar se muestran en la barra de herramientas de componentes.

   ![screen_shot_2018-03-22at133843](assets/screen_shot_2018-03-22at133843.png)

   Ahora puede modificar el diseño del componente como haría en el [modo de diseño](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode).

1. Después de realizar los cambios necesarios, haga clic en el botón **Cerrar** del menú de acciones del componente para detener la edición del diseño. La barra de herramientas del componente recuperará su estado de edición normal.

   ![Cerrar](do-not-localize/screen_shot_2018-03-22at133920.png)

>[!NOTE]
>
>El ámbito de la acción Diseño se reduce al componente seleccionado. Por ejemplo, si está editando el diseño de un componente y hace clic en otro componente, se muestra la barra de herramientas de edición estándar del componente recién seleccionado (no la barra de herramientas de diseño) y desaparecen los controladores de cambio de tamaño y la barra de herramientas del emulador.
>
>Si necesita editar el diseño general de la página y modificar múltiples componentes, cambie al [modo de diseño](/help/sites-authoring/responsive-layout.md).

## Componentes heredados {#inherited-components}

Los componentes heredados pueden ser el producto de distintos escenarios, como por ejemplo:

* [Administración de varios sitios](/help/sites-administering/msm.md)
* [Lanzamientos](/help/sites-authoring/launches.md) (cuando se basan en una Live Copy).
* Componentes específicos, como el sistema de párrafos heredados dentro de Geometrixx.

Puede cancelar (y volver a habilitar) la herencia. Según el componente, esto puede estar disponible en:

* **Live Copy**

  La barra de herramientas de componentes, si el componente se encuentra en una página que forma parte de una Live Copy o Launch (basado en una Live Copy). Por ejemplo:

  ![screen_shot_2018-03-22at134339](assets/screen_shot_2018-03-22at134339.png)

  La opción Cancelar herencia está disponible:

  ![Cancelar herencia](do-not-localize/screen_shot_2018-03-22at134406.png)

  O volver a habilitar la herencia si ya se ha cancelado:

  ![Volver a habilitar herencia](do-not-localize/screen_shot_2018-03-22at134417.png)

  La acción Despliegue también está disponible en el modelo o en el origen de Live Copy:

  ![Despliegue](do-not-localize/screen_shot_2018-03-22at134516.png)

* **Un sistema de párrafos heredado**

  El cuadro de diálogo Configuración. Por ejemplo, como con el sistema de párrafos heredados:

  ![chlimage_1-124](assets/chlimage_1-124.png)

## Edición de las plantilla de página {#editing-the-page-template}

Si la página está basada en un [plantilla editable](/help/sites-authoring/templates.md#editable-and-static-templates), puede cambiar fácilmente al [editor de plantillas](/help/sites-authoring/templates.md#editing-templates-template-authors) seleccionando **Editar plantilla** en el [Menú Información de página](/help/sites-authoring/author-environment-tools.md#page-information).

Si la página está basada en un [plantilla estática](/help/sites-authoring/templates.md#editable-and-static-templates), puede cambiar a [Modo de diseño](/help/sites-authoring/default-components-designmode.md) uso del [selector de modo de página](/help/sites-authoring/author-environment-tools.md#page-modes) en la barra de herramientas para habilitar o deshabilitar componentes para su uso en la página.

Puede ver fácilmente en qué plantilla se basa la página al seleccionar la página en la vista [Columna](/help/sites-authoring/basic-handling.md#column-view) o en la [vista Lista](/help/sites-authoring/basic-handling.md#list-view).

## Estado de Live Copy   {#live-copy-status}

El [Modo de página Estado de Live Copy](/help/sites-authoring/author-environment-tools.md#page-modes) permite obtener una descripción general rápida del estado de live copy y de los componentes que se heredan o no:

* Borde verde: heredado
* Borde rosa: se ha cancelado la herencia

Por ejemplo:

![screen_shot_2018-03-22at134820](assets/screen_shot_2018-03-22at134820.png)

## Agregar anotaciones {#adding-annotations}

[Anotaciones](/help/sites-authoring/annotations.md) permite que los revisores y otros autores proporcionen comentarios sobre el contenido. A menudo se utilizan con fines de revisión y validación.

## Previsualizar páginas   {#previewing-pages}

Existen dos métodos para visualizar la vista previa de una página:

* [Modo de vista previa](#preview-mode): una vista previa rápida y en el sitio

* [Ver como aparece publicado](#view-as-published) : una vista previa completa que abre la página en una nueva pestaña

>[!NOTE]
>
>* Los vínculos del contenido son visibles, pero no se puede acceder a ellos en el modo de edición.
>* Utilice cualquiera de las opciones de vista previa si desea navegar mediante sus vínculos.
>* Utilice el [atajo de teclado](/help/sites-authoring/keyboard-shortcuts.md) `Ctrl-Shift-M` para cambiar entre la vista previa y el último modo seleccionado.
>

>[!NOTE]
>
>La cookie del modo WCM está establecida para ambas opciones.

### Modo de vista previa {#preview-mode}

Al editar contenido, puede obtener una vista previa de la página mediante la vista previa [modo](/help/sites-authoring/author-environment-tools.md#page-modes). Este modo:

* Oculta los distintos mecanismos de edición para ofrecerle una vista rápida del aspecto que tendrá la página cuando se publique.
* Permite utilizar vínculos para navegar.
* Does **no** actualice el contenido de la página.

Durante la creación, el modo de vista previa está disponible mediante el icono situado en la parte superior derecha del editor de páginas:

![chlimage_1-125](assets/chlimage_1-125.png)

### Ver como aparece publicado {#view-as-published}

El **Ver como aparece publicado** La opción está disponible en [Información de página](/help/sites-authoring/author-environment-tools.md#page-information) menú. Esta opción abre la página en una nueva pestaña, actualiza el contenido y muestra la página exactamente como aparecerá en el entorno de publicación.

## Bloquear una página   {#locking-a-page}

AEM le permite bloquear páginas para que nadie más pueda modificar su contenido. Esta función es útil cuando realice muchas ediciones en una página concreta o cuando tenga que congelar una página durante un rato.

Las páginas se pueden bloquear desde las ubicaciones siguientes:

* consola **Sitios**

   1. Seleccione la página con [modo de selección](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
   1. Seleccione el icono de bloqueo.

  ![screen_shot_2018-03-22at134928](assets/screen_shot_2018-03-22at134928.png)

* **Editor de página**

   1. Seleccione el **Información de página** para abrir el menú.
   1. Seleccione el **Bloquear página** opción.

Una vez bloqueada, se actualiza la información de la vista de la consola y, al editar, se muestra un símbolo de bloqueo en la barra de herramientas.

![screen_shot_2018-03-22at135010](assets/screen_shot_2018-03-22at135010.png)

>[!CAUTION]
>
>El bloqueo de páginas se puede realizar cuando [suplantación de un usuario](/help/sites-administering/security.md#impersonating-another-user). Sin embargo, una página bloqueada de este modo solo puede ser desbloqueada por el usuario que se ha suplantado o por el administrador.
>
>Las páginas no se pueden desbloquear al suplantar al usuario que ha bloqueado la página.

## Desbloquear una página {#unlocking-a-page}

Desbloquear una página es muy similar a [bloquearla](#locking-a-page). Cuando una página está bloqueada, las opciones de bloqueo se sustituyen con las acciones de desbloqueo.

El menú Información de página muestra la opción **Desbloquear** y el icono Bloquear de la consola Sitios se reemplaza con el icono **Desbloquear**.

![screen_shot_2018-03-22at134942](assets/screen_shot_2018-03-22at134942.png)

>[!CAUTION]
>
>El bloqueo de páginas se puede realizar cuando [suplantación de un usuario](/help/sites-administering/security.md#impersonating-another-user). Sin embargo, una página bloqueada de este modo solo puede ser desbloqueada por el usuario que se ha suplantado o por el administrador.
>
>Las páginas no se pueden desbloquear al suplantar al usuario que ha bloqueado la página.

## Deshacer y rehacer modificaciones de páginas {#undoing-and-redoing-page-edits}

Los iconos siguientes le permiten deshacer o rehacer una acción. Se muestran en la barra de herramientas cuando corresponde:

![Deshacer y rehacer](do-not-localize/screen_shot_2018-03-23at093614.png)

>[!NOTE]
>
>El [atajo de teclado](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) `Ctrl-Z` también está disponible para deshacer las acciones de edición de página.
>
>El método abreviado de teclado `Ctrl-Y` también está disponible para rehacer las acciones de edición de página.

>[!NOTE]
>
>Consulte [Deshacer y rehacer ediciones de página: la teoría](#undoing-and-redoing-page-edits-the-theory) para ver toda la información sobre las posibilidades de deshacer y rehacer ediciones de página.

## Deshacer y rehacer ediciones de página: la teoría {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>El administrador del sistema puede [configurar varios aspectos de las funciones de Deshacer/Rehacer](/help/sites-administering/config-undo.md) según los requisitos de su instancia.

AEM almacena un historial de las acciones que realiza y la secuencia en que las realizó, de modo que puede deshacer varias acciones en el orden en que se realizaron, y también rehacerlas para volver a aplicar una o más acciones.

Si hay un elemento seleccionado en la página de contenido (por ejemplo, un componente de texto), el comando para deshacer o rehacer se aplica a dicho elemento.

El comportamiento de los comandos Deshacer y Rehacer es similar al de otros programas de software. Utilice los comandos para restaurar el estado reciente de la página web a medida que toma decisiones sobre el contenido. Por ejemplo, si mueve un párrafo de texto a una ubicación diferente en la página, puede usar el comando Deshacer para mover el párrafo a la posición original. Si, a continuación, decide que la posición anterior es mejor, utilice el comando Rehacer para &quot;deshacer la operación de deshacer&quot;.

>[!NOTE]
>
>Puede hacer lo siguiente:
>
>* Rehacer acciones siempre que no haya realizado una edición de página desde que utilizó Deshacer.
>* Deshacer un máximo de 20 acciones de edición (configuración predeterminada).
>* También utilice [Métodos abreviados del teclado](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) para deshacer y rehacer.
>

Puede utilizar las funciones Deshacer y Rehacer para los siguientes tipos de cambios de página:

* Adición, edición, eliminación y movimiento de párrafos
* Edición in situ del contenido del párrafo
* Copiar, cortar y pegar elementos dentro de una página

Los campos de formulario que representan los componentes de formulario no están pensados para tener valores especificados durante la creación de páginas. Por lo tanto, los comandos Deshacer y Rehacer no afectan a los cambios realizados en los valores de esos tipos de componentes. Por ejemplo, no se puede deshacer la selección de un valor en una lista desplegable.

>[!NOTE]
>
>Se necesitan permisos especiales para deshacer y rehacer cambios en archivos e imágenes.

>[!NOTE]
>
>El historial de cambios en archivos e imágenes dura un mínimo de diez horas. Sin embargo, más allá de este tiempo, no se garantiza la anulación de los cambios. El administrador puede cambiar el tiempo predeterminado de diez horas.
