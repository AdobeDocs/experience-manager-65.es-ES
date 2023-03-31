---
title: Funciones de la comunidad
seo-title: Community Functions
description: Obtenga información sobre cómo acceder a la consola Funciones de la comunidad
seo-description: Learn how to access the Community Functions console
uuid: d3d70134-f318-4709-a673-b01a3467d980
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 91833914-b811-4355-a97d-e1a9cb7441f1
docset: aem65
role: Admin
exl-id: 2395c895-c611-43ac-abb6-c2bc4b4a41f4
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '2224'
ht-degree: 6%

---

# Funciones de la comunidad{#community-functions}

El tipo de funciones que se esperan de una experiencia de comunidad son bien conocidas. Las funciones de comunidad están disponibles como funciones de la comunidad. Fundamentalmente, son una o más páginas precableadas para implementar una función de comunidad que requiere algo más que simplemente añadir un componente a una página en modo de autor. Son los componentes básicos utilizados para definir la estructura de una [plantilla del sitio de la comunidad](/help/communities/sites.md) desde los cuales se encuentran los sitios de la comunidad [created](/help/communities/sites-console.md).

Una vez creado el sitio de la comunidad, se puede agregar contenido a las páginas resultantes mediante el estándar [AEM modo de creación](/help/sites-authoring/editing-content.md). Hay varias funciones de la comunidad disponibles como se ve en la consola de funciones de la comunidad.

>[!NOTE]
>
>Las consolas para la creación de [sitios de la comunidad](/help/communities/sites-console.md), [plantillas de sitio de la comunidad](/help/communities/sites.md), [plantillas de grupo de la comunidad](/help/communities/tools-groups.md)y [funciones de la comunidad](/help/communities/functions.md) solo se utilizan en el entorno de creación.

## Consola Funciones de la comunidad {#community-functions-console}

Para llegar a la consola de funciones de la comunidad en el entorno de creación:

* Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Funciones de la comunidad]**.

![funciones de comunidad](assets/community-functions.png)

## Funciones creadas previamente {#pre-built-functions}

A continuación se ofrece una breve descripción de las funciones entregadas con AEM Communities. Cada función incluye una o varias páginas AEM que contienen componentes de Communities conectados en una función que se incorpora fácilmente en una [plantilla del sitio de la comunidad](/help/communities/sites.md).

Una plantilla de sitio de la comunidad proporciona la estructura para un sitio de la comunidad, que incluye: inicio de sesión, perfiles de usuario, notificaciones, mensajes, menú del sitio, búsqueda, tema y funciones de marca.

### Configuración de título y dirección URL {#title-and-url-settings}

**Título** y **URL** son propiedades comunes a todas las funciones de la comunidad.

Cuando se agrega una función de comunidad a una plantilla de sitio de comunidad o se agrega al [modificar](/help/communities/sites-console.md#modifying-site-properties) En la estructura de un sitio de comunidad, se abre el cuadro de diálogo de la función para que se puedan configurar el Título y la URL.

#### Detalles de la función de configuración {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **Título**

   (*Requerido*) Texto que aparece en el menú de características del sitio

* **URL**

   (*Requerido*) Nombre utilizado para generar el URI. El nombre debe cumplir la función [convenciones de nomenclatura](/help/sites-developing/naming-conventions.md) impuesto por AEM y JCR.

Por ejemplo, usar el sitio creado a partir de la variable [Introducción](/help/communities/getting-started.md) tutorial, si

* Título = Página Web
* URL = página

A continuación, la dirección URL de la página es https://localhost:4503/content/sites/engage/en/page.html

y el vínculo de menú de la página aparece como:

![página de participación](assets/engage-page.png)

### Función Secuencia de actividades {#activity-stream-function}

La función de flujo de actividad es una página con un [Componente Flujos de actividad](/help/communities/activities.md) con todas las vistas seleccionadas (todas las actividades, actividades de usuario y siguientes). Consulte también [Aspectos básicos del flujo de actividad](/help/communities/essentials-activities.md) para desarrolladores.

Cuando se agrega a una plantilla, se abre el cuadro de diálogo siguiente:

#### Detalles de la función de configuración {#configuration-function-details-1}

![function-details](assets/function-details.png)

* [Configuración de título y dirección URL](#title-and-url-settings)

* **Mostrar vista de “Mis actividades”**

   Si se selecciona, la página Actividades incluye una pestaña que filtra las actividades en función de las generadas dentro de la comunidad por el miembro actual. El valor predeterminado está seleccionado.

* **Mostrar vista de “todas las actividades”**

   Si se selecciona, la página Actividades incluye una pestaña que incluye todas las actividades generadas dentro de la comunidad a la que tiene acceso el miembro actual. El valor predeterminado está seleccionado.

* **Mostrar vista de “Últimas noticias”**

   Si se selecciona, las páginas Actividades incluyen una pestaña que filtra las actividades en función de las que sigue el miembro actual. El valor predeterminado está seleccionado.

### Función Blog {#blog-function}

La función de blog es una página con un [Componente de blog](/help/communities/blog-feature.md) configurado para etiquetado, cargas de archivos, seguimiento, miembros para autoedición, votación y moderación. Consulte también [Elementos esenciales del blog](/help/communities/blog-developer-basics.md) para desarrolladores.

Cuando se agrega a una plantilla, se abre el cuadro de diálogo siguiente:

![blog-component](assets/blog-component.png)

* [Configuración de título y dirección URL](#title-and-url-settings)

* **Permitir miembros privilegiados**

   Si se selecciona, el blog solo permite que los miembros privilegiados creen artículos permitiendo la selección de un [grupo de miembros privilegiados](/help/communities/users.md#privileged-members-group). Si no se selecciona, todos los miembros de la comunidad pueden crear. El valor predeterminado no está seleccionado.

* **Permitir cargas de archivos**

   Si se selecciona, el blog incluye la posibilidad de que los miembros carguen archivos. El valor predeterminado está seleccionado.

* **Permitir respuestas de debate**

   Si no se selecciona, el blog permite respuestas (comentarios) a un artículo, pero no se permiten respuestas a comentarios. El valor predeterminado está seleccionado.

* **Permitir contenido destacado**

   Si se selecciona, el blog se identifica como [contenido destacado](/help/communities/featured.md). El valor predeterminado está seleccionado.

### Función Calendario {#calendar-function}

La función de calendario es una página con un [Componente de calendario](/help/communities/calendar.md) configurado para permitir el etiquetado. Consulte también [Elementos básicos del calendario](/help/communities/calendar-basics-for-developers.md) para desarrolladores.

Cuando se agrega a una plantilla, se abre el cuadro de diálogo siguiente:

![calendar-details](assets/calendar-details.png)

* [Configuración de título y dirección URL](#title-and-url-settings)

* **Permitir fijación**

   Si se selecciona, el foro permite que las respuestas de temas se fijen al principio de la lista de comentarios. El valor predeterminado está seleccionado.

* **Permitir miembros privilegiados**

   Si se selecciona, el blog solo permite que los miembros privilegiados creen artículos permitiendo la selección de un [grupo de miembros privilegiados](/help/communities/users.md#privileged-members-group). Si no se selecciona, todos los miembros de la comunidad pueden crear. El valor predeterminado no está seleccionado.

* **Permitir cargas de archivos**

   Si se selecciona, el blog incluye la posibilidad de que los miembros carguen archivos. El valor predeterminado está seleccionado.

* **Permitir respuestas de debate**

   Si no se selecciona, el blog permite respuestas (comentarios) a un artículo, pero no se permiten respuestas a comentarios. El valor predeterminado está seleccionado.

* **Permitir contenido destacado**

   Si se selecciona, su contenido se identifica como [contenido destacado](/help/communities/featured.md). El valor predeterminado está seleccionado.

### Función de contenido destacado {#featured-content-function}

La función de contenido destacado es una página con un [Componente de contenido destacado](/help/communities/featured.md) configurado para permitir que se agreguen y eliminen comentarios.

La capacidad de presentar contenido puede estar permitida o no permitida por componente (consulte [Función del blog](#blog-function), [Función Calendario](#calendar-function), [Función del foro](#forum-function), [Función de ideación](#ideation-function)y [Función QnA](#qna-function)).

Cuando se añade a una plantilla, la única configuración es para la variable [Configuración de título y dirección URL](#title-and-url-settings).

### Función Biblioteca del archivo {#file-library-function}

La función de biblioteca de archivos es una página con un [Componente Biblioteca de archivos](/help/communities/file-library.md) configurado para permitir que se agreguen y eliminen comentarios.

Cuando se añade a una plantilla, la única configuración es para la variable [Configuración de título y dirección URL](#title-and-url-settings).

### Función Foro {#forum-function}

La función de foro es una página con un [Componente de foro](/help/communities/forum.md) configurado para etiquetado, cargas de archivos, seguimiento, miembros para autoedición, votación y moderación.

Cuando se agrega a una plantilla, se abre el cuadro de diálogo siguiente:

#### Detalles de la función de configuración {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [Configuración de título y dirección URL](#title-and-url-settings)

* **Permitir fijación**

   Si se selecciona, el foro permite que las respuestas de temas se fijen al principio de la lista de comentarios. El valor predeterminado está seleccionado.

* **Permitir miembros privilegiados**

   Si se selecciona, el foro solo permite que los miembros privilegiados publiquen temas permitiendo la selección de un [grupo de miembros privilegiados](/help/communities/users.md#privileged-members-group). Si no se selecciona, todos los miembros de la comunidad pueden publicar. El valor predeterminado no está seleccionado.

* **Permitir cargas de archivos**

   Si se selecciona, el foro incluye la posibilidad de que los miembros carguen archivos. El valor predeterminado está seleccionado.

* **Permitir respuestas de debate**

   Si no se selecciona, el foro permite comentarios sobre un tema, pero no se permiten las respuestas a esos comentarios. El valor predeterminado está seleccionado.

* **Permitir contenido destacado**

   Si se selecciona, el contenido del componente se identifica como [contenido destacado](/help/communities/featured.md). El valor predeterminado está seleccionado.

### Función Grupos {#groups-function}

>[!CAUTION]
>
>La función de grupos debe *not* sea el *primero ni único* en la estructura de un sitio o en una plantilla de sitio de la comunidad.
>
>Cualquier otra función, como la [función de página](#page-function), debe incluirse y aparecer en primer lugar en la lista.

La función de grupos permite a los miembros de la comunidad crear subcomunidades dentro del sitio de la comunidad en el entorno de publicación.

Dependiendo de [configuración](/help/communities/sites-console.md#groupmanagement) cuando la función Grupos está incluida en un [plantilla del sitio de la comunidad](/help/communities/sites.md), los grupos pueden ser públicos o privados y se puede configurar una o más plantillas de grupo de comunidad para proporcionar una selección de plantillas cuando se crea el grupo de comunidad (como desde el entorno de publicación). A [plantilla de grupo de la comunidad](/help/communities/tools-groups.md) especifica qué funciones de Communities se crean para las páginas de grupo, como foros y calendarios.

Cuando se crea un grupo de comunidad, se crea dinámicamente un grupo de miembros para el nuevo grupo, al que se pueden asignar o unir miembros. Para obtener más información, consulte [Administración de usuarios y grupos de usuarios](/help/communities/users.md).

Como comunidades [paquete de características 1](/help/communities/deploy-communities.md#latestfeaturepack), los grupos de comunidad se crean en el entorno de creación utilizando la variable [Consola de grupos de sitios de Communities](/help/communities/groups.md)y se pueden crear en el entorno de publicación cuando está habilitado.

Cuando se agrega a una plantilla, se abre el cuadro de diálogo siguiente:

![group-template-config](assets/group-template-config.png)

* [Configuración de título y dirección URL](#title-and-url-settings)

* **Seleccione las plantillas de grupo**

   Menú desplegable que permite seleccionar una o más plantillas de grupo habilitadas a partir de las cuales el futuro creador de un nuevo grupo de comunidad (en el entorno de publicación) puede elegir.

* **Permitir miembros privilegiados**

   Si se selecciona, el foro solo permite que los miembros privilegiados publiquen temas permitiendo la selección de un [grupo de seguridad miembros privilegiados](/help/communities/users.md#privileged-members-group). Si no se selecciona, todos los miembros de la comunidad pueden publicar. El valor predeterminado no está seleccionado.

* **Permitir la creación de publicación**

   Si se selecciona, los miembros autorizados de la comunidad pueden crear un grupo en el entorno de publicación. Si se anula la selección, solo se pueden crear nuevos grupos (subcomunidades) en el entorno de creación desde la consola Grupos de sitios de Communities.
El valor predeterminado está seleccionado.

### Función ideación {#ideation-function}

La función ideation es una página con una [Componente de ideación](/help/communities/ideation-feature.md).

Cuando se agrega a una plantilla, se abre el cuadro de diálogo siguiente, que especifica los nombres predeterminados Título y URL, así como la configuración de visualización predeterminada para la plantilla:

![ideation-function](assets/ideation-function.png)

* [Configuración de título y dirección URL](#title-and-url-settings)

* **Permitir miembros privilegiados**

   Si se selecciona, el foro solo permite que los miembros privilegiados publiquen temas permitiendo la selección de un [grupo de seguridad miembros privilegiados](/help/communities/users.md#privileged-members-group). Si no se selecciona, todos los miembros de la comunidad pueden publicar. El valor predeterminado no está seleccionado.

* **Permitir cargas de archivos**

   Si se selecciona, la idea incluye la posibilidad de que los miembros carguen archivos. El valor predeterminado está seleccionado.

* **Permitir respuestas de debate**

   Si no se selecciona, la idea permite respuestas (comentarios) a un tema, pero no se permiten respuestas a comentarios. El valor predeterminado está seleccionado.

* **Permitir contenido destacado**

   Si se selecciona, su contenido se identifica como [contenido destacado](/help/communities/featured.md). El valor predeterminado está seleccionado.

### Función de la tabla de clasificación {#leaderboard-function}

La función de panel de encabezado es una página con una [Componente del panel de control](/help/communities/enabling-leaderboard.md).

**NOTA**: El componente del panel de control de Campaign necesita más configuración *after* se crea un sitio de comunidad a partir de una plantilla de comunidad que incluye la función de panel de clientes. Especificar el componente del panel de control de Campaign [reglas](/help/communities/enabling-leaderboard.md#rules-tab), que dependen de la configuración de [puntuación y distintivos](/help/communities/implementing-scoring.md) para el sitio de la comunidad.

Cuando se agrega a una plantilla, se abre el cuadro de diálogo siguiente, que especifica los nombres predeterminados Título y URL, así como la configuración de visualización predeterminada para la plantilla:

![cuadro de diálogo de la mesa de liderazgo](assets/leaderboard-dialog.png)

* [Configuración de título y dirección URL](#title-and-url-settings)

* **Mostrar distintivo**

   Si se selecciona, se incluye una columna para los iconos de distintivo en el panel frontal.
El valor predeterminado no está seleccionado.

* **Mostrar nombre del distintivo**

   Si se selecciona, se incluye una columna para el nombre del distintivo en el panel inicial.
El valor predeterminado no está seleccionado.

* **Mostrar avatar**

   Si se selecciona, la imagen de avatar del miembro se incluye en el panel de control, junto al vínculo de nombre a su perfil de miembro.
El valor predeterminado no está seleccionado.

### Función Página {#page-function}

La función de página agrega una página en blanco al sitio de la comunidad que está conectada a las características del sitio de la comunidad: inicio de sesión, menú, notificaciones, mensajería, tema y promoción de la marca. El contenido se agrega a la página mediante el uso de [modo de creación de AEM estándar](/help/sites-authoring/editing-content.md).

Cuando se añade a una plantilla, la única configuración es para la variable [Configuración de título y dirección URL](#title-and-url-settings).

### Función Preguntas y respuestas {#qna-function}

La función QnA es una página con un [Componente QnA](/help/communities/working-with-qna.md) configurado para etiquetado, cargas de archivos, seguimiento, miembros para autoedición, votación y moderación.

Cuando se agrega a una plantilla, la configuración permite restricciones a miembros con privilegios:

![qna-dialog](assets/qna-dialog.png)

* [Configuración de título y dirección URL](#title-and-url-settings)

* **Permitir fijación**

   Si se selecciona, el foro permite que las respuestas de temas se fijen al principio de la lista de comentarios. El valor predeterminado está seleccionado.

* **Permitir miembros privilegiados**

   Si se selecciona, el foro QnA solo permite que los miembros privilegiados publiquen preguntas permitiendo la selección de un [grupo de miembros privilegiados](/help/communities/users.md#privileged-members-group). Si no se selecciona, todos los miembros de la comunidad pueden publicar. El valor predeterminado no está seleccionado.

* **Permitir cargas de archivos**

   Si se selecciona, el foro QnA incluye la posibilidad de que los miembros carguen archivos. El valor predeterminado está seleccionado.

* **Permitir respuestas de debate**

   Si no se selecciona, el foro QnA permite comentarios (respuestas) a una pregunta publicada, pero no se permiten respuestas a respuestas. El valor predeterminado está seleccionado.

* **Permitir contenido destacado**

   Si se selecciona, su contenido se identifica como [contenido destacado](/help/communities/featured.md). El valor predeterminado está seleccionado.

## Crear función de la comunidad {#create-community-function}

Se llega a la capacidad de crear una función de comunidad seleccionando la variable `Create Community Function` en la parte superior de la consola Funciones de la comunidad . Se pueden crear varias funciones basadas en el mismo modelo de AEM y luego personalizarlas de forma exclusiva abriendo en modo de edición de autor.

![create-community-function](assets/create-community-function.png)

### Nombre de función de la comunidad {#community-function-name}

![function-name](assets/function-name.png)

En el panel Nombre de función de la comunidad, se configuran un nombre, una descripción y si la función está habilitada o deshabilitada:

* **Nombre de función de la comunidad**

   El nombre de función que se utiliza para la visualización y el almacenamiento.

* **Descripción de la función de la comunidad**

   La descripción de función para mostrar.

* **Deshabilitado/Habilitado**

   Conmutador que controla si se puede hacer referencia a la función.

### Modelo AEM {#aem-blueprint}

![aem-blueprint](assets/aem-blueprint.png)

En el `AEM Blueprint` , es posible seleccionar el modelo que es la implementación subyacente de la función de comunidad.

La función de la comunidad es un minisitio que incluye una o más páginas, precableadas para su inclusión en un sitio de la comunidad, incluidos el inicio de sesión, los perfiles de usuario, las notificaciones, los mensajes, el menú del sitio, la búsqueda, el tema y las funciones de promoción de la marca. Una vez creada la función, es posible [abrir la función](#open-community-function) en el modo de edición de autor y personalice la configuración de la página o del componente.

Dado que la función de comunidad se implementa como un [live copy](/help/sites-administering/msm.md#live-copies) de [modelo](/help/sites-administering/msm-livecopy.md#creatingablueprint), es posible implementar los cambios realizados en una función que afecte a todas las páginas del sitio de la comunidad creadas a partir de la variable [plantilla del sitio de la comunidad](/help/communities/sites.md) o [plantilla de grupo de la comunidad](/help/communities/tools-groups.md) que incluye la función . También es posible desasociar una página de su modelo principal para realizar modificaciones en el nivel de página.

Consulte también [Administrador de varios sitios](/help/sites-administering/msm.md).

### Miniatura    {#thumbnail}

![función-miniatura](assets/funtion-thumbnail.png)

En el panel Miniatura, se puede cargar una imagen para mostrarla en la [Consola de funciones de comunidad](#community-functions-console).

## Abrir función de la comunidad {#open-community-function}

![open-function](assets/open-function.png)

Seleccione el `Open Community Function` para entrar al modo de edición de autor para crear el contenido de la página y modificar la configuración de los componentes de la función.

### Configuración de componentes {#configuring-components}

Una función de comunidad se implementa como una Live Copy de un modelo de AEM, cuyos detalles están documentados en [Administrador de varios sitios](/help/sites-administering/msm.md).

Es posible no solo crear contenido de página, sino también configurar componentes.

Si configura un componente en una página de un sitio de comunidad creado, puede ser necesario cancelar [herencia](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) para configurar el componente. La herencia debe restablecerse cuando se complete la configuración.

Para obtener más información sobre la configuración, visite [Componentes de Communities](/help/communities/author-communities.md) para autores.

## Editar función de la comunidad {#edit-community-function}

![edit-function](assets/edit-function.png)

Seleccione el `Edit Community Function` para editar las propiedades de la función utilizando los mismos paneles que [creación de una función de comunidad](#create-community-function), incluida la activación o desactivación de la función .
