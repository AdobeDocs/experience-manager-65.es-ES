---
title: API para invocar el servicio del modelo de datos de formulario desde formularios adaptables
seo-title: API para invocar el servicio del modelo de datos de formulario desde formularios adaptables
description: Explica la API invokeWebServices que puede utilizar para invocar servicios Web escritos en WSDL desde un campo de formulario adaptable.
seo-description: Explica la API invokeWebServices que puede utilizar para invocar servicios Web escritos en WSDL desde un campo de formulario adaptable.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
translation-type: tm+mt
source-git-commit: adf1ac2cb84049ca7e42921ce31135a6149ef510
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---


# API para invocar el servicio del modelo de datos de formulario desde formularios adaptables {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## Información general {#overview}

AEM Forms permite a los autores de formularios simplificar y mejorar aún más la experiencia de cumplimentación de formularios invocando servicios configurados en un modelo de datos de formulario desde un campo de formulario adaptable. Para invocar un servicio de modelo de datos, puede crear una regla en el editor visual o especificar un JavaScript mediante la `guidelib.dataIntegrationUtils.executeOperation` API en el editor de código del editor [de](/help/forms/using/rule-editor.md)reglas.

Este documento se centra en escribir un JavaScript usando la `guidelib.dataIntegrationUtils.executeOperation` API para invocar un servicio.

## Uso de la API {#using-the-api}

La `guidelib.dataIntegrationUtils.executeOperation` API invoca un servicio desde un campo de formulario adaptable. La sintaxis de la API es la siguiente:

```
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

La estructura de la `guidelib.dataIntegrationUtils.executeOperation` API especifica detalles sobre la operación de servicio. La sintaxis de la estructura es la siguiente:

```
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

La estructura de la API especifica los siguientes detalles sobre la operación de servicio.

<table>
 <tbody>
  <tr>
   <th>Parámetro</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>Estructura para especificar el identificador del modelo de datos de formulario, el título de la operación y el nombre de la operación</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>Especifica la ruta del repositorio al modelo de datos del formulario, incluido su nombre</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>Especifica el nombre de la operación de servicio que se va a ejecutar</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>Asigna uno o varios objetos de formulario a los argumentos de entrada para la operación de servicio</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>Asigna uno o varios objetos de formulario a los valores de salida de la operación de servicio para rellenar los campos de formulario<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>Devuelve valores basados en los argumentos de entrada para la operación de servicio. Es un parámetro opcional utilizado como función de llamada de retorno.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>Muestra un mensaje de error si la función de llamada de retorno de éxito no muestra los valores de salida según los argumentos de entrada. Es un parámetro opcional utilizado como función de llamada de retorno.<br /> </td>
  </tr>
 </tbody>
</table>

## Secuencia de comandos de ejemplo para invocar un servicio {#sample-script-to-invoke-a-service}

La siguiente secuencia de comandos de ejemplo utiliza la `guidelib.dataIntegrationUtils.executeOperation` API para invocar la operación de `getAccountById` servicio configurada en el modelo de datos del `employeeAccount` formulario.

La `getAccountById` operación toma el valor en el campo del `employeeID` formulario como entrada para el `empId` argumento y devuelve el nombre del empleado, el número de cuenta y el saldo de la cuenta del empleado correspondiente. Los valores de salida se rellenan en los campos de formulario especificados. Por ejemplo, el valor del `name` argumento se rellena en el elemento de `fullName` formulario y el valor del `accountNumber` argumento en el elemento `account` de formulario.

```
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

## Uso de la API con la función de llamada de retorno {#using-the-api-callback}

También puede invocar el servicio del modelo de datos de formulario mediante la `guidelib.dataIntegrationUtils.executeOperation` API con una función de llamada de retorno. La sintaxis de la API es la siguiente:

```
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

La función de llamada de retorno puede tener `success` y `failure` funciones de llamada de retorno.

### Secuencia de comandos de muestra con funciones de llamada de retorno de éxito y error {#callback-function-success-failure}

La siguiente secuencia de comandos de ejemplo utiliza la `guidelib.dataIntegrationUtils.executeOperation` API para invocar la operación de `GETOrder` servicio configurada en el modelo de datos del `employeeOrder` formulario.

La `GETOrder` operación toma el valor del campo del `Order ID` formulario como entrada para el `orderId` argumento y devuelve el valor de cantidad de pedido en la función de llamada de retorno `success` .  Si la función de `success` llamada de retorno no devuelve la cantidad de pedido, la función de llamada de retorno `failure` muestra el `Error occured` mensaje.

>[!NOTE]
>
> Si utiliza la función de `success` llamada de retorno, los valores de salida no se rellenan en los campos de formulario especificados.

```
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
