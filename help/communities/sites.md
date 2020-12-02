---
title: Plantillas de sitios
seo-title: Plantillas de sitios
description: Cómo acceder a la consola Plantillas de sitio
seo-description: Cómo acceder a la consola Plantillas de sitio
uuid: d2f7556e-7e43-424e-82f1-41790aeb2d98
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 202d7dba-2b34-431d-b10f-87775632807f
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 4%

---


# Plantillas de sitios {#site-templates}

La consola Plantillas de sitio es muy similar a la consola [Plantillas de grupo](tools-groups.md), que se centra en funciones de interés para los grupos de la comunidad.

>[!NOTE]
>
>Las consolas para la creación de [sitios de comunidad](sites-console.md), [plantillas de sitio de comunidad](sites.md), [plantillas de grupo de comunidad](tools-groups.md) y [funciones de comunidad](functions.md) sólo se pueden usar en el entorno de creación.

## Consola de plantillas de sitio {#site-templates-console}

En el entorno de creación, para llegar a la consola de sitios de comunidad:

* Desde la navegación global: **[!UICONTROL Herramientas > Comunidades > Plantillas de sitio]**

Esta consola muestra las plantillas desde las que se puede crear un [sitio de comunidad](sites-console.md) y permite crear nuevas plantillas de sitio.

![site-template](assets/site-template.png)

## Crear plantilla del sitio {#create-site-template}

Para empezar a crear una nueva plantilla de sitio, seleccione `Create`.

Esto mostrará el panel Editor del sitio, que contiene 3 subpaneles:

### Información básica {#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

En el panel Información básica, se configura un nombre, una descripción y si la plantilla está habilitada o deshabilitada:

* **[!UICONTROL Nombre de la plantilla del sitio de la comunidad]**

   ID del nombre de la plantilla.

* **[!UICONTROL Descripción de la plantilla del sitio de la comunidad]**

   Descripción de la plantilla.

* **[!UICONTROL Deshabilitado/Habilitado]**

   Un conmutador que controla si se puede hacer referencia a la plantilla.

### Miniatura    {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

(Opcional) Seleccione el icono Cargar imagen para mostrar una miniatura junto con el nombre y la descripción a los creadores de los sitios de la comunidad.

### Estructura {#structure}

![site-structure](assets/site-structure.png)

Para agregar funciones de comunidad, arrástrelas de derecha a izquierda en el orden en que deberían aparecer los vínculos de menú del sitio. Los estilos se aplicarán a la plantilla durante la creación del sitio.

Por ejemplo, si desea una página de inicio, arrastre la función Página de la biblioteca y suéltela debajo del generador de plantillas. Esto resultará en la apertura del cuadro de diálogo de configuración de página. Consulte la [consola de funciones](functions.md) para obtener información sobre los cuadros de diálogo de configuración.

Continúe arrastrando y soltando cualquier otra función de comunidad que desee para un sitio de comunidad basado en esta plantilla.

La función de página proporciona una página vacía. La función de grupos permite crear un sitio de grupo (subcomunidad) dentro del sitio de la comunidad.

>[!CAUTION]
>
>La función de grupos debe *no* ser la *primera ni la única* función de la estructura del sitio.
>
>Cualquier otra función, como la [función de página](functions.md#page-function), debe incluirse y enumerarse primero.

![site-editor](assets/site-editor.png)

### Función Plantillas de grupo para grupos {#group-templates-for-groups-function}

Al incluir una función de grupos en la plantilla de sitio, la configuración requiere la especificación de las opciones de plantilla de grupo permitidas cuando se crea un nuevo grupo en el entorno de publicación.

>[!CAUTION]
>
>La función Groups debe *no* ser la *primera ni la única* función de la estructura del sitio.

![site-features](assets/site-functions.png)

Al seleccionar dos o más plantillas de grupo de comunidad, se proporciona una opción al administrador del grupo al crear un nuevo grupo en la comunidad.

![site-function](assets/site-functions1.png)

## Editar plantilla del sitio{#edit-site-template}

Al ver las plantillas de sitio en la consola [Plantillas de sitio](#site-templates-console) principal, es posible seleccionar una plantilla de sitio existente para editarla.

Este proceso proporciona los mismos paneles que [crear una plantilla de sitio](#create-site-template).
