---
title: SSL de forma predeterminada
seo-title: SSL de forma predeterminada
description: Obtenga información sobre cómo utilizar SSL de forma predeterminada en AEM.
seo-description: Obtenga información sobre cómo utilizar SSL de forma predeterminada en AEM.
uuid: 2fbfd020-1d33-4b22-b963-c698e62f5bf6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
discoiquuid: 68077369-0549-4c0f-901b-952e323013ea
docset: aem65
translation-type: tm+mt
source-git-commit: 93ee9338fc2e78d01a9b62e8040c4674262ef6be
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 0%

---


# SSL de forma predeterminada{#ssl-by-default}

En un esfuerzo por mejorar continuamente la seguridad de AEM, Adobe ha introducido una función llamada SSL de forma predeterminada. El propósito es fomentar el uso de HTTPS para conectarse a AEM instancias.

## Habilitando SSL de forma predeterminada {#enabling-ssl-by-default}

Para configurar SSL de forma predeterminada, haga clic en el mensaje Bandeja de entrada correspondiente en la pantalla de inicio de AEM. Para acceder a la Bandeja de entrada, pulse el icono de la campana en la esquina superior derecha de la pantalla. A continuación, haga clic en **Vista de todo**. Esto mostrará una lista de todas las alertas ordenadas en una vista de lista.

En la lista, seleccione y abra la alerta **Configurar HTTPS**:

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>Si la alerta **Configurar HTTPS** no está presente en la Bandeja de entrada, puede navegar directamente al Asistente para HTTPS si ingresa a *<http://serveraddress:serverport/libs/granite/security/content/sslConfig.html?item=configuration%2fconfiguressl&_charset_=utf-8>*

Se ha creado un usuario de servicio llamado **ssl-service** para esta función. Una vez que abra la alerta, se le guiará a través del siguiente asistente de configuración:

1. Primero, configure las credenciales de la tienda. Estas son las credenciales del almacén de claves del usuario del sistema **ssl-service** que contendrán la clave privada y el almacén de confianza para el detector HTTPS.

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. Una vez ingresadas las credenciales, haga clic en **Siguiente** en la esquina superior derecha de la página. A continuación, cargue la clave privada y el certificado asociados para la conexión SSL.

   ![chlimage_1-106](assets/chlimage_1-105.png)

   >[!NOTE]
   >
   >Para obtener información sobre cómo generar una clave privada y un certificado para usar con el asistente, consulte [este procedimiento](/help/sites-administering/ssl-by-default.md#generating-a-private-key-certificate-pair-to-use-with-the-wizard) a continuación.

1. Por último, especifique el nombre de host HTTPS y el puerto TCP para el detector HTTPS.

   ![screen_shot_2018-07-25at31658pm](assets/screen_shot_2018-07-25at31658pm.png)

## Automatización de SSL de forma predeterminada {#automating-ssl-by-default}

Existen tres maneras de automatizar SSL de manera predeterminada.

### Mediante el POST HTTP {#via-http-post}

El primer método implica la publicación en el servidor SSLSetup que está utilizando el asistente de configuración:

```shell
POST /libs/granite/security/post/sslSetup.html
```

Puede utilizar la siguiente carga útil en el POST para automatizar la configuración:

```xml
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="keystorePassword"

test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="keystorePasswordConfirm"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="truststorePassword"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="truststorePasswordConfirm"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="privatekeyFile"; filename="server.der"
Content-Type: application/x-x509-ca-cert

------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="certificateFile"; filename="server.crt"
Content-Type: application/x-x509-ca-cert

------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="httpsPort"
8443
```

El servlet, como cualquier servlet POST sling, responderá con 200 OK o con un código de estado HTTP de error. Puede encontrar detalles sobre el estado en el cuerpo HTML de la respuesta.

A continuación se muestran ejemplos de una respuesta correcta y de un error.

**EJEMPLO**  DE ÉXITO(status = 200):

```xml
<!DOCTYPE html>
<html lang='en'>
<head>
<title>OK</title>
</head>
<body>
<h1>OK</h1>
<dl>
<dt class='foundation-form-response-status-code'>Status</dt>
<dd>200</dd>
<dt class='foundation-form-response-status-message'>Message</dt>
<dd>SSL successfully configured</dd>
<dt class='foundation-form-response-title'>Title</dt>
<dd>OK</dd>
<dt class='foundation-form-response-description'>Description</dt>
<dd>HTTPS has been configured on port 8443. The private key and
certificate were stored in the key store of the user ssl-service.
Please take note of the key store password you provided. You will need
it for any subsequent updating of the private key or certificate.</dd>
</dl>
<h2>Links</h2>
<ul class='foundation-form-response-links'>
<li><a class='foundation-form-response-redirect' href='/'>Done</a></li>
</ul>
</body>
</html>
```

**EJEMPLO**  DE ERROR(status = 500):

```xml
<!DOCTYPE html>
<html lang='en'>
<head>
<title>Error</title>
</head>
<body>
<h1>Error</h1>
<dl>
<dt class='foundation-form-response-status-code'>Status</dt>
<dd>500</dd>
<dt class='foundation-form-response-status-message'>Message</dt>
<dd>The provided file is not a valid key, DER format expected</dd>
<dt class='foundation-form-response-title'>Title</dt>
<dd>Error</dd>
</dl>
</body>
</html>
```

### Vía el paquete {#via-package}

También puede automatizar la configuración de SSL cargando un paquete que ya contiene estos elementos necesarios:

* El almacén de claves del usuario del servicio ssl. Se encuentra en */home/users/system/security/ssl-service/keystore* en el repositorio.
* La configuración `GraniteSslConnectorFactory`

### Generación de un par de claves privadas/certificados para utilizarlo con el Asistente {#generating-a-private-key-certificate-pair-to-use-with-the-wizard}

A continuación encontrará un ejemplo para crear un certificado autofirmado en formato DER que puede utilizar el Asistente para SSL. Instale OpenSSL en función del sistema operativo, abra el símbolo del sistema OpenSSL y cambie el directorio a la carpeta en la que desee generar el certificado o clave privada.

>[!NOTE]
>
>El uso de un certificado con firma automática es sólo para fines de ejemplo y no debe utilizarse en la producción.

1. En primer lugar, cree la clave privada:

   ```shell
   openssl genrsa -aes256 -out localhostprivate.key 4096
   openssl rsa -in localhostprivate.key -out localhostprivate.key
   ```

1. A continuación, genere una solicitud de firma de certificado (CSR) utilizando la clave privada:

   ```shell
   openssl req -sha256 -new -key localhostprivate.key -out localhost.csr -subj "/CN=localhost"
   ```

1. Genere el certificado SSL y fírmelo con la clave privada. En este ejemplo, caducará dentro de un año:

   ```shell
   openssl x509 -req -days 365 -in localhost.csr -signkey localhostprivate.key -out localhost.crt
   ```

Convertir la clave privada al formato DER. Esto se debe a que el asistente SSL requiere que la clave esté en formato DER:

```shell
openssl pkcs8 -topk8 -inform PEM -outform DER -in localhostprivate.key -out localhostprivate.der -nocrypt
```

Finalmente, cargue el **localhostprivate.der** como Clave privada y **localhost.crt** como certificado SSL en el paso 2 del Asistente gráfico SSL descrito al principio de esta página.

### Actualización de la configuración SSL mediante cURL {#updating-the-ssl-configuration-via-curl}

>[!NOTE]
>
>Consulte [Uso de cURL con AEM](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/curl.html) para obtener una lista centralizada de comandos cURL útiles en AEM.

También puede automatizar la configuración SSL mediante la herramienta cURL. Para ello, publique los parámetros de configuración en esta dirección URL:

*https://&lt;serveraddress>:&lt;serverport>/libs/granite/security/post/sslSetup.html*

A continuación se muestran los parámetros que puede utilizar para cambiar las distintas opciones del asistente de configuración:

* `-F "keystorePassword=password"` - la contraseña del almacén de claves;

* `-F "keystorePasswordConfirm=password"` - confirmar la contraseña del almacén de claves;

* `-F "truststorePassword=password"` - la contraseña del almacén de confianza;

* `-F "truststorePasswordConfirm=password"` - Confirmar la contraseña del almacén de confianza;

* `-F "privatekeyFile=@localhostprivate.der"` - especificar la clave privada;

* `-F "certificateFile=@localhost.crt"` - especificar el certificado;

* `-F "httpsHostname=host.example.com"`- especificar el nombre del host;
* `-F "httpsPort=8443"` - el puerto en el que funcionará el detector HTTPS.

>[!NOTE]
>
>La forma más rápida de ejecutar cURL para automatizar la configuración SSL es desde la carpeta donde se encuentran los archivos DER y CRT. También puede especificar la ruta completa en los argumentos `privatekeyFile` y certificateFile.
>
>También es necesario autenticarse para realizar la actualización, por lo que debe anexar el comando cURL con el parámetro `-u user:passeword`.
>
>Un comando cURL posterior correcto debería tener este aspecto:

```shell
curl -u user:password -F "keystorePassword=password" -F "keystorePasswordConfirm=password" -F "truststorePassword=password" -F "truststorePasswordConfirm=password" -F "privatekeyFile=@localhostprivate.der" -F "certificateFile=@localhost.crt" -F "httpsHostname=host.example.com" -F "httpsPort=8443" https://host:port/libs/granite/security/post/sslSetup.html
```

#### Varios certificados con cURL {#multiple-certificates-using-curl}

Puede enviar el servlet una cadena de certificados repitiendo el parámetro certificateFile de esta forma:

`-F "certificateFile=@root.crt" -F "certificateFile=@localhost.crt"..`

Una vez ejecutado el comando, compruebe que todos los certificados hayan llegado al almacén de claves. Compruebe el almacén de claves desde:
[http://localhost:4502/libs/granite/security/content/userEditor.html/home/users/system/security/ssl-service](http://localhost:4502/libs/granite/security/content/userEditor.html/home/users/system/security/ssl-service)
