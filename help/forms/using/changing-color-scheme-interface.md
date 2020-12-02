---
title: Cambio de la combinación de colores de la interfaz
seo-title: Cambio de la combinación de colores de la interfaz
description: Cómo modificar la combinación de colores de las partes de la interfaz de usuario del espacio de trabajo de AEM Forms de forma selectiva.
seo-description: Cómo modificar la combinación de colores de las partes de la interfaz de usuario del espacio de trabajo de AEM Forms de forma selectiva.
uuid: 32c32f7a-8271-4d2c-8a1f-ad5ab3c90b83
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 18dab82a-badf-4c32-83a2-cd5cb04cae89
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# Cambio del esquema de colores de la interfaz {#changing-the-color-scheme-of-the-interface}

Puede modificar la combinación de colores de las partes de la interfaz de usuario del espacio de trabajo de AEM Forms para adaptarlas a sus necesidades. A continuación se muestran algunos ejemplos de personalizaciones representativas de combinaciones de colores. Además de los pasos descritos en este artículo, consulte [Pasos genéricos para la personalización del espacio de trabajo de AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).

## Barra de navegación superior {#top-navigation-bar}

### Uso de la imagen de fondo {#using-background-image}

Para actualizar la barra de navegación en la parte superior del espacio de trabajo de AEM Forms.

1. Cree una imagen de fondo para actualizar el color. Asigne un nombre al archivo como newBackground.jpg.
1. Cargue el archivo de imagen de fondo en la carpeta /apps/ws/images mediante un cliente WebDAV.

   >[!NOTE]
   >
   >Para obtener más información sobre el acceso a WebDAV, consulte [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

1. Haga referencia a la nueva imagen de fondo en /apps/ws/css/newStyle.css añadiendo el siguiente estilo.

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### Uso de la propiedad de color en CSS {#using-color-property-in-css}

1. Añada el siguiente estilo en newStyle.css en /apps/ws/css

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## Componente de categoría {#category-component}

El componente categoría muestra las distintas categorías de sus tareas en el panel izquierdo. Para cambiar su color, defina el color de fondo en el elemento `.category` del archivo CSS.

## Componente de tarea {#task-component}

Las tareas se muestran en el panel central denominado Componente TaskList. Para cambiar el color, modifique el estilo asociado con el selector de tarea .en la hoja de estilo.
