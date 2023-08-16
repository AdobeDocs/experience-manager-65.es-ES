---
title: Introducción a la IU de creación de una comunicación interactiva
seo-title: An introduction to the various user interface elements you can use to author Interactive Communication
description: Introducción a los distintos elementos de la interfaz de usuario que puede utilizar para crear una comunicación interactiva
seo-description: An introduction to the various user interface elements you can use to author Interactive Communication
uuid: e8c5b1e8-b2bb-46b4-b42e-1f343192641a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
discoiquuid: 5855d21b-340c-4139-aabe-c3a534cedb98
docset: aem65
feature: Interactive Communication
exl-id: 3d15a723-df6c-4b4a-992e-a6636f4cf3dc
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 96%

---

# Introducción a la IU de creación de una comunicación interactiva{#introduction-to-interactive-communication-authoring-ui}

La interfaz de usuario para la creación de [comunicaciones interactivas](/help/forms/using/interactive-communications-overview.md) es intuitiva y proporciona lo siguiente para la creación de los canales impreso y web de las comunicaciones interactivas:

* Editor de documentos de arrastrar y soltar WYSIWYG
* Repositorio integrado para recursos: los recursos cargados y creados en el servidor están disponibles en el Explorador de recursos de la interfaz de creación de las comunicaciones interactivas.

Cuando [crea una nueva comunicación interactiva o edita una existente](../../forms/using/create-interactive-communication.md), utiliza los siguientes elementos de la interfaz de usuario:

* [Barra lateral](#sidebar)
* [Barra de herramientas de la página](#page-toolbar)
* [Barra de herramientas de los componentes](#component-toolbar)
* Área de contenido

![interfaz de usuario de creación de comunicaciones interactivas](assets/form-editor.png)

**A.** Barra lateral **B.** Barra de herramientas de la página **C.** Área de contenido

## Barra lateral {#sidebar}

![Barra lateral](assets/sidebar-comps-2.png)

**A.** Explorador de canales **B.** Explorador de contenido **C.** Explorador de propiedades **D.** Explorador de recursos **E.** Explorador de componentes **F.** Explorador de fuentes de datos: modelo de datos **G.** Explorador de fuentes de datos: contenido maestro

<!-- Click to enlarge

![sidebar-comps-3](assets/sidebar-comps-3.png)-->

La barra lateral incluye lo siguiente:

* **Explorador de canales**

El Explorador de canales le permite alternar entre los canales impreso y web de la comunicación interactiva. Según el canal que haya seleccionado en el Explorador de canales, los exploradores, como Contenido y Componentes, muestran las opciones.

* **Explorador de contenido**
En el Explorador de contenido, puede ver la jerarquía de objetos del documento del canal seleccionado. El autor puede desplazarse a un componente específico al pulsar ese elemento en el árbol de objetos del formulario. El autor puede buscar objetos en el canal web y reorganizarlos desde este árbol.

* **Explorador de propiedades**

  Permite editar las propiedades de un componente. Las propiedades cambian en función del componente. Por ejemplo, para ver las propiedades del contenedor de documentos, seleccione un componente, pulse ![nivel de campo](assets/field-level.png) > **Contenedor de documento** y, a continuación, pulse ![cmppr](assets/cmppr.png).

* **Explorador de recursos**
Segmenta distintos tipos de contenido, como fragmentos de diseño, imágenes, documentos, páginas o vídeos. El autor puede arrastrar y soltar recursos en la comunicación interactiva.

* **Explorador de componentes**
Incluye los componentes que puede utilizar para crear los canales impreso y web de un documento. Puede arrastrar componentes hasta la comunicación interactiva para agregar elementos y configurar los elementos agregados según los requisitos. En la siguiente tabla se describen los componentes que se muestran en el Explorador de componentes para los canales impreso y web:

| **Componente** | **Canal de impresión** | **Canal web** | **Funcionalidad** |
|---|---|---|---|
| Gráfico | ✓ | ✓ | Agrega un gráfico que puede usar en una comunicación interactiva para la representación visual de datos bidimensionales recuperados de un elemento de colección del modelo de datos de formulario. |
| Fragmento de documento | ✓ | ✓ | Permite agregar un componente, un texto, una lista o una condición reutilizables a una comunicación interactiva. El componente reutilizable que agregue a una comunicación interactiva puede estar basado en el modelo de datos de formulario o carecer de él. |
| Imagen | ✓ | ✓ | Permite insertar una imagen. |
| Panel | - | ✓ | El componente Panel es un marcador de posición para agrupar otros componentes, y controla cómo se coloca un grupo de componentes en una comunicación interactiva. Un componente de panel también le permite hacer que un grupo de componentes se repita para el usuario final, por ejemplo, en varias entradas obligatorias para rellenar credenciales educativas. También se recomienda utilizar un panel para cada una de las pestañas de una comunicación interactiva con varias pestañas. |
| Tabla | &#42; | ✓ | Agrega una tabla que le permite organizar los datos en filas y columnas. |
| Área de destino | &#42;&#42; | ✓ | Inserta un área de destino en un canal web para organizar los componentes específicos de ese canal. |
| Texto | - | ✓ | Agrega texto al canal web de una comunicación interactiva. El texto puede utilizar objetos del modelo de datos de formulario para hacer que el contenido sea dinámico. |

&#42; Utilice fragmentos de diseño en el canal de impresión para añadir tablas.

&#42;&#42; En el canal de impresión, las áreas de destino están predefinidas en la plantilla XDP/de impresión. No se pueden agregar nuevas áreas de destino mediante la interfaz de usuario de creación de comunicaciones interactivas.

* **Explorador de fuentes de datos**
El Explorador de fuentes de datos muestra las fuentes de datos disponibles en el modelo de datos de formulario que seleccionó al crear la comunicación interactiva.

### Puntos clave para trabajar con componentes {#key-points-for-working-with-components}

Los puntos clave para trabajar con los componentes de las comunicaciones interactivas son los siguientes:

* Cada componente tiene propiedades asociadas que controlan su aspecto y su funcionalidad. Para configurar las propiedades de un componente, pulse el componente y luego pulse ![cmppr](assets/cmppr.png) para abrir las propiedades del componente en el Explorador de propiedades.
* Cada componente se identifica con su nombre de elemento. Al pulsar ![cmppr](assets/cmppr.png), puede cambiar el nombre del componente cambiando el valor del campo Nombre del elemento en el Explorador de propiedades. El campo Nombre de elemento solo acepta letras, números, guiones (-) y guiones bajos (_). No se permite ningún otro tipo de caracteres especiales, y el nombre del elemento debe comenzar con una letra.
* Puede modificar la propiedad Título de los componentes en línea de una comunicación interactiva en el editor sin abrir el Explorador de propiedades siempre que el título esté visible en la comunicación. Para ello:

   1. Pulse para seleccionar un componente que tenga la propiedad Título y cuya propiedad Ocultar título esté deshabilitada.
   1. Pulse ![aem_6_3_editar](assets/aem_6_3_edit.png) para poder editar el título.

   1. Modifique el título y pulse la tecla Retroceso o pulse en cualquier sitio fuera del componente para guardar los cambios. Pulse la tecla Esc para descartar los cambios.

## Barra de herramientas de los componentes {#component-toolbar}

![Etiquetas de la barra de herramientas de componentes](do-not-localize/component_toolbar_labels_new.png)

Al seleccionar un componente, aparece una barra de herramientas que le permite trabajar con él. Puede obtener opciones para cortar, pegar, mover y especificar propiedades de los componentes. Las opciones son las siguientes:

A.**Configurar**: al pulsar **Configurar**, las propiedades de los componentes se pueden ver en la barra lateral.

B.**Editar reglas**: cuando pulse Editar reglas, aparecerá el Editor de reglas, en el que podrá editar y crear reglas para el componente seleccionado. En el Editor de reglas, también puede seleccionar otros objetos de formulario (componentes) y editar/crear reglas para dichos objetos.

B.**Copiar**: puede utilizar la opción Copiar para copiar un componente y pegarlo en otros lugares de la comunicación interactiva.

C.**Cortar**: puede utilizar la opción Cortar para mover un componente de un lugar a otro en la comunicación interactiva.

E. **Eliminar**: permite eliminar el componente de la comunicación interactiva.

F. **Insertar componente**: permite insertar un componente sobre el componente seleccionado.

G. **Pegar**: permite pegar el componente cortado o copiado mediante las opciones descritas anteriormente.

H. **Grupo**: permite seleccionar varios componentes si desea cortar, copiar o pegar más de un componente a la vez.

I. **Principal**: permite seleccionar el elemento principal de un componente.

J. **Ver expresión SOM:** permite ver la [expresión SOM](../../forms/using/using-som-expressions-adaptive-forms.md) del componente.

K: **Agrupar objetos en el panel:** permite agrupar los componentes en un panel para poder realizar operaciones en esos componentes de forma simultánea. Para obtener más información, consulte [Agrupar objetos en el panel](create-interactive-communication.md#groupobjectspanel).

L. **Agregar panel secundario** (solo para paneles): permite agregar un panel secundario al panel.

M: **Agregar barra de herramientas del panel** (solo para paneles): le permite añadir la barra de herramientas del componente Panel. Después, puede realizar más acciones en la barra de herramientas.

Además, la opción **Reemplazar** de la barra de herramientas permite reemplazar el componente existente con un componente alternativo. La opción no está disponible para el componente Panel.

## Barra de herramientas de la página {#page-toolbar}

La barra de herramientas Página de la parte superior proporciona opciones que le permiten previsualizar la comunicación interactiva y cambiar sus propiedades. Puede obtener una vista previa de la comunicación interactiva al crearla y realizar los cambios correspondientes. En la barra de herramientas Página, verá lo siguiente:

* Alternar panel lateral![ alternar-panel-lateral](assets/toggle-side-panel.png): permite mostrar u ocultar la barra lateral.
* Información de la página ![información_de_la_página](assets/pageinformationad.png): permite ver las propiedades de la página.
* Emulador ![regla](assets/ruler.png): permite emular el aspecto de la comunicación interactiva en diferentes tamaños de visualización, como tabletas y teléfonos.
* Edición: permite seleccionar otros modos, como Edición, Estilo, Desarrollador y Diseño.

   * Edición: permite editar las propiedades de la comunicación interactiva y sus componentes. Por ejemplo, agregar un componente, soltar una imagen y especificar campos obligatorios.
   * Estilo: permite aplicar un estilo a la apariencia de los componentes de la comunicación interactiva. Por ejemplo, en el modo Estilo, puede seleccionar un panel y especificar su color de fondo.
   * Desarrollador: permite a los desarrolladores lo siguiente:

      * Ver los componentes de la comunicación interactiva.
      * Depurar lo que sucede, dónde y cuándo, lo que a su vez ayuda a resolver problemas.

   * Destino: permite habilitar o deshabilitar componentes personalizados o componentes integrados que no aparecen en la barra lateral.

* Vista previa: permite obtener una vista previa del aspecto de la comunicación interactiva al publicarla.
