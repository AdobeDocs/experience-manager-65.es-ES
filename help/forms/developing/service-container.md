---
title: Contenedor de servicio
seo-title: Contenedor de servicio
description: Servicios de AEM Forms ubicados en el contenedor de servicios
uuid: 89f2fd3d-63d7-4b70-b335-47314441f3ec
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: dd9c0ec4-a195-4b78-8992-81d0efcc0a7e
role: Desarrollador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---


# Contenedor de servicio {#service-container}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

Los servicios de AEM Forms ubicados en el contenedor de servicios (incluidos servicios estándar como el servicio de cifrado, procesos de larga duración y de corta duración) se pueden invocar mediante varios proveedores, como un proveedor de EJB. Un proveedor de EJB permite que los servicios de AEM Forms se invoquen a través de RMI/IIOP. Un proveedor de servicios web expone los servicios como servicios web (generación WSDL) utilizando estándares como SOAP/HTTP y SOAP/JMS.

En la tabla siguiente se describen las distintas formas en que puede invocar los servicios de AEM Forms mediante programación.

<table>
 <thead>
  <tr>
   <th><p>Método de invocación</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Integración remota</p></td>
   <td><p>La integración remota permite a los clientes de Flex invocar operaciones de servicio. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">Invocación de AEM Forms mediante (obsoleto para AEM formularios) AEM Forms Remoting</a>).</p></td>
  </tr>
  <tr>
   <td><p>API de Java</p></td>
   <td><p>Una API de Java puede invocar un servicio de AEM Forms. La API de Java está organizada en bibliotecas de cliente y en la API de invocación de Java. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">Invocación de AEM Forms mediante la API de Java</a>).</p></td>
  </tr>
  <tr>
   <td><p>Servicios web</p></td>
   <td><p>AEM Forms admite estándares de servicios web como SOAP/HTTP. Un servicio se puede exponer como un servicio web, con el WSDL cumpliendo con los estándares de servicio web definidos por W3C.</p><p>Se puede invocar un servicio desde cualquier pila de servicios web, incluidos .NET Framework y el SDK de los servicios web de Sun™. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">Invocación de AEM Forms mediante servicios Web</a>).</p></td>
  </tr>
  <tr>
   <td><p>Solicitudes REST</p></td>
   <td><p>AEM Forms admite solicitudes REST. Un servicio se puede invocar directamente desde una página HTML. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">Invocación de AEM Forms mediante solicitudes REST</a>).</p></td>
  </tr>
 </tbody>
</table>

La siguiente ilustración proporciona una representación visual de las diferentes formas en que se pueden invocar los servicios de AEM Forms mediante programación.

>[!NOTE]
>
>Además de utilizar el SDK de AEM Forms para crear aplicaciones cliente que puedan invocar los servicios de AEM Forms, también puede crear componentes que se puedan implementar en el contenedor de servicios. Por ejemplo, puede crear un componente Banco que contenga tipos de datos personalizados que se puedan utilizar en procesos. Es decir, puede crear un tipo de datos como `com.adobe.idp.BankAccount`. A continuación, puede crear instancias `com.adobe.idp.BankAccount` en las aplicaciones cliente.

El contenedor de servicio proporciona la siguiente funcionalidad:

* Permite que los servicios de AEM Forms se invoquen con métodos diferentes. Puede configurar un servicio estableciendo extremos para que se pueda invocar mediante todos los métodos: Remoting, la API de Java, los servicios web y REST. (Consulte [Administración programática de puntos de conexión](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints)).
* Convierte un mensaje en un formato normalizado denominado solicitud de invocación. Se envía una solicitud de invocación desde una aplicación cliente (u otro servicio) a un servicio ubicado en el contenedor de servicios. Una solicitud de invocación contiene información como el nombre del servicio que se va a invocar y los valores de datos necesarios para realizar la operación. Muchos servicios requieren un documento para realizar una operación. Por lo tanto, una solicitud de invocación generalmente contiene un documento, que puede ser datos PDF, datos XDP, datos XML, etc.
* Envía solicitudes de invocación a servicios apropiados (el nombre del servicio que se va a invocar forma parte de la solicitud de invocación).
* Realiza tareas como determinar si el llamador tiene permiso para invocar la operación de servicio especificada. La solicitud de invocación debe contener un nombre de usuario y una contraseña válidos para los formularios AEM.

   Existen diferentes maneras de enviar una solicitud de invocación a un servicio. Además, existen diferentes maneras de enviar los valores de entrada necesarios al servicio. Por ejemplo, supongamos que utiliza la API de Java para invocar un servicio que requiere un documento PDF. El método Java correspondiente contiene un parámetro que acepta un documento PDF. En este caso, el tipo de datos del parámetro es `com.adobe.idp.Document`. (Consulte [Pasar datos a servicios de AEM Forms mediante la API de Java](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)).

   Si invoca un servicio mediante carpetas vigiladas, se envía una solicitud de invocación cuando se coloca un archivo en una carpeta vigilada configurada. Si invoca un servicio mediante correo electrónico, se envía una solicitud de invocación a un servicio cuando llega un mensaje de correo electrónico a una bandeja de entrada configurada.

   El contenedor de servicio devuelve una respuesta de invocación una vez realizada la operación. Una respuesta de invocación contiene información como los resultados de la operación. Por ejemplo, si la operación modifica un documento PDF, la respuesta de invocación contiene el documento PDF modificado. Si la operación no se realizó correctamente, la respuesta de invocación contiene un mensaje de error.

   Se puede recuperar una respuesta de invocación del mismo modo en que se envía una solicitud de invocación. Es decir, si la solicitud de invocación se envía mediante la API de Java, se puede recuperar una respuesta de invocación mediante la API de Java. Supongamos, por ejemplo, que una operación modifica un documento PDF. Puede recuperar el documento PDF modificado obteniendo el valor devuelto del método Java que invocó el servicio.

   Cuando se invoca un proceso de larga duración, una respuesta de invocación contiene un valor de identificador asociado con la solicitud de invocación. Utilizando este valor de identificador, puede comprobar el estado del proceso en un momento posterior. Por ejemplo, consideremos el servicio de larga duración de MortgageLoan. Con el valor del identificador, puede comprobar si el proceso se completó correctamente. (Consulte [Invocación de procesos de larga duración centrados en los humanos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)).

   El diagrama siguiente muestra una aplicación cliente (que utiliza la API de Java) que invoca un servicio.

   Cuando una aplicación cliente invoca un servicio, se producen tres eventos:

   1. Una aplicación cliente envía una solicitud de invocación a un servicio.
   1. El servicio realiza la operación especificada en la solicitud de invocación.
   1. El contenedor de servicio devuelve una respuesta de invocación a la aplicación cliente.

**Consulte también**

[Explicación de los procesos de AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[Invocación de AEM Forms mediante AEM Forms Remoting (obsoleto para formularios AEM)](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Invocación de AEM Forms mediante la API de Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Invocación de AEM Forms mediante servicios web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[Invocación de procesos de larga vida centrados en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Invocación de AEM Forms mediante solicitudes REST](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
