---
title: Introducción a la IU de creación de Interactive Communication
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
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 21%

---

# Introducción a la IU de creación de Interactive Communication{#introduction-to-interactive-communication-authoring-ui}

La interfaz de usuario para la creación [Comunicación interactiva](/help/forms/using/interactive-communications-overview.md) es intuitivo y proporciona lo siguiente para la creación de impresión y canal web de la comunicación interactiva:

* WYSIWYG arrastrar y soltar editor de documentos
* Repositorio integrado para recursos: los recursos cargados y creados en el servidor están disponibles en el navegador de recursos de la interfaz de creación de Interactive Communication

Cuando [crear o editar una comunicación interactiva existente](../../forms/using/create-interactive-communication.md), se utilizan los siguientes elementos de la interfaz de usuario:

* [Barra lateral](#sidebar)
* [Barra de herramientas de la página](#page-toolbar)
* [Barra de herramientas de los componentes](#component-toolbar)
* Área de contenido

![interfaz de usuario de creación de comunicaciones interactivas](assets/form-editor.png)

**A.** Barra lateral **B.** Barra de herramientas de página **C.** Área de contenido

## Barra lateral {#sidebar}

![Barra lateral](assets/sidebar-comps-2.png)

**A.** Explorador de canales **B.** Navegador de contenido **C.** Explorador de propiedades **D.** Navegador de recursos **E.** Navegador de componentes **F.** Explorador de fuentes de datos: modelo de datos **G.** Explorador de fuentes de datos: contenido maestro

<!-- Click to enlarge

![sidebar-comps-3](assets/sidebar-comps-3.png)-->

La barra lateral incluye lo siguiente:

* **Explorador de canales**

El navegador de canal le ayuda a cambiar entre los canales web e impresos de la comunicación interactiva. Según el canal que haya seleccionado en el navegador de canales, los navegadores, como Contenido y Componentes, muestran las opciones.

* **Navegador de contenido**
En el navegador de contenido, puede ver la jerarquía de objetos del documento para el canal seleccionado. El autor puede desplazarse a un componente específico tocando ese elemento en el árbol de objetos del documento. El autor puede buscar objetos en el canal web y reorganizarlos desde este árbol.

* **Explorador de propiedades**

   Permite editar las propiedades de un componente. Las propiedades cambian según el componente. Por ejemplo, para ver las propiedades del contenedor de documentos: Seleccione un componente y, a continuación, pulse ![nivel de campo](assets/field-level.png) > **Contenedor de documento** y, a continuación, toque ![cmppr](assets/cmppr.png).

* **Navegador de recursos**
Segmenta distintos tipos de contenido, como fragmentos de diseño, imágenes, documentos, páginas o vídeos. El autor puede arrastrar y soltar recursos en la comunicación interactiva.

* **Navegador de componentes**
Incluye componentes que se pueden utilizar para crear los canales web e impresos de un documento. Puede arrastrar componentes a la comunicación interactiva para añadir elementos y configurar el elemento añadido según los requisitos. En la tabla siguiente se describen los componentes enumerados en el navegador de componentes para imprimir y canales web:

| **Component** | **Canal de impresión** | **Canal web** | **Funcionalidad** |
|---|---|---|---|
| Gráfico | ✓ | ✓ | Agrega un gráfico que puede usar en una comunicación interactiva para la representación visual de datos bidimensionales recuperados de un elemento de recopilación del modelo de datos de formulario. |
| Fragmento de documento | ✓ | ✓ | Permite añadir un componente, texto, lista o condición reutilizables a una comunicación interactiva. El componente reutilizable que agregue a una comunicación interactiva puede estar basado en el modelo de datos de formulario o sin un modelo de datos de formulario. |
| Imagen | ✓ | ✓ | Permite insertar una imagen. |
| Panel | - | ✓ | El componente Panel es un marcador de posición para agrupar otros componentes y controla cómo se coloca un grupo de componentes en una comunicación interactiva. Un componente de panel también le permite hacer que un grupo de componentes se repita para el usuario final, como en varias entradas necesarias para rellenar las credenciales educativas. También se recomienda utilizar un panel para cada una de las pestañas de una comunicación interactiva con varias pestañas. |
| Tabla | &#42; | ✓ | Agrega una tabla que le permite organizar los datos en filas y columnas. |
| Área de destino | &#42;&#42; | ✓ | Inserta un área de destino en un canal web para organizar los componentes específicos del canal web. |
| Texto | - | ✓ | Agrega texto al canal web de una comunicación interactiva. El texto puede utilizar objetos del modelo de datos de formulario para hacer que el contenido sea dinámico. |

&#42; Utilice Fragmentos de diseño en el canal Imprimir para añadir tablas.

&#42;&#42; En el canal Imprimir, las áreas de destino están predefinidas en la plantilla XDP/print. No se pueden agregar nuevas áreas de destino mediante la interfaz de usuario de creación de Interactive Communication.

* **Explorador de fuentes de datos**
El explorador de fuentes de datos muestra los orígenes de datos disponibles en el modelo de datos de formulario que seleccionó al crear la comunicación interactiva.

### Puntos clave para trabajar con componentes {#key-points-for-working-with-components}

Los puntos clave al trabajar con componentes de comunicación interactiva son los siguientes:

* Cada componente tiene propiedades asociadas que controlan su aspecto y su funcionalidad. Para configurar las propiedades de un componente, pulse el componente y pulse ![cmppr](assets/cmppr.png) para abrir las propiedades del componente en el navegador Propiedades.
* Cada componente se identifica con su nombre de elemento. Al tocar ![cmppr](assets/cmppr.png), puede cambiar el nombre del componente cambiando el valor del campo Nombre de elemento en el navegador de propiedades. El campo Nombre de elemento solo acepta letras, números, guiones (-) y guiones bajos (_). No se permite ningún otro tipo de caracteres especiales, y el nombre del elemento debe comenzar con una letra.
* Puede modificar la propiedad Título de un componente Comunicación interactiva en línea en el editor sin abrir el navegador Propiedades siempre que el título esté visible en la Comunicación interactiva. Para ello:

   1. Pulse para seleccionar un componente que tenga la propiedad Título y cuya propiedad Ocultar título esté deshabilitada.
   1. Toque ![aem_6_3_edit](assets/aem_6_3_edit.png) para que el título se pueda editar.

   1. Modifique el título y pulse la tecla Retroceso o pulse en cualquier sitio fuera del componente para guardar los cambios. Pulse la tecla Esc para descartar los cambios.

## Barra de herramientas de los componentes {#component-toolbar}

![Etiquetas de la barra de herramientas de componentes](do-not-localize/component_toolbar_labels_new.png)

Al seleccionar un componente, aparece una barra de herramientas que le permite trabajar con él. Puede obtener opciones para cortar, pegar, mover y especificar propiedades de los componentes. Las opciones son las siguientes:

A.**Configurar**: Al pulsar **Configurar**, las propiedades de los componentes se pueden ver en la barra lateral.

B.**Editar reglas**: Cuando pulse Editar reglas, aparecerá el Editor de reglas en el que podrá editar y crear reglas para el componente seleccionado. En el Editor de reglas, también puede seleccionar otros objetos de formulario (componentes) y editar/crear reglas para dichos objetos de formulario.

C.**Copiar**: Puede utilizar la opción de copia para copiar un componente y pegarlo en otros lugares de la comunicación interactiva.

D.**Cortar**: Puede utilizar la opción de corte para mover un componente de un lugar a otro en la comunicación interactiva.

E. **Eliminar**: Permite eliminar el componente de la comunicación interactiva.

F. **Insertar componente**: Permite insertar un componente sobre el componente seleccionado.

G. **Pegar**: Permite pegar el componente cortado o copiado mediante las opciones descritas anteriormente.

H. **Grupo**: Permite seleccionar varios componentes si desea cortar, copiar o pegar más de un componente a la vez.

I. **Principal**: Permite seleccionar el elemento principal de un componente.

J. **Ver expresión SOM:** Permite ver la [Expresión SOM](../../forms/using/using-som-expressions-adaptive-forms.md) para el componente.

K: **Agrupar objetos en Panel:** Permite agrupar los componentes en un panel para poder realizar operaciones en esos componentes de forma simultánea. Para obtener más información, consulte [Agrupar objetos en el panel](create-interactive-communication.md#groupobjectspanel).

L. **Agregar panel secundario** (solo para paneles): Permite agregar un panel secundario al panel.

M: **Agregar barra de herramientas del panel** (solo para paneles): le permite añadir la barra de herramientas para el componente Panel. A continuación, puede realizar más acciones en la barra de herramientas.

Además, la variable **Reemplazar** en la barra de herramientas, permite reemplazar el componente existente con un componente alternativo. La opción no está disponible para el componente Panel.

## Barra de herramientas de la página {#page-toolbar}

La barra de herramientas Página de la parte superior ofrece opciones que le permiten previsualizar la comunicación interactiva y cambiar sus propiedades. Puede obtener una vista previa de la comunicación interactiva cuando la crea y realizar los cambios correspondientes. En la barra de herramientas de la página, verá lo siguiente:

* Alternar panel lateral![ toggle-side-panel](assets/toggle-side-panel.png): permite mostrar u ocultar la barra lateral.
* Información de la página ![pageinformationad](assets/pageinformationad.png): Permite ver las propiedades de la página.
* Emulador ![regla](assets/ruler.png): Le permite emular el aspecto de su comunicación interactiva para diferentes tamaños de pantalla, como tabletas y teléfonos.
* Editar: Permite seleccionar otros modos, como: Editar, Estilo, Desarrollador y Diseño.

   * Editar: Permite editar las propiedades de la comunicación interactiva y sus componentes. Por ejemplo, agregar un componente, soltar una imagen y especificar campos obligatorios.
   * Estilo: Permite aplicar estilo al aspecto de los componentes de la comunicación interactiva. Por ejemplo, en el modo Estilo, puede seleccionar un panel y especificar su color de fondo.
   * Desarrollador: Permite a un desarrollador lo siguiente:

      * Descubra de qué se compone la comunicación interactiva.
      * Depurar lo que sucede, dónde y cuándo, lo que a su vez ayuda a resolver problemas.
   * Target: Permite habilitar o deshabilitar componentes personalizados o componentes integrados que no aparecen en la barra lateral.


* Vista previa: Le permite previsualizar el aspecto de la comunicación interactiva cuando la publica.
