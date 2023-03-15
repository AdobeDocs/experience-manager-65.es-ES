---
title: Grupos de la comunidad
seo-title: Community Groups
description: Creación de grupos de comunidad
seo-description: Creating community groups
uuid: c677d23d-5edb-414c-9013-130c88c2ea52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d94708ee-ca6b-420c-9536-6889d752f9de
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
source-git-commit: 1074843a0105df39382b64defe66fc262986b9c9
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 3%

---

# Grupos de la comunidad {#community-groups}

La función de grupos de comunidad permite que usuarios autorizados (miembros y autores de la comunidad) creen dinámicamente una subcomunidad en un sitio de comunidad desde los entornos de publicación y creación.

Esta capacidad está presente cuando la variable [función de grupos](/help/communities/functions.md#groups-function) está presente en el [sitio comunitario](/help/communities/sites-console.md) estructura.

A [plantilla de grupo de comunidad](/help/communities/tools-groups.md) proporciona el diseño de la página del grupo de comunidad cuando se crea un grupo de comunidad de forma dinámica.

Se seleccionan una o más plantillas de grupo para la función de grupos cuando la función se agrega a la estructura de un sitio de comunidad o a una plantilla de sitio de comunidad. Esta lista de plantillas de grupo se presenta al miembro o autor que crea dinámicamente un nuevo grupo desde el sitio de la comunidad.

## Creación de un nuevo grupo {#creating-a-new-group}

La capacidad de crear un nuevo grupo de comunidad depende de la existencia de un sitio de comunidad que incluya la función de grupos, como uno creado a partir de [Plantilla del sitio de referencia](/help/communities/sites.md).

Los ejemplos siguientes utilizan el sitio de la comunidad creado a partir de `Reference Site Template` como se describe en la [Introducción a AEM Communities](/help/communities/getting-started.md) tutorial.

Esta es la página que se carga en la publicación cuando el **Grupos** elemento de menú seleccionado:

![new-group](assets/new-group.png)

Al seleccionar la variable **Nuevo grupo** , se abrirá un cuadro de diálogo de edición.

En el **Configuración** , se proporcionan las funciones básicas del grupo:

![group-settings](assets/group-settings.png)

* **Nombre del grupo**

   El título del grupo que se mostrará en el sitio de la comunidad. Evite utilizar caracteres de subrayado (_) y palabras clave como recursos y configuración en el nombre del grupo.

* **Descripción**

   Descripción del grupo que se mostrará en el sitio de la comunidad.

* **Invitar**

   Lista de miembros a los que invitar para unirse al grupo. La búsqueda por adelantado proporcionará sugerencias de los miembros de la comunidad para invitar.

* **Nombre de URL del grupo**

   Nombre de la página del grupo que forma parte de la dirección URL.

* **Abrir grupo**

   Seleccionar `Open Group` indica que cualquier visitante anónimo del sitio puede ver el contenido y deseleccionará `Member Only Group`.

* **Grupo de solo miembros**

   Seleccionar `Member Only Group` indica que solo los miembros del grupo pueden ver el contenido y deseleccionarán `Open Group`.

En el **Plantilla** La pestaña es la capacidad de seleccionar de la lista de plantillas de grupo de comunidad que se especificaron cuando la función de grupos se incluyó en la estructura del sitio de comunidad o en una plantilla de sitio de comunidad.

![group-template](assets/group-template.png)

En el **Imagen** es la capacidad de cargar una imagen para mostrarla para el grupo en la página Grupos del sitio de la comunidad. La hoja de estilos predeterminada ajusta el tamaño de la imagen a 170 x 90 píxeles.

![group-image](assets/group-image.png)

Al seleccionar la variable **Crear grupo** , las páginas del grupo se crearán en función de la plantilla seleccionada, se creará un grupo de usuarios para la pertenencia y la página Grupos se actualizará para mostrar la nueva subcomunidad.

Por ejemplo, la página Grupos con una nueva subcomunidad titulada &quot;Grupo de enfoque&quot;, para la que se ha cargado una miniatura de imagen, aparecerá de la siguiente manera (con sesión iniciada como administrador del grupo de comunidad):

![group-page](assets/group-page.png)

Selección de la `Focus Group` Este vínculo abrirá la página Grupo de enfoque en el explorador, que tiene una apariencia inicial basada en la plantilla seleccionada e incluye un submenú debajo del menú del sitio principal de la comunidad:

![open-group-page](assets/open-group-page.png)

### Componente de lista de miembros del grupo de comunidad {#community-group-member-list-component}

El `Community Group Member List` está diseñado para que lo utilicen los desarrolladores de plantillas de grupo.

### Información adicional {#additional-information}

Puede encontrar más información en la [Elementos esenciales del grupo de comunidad](/help/communities/essentials-groups.md) para desarrolladores.

Para obtener más información relacionada con los grupos comunitarios, visite [Administración de usuarios y grupos de usuarios](/help/communities/users.md).
