---
title: Representación de Forms según fragmentos
seo-title: Representación de Forms según fragmentos
description: Utilice el servicio Forms para procesar formularios basados en fragmentos creados con Designer.
seo-description: Utilice el servicio Forms para procesar formularios basados en fragmentos creados con Designer.
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2215'
ht-degree: 7%

---


# Representación de Forms en base a fragmentos {#rendering-forms-based-on-fragments}

## Representación de Forms en base a fragmentos {#rendering-forms-based-on-fragments-inner}

El servicio Forms puede procesar formularios basados en fragmentos creados con Designer. Un *fragmento* es una parte reutilizable de un formulario y se guarda como un archivo XDP independiente que se puede insertar en varios diseños de formulario. Por ejemplo, un fragmento puede incluir un bloque de direcciones o texto legal.

El uso de fragmentos simplifica y acelera la creación y el mantenimiento de una gran cantidad de formularios. Al crear un nuevo formulario, se inserta una referencia al fragmento requerido y éste aparece en el formulario. La referencia de fragmento contiene un subformulario que señala al archivo XDP físico. Para obtener información sobre la creación de diseños de formulario basados en fragmentos, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Un fragmento puede incluir varios subformularios ajustados en un conjunto de subformularios de opciones. Los conjuntos de subformularios de opciones controlan la visualización de subformularios en función del flujo de datos de una conexión de datos. Se utilizan afirmaciones condicionales para determinar qué subformulario del conjunto aparece en el formulario entregado. Por ejemplo, cada subformulario de un conjunto puede incluir información de una ubicación geográfica determinada y el subformulario que se muestra puede determinarse en función de la ubicación del usuario.

Un *fragmento de secuencia de comandos* contiene funciones o valores de JavaScript reutilizables que se almacenan por separado de cualquier objeto en particular, como un analizador de fechas o una invocación de servicio Web. Estos fragmentos incluyen un único objeto de secuencia de comandos que aparece como un elemento secundario de variables en la paleta Jerarquía. Los fragmentos no pueden crearse a partir de secuencias de comandos que sean propiedades de otros objetos, tales como secuencias de comandos de sucesos validate, calculate o initialize.

A continuación se indican las ventajas de utilizar fragmentos:

* **Reutilización** del contenido: Puede utilizar fragmentos para reutilizar el contenido en varios diseños de formulario. Cuando necesite utilizar parte del mismo contenido en varios formularios, es más rápido y sencillo utilizar un fragmento que copiar o volver a crear el contenido. El uso de fragmentos también garantiza que las partes de un diseño de formulario utilizadas con frecuencia tengan un contenido y un aspecto coherentes en todos los formularios de referencia.
* **Actualizaciones** globales: Puede utilizar fragmentos para realizar cambios globales en varios formularios solo una vez, en un archivo. Puede cambiar el contenido, los objetos de secuencia de comandos, los enlaces de datos, la presentación o los estilos de un fragmento, y todos los formularios XDP que hagan referencia al fragmento reflejarán los cambios.
* Por ejemplo, un elemento común en muchos formularios podría ser un bloque de direcciones que incluya un objeto de lista desplegable para el país. Si necesita actualizar los valores del objeto de lista desplegable, debe abrir muchos formularios para realizar los cambios. Si incluye el bloque de direcciones en un fragmento, solo necesita abrir un archivo de fragmento para realizar los cambios.
* Para actualizar un fragmento en un formulario PDF, debe volver a guardarlo en Designer.
* **Creación** de formularios compartidos: Puede utilizar fragmentos para compartir la creación de formularios entre varios recursos. Los desarrolladores de formularios con conocimientos de secuencias de comandos u otras funciones avanzadas de Designer pueden desarrollar y compartir fragmentos que aprovechan las secuencias de comandos y las propiedades dinámicas. Los diseñadores de formularios pueden utilizar tales fragmentos para presentar diseños de formulario y garantizar que todas las partes de un formulario tengan un aspecto y una funcionalidad coherentes en los múltiples formularios diseñados por varias personas.

### Compilación de un diseño de formulario ensamblado con fragmentos {#assembling-a-form-design-assembled-using-fragments}

Puede montar un diseño de formulario para pasarlo al servicio Forms en función de varios fragmentos. Para ensamblar varios fragmentos, utilice el servicio Ensamblador. Para ver un ejemplo del uso del servicio Compilación para crear un diseño de formulario que utilice otro servicio de Forms (el servicio Output), consulte [Creación de Documentos PDF con fragmentos](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments). En lugar de utilizar el servicio Output, puede realizar el mismo flujo de trabajo con el servicio Forms.

Al utilizar el servicio Compilador, se pasa un diseño de formulario que se ensambló con fragmentos. El diseño de formulario creado no hace referencia a otros fragmentos. Por el contrario, en este tema se trata el paso de un diseño de formulario que hace referencia a otros fragmentos al servicio Forms. Sin embargo, el diseño de formulario no fue ensamblado por el Ensamblador. Se creó en Designer.

>[!NOTE]
>
>Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener información sobre la creación de una aplicación basada en Web que procese formularios basados en fragmentos, consulte [Creación de Aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

### Resumen de los pasos {#summary-of-steps}

Para procesar un formulario basado en fragmentos, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Especifique los valores de URI.
1. Representar el formulario.
1. Escriba la secuencia de datos del formulario en el navegador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Forms Client**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms.

**Especificar valores de URI**

Para procesar correctamente un formulario basado en fragmentos, debe asegurarse de que el servicio Forms puede localizar tanto el formulario como los fragmentos (archivos XDP) a los que hace referencia el diseño de formulario. Por ejemplo, supongamos que el formulario se denomina PO.xdp y que este formulario utiliza dos fragmentos denominados FooterUS.xdp y FooterCanada.xdp. En este caso, el servicio de Forms debe poder localizar los tres archivos XDP.

Puede organizar un formulario y sus fragmentos colocándolo en una ubicación y los fragmentos en otra, o bien puede colocar todos los archivos XDP en la misma ubicación. A los efectos de esta sección, supongamos que todos los archivos XDP se encuentran en el repositorio de AEM Forms. Para obtener información sobre la colocación de archivos XDP en el repositorio de AEM Forms, consulte [Escritura de recursos](/help/forms/developing/aem-forms-repository.md#writing-resources).

Cuando se procesa un formulario basado en fragmentos, solo se debe hacer referencia al propio formulario y no a los fragmentos. Por ejemplo, debe hacer referencia a PO.xdp y no a FooterUS.xdp o FooterCanada.xdp. Asegúrese de colocar los fragmentos en una ubicación en la que el servicio de Forms pueda localizarlos.

**Representar el formulario**

Un formulario basado en fragmentos se puede procesar del mismo modo que los formularios no fragmentados. Es decir, puede procesar el formulario como PDF, HTML o guías de formulario (obsoleto). El ejemplo de esta sección representa un formulario basado en fragmentos como un formulario PDF interactivo. (Consulte [Representación de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md).)

**Escribir el flujo de datos del formulario en el navegador web del cliente**

Cuando el servicio Forms procesa un formulario, devuelve una secuencia de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el navegador web del cliente, el formulario es visible para el usuario.

**Consulte también**

[Representar formularios en función de fragmentos mediante la API de Java](#render-forms-based-on-fragments-using-the-java-api)

[Representar formularios en función de fragmentos mediante la API de servicio web](#render-forms-based-on-fragments-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API de servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Representación de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Creación de Aplicaciones web que procesan Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Representar formularios en función de fragmentos mediante la API de Java {#render-forms-based-on-fragments-using-the-java-api}

Representar un formulario basado en fragmentos mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Forms Client

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Especificar valores de URI

   * Cree un objeto `URLSpec` que almacene valores URI mediante su constructor.
   * Invoque el método `URLSpec` del objeto `setApplicationWebRoot` y pase un valor de cadena que represente la raíz web de la aplicación.
   * Invoque el método `URLSpec` del objeto `setContentRootURI` y pase un valor de cadena que especifique el valor de URI raíz del contenido. Asegúrese de que el diseño de formulario y los fragmentos están ubicados en el URI raíz de contenido. Si no es así, el servicio Forms emite una excepción. Para hacer referencia al repositorio, especifique `repository://`.
   * Invoque el método `URLSpec` del objeto `setTargetURL` y pase un valor de cadena que especifique el valor de la URL de destinatario al que se registran los datos del formulario. Si define la URL de destinatario en el diseño de formulario, puede pasar una cadena vacía. También puede especificar la dirección URL a la que se envía un formulario para realizar cálculos.

1. Representar el formulario

   Invoque el método `FormsServiceClient` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto vacío `com.adobe.idp.Document`.
   * Un objeto `PDFFormRenderSpec` que almacena opciones de tiempo de ejecución.
   * Un objeto `URLSpec` que contiene valores URI que el servicio de Forms necesita para procesar un formulario basado en fragmentos.
   * Objeto `java.util.HashMap` que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `renderPDFForm` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario que debe escribirse en el explorador Web del cliente.

1. Escribir el flujo de datos del formulario en el navegador web del cliente

   * Cree un objeto `com.adobe.idp.Document` invocando el método `FormsResult` del objeto ‘s `getOutputContent`.
   * Obtenga el tipo de contenido del objeto `com.adobe.idp.Document` invocando su método `getContentType`.
   * Configure el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `com.adobe.idp.Document`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se utilice para escribir la secuencia de datos del formulario en el navegador web del cliente invocando el método `javax.servlet.http.HttpServletResponse` del objeto `getOutputStream`.
   * Cree un objeto `java.io.InputStream` invocando el método `com.adobe.idp.Document` del objeto `getInputStream`.
   * Cree una matriz de bytes para rellenarla con la secuencia de datos del formulario invocando el método `InputStream` del objeto `read`y pasando la matriz de bytes como argumento.
   * Invoque el método `javax.servlet.ServletOutputStream` del objeto `write` para enviar la secuencia de datos del formulario al explorador Web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Representación de Forms según fragmentos](#rendering-forms-based-on-fragments)

[Inicio rápido (modo SOAP): Representación de un formulario basado en fragmentos mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Representar formularios en función de fragmentos mediante la API de servicio Web {#render-forms-based-on-fragments-using-the-web-service-api}

Representar un formulario basado en fragmentos mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases proxy de Java que consuman el WSDL del servicio de Forms.
   * Incluya las clases proxy de Java en la ruta de clases.

1. Creación de un objeto de API de Forms Client

   Cree un objeto `FormsService` y defina los valores de autenticación.

1. Especificar valores de URI

   * Cree un objeto `URLSpec` que almacene valores de URI mediante su constructor.
   * Invoque el método `URLSpec` del objeto `setApplicationWebRoot` y pase un valor de cadena que represente la raíz web de la aplicación.
   * Invoque el método `URLSpec` del objeto `setContentRootURI` y pase un valor de cadena que especifique el valor de URI raíz del contenido. Asegúrese de que el diseño de formulario se encuentra en el URI raíz de contenido. Si no es así, el servicio Forms emite una excepción. Para hacer referencia al repositorio, especifique `repository://`.
   * Invoque el método `URLSpec` del objeto `setTargetURL` y pase un valor de cadena que especifique el valor de la URL de destinatario al que se registran los datos del formulario. Si define la URL de destinatario en el diseño de formulario, puede pasar una cadena vacía. También puede especificar la dirección URL a la que se envía un formulario para realizar cálculos.

1. Representar el formulario

   Invoque el método `FormsService` del objeto `renderPDFForm` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño de formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un objeto `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`.
   * Un objeto `PDFFormRenderSpec` que almacena opciones de tiempo de ejecución. Tenga en cuenta que la opción PDF con etiquetas no se puede establecer si el documento de entrada es un documento PDF. Si el archivo de entrada es un archivo XDP, se puede establecer la opción PDF con etiquetas.
   * Un objeto `URLSpec` que contiene valores URI requeridos por el servicio de Forms.
   * Objeto `java.util.HashMap` que almacena archivos adjuntos. Es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un objeto vacío `com.adobe.idp.services.holders.BLOBHolder` que se rellena con el método. Este parámetro se utiliza para almacenar el formulario procesado.
   * Un objeto vacío `javax.xml.rpc.holders.LongHolder` que se rellena con el método. Este argumento almacenará el número de páginas del formulario.
   * Un objeto vacío `javax.xml.rpc.holders.StringHolder` que se rellena con el método. Este argumento almacenará el valor de configuración regional.
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

[Representación de Forms según fragmentos](#rendering-forms-based-on-fragments)

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
