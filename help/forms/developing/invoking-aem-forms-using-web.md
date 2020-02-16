---
title: Invocación de AEM Forms mediante servicios Web
seo-title: Invocación de AEM Forms mediante servicios Web
description: nulo
seo-description: nulo
uuid: 66bcd010-c476-4b66-831d-a48307d8d67a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: d5722281-bea9-4fc7-abdc-e678899e0a15
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Invocación de AEM Forms mediante servicios Web {#invoking-aem-forms-using-web-services}

La mayoría de los servicios de AEM Forms del contenedor de servicios están configurados para exponer un servicio Web, con compatibilidad total con la generación del lenguaje de definición de servicio Web (WSDL). Es decir, puede crear objetos proxy que consuman la pila SOAP nativa de un servicio de AEM Forms. Como resultado, los servicios de AEM Forms pueden intercambiar y procesar los siguientes mensajes SOAP:

* **Solicitud** SOAP: Enviado a un servicio de Forms por una aplicación cliente que solicita una acción.
* **Respuesta** SOAP: Enviado a una aplicación cliente por un servicio de Forms después de procesar una solicitud SOAP.

Con los servicios web, puede realizar las mismas operaciones de servicios de AEM Forms que con la API de Java. La ventaja de utilizar servicios web para invocar los servicios de AEM Forms es que puede crear una aplicación cliente en un entorno de desarrollo compatible con SOAP. Una aplicación cliente no está vinculada a un entorno de desarrollo o lenguaje de programación específicos. Por ejemplo, puede crear una aplicación cliente utilizando Microsoft Visual Studio .NET y C# como lenguaje de programación.

Los servicios de AEM Forms se exponen a través del protocolo SOAP y son compatibles con WSI Basic Profile 1.1. La interoperabilidad de los servicios Web (WSI) es una organización de estándares abiertos que promueve la interoperabilidad de los servicios Web entre plataformas. Para obtener más información, consulte [https://www.ws-i.org/](https://www.ws-i.org).

AEM Forms admite los siguientes estándares de servicio web:

* **Codificación**: Solo admite codificación de documento y literal (que es la codificación preferida según el perfil básico de WSI). (Consulte [Invocación de formularios AEM mediante codificación](#invoking-aem-forms-using-base64-encoding)Base64).
* **MTOM**: Representa una forma de codificar datos adjuntos con solicitudes SOAP. (Consulte [Invocación de formularios AEM mediante MTOM](#invoking-aem-forms-using-mtom)).
* **SwaRef**: Representa otra forma de codificar datos adjuntos con solicitudes SOAP. (Consulte [Invocación de formularios AEM mediante SwaRef](#invoking-aem-forms-using-swaref)).
* **SOAP con datos adjuntos**: Admite MIME y DIME (Encapsulación directa de mensajes de Internet). Estos protocolos son formas estándar de enviar archivos adjuntos a través de SOAP. Las aplicaciones Microsoft Visual Studio .NET utilizan DIME. (Consulte [Invocación de formularios AEM mediante codificación](#invoking-aem-forms-using-base64-encoding)Base64).
* **WS-Security**: Admite un perfil de token de contraseña de nombre de usuario, que es una forma estándar de enviar nombres de usuario y contraseñas como parte del encabezado SOAP de seguridad de WS. AEM Forms también admite la autenticación básica HTTP. (Consulte [Paso de credenciales mediante encabezados](https://www.adobe.com/devnet/livecycle/articles/passing_credentials.html)WS-Security).

Para invocar los servicios de AEM Forms mediante un servicio web, normalmente se crea una biblioteca proxy que consume el servicio WSDL. La sección *Invocar formularios AEM mediante servicios* Web utiliza JAX-WS para crear clases proxy de Java e invocar servicios. (Consulte [Creación de clases proxy de Java mediante JAX-WS](#creating-java-proxy-classes-using-jax-ws)).

Puede recuperar un WDSL de servicio especificando la siguiente definición de URL (los elementos entre corchetes son opcionales):

```as3
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

donde:

* *your_serverhost* representa la dirección IP del servidor de aplicaciones J2EE que aloja AEM Forms.
* *your_port* representa el puerto HTTP que utiliza el servidor de aplicaciones J2EE.
* *service_name* representa el nombre del servicio.
* *la versión* representa la versión de destino de un servicio (se utiliza la última versión de servicio de forma predeterminada).
* `async` especifica el valor `true` para habilitar operaciones adicionales para la invocación asincrónica ( `false` de forma predeterminada).
* *lc_version* representa la versión de AEM Forms que desea invocar.

En la tabla siguiente se enumeran las definiciones de WSDL de servicio (suponiendo que AEM Forms se implementa en el host local y que el anuncio es 8080).

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
   <td><p>DocumentManagement</p></td>
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
   <td><p>Utilidades de PDF </p></td>
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
   <td><p>Utilidades XMP</p></td>
   <td><p><code>http://localhost:8080/soap/services/ XMPUtilityService?wsdl</code></p></td>
  </tr>
 </tbody>
</table>

**Definiciones WSDL de proceso de AEM Forms**

Debe especificar el nombre de la aplicación y el nombre del proceso en la definición WSDL para acceder a un WSDL que pertenece a un proceso creado en Workbench. Supongamos que el nombre de la aplicación es `MyApplication` y que el nombre del proceso es `EncryptDocument`. En este caso, especifique la siguiente definición WSDL:

```as3
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>Para obtener información sobre el proceso de corta duración de ejemplo `MyApplication/EncryptDocument` , consulte Ejemplo [de proceso de](/help/forms/developing/aem-forms-processes.md)corta duración.

>[!NOTE]
>
>Una aplicación puede contener carpetas. En este caso, especifique los nombres de carpeta en la definición WSDL:

```as3
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**Acceso a nuevas funciones mediante servicios Web**

Se puede acceder a la nueva funcionalidad del servicio de AEM Forms mediante servicios web. Por ejemplo, en AEM Forms, se introduce la capacidad de codificar archivos adjuntos mediante MTOM. (Consulte [Invocación de formularios AEM mediante MTOM](#invoking-aem-forms-using-mtom)).

Para acceder a las nuevas funciones introducidas en AEM Forms, especifique el `lc_version` atributo en la definición WSDL. Por ejemplo, para acceder a la nueva funcionalidad de servicio (incluida la compatibilidad con MTOM), especifique la siguiente definición WSDL:

```as3
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>Al configurar el `lc_version` atributo, asegúrese de que utiliza tres dígitos. Por ejemplo, 9.0.1 es igual a la versión 9.0.

**Tipo de datos BLOB de servicio Web**

Los WSDL del servicio de AEM Forms definen muchos tipos de datos. Uno de los tipos de datos más importantes expuestos en un servicio Web es un `BLOB` tipo. Este tipo de datos se asigna a la `com.adobe.idp.Document` clase cuando se trabaja con las API de Java de AEM Forms. (Consulte [Paso de datos a los servicios de AEM Forms mediante la API](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)de Java).

Un `BLOB` objeto envía y recupera datos binarios (por ejemplo, archivos PDF, datos XML, etc.) desde y hacia los servicios de AEM Forms. El tipo `BLOB` se define en un WSDL de servicio de la siguiente manera:

```as3
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

Los campos `MTOM` y `swaRef` solo se admiten en AEM Forms. Estos campos nuevos solo se pueden usar si se especifica una URL que incluya la `lc_version` propiedad.

**Suministro de objetos BLOB en solicitudes de servicio**

Si una operación de servicio de AEM Forms requiere un `BLOB` tipo como valor de entrada, cree una instancia del `BLOB` tipo en la lógica de la aplicación. (Muchos de los inicios rápidos del servicio web ubicados en *Programación con formularios* AEM muestran cómo trabajar con un tipo de datos BLOB).

Asigne valores a los campos que pertenecen a la `BLOB` instancia de la siguiente manera:

* **Base64**: Para pasar datos como texto codificado en formato Base64, establezca los datos en el `BLOB.binaryData` campo y defina el tipo de datos en formato MIME (por ejemplo `application/pdf`) en el `BLOB.contentType` campo. (Consulte [Invocación de formularios AEM mediante codificación](#invoking-aem-forms-using-base64-encoding)Base64).
* **MTOM**: Para pasar datos binarios en un archivo adjunto MTOM, establezca los datos en el `BLOB.MTOM` campo. Esta configuración adjunta los datos a la solicitud SOAP mediante el marco JAX-WS de Java o la API nativa del marco SOAP. (Consulte [Invocación de formularios AEM mediante MTOM](#invoking-aem-forms-using-mtom)).
* **SwaRef**: Para pasar datos binarios en un archivo adjunto WS-I SwaRef, establezca los datos en el `BLOB.swaRef` campo. Esta configuración adjunta los datos a la solicitud SOAP mediante el marco JAX-WS de Java. (Consulte [Invocación de formularios AEM mediante SwaRef](#invoking-aem-forms-using-swaref)).
* **Datos adjuntos** MIME o DIME: Para pasar datos en un archivo adjunto MIME o DIME, adjunte los datos a la solicitud SOAP mediante la API nativa del marco SOAP. Establezca el identificador de datos adjuntos en el `BLOB.attachmentID` campo. (Consulte [Invocación de formularios AEM mediante codificación](#invoking-aem-forms-using-base64-encoding)Base64).
* **Dirección URL** remota: Si los datos están alojados en un servidor web y se puede acceder a ellos a través de una URL HTTP, establezca la URL HTTP en el `BLOB.remoteURL` campo. (Consulte [Invocación de formularios AEM mediante datos BLOB a través de HTTP](#invoking-aem-forms-using-blob-data-over-http)).

**Acceso a datos en objetos BLOB devueltos por servicios**

El protocolo de transmisión de los objetos devueltos `BLOB` depende de varios factores, que se consideran en el siguiente orden, que se detienen cuando se cumple la condición principal:

1. **La dirección URL de destino especifica el protocolo** de transmisión. Si la dirección URL de destino especificada en la invocación SOAP contiene el parámetro `blob="`*BLOB_TYPE *&quot;,* BLOB_TYPE *determina el protocolo de transmisión.* BLOB_TYPE *es un marcador de posición para base64, DIME, Mime, http, Mtom o swaref.
1. **El extremo SOAP de servicio es inteligente**. Si se cumplen las condiciones siguientes, los documentos de salida se devuelven utilizando el mismo protocolo de transmisión que los documentos de entrada:

   * El parámetro de extremo SOAP del servicio Protocolo predeterminado para objetos de blob de salida se establece en Smart.

      Para cada servicio con un extremo SOAP, la consola de administración permite especificar el protocolo de transmisión para cualquier blobs devuelto. (Consulte la ayuda [de](https://www.adobe.com/go/learn_aemforms_admin_63)administración).

   * El servicio AEM Forms toma uno o varios documentos como entrada.

1. **El extremo SOAP de servicio no es inteligente**. El protocolo configurado determina el protocolo de transmisión del documento y los datos se devuelven en el `BLOB` campo correspondiente. Por ejemplo, si el punto final de SOAP está establecido en DIME, el botón devuelto estará en el `blob.attachmentID` campo independientemente del protocolo de transmisión de cualquier documento de entrada.
1. **De lo contrario**. Si un servicio no toma el tipo de documento como entrada, los documentos de salida se devuelven en el `BLOB.remoteURL` campo sobre el protocolo HTTP.

Como se describe en la primera condición, puede garantizar el tipo de transmisión de cualquier documento devuelto extendiendo la dirección URL del extremo SOAP con un sufijo como se indica a continuación:

```as3
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

Esta es la correlación entre los tipos de transmisión y el campo desde el cual se obtienen los datos:

* **Formato** Base64: Configure el `blob` sufijo para que `base64` devuelva los datos en el `BLOB.binaryData` campo.
* **Datos adjuntos** MIME o DIME: Establezca el `blob` sufijo en `DIME` o `MIME` para devolver los datos como un tipo de datos adjuntos correspondiente con el identificador de datos adjuntos devuelto en el `BLOB.attachmentID` campo. Utilice la API patentada del marco SOAP para leer los datos del archivo adjunto.
* **Dirección URL** remota: Establezca el `blob` sufijo para `http` mantener los datos en el servidor de aplicaciones y devolver la URL que apunta a los datos del `BLOB.remoteURL` campo.
* **MTOM o SwaRef**: Establezca el `blob` sufijo en `mtom` o `swaref` para devolver los datos como un tipo de datos adjuntos correspondiente con el identificador de datos adjuntos devuelto en los `BLOB.MTOM` campos o `BLOB.swaRef` . Utilice la API nativa del marco SOAP para leer los datos del archivo adjunto.

>[!NOTE]
>
>Se recomienda no superar los 30 MB al rellenar un `BLOB` objeto invocando su `setBinaryData` método. De lo contrario, existe la posibilidad de que se produzca una `OutOfMemory` excepción.

>[!NOTE]
>
>Las aplicaciones basadas en JAX WS que utilizan el protocolo de transmisión MTOM están limitadas a 25 MB de datos enviados y recibidos. Esta limitación se debe a un error en JAX-WS. Si el tamaño combinado de los archivos enviados y recibidos supera los 25 MB, utilice el protocolo de transmisión SwaRef en lugar del MTOM. De lo contrario, existe la posibilidad de una excepción `OutOfMemory`*.*

**Transmisión MTOM de matrices de bytes con codificación base64**

Además del `BLOB` objeto, el protocolo MTOM admite cualquier parámetro de matriz de bytes o campo de matriz de bytes de un tipo complejo. Esto significa que los marcos SOAP de cliente que admiten MTOM pueden enviar cualquier `xsd:base64Binary` elemento como datos adjuntos MTOM (en lugar de un texto con codificación base64). Los extremos SOAP de AEM Forms pueden leer este tipo de codificación de matriz de bytes. Sin embargo, el servicio AEM Forms siempre devuelve un tipo de matriz de bytes como texto codificado en base64. Los parámetros de matriz de bytes de salida no admiten MTOM.

Los servicios de AEM Forms que devuelven una gran cantidad de datos binarios utilizan el tipo Documento/BLOB en lugar del tipo de matriz de bytes. El tipo de documento es mucho más eficaz para transmitir grandes cantidades de datos.

## Tipos de datos del servicio Web {#web-service-data-types}

La siguiente tabla enumera los tipos de datos Java y muestra el tipo de datos de servicio Web correspondiente.

<table>
 <thead>
  <tr>
   <th><p>Tipo de datos Java</p></th>
   <th><p>Tipo de datos del servicio Web</p></th>
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
   <td><p>El <code>DATE</code> tipo, que se define en un WSDL de servicio de la siguiente manera:</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Si una operación de servicio de AEM Forms toma un <code>java.util.Date</code> valor como entrada, la aplicación cliente SOAP debe pasar la fecha en el <code>DATE.date</code> campo. Si se establece el <code>DATE.calendar</code> campo en este caso, se produce una excepción de tiempo de ejecución. Si el servicio devuelve un valor <code>java.util.Date</code>, la fecha se devuelve en el <code>DATE.date</code> campo.</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p>El <code>DATE</code> tipo, que se define en un WSDL de servicio de la siguiente manera:</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Si una operación de servicio de AEM Forms toma un <code>java.util.Calendar</code> valor como entrada, la aplicación cliente SOAP debe pasar la fecha en el <code>DATE.caledendar</code> campo. Si se establece el <code>DATE.date</code> campo en este caso, se produce una excepción en tiempo de ejecución. Si el servicio devuelve un <code>java.util.Calendar</code>, la fecha se devuelve en el <code>DATE.calendar</code> campo. </p></td>
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
   <td><p>El <code>apachesoap:Map</code>, que se define en un WSDL de servicio de la siguiente manera:</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>El mapa se representa como una secuencia de pares clave/valor.</p></td>
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
   <td><p>El tipo XML, que se define en un WSDL de servicio de la siguiente manera:</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Si una operación de servicio de AEM Forms acepta un <code>org.w3c.dom.Document</code> valor, pase los datos XML en el <code>XML.document</code> campo.</p><p>La configuración del <code>XML.element</code> campo provoca una excepción de tiempo de ejecución. Si el servicio devuelve un <code>org.w3c.dom.Document</code>, los datos XML se devuelven en el <code>XML.document</code> campo.</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>El tipo XML, que se define en un WSDL de servicio de la siguiente manera:</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Si una operación de servicio de AEM Forms realiza una operación <code>org.w3c.dom.Element</code> como entrada, pase los datos XML en el <code>XML.element</code> campo.</p><p>La configuración del <code>XML.document</code> campo provoca una excepción de tiempo de ejecución. Si el servicio devuelve un <code>org.w3c.dom.Element</code>, los datos XML se devuelven en el <code>XML.element</code> campo.</p></td>
  </tr>
 </tbody>
</table>

**Sitio web de Adobe Developer**

El sitio web de desarrolladores de Adobe contiene el siguiente artículo que explica cómo invocar los servicios de AEM Forms mediante la API de servicio web:

[Creación de formularios que procesan aplicaciones ASP.NET](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)

[Invocación de servicios Web mediante componentes personalizados](https://www.adobe.com/devnet/livecycle/articles/extend_webservices.html)

>[!NOTE]
>
>Al invocar servicios web mediante componentes personalizados, se describe cómo crear un componente de AEM Forms que invoque servicios web de terceros.

## Creación de clases proxy de Java mediante JAX-WS {#creating-java-proxy-classes-using-jax-ws}

Puede utilizar JAX-WS para convertir un servicio de Forms WSDL a clases proxy de Java. Estas clases le permiten invocar operaciones de servicios de AEM Forms. Apache Ant le permite crear una secuencia de comandos de compilación que genere clases proxy de Java haciendo referencia a un WSDL de servicio de AEM Forms. Puede generar archivos proxy JAX-WS siguiendo estos pasos:

1. Instale Apache Ant en el equipo cliente. (Consulte [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi)).

   * Agregue el directorio bin a la ruta de clases.
   * Configure la variable de `ANT_HOME` entorno en el directorio donde instaló Ant.

1. Instale JDK 1.6 o posterior.

   * Agregue el directorio bin JDK a la ruta de clases.
   * Agregue el directorio bin JRE a la ruta de clases. Esta bandeja se encuentra en el directorio [*JDK_INSTALL_LOCATION*]/jre.
   * Configure la variable de entorno en el directorio donde instaló el JDK. `JAVA_HOME`
   JDK 1.6 incluye el programa wsimport utilizado en el archivo build.xml. El JDK 1.5 no incluye ese programa.

1. Instale JAX-WS en el equipo cliente. (Consulte API de [Java para servicios](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html)Web XML).
1. Utilice JAX-WS y Apache Ant para generar clases proxy de Java. Cree una secuencia de comandos de creación de hormigas para realizar esta tarea. La siguiente secuencia de comandos es una secuencia de comandos de compilación de Ant de muestra denominada build.xml:

   ```as3
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

   En esta secuencia de comandos de compilación de Ant, observe que la `url` propiedad está establecida para hacer referencia al WSDL del servicio de cifrado que se ejecuta en localhost. Las propiedades `username` y `password` deben establecerse en un nombre de usuario y una contraseña de formularios AEM válidos. Observe que la dirección URL contiene el `lc_version` atributo. Sin especificar la `lc_version` opción, no puede invocar nuevas operaciones de servicio de AEM Forms.

   >[!NOTE]
   >
   >Reemplazar `EncryptionService`por el nombre de servicio de AEM Forms que desea invocar mediante clases proxy de Java. Por ejemplo, para crear clases proxy de Java para el servicio Rights Management, especifique:

   ```as3
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. Cree un archivo BAT para ejecutar la secuencia de comandos de compilación de Ant. El siguiente comando se encuentra dentro de un archivo BAT responsable de ejecutar la secuencia de comandos de compilación de Ant:

   ```as3
    ant -buildfile "build.xml" wsdl
   ```

   Coloque el script de compilación ANT en el directorio C:\Program Files\Java\jaxws-ri\bin directory. El script escribe los archivos JAVA en el .carpeta /classes. La secuencia de comandos genera archivos JAVA que pueden invocar el servicio.

1. Empaquete los archivos JAVA en un archivo JAR. Si está trabajando en Eclipse, siga estos pasos:

   * Cree un nuevo proyecto Java que se utilice para empaquetar los archivos JAVA proxy en un archivo JAR.
   * Cree una carpeta de origen en el proyecto.
   * Cree un `com.adobe.idp.services` paquete en la carpeta Origen.
   * Seleccione el `com.adobe.idp.services` paquete y, a continuación, importe los archivos JAVA de la carpeta adobe/idp/services en el paquete.
   * Si es necesario, cree un `org/apache/xml/xmlsoap` paquete en la carpeta Origen.
   * Seleccione la carpeta de origen y, a continuación, importe los archivos JAVA desde la carpeta org/apache/xml/xmlsoap.
   * Establezca el nivel de cumplimiento del compilador Java en 5.0 o superior.
   * Cree el proyecto.
   * Exporte el proyecto como archivo JAR.
   * Importe este archivo JAR en la ruta de clases de un proyecto cliente. Además, importe todos los archivos JAR ubicados en &lt;Directorio de instalación>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty.
   >[!NOTE]
   >
   >Todos los inicios rápidos del servicio web Java (excepto el servicio Forms) ubicados en Programación con formularios AEM crean archivos proxy de Java con JAX-WS. Además, todos los inicios rápidos del servicio web de Java utilizan SwaRef. (Consulte [Invocación de formularios AEM mediante SwaRef](#invoking-aem-forms-using-swaref)).

**Consulte también**

[Creación de clases proxy de Java mediante el eje Apache](#creating-java-proxy-classes-using-apache-axis)

[Invocación de formularios AEM con codificación Base64](#invoking-aem-forms-using-base64-encoding)

[Invocación de AEM Forms mediante datos BLOB a través de HTTP](#invoking-aem-forms-using-blob-data-over-http)

[Invocación de formularios AEM mediante SwaRef](#invoking-aem-forms-using-swaref)

## Creación de clases proxy de Java mediante el eje Apache {#creating-java-proxy-classes-using-apache-axis}

Puede utilizar la herramienta Java WSDL2Java del eje Apache para convertir un servicio Forms en clases proxy de Java. Estas clases permiten invocar operaciones de servicio de Forms. Con Apache Ant, puede generar archivos de biblioteca del eje a partir de un WSDL de servicio. Puede descargar Apache Axis en la dirección URL [https://ws.apache.org/axis/](https://ws.apache.org/axis/).

>[!NOTE]
>
>El servicio web rápido se inicia asociado con el servicio Forms mediante clases proxy de Java creadas con el eje Apache. El servicio web Forms rápido también utiliza Base64 como tipo de codificación. (Consulte Inicio [rápido de la API de](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)Forms Service).

Puede generar archivos de biblioteca de Java del eje siguiendo estos pasos:

1. Instale Apache Ant en el equipo cliente. Está disponible en [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).

   * Agregue el directorio bin a la ruta de clases.
   * Configure la variable de `ANT_HOME` entorno en el directorio donde instaló Ant.

1. Instale Apache Axis 1.4 en el equipo cliente. Está disponible en [https://ws.apache.org/axis/](https://ws.apache.org/axis/.md).
1. Configure la ruta de clases para utilizar los archivos JAR del eje en el cliente de servicios web, tal como se describe en las instrucciones de instalación del eje en [https://ws.apache.org/axis/java/install.html](https://ws.apache.org/axis/java/install.html).
1. Utilice la herramienta Apache WSDL2Java en Axis para generar clases proxy de Java. Cree una secuencia de comandos de creación de hormigas para realizar esta tarea. La siguiente secuencia de comandos es una secuencia de comandos de compilación de Ant de muestra denominada build.xml:

   ```as3
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

   En esta secuencia de comandos de compilación de Ant, observe que la `url` propiedad está establecida para hacer referencia al WSDL del servicio de cifrado que se ejecuta en localhost. Las propiedades `username` y `password` deben establecerse en un nombre de usuario y una contraseña de formularios AEM válidos.

1. Cree un archivo BAT para ejecutar la secuencia de comandos de compilación de Ant. El siguiente comando se encuentra dentro de un archivo BAT responsable de ejecutar la secuencia de comandos de compilación de Ant:

   ```as3
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   Los archivos JAVA se escriben en la propiedad C:\JavaFiles folder as specified by the `output` . Para invocar correctamente el servicio Forms, importe estos archivos JAVA en la ruta de clases.

   De forma predeterminada, estos archivos pertenecen a un paquete Java denominado `com.adobe.idp.services`. Se recomienda colocar estos archivos JAVA en un archivo JAR. A continuación, importe el archivo JAR en la ruta de clases de la aplicación cliente.

   >[!NOTE]
   >
   >Existen diferentes maneras de colocar archivos .JAVA en un JAR. Una forma es utilizar un IDE de Java como Eclipse. Cree un proyecto Java y un `com.adobe.idp.services`paquete (todos los archivos .JAVA pertenecen a este paquete). A continuación, importe todos los archivos .JAVA en el paquete. Por último, exporte el proyecto como archivo JAR.

1. Modifique la dirección URL en la `EncryptionServiceLocator` clase para especificar el tipo de codificación. Por ejemplo, para utilizar base64, especifique `?blob=base64` para asegurarse de que el `BLOB` objeto devuelve datos binarios. Es decir, en la `EncryptionServiceLocator` clase, busque la siguiente línea de código:

   ```as3
    http://localhost:8080/soap/services/EncryptionService;
   ```

   y cambiarlo a:

   ```as3
    http://localhost:8080/soap/services/EncryptionService?blob=base64;
   ```

1. Agregue los siguientes archivos JAR de eje a la ruta de clases del proyecto Java:

   * activation.jar
   * axis.jar
   * commons-codec-1.3.jar
   * commons-collection-3.1.jar
   * commons-discover.jar
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
   Estos archivos JAR se encuentran en el directorio *[de instalación]*/Adobe/Adobe Experience Manager Forms/sdk/lib/thirdparty.

**Consulte también**

[Creación de clases proxy de Java mediante JAX-WS](#creating-java-proxy-classes-using-jax-ws)

[Invocación de formularios AEM con codificación Base64](#invoking-aem-forms-using-base64-encoding)

[Invocación de AEM Forms mediante datos BLOB a través de HTTP](#invoking-aem-forms-using-blob-data-over-http)

## Invocación de formularios AEM con codificación Base64 {#invoking-aem-forms-using-base64-encoding}

Puede invocar un servicio de AEM Forms mediante la codificación Base64. La codificación Base64 codifica los datos adjuntos que se envían con una solicitud de invocación de servicio Web. Es decir, `BLOB` los datos están codificados en Base64, no en todo el mensaje SOAP.

&quot;Invocación de formularios AEM con codificación Base64&quot; explica cómo invocar el siguiente proceso breve de formularios AEM Forms denominado `MyApplication/EncryptDocument` mediante la codificación Base64.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para seguir el ejemplo de código, cree un proceso denominado `MyApplication/EncryptDocument` mediante Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento PDF no seguro que se pasa al proceso. Esta acción se basa en la `SetValue` operación. El parámetro de entrada para este proceso es una variable de `document` proceso denominada `inDoc`.
1. Codifica el documento PDF con una contraseña. Esta acción se basa en la `PasswordEncryptPDF` operación. El documento PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

### Creación de un ensamblado de cliente .NET que utilice codificación Base64 {#creating-a-net-client-assembly-that-uses-base64-encoding}

Puede crear un ensamblado de cliente .NET para invocar un servicio Forms desde un proyecto .NET de Microsoft Visual Studio. Para crear un ensamblado de cliente .NET que utilice codificación base64, lleve a cabo los siguientes pasos:

1. Cree una clase proxy basada en una URL de invocación de AEM Forms.
1. Cree un proyecto de Microsoft Visual Studio .NET que genere el ensamblado de cliente .NET.

**Creación de una clase proxy**

Puede crear una clase proxy que se utilice para crear el ensamblado de cliente .NET mediante una herramienta que acompañe a Microsoft Visual Studio. El nombre de la herramienta es wsdl.exe y se encuentra en la carpeta de instalación de Microsoft Visual Studio. Para crear una clase proxy, abra el símbolo del sistema y navegue a la carpeta que contiene el archivo wsdl.exe. Para obtener más información sobre la herramienta wsdl.exe, consulte la Ayuda de *MSDN*.

Introduzca el siguiente comando en el símbolo del sistema:

```as3
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

De forma predeterminada, esta herramienta crea un archivo CS en la misma carpeta que se basa en el nombre del WSDL. En este caso, crea un archivo CS denominado *EncryptDocumentService.cs*. Utilice este archivo CS para crear un objeto proxy que le permita invocar el servicio especificado en la URL de invocación.

Modifique la dirección URL en la clase proxy para que se incluya `?blob=base64` a fin de asegurarse de que el `BLOB` objeto devuelve datos binarios. En la clase proxy, busque la siguiente línea de código:

```as3
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

y cambiarlo a:

```as3
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

La sección *Invocación de formularios AEM mediante codificación* Base64 utiliza `MyApplication/EncryptDocument` como ejemplo. Si va a crear un ensamblado de cliente .NET para otro servicio de Forms, asegúrese de reemplazar `MyApplication/EncryptDocument` por el nombre del servicio.

**Desarrollo del ensamblado de cliente .NET**

Cree un proyecto de la biblioteca de clases de Visual Studio que genere un ensamblado de cliente .NET. El archivo CS que ha creado con wsdl.exe se puede importar en este proyecto. Este proyecto produce un archivo DLL (el ensamblado de cliente .NET) que puede utilizar en otros proyectos de Visual Studio .NET para invocar un servicio.

1. Inicie Microsoft Visual Studio .NET.
1. Cree un proyecto de la biblioteca de clases y asígnele el nombre DocumentService.
1. Importe el archivo CS que ha creado mediante wsdl.exe.
1. En el menú **Proyecto** , seleccione **Agregar referencia**.
1. En el cuadro de diálogo Agregar referencia, seleccione **System.Web.Services.dll**.
1. Click **Select** and then click **OK**.
1. Compile y construya el proyecto.

>[!NOTE]
>
>Este procedimiento crea un ensamblado de cliente .NET denominado DocumentService.dll que puede utilizar para enviar solicitudes SOAP al `MyApplication/EncryptDocument` servicio.

>[!NOTE]
>
>Asegúrese de agregar `?blob=base64` a la dirección URL en la clase proxy que se utiliza para crear el ensamblado de cliente .NET. De lo contrario, no se pueden recuperar datos binarios del `BLOB` objeto.

**Referencia al ensamblado de cliente .NET**

Coloque el ensamblado de cliente .NET recién creado en el equipo en el que está desarrollando la aplicación cliente. Después de colocar el ensamblado de cliente .NET en un directorio, puede hacer referencia a él desde un proyecto. También haga referencia a la `System.Web.Services` biblioteca del proyecto. Si no hace referencia a esta biblioteca, no puede utilizar el ensamblado de cliente .NET para invocar un servicio.

1. En el menú **Proyecto** , seleccione **Agregar referencia**.
1. Click the **.NET** tab.
1. Haga clic en **Examinar** y busque el archivo DocumentService.dll.
1. Click **Select** and then click **OK**.

**Invocación de un servicio mediante un ensamblado de cliente .NET que utiliza codificación Base64**

Puede invocar el `MyApplication/EncryptDocument` servicio (que se creó en Workbench) mediante un ensamblado de cliente .NET que utilice la codificación Base64. Para invocar el `MyApplication/EncryptDocument` servicio, lleve a cabo los siguientes pasos:

1. Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL del `MyApplication/EncryptDocument` servicio.
1. Cree un proyecto cliente de Microsoft .NET. Haga referencia al ensamblado de cliente de Microsoft .NET en el proyecto de cliente. También referencia `System.Web.Services`.
1. Mediante el ensamblado de cliente de Microsoft .NET, cree un `MyApplication_EncryptDocumentService` objeto invocando su constructor predeterminado.
1. Defina la `MyApplication_EncryptDocumentService` propiedad del `Credentials` objeto con un `System.Net.NetworkCredential` objeto. En el `System.Net.NetworkCredential` constructor, especifique un nombre de usuario de formularios AEM y la contraseña correspondiente. Defina los valores de autenticación para permitir que la aplicación cliente .NET pueda intercambiar correctamente mensajes SOAP con AEM Forms.
1. Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento PDF que se pasa al `MyApplication/EncryptDocument` proceso.
1. Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
1. Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
1. Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
1. Rellene el `BLOB` objeto asignando su `binaryData` propiedad con el contenido de la matriz de bytes.
1. Invoque el `MyApplication/EncryptDocument` proceso invocando el `MyApplication_EncryptDocumentService` método del `invoke` objeto y pasando el `BLOB` objeto que contiene el documento PDF. Este proceso devuelve un documento PDF cifrado dentro de un `BLOB` objeto.
1. Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento cifrado con contraseña.
1. Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `MyApplicationEncryptDocumentService` método `invoke` del objeto. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `binaryData` objeto.
1. Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
1. Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

### Invocación de un servicio mediante clases proxy Java y codificación Base64 {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}

Puede invocar un servicio de AEM Forms mediante clases proxy de Java y Base64. Para invocar el `MyApplication/EncryptDocument` servicio mediante clases proxy de Java, lleve a cabo los siguientes pasos:

1. Cree clases proxy de Java mediante JAX-WS que consuma el WSDL del `MyApplication/EncryptDocument` servicio. Utilice el siguiente extremo WSDL:

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >Reemplazar `hiro-xp`por la dirección IP del servidor de aplicaciones J2EE que aloja AEM Forms.

1. Empaquete las clases proxy de Java creadas con JAX-WS en un archivo JAR.
1. Incluya el archivo JAR de proxy Java y los archivos JAR ubicados en la siguiente ruta:

   &lt;Directorio de instalación>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   en la ruta de clases del proyecto de cliente Java.

1. Cree un `MyApplicationEncryptDocumentService` objeto con su constructor.
1. Cree un `MyApplicationEncryptDocument` objeto invocando el `MyApplicationEncryptDocumentService` método `getEncryptDocument` del objeto.
1. Defina los valores de conexión necesarios para invocar AEM Forms asignando valores a los siguientes miembros de datos:

   * Asigne el extremo WSDL y el tipo de codificación al `javax.xml.ws.BindingProvider` campo del `ENDPOINT_ADDRESS_PROPERTY` objeto. Para invocar el `MyApplication/EncryptDocument` servicio con codificación Base64, especifique el siguiente valor de URL:

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * Asigne el usuario de formularios AEM al `javax.xml.ws.BindingProvider` campo del `USERNAME_PROPERTY` objeto.
   * Asigne el valor de contraseña correspondiente al `javax.xml.ws.BindingProvider` campo del `PASSWORD_PROPERTY` objeto.
   El siguiente ejemplo de código muestra esta lógica de aplicación:

   ```as3
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Recupere el documento PDF para enviarlo al `MyApplication/EncryptDocument` proceso creando un `java.io.FileInputStream` objeto mediante su constructor. Pase un valor de cadena que especifique la ubicación del documento PDF.
1. Cree una matriz de bytes y rellénela con el contenido del `java.io.FileInputStream` objeto.
1. Cree un `BLOB` objeto con su constructor.
1. Rellene el `BLOB` objeto invocando su `setBinaryData` método y pasando la matriz de bytes. El objeto `BLOB` s `setBinaryData` es el método al que se llama cuando se utiliza la codificación Base64. Consulte Suministro de objetos BLOB en solicitudes de servicio.
1. Invocar el `MyApplication/EncryptDocument` proceso invocando el `MyApplicationEncryptDocument` método `invoke` del objeto. Pase el `BLOB` objeto que contiene el documento PDF. El método invoke devuelve un `BLOB` objeto que contiene el documento PDF codificado.
1. Cree una matriz de bytes que contenga el documento PDF codificado invocando el `BLOB` método `getBinaryData` del objeto.
1. Guarde el documento PDF codificado como archivo PDF. Escriba la matriz de bytes en un archivo.

**Consulte también**

[Inicio rápido: Invocación de un servicio mediante archivos proxy Java y codificación Base64](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[Creación de un ensamblado de cliente .NET que utilice codificación Base64](#creating-a-net-client-assembly-that-uses-base64-encoding)

## Invocación de formularios AEM mediante MTOM {#invoking-aem-forms-using-mtom}

Puede invocar los servicios de AEM Forms mediante el uso de MTOM estándar de servicio web. Este estándar define cómo se transmiten los datos binarios, como un documento PDF, a través de Internet o de la intranet. Una característica de MTOM es el uso del `XOP:Include` elemento . Este elemento se define en la especificación XML Binary Optimized Packaging (XOP) para hacer referencia a los archivos adjuntos binarios de un mensaje SOAP.

El análisis que se realiza aquí consiste en utilizar MTOM para invocar el siguiente proceso de corta duración de AEM Forms denominado `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para seguir el ejemplo de código, cree un proceso denominado `MyApplication/EncryptDocument` mediante Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento PDF no seguro que se pasa al proceso. Esta acción se basa en la `SetValue` operación. El parámetro de entrada para este proceso es una variable de `document` proceso denominada `inDoc`.
1. Codifica el documento PDF con una contraseña. Esta acción se basa en la `PasswordEncryptPDF` operación. El documento PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

>[!NOTE]
>
>Se agregó compatibilidad con MTOM en AEM Forms, versión 9.

>[!NOTE]
>
>Las aplicaciones basadas en JAX WS que utilizan el protocolo de transmisión MTOM están limitadas a 25 MB de datos enviados y recibidos. Esta limitación se debe a un error en JAX-WS. Si el tamaño combinado de los archivos enviados y recibidos supera los 25 MB, utilice el protocolo de transmisión SwaRef en lugar del MTOM. De lo contrario, existe la posibilidad de una `OutOfMemory` excepción.

El análisis aquí trata sobre el uso de MTOM dentro de un proyecto de Microsoft .NET para invocar los servicios de AEM Forms. .NET framework utilizado es 3.5 y el entorno de desarrollo es Visual Studio 2008. Si tiene instaladas mejoras en el servicio Web (WSE) en el equipo de desarrollo, elimínelo. El marco de trabajo de .NET 3.5 admite un marco de trabajo SOAP denominado Windows Communication Foundation (WCF). Al invocar formularios AEM mediante MTOM, solo se admite WCF (no WSE).

### Creación de un proyecto de .NET que invoque un servicio mediante MTOM {#creating-a-net-project-that-invokes-a-service-using-mtom}

Puede crear un proyecto de Microsoft .NET que pueda invocar un servicio de AEM Forms mediante servicios Web. En primer lugar, cree un proyecto de Microsoft .NET mediante Visual Studio 2008. Para invocar un servicio de AEM Forms, cree una referencia de servicio al servicio de AEM Forms que desee invocar en el proyecto. Cuando cree una referencia de servicio, especifique una URL para el servicio de AEM Forms:

```as3
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

Reemplazar `localhost` por la dirección IP del servidor de aplicaciones J2EE que aloja AEM Forms. Reemplazar `MyApplication/EncryptDocument` por el nombre del servicio de AEM Forms que se va a invocar. Por ejemplo, para invocar una operación de Rights Management, especifique:

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

La `lc_version` opción garantiza que la funcionalidad de AEM Forms, como MTOM, esté disponible. Sin especificar la `lc_version` opción, no puede invocar AEM Forms mediante MTOM.

Después de crear una referencia de servicio, los tipos de datos asociados con el servicio AEM Forms están disponibles para su uso en el proyecto .NET. Para crear un proyecto de .NET que invoque un servicio de AEM Forms, lleve a cabo los siguientes pasos:

1. Cree un proyecto .NET con Microsoft Visual Studio 2008.
1. En el menú **Proyecto** , seleccione **Agregar referencia** de servicio.
1. En el cuadro de diálogo **Dirección** , especifique el WSDL en el servicio de AEM Forms. Por ejemplo,

   ```as3
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. Click **Go** and then click **OK**.

###  Invocación de un servicio mediante MTOM en un proyecto .NET {#invoking-a-service-using-mtom-in-a-net-project}

Considere el `MyApplication/EncryptDocument` proceso que acepta un documento PDF no seguro y devuelve un documento PDF con contraseña cifrada. Para invocar el `MyApplication/EncryptDocument` proceso (que se generó en Workbench) mediante MTOM, lleve a cabo los siguientes pasos:

1. Crear un proyecto de Microsoft .NET.
1. Cree un `MyApplication_EncryptDocumentClient` objeto utilizando su constructor predeterminado.
1. Cree un `MyApplication_EncryptDocumentClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms y el tipo de codificación:

   ```as3
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, asegúrese de especificar `?blob=mtom`.

   >[!NOTE]
   >
   >Reemplazar `hiro-xp`por la dirección IP del servidor de aplicaciones J2EE que aloja AEM Forms.

1. Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del miembro de `EncryptDocumentClient.Endpoint.Binding` datos. Convierta el valor devuelto a `BasicHttpBinding`.
1. Establezca el miembro de `System.ServiceModel.BasicHttpBinding` datos del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
1. Habilite la autenticación HTTP básica realizando las siguientes tareas:

   * Asigne el nombre de usuario de los formularios AEM al miembro de datos `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`.
   * Asigne el valor de contraseña correspondiente al miembro de datos `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`.
   * Asigne el valor constante `HttpClientCredentialType.Basic` al miembro de datos `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al miembro de datos `BasicHttpBindingSecurity.Security.Mode`.
   El siguiente ejemplo de código muestra estas tareas.

   ```as3
    //Enable BASIC HTTP authentication
    encryptProcess.ClientCredentials.UserName.UserName = "administrator";
    encryptProcess.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 4000000;
    b.MaxBufferSize = 4000000;
    b.ReaderQuotas.MaxArrayLength = 4000000;
   ```

1. Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento PDF que se pasa al `MyApplication/EncryptDocument` proceso.
1. Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
1. Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
1. Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
1. Rellene el `BLOB` objeto asignando su miembro `MTOM` de datos con el contenido de la matriz de bytes.
1. Invocar el `MyApplication/EncryptDocument` proceso invocando el `MyApplication_EncryptDocumentClient` método `invoke` del objeto. Pase el `BLOB` objeto que contiene el documento PDF. Este proceso devuelve un documento PDF cifrado dentro de un `BLOB` objeto.
1. Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF protegido.
1. Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `invoke` método. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
1. Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
1. Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

>[!NOTE]
>
>La mayoría de las operaciones de servicio de AEM Forms tienen un inicio rápido de MTOM. Puede ver estos inicios rápidos en la sección de inicio rápido correspondiente de un servicio. Por ejemplo, para ver la sección Inicio rápido de Output, consulte Inicio rápido de API de [Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**Consulte también**

[Inicio rápido: Invocación de un servicio mediante MTOM en un proyecto .NET](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[Acceso a varios servicios mediante servicios Web](#accessing-multiple-services-using-web-services)

[Creación de una aplicación Web ASP.NET que invoque un proceso prolongado centrado en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## Invocación de formularios AEM mediante SwaRef {#invoking-aem-forms-using-swaref}

Puede invocar los servicios de AEM Forms mediante SwaRef. El contenido del elemento `wsi:swaRef` XML se envía como datos adjuntos dentro de un cuerpo SOAP que almacena la referencia al archivo adjunto. Al invocar un servicio de Forms mediante SwaRef, cree clases proxy de Java mediante la API de Java para servicios Web XML (JAX-WS). (Consulte API de [Java para servicios](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html)Web XML).

La discusión aquí consiste en invocar el siguiente proceso de corta duración de Forms llamado `MyApplication/EncryptDocument` mediante SwaRef.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para seguir el ejemplo de código, cree un proceso denominado `MyApplication/EncryptDocument` mediante Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento PDF no seguro que se pasa al proceso. Esta acción se basa en la `SetValue` operación. El parámetro de entrada para este proceso es una variable de `document` proceso denominada `inDoc`.
1. Codifica el documento PDF con una contraseña. Esta acción se basa en la `PasswordEncryptPDF` operación. El documento PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

>[!NOTE]
>
>Se agregó compatibilidad con SwaRef en AEM Forms

El siguiente análisis trata sobre cómo invocar los servicios de Forms mediante SwaRef en una aplicación cliente Java. La aplicación Java utiliza clases proxy creadas mediante JAX-WS.

### Invocar un servicio mediante archivos de biblioteca JAX-WS que utilizan SwaRef {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}

Para invocar el `MyApplication/EncryptDocument` proceso mediante archivos proxy de Java creados con JAX-WS y SwaRef, lleve a cabo los siguientes pasos:

1. Cree clases proxy de Java mediante JAX-WS que consuma el WSDL del `MyApplication/EncryptDocument` servicio. Utilice el siguiente extremo WSDL:

   ```as3
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   Para obtener más información, consulte [Creación de clases proxy de Java mediante JAX-WS](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >Reemplazar `hiro-xp`* con la dirección IP del servidor de aplicaciones J2EE que aloja AEM Forms. *

1. Empaquete las clases proxy de Java creadas con JAX-WS en un archivo JAR.
1. Incluya el archivo JAR de proxy Java y los archivos JAR ubicados en la siguiente ruta:

   &lt;Directorio de instalación>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   en la ruta de clases del proyecto de cliente Java.

1. Cree un `MyApplicationEncryptDocumentService` objeto con su constructor.
1. Cree un `MyApplicationEncryptDocument` objeto invocando el `MyApplicationEncryptDocumentService` método `getEncryptDocument` del objeto.
1. Defina los valores de conexión necesarios para invocar AEM Forms asignando valores a los siguientes miembros de datos:

   * Asigne el extremo WSDL y el tipo de codificación al `javax.xml.ws.BindingProvider` campo del `ENDPOINT_ADDRESS_PROPERTY` objeto. Para invocar el `MyApplication/EncryptDocument` servicio con codificación SwaRef, especifique el siguiente valor de URL:

      ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * Asigne el usuario de formularios AEM al `javax.xml.ws.BindingProvider` campo del `USERNAME_PROPERTY` objeto.
   * Asigne el valor de contraseña correspondiente al `javax.xml.ws.BindingProvider` campo del `PASSWORD_PROPERTY` objeto.
   El siguiente ejemplo de código muestra esta lógica de aplicación:

   ```as3
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Recupere el documento PDF para enviarlo al `MyApplication/EncryptDocument` proceso creando un `java.io.File` objeto mediante su constructor. Pase un valor de cadena que especifique la ubicación del documento PDF.
1. Cree un `javax.activation.DataSource` objeto mediante el `FileDataSource` constructor. Pase el `java.io.File` objeto.
1. Cree un `javax.activation.DataHandler` objeto utilizando su constructor y pasando el `javax.activation.DataSource` objeto.
1. Cree un `BLOB` objeto con su constructor.
1. Rellene el `BLOB` objeto invocando su `setSwaRef` método y pasando el `javax.activation.DataHandler` objeto.
1. Invoque el `MyApplication/EncryptDocument` proceso invocando el `MyApplicationEncryptDocument` método del `invoke` objeto y pasando el `BLOB` objeto que contiene el documento PDF. El método invoke devuelve un `BLOB` objeto que contiene un documento PDF codificado.
1. Rellene un `javax.activation.DataHandler` objeto invocando el `BLOB` método `getSwaRef` del objeto.
1. Convierta el `javax.activation.DataHandler` objeto en una `java.io.InputSteam` instancia invocando el `javax.activation.DataHandler` método `getInputStream` del objeto.
1. Escriba la `java.io.InputSteam` instancia en un archivo PDF que represente el documento PDF codificado.

>[!NOTE]
>
>La mayoría de las operaciones de servicio de AEM Forms tienen un inicio rápido de SwaRef. Puede ver estos inicios rápidos en la sección de inicio rápido correspondiente de un servicio. Por ejemplo, para ver la sección Inicio rápido de Output, consulte Inicio rápido de API de [Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**Consulte también**

[Inicio rápido: Invocación de un servicio mediante SwaRef en un proyecto de Java](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## Invocación de AEM Forms mediante datos BLOB a través de HTTP {#invoking-aem-forms-using-blob-data-over-http}

Puede invocar los servicios de AEM Forms mediante servicios web y pasando datos BLOB a través de HTTP. Pasar datos BLOB por HTTP es una técnica alternativa en lugar de utilizar codificación base64, DIME o MIME. Por ejemplo, puede pasar datos a través de HTTP en un proyecto de Microsoft .NET que utilice Web Service Enhancement 3.0, que no admite DIME o MIME. Al utilizar datos BLOB a través de HTTP, los datos de entrada se cargan antes de que se invoque el servicio AEM Forms.

&quot;Invocar formularios AEM mediante datos BLOB sobre HTTP&quot; explica cómo invocar el siguiente proceso de corta duración de AEM Forms denominado `MyApplication/EncryptDocument` pasando datos BLOB por HTTP.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para seguir el ejemplo de código, cree un proceso denominado `MyApplication/EncryptDocument` mediante Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento PDF no seguro que se pasa al proceso. Esta acción se basa en la `SetValue` operación. El parámetro de entrada para este proceso es una variable de `document` proceso denominada `inDoc`.
1. Codifica el documento PDF con una contraseña. Esta acción se basa en la `PasswordEncryptPDF` operación. El documento PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

>[!NOTE]
>
>Se recomienda familiarizarse con la invocación de formularios AEM mediante SOAP. (Consulte [Invocación de formularios AEM mediante servicios](#invoking-aem-forms-using-web-services)web).

### Creación de un ensamblado de cliente .NET que utilice datos a través de HTTP {#creating-a-net-client-assembly-that-uses-data-over-http}

Para crear un ensamblado de cliente que utilice datos a través de HTTP, siga el proceso especificado en [Invocación de formularios AEM mediante codificación](#invoking-aem-forms-using-base64-encoding)Base64. Sin embargo, modifique la dirección URL en la clase proxy para incluirla `?blob=http` en lugar de `?blob=base64`. Esta acción garantiza que los datos se pasen por HTTP. En la clase proxy, busque la siguiente línea de código:

```as3
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

y cambiarlo a:

```as3
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**Referencia al ensamblado de .NET clientMyApplication/EncryptDocument**

Coloque el nuevo ensamblado de cliente .NET en el equipo en el que está desarrollando la aplicación cliente. Después de colocar el ensamblado de cliente .NET en un directorio, puede hacer referencia a él desde un proyecto. Haga referencia a la `System.Web.Services` biblioteca del proyecto. Si no hace referencia a esta biblioteca, no puede utilizar el ensamblado de cliente .NET para invocar un servicio.

1. En el menú **Proyecto** , seleccione **Agregar referencia**.
1. Click the **.NET** tab.
1. Haga clic en **Examinar** y busque el archivo DocumentService.dll.
1. Click **Select** and then click **OK**.

**Invocación de un servicio mediante un ensamblado de cliente .NET que utiliza datos BLOB a través de HTTP**

Puede invocar el `MyApplication/EncryptDocument` servicio (que se creó en Workbench) mediante un ensamblado de cliente .NET que utiliza datos a través de HTTP. Para invocar el `MyApplication/EncryptDocument` servicio, lleve a cabo los siguientes pasos:

1. Cree el ensamblado de cliente .NET.
1. Haga referencia al ensamblado de cliente de Microsoft .NET. Cree un proyecto cliente de Microsoft .NET. Haga referencia al ensamblado de cliente de Microsoft .NET en el proyecto de cliente. También referencia `System.Web.Services`.
1. Mediante el ensamblado de cliente de Microsoft .NET, cree un `MyApplication_EncryptDocumentService` objeto invocando su constructor predeterminado.
1. Defina la `MyApplication_EncryptDocumentService` propiedad del `Credentials` objeto con un `System.Net.NetworkCredential` objeto. En el `System.Net.NetworkCredential` constructor, especifique un nombre de usuario de formularios AEM y la contraseña correspondiente. Defina los valores de autenticación para permitir que la aplicación cliente .NET pueda intercambiar correctamente mensajes SOAP con AEM Forms.
1. Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para pasar datos al `MyApplication/EncryptDocument` proceso.
1. Asigne un valor de cadena al miembro de datos del `BLOB` objeto que especifica la ubicación URI de un documento PDF que se pasará al `remoteURL` `MyApplication/EncryptDocument`servicio.
1. Invocar el `MyApplication/EncryptDocument` proceso invocando el `MyApplication_EncryptDocumentService` método del `invoke` objeto y pasando el `BLOB` objeto. Este proceso devuelve un documento PDF cifrado dentro de un `BLOB` objeto.
1. Cree un `System.UriBuilder` objeto utilizando su constructor y pasando el valor del miembro de datos del `BLOB` objeto devuelto `remoteURL` .
1. Convierta el `System.UriBuilder` objeto en un `System.IO.Stream` objeto. (El inicio rápido de C# que sigue a esta lista ilustra cómo realizar esta tarea).
1. Cree una matriz de bytes y rellénela con los datos ubicados en el `System.IO.Stream` objeto.
1. Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
1. Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

### Invocación de un servicio mediante clases proxy Java y datos BLOB a través de HTTP {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}

Puede invocar un servicio de AEM Forms mediante clases proxy de Java y datos BLOB a través de HTTP. Para invocar el `MyApplication/EncryptDocument` servicio mediante clases proxy de Java, lleve a cabo los siguientes pasos:

1. Cree clases proxy de Java mediante JAX-WS que consuma el WSDL del `MyApplication/EncryptDocument` servicio. Utilice el siguiente extremo WSDL:

   ```as3
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   Para obtener más información, consulte [Creación de clases proxy de Java mediante JAX-WS](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >Reemplazar `hiro-xp`* con la dirección IP del servidor de aplicaciones J2EE que aloja AEM Forms. *

1. Empaquete las clases proxy de Java creadas con JAX-WS en un archivo JAR.
1. Incluya el archivo JAR de proxy Java y los archivos JAR ubicados en la siguiente ruta:

   &lt;Directorio de instalación>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   en la ruta de clases del proyecto de cliente Java.

1. Cree un `MyApplicationEncryptDocumentService` objeto con su constructor.
1. Cree un `MyApplicationEncryptDocument` objeto invocando el `MyApplicationEncryptDocumentService` método `getEncryptDocument` del objeto.
1. Defina los valores de conexión necesarios para invocar AEM Forms asignando valores a los siguientes miembros de datos:

   * Asigne el extremo WSDL y el tipo de codificación al `javax.xml.ws.BindingProvider` campo del `ENDPOINT_ADDRESS_PROPERTY` objeto. Para invocar el `MyApplication/EncryptDocument` servicio con codificación BLOB sobre HTTP, especifique el siguiente valor de URL:

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * Asigne el usuario de formularios AEM al `javax.xml.ws.BindingProvider` campo del `USERNAME_PROPERTY` objeto.
   * Asigne el valor de contraseña correspondiente al `javax.xml.ws.BindingProvider` campo del `PASSWORD_PROPERTY` objeto.
   El siguiente ejemplo de código muestra esta lógica de aplicación:

   ```as3
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Cree un `BLOB` objeto con su constructor.
1. Rellene el `BLOB` objeto invocando su `setRemoteURL` método. Pase un valor de cadena que especifique la ubicación URI de un documento PDF para pasarlo al `MyApplication/EncryptDocument` servicio.
1. Invoque el `MyApplication/EncryptDocument` proceso invocando el `MyApplicationEncryptDocument` método del `invoke` objeto y pasando el `BLOB` objeto que contiene el documento PDF. Este proceso devuelve un documento PDF cifrado dentro de un `BLOB` objeto.
1. Cree una matriz de bytes para almacenar la secuencia de datos que representa el documento PDF codificado. Invocar el `BLOB` método del `getRemoteURL` objeto (utilizar el `BLOB` objeto devuelto por el `invoke` método).
1. Cree un `java.io.File` objeto con su constructor. Este objeto representa el documento PDF codificado.
1. Cree un `java.io.FileOutputStream` objeto utilizando su constructor y pasando el `java.io.File` objeto.
1. Invocar el `java.io.FileOutputStream` método del `write` objeto. Pase la matriz de bytes que contiene la secuencia de datos que representa el documento PDF codificado.

## Invocación de formularios AEM mediante DIME {#invoking-aem-forms-using-dime}

Puede invocar los servicios de AEM Forms mediante SOAP con archivos adjuntos. AEM Forms admite los estándares de servicio web MIME y DIME. DIME permite enviar archivos adjuntos binarios, como documentos PDF, junto con solicitudes de invocación en lugar de codificar los datos adjuntos. En la sección *Invocar formularios AEM mediante DIME* se explica cómo invocar el siguiente proceso de corta duración de AEM Forms denominado `MyApplication/EncryptDocument` mediante DIME.

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento PDF no seguro que se pasa al proceso. Esta acción se basa en la `SetValue` operación. El parámetro de entrada para este proceso es una variable de `document` proceso denominada `inDoc`.
1. Codifica el documento PDF con una contraseña. Esta acción se basa en la `PasswordEncryptPDF` operación. El documento PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

Este proceso no se basa en un proceso de AEM Forms existente. Para seguir los ejemplos de código, cree un proceso denominado `MyApplication/EncryptDocument`**mediante Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

>[!NOTE]
>
>La invocación de operaciones de servicio de AEM Forms mediante DIME está en desuso. Se recomienda que utilice MTOM. (Consulte [Invocación de formularios AEM mediante MTOM](#invoking-aem-forms-using-mtom)).

### Creación de un proyecto de .NET que utilice DIME {#creating-a-net-project-that-uses-dime}

Para crear un proyecto de .NET que pueda invocar un servicio de Forms mediante DIME, realice las siguientes tareas:

* Instale las mejoras de servicios Web 2.0 en el equipo de desarrollo.
* Desde el proyecto .NET, cree una referencia web al servicio FormsAEM Forms.

**Instalación de mejoras de servicios Web 2.0**

Instale las mejoras de los servicios Web 2.0 en el equipo de desarrollo e integre la aplicación con Microsoft Visual Studio .NET. Puede descargar las mejoras de servicios Web 2.0 desde el Centro de descargas de [Microsoft.](https://www.microsoft.com/downloads/search.aspx)

En esta página web, busque las mejoras de servicios web 2.0 y descárguela en el equipo de desarrollo. Esta descarga coloca un archivo denominado Microsoft WSE 2.0 SPI.msi en el equipo. Ejecute el programa de instalación y siga las instrucciones en línea.

>[!NOTE]
>
>Las mejoras en los servicios Web 2.0 son compatibles con DIME. La versión admitida de Microsoft Visual Studio es 2003 al trabajar con las mejoras de servicios Web 2.0. Las mejoras en los servicios Web 3.0 no admiten DIME; sin embargo, admite MTOM.

**Creación de una referencia web en un servicio de AEM Forms**

Después de instalar las mejoras de servicios web 2.0 en el equipo de desarrollo y crear un proyecto de Microsoft .NET, cree una referencia web al servicio Forms. Por ejemplo, para crear una referencia web al `MyApplication/EncryptDocument` proceso y suponiendo que Forms está instalado en el equipo local, especifique la siguiente dirección URL:

```as3
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

Después de crear una referencia web, los dos tipos de datos proxy siguientes están disponibles para su uso en el proyecto .NET: `EncryptDocumentService` y `EncryptDocumentServiceWse`. Para invocar el `MyApplication/EncryptDocument` proceso mediante DIME, utilice el `EncryptDocumentServiceWse` tipo .

>[!NOTE]
>
>Antes de crear una referencia web al servicio Forms, asegúrese de hacer referencia a las mejoras de los servicios web 2.0 en el proyecto. (Consulte &quot;Instalación de mejoras de servicios Web 2.0&quot;).

**Referencia a la biblioteca WSE**

1. En el menú Proyecto, seleccione Agregar referencia.
1. En el cuadro de diálogo Agregar referencia, seleccione Microsoft.Web.Services2.dll.
1. Seleccione System.Web.Services.dll.
1. Haga clic en Seleccionar y, a continuación, en Aceptar.

**Creación de una referencia web a un servicio de Forms**

1. En el menú Proyecto, seleccione Agregar referencia web.
1. En el cuadro de diálogo URL, especifique la URL del servicio Forms.
1. Haga clic en Ir y, a continuación, en Agregar referencia.

>[!NOTE]
>
>Asegúrese de activar el proyecto .NET para utilizar la biblioteca WSE. Desde el Explorador de proyectos, haga clic con el botón derecho en el nombre del proyecto y seleccione Activar WSE 2.0. Asegúrese de que la casilla de verificación del cuadro de diálogo que aparece está seleccionada.

**Invocación de un servicio mediante DIME en un proyecto .NET**

Puede invocar un servicio de Forms mediante DIME. Considere el `MyApplication/EncryptDocument` proceso que acepta un documento PDF no seguro y devuelve un documento PDF con contraseña cifrada. Para invocar el `MyApplication/EncryptDocument` proceso mediante DIME, lleve a cabo los siguientes pasos:

1. Cree un proyecto de Microsoft .NET que le permita invocar un servicio de Forms mediante DIME. Asegúrese de incluir las mejoras de los servicios web 2.0 y de crear una referencia web al servicio de AEM Forms.
1. Después de establecer una referencia web al `MyApplication/EncryptDocument` proceso, cree un `EncryptDocumentServiceWse` objeto utilizando su constructor predeterminado.
1. Establezca el miembro de datos del `EncryptDocumentServiceWse` objeto con un valor que especifique el nombre de usuario y el valor de la contraseña de los formularios de AEM `Credentials` `System.Net.NetworkCredential` .
1. Cree un `Microsoft.Web.Services2.Dime.DimeAttachment` objeto con su constructor y pasando los siguientes valores:

   * Un valor de cadena que especifica un valor GUID. Puede obtener un valor GUID invocando el `System.Guid.NewGuid.ToString` método.
   * Un valor de cadena que especifica el tipo de contenido. Dado que este proceso requiere un documento PDF, especifique `application/pdf`.
   * Un valor `TypeFormat` de enumeración. Especifique `TypeFormat.MediaType`.
   * Un valor de cadena que especifica la ubicación del documento PDF que se pasará al proceso de AEM Forms.

1. Cree un `BLOB` objeto con su constructor.
1. Agregue el adjunto DIME al `BLOB` objeto asignando el valor del miembro de datos del `Microsoft.Web.Services2.Dime.DimeAttachment` objeto `Id` al miembro de datos del `BLOB` objeto `attachmentID` .
1. Invoque el `EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add` método y pase el `Microsoft.Web.Services2.Dime.DimeAttachment` objeto.
1. Invoque el `MyApplication/EncryptDocument` proceso invocando el `EncryptDocumentServiceWse` método del `invoke` objeto y pasando el `BLOB` objeto que contiene el adjunto DIME. Este proceso devuelve un documento PDF cifrado dentro de un `BLOB` objeto.
1. Obtenga el valor del identificador de datos adjuntos obteniendo el valor del miembro de datos del `BLOB` objeto `attachmentID` devuelto.
1. Repita los datos adjuntos ubicados en `EncryptDocumentServiceWse.ResponseSoapContext.Attachments` y utilice el valor del identificador de datos adjuntos para obtener el documento PDF codificado.
1. Obtenga un `System.IO.Stream` objeto obteniendo el valor del miembro de datos del `Attachment` objeto `Stream` .
1. Cree una matriz de bytes y pase dicha matriz de bytes al `System.IO.Stream` método `Read` del objeto. Este método rellena la matriz de bytes con un flujo de datos que representa el documento PDF codificado.
1. Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente una ubicación de archivo PDF. Este objeto representa el documento PDF codificado.
1. Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
1. Escriba el contenido de la matriz de bytes en el archivo PDF invocando el `System.IO.BinaryWriter` método del `Write` objeto y pasando la matriz de bytes.

### Creación de clases proxy Java Apache Axis que utilizan DIME {#creating-apache-axis-java-proxy-classes-that-use-dime}

Puede utilizar la herramienta Java WSDL2Eje Apache para convertir un servicio WSDL en clases proxy de Java, de modo que pueda invocar operaciones de servicio. Con Apache Ant, puede generar archivos de biblioteca del eje desde un WSDL del servicio de AEM Forms que le permite invocar el servicio. (Consulte [Creación de clases proxy de Java mediante Apache Axis](#creating-java-proxy-classes-using-apache-axis)).

La herramienta Apache Axis WSDL2Java genera archivos JAVA que contienen métodos que se utilizan para enviar solicitudes SOAP a un servicio. Las solicitudes SOAP recibidas por un servicio son descodificadas por las bibliotecas generadas por el eje y devueltas a los métodos y argumentos.

Para invocar el `MyApplication/EncryptDocument` servicio (que se creó en Workbench) mediante archivos de biblioteca generados por el eje y DIME, lleve a cabo los siguientes pasos:

1. Cree clases proxy de Java que consuman el `MyApplication/EncryptDocument` servicio WSDL mediante Apache Axis. (Consulte [Creación de clases proxy de Java mediante Apache Axis](#creating-java-proxy-classes-using-apache-axis)).
1. Incluya las clases proxy de Java en la ruta de clases.
1. Cree un `MyApplicationEncryptDocumentServiceLocator` objeto con su constructor.
1. Cree un `URL` objeto utilizando su constructor y pasando un valor de cadena que especifica la definición WSDL del servicio de AEM Forms. Asegúrese de especificar `?blob=dime` al final de la dirección URL del extremo SOAP. Por ejemplo, use

   ```as3
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. Cree un `EncryptDocumentSoapBindingStub` objeto invocando su constructor y pasando el `MyApplicationEncryptDocumentServiceLocator`objeto y el `URL` objeto.
1. Establezca el nombre de usuario y el valor de la contraseña de los formularios AEM invocando los métodos `EncryptDocumentSoapBindingStub` y `setUsername` los métodos del `setPassword` objeto.

   ```as3
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. Recupere el documento PDF para enviarlo al `MyApplication/EncryptDocument` servicio creando un `java.io.File` objeto. Pase un valor de cadena que especifique la ubicación del documento PDF.
1. Cree un `javax.activation.DataHandler` objeto utilizando su constructor y pasando un `javax.activation.FileDataSource` objeto. El `javax.activation.FileDataSource` objeto se puede crear utilizando su constructor y pasando el `java.io.File` objeto que representa el documento PDF.
1. Cree un `org.apache.axis.attachments.AttachmentPart` objeto utilizando su constructor y pasando el `javax.activation.DataHandler` objeto.
1. Adjuntar los datos adjuntos invocando el `EncryptDocumentSoapBindingStub` método `addAttachment` del objeto y pasando el `org.apache.axis.attachments.AttachmentPart` objeto.
1. Cree un `BLOB` objeto con su constructor. Rellene el `BLOB` objeto con el valor del identificador de datos adjuntos invocando el método del `BLOB` objeto y pasando el valor del identificador `setAttachmentID` de datos adjuntos. Este valor se puede obtener invocando el `org.apache.axis.attachments.AttachmentPart` método `getContentId` del objeto.
1. Invocar el `MyApplication/EncryptDocument` proceso invocando el `EncryptDocumentSoapBindingStub` método `invoke` del objeto. Pase el `BLOB` objeto que contiene el adjunto DIME. Este proceso devuelve un documento PDF cifrado dentro de un `BLOB` objeto.
1. Obtenga el valor del identificador de datos adjuntos invocando el método del `BLOB` objeto devuelto `getAttachmentID` . Este método devuelve un valor de cadena que representa el valor de identificador del adjunto devuelto.
1. Recupere los datos adjuntos invocando el `EncryptDocumentSoapBindingStub` método `getAttachments` del objeto. Este método devuelve una matriz de `Objects` que representan los archivos adjuntos.
1. Repita los datos adjuntos (la `Object` matriz) y utilice el valor del identificador de datos adjuntos para obtener el documento PDF codificado. Cada elemento es un `org.apache.axis.attachments.AttachmentPart` objeto.
1. Obtenga el `javax.activation.DataHandler` objeto asociado al archivo adjunto invocando el `org.apache.axis.attachments.AttachmentPart` método `getDataHandler` del objeto.
1. Obtenga un `java.io.FileStream` objeto invocando el `javax.activation.DataHandler` método `getInputStream` del objeto.
1. Cree una matriz de bytes y pase dicha matriz de bytes al `java.io.FileStream` método `read` del objeto. Este método rellena la matriz de bytes con un flujo de datos que representa el documento PDF codificado.
1. Cree un `java.io.File` objeto con su constructor. Este objeto representa el documento PDF codificado.
1. Cree un `java.io.FileOutputStream` objeto utilizando su constructor y pasando el `java.io.File` objeto.
1. Invoque el `java.io.FileOutputStream` método del `write` objeto y pase la matriz de bytes que contiene la secuencia de datos que representa el documento PDF codificado.

**Consulte también**

[Inicio rápido: Invocación de un servicio mediante DIME en un proyecto de Java](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## Uso de la autenticación basada en SAML {#using-saml-based-authentication}

AEM Forms admite varios modos de autenticación de servicios web al invocar servicios. Un modo de autenticación es especificar un nombre de usuario y un valor de contraseña mediante un encabezado de autorización básico en la llamada al servicio Web. AEM Forms también admite la autenticación basada en aserciones SAML. Cuando una aplicación cliente invoca un servicio de AEM Forms mediante un servicio Web, la aplicación cliente puede proporcionar información de autenticación de una de las siguientes formas:

* Pasar credenciales como parte de la autorización básica
* Pasar el token de nombre de usuario como parte del encabezado WS-Security
* Paso de una afirmación SAML como parte del encabezado WS-Security
* Paso del token Kerberos como parte del encabezado WS-Security

AEM Forms no admite la autenticación basada en certificados estándar, pero sí la autenticación basada en certificados en un formulario distinto.

>[!NOTE]
>
>El servicio web rápido comienza en Programación con AEM Forms y especifica los valores de nombre de usuario y contraseña para realizar la autorización.

La identidad de los usuarios de formularios AEM se puede representar mediante una afirmación SAML firmada con una clave secreta. El siguiente código XML muestra un ejemplo de una afirmación SAML.

```as3
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

Esta afirmación de ejemplo se emite para un usuario administrador. Esta afirmación contiene los siguientes elementos notables:

* Es válido durante un tiempo determinado.
* Se emite para un usuario en particular.
* Se firma digitalmente. Así que cualquier modificación que se le haga rompería la firma.
* Se puede presentar en AEM Forms como un distintivo de la identidad del usuario similar al nombre de usuario y la contraseña.

Una aplicación cliente puede recuperar la afirmación de cualquier API de AEM Forms AuthenticationManager que devuelva un `AuthResult` objeto. Puede obtener una `AuthResult` instancia mediante uno de los dos métodos siguientes:

* Autentificación del usuario mediante cualquiera de los métodos de autenticación expuestos por la API de AuthenticationManager. Normalmente, se utilizarían el nombre de usuario y la contraseña; sin embargo, también puede utilizar la autenticación de certificado.
* Uso del `AuthenticationManager.getAuthResultOnBehalfOfUser` método. Este método permite que una aplicación cliente obtenga un `AuthResult` objeto para cualquier usuario de formularios AEM.

un usuario de formularios AEM puede autenticarse con un token SAML obtenido. Esta afirmación de SAML (fragmento xml) se puede enviar como parte del encabezado WS-Security con la llamada de servicio web para la autenticación de usuarios. Normalmente, una aplicación cliente ha autenticado a un usuario pero no ha almacenado las credenciales de usuario. (O bien, el usuario ha iniciado sesión en ese cliente mediante un mecanismo que no sea el uso de un nombre de usuario y una contraseña). En este caso, la aplicación cliente tiene que invocar AEM Forms y suplantar a un usuario específico que puede invocar AEM Forms.

Para suplantar a un usuario específico, invoque el `AuthenticationManager.getAuthResultOnBehalfOfUser` método mediante un servicio Web. Este método devuelve una `AuthResult` instancia que contiene la afirmación SAML para ese usuario.

A continuación, utilice esa afirmación de SAML para invocar cualquier servicio que requiera autenticación. Esta acción implica enviar la afirmación como parte del encabezado SOAP. Cuando se realiza una llamada de servicio web con esta afirmación, AEM Forms identifica al usuario como el representado por esa afirmación. Es decir, el usuario especificado en la afirmación es el usuario que invoca el servicio.

### Uso de clases Apache Axis y autenticación basada en SAML {#using-apache-axis-classes-and-saml-based-authentication}

Puede invocar un servicio de AEM Forms mediante clases proxy de Java que se crearon con la biblioteca Axis. (Consulte [Creación de clases proxy de Java mediante Apache Axis](#creating-java-proxy-classes-using-apache-axis)).

Cuando utilice AXIS que utilice autenticación basada en SAML, registre la solicitud y el controlador de respuesta con Axis. Apache Axis invoca al controlador antes de enviar una solicitud de invocación a AEM Forms. Para registrar un controlador, cree una clase Java que se extienda `org.apache.axis.handlers.BasicHandler`.

**Creación de un controlador de aserción con eje**

La siguiente clase Java, denominada `AssertionHandler.java`, muestra un ejemplo de una clase Java que se extiende `org.apache.axis.handlers.BasicHandler`.

```as3
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

```as3
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

```as3
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

Puede invocar un servicio Forms mediante un ensamblado de cliente .NET y una autenticación basada en SAML. Para ello, debe utilizar las mejoras del servicio Web 3.0 (WSE). Para obtener información sobre la creación de un ensamblado de cliente .NET que utilice WSE, consulte [Creación de un proyecto .NET que utilice DIME](#creating-a-net-project-that-uses-dime).

>[!NOTE]
>
>La sección DIME utiliza WSE 2.0. Para utilizar la autenticación basada en SAML, siga las mismas instrucciones especificadas en el tema DIME. Sin embargo, sustituya WSE 2.0 por WSE 3.0. Instale las mejoras de los servicios Web 3.0 en el equipo de desarrollo e integre la aplicación con Microsoft Visual Studio .NET. Puede descargar las mejoras de servicios Web 3.0 desde el Centro [de descargas de](https://www.microsoft.com/downloads/search.aspx)Microsoft.

La arquitectura WSE utiliza los tipos de datos Directivas, Aserciones y SecurityToken. Brevemente, para una llamada de servicio Web, especifique una política. Una política puede tener varias aserciones. Cada afirmación puede contener filtros. Un filtro se invoca en determinadas etapas de una llamada de servicio Web y, en ese momento, puede modificar la solicitud SOAP. Para obtener más información, consulte la documentación sobre las mejoras del servicio Web 3.0.

**Crear la aserción y el filtro**

El siguiente ejemplo de código C# crea clases de filtro y afirmación. En este ejemplo de código se crea un SamlAssertionOutputFilter. El marco de trabajo de WSE invoca este filtro antes de que la solicitud SOAP se envíe a AEM Forms.

```as3
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

**Crear el autentificador SAML**

Cree una clase para representar la afirmación SAML. La tarea principal que realiza esta clase es convertir valores de datos de cadena a xml y conservar espacio en blanco. Este xml de afirmación se importa posteriormente en la solicitud SOAP.

```as3
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

El siguiente ejemplo de código C# invoca un servicio Forms mediante la autenticación basada en SAML.

```as3
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

## Consideraciones relacionadas al utilizar servicios Web {#related-considerations-when-using-web-services}

A veces se producen problemas al invocar determinadas operaciones de servicios de AEM Forms mediante servicios Web. El objetivo de este debate es determinar esas cuestiones y proporcionar una solución, si se dispone de una.

### Invocación de operaciones de servicio asincrónica {#invoking-service-operations-asynchronously}

Si intenta invocar de forma asíncrona una operación de servicio de AEM Forms, como la operación Generar archivo PDF, `htmlToPDF` se `SoapFaultException` producirá un error. Para resolver este problema, cree un archivo XML de enlace personalizado que asigne el `ExportPDF_Result` elemento y otros elementos a diferentes clases. El siguiente XML representa un archivo de enlace personalizado.

```as3
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

Utilice este archivo XML al crear archivos proxy Java mediante JAX-WS. (Consulte [Creación de clases proxy de Java mediante JAX-WS](#creating-java-proxy-classes-using-jax-ws)).

Haga referencia a este archivo XML al ejecutar la herramienta JAX-WS (wsimport.exe) mediante la opción de línea de comandos - `b` . Actualice el `wsdlLocation` elemento en el archivo XML de enlace para especificar la URL de AEM Forms.

Para asegurarse de que la invocación asincrónica funciona, modifique el valor de la URL del punto final y especifique `async=true`. Por ejemplo, para los archivos proxy de Java que se crean con JAX-WS, especifique lo siguiente para el `BindingProvider.ENDPOINT_ADDRESS_PROPERTY`.

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

La siguiente lista especifica otros servicios que necesitan un archivo de enlace personalizado cuando se invocan de forma asíncrona:

* PDFG3D
* Administrador de tareas
* Application Manager
* Administrador de directorios
* Distiller
* Rights Management
* Administración de documentos

### Diferencias en los servidores de aplicaciones J2EE {#differences-in-j2ee-application-servers}

A veces, una biblioteca proxy creada con un servidor de aplicaciones J2EE específico no invoca correctamente los formularios AEM alojados en otro servidor de aplicaciones J2EE. Considere la posibilidad de crear una biblioteca proxy que se genere con AEM Forms y que se implemente en WebSphere. Esta biblioteca proxy no puede invocar correctamente los servicios de AEM Forms implementados en el servidor de aplicaciones JBoss.

Algunos tipos de datos complejos de AEM Forms, como `PrincipalReference`AEM Forms, se definen de forma diferente cuando AEM Forms se implementa en WebSphere en comparación con JBoss Application Server. Las diferencias en los JDK utilizados por los diferentes servicios de aplicación J2EE son la razón por la que existen diferencias en las definiciones de WSDL. Como resultado, utilice bibliotecas proxy generadas desde el mismo servidor de aplicaciones J2EE.

### Acceso a varios servicios mediante servicios Web {#accessing-multiple-services-using-web-services}

Debido a conflictos de espacio de nombres, los objetos de datos no se pueden compartir entre varios WSDL de servicio. Los diferentes servicios pueden compartir tipos de datos y, por lo tanto, los servicios comparten la definición de estos tipos en los WSDL. Por ejemplo, no puede agregar dos ensamblados de cliente .NET que contengan un tipo `BLOB` de datos al mismo proyecto de cliente .NET. Si intenta hacerlo, se producirá un error de compilación.

La siguiente lista especifica los tipos de datos que no se pueden compartir entre varios WSDL de servicios:

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

Para evitar este problema, se recomienda que califique completamente los tipos de datos. Por ejemplo, piense en una aplicación .NET que haga referencia tanto al servicio Forms como al servicio Signature mediante una referencia de servicio. Ambas referencias de servicio contendrán una `BLOB` clase. Para utilizar una `BLOB` instancia, califique completamente el `BLOB` objeto cuando lo declare. Este enfoque se muestra en el siguiente ejemplo de código. Para obtener información sobre este ejemplo de código, consulte Firma [digital de formularios](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)interactivos.

En el siguiente ejemplo de código C# se firma un formulario interactivo procesado por el servicio Forms. La aplicación cliente tiene dos referencias de servicio. La `BLOB` instancia asociada al servicio Forms pertenece al `SignInteractiveForm.ServiceReference2` espacio de nombres. Del mismo modo, la `BLOB` instancia asociada al servicio Signature pertenece al `SignInteractiveForm.ServiceReference1` espacio de nombres. El formulario interactivo firmado se guarda como un archivo PDF denominado *LoanXFASigned.pdf*.

```as3
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

### Servicios que comienzan con la letra Produzco archivos proxy no válidos {#services-starting-with-the-letter-i-produce-invalid-proxy-files}

El nombre de algunas clases proxy generadas por AEM Forms es incorrecto al utilizar Microsoft .Net 3.5 y WCF. Este problema se produce cuando se crean clases proxy para IBMFilenetContentRepositoryConnector, IDPSchedulerService o cualquier otro servicio cuyo nombre comience por la letra I. Por ejemplo, el nombre del cliente generado en el caso de IBMFileNetContentRepositoryConnector es `BMFileNetContentRepositoryConnectorClient`. Falta la letra I en la clase proxy generada.

