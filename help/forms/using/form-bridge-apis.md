---
title: API de Form Bridge para formularios HTML5
seo-title: Form Bridge APIs for HTML5 forms
description: Las aplicaciones externas utilizan la API de FormBridge para conectarse al formulario móvil XFA. La API distribuye un evento FormBridgeInitialized en la ventana principal.
seo-description: External applications use the FormBridge API to connect to the XFA Mobile Form. The API dispatches a FormBridgeInitialized event on the parent window.
uuid: 0db22649-522b-4857-9ffd-826c52381d15
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
discoiquuid: c05c9911-7c49-4342-89de-61b8b9953c83
exl-id: b598ef47-49ff-4806-8cc7-4394aa068eaa
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---

# API de Form Bridge para formularios HTML5 {#form-bridge-apis-for-html-forms}

Puede utilizar las API de Form Bridge para abrir un canal de comunicación entre los formularios HTML5 basados en XFA y las aplicaciones. Las API de Form Bridge proporcionan un **connect** para crear la conexión.

La variable **connect** La API acepta un controlador como argumento. Después de crear una conexión correcta entre el formulario HTML5 basado en XFA y Form Bridge, se invoca el controlador.

Puede utilizar el siguiente código de ejemplo para crear la conexión.

```javascript
// Example showing how to connect to FormBridge
window.addEventListener("FormBridgeInitialized",
                                function(event) {
                                    var fb = event.detail.formBridge;
                                    fb.connect(function() {
                                           //use form bridge functions
                         })
                            })
```

>[!NOTE]
>
>Asegúrese de crear una conexión antes de incluir el archivo formRuntime.jsp.

## API de Form Bridge disponible  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

Devuelve el número de versión de la biblioteca Scripting

* **Entrada**: Ninguna
* **Salida**: Número de versión de la biblioteca de secuencias de comandos
* **Errores**: Ninguna

**isConnected()** Comprueba si el estado del formulario se ha inicializado

* **Entrada**: Ninguna
* **Salida**: **True** si el estado del formulario XFA se ha inicializado

* **Errores**: Ninguna

**connect(handler, context)** Realiza una conexión con FormBridge y ejecuta la función después de establecer la conexión y de inicializar Form State

* **Entrada**:

   * **handler**: Función que se ejecuta después de conectar Form Bridge
   * **context**: El objeto en el que el contexto (esto) de la variable *handler* están definidas.

* **Salida**: Ninguna
* **Error**: Ninguna

**getDataXML(options)** Devuelve los datos del formulario actual en formato XML

* **Entrada:**

   * **opciones:** Objeto JavaScript que contiene las siguientes propiedades:

      * **Error**: Función del controlador de errores
      * **success**: Función del controlador de éxito. Esta función pasa a un objeto que contiene XML en *data* propiedad.
      * **context**: El objeto en el que el contexto (esto) de la variable *success* está establecida
      * **validationChecker**: Función a la que llamar para comprobar los errores de validación recibidos del servidor. La función de validación se pasa a una matriz de cadenas de error.
      * **formState**: Estado JSON del formulario XFA para el que se debe devolver XML de datos. Si no se especifica, devuelve el XML de datos del formulario procesado actualmente.

* **Salida:** Ninguna
* **Error:** Ninguna

**registerConfig(configName, config)** Registra configuraciones específicas del usuario/portal con FormBridge. Estas configuraciones anulan las configuraciones predeterminadas. Las configuraciones admitidas se especifican en la sección de configuración .

* **Entrada:**

   * **configName:** Nombre de la configuración que desea anular

      * **widgetConfig:** Permite que el usuario anule los widgets predeterminados del formulario con widgets personalizados. La configuración se anula de la siguiente manera:

         *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig:** Permite al usuario anular el comportamiento predeterminado de procesar solo la primera página. La configuración se anula de la siguiente manera:

         *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true false=&quot;&quot;>, scarinkPageDisabled: &lt;true false=&quot;&quot;> }).*

      * **LoggingConfig:** Permite al usuario anular el nivel de registro, desactivar el registro de una categoría, o mostrar la consola de registros o enviar al servidor. La configuración se puede sobrescribir de la siguiente manera:

      ```javascript
      formBridge.registerConfig{
        "LoggerConfig" : {
      {
      "on":`<true *| *false>`,
      "category":`<array of categories>`,
      "level":`<level of categories>`, "
      type":`<"console"/"server"/"both">`
      }
        }
      ```

      * **SubmitServiceProxyConfig:** Permita que los usuarios registren los servicios proxy de envío y registrador.

         ```javascript
         window.formBridge.registerConfig("submitServiceProxyConfig",
         {
         "submitServiceProxy" : "`<submitServiceProxy>`",
         "logServiceProxy": "`<logServiceProxy>`",
         "submitUrl" : "`<submitUrl>`"
         });
         ```
   * **config:** Valor de la configuración



* **Salida:** Objeto que contiene el valor original de la configuración en *data* propiedad.

* **Error:** Ninguna

**hideFields(fieldArray)** Oculta los campos cuyas expresiones Som se proporcionan en fieldArray. Establece la propiedad presence de los campos especificados como invisible

* **Entrada:**

   * **fieldArray:** Matriz de expresiones Som para los campos que desea ocultar

* **Salida:** Ninguna
* **Error:** Ninguna

**showFields(fieldArray)** Muestra los campos cuyas expresiones Som se proporcionan en fieldArray. Define la propiedad presence de los campos proporcionados como visible

* **Entrada:**

   * **fieldArray:** Matriz de expresiones Som para los campos que se van a mostrar

* **Salida:** Ninguna
* **Error:** Ninguna

**hideSubmitButton()** Oculta todos los botones de envío del formulario

* **Entrada**: Ninguna
* **Salida**: Ninguna
* **Error**: Muestra la excepción si el estado del formulario no está inicializado

**getFormState()** Devuelve el JSON que representa el estado del formulario

* **Entrada:** Ninguna
* **Salida:** Objeto que contiene JSON que representa el estado de formulario actual en *data* propiedad.

* **Error:** Ninguna

**restoreFormState(options)** Restaura el estado del formulario a partir del estado JSON proporcionado en el objeto options . Se aplica el estado y se llaman a los controladores de éxito o de error una vez finalizada la operación

* **Entrada:**

   * **Opciones:** Objeto JavaScript que contiene las siguientes propiedades:

      * **Error**: Función del controlador de errores
      * **success**: Función del controlador de éxito
      * **context**: El objeto en el que el contexto (esto) de la variable *success* están definidas
      * **formState**: Estado JSON del formulario. El formulario se restaura al estado JSON.

* **Salida:** Ninguna
* **Error:** Ninguna

**setFocus (som)** Define el enfoque en el campo especificado en la expresión Som

* **Entrada:** Expresión del campo en el que se va a definir el enfoque
* **Salida:** Ninguna
* **Error:** Genera una excepción en caso de expresión Som incorrecta

**setFieldValue (som, value)** Define el valor de los campos para las expresiones Som dadas

* **Entrada:**

   * **som:** Matriz que contiene expresiones Som del campo. La expresión som para establecer el valor de los campos.
   * **valor:** Matriz que contiene los valores correspondientes a las expresiones Som proporcionadas en una **som** matriz. Si el tipo de datos del valor no es el mismo que fieldType, el valor no se modifica.

* **Salida:** Ninguna
* **Error:** Genera una excepción en el caso de una expresión Som incorrecta

**getFieldValue (som)** Devuelve el valor de los campos de las expresiones Som dadas

* **Entrada:** Matriz que contiene expresiones Som de los campos cuyo valor debe recuperarse
* **Salida:** Objeto que contiene el resultado como matriz en **data** propiedad.

* **Error:** Ninguna

### Ejemplo de la API getFieldValue() {#example-of-nbsp-getfieldvalue-api}

```JavaScript
var a =  formBridge.getFieldValue("xfa.form.form1.Subform1.TextField");
if(a.errors) {
    var err;
     while((err = a.getNextMessage()) != null)
               alert(a.message)
} else {
   alert(a.data[0])
}
```

**getFieldProperties(som, propiedad)** Recupere la lista de valores para la propiedad dada de los campos especificados en expresiones Som

* **Entrada:**

   * **som:** Matriz que contiene expresiones Som para los campos
   * **property**: Nombre de la propiedad cuyo valor es obligatorio

* **Salida:** Objeto que contiene el resultado como matriz en *data* property

* **Error:** Ninguna

**setFieldProperties(som, property, values)** Define el valor de la propiedad dada para todos los campos especificados en las expresiones Som

* **Entrada:**

   * **som:** Matriz que contiene expresiones Som de los campos cuyo valor debe establecerse
   * **property**: Propiedad cuyo valor debe establecerse
   * **valor:** Matriz que contiene valores de la propiedad dada para los campos especificados en Expresiones Som

* **Salida:** Ninguna
* **Error:** Ninguna

## Ejemplo de uso de la API de Form Bridge {#sample-usage-of-form-bridge-api}

```JavaScript
// Example 1: FormBridge.restoreFormState
  function loadFormState() {
    var suc = function(obj) {
             //success
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
        var _formState = // load form state from storage
    formBridge.restoreFormState({success:suc,error:err,formState:_formState}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }

//--------------------------------------------------------------------------------------------------

//Example 2: FormBridge.submitForm
  function SubmitForm() {
    var suc = function(obj) {
             var data = obj.data;
         // submit the data to a url;
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
    formBridge.submitForm({success:suc,error:err}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }
```
