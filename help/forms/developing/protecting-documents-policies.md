---
title: Protección de documentos con políticas
seo-title: Protección de documentos con políticas
description: nulo
seo-description: nulo
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Protección de documentos con políticas {#protecting-documents-with-policies}

**Acerca de Document Security Service**

El servicio de Document Security permite a los usuarios aplicar de forma dinámica la configuración de confidencialidad a los documentos PDF de Adobe y mantener el control sobre los documentos, independientemente de la amplia distribución que se distribuyan.

El servicio Document Security evita que la información se extienda más allá del alcance del usuario, ya que permite a los usuarios mantener el control sobre cómo los destinatarios utilizan el documento PDF protegido por una política. Un usuario puede especificar quién puede abrir un documento, limitar su uso y supervisar el documento después de distribuirlo. Un usuario también puede controlar dinámicamente el acceso a un documento protegido por una política e incluso puede anular dinámicamente el acceso al documento.

El servicio Document Security también protege otros tipos de archivos, como los archivos de Microsoft Word (DOC). Puede utilizar la API del cliente de Document Security para trabajar con estos tipos de archivo. Se admiten las siguientes versiones:

* Archivos de Microsoft Office 2003 (DOC, XLS, PPT)
* Archivos de Microsoft Office 2007 (archivos DOCX, XLSX, PPTX)
* Archivos PTC Pro/E

Para mayor claridad, en las dos secciones siguientes se explica cómo trabajar con documentos de Word:

* [Aplicación de políticas a documentos de Word](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Eliminación de directivas de documentos de Word](protecting-documents-policies.md#removing-policies-from-word-documents)

Puede realizar estas tareas mediante el servicio Document Security:

* Crear directivas. Para obtener más información, consulte [Creación de políticas](protecting-documents-policies.md#creating-policies).
* Modificar directivas. Para obtener más información, consulte [Modificación de políticas](protecting-documents-policies.md#modifying-policies).
* Eliminar directivas. Para obtener más información, consulte [Eliminación de directivas](protecting-documents-policies.md#deleting-policies).
* Aplicar directivas a documentos PDF. Para obtener más información, consulte [Aplicación de políticas a documentos](protecting-documents-policies.md#applying-policies-to-pdf-documents)PDF.
* Quitar directivas de documentos PDF. Para obtener más información, consulte [Eliminación de directivas de documentos](protecting-documents-policies.md#removing-policies-from-pdf-documents)PDF.
* Inspeccione los documentos protegidos por políticas. Para obtener más información, consulte [Inspección de documentos](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents)PDF protegidos por políticas.
* Revocar el acceso a documentos PDF. Para obtener más información, consulte [Revocación del acceso a documentos](protecting-documents-policies.md#revoking-access-to-documents).
* Restablece el acceso a los documentos revocados. Para obtener más información, consulte [Restablecimiento del acceso a documentos](protecting-documents-policies.md#reinstating-access-to-revoked-documents)revocados.
* Crear marcas de agua. Para obtener más información, consulte [Creación de marcas de agua](protecting-documents-policies.md#creating-watermarks).
* Buscar eventos. Para obtener más información, consulte [Búsqueda de eventos](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Creación de políticas {#creating-policies}

Puede crear políticas mediante programación mediante la API de Java o la API de servicio Web de Document Security. Una *directiva* es una colección de información que incluye la configuración de seguridad del documento, usuarios autorizados y derechos de uso. Puede crear y guardar cualquier número de directivas, utilizando la configuración de seguridad adecuada para diferentes situaciones y usuarios.

Las políticas le permiten realizar estas tareas:

* Especifique las personas que pueden abrir el documento. Los destinatarios pueden pertenecer a su organización o ser externos a ella.
* Especifique cómo pueden utilizar el documento los destinatarios. Puede restringir el acceso a diferentes funciones de Acrobat y Adobe Reader. Estas funciones incluyen la capacidad de imprimir y copiar texto, agregar firmas y agregar comentarios a un documento.
* Cambie la configuración de acceso y seguridad en cualquier momento, incluso después de distribuir el documento protegido por una política.
* Monitoree el uso del documento después de distribuirlo. Puede ver cómo se utiliza el documento y quién lo utiliza. Por ejemplo, puede averiguar cuándo alguien ha abierto el documento.

### Creación de una directiva mediante servicios Web {#creating-a-policy-using-web-services}

Al crear una directiva mediante la API de servicio Web, haga referencia a un archivo XML existente del lenguaje de derechos de documento portátil (PDRL) que describa la política. Los permisos de directiva y el principal se definen en el documento PDRL. El siguiente documento XML es un ejemplo de documento PDRL.

```as3
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
>Para obtener más información sobre el servicio Document Security, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para crear una directiva, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto API de cliente de Document Security.
1. Defina los atributos de la política.
1. Cree una entrada de directiva.
1. Registre la directiva.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-rightsmanagement-client.jar
* namespace.jar (si AEM Forms está implementado en JBoss)
* jaxb-api.jar (si AEM Forms se implementa en JBoss)
* jaxb-impl.jar (si AEM Forms está implementado en JBoss)
* jaxb-libs.jar (si AEM Forms se implementa en JBoss)
* jaxb-xjc.jar (si AEM Forms está implementado en JBoss)
* relajngDataType.jar (si AEM Forms está implementado en JBoss)
* xsdlib.jar (si AEM Forms está implementado en JBoss)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar (utilice otro archivo JAR si AEM Forms no está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.

**Creación de un objeto de API de Document Security Client**

Antes de realizar una operación de servicio de Document Security mediante programación, cree un objeto cliente de servicio de Document Security.

**Definir los atributos de la política**

Para crear una directiva, defina los atributos de la directiva. Un atributo obligatorio es el nombre de la política. Los nombres de directiva deben ser únicos para cada conjunto de directivas. Un conjunto de políticas es simplemente un conjunto de políticas. Puede haber dos directivas con el mismo nombre si las directivas pertenecen a conjuntos de directivas independientes. Sin embargo, dos directivas dentro de un único conjunto de directivas no pueden tener el mismo nombre de directiva.

Otro atributo útil para establecer es el período de validez. Un período de validez es el período de tiempo durante el cual los destinatarios autorizados pueden acceder a un documento protegido por una política. Si no establece este atributo, la política siempre es válida.

Se puede establecer un período de validez en una de estas opciones:

* Número de días que se puede acceder al documento desde el momento en que se publica
* Una fecha de finalización después de la cual no se puede acceder al documento
* Intervalo de fechas específico para el que se puede acceder al documento
* Siempre válido

Puede especificar sólo una fecha de inicio, lo que resulta en que la directiva sea válida después de la fecha de inicio. Si sólo especifica una fecha de finalización, la política será válida hasta la fecha de finalización. Sin embargo, se genera una excepción si no se definen una fecha de inicio ni una fecha de finalización.

Al establecer atributos que pertenecen a una política, también puede definir la configuración de codificación. Esta configuración de codificación se aplica cuando la política se aplica a un documento. Puede especificar los siguientes valores de codificación:

* **AES256**: Representa el algoritmo de codificación AES con una clave de 256 bits.
* **AES128**: Representa el algoritmo de codificación AES con una clave de 128 bits.
* **** SinCifrado: No representa cifrado.

Al especificar la `NoEncryption` opción, no se puede establecer la `PlaintextMetadata` opción en `false`. Si intenta hacerlo, se genera una excepción.

>[!NOTE]
>
>Para obtener información sobre otros atributos que puede definir, consulte la descripción de la `Policy` interfaz en la Referencia [de API de formularios](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM.

**Crear una entrada de directiva**

Una entrada de directiva adjunta entidades principales, que son grupos y usuarios, y permisos a una directiva. Una política debe tener al menos una entrada de política. Supongamos, por ejemplo, que realiza estas tareas:

* Cree y registre una entrada de directiva que permita que un grupo solo vea un documento mientras esté en línea y prohíba que los destinatarios lo copien.
* Adjunte la entrada de directiva a la directiva.
* Proteja un documento con la política mediante Acrobat.

Estas acciones hacen que los destinatarios solo puedan ver el documento en línea y no puedan copiarlo. El documento permanece seguro hasta que se elimina la seguridad.

**Registrar la directiva**

Se debe registrar una nueva directiva antes de poder utilizarla. Después de registrar una política, puede utilizarla para proteger documentos.

### Creación de una directiva mediante la API de Java {#create-a-policy-using-the-java-api}

Cree una directiva mediante la API de Document Security (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `DocumentSecurityClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Defina los atributos de la política.

   * Cree un `Policy` objeto invocando el `InfomodelObjectFactory` método estático `createPolicy` del objeto. Este método devuelve un `Policy` objeto.
   * Establezca el atributo name de la política invocando el `Policy` método del `setName` objeto y pasando un valor de cadena que especifica el nombre de la política.
   * Defina la descripción de la política invocando el `Policy` método del `setDescription` objeto y pasando un valor de cadena que especifica la descripción de la política.
   * Defina el conjunto de directivas al que pertenece la nueva directiva invocando el `Policy` método `setPolicySetName` del objeto y pasando un valor de cadena que especifica el nombre del conjunto de directivas. (Puede especificar `null` para este valor de parámetro que resulte en que la directiva se agregue al conjunto de directivas *Mis políticas* ).
   * Cree el período de validez de la política invocando el `InfomodelObjectFactory` método estático del `createValidityPeriod` objeto. Este método devuelve un `ValidityPeriod` objeto.
   * Establezca el número de días para el que se puede acceder a un documento protegido por una política invocando el `ValidityPeriod` método del `setRelativeExpirationDays` objeto y pasando un valor entero que especifique el número de días.
   * Establezca el período de validez de la política invocando el `Policy` método del `setValidityPeriod` objeto y pasando el `ValidityPeriod` objeto.

1. Cree una entrada de directiva.

   * Cree una entrada de política invocando el `InfomodelObjectFactory` método estático del `createPolicyEntry` objeto. Este método devuelve un `PolicyEntry` objeto.
   * Especifique los permisos de la directiva invocando el `InfomodelObjectFactory` método estático del `createPermission` objeto. Pase un miembro de datos estático que pertenezca a la `Permission` interfaz que representa el permiso. Este método devuelve un `Permission` objeto. Por ejemplo, para agregar el permiso que permite a los usuarios copiar datos de un documento PDF protegido por una política, pase `Permission.COPY`. (Repita este paso para cada permiso que desee agregar).
   * Agregue el permiso a la entrada de directiva invocando el `PolicyEntry` método del `addPermission` objeto y pasando el `Permission` objeto. (Repita este paso para cada `Permission` objeto que haya creado).
   * Cree el principal de directiva invocando el `InfomodelObjectFactory` método estático del `createSpecialPrincipal` objeto. Pase un miembro de datos que pertenezca al `InfomodelObjectFactory` objeto que representa el principal. Este método devuelve un `Principal` objeto. Por ejemplo, para agregar el publicador del documento como principal, pase `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * Agregue el principal a la entrada de directiva invocando el `PolicyEntry` método del `setPrincipal`objeto y pasando el `Principal` objeto.
   * Agregue la entrada de directiva a la directiva invocando el `Policy` método del `addPolicyEntry` objeto y pasando el `PolicyEntry` objeto.

1. Registre la directiva.

   * Cree un `PolicyManager` objeto invocando el `DocumentSecurityClient` método `getPolicyManager` del objeto.
   * Registre la directiva invocando el `PolicyManager` método del `registerPolicy` objeto y pasando los siguientes valores:

      * El `Policy` objeto que representa la directiva que se va a registrar.
   * Un valor de cadena que representa el conjunto de directivas al que pertenece la directiva.
   Si utiliza una cuenta de administrador de formularios AEM en la configuración de conexión para crear el `DocumentSecurityClient` objeto, especifique el nombre del conjunto de políticas al invocar el `registerPolicy` método. Si pasa un `null` valor para el conjunto de directivas, la directiva se crea en el conjunto de directivas *Mis políticas* de administradores.

   Si utiliza un usuario de Document Security en la configuración de la conexión, puede invocar el `registerPolicy` método de sobrecarga que solo acepta la directiva. Es decir, no es necesario especificar el nombre del conjunto de directivas. Sin embargo, la política se agrega al conjunto de directivas denominado *Mis políticas*. Si no desea agregar la nueva directiva a este conjunto de directivas, especifique un nombre de conjunto de directivas cuando invoque el `registerPolicy` método.

   >[!NOTE]
   >
   >Al crear una directiva, haga referencia a un conjunto de directivas existente. Si especifica un conjunto de directivas que no existe, se genera una excepción.

Para ver ejemplos de código que utilizan el servicio Document Security, consulte:

* &quot;Inicio rápido (modo SOAP): Creación de una directiva mediante la API de Java&quot;

### Creación de una directiva mediante la API de servicio web {#create-a-policy-using-the-web-service-api}

Cree una directiva mediante la API de Document Security (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `DocumentSecurityServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `DocumentSecurityServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `RightsManagementServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Defina los atributos de la política.

   * Cree un `PolicySpec` objeto con su constructor.
   * Defina el nombre de la política asignando un valor de cadena al miembro de datos del `PolicySpec` objeto `name` .
   * Defina la descripción de la política asignando un valor de cadena al miembro de datos del `PolicySpec` objeto `description` .
   * Defina el conjunto de directivas al que pertenecerá la directiva asignando un valor de cadena al miembro de `PolicySpec` datos del `policySetName` objeto. Debe especificar un nombre de conjunto de directivas existente. (Puede especificar `null` para este valor de parámetro que resulte en que la directiva se agregue a *Mis políticas*).
   * Establezca el período de concesión sin conexión de la política asignando un valor entero al miembro de datos del `PolicySpec` objeto `offlineLeasePeriod` .
   * Establezca el miembro de datos del `PolicySpec` `policyXml` objeto con un valor de cadena que represente los datos XML de PDRL. Para realizar esta tarea, cree un objeto .NET `StreamReader` con su constructor. Pase la ubicación de un archivo XML PDRL que represente la directiva al constructor `StreamReader` . A continuación, invoque el `StreamReader` método `ReadLine` del objeto y asigne el valor devuelto a una variable de cadena. Repita el `StreamReader` objeto hasta que el `ReadLine` método devuelva null. Asigne la variable de cadena al miembro de `PolicySpec` datos del `policyXml` objeto.

1. Cree una entrada de directiva.

   No es necesario crear una entrada de política al crear una política con la API de servicio web de Document Security. La entrada de directiva se define en el documento PDRL.

1. Registre la directiva.

   Registre la directiva invocando el `DocumentSecurityServiceClient` método del `registerPolicy` objeto y pasando los siguientes valores:

   * El `PolicySpec` objeto que representa la directiva que se va a registrar.
   * Un valor de cadena que representa el conjunto de directivas al que pertenece la directiva. Puede especificar un `null` valor que tenga como resultado que la directiva se agregue al conjunto de directivas *MyPolices* .
   Si utiliza una cuenta de administrador de formularios AEM en la configuración de conexión para crear el `DocumentSecurityClient` objeto, especifique el nombre del conjunto de políticas al invocar el `registerPolicy` método.

   Si utiliza un usuario de Document SecurityDocument Security en los ajustes de conexión, puede invocar el `registerPolicy` método de sobrecarga que acepta únicamente la directiva. Es decir, no es necesario especificar el nombre del conjunto de directivas. Sin embargo, la política se agrega al conjunto de directivas denominado *Mis políticas*. Si no desea agregar la nueva directiva a este conjunto de directivas, especifique un nombre de conjunto de directivas cuando invoque el `registerPolicy` método.

   >[!NOTE]
   >
   >Al crear una directiva y especificar un conjunto de directivas, asegúrese de especificar un conjunto de directivas existente. Si especifica un conjunto de directivas que no existe, se genera una excepción.

Para ver ejemplos de código que utilizan el servicio Document Security, consulte los siguientes Quick Starts:

* &quot;Inicio rápido (MTOM): Creación de una directiva mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Creación de una directiva mediante la API de servicio web&quot;

## Modificación de políticas {#modifying-policies}

Puede modificar una directiva existente mediante la API de Java o el servicio Web de Document Security. Para realizar cambios en una directiva existente, debe recuperarla, modificarla y, a continuación, actualizar la directiva en el servidor. Por ejemplo, supongamos que recupera una directiva existente y amplía su período de validez. Antes de que el cambio surta efecto, debe actualizar la directiva.

Puede modificar una política cuando cambien los requisitos comerciales y ésta ya no refleje dichos requisitos. En lugar de crear una nueva directiva, simplemente puede actualizar una existente.

Para modificar los atributos de directiva mediante un servicio Web (por ejemplo, mediante el uso de clases proxy de Java que se crearon con JAX-WS), debe asegurarse de que la directiva está registrada en el servicio Document Security. A continuación, puede hacer referencia a la directiva existente mediante el `PolicySpec.getPolicyXml` método y modificar los atributos de la política mediante los métodos aplicables. Por ejemplo, puede modificar el período de concesión sin conexión invocando el `PolicySpec.setOfflineLeasePeriod` método .

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para modificar una directiva existente, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto API de cliente de Document Security.
1. Recuperar una directiva existente.
1. Cambiar atributos de directivas.
1. Actualice la directiva.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Document Security Client**

Antes de realizar una operación de servicio Document Security mediante programación, debe crear un objeto cliente de servicio Document Security. Si utiliza la API de Java, cree un `RightsManagementClient` objeto. Si utiliza la API de servicio web de Document Security, cree un `RightsManagementServiceService` objeto.

**Recuperar una directiva existente**

Debe recuperar una directiva existente para modificarla. Para recuperar una directiva, especifique el nombre de la directiva y el conjunto de directivas al que pertenece la directiva. Si especifica un `null` valor para el nombre del conjunto de directivas, la directiva se recupera del conjunto de directivas *Mis directivas* .

**Definir los atributos de la política**

Para modificar una política, se modifica el valor de los atributos de la política. El único atributo de directiva que no se puede cambiar es el atributo name. Por ejemplo, para cambiar el período de concesión sin conexión de la política, puede modificar el valor del atributo de período de concesión sin conexión de la política.

Al modificar el período de concesión sin conexión de una política mediante un servicio Web, se ignora el `offlineLeasePeriod` campo de la `PolicySpec` interfaz. Para actualizar el período de concesión sin conexión, modifique el `OfflineLeasePeriod` elemento en el documento XML de PDRL. A continuación, haga referencia al documento XML de PDRL actualizado utilizando el miembro de `PolicySpec` datos de la interfaz `policyXML` .

>[!NOTE]
>
>Para obtener información sobre otros atributos que puede definir, consulte la descripción de la `Policy` interfaz en la Referencia [de API de formularios](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM.

**Actualizar la directiva**

Antes de que los cambios que realice en una política se vean afectados, debe actualizar la directiva con el servicio Document Security. Los cambios en las directivas que protegen documentos se actualizan la próxima vez que el documento protegido por una política se sincroniza con el servicio de Document Security.

### Modificación de directivas existentes mediante la API de Java {#modify-existing-policies-using-the-java-api}

Modifique una directiva existente mediante la API de Document Security (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `RightsManagementClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recuperar una directiva existente.

   * Cree un `PolicyManager` objeto invocando el `RightsManagementClient` método `getPolicyManager` del objeto.
   * Cree un `Policy` objeto que represente la directiva que se va a actualizar invocando el `PolicyManager` método `getPolicy` del objeto y pasando los siguientes valores&quot;

      * Un valor de cadena que representa el nombre del conjunto de políticas al que pertenece la directiva. Puede especificar `null` que el resultado sea el conjunto de `MyPolicies` directivas que se está utilizando.
      * Un valor de cadena que representa el nombre de la política.

1. Defina los atributos de la política.

   Cambie los atributos de la directiva para cumplir los requisitos comerciales. Por ejemplo, para cambiar el período de concesión sin conexión de la política, invoque el `Policy` método del `setOfflineLeasePeriod` objeto.

1. Actualice la directiva.

   Actualice la directiva invocando `PolicyManager` el `updatePolicy` método del objeto. Pase el `Policy` objeto que representa la directiva que se va a actualizar.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte Inicio rápido (modo SOAP): Modificación de una directiva mediante la sección API de Java.

### Modificación de directivas existentes mediante la API de servicio Web {#modify-existing-policies-using-the-web-service-api}

Modifique una directiva existente mediante la API de Document Security (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `RightsManagementServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `RightsManagementServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `RightsManagementServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperar una directiva existente.

   Cree un `PolicySpec` objeto que represente la política que se va a modificar invocando el método del `RightsManagementServiceClient` `getPolicy` objeto y pasando los siguientes valores:

   * Un valor de cadena que especifica el nombre del conjunto de políticas al que pertenece la directiva. Puede especificar `null` que el resultado sea el conjunto de `MyPolicies` directivas que se está utilizando.
   * Un valor de cadena que especifica el nombre de la directiva.

1. Defina los atributos de la política.

   Cambie los atributos de la directiva para cumplir los requisitos comerciales.

1. Actualice la directiva.

   Actualice la directiva invocando el `RightsManagementServiceClient` método `updatePolicyFromSDK` del objeto y pasando el `PolicySpec` objeto que representa la directiva que se va a actualizar.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte los siguientes Quick Starts:

* &quot;Inicio rápido (MTOM): Modificación de una directiva mediante la API de servicio Web&quot;
* &quot;Inicio rápido (SwaRef): Modificación de una directiva mediante la API de servicio Web&quot;

## Eliminación de directivas {#deleting-policies}

Puede eliminar una directiva existente mediante la API de Java o el servicio Web de Document Security. Después de eliminar una directiva, ya no se puede usar para proteger documentos. Sin embargo, los documentos existentes protegidos por políticas que utilizan la política siguen estando protegidos. Puede eliminar una directiva cuando haya una más reciente disponible.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para eliminar una directiva existente, realice los siguientes pasos:

1. Incluir archivos de proyecto
1. Cree un objeto API de cliente de Document Security.
1. Elimine la directiva.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Document Security Client**

Para poder realizar una operación de servicio de Document Security mediante programación, debe crear un objeto cliente de servicio de Document Security. Si utiliza la API de Java, cree un `RightsManagementClient` objeto. Si utiliza la API de servicio web de Document Security, cree un `RightsManagementServiceService` objeto.

**Eliminar la directiva**

Para eliminar una directiva, especifique la directiva que desea eliminar y el conjunto de directivas al que pertenece la directiva. El usuario cuya configuración se utiliza para invocar AEM Forms debe tener permiso para eliminar la directiva; de lo contrario, se produce una excepción. Del mismo modo, si intenta eliminar una directiva que no existe, se producirá una excepción.

### Eliminar directivas mediante la API de Java {#delete-policies-using-the-java-api}

Elimine una directiva mediante la API de Document Security (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `RightsManagementClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Elimine la directiva.

   * Cree un `PolicyManager` objeto invocando el `RightsManagementClient` método `getPolicyManager` del objeto.
   * Para eliminar la directiva, invoque el `PolicyManager` método del `deletePolicy` objeto y pase los valores siguientes:

      * Un valor de cadena que especifica el nombre del conjunto de políticas al que pertenece la directiva. Puede especificar `null` que el resultado sea el conjunto de `MyPolicies` directivas que se está utilizando.
      * Un valor de cadena que especifica el nombre de la directiva que se va a eliminar.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte los siguientes Quick Starts:

* &quot;Inicio rápido (modo SOAP): Eliminación de una directiva mediante la API de Java&quot;

### Eliminar directivas mediante la API de servicio Web {#delete-policies-using-the-web-service-api}

Elimine una directiva mediante la API de Document Security (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `RightsManagementServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `RightsManagementServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `RightsManagementServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Elimine la directiva.

   Para eliminar una política, invoque el `RightsManagementServiceClient` método del `deletePolicy` objeto y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del conjunto de políticas al que pertenece la directiva. Puede especificar `null` que el resultado sea el conjunto de `MyPolicies` directivas que se está utilizando.
   * Un valor de cadena que especifica el nombre de la directiva que se va a eliminar.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte los siguientes Quick Starts:

* &quot;Inicio rápido (MTOM): Eliminación de una directiva mediante la API de servicio Web&quot;
* &quot;Inicio rápido (SwaRef): Eliminación de una directiva mediante la API de servicio Web&quot;

## Aplicación de políticas a documentos PDF {#applying-policies-to-pdf-documents}

Puede aplicar una política a un documento PDF para protegerlo. Al aplicar una política a un documento PDF, se restringe el acceso al documento. No puede aplicar una política a un documento si el documento ya está protegido con una política.

Mientras el documento está abierto, también puede restringir el acceso a las funciones de Acrobat y Adobe Reader, incluida la capacidad de imprimir y copiar texto, realizar cambios y agregar firmas y comentarios a un documento. Además, puede revocar un documento PDF protegido por una política cuando ya no desee que los usuarios tengan acceso al documento.

Puede supervisar el uso de un documento protegido por una política después de distribuirlo. Es decir, puede ver cómo se utiliza el documento y quién lo utiliza. Por ejemplo, puede averiguar cuándo alguien ha abierto el documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-3}

Para aplicar una política a un documento PDF, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto API de cliente de Document Security.
1. Recupere un documento PDF al que se aplique una política.
1. Aplicar una directiva existente al documento PDF.
1. Guarde el documento PDF protegido por una política.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Crear un objeto API de cliente de Document Security**

Antes de realizar una operación de servicio de Document Security mediante programación, cree un objeto cliente de servicio de Document Security. Si utiliza la API de Java, cree un `DocumentSecurityClient` objeto. Si utiliza la API de servicio web de Document Security, cree un `DocumentSecurityServiceService` objeto.

**Recuperar un documento PDF**

Puede recuperar un documento PDF para aplicar una política. Después de aplicar una política al documento PDF, los usuarios quedan restringidos al usar el documento. Por ejemplo, si la política no permite que el documento se abra sin conexión, los usuarios deben estar en línea para abrirlo.

**Aplicar una directiva existente al documento PDF**

Para aplicar una política a un documento PDF, haga referencia a una política existente y especifique a qué conjunto de políticas pertenece la política. El usuario que está configurando las propiedades de conexión debe tener acceso a la directiva especificada. De lo contrario, se produce una excepción.

**Guardar el documento PDF**

Una vez que el servicio Document Security haya aplicado una política a un documento PDF, puede guardar el documento PDF protegido por una política como archivo PDF.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revocación del acceso a los documentos](protecting-documents-policies.md#revoking-access-to-documents)

### Aplicar una política a un documento PDF mediante la API de Java {#apply-a-policy-to-a-pdf-document-using-the-java-api}

Aplicar una política a un documento PDF mediante la API de Document Security (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `RightsManagementClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recupere un documento PDF.

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF utilizando su constructor. Pase un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Aplicar una directiva existente al documento PDF.

   * Cree un `DocumentManager` objeto invocando el `RightsManagementClient` método `getDocumentManager` del objeto.
   * Para aplicar una política al documento PDF, invoque el `DocumentManager` método del `protectDocument` objeto y pase los valores siguientes:

      * El `com.adobe.idp.Document` objeto que contiene el documento PDF al que se aplica la política.
      * Un valor de cadena que especifica el nombre del documento.
      * Un valor de cadena que especifica el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar un `null` valor que resulte en el uso del conjunto de `MyPolicies` directivas.
      * Un valor de cadena que especifica el nombre de la directiva.
      * Un valor de cadena que representa el nombre del dominio del administrador de usuarios del usuario que es el editor del documento. Este valor de parámetro es opcional y puede ser nulo (si este parámetro es nulo, el siguiente valor de parámetro debe ser nulo).
      * Un valor de cadena que representa el nombre canónico del usuario del administrador de usuarios que es el editor del documento. Este valor de parámetro es opcional y puede ser `null` (si este parámetro es nulo, el valor del parámetro anterior debe ser `null`).
      * Una `com.adobe.livecycle.rightsmanagement.Locale` que representa la configuración regional que se utiliza para seleccionar la plantilla de MS Office. Este valor de parámetro es opcional y no se utiliza para documentos PDF. Para proteger un documento PDF, especifique `null`.
      El `protectDocument` método devuelve un `RMSecureDocumentResult` objeto que contiene el documento PDF protegido por una política.


1. Guarde el documento PDF.

   * Invoque el `RMSecureDocumentResult` método del `getProtectedDoc` objeto para obtener el documento PDF protegido por una política. Este método devuelve un `com.adobe.idp.Document` objeto.
   * Cree un `java.io.File` objeto y asegúrese de que la extensión del archivo es PDF.
   * Invoque el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `Document` objeto en el archivo (asegúrese de utilizar el `Document` objeto devuelto por el `getProtectedDoc` método).

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte los siguientes Quick Starts:

* &quot;Inicio rápido (modo EJB): Aplicación de una política a un documento PDF mediante la API de Java&quot;
* &quot;Inicio rápido (modo SOAP): Aplicación de una política a un documento PDF mediante la API de Java&quot;

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aplicar una política a un documento PDF mediante la API de servicio Web {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

Aplicar una política a un documento PDF mediante la API de Document Security (servicio Web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `RightsManagementServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `RightsManagementServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `RightsManagementServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere un documento PDF.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento PDF al que se aplica una política.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Aplicar una directiva existente al documento PDF.

   Para aplicar una política al documento PDF, invoque el `RightsManagementServiceClient` método del `protectDocument` objeto y pase los valores siguientes:

   * El `BLOB` objeto que contiene el documento PDF al que se aplica la política.
   * Un valor de cadena que especifica el nombre del documento.
   * Un valor de cadena que especifica el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar un `null` valor que resulte en el uso del conjunto de `MyPolicies` directivas.
   * Un valor de cadena que especifica el nombre de la directiva.
   * Un valor de cadena que representa el nombre del dominio del administrador de usuarios del usuario que es el editor del documento. Este valor de parámetro es opcional y puede ser nulo (si este parámetro es nulo, el siguiente valor de parámetro debe ser `null`).
   * Un valor de cadena que representa el nombre canónico del usuario del administrador de usuarios que es el editor del documento. Este valor de parámetro es opcional y puede ser nulo (si este parámetro es nulo, el valor del parámetro anterior debe ser `null`).
   * Un `RMLocale` valor que especifica el valor de configuración regional (por ejemplo, `RMLocale.en`).
   * Parámetro de salida de cadena que se utiliza para almacenar el valor del identificador de directiva.
   * Parámetro de salida de cadena que se utiliza para almacenar el valor de identificador protegido por una política.
   * Parámetro de salida de cadena que se utiliza para almacenar el tipo MIME (por ejemplo, `application/pdf`).
   El `protectDocument` método devuelve un `BLOB` objeto que contiene el documento PDF protegido por una política.

1. Guarde el documento PDF.

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF protegido por una política.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `protectDocument` método. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte los siguientes Quick Starts:

* &quot;Inicio rápido (MTOM): Aplicación de una política a un documento PDF mediante la API de servicio Web&quot;
* &quot;Inicio rápido (SwaRef): Aplicación de una política a un documento PDF mediante la API de servicio Web&quot;

## Eliminación de directivas de documentos PDF {#removing-policies-from-pdf-documents}

Puede quitar una política de un documento protegido por una política para quitar la seguridad del documento. Es decir, si ya no desea que el documento esté protegido por una política. Si desea actualizar un documento protegido por una política con una política más reciente, en lugar de eliminar la política y agregar la política actualizada, es más eficaz cambiar la política.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-4}

Para quitar una política de un documento PDF protegido por una política, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto
1. Cree un objeto API de cliente de Document Security.
1. Recupere un documento PDF protegido por una política.
1. Elimine la directiva del documento PDF.
1. Guarde el documento PDF no seguro.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Document Security Client**

Antes de realizar una operación de servicio de Document Security mediante programación, cree un objeto cliente de servicio de Document Security.

**Recuperar un documento PDF protegido por una política**

Puede recuperar un documento PDF protegido por una política para eliminar una política. Si intenta eliminar una política de un documento PDF que no esté protegido por una política, provocará una excepción.

**Quitar la directiva del documento PDF**

Puede quitar una política de un documento PDF protegido por una política siempre que se especifique un administrador en la configuración de conexión. Si no es así, la política utilizada para proteger un documento debe contener el `SWITCH_POLICY` permiso para eliminar una política de un documento PDF. Además, el usuario especificado en la configuración de conexión de AEM Forms también debe tener ese permiso. De lo contrario, se genera una excepción.

**Guardar el documento PDF no seguro**

Una vez que el servicio de Document Security haya eliminado una política de un documento PDF, puede guardar el documento PDF no seguro como archivo PDF.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicación de políticas a documentos PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Eliminar una política de un documento PDF mediante la API de Java {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Elimine una política de un documento PDF protegido por una política mediante la API de Document Security (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `DocumentSecurityClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recupere un documento PDF protegido por una política.

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF protegido por una política utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Elimine la directiva del documento PDF.

   * Cree un `DocumentManager` objeto invocando el `DocumentSecurityClient` método `getDocumentManager` del objeto.
   * Elimine una política del documento PDF invocando el `DocumentManager` método del `removeSecurity` objeto y pasando el `com.adobe.idp.Document` objeto que contiene el documento PDF protegido por una política. Este método devuelve un `com.adobe.idp.Document` objeto que contiene un documento PDF no seguro.

1. Guarde el documento PDF no seguro.

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del archivo es PDF.
   * Invoque el `Document` método del `copyToFile` objeto para copiar el contenido del `Document` objeto en el archivo (asegúrese de utilizar el `Document` objeto devuelto por el `removeSecurity` método).

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte los siguientes Quick Starts:

* &quot;Inicio rápido (modo SOAP): Eliminación de una política de un documento PDF mediante la API de Java&quot;

### Eliminar una directiva mediante la API de servicio Web {#remove-a-policy-using-the-web-service-api}

Elimine una política de un documento PDF protegido por una política mediante la API de Document Security (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `DocumentSecurityServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `DocumentSecurityServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `DocumentSecurityServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere un documento PDF protegido por una política.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el documento PDF protegido por una política del que se ha eliminado la política.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Elimine la directiva del documento PDF.

   Elimine la política del documento PDF invocando el `DocumentSecurityServiceClient` método del `removePolicySecurity` objeto y pasando el `BLOB` objeto que contiene el documento PDF protegido por una política. Este método devuelve un `BLOB` objeto que contiene un documento PDF no seguro.

1. Guarde el documento PDF no seguro.

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF no protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `removePolicySecurity` método. Rellene la matriz de bytes obteniendo el valor del `BLOB` campo del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte los siguientes Quick Starts:

* &quot;Inicio rápido (MTOM): Eliminación de una política de un documento PDF mediante la API de servicio Web&quot;
* &quot;Inicio rápido (SwaRef): Eliminación de una política de un documento PDF mediante la API de servicio Web&quot;

**Consulte también**

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Revocación del acceso a los documentos {#revoking-access-to-documents}

Puede revocar el acceso a un documento PDF protegido por una política, lo que resulta en que los usuarios no tengan acceso a todas las copias del documento. Cuando un usuario intenta abrir un documento PDF revocado, se le redirige a una dirección URL especificada donde se puede ver un documento revisado. La dirección URL a la que se redirige al usuario debe especificarse mediante programación. Cuando se anula el acceso a un documento, el cambio surte efecto la próxima vez que el usuario se sincronice con el servicio de Document Security abriendo el documento protegido por una política en línea.

La posibilidad de revocar el acceso a un documento proporciona seguridad adicional. Por ejemplo, supongamos que una versión más reciente de un documento está disponible y que ya no desea que nadie vea la versión obsoleta. En este caso, se puede revocar el acceso al documento anterior y nadie puede verlo a menos que se restablezca el acceso.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-5}

Para revocar un documento protegido por una política, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto API de cliente de Document Security.
1. Recupere un documento PDF protegido por una política.
1. Revocar el documento protegido por una política.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Document Security Client**

Para poder realizar una operación de servicio de Document Security mediante programación, debe crear un objeto cliente de servicio de Document Security.

**Recuperar un documento PDF protegido por una política**

Debe recuperar un documento PDF protegido por una política para revocarlo. No puede revocar un documento que ya se ha revocado o que no está protegido por una política.

Si conoce el valor del identificador de licencia del documento protegido por una política, no es necesario recuperar el documento PDF protegido por una política. Sin embargo, en la mayoría de los casos, deberá recuperar el documento PDF para obtener el valor del identificador de licencia.

**Revocar el documento protegido por una política**

Para revocar un documento protegido por una política, especifique el identificador de licencia del documento protegido por una política. Además, puede especificar la dirección URL de un documento que el usuario puede ver al intentar abrir el documento revocado. Es decir, supongamos que se revoca un documento obsoleto. Cuando un usuario intenta abrir el documento revocado, verá un documento actualizado en lugar del documento revocado.

>[!NOTE]
>
>Si intenta revocar un documento que ya está revocado, se genera una excepción.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicación de políticas a documentos PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Restablecimiento del acceso a documentos revocados](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Revocar el acceso a los documentos mediante la API de Java {#revoke-access-to-documents-using-the-java-api}

Revocar el acceso a un documento PDF protegido por una política mediante la API de Document Security (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Document Security Client

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `DocumentSecurityClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recuperar un documento PDF protegido por una política

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF protegido por una política utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Revocar el documento protegido por una política

   * Cree un `DocumentManager` objeto invocando el `DocumentSecurityClient` método `getDocumentManager` del objeto.
   * Recupere el valor del identificador de licencia del documento protegido por una política invocando el `DocumentManager` método del `getLicenseId` objeto. Pase el `com.adobe.idp.Document` objeto que representa el documento protegido por una política. Este método devuelve un valor de cadena que representa el valor del identificador de licencia.
   * Cree un `LicenseManager` objeto invocando el `DocumentSecurityClient` método `getLicenseManager` del objeto.
   * Para anular el documento protegido por una política, invoque el `LicenseManager` método del `revokeLicense` objeto y pase los valores siguientes:

      * Un valor de cadena que especifica el valor del identificador de licencia del documento protegido por una política (especifique el valor devuelto del `DocumentManager` método del `getLicenseId` objeto).
      * Miembro de datos estático de la `License` interfaz que especifica el motivo para revocar el documento. Por ejemplo, puede especificar `License.DOCUMENT_REVISED`.
      * Un `java.net.URL` valor que especifica la ubicación en la que se encuentra un documento revisado. Si no desea redirigir a un usuario a otra dirección URL, puede pasar `null`.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte los siguientes Quick Starts:

* &quot;Inicio rápido (modo SOAP): Revocación de un documento mediante la API de Java&quot;

### Revocar el acceso a los documentos mediante la API de servicio web {#revoke-access-to-documents-using-the-web-service-api}

Revocar el acceso a un documento PDF protegido por una política mediante la API de Document Security (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Creación de un objeto de API de Document Security Client

   * Cree un `DocumentSecurityServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `DocumentSecurityServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `DocumentSecurityServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperar un documento PDF protegido por una política

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento PDF protegido por una política que se ha revocado.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento PDF protegido por una política que se va a revocar y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Revocar el documento protegido por una política

   * Recupere el valor del identificador de licencia del documento protegido por una política invocando el `DocumentSecurityServiceClient` método `getLicenseID` del objeto y pasando el `BLOB` objeto que representa el documento protegido por una política. Este método devuelve un valor de cadena que representa el identificador de licencia.
   * Para anular el documento protegido por una política, invoque el `DocumentSecurityServiceClient` método del `revokeLicense` objeto y pase los valores siguientes:

      * Un valor de cadena que especifica el valor del identificador de licencia del documento protegido por una política (especifique el valor devuelto del `DocumentSecurityServiceService` método del `getLicenseId` objeto).
      * Un miembro de datos estático de la enumeración que especifica el motivo para revocar el documento. `Reason` Por ejemplo, puede especificar `Reason.DOCUMENT_REVISED`.
      * Un `string` valor que especifica la ubicación URL en la que se encuentra un documento revisado. Si no desea redirigir a un usuario a otra dirección URL, puede pasar `null`.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte los siguientes Quick Starts:

* &quot;Inicio rápido (MTOM): Revocación de un documento mediante la API de servicio Web&quot;
* &quot;Inicio rápido (SwaRef): Revocación de un documento mediante la API de servicio Web&quot;

**Consulte también**

[Eliminación de directivas de documentos de Word](protecting-documents-policies.md#removing-policies-from-word-documents)

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Restablecimiento del acceso a documentos revocados {#reinstating-access-to-revoked-documents}

Puede restablecer el acceso a un documento PDF revocado, lo que permite que todos los usuarios tengan acceso a todas las copias del documento revocado. Cuando un usuario abre un documento restablecido que fue revocado, puede ver el documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-6}

Para restablecer el acceso a un documento PDF revocado, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto API de cliente de Document Security.
1. Recupere el identificador de licencia del documento PDF revocado.
1. Restablece el acceso al documento PDF revocado.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Document Security Client**

Para poder realizar una operación de servicio de Document Security mediante programación, debe crear un objeto cliente de servicio de Document Security. Si utiliza la API de Java, cree un `DocumentSecurityClient` objeto. Si utiliza la API de servicio web de Document Security, cree un `DocumentSecurityServiceService` objeto.

**Recuperar el identificador de licencia del documento PDF revocado**

Debe recuperar el identificador de licencia del documento PDF revocado para poder restablecer un documento PDF revocado. Después de obtener el valor del identificador de licencia, puede restablecer un documento revocado. Si intenta restablecer un documento que no está revocado, provocará una excepción.

**Restablecer el acceso al documento PDF revocado**

Para restablecer el acceso a un documento PDF revocado, debe especificar el identificador de licencia del documento revocado. Si intenta restablecer el acceso a un documento PDF que no está revocado, provocará una excepción.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicación de políticas a documentos PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Revocación del acceso a los documentos](protecting-documents-policies.md#revoking-access-to-documents)

### Restablecimiento del acceso a documentos revocados mediante la API de Java {#reinstate-access-to-revoked-documents-using-the-java-api}

Restablecer el acceso a un documento revocado mediante la API de Document Security (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `DocumentSecurityClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recupere el identificador de licencia del documento PDF revocado.

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF revocado utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.
   * Cree un `DocumentManager` objeto invocando el `DocumentSecurityClient` método `getDocumentManager` del objeto.
   * Recupere el valor del identificador de licencia del documento revocado invocando el `DocumentManager` método `getLicenseId` del objeto y pasando el `com.adobe.idp.Document` objeto que representa el documento revocado. Este método devuelve un valor de cadena que representa el identificador de licencia.

1. Restablece el acceso al documento PDF revocado.

   * Cree un `LicenseManager` objeto invocando el `DocumentSecurityClient` método `getLicenseManager` del objeto.
   * Restablezca el acceso al documento PDF revocado invocando el `LicenseManager` método del `unrevokeLicense` objeto y pasando el valor del identificador de licencia del documento revocado.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte los siguientes Quick Starts:

* &quot;Inicio rápido (modo SOAP): Restablecimiento del acceso a un documento revocado mediante la API de servicio web&quot;

### Restablecimiento del acceso a documentos revocados mediante la API de servicio web {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Restablecer el acceso a un documento revocado mediante la API de Document Security (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `DocumentSecurityServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `DocumentSecurityServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `DocumentSecurityServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere el identificador de licencia del documento PDF revocado.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento PDF revocado al que se restablece el acceso.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento PDF revocado y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Restablece el acceso al documento PDF revocado.

   * Recupere el valor del identificador de licencia del documento revocado invocando el `DocumentSecurityServiceClient` método `getLicenseID` del objeto y pasando el `BLOB` objeto que representa el documento revocado. Este método devuelve un valor de cadena que representa el identificador de licencia.
   * Restablezca el acceso al documento PDF revocado invocando el `DocumentSecurityServiceClient` método `unrevokeLicense` del objeto y pasando un valor de cadena que especifica el valor del identificador de licencia del documento PDF revocado (pase el valor devuelto del `DocumentSecurityServiceClient` método `getLicenseId` del objeto).

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte los siguientes Quick Starts:

* &quot;Inicio rápido (MTOM): Restablecimiento del acceso a un documento revocado mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Restablecimiento del acceso a un documento revocado mediante la API de servicio web&quot;

**Consulte también**

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Inspección de documentos PDF protegidos por políticas {#inspecting-policy-protected-pdf-documents}

Puede utilizar la API de Document Security Service (Java y servicio Web) para inspeccionar documentos PDF protegidos por políticas. La inspección de documentos PDF protegidos por políticas devuelve información sobre el documento PDF protegido por políticas. Por ejemplo, puede determinar la política que se utilizó para proteger el documento y la fecha en que se protegió el documento.

No puede realizar esta tarea si la versión de LiveCycle es 8.x o una versión anterior. En AEM Forms se ha añadido la compatibilidad con la inspección de documentos protegidos por políticas. Si intenta inspeccionar un documento protegido por una política con LiveCycle 8.x (o anterior), se genera una excepción.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-7}

Para inspeccionar un documento PDF protegido por una política, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto API de cliente de Document Security.
1. Recupere un documento protegido por una política para inspeccionar.
1. Obtenga información sobre el documento protegido por una política.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Document Security Client**

Antes de realizar una operación de servicio de Document Security mediante programación, cree un objeto cliente de servicio de Document Security. Si utiliza la API de Java, cree un `RightsManagementClient` objeto. Si utiliza la API de servicio web de Document Security, cree un `RightsManagementServiceService` objeto.

**Recuperar un documento protegido por una política para inspeccionar**

Para inspeccionar un documento protegido por una política, recuperarlo. Si intenta inspeccionar un documento que no está protegido con una política o que está revocado, se genera una excepción.

**Inspeccionar el documento**

Después de recuperar un documento protegido por una política, puede inspeccionarlo.

**Obtener información sobre el documento protegido por una política**

Después de inspeccionar un documento PDF protegido por una política, puede obtener información al respecto. Por ejemplo, puede determinar la política que se utiliza para proteger el documento.

Si protege un documento con una política que pertenece a Mis políticas y, a continuación, llama `RMInspectResult.getPolicysetName` o `RMInspectResult.getPolicysetId`, devuelve null.

Si el documento está protegido mediante una política incluida en un conjunto de políticas (que no sea Mis políticas), `RMInspectResult.getPolicysetName` y `RMInspectResult.getPolicysetId` devuelve cadenas válidas.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Inspeccionar documentos PDF protegidos por políticas mediante la API de Java {#inspect-policy-protected-pdf-documents-using-the-java-api}

Inspeccione un documento PDF protegido por una política mediante la API de Document Security Service (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clases del proyecto Java. Para obtener información sobre la ubicación de estos archivos, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión. (Consulte [Configuración de propiedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexión).
   * Cree un `RightsManagementClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recupere un documento protegido por una política para inspeccionar.

   * Cree un `java.io.FileInputStream` objeto que represente el documento PDF protegido por una política utilizando su constructor. Pase un valor de cadena que especifique la ubicación del documento PDF.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Inspeccione el documento.

   * Cree un `DocumentManager` objeto invocando el `RightsManagementClient` método `getDocumentManager` del objeto.
   * Inspeccione el documento protegido por una política invocando el `LicenseManager` método `inspectDocument` del objeto. Pase el `com.adobe.idp.Document` objeto que contiene el documento PDF protegido por una política. Este método devuelve un `RMInspectResult` objeto que contiene información sobre el documento protegido por una política.

1. Obtenga información sobre el documento protegido por una política.

   Para obtener información sobre el documento protegido por una política, invoque el método adecuado que pertenece al `RMInspectResult` objeto. Por ejemplo, para recuperar el nombre de la directiva, invoque el `RMInspectResult` método del `getPolicyName` objeto.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte los siguientes Quick Starts:

* &quot;Inicio rápido (modo SOAP): Inspección de documentos PDF protegidos por políticas mediante la API de Java&quot;

### Inspeccionar documentos PDF protegidos por políticas mediante la API de servicio web {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Inspeccione un documento PDF protegido por una política mediante la API del servicio de Document Security (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `RightsManagementServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `RightsManagementServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `RightsManagementServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere un documento protegido por una política para inspeccionar.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento PDF que inspeccionar.
   * Cree un `System.IO.FileStream` objeto invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento PDF y el modo en el que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Inspeccione el documento.

   Inspeccione el documento protegido por una política invocando el `RightsManagementServiceClient` método `inspectDocument` del objeto. Pase el `BLOB` objeto que contiene el documento PDF protegido por una política. Este método devuelve un `RMInspectResult` objeto que contiene información sobre el documento protegido por una política.

1. Obtenga información sobre el documento protegido por una política.

   Para obtener información sobre el documento protegido por una política, obtenga el valor del campo correspondiente que pertenece al `RMInspectResult` objeto. Por ejemplo, para recuperar el nombre de la política, obtenga el valor del `RMInspectResult` campo del `policyName` objeto.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte los siguientes Quick Starts:

* &quot;Inicio rápido (MTOM): Inspección de documentos PDF protegidos por políticas mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Inspección de documentos PDF protegidos por políticas mediante la API de servicio web&quot;

**Consulte también**

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Creación de marcas de agua {#creating-watermarks}

Las marcas de agua ayudan a garantizar la seguridad de un documento al identificar exclusivamente el documento y controlar la infracción de los derechos de autor. Por ejemplo, puede crear y colocar una marca de agua que indique Confidencial en todas las páginas de un documento. Después de crear una marca de agua, puede incluirla como parte de una política. Es decir, puede establecer el atributo de marca de agua de la política con la marca de agua recién creada. Después de aplicar una política que contiene una marca de agua a un documento, la marca de agua aparece en el documento protegido por una política.

>[!NOTE]
>
>Solo los usuarios con privilegios administrativos de Document Security pueden crear marcas de agua. Es decir, debe especificar dicho usuario al definir la configuración de conexión necesaria para crear un objeto cliente del servicio Document Security.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-8}

Para crear una marca de agua, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto API de cliente de Document Security.
1. Defina los atributos de las marcas de agua.
1. Registre la marca de agua en el servicio de Document Security.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Document Security Client**

Para poder realizar una operación de servicio de Document Security mediante programación, debe crear un objeto cliente de servicio de Document Security. Si utiliza la API de Java, cree un `RightsManagementClient` objeto. Si utiliza la API de servicio web de Document Security, cree un `RightsManagementServiceService` objeto.

**Definir los atributos de las marcas de agua**

Para crear una nueva marca de agua, debe definir atributos de marca de agua. Siempre se debe definir el atributo name. Además del atributo name, debe establecer al menos uno de los atributos siguientes:

* Texto personalizado
* FechaIncluida
* UserIdIncluded
* UserNameIncluded

En la tabla siguiente se muestran los pares de clave y valor que son necesarios para crear una marca de agua mediante servicios Web.

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
   <td><p>Si este valor es true, se debe especificar el valor del texto personalizado mediante <code>WaterBackCmd:SRCTEXT</code>.</p></td>
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
   <td><p>Si se especifica este valor, <code>WaterBackCmd:IS_SIZE_ENABLED</code> debe estar presente y el valor debe ser true. Si no se especifica este atributo, el comportamiento predeterminado se ajusta a la página.</p></td>
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
   <td><p>Especifica si la marca de agua es un fondo. El valor predeterminado es false.</p></td>
   <td><p>True o false</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>True si se especifica una escala personalizada. Si este valor es true, también se debe especificar SCALE. Si este valor es false, el valor predeterminado se ajusta a la página.</p></td>
   <td><p>True o false</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>Especifica el texto personalizado para una marca de agua. Si este valor está presente, también <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> debe estar presente y definido como verdadero.</p></td>
   <td><p>True o false</p></td>
  </tr>
 </tbody>
</table>

Todas las marcas de agua deben tener uno de los atributos siguientes definidos:

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

Todos los demás atributos son opcionales.

**Registro de la marca de agua**

Una nueva marca de agua debe registrarse en el servicio de Document Security para poder utilizarse. Después de registrar una marca de agua, puede utilizarla dentro de políticas.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicación de políticas a documentos PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Creación de marcas de agua mediante la API de Java {#create-watermarks-using-the-java-api}

Cree una marca de agua mediante la API de Document Security (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como el `adobe-rightsmanagement-client.jar`, en la ruta de clases del proyecto Java.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `RightsManagementClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Definir los atributos de marca de agua

   * Cree un `Watermark` objeto invocando el `InfomodelObjectFactory` método estático `createWatermark` del objeto. Este método devuelve un `Watermark` objeto.
   * Establezca el atributo name de la marca de agua invocando el `Watermark` método del `setName` objeto y pasando un valor de cadena que especifica el nombre de la política.
   * Establezca el atributo de fondo de la marca de agua invocando el `Watermark` método `setBackground` del objeto y pasando `true`. Al configurar este atributo, la marca de agua aparece en el fondo del documento.
   * Establezca el atributo de texto personalizado de la marca de agua invocando el `Watermark` método `setCustomText` del objeto y pasando un valor de cadena que represente el texto de la marca de agua.
   * Establezca el atributo de opacidad de la marca de agua invocando el `Watermark` método `setOpacity` del objeto y pasando un valor entero que especifica el nivel de opacidad. Un valor de 100 indica que la marca de agua es completamente opaca y un valor de 0 indica que la marca de agua es completamente transparente.

1. Registre la marca de agua.

   * Cree un `WatermarkManager` objeto invocando el `RightsManagementClient` método `getWatermarkManager` del objeto. Este método devuelve un `WatermarkManager` objeto.
   * Registre la marca de agua invocando el `WatermarkManager` método `registerWatermark` del objeto y pasando el `Watermark` objeto que representa la marca de agua que se va a registrar. Este método devuelve un valor de cadena que representa el valor de identificación de la marca de agua.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte los siguientes Quick Starts:

* &quot;Inicio rápido (modo SOAP): Creación de una marca de agua mediante la API de Java&quot;

### Creación de marcas de agua mediante la API de servicio web {#create-watermarks-using-the-web-service-api}

Cree una marca de agua mediante la API de Document Security (servicio web):

1. Cree un objeto API de cliente de Document Security.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `RightsManagementServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `RightsManagementServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `RightsManagementServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Defina los atributos de marca de agua.

   * Cree un `WatermarkSpec` objeto invocando el `WatermarkSpec` constructor.
   * Defina el nombre de la marca de agua asignando un valor de cadena al miembro de `WatermarkSpec` datos del `name` objeto.
   * Defina el atributo de la marca de agua `id` asignando un valor de cadena al miembro de `WatermarkSpec` datos del `id` objeto.
   * Para cada propiedad de marca de agua que se va a establecer, cree un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto independiente.
   * Establezca el valor clave asignando un valor al miembro de datos del `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto (por ejemplo, `key` `WaterBackCmd:OPACITY)`).
   * Establezca el valor asignando un valor al miembro de datos del `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto (por ejemplo, `value` `.25`).
   * Create a `MyArrayOf_xsd_anyType` object. Para cada `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto, invoque el `MyArrayOf_xsd_anyType` método `Add` del objeto. Pase el `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Asigne el `MyArrayOf_xsd_anyType` objeto al miembro de `WatermarkSpec` datos `values` del objeto.

1. Registre la marca de agua.

   Registre la marca de agua invocando el `RightsManagementServiceClient` método `registerWatermark` del objeto y pasando el `WatermarkSpec` objeto que representa la marca de agua que se va a registrar.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte los siguientes Quick Starts:

* &quot;Inicio rápido (MTOM): Creación de una marca de agua mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Creación de una marca de agua mediante la API de servicio web&quot;

**Consulte también**

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modificación de marcas de agua {#modifying-watermarks}

Puede modificar una marca de agua existente mediante la API Java de Document Security o la API de servicio Web. Para realizar cambios en una marca de agua existente, debe recuperarla, modificar sus atributos y, a continuación, actualizarla en el servidor. Por ejemplo, supongamos que recupera una marca de agua y modifica su atributo de opacidad. Antes de que el cambio surta efecto, debe actualizar la marca de agua.

Al modificar una marca de agua, el cambio afecta a los documentos futuros que tengan la marca de agua aplicada. Es decir, los documentos PDF existentes que contienen la marca de agua no se ven afectados.

>[!NOTE]
>
>Solo los usuarios con privilegios administrativos de Document Security pueden modificar las marcas de agua. Es decir, debe especificar dicho usuario al definir la configuración de conexión necesaria para crear un objeto cliente del servicio Document Security.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-9}

Para modificar una marca de agua, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto API de cliente de Document Security.
1. Recupere la marca de agua que desea modificar.
1. Defina los atributos de las marcas de agua.
1. Actualice la marca de agua.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Document Security Client**

Para poder realizar una operación de servicio de Document Security mediante programación, debe crear un objeto cliente de servicio de Document Security. Si utiliza la API de Java, cree un `DocumentSecurityClient` objeto. Si utiliza la API de servicio web de Document Security, cree un `DocumentSecurityServiceService` objeto.

**Recuperar la marca de agua para modificar**

Para modificar una marca de agua, debe recuperar una ya existente. Puede recuperar una marca de agua especificando su nombre o especificando su valor de identificador.

**Definir los atributos de las marcas de agua**

Para modificar una marca de agua existente, cambie el valor de uno o varios atributos de marca de agua. Al actualizar mediante programación una marca de agua mediante un servicio Web, debe definir todos los atributos que se establecieron originalmente, aunque el valor no cambie. Por ejemplo, supongamos que se establecen los siguientes atributos de marca de agua: `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY`y `WaterBackCmd:SRCTEXT`. Aunque el único atributo que desea modificar es `WaterBackCmd:OPACITY`, debe establecer que los demás valores estén bien.

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

Modifique una marca de agua mediante la API de Document Security (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `DocumentSecurityClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recupere la marca de agua que desea modificar.

   Cree un `WatermarkManager` objeto invocando el `DocumentSecurityClient` método `getWatermarkManager` del objeto y pase un valor de cadena que especifique el nombre de la marca de agua. Este método devuelve un `Watermark` objeto que representa la marca de agua que se va a modificar.

1. Defina los atributos de marca de agua.

   Establezca el atributo de opacidad de la marca de agua invocando el `Watermark` método `setOpacity` del objeto y pasando un valor entero que especifica el nivel de opacidad. Un valor de 100 indica que la marca de agua es completamente opaca y un valor de 0 indica que la marca de agua es completamente transparente.

   >[!NOTE]
   >
   >Este ejemplo modifica únicamente el atributo opacity.

1. Actualice la marca de agua.

   * Actualice la marca de agua invocando el `WatermarkManager` método `updateWatermark` del objeto y pasando el `Watermark` objeto cuyo atributo se modificó.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte Inicio rápido (modo SOAP): Modificación de una marca de agua mediante la sección API de Java.

### Modificación de marcas de agua mediante la API de servicio web {#modify-watermarks-using-the-web-service-api}

Modifique una marca de agua mediante la API de Document Security (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `DocumentSecurityServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `RightsManagementServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `DocumentSecurityServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere la marca de agua que desea modificar.

   Recupere la marca de agua que desea modificar invocando el `DocumentSecurityServiceClient` método `getWatermarkByName` del objeto. Pase un valor de cadena que especifique el nombre de la marca de agua. Este método devuelve un `WatermarkSpec` objeto que representa la marca de agua que se va a modificar.

1. Defina los atributos de marca de agua.

   * Para cada propiedad de marca de agua que se va a actualizar, cree un `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto independiente.
   * Establezca el valor clave asignando un valor al miembro de datos del `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto (por ejemplo, `key` `WaterBackCmd:OPACITY)`).
   * Establezca el valor asignando un valor al miembro de datos del `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto (por ejemplo, `value` `.50`).
   * Create a `MyArrayOf_xsd_anyType` object. Para cada `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto, invoque el `MyArrayOf_xsd_anyType` método `Add` del objeto. Pase el `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Asigne el `MyArrayOf_xsd_anyType` objeto al miembro de `WatermarkSpec` datos `values` del objeto.

1. Actualice la marca de agua.

   Actualice la marca de agua invocando el `DocumentSecurityServiceClient` método `updateWatermark` del objeto y pasando el `WatermarkSpec` objeto que representa la marca de agua que se va a modificar.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte el siguiente inicio rápido:

* &quot;Inicio rápido (MTOM): Modificación de una marca de agua mediante la API de servicio web&quot;

## Búsqueda de eventos {#searching-for-events}

El servicio Rights Management rastrea acciones específicas a medida que se producen, como la aplicación de una política a un documento, la apertura de un documento protegido por una política y la revocación del acceso a los documentos. La auditoría de eventos debe habilitarse para el servicio Rights Management o no se realiza el seguimiento de los eventos.

Los eventos se dividen en una de las siguientes categorías:

* Los eventos de administrador son acciones relacionadas con un administrador, como la creación de una nueva cuenta de administrador.
* Los eventos de documento son acciones relacionadas con un documento, como cerrar un documento protegido por una política.
* Los eventos de política son acciones relacionadas con una política, como la creación de una nueva política.
* Los eventos de servicio son acciones relacionadas con el servicio Rights Management, como la sincronización con el directorio del usuario.

Puede buscar eventos específicos mediante la API de Java de Rights Management o la API de servicio web. Al buscar eventos, puede realizar tareas como crear un archivo de registro de ciertos eventos.

>[!NOTE]
>
>Para obtener más información sobre el servicio Rights Management, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-10}

Para buscar un evento de Rights Management, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Rights Management.
1. Especifique el evento para el cual buscar.
1. Busque el evento.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Rights Management Client**

Antes de realizar una operación de servicio de Rights Management mediante programación, debe crear un objeto de cliente de servicio de Rights Management. Si utiliza la API de Java, cree un `DocumentSecurityClient` objeto. Si utiliza la API de servicio web de Rights Management, cree un `DocumentSecurityServiceService` objeto.

**Especifique los eventos para buscar**

Debe especificar el evento que desea buscar. Por ejemplo, puede buscar el evento de creación de directiva, que se produce cuando se crea una nueva directiva.

**Buscar el evento**

Después de especificar el evento que se va a buscar, puede utilizar la API de Java de Rights Management o la API de servicio web de Rights Management para buscar el evento.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Buscar eventos mediante la API de Java {#search-for-events-using-the-java-api}

Busque eventos mediante la API de Rights Management (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Rights Management Client

   Cree un `DocumentSecurityClient` objeto utilizando su constructor y pasando un `ServiceClientFactory` objeto que contenga propiedades de conexión.

1. Especifique los eventos para buscar

   * Cree un `EventManager` objeto invocando el `DocumentSecurityClient` método `getEventManager` del objeto. Este método devuelve un `EventManager` objeto.
   * Cree un `EventSearchFilter` objeto invocando su constructor.
   * Especifique el evento para el que desea realizar la búsqueda invocando el `EventSearchFilter` método del `setEventCode` objeto y pasando un miembro de datos estático que pertenece a la `EventManager` clase que representa el evento para el que desea realizar la búsqueda. Por ejemplo, para buscar el evento de creación de directiva, pase `EventManager.POLICY_CREATE_EVENT`.
   >[!NOTE]
   >
   >Puede definir criterios de búsqueda adicionales invocando métodos de `EventSearchFilter` objeto. Por ejemplo, invoque el `setUserName` método para especificar un usuario asociado al evento.

1. Buscar el evento

   Busque el evento invocando el `EventManager` método `searchForEvents` del objeto y pasando el `EventSearchFilter` objeto que define los criterios de búsqueda de eventos. Este método devuelve una matriz de `Event` objetos.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Rights Management, consulte los siguientes Inicio rápido:

* &quot;Inicio rápido (SOAP): Búsqueda de eventos mediante la API de Java&quot;

### Buscar eventos mediante la API de servicio Web {#search-for-events-using-the-web-service-api}

Buscar eventos mediante la API de Rights Management (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Creación de un objeto de API de Rights Management Client

   * Cree un `DocumentSecurityServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `DocumentSecurityServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `DocumentSecurityServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Especifique los eventos para buscar

   * Cree un `EventSpec` objeto con su constructor.
   * Especifique el inicio del período de tiempo durante el cual se produjo el evento estableciendo el miembro de datos del `EventSpec` objeto con una instancia `firstTime.date` `DataTime` que represente el inicio del intervalo de fechas en el que se produjo el evento.
   * Asigne el valor `true` al miembro de `EventSpec` datos del `firstTime.dateSpecified` objeto.
   * Especifique el final del período de tiempo durante el cual se produjo el evento configurando el miembro de datos del `EventSpec` objeto con una instancia `lastTime.date` `DataTime` que represente el final del intervalo de fechas en el que se produjo el evento.
   * Asigne el valor `true` al miembro de `EventSpec` datos del `lastTime.dateSpecified` objeto.
   * Configure el evento que se va a buscar asignando un valor de cadena al miembro de datos del `EventSpec` objeto `eventCode` . En la tabla siguiente se muestran los valores numéricos que se pueden asignar a esta propiedad:
   <table>
    <thead>
    <tr>
    <th><p>Tipo de evento</p></th>
    <th><p>Value</p></th>
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

   Para buscar el evento, invoque el `DocumentSecurityServiceClient` método `searchForEvents` del objeto y pase el `EventSpec` objeto que representa el evento para el que desea realizar la búsqueda y el número máximo de resultados. Este método devuelve una `MyArrayOf_xsd_anyType` colección donde cada elemento es una `AuditSpec` instancia. Mediante una `AuditSpec` instancia, puede obtener información sobre el evento, como la hora en que se produjo. La `AuditSpec` instancia contiene un miembro `timestamp` de datos que especifica esta información.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Rights Management, consulte los siguientes Inicio rápido:

* &quot;Inicio rápido (MTOM): Búsqueda de eventos mediante la API de servicio web&quot;
* &quot;Inicio rápido (SwaRef): Búsqueda de eventos mediante la API de servicio web&quot;

**Consulte también**

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de formularios AEM mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Aplicación de políticas a documentos de Word {#applying-policies-to-word-documents}

Además de los documentos PDF, el servicio Rights Management admite formatos de documento adicionales, como un documento de Microsoft Word (archivo DOC) y otros formatos de archivo de Microsoft Office. Por ejemplo, puede aplicar una política a un documento de Word para protegerlo. Al aplicar una política a un documento de Word, se restringe el acceso al documento. No puede aplicar una política a un documento si el documento ya está protegido con una política.

Puede supervisar el uso de un documento de Word protegido por una política después de distribuirlo. Es decir, puede ver cómo se utiliza el documento y quién lo utiliza. Por ejemplo, puede averiguar cuándo alguien ha abierto el documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-11}

Para aplicar una política a un documento de Word, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto API de cliente de Document Security.
1. Recupere un documento de Word al que se aplica una política.
1. Aplique una directiva existente al documento de Word.
1. Guarde el documento de Word protegido por una política.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Crear un objeto API de cliente de Document Security**

Para poder realizar una operación de servicio de Document Security mediante programación, debe crear un objeto cliente de servicio de Document Security.

**Recuperar un documento de Word**

Debe recuperar un documento de Word para aplicar una política. Después de aplicar una política al documento de Word, los usuarios quedan restringidos al usar el documento. Por ejemplo, si la política no permite que el documento se abra sin conexión, los usuarios deben estar en línea para abrirlo.

**Aplicar una directiva existente al documento de Word**

Para aplicar una política a un documento de Word, debe hacer referencia a una política existente y especificar a qué conjunto de políticas pertenece la política. El usuario que está configurando las propiedades de conexión debe tener acceso a la directiva especificada. De lo contrario, se produce una excepción.

**Guardar el documento de Word**

Después de que el servicio Document Security aplique una política a un documento de Word, puede guardar el documento de Word protegido por una política como archivo DOC.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revocación del acceso a los documentos](protecting-documents-policies.md#revoking-access-to-documents)

### Aplicar una política a un documento de Word mediante la API de Java {#apply-a-policy-to-a-word-document-using-the-java-api}

Aplicar una política a un documento de Word mediante la API de Document Security (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `DocumentSecurityClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recuperar un documento de Word.

   * Cree un `java.io.FileInputStream` objeto que represente el documento de Word utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento de Word.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Aplique una directiva existente al documento de Word.

   * Cree un `DocumentManager` objeto invocando el `DocumentSecurityClient` método `getDocumentManager` del objeto.
   * Aplique una política al documento de Word invocando el `DocumentManager` método del `protectDocument` objeto y pasando los valores siguientes:

      * El `com.adobe.idp.Document` objeto que contiene el documento de Word al que se aplica la política.
      * Un valor de cadena que especifica el nombre del documento.
      * Un valor de cadena que especifica el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar un `null` valor que resulte en el uso del conjunto de `MyPolicies` directivas.
      * Un valor de cadena que especifica el nombre de la directiva.
      * Un valor de cadena que representa el nombre del dominio del administrador de usuarios del usuario que es el editor del documento. Este valor de parámetro es opcional y puede ser nulo (si este parámetro es nulo, el siguiente valor de parámetro debe ser nulo).
      * Un valor de cadena que representa el nombre canónico del usuario del administrador de usuarios que es el editor del documento. Este valor de parámetro es opcional y puede ser `null` (si este parámetro es `null`, el valor del parámetro anterior debe ser `null`).
      * Una `com.adobe.livecycle.rightsmanagement.Locale` que representa la configuración regional que se utiliza para seleccionar la plantilla de MS Office. Este valor de parámetro es opcional y se puede especificar `null`.
      El `protectDocument` método devuelve un `RMSecureDocumentResult` objeto que contiene el documento de Word protegido por una política.


1. Guarde el documento de Word.

   * Invoque el `RMSecureDocumentResult` método del `getProtectedDoc` objeto para obtener el documento de Word protegido por una política. Este método devuelve un `com.adobe.idp.Document` objeto.
   * Cree un `java.io.File` objeto y asegúrese de que la extensión del archivo sea DOC.
   * Invoque el `com.adobe.idp.Document` método del `copyToFile` objeto para copiar el contenido del `Document` objeto en el archivo (asegúrese de utilizar el `Document` objeto devuelto por el `getProtectedDoc` método).

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte el siguiente inicio rápido:

* &quot;Inicio rápido (modo SOAP): Aplicación de una política a un documento de Word mediante la API de Java&quot;

### Aplicar una política a un documento de Word mediante la API de servicio Web {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Aplicar una política a un documento de Word mediante la API de Document Security (servicio Web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un objeto API de cliente de Document Security.

   * Cree un `DocumentSecurityServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `DocumentSecurityServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `DocumentSecurityServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperar un documento de Word.

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar un documento de Word al que se aplica una política.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento de Word y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto. Pase la matriz de bytes, la posición inicial y la longitud del flujo para leerlos.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Aplique una directiva existente al documento de Word.

   Aplique una política al documento de Word invocando el `DocumentSecurityServiceClient` método del `protectDocument` objeto y pasando los valores siguientes:

   * El `BLOB` objeto que contiene el documento de Word al que se aplica la política.
   * Un valor de cadena que especifica el nombre del documento.
   * Un valor de cadena que especifica el nombre del conjunto de directivas al que pertenece la directiva. Puede especificar un `null` valor que resulte en el uso del conjunto de `MyPolicies` directivas.
   * Un valor de cadena que especifica el nombre de la directiva.
   * Un valor de cadena que representa el nombre del dominio del administrador de usuarios del usuario que es el editor del documento. Este valor de parámetro es opcional y puede ser nulo (si este parámetro es nulo, el siguiente valor de parámetro debe ser `null`).
   * Un valor de cadena que representa el nombre canónico del usuario del administrador de usuarios que es el editor del documento. Este valor de parámetro es opcional y puede ser nulo (si este parámetro es nulo, el valor del parámetro anterior debe ser `null`).
   * Un `RMLocale` valor que especifica el valor de configuración regional (por ejemplo, `RMLocale.en`).
   * Parámetro de salida de cadena que se utiliza para almacenar el valor del identificador de directiva.
   * Parámetro de salida de cadena que se utiliza para almacenar el valor de identificador protegido por una política.
   * Parámetro de salida de cadena que se utiliza para almacenar el tipo MIME (por ejemplo, `application/doc`).
   El `protectDocument` método devuelve un `BLOB` objeto que contiene el documento de Word protegido por una política.

1. Guarde el documento de Word.

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento de Word protegido por una política.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `protectDocument` método. Rellene la matriz de bytes obteniendo el valor del miembro de `BLOB` datos del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.
   * Escriba el contenido de la matriz de bytes en un archivo de Word invocando el `System.IO.BinaryWriter` método `Write` del objeto y pasando la matriz de bytes.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte el siguiente inicio rápido:

* &quot;Inicio rápido (MTOM): Aplicación de una política a un documento de Word mediante la API de servicio Web&quot;

## Eliminación de directivas de documentos de Word {#removing-policies-from-word-documents}

Puede quitar una política de un documento de Word protegido por una política para eliminar la seguridad del documento. Es decir, si ya no desea que el documento esté protegido por una política. Si desea actualizar un documento de Word protegido por una política con una política más reciente, en lugar de quitar la política y agregar la política actualizada, es más eficaz cambiar la política.

>[!NOTE]
>
>Para obtener más información sobre el servicio Document Security, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-12}

Para quitar una política de un documento de Word protegido por una política, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto
1. Cree un objeto API de cliente de Document Security.
1. Recupere un documento de Word protegido por una política.
1. Elimine la directiva del documento de Word.
1. Guardar los documentos de Word no protegidos

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Creación de un objeto de API de Document Security Client**

Antes de realizar una operación de servicio de Document Security mediante programación, cree un objeto cliente de servicio de Document Security.

**Recuperar un documento de Word protegido por una política**

Debe recuperar un documento de Word protegido por una política para eliminar una política. Si intenta eliminar una política de un documento de Word que no esté protegido por una política, provocará una excepción.

**Quitar la directiva del documento de Word**

Puede quitar una directiva de un documento de Word protegido por una política siempre que se especifique un administrador en la configuración de la conexión. Si no es así, la política utilizada para proteger un documento debe contener el `SWITCH_POLICY` permiso para eliminar una política de un documento de Word. Además, el usuario especificado en la configuración de conexión de AEM Forms también debe tener ese permiso. De lo contrario, se genera una excepción.

**Guardar el documento de Word no seguro**

Después de que el servicio Document Security elimine una política de un documento de Word, puede guardar el documento de Word no seguro como un archivo DOC.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicación de políticas a documentos de Word](protecting-documents-policies.md#applying-policies-to-word-documents)

### Eliminar una política de un documento de Word mediante la API de Java {#remove-a-policy-from-a-word-document-using-the-java-api}

Elimine una política de un documento de Word protegido por una política mediante la API de Document Security (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-rightsmanagement-client.jar, en la ruta de clases del proyecto Java.

1. Creación de un objeto de API de Document Security Client

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión.
   * Cree un `RightsManagementClient` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Recuperar un documento de Word protegido por una política

   * Cree un `java.io.FileInputStream` objeto que represente el documento de Word protegido por una política utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento de Word.
   * Cree un `com.adobe.idp.Document` objeto utilizando su constructor y pasando el `java.io.FileInputStream` objeto.

1. Quitar la directiva del documento de Word

   * Cree un `DocumentManager` objeto invocando el `RightsManagementClient` método `getDocumentManager` del objeto.
   * Elimine una política del documento de Word invocando el `DocumentManager` método del `removeSecurity` objeto y pasando el `com.adobe.idp.Document` objeto que contiene el documento de Word protegido por una política. Este método devuelve un `com.adobe.idp.Document` objeto que contiene un documento de Word no seguro.

1. Guardar el documento de Word no seguro

   * Cree un `java.io.File` objeto y asegúrese de que la extensión del archivo sea DOC.
   * Invoque el `Document` método del `copyToFile` objeto para copiar el contenido del `Document` objeto en el archivo (asegúrese de utilizar el `Document` objeto devuelto por el `removeSecurity` método).

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte el siguiente inicio rápido:

* &quot;Inicio rápido (modo SOAP): Eliminación de una directiva de un documento de Word mediante la API de Java&quot;

### Quitar una política de un documento de Word mediante la API de servicio Web {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Elimine una política de un documento de Word protegido por una política mediante la API de Document Security (servicio Web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplazar `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Creación de un objeto de API de Document Security Client

   * Cree un `RightsManagementServiceClient` objeto utilizando su constructor predeterminado.
   * Cree un `RightsManagementServiceClient.Endpoint.Address` objeto mediante el `System.ServiceModel.EndpointAddress` constructor. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) No es necesario usar el `lc_version` atributo. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un `System.ServiceModel.BasicHttpBinding` objeto obteniendo el valor del `RightsManagementServiceClient.Endpoint.Binding` campo. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el `System.ServiceModel.BasicHttpBinding` campo del `MessageEncoding` objeto en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperar un documento de Word protegido por una política

   * Cree un `BLOB` objeto con su constructor. El `BLOB` objeto se utiliza para almacenar el documento de Word protegido por una política del que se ha eliminado la directiva.
   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento de Word y el modo en que se abre el archivo.
   * Cree una matriz de bytes que almacene el contenido del `System.IO.FileStream` objeto. Puede determinar el tamaño de la matriz de bytes obteniendo la `System.IO.FileStream` propiedad del `Length` objeto.
   * Rellene la matriz de bytes con datos de flujo invocando el `System.IO.FileStream` método `Read` del objeto y pasando la matriz de bytes, la posición inicial y la longitud de flujo que se va a leer.
   * Rellene el `BLOB` objeto asignando su `MTOM` campo con el contenido de la matriz de bytes.

1. Quitar la directiva del documento de Word

   Elimine la política del documento de Word invocando el `RightsManagementServiceClient` método del `removePolicySecurity` objeto y pasando el `BLOB` objeto que contiene el documento de Word protegido por una política. Este método devuelve un `BLOB` objeto que contiene un documento de Word no seguro.

1. Guardar el documento de Word no seguro

   * Cree un `System.IO.FileStream` objeto invocando su constructor y pasando un valor de cadena que representa la ubicación del archivo del documento de Word no protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del `BLOB` objeto devuelto por el `removePolicySecurity` método. Rellene la matriz de bytes obteniendo el valor del `BLOB` campo del `MTOM` objeto.
   * Cree un `System.IO.BinaryWriter` objeto invocando su constructor y pasando el `System.IO.FileStream` objeto.

**Ejemplos de código**

Para ver ejemplos de código que utilizan el servicio Document Security, consulte el siguiente inicio rápido:

* &quot;Inicio rápido (MTOM): Eliminación de una política de un documento de Word mediante la API de servicio Web&quot;

**Consulte también**

[Invocación de formularios AEM mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
