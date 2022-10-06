---
title: Uso de utilidades XMP
seo-title: Working with XMP Utilities
description: Utilice las API de XMP Utilities Java y Web Service para importar de forma programada metadatos de XMP en un documento de PDF y recuperar y guardar XMP metadatos de un documento de PDF.
seo-description: Use the XMP Utilities Java and Web Service APIs to programmatically import XMP metadata into a PDF document and retrieve and save XMP metadata from a PDF document.
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
role: Developer
exl-id: cff65f74-ba95-438e-88a4-5ec7d22aafba
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 0%

---

# Uso de utilidades XMP {#working-with-xmp-utilities}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

**Acerca del servicio de utilidades XMP**

Los documentos del PDF contienen metadatos, que son información sobre el documento distinguida del contenido del documento, como texto y gráficos. Adobe Extensible Metadata Platform (XMP) es un estándar para la gestión de metadatos de documentos.

El servicio XMP Utilidades puede recuperar y guardar XMP metadatos de documentos de PDF e importar XMP metadatos en documentos de PDF.

Puede realizar estas tareas mediante el servicio XMP Utilidades:

* Importe metadatos en documentos de PDF. (Consulte [Importación de metadatos en documentos de PDF](xmp-utilities.md#importing-metadata-into-pdf-documents).)
* Exportar metadatos de documentos de PDF. (Consulte [Exportación de metadatos desde documentos de PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents).)

>[!NOTE]
>
>Para obtener más información sobre el servicio XMP Utilidades, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importación de metadatos en documentos de PDF {#importing-metadata-into-pdf-documents}

Puede utilizar las API de servicios web y Java de utilidades de XMP para importar XMP metadatos mediante programación a un documento de PDF. Los metadatos proporcionan información sobre un documento de PDF, como el autor del documento y las palabras clave relacionadas con él. Los metadatos se pueden encontrar en el cuadro de diálogo Propiedades del documento del documento, como se muestra en la siguiente ilustración.

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

Para importar metadatos mediante programación a un documento de PDF, puede utilizar un documento XML existente que especifique los valores de los metadatos o puede utilizar un objeto de tipo `XMPUtilityMetadata`. (Consulte [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

>[!NOTE]
>
>En esta sección se explica cómo utilizar un documento XML para importar metadatos en un documento de PDF.

El siguiente código XML contiene valores de metadatos que corresponden a la ilustración anterior. Por ejemplo, observe los elementos en negrita, que especifican palabras clave.

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
>Para obtener más información sobre el servicio XMP Utilidades, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para importar XMP metadatos en un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente XMPUtilityService.
1. Invoque la operación de importación de metadatos de XMP.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un cliente XMPUtilityService**

Para poder realizar mediante programación una operación XMP Utilidades, debe crear un cliente XMPUtilityService. Con la API de Java, esto se logra creando un `XMPUtilityServiceClient` objeto. Con la API del servicio web, esto se logra mediante el uso de un `XMPUtilityServiceService` objeto.

**Invocar la operación de importación de metadatos de XMP**

Después de crear el cliente de servicio, puede invocar una de las operaciones de importación de metadatos de XMP para importar los metadatos de XMP en el documento de PDF especificado.

**Consulte también lo siguiente**

[Importación XMP metadatos mediante la API de Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importación de metadatos de XMP mediante la API de servicio web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importación XMP metadatos mediante la API de Java {#import-xmp-metadata-using-the-java-api}

Importe XMP metadatos mediante la API de utilidades XMP (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

   >[!NOTE]
   >
   >El archivo adobe-pdfutility-client.jar contiene clases que le permiten invocar mediante programación el servicio XMP Utilidades.

1. Creación de un cliente XMPUtilityService

   Cree un `XMPUtilityServiceClient` usando su constructor y pasando un `ServiceClientFactory` objeto que contiene propiedades de conexión.

1. Invocar la operación de importación de metadatos de XMP

   Para modificar los metadatos de XMP, invoque la variable `XMPUtilityServiceClient` del objeto `importMetadata` método o `importXMP` método.

   Si usa la variable `importMetadata` pasa los siguientes valores:

   * A `com.adobe.idp.Document` que representa el archivo PDF.
   * Un `XMPUtilityMetadata` objeto que contiene los metadatos que se van a importar.

   Si usa la variable `importXMP` pasa los siguientes valores:

   * A `com.adobe.idp.Document` que representa el archivo PDF.
   * A `com.adobe.idp.Document` que representa un archivo XML que contiene los metadatos que se van a importar.

   En cualquier caso, el valor devuelto es un `com.adobe.idp.Document` que representa el archivo PDF con los metadatos recién importados. A continuación, puede guardar este objeto en el disco.

**Consulte también lo siguiente**

[Importación de metadatos en documentos de PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importación de metadatos de XMP mediante la API de servicio web {#importing-xmp-metadata-using-the-web-service-api}

Para importar mediante programación metadatos de XMP mediante la API de servicio web de utilidades de XMP, realice las siguientes tareas:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio de utilidades de XMP. (Consulte [Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Haga referencia al ensamblado del cliente Microsoft .NET. (Consulte [Creación de un ensamblado de cliente .NET que utilice la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Creación de un cliente XMPUtilityService

   Cree un `XMPUtilityServiceService` usando el constructor de clase proxy.

1. Invocar la operación de importación de metadatos de XMP

   Para modificar los metadatos de XMP, invoque la variable `XMPUtilityServiceService` del objeto `importMetadata` método o `importXMP` método.

   Si usa la variable `importMetadata` pasa los siguientes valores:

   * A `BLOB` que representa el archivo PDF.
   * Un `XMPUtilityMetadata` objeto que contiene los metadatos que se van a importar.

   Si usa la variable `importXMP` pasa los siguientes valores:

   * A `BLOB` que representa el archivo PDF.
   * A `BLOB` que representa un archivo XML que contiene los metadatos que se van a importar.

   En cualquier caso, el valor devuelto es un `BLOB` que representa el archivo PDF con los metadatos recién importados. A continuación, puede guardar este objeto en el disco.

**Consulte también lo siguiente**

[Importación de metadatos en documentos de PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Exportación de metadatos desde documentos de PDF {#exporting-metadata-from-pdf-documents}

Puede utilizar las API de servicios web y Java de utilidades de XMP para recuperar y guardar XMP metadatos mediante programación desde un documento de PDF.

>[!NOTE]
>
>Para obtener más información sobre el servicio XMP Utilidades, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para exportar XMP metadatos de un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente XMPUtilityService.
1. Invoque la operación de exportación de metadatos de XMP.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un cliente XMPUtilityService**

Para poder realizar mediante programación una operación XMP Utilidades, debe crear un cliente XMPUtilityService. Con la API de Java, esto se logra creando una `XMPUtilityServiceClient` objeto. Con la API del servicio web, esto se lleva a cabo mediante un `XMPUtilityServiceService` objeto.

**Invocar la operación de exportación de metadatos de XMP**

Después de crear el cliente de servicio, puede invocar una de las operaciones de exportación de metadatos de XMP, que se puede utilizar para inspeccionar los metadatos de XMP o guardarlos en el disco.

**Consulte también lo siguiente**

[Importación XMP metadatos mediante la API de Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importación de metadatos de XMP mediante la API de servicio web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportar metadatos de XMP mediante la API de Java {#export-xmp-metadata-using-the-java-api}

Exporte XMP metadatos mediante la API de utilidades de XMP (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

   >[!NOTE]
   >
   >El archivo adobe-pdfutility-client.jar contiene clases que le permiten invocar mediante programación el servicio XMP Utility.

1. Creación de un cliente XMPUtilityService

   Cree un `XMPUtilityServiceClient` usando su constructor y pasando un `ServiceClientFactory` objeto que contiene propiedades de conexión.

1. Invocar la operación de importación de metadatos de XMP

   Para inspeccionar los metadatos de XMP, invoque la variable `XMPUtilityServiceClient` del objeto `exportMetadata` método y pasar un `com.adobe.idp.Document` que representa el archivo PDF. El método devuelve un valor `XMPUtilityMetadata` que contiene los metadatos recuperados.

   Para recuperar y guardar los metadatos de XMP, invoque la variable `XMPUtilityServiceClient` del objeto `exportXMP` método y pasar un `com.adobe.idp.Document` que representa el archivo PDF. El método devuelve un valor `com.adobe.idp.Document` que contiene los metadatos recuperados, que posteriormente se pueden guardar en disco como un archivo XML.

**Consulte también lo siguiente**

[Exportación de metadatos desde documentos de PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportar metadatos de XMP mediante la API de servicio web {#export-xmp-metadata-using-the-web-service-api}

Exporte XMP metadatos mediante la API de utilidades XMP (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio de utilidades de XMP.
   * Haga referencia al ensamblado del cliente Microsoft .NET.

1. Creación de un cliente XMPUtilityService

   Cree un `XMPUtilityServiceService` usando el constructor de clase proxy.

1. Invocar la operación de importación de metadatos de XMP

   Para inspeccionar los metadatos de XMP, invoque la variable `XMPUtilityServiceClient` del objeto `exportMetadata` método y pasar un `BLOB` que representa el archivo PDF. El método devuelve un valor `XMPUtilityMetadata` que contiene los metadatos recuperados.

   Para recuperar y guardar los metadatos de XMP, invoque la variable `XMPUtilityServiceClient` del objeto `exportXMP` método y pasar un `BLOB` que representa el archivo PDF. El método devuelve un valor `BLOB` que contiene los metadatos recuperados, que posteriormente se pueden guardar en disco como un archivo XML.

**Consulte también lo siguiente**

[Exportación de metadatos desde documentos de PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
