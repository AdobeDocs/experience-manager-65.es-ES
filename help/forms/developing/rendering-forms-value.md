---
title: Representación de formularios por valor
seo-title: Representación de formularios por valor
description: nulo
seo-description: nulo
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Representación de formularios por valor {#rendering-forms-by-value}

Normalmente, un diseño de formulario creado en Designer se pasa por referencia al servicio Forms. Los diseños de formulario pueden ser grandes y, por tanto, es más eficaz pasarlos por referencia para evitar tener que calcular los bytes de diseño de formulario por valor. El servicio Forms también puede almacenar en caché el diseño de formulario para que, cuando se almacena en caché, no tenga que leer continuamente el diseño de formulario.

Si un diseño de formulario contiene un atributo UUID, se almacena en la caché. El valor UUID es único para todos los diseños de formulario y se utiliza para identificar un formulario de forma única. Cuando se procesa un formulario por valor, el formulario solo se debe almacenar en caché cuando se utiliza repetidamente. Sin embargo, si el formulario no se utiliza repetidamente y tiene que ser único, puede evitar la caché del formulario mediante las opciones de almacenamiento en caché que se establecen mediante la API de AEM Forms.

El servicio Forms también puede resolver la ubicación del contenido vinculado en el diseño de formulario. Por ejemplo, las imágenes vinculadas a las que se hace referencia desde el diseño de formulario son direcciones URL relativas. Siempre se da por hecho que el contenido vinculado es relativo a la ubicación del diseño de formulario. Por lo tanto, resolver el contenido vinculado es una cuestión que consiste en determinar su ubicación aplicando la ruta relativa a la ubicación absoluta del diseño de formulario.

En lugar de pasar un diseño de formulario por referencia, puede pasar un diseño de formulario por valor. Transmitir un diseño de formulario por valor resulta eficaz cuando se crea dinámicamente un diseño de formulario; es decir, cuando una aplicación cliente genera el XML que crea un diseño de formulario durante la ejecución. En este caso, un diseño de formulario no se almacena en un repositorio físico porque se almacena en la memoria. Al crear dinámicamente un diseño de formulario en tiempo de ejecución y pasarlo por valor, puede almacenar en caché el formulario y mejorar el rendimiento del servicio Forms.

**Limitaciones de pasar un formulario por valor**

Las siguientes limitaciones se aplican cuando un diseño de formulario se pasa por valor:

* No puede haber contenido vinculado relativo en el diseño de formulario. Todas las imágenes y los fragmentos deben incrustarse dentro del diseño de formulario o hacerse referencia a ellos de forma absoluta.
* Los cálculos del lado del servidor no se pueden realizar después de procesar el formulario. Si el formulario se devuelve al servicio Forms, los datos se extraen y devuelven sin ningún cálculo del lado del servidor.
* Dado que HTML solo puede utilizar imágenes vinculadas en tiempo de ejecución, no es posible generar HTML con imágenes incrustadas. Esto se debe a que el servicio Forms admite imágenes incrustadas con HTML recuperando las imágenes de un diseño de formulario al que se hace referencia. Dado que un diseño de formulario que se pasa por valor no tiene una ubicación a la que se hace referencia, las imágenes incrustadas no se pueden extraer cuando se muestra la página HTML. Por lo tanto, las referencias de imagen deben ser rutas absolutas para procesarse en HTML.

>[!NOTE]
>
>Aunque puede procesar diferentes tipos de formularios por valor (por ejemplo, formularios HTML o formularios que contienen derechos de uso), en esta sección se trata la representación de formularios PDF interactivos.

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para procesar un formulario por valor, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de Forms Client.
1. Haga referencia al diseño de formulario.
1. Representar un formulario por valor.
1. Escriba la secuencia de datos del formulario en el navegador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Forms Client**

Para poder importar datos mediante programación en una API de cliente de formulario PDF, debe crear un cliente de servicio de integración de datos. Al crear un cliente de servicio, se define la configuración de conexión necesaria para invocar un servicio.

**Hacer referencia al diseño de formulario**

Cuando se procesa un formulario por valor, hay que crear un `com.adobe.idp.Document` objeto que contenga el diseño de formulario que se va a procesar. Puede hacer referencia a un archivo XDP existente o puede crear dinámicamente un diseño de formulario en tiempo de ejecución y rellenar un `com.adobe.idp.Document` archivo con esos datos.

>[!NOTE]
>
>Esta sección y el inicio rápido correspondiente hacen referencia a un archivo XDP existente.

**Representar un formulario por valor**

Para procesar un formulario por valor, pase una `com.adobe.idp.Document` instancia que contenga el diseño de formulario al parámetro `inDataDoc` del método de procesamiento (puede ser cualquiera de los métodos de procesamiento del `FormsServiceClient` objeto, como `renderPDFForm`, `(Deprecated) renderHTMLForm`, etc.). Normalmente, este valor de parámetro se reserva a los datos que se combinan con el formulario. Del mismo modo, pase un valor de cadena vacío al `formQuery` parámetro. Normalmente, este parámetro requiere un valor de cadena que especifica el nombre del diseño de formulario.

>[!NOTE]
>
>Si desea mostrar datos dentro del formulario, los datos deben especificarse dentro del `xfa:datasets` elemento. Para obtener información sobre la arquitectura XFA, vaya a [https://partners.adobe.com/public/developer/xml/index_arch.html](https://partners.adobe.com/public/developer/xml/index_arch.html).

**Escribir el flujo de datos del formulario en el navegador web del cliente**

Cuando el servicio Forms procesa un formulario por valor, devuelve una secuencia de datos de formulario que debe escribir en el explorador Web del cliente. Cuando se escribe en el navegador web del cliente, el formulario es visible para el usuario.

**Consulte también**

[Representar un formulario por valor mediante la API de Java](#render-a-form-by-value-using-the-java-api)

[Representación de un formulario por valor mediante la API de servicio Web](#render-a-form-by-value-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de formularios](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Pasar documentos al servicio Forms](/help/forms/developing/passing-documents-forms-service.md)

[Creación de aplicaciones Web que procesan formularios](/help/forms/developing/creating-web-applications-renders-forms.md)

## Representar un formulario por valor mediante la API de Java {#render-a-form-by-value-using-the-java-api}

Representar un formulario por valor mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Forms Client

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `FormsServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Hacer referencia al diseño de formulario

   * Cree un `java.io.FileInputStream` objeto que represente el diseño de formulario que se va a procesar mediante su constructor y pasando un valor de cadena que especifique la ubicación del archivo XDP.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Representar un formulario por valor

   Invoque el `FormsServiceClient` método del `renderPDFForm` objeto y pase los valores siguientes:

   * Un valor de cadena vacío. (Normalmente, este parámetro requiere un valor de cadena que especifica el nombre del diseño de formulario).
   * Un `com.adobe.idp.Document` objeto que contiene el diseño de formulario. Normalmente, este valor de parámetro está reservado para datos que se combinan con el formulario.
   * Un `PDFFormRenderSpec` objeto que almacena opciones de tiempo de ejecución. Se trata de un parámetro opcional que puede especificar `null` si no desea especificar opciones de tiempo de ejecución.
   * Un `URLSpec` objeto que contiene valores de URI necesarios para el servicio Forms.
   * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   El `renderPDFForm` método devuelve un `FormsResult` objeto que contiene una secuencia de datos de formulario que se puede escribir en el navegador web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un `com.adobe.idp.Document` objeto invocando el `FormsResult` método ‘s `getOutputContent` .
   * Obtenga el tipo de contenido del `com.adobe.idp.Document` objeto invocando su `getContentType` método.
   * Defina el tipo de contenido del `javax.servlet.http.HttpServletResponse` objeto invocando su `setContentType` método y pasando el tipo de contenido del `com.adobe.idp.Document` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el `javax.servlet.http.HttpServletResponse` método `getOutputStream` del objeto.
   * Cree un `java.io.InputStream` objeto invocando el `com.adobe.idp.Document` método `getInputStream` del objeto.
   * Cree una matriz de bytes y asigne el tamaño del `InputStream` objeto. Invocar el `InputStream` método del `available` objeto para obtener el tamaño del `InputStream` objeto.
   * Rellene la matriz de bytes con la secuencia de datos del formulario invocando el `InputStream` método del `read`objeto y pasando la matriz de bytes como un argumento.
   * Invoque el `javax.servlet.ServletOutputStream` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .

**Consulte también**

[Representación de formularios por valor](/help/forms/develop/procesando-formularios-procesando-formularios-procesando-formularios-formulario-valor-procesando-formularios.md#procesando-formularios-por-valor)

[Inicio rápido (modo SOAP): Representación por valor mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Representación de un formulario por valor mediante la API de servicio Web {#render-a-form-by-value-using-the-web-service-api}

Representar un formulario por valor mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases proxy de Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clases.

1. Creación de un objeto de API de Forms Client

   Cree un `FormsService` objeto y defina los valores de autenticación.

1. Hacer referencia al diseño de formulario

   * Cree un `java.io.FileInputStream` objeto con su constructor. Pase un valor de cadena que especifique la ubicación del archivo XDP.
   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento PDF codificado con una contraseña.
   * Cree una matriz de bytes que almacene el contenido del `java.io.FileInputStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el tamaño del `java.io.FileInputStream` objeto mediante su `available` método.
   * Rellene la matriz de bytes con datos de flujo invocando el `java.io.FileInputStream` método del `read` objeto y pasando la matriz de bytes.
   * Rellene el `BLOB` objeto invocando su `setBinaryData` método y pasando la matriz de bytes.

1. Representar un formulario por valor

   Invoque el `FormsService` método del `renderPDFForm` objeto y pase los valores siguientes:

   * Un valor de cadena vacío. (Normalmente, este parámetro requiere un valor de cadena que especifica el nombre del diseño de formulario).
   * Un `BLOB` objeto que contiene el diseño de formulario. Normalmente, este valor de parámetro está reservado para datos que se combinan con el formulario.
   * Un `PDFFormRenderSpec` objeto que almacena opciones de tiempo de ejecución. Se trata de un parámetro opcional que puede especificar `null` si no desea especificar opciones de tiempo de ejecución.
   * Un `URLSpec` objeto que contiene valores de URI necesarios para el servicio Forms.
   * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el método . Se utiliza para almacenar el formulario PDF procesado.
   * Objeto vacío `javax.xml.rpc.holders.LongHolder` que se rellena con el método . (Este argumento almacena el número de páginas del formulario).
   * Objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el método . (Este argumento almacena el valor de configuración regional).
   * Un `com.adobe.idp.services.holders.FormsResultHolder` objeto vacío que contendrá los resultados de esta operación.
   El `renderPDFForm` método rellena el `com.adobe.idp.services.holders.FormsResultHolder` objeto que se pasa como el último valor de argumento con una secuencia de datos de formulario que se debe escribir en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un `FormResult` objeto obteniendo el valor del `com.adobe.idp.services.holders.FormsResultHolder` miembro de `value` datos del objeto.
   * Cree un `BLOB` objeto que contenga datos de formulario invocando el `FormsResult` método `getOutputContent` del objeto.
   * Obtenga el tipo de contenido del `BLOB` objeto invocando su `getContentType` método.
   * Defina el tipo de contenido del `javax.servlet.http.HttpServletResponse` objeto invocando su `setContentType` método y pasando el tipo de contenido del `BLOB` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el `javax.servlet.http.HttpServletResponse` método `getOutputStream` del objeto.
   * Cree una matriz de bytes y rellénela invocando el `BLOB` método `getBinaryData` del objeto. Esta tarea asigna el contenido del `FormsResult` objeto a la matriz de bytes.
   * Invoque el `javax.servlet.http.HttpServletResponse` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .

**Consulte también**

[Representación de formularios por valor](#rendering-forms-by-value)

[Invocación de formularios AEM con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
