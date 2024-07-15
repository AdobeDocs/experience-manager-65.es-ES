---
title: Plantillas de grupo
description: Obtenga información sobre cómo acceder a la consola de plantillas de grupo para un conjunto de páginas precableadas y funciones que forman un sitio de la comunidad.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: aed2c3f2-1b5e-4065-8cec-433abb738ef5
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---

# Plantillas de grupo {#group-templates}

La consola de plantillas de grupo es similar a la consola [Plantillas de sitio](/help/communities/sites.md). Ambos son modelos para un conjunto de páginas precableadas y funciones que forman un sitio de la comunidad. La diferencia es que una plantilla de sitio es para la comunidad principal y una plantilla de grupo es para un grupo de comunidad, una subcomunidad anidada dentro de la comunidad principal.

Un grupo de comunidad se incorpora a una plantilla de sitio al incluir la función [Grupos](/help/communities/functions.md#groups-function) (que puede no ser la primera ni la única función de la plantilla).

A partir del paquete de características 1](/help/communities/deploy-communities.md#latestfeaturepack) de Communities [es posible anidar grupos incluyendo la función Grupos dentro de una plantilla de grupo.

En el momento en que se realiza una acción para crear un grupo de comunidad, se selecciona la plantilla (estructura) del grupo. La selección depende de cómo se configuró la función Grupos cuando se agregó al sitio o a la plantilla del grupo.

>[!NOTE]
>
>Las consolas para la creación de [sitios de la comunidad](/help/communities/sites-console.md), [plantillas de sitios de la comunidad](/help/communities/sites.md), [plantillas de grupos de la comunidad](/help/communities/tools-groups.md) y [funciones de la comunidad](/help/communities/functions.md) solo se pueden usar en el entorno de creación.

## Consola de plantillas de grupo {#group-templates-console}

AEM Para llegar a la consola de plantillas de grupo en el entorno de autor de la:

* Seleccionar **herramientas | Communities | Plantillas de grupo,** de navegación global.

Esta consola muestra las plantillas a partir de las cuales se puede crear un [sitio de la comunidad](/help/communities/sites-console.md) y permite crear nuevas plantillas de grupo.

![Plantilla de grupos de la comunidad](assets/groups-template.png)

## Crear plantilla del grupo {#create-group-template}

Para empezar a crear una plantilla de grupo, seleccione `Create`.

Esto abre el panel Editor del sitio, que contiene tres subpaneles:

### Información básica {#basic-info}

![información básica del sitio](assets/site-basic-info.png)

En el panel Información básica, se configura un nombre, una descripción y si la plantilla está habilitada o deshabilitada:

* **Nuevo nombre de plantilla de grupo**

  ID del nombre de la plantilla.

* **Descripción**

  La descripción de la plantilla.

* **Deshabilitado/Habilitado**

  Conmutador que controla si la plantilla es referenciable.

#### Miniatura    {#thumbnail}

![miniatura de sitio](assets/site-thumbnail.png)

(Opcional) Seleccione el icono Cargar imagen para mostrar una miniatura junto con el Nombre y la Descripción a los creadores de los sitios de la comunidad.

#### Estructura {#structure}

>[!CAUTION]
>
>AEM Si trabaja con comunidades FP4 de 6.1 o versiones anteriores, no agregue una función de grupos a una plantilla de grupo.
>
>La característica de grupos anidados está disponible a partir de las comunidades [FP1](/help/communities/communities.md#latestfeaturepack).
>
>Sigue sin estar permitido agregar una función de grupos como primera o única función en una plantilla.

![Editor de plantillas de grupo](assets/template-editor.png)

Para agregar funciones de la comunidad, arrastre desde el lado derecho hacia la izquierda en el orden en que deben aparecer los vínculos de menú del sitio. Los estilos se aplican a la plantilla durante la creación del sitio.

Por ejemplo, si desea un foro, arrastre la función del foro desde la biblioteca y suéltela debajo del generador de plantillas. Esto da como resultado la apertura del cuadro de diálogo de configuración del foro. Consulte la [consola de funciones](/help/communities/functions.md) para obtener información sobre los cuadros de diálogo de configuración.

Continúe arrastrando y soltando cualquier otra función de la comunidad que desee para un sitio (grupo) de subcomunidad basado en esta plantilla.

![funciones de arrastre](assets/dragfunctions.png)

Una vez que todas las funciones deseadas se hayan colocado en el área del generador de plantillas y se hayan configurado, seleccione **Guardar** en la esquina superior derecha.

## Editar plantilla del grupo {#edit-group-template}

Al ver los grupos de la comunidad en la [consola de plantillas de grupo](#group-templates-console) principal, es posible seleccionar una plantilla de grupo existente para editarla.

La edición de una plantilla de grupo no afecta a los sitios de la comunidad ya creados a partir de la plantilla. En su lugar, es posible [editar directamente la estructura de un sitio de la comunidad](/help/communities/sites-console.md#modify-structure).

Este proceso proporciona los mismos paneles que [creando una plantilla de grupo](#create-group-template).
