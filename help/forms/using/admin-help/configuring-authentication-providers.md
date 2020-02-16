---
title: Configuración de proveedores de autenticación
seo-title: Configuración de proveedores de autenticación
description: Agregue, edite o elimine proveedores de autenticación, cambie la configuración de autenticación y lea información sobre el aprovisionamiento justo a tiempo de los usuarios.
seo-description: Agregue, edite o elimine proveedores de autenticación, cambie la configuración de autenticación y lea información sobre el aprovisionamiento justo a tiempo de los usuarios.
uuid: 90e7690b-1ce0-4604-b58f-6dca4f2372cf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 31dd8db3-ddac-429e-82f8-8c5dc4ffc186
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración de proveedores de autenticación {#configuring-authentication-providers}

Los dominios híbridos requieren al menos un proveedor de autenticación y los dominios empresariales requieren al menos un proveedor de autenticación o de directorio.

Si habilita SSO mediante SPNEGO, agregue un proveedor de autenticación Kerberos con SPNEGO habilitado y un proveedor LDAP como copia de seguridad. Esta configuración permite la autenticación de usuarios con un ID de usuario y una contraseña si SPNEGO no funciona. (Consulte [Habilitar SSO mediante SPNEGO](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego)).

## Agregar un proveedor de autenticación {#add-an-authentication-provider}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en un dominio existente de la lista. Si va a agregar autenticación para un nuevo dominio, consulte [Agregar un dominio](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain) de empresa o [Agregar un dominio](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain)híbrido.
1. Haga clic en Agregar autenticación y, en la lista Proveedor de autenticación, seleccione un proveedor, según el mecanismo de autenticación que utilice su organización.
1. Proporcione la información adicional necesaria en la página. (Consulte Configuración [de autenticación](configuring-authentication-providers.md#authentication-settings)).
1. (Opcional) Haga clic en Prueba para probar la configuración.
1. Haga clic en Aceptar y, a continuación, en Aceptar nuevamente.

## Editar un proveedor de autenticación existente {#edit-an-existing-authentication-provider}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el dominio correspondiente de la lista.
1. En la página que aparece, seleccione el proveedor de autenticación adecuado de la lista y realice los cambios que sean necesarios. (Consulte Configuración [de autenticación](configuring-authentication-providers.md#authentication-settings)).
1. Haga clic en Aceptar.

## Eliminar un proveedor de autenticación {#delete-an-authentication-provider}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el dominio correspondiente de la lista.
1. Seleccione las casillas de verificación de los proveedores de autenticación que desea eliminar y haga clic en Eliminar.
1. Haga clic en Aceptar en la página de confirmación que aparece y vuelva a hacer clic en Aceptar.

## Authentication settings {#authentication-settings}

Las siguientes opciones de configuración están disponibles, según el tipo de dominio y el tipo de autenticación que elija.

### Ajustes LDAP {#ldap-settings}

Si está configurando la autenticación para un dominio empresarial o híbrido y selecciona la autenticación LDAP, puede elegir utilizar el servidor LDAP especificado en la configuración del directorio o elegir otro servidor LDAP para la autenticación. Si elige otro servidor, los usuarios deben existir en ambos servidores LDAP.

Para utilizar el servidor LDAP especificado en la configuración del directorio, seleccione LDAP como proveedor de autenticación y haga clic en Aceptar.

Para utilizar un servidor LDAP diferente para realizar la autenticación, seleccione LDAP como proveedor de autenticación y active la casilla de verificación Autenticación LDAP personalizada. Se muestran las siguientes opciones de configuración.

**** Servidor: (Obligatorio) Nombre de dominio completo (FQDN) del servidor de directorio. Por ejemplo, para un equipo llamado x en la red corp.ejemplo.com, el FQDN es x.corp.ejemplo.com. Se puede usar una dirección IP en lugar del nombre del servidor FQDN.

**** Puerto: (Obligatorio) El puerto que utiliza el servidor de directorio. Generalmente, 389 o 636 si se utiliza el protocolo Secure Sockets Layer (SSL) para enviar información de autenticación a través de la red.

**** SSL: (Obligatorio) Especifica si el servidor de directorio utiliza SSL al enviar datos a través de la red. El valor predeterminado es No. Cuando se establece en Sí, el entorno de tiempo de ejecución de Java™ (JRE) del servidor de aplicaciones debe confiar en el certificado de servidor LDAP correspondiente.

**Enlace** (obligatorio) Especifica cómo acceder al directorio.

**** Anónimo: No se requiere nombre de usuario ni contraseña.

**** Usuario: Se requiere autenticación. En el cuadro Nombre, especifique el nombre del registro de usuario que puede acceder al directorio. Es mejor introducir el nombre de reconocimiento completo (DN) de la cuenta de usuario, como cn=Jane Doe, ou=user, dc=can, dc=com. En el cuadro Contraseña, especifique la contraseña asociada. Estas opciones de configuración son necesarias cuando selecciona Usuario como opción de enlace.

**** Recuperar DN base: (No obligatorio) Recupera los DN base y los muestra en la lista desplegable. Esta configuración resulta útil cuando tiene varios DN base y necesita seleccionar un valor.

**** DN base: (Obligatorio) Se utiliza como punto de partida para sincronizar usuarios y grupos desde la jerarquía de LDAP. Es mejor especificar un DN base en el nivel más bajo de la jerarquía que incluya a todos los usuarios y grupos que necesitan sincronizarse para los servicios.  No incluya el DN del usuario en esta configuración. Para sincronizar un usuario en particular, utilice la configuración Filtro de búsqueda.

**** Rellene la página con: (No obligatorio) Cuando se selecciona, rellena los atributos en las páginas de configuración de usuario y grupo con los valores LDAP predeterminados correspondientes.

**** Filtro de búsqueda: (Obligatorio) Filtro de búsqueda que se usará para encontrar el registro asociado al usuario. Consulte Sintaxis del filtro de búsqueda.

### Configuración de Kerberos {#kerberos-settings}

Si está configurando la autenticación para un dominio empresarial o híbrido y selecciona la autenticación Kerberos, se dispone de las siguientes opciones de configuración.

**** IP DNS: La dirección IP DNS del servidor en el que se ejecutan los formularios AEM. En Windows, puede determinar esta dirección IP ejecutando ipconfig /all en la línea de comandos.

**** Host KDC: Nombre de host completo o dirección IP del servidor de Active Directory que se utiliza para la autenticación.

**** Usuario de servicio: Si utiliza Active Directory 2003, este valor es la asignación creada para el principal de servicio en el formulario `HTTP/<server name>`. Si utiliza Active Directory 2008, este valor es el ID de inicio de sesión del principal de servicio. Por ejemplo, supongamos que el principal de servicio se llama um spnego, que el ID de usuario es spnegodemo y que la asignación es HTTP/example.corp.yourcompany.com. Con Active Directory 2003, debe establecer el usuario de servicios en HTTP/example.corp.yourcompany.com. Con Active Directory 2008, se establece el usuario de servicios en spnegodemo. (Consulte Habilitar SSO con SPNEGO).

**** Dominio de servicio: Nombre de dominio para Active Directory

**** Contraseña de servicio: Contraseña del usuario del servicio

**** Habilitar SPNEGO: Habilita el uso de SPNEGO para el inicio de sesión único (SSO). (Consulte Habilitar SSO con SPNEGO).

### Configuración de SAML {#saml-settings}

Si está configurando la autenticación para un dominio empresarial o híbrido y selecciona la autenticación SAML, se dispone de las siguientes opciones de configuración. Para obtener información sobre la configuración de SAML adicional, consulte [Configuración de la configuración](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings)del proveedor de servicios SAML.

**** Seleccione un archivo de metadatos de proveedor de identidad SAML para importar: Haga clic en Examinar para seleccionar un archivo de metadatos del proveedor de identidad SAML generado a partir de su IDP y, a continuación, haga clic en Importar. Se muestran los detalles de IDP.

**** Título: Alias a la dirección URL indicada por EntityID. El título también se muestra en la página de inicio de sesión para usuarios empresariales y locales.

**** El proveedor de identidad admite la autenticación básica del cliente: La autenticación básica del cliente se utiliza cuando el IDP utiliza un perfil de resolución de artefactos SAML. En este perfil, la Administración de usuarios se conecta de nuevo a un servicio Web que se ejecuta en el IDP para recuperar la afirmación real de SAML. El IDP puede requerir autenticación. Si el IDP requiere autenticación, seleccione esta opción y especifique un nombre de usuario y una contraseña en las casillas proporcionadas.

**** Propiedades personalizadas: Permite especificar propiedades adicionales. Las propiedades adicionales son pares name=value separados por nuevas líneas.

Se requieren las siguientes propiedades personalizadas si se utiliza el enlace de artefactos.

* Agregue la siguiente propiedad personalizada para especificar un nombre de usuario que represente al proveedor de servicios de formularios AEM, que se utilizará para autenticarse en el servicio de resolución de artefactos IDP.
   `saml.idp.resolve.username=<username>`

* Agregue la siguiente propiedad personalizada para especificar la contraseña del usuario especificado en `saml.idp.resolve.username`.
   `saml.idp.resolve.password=<password>`

* Agregue la siguiente propiedad personalizada para permitir que el proveedor de servicios ignore la validación del certificado al establecer la conexión con el servicio de resolución de artefactos a través de SSL.
   `saml.idp.resolve.ignorecert=true`

### Custom settings {#custom-settings}

Si está configurando la autenticación para un dominio empresarial o híbrido y selecciona Autenticación personalizada, seleccione el nombre del proveedor de autenticación personalizada.

## Aprovisionamiento puntual de los usuarios {#just-in-time-provisioning-of-users}

El aprovisionamiento justo a tiempo crea un usuario en la base de datos de Administración de usuarios automáticamente después de autenticarlo correctamente mediante un proveedor de autenticación. Los roles y grupos relevantes también se asignan de forma dinámica al nuevo usuario. Puede habilitar el aprovisionamiento justo a tiempo para dominios empresariales e híbridos.

Este procedimiento describe el modo en que funciona la autenticación tradicional en los formularios AEM:

1. Cuando un usuario intenta iniciar sesión en formularios AEM, la Administración de usuarios pasa sus credenciales de forma secuencial a todos los proveedores de autenticación disponibles. (Las credenciales de inicio de sesión incluyen combinación de nombre de usuario y contraseña, vale Kerberos, firma PKCS7, etc.)
1. El proveedor de autenticación valida las credenciales.
1. A continuación, el proveedor de autenticación comprueba si el usuario existe en la base de datos de Administración de usuarios. Los siguientes estados son posibles:

   **Existe** Si el usuario está actualizado y desbloqueado, Administración de usuarios devuelve la autenticación correcta. Sin embargo, si el usuario no está actualizado o está bloqueado, Administración de usuarios devuelve un error de autenticación.

   **No existe** Administración de usuarios devuelve un error de autenticación.

   **Administración de usuarios no válida** devuelve un error de autenticación.

1. Se evalúa el resultado devuelto por el proveedor de autenticación. Si el proveedor de autenticación devolvió la autenticación correctamente, se permite al usuario iniciar sesión. De lo contrario, la Administración de usuarios comprueba con el siguiente proveedor de autenticación (pasos 2 a 3).
1. Se devuelve un error de autenticación si ningún proveedor de autenticación disponible valida las credenciales de usuario.

Cuando se habilita el aprovisionamiento justo a tiempo, los usuarios nuevos se crean de forma dinámica en Administración de usuarios si uno de los proveedores de autenticación valida sus credenciales. (Después del paso 3 del procedimiento anterior).

Sin aprovisionamiento justo a tiempo, cuando un usuario se autentica correctamente pero no se encuentra en la base de datos de Administración de usuarios, se produce un error en la autenticación. El aprovisionamiento justo a tiempo agrega un paso en el procedimiento de autenticación para crear el usuario y asignar funciones y grupos al usuario.

### Habilitar el aprovisionamiento justo a tiempo para un dominio {#enable-just-in-time-provisioning-for-a-domain}

1. Escriba un contenedor de servicios que implemente las interfaces IdentityCreator y AssignmentProvider. (Consulte [Programación con formularios](https://www.adobe.com/go/learn_aemforms_programming_63)AEM).
1. Implemente el contenedor de servicio en el servidor de formularios.
1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.

   Seleccione un dominio existente o haga clic en Nuevo dominio de empresa.

1. Para crear un dominio, haga clic en Nuevo dominio de empresa o Nuevo dominio híbrido. Para editar un dominio existente, haga clic en el nombre del dominio.
1. Seleccione Habilitar aprovisionamiento justo a tiempo.

   ***nota **: Si falta la casilla Activar aprovisionamiento justo a tiempo, haga clic en Inicio > Configuración > Administración de usuarios > Configuración > Atributos avanzados del sistema y, a continuación, haga clic en Volver a cargar.*

1. Agregue proveedores de autenticación. Al agregar proveedores de autenticación, en la pantalla Nueva autenticación, seleccione un Creador de identidad y un Proveedor de asignación registrados. (Consulte [Configuración de proveedores](configuring-authentication-providers.md#configuring-authentication-providers)de autenticación.)
1. Guarde el dominio.

