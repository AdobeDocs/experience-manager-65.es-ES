---
title: Configuración de SSL para el servidor de aplicaciones WebSphere
seo-title: Configuring SSL for WebSphere Application Server
description: Aprenda a configurar SSL para el servidor de aplicaciones WebSphere.
seo-description: Learn how to configure SSL for WebSphere Application Server.
uuid: f939a806-346e-41e0-b2c0-6d0ba83f8f6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7c0efcb3-5b07-4090-9119-b7318c8b7980
exl-id: b0786b52-879e-4a24-9cc9-bd9dcb2473cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 1%

---

# Configuración de SSL para el servidor de aplicaciones WebSphere {#configuring-ssl-for-websphere-application-server}

Esta sección incluye los siguientes pasos para configurar SSL con el servidor de aplicaciones IBM WebSphere.

## Creación de una cuenta de usuario local en WebSphere {#creating-a-local-user-account-on-websphere}

Para habilitar SSL, WebSphere necesita acceder a una cuenta de usuario en el registro de usuario del sistema operativo local que tiene permiso para administrar el sistema:

* (Windows) Cree un nuevo usuario de Windows que forme parte del grupo Administradores y que tenga el privilegio de actuar como parte del sistema operativo. (Consulte [Crear un usuario de Windows para WebSphere](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere).)
* (Linux, UNIX) El usuario puede ser un usuario raíz u otro usuario que tenga privilegios de root. Cuando habilite SSL en WebSphere, utilice la identificación del servidor y la contraseña de este usuario.

### Crear un usuario Linux o UNIX para WebSphere {#create-a-linux-or-unix-user-for-websphere}

1. Inicie sesión como usuario raíz.
1. Cree un usuario introduciendo el siguiente comando en un símbolo del sistema:

   * (Linux y Sun Solaris) `useradd`
   * (IBM AIX) `mkuser`

1. Establezca la contraseña del nuevo usuario introduciendo `passwd` en el símbolo del sistema.
1. (Linux y Solaris) Cree un archivo de contraseña de sombra introduciendo `pwconv` (sin parámetros) en el símbolo del sistema.

   >[!NOTE]
   >
   >(Linux y Solaris) Para que funcione el registro de seguridad del sistema operativo local del servidor de aplicaciones WebSphere, debe existir un archivo de contraseña de sombra. El nombre del archivo de contraseña de la sombra suele ser **/etc/Shadow** y se basa en el archivo /etc/passwd. Si el archivo de contraseña de sombra no existe, se produce un error después de habilitar la seguridad global y configurar el registro de usuario como sistema operativo local.

1. Abra el archivo de grupo desde el directorio /etc en un editor de texto.
1. Agregue al usuario que creó en el paso 2 al `root` grupo.
1. Guarde y cierre el archivo.
1. (UNIX con SSL habilitado) Inicie y detenga WebSphere como el usuario raíz.

### Crear un usuario de Windows para WebSphere {#create-a-windows-user-for-websphere}

1. Inicie sesión en Windows con una cuenta de usuario administrador.
1. Select **Inicio > Panel de control de Campaign > Herramientas administrativas > Administración de equipos > Usuarios y grupos locales**.
1. Haga clic con el botón derecho del ratón en Usuarios y seleccione **Nuevo usuario**.
1. Escriba un nombre de usuario y una contraseña en los cuadros correspondientes y escriba cualquier otra información que necesite en los cuadros restantes.
1. Anular selección **El Usuario Debe Cambiar La Contraseña En El Siguiente Inicio De Sesión**, haga clic en **Crear** y, a continuación, haga clic en **Cerrar**.
1. Haga clic en **Usuarios**, haga clic con el botón derecho en el usuario que acaba de crear y seleccione **Propiedades**.
1. Haga clic en el **Miembro de** y, a continuación, haga clic en **Agregar**.
1. En el cuadro Introducir los nombres de objeto que desea seleccionar, escriba `Administrators`, haga clic en Comprobar nombres para asegurarse de que el nombre del grupo es correcto.
1. Haga clic en **OK** y haga clic en **OK** de nuevo.
1. Select **Inicio > Panel de control de Campaign > Herramientas administrativas > Política de seguridad local > Políticas locales**.
1. Haga clic en Asignación de derechos de usuario y, a continuación, haga clic con el botón secundario en Accionar como parte del sistema operativo y seleccione Propiedades.
1. Haga clic en **Agregar usuario o grupo**.
1. En el cuadro Introducir los nombres de objeto que se deben seleccionar, escriba el nombre del usuario que creó en el paso 4 y haga clic en **Comprobar nombres** para asegurarse de que el nombre es correcto y, a continuación, haga clic en **OK**.
1. Haga clic en **OK** para cerrar el cuadro de diálogo Actuar como parte de las propiedades del sistema operativo.

### Configure WebSphere para utilizar el usuario recién creado como administrador {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. Asegúrese de que WebSphere se esté ejecutando.
1. En la Consola administrativa de WebSphere, seleccione **Seguridad > Seguridad global**.
1. En Seguridad administrativa, seleccione **Funciones de usuario administrativas**.
1. Haga clic en Agregar y haga lo siguiente:

   1. Tipo **&amp;ast;** en el cuadro de búsqueda y haga clic en buscar.
   1. Haga clic en **Administrador** en funciones.
   1. Agregue el usuario recién creado a Asignado a la función y asígnelo a Administrador.

1. Haga clic en **OK** y guarde los cambios.
1. Reinicie el perfil de WebSphere.

## Habilitar la seguridad administrativa {#enable-administrative-security}

1. En la Consola administrativa de WebSphere, seleccione **Seguridad > Seguridad global**.
1. Haga clic en **Asistente de configuración de seguridad**.
1. Asegúrese **Habilitar la seguridad de la aplicación** está activada. Haga clic en **Siguiente**.
1. Select **Repositorios federados** y haga clic en **Siguiente**.
1. Especifique las credenciales que desea establecer y haga clic en **Siguiente**.
1. Haga clic en **Finalizar**.
1. Reinicie el perfil de WebSphere.

   WebSphere empezará a utilizar el almacén de claves predeterminado y el almacén de confianza.

## Habilitar SSL (clave personalizada y almacén de confianza) {#enable-ssl-custom-key-and-truststore}

Las tiendas de confianza y las tiendas de claves se pueden crear usando la utilidad ikeyman o admin console. Para que ikeyman funcione correctamente, asegúrese de que la ruta de instalación de WebSphere no contenga paréntesis.

1. En la Consola administrativa de WebSphere, seleccione **Seguridad > Gestión de claves y certificados SSL**.
1. Haga clic en **Almacenes de claves y certificados** en Elementos relacionados.
1. En el **Usos del almacén de claves** lista desplegable, asegúrese de que **Almacenes de claves SSL** está seleccionado. Haga clic en **Nuevo**.
1. Escriba un nombre lógico y una descripción.
1. Especifique la ruta en la que desea crear el almacén de claves. Si ya ha creado un almacén de claves a través de ikeyman, especifique la ruta al archivo del almacén de claves.
1. Especifique y confirme la contraseña.
1. Elija el tipo de almacén de claves y haga clic en **Aplicar**.
1. Guarde la configuración maestra.
1. Haga clic en **Certificado personal**.
1. Si agregó que ya ha creado un almacén de claves con ikeyman, aparecerá el certificado. De lo contrario, debe agregar un nuevo certificado autofirmado siguiendo estos pasos:

   1. Select **Crear > Certificado autofirmado**.
   1. Especifique los valores adecuados en el formulario de certificado. Asegúrese de mantener Alias y el nombre común como nombre de dominio completo del equipo.
   1. Haga clic en **Aplicar**.

1. Repita los pasos del 2 al 10 para crear un almacén de confianza.

## Aplicar almacén de claves personalizado y almacén de confianza al servidor {#apply-custom-keystore-and-truststore-to-the-server}

1. En la Consola administrativa de WebSphere, seleccione **Seguridad > Gestión de claves y certificados SSL**.
1. Haga clic en **Administrar configuración de seguridad de extremo**. Se abre el mapa de topología local.
1. En Inbound, seleccione direct child of nodes.
1. En Elementos relacionados, seleccione **Configuraciones SSL**.
1. Select **NodeDefaultSSLSsetting**.
1. En las listas desplegables nombre del almacén de confianza y nombre del almacén de claves, seleccione el almacén de confianza personalizado y el almacén de claves que ha creado.
1. Haga clic en **Aplicar**.
1. Guarde la configuración maestra.
1. Reinicie el perfil de WebSphere.

   Su perfil ahora se ejecuta en la configuración personalizada de SSL y su certificado.

## Habilitación de la compatibilidad con nativos de formularios AEM {#enabling-support-for-aem-forms-natives}

1. En la Consola administrativa de WebSphere, seleccione **Seguridad > Seguridad global**.
1. En la sección Autenticación , expanda **Seguridad RMI/IIOP** y haga clic en **Comunicaciones entrantes de CSIv2**.
1. Asegúrese de que **Compatible con SSL** está seleccionado en la lista desplegable Transporte .
1. Reinicie el perfil de WebSphere.

## Configuración de WebSphere para convertir direcciones URL que empiecen por https {#configuring-websphere-to-convert-urls-that-begins-with-https}

Para convertir una URL que comience con https, agregue un certificado Signer para esa URL al servidor WebSphere.

**Creación de un certificado Signer para un sitio habilitado para https**

1. Asegúrese de que WebSphere se esté ejecutando.
1. En la Consola Administrativa de WebSphere, vaya a los certificados Firmante y, a continuación, haga clic en Seguridad > Certificado SSL y Administración de claves > Almacenes de claves y certificados > NodeDefaultTrustStore > Certificados Firmantes.
1. Haga clic en Recuperar del puerto y realice estas tareas:

   * En el cuadro Host, escriba la dirección URL. Por ejemplo, escriba `www.paypal.com`.
   * En el cuadro Puerto, escriba `443`. Este puerto es el puerto SSL predeterminado.
   * En el cuadro Alias, escriba un alias.

1. Haga clic en Recuperar información del firmante y, a continuación, verifique que se recupera la información.
1. Haga clic en Aplicar y, a continuación, en Guardar.

La conversión de HTML a PDF desde el sitio cuyo certificado se agrega ahora funcionará desde el servicio Generar PDF.

>[!NOTE]
>
>Para que una aplicación se conecte a sitios SSL desde WebSphere, se requiere un certificado Signer. La utiliza Java Secure Socket Extensions (JSSE) para validar certificados que el lado remoto de la conexión se envía durante un protocolo de enlace SSL.

## Configuración de puertos dinámicos {#configuring-dynamic-ports}

IBM WebSphere no permite múltiples llamadas a ORB.init() cuando la seguridad global está habilitada. Puede leer sobre la restricción permanente en https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704.

Realice los siguientes pasos para configurar el puerto para que sea dinámico y resuelva el problema:

1. En la Consola administrativa de WebSphere, seleccione **Servidores** > **Tipos de servidor** > **Servidor de aplicaciones WebSphere**.
1. En la sección Preferencias , seleccione el servidor.
1. En el **Configuración** en **Comunicaciones** sección, expandir **Puertos** y haga clic en **Detalles**.
1. Haga clic en los siguientes nombres de puerto y cambie la **número de puerto** a 0 y haga clic en **OK**.

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## Configuración del archivo sling.properties {#configure-the-sling-properties-file}

1. Apertura `[aem-forms_root]`\crx-repository\launchpad\sling.properties para editar.
1. Busque la variable `sling.bootdelegation.ibm` propiedad y agregar `com.ibm.websphere.ssl.*`a su campo de valor. El campo actualizado tiene un aspecto similar al siguiente:

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. Guarde el archivo y reinicie el servidor.
