---
title: Sincronización de la aplicación
seo-title: Synchronizing the app
description: Sincronice la aplicación de AEM Forms en su dispositivo móvil con el servidor de AEM Forms.
seo-description: Synchronize the AEM Forms app on your mobile device with the AEM Forms server.
uuid: 3a6fb2d5-2ec4-4f78-a42a-fc921b66238e
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 393e4332-a2cc-42c8-a18f-3035addbcfaa
docset: aem65
exl-id: 6bb1d6df-b322-4112-bc25-6300877ee146
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Sincronización de la aplicación{#synchronizing-the-app}

## Sincronización de la aplicación {#synchronizing-the-app-1}

Los formularios de la aplicación se descargan del servidor de AEM Forms. Los formularios se descargan en las fichas Tareas y Forms . Los borradores creados a partir de los formularios se descargan en la pestaña borradores y los borradores creados a partir de las tareas se descargan en la pestaña tareas. Para un formulario independiente en el servidor OSGi, los formularios y borradores se descargan en las pestañas Forms y Borrador respectivamente.

Cuando se completa y envía un formulario, este se vuelve a cargar en el servidor de AEM Forms al instante si la aplicación está en línea. Los formularios se recuperan del servidor cuando la aplicación se sincroniza. Sin embargo, los borradores se sincronizan con el servidor instantáneamente si la aplicación está en línea.

Cuando está en línea con el servidor de AEM Forms, de forma predeterminada, la aplicación se sincroniza cada 15 minutos. Sin embargo, tiene la opción de cambiar la frecuencia de sincronización. Como alternativa, puede sincronizar manualmente la aplicación en cualquier momento.

**Para sincronizar la aplicación manualmente**

Puntee en el botón Sincronizar ![sync-app](assets/sync-app.png) en la esquina inferior derecha de la pantalla principal.

**Modificación de la frecuencia de sincronización**

1. Para ir a la pantalla Configuración , pulse el botón de menú en la esquina superior izquierda de la pantalla Inicio y, a continuación, pulse **Configuración**.
1. En la pantalla Configuración , pulse la pestaña General .

   ![Configuración de frecuencia de sincronización en la ventana Configuración general](assets/gen-settings-2.png)

1. En la opción Frecuencia de sincronización , pulse el valor a la derecha de Frecuencia de sincronización.
1. En la lista desplegable, seleccione la nueva frecuencia de sincronización.

### Especificaciones técnicas {#technical-specifications}

* La lógica principal del envío de datos de aplicaciones sin conexión al servidor de AEM Forms se incluye en runtime/offline/util/offline.js.
* En el .js, la llamada a la función processOfflineSubmittedSavedTasks(...) envía las tareas guardadas/enviadas al servidor. También gestiona cualquier error o conflicto en el proceso de sincronización. Si falla el envío de una tarea, la tarea de la aplicación se marca como fallida. Además, la tarea permanece en la Bandeja de salida.
* La función syncSubmittedTask() y syncSavedTask() realizan operaciones en tareas individuales.
* La llamada a la función processOfflineSubmittedSavedTasks() se inicia mediante el componente de lista de tareas después de que un usuario selecciona sincronizar el estado sin conexión con el servidor o una sincronización automática por el subproceso en segundo plano.
