---
title: Compatibilidad con OAuth2 para el servicio de correo
description: 'Soporte de Oauth2 para el servicio de correo  '
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 47%

---

# Compatibilidad con OAuth2 para el servicio de correo {#oauth2-support-for-the-mail-service}

AEM as a Cloud Service ofrece compatibilidad con OAuth2 para su servicio de correo integrado, con el fin de permitir que las organizaciones se adhieran a los requisitos de correo electrónico seguros.

Puede configurar OAuth para varios proveedores de correo electrónico. A continuación se proporcionan instrucciones paso a paso para configurar el servicio de correo de AEM para autenticarse mediante OAuth2 con Outlook de Microsoft Office 365. Otros proveedores se pueden configurar de manera similar.

## Microsoft Outlook {#microsoft-outlook}

1. Vaya a [https://portal.azure.com/](https://portal.azure.com/) e inicie sesión.
1. Busque **Azure Active Directory** en la barra de búsqueda y haga clic en el resultado. También puede navegar directamente a [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Haga clic en **Registro de aplicaciones** - **Nuevo registro**

   ![](/help/forms/using/assets/outh_outlook.PNG)

1. Rellene la información según sus necesidades y haga clic en **Registro**
1. Vaya a la aplicación recién creada y seleccione **Permisos de API**
1. Vaya a **Añadir permiso** - **Permiso de gráfico** - **Permisos delegados**
1. Seleccione los siguientes permisos para su aplicación y haga clic en **Añadir permiso**:
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. Vaya a **Autenticación** - **Añadir una plataforma** - **Web** y en la sección **Redirección de URL**, añada las siguientes direcciones URL: una con barra diagonal y otra sin:
   * `http://localhost/`
   * `http://localhost`
1. Pulse **Configurar** después de añadir cada URL y configurar los ajustes según sus necesidades
1. A continuación, vaya a **Certificados y secretos**, haga clic en **Nuevo secreto de cliente** y siga los pasos que aparecen en la pantalla para crear un secreto. Asegúrese de tomar nota de este secreto para utilizarlo posteriormente
1. Press **Información general** en el panel izquierdo y copie los valores de **ID de aplicación (cliente)** para uso posterior.

Para recapitular, necesita la siguiente información para configurar OAuth2 para el servicio de correo en el lado AEM:

* La URL de autenticación en el formulario: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/authorize`
* La URL del token en el formulario: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/token`
* La URL de actualización del formulario: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/token`
* El ID de cliente
* El secreto del cliente

### Generación del token de actualización {#generating-the-refresh-token}

A continuación, debe generar el token de actualización, como se ilustra en un paso posterior.

Para ello, siga estos pasos:

1. Abra la siguiente URL en el explorador después de reemplazar `clientID` con los valores específicos de su cuenta:

   ```https://login.microsoftonline.com/common/oauth2/v2/authorize?client_id=<client_id>&scope=IMAP.AccessAsUser.A;;%20POP.AccessAsUser.All%20SMTP.Send%20User.Read&response_type=code&redirect-uri=http://loginmicrosoftonline.com/common/outh2/nativeclient&prompt=login```

1. Permita, donde sea necesario.
1. La dirección URL se redireccionará a una nueva ubicación, construida con este formato: `http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. Copie el valor de `<code>` en el ejemplo anterior
1. Utilice el siguiente comando cURL para obtener el refreshToken. Reemplace clientID, clientSecret con los valores de su cuenta y el valor de `<code>`:

   ```
   curl -H “ContentType application/x-www-form-urlencoded” -d 
   "client_id=<client-id>
   &scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All&code=M.R3_BAY.1bf609bf-25b3-2fcd-d910-02e02c53bc
   &grant_type=authorization_code
   &redirect_uri= https://login.microsoftonline.com/common/oauth2/nativeclient
   &client_secret=~1E8Q~cz-m6vgOb9m~SI.eF9jSVTbFUiP5f0” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token
   ```

1. Tome nota de refreshToken y accessToken.

### Validación de tokens {#validating-the-tokens}

Antes de configurar OAuth en el lado de AEM, asegúrese de validar accessToken y refreshToken con el siguiente procedimiento:

1. Genere el accessToken utilizando el refreshToken producido en el procedimiento anterior. Puede conseguirlo con el siguiente curl y reemplazando los valores de `<client_id>`,`<client_secret>` junto con la variable `<refreshToken>`:

   ```
   curl -H “ContentType application/x-www-form-urlencoded” -d 
   "client_id=<client_id>
   &scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All&code=<code>
   &grant_type=authorization_code
   &redirect_uri= https://login.microsoftonline.com/common/oauth2/nativeclient
   &client_secret=<client_secret>
   &refresh_token=<refresh_token” 
   -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token
   ```

1. Envíe un correo utilizando accessToken para ver si está funcionando correctamente.

>[!NOTE]
>
> Puede obtener la colección de la API Postman desde [esta ubicación](https://docs.microsoft.com/es-es/azure/active-directory/develop/v2-oauth2-auth-code-flow).

### Configurar el servicio de correo electrónico con compatibilidad con Auth2.0 {#configureemailservice}

Ahora, debe configurar el servicio de correo electrónico al último servidor JEE mediante el inicio de sesión en la interfaz de usuario de administración:

1. Vaya a **Página principal** - **Servicio** - **Aplicación y servicios** - **Administración de servicios** - **Servicio de correo electrónico**
1. **Servicio de correo electrónico de configuración** ventana , configure **SMPT** y **IMP** para la autenticación básica.
1. Para habilitar el servicio de autenticación de correo de Outlook, seleccione **Configuración de autenticación oAuth 2.0** casilla de verificación.
1. Copiar los valores de **ID de cliente** y **Secreto del cliente** desde Azure Portal.
1. Copiar el valor de **Actualizar token**.
1. Haga clic en **Guardar** para guardar los detalles.
1. Inicie sesión en Workbench y busque **Correo electrónico 1.0** from **Selector de actividades**.
1. Hay tres opciones disponibles en Correo electrónico 1.0 como:
   * **Enviar con documento**: Envía correo electrónico con archivos adjuntos únicos.
   * **Enviar con mapa de archivos adjuntos**: Envía correo electrónico con varios archivos adjuntos.
   * **Recibir**: Recibe un correo electrónico de POP3 o IMAP.
1. Pruebe la aplicación seleccionando **Enviar con documento**
1. Proporcionar **A** y **De** direcciones.
1. Invoque la aplicación y el correo electrónico se enviará mediante la autenticación oAuth2.0.

>[!NOTE]
>
> Si desea cambiar la configuración de autenticación de autenticación 2.0 a autenticación básica para un proceso en particular en un área de trabajo, puede desactivar la casilla **Autenticación oAuth2.0** casilla de verificación en **Usar configuración global** en el **Configuración de conexión** pestaña .

### Solución de problemas {#troubleshooting}

Si el servicio de correo no funciona correctamente, vuelva a generar la variable `refreshToken` como se ha descrito anteriormente. El nuevo valor tarda unos minutos en implementarse.


