---
title: Protección de documentos con directivas
seo-title: Protección de documentos con directivas
description: Utilice el servicio de seguridad de documentos para aplicar de forma dinámica la configuración de confidencialidad a los documentos de Adobe PDF y para mantener el control sobre los documentos. El servicio Document Security también permite a los usuarios mantener el control sobre cómo los destinatarios utilizan el documento PDF protegido por políticas.
seo-description: Utilice el servicio de seguridad de documentos para aplicar de forma dinámica la configuración de confidencialidad a los documentos de Adobe PDF y para mantener el control sobre los documentos. El servicio Document Security también permite a los usuarios mantener el control sobre cómo los destinatarios utilizan el documento PDF protegido por políticas.
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
role: Desarrollador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '15559'
ht-degree: 0%

---


# Protección de documentos con directivas {#protecting-documents-with-policies}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

**Acerca del servicio de seguridad de documentos**

El servicio de seguridad de documentos permite a los usuarios aplicar de forma dinámica la configuración de confidencialidad a los documentos de Adobe PDF y mantener el control sobre los documentos, independientemente de su amplia distribución.

El servicio de seguridad de documentos evita que la información se extienda más allá del alcance del usuario, ya que permite a los usuarios mantener el control sobre cómo los destinatarios utilizan el documento PDF protegido por políticas. Un usuario puede especificar quién puede abrir un documento, limitar cómo puede utilizarlo y supervisar el documento después de distribuirlo. Un usuario también puede controlar dinámicamente el acceso a un documento protegido por políticas e incluso puede revocar dinámicamente el acceso al documento.

El servicio de seguridad de documentos también protege otros tipos de archivos, como archivos de Microsoft Word (archivos DOC). Puede utilizar la API de cliente de Document Security para trabajar con estos tipos de archivo. Se admiten las siguientes versiones:

* Archivos de Microsoft Office 2003 (DOC, XLS, PPT)
* Archivos de Microsoft Office 2007 (archivos DOCX, XLSX, PPTX)
* Archivos PTC Pro/E

Para una mayor claridad, las dos secciones siguientes tratan sobre cómo trabajar con documentos de Word:

* [Aplicación de directivas a documentos de Word](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Eliminación de directivas de documentos de Word](protecting-documents-policies.md#removing-policies-from-word-documents)

Puede realizar estas tareas mediante el servicio Document Security:

* Crear directivas. Para obtener más información, consulte [Creación de directivas](protecting-documents-policies.md#creating-policies).
* Modificar directivas. Para obtener más información, consulte [Modificación de directivas](protecting-documents-policies.md#modifying-policies).
* Eliminar directivas. Para obtener más información, consulte [Eliminación de directivas](protecting-documents-policies.md#deleting-policies).
* Aplicar directivas a documentos PDF. Para obtener más información, consulte [Aplicación de directivas a documentos PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents).
* Elimine directivas de documentos PDF. Para obtener más información, consulte [Eliminación de directivas de documentos PDF](protecting-documents-policies.md#removing-policies-from-pdf-documents).
* Documentos protegidos por políticas de Inspect. Para obtener más información, consulte [Inspección de documentos PDF protegidos por políticas](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents).
* Revocar el acceso a los documentos PDF. Para obtener más información, consulte [Revocar acceso a documentos](protecting-documents-policies.md#revoking-access-to-documents).
* Restablezca el acceso a los documentos revocados. Para obtener más información, consulte [Restablecimiento del acceso a documentos revocados](protecting-documents-policies.md#reinstating-access-to-revoked-documents).
* Crear marcas de agua. Para obtener más información, consulte [Creación de marcas de agua](protecting-documents-policies.md#creating-watermarks).
* Busque eventos. Para obtener más información, consulte [Búsqueda de eventos](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>Para obtener más información sobre el servicio de seguridad de documentos, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Creación de directivas {#creating-policies}

Puede crear directivas mediante programación mediante la API Java de Document Security o la API de servicio web. Una *directiva* es una colección de información que incluye la configuración de seguridad del documento, los usuarios autorizados y los derechos de uso. Puede crear y guardar cualquier número de directivas, utilizando la configuración de seguridad adecuada para diferentes situaciones y usuarios.

Las directivas permiten realizar estas tareas:

* Especifique las personas que pueden abrir el documento. Los destinatarios pueden pertenecer a su organización o ser externos a ella.
* Especifique cómo pueden utilizar el documento los destinatarios. Puede restringir el acceso a diferentes funciones de Acrobat y Adobe Reader. Estas funciones incluyen la capacidad de imprimir y copiar texto, agregar firmas y agregar comentarios a un documento.
* Cambie la configuración de acceso y seguridad en cualquier momento, incluso después de distribuir el documento protegido por políticas.
* Monitorice el uso del documento después de distribuirlo. Puede ver cómo se está utilizando el documento y quién lo está utilizando. Por ejemplo, puede averiguar cuándo alguien ha abierto el documento.

### Creación de una directiva mediante servicios Web {#creating-a-policy-using-web-services}

Al crear una directiva mediante la API de servicio web, haga referencia a un archivo XML existente del lenguaje de derechos de documento portátiles (PDRL) que describa la directiva. Los permisos de directiva y el principal se definen en el documento PDRL. El siguiente documento XML es un ejemplo de documento PDRL.

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
>Para obtener más información sobre el servicio de seguridad de documentos, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para crear una directiva, realice los pasos siguientes:

1. Incluir archivos de proyecto.
1. Cree un objeto de API cliente de Document Security.
1. Establezca los atributos de la política.
1. Cree una entrada de directiva.
1. Registre la directiva.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-rightsmanagement-client.jar
* namespace.jar (si AEM Forms está implementado en JBoss)
* jaxb-api.jar (si AEM Forms está implementado en JBoss)
* jaxb-impl.jar (si AEM Forms está implementado en JBoss)
* jaxb-libs.jar (si AEM Forms está implementado en JBoss)
* jaxb-xjc.jar (si AEM Forms está implementado en JBoss)
* relajngDataType.jar (si AEM Forms está implementado en JBoss)
* xsdlib.jar (si AEM Forms está implementado en JBoss)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar (utilice un archivo JAR diferente si AEM Forms no está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un objeto de API cliente de Document Security**

Antes de poder realizar una operación de servicio Document Security mediante programación, cree un objeto cliente de servicio Document Security.

**Establezca los atributos de la política**

Para crear una directiva, establezca los atributos de la directiva. Un atributo obligatorio es el nombre de la política. Los nombres de directiva deben ser únicos para cada conjunto de directivas. Un conjunto de políticas es simplemente una colección de políticas. Puede haber dos directivas con el mismo nombre si las directivas pertenecen a conjuntos de directivas independientes. Sin embargo, dos directivas dentro de un único conjunto de directivas no pueden tener el mismo nombre de directiva.

Otro atributo útil que se debe establecer es el periodo de validez. Un periodo de validez es el periodo durante el cual los destinatarios autorizados pueden acceder a un documento protegido por políticas. Si no establece este atributo, la política siempre es válida.

Se puede establecer un periodo de validez en una de estas opciones:

* Un número determinado de días en los que se puede acceder al documento desde el momento en que se publica
* Una fecha final después de la cual no se puede acceder al documento
* Un intervalo de fechas específico para el que se puede acceder al documento
* Siempre válido

Solo puede especificar una fecha de inicio, lo que hace que la directiva sea válida después de la fecha de inicio. Si solo especifica una fecha de finalización, la política es válida hasta la fecha de finalización. Sin embargo, se genera una excepción si no se definen una fecha de inicio ni una de finalización.

Al establecer atributos que pertenecen a una directiva, también puede definir la configuración de codificación. Esta configuración de codificación se aplica cuando la directiva se aplica a un documento. Puede especificar los siguientes valores de codificación:

* **AES256**: Representa el algoritmo de cifrado AES con una clave de 256 bits.
* **AES128**: Representa el algoritmo de cifrado AES con una clave de 128 bits.
* **SinCifrado:** no representa ningún cifrado.

Al especificar la opción `NoEncryption`, no se puede establecer la opción `PlaintextMetadata` en `false`. Si intenta hacerlo, se genera una excepción.

>[!NOTE]
>
>Para obtener información sobre otros atributos que puede establecer, consulte la descripción de la interfaz `Policy` en la [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Crear una entrada de directiva**

Una entrada de directiva adjunta entidades principales, que son grupos y usuarios, y permisos para una directiva. Una directiva debe tener al menos una entrada de directiva. Supongamos, por ejemplo, que realiza estas tareas:

* Cree y registre una entrada de directiva que permita a un grupo ver únicamente un documento mientras esté en línea y prohíba que los destinatarios lo copien.
* Adjunte la entrada de directiva a la directiva.
* Proteja un documento con la directiva utilizando Acrobat.

Estas acciones hacen que los destinatarios solo puedan ver el documento en línea y no puedan copiarlo. El documento permanece seguro hasta que se elimina la seguridad de él.

**Registrar la directiva**

Se debe registrar una nueva directiva para poder utilizarla. Después de registrar una directiva, puede utilizarla para proteger documentos.

### Crear una directiva mediante la API de Java {#create-a-policy-using-the-java-api}

Cree una directiva utilizando la API de seguridad de documentos (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `DocumentSecurityClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Establezca los atributos de la política.

   * Cree un objeto `Policy` invocando el método estático `InfomodelObjectFactory` del objeto `createPolicy`. Este método devuelve un objeto `Policy`.
   * Establezca el atributo de nombre de la directiva invocando el método `Policy` del objeto `setName` y pasando un valor de cadena que especifica el nombre de la directiva.
   * Establezca la descripción de la directiva invocando el método `Policy` del objeto `setDescription` y pasando un valor de cadena que especifica la descripción de la directiva.
   * Establezca el conjunto de directivas al que pertenece la nueva directiva invocando el método `Policy` del objeto `setPolicySetName` y pasando un valor de cadena que especifica el nombre del conjunto de directivas. (Puede especificar `null` para este valor de parámetro que resulta en que la directiva se agregue al conjunto de directivas *Mis directivas*).
   * Cree el periodo de validez de la directiva invocando el método estático `InfomodelObjectFactory` del objeto `createValidityPeriod`. Este método devuelve un objeto `ValidityPeriod`.
   * Establezca el número de días durante los cuales se puede acceder a un documento protegido por políticas invocando el método `ValidityPeriod` del objeto `setRelativeExpirationDays` y pasando un valor entero que especifica el número de días.
   * Establezca el periodo de validez de la directiva invocando el método `Policy` del objeto `setValidityPeriod` y pasando el objeto `ValidityPeriod`.

1. Cree una entrada de directiva.

   * Cree una entrada de política invocando el método estático `InfomodelObjectFactory` del objeto `createPolicyEntry`. Este método devuelve un objeto `PolicyEntry`.
   * Especifique los permisos de la directiva invocando el método estático `InfomodelObjectFactory` del objeto `createPermission`. Pase un miembro de datos estático que pertenezca a la interfaz `Permission` que represente el permiso. Este método devuelve un objeto `Permission`. Por ejemplo, para agregar el permiso que permite a los usuarios copiar datos de un documento PDF protegido por políticas, pase `Permission.COPY`. (Repita este paso para cada permiso que desee añadir).
   * Agregue el permiso a la entrada de directiva invocando el método `PolicyEntry` del objeto `addPermission` y pasando el objeto `Permission`. (Repita este paso para cada objeto `Permission` que haya creado).
   * Cree la entidad de seguridad de directiva invocando el método estático `InfomodelObjectFactory` del objeto `createSpecialPrincipal`. Pase un miembro de datos que pertenezca al objeto `InfomodelObjectFactory` que represente la entidad de seguridad. Este método devuelve un objeto `Principal`. Por ejemplo, para agregar el editor del documento como principal, pase `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * Agregue la entidad de seguridad a la entrada de directiva invocando el método `PolicyEntry` del objeto `setPrincipal`y pasando el objeto `Principal`.
   * Agregue la entrada de directiva a la directiva invocando el método `Policy` del objeto `addPolicyEntry` y pasando el objeto `PolicyEntry`.

1. Registre la directiva.

   * Cree un objeto `PolicyManager` invocando el método `DocumentSecurityClient` del objeto `getPolicyManager`.
   * Registre la directiva invocando el método `PolicyManager` del objeto `registerPolicy` y pasando los siguientes valores:

      * El objeto `Policy` que representa la directiva que se va a registrar.
   * Un valor de cadena que representa el conjunto de directivas al que pertenece la directiva.

   Si utiliza una cuenta de administrador de formularios AEM en la configuración de conexión para crear el objeto `DocumentSecurityClient`, especifique el nombre del conjunto de directivas cuando invoque el método `registerPolicy`. Si pasa un valor `null` para el conjunto de directivas, la directiva se crea en el conjunto de directivas *Mis directivas* de los administradores.

   Si utiliza un usuario de Document Security dentro de la configuración de conexión, puede invocar el método de sobrecarga `registerPolicy` que acepta únicamente la directiva. Es decir, no es necesario especificar el nombre del conjunto de directivas. Sin embargo, la directiva se agrega al conjunto de directivas denominado *Mis directivas*. Si no desea agregar la nueva directiva a este conjunto de directivas, especifique un nombre de conjunto de directivas cuando invoque el método `registerPolicy`.

   >[!NOTE]
   >
   >Al crear una directiva, haga referencia a un conjunto de directivas existente. Si especifica un conjunto de directivas que no existe, se genera una excepción.

Para ver ejemplos de código que utilicen el servicio Document Security, consulte lo siguiente:

* &quot;Inicio rápido (modo SOAP): Creación de una directiva mediante la API de Java&quot;

### Crear una directiva mediante la API de servicio web {#create-a-policy-using-the-web-service-api}

Cree una directiva utilizando la API de seguridad de documentos (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `DocumentSecurityServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `DocumentSecurityServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `RightsManagementServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Establezca los atributos de la política.

   * Cree un objeto `PolicySpec` utilizando su constructor.
   * Establezca el nombre de la directiva asignando un valor de cadena al miembro de datos `PolicySpec` del objeto `name`.
   * Defina la descripción de la directiva asignando un valor de cadena al miembro de datos `PolicySpec` del objeto `description`.
   * Establezca el conjunto de directivas al que pertenecerá la directiva asignando un valor de cadena al miembro de datos `PolicySpec` del objeto `policySetName`. Debe especificar un nombre de conjunto de directivas existente. (Puede especificar `null` para este valor de parámetro que resulta en que la directiva se agregue a *Mis directivas*).
   * Establezca el periodo de concesión sin conexión de la directiva asignando un valor entero al miembro de datos `PolicySpec` del objeto `offlineLeasePeriod`.
   * Establezca el miembro de datos `PolicySpec` del objeto `policyXml` con un valor de cadena que represente los datos XML de PDRL. Para realizar esta tarea, cree un objeto .NET `StreamReader` utilizando su constructor. Pase la ubicación de un archivo XML PDRL que represente la directiva al constructor `StreamReader`. A continuación, invoque el método `StreamReader` del objeto `ReadLine` y asigne el valor devuelto a una variable de cadena. Se repite mediante el objeto `StreamReader` hasta que el método `ReadLine` devuelve nulo. Asigne la variable de cadena al miembro de datos `PolicySpec` del objeto `policyXml`.

1. Cree una entrada de directiva.

   No es necesario crear una entrada de directiva al crear una directiva mediante la API del servicio web Document Security. La entrada de directiva se define en el documento PDRL.

1. Registre la directiva.

   Registre la directiva invocando el método `DocumentSecurityServiceClient` del objeto `registerPolicy` y pasando los siguientes valores:

   * El objeto `PolicySpec` que representa la directiva que se va a registrar.
   * Un valor de cadena que representa el conjunto de directivas al que pertenece la directiva. Puede especificar un valor `null` que tenga como resultado que la directiva se agregue al conjunto de directivas *MyPolices*.

   Si utiliza una cuenta de administrador de formularios AEM en la configuración de conexión para crear el objeto `DocumentSecurityClient`, especifique el nombre del conjunto de directivas cuando invoque el método `registerPolicy`.

   Si utiliza un usuario de Document SecurityDocument Security dentro de la configuración de la conexión, puede invocar el método sobrecargado `registerPolicy` que sólo acepta la directiva. Es decir, no es necesario especificar el nombre del conjunto de directivas. Sin embargo, la directiva se agrega al conjunto de directivas denominado *Mis directivas*. Si no desea agregar la nueva directiva a este conjunto de directivas, especifique un nombre de conjunto de directivas cuando invoque el método `registerPolicy`.

   >[!NOTE]
   >
   >Al crear una directiva y especificar un conjunto de directivas, asegúrese de especificar un conjunto de directivas existente. Si especifica un conjunto de directivas que no existe, se genera una excepción.

Para ver ejemplos de código que utilicen el servicio de seguridad de documentos, consulte Inicio rápido siguiente:

* &quot;Inicio rápido (MTOM): Creación de una directiva mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Creación de una directiva mediante la API de servicio web&quot;

## Modificación de directivas {#modifying-policies}

Puede modificar una directiva existente mediante la API de Java o la API de servicio web de Document Security. Para realizar cambios en una directiva existente, debe recuperarla, modificarla y, a continuación, actualizar la directiva en el servidor. Por ejemplo, supongamos que recupera una directiva existente y amplía su periodo de validez. Antes de que el cambio surta efecto, debe actualizar la directiva.

Puede modificar una directiva cuando cambien los requisitos comerciales y esta ya no refleje estos requisitos. En lugar de crear una directiva nueva, simplemente puede actualizar una existente.

Para modificar los atributos de directiva mediante un servicio web (por ejemplo, mediante el uso de clases proxy de Java creadas con JAX-WS), debe asegurarse de que la directiva esté registrada en el servicio Document Security. A continuación, puede hacer referencia a la política existente utilizando el método `PolicySpec.getPolicyXml` y modificar los atributos de política utilizando los métodos aplicables. Por ejemplo, puede modificar el periodo de arrendamiento sin conexión invocando el método `PolicySpec.setOfflineLeasePeriod`.

>[!NOTE]
>
>Para obtener más información sobre el servicio de seguridad de documentos, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para modificar una directiva existente, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API cliente de Document Security.
1. Recupere una directiva existente.
1. Cambiar atributos de directivas.
1. Actualice la directiva.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API cliente de Document Security**

Antes de poder realizar mediante programación una operación del servicio Document Security, debe crear un objeto cliente del servicio Document Security. Si utiliza la API de Java, cree un objeto `RightsManagementClient`. Si utiliza la API del servicio web de Document Security, cree un objeto `RightsManagementServiceService`.

**Recuperar una directiva existente**

Debe recuperar una directiva existente para modificarla. Para recuperar una directiva, especifique el nombre de la directiva y el conjunto de directivas al que pertenece la directiva. Si especifica un valor `null` para el nombre del conjunto de directivas, la directiva se recupera del conjunto de directivas *Mis directivas*.

**Establezca los atributos de la política**

Para modificar una directiva, modifique el valor de los atributos de directiva. El único atributo de política que no puede cambiar es el atributo de nombre. Por ejemplo, para cambiar el periodo de arrendamiento sin conexión de la política, puede modificar el valor del atributo de periodo de arrendamiento sin conexión de la política.

Al modificar el periodo de concesión sin conexión de una directiva mediante un servicio web, se ignora el campo `offlineLeasePeriod` de la interfaz `PolicySpec`. Para actualizar el periodo de arrendamiento sin conexión, modifique el elemento `OfflineLeasePeriod` en el documento XML de PDRL. A continuación, haga referencia al documento XML de PDRL actualizado utilizando el miembro de datos `PolicySpec` de la interfaz `policyXML`.

>[!NOTE]
>
>Para obtener información sobre otros atributos que puede establecer, consulte la descripción de la interfaz `Policy` en la [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Actualizar la directiva**

Antes de que se apliquen los cambios realizados en una directiva, debe actualizarla con el servicio de seguridad de documentos. Los cambios en las políticas que protegen documentos se actualizan la próxima vez que el documento protegido por políticas se sincroniza con el servicio de seguridad de documentos.

### Modifique las directivas existentes mediante la API de Java {#modify-existing-policies-using-the-java-api}

Modifique una directiva existente utilizando la API de seguridad de documentos (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `RightsManagementClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recupere una directiva existente.

   * Cree un objeto `PolicyManager` invocando el método `RightsManagementClient` del objeto `getPolicyManager`.
   * Cree un objeto `Policy` que represente la directiva que desea actualizar invocando el método `PolicyManager` del objeto `getPolicy` y pasando los siguientes valores&quot;

      * Un valor de cadena que representa el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar `null` que resultará en el uso del conjunto de directivas `MyPolicies`.
      * Un valor de cadena que representa el nombre de la directiva.

1. Establezca los atributos de la política.

   Cambie los atributos de la directiva para satisfacer los requisitos comerciales. Por ejemplo, para cambiar el periodo de concesión sin conexión de la directiva, invoque el método `Policy` del objeto `setOfflineLeasePeriod`.

1. Actualice la directiva.

   Actualice la directiva invocando el método `PolicyManager` del objeto `updatePolicy`. Pase el objeto `Policy` que representa la directiva que desea actualizar.

**Ejemplos de código**

Para obtener ejemplos de código mediante el servicio Document Security, consulte Inicio rápido (modo SOAP): Modificación de una directiva mediante la sección API de Java.

### Modifique las directivas existentes mediante la API de servicio web {#modify-existing-policies-using-the-web-service-api}

Modifique una directiva existente utilizando la API de seguridad de documentos (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `RightsManagementServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `RightsManagementServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `RightsManagementServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere una directiva existente.

   Cree un objeto `PolicySpec` que represente la directiva que desea modificar invocando el método `getPolicy` del objeto `RightsManagementServiceClient` y pasando los siguientes valores:

   * Un valor de cadena que especifica el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar `null` que resultará en el uso del conjunto de directivas `MyPolicies`.
   * Un valor de cadena que especifica el nombre de la directiva.

1. Establezca los atributos de la política.

   Cambie los atributos de la directiva para satisfacer los requisitos comerciales.

1. Actualice la directiva.

   Actualice la directiva invocando el método `RightsManagementServiceClient` del objeto `updatePolicyFromSDK` y pasando el objeto `PolicySpec` que representa la directiva que se va a actualizar.

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio de seguridad de documentos, consulte Inicio rápido siguiente:

* &quot;Inicio rápido (MTOM): Modificación de una directiva mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Modificación de una directiva mediante la API de servicio web&quot;

## Eliminación de directivas {#deleting-policies}

Puede eliminar una directiva existente mediante la API de Java o la API de servicio web de Document Security. Una vez eliminada una directiva, ya no se puede utilizar para proteger documentos. Sin embargo, los documentos protegidos por políticas existentes que utilizan la política siguen estando protegidos. Puede eliminar una directiva cuando una más reciente esté disponible.

>[!NOTE]
>
>Para obtener más información sobre el servicio de seguridad de documentos, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para eliminar una directiva existente, realice los siguientes pasos:

1. Incluir archivos de proyecto
1. Cree un objeto de API cliente de Document Security.
1. Elimine la directiva.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API cliente de Document Security**

Para poder realizar una operación de servicio Document Security mediante programación, debe crear un objeto cliente de servicio Document Security. Si utiliza la API de Java, cree un objeto `RightsManagementClient`. Si utiliza la API del servicio web de Document Security, cree un objeto `RightsManagementServiceService`.

**Eliminar la directiva**

Para eliminar una directiva, especifique la directiva que desea eliminar y el conjunto de directivas al que pertenece la directiva. El usuario cuya configuración se utilice para invocar a AEM Forms debe tener permiso para eliminar la directiva; de lo contrario, se produce una excepción. Del mismo modo, si intenta eliminar una directiva que no existe, se producirá una excepción.

### Eliminar directivas utilizando la API de Java {#delete-policies-using-the-java-api}

Elimine una directiva utilizando la API de seguridad de documentos (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `RightsManagementClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Elimine la directiva.

   * Cree un objeto `PolicyManager` invocando el método `RightsManagementClient` del objeto `getPolicyManager`.
   * Para eliminar la directiva, invoque el método `PolicyManager` del objeto `deletePolicy` y pase los siguientes valores:

      * Un valor de cadena que especifica el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar `null` que resultará en el uso del conjunto de directivas `MyPolicies`.
      * Un valor de cadena que especifica el nombre de la directiva que se va a eliminar.

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio de seguridad de documentos, consulte Inicio rápido siguiente:

* &quot;Inicio rápido (modo SOAP): Eliminación de una directiva mediante la API de Java&quot;

### Eliminar directivas utilizando la API de servicio web {#delete-policies-using-the-web-service-api}

Elimine una directiva utilizando la API de seguridad de documentos (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `RightsManagementServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `RightsManagementServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `RightsManagementServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Elimine la directiva.

   Para eliminar una directiva, invoque el método `RightsManagementServiceClient` del objeto `deletePolicy` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar `null` que resultará en el uso del conjunto de directivas `MyPolicies`.
   * Un valor de cadena que especifica el nombre de la directiva que se va a eliminar.

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio de seguridad de documentos, consulte Inicio rápido siguiente:

* &quot;Inicio rápido (MTOM): Eliminación de una directiva mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Eliminación de una directiva mediante la API de servicio web&quot;

## Aplicación de directivas a documentos PDF {#applying-policies-to-pdf-documents}

Puede aplicar una directiva a un documento PDF para protegerlo. Al aplicar una directiva a un documento PDF, se restringe el acceso al documento. No puede aplicar una directiva a un documento si el documento ya está protegido con una directiva.

Mientras el documento está abierto, también puede restringir el acceso a las funciones de Acrobat y Adobe Reader, incluida la capacidad de imprimir y copiar texto, realizar cambios y agregar firmas y comentarios a un documento. Además, puede revocar un documento PDF protegido por políticas cuando ya no desee que los usuarios accedan al documento.

Después de distribuirlo, puede supervisar el uso de un documento protegido por políticas. Es decir, puede ver cómo se utiliza el documento y quién lo utiliza. Por ejemplo, puede averiguar cuándo alguien ha abierto el documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio de seguridad de documentos, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-3}

Para aplicar una directiva a un documento PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API cliente de Document Security.
1. Recupere un documento PDF al que se aplica una política.
1. Aplicar una política existente al documento PDF.
1. Guarde el documento PDF protegido por políticas.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto API cliente de Document Security**

Antes de poder realizar una operación de servicio Document Security mediante programación, cree un objeto cliente de servicio Document Security. Si utiliza la API de Java, cree un objeto `DocumentSecurityClient`. Si utiliza la API del servicio web de Document Security, cree un objeto `DocumentSecurityServiceService`.

**Recuperar un documento PDF**

Puede recuperar un documento PDF para aplicar una directiva. Después de aplicar una directiva al documento PDF, los usuarios se ven restringidos al usar el documento. Por ejemplo, si la directiva no permite abrir el documento sin conexión, los usuarios deben estar en línea para abrirlo.

**Aplicar una política existente al documento PDF**

Para aplicar una directiva a un documento PDF, haga referencia a una directiva existente y especifique a qué conjunto de directivas pertenece la directiva. El usuario que esté configurando las propiedades de conexión debe tener acceso a la directiva especificada. Si no es así, se produce una excepción.

**Guardar el documento PDF**

Después de que el servicio de seguridad de documentos aplique una directiva a un documento PDF, puede guardar el documento PDF protegido por políticas como un archivo PDF.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revocación del acceso a los documentos](protecting-documents-policies.md#revoking-access-to-documents)

### Aplicar una directiva a un documento PDF utilizando la API de Java {#apply-a-policy-to-a-pdf-document-using-the-java-api}

Aplique una directiva a un documento PDF utilizando la API de seguridad de documentos (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `RightsManagementClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recupere un documento PDF.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF utilizando su constructor. Pase un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Aplicar una política existente al documento PDF.

   * Cree un objeto `DocumentManager` invocando el método `RightsManagementClient` del objeto `getDocumentManager`.
   * Aplique una política al documento PDF invocando el método `DocumentManager` del objeto `protectDocument` y pasando los siguientes valores:

      * El objeto `com.adobe.idp.Document` que contiene el documento PDF al que se aplica la política.
      * Un valor de cadena que especifica el nombre del documento.
      * Un valor de cadena que especifica el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar un valor `null` que resulte en el uso del conjunto de directivas `MyPolicies`.
      * Un valor de cadena que especifica el nombre de la directiva.
      * Un valor de cadena que representa el nombre del dominio de administrador de usuarios del usuario que es el editor del documento. Este valor del parámetro es opcional y puede ser nulo (si este parámetro es nulo, el siguiente valor del parámetro debe ser nulo).
      * Un valor de cadena que representa el nombre canónico del usuario administrador de usuarios que es el editor del documento. Este valor de parámetro es opcional y puede ser `null` (si este parámetro es nulo, el valor del parámetro anterior debe ser `null`).
      * `com.adobe.livecycle.rightsmanagement.Locale` que representa la configuración regional que se utiliza para seleccionar la plantilla de MS Office. Este valor de parámetro es opcional y no se utiliza para documentos PDF. Para proteger un documento PDF, especifique `null`.

      El método `protectDocument` devuelve un objeto `RMSecureDocumentResult` que contiene el documento PDF protegido por políticas.


1. Guarde el documento PDF.

   * Invoque el método `RMSecureDocumentResult` del objeto `getProtectedDoc` para obtener el documento PDF protegido por políticas. Este método devuelve un objeto `com.adobe.idp.Document`.
   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea PDF.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del objeto `Document` en el archivo (asegúrese de utilizar el objeto `Document` que devolvió el método `getProtectedDoc`).

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio de seguridad de documentos, consulte Inicio rápido siguiente:

* &quot;Inicio rápido (modo EJB): Aplicación de una directiva a un documento PDF mediante la API de Java&quot;
* &quot;Inicio rápido (modo SOAP): Aplicación de una directiva a un documento PDF mediante la API de Java&quot;

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aplicar una directiva a un documento PDF utilizando la API de servicio Web {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

Aplique una política a un documento PDF utilizando la API de seguridad de documentos (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `RightsManagementServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `RightsManagementServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `RightsManagementServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere un documento PDF.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF al que se aplica una política.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Determine el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Aplicar una política existente al documento PDF.

   Aplique una política al documento PDF invocando el método `RightsManagementServiceClient` del objeto `protectDocument` y pasando los siguientes valores:

   * El objeto `BLOB` que contiene el documento PDF al que se aplica la política.
   * Un valor de cadena que especifica el nombre del documento.
   * Un valor de cadena que especifica el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar un valor `null` que resulte en el uso del conjunto de directivas `MyPolicies`.
   * Un valor de cadena que especifica el nombre de la directiva.
   * Un valor de cadena que representa el nombre del dominio de administrador de usuarios del usuario que es el editor del documento. Este valor de parámetro es opcional y puede ser nulo (si este parámetro es nulo, el siguiente valor de parámetro debe ser `null`).
   * Un valor de cadena que representa el nombre canónico del usuario administrador de usuarios que es el editor del documento. Este valor de parámetro es opcional y puede ser nulo (si este parámetro es nulo, el valor del parámetro anterior debe ser `null`).
   * Un valor `RMLocale` que especifica el valor de configuración regional (por ejemplo, `RMLocale.en`).
   * Un parámetro de salida de cadena que se utiliza para almacenar el valor del identificador de la política.
   * Un parámetro de salida de cadena que se utiliza para almacenar el valor del identificador protegido por políticas.
   * Un parámetro de salida de cadena que se utiliza para almacenar el tipo mime (por ejemplo, `application/pdf`).

   El método `protectDocument` devuelve un objeto `BLOB` que contiene el documento PDF protegido por políticas.

1. Guarde el documento PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF protegido por políticas.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` que el método `protectDocument` devolvió. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio de seguridad de documentos, consulte Inicio rápido siguiente:

* &quot;Inicio rápido (MTOM): Aplicación de una directiva a un documento PDF mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Aplicación de una directiva a un documento PDF mediante la API de servicio web&quot;

## Eliminación de directivas de documentos PDF {#removing-policies-from-pdf-documents}

Puede quitar una directiva de un documento protegido por una directiva para eliminar la seguridad del documento. Es decir, si ya no desea que el documento esté protegido por una directiva. Si desea actualizar un documento protegido por políticas con una directiva más reciente, en lugar de eliminar la directiva y agregar la directiva actualizada, es más eficiente cambiar la directiva.

>[!NOTE]
>
>Para obtener más información sobre el servicio de seguridad de documentos, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-4}

Para quitar una directiva de un documento PDF protegido por políticas, realice los siguientes pasos:

1. Incluir archivos de proyecto
1. Cree un objeto de API cliente de Document Security.
1. Recupere un documento PDF protegido por políticas.
1. Elimine la directiva del documento PDF.
1. Guarde el documento PDF no protegido.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API cliente de Document Security**

Antes de poder realizar una operación de servicio Document Security mediante programación, cree un objeto cliente de servicio Document Security.

**Recuperar un documento PDF protegido por políticas**

Puede recuperar un documento PDF protegido por políticas para eliminar una directiva. Si intenta quitar una directiva de un documento PDF que no esté protegido por una directiva, provocará una excepción.

**Quitar la directiva del documento PDF**

Puede quitar una directiva de un documento PDF protegido por políticas siempre que se especifique un administrador en la configuración de conexión. Si no es así, la política utilizada para proteger un documento debe contener el permiso `SWITCH_POLICY` para eliminar una política de un documento PDF. Además, el usuario especificado en la configuración de conexión de AEM Forms también debe tener ese permiso. De lo contrario, se genera una excepción.

**Guardar el documento PDF no protegido**

Una vez que el servicio de seguridad de documentos elimina una directiva de un documento PDF, puede guardar el documento PDF no protegido como un archivo PDF.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicación de directivas a documentos PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Eliminar una directiva de un documento PDF utilizando la API de Java {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Elimine una directiva de un documento PDF protegido por políticas utilizando la API de seguridad de documentos (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `DocumentSecurityClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recupere un documento PDF protegido por políticas.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF protegido por políticas utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Elimine la directiva del documento PDF.

   * Cree un objeto `DocumentManager` invocando el método `DocumentSecurityClient` del objeto `getDocumentManager`.
   * Elimine una política del documento PDF invocando el método `DocumentManager` del objeto `removeSecurity` y pasando el objeto `com.adobe.idp.Document` que contiene el documento PDF protegido por políticas. Este método devuelve un objeto `com.adobe.idp.Document` que contiene un documento PDF no protegido.

1. Guarde el documento PDF no protegido.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea PDF.
   * Invoque el método `Document` del objeto `copyToFile` para copiar el contenido del objeto `Document` en el archivo (asegúrese de utilizar el objeto `Document` que devolvió el método `removeSecurity`).

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio de seguridad de documentos, consulte Inicio rápido siguiente:

* &quot;Inicio rápido (modo SOAP): Eliminación de una directiva de un documento PDF mediante la API de Java&quot;

### Eliminar una directiva mediante la API de servicio web {#remove-a-policy-using-the-web-service-api}

Elimine una directiva de un documento PDF protegido por políticas mediante la API de seguridad de documentos (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `DocumentSecurityServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `DocumentSecurityServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `DocumentSecurityServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere un documento PDF protegido por políticas.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento PDF protegido por políticas del que se ha eliminado la directiva.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Elimine la directiva del documento PDF.

   Elimine la directiva del documento PDF invocando el método `DocumentSecurityServiceClient` del objeto `removePolicySecurity` y pasando el objeto `BLOB` que contiene el documento PDF protegido por políticas. Este método devuelve un objeto `BLOB` que contiene un documento PDF no protegido.

1. Guarde el documento PDF no protegido.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF no protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` que el método `removePolicySecurity` devolvió. Rellene la matriz de bytes obteniendo el valor del campo `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio de seguridad de documentos, consulte Inicio rápido siguiente:

* &quot;Inicio rápido (MTOM): Eliminación de una directiva de un documento PDF mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Eliminación de una directiva de un documento PDF mediante la API de servicio web&quot;

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Revocación del acceso a los documentos {#revoking-access-to-documents}

Puede revocar el acceso a un documento PDF protegido por políticas, lo que hace que todos los textos del documento no sean accesibles para los usuarios. Cuando un usuario intenta abrir un documento PDF revocado, se le redirige a una dirección URL específica donde se puede ver un documento revisado. La dirección URL a la que se redirige al usuario debe especificarse mediante programación. Cuando se revoca el acceso a un documento, el cambio entra en vigor la próxima vez que el usuario se sincroniza con el servicio de seguridad de documentos abriendo en línea el documento protegido por políticas.

La posibilidad de revocar el acceso a un documento proporciona seguridad adicional. Por ejemplo, supongamos que una versión más reciente de un documento está disponible y que ya no desea que nadie vea la versión obsoleta. En esta situación, el acceso al documento más antiguo se puede revocar y nadie puede ver el documento a menos que se restablezca el acceso.

>[!NOTE]
>
>Para obtener más información sobre el servicio de seguridad de documentos, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-5}

Para revocar un documento protegido por políticas, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API cliente de Document Security.
1. Recupere un documento PDF protegido por políticas.
1. Revocar el documento protegido por políticas.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API cliente de Document Security**

Para poder realizar una operación de servicio Document Security mediante programación, debe crear un objeto cliente de servicio Document Security.

**Recuperar un documento PDF protegido por políticas**

Debe recuperar un documento PDF protegido por políticas para revocarlo. No puede revocar un documento que ya se haya revocado o que no sea un documento protegido por políticas.

Si conoce el valor del identificador de licencia del documento protegido por políticas, no es necesario recuperar el documento PDF protegido por políticas. Sin embargo, en la mayoría de los casos, deberá recuperar el documento PDF para obtener el valor del identificador de licencia.

**Revocar el documento protegido por políticas**

Para revocar un documento protegido por políticas, especifique el identificador de licencia del documento protegido por políticas. Además, puede especificar la dirección URL de un documento que el usuario puede ver cuando intenta abrir el documento revocado. Es decir, supongamos que se revoca un documento obsoleto. Cuando un usuario intenta abrir el documento revocado, verá un documento actualizado en lugar del documento revocado.

>[!NOTE]
>
>Si intenta revocar un documento que ya se ha revocado, se produce una excepción.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicación de directivas a documentos PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Restablecimiento del acceso a documentos revocados](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Revocar el acceso a los documentos mediante la API de Java {#revoke-access-to-documents-using-the-java-api}

Revocar el acceso a un documento PDF protegido por políticas utilizando la API de seguridad de documentos (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto de API cliente de Document Security

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `DocumentSecurityClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recuperar un documento PDF protegido por políticas

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF protegido por políticas utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Revocar el documento protegido por políticas

   * Cree un objeto `DocumentManager` invocando el método `DocumentSecurityClient` del objeto `getDocumentManager`.
   * Recupere el valor del identificador de licencia del documento protegido por políticas invocando el método `DocumentManager` del objeto `getLicenseId`. Pase el objeto `com.adobe.idp.Document` que representa el documento protegido por políticas. Este método devuelve un valor de cadena que representa el valor del identificador de licencia.
   * Cree un objeto `LicenseManager` invocando el método `DocumentSecurityClient` del objeto `getLicenseManager`.
   * Revocar el documento protegido por políticas invocando el método `LicenseManager` del objeto `revokeLicense` y pasando los siguientes valores:

      * Un valor de cadena que especifica el valor del identificador de licencia del documento protegido por políticas (especifique el valor devuelto del método `DocumentManager` del objeto `getLicenseId`).
      * Miembro de datos estáticos de la interfaz `License` que especifica el motivo para revocar el documento. Por ejemplo, puede especificar `License.DOCUMENT_REVISED`.
      * Un valor `java.net.URL` que especifica la ubicación donde se encuentra un documento revisado. Si no desea redirigir a un usuario a otra dirección URL, puede pasar `null`.

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio de seguridad de documentos, consulte Inicio rápido siguiente:

* &quot;Inicio rápido (modo SOAP): Revocación de un documento mediante la API de Java&quot;

### Revocar el acceso a los documentos mediante la API de servicio web {#revoke-access-to-documents-using-the-web-service-api}

Revocar el acceso a un documento PDF protegido por una política utilizando la API de seguridad de documentos (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Crear un objeto de API cliente de Document Security

   * Cree un objeto `DocumentSecurityServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `DocumentSecurityServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `DocumentSecurityServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperar un documento PDF protegido por políticas

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF protegido por políticas que se revoque.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF protegido por políticas que desea revocar y el modo en que desea abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Revocar el documento protegido por políticas

   * Recupere el valor del identificador de licencia del documento protegido por políticas invocando el método `DocumentSecurityServiceClient` del objeto `getLicenseID` y pasando el objeto `BLOB` que representa el documento protegido por políticas. Este método devuelve un valor de cadena que representa el identificador de licencia.
   * Revocar el documento protegido por políticas invocando el método `DocumentSecurityServiceClient` del objeto `revokeLicense` y pasando los siguientes valores:

      * Un valor de cadena que especifica el valor del identificador de licencia del documento protegido por políticas (especifique el valor devuelto del método `DocumentSecurityServiceService` del objeto `getLicenseId`).
      * Miembro de datos estáticos de la enumeración `Reason` que especifica el motivo para revocar el documento. Por ejemplo, puede especificar `Reason.DOCUMENT_REVISED`.
      * Un valor `string` que especifica la ubicación URL donde se encuentra un documento revisado. Si no desea redirigir a un usuario a otra dirección URL, puede pasar `null`.

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio de seguridad de documentos, consulte Inicio rápido siguiente:

* &quot;Inicio rápido (MTOM): Revocación de un documento mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Revocación de un documento mediante la API de servicio web&quot;

**Consulte también**

[Eliminación de directivas de documentos de Word](protecting-documents-policies.md#removing-policies-from-word-documents)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Restablecimiento del acceso a documentos revocados {#reinstating-access-to-revoked-documents}

Puede restablecer el acceso a un documento PDF revocado, lo que hace que todos los usuarios tengan acceso a todas las copias del documento revocado. Cuando un usuario abre un documento restablecido que fue revocado, puede ver el documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio de seguridad de documentos, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-6}

Para restablecer el acceso a un documento PDF revocado, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API cliente de Document Security.
1. Recupere el identificador de licencia del documento PDF revocado.
1. Restablezca el acceso al documento PDF revocado.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API cliente de Document Security**

Para poder realizar una operación de servicio Document Security mediante programación, debe crear un objeto cliente de servicio Document Security. Si utiliza la API de Java, cree un objeto `DocumentSecurityClient`. Si utiliza la API del servicio web de Document Security, cree un objeto `DocumentSecurityServiceService`.

**Recuperar el identificador de licencia del documento PDF revocado**

Debe recuperar el identificador de licencia del documento PDF revocado para restablecer un documento PDF revocado. Después de obtener el valor del identificador de licencia, puede restablecer un documento revocado. Si intenta restablecer un documento que no se revoque, provocará una excepción.

**Restablecer el acceso al documento PDF revocado**

Para restablecer el acceso a un documento PDF revocado, debe especificar el identificador de licencia del documento revocado. Si intenta restablecer el acceso a un documento PDF que no se revoque, provocará una excepción.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicación de directivas a documentos PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Revocación del acceso a los documentos](protecting-documents-policies.md#revoking-access-to-documents)

### Restablecer el acceso a los documentos revocados mediante la API de Java {#reinstate-access-to-revoked-documents-using-the-java-api}

Restablezca el acceso a un documento revocado mediante la API de seguridad de documentos (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `DocumentSecurityClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recupere el identificador de licencia del documento PDF revocado.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF revocado utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.
   * Cree un objeto `DocumentManager` invocando el método `DocumentSecurityClient` del objeto `getDocumentManager`.
   * Recupere el valor del identificador de licencia del documento revocado invocando el método `DocumentManager` del objeto `getLicenseId` y pasando el objeto `com.adobe.idp.Document` que representa el documento revocado. Este método devuelve un valor de cadena que representa el identificador de licencia.

1. Restablezca el acceso al documento PDF revocado.

   * Cree un objeto `LicenseManager` invocando el método `DocumentSecurityClient` del objeto `getLicenseManager`.
   * Restablezca el acceso al documento PDF revocado invocando el método `LicenseManager` del objeto `unrevokeLicense` y pasando el valor del identificador de licencia del documento revocado.

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio de seguridad de documentos, consulte Inicio rápido siguiente:

* &quot;Inicio rápido (modo SOAP): Restablecimiento del acceso a un documento revocado mediante la API de servicio web&quot;

### Restablecer el acceso a los documentos revocados mediante la API de servicio web {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Restablezca el acceso a un documento revocado mediante la API de seguridad de documentos (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `DocumentSecurityServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `DocumentSecurityServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `DocumentSecurityServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere el identificador de licencia del documento PDF revocado.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF revocado al que se restablece el acceso.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF revocado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Restablezca el acceso al documento PDF revocado.

   * Recupere el valor del identificador de licencia del documento revocado invocando el método `DocumentSecurityServiceClient` del objeto `getLicenseID` y pasando el objeto `BLOB` que representa el documento revocado. Este método devuelve un valor de cadena que representa el identificador de licencia.
   * Restablezca el acceso al documento PDF revocado invocando el método `DocumentSecurityServiceClient` del objeto `unrevokeLicense` y pasando un valor de cadena que especifica el valor del identificador de licencia del documento PDF revocado (pase el valor devuelto del método `DocumentSecurityServiceClient` del objeto `getLicenseId`).

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio de seguridad de documentos, consulte Inicio rápido siguiente:

* &quot;Inicio rápido (MTOM): Restablecimiento del acceso a un documento revocado mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Restablecimiento del acceso a un documento revocado mediante la API de servicio web&quot;

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Inspección de documentos PDF protegidos por políticas {#inspecting-policy-protected-pdf-documents}

Puede utilizar la API del servicio de seguridad de documentos (Java y servicio web) para inspeccionar documentos PDF protegidos por políticas. La inspección de documentos PDF protegidos por políticas devuelve información sobre el documento PDF protegido por políticas. Por ejemplo, puede determinar la política que se utilizó para proteger el documento y la fecha en que se protegió el documento.

No puede realizar esta tarea si la versión de LiveCycle es 8.x o una versión anterior. La compatibilidad con la inspección de documentos protegidos por políticas se agrega en AEM Forms. Si intenta inspeccionar un documento protegido por una política utilizando el LiveCycle 8.x (o anterior), se produce una excepción.

>[!NOTE]
>
>Para obtener más información sobre el servicio de seguridad de documentos, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-7}

Para inspeccionar un documento PDF protegido por políticas, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API cliente de Document Security.
1. Recupere un documento protegido por políticas para inspeccionar.
1. Obtenga información sobre el documento protegido por políticas.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API cliente de Document Security**

Antes de poder realizar una operación de servicio Document Security mediante programación, cree un objeto cliente de servicio Document Security. Si utiliza la API de Java, cree un objeto `RightsManagementClient`. Si utiliza la API del servicio web de Document Security, cree un objeto `RightsManagementServiceService`.

**Recuperar un documento protegido por políticas para inspeccionar**

Para inspeccionar un documento protegido por políticas, recuperarlo. Si intenta inspeccionar un documento que no está protegido con una directiva o que está revocado, se genera una excepción.

**Inspect el documento**

Después de recuperar un documento protegido por políticas, puede inspeccionarlo.

**Obtener información sobre el documento protegido por políticas**

Después de inspeccionar un documento PDF protegido por políticas, puede obtener información al respecto. Por ejemplo, puede determinar la directiva que se utiliza para proteger el documento.

Si protege un documento con una directiva que pertenece a Mis directivas y luego llama a `RMInspectResult.getPolicysetName` o `RMInspectResult.getPolicysetId`, se devuelve nulo.

Si el documento está protegido mediante una política incluida en un conjunto de políticas (que no sea Mis políticas), `RMInspectResult.getPolicysetName` y `RMInspectResult.getPolicysetId` devuelven cadenas válidas.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Documentos PDF protegidos por políticas de Inspect que utilizan la API de Java {#inspect-policy-protected-pdf-documents-using-the-java-api}

Inspect es un documento PDF protegido por políticas que utiliza la API del servicio de seguridad de documentos (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java. Para obtener información sobre la ubicación de estos archivos, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión. (Consulte [Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).
   * Cree un objeto `RightsManagementClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recupere un documento protegido por políticas para inspeccionar.

   * Cree un objeto `java.io.FileInputStream` que represente el documento PDF protegido por políticas utilizando su constructor. Pase un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Inspect el documento.

   * Cree un objeto `DocumentManager` invocando el método `RightsManagementClient` del objeto `getDocumentManager`.
   * Inspect el documento protegido por políticas invocando el método `LicenseManager` del objeto `inspectDocument`. Pase el objeto `com.adobe.idp.Document` que contiene el documento PDF protegido por políticas. Este método devuelve un objeto `RMInspectResult` que contiene información sobre el documento protegido por políticas.

1. Obtenga información sobre el documento protegido por políticas.

   Para obtener información sobre el documento protegido por políticas, invoque el método apropiado que pertenece al objeto `RMInspectResult`. Por ejemplo, para recuperar el nombre de la directiva, invoque el método `RMInspectResult` del objeto `getPolicyName`.

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio de seguridad de documentos, consulte Inicio rápido siguiente:

* &quot;Inicio rápido (modo SOAP): Inspección de documentos PDF protegidos por políticas mediante la API de Java&quot;

### Documentos PDF protegidos por políticas de Inspect que utilizan la API de servicio web {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Inspect es un documento PDF protegido por políticas que utiliza la API del servicio de seguridad de documentos (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `RightsManagementServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `RightsManagementServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `RightsManagementServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere un documento protegido por políticas para inspeccionar.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento PDF que inspeccionar.
   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Inspect el documento.

   Inspect el documento protegido por políticas invocando el método `RightsManagementServiceClient` del objeto `inspectDocument`. Pase el objeto `BLOB` que contiene el documento PDF protegido por políticas. Este método devuelve un objeto `RMInspectResult` que contiene información sobre el documento protegido por políticas.

1. Obtenga información sobre el documento protegido por políticas.

   Para obtener información sobre el documento protegido por políticas, obtenga el valor del campo correspondiente que pertenece al objeto `RMInspectResult`. Por ejemplo, para recuperar el nombre de la directiva, obtenga el valor del campo `RMInspectResult` del objeto `policyName`.

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio de seguridad de documentos, consulte Inicio rápido siguiente:

* &quot;Inicio rápido (MTOM): Inspección de documentos PDF protegidos por políticas mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Inspección de documentos PDF protegidos por políticas mediante la API de servicio web&quot;

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Creación de marcas de agua {#creating-watermarks}

Las marcas de agua ayudan a garantizar la seguridad de un documento al identificar de forma exclusiva el documento y controlar la infracción de los derechos de autor. Por ejemplo, puede crear y colocar una marca de agua que indique Confidencial en todas las páginas de un documento. Después de crear una marca de agua, puede incluirla como parte de una directiva. Es decir, puede establecer el atributo de marca de agua de la política con la marca de agua recién creada. Después de aplicar a un documento una directiva que contiene una marca de agua, esta aparece en el documento protegido por políticas.

>[!NOTE]
>
>Solo los usuarios con privilegios administrativos de Document Security pueden crear marcas de agua. Es decir, debe especificar dicho usuario al definir la configuración de conexión necesaria para crear un objeto cliente del servicio Document Security.

>[!NOTE]
>
>Para obtener más información sobre el servicio de seguridad de documentos, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-8}

Para crear una marca de agua, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API cliente de Document Security.
1. Establezca los atributos de las marcas de agua.
1. Registre la marca de agua en el servicio Document Security.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API cliente de Document Security**

Para poder realizar una operación de servicio Document Security mediante programación, debe crear un objeto cliente de servicio Document Security. Si utiliza la API de Java, cree un objeto `RightsManagementClient`. Si utiliza la API del servicio web de Document Security, cree un objeto `RightsManagementServiceService`.

**Definición de los atributos de las marcas de agua**

Para crear una nueva marca de agua, debe definir los atributos de marca de agua. El atributo name siempre debe estar definido. Además del atributo name , debe establecer al menos uno de los siguientes atributos:

* Texto personalizado
* Fecha de inclusión
* UserIdIncluded
* UserNameIncluded

En la tabla siguiente se enumeran los pares de clave y valor que son necesarios para crear una marca de agua mediante servicios web.

<table>
 <thead>
  <tr>
   <th><p>Nombre de clave</p></th>
   <th><p>Descripción</p></th>
   <th><p>Value</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERNAME_ENABLED</code></p></td>
   <td><p>Especifica si el nombre de usuario del usuario que abre el documento forma parte de la marca de agua.</p></td>
   <td><p>True o false</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td>
   <td><p>Especifica si la identificación del usuario que abre el documento forma parte de la marca de agua.</p></td>
   <td><p>True o false</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>Especifica si la fecha actual forma parte de la marca de agua.</p></td>
   <td><p>True o false</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>Si este valor es true, el valor del texto personalizado debe especificarse con <code>WaterBackCmd:SRCTEXT</code>.</p></td>
   <td><p>True o false</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>Especifica la opacidad de la marca de agua. El valor predeterminado es 0,5 si no se especifica.</p></td>
   <td><p>Un valor entre 0,0 y 1,0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>Especifica la rotación de la marca de agua. El valor predeterminado es 0 grados.</p></td>
   <td><p>Un valor entre 0 y 359.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>Si se especifica este valor, <code>WaterBackCmd:IS_SIZE_ENABLED</code> debe estar presente y el valor debe ser verdadero. Si no se especifica este atributo, el comportamiento predeterminado se ajusta a la página.</p></td>
   <td><p>Un valor mayor que 0.0 y menor o igual que 1.0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>Especifica la alineación horizontal de la marca de agua. El valor predeterminado es center.</p></td>
   <td><p>izquierda, centro o derecha</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>Especifica la alineación vertical de la marca de agua. El valor predeterminado es center.</p></td>
   <td><p>superior, central o inferior</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>Especifica si la marca de agua es de fondo. El valor predeterminado es false.</p></td>
   <td><p>True o false</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>True si se especifica una escala personalizada. Si este valor es true, también debe especificarse SCALE. Si este valor es false, el valor predeterminado se ajusta a la página.</p></td>
   <td><p>True o false</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>Especifica el texto personalizado para una marca de agua. Si este valor está presente, <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> también debe estar presente y establecerse como verdadero.</p></td>
   <td><p>True o false</p></td>
  </tr>
 </tbody>
</table>

Todas las marcas de agua deben tener uno de los siguientes atributos definidos:

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

Todos los demás atributos son opcionales.

**Registro de la marca de agua**

Una nueva marca de agua debe estar registrada en el servicio de seguridad de documentos para poder utilizarse. Después de registrar una marca de agua, puede utilizarla dentro de las directivas.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicación de directivas a documentos PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Creación de marcas de agua mediante la API de Java {#create-watermarks-using-the-java-api}

Cree una marca de agua utilizando la API de seguridad de documentos (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como `adobe-rightsmanagement-client.jar`, en la ruta de clase del proyecto Java.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `RightsManagementClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Definición de los atributos de marca de agua

   * Cree un objeto `Watermark` invocando el método estático `InfomodelObjectFactory` del objeto `createWatermark`. Este método devuelve un objeto `Watermark`.
   * Establezca el atributo de nombre de la marca de agua invocando el método `Watermark` del objeto `setName` y pasando un valor de cadena que especifica el nombre de la política.
   * Establezca el atributo de fondo de la marca de agua invocando el método `Watermark` del objeto `setBackground` y pasando `true`. Al establecer este atributo, la marca de agua aparece en el fondo del documento.
   * Establezca el atributo de texto personalizado de la marca de agua invocando el método `Watermark` del objeto `setCustomText` y pasando un valor de cadena que represente el texto de la marca de agua.
   * Establezca el atributo de opacidad de la marca de agua invocando el método `Watermark` del objeto `setOpacity` y pasando un valor entero que especifica el nivel de opacidad. Un valor de 100 indica que la marca de agua es completamente opaca y un valor de 0 indica que la marca de agua es completamente transparente.

1. Registre la marca de agua.

   * Cree un objeto `WatermarkManager` invocando el método `RightsManagementClient` del objeto `getWatermarkManager`. Este método devuelve un objeto `WatermarkManager`.
   * Registre la marca de agua invocando el método `WatermarkManager` del objeto `registerWatermark` y pasando el objeto `Watermark` que representa la marca de agua que se va a registrar. Este método devuelve un valor de cadena que representa el valor de identificación de la marca de agua.

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio de seguridad de documentos, consulte Inicio rápido siguiente:

* &quot;Inicio rápido (modo SOAP): Creación de una marca de agua mediante la API de Java&quot;

### Creación de marcas de agua mediante la API de servicio web {#create-watermarks-using-the-web-service-api}

Cree una marca de agua utilizando la API de seguridad de documentos (servicio web):

1. Cree un objeto de API cliente de Document Security.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `RightsManagementServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `RightsManagementServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `RightsManagementServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Establezca los atributos de marca de agua.

   * Cree un objeto `WatermarkSpec` invocando el constructor `WatermarkSpec`.
   * Establezca el nombre de la marca de agua asignando un valor de cadena al miembro de datos `WatermarkSpec` del objeto `name`.
   * Establezca el atributo `id` de la marca de agua asignando un valor de cadena al miembro de datos `WatermarkSpec` del objeto `id`.
   * Para que establezca cada propiedad de marca de agua, cree un objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` independiente.
   * Establezca el valor clave asignando un valor al miembro de datos `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` (por ejemplo, `WaterBackCmd:OPACITY)`).
   * Establezca el valor asignando un valor al miembro de datos `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` (por ejemplo, `.25`).
   * Cree un objeto `MyArrayOf_xsd_anyType`. Para cada objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`, invoque el método `MyArrayOf_xsd_anyType` del objeto `Add`. Pase el objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Asigne el objeto `MyArrayOf_xsd_anyType` al miembro de datos `WatermarkSpec` del objeto `values`.

1. Registre la marca de agua.

   Registre la marca de agua invocando el método `RightsManagementServiceClient` del objeto `registerWatermark` y pasando el objeto `WatermarkSpec` que representa la marca de agua que se va a registrar.

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio de seguridad de documentos, consulte Inicio rápido siguiente:

* &quot;Inicio rápido (MTOM): Creación de una marca de agua mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Creación de una marca de agua mediante la API de servicio web&quot;

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modificación de marcas de agua {#modifying-watermarks}

Puede modificar una marca de agua existente mediante la API Java de Document Security o la API de servicio web. Para realizar cambios en una marca de agua existente, debe recuperarla, modificar sus atributos y actualizarla en el servidor. Por ejemplo, suponga que recupera una marca de agua y modifica su atributo de opacidad. Antes de que el cambio surta efecto, debe actualizar la marca de agua.

Cuando se modifica una marca de agua, el cambio afecta a los documentos futuros que tengan la marca de agua aplicada a ellos. Es decir, los documentos PDF existentes que contienen la marca de agua no se ven afectados.

>[!NOTE]
>
>Solo los usuarios con privilegios administrativos de Document Security pueden modificar las marcas de agua. Es decir, debe especificar dicho usuario al definir la configuración de conexión necesaria para crear un objeto cliente del servicio Document Security.

>[!NOTE]
>
>Para obtener más información sobre el servicio de seguridad de documentos, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-9}

Para modificar una marca de agua, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API cliente de Document Security.
1. Recupere la marca de agua que desea modificar.
1. Establezca los atributos de las marcas de agua.
1. Actualice la marca de agua.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API cliente de Document Security**

Para poder realizar una operación de servicio Document Security mediante programación, debe crear un objeto cliente de servicio Document Security. Si utiliza la API de Java, cree un objeto `DocumentSecurityClient`. Si utiliza la API del servicio web de Document Security, cree un objeto `DocumentSecurityServiceService`.

**Recupere la marca de agua para modificar**

Para modificar una marca de agua, debe recuperar una marca de agua existente. Puede recuperar una marca de agua especificando su nombre o especificando su valor identificador.

**Definición de los atributos de las marcas de agua**

Para modificar una marca de agua existente, cambie el valor de uno o varios atributos de marca de agua. Al actualizar mediante programación una marca de agua mediante un servicio Web, debe definir todos los atributos que se establecieron originalmente, incluso aunque el valor no cambie. Por ejemplo, supongamos que se establecen los siguientes atributos de marca de agua: `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY` y `WaterBackCmd:SRCTEXT`. Aunque el único atributo que desea modificar es `WaterBackCmd:OPACITY`, debe establecer que los demás valores estén bien.

>[!NOTE]
>
>Al utilizar la API de Java para modificar una marca de agua, no es necesario especificar todos los atributos. Establezca el atributo de marca de agua que desea modificar.

>[!NOTE]
>
>Para obtener información sobre los nombres de atributos de marca de agua, consulte [Creación de marcas de agua](protecting-documents-policies.md#creating-watermarks).

**Actualizar la marca de agua**

Después de modificar los atributos de una marca de agua, debe actualizarla.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Creación de marcas de agua](protecting-documents-policies.md#creating-watermarks)

### Modificación de marcas de agua mediante la API de Java {#modify-watermarks-using-the-java-api}

Modifique una marca de agua utilizando la API de seguridad de documentos (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `DocumentSecurityClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recupere la marca de agua que desea modificar.

   Cree un objeto `WatermarkManager` invocando el método `DocumentSecurityClient` del objeto `getWatermarkManager` y pase un valor de cadena que especifique el nombre de la marca de agua. Este método devuelve un objeto `Watermark` que representa la marca de agua que se va a modificar.

1. Establezca los atributos de marca de agua.

   Establezca el atributo de opacidad de la marca de agua invocando el método `Watermark` del objeto `setOpacity` y pasando un valor entero que especifica el nivel de opacidad. Un valor de 100 indica que la marca de agua es completamente opaca y un valor de 0 indica que la marca de agua es completamente transparente.

   >[!NOTE]
   >
   >En este ejemplo solo se modifica el atributo de opacidad.

1. Actualice la marca de agua.

   * Actualice la marca de agua invocando el método `WatermarkManager` del objeto `updateWatermark` y pasando el objeto `Watermark` cuyo atributo se modificó.

**Ejemplos de código**

Para obtener ejemplos de código mediante el servicio Document Security, consulte Inicio rápido (modo SOAP): Modificación de una marca de agua mediante la sección API de Java.

### Modificación de marcas de agua mediante la API de servicio web {#modify-watermarks-using-the-web-service-api}

Modifique una marca de agua utilizando la API de seguridad de documentos (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `DocumentSecurityServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `RightsManagementServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `DocumentSecurityServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere la marca de agua que desea modificar.

   Recupere la marca de agua que desea modificar invocando el método `DocumentSecurityServiceClient` del objeto `getWatermarkByName`. Pase un valor de cadena que especifique el nombre de la marca de agua. Este método devuelve un objeto `WatermarkSpec` que representa la marca de agua que se va a modificar.

1. Establezca los atributos de marca de agua.

   * Para que cada propiedad de marca de agua se actualice, cree un objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` independiente.
   * Establezca el valor clave asignando un valor al miembro de datos `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `key` (por ejemplo, `WaterBackCmd:OPACITY)`).
   * Establezca el valor asignando un valor al miembro de datos `MyMapOf_xsd_string_To_xsd_anyType_Item` del objeto `value` (por ejemplo, `.50`).
   * Cree un objeto `MyArrayOf_xsd_anyType`. Para cada objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`, invoque el método `MyArrayOf_xsd_anyType` del objeto `Add`. Pase el objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Asigne el objeto `MyArrayOf_xsd_anyType` al miembro de datos `WatermarkSpec` del objeto `values`.

1. Actualice la marca de agua.

   Actualice la marca de agua invocando el método `DocumentSecurityServiceClient` del objeto `updateWatermark` y pasando el objeto `WatermarkSpec` que representa la marca de agua que se va a modificar.

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio Document Security, consulte el siguiente Inicio rápido:

* &quot;Inicio rápido (MTOM): Modificación de una marca de agua mediante la API de servicio web&quot;

## Búsqueda de eventos {#searching-for-events}

El servicio de Rights Management realiza el seguimiento de las acciones específicas a medida que se producen, como la aplicación de una política a un documento, la apertura de un documento protegido por políticas y la revocación del acceso a los documentos. La auditoría de eventos debe estar habilitada para el servicio de Rights Management o no se debe realizar un seguimiento de los eventos.

Los eventos se dividen en una de las siguientes categorías:

* Los eventos de administrador son acciones relacionadas con un administrador, como la creación de una nueva cuenta de administrador.
* Los eventos de documento son acciones relacionadas con un documento, como cerrar un documento protegido por políticas.
* Los eventos de política son acciones relacionadas con una política, como la creación de una política nueva.
* Los eventos de servicio son acciones relacionadas con el servicio de Rights Management, como la sincronización con el directorio de usuario.

Puede buscar eventos específicos utilizando la API de Java del Rights Management o la API de servicio web. Al buscar eventos, puede realizar tareas, como crear un archivo de registro de ciertos eventos.

>[!NOTE]
>
>Para obtener más información sobre el servicio de Rights Management, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-10}

Para buscar un evento de Rights Management, realice los pasos siguientes:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Rights Management.
1. Especifique el evento para el que desea buscar.
1. Busque el evento .

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de cliente de Rights Management**

Para poder realizar una operación de servicio de Rights Management mediante programación, debe crear un objeto cliente de servicio de Rights Management. Si utiliza la API de Java, cree un objeto `DocumentSecurityClient`. Si utiliza la API de servicio web de Rights Management, cree un objeto `DocumentSecurityServiceService`.

**Especifique los eventos para buscar**

Debe especificar el evento que desea buscar. Por ejemplo, puede buscar el evento de creación de directivas, que se produce cuando se crea una política nueva.

**Buscar el evento**

Después de especificar el evento que se va a buscar, puede utilizar la API de Java de Rights Management o la API de servicio web de Rights Management para buscar el evento.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Buscar eventos usando la API de Java {#search-for-events-using-the-java-api}

Busque eventos mediante la API de Rights Management (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Creación de un objeto de API de cliente de Rights Management

   Cree un objeto `DocumentSecurityClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Especifique los eventos para buscar

   * Cree un objeto `EventManager` invocando el método `DocumentSecurityClient` del objeto `getEventManager`. Este método devuelve un objeto `EventManager`.
   * Cree un objeto `EventSearchFilter` invocando su constructor.
   * Especifique el evento para el que desea buscar invocando el método `EventSearchFilter` del objeto `setEventCode` y pasando un miembro de datos estáticos que pertenece a la clase `EventManager` que representa el evento para el que desea buscar. Por ejemplo, para buscar el evento de creación de directivas, pase `EventManager.POLICY_CREATE_EVENT`.

   >[!NOTE]
   >
   >Puede definir criterios de búsqueda adicionales invocando métodos de objeto `EventSearchFilter`. Por ejemplo, invoque el método `setUserName` para especificar un usuario asociado al evento.

1. Buscar el evento

   Busque el evento invocando el método `EventManager` del objeto `searchForEvents` y pasando el objeto `EventSearchFilter` que define los criterios de búsqueda del evento. Este método devuelve una matriz de objetos `Event`.

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio de Rights Management, consulte los siguientes ejemplos de inicio rápido:

* &quot;Inicio rápido (SOAP): Búsqueda de eventos mediante la API de Java&quot;

### Buscar eventos usando la API de servicio web {#search-for-events-using-the-web-service-api}

Busque eventos mediante la API de Rights Management (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Creación de un objeto de API de cliente de Rights Management

   * Cree un objeto `DocumentSecurityServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `DocumentSecurityServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `DocumentSecurityServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Especifique los eventos para buscar

   * Cree un objeto `EventSpec` utilizando su constructor.
   * Especifique el inicio del período de tiempo durante el cual se produjo el evento estableciendo el miembro de datos `EventSpec` del objeto `firstTime.date` con la instancia `DataTime` que representa el inicio del intervalo de fechas en el que se produjo el evento.
   * Asigne el valor `true` al miembro de datos `EventSpec` del objeto `firstTime.dateSpecified`.
   * Especifique el final del período de tiempo durante el cual se produjo el evento estableciendo el miembro de datos `EventSpec` del objeto `lastTime.date` con la instancia `DataTime` que representa el final del intervalo de fechas en el que se produjo el evento.
   * Asigne el valor `true` al miembro de datos `EventSpec` del objeto `lastTime.dateSpecified`.
   * Configure el evento para buscar asignando un valor de cadena al miembro de datos `EventSpec` del objeto `eventCode`. La tabla siguiente muestra los valores numéricos que se pueden asignar a esta propiedad:

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

   Busque el evento invocando el método `DocumentSecurityServiceClient` del objeto `searchForEvents` y pasando el objeto `EventSpec` que representa el evento para el que desea buscar y el número máximo de resultados. Este método devuelve una colección `MyArrayOf_xsd_anyType` donde cada elemento es una instancia `AuditSpec`. Con una instancia `AuditSpec`, puede obtener información sobre el evento, como la hora en que se produjo. La instancia `AuditSpec` contiene un miembro de datos `timestamp` que especifica esta información.

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio de Rights Management, consulte los siguientes ejemplos de inicio rápido:

* &quot;Inicio rápido (MTOM): Búsqueda de eventos mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Búsqueda de eventos mediante la API de servicio web&quot;

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Aplicación de directivas a documentos de Word {#applying-policies-to-word-documents}

Además de los documentos PDF, el servicio Rights Management admite formatos de documento adicionales, como un documento de Microsoft Word (archivo DOC) y otros formatos de archivo de Microsoft Office. Por ejemplo, puede aplicar una política a un documento de Word para protegerlo. Al aplicar una directiva a un documento de Word, se restringe el acceso al documento. No puede aplicar una directiva a un documento si el documento ya está protegido con una directiva.

Después de distribuirlo, puede supervisar el uso de un documento de Word protegido por políticas. Es decir, puede ver cómo se utiliza el documento y quién lo utiliza. Por ejemplo, puede averiguar cuándo alguien ha abierto el documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio de seguridad de documentos, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-11}

Para aplicar una directiva a un documento de Word, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API cliente de Document Security.
1. Recupere un documento de Word al que se aplica una política.
1. Aplicar una política existente al documento de Word.
1. Guarde el documento de Word protegido por políticas.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Creación de un objeto API cliente de Document Security**

Para poder realizar una operación de servicio Document Security mediante programación, debe crear un objeto cliente de servicio Document Security.

**Recuperar un documento de Word**

Debe recuperar un documento de Word para aplicar una directiva. Después de aplicar una directiva al documento de Word, los usuarios se ven restringidos al usar el documento. Por ejemplo, si la directiva no permite abrir el documento sin conexión, los usuarios deben estar en línea para abrirlo.

**Aplicar una política existente al documento de Word**

Para aplicar una directiva a un documento de Word, debe hacer referencia a una directiva existente y especificar a qué conjunto de directivas pertenece la directiva. El usuario que esté configurando las propiedades de conexión debe tener acceso a la directiva especificada. Si no es así, se produce una excepción.

**Guardar el documento de Word**

Después de que el servicio de seguridad de documentos aplique una directiva a un documento de Word, puede guardar el documento de Word protegido por políticas como un archivo DOC.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revocación del acceso a los documentos](protecting-documents-policies.md#revoking-access-to-documents)

### Aplicar una directiva a un documento de Word utilizando la API de Java {#apply-a-policy-to-a-word-document-using-the-java-api}

Aplique una directiva a un documento de Word utilizando la API de seguridad de documentos (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `DocumentSecurityClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recupere un documento de Word.

   * Cree un objeto `java.io.FileInputStream` que represente el documento de Word utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento de Word.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Aplicar una política existente al documento de Word.

   * Cree un objeto `DocumentManager` invocando el método `DocumentSecurityClient` del objeto `getDocumentManager`.
   * Aplique una política al documento de Word invocando el método `DocumentManager` del objeto `protectDocument` y pasando los siguientes valores:

      * El objeto `com.adobe.idp.Document` que contiene el documento de Word al que se aplica la política.
      * Un valor de cadena que especifica el nombre del documento.
      * Un valor de cadena que especifica el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar un valor `null` que resulte en el uso del conjunto de directivas `MyPolicies`.
      * Un valor de cadena que especifica el nombre de la directiva.
      * Un valor de cadena que representa el nombre del dominio de administrador de usuarios del usuario que es el editor del documento. Este valor del parámetro es opcional y puede ser nulo (si este parámetro es nulo, el siguiente valor del parámetro debe ser nulo).
      * Un valor de cadena que representa el nombre canónico del usuario administrador de usuarios que es el editor del documento. Este valor de parámetro es opcional y puede ser `null` (si este parámetro es `null`, el valor del parámetro anterior debe ser `null`).
      * `com.adobe.livecycle.rightsmanagement.Locale` que representa la configuración regional que se utiliza para seleccionar la plantilla de MS Office. Este valor de parámetro es opcional y puede especificar `null`.

      El método `protectDocument` devuelve un objeto `RMSecureDocumentResult` que contiene el documento de Word protegido por políticas.


1. Guarde el documento de Word.

   * Invoque el método `RMSecureDocumentResult` del objeto `getProtectedDoc` para obtener el documento de Word protegido por políticas. Este método devuelve un objeto `com.adobe.idp.Document`.
   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea DOC.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del objeto `Document` en el archivo (asegúrese de utilizar el objeto `Document` que devolvió el método `getProtectedDoc`).

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio Document Security, consulte el siguiente Inicio rápido:

* &quot;Inicio rápido (modo SOAP): Aplicación de una directiva a un documento de Word mediante la API de Java&quot;

### Aplicar una directiva a un documento de Word utilizando la API de servicio Web {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Aplique una política a un documento de Word utilizando la API de seguridad de documentos (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto de API cliente de Document Security.

   * Cree un objeto `DocumentSecurityServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `DocumentSecurityServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `DocumentSecurityServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere un documento de Word.

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar un documento de Word al que se aplica una política.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento de Word y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Determine el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read`. Pase la matriz de bytes, la posición de inicio y la longitud del flujo para leerlos.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Aplicar una política existente al documento de Word.

   Aplique una política al documento de Word invocando el método `DocumentSecurityServiceClient` del objeto `protectDocument` y pasando los siguientes valores:

   * El objeto `BLOB` que contiene el documento de Word al que se aplica la política.
   * Un valor de cadena que especifica el nombre del documento.
   * Un valor de cadena que especifica el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar un valor `null` que resulte en el uso del conjunto de directivas `MyPolicies`.
   * Un valor de cadena que especifica el nombre de la directiva.
   * Un valor de cadena que representa el nombre del dominio de administrador de usuarios del usuario que es el editor del documento. Este valor de parámetro es opcional y puede ser nulo (si este parámetro es nulo, el siguiente valor de parámetro debe ser `null`).
   * Un valor de cadena que representa el nombre canónico del usuario administrador de usuarios que es el editor del documento. Este valor de parámetro es opcional y puede ser nulo (si este parámetro es nulo, el valor del parámetro anterior debe ser `null`).
   * Un valor `RMLocale` que especifica el valor de configuración regional (por ejemplo, `RMLocale.en`).
   * Un parámetro de salida de cadena que se utiliza para almacenar el valor del identificador de la política.
   * Un parámetro de salida de cadena que se utiliza para almacenar el valor del identificador protegido por políticas.
   * Un parámetro de salida de cadena que se utiliza para almacenar el tipo mime (por ejemplo, `application/doc`).

   El método `protectDocument` devuelve un objeto `BLOB` que contiene el documento de Word protegido por políticas.

1. Guarde el documento de Word.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento de Word protegido por políticas.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` que el método `protectDocument` devolvió. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo de Word invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio Document Security, consulte el siguiente Inicio rápido:

* &quot;Inicio rápido (MTOM): Aplicación de una directiva a un documento de Word mediante la API de servicio Web&quot;

## Eliminación de directivas de documentos de Word {#removing-policies-from-word-documents}

Puede quitar una directiva de un documento de Word protegido por políticas para quitar la seguridad del documento. Es decir, si ya no desea que el documento esté protegido por una directiva. Si desea actualizar un documento de Word protegido por políticas con una directiva más reciente, en lugar de quitar la directiva y agregar la directiva actualizada, es más eficaz cambiar la directiva.

>[!NOTE]
>
>Para obtener más información sobre el servicio de seguridad de documentos, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-12}

Para quitar una directiva de un documento de Word protegido por políticas, realice los siguientes pasos:

1. Incluir archivos de proyecto
1. Cree un objeto de API cliente de Document Security.
1. Recupere un documento de Word protegido por políticas.
1. Elimine la directiva del documento de Word.
1. Guarde los documentos de Word no protegidos

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API cliente de Document Security**

Antes de poder realizar una operación de servicio Document Security mediante programación, cree un objeto cliente de servicio Document Security.

**Recuperar un documento de Word protegido por políticas**

Debe recuperar un documento de Word protegido por políticas para eliminar una directiva. Si intenta quitar una directiva de un documento de Word que no esté protegido por una directiva, provocará una excepción.

**Quitar la directiva del documento de Word**

Puede quitar una directiva de un documento de Word protegido por políticas siempre que se especifique un administrador en la configuración de conexión. Si no es así, la política utilizada para proteger un documento debe contener el permiso `SWITCH_POLICY` para eliminar una política de un documento de Word. Además, el usuario especificado en la configuración de conexión de AEM Forms también debe tener ese permiso. De lo contrario, se genera una excepción.

**Guardar el documento de Word no protegido**

Una vez que el servicio de seguridad de documentos elimina una directiva de un documento de Word, puede guardar el documento de Word no protegido como un archivo DOC.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicación de directivas a documentos de Word](protecting-documents-policies.md#applying-policies-to-word-documents)

### Eliminar una directiva de un documento de Word mediante la API de Java {#remove-a-policy-from-a-word-document-using-the-java-api}

Elimine una directiva de un documento de Word protegido por políticas utilizando la API de seguridad de documentos (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR del cliente, como adobe-rightsmanagement-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto de API cliente de Document Security

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `RightsManagementClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recuperar un documento de Word protegido por políticas

   * Cree un objeto `java.io.FileInputStream` que represente el documento de Word protegido por políticas utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento de Word.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Quitar la directiva del documento de Word

   * Cree un objeto `DocumentManager` invocando el método `RightsManagementClient` del objeto `getDocumentManager`.
   * Elimine una directiva del documento de Word invocando el método `DocumentManager` del objeto `removeSecurity` y pasando el objeto `com.adobe.idp.Document` que contiene el documento de Word protegido por políticas. Este método devuelve un objeto `com.adobe.idp.Document` que contiene un documento de Word no protegido.

1. Guardar el documento de Word no protegido

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea DOC.
   * Invoque el método `Document` del objeto `copyToFile` para copiar el contenido del objeto `Document` en el archivo (asegúrese de utilizar el objeto `Document` que devolvió el método `removeSecurity`).

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio Document Security, consulte el siguiente Inicio rápido:

* &quot;Inicio rápido (modo SOAP): Eliminación de una directiva de un documento de Word mediante la API de Java&quot;

### Eliminar una directiva de un documento de Word utilizando la API de servicio Web {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Elimine una directiva de un documento de Word protegido por políticas utilizando la API de seguridad de documentos (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Crear un objeto de API cliente de Document Security

   * Cree un objeto `RightsManagementServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `RightsManagementServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `RightsManagementServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperar un documento de Word protegido por políticas

   * Cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se utiliza para almacenar el documento de Word protegido por políticas del que se quita la directiva.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento de Word y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de flujo invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición de inicio y la longitud de flujo para leer.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Quitar la directiva del documento de Word

   Elimine la directiva del documento de Word invocando el método `RightsManagementServiceClient` del objeto `removePolicySecurity` y pasando el objeto `BLOB` que contiene el documento de Word protegido por políticas. Este método devuelve un objeto `BLOB` que contiene un documento de Word no protegido.

1. Guardar el documento de Word no protegido

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento de Word no protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` que el método `removePolicySecurity` devolvió. Rellene la matriz de bytes obteniendo el valor del campo `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.

**Ejemplos de código**

Para ver ejemplos de código que utilicen el servicio Document Security, consulte el siguiente Inicio rápido:

* &quot;Inicio rápido (MTOM): Eliminación de una directiva de un documento de Word mediante la API de servicio Web&quot;

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
