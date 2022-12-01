---
title: Configuración de la autenticación basada en OAuth2 para los protocolos de servidor de correo de Microsoft® Office 365
description: Configuración de la autenticación basada en OAuth2 para los protocolos de servidor de correo de Microsoft® Office 365
source-git-commit: 35595ffca9d2f6fd80bfe93bade247f5b4600469
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 3%

---

# Integración con los protocolos de servidor de correo de Microsoft® Office 365 {#oauth2-support-for-the-microsoft-mail-server-protocols}

Para permitir que las organizaciones cumplan los requisitos de seguridad de los correos electrónicos, AEM Forms ofrece compatibilidad con OAuth 2.0 para la integración con los protocolos de servidor de correo de Microsoft® Office 365. Puede utilizar el servicio de autenticación de Azure Active Directory (Azure AD) OAuth 2.0 para conectarse con varios protocolos, como IMAP, POP o SMTP, y acceder a los datos de correo electrónico de los usuarios de Office 365. A continuación se proporcionan instrucciones paso a paso para configurar los protocolos del servidor de correo de Microsoft® Office 365 para la autenticación mediante el servicio OAuth 2.0:

1. Inicio de sesión [https://portal.azure.com/](https://portal.azure.com/) y busque **Azure Active Directory** en la barra de búsqueda y haga clic en el resultado.
También puede navegar directamente a [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Haga clic en **Agregar** > **Registro de aplicaciones** > **Nuevo registro**

   ![Registro de aplicaciones](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. Rellene la información según sus necesidades y haga clic en **Registro**.
   ![Cuenta admitida](/help/forms/using/assets/azure_suuportedaccountype.png)
En el caso anterior, 
**Cuentas en cualquier directorio organizativo (Cualquier directorio de Azure AD - Multitenant) y cuentas personales de Microsoft® (por ejemplo, Skype, Xbox)** está seleccionada.

   >[!NOTE]
   >
   > * Para **Cuentas en cualquier directorio organizativo (cualquier directorio de Azure AD - Multitenant)** , se recomienda utilizar cuenta de trabajo en lugar de cuenta de correo electrónico personal.
   > * **Solo cuentas Microsoft® personales** y **Inquilino único** no son compatibles.
   > * Se recomienda utilizar **Cuenta Microsoft® personal y de varios inquilinos** aplicación.


1. A continuación, vaya a **Certificados y secretos**, haga clic en **Nuevo secreto de cliente** y siga los pasos que aparecen en la pantalla para crear un secreto. Asegúrese de tomar nota de este valor de secreto para su uso posterior.

   ![Clave secreta](/help/forms/using/assets/azure_secretkey.png)

1. Para añadir permisos, vaya a la aplicación recién creada y seleccione **Permisos de API** > **Añadir un permiso** > **Gráfico Microsoft®** > **Permisos delegados**
1. Seleccione las casillas de verificación de los permisos siguientes para la aplicación y haga clic en **Añadir permiso**:

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![Permiso de API](/help/forms/using/assets/azure_apipermission.png)

1. Select **Autenticación** > **Añadir una plataforma** > **Web** y en la **Direccionamiento Url** , agregue cualquiera de los siguientes URIs (identificador universal de recursos) como:
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   En este caso, `https://login.microsoftonline.com/common/oauth2/nativeclient` se utiliza como URI de redirección.

1. Haga clic en **Configurar** después de añadir cada URL y configurar los ajustes según sus necesidades.
   ![URI de redirección](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > Es obligatorio seleccionar **Tokens de acceso** y **Tokens de ID** casillas de verificación.

1. Haga clic en **Información general** en el panel izquierdo y copie los valores de **ID de aplicación (cliente)**, **ID de directorio (inquilino)** y **Secreto del cliente** para uso posterior.

   ![Información general](/help/forms/using/assets/azure_overview.png)

## Generación del código de autorización {#generating-the-authorization-code}

A continuación, debe generar el código de autorización, tal como se explica en los pasos siguientes:

1. Abra la siguiente URL en el explorador después de reemplazar `clientID` con la variable `<client_id>` y `redirect_uri` con el URI de redireccionamiento de la aplicación:

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

1. Cuando escriba la dirección URL anterior, se le redirigirá a la pantalla de inicio de sesión:
   ![Pantalla de inicio de sesión](/help/forms/using/assets/azure_loginscreen.png)

1. Introduzca el correo electrónico y haga clic en **Siguiente** Aparece la pantalla de permiso de y aplicación:

   ![Permitir permiso](/help/forms/using/assets/azure_permission.png)

1. Una vez que lo permita, se le redirigirá a una nueva dirección URL como: `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. Copiar el valor de `<code>` desde la dirección URL anterior desde `0.ASY...` a `&session_state` en la URL anterior.

## Generación del token de actualización {#generating-the-refresh-token}

A continuación, debe generar el token de actualización, tal como se explica en los pasos siguientes:

1. Abra el símbolo del sistema y utilice el siguiente comando cURL para obtener el token de actualización.

1. Sustituya el `clientID`, `client_secret` y `redirect_uri` con los valores de la aplicación junto con el valor de `<code>`:

   `curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

1. Tenga en cuenta el token de actualización.

## Configuración del servicio de correo electrónico con compatibilidad con OAuth 2.0 {#configureemailservice}

Ahora, debe configurar el servicio de correo electrónico al último servidor JEE mediante el inicio de sesión en la interfaz de usuario de administración:

1. Vaya a **Página principal** > **Servicio** > **Aplicación y servicios** > **Administración de servicios** > **Servicio de correo electrónico**, el **Servicio de correo electrónico de configuración** aparece, configurado para la autenticación básica.

   >[!NOTE]
   >
   > Para habilitar el servicio de autenticación oAuth 2.0, es obligatorio seleccionar **Si el servidor SMTP requiere autenticación (SMTP Authenticate)** casilla de verificación.

1. Establezca **Configuración de autenticación oAuth 2.0** como `True`.
1. Copiar los valores de **ID de cliente** y **Secreto del cliente** desde Azure Portal.
1. Copiar el valor de **Actualizar token**.
1. Inicie sesión en **Workbench** y buscar **Correo electrónico 1.0** from **Selector de actividades**.
1. Hay tres opciones disponibles en Correo electrónico 1.0 como:
   * **Enviar con documento**: Envía correo electrónico con archivos adjuntos únicos.
   * **Enviar con mapa de archivos adjuntos**: Envía correo electrónico con varios archivos adjuntos.
   * **Recibir**: Recibe un correo electrónico de IMAP.

   >[!NOTE]
   >
   >* El protocolo de seguridad de transporte tiene valores válidos como: &#39;blank&#39;, &#39;SSL&#39; o &#39;TLS&#39;. Debe establecer los valores de **Seguridad de transporte SMTP** y **Recibir seguridad de transporte** a **TLS** para activar el servicio de autenticación oAuth.
   >* **Protocolo POP3** no es compatible con OAuth.


   ![Configuración de conexión](/help/forms/using/assets/oauth_connectionsettings.png)

1. Pruebe la aplicación seleccionando **Enviar con documento**.
1. Proporcionar **A** y **De** direcciones.
1. Invoque la aplicación y el correo electrónico se envíe utilizando la autenticación 0Auth 2.0.

   >[!NOTE]
   >
   >Si desea cambiar la configuración de autenticación de autenticación 2.0 a autenticación básica para un proceso en particular en un área de trabajo, puede establecer la variable **Autenticación OAuth 2.0** valor como &#39;False&#39; en **Usar configuración global** en el **Configuración de conexión** pestaña .

## Para habilitar las notificaciones de tareas oAuth {#enable_oauth_task}

1. Vaya a **Página principal** > **Servicios** > **Flujo de trabajo del formulario** > **Configuración del servidor** > **Configuración de correo electrónico**
1. Para habilitar las notificaciones de tareas oAuth, seleccione la opción **Habilitar oAuth** casilla de verificación.
1. Copiar los valores de **ID de cliente** y **Secreto del cliente** desde Azure Portal.
1. Copiar el valor de **Actualizar token**.
1. Haga clic en **Guardar** para guardar los detalles.

   ![Notificación de tarea](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > Para obtener más información relacionada con las notificaciones de tareas, [haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service).

## Para configurar el extremo de correo electrónico {#configure_email_endpoint}

1. Vaya a **Página principal** > **Servicios** > **Aplicación y servicios** > **Administración de extremos**
1. Para configurar el extremo del correo electrónico, establezca **Configuración de autenticación oAuth 2.0** como `True`.
1. Copiar los valores de **ID de cliente** y **Secreto del cliente** desde Azure Portal.
1. Copiar el valor de **Actualizar token**.
1. Haga clic en **Guardar** para guardar los detalles.

   ![Configuración de conexión](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > Para obtener más información sobre la configuración de los extremos de correo electrónico, haga clic en [Configurar un extremo de correo electrónico](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html).

## Solución de problemas {#troubleshooting}

* Si el servicio de correo electrónico no funciona correctamente. Intente volver a generar el `Refresh Token` como se ha descrito anteriormente. El nuevo valor tarda unos minutos en implementarse.

* Error al configurar los detalles del servidor de correo electrónico en el extremo de correo electrónico mediante Workbench. Intente configurar el extremo mediante la IU de administración en lugar de Workbench.

