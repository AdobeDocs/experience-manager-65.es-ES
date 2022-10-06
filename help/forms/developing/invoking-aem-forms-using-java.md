---
title: Invocación de AEM Forms mediante la API de Java
seo-title: Invoking AEM Forms using the JavaAPI
description: Utilice el protocolo de transporte AEM Forms Java API for RMI para invocación remota, transporte de VM para invocación local, SOAP para invocación remota, autenticación diferente, como nombre de usuario y contraseña, y solicitudes de invocación sincrónicas y asincrónicas.
seo-description: Use the AEM Forms Java API for RMI transport protocol for remote invocation, VM transport for local invocation, SOAP for remote invocation, different authentication, such as user name and password, and synchronous and asynchronous invocation requests.
uuid: 5e2fef2a-05f3-4283-8fd3-2d7dca411000
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0e6e7850-6137-42c5-b8e2-d4e352fddae2
role: Developer
exl-id: 036c35c1-1be7-4825-bbb6-ea025e49c6f6
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '5398'
ht-degree: 0%

---

# Invocación de AEM Forms mediante la API de Java {#invoking-aem-forms-using-the-javaapi}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

AEM Forms se puede invocar utilizando la API Java de AEM Forms. Al utilizar la API Java de AEM Forms, puede utilizar las bibliotecas API de invocación o de cliente Java. Las bibliotecas de cliente Java están disponibles para servicios como el servicio de Rights Management. Estas API con establecimiento inflexible de tipos le permiten desarrollar aplicaciones Java que invoquen AEM Forms.

La API de invocación son clases que se encuentran en la `com.adobe.idp.dsc` paquete. Con estas clases, puede enviar una solicitud de invocación directamente a un servicio y administrar una respuesta de invocación que se devuelve. Utilice la API de invocación para invocar procesos de corta duración o de larga duración creados mediante Workbench.

La forma recomendada de invocar un servicio mediante programación es utilizar una biblioteca de cliente Java que corresponda al servicio en lugar de la API de invocación. Por ejemplo, para invocar el servicio Encryption , utilice la biblioteca de cliente del servicio Encryption . Para realizar una operación del servicio de cifrado, invoque un método que pertenece al objeto cliente del servicio de cifrado. Puede cifrar un documento PDF con una contraseña invocando la variable `EncryptionServiceClient` del objeto `encryptPDFUsingPassword` método.

La API de Java admite las siguientes funciones:

* Protocolo de transporte RMI para invocación remota
* Transporte de VM para invocación local
* SOAP para invocación remota
* Distinta autenticación, como el nombre de usuario y la contraseña
* Solicitudes de invocación sincrónicas y asíncronas

[Inclusión de archivos de biblioteca Java de AEM Forms](#including-aem-forms-java-library-files)

[Invocación de procesos de larga vida centrados en el ser humano](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Invocación de AEM Forms mediante servicios web](/help/forms/developing/invoking-aem-forms-using-web.md)

[Configuración de las propiedades de conexión](#setting-connection-properties)

[Pasar datos a servicios de AEM Forms mediante la API de Java](#passing-data-to-aem-forms-services-using-the-java-api)

[Invocación de un servicio mediante una biblioteca de cliente Java](#invoking-a-service-using-a-java-client-library)

[Invocación de un proceso de corta duración mediante la API de invocación](#invoking-a-short-lived-process-using-the-invocation-api)

[Creación de una aplicación web de Java que invoque un proceso prolongado centrado en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md)

## Inclusión de archivos de biblioteca Java de AEM Forms {#including-aem-forms-java-library-files}

Para invocar mediante programación un servicio de AEM Forms utilizando la API de Java, incluya los archivos de biblioteca necesarios (archivos JAR) en la ruta de clase del proyecto Java. Los archivos JAR que incluye en la ruta de clase de la aplicación cliente dependen de varios factores:

* El servicio de AEM Forms que se va a invocar. Una aplicación cliente puede invocar uno o más servicios.
* Modo en el que desea invocar un servicio de AEM Forms. Puede utilizar el modo EJB o SOAP. (Consulte [Configuración de las propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>(Solo llave en mano) Inicie el servidor AEM Forms con el comando `standalone.bat -b <Server IP> -c lc_turnkey.xml` para especificar una IP de servidor para EJB

* El servidor de aplicaciones J2EE en el que se implementa AEM Forms.

### Archivos JAR específicos del servicio {#service-specific-jar-files}

La siguiente tabla enumera los archivos JAR necesarios para invocar los servicios de AEM Forms.

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
   <td><p>Necesario para invocar el servicio del Administrador de aplicaciones.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Assembler. </p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>Necesario para invocar la API de servicio de copia de seguridad y restauración.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de formularios con códigos de barras. </p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Convertir PDF. </p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de Distiller.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>Necesario para invocar el servicio DocConverter.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de gestión de documentos.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de cifrado.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de Forms.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de integración de datos de formulario.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Generate PDF .</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Generate 3D PDF .</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>Necesario para invocar el servicio Administrador de trabajos. </p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Output .</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de Utilidades del PDF o XMP Utilidades.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de extensiones de Acrobat Reader DC.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>Necesario para invocar el servicio Repositorio.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs\thirdparty</p></td>
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
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p><p>Directorio de biblioteca específico de JBoss</p></td>
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

La siguiente tabla enumera los archivos JAR que dependen del modo de conexión y del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

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
   <td><p>si AEM Forms se invoca mediante el modo SOAP, incluya estos archivos JAR.</p> </td>
   <td><p>&lt;<em>directorio de instalación</em>&gt;/sdk/client-libs/thirdparty</p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>si AEM Forms está implementado en JBoss Application Server, incluya este archivo JAR.</p> <p>El cargador de clases no encontrará las clases requeridas si jboss-client.jar y los tarros a los que se hace referencia no están ubicados de manera conjunta.</p> </td>
   <td><p>Directorio de biblioteca de cliente JBoss</p> <p>Si implementa la aplicación cliente en el mismo servidor de aplicaciones J2EE, no es necesario incluir este archivo.</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>si AEM Forms está implementado en BEA WebLogic Server®, incluya este archivo JAR.</p> </td>
   <td><p>Directorio de bibliotecas específico de WebLogic</p> <p>Si implementa la aplicación cliente en el mismo servidor de aplicaciones J2EE, no es necesario incluir este archivo.</p> </td>
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
     <li><p>(com.ibm.ws.webservices.thinclient_6.1.0.jar es necesario para la invocación de servicio web).</p> </li>
    </ul> </td>
   <td><p>Directorio de biblioteca específico de WebSphere (<em>[WAS_HOME]</em>/runtimes)</p> <p>Si implementa la aplicación cliente en el mismo servidor de aplicaciones J2EE, no es necesario incluir estos archivos.</p> </td>
  </tr>
 </tbody>
</table>

### Invocación de escenarios {#invoking-scenarios}

La siguiente tabla especifica las situaciones de invocación y enumera los archivos JAR necesarios para invocar AEM Forms correctamente.

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
   <td><p>Servicio de Forms</p> </td>
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
   <td><p>Servicio de Forms</p> <p>Servicio de extensiones de Acrobat Reader DC</p> <p>Servicio de firmas</p> </td>
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
   <td><p>Servicio de Forms</p> </td>
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
   <td><p>Servicio de Forms</p> <p>Servicio de extensiones de Acrobat Reader DC</p> <p>Servicio de firmas</p> </td>
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

Si está actualizando de LiveCycle a AEM Forms, se recomienda incluir los archivos JAR de AEM Forms en la ruta de clase de su proyecto Java. Por ejemplo, si utiliza servicios como el servicio de Rights Management, tendrá un problema de compatibilidad si no incluye archivos JAR de AEM Forms en la ruta de la clase.

Suponiendo que esté actualizando a AEM Forms. Para utilizar una aplicación Java que invoque el servicio de Rights Management, incluya las versiones de AEM Forms de los siguientes archivos JAR:

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuración de las propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

[Pasar datos a servicios de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Invocación de un servicio mediante una biblioteca de cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Configuración de las propiedades de conexión {#setting-connection-properties}

Las propiedades de conexión se establecen para invocar AEM Forms al utilizar la API de Java. Al configurar las propiedades de conexión, especifique si desea invocar los servicios de forma remota o local, así como el modo de conexión y los valores de autenticación. Los valores de autenticación son necesarios si la seguridad del servicio está habilitada. Sin embargo, si la seguridad del servicio está deshabilitada, no es necesario especificar los valores de autenticación.

El modo de conexión puede ser SOAP o EJB. El modo EJB utiliza el protocolo RMI/IIOP y el rendimiento del modo EJB es mejor que el del modo SOAP. El modo SOAP se utiliza para eliminar una dependencia del servidor de aplicaciones J2EE o cuando se encuentra un firewall entre AEM Forms y la aplicación cliente. El modo SOAP utiliza el protocolo https como transporte subyacente y puede comunicarse a través de los límites del cortafuegos. Si no hay ningún problema con la dependencia del servidor de aplicaciones J2EE o con un cortafuegos, se recomienda utilizar el modo EJB.

Para invocar correctamente un servicio de AEM Forms, establezca las siguientes propiedades de conexión:

* **DSC_DEFAULT_EJB_ENDPOINT:** Si está utilizando el modo de conexión EJB, este valor representa la URL del servidor de aplicaciones J2EE en el que se implementa AEM Forms. Para invocar AEM Forms de forma remota, especifique el nombre del servidor de aplicaciones J2EE en el que se implementa AEM Forms. Si la aplicación cliente está ubicada en el mismo servidor de aplicaciones J2EE, puede especificar `localhost`. Dependiendo del servidor de aplicaciones J2EE en el que se implemente AEM Forms, especifique uno de los siguientes valores:

   * JBoss: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLogic: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**: Si está utilizando el modo de conexión SOAP, este valor representa el punto final al que se envía una solicitud de invocación. Para invocar AEM Forms de forma remota, especifique el nombre del servidor de aplicaciones J2EE en el que se implementa AEM Forms. Si la aplicación cliente está ubicada en el mismo servidor de aplicaciones J2EE, puede especificar `localhost` (por ejemplo, `http://localhost:8080`.)

   * El valor de puerto `8080` es aplicable si la aplicación J2EE es JBoss. Si el servidor de aplicaciones J2EE es IBM® WebSphere®, utilice el puerto `9080`. Del mismo modo, si el servidor de aplicaciones J2EE es WebLogic, utilice el puerto `7001`. (Estos valores son valores de puerto predeterminados. Si cambia el valor del puerto, utilice el número de puerto aplicable).

* **DSC_TRANSPORT_PROTOCOL**: Si está utilizando el modo de conexión EJB, especifique `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` para este valor. Si utiliza el modo de conexión SOAP, especifique `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`.
* **DSC_SERVER_TYPE**: Especifica el servidor de aplicaciones J2EE en el que se implementa AEM Forms. Los valores válidos son `JBoss`, `WebSphere`, `WebLogic`.

   * Si establece esta propiedad de conexión en `WebSphere`, el `java.naming.factory.initial` el valor se establece en `com.ibm.ws.naming.util.WsnInitCtxFactory`.
   * Si establece esta propiedad de conexión en `WebLogic`, el `java.naming.factory.initial` el valor se establece en `weblogic.jndi.WLInitialContextFactory`.
   * Del mismo modo, si establece esta propiedad de conexión en `JBoss`, el `java.naming.factory.initial` el valor se establece en `org.jnp.interfaces.NamingContextFactory`.
   * Puede configurar la variable `java.naming.factory.initial` a un valor que cumpla sus requisitos si no desea utilizar los valores predeterminados.

   >[!NOTE]
   >
   >En lugar de usar una cadena para establecer la variable `DSC_SERVER_TYPE` propiedad connection, puede utilizar un miembro estático de `ServiceClientFactoryProperties` Clase . Se pueden utilizar los siguientes valores: `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`, `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE`o `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`.

* **DSC_CREDENTIAL_USERNAME:** Especifica el nombre de usuario de los formularios AEM. Para que un usuario invoque correctamente un servicio de AEM Forms, necesita la función de usuario de servicios. Un usuario también puede tener otra función que incluya el permiso Invocar servicio. De lo contrario, se genera una excepción cuando intentan invocar un servicio. Si la seguridad del servicio está deshabilitada, no es necesario especificar esta propiedad de conexión.
* **DSC_CREDENTIAL_PASSWORD:** Especifica el valor de contraseña correspondiente. Si la seguridad del servicio está deshabilitada, no es necesario especificar esta propiedad de conexión.
* **DSC_REQUEST_TIMEOUT:** El límite de tiempo de espera predeterminado de la solicitud SOAP es de 120 000 milisegundos (20 minutos). En algún momento, una solicitud puede requerir más tiempo para completar la operación. Por ejemplo, una solicitud SOAP que recupera un gran conjunto de registros puede requerir un límite de tiempo de espera más largo. Puede usar la variable `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` para aumentar el límite de tiempo de espera de llamada de solicitud para las solicitudes SOAP.

   **nota**: Solo las invocaciones basadas en SOAP admiten la propiedad DSC_REQUEST_TIMEOUT.

Para establecer las propiedades de conexión, realice las siguientes tareas:

1. Cree un `java.util.Properties` usando su constructor.
1. Para configurar la variable `DSC_DEFAULT_EJB_ENDPOINT` propiedad connection, invocar `java.util.Properties` del objeto `setProperty` y pase los siguientes valores:

   * La variable `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` valor de enumeración
   * Un valor de cadena que especifica la dirección URL del servidor de aplicaciones J2EE que aloja AEM Forms

   >[!NOTE]
   >
   >Si está utilizando el modo de conexión SOAP, especifique la variable `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` valor de enumeración en lugar de la variable `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` valor de enumeración.

1. Para configurar la variable `DSC_TRANSPORT_PROTOCOL` propiedad connection, invocar `java.util.Properties` del objeto `setProperty` y pase los siguientes valores:

   * La variable `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL` valor de enumeración
   * La variable `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` valor de enumeración

   >[!NOTE]
   >
   >Si está utilizando el modo de conexión SOAP, especifique la variable `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`valor de enumeración en lugar de la variable `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` valor de enumeración.

1. Para configurar la variable `DSC_SERVER_TYPE` propiedad connection, invocar `java.util.Properties` del objeto `setProperty` y pase los siguientes valores:

   * La variable `ServiceClientFactoryProperties.DSC_SERVER_TYPE`valor de enumeración
   * Un valor de cadena que especifica el servidor de aplicaciones J2EE que aloja AEM Forms (por ejemplo, si AEM Forms está implementado en JBoss, especifique `JBoss`).

      1. Para configurar la variable `DSC_CREDENTIAL_USERNAME` propiedad connection, invocar `java.util.Properties` del objeto `setProperty` y pase los siguientes valores:
   * La variable `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME` valor de enumeración
   * Un valor de cadena que especifica el nombre de usuario necesario para invocar AEM Forms

      1. Para configurar la variable `DSC_CREDENTIAL_PASSWORD` propiedad connection, invocar `java.util.Properties` del objeto `setProperty` y pase los siguientes valores:
   * La variable `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD` valor de enumeración
   * Un valor de cadena que especifica el valor de contraseña correspondiente



**Configuración del modo de conexión EJB para JBoss**

El siguiente ejemplo de código Java establece propiedades de conexión para invocar AEM Forms implementado en JBoss y utilizando el modo de conexión EJB.

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

El siguiente ejemplo de código Java establece las propiedades de conexión para invocar AEM Forms implementado en WebLogic y utilizando el modo de conexión EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Configuración del modo de conexión EJB para WebSphere**

El siguiente ejemplo de código Java establece las propiedades de conexión para invocar AEM Forms implementado en WebSphere y utilizando el modo de conexión EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Configuración del modo de conexión SOAP**

El siguiente ejemplo de código Java establece las propiedades de conexión en modo SOAP para invocar AEM Forms implementado en JBoss.

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
>Si selecciona el modo de conexión SOAP, asegúrese de incluir archivos JAR adicionales en la ruta de clase de la aplicación cliente.

**Configuración de las propiedades de conexión cuando está deshabilitada la seguridad del servicio**

El siguiente ejemplo de código Java establece las propiedades de conexión necesarias para invocar AEM Forms implementado en el servidor de aplicaciones JBoss y cuando la seguridad del servicio está deshabilitada.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>Todos los inicios rápidos de Java asociados con la programación con AEM Forms muestran la configuración de conexión EJB y SOAP.

**Configuración del modo de conexión SOAP con límite de tiempo de espera de solicitud personalizado**

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**Uso de un objeto de contexto para invocar AEM Forms**

Puede usar un `com.adobe.idp.Context` para invocar un servicio de AEM Forms con un usuario autenticado (la variable `com.adobe.idp.Context` representa un usuario autenticado). Al usar un `com.adobe.idp.Context` , no es necesario configurar la variable `DSC_CREDENTIAL_USERNAME` o `DSC_CREDENTIAL_PASSWORD` propiedades. Puede obtener una `com.adobe.idp.Context` al crear usuarios mediante la `AuthenticationManagerServiceClient` del objeto `authenticate` método.

La variable `authenticate` devuelve un valor `AuthResult` que contiene los resultados de la autenticación. Puede crear un `com.adobe.idp.Context` invocando su constructor. A continuación, invoque el `com.adobe.idp.Context` del objeto `initPrincipal` y pase el `AuthResult` como se muestra en el siguiente código:

```java
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

En lugar de configurar la variable `DSC_CREDENTIAL_USERNAME` o `DSC_CREDENTIAL_PASSWORD` propiedades, puede invocar la variable `ServiceClientFactory` del objeto `setContext` y pase el `com.adobe.idp.Context` objeto. Cuando utilice un usuario de AEM formularios para invocar un servicio, asegúrese de que tenga la función denominada `Services User` que es necesario para invocar un servicio de AEM Forms.

El siguiente ejemplo de código muestra cómo utilizar un `com.adobe.idp.Context` dentro de la configuración de conexión que se utiliza para crear un `EncryptionServiceClient` objeto.

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
>Para obtener todos los detalles sobre la autenticación de un usuario, consulte [Autenticar usuarios](/help/forms/developing/users.md#authenticating-users).

### Invocación de escenarios {#invoking_scenarios-1}

En esta sección se tratan los siguientes casos de invocación:

* Una aplicación cliente que se ejecuta en su propia máquina virtual Java (JVM) invoca una instancia AEM Forms independiente.
* Una aplicación cliente que se ejecuta en su propia JVM invoca instancias de AEM Forms agrupadas.

### Aplicación de cliente que invoca una instancia de AEM Forms independiente {#client-application-invoking-a-stand-alone-aem-forms-instance}

El diagrama siguiente muestra una aplicación cliente que se ejecuta en su propia JVM e invoca una instancia independiente de AEM Forms.

En este escenario, una aplicación cliente se ejecuta en su propia JVM e invoca los servicios de AEM Forms.

>[!NOTE]
>
>Este escenario es el escenario de invocación en el que se basan todos los inicios rápidos.

### Aplicación de cliente que invoca instancias de AEM Forms agrupadas {#client-application-invoking-clustered-aem-forms-instances}

El diagrama siguiente muestra una aplicación cliente que se ejecuta en su propia JVM e invoca instancias de AEM Forms ubicadas en un clúster.

Este escenario es similar a una aplicación cliente que invoca una instancia de AEM Forms independiente. Sin embargo, la dirección URL del proveedor es diferente. Si una aplicación cliente desea conectarse a un servidor de aplicaciones J2EE específico, la aplicación debe cambiar la URL para hacer referencia al servidor de aplicaciones J2EE específico.

No se recomienda hacer referencia a un servidor de aplicaciones J2EE específico porque la conexión entre la aplicación cliente y AEM Forms termina si el servidor de aplicaciones se detiene. Se recomienda que la URL del proveedor haga referencia a un administrador de JNDI a nivel de celda, en lugar de a un servidor de aplicaciones J2EE específico.

Las aplicaciones cliente que utilizan el modo de conexión SOAP pueden utilizar el puerto de equilibrador de carga HTTP para el clúster. Las aplicaciones cliente que utilizan el modo de conexión EJB pueden conectarse al puerto EJB de un servidor de aplicaciones J2EE específico. Esta acción gestiona el equilibrio de carga entre los nodos del clúster.

**WebSphere**

El siguiente ejemplo muestra el contenido de un archivo jndi.properties que se utiliza para conectarse a AEM Forms y que se implementa en WebSphere.

```ini
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**WebLogic**

El siguiente ejemplo muestra el contenido de un archivo jndi.properties que se utiliza para conectarse a AEM Forms que se implementa en WebLogic.

```ini
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

El siguiente ejemplo muestra el contenido de un archivo jndi.properties que se utiliza para conectarse a AEM Forms y que se implementa en JBoss.

```ini
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>Consulte con su administrador para determinar el nombre y el número de puerto del servidor de aplicaciones J2EE.

**Consulte también lo siguiente**

[Inclusión de archivos de biblioteca Java de AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Pasar datos a servicios de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Invocación de un servicio mediante una biblioteca de cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Pasar datos a servicios de AEM Forms mediante la API de Java {#passing-data-to-aem-forms-services-using-the-java-api}

Las operaciones de servicio de AEM Forms suelen consumir o producir documentos PDF. Al invocar un servicio, a veces es necesario pasar un documento PDF (u otros tipos de documento como datos XML) al servicio. Del mismo modo, a veces es necesario gestionar un documento PDF que se devuelve del servicio. La clase Java que le permite pasar datos desde y hacia los servicios de AEM Forms es `com.adobe.idp.Document`.

Los servicios de AEM Forms no aceptan un documento de PDF como otros tipos de datos, como un `java.io.InputStream` o una matriz de bytes. A `com.adobe.idp.Document` también se puede utilizar para pasar otros tipos de datos, como datos XML, a servicios.

A `com.adobe.idp.Document` es un tipo serializable de Java, por lo que se puede pasar a través de una llamada de RMI. El lado receptor puede estar ubicado en el mismo lugar (mismo host, mismo cargador de clase), local (mismo host, diferente cargador de clase) o remoto (diferente host). El paso del contenido del documento está optimizado para cada caso. Por ejemplo, si el remitente y el receptor están ubicados en el mismo host, el contenido se pasa a través de un sistema de archivos local. (En algunos casos, los documentos se pueden pasar en la memoria).

Según el `com.adobe.idp.Document` tamaño del objeto, los datos se transmiten dentro de la variable `com.adobe.idp.Document` o se almacenan en el sistema de archivos del servidor. Cualquier recurso de almacenamiento temporal ocupado por el `com.adobe.idp.Document` se quitan automáticamente al `com.adobe.idp.Document` eliminación. (Consulte [Eliminación de objetos de documento](invoking-aem-forms-using-java.md#disposing-document-objects).)

A veces es necesario conocer el tipo de contenido de un `com.adobe.idp.Document` para poder pasarlo a un servicio. Por ejemplo, si una operación requiere un tipo de contenido específico, como `application/pdf`, se recomienda determinar el tipo de contenido. (Consulte [Determinación del tipo de contenido de un documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document).)

La variable `com.adobe.idp.Document` intenta determinar el tipo de contenido utilizando los datos suministrados. Si no se puede recuperar el tipo de contenido de los datos suministrados (por ejemplo, cuando los datos se suministraron como una matriz de bytes), defina el tipo de contenido. Para establecer el tipo de contenido, invoque la variable `com.adobe.idp.Document` del objeto `setContentType` método. (Consulte [Determinación del tipo de contenido de un documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

Si los archivos colaterales residen en el mismo sistema de archivos, se crea una `com.adobe.idp.Document` es más rápido. Si los archivos colaterales residen en sistemas de archivos remotos, se debe realizar una operación de copia, lo que afecta al rendimiento.

Una aplicación puede contener ambos `com.adobe.idp.Document` y `org.w3c.dom.Document` tipos de datos. Sin embargo, asegúrese de que cumple todos los requisitos para la variable `org.w3c.dom.Document` tipo de datos. Para obtener información sobre cómo convertir una `org.w3c.dom.Document` a `com.adobe.idp.Document` objeto, consulte [Inicio rápido (modo EJB): Rellenado previo de Forms con diseños flexibles mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api).

>[!NOTE]
>
>Para evitar una fuga de memoria en WebLogic al utilizar un `com.adobe.idp.Document` lea la información del documento en fragmentos de 2048 bytes o menos. Por ejemplo, el siguiente código lee la información del documento en trozos de 2048 bytes:

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

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuración de las propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

### Creación de documentos {#creating-documents}

Cree un `com.adobe.idp.Document` antes de invocar una operación de servicio que requiere un documento de PDF (u otros tipos de documento) como valor de entrada. La variable `com.adobe.idp.Document` proporciona constructores que permiten crear un documento a partir de los siguientes tipos de contenido:

* Matriz de bytes
* Una `com.adobe.idp.Document` object
* A `java.io.File` object
* A `java.io.InputStream` object
* A `java.net.URL` object

#### Creación de un documento basado en una matriz de bytes {#creating-a-document-based-on-a-byte-array}

El siguiente ejemplo de código crea una `com.adobe.idp.Document` objeto basado en una matriz de bytes.

**Creación de un objeto Document basado en una matriz de bytes**

```java
 Document myPDFDocument = new Document(myByteArray);
```

#### Creación de un documento basado en otro documento {#creating-a-document-based-on-another-document}

El siguiente ejemplo de código crea una `com.adobe.idp.Document` objeto basado en otro `com.adobe.idp.Document` objeto.

**Creación de un objeto Document basado en otro documento**

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

El siguiente ejemplo de código crea una `com.adobe.idp.Document` objeto basado en un archivo PDF denominado *map.pdf*. Este archivo se encuentra en la raíz del disco duro C. Este constructor intenta establecer el tipo de contenido MIME de la variable `com.adobe.idp.Document` con la extensión de nombre de archivo.

La variable `com.adobe.idp.Document` constructor que acepta un `java.io.File` también acepta un parámetro booleano. Si establece este parámetro en `true`, el `com.adobe.idp.Document` elimina el archivo. Esta acción significa que no es necesario eliminar el archivo después de pasarlo a la `com.adobe.idp.Document` constructor.

Configuración de este parámetro en `false` significa que se mantiene la propiedad de este archivo. Configuración de este parámetro en `true` es más eficiente. La razón es porque la variable `com.adobe.idp.Document` puede mover el archivo directamente al área local administrada en lugar de copiarlo (lo que es más lento).

**Creación de un objeto Document basado en un archivo PDF**

```java
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### Creación de un documento basado en un objeto InputStream {#creating-a-document-based-on-an-inputstream-object}

El siguiente ejemplo de código Java crea una `com.adobe.idp.Document` objeto basado en un `java.io.InputStream` objeto.

**Creación de un documento basado en un objeto InputStream**

```java
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### Creación de un documento basado en contenido accesible desde una dirección URL {#creating-a-document-based-on-content-accessible-from-an-url}

El siguiente ejemplo de código Java crea una `com.adobe.idp.Document` objeto basado en un archivo PDF denominado *map.pdf*. Este archivo se encuentra dentro de una aplicación web denominada `WebApp` que se está ejecutando en `localhost`. Este constructor intenta establecer la variable `com.adobe.idp.Document` tipo de contenido MIME del objeto que utiliza el tipo de contenido devuelto con el protocolo URL.

La URL proporcionada a la variable `com.adobe.idp.Document` siempre se lee en el lateral donde se encuentra el objeto original `com.adobe.idp.Document` se crea, como se muestra en este ejemplo:

```java
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

El archivo c:/temp/input.pdf debe estar ubicado en el equipo cliente (no en el equipo servidor). El equipo cliente es el lugar donde se lee la dirección URL y donde se lee la `com.adobe.idp.Document` se creó.

**Creación de un documento basado en contenido accesible desde una dirección URL**

```java
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuración de las propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

### Gestión de documentos devueltos {#handling-returned-documents}

Las operaciones de servicio que devuelven un documento de PDF (u otros tipos de datos, como datos XML) como valor de salida devuelven un valor `com.adobe.idp.Document` objeto. Después de recibir un `com.adobe.idp.Document` , puede convertirlo a los siguientes formatos:

* A `java.io.File` object
* A `java.io.InputStream` object
* Matriz de bytes

La siguiente línea de código convierte un `com.adobe.idp.Document` a `java.io.InputStream` objeto. Supongamos que `myPDFDocument` representa un `com.adobe.idp.Document` objeto:

```java
     java.io.InputStream resultStream = myDocument.getInputStream();
```

Del mismo modo, puede copiar el contenido de un `com.adobe.idp.Document` a un archivo local realizando las siguientes tareas:

1. Cree un `java.io.File` objeto.
1. Invocar el `com.adobe.idp.Document` del objeto `copyToFile` y pase el `java.io.File`objeto.

El siguiente ejemplo de código copia el contenido de un `com.adobe.idp.Document` a un archivo denominado *AnotherMap.pdf*.

**Copia del contenido de un objeto de documento en un archivo**

```java
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuración de las propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinación del tipo de contenido de un documento {#determining-the-content-type-of-a-document}

Determine el tipo MIME de un `com.adobe.idp.Document` invocando el objeto `com.adobe.idp.Document` del objeto `getContentType` método. Este método devuelve un valor de cadena que especifica el tipo de contenido de la variable `com.adobe.idp.Document` objeto. En la tabla siguiente se describen los diferentes tipos de contenido que devuelve AEM Forms.

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
   <td><p>documento del PDF</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xdp+xml</code></p></td>
   <td><p>Paquete de datos XML (XDP), que se utiliza para formularios exportados de XML Forms Architecture (XFA)</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>Marcadores, archivos adjuntos u otros documentos XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>Formato de datos de Forms (FDF), que se utiliza para formularios Acrobat exportados</p></td>
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

El siguiente ejemplo de código determina el tipo de contenido de un `com.adobe.idp.Document` objeto.

**Determinación del tipo de contenido de un objeto Document**

```java
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuración de las propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminación de objetos de documento {#disposing-document-objects}

Cuando ya no necesite un `Document` , se recomienda eliminarlo invocando su `dispose` método. Cada `Document` consume un descriptor de archivo y hasta 75 MB de espacio RAM en la plataforma host de la aplicación. Si `Document` no se ha eliminado, el proceso de recopilación de Java Garage lo elimina. Sin embargo, eliminándolo antes, usando la variable `dispose` , puede liberar la memoria ocupada por el `Document` objeto.

**Consulte también lo siguiente**

[Invocación de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Invocación de un servicio mediante una biblioteca de cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Invocación de un servicio mediante una biblioteca de cliente Java {#invoking-a-service-using-a-java-client-library}

Las operaciones del servicio AEM Forms se pueden invocar utilizando la API con establecimiento inflexible de tipos de un servicio, conocida como biblioteca de cliente Java. A *Biblioteca de cliente Java* es un conjunto de clases concretas que proporcionan acceso a los servicios implementados en el contenedor de servicios. Cree una instancia de un objeto Java que represente el servicio que se va a invocar en lugar de crear una `InvocationRequest` mediante la API de invocación. La API de invocación se utiliza para invocar procesos, como procesos de larga duración, creados en Workbench. (Consulte [Invocación de procesos de larga vida centrados en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

Para realizar una operación de servicio, invoque un método que pertenezca al objeto Java. Una biblioteca de cliente Java contiene métodos que normalmente asignan una a una con operaciones de servicio. Cuando utilice una biblioteca de cliente Java, establezca las propiedades de conexión necesarias. (Consulte [Configuración de las propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties).)

Después de establecer las propiedades de conexión, cree una `ServiceClientFactory` objeto que se utiliza para crear una instancia de un objeto Java que le permita invocar un servicio. Cada servicio que tiene una biblioteca de cliente Java tiene un objeto cliente correspondiente. Por ejemplo, para invocar el servicio Repositorio, cree un `ResourceRepositoryClient` usando su constructor y pasando el `ServiceClientFactory` objeto. La variable `ServiceClientFactory` es responsable de mantener la configuración de conexión necesaria para invocar los servicios de AEM Forms.

Aunque obtiene un `ServiceClientFactory` normalmente es rápido, se incurre en cierta sobrecarga cuando se utiliza por primera vez la fábrica. Este objeto está optimizado para su reutilización y, por lo tanto, cuando sea posible, utilice el mismo `ServiceClientFactory` cuando esté creando varios objetos de cliente Java. Es decir, no cree un `ServiceClientFactory` para cada objeto de biblioteca de cliente que cree.

Existe una configuración del Administrador de usuarios que controla la duración de la afirmación de SAML que se encuentra dentro de la variable `com.adobe.idp.Context` objeto que afecta a la variable `ServiceClientFactory` objeto. Esta configuración controla todas las duraciones del contexto de autenticación en AEM Forms, incluidas todas las invocaciones realizadas mediante la API de Java. De forma predeterminada, el periodo de tiempo en el que una `ServiceCleintFactory` se puede utilizar en dos horas.

>[!NOTE]
>
>Para explicar cómo invocar un servicio utilizando la API de Java, el servicio Repositorio de `writeResource` se invoca a . Esta operación coloca un nuevo recurso en el repositorio.

Puede invocar el servicio Repositorio utilizando una biblioteca de cliente Java y realizando los siguientes pasos:

1. Incluya archivos JAR del cliente, como adobe-repository-client.jar, en la ruta de clase de su proyecto Java. Para obtener información sobre la ubicación de estos archivos, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).
1. Establezca las propiedades de conexión necesarias para invocar un servicio.
1. Cree un `ServiceClientFactory` invocando el objeto `ServiceClientFactory` estático del objeto `createInstance` y pasando el `java.util.Properties` objeto que contiene propiedades de conexión.
1. Cree un `ResourceRepositoryClient` usando su constructor y pasando el `ServiceClientFactory` objeto. Utilice la variable `ResourceRepositoryClient` para invocar operaciones de servicio de Repositorio.
1. Cree un `RepositoryInfomodelFactoryBean` mediante el uso de su constructor y pase `null`. Este objeto permite crear un `Resource` que representa el contenido que se agrega al repositorio.
1. Cree un `Resource` invocando el objeto `RepositoryInfomodelFactoryBean` del objeto `newImage` y pasando los siguientes valores:

   * Un valor de ID único especificando `new Id()`.
   * Un valor UUID único especificando `new Lid()`.
   * Nombre del recurso. Puede especificar el nombre del archivo XDP.

   Conversión del valor devuelto a `Resource`.

1. Cree un `ResourceContent` invocando el objeto `RepositoryInfomodelFactoryBean` del objeto `newImage` y convertir el valor devuelto a `ResourceContent`. Este objeto representa el contenido que se agrega al repositorio.
1. Cree un `com.adobe.idp.Document` objeto pasando un `java.io.FileInputStream` que almacena el archivo XDP que se agregará al repositorio. (Consulte [Creación de un documento basado en un objeto InputStream](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object).)
1. Añada el contenido del `com.adobe.idp.Document` al `ResourceContent` invocando el objeto `ResourceContent` del objeto `setDataDocument` método. Pase el `com.adobe.idp.Document` objeto.
1. Establezca el tipo MIME del archivo XDP que desea agregar al repositorio invocando la variable `ResourceContent` del objeto `setMimeType` método y paso `application/vnd.adobe.xdp+xml`.
1. Añada el contenido del `ResourceContent` al `Resource` invocando el objeto `Resource` objeto ‘s `setContent` y pasando el `ResourceContent` objeto.
1. Añada una descripción del recurso invocando la variable `Resource` objeto ‘s `setDescription` y pasando un valor de cadena que representa una descripción del recurso.
1. Agregue el diseño de formulario al repositorio invocando la variable `ResourceRepositoryClient` del objeto `writeResource` y pasando los siguientes valores:

   * Un valor de cadena que especifica la ruta a la colección de recursos que contiene el nuevo recurso
   * La variable `Resource` objeto creado

**Consulte también lo siguiente**

[Inicio rápido (modo EJB): Escritura de un recurso mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Invocación de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## Invocación de un proceso de corta duración mediante la API de invocación {#invoking-a-short-lived-process-using-the-invocation-api}

Puede invocar un proceso de corta duración mediante la API de invocación de Java. Cuando se invoca un proceso de corta duración mediante la API de invocación, se pasan los valores de parámetro necesarios mediante una `java.util.HashMap` objeto. Para que cada parámetro pase a un servicio, invoque la variable `java.util.HashMap` del objeto `put` y especifique el par nombre-valor que requiere el servicio para realizar la operación especificada. Especifique el nombre exacto de los parámetros que pertenecen al proceso de corta duración.

>[!NOTE]
>
>Para obtener información sobre cómo invocar un proceso de larga duración, consulte [Invocación de procesos de larga vida centrados en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

La discusión aquí es sobre el uso de la API de invocación para invocar el siguiente proceso breve de AEM Forms llamado `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para seguir con el ejemplo de código, cree un proceso denominado `MyApplication/EncryptDocument` usando Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento PDF no protegido que se pasa al proceso. Esta acción se basa en la variable `SetValue` operación. El parámetro de entrada para este proceso es un `document` variable de proceso denominada `inDoc`.
1. Codifica el documento del PDF con una contraseña. Esta acción se basa en la variable `PasswordEncryptPDF` operación. El documento del PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

### Invocar el proceso breve MyApplication/EncryptDocument usando la API de invocación de Java {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

Invocar el `MyApplication/EncryptDocument` proceso breve mediante la API de invocación de Java:

1. Incluya archivos JAR del cliente, como adobe-livecycle-client.jar, en la ruta de clase de su proyecto Java. (Consulte [Inclusión de archivos de biblioteca Java de AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)
1. Cree un `ServiceClientFactory` objeto que contiene propiedades de conexión. (Consulte [Configuración de las propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties).)
1. Cree un `ServiceClient` usando su constructor y pasando el `ServiceClientFactory` objeto. A `ServiceClient` permite invocar una operación de servicio. Gestiona tareas como la localización, el envío y las solicitudes de invocación de enrutamiento.
1. Cree un `java.util.HashMap` usando su constructor.
1. Invocar el `java.util.HashMap` del objeto `put` para que cada parámetro de entrada pase al proceso de larga duración. Porque la variable `MyApplication/EncryptDocument` el proceso de corta duración requiere un parámetro de entrada de tipo `Document`, solo tiene que invocar la variable `put` método una vez, como se muestra en el siguiente ejemplo.

   ```java
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. Cree un `InvocationRequest` invocando el objeto `ServiceClientFactory` del objeto `createInvocationRequest` y pasando los siguientes valores:

   * Un valor de cadena que especifica el nombre del proceso de larga duración que se va a invocar. Para invocar la variable `MyApplication/EncryptDocument` procesar, especificar `MyApplication/EncryptDocument`.
   * Valor de cadena que representa el nombre de la operación de proceso. Normalmente, el nombre de una operación de proceso de corta duración es `invoke`.
   * La variable `java.util.HashMap` que contiene los valores de parámetro que requiere la operación de servicio.
   * Un valor booleano que especifica `true`, que crea una solicitud sincrónica (este valor se aplica para invocar un proceso de corta duración).

1. Envíe la solicitud de invocación al servicio invocando el `ServiceClient` del objeto `invoke` y pasando el `InvocationRequest` objeto. La variable `invoke` devuelve un valor `InvocationReponse` objeto.

   >[!NOTE]
   >
   >Se puede invocar un proceso de larga duración pasando el valor `false`como cuarto parámetro de la función `createInvocationRequest` método. Paso del valor `false`*crea una solicitud asincrónica.*

1. Recupere el valor devuelto del proceso invocando la variable `InvocationReponse` del objeto `getOutputParameter` y pasando un valor de cadena que especifica el nombre del parámetro de salida. En este caso, especifique `outDoc` ( `outDoc` es el nombre del parámetro de salida para la variable `MyApplication/EncryptDocument` proceso). Conversión del valor devuelto a `Document`, como se muestra en el siguiente ejemplo.

   ```java
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. Cree un `java.io.File` y asegúrese de que la extensión de archivo es .pdf.
1. Invocar el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `com.adobe.idp.Document` al archivo. Asegúrese de usar la variable `com.adobe.idp.Document` objeto devuelto por el `getOutputParameter` método.

**Consulte también lo siguiente**

[Inicio rápido: Invocación de un proceso de corta duración mediante la API de invocación](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[Invocación de procesos de larga vida centrados en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Inclusión de archivos de biblioteca Java de AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
