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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Plantillas de grupos{#group-templates}

La consola Plantillas de grupo es similar a la consola Plantillas [de](/help/communities/sites.md) sitio. Ambos son modelos para un conjunto de páginas precableadas y funciones que forman un sitio de comunidad. La diferencia es que una plantilla de sitio es para la comunidad principal y una plantilla de grupo es para un grupo de comunidad, una subcomunidad anidada dentro de la comunidad principal.

Un grupo de comunidad se incorpora a una plantilla de sitio mediante la inclusión de la función [](/help/communities/functions.md#groups-function) Grupos (que puede no ser la primera ni la única función de la plantilla).

En el paquete de [funciones 1](/help/communities/deploy-communities.md#latestfeaturepack)de Comunidades, es posible anidar grupos incluyendo la función Grupos dentro de una plantilla de grupo.

Cuando se realiza una acción para crear un nuevo grupo de comunidad, se selecciona la plantilla (estructura) del grupo. La selección depende de cómo se configuró la función Grupos al agregarla a la plantilla de grupo o sitio.

>[!NOTE]
>
>Las consolas para la creación de sitios [de](/help/communities/sites-console.md)comunidad, plantillas [de sitio de](/help/communities/sites.md)comunidad, plantillas [de grupo de](/help/communities/tools-groups.md) comunidad y funciones [de](/help/communities/functions.md) comunidad solo se pueden usar en el entorno de creación.

## Consola Plantillas de grupo {#group-templates-console}

Para acceder a la consola de plantillas de grupos en el entorno de AEM Author:

* Seleccionar **herramientas| Comunidades| Plantillas de grupo,** desde la navegación global.

Esta consola muestra las plantillas desde las que se puede crear un sitio [de](/help/communities/sites-console.md) comunidad y permite crear nuevas plantillas de grupo.

![Plantilla de grupos de la comunidad](assets/groups-template.png)

## Crear plantilla del grupo {#create-group-template}

Para empezar a crear una nueva plantilla de grupo, seleccione `Create`

Esto mostrará el panel Editor del sitio, que contiene 3 subpaneles:

### Información básica {#basic-info}

![chlimage_1-137](assets/chlimage_1-137.png)

En el panel Información básica, se configura un nombre, una descripción y si la plantilla está habilitada o deshabilitada:

* **Nuevo nombre** de plantilla de grupo ID del nombre de la plantilla

* **Descripción**

   la descripción de la plantilla

* **Deshabilitado/Habilitado**

   un conmutador que controla si se puede hacer referencia a la plantilla

#### Miniatura {#thumbnail}

![chlimage_1-138](assets/chlimage_1-138.png)

(Opcional) Seleccione el icono Cargar imagen para mostrar una miniatura junto con el nombre y la descripción a los creadores de los sitios de la comunidad.

#### Estructura {#structure}

>[!CAUTION]
>
>Si trabaja con AEM 6.1 Communities FP4 o anterior, no agregue una función de grupo a una plantilla de grupo.
>
>La función de grupos anidados está disponible a partir de Communities [FP1](/help/communities/communities.md#latestfeaturepack).
>
>Todavía no se permite agregar una función Grupos como la primera o única función de una plantilla.

![Editor de plantillas de grupo](assets/template-editor.png)

Para agregar funciones de comunidad, arrástrelas de derecha a izquierda en el orden en que deberían aparecer los vínculos de menú del sitio. Los estilos se aplicarán a la plantilla durante la creación del sitio.

Por ejemplo, si desea un foro, arrastre la función de foro desde la biblioteca y coloque debajo del generador de plantillas. Esto resultará en la apertura del cuadro de diálogo de configuración del foro. Consulte la consola [de](/help/communities/functions.md) funciones para obtener información sobre los cuadros de diálogo de configuración.

Continúe arrastrando y soltando cualquier otra función de la comunidad que desee para un sitio de subcomunidad (grupo) basado en esta plantilla.

![funciones de arrastrar](assets/dragfunctions.png)

Una vez que todas las funciones deseadas se hayan colocado en el área del generador de plantillas y se hayan configurado, seleccione **Guardar **en la esquina superior derecha.

## Editar plantilla del grupo {#edit-group-template}

Al ver grupos de comunidad en la consola [principal Plantillas de](#group-templates-console)grupo, es posible seleccionar una plantilla de grupo existente para editarla.

Editar una plantilla de grupo no afectará a los sitios de comunidad que ya se hayan creado a partir de la plantilla. En su lugar, es posible [editar directamente la estructura de un sitio](/help/communities/sites-console.md#modify-structure)de la comunidad.

Este proceso proporciona los mismos paneles que [crear una plantilla](#create-group-template)de grupo.
