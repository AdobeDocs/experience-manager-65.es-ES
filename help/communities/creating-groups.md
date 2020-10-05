---
title: Grupos de la comunidad
seo-title: Grupos de la comunidad
description: Creación de grupos de comunidad
seo-description: Creación de grupos de comunidad
uuid: c677d23d-5edb-414c-9013-130c88c2ea52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d94708ee-ca6b-420c-9536-6889d752f9de
docset: aem65
translation-type: tm+mt
source-git-commit: 6337a57ea12f1e026f6c754a083307ce018a1c13
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 3%

---


# Grupos de la comunidad {#community-groups}

La función de grupos de comunidad es la capacidad para que una subcomunidad sea creada dinámicamente dentro de un sitio de comunidad por usuarios autorizados (miembros de la comunidad y autores) desde los entornos de publicación y creación.

Esta capacidad está presente cuando la función [de](/help/communities/functions.md#groups-function) grupos está presente en la estructura del sitio [de la](/help/communities/sites-console.md) comunidad.

Una plantilla [de grupo de](/help/communities/tools-groups.md) comunidad proporciona el diseño de la página de grupo de comunidad cuando se crea dinámicamente un grupo de comunidad.

Se seleccionan una o varias plantillas de grupo para la función de grupo cuando la función se agrega a la estructura de un sitio de comunidad o a una plantilla de sitio de comunidad. Esta lista de plantillas de grupo se presenta al miembro o autor que crea dinámicamente un nuevo grupo desde el sitio de la comunidad.

## Creating a New Group {#creating-a-new-group}

La capacidad de crear un nuevo grupo de comunidad depende de la existencia de un sitio de comunidad que incluya la función de grupos, como uno creado a partir de la plantilla [de sitio de](/help/communities/sites.md)referencia.

Los ejemplos que siguen utilizan el sitio de comunidad creado a partir de la página `Reference Site Template` tal como se describe en el tutorial [Introducción a AEM Communities](/help/communities/getting-started.md) .

Esta es la página que se carga al publicar cuando se selecciona el elemento de menú **Grupos** :

![new-group](assets/new-group.png)

Al seleccionar el icono **Nuevo grupo** , se abre un cuadro de diálogo de edición.

En la ficha **Configuración** , se proporcionan las funciones básicas del grupo:

![group-settings](assets/group-settings.png)

* **Nombre del grupo**

   Título del grupo que se mostrará en el sitio de la comunidad.

* **Descripción**

   Descripción del grupo que se va a mostrar en el sitio de la comunidad.

* **Invitar**

   Una lista de miembros para invitar a unirse al grupo. La búsqueda de tipo por adelantado proporcionará sugerencias de los miembros de la comunidad que invitar.

* **Nombre de URL del grupo**

   Nombre de la página de grupo que forma parte de la dirección URL.

* **Abrir grupo**

   Si selecciona `Open Group` se indica que cualquier visitante anónimo del sitio puede vista del contenido y se anula la selección `Member Only Group`.

* **Grupo de solo miembros**

   Si selecciona `Member Only Group` se indica que solo los miembros del grupo pueden vista del contenido y se anula la selección `Open Group`.

En la ficha **Plantilla** se encuentra la capacidad de seleccionar entre la lista de las plantillas de grupo de la comunidad que se especificaron cuando la función de grupo se incluyó en la estructura del sitio de la comunidad o en una plantilla de sitio de la comunidad.

![group-template](assets/group-template.png)

En la ficha **Imagen** se encuentra la posibilidad de cargar una imagen para que se muestre en el grupo en la página Grupos del sitio de la comunidad. La hoja de estilo predeterminada ajustará el tamaño de la imagen a 170 x 90 píxeles.

![group-image](assets/group-image.png)

Al seleccionar el botón **Crear grupo** , las páginas del grupo se crean en función de la plantilla elegida, se crea un grupo de usuarios para la pertenencia y se actualiza la página Grupos para mostrar la nueva subcomunidad.

Por ejemplo, la página Grupos con una nueva subcomunidad titulada &quot;Grupo de enfoque&quot;, para la que se cargó una miniatura de imagen, aparecerá de la siguiente manera (aún con la sesión iniciada como administrador de grupos de la comunidad):

![group-page](assets/group-page.png)

Al seleccionar el `Focus Group` vínculo, se abrirá la página Grupo de enfoque en el explorador, que tiene un aspecto inicial basado en la plantilla seleccionada e incluye un submenú debajo del menú del sitio de la comunidad principal:

![open-group-page](assets/open-group-page.png)

### Community Group Member List Component {#community-group-member-list-component}

El `Community Group Member List` componente está diseñado para que lo utilicen los desarrolladores de plantillas de grupo.

### Información adicional {#additional-information}

Puede encontrar más información en la página [Community Group Essentials](/help/communities/essentials-groups.md) para desarrolladores.

Para obtener más información relacionada con los grupos de comunidad, visite [Administración de usuarios y grupos](/help/communities/users.md)de usuarios.
