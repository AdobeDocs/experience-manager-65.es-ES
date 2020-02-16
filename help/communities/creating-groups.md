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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Grupos de la comunidad{#community-groups}

La función de grupos de comunidad es la capacidad para que una subcomunidad sea creada dinámicamente dentro de un sitio de comunidad por usuarios autorizados (miembros de la comunidad y autores) desde los entornos de publicación y creación.

Esta capacidad está presente cuando la función [de](/help/communities/functions.md#groups-function) grupos está presente en la estructura del sitio [de la](/help/communities/sites-console.md) comunidad.

Una plantilla [de grupo de](/help/communities/tools-groups.md) comunidad proporciona el diseño de la página de grupo de comunidad cuando se crea dinámicamente un grupo de comunidad.

Se seleccionan una o varias plantillas de grupo para la función de grupo cuando la función se agrega a la estructura de un sitio de comunidad o a una plantilla de sitio de comunidad. Esta lista de plantillas de grupo se presenta al miembro o autor que crea dinámicamente un nuevo grupo desde el sitio de la comunidad.

## Creación de un nuevo grupo {#creating-a-new-group}

La capacidad de crear un nuevo grupo de comunidad depende de la existencia de un sitio de comunidad que incluya la función de grupos, como uno creado a partir del ` [Reference Site Template](/help/communities/sites.md)`.

Los ejemplos que siguen utilizan el sitio de comunidad creado a partir del `Reference Site Template` informe, tal como se describe en el tutorial [Introducción a las comunidades](/help/communities/getting-started.md) de AEM.

Esta es la página que se carga al publicar cuando se selecciona el elemento de menú **Groups **menu:

![chlimage_1-85](assets/chlimage_1-85.png)

Al seleccionar el icono **Nuevo grupo** , se abre un cuadro de diálogo de edición.

En la ficha **Configuración **, se proporcionan las funciones básicas del grupo:

![chlimage_1-86](assets/chlimage_1-86.png)

* **Nombre** del grupo El título del grupo que se mostrará en el sitio de la comunidad.

* **Descripción** Una descripción del grupo que se mostrará en el sitio de la comunidad.

* **Invitar** una lista de miembros para invitar a unirse al grupo. La búsqueda de tipo por adelantado proporcionará sugerencias de los miembros de la comunidad que invitar.

* **Nombre** de la dirección URL del grupo El nombre de la página del grupo que forma parte de la dirección URL.

* **Abrir grupo** Al seleccionar `Open Group` se indica que cualquier visitante anónimo del sitio puede ver el contenido y se anula la selección `Member Only Group`.

* **La opción Grupo** de solo miembros `Member Only Group` indica que solo los miembros del grupo pueden ver el contenido y se anula la selección `Open Group`.

En la **Plantilla **ficha es la capacidad de seleccionar de la lista de plantillas de grupo de comunidad que se especificaron cuando la función de grupo se incluyó en la estructura del sitio de comunidad o en una plantilla de sitio de comunidad.

![chlimage_1-87](assets/chlimage_1-87.png)

En la **Imagen **ficha se muestra la capacidad de cargar una imagen para que se muestre en el grupo en la página Grupos del sitio de la comunidad. La hoja de estilo predeterminada ajustará el tamaño de la imagen a 170 x 90 píxeles.

![chlimage_1-88](assets/chlimage_1-88.png)

Al seleccionar el botón **Crear grupo** , las páginas del grupo se crean en función de la plantilla elegida, se crea un grupo de usuarios para la pertenencia y se actualiza la página Grupos para mostrar la nueva subcomunidad.

Por ejemplo, la página Grupos con una nueva subcomunidad titulada &quot;Grupo de enfoque&quot;, para la que se cargó una miniatura de imagen, aparecerá de la siguiente manera (aún con la sesión iniciada como administrador de grupos de la comunidad):

![chlimage_1-89](assets/chlimage_1-89.png)

Al seleccionar el `Focus Group` vínculo, se abrirá la página Grupo de enfoque en el explorador, que tiene un aspecto inicial basado en la plantilla seleccionada e incluye un submenú debajo del menú del sitio de la comunidad principal:

![chlimage_1-90](assets/chlimage_1-90.png)

### Community Group Member List Component {#community-group-member-list-component}

El `Community Group Member List` componente está diseñado para que lo utilicen los desarrolladores de plantillas de grupo.

### Información adicional {#additional-information}

Puede encontrar más información en la página [Community Group Essentials](/help/communities/essentials-groups.md) para desarrolladores.

Para obtener más información relacionada con los grupos de comunidad, visite [Administración de usuarios y grupos](/help/communities/users.md)de usuarios.
