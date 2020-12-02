---
title: Plantillas de formulario adaptables
seo-title: Plantillas de formulario adaptables
description: Cree plantillas de formulario adaptables definiendo la estructura básica y el contenido inicial del formulario con el Editor de plantillas.
seo-description: Cree plantillas de formulario adaptables definiendo la estructura básica y el contenido inicial del formulario con el Editor de plantillas.
uuid: 317ca3ab-f809-49a7-a063-9d0c17a35fe4
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: b21a48ba-eccd-4bb5-9b92-3039026ddf2a
docset: aem65
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1984'
ht-degree: 0%

---


# Plantillas de formulario adaptables{#adaptive-form-templates}

Cuando se crea un formulario, se agregan campos y componentes para definir la estructura, el contenido y las acciones del formulario en el editor. Los campos y componentes se agregan en el `guideRootPanel` del contenedor de formulario. Con el Editor de plantillas, puede crear una plantilla que contenga estructura básica y contenido inicial que los autores puedan utilizar para crear formularios.

Por ejemplo, desea que todos los autores de formularios tengan determinados cuadros de texto, botones de navegación y un botón de envío en un formulario de inscripción. Puede crear una plantilla con los componentes que los autores pueden utilizar para crear un formulario coherente con otros formularios de matriculación. Cuando los autores utilizan la plantilla para crear un formulario adaptable, el nuevo formulario hereda la estructura y los componentes especificados en la plantilla. El Editor de plantillas le permite:

* Añada los componentes de encabezado y pie de página de un formulario en la capa de estructura.
* Proporcione el contenido inicial del formulario.
* Especifique un tema y envíe acciones.

## Uso de plantillas {#working-with-templates}

Puede acceder al editor de plantillas desde el menú Herramientas navegando a **Adobe Experience Manager > Herramientas > Plantillas**. Aquí, las plantillas están organizadas en carpetas habilitadas para plantillas editables. AEM proporciona una carpeta global para organizar las plantillas. Sin embargo, no está activado de forma predeterminada. Puede solicitar al administrador que habilite la carpeta global o que cree una nueva carpeta para plantillas. Para obtener más información sobre cómo crear carpetas, consulte [Carpetas de plantillas](/help/sites-developing/page-templates-editable.md).

Una vez que toque para abrir una carpeta, encontrará un botón Crear que permite crear una nueva plantilla para formularios adaptables.

### Crear una plantilla {#create-template}

Después de crear una carpeta, ábrala y realice los siguientes pasos para crear una plantilla:

1. En la consola Plantilla, toque **Crear** dentro de la carpeta que ha creado.
1. En la sección Elegir un tipo de plantilla, seleccione **Plantilla de formulario adaptable** y toque **Siguiente**.

1. En la sección Detalles de plantilla, proporcione un Título de plantilla y toque **Crear**.
Puede proporcionar una descripción y una miniatura que podrá ver cuando seleccione la plantilla creada en el momento de la creación del formulario.

1. Toque **Listo** para volver a la consola o toque **Abrir** para abrir la plantilla en el editor.

### IU del editor de plantillas {#template-editor-ui}

Al abrir una plantilla para editarla, se pueden ver los siguientes componentes AEM Editor:

* **Barra de**
herramientas de páginaContiene las siguientes opciones:

   * **Alternar panel** lateral: Permite mostrar u ocultar la barra lateral.
   * **Información** de página: Permite especificar información como, por ejemplo, la hora de publicación/cancelación de publicación, las miniaturas, las bibliotecas del lado del cliente, la directiva de página y la biblioteca del lado del cliente de diseño de página.
   * **Emulador**: Permite simular y personalizar el aspecto de los distintos dispositivos.
   * **Selector de capa:** permite cambiar la capa.
Puede elegir la capa **Estructura** o **Contenido inicial**. La capa de estructura permite agregar y personalizar el encabezado y el pie de página. La capa Contenido inicial permite personalizar el contenido del formulario.

   * **Previsualización:** permite realizar una previsualización del aspecto de la plantilla al publicarla. Puede utilizar Selector de capas y Previsualización para alternar los modos de edición y previsualización.

* **Barra lateral:** Proporciona los exploradores Contenido, Propiedades, Recursos y Componentes.
* **Barra de herramientas de componentes:** cuando selecciona un componente, aparece una barra de herramientas que le permite personalizar el componente.
* **Página**: Área en la que se agrega contenido para crear la plantilla.

Consulte [Introducción a la creación de formularios adaptables](../../forms/using/introduction-forms-authoring.md) para comprender el editor de IU táctil.

### Edición de una plantilla {#editing-a-template}

Se crea una plantilla de formulario adaptable con dos capas:

* Estructura
* Contenido inicial

El selector de capas está disponible junto a la opción de Previsualización en la esquina superior derecha de la pantalla.

### Estructura {#structure}

Al seleccionar la capa de estructura en el Editor de plantillas, se pueden ver los contenedores de diseño encima y debajo del Contenedor Formulario adaptable. Los autores pueden utilizar estos contenedores de diseño para el encabezado y el pie de página. Puede agregar, editar o personalizar el encabezado y el pie de página. Arrastre y suelte el componente Encabezado de formulario adaptable en el contenedor de presentación encima del Contenedor Formulario adaptable para personalizar el encabezado de la plantilla. Arrastre y suelte el componente Pie de página del formulario adaptable en el contenedor de presentación debajo del Contenedor Formulario adaptable para personalizar el pie de página de la plantilla.

![Contenedor de diseño en la capa de estructura](assets/header-layer-selector.png)

Contenedores de diseño en la capa de estructura

**A.** contenedor de diseño para el componente Encabezado  **B.** contenedor de diseño para el componente Pie de página

Arrastre y suelte el componente Encabezado de formulario adaptable en el contenedor de presentación encima del Contenedor Formulario adaptable. Después de agregar el componente, puede especificar sus propiedades que le permiten agregar un logotipo y proporcionar su título.

Del mismo modo, cuando arrastra y suelta el componente de pie de página en el contenedor de presentación debajo del Contenedor Formulario adaptable, puede proporcionar la información de copyright y los detalles de compañía.

![Encabezado y pie de página agregados en la capa Estructura](assets/header-and-footer.png)

Encabezado y pie de página agregados en la capa Estructura

#### Bloqueo y desbloqueo de componentes en la capa de estructura {#locking-unlocking-components-in-the-structure-layer}

Cuando edita la plantilla con la capa de estructura seleccionada, puede desbloquear el encabezado y el pie de página de la plantilla. Si un componente está desbloqueado en la plantilla, los autores de formularios pueden editar el componente en el formulario adaptable que utiliza la plantilla. Bloquear un componente impide que los autores de formularios lo editen en el formulario adaptable. La opción Bloquear está disponible en la barra de herramientas de componentes.

Por ejemplo, se agrega el componente de encabezado a la plantilla. Cuando selecciona el componente, puede ver una opción de bloqueo en la barra de herramientas del componente. Normalmente, el encabezado incluye el nombre y el logotipo de la compañía y no desea que los autores de formularios cambien el logotipo y el encabezado de una plantilla. En un formulario adaptable creado con la plantilla con el componente de encabezado bloqueado, los autores de formularios no pueden cambiar el logotipo ni el nombre de la compañía.

>[!NOTE]
>
>No se recomienda bloquear o desbloquear la imagen o el logotipo en el componente de encabezado de forma individual. Puede desbloquear el componente de encabezado.

### Contenido inicial {#initial-content}

Cuando se selecciona la opción Contenido inicial, el Contenedor Formulario adaptable de la plantilla se abre como un formulario adaptable para la edición. Al igual que la creación de un formulario adaptable, puede especificar la configuración inicial, como seleccionar un tema y enviar acciones.

Los autores de formularios lo utilizan como base para crear un formulario. La estructura de flujo de contenido se especifica en la capa Contenido inicial de la plantilla. Para cambiar a la edición del contenido inicial de la plantilla de formulario, antes de la Previsualización en la barra de herramientas de la página, toque ![lienzo-desplegable](assets/canvas-drop-down.png) **Contenido inicial**.
![Capa de contenido inicial en el Editor de plantillas](assets/initial-content-layer.png)

La capa de contenido inicial del Editor de plantillas muestra el Contenedor de formulario adaptable seleccionado para especificar propiedades.

![contenido inicial](assets/initial-content-layer-1.png)

En la capa Contenido inicial, se crea la plantilla de formulario adaptable que los autores utilizan como base. La creación de una plantilla es similar a la creación de un formulario; se utilizan las opciones disponibles en la barra lateral. La barra lateral proporciona exploradores de contenido, propiedades, recursos y componentes.

Consulte [Barra lateral](../../forms/using/introduction-forms-authoring.md#sidebar).

>[!NOTE]
>
>Al seleccionar Almacenar contenido o StorePDF como acción de envío, se obtiene una opción para especificar la ruta de Almacenamiento. Si especifica una ruta en la plantilla, todos los formularios creados a partir de ella tendrán la misma ruta. Puede especificar la ruta de almacenamiento correcta o asegurarse de que los autores de formularios la actualicen para evitar que los datos de todos los formularios se almacenen en la misma ubicación.

#### Creación de una plantilla de formulario adaptable con fichas y paneles  {#creating-an-adaptive-form-template-with-tabs-and-panels-nbsp}

Por ejemplo, desea crear una plantilla con las fichas siguientes:

* Información general
* Información profesional

Ha agregado un logotipo, proporcionado un título y un pie de página en la capa de estructura. Bloquear el encabezado y el pie de página para evitar que los autores de formularios los editen cuando utilicen la plantilla para crear formularios.

Cambie la capa de Estructura a Contenido inicial y inicio para agregar contenido al formulario. Para crear una estructura con fichas, agregue un Panel secundario en el parámetro guideRootPanel del contenedor Formulario adaptable. Para agregar un panel:

* Puede agregar un panel tocando el botón **+** cuando seleccione la opción **Arrastrar componentes aquí**.

* Puede arrastrar y soltar el componente de panel desde el navegador de componentes en la barra lateral.
* Puede agregar el panel secundario del `guideRootPanel` desde la barra de herramientas de componentes.

Para crear las fichas Información general e Información profesional, agregue dos paneles en el panel secundario del `guideRootPanel`. Seleccione los paneles y toque ![cmppr](assets/cmppr.png) para abrir las propiedades en la barra lateral. Cambie los nombres de los elementos como `general-info` y `professional-info`, y los títulos como Información general e Información profesional respectivamente. En la barra lateral, toque contenido para abrir el navegador de contenido. En la ficha Objetos de formulario, seleccione `guideRootPanel`. En el editor, se selecciona guideRootPanel. Toque ![cmppr](assets/cmppr.png) en la barra de herramientas de componentes para abrir sus propiedades. En el campo Diseño del panel, seleccione **Fichas en la parte superior** y toque **Listo**. Se aplica la estructura de plantilla con fichas.

#### Añadir contenido en fichas {#adding-content-in-tabs}

![Añadir campos en la plantilla de formulario adaptable](assets/template-edit-initial-content.png)

Después de agregar paneles y estructurarlos como fichas, puede agregar campos dentro de las fichas. Cuando selecciona una ficha en el editor, puede ver la opción **Arrastrar componentes aquí**. Puede arrastrar y soltar componentes como cuadros de texto, elementos de lista y botones. Puede arrastrar y soltar componentes desde el navegador de componentes en la barra lateral.

Cada componente tiene propiedades que mejoran la captura y manipulación de datos. Por ejemplo, puede habilitar la propiedad **Campo requerido** de un componente. Los autores pueden especificar un mensaje que sus clientes verán cuando omitan rellenar un campo obligatorio. Especifique el mensaje en la propiedad **Mensaje de campo requerido**.

En la plantilla de ejemplo, los campos Nombre, Número de teléfono y Fecha de nacimiento se agregan en la ficha Información general. En la ficha Información profesional, se agregan campos de cualificación educativa, Tipo de empleo actualmente empleado y Tipo de empleo.

Después de agregar campos, puede agregar botones como Enviar y Restablecer.

### Habilitación de la plantilla {#enabling-the-template}

Al crear una plantilla, ésta se agrega como borrador. Active la plantilla para utilizarla en la creación de formularios adaptables. Para habilitar una plantilla:

1. Vaya a **Adobe Experience Manager > Herramientas > Plantillas** y abra la carpeta en la que ha creado la plantilla.

1. La plantilla que ha creado se marca como borrador.
1. Seleccione la plantilla y toque **Habilitar** en la barra de herramientas.
Al crear un formulario adaptable, puede ver la plantilla en la lista cuando se le pida que elija una plantilla.

## Importación o exportación de una plantilla {#importing-or-exporting-a-template}

Un formulario funciona con su plantilla. Cuando se descarga un formulario adaptable creado con una plantilla personalizada, la plantilla no se descarga. Al importar el formulario en una instancia de AEM Forms diferente, se importa sin su plantilla. Si se importa un formulario pero su plantilla no está disponible, el formulario no se procesa. Puede empaquetar la plantilla personalizada desde el nodo `/conf` en `https://<server>:<port>/crx/packmgr` y portarla en la instancia de AEM Forms donde desee cargar el formulario.

## Creación de un formulario adaptable mediante la plantilla {#creating-an-adaptive-form-using-the-template}

Después de crear y activar una plantilla, estará disponible en el administrador de formularios al crear un formulario adaptable. Para utilizar una plantilla y crear un formulario adaptable, consulte [Creación de un formulario adaptable](../../forms/using/creating-adaptive-form.md).

## Cambiar la opción de visualización de las plantillas predeterminadas {#change-display-option-of-out-of-the-box-templates}

Puede crear plantillas personalizadas para formularios adaptables para definir la estructura básica y el contenido inicial. AEM Forms también proporciona un conjunto de plantillas integradas para formularios adaptables. Puede elegir mostrar u ocultar las plantillas.

Siga estos pasos para mostrar y ocultar plantillas:

1. Inicie sesión en la instancia de creación de AEM Forms y vaya a **Herramientas** > **Operaciones** > **Consola Web**.

   >[!NOTE]
   >
   >La dirección URL de AEM consola web es https://&#39;[server]:[port]&#39;/system/console/configMgr

1. Busque y abra la configuración de **Configuración de FormsManager**:

   * Para mostrar u ocultar la plantilla de formularios adaptables, marque o desmarque la opción **Incluir fuera de la casilla Plantillas AF y AD**.
   * Para mostrar u ocultar las plantillas de formulario adaptables predeterminadas que se agregaron en las versiones de AEM 6.0 Forms o AEM 6.1 de Forms pero que ahora están en desuso, marque o desmarque la opción **Incluir plantillas AF AEM 6.0**. Si esta opción está activada, para que surta efecto, requiere que se habilite la configuración **Incluir fuera de la casilla Plantillas AF y Plantillas de AD**.

1. Haga clic en **Guardar.** Se cambian las opciones de visualización de las plantillas listas para usar.

## Recomendaciones {#recommendations}

* Cuando modifique las propiedades del formulario en el editor de plantillas, no utilice la propiedad BindReference.
* Si desea agregar un punto de interrupción, créelo cuando cree una plantilla de formulario adaptable.
Para obtener más información sobre los puntos de interrupción, consulte [Diseño interactivo](/help/sites-authoring/responsive-layout.md).

