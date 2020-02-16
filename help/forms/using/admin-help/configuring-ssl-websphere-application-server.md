---
title: Configuración de SSL para el servidor de aplicaciones WebSphere
seo-title: Configuración de SSL para el servidor de aplicaciones WebSphere
description: Obtenga información sobre cómo configurar SSL para el servidor de aplicaciones WebSphere.
seo-description: Obtenga información sobre cómo configurar SSL para el servidor de aplicaciones WebSphere.
uuid: f939a806-346e-41e0-b2c0-6d0ba83f8f6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7c0efcb3-5b07-4090-9119-b7318c8b7980
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# Configuración de SSL para el servidor de aplicaciones WebSphere {#configuring-ssl-for-websphere-application-server}

Esta sección incluye los siguientes pasos para configurar SSL con el servidor de aplicaciones IBM WebSphere.

## Creación de una cuenta de usuario local en WebSphere {#creating-a-local-user-account-on-websphere}

Para habilitar SSL, WebSphere necesita acceder a una cuenta de usuario en el registro de usuarios del sistema operativo local que tenga permiso para administrar el sistema:

* (Windows) Cree un nuevo usuario de Windows que forme parte del grupo Administradores y tenga el privilegio de actuar como parte del sistema operativo. (Consulte [Creación de un usuario de Windows para WebSphere](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere)).
* (Linux, UNIX) El usuario puede ser un usuario raíz u otro usuario que tenga privilegios de root. Cuando habilite SSL en WebSphere, utilice la identificación del servidor y la contraseña de este usuario.

### Crear un usuario de Linux o UNIX para WebSphere {#create-a-linux-or-unix-user-for-websphere}

1. Inicie sesión como usuario raíz.
1. Cree un usuario introduciendo el siguiente comando en un símbolo del sistema:

   * (Linux y Sun Solaris) `useradd`
   * (IBM AIX) `mkuser`

1. Para configurar la contraseña del nuevo usuario, ingrese `passwd` en el símbolo del sistema.
1. (Linux y Solaris) Para crear un archivo de contraseña de sombra, introduzca `pwconv` (sin parámetros) en el símbolo del sistema.

   >[!NOTE]
   >
   >(Linux y Solaris) Para que funcione el registro de seguridad del sistema operativo local de WebSphere Application Server, debe existir un archivo de contraseña de sombra. El archivo de contraseña de sombra se denomina generalmente **/etc/Shadow** y se basa en el archivo /etc/passwd. Si el archivo de contraseña de sombra no existe, se producirá un error después de habilitar la seguridad global y configurar el registro de usuarios como sistema operativo local.

1. Abra el archivo de grupo desde el directorio /etc en un editor de texto.
1. Agregue al grupo el usuario que creó en el paso 2. `root`
1. Guarde y cierre el archivo.
1. (UNIX con SSL habilitado) Inicie y detenga WebSphere como usuario raíz.

### Crear un usuario de Windows para WebSphere {#create-a-windows-user-for-websphere}

1. Inicie sesión en Windows con una cuenta de usuario de administrador.
1. Seleccione **Inicio > Panel de control > Herramientas administrativas > Administración de equipos > Usuarios y grupos** locales.
1. Haga clic con el botón derecho en Usuarios y seleccione **Nuevo usuario**.
1. Escriba un nombre de usuario y una contraseña en los cuadros correspondientes y escriba cualquier otra información que necesite en los cuadros restantes.
1. Anule la selección de **Usuario debe cambiar la contraseña en el próximo inicio de sesión**, haga clic en **Crear** y, a continuación, haga clic en **Cerrar**.
1. Haga clic en **Usuarios**, haga clic con el botón secundario en el usuario que acaba de crear y seleccione **Propiedades**.
1. Haga clic en la ficha **Miembro** y, a continuación, haga clic en **Agregar**.
1. En el cuadro Escriba los nombres de los objetos que desea seleccionar, haga clic en Comprobar nombres para asegurarse de que el nombre del grupo es correcto. `Administrators`
1. Haga clic en **Aceptar** y, a continuación, en **Aceptar** de nuevo.
1. Seleccione **Inicio > Panel de control > Herramientas administrativas > Directiva de seguridad local > Directivas** locales.
1. Haga clic en Asignación de derechos de usuario y, a continuación, haga clic con el botón secundario en Accionar como parte del sistema operativo y seleccione Propiedades.
1. Click **Add User or Group**.
1. En el cuadro Escriba los nombres de los objetos que desea seleccionar, escriba el nombre del usuario que creó en el paso 4, haga clic en **Comprobar nombres** para asegurarse de que el nombre es correcto y, a continuación, haga clic en **Aceptar**.
1. Haga clic en **Aceptar** para cerrar el cuadro de diálogo Propiedades del sistema operativo.

### Configure WebSphere para utilizar al usuario recién creado como administrador {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. Asegúrese de que WebSphere se esté ejecutando.
1. En la Consola administrativa de WebSphere, seleccione **Seguridad > Seguridad** global.
1. En Seguridad administrativa, seleccione Funciones de usuario **administrativas**.
1. Haga clic en Agregar y haga lo siguiente:

   1. **Type**&amp;ast; en el cuadro de búsqueda y haga clic en buscar.
   1. Haga clic en **Administrador** en Funciones.
   1. Agregue el usuario recién creado a Asignado a la función y asígnelo al administrador.

1. Click **OK** and save your changes.
1. Reinicie el perfil de WebSphere.

## Habilitar seguridad administrativa {#enable-administrative-security}

1. En la Consola administrativa de WebSphere, seleccione **Seguridad > Seguridad** global.
1. Haga clic en Asistente **de configuración de seguridad**.
1. Asegúrese de que la casilla **Activar seguridad** de la aplicación está activada. Haga clic en **Siguiente**. 
1. Seleccione **Repositorios** federados y haga clic en **Siguiente**.
1. Especifique las credenciales que desee configurar y haga clic en **Siguiente**.
1. Click **Finish**.
1. Reinicie el perfil de WebSphere.

   WebSphere comenzará a utilizar el almacén de claves y el almacén de confianza predeterminados.

## Habilitar SSL (clave personalizada y almacén de confianza) {#enable-ssl-custom-key-and-truststore}

Los almacenes de confianza y los almacenes de claves se pueden crear con la utilidad ikeyman o la consola de administración. Para que ikeyman funcione correctamente, asegúrese de que la ruta de instalación de WebSphere no contenga paréntesis.

1. En la Consola de administración de WebSphere, seleccione **Seguridad > Certificado SSL y administración** de claves.
1. Haga clic en **Almacenes de claves y certificados** en Elementos relacionados.
1. En la lista desplegable de usos **del almacén de** claves, asegúrese de que esté seleccionada la opción Almacenes **de claves** SSL. Haga clic en **Nuevo**.
1. Escriba un nombre lógico y una descripción.
1. Especifique la ruta en la que desea que se cree el almacén de claves. Si ya ha creado un almacén de claves mediante ikeyman, especifique la ruta al archivo de almacén de claves.
1. Especifique y confirme la contraseña.
1. Elija el tipo de almacén de claves y haga clic en **Aplicar**.
1. Guarde la configuración maestra.
1. Haga clic en Certificado **personal**.
1. Si ya ha creado un almacén de claves con ikeyman, aparecerá el certificado. De lo contrario, deberá agregar un nuevo certificado con firma automática siguiendo estos pasos:

   1. Seleccione **Crear > Certificado** con firma automática.
   1. Especifique los valores adecuados en el formulario de certificado. Asegúrese de mantener Alias y nombre común como nombre de dominio completo del equipo.
   1. Haga clic en **Aplicar**.

1. Repita los pasos del 2 al 10 para crear un almacén de confianza.

## Aplicar almacén de claves y almacén de confianza personalizados al servidor {#apply-custom-keystore-and-truststore-to-the-server}

1. En la Consola de administración de WebSphere, seleccione **Seguridad > Certificado SSL y administración** de claves.
1. Haga clic en **Administrar configuración** de seguridad de extremo. Se abre el mapa de topología local.
1. En Entrante, seleccione secundario directo de nodos.
1. En Elementos relacionados, seleccione Configuraciones **** SSL.
1. Seleccione **NodeDefaultSSLSeteo**.
1. En las listas desplegables de nombre de almacén de confianza y nombre de almacén de claves, seleccione el almacén de confianza personalizado y el almacén de claves que ha creado.
1. Haga clic en **Aplicar**.
1. Guarde la configuración maestra.
1. Reinicie el perfil de WebSphere.

   Su perfil ahora se ejecuta con la configuración SSL personalizada y su certificado.

## Activación de la compatibilidad con formularios nativos de AEM {#enabling-support-for-aem-forms-natives}

1. En la Consola administrativa de WebSphere, seleccione **Seguridad > Seguridad** global.
1. En la sección Autenticación, expanda la seguridad **de** RMI/IIOP y haga clic en Comunicaciones **entrantes de** CSIv2.
1. Asegúrese de que la opción Compatible con **** SSL está seleccionada en la lista desplegable Transporte.
1. Reinicie el perfil de WebSphere.

## Configuración de WebSphere para convertir direcciones URL que empiecen por https {#configuring-websphere-to-convert-urls-that-begins-with-https}

Para convertir una dirección URL que empiece por https, agregue un certificado de firmante para esa dirección URL al servidor WebSphere.

**Crear un certificado de firmante para un sitio habilitado para https**

1. Asegúrese de que WebSphere se esté ejecutando.
1. En la Consola administrativa de WebSphere, vaya a los certificados Firmante y, a continuación, haga clic en Seguridad > Administración de certificados SSL y claves > Almacenes y certificados clave > NodeDefaultTrustStore > Certificados firmantes.
1. Haga clic en Recuperar del puerto y realice las siguientes tareas:

   * En el cuadro Host, escriba la dirección URL. For example, type `www.paypal.com`.
   * En el cuadro Puerto, escriba `443`. Este puerto es el puerto SSL predeterminado.
   * En el cuadro Alias, escriba un alias.

1. Haga clic en Recuperar información del firmante y, a continuación, verifique que se recuperó la información.
1. Haga clic en Aplicar y, a continuación, en Guardar.

La conversión de HTML a PDF desde el sitio cuyo certificado se agrega ahora funcionará desde el servicio Generar PDF.

>[!NOTE]
>
>Para que una aplicación se conecte a sitios SSL desde WebSphere, se requiere un certificado de firmante. Java Secure Socket Extensions (JSSE) lo utiliza para validar certificados que el lado remoto de la conexión se envía durante un protocolo de enlace SSL.

## Configuración de puertos dinámicos {#configuring-dynamic-ports}

IBM WebSphere no permite múltiples llamadas a ORB.init() cuando Global Security está habilitado. Puede leer sobre la restricción permanente en https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704.

Realice los siguientes pasos para establecer que el puerto sea dinámico y resolver el problema:

1. En la Consola administrativa de WebSphere, seleccione **Servidores** > Tipos **** de servidores > Servidor **de aplicaciones de** WebSphere.
1. En la sección Preferencias, seleccione el servidor.
1. En la ficha **Configuración** , en la sección **Comunicaciones** , expanda **Puertos** y haga clic en **Detalles**.
1. Haga clic en los siguientes nombres de puerto, cambie el número **de** puerto a 0 y haga clic en **Aceptar**.

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## Configuración del archivo sling.properties {#configure-the-sling-properties-file}

1. Abra el `[aem-forms_root]`archivo \crx-repository\launchpad\sling.properties para editarlo.
1. Busque la `sling.bootdelegation.ibm` propiedad y añádala `com.ibm.websphere.ssl.*`a su campo de valor. El campo actualizado tiene el siguiente aspecto:

   ```as3
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. Guarde el archivo y reinicie el servidor.

