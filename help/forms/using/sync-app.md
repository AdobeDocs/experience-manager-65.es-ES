---
title: Sincronización de la aplicación
seo-title: Sincronización de la aplicación
description: Sincronice la aplicación de AEM Forms en su dispositivo móvil con el servidor de AEM Forms.
seo-description: Sincronice la aplicación de AEM Forms en su dispositivo móvil con el servidor de AEM Forms.
uuid: 3a6fb2d5-2ec4-4f78-a42a-fc921b66238e
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 393e4332-a2cc-42c8-a18f-3035addbcfaa
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Sincronización de la aplicación{#synchronizing-the-app}

## Sincronización de la aplicación {#synchronizing-the-app-1}

Los formularios de su aplicación se descargan del servidor de AEM Forms. Los formularios se descargan en las fichas Tareas y Formularios. Los borradores creados a partir de formularios se descargan en la ficha Borradores y los borradores creados a partir de tareas se descargan en la ficha Tareas. Para un formulario independiente en el servidor OSGi, los formularios y los borradores se descargan en las fichas Formularios y Borrador, respectivamente.

Cuando completa y envía un formulario, éste se carga de nuevo en el servidor de AEM Forms instantáneamente si la aplicación está en línea. Los formularios se recuperan del servidor cuando se sincroniza la aplicación. Sin embargo, los borradores se sincronizan con el servidor instantáneamente si la aplicación está en línea.

Cuando está en línea con el servidor de AEM Forms, de forma predeterminada, la aplicación se sincroniza cada 15 minutos. Sin embargo, tiene la opción de cambiar la frecuencia de sincronización. Como alternativa, puede sincronizar manualmente la aplicación en cualquier momento.

**Para sincronizar la aplicación manualmente**

Toque el botón Sincronizar aplicación ![de](assets/sync-app.png) sincronización en la esquina inferior derecha de la pantalla de inicio.

**Para alterar la frecuencia de sincronización**

1. Para ir a la pantalla Configuración, toque el botón de menú en la esquina superior izquierda de la pantalla Inicio y, a continuación, toque **Configuración**.
1. En la pantalla Configuración, toque la ficha General.

   ![Configuración de frecuencia de sincronización en la ventana Configuración general](assets/gen-settings-2.png)

1. En la opción Sincronizar frecuencia, toque el valor a la derecha de la frecuencia de sincronización.
1. En la lista desplegable, seleccione la nueva frecuencia de sincronización.

### Especificaciones técnicas {#technical-specifications}

* La lógica principal del envío de datos de la aplicación sin conexión al servidor de AEM Forms se incluye en runtime/offline/util/offline.js.
* En el archivo .js, la llamada a la función processOfflineSubmissionSavedTasks(...) envía las tareas guardadas o enviadas al servidor. También se ocupa de los errores o conflictos en el proceso de sincronización. Si falla el envío de una tarea, la tarea de la aplicación se marca como fallida. Además, la tarea permanece en la Bandeja de salida.
* Las funciones syncSubmissionTask() y syncSavedTask() realizan operaciones en tareas individuales.
* El componente de lista de tareas inicia la llamada a la función processOfflineSubmissionSavedTasks() después de que un usuario selecciona sincronizar el estado sin conexión con el servidor o una sincronización automática por el subproceso en segundo plano.

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
