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
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '6243'
ht-degree: 0%

---


# Administración de usuarios {#managing-users}

**Acerca de la administración de usuarios**

Puede utilizar la API de administración de usuarios para crear aplicaciones cliente que puedan administrar funciones, permisos y entidades principales (que pueden ser usuarios o grupos), así como autenticar usuarios. La API de administración de usuarios consta de las siguientes API de AEM Forms:

* API del servicio Administrador de directorios
* API de servicio de Authentication Manager
* API de servicio de Administrador de autorización

La Administración de usuarios permite asignar, eliminar y determinar funciones y permisos. También permite asignar, eliminar y consulta dominios, usuarios y grupos. Finalmente, puede utilizar Administración de usuarios para autenticar a los usuarios.

En [Añadir usuarios](users.md#adding-users) comprenderá cómo agregar usuarios mediante programación. Esta sección utiliza la API de servicio del Administrador de directorios.

En [Eliminación de usuarios](users.md#deleting-users) comprenderá cómo eliminar usuarios mediante programación. Esta sección utiliza la API de servicio del Administrador de directorios.

En [Administración de usuarios y grupos](users.md#managing-users-and-groups) comprenderá la diferencia entre un usuario local y un usuario de directorio, y verá ejemplos de cómo utilizar las API de Java y de servicio Web para administrar mediante programación usuarios y grupos. Esta sección utiliza la API de servicio del Administrador de directorios.

En [Administración de roles y permisos](users.md#managing-roles-and-permissions) aprenderá sobre las funciones y los permisos del sistema y lo que puede hacer programáticamente para aumentarlos, y verá ejemplos de cómo utilizar las API de Java y de servicios Web para administrar mediante programación las funciones y los permisos. Esta sección utiliza la API de servicio del Administrador de directorios y la API de servicio del Administrador de autorización.

En [Autenticar usuarios](users.md#authenticating-users) verá ejemplos de cómo utilizar las API de Java y de servicio Web para autenticar usuarios mediante programación. Esta sección utiliza la API de servicio de Administrador de autorización.

**Explicación del proceso de autenticación**

La Administración de usuarios proporciona funcionalidad de autenticación integrada y también le permite conectarse con su propio proveedor de autenticación. Cuando la Administración de usuarios recibe una solicitud de autenticación (por ejemplo, un usuario intenta iniciar sesión), pasa la información del usuario al proveedor de autenticación para autenticarse. La Administración de usuarios recibe los resultados del proveedor de autenticación después de autenticar al usuario.

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
   <td><p>Un usuario intenta iniciar sesión en un servicio que invoque Administración de usuarios. El usuario especifica un nombre de usuario y una contraseña. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>La Administración de usuarios envía el nombre de usuario y la contraseña, así como la información de configuración, al proveedor de autenticación.</p></td>
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
>Si el huso horario del servidor es diferente del huso horario del cliente, al utilizar el WSDL para el servicio Generar PDF de AEM Forms en una pila SOAP nativa mediante un cliente .NET en un clúster de servidor de aplicaciones WebSphere, puede producirse el siguiente error de autenticación de Administración de usuarios:

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**Explicación de la administración de directorios**

La Administración de usuarios se empaqueta con un proveedor de servicio de directorio (DirectoryManagerService) que admite conexiones a directorios LDAP. Si su organización utiliza un repositorio que no sea LDAP para almacenar registros de usuarios, puede crear su propio proveedor de servicio de directorios que funcione con el repositorio.

Los proveedores de servicio de directorios recuperan registros de un almacén de usuarios a petición de la Administración de usuarios. La Administración de usuarios almacena en caché periódicamente los registros de usuarios y grupos de la base de datos para mejorar el rendimiento.

El proveedor de servicio de directorios puede utilizarse para sincronizar la base de datos de Administración de usuarios con el almacén de usuarios. Este paso garantiza que toda la información del directorio de usuarios y todos los registros de usuarios y grupos estén actualizados.

Además, DirectoryManagerService le permite crear y administrar dominios. Los dominios definen diferentes bases de usuario. El límite de un dominio se define generalmente según la forma en que se estructura su organización o cómo se configura el almacén de usuarios. Los dominios de Administración de usuarios proporcionan opciones de configuración que utilizan los proveedores de autenticación y los proveedores de servicio de directorio.

En el XML de configuración que la Administración de usuarios exporta, el nodo raíz que tiene el valor de atributo `Domains` contiene un elemento XML para cada dominio definido para la Administración de usuarios. Cada uno de estos elementos contiene otros elementos que definen aspectos del dominio asociados con proveedores de servicio específicos.

**Explicación de los valores de objectSID**

Al utilizar Active Directory, es importante comprender que un valor `objectSID` no es un atributo único en varios dominios. Este valor almacena el identificador de seguridad de un objeto. En un entorno de varios dominios (por ejemplo, un árbol de dominios), el valor `objectSID` puede ser diferente.

Un valor `objectSID` cambiaría si un objeto se movía de un dominio de Active Directory a otro dominio. Algunos objetos tienen el mismo valor `objectSID` en cualquier parte del dominio. Por ejemplo, grupos como BUILTIN\Administradores, BUILTIN\Power Users, etc., tendrían el mismo valor `objectSID` independientemente de los dominios. Estos valores `objectSID` son bien conocidos.

## Añadir usuarios {#adding-users}

Puede utilizar la API de servicio Administrador de directorios (Java y servicio Web) para agregar usuarios a AEM Forms mediante programación. Después de agregar un usuario, puede utilizarlo cuando realice una operación de servicio que requiera un usuario. Por ejemplo, puede asignar una tarea al nuevo usuario.

### Resumen de los pasos {#summary-of-steps}

Para agregar un usuario, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente DirectoryManagerService.
1. Defina la información del usuario.
1. Añada el usuario a AEM Forms.
1. Compruebe que se ha agregado al usuario.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

**Crear un cliente DirectoryManagerService**

Antes de realizar mediante programación una operación de servicio del Administrador de directorios, cree un cliente de API de servicio del Administrador de directorios.

**Definir información de usuario**

Cuando agregue un usuario nuevo mediante la API de servicio del Administrador de directorios, defina la información para ese usuario. Normalmente, cuando se agrega un usuario nuevo, se definen los valores siguientes:

* **Nombre** de dominio: Dominio al que pertenece el usuario (por ejemplo,  `DefaultDom`).
* **Valor** del identificador de usuario: El valor de identificador del usuario (por ejemplo,  `wblue`).
* **Tipo** principal: Tipo de usuario (por ejemplo, puede especificar  `USER)`.
* **Nombre** dado: Un nombre dado para el usuario (por ejemplo,  `Wendy`).
* **Apellido**: El nombre de la familia del usuario (por ejemplo,  `Blue)`.
* **Configuración regional**: Información de configuración regional para el usuario.

**Añadir el usuario a AEM Forms**

Después de definir la información del usuario, puede agregarlo a AEM Forms. Para agregar un usuario, invoque el método `DirectoryManagerServiceClient` del objeto `createLocalUser`.

**Verifique que se haya agregado al usuario**

Puede verificar que el usuario se agregó para asegurarse de que no se produjo ningún problema. Localice al nuevo usuario utilizando el valor de identificador de usuario.

**Consulte también**

[Añadir usuarios mediante la API de Java](users.md#add-users-using-the-java-api)

[Añadir usuarios mediante la API de servicio web](users.md#add-users-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Eliminación de usuarios](users.md#deleting-users)

### Añadir usuarios mediante la API de Java {#add-users-using-the-java-api}

Añadir usuarios mediante la API de servicio del Administrador de directorios (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-usermanager-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente DirectoryManagerServices.

   Cree un objeto `DirectoryManagerServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Defina la información del usuario.

   * Cree un objeto `UserImpl` utilizando su constructor.
   * Establezca el nombre del objeto principal invocando el método `UserImpl` del objeto `setDomainName`. Pase un valor de cadena que especifique el nombre de dominio.
   * Configure el tipo principal invocando el método `UserImpl` del objeto `setPrincipalType`. Pase un valor de cadena que especifique el tipo de usuario. Por ejemplo, puede especificar `USER`.
   * Establezca el valor del identificador de usuario invocando el método `UserImpl` del objeto `setUserid`. Pase un valor de cadena que especifique el valor del identificador de usuario. Por ejemplo, puede especificar `wblue`.
   * Establezca el nombre canónico invocando el método `UserImpl` del objeto `setCanonicalName`. Pase un valor de cadena que especifique el nombre canónico del usuario. Por ejemplo, puede especificar `wblue`.
   * Establezca el nombre dado invocando el método `UserImpl` del objeto `setGivenName`. Pase un valor de cadena que especifique el nombre dado del usuario. Por ejemplo, puede especificar `Wendy`.
   * Establezca el nombre de familia invocando el método `UserImpl` del objeto `setFamilyName`. Pase un valor de cadena que especifique el nombre de familia del usuario. Por ejemplo, puede especificar `Blue`.

   >[!NOTE]
   >
   >Invoque un método que pertenezca al objeto `UserImpl` para establecer otros valores. Por ejemplo, puede establecer el valor de configuración regional invocando el método `UserImpl` del objeto `setLocale`.

1. Añada el usuario a AEM Forms.

   Invoque el método `DirectoryManagerServiceClient` del objeto `createLocalUser` y pase los siguientes valores:

   * El objeto `UserImpl` que representa al nuevo usuario
   * Un valor de cadena que representa la contraseña del usuario

   El método `createLocalUser` devuelve un valor de cadena que especifica el valor del identificador de usuario local.

1. Compruebe que se ha agregado al usuario.

   * Cree un objeto `PrincipalSearchFilter` utilizando su constructor.
   * Establezca el valor del identificador de usuario invocando el método `PrincipalSearchFilter` del objeto `setUserId`. Pase un valor de cadena que represente el valor del identificador de usuario.
   * Invoque el método `DirectoryManagerServiceClient` del objeto `findPrincipals` y pase el objeto `PrincipalSearchFilter`. Este método devuelve una instancia `java.util.List`, donde cada elemento es un objeto `User`. Repita la instancia `java.util.List` para localizar al usuario.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Inicio rápido (modo SOAP): Añadir usuarios mediante la API de Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Añadir usuarios mediante la API de servicio Web {#add-users-using-the-web-service-api}

Añadir usuarios mediante la API de servicio del Administrador de directorios (servicio Web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL para la referencia del servicio: `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente DirectoryManagerService.

   * Cree un objeto `DirectoryManagerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `DirectoryManagerServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio. Asegúrese de especificar `?blob=mtom`.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `DirectoryManagerServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Defina la información del usuario.

   * Cree un objeto `UserImpl` utilizando su constructor.
   * Defina el nombre del objeto principal asignando un valor de cadena al campo `UserImpl` del objeto `domainName`.
   * Defina el tipo principal asignando un valor de cadena al campo `UserImpl` del objeto `principalType`. Por ejemplo, puede especificar `USER`.
   * Establezca el valor del identificador de usuario asignando un valor de cadena al campo `UserImpl` del objeto `userid`.
   * Establezca el valor de nombre canónico asignando un valor de cadena al campo `UserImpl` del objeto `canonicalName`.
   * Establezca el valor de nombre determinado asignando un valor de cadena al campo `UserImpl` del objeto `givenName`.
   * Establezca el valor del nombre de familia asignando un valor de cadena al campo `UserImpl` del objeto `familyName`.

1. Añada el usuario a AEM Forms.

   Invoque el método `DirectoryManagerServiceClient` del objeto `createLocalUser` y pase los siguientes valores:

   * El objeto `UserImpl` que representa al nuevo usuario
   * Un valor de cadena que representa la contraseña del usuario

   El método `createLocalUser` devuelve un valor de cadena que especifica el valor del identificador de usuario local.

1. Compruebe que se ha agregado al usuario.

   * Cree un objeto `PrincipalSearchFilter` utilizando su constructor.
   * Establezca el valor del identificador de usuario del usuario asignando un valor de cadena que represente el valor del identificador de usuario al campo `PrincipalSearchFilter` del objeto `userId`.
   * Invoque el método `DirectoryManagerServiceClient` del objeto `findPrincipals` y pase el objeto `PrincipalSearchFilter`. Este método devuelve un objeto de colección `MyArrayOfUser`, donde cada elemento es un objeto `User`. Repita la colección `MyArrayOfUser` para localizar al usuario.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminación de usuarios {#deleting-users}

Puede utilizar la API de servicio Administrador de directorios (Java y servicio Web) para eliminar usuarios de AEM Forms mediante programación. Después de eliminar un usuario, ya no se puede usar para realizar una operación de servicio que requiera un usuario. Por ejemplo, no se puede asignar una tarea a un usuario eliminado.

### Resumen de los pasos {#summary_of_steps-1}

Para eliminar un usuario, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente DirectoryManagerService.
1. Especifique el usuario que desea eliminar.
1. Elimine el usuario de AEM Forms.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

**Crear un cliente DirectoryManagerService**

Antes de realizar mediante programación una operación de API de servicio de Directory Manager, cree un cliente de servicio de Directory Manager.

**Especifique el usuario que desea eliminar**

Puede especificar un usuario para eliminarlo mediante el valor de identificador del usuario.

**Eliminar el usuario de AEM Forms**

Para eliminar un usuario, invoque el método `DirectoryManagerServiceClient` del objeto `deleteLocalUser`.

**Consulte también**

[Eliminar usuarios mediante la API de Java](users.md#delete-users-using-the-java-api)

[Eliminar usuarios mediante la API de servicio Web](users.md#delete-users-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Añadir usuarios](users.md#adding-users)

### Eliminar usuarios mediante la API de Java {#delete-users-using-the-java-api}

Eliminar usuarios mediante la API de servicio del Administrador de directorios (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-usermanager-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente DirectoryManagerService.

   Cree un objeto `DirectoryManagerServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Especifique el usuario que desea eliminar.

   * Cree un objeto `PrincipalSearchFilter` utilizando su constructor.
   * Establezca el valor del identificador de usuario invocando el método `PrincipalSearchFilter` del objeto `setUserId`. Pase un valor de cadena que represente el valor del identificador de usuario.
   * Invoque el método `DirectoryManagerServiceClient` del objeto `findPrincipals` y pase el objeto `PrincipalSearchFilter`. Este método devuelve una instancia `java.util.List`, donde cada elemento es un objeto `User`. Repita la instancia `java.util.List` para localizar al usuario que desea eliminar.

1. Elimine el usuario de AEM Forms.

   Invoque el método `DirectoryManagerServiceClient` del objeto `deleteLocalUser` y pase el valor del campo `User` del objeto `oid`. Invocar el método `User` del objeto `getOid`. Utilice el objeto `User` recuperado de la instancia `java.util.List`.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Inicio rápido (modo EJB): Eliminación de usuarios mediante la API de Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Inicio rápido (modo SOAP): Eliminación de usuarios mediante la API de Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminar usuarios mediante la API de servicio Web {#delete-users-using-the-web-service-api}

Eliminar usuarios mediante la API de servicio del Administrador de directorios (servicio Web):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-usermanager-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente DirectoryManagerService.

   * Cree un objeto `DirectoryManagerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `DirectoryManagerServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio. Asegúrese de especificar `blob=mtom.`
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `DirectoryManagerServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Especifique el usuario que desea eliminar.

   * Cree un objeto `PrincipalSearchFilter` utilizando su constructor.
   * Establezca el valor del identificador de usuario asignando un valor de cadena al campo `PrincipalSearchFilter` del objeto `userId`.
   * Invoque el método `DirectoryManagerServiceClient` del objeto `findPrincipals` y pase el objeto `PrincipalSearchFilter`. Este método devuelve un objeto de colección `MyArrayOfUser`, donde cada elemento es un objeto `User`. Repita la colección `MyArrayOfUser` para localizar al usuario. El objeto `User` recuperado del objeto de colección `MyArrayOfUser` se utiliza para eliminar al usuario.

1. Elimine el usuario de AEM Forms.

   Elimine el usuario pasando el valor de campo `User` del objeto `oid` al método `DirectoryManagerServiceClient` del objeto `deleteLocalUser`.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Creación de grupos {#creating-groups}

Puede utilizar la API de servicio Administrador de directorios (Java y servicio Web) para crear grupos de AEM Forms mediante programación. Después de crear un grupo, puede utilizarlo para realizar una operación de servicio que requiera un grupo. Por ejemplo, puede asignar un usuario al nuevo grupo. (Consulte [Administración de usuarios y grupos](users.md#managing-users-and-groups)).

### Resumen de los pasos {#summary_of_steps-2}

Para crear un grupo, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente DirectoryManagerService.
1. Determine que el grupo no existe.
1. Cree el grupo.
1. Realice una acción con el grupo.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms se implementa en JBoss)
* jbossall-client.jar (obligatorio si AEM Forms se implementa en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente DirectoryManagerService**

Antes de realizar mediante programación una operación de servicio del Administrador de directorios, cree un cliente de API de servicio del Administrador de directorios.

**Determinar si el grupo existe**

Al crear un grupo, asegúrese de que no existe en el mismo dominio. Es decir, dos grupos no pueden tener el mismo nombre dentro del mismo dominio. Para realizar esta tarea, realice una búsqueda y filtre los resultados de búsqueda en función de dos valores. Establezca el tipo principal en `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` para garantizar que solo se devuelvan los grupos. Además, asegúrese de especificar el nombre de dominio.

**Crear el grupo**

Después de determinar que el grupo no existe en el dominio, cree el grupo y especifique los atributos siguientes:

* **CommonName**: Nombre del grupo.
* **Dominio**: Dominio en el que se agrega el grupo.
* **Descripción**: Una descripción del grupo.

**Realizar una acción con el grupo**

Después de crear un grupo, puede realizar una acción utilizando el grupo. Por ejemplo, puede agregar un usuario al grupo. Para agregar un usuario a un grupo, recupere el valor de identificador único del usuario y del grupo. Pase estos valores al método `addPrincipalToLocalGroup`.

**Consulte también**

[Creación de grupos mediante la API de Java](users.md#create-groups-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Añadir usuarios](users.md#adding-users)

[Eliminación de usuarios](users.md#deleting-users)

### Crear grupos mediante la API de Java {#create-groups-using-the-java-api}

Cree un grupo mediante la API de servicio del Administrador de directorios (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-usermanager-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente DirectoryManagerService.

   Cree un objeto `DirectoryManagerServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Determine si el grupo existe.

   * Cree un objeto `PrincipalSearchFilter` utilizando su constructor.
   * Configure el tipo principal invocando el objeto `PrincipalSearchFilter` del objeto `setPrincipalType`. Pase el valor `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`.
   * Establezca el dominio invocando el objeto `PrincipalSearchFilter` del objeto `setSpecificDomainName`. Pase un valor de cadena que especifique el nombre de dominio.
   * Para encontrar un grupo, invoque el método `DirectoryManagerServiceClient` del objeto `findPrincipals` (un principal puede ser un grupo). Pase el objeto `PrincipalSearchFilter` que especifica el tipo principal y el nombre de dominio. Este método devuelve una instancia `java.util.List` donde cada elemento es una instancia `Group`. Cada instancia de grupo se ajusta al filtro especificado mediante el objeto `PrincipalSearchFilter`.
   * Repita la instancia `java.util.List`. Para cada elemento, recupere el nombre del grupo. Asegúrese de que el nombre del grupo no es igual al nuevo nombre del grupo.

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
   * Añada un usuario al grupo invocando el método `DirectoryManagerServiceClient` del objeto `addPrincipalToLocalGroup`. Pase el valor devuelto del método `User` del objeto `getOid`. Pase el valor devuelto del método `Group` del objeto `getOid` (utilice la instancia `Group` que representa al nuevo grupo).

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Administración de usuarios y grupos {#managing-users-and-groups}

En este tema se describe cómo puede utilizar (Java) para asignar, eliminar y consulta mediante programación a dominios, usuarios y grupos.

>[!NOTE]
>
>Al configurar un dominio, debe establecer el identificador único para grupos y usuarios. El atributo que se elija no sólo debe ser único dentro del entorno LDAP, sino que también debe ser inmutable y no cambiará dentro del directorio. Este atributo también debe ser de un tipo de datos de cadena simple (la única excepción permitida actualmente para Active Directory 2000/2003 es `"objectsid"`, que es un valor binario). El atributo de Novell eDirectory `"GUID"`, por ejemplo, no es un tipo de datos de cadena simple y, por lo tanto, no funcionará.

* Para Active Directory, utilice `"objectsid"`.
* Para SunOne, utilice `"nsuniqueid"`.

>[!NOTE]
>
>No se admite la creación de varios usuarios y grupos locales mientras hay una sincronización de directorio LDAP en curso. Intentar este proceso puede provocar errores.

### Resumen de los pasos {#summary_of_steps-3}

Para administrar usuarios y grupos, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente DirectoryManagerService.
1. Invoque las operaciones de usuario o grupo correspondientes.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Crear un cliente DirectoryManagerService**

Para poder realizar mediante programación una operación de servicio del Administrador de directorios, debe crear un cliente de servicio del Administrador de directorios. Con la API de Java esto se logra creando un objeto `DirectoryManagerServiceClient`. Con la API de servicio Web esto se logra creando un objeto `DirectoryManagerServiceService`.

**Invocar las operaciones de usuario o grupo correspondientes**

Una vez creado el cliente de servicio, puede invocar las operaciones de administración de usuarios o grupos. El cliente de servicios permite asignar, eliminar y consulta de dominios, usuarios y grupos. Tenga en cuenta que es posible agregar un principal de directorio o un principal local a un grupo local, pero no es posible agregar un principal local a un grupo de directorios.

**Consulte también**

[Administración de usuarios y grupos mediante la API de Java](users.md#managing-users-and-groups-using-the-java-api)

[Administración de usuarios y grupos mediante la API de servicio web](users.md#managing-users-and-groups-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API del Administrador de usuarios](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Administración de usuarios y grupos mediante la API de Java {#managing-users-and-groups-using-the-java-api}

Para administrar mediante programación usuarios, grupos y dominios mediante (Java), realice las siguientes tareas:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-usermanager-client.jar, en la ruta de clases del proyecto Java. Para obtener información sobre la ubicación de estos archivos, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Cree un cliente DirectoryManagerService.

   Cree un objeto `DirectoryManagerServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión. Para obtener más información, consulte [Configuración de propiedades de conexión ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*.*

1. Invoque las operaciones de usuario o grupo correspondientes.

   Para encontrar un usuario o grupo, invoque uno de los métodos del objeto `DirectoryManagerServiceClient` para buscar entidades principales (ya que una entidad de seguridad puede ser un usuario o un grupo). En el ejemplo siguiente, se llama al método `findPrincipals` mediante un filtro de búsqueda (un objeto `PrincipalSearchFilter`).

   Dado que el valor devuelto en este caso es un objeto `java.util.List` que contiene `Principal`, repita el resultado y convierta los objetos `Principal` en objetos `User` u `Group`.

   Con el objeto resultante `User` o `Group` (que ambos heredan de la interfaz `Principal`), recupere la información que necesita en sus flujos de trabajo. Por ejemplo, el nombre de dominio y los valores de nombre canónicos, en combinación, identifican de forma exclusiva un principal. Estos se recuperan invocando los métodos `Principal` y `getDomainName` del objeto `getCanonicalName`, respectivamente.

   Para eliminar un usuario local, invoque el método `DirectoryManagerServiceClient` del objeto `deleteLocalUser` y pase el identificador del usuario.

   Para eliminar un grupo local, invoque el método `DirectoryManagerServiceClient` del objeto `deleteLocalGroup` y pase el identificador del grupo.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Administración de usuarios y grupos mediante la API de servicio Web {#managing-users-and-groups-using-the-web-service-api}

Para administrar mediante programación usuarios, grupos y dominios mediante la API de servicio del Administrador de directorios (servicio Web), lleve a cabo las siguientes tareas:

1. Incluir archivos de proyecto.

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el WSDL del Administrador de directorios. (Consulte [Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)).
   * Haga referencia al ensamblado de cliente de Microsoft .NET. (Consulte [Creación de un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Cree un cliente DirectoryManagerService.

   Cree un objeto `DirectoryManagerServiceService` utilizando el constructor de la clase proxy.

1. Invoque las operaciones de usuario o grupo correspondientes.

   Para encontrar un usuario o grupo, invoque uno de los métodos del objeto `DirectoryManagerServiceService` para buscar entidades principales (ya que una entidad de seguridad puede ser un usuario o un grupo). En el ejemplo siguiente, se llama al método `findPrincipalsWithFilter` mediante un filtro de búsqueda (un objeto `PrincipalSearchFilter`). Cuando se utiliza un objeto `PrincipalSearchFilter`, los principales locales solo se devuelven si la propiedad `isLocal` se establece en `true`. Este comportamiento es diferente al que se produciría con la API de Java.

   >[!NOTE]
   >
   >Si no se especifica el número máximo de resultados en el filtro de búsqueda (a través del campo `PrincipalSearchFilter.resultsMax`), se devolverá un máximo de 1000 resultados. Este comportamiento es diferente al que se produce con la API de Java, en la que 10 resultados es el máximo predeterminado. Además, los métodos de búsqueda como `findGroupMembers` no arrojan ningún resultado a menos que se especifique el número máximo de resultados en el filtro de búsqueda (por ejemplo, a través del campo `GroupMembershipSearchFilter.resultsMax`). Esto se aplica a todos los filtros de búsqueda que heredan de la clase `GenericSearchFilter`. Para obtener más información, consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   Dado que el valor devuelto en este caso es un objeto `object[]` que contiene `Principal`, repita el resultado y convierta los objetos `Principal` en objetos `User` u `Group`.

   Con el objeto resultante `User` o `Group` (que ambos heredan de la interfaz `Principal`), recupere la información que necesita en sus flujos de trabajo. Por ejemplo, el nombre de dominio y los valores de nombre canónicos, en combinación, identifican de forma exclusiva un principal. Estos se recuperan invocando los campos `Principal` `domainName` y `canonicalName` del objeto, respectivamente.

   Para eliminar un usuario local, invoque el método `DirectoryManagerServiceService` del objeto `deleteLocalUser` y pase el identificador del usuario.

   Para eliminar un grupo local, invoque el método `DirectoryManagerServiceService` del objeto `deleteLocalGroup` y pase el identificador del grupo.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Administración de roles y permisos {#managing-roles-and-permissions}

En este tema se describe cómo puede utilizar la API de servicio de Administrador de autorización (Java) para asignar, eliminar y determinar mediante programación funciones y permisos.

En AEM Forms, una *función* es un grupo de permisos para acceder a uno o más recursos a nivel de sistema. Estos permisos se crean a través de Administración de usuarios y los componentes del servicio los aplican. Por ejemplo, un administrador podría asignar la función &quot;Autor de conjuntos de políticas&quot; a un grupo de usuarios. El Rights Management permitiría entonces a los usuarios de ese grupo con esa función crear conjuntos de políticas a través de la consola de administración.

Existen dos tipos de funciones: *funciones predeterminadas* y *funciones personalizadas*. Las funciones predeterminadas (*funciones del sistema)* ya residen en AEM Forms. Se da por hecho que el administrador no puede eliminar ni modificar las funciones predeterminadas, por lo que son inmutables. Las funciones personalizadas creadas por el administrador, que posteriormente pueden modificarlas o eliminarlas, son por lo tanto mutables.

Las funciones facilitan la administración de permisos. Cuando se asigna una función a una entidad de seguridad, se asigna automáticamente un conjunto de permisos a esa entidad de seguridad y todas las decisiones específicas relacionadas con el acceso para la entidad de seguridad se basan en ese conjunto general de permisos asignados.

### Resumen de los pasos {#summary_of_steps-4}

Para administrar funciones y permisos, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente AuthorizationManagerService.
1. Invocar la función o las operaciones de permisos correspondientes.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Crear un cliente AuthorizationManagerService**

Para poder realizar mediante programación una operación AuthorizationManagerService de Administración de usuarios, debe crear un cliente AuthorizationManagerService. Con la API de Java esto se logra creando un objeto `AuthorizationManagerServiceClient`.

**Invocar la función o las operaciones de permisos correspondientes**

Una vez creado el cliente de servicios, puede invocar la función o las operaciones de permisos. El cliente del servicio le permite asignar, eliminar y determinar funciones y permisos.

**Consulte también**

[Administración de funciones y permisos mediante la API de Java](users.md#managing-roles-and-permissions-using-the-java-api)

[Administración de funciones y permisos mediante la API de servicio web](users.md#managing-roles-and-permissions-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API del Administrador de usuarios](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Administración de funciones y permisos mediante la API de Java {#managing-roles-and-permissions-using-the-java-api}

Para administrar funciones y permisos mediante la API de servicio de Administrador de autorización (Java), lleve a cabo las siguientes tareas:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-usermanager-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente AuthorizationManagerService.

   Cree un objeto `AuthorizationManagerServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invocar la función o las operaciones de permisos correspondientes.

   Para asignar una función a un principal, invoque el método `AuthorizationManagerServiceClient` del objeto `assignRole` y pase los valores siguientes:

   * Un objeto `java.lang.String` que contiene el identificador de función
   * Matriz de objetos `java.lang.String` que contiene los identificadores principales.

   Para quitar una función de un principal, invoque el método `AuthorizationManagerServiceClient` del objeto `unassignRole` y pase los valores siguientes:

   * Un objeto `java.lang.String` que contiene el identificador de función.
   * Matriz de objetos `java.lang.String` que contiene los identificadores principales.


**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Inicio rápido (modo SOAP): Administración de funciones y permisos mediante la API de Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Administración de funciones y permisos mediante la API de servicio Web {#managing-roles-and-permissions-using-the-web-service-api}

Administre funciones y permisos mediante la API de servicio de Administrador de autorización (servicio Web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición WSDL: `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que aloja AEM Forms.

1. Cree un cliente AuthorizationManagerService.

   * Cree un objeto `AuthorizationManagerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `AuthorizationManagerServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`). No es necesario usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `AuthorizationManagerServiceClient.Endpoint.Binding`. Convierta el valor devuelto a `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utilice MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM al campo `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Invocar la función o las operaciones de permisos correspondientes.

   Para asignar una función a un principal, invoque el método `AuthorizationManagerServiceClient` del objeto `assignRole` y pase los valores siguientes:

   * Un objeto `string` que contiene el identificador de función
   * Un objeto `MyArrayOf_xsd_string` que contiene los identificadores principales.

   Para quitar una función de un principal, invoque el método `AuthorizationManagerServiceService` del objeto `unassignRole` y pase los valores siguientes:

   * Un objeto `string` que contiene el identificador de función.
   * Matriz de objetos `string` que contiene los identificadores principales.


**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Autenticar usuarios {#authenticating-users}

En este tema se describe cómo puede utilizar la API de servicio de Authentication Manager (Java) para habilitar las aplicaciones cliente para autenticar usuarios mediante programación.

Es posible que se requiera la autenticación del usuario para interactuar con una base de datos empresarial u otros repositorios empresariales que almacenen datos seguros.

Considere, por ejemplo, un escenario en el que un usuario introduce un nombre de usuario y una contraseña en una página web y envía los valores a un servidor de aplicaciones J2EE con Forms. Una aplicación personalizada de Forms puede autenticar al usuario con el servicio Authentication Manager.

Si la autenticación se realiza correctamente, la aplicación accede a una base de datos empresarial segura. De lo contrario, se envía un mensaje al usuario en el que se indica que no es un usuario autorizado.

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
   <td><p>Las credenciales de usuario se autentican con el servicio Authentication Manager. Si las credenciales de usuario son válidas, el flujo de trabajo continúa con el paso 3. De lo contrario, se envía un mensaje al usuario en el que se indica que no es un usuario autorizado.</p></td>
  </tr>
  <tr>
   <td><p>1</p></td>
   <td><p>La información del usuario y el diseño de formulario se recuperan de una base de datos empresarial segura. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>La información del usuario se combina con un diseño de formulario y éste se procesa para el usuario. </p></td>
  </tr>
 </tbody>
</table>

### Resumen de los pasos {#summary_of_steps-5}

Para autenticar a un usuario mediante programación, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente AuthenticationManagerService.
1. Invocar la operación de autenticación.
1. Si es necesario, recupere el contexto para que la aplicación cliente pueda reenviarlo a otro servicio de AEM Forms para su autenticación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Crear un cliente AuthenticationManagerService**

Para poder autenticar a un usuario mediante programación, debe crear un cliente AuthenticationManagerService. Al utilizar la API de Java, cree un objeto `AuthenticationManagerServiceClient`.

**Invocar la operación de autenticación**

Una vez creado el cliente de servicio, puede invocar la operación de autenticación. Esta operación necesitará información sobre el usuario, como el nombre y la contraseña del usuario. Si el usuario no se autentica, se genera una excepción.

**Recuperar el contexto de autenticación**

Una vez autenticado el usuario, puede crear un contexto basado en el usuario autenticado. A continuación, puede utilizar el contenido para invocar otros servicios de AEM Forms. Por ejemplo, puede utilizar el contexto para crear un `EncryptionServiceClient` y cifrar un documento PDF con una contraseña. Asegúrese de que el usuario autenticado tiene la función `Services User` que se requiere para invocar un servicio de AEM Forms.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API del Administrador de usuarios](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Cifrado de Documentos PDF con contraseña](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Autentique a un usuario mediante la API de Java {#authenticate-a-user-using-the-java-api}

Autentique a un usuario mediante la API de servicio de Authentication Manager (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-usermanager-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente AuthenticationManagerServices.

   Cree un objeto `AuthenticationManagerServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invocar la operación de autenticación.

   Invoque el método `AuthenticationManagerServiceClient` del objeto `authenticate` y pase los siguientes valores:

   * Un objeto `java.lang.String` que contiene el nombre del usuario.
   * Matriz de bytes (un objeto `byte[]`) que contiene la contraseña del usuario. Puede obtener el objeto `byte[]` invocando el método `java.lang.String` del objeto `getBytes`.

   El método authentication devuelve un objeto `AuthResult`, que contiene información sobre el usuario autenticado.

1. Recupere el contexto de autenticación.

   Invoque el método `ServiceClientFactory` del objeto `getContext`, que devolverá un objeto `Context`.

   A continuación, invoque el método `Context` del objeto `initPrincipal` y pase el `AuthResult`.

### Autenticar a un usuario mediante la API de servicio Web {#authenticate-a-user-using-the-web-service-api}

Autentique a un usuario mediante la API de servicio de Authentication Manager (servicio Web):

1. Incluir archivos de proyecto.

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el WSDL del administrador de autenticación. (Consulte [Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)).
   * Haga referencia al ensamblado de cliente de Microsoft .NET. (Consulte &quot;Referencia al ensamblado de cliente .NET&quot; en [Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)

1. Cree un cliente AuthenticationManagerService.

   Cree un objeto `AuthenticationManagerServiceService` utilizando el constructor de la clase proxy.

1. Invocar la operación de autenticación.

   Invoque el método `AuthenticationManagerServiceClient` del objeto `authenticate` y pase los siguientes valores:

   * Un objeto `string` que contiene el nombre del usuario
   * Matriz de bytes (un objeto `byte[]`) que contiene la contraseña del usuario. Puede obtener el objeto `byte[]` convirtiendo un objeto `string` que contenga la contraseña en una matriz `byte[]` utilizando la lógica mostrada en el ejemplo siguiente.
   * El valor devuelto será un objeto `AuthResult`, que puede utilizarse para recuperar información sobre el usuario. En el ejemplo siguiente, la información del usuario se recupera primero obteniendo el campo `AuthResult` del objeto `authenticatedUser` y obteniendo posteriormente los campos `User` y `domainName` del objeto resultante.`canonicalName`

**Consulte también**

[Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Sincronización programada de usuarios {#programmatically-synchronizing-users}

Puede sincronizar usuarios mediante programación mediante la API de administración de usuarios. Al sincronizar usuarios, está actualizando AEM Forms con los datos de usuario que se encuentran en el repositorio de usuarios. Por ejemplo, supongamos que agrega usuarios nuevos al repositorio de usuarios. Después de realizar una operación de sincronización, los nuevos usuarios se convierten en usuarios AEM formularios. Asimismo, los usuarios que ya no se encuentren en el repositorio del usuario se eliminarán de AEM Forms.

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
   <td><p>1</p></td>
   <td><p>Se actualiza la información del usuario.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Un usuario puede realizar la vista de la información de usuario actualizada. </p></td>
  </tr>
 </tbody>
</table>

### Resumen de los pasos {#summary_of_steps-6}

Para sincronizar usuarios mediante programación, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente UserManagerUtilServiceClient.
1. Especifique el dominio de empresa.
1. Invocar la operación de autenticación.
1. Determinar si la operación de sincronización ha finalizado

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Crear un cliente UserManagerUtilServiceClient**

Para poder sincronizar usuarios mediante programación, debe crear un objeto `UserManagerUtilServiceClient`.

**Especificar el dominio de empresa**

Antes de realizar una operación de sincronización mediante la API de administración de usuarios, debe especificar el dominio de empresa al que pertenecen los usuarios. Puede especificar uno o varios dominios de empresa. Antes de realizar una operación de sincronización mediante programación, debe configurar un dominio de empresa mediante la Consola de administración. (Consulte [ayuda de administración](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Invocar la operación de sincronización**

Después de especificar uno o varios dominios de empresa, puede realizar la operación de sincronización. El tiempo que tarda en realizar esta operación depende del número de registros de usuario que se encuentren en el repositorio del usuario.

**Determinar si la operación de sincronización ha finalizado**

Después de realizar una operación de sincronización mediante programación, puede determinar si la operación ha finalizado.

**Consulte también**

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API del Administrador de usuarios](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Cifrado de Documentos PDF con contraseña](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Sincronización programada de usuarios mediante la API de Java {#programmatically-synchronizing-users-using-the-java-api}

Sincronizar usuarios mediante la API de administración de usuarios (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-usermanager-client.jar y adobe-usermanager-util-client.jar, en la ruta de clases del proyecto Java.

1. Cree un cliente UserManagerUtilServiceClient.

   Cree un objeto `UserManagerUtilServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Especifique el dominio de empresa.

   * Invocar el método `UserManagerUtilServiceClient` del objeto `scheduleSynchronization` para inicio de la operación de sincronización del usuario.
   * Cree una instancia `java.util.Set` mediante un constructor `HashSet`. Asegúrese de especificar `String` como tipo de datos. Esta instancia `Java.util.Set` almacena los nombres de dominio a los que se aplica la operación de sincronización.
   * Para cada nombre de dominio que agregar, invoque el método add del objeto `java.util.Set` y pase el nombre de dominio.

1. Invocar la operación de sincronización.

   Invoque el método `ServiceClientFactory` del objeto `getContext`, que devolverá un objeto `Context`.

   A continuación, invoque el método `Context` del objeto `initPrincipal` y pase el `AuthResult`.

**Consulte también**

[Sincronización programada de usuarios](users.md#programmatically-synchronizing-users)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
