---
title: Plantillas de formulario adaptables
seo-title: Plantillas de formulario adaptables
description: Cree plantillas de formulario adaptables definiendo la estructura básica y el contenido del formulario inicial con el Editor de plantillas.
seo-description: Cree plantillas de formulario adaptables definiendo la estructura básica y el contenido del formulario inicial con el Editor de plantillas.
uuid: 317ca3ab-f809-49a7-a063-9d0c17a35fe4
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: b21a48ba-eccd-4bb5-9b92-3039026ddf2a
docset: aem65
feature: Formularios adaptables
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1986'
ht-degree: 0%

---


# Plantillas de formulario adaptables{#adaptive-form-templates}

Al crear un formulario, se agregan campos y componentes para definir la estructura del formulario, el contenido y las acciones en el editor. Los campos y componentes se añaden en el `guideRootPanel` del contenedor de formulario. Con el Editor de plantillas, puede crear una plantilla que contenga estructura básica y contenido inicial que los autores puedan utilizar para crear formularios.

Por ejemplo, desea que todos los autores de formularios tengan ciertos cuadros de texto, botones de navegación y un botón de envío en un formulario de inscripción. Puede crear una plantilla con los componentes que los autores pueden utilizar para crear un formulario coherente con otros formularios de inscripción. Cuando los autores utilizan la plantilla para crear un formulario adaptable, el nuevo formulario hereda la estructura y los componentes especificados en la plantilla. El Editor de plantillas le permite:

* Agregue componentes de encabezado y pie de página de un formulario en la capa de estructura.
* Proporcione el contenido inicial para el formulario.
* Especifique un tema y envíe acciones.

## Uso de plantillas {#working-with-templates}

Puede acceder al editor de plantillas desde el menú Herramientas accediendo a **Adobe Experience Manager > Herramientas > Plantillas**. En este caso, las plantillas están organizadas en carpetas habilitadas para plantillas editables. AEM proporciona una carpeta global para organizar las plantillas. Sin embargo, no está activada de forma predeterminada. Puede solicitar al administrador que habilite la carpeta global o que cree una nueva carpeta para plantillas. Para obtener más información sobre cómo crear carpetas, consulte [Carpetas de plantilla](/help/sites-developing/page-templates-editable.md).

Una vez que pulse para abrir una carpeta, encontrará un botón Crear que permite crear una nueva plantilla para formularios adaptables.

### Crear una plantilla {#create-template}

Después de crear una carpeta, ábrala y realice los pasos siguientes para crear una plantilla:

1. En la consola Plantilla , pulse **Crear** dentro de la carpeta que ha creado.
1. En la sección Elegir un tipo de plantilla , seleccione **Plantilla de formulario adaptable** y pulse **Siguiente**.

1. En la sección Detalles de plantilla , proporcione un Título de plantilla y pulse **Crear**.
Puede proporcionar una descripción y una miniatura que pueda ver cuando puede seleccionar la plantilla creada en el momento de la creación del formulario.

1. Toque **Listo** para volver a la consola o pulse **Abrir** para abrir la plantilla en el editor.

### Interfaz de usuario del editor de plantillas {#template-editor-ui}

Cuando abra una plantilla para editarla, verá los siguientes componentes AEM Editor:

* **Barra de**
herramientas de páginaContiene las siguientes opciones:

   * **Alternar panel lateral**: Permite mostrar u ocultar la barra lateral.
   * **Información** de página: Permite especificar información, como el tiempo de publicación/cancelación de publicación, las miniaturas, las bibliotecas del lado del cliente, la directiva de página y la biblioteca del lado del cliente de diseño de página.
   * **Emulador**: Permite simular y personalizar el aspecto de distintos dispositivos.
   * **Selector de capa:** permite cambiar la capa.
Puede elegir la capa **Structure** o la capa **Initial Content**. La capa de estructura permite añadir y personalizar el encabezado y el pie de página. La capa Contenido inicial permite personalizar el contenido del formulario.

   * **Vista previa:** permite previsualizar el aspecto de la plantilla cuando la publica. Puede utilizar Selector de capa y Vista previa para alternar los modos de edición y vista previa.

* **Barra lateral:** proporciona los navegadores Contenido, Propiedades, Recursos y Componentes.
* **Barra de herramientas de componentes:** cuando selecciona un componente, aparece una barra de herramientas que le permite personalizar el componente.
* **Página**: Área donde se agrega contenido para crear la plantilla.

Consulte [Introducción a la creación de formularios adaptables](../../forms/using/introduction-forms-authoring.md) para comprender el editor de IU táctil.

### Edición de una plantilla {#editing-a-template}

Se crea una plantilla de formulario adaptable con dos capas:

* Estructura
* Contenido inicial

El selector de capas está disponible junto a la opción Vista previa en la esquina superior derecha de la pantalla.

### Estructura {#structure}

Al seleccionar la capa de estructura en el Editor de plantillas, puede ver los contenedores de diseño encima y debajo del contenedor del formulario adaptable. Los autores pueden utilizar estos contenedores de diseño para el encabezado y el pie de página. Puede agregar, editar o personalizar el encabezado y el pie de página. Arrastre y suelte el componente Encabezado de formulario adaptable en el contenedor de diseño sobre el contenedor de formulario adaptable para personalizar el encabezado de la plantilla. Arrastre y suelte el componente Pie de página del formulario adaptable en el contenedor de diseño debajo del contenedor del formulario adaptable para personalizar el pie de página de la plantilla.

![Contenedor de diseño en la capa de estructura](assets/header-layer-selector.png)

Contenedores de diseño en la capa de estructura

**A.** Contenedor de diseño para el componente de encabezado  **B.** Contenedor de diseño para el componente de pie de página

Arrastre y suelte el componente Encabezado de formulario adaptable en el contenedor de diseño situado encima del contenedor de formulario adaptable. Después de agregar el componente, puede especificar sus propiedades, que le permiten agregar un logotipo y proporcionar su título.

Del mismo modo, cuando arrastra y suelta el componente de pie de página en el contenedor de diseño debajo del contenedor de formulario adaptable, puede proporcionar la información de copyright y los detalles de la empresa.

![Encabezado y pie de página agregados en la capa Estructura](assets/header-and-footer.png)

Encabezado y pie de página agregados en la capa Estructura

#### Bloqueo/desbloqueo de componentes en la capa de estructura {#locking-unlocking-components-in-the-structure-layer}

Cuando edita la plantilla con la capa de estructura seleccionada, puede desbloquear el encabezado y el pie de página de la plantilla. Si un componente está desbloqueado en la plantilla, los autores de formularios pueden editar el componente en el formulario adaptable que utiliza la plantilla. Bloquear un componente impide que los autores de formularios lo editen en el formulario adaptable. La opción Bloquear está disponible en la barra de herramientas de componentes.

Por ejemplo, puede añadir el componente de encabezado en la plantilla. Al seleccionar el componente, puede ver una opción de bloqueo en la barra de herramientas de componentes. Normalmente, el encabezado incluye el nombre de la empresa y el logotipo, y no desea que los autores de formularios cambien el logotipo y el encabezado de una plantilla. En un formulario adaptable creado con la plantilla con el componente de encabezado bloqueado, los autores de formularios no pueden cambiar el logotipo y el nombre de la empresa.

>[!NOTE]
>
>No se recomienda bloquear o desbloquear la imagen o el logotipo en el componente del encabezado de forma individual. Puede desbloquear el componente del encabezado.

### Contenido inicial {#initial-content}

Cuando se selecciona la opción Contenido inicial , el contenedor de formulario adaptable de la plantilla se abre como un formulario adaptable para su edición. Al igual que la creación de un formulario adaptable, puede especificar la configuración inicial, como seleccionar un tema y enviar acciones.

Los autores de formularios lo utilizan como base para crear un formulario. La estructura del flujo de contenido se especifica en la capa Initial Content de la plantilla. Para cambiar a la edición del contenido inicial de la plantilla de formulario, antes de Vista previa en la barra de herramientas de la página, pulse ![canvas-drop](assets/canvas-drop-down.png) **> Contenido inicial**.
![Capa de contenido inicial en el Editor de plantillas](assets/initial-content-layer.png)

La capa de contenido inicial en el Editor de plantillas muestra el contenedor de formulario adaptable seleccionado para especificar propiedades.

![contenido inicial](assets/initial-content-layer-1.png)

En la capa Contenido inicial , se crea la plantilla de formulario adaptable que los autores utilizan como base. La creación de una plantilla es similar a la creación de un formulario, se utilizan las opciones disponibles en la barra lateral. La barra lateral proporciona navegadores de contenido, propiedades, recursos y componentes.

Consulte [Barra lateral](../../forms/using/introduction-forms-authoring.md#sidebar).

>[!NOTE]
>
>Cuando selecciona Almacenar contenido o Almacenar PDF como Acción de envío, obtiene una opción para especificar la ruta de almacenamiento. Si especifica la ruta en la plantilla, todos los formularios creados a partir de ella tendrán la misma ruta. Puede especificar la ruta de almacenamiento correcta o asegurarse de que los autores de los formularios lo actualicen para evitar que los datos de todos los formularios se almacenen en la misma ubicación.

#### Creación de una plantilla de formulario adaptable con fichas y paneles  {#creating-an-adaptive-form-template-with-tabs-and-panels-nbsp}

Por ejemplo, desea crear una plantilla con las siguientes pestañas:

* Información general
* Información profesional

Ha agregado un logotipo, proporcionado un título y agregado un pie de página en la capa de estructura. Bloquee el encabezado y el pie de página para impedir que los autores de formularios los editen cuando utilicen la plantilla para crear formularios.

Cambie la capa de Estructura a Contenido inicial y empiece a añadir contenido al formulario. Para crear una estructura con fichas, agregue un Panel secundario en el guideRootPanel del contenedor del formulario adaptable. Para agregar un panel:

* Puede agregar un panel tocando el botón **+** cuando seleccione la opción **Arrastrar componentes aquí**.

* Puede arrastrar y soltar el componente del panel desde el navegador de componentes de la barra lateral.
* Puede añadir el panel secundario del `guideRootPanel` desde la barra de herramientas de componentes.

Para crear las pestañas Información general e Información profesional , agregue dos paneles en el panel secundario del `guideRootPanel`. Seleccione los paneles y pulse ![cmppr](assets/cmppr.png) para abrir las propiedades en la barra lateral. Cambie los nombres de los elementos como `general-info` y `professional-info`, y los títulos como Información general e Información profesional respectivamente. En la barra lateral, pulse contenido para abrir el navegador de contenido. En la ficha Objetos de formulario, seleccione `guideRootPanel`. En el editor, se selecciona guideRootPanel . Pulse ![cmppr](assets/cmppr.png) en la barra de herramientas de componentes para abrir sus propiedades. En el campo Diseño del panel , seleccione **Tabs on Top** y pulse **Listo**. Se aplica la estructura de la plantilla con pestañas.

#### Adición de contenido en pestañas {#adding-content-in-tabs}

![Adición de campos en la plantilla de formulario adaptable](assets/template-edit-initial-content.png)

Después de agregar paneles y estructurarlos como fichas, puede agregar campos dentro de las pestañas. Cuando selecciona una pestaña en el editor, puede ver la opción **Arrastrar componentes aquí**. Puede arrastrar y soltar componentes, como cuadros de texto, elementos de lista y botones. Puede arrastrar y soltar componentes desde el navegador de componentes en la barra lateral.

Cada componente tiene propiedades que mejoran la captura y manipulación de datos. Por ejemplo, puede activar la propiedad **Required field** de un componente. Los autores pueden especificar un mensaje que los clientes verán cuando omitan rellenar un campo obligatorio. Especifique el mensaje en la propiedad **Mensaje de campo obligatorio**.

En los campos plantilla de ejemplo, Nombre, Número de teléfono y Fecha de nacimiento se añaden en la pestaña Información general . En la pestaña Información profesional , Actualmente empleada, tipo de empleo, se añaden campos de cualificación educativa .

Después de agregar campos, puede agregar botones como Enviar y Restablecer.

### Activación de la plantilla {#enabling-the-template}

Al crear una plantilla, esta se agrega como borrador. Active la plantilla para utilizarla en la creación de formularios adaptables. Para habilitar una plantilla:

1. Vaya a **Adobe Experience Manager > Herramientas > Plantillas** y abra la carpeta en la que ha creado la plantilla.

1. La plantilla que ha creado se marca como borrador.
1. Seleccione la plantilla y pulse **Habilitar** en la barra de herramientas.
Al crear un formulario adaptable, puede ver la plantilla en la lista cuando se le pide que elija una plantilla.

## Importación o exportación de una plantilla {#importing-or-exporting-a-template}

Un formulario funciona con su plantilla. Al descargar un formulario adaptable creado con una plantilla personalizada, la plantilla no se descarga. Al importar el formulario en una instancia de AEM Forms diferente, se importa sin su plantilla. Si se importa un formulario pero su plantilla no está disponible, el formulario no se procesa. Puede empaquetar la plantilla personalizada desde el nodo `/conf` en `https://<server>:<port>/crx/packmgr` y portarla en la instancia de AEM Forms donde desee cargar el formulario.

## Creación de un formulario adaptable mediante la plantilla {#creating-an-adaptive-form-using-the-template}

Después de crear y habilitar una plantilla, esta estará disponible en el administrador de formularios al crear un formulario adaptable. Para utilizar una plantilla y crear un formulario adaptable, consulte [Creación de un formulario adaptable](../../forms/using/creating-adaptive-form.md).

## Cambiar la opción de visualización de las plantillas predeterminadas {#change-display-option-of-out-of-the-box-templates}

Puede crear plantillas personalizadas para formularios adaptables para definir la estructura básica y el contenido inicial. AEM Forms también proporciona un conjunto de plantillas predeterminadas para formularios adaptables. Puede elegir mostrar u ocultar las plantillas.

Siga estos pasos para mostrar y ocultar plantillas:

1. Inicie sesión en la instancia de autor de AEM Forms y vaya a **Tools** > **Operations** > **Web Console**.

   >[!NOTE]
   >
   >La URL de AEM consola web es https://&#39;[server]:[port]&#39;/system/console/configMgr

1. Busque y abra la configuración **FormsManager Configuration**:

   * Para mostrar u ocultar la plantilla de formularios adaptables, marque o desmarque la opción **Incluir fuera de la caja AF y Plantillas de AD**.
   * Para mostrar u ocultar las plantillas de formulario adaptables que se agregaron en AEM versión 6.0 de Forms o AEM 6.1 de Forms pero que ahora están en desuso, marque o desmarque la opción **Incluir plantillas AEM 6.0 AF**. Si esta opción está marcada, para que surta efecto, requiere que la configuración **Include Out of the box AF and AD Templates** esté habilitada.

1. Haga clic en **Guardar**. Se cambian las opciones de visualización de las plantillas predeterminadas.

## Recomendaciones {#recommendations}

* Cuando modifique las propiedades del formulario en el editor de plantillas, no utilice la propiedad BindReference .
* Si desea agregar un punto de interrupción, créelo cuando cree una plantilla de formulario adaptable.
Para obtener más información sobre los puntos de interrupción, consulte [Diseño interactivo](/help/sites-authoring/responsive-layout.md).

