---
title: Funciones de comunidad
seo-title: Funciones de comunidad
description: Obtenga información sobre cómo acceder a la consola Funciones de comunidad
seo-description: Obtenga información sobre cómo acceder a la consola Funciones de comunidad
uuid: d3d70134-f318-4709-a673-b01a3467d980
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 91833914-b811-4355-a97d-e1a9cb7441f1
docset: aem65
translation-type: tm+mt
source-git-commit: 94a5a8d99d052d7bcf01f237dc2b73157a2f11c2
workflow-type: tm+mt
source-wordcount: '2458'
ht-degree: 6%

---


# Funciones de comunidad{#community-functions}

El tipo de características que se esperan de una experiencia de comunidad son bien conocidas. Las funciones de la comunidad están disponibles como funciones de la comunidad. Fundamentalmente, son una o más páginas preprogramadas para implementar una función de comunidad que requiere más que simplemente agregar un componente a una página en modo de autor. Son los componentes básicos utilizados para definir la estructura de una [plantilla de sitio de comunidad](/help/communities/sites.md) desde la cual se [crean los sitios de comunidad](/help/communities/sites-console.md).

Una vez creado un sitio de comunidad, se puede agregar contenido a las páginas resultantes mediante el modo de creación estándar [AEM](/help/sites-authoring/editing-content.md). Hay varias funciones de la comunidad disponibles, como se ve en la consola de funciones de la comunidad.

>[!NOTE]
>
>Las consolas para la creación de [sitios de comunidad](/help/communities/sites-console.md), [plantillas de sitio de comunidad](/help/communities/sites.md), [plantillas de grupo de comunidad](/help/communities/tools-groups.md) y [funciones de comunidad](/help/communities/functions.md) sólo se pueden usar en el entorno de creación.

## Consola de funciones de comunidad {#community-functions-console}

Para llegar a la consola de funciones de comunidad en el entorno de creación:

* Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Funciones de la comunidad]**.

![funciones de comunidad](assets/community-functions.png)

## Funciones precompiladas {#pre-built-functions}

A continuación se ofrece una breve descripción de las funciones que se ofrecen con AEM Communities. Cada función incluye una o más páginas AEM que contienen componentes de Communities conectados en una función que se incorpora fácilmente a una [plantilla de sitio de comunidad](/help/communities/sites.md).

Una plantilla de sitio de comunidad proporciona la estructura de un sitio de comunidad, incluyendo inicio de sesión, perfiles de usuario, notificaciones, mensajes, menú del sitio, búsqueda, tema y características de marca.

### Configuración de título y dirección URL {#title-and-url-settings}

**** Título y  **** URLson propiedades comunes a todas las funciones de la comunidad.

Cuando se agrega una función de comunidad a una plantilla de sitio de comunidad o cuando [modifica](/help/communities/sites-console.md#modifying-site-properties) la estructura de un sitio de comunidad, se abre el cuadro de diálogo de la función para que se puedan configurar el Título y la dirección URL.

#### Detalles de la función de configuración {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **Título**

   (*Requerido*) El texto que aparece en el menú de características del sitio

* **URL**

   (*Requerido*) El nombre utilizado para generar el URI. El nombre debe cumplir las [convenciones de nombres](/help/sites-developing/naming-conventions.md) impuestas por AEM y JCR.

Por ejemplo, si utiliza el sitio creado a partir del tutorial [Introducción](/help/communities/getting-started.md), si

* Título = Página Web
* URL = página

A continuación, la dirección URL de la página es https://localhost:4503/content/sites/engage/en/page.html

y el vínculo de menú de la página aparece como:

![engagement-page](assets/engage-page.png)

### Función Secuencia de actividades {#activity-stream-function}

La función de flujo de actividad es una página con un [componente Flujos de Actividad](/help/communities/activities.md) con todas las vistas seleccionadas (todas las actividades, actividades de usuario y siguientes). Consulte también [Actividad Stream Essentials](/help/communities/essentials-activities.md) para desarrolladores.

Cuando se agrega a una plantilla, se abre el siguiente cuadro de diálogo:

#### Detalles de la función de configuración {#configuration-function-details-1}

![function-details](assets/function-details.png)

* [Configuración de título y dirección URL](#title-and-url-settings)

* **Mostrar vista de “Mis actividades”**

   Si se selecciona, la página Actividades incluye una ficha que filtros actividades basadas en las generadas dentro de la comunidad por el miembro actual. Predeterminado está seleccionado.

* **Mostrar vista de “todas las actividades”**

   Si se selecciona, la página Actividades incluye una ficha que incluye todas las actividades generadas dentro de la comunidad a la que tiene acceso el miembro actual. Predeterminado está seleccionado.

* **Mostrar vista de “Últimas noticias”**

   Si se selecciona, las páginas de Actividades incluyen una ficha que filtros actividades en función de las que sigue el miembro actual. Predeterminado está seleccionado.

### Función Asignaciones {#assignments-function}

La función de asignaciones es la función básica que define un [sitio de comunidad para la habilitación](/help/communities/overview.md#enablement-community). Permite asignar recursos de habilitación a los miembros de la comunidad. Consulte también [Assignments Essentials](/help/communities/essentials-assignments.md) para desarrolladores.

Esta función está disponible como una función del complemento [de habilitación](/help/communities/enablement.md). El complemento de habilitación requiere licencias adicionales para su uso en un entorno de producción.

Cuando se agrega a una plantilla, la única configuración es para [Configuración de título y URL](#title-and-url-settings).

### Función Blog {#blog-function}

La función de blog es una página con un [componente de blog](/help/communities/blog-feature.md) configurado para el etiquetado, la carga de archivos, el seguimiento y los miembros para la autoedición, la votación y la moderación. Consulte también [Blog Essentials](/help/communities/blog-developer-basics.md) para desarrolladores.

Cuando se agrega a una plantilla, se abre el siguiente cuadro de diálogo:

![blog-component](assets/blog-component.png)

* [Configuración de título y dirección URL](#title-and-url-settings)

* **Permitir miembros privilegiados**

   Si se selecciona, el blog solo permite que los miembros con privilegios creen artículos permitiendo la selección de un [grupo de miembros con privilegios](/help/communities/users.md#privileged-members-group). Si no se selecciona, todos los miembros de la comunidad pueden crear. El valor predeterminado no está seleccionado.

* **Permitir cargas de archivos**

   Si se selecciona, el blog incluye la posibilidad de que los miembros carguen archivos. Predeterminado está seleccionado.

* **Permitir respuestas de debate**

   Si no se selecciona, el blog permite respuestas (comentarios) a un artículo, pero no se permiten respuestas a los comentarios. Predeterminado está seleccionado.

* **Permitir contenido destacado**

   Si se selecciona, el blog se identifica como [contenido destacado](/help/communities/featured.md). Predeterminado está seleccionado.

### Función Calendario {#calendar-function}

La función de calendario es una página con un [componente de calendario](/help/communities/calendar.md) configurado para permitir el etiquetado. Consulte también [Calendar Essentials](/help/communities/calendar-basics-for-developers.md) para desarrolladores.

Cuando se agrega a una plantilla, se abre el siguiente cuadro de diálogo:

![calendar-details](assets/calendar-details.png)

* [Configuración de título y dirección URL](#title-and-url-settings)

* **Permitir fijación**

   Si se selecciona, el foro permite que las respuestas al tema se fijen al principio de la lista de comentarios. Predeterminado está seleccionado.

* **Permitir miembros privilegiados**

   Si se selecciona, el blog solo permite que los miembros con privilegios creen artículos permitiendo la selección de un [grupo de miembros con privilegios](/help/communities/users.md#privileged-members-group). Si no se selecciona, todos los miembros de la comunidad pueden crear. El valor predeterminado no está seleccionado.

* **Permitir cargas de archivos**

   Si se selecciona, el blog incluye la posibilidad de que los miembros carguen archivos. Predeterminado está seleccionado.

* **Permitir respuestas de debate**

   Si no se selecciona, el blog permite respuestas (comentarios) a un artículo, pero no se permiten respuestas a los comentarios. Predeterminado está seleccionado.

* **Permitir contenido destacado**

   Si se selecciona, su contenido se identifica como [contenido destacado](/help/communities/featured.md). Predeterminado está seleccionado.

### Función Catálogo {#catalog-function}

La función de catálogo permite que los miembros de [comunidad de habilitación](/help/communities/overview.md#enablement-community) exploren los recursos de habilitación que no están asignados a ellos. Consulte [Etiquetado de recursos de habilitación](/help/communities/tag-resources.md) y [Catalog Essentials](/help/communities/catalog-developer-essentials.md) para desarrolladores.

Todos los recursos de habilitación y las rutas de aprendizaje del sitio de la comunidad muestran en todos los catálogos si su propiedad, ` [Show in Catalog](/help/communities/resources.md)`, está establecida en true. Para incluir explícitamente recursos y rutas de aprendizaje, es necesario aplicar un [prefiltro](/help/communities/catalog-developer-essentials.md#pre-filters) al catálogo.

Cuando se agrega a una plantilla, la configuración permite especificar las Áreas de nombres de etiquetas utilizadas para configurar el filtro de etiquetas presentado en los visitantes del sitio:

![Función Catálogo](assets/catalog-function.png)

* [Configuración de título y dirección URL](#title-and-url-settings)

* **Seleccionar todos los espacios de nombres**

   Las Áreas de nombres de etiquetas seleccionadas definen las etiquetas que pueden seleccionar los visitantes para filtrar la lista de los recursos de activación enumerados en el catálogo.
Si se selecciona, están disponibles todas las Áreas de nombres de etiquetas permitidas para el sitio de la comunidad.
Si no se selecciona, es posible seleccionar una o varias Áreas de nombres permitidas para el sitio de la comunidad.
Predeterminado está seleccionado.

### Función de contenido destacado {#featured-content-function}

La función de contenido destacado es una página con un [componente de contenido destacado](/help/communities/featured.md) configurado para permitir que se agreguen y eliminen comentarios.

Se puede permitir o no admitir la capacidad de presentar contenido por componente (consulte [Función de blog](#blog-function), [Función de calendario](#calendar-function), [Función de foro](#forum-function), [Función de ideación](#ideation-function) y [Función de QnA](#qna-function)).

Cuando se agrega a una plantilla, la única configuración es para [Configuración de título y URL](#title-and-url-settings).

### Función Biblioteca del archivo {#file-library-function}

La función de biblioteca de archivos es una página con un [componente de biblioteca de archivos](/help/communities/file-library.md) configurado para permitir que se agreguen y eliminen comentarios.

Cuando se agrega a una plantilla, la única configuración es para [Configuración de título y URL](#title-and-url-settings).

### Función Foro {#forum-function}

La función de foro es una página con un [componente de foro](/help/communities/forum.md) configurado para el etiquetado, la carga de archivos, el seguimiento de miembros para la autoedición, la votación y la moderación.

Cuando se agrega a una plantilla, se abre el siguiente cuadro de diálogo:

#### Detalles de la función de configuración {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [Configuración de título y dirección URL](#title-and-url-settings)

* **Permitir fijación**

   Si se selecciona, el foro permite que las respuestas al tema se fijen al principio de la lista de comentarios. Predeterminado está seleccionado.

* **Permitir miembros privilegiados**

   Si se selecciona, el foro solo permite que los miembros con privilegios publiquen temas al permitir la selección de un [grupo de miembros con privilegios](/help/communities/users.md#privileged-members-group). Si no se selecciona, todos los miembros de la comunidad pueden publicar. El valor predeterminado no está seleccionado.

* **Permitir cargas de archivos**

   Si se selecciona, el foro incluye la posibilidad de que los miembros carguen archivos. Predeterminado está seleccionado.

* **Permitir respuestas de debate**

   Si no se selecciona, el foro permite comentarios sobre un tema, pero no se permiten las respuestas a esos comentarios. Predeterminado está seleccionado.

* **Permitir contenido destacado**

   Si se selecciona, el contenido del componente se identifica como [contenido destacado](/help/communities/featured.md). Predeterminado está seleccionado.

### Función Grupos {#groups-function}

>[!CAUTION]
>
>La función de grupos debe *no* ser la *primera ni la única* función en la estructura de un sitio o en una plantilla de sitio de comunidad.
>
>Cualquier otra función, como la [función de página](#page-function), debe incluirse y enumerarse primero.

La función de grupos permite a los miembros de la comunidad crear subcomunidades dentro del sitio de la comunidad en el entorno de publicación.

Según la [configuración](/help/communities/sites-console.md#groupmanagement) cuando la función Grupos se incluya en una [plantilla de sitio de comunidad](/help/communities/sites.md), los grupos pueden ser públicos o privados y se pueden configurar una o más plantillas de grupo de comunidad para proporcionar una selección de plantillas cuando se cree realmente el grupo de comunidad (por ejemplo, desde el entorno de publicación). Una [plantilla de grupo de comunidad](/help/communities/tools-groups.md) especifica qué características de comunidades se crean para las páginas de grupo, como los foros y los calendarios.

Cuando se crea un grupo de comunidad, se crea dinámicamente un grupo de miembros para el nuevo grupo, al que se pueden asignar o unir miembros. Para obtener más información, consulte [Administración de usuarios y grupos de usuarios](/help/communities/users.md).

A partir del paquete de funciones 1](/help/communities/deploy-communities.md#latestfeaturepack) de Communities [, los grupos de comunidades se crean en el entorno de creación mediante la consola [Grupos de sitios de comunidades](/help/communities/groups.md) y se pueden crear en el entorno de publicación cuando está habilitada.

Cuando se agrega a una plantilla, se abre el siguiente cuadro de diálogo:

![group-template-config](assets/group-template-config.png)

* [Configuración de título y dirección URL](#title-and-url-settings)

* **Seleccione las plantillas de grupo**

   Una lista desplegable que permite seleccionar una o varias plantillas de grupo habilitadas desde las que el futuro creador de un nuevo grupo de comunidad (en el entorno de publicación) puede elegir.

* **Permitir miembros privilegiados**

   Si se selecciona, el foro solo permite que los miembros con privilegios publiquen temas al permitir la selección de un [grupo de seguridad de miembros con privilegios](/help/communities/users.md#privileged-members-group). Si no se selecciona, todos los miembros de la comunidad pueden publicar. El valor predeterminado no está seleccionado.

* **Permitir la creación de publicación**

   Si se selecciona, los miembros de la comunidad autorizados pueden crear un grupo en el entorno de publicación. Si no se selecciona, los nuevos grupos (subcomunidades) solo se pueden crear en el entorno de creación desde la consola Grupos de sitios de comunidades.
Predeterminado está seleccionado.

### Función ideación {#ideation-function}

La función de ideación es una página con un [componente de ideación](/help/communities/ideation-feature.md).

Cuando se agrega a una plantilla, se abre el siguiente cuadro de diálogo, que especifica los nombres predeterminados de Título y URL, así como la configuración de visualización predeterminada de la plantilla:

![ideation-function](assets/ideation-function.png)

* [Configuración de título y dirección URL](#title-and-url-settings)

* **Permitir miembros privilegiados**

   Si se selecciona, el foro solo permite que los miembros con privilegios publiquen temas al permitir la selección de un [grupo de seguridad de miembros con privilegios](/help/communities/users.md#privileged-members-group). Si no se selecciona, todos los miembros de la comunidad pueden publicar. El valor predeterminado no está seleccionado.

* **Permitir cargas de archivos**

   Si se selecciona, la idea incluye la posibilidad de que los miembros carguen archivos. Predeterminado está seleccionado.

* **Permitir respuestas de debate**

   Si no se selecciona, la idea permite responder (comentarios) a un tema, pero no se permiten las respuestas a los comentarios. Predeterminado está seleccionado.

* **Permitir contenido destacado**

   Si se selecciona, su contenido se identifica como [contenido destacado](/help/communities/featured.md). Predeterminado está seleccionado.

### Función de la tabla de clasificación {#leaderboard-function}

La función de tabla de clasificación es una página con un [componente de tabla de clasificación](/help/communities/enabling-leaderboard.md).

**NOTA**: El componente Mesa de liderazgo necesita una configuración adicional  ** después de que el sitio de la comunidad se cree a partir de una plantilla de comunidad que incluya la función Mesa de liderazgo. Especifique las [reglas](/help/communities/enabling-leaderboard.md#rules-tab) del componente Leaderboard, que dependen de la configuración de [puntuación y distintivos](/help/communities/implementing-scoring.md) para el sitio de la comunidad.

Cuando se agrega a una plantilla, se abre el siguiente cuadro de diálogo, que especifica los nombres predeterminados de Título y URL, así como la configuración de visualización predeterminada de la plantilla:

![cuadro de diálogo](assets/leaderboard-dialog.png)

* [Configuración de título y dirección URL](#title-and-url-settings)

* **Mostrar distintivo**

   Si se selecciona, se incluye una columna para los iconos de distintivo en la tabla de clasificación.
El valor predeterminado no está seleccionado.

* **Mostrar nombre del distintivo**

   Si se selecciona, se incluye una columna para el nombre del distintivo en la tabla de clasificación.
El valor predeterminado no está seleccionado.

* **Mostrar avatar**

   Si se selecciona, la imagen de avatar del miembro se incluye en la tabla de clasificación, junto al vínculo de nombre del perfil del miembro.
El valor predeterminado no está seleccionado.

### Función Página {#page-function}

La función de página agrega una página en blanco al sitio de la comunidad que está conectada a las características del sitio de la comunidad: inicio de sesión, menú, notificaciones, mensajes, temas y marca. El contenido se agrega a la página mediante el [modo de creación de AEM estándar](/help/sites-authoring/editing-content.md).

Cuando se agrega a una plantilla, la única configuración es para [Configuración de título y URL](#title-and-url-settings).

### Función Preguntas y respuestas {#qna-function}

La función QnA es una página con un [componente QnA](/help/communities/working-with-qna.md) configurado para el etiquetado, la carga de archivos, el seguimiento y los miembros para la autoedición, la votación y la moderación.

Cuando se agrega a una plantilla, la configuración permite la restricción a los miembros privilegiados:

![qna-dialog](assets/qna-dialog.png)

* [Configuración de título y dirección URL](#title-and-url-settings)

* **Permitir fijación**

   Si se selecciona, el foro permite que las respuestas al tema se fijen al principio de la lista de comentarios. Predeterminado está seleccionado.

* **Permitir miembros privilegiados**

   Si se selecciona, el foro QnA solo permite que los miembros privilegiados publiquen preguntas, permitiendo la selección de un [grupo de miembros privilegiados](/help/communities/users.md#privileged-members-group). Si no se selecciona, todos los miembros de la comunidad pueden publicar. El valor predeterminado no está seleccionado.

* **Permitir cargas de archivos**

   Si se selecciona, el foro QnA incluye la posibilidad de que los miembros carguen archivos. Predeterminado está seleccionado.

* **Permitir respuestas de debate**

   Si no se selecciona, el foro QnA permite comentarios (respuestas) a una pregunta publicada, pero no se permiten respuestas a las respuestas. Predeterminado está seleccionado.

* **Permitir contenido destacado**

   Si se selecciona, su contenido se identifica como [contenido destacado](/help/communities/featured.md). Predeterminado está seleccionado.

## Crear función de la comunidad {#create-community-function}

La capacidad de crear una función de comunidad se alcanza seleccionando el icono `Create Community Function` situado en la parte superior de la consola de funciones de comunidad. Se pueden crear varias funciones basadas en el mismo modelo de AEM y, a continuación, personalizarlas de forma única abriéndolas en el modo de edición de autor.

![create-community-function](assets/create-community-function.png)

### Nombre de función de la comunidad {#community-function-name}

![function-name](assets/function-name.png)

En el panel Nombre de función de comunidad, se configuran un nombre, una descripción y si la función está habilitada o deshabilitada:

* **Nombre de función de la comunidad**

   El nombre de la función que se utiliza para mostrar y almacenamiento.

* **Descripción de la función de la comunidad**

   La descripción de la función para mostrar.

* **Deshabilitado/Habilitado**

   Un conmutador que controla si se puede hacer referencia a la función.

### Modelo AEM {#aem-blueprint}

![aem-blueprint](assets/aem-blueprint.png)

En el panel `AEM Blueprint`, es posible seleccionar el modelo que es la implementación subyacente de la función de comunidad.

La función de comunidad es un minisitio que incluye una o más páginas, preprogramadas para su inclusión en un sitio de la comunidad, incluyendo inicio de sesión, perfiles de usuario, notificaciones, mensajes, menú del sitio, búsqueda, tema y características de marca. Una vez creada la función, es posible [abrir la función](#open-community-function) en modo de edición de autor y personalizar la configuración de la página o del componente.

Dado que la función de comunidad se implementa como [Live Copy](/help/sites-administering/msm.md#live-copies) de un [modelo](/help/sites-administering/msm-livecopy.md#creatingablueprint), es posible implementar los cambios realizados en una función que afecta a todas las páginas del sitio de comunidad creadas a partir de la [plantilla del sitio de comunidad](/help/communities/sites.md) o [plantilla de grupo de comunidad](/help/communities/tools-groups.md) que incluye la función. También es posible desasociar una página de su modelo principal para realizar modificaciones a nivel de página.

Consulte también [Administrador de múltiples sitios](/help/sites-administering/msm.md).

### Miniatura    {#thumbnail}

![funtion-thumbnail](assets/funtion-thumbnail.png)

En el panel Miniatura, se puede cargar una imagen para mostrarla en la [consola de funciones de comunidad](#community-functions-console).

## Abrir función de la comunidad {#open-community-function}

![open-function](assets/open-function.png)

Seleccione el icono `Open Community Function` para acceder al modo de edición del autor y crear el contenido de la página y modificar la configuración de los componentes de la función.

### Configurar componentes {#configuring-components}

Una función de comunidad se implementa como Live Copy de un modelo de AEM, cuyos detalles se documentan en [Multi Site Manager](/help/sites-administering/msm.md).

Es posible no sólo crear contenido de página, sino también configurar componentes.

Si configura un componente en una página de un sitio de comunidad creado, puede que sea necesario cancelar [herencia](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) para configurar el componente. La herencia debe restablecerse cuando se complete la configuración.

Para obtener más información sobre la configuración, visite [Communities Components](/help/communities/author-communities.md) para autores.

## Editar función de la comunidad {#edit-community-function}

![edit-function](assets/edit-function.png)

Seleccione el icono `Edit Community Function` para editar las propiedades de la función utilizando los mismos paneles que [para crear una función de comunidad](#create-community-function), incluyendo habilitar o deshabilitar la función.
