---
title: Creación
seo-title: Authoring
description: Conceptos sobre la creación de contenido en AEM
seo-description: Concepts of authoring in AEM
uuid: eaa5f613-a138-4215-8f84-dfc962fe7fa7
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 81ff6f6f-11b3-4f8e-80e6-b3e104158394
docset: aem65
exl-id: dcda537a-1bb2-4ce3-9904-40d158b47556
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 25%

---

# Creación  {#authoring}

## Concepto de creación (y publicación) {#concept-of-authoring-and-publishing}

AEM La aplicación le proporciona dos entornos:

* Autor
* Publicación

Interactúan para permitirle ofrecer contenido en su sitio web, de modo que los visitantes puedan leerlo.

El entorno de creación proporciona los mecanismos para crear, actualizar y revisar este contenido antes de publicarlo:

* Un autor crea y revisa el contenido (que puede ser de varios tipos; por ejemplo, páginas, recursos, publicaciones, etc.)
* que, en algún momento, se publicará en su sitio web.

![chlimage_1-132](assets/chlimage_1-132.png)

AEM En el entorno de creación, la funcionalidad de la creación de informes está disponible a través de dos IU de. Desde el entorno de publicación se diseña todo el aspecto y funcionamiento de la interfaz de usuario.

### Entorno de creación {#author-environment}

El creador trabaja en lo que se conoce como **entorno de creación**. Esto proporciona una interfaz fácil de usar (interfaz gráfica de usuario (GUI o IU)) para crear el contenido. Normalmente se encuentra detrás del cortafuegos de una empresa que proporciona protección total y requiere que el autor inicie sesión con una cuenta a la que se le han asignado los derechos de acceso correspondientes.

>[!NOTE]
>
>Su cuenta necesita los derechos de acceso adecuados para crear, editar o publicar contenido.

Según la configuración de su instancia y de sus derechos de acceso personales, puede realizar muchas tareas en su contenido, entre otras:

* generar contenido nuevo o editar contenido existente en una página
* usar plantillas predefinidas para crear páginas de contenido nuevo
* crear, editar y administrar sus recursos y colecciones
* crear, editar y administrar sus publicaciones
* desarrolle sus campañas y los recursos relacionados
* desarrollar y administrar sitios de la comunidad
* mover, copiar o eliminar páginas de contenido, recursos, etc
* publicar (o cancelar la publicación) de páginas, recursos, etc

Asimismo, hay tareas administrativas que le ayudan a administrar su contenido:

* flujos de trabajo que controlan cómo se administran los cambios; por ejemplo. aplicación de una revisión antes de la publicación
* proyectos que coordinan tareas individuales

>[!NOTE]
>
>AEM también está en la [administrado](/help/sites-administering/home.md) (para la mayoría de las tareas) del entorno de creación.

#### Entorno de publicación {#publish-environment}

AEM Cuando esté listo, el contenido del sitio de la se publica en el **entorno de publicación**. Aquí las páginas del sitio web se ponen a disposición de la audiencia objetivo de acuerdo con la apariencia de la interfaz diseñada.

Por lo general, el entorno de publicación se encuentra dentro de la zona desmilitarizada; es decir, disponible para Internet, pero ya no bajo la plena protección de la red interna.

AEM Cuando el sitio de la es un [sitio comunitario](/help/communities/overview.md), o incluye [Componentes de Communities](/help/communities/author-communities.md), los visitantes (miembros) del sitio que hayan iniciado sesión pueden interactuar con las funciones de las Comunidades. Por ejemplo, pueden publicar en un foro, publicar un comentario o seguir a otros miembros. A los miembros se les puede conceder permiso para realizar actividades que normalmente se limitan al entorno de creación, como crear páginas nuevas (grupos de la comunidad), artículos de blogs y moderar las publicaciones de otros miembros.

>[!NOTE]
>
>Lamentablemente, a veces se produce una superposición en la terminología utilizada. Esto puede ocurrir con:
>
>* **Publicar o cancelar la publicación**
   >  Estos son los términos principales de las acciones que harán que el contenido esté disponible o no para los visitantes en su entorno de publicación.
>
>* **Activar o desactivar**
   >  Estos términos son sinónimos de publicar y cancelar la publicación.
>
>* **Replicar o replicación**
   >  Son los términos técnicos utilizados para indicar el movimiento de datos (p. ej., contenido de página, archivos, código, comentarios del usuario) de un entorno a otro; es decir, al publicar o replicar de forma inversa los comentarios del usuario.
>


#### Dispatcher {#dispatcher}

A fin de optimizar el rendimiento para los usuarios que visiten su sitio web, **[Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) implementa almacenamiento en caché y equilibrio de carga.**
