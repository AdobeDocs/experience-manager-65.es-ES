---
title: Cambiar el esquema de colores de la interfaz
description: Cómo modificar el esquema de colores de las partes de la interfaz de usuario de AEM Forms Workspace de forma selectiva.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: e0a261a2-518b-4984-a5b5-24f0b9222e24
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 96%

---

# Cambiar el esquema de colores de la interfaz {#changing-the-color-scheme-of-the-interface}

Puede modificar el esquema de colores de las partes de la interfaz de usuario de AEM Forms Workspace para adaptarlas a sus necesidades. A continuación se muestran algunos ejemplos de personalizaciones representativas de combinaciones de colores. Además de los pasos mencionados en este artículo, consulte [Pasos genéricos para personalizar AEM Forms Workspace](/help/forms/using/generic-steps-html-workspace-customization.md).

## Barra de navegación superior {#top-navigation-bar}

### Usar la imagen de fondo {#using-background-image}

Actualizar la barra de navegación de la parte superior de AEM Forms Workspace.

1. Cree una imagen de fondo para actualizar el color. Asigne un nombre al archivo como newBackground.jpg.
1. Cargue el archivo de imagen de fondo en la carpeta /apps/ws/images mediante un cliente WebDAV.

   >[!NOTE]
   >
   >Para obtener más información, consulte [Acceso a WebDAV](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=es).

1. Agregue el siguiente estilo para hacer referencia a la nueva imagen de fondo en /apps/ws/css/newStyle.css

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### Usar la propiedad de color en CSS {#using-color-property-in-css}

1. Agregue el siguiente estilo en newStyle.css en /apps/ws/css

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## Componente Categoría {#category-component}

El componente Categoría muestra las distintas categorías de las tareas en el panel izquierdo. Para cambiar su color, defina el color de fondo en el elemento `.category` del archivo CSS.

## Componente Tarea {#task-component}

Las tareas se muestran en el panel central llamado Componente TaskList. Para cambiar su color, modifique el estilo asociado con el selector .task en la hoja de estilo.
