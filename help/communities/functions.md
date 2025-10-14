---
title: Funciones de la comunidad
description: Obtenga información sobre cómo acceder a la consola de funciones de la comunidad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 2395c895-c611-43ac-abb6-c2bc4b4a41f4
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2215'
ht-degree: 2%

---

# Funciones de la comunidad{#community-functions}

El tipo de funciones que se esperan de una experiencia de comunidad son bien conocidas. Las funciones de la comunidad están disponibles como funciones de la comunidad. Básicamente, son una o más páginas precableadas para implementar una función de la comunidad, lo que requiere algo más que simplemente agregar un componente a una página en modo de autor. Son los componentes básicos utilizados para definir la estructura de una [plantilla del sitio de la comunidad](/help/communities/sites.md) a partir de la cual se [crean](/help/communities/sites-console.md) los sitios de la comunidad.

AEM Una vez creado un sitio de la comunidad, se puede agregar contenido a las páginas resultantes utilizando el [modo de creación estándar de la &#x200B;](/help/sites-authoring/editing-content.md). Hay varias funciones de la comunidad disponibles, tal como se ven en la consola de funciones de la comunidad.

>[!NOTE]
>
>Las consolas para la creación de [sitios de la comunidad](/help/communities/sites-console.md), [plantillas de sitios de la comunidad](/help/communities/sites.md), [plantillas de grupos de la comunidad](/help/communities/tools-groups.md) y [funciones de la comunidad](/help/communities/functions.md) solo se pueden usar en el entorno de creación.

## Consola de funciones de comunidad {#community-functions-console}

Para llegar a la consola de funciones de la comunidad en el entorno de creación:

* Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Funciones de la comunidad]**.

![funciones de la comunidad](assets/community-functions.png)

## Funciones creadas previamente {#pre-built-functions}

A continuación se muestra una breve descripción de las funciones que se proporcionan con AEM Communities. AEM Cada función incluye una o más páginas que contienen componentes de comunidades conectados entre sí en una característica que se incorpora fácilmente a una [plantilla de sitio de comunidad](/help/communities/sites.md).

Una plantilla de sitio de comunidad proporciona la estructura para un sitio de comunidad, incluidos el inicio de sesión, los perfiles de usuario, las notificaciones, los mensajes, el menú del sitio, la búsqueda, el tema y las funciones de promoción de la marca.

### Configuración de título y URL {#title-and-url-settings}

**Title** y **URL** son propiedades comunes a todas las funciones de la comunidad.

Cuando se agrega una función de comunidad a una plantilla de sitio de comunidad o se agrega al [modificar](/help/communities/sites-console.md#modifying-site-properties) la estructura de un sitio de comunidad, se abre el cuadro de diálogo de la función para que se puedan configurar el Título y la URL.

#### Detalles de la función de configuración {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **Título**

  (*Requerido*) El texto que aparece en el menú de características del sitio

* **URL**

  (*Obligatorio*) El nombre usado para generar el URI. AEM El nombre debe cumplir con las [convenciones de nomenclatura](/help/sites-developing/naming-conventions.md) impuestas por el JCR y el servicio de nombres de la red de nombres de la red (JCR) y el servicio de nombres de la red.

Por ejemplo, si usa el sitio creado a partir de seguir el tutorial [Introducción](/help/communities/getting-started.md),

* Título = Página web
* URL = página

A continuación, la dirección URL de la página es https://localhost:4503/content/sites/engage/en/page.html

y el vínculo de menú de la página aparece de la siguiente manera:

![página de participación](assets/engage-page.png)

### Función Secuencia de actividades {#activity-stream-function}

La función de flujo de actividad es una página con un [componente de flujos de actividad](/help/communities/activities.md) con todas las vistas seleccionadas (todas las actividades, actividades de usuario y siguientes). Consulte también [Activity Stream Essentials](/help/communities/essentials-activities.md) para desarrolladores.

Cuando se añade a una plantilla, se abre el siguiente cuadro de diálogo:

#### Detalles de la función de configuración {#configuration-function-details-1}

![detalles de función](assets/function-details.png)

* [Configuración de título y URL](#title-and-url-settings)

* **Mostrar vista de &quot;Mis actividades&quot;**

  Si se selecciona, la página Actividades incluye una pestaña que filtra las actividades en función de las que genera el miembro actual dentro de la comunidad. La opción predeterminada está seleccionada.

* **Mostrar vista de &quot;todas las actividades&quot;**

  Si se selecciona, la página Actividades incluye una pestaña que incluye todas las actividades generadas dentro de la comunidad a la que tiene acceso el miembro actual. La opción predeterminada está seleccionada.

* **Mostrar vista de &quot;Fuente de noticias&quot;**

  Si se selecciona, las páginas Actividades incluyen una pestaña que filtra las actividades en función de las que sigue el miembro actual. La opción predeterminada está seleccionada.

### Función Blog {#blog-function}

La función de blog es una página con un [componente de blog](/help/communities/blog-feature.md) configurado para el etiquetado, las cargas de archivos, el seguimiento, los miembros para la autoedición, la votación y la moderación. Consulte también [Blog Essentials](/help/communities/blog-developer-basics.md) para desarrolladores.

Cuando se añade a una plantilla, se abre el siguiente cuadro de diálogo:

![componente de blog](assets/blog-component.png)

* [Configuración de título y URL](#title-and-url-settings)

* **Permitir miembros privilegiados**

  Si se selecciona, el blog solo permite que los miembros privilegiados creen artículos al permitir la selección de un [grupo de miembros privilegiados](/help/communities/users.md#privileged-members-group). Si no se selecciona, se permite crear a todos los miembros de la comunidad. La opción predeterminada no está seleccionada.

* **Permitir cargas de archivos**

  Si se selecciona, el blog incluye la capacidad para que los miembros carguen archivos. La opción predeterminada está seleccionada.

* **Permitir respuestas de subprocesos**

  Si no está seleccionado, el blog permite las respuestas (comentarios) a un artículo, pero no las respuestas a los comentarios. La opción predeterminada está seleccionada.

* **Permitir contenido destacado**

  Si se selecciona, el blog se identifica como [contenido destacado](/help/communities/featured.md). La opción predeterminada está seleccionada.

### Función Calendario {#calendar-function}

La función de calendario es una página con un [componente de calendario](/help/communities/calendar.md) configurado para permitir el etiquetado. Consulte también [Calendar Essentials](/help/communities/calendar-basics-for-developers.md) para desarrolladores.

Cuando se añade a una plantilla, se abre el siguiente cuadro de diálogo:

![detalles-calendario](assets/calendar-details.png)

* [Configuración de título y URL](#title-and-url-settings)

* **Permitir anclaje**

  Si se selecciona, el foro permite anclar las respuestas del tema al principio de la lista de comentarios. La opción predeterminada está seleccionada.

* **Permitir miembros privilegiados**

  Si se selecciona, el blog solo permite que los miembros privilegiados creen artículos al permitir la selección de un [grupo de miembros privilegiados](/help/communities/users.md#privileged-members-group). Si no se selecciona, se permite crear a todos los miembros de la comunidad. La opción predeterminada no está seleccionada.

* **Permitir cargas de archivos**

  Si se selecciona, el blog incluye la capacidad para que los miembros carguen archivos. La opción predeterminada está seleccionada.

* **Permitir respuestas de subprocesos**

  Si no está seleccionado, el blog permite las respuestas (comentarios) a un artículo, pero no las respuestas a los comentarios. La opción predeterminada está seleccionada.

* **Permitir contenido destacado**

  Si se selecciona, su contenido se identifica como [contenido destacado](/help/communities/featured.md). La opción predeterminada está seleccionada.

### Función Contenido destacado {#featured-content-function}

La función de contenido destacado es una página con un [componente Contenido destacado](/help/communities/featured.md) configurado para permitir que se agreguen y eliminen comentarios.

Se puede permitir o no la capacidad de incluir contenido por componente (consulte [Función Blog](#blog-function), [Función Calendario](#calendar-function), [Función Foro](#forum-function), [Función Ideación](#ideation-function) y [Función QnA](#qna-function)).

Cuando se agrega a una plantilla, la única configuración es para [Configuración de título y dirección URL](#title-and-url-settings).

### Función Biblioteca del archivo {#file-library-function}

La función de biblioteca de archivos es una página con un [componente de biblioteca de archivos](/help/communities/file-library.md) configurado para permitir que se agreguen y eliminen comentarios.

Cuando se agrega a una plantilla, la única configuración es para [Configuración de título y dirección URL](#title-and-url-settings).

### Función Foro {#forum-function}

La función de foro es una página con un [componente de foro](/help/communities/forum.md) configurado para el etiquetado, las cargas de archivos, el seguimiento, los miembros para la autoedición, la votación y la moderación.

Cuando se añade a una plantilla, se abre el siguiente cuadro de diálogo:

#### Detalles de la función de configuración {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [Configuración de título y URL](#title-and-url-settings)

* **Permitir anclaje**

  Si se selecciona, el foro permite anclar las respuestas del tema al principio de la lista de comentarios. La opción predeterminada está seleccionada.

* **Permitir miembros privilegiados**

  Si se selecciona, el foro solo permite que los miembros privilegiados publiquen temas al permitir la selección de un [grupo de miembros privilegiados](/help/communities/users.md#privileged-members-group). Si no se selecciona, todos los miembros de la comunidad pueden publicar. La opción predeterminada no está seleccionada.

* **Permitir cargas de archivos**

  Si se selecciona, el foro incluye la capacidad para que los miembros carguen archivos. La opción predeterminada está seleccionada.

* **Permitir respuestas de subprocesos**

  Si no está seleccionado, el foro permite comentarios sobre un tema, pero no se permiten las respuestas a esos comentarios. La opción predeterminada está seleccionada.

* **Permitir contenido destacado**

  Si se selecciona, el contenido del componente se identifica como [contenido destacado](/help/communities/featured.md). La opción predeterminada está seleccionada.

### Función Grupos {#groups-function}

>[!CAUTION]
>
>La función de grupos debe *no* ser la función *primero ni la única* en la estructura de un sitio o en una plantilla de sitio de la comunidad.
>
>Cualquier otra función, como [page function](#page-function), debe incluirse y enumerarse primero.

La función de grupos permite a los miembros de la comunidad crear subcomunidades dentro del sitio de la comunidad en el entorno de publicación.

Según la configuración [settings](/help/communities/sites-console.md#groupmanagement), cuando la función Groups se incluya en una [plantilla de sitio de comunidad](/help/communities/sites.md), los grupos pueden ser públicos o privados y se pueden configurar una o más plantillas de grupo de comunidad para proporcionar una selección de plantillas cuando se cree realmente el grupo de comunidad (por ejemplo, desde el entorno de publicación). Una [plantilla de grupo de comunidad](/help/communities/tools-groups.md) especifica qué características de Communities se crean para las páginas de grupo, como foros y calendarios.

Cuando se crea un grupo de comunidad, se crea dinámicamente un grupo de miembros para el nuevo grupo, al que se pueden asignar o unir miembros. Para obtener más información, consulte [Administración de usuarios y grupos de usuarios](/help/communities/users.md).

A partir del paquete de funciones 1[&#128279;](/help/communities/deploy-communities.md#latestfeaturepack) de las comunidades se crean grupos de comunidades en el entorno de creación mediante la consola de grupos de [sitios de comunidades](/help/communities/groups.md), y se pueden crear en el entorno de publicación cuando está habilitada.

Cuando se añade a una plantilla, se abre el siguiente cuadro de diálogo:

![group-template-config](assets/group-template-config.png)

* [Configuración de título y URL](#title-and-url-settings)

* **Seleccionar plantillas de grupo**

  Lista desplegable que permite seleccionar una o más plantillas de grupo habilitadas entre las que puede elegir el futuro creador de un nuevo grupo de comunidad (en el entorno de publicación).

* **Permitir miembros privilegiados**

  Si se selecciona, el foro solo permite que los miembros privilegiados publiquen temas al permitir la selección de un [grupo de seguridad de miembros privilegiados](/help/communities/users.md#privileged-members-group). Si no se selecciona, todos los miembros de la comunidad pueden publicar. La opción predeterminada no está seleccionada.

* **Permitir la creación de Publish**

  Si se selecciona, los miembros de la comunidad autorizados pueden crear un grupo en el entorno de publicación. Si no se selecciona, los nuevos grupos (subcomunidades) solo se pueden crear en el entorno de creación desde la consola Grupos de sitios de comunidades.
La opción predeterminada está seleccionada.

### Función ideación {#ideation-function}

La función ideation es una página con un [componente ideation](/help/communities/ideation-feature.md).

Cuando se agrega a una plantilla, se abre el siguiente cuadro de diálogo, que especifica los nombres predeterminados de Título y URL, y la configuración de visualización predeterminada para la plantilla:

![función de ideación](assets/ideation-function.png)

* [Configuración de título y URL](#title-and-url-settings)

* **Permitir miembros privilegiados**

  Si se selecciona, el foro solo permite que los miembros privilegiados publiquen temas al permitir la selección de un [grupo de seguridad de miembros privilegiados](/help/communities/users.md#privileged-members-group). Si no se selecciona, todos los miembros de la comunidad pueden publicar. La opción predeterminada no está seleccionada.

* **Permitir cargas de archivos**

  Si se selecciona, la idea incluye la capacidad para que los miembros carguen archivos. La opción predeterminada está seleccionada.

* **Permitir respuestas de subprocesos**

  Si no está seleccionada, la idea permite las respuestas (comentarios) a un tema, pero no las respuestas a comentarios. La opción predeterminada está seleccionada.

* **Permitir contenido destacado**

  Si se selecciona, su contenido se identifica como [contenido destacado](/help/communities/featured.md). La opción predeterminada está seleccionada.

### Función de la tabla de clasificación {#leaderboard-function}

La función de clasificación es una página con un [componente de tabla de clasificación](/help/communities/enabling-leaderboard.md).

**NOTA**: el componente Tabla de clasificación necesita una configuración adicional *después de*, se crea un sitio de comunidad a partir de una plantilla de comunidad que incluye la función Tabla de clasificación. Especifique las [reglas](/help/communities/enabling-leaderboard.md#rules-tab) del componente de la tabla de clasificación, que dependen de la configuración de [puntuación e insignias](/help/communities/implementing-scoring.md) para el sitio de la comunidad.

Cuando se agrega a una plantilla, se abre el siguiente cuadro de diálogo, que especifica los nombres predeterminados de Título y URL, y la configuración de visualización predeterminada para la plantilla:

![cuadro de diálogo de tabla de clasificación](assets/leaderboard-dialog.png)

* [Configuración de título y URL](#title-and-url-settings)

* **Mostrar distintivo**

  Si se selecciona, se incluye una columna para los iconos de distintivo en la tabla de clasificación.
La opción predeterminada no está seleccionada.

* **Mostrar nombre del distintivo**

  Si se selecciona, se incluye en la tabla de clasificación una columna para el nombre del distintivo.
La opción predeterminada no está seleccionada.

* **Mostrar avatar**

  Si se selecciona, la imagen de avatar del miembro se incluirá en la tabla de clasificación, junto al vínculo de su nombre a su perfil de miembro.
La opción predeterminada no está seleccionada.

### Función Página {#page-function}

La función de página agrega una página en blanco al sitio de la comunidad que está cableada con las funciones del sitio de la comunidad: inicio de sesión, menú, notificaciones, mensajería, temas y marca. AEM El contenido se agrega a la página usando el [modo de creación estándar de la](/help/sites-authoring/editing-content.md).

Cuando se agrega a una plantilla, la única configuración es para [Configuración de título y dirección URL](#title-and-url-settings).

### Función Preguntas y respuestas {#qna-function}

La función de control de calidad es una página con un [componente de control de calidad](/help/communities/working-with-qna.md) configurado para el etiquetado, las cargas de archivos, el seguimiento, los miembros para la autoedición, el voto y la moderación.

Cuando se agrega a una plantilla, la configuración permite la restricción a los miembros privilegiados:

![qna-dialog](assets/qna-dialog.png)

* [Configuración de título y URL](#title-and-url-settings)

* **Permitir anclaje**

  Si se selecciona, el foro permite anclar las respuestas del tema al principio de la lista de comentarios. La opción predeterminada está seleccionada.

* **Permitir miembros privilegiados**

  Si se selecciona, el foro de control de calidad solo permite a los miembros privilegiados publicar preguntas al permitir la selección de un [grupo de miembros privilegiados](/help/communities/users.md#privileged-members-group). Si no se selecciona, todos los miembros de la comunidad pueden publicar. La opción predeterminada no está seleccionada.

* **Permitir cargas de archivos**

  Si se selecciona, el foro de control de calidad incluye la capacidad para que los miembros carguen archivos. La opción predeterminada está seleccionada.

* **Permitir respuestas de subprocesos**

  Si no está seleccionado, el foro de control de calidad permite comentarios (respuestas) a una pregunta publicada, pero no se permiten respuestas a las respuestas. La opción predeterminada está seleccionada.

* **Permitir contenido destacado**

  Si se selecciona, su contenido se identifica como [contenido destacado](/help/communities/featured.md). La opción predeterminada está seleccionada.

## Crear función de la comunidad {#create-community-function}

Para crear una función de la comunidad, seleccione el icono `Create Community Function` que se encuentra en la parte superior de la consola Funciones de la comunidad. AEM Se pueden crear varias funciones basadas en el mismo modelo de creación y, a continuación, personalizarse de forma exclusiva abriéndose en el modo de edición de autor.

![create-community-function](assets/create-community-function.png)

### Nombre de función de la comunidad {#community-function-name}

![nombre-función](assets/function-name.png)

En el panel Nombre de función de la comunidad, se configura un nombre, una descripción y si la función está habilitada o deshabilitada:

* **Nombre de función de comunidad**

  El nombre de función utilizado para la visualización y el almacenamiento.

* **Descripción de función de la comunidad**

  Descripción de la función que se va a mostrar.

* **Deshabilitado/Habilitado**

  Conmutador que controla si la función es referenciable.

### Modelo AEM {#aem-blueprint}

![modelo aem](assets/aem-blueprint.png)

En el panel `AEM Blueprint`, se puede seleccionar el modelo que es la implementación subyacente de la función de la comunidad.

La función de comunidad es un minisitio que incluye una o más páginas preconfiguradas para su inclusión en un sitio de comunidad, incluidos el inicio de sesión, los perfiles de usuario, las notificaciones, los mensajes, el menú del sitio, la búsqueda, el establecimiento de temas y las funciones de marca. Una vez creada la función, es posible [abrir la función](#open-community-function) en el modo de edición de autor y personalizar la configuración de la página o el componente.

Dado que la función de comunidad se implementa como [Live Copy](/help/sites-administering/msm.md#live-copies) de un [modelo](/help/sites-administering/msm-livecopy.md#creatingablueprint), es posible desplegar los cambios realizados en una función que afecte a todas las páginas de sitios de la comunidad creadas a partir de la [plantilla de sitio de comunidad](/help/communities/sites.md) o la [plantilla de grupo de comunidad](/help/communities/tools-groups.md) que incluyeron la función. También es posible desasociar una página de su modelo principal para realizar modificaciones a nivel de página.

Consulte también [Administrador de varios sitios](/help/sites-administering/msm.md).

### Miniatura    {#thumbnail}

![miniatura de función](assets/funtion-thumbnail.png)

En el panel de miniaturas, se puede cargar una imagen para mostrarla en la [consola de funciones de la comunidad](#community-functions-console).

## Abrir función de la comunidad {#open-community-function}

![función abierta](assets/open-function.png)

Seleccione el icono `Open Community Function` para entrar al modo de edición de autor con el fin de crear el contenido de la página y modificar la configuración de los componentes de la función.

### Configuración de componentes {#configuring-components}

AEM Una función de comunidad se implementa como una Live Copy de un modelo de, cuyos detalles se documentan en [Administrador de varios sitios](/help/sites-administering/msm.md).

Es posible no solo crear contenido de página, sino también configurar componentes.

Si configura un componente en una página de un sitio de comunidad creado, puede ser necesario cancelar [inheritance](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) para configurar el componente. La herencia debe restablecerse cuando se complete la configuración.

Para obtener detalles de configuración, visite [Componentes de comunidades](/help/communities/author-communities.md) para autores.

## Editar función de la comunidad {#edit-community-function}

![editar-función](assets/edit-function.png)

Seleccione el icono `Edit Community Function` para editar las propiedades de la función con los mismos paneles que [creando una función de la comunidad](#create-community-function), incluida la activación o desactivación de la función.
