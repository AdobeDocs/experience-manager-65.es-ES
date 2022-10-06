---
title: Actualización de la configuración general
seo-title: Updating general settings
description: Actualice la configuración de la aplicación de AEM Forms, como la pantalla principal y recupere las opciones de puntos de inicio y archivos adjuntos
seo-description: Update AEM Forms app settings such as the Home screen and fetch Startpoints and attachments options
uuid: 650d677e-2b3c-498e-9e46-fa659af934ca
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 7fdb9fab-6bae-49b8-86b6-66138a2a6cd3
docset: aem65
exl-id: 3e74cda2-ba3e-4ee9-b7d0-76a804232199
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 1%

---

# Actualización de la configuración general{#updating-general-settings}

La configuración general de la aplicación de AEM Forms permite especificar opciones de configuración, como recuperar archivos adjuntos, modo sin conexión, pantalla de aterrizaje, categoría predeterminada y frecuencia de guardado automático.

## Actualización de la configuración general en la aplicación {#working-with-the-form}

Al sincronizar la aplicación con el servidor de AEM Forms, todos los formularios y las tareas definidas se descargan en el dispositivo móvil.

La solución predeterminada de aplicaciones de AEM Forms no descarga los archivos adjuntos asociados a cada formulario cuando la aplicación está sincronizada.

En la pestaña General , cambie los ajustes de descarga de archivos adjuntos, modo sin conexión, pantalla de aterrizaje, guardado automático y sincronización. Puede cambiar el [Pantalla principal](../../forms/using/home-screen.md) de su aplicación.

**Vaya a la ficha General en la pantalla Configuración**

1. Para ir a la pantalla Configuración , pulse el botón Menú en la esquina superior izquierda de la pantalla Inicio y, a continuación, pulse **Configuración**.
1. En la pantalla Configuración , pulse la pestaña General .

   ![Configuración general en la aplicación de AEM Forms](assets/gen-settings-1.png)

   Pantalla Configuración general

   >[!NOTE]
   >
   >Las opciones pueden mostrarse de forma diferente en distintos dispositivos móviles.

### Configuración general {#general-settings}

Puede realizar los siguientes cambios en la configuración de la aplicación.

* **Buscar archivos adjuntos de tareas**: Para especificar si desea descargar o no los archivos adjuntos asociados cuando se descarga cada tarea en la aplicación.
* **Modo sin conexión**: Para habilitar o deshabilitar el servicio sin conexión para la aplicación AEM Forms. Consulte [Trabajo en modo sin conexión](/help/forms/using/work-offline-mode.md) para obtener más información.
* **Pantalla de aterrizaje**: Para establecer la ubicación de inicio ([Pantalla principal](../../forms/using/home-screen.md)) para la aplicación.
Opciones disponibles:

   * Forms
   * Tareas
   * Favoritos

* **Categoría predeterminada**: Permite seleccionar la categoría de formularios que se va a mostrar en la pantalla principal. Al seleccionar Todos, puede ver todos los formularios en la pantalla principal. Las categorías se rellenan en función de los formularios cargados en la aplicación. Forms está disponible en la aplicación en función de la configuración de formulario especificada en el servidor de AEM Forms.

* **Frecuencia de guardado automático**: Para definir la frecuencia con la que [aplicación móvil guarda datos de formulario](../../forms/using/autosave-data-app.md) local.
* **Frecuencia de sincronización**: Para definir la frecuencia con la que [la aplicación móvil está sincronizada](../../forms/using/sync-app.md) con el servidor de AEM Forms en modo en línea.
   **Borrar datos locales**: Borre la base de datos, incluida la configuración y los datos locales de todos los usuarios y el almacenamiento de archivos del dispositivo.

>[!NOTE]
>
>Al borrar la caché, se cerrará la sesión inmediatamente de la aplicación.
>
>Sin embargo, se le pedirá que confirme la operación de borrado de caché.
