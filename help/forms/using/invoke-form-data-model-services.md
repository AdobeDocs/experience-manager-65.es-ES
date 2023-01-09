---
title: API para invocar el servicio del modelo de datos de formulario desde formularios adaptables
seo-title: API to invoke form data model service from adaptive forms
description: Explica la API de invokeWebServices que puede utilizar para invocar servicios web escritos en WSDL desde un campo de un formulario adaptable.
seo-description: Explains the invokeWebServices API that you can use to invoke web services written in WSDL from within an adaptive form field.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: Adaptive Forms
exl-id: cf037174-3153-486f-85b1-c974cd5a1ace
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 100%

---

# API para invocar el servicio del modelo de datos de formulario desde formularios adaptables {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## Información general {#overview}

AEM Forms permite a los autores de formularios simplificar y mejorar aún más la experiencia de rellenado de formularios invocando los servicios configurados en un modelo de datos de formulario desde un campo de un formulario adaptable. Para invocar un servicio del modelo de datos, puede crear una regla en el Editor visual o especificar un JavaScript utilizando la API `guidelib.dataIntegrationUtils.executeOperation` en el Editor de código del [Editor de reglas](/help/forms/using/rule-editor.md).

Este documento explica cómo escribir un JavaScript usando la API `guidelib.dataIntegrationUtils.executeOperation` para invocar un servicio.

## Uso de la API {#using-the-api}

La API `guidelib.dataIntegrationUtils.executeOperation` invoca un servicio desde un campo de formulario adaptable. La sintaxis de la API es la siguiente:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

La estructura de la API `guidelib.dataIntegrationUtils.executeOperation` especifica los detalles de la operación del servicio. La sintaxis de la estructura es la siguiente:

```javascript
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

La estructura de la API especifica los siguientes detalles sobre la operación del servicio.

<table>
 <tbody>
  <tr>
   <th>Parámetro</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>La estructura para especificar el identificador del modelo de datos de formulario, el título y el nombre de la operación.</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>Especifica la ruta del repositorio del modelo de datos de formulario, incluido su nombre.</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>Especifica el nombre de la operación de servicio que se va a ejecutar.</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>Asigna uno o varios objetos de formulario a los argumentos de entrada para la operación de servicio.</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>Asigna uno o varios objetos de formulario a los valores de salida de la operación de servicio para rellenar los campos del formulario.<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>Devuelve valores basados en los argumentos de entrada de la operación de servicio. Es un parámetro opcional utilizado como función de devolución de llamada.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>Muestra un mensaje de error si la función de devolución de llamada success no muestra los valores de salida en función de los argumentos de entrada. Es un parámetro opcional utilizado como función de devolución de llamada.<br /> </td>
  </tr>
 </tbody>
</table>

## Script de ejemplo para invocar un servicio {#sample-script-to-invoke-a-service}

El siguiente script de ejemplo utiliza la API `guidelib.dataIntegrationUtils.executeOperation` para invocar la operación de servicio `getAccountById` configurada en el modelo de datos de formulario `employeeAccount`.

La operación `getAccountById` toma el valor del campo del formulario `employeeID` como entrada para el argumento `empId` y devuelve el nombre del empleado y el número y el saldo de la cuenta del empleado correspondiente. Los valores de salida se rellenan en los campos del formulario especificados. Por ejemplo, el valor del argumento `name` se rellena en el elemento de formulario `fullName`, y el valor del argumento `accountNumber` argumento en el elemento de formulario `account`.

```javascript
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

## Uso de la API con una función de devolución de llamada {#using-the-api-callback}

También puede invocar el servicio del modelo de datos de formulario utilizando la API `guidelib.dataIntegrationUtils.executeOperation` con una función de devolución de llamada. La sintaxis de la API es la siguiente:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

La función de devolución de llamada puede tener las funciones de devolución de llamada `success` y `failure`.

### Script de ejemplo con las funciones de devolución de llamada success y failure {#callback-function-success-failure}

El siguiente script de ejemplo utiliza la API `guidelib.dataIntegrationUtils.executeOperation` para invocar la operación de servicio `GETOrder` configurada en el modelo de datos de formulario `employeeOrder`.

La operación `GETOrder` toma el valor del campo de formulario `Order ID` como entrada para el argumento `orderId` y devuelve el valor de la cantidad del pedido en la función de devolución de llamada `success`. Si la función de devolución de llamada `success` no devuelve la cantidad del pedido, la función de devolución de llamada `failure` muestra el mensaje `Error occured`.

>[!NOTE]
>
>Si usa la función de devolución de llamada `success`, los valores de salida no se rellenan en los campos del formulario especificados.

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
