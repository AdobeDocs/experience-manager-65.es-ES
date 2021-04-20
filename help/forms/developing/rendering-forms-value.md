---
title: Representar Forms por valor
seo-title: Representar Forms por valor
description: Utilice la API de Forms (Java) para procesar un formulario por valor mediante la API de Java y la API de servicio web.
seo-description: Utilice la API de Forms (Java) para procesar un formulario por valor mediante la API de Java y la API de servicio web.
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 0%

---


# Renderización de Forms por valor {#rendering-forms-by-value}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

Normalmente, un diseño de formulario creado en Designer se pasa por referencia al servicio Forms. Los diseños de formulario pueden ser grandes y, como resultado, es más eficaz pasarlos por referencia para evitar tener que calcular los bytes de diseño de formulario por valor. El servicio Forms también puede almacenar en caché el diseño de formulario para que, cuando se almacena en caché, no tenga que leer continuamente el diseño de formulario.

Si un diseño de formulario contiene un atributo UUID, se almacena en la caché. El valor UUID es único para todos los diseños de formulario y se utiliza para identificar un formulario de forma única. Al procesar un formulario por valor, solo se debe almacenar en caché cuando se utiliza repetidamente. Sin embargo, si el formulario no se utiliza repetidamente y tiene que ser único, puede evitar el procesamiento en la caché mediante las opciones de almacenamiento en caché establecidas mediante la API de AEM Forms.

El servicio Forms también puede resolver la ubicación del contenido vinculado dentro del diseño de formulario. Por ejemplo, las imágenes vinculadas a las que se hace referencia desde el diseño de formulario son direcciones URL relativas. Siempre se asume que el contenido vinculado es relativo a la ubicación del diseño de formulario. Por lo tanto, la resolución del contenido vinculado depende de si se determina su ubicación aplicando la ruta relativa a la ubicación absoluta del diseño de formulario.

En lugar de pasar un diseño de formulario por referencia, puede pasar un diseño de formulario por valor. Pasar un diseño de formulario por valor es eficaz cuando se crea dinámicamente un diseño de formulario; es decir, cuando una aplicación cliente genera el XML que crea un diseño de formulario durante la ejecución. En este caso, un diseño de formulario no se almacena en un repositorio físico porque está almacenado en la memoria. Al crear dinámicamente un diseño de formulario en tiempo de ejecución y pasarlo por valor, puede almacenar el formulario en caché y mejorar el rendimiento del servicio Forms.

**Limitaciones de pasar un formulario por valor**

Las siguientes limitaciones se aplican cuando un diseño de formulario pasa por valor:

* No puede haber contenido relacionado dentro del diseño de formulario. Todas las imágenes y fragmentos deben incrustarse dentro del diseño de formulario o incluirse en una referencia absoluta.
* Los cálculos del lado del servidor no se pueden realizar después de procesar el formulario. Si el formulario se envía de nuevo al servicio de Forms, los datos se extraen y se devuelven sin ningún cálculo del lado del servidor.
* Como HTML solo puede utilizar imágenes vinculadas en tiempo de ejecución, no es posible generar HTML con imágenes incrustadas. Esto se debe a que el servicio Forms admite imágenes incrustadas con HTML recuperando las imágenes de un diseño de formulario al que se hace referencia. Dado que un diseño de formulario que se pasa por valor no tiene una ubicación a la que se hace referencia, las imágenes incrustadas no se pueden extraer cuando se muestra la página HTML. Por lo tanto, las referencias de imagen deben ser rutas absolutas para que se representen en HTML.

>[!NOTE]
>
>Aunque se pueden procesar distintos tipos de formularios por valor (por ejemplo, formularios HTML o formularios que contienen derechos de uso), en esta sección se trata la representación de PDF forms interactivos.

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para procesar un formulario por valor, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Haga referencia al diseño de formulario.
1. Representar un formulario por valor.
1. Escriba el flujo de datos del formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de cliente de Forms**

Para poder importar datos mediante programación a una API de cliente de formulario PDF, debe crear un cliente de servicio de integración de datos. Al crear un cliente de servicio, define la configuración de conexión necesaria para invocar un servicio.

**Referencia al diseño de formulario**

Al procesar un formulario por valor, debe crear un objeto `com.adobe.idp.Document` que contenga el diseño de formulario que se va a procesar. Puede hacer referencia a un archivo XDP existente o crear dinámicamente un diseño de formulario en tiempo de ejecución y rellenar un `com.adobe.idp.Document` con esos datos.

>[!NOTE]
>
>Esta sección y el inicio rápido correspondiente hacen referencia a un archivo XDP existente.

**Representar un formulario por valor**

Para procesar un formulario por valor, pase una instancia `com.adobe.idp.Document` que contenga el diseño de formulario al parámetro `inDataDoc` del método de renderización (puede ser cualquiera de los métodos de renderización del objeto `FormsServiceClient` como `renderPDFForm`, `(Deprecated) renderHTMLForm`, etc.). Normalmente, este valor de parámetro se reserva para los datos combinados con el formulario. Del mismo modo, pase un valor de cadena vacío al parámetro `formQuery`. Normalmente, este parámetro requiere un valor de cadena que especifique el nombre del diseño de formulario.

>[!NOTE]
>
>Si desea mostrar datos dentro del formulario, los datos deben especificarse dentro del elemento `xfa:datasets` . Para obtener información sobre la arquitectura XFA, vaya a [https://partners.adobe.com/public/developer/xml/index_arch.html](https://partners.adobe.com/public/developer/xml/index_arch.html).

**Escribir el flujo de datos del formulario en el explorador web del cliente**

Cuando el servicio Forms procesa un formulario por valor, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el explorador web del cliente, el formulario es visible para el usuario.

**Consulte también**

[Representar un formulario por valor utilizando la API de Java](#render-a-form-by-value-using-the-java-api)

[Representar un formulario por valor utilizando la API de servicio web](#render-a-form-by-value-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Pasar documentos al servicio de Forms](/help/forms/developing/passing-documents-forms-service.md)

[Creación de aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Representar un formulario por valor utilizando la API de Java {#render-a-form-by-value-using-the-java-api}

Representar un formulario por valor utilizando la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-forms-client.jar, en la ruta de clase de su proyecto Java.

1. Creación de un objeto de API de cliente de Forms

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Referencia al diseño de formulario

   * Cree un objeto `java.io.FileInputStream` que represente el diseño de formulario que se va a procesar empleando su constructor y pasando un valor de cadena que especifique la ubicación del archivo XDP.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Representar un formulario por valor

   Invoque el método `FormsServiceClient` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena vacío. (Normalmente, este parámetro requiere un valor de cadena que especifique el nombre del diseño de formulario).
   * Un objeto `com.adobe.idp.Document` que contiene el diseño de formulario. Normalmente, este valor de parámetro se reserva para los datos combinados con el formulario.
   * Un objeto `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. Se trata de un parámetro opcional y puede especificar `null` si no desea especificar opciones en tiempo de ejecución.
   * Un objeto `URLSpec` que contiene valores de URI necesarios para el servicio Forms.
   * Un objeto `java.util.HashMap` que almacena archivos adjuntos. Se trata de un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `renderPDFForm` devuelve un objeto `FormsResult` que contiene un flujo de datos de formulario que se puede escribir en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `com.adobe.idp.Document` invocando el método `FormsResult` del objeto ‘s `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `com.adobe.idp.Document` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `com.adobe.idp.Document`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir el flujo de datos del formulario en el explorador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree un objeto `java.io.InputStream` invocando el método `com.adobe.idp.Document` del objeto `getInputStream`.
   * Cree una matriz de bytes y asigne el tamaño del objeto `InputStream`. Invoque el método `InputStream` del objeto `available` para obtener el tamaño del objeto `InputStream`.
   * Rellene la matriz de bytes con la secuencia de datos del formulario invocando el método `InputStream` del objeto `read` y pasando la matriz de bytes como argumento.
   * Invoque el método `javax.servlet.ServletOutputStream` del objeto `write` para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Representar Forms por valor](/help/forms/developing/rendering-forms.md)

[Inicio rápido (modo SOAP): Renderización por valor utilizando la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Representar un formulario por valor utilizando la API de servicio web {#render-a-form-by-value-using-the-web-service-api}

Representar un formulario por valor utilizando la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clase.

1. Creación de un objeto de API de cliente de Forms

   Cree un objeto `FormsService` y establezca valores de autenticación.

1. Referencia al diseño de formulario

   * Cree un objeto `java.io.FileInputStream` utilizando su constructor. Pase un valor de cadena que especifique la ubicación del archivo XDP.
   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF cifrado con una contraseña.
   * Cree una matriz de bytes que almacene el contenido del objeto `java.io.FileInputStream`. Puede determinar el tamaño de la matriz de bytes obteniendo el tamaño del objeto `java.io.FileInputStream` mediante su método `available`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `java.io.FileInputStream` del objeto `read` y pasando la matriz de bytes.
   * Rellene el objeto `BLOB` invocando su método `setBinaryData` y pasando la matriz de bytes.

1. Representar un formulario por valor

   Invoque el método `FormsService` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena vacío. (Normalmente, este parámetro requiere un valor de cadena que especifique el nombre del diseño de formulario).
   * Un objeto `BLOB` que contiene el diseño de formulario. Normalmente, este valor de parámetro se reserva para los datos combinados con el formulario.
   * Un objeto `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. Se trata de un parámetro opcional y puede especificar `null` si no desea especificar opciones en tiempo de ejecución.
   * Un objeto `URLSpec` que contiene valores de URI necesarios para el servicio Forms.
   * Un objeto `java.util.HashMap` que almacena archivos adjuntos. Se trata de un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un objeto `com.adobe.idp.services.holders.BLOBHolder` vacío que se rellena con el método . Se utiliza para almacenar el formulario PDF procesado.
   * Un objeto `javax.xml.rpc.holders.LongHolder` vacío que se rellena con el método . (Este argumento almacena el número de páginas del formulario).
   * Un objeto `javax.xml.rpc.holders.StringHolder` vacío que se rellena con el método . (Este argumento almacena el valor de configuración regional).
   * Un objeto `com.adobe.idp.services.holders.FormsResultHolder` vacío que contendrá los resultados de esta operación.

   El método `renderPDFForm` rellena el objeto `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `FormResult` obteniendo el valor del miembro de datos `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value`.
   * Cree un objeto `BLOB` que contenga datos de formulario invocando el método `FormsResult` del objeto `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `BLOB` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `BLOB`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir el flujo de datos del formulario en el explorador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData`. Esta tarea asigna el contenido del objeto `FormsResult` a la matriz de bytes.
   * Invoque el método `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Representar Forms por valor](#rendering-forms-by-value)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
