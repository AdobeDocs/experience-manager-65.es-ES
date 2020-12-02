---
title: Anotaciones al editar una página
seo-title: Anotaciones al editar una página
description: La adición de contenido a las páginas de un sitio web suele someterse a análisis antes de publicarse. Para facilitar las cosas, muchos componentes directamente relacionados con el contenido permiten agregar anotaciones.
seo-description: La adición de contenido a las páginas de un sitio web suele someterse a análisis antes de publicarse. Para facilitar las cosas, muchos componentes directamente relacionados con el contenido permiten agregar anotaciones.
page-status-flag: de-activated
uuid: d8d6ba76-f2aa-4044-98bf-5d506742d90d
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9bee0197-f275-49cc-922d-62cba826c4e5
translation-type: tm+mt
source-git-commit: c8a02ad9fc33e963d2c760840e70c40ede988054
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 95%

---


# Anotaciones al editar una página{#annotations-when-editing-a-page}

La adición de contenido a las páginas de un sitio web suele someterse a análisis antes de publicarse. Para ayudarle, muchos componentes directamente relacionados con el contenido (en vez de, por ejemplo, el diseño) permiten añadir anotaciones.

Una anotación coloca un marcador o una nota adhesiva de colores en la página. La anotación le permite (a usted o a otros usuarios) dejar comentarios o preguntas para otros autores o revisores.

>[!NOTE]
>
>La definición de un tipo de componente individual determina si se puede añadir una anotación o no en instancias de dicho componente.

>[!NOTE]
>
>Las anotaciones creadas en la IU clásica también se muestran en la IU táctil. Sin embargo, los esbozos son específicos de la IU y solo se muestran en la interfaz en la que se crearon.

>[!CAUTION]
>
>Al eliminar un medio (p. ej. un párrafo), se eliminan todas las anotaciones y los bocetos relacionados con ese medio, independientemente de su posición en la página en general.

>[!NOTE]
>
>Según sus necesidades, también puede desarrollar un flujo de trabajo para enviar notificaciones cuando se agregan, actualicen o eliminen anotaciones.

## Anotaciones {#annotations}

Dependiendo del diseño del párrafo, la anotación está disponible como opción en el menú contextual (generalmente con el botón derecho del ratón cuando se sitúa sobre el párrafo necesario) o como botón en la barra de edición de párrafos.

En cualquier caso, seleccione **Anotar**. Se aplicará al párrafo una anotación en forma de nota adhesiva de colores; entrará inmediatamente en el modo de edición y podrá añadir texto directamente:

![chlimage_1-137](assets/chlimage_1-137.png)

La anotación se puede mover a una nueva posición de la página. Haga clic en el área del borde superior y después mantenga y arrastre al mismo tiempo la anotación a la nueva posición. Se puede situar en cualquier lugar de la página, aunque suele ser adecuado conectarla al párrafo de algún modo.

Las anotaciones (incluyendo los bocetos relacionados) también se incluyen en cualquier acción de copia, corte o eliminación que se realice en el párrafo al que estén relacionadas; para las operaciones de copia o corte, la posición de la anotación (y de los bocetos relacionados) sigue siendo la misma en relación con el párrafo original.

El tamaño de la anotación también se puede aumentar o reducir arrastrando la esquina inferior derecha.

Para realizar un seguimiento, el pie de página indicará el usuario que creó la anotación y la fecha. Los siguientes autores puede editar la misma anotación (el pie de página se actualizará) o crear una nueva para el mismo párrafo.

La confirmación se solicitará cuando opte por eliminar la anotación (con la eliminación de una anotación también se eliminan todos los bocetos relacionados con la misma).

Los tres iconos situados en la parte izquierda permiten minimizar la anotación (junto con los bocetos relacionados), cambiar el color y añadir bocetos.

>[!NOTE]
>
>Las anotaciones solo se pueden ver en el modo de edición del entorno de creación.
>
>No están visibles en un entorno de publicación ni en los modos de diseño o previsualización disponibles en un entorno de creación.

>[!NOTE]
>
>Las anotaciones no se pueden agregar a una página que otro usuario haya bloqueado.

## Anotación de bocetos {#annotation-sketches}

>[!NOTE]
>
>Los bocetos no están disponibles en Internet Explorer, por lo tanto:
>
>* El icono no se mostrará.
>* Los bocetos existentes, creados en otro navegador, no aparecerán.

>



Los bocetos son una función de las anotaciones que permiten crear sencillos gráficos de línea en cualquier lugar de la ventana de navegación (parte visible):

![chlimage_1-138](assets/chlimage_1-138.png)

* El cursor cambiará a una cruz cuando se esté en modo de boceto. Puede dibujar varias líneas distintas.
* Las líneas del boceto reflejan el color de la anotación y pueden ser:

   * A mano alzada.

      Modo predeterminado; termine soltando el botón del ratón.

   * Rectas:

      Mantenga presionada la tecla `ALT` y haga clic en los puntos de inicio y fin; termine con un doble clic.

* Una vez que haya salido del modo de boceto, puede hacer clic en una línea de boceto para seleccionarlo.
* Mueva el boceto seleccionándolo y arrastrándolo a la posición deseada.
* Los bocetos se superponen en el contenido. Esto significa que dentro de las 4 esquinas del boceto no se puede hacer clic en el párrafo subyacente; por ejemplo, si necesita editar o acceder a un vínculo. Si esto supone un problema (por ejemplo, un boceto cubre un área grande de la página), minimice la anotación correspondiente y también se reducirán todos los bocetos relacionados, por lo que podrá acceder al área subyacente.
* Para eliminar un boceto individual, selecciónelo y después presione la tecla **Supr** (**fn**-**retroceso** en un MAC).

* Si mueve o copia un párrafo, todas las anotaciones relacionadas y sus bocetos también se moverán o copiarán; su posición en relación con el párrafo seguirá siendo la misma.
* Si se elimine una anotación, todos los bocetos adjuntos a la anotación también se borrarán.

