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

Esta capacidad está presente cuando la [función de grupos](/help/communities/functions.md#groups-function) está presente en la estructura [sitio de comunidad](/help/communities/sites-console.md).

Una [plantilla de grupo de comunidad](/help/communities/tools-groups.md) proporciona el diseño de la página de grupo de comunidad cuando se crea dinámicamente un grupo de comunidad.

Se seleccionan una o varias plantillas de grupo para la función de grupo cuando la función se agrega a la estructura de un sitio de comunidad o a una plantilla de sitio de comunidad. Esta lista de plantillas de grupo se presenta al miembro o autor que crea dinámicamente un nuevo grupo desde el sitio de la comunidad.

## Creación de un nuevo grupo {#creating-a-new-group}

La capacidad de crear un nuevo grupo de comunidad depende de la existencia de un sitio de comunidad que incluya la función de grupos, como uno creado a partir de la [Plantilla del sitio de referencia](/help/communities/sites.md).

Los ejemplos que siguen utilizan el sitio de comunidad creado a partir del `Reference Site Template` como se describe en el tutorial [Introducción a AEM Communities](/help/communities/getting-started.md).

Esta es la página que se carga al publicar cuando se selecciona el elemento de menú **Grupos**:

![new-group](assets/new-group.png)

Al seleccionar el icono **Nuevo grupo**, se abre un cuadro de diálogo de edición.

En la ficha **Configuración**, se proporcionan las características básicas del grupo:

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

   Al seleccionar `Open Group` se indica que cualquier visitante anónimo del sitio puede vista del contenido y se anula la selección de `Member Only Group`.

* **Grupo de solo miembros**

   Si selecciona `Member Only Group`, solo los miembros del grupo pueden vista del contenido y se anula la selección de `Open Group`.

En la ficha **Plantilla** se encuentra la capacidad de
seleccione entre la lista de las plantillas de grupo de comunidad que se especificaron cuando la función de grupo se incluyó en la estructura del sitio de comunidad o en una plantilla de sitio de comunidad.

![group-template](assets/group-template.png)

En la ficha **Imagen** se encuentra la capacidad de cargar una imagen para que se muestre para el grupo en la página Grupos del sitio de la comunidad. La hoja de estilo predeterminada ajustará el tamaño de la imagen a 170 x 90 píxeles.

![group-image](assets/group-image.png)

Al seleccionar el botón **Crear grupo**, las páginas para el grupo se crean en función de la plantilla elegida y se crea un grupo de usuarios para la pertenencia y la página Grupos se actualiza para mostrar la nueva subcomunidad.

Por ejemplo, la página Grupos con una nueva subcomunidad titulada &quot;Grupo de enfoque&quot;, para la que se cargó una miniatura de imagen, aparecerá de la siguiente manera (aún con la sesión iniciada como administrador de grupos de la comunidad):

![group-page](assets/group-page.png)

Al seleccionar el vínculo `Focus Group` se abrirá la página Grupo de enfoque en el explorador, que tiene una apariencia inicial basada en la plantilla seleccionada e incluye un submenú debajo del menú del sitio de la comunidad principal:

![open-group-page](assets/open-group-page.png)

### Componente de Lista de miembros del grupo de la comunidad {#community-group-member-list-component}

El componente `Community Group Member List` está diseñado para ser utilizado por desarrolladores de plantillas de grupo.

### Información adicional {#additional-information}

Puede encontrar más información en la página [Community Group Essentials](/help/communities/essentials-groups.md) para desarrolladores.

Para obtener más información relacionada con los grupos de comunidad, visite [Administración de usuarios y grupos de usuarios](/help/communities/users.md).
