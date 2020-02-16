---
title: Invocación de formularios AEM mediante solicitudes REST
seo-title: Invocación de formularios AEM mediante solicitudes REST
description: nulo
seo-description: nulo
uuid: 3a19a296-f3fe-4e50-9143-b68aed37f9ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: df7b60bb-4897-479e-a05e-1b1e9429ed87
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Invocación de formularios AEM mediante solicitudes REST {#invoking-aem-forms-using-rest-requests}

Los procesos creados en Workbench se pueden configurar para que pueda invocarlos mediante solicitudes de transferencia de estado representativa (REST). Las solicitudes REST se envían desde páginas HTML. Es decir, puede invocar un proceso de Forms directamente desde una página web mediante una solicitud REST. Por ejemplo, puede abrir una nueva instancia de una página web. A continuación, puede invocar un proceso de Forms y cargar un documento PDF procesado con datos enviados en una solicitud HTTP POST.

Existen dos tipos de clientes HTML. El primer cliente HTML es un cliente AJAX que está escrito en JavaScript. El segundo cliente es un formulario HTML que contiene un botón de envío. Una aplicación cliente basada en HTML no es el único cliente REST posible. Cualquier aplicación cliente que admita solicitudes HTTP puede invocar un servicio mediante una invocación REST. Por ejemplo, puede invocar un servicio mediante una invocación REST desde un formulario PDF. (Consulte [Invocación del proceso MyApplication/EncryptDocument desde Acrobat](#rest-invocation-examples)).

Cuando se utilizan solicitudes REST, se recomienda no invocar los servicios de Forms directamente. En su lugar, invoque procesos creados en Workbench. Cuando cree un proceso que esté diseñado para la invocación de REST, utilice un punto de inicio programático. En este caso, el extremo REST se agrega automáticamente. Para obtener información sobre la creación de procesos en Workbench, consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Al invocar un servicio mediante REST, se le pedirá un nombre de usuario y una contraseña para los formularios AEM. Sin embargo, si no desea especificar un nombre de usuario y una contraseña, puede desactivar la seguridad del servicio.

Para invocar un servicio Forms (un proceso se convierte en un servicio cuando se activa el proceso) mediante REST, configure un extremo REST. (Consulte &quot;Administración de extremos&quot; en la ayuda [de](https://www.adobe.com/go/learn_aemforms_admin_63)administración).

Una vez configurado un extremo REST, puede invocar un servicio Forms mediante un método HTTP GET o un método POST.

```as3
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

El valor obligatorio `ServiceName` es el nombre del servicio Forms que se va a invocar. El valor opcional `OperationName` es el nombre de la operación del servicio. Si no se especifica este valor, el nombre predeterminado es `invoke`, que es el nombre de la operación que inicia el proceso. El valor opcional `ServiceVersion` es la versión codificada en formato X.Y. Si no se especifica este valor, se utiliza la versión más reciente. El `enctype` valor también puede ser `application/x-www-form-urlencoded`.

## Tipos de datos admitidos {#supported-data-types}

Se admiten los siguientes tipos de datos al invocar servicios de AEM Forms mediante solicitudes REST:

* Tipos de datos primitivos de Java, como cadenas e enteros
* `com.adobe.idp.Document` tipo de datos
* Tipos de datos XML como `org.w3c.Document` y `org.w3c.Element`
* Objetos de colección como `java.util.List` y `java.util.Map`

   Estos tipos de datos suelen aceptarse como valores de entrada para procesos creados en Workbench.

   Si se invoca un servicio Forms con el método HTTP POST, los argumentos se pasan dentro del cuerpo de la solicitud HTTP. Si la firma del servicio AEM Forms tiene un parámetro de entrada de cadena, el cuerpo de la solicitud puede contener el valor de texto del parámetro de entrada. Si la firma del servicio define varios parámetros de cadena, la solicitud puede seguir la `application/x-www-form-urlencoded` notación de HTTP con los nombres de parámetro utilizados como nombres de campo del formulario.

   Si un servicio Forms devuelve un parámetro de cadena, el resultado es una representación textual del parámetro de salida. Si un servicio devuelve varios parámetros de cadena, el resultado es un documento XML que codifica los parámetros de salida en el siguiente formato:
   ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`**Nota **: El`output-paramater1`valor representa el nombre del parámetro de salida.

   Si un servicio Forms requiere un `com.adobe.idp.Document` parámetro, solo se puede invocar el servicio mediante el método HTTP POST. Si el servicio requiere un `com.adobe.idp.Document` parámetro, el cuerpo de la solicitud HTTP se convierte en el contenido del objeto Document de entrada.

   Si un servicio de AEM Forms requiere varios parámetros de entrada, el cuerpo de la solicitud HTTP debe ser un mensaje MIME de varias partes, tal como se define en RFC 1867. (RFC 1867 es un estándar que utilizan los navegadores web para cargar archivos en sitios web). Cada parámetro de entrada debe enviarse como una parte independiente del mensaje de varias partes y codificarse en el `multipart/form-data` formato. El nombre de cada pieza debe coincidir con el nombre del parámetro.

   Las listas y los mapas también se utilizan como valores de entrada para los procesos de AEM Forms creados en Workbench. Como resultado, puede utilizar estos tipos de datos al utilizar una solicitud REST. No se admiten matrices Java porque no se utilizan como valor de entrada en un proceso de AEM Forms.

   Si un parámetro de entrada es una lista, un cliente REST puede enviarlo especificando el parámetro varias veces (una para cada elemento de la lista). Por ejemplo, si A es una lista de documentos, la entrada debe ser un mensaje de varias partes compuesto por varias partes denominadas A. En este caso, cada parte llamada A se convierte en un elemento de la lista de entrada. Si B es una lista de cadenas, la entrada puede ser un `application/x-www-form-urlencoded` mensaje que consta de varios campos denominados B. En este caso, cada campo de formulario denominado B se convierte en un elemento de la lista de entrada.

   Si un parámetro de entrada es un mapa y es el parámetro de entrada solo de servicios, cada parte/campo del mensaje de entrada se convierte en un registro de clave/valor en el mapa. El nombre de cada pieza o campo se convierte en la clave del registro. El contenido de cada pieza o campo se convierte en el valor del registro.

   Si un mapa de entrada no es el parámetro de entrada solo de servicios, cada registro clave/valor que pertenece al mapa se puede enviar usando un parámetro denominado como concatenación del nombre del parámetro y la clave del registro. Por ejemplo, un mapa de entrada llamado `attributes` se puede enviar con una lista de los siguientes pares de clave/valores:

   `attributesColor=red`

   `attributesShape=box`

   `attributesWidth=5`

   Esto se traduce en un mapa de tres registros: `Color=red`, `Shape=box`, y `Width=5`.

   Los parámetros de salida de la lista y los tipos de mapa pasan a formar parte del mensaje XML resultante. La lista de resultados se representa en XML como una serie de elementos XML con un elemento por cada elemento de la lista. Cada elemento recibe el mismo nombre que el parámetro de lista de resultados. El valor de cada elemento XML es una de las dos cosas:

* Una representación de texto del elemento de la lista (si la lista consta de tipos de cadena)
* Dirección URL que apunta al contenido del documento (si la lista consta de `com.adobe.idp.Document` objetos)

   El siguiente ejemplo es un mensaje XML devuelto por un servicio que tiene un solo parámetro de salida denominado *list*, que es una lista de enteros.
   ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`Un parámetro de mapa de salida se representa en el mensaje XML resultante como una serie de elementos XML con un elemento para cada registro del mapa. Cada elemento recibe el mismo nombre que la clave del registro del mapa. El valor de cada elemento es una representación textual del valor del registro del mapa (si el mapa consta de registros con un valor de cadena) o una dirección URL que apunta al contenido del documento (si el mapa consta de registros con el `com.adobe.idp.Document` valor). A continuación se muestra un ejemplo de un mensaje XML devuelto por un servicio que tiene un solo parámetro de salida denominado `map`. Este valor de parámetro es un mapa que consta de registros que asocian letras con `com.adobe.idp.Document` objetos.
   ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## Invocaciones asincrónicas {#asynchronous-invocations}

Algunos servicios de AEM Forms, como los procesos de larga duración centrados en el ser humano, requieren mucho tiempo para completarse. Estos servicios se pueden invocar de forma asíncrona y sin bloqueo. (Consulte [Invocación De Procesos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)Largos Centrados En El Hombre).

Un servicio de AEM Forms se puede invocar asincrónicamente sustituyendo `services` por `async_invoke` en la URL de invocación, como se muestra en el siguiente ejemplo.

```as3
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

Esta URL devuelve el valor de identificador (en formato &quot;text/plain&quot;) del trabajo responsable de esta invocación.

El estado de la invocación asincrónica se puede recuperar utilizando una URL de invocación con `services` sustitución por `async_status`. La dirección URL debe contener un `job_id` parámetro que especifique el valor de identificador del trabajo asociado con esta invocación. Por ejemplo:

```as3
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

Esta URL devuelve un valor entero (en formato &quot;text/plain&quot;) que codifica el estado del trabajo según la especificación del Administrador de trabajos (por ejemplo, 2 significa que se está ejecutando, 3 significa completado, 4 significa que se ha producido un error, etc.).

Si se completa el trabajo, la dirección URL devuelve el mismo resultado que si el servicio se hubiera invocado sincrónicamente.

Una vez finalizado el trabajo y recuperado el resultado, el trabajo se puede eliminar usando una URL de invocación con la que `services` se sustituye por `async_dispose`. La dirección URL también debe contener un `job_id` parámetro que especifique el valor de identificador del trabajo. Por ejemplo:

```as3
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

Si el trabajo se elimina correctamente, esta URL devuelve un mensaje vacío.

## Informes de errores {#error-reporting}

Si no se puede completar una solicitud de invocación sincrónica o asincrónica debido a una excepción que se está generando en el servidor, la excepción se notifica como parte del mensaje de respuesta HTTP. Si la URL de invocación (o la `async_result` URL en caso de una invocación asincrónica) no tiene un sufijo .xml, el proveedor de REST devuelve el código HTTP `500 Internal Server Error` seguido de un mensaje de excepción.

Si la URL de invocación (o la `async_result` URL en caso de una invocación asincrónica) tiene un sufijo .xml, el proveedor de REST devuelve el código HTTP `200 OK`seguido de un documento XML que describe la excepción en el siguiente formato.

```as3
 <exception>
       <exception_class_name>[
       <DSCError>
          <componentUID>component_UUD</componentUID>
         <errorCode>error_code</errorCode>
         <minorCode>minor_code</minorCode>
         <message>error_message</message>
       </DSCError>
 ]
       <message>exception_message</message>
     <stackTrace>exception_stack_trace</stackTrace>
       </exception_class_name>
     <exception>
       </exception>
 </exception>
```

El `DSCError` elemento es opcional y solo está presente si la excepción es una instancia de `com.adobe.idp.dsc.DSCException`.

## Seguridad y autenticación {#security-and-authentication}

Para proporcionar un transporte seguro a las invocaciones REST, un administrador de formularios AEM puede activar el protocolo HTTPS en el servidor de aplicaciones J2EE que aloja AEM Forms. Esta configuración es específica del servidor de aplicaciones J2EE; no forma parte de la configuración del servidor de formularios.

>[!NOTE]
>
>Como desarrollador de Workbench que desea exponer sus procesos a través de un punto final de REST, tenga en cuenta el problema de vulnerabilidad XSS. Las vulnerabilidades XSS pueden utilizarse para robar o manipular cookies, modificar la presentación del contenido y comprometer la información confidencial. Se recomienda ampliar la lógica del proceso con las reglas de validación de datos de entrada y salida adicionales si existe algún problema con la vulnerabilidad XSS.

## Servicios de AEM Forms que admiten invocación REST {#aem-forms-services-that-support-rest-invocation}

Aunque se recomienda invocar procesos creados con Workbench en lugar de servicios directamente, hay algunos servicios de AEM Forms que sí admiten la invocación de REST. El motivo por el que se recomienda que invoque un proceso en lugar de un servicio directamente es porque es más eficaz invocar un proceso. Considere el siguiente escenario. Supongamos que desea crear una directiva a partir de un cliente REST. Es decir, desea que el cliente REST defina valores como el nombre de la política, el período de concesión sin conexión.

Para crear una directiva, debe definir tipos de datos complejos como un `PolicyEntry` objeto. Un `PolicyEntry` objeto define atributos como los permisos asociados a la política. (Consulte [Creación de políticas](/help/forms/developing/protecting-documents-policies.md#creating-policies).)

En lugar de enviar una solicitud REST para crear una directiva (que incluiría la definición de tipos de datos complejos como un `PolicyEntry` objeto), cree un proceso que cree una directiva mediante Workbench. Defina el proceso para aceptar variables de entrada primitivas, como un valor de cadena que define el nombre del proceso o un entero que define el período de concesión sin conexión.

De este modo, no es necesario crear una solicitud de invocación REST que incluya tipos de datos complejos que requiera la operación. El proceso define los tipos de datos complejos y todo lo que se hace desde el cliente REST es invocar el proceso y pasar tipos de datos primitivos. Para obtener información sobre cómo invocar un proceso mediante REST, consulte [Invocación del proceso MyApplication/EncryptDocument mediante REST](#rest-invocation-examples).

Las listas siguientes especifican los servicios de AEM Forms que admiten la invocación directa de REST.

* Servicio Distiller
* Servicio Rights Management
* Servicio GeneratePDF
* Servicio Generate3dPDF
* FormDataIntegration

## Ejemplos de invocación de REST {#rest-invocation-examples}

Se proporcionan los siguientes ejemplos de invocación de REST:

* Pasar valores booleanos a un proceso de AEM Forms
* Pasar valores de fecha a un proceso de AEM Forms
* Paso de documentos a un proceso de AEM Forms
* Pasar valores de documento y texto a un proceso de AEM Forms
* Pasar valores de enumeración a un proceso de AEM Forms
* Invocación del proceso MyApplication/EncryptDocument mediante REST
* Invocación del proceso MyApplication/EncryptDocument desde Acrobat

   Cada ejemplo muestra cómo pasar distintos tipos de datos a un proceso de AEM Forms

**Pasar valores booleanos a un proceso**

El siguiente ejemplo HTML pasa dos `Boolean` valores a un proceso de AEM Forms denominado `RestTest2`. El nombre del método de invocación es `invoke` y la versión es 1.0. Tenga en cuenta que se utiliza el método Post HTML.

```as3
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest2/invoke/1.0" method="post">
 
 Boolean 1: <input type="text" name="inBooleanList" value="true">
 Boolean 2: <input type="text" name="inBooleanList" value="false">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**Pasar valores de fecha a un proceso**

El siguiente ejemplo HTML pasa un valor de fecha a un proceso de AEM Forms denominado `SOAPEchoService`. El nombre del método de invocación es `echoCalendar`. Observe que se utiliza el método HTML `Post` .

```as3
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/SOAPEchoService/echoCalendar" method="post">
 
 Date: <input type="text" name="value-to-echo" value="2009-01-02T12:15:30Z">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**Pasar documentos a un proceso**

El siguiente ejemplo HTML invoca un proceso de AEM Forms denominado `MyApplication/EncryptDocument` que requiere un documento PDF. Para obtener información sobre este proceso, consulte [Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).

```as3
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/MyApplication/EncryptDocument/invoke" method="post"
          enctype="multipart/form-data">
 
 File: <input type="file" name="value-to-echo">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**Pasar valores de documento y texto a un proceso**

El siguiente ejemplo HTML invoca un proceso de AEM Forms denominado `RestTest3` que requiere un documento y dos valores de texto.  Tenga en cuenta que se utiliza el método Post HTML.

```as3
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest3" method="post"
          enctype="multipart/form-data">
 
 Doc: <input type="file" name="inDoc">
 String 1: <input type="text" name="inListOfStrings" value="hello">
 String 2: <input type="text" name="inListOfStrings" value="privet">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**Pasar valores de enumeración a un proceso**

El siguiente ejemplo HTML invoca un proceso de AEM Forms denominado `SOAPEchoService` que requiere un valor de enumeración.  Tenga en cuenta que se utiliza el método Post HTML.

```as3
 <html>
 <body>
 
 <form name="input" action="https://hiro-xp:8080/rest/services/SOAPEchoService/echoEnum" method="post">
 
 Color Enum Value: <input type="text" name="value-to-echo" value="green">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**Invocación del proceso MyApplication/EncryptDocument mediante REST**

Puede invocar un proceso de corta duración de AEM Forms denominado *MyApplication/EncryptDocument* mediante REST.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para seguir el ejemplo de código, cree un proceso denominado `MyApplication/EncryptDocument` mediante Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento PDF no seguro que se pasa al proceso. Esta acción se basa en la `SetValue` operación. El parámetro de entrada para este proceso es una variable de `document` proceso denominada `inDoc`.
1. Codifica el documento PDF con una contraseña. Esta acción se basa en la `PasswordEncryptPDF` operación. El documento PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

   Cuando se invoca este proceso mediante una solicitud REST, el documento PDF codificado se muestra en el navegador web. Antes de ver el documento PDF, debe especificar la contraseña (a menos que la seguridad esté deshabilitada). El siguiente código HTML representa una solicitud de invocación REST para el `MyApplication/EncryptDocument` proceso.

   ```as3
    <html>
    <body>
    <form action="https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument" method="post" enctype="multipart/form-data">
         <p>Chose a PDF file (.pdf) to send to the EncryptDocument process.</p>
         <p>file:
           <input type="file" name="inDoc" />
         </p>
         <p>
           <input type="submit"/>
         </p>
    </form>
    </body>
   ```

**Invocación del proceso MyApplication/EncryptDocument desde Acrobat**{#invoke-process-acrobat}

Puede invocar un proceso de formularios desde Acrobat mediante una solicitud REST. Por ejemplo, puede invocar el proceso *MyApplication/EncryptDocument* . Para invocar un proceso de formularios desde Acrobat, coloque un botón de envío en un archivo XDP dentro de Designer. (Consulte la Ayuda [de](https://www.adobe.com/go/learn_aemforms_designer_63)Designer).

Especifique la URL para invocar el proceso en el campo *Enviar a URL* del botón, como se muestra en la siguiente ilustración.

La dirección URL completa para invocar el proceso es https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument.

Si el proceso requiere un documento PDF como valor de entrada, asegúrese de enviar el formulario como PDF, como se muestra en la ilustración anterior. Además, para invocar correctamente un proceso, el proceso debe devolver un documento PDF. De lo contrario, Acrobat no puede gestionar el valor devuelto y se produce un error. No es necesario especificar el nombre de la variable del proceso de entrada. Por ejemplo, el proceso *MyApplication/EncryptDocument* tiene una variable de entrada denominada `inDoc`. No es necesario especificar enDoc, siempre que el formulario se envíe como PDF.

También puede enviar datos de formulario como XML a un proceso de Forms. Para enviar datos XML, asegúrese de que la `Submit As` lista desplegable especifica XML. Dado que el valor devuelto por el proceso debe ser un documento PDF, el documento PDF se muestra en Acrobat.
