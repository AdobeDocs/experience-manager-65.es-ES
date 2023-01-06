---
title: Detalles del documento para el procesador
seo-title: Document details for renderer
description: Información conceptual sobre cómo funcionan los procesamientos en AEM Forms Workspace para procesar los distintos tipos de formularios y archivos admitidos.
seo-description: Conceptual information on how renders work in AEM Forms workspace to render the various supported form and file types.
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '653'
ht-degree: 100%

---

# Detalles del documento para el procesador {#document-details-for-renderer}

## Introducción {#introduction}

En AEM Forms Workspace, se admiten varios tipos de formularios. Entre estas características se incluyen:

* Formularios PDF (XDP/Acroform/PDF aplanados)
* Nuevos formularios HTML
* Imágenes
* Aplicaciones de terceros (por ejemplo, Administración de correspondencia)

Este documento explica el trabajo de estos procesadores desde la perspectiva de la personalización semántica / reutilización de componentes, de modo que los requisitos del cliente se cumplan sin romper ninguna representación. Aunque AEM Forms Workspace permite cualquier cambio semántico/de interfaz de usuario, se recomienda que no se cambie la lógica de procesamiento de distintos tipos de formulario; de lo contrario, los resultados pueden ser impredecibles. El propósito de este documento es para orientación / conocimiento para admitir el procesamiento del mismo formulario, mediante el uso de los mismos componentes de espacio de trabajo en diferentes portales y no para modificar la propia lógica de procesamiento.

## Formularios PDF {#pdf-forms}

Los formularios PDF son procesados por `PdfTaskForm View`.

Cuando se procesa un formulario XDP como PDF, el servicio FormsAugmenter agrega un `FormBridge` JavaScript™. Este JavaScript™ (dentro del formulario PDF) ayuda a realizar acciones como enviar, guardar o quitar formularios sin conexión.

En AEM Forms Workspace, la vista PDFTaskForm se comunica con el javaScript `FormBridge`, a través de un HTML intermedio presente en `/lc/libs/ws/libs/ws/pdf.html`. El flujo es:

**Vista de PDFTaskForm: pdf.html**

Se comunica mediante `window.postMessage` / `window.attachEvent('message')`

Este método es la forma estándar de comunicación entre un marco principal y un iframe. Los oyentes de eventos existentes de los formularios PDF abiertos anteriormente se quitan antes de agregar uno nuevo. Esta depuración también tiene en cuenta el cambio entre la pestaña del formulario y la del historial en la vista de detalles de la tarea.

**pdf.html: `FormBridge` javascript dentro del PDF representado**

Se comunica mediante `pdfObject.postMessage` / `pdfObject.messageHandler`

Este método es la forma estándar de comunicación con un PDFJavaScript de un HTML. La vista PdfTaskForm también se encarga del PDF aplanado y lo procesa claramente.

>[!NOTE]
>
>No se recomienda modificar el pdf.html / contenido de la vista PdfTaskForm.

## Nuevos formularios HTML {#new-html-forms}

La vista de NewHTMLTaskForm representa los nuevos formularios HTML.

Cuando un formulario XDP se procesa como HTML mediante el paquete de formularios móviles implementado en CRX, también agrega `FormBridge` JavaScript para el formulario, que expone diferentes métodos para guardar y enviar datos de formulario.

Este JavaScript es diferente del mencionado en los formularios PDF anteriores, pero tiene un propósito similar.

>[!NOTE]
>
>No se recomienda modificar el contenido de la vista de NewHTMLTaskForm.

## Formularios Flex y guías {#flex-forms-and-guides}

SwfTaskForm procesa los formularios Flex, y las vistas de HtmlTaskFormlas procesan las guías, respectivamente.

En AEM Forms Workspace, estas vistas se comunican con el SWF real que conforma el formulario/guía Flex mediante un SWF intermedio presente en `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

La comunicación se produce mediante `swfObject.postMessage` / `window.flexMessageHandler`.

Este protocolo se define mediante `WsNextAdapter.swf`. Los `flexMessageHandlers` existentes en el objeto window, de los formularios SWF abiertos previamente se quitan antes de agregar uno nuevo. La lógica también tiene en cuenta el cambio entre la pestaña del formulario y la del historial en la vista de detalles de la tarea. `WsNextAdapter.swf` se utiliza para realizar diversas acciones de formulario, como guardar o enviar.

>[!NOTE]
>
>No se recomienda modificar `WSNextAdapter.swf` o el contenido de la vista de SwfTaskForm / HtmlTaskForm.

## Aplicaciones de terceros (por ejemplo, Administración de correspondencia) {#third-party-applications-for-example-correspondence-management}

Las aplicaciones de terceros se procesan mediante la vista de ExtAppTaskForm.

**Comunicación de la aplicación de terceros con AEM Forms Workspace**

El espacio de trabajo de AEM Forms escucha en `window.global.postMessage([Message],[Payload])`

[El mensaje] puede ser una cadena especificada como `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`en el `runtimeMap`. Las aplicaciones de terceros deben utilizar esta interfaz para notificar al espacio de trabajo de AEM Forms según sea necesario. El uso de esta interfaz es obligatorio, ya que AEM Forms Workspace debe saber que, cuando se envía la tarea, puede limpiar la ventana de tareas.

**Comunicación de AEM Forms Workspace con aplicaciones de terceros**

Si los botones de acción directa de AEM Forms Workspace están visibles, llama a `window.[External-App-Name].getMessage([Action])`, donde `[Action]` se lee desde el `routeActionMap`. La aplicación de terceros debe escuchar en esta interfaz y, a continuación, notificar al espacio de trabajo de AEM Forms a través de la API `postMessage ()`.

Por ejemplo, una aplicación de Flex puede definir `ExternalInterface.addCallback('getMessage', listener)` para apoyar esta comunicación. Si la aplicación de terceros desea administrar el envío de formularios mediante sus propios botones, debe especificar `hideDirectActions = true() in the runtimeMap` y puede omitir este oyente. Por lo tanto, esta construcción es opcional.

Puede obtener más información sobre la integración de aplicaciones de terceros con respecto a Administración de correspondencia en [Integración de Administración de correspondencia en AEM Forms Workspace](/help/forms/using/integrating-correspondence-management-html-workspace.md).
