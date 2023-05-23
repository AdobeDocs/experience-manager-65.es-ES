---
title: Plantillas de grupo
seo-title: Group Templates
description: Cómo acceder a la consola Plantillas de grupo
seo-description: How to access the Group Templates console
uuid: 4cf20c91-32b0-4051-a98d-44e4eb50a231
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e9bfbbce-93fc-455c-a2f7-4ee44e63c03f
docset: aem65
role: Admin
exl-id: aed2c3f2-1b5e-4065-8cec-433abb738ef5
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 3%

---

# Plantillas de grupo {#group-templates}

La consola Plantillas de grupo es similar a [Plantillas de sitio](/help/communities/sites.md) consola. Ambos son modelos para un conjunto de páginas precableadas y funciones que forman un sitio de la comunidad. La diferencia es que una plantilla de sitio es para la comunidad principal y una plantilla de grupo es para un grupo de comunidad, una subcomunidad anidada dentro de la comunidad principal.

Un grupo de comunidad se incorpora a una plantilla de sitio incluyendo el [Función Grupos](/help/communities/functions.md#groups-function) (que puede no ser la primera ni la única función de la plantilla).

A partir de comunidades [paquete de funciones 1](/help/communities/deploy-communities.md#latestfeaturepack)Además, es posible anidar grupos incluyendo la función Grupos dentro de una plantilla de grupo.

En el momento en que se realiza una acción para crear un nuevo grupo de comunidad, se selecciona la plantilla (estructura) del grupo. La selección depende de cómo se configuró la función Grupos cuando se agregó al sitio o a la plantilla del grupo.

>[!NOTE]
>
>Las consolas para la creación de [sitios de la comunidad](/help/communities/sites-console.md), [plantillas de sitio de comunidad](/help/communities/sites.md), [plantillas de grupo de comunidad](/help/communities/tools-groups.md) y [funciones de comunidad](/help/communities/functions.md) solo se utilizan en el entorno de creación.

## Consola de plantillas de grupo {#group-templates-console}

Para llegar a la consola de plantillas de grupos en el entorno de AEM Author:

* Seleccionar **Herramientas | Communities | Plantillas de grupo,** desde la navegación global.

Esta consola muestra las plantillas desde las que se puede crear una [sitio comunitario](/help/communities/sites-console.md) se puede crear y permite crear nuevas plantillas de grupo.

![Plantilla de grupos de comunidad](assets/groups-template.png)

## Crear plantilla del grupo {#create-group-template}

Para empezar a crear una nueva plantilla de grupo, seleccione `Create`.

Esto mostrará el panel Editor del sitio, que contiene 3 subpaneles:

### Información básica {#basic-info}

![site-basic-info](assets/site-basic-info.png)

En el panel Información básica, se configura un nombre, una descripción y si la plantilla está habilitada o deshabilitada:

* **Nombre de la plantilla del grupo nuevo**

   ID del nombre de la plantilla.

* **Descripción**

   La descripción de la plantilla.

* **Desactivado/Habilitado**

   Conmutador que controla si la plantilla es referenciable.

#### Miniatura    {#thumbnail}

![miniatura del sitio](assets/site-thumbnail.png)

(Opcional) Seleccione el icono Cargar imagen para mostrar una miniatura junto con el Nombre y la Descripción a los creadores de los sitios de la comunidad.

#### Estructura {#structure}

>[!CAUTION]
>
>AEM Si trabaja con comunidades FP4 de 6.1 o versiones anteriores, no agregue una función de grupos a una plantilla de grupo.
>
>La función de grupos anidados está disponible a partir de Communities [FP1](/help/communities/communities.md#latestfeaturepack).
>
>Sigue sin estar permitido agregar una función de grupos como primera o única función en una plantilla.

![Editor de plantillas de grupo](assets/template-editor.png)

Para agregar funciones de la comunidad, arrastre desde el lado derecho hacia la izquierda en el orden en que deben aparecer los vínculos de menú del sitio. Los estilos se aplicarán a la plantilla durante la creación del sitio.

Por ejemplo, si desea un foro, arrastre la función del foro desde la biblioteca y suéltela debajo del generador de plantillas. Esto hará que se abra el cuadro de diálogo de configuración del foro. Consulte la [consola de funciones](/help/communities/functions.md) para obtener información sobre los cuadros de diálogo de configuración.

Continúe arrastrando y soltando cualquier otra función de la comunidad que desee para un sitio (grupo) de subcomunidad basado en esta plantilla.

![arrastrar funciones](assets/dragfunctions.png)

Una vez que todas las funciones deseadas se hayan colocado en el área del generador de plantillas y se hayan configurado, seleccione **Guardar** en la esquina superior derecha.

## Editar plantilla del grupo {#edit-group-template}

Al ver los grupos de la comunidad en el [Consola de plantillas de grupo](#group-templates-console), es posible seleccionar una plantilla de grupo existente para editarla.

La edición de una plantilla de grupo no afectará a los sitios de la comunidad ya creados a partir de la plantilla. Es posible hacer lo siguiente [editar un sitio de la comunidad](/help/communities/sites-console.md#modify-structure)La estructura de en su lugar.

Este proceso proporciona los mismos paneles que [creación de una plantilla de grupo](#create-group-template).
