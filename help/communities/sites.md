---
title: Plantillas de sitios
description: Obtenga información sobre cómo acceder a la consola Plantillas de sitio para crear un sitio de la comunidad.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 05a944a3-adb1-47b4-b4a5-15bac91c995e
source-git-commit: 00b6f2f03470aca7f87717818d0dfcd17ac16bed
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 4%

---

# Plantillas de sitios {#site-templates}

La consola Plantillas de sitio es similar a [Plantillas de grupo](tools-groups.md) , que se centra en funciones de interés para los grupos de la comunidad.

>[!NOTE]
>
>Las consolas para la creación de [sitios de la comunidad](sites-console.md), [plantillas de sitio de comunidad](sites.md), [plantillas de grupo de comunidad](tools-groups.md), y [funciones de comunidad](functions.md) solo se utilizan en el entorno de creación.

## Consola de plantillas del sitio {#site-templates-console}

En el entorno de creación, para llegar a la consola de sitios de la comunidad:

* Desde la navegación global: **[!UICONTROL Herramientas > Comunidades > Plantillas de sitio]**

Esta consola muestra las plantillas desde las que se puede crear una [sitio comunitario](sites-console.md) se puede crear y permite crear nuevas plantillas de sitio.

![site-template](assets/site-template.png)

## Crear plantilla del sitio {#create-site-template}

Para empezar a crear una plantilla de sitio, seleccione `Create`.

Se abrirá el panel Editor del sitio, que contiene tres subpaneles:

### Información básica {#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

En el panel Información básica, se configura un nombre, una descripción y si la plantilla está habilitada o deshabilitada:

* **[!UICONTROL Nombre de la plantilla del sitio de la comunidad]**

  ID del nombre de la plantilla.

* **[!UICONTROL Descripción de la plantilla del sitio de la comunidad]**

  La descripción de la plantilla.

* **[!UICONTROL Desactivado/Habilitado]**

  Conmutador que controla si la plantilla es referenciable.

### Miniatura    {#thumbnail}

![miniatura del sitio](assets/site-thumbnail.png)

(Opcional) Seleccione el icono Cargar imagen para mostrar una miniatura junto con el nombre y la descripción a los creadores de los sitios de la comunidad.

### Estructura {#structure}

![estructura del sitio](assets/site-structure.png)

Para agregar funciones de la comunidad, arrastre desde el lado derecho hacia la izquierda en el orden en que deben aparecer los vínculos de menú del sitio. Los estilos se aplican a la plantilla durante la creación del sitio.

Por ejemplo, si desea una página de inicio, arrastre la función Página desde la biblioteca y suéltela debajo del generador de plantillas. Esto da como resultado la apertura del cuadro de diálogo de configuración de página. Consulte la [consola de funciones](functions.md) para obtener información sobre los cuadros de diálogo de configuración.

Continúe arrastrando y soltando cualquier otra función de la comunidad que desee para un sitio de la comunidad basado en esta plantilla.

La función de página proporciona una página vacía. La función Grupos permite crear un sitio de grupo (subcomunidad) dentro del sitio de la comunidad.

>[!CAUTION]
>
>La función Grupos debe *no ser el primero ni el único* función en la estructura del sitio.
>
>Cualquier otra función, como la [función de página](functions.md#page-function), debe incluirse y enumerarse primero.

![editor del sitio](assets/site-editor.png)

### Plantillas de grupo para la función Grupos {#group-templates-for-groups-function}

Al incluir una función Grupos en la plantilla del sitio, la configuración requiere la especificación de las opciones de plantilla de grupo permitidas cuando se crea un nuevo grupo en el entorno de publicación.

>[!CAUTION]
>
>La función Grupos debe *no ser el primero ni el único* función en la estructura del sitio.

![site-functions](assets/site-functions.png)

Al seleccionar dos o más plantillas de grupo de comunidad, se proporciona una opción al administrador del grupo al crear realmente un grupo en la comunidad.

![site-function](assets/site-functions1.png)

## Editar plantilla del sitio {#edit-site-template}

Cuando se visualizan plantillas de sitio en el [Consola Plantillas del sitio](#site-templates-console), es posible seleccionar una plantilla de sitio existente para editarla.

Este proceso proporciona los mismos paneles que [creación de una plantilla del sitio](#create-site-template).
