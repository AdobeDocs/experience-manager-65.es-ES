---
title: Pantalla principal
seo-title: Home screen
description: Descripción de los componentes de la pantalla Inicio de la aplicación AEM Forms
seo-description: Description of the components of the AEM Forms app Home screen
uuid: abc95e58-a685-42a9-82ab-4990155945d3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: ba79479b-4159-4a39-95eb-2285e7ece9d4
docset: aem65
exl-id: 6c6fb516-1b11-4da4-b638-4388a070e397
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '331'
ht-degree: 100%

---

# Pantalla principal{#home-screen}

Al iniciar sesión en la aplicación AEM Forms, se le redirige a la pantalla Inicio.

## Pantalla Inicio predeterminada {#default-home-screen}

De forma predeterminada, la pantalla Inicio muestra todos los formularios, incluidos los puntos de inicio y las tareas (si el servidor conectado está habilitado para AEM Forms Workflow), junto con las miniaturas asociadas. Puede especificar las miniaturas en el servidor de AEM Forms.

La siguiente figura muestra anotaciones con llamadas a los componentes esenciales en la pantalla Inicio predeterminada.

![Pantalla Inicio de la aplicación Forms](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **Botón Menú**: pulse el botón **Menú** para ir a Tareas, Forms, Bandeja de salida y Configuración. Si la aplicación AEM Forms está conectada a un servidor de AEM Forms JEE, puede ver la opción Tareas. La opción Tareas también almacena los borradores creados a partir de las tareas de un proceso. En los servidores OSGi de AEM Forms, la opción Tareas está oculta. La Bandeja de salida almacena los formularios y los borradores guardados antes de sincronizarse con el servidor. Todos los formularios y borradores guardados en la Bandeja de salida se cargan en el servidor de AEM Forms cuando la aplicación [se sincroniza con el servidor](../../forms/using/sync-app.md). Para obtener información sobre la configuración, consulte [Actualización de la configuración general](../../forms/using/update-general-settings.md).
1. **Tarea o formulario**: pulse la tarea o el formulario de la lista con los que desea trabajar.
1. **Puntos suspensivos horizontales**: indican que hay acciones disponibles en el formulario. Al pulsar los puntos suspensivos, se muestran las acciones y la descripción que ha proporcionado el autor. Las opciones **Eliminar borrador** y **Completar** se muestran al pulsar los puntos suspensivos.
1. **Icono Actualizar**: pulse el icono Actualizar para sincronizar la aplicación con el servidor de AEM Forms.

### Personalización de la pantalla Inicio {#customizing-the-home-screen}

![Configuración general](assets/gen-settings.png)

Puede cambiar la pantalla Inicio predeterminada de la aplicación desde la **[Configuración general](../../forms/using/update-general-settings.md)** de la aplicación o desde la pestaña **Preferencia** de HTML Workspace.

Los cambios realizados en la configuración de la pantalla Inicio de la aplicación afectan a la pantalla Inicio del usuario que ha iniciado sesión o el usuario que utiliza el dispositivo móvil actual.

Sin embargo, los cambios realizado en HTML Workspace afectan a todos los usuarios de la aplicación de AEM Forms que han iniciado sesión en el servidor de AEM Forms.
