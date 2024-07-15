---
title: Plantillas de sitios
description: Obtenga información sobre cómo acceder a la consola Plantillas de sitio para crear un sitio de la comunidad.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 05a944a3-adb1-47b4-b4a5-15bac91c995e
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 3%

---

# Plantillas de sitios {#site-templates}

La consola Plantillas de sitio es similar a la consola [Plantillas de grupo](tools-groups.md), que se centra en funciones de interés para los grupos de la comunidad.

>[!NOTE]
>
>Las consolas para la creación de [sitios de la comunidad](sites-console.md), [plantillas de sitios de la comunidad](sites.md), [plantillas de grupos de la comunidad](tools-groups.md) y [funciones de la comunidad](functions.md) solo se pueden usar en el entorno de creación.

## Consola de plantillas del sitio {#site-templates-console}

En el entorno de creación, para llegar a la consola de sitios de la comunidad:

* Desde la navegación global: **[!UICONTROL Herramientas > Comunidades > Plantillas de sitio]**

Esta consola muestra las plantillas a partir de las cuales se puede crear un [sitio de la comunidad](sites-console.md) y permite crear nuevas plantillas de sitio.

![plantilla del sitio](assets/site-template.png)

## Crear plantilla del sitio {#create-site-template}

Para empezar a crear una plantilla de sitio, seleccione `Create`.

Se abrirá el panel Editor del sitio, que contiene tres subpaneles:

### Información básica {#basic-info}

![información básica sobre la plantilla del sitio](assets/site-template-basicinfo.png)

En el panel Información básica, se configura un nombre, una descripción y si la plantilla está habilitada o deshabilitada:

* **[!UICONTROL Nombre de plantilla de sitio de comunidad]**

  ID del nombre de la plantilla.

* **[!UICONTROL Descripción de la plantilla del sitio de la comunidad]**

  La descripción de la plantilla.

* **[!UICONTROL Deshabilitado/Habilitado]**

  Conmutador que controla si la plantilla es referenciable.

### Miniatura    {#thumbnail}

![miniatura de sitio](assets/site-thumbnail.png)

(Opcional) Seleccione el icono Cargar imagen para mostrar una miniatura junto con el nombre y la descripción a los creadores de los sitios de la comunidad.

### Estructura {#structure}

![estructura del sitio](assets/site-structure.png)

Para agregar funciones de la comunidad, arrastre desde el lado derecho hacia la izquierda en el orden en que deben aparecer los vínculos de menú del sitio. Los estilos se aplican a la plantilla durante la creación del sitio.

Por ejemplo, si desea una página de inicio, arrastre la función Página desde la biblioteca y suéltela debajo del generador de plantillas. Esto da como resultado la apertura del cuadro de diálogo de configuración de página. Consulte la [consola de funciones](functions.md) para obtener información sobre los cuadros de diálogo de configuración.

Continúe arrastrando y soltando cualquier otra función de la comunidad que desee para un sitio de la comunidad basado en esta plantilla.

La función de página proporciona una página vacía. La función Grupos permite crear un sitio de grupo (subcomunidad) dentro del sitio de la comunidad.

>[!CAUTION]
>
>La función Grupos debe *no ser la primera ni la única función* en la estructura del sitio.
>
>Cualquier otra función, como [page function](functions.md#page-function), debe incluirse y enumerarse primero.

![editor del sitio](assets/site-editor.png)

### Plantillas de grupo para la función Grupos {#group-templates-for-groups-function}

Al incluir una función Grupos en la plantilla del sitio, la configuración requiere la especificación de las opciones de plantilla de grupo permitidas cuando se crea un nuevo grupo en el entorno de publicación.

>[!CAUTION]
>
>La función Grupos debe *no ser la primera ni la única función* en la estructura del sitio.

![funciones del sitio](assets/site-functions.png)

Al seleccionar dos o más plantillas de grupo de comunidad, se proporciona una opción al administrador del grupo al crear realmente un grupo en la comunidad.

![función del sitio](assets/site-functions1.png)

## Editar plantilla del sitio {#edit-site-template}

Al ver las plantillas de sitio en la [consola de plantillas de sitio](#site-templates-console) principal, es posible seleccionar una plantilla de sitio existente para editarla.

Este proceso proporciona los mismos paneles que [creando una plantilla de sitio](#create-site-template).
