---
title: Creación
seo-title: Creación
description: Conceptos sobre la creación de contenido en AEM
seo-description: Conceptos sobre la creación de contenido en AEM
uuid: eaa5f613-a138-4215-8f84-dfc962fe7fa7
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 81ff6f6f-11b3-4f8e-80e6-b3e104158394
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# Creación{#authoring}

## Conceptos de creación (y publicación) {#concept-of-authoring-and-publishing}

AEM le ofrece dos entornos:

* Creación
* Publicación

Interactúan para permitirle ofrecer contenido en su sitio web para que los visitantes puedan leerlo.

El entorno de creación ofrece mecanismos para crear, actualizar y revisar el contenido antes de publicarlo:

* Un autor crea y revisa el contenido (que puede ser de varios tipos; por ejemplo, páginas, recursos, publicaciones, etc.)
* Este, en algún momento, se publicará en su sitio web.

![chlimage_1-132](assets/chlimage_1-132.png)

En el entorno de creación, las funciones de AEM están disponibles mediante dos IU. Desde el entorno de publicación se diseña todo el aspecto y funcionamiento de la interfaz de usuario.

>[!NOTE]
>
>AEM se utiliza para crear la documentación de AEM.
>
>Junto con el Dispatcher, se utiliza para la publicación.

### Entorno de creación {#author-environment}

The author works in what is known as the **author environment**. This provides an easy to use interface (graphical user interface (GUI or UI)) for creating the content. It is usually located behind a company&#39;s firewall that provides full protection and requires the author to login, using an account that has been assigned the appropriate access rights.

>[!NOTE]
>
>Su cuenta necesita tener los derechos de acceso correspondientes para crear, editar o publicar contenido.

Según la configuración de su instancia y sus derechos personales de acceso, puede realizar muchas tareas en el contenido, como (entre otras):

* generar contenido nuevo o editar contenido existente en una página
* utilizar plantillas predefinidas para crear páginas de contenido nuevo
* crear, editar y administrar sus recursos y colecciones
* crear, editar y administrar sus publicaciones
* desarrollar sus campañas y los medios relacionados
* desarrollar y administrar sitios de la comunidad
* mover, copiar o eliminar recursos, páginas de contenido, etc.
* publicar (o cancelar la publicación de) páginas, recursos, etc.

Asimismo, hay tareas administrativas que le ayudan a administrar su contenido:

* flujos de trabajo que controlan la administración de cambios; por ejemplo, implementar una revisión antes de la publicación
* proyectos que coordinan tareas individuales

>[!NOTE]
>
>AEM también se [administra](/help/sites-administering/home.md) (para una gran mayoría de tareas) desde el entorno de creación.

#### Entorno de publicación {#publish-environment}

When ready, the AEM site&#39;s content is published to the **publish environment**. Aquí las páginas del sitio web se ponen a disposición de la audiencia objetivo de acuerdo con la apariencia de la interfaz diseñada.

Normalmente, el entorno de publicación se encuentra dentro de la zona desmilitarizada, es decir, disponible para Internet, pero ya no bajo la protección completa de la red interna.

Cuando el sitio de AEM es un [sitio de la comunidad](/help/communities/overview.md) o incluye [componentes de Communities](/help/communities/author-communities.md), los visitantes del sitio que han iniciado sesión (miembros) pueden utilizar las funciones de Communities. Por ejemplo, pueden publicar en un foro, publicar un comentario o seguir a otros miembros. Los miembros pueden recibir permiso para realizar actividades habitualmente limitadas al entorno de creación, como crear páginas nuevas (grupos de la comunidad) y artículos de blog o moderar las publicaciones de otros miembros.

>[!NOTE]
>
>Por desgracia, a veces la terminología utilizada se superpone. Esto puede pasar con:
>
>* **Publicar / Cancelar la publicación**
   >  Estos son los términos principales para las acciones que hacen que el contenido esté disponible para el público en su entorno de publicación (o no).
   >
   >
* **Activar/Desactivar**
   >  Estos términos son sinónimos de Publicar/Cancelar la publicación.
   >
   >
* **Replicar / Replicación**
   >  Son los términos técnicos utilizados para indicar el movimiento de datos (por ejemplo, contenido de la página, archivos, código o comentarios del usuario) de un entorno a otro; es decir, al publicar o replicar a la inversa los comentarios de los usuarios.
>



#### Dispatcher {#dispatcher}

To optimize performance for visitors to your website, the **[dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)**implements load balancing and caching.
