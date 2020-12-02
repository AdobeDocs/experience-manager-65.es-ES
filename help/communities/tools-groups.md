---
title: Plantillas de grupos
seo-title: Plantillas de grupos
description: Cómo acceder a la consola Plantillas de grupo
seo-description: Cómo acceder a la consola Plantillas de grupo
uuid: 4cf20c91-32b0-4051-a98d-44e4eb50a231
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e9bfbbce-93fc-455c-a2f7-4ee44e63c03f
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 3%

---


# Plantillas de grupos {#group-templates}

La consola Plantillas de grupo es similar a la consola [Plantillas de sitio](/help/communities/sites.md). Ambos son modelos para un conjunto de páginas precableadas y funciones que forman un sitio de comunidad. La diferencia es que una plantilla de sitio es para la comunidad principal y una plantilla de grupo es para un grupo de comunidad, una subcomunidad anidada dentro de la comunidad principal.

Un grupo de comunidad se incorpora a una plantilla de sitio mediante la inclusión de la función [Grupos](/help/communities/functions.md#groups-function) (que puede no ser la primera ni la única función de la plantilla).

En el paquete de funciones 1](/help/communities/deploy-communities.md#latestfeaturepack) de Comunidades [, es posible anidar grupos incluyendo la función Grupos dentro de una plantilla de grupo.

Cuando se realiza una acción para crear un nuevo grupo de comunidad, se selecciona la plantilla (estructura) del grupo. La selección depende de cómo se configuró la función Grupos al agregarla a la plantilla de grupo o sitio.

>[!NOTE]
>
>Las consolas para la creación de [sitios de comunidad](/help/communities/sites-console.md), [plantillas de sitio de comunidad](/help/communities/sites.md), [plantillas de grupo de comunidad](/help/communities/tools-groups.md) y [funciones de comunidad](/help/communities/functions.md) sólo se pueden usar en el entorno de creación.

## Consola de plantillas de grupo {#group-templates-console}

Para acceder a la consola de plantillas de grupos en AEM Author entorno:

* Seleccionar **Herramientas | Comunidades | Plantillas de grupo,** de navegación global.

Esta consola muestra las plantillas desde las que se puede crear un [sitio de comunidad](/help/communities/sites-console.md) y permite crear nuevas plantillas de grupo.

![Plantilla de grupos de la comunidad](assets/groups-template.png)

## Crear plantilla del grupo {#create-group-template}

Para empezar a crear una nueva plantilla de grupo, seleccione `Create`.

Esto mostrará el panel Editor del sitio, que contiene 3 subpaneles:

### Información básica {#basic-info}

![site-basic-info](assets/site-basic-info.png)

En el panel Información básica, se configura un nombre, una descripción y si la plantilla está habilitada o deshabilitada:

* **Nombre de la plantilla del grupo nuevo**

   ID del nombre de la plantilla.

* **Descripción**

   Descripción de la plantilla.

* **Deshabilitado/Habilitado**

   Un conmutador que controla si se puede hacer referencia a la plantilla.

#### Miniatura    {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

(Opcional) Seleccione el icono Cargar imagen para mostrar una miniatura junto con el nombre y la descripción a los creadores de los sitios de la comunidad.

#### Estructura {#structure}

>[!CAUTION]
>
>Si trabaja con AEM 6.1 Communities FP4 o anterior, no agregue una función de grupo a una plantilla de grupo.
>
>La función de grupos anidados está disponible desde Communities [FP1](/help/communities/communities.md#latestfeaturepack).
>
>Todavía no se permite agregar una función Grupos como la primera o única función de una plantilla.

![Editor de plantillas de grupo](assets/template-editor.png)

Para agregar funciones de comunidad, arrástrelas de derecha a izquierda en el orden en que deberían aparecer los vínculos de menú del sitio. Los estilos se aplicarán a la plantilla durante la creación del sitio.

Por ejemplo, si desea un foro, arrastre la función de foro desde la biblioteca y coloque debajo del generador de plantillas. Esto resultará en la apertura del cuadro de diálogo de configuración del foro. Consulte la [consola de funciones](/help/communities/functions.md) para obtener información sobre los cuadros de diálogo de configuración.

Continúe arrastrando y soltando cualquier otra función de la comunidad que desee para un sitio de subcomunidad (grupo) basado en esta plantilla.

![funciones de arrastrar](assets/dragfunctions.png)

Una vez que todas las funciones deseadas se hayan colocado en el área del generador de plantillas y se hayan configurado, seleccione **Guardar** en la esquina superior derecha.

## Editar plantilla del grupo {#edit-group-template}

Al ver grupos de comunidad en la consola [Plantillas de grupo](#group-templates-console) principal, es posible seleccionar una plantilla de grupo existente para editarla.

Editar una plantilla de grupo no afectará a los sitios de comunidad que ya se hayan creado a partir de la plantilla. En su lugar, es posible editar directamente [la estructura de un sitio de comunidad](/help/communities/sites-console.md#modify-structure).

Este proceso proporciona los mismos paneles que [crear una plantilla de grupo](#create-group-template).
