---
title: Administración de usuarios
seo-title: Administración de usuarios
description: Utilice la API de administración de usuarios para crear aplicaciones cliente que puedan administrar funciones, permisos y entidades principales (que pueden ser usuarios o grupos), así como autenticar usuarios.
seo-description: Utilice la API de administración de usuarios para crear aplicaciones cliente que puedan administrar funciones, permisos y entidades principales (que pueden ser usuarios o grupos), así como autenticar usuarios.
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
role: Desarrollador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '6258'
ht-degree: 0%

---


# Administración de usuarios {#managing-users}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

**Acerca de la administración de usuarios**

Puede utilizar la API de administración de usuarios para crear aplicaciones cliente que puedan administrar funciones, permisos y entidades principales (que pueden ser usuarios o grupos), así como autenticar usuarios. La API de administración de usuarios consta de las siguientes API de AEM Forms:

* API del servicio de Directory Manager
* API del servicio de Authentication Manager
* API del servicio de Administrador de autorización

La administración de usuarios permite asignar, eliminar y determinar funciones y permisos. También le permite asignar, eliminar y consultar dominios, usuarios y grupos. Por último, puede utilizar Administración de usuarios para autenticar a los usuarios.

En [Agregar usuarios](users.md#adding-users) comprenderá cómo agregar usuarios mediante programación. Esta sección utiliza la API de servicio del Administrador de directorios.

En [Eliminación de usuarios](users.md#deleting-users) comprenderá cómo eliminar usuarios mediante programación. Esta sección utiliza la API de servicio del Administrador de directorios.

En [Administración de usuarios y grupos](users.md#managing-users-and-groups) comprenderá la diferencia entre un usuario local y un usuario de directorio, y verá ejemplos de cómo usar las API de servicio web y Java para administrar usuarios y grupos mediante programación. Esta sección utiliza la API de servicio del Administrador de directorios.

En [Administración de funciones y permisos](users.md#managing-roles-and-permissions) aprenderá sobre las funciones y los permisos del sistema y lo que puede hacer mediante programación para aumentarlos, y verá ejemplos de cómo utilizar las API de servicio web y Java para administrar funciones y permisos mediante programación. Esta sección utiliza tanto la API de servicio del Administrador de directorios como la API de servicio del Administrador de autorizaciones.

En [Autenticar usuarios](users.md#authenticating-users) verá ejemplos de cómo utilizar las API de Java y de servicio web para autenticar usuarios mediante programación. Esta sección utiliza la API de servicio de Administrador de autorización.

**Explicación del proceso de autenticación**

La administración de usuarios proporciona funcionalidad de autenticación integrada y también le proporciona la capacidad de conectarla con su propio proveedor de autenticación. Cuando la Administración de usuarios recibe una solicitud de autenticación (por ejemplo, cuando un usuario intenta iniciar sesión), pasa la información del usuario al proveedor de autenticación para que la autentique. La Administración de usuarios recibe los resultados del proveedor de autenticación después de autenticar al usuario.

El diagrama siguiente muestra la interacción entre un usuario final que intenta iniciar sesión, Administración de usuarios y el proveedor de autenticación.

![mu_mu_umauth_process](assets/mu_mu_umauth_process.png)

La siguiente tabla describe cada paso del proceso de autenticación.

<table>
 <thead>
  <tr>
   <th><p>Etapa</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Un usuario intenta iniciar sesión en un servicio que invoca la Administración de usuarios. El usuario especifica un nombre de usuario y una contraseña. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>La administración de usuarios envía el nombre de usuario y la contraseña, así como la información de configuración, al proveedor de autenticación.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>El proveedor de autenticación se conecta al almacén de usuarios y autentica al usuario.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>El proveedor de autenticación devuelve los resultados a Administración de usuarios.</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>La Administración de usuarios permite al usuario iniciar sesión o deniega el acceso al producto.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Si la zona horaria del servidor es diferente de la zona horaria del cliente, al consumir el WSDL para el servicio AEM Forms Generate PDF en una pila SOAP nativa mediante un cliente .NET en un clúster de Servidor de aplicaciones WebSphere, puede producirse el siguiente error de autenticación de Administración de usuarios:

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**Explicación de la administración de directorios**

La Administración de usuarios está empaquetada con un proveedor de servicios de directorio (DirectoryManagerService) que admite conexiones a directorios LDAP. Si su organización utiliza un repositorio no LDAP para almacenar registros de usuario, puede crear su propio proveedor de servicios de directorio que funcione con su repositorio.

Los proveedores de servicios de directorio recuperan registros de un almacén de usuarios a petición de la Administración de usuarios. La Administración de usuarios almacena en caché regularmente los registros de usuarios y grupos de la base de datos para mejorar el rendimiento.

El proveedor de servicios de directorio puede utilizarse para sincronizar la base de datos de Administración de usuarios con el almacén de usuarios. Este paso garantiza que toda la información del directorio de usuario y todos los registros de usuario y grupo estén actualizados.

Además, DirectoryManagerService permite crear y administrar dominios. Los dominios definen diferentes bases de usuario. El límite de un dominio se define generalmente según la forma en que se estructura su organización o cómo se configura el almacén de usuarios. Los dominios de administración de usuarios proporcionan configuraciones que utilizan los proveedores de autenticación y los proveedores de servicios de directorio.

En el XML de configuración que exporta User Management, el nodo raíz que tiene el valor de atributo `Domains` contiene un elemento XML para cada dominio definido para User Management. Cada uno de estos elementos contiene otros elementos que definen aspectos del dominio asociados a proveedores de servicios específicos.

**Explicación de los valores de objectSID**

Al utilizar Active Directory, es importante comprender que un valor `objectSID` no es un atributo único en varios dominios. Este valor almacena el identificador de seguridad de un objeto. En un entorno de varios dominios (por ejemplo, un árbol de dominios), el valor `objectSID` puede ser diferente.

Un valor `objectSID` cambiaría si un objeto se movía de un dominio de Active Directory a otro dominio. Algunos objetos tienen el mismo valor `objectSID` en cualquier parte del dominio. Por ejemplo, grupos como BUILTIN\Administradores, BUILTIN\Power Users, etc. tendrían el mismo valor `objectSID` independientemente de los dominios. Estos valores `objectSID` son bien conocidos.

## Adición de usuarios {#adding-users}

Puede utilizar la API de servicio del Administrador de directorios (Java y servicio web) para agregar usuarios mediante programación a AEM Forms. Después de agregar un usuario, puede utilizarlo cuando realice una operación de servicio que requiera un usuario. Por ejemplo, puede asignar una tarea al nuevo usuario.

### Resumen de los pasos {#summary-of-steps}

Para agregar un usuario, realice los pasos siguientes:

1. Incluir archivos de proyecto.
1. Cree un cliente DirectoryManagerService.
1. Defina la información del usuario.
1. Agregue el usuario a AEM Forms.
1. Compruebe que se ha agregado el usuario.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Crear un cliente DirectoryManagerService**

Antes de realizar una operación de servicio de Directory Manager mediante programación, cree un cliente de API de Directory Manager Service.

**Definir la información del usuario**

Cuando agregue un nuevo usuario mediante la API de servicio del Administrador de directorios, defina la información para ese usuario. Normalmente, al agregar un nuevo usuario, se definen los siguientes valores:

* **Nombre** de dominio: Dominio al que pertenece el usuario (por ejemplo,  `DefaultDom`).
* **Valor** del identificador de usuario: El valor identificador del usuario (por ejemplo,  `wblue`).
* **Tipo** principal: Tipo de usuario (por ejemplo, puede especificar  `USER)`.
* **Nombre** dado: Un nombre determinado para el usuario (por ejemplo,  `Wendy`).
* **Nombre** de la familia: El apellido del usuario (por ejemplo,  `Blue)`.
* **Configuración regional**: Información de configuración regional para el usuario.

**Agregar el usuario a AEM Forms**

Después de definir la información de usuario, puede agregarlo a AEM Forms. Para agregar un usuario, invoque el método `DirectoryManagerServiceClient` del objeto `createLocalUser`.

**Comprobar que se ha agregado el usuario**

Puede verificar que el usuario se agregó para asegurarse de que no se produjeron problemas. Busque el nuevo usuario utilizando el valor del identificador de usuario.

**Consulte también**

[Agregar usuarios mediante la API de Java](users.md#add-users-using-the-java-api)

[Agregar usuarios mediante la API de servicio web](users.md#add-users-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Eliminación de usuarios](users.md#deleting-users)

### Agregar usuarios mediante la API de Java {#add-users-using-the-java-api}

Agregue usuarios mediante la API del servicio Directory Manager (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-usermanager-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de DirectoryManagerServices.

   Cree un objeto `DirectoryManagerServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Defina la información del usuario.

   * Cree un objeto `UserImpl` utilizando su constructor.
   * Establezca el nombre del dominio invocando el método `UserImpl` del objeto `setDomainName`. Pase un valor de cadena que especifique el nombre de dominio.
   * Establezca el tipo principal invocando el método `UserImpl` del objeto `setPrincipalType`. Pasa un valor de cadena que especifica el tipo de usuario. Por ejemplo, puede especificar `USER`.
   * Establezca el valor del identificador de usuario invocando el método `UserImpl` del objeto `setUserid`. Pase un valor de cadena que especifique el valor del identificador de usuario. Por ejemplo, puede especificar `wblue`.
   * Establezca el nombre canónico invocando el método `UserImpl` del objeto `setCanonicalName`. Pase un valor de cadena que especifique el nombre canónico del usuario. Por ejemplo, puede especificar `wblue`.
   * Establezca el nombre dado invocando el método `UserImpl` del objeto `setGivenName`. Pase un valor de cadena que especifique el nombre dado del usuario. Por ejemplo, puede especificar `Wendy`.
   * Establezca el nombre de la familia invocando el método `UserImpl` del objeto `setFamilyName`. Pase un valor de cadena que especifique el nombre de familia del usuario. Por ejemplo, puede especificar `Blue`.

   >[!NOTE]
   >
   >Invoque un método que pertenezca al objeto `UserImpl` para establecer otros valores. Por ejemplo, puede establecer el valor de configuración regional invocando el método `UserImpl` del objeto `setLocale`.

1. Agregue el usuario a AEM Forms.

   Invoque el método `DirectoryManagerServiceClient` del objeto `createLocalUser` y pase los siguientes valores:

   * El objeto `UserImpl` que representa al nuevo usuario
   * Un valor de cadena que representa la contraseña del usuario

   El método `createLocalUser` devuelve un valor de cadena que especifica el valor del identificador de usuario local.

1. Compruebe que se ha agregado el usuario.

   * Cree un objeto `PrincipalSearchFilter` utilizando su constructor.
   * Establezca el valor del identificador de usuario invocando el método `PrincipalSearchFilter` del objeto `setUserId`. Pase un valor de cadena que represente el valor del identificador de usuario.
   * Invoque el método `DirectoryManagerServiceClient` del objeto `findPrincipals` y pase el objeto `PrincipalSearchFilter`. Este método devuelve una instancia `java.util.List`, donde cada elemento es un objeto `User`. Repita la instancia `java.util.List` para localizar al usuario.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Inicio rápido (modo SOAP): Adición de usuarios mediante la API de Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Agregar usuarios mediante la API de servicio web {#add-users-using-the-web-service-api}

Agregue usuarios mediante la API del servicio Directory Manager (servicio Web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL para la referencia de servicio: `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente DirectoryManagerService.

   * Cree un objeto `DirectoryManagerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `DirectoryManagerServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio. Asegúrese de especificar `?blob=mtom`.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `DirectoryManagerServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Defina la información del usuario.

   * Cree un objeto `UserImpl` utilizando su constructor.
   * Establezca el nombre del dominio asignando un valor de cadena al campo `UserImpl` del objeto `domainName`.
   * Establezca el tipo principal asignando un valor de cadena al campo `UserImpl` del objeto `principalType`. Por ejemplo, puede especificar `USER`.
   * Establezca el valor del identificador de usuario asignando un valor de cadena al campo `UserImpl` `userid` del objeto.
   * Establezca el valor del nombre canónico asignando un valor de cadena al campo `UserImpl` del objeto `canonicalName`.
   * Establezca el valor de nombre asignado asignando un valor de cadena al campo `UserImpl` del objeto `givenName`.
   * Establezca el valor del nombre de familia asignando un valor de cadena al campo `UserImpl` del objeto `familyName`.

1. Agregue el usuario a AEM Forms.

   Invoque el método `DirectoryManagerServiceClient` del objeto `createLocalUser` y pase los siguientes valores:

   * El objeto `UserImpl` que representa al nuevo usuario
   * Un valor de cadena que representa la contraseña del usuario

   El método `createLocalUser` devuelve un valor de cadena que especifica el valor del identificador de usuario local.

1. Compruebe que se ha agregado el usuario.

   * Cree un objeto `PrincipalSearchFilter` utilizando su constructor.
   * Establezca el valor del identificador de usuario asignando un valor de cadena que represente el valor del identificador de usuario al campo `PrincipalSearchFilter` del objeto `userId`.
   * Invoque el método `DirectoryManagerServiceClient` del objeto `findPrincipals` y pase el objeto `PrincipalSearchFilter`. Este método devuelve un objeto de colección `MyArrayOfUser`, donde cada elemento es un objeto `User`. Repita la colección `MyArrayOfUser` para localizar al usuario.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminación de usuarios {#deleting-users}

Puede utilizar la API de servicio del Administrador de directorios (Java y servicio web) para eliminar usuarios mediante programación de AEM Forms. Después de eliminar un usuario, este ya no se puede utilizar para realizar una operación de servicio que requiera un usuario. Por ejemplo, no se puede asignar una tarea a un usuario eliminado.

### Resumen de los pasos {#summary_of_steps-1}

Para eliminar un usuario, realice los pasos siguientes:

1. Incluir archivos de proyecto.
1. Cree un cliente DirectoryManagerService.
1. Especifique el usuario que desea eliminar.
1. Elimine el usuario de AEM Forms.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Crear un cliente DirectoryManagerService**

Antes de poder realizar mediante programación una operación de API de servicio de Directory Manager, cree un cliente de servicio de Directory Manager.

**Especificar el usuario que se va a eliminar**

Puede especificar el usuario que desea eliminar utilizando el valor de identificador del usuario.

**Eliminar el usuario de AEM Forms**

Para eliminar un usuario, invoque el método `DirectoryManagerServiceClient` del objeto `deleteLocalUser`.

**Consulte también**

[Eliminar usuarios mediante la API de Java](users.md#delete-users-using-the-java-api)

[Eliminar usuarios mediante la API de servicio web](users.md#delete-users-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adición de usuarios](users.md#adding-users)

### Eliminar usuarios mediante la API de Java {#delete-users-using-the-java-api}

Eliminar usuarios mediante la API del servicio Directory Manager (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-usermanager-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente DirectoryManagerService.

   Cree un objeto `DirectoryManagerServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Especifique el usuario que desea eliminar.

   * Cree un objeto `PrincipalSearchFilter` utilizando su constructor.
   * Establezca el valor del identificador de usuario invocando el método `PrincipalSearchFilter` del objeto `setUserId`. Pase un valor de cadena que represente el valor del identificador de usuario.
   * Invoque el método `DirectoryManagerServiceClient` del objeto `findPrincipals` y pase el objeto `PrincipalSearchFilter`. Este método devuelve una instancia `java.util.List`, donde cada elemento es un objeto `User`. Repita la instancia `java.util.List` para localizar el usuario que desea eliminar.

1. Elimine el usuario de AEM Forms.

   Invoque el método `DirectoryManagerServiceClient` del objeto `deleteLocalUser` y pase el valor del campo `User` del objeto `oid`. Invoque el método `User` del objeto `getOid`. Utilice el objeto `User` recuperado de la instancia `java.util.List`.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Inicio rápido (modo EJB): Eliminación de usuarios mediante la API de Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Inicio rápido (modo SOAP): Eliminación de usuarios mediante la API de Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminar usuarios mediante la API de servicio web {#delete-users-using-the-web-service-api}

Eliminar usuarios mediante la API del servicio Directory Manager (servicio Web):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-usermanager-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente DirectoryManagerService.

   * Cree un objeto `DirectoryManagerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `DirectoryManagerServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio. Asegúrese de especificar `blob=mtom.`
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `DirectoryManagerServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Especifique el usuario que desea eliminar.

   * Cree un objeto `PrincipalSearchFilter` utilizando su constructor.
   * Establezca el valor del identificador de usuario asignando un valor de cadena al campo `PrincipalSearchFilter` `userId` del objeto.
   * Invoque el método `DirectoryManagerServiceClient` del objeto `findPrincipals` y pase el objeto `PrincipalSearchFilter`. Este método devuelve un objeto de colección `MyArrayOfUser`, donde cada elemento es un objeto `User`. Repita la colección `MyArrayOfUser` para localizar al usuario. El objeto `User` recuperado del objeto de colección `MyArrayOfUser` se utiliza para eliminar al usuario.

1. Elimine el usuario de AEM Forms.

   Elimine el usuario pasando el valor del campo `User` del objeto `oid` al método `DirectoryManagerServiceClient` del objeto `deleteLocalUser`.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Creación de grupos {#creating-groups}

Puede utilizar la API de servicio del Administrador de directorios (Java y servicio web) para crear grupos de AEM Forms mediante programación. Después de crear un grupo, puede utilizarlo para realizar una operación de servicio que requiera un grupo. Por ejemplo, puede asignar un usuario al nuevo grupo. (Consulte [Administración de usuarios y grupos](users.md#managing-users-and-groups)).

### Resumen de los pasos {#summary_of_steps-2}

Para crear un grupo, realice los pasos siguientes:

1. Incluir archivos de proyecto.
1. Cree un cliente DirectoryManagerService.
1. Determine que el grupo no existe.
1. Cree el grupo.
1. Realice una acción con el grupo.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-Utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente DirectoryManagerService**

Antes de realizar una operación de servicio de Directory Manager mediante programación, cree un cliente de API de Directory Manager Service.

**Determinar si el grupo existe**

Cuando cree un grupo, asegúrese de que el grupo no exista en el mismo dominio. Es decir, dos grupos no pueden tener el mismo nombre dentro del mismo dominio. Para realizar esta tarea, realice una búsqueda y filtre los resultados de búsqueda en función de dos valores. Establezca el tipo principal en `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` para asegurarse de que solo se devuelvan los grupos. Además, asegúrese de especificar el nombre de dominio.

**Crear el grupo**

Después de determinar que el grupo no existe en el dominio, cree el grupo y especifique los siguientes atributos:

* **Nombre** común: Nombre del grupo.
* **Dominio**: Dominio en el cual se agrega el grupo.
* **Descripción**: Descripción del grupo.

**Realizar una acción con el grupo**

Después de crear un grupo, puede realizar una acción utilizando el grupo . Por ejemplo, puede agregar un usuario al grupo. Para agregar un usuario a un grupo, recupere el valor de identificador único del usuario y del grupo. Pase estos valores al método `addPrincipalToLocalGroup` .

**Consulte también**

[Creación de grupos mediante la API de Java](users.md#create-groups-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adición de usuarios](users.md#adding-users)

[Eliminación de usuarios](users.md#deleting-users)

### Creación de grupos mediante la API de Java {#create-groups-using-the-java-api}

Cree un grupo utilizando la API del servicio Directory Manager (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-usermanager-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente DirectoryManagerService.

   Cree un objeto `DirectoryManagerServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Determine si existe el grupo.

   * Cree un objeto `PrincipalSearchFilter` utilizando su constructor.
   * Establezca el tipo principal invocando el objeto `PrincipalSearchFilter` del objeto `setPrincipalType`. Pase el valor `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`.
   * Establezca el dominio invocando el objeto `PrincipalSearchFilter` del objeto `setSpecificDomainName`. Pase un valor de cadena que especifique el nombre de dominio.
   * Para encontrar un grupo, invoque el método `DirectoryManagerServiceClient` del objeto `findPrincipals` (una entidad de seguridad puede ser un grupo). Pase el objeto `PrincipalSearchFilter` que especifica el tipo principal y el nombre de dominio. Este método devuelve una instancia `java.util.List` donde cada elemento es una instancia `Group`. Cada instancia de grupo se ajusta al filtro especificado utilizando el objeto `PrincipalSearchFilter` .
   * Se repite a través de la instancia `java.util.List`. Para cada elemento, recupere el nombre del grupo. Asegúrese de que el nombre del grupo no sea igual al nuevo nombre del grupo.

1. Cree el grupo.

   * Si el grupo no existe, invoque el método `Group` del objeto `setCommonName` y pase un valor de cadena que especifique el nombre del grupo.
   * Invoque el método `Group` del objeto `setDescription` y pase un valor de cadena que especifique la descripción del grupo.
   * Invoque el método `Group` del objeto `setDomainName` y pase un valor de cadena que especifique el nombre de dominio.
   * Invoque el método `DirectoryManagerServiceClient` del objeto `createLocalGroup` y pase la instancia `Group`.

   El método `createLocalUser` devuelve un valor de cadena que especifica el valor del identificador de usuario local.

1. Realice una acción con el grupo.

   * Cree un objeto `PrincipalSearchFilter` utilizando su constructor.
   * Establezca el valor del identificador de usuario invocando el método `PrincipalSearchFilter` del objeto `setUserId`. Pase un valor de cadena que represente el valor del identificador de usuario.
   * Invoque el método `DirectoryManagerServiceClient` del objeto `findPrincipals` y pase el objeto `PrincipalSearchFilter`. Este método devuelve una instancia `java.util.List`, donde cada elemento es un objeto `User`. Repita la instancia `java.util.List` para localizar al usuario.
   * Agregue un usuario al grupo invocando el método `DirectoryManagerServiceClient` del objeto `addPrincipalToLocalGroup`. Pase el valor devuelto del método `User` del objeto `getOid`. Pase el valor devuelto del método `Group` del objeto `getOid` (utilice la instancia `Group` que representa el nuevo grupo).

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Administración de usuarios y grupos {#managing-users-and-groups}

En este tema se describe cómo puede utilizar (Java) para asignar, quitar y consultar mediante programación dominios, usuarios y grupos.

>[!NOTE]
>
>Al configurar un dominio, debe establecer el identificador único para grupos y usuarios. El atributo elegido no solo debe ser único dentro del entorno LDAP, sino que también debe ser inmutable y no cambiará dentro del directorio. Este atributo también debe ser de un tipo de datos de cadena simple (la única excepción actualmente permitida para Active Directory 2000/2003 es `"objectsid"`, que es un valor binario). El atributo `"GUID"` de Novell eDirectory, por ejemplo, no es un tipo de datos de cadena simple y, por lo tanto, no funcionará.

* Para Active Directory, utilice `"objectsid"`.
* Para SunOne, utilice `"nsuniqueid"`.

>[!NOTE]
>
>No se admite la creación de varios usuarios y grupos locales mientras la sincronización de directorios LDAP está en curso. Si se intenta este proceso, pueden producirse errores.

### Resumen de los pasos {#summary_of_steps-3}

Para administrar usuarios y grupos, realice los pasos siguientes:

1. Incluir archivos de proyecto.
1. Cree un cliente DirectoryManagerService.
1. Invoque las operaciones de usuario o grupo correspondientes.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente DirectoryManagerService**

Para poder realizar una operación de servicio de Directory Manager mediante programación, debe crear un cliente de servicio de Directory Manager. Con la API de Java, esto se consigue creando un objeto `DirectoryManagerServiceClient`. Con la API de servicio web, esto se consigue creando un objeto `DirectoryManagerServiceService`.

**Invocar las operaciones de usuario o grupo apropiadas**

Una vez creado el cliente de servicio, puede invocar las operaciones de administración de usuarios o grupos. El cliente de servicio permite asignar, eliminar y consultar dominios, usuarios y grupos. Tenga en cuenta que es posible añadir una entidad de seguridad de directorio o una entidad de seguridad local a un grupo local, pero no es posible añadir una entidad de seguridad local a un grupo de directorios.

**Consulte también**

[Administración de usuarios y grupos mediante la API de Java](users.md#managing-users-and-groups-using-the-java-api)

[Administración de usuarios y grupos mediante la API de servicio web](users.md#managing-users-and-groups-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API de User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Administración de usuarios y grupos mediante la API de Java {#managing-users-and-groups-using-the-java-api}

Para administrar mediante programación usuarios, grupos y dominios que utilizan (Java), realice las siguientes tareas:

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-usermanager-client.jar, en la ruta de clase de su proyecto Java. Para obtener información sobre la ubicación de estos archivos, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Cree un cliente DirectoryManagerService.

   Cree un objeto `DirectoryManagerServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión. Para obtener más información, consulte [Configuración de las propiedades de conexión ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*.*

1. Invoque las operaciones de usuario o grupo correspondientes.

   Para encontrar un usuario o grupo, invoque uno de los métodos del objeto `DirectoryManagerServiceClient` para buscar entidades principales (ya que una entidad de seguridad puede ser un usuario o un grupo). En el ejemplo siguiente, se llama al método `findPrincipals` mediante un filtro de búsqueda (un objeto `PrincipalSearchFilter`).

   Dado que el valor devuelto en este caso es un `java.util.List` que contiene `Principal` objetos, repita el resultado y convierta los objetos `Principal` en objetos `User` u `Group`.

   Mediante el objeto `User` o `Group` resultante (que ambos heredan de la interfaz `Principal`), recupere la información que necesita en los flujos de trabajo. Por ejemplo, los valores de nombre de dominio y nombre canónico, en combinación, identifican de forma exclusiva una entidad de seguridad. Se recuperan invocando los métodos `Principal` y `getCanonicalName` del objeto `getDomainName`, respectivamente.

   Para eliminar un usuario local, invoque el método `DirectoryManagerServiceClient` del objeto `deleteLocalUser` y pase el identificador del usuario.

   Para eliminar un grupo local, invoque el método `DirectoryManagerServiceClient` del objeto `deleteLocalGroup` y pase el identificador del grupo.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Administración de usuarios y grupos mediante la API de servicio web {#managing-users-and-groups-using-the-web-service-api}

Para administrar mediante programación usuarios, grupos y dominios mediante la API del servicio Administrador de directorios (servicio web), realice las siguientes tareas:

1. Incluir archivos de proyecto.

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL del Administrador de directorios. (Consulte [Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)).
   * Haga referencia al ensamblado cliente de Microsoft .NET. (Consulte [Creación de un ensamblado de cliente .NET que utilice la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)).

1. Cree un cliente DirectoryManagerService.

   Cree un objeto `DirectoryManagerServiceService` utilizando el constructor de su clase proxy.

1. Invoque las operaciones de usuario o grupo correspondientes.

   Para encontrar un usuario o grupo, invoque uno de los métodos del objeto `DirectoryManagerServiceService` para buscar entidades principales (ya que una entidad de seguridad puede ser un usuario o un grupo). En el ejemplo siguiente, se llama al método `findPrincipalsWithFilter` mediante un filtro de búsqueda (un objeto `PrincipalSearchFilter`). Cuando se utiliza un objeto `PrincipalSearchFilter`, los principales locales solo se devuelven si la propiedad `isLocal` está establecida en `true`. Este comportamiento es diferente a lo que ocurriría con la API de Java.

   >[!NOTE]
   >
   >Si no se especifica el número máximo de resultados en el filtro de búsqueda (a través del campo `PrincipalSearchFilter.resultsMax` ), se devuelve un máximo de 1000 resultados. Este comportamiento es diferente al que se produce con la API de Java, en la que el máximo predeterminado es 10 resultados. Además, los métodos de búsqueda como `findGroupMembers` no darán ningún resultado a menos que se especifique el número máximo de resultados en el filtro de búsqueda (por ejemplo, a través del campo `GroupMembershipSearchFilter.resultsMax` ). Esto se aplica a todos los filtros de búsqueda que heredan de la clase `GenericSearchFilter`. Para obtener más información, consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   Dado que el valor devuelto en este caso es un `object[]` que contiene `Principal` objetos, repita el resultado y convierta los objetos `Principal` en objetos `User` u `Group`.

   Mediante el objeto `User` o `Group` resultante (que ambos heredan de la interfaz `Principal`), recupere la información que necesita en los flujos de trabajo. Por ejemplo, los valores de nombre de dominio y nombre canónico, en combinación, identifican de forma exclusiva una entidad de seguridad. Se recuperan invocando los campos `Principal` y `canonicalName` del objeto `domainName`, respectivamente.

   Para eliminar un usuario local, invoque el método `DirectoryManagerServiceService` del objeto `deleteLocalUser` y pase el identificador del usuario.

   Para eliminar un grupo local, invoque el método `DirectoryManagerServiceService` del objeto `deleteLocalGroup` y pase el identificador del grupo.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Administración de roles y permisos {#managing-roles-and-permissions}

En este tema se describe cómo puede utilizar la API de servicio de Administrador de autorización (Java) para asignar, quitar y determinar funciones y permisos mediante programación.

En AEM Forms, una *función* es un grupo de permisos para acceder a uno o más recursos a nivel del sistema. Estos permisos se crean mediante Administración de usuarios y los componentes del servicio los aplican. Por ejemplo, un administrador podría asignar la función &quot;Autor de conjuntos de políticas&quot; a un grupo de usuarios. El Rights Management permitiría entonces a los usuarios de ese grupo con esa función crear conjuntos de políticas a través de la consola de administración.

Existen dos tipos de funciones: *funciones predeterminadas* y *funciones personalizadas*. Las funciones predeterminadas (*roles del sistema)* ya residen en AEM Forms. Se da por hecho que el administrador no puede eliminar ni modificar las funciones predeterminadas y, por lo tanto, son inmutables. Por lo tanto, las funciones personalizadas creadas por el administrador, que posteriormente pueden modificarlas o eliminarlas, son mutables.

Las funciones facilitan la administración de permisos. Cuando se asigna una función a una entidad de seguridad, se asigna automáticamente un conjunto de permisos a esa entidad de seguridad y todas las decisiones específicas relacionadas con el acceso para la entidad de seguridad se basan en ese conjunto general de permisos asignados.

### Resumen de los pasos {#summary_of_steps-4}

Para administrar las funciones y los permisos, realice los pasos siguientes:

1. Incluir archivos de proyecto.
1. Cree un cliente AuthorizationManagerService.
1. Invoque la función adecuada o las operaciones de permisos.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de AuthorizationManagerService**

Antes de poder realizar mediante programación una operación User Management AuthorizationManagerService, debe crear un cliente AuthorizationManagerService. Con la API de Java, esto se consigue creando un objeto `AuthorizationManagerServiceClient`.

**Invocar la función adecuada o las operaciones de permisos**

Una vez creado el cliente de servicio, puede invocar la función o las operaciones de permiso. El cliente de servicio permite asignar, quitar y determinar funciones y permisos.

**Consulte también**

[Administración de funciones y permisos mediante la API de Java](users.md#managing-roles-and-permissions-using-the-java-api)

[Administración de funciones y permisos mediante la API de servicio web](users.md#managing-roles-and-permissions-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API de User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Administración de funciones y permisos mediante la API de Java {#managing-roles-and-permissions-using-the-java-api}

Para administrar funciones y permisos mediante la API de servicio de Administrador de autorización (Java), realice las siguientes tareas:

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-usermanager-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente AuthorizationManagerService.

   Cree un objeto `AuthorizationManagerServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invoque la función adecuada o las operaciones de permisos.

   Para asignar una función a una entidad de seguridad, invoque el método `AuthorizationManagerServiceClient` del objeto `assignRole` y pase los siguientes valores:

   * Un objeto `java.lang.String` que contiene el identificador de función
   * Matriz de objetos `java.lang.String` que contiene los identificadores principales.

   Para quitar una función de una entidad de seguridad, invoque el método `AuthorizationManagerServiceClient` del objeto `unassignRole` y pase los siguientes valores:

   * Un objeto `java.lang.String` que contiene el identificador de función.
   * Matriz de objetos `java.lang.String` que contiene los identificadores principales.


**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Inicio rápido (modo SOAP): Administración de funciones y permisos mediante la API de Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Administración de funciones y permisos mediante la API de servicio web {#managing-roles-and-permissions-using-the-web-service-api}

Administre las funciones y los permisos mediante la API de servicio de Administrador de autorización (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sustituya `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente AuthorizationManagerService.

   * Cree un objeto `AuthorizationManagerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `AuthorizationManagerServiceClient.Endpoint.Address` utilizando el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`). No es necesario utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `AuthorizationManagerServiceClient.Endpoint.Binding`. Establezca el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Invoque la función adecuada o las operaciones de permisos.

   Para asignar una función a una entidad de seguridad, invoque el método `AuthorizationManagerServiceClient` del objeto `assignRole` y pase los siguientes valores:

   * Un objeto `string` que contiene el identificador de función
   * Un objeto `MyArrayOf_xsd_string` que contiene los identificadores principales.

   Para quitar una función de una entidad de seguridad, invoque el método `AuthorizationManagerServiceService` del objeto `unassignRole` y pase los siguientes valores:

   * Un objeto `string` que contiene el identificador de función.
   * Matriz de objetos `string` que contiene los identificadores principales.


**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Autenticar usuarios {#authenticating-users}

En este tema se describe cómo puede utilizar la API de servicio de Authentication Manager (Java) para habilitar las aplicaciones cliente para autenticar usuarios mediante programación.

Es posible que se requiera autenticación de usuarios para interactuar con una base de datos empresarial u otros repositorios empresariales que almacenan datos seguros.

Considere, por ejemplo, un escenario en el que un usuario introduce un nombre de usuario y una contraseña en una página web y envía los valores a un servidor de aplicaciones J2EE que aloja Forms. Una aplicación personalizada de Forms puede autenticar al usuario con el servicio Authentication Manager.

Si la autenticación se realiza correctamente, la aplicación accede a una base de datos empresarial segura. De lo contrario, se envía un mensaje al usuario en el que se indica que el usuario no es un usuario autorizado.

El diagrama siguiente muestra el flujo lógico de la aplicación.

![au_au_umauth_process](assets/au_au_umauth_process.png)

En la tabla siguiente se describen los pasos de este diagrama

<table>
 <thead>
  <tr>
   <th><p>Etapa</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>El usuario accede a un sitio web y especifica un nombre de usuario y una contraseña. Esta información se envía a un servidor de aplicaciones J2EE que aloja AEM Forms.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Las credenciales del usuario se autentican con el servicio de Authentication Manager. Si las credenciales del usuario son válidas, el flujo de trabajo continúa con el paso 3. De lo contrario, se envía un mensaje al usuario en el que se indica que el usuario no es un usuario autorizado.</p></td>
  </tr>
  <tr>
   <td><p>1</p></td>
   <td><p>La información de usuario y el diseño de formulario se recuperan de una base de datos empresarial segura. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>La información del usuario se combina con un diseño de formulario y este se representa para el usuario. </p></td>
  </tr>
 </tbody>
</table>

### Resumen de los pasos {#summary_of_steps-5}

Para autenticar a un usuario mediante programación, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente AuthenticationManagerService.
1. Invoque la operación de autenticación.
1. Si es necesario, recupere el contexto para que la aplicación cliente pueda reenviarlo a otro servicio de AEM Forms para su autenticación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente AuthenticationManagerService**

Para poder autenticar a un usuario mediante programación, debe crear un cliente AuthenticationManagerService. Cuando utilice la API de Java, cree un objeto `AuthenticationManagerServiceClient`.

**Invocar la operación de autenticación**

Una vez creado el cliente de servicio, puede invocar la operación de autenticación. Esta operación necesitará información sobre el usuario, como el nombre y la contraseña del usuario. Si el usuario no se autentica, se genera una excepción.

**Recuperar el contexto de autenticación**

Una vez que haya autenticado al usuario, puede crear un contexto basado en el usuario autenticado. A continuación, puede utilizar el contenido para invocar otros servicios de AEM Forms. Por ejemplo, puede utilizar el contexto para crear un `EncryptionServiceClient` y cifrar un documento PDF con una contraseña. Asegúrese de que el usuario autenticado tiene la función denominada `Services User` necesaria para invocar un servicio de AEM Forms.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API de User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Codificación de documentos PDF con contraseña](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Autenticar un usuario mediante la API de Java {#authenticate-a-user-using-the-java-api}

Autentique a un usuario mediante la API de servicio de Authentication Manager (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-usermanager-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente de AuthenticationManagerServices.

   Cree un objeto `AuthenticationManagerServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invoque la operación de autenticación.

   Invoque el método `AuthenticationManagerServiceClient` del objeto `authenticate` y pase los siguientes valores:

   * Un objeto `java.lang.String` que contiene el nombre del usuario.
   * Matriz de bytes (objeto `byte[]`) que contiene la contraseña del usuario. Puede obtener el objeto `byte[]` invocando el método `java.lang.String` del objeto `getBytes`.

   El método de autenticación devuelve un objeto `AuthResult`, que contiene información sobre el usuario autenticado.

1. Recupere el contexto de autenticación.

   Invoque el método `ServiceClientFactory` del objeto `getContext`, que devolverá un objeto `Context`.

   A continuación, invoque el método `Context` del objeto `initPrincipal` y pase el `AuthResult`.

### Autenticar un usuario mediante la API de servicio web {#authenticate-a-user-using-the-web-service-api}

Autentique a un usuario mediante la API de servicio de Authentication Manager (servicio web):

1. Incluir archivos de proyecto.

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL del administrador de autenticación. (Consulte [Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)).
   * Haga referencia al ensamblado cliente de Microsoft .NET. (Consulte &quot;Referencia al ensamblado de cliente .NET&quot; en [Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)).

1. Cree un cliente AuthenticationManagerService.

   Cree un objeto `AuthenticationManagerServiceService` utilizando el constructor de su clase proxy.

1. Invoque la operación de autenticación.

   Invoque el método `AuthenticationManagerServiceClient` del objeto `authenticate` y pase los siguientes valores:

   * Un objeto `string` que contiene el nombre del usuario
   * Matriz de bytes (objeto `byte[]`) que contiene la contraseña del usuario. Puede obtener el objeto `byte[]` convirtiendo un objeto `string` que contenga la contraseña en una matriz `byte[]` utilizando la lógica que se muestra en el ejemplo siguiente.
   * El valor devuelto será un objeto `AuthResult`, que se puede utilizar para recuperar información sobre el usuario. En el ejemplo siguiente, la información del usuario se recupera primero obteniendo el campo `AuthResult` del objeto `authenticatedUser` y, a continuación, obteniendo los campos `User` y `domainName` del objeto resultante.`canonicalName`

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Sincronización programática de usuarios {#programmatically-synchronizing-users}

Puede sincronizar los usuarios mediante programación mediante la API de administración de usuarios. Al sincronizar usuarios, está actualizando AEM Forms con los datos de usuario que se encuentran en su repositorio de usuarios. Por ejemplo, supongamos que agrega nuevos usuarios al repositorio de usuarios. Después de realizar una operación de sincronización, los nuevos usuarios se convierten en AEM usuarios de formularios. Además, los usuarios que ya no se encuentran en el repositorio de usuario se eliminan de AEM Forms.

El diagrama siguiente muestra la sincronización de AEM Forms con un repositorio de usuario.

![ps_ps_umauth_sync](assets/ps_ps_umauth_sync.png)

En la tabla siguiente se describen los pasos de este diagrama

<table>
 <thead>
  <tr>
   <th><p>Etapa</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Una aplicación cliente solicita que AEM Forms realice una operación de sincronización.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>AEM Forms realiza una operación de sincronización.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Se actualiza la información del usuario.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Un usuario puede ver la información actualizada del usuario. </p></td>
  </tr>
 </tbody>
</table>

### Resumen de los pasos {#summary_of_steps-6}

Para sincronizar los usuarios mediante programación, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente UserManagerUtilServiceClient.
1. Especifique el dominio de empresa.
1. Invoque la operación de autenticación.
1. Determinar si la operación de sincronización ha finalizado

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente utilizando Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un UserManagerUtilServiceClientClient**

Para poder sincronizar usuarios mediante programación, debe crear un objeto `UserManagerUtilServiceClient`.

**Especifique el dominio de empresa**

Antes de realizar una operación de sincronización utilizando la API de administración de usuarios, debe especificar el dominio de empresa al que pertenecen los usuarios. Puede especificar uno o varios dominios de empresa. Para poder realizar una operación de sincronización mediante programación, debe configurar un dominio de empresa mediante la Consola de administración. (Consulte [ayuda de administración](https://www.adobe.com/go/learn_aemforms_admin_63)).

**Invocar la operación de sincronización**

Después de especificar uno o varios dominios de empresa, puede realizar la operación de sincronización. El tiempo que tarda en realizar esta operación depende del número de registros de usuario que se encuentran en el repositorio de usuarios.

**Determinar si la operación de sincronización ha finalizado**

Después de realizar una operación de sincronización mediante programación, puede determinar si la operación ha finalizado.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API de User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Codificación de documentos PDF con contraseña](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Sincronización programática de usuarios con la API de Java {#programmatically-synchronizing-users-using-the-java-api}

Sincronizar usuarios mediante la API de administración de usuarios (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR del cliente, como adobe-usermanager-client.jar y adobe-usermanager-util-client.jar, en la ruta de clase de su proyecto Java.

1. Cree un cliente UserManagerUtilServiceClient.

   Cree un objeto `UserManagerUtilServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Especifique el dominio de empresa.

   * Invoque el método `UserManagerUtilServiceClient` del objeto `scheduleSynchronization` para iniciar la operación de sincronización del usuario.
   * Cree una instancia `java.util.Set` utilizando un constructor `HashSet`. Asegúrese de especificar `String` como tipo de datos. Esta instancia `Java.util.Set` almacena los nombres de dominio a los que se aplica la operación de sincronización.
   * Para que se agregue cada nombre de dominio, invoque el método add del objeto `java.util.Set` y pase el nombre de dominio.

1. Invocar la operación de sincronización.

   Invoque el método `ServiceClientFactory` del objeto `getContext`, que devolverá un objeto `Context`.

   A continuación, invoque el método `Context` del objeto `initPrincipal` y pase el `AuthResult`.

**Consulte también**

[Sincronización programática de usuarios](users.md#programmatically-synchronizing-users)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
