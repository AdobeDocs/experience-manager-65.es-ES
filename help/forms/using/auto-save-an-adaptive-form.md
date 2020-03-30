---
title: Guardado automático de un formulario adaptable
seo-title: Guardado automático de un formulario adaptable
description: Puede configurar un formulario adaptable para que guarde automáticamente en inicio el contenido en función de un evento o un intervalo de tiempo predefinido
seo-description: Puede configurar un formulario adaptable para que guarde automáticamente en inicio el contenido en función de un evento o un intervalo de tiempo predefinido
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Guardado automático de un formulario adaptable {#auto-save-an-adaptive-form}

Puede configurar un formulario adaptable para que guarde automáticamente en inicio el contenido en función de un evento o un intervalo de tiempo predefinido. De forma predeterminada, el contenido de un formulario adaptable se guarda en una acción del usuario, como al pulsar el botón Guardar. La opción de guardado automático es útil en:

* Guardar automáticamente el contenido para usuarios anónimos e iniciados en sesión
* Guardado del contenido de un formulario sin la intervención mínima del usuario
* Inicio para guardar el contenido de un formulario basado en un evento de usuario
* Guardar el contenido de un formulario repetidamente después de un intervalo de tiempo especificado

## Habilitar el guardado automático para un formulario adaptable {#enable-autosave-for-an-adaptive-form}

Para un formulario adaptable, la opción de guardado automático no está activada de forma predeterminada. Puede activar la opción de guardado automático desde la sección Guardar **** automáticamente en las propiedades de un formulario adaptable. La sección Guardado **** automático también ofrece otras opciones de configuración. Realice los siguientes pasos para habilitar y configurar la opción de guardado automático para un formulario adaptable:

1. Para acceder a la sección de guardado automático de las propiedades, seleccione un componente, toque ![campo](assets/field-level.png) > Contenedor **[!UICONTROL de formulario]** adaptable y, a continuación, toque ![cmppr](assets/cmppr.png).
1. En la sección Guardar **** automáticamente, **[!UICONTROL active]** la opción de guardar automáticamente.
1. En el cuadro Evento **[!UICONTROL de formulario]** adaptable, especifique 1 o VERDADERO para guardar automáticamente el formulario cuando se cargue en el explorador con inicio. También puede especificar una expresión condicional para un evento, que cuando se activa y devuelve verdadero, inicios que guardan el contenido del formulario.
1. Especifique el activador. El guardado automático se activa según la configuración. Sus opciones son:

   * **[!UICONTROL Basado en el tiempo:]** Seleccione la opción para guardar en inicio el contenido según un intervalo de tiempo específico.
   * **[!UICONTROL Basado en Evento:]** Seleccione la opción para guardar en inicio el contenido en función de cuándo se activa un evento.
   Al seleccionar un activador, se activa el cuadro Configuración de estrategia. El cuadro Configuración de estrategia permite:

   * Especifique un intervalo de tiempo si selecciona un activador basado en **[!UICONTROL tiempo]** .
   * Especifique un nombre de evento si selecciona un activador basado en **[!UICONTROL Eventos]** .
   También puede crear y agregar su propia estrategia personalizada a la lista. Para obtener más información, consulte [Implementación de una estrategia personalizada para guardar automáticamente los formularios](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. (Solo guardado automático basado en el tiempo) Realice los siguientes pasos para configurar las opciones de guardado automático basado en el tiempo.

   1. En el cuadro Guardar **[!UICONTROL automáticamente en este intervalo]** , especifique el intervalo de tiempo en segundos. El formulario se guarda repetidamente después de que transcurra el número de segundos especificado en el cuadro de intervalo.

1. (Solo guardado automático basado en Eventos) Realice los siguientes pasos para configurar las opciones de guardado automático basado en Eventos.

   1. En el cuadro Guardar **automáticamente después de este evento** , especifique un evento de [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) . El formulario se guarda cada vez que la expresión se evalúa como VERDADERA.

1. (Opcional) Para guardar automáticamente el contenido para usuarios anónimos, seleccione la opción **Activar guardado automático para usuarios** anónimos y haga clic en **[!UICONTROL Aceptar]**.

   >[!NOTE]
   >
   >Para que la opción de guardado automático funcione para usuarios anónimos, asegúrese de configurar el servicio de configuración común de formularios para permitir que todos los usuarios realicen la previsualización, la comprobación y la firma de formularios.
   >
   >Para configurar el servicio, vaya a la configuración de la consola web de AEM en `https://server:port/system/console/configMgr` y edite el servicio **[!UICONTROL de configuración común de]** Forms para elegir la opción **[!UICONTROL Todos los usuarios]** en el campo **[!UICONTROL Permitir]** y guardar la configuración.

## Implementar una estrategia personalizada para permitir el guardado automático en formularios adaptables {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

Puede implementar un evento personalizado para activar la funcionalidad de guardado automático. Realice los siguientes pasos para crear e implementar el evento personalizado:

1. Cree carpetas de biblioteca de cliente y de biblioteca de cliente. Para ver los pasos detallados, consulte el documento [](/help/sites-developing/clientlibs.md)Uso de bibliotecas del lado del cliente.

   Por ejemplo, la siguiente secuencia de comandos utiliza el `emailFocusChange`evento personalizado para activar la funcionalidad de guardado automático:

   ```
   window.addEventListener("bridgeInitializeStart", function (){
       guideBridge.connect(function () { guideBridge.on("elementFocusChanged", function (event,data) {
           if(data.target.name === 'Email') {
               guideBridge.trigger("emailFocusChange");
           }
       });
      });
   });
   ```

   >[!NOTE]
   >
   >Se define una propiedad de categoría al crear las carpetas de la biblioteca del cliente. Mantenga a mano el valor asignado a la propiedad categoría.

1. Abra el formulario adaptable en modo de autor.

1. En el modo de edición, seleccione un componente, toque ![campo](assets/field-level.png) > Contenedor **[!UICONTROL de formulario]** adaptable y, a continuación, toque ![cmppr](assets/cmppr.png).
1. En las propiedades, abra la sección **[!UICONTROL Básico]** . En el cuadro Categoría **[!UICONTROL de la biblioteca de]** clientes, introduzca el valor de la propiedad de categoría definida al crear las carpetas de la biblioteca de clientes.
1. Abra la sección Guardado automático. En el cuadro Guardar **[!UICONTROL automáticamente después de este evento]** , especifique un evento personalizado ya definido en la biblioteca del cliente. Haga clic en **[!UICONTROL Aceptar]**.

