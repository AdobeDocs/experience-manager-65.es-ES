---
title: Uso de utilidades XMP
seo-title: Uso de utilidades XMP
description: nulo
seo-description: nulo
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 1%

---


# Uso de utilidades de XMP {#working-with-xmp-utilities}

**Acerca del servicio de utilidades de XMP**

Los documentos PDF contienen metadatos, que es información sobre el documento, tal como se distingue del contenido del documento, como texto y gráficos. Adobe Extensible Metadata Platform (XMP) es un estándar para el manejo de metadatos de documento.

El servicio Utilidades de XMP puede recuperar y guardar XMP metadatos de documentos PDF e importar XMP metadatos en documentos PDF.

Puede realizar estas tareas mediante el servicio Utilidades de XMP:

* Importe metadatos en documentos PDF. (Consulte [Importación de metadatos en Documentos PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)).
* Exporte metadatos de documentos PDF. (Consulte [Exportación de metadatos desde Documentos PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)).

>[!NOTE]
>
>Para obtener más información sobre el servicio Utilidades de XMP, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importación de metadatos en Documentos PDF {#importing-metadata-into-pdf-documents}

Puede utilizar las API de servicios web y Java de Utilidades de XMP para importar XMP metadatos en un documento PDF mediante programación. Los metadatos proporcionan información sobre un documento PDF, como el autor del documento y las palabras clave relacionadas con el documento. Los metadatos se pueden encontrar en el cuadro de diálogo Propiedades del Documento del documento, como se muestra en la siguiente ilustración.

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

Para importar metadatos mediante programación a un documento PDF, puede utilizar un documento XML existente que especifique los valores de metadatos o un objeto de tipo `XMPUtilityMetadata`. (Consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

>[!NOTE]
>
>En esta sección se explica cómo utilizar un documento XML para importar metadatos en un documento PDF.

El siguiente código XML contiene valores de metadatos que corresponden a la ilustración anterior. Por ejemplo: observe los elementos en negrita, que especifican palabras clave.

```xml
 <?xpacket begin="?" id="W5M0MpCehiHzreSzNTczkc9d"?>
 <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="Adobe XMP Core 4.2-jc015 52.349034, 2008 Jun 20 00:30:39-PDT (debug)">
       <rdf:RDF xmlns:rdf="https://www.w3.org/1999/02/22-rdf-syntax-ns#">
          <rdf:Description rdf:about=""
                xmlns:xmp="https://ns.adobe.com/xap/1.0/">
             <xmp:MetadataDate>2008-10-22T10:52:21-04:00</xmp:MetadataDate>
             <xmp:CreatorTool>AEM Forms</xmp:CreatorTool>
             <xmp:ModifyDate>2008-10-22T10:52:21-04:00</xmp:ModifyDate>
             <xmp:CreateDate>2008-02-13T11:00:18-05:00</xmp:CreateDate>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:pdf="https://ns.adobe.com/pdf/1.3/">
             <pdf:Producer>AEM Forms</pdf:Producer>
             <pdf:Keywords>keyword1, keyword2, keyword3,keyword4</pdf:Keywords>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:xmpMM="https://ns.adobe.com/xap/1.0/mm/">
             <xmpMM:DocumentID>uuid:1cce1f84-331e-4d8d-8538-15441c271dd7</xmpMM:DocumentID>
             <xmpMM:InstanceID>uuid:cdda0ca6-7c91-4771-9dc9-796c8fe59350</xmpMM:InstanceID>
          </rdf:Description>
          <rdf:Description rdf:about=""
                >
             <dc:format>application/pdf</dc:format>
             <dc:description>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Adobe Designer Sample</rdf:li>
                </rdf:Alt>
             </dc:description>
             <dc:title>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Grant Application</rdf:li>
                </rdf:Alt>
             </dc:title>
             <dc:creator>
                <rdf:Seq>
                   <rdf:li>Tony Blue</rdf:li>
                </rdf:Seq>
             </dc:creator>
             <dc:subject>
                <rdf:Bag>
                   <rdf:li>keyword1</rdf:li>
                   <rdf:li>keyword2</rdf:li>
                   <rdf:li>keyword3</rdf:li>
                   <rdf:li>keyword4</rdf:li>
                </rdf:Bag>
             </dc:subject>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:desc="https://ns.adobe.com/xfa/promoted-desc/">
             <desc:version rdf:parseType="Resource">
                <rdf:value>1.0</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:version>
             <desc:contact rdf:parseType="Resource">
                <rdf:value>Adobe Systems Incorporated</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:contact>
          </rdf:Description>
       </rdf:RDF>
 </x:xmpmeta>
```

>[!NOTE]
>
>Para obtener más información sobre el servicio Utilidades de XMP, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para importar metadatos de XMP a un documento PDF, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente XMPUtilityService.
1. Invoque la operación de importación de metadatos de XMP.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un cliente XMPUtilityService**

Para poder realizar mediante programación una operación de Utilidades de XMP, debe crear un cliente XMPUtilityService. Con la API de Java, esto se logra creando un objeto `XMPUtilityServiceClient`. Con la API de servicio Web, esto se logra mediante el uso de un objeto `XMPUtilityServiceService`.

**Invocar la operación de importación de metadatos de XMP**

Después de crear el cliente de servicios, puede invocar una de las operaciones de importación de metadatos de XMP para importar los metadatos de XMP en el documento PDF especificado.

**Consulte también**

[Importación XMP metadatos mediante la API de Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importación de metadatos de XMP mediante la API de servicio web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importar metadatos de XMP mediante la API de Java {#import-xmp-metadata-using-the-java-api}

Importe metadatos de XMP mediante la API de utilidades de XMP (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clases del proyecto Java.

   >[!NOTE]
   >
   >El archivo adobe-pdfutility-client.jar contiene clases que le permiten invocar mediante programación el servicio Utilidades de XMP.

1. Creación de un cliente XMPUtilityService

   Cree un objeto `XMPUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invocar la operación de importación de metadatos de XMP

   Para modificar los metadatos de XMP, invoque el método `XMPUtilityServiceClient` del objeto `importMetadata` o su método `importXMP`.

   Si utiliza el método `importMetadata`, pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el archivo PDF.
   * Un objeto `XMPUtilityMetadata` que contiene los metadatos que se van a importar.

   Si utiliza el método `importXMP`, pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el archivo PDF.
   * Un objeto `com.adobe.idp.Document` que representa un archivo XML que contiene los metadatos que se van a importar.

   En cualquier caso, el valor devuelto es un objeto `com.adobe.idp.Document` que representa el archivo PDF con los metadatos recién importados. A continuación, puede guardar este objeto en el disco.

**Consulte también**

[Importación de metadatos en Documentos PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importación de metadatos de XMP mediante la API de servicio Web {#importing-xmp-metadata-using-the-web-service-api}

Para importar metadatos de XMP mediante programación mediante la API del servicio web de utilidades de XMP, realice las siguientes tareas:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el archivo WSDL del servicio de utilidades de XMP. (Consulte [Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)).
   * Haga referencia al ensamblado de cliente de Microsoft .NET. (Consulte [Creación de un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Creación de un cliente XMPUtilityService

   Cree un objeto `XMPUtilityServiceService` mediante el constructor de la clase proxy.

1. Invocar la operación de importación de metadatos de XMP

   Para modificar los metadatos de XMP, invoque el método `XMPUtilityServiceService` del objeto `importMetadata` o su método `importXMP`.

   Si utiliza el método `importMetadata`, pase los siguientes valores:

   * Un objeto `BLOB` que representa el archivo PDF.
   * Un objeto `XMPUtilityMetadata` que contiene los metadatos que se van a importar.

   Si utiliza el método `importXMP`, pase los siguientes valores:

   * Un objeto `BLOB` que representa el archivo PDF.
   * Un objeto `BLOB` que representa un archivo XML que contiene los metadatos que se van a importar.

   En cualquier caso, el valor devuelto es un objeto `BLOB` que representa el archivo PDF con los metadatos recién importados. A continuación, puede guardar este objeto en el disco.

**Consulte también**

[Importación de metadatos en Documentos PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Exportación de metadatos desde Documentos PDF {#exporting-metadata-from-pdf-documents}

Puede utilizar las API de servicio Web y Java de Utilidades de XMP para recuperar y guardar XMP metadatos mediante programación desde un documento PDF.

>[!NOTE]
>
>Para obtener más información sobre el servicio Utilidades de XMP, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para exportar metadatos de XMP desde un documento PDF, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente XMPUtilityService.
1. Invoque la operación de exportación de metadatos de XMP.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un cliente XMPUtilityService**

Para poder realizar mediante programación una operación de Utilidades de XMP, debe crear un cliente XMPUtilityService. Con la AP de Java, esto se logra creando un objeto `XMPUtilityServiceClient`. Con la API de servicio Web, esto se logra mediante un objeto `XMPUtilityServiceService`.

**Invocar la operación de exportación de metadatos de XMP**

Después de crear el cliente de servicio, puede invocar una de las operaciones de exportación de metadatos de XMP, que se puede utilizar para inspeccionar los metadatos de XMP o guardarlos en disco.

**Consulte también**

[Importación XMP metadatos mediante la API de Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importación de metadatos de XMP mediante la API de servicio web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportar metadatos de XMP mediante la API de Java {#export-xmp-metadata-using-the-java-api}

Exporte metadatos de XMP mediante la API de utilidades de XMP (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clases del proyecto Java.

   >[!NOTE]
   >
   >El archivo adobe-pdfutility-client.jar contiene clases que le permiten invocar mediante programación el servicio XMP Utility.

1. Creación de un cliente XMPUtilityService

   Cree un objeto `XMPUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invocar la operación de importación de metadatos de XMP

   Para inspeccionar los metadatos de XMP, invoque el método `XMPUtilityServiceClient` del objeto `exportMetadata` y pase un objeto `com.adobe.idp.Document` que represente el archivo PDF. El método devuelve un objeto `XMPUtilityMetadata` que contiene los metadatos recuperados.

   Para recuperar y guardar los metadatos de XMP, invoque el método `XMPUtilityServiceClient` del objeto `exportXMP` y pase un objeto `com.adobe.idp.Document` que represente el archivo PDF. El método devuelve un objeto `com.adobe.idp.Document` que contiene los metadatos recuperados, que posteriormente puede guardar en disco como archivo XML.

**Consulte también**

[Exportación de metadatos desde Documentos PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportar metadatos de XMP mediante la API de servicio Web {#export-xmp-metadata-using-the-web-service-api}

Exportar metadatos de XMP mediante la API de utilidades de XMP (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el archivo WSDL del servicio de utilidades de XMP.
   * Haga referencia al ensamblado de cliente de Microsoft .NET.

1. Creación de un cliente XMPUtilityService

   Cree un objeto `XMPUtilityServiceService` mediante el constructor de la clase proxy.

1. Invocar la operación de importación de metadatos de XMP

   Para inspeccionar los metadatos de XMP, invoque el método `XMPUtilityServiceClient` del objeto `exportMetadata` y pase un objeto `BLOB` que represente el archivo PDF. El método devuelve un objeto `XMPUtilityMetadata` que contiene los metadatos recuperados.

   Para recuperar y guardar los metadatos de XMP, invoque el método `XMPUtilityServiceClient` del objeto `exportXMP` y pase un objeto `BLOB` que represente el archivo PDF. El método devuelve un objeto `BLOB` que contiene los metadatos recuperados, que posteriormente puede guardar en disco como archivo XML.

**Consulte también**

[Exportación de metadatos desde Documentos PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
