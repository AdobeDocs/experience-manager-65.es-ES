---
title: Guardado automático de un formulario adaptable
seo-title: Auto-save an adaptive form
description: Puede configurar un formulario adaptable para que empiece a guardar automáticamente el contenido en función de un evento o de un intervalo de tiempo predefinido
seo-description: You can configure an adaptive form to automatically start saving the content based on an event or a pre-defined time-interval
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
feature: Adaptive Forms
exl-id: 948b2c12-895d-49e3-a943-d8fe87174fc4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 3%

---

# Guardado automático de un formulario adaptable {#auto-save-an-adaptive-form}

Puede configurar un formulario adaptable para que empiece a guardar automáticamente el contenido en función de un evento o un intervalo de tiempo predefinido. De forma predeterminada, el contenido de un formulario adaptable se guarda en una acción del usuario, como al pulsar el botón guardar. La opción de guardado automático es útil en:

* Guardar automáticamente el contenido para usuarios anónimos y con sesión iniciada
* Guardado del contenido de un formulario sin la intervención mínima del usuario
* Empezar a guardar contenido de un formulario basado en un suceso de usuario
* Guardar el contenido de un formulario repetidamente después de un intervalo de tiempo especificado

## Habilitar el guardado automático para un formulario adaptable {#enable-autosave-for-an-adaptive-form}

Para un formulario adaptable, la opción de guardado automático no está activada de forma predeterminada. Puede activar la opción de guardado automático desde el **Guardar automáticamente** en las propiedades de un formulario adaptable. La variable **Guardar automáticamente** también proporciona otras opciones de configuración. Realice los siguientes pasos para habilitar y configurar la opción de guardado automático para un formulario adaptable:

1. Para acceder a la sección de guardado automático de las propiedades, seleccione un componente y pulse ![nivel de campo](assets/field-level.png) > **[!UICONTROL Contenedor de formulario adaptable]** y, a continuación, toque ![cmppr](assets/cmppr.png).
1. En el **[!UICONTROL Guardar automáticamente]** sección, **[!UICONTROL Habilitar]** la opción guardar automáticamente.
1. En el **[!UICONTROL Evento de formulario adaptable]** especifique 1 o TRUE para comenzar a guardar automáticamente el formulario cuando se carga en el explorador. También se puede especificar una expresión condicional para un suceso, que cuando se activa y devuelve el valor &quot;True&quot;, comienza a guardar el contenido del formulario.
1. Especifique el Déclencheur. El guardado automático se activa según la configuración. Las opciones son las siguientes:

   * **[!UICONTROL Basado en el tiempo:]** Seleccione la opción para comenzar a guardar el contenido en función de un intervalo de tiempo específico.
   * **[!UICONTROL Basado en eventos:]** Seleccione la opción para comenzar a guardar el contenido en función de cuándo se activa un evento.

   Cuando selecciona un déclencheur, se activa el cuadro Configuración de estrategia . El cuadro Configuración de estrategia le permite:

   * Especifique un intervalo de tiempo si selecciona **[!UICONTROL Basado en el tiempo]** déclencheur.
   * Especifique un nombre de evento si selecciona **[!UICONTROL Basado en eventos]** déclencheur.

   También puede crear y agregar su propia estrategia personalizada a la lista. Para obtener más información, consulte [Implementar una estrategia personalizada para guardar automáticamente los formularios](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. (Solo guardado automático basado en el tiempo) Realice los siguientes pasos para configurar las opciones de guardado automático basado en el tiempo.

   1. En el **[!UICONTROL Guardar automáticamente en este intervalo]** especifique el intervalo de tiempo en segundos. El formulario se guarda repetidamente después de que transcurra el número de segundos especificado en el cuadro de intervalo.

1. (Solo guardado automático basado en eventos) Realice los siguientes pasos para configurar las opciones de guardado automático basado en eventos.

   1. En la **Guardar automáticamente después de este evento** , especifique un [GuideBridge](https://helpx.adobe.com/es/aem-forms/6/javascript-api/GuideBridge.html) evento. El formulario se guarda cada vez que la expresión se evalúa como TRUE.

1. (Opcional) Para guardar automáticamente el contenido para usuarios anónimos, seleccione la opción **Habilitar el guardado automático para usuarios anónimos** y haga clic en **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Para que la opción de guardado automático funcione para usuarios anónimos, asegúrese de configurar el servicio de configuración común de Forms para permitir que todos los usuarios puedan obtener una vista previa, verificar y firmar formularios.
   >
   >Para configurar el servicio, vaya a AEM configuración de la consola web en `https://server:port/system/console/configMgr` y edite el **[!UICONTROL Servicio de configuración común de Forms]** para elegir **[!UICONTROL Todos los usuarios]** en la **[!UICONTROL Permitir]** y guarde la configuración.

## Implementar una estrategia personalizada para habilitar el guardado automático para formularios adaptables {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

Puede implementar un evento personalizado para almacenar en déclencheur la funcionalidad de guardado automático. Siga estos pasos para crear e implementar el evento personalizado:

1. Cree carpetas de biblioteca de cliente y de biblioteca de cliente. Para ver los pasos detallados, consulte la [Uso del documento de bibliotecas del lado del cliente](/help/sites-developing/clientlibs.md).

   Por ejemplo, la siguiente secuencia de comandos utiliza la variable `emailFocusChange`para almacenar en déclencheur la funcionalidad de guardado automático:

   ```javascript
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
   >Se define una propiedad category al crear las carpetas de la biblioteca cliente. Mantenga a mano el valor asignado a la propiedad category .

1. Abra el formulario adaptable en modo de autor.

1. En el modo de edición, seleccione un componente y, a continuación, pulse ![field-level](assets/field-level.png) > **[!UICONTROL Contenedor de formulario adaptable]** y haga clic en ![cmppr](assets/cmppr.png).
1. En las propiedades, abra la **[!UICONTROL Básico]** para obtener más información. En el **[!UICONTROL Categoría de la biblioteca del cliente]** , introduzca el valor de la propiedad category definida al crear las carpetas de la biblioteca cliente.
1. Abra la sección Guardar automáticamente . En el **[!UICONTROL Guardar automáticamente después de este evento]** especifique un evento personalizado ya definido en la biblioteca de cliente. Haga clic en **[!UICONTROL Aceptar]**.
