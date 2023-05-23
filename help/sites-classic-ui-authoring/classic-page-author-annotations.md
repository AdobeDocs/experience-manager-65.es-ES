---
title: Anotaciones al editar una página
description: La adición de contenido a las páginas del sitio web suele estar sujeta a discusiones antes de que se publique. Para ayudarle, muchos componentes directamente relacionados con el contenido le permiten añadir una anotación.
page-status-flag: de-activated
uuid: d8d6ba76-f2aa-4044-98bf-5d506742d90d
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9bee0197-f275-49cc-922d-62cba826c4e5
exl-id: d60e9601-d15b-4378-a33e-e90961f63195
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 7%

---

# Anotaciones al editar una página{#annotations-when-editing-a-page}

La adición de contenido a las páginas del sitio web suele estar sujeta a discusiones antes de que se publique. Para ayudarle, muchos componentes directamente relacionados con el contenido (a diferencia, por ejemplo, del diseño) le permiten añadir una anotación.

Una anotación coloca un marcador de color/nota adhesiva en la página. La anotación le permite (a usted o a otros usuarios) dejar comentarios o preguntas para otros autores o revisores.

>[!NOTE]
>
>La definición de un tipo de componente individual determina si se puede añadir una anotación o no en instancias de dicho componente.

>[!NOTE]
>
>Las anotaciones creadas en la IU clásica también se mostrarán en la IU táctil optimizada. Sin embargo, los bocetos son específicos de la interfaz de usuario y solo se muestran en la interfaz en la que se crearon.

>[!CAUTION]
>
>Al eliminar un recurso (por ejemplo, un párrafo), se eliminan todas las anotaciones y bocetos relacionados con ese recurso, independientemente de su posición en la página en general.

>[!NOTE]
>
>Según sus necesidades, también puede desarrollar un flujo de trabajo para enviar notificaciones cuando estas se añadan, actualicen o eliminen.

## Anotaciones {#annotations}

Según el diseño del párrafo, la anotación está disponible como opción en el menú contextual (normalmente, el botón derecho del ratón al pasar el ratón por encima del párrafo requerido) o como botón en la barra de edición del párrafo.

En cualquier caso, seleccione **Anotar**. Se aplicará una anotación de nota adhesiva de color al párrafo; se encuentra inmediatamente en el modo Editar, lo que le permite agregar texto directamente:

![chlimage_1-137](assets/chlimage_1-137.png)

Puede mover la anotación a una nueva posición en la página. Haga clic en el área de borde superior, luego mantenga presionada y arrastre simultáneamente la anotación a la nueva posición. Puede estar en cualquier parte de la página, aunque suele ser importante mantenerla conectada al párrafo de alguna manera.

Las anotaciones (incluidos los bocetos relacionados) también se incluyen en las acciones de copia, corte o eliminación realizadas en el párrafo al que están adjuntas; en el caso de las acciones de copia o corte, la posición de la anotación (y los bocetos relacionados) conserva su posición en relación con el párrafo de origen.

El tamaño de la anotación también se puede aumentar o reducir arrastrando la esquina inferior derecha.

Para fines de seguimiento, la línea de pie de página indicará el usuario que creó la anotación y la fecha. Los autores posteriores pueden editar la misma anotación (se actualizará el pie de página) o crear una nueva anotación para el mismo párrafo.

Se solicitará confirmación cuando seleccione eliminar la anotación (al eliminar una anotación, también se eliminan los bocetos adjuntos a esa anotación).

Los tres iconos de la parte superior izquierda le permiten minimizar la anotación (junto con cualquier boceto relacionado), cambiar el color y añadir bocetos.

>[!NOTE]
>
>Las anotaciones solo están visibles en el modo de edición del entorno de creación.
>
>No son visibles en un entorno de publicación, ni en los modos de Previsualización o Diseño disponibles en un entorno de creación.

>[!NOTE]
>
>Las anotaciones no se pueden agregar a una página que otro usuario haya bloqueado.

## Bocetos de anotación {#annotation-sketches}

>[!NOTE]
>
>Los bocetos no están disponibles en Internet Explorer, por lo que:
>
>* el icono no se mostrará.
>* los bocetos existentes, creados en otro navegador, no se mostrarán.
>


Los bocetos son una función de las anotaciones que le permiten crear gráficos de línea simples en cualquier parte de la ventana del explorador (parte visible):

![chlimage_1-138](assets/chlimage_1-138.png)

* El cursor cambiará a una cruz cuando esté en modo de esbozo. Puede dibujar varias líneas distintas.
* La línea del boceto refleja el color de la anotación y puede ser:

   * a pulso

      el modo predeterminado; termine soltando el botón del mouse.

   * recto:

      mantener presionado `ALT` y haga clic en los puntos inicial y final; finalice con un doble clic.

* Una vez que haya salido del módulo de esbozo, puede pulsar en una línea de esbozo para seleccionarla.
* Para mover un boceto, selecciónelo y arrástrelo a la posición que desee.
* Un boceto superpone el contenido. Esto significa que dentro de las 4 esquinas del boceto no puede hacer clic en el párrafo subyacente; por ejemplo, si necesita editar o acceder a un vínculo. Si esto se convierte en un problema (por ejemplo, si tiene un boceto que cubre una gran área de la página), minimice la anotación adecuada, ya que esto también minimizará todos los bocetos relacionados, lo que le dará acceso al área subyacente.
* Para eliminar un boceto individual, seleccione el boceto necesario y, a continuación, pulse la tecla **Eliminar** clave (**fan**-**retroceso** en un MAC).

* Si mueve o copia un párrafo, las anotaciones relacionadas y sus bocetos también se moverán o copiarán; su posición en relación con el párrafo seguirá siendo la misma.
* Si elimina una anotación, también se eliminarán todos los bocetos adjuntos a esa anotación.
