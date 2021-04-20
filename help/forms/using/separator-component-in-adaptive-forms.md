---
title: Componente separador en formularios adaptables
seo-title: Componente separador en formularios adaptables
description: Puede utilizar el componente separador para separar visualmente secciones de un formulario.
seo-description: Puede utilizar el componente separador para separar visualmente secciones de un formulario.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# Componente separador en formularios adaptables{#separator-component-in-adaptive-forms}

Puede utilizar el componente separador para separar visualmente los paneles de un formulario. Puede definir el aspecto general y el estilo de un componente separador especificando las siguientes propiedades del componente separador:

* **Nombre del elemento:** especifica el nombre del componente. Las expresiones SOM se dirigen al componente con el valor especificado en el campo Nombre de elemento .
* **Grosor:** especifica el grosor del componente separador en píxeles.

* **Clase CSS:** especifica la clase CSS personalizada para el componente separador

* **Estilos en línea:** con AEM Forms, ahora puede aplicar estilos CSS en línea a componentes de formulario adaptables individuales y previsualizar los cambios en tiempo real.

Puede utilizar el modo Diseño para definir el número de columnas a las que se expande el componente separador. Para obtener más información, consulte [Uso del modo Diseño para cambiar el tamaño de los componentes](../../forms/using/resize-using-layout-mode.md).

Para especificar las propiedades de un componente separador:

1. Seleccione un componente separador y pulse ![cmppr](assets/cmppr.png). Las propiedades se abren en la barra lateral.
1. Haga clic en una ficha de la sección Propiedades CSS en línea para especificar las propiedades CSS. Por ejemplo: a. En la ficha Campo, haga clic en **Agregar elemento**. Se añade una fila con dos campos.
1. En el primer campo de la izquierda, especifique la propiedad CSS3 que desee aplicar. Por ejemplo, **border**. También puede seleccionar una propiedad haciendo clic en el botón de flecha hacia abajo. La lista desplegable no es exhaustiva y puede especificar cualquier nombre de propiedad CSS3 admitido en este campo.
1. En el campo adyacente, especifique un valor válido para la propiedad CSS3 especificada. Por ejemplo, **3px negro sólido**.
1. Haga clic en **Agregar elemento** para especificar otra propiedad y su valor.
1. Haga clic en **Preview** para obtener una vista previa de los cambios en el formulario.
1. Haga clic en **Aceptar** para confirmar los cambios o en **Cancelar** para salir del cuadro de diálogo sin ningún cambio.

