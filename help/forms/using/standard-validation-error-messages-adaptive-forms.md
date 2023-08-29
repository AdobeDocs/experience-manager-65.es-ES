---
title: Mensajes de error de validación estándar para formularios adaptables
seo-title: Standard validation error messages for adaptive forms
description: Transformar los mensajes de error de validación para formularios adaptables al formato estándar mediante controladores de error personalizados
seo-description: Transform the validation error messages for adaptive forms into standard format using custom error handlers
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
source-git-commit: 34be3b4695679a9b5e8001d28f05ed804f929e61
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 95%

---


# Mensajes de error de validación estándar para formularios adaptables {#standard-validation-error-messages}

Los formularios adaptables validan las entradas que se proporcionan en los campos en función de criterios de validación predefinidos. Los criterios de validación hacen referencia a los valores de entrada aceptables para los campos de un formulario adaptable. Puede definir los criterios de validación en función del origen de datos que utilice con el formulario adaptable. Por ejemplo, si utiliza los servicios web RESTful como fuente de datos, puede definir los criterios de validación en un archivo de definición Swagger.

Si los valores de entrada cumplen los criterios de validación, los valores se envían a la fuente de datos. De lo contrario, el formulario adaptable mostrará un mensaje de error.

De forma similar a este enfoque, los formularios adaptables ahora se pueden integrar con servicios personalizados para realizar validaciones de datos. Si los valores de entrada no cumplen los criterios de validación y el mensaje de error de validación que devuelve el servidor está en el formato de mensaje estándar, los mensajes de error se muestran en el formulario a nivel de campo.

Si los valores de entrada no cumplen los criterios de validación y el mensaje de error de validación del servidor no está en el formato de mensaje estándar, los formularios adaptables proporcionan un mecanismo para transformar los mensajes de error de validación en un formato estándar para que se muestren en el campo del formulario. Puede transformar el mensaje de error en el formato estándar mediante cualquiera de los dos siguientes métodos:

* Agregar un controlador de error personalizado en el envío de formulario adaptable
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

Antes de agregar el controlador personalizado, debe configurar el formulario adaptable para el envío asincrónico. Siga estos pasos:

<!-- 1. In adaptive form authoring mode, select the Form Container object and tap ![adaptive form properties](assets/af_properties.png) to open its properties.
1. In the **[!UICONTROL Submission]** properties section, enable **[!UICONTROL Use asynchronous submission]**.
1. Select **[!UICONTROL Revalidate on server]** to validate the input field values on server before submission.
1. Select the Submit Action:

    * Select **[!UICONTROL Submit using Form Data Model]** and select the appropriate data model, if you are using RESTful web service based [form data model](work-with-form-data-model.md) as the data source.
    * Select **[!UICONTROL Submit to REST endpoint]** and specify the **[!UICONTROL Redirect URL/Path]**, if you are using RESTful web services as the data source.

    ![adaptive form submission properties](assets/af_submission_properties.png)

1. Tap ![Save](assets/af_save.png) to save the properties.-->

### Agregar un controlador de error personalizado en el envío de formulario adaptable {#add-custom-error-handler-af-submission}

AEM Forms proporciona controladores de éxito y de error predeterminados para los envíos de formularios. Los controladores son funciones del lado del cliente que se ejecutan en función de la respuesta del servidor. Cuando se envía un formulario, los datos se transmiten al servidor para su validación, lo que devuelve una respuesta al cliente con información sobre el evento de éxito o error del envío. La información se pasa en forma de parámetros al controlador correspondiente para ejecutar la función.

Ejecute los siguientes pasos para agregar el controlador de error personalizado en el envío del formulario adaptable:

1. Abra el formulario adaptable en el modo de creación, seleccione cualquier objeto del formulario y pulse <!--![Rule Editor](assets/af_edit_rules.png)--> para abrir el editor de reglas.
1. Seleccione **[!UICONTROL Formulario]** en el árbol Objetos de formulario y pulse **[!UICONTROL Crear]**.
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

El `var som_map` enumera la expresión SOM de los campos de formulario adaptables que desea transformar en el formato estándar. Puede ver la expresión SOM de cualquier campo en un formulario adaptable; para ello, pulse el campo y seleccione **[!UICONTROL Ver expresión SOM]**.

Con este controlador de error personalizado, el formulario adaptable convierte los campos enumerados en `var som_map` al formato de mensaje de error estándar. Como resultado, los mensajes de error de validación se muestran a nivel de campo en el formulario adaptable.

## Agregar un controlador personalizado mediante la acción Invocar servicio

Ejecute los siguientes pasos para agregar el controlador de error para convertir una estructura de error personalizada en la estructura de error estándar mediante la acción Invocar servicio [del Editor de reglas](rule-editor.md).

<!-- 1. Open the adaptive form in authoring mode, select any form object, and tap ![Rule Editor](assets/af_edit_rules.png) to open the rule editor.
1. Tap **[!UICONTROL Create]**.
1. Create a condition in the **[!UICONTROL When]** section of the rule. For example, When[Name of field] is changed. Select **[!UICONTROL is changed]** from the **[!UICONTROL Select State]** drop-down list to achieve this condition.
1. In the **[!UICONTROL Then]** section, select **[!UICONTROL Invoke Service]** from the **[!UICONTROL Select Action]** drop-down list.
1. Select a Post service and its corresponding data bindings from the **[!UICONTROL Input]** section. For example, if you want to validate **Name**, **ID**, and **Status** fields in the adaptive form, select a Post service (pet) and select pet.name, pet.id, and pet.status in the **[!UICONTROL Input]** section.-->

    Como resultado de esta regla, los valores especificados para los campos **Nombre**, **ID** y **Estado** se validan, en cuanto se cambia el campo definido en el paso 2 y se elimina el campo del formulario.

1. Seleccione **[!UICONTROL Editor de código]** de la lista desplegable selección de modo.
1. Pulse **[!UICONTROL Editar código]**.
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

   El `var som_map` enumera la expresión SOM de los campos de formulario adaptables que desea transformar en el formato estándar. Puede ver la expresión SOM de cualquier campo en un formulario adaptable; para ello, pulse el campo y seleccione **[!UICONTROL Ver expresión SOM]** del menú **[!UICONTROL Más opciones]** (...).

   Asegúrese de copiar la siguiente línea del código de ejemplo en el controlador de error personalizado:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   La API executeOperation incluye los parámetros `null` y `errorHandler` basados en el nuevo controlador de error personalizado.

   Con este controlador de error personalizado, el formulario adaptable convierte los campos enumerados en `var som_map` al formato de mensaje de error estándar. Como resultado, los mensajes de error de validación se muestran a nivel de campo en el formulario adaptable.