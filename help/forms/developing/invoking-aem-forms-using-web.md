---
title: Invocación de AEM Forms mediante servicios web
seo-title: Invoking AEM Forms using Web Services
description: Invoque los procesos de AEM Forms mediante servicios web con compatibilidad total con la generación de WSDL.
seo-description: Invoke AEM Forms processes using web services with full support for WSDL generation.
uuid: 66bcd010-c476-4b66-831d-a48307d8d67a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: d5722281-bea9-4fc7-abdc-e678899e0a15
role: Developer
exl-id: 3139564f-9346-4933-8e39-2e1642bff097
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '9905'
ht-degree: 0%

---

# Invocación de AEM Forms mediante servicios web {#invoking-aem-forms-using-web-services}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

La mayoría de los servicios de AEM Forms del contenedor de servicios están configurados para exponer un servicio web, con compatibilidad total con la generación de lenguaje de definición de servicio web (WSDL). Es decir, puede crear objetos proxy que consuman la pila nativa SOAP de un servicio AEM Forms. Como resultado, los servicios de AEM Forms pueden intercambiar y procesar los siguientes mensajes SOAP:

* **solicitud SOAP**: Enviado a un servicio de Forms por una aplicación cliente que solicita una acción.
* **Respuesta SOAP**: Enviado a una aplicación cliente por un servicio de Forms después de procesar una solicitud SOAP.

Con los servicios web, puede realizar las mismas operaciones de servicios de AEM Forms que con la API de Java. Una ventaja de utilizar servicios web para invocar servicios de AEM Forms es que puede crear una aplicación cliente en un entorno de desarrollo que admita SOAP. Una aplicación cliente no está vinculada a un entorno de desarrollo o a un lenguaje de programación específicos. Por ejemplo, puede crear una aplicación cliente utilizando Microsoft Visual Studio .NET y C# como lenguaje de programación.

Los servicios de AEM Forms se exponen a través del protocolo SOAP y son compatibles con WSI Basic Profile 1.1. La interoperabilidad de los servicios web (WSI) es una organización de estándares abiertos que promueve la interoperabilidad de los servicios web en todas las plataformas. Para obtener más información, consulte [https://www.ws-i.org/](https://www.ws-i.org).

AEM Forms es compatible con los siguientes estándares de servicio web:

* **Codificación**: Solo admite codificación de documento y literal (que es la codificación preferida según el perfil básico de WSI). (Consulte [Invocación de AEM Forms mediante la codificación Base64](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**: Representa una forma de codificar archivos adjuntos con solicitudes SOAP. (Consulte [Invocación de AEM Forms mediante MTOM](#invoking-aem-forms-using-mtom).)
* **SwaRef**: Representa otra forma de codificar archivos adjuntos con solicitudes SOAP. (Consulte [Invocación de AEM Forms mediante SwaRef](#invoking-aem-forms-using-swaref).)
* **SOAP con archivos adjuntos**: Admite MIME y DIME (Encapsulación de mensajes directos de Internet). Estos protocolos son formas estándar de enviar archivos adjuntos a través de SOAP. Las aplicaciones Microsoft Visual Studio .NET utilizan DIME. (Consulte [Invocación de AEM Forms mediante la codificación Base64](#invoking-aem-forms-using-base64-encoding).)
* **WS-Security**: Admite un perfil de token de contraseña de nombre de usuario, que es una forma estándar de enviar nombres de usuario y contraseñas como parte del encabezado SOAP de seguridad de WS. AEM Forms también admite la autenticación básica HTTP. s

Para invocar servicios de AEM Forms mediante un servicio web, normalmente se crea una biblioteca proxy que consume el servicio WSDL. La variable *Invocación de AEM Forms mediante servicios web* utiliza JAX-WS para crear clases proxy de Java e invocar servicios. (Consulte [Creación de clases de proxy Java mediante JAX-WS](#creating-java-proxy-classes-using-jax-ws).)

Puede recuperar un WDSL de servicio especificando la siguiente definición de URL (los elementos entre corchetes son opcionales):

```java
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

donde:

* *your_serverhost* representa la dirección IP del servidor de aplicaciones J2EE que aloja AEM Forms.
* *your_port* representa el puerto HTTP que utiliza el servidor de aplicaciones J2EE.
* *service_name* representa el nombre del servicio.
* *version* representa la versión de destino de un servicio (se utiliza la última versión del servicio de forma predeterminada).
* `async` especifica el valor `true` para habilitar operaciones adicionales para invocación asincrónica ( `false` de forma predeterminada).
* *lc_version* representa la versión de AEM Forms que desea invocar.

En la tabla siguiente se enumeran las definiciones de WSDL de servicio (suponiendo que AEM Forms se implementa en el host local y el anuncio es 8080).

<table>
 <thead>
  <tr>
   <th><p>Servicio</p></th>
   <th><p>Definición WSDL</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Ensamblador</p></td>
   <td><p><code>http://localhost:8080/soap/services/ AssemblerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Atrás y restaurar</p></td>
   <td><p><code>http://localhost:8080/soap/services/BackupService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>formularios con códigos de barras</p></td>
   <td><p><code>http://localhost:8080/soap/services/ BarcodedFormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Convertir PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ConvertPDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Distiller</p></td>
   <td><p><code>http://localhost:8080/soap/services/ DistillerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>DocConverter </p></td>
   <td><p><code>http://localhost:8080/soap/services/DocConverterService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>Gestión de documentos</p></td>
   <td><p><code>http://localhost:8080/soap/services/DocumentManagementService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>Cifrado </p></td>
   <td><p><code>http://localhost:8080/soap/services/EncryptionService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Forms</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Integración de datos de formulario</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormDataIntegration?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Generar PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/ GeneratePDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Generar PDF 3D</p></td>
   <td><p><code>http://localhost:8080/soap/services/Generate3dPDFService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>Salida</p></td>
   <td><p><code>http://localhost:8080/soap/services/ OutputService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Utilidades del PDF </p></td>
   <td><p><code>http://localhost:8080/soap/services/ PDFUtilityService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Extensiones de Acrobat Reader DC</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ReaderExtensionsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Repositorio</p></td>
   <td><p><code>http://localhost:8080/soap/services/ RepositoryService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Rights Management </p></td>
   <td><p><code>http://localhost:8080/soap/services/ RightsManagementService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Firma </p></td>
   <td><p><code>http://localhost:8080/soap/services/ SignatureService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>XMP Utilidades</p></td>
   <td><p><code>http://localhost:8080/soap/services/ XMPUtilityService?wsdl</code></p></td>
  </tr>
 </tbody>
</table>

**Definiciones de WSDL del proceso de AEM Forms**

Debe especificar el nombre de la aplicación y el nombre del proceso en la definición WSDL para acceder a un WSDL que pertenece a un proceso creado en Workbench. Supongamos que el nombre de la aplicación es `MyApplication` y el nombre del proceso es `EncryptDocument`. En este caso, especifique la siguiente definición WSDL:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>Para obtener información sobre el ejemplo `MyApplication/EncryptDocument` proceso de corta duración, consulte [Ejemplo de proceso de corta duración](/help/forms/developing/aem-forms-processes.md).

>[!NOTE]
>
>Una aplicación puede contener carpetas. En este caso, especifique los nombres de carpeta en la definición WSDL:

```java
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**Acceso a la nueva funcionalidad mediante servicios web**

Se puede acceder a la nueva funcionalidad del servicio AEM Forms mediante los servicios web. Por ejemplo, en AEM Forms, se introduce la capacidad de codificar archivos adjuntos mediante MTOM. (Consulte [Invocación de AEM Forms mediante MTOM](#invoking-aem-forms-using-mtom).)

Para acceder a las nuevas funciones introducidas en AEM Forms, especifique la `lc_version` en la definición de WSDL. Por ejemplo, para acceder a la nueva funcionalidad de servicio (incluida la compatibilidad con MTOM), especifique la siguiente definición de WSDL:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>Al configurar la variable `lc_version` , asegúrese de usar tres dígitos. Por ejemplo, 9.0.1 es igual a la versión 9.0.

**Tipo de datos BLOB del servicio web**

Los WSDL del servicio AEM Forms definen muchos tipos de datos. Uno de los tipos de datos más importantes expuestos en un servicio web es un `BLOB` tipo . Este tipo de datos se asigna a la variable `com.adobe.idp.Document` al trabajar con las API de Java de AEM Forms. (Consulte [Pasar datos a servicios de AEM Forms mediante la API de Java](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

A `BLOB` El objeto envía y recupera datos binarios (por ejemplo, archivos PDF, datos XML, etc.) a y desde los servicios de AEM Forms. La variable `BLOB` se define en un WSDL de servicio de la siguiente manera:

```xml
 <complexType name="BLOB">
     <sequence>
         <element maxOccurs="1" minOccurs="0" name="contentType"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="binaryData"
             type="xsd:base64Binary"/>
         <element maxOccurs="1" minOccurs="0" name="attachmentID"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="remoteURL"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="MTOM"
             type="xsd:base64Binary"
             xmime:expectedContentTypes="*/*"
             xmlns:xmime="https://www.w3.org/2005/05/xmlmime"/>
         <element maxOccurs="1" minOccurs="0" name="swaRef"
             type="tns1:swaRef"/>
         <element maxOccurs="1" minOccurs="0" name="attributes"
             type="impl:MyMapOf_xsd_string_To_xsd_anyType"/>
     </sequence>
 </complexType>
```

La variable `MTOM` y `swaRef` solo son compatibles con AEM Forms. Solo puede utilizar estos campos nuevos si especifica una dirección URL que incluya la variable `lc_version` propiedad.

**Suministro de objetos BLOB en solicitudes de servicio**

Si una operación de servicio de AEM Forms requiere un `BLOB` como valor de entrada, cree una instancia de `BLOB` escriba la lógica de la aplicación. (Muchos de los inicios rápidos del servicio web se encuentran en *Programación con formularios AEM* mostrar cómo trabajar con un tipo de datos BLOB).

Asignar valores a campos que pertenecen a la variable `BLOB` de la siguiente manera:

* **Base64**: Para pasar datos como texto codificado en formato Base64, establezca los datos en la variable `BLOB.binaryData` y establezca el tipo de datos en el formato MIME (por ejemplo `application/pdf`) en el `BLOB.contentType` campo . (Consulte [Invocación de AEM Forms mediante la codificación Base64](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**: Para pasar datos binarios en un archivo adjunto MTOM, establezca los datos en la variable `BLOB.MTOM` campo . Esta configuración adjunta los datos a la solicitud SOAP mediante el marco Java JAX-WS o la API nativa del marco SOAP. (Consulte [Invocación de AEM Forms mediante MTOM](#invoking-aem-forms-using-mtom).)
* **SwaRef**: Para pasar datos binarios en un archivo adjunto de SwaRef WS-I, establezca los datos en la variable `BLOB.swaRef` campo . Esta configuración adjunta los datos a la solicitud SOAP mediante el marco Java JAX-WS. (Consulte [Invocación de AEM Forms mediante SwaRef](#invoking-aem-forms-using-swaref).)
* **Adjuntar MIME o DIME**: Para pasar datos en un archivo adjunto MIME o DIME, adjunte los datos a la solicitud SOAP utilizando la API nativa del marco SOAP. Configure el identificador de archivo adjunto en la variable `BLOB.attachmentID` campo . (Consulte [Invocación de AEM Forms mediante la codificación Base64](#invoking-aem-forms-using-base64-encoding).)
* **Dirección URL remota**: Si los datos están alojados en un servidor web y se puede acceder a ellos a través de una URL HTTP, establezca la URL HTTP en la variable `BLOB.remoteURL` campo . (Consulte [Invocación de AEM Forms mediante datos BLOB a través de HTTP](#invoking-aem-forms-using-blob-data-over-http).)

**Acceso a datos en objetos BLOB devueltos por servicios**

El protocolo de transmisión para la devolución `BLOB` Los objetos dependen de varios factores, que se tienen en cuenta en el siguiente orden, y se detienen cuando se cumple la condición principal:

1. **La dirección URL de destino especifica el protocolo de transmisión**. Si la dirección URL de destino especificada en la invocación SOAP contiene el parámetro `blob="`*BLOB_TYPE*&quot;, entonces *BLOB_TYPE* determina el protocolo de transmisión. *BLOB_TYPE* es un marcador de posición para base64, DIME, mime, http, mtom o swaref.
1. **El extremo SOAP del servicio es inteligente**. Si las siguientes condiciones son verdaderas, los documentos de salida se devuelven utilizando el mismo protocolo de transmisión que los documentos de entrada:

   * El parámetro de extremo SOAP del servicio Default Protocol For Output Blob Objects está establecido en Smart.

      Para cada servicio con un extremo SOAP, la consola de administración permite especificar el protocolo de transmisión para cualquier blobs devuelto. (Consulte [ayuda de administración](https://www.adobe.com/go/learn_aemforms_admin_63).)

   * El servicio AEM Forms toma uno o más documentos como entrada.

1. **El extremo SOAP del servicio no es inteligente**. El protocolo configurado determina el protocolo de transmisión del documento y los datos se devuelven en el `BLOB` campo . Por ejemplo, si el extremo SOAP está establecido en DIME, el blob devuelto está en la variable `blob.attachmentID` independientemente del protocolo de transmisión de cualquier documento de entrada.
1. **De otro modo**. Si un servicio no toma el tipo de documento como entrada, los documentos de salida se devuelven en la variable `BLOB.remoteURL` sobre el protocolo HTTP.

Como se describe en la primera condición, puede garantizar el tipo de transmisión de cualquier documento devuelto ampliando la URL del extremo SOAP con un sufijo como se indica a continuación:

```java
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

Esta es la correlación entre los tipos de transmisión y el campo desde el cual se obtienen los datos:

* **Formato Base64**: Configure las variables `blob` sufijo a `base64` para devolver los datos en la variable `BLOB.binaryData` campo .
* **Adjuntar MIME o DIME**: Configure las variables `blob` sufijo a `DIME` o `MIME` para devolver los datos como un tipo de archivo adjunto correspondiente con el identificador de archivo adjunto devuelto en la variable `BLOB.attachmentID` campo . Utilice la API propietaria del marco SOAP para leer los datos del archivo adjunto.
* **Dirección URL remota**: Configure las variables `blob` sufijo a `http` para conservar los datos en el servidor de aplicaciones y devolver la URL que señala a los datos en la variable `BLOB.remoteURL` campo .
* **MTOM o SwaRef**: Configure las variables `blob` sufijo a `mtom` o `swaref` para devolver los datos como un tipo de archivo adjunto correspondiente con el identificador de archivo adjunto devuelto en la variable `BLOB.MTOM` o `BLOB.swaRef` campos. Utilice la API nativa del marco SOAP para leer los datos del archivo adjunto.

>[!NOTE]
>
>Se recomienda que no supere los 30 MB al rellenar un `BLOB` invocando su `setBinaryData` método. De lo contrario, existe la posibilidad de que `OutOfMemory` se produce una excepción.

>[!NOTE]
>
>Las aplicaciones basadas en JAX WS que utilizan el protocolo de transmisión MTOM están limitadas a 25 MB de datos enviados y recibidos. Esta limitación se debe a un error en JAX-WS. Si el tamaño combinado de los archivos enviados y recibidos supera los 25 MB, utilice el protocolo de transmisión SwaRef en lugar del MTOM. De lo contrario, existe la posibilidad de que `OutOfMemory` excepción.

**Transmisión MTOM de matrices de bytes codificadas en base64**

Además del `BLOB` , el protocolo MTOM admite cualquier parámetro de matriz de bytes o campo de matriz de bytes de un tipo complejo. Esto significa que los marcos de SOAP del cliente que admiten MTOM pueden enviar cualquier `xsd:base64Binary` elemento como archivo adjunto MTOM (en lugar de texto codificado en base64). Los extremos SOAP de AEM Forms pueden leer este tipo de codificación de matriz de bytes. Sin embargo, el servicio AEM Forms siempre devuelve un tipo de matriz de bytes como texto codificado en base64. Los parámetros de matriz de bytes de salida no admiten MTOM.

Los servicios de AEM Forms que devuelven una gran cantidad de datos binarios utilizan el tipo Document/BLOB en lugar del tipo de matriz de bytes. El tipo de documento es mucho más eficaz para transmitir grandes cantidades de datos.

## Tipos de datos de servicio web {#web-service-data-types}

En la tabla siguiente se enumeran los tipos de datos Java y se muestra el tipo de datos correspondiente del servicio Web.

<table>
 <thead>
  <tr>
   <th><p>Tipo de datos Java</p></th>
   <th><p>Tipo de datos de servicio web</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>java.lang.byte[]</code></p></td>
   <td><p><code>xsd:base64Binary</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Boolean</code></p></td>
   <td><p><code>xsd:boolean</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Date</code></p></td>
   <td><p>La variable <code>DATE</code> , que se define en un WSDL de servicio de la siguiente manera:</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Si una operación de servicio de AEM Forms requiere un <code>java.util.Date</code> como entrada, la aplicación cliente SOAP debe pasar la fecha en la variable <code>DATE.date</code> campo . Configuración de la variable <code>DATE.calendar</code> en este caso, provoca una excepción de tiempo de ejecución. Si el servicio devuelve un valor <code>java.util.Date</code>, la fecha se devuelve en la variable <code>DATE.date</code> campo .</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p>La variable <code>DATE</code> , que se define en un WSDL de servicio de la siguiente manera:</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Si una operación de servicio de AEM Forms requiere un <code>java.util.Calendar</code> como entrada, la aplicación cliente SOAP debe pasar la fecha en la variable <code>DATE.caledendar</code> campo . Configuración de la variable <code>DATE.date</code> en este caso, genera una excepción en tiempo de ejecución. Si el servicio devuelve un valor <code>java.util.Calendar</code>, la fecha se devuelve en la variable <code>DATE.calendar</code> campo . </p></td>
  </tr>
  <tr>
   <td><p><code>java.math.BigDecimal</code></p></td>
   <td><p><code>xsd:decimal</code></p></td>
  </tr>
  <tr>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p><code>BLOB</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Double</code></p></td>
   <td><p><code>xsd:double</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Float</code></p></td>
   <td><p><code>xsd:float</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Integer</code></p></td>
   <td><p><code>xsd:int</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.List</code></p></td>
   <td><p><code>MyArrayOf_xsd_anyType</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Long</code></p></td>
   <td><p><code>xsd:long</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Map</code></p></td>
   <td><p>La variable <code>apachesoap:Map</code>, que se define en un WSDL de servicio de la siguiente manera:</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>El mapa se representa como una secuencia de pares clave/valor.</p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Object</code></p></td>
   <td><p><code>$1</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Short</code></p></td>
   <td><p><code>xsd:short</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.String</code></p></td>
   <td><p><code>xsd:string</code></p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Document</code></p></td>
   <td><p>El tipo XML, que se define en un WSDL de servicio de la siguiente manera:</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Si una operación de servicio de AEM Forms acepta una <code>org.w3c.dom.Document</code> pase los datos XML en la variable <code>XML.document</code> campo .</p><p>Configuración de la variable <code>XML.element</code> genera una excepción de tiempo de ejecución. Si el servicio devuelve un valor <code>org.w3c.dom.Document</code>, los datos XML se devuelven en la variable <code>XML.document</code> campo .</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>El tipo XML, que se define en un WSDL de servicio de la siguiente manera:</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Si una operación de servicio de AEM Forms requiere un <code>org.w3c.dom.Element</code> como entrada, pase los datos XML en el <code>XML.element</code> campo .</p><p>Configuración de la variable <code>XML.document</code> genera una excepción de tiempo de ejecución. Si el servicio devuelve un valor <code>org.w3c.dom.Element</code>, los datos XML se devuelven en la variable <code>XML.element</code> campo .</p></td>
  </tr>
 </tbody>
</table>

## Creación de clases de proxy Java mediante JAX-WS {#creating-java-proxy-classes-using-jax-ws}

Puede utilizar JAX-WS para convertir un servicio WSDL de Forms a clases proxy de Java. Estas clases permiten invocar operaciones de servicios de AEM Forms. Apache Ant permite crear una secuencia de comandos de compilación que genere clases proxy de Java haciendo referencia a un WSDL de servicio de AEM Forms. Puede generar archivos proxy JAX-WS realizando los siguientes pasos:

1. Instale Apache Ant en el equipo cliente. (Consulte [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).)

   * Añada el directorio bin a la ruta de la clase.
   * Configure las variables `ANT_HOME` al directorio donde instaló Ant.

1. Instale JDK 1.6 o posterior.

   * Añada el directorio JDK bin a su ruta de clase.
   * Añada el directorio JRE bin a la ruta de la clase. Este grupo se encuentra en el `[JDK_INSTALL_LOCATION]/jre` directorio.
   * Configure las variables `JAVA_HOME` al directorio donde instaló el JDK.

   JDK 1.6 incluye el programa wsimport utilizado en el archivo build.xml. JDK 1.5 no incluye ese programa.

1. Instale JAX-WS en el equipo cliente. (Consulte [API de Java para servicios Web XML](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)
1. Utilice JAX-WS y Apache Ant para generar clases proxy de Java. Cree una secuencia de comandos de creación de Ant para realizar esta tarea. El siguiente script es un script de compilación de Ant de ejemplo llamado build.xml:

   ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    
    <project basedir="." default="compile">
    
    <property name="port" value="8080" />
    <property name="host" value="localhost" />
    <property name="username" value="administrator" />
    <property name="password" value="password" />
    <property name="tests" value="all" />
    
    <target name="clean" >
           <delete dir="classes" />
    </target>
    
    <target name="wsdl" depends="clean">
           <mkdir dir="classes"/>
           <exec executable="wsimport" failifexecutionfails="false" failonerror="true" resultproperty="foundWSIMPORT">
               <arg line="-keep -d classes https://${host}:${port}/soap/services/EncryptionService?wsdl&lc_version=9.0.1"/>
           </exec>
           <fail unless="foundWSIMPORT">
              !!! Failed to execute JDK's wsimport tool. Make sure that JDK 1.6 (or later) is on your PATH !!!
           </fail>
    </target>
    
    <target name="compile" depends="clean, wsdl" >
         <javac destdir="./classes" fork="true" debug="true">
            <src path="./src"/>
         </javac>
    </target>
    
    <target name="run">
         <java classname="Client" fork="yes" failonerror="true" maxmemory="200M">
            <classpath>
              <pathelement location="./classes"/>
            </classpath>
            <arg value="${port}"/>
            <arg value="${host}"/>
            <arg value="${username}"/>
            <arg value="${password}"/>
            <arg value="${tests}"/>
         </java>
    </target>
    </project>
   ```

   Dentro de este script de compilación de Ant, observe que la variable `url` se establece para hacer referencia al WSDL del servicio de cifrado que se ejecuta en localhost. La variable `username` y `password` las propiedades deben establecerse en un nombre de usuario y contraseña de los formularios AEM válidos. Observe que la dirección URL contiene la variable `lc_version` atributo. Sin especificar la variable `lc_version` , no puede invocar nuevas operaciones de servicio de AEM Forms.

   >[!NOTE]
   >
   >Reemplazar `EncryptionService`con el nombre de servicio de AEM Forms que desea invocar mediante las clases proxy de Java. Por ejemplo, para crear clases proxy de Java para el servicio de Rights Management, especifique:

   ```java
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. Cree un archivo BAT para ejecutar el script de compilación de Ant. El siguiente comando puede encontrarse dentro de un archivo BAT responsable de ejecutar el script de compilación de Ant:

   ```java
    ant -buildfile "build.xml" wsdl
   ```

   Coloque el script de compilación ANT en C:\Program Files\Java\jaxws-ri\bin directory. El script escribe los archivos JAVA en .carpeta /classes. La secuencia de comandos genera archivos JAVA que pueden invocar el servicio.

1. Empaquete los archivos JAVA en un archivo JAR. Si está trabajando en Eclipse, siga estos pasos:

   * Cree un nuevo proyecto Java que se utilice para empaquetar los archivos JAVA proxy en un archivo JAR.
   * Cree una carpeta de origen en el proyecto.
   * Cree un `com.adobe.idp.services` en la carpeta Source.
   * Seleccione el `com.adobe.idp.services` y, a continuación, importe los archivos JAVA de la carpeta adobe/idp/services en el paquete.
   * Si es necesario, cree un `org/apache/xml/xmlsoap` en la carpeta Source.
   * Seleccione la carpeta de origen y, a continuación, importe los archivos JAVA desde la carpeta org/apache/xml/xmlsoap.
   * Establezca el nivel de cumplimiento del compilador de Java en 5.0 o bueno.
   * Cree el proyecto.
   * Exporte el proyecto como archivo JAR.
   * Importe este archivo JAR en la ruta de clase de un proyecto cliente. Además, importe todos los archivos JAR ubicados en &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty.

   >[!NOTE]
   >
   >Todos los inicios rápidos del servicio web Java (excepto el servicio Forms) ubicados en Programación con formularios AEM crean archivos proxy Java usando JAX-WS. Además, todos los inicios rápidos del servicio web de Java, utilizan SwaRef. (Consulte [Invocación de AEM Forms mediante SwaRef](#invoking-aem-forms-using-swaref).)

**Consulte también lo siguiente**

[Creación de clases de proxy Java mediante el eje Apache](#creating-java-proxy-classes-using-apache-axis)

[Invocación de AEM Forms mediante la codificación Base64](#invoking-aem-forms-using-base64-encoding)

[Invocación de AEM Forms mediante datos BLOB a través de HTTP](#invoking-aem-forms-using-blob-data-over-http)

[Invocación de AEM Forms mediante SwaRef](#invoking-aem-forms-using-swaref)

## Creación de clases de proxy Java mediante el eje Apache {#creating-java-proxy-classes-using-apache-axis}

Puede utilizar la herramienta Java WSDL2del eje Apache para convertir un servicio Forms en clases proxy de Java. Estas clases permiten invocar operaciones de servicio de Forms. Con Apache Ant, puede generar archivos de biblioteca Axis a partir de un WSDL de servicio. Puede descargar el eje de Apache en la URL [https://ws.apache.org/axis/](https://ws.apache.org/axis/).

>[!NOTE]
>
>Los inicios rápidos del servicio web asociados con el servicio Forms utilizan las clases proxy de Java creadas mediante el eje Apache. Los inicios rápidos del servicio web de Forms también utilizan Base64 como tipo de codificación. (Consulte [Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts).)

Puede generar archivos de biblioteca Java del eje siguiendo estos pasos:

1. Instale Apache Ant en el equipo cliente. Está disponible en [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).

   * Añada el directorio bin a la ruta de la clase.
   * Configure las variables `ANT_HOME` al directorio donde instaló Ant.

1. Instale Apache Axis 1.4 en el equipo cliente. Está disponible en [https://ws.apache.org/axis/](https://ws.apache.org/axis/).
1. Configure la ruta de clase para utilizar los archivos JAR del eje en su cliente de servicio web, tal como se describe en las instrucciones de instalación del eje en [https://ws.apache.org/axis/java/install.html](https://ws.apache.org/axis/java/install.html).
1. Utilice la herramienta Apache WSDL2Java en Axis para generar clases proxy de Java. Cree una secuencia de comandos de creación de Ant para realizar esta tarea. El siguiente script es un script de compilación de Ant de ejemplo llamado build.xml:

   ```java
    <?xml version="1.0"?>
    <project name="axis-wsdl2java">
    
    <path id="axis.classpath">
    <fileset dir="C:\axis-1_4\lib" >
        <include name="**/*.jar" />
    </fileset>
    </path>
    
    <taskdef resource="axis-tasks.properties" classpathref="axis.classpath" />
    
    <target name="encryption-wsdl2java-client" description="task">
    <axis-wsdl2java
        output="C:\JavaFiles"
        testcase="false"
        serverside="false"
        verbose="true"
        username="administrator"
        password="password"
        url="http://localhost:8080/soap/services/EncryptionService?wsdl&lc_version=9.0.1" >
    </axis-wsdl2java>
    </target>
    
    </project>
   ```

   Dentro de este script de compilación de Ant, observe que la variable `url` se establece para hacer referencia al WSDL del servicio de cifrado que se ejecuta en localhost. La variable `username` y `password` las propiedades deben establecerse en un nombre de usuario y contraseña de los formularios AEM válidos.

1. Cree un archivo BAT para ejecutar el script de compilación de Ant. El siguiente comando puede encontrarse dentro de un archivo BAT responsable de ejecutar el script de compilación de Ant:

   ```java
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   Los archivos JAVA se escriben en C:\JavaFiles folder as specified by the `output` propiedad. Para invocar correctamente el servicio Forms, importe estos archivos JAVA en la ruta de la clase.

   De forma predeterminada, estos archivos pertenecen a un paquete Java denominado `com.adobe.idp.services`. Se recomienda colocar estos archivos JAVA en un archivo JAR. A continuación, importe el archivo JAR en la ruta de clase de la aplicación cliente.

   >[!NOTE]
   >
   >Existen diferentes maneras de colocar archivos .JAVA en un JAR. Una forma es usar un IDE de Java como Eclipse. Cree un proyecto Java y `com.adobe.idp.services`(todos los archivos .JAVA pertenecen a este paquete). A continuación, importe todos los archivos .JAVA en el paquete. Finalmente, exporte el proyecto como archivo JAR.

1. Modifique la dirección URL en la `EncryptionServiceLocator` para especificar el tipo de codificación. Por ejemplo, para usar base64, especifique `?blob=base64` para garantizar que `BLOB` devuelve datos binarios. Es decir, en la variable `EncryptionServiceLocator` ubique la siguiente línea de código:

   ```java
    http://localhost:8080/soap/services/EncryptionService;
   ```

   y cambie a:

   ```java
    http://localhost:8080/soap/services/EncryptionService?blob=base64;
   ```

1. Agregue los siguientes archivos JAR de eje a la ruta de clase de su proyecto Java:

   * activation.jar
   * axis.jar
   * commons-codec-1.3.jar
   * commons-collections-3.1.jar
   * commons-discovery.jar
   * commons-logging.jar
   * dom3-xml-apis-2.5.0.jar
   * jai_imageio.jar
   * jaxen-1.1-beta-9.jar
   * jaxrpc.jar
   * log4j.jar
   * mail.jar
   * saaj.jar
   * wsdl4j.jar
   * xalan.jar
   * xbean.jar
   * xercesImpl.jar

   Estos archivos JAR están en la `[install directory]/Adobe/Adobe Experience Manager Forms/sdk/lib/thirdparty` directorio.

**Consulte también lo siguiente**

[Creación de clases de proxy Java mediante JAX-WS](#creating-java-proxy-classes-using-jax-ws)

[Invocación de AEM Forms mediante la codificación Base64](#invoking-aem-forms-using-base64-encoding)

[Invocación de AEM Forms mediante datos BLOB a través de HTTP](#invoking-aem-forms-using-blob-data-over-http)

## Invocación de AEM Forms mediante la codificación Base64 {#invoking-aem-forms-using-base64-encoding}

Puede invocar un servicio de AEM Forms utilizando la codificación Base64. La codificación Base64 codifica los archivos adjuntos que se envían con una solicitud de invocación de servicio Web. Es decir, `BLOB` Los datos están codificados en Base64, no en el mensaje SOAP completo.

&quot;Invocación de AEM Forms mediante la codificación Base64&quot; analiza la invocación del siguiente proceso breve de AEM Forms llamado `MyApplication/EncryptDocument` utilizando la codificación Base64.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para seguir con el ejemplo de código, cree un proceso denominado `MyApplication/EncryptDocument` usando Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento PDF no protegido que se pasa al proceso. Esta acción se basa en la variable `SetValue` operación. El parámetro de entrada para este proceso es un `document` variable de proceso denominada `inDoc`.
1. Codifica el documento del PDF con una contraseña. Esta acción se basa en la variable `PasswordEncryptPDF` operación. El documento del PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

### Creación de un ensamblado de cliente .NET que utilice la codificación Base64 {#creating-a-net-client-assembly-that-uses-base64-encoding}

Puede crear un ensamblado de cliente .NET para invocar un servicio Forms desde un proyecto .NET de Microsoft Visual Studio. Para crear un ensamblado de cliente .NET que utilice la codificación base64, realice los siguientes pasos:

1. Cree una clase proxy basada en una URL de invocación de AEM Forms.
1. Cree un proyecto de Microsoft Visual Studio .NET que produzca el ensamblado del cliente .NET.

**Creación de una clase proxy**

Puede crear una clase proxy que se utilice para crear el ensamblado de cliente .NET utilizando una herramienta que acompañe a Microsoft Visual Studio. El nombre de la herramienta es wsdl.exe y se encuentra en la carpeta de instalación de Microsoft Visual Studio. Para crear una clase proxy, abra el símbolo del sistema y vaya a la carpeta que contiene el archivo wsdl.exe. Para obtener más información sobre la herramienta wsdl.exe, consulte la *Ayuda de MSDN*.

Introduzca el siguiente comando en el símbolo del sistema:

```java
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

De forma predeterminada, esta herramienta crea un archivo CS en la misma carpeta que se basa en el nombre del WSDL. En este caso, crea un archivo CS denominado *EncryptDocumentService.cs*. Utilice este archivo CS para crear un objeto proxy que le permita invocar el servicio especificado en la URL de invocación.

Modifique la dirección URL en la clase proxy para incluir `?blob=base64` para garantizar que `BLOB` devuelve datos binarios. En la clase proxy, busque la siguiente línea de código:

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

y cambie a:

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

La variable *Invocación de AEM Forms mediante la codificación Base64* sección utiliza `MyApplication/EncryptDocument` como ejemplo. Si está creando un ensamblado de cliente .NET para otro servicio de Forms, asegúrese de reemplazar `MyApplication/EncryptDocument` con el nombre del servicio.

**Desarrollo del ensamblado del cliente .NET**

Cree un proyecto de Biblioteca de clases de Visual Studio que produzca un ensamblado de cliente .NET. El archivo CS que ha creado con wsdl.exe se puede importar en este proyecto. Este proyecto genera un archivo DLL (el ensamblado cliente .NET) que puede usar en otros proyectos de Visual Studio .NET para invocar un servicio.

1. Inicie Microsoft Visual Studio .NET.
1. Cree un proyecto de Biblioteca de clases y asígnele el nombre DocumentService.
1. Importe el archivo CS que ha creado mediante wsdl.exe.
1. En el **Proyecto** seleccione **Agregar referencia**.
1. En el cuadro de diálogo Agregar referencia, seleccione **System.Web.Services.dll**.
1. Haga clic en **Select** y haga clic en **OK**.
1. Compile y cree el proyecto.

>[!NOTE]
>
>Este procedimiento crea un ensamblado de cliente de .NET llamado DocumentService.dll que puede utilizar para enviar solicitudes SOAP al `MyApplication/EncryptDocument` servicio.

>[!NOTE]
>
>Asegúrese de que ha añadido `?blob=base64` a la URL de la clase proxy que se utiliza para crear el ensamblado cliente .NET. De lo contrario, no se pueden recuperar datos binarios del `BLOB` objeto.

**Referencia al ensamblado de cliente .NET**

Coloque el ensamblado de cliente .NET recién creado en el equipo donde esté desarrollando la aplicación cliente. Después de colocar el ensamblado de cliente .NET en un directorio, puede hacer referencia a él desde un proyecto. Consulte también la `System.Web.Services` biblioteca del proyecto. Si no hace referencia a esta biblioteca, no puede utilizar el ensamblado cliente .NET para invocar un servicio.

1. En el **Proyecto** seleccione **Agregar referencia**.
1. Haga clic en el **.NET** pestaña .
1. Haga clic en **Examinar** y busque el archivo DocumentService.dll.
1. Haga clic en **Select** y haga clic en **OK**.

**Invocación de un servicio mediante un ensamblado cliente .NET que utiliza la codificación Base64**

Puede invocar la variable `MyApplication/EncryptDocument` (que se creó en Workbench) utilizando un ensamblado cliente .NET que utiliza la codificación Base64. Para invocar la variable `MyApplication/EncryptDocument` realice los siguientes pasos:

1. Crear un ensamblado de cliente de Microsoft .NET que consuma el `MyApplication/EncryptDocument` WSDL del servicio.
1. Cree un proyecto cliente de Microsoft .NET. Haga referencia al ensamblado del cliente Microsoft .NET en el proyecto cliente. Referencia también `System.Web.Services`.
1. Con el ensamblado del cliente Microsoft .NET, cree un `MyApplication_EncryptDocumentService` invocando su constructor predeterminado.
1. Configure las variables `MyApplication_EncryptDocumentService` del objeto `Credentials` propiedad con un `System.Net.NetworkCredential` objeto. Dentro de `System.Net.NetworkCredential` constructor, especifique un nombre de usuario de formularios AEM y la contraseña correspondiente. Establezca valores de autenticación para permitir que la aplicación cliente .NET intercambie correctamente mensajes SOAP con AEM Forms.
1. Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar un pase de documento del PDF al `MyApplication/EncryptDocument` proceso.
1. Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento del PDF y el modo en que se abre el archivo.
1. Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
1. Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
1. Rellene el `BLOB` asignando su `binaryData` con el contenido de la matriz de bytes.
1. Invocar el `MyApplication/EncryptDocument` proceso invocando la variable `MyApplication_EncryptDocumentService` del objeto `invoke` y pasando el `BLOB` objeto que contiene el documento PDF. Este proceso devuelve un documento PDF cifrado dentro de un `BLOB` objeto.
1. Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento cifrado con contraseña.
1. Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `MyApplicationEncryptDocumentService` del objeto `invoke` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `binaryData` miembro de datos.
1. Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
1. Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

### Invocación de un servicio mediante clases de proxy Java y codificación Base64 {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}

Puede invocar un servicio de AEM Forms utilizando las clases proxy de Java y Base64. Para invocar la variable `MyApplication/EncryptDocument` mediante las clases proxy de Java, realice los siguientes pasos:

1. Cree clases de proxy Java usando JAX-WS que consuma el `MyApplication/EncryptDocument` WSDL del servicio. Utilice el siguiente extremo WSDL:

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >Reemplazar `hiro-xp` *con la dirección IP del servidor de aplicaciones J2EE que hospeda AEM Forms.*

1. Empaquete las clases de proxy Java creadas usando JAX-WS en un archivo JAR.
1. Incluya el archivo JAR del proxy Java y los archivos JAR ubicados en la siguiente ruta:

   &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   en la ruta de clase de su proyecto cliente Java.

1. Cree un `MyApplicationEncryptDocumentService` usando su constructor.
1. Cree un `MyApplicationEncryptDocument` invocando el objeto `MyApplicationEncryptDocumentService` del objeto `getEncryptDocument` método.
1. Defina los valores de conexión necesarios para invocar AEM Forms asignando valores a los siguientes miembros de datos:

   * Asigne el extremo WSDL y el tipo de codificación a la variable `javax.xml.ws.BindingProvider` del objeto `ENDPOINT_ADDRESS_PROPERTY` campo . Para invocar la variable `MyApplication/EncryptDocument` con la codificación Base64, especifique el siguiente valor de URL:

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * Asigne el usuario de AEM formularios al `javax.xml.ws.BindingProvider` del objeto `USERNAME_PROPERTY` campo .
   * Asigne el valor de contraseña correspondiente a la variable `javax.xml.ws.BindingProvider` del objeto `PASSWORD_PROPERTY` campo .

   El siguiente ejemplo de código muestra esta lógica de aplicación:

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Recupere el documento del PDF para enviarlo al `MyApplication/EncryptDocument` proceso creando un `java.io.FileInputStream` usando su constructor. Pase un valor de cadena que especifique la ubicación del documento del PDF.
1. Cree una matriz de bytes y rellénela con el contenido del `java.io.FileInputStream` objeto.
1. Cree un `BLOB` usando su constructor.
1. Rellene el `BLOB` invocando su `setBinaryData` y pasando la matriz de bytes. La variable `BLOB` del objeto `setBinaryData` es el método al que se llama cuando se utiliza la codificación Base64. Consulte Suministro de objetos BLOB en solicitudes de servicio.
1. Invocar el `MyApplication/EncryptDocument` proceso invocando la variable `MyApplicationEncryptDocument` del objeto `invoke` método. Pase el `BLOB` objeto que contiene el documento PDF. El método invoke devuelve un valor `BLOB` objeto que contiene el documento de PDF cifrado.
1. Cree una matriz de bytes que contenga el documento del PDF cifrado invocando la variable `BLOB` del objeto `getBinaryData` método.
1. Guarde el documento de PDF cifrado como archivo de PDF. Escriba la matriz de bytes en un archivo.

**Consulte también lo siguiente**

[Inicio rápido: Invocación de un servicio mediante archivos proxy Java y codificación Base64](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice la codificación Base64](#creating-a-net-client-assembly-that-uses-base64-encoding)

## Invocación de AEM Forms mediante MTOM {#invoking-aem-forms-using-mtom}

Puede invocar los servicios de AEM Forms utilizando el MTOM estándar del servicio web. Este estándar define cómo se transmiten los datos binarios, como un documento PDF, a través de Internet o intranet. Una característica de MTOM es el uso de la variable `XOP:Include` elemento. Este elemento se define en la especificación XML Binary Optimized Packaging (XOP) para hacer referencia a los archivos adjuntos binarios de un mensaje SOAP.

La discusión aquí es sobre el uso de MTOM para invocar el siguiente proceso breve de AEM Forms llamado `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para seguir con el ejemplo de código, cree un proceso denominado `MyApplication/EncryptDocument` usando Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento PDF no protegido que se pasa al proceso. Esta acción se basa en la variable `SetValue` operación. El parámetro de entrada para este proceso es un `document` variable de proceso denominada `inDoc`.
1. Codifica el documento del PDF con una contraseña. Esta acción se basa en la variable `PasswordEncryptPDF` operación. El documento del PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

>[!NOTE]
>
>Se agregó compatibilidad con MTOM en AEM Forms, versión 9.

>[!NOTE]
>
>Las aplicaciones basadas en JAX WS que utilizan el protocolo de transmisión MTOM están limitadas a 25 MB de datos enviados y recibidos. Esta limitación se debe a un error en JAX-WS. Si el tamaño combinado de los archivos enviados y recibidos supera los 25 MB, utilice el protocolo de transmisión SwaRef en lugar del MTOM. De lo contrario, existe la posibilidad de que `OutOfMemory` excepción.

La discusión aquí es sobre el uso de MTOM dentro de un proyecto de Microsoft .NET para invocar los servicios de AEM Forms. El .NET framework utilizado es 3.5 y el entorno de desarrollo es Visual Studio 2008. Si tiene instalado Web Service Enhances (WSE) en el equipo de desarrollo, elimínelo. El marco de trabajo de .NET 3.5 es compatible con un marco SOAP denominado Windows Communication Foundation (WCF). Al invocar AEM Forms utilizando MTOM, solo se admite WCF (no WSE).

### Creación de un proyecto de .NET que invoque un servicio mediante MTOM {#creating-a-net-project-that-invokes-a-service-using-mtom}

Puede crear un proyecto de Microsoft .NET que pueda invocar un servicio de AEM Forms mediante servicios Web. En primer lugar, cree un proyecto de Microsoft .NET utilizando Visual Studio 2008. Para invocar un servicio de AEM Forms, cree una referencia de servicio al servicio de AEM Forms que desee invocar en el proyecto. Cuando cree una referencia de servicio, especifique una URL para el servicio de AEM Forms:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

Reemplazar `localhost` con la dirección IP del servidor de aplicaciones J2EE que hospeda AEM Forms. Reemplazar `MyApplication/EncryptDocument` con el nombre del servicio de AEM Forms que se va a invocar. Por ejemplo, para invocar una operación de Rights Management, especifique:

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

La variable `lc_version` garantiza que la funcionalidad de AEM Forms, como MTOM, esté disponible. Sin especificar la variable `lc_version` no puede invocar AEM Forms mediante MTOM.

Después de crear una referencia de servicio, los tipos de datos asociados con el servicio AEM Forms están disponibles para su uso en el proyecto .NET. Para crear un proyecto de .NET que invoque un servicio de AEM Forms, realice los pasos siguientes:

1. Cree un proyecto .NET con Microsoft Visual Studio 2008.
1. En el **Proyecto** seleccione **Agregar referencia de servicio**.
1. En el **Dirección** , especifique el WSDL en el servicio de AEM Forms. Por ejemplo,

   ```java
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. Haga clic en **Ir** y haga clic en **OK**.

### Invocación de un servicio mediante MTOM en un proyecto .NET {#invoking-a-service-using-mtom-in-a-net-project}

Tenga en cuenta las `MyApplication/EncryptDocument` proceso que acepta un documento de PDF no protegido y devuelve un documento de PDF cifrado con contraseña. Para invocar la variable `MyApplication/EncryptDocument` (que se creó en Workbench) mediante MTOM, realice los siguientes pasos:

1. Cree un proyecto de Microsoft .NET.
1. Cree un `MyApplication_EncryptDocumentClient` usando su constructor predeterminado.
1. Cree un `MyApplication_EncryptDocumentClient.Endpoint.Address` usando la variable `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms y el tipo de codificación:

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   No es necesario que use la variable `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, asegúrese de especificar `?blob=mtom`.

   >[!NOTE]
   >
   >Reemplazar `hiro-xp` *con la dirección IP del servidor de aplicaciones J2EE que hospeda AEM Forms.*

1. Cree un `System.ServiceModel.BasicHttpBinding` obteniendo el valor de `EncryptDocumentClient.Endpoint.Binding` miembro de datos. Conversión del valor devuelto a `BasicHttpBinding`.
1. Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` miembro de datos a `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
1. Habilite la autenticación HTTP básica realizando las siguientes tareas:

   * Asignar el nombre de usuario de los formularios AEM al miembro de datos `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`.
   * Asignar el valor de contraseña correspondiente al miembro de datos `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`.
   * Asignar el valor constante `HttpClientCredentialType.Basic` al miembro de datos `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al miembro de datos `BasicHttpBindingSecurity.Security.Mode`.

   El siguiente ejemplo de código muestra estas tareas.

   ```java
    //Enable BASIC HTTP authentication
    encryptProcess.ClientCredentials.UserName.UserName = "administrator";
    encryptProcess.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 4000000;
    b.MaxBufferSize = 4000000;
    b.ReaderQuotas.MaxArrayLength = 4000000;
   ```

1. Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para almacenar un documento del PDF que se pasa al `MyApplication/EncryptDocument` proceso.
1. Cree un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento del PDF y el modo en que se abre el archivo.
1. Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la variable `System.IO.FileStream` del objeto `Length` propiedad.
1. Rellene la matriz de bytes con los datos de flujo invocando la variable `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
1. Rellene el `BLOB` asignando su `MTOM` miembro de datos con el contenido de la matriz de bytes.
1. Invocar el `MyApplication/EncryptDocument` proceso invocando la variable `MyApplication_EncryptDocumentClient` del objeto `invoke` método. Pase el `BLOB` objeto que contiene el documento PDF. Este proceso devuelve un documento PDF cifrado dentro de un `BLOB` objeto.
1. Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento de PDF protegido.
1. Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `invoke` método. Rellene la matriz de bytes obteniendo el valor de la variable `BLOB` del objeto `MTOM` miembro de datos.
1. Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
1. Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

>[!NOTE]
>
>La mayoría de las operaciones de servicio de AEM Forms tienen un inicio rápido MTOM. Puede ver estos inicios rápidos en la sección de inicio rápido correspondiente de un servicio. Por ejemplo, para ver la sección Salida de inicio rápido , consulte [Inicio rápido de la API del servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**Consulte también lo siguiente**

[Inicio rápido: Invocación de un servicio mediante MTOM en un proyecto .NET](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[Acceso a varios servicios mediante servicios web](#accessing-multiple-services-using-web-services)

[Creación de una aplicación web ASP.NET que invoque un proceso prolongado centrado en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## Invocación de AEM Forms mediante SwaRef {#invoking-aem-forms-using-swaref}

Puede invocar los servicios de AEM Forms mediante SwaRef. El contenido de la variable `wsi:swaRef` El elemento XML se envía como archivo adjunto dentro de un cuerpo SOAP que almacena la referencia al archivo adjunto. Al invocar un servicio de Forms mediante SwaRef, cree clases de proxy de Java utilizando la API de Java para los servicios web XML (JAX-WS). (Consulte [API de Java para servicios Web XML](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)

La discusión aquí es sobre invocar el siguiente proceso de corta duración de Forms llamado `MyApplication/EncryptDocument` usando SwaRef.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para seguir con el ejemplo de código, cree un proceso denominado `MyApplication/EncryptDocument` usando Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento PDF no protegido que se pasa al proceso. Esta acción se basa en la variable `SetValue` operación. El parámetro de entrada para este proceso es un `document` variable de proceso denominada `inDoc`.
1. Codifica el documento del PDF con una contraseña. Esta acción se basa en la variable `PasswordEncryptPDF` operación. El documento del PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

>[!NOTE]
>
>Se agregó compatibilidad con SwaRef en AEM Forms

La siguiente discusión es sobre cómo invocar los servicios de Forms usando SwaRef dentro de una aplicación cliente Java. La aplicación Java utiliza clases proxy creadas mediante JAX-WS.

### Invocar un servicio utilizando archivos de biblioteca JAX-WS que utilicen SwaRef {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}

Para invocar la variable `MyApplication/EncryptDocument` Para procesar mediante archivos proxy Java creados con JAX-WS y SwaRef, siga estos pasos:

1. Cree clases de proxy Java usando JAX-WS que consuma el `MyApplication/EncryptDocument` WSDL del servicio. Utilice el siguiente extremo WSDL:

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   Para obtener más información, consulte [Creación de clases de proxy Java mediante JAX-WS](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >Reemplazar `hiro-xp` *con la dirección IP del servidor de aplicaciones J2EE que hospeda AEM Forms.*

1. Empaquete las clases de proxy Java creadas usando JAX-WS en un archivo JAR.
1. Incluya el archivo JAR del proxy Java y los archivos JAR ubicados en la siguiente ruta:

   &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   en la ruta de clase de su proyecto cliente Java.

1. Cree un `MyApplicationEncryptDocumentService` usando su constructor.
1. Cree un `MyApplicationEncryptDocument` invocando el objeto `MyApplicationEncryptDocumentService` del objeto `getEncryptDocument` método.
1. Defina los valores de conexión necesarios para invocar AEM Forms asignando valores a los siguientes miembros de datos:

   * Asigne el extremo WSDL y el tipo de codificación a la variable `javax.xml.ws.BindingProvider` del objeto `ENDPOINT_ADDRESS_PROPERTY` campo . Para invocar la variable `MyApplication/EncryptDocument` con la codificación SwaRef, especifique el siguiente valor URL:

      ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * Asigne el usuario de AEM formularios al `javax.xml.ws.BindingProvider` del objeto `USERNAME_PROPERTY` campo .
   * Asigne el valor de contraseña correspondiente a la variable `javax.xml.ws.BindingProvider` del objeto `PASSWORD_PROPERTY` campo .

   El siguiente ejemplo de código muestra esta lógica de aplicación:

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Recupere el documento del PDF para enviarlo al `MyApplication/EncryptDocument` proceso creando un `java.io.File` usando su constructor. Pase un valor de cadena que especifique la ubicación del documento del PDF.
1. Cree un `javax.activation.DataSource` usando la variable `FileDataSource` constructor. Pase el `java.io.File` objeto.
1. Cree un `javax.activation.DataHandler` usando su constructor y pasando el `javax.activation.DataSource` objeto.
1. Cree un `BLOB` usando su constructor.
1. Rellene el `BLOB` invocando su `setSwaRef` y pasando el `javax.activation.DataHandler` objeto.
1. Invocar el `MyApplication/EncryptDocument` proceso invocando la variable `MyApplicationEncryptDocument` del objeto `invoke` y pasando el `BLOB` objeto que contiene el documento PDF. El método invoke devuelve un valor `BLOB` objeto que contiene un documento de PDF cifrado.
1. Rellenar un `javax.activation.DataHandler` invocando el objeto `BLOB` del objeto `getSwaRef` método.
1. Convertir el `javax.activation.DataHandler` a `java.io.InputSteam` invocando la variable `javax.activation.DataHandler` del objeto `getInputStream` método.
1. Escriba el `java.io.InputSteam` a un archivo PDF que representa el documento PDF cifrado.

>[!NOTE]
>
>La mayoría de las operaciones de servicio de AEM Forms tienen un inicio rápido de SwaRef. Puede ver estos inicios rápidos en la sección de inicio rápido correspondiente de un servicio. Por ejemplo, para ver la sección Salida de inicio rápido , consulte [Inicio rápido de la API del servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**Consulte también lo siguiente**

[Inicio rápido: Invocación de un servicio mediante SwaRef en un proyecto Java](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## Invocación de AEM Forms mediante datos BLOB a través de HTTP {#invoking-aem-forms-using-blob-data-over-http}

Puede invocar los servicios de AEM Forms mediante servicios web y pasando datos BLOB a través de HTTP. Pasar datos BLOB a través de HTTP es una técnica alternativa en lugar de usar codificación base64, DIME o MIME. Por ejemplo, puede pasar datos sobre HTTP en un proyecto de Microsoft .NET que utilice la mejora del servicio web 3.0, que no admite DIME ni MIME. Al utilizar datos BLOB a través de HTTP, los datos de entrada se cargan antes de que se invoque el servicio AEM Forms .

&quot;Invocación de AEM Forms mediante datos BLOB sobre HTTP&quot; discute la invocación del siguiente proceso breve de AEM Forms llamado `MyApplication/EncryptDocument` pasando datos BLOB a través de HTTP.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para seguir con el ejemplo de código, cree un proceso denominado `MyApplication/EncryptDocument` usando Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento PDF no protegido que se pasa al proceso. Esta acción se basa en la variable `SetValue` operación. El parámetro de entrada para este proceso es un `document` variable de proceso denominada `inDoc`.
1. Codifica el documento del PDF con una contraseña. Esta acción se basa en la variable `PasswordEncryptPDF` operación. El documento del PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

>[!NOTE]
>
>Se recomienda que esté familiarizado con la invocación de AEM Forms mediante SOAP. (Consulte [Invocación de AEM Forms mediante servicios web](#invoking-aem-forms-using-web-services).)

### Creación de un ensamblado de cliente .NET que utilice datos a través de HTTP {#creating-a-net-client-assembly-that-uses-data-over-http}

Para crear un ensamblado de cliente que utilice datos sobre HTTP, siga el proceso especificado en [Invocación de AEM Forms mediante la codificación Base64](#invoking-aem-forms-using-base64-encoding). Sin embargo, modifique la URL en la clase proxy para incluir `?blob=http` en lugar de `?blob=base64`. Esta acción garantiza que los datos se pasen a través de HTTP. En la clase proxy, busque la siguiente línea de código:

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

y cambie a:

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**Referencia al ensamblado de .NET clienMyApplication/EncryptDocumentt**

Coloque el nuevo ensamblado de cliente .NET en el equipo donde esté desarrollando la aplicación cliente. Después de colocar el ensamblado de cliente .NET en un directorio, puede hacer referencia a él desde un proyecto. Consulte la `System.Web.Services` biblioteca del proyecto. Si no hace referencia a esta biblioteca, no puede utilizar el ensamblado cliente .NET para invocar un servicio.

1. En el **Proyecto** seleccione **Agregar referencia**.
1. Haga clic en el **.NET** pestaña .
1. Haga clic en **Examinar** y busque el archivo DocumentService.dll.
1. Haga clic en **Select** y haga clic en **OK**.

**Invocación de un servicio mediante un ensamblado de cliente .NET que utiliza datos BLOB a través de HTTP**

Puede invocar la variable `MyApplication/EncryptDocument` (que se creó en Workbench) utilizando un ensamblado de cliente .NET que utiliza datos a través de HTTP. Para invocar la variable `MyApplication/EncryptDocument` realice los siguientes pasos:

1. Cree el ensamblado cliente .NET.
1. Haga referencia al ensamblado del cliente Microsoft .NET. Cree un proyecto cliente de Microsoft .NET. Haga referencia al ensamblado del cliente Microsoft .NET en el proyecto cliente. Referencia también `System.Web.Services`.
1. Con el ensamblado del cliente Microsoft .NET, cree un `MyApplication_EncryptDocumentService` invocando su constructor predeterminado.
1. Configure las variables `MyApplication_EncryptDocumentService` del objeto `Credentials` propiedad con un `System.Net.NetworkCredential` objeto. Dentro de `System.Net.NetworkCredential` constructor, especifique un nombre de usuario de formularios AEM y la contraseña correspondiente. Establezca valores de autenticación para permitir que la aplicación cliente .NET intercambie correctamente mensajes SOAP con AEM Forms.
1. Cree un `BLOB` usando su constructor. La variable `BLOB` se utiliza para pasar datos al `MyApplication/EncryptDocument` proceso.
1. Asignar un valor de cadena a la variable `BLOB` del objeto `remoteURL` miembro de datos que especifica la ubicación URI de un documento de PDF para pasar al `MyApplication/EncryptDocument`servicio.
1. Invocar el `MyApplication/EncryptDocument` proceso invocando la variable `MyApplication_EncryptDocumentService` del objeto `invoke` y pasando el `BLOB` objeto. Este proceso devuelve un documento PDF cifrado dentro de un `BLOB` objeto.
1. Cree un `System.UriBuilder` usando su constructor y pasando el valor del `BLOB` del objeto `remoteURL` miembro de datos.
1. Convertir el `System.UriBuilder` a `System.IO.Stream` objeto. (El Inicio rápido C# que sigue esta lista ilustra cómo realizar esta tarea).
1. Cree una matriz de bytes y rellénela con los datos ubicados en la variable `System.IO.Stream` objeto.
1. Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
1. Escriba el contenido de la matriz de bytes en un archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

### Invocación de un servicio mediante clases proxy de Java y datos BLOB a través de HTTP {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}

Puede invocar un servicio de AEM Forms utilizando clases proxy de Java y datos BLOB a través de HTTP. Para invocar la variable `MyApplication/EncryptDocument` mediante las clases proxy de Java, realice los siguientes pasos:

1. Cree clases de proxy Java usando JAX-WS que consuma el `MyApplication/EncryptDocument` WSDL del servicio. Utilice el siguiente extremo WSDL:

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   Para obtener más información, consulte [Creación de clases de proxy Java mediante JAX-WS](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >Reemplazar `hiro-xp` *con la dirección IP del servidor de aplicaciones J2EE que hospeda AEM Forms.*

1. Empaquete las clases de proxy Java creadas usando JAX-WS en un archivo JAR.
1. Incluya el archivo JAR del proxy Java y los archivos JAR ubicados en la siguiente ruta:

   &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   en la ruta de clase de su proyecto cliente Java.

1. Cree un `MyApplicationEncryptDocumentService` usando su constructor.
1. Cree un `MyApplicationEncryptDocument` invocando el objeto `MyApplicationEncryptDocumentService` del objeto `getEncryptDocument` método.
1. Defina los valores de conexión necesarios para invocar AEM Forms asignando valores a los siguientes miembros de datos:

   * Asigne el extremo WSDL y el tipo de codificación a la variable `javax.xml.ws.BindingProvider` del objeto `ENDPOINT_ADDRESS_PROPERTY` campo . Para invocar la variable `MyApplication/EncryptDocument` mediante la codificación BLOB sobre HTTP, especifique el siguiente valor de URL:

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * Asigne el usuario de AEM formularios al `javax.xml.ws.BindingProvider` del objeto `USERNAME_PROPERTY` campo .
   * Asigne el valor de contraseña correspondiente a la variable `javax.xml.ws.BindingProvider` del objeto `PASSWORD_PROPERTY` campo .

   El siguiente ejemplo de código muestra esta lógica de aplicación:

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Cree un `BLOB` usando su constructor.
1. Rellene el `BLOB` invocando su `setRemoteURL` método. Pase un valor de cadena que especifique la ubicación URI de un documento de PDF para pasarlo a la variable `MyApplication/EncryptDocument` servicio.
1. Invocar el `MyApplication/EncryptDocument` proceso invocando la variable `MyApplicationEncryptDocument` del objeto `invoke` y pasando el `BLOB` objeto que contiene el documento PDF. Este proceso devuelve un documento PDF cifrado dentro de un `BLOB` objeto.
1. Cree una matriz de bytes para almacenar el flujo de datos que representa el documento del PDF cifrado. Invocar el `BLOB` del objeto `getRemoteURL` (utilice el método `BLOB` objeto devuelto por el `invoke` método).
1. Cree un `java.io.File` usando su constructor. Este objeto representa el documento de PDF cifrado.
1. Cree un `java.io.FileOutputStream` usando su constructor y pasando el `java.io.File` objeto.
1. Invocar el `java.io.FileOutputStream` del objeto `write` método. Pase la matriz de bytes que contiene el flujo de datos que representa el documento del PDF cifrado.

## Invocación de AEM Forms mediante DIME {#invoking-aem-forms-using-dime}

Puede invocar los servicios de AEM Forms mediante SOAP con archivos adjuntos. AEM Forms admite los estándares de servicio web MIME y DIME. DIME permite enviar archivos adjuntos binarios, como documentos PDF, junto con solicitudes de invocación en lugar de codificar el archivo adjunto. La variable *Invocación de AEM Forms mediante DIME* se trata de invocar el siguiente proceso de corta duración de AEM Forms llamado `MyApplication/EncryptDocument` uso de DIME.

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento PDF no protegido que se pasa al proceso. Esta acción se basa en la variable `SetValue` operación. El parámetro de entrada para este proceso es un `document` variable de proceso denominada `inDoc`.
1. Codifica el documento del PDF con una contraseña. Esta acción se basa en la variable `PasswordEncryptPDF` operación. El documento del PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

Este proceso no se basa en un proceso de AEM Forms existente. Para seguir junto con los ejemplos de código, cree un proceso denominado `MyApplication/EncryptDocument` usando Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

>[!NOTE]
>
>La invocación de operaciones de servicio de AEM Forms mediante DIME está en desuso. Se recomienda utilizar MTOM. (Consulte [Invocación de AEM Forms mediante MTOM](#invoking-aem-forms-using-mtom).)

### Creación de un proyecto de .NET que utilice DIME {#creating-a-net-project-that-uses-dime}

Para crear un proyecto de .NET que pueda invocar un servicio de Forms mediante DIME, realice las siguientes tareas:

* Instale las mejoras de los servicios web 2.0 en su equipo de desarrollo.
* Desde el proyecto .NET, cree una referencia web al servicio Forms de FormsAEM.

**Instalación de mejoras de servicios web 2.0**

Instale las mejoras de los servicios web 2.0 en el equipo de desarrollo e inclúyalo con Microsoft Visual Studio .NET. Puede descargar las mejoras de los servicios web 2.0 desde la [Centro de descargas de Microsoft.](https://www.microsoft.com/downloads/search.aspx)

Desde esta página web, busque Mejoras en los servicios web 2.0 y descárguela en su equipo de desarrollo. Esta descarga coloca un archivo denominado Microsoft WSE 2.0 SPI.msi en el equipo. Ejecute el programa de instalación y siga las instrucciones en línea.

>[!NOTE]
>
>Mejoras en los servicios web 2.0 admite DIME. La versión compatible de Microsoft Visual Studio es 2003 cuando se trabaja con las mejoras de los servicios web 2.0. Las mejoras de los servicios web 3.0 no son compatibles con DIME; sin embargo, es compatible con MTOM.

**Creación de una referencia web para un servicio AEM Forms**

Después de instalar las mejoras de servicios web 2.0 en el equipo de desarrollo y crear un proyecto de Microsoft .NET, cree una referencia web al servicio de Forms. Por ejemplo, para crear una referencia web a la variable `MyApplication/EncryptDocument` procese y suponiendo que Forms esté instalado en el equipo local, especifique la siguiente URL:

```java
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

Después de crear una referencia web, los dos tipos de datos proxy siguientes están disponibles para usar en el proyecto .NET: `EncryptDocumentService` y `EncryptDocumentServiceWse`. Para invocar la variable `MyApplication/EncryptDocument` procesar mediante DIME, utilice la variable `EncryptDocumentServiceWse` tipo .

>[!NOTE]
>
>Antes de crear una referencia web al servicio Forms, asegúrese de hacer referencia a las mejoras de los servicios web 2.0 en su proyecto. (Consulte &quot;Instalación de mejoras de servicios web 2.0&quot;).

**Referencia a la biblioteca WSE**

1. En el menú Proyecto, seleccione Agregar referencia.
1. En el cuadro de diálogo Agregar referencia, seleccione Microsoft.Web.Services2.dll.
1. Seleccione System.Web.Services.dll.
1. Haga clic en Seleccionar y, a continuación, en Aceptar.

**Creación de una referencia web a un servicio de Forms**

1. En el menú Proyecto, seleccione Agregar referencia web.
1. En el cuadro de diálogo URL, especifique la URL del servicio de Forms.
1. Haga clic en Ir y, a continuación, en Agregar referencia.

>[!NOTE]
>
>Asegúrese de habilitar el proyecto .NET para utilizar la biblioteca WSE. Desde el Explorador de proyectos, haga clic con el botón derecho en el nombre del proyecto y seleccione Habilitar WSE 2.0. Asegúrese de que la casilla de verificación del cuadro de diálogo que aparece esté seleccionada.

**Invocación de un servicio mediante DIME en un proyecto .NET**

Puede invocar un servicio de Forms mediante DIME. Tenga en cuenta las `MyApplication/EncryptDocument` proceso que acepta un documento de PDF no protegido y devuelve un documento de PDF cifrado con contraseña. Para invocar la variable `MyApplication/EncryptDocument` Para procesar mediante DIME, siga estos pasos:

1. Cree un proyecto de Microsoft .NET que le permita invocar un servicio de Forms mediante DIME. Asegúrese de incluir las mejoras de los servicios web 2.0 y crear una referencia web al servicio AEM Forms.
1. Después de configurar una referencia web a la variable `MyApplication/EncryptDocument` proceso, crear un `EncryptDocumentServiceWse` usando su constructor predeterminado.
1. Configure las variables `EncryptDocumentServiceWse` del objeto `Credentials` miembro de datos con un `System.Net.NetworkCredential` que especifica el nombre de usuario y el valor de contraseña de los formularios AEM.
1. Cree un `Microsoft.Web.Services2.Dime.DimeAttachment` usando su constructor y pasando los siguientes valores:

   * Un valor de cadena que especifica un valor GUID. Puede obtener un valor de GUID invocando la variable `System.Guid.NewGuid.ToString` método.
   * Un valor de cadena que especifica el tipo de contenido. Dado que este proceso requiere un documento del PDF, especifique `application/pdf`.
   * A `TypeFormat` valor de enumeración. Especifique `TypeFormat.MediaType`.
   * Un valor de cadena que especifica la ubicación del documento de PDF que se pasará al proceso de AEM Forms.

1. Cree un `BLOB` usando su constructor.
1. Añadir el adjunto DIME al `BLOB` asignando la variable `Microsoft.Web.Services2.Dime.DimeAttachment` del objeto `Id` valor del miembro de datos en la variable `BLOB` del objeto `attachmentID` miembro de datos.
1. Invocar el `EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add` y pase el `Microsoft.Web.Services2.Dime.DimeAttachment` objeto.
1. Invocar el `MyApplication/EncryptDocument` proceso invocando la variable `EncryptDocumentServiceWse` del objeto `invoke` y pasando el `BLOB` objeto que contiene el adjunto DIME. Este proceso devuelve un documento PDF cifrado dentro de un `BLOB` objeto.
1. Obtenga el valor del identificador de datos adjuntos obteniendo el valor de la variable devuelta `BLOB` del objeto `attachmentID` miembro de datos.
1. Iterar a través de los archivos adjuntos ubicados en `EncryptDocumentServiceWse.ResponseSoapContext.Attachments` y utilice el valor del identificador de archivo adjunto para obtener el documento del PDF cifrado.
1. Obtenga una `System.IO.Stream` obteniendo el valor de `Attachment` del objeto `Stream` miembro de datos.
1. Cree una matriz de bytes y pase esa matriz de bytes a la `System.IO.Stream` del objeto `Read` método. Este método rellena la matriz de bytes con un flujo de datos que representa el documento de PDF cifrado.
1. Cree un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de un archivo PDF. Este objeto representa el documento de PDF cifrado.
1. Cree un `System.IO.BinaryWriter` invocando su constructor y pasando el `System.IO.FileStream` objeto.
1. Escriba el contenido de la matriz de bytes en el archivo de PDF invocando la variable `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

### Creación de clases proxy Java del eje Apache que utilizan DIME {#creating-apache-axis-java-proxy-classes-that-use-dime}

Puede utilizar la herramienta Java WSDL2del eje Apache para convertir un WSDL de servicio en clases proxy de Java, de modo que pueda invocar operaciones de servicio. Con Apache Ant, puede generar archivos de biblioteca Axis desde un WSDL del servicio AEM Forms que le permita invocar el servicio. (Consulte [Creación de clases de proxy Java mediante el eje Apache](#creating-java-proxy-classes-using-apache-axis).)

La herramienta Java WSDL2del eje Apache genera archivos JAVA que contienen métodos que se utilizan para enviar solicitudes SOAP a un servicio. Las bibliotecas generadas por el eje descodifican las solicitudes SOAP recibidas por un servicio y las vuelven a convertir en métodos y argumentos.

Para invocar la variable `MyApplication/EncryptDocument` (que se creó en Workbench) utilizando archivos de biblioteca generados por el eje y DIME, realice los siguientes pasos:

1. Cree clases de proxy Java que consuman la variable `MyApplication/EncryptDocument` servicio WSDL utilizando Apache Axis. (Consulte [Creación de clases de proxy Java mediante el eje Apache](#creating-java-proxy-classes-using-apache-axis).)
1. Incluya las clases proxy de Java en la ruta de clase.
1. Cree un `MyApplicationEncryptDocumentServiceLocator` usando su constructor.
1. Cree un `URL` usando su constructor y pasando un valor de cadena que especifica la definición WSDL del servicio AEM Forms. Asegúrese de especificar `?blob=dime` al final de la URL del extremo SOAP. Por ejemplo, use

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. Cree un `EncryptDocumentSoapBindingStub` invocando su constructor y pasando el `MyApplicationEncryptDocumentServiceLocator`y `URL` objeto.
1. Establezca el nombre de usuario y el valor de contraseña de los formularios AEM invocando la variable `EncryptDocumentSoapBindingStub` del objeto `setUsername` y `setPassword` métodos.

   ```java
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. Recupere el documento del PDF para enviarlo al `MyApplication/EncryptDocument` creando un `java.io.File` objeto. Pase un valor de cadena que especifique la ubicación del documento del PDF.
1. Cree un `javax.activation.DataHandler` usando su constructor y pasando un `javax.activation.FileDataSource` objeto. La variable `javax.activation.FileDataSource` puede crearse usando su constructor y pasando el `java.io.File` que representa el documento PDF.
1. Cree un `org.apache.axis.attachments.AttachmentPart` usando su constructor y pasando el `javax.activation.DataHandler` objeto.
1. Adjunte el archivo adjunto invocando la variable `EncryptDocumentSoapBindingStub` del objeto `addAttachment` y pasando el `org.apache.axis.attachments.AttachmentPart` objeto.
1. Cree un `BLOB` usando su constructor. Rellene el `BLOB` objeto con el valor del identificador de datos adjuntos invocando la variable `BLOB` del objeto `setAttachmentID` y pasando el valor del identificador de datos adjuntos. Este valor se puede obtener invocando la variable `org.apache.axis.attachments.AttachmentPart` del objeto `getContentId` método.
1. Invocar el `MyApplication/EncryptDocument` proceso invocando la variable `EncryptDocumentSoapBindingStub` del objeto `invoke` método. Pase el `BLOB` objeto que contiene el adjunto DIME. Este proceso devuelve un documento PDF cifrado dentro de un `BLOB` objeto.
1. Obtenga el valor del identificador de archivo adjunto invocando el valor devuelto `BLOB` del objeto `getAttachmentID` método. Este método devuelve un valor de cadena que representa el valor identificador del archivo adjunto devuelto.
1. Recupere los archivos adjuntos invocando la variable `EncryptDocumentSoapBindingStub` del objeto `getAttachments` método. Este método devuelve una matriz de `Objects` que representan los archivos adjuntos.
1. Iterar a través de los archivos adjuntos (la variable `Object` matriz) y utilice el valor del identificador de archivo adjunto para obtener el documento del PDF cifrado. Cada elemento es un `org.apache.axis.attachments.AttachmentPart` objeto.
1. Obtenga la variable `javax.activation.DataHandler` objeto asociado al archivo adjunto invocando la variable `org.apache.axis.attachments.AttachmentPart` del objeto `getDataHandler` método.
1. Obtenga una `java.io.FileStream` invocando el objeto `javax.activation.DataHandler` del objeto `getInputStream` método.
1. Cree una matriz de bytes y pase esa matriz de bytes a la `java.io.FileStream` del objeto `read` método. Este método rellena la matriz de bytes con un flujo de datos que representa el documento de PDF cifrado.
1. Cree un `java.io.File` usando su constructor. Este objeto representa el documento de PDF cifrado.
1. Cree un `java.io.FileOutputStream` usando su constructor y pasando el `java.io.File` objeto.
1. Invocar el `java.io.FileOutputStream` del objeto `write` y pase la matriz de bytes que contiene el flujo de datos que representa el documento del PDF cifrado.

**Consulte también lo siguiente**

[Inicio rápido: Invocación de un servicio mediante DIME en un proyecto Java](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## Uso de autenticación basada en SAML {#using-saml-based-authentication}

AEM Forms admite varios modos de autenticación de servicios web al invocar servicios. Un modo de autenticación especifica un nombre de usuario y un valor de contraseña utilizando un encabezado de autorización básico en la llamada de servicio web. AEM Forms también admite la autenticación basada en afirmaciones SAML. Cuando una aplicación cliente invoca un servicio AEM Forms mediante un servicio Web, la aplicación cliente puede proporcionar información de autenticación de una de las siguientes maneras:

* Pasar credenciales como parte de la autorización básica
* Pasar el token de nombre de usuario como parte del encabezado WS-Security
* Pasar una afirmación SAML como parte del encabezado WS-Security
* Pasar el token Kerberos como parte del encabezado WS-Security

AEM Forms no admite la autenticación basada en certificados estándar, pero sí la autenticación basada en certificados de forma distinta.

>[!NOTE]
>
>El inicio rápido del servicio web en Programación con AEM Forms especifica los valores de nombre de usuario y contraseña para realizar la autorización.

La identidad de AEM usuarios de formularios se puede representar mediante una afirmación SAML firmada con una clave secreta. El siguiente código XML muestra un ejemplo de una afirmación SAML.

```xml
 <Assertion xmlns="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:saml="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:samlp="urn:oasis:names:tc:SAML:1.0:protocol"
     AssertionID="fd4bd0c87302780e0d9bbfa8726d5bc0" IssueInstant="2008-04-17T13:47:00.720Z" Issuer="LiveCycle"
     MajorVersion="1" MinorVersion="1">
     <Conditions NotBefore="2008-04-17T13:47:00.720Z" NotOnOrAfter="2008-04-17T15:47:00.720Z">
     </Conditions>
     <AuthenticationStatement
         AuthenticationInstant="2008-04-17T13:47:00.720Z"
         AuthenticationMethod="urn:oasis:names:tc:SAML:1.0:am:unspecified">
         <Subject>
             <NameIdentifier NameQualifier="DefaultDom">administrator</NameIdentifier>
             <SubjectConfirmation>
                 <ConfirmationMethod>urn:oasis:names:tc:SAML:1.0:cm:sender-vouches</ConfirmationMethod>
             </SubjectConfirmation>
         </Subject>
     </AuthenticationStatement>
     <ds:Signature >
         <ds:SignedInfo>
             <ds:CanonicalizationMethod Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#"></ds:CanonicalizationMethod>
             <ds:SignatureMethod    Algorithm="https://www.w3.org/2000/09/xmldsig#hmac-sha1"></ds:SignatureMethod>
             <ds:Reference URI="#fd4bd0c87302780e0d9bbfa8726d5bc0">
                 <ds:Transforms>
                     <ds:Transform Algorithm="https://www.w3.org/2000/09/xmldsig#enveloped-signature"></ds:Transform>
                     <ds:Transform Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#">
                         <ec:InclusiveNamespaces
                             PrefixList="code ds kind rw saml samlp typens #default">
                         </ec:InclusiveNamespaces>
                     </ds:Transform>
                 </ds:Transforms>
                 <ds:DigestMethod Algorithm="https://www.w3.org/2000/09/xmldsig#sha1"></ds:DigestMethod>
                 <ds:DigestValue>hVrtqjWr+VzaVUIpQx0YI9lIjaY=</ds:DigestValue>
             </ds:Reference>
         </ds:SignedInfo>
         <ds:SignatureValue>UMbBb+cUcPtcWDCIhXes4n4FxfU=</ds:SignatureValue>
     </ds:Signature>
 </Assertion>
```

Este ejemplo de afirmación se emite para un usuario administrador. Esta afirmación contiene los siguientes elementos visibles:

* Es válido durante un tiempo determinado.
* Se emite para un usuario en particular.
* Se firma digitalmente. Así que cualquier modificación que se le haga rompería la firma.
* Se puede presentar a AEM Forms como un token de identidad del usuario similar al nombre de usuario y la contraseña.

Una aplicación cliente puede recuperar la afirmación de cualquier API de AEM Forms AuthenticationManager que devuelva una `AuthResult` objeto. Puede obtener una `AuthResult` realizando uno de los dos métodos siguientes:

* Autenticación del usuario mediante cualquiera de los métodos de autenticación expuestos por la API de AuthenticationManager. Normalmente, se utilizarían el nombre de usuario y la contraseña; sin embargo, también puede utilizar la autenticación de certificado.
* Al usar la variable `AuthenticationManager.getAuthResultOnBehalfOfUser` método. Este método permite que una aplicación cliente obtenga un `AuthResult` para cualquier usuario de formularios AEM.

un usuario de AEM forms puede autenticarse utilizando un token SAML obtenido. Esta afirmación SAML (fragmento xml) se puede enviar como parte del encabezado WS-Security con la llamada del servicio web para la autenticación de usuarios. Normalmente, una aplicación cliente ha autenticado a un usuario, pero no ha almacenado las credenciales del usuario. (O el usuario ha iniciado sesión en ese cliente a través de un mecanismo que no sea usar un nombre de usuario y una contraseña). En este caso, la aplicación cliente debe invocar AEM Forms y suplantar a un usuario específico al que se le permite invocar AEM Forms.

Para suplantar a un usuario específico, invoque la función `AuthenticationManager.getAuthResultOnBehalfOfUser` mediante un servicio web. Este método devuelve un `AuthResult` que contiene la afirmación SAML para ese usuario.

A continuación, utilice esa afirmación SAML para invocar cualquier servicio que requiera autenticación. Esta acción implica enviar la afirmación como parte del encabezado SOAP. Cuando se realiza una llamada de servicio web con esta afirmación, AEM Forms identifica al usuario como el representado por esa afirmación. Es decir, el usuario especificado en la afirmación es el usuario que invoca el servicio.

### Uso de clases de Apache Axis y autenticación basada en SAML {#using-apache-axis-classes-and-saml-based-authentication}

Puede invocar un servicio de AEM Forms mediante las clases proxy de Java que se crearon con la biblioteca Axis . (Consulte [Creación de clases de proxy Java mediante el eje Apache](#creating-java-proxy-classes-using-apache-axis).)

Cuando utilice AXIS que utilice autenticación basada en SAML, registre la solicitud y el controlador de respuesta con Axis. Apache Axis invoca al controlador antes de enviar una solicitud de invocación a AEM Forms. Para registrar un controlador, cree una clase Java que se amplíe `org.apache.axis.handlers.BasicHandler`.

**Creación de un controlador de aserción con eje**

La siguiente clase Java, denominada `AssertionHandler.java`, muestra un ejemplo de una clase Java que se amplía `org.apache.axis.handlers.BasicHandler`.

```java
 public class AssertionHandler extends BasicHandler {
        public void invoke(MessageContext ctx) throws AxisFault {
            String assertion = (String) ctx.getProperty(LC_ASSERTION);
 
            //no assertion hence nothing to insert
            if(assertion == null) return;
 
            try {
                MessageElement samlElement = new MessageElement(convertToXML(assertion));
                SOAPHeader header = (SOAPHeader) ctx.getRequestMessage().getSOAPHeader();
                //Create the wsse:Security element which would contain the SAML element
                SOAPElement wsseHeader = header.addChildElement("Security", "wsse", WSSE_NS);
                wsseHeader.appendChild(samlElement);
                //remove the actor attribute as in LC we do not specify any actor. This would not remove the actor attribute though
                //it would only remove it from the soapenv namespace
                wsseHeader.getAttributes().removeNamedItem("actor");
            } catch (SOAPException e) {
                throw new AxisFault("Error occured while adding the assertion to the SOAP Header",e);
            }
        }
 }
```

**Registrar el controlador**

Para registrar un controlador con Axis, cree un archivo client-config.wsdd. De forma predeterminada, Axis busca un archivo con este nombre. El siguiente código XML es un ejemplo de archivo client-config.wsdd. Consulte la documentación del eje para obtener más información.

```xml
 <deployment xmlns="https://xml.apache.org/axis/wsdd/" xmlns:java="https://xml.apache.org/axis/wsdd/providers/java">
     <transport name="http" pivot="java:org.apache.axis.transport.http.HTTPSender"/>
      <globalConfiguration >
       <requestFlow >
        <handler type="java:com.adobe.idp.um.example.AssertionHandler" />
       </requestFlow >
      </globalConfiguration >
 </deployment>
 
```

**Invocar un servicio de AEM Forms**

El siguiente ejemplo de código invoca un servicio de AEM Forms mediante autenticación basada en SAML.

```java
 public class ImpersonationExample {
        . . .
        public void  authenticateOnBehalf(String superUsername,String password,
                String canonicalName,String domainName) throws UMException, RemoteException{
            ((org.apache.axis.client.Stub) authenticationManager).setUsername(superUsername);
            ((org.apache.axis.client.Stub) authenticationManager).setPassword(password);
 
            //Step 1 - Invoke the Auth manager api to get an assertion for the user to be impersonated
            AuthResult ar = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            String assertion = ar.getAssertion();
            //Step 2 - Setting the assertion here to be picked later by the AssertionHandler. Note that stubs are not threadSafe
            //hence should not be reused. For this simple example we have made them instance variable but care should be taken
            //regarding the thread safety
            ((javax.xml.rpc.Stub) authorizationManager)._setProperty(AssertionHandler.LC_ASSERTION, assertion);
        }
 
        public Role findRole(String roleId) throws UMException, RemoteException{
            //This api would be invoked under bob's user rights
            return authorizationManager.findRole(roleId);
        }
 
        public static void main(String[] args) throws Exception {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            //Get the SAML assertion for the user to impersonate and store it in stub
            ie.authenticateOnBehalf(
                    "administrator", //The Super user which has the required impersonation permission
                    "password", // Password of the super user as referred above
                    "bob", //Cannonical name of the user to impersonate
                    "testdomain" //Domain of the user to impersonate
                    );
 
            Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.out.println("Role "+r.getName());
        }
 }
```

### Uso de un ensamblado de cliente .NET y autenticación basada en SAML {#using-a-net-client-assembly-and-saml-based-authentication}

Puede invocar un servicio de Forms utilizando un ensamblado de cliente .NET y una autenticación basada en SAML. Para ello, debe utilizar las mejoras del servicio web 3.0 (WSE). Para obtener información sobre la creación de un ensamblado de cliente .NET que utilice WSE, consulte [Creación de un proyecto de .NET que utilice DIME](#creating-a-net-project-that-uses-dime).

>[!NOTE]
>
>La sección DIME utiliza WSE 2.0. Para utilizar la autenticación basada en SAML, siga las mismas instrucciones especificadas en el tema DIME. Sin embargo, sustituya WSE 2.0 por WSE 3.0. Instale las mejoras 3.0 de los servicios web en el equipo de desarrollo e inclúyalo con Microsoft Visual Studio .NET. Puede descargar las mejoras de los servicios web 3.0 desde la [Centro de descargas de Microsoft](https://www.microsoft.com/downloads/search.aspx).

La arquitectura WSE utiliza los tipos de datos Directivas, Aserciones y SecurityToken. Brevemente, para una llamada de servicio web, especifique una directiva. Una política puede tener varias aserciones. Cada afirmación puede contener filtros. Se invoca un filtro en determinadas etapas de una llamada de servicio web y, en ese momento, puede modificar la solicitud SOAP. Para obtener más información, consulte la documentación sobre las mejoras del servicio web 3.0 .

**Crear la aserción y el filtro**

El siguiente ejemplo de código C# crea clases de filtro y afirmación. En este ejemplo de código se crea un SamlAssertionOutputFilter. El marco WSE invoca este filtro antes de que la solicitud SOAP se envíe a AEM Forms.

```java
 class LCSamlPolicyAssertion : Microsoft.Web.ServicES4.Design.PolicyAssertion
 {
        public override Microsoft.Web.ServicES4.SoapFilter CreateClientOutputFilter(FilterCreationContext context)
        {
           return new SamlAssertionOutputFilter();
        }
        . . .
 }
 
 
 class SamlAssertionOutputFilter : SendSecurityFilter
 {
        public override void SecureMessage(SoapEnvelope envelope, Security security)
        {
           // Get the SamlToken from the SessionState
           SamlToken samlToken = envelope.Context.Credentials.UltimateReceiver.GetClientToken<SamlToken>();
           security.Tokens.Add(samlToken);
        }
 }
```

**Creación del token SAML**

Cree una clase para representar la afirmación SAML. La tarea principal que realiza esta clase es convertir los valores de datos de cadena a xml y conservar el espacio en blanco. Este xml de afirmación se importa posteriormente en la solicitud SOAP.

```java
 class SamlToken : SecurityToken
 {
        public const string SAMLAssertion = "https://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1";
        private XmlElement _assertionElement;
 
        public SamlToken(string assertion)
             : base(SAMLAssertion)
        {
           XmlDocument xmlDoc = new XmlDocument();
           //The white space has to be preserved else the digital signature would get broken
           xmlDoc.PreserveWhitespace = true;
           xmlDoc.LoadXml(assertion);
           _assertionElement = xmlDoc.DocumentElement;
         }
 
         public override XmlElement GetXml(XmlDocument document)
         {
            return (XmlElement)document.ImportNode(_assertionElement, true);
         }
        . . .
 }
```

**Invocar un servicio de AEM Forms**

El siguiente ejemplo de código C# invoca un servicio de Forms mediante autenticación basada en SAML.

```java
 public class ImpersonationExample
 {
        . . .
        public void AuthenticateOnBehalf(string superUsername, string password, string canonicalName, string domainName)
        {
            //Create a policy for UsernamePassword Token
            Policy usernamePasswordPolicy = new Policy();
            usernamePasswordPolicy.Assertions.Add(new UsernameOverTransportAssertion());
 
            UsernameToken token = new UsernameToken(superUsername, password, PasswordOption.SendPlainText);
            authenticationManager.SetClientCredential(token);
            authenticationManager.SetPolicy(usernamePasswordPolicy);
 
            //Get the SAML assertion for impersonated user
            AuthClient.AuthenticationManagerService.AuthResult ar
                = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            System.Console.WriteLine("Received assertion " + ar.assertion);
 
            //Create a policy for inserting SAML assertion
            Policy samlPolicy = new Policy();
            samlPolicy.Assertions.Add(new LCSamlPolicyAssertion());
            authorizationManager.SetPolicy(samlPolicy);
            //Set the SAML assertion obtained previously as the token
            authorizationManager.SetClientCredential(new SamlToken(ar.assertion));
        }
 
        public Role findRole(string roleId)
        {
            return authorizationManager.findRole(roleId);
        }
 
        static void Main(string[] args)
        {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            ie.AuthenticateOnBehalf(
                 "administrator", //The Super user which has the required impersonation permission
                 "password", // Password of the super user as referred above
                 "bob", //Cannonical name of the user to impersonate
                 "testdomain" //Domain of the user to impersonate
                 );
 
         Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.Console.WriteLine("Role "+r.name);
     }
 }
```

## Consideraciones relacionadas al utilizar servicios web {#related-considerations-when-using-web-services}

A veces se producen problemas al invocar determinadas operaciones de servicios de AEM Forms mediante servicios web. El objetivo de este debate es determinar esas cuestiones y proporcionar una solución, si se dispone de ellas.

### Invocación asincrónica de operaciones de servicio {#invoking-service-operations-asynchronously}

Si intenta invocar de forma asíncrona una operación de servicio de AEM Forms, como la de Generación de PDF `htmlToPDF` operación, una `SoapFaultException` ocurre. Para resolver este problema, cree un archivo XML de enlace personalizado que asigne la variable `ExportPDF_Result` elementos y otros elementos en clases diferentes. El siguiente XML representa un archivo de enlace personalizado.

```xml
 <bindings
        xmlns:xsd="https://www.w3.org/2001/XMLSchema"
        xmlns:jxb="https://java.sun.com/xml/ns/jaxb" jxb:version="1.0"
        xmlns:wsdl="https://schemas.xmlsoap.org/wsdl/"
      wsdlLocation="http://localhost:8080/soap/services/GeneratePDFService?wsdl&async=true&lc_version=9.0.0"
        xmlns="https://java.sun.com/xml/ns/jaxws">
        <enableAsyncMapping>false</enableAsyncMapping>
        <package name="external_customize.client"/>
        <enableWrapperStyle>true</enableWrapperStyle>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='ExportPDF_Result']">
            <jxb:class name="ExportPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='CreatePDF_Result']">
            <jxb:class name="CreatePDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='OptimizePDF_Result']">
            <jxb:class name="OptimizePDFAsyncResult">
            </jxb:class>
        </bindings>
        <!--bindings node="//wsdl:portType[@name='GeneratePDFService']/wsdl:operation[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult"/>
        </bindings-->
 </bindings>
```

Utilice este archivo XML al crear archivos proxy Java mediante JAX-WS. (Consulte [Creación de clases de proxy Java mediante JAX-WS](#creating-java-proxy-classes-using-jax-ws).)

Haga referencia a este archivo XML al ejecutar la herramienta JAX-WS (wsimport.exe) utilizando el `b` línea de comandos. Actualice el `wsdlLocation` en el archivo XML de enlace para especificar la URL de AEM Forms.

Para garantizar que la invocación asincrónica funcione, modifique el valor de la URL del punto final y especifique `async=true`. Por ejemplo, para los archivos proxy de Java que se crean con JAX-WS, especifique lo siguiente para la variable `BindingProvider.ENDPOINT_ADDRESS_PROPERTY`.

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

La siguiente lista especifica otros servicios que necesitan un archivo de enlace personalizado cuando se invocan de forma asíncrona:

* PDFG3D
* Administrador de tareas
* Administrador de aplicaciones
* Administrador de directorios
* Distiller
* Rights Management
* Gestión de documentos

### Diferencias en los servidores de aplicaciones J2EE {#differences-in-j2ee-application-servers}

A veces, una biblioteca proxy creada con un servidor de aplicaciones J2EE específico no invoca correctamente AEM Forms alojado en un servidor de aplicaciones J2EE diferente. Considere una biblioteca proxy que se genera mediante AEM Forms y que se implementa en WebSphere. Esta biblioteca proxy no puede invocar correctamente los servicios de AEM Forms que se implementan en el servidor de aplicaciones JBoss.

Algunos tipos de datos complejos de AEM Forms, como `PrincipalReference`, se definen de forma diferente cuando AEM Forms se implementa en WebSphere en comparación con JBoss Application Server. Las diferencias en los JDK utilizados por los diferentes servicios de aplicaciones J2EE son la razón por la que hay diferencias en las definiciones de WSDL. Como resultado, utilice bibliotecas proxy generadas desde el mismo servidor de aplicaciones J2EE.

### Acceso a varios servicios mediante servicios web {#accessing-multiple-services-using-web-services}

Debido a conflictos de área de nombres, los objetos de datos no se pueden compartir entre varios WSDL de servicio. Los distintos servicios pueden compartir tipos de datos y, por lo tanto, los servicios comparten la definición de estos tipos en los WSDL. Por ejemplo, no se pueden agregar dos ensamblados de cliente .NET que contengan `BLOB` tipo de datos en el mismo proyecto cliente .NET. Si intenta hacerlo, se producirá un error de compilación.

La siguiente lista especifica los tipos de datos que no se pueden compartir entre varios WSDL de servicio:

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

Para evitar este problema, se recomienda que califique completamente los tipos de datos. Por ejemplo, considere una aplicación .NET que haga referencia tanto al servicio de Forms como al servicio de firmas mediante una referencia de servicio. Ambas referencias de servicio contendrán un `BLOB` Clase . Para usar un `BLOB` , califique completamente la variable `BLOB` cuando lo declare. Este enfoque se muestra en el siguiente ejemplo de código. Para obtener información sobre este ejemplo de código, consulte [Firma digital de Forms interactivo](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms).

El siguiente ejemplo de código C# firma un formulario interactivo procesado por el servicio Forms. La aplicación cliente tiene dos referencias de servicio. La variable `BLOB` la instancia asociada al servicio de Forms pertenece al `SignInteractiveForm.ServiceReference2` espacio de nombres. Del mismo modo, la variable `BLOB` la instancia asociada con el servicio de firma pertenece al grupo `SignInteractiveForm.ServiceReference1` espacio de nombres. El formulario interactivo firmado se guarda como un archivo PDF denominado *LoanXFASigned.pdf*.

```csharp
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
     *
     * For information, see "Invoking AEM Forms using MTOM" in Programming with AEM forms
     */
 using System;
 using System.Collections.Generic;
 using System.Linq;
 using System.Text;
 using System.ServiceModel;
 using System.IO;
 
 //A reference to the Signature service
 using SignInteractiveForm.ServiceReference1;
 
 //A reference to the Forms service
 using SignInteractiveForm.ServiceReference2;
 
 namespace SignInteractiveForm
 {
        class Program
        {
            static void Main(string[] args)
            {
                try
                {
                    //Because BLOB objects are used in both service references
                    //it is necessary to fully-qualify the BLOB objects
 
                    //Retrieve the form -- invoke the Forms service
                    SignInteractiveForm.ServiceReference2.BLOB formData = GetForm();
 
                    //Create a BLOB object associated with the Signature service
                    SignInteractiveForm.ServiceReference1.BLOB sigData = new SignInteractiveForm.ServiceReference1.BLOB();
 
                    //Transfer the byte stream from one Forms BLOB object to the
                    //Signature BLOB object
                    sigData.MTOM = formData.MTOM;
 
                    //Sign the Form -- invoke the Signature service
                    SignForm(sigData);
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
 
            //Creates an interactive PDF form based on a XFA form - invoke the Forms service
            private static SignInteractiveForm.ServiceReference2.BLOB GetForm()
            {
 
                try
                {
                    //Create a FormsServiceClient object
                    FormsServiceClient formsClient = new FormsServiceClient();
                    formsClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FormsService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)formsClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    formsClient.ClientCredentials.UserName.UserName = "administrator";
                    formsClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Create a BLOB to store form data
                    SignInteractiveForm.ServiceReference2.BLOB formData = new SignInteractiveForm.ServiceReference2.BLOB();
                    SignInteractiveForm.ServiceReference2.BLOB pdfForm = new SignInteractiveForm.ServiceReference2.BLOB();
 
                    //Specify a XML form data
                    string path = "C:\\Adobe\Loan.xml";
                    FileStream fs = new FileStream(path, FileMode.Open);
 
                    //Get the length of the file stream
                    int len = (int)fs.Length;
                    byte[] ByteArray = new byte[len];
 
                    fs.Read(ByteArray, 0, len);
                    formData.MTOM = ByteArray;
 
                    //Specify a XML form data
                    string path2 = "C:\\Adobe\LoanSigXFA.pdf";
                    FileStream fs2 = new FileStream(path2, FileMode.Open);
 
                    //Get the length of the file stream
                    int len2 = (int)fs2.Length;
                    byte[] ByteArray2 = new byte[len2];
 
                    fs2.Read(ByteArray2, 0, len2);
                    pdfForm.MTOM = ByteArray2;
 
                    PDFFormRenderSpec renderSpec = new PDFFormRenderSpec();
                    renderSpec.generateServerAppearance = true;
 
                    //Set out parameter values
                    long pageCount = 1;
                    String localValue = "en_US";
                    FormsResult result = new FormsResult();
 
                    //Render an interactive PDF form
                    formsClient.renderPDFForm2(
                        pdfForm,
                        formData,
                        renderSpec,
                        null,
                        null,
                        out pageCount,
                        out localValue,
                        out result);
 
                    //Write the data stream to the BLOB object
                    SignInteractiveForm.ServiceReference2.BLOB outForm = result.outputContent;
                    return outForm;
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
                return null;
            }
 
            //Sign the form -- invoke the Signature service
            private static void SignForm(SignInteractiveForm.ServiceReference1.BLOB inDoc)
            {
 
                try
                {
                    //Create a SignatureServiceClient object
                    SignatureServiceClient signatureClient = new SignatureServiceClient();
                    signatureClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/SignatureService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)signatureClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    signatureClient.ClientCredentials.UserName.UserName = "administrator";
                    signatureClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Specify the name of the signature field
                    string fieldName = "form1[0].grantApplication[0].page1[0].SignatureField1[0]";
 
                    //Create a Credential object
                    Credential myCred = new Credential();
                    myCred.alias = "secure";
 
                    //Specify the reason to sign the document
                    string reason = "The document was reviewed";
 
                    //Specify the location of the signer
                    string location = "New York HQ";
 
                    //Specify contact information
                    string contactInfo = "Tony Blue";
 
                    //Create a PDFSignatureAppearanceOptions object
                    //and show date information
                    PDFSignatureAppearanceOptionSpec appear = new PDFSignatureAppearanceOptionSpec();
                    appear.showDate = true;
 
                    //Sign the PDF document
                    SignInteractiveForm.ServiceReference1.BLOB signedDoc = signatureClient.sign(
                        inDoc,
                        fieldName,
                        myCred,
                        HashAlgorithm.SHA1,
                        reason,
                        location,
                        contactInfo,
                        appear,
                        true,
                        null,
                        null,
                        null);
 
                    //Populate a byte array with BLOB data that represents the signed form
                    byte[] outByteArray = signedDoc.MTOM;
 
                    //Save the signed PDF document
                    string fileName = "C:\\Adobe\LoanXFASigned.pdf";
                    FileStream fs2 = new FileStream(fileName, FileMode.OpenOrCreate);
 
                    //Create a BinaryWriter object
                    BinaryWriter w = new BinaryWriter(fs2);
                    w.Write(outByteArray);
                    w.Close();
                    fs2.Close();
                }
 
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
        }
 }
 
 
```

### Los servicios que comienzan con la letra producen archivos proxy no válidos {#services-starting-with-the-letter-i-produce-invalid-proxy-files}

El nombre de algunas clases proxy generadas por AEM Forms es incorrecto al usar Microsoft .Net 3.5 y WCF. Este problema se produce cuando se crean clases proxy para IBMFilenetContentRepositoryConnector, IDPSchedulerService o cualquier otro servicio cuyo nombre comience por la letra I. Por ejemplo, el nombre del cliente generado en el caso de IBMFileNetContentRepositoryConnector es `BMFileNetContentRepositoryConnectorClient`. Falta la letra I en la clase proxy generada.
