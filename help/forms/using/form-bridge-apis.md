---
title: API de puente de formulario para formularios HTML5
seo-title: API de puente de formulario para formularios HTML5
description: Las aplicaciones externas utilizan la API de FormBridge para conectarse al formulario móvil XFA. La API distribuye un evento FormBridgeInitialized en la ventana principal.
seo-description: Las aplicaciones externas utilizan la API de FormBridge para conectarse al formulario móvil XFA. La API distribuye un evento FormBridgeInitialized en la ventana principal.
uuid: 0db22649-522b-4857-9ffd-826c52381d15
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
discoiquuid: c05c9911-7c49-4342-89de-61b8b9953c83
translation-type: tm+mt
source-git-commit: 8f90dc4865126d52e04effc9197ef7145b1a167e

---


# API de puente de formulario para formularios HTML5 {#form-bridge-apis-for-html-forms}

Puede utilizar las API de puente de formulario para abrir un canal de comunicación entre los formularios HTML5 basados en XFA y las aplicaciones. Las API de puente de formulario proporcionan una API de **conexión** para crear la conexión.

La API de **conexión** acepta un controlador como argumento. Después de crear una conexión correcta entre el formulario HTML5 basado en XFA y el puente de formulario, se invoca el controlador.

Puede utilizar el siguiente código de muestra para crear la conexión.

```
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

## API de puente de formulario disponible {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

Devuelve el número de versión de la biblioteca de secuencias de comandos

* **Entrada**: Ninguno
* **Salida**: Número de versión de la biblioteca de secuencias de comandos
* **Errores**: Ninguno

**isConnected()** Comprueba si se ha inicializado el estado del formulario

* **Entrada**: Ninguno
* **Salida**: **True** si se ha inicializado el estado del formulario XFA

* **Errores**: Ninguno

**connect(handler, context)** Realiza una conexión con FormBridge y ejecuta la función después de realizar la conexión y de inicializar el estado del formulario

* **Entrada**:

   * **handler**: Función que se ejecutará después de que se haya conectado el puente de formulario
   * **contexto**: El objeto en el que se establece el contexto (esto) de la función de *controlador* .

* **Salida**: Ninguno
* **Error**: Ninguno

**getDataXML(options)** Devuelve los datos de formulario actuales en formato XML

* **Entrada:**

   * **** opciones: Objeto JavaScript que contiene las siguientes propiedades:

      * **Error**: Función del controlador de errores
      * **success**: Función de controlador de éxito. Esta función se pasa a un objeto que contiene XML en la propiedad *data* .
      * **contexto**: El objeto en el que se establece el contexto (esto) de la función de *éxito*
      * **validationChecker**: Función para llamar para comprobar los errores de validación recibidos del servidor. La función de validación se pasa a una matriz de cadenas de error.
      * **formState**: Estado JSON del formulario XFA para el que se debe devolver el XML de datos. Si no se especifica, devuelve el XML de datos del formulario procesado actualmente.

* **** Salida: Ninguno
* **** Error: Ninguno

**registerConfig(configName, config)** Registra configuraciones específicas de usuario/portal con FormBridge. Estas configuraciones anulan las configuraciones predeterminadas. Las configuraciones admitidas se especifican en la sección de configuración.

* **Entrada:**

   * **** configName: Nombre de la configuración que se va a omitir

      * **** widgetConfig: Permite al usuario anular los widgets predeterminados del formulario con widgets personalizados. La configuración se sobrescribe de la siguiente manera:

         *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **** pagingConfig: Permite que el usuario anule el comportamiento predeterminado de procesar solo la primera página. La configuración se sobrescribe de la siguiente manera:

         *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true| false>, shrinkPageDisabled: &lt;true| false> }).*

      * **** LoggingConfig: Permite al usuario anular el nivel de registro, deshabilitar el registro de una categoría o mostrar la consola de registros o enviar al servidor. La configuración se puede anular de la siguiente manera:

      ```JavaScript
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

      * **** SubmitServiceProxyConfig: Permita que los usuarios registren los servicios proxy de envío y de registro.

         ```JavaScript
         window.formBridge.registerConfig("submitServiceProxyConfig",
         {
         "submitServiceProxy" : "`<submitServiceProxy>`",
         "logServiceProxy": "`<logServiceProxy>`",
         "submitUrl" : "`<submitUrl>`"
         });
         ```
   * **** config: Valor de la configuración



* **** Salida: Objeto que contiene el valor original de la configuración en la propiedad *data* .

* **** Error: Ninguno

**hideFields(fieldArray)** Oculta los campos cuyas expresiones Som se proporcionan en fieldArray. Establece la propiedad presence de los campos especificados como invisible

* **Entrada:**

   * **** fieldArray: Matriz de expresiones Som para los campos que se van a ocultar

* **** Salida: Ninguno
* **** Error: Ninguno

**showFields(fieldArray)** Muestra los campos cuyas expresiones Som se proporcionan en fieldArray. Define la propiedad presence de los campos proporcionados como visible

* **Entrada:**

   * **** fieldArray: Matriz de expresiones Som para los campos que se van a mostrar

* **** Salida: Ninguno
* **** Error: Ninguno

**hideSubmitButtons()** Oculta todos los botones de envío del formulario

* **Entrada**: Ninguno
* **Salida**: Ninguno
* **Error**: Emite una excepción si el estado del formulario no se ha inicializado

**getFormState()** Devuelve el JSON que representa el estado del formulario

* **** Entrada: Ninguno
* **** Salida: Objeto que contiene JSON que representa el estado de formulario actual en la propiedad *data* .

* **** Error: Ninguno

**restoreFormState(options)** Restaura el estado del formulario a partir del estado JSON proporcionado en el objeto options. Se aplica el estado y se llaman a los controladores de éxito o error una vez finalizada la operación

* **Entrada:**

   * **** Opciones: Objeto JavaScript que contiene las siguientes propiedades:

      * **Error**: Función del controlador de errores
      * **success**: Función de controlador de éxito
      * **contexto**: El objeto en el que se establece el contexto (esto) de la función de *éxito*
      * **formState**: Estado JSON del formulario. El formulario se restaura al estado JSON.

* **** Salida: Ninguno
* **** Error: Ninguno

**setFocus (som)** Define el enfoque en el campo especificado en la expresión Som

* **** Entrada: Una expresión del campo en el que se va a definir el enfoque
* **** Salida: Ninguno
* **** Error: Emite una excepción en caso de una expresión Som incorrecta

**setFieldValue (som, value)** Establece el valor de los campos de las expresiones Som determinadas

* **Entrada:**

   * **** som: Matriz que contiene expresiones de tipo &quot;Som&quot; del campo. Expresión som para establecer el valor de los campos.
   * **** value: Matriz que contiene los valores correspondientes a expresiones Som proporcionadas en una **** matriz. Si el tipo de datos del valor no es el mismo que fieldType, el valor no se modifica.

* **** Salida: Ninguno
* **** Error: Emite una excepción en el caso de una expresión Som incorrecta

**getFieldValue (som)** Devuelve el valor de los campos de las expresiones Som determinadas

* **** Entrada: Matriz que contiene expresiones de tipo de los campos cuyo valor se debe recuperar
* **** Salida: Objeto que contiene el resultado como matriz en la propiedad **data** .

* **** Error: Ninguno

### Ejemplo de la API getFieldValue() {#example-of-nbsp-getfieldvalue-api}

```JavaScript
var a =  formBridge.getFieldValue(“xfa.form.form1.Subform1.TextField”);
if(a.errors) {
    var err;
     while((err = a.getNextMessage()) != null)
               alert(a.message)
} else {
   alert(a.data[0])
}
```

**getFieldProperties(som, property)** Recupere la lista de valores de la propiedad dada de los campos especificados en las expresiones Som

* **Entrada:**

   * **** som: Matriz que contiene expresiones Som para los campos
   * **propiedad**: Nombre de la propiedad cuyo valor es obligatorio

* **** Salida: Objeto que contiene el resultado como matriz en la propiedad *data*

* **** Error: Ninguno

**setFieldProperties(som, property, values)** Establece el valor de la propiedad dada para todos los campos especificados en las expresiones Som

* **Entrada:**

   * **** som: Matriz que contiene expresiones Som de los campos cuyo valor se debe definir
   * **propiedad**: Propiedad cuyo valor debe establecerse
   * **** value: Matriz que contiene valores de la propiedad dada para los campos especificados en expresiones Som

* **** Salida: Ninguno
* **** Error: Ninguno

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

**[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)**
