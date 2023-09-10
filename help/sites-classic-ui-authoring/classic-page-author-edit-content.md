---
title: Edición del contenido de página
description: El contenido se añade mediante componentes que se pueden arrastrar hasta la página. Después estos se pueden editar local, mover o eliminar.
uuid: e7b65ceb-263c-46f2-91e3-11dec3a016fa
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: de321869-ebf9-41a1-8203-e12bdb088678
docset: aem65
exl-id: e1b5aea0-983c-4e7b-9d35-d7beeee45dc7
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 18%

---

# Edición del contenido de una página{#editing-page-content}

Después de crear una página (nueva o como parte de un lanzamiento o Live Copy), puede editar el contenido para realizar las actualizaciones que requiera.

El contenido se añade empleando los [componentes](/help/sites-classic-ui-authoring/classic-page-author-default-components.md) (según el tipo de contenido) que pueden arrastrarse a la página. Después estos se pueden editar local, mover o eliminar.

>[!NOTE]
>
>Su cuenta necesita el [derechos de acceso adecuados](/help/sites-administering/security.md) y [permissions](/help/sites-administering/security.md#permissions) para editar páginas; por ejemplo, añadir, editar o eliminar componentes, anotar o desbloquear.
>
>Si se producen problemas, le sugerimos que se ponga en contacto con el administrador del sistema.

## Sidekick {#sidekick}

La barra de tareas es una herramienta clave al crear páginas. Flota al crear una página, por lo que siempre es visible.

Hay varias pestañas e iconos disponibles, entre ellos:

* Componentes
* Página
* Información
* Versiones
* Flujo de trabajo
* Modos
* Andamiaje
* Client Context
* Sitios web

![chlimage_1-71](assets/chlimage_1-71.png)

Estos proporcionan acceso a una amplia selección de funcionalidades, entre las que se incluyen:

* [selección de componentes](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick)
* [mostrar referencias](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#showing-references)
* [acceso al registro de auditoría](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#audit-log)
* [modos de conmutación](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)
* [creación](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#creating-a-new-version), [restauración](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoring-a-page-version-from-sidekick) y [comparación](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#comparing-with-a-previous-version) versiones

* [publicación](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#publishing-a-page), [cancelación de publicación](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#unpublishing-a-page) una página

* [editar propiedades de página](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)

* [andamiaje](/help/sites-authoring/scaffolding.md)

* [Client Context](/help/sites-administering/client-context.md)

## Insertar un componente {#inserting-a-component}

### Insertar un componente {#inserting-a-component-1}

Después de abrir la página, puede empezar a agregar contenido. Para ello, agregue componentes (también denominados párrafos).

Para insertar un componente nuevo:

1. Existen varios métodos para seleccionar el tipo de párrafo que desea insertar:

   * Haga doble clic en el área denominada **Arrastre componentes o recursos aquí...** - el **Insertar nuevo componente** se abre la barra de herramientas. Seleccione un componente y haga clic en **OK**.

   * Arrastre un componente desde la barra de herramientas flotante (denominada barra de tareas) para insertar un nuevo párrafo.
   * Haga clic con el botón derecho en un párrafo existente y seleccione **Nuevo...** : se abre la barra de herramientas Insertar nuevo componente. Seleccione un componente y haga clic en **OK**.

   ![screen_shot_2012-02-15at115605am](assets/screen_shot_2012-02-15at115605am.png)

1. Tanto en la barra de tareas como en **Insertar nuevo componente** barra de herramientas aparece una lista de los componentes disponibles (tipos de párrafo). Pueden dividirse en varias secciones (por ejemplo, General, Columnas, etc.), que se pueden expandir según sea necesario.

   Según el entorno de producción, estas opciones pueden diferir. Para obtener información detallada sobre los componentes, consulte [Componentes predeterminados](/help/sites-classic-ui-authoring/classic-page-author-default-components.md).

1. Inserte el componente que desee en la página. A continuación, haga doble clic en el párrafo y se abrirá una ventana que le permitirá configurar el párrafo y añadir contenido.

### Inserción de un componente mediante el buscador de contenido {#inserting-a-component-using-the-content-finder}

También puede agregar un componente nuevo a la página arrastrando un recurso desde el [Buscador de contenido](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder). Esto creará automáticamente un nuevo componente del tipo adecuado que contenga el recurso.

Esto es válido para los siguientes tipos de recursos (algunos dependerán del sistema de páginas o párrafos):

| Tipo de recurso | Tipo de componente resultante |
|---|---|
| Imagen | Imagen |
| Documento | Descargar |
| Producto | Producto |
| Vídeo | Flash |

>[!NOTE]
>
>Puede configurar este comportamiento en su instalación. Consulte [Configuración de un sistema de párrafos para que, al arrastrar un recurso, se cree una instancia de componente](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) para obtener más información.

Para crear un componente arrastrando uno de los tipos de activo anteriores:

1. Asegúrese de que la página se encuentra en el modo de [**edición**.](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)
1. Abra el [Buscador de contenido](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder).
1. Arrastre el recurso en cuestión hasta la posición deseada. El [marcador de posición de componente](#componentplaceholder) le muestra dónde se colocará el componente.

   Se creará un componente, adecuado para el tipo de recurso, en la ubicación requerida; contendrá el recurso seleccionado.

1. [Edite](#editmovecopypastedelete) el componente, si es necesario.

## Edición de un componente (contenido y propiedades) {#editing-a-component-content-and-properties}

Para editar un párrafo existente, realice una de las siguientes acciones:

* **Doble clic** el párrafo para abrirlo. Verá la misma ventana que cuando creó el párrafo con el contenido existente. Realice los cambios y haga clic en **OK**.

* **Clic con el botón derecho** Seleccione el párrafo y haga clic en **Editar**.

* **Clic** dos veces en el párrafo (un doble clic lento) para entrar en el modo de edición in-situ. Podrá editar directamente el texto de la página, en lugar de hacerlo desde una ventana de diálogo. En este modo, se le proporcionará una barra de herramientas en la parte superior de la página. Simplemente realice los cambios y se guardarán automáticamente.

## Mover un componente {#moving-a-component}

Para mover un párrafo:

>[!NOTE]
>
>También puede utilizar [Cortar y pegar](#cut-copy-paste-a-component) para mover un componente.

1. Seleccione el párrafo que desea mover:

   ![screen_shot_2012-02-15at115855am](assets/screen_shot_2012-02-15at115855am.png)

1. AEM Arrastre el párrafo a la nueva ubicación: indica a dónde se puede mover el párrafo con una marca de verificación verde. Colóquelo en la ubicación que desee.
1. Se mueve el párrafo:

   ![screen_shot_2012-02-15at120030pm](assets/screen_shot_2012-02-15at120030pm.png)

## Eliminación de un componente {#deleting-a-component}

Para eliminar un párrafo:

1. Seleccione el párrafo y **clic con el botón derecho**:

   ![screen_shot_2012-02-15at120220pm](assets/screen_shot_2012-02-15at120220pm.png)

1. Seleccionar **Eliminar** en el menú. AEM WCM solicita la confirmación de que desea eliminar el párrafo, ya que esta acción no se puede deshacer.
1. Haga clic en **Aceptar**.

>[!NOTE]
>
>Si ha configurado su [Propiedades del usuario para mostrar la barra de herramientas de edición global](/help/sites-classic-ui-authoring/author-env-user-props.md) también puede realizar determinadas acciones en los párrafos utilizando la variable **Copiar**, **Cortar**, **Pegar**, **Eliminar** botones disponibles.
>
>Varios [métodos abreviados del teclado](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) también están disponibles.

## Cortar/copiar/pegar un componente {#cut-copy-paste-a-component}

Como cuando [Eliminación de un componente](#deleting-a-component) puede utilizar el menú contextual para copiar, cortar o pegar un componente

>[!NOTE]
>
>Si ha configurado su [Propiedades del usuario para mostrar la barra de herramientas de edición global](/help/sites-classic-ui-authoring/author-env-user-props.md) también puede realizar determinadas acciones en los párrafos utilizando la variable **Copiar**, **Cortar**, **Pegar**, **Eliminar** botones disponibles.
>
>Varios [métodos abreviados del teclado](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) también están disponibles.

>[!NOTE]
>
>Cortar, copiar y pegar contenido solo es compatible dentro de la misma página.

## Componentes heredados {#inherited-components}

Los componentes heredados pueden ser el producto de distintos escenarios, como por ejemplo:

* [Administración de varios sitios](/help/sites-administering/msm.md); también en combinación con [andamiaje](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md#scaffolding-with-msm-inheritance).

* [Lanzamientos](/help/sites-classic-ui-authoring/classic-launches.md) (cuando se basa en livecopy).
* Componentes específicos; por ejemplo, el sistema de párrafos heredado dentro de Geometrixx.

Puede cancelar (y volver a habilitar) la herencia. Según el componente, esto puede estar disponible en:

1. **Live Copy**

   Si un componente forma parte de una Live Copy o un lanzamiento, se indica mediante un icono de candado. Puede hacer clic en el candado para cancelar la herencia.

   * El icono de candado se muestra cuando se selecciona el componente; por ejemplo:

   ![chlimage_1-72](assets/chlimage_1-72.png)

   * El candado también se muestra en el cuadro de diálogo de componentes; por ejemplo:

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. **Un sistema de párrafos heredado**

   El cuadro de diálogo Configuración. Por ejemplo, como con el sistema de párrafos heredado en Geometrixx:

   ![chlimage_1-74](assets/chlimage_1-74.png)

## Agregar anotaciones {#adding-annotations}

[Anotaciones](/help/sites-classic-ui-authoring/classic-page-author-annotations.md) permite que otros autores proporcionen comentarios sobre el contenido. Esto se utiliza a menudo con fines de revisión y validación.

## Previsualizar páginas   {#previewing-pages}

Hay dos iconos en el borde inferior de la barra de tareas que son importantes para obtener una vista previa de las páginas:

![Borde inferior de la barra de tareas con una fila horizontal de siete iconos. Dos de los iconos al principio de la fila, el icono de edición y el icono de modo de vista previa, se indican mediante un símbolo de lápiz y un símbolo de lupa, respectivamente.](do-not-localize/chlimage_1-5.png)

* El icono de lápiz le muestra que está actualmente en modo de edición, donde puede agregar, modificar, mover o eliminar contenido.

  ![Icono de edición indicado por un símbolo de lápiz.](do-not-localize/chlimage_1-6.png)

* El icono de lupa le permite seleccionar el modo de vista previa en el que la página se muestra tal y como se verá en el entorno de publicación (a veces también es necesario actualizar la página):

  ![Icono de modo de vista previa indicado por un símbolo de lupa.](do-not-localize/chlimage_1-7.png)

  En el modo de vista previa, se reducirá la barra de tareas y haga clic en el icono de flecha abajo para volver al modo de edición:

  ![AEM Barra con el título y un icono de modo de edición a la derecha del título, que se indica con un símbolo de flecha hacia abajo.](do-not-localize/chlimage_1-8.png)

## Buscar y reemplazar {#find-replace}

Para ediciones a mayor escala de la misma frase a **[Buscar y reemplazar](/help/sites-classic-ui-authoring/author-env-search.md#find-and-replace)** La opción de menú permite buscar y reemplazar varias instancias de una cadena, dentro de una sección del sitio web.

## Bloquear una página   {#locking-a-page}

AEM permite bloquear páginas para que nadie más pueda modificar su contenido. Esto resulta útil cuando realice muchas ediciones en una página concreta o cuando tenga que congelar una página durante un rato.

>[!CAUTION]
>
>El bloqueo de páginas debe utilizarse con cuidado, ya que la única persona que puede desbloquear una página es la persona que la bloqueó (o una cuenta con privilegios de administrador).

Para bloquear una página:

1. En el **Sitios web** , seleccione la página que desea bloquear.
1. Haga doble clic en la página para abrirla y editarla.
1. En el **Página** pestaña de la barra de tareas, seleccione **Bloquear página**:

   ![screen_shot_2012-02-08at15750pm](assets/screen_shot_2012-02-08at15750pm.png)

   Aparece un mensaje que indica que la página está bloqueada para otros usuarios. Además, en el panel derecho del **Sitios web** AEM , WCM muestra la página como bloqueada e indica qué usuario ha bloqueado la página.

   ![screen_shot_2012-02-08at20657pm](assets/screen_shot_2012-02-08at20657pm.png)

## Desbloquear una página {#unlocking-a-page}

Para desbloquear una página:

1. En el **Sitios web** , seleccione la página que desea desbloquear.
1. Haga doble clic en la página para abrirla.
1. En el **Página** pestaña de la barra de tareas, seleccione **Desbloquear página**.

## Deshacer y rehacer modificaciones de páginas {#undoing-and-redoing-page-edits}

Utilice los siguientes métodos abreviados del teclado mientras el marco de contenido de la página está seleccionado:

* Deshacer: Ctrl+Z (Windows) o Cmd+Z (Mac)
* Rehacer: Ctrl+Y (Windows) o Cmd+Y (Mac)

Al deshacer o rehacer la eliminación, adición o reubicación de uno o más párrafos, los resaltados parpadeantes (comportamiento predeterminado) indican los párrafos afectados.

>[!NOTE]
>
>Consulte [Deshacer y rehacer ediciones de página: la teoría](#undoing-and-redoing-page-edits-the-theory) para ver toda la información sobre las posibilidades de deshacer y rehacer ediciones de página.

## Deshacer y rehacer ediciones de página: la teoría {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>El administrador del sistema puede [configurar varios aspectos de las funciones de Deshacer/Rehacer](/help/sites-administering/config-undo.md) según los requisitos de su instancia.

AEM Almacena un historial de las acciones que realiza y la secuencia en que las realizó. Por lo tanto, deshace varias acciones en el orden en que las realizó. A continuación, puede utilizar rehacer para volver a aplicar una o varias acciones.

Si hay un elemento seleccionado en la página de contenido, el comando Deshacer y Rehacer se aplica al elemento seleccionado, como un componente de texto.

El comportamiento de los comandos Deshacer y Rehacer es similar al de otros programas de software. Utilice los comandos para restaurar el estado reciente de la página web a medida que toma decisiones sobre el contenido. Por ejemplo, si mueve un párrafo de texto a una ubicación diferente en la página, puede usar el comando Deshacer para mover el párrafo a la posición original. Si, a continuación, decide volver a mover el párrafo, utilice el comando Rehacer.

>[!NOTE]
>
>Puede hacer lo siguiente:
>
>* rehacer acciones siempre que no haya realizado una edición de página desde que utilizó deshacer.
>* deshacer un máximo de 20 acciones de edición (configuración predeterminada).
>* también utilice [Métodos abreviados del teclado](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) para deshacer y rehacer.
>

Puede usar los comandos Deshacer y Rehacer para los siguientes tipos de cambios de página:

* Añadir, editar, quitar y mover párrafos
* Editar contenido de párrafos in-situ
* Copiar, cortar y pegar elementos en una página
* Copiar, cortar y pegar elementos en las páginas
* Agregar, quitar y cambiar archivos e imágenes
* Adición, eliminación y cambio de anotaciones y bocetos
* Cambios en el andamiaje
* Adición y eliminación de referencias
* Cambiar valores de propiedad en cuadros de diálogo de componentes.

Los campos de formulario que representan los componentes de formulario no están pensados para tener valores especificados durante la creación de páginas. Por lo tanto, los comandos Deshacer y Rehacer no afectan a los cambios realizados en los valores de esos tipos de componentes. Por ejemplo, no se puede deshacer la selección de un valor en una lista desplegable.

>[!NOTE]
>
>Se necesitan permisos especiales para deshacer y rehacer cambios en archivos e imágenes. Además, el historial de deshacer para cambios en archivos e imágenes dura un mínimo de horas. No obstante, pasado ese tiempo, no se garantiza que se puedan deshacer los cambios. El administrador puede proporcionar permisos y cambiar el tiempo predeterminado de diez horas.
