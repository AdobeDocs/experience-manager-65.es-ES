---
title: 'Uso de versiones de página  '
seo-title: 'Uso de versiones de página  '
description: Cree, compare y restaure versiones de una página
seo-description: Cree, compare y restaure versiones de una página
uuid: 29e049f0-532c-4e3b-b64f-5be88ee6b08c
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1368347a-9b65-4cfc-87e1-62993dc627fd
docset: aem65
exl-id: cb7a9da2-7112-4ef0-b1cf-211a7df93625
source-git-commit: 4d5f7057178ea0a1f00ea363b76dacdfb714b5e3
workflow-type: tm+mt
source-wordcount: '1487'
ht-degree: 69%

---

# Uso de versiones de página  {#working-with-page-versions}

Al generar una versión, se crea una “instantánea” de una página en un punto específico del tiempo. Con la función de versiones, se pueden realizar las siguientes operaciones:

* Crear una versión de la página.
* Restaurar una página a una versión anterior, por ejemplo, para deshacer un cambio realizado en ella.
* Comparar la versión actual de una página con una versión anterior resaltando las diferencias en el texto y las imágenes. 

## Creación de una nueva versión   {#creating-a-new-version}

Puede crear una versión de su recurso desde:

* el [raíl de la línea de tiempo](#creating-a-new-version-timeline)
* la opción [Crear](#creating-a-new-version-create-with-a-selected-resource) (cuando hay un recurso seleccionado)

### Crear una nueva versión: línea de tiempo {#creating-a-new-version-timeline}

1. Desplácese para mostrar la página para la que desea crear una versión.
1. Seleccione la página en [modo de selección](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Abra la columna **Línea de tiempo**.
1. Toque o haga clic en la punta de la flecha junto al campo de comentarios para mostrar las opciones:

   ![screen-shot_2019-03-05at112335](assets/screen-shot_2019-03-05at112335.png)

1. Seleccione **Guardar como versión**.
1. Si procede, introduzca un valor en **Etiqueta** y en **Comentario**.

   ![imagen_1-42](assets/chlimage_1-42.png)

1. Confirme la nueva versión con **Crear**.

   La información en la línea de tiempo se actualizará para indicar la nueva versión.

### Crear una nueva versión: creación con un recurso seleccionado {#creating-a-new-version-create-with-a-selected-resource}

1. Desplácese para mostrar la página para la que desea crear una versión.
1. Seleccione la página en [modo de selección](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Seleccione la opción **Crear** en la barra de herramientas.
1. Se abrirá el cuadro de diálogo. Si procede, puede introducir un valor **Etiqueta** y **Comentario:**

   ![screen_shot_2012-02-15at105050am](assets/screen_shot_2012-02-15at105050am.png)

1. Confirme la nueva versión con **Crear**.

   La línea de tiempo se abrirá con información actualizada para indicar la nueva versión. 

## Restablecimiento de versiones {#reinstating-versions}

Una vez creada una versión de la página, existen varios métodos para restablecer una versión anterior:

* la opción **Revertir a esta versión** del carril [Línea de tiempo](/help/sites-authoring/basic-handling.md#timeline)

   Restablezca una versión anterior de una página seleccionada.

* las opciones **Restaurar** de la barra de herramientas de acciones [superior](/help/sites-authoring/basic-handling.md#actions-toolbar)

   * **Restaurar versión**

      Restablecer versiones de páginas especificadas dentro de la carpeta seleccionada actualmente; esto también puede incluir la restauración de páginas que se han eliminado anteriormente.

   * **Restaurar árbol**

      Restablecer una versión de todo un árbol en una fecha y hora especificadas; esto puede incluir páginas que se han eliminado anteriormente.

>[!NOTE]
>
>Al restablecer una página, la versión creada formará parte de una rama nueva.
>
>Como ejemplo:
>
>1. Cree una versión de una página cualquiera.
>1. Las etiquetas y los nombres de nodo iniciales serán 1.0., 1.1, 1.2, etc.
>1. Restablecer la primera versión; es decir, 1.0.
>1. Vuelva a crear versiones nuevas.
>1. Las etiquetas generadas y los nombres de nodo ahora serán 1.0.0, 1.0.1, 1.0.2, etc.


### Revertir a una versión {#revert-to-a-version}

Para **Revertir** la página seleccionada a una versión anterior:

1. Desplácese para mostrar la página que quiere revertir a una versión anterior.
1. Seleccione la página en [modo de selección](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Abra la columna **Línea de tiempo** y seleccione **Mostrar todo** o **Versiones**. Se enumerarán las versiones de página de la página seleccionada.
1. Seleccione la versión a la que desee revertir. Se mostrarán las opciones posibles:

   ![Volver a esta versión](assets/screen-shot_2019-03-05at112505.png)

1. Seleccione **Revertir a esta versión**. Se restaurará la versión seleccionada y se actualizará la información en la línea de tiempo.

### Restaurar versión {#restore-version}

Este método se puede utilizar para restaurar versiones de páginas especificadas dentro de la carpeta actual; esto también puede incluir la restauración de páginas que se han eliminado anteriormente:

1. Vaya a la carpeta requerida y [seleccione](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).

1. Seleccione **Restaurar** y, a continuación, **Restaurar versión** en la barra de herramientas de acciones](/help/sites-authoring/basic-handling.md#actions-toolbar) superior.[

   >[!NOTE]
   >
   >Si:
   >
   >* ha seleccionado una sola página, que nunca ha tenido páginas secundarias,
   >* o ninguna de las páginas de la carpeta tiene versiones,

   >
   >A continuación, la pantalla estará vacía ya que no hay versiones aplicables.

1. Se enumerarán las versiones disponibles:

   ![Restaurar versión: lista de todas las páginas de la carpeta](/help/sites-authoring/assets/versions-restore-version-01.png)

1. Para una página específica, utilice el selector desplegable en **RESTAURAR A VERSIÓN** para seleccionar la versión requerida para esa página.

   ![Restaurar versión: seleccionar versión](/help/sites-authoring/assets/versions-restore-version-02.png)

1. En la pantalla principal, seleccione la página requerida para la restauración:

   ![Restaurar versión: seleccionar página](/help/sites-authoring/assets/versions-restore-version-03.png)

1. Seleccione **Restaurar** para la versión seleccionada, de la página seleccionada, que se restaurará como versión actual.

>[!NOTE]
>
>El orden en que se selecciona una página requerida y la versión relacionada son intercambiables.

### Restaurar árbol {#restore-tree}

Este método puede utilizarse para restaurar una versión de un árbol en una fecha y hora especificadas; esto puede incluir páginas que se han eliminado anteriormente:

1. Vaya a la carpeta requerida y [seleccione](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).

1. Seleccione **Restaurar** y, a continuación, **Restaurar árbol** en la barra de herramientas de acciones](/help/sites-authoring/basic-handling.md#actions-toolbar) superior. [ Se mostrará la última versión del árbol:

   ![Restaurar árbol](/help/sites-authoring/assets/versions-restore-tree-02.png)

1. Utilice el selector de fecha y hora **Últimas versiones en fecha** para seleccionar otra versión del árbol: la que se va a restaurar.

1. Establezca el indicador **Páginas sin versiones conservadas** según sea necesario:

   * Si está activo (seleccionado), las páginas sin versiones se mantendrán y no se verán afectadas por la restauración.

   * Si está inactivo (sin seleccionar), todas las páginas sin versiones se eliminarán, ya que no existían en el árbol con versiones.

1. Seleccione **Restaurar** para que la versión seleccionada del árbol se restaure como la versión *actual*.

## Vista previa de una versión    {#previewing-a-version}

Puede previsualizar una versión específica:

1. Desplácese para mostrar la página que desea comparar.
1. Seleccione la página en [modo de selección](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Abra la columna **Línea de tiempo** y seleccione **Mostrar todo** o **Versiones**.
1. Se enumerarán las versiones de la página. Seleccione la versión que quiere previsualizar:

   ![screen-shot_2019-03-05at112505-1](assets/screen-shot_2019-03-05at112505-1.png)

1. Seleccione **Vista previa**. La página se muestra en una nueva pestaña.

   >[!CAUTION]
   >
   >Si se ha movido una página, ya no podrá realizar vistas previas en ninguna versión realizada antes del movimiento.
   >
   >* Si tiene problemas con una vista previa, compruebe la [línea de tiempo](/help/sites-authoring/basic-handling.md#timeline) para ver si la página se ha movido.


## Comparar una versión con la página actual {#comparing-a-version-with-current-page}

Para comparar una versión anterior con la página actual:

1. Desplácese para mostrar la página que desea comparar.
1. Seleccione la página en [modo de selección](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Abra la columna **Línea de tiempo** y seleccione **Mostrar todo** o **Versiones**.
1. Se enumerarán las versiones de la página. Seleccione la versión que desee comparar:

   ![screen-shot_2019-03-05at112505-2](assets/screen-shot_2019-03-05at112505-2.png)

1. Seleccione **Comparar con actual**. Se abrirá [Diferencias de página](/help/sites-authoring/page-diff.md) para mostrar las diferencias.

## Deformación de tiempo   {#timewarp}

Deformación de tiempo es una función diseñada para simular el estado *publicado* de una página en periodos específicos en el pasado.

Debido a que la creación de contenido es un proceso continuo y colaborativo, el propósito de Deformación de tiempo es permitir que los creadores rastreen el sitio web publicado con el paso del tiempo para comprender cómo ha cambiado el contenido. Esta función emplea las versiones de página para determinar el estado del entorno de publicación.

Para ello:

* El sistema busca la versión de la página activa en el tiempo seleccionado.
* Esto significa que la versión mostrada se creó o activó *antes del* punto temporal seleccionado en Deformación de tiempo.
* Al navegar a una página que se haya eliminado, también se procesa, siempre que las versiones anteriores de la página estén disponibles en el repositorio.
* Si no se encuentran versiones publicadas, Deformación de tiempo volverá al estado actual de la página en el entorno de creación (para evitar una página de error/404, lo que impediría el examen).

### Utilizar la Deformación de tiempo {#using-timewarp}

Deformación de tiempo es un [modo](/help/sites-authoring/author-environment-tools.md#page-modes) del editor de páginas. Para iniciarlo, basta con activarlo como cualquier otro modo.

1. Inicie el editor de la página donde desee comenzar Deformación de tiempo y, a continuación, elija **Deformación de tiempo** en la selección de modo.

   ![wpv-01](assets/wwpv-01.png)

1. En el cuadro de diálogo establezca una fecha y hora de destino y pulse o haga clic en **Establecer fecha**. Si no selecciona una hora, la hora actual será la predeterminada.

   ![wpv-02](assets/wwpv-02.png)

1. La página se muestra en función de la fecha establecida. El modo Deformación de tiempo se indica mediante la barra de estado azul en la parte superior de la ventana. Utilice los vínculos de la barra de estado para seleccionar una nueva fecha de destino o para salir del modo Deformación de tiempo.

   ![wpv-03](assets/wwpv-03.png)

### Limitaciones de Deformación de tiempo {#timewarp-limitations}

Deformación de tiempo realiza el mejor esfuerzo para reproducir una página en un punto temporal seleccionado. Sin embargo, debido a las complejidades de la creación continua de contenido en AEM, esto no siempre es posible. Estas limitaciones deben tenerse en cuenta al utilizar Deformación de tiempo.

* **Deformación de tiempo funciona dependiendo de las páginas publicadas**: Deformación de tiempo solo funciona a la perfección si ya ha publicado la página. En caso contrario, Deformación de tiempo mostrará la página actual en el entorno de creación.
* **Deformación de tiempo emplea las versiones de página**: si se desplaza a una página que se ha eliminado del repositorio, se procesa correctamente si aún hay versiones antiguas de la página en el repositorio.
* **Las versiones eliminadas afectan a la función Deformación de tiempo**: si las versiones se eliminan del repositorio, Deformación de tiempo no puede mostrar resultados correctos.

* **Deformación de tiempo es de solo lectura**: no se puede editar la versión antigua de la página. Tan solo pueden visualizarse. Si desea restaurar la versión anterior, deberá hacerlo manualmente mediante la [restauración](#reverting-to-a-page-version).

* **Deformación de tiempo se basa únicamente en el contenido de la página**: si los elementos para procesar el sitio web (código, CSS, recursos e imágenes, etc.) cambian, la vista será diferente de la original, ya que no hay versiones de dichos elementos en el repositorio.

>[!CAUTION]
>
>Deformación de tiempo está diseñada como una herramienta para ayudar a los autores a comprender y crear su contenido. No se trata de un registro de auditoría ni de un registro jurídico.
