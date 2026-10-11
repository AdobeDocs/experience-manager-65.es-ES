---
title: Trabajar con puntos de inicio
description: Pasos para trabajar con un proceso de Adobe Experience Manager Forms desde su dispositivo móvil definido en Workbench.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: d5970f90-2899-43a5-a3a0-61a2c844d919
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 43%
---

# Trabajar con puntos de inicio{#working-with-startpoints}

>[!NOTE]
>
>La aplicación de AEM Forms está actualmente en desuso. Si tiene alguna pregunta o ayuda, comuníquese con [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com).

Un punto de inicio invoca un proceso creado en Workbench. Está asociado a un formulario que invoca el proceso cuando se envía el formulario.

>[!NOTE]
>
>Los puntos de inicio, el proceso de inicio y el formulario de los términos se utilizan de forma intercambiable al hacer referencia a este concepto.

Para iniciar un proceso desde la aplicación Forms de Adobe Experience Manager (AEM), debe tener un punto de inicio de tipo **Workspace** en su proceso. Además, debe seleccionar la opción **[!UICONTROL Visible en Workspace móvil]** para el punto de inicio.

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Para iniciar un proceso definido en Workbench**

1. Para ver los puntos de inicio disponibles en la aplicación de AEM Forms, vaya a la [Pantalla de inicio](../../forms/using/home-screen.md).
1. En la pantalla **[!UICONTROL Inicio]**, de forma predeterminada, se muestra la lista **[!UICONTROL Todos los formularios]**.

   El punto de inicio está asociado a un formulario. Seleccione el formulario asociado al punto de inicio en la lista para abrirlo.

   Se abre el formulario asociado al punto de inicio.

1. Introduzca los detalles en el formulario **[!UICONTROL Punto de inicio]**.

   Puede agregar anotaciones a esta tarea con el botón [Archivo adjunto](../../forms/using/add-attachments.md).

1. Después de rellenar el formulario, selecciona el botón **[!UICONTROL Enviar]**.

Si la aplicación está sin conexión, el formulario y sus datos se guardan en la carpeta Bandeja de salida.

Si la aplicación está en línea, la tarea se sincroniza con el servidor de AEM Forms y se asigna al usuario especificado en el proceso.

Para trabajar con la tarea en la lista de tareas, consulte [Abrir una tarea](/help/forms/using/open-task.md).
