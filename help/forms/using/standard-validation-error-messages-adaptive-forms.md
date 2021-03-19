---
title: Mensajes de error de validación estándar para formularios adaptables
seo-title: Mensajes de error de validación estándar para formularios adaptables
description: Transformar los mensajes de error de validación para formularios adaptables al formato estándar mediante controladores de error personalizados
seo-description: Transformar los mensajes de error de validación para formularios adaptables al formato estándar mediante controladores de error personalizados
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
feature: Formularios adaptables
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 0%

---


# Mensajes de error de validación estándar para formularios adaptables {#standard-validation-error-messages}

Los formularios adaptables validan las entradas que se proporcionan en los campos en función de criterios de validación predefinidos. Los criterios de validación hacen referencia a los valores de entrada aceptables para los campos de un formulario adaptable. Puede definir los criterios de validación en función del origen de datos que utilice con el formulario adaptable. Por ejemplo, si utiliza los servicios web RESTful como fuente de datos, puede definir los criterios de validación en un archivo de definición Swagger.

Si los valores de entrada cumplen los criterios de validación, los valores se envían al origen de datos. De lo contrario, el formulario adaptable muestra un mensaje de error.

De forma similar a este enfoque, los formularios adaptables ahora se pueden integrar con servicios personalizados para realizar validaciones de datos. Si los valores de entrada no cumplen los criterios de validación y el mensaje de error de validación que devuelve el servidor está en el formato de mensaje estándar, los mensajes de error se muestran en el formulario a nivel de campo.

Si los valores de entrada no cumplen los criterios de validación y el mensaje de error de validación del servidor no está en el formato de mensaje estándar, los formularios adaptables proporcionan un mecanismo para transformar los mensajes de error de validación en un formato estándar para que se muestren en el campo del formulario. Puede transformar el mensaje de error en el formato estándar utilizando cualquiera de los dos métodos siguientes:

* Agregar controlador de error personalizado en el envío de formulario adaptable
* Agregar un controlador personalizado a la acción Invocar servicio mediante el Editor de reglas

En este artículo se describe el formato estándar para los mensajes de error de validación y las instrucciones para transformar los mensajes de error de un formato personalizado a un formato estándar.

## Formato de mensaje de error de validación estándar {#standard-validation-message-format}

Los formularios adaptables muestran los errores en el nivel de campo si los mensajes de error de validación del servidor tienen el siguiente formato estándar:

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             somExpression  : <somexpr>
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]

        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
}
```

Donde:

* `errorCausedBy` describe el motivo del error
* `errors` mencione la expresión SOM de los campos en los que se han producido errores en los criterios de validación junto con el mensaje de error de validación
* `originCode` contiene el código de error devuelto por el servicio externo
* `originMessage` contiene los datos de error sin procesar devueltos por el servicio externo

## Configurar el envío de formularios adaptables para agregar controladores personalizados {#configure-adaptive-form-submission}

Si el mensaje de error de validación del servidor no se muestra en el formato estándar, puede habilitar el envío asincrónico y agregar un controlador de error personalizado en el envío del formulario adaptable para convertir el mensaje en un formato estándar.

### Configurar el envío asincrónico de formularios adaptables {#configure-asynchronous-adaptive-form-submission}

Antes de añadir el controlador personalizado, debe configurar el formulario adaptable para el envío asincrónico. Siga estos pasos:

1. En el modo de creación de formularios adaptables, seleccione el objeto Contenedor de formulario y pulse ![propiedades de formulario adaptables](assets/configure_icon.png) para abrir sus propiedades.
1. En la sección **[!UICONTROL Submission]** properties , habilite **[!UICONTROL Usar envío asincrónico]**.
1. Seleccione **[!UICONTROL Revalidate on server]** para validar los valores de los campos de entrada en el servidor antes del envío.
1. Seleccione Enviar acción:

   * Seleccione **[!UICONTROL Enviar con el Modelo de datos de formulario]** y seleccione el modelo de datos adecuado si utiliza el modelo de datos de formulario [basado en el servicio web RESTful](work-with-form-data-model.md) como origen de datos.
   * Seleccione **[!UICONTROL Submit to REST endpoint]** y especifique el **[!UICONTROL Redirect URL/Path]** si utiliza los servicios web RESTful como fuente de datos.

   ![propiedades de envío de formulario adaptable](assets/af_submission_properties.png)

1. Toque ![Guardar](assets/save_icon.png) para guardar las propiedades.

### Agregar controlador de error personalizado en el envío de formulario adaptable {#add-custom-error-handler-af-submission}

AEM Forms proporciona controladores de éxito y de errores listos para usar para los envíos de formularios. Los controladores son funciones del lado del cliente que se ejecutan en función de la respuesta del servidor. Cuando se envía un formulario, los datos se transmiten al servidor para su validación, lo que devuelve una respuesta al cliente con información sobre el suceso success o error del envío. La información se pasa como parámetros al controlador correspondiente para ejecutar la función.

Ejecute los siguientes pasos para agregar el controlador de error personalizado en el envío del formulario adaptable:

1. Abra el formulario adaptable en modo de creación, seleccione cualquier objeto de formulario y pulse <!--![Rule Editor](assets/af_edit_rules.png)--> para abrir el editor de reglas.
1. Seleccione **[!UICONTROL Formulario]** en el árbol de objetos de formulario y pulse **[!UICONTROL Crear]**.
1. Seleccione **[!UICONTROL Error en el envío]** en la lista desplegable Evento.
1. Escriba una regla para convertir la estructura de error personalizada a la estructura de error estándar y pulse **[!UICONTROL Listo]** para guardar la regla.

El siguiente es un código de ejemplo para convertir una estructura de error personalizada en la estructura de error estándar:

```javascript
var data = $event.data;
var som_map = {
    "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
    "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
    "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
};

var errorJson = {};
errorJson.errors = [];

if (data) {
    if (data.originMessage) {
        var errorData;
        try {
            errorData = JSON.parse(data.originMessage);
        } catch (err) {
            // not in json format
        }

        if (errorData) {
            Object.keys(errorData).forEach(function(key) {
                var som_key = som_map[key];
                if (som_key) {
                    var error = {};
                    error.somExpression = som_key;
                    error.errorMessage = errorData[key];
                    errorJson.errors.push(error);
                }
            });
        }
        window.guideBridge.handleServerValidationError(errorJson);
    } else {
        window.guideBridge.handleServerValidationError(data);
    }
}
```

La `var som_map` enumera la expresión SOM de los campos de formulario adaptables que desea transformar en el formato estándar. Puede ver la expresión SOM de cualquier campo en un formulario adaptable; para ello, pulse el campo y seleccione **[!UICONTROL View SOM Expression]**.

Con este controlador de error personalizado, el formulario adaptable convierte los campos enumerados en `var som_map` al formato de mensaje de error estándar. Como resultado, los mensajes de error de validación se muestran a nivel de campo en el formulario adaptable.

## Añadir un controlador personalizado mediante la acción Invocar servicio

Ejecute los siguientes pasos para agregar el controlador de error para convertir una estructura de error personalizada en la estructura de error estándar mediante la acción [Servicio de invocación del ](rule-editor.md) Editor de reglas:

1. Abra el formulario adaptable en modo de creación, seleccione cualquier objeto de formulario y pulse ![Editor de reglas](assets/rule_editor_icon.png) para abrir el editor de reglas.
1. Toque **[!UICONTROL Crear]**.
1. Cree una condición en la sección **[!UICONTROL When]** de la regla. Por ejemplo, cuando se cambia el nombre del campo[Name of field]. Seleccione **[!UICONTROL is changed]** en la lista desplegable **[!UICONTROL Select State]** para lograr esta condición.
1. En la sección **[!UICONTROL Then]**, seleccione **[!UICONTROL Invocar servicio]** en la lista desplegable **[!UICONTROL Seleccionar acción]**.
1. Seleccione un servicio Post y sus enlaces de datos correspondientes en la sección **[!UICONTROL Input]** . Por ejemplo, si desea validar los campos **Name**, **ID** y **Status** en el formulario adaptable, seleccione un servicio Post (pet) y seleccione pet.name, pet.id y pet.status en la sección **[!UICONTROL Input]**.

Como resultado de esta regla, los valores introducidos para los campos **Name**, **ID** y **Status** se validan en cuanto se cambia el campo definido en el paso 2 y se elimina el campo del formulario mediante tabulación.

1. Seleccione **[!UICONTROL Editor de código]** en la lista desplegable de selección de modo.
1. Toque **[!UICONTROL Editar código]**.
1. Elimine la línea siguiente del código existente:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. Escriba una regla para convertir la estructura de error personalizada a la estructura de error estándar y pulse **[!UICONTROL Listo]** para guardar la regla.
Por ejemplo, agregue el siguiente código de ejemplo al final para convertir una estructura de error personalizada en la estructura de error estándar:

   ```javascript
   var errorHandler = function(jqXHR, data) {
   var som_map = {
       "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
       "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
       "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
   };
   
   
   var errorJson = {};
   errorJson.errors = [];
   
   if (data) {
       if (data.originMessage) {
           var errorData;
           try {
               errorData = JSON.parse(data.originMessage);
           } catch (err) {
               // not in json format
           }
   
           if (errorData) {
               Object.keys(errorData).forEach(function(key) {
                   var som_key = som_map[key];
                   if (som_key) {
                       var error = {};
                       error.somExpression = som_key;
                       error.errorMessage = errorData[key];
                       errorJson.errors.push(error);
                   }
               });
           }
           window.guideBridge.handleServerValidationError(errorJson);
       } else {
           window.guideBridge.handleServerValidationError(data);
       }
     }
   };
   
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   La `var som_map` enumera la expresión SOM de los campos de formulario adaptables que desea transformar en el formato estándar. Puede ver la expresión SOM de cualquier campo en un formulario adaptable; para ello, pulse el campo y seleccione **[!UICONTROL View SOM Expression]** en el menú **[!UICONTROL More Options]** (...).

   Asegúrese de copiar la línea siguiente del código de ejemplo en el controlador de error personalizado:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   La API executeOperation incluye los parámetros `null` y `errorHandler` basados en el nuevo controlador de error personalizado.

   Con este controlador de error personalizado, el formulario adaptable convierte los campos enumerados en `var som_map` al formato de mensaje de error estándar. Como resultado, los mensajes de error de validación se muestran a nivel de campo en el formulario adaptable.