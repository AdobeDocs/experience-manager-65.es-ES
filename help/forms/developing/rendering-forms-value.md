---
title: Representar Forms por valor
seo-title: Rendering Forms By Value
description: Utilice la API de Forms (Java) para procesar un formulario por valor mediante la API de Java y la API de servicio web.
seo-description: Use the Forms API (Java) to render a form by value using the Java API and Web Service API.
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
role: Developer
exl-id: a3a6a06d-ec90-4147-a5f0-e776a086ee12
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '1835'
ht-degree: 0%

---

# Representar Forms por valor {#rendering-forms-by-value}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

Normalmente, un diseño de formulario creado en Designer se pasa por referencia al servicio Forms. Los diseños de formulario pueden ser grandes y, como resultado, es más eficaz pasarlos por referencia para evitar tener que calcular los bytes de diseño de formulario por valor. El servicio Forms también puede almacenar en caché el diseño de formulario para que, cuando se almacena en caché, no tenga que leer continuamente el diseño de formulario.

Si un diseño de formulario contiene un atributo UUID, se almacena en la caché. El valor UUID es único para todos los diseños de formulario y se utiliza para identificar un formulario de forma única. Al procesar un formulario por valor, solo se debe almacenar en caché cuando se utiliza repetidamente. Sin embargo, si el formulario no se utiliza repetidamente y tiene que ser único, puede evitar el procesamiento en la caché mediante las opciones de almacenamiento en caché establecidas mediante la API de AEM Forms.

El servicio Forms también puede resolver la ubicación del contenido vinculado dentro del diseño de formulario. Por ejemplo, las imágenes vinculadas a las que se hace referencia desde el diseño de formulario son direcciones URL relativas. Siempre se asume que el contenido vinculado es relativo a la ubicación del diseño de formulario. Por lo tanto, la resolución del contenido vinculado depende de si se determina su ubicación aplicando la ruta relativa a la ubicación absoluta del diseño de formulario.

En lugar de pasar un diseño de formulario por referencia, puede pasar un diseño de formulario por valor. Pasar un diseño de formulario por valor es eficaz cuando se crea dinámicamente un diseño de formulario; es decir, cuando una aplicación cliente genera el XML que crea un diseño de formulario durante la ejecución. En este caso, un diseño de formulario no se almacena en un repositorio físico porque está almacenado en la memoria. Al crear dinámicamente un diseño de formulario en tiempo de ejecución y pasarlo por valor, puede almacenar el formulario en caché y mejorar el rendimiento del servicio Forms.

**Limitaciones de pasar un formulario por valor**

Las siguientes limitaciones se aplican cuando un diseño de formulario pasa por valor:

* No puede haber contenido relacionado dentro del diseño de formulario. Todas las imágenes y fragmentos deben incrustarse dentro del diseño de formulario o incluirse en una referencia absoluta.
* Los cálculos del lado del servidor no se pueden realizar después de procesar el formulario. Si el formulario se envía de nuevo al servicio de Forms, los datos se extraen y se devuelven sin ningún cálculo del lado del servidor.
* Como HTML solo puede utilizar imágenes vinculadas en tiempo de ejecución, no es posible generar HTML con imágenes incrustadas. Esto se debe a que el servicio Forms admite imágenes incrustadas con HTML recuperando las imágenes de un diseño de formulario al que se hace referencia. Dado que un diseño de formulario que se pasa por valor no tiene una ubicación a la que se hace referencia, las imágenes incrustadas no se pueden extraer cuando se muestra la página HTML. Por lo tanto, las referencias de imagen deben ser rutas absolutas para que se representen en el HTML.

>[!NOTE]
>
>Aunque puede procesar diferentes tipos de formularios por valor (por ejemplo, formularios HTML o formularios que contienen derechos de uso), en esta sección se trata la renderización de PDF forms interactivos.

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

Para poder importar datos mediante programación a una API de cliente de formulario de PDF, debe crear un cliente de servicio de integración de datos. Al crear un cliente de servicio, define la configuración de conexión necesaria para invocar un servicio.

**Referencia al diseño de formulario**

Al procesar un formulario por valor, debe crear un `com.adobe.idp.Document` objeto que contiene el diseño de formulario que se va a procesar. Puede hacer referencia a un archivo XDP existente o crear dinámicamente un diseño de formulario en tiempo de ejecución y rellenar un `com.adobe.idp.Document` con esos datos.

>[!NOTE]
>
>Esta sección y el inicio rápido correspondiente hacen referencia a un archivo XDP existente.

**Representar un formulario por valor**

Para procesar un formulario por valor, pase un `com.adobe.idp.Document` instancia que contiene el diseño de formulario en el `inDataDoc` (puede ser cualquiera de los `FormsServiceClient` métodos de renderización del objeto, como `renderPDFForm`, `(Deprecated) renderHTMLForm`, etc.). Normalmente, este valor de parámetro se reserva para los datos combinados con el formulario. Del mismo modo, pase un valor de cadena vacío a la variable `formQuery` parámetro. Normalmente, este parámetro requiere un valor de cadena que especifique el nombre del diseño de formulario.

>[!NOTE]
>
>Si desea mostrar datos dentro del formulario, los datos deben especificarse dentro de la variable `xfa:datasets` elemento. Para obtener información sobre la arquitectura XFA, vaya a [https://www.pdfa.org/norm-refs/XFA-3_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf).

**Escribir el flujo de datos del formulario en el explorador web del cliente**

Cuando el servicio Forms procesa un formulario por valor, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el explorador web del cliente, el formulario es visible para el usuario.

**Consulte también lo siguiente**

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

   * Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión.
   * Cree un `FormsServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto.

1. Referencia al diseño de formulario

   * Cree un `java.io.FileInputStream` objeto que representa el diseño de formulario que se va a procesar utilizando su constructor y pasando un valor de cadena que especifica la ubicación del archivo XDP.
   * Cree un `com.adobe.idp.Document` usando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Representar un formulario por valor

   Invocar el `FormsServiceClient` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena vacío. (Normalmente, este parámetro requiere un valor de cadena que especifique el nombre del diseño de formulario).
   * A `com.adobe.idp.Document` objeto que contiene el diseño de formulario. Normalmente, este valor de parámetro se reserva para los datos combinados con el formulario.
   * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. Este es un parámetro opcional y puede especificar `null` si no desea especificar opciones de tiempo de ejecución.
   * A `URLSpec` que contiene valores de URI necesarios para el servicio Forms.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   La variable `renderPDFForm` el método devuelve un `FormsResult` objeto que contiene una secuencia de datos de formulario que se puede escribir en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un `com.adobe.idp.Document` invocando el objeto `FormsResult` objeto ‘s `getOutputContent` método.
   * Obtenga el tipo de contenido de la variable `com.adobe.idp.Document` invocando su `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasar el tipo de contenido de la variable `com.adobe.idp.Document` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos del formulario en el explorador web del cliente invocando la variable `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree un `java.io.InputStream` invocando el objeto `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y asigne el tamaño de la variable `InputStream` objeto. Invocar el `InputStream` del objeto `available` para obtener el tamaño de la variable `InputStream` objeto.
   * Rellene la matriz de bytes con la secuencia de datos del formulario invocando la variable `InputStream` del objeto `read`y pasando la matriz de bytes como argumento.
   * Invocar el `javax.servlet.ServletOutputStream` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.

**Consulte también lo siguiente**

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

   Cree un `FormsService` y establezca los valores de autenticación.

1. Referencia al diseño de formulario

   * Cree un `java.io.FileInputStream` usando su constructor. Pase un valor de cadena que especifique la ubicación del archivo XDP.
   * Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar un documento de PDF cifrado con una contraseña.
   * Cree una matriz de bytes que almacene el contenido del `java.io.FileInputStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `java.io.FileInputStream` tamaño del objeto utilizando su `available` método.
   * Rellene la matriz de bytes con los datos de flujo invocando la variable `java.io.FileInputStream` del objeto `read` y pasando la matriz de bytes.
   * Rellene el `BLOB` invocando su `setBinaryData` y pasando la matriz de bytes.

1. Representar un formulario por valor

   Invocar el `FormsService` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena vacío. (Normalmente, este parámetro requiere un valor de cadena que especifique el nombre del diseño de formulario).
   * A `BLOB` objeto que contiene el diseño de formulario. Normalmente, este valor de parámetro se reserva para los datos combinados con el formulario.
   * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. Este es un parámetro opcional y puede especificar `null` si no desea especificar opciones de tiempo de ejecución.
   * A `URLSpec` que contiene valores de URI necesarios para el servicio Forms.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que rellena el método . Se utiliza para almacenar el formulario de PDF procesado.
   * Un vacío `javax.xml.rpc.holders.LongHolder` objeto que rellena el método . (Este argumento almacena el número de páginas del formulario).
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el método . (Este argumento almacena el valor de configuración regional).
   * Un vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   La variable `renderPDFForm` rellena el `com.adobe.idp.services.holders.FormsResultHolder` objeto que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un `FormResult` obteniendo el valor de `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value` miembro de datos.
   * Cree un `BLOB` objeto que contiene datos de formulario invocando la variable `FormsResult` del objeto `getOutputContent` método.
   * Obtenga el tipo de contenido de la variable `BLOB` invocando su `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasar el tipo de contenido de la variable `BLOB` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos del formulario en el explorador web del cliente invocando la variable `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree una matriz de bytes y rellénela invocando la variable `BLOB` del objeto `getBinaryData` método. Esta tarea asigna el contenido de la variable `FormsResult` a la matriz de bytes.
   * Invocar el `javax.servlet.http.HttpServletResponse` del objeto `write` método para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes a la `write` método.

**Consulte también lo siguiente**

[Representar Forms por valor](#rendering-forms-by-value)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
