---
title: Detalles de documento para el procesador
seo-title: Detalles de documento para el procesador
description: Información conceptual sobre cómo funcionan los procesamientos en el espacio de trabajo de AEM Forms para procesar los distintos tipos de archivo y formulario admitidos.
seo-description: Información conceptual sobre cómo funcionan los procesamientos en el espacio de trabajo de AEM Forms para procesar los distintos tipos de archivo y formulario admitidos.
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# Detalles de documento para el procesador {#document-details-for-renderer}

## Introducción {#introduction}

En el espacio de trabajo de AEM Forms, se admiten varios tipos de formularios sin problemas. Entre estas características se incluyen:

* PDF forms (XDP/Acroform/PDF planos)
* Nuevos formularios HTML
* Imágenes
* Aplicaciones de terceros (por ejemplo, Administración de correspondencia)

Este documento explica el trabajo de estos procesadores desde la perspectiva de la personalización semántica / reutilización de componentes, de modo que los requisitos del cliente se cumplan sin romper ninguna representación. Aunque el espacio de trabajo de AEM Forms permite cualquier cambio semántico/de interfaz de usuario, se recomienda no cambiar la lógica de procesamiento de los distintos tipos de formularios, de lo contrario los resultados pueden ser impredecibles. Este documento es para guía / conocimiento que permite procesar el mismo formulario, utilizando los mismos componentes de espacio de trabajo en diferentes portales, y no para modificar la lógica de procesamiento en sí.

## PDF forms {#pdf-forms}

Los PDF forms se representan con `PdfTaskForm View`.

Cuando un formulario XDP se procesa como PDF, el servicio FormsAugmenter agrega un `FormBridge` JavaScript™. Este JavaScript™ (dentro del formulario PDF) ayuda a realizar acciones como enviar formularios, guardarlos o desconectarlos.

En el espacio de trabajo de AEM Forms, la vista PDFTaskForm se comunica con `FormBridge`javascript mediante un HTML intermedio presente en `/lc/libs/ws/libs/ws/pdf.html`. El flujo es:

**VISTA PDFTaskForm - pdf.html**

Se comunica mediante `window.postMessage` / `window.attachEvent('message')`

Este método es la forma estándar de comunicación entre un marco principal y un iframe. Los oyentes de evento existentes de PDF forms abiertos anteriormente se eliminan antes de agregar uno nuevo. Esta depuración también tiene en cuenta el cambio entre la ficha de formulario y la ficha de historial en la vista de detalles de tarea.

**pdf.html:  `FormBridge`javascript dentro del PDF procesado**

Se comunica mediante `pdfObject.postMessage` / `pdfObject.messageHandler`

Este método es la forma estándar de comunicación con un PDFJavaScript desde un HTML. La vista PdfTaskForm también se encarga de los archivos PDF planos y los procesa con claridad.

>[!NOTE]
>
>No se recomienda modificar el contenido de la vista pdf.html / de PdfTaskForm.

## Nuevo Forms HTML {#new-html-forms}

Los nuevos formularios HTML son procesados por la Vista NewHTMLTaskForm.

Cuando un formulario XDP se procesa como HTML mediante el paquete de formularios móviles implementado en CRX, también agrega `FormBridge`JavaScript adicional al formulario, que expone diferentes métodos para guardar y enviar datos de formulario.

Este JavaScript es diferente del mencionado en los PDF forms anteriores, pero tiene un propósito similar.

>[!NOTE]
>
>No se recomienda modificar el contenido de la vista NewHTMLTaskForm.

## Flex Forms y Guías {#flex-forms-and-guides}

SwfTaskForm representa Flex Forms y las guías las Vistas HtmlTaskForm respectivamente.

En el espacio de trabajo de AEM Forms, estas vistas se comunican con el SWF real que conforma el formulario/guía flexible mediante un SWF intermedio que se encuentra en `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

La comunicación se produce utilizando `swfObject.postMessage` / `window.flexMessageHandler`.

Este protocolo está definido por `WsNextAdapter.swf`. El objeto `flexMessageHandlers`existente en la ventana, de los formularios SWF previamente abiertos, se elimina antes de agregar uno nuevo. La lógica también tiene en cuenta el cambio entre la ficha de formulario y la ficha de historial en la vista de detalles de tarea. `WsNextAdapter.swf` se utiliza para realizar varias acciones de formulario como guardar o enviar.

>[!NOTE]
>
>No se recomienda modificar `WSNextAdapter.swf` ni el contenido de la vista SwfTaskForm / HtmlTaskForm.

## Aplicaciones de terceros (por ejemplo, Administración de correspondencia) {#third-party-applications-for-example-correspondence-management}

Las aplicaciones de terceros se representan mediante la vista ExtAppTaskForm.

**Comunicación de aplicaciones de terceros al espacio de trabajo de AEM Forms**

El espacio de trabajo de AEM Forms escucha en `window.global.postMessage([Message],[Payload])`

[] Messageccan puede ser una cadena especificada como  `SubmitMessage`|  `CancelMessage`|  `ErrorMessage`|  `actionEnabledMessage`en el  `runtimeMap`. Las aplicaciones de terceros deben utilizar esta interfaz para notificar el espacio de trabajo de AEM Forms según sea necesario. El uso de esta interfaz es obligatorio, ya que el espacio de trabajo de AEM Forms debe saber que cuando se envía la tarea para que pueda limpiar la ventana de tarea.

**Comunicación del espacio de trabajo de AEM Forms con aplicaciones de terceros**

Si los botones de acción directa del espacio de trabajo de AEM Forms están visibles, llama a `window.[External-App-Name].getMessage([Action])`, donde `[Action]` se lee desde `routeActionMap`. La aplicación de terceros debe escuchar en esta interfaz y, a continuación, notificar al espacio de trabajo de AEM Forms mediante la API `postMessage ()`.

Por ejemplo, una aplicación de Flex puede definir `ExternalInterface.addCallback('getMessage', listener)` para admitir esta comunicación. Si la aplicación de terceros desea controlar el envío de formularios mediante sus propios botones, debe especificar `hideDirectActions = true() in the runtimeMap` y puede omitir este detector. Por lo tanto, esta construcción es opcional.

Puede leer más sobre la integración de aplicaciones de terceros con respecto a la Administración de correspondencia en [Integración de la Administración de correspondencia en el área de trabajo de AEM Forms](/help/forms/using/integrating-correspondence-management-html-workspace.md).
