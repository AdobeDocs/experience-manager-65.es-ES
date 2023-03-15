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
ht-degree: 100%

---

# Guardado automático de un formulario adaptable {#auto-save-an-adaptive-form}

Puede configurar un formulario adaptable para que empiece a guardar automáticamente el contenido en función de un evento o un intervalo de tiempo predefinido. De forma predeterminada, el contenido de un formulario adaptable se guarda con una acción del usuario, como al pulsar el botón guardar. La opción de guardado automático es útil para lo siguiente:

* Guardar automáticamente el contenido para usuarios anónimos y con sesión iniciada
* Guardar el contenido de un formulario sin la intervención mínima del usuario
* Empezar a guardar contenido de un formulario basado en un evento de usuario
* Guardar el contenido de un formulario repetidamente después de un intervalo de tiempo especificado

## Habilitar el guardado automático para un formulario adaptable {#enable-autosave-for-an-adaptive-form}

Para un formulario adaptable, la opción de guardado automático no está activada de forma predeterminada. Puede activar la opción de guardado automático desde la sección **Guardar automáticamente** en las propiedades de un formulario adaptable. La sección **Guardar automáticamente** también proporciona otras opciones de configuración. Realice los siguientes pasos para habilitar y configurar la opción de guardado automático para un formulario adaptable:

1. Para acceder a la sección de guardado automático de las propiedades, seleccione un componente y pulse ![field-level](assets/field-level.png) > **[!UICONTROL Contenedor del formulario adaptable]** y, a continuación, pulse ![cmppr](assets/cmppr.png).
1. En la sección **[!UICONTROL Guardar automáticamente]**, **[!UICONTROL habilite]** la opción Guardar automáticamente.
1. En el cuadro **[!UICONTROL Evento de formulario adaptable]** especifique 1 o TRUE para comenzar a guardar automáticamente el formulario cuando se cargue en el explorador. También se puede especificar una expresión condicional para un evento, que cuando se activa y devuelve el valor “True”, comienza a guardar el contenido del formulario.
1. Especifique el Activador. El guardado automático se activará según la configuración. Las opciones son las siguientes:

   * **[!UICONTROL En base a tiempo:]** seleccione esta opción para comenzar a guardar el contenido en función de un intervalo de tiempo específico.
   * **[!UICONTROL En base a eventos:]** seleccione esta opción para comenzar a guardar el contenido en función de cuándo se activa un evento.

   Cuando selecciona un activador, se activará el cuadro Configuración de estrategia. El cuadro Configuración de estrategia le permite:

   * Especificar un intervalo de tiempo si selecciona el activador **[!UICONTROL En base a tiempo]**.
   * Especificar un nombre de evento si selecciona el activador **[!UICONTROL En base a eventos]**.

   También puede crear y agregar estrategias personalizadas a la lista. Para obtener más información, consulte [Implementar una estrategia personalizada para guardar automáticamente los formularios](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. (Solo guardado automático en base a tiempo) Realice los siguientes pasos para configurar las opciones de guardado automático en base a tiempo.

   1. En el cuadro **[!UICONTROL Guardar automáticamente en este intervalo]** especifique el intervalo de tiempo en segundos. El formulario se guarda repetidamente después de que transcurra el número de segundos especificado en el cuadro de intervalo.

1. (Solo guardado automático basado en eventos) Realice los siguientes pasos para configurar las opciones de guardado automático en base a eventos.

   1. En el cuadro **Guardar automáticamente después de este evento**, especifique un evento [GuideBridge](https://helpx.adobe.com/es/aem-forms/6/javascript-api/GuideBridge.html). El formulario se guardará cada vez que la expresión se evalúe como TRUE.

1. (Opcional) Para guardar automáticamente el contenido para usuarios anónimos, seleccione la opción **Habilitar el guardado automático para usuarios anónimos** y haga clic en **[!UICONTROL Aceptar]**.

   >[!NOTE]
   >
   >Para que la opción de guardado automático funcione para usuarios anónimos, asegúrese de configurar el servicio de configuración común de Forms para permitir que todos los usuarios puedan obtener una vista previa, comprobar y firmar formularios.
   >
   >Para configurar el servicio, vaya a la configuración de la consola web de AEM en `https://server:port/system/console/configMgr` y edite el **[!UICONTROL Servicio de configuración común de Forms]** para elegir la opción **[!UICONTROL Todos los usuarios]** en el campo **[!UICONTROL Permitir]** y guarde la configuración.

## Implementar una estrategia personalizada para habilitar el guardado automático para formularios adaptables {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

Puede implementar un evento personalizado para habilitar la funcionalidad de guardado automático. Siga estos pasos para crear e implementar el evento personalizado:

1. Cree una biblioteca de cliente y carpetas de la biblioteca de cliente. Para ver los pasos detallados, consulte el documento [Usar el documento de bibliotecas del lado del cliente](/help/sites-developing/clientlibs.md).

   Por ejemplo, el siguiente script utiliza el evento personalizado `emailFocusChange` para habilitar la funcionalidad de guardado automático:

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
   >Se define una propiedad category al crear las carpetas de la biblioteca cliente. Mantenga a mano el valor asignado a la propiedad category.

1. Abra el formulario adaptable en el modo de autor.

1. En el modo de edición, seleccione un componente y, a continuación, pulse ![field-level](assets/field-level.png) > **[!UICONTROL Contenedor de formulario adaptable]** y haga clic en ![cmppr](assets/cmppr.png).
1. En las propiedades, abra la sección **[!UICONTROL Básico]**. En el cuadro **[!UICONTROL Categoría de la biblioteca del cliente]**, escriba el valor de la propiedad category definida al crear las carpetas de la biblioteca cliente.
1. Abra la sección Guardar automáticamente. En el cuadro **[!UICONTROL Guardar automáticamente después de este evento]** especifique un evento personalizado ya definido en la biblioteca de cliente. Haga clic en **[!UICONTROL Aceptar]**.
