---
title: Proteger documentos mediante directivas
description: Utilice el servicio Document Security para aplicar dinámicamente la configuración de confidencialidad a los documentos de Adobe PDF y mantener el control sobre los documentos. El servicio Document Security también permite a los usuarios mantener el control sobre cómo utilizan los destinatarios el documento de PDF protegido por políticas.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: ff42579e-6aaf-433d-8b5d-9e9dd0957250
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '15464'
ht-degree: 0%

---

# Proteger documentos mediante directivas {#protecting-documents-with-policies}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

**Acerca del servicio Document Security**

El servicio Document Security permite a los usuarios aplicar dinámicamente la configuración de confidencialidad a los documentos de Adobe PDF y mantener el control sobre los documentos, independientemente de su distribución.

El servicio Document Security evita que la información se propague más allá del alcance del usuario, ya que permite a los usuarios mantener el control sobre cómo utilizan los destinatarios el documento de PDF protegido por políticas. Un usuario puede especificar quién puede abrir un documento, limitar cómo puede utilizarlo y supervisar el documento después de distribuirlo. Un usuario también puede controlar dinámicamente el acceso a un documento protegido por políticas e incluso puede revocar dinámicamente el acceso al documento.

El servicio Document Security también protege otros tipos de archivo, como archivos de Microsoft Word (archivos DOC). Puede utilizar la API de cliente de Document Security para trabajar con estos tipos de archivos. Se admiten las siguientes versiones:

* Archivos de Microsoft Office 2003 (archivos DOC, XLS, PPT)
* Archivos de Microsoft Office 2007 (archivos DOCX, XLSX, PPTX)
* Archivos de PTC Pro/E

Para mayor claridad, las dos secciones siguientes tratan sobre cómo trabajar con documentos de Word:

* [Aplicar directivas a documentos de Word](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Quitar directivas de documentos de Word](protecting-documents-policies.md#removing-policies-from-word-documents)

Puede realizar estas tareas mediante el servicio Document Security:

* Crear directivas. Para obtener más información, consulte [Creación de directivas](protecting-documents-policies.md#creating-policies).
* Modificar directivas. Para obtener más información, consulte [Modificación de directivas](protecting-documents-policies.md#modifying-policies).
* Eliminar directivas. Para obtener más información, consulte [Eliminación de directivas](protecting-documents-policies.md#deleting-policies).
* Aplicar directivas a documentos de PDF. Para obtener más información, consulte [Aplicación de directivas a documentos de PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents).
* Quitar directivas de documentos de PDF. Para obtener más información, consulte [Quitar directivas de documentos de PDF](protecting-documents-policies.md#removing-policies-from-pdf-documents).
* Documentos protegidos por directivas de Inspect. Para obtener más información, consulte [Inspección de documentos de PDF protegidos por directivas](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents).
* Revocar acceso a documentos de PDF. Para obtener más información, consulte [Revocar acceso a documentos](protecting-documents-policies.md#revoking-access-to-documents).
* Restablecer el acceso a los documentos revocados. Para obtener más información, consulte [Restablecer el acceso a los documentos revocados](protecting-documents-policies.md#reinstating-access-to-revoked-documents).
* Crear marcas de agua. Para obtener más información, consulte [Creación de marcas de agua](protecting-documents-policies.md#creating-watermarks).
* Buscar eventos. Para obtener más información, consulte [Búsqueda de eventos](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Creación de directivas {#creating-policies}

Puede crear directivas mediante programación utilizando la API de Java de Document Security o la API del servicio web. A *directiva* es una recopilación de información que incluye la configuración de Document Security, usuarios autorizados y derechos de uso. Puede crear y guardar cualquier número de directivas, utilizando la configuración de seguridad adecuada para diferentes situaciones y usuarios.

Las directivas permiten realizar estas tareas:

* Especifique las personas que pueden abrir el documento. Los destinatarios pueden pertenecer a su organización o ser externos a ella.
* Especifique cómo pueden utilizar el documento los destinatarios. Puede restringir el acceso a diferentes funciones de Acrobat y Adobe Reader. Estas características incluyen la capacidad de imprimir y copiar texto, agregar firmas y agregar comentarios a un documento.
* Cambie la configuración de acceso y seguridad en cualquier momento, incluso después de distribuir el documento protegido por una directiva.
* Supervise el uso del documento después de distribuirlo. Puede ver cómo se utiliza el documento y quién lo utiliza. Por ejemplo, puede averiguar cuándo alguien ha abierto el documento.

### Creación de una directiva mediante servicios web {#creating-a-policy-using-web-services}

Al crear una directiva mediante la API del servicio web, haga referencia a un archivo XML del lenguaje de derechos de documentos portátiles (PDRL) existente que describa la directiva. Los permisos de directiva y el principal se definen en el documento PDRL. El siguiente documento XML es un ejemplo de documento PDRL.

```xml
 <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
 <Policy PolicyInstanceVersion="1" PolicyID="5DA3F847-DE76-F9CC-63EA-49A8D59154DE" PolicyCreationTime="2004-08-30T00:02:28.294+00:00" PolicyType="1" PolicySchemaVersion="1.0" PolicyName="SDK Test Policy -4344050357301573237" PolicyDescription="An SDK Test policy" xmlns="https://www.adobe.com/schema/1.0/pdrl">
       <PolicyEntry>
          <ns1:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns1="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns2:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns2="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns3:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns3="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns4:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns4="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>all_internal_users</PrincipalName>
          </Principal>
       </PolicyEntry>
       <PolicyEntry>
          <ns5:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns5="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns6:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns6="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns7:Permission PermissionName="com.adobe.aps.pdf.copy" Access="ALLOW" xmlns:ns7="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns8:Permission PermissionName="com.adobe.aps.pdf.printLow" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns8="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns9:Permission PermissionName="com.adobe.aps.policySwitch" Access="ALLOW" xmlns:ns9="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns10:Permission PermissionName="com.adobe.aps.revoke" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns10="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns11:Permission PermissionName="com.adobe.aps.pdf.edit" Access="ALLOW" xmlns:ns11="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns12:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns12="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns13:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns13="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns14:Permission PermissionName="com.adobe.aps.pdf.printHigh" Access="ALLOW" xmlns:ns14="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>publisher</PrincipalName>
          </Principal>
       </PolicyEntry>
 
       <OfflineLeasePeriod>
          <Duration>P31D</Duration>
       </OfflineLeasePeriod>
 
       <AuditSettings isTracked="true" />
 
       <PolicyValidityPeriod isAbsoluteTime="false">
          <ValidityPeriodRelative>
             <NotBeforeRelative>PT0S</NotBeforeRelative>
 
             <NotAfterRelative>P20D</NotAfterRelative>
          </ValidityPeriodRelative>
       </PolicyValidityPeriod>
 </Policy>
 
```

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para crear una directiva, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de la API de cliente de Document Security.
1. Establezca los atributos de la directiva.
1. Crear una entrada de directiva.
1. Registre la directiva.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-rightsmanagement-client.jar
* namespace.jar (si AEM Forms está implementado en JBoss)
* jaxb-api.jar (si AEM Forms está implementado en JBoss)
* jaxb-impl.jar (si AEM Forms está implementado en JBoss)
* jaxb-libs.jar (si AEM Forms está implementado en JBoss)
* jaxb-xjc.jar (si AEM Forms está implementado en JBoss)
* refreshDatatype.jar (si AEM Forms está implementado en JBoss)
* xsdlib.jar (si AEM Forms está implementado en JBoss)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar (utilice un archivo JAR diferente si AEM Forms no está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un objeto de API de cliente de Document Security**

Para poder realizar mediante programación una operación del servicio Document Security, cree un objeto de cliente del servicio Document Security.

**Establecer los atributos de la directiva**

Para crear una directiva, establezca los atributos de la directiva. Un atributo obligatorio es el nombre de la política. Los nombres de las directivas deben ser únicos para cada conjunto de directivas. Un conjunto de directivas es simplemente una colección de directivas. Puede haber dos directivas con el mismo nombre si pertenecen a conjuntos de directivas independientes. Sin embargo, dos directivas dentro de un único conjunto de directivas no pueden tener el mismo nombre de directiva.

Otro atributo útil que se debe establecer es el periodo de validez. Un período de validez es el período de tiempo durante el cual un documento protegido por una directiva es accesible para los destinatarios autorizados. Si no establece este atributo, la directiva siempre es válida.

Un periodo de validez se puede establecer en una de estas opciones:

* Se establece el número de días durante los cuales se puede acceder al documento desde el momento en que se publica
* Una fecha final tras la cual no se puede acceder al documento
* Un intervalo de fechas específico para el que se puede acceder al documento
* Siempre válido

Puede especificar simplemente una fecha de inicio, lo que hace que la directiva sea válida después de la fecha de inicio. Si especifica solamente una fecha de finalización, la directiva es válida hasta la fecha de finalización. Sin embargo, se produce una excepción si no se definen una fecha de inicio y una fecha de finalización.

Al establecer atributos que pertenecen a una directiva, también puede establecer la configuración de cifrado. Esta configuración de cifrado se aplica cuando la directiva se aplica a un documento. Puede especificar los siguientes valores de cifrado:

* **AES256**: representa el algoritmo de cifrado AES con una clave de 256 bits.
* **AES128**: representa el algoritmo de cifrado AES con una clave de 128 bits.
* **Sin cifrado:** No representa ningún cifrado.

Al especificar el `NoEncryption` , no se puede establecer la opción `PlaintextMetadata` opción para `false`. Si intenta hacerlo, se produce una excepción.

>[!NOTE]
>
>Para obtener información sobre otros atributos que puede establecer, consulte la `Policy` descripción de la interfaz en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Crear una entrada de directiva**

Una entrada de directiva adjunta entidades principales, que son grupos y usuarios, y permisos a una directiva. Una directiva debe tener al menos una entrada de directiva. Supongamos, por ejemplo, que realiza estas tareas:

* Cree y registre una entrada de directiva que permita a un grupo ver un documento únicamente mientras está en línea y que prohíba a los destinatarios copiarlo.
* Adjunte la entrada de directiva a la directiva.
* Proteja un documento con la directiva mediante Acrobat.

Estas acciones hacen que los destinatarios solo puedan ver el documento en línea y no puedan copiarlo. El documento permanecerá seguro hasta que se quite la seguridad del mismo.

**Registrar la directiva**

Se debe registrar una nueva directiva para poder utilizarla. Después de registrar una directiva, puede utilizarla para proteger documentos.

### Creación de una política con la API de Java {#create-a-policy-using-the-java-api}

Cree una directiva mediante la API de seguridad de los documentos (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `DocumentSecurityClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Establezca los atributos de la directiva.

   * Crear un `Policy` invocando el objeto de `InfomodelObjectFactory` objeto estático `createPolicy` método. Este método devuelve un `Policy` objeto.
   * Establezca el atributo name de la directiva invocando el `Policy` del objeto `setName` y pasando un valor de cadena que especifica el nombre de la directiva.
   * Establezca la descripción de la directiva invocando la variable `Policy` del objeto `setDescription` y pasando un valor de cadena que especifica la descripción de la directiva.
   * Especifique el conjunto de directivas al que pertenece la nueva directiva invocando `Policy` del objeto `setPolicySetName` y pasando un valor de cadena que especifica el nombre del conjunto de directivas. (Puede especificar `null` para este valor de parámetro que da como resultado que la política se añada a *Mis directivas* conjunto de directivas.)
   * Cree el periodo de validez de la política invocando el `InfomodelObjectFactory` objeto estático `createValidityPeriod` método. Este método devuelve un `ValidityPeriod` objeto.
   * Establezca el número de días durante los cuales se puede acceder a un documento protegido por una directiva invocando el `ValidityPeriod` del objeto `setRelativeExpirationDays` y pasando un valor entero que especifica el número de días.
   * Establezca el período de validez de la directiva invocando el `Policy` del objeto `setValidityPeriod` y pasando el `ValidityPeriod` objeto.

1. Crear una entrada de directiva.

   * Cree una entrada de directiva invocando el `InfomodelObjectFactory` objeto estático `createPolicyEntry` método. Este método devuelve un `PolicyEntry` objeto.
   * Especifique los permisos de la directiva invocando el `InfomodelObjectFactory` objeto estático `createPermission` método. Pase un miembro de datos estáticos que pertenezca a `Permission` que representa el permiso. Este método devuelve un `Permission` objeto. Por ejemplo, para agregar el permiso que permite a los usuarios copiar datos de un documento de PDF protegido por una directiva, pase `Permission.COPY`. (Repita este paso para cada permiso que desee agregar).
   * Agregue el permiso a la entrada de directiva invocando el `PolicyEntry` del objeto `addPermission` y pasando el `Permission` objeto. (Repita este paso para cada `Permission` objeto que ha creado).
   * Cree el principal de la política invocando el `InfomodelObjectFactory` objeto estático `createSpecialPrincipal` método. Pase un miembro de datos que pertenezca a `InfomodelObjectFactory` que representa el principal. Este método devuelve un `Principal` objeto. Por ejemplo, para agregar el editor del documento como principal, pase `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * Agregue el principal a la entrada de directiva invocando el `PolicyEntry` del objeto `setPrincipal`y pasando el `Principal` objeto.
   * Añada la entrada de directiva a la directiva invocando el `Policy` del objeto `addPolicyEntry` y pasando el `PolicyEntry` objeto.

1. Registre la directiva.

   * Crear un `PolicyManager` invocando el objeto de `DocumentSecurityClient` del objeto `getPolicyManager` método.
   * Registre la directiva invocando el `PolicyManager` del objeto `registerPolicy` y pasando los siguientes valores:

      * El `Policy` que representa la directiva que se va a registrar.

   * Valor de cadena que representa el conjunto de directivas al que pertenece la directiva.

   AEM Si utiliza una cuenta de administrador de formularios en la configuración de conexión para crear la cuenta de administrador de formularios en la aplicación de `DocumentSecurityClient` objeto y, a continuación, especifique el nombre del conjunto de directivas al invocar el `registerPolicy` método. Si pasa un `null` valor para el conjunto de directivas, la directiva se crea en los administradores *Mis directivas* conjunto de directivas.

   Si utiliza un usuario de Document Security dentro de la configuración de conexión, puede invocar la sobrecarga `registerPolicy` que solo acepta la directiva. Es decir, no es necesario especificar el nombre del conjunto de directivas. Sin embargo, la directiva se agrega al conjunto de directivas denominado *Mis directivas*. Si no desea agregar la nueva directiva a este conjunto de directivas, especifique un nombre de conjunto de directivas cuando invoque el `registerPolicy` método.

   >[!NOTE]
   >
   >Al crear una directiva, haga referencia a un conjunto de directivas existente. Si especifica un conjunto de directivas que no existe, se produce una excepción.

Para ver ejemplos de código utilizando el servicio Document Security, consulte lo siguiente:

* &quot;Inicio rápido (modo SOAP): Creación de una directiva con la API de Java&quot;

### Creación de una directiva mediante la API de servicio web {#create-a-policy-using-the-web-service-api}

Cree una directiva mediante la API de seguridad de los documentos (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `DocumentSecurityServiceClient` mediante su constructor predeterminado.
   * Crear un `DocumentSecurityServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `RightsManagementServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Establezca los atributos de la directiva.

   * Crear un `PolicySpec` mediante su constructor.
   * Establezca el nombre de la directiva asignando un valor de cadena al `PolicySpec` del objeto `name` miembro de datos.
   * Establezca la descripción de la directiva asignando un valor de cadena al `PolicySpec` del objeto `description` miembro de datos.
   * Especifique el conjunto de directivas al que pertenece la directiva asignando un valor de cadena al `PolicySpec` del objeto `policySetName` miembro de datos. Especifique un nombre de conjunto de directivas existente. (Puede especificar `null` para este valor de parámetro que resulta en la directiva agregada a *Mis directivas*.)
   * Establezca el período de concesión sin conexión de la directiva asignando un valor entero al `PolicySpec` del objeto `offlineLeasePeriod` miembro de datos.
   * Configure las variables `PolicySpec` del objeto `policyXml` miembro de datos con un valor de cadena que representa los datos XML de PDRL. Para realizar esta tarea, cree un archivo .NET `StreamReader` mediante su constructor. Pase la ubicación de un archivo XML de PDRL que represente la directiva a `StreamReader` constructor. A continuación, invoque el `StreamReader` del objeto `ReadLine` y asigne el valor devuelto a una variable de cadena. Itere a través de `StreamReader` objeto hasta que `ReadLine` el método devuelve null. Asigne la variable de cadena a `PolicySpec` del objeto `policyXml` miembro de datos.

1. Crear una entrada de directiva.

   No es necesario crear una entrada de directiva al crear una directiva mediante la API del servicio web de Document Security. La entrada de directiva se define en el documento PDRL.

1. Registre la directiva.

   Registre la directiva invocando el `DocumentSecurityServiceClient` del objeto `registerPolicy` y pasando los siguientes valores:

   * El `PolicySpec` que representa la directiva que se va a registrar.
   * Valor de cadena que representa el conjunto de directivas al que pertenece la directiva. Puede especificar un `null` valor que hace que la política se añada a *Mis directivas* conjunto de directivas.

   AEM Si utiliza una cuenta de administrador de formularios en la configuración de conexión para crear la cuenta de administrador de formularios en la aplicación de `DocumentSecurityClient` objeto, especifique el nombre del conjunto de directivas al invocar el `registerPolicy` método.

   Si utiliza un usuario de Document Security dentro de la configuración de conexión, puede invocar la sobrecarga `registerPolicy` que solo acepta la directiva. Es decir, no es necesario especificar el nombre del conjunto de directivas. Sin embargo, la directiva se agrega al conjunto de directivas denominado *Mis directivas*. Si no desea agregar la nueva directiva a este conjunto de directivas, especifique un nombre de conjunto de directivas cuando invoque el `registerPolicy` método.

   >[!NOTE]
   >
   >Al crear una directiva y especificar un conjunto de directivas, asegúrese de especificar un conjunto de directivas existente. Si especifica un conjunto de directivas que no existe, se produce una excepción.

Para ver ejemplos de código utilizando el servicio Document Security, consulte los siguientes tutoriales rápidos:

* &quot;Inicio rápido (MTOM): Creación de una directiva mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Creación de una directiva mediante la API de servicio web&quot;

## Modificación de directivas {#modifying-policies}

Puede modificar una directiva existente mediante la API de Java de Document Security o la API del servicio web. Para cambiar una directiva existente, puede recuperarla, modificarla y, a continuación, actualizar la directiva en el servidor. Por ejemplo, supongamos que recupera una política existente y amplía su periodo de validez. Antes de que el cambio surta efecto, debe actualizar la directiva.

Puede modificar una política cuando cambien los requisitos de la empresa y la política ya no refleje estos requisitos. En lugar de crear una política, simplemente puede actualizar una política existente.

Para modificar atributos de directiva mediante un servicio web (por ejemplo, mediante clases de proxy Java creadas con JAX-WS), debe asegurarse de que la directiva esté registrada en el servicio Document Security. A continuación, puede hacer referencia a la directiva existente mediante la variable `PolicySpec.getPolicyXml` y modificar los atributos de la directiva mediante los métodos aplicables. Por ejemplo, puede modificar el período de concesión sin conexión invocando la variable `PolicySpec.setOfflineLeasePeriod` método.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para modificar una directiva existente, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de la API de cliente de Document Security.
1. Recuperar una directiva existente.
1. Cambiar directivas y atributos.
1. Actualice la directiva.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Document Security**

Para poder realizar mediante programación una operación del servicio Document Security, debe crear un objeto de cliente del servicio Document Security. Si utiliza la API de Java, cree un `RightsManagementClient` objeto. Si utiliza la API del servicio web de Document Security, cree un `RightsManagementServiceService` objeto.

**Recuperar una política existente**

Recupere una directiva existente para modificarla. Para recuperar una directiva, especifique el nombre de la directiva y el conjunto de directivas al que pertenece. Si especifica un `null` valor para el nombre del conjunto de directivas, la directiva se recupera del *Mis directivas* conjunto de directivas.

**Establecer los atributos de la directiva**

Para modificar una directiva, modifique el valor de sus atributos. El único atributo de directiva que no se puede cambiar es el atributo de nombre. Por ejemplo, para cambiar el período de concesión sin conexión de la política, puede modificar el valor del atributo de período de concesión sin conexión de la política.

Al modificar el período de concesión sin conexión de una directiva mediante un servicio web, la variable `offlineLeasePeriod` en el campo `PolicySpec` se ignora la interfaz. Para actualizar el período de concesión sin conexión, modifique la `OfflineLeasePeriod` en el documento XML de PDRL. A continuación, haga referencia al documento XML PDRL actualizado utilizando la variable `PolicySpec` de la interfaz `policyXML` miembro de datos.

>[!NOTE]
>
>Para obtener información sobre otros atributos que puede establecer, consulte la `Policy` descripción de la interfaz en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Actualizar la directiva**

Antes de que los cambios que realice en una directiva surtan efecto, debe actualizar la directiva con el servicio Document Security. Los cambios en las directivas que protegen documentos se actualizan la próxima vez que el documento protegido por directivas se sincronice con el servicio Document Security.

### Modificación de directivas existentes mediante la API de Java {#modify-existing-policies-using-the-java-api}

Modifique una directiva existente mediante la API de seguridad de los documentos (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `RightsManagementClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Recuperar una directiva existente.

   * Crear un `PolicyManager` invocando el objeto de `RightsManagementClient` del objeto `getPolicyManager` método.
   * Crear un `Policy` que representa la directiva que se va a actualizar invocando el objeto `PolicyManager` del objeto `getPolicy` y pasando los siguientes valores&quot;

      * Valor de cadena que representa el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar `null` que da como resultado la `MyPolicies` conjunto de directivas en uso.
      * Valor de cadena que representa el nombre de la directiva.

1. Establezca los atributos de la directiva.

   Cambie los atributos de la póliza para satisfacer sus necesidades comerciales. Por ejemplo, para cambiar el período de concesión sin conexión de la directiva, invoque el `Policy` del objeto `setOfflineLeasePeriod` método.

1. Actualice la directiva.

   Actualice la directiva invocando `PolicyManager` del objeto `updatePolicy` método. Pase el `Policy` que representa la directiva que se va a actualizar.

**Ejemplos de código**

Para obtener ejemplos de código utilizando el servicio Document Security, consulte Inicio rápido (modo SOAP): Modificación de una directiva mediante la sección API de Java.

### Modificar directivas existentes mediante la API de servicio web {#modify-existing-policies-using-the-web-service-api}

Modifique una directiva existente mediante la API de seguridad de los documentos (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `RightsManagementServiceClient` mediante su constructor predeterminado.
   * Crear un `RightsManagementServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `RightsManagementServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperar una directiva existente.

   Crear un `PolicySpec` que representa la directiva que se va a modificar invocando el objeto `RightsManagementServiceClient` del objeto `getPolicy` y pasando los siguientes valores:

   * Valor de cadena que especifica el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar `null` que da como resultado la `MyPolicies` conjunto de directivas en uso.
   * Valor de cadena que especifica el nombre de la directiva.

1. Establezca los atributos de la directiva.

   Cambie los atributos de la póliza para satisfacer sus necesidades comerciales.

1. Actualice la directiva.

   Actualice la directiva invocando el `RightsManagementServiceClient` del objeto `updatePolicyFromSDK` y pasando el `PolicySpec` que representa la directiva que se va a actualizar.

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte los siguientes tutoriales rápidos:

* &quot;Inicio rápido (MTOM): Modificar una directiva mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Modificación de una directiva mediante la API de servicio web&quot;

## Eliminación de directivas {#deleting-policies}

Puede eliminar una política existente mediante la API de Java de Document Security o la API del servicio web. Una vez eliminada una directiva, ya no se puede utilizar para proteger documentos. Sin embargo, los documentos protegidos por directivas existentes que utilizan la directiva siguen protegidos. Puede eliminar una directiva cuando haya una más reciente disponible.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para eliminar una directiva existente, realice los siguientes pasos:

1. Incluir archivos de proyecto
1. Cree un objeto de la API de cliente de Document Security.
1. Elimine la directiva.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Document Security**

Para poder realizar mediante programación una operación del servicio Document Security, debe crear un objeto de cliente del servicio Document Security. Si utiliza la API de Java, cree un `RightsManagementClient` objeto. Si utiliza la API del servicio web de Document Security, cree un `RightsManagementServiceService` objeto.

**Eliminar la política**

Para eliminar una directiva, especifique la directiva que desea eliminar y el conjunto de directivas al que pertenece. El usuario cuya configuración se utilice para invocar AEM Forms debe tener permiso para eliminar la directiva; de lo contrario, se produce una excepción. Del mismo modo, si intenta eliminar una directiva que no existe, se produce una excepción.

### Eliminación de directivas mediante la API de Java {#delete-policies-using-the-java-api}

Eliminar una directiva mediante la API de Document Security (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `RightsManagementClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Elimine la directiva.

   * Crear un `PolicyManager` invocando el objeto de `RightsManagementClient` del objeto `getPolicyManager` método.
   * Elimine la directiva invocando el `PolicyManager` del objeto `deletePolicy` y pasando los siguientes valores:

      * Valor de cadena que especifica el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar `null` que da como resultado la `MyPolicies` conjunto de directivas en uso.
      * Valor de cadena que especifica el nombre de la directiva que se va a eliminar.

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte los siguientes tutoriales rápidos:

* &quot;Inicio rápido (modo SOAP): Eliminación de una directiva mediante la API de Java&quot;

### Eliminar directivas mediante la API de servicio web {#delete-policies-using-the-web-service-api}

Eliminar una directiva mediante la API de Document Security (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `RightsManagementServiceClient` mediante su constructor predeterminado.
   * Crear un `RightsManagementServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `RightsManagementServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Elimine la directiva.

   Eliminar una directiva invocando el `RightsManagementServiceClient` del objeto `deletePolicy` y pasando los siguientes valores:

   * Valor de cadena que especifica el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar `null` que da como resultado la `MyPolicies` conjunto de directivas en uso.
   * Valor de cadena que especifica el nombre de la directiva que se va a eliminar.

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte los siguientes tutoriales rápidos:

* &quot;Inicio rápido (MTOM): Eliminación de una directiva mediante la API del servicio web&quot;
* &quot;Inicio rápido (SwaRef): Eliminación de una directiva mediante la API del servicio web&quot;

## Aplicación de directivas a documentos de PDF {#applying-policies-to-pdf-documents}

Puede aplicar una directiva a un documento de PDF para proteger el documento. Al aplicar una directiva a un documento de PDF, se restringe el acceso al documento. No puede aplicar una directiva a un documento si éste ya está protegido con una directiva.

Mientras el documento esté abierto, también puede restringir el acceso a las funciones de Acrobat y Adobe Reader, incluida la capacidad de imprimir y copiar texto, realizar cambios y agregar firmas y comentarios a un documento. Además, puede revocar un documento de PDF protegido por una directiva cuando ya no desee que los usuarios accedan al documento.

Puede monitorizar el uso de un documento protegido por políticas después de distribuirlo. Es decir, puede ver cómo se utiliza el documento y quién lo está utilizando. Por ejemplo, puede averiguar cuándo alguien ha abierto el documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-3}

Para aplicar una directiva a un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de la API de cliente de Document Security.
1. Recupere un documento de PDF al que se aplique una directiva.
1. Aplicar una directiva existente al documento de PDF.
1. Guarde el documento de PDF protegido por una directiva.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto API de cliente de Document Security**

Para poder realizar mediante programación una operación del servicio Document Security, cree un objeto de cliente del servicio Document Security. Si utiliza la API de Java, cree un `DocumentSecurityClient` objeto. Si utiliza la API del servicio web de Document Security, cree un `DocumentSecurityServiceService` objeto.

**Recuperación de un documento de PDF**

Puede recuperar un documento de PDF para aplicar una directiva. Después de aplicar una directiva al documento de PDF, los usuarios están restringidos al utilizar el documento. Por ejemplo, si la directiva no permite abrir el documento sin conexión, los usuarios deben estar en línea para abrirlo.

**Aplicar una directiva existente al documento del PDF**

Para aplicar una directiva a un documento de PDF, haga referencia a una directiva existente y especifique a qué conjunto de directivas pertenece la directiva. El usuario que configura las propiedades de conexión debe tener acceso a la directiva especificada. Si no es así, se produce una excepción.

**Guardar el documento del PDF**

Una vez que el servicio Document Security aplica una directiva a un documento de PDF, puede guardar el documento de PDF protegido por una directiva como archivo de PDF.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revocar acceso a documentos](protecting-documents-policies.md#revoking-access-to-documents)

### Aplicación de una directiva a un documento de PDF mediante la API de Java {#apply-a-policy-to-a-pdf-document-using-the-java-api}

Aplicar una directiva a un documento de PDF mediante la API de Document Security (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `RightsManagementClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Recupere un documento de PDF.

   * Crear un `java.io.FileInputStream` que representa el documento de PDF utilizando su constructor. Pase un valor de cadena que especifique la ubicación del documento del PDF.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Aplicar una directiva existente al documento de PDF.

   * Crear un `DocumentManager` invocando el objeto de `RightsManagementClient` del objeto `getDocumentManager` método.
   * Aplique una directiva al documento del PDF invocando el `DocumentManager` del objeto `protectDocument` y pasando los siguientes valores:

      * El `com.adobe.idp.Document` que contiene el documento del PDF al que se aplica la directiva.
      * Valor de cadena que especifica el nombre del documento.
      * Valor de cadena que especifica el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar un `null` que resulta en el `MyPolicies` conjunto de directivas en uso.
      * Valor de cadena que especifica el nombre de la directiva.
      * Valor de cadena que representa el nombre del dominio del administrador de usuarios del usuario que es el editor del documento. Este valor de parámetro es opcional y puede ser nulo (si este parámetro es nulo, el siguiente valor de parámetro debe ser nulo).
      * Valor de cadena que representa el nombre canónico del usuario administrador de usuarios que es el editor del documento. Este valor de parámetro es opcional y puede ser `null` (si este parámetro es nulo, el valor del parámetro anterior debe ser `null`).
      * A `com.adobe.livecycle.rightsmanagement.Locale` que representa la configuración regional utilizada para seleccionar la plantilla de MS Office. Este valor de parámetro es opcional y no se utiliza para documentos de PDF. Para proteger un documento de PDF, especifique `null`.

     El `protectDocument` El método devuelve un valor `RMSecureDocumentResult` que contiene el documento de PDF protegido por una directiva.

1. Guarde el documento del PDF.

   * Invoque el `RMSecureDocumentResult` del objeto `getProtectedDoc` para obtener el documento de PDF protegido por una directiva. Este método devuelve un `com.adobe.idp.Document` objeto.
   * Crear un `java.io.File` y asegúrese de que la extensión del archivo es PDF.
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `Document` al archivo (asegúrese de utilizar la variable `Document` objeto que ha devuelto el `getProtectedDoc` método).

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte los siguientes tutoriales rápidos:

* &quot;Inicio rápido (modo EJB): Aplicar una directiva a un documento de PDF mediante la API de Java&quot;
* &quot;Inicio rápido (modo SOAP): Aplicar una directiva a un documento de PDF mediante la API de Java&quot;

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aplicar una directiva a un documento de PDF mediante la API de servicio web {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

Aplicar una directiva a un documento de PDF mediante la API de Document Security (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `RightsManagementServiceClient` mediante su constructor predeterminado.
   * Crear un `RightsManagementServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `RightsManagementServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere un documento de PDF.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar un documento de PDF al que se aplica una directiva.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento de PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Determinar el tamaño de la matriz de bytes obteniendo `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` método. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Aplicar una directiva existente al documento de PDF.

   Aplique una directiva al documento del PDF invocando el `RightsManagementServiceClient` del objeto `protectDocument` y pasando los siguientes valores:

   * El `BLOB` que contiene el documento del PDF al que se aplica la directiva.
   * Valor de cadena que especifica el nombre del documento.
   * Valor de cadena que especifica el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar un `null` que resulta en el `MyPolicies` conjunto de directivas en uso.
   * Valor de cadena que especifica el nombre de la directiva.
   * Valor de cadena que representa el nombre del dominio del administrador de usuarios del usuario que es el editor del documento. Este valor de parámetro es opcional y puede ser nulo (si este parámetro es nulo, el siguiente valor de parámetro debe ser `null`).
   * Valor de cadena que representa el nombre canónico del usuario administrador de usuarios que es el editor del documento. Este valor de parámetro es opcional y puede ser nulo (si este parámetro es nulo, el valor del parámetro anterior debe ser `null`).
   * A `RMLocale` que especifica el valor locale (por ejemplo, `RMLocale.en`).
   * Un parámetro de salida de cadena que se utiliza para almacenar el valor del identificador de directiva.
   * Un parámetro de salida de cadena que se utiliza para almacenar el valor del identificador protegido por una directiva.
   * Un parámetro de salida de cadena que se utiliza para almacenar el tipo mime (por ejemplo, `application/pdf`).

   El `protectDocument` El método devuelve un valor `BLOB` que contiene el documento de PDF protegido por una directiva.

1. Guarde el documento del PDF.

   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento de PDF protegido por una directiva.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto que ha devuelto el `protectDocument` método. Rellene la matriz de bytes obteniendo el valor de `BLOB` del objeto `MTOM` miembro de datos.
   * Crear un `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte los siguientes tutoriales rápidos:

* &quot;Inicio rápido (MTOM): Aplicar una directiva a un documento de PDF mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Aplicar una directiva a un documento de PDF mediante la API de servicio web&quot;

## Quitar directivas de documentos de PDF {#removing-policies-from-pdf-documents}

Puede quitar una directiva de un documento protegido por una directiva para quitar la seguridad del documento. Es decir, si ya no desea que el documento esté protegido por una directiva. Si desea actualizar un documento protegido por una directiva con una directiva más reciente, en lugar de quitar la directiva y agregar la directiva actualizada, es más eficaz cambiar la directiva.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-4}

Para quitar una directiva de un documento de PDF protegido por una directiva, realice los siguientes pasos:

1. Incluir archivos de proyecto
1. Cree un objeto de la API de cliente de Document Security.
1. Recupere un documento de PDF protegido por una directiva.
1. Quite la directiva del documento de PDF.
1. Guarde el documento de PDF no protegido.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Document Security**

Para poder realizar mediante programación una operación del servicio Document Security, cree un objeto de cliente del servicio Document Security.

**Recuperar un documento de PDF protegido por una directiva**

Puede recuperar un documento de PDF protegido por una directiva para quitar una directiva. Si intenta quitar una directiva de un documento de PDF que no está protegido por una directiva, se producirá una excepción.

**Quitar la directiva del documento de PDF**

Puede quitar una directiva de un documento de PDF protegido por una directiva siempre que se especifique un administrador en la configuración de conexión. Si no es así, la directiva utilizada para proteger un documento debe contener la variable `SWITCH_POLICY` permiso para quitar una directiva de un documento de PDF. Además, el usuario especificado en la configuración de conexión de AEM Forms también debe tener ese permiso. De lo contrario, se produce una excepción.

**Guardar el documento de PDF no protegido**

Una vez que el servicio Document Security quita una directiva de un documento de PDF, puede guardar el documento de PDF no protegido como archivo de PDF.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicación de directivas a documentos de PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Eliminación de una directiva de un documento de PDF mediante la API de Java {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Elimine una directiva de un documento de PDF protegido por una directiva mediante la API de Document Security (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `DocumentSecurityClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Recupere un documento de PDF protegido por una directiva.

   * Crear un `java.io.FileInputStream` que representa el documento PDF protegido por una directiva utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento PDF.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Quite la directiva del documento de PDF.

   * Crear un `DocumentManager` invocando el objeto de `DocumentSecurityClient` del objeto `getDocumentManager` método.
   * Quitar una directiva del documento de PDF invocando el `DocumentManager` del objeto `removeSecurity` y pasando el `com.adobe.idp.Document` que contiene el documento de PDF protegido por una directiva. Este método devuelve un `com.adobe.idp.Document` que contiene un documento de PDF no protegido.

1. Guarde el documento de PDF no protegido.

   * Crear un `java.io.File` y asegúrese de que la extensión del archivo es PDF.
   * Invoque el `Document` del objeto `copyToFile` para copiar el contenido del `Document` al archivo (asegúrese de utilizar la variable `Document` objeto que ha devuelto el `removeSecurity` método).

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte los siguientes tutoriales rápidos:

* &quot;Inicio rápido (modo SOAP): Eliminación de una directiva de un documento de PDF mediante la API de Java&quot;

### Eliminación de una directiva mediante la API de servicio web {#remove-a-policy-using-the-web-service-api}

Quitar una directiva de un documento de PDF protegido por una directiva mediante la API de Document Security (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `DocumentSecurityServiceClient` mediante su constructor predeterminado.
   * Crear un `DocumentSecurityServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `DocumentSecurityServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere un documento de PDF protegido por una directiva.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el documento de PDF protegido por una directiva del que se elimina la directiva.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento de PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Quite la directiva del documento de PDF.

   Elimine la directiva del documento del PDF invocando el `DocumentSecurityServiceClient` del objeto `removePolicySecurity` y pasando el `BLOB` que contiene el documento de PDF protegido por una directiva. Este método devuelve un `BLOB` que contiene un documento de PDF no protegido.

1. Guarde el documento de PDF no protegido.

   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento de PDF no protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto que ha devuelto el `removePolicySecurity` método. Rellene la matriz de bytes obteniendo el valor de `BLOB` del objeto `MTOM` field.
   * Crear un `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream` objeto.

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte los siguientes tutoriales rápidos:

* &quot;Inicio rápido (MTOM): Quitar una directiva de un documento de PDF mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): eliminación de una directiva de un documento de PDF mediante la API de servicio web&quot;

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Revocar acceso a documentos {#revoking-access-to-documents}

Puede revocar el acceso a un documento PDF protegido por una directiva, lo que hace que todas las copias del documento sean inaccesibles para los usuarios. Cuando un usuario intenta abrir un documento de PDF revocado, se le redirige a una URL especificada donde se puede ver un documento revisado. La dirección URL a la que se redirige al usuario debe especificarse mediante programación. Cuando se anula el acceso a un documento, el cambio surte efecto la próxima vez que el usuario se sincronice con el servicio de Document Security abriendo el documento protegido por políticas en línea.

La capacidad de revocar el acceso a un documento proporciona seguridad adicional. Por ejemplo, supongamos que hay disponible una versión más reciente de un documento y que ya no desea que nadie vea la versión obsoleta. En este caso, el acceso al documento anterior se puede revocar y nadie puede ver el documento a menos que se restablezca el acceso.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-5}

Para revocar un documento protegido por una directiva, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de la API de cliente de Document Security.
1. Recupere un documento de PDF protegido por una directiva.
1. Revocar el documento protegido por una directiva.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Document Security**

Para poder realizar mediante programación una operación del servicio Document Security, debe crear un objeto de cliente del servicio Document Security.

**Recuperar un documento de PDF protegido por una directiva**

Recupere un documento de PDF protegido por una directiva para revocarlo. No puede revocar un documento que ya se haya revocado o que no sea un documento protegido por una directiva.

Si conoce el valor del identificador de licencia del documento protegido por una directiva, no es necesario recuperar el documento de PDF protegido por una directiva. Sin embargo, en la mayoría de los casos, debe recuperar el documento del PDF para obtener el valor del identificador de licencia.

**Revocar el documento protegido por una directiva**

Para revocar un documento protegido por una directiva, especifique el identificador de licencia del documento protegido por una directiva. Además, puede especificar la dirección URL de un documento que el usuario puede ver cuando intenta abrir el documento revocado. Es decir, supongamos que se revoca un documento obsoleto. Cuando un usuario intenta abrir el documento revocado, verá un documento actualizado en lugar del documento revocado.

>[!NOTE]
>
>Si intenta revocar un documento que ya está revocado, se produce una excepción.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicación de directivas a documentos de PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Restablecer el acceso a los documentos revocados](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Revocar acceso a documentos mediante la API de Java {#revoke-access-to-documents-using-the-java-api}

Revocar acceso a un documento de PDF protegido por una directiva mediante la API de Document Security (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de Document Security

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `DocumentSecurityClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Recuperar un documento de PDF protegido por una directiva

   * Crear un `java.io.FileInputStream` que representan el documento PDF protegido por una directiva utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento PDF.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Revocar el documento protegido por una directiva

   * Crear un `DocumentManager` invocando el objeto de `DocumentSecurityClient` del objeto `getDocumentManager` método.
   * Recupere el valor del identificador de licencia del documento protegido por políticas invocando el `DocumentManager` del objeto `getLicenseId` método. Pase el `com.adobe.idp.Document` que representa el documento protegido por una directiva. Este método devuelve un valor de cadena que representa el valor del identificador de licencia.
   * Crear un `LicenseManager` invocando el objeto de `DocumentSecurityClient` del objeto `getLicenseManager` método.
   * Revocar el documento protegido por una directiva invocando el `LicenseManager` del objeto `revokeLicense` y pasando los siguientes valores:

      * Un valor de cadena que especifica el valor del identificador de licencia del documento protegido por una directiva (especifique el valor devuelto del `DocumentManager` del objeto `getLicenseId` método).
      * Un miembro de datos estáticos de `License` que especifica el motivo para revocar el documento. Por ejemplo, puede especificar `License.DOCUMENT_REVISED`.
      * A `java.net.URL` valor que especifica la ubicación donde se encuentra un documento revisado. Si no desea redirigir a un usuario a otra dirección URL, puede pasar `null`.

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte los siguientes tutoriales rápidos:

* &quot;Inicio rápido (modo SOAP): Revocar un documento mediante la API de Java&quot;

### Revocar acceso a documentos mediante la API de servicio web {#revoke-access-to-documents-using-the-web-service-api}

Revocar acceso a un documento de PDF protegido por una directiva mediante la API de Document Security (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Crear un objeto de API de cliente de Document Security

   * Crear un `DocumentSecurityServiceClient` mediante su constructor predeterminado.
   * Crear un `DocumentSecurityServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `DocumentSecurityServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperar un documento de PDF protegido por una directiva

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar un documento de PDF protegido por una directiva que se ha revocado.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento de PDF protegido por una directiva que se va a revocar y el modo en que se va a abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Revocar el documento protegido por una directiva

   * Recupere el valor del identificador de licencia del documento protegido por políticas invocando el `DocumentSecurityServiceClient` del objeto `getLicenseID` y pasando el `BLOB` que representa el documento protegido por una directiva. Este método devuelve un valor de cadena que representa el identificador de licencia.
   * Revocar el documento protegido por una directiva invocando el `DocumentSecurityServiceClient` del objeto `revokeLicense` y pasando los siguientes valores:

      * Un valor de cadena que especifica el valor del identificador de licencia del documento protegido por una directiva (especifique el valor devuelto del `DocumentSecurityServiceService` del objeto `getLicenseId` método).
      * Un miembro de datos estáticos de `Reason` enumeración que especifica el motivo para revocar el documento. Por ejemplo, puede especificar `Reason.DOCUMENT_REVISED`.
      * A `string` que especifica la ubicación URL donde se encuentra un documento revisado. Si no desea redirigir a un usuario a otra dirección URL, puede pasar `null`.

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte los siguientes tutoriales rápidos:

* &quot;Inicio rápido (MTOM): Revocar un documento mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Revocar un documento mediante la API de servicio web&quot;

**Consulte también**

[Quitar directivas de documentos de Word](protecting-documents-policies.md#removing-policies-from-word-documents)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Restablecer el acceso a los documentos revocados {#reinstating-access-to-revoked-documents}

Puede restablecer el acceso a un documento de PDF revocado, lo que hace que todas las copias del documento revocado sean accesibles a los usuarios. Cuando un usuario abre un documento rehabilitado que se ha revocado, puede ver el documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-6}

Para restablecer el acceso a un documento de PDF revocado, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de la API de cliente de Document Security.
1. Recupere el identificador de licencia del documento de PDF revocado.
1. Restablezca el acceso al documento de PDF revocado.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Document Security**

Para poder realizar mediante programación una operación del servicio Document Security, debe crear un objeto de cliente del servicio Document Security. Si utiliza la API de Java, cree un `DocumentSecurityClient` objeto. Si utiliza la API del servicio web de Document Security, cree un `DocumentSecurityServiceService` objeto.

**Recuperar el identificador de licencia del documento de PDF revocado**

Recupere el identificador de licencia del documento de PDF revocado para restablecer un documento de PDF revocado. Después de obtener el valor del identificador de licencia, puede restablecer un documento revocado. Si intenta restablecer un documento que no se ha revocado, se producirá una excepción.

**Restablecer el acceso al documento de PDF revocado**

Para restablecer el acceso a un documento de PDF revocado, debe especificar el identificador de licencia del documento revocado. Si intenta restablecer el acceso a un documento de PDF que no se ha revocado, se producirá una excepción.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicación de directivas a documentos de PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Revocar acceso a documentos](protecting-documents-policies.md#revoking-access-to-documents)

### Restablecer el acceso a los documentos revocados mediante la API de Java {#reinstate-access-to-revoked-documents-using-the-java-api}

Restablezca el acceso a un documento revocado mediante la API de seguridad de los documentos (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `DocumentSecurityClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Recupere el identificador de licencia del documento de PDF revocado.

   * Crear un `java.io.FileInputStream` que representa el documento de PDF revocado utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento de PDF.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.
   * Crear un `DocumentManager` invocando el objeto de `DocumentSecurityClient` del objeto `getDocumentManager` método.
   * Recupere el valor del identificador de licencia del documento revocado invocando el `DocumentManager` del objeto `getLicenseId` y pasando el `com.adobe.idp.Document` que representa el documento revocado. Este método devuelve un valor de cadena que representa el identificador de licencia.

1. Restablezca el acceso al documento de PDF revocado.

   * Crear un `LicenseManager` invocando el objeto de `DocumentSecurityClient` del objeto `getLicenseManager` método.
   * Restablezca el acceso al documento de PDF revocado invocando el `LicenseManager` del objeto `unrevokeLicense` y pasar el valor del identificador de licencia del documento revocado.

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte los siguientes tutoriales rápidos:

* &quot;Inicio rápido (modo SOAP): Restablecer el acceso a un documento revocado mediante la API de servicio web&quot;

### Restablecer el acceso a los documentos revocados mediante la API del servicio web {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Restablezca el acceso a un documento revocado mediante la API de seguridad de los documentos (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `DocumentSecurityServiceClient` mediante su constructor predeterminado.
   * Crear un `DocumentSecurityServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `DocumentSecurityServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere el identificador de licencia del documento de PDF revocado.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar un documento de PDF revocado al que se restablece el acceso.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento de PDF revocado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Restablezca el acceso al documento de PDF revocado.

   * Recupere el valor del identificador de licencia del documento revocado invocando el `DocumentSecurityServiceClient` del objeto `getLicenseID` y pasando el `BLOB` que representa el documento revocado. Este método devuelve un valor de cadena que representa el identificador de licencia.
   * Restablezca el acceso al documento de PDF revocado invocando el `DocumentSecurityServiceClient` del objeto `unrevokeLicense` y pasando un valor de cadena que especifica el valor del identificador de licencia del documento de PDF revocado (pase el valor devuelto del `DocumentSecurityServiceClient` del objeto `getLicenseId` método).

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte los siguientes tutoriales rápidos:

* &quot;Inicio rápido (MTOM): Restablecer el acceso a un documento revocado mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Restablecer el acceso a un documento revocado mediante la API de servicio web&quot;

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Inspección de documentos de PDF protegidos por directivas {#inspecting-policy-protected-pdf-documents}

Puede utilizar la API del servicio de seguridad de los documentos (Java y servicio web) para inspeccionar documentos de PDF protegidos por políticas. La inspección de documentos de PDF protegidos por directivas devuelve información sobre el documento de PDF protegido por directivas. Por ejemplo, puede determinar la directiva que se utilizó para proteger el documento y la fecha en la que se protegió.

No puede realizar esta tarea si la versión del LiveCycle es 8.x o una versión anterior. La compatibilidad con la inspección de documentos protegidos por directivas se agrega en AEM Forms. Si intenta inspeccionar un documento protegido por una directiva mediante el LiveCycle 8.x (o una versión anterior), se genera una excepción.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-7}

Para inspeccionar un documento de PDF protegido por una directiva, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de la API de cliente de Document Security.
1. Recupere un documento protegido por una directiva para inspeccionarlo.
1. Obtenga información sobre el documento protegido por políticas.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Document Security**

Para poder realizar mediante programación una operación del servicio Document Security, cree un objeto de cliente del servicio Document Security. Si utiliza la API de Java, cree un `RightsManagementClient` objeto. Si utiliza la API del servicio web de Document Security, cree un `RightsManagementServiceService` objeto.

**Recuperar un documento protegido por una directiva para inspeccionarlo**

Para inspeccionar un documento protegido por una directiva, recupere el documento. Si intenta inspeccionar un documento que no está protegido con una directiva o que está revocado, se produce una excepción.

**Inspect el documento**

Después de recuperar un documento protegido por una directiva, puede inspeccionarlo.

**Obtener información sobre el documento protegido por políticas**

Después de inspeccionar un documento de PDF protegido por una directiva, puede obtener información sobre él. Por ejemplo, puede determinar la directiva que se utiliza para proteger el documento.

Si protege un documento con una directiva que pertenece a Mis directivas y, a continuación, llama a `RMInspectResult.getPolicysetName` o `RMInspectResult.getPolicysetId`, se devuelve nulo.

Si el documento está protegido mediante una directiva incluida en un conjunto de directivas (que no sea Mis directivas), `RMInspectResult.getPolicysetName` y `RMInspectResult.getPolicysetId` devuelve cadenas válidas.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Documentos de PDF protegidos por directivas de Inspect que utilizan la API de Java {#inspect-policy-protected-pdf-documents-using-the-java-api}

Inspect crea un documento de PDF protegido por políticas mediante la API del servicio de seguridad de los documentos (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java. Para obtener información acerca de la ubicación de estos archivos, consulte [Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión. (Consulte [Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crear un `RightsManagementClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Recupere un documento protegido por una directiva para inspeccionarlo.

   * Crear un `java.io.FileInputStream` que representa el documento PDF protegido por una directiva mediante su constructor. Pase un valor de cadena que especifique la ubicación del documento del PDF.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Inspect el documento.

   * Crear un `DocumentManager` invocando el objeto de `RightsManagementClient` del objeto `getDocumentManager` método.
   * Inspect el documento protegido por políticas invocando el `LicenseManager` del objeto `inspectDocument` método. Pase el `com.adobe.idp.Document` que contiene el documento de PDF protegido por una directiva. Este método devuelve un `RMInspectResult` que contiene información sobre el documento protegido por una directiva.

1. Obtenga información sobre el documento protegido por políticas.

   Para obtener información sobre el documento protegido por una directiva, invoque el método apropiado que pertenece a `RMInspectResult` objeto. Por ejemplo, para recuperar el nombre de la directiva, invoque el `RMInspectResult` del objeto `getPolicyName` método.

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte los siguientes tutoriales rápidos:

* &quot;Inicio rápido (modo SOAP): Inspección de documentos de PDF protegidos por directivas mediante la API de Java&quot;

### Documentos de PDF protegidos por directivas de Inspect que utilizan la API de servicio web {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Inspect crea un documento de PDF protegido por políticas mediante la API del servicio de seguridad de los documentos (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `RightsManagementServiceClient` mediante su constructor predeterminado.
   * Crear un `RightsManagementServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `RightsManagementServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere un documento protegido por una directiva para inspeccionarlo.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar un documento de PDF para inspeccionar.
   * Crear un `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento de PDF y el modo para abrir el archivo en.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` método. Pase la matriz de bytes, la posición inicial y la longitud de la secuencia a leer.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Inspect el documento.

   Inspect el documento protegido por políticas invocando el `RightsManagementServiceClient` del objeto `inspectDocument` método. Pase el `BLOB` que contiene el documento de PDF protegido por una directiva. Este método devuelve un `RMInspectResult` que contiene información sobre el documento protegido por una directiva.

1. Obtenga información sobre el documento protegido por políticas.

   Para obtener información sobre el documento protegido por una directiva, obtenga el valor del campo correspondiente que pertenece a `RMInspectResult` objeto. Por ejemplo, para recuperar el nombre de la directiva, obtenga el valor de `RMInspectResult` del objeto `policyName` field.

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte los siguientes tutoriales rápidos:

* &quot;Inicio rápido (MTOM): Inspección de documentos de PDF protegidos por directivas mediante la API del servicio web&quot;
* &quot;Inicio rápido (SwaRef): Inspección de documentos de PDF protegidos por directivas mediante la API del servicio web&quot;

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Creación de marcas de agua {#creating-watermarks}

Las marcas de agua ayudan a garantizar la seguridad de un documento al identificarlo de forma única y controlar la infracción de derechos de autor. Por ejemplo, puede crear y colocar una marca de agua que indique Confidencial en todas las páginas de un documento. Una vez creada una marca de agua, puede incluirla como parte de una directiva. Es decir, puede establecer el atributo de marca de agua de la directiva con la marca de agua recién creada. Después de aplicar a un documento una directiva que contiene una marca de agua, esta aparece en el documento protegido por una directiva.

>[!NOTE]
>
>Solo los usuarios con privilegios administrativos de Document Security pueden crear marcas de agua. Es decir, debe especificar dicho usuario al definir la configuración de conexión necesaria para crear un objeto de cliente del servicio de Document Security.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-8}

Para crear una marca de agua, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de la API de cliente de Document Security.
1. Establezca los atributos de marcas de agua.
1. Registre la marca de agua con el servicio Document Security.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Document Security**

Para poder realizar mediante programación una operación del servicio Document Security, debe crear un objeto de cliente del servicio Document Security. Si utiliza la API de Java, cree un `RightsManagementClient` objeto. Si utiliza la API del servicio web de Document Security, cree un `RightsManagementServiceService` objeto.

**Establecer los atributos de marcas de agua**

Para crear una marca de agua, debe establecer los atributos de la marca de agua. El atributo name siempre debe estar definido. Además del atributo name, debe establecer al menos uno de los atributos siguientes:

* Texto personalizado
* DateIncluded
* UserIdIncluded
* UserNameIncluded

En la tabla siguiente se enumeran los pares de clave y valor necesarios al crear una marca de agua mediante servicios web.

<table>
 <thead>
  <tr>
   <th><p>Nombre de clave</p></th>
   <th><p>Descripción</p></th>
   <th><p>Valor</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERNAME_ENABLED</code></p></td>
   <td><p>Especifica si el nombre de usuario del usuario que abre el documento forma parte de la marca de agua.</p></td>
   <td><p>Verdadero o falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td>
   <td><p>Especifica si la identificación del usuario que abre el documento forma parte de la marca de agua.</p></td>
   <td><p>Verdadero o falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>Especifica si la fecha actual forma parte de la marca de agua.</p></td>
   <td><p>Verdadero o falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>Si este valor es true, el valor del texto personalizado debe especificarse usando <code>WaterBackCmd:SRCTEXT</code>.</p></td>
   <td><p>Verdadero o falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>Especifica la opacidad de la marca de agua. El valor predeterminado es 0,5 si no se especifica.</p></td>
   <td><p>Un valor entre 0,0 y 1,0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>Especifica el giro de la marca de agua. El valor predeterminado es 0 grados.</p></td>
   <td><p>Un valor entre 0 y 359.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>Si se especifica este valor, entonces <code>WaterBackCmd:IS_SIZE_ENABLED</code> debe estar presente y el valor debe ser verdadero. Si no se especifica este atributo, el comportamiento predeterminado se ajusta a la página.</p></td>
   <td><p>Un valor mayor que 0,0 y menor o igual que 1,0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>Especifica la alineación horizontal de la marca de agua. El valor predeterminado es centro.</p></td>
   <td><p>izquierda, centro o derecha</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>Especifica la alineación vertical de la marca de agua. El valor predeterminado es centro.</p></td>
   <td><p>superior, centro o inferior</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>Especifica si la marca de agua es un fondo. El valor predeterminado es False.</p></td>
   <td><p>Verdadero o falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>True si se especifica una escala personalizada. Si este valor es true, también se debe especificar SCALE. Si este valor es false, el valor predeterminado se ajusta a la página.</p></td>
   <td><p>Verdadero o falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>Especifica el texto personalizado de una marca de agua. Si este valor está presente, <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> también debe estar presente y debe establecerse como verdadero.</p></td>
   <td><p>Verdadero o falso</p></td>
  </tr>
 </tbody>
</table>

Todas las marcas de agua deben tener uno de los atributos siguientes definidos:

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

Todos los demás atributos son opcionales.

**Registrar la marca de agua**

Se debe registrar una nueva marca de agua con el servicio Document Security para poder utilizarla. Después de registrar una marca de agua, puede utilizarla dentro de las directivas.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicación de directivas a documentos de PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Creación de marcas de agua mediante la API de Java {#create-watermarks-using-the-java-api}

Crear una marca de agua mediante la API de seguridad de los documentos (Java):

1. Incluir archivos de proyecto.

   Incluir archivos JAR de cliente, como `adobe-rightsmanagement-client.jar`, en la ruta de clase del proyecto Java.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `RightsManagementClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Definir los atributos de filigrana

   * Crear un `Watermark` invocando el objeto de `InfomodelObjectFactory` objeto estático `createWatermark` método. Este método devuelve un `Watermark` objeto.
   * Establezca el atributo name de la marca de agua invocando la variable `Watermark` del objeto `setName` y pasando un valor de cadena que especifica el nombre de la directiva.
   * Establezca el atributo de fondo de la marca de agua invocando la variable `Watermark` del objeto `setBackground` método y paso `true`. Al establecer este atributo, la marca de agua aparece en segundo plano del documento.
   * Establezca el atributo de texto personalizado de la marca de agua invocando la variable `Watermark` del objeto `setCustomText` y pasando un valor de cadena que representa el texto de la marca de agua.
   * Establezca el atributo de opacidad de la marca de agua invocando la variable `Watermark` del objeto `setOpacity` y pasando un valor entero que especifica el nivel de opacidad. El valor 100 indica que la marca de agua es completamente opaca y el valor 0 indica que es completamente transparente.

1. Registre la marca de agua.

   * Crear un `WatermarkManager` invocando el objeto de `RightsManagementClient` del objeto `getWatermarkManager` método. Este método devuelve un `WatermarkManager` objeto.
   * Registre la marca de agua invocando el `WatermarkManager` del objeto `registerWatermark` y pasando el `Watermark` que representa la marca de agua que se va a registrar. Este método devuelve un valor de cadena que representa el valor de identificación de la marca de agua.

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte los siguientes tutoriales rápidos:

* &quot;Inicio rápido (modo SOAP): Creación de una marca de agua mediante la API de Java&quot;

### Creación de marcas de agua mediante la API de servicio web {#create-watermarks-using-the-web-service-api}

Crear una marca de agua mediante la API de Document Security (servicio web):

1. Cree un objeto de la API de cliente de Document Security.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `RightsManagementServiceClient` mediante su constructor predeterminado.
   * Crear un `RightsManagementServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `RightsManagementServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Establezca los atributos de marca de agua.

   * Crear un `WatermarkSpec` invocando el objeto de `WatermarkSpec` constructor.
   * Establezca el nombre de la marca de agua asignando un valor de cadena al `WatermarkSpec` del objeto `name` miembro de datos.
   * Establecer la marca de agua `id` al asignar un valor de cadena a la variable `WatermarkSpec` del objeto `id` miembro de datos.
   * Para cada propiedad de marca de agua que se va a establecer, cree una `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Establezca el valor clave asignando un valor a la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` miembro de datos (por ejemplo, `WaterBackCmd:OPACITY)`.
   * Establezca el valor asignando un valor a `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` miembro de datos (por ejemplo, `.25`).
   * Crear un `MyArrayOf_xsd_anyType` objeto. Para cada `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto, invoque el `MyArrayOf_xsd_anyType` del objeto `Add` método. Pase el `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Asigne el `MyArrayOf_xsd_anyType` objeto a `WatermarkSpec` del objeto `values` miembro de datos.

1. Registre la marca de agua.

   Registre la marca de agua invocando el `RightsManagementServiceClient` del objeto `registerWatermark` y pasando el `WatermarkSpec` que representa la marca de agua que se va a registrar.

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte los siguientes tutoriales rápidos:

* &quot;Inicio rápido (MTOM): Creación de una marca de agua mediante la API del servicio web&quot;
* &quot;Inicio rápido (SwaRef): Creación de una marca de agua mediante la API del servicio web&quot;

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modificación de marcas de agua {#modifying-watermarks}

Puede modificar una marca de agua existente mediante la API de Java o la API del servicio web de Document Security. Para cambiar una marca de agua existente, debe recuperarla, modificar sus atributos y, a continuación, actualizarla en el servidor. Por ejemplo, supongamos que recupera una marca de agua y modifica su atributo de opacidad. Antes de que el cambio surta efecto, debe actualizar la marca de agua.

Al modificar una marca de agua, el cambio afecta a los documentos futuros a los que se les haya aplicado dicha marca. Es decir, los documentos de PDF existentes que contienen la marca de agua no se ven afectados.

>[!NOTE]
>
>Solo los usuarios con privilegios administrativos de Document Security pueden modificar las marcas de agua. Es decir, debe especificar dicho usuario al definir la configuración de conexión necesaria para crear un objeto de cliente del servicio de Document Security.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-9}

Para modificar una marca de agua, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de la API de cliente de Document Security.
1. Recupere la marca de agua que desea modificar.
1. Establezca los atributos de marcas de agua.
1. Actualice la marca de agua.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Document Security**

Para poder realizar mediante programación una operación del servicio Document Security, debe crear un objeto de cliente del servicio Document Security. Si utiliza la API de Java, cree un `DocumentSecurityClient` objeto. Si utiliza la API del servicio web de Document Security, cree un `DocumentSecurityServiceService` objeto.

**Recuperar la marca de agua que desea modificar**

Para modificar una marca de agua, debe recuperar una marca de agua existente. Puede recuperar una marca de agua especificando su nombre o su valor identificador.

**Establecer los atributos de marcas de agua**

Para modificar una marca de agua existente, cambie el valor de uno o varios atributos de marca de agua. Al actualizar mediante programación una marca de agua mediante un servicio web, debe establecer todos los atributos que se establecieron originalmente, aunque el valor no cambie. Por ejemplo, supongamos que se establecen los siguientes atributos de marca de agua: `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY`, y `WaterBackCmd:SRCTEXT`. Aunque el único atributo que desea modificar es `WaterBackCmd:OPACITY`, debe establecer que los demás valores estén bien.

>[!NOTE]
>
>Al utilizar la API de Java para modificar una marca de agua, no es necesario especificar todos los atributos. Establezca el atributo de marca de agua que desea modificar.

>[!NOTE]
>
>Para obtener información sobre los nombres de atributos de marca de agua, consulte [Creación de marcas de agua](protecting-documents-policies.md#creating-watermarks).

**Actualizar la marca de agua**

Después de modificar los atributos de una marca de agua, debe actualizarla.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Creación de marcas de agua](protecting-documents-policies.md#creating-watermarks)

### Modificación de marcas de agua mediante la API de Java {#modify-watermarks-using-the-java-api}

Modifique una marca de agua mediante la API de seguridad de los documentos (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `DocumentSecurityClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Recupere la marca de agua que desea modificar.

   Crear un `WatermarkManager` invocando el objeto de `DocumentSecurityClient` del objeto `getWatermarkManager` y pasar un valor de cadena que especifique el nombre de la marca de agua. Este método devuelve un `Watermark` que representa la marca de agua que se va a modificar.

1. Establezca los atributos de marca de agua.

   Establezca el atributo de opacidad de la marca de agua invocando la variable `Watermark` del objeto `setOpacity` y pasando un valor entero que especifica el nivel de opacidad. El valor 100 indica que la marca de agua es completamente opaca y el valor 0 indica que es completamente transparente.

   >[!NOTE]
   >
   >En este ejemplo se modifica únicamente el atributo opacity.

1. Actualice la marca de agua.

   * Actualice la marca de agua invocando el `WatermarkManager` del objeto `updateWatermark` y pase el `Watermark` objeto cuyo atributo se ha modificado.

**Ejemplos de código**

Para obtener ejemplos de código utilizando el servicio Document Security, consulte Inicio rápido (modo SOAP): Modificación de una marca de agua mediante la sección API de Java.

### Modificación de marcas de agua mediante la API de servicio web {#modify-watermarks-using-the-web-service-api}

Modificar una marca de agua mediante la API de seguridad de los documentos (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `DocumentSecurityServiceClient` mediante su constructor predeterminado.
   * Crear un `RightsManagementServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `DocumentSecurityServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere la marca de agua que desea modificar.

   Recupere la marca de agua que desea modificar invocando el `DocumentSecurityServiceClient` del objeto `getWatermarkByName` método. Pase un valor de cadena que especifique el nombre de la marca de agua. Este método devuelve un `WatermarkSpec` que representa la marca de agua que se va a modificar.

1. Establezca los atributos de marca de agua.

   * Para que se actualice cada propiedad de marca de agua, cree una `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Establezca el valor clave asignando un valor a la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` miembro de datos (por ejemplo, `WaterBackCmd:OPACITY)`.
   * Establezca el valor asignando un valor a `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` miembro de datos (por ejemplo, `.50`).
   * Crear un `MyArrayOf_xsd_anyType` objeto. Para cada `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto, invoque el `MyArrayOf_xsd_anyType` del objeto `Add` método. Pase el `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Asigne el `MyArrayOf_xsd_anyType` objeto a `WatermarkSpec` del objeto `values` miembro de datos.

1. Actualice la marca de agua.

   Actualice la marca de agua invocando el `DocumentSecurityServiceClient` del objeto `updateWatermark` y pasando el `WatermarkSpec` que representa la marca de agua que se va a modificar.

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte el siguiente Inicio rápido:

* &quot;Inicio rápido (MTOM): Modificación de una marca de agua mediante la API del servicio web&quot;

## Búsqueda de eventos {#searching-for-events}

El servicio Rights Management realiza un seguimiento de acciones específicas a medida que se producen, como aplicar una directiva a un documento, abrir un documento protegido por una directiva y revocar el acceso a documentos. La auditoría de eventos debe estar habilitada para el servicio de Rights Management o no se realiza un seguimiento de los eventos.

Los eventos se clasifican en una de las siguientes categorías:

* Los eventos de administrador son acciones relacionadas con un administrador, como crear una cuenta de administrador.
* Los eventos de documento son acciones relacionadas con un documento, como cerrar un documento protegido por una directiva.
* Los eventos de directiva son acciones relacionadas con una directiva, como crear una directiva.
* Los eventos de servicio son acciones relacionadas con el servicio de Rights Management, como la sincronización con el directorio de usuario.

Puede buscar eventos específicos utilizando la API de Java de Rights Management o la API del servicio web. Al buscar eventos, puede realizar tareas como, por ejemplo, crear un archivo de registro de ciertos eventos.

>[!NOTE]
>
>Para obtener más información sobre el servicio Rights Management, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-10}

Para buscar un evento de Rights Management, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Rights Management.
1. Especifique el evento para el que desea buscar.
1. Busque el evento.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Rights Management**

Para poder realizar mediante programación una operación de servicio de Rights Management, debe crear un objeto de cliente de servicio de Rights Management. Si utiliza la API de Java, cree un `DocumentSecurityClient` objeto. Si utiliza la API del servicio web de Rights Management, cree un `DocumentSecurityServiceService` objeto.

**Especifique los eventos que desea buscar**

Especifique el evento que desea buscar. Por ejemplo, puede buscar el evento de creación de directivas, que se produce cuando se crea una directiva nueva.

**Buscar el evento**

Una vez especificado el evento que se va a buscar, se puede utilizar la API de Java de Rights Management o la API del servicio web de Rights Management para buscar el evento.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Búsqueda de eventos mediante la API de Java {#search-for-events-using-the-java-api}

Busque eventos mediante la API de Rights Management (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de Rights Management

   Crear un `DocumentSecurityClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. Especifique los eventos que desea buscar

   * Crear un `EventManager` invocando el objeto de `DocumentSecurityClient` del objeto `getEventManager` método. Este método devuelve un `EventManager` objeto.
   * Crear un `EventSearchFilter` invocando su constructor.
   * Especifique el evento para el que desea buscar invocando el `EventSearchFilter` del objeto `setEventCode` y pasando un miembro de datos estáticos que pertenece al método `EventManager` que representa el evento para el que se va a buscar. Por ejemplo, para buscar el evento de creación de directivas, apruebe `EventManager.POLICY_CREATE_EVENT`.

   >[!NOTE]
   >
   >Puede definir criterios de búsqueda adicionales invocando `EventSearchFilter` métodos de objeto. Por ejemplo, invoque el `setUserName` para especificar un usuario asociado al evento.

1. Buscar el evento

   Busque el evento invocando la variable `EventManager` del objeto `searchForEvents` y pasando el `EventSearchFilter` que define los criterios de búsqueda de eventos. Este método devuelve una matriz de `Event` objetos.

**Ejemplos de código**

Para obtener ejemplos de código utilizando el servicio Rights Management, consulte los siguientes tutoriales rápidos:

* &quot;Inicio rápido (SOAP): Búsqueda de eventos mediante la API de Java&quot;

### Búsqueda de eventos mediante la API de servicio web {#search-for-events-using-the-web-service-api}

Busque eventos mediante la API de Rights Management (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Crear un objeto de API de cliente de Rights Management

   * Crear un `DocumentSecurityServiceClient` mediante su constructor predeterminado.
   * Crear un `DocumentSecurityServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `DocumentSecurityServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Especifique los eventos que desea buscar

   * Crear un `EventSpec` mediante su constructor.
   * Especifique el inicio del período de tiempo durante el cual se produjo el evento configurando la variable `EventSpec` del objeto `firstTime.date` miembro de datos con `DataTime` que representa el inicio del intervalo de fechas en el que se produjo el evento.
   * Asignar el valor `true` a la `EventSpec` del objeto `firstTime.dateSpecified` miembro de datos.
   * Especifique el final del período de tiempo durante el cual se produjo el evento configurando la variable `EventSpec` del objeto `lastTime.date` miembro de datos con `DataTime` que representa el final del intervalo de fechas en el que se produjo el evento.
   * Asignar el valor `true` a la `EventSpec` del objeto `lastTime.dateSpecified` miembro de datos.
   * Configure el evento que desea buscar asignando un valor de cadena a `EventSpec` del objeto `eventCode` miembro de datos. En la tabla siguiente se enumeran los valores numéricos que puede asignar a esta propiedad:

   <table>
    <thead>
    <tr>
    <th><p>Tipo de evento</p></th>
    <th><p>Valor</p></th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td><p><code>ALL_EVENTS</code></p></td>
    <td><p>999</p></td>
    </tr>
    <tr>
    <td><p><code>USER_CHANGE_PASSWORD_EVENT</code></p></td>
    <td><p>1000</p></td>
    </tr>
    <tr>
    <td><p><code>USER_REGISTER_EVENT</code></p></td>
    <td><p>1001</p></td>
    </tr>
    <tr>
    <td><p><code>USER_PREREGISTER_EVENT</code></p></td>
    <td><p>1002</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACTIVATE_EVENT</code></p></td>
    <td><p>1003</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DEACTIVATE_EVENT</code></p></td>
    <td><p>1004</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_EVENT</code></p></td>
    <td><p>1005</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_DENY_EVENT </code></p></td>
    <td><p>1006</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACCOUNT_LOCK_EVENT</code></p></td>
    <td><p>1007</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DELETE_EVENT </code></p></td>
    <td><p>1008</p></td>
    </tr>
    <tr>
    <td><p><code>USER_UPDATE_PROFILE_EVENT </code></p></td>
    <td><p>1009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_VIEW_EVENT </code></p></td>
    <td><p>2000</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_LOW_EVENT </code></p></td>
    <td><p>2001</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_HIGH_EVENT </code></p></td>
    <td><p>2002</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SIGN_EVENT </code></p></td>
    <td><p>2003</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_ADD_ANNOTATION_EVENT </code></p></td>
    <td><p>2004</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_FORM_FILL_EVENT </code></p></td>
    <td><p>2005</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CLOSE_EVENT </code></p></td>
    <td><p>2006</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_MODIFY_EVENT </code></p></td>
    <td><p>2007</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_SECURITY_HANDLER_EVENT </code></p></td>
    <td><p>2008</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SWITCH_POLICY_EVENT </code></p></td>
    <td><p>2009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_REVOKE_EVENT </code></p></td>
    <td><p>2010</p></td>
    </tr>
    <tr>
    <td><p><code>$1</code></p></td>
    <td><p>2011</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SECURE_EVENT </code></p></td>
    <td><p>2012</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_UNKNOWN_CLIENT_EVENT </code></p></td>
    <td><p>2013</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_REVOKE_URL_EVENT </code></p></td>
    <td><p>2014</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_EVENT </code></p></td>
    <td><p>3000</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_ENABLE_EVENT </code></p></td>
    <td><p>3001</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DISABLE_EVENT </code></p></td>
    <td><p>3002</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CREATE_EVENT </code></p></td>
    <td><p>3003</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DELETE_EVENT </code></p></td>
    <td><p>3004</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_OWNER_EVENT </code></p></td>
    <td><p>3005</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CLIENT_SYNC_EVENT </code></p></td>
    <td><p>4000</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_INFO_EVENT </code></p></td>
    <td><p>4001</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_COMPLETE_EVENT </code></p></td>
    <td><p>4002</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_VERSION_MISMATCH_EVENT </code></p></td>
    <td><p>4003</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CONFIG_CHANGE_EVENT </code></p></td>
    <td><p>4004</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_ENABLE_OFFLINE_ACCESS_EVENT </code></p></td>
    <td><p>4005</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ADD_EVENT </code></p></td>
    <td><p>5000</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DELETE_EVENT </code></p></td>
    <td><p>5001</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_EDIT_EVENT </code></p></td>
    <td><p>5002</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ACTIVATE_EVENT </code></p></td>
    <td><p>5003</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DEACTIVATE_EVENT </code></p></td>
    <td><p>5004</p></td>
    </tr>
    <tr>
    <td><p><code>ERROR_DIRECTORY_SERVICE_EVENT </code></p></td>
    <td><p>6000</p></td>
    </tr>
    <tr>
    <td><p><code>CREATED_POLICYSET_EVENT</code></p></td>
    <td><p>7000</p></td>
    </tr>
    <tr>
    <td><p><code>DELETED_POLICYSET_EVENT</code></p></td>
    <td><p>7001</p></td>
    </tr>
    <tr>
    <td><p><code>MODIFIED_POLICYSET_EVENT</code></p></td>
    <td><p>7002</p></td>
    </tr>
    </tbody>
    </table>

1. Buscar el evento

   Busque el evento invocando la variable `DocumentSecurityServiceClient` del objeto `searchForEvents` y pasando el `EventSpec` que representa el evento que se va a buscar y el número máximo de resultados. Este método devuelve un `MyArrayOf_xsd_anyType` colección donde cada elemento es un `AuditSpec` ejemplo. Uso de un `AuditSpec` Por ejemplo, puede obtener información sobre el evento, como la hora en que se produjo. El `AuditSpec` La instancia contiene un `timestamp` miembro de datos que especifica esta información.

**Ejemplos de código**

Para obtener ejemplos de código utilizando el servicio Rights Management, consulte los siguientes tutoriales rápidos:

* &quot;Inicio rápido (MTOM): Búsqueda de eventos mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Búsqueda de eventos mediante la API del servicio web&quot;

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Aplicar directivas a documentos de Word {#applying-policies-to-word-documents}

Además de los documentos de PDF, el servicio Rights Management admite formatos de documento adicionales, como un documento de Microsoft Word (archivo DOC) y otros formatos de archivo de Microsoft Office. Por ejemplo, puede aplicar una directiva a un documento de Word para protegerlo. Al aplicar una directiva a un documento de Word, se restringe el acceso al documento. No puede aplicar una directiva a un documento si éste ya está protegido con una directiva.

Puede supervisar el uso de un documento de Word protegido por una directiva después de distribuirlo. Es decir, puede ver cómo se utiliza el documento y quién lo está utilizando. Por ejemplo, puede averiguar cuándo alguien ha abierto el documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-11}

Para aplicar una directiva a un documento de Word, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de la API de cliente de Document Security.
1. Recuperar un documento de Word al que se aplica una directiva.
1. Aplicar una directiva existente al documento de Word.
1. Guarde el documento de Word protegido por una directiva.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto API de cliente de Document Security**

Para poder realizar mediante programación una operación del servicio Document Security, debe crear un objeto de cliente del servicio Document Security.

**Recuperar un documento de Word**

Recuperar un documento de Word para aplicar una directiva. Después de aplicar una directiva al documento de Word, los usuarios están restringidos al utilizar el documento. Por ejemplo, si la directiva no permite abrir el documento sin conexión, los usuarios deben estar en línea para abrirlo.

**Aplicar una directiva existente al documento de Word**

Para aplicar una directiva a un documento de Word, debe hacer referencia a una directiva existente y especificar a qué conjunto de directivas pertenece la directiva. El usuario que configura las propiedades de conexión debe tener acceso a la directiva especificada. Si no es así, se produce una excepción.

**Guardar el documento de Word**

Una vez que el servicio Document Security aplica una directiva a un documento de Word, puede guardar el documento de Word protegido por directivas como un archivo DOC.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revocar acceso a documentos](protecting-documents-policies.md#revoking-access-to-documents)

### Aplicar una directiva a un documento de Word mediante la API de Java {#apply-a-policy-to-a-word-document-using-the-java-api}

Aplicar una directiva a un documento de Word mediante la API de Document Security (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `DocumentSecurityClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Recupere un documento de Word.

   * Crear un `java.io.FileInputStream` que representa el documento de Word utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento de Word.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Aplicar una directiva existente al documento de Word.

   * Crear un `DocumentManager` invocando el objeto de `DocumentSecurityClient` del objeto `getDocumentManager` método.
   * Aplicar una directiva al documento de Word invocando la variable `DocumentManager` del objeto `protectDocument` y pasando los siguientes valores:

      * El `com.adobe.idp.Document` que contiene el documento de Word al que se aplica la directiva.
      * Valor de cadena que especifica el nombre del documento.
      * Valor de cadena que especifica el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar un `null` que resulta en el `MyPolicies` conjunto de directivas en uso.
      * Valor de cadena que especifica el nombre de la directiva.
      * Valor de cadena que representa el nombre del dominio del administrador de usuarios del usuario que es el editor del documento. Este valor de parámetro es opcional y puede ser nulo (si este parámetro es nulo, el siguiente valor de parámetro debe ser nulo).
      * Valor de cadena que representa el nombre canónico del usuario administrador de usuarios que es el editor del documento. Este valor de parámetro es opcional y puede ser `null` (si este parámetro es `null`, el valor del parámetro anterior debe ser `null`).
      * A `com.adobe.livecycle.rightsmanagement.Locale` que representa la configuración regional utilizada para seleccionar la plantilla de MS Office. Este valor de parámetro es opcional y puede especificar `null`.

     El `protectDocument` El método devuelve un valor `RMSecureDocumentResult` que contiene el documento de Word protegido por una directiva.

1. Guarde el documento de Word.

   * Invoque el `RMSecureDocumentResult` del objeto `getProtectedDoc` para obtener el documento de Word protegido por una directiva. Este método devuelve un `com.adobe.idp.Document` objeto.
   * Crear un `java.io.File` y asegúrese de que la extensión del archivo es DOC.
   * Invoque el `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del `Document` al archivo (asegúrese de utilizar la variable `Document` objeto que ha devuelto el `getProtectedDoc` método).

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte el siguiente Inicio rápido:

* &quot;Inicio rápido (modo SOAP): Aplicar una directiva a un documento de Word mediante la API de Java&quot;

### Aplicar una directiva a un documento de Word mediante la API de servicio web {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Aplicar una directiva a un documento de Word mediante la API de Document Security (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto de la API de cliente de Document Security.

   * Crear un `DocumentSecurityServiceClient` mediante su constructor predeterminado.
   * Crear un `DocumentSecurityServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `DocumentSecurityServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere un documento de Word.

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar un documento de Word al que se aplica una directiva.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento de Word y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Determinar el tamaño de la matriz de bytes obteniendo `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` método. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Aplicar una directiva existente al documento de Word.

   Aplicar una directiva al documento de Word invocando la variable `DocumentSecurityServiceClient` del objeto `protectDocument` y pasando los siguientes valores:

   * El `BLOB` que contiene el documento de Word al que se aplica la directiva.
   * Valor de cadena que especifica el nombre del documento.
   * Valor de cadena que especifica el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar un `null` que resulta en el `MyPolicies` conjunto de directivas en uso.
   * Valor de cadena que especifica el nombre de la directiva.
   * Valor de cadena que representa el nombre del dominio del administrador de usuarios del usuario que es el editor del documento. Este valor de parámetro es opcional y puede ser nulo (si este parámetro es nulo, el siguiente valor de parámetro debe ser `null`).
   * Valor de cadena que representa el nombre canónico del usuario administrador de usuarios que es el editor del documento. Este valor de parámetro es opcional y puede ser nulo (si este parámetro es nulo, el valor del parámetro anterior debe ser `null`).
   * A `RMLocale` que especifica el valor locale (por ejemplo, `RMLocale.en`).
   * Un parámetro de salida de cadena que se utiliza para almacenar el valor del identificador de directiva.
   * Un parámetro de salida de cadena que se utiliza para almacenar el valor del identificador protegido por una directiva.
   * Un parámetro de salida de cadena que se utiliza para almacenar el tipo mime (por ejemplo, `application/doc`).

   El `protectDocument` El método devuelve un valor `BLOB` que contiene el documento de Word protegido por una directiva.

1. Guarde el documento de Word.

   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento de Word protegido por una directiva.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto que ha devuelto el `protectDocument` método. Rellene la matriz de bytes obteniendo el valor de `BLOB` del objeto `MTOM` miembro de datos.
   * Crear un `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de Word invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte el siguiente Inicio rápido:

* &quot;Inicio rápido (MTOM): Aplicar una directiva a un documento de Word mediante la API de servicio web&quot;

## Quitar directivas de documentos de Word {#removing-policies-from-word-documents}

Puede quitar una directiva de un documento de Word protegido por una directiva para quitar la seguridad del documento. Es decir, si ya no desea que el documento esté protegido por una directiva. Si desea actualizar un documento de Word protegido por una directiva con una directiva más reciente, en lugar de quitar la directiva y agregar la directiva actualizada, es más eficaz cambiar la directiva.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-12}

Para quitar una directiva de un documento de Word protegido por una directiva, realice los siguientes pasos:

1. Incluir archivos de proyecto
1. Cree un objeto de la API de cliente de Document Security.
1. Recupere un documento de Word protegido por una directiva.
1. Quitar la directiva del documento de Word.
1. Guardar los documentos de Word no protegidos

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Document Security**

Para poder realizar mediante programación una operación del servicio Document Security, cree un objeto de cliente del servicio Document Security.

**Recuperar un documento de Word protegido por una directiva**

Recupere un documento de Word protegido por una directiva para quitar una directiva. Si intenta quitar una directiva de un documento de Word que no está protegido por una directiva, se producirá una excepción.

**Quitar la directiva del documento de Word**

Puede quitar una directiva de un documento de Word protegido por una directiva siempre que se especifique un administrador en la configuración de conexión. Si no es así, la directiva utilizada para proteger un documento debe contener la variable `SWITCH_POLICY` permiso para quitar una directiva de un documento de Word. Además, el usuario especificado en la configuración de conexión de AEM Forms también debe tener ese permiso. De lo contrario, se produce una excepción.

**Guardar el documento de Word no protegido**

Una vez que el servicio Document Security quita una directiva de un documento de Word, puede guardar el documento de Word no protegido como un archivo DOC.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicar directivas a documentos de Word](protecting-documents-policies.md#applying-policies-to-word-documents)

### Quitar una directiva de un documento de Word mediante la API de Java {#remove-a-policy-from-a-word-document-using-the-java-api}

Quitar una directiva de un documento de Word protegido por una directiva mediante la API de Document Security (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de Document Security

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `RightsManagementClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Recuperar un documento de Word protegido por una directiva

   * Crear un `java.io.FileInputStream` que representa el documento de Word protegido por una directiva utilizando su constructor y pasando un valor de cadena que especifica la ubicación del documento de Word.
   * Crear un `com.adobe.idp.Document` usando su constructor y pasando el objeto `java.io.FileInputStream` objeto.

1. Quitar la directiva del documento de Word

   * Crear un `DocumentManager` invocando el objeto de `RightsManagementClient` del objeto `getDocumentManager` método.
   * Quitar una directiva del documento de Word invocando la variable `DocumentManager` del objeto `removeSecurity` y pasando el `com.adobe.idp.Document` que contiene el documento de Word protegido por una directiva. Este método devuelve un `com.adobe.idp.Document` que contiene un documento de Word no protegido.

1. Guardar el documento de Word no protegido

   * Crear un `java.io.File` y asegúrese de que la extensión del archivo es DOC.
   * Invoque el `Document` del objeto `copyToFile` para copiar el contenido del `Document` al archivo (asegúrese de utilizar la variable `Document` objeto que ha devuelto el `removeSecurity` método).

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte el siguiente Inicio rápido:

* &quot;Inicio rápido (modo SOAP): Quitar una directiva de un documento de Word mediante la API de Java&quot;

### Quitar una directiva de un documento de Word mediante la API de servicio web {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Quitar una directiva de un documento de Word protegido por una directiva mediante la API de Document Security (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` con la dirección IP del servidor que aloja AEM Forms.

1. Crear un objeto de API de cliente de Document Security

   * Crear un `RightsManagementServiceClient` mediante su constructor predeterminado.
   * Crear un `RightsManagementServiceClient.Endpoint.Address` mediante el uso del objeto `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario que utilice el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Crear un `System.ServiceModel.BasicHttpBinding` al obtener el valor de la variable `RightsManagementServiceClient.Endpoint.Binding` field. Convierta el valor devuelto en `BasicHttpBinding`.
   * Configure las variables `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` field a `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * AEM Asigne el nombre de usuario del formulario de la al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asignar el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Asignar el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperar un documento de Word protegido por una directiva

   * Crear un `BLOB` mediante su constructor. El `BLOB` se utiliza para almacenar el documento de Word protegido por una directiva del que se quita la directiva.
   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento de Word y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo el `System.IO.FileStream` del objeto `Length` propiedad.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de la secuencia que se va a leer.
   * Rellene el `BLOB` al asignar su `MTOM` con el contenido de la matriz de bytes.

1. Quitar la directiva del documento de Word

   Quite la directiva del documento de Word invocando el `RightsManagementServiceClient` del objeto `removePolicySecurity` y pasando el `BLOB` que contiene el documento de Word protegido por una directiva. Este método devuelve un `BLOB` que contiene un documento de Word no protegido.

1. Guardar el documento de Word no protegido

   * Crear un `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que representa la ubicación de archivo del documento de Word no protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto que ha devuelto el `removePolicySecurity` método. Rellene la matriz de bytes obteniendo el valor de `BLOB` del objeto `MTOM` field.
   * Crear un `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream` objeto.

**Ejemplos de código**

Para ver ejemplos de código utilizando el servicio Document Security, consulte el siguiente Inicio rápido:

* &quot;Inicio rápido (MTOM): Quitar una directiva de un documento de Word mediante la API de servicio web&quot;

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
