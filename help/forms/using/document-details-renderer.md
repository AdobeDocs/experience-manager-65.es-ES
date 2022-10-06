---
title: Detalles del documento para el procesador
seo-title: Document details for renderer
description: Información conceptual sobre cómo funcionan las renderizaciones en el espacio de trabajo de AEM Forms para procesar los distintos tipos de formularios y archivos admitidos.
seo-description: Conceptual information on how renders work in AEM Forms workspace to render the various supported form and file types.
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# Detalles del documento para el procesador {#document-details-for-renderer}

## Introducción {#introduction}

En el espacio de trabajo de AEM Forms, se admiten varios tipos de formularios sin problemas. Entre estas características se incluyen:

* PDF forms (XDP/Acroform/PDF planos)
* Nuevos formularios de HTML
* Imágenes
* Aplicaciones de terceros (por ejemplo, Gestión de Correspondencia)

Este documento explica el trabajo de estos procesadores desde la perspectiva de la personalización semántica / reutilización de componentes, de modo que los requisitos del cliente se cumplan sin romper ninguna representación. Aunque el espacio de trabajo de AEM Forms permite cualquier cambio semántico/de interfaz de usuario, se recomienda que no se cambie la lógica de renderización de distintos tipos de formulario; de lo contrario, los resultados pueden ser impredecibles. Este documento es para orientación / conocimiento para admitir la renderización del mismo formulario, utilizando los mismos componentes de espacio de trabajo en diferentes portales, y no para modificar la propia lógica de renderización.

## PDF forms {#pdf-forms}

Los PDF forms son procesados por `PdfTaskForm View`.

Cuando se procesa un formulario XDP como PDF, se muestra una variable `FormBridge` El servicio FormsAugmenter agrega JavaScript™. Este JavaScript™ (dentro del formulario de PDF) ayuda a realizar acciones como enviar formularios, guardar formularios o quitar formularios sin conexión.

En el espacio de trabajo de AEM Forms, la vista PDFTaskForm se comunica con la `FormBridge`javascript, a través de un HTML intermedio presente en `/lc/libs/ws/libs/ws/pdf.html`. El flujo es:

**Vista PDFTaskForm: pdf.html**

Se comunica mediante `window.postMessage` / `window.attachEvent('message')`

Este método es la forma estándar de comunicación entre un fotograma principal y un iframe. Los oyentes de eventos existentes de los PDF forms abiertos anteriormente se eliminan antes de agregar uno nuevo. Esta depuración también tiene en cuenta el cambio entre la pestaña del formulario y la pestaña del historial en la vista de detalles de la tarea.

**pdf.html - `FormBridge`javascript dentro del PDF representado**

Se comunica mediante `pdfObject.postMessage` / `pdfObject.messageHandler`

Este método es la forma estándar de comunicación con un PDFJavaScript de un HTML. La vista PdfTaskForm también se encarga del PDF plano y lo procesa claramente.

>[!NOTE]
>
>No se recomienda modificar el pdf.html / contenido de la vista PdfTaskForm.

## Nueva Forms HTML {#new-html-forms}

NewHTMLTaskForm View representa los nuevos formularios HTML.

Cuando un formulario XDP se procesa como HTML utilizando el paquete de formularios móviles implementado en CRX, también agrega `FormBridge`JavaScript para el formulario, que expone diferentes métodos para guardar y enviar datos de formulario.

Este JavaScript es diferente del mencionado en los PDF forms anteriores, pero tiene un propósito similar.

>[!NOTE]
>
>No se recomienda modificar el contenido de la vista NewHTMLTaskForm.

## Flex Forms y guías {#flex-forms-and-guides}

SwfTaskForm representa Flex Forms y las guías las procesan las Vistas HtmlTaskForm, respectivamente.

En el espacio de trabajo de AEM Forms, estas vistas se comunican con el SWF real que conforma el formulario/guía de flexión mediante un SWF intermedio presente en `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

La comunicación se produce mediante `swfObject.postMessage` / `window.flexMessageHandler`.

Este protocolo se define mediante la variable `WsNextAdapter.swf`. El `flexMessageHandlers`en el objeto window, los formularios SWF abiertos anteriormente se eliminan antes de agregar uno nuevo. La lógica también tiene en cuenta el cambio entre la pestaña del formulario y la pestaña del historial en la vista de detalles de la tarea. `WsNextAdapter.swf` se utiliza para realizar diversas acciones de formulario, como guardar o enviar.

>[!NOTE]
>
>No se recomienda modificar `WSNextAdapter.swf` o el contenido de la vista SwfTaskForm / HtmlTaskForm .

## Aplicaciones de terceros (por ejemplo, Gestión de Correspondencia) {#third-party-applications-for-example-correspondence-management}

Las aplicaciones de terceros se procesan mediante la vista ExtAppTaskForm.

**Comunicación de la aplicación de terceros al espacio de trabajo de AEM Forms**

El espacio de trabajo de AEM Forms escucha en `window.global.postMessage([Message],[Payload])`

[Mensaje] puede ser una cadena especificada como `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`en el `runtimeMap`. Las aplicaciones de terceros deben utilizar esta interfaz para notificar al espacio de trabajo de AEM Forms según sea necesario. El uso de esta interfaz es obligatorio, ya que el espacio de trabajo de AEM Forms debe saber que, cuando se envía la tarea, puede limpiar la ventana de tareas.

**Comunicación del espacio de trabajo de AEM Forms con aplicaciones de terceros**

Si los botones de acción directa del espacio de trabajo de AEM Forms están visibles, llama a `window.[External-App-Name].getMessage([Action])`, donde `[Action]` se lee desde el `routeActionMap`. La aplicación de terceros debe escuchar en esta interfaz y, a continuación, notificar al espacio de trabajo de AEM Forms a través del `postMessage ()` API.

Por ejemplo, una aplicación de Flex puede definir `ExternalInterface.addCallback('getMessage', listener)` para apoyar esta comunicación. Si la aplicación de terceros desea gestionar el envío de formularios mediante sus propios botones, debe especificar `hideDirectActions = true() in the runtimeMap` y puede omitir este oyente. Por lo tanto, esta construcción es opcional.

Puede obtener más información sobre la integración de aplicaciones de terceros con respecto a la Gestión de Correspondencia en [Integración de la gestión de correspondencia en el espacio de trabajo de AEM Forms](/help/forms/using/integrating-correspondence-management-html-workspace.md).
