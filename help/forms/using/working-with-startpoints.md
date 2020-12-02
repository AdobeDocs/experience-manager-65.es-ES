---
title: Uso de puntos de inicio
seo-title: Uso de puntos de inicio
description: Pasos para trabajar con un proceso de AEM Forms desde un dispositivo móvil definido en Workbench.
seo-description: Pasos para trabajar con un proceso de AEM Forms desde un dispositivo móvil definido en Workbench.
uuid: 1c4b4c86-cbdb-4e72-b0eb-7f8a2f5dcdde
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 1ea60fb2-cf9f-4a87-bd8e-98150e668456
docset: aem65
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Uso de puntos de inicio{#working-with-startpoints}

Un punto de partida invoca un proceso creado en Workbench. Se asocia a un formulario que invoca el proceso cuando se envía.

>[!NOTE]
>
>Los términos puntos de inicio, proceso de inicio y formulario se utilizan de forma intercambiable al hacer referencia a este concepto.

Para iniciar un proceso desde la aplicación de AEM Forms, debe tener un punto de partida de tipo **Workspace** en el proceso. Además, debe seleccionar la opción **[!UICONTROL Visibilidad en Mobile Workspace]** para el punto de inicio.

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Inicio de un proceso definido en Workbench**

1. Para realizar la vista de los puntos de inicio disponibles en la aplicación de AEM Forms, vaya a [Pantalla principal](../../forms/using/home-screen.md).
1. En la pantalla **[!UICONTROL Inicio]**, de forma predeterminada, se muestra la lista **[!UICONTROL Todo Forms]**.

   El punto de inicio se asocia a un formulario. Toque el formulario asociado de punto de inicio en la lista para abrirlo.

   Se abre el formulario asociado al punto de inicio.

1. Introduzca los detalles en el formulario **[!UICONTROL Punto de inicio]**.

   Puede agregar anotaciones a esta tarea mediante el botón [datos adjuntos](../../forms/using/add-attachments.md).

1. Después de rellenar el formulario, toque el botón **[!UICONTROL Enviar]**.

Si la aplicación está sin conexión, el formulario y sus datos se guardan en la carpeta Bandeja de salida.

Si la aplicación está en línea, la tarea se sincroniza con el servidor de AEM Forms y se asigna al usuario especificado en el proceso.

Para trabajar con la tarea en su lista de tarea, consulte [Apertura de una tarea](/help/forms/using/open-task.md).
