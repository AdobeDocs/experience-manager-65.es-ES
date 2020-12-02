---
title: Introducción a la IU de creación de comunicación interactiva
seo-title: Introducción a los distintos elementos de la interfaz de usuario que puede utilizar para crear una comunicación interactiva
description: Introducción a los distintos elementos de la interfaz de usuario que puede utilizar para crear una comunicación interactiva
seo-description: Introducción a los distintos elementos de la interfaz de usuario que puede utilizar para crear una comunicación interactiva
uuid: e8c5b1e8-b2bb-46b4-b42e-1f343192641a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
discoiquuid: 5855d21b-340c-4139-aabe-c3a534cedb98
docset: aem65
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 3%

---


# Introducción a la IU de creación de comunicación interactiva{#introduction-to-interactive-communication-authoring-ui}

La interfaz de usuario para la creación de [Comunicación interactiva](/help/forms/using/interactive-communications-overview.md) es intuitiva y proporciona lo siguiente para la creación de impresión y canal web de la Comunicación interactiva:

* Editor de documentos de arrastrar y soltar WYSIWYG
* Repositorio integrado para recursos: los recursos cargados y creados en el servidor están disponibles en el navegador de recursos de la interfaz de creación de Interactive Communication

Cuando [crea una comunicación interactiva nueva o edita una existente](../../forms/using/create-interactive-communication.md), utiliza los siguientes elementos de la interfaz de usuario:

* [Barra lateral](#sidebar)
* [Barra de herramientas de página](#page-toolbar)
* [Barra de herramientas Componente](#component-toolbar)
* Área de contenido

![interfaz de usuario de creación de comunicación interactiva](assets/form-editor.png)

**A.** Barra lateral  **B.Barra de herramientas** Página  **C.** Área de contenido

## Barra lateral {#sidebar}

![Barra lateral](assets/sidebar-comps-2.png)

**A.** Canal browser  **B.** Content browser  **C.** Properties browser  **D.** Asset browser  **E.** Components browser  ****   **** F.Data Sources browser - Data ModelG.Data Sources browser - Master Content

<!-- Click to enlarge

![sidebar-comps-3](assets/sidebar-comps-3.png)-->

La barra lateral incluye lo siguiente:

* **Navegador de canal**

El navegador de Canal le ayuda a cambiar entre los canales de impresión y web de la Comunicación interactiva. En función del canal seleccionado en el navegador de canal, los navegadores, como Contenido y Componentes, muestran las opciones.

* ****
Navegador de contenidoEn el navegador de contenido, puede ver la jerarquía de objetos del documento para el canal seleccionado. El autor puede desplazarse a un componente específico tocando ese elemento en el árbol de objetos de Documento. El autor puede buscar objetos en el canal web y reorganizarlos desde este árbol.

* **Navegador de propiedades**

   Permite editar las propiedades de un componente. Las propiedades cambian según el componente. Por ejemplo, para ver las propiedades del contenedor de documento:
Seleccione un componente, luego toque ![Documento de nivel de campo](assets/field-level.png) > **Contenedor** y luego toque ![cmppr](assets/cmppr.png).

* **Navegador**
de recursosSegmenta distintos tipos de contenido, como fragmentos de diseño, imágenes, documentos, páginas y vídeos. El autor puede arrastrar y soltar recursos en la comunicación interactiva.

* **Navegador**
de componentesIncluye componentes que se pueden utilizar para generar los canales de impresión y web de un documento. Puede arrastrar componentes a la comunicación interactiva para agregar elementos y configurar el elemento agregado según los requisitos. En la tabla siguiente se describen los componentes enumerados en el navegador de componentes para impresión y canales web:

| **Componente** | **Canal de impresión** | **Canal web** | **Funcionalidad** |
|---|---|---|---|
| Gráfico | xib | xib | Añade un gráfico que puede utilizar en una comunicación interactiva para la representación visual de datos bidimensionales recuperados de un elemento de recopilación del modelo de datos de formulario. |
| Fragmento de documento | xib | xib | Permite agregar un componente, texto, lista o condición reutilizables a una comunicación interactiva. El componente reutilizable que se agrega a una comunicación interactiva puede estar basado en modelos de datos de formulario o sin modelo de datos de formulario. |
| Imagen | xib | xib | Permite insertar una imagen. |
| Panel | - | xib | El componente Panel es un marcador de posición para agrupar otros componentes y controla cómo se distribuye un grupo de componentes en una comunicación interactiva. Un componente de panel también permite hacer que un grupo de componentes se pueda repetir para el usuario final, como en varias entradas necesarias para rellenar las credenciales educativas. También es recomendable utilizar un panel para cada ficha de una comunicación interactiva con varias fichas. |
| Tabla | * | xib | Agrega una tabla que le permite organizar los datos en filas y columnas. |
| Área de destino | ** | xib | Inserta un área de destinatario en un canal web para organizar los componentes específicos del canal web. |
| Texto | - | xib | Añade texto al canal web de una comunicación interactiva. El texto puede utilizar objetos del modelo de datos de formulario para hacer que el contenido sea dinámico. |

* Utilice Fragmentos de diseño en el canal Imprimir para agregar tablas.

** En el canal de impresión, las áreas de destinatario están predefinidas en la plantilla XDP/print. No puede agregar nuevas áreas de destinatario mediante la interfaz de usuario de creación de Interactive Communication.

* **Explorador**
de fuentes de datosEl explorador de fuentes de datos muestra los orígenes de datos disponibles en el modelo de datos de formulario seleccionado al crear la comunicación interactiva.

### Puntos clave para trabajar con componentes {#key-points-for-working-with-components}

Los puntos clave para trabajar con componentes de comunicación interactivos son los siguientes:

* Cada componente tiene propiedades asociadas que controlan su apariencia y funcionalidad. Para configurar las propiedades de un componente, toque el componente y toque ![cmppr](assets/cmppr.png) para abrir las propiedades del componente en el navegador de propiedades.
* Un componente se identifica con su nombre de elemento. Al tocar ![cmppr](assets/cmppr.png), puede cambiar el nombre del componente cambiando el valor del campo Nombre del elemento en el navegador de propiedades. El campo Nombre del elemento solo acepta letras, números, guiones (-) y subrayados (_). No se permiten otros caracteres especiales y el nombre del elemento debe comenzar con una letra.
* Puede modificar la propiedad Título de un componente de comunicación interactiva en línea en el editor sin abrir el navegador Propiedades siempre que el título esté visible en la comunicación interactiva. Para ello:

   1. Toque para seleccionar un componente que tenga una propiedad Title y cuya propiedad Hide title esté desactivada.
   1. Toque ![aem_6_3_edit](assets/aem_6_3_edit.png) para que el título se pueda editar.

   1. Modifique el título y toque la tecla de retorno o toque cualquier lugar fuera del componente para guardar los cambios. Toque la tecla Esc para descartar los cambios.

## Barra de herramientas de componentes {#component-toolbar}

![Etiquetas de la barra de herramientas de componentes](do-not-localize/component_toolbar_labels_new.png)

Al seleccionar un componente, verá una barra de herramientas que le permite trabajar con él. Se obtienen opciones para cortar, pegar, mover y especificar propiedades de los componentes. Sus opciones son:

A.**Configurar**: Al tocar **Configurar**, las propiedades de los componentes son visibles en la barra lateral.

B.**Editar reglas**: Al tocar Editar reglas, aparece el Editor de reglas, donde puede editar y crear reglas para el componente seleccionado. En el Editor de reglas, también puede seleccionar otros objetos de formulario (componentes) y editar/crear reglas para dichos objetos de formulario.

C.**Copiar**: Puede utilizar la opción de copia para copiar un componente y pegarlo en otros lugares de la comunicación interactiva.

D.**Cortar**: Puede utilizar la opción de corte para mover un componente de un lugar a otro en la Comunicación interactiva.

E. **Eliminar**: Permite eliminar el componente de la comunicación interactiva.

F. **Insertar componente**: Permite insertar un componente sobre el componente seleccionado.

G. **Pegar**: Permite pegar el componente que se corta o copia mediante las opciones descritas anteriormente.

H. **Grupo**: Permite seleccionar varios componentes si desea cortar, copiar o pegar varios componentes juntos.

I. **Principal**: Permite seleccionar el elemento principal de un componente.

J. **Expresión SOM de Vista:** Permite vista de la [expresión SOM](../../forms/using/using-som-expressions-adaptive-forms.md) para el componente.

K: **Agrupar objetos en el panel:** Permite agrupar los componentes en un panel para poder realizar operaciones en esos componentes simultáneamente. Para obtener más información, consulte [Objetos de grupo en Panel](create-interactive-communication.md#groupobjectspanel).

L. **Añadir panel secundario** (solo para paneles): Permite agregar un panel secundario al panel.

M: **Añadir barra de herramientas del panel** (solo para paneles):Permite agregar la barra de herramientas para el componente Panel. A continuación, puede realizar más acciones en la barra de herramientas.

Además, la opción **Reemplazar** de la barra de herramientas permite reemplazar el componente existente por un componente alternativo. La opción no está disponible para el componente Panel.

## Barra de herramientas de página {#page-toolbar}

La barra de herramientas Página de la parte superior ofrece opciones que le permiten realizar previsualizaciones de la comunicación interactiva y cambiar sus propiedades. Puede realizar la previsualización de la comunicación interactiva al crearla y realizar los cambios correspondientes. En la barra de herramientas de la página, verá:

* Alternar panel lateral ![alternar panel lateral](assets/toggle-side-panel.png): Permite mostrar u ocultar la barra lateral.
* Información de página ![pageinformationad](assets/pageinformationad.png): Permite la vista de propiedades de página.
* Emulador ![regla](assets/ruler.png): Permite emular el aspecto de la comunicación interactiva para diferentes tamaños de pantalla, como tablets y teléfonos.
* Editar: Permite seleccionar otros modos como: Editar, Estilo, Desarrollador y Diseño.

   * Editar: Permite editar las propiedades de la comunicación interactiva y sus componentes. Por ejemplo, agregar un componente, soltar una imagen y especificar campos obligatorios.
   * Estilo: Permite aplicar estilo al aspecto de los componentes de la comunicación interactiva. Por ejemplo, en el modo de estilo, puede seleccionar un panel y especificar su color de fondo.
   * Desarrollador: Permite a un desarrollador:

      * Descubra de qué se compone Interactive Communication.
      * Depurar lo que está sucediendo donde y cuando, lo que a su vez ayuda a resolver problemas.
   * Destinatario: Permite habilitar o deshabilitar componentes personalizados o componentes predeterminados que no aparecen en la barra lateral.


* Previsualización: Le permite realizar previsualizaciones del aspecto de la comunicación interactiva al publicarla.

