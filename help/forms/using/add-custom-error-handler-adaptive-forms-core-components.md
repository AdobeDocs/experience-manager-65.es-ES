---
title: Añadir un controlador de error personalizado en Forms AEM adaptable basado en componentes principales para Forms adaptable de la
seo-title: Error Handlers in Adaptive Forms for AEM Adaptive Forms core components
description: AEM Forms proporciona controladores de éxitos y de errores predeterminados para un formulario mediante el punto final REST configurado para invocar un servicio externo. AEM Puede agregar un controlador de error predeterminado y un controlador de error personalizado en un formulario adaptable con un formato de formulario adaptable con un nombre de usuario.
seo-description: Error handler function and Rule Editor in Adaptive Forms core components helps you to effectively manage and customize error handling. You can add a default error handler as well as custom error handler in an AEM Adaptive Form.
keywords: Añadir un controlador de errores personalizado, añadir un controlador de errores predeterminado, añadir un controlador de errores en el formulario, utilizar el servicio de invocación del editor de reglas para añadir un controlador de errores personalizado, configurar el editor de reglas para añadir un controlador de errores personalizado y añadir un controlador de errores personalizado mediante el editor de reglas
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms
source-git-commit: f8e0ac45d98d6485ccb60e754657caf9d190c3ea
workflow-type: tm+mt
source-wordcount: '2281'
ht-degree: 74%

---


# Controladores de errores en formularios adaptables (Componentes principales) {#error-handlers-in-adaptive-form}

AEM Forms proporciona controladores de éxito y de error predeterminados para los envíos de formularios. También proporciona una función para personalizar las funciones del controlador de errores. Por ejemplo, puede invocar un flujo de trabajo personalizado en el back-end para códigos de error específicos o informar al cliente de que el servicio está inactivo. Los controladores son funciones del lado del cliente que se ejecutan en función de la respuesta del servidor. Cuando se invoca un servicio externo mediante las API, los datos se transmiten al servidor para su validación, lo que devuelve una respuesta al cliente con información sobre el evento de éxito o error del envío. La información se pasa en forma de parámetros al controlador correspondiente para ejecutar la función. Un controlador de errores ayuda a administrar y mostrar los errores o problemas de validación encontrados.

![flujo de trabajo del controlador de errores para comprender cómo añadir el controlador de errores personalizado en los formularios](/help/forms/using/assets/error-handler-workflow.png)

El formulario adaptable valida las entradas que se proporcionan en los campos en función de criterios de validación predefinidos y comprueba los distintos errores devueltos por el extremo REST configurado para invocar un servicio externo. Puede definir los criterios de validación en función de la fuente de datos que utilice con el formulario adaptable. Por ejemplo, si utiliza los servicios web RESTful como fuente de datos, puede definir los criterios de validación en un archivo de definición Swagger.

Si los valores de entrada cumplen los criterios de validación, los valores se envían al origen de datos; de lo contrario, el formulario adaptable muestra un mensaje de error utilizando un controlador de errores. De forma similar a este enfoque, el Forms adaptable se integra con controladores de error personalizados para realizar validaciones de datos. Si los valores de entrada no cumplen los criterios de validación, los mensajes de error se muestran a nivel de campo en el formulario adaptable. Esto ocurre cuando el mensaje de error de validación devuelto por el servidor tiene el formato de mensaje estándar.


## Usos de los controladores de errores {#uses-of-error-handler}

Los controladores de errores se utilizan para varios fines. A continuación se enumeran algunos de los usos de las funciones del controlador de errores:

* **Realizar validación**: la gestión de errores comienza con la validación de las entradas del usuario con reglas o criterios predefinidos. A medida que los usuarios rellenan un formulario adaptable, el controlador de errores valida la entrada para asegurarse de que cumple el formato, la longitud o cualquier otra restricción necesaria.

* **Proporcionar comentarios en tiempo real**: cuando se detecta cualquier error, el controlador de errores muestra comentarios inmediatos al usuario, como mensajes de error en línea debajo de los campos de formulario correspondientes. Estos comentarios ayudan a los usuarios a identificar y corregir errores sin tener que enviar el formulario y esperar una respuesta.


* **Mostrar mensajes de error**: cuando el envío de un formulario adaptable encuentra algún error de validación, el controlador de errores muestra un mensaje de error adecuado. Los mensajes de error deben ser claros, concisos y resaltar los campos específicos que requieren atención.

* **Resalta el campo erróneo**: para llamar la atención del usuario sobre los campos incorrectos específicos, el controlador de errores resalta o diferencia visualmente los campos correspondientes. Se lleva a cabo cambiando el color de fondo, agregando un icono o borde, o cualquier otra señal visual que ayude a los usuarios a localizar rápidamente los errores y solucionarlos.


## Formato de respuesta de errores {#failure-response-format}

Un formulario adaptable muestra los errores en un nivel de campo si los mensajes de error de validación del servidor tienen el siguiente formato estándar.
El siguiente código ilustra la estructura de respuesta a errores existente:

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]
        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
    }
```


Donde:

* `errorCausedBy` describe el motivo del error.
* `errors` mencione el nombre de campo completo de los campos en los que se han producido errores en los criterios de validación junto con el mensaje de error de validación.
* El campo `originCode` añadido por AEM que contiene el código de estado HTTP devuelto por el servicio externo.
* El campo `originMessage` añadido por AEM que contiene los datos de error sin procesar devueltos por el servicio externo.

Con las mejoras en las funciones y las actualizaciones posteriores en las versiones de AEM Forms, la estructura de respuesta a errores existente ha cambiado a un nuevo formato basado en RFC7807, que es compatible con versiones anteriores de la estructura de respuesta a errores existente:

```javascript
    {
        "type": "SERVER_SIDE_VALIDATION/FORM_SUBMISSION/SERVICE_INVOCATION/FAILURE/VALIDATION_ERROR", (required)
        "title": "Server side validation failed/Third party service invocation failed", (optional)
        "detail": "", (optional)
        "instance": "", (optional)
        "validationErrors" : [ (required)
            {
                "fieldName":"<qualified fieldname of the field whose data sent is invalid>",
                "dataRef":<JSONPath (or XPath) of the data element which is invalid>
                "details": ["Error Message(s) for the field"] (required)
    
            }
        ],
        "originCode": <Origin http status code>, (optional - in case of SERVER_SIDE_VALIDATION)
        "originMessage" : "<unstructured error message returned by service>" (optional - in case of SERVER_SIDE_VALIDATION)
    }
```


>[!NOTE]
>
> * Asegúrese de que la estructura de respuesta de error incluya lo siguiente **fieldName** o **dataRef**.
> * Asegúrese de que el encabezado **ContentType** es **application/problem+json**.

Donde:
* `type (required)` especifica el tipo de error. Puede tener uno de los siguientes valores:
   * `SERVER_SIDE_VALIDATION` indica un error debido a la validación del lado del servidor.
   * `FORM_SUBMISSION` indica un error durante el envío del formulario
   * `SERVICE_INVOCATION` indica un error durante una invocación de servicio de terceros.
   * `FAILURE` indica un error general.
   * `VALIDATION_ERROR` indica un error debido a un error de validación.

* `title (optional)` proporciona un título o una breve descripción del error.
* `detail (optional)` proporciona detalles adicionales sobre el error si es necesario.
* `instance (optional)` representa una instancia o identificador asociado con el error y ayuda a rastrear o identificar la incidencia específica del error.
* `validationErrors (required)` contiene información sobre errores de validación. Incluye los siguientes campos:
   * `fieldname` menciona el nombre de campo completo de los campos en los que se han producido errores en los criterios de validación.
   * `dataRef` representa la ruta JSON o XPath de los campos en los que se ha producido un error en la validación.
   * `details` contiene el mensaje de error de validación con el campo erróneo.
* El campo `originCode (optional)` añadido por AEM contiene el código de estado HTTP devuelto por el servicio externo
* El campo `originMessage (optional)` añadido por AEM contiene los datos de error sin procesar devueltos por el servicio externo.

### Formato de respuesta de error de muestra {#sample-error-response-format}

Algunas de las opciones para mostrar las respuestas de error son las siguientes:

+++  Basado en la propiedad fieldName del formulario adaptable


* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
          {
              "type": "VALIDATION_ERROR",
              "validationErrors": [
              {
              "fieldName": "$form.PetId",
              "dataRef": "",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
          ]
          }
          ]}
  ```


+++


+++ Basado en la propiedad dataRef del formulario adaptable

* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
      {
          "type": "VALIDATION_ERROR",
          "validationErrors": [
          {
              "fieldName": "",
              "dataRef": "$.Pet.id",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
              ]
              }
      ]}
  ```

+++

## Requisitos previos {#prerequisites}

Antes de utilizar el controlador de error en un Forms adaptable:

* [Habilitar los componentes principales de formularios adaptables para su entorno](enable-adaptive-forms-core-components.md).
* Conocimientos básicos para [crear una función personalizada](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/adaptive-forms/custom-functions-aem-forms.html?lang=en#:~:text=AEM%20Forms%206.5%20introduced%20the,use%20them%20across%20multiple%20forms.).
* Instale la última versión de [Apache Maven](https://maven.apache.org/download.cgi).

## Adición de un controlador de error mediante el Editor de reglas {#add-error-handler-using-rule-editor}

Utilizando la acción del [Servicio de invocación del editor de reglas](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=es#invoke), se definen los criterios de validación en función de la fuente de datos que se utilice con el formulario adaptable. Por ejemplo, si utiliza los servicios web RESTful como fuente de datos, puede definir los criterios de validación en un archivo de definición Swagger. Al utilizar las funciones de controlador de error y el Editor de reglas en Forms adaptable, puede administrar y personalizar de forma eficaz la gestión de errores. Las condiciones se definen mediante el Editor de reglas y se configuran las acciones que deben realizarse cuando se activa la regla. Los formularios adaptables validan las entradas que se proporcionan en los campos en función de criterios de validación predefinidos. En caso de que los valores de entrada no cumplan los criterios de validación, los mensajes de error se muestran a nivel de campo en un formulario adaptable.

>[!NOTE]
>
> * Para utilizar controladores de errores con la acción Invocar servicio del Editor de reglas, configure los formularios adaptables con un modelo de datos de formulario.
> * Se proporciona un controlador de error predeterminado para mostrar mensajes de error en los campos si la respuesta de error está en el esquema estándar. También puede llamar al controlador de error predeterminado desde la función del controlador de error personalizado.

Con el Editor de reglas, puede:

* [Agregar función de controlador de error predeterminada](#add-default-errror-handler)
* [Añadir función del controlador de errores personalizado](#add-custom-errror-handler)


### Agregar función de controlador de error predeterminada {#add-default-errror-handler}

Se admite un controlador de error predeterminado para mostrar mensajes de error en los campos si la respuesta de error está en el esquema estándar o en un error de validación del lado del servidor.
Para comprender cómo utilizar un controlador de error predeterminado con [Servicio de invocación del editor de reglas](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=es#invoke) acción, tome un ejemplo de un formulario adaptable simple con dos campos, **ID de mascota** y **Nombre de mascota** y utilice un controlador de error predeterminado en **ID de mascota** para comprobar si hay varios errores devueltos por el extremo REST configurado para invocar un servicio externo, por ejemplo, `200 - OK`,`404 - Not Found`, `400 - Bad Request`. Para agregar un controlador de error predeterminado mediante la acción Invocar servicio del Editor de reglas, ejecute los siguientes pasos:

1. Abra el formulario adaptable en el modo de creación, seleccione cualquier objeto del formulario y pulse **[!UICONTROL Editor de reglas]** para abrir el editor de reglas.
1. Pulse **[!UICONTROL Crear]**.
1. Crear una condición en la sección **Cuando** de la regla. Por ejemplo, **Cuándo[Nombre del campo ID de mascota]** se ha cambiado. Seleccione se cambia de la **Seleccionar estado** lista desplegable.
1. En la sección **Entonces**, seleccione **[!UICONTROL Invocar servicio]** de la lista desplegable **Seleccionar acción**.
1. Seleccione un **servicio Post** y sus enlaces de datos correspondientes en la sección **Entrada**. Por ejemplo, para validar **ID de mascota**, seleccione un **servicio Post** como **GET /pet/{petId}** y seleccione **ID de mascota** en la sección **Entrada**.
1. Seleccione los enlaces de datos en la sección **Salida**. Seleccionar **Nombre de mascota** en el **Output** sección.
1. Seleccionar **[!UICONTROL Controlador de error predeterminado]** desde el **Controlador de errores** sección.
1. Haga clic en **[!UICONTROL Listo]**.

![agregar un controlador de error predeterminado para las comprobaciones de validación de campos en un formulario](/help/forms/using/assets/default-error-handler.png)

Como resultado de esta regla, los valores introducidos para **ID de mascota** comprueban la validación de **Nombre de mascota** utilizando el servicio externo invocado por el punto final REST. Si los criterios de validación basados en la fuente de datos fallan, los mensajes de error se muestran en el nivel de campo.

![mostrar el mensaje de error predeterminado cuando se agrega un controlador de error predeterminado en un formulario para controlar las respuestas de error](/help/forms/using/assets/default-error-message.png)

### Añadir función del controlador de errores personalizado {#add-custom-errror-handler}

Puede añadir una función del controlador de errores personalizado para realizar algunas de las acciones como:

* gestionar respuestas de error que utilizan respuestas de error no estándar o estándar. Es importante tener en cuenta que estas respuestas de error no estándar no cumplen con el [esquema estándar de respuestas de error](#failure-response-format).
* enviar eventos de Analytics a cualquier plataforma de Analytics. Por ejemplo, Adobe Analytics.
* mostrar cuadro de diálogo modal con mensajes de error.

Además de las acciones mencionadas, los controladores de errores personalizados se pueden utilizar para ejecutar funciones personalizadas que cumplan con los requisitos específicos del usuario.

El controlador de errores personalizado es una función (Biblioteca de cliente) diseñada para responder a los errores devueltos por un servicio externo y proporcionar una respuesta personalizada a los usuarios finales. Cualquier biblioteca de cliente con anotación `@errorHandler` se considera que es una función del controlador de errores personalizado. Esta anotación identifica la función de controlador de errores especificada en el archivo `.js`.


Para comprender cómo crear y utilizar un controlador de errores personalizado con la acción [Invocar servicio del editor de reglas](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=es#invoke), vamos a ver un ejemplo de formulario adaptable con dos campos, **ID de mascota** y **Nombre de mascota**. Además, usar un controlador de errores personalizado en el campo **ID de mascota** para comprobar si hay varios errores devueltos por el punto final REST configurado para invocar un servicio externo, por ejemplo, `200 - OK`, `404 - Not Found` y `400 - Bad Request`.

Para añadir y utilizar un controlador de errores personalizado en un formulario adaptable, realice los siguientes pasos:

1. [Crear un controlador de errores personalizado](#create-custom-error-message)
1. [Utilice el Editor de reglas para configurar el controlador de errores personalizado](#use-custom-error-handler)

#### 1. Crear un controlador de errores personalizado {#create-custom-error-message}

Para crear una función de error personalizada, realice los siguientes pasos:

1. Iniciar sesión en `http://server:port/crx/de/index.jsp#`.
1. Cree una carpeta en `/apps` carpeta. Por ejemplo, cree una carpeta denominada como `experience-league`.
1. Guarde los cambios.
1. Vaya a la carpeta creada y cree un nodo de tipo `cq:ClientLibraryFolder` as `clientlibs`.
1. Vaya al recién creado `clientlibs` y añada la `allowProxy` y `categories` propiedades:

   ![Propiedades del nodo de biblioteca personalizado](/help/forms/using/assets/customlibrary-properties.png)

   >[!NOTE]
   >
   > Puede proporcionar cualquier nombre en lugar de `customfunctionsdemo`.

1. Guarde los cambios.

1. Cree una carpeta llamada `js` en el `clientlibs` carpeta.
1. Cree un archivo JavaScript llamado `functions.js` en el `js` carpeta
1. Cree un archivo llamado `js.txt` en el `clientlibs` carpeta.
1. Guarde los cambios.
La estructura de carpetas creada tiene este aspecto:

   ![Estructura de carpetas de la biblioteca de cliente creada](/help/forms/using/assets/customclientlibrary_folderstructure.png)
1. Haga doble clic en `functions.js` para abrir el editor. El archivo contiene el código del controlador de errores personalizado.
Vamos a añadir el siguiente código al archivo JavaScript para mostrar la respuesta y los encabezados, recibidos del extremo del servicio REST, en la consola del explorador.

   ```javascript
       /** 
       Custom Error handler
       * @name customErrorHandler Custom Error Handler Function
       * @errorHandler
       */
       function customErrorHandler(response, headers, globals)
       {
           console.log("Custom Error Handler processing start...");
           console.log("response:"+JSON.stringify(response));
           console.log("headers:"+JSON.stringify(headers));
           alert("CustomErrorHandler - Please enter valid PetId.")
           globals.invoke('defaultErrorHandler',response, headers)
           console.log("Custom Error Handler processing end...");
       }
   ```

   Para llamar al controlador de error predeterminado desde el controlador de error personalizado, se utiliza la siguiente línea del código de ejemplo:
   `globals.invoke('defaultErrorHandler',response, headers) `

1. Guardar `function.js`.
1. Vaya a `js.txt` y agregue el siguiente código:

   ```javascript
       #base=js
       functions.js
   ```

1. Guarde el archivo `js.txt`.

Ahora, vamos a comprender cómo configurar y utilizar un controlador de errores personalizado mediante el servicio Invocar del Editor de reglas de AEM Forms.

#### 2. Utilizar el Editor de reglas para configurar el controlador de errores personalizado {#use-custom-error-handler}

Antes de implementar el controlador de error personalizado en un formulario adaptable, asegúrese de que el nombre de la biblioteca de cliente en la variable **[!UICONTROL Categoría de biblioteca de cliente]** se alinea con el nombre especificado en la opción categories de `.content.xml` archivo.

![Agregar el nombre de la biblioteca de cliente en la configuración del contenedor del formulario adaptable](/help/forms/using/assets/client-library-category-name-core-component.png)

En este caso, el nombre de la biblioteca de cliente se proporciona como `customfunctionsdemo` en el `.content.xml` archivo.

Para utilizar un controlador de errores personalizado utilizando la acción **[!UICONTROL Invocar servicio del Editor de reglas]**:

1. Abra el formulario adaptable en el modo de creación, seleccione cualquier objeto del formulario y pulse **[!UICONTROL Editor de reglas]** para abrir el editor de reglas.
1. Pulse **[!UICONTROL Crear]**.
1. Crear una condición en la sección **Cuando** de la regla. Por ejemplo, cuando se ha cambiado el **[Nombre del campo ID de mascota]**, seleccione **se ha cambiado** en la lista desplegable **Seleccionar estado**.
1. En la sección **Entonces**, seleccione **[!UICONTROL Invocar servicio]** de la lista desplegable **Seleccionar acción**.
1. Seleccione un **servicio Post** y sus enlaces de datos correspondientes en la sección **Entrada**. Por ejemplo, para validar **ID de mascota**, seleccione un **servicio Post** como **GET /pet/{petId}** y seleccione **ID de mascota** en la sección **Entrada**.
1. Seleccione los enlaces de datos en la sección **Salida**. Por ejemplo, seleccione **Nombre de mascota** en la sección **Salida**.
1. Seleccione **[!UICONTROL Controlador de errores personalizado]** en la sección **[!UICONTROL Controlador de errores]**.
1. Haga clic en **[!UICONTROL Listo]**.

![añadir un controlador de errores personalizado en un formulario para controlar las respuestas de error](/help/forms/using/assets/custom-error-handler.png)

Como resultado de esta regla, los valores introducidos para **ID de mascota** comprueban la validación de **Nombre de mascota** utilizando el servicio externo invocado por el punto final REST. Si los criterios de validación basados en la fuente de datos fallan, los mensajes de error se muestran en el nivel de campo.

![añadir un controlador de error personalizado en un formulario para controlar las respuestas de error](/help/forms/using/assets/custom-error-handler-message-core-component.png)

Abra la consola del explorador y compruebe la respuesta y el encabezado, recibidos del punto final de servicio REST, para el mensaje de error de validación.

La función del controlador de errores personalizado es responsable de ejecutar acciones adicionales, como mostrar un cuadro de diálogo modal o enviar un evento de análisis, en función de la respuesta de error. Una función del controlador de errores personalizado proporciona la flexibilidad para adaptar la gestión de errores a los requisitos específicos del usuario.
