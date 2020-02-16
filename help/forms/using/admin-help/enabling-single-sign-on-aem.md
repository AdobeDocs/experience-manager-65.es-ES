---
title: Activación del inicio de sesión único en formularios AEM
seo-title: Activación del inicio de sesión único en formularios AEM
description: Obtenga información sobre cómo habilitar el inicio de sesión único (SSO) mediante encabezados HTTP y SPNEGO.
seo-description: Obtenga información sobre cómo habilitar el inicio de sesión único (SSO) mediante encabezados HTTP y SPNEGO.
uuid: 2bc08b4f-dcbe-4a16-9025-32fc14605e13
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ee54d9d4-190d-4665-925a-9740ac65fbd5
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# Activación del inicio de sesión único en formularios AEM{#enabling-single-sign-on-in-aem-forms}

Los formularios AEM ofrecen dos formas de activar el inicio de sesión único (SSO): encabezados HTTP y SPNEGO.

Cuando se implementa SSO, las páginas de inicio de sesión del usuario de los formularios AEM no son necesarias y no aparecen si el usuario ya está autenticado a través del portal de su empresa.

Si los formularios AEM no pueden autenticar a un usuario mediante cualquiera de estos métodos, se redirige al usuario a una página de inicio de sesión.

## Habilitar SSO mediante encabezados HTTP {#enable-sso-using-http-headers}

Puede utilizar la página Configuración del portal para habilitar el inicio de sesión único (SSO) entre las aplicaciones y cualquier aplicación que admita la transmisión de la identidad a través del encabezado HTTP. Cuando se implementa SSO, las páginas de inicio de sesión del usuario de los formularios AEM no son necesarias y no aparecen si el usuario ya está autenticado a través del portal de su empresa.

También puede activar SSO mediante SPNEGO. (Consulte [Habilitar SSO mediante SPNEGO](enabling-single-sign-on-aem.md#enable-sso-using-spnego)).

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Configurar atributos del portal.
1. Seleccione Sí para activar SSO. Si selecciona No, las opciones de configuración restantes de la página no estarán disponibles.
1. Configure las opciones restantes de la página según sea necesario y haga clic en Aceptar:

   * **** Tipo de SSO: (Obligatorio) Seleccione Encabezado HTTP para habilitar SSO mediante encabezados HTTP.
   * **** Encabezado HTTP para el identificador del usuario: (Obligatorio) Nombre del encabezado cuyo valor contiene el identificador único del usuario que ha iniciado sesión. La Administración de usuarios utiliza este valor para buscar al usuario en la base de datos de Administración de usuarios. El valor obtenido a partir de este encabezado debe coincidir con el identificador único del usuario que se sincroniza desde el directorio LDAP. (Consulte Configuración [de usuario](/help/forms/using/admin-help/adding-configuring-users.md#user-settings)).
   * **** El valor de identificador se asigna al ID de usuario del usuario en lugar del identificador único del usuario: Asigna el valor de identificador único del usuario al ID de usuario. Seleccione esta opción si el identificador único del usuario es un valor binario que no se puede propagar fácilmente a través de encabezados HTTP (por ejemplo, objectGUID si está sincronizando usuarios de Active Directory).
   * **** Encabezado HTTP para dominio: (No obligatorio) Nombre del encabezado cuyo valor contiene el nombre de dominio. Utilice esta configuración solo si ningún encabezado HTTP identifica exclusivamente al usuario. Utilice esta configuración para los casos en los que existen varios dominios y el identificador único es único dentro de un dominio. En este caso, especifique el nombre del encabezado en este cuadro de texto y la asignación de dominios para los varios dominios en el cuadro Asignación de dominios. (Consulte [Edición y conversión de dominios](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)existentes.)
   * **** Asignación de dominios: (Obligatorio) Especifica la asignación de varios dominios con el formato *header value=nombre* de dominio.

      Por ejemplo, supongamos una situación en la que el encabezado HTTP de un dominio es domainName y puede tener valores de domain1, domain2 o domain3. En este caso, utilice la asignación de dominios para asignar los valores de domainName a los nombres de dominio de Administración de usuarios. Cada asignación debe estar en una línea diferente:

      domain1=UMdomain1

      domain2=UMdomain2

      domain3=UMdomain3

### Configurar referentes permitidos {#configure-allowed-referers}

Para ver los pasos para configurar los referentes permitidos, consulte [Configuración de los referentes](/help/forms/using/admin-help/preventing-csrf-attacks.md#configure-allowed-referers)permitidos.

## Habilitar SSO mediante SPNEGO {#enable-sso-using-spnego}

Puede utilizar el mecanismo de negociación simple y protegido de GSSAPI (SPNEGO) para habilitar el inicio de sesión único (SSO) al utilizar Active Directory como servidor LDAP en un entorno Windows. Cuando SSO está activado, las páginas de inicio de sesión del usuario de los formularios AEM no son necesarias y no aparecen.

También puede activar SSO mediante encabezados HTTP. (Consulte [Habilitar SSO mediante encabezados](enabling-single-sign-on-aem.md#enable-sso-using-http-headers)HTTP).

>[!NOTE]
>
>AEM Forms en JEE no admite la configuración de SSO mediante Kerberos/SPNEGO en varios entornos de dominio secundarios.

1. Decida qué dominio utilizar para habilitar SSO. El servidor de formularios AEM y los usuarios deben formar parte del mismo dominio de Windows o dominio de confianza.
1. En Active Directory, cree un usuario que represente el servidor de formularios AEM. (Consulte [Creación de una cuenta](enabling-single-sign-on-aem.md#create-a-user-account)de usuario.) Si va a configurar más de un dominio para utilizar SPNEGO, asegúrese de que las contraseñas de cada uno de estos usuarios sean diferentes. Si las contraseñas no son diferentes, SPNEGO SSO no funciona.
1. Asigne el nombre principal del servicio. (Consulte [Asignación de un nombre principal de servicio (SPN)](enabling-single-sign-on-aem.md#map-a-service-principal-name-spn)).
1. Configure el controlador de dominio. (Consulte [Prevención de errores](enabling-single-sign-on-aem.md#prevent-kerberos-integrity-check-failures)de comprobación de integridad Kerberos.)
1. Agregue o edite un dominio de empresa como se describe en [Adición de dominios](/help/forms/using/admin-help/adding-domains.md#adding-domains) o [Edición y conversión de dominios](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)existentes. Cuando cree o edite el dominio de empresa, realice las siguientes tareas:

   * Agregue o edite un directorio que contenga la información de Active Directory.
   * Agregue LDAP como proveedor de autenticación.
   * Agregue Kerberos como proveedor de autenticación. Proporcione la siguiente información en la página Nueva o Editar autenticación para Kerberos:

      * **** Proveedor de autenticación: Kerberos
      * **** IP DNS: La dirección IP DNS del servidor en el que se ejecutan los formularios AEM. Puede determinar esta dirección IP ejecutándose `ipconfig/all` en la línea de comandos.
      * **** Host KDC: Nombre de host completo o dirección IP del servidor de Active Directory utilizado para la autenticación
      * **** Usuario de servicio: El nombre principal de servicio (SPN) pasado a la herramienta KtPass. En el ejemplo utilizado anteriormente, el usuario del servicio es `HTTP/lcserver.um.lc.com`.
      * **** Dominio de servicio: Nombre de dominio para Active Directory. En el ejemplo utilizado anteriormente, el nombre de dominio es `UM.LC.COM.`
      * **** Contraseña de servicio: Contraseña del usuario del servicio. En el ejemplo utilizado anteriormente, la contraseña del servicio es `password`.
      * **** Habilitar SPNEGO: Habilita el uso de SPNEGO para el inicio de sesión único (SSO). Seleccione esta opción.

1. Configure la configuración del explorador del cliente SPNEGO. (Consulte [Configuración de la configuración](enabling-single-sign-on-aem.md#configuring-spnego-client-browser-settings)del navegador del cliente SPNEGO).

### Crear una cuenta de usuario {#create-a-user-account}

1. En SPNEGO, registre un servicio como usuario en Active Directory en el controlador de dominio para representar formularios AEM. En el controlador de dominio, vaya al menú Inicio > Herramientas administrativas > Usuarios y equipos de Active Directory. Si Herramientas administrativas no está en el menú Inicio, utilice el Panel de control.
1. Haga clic en la carpeta Usuarios para mostrar una lista de usuarios.
1. Haga clic con el botón derecho en la carpeta de usuario y seleccione Nuevo > Usuario.
1. Escriba el nombre y los apellidos y el nombre de inicio de sesión del usuario y, a continuación, haga clic en Siguiente. Por ejemplo, establezca los siguientes valores:

   * **Nombre**: umspnego
   * **Nombre** de inicio de sesión del usuario: spnegodemo

1. Escriba una contraseña. Por ejemplo, configúrela en *contraseña*. Asegúrese de que la contraseña nunca caduca está seleccionada y de que no hay ninguna otra opción seleccionada.
1. Haga clic en Siguiente y, a continuación, en Finalizar.

### Asignar un nombre principal de servicio (SPN) {#map-a-service-principal-name-spn}

1. Obtenga la utilidad KtPass. Esta utilidad se utiliza para asignar un SPN a un REALM. Puede obtener la utilidad KtPass como parte del paquete de herramientas de Windows Server o del Kit de recursos. (Consulte Herramientas [de soporte de](https://support.microsoft.com/kb/892777)Windows Server 2003 Service Pack 1).
1. En un símbolo del sistema, ejecute `ktpass` utilizando los siguientes argumentos:

   `ktpass -princ HTTP/`*host *`@`*REALM* `-mapuser`*user *

   Por ejemplo, escriba el siguiente texto:

   `ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo`

   Los valores que debe proporcionar se describen a continuación:

   **** host: Nombre completo del servidor de formularios o cualquier dirección URL única. En este ejemplo, se establece en lcserver.um.lc.com.

   **** REALM: Dominio de Active Directory para el controlador de dominio. En este ejemplo, se establece en UM.LC.COM. Asegúrese de introducir el territorio en caracteres en mayúsculas. Para determinar el territorio para Windows 2003, complete los siguientes pasos:

   * Haga clic con el botón derecho en Mi PC y seleccione Propiedades
   * Haga clic en la ficha Nombre del equipo. El valor Nombre de dominio es el nombre del territorio.
   **** user: El nombre de inicio de sesión de la cuenta de usuario que creó en la tarea anterior. En este ejemplo, se establece en spnegodemo.

Si aparece este error:

```as3
DsCrackNames returned 0x2 in the name entry for spnegodemo.
ktpass:failed getting target domain for specified user.
```

intente especificar el usuario como spnegodemo@um.lc.com:

```as3
ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo
```

### Evitar errores de comprobación de integridad Kerberos {#prevent-kerberos-integrity-check-failures}

1. En el controlador de dominio, vaya al menú Inicio > Herramientas administrativas > Usuarios y equipos de Active Directory. Si Herramientas administrativas no está en el menú Inicio, utilice el Panel de control.
1. Haga clic en la carpeta Usuarios para mostrar una lista de usuarios.
1. Haga clic con el botón secundario en la cuenta de usuario que creó en una tarea anterior. En este ejemplo, la cuenta de usuario es `spnegodemo`.
1. Haga clic en Restablecer contraseña.
1. Escriba y confirme la misma contraseña que escribió anteriormente. En este ejemplo, se establece en `password`.
1. Anule la selección de Cambiar contraseña en el siguiente inicio de sesión y, a continuación, haga clic en Aceptar.

### Configuración de la configuración del navegador del cliente SPNEGO {#configuring-spnego-client-browser-settings}

Para que la autenticación basada en SPNEGO funcione, el equipo cliente debe formar parte del dominio en el que se crea la cuenta de usuario. También debe configurar el navegador del cliente para permitir la autenticación basada en SPNEGO. Además, el sitio que requiere autenticación basada en SPNEGO debe ser un sitio de confianza.

Si se accede al servidor con el nombre del equipo, como https://lcserver:8080, no se requiere ninguna configuración para Internet Explorer. Si introduce una dirección URL que no contenga puntos (&quot;.&quot;), Internet Explorer tratará el sitio como un sitio de intranet local. Si utiliza un nombre completo para el sitio, éste debe agregarse como un sitio de confianza.

**Configurar Internet Explorer 6.x**

1. Vaya a Herramientas > Opciones de Internet y haga clic en la ficha Seguridad.
1. Haga clic en el icono de Intranet local y, a continuación, haga clic en Sitios.
1. Haga clic en Avanzadas y, en el cuadro Agregar este sitio Web a la zona, escriba la dirección URL del servidor de formularios. For example, type `https://lcserver.um.lc.com`
1. Haga clic en Aceptar hasta que se cierren todos los cuadros de diálogo.
1. Compruebe la configuración accediendo a la URL del servidor de formularios AEM. Por ejemplo, en el cuadro URL del explorador, escriba `https://lcserver.um.lc.com:8080/um/login?um_no_redirect=true`

**Configurar Mozilla Firefox**

1. En el cuadro URL del explorador, escriba `about:config`

   Aparece el cuadro de diálogo about:config - Mozilla Firefox.

1. En el cuadro Filtro, escriba `negotiate`
1. En la lista mostrada, haga clic en network.Negoti-auth.Trusted-uri y escriba uno de los siguientes comandos según corresponda para su entorno:

   `.um.lc.com`- Configura Firefox para permitir SPNEGO para cualquier URL que termine con um.lc.com. Asegúrese de incluir el punto (&quot;.&quot;) al principio.

   `lcserver.um.lc.com` - Configura Firefox para permitir SPNEGO sólo para su servidor específico. No inicie este valor con un punto (&quot;.&quot;).

1. Compruebe la configuración accediendo a la aplicación. Debe aparecer la página de bienvenida para la aplicación de destino.

