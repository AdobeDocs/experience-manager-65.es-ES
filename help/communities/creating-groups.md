---
title: Grupos de la comunidad
description: Descubra cómo la función de grupos de comunidad permite crear dinámicamente una subcomunidad dentro de un sitio de comunidad mediante usuarios autorizados en Publish y Author.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# Grupos de la comunidad {#community-groups}

La función de grupos de comunidad permite que usuarios autorizados (miembros y autores de la comunidad) creen dinámicamente una subcomunidad en un sitio de comunidad desde los entornos de publicación y creación.

Esta capacidad está presente cuando la función [grupos](/help/communities/functions.md#groups-function) está presente en la estructura del [sitio de la comunidad](/help/communities/sites-console.md).

Una [plantilla de grupo de comunidad](/help/communities/tools-groups.md) proporciona el diseño de la página de grupo de comunidad cuando se crea dinámicamente un grupo de comunidad.

Se seleccionan una o más plantillas de grupo para la función de grupos cuando la función se agrega a la estructura de un sitio de comunidad o a una plantilla de sitio de comunidad. Esta lista de plantillas de grupo se presenta al miembro o autor que crea dinámicamente un grupo desde el sitio de la comunidad.

## Creación de un nuevo grupo {#creating-a-new-group}

La capacidad para crear un grupo de comunidad depende de la existencia de un sitio de comunidad que incluya la función de grupos, como uno creado a partir de la [Plantilla de sitio de referencia](/help/communities/sites.md).

Los ejemplos siguientes utilizan el sitio de la comunidad creado a partir de `Reference Site Template` tal como se describe en el tutorial de [Introducción a AEM Communities](/help/communities/getting-started.md).

Esta es la página que se carga al publicar cuando se selecciona el elemento de menú **Grupos**:

![nuevo-grupo](assets/new-group.png)

Al seleccionar el icono **Nuevo grupo**, se abre un cuadro de diálogo de edición.

En la ficha **Configuración**, proporciona las características básicas del grupo:

![configuración de grupo](assets/group-settings.png)

* **Nombre de grupo**

  El título del grupo que desea mostrar en el sitio de la comunidad. Evite utilizar caracteres de subrayado (_) y palabras clave como recursos y configuración en el nombre del grupo.

* **Descripción**

  Descripción del grupo que se mostrará en el sitio de la comunidad.

* **Invitar**

  Una lista de miembros a los que invitar al grupo. La búsqueda de escritura anticipada proporciona sugerencias de miembros de la comunidad para invitar.

* **Nombre de URL del grupo**

  Nombre de la página del grupo que forma parte de la dirección URL.

* **Abrir grupo**

  Seleccionar `Open Group` indica que cualquier visitante anónimo del sitio puede ver el contenido y anula la selección de `Member Only Group`.

* **Grupo de solo miembros**

  Seleccionar `Member Only Group` indica que solamente los miembros del grupo pueden ver el contenido y anula la selección de `Open Group`.

En la ficha **Plantilla**, puede seleccionar de la lista de plantillas de grupo de la comunidad. Estas plantillas se especificaron cuando la función de grupos se incluía en la estructura del sitio de la comunidad o en una plantilla de sitio de la comunidad.

![plantilla-grupo](assets/group-template.png)

En la ficha **Imagen**, puede cargar una imagen para mostrar para el grupo en la página Grupos del sitio de la comunidad. La hoja de estilos predeterminada ajusta el tamaño de la imagen a 170 x 90 píxeles.

![imagen de grupo](assets/group-image.png)

Al seleccionar **Crear grupo**, las páginas del grupo se crean según la plantilla elegida, se crea un grupo de usuarios para la pertenencia y la página Grupos se actualiza para mostrar la nueva subcomunidad.

Por ejemplo, la página Grupos con una nueva subcomunidad titulada &quot;Grupo de enfoque&quot;, para la que se ha cargado una miniatura de imagen, aparece de la siguiente manera (con sesión iniciada como administrador del grupo de comunidad):

![página-grupo](assets/group-page.png)

Al seleccionar el vínculo `Focus Group`, se abre la página Grupo de enfoque en el explorador, que tiene una apariencia inicial basada en la plantilla seleccionada e incluye un submenú debajo del menú del sitio principal de la comunidad:

![página-grupo-abierta](assets/open-group-page.png)

### Componente de lista de miembros del grupo de comunidad {#community-group-member-list-component}

El componente `Community Group Member List` está diseñado para que lo utilicen los desarrolladores de plantillas de grupo.

### Información adicional {#additional-information}

Encontrará más información en la página de [Community Group Essentials](/help/communities/essentials-groups.md) para desarrolladores.

Para obtener más información relacionada con los grupos de la comunidad, visite [Administración de usuarios y grupos de usuarios](/help/communities/users.md).
