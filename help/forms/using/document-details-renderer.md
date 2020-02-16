---
title: Detalles del documento para el procesador
seo-title: Detalles del documento para el procesador
description: Información conceptual sobre cómo funcionan los procesamientos en el espacio de trabajo de AEM Forms para procesar los distintos tipos de archivo y formulario admitidos.
seo-description: Información conceptual sobre cómo funcionan los procesamientos en el espacio de trabajo de AEM Forms para procesar los distintos tipos de archivo y formulario admitidos.
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Detalles del documento para el procesador {#document-details-for-renderer}

## Introducción {#introduction}

En el espacio de trabajo de AEM Forms, se admiten varios tipos de formularios sin problemas. Entre estas características se incluyen:

* Formularios PDF (XDP/Acroform/PDF planos)
* Nuevos formularios HTML
* Imágenes
* Aplicaciones de terceros (por ejemplo, Administración de correspondencia)

Este documento explica el trabajo de estos procesadores desde la perspectiva de la personalización semántica / reutilización de componentes, de modo que los requisitos del cliente se cumplan sin romper ninguna representación. Aunque el espacio de trabajo de AEM Forms permite cualquier cambio semántico o de interfaz de usuario, se recomienda no cambiar la lógica de representación de distintos tipos de formularios; de lo contrario, los resultados pueden ser impredecibles. Este documento sirve para obtener instrucciones y conocimientos que permiten procesar el mismo formulario, utilizando los mismos componentes de espacio de trabajo en distintos portales, y no para modificar la lógica de procesamiento en sí.

## Formularios PDF {#pdf-forms}

Los formularios PDF son procesados por `PdfTaskForm View`.

Cuando un formulario XDP se procesa como PDF, el servicio FormsAugmenter agrega un `FormBridge` JavaScript™. Este JavaScript™ (dentro del formulario PDF) ayuda a realizar acciones como enviar formularios, guardarlos o desconectarlos.

En el espacio de trabajo de AEM Forms, la vista PDFTaskForm se comunica con `FormBridge`javascript mediante un HTML intermedio presente en `/lc/libs/ws/libs/ws/pdf.html`. El flujo es:

**Vista PDFTaskForm - pdf.html**

Se comunica mediante `window.postMessage` / `window.attachEvent('message')`

Este método es la forma estándar de comunicación entre un marco principal y un iframe. Los oyentes de eventos existentes de los formularios PDF abiertos anteriormente se eliminan antes de agregar uno nuevo. Esta depuración también tiene en cuenta el cambio entre la ficha de formulario y la ficha de historial en la vista de detalles de la tarea.

**pdf.html:`FormBridge`javascript dentro del PDF procesado**

Se comunica mediante `pdfObject.postMessage` / `pdfObject.messageHandler`

Este método es la forma estándar de comunicación con un javascript PDF desde un HTML. La vista PdfTaskForm también se ocupa de los archivos PDF planos y los procesa de forma sencilla.

>[!NOTE]
>
>No se recomienda modificar el contenido de la vista PdfTaskForm en pdf.html.

## Nuevos formularios HTML {#new-html-forms}

Los nuevos formularios HTML son procesados por la vista NewHTMLTaskForm.

Cuando un formulario XDP se procesa como HTML mediante el paquete de formularios móviles implementado en CRX, también agrega `FormBridge` javascript adicional al formulario, que expone diferentes métodos para guardar y enviar datos de formulario.

Este javascript es diferente del que se menciona en Formularios PDF, pero tiene un propósito similar.

>[!NOTE]
>
>No se recomienda modificar el contenido de la vista NewHTMLTaskForm.

## Formularios y guías de Flex {#flex-forms-and-guides}

SwfTaskForm procesa los formularios Flex y las guías las procesan las vistas HtmlTaskForm respectivamente.

En el espacio de trabajo de AEM Forms, estas vistas se comunican con el SWF real que conforma el formulario/guía flexible mediante un SWF intermedio presente en `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

La comunicación se produce usando `swfObject.postMessage` / `window.flexMessageHandler`.

Este protocolo está definido por el `WsNextAdapter.swf`. El objeto `flexMessageHandlers`de ventana existente, de formularios SWF previamente abiertos, se elimina antes de agregar uno nuevo. La lógica también tiene en cuenta el cambio entre la ficha de formulario y la ficha de historial en la vista de detalles de la tarea. `WsNextAdapter.swf` se utiliza para realizar varias acciones de formulario como guardar o enviar.

>[!NOTE]
>
>No se recomienda modificar `WSNextAdapter.swf` ni el contenido de la vista SwfTaskForm / HtmlTaskForm.

## Aplicaciones de terceros (por ejemplo, Administración de correspondencia) {#third-party-applications-for-example-correspondence-management}

Las aplicaciones de terceros se representan mediante la vista ExtAppTaskForm.

**Comunicación de la aplicación de terceros al espacio de trabajo de AEM Forms**

El espacio de trabajo de AEM Forms escucha en `window.global.postMessage([Message],[Payload])`

[]`SubmitMessage``CancelMessage`El mensaje`ErrorMessage` puede ser una cadena especificada como||| `actionEnabledMessage`en el `runtimeMap`. Las aplicaciones de terceros deben utilizar esta interfaz para notificar al espacio de trabajo de AEM Forms según sea necesario. El uso de esta interfaz es obligatorio, ya que el espacio de trabajo de AEM Forms debe saber que, cuando se envía la tarea, puede limpiar la ventana de tareas.

**Espacio de trabajo de AEM Forms para comunicación con aplicaciones de terceros**

Si los botones de acción directa del espacio de trabajo de AEM Forms están visibles, llama `window.[External-App-Name].getMessage([Action])`, donde [ `Action]` se lee desde el `routeActionMap`. La aplicación de terceros debe escuchar esta interfaz y, a continuación, notificar el espacio de trabajo de AEM Forms mediante la `postMessage ()` API.

Por ejemplo, una aplicación Flex puede definir `ExternalInterface.addCallback('getMessage', listener)` para admitir esta comunicación. Si la aplicación de terceros desea gestionar el envío de formularios mediante sus propios botones, debe especificarlo `hideDirectActions = true() in the runtimeMap` y puede omitir este detector. Por lo tanto, esta construcción es opcional.

Puede leer más sobre la integración de aplicaciones de terceros con respecto a la gestión de correspondencia en [Integración de la gestión de correspondencia en el espacio de trabajo](/help/forms/using/integrating-correspondence-management-html-workspace.md)de AEM Forms.


[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
