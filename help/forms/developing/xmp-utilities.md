---
title: Trabajar con utilidades XMP
description: XMP XMP Utilice las API de Java y Servicio Web de Utilidades de la para importar mediante programación metadatos de la aplicación en un documento de PDF XMP y recuperar y guardar metadatos de la aplicación de un documento de PDF.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: cff65f74-ba95-438e-88a4-5ec7d22aafba
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 1%

---

# Trabajar con utilidades XMP {#working-with-xmp-utilities}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

**XMP Acerca del servicio de utilidades de**

Los documentos de PDF contienen metadatos, que son información sobre el documento tal como se distingue del contenido del documento, como texto y gráficos. La plataforma de metadatos extensible de Adobe XMP () es un estándar para administrar metadatos de documentos.

XMP XMP El servicio Utilidades de la puede recuperar y guardar metadatos de la de documentos de PDF XMP, así como importarlos en documentos de PDF.

XMP Puede llevar a cabo estas tareas mediante el servicio Utilidades de la:

* Importa metadatos en documentos de PDF. (Consulte [Importación de metadatos en documentos de PDF](xmp-utilities.md#importing-metadata-into-pdf-documents).)
* Exportar metadatos de documentos de PDF. (Consulte [Exportación de metadatos desde documentos del PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents).)

>[!NOTE]
>
>XMP Para obtener más información sobre el servicio Utilidades de la, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importación de metadatos en documentos de PDF {#importing-metadata-into-pdf-documents}

XMP XMP Puede utilizar las API de Java y servicios web de Utilidades de la para importar mediante programación metadatos de la aplicación en un documento de PDF. Los metadatos proporcionan información sobre un documento de PDF, como el autor del documento y las palabras clave relacionadas con él. Los metadatos pueden encontrarse en el cuadro de diálogo Propiedades del documento, como se muestra en la siguiente ilustración.

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

Para importar metadatos mediante programación en un documento de PDF, puede utilizar un documento XML existente que especifique los valores de los metadatos o puede utilizar un objeto de tipo `XMPUtilityMetadata`. (Consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

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
>XMP Para obtener más información sobre el servicio Utilidades de la, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

XMP Para importar metadatos de la en un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de XMPUtilityService.
1. XMP Invoque la operación de importación de metadatos de la.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de XMPUtilityService**

XMP Antes de poder realizar mediante programación una operación de Utilidades de, debe crear un cliente de XMPUtilityService. Con la API de Java, esto se logra creando un `XMPUtilityServiceClient` objeto. Con la API del servicio web, esto se logra mediante una `XMPUtilityServiceService` objeto.

**XMP Invocar la operación de importación de metadatos de la**

XMP XMP Después de crear el cliente de servicios, puede invocar una de las operaciones de importación de metadatos de la para importar los metadatos de la en el documento de PDF especificado.

**Consulte también**

[XMP Importación de metadatos de la mediante la API de Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[XMP Importación de metadatos de la mediante la API de servicio web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### XMP Importación de metadatos de la mediante la API de Java {#import-xmp-metadata-using-the-java-api}

XMP XMP Importación de metadatos de la mediante la API de utilidades (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

   >[!NOTE]
   >
   >XMP El archivo adobe-pdfutility-client.jar contiene clases que permiten invocar mediante programación el servicio Utilidades de la.

1. Crear un cliente de XMPUtilityService

   Crear un `XMPUtilityServiceClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. XMP Invocar la operación de importación de metadatos de la

   XMP Para modificar los metadatos de la, invoque el método `XMPUtilityServiceClient` del objeto `importMetadata` o su `importXMP` método.

   Si usa el `importMetadata` , pase los siguientes valores:

   * A `com.adobe.idp.Document` que representa el archivo del PDF.
   * Un `XMPUtilityMetadata` que contiene los metadatos que se van a importar.

   Si usa el `importXMP` , pase los siguientes valores:

   * A `com.adobe.idp.Document` que representa el archivo del PDF.
   * A `com.adobe.idp.Document` que representa un archivo XML que contiene los metadatos que se van a importar.

   En cualquier caso, el valor devuelto es un `com.adobe.idp.Document` que representa el archivo del PDF con los metadatos recién importados. A continuación, puede guardar este objeto en el disco.

**Consulte también**

[Importación de metadatos en documentos de PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### XMP Importación de metadatos de la mediante la API de servicio web {#importing-xmp-metadata-using-the-web-service-api}

XMP XMP Para importar mediante programación metadatos de la mediante la API del servicio web de Utilidades de la aplicación, realice las siguientes tareas:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft XMP .NET que consuma el archivo WSDL del servicio Utilidades de la. (Consulte [Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Hacer referencia al ensamblado de cliente de Microsoft .NET. (Consulte [Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Crear un cliente de XMPUtilityService

   Crear un `XMPUtilityServiceService` mediante el constructor de la clase de proxy.

1. XMP Invocar la operación de importación de metadatos de la

   XMP Para modificar los metadatos de la, invoque el método `XMPUtilityServiceService` del objeto `importMetadata` o su `importXMP` método.

   Si usa el `importMetadata` , pase los siguientes valores:

   * A `BLOB` que representa el archivo del PDF.
   * Un `XMPUtilityMetadata` que contiene los metadatos que se van a importar.

   Si usa el `importXMP` , pase los siguientes valores:

   * A `BLOB` que representa el archivo del PDF.
   * A `BLOB` que representa un archivo XML que contiene los metadatos que se van a importar.

   En cualquier caso, el valor devuelto es un `BLOB` que representa el archivo del PDF con los metadatos recién importados. A continuación, puede guardar este objeto en el disco.

**Consulte también**

[Importación de metadatos en documentos de PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Exportación de metadatos desde documentos del PDF {#exporting-metadata-from-pdf-documents}

XMP XMP Puede utilizar las API de Java y del servicio web de Utilidades de para recuperar y guardar metadatos de un documento de PDF mediante programación.

>[!NOTE]
>
>XMP Para obtener más información sobre el servicio Utilidades de la, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

XMP Para exportar metadatos de la desde un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de XMPUtilityService.
1. XMP Invoque la operación de exportación de metadatos de la.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de XMPUtilityService**

XMP Antes de poder realizar mediante programación una operación de Utilidades de, debe crear un cliente de XMPUtilityService. Con la API de Java, esto se consigue creando una `XMPUtilityServiceClient` objeto. Con la API del servicio web, esto se logra mediante una `XMPUtilityServiceService` objeto.

**XMP Invocar la operación de exportación de metadatos de la**

XMP XMP Después de crear el cliente de servicio, puede invocar una de las operaciones de exportación de metadatos de la, que se puede utilizar para inspeccionar los metadatos de la o guardarlos en el disco.

**Consulte también**

[XMP Importación de metadatos de la mediante la API de Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[XMP Importación de metadatos de la mediante la API de servicio web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### XMP Exportación de metadatos de la mediante la API de Java {#export-xmp-metadata-using-the-java-api}

XMP XMP Exportación de metadatos de la mediante la API de utilidades (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

   >[!NOTE]
   >
   >XMP El archivo adobe-pdfutility-client.jar contiene clases que permiten invocar mediante programación el servicio de utilidad de.

1. Crear un cliente de XMPUtilityService

   Crear un `XMPUtilityServiceClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. XMP Invocar la operación de importación de metadatos de la

   XMP Para inspeccionar los metadatos de la, invoque el `XMPUtilityServiceClient` del objeto `exportMetadata` método y pasar un `com.adobe.idp.Document` que representa el archivo del PDF. El método devuelve un valor `XMPUtilityMetadata` que contiene los metadatos recuperados.

   XMP Para recuperar y guardar los metadatos de la, invoque el `XMPUtilityServiceClient` del objeto `exportXMP` método y pasar un `com.adobe.idp.Document` que representa el archivo del PDF. El método devuelve un valor `com.adobe.idp.Document` que contiene los metadatos recuperados, que posteriormente puede guardar en disco como archivo XML.

**Consulte también**

[Exportación de metadatos desde documentos del PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### XMP Exportación de metadatos de la mediante la API de servicio web {#export-xmp-metadata-using-the-web-service-api}

XMP XMP Exportación de metadatos de la mediante la API de utilidades (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft XMP .NET que consuma el archivo WSDL del servicio Utilidades de la.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente de XMPUtilityService

   Crear un `XMPUtilityServiceService` mediante el constructor de la clase de proxy.

1. XMP Invocar la operación de importación de metadatos de la

   XMP Para inspeccionar los metadatos de la, invoque el `XMPUtilityServiceClient` del objeto `exportMetadata` método y pasar un `BLOB` que representa el archivo del PDF. El método devuelve un valor `XMPUtilityMetadata` que contiene los metadatos recuperados.

   XMP Para recuperar y guardar los metadatos de la, invoque el `XMPUtilityServiceClient` del objeto `exportXMP` método y pasar un `BLOB` que representa el archivo del PDF. El método devuelve un valor `BLOB` que contiene los metadatos recuperados, que posteriormente puede guardar en disco como archivo XML.

**Consulte también**

[Exportación de metadatos desde documentos del PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
