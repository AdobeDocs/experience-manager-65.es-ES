---
title: Procesar formularios por valor
description: Utilice la API de Forms (Java) para procesar un formulario por valor mediante la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: a3a6a06d-ec90-4147-a5f0-e776a086ee12
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '1822'
ht-degree: 1%

---

# Procesar formularios por valor {#rendering-forms-by-value}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Normalmente, un diseño de formulario creado en Designer se pasa por referencia al servicio de Forms. Los diseños de formulario pueden ser grandes y, como resultado, es más eficaz pasarlos por referencia para evitar tener que calcular las referencias de los bytes de diseño de formulario por valor. El servicio Forms también puede almacenar en caché el diseño de formulario para que, cuando se almacene en caché, no tenga que leer continuamente el diseño de formulario.

Si un diseño de formulario contiene un atributo UUID, se almacena en caché. El valor UUID es único para todos los diseños de formulario y se utiliza para identificar un formulario de forma exclusiva. Al procesar un formulario por valor, el formulario solo debe almacenarse en caché cuando se utiliza repetidamente. Sin embargo, si el formulario no se utiliza repetidamente y debe ser único, puede evitar almacenar en caché el formulario mediante las opciones de almacenamiento en caché establecidas mediante la API de AEM Forms.

El servicio Forms también puede resolver la ubicación del contenido vinculado dentro del diseño de formulario. Por ejemplo, las imágenes vinculadas a las que se hace referencia desde el diseño de formulario son direcciones URL relativas. Se supone que el contenido vinculado siempre es relativo a la ubicación del diseño del formulario. Por lo tanto, para resolver el contenido vinculado es necesario determinar su ubicación aplicando la ruta relativa a la ubicación absoluta del diseño de formulario.

En lugar de pasar un diseño de formulario por referencia, puede pasar un diseño de formulario por valor. Pasar un diseño de formulario por valor es eficaz cuando se crea dinámicamente un diseño de formulario; es decir, cuando una aplicación cliente genera el XML que crea un diseño de formulario durante el tiempo de ejecución. En este caso, un diseño de formulario no se almacena en un repositorio físico porque se almacena en la memoria. Al crear dinámicamente un diseño de formulario en tiempo de ejecución y pasarlo por valor, puede almacenar en caché el formulario y mejorar el rendimiento del servicio de Forms.

**Limitaciones al pasar un formulario por valor**

Cuando se pasa un diseño de formulario por valor, se aplican las siguientes limitaciones:

* No se puede incluir contenido vinculado relativo dentro del diseño de formulario. Todas las imágenes y fragmentos deben incrustarse dentro del diseño de formulario o deben mencionarse absolutamente.
* Los cálculos del lado del servidor no se pueden realizar después de procesar el formulario. Si el formulario se devuelve al servicio Forms, los datos se extraen y se devuelven sin ningún cálculo del lado del servidor.
* Como HTML solo puede utilizar imágenes vinculadas en tiempo de ejecución, no es posible generar un HTML con imágenes incrustadas. Esto se debe a que el servicio Forms admite imágenes incrustadas con HTML al recuperar las imágenes de un diseño de formulario al que se hace referencia. Dado que un diseño de formulario transferido por un valor no tiene una ubicación a la que se haga referencia, las imágenes incrustadas no se pueden extraer cuando se muestra la página del HTML. Por lo tanto, las referencias de imagen deben ser rutas absolutas para que se representen en HTML.

>[!NOTE]
>
>Aunque se pueden procesar distintos tipos de formularios por valor (por ejemplo, formularios de HTML o formularios que contengan derechos de uso), en esta sección se describe la representación de PDF forms interactivos.

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para procesar un formulario por valor, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Hacer referencia al diseño de formulario.
1. Procesar un formulario por valor.
1. Escriba el flujo de datos del formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Forms**

Para poder importar datos mediante programación en una API de cliente de formulario de PDF, debe crear un cliente de servicio de integración de datos. Al crear un cliente de servicios, define la configuración de conexión necesaria para invocar un servicio.

**Hacer referencia al diseño de formulario**

Al procesar un formulario por valor, debe crear un `com.adobe.idp.Document` que contiene el diseño de formulario que se va a procesar. Puede hacer referencia a un archivo XDP existente o puede crear dinámicamente un diseño de formulario en tiempo de ejecución y rellenar un `com.adobe.idp.Document` con esos datos.

>[!NOTE]
>
>Esta sección y el inicio rápido correspondiente hacen referencia a un archivo XDP existente.

**Procesar un formulario por valor**

Para procesar un formulario por valor, pase un `com.adobe.idp.Document` instancia que contiene el diseño de formulario en el método de procesamiento `inDataDoc` parámetro (puede ser cualquiera de las `FormsServiceClient` métodos de procesamiento del objeto, como `renderPDFForm`, `(Deprecated) renderHTMLForm`, etc.). Este valor de parámetro se reserva normalmente para los datos que se combinan con el formulario. Del mismo modo, pase un valor de cadena vacío a `formQuery` parámetro. Normalmente, este parámetro requiere un valor de cadena que especifica el nombre del diseño de formulario.

>[!NOTE]
>
>Si desea mostrar datos dentro del formulario, los datos deben especificarse dentro del `xfa:datasets` Elemento. Para obtener información acerca de la arquitectura XFA, vaya a [https://www.pdfa.org/norm-refs/XFA-3_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf).

**Escribir el flujo de datos del formulario en el explorador web del cliente**

Cuando el servicio Forms procesa un formulario por valor, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el explorador web del cliente, el formulario es visible para el usuario.

**Consulte también**

[Procesar un formulario por valor mediante la API de Java](#render-a-form-by-value-using-the-java-api)

[Procesar un formulario por valor mediante la API de servicio web](#render-a-form-by-value-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Pasar documentos al servicio de Forms](/help/forms/developing/passing-documents-forms-service.md)

[Crear aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Procesar un formulario por valor mediante la API de Java {#render-a-form-by-value-using-the-java-api}

Procesar un formulario por valor mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de Forms

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `FormsServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Hacer referencia al diseño de formulario

   * Crear un `java.io.FileInputStream` que representa el diseño de formulario que se va a procesar mediante su constructor y pasando un valor de cadena que especifica la ubicación del archivo XDP.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Procesar un formulario por valor

   Invoque el `FormsServiceClient` del objeto `renderPDFForm` y pasar los siguientes valores:

   * Un valor de cadena vacío. (Normalmente, este parámetro requiere un valor de cadena que especifica el nombre del diseño de formulario).
   * A `com.adobe.idp.Document` que contiene el diseño de formulario. Normalmente, este valor de parámetro se reserva para los datos que se combinan con el formulario.
   * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. Este es un parámetro opcional y puede especificar `null` si no desea especificar opciones en tiempo de ejecución.
   * A `URLSpec` que contiene valores de URI requeridos por el servicio de Forms.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El `renderPDFForm` El método devuelve un valor `FormsResult` que contiene un flujo de datos de formulario que se puede escribir en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Crear un `com.adobe.idp.Document` invocando el objeto de `FormsResult` del objeto `getOutputContent` método.
   * Obtenga el tipo de contenido del `com.adobe.idp.Document` invocando su objeto `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasando el tipo de contenido del `com.adobe.idp.Document` objeto.
   * Crear un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Crear un `java.io.InputStream` invocando el objeto de `com.adobe.idp.Document` del objeto `getInputStream` método.
   * Cree una matriz de bytes y asigne el tamaño del `InputStream` objeto. Invoque el `InputStream` del objeto `available` para obtener el tamaño del objeto `InputStream` objeto.
   * Rellene la matriz de bytes con el flujo de datos de formulario invocando el método `InputStream` del objeto `read`y pasando la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

**Consulte también**

[Procesar formularios por valor](/help/forms/developing/rendering-forms.md)

[Inicio rápido (modo SOAP): Procesamiento por valor mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Procesar un formulario por valor mediante la API de servicio web {#render-a-form-by-value-using-the-web-service-api}

Procesar un formulario por valor utilizando la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases de proxy Java en la ruta de clase.

1. Crear un objeto de API de cliente de Forms

   Crear un `FormsService` y establezca los valores de autenticación.

1. Hacer referencia al diseño de formulario

   * Crear un `java.io.FileInputStream` mediante su constructor. Pase un valor de cadena que especifique la ubicación del archivo XDP.
   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar un documento de PDF cifrado con una contraseña.
   * Cree una matriz de bytes que almacene el contenido del `java.io.FileInputStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `java.io.FileInputStream` tamaño del objeto con su `available` método.
   * Rellene la matriz de bytes con datos de flujo invocando el método `java.io.FileInputStream` del objeto `read` y pasando la matriz de bytes.
   * Rellene el `BLOB` invocando su objeto `setBinaryData` y pasando la matriz de bytes.

1. Procesar un formulario por valor

   Invoque el `FormsService` del objeto `renderPDFForm` y pasar los siguientes valores:

   * Un valor de cadena vacío. (Normalmente, este parámetro requiere un valor de cadena que especifica el nombre del diseño de formulario).
   * A `BLOB` que contiene el diseño de formulario. Normalmente, este valor de parámetro se reserva para los datos que se combinan con el formulario.
   * A `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. Este es un parámetro opcional y puede especificar `null` si no desea especificar opciones en tiempo de ejecución.
   * A `URLSpec` que contiene valores de URI requeridos por el servicio de Forms.
   * A `java.util.HashMap` que almacena archivos adjuntos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un vacío `com.adobe.idp.services.holders.BLOBHolder` objeto que rellena el método. Se utiliza para almacenar el formulario de PDF procesado.
   * Un vacío `javax.xml.rpc.holders.LongHolder` objeto que rellena el método. (Este argumento almacena el número de páginas del formulario.)
   * Un vacío `javax.xml.rpc.holders.StringHolder` objeto que rellena el método. (Este argumento almacena el valor de configuración regional.)
   * Un vacío `com.adobe.idp.services.holders.FormsResultHolder` que contendrá los resultados de esta operación.

   El `renderPDFForm` rellena el método `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con un flujo de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Crear un `FormResult` al obtener el valor de la variable `com.adobe.idp.services.holders.FormsResultHolder` del objeto `value` miembro de datos.
   * Crear un `BLOB` que contiene datos de formulario invocando el `FormsResult` del objeto `getOutputContent` método.
   * Obtenga el tipo de contenido del `BLOB` invocando su objeto `getContentType` método.
   * Configure las variables `javax.servlet.http.HttpServletResponse` tipo de contenido del objeto invocando su `setContentType` y pasando el tipo de contenido del `BLOB` objeto.
   * Crear un `javax.servlet.ServletOutputStream` objeto utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream` método.
   * Cree una matriz de bytes y rellénela invocando el método `BLOB` del objeto `getBinaryData` método. Esta tarea asigna el contenido del `FormsResult` a la matriz de bytes.
   * Invoque el `javax.servlet.http.HttpServletResponse` del objeto `write` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes a `write` método.

**Consulte también**

[Procesar formularios por valor](#rendering-forms-by-value)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
