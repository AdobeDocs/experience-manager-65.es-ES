---
title: Configurar proveedores de autenticación
seo-title: Configuring authentication providers
description: Agregue, edite o elimine proveedores de autenticación, cambie la configuración de autenticación y lea acerca del aprovisionamiento Just-In-Time de los usuarios.
seo-description: Add, edit, or delete authentication providers, change authentication settings, and read about just-in-time provisioning of users.
uuid: 90e7690b-1ce0-4604-b58f-6dca4f2372cf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 31dd8db3-ddac-429e-82f8-8c5dc4ffc186
exl-id: d72a3977-1423-49e0-899b-234bb76be378
source-git-commit: 1cdd15800548362ccdd9e70847d9df8ce93ee06e
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 0%

---

# Configurar proveedores de autenticación {#configuring-authentication-providers}

Los dominios híbridos requieren al menos un proveedor de autenticación y los dominios empresariales requieren al menos un proveedor de autenticación o de directorio.

Si habilita el SSO mediante SPNEGO, agregue un proveedor de autenticación Kerberos con SPNEGO habilitado y un proveedor LDAP como copia de seguridad. Esta configuración habilita la autenticación de usuarios con un identificador de usuario y una contraseña si SPNEGO no funciona. (Consulte [Habilitar SSO con SPNEGO](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego).)

## Agregar un proveedor de autenticación {#add-an-authentication-provider}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en un dominio existente de la lista. Si agrega autenticación para un nuevo dominio, consulte [Agregar un dominio de empresa](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain) o [Añadir un dominio híbrido](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain).
1. Haga clic en Agregar autenticación y, en la lista Proveedor de autenticación, seleccione un proveedor, según el mecanismo de autenticación que utilice su organización.
1. Proporcione la información adicional que necesite en la página. (Consulte [Configuración de autenticación](configuring-authentication-providers.md#authentication-settings).)
1. (Opcional) Haga clic en Probar para probar la configuración.
1. Haga clic en Aceptar y vuelva a hacer clic en Aceptar.

## Editar un proveedor de autenticación existente {#edit-an-existing-authentication-provider}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el dominio correspondiente en la lista.
1. En la página que aparece, seleccione el proveedor de autenticación adecuado en la lista y realice los cambios necesarios. (Consulte [Configuración de autenticación](configuring-authentication-providers.md#authentication-settings).)
1. Haga clic en Aceptar.

## Eliminar un proveedor de autenticación {#delete-an-authentication-provider}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el dominio correspondiente en la lista.
1. Seleccione las casillas de verificación de los proveedores de autenticación que desea eliminar y haga clic en Eliminar.
1. Haga clic en Aceptar en la página de confirmación que aparece y vuelva a hacer clic en Aceptar.

## Configuración de autenticación {#authentication-settings}

Las siguientes configuraciones están disponibles, según el tipo de dominio y el tipo de autenticación que elija.

### Configuración de LDAP {#ldap-settings}

Si está configurando la autenticación para un dominio híbrido o de empresa y selecciona Autenticación LDAP, puede elegir utilizar el servidor LDAP especificado en la configuración del directorio o elegir otro servidor LDAP que utilizar para la autenticación. Si elige un servidor diferente, los usuarios deben existir en ambos servidores LDAP.

Para utilizar el servidor LDAP especificado en la configuración de directorio, seleccione LDAP como proveedor de autenticación y haga clic en Aceptar.

Para utilizar un servidor LDAP diferente para realizar la autenticación, seleccione LDAP como proveedor de autenticación y active la casilla Autenticación LDAP personalizada. Se muestran las siguientes opciones de configuración.

**Servidor:** (Obligatorio) Nombre de dominio completo (FQDN) del servidor de directorio. Por ejemplo, para un equipo llamado x en la red example.com, el FQDN es x.example.com. Se puede usar una dirección IP en lugar del nombre de servidor FQDN.

**Puerto:** (Obligatorio) El puerto que utiliza el servidor de directorios. Normalmente, 389 o 636 si se utiliza el protocolo Secure Sockets Layer (SSL) para enviar información de autenticación a través de la red.

**SSL:** (Obligatorio) Especifica si el servidor de directorios utiliza SSL al enviar datos a través de la red. El valor predeterminado es No. Cuando se establece en Yes, el entorno de tiempo de ejecución de Java™ (JRE) del servidor de aplicaciones debe confiar en el certificado del servidor LDAP correspondiente.

**Enlace** (Obligatorio) Especifica cómo acceder al directorio.

**Anónimo:** No se requiere nombre de usuario ni contraseña.

**Usuario:** Se requiere autenticación. En el cuadro Nombre, especifique el nombre del registro de usuario que puede acceder al directorio. Se recomienda introducir el nombre distinguido completo (DN) de la cuenta de usuario, como cn=Jane Doe, ou=user, dc=can, dc=com. En el cuadro Contraseña, especifique la contraseña asociada. Esta configuración es necesaria cuando selecciona Usuario como opción de enlace.

**Recuperar DN Base:** (No obligatorio) Recupera los DN base y los muestra en la lista desplegable. Esta configuración es útil cuando tiene varios DN base y necesita seleccionar un valor.

**DN base:** (Obligatorio) Se utiliza como punto de partida para sincronizar usuarios y grupos desde la jerarquía LDAP. Es mejor especificar un DN base en el nivel inferior de la jerarquía que incluya todos los usuarios y grupos que necesitan sincronizarse para los servicios. No incluya el DN del usuario en esta configuración. Para sincronizar un usuario en particular, utilice la configuración Filtro de búsqueda.

**Rellenar página con:** (No obligatorio) Cuando se selecciona, rellena los atributos en las páginas de configuración Usuario y grupo con los valores LDAP predeterminados correspondientes.

**Filtro de búsqueda:** (Obligatorio) El filtro de búsqueda que se utiliza para encontrar el registro asociado al usuario. Consulte Sintaxis del filtro de búsqueda.

### Configuración de Kerberos {#kerberos-settings}

Si está configurando la autenticación para un dominio empresarial o híbrido y selecciona la autenticación Kerberos, está disponible la siguiente configuración.

**IP DNS:** AEM La dirección IP DNS del servidor donde se está ejecutando el formulario de la. En Windows, puede determinar esta dirección IP ejecutando ipconfig /all en la línea de comandos.

**Host de KDC:** Nombre de host completo o dirección IP del servidor Active Directory que se utiliza para la autenticación.

**Usuario de servicio:** Si utiliza Active Directory 2003, este valor es la asignación creada para la entidad de seguridad de servicio en el formulario `HTTP/<server name>`. Si utiliza Active Directory 2008, este valor es el identificador de inicio de sesión de la entidad de seguridad de servicio. Por ejemplo, supongamos que la entidad de seguridad de servicio se llama um spnego, el ID de usuario es spnegodemo y la asignación es HTTP/example.yourcompany.com. Con Active Directory 2003, establece el Usuario de servicio en HTTP/example.yourcompany.com. Con Active Directory 2008, el usuario de servicio se establece en spnegodemo. (Consulte Habilitar SSO con SPNEGO).

**Dominio de servicio:** Nombre de dominio para Active Directory

**Contraseña de servicio:** Contraseña del usuario del servicio

**Activar SPNEGO:** Habilita el uso de SPNEGO para el inicio de sesión único (SSO). (Consulte Habilitar SSO con SPNEGO).

### Configuración de SAML {#saml-settings}

Si está configurando la autenticación para un dominio empresarial o híbrido y selecciona Autenticación SAML, están disponibles las siguientes opciones. Para obtener información sobre la configuración adicional de SAML, consulte [Configuración del proveedor de servicios SAML](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings).

**Seleccione el archivo de metadatos del proveedor de identidad de SAML que desea importar:** Haga clic en Examinar para seleccionar un archivo de metadatos de proveedor de identidad SAML generado a partir del IDP y, a continuación, haga clic en Importar. Se muestran los detalles del IDP.

**Título:** Alias a la dirección URL indicada por EntityID. El título también se muestra en la página de inicio de sesión para usuarios empresariales y locales.

**El Proveedor De Identidad Admite La Autenticación Básica Del Cliente:** La autenticación básica de cliente se utiliza cuando el IDP utiliza un perfil de resolución de artefactos SAML. En este perfil, Administración de usuarios se conecta de nuevo a un servicio web que se ejecuta en el IDP para recuperar la afirmación de SAML real. El IDP puede requerir autenticación. Si el IDP requiere autenticación, seleccione esta opción y especifique un nombre de usuario y una contraseña en los cuadros correspondientes.

**Propiedades personalizadas:** Permite especificar propiedades adicionales. Las propiedades adicionales son pares nombre=valor separados por nuevas líneas.

Se requieren las siguientes propiedades personalizadas si se utiliza el enlace de artefactos.

* AEM Agregue la siguiente propiedad personalizada para especificar un nombre de usuario que represente al proveedor de servicios de Forms, que se utilizará para autenticarse en el servicio de resolución de artefactos IDP.
   `saml.idp.resolve.username=<username>`

* Agregue la siguiente propiedad personalizada para especificar la contraseña del usuario especificado en `saml.idp.resolve.username`.
   `saml.idp.resolve.password=<password>`

* Agregue la siguiente propiedad personalizada para permitir que el proveedor de servicios ignore la validación del certificado al establecer la conexión con el servicio de resolución de artefactos a través de SSL.
   `saml.idp.resolve.ignorecert=true`

### Configuración personalizada {#custom-settings}

Si está configurando la autenticación para un dominio empresarial o híbrido y selecciona Autenticación personalizada, seleccione el nombre del proveedor de autenticación personalizada.

## Aprovisionamiento puntual de usuarios de {#just-in-time-provisioning-of-users}

El aprovisionamiento Just-In-Time crea un usuario en la base de datos de administración de usuarios automáticamente después de que el usuario se autentique correctamente a través de un proveedor de autenticación. Los roles y grupos relevantes también se asignan dinámicamente al nuevo usuario. Puede habilitar el aprovisionamiento justo a tiempo para dominios empresariales e híbridos.

AEM Este procedimiento describe el modo en que funciona la autenticación tradicional en los formularios de:

1. AEM Cuando un usuario intenta iniciar sesión en los formularios de la, Administración de usuarios pasa sus credenciales secuencialmente a todos los proveedores de autenticación disponibles. (Las credenciales de inicio de sesión incluyen la combinación de nombre de usuario y contraseña, vale Kerberos, firma PKCS7, etc.).
1. El proveedor de autenticación valida las credenciales.
1. A continuación, el proveedor de autenticación comprueba si el usuario existe en la base de datos de administración de usuarios. Los siguientes estados son posibles:

   **Existe** Si el usuario está actualizado y desbloqueado, Administración de usuarios devuelve la autenticación correcta. Sin embargo, si el usuario no está actualizado o bloqueado, Administración de usuarios devolverá un error de autenticación.

   **No existe** Administración de usuarios devuelve un error de autenticación.

   **No válido** Administración de usuarios devuelve un error de autenticación.

1. Se evalúa el resultado devuelto por el proveedor de autenticación. Si el proveedor de autenticación devolvió la autenticación correctamente, el usuario podrá iniciar sesión. De lo contrario, Administración de usuarios consulta con el siguiente proveedor de autenticación (pasos 2-3).
1. Se devuelve un error de autenticación si ningún proveedor de autenticación disponible valida las credenciales del usuario.

Cuando se habilita el aprovisionamiento Just-In-Time, los nuevos usuarios se crean dinámicamente en Administración de usuarios si uno de los proveedores de autenticación valida sus credenciales. (Después del paso 3 del procedimiento anterior).

Sin el aprovisionamiento Just-In-Time, cuando un usuario se autentica correctamente pero no se encuentra en la base de datos de Administración de usuarios, la autenticación falla. El aprovisionamiento Just-In-Time agrega un paso en el procedimiento de autenticación para crear el usuario y asignar funciones y grupos al usuario.

### Habilitar el aprovisionamiento justo a tiempo para un dominio {#enable-just-in-time-provisioning-for-a-domain}

1. Escriba un contenedor de servicio que implemente las interfaces IdentityCreator y AssignmentProvider. (Consulte [AEM Programar con formularios de](https://www.adobe.com/go/learn_aemforms_programming_63).)
1. Implemente el contenedor de servicios en el servidor de Forms.
1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.

   Seleccione un dominio existente o haga clic en Nuevo dominio de empresa.

1. Para crear un dominio, haga clic en Nuevo dominio empresarial o Nuevo dominio híbrido. Para editar un dominio existente, haga clic en el nombre del dominio.
1. Seleccione Habilitar aprovisionamiento Just In Time.

   ***nota **: Si falta la casilla de verificación Habilitar aprovisionamiento justo a tiempo, haga clic en Inicio > Configuración > Administración de usuarios > Configuración > Atributos avanzados del sistema y, a continuación, haga clic en Recargar.*

1. Agregar proveedores de autenticación. Al agregar proveedores de autenticación, en la pantalla Nueva autenticación, seleccione un creador de identidad y un proveedor de asignación registrados. (Consulte [Configuración de proveedores de autenticación](configuring-authentication-providers.md#configuring-authentication-providers).)
1. Guarde el dominio.
