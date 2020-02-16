---
title: Invocación de AEM Forms mediante JavaAPI
seo-title: Invocación de AEM Forms mediante JavaAPI
description: nulo
seo-description: nulo
uuid: 5e2fef2a-05f3-4283-8fd3-2d7dca411000
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0e6e7850-6137-42c5-b8e2-d4e352fddae2
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Invocación de AEM Forms mediante la API de Java {#invoking-aem-forms-using-the-javaapi}

Los formularios AEM se pueden invocar mediante la API Java de AEM Forms. Al utilizar la API de Java de AEM Forms, puede utilizar la API de invocación o las bibliotecas de cliente Java. Las bibliotecas de cliente Java están disponibles para servicios como el servicio Rights Management. Estas API con establecimiento inflexible de tipos permiten desarrollar aplicaciones Java que invocan AEM Forms.

La API de invocación son clases que se encuentran en el `com.adobe.idp.dsc` paquete. Con estas clases, puede enviar una solicitud de invocación directamente a un servicio y gestionar una respuesta de invocación que se devuelve. Utilice la API de invocación para invocar procesos de corta duración o de larga duración creados mediante Workbench.

La forma recomendada de invocar mediante programación un servicio es utilizar una biblioteca de cliente Java que corresponda al servicio en lugar de la API de invocación. Por ejemplo, para invocar el servicio Cifrado, utilice la biblioteca del cliente del servicio Cifrado. Para realizar una operación de servicio de cifrado, invoque un método que pertenece al objeto cliente del servicio de cifrado. Puede cifrar un documento PDF con una contraseña invocando el `EncryptionServiceClient` método `encryptPDFUsingPassword` del objeto.

La API de Java admite las siguientes funciones:

* Protocolo de transporte RMI para invocación remota
* Transporte de VM para invocación local
* SOAP para invocación remota
* Distinta autenticación, como nombre de usuario y contraseña
* Solicitudes de invocación sincrónicas y asincrónicas

**Sitio web de Adobe Developer**

El sitio web de desarrolladores de Adobe contiene los siguientes artículos en los que se explica cómo invocar los servicios de AEM Forms mediante la API de Java:

[Uso de servlets de Java para invocar procesos de AEM Forms](https://www.adobe.com/devnet/livecycle/articles/java_servlets.html)

[Invocación de la API de AEM Forms Distiller desde Java](https://www.adobe.com/devnet/livecycle/articles/distiller_java_03.html)

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](#including-aem-forms-java-library-files)

[Invocar procesos de larga vida centrados en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#main-pars-text-0)

[Invocación de AEM Forms mediante servicios Web](/help/forms/developing/invoking-aem-forms-using-web.md)

[Configuración de las propiedades de conexión](#setting-connection-properties)

[Pasar datos a los servicios de AEM Forms mediante la API de Java](#passing-data-to-aem-forms-services-using-the-java-api)

[Invocación de un servicio mediante una biblioteca de cliente Java](#invoking-a-service-using-a-java-client-library)

[Invocación de un proceso de corta duración mediante la API de invocación](#invoking-a-short-lived-process-using-the-invocation-api)

[Creación de una aplicación web de Java que invoque un proceso prolongado centrado en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md)

## Inclusión de archivos de biblioteca Java de AEM Forms {#including-aem-forms-java-library-files}

Para invocar mediante programación un servicio de AEM Forms mediante la API de Java, incluya los archivos de biblioteca necesarios (archivos JAR) en la ruta de clases del proyecto Java. Los archivos JAR que se incluyen en la ruta de clases de la aplicación cliente dependen de varios factores:

* El servicio AEM Forms que se va a invocar. Una aplicación cliente puede invocar uno o más servicios.
* Modo en el que desea invocar un servicio de AEM Forms. Puede utilizar el modo EJB o SOAP. (Consulte [Configuración de propiedades](invoking-aem-forms-using-java.md#setting-connection-properties)de conexión).
* Servidor de aplicaciones J2EE en el que se implementa AEM Forms.

### Archivos JAR específicos del servicio {#service-specific-jar-files}

En la tabla siguiente se muestran los archivos JAR necesarios para invocar los servicios de AEM Forms.

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
   <td><p>Siempre debe incluirse en la ruta de clases de una aplicación cliente Java.</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>Siempre debe incluirse en la ruta de clases de una aplicación cliente Java.</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>Siempre debe incluirse en la ruta de clases de una aplicación cliente Java.</p></td>
   <td><p>&lt;directorio<i>de</i>instalación&gt;/sdk//client-libs/&lt;servidor de aplicaciones&gt;</p></td>
  </tr>
  <tr>
   <td><p>adobe-application-manager-client-sdk.jar</p></td>
   <td><p>Necesario para invocar el servicio Application Manager.</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Ensamblador. </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>Necesario para invocar la API de servicio de copia de seguridad y restauración.</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de formularios con códigos de barras. </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Convertir PDF. </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Distiller.</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>Necesario para invocar el servicio DocConverter.</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de Document Management.</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-encoding-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de cifrado.</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Forms.</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de integración de datos de formulario.</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Generar PDF.</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Generar PDF 3D.</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>Necesario para invocar el servicio de Job Manager. </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Output.</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Utilidades de PDF o Utilidades XMP.</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-Extensions-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de extensiones de Acrobat Reader DC.</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>Necesario para invocar el servicio Repositorio.</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p><p>&lt;<i>install directory</i>&gt;/sdk/client-libs\thirdparty</p></td>
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
     <li><p>relajngDataType.jar</p></li>
     <li><p>xsdlib.jar</p></li>
    </ul></td>
   <td><p>Necesario para invocar el servicio Rights Management.</p><p>Si AEM Forms se implementa en JBoss, incluya todos estos archivos. </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p><p>Directorio de biblioteca específica de JBoss</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Signature.</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>Necesario para invocar el servicio Administrador de tareas. </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-trust-store-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de almacén de confianza. </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
 </tbody>
</table>

### Modo de conexión y archivos JAR de la aplicación J2EE {#connection-mode-and-j2ee-application-jar-files}

En la tabla siguiente se muestran los archivos JAR que dependen del modo de conexión y del servidor de aplicaciones J2EE en el que se implementa AEM Forms.

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
     <li><p>commons-collection-3.1.jar</p> </li>
     <li><p>commons-discover.jar</p> </li>
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
   <td><p>si se invoca AEM Forms mediante el modo SOAP, incluya estos archivos JAR.</p> </td>
   <td><p>&lt;<em>install directory</em>&gt;/sdk/client-libs/thirdparty</p> </td>
  </tr>
  <tr>
   <td><p> jpatrón-client.jar</p> </td>
   <td><p>si AEM Forms se implementa en JBoss Application Server, incluya este archivo JAR.</p> <p>Las clases requeridas no serán encontradas por el cargador de clase si jpatrón-client.jar y las tarros a las que se hace referencia no están ubicadas de manera conjunta.</p> </td>
   <td><p>Directorio de biblioteca de cliente JBoss</p> <p>Si implementa la aplicación cliente en el mismo servidor de aplicaciones J2EE, no es necesario incluir este archivo.</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>si AEM Forms se implementa en BEA WebLogic Server®, incluya este archivo JAR.</p> </td>
   <td><p>Directorio de bibliotecas específicas de WebLogic</p> <p>Si implementa la aplicación cliente en el mismo servidor de aplicaciones J2EE, no es necesario incluir este archivo.</p> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>com.ibm.ws.admin.client_6.1.0.jar</p> </li>
     <li><p>com.ibm.ws.webservices.thinclient_6.1.0.jar</p> </li>
    </ul> </td>
   <td>
    <ul>
     <li><p>si AEM Forms se implementa en WebSphere Application Server, incluya estos archivos JAR.</p> </li>
     <li><p>(Se requiere com.ibm.ws.webservices.thinclient_6.1.0.jar para la invocación de servicio Web).</p> </li>
    </ul> </td>
   <td><p>Directorio de biblioteca específico de WebSphere (<em>[WAS_HOME]</em>/runtimes)</p> <p>Si implementa la aplicación cliente en el mismo servidor de aplicaciones J2EE, no es necesario incluir estos archivos.</p> </td>
  </tr>
 </tbody>
</table>

### Invocación de escenarios {#invoking-scenarios}

En la tabla siguiente se especifican los escenarios de invocación y se enumeran los archivos JAR necesarios para invocar correctamente los formularios AEM.

<table>
 <thead>
  <tr>
   <th><p>Servicios</p> </th>
   <th><p>Modo de invocación</p> </th>
   <th><p>Servidor de aplicaciones J2EE</p> </th>
   <th><p>Archivos JAR requeridos</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td><p>Servicio de formularios</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jpatrón-client.jar</li>
    </ul>
    <ul>
     <li>adobe-forms-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Servicio de formularios</p> <p>Servicio de extensiones de Acrobat Reader DC</p> <p>Servicio de firmas</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jpatrón-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul>
    <ul>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-Extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Servicio de formularios</p> </td>
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
     <li><p>commons-collection-3.1.jar</p> </li>
     <li><p>commons-discover.jar</p> </li>
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
   <td><p>Servicio de formularios</p> <p>Servicio de extensiones de Acrobat Reader DC</p> <p>Servicio de firmas</p> </td>
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
     <li><p>commons-collection-3.1.jar</p> </li>
     <li><p>commons-discover.jar</p> </li>
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
     <li><p>adobe-reader-Extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr> xmp-uti
 </tbody>
</table>

### Actualización de archivos JAR {#upgrading-jar-files}

Si va a actualizar de LiveCycle a AEM Forms, se recomienda incluir los archivos JAR de AEM Forms en la ruta de clases del proyecto Java. Por ejemplo, si está utilizando servicios como el servicio Rights Management, encontrará un problema de compatibilidad si no incluye archivos JAR de AEM Forms en la ruta de clases.

Suponiendo que está actualizando a AEM Forms. Para utilizar una aplicación Java que invoque el servicio Rights Management, incluya las versiones de AEM Forms de los siguientes archivos JAR:

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**Consulte también**

[Invocación de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuración de las propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

[Pasar datos a los servicios de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Invocación de un servicio mediante una biblioteca de cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Configuración de las propiedades de conexión {#setting-connection-properties}

Las propiedades de conexión se establecen para invocar AEM Forms al utilizar la API de Java. Al establecer las propiedades de conexión, especifique si desea invocar los servicios de forma remota o local, así como el modo de conexión y los valores de autenticación. Los valores de autenticación son obligatorios si la seguridad del servicio está habilitada. Sin embargo, si la seguridad del servicio está deshabilitada, no es necesario especificar los valores de autenticación.

El modo de conexión puede ser SOAP o EJB. El modo EJB utiliza el protocolo RMI/IIOP y el rendimiento del modo EJB es mejor que el del modo SOAP. El modo SOAP se utiliza para eliminar una dependencia del servidor de aplicaciones J2EE o cuando se encuentra un servidor de seguridad entre AEM Forms y la aplicación cliente. El modo SOAP utiliza el protocolo https como transporte subyacente y puede comunicarse a través de los límites del cortafuegos. Si no hay ningún problema con la dependencia del servidor de aplicaciones J2EE o con un servidor de seguridad, se recomienda utilizar el modo EJB.

Para invocar correctamente un servicio de AEM Forms, defina las siguientes propiedades de conexión:

* **** DSC_DEFAULT_EJB_ENDPOINT: Si utiliza el modo de conexión EJB, este valor representa la URL del servidor de aplicaciones J2EE en el que se implementa AEM Forms. Para invocar AEM Forms de forma remota, especifique el nombre del servidor de aplicaciones J2EE en el que se implementa AEM Forms. Si la aplicación cliente se encuentra en el mismo servidor de aplicaciones J2EE, puede especificar `localhost`. En función de la implementación de AEM Forms en el servidor de aplicaciones J2EE, especifique uno de los siguientes valores:

   * JBoss: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLogic: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**: Si utiliza el modo de conexión SOAP, este valor representa el punto final al que se envía una solicitud de invocación. Para invocar AEM Forms de forma remota, especifique el nombre del servidor de aplicaciones J2EE en el que se implementa AEM Forms. Si la aplicación cliente se encuentra en el mismo servidor de aplicaciones J2EE, puede especificar `localhost` (por ejemplo, `http://localhost:8080`.)

   * El valor del puerto `8080` es aplicable si la aplicación J2EE es JBoss. Si el servidor de aplicaciones J2EE es IBM® WebSphere®, utilice el puerto `9080`. Del mismo modo, si el servidor de aplicaciones J2EE es WebLogic, utilice el puerto `7001`. (Estos valores son valores de puerto predeterminados. Si cambia el valor del puerto, utilice el número de puerto correspondiente).

* **DSC_TRANSPORT_PROTOCOL**: Si está utilizando el modo de conexión EJB, especifique `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` para este valor. Si está utilizando el modo de conexión SOAP, especifique `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`.
* **DSC_SERVER_TYPE**: Especifica el servidor de aplicaciones J2EE en el que se implementa AEM Forms. Los valores válidos son `JBoss`, `WebSphere`, `WebLogic`.

   * Si establece esta propiedad de conexión en `WebSphere`, el `java.naming.factory.initial` valor se establece en `com.ibm.ws.naming.util.WsnInitCtxFactory`.
   * Si establece esta propiedad de conexión en `WebLogic`, el `java.naming.factory.initial` valor se establece en `weblogic.jndi.WLInitialContextFactory`.
   * Del mismo modo, si establece esta propiedad de conexión en `JBoss`, el `java.naming.factory.initial` valor se establece en `org.jnp.interfaces.NamingContextFactory`.
   * Puede establecer la `java.naming.factory.initial` propiedad en un valor que cumpla sus requisitos si no desea utilizar los valores predeterminados.
   ***Nota**: En lugar de utilizar una cadena para establecer la propiedad de `DSC_SERVER_TYPE` conexión, puede utilizar un miembro estático de la `ServiceClientFactoryProperties` clase. Se pueden utilizar los siguientes valores: `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`, `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE`o `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`.

* **** DSC_CREDENTIAL_USERNAME: Especifica el nombre de usuario de los formularios AEM. Para que un usuario invoque correctamente un servicio de AEM Forms, necesita la función de usuario de servicios. Un usuario también puede tener otra función que incluya el permiso Invocar servicio. De lo contrario, se genera una excepción cuando intentan invocar un servicio. Si la seguridad del servicio está deshabilitada, no es necesario especificar esta propiedad de conexión.
* **** DSC_CREDENTIAL_PASSWORD: Especifica el valor de contraseña correspondiente. Si la seguridad del servicio está deshabilitada, no es necesario especificar esta propiedad de conexión.
* **** DSC_REQUEST_TIMEOUT: El límite de tiempo de espera de solicitud predeterminado para la solicitud SOAP es de 1200000 milisegundos (20 minutos). En ocasiones, una solicitud puede requerir más tiempo para completar la operación. Por ejemplo, una solicitud SOAP que recupera un gran conjunto de registros puede requerir un límite de tiempo de espera más largo. Puede usar el `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` para aumentar el límite de tiempo de espera de llamada de solicitud para las solicitudes SOAP.

   **nota**: Solo las invocaciones basadas en SOAP admiten la propiedad DSC_REQUEST_TIMEOUT.

Para establecer las propiedades de conexión, realice las siguientes tareas:

1. Cree un `java.util.Properties` objeto con su constructor.
1. Para establecer la propiedad `DSC_DEFAULT_EJB_ENDPOINT` connection, invoque el `java.util.Properties` método `setProperty` del objeto y pase los valores siguientes:

   * El valor `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` de enumeración
   * Un valor de cadena que especifica la dirección URL del servidor de aplicaciones J2EE que aloja AEM Forms
   >[!NOTE]
   >
   >Si utiliza el modo de conexión SOAP, especifique el valor de enumeración en lugar del valor de `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` enumeración en lugar del valor de `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` enumeración.

1. Para establecer la propiedad `DSC_TRANSPORT_PROTOCOL` connection, invoque el `java.util.Properties` método `setProperty` del objeto y pase los valores siguientes:

   * El valor `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL` de enumeración
   * El valor `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` de enumeración
   >[!NOTE]
   >
   >Si utiliza el modo de conexión SOAP, especifique el valor de `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`enumeración en lugar del valor de `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` enumeración.

1. Para establecer la propiedad `DSC_SERVER_TYPE` connection, invoque el `java.util.Properties` método `setProperty` del objeto y pase los valores siguientes:

   * El valor `ServiceClientFactoryProperties.DSC_SERVER_TYPE`de enumeración
   * Un valor de cadena que especifica el servidor de aplicaciones J2EE que aloja AEM Forms (por ejemplo, si AEM Forms se implementa en JBoss, especifique `JBoss`).

      1. Para establecer la propiedad `DSC_CREDENTIAL_USERNAME` connection, invoque el `java.util.Properties` método `setProperty` del objeto y pase los valores siguientes:
   * El valor `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME` de enumeración
   * Un valor de cadena que especifica el nombre de usuario necesario para invocar AEM Forms

      1. Para establecer la propiedad `DSC_CREDENTIAL_PASSWORD` connection, invoque el `java.util.Properties` método `setProperty` del objeto y pase los valores siguientes:
   * El valor `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD` de enumeración
   * Un valor de cadena que especifica el valor de contraseña correspondiente



**Configuración del modo de conexión EJB para JBoss**

El siguiente ejemplo de código Java establece las propiedades de conexión para invocar los formularios AEM implementados en JBoss y mediante el modo de conexión EJB.

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

El siguiente ejemplo de código Java establece las propiedades de conexión para invocar los formularios AEM implementados en WebLogic y mediante el modo de conexión EJB.

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Configuración del modo de conexión EJB para WebSphere**

El siguiente ejemplo de código Java establece propiedades de conexión para invocar los formularios AEM implementados en WebSphere y mediante el modo de conexión EJB.

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Configuración del modo de conexión SOAP**

El siguiente ejemplo de código Java establece las propiedades de conexión en modo SOAP para invocar los formularios AEM implementados en JBoss.

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

>[!NOTE]
>
>Si selecciona el modo de conexión SOAP, asegúrese de incluir archivos JAR adicionales en la ruta de clases de la aplicación cliente.

**Configuración de las propiedades de conexión cuando la seguridad del servicio está deshabilitada**

El siguiente ejemplo de código Java establece las propiedades de conexión necesarias para invocar los formularios AEM implementados en el servidor de aplicaciones JBoss y cuando la seguridad del servicio está deshabilitada.

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>Todos los inicios rápidos de Java asociados con la programación con AEM Forms muestran la configuración de conexión EJB y SOAP.

**Configuración del modo de conexión SOAP con el límite de tiempo de espera de solicitud personalizado**

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**Uso de un objeto de contexto para invocar AEM Forms**

Puede utilizar un `com.adobe.idp.Context` objeto para invocar un servicio de AEM Forms con un usuario autenticado (el `com.adobe.idp.Context` objeto representa a un usuario autenticado). Al utilizar un `com.adobe.idp.Context` objeto, no es necesario establecer las propiedades `DSC_CREDENTIAL_USERNAME` o `DSC_CREDENTIAL_PASSWORD` . Puede obtener un `com.adobe.idp.Context` objeto al autenticar usuarios mediante el `AuthenticationManagerServiceClient` método `authenticate` del objeto.

El `authenticate` método devuelve un `AuthResult` objeto que contiene los resultados de la autenticación. Puede crear un `com.adobe.idp.Context` objeto invocando su constructor. A continuación, invoque el `com.adobe.idp.Context` método del `initPrincipal` objeto y pase el `AuthResult` objeto, como se muestra en el código siguiente:

```as3
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

En lugar de definir las propiedades `DSC_CREDENTIAL_USERNAME` o `DSC_CREDENTIAL_PASSWORD` , puede invocar el `ServiceClientFactory` método del `setContext` objeto y pasar el `com.adobe.idp.Context` objeto. Cuando utilice un usuario de formularios AEM para invocar un servicio, asegúrese de que tiene la función denominada `Services User` que se requiere para invocar un servicio de AEM Forms.

En el siguiente ejemplo de código se muestra cómo utilizar un `com.adobe.idp.Context` objeto dentro de la configuración de conexión que se utiliza para crear un `EncryptionServiceClient` objeto.

```as3
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

En esta sección se analizan los siguientes escenarios de invocación:

* Una aplicación cliente que se ejecuta en su propia máquina virtual Java (JVM) invoca una instancia independiente de AEM Forms.
* Una aplicación cliente que se ejecuta en su propio JVM invoca instancias de AEM Forms agrupadas.

### Aplicación cliente que invoca una instancia independiente de AEM Forms {#client-application-invoking-a-stand-alone-aem-forms-instance}

El diagrama siguiente muestra una aplicación cliente que se ejecuta en su propio JVM e invoca una instancia independiente de AEM Forms.

En este escenario, una aplicación cliente se ejecuta en su propio JVM e invoca los servicios de AEM Forms.

>[!NOTE]
>
>Este escenario es el escenario invocante en el que se basan todos los inicios rápidos.

### Aplicación cliente que invoca instancias de AEM Forms agrupadas {#client-application-invoking-clustered-aem-forms-instances}

El diagrama siguiente muestra una aplicación cliente que se ejecuta en su propio JVM e invoca instancias de AEM Forms ubicadas en un clúster.

Este escenario es similar al de una aplicación cliente que invoca una instancia independiente de AEM Forms. Sin embargo, la dirección URL del proveedor es diferente. Si una aplicación cliente desea conectarse a un servidor de aplicaciones J2EE específico, la aplicación debe cambiar la URL para hacer referencia al servidor de aplicaciones J2EE específico.

No se recomienda hacer referencia a un servidor de aplicaciones J2EE específico porque la conexión entre la aplicación cliente y AEM Forms finaliza si se detiene el servidor de aplicaciones. Se recomienda que la dirección URL del proveedor haga referencia a un administrador JNDI de nivel de celda, en lugar de a un servidor de aplicaciones J2EE específico.

Las aplicaciones cliente que utilizan el modo de conexión SOAP pueden utilizar el puerto de equilibrador de carga HTTP para el clúster. Las aplicaciones cliente que utilizan el modo de conexión EJB pueden conectarse al puerto EJB de un servidor de aplicaciones J2EE específico. Esta acción controla el equilibrio de carga entre los nodos del clúster.

**WebSphere**

El siguiente ejemplo muestra el contenido de un archivo jndi.properties que se utiliza para conectarse a AEM Forms que se implementa en WebSphere.

```as3
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**WebLogic**

El siguiente ejemplo muestra el contenido de un archivo jndi.properties que se utiliza para conectarse a AEM Forms que se implementa en WebLogic.

```as3
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

El siguiente ejemplo muestra el contenido de un archivo jndi.properties que se utiliza para conectarse a AEM Forms que se implementa en JBoss.

```as3
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>Consulte con el administrador para determinar el nombre y el número de puerto del servidor de aplicaciones J2EE.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Pasar datos a los servicios de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Invocación de un servicio mediante una biblioteca de cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Pasar datos a los servicios de AEM Forms mediante la API de Java {#passing-data-to-aem-forms-services-using-the-java-api}

Las operaciones de servicio de AEM Forms suelen consumir o producir documentos PDF. Al invocar un servicio, a veces es necesario pasar un documento PDF (u otros tipos de documentos como datos XML) al servicio. De igual modo, a veces es necesario gestionar un documento PDF que se devuelve desde el servicio. La clase Java que le permite pasar datos desde y hacia los servicios de AEM Forms es `com.adobe.idp.Document`.

Los servicios de AEM Forms no aceptan un documento PDF como otros tipos de datos, como un `java.io.InputStream` objeto o una matriz de bytes. Un `com.adobe.idp.Document` objeto también se puede utilizar para pasar otros tipos de datos, como datos XML, a servicios.

Un `com.adobe.idp.Document` objeto es un tipo serializable Java, por lo que se puede pasar a través de una llamada RMI. El lado receptor puede estar ubicado en el mismo lugar (el mismo host, el mismo cargador de clase), local (el mismo host, un cargador de clase diferente) o remoto (un host diferente). El paso del contenido del documento se optimiza para cada caso. Por ejemplo, si el remitente y el receptor están ubicados en el mismo host, el contenido se pasa a través de un sistema de archivos local. (En algunos casos, los documentos se pueden pasar en memoria).

Según el tamaño del `com.adobe.idp.Document` objeto, los datos se transportan dentro del `com.adobe.idp.Document` objeto o se almacenan en el sistema de archivos del servidor. Los recursos de almacenamiento temporal que ocupe el `com.adobe.idp.Document` objeto se eliminarán automáticamente al `com.adobe.idp.Document` eliminarlos. (Consulte [Eliminación de objetos](invoking-aem-forms-using-java.md#disposing-document-objects)de documento).

A veces es necesario conocer el tipo de contenido de un `com.adobe.idp.Document` objeto para poder pasarlo a un servicio. Por ejemplo, si una operación requiere un tipo de contenido específico, como `application/pdf`, se recomienda que determine el tipo de contenido. (Consulte [Determinación del tipo de contenido de un documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document)).

El `com.adobe.idp.Document` objeto intenta determinar el tipo de contenido utilizando los datos suministrados. Si no se puede recuperar el tipo de contenido de los datos suministrados (por ejemplo, cuando los datos se suministraron como una matriz de bytes), defina el tipo de contenido. Para definir el tipo de contenido, invoque el `com.adobe.idp.Document` método `setContentType` del objeto. (Consulte [Determinación del tipo de contenido de un documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

Si los archivos colaterales residen en el mismo sistema de archivos, la creación de un `com.adobe.idp.Document` objeto es más rápida. Si los archivos colaterales residen en sistemas de archivos remotos, se debe realizar una operación de copia, lo que afecta al rendimiento.

Una aplicación puede contener tanto `com.adobe.idp.Document` como `org.w3c.dom.Document` tipos de datos. Sin embargo, asegúrese de que califica completamente el tipo de `org.w3c.dom.Document` datos. Para obtener información sobre la conversión de un `org.w3c.dom.Document` objeto a un `com.adobe.idp.Document` objeto, consulte Inicio [rápido (modo EJB): Rellenado previo de formularios con diseños de posición variable mediante la API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)de Java.

>[!NOTE]
>
>Para evitar una pérdida de memoria en WebLogic mientras se utiliza un `com.adobe.idp.Document` objeto, lea la información del documento en fragmentos de 2048 bytes o menos. Por ejemplo, el siguiente código lee la información del documento en fragmentos de 2048 bytes:

```as3
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

[Invocación de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuración de las propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

### Creación de documentos {#creating-documents}

Cree un `com.adobe.idp.Document` objeto antes de invocar una operación de servicio que requiera un documento PDF (u otros tipos de documentos) como valor de entrada. La `com.adobe.idp.Document` clase proporciona constructores que permiten crear un documento a partir de los siguientes tipos de contenido:

* Una matriz de bytes
* Un objeto `com.adobe.idp.Document` existente
* Un `java.io.File` objeto
* Un `java.io.InputStream` objeto
* Un `java.net.URL` objeto

#### Creación de un documento basado en una matriz de bytes {#creating-a-document-based-on-a-byte-array}

El siguiente ejemplo de código crea un `com.adobe.idp.Document` objeto basado en una matriz de bytes.

**Creación de un objeto Document basado en una matriz de bytes**

```as3
 Document myPDFDocument = new Document(myByteArray);
```

#### Creación de un documento basado en otro documento {#creating-a-document-based-on-another-document}

El siguiente ejemplo de código crea un `com.adobe.idp.Document` objeto basado en otro `com.adobe.idp.Document` objeto.

**Creación de un objeto Document basado en otro documento**

```as3
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

El siguiente ejemplo de código crea un `com.adobe.idp.Document` objeto basado en un archivo PDF denominado *map.pdf*. Este archivo se encuentra en la raíz del disco duro C. Este constructor intenta establecer el tipo de contenido MIME del `com.adobe.idp.Document` objeto mediante la extensión de nombre de archivo.

El `com.adobe.idp.Document` constructor que acepta un `java.io.File` objeto también acepta un parámetro booleano. Al establecer este parámetro en `true`, el `com.adobe.idp.Document` objeto elimina el archivo. Esta acción significa que no es necesario quitar el archivo después de pasarlo al constructor `com.adobe.idp.Document` .

Definir este parámetro como `false` significa que se mantiene la propiedad de este archivo. Definir este parámetro como `true` es más eficaz. El motivo es que el `com.adobe.idp.Document` objeto puede mover el archivo directamente al área administrada local en lugar de copiarlo (que es más lento).

**Creación de un objeto Document basado en un archivo PDF**

```as3
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### Creación de un documento basado en un objeto InputStream {#creating-a-document-based-on-an-inputstream-object}

El siguiente ejemplo de código Java crea un `com.adobe.idp.Document` objeto basado en un `java.io.InputStream` objeto.

**Creación de un documento basado en un objeto InputStream**

```as3
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### Creación de un documento basado en contenido accesible desde una dirección URL {#creating-a-document-based-on-content-accessible-from-an-url}

El siguiente ejemplo de código Java crea un `com.adobe.idp.Document` objeto basado en un archivo PDF denominado *map.pdf*. Este archivo se encuentra dentro de una aplicación web denominada `WebApp` que se está ejecutando en `localhost`. Este constructor intenta establecer el tipo de contenido MIME del `com.adobe.idp.Document` objeto mediante el tipo de contenido devuelto con el protocolo URL.

La dirección URL proporcionada al `com.adobe.idp.Document` objeto siempre se lee en el lado en el que se crea el `com.adobe.idp.Document` objeto original, como se muestra en este ejemplo:

```as3
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

El archivo c:/temp/input.pdf debe estar ubicado en el equipo cliente (no en el equipo servidor). El equipo cliente es donde se lee la dirección URL y donde se creó el `com.adobe.idp.Document` objeto.

**Creación de un documento basado en contenido accesible desde una dirección URL**

```as3
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**Consulte también**

[Invocación de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuración de las propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

### Gestión de documentos devueltos {#handling-returned-documents}

Las operaciones de servicio que devuelven un documento PDF (u otros tipos de datos como datos XML) como valor de salida devuelven un `com.adobe.idp.Document` objeto. Después de recibir un `com.adobe.idp.Document` objeto, puede convertirlo a los siguientes formatos:

* Un `java.io.File` objeto
* Un `java.io.InputStream` objeto
* Una matriz de bytes

La línea de código siguiente convierte un `com.adobe.idp.Document` objeto en un `java.io.InputStream` objeto. Supongamos que `myPDFDocument` representa un `com.adobe.idp.Document` objeto:

```as3
     java.io.InputStream resultStream = myDocument.getInputStream();
```

Del mismo modo, puede copiar el contenido de un archivo `com.adobe.idp.Document` a un archivo local realizando las siguientes tareas:

1. Create a `java.io.File` object.
1. Invoque el `com.adobe.idp.Document` método del `copyToFile` objeto y pase el `java.io.File`objeto.

El siguiente ejemplo de código copia el contenido de un `com.adobe.idp.Document` objeto en un archivo denominado *AnotherMap.pdf*.

**Copia del contenido de un objeto de documento en un archivo**

```as3
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**Consulte también**

[Invocación de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuración de las propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinación del tipo de contenido de un documento {#determining-the-content-type-of-a-document}

Determine el tipo MIME de un `com.adobe.idp.Document` objeto invocando el `com.adobe.idp.Document` método `getContentType` del objeto. Este método devuelve un valor de cadena que especifica el tipo de contenido del `com.adobe.idp.Document` objeto. En la tabla siguiente se describen los distintos tipos de contenido que devuelve AEM Forms.

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
   <td><p>Documento PDF</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xdp+xml</code></p></td>
   <td><p>Paquete de datos XML (XDP), que se utiliza para los formularios exportados de la Arquitectura de formularios XML (XFA)</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>Marcadores, archivos adjuntos u otros documentos XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>Formato de datos de formularios (FDF), que se utiliza para formularios exportados de Acrobat</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>Formato de datos de formularios XML (XFDF), que se utiliza para los formularios exportados de Acrobat</p></td>
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

```as3
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**Consulte también**

[Invocación de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuración de las propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminación de objetos de documento {#disposing-document-objects}

Cuando ya no necesite un `Document` objeto, se recomienda eliminarlo invocando su `dispose` método. Cada `Document` objeto consume un descriptor de archivo y hasta 75 MB de espacio de RAM en la plataforma host de la aplicación. Si un `Document` objeto no se elimina, el proceso de recopilación de Java Garage lo descarta. Sin embargo, al eliminarlo antes mediante el `dispose` método, puede liberar la memoria ocupada por el `Document` objeto.

**Consulte también**

[Invocación de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Invocación de un servicio mediante una biblioteca de cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Invocación de un servicio mediante una biblioteca de cliente Java {#invoking-a-service-using-a-java-client-library}

Las operaciones del servicio de AEM Forms se pueden invocar mediante la API con establecimiento inflexible de tipos de un servicio, conocida como biblioteca de clientes Java. Una biblioteca *cliente* Java es un conjunto de clases concretas que proporcionan acceso a los servicios implementados en el contenedor de servicios. Se crea una instancia de un objeto Java que representa el servicio que se va a invocar en lugar de crear un `InvocationRequest` objeto mediante la API de invocación. La API de invocación se utiliza para invocar procesos, como procesos de larga duración, creados en Workbench. (Consulte [Invocación De Procesos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)Largos Centrados En El Hombre).

Para realizar una operación de servicio, invoque un método que pertenece al objeto Java. Una biblioteca de cliente Java contiene métodos que generalmente asignan uno a uno con las operaciones de servicio. Al utilizar una biblioteca de cliente Java, establezca las propiedades de conexión necesarias. (Consulte [Configuración de propiedades](invoking-aem-forms-using-java.md#setting-connection-properties)de conexión).

Después de definir las propiedades de conexión, cree un `ServiceClientFactory` objeto que se utilice para crear una instancia de un objeto Java que le permita invocar un servicio. Cada servicio que tiene una biblioteca de cliente Java tiene un objeto de cliente correspondiente. Por ejemplo, para invocar el servicio Repositorio, cree un `ResourceRepositoryClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto. El `ServiceClientFactory` objeto es responsable de mantener la configuración de conexión necesaria para invocar los servicios de AEM Forms.

Aunque la obtención de una `ServiceClientFactory` es generalmente rápida, algunos gastos generales están relacionados cuando se utiliza la fábrica por primera vez. Este objeto está optimizado para su reutilización y, por lo tanto, cuando sea posible, utilice el mismo `ServiceClientFactory` objeto al crear varios objetos de cliente Java. Es decir, no cree un `ServiceClientFactory` objeto independiente para cada objeto de biblioteca de cliente que cree.

Existe una configuración del Administrador de usuarios que controla la duración de la afirmación SAML que se encuentra dentro del `com.adobe.idp.Context` objeto que afecta al `ServiceClientFactory` objeto. Esta configuración controla todas las duraciones del contexto de autenticación en todos los formularios AEM, incluidas todas las invocaciones realizadas mediante la API de Java. De forma predeterminada, el período de tiempo en el que se puede utilizar un `ServiceCleintFactory` objeto es de dos horas.

>[!NOTE]
>
>Para explicar cómo invocar un servicio mediante la API de Java, se invoca la `writeResource` operación del servicio Repositorio. Esta operación coloca un nuevo recurso en el repositorio.

Puede invocar el servicio Repositorio mediante una biblioteca de cliente Java y siguiendo los pasos siguientes:

1. Incluya archivos JAR de cliente, como adobe-repository-client.jar, en la ruta de clases del proyecto Java. Para obtener información sobre la ubicación de estos archivos, consulte [Inclusión de archivos](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.
1. Establezca las propiedades de conexión necesarias para invocar un servicio.
1. Cree un `ServiceClientFactory` objeto invocando el `ServiceClientFactory` método estático del `createInstance` objeto y pasando el `java.util.Properties` objeto que contiene propiedades de conexión.
1. Cree un `ResourceRepositoryClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto. Utilice el `ResourceRepositoryClient` objeto para invocar operaciones del servicio Repositorio.
1. Cree un `RepositoryInfomodelFactoryBean` objeto mediante su constructor y pase `null`. Este objeto permite crear un `Resource` objeto que representa el contenido que se agrega al repositorio.
1. Cree un `Resource` objeto invocando el `RepositoryInfomodelFactoryBean` método `newImage` del objeto y pasando los siguientes valores:

   * Un valor de ID único especificando `new Id()`.
   * Un valor UUID único especificando `new Lid()`.
   * Nombre del recurso. Puede especificar el nombre de archivo del archivo XDP.
   Convierta el valor devuelto a `Resource`.

1. Cree un `ResourceContent` objeto invocando el `RepositoryInfomodelFactoryBean` método `newImage` del objeto y convirtiendo el valor devuelto en `ResourceContent`. Este objeto representa el contenido que se agrega al repositorio.
1. Cree un `com.adobe.idp.Document` objeto pasando un `java.io.FileInputStream` objeto que almacene el archivo XDP para agregarlo al repositorio. (Consulte [Creación de un documento basado en un objeto](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object)InputStream).
1. Agregue el contenido del `com.adobe.idp.Document` objeto al `ResourceContent` objeto invocando el `ResourceContent` método `setDataDocument` del objeto. Pase el `com.adobe.idp.Document` objeto.
1. Configure el tipo MIME del archivo XDP para agregarlo al repositorio invocando el `ResourceContent` método del `setMimeType` objeto y pasando `application/vnd.adobe.xdp+xml`.
1. Agregue el contenido del `ResourceContent` objeto al `Resource` objeto invocando el `Resource` método s `setContent` del objeto y pasando el `ResourceContent` objeto.
1. Agregue una descripción del recurso invocando el `Resource` método ‘s `setDescription` del objeto y pasando un valor de cadena que represente una descripción del recurso.
1. Agregue el diseño de formulario al repositorio invocando el `ResourceRepositoryClient` método `writeResource` del objeto y pasando los valores siguientes:

   * Un valor de cadena que especifica la ruta a la colección de recursos que contiene el nuevo recurso
   * El `Resource` objeto que se creó

**Consulte también**

[Inicio rápido (modo EJB): Escritura de un recurso mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Invocación de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

##  Invocación de un proceso de corta duración mediante la API de invocación {#invoking-a-short-lived-process-using-the-invocation-api}

Puede invocar un proceso de corta duración mediante la API de invocación de Java. Cuando se invoca un proceso de corta duración mediante la API de invocación, se pasan los valores de parámetro requeridos mediante un `java.util.HashMap` objeto. Para que cada parámetro pase a un servicio, invoque el `java.util.HashMap` método del `put` objeto y especifique el par nombre-valor que requiere el servicio para realizar la operación especificada. Especifique el nombre exacto de los parámetros que pertenecen al proceso de corta duración.

>[!NOTE]
>
>Para obtener información sobre cómo invocar un proceso de larga duración, consulte [Invocación de procesos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)de larga duración centrados en el ser humano.

El análisis aquí trata sobre el uso de la API de invocación para invocar el siguiente proceso breve de AEM Forms denominado `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para seguir el ejemplo de código, cree un proceso denominado `MyApplication/EncryptDocument` mediante Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento PDF no seguro que se pasa al proceso. Esta acción se basa en la `SetValue` operación. El parámetro de entrada para este proceso es una variable de `document` proceso denominada `inDoc`.
1. Codifica el documento PDF con una contraseña. Esta acción se basa en la `PasswordEncryptPDF` operación. El documento PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

### Invocar el proceso breve de MyApplication/EncryptDocument mediante la API de invocación de Java {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

Invoque el `MyApplication/EncryptDocument` proceso de corta duración mediante la API de invocación de Java:

1. Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clases del proyecto Java. (Consulte [Inclusión de archivos](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms).
1. Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión. (Consulte [Configuración de propiedades](invoking-aem-forms-using-java.md#setting-connection-properties)de conexión).
1. Cree un `ServiceClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto. Un `ServiceClient` objeto permite invocar una operación de servicio. Gestiona tareas como la localización, el envío y el enrutamiento de solicitudes de invocación.
1. Cree un `java.util.HashMap` objeto con su constructor.
1. Invocar el `java.util.HashMap` método del `put` objeto para que cada parámetro de entrada pase al proceso de larga duración. Dado que el proceso de corta duración `MyApplication/EncryptDocument` requiere un parámetro de entrada de tipo `Document`, sólo tiene que invocar el `put` método una vez, como se muestra en el siguiente ejemplo.

   ```as3
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. Cree un `InvocationRequest` objeto invocando el método del `ServiceClientFactory` objeto y pasando `createInvocationRequest` los siguientes valores:

   * Un valor de cadena que especifica el nombre del proceso de larga duración que se va a invocar. Para invocar el `MyApplication/EncryptDocument` proceso, especifique `MyApplication/EncryptDocument`.
   * Un valor de cadena que representa el nombre de la operación de proceso. Normalmente, el nombre de una operación de proceso de corta duración es `invoke`.
   * El `java.util.HashMap` objeto que contiene los valores de parámetro que requiere la operación de servicio.
   * Un valor booleano que especifica `true`, que crea una solicitud sincrónica (este valor se aplica para invocar un proceso de corta duración).

1. Envíe la solicitud de invocación al servicio invocando el `ServiceClient` método del `invoke` objeto y pasando el `InvocationRequest` objeto. El `invoke` método devuelve un `InvocationReponse` objeto.

   >[!NOTE]
   >
   >Se puede invocar un proceso de larga duración pasando el valor `false`como el cuarto parámetro del `createInvocationRequest` método. Al pasar el valor, `false`*se crea una solicitud asincrónica.*

1. Recupere el valor devuelto por el proceso invocando el `InvocationReponse` método `getOutputParameter` del objeto y pasando un valor de cadena que especifica el nombre del parámetro de salida. En este caso, especifique `outDoc` ( `outDoc` es el nombre del parámetro de salida para el `MyApplication/EncryptDocument` proceso). Convierta el valor devuelto a `Document`, como se muestra en el siguiente ejemplo.

   ```as3
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. Cree un `java.io.File` objeto y asegúrese de que la extensión del archivo sea .pdf.
1. Invocar el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `com.adobe.idp.Document` objeto en el archivo. Asegúrese de utilizar el `com.adobe.idp.Document` objeto devuelto por el `getOutputParameter` método .

**Consulte también**

[Inicio rápido: Invocación de un proceso de corta duración mediante la API de invocación](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[Invocar procesos de larga vida centrados en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Inclusión de archivos de biblioteca Java de AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)