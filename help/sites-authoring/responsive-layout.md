---
title: Diseño interactivo para las páginas de contenido
description: Adobe Experience Manager le permite crear un diseño interactivo para sus páginas.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: 760b8419-5cf8-49c5-8d4f-6691f5256c53
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1798'
ht-degree: 62%

---

# Diseño adaptable{#responsive-layout}

AEM le permite tener un diseño adaptable para las páginas mediante el uso de la variable **Contenedor de diseño** componente.

Proporciona un sistema de párrafos que le permite colocar componentes en una cuadrícula adaptable. Esta cuadrícula puede reorganizar el diseño según el tamaño y el formato del dispositivo o la ventana. El componente se utiliza junto con el [**Diseño** modo](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode), que le permite crear y editar su diseño interactivo en función del dispositivo.

El contenedor de diseño:

* Proporciona un ajuste horizontal a la cuadrícula, junto con la capacidad de colocar componentes en la cuadrícula en paralelo y definir cuándo deben contraerse o redistribuirse.
* Utiliza puntos de interrupción predefinidos (por ejemplo, para un teléfono, una tableta, etc.) para permitirle definir el comportamiento del contenido necesario para la orientación o los dispositivos relacionados.

   * Por ejemplo, puede personalizar el tamaño del componente o si el componente se puede ver en dispositivos específicos.

* Se puede anidar para permitir el control de columnas.

A continuación, el usuario puede ver cómo se representará el contenido para dispositivos específicos mediante el emulador.

>[!CAUTION]
>
>Aunque el componente Contenedor de diseño está disponible en la IU clásica, su funcionalidad completa solo está disponible y es compatible con la IU táctil.

AEM realiza un diseño interactivo para sus páginas mediante una combinación de diferentes mecanismos:

* Componente [**Contenedor de diseño**](#adding-a-layout-container-and-its-content-edit-mode)

  Este componente está disponible en el [navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser) y proporciona un sistema de párrafos de cuadrícula que le permite agregar y colocar componentes en una cuadrícula adaptable. También se puede establecer como sistema de párrafos predeterminado en la página.

* [**Modo de diseño**](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)

  Después de colocar el contenedor de diseño en la página, puede usar el modo de **diseño** para colocar el contenido en la red interactiva.

* [**Emulador**](#selecting-a-device-to-emulate)
Esto permite crear y editar sitios web interactivos que reorganizan el diseño según el tamaño del dispositivo o la ventana, mediante el cambio de tamaño de los componentes de forma interactiva. A continuación, el usuario puede ver cómo se representará el contenido mediante el emulador.

Con estos mecanismos de cuadrícula adaptable puede hacer lo siguiente:

* Utilizar puntos de interrupción para definir diferentes diseños de contenido según la anchura del dispositivo (en relación con el tipo y la orientación del dispositivo).
* Utilizar estos mismos puntos de interrupción y diseños de contenido para asegurarse de que el contenido es adaptable al tamaño de la ventana del navegador en el escritorio.
* Utilizar el ajuste horizontal a la cuadrícula que le permite colocar componentes en la cuadrícula, cambiar su tamaño según sea necesario y definir cuándo deben contraerse o redistribuirse lateralmente o arriba/abajo.
* Ocultar componentes de diseños de dispositivo específicos.
* Realizar el control de columnas.

En función del proyecto, el contenedor de diseño se puede utilizar como sistema de párrafos predeterminado para las páginas o como componente disponible para añadirse a su página mediante el explorador de componentes (o ambos).

>[!NOTE]
>
>El Adobe proporciona [Documentación de GitHub](https://adobe-marketing-cloud.github.io/aem-responsivegrid/) AEM AEM del diseño interactivo como referencia que se puede dar a los desarrolladores de front-end para que puedan utilizar la cuadrícula de la fuera de la red de la interfaz de usuario de, por ejemplo, al crear maquetas de HTML AEM estáticos para un sitio futuro en el que se vaya a realizar un seguimiento de la interfaz de usuario de la interfaz de usuario de la aplicación de red.

>[!NOTE]
>
>El uso de los mecanismos anteriores se habilita en la configuración de la plantilla. Consulte [Configuración del diseño interactivo](/help/sites-administering/configuring-responsive-layout.md) para obtener más información.

## Definiciones de diseños, emulación de dispositivos y puntos de interrupción {#layout-definitions-device-emulation-and-breakpoints}

Al crear el contenido de su sitio web desea asegurarse de que el contenido se muestre correctamente según el dispositivo utilizado para ello.

AEM definir diseños según la anchura del dispositivo:

* El emulador permite emular estos diseños en una amplia gama de dispositivos. Además del tipo de dispositivo, la orientación, que se selecciona mediante la opción **Rotar dispositivo**, puede afectar al punto de interrupción seleccionado a medida que cambia la anchura.
* Los puntos de interrupción son puntos que separan las definiciones de diseño.

   * Definen efectivamente la anchura máxima (en píxeles) de cualquier dispositivo que utilice un diseño específico.
   * Normalmente, los puntos de interrupción son válidos para una selección de dispositivos, en función del ancho de sus pantallas.
   * El alcance de un punto de interrupción se extiende hacia la izquierda hasta el siguiente punto de interrupción.
   * No puede seleccionar específicamente un punto de interrupción; al seleccionar el dispositivo y la orientación se selecciona automáticamente el punto de interrupción adecuado.

El dispositivo **Escritorio** no tiene una anchura específica y está relacionado con el punto de interrupción predeterminado (por ejemplo, todo lo que está por encima del último punto de interrupción configurado).

>[!NOTE]
>
>Es posible definir puntos de interrupción para cada dispositivo individual, pero esto incrementaría drásticamente los trabajos de definición de diseño y mantenimiento.

Al seleccionar en el emulador un dispositivo específico para emular y definir el diseño, el punto de interrupción relacionado también quedará resaltado. Cualquier cambio de diseño que realice se aplicará a otros dispositivos a los que se aplique el punto de interrupción, es decir, cualquier dispositivo situado a la izquierda del marcador del punto de interrupción activo, pero antes del marcador del siguiente punto de interrupción.

Por ejemplo, si selecciona el dispositivo **iPhone 6 Plus** (definido con una anchura de 540 píxeles) para emulación y diseño, se activará también el punto de interrupción **Teléfono** (definido como 768 píxeles). Cualquier cambio de diseño que realice en **IPHONE 6** será aplicable a otros dispositivos bajo el **Teléfonos** punto de interrupción, como **IPHONE 5** (definido como 320 píxeles).

![screen_shot_2018-03-23at084058](assets/screen_shot_2018-03-23at084058.png)

## Selección de un dispositivo para emular {#selecting-a-device-to-emulate}

1. Abra la página necesaria para editarla. Por ejemplo:

   `http://localhost:4502/editor.html/content/we-retail/us/en/experience.html`

1. Seleccione el icono **Emulador** de la barra de herramientas superior:

   ![Emulador](do-not-localize/screen_shot_2018-03-23at084256.png)

1. Se abrirá la barra de herramientas del emulador.

   ![screen_shot_2018-03-23at084551](assets/screen_shot_2018-03-23at084551.png)

   La barra de herramientas del emulador muestra opciones de diseño adicionales:

   * **Rotar dispositivo** : Permite girar un dispositivo desde la orientación vertical (vertical) a la horizontal (horizontal) y a la inversa.

     ![Rotar dispositivo](do-not-localize/screen_shot_2018-03-23at084612.png) ![Rotar dispositivo](do-not-localize/screen_shot_2018-03-23at084637.png)

   * **Seleccionar dispositivo**: le permite definir un dispositivo específico para emular de una lista (consulte el paso siguiente para obtener detalles)

     ![Seleccionar dispositivo](do-not-localize/screen_shot_2018-03-23at084743.png)

1. Para seleccionar un dispositivo específico para emular, puede hacer lo siguiente:

   * Utilizar el icono Seleccionar dispositivo y seleccionarlo desde un selector desplegable.
   * Haga clic en el indicador de dispositivo en la barra de herramientas del emulador.

   ![screen_shot_2018-03-23at084818](assets/screen_shot_2018-03-23at084818.png)

1. Una vez que haya seleccionado un dispositivo específico, puede:

   * Ver el marcador activo del dispositivo seleccionado; por ejemplo, **iPad.**
   * Ver el marcador activo del [punto de interrupción](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) adecuado; por ejemplo, **Tableta.**

   ![screen_shot_2018-03-23at084932](assets/screen_shot_2018-03-23at084932.png)

   * La línea discontinua azul representa el *doblar* para el dispositivo seleccionado (aquí un **IPHONE 6**).

   ![screen_shot_2018-03-23at084947](assets/screen_shot_2018-03-23at084947.png)

   * El pliegue también se puede considerar el salto de línea de la página (no confundir con los [puntos de interrupción](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints)) del contenido. Esto se muestra para mayor comodidad, a fin de mostrar qué parte del contenido verá el usuario en el dispositivo antes de desplazarse.
   * La línea para el pliegue no se mostrará si la altura del dispositivo que se está emulando es mayor que el tamaño de pantalla.
   * El pliegue se muestra para la comodidad del autor y no aparece en la página publicada.

## Adición de un contenedor de diseño y su contenido (modo de edición) {#adding-a-layout-container-and-its-content-edit-mode}

Un **contenedor de diseño** es un sistema de párrafos que:

* Contiene otros componentes.
* Define el diseño.
* Responde a los cambios.

>[!NOTE]
>
>Si no está disponible, la variable **Contenedor de diseño** debe ser explícitamente [activado para un sistema de párrafos o una página](/help/sites-administering/configuring-responsive-layout.md) (por ejemplo, utilizando [**Diseño** modo](/help/sites-authoring/default-components-designmode.md)).

1. El **contenedor de diseño** está disponible como componente estándar en el [navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser). Desde aquí puede arrastrarlo a la ubicación deseada en la página tras la cual verá el marcador de posición **Arrastrar componentes aquí**.
1. A continuación, puede agregar componentes al contenedor del diseño. Estos componentes contendrán el contenido real:

   ![screen_shot_2018-03-23at085500](assets/screen_shot_2018-03-23at085500.png)

## Selección y ejecución de una acción en un contenedor de diseños (modo de edición) {#selecting-and-taking-action-on-a-layout-container-edit-mode}

Al igual que con otros componentes, puede seleccionar un contenedor de diseños (cuando se encuentra en el modo de **edición**) y luego realizar una acción en él (copiar, cortar, eliminar):

>[!CAUTION]
>
>Como un contenedor de diseño es un sistema de párrafos, al eliminar el componente se eliminará tanto la cuadrícula de diseño como todos los componentes (y su contenido) que se encuentren dentro del contenedor.

1. Si pasa el ratón por encima o selecciona el marcador de posición de la cuadrícula, se muestra el menú de acción.

   ![screen_shot_2018-03-23at085357](assets/screen_shot_2018-03-23at085357.png)

   Debe seleccionar la opción **Principal**.

   ![Opción principal](do-not-localize/screen_shot_2018-03-23at085417.png)

1. Si el componente de diseño está anidado, seleccione la opción **Principal** presenta una selección desplegable, que le permite seleccionar el contenedor de diseño anidado o sus elementos principales.

   Cuando pasa el ratón sobre los nombres de contenedor en la lista desplegable, sus contornos se muestran en la página.

   * El contenedor de diseños anidado en la parte inferior se muestra en negro.
   * El contenedor de diseños anidado en la posición inferior siguiente aparece en gris oscuro.
   * Cada contenedor sucesivo aparece en un tono más claro de gris.

   ![screen_shot_2018-03-23at085636](assets/screen_shot_2018-03-23at085636.png)

1. De esta forma se resaltará toda la cuadrícula con su contenido. Se muestra la barra de herramientas de acciones, desde donde puede seleccionar una acción como **Eliminar.**

   ![screen_shot_2018-03-23at085724](assets/screen_shot_2018-03-23at085724.png)

## Definición de diseños (modo de diseño) {#defining-layouts-layout-mode}

>[!NOTE]
>
>Puede definir un diseño distinto para cada [punto de interrupción](#layout-definitions-device-emulation-and-breakpoints) (tal y como determinan el tipo y la orientación del dispositivo emulado).

Para configurar el diseño de una cuadrícula interactiva implementada con el contenedor de diseño, debe usar el modo **Diseño**.

El modo **Diseño** puede iniciarse de dos formas.

* Mediante el uso del [menú de modo de la barra de herramientas](/help/sites-authoring/author-environment-tools.md#page-modes) y seleccionando el modo **Diseño**.

   * Seleccione el modo **Diseño** del mismo modo que si desea cambiar al modo **Editar** o **Segmentación**.
   * El modo **Diseño** se mantiene y no abandona el modo **Diseño** hasta que se selecciona otro modo a través del selector correspondiente.

* Cuándo [edición de un componente individual.](/help/sites-authoring/editing-content.md#edit-component-layout)

   * Mediante la opción **Diseño** en el menú de acción rápida del componente, puede cambiar al modo **Diseño**.
   * El modo **Diseño** persiste mientras se edita el componente y vuelve al modo **Editar** en cuanto el enfoque cambia a otro componente.

En el modo de diseño, puede ejecutar una serie de acciones a una cuadrícula:

* Redimensionar los componentes del contenido utilizando los puntos azules. Al redimensionar, siempre se hará un ajuste a la cuadrícula. Al redimensionar, se muestra la cuadrícula de fondo como referencia para la alineación:

  ![screen_shot_2018-03-23at090140](assets/screen_shot_2018-03-23at090140.png)

  >[!NOTE]
  >
  >Se mantendrán las proporciones y relaciones al cambiar el tamaño de componentes como **Imágenes**.

* Haga clic en un componente de contenido y la barra de herramientas le permite:

   * **Principal**

     Permite seleccionar todo el componente del contenedor de diseños para realizar acciones en conjunto.

   * **Flotar a una línea nueva**

     El componente se moverá a una nueva línea, en función del espacio disponible en la cuadrícula.

   * **Ocultar componente**

     El componente se hace invisible (puede restaurarse desde la barra de herramientas del contenedor de diseño).

  ![screen_shot_2018-03-23at090246](assets/screen_shot_2018-03-23at090246.png)

* Entrada **Diseño** modo en el que puede hacer clic en **Arrastre los componentes aquí** para seleccionar todo el componente. Se mostrará la barra de herramientas de este modo.

  La barra de herramientas tendrá diferentes opciones en función del estado del componente de diseño y de los componentes que le pertenecen. Por ejemplo:

   * **Principal**: seleccione el componente principal.

     ![Principal](do-not-localize/screen_shot_2018-03-23at090823.png)

   * **Mostrar componentes ocultos** : Muestre todos los componentes o cada componente por separado. El número indica cuántos componentes ocultos hay actualmente. El contador muestra cuántos componentes están ocultos.

     ![Mostrar componentes ocultos](do-not-localize/screen_shot_2018-03-23at091007.png)

   * **Revertir diseño de punto de interrupción**: volver al diseño predeterminado. Esto significa que no se aplicará ningún diseño personalizado.

     ![Revertir diseño de punto de interrupción](do-not-localize/screen_shot_2018-03-23at091013.png)

   * **Flotar hasta una nueva línea**: suba el componente una posición si el espacio lo permite.

     ![screen_shot_2018-03-23at090829](assets/screen_shot_2018-03-23at090829.png)

   * **Ocultar componente**: oculte el componente actual.

     ![Ocultar componente](do-not-localize/screen_shot_2018-03-23at090834.png)

     >[!NOTE]
     >
     >En el ejemplo anterior, las acciones de flotar y ocultar están disponibles porque este contenedor de diseño está anidado en un contenedor de diseño principal.

   * **Mostrar los componentes:** permite seleccionar los componentes principales para mostrar la barra de herramientas de acciones con la opción **Mostrar componentes ocultos**. En este ejemplo, hay dos componentes ocultos.

     ![screen_shot_2018-03-23at091200](assets/screen_shot_2018-03-23at091200.png)

  Si se selecciona la opción **Mostrar componentes ocultos**, se mostrarán en azul los componentes que están ocultos actualmente en sus posiciones originales.

  ![screen_shot_2018-03-23at091224](assets/screen_shot_2018-03-23at091224.png)

  La selección de la opción **Restaurar todo** permitirá que se muestren todos los componentes ocultos.
