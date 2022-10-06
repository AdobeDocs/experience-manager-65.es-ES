---
title: Uso de puntos de inicio
seo-title: Working with Startpoints
description: Pasos para trabajar con un proceso AEM Forms desde su dispositivo móvil definido en Workbench.
seo-description: Steps to work with a AEM Forms process from your Mobile device defined in Workbench.
uuid: 1c4b4c86-cbdb-4e72-b0eb-7f8a2f5dcdde
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 1ea60fb2-cf9f-4a87-bd8e-98150e668456
docset: aem65
exl-id: d5970f90-2899-43a5-a3a0-61a2c844d919
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Uso de puntos de inicio{#working-with-startpoints}

Un punto de inicio invoca un proceso creado en Workbench. Está asociado a un formulario que invoca el proceso cuando se envía el formulario.

>[!NOTE]
>
>Los puntos de inicio, el proceso de inicio y el formulario de los términos se utilizan de forma intercambiable al hacer referencia a este concepto.

Para iniciar un proceso desde la aplicación de AEM Forms, debe tener un punto de inicio de tipo **Espacio de trabajo** en su proceso. Además, debe seleccionar la variable **[!UICONTROL Visible en Mobile Workspace]** para el punto de inicio.

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Inicio de un proceso definido en Workbench**

1. Para ver los puntos de inicio disponibles en la aplicación de AEM Forms, vaya a [Pantalla principal](../../forms/using/home-screen.md).
1. En el **[!UICONTROL Página principal]** de forma predeterminada, la variable **[!UICONTROL Todas las Forms]** se muestra.

   El punto de inicio está asociado a un formulario. Pulse el formulario asociado de punto de inicio en la lista para abrirlo.

   Se abre el formulario asociado al punto de inicio.

1. Introduzca los detalles en la **[!UICONTROL Punto de inicio]** formulario.

   Puede añadir anotaciones a esta tarea utilizando el [archivo](../../forms/using/add-attachments.md) botón.

1. Después de rellenar el formulario, pulse la tecla **[!UICONTROL Submit]** botón.

Si la aplicación está sin conexión, el formulario y sus datos se guardan en la carpeta Bandeja de salida.

Si la aplicación está en línea, la tarea se sincroniza con el servidor de AEM Forms y se asigna al usuario especificado en el proceso.

Para trabajar con la tarea en la lista de tareas, consulte [Apertura de una tarea](/help/forms/using/open-task.md).
