---
title: Componente separador en formularios adaptables
seo-title: Separator component in adaptive forms
description: Puede utilizar el componente Separador para separar visualmente las secciones de un formulario.
seo-description: You can use the separator component to visually segregate sections of a form.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
feature: Adaptive Forms
exl-id: 11cbf865-c8e2-4833-b0b8-a3cb5e42f5cd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 88%

---

# Componente separador en formularios adaptables{#separator-component-in-adaptive-forms}

Puede utilizar el componente separador para separar visualmente los paneles de un formulario. Puede definir el aspecto general y el estilo de un componente Separador especificando las siguientes propiedades del componente Separador:

* **Nombre del elemento:** especifica el nombre del componente. Las expresiones SOM se dirigen al componente con el valor especificado en el campo Nombre del elemento.
* **Grosor:** especifica el grosor del componente Separador en píxeles.

* **Clase CSS:** especifica la clase CSS personalizada para el componente Separador.

* **Estilos en línea:** Con AEM Forms, ahora puede aplicar estilos CSS en línea a componentes de formulario adaptables individuales y previsualizar los cambios en tiempo real.

Puede utilizar el modo Diseño para definir el número de columnas a las que se expande el componente Separador. Para obtener más información, consulte [Uso del modo Diseño para cambiar el tamaño de los componentes](../../forms/using/resize-using-layout-mode.md).

Para especificar las propiedades de un componente Separador:

1. Seleccione un componente Separador y pulse ![cmppr](assets/cmppr.png). Las propiedades se abren en la barra lateral.
1. Haga clic en una pestaña de la sección Propiedades CSS en línea para especificar las propiedades CSS. Por ejemplo: a. En la pestaña Campo, haga clic en **Agregar elemento**. Se añade una fila con dos campos.
1. En el primer campo de la izquierda, especifique la propiedad CSS3 que desee aplicar. Por ejemplo, **border**. También puede seleccionar una propiedad haciendo clic en el botón de flecha hacia abajo. La lista desplegable no es exhaustiva y puede especificar cualquier nombre de propiedad CSS3 admitido en este campo.
1. En el campo adyacente, especifique un valor válido para la propiedad CSS3 especificada. Por ejemplo, **3px solid black**.
1. Haga clic en **Agregar elemento** para especificar otra propiedad y su valor.
1. Haga clic en **Vista previa** para previsualizar los cambios en el formulario.
1. Haga clic en **Aceptar** para confirmar los cambios o en **Cancelar** para salir del cuadro de diálogo realizar cambios.
