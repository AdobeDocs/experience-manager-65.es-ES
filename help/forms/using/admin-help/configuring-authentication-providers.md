---
title: Configuración de proveedores de autenticación
seo-title: Configuring authentication providers
description: Agregue, edite o elimine proveedores de autenticación, cambie la configuración de autenticación y lea acerca del aprovisionamiento justo a tiempo de los usuarios.
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

# Configuración de proveedores de autenticación {#configuring-authentication-providers}

Los dominios híbridos requieren al menos un proveedor de autenticación y los dominios empresariales requieren al menos un proveedor de autenticación o un proveedor de directorios.

Si habilita SSO mediante SPNEGO, agregue un proveedor de autenticación Kerberos con SPNEGO habilitado y un proveedor LDAP como copia de seguridad. Esta configuración habilita la autenticación de usuarios con un ID de usuario y una contraseña si SPNEGO no funciona. (Consulte [Habilitar SSO mediante SPNEGO](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego)).

## Agregar un proveedor de autenticación {#add-an-authentication-provider}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en un dominio existente de la lista. Si agrega autenticación para un nuevo dominio, consulte [Agregar un dominio de empresa](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain) o [Agregar un dominio híbrido](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain).
1. Haga clic en Agregar autenticación y, en la lista Proveedor de autenticación, seleccione un proveedor, según el mecanismo de autenticación que utilice su organización.
1. Proporcione la información adicional requerida en la página. (Consulte [Configuración de autenticación](configuring-authentication-providers.md#authentication-settings)).
1. (Opcional) Haga clic en Probar para probar la configuración.
1. Haga clic en Aceptar y, a continuación, en Aceptar de nuevo.

## Editar un proveedor de autenticación existente {#edit-an-existing-authentication-provider}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el dominio correspondiente de la lista.
1. En la página que aparece, seleccione el proveedor de autenticación correspondiente en la lista y realice los cambios que sean necesarios. (Consulte [Configuración de autenticación](configuring-authentication-providers.md#authentication-settings)).
1. Haga clic en Aceptar.

## Eliminar un proveedor de autenticación {#delete-an-authentication-provider}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el dominio correspondiente de la lista.
1. Seleccione las casillas de verificación de los proveedores de autenticación que desea eliminar y haga clic en Eliminar.
1. Haga clic en Aceptar en la página de confirmación que aparece y vuelva a hacer clic en Aceptar.

## Configuración de autenticación {#authentication-settings}

Las siguientes opciones de configuración están disponibles en función del tipo de dominio y el tipo de autenticación que haya elegido.

### Configuración LDAP {#ldap-settings}

Si está configurando la autenticación para un dominio empresarial o híbrido y selecciona la autenticación LDAP, puede elegir utilizar el servidor LDAP especificado en la configuración del directorio o elegir un servidor LDAP diferente para la autenticación. Si elige un servidor diferente, los usuarios deben existir en ambos servidores LDAP.

Para utilizar el servidor LDAP especificado en la configuración del directorio, seleccione LDAP como proveedor de autenticación y haga clic en OK.

Para utilizar un servidor LDAP diferente para realizar la autenticación, seleccione LDAP como proveedor de autenticación y active la casilla de verificación Autenticación LDAP personalizada . Se muestran los siguientes ajustes de configuración.

**Servidor:**  (obligatorio) nombre de dominio completo (FQDN) del servidor de directorios. Por ejemplo, para un equipo llamado x en la red example.com, el FQDN es x.example.com. Se puede usar una dirección IP en lugar del nombre del servidor FQDN.

**Puerto:**  (obligatorio) puerto que utiliza el servidor de directorios. Normalmente, 389 o 636 si el protocolo Secure Sockets Layer (SSL) se utiliza para enviar información de autenticación a través de la red.

**SSL:**  (obligatorio) Especifica si el servidor de directorio utiliza SSL al enviar datos a través de la red. El valor predeterminado es No. Cuando se establece en Sí, el certificado de servidor LDAP correspondiente debe ser de confianza para el entorno de tiempo de ejecución (JRE) de Java™ del servidor de aplicaciones.

**Enlace**  (obligatorio) Especifica cómo acceder al directorio.

**Anónimo:**  no se requiere nombre de usuario ni contraseña.

**Usuario:** se requiere autenticación. En el cuadro Nombre, especifique el nombre del registro de usuario que puede acceder al directorio. Es mejor introducir el nombre de reconocimiento completo (DN) de la cuenta de usuario, como cn=Jane Doe, ou=user, dc=can, dc=com. En el cuadro Contraseña, especifique la contraseña asociada. Estos ajustes son necesarios cuando selecciona Usuario como opción de enlace.

**Recuperar DN base:**  (no obligatorio) recupera los DN base y los muestra en la lista desplegable. Esta configuración es útil cuando tiene varios DN base y necesita seleccionar un valor.

**DN base:**  (obligatorio) se utiliza como punto de partida para sincronizar usuarios y grupos desde la jerarquía LDAP. Es mejor especificar un DN base en el nivel más bajo de la jerarquía que incluya a todos los usuarios y grupos que necesitan sincronizarse para los servicios. No incluya el DN del usuario en esta configuración. Para sincronizar un usuario concreto, utilice la configuración Filtro de búsqueda .

**Rellenar página con:**  (no obligatorio) Cuando está seleccionado, rellena los atributos de las páginas de configuración de usuario y grupo con los valores LDAP predeterminados correspondientes.

**Filtro de búsqueda:** (obligatorio) el filtro de búsqueda que se utilizará para encontrar el registro asociado al usuario. Consulte Sintaxis del filtro de búsqueda.

### Configuración Kerberos {#kerberos-settings}

Si está configurando la autenticación para un dominio empresarial o híbrido y selecciona la autenticación Kerberos, están disponibles las siguientes opciones de configuración.

**IP DNS:** la dirección IP DNS del servidor en el que se ejecutan AEM formularios. En Windows, puede determinar esta dirección IP ejecutando ipconfig /all en la línea de comandos.

**Host KDC:** nombre de host o dirección IP completa del servidor de Active Directory que se utiliza para la autenticación.

**Usuario de servicio:** si utiliza Active Directory 2003, este valor es la asignación creada para la entidad de seguridad de servicio en el formulario  `HTTP/<server name>`. Si utiliza Active Directory 2008, este valor es el ID de inicio de sesión de la entidad de seguridad del servicio. Por ejemplo, supongamos que la entidad de seguridad del servicio se llama um spnego, que el ID del usuario es spnegodemo y que la asignación es HTTP/example.yourcompany.com. Con Active Directory 2003, se establece el usuario de servicio en HTTP/example.yourcompany.com. Con Active Directory 2008, se establece el usuario de servicio en spnegodemo. (Consulte Habilitar SSO mediante SPNEGO.)

**Dominio de servicio:** Nombre de dominio para Active Directory

**Contraseña de servicio:** Contraseña del usuario del servicio

**Habilitar SPNEGO:** permite el uso de SPNEGO para el inicio de sesión único (SSO). (Consulte Habilitar SSO mediante SPNEGO.)

### Configuración de SAML {#saml-settings}

Si está configurando la autenticación para un dominio empresarial o híbrido y selecciona la autenticación SAML, están disponibles las siguientes opciones. Para obtener más información sobre la configuración adicional de SAML, consulte [Configuración de la configuración del proveedor de servicios SAML](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings).

**Seleccione un archivo de metadatos de proveedor de identidad SAML para importar:** haga clic en Examinar para seleccionar un archivo de metadatos de proveedor de identidad SAML generado a partir de su IDP y, a continuación, haga clic en Importar. Se muestran los detalles de IDP.

**Título:** Alias a la URL indicada por EntityID. El título también se muestra en la página de inicio de sesión para usuarios empresariales y locales.

**El proveedor de identidad admite la autenticación básica del cliente:** la autenticación básica del cliente se utiliza cuando el IDP utiliza un perfil de resolución de artefactos SAML. En este perfil, la Administración de usuarios se conecta de nuevo a un servicio web que se ejecuta en el IDP para recuperar la afirmación real de SAML. El IDP puede requerir autenticación. Si el IDP requiere autenticación, seleccione esta opción y especifique un nombre de usuario y contraseña en las casillas proporcionadas.

**Propiedades personalizadas:** permite especificar propiedades adicionales. Las propiedades adicionales son pares name=value separados por nuevas líneas.

Las siguientes propiedades personalizadas son necesarias si se utiliza el enlace de artefactos.

* Agregue la siguiente propiedad personalizada para especificar un nombre de usuario que represente al proveedor de servicios de formularios AEM, que se utilizará para autenticarse en el servicio de resolución de artefactos IDP.
   `saml.idp.resolve.username=<username>`

* Agregue la siguiente propiedad personalizada para especificar la contraseña del usuario especificado en `saml.idp.resolve.username`.
   `saml.idp.resolve.password=<password>`

* Agregue la siguiente propiedad personalizada para permitir que el proveedor de servicios ignore la validación del certificado al establecer la conexión con el servicio de resolución de artefactos sobre SSL.
   `saml.idp.resolve.ignorecert=true`

### Configuración personalizada {#custom-settings}

Si está configurando la autenticación para un dominio empresarial o híbrido y selecciona Autenticación personalizada, seleccione el nombre del proveedor de autenticación personalizada.

## Aprovisionamiento puntual de los usuarios {#just-in-time-provisioning-of-users}

El aprovisionamiento justo a tiempo crea un usuario en la base de datos de Administración de usuarios automáticamente después de que el usuario se autentique correctamente mediante un proveedor de autenticación. Las funciones y los grupos relevantes también se asignan de forma dinámica al nuevo usuario. Puede habilitar el aprovisionamiento justo a tiempo para dominios empresariales e híbridos.

Este procedimiento describe el funcionamiento de la autenticación tradicional en AEM formularios:

1. Cuando un usuario intenta iniciar sesión en formularios AEM, Administración de usuarios pasa sus credenciales secuencialmente a todos los proveedores de autenticación disponibles. (Las credenciales de inicio de sesión incluyen combinación de nombre de usuario y contraseña, ticket Kerberos, firma PKCS7, etc.)
1. El proveedor de autenticación valida las credenciales.
1. A continuación, el proveedor de autenticación comprueba si el usuario existe en la base de datos de Administración de usuarios. Los siguientes estados son posibles:

   **** ExisteSi el usuario está actualizado y desbloqueado, Administración de usuarios devuelve la autenticación correctamente. Sin embargo, si el usuario no está actualizado o está bloqueado, Administración de usuarios devuelve un error de autenticación.

   **Does not** existUser Management devuelve un error de autenticación.

   **** InvalidUser Management devuelve un error de autenticación.

1. Se evalúa el resultado devuelto por el proveedor de autenticación. Si el proveedor de autenticación devolvió la autenticación correctamente, el usuario puede iniciar sesión. De lo contrario, la Administración de usuarios comprueba con el siguiente proveedor de autenticación (pasos 2-3).
1. Se devuelve un error de autenticación si ningún proveedor de autenticación disponible valida las credenciales del usuario.

Cuando el aprovisionamiento justo a tiempo está habilitado, los nuevos usuarios se crean dinámicamente en Administración de usuarios si uno de los proveedores de autenticación valida sus credenciales. (Después del paso 3 del procedimiento anterior).

Sin aprovisionamiento justo en el tiempo, cuando un usuario se autentica correctamente pero no se encuentra en la base de datos de Administración de usuarios, la autenticación falla. El aprovisionamiento justo a tiempo añade un paso en el procedimiento de autenticación para crear el usuario y asignar funciones y grupos al usuario.

### Habilitar el aprovisionamiento justo a tiempo para un dominio {#enable-just-in-time-provisioning-for-a-domain}

1. Escriba un contenedor de servicio que implemente las interfaces IdentityCreator y AssignmentProvider. (Consulte [Programación con formularios AEM](https://www.adobe.com/go/learn_aemforms_programming_63)).
1. Implemente el contenedor de servicio en el servidor de formularios.
1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.

   Seleccione un dominio existente o haga clic en Nuevo dominio de Enterprise.

1. Para crear un dominio, haga clic en Nuevo dominio de empresa o en Nuevo dominio híbrido. Para editar un dominio existente, haga clic en el nombre del dominio.
1. Seleccione Habilitar Aprovisionamiento Justo A Tiempo.

   ***nota **: Si falta la casilla de verificación Habilitar aprovisionamiento justo a tiempo , haga clic en Inicio > Configuración > Administración de usuarios > Configuración > Atributos del sistema avanzados y, a continuación, haga clic en Recargar.*

1. Agregue proveedores de autenticación. Al agregar proveedores de autenticación, en la pantalla Nueva autenticación , seleccione un Creador de identidad y Proveedor de asignación registrados. (Consulte [Configuración de proveedores de autenticación](configuring-authentication-providers.md#configuring-authentication-providers)).
1. Guarde el dominio.
