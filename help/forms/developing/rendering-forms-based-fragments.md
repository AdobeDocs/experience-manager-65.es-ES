---
title: Representación de formularios basados en fragmentos
seo-title: Representación de formularios basados en fragmentos
description: nulo
seo-description: nulo
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Representación de formularios basados en fragmentos {#rendering-forms-based-on-fragments}

## Representación de formularios basados en fragmentos {#rendering-forms-based-on-fragments-inner}

El servicio Forms puede procesar formularios basados en fragmentos creados con Designer. Un *fragmento* es una parte reutilizable de un formulario y se guarda como un archivo XDP independiente que se puede insertar en varios diseños de formulario. Por ejemplo, un fragmento puede incluir un bloque de direcciones o texto legal.

El uso de fragmentos simplifica y acelera la creación y el mantenimiento de una gran cantidad de formularios. Al crear un nuevo formulario, se inserta una referencia al fragmento requerido y éste aparece en el formulario. La referencia de fragmento contiene un subformulario que señala al archivo XDP físico. Para obtener información sobre la creación de diseños de formulario basados en fragmentos, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Un fragmento puede incluir varios subformularios ajustados en un conjunto de subformularios de opciones. Los conjuntos de subformularios de opciones controlan la visualización de subformularios en función del flujo de datos de una conexión de datos. Se utilizan afirmaciones condicionales para determinar qué subformulario del conjunto aparece en el formulario entregado. Por ejemplo, cada subformulario de un conjunto puede incluir información de una ubicación geográfica determinada y el subformulario que se muestra puede determinarse en función de la ubicación del usuario.

A *script fragment* contains reusable JavaScript functions or values that are stored separately from any particular object, such as a date parser or a web service invocation. Estos fragmentos incluyen un único objeto de secuencia de comandos que aparece como un elemento secundario de variables en la paleta Jerarquía. Los fragmentos no pueden crearse a partir de secuencias de comandos que sean propiedades de otros objetos, tales como secuencias de comandos de sucesos validate, calculate o initialize.

A continuación se indican las ventajas de utilizar fragmentos:

* **Reutilización** del contenido: Puede utilizar fragmentos para reutilizar el contenido en varios diseños de formulario. Cuando necesite utilizar parte del mismo contenido en varios formularios, es más rápido y sencillo utilizar un fragmento que copiar o volver a crear el contenido. El uso de fragmentos también garantiza que las partes de un diseño de formulario utilizadas con frecuencia tengan un contenido y un aspecto coherentes en todos los formularios de referencia.
* **Actualizaciones** globales: Puede utilizar fragmentos para realizar cambios globales en varios formularios solo una vez, en un archivo. Puede cambiar el contenido, los objetos de secuencia de comandos, los enlaces de datos, la presentación o los estilos de un fragmento, y todos los formularios XDP que hagan referencia al fragmento reflejarán los cambios.
* Por ejemplo, un elemento común en muchos formularios podría ser un bloque de direcciones que incluya un objeto de lista desplegable para el país. Si necesita actualizar los valores del objeto de lista desplegable, debe abrir muchos formularios para realizar los cambios. Si incluye el bloque de direcciones en un fragmento, solo necesita abrir un archivo de fragmento para realizar los cambios.
* Para actualizar un fragmento en un formulario PDF, debe volver a guardarlo en Designer.
* **Creación** de formularios compartidos: Puede utilizar fragmentos para compartir la creación de formularios entre varios recursos. Los desarrolladores de formularios con conocimientos de secuencias de comandos u otras funciones avanzadas de Designer pueden desarrollar y compartir fragmentos que aprovechan las secuencias de comandos y las propiedades dinámicas. Los diseñadores de formularios pueden utilizar tales fragmentos para presentar diseños de formulario y garantizar que todas las partes de un formulario tengan un aspecto y una funcionalidad coherentes en los múltiples formularios diseñados por varias personas.

### Compilación de un diseño de formulario ensamblado mediante fragmentos {#assembling-a-form-design-assembled-using-fragments}

Puede montar un diseño de formulario para pasarlo al servicio Forms en función de varios fragmentos. Para ensamblar varios fragmentos, utilice el servicio Ensamblador. Para ver un ejemplo del uso del servicio Compilación para crear un diseño de formulario que utilice otro servicio de Forms (el servicio Output), consulte [Creación de documentos PDF con fragmentos](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments). En lugar de utilizar el servicio Output, puede realizar el mismo flujo de trabajo con el servicio Forms.

Al utilizar el servicio Compilador, se pasa un diseño de formulario que se ensambló con fragmentos. El diseño de formulario creado no hace referencia a otros fragmentos. Por el contrario, en este tema se trata el paso de un diseño de formulario que hace referencia a otros fragmentos al servicio Forms. Sin embargo, el diseño de formulario no fue ensamblado por el Ensamblador. Se creó en Designer.

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener información sobre la creación de una aplicación basada en Web que procesa formularios basados en fragmentos, consulte [Creación de aplicaciones Web que procesan formularios](/help/forms/developing/creating-web-applications-renders-forms.md).

### Resumen de los pasos {#summary-of-steps}

Para procesar un formulario basado en fragmentos, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de Forms Client.
1. Especifique los valores de URI.
1. Representar el formulario.
1. Escriba la secuencia de datos del formulario en el navegador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Forms Client**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms.

**Especificar valores de URI**

Para procesar correctamente un formulario basado en fragmentos, debe asegurarse de que el servicio Forms puede localizar tanto el formulario como los fragmentos (archivos XDP) a los que hace referencia el diseño de formulario. Por ejemplo, supongamos que el formulario se denomina PO.xdp y que este formulario utiliza dos fragmentos denominados FooterUS.xdp y FooterCanada.xdp. En este caso, el servicio Forms debe poder localizar los tres archivos XDP.

Puede organizar un formulario y sus fragmentos colocándolo en una ubicación y los fragmentos en otra, o bien puede colocar todos los archivos XDP en la misma ubicación. A efectos de esta sección, supongamos que todos los archivos XDP se encuentran en el repositorio de AEM Forms. Para obtener información sobre la colocación de archivos XDP en el repositorio de AEM Forms, consulte [Escritura de recursos](/help/forms/developing/aem-forms-repository.md#writing-resources).

Cuando se procesa un formulario basado en fragmentos, solo se debe hacer referencia al propio formulario y no a los fragmentos. Por ejemplo, debe hacer referencia a PO.xdp y no a FooterUS.xdp o FooterCanada.xdp. Asegúrese de colocar los fragmentos en una ubicación en la que el servicio Forms pueda localizarlos.

**Representar el formulario**

Un formulario basado en fragmentos se puede procesar del mismo modo que los formularios no fragmentados. Es decir, puede procesar el formulario como PDF, HTML o guías de formulario (obsoleto). El ejemplo de esta sección representa un formulario basado en fragmentos como un formulario PDF interactivo. (Consulte [Representación de formularios](/help/forms/developing/rendering-interactive-pdf-forms.md)PDF interactivos).

**Escribir el flujo de datos del formulario en el navegador web del cliente**

Cuando el servicio Forms procesa un formulario, devuelve una secuencia de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el navegador web del cliente, el formulario es visible para el usuario.

**Consulte también**

[Representar formularios en función de fragmentos mediante la API de Java](#render-forms-based-on-fragments-using-the-java-api)

[Representar formularios en función de fragmentos mediante la API de servicio web](#render-forms-based-on-fragments-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de formularios](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Representación de formularios PDF interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Creación de aplicaciones Web que procesan formularios](/help/forms/developing/creating-web-applications-renders-forms.md)

### Representar formularios en función de fragmentos mediante la API de Java {#render-forms-based-on-fragments-using-the-java-api}

Representar un formulario basado en fragmentos mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Forms Client

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `FormsServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Especificar valores de URI

   * Cree un `URLSpec` objeto que almacene valores URI mediante su constructor.
   * Invoque el `URLSpec` método del `setApplicationWebRoot` objeto y pase un valor de cadena que represente la raíz web de la aplicación.
   * Invoque el `URLSpec` método del `setContentRootURI` objeto y pase un valor de cadena que especifique el valor de URI raíz del contenido. Asegúrese de que el diseño de formulario y los fragmentos están ubicados en el URI raíz de contenido. De lo contrario, el servicio Forms genera una excepción. Para hacer referencia al repositorio, especifique `repository://`.
   * Invoque el `URLSpec` método del `setTargetURL` objeto y pase un valor de cadena que especifique el valor de la dirección URL de destino al que se registran los datos del formulario. Si define la dirección URL de destino en el diseño de formulario, puede pasar una cadena vacía. También puede especificar la dirección URL a la que se envía un formulario para realizar cálculos.

1. Representar el formulario

   Invoque el `FormsServiceClient` método del `renderPDFForm` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un `com.adobe.idp.Document` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un `com.adobe.idp.Document` objeto vacío.
   * Un `PDFFormRenderSpec` objeto que almacena opciones de tiempo de ejecución.
   * Un `URLSpec` objeto que contiene valores URI que el servicio Forms requiere para procesar un formulario basado en fragmentos.
   * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   El `renderPDFForm` método devuelve un `FormsResult` objeto que contiene una secuencia de datos de formulario que se debe escribir en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un `com.adobe.idp.Document` objeto invocando el `FormsResult` método ‘s `getOutputContent` .
   * Obtenga el tipo de contenido del `com.adobe.idp.Document` objeto invocando su `getContentType` método.
   * Defina el tipo de contenido del `javax.servlet.http.HttpServletResponse` objeto invocando su `setContentType` método y pasando el tipo de contenido del `com.adobe.idp.Document` objeto.
   * Cree un `javax.servlet.ServletOutputStream` objeto que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el `javax.servlet.http.HttpServletResponse` método `getOutputStream` del objeto.
   * Cree un `java.io.InputStream` objeto invocando el `com.adobe.idp.Document` método `getInputStream` del objeto.
   * Cree una matriz de bytes para rellenarla con la secuencia de datos del formulario invocando el `InputStream` método del `read`objeto y pasando la matriz de bytes como argumento.
   * Invoque el `javax.servlet.ServletOutputStream` método del `write` objeto para enviar la secuencia de datos del formulario al explorador web del cliente. Pase la matriz de bytes al `write` método .

**Consulte también**

[Representación de formularios basados en fragmentos](#rendering-forms-based-on-fragments)

[Inicio rápido (modo SOAP): Representación de un formulario basado en fragmentos mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Representar formularios en función de fragmentos mediante la API de servicio web {#render-forms-based-on-fragments-using-the-web-service-api}

Representar un formulario basado en fragmentos mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases proxy de Java que consuman el WSDL del servicio Forms.
   * Incluya las clases proxy de Java en la ruta de clases.

1. Creación de un objeto de API de Forms Client

   Cree un `FormsService` objeto y defina los valores de autenticación.

1. Especificar valores de URI

   * Cree un `URLSpec` objeto que almacene valores de URI mediante su constructor.
   * Invoque el `URLSpec` método del `setApplicationWebRoot` objeto y pase un valor de cadena que represente la raíz web de la aplicación.
   * Invoque el `URLSpec` método del `setContentRootURI` objeto y pase un valor de cadena que especifique el valor de URI raíz del contenido. Asegúrese de que el diseño de formulario se encuentra en el URI raíz de contenido. De lo contrario, el servicio Forms genera una excepción. Para hacer referencia al repositorio, especifique `repository://`.
   * Invoque el `URLSpec` método del `setTargetURL` objeto y pase un valor de cadena que especifique el valor de la dirección URL de destino al que se registran los datos del formulario. Si define la dirección URL de destino en el diseño de formulario, puede pasar una cadena vacía. También puede especificar la dirección URL a la que se envía un formulario para realizar cálculos.

1. Representar el formulario

   Invoque el `FormsService` método del `renderPDFForm` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un `BLOB` objeto que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`.
   * Un `PDFFormRenderSpec` objeto que almacena opciones de tiempo de ejecución. Tenga en cuenta que la opción PDF con etiquetas no se puede establecer si el documento de entrada es un documento PDF. Si el archivo de entrada es un archivo XDP, se puede establecer la opción PDF con etiquetas.
   * Un `URLSpec` objeto que contiene valores URI requeridos por el servicio Forms.
   * Un `java.util.HashMap` objeto que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el método . Este parámetro se utiliza para almacenar el formulario procesado.
   * Objeto vacío `javax.xml.rpc.holders.LongHolder` que se rellena con el método . Este argumento almacenará el número de páginas del formulario.
   * Objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el método . Este argumento almacenará el valor de configuración regional.
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

[Representación de formularios basados en fragmentos](#rendering-forms-based-on-fragments)

[Invocación de formularios AEM con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
