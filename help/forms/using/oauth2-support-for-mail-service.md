---
title: Configurar la autenticación basada en OAuth2 para los protocolos de servidor de correo de Microsoft® Office 365
description: Configurar la autenticación basada en OAuth2 para los protocolos de servidor de correo de Microsoft® Office 365
exl-id: cd3da71f-892c-4fde-905f-71a64fb5d4e4
source-git-commit: d19de2955adef56570378a6d62ec0015718f9039
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 3%

---

# Integración con los protocolos del servidor de correo de Microsoft® Office 365 {#oauth2-support-for-the-microsoft-mail-server-protocols}

Para permitir que las organizaciones cumplan con los requisitos de correo electrónico seguro, AEM Forms ofrece compatibilidad con OAuth 2.0 para la integración con los protocolos de servidor de correo de Microsoft® Office 365. Puede utilizar el servicio de autenticación OAuth 2.0 de Azure Active Directory (Azure AD) para conectarse con varios protocolos como IMAP, POP o SMTP y acceder a los datos de correo electrónico de los usuarios de Office 365. A continuación se proporcionan instrucciones paso a paso para configurar los protocolos del servidor de correo de Microsoft® Office 365 para autenticarse mediante el servicio OAuth 2.0:

1. Iniciar sesión [https://portal.azure.com/](https://portal.azure.com/) y buscar **Azure Active Directory** en la barra de búsqueda y haga clic en el resultado.
También puede navegar directamente a [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Clic **Añadir** > **Registro de aplicación** > **Nuevo registro**

   ![Registro de aplicaciones](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. Rellene la información según sus necesidades y haga clic en **Registrar**.
   ![Cuenta admitida](/help/forms/using/assets/azure_suuportedaccountype.png)
En el caso anterior, 
**Cuentas en cualquier directorio organizativo (cualquier directorio de Azure AD - Multitenant) y cuentas personales de Microsoft® (por ejemplo, Skype, Xbox)** La opción está seleccionada.

   >[!NOTE]
   >
   > * Para **Cuentas en cualquier directorio organizativo (cualquier directorio de Azure AD - Multitenant)** aplicación, se recomienda utilizar una cuenta de trabajo en lugar de una cuenta de correo electrónico personal.
   > * **Solo cuentas personales de Microsoft®** no se admite la aplicación.
   > * Se recomienda utilizar **Cuenta personal de Microsoft® y de varios inquilinos** aplicación.


1. A continuación, vaya a **Certificados y secretos**, haga clic en **Nuevo secreto de cliente** y siga los pasos que aparecen en pantalla para crear un secreto. Asegúrese de tomar nota de este valor de secret para utilizarlo posteriormente.

   ![Clave secreta](/help/forms/using/assets/azure_secretkey.png)

1. Para añadir permisos, vaya a la aplicación recién creada y seleccione **Permisos de API** > **Añadir un permiso** > **Microsoft® Graph** > **Permisos delegados**
1. Seleccione las casillas de los siguientes permisos para la aplicación y haga clic en **Añadir permiso**:

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![Permiso de API](/help/forms/using/assets/azure_apipermission.png)

1. Seleccionar **Autenticación** > **Añadir una plataforma** > **Web**, y en el **Redirigir direcciones Url** , agregue cualquiera de los siguientes URI (Identificador de recurso universal) como:
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   En este caso, `https://login.microsoftonline.com/common/oauth2/nativeclient` se utiliza como URI de redireccionamiento.

1. Clic **Configurar** después de agregar cada dirección URL, configure los ajustes según sus necesidades.
   ![URI de redirección](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > Es obligatorio seleccionar **Tokens de acceso** y **Tokens de ID** casillas de verificación.

1. Clic **Información general** en el panel izquierdo y copie los valores de **ID de aplicación (cliente)**, **ID de directorio (inquilino)**, y **Secreto del cliente** para su uso posterior.

   ![Información general](/help/forms/using/assets/azure_overview.png)

## Generación del código de autorización {#generating-the-authorization-code}

A continuación, debe generar el código de autorización, tal y como se explica en los pasos siguientes:

1. Abra la siguiente URL en el explorador después de reemplazar `clientID` con el `<client_id>` y `redirect_uri` con el URI de redireccionamiento de la aplicación:

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

   >[!NOTE]
   >
   > En el caso de la aplicación de un solo inquilino, reemplace `common` con su `[tenantid]` en la siguiente URL para generar el código de autorización: `https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/authorize?client_id=[[clientid]]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20openid%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login`

1. Cuando escriba la dirección URL anterior, se le redirigirá a la pantalla de inicio de sesión:
   ![Pantalla de inicio](/help/forms/using/assets/azure_loginscreen.png)

1. Introduzca el correo electrónico y haga clic en **Siguiente** y aparece la pantalla de permisos de la aplicación:

   ![Permitir permiso](/help/forms/using/assets/azure_permission.png)

1. Una vez concedido el permiso, se le redirigirá a una nueva dirección URL como: `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. Copie el valor de `<code>` desde la URL anterior desde `0.ASY...` hasta `&session_state` en la dirección URL anterior.

## Generación del token de actualización {#generating-the-refresh-token}

A continuación, debe generar el token de actualización, tal y como se explica en los pasos siguientes:

1. Abra el símbolo del sistema y utilice el siguiente comando cURL para obtener el refreshToken.

1. Reemplace el `clientID`, `client_secret` y `redirect_uri` con los valores de la aplicación junto con el valor de `<code>`:

   `curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

   >[!NOTE]
   >
   > En la aplicación de un solo inquilino, para generar el token de actualización, utilice el siguiente comando cURL y reemplace `common` con el `[tenantid]` en:
   >`curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/token`

1. Tome nota del token de actualización.

## Configuración del servicio de correo electrónico con compatibilidad con OAuth 2.0 {#configureemailservice}

Ahora, debe configurar el servicio de correo electrónico en el servidor JEE más reciente iniciando sesión en la IU del administrador:

1. Ir a **Inicio** > **Servicio** > **Aplicaciones y servicios** > **Administración de servicios** > **Servicio de correo electrónico**, el **Servicio de correo electrónico de configuración** aparece la ventana, configurada para la autenticación básica.

   >[!NOTE]
   >
   > Para habilitar el servicio de autenticación oAuth 2.0, es obligatorio seleccionar **Si el servidor SMTP requiere autenticación (autenticación SMTP)** casilla de verificación

1. Establecer **Configuración de autenticación de oAuth 2.0** as `True`.
1. Copie los valores de **ID de cliente** y **Secreto del cliente** desde Azure Portal.
1. Copie el valor de **Actualizar token**.
1. Inicie sesión en **Workbench** y buscar **Correo electrónico 1.0** de **Selector de actividades**.
1. Hay tres opciones disponibles en Correo electrónico 1.0 como:
   * **Enviar con documento**: envía correos electrónicos con archivos adjuntos únicos.
   * **Enviar con mapa de archivos adjuntos**: envía correos electrónicos con varios archivos adjuntos.
   * **Recibir**: Recibe un correo electrónico de IMAP.

   >[!NOTE]
   >
   >* El protocolo de seguridad de transporte tiene valores válidos como: &quot;blank&quot;, &quot;SSL&quot; o &quot;TLS&quot;. Debe establecer los valores de **Seguridad de transporte SMTP** y **Seguridad de transporte de recepción** hasta **TLS** para habilitar el servicio de autenticación oAuth.
   >* **Protocolo POP3** no es compatible con OAuth mientras se utilizan extremos de correo electrónico.


   ![Configuración de conexión](/help/forms/using/assets/oauth_connectionsettings.png)

1. Pruebe la aplicación seleccionando **Enviar con documento**.
1. Proporcionar **HASTA** y **Desde** direcciones.
1. Invoque la aplicación y el correo electrónico se enviará con la autenticación 0Auth 2.0.

   >[!NOTE]
   >
   >Si desea cambiar la configuración de autenticación Auth 2.0 a autenticación básica para un proceso determinado en un área de trabajo, puede establecer la variable **Autenticación OAuth 2.0** valor como &quot;False&quot; en **Usar configuración global** en el **Configuración de conexión** pestaña.

## Para habilitar las notificaciones de tareas oAuth {#enable_oauth_task}

1. Ir a **Inicio** > **Servicios** > **Flujo de trabajo de formulario** > **Configuración del servidor** > **Configuración de correo electrónico**
1. Para habilitar las notificaciones de tareas oAuth, seleccione la **Activar oAuth** casilla de verificación
1. Copie los valores de **ID de cliente** y **Secreto del cliente** desde Azure Portal.
1. Copie el valor de **Actualizar token**.
1. Clic **Guardar** para guardar los detalles.

   ![Notificación de tarea](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > Para obtener más información relacionada con las notificaciones de tareas, [haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service).

## Para configurar el extremo de correo electrónico {#configure_email_endpoint}

1. Ir a **Inicio** > **Servicios** > **Aplicaciones y servicios** > **Endpoint Management**
1. Para configurar el extremo del correo electrónico, establezca **Configuración de autenticación de oAuth 2.0** as `True`.
1. Copie los valores de **ID de cliente** y **Secreto del cliente** desde Azure Portal.
1. Copie el valor de **Actualizar token**.
1. Clic **Guardar** para guardar los detalles.

   ![Configuración de conexión](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > Para obtener más información sobre la configuración de los extremos de los correos electrónicos, haga clic en [Configurar un extremo de correo electrónico](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html).

## Solución de problemas {#troubleshooting}

* Si el servicio de correo electrónico no funciona correctamente. Intente volver a generar el `Refresh Token` como se ha descrito anteriormente. El nuevo valor tarda unos minutos en implementarse.

* Error al configurar los detalles del servidor de correo electrónico en el extremo de correo electrónico mediante Workbench. Intente configurar el extremo mediante la IU de administración en lugar de Workbench.
