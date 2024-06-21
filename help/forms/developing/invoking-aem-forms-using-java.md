---
title: Invocar AEM Forms mediante la API de Java
description: Utilice la API de Java de AEM Forms SOAP para el protocolo de transporte RMI para la invocación remota, el transporte de VM para la invocación local, el transporte para la invocación remota, la autenticación diferente, como el nombre de usuario y la contraseña, y las solicitudes de invocación sincrónicas y asincrónicas.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
exl-id: 036c35c1-1be7-4825-bbb6-ea025e49c6f6
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '5333'
ht-degree: 0%

---

# Invocar AEM Forms mediante la API de Java {#invoking-aem-forms-using-the-javaapi}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

AEM Forms se puede invocar mediante la API de Java de AEM Forms. Al utilizar la API de Java de AEM Forms, puede utilizar la API de invocación o las bibliotecas de cliente de Java. Las bibliotecas de cliente Java están disponibles para servicios como el servicio Rights Management. Estas API con establecimiento inflexible de tipos le permiten desarrollar aplicaciones Java que invocan AEM Forms.

La API de invocación son clases que se encuentran en `com.adobe.idp.dsc` paquete. Con estas clases, se puede enviar una solicitud de invocación directamente a un servicio y controlar una respuesta de invocación que se devuelve. Utilice la API de invocación para invocar procesos de corta o larga duración creados con Workbench.

La forma recomendada de invocar un servicio mediante programación es utilizar una biblioteca de cliente Java que corresponda al servicio en lugar de la API de invocación. Por ejemplo, para invocar el servicio Encryption, utilice la biblioteca de cliente del servicio Encryption. Para realizar una operación del servicio Encryption, invoque un método que pertenezca al objeto de cliente del servicio Encryption. Puede cifrar un documento de PDF con una contraseña invocando la variable `EncryptionServiceClient` del objeto `encryptPDFUsingPassword` método.

La API de Java admite las siguientes funciones:

* Protocolo de transporte RMI para invocación remota
* Transporte de VM para invocación local
* SOAP para invocación remota de
* Autenticación diferente, como nombre de usuario y contraseña
* Solicitudes de invocación sincrónicas y asincrónicas

[Incluir archivos de biblioteca Java de AEM Forms](#including-aem-forms-java-library-files)

[Invocar procesos de larga duración centrados en el ser humano](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Invocar AEM Forms mediante servicios web](/help/forms/developing/invoking-aem-forms-using-web.md)

[Estableciendo propiedades de conexión](#setting-connection-properties)

[Pasar datos a servicios de AEM Forms mediante la API de Java](#passing-data-to-aem-forms-services-using-the-java-api)

[Invocar un servicio mediante una biblioteca de cliente Java](#invoking-a-service-using-a-java-client-library)

[Invocación de un proceso de corta duración mediante la API de invocación](#invoking-a-short-lived-process-using-the-invocation-api)

[Creación de una aplicación web Java que invoque un proceso de larga duración centrado en humanos](/help/forms/developing/invoking-human-centric-long-lived.md)

## Incluir archivos de biblioteca Java de AEM Forms {#including-aem-forms-java-library-files}

Para invocar mediante programación un servicio de AEM Forms mediante la API de Java, incluya los archivos de biblioteca necesarios (archivos JAR) en la ruta de clase del proyecto Java. Los archivos JAR que se incluyen en la ruta de clase de la aplicación cliente dependen de varios factores:

* El servicio AEM Forms que se va a invocar. Una aplicación cliente puede invocar uno o varios servicios.
* El modo en el que desea invocar un servicio de AEM Forms. SOAP Puede utilizar el modo EJB o de. (Consulte [Estableciendo propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>(Solo llave en mano) Inicie el servidor de AEM Forms con el comando `standalone.bat -b <Server IP> -c lc_turnkey.xml` para especificar una IP de servidor para EJB

* Servidor de aplicaciones J2EE en el que está implementado AEM Forms.

### Archivos JAR específicos del servicio {#service-specific-jar-files}

En la tabla siguiente se enumeran los archivos JAR necesarios para invocar los servicios de AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>Archivo</p></th>
   <th><p>Descripción</p></th>
   <th><p>Lugar de residencia</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe-livecycle-client.jar</p></td>
   <td><p>Siempre debe incluirse en la ruta de clase de una aplicación cliente Java.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>Siempre debe incluirse en la ruta de clase de una aplicación cliente Java.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>Siempre debe incluirse en la ruta de clase de una aplicación cliente Java.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk//client-libs/&lt;app server=""&gt;</p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>Necesario para invocar el servicio Administrador de aplicaciones.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Assembler. </p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>Necesario para invocar la API del servicio de backup y restauración.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de Forms con códigos de barras. </p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>Necesario para invocar el servicio ConvertPDF. </p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Distiller.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>Necesario para invocar el servicio DocConverter.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de Administración de documentos.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Encryption.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Forms.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de integración de datos de formulario.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Generate PDF.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Generate 3D PDF.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>Necesario para invocar el servicio Administrador de trabajos. </p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Output.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Utilidades de PDF XMP o Utilidades de la.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Acrobat Reader DC Extensions.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>Necesario para invocar el servicio de repositorio.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs\third-party</p></td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>adobe-rightsmanagement-client.jar</p></li>
     <li><p>namespace.jar</p></li>
     <li><p>jaxb-api.jar</p></li>
     <li><p>jaxb-impl.jar</p></li>
     <li><p>jaxb-libs.jar</p></li>
     <li><p>jaxb-xjc.jar</p></li>
     <li><p>relaxngDatatype.jar</p></li>
     <li><p>xsdlib.jar</p></li>
    </ul></td>
   <td><p>Necesario para invocar el servicio de Rights Management.</p><p>Si AEM Forms está implementado en JBoss, incluya todos estos archivos. </p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p><p>Directorio lib específico de JBoss</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Signature.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>Necesario para invocar el servicio Administrador de tareas. </p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Almacén de confianza. </p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
 </tbody>
</table>

### Modo de conexión y archivos JAR de la aplicación J2EE {#connection-mode-and-j2ee-application-jar-files}

En la tabla siguiente se enumeran los archivos JAR que dependen del modo de conexión y del servidor de aplicaciones J2EE en el que AEM Forms está implementado.

<table>
 <thead>
  <tr>
   <th><p>Archivo</p> </th>
   <th><p>Descripción</p> </th>
   <th><p>Lugar de residencia</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td>
    <ul>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
    </ul>
    <ul>
     <li>xercesImpl.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> <p> </p> </td>
   <td><p>si se invoca AEM Forms SOAP mediante el modo de, incluya estos archivos JAR.</p> </td>
   <td><p>&lt;<em>directorio de instalación</em>&gt;/sdk/client-libs/third-party</p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>si AEM Forms está implementado en el servidor de aplicaciones JBoss, incluya este archivo JAR.</p> <p>El cargador de clases no encontrará las clases requeridas si jboss-client.jar y los archivos .jar a los que se hace referencia no están ubicados conjuntamente.</p> </td>
   <td><p>Directorio de biblioteca del cliente de JBoss</p> <p>Si implementa la aplicación cliente en el mismo servidor de aplicaciones J2EE, no es necesario incluir este archivo.</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>si AEM Forms está implementado en BEA WebLogic Server®, incluya este archivo JAR.</p> </td>
   <td><p>Directorio de biblioteca específico de WebLogic</p> <p>Si implementa la aplicación cliente en el mismo servidor de aplicaciones J2EE, no es necesario incluir este archivo.</p> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>com.ibm.ws.admin.client_6.1.0.jar</p> </li>
     <li><p>com.ibm.ws.webservices.thinclient_6.1.0.jar</p> </li>
    </ul> </td>
   <td>
    <ul>
     <li><p>si AEM Forms está implementado en el servidor de aplicaciones WebSphere, incluya estos archivos JAR.</p> </li>
     <li><p>(com.ibm.ws.webservices.thinclient_6.1.0.jar es necesario para invocar el servicio web).</p> </li>
    </ul> </td>
   <td><p>Directorio lib específico de WebSphere (<em>[WAS_HOME]</em>/runtimes)</p> <p>Si implementa la aplicación cliente en el mismo servidor de aplicaciones J2EE, no tiene que incluir estos archivos.</p> </td>
  </tr>
 </tbody>
</table>

### Invocación de escenarios {#invoking-scenarios}

La siguiente tabla especifica la invocación de escenarios y enumera los archivos JAR necesarios para invocar correctamente AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>Servicios</p> </th>
   <th><p>Modo de invocación</p> </th>
   <th><p>Servidor de aplicaciones J2EE</p> </th>
   <th><p>Archivos JAR necesarios</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td><p>servicio de Forms</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar</li>
    </ul>
    <ul>
     <li>adobe-forms-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>servicio de Forms</p> <p>servicio de extensiones de Acrobat Reader DC</p> <p>Servicio de firmas</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul>
    <ul>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>servicio de Forms</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>servicio de Forms</p> <p>servicio de extensiones de Acrobat Reader DC</p> <p>Servicio de firmas</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr> xmp-uti
 </tbody>
</table>

### Actualización de archivos JAR {#upgrading-jar-files}

Si está actualizando desde la LiveCycle a AEM Forms, se recomienda incluir los archivos JAR de AEM Forms en la ruta de clase del proyecto Java. Por ejemplo, si utiliza servicios como el servicio Rights Management, encontrará un problema de compatibilidad si no incluye archivos JAR de AEM Forms en la ruta de clase.

Suponiendo que está actualizando a AEM Forms. Para utilizar una aplicación Java que invoque el servicio de Rights Management, incluya las versiones de AEM Forms de los siguientes archivos JAR:

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**Consulte también**

[Invocar AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Estableciendo propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

[Pasar datos a servicios de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Invocar un servicio mediante una biblioteca de cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Estableciendo propiedades de conexión {#setting-connection-properties}

Las propiedades de conexión se establecen para invocar AEM Forms al utilizar la API de Java. Al establecer las propiedades de conexión, especifique si desea invocar los servicios de forma remota o local, así como el modo de conexión y los valores de autenticación. Se requieren valores de autenticación si la seguridad del servicio está habilitada. Sin embargo, si la seguridad del servicio está deshabilitada, no es necesario especificar los valores de autenticación.

SOAP El modo de conexión puede ser modo de conexión o modo de EJB de tipo. SOAP El modo EJB utiliza el protocolo RMI/IIOP, y el rendimiento del modo EJB es mejor que el rendimiento del modo de. SOAP El modo de la aplicación se utiliza para eliminar una dependencia del servidor de aplicaciones J2EE o cuando se encuentra un cortafuegos entre AEM Forms y la aplicación cliente. SOAP El modo de utiliza el protocolo https como transporte subyacente y puede comunicarse entre los límites del cortafuegos. Si no existe ninguna dependencia del servidor de aplicaciones J2EE o un cortafuegos, se recomienda utilizar el modo EJB.

Para invocar correctamente un servicio de AEM Forms, establezca las siguientes propiedades de conexión:

* **DSC_DEFAULT_EJB_ENDPOINT:** Si está utilizando el modo de conexión EJB, este valor representa la URL del servidor de aplicaciones J2EE en el que está implementado AEM Forms. Para invocar AEM Forms de forma remota, especifique el nombre del servidor de aplicaciones J2EE en el que está implementado AEM Forms. Si la aplicación cliente se encuentra en el mismo servidor de aplicaciones J2EE, puede especificar `localhost`. En función del servidor de aplicaciones J2EE en el que esté implementado AEM Forms, especifique uno de los siguientes valores:

   * JBoss: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLogic: `t3://<ServerName>:7001 (default port)`

* **SOAP DSC_DEFAULT__ENDPOINT** SOAP : Si utiliza el modo de conexión de la, este valor representa el extremo al que se envía una solicitud de invocación. Para invocar AEM Forms de forma remota, especifique el nombre del servidor de aplicaciones J2EE en el que está implementado AEM Forms. Si la aplicación cliente se encuentra en el mismo servidor de aplicaciones J2EE, puede especificar `localhost` (por ejemplo, `http://localhost:8080`.)

   * El valor de puerto `8080` es aplicable si la aplicación J2EE es JBoss. Si el servidor de aplicaciones J2EE es IBM® WebSphere®, utilice el puerto `9080`. Igualmente, si el servidor de aplicaciones J2EE es WebLogic, utilice el puerto `7001`. (Estos valores son valores de puerto predeterminados. Si cambia el valor del puerto, utilice el número de puerto aplicable).

* **DSC_TRANSPORT_PROTOCOL**: Si utiliza el modo de conexión EJB, especifique `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` para este valor. SOAP Si está utilizando el modo de conexión de, especifique `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`.
* **DSC_SERVER_TYPE**: Especifica el servidor de aplicaciones J2EE en el que se implementa AEM Forms. Los valores válidos son `JBoss`, `WebSphere`, `WebLogic`.

   * Si establece esta propiedad de conexión en `WebSphere`, el `java.naming.factory.initial` el valor se establece en `com.ibm.ws.naming.util.WsnInitCtxFactory`.
   * Si establece esta propiedad de conexión en `WebLogic`, el `java.naming.factory.initial` el valor se establece en `weblogic.jndi.WLInitialContextFactory`.
   * Del mismo modo, si establece esta propiedad de conexión en `JBoss`, el `java.naming.factory.initial` el valor se establece en `org.jnp.interfaces.NamingContextFactory`.
   * Puede configurar las variables `java.naming.factory.initial` a un valor que cumpla sus necesidades si no desea utilizar los valores predeterminados.

  >[!NOTE]
  >
  >En lugar de utilizar una cadena para establecer la variable `DSC_SERVER_TYPE` propiedad de conexión, puede utilizar un miembro estático del `ServiceClientFactoryProperties` clase. Se pueden utilizar los siguientes valores: `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`, `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE`, o `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`.

* **DSC_CREDENTIAL_USERNAME:** AEM Especifica el nombre de usuario de los formularios. Para que un usuario invoque correctamente un servicio de AEM Forms, necesita la función Usuario de servicios. Un usuario también puede tener otra función que incluya el permiso Invocar servicio. De lo contrario, se produce una excepción cuando intentan invocar un servicio. Si la seguridad del servicio está deshabilitada, no es necesario especificar esta propiedad de conexión.
* **DSC_CREDENTIAL_PASSWORD:** Especifica el valor de contraseña correspondiente. Si la seguridad del servicio está deshabilitada, no es necesario especificar esta propiedad de conexión.
* **DSC_REQUEST_TIMEOUT:** SOAP El límite de tiempo de espera de solicitud predeterminado para la solicitud de es de 1200000 milisegundos (20 minutos). En ocasiones, una solicitud puede requerir más tiempo para completar la operación. SOAP Por ejemplo, una solicitud de que recupera un gran conjunto de registros puede requerir un límite de tiempo de espera más largo. Puede usar el complemento `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` SOAP para aumentar el límite de tiempo de espera de la llamada de solicitud para las solicitudes de.

  **nota** SOAP : Solo las invocaciones basadas en la admiten la propiedad DSC_REQUEST_TIMEOUT.

Para establecer las propiedades de conexión, realice las siguientes tareas:

1. Crear un `java.util.Properties` mediante su constructor.
1. Para establecer la variable `DSC_DEFAULT_EJB_ENDPOINT` propiedad de conexión, invocar el `java.util.Properties` del objeto `setProperty` y pasar los siguientes valores:

   * El `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` valor de enumeración
   * Valor de cadena que especifica la dirección URL del servidor de aplicaciones J2EE que aloja AEM Forms

   >[!NOTE]
   >
   >SOAP Si está utilizando el modo de conexión de, especifique el `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` valor de enumeración en lugar de `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` valor de enumeración.

1. Para establecer la variable `DSC_TRANSPORT_PROTOCOL` propiedad de conexión, invocar el `java.util.Properties` del objeto `setProperty` y pasar los siguientes valores:

   * El `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL` valor de enumeración
   * El `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` valor de enumeración

   >[!NOTE]
   >
   >SOAP Si está utilizando el modo de conexión de, especifique el `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`valor de enumeración en lugar de `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` valor de enumeración.

1. Para establecer la variable `DSC_SERVER_TYPE` propiedad de conexión, invocar el `java.util.Properties` del objeto `setProperty` y pasar los siguientes valores:

   * El `ServiceClientFactoryProperties.DSC_SERVER_TYPE`valor de enumeración
   * Un valor de cadena que especifica el servidor de aplicaciones J2EE que aloja AEM Forms (por ejemplo, si AEM Forms está implementado en JBoss, especifique `JBoss`).

      1. Para establecer la variable `DSC_CREDENTIAL_USERNAME` propiedad de conexión, invocar el `java.util.Properties` del objeto `setProperty` y pasar los siguientes valores:

   * El `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME` valor de enumeración
   * Valor de cadena que especifica el nombre de usuario necesario para invocar AEM Forms

      1. Para establecer la variable `DSC_CREDENTIAL_PASSWORD` propiedad de conexión, invocar el `java.util.Properties` del objeto `setProperty` y pasar los siguientes valores:

   * El `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD` valor de enumeración
   * Un valor de cadena que especifica el valor de contraseña correspondiente

**Configuración del modo de conexión EJB para JBoss**

El siguiente ejemplo de código Java establece las propiedades de conexión para invocar AEM Forms implementado en JBoss y utilizar el modo de conexión EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "https://<hostname>:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"https://<hostname>:8080");
```

**Configuración del modo de conexión EJB para WebLogic**

En el siguiente ejemplo de código Java se establecen las propiedades de conexión para invocar AEM Forms implementado en WebLogic y utilizar el modo de conexión EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Configuración del modo de conexión EJB para WebSphere**

El siguiente ejemplo de código Java establece las propiedades de conexión para invocar AEM Forms implementado en WebSphere y utilizar el modo de conexión EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**SOAP Configuración del modo de conexión de la**

SOAP En el siguiente ejemplo de código Java se establecen las propiedades de conexión en modo de para invocar el AEM Forms implementado en JBoss.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

>[!NOTE]
>
>SOAP Si selecciona el modo de conexión de, asegúrese de incluir archivos JAR adicionales en la ruta de clase de la aplicación cliente.

**Establecer propiedades de conexión cuando la seguridad del servicio está deshabilitada**

El siguiente ejemplo de código Java establece las propiedades de conexión necesarias para invocar AEM Forms implementado en el servidor de aplicaciones JBoss y cuando la seguridad del servicio está deshabilitada.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>Todos los tutoriales rápidos de Java asociados con la programación con AEM Forms SOAP muestran la configuración de conexión de EJB y de la conexión de la.

**SOAP Configuración del modo de conexión de la con el límite de tiempo de espera de solicitud personalizado**

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**Uso de un objeto Context para invocar AEM Forms**

Puede usar un `com.adobe.idp.Context` objeto para invocar un servicio de AEM Forms con un usuario autenticado (el `com.adobe.idp.Context` representa un usuario autenticado). Cuando se utiliza un `com.adobe.idp.Context` objeto, no es necesario configurar el `DSC_CREDENTIAL_USERNAME` o `DSC_CREDENTIAL_PASSWORD` propiedades. Puede obtener un `com.adobe.idp.Context` al autenticar usuarios mediante el uso del objeto `AuthenticationManagerServiceClient` del objeto `authenticate` método.

El `authenticate` El método devuelve un `AuthResult` que contiene los resultados de la autenticación. Puede crear un `com.adobe.idp.Context` invocando su constructor. A continuación, invoque el `com.adobe.idp.Context` del objeto `initPrincipal` y pase el `AuthResult` , tal como se muestra en el código siguiente:

```java
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

En lugar de configurar la variable `DSC_CREDENTIAL_USERNAME` o `DSC_CREDENTIAL_PASSWORD` , puede invocar el método `ServiceClientFactory` del objeto `setContext` y pase el `com.adobe.idp.Context` objeto. AEM Cuando utilice un usuario de formularios para invocar un servicio, asegúrese de que tiene la función denominada `Services User` que es necesario para invocar un servicio de AEM Forms.

En el ejemplo de código siguiente se muestra cómo utilizar un `com.adobe.idp.Context` dentro de la configuración de conexión que se utiliza para crear un objeto `EncryptionServiceClient` objeto.

```java
 //Authenticate a user and use the Context object within connection settings
 // Authenticate the user
 String username = "wblue";
 String password = "password";
 AuthResult authResult = authClient.authenticate(username, password.getBytes());
 
 //Set a Content object that represents the authenticated user
 //Use the Context object to invoke the Encryption service
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
 
 //Set connection settings
 Properties connectionProps = new Properties();
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://<server>:1099");
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"jnp://<server>:1099");

 
 //Create a ServiceClientFactory object
 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 myFactory.setContext(myCtx);
 
 //Create an EncryptionServiceClient object
 EncryptionServiceClient encryptClient  = new EncryptionServiceClient(myFactory);
```

>[!NOTE]
>
>Para obtener información detallada sobre la autenticación de un usuario, consulte [Autenticar usuarios](/help/forms/developing/users.md#authenticating-users).

### Invocación de escenarios {#invoking_scenarios-1}

Los siguientes escenarios de invocación se analizan en esta sección:

* Una aplicación cliente que se ejecuta en su propia máquina virtual Java (JVM) invoca una instancia de AEM Forms independiente.
* Una aplicación cliente que se ejecuta en su propia JVM invoca instancias de AEM Forms agrupadas.

### Aplicación cliente que invoca una instancia de AEM Forms independiente {#client-application-invoking-a-stand-alone-aem-forms-instance}

El diagrama siguiente muestra una aplicación cliente ejecutándose en su propia JVM e invocando una instancia de AEM Forms independiente.

En esta situación, una aplicación cliente se está ejecutando en su propia JVM e invoca los servicios de AEM Forms.

>[!NOTE]
>
>Este escenario es el escenario de invocación en el que se basan todos los inicios rápidos.

### Aplicación cliente que invoca instancias de AEM Forms agrupadas {#client-application-invoking-clustered-aem-forms-instances}

En el diagrama siguiente se muestra una aplicación cliente ejecutándose en su propia JVM e invocando instancias de AEM Forms en un clúster.

Este escenario es similar a una aplicación cliente que invoca una instancia de AEM Forms independiente. Sin embargo, la dirección URL del proveedor es diferente. Si una aplicación cliente desea conectarse a un servidor de aplicaciones J2EE específico, la aplicación debe cambiar la URL para hacer referencia al servidor de aplicaciones J2EE específico.

No se recomienda hacer referencia a un servidor de aplicaciones J2EE específico porque la conexión entre la aplicación cliente y AEM Forms finaliza si el servidor de aplicaciones se detiene. Se recomienda que la dirección URL del proveedor haga referencia a un administrador JNDI de nivel de celda, en lugar de a un servidor de aplicaciones J2EE específico.

SOAP Las aplicaciones cliente que utilizan el modo de conexión de la red de distribución pueden utilizar el puerto del equilibrador de carga HTTP para el clúster. Las aplicaciones cliente que utilizan el modo de conexión EJB pueden conectarse al puerto EJB de un servidor de aplicaciones J2EE específico. Esta acción administra el equilibrio de carga entre los nodos del clúster.

**WebSphere**

En el ejemplo siguiente se muestra el contenido de un archivo jndi.properties que se utiliza para conectarse a AEM Forms implementado en WebSphere.

```ini
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**Lógica web**

El ejemplo siguiente muestra el contenido de un archivo jndi.properties que se utiliza para conectarse a AEM Forms que se implementa en WebLogic.

```ini
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

El ejemplo siguiente muestra el contenido de un archivo jndi.properties que se utiliza para conectarse a AEM Forms que se despliega en JBoss.

```ini
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>Consulte al administrador para determinar el nombre y el número de puerto del servidor de aplicaciones J2EE.

**Consulte también**

[Inclusión AEM Forms archivos de biblioteca Java](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Transmisión de datos a servicios de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Llamada a un servicio mediante un biblioteca de cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Transmisión de datos a servicios de AEM Forms mediante la API de Java {#passing-data-to-aem-forms-services-using-the-java-api}

Las operaciones del servicio AEM Forms suelen consumir o producir documentos de PDF. Al invocar un servicio, a veces es necesario pasar un documento de PDF (u otros tipos de documento como datos XML) al servicio. Del mismo modo, a veces es necesario gestionar un documento de PDF que se devuelve desde el servicio. La clase Java que permite pasar datos desde y hacia servicios de AEM Forms es `com.adobe.idp.Document`.

Los servicios de AEM Forms no aceptan un documento de PDF como otros tipos de datos, como `java.io.InputStream` o una matriz de bytes. A `com.adobe.idp.Document` también se puede utilizar para pasar otros tipos de datos, como datos XML, a los servicios.

A `com.adobe.idp.Document` El objeto es un tipo serializable Java, por lo que se puede pasar a través de una llamada RMI. El lado receptor puede estar ubicado (el mismo host, el mismo cargador de clase), ser local (el mismo host, un cargador de clase diferente) o remoto (un host diferente). La transferencia del contenido del documento está optimizada para cada caso. Por ejemplo, si el remitente y el destinatario se encuentran en el mismo host, el contenido se pasa a través de un sistema de archivos local. (En algunos casos, los documentos se pueden pasar en la memoria).

Según la variable `com.adobe.idp.Document` tamaño del objeto, los datos se transmiten dentro del `com.adobe.idp.Document` objeto o almacenado en el sistema de archivos del servidor. Cualquier recurso de almacenamiento temporal ocupado por el `com.adobe.idp.Document` se quitan automáticamente al `com.adobe.idp.Document` eliminación. (Consulte [Desechar objetos de documento](invoking-aem-forms-using-java.md#disposing-document-objects).)

A veces es necesario conocer el tipo de contenido de una `com.adobe.idp.Document` antes de poder pasarlo a un servicio. Por ejemplo, si una operación requiere un tipo de contenido específico, como `application/pdf`Sin embargo, se recomienda determinar el tipo de contenido. (Consulte [Determinación del tipo de contenido de un documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document).)

El `com.adobe.idp.Document` intenta determinar el tipo de contenido mediante los datos proporcionados. Si no se puede recuperar el tipo de contenido de los datos suministrados (por ejemplo, cuando los datos se suministraron como una matriz de bytes), establezca el tipo de contenido. Para establecer el tipo de contenido, invoque el `com.adobe.idp.Document` del objeto `setContentType` método. (Consulte [Determinación del tipo de contenido de un documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

Si los archivos colaterales residen en el mismo sistema de archivos, crear un `com.adobe.idp.Document` El objeto es más rápido. Si los archivos auxiliares residen en sistemas de archivos remotos, se debe realizar una operación de copia, lo que afecta al rendimiento.

Una aplicación puede contener ambos `com.adobe.idp.Document` y `org.w3c.dom.Document` tipos de datos. No obstante, asegúrese de que cumple todos los requisitos del `org.w3c.dom.Document` tipo de datos. Para obtener información sobre la conversión de un `org.w3c.dom.Document` objeto a `com.adobe.idp.Document` objeto, consulte [Inicio rápido (modo EJB): rellenar previamente Forms con diseños flexibles mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api).

>[!NOTE]
>
>Para evitar una fuga de memoria en WebLogic mientras se utiliza un `com.adobe.idp.Document` , lea la información del documento en fragmentos de 2048 bytes o menos. Por ejemplo, el siguiente código lee la información del documento en fragmentos de 2048 bytes:

```java
        // Set up the chunk size to prevent a potential memory leak
        int buffSize = 2048;
 
        // Determine the total number of bytes to read
        int docLength = (int) inDoc.length();
        byte [] byteDoc = new byte[docLength];
 
        // Set up the reading position
        int pos = 0;
 
        // Loop through the document information, 2048 bytes at a time
        while (docLength > 0) {
      // Read the next chunk of information
            int toRead = Math.min(buffSize, docLength);
            int bytesRead = inDoc.read(pos, byteDoc, pos, toRead);
 
            // Handle the exception in case data retrieval failed
            if (bytesRead == -1) {
 
                inDoc.doneReading();
                inDoc.dispose();
                throw new RuntimeException("Data retrieval failed!");
 
            }
 
             // Update the reading position and number of bytes remaining
             pos += bytesRead;
             docLength -= bytesRead;
 
        }
 
        // The document information has been successfully read
        inDoc.doneReading();
        inDoc.dispose();
```

**Consulte también**

[Invocar AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Estableciendo propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

### Creación de documentos {#creating-documents}

Crear un `com.adobe.idp.Document` antes de invocar una operación de servicio que requiere un documento de PDF (u otros tipos de documento) como valor de entrada. El `com.adobe.idp.Document` proporciona constructores que permiten crear un documento a partir de los siguientes tipos de contenido:

* Una matriz de bytes
* Un existente `com.adobe.idp.Document` objeto
* A `java.io.File` objeto
* A `java.io.InputStream` objeto
* A `java.net.URL` objeto

#### Creación de un documento basado en una matriz de bytes {#creating-a-document-based-on-a-byte-array}

En el ejemplo de código siguiente se crea un `com.adobe.idp.Document` que se basa en una matriz de bytes.

**Crear un objeto Document basado en una matriz de bytes**

```java
 Document myPDFDocument = new Document(myByteArray);
```

#### Creación de un documento basado en otro documento {#creating-a-document-based-on-another-document}

En el ejemplo de código siguiente se crea un `com.adobe.idp.Document` objeto basado en otro `com.adobe.idp.Document` objeto.

**Crear un objeto Document basado en otro documento**

```java
 //Create a Document object based on a byte array
 InputStream is = new FileInputStream("C:\\Map.pdf");
 int len = is.available();
 byte [] myByteArray = new byte[len];
 int i = 0;
 while (i < len) {
       i += is.read(myByteArray, i, len);
 }
 Document myPDFDocument = new Document(myByteArray);
 
 //Create another Document object
 Document anotherDocument = new Document(myPDFDocument);
```

#### Creación de un documento basado en un archivo {#creating-a-document-based-on-a-file}

En el ejemplo de código siguiente se crea un `com.adobe.idp.Document` objeto basado en un archivo de PDF denominado *map.pdf*. Este archivo se encuentra en la raíz del disco duro C. Este constructor intenta establecer el tipo de contenido MIME de `com.adobe.idp.Document` usando la extensión de nombre de archivo.

El `com.adobe.idp.Document` constructor que acepta un `java.io.File` El objeto también acepta un parámetro Boolean. Estableciendo este parámetro en `true`, el `com.adobe.idp.Document` elimina el archivo. Esta acción significa que no tiene que eliminar el archivo después de pasarlo al `com.adobe.idp.Document` constructor.

Estableciendo este parámetro en `false` significa que conserva la propiedad de este archivo. Estableciendo este parámetro en `true` es más eficiente. El motivo es que la variable `com.adobe.idp.Document` puede mover el archivo directamente al área administrada local en lugar de copiarlo (lo que es más lento).

**Crear un objeto Document basado en un archivo de PDF**

```java
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### Crear un documento basado en un objeto InputStream {#creating-a-document-based-on-an-inputstream-object}

El siguiente ejemplo de código Java crea un `com.adobe.idp.Document` objeto que se basa en un `java.io.InputStream` objeto.

**Crear un documento basado en un objeto InputStream**

```java
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### Creación de un documento basado en contenido accesible desde una dirección URL {#creating-a-document-based-on-content-accessible-from-an-url}

El siguiente ejemplo de código Java crea un `com.adobe.idp.Document` objeto basado en un archivo de PDF denominado *map.pdf*. Este archivo se encuentra en una aplicación web denominada `WebApp` que se está ejecutando el `localhost`. Este constructor intenta establecer la variable `com.adobe.idp.Document` tipo de contenido MIME del objeto mediante el tipo de contenido devuelto con el protocolo URL.

La URL proporcionada a la `com.adobe.idp.Document` El objeto siempre se lee en el lado donde está el original `com.adobe.idp.Document` se crea el objeto, como se muestra en este ejemplo:

```java
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

El archivo c:/temp/input.pdf debe estar ubicado en el equipo cliente (no en el equipo servidor). El equipo cliente es donde se lee el URL y donde se crea el `com.adobe.idp.Document` objeto.

**Creación de una documento basada en contenido accesible desde una URL**

```java
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**Consulte también**

[Invocar AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Estableciendo propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

### Gestión de documentos devueltos {#handling-returned-documents}

Las operaciones de servicio que devuelven una documento PDF (u otros tipos de datos, como datos XML) como un valor de salida, devuelven un `com.adobe.idp.Document` objeto. Una vez recibido un `com.adobe.idp.Document` objeto, puede convertir a los formatos siguientes:

* Un `java.io.File` objeto
* Un `java.io.InputStream` objeto
* Una matriz de bytes

La siguiente línea de código convierte un `com.adobe.idp.Document` objeto a `java.io.InputStream` objeto. Supongamos que `myPDFDocument` representa un `com.adobe.idp.Document` objeto:

```java
     java.io.InputStream resultStream = myDocument.getInputStream();
```

Del mismo modo, puede copiar el contenido de una `com.adobe.idp.Document` a un archivo local realizando las siguientes tareas:

1. Crear un `java.io.File` objeto.
1. Invoque el `com.adobe.idp.Document` del objeto `copyToFile` y pase el `java.io.File`objeto.

En el ejemplo de código siguiente se copia el contenido de un objeto `com.adobe.idp.Document` objeto a un archivo denominado *AnotherMap.pdf*.

**Copiar el contenido de un objeto de documento en un archivo**

```java
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**Consulte también**

[Invocar AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Estableciendo propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinación del tipo de contenido de un documento {#determining-the-content-type-of-a-document}

Determinar el tipo MIME de una `com.adobe.idp.Document` invocando el objeto de `com.adobe.idp.Document` del objeto `getContentType` método. Este método devuelve un valor de cadena que especifica el tipo de contenido del `com.adobe.idp.Document` objeto. En la tabla siguiente se describen los diferentes tipos de contenido que devuelve AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>Tipo MIME</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>application/pdf</code></p></td>
   <td><p>documento de PDF</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xdp+xml</code></p></td>
   <td><p>Paquete de datos XML (XDP), que se utiliza para formularios XFA (arquitectura de Forms XML) exportados</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>Marcadores, archivos adjuntos u otros documentos XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>Formato de datos Forms (FDF), que se utiliza para formularios Acrobat exportados</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>Formato de datos XML Forms (XFDF), que se utiliza para formularios Acrobat exportados</p></td>
  </tr>
  <tr>
   <td><p><code>application/rdf+xml</code></p></td>
   <td><p>Formato de datos enriquecido y XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/octet-stream</code></p></td>
   <td><p>Formato de datos genérico</p></td>
  </tr>
  <tr>
   <td><p><code>NULL</code></p></td>
   <td><p>Tipo MIME no especificado</p></td>
  </tr>
 </tbody>
</table>

En el ejemplo de código siguiente se determina el tipo de contenido de un elemento `com.adobe.idp.Document` objeto.

**Determinar el tipo de contenido de un objeto Document**

```java
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**Consulte también**

[Invocar AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Estableciendo propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

### Desechar objetos de documento {#disposing-document-objects}

Cuando ya no necesite un `Document` objeto, se recomienda deshacerse de él invocando su `dispose` método. Cada `Document` consume un descriptor de archivo y hasta 75 MB de espacio en RAM en la plataforma host de la aplicación. Si un `Document` no se elimina, el proceso de recopilación Java Garage lo elimina. Sin embargo, si se elimina antes, se debe utilizar el `dispose` método, puede liberar la memoria ocupada por el `Document` objeto.

**Consulte también**

[Invocar AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Invocar un servicio mediante una biblioteca de cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Invocar un servicio mediante una biblioteca de cliente Java {#invoking-a-service-using-a-java-client-library}

Las operaciones del servicio AEM Forms se pueden invocar mediante la API con establecimiento inflexible de tipos de un servicio, que se conoce como biblioteca de cliente Java. A *Biblioteca de cliente Java* es un conjunto de clases concretas que proporcionan acceso a los servicios implementados en el contenedor de servicios. Puede crear una instancia de un objeto Java que represente el servicio que se va a invocar en lugar de crear un `InvocationRequest` mediante la API de invocación. La API de invocación se utiliza para invocar procesos, como procesos de larga duración, creados en Workbench. (Consulte [Invocar procesos de larga duración centrados en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

Para realizar una operación de servicio, invoque un método que pertenezca al objeto Java. Una biblioteca de cliente Java contiene métodos que generalmente se asignan de uno a uno con operaciones de servicio. Cuando utilice una biblioteca de cliente Java, establezca las propiedades de conexión necesarias. (Consulte [Estableciendo propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties).)

Después de establecer las propiedades de conexión, cree un `ServiceClientFactory` que se utiliza para crear una instancia de un objeto Java que le permite invocar un servicio. Cada servicio que tiene una biblioteca de cliente Java tiene un objeto de cliente correspondiente. Por ejemplo, para invocar el servicio de repositorio, cree un `ResourceRepositoryClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto. El `ServiceClientFactory` es responsable de mantener la configuración de conexión necesaria para invocar los servicios de AEM Forms.

Aunque la obtención de un `ServiceClientFactory` suele ser rápido, hay cierta sobrecarga cuando se utiliza la fábrica por primera vez. Este objeto está optimizado para su reutilización y, por lo tanto, cuando sea posible, utilice el mismo `ServiceClientFactory` cuando se crean varios objetos de cliente Java. Es decir, no cree un `ServiceClientFactory` para cada objeto de biblioteca de cliente que cree.

Existe una configuración del Administrador de usuarios que controla la duración de la aserción de SAML que se encuentra dentro de `com.adobe.idp.Context` objeto que afecta a `ServiceClientFactory` objeto. Esta opción controla todas las duraciones del contexto de autenticación a través de AEM Forms, incluidas todas las invocaciones realizadas mediante la API de Java. De forma predeterminada, el período de tiempo en el que `ServiceCleintFactory` el objeto puede usarse en dos horas.

>[!NOTE]
>
>Para explicar cómo invocar un servicio mediante la API de Java, el servicio de repositorio de `writeResource` se invoca la operación. Esta operación coloca un nuevo recurso en el repositorio.

Puede invocar el servicio de repositorio utilizando un biblioteca de cliente Java y realizando los pasos siguientes:

1. Incluya los archivos JAR del cliente, como adobe-repositorio-client.jar, en la ruta de clase del proyecto Java. Para obtener información sobre la ubicación de estos archivos, consulte [Incluidos AEM Forms archivos](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files) de biblioteca Java.
1. Establezca las propiedades de conexión necesarias para invocar un servicio.
1. Crear un `ServiceClientFactory` invocando el objeto de `ServiceClientFactory` objeto estático `createInstance` y pasando el `java.util.Properties` que contiene las propiedades de conexión.
1. Crear un `ResourceRepositoryClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto. Utilice el objeto para invocar operaciones de `ResourceRepositoryClient` servicio de repositorio.
1. Crear un `RepositoryInfomodelFactoryBean` objeto utilizando su constructor y pase `null`. Este objeto permite crear un `Resource` objeto que represente el contenido que se añade al repositorio.
1. Crear un `Resource` objeto invocando el `RepositoryInfomodelFactoryBean` método del `newImage` objeto y pasando los siguientes valores:

   * Un valor de ID único especificando `new Id()`.
   * Un valor UUID único especificando `new Lid()`.
   * Nombre del recurso. Puede especificar el nombre del archivo XDP.

   Convierta el valor devuelto en `Resource`.

1. Crear un `ResourceContent` invocando el objeto de `RepositoryInfomodelFactoryBean` del objeto `newImage` y convertir el valor devuelto en `ResourceContent`. Este objeto representa el contenido que se agrega al repositorio.
1. Crear un `com.adobe.idp.Document` al pasar un objeto `java.io.FileInputStream` que almacena el archivo XDP para agregarlo al repositorio. (Consulte [Crear un documento basado en un objeto InputStream](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object).)
1. Añada el contenido del `com.adobe.idp.Document` objeto a `ResourceContent` invocando el objeto de `ResourceContent` del objeto `setDataDocument` método. Pase el `com.adobe.idp.Document` objeto.
1. Establezca el tipo MIME del archivo XDP que se agregará al repositorio invocando el `ResourceContent` del objeto `setMimeType` método y paso `application/vnd.adobe.xdp+xml`.
1. Añada el contenido del `ResourceContent` objeto a `Resource` invocando el objeto de `Resource` del objeto `setContent` y pasando el `ResourceContent` objeto.
1. Añada una descripción del recurso invocando el `Resource` del objeto `setDescription` y pasando un valor de cadena que representa una descripción del recurso.
1. Agregue el diseño de formulario al repositorio invocando el `ResourceRepositoryClient` del objeto `writeResource` y pasando los siguientes valores:

   * Valor de cadena que especifica la ruta de acceso a la colección de recursos que contiene el nuevo recurso
   * El `Resource` objeto que se ha creado

**Consulte también**

[Inicio rápido (modo EJB): Escritura de un recurso mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Invocar AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## Invocación de un proceso de corta duración mediante la API de invocación {#invoking-a-short-lived-process-using-the-invocation-api}

Puede invocar un proceso de corta duración mediante la API de invocación de Java. Cuando invoca un proceso de corta duración mediante la API de invocación, pasa los valores de parámetro necesarios mediante una `java.util.HashMap` objeto. Para que cada parámetro pase a un servicio, invoque el `java.util.HashMap` del objeto `put` y especifique el par nombre-valor que requiere el servicio para realizar la operación especificada. Especifique el nombre exacto de los parámetros que pertenecen al proceso de corta duración.

>[!NOTE]
>
>Para obtener información sobre cómo invocar un proceso de larga duración, consulte [Invocar procesos de larga duración centrados en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

La discusión aquí trata sobre el uso de la API de invocación para invocar el siguiente proceso de corta duración de AEM Forms denominado `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para continuar con el ejemplo de código, cree un proceso denominado `MyApplication/EncryptDocument` Uso de Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento de PDF no protegido que se pasa al proceso. Esta acción se basa en `SetValue` operación. El parámetro de entrada para este proceso es un `document` variable de proceso denominada `inDoc`.
1. Cifra el documento del PDF con una contraseña. Esta acción se basa en `PasswordEncryptPDF` operación. El documento del PDF cifrado por contraseña se devuelve en una variable de proceso denominada `outDoc`.

### Invocar el proceso de corta duración MyApplication/EncryptDocument mediante la API de invocación de Java {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

Invoque el `MyApplication/EncryptDocument` proceso de corta duración mediante la API de invocación de Java:

1. Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clase del proyecto Java. (Consulte [Incluir archivos de biblioteca Java de AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)
1. Crear un `ServiceClientFactory` que contiene las propiedades de conexión. (Consulte [Estableciendo propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties).)
1. Crear un `ServiceClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto. A `ServiceClient` permite invocar una operación de servicio. Administra tareas como localizar, enviar y enrutar solicitudes de invocación.
1. Crear un `java.util.HashMap` mediante su constructor.
1. Invoque el `java.util.HashMap` del objeto `put` para que cada parámetro de entrada pase al proceso de larga duración. Debido a que el `MyApplication/EncryptDocument` el proceso de corta duración requiere un parámetro de entrada de tipo `Document`, solo tiene que invocar el `put` una vez, como se muestra en el ejemplo siguiente.

   ```java
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. Crear un `InvocationRequest` invocando el objeto de `ServiceClientFactory` del objeto `createInvocationRequest` y pasando los siguientes valores:

   * Un valor de cadena que especifica el nombre del proceso de larga duración que se va a invocar. Para invocar el `MyApplication/EncryptDocument` proceso, especificar `MyApplication/EncryptDocument`.
   * Valor de cadena que representa el nombre de la operación de proceso. Normalmente, el nombre de una operación de proceso de corta duración es `invoke`.
   * El `java.util.HashMap` que contiene los valores de parámetro que requiere la operación de servicio.
   * Un valor booleano que especifica `true`, que crea una solicitud sincrónica (este valor es aplicable para invocar un proceso de corta duración).

1. Envíe la solicitud de invocación al servicio invocando el `ServiceClient` del objeto `invoke` y pasando el `InvocationRequest` objeto. El `invoke` El método devuelve un `InvocationReponse` objeto.

   >[!NOTE]
   >
   >Se puede invocar un proceso de larga duración pasando el valor `false`como cuarto parámetro de la variable `createInvocationRequest` método. Pasar el valor `false`*crea una solicitud asincrónica.*

1. Recupere el valor devuelto del proceso invocando el método `InvocationReponse` del objeto `getOutputParameter` y pasando un valor de cadena que especifica el nombre del parámetro de salida. En esta situación, especifique `outDoc` ( `outDoc` es el nombre del parámetro de salida para `MyApplication/EncryptDocument` proceso). Convierta el valor devuelto en `Document`, como se muestra en el ejemplo siguiente.

   ```java
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. Crear un `java.io.File` y asegúrese de que la extensión del archivo es .pdf.
1. Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo. Asegúrese de utilizar el `com.adobe.idp.Document` objeto que ha devuelto el `getOutputParameter` método.

**Consulte también**

[Inicio rápido: invocación de un proceso de corta duración mediante la API de invocación](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[Invocar procesos de larga duración centrados en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Incluir archivos de biblioteca Java de AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
