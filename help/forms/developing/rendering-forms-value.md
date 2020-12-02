---
title: Representación de Forms por valor
seo-title: Representación de Forms por valor
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
source-git-commit: 66bfd6870b4c09dc2ca1b66058e0b9e040a71507
workflow-type: tm+mt
source-wordcount: '1812'
ht-degree: 0%

---


# Representación de Forms por valor {#rendering-forms-by-value}

Normalmente, un diseño de formulario creado en Designer se pasa por referencia al servicio Forms. Los diseños de formulario pueden ser grandes y, como resultado, es más eficaz pasarlos por referencia para evitar tener que calcular los bytes de diseño de formulario por valor. El servicio Forms también puede almacenar en caché el diseño de formulario para que, cuando se almacena en caché, no tenga que leer continuamente el diseño de formulario.

Si un diseño de formulario contiene un atributo UUID, se almacena en la caché. El valor UUID es único para todos los diseños de formulario y se utiliza para identificar un formulario de forma única. Cuando se procesa un formulario por valor, el formulario solo se debe almacenar en caché cuando se utiliza repetidamente. Sin embargo, si el formulario no se utiliza repetidamente y tiene que ser único, puede evitar guardar el formulario en la caché mediante las opciones de almacenamiento en caché que se establecen con la API de AEM Forms.

El servicio Forms también puede resolver la ubicación del contenido vinculado dentro del diseño de formulario. Por ejemplo, las imágenes vinculadas a las que se hace referencia desde el diseño de formulario son direcciones URL relativas. Siempre se da por hecho que el contenido vinculado es relativo a la ubicación del diseño de formulario. Por lo tanto, resolver el contenido vinculado es una cuestión que consiste en determinar su ubicación aplicando la ruta relativa a la ubicación absoluta del diseño de formulario.

En lugar de pasar un diseño de formulario por referencia, puede pasar un diseño de formulario por valor. Transmitir un diseño de formulario por valor resulta eficaz cuando se crea dinámicamente un diseño de formulario; es decir, cuando una aplicación cliente genera el XML que crea un diseño de formulario durante la ejecución. En este caso, un diseño de formulario no se almacena en un repositorio físico porque se almacena en la memoria. Al crear dinámicamente un diseño de formulario en tiempo de ejecución y pasarlo por valor, puede almacenar en caché el formulario y mejorar el rendimiento del servicio Forms.

**Limitaciones de pasar un formulario por valor**

Las siguientes limitaciones se aplican cuando un diseño de formulario se pasa por valor:

* No puede haber contenido vinculado relativo en el diseño de formulario. Todas las imágenes y los fragmentos deben incrustarse dentro del diseño de formulario o hacerse referencia a ellos de forma absoluta.
* Los cálculos del lado del servidor no se pueden realizar después de procesar el formulario. Si el formulario se devuelve al servicio Forms, los datos se extraen y devuelven sin ningún cálculo del lado del servidor.
* Dado que HTML solo puede utilizar imágenes vinculadas en tiempo de ejecución, no es posible generar HTML con imágenes incrustadas. Esto se debe a que el servicio Forms admite imágenes incrustadas con HTML recuperando las imágenes de un diseño de formulario al que se hace referencia. Dado que un diseño de formulario que se pasa por valor no tiene una ubicación a la que se hace referencia, las imágenes incrustadas no se pueden extraer cuando se muestra la página HTML. Por lo tanto, las referencias de imagen deben ser rutas absolutas para procesarse en HTML.

>[!NOTE]
>
>Aunque puede procesar distintos tipos de formularios por valor (por ejemplo, formularios HTML o formularios que contienen derechos de uso), en esta sección se trata la representación de PDF forms interactivos.

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para procesar un formulario por valor, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Haga referencia al diseño de formulario.
1. Representar un formulario por valor.
1. Escriba la secuencia de datos del formulario en el navegador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Forms Client**

Para poder importar datos mediante programación en una API de cliente de formulario PDF, debe crear un cliente de servicio de integración de datos. Al crear un cliente de servicio, se define la configuración de conexión necesaria para invocar un servicio.

**Hacer referencia al diseño de formulario**

Al procesar un formulario por valor, debe crear un objeto `com.adobe.idp.Document` que contenga el diseño de formulario que se va a procesar. Puede hacer referencia a un archivo XDP existente o puede crear dinámicamente un diseño de formulario en tiempo de ejecución y rellenar un `com.adobe.idp.Document` con esos datos.

>[!NOTE]
>
>Esta sección y el inicio rápido correspondiente hacen referencia a un archivo XDP existente.

**Representar un formulario por valor**

Para procesar un formulario por valor, pase una instancia `com.adobe.idp.Document` que contenga el diseño de formulario al parámetro `inDataDoc` del método de procesamiento (puede ser cualquiera de los métodos de procesamiento del objeto `FormsServiceClient` como `renderPDFForm`, `(Deprecated) renderHTMLForm`, etc.). Normalmente, este valor de parámetro se reserva a los datos que se combinan con el formulario. Del mismo modo, pase un valor de cadena vacío al parámetro `formQuery`. Normalmente, este parámetro requiere un valor de cadena que especifica el nombre del diseño de formulario.

>[!NOTE]
>
>Si desea mostrar datos dentro del formulario, los datos deben especificarse dentro del elemento `xfa:datasets`. Para obtener información sobre la arquitectura XFA, vaya a [https://partners.adobe.com/public/developer/xml/index_arch.html](https://partners.adobe.com/public/developer/xml/index_arch.html).

**Escribir el flujo de datos del formulario en el navegador web del cliente**

Cuando el servicio Forms procesa un formulario por valor, devuelve una secuencia de datos de formulario que debe escribir en el explorador Web del cliente. Cuando se escribe en el navegador web del cliente, el formulario es visible para el usuario.

**Consulte también**

[Representar un formulario por valor mediante la API de Java](#render-a-form-by-value-using-the-java-api)

[Representación de un formulario por valor mediante la API de servicio Web](#render-a-form-by-value-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API de servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Pasar Documentos al servicio Forms](/help/forms/developing/passing-documents-forms-service.md)

[Creación de Aplicaciones web que procesan Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Representar un formulario por valor mediante la API de Java {#render-a-form-by-value-using-the-java-api}

Representar un formulario por valor mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Forms Client

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia al diseño de formulario

   * Cree un objeto `java.io.FileInputStream` que represente el diseño de formulario que se va a procesar mediante su constructor y pasando un valor de cadena que especifique la ubicación del archivo XDP.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Representar un formulario por valor

   Invoque el método `FormsServiceClient` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena vacío. (Normalmente, este parámetro requiere un valor de cadena que especifica el nombre del diseño de formulario).
   * Un objeto `com.adobe.idp.Document` que contiene el diseño de formulario. Normalmente, este valor de parámetro está reservado para datos que se combinan con el formulario.
   * Un objeto `PDFFormRenderSpec` que almacena opciones de tiempo de ejecución. Es un parámetro opcional y puede especificar `null` si no desea especificar opciones de tiempo de ejecución.
   * Un objeto `URLSpec` que contiene valores de URI necesarios para el servicio de Forms.
   * Objeto `java.util.HashMap` que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `renderPDFForm` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario que se puede escribir en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un objeto `com.adobe.idp.Document` invocando el método `FormsResult` del objeto ‘s `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `com.adobe.idp.Document` invocando su método `getContentType`.
   * Configure el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `com.adobe.idp.Document`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree un objeto `java.io.InputStream` invocando el método `com.adobe.idp.Document` del objeto `getInputStream`.
   * Cree una matriz de bytes y asigne el tamaño del objeto `InputStream`. Invoque el método `InputStream` del objeto `available` para obtener el tamaño del objeto `InputStream`.
   * Rellene la matriz de bytes con la secuencia de datos del formulario invocando el método `InputStream` del objeto `read`y pasando la matriz de bytes como argumento.
   * Invoque el método `javax.servlet.ServletOutputStream` del objeto `write` para enviar la secuencia de datos del formulario al explorador Web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Representación de Forms por valor](/help/forms/developing/rendering-forms.md)

[Inicio rápido (modo SOAP): Representación por valor mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Representar un formulario por valor mediante la API de servicio Web {#render-a-form-by-value-using-the-web-service-api}

Representar un formulario por valor mediante la API de Forms (servicio Web):

1. Incluir archivos de proyecto

   * Cree clases proxy de Java que consuman el WSDL del servicio de Forms.
   * Incluya las clases proxy de Java en la ruta de clases.

1. Creación de un objeto de API de Forms Client

   Cree un objeto `FormsService` y defina los valores de autenticación.

1. Hacer referencia al diseño de formulario

   * Cree un objeto `java.io.FileInputStream` utilizando su constructor. Pase un valor de cadena que especifique la ubicación del archivo XDP.
   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF cifrado con una contraseña.
   * Cree una matriz de bytes que almacene el contenido del objeto `java.io.FileInputStream`. Puede determinar el tamaño de la matriz de bytes obteniendo el tamaño del objeto `java.io.FileInputStream` mediante su método `available`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `java.io.FileInputStream` del objeto `read` y pasando la matriz de bytes.
   * Rellene el objeto `BLOB` invocando su método `setBinaryData` y pasando la matriz de bytes.

1. Representar un formulario por valor

   Invoque el método `FormsService` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena vacío. (Normalmente, este parámetro requiere un valor de cadena que especifica el nombre del diseño de formulario).
   * Un objeto `BLOB` que contiene el diseño de formulario. Normalmente, este valor de parámetro está reservado para datos que se combinan con el formulario.
   * Un objeto `PDFFormRenderSpec` que almacena opciones de tiempo de ejecución. Es un parámetro opcional y puede especificar `null` si no desea especificar opciones de tiempo de ejecución.
   * Un objeto `URLSpec` que contiene valores de URI necesarios para el servicio de Forms.
   * Objeto `java.util.HashMap` que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el método. Se utiliza para almacenar el formulario PDF procesado.
   * Un objeto vacío `javax.xml.rpc.holders.LongHolder` que se rellena con el método. (Este argumento almacena el número de páginas del formulario).
   * Un objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el método. (Este argumento almacena el valor de configuración regional).
   * Un objeto vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   El método `renderPDFForm` rellena el objeto `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con una secuencia de datos de formulario que debe escribirse en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un objeto `FormResult` obteniendo el valor del miembro de datos `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value`.
   * Cree un objeto `BLOB` que contenga datos de formulario invocando el método `FormsResult` del objeto `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `BLOB` invocando su método `getContentType`.
   * Configure el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `BLOB`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData`. Esta tarea asigna el contenido del objeto `FormsResult` a la matriz de bytes.
   * Invoque el método `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar la secuencia de datos del formulario al explorador Web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Representación de Forms por valor](#rendering-forms-by-value)

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
