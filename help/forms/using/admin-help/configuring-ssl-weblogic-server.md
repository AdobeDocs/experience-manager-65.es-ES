---
title: Configuración de SSL para WebLogic Server
seo-title: Configuración de SSL para WebLogic Server
description: Obtenga información sobre cómo crear una credencial SSL para su uso en el servidor WebLogic y cómo configurar SSL para el servidor WebLogic.
seo-description: Obtenga información sobre cómo crear una credencial SSL para su uso en el servidor WebLogic y cómo configurar SSL para el servidor WebLogic.
uuid: 8ee979fd-2615-451b-a607-4f73ecfed4f9
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 968c2574-ec9a-45ca-9c64-66f4caeec285
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Configuración de SSL para WebLogic Server {#configuring-ssl-for-weblogic-server}

Para configurar SSL en el servidor WebLogic, necesita una credencial SSL para la autenticación. Puede utilizar la herramienta de clave de Java para realizar las siguientes tareas a fin de crear una credencial:

* Cree un par de claves pública y privada, ajuste la clave pública en un certificado autofirmado X.509 v1 que se almacene como cadena de certificados de un solo elemento y, a continuación, almacene la cadena de certificados y la clave privada en un nuevo almacén de claves. Este almacén de claves es el almacén de claves de identidad personalizada del servidor de aplicaciones.
* Extraiga el certificado e insértelo en un nuevo almacén de claves. Este almacén de claves es el almacén de claves de confianza personalizada del servidor de aplicaciones.

A continuación, configure WebLogic para que utilice el almacén de claves de identidad personalizada y el almacén de claves de confianza personalizada que ha creado. Además, deshabilite la función de verificación del nombre de host de WebLogic porque el nombre distintivo utilizado para crear los archivos del almacén de claves no incluía el nombre del equipo que aloja WebLogic.

## Creación de credenciales SSL para su uso en WebLogic Server {#creating-an-ssl-credential-for-use-on-weblogic-server}

El comando keytool generalmente se encuentra en el directorio jre/bin de Java y debe incluir varias opciones y valores de opción, que se enumeran en la siguiente tabla.

<table>
 <thead>
  <tr>
   <th><p>Opción de la herramienta Keytool</p></th>
   <th><p>Descripción</p></th>
   <th><p>Valor de opción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>-alias</p></td>
   <td><p>Alias del almacén de claves.</p></td>
   <td>
    <ul>
     <li><p>Almacén de claves de identidad personalizado: <code>ads-credentials</code></p></li>
     <li><p>Almacén de claves de confianza personalizado: <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>El algoritmo que se va a usar para generar el par de claves.</p></td>
   <td><p>RSA</p><p>Puede utilizar un algoritmo diferente, según la política de su compañía.</p></td>
  </tr>
  <tr>
   <td><p>-keystore</p></td>
   <td><p>Ubicación y nombre del archivo del almacén de claves.</p><p>La ubicación puede incluir la ruta absoluta del archivo. O bien, puede ser relativo al directorio actual del símbolo del sistema donde se introduce el comando keytool.</p></td>
   <td>
    <ul>
     <li><p>Almacén de claves de identidad personalizado: <code>[</code><i>appserverdomain]</i><code>/adobe/</code><i>[nombre del servidor]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>Almacén de claves de confianza personalizado: <code>[</code><i>appserverdomain]</i><code>/adobe/</code><i>[nombre del servidor]</i><code>/ads-ca.jks</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-archivo</p></td>
   <td><p>Ubicación y nombre del archivo de certificado.</p></td>
   <td><code> ads-ca.cer</code></td>
  </tr>
  <tr>
   <td><p>-valid</p></td>
   <td><p>Número de días que el certificado se considera válido.</p></td>
   <td><p>3650</p><p>Puede utilizar un valor diferente, según la política de su compañía.</p></td>
  </tr>
  <tr>
   <td><p>-storepass</p></td>
   <td><p>La contraseña que protege el contenido del almacén de claves. </p></td>
   <td>
    <ul>
     <li><p>Almacén de claves de identidad personalizado: La contraseña del almacén de claves debe coincidir con la contraseña de credenciales SSL especificada para el componente Almacén de confianza de la Consola de administración.</p></li>
     <li><p>Almacén de claves de confianza personalizado: Utilice la misma contraseña que utilizó para el almacén de claves de identidad personalizada.</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keypass</p></td>
   <td><p>La contraseña que protege la clave privada del par de claves.</p></td>
   <td><p>Utilice la misma contraseña que utilizó para la <code>-storepass</code> opción. La contraseña de clave debe tener al menos seis caracteres.</p></td>
  </tr>
  <tr>
   <td><p>-dname</p></td>
   <td><p>Nombre distintivo que identifica a la persona propietaria del almacén de claves.</p></td>
   <td><p><code>"CN=</code><code>[User name]</code><code>,OU=</code><code>[Group Name]</code><code>, O=</code><code>[Company Name]</code><code>, L=</code><code>[City Name]</code><code>, S=</code><code>[State or province]</code><code>, C=</code><code>[Country Code]</code><code>"</code></p>
    <ul>
     <li><p><code><i>[User name]</i></code> es la identificación del usuario propietario del almacén de claves.</p></li>
     <li><p><code><i>[Group Name]</i></code> es la identificación del grupo corporativo al que pertenece el propietario del almacén de claves.</p></li>
     <li><p><code><i>[Company Name]</i></code> es el nombre de su organización.</p></li>
     <li><p><code><i>[City Name]</i></code> es la ciudad donde se encuentra su organización.</p></li>
     <li><p><code><i>[State or province]</i></code> es el estado o provincia donde se encuentra su organización.</p></li>
     <li><p><code><i>[Country Code]</i></code> es el código de dos letras del país en el que se encuentra su organización.</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

Para obtener más información sobre el uso del comando keytool, consulte el archivo keytool.html que forma parte de la documentación de JDK.

## Creación de los almacenes de claves Identidad personalizada y Confianza {#create-the-custom-identity-and-trust-keystores}

1. Desde un símbolo del sistema, desplácese hasta *[appserverdomain]*/adobe/*[server name]*.
1. Introduzca el siguiente comando:

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >Reemplace `[JAVA_HOME]`*con el directorio donde está instalado el JDK y reemplace el texto en cursiva por valores que correspondan con su entorno.*

   Por ejemplo:

   ```as3
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   El archivo del almacén de claves de identidad personalizado denominado &quot;ads-dentials.jks&quot; se crea en el directorio [appserverdomain]/adobe/[server name] .

1. Extraiga el certificado del almacén de claves de las credenciales de publicidad introduciendo el siguiente comando:

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**password**

   >[!NOTE]
   >
   >Reemplace `[JAVA_HOME]` con el directorio en el que está instalado JDK y reemplace `store`*_*`password`* por la contraseña del almacén de claves de identidad personalizada.*

   Por ejemplo:

   ```as3
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   El archivo de certificado denominado &quot;ads-ca.cer&quot; se crea en el directorio [appserverdomain]/adobe/[*server name*] .

1. Copie el archivo ads-ca.cer en cualquier equipo host que necesite una comunicación segura con el servidor de aplicaciones.
1. Inserte el certificado en un nuevo archivo de almacén de claves (el almacén de claves de confianza personalizada) mediante el siguiente comando:

   [JAVA_HOME]`/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >Reemplace `[JAVA_HOME]` con el directorio donde está instalado JDK y reemplace `store`*_*`password`y`key`*_* `password` *con sus propias contraseñas.*

   Por ejemplo:

   ```as3
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

El archivo del almacén de claves de confianza personalizado denominado &quot;ads-ca.jks&quot; se crea en el directorio [appserverdomain]/adobe/&#39;server&#39;.

Configure WebLogic para que utilice el almacén de claves de identidad personalizada y el almacén de claves de confianza personalizada que ha creado. Además, deshabilite la función de verificación del nombre de host de WebLogic porque el nombre distintivo utilizado para crear los archivos del almacén de claves no incluía el nombre del equipo que aloja el servidor WebLogic.

## Configurar WebLogic para utilizar SSL {#configure-weblogic-to-use-ssl}

1. Inicio la consola de administración de WebLogic Server escribiendo el nombre `https://`*[de ]*host`:7001/console`en la línea URL de un explorador Web.
1. En Entorno, en Configuraciones de dominio, seleccione **Servidores > &#39;Servidor&#39; > Configuración > General**.
1. En General, en Configuración, asegúrese de que **Escuchar puerto habilitado** y Puerto de escucha **SSL habilitado** están seleccionados. Si no está habilitado, haga lo siguiente:

   1. En el Centro de cambios, haga clic en **Bloquear y editar** para modificar las selecciones y los valores.
   1. Marque las casillas de verificación Puerto de **escucha habilitado** y Puerto de escucha **SSL habilitado** .

1. Si este servidor es un servidor administrado, cambie Puerto de escucha a un valor de puerto no utilizado (como 8001) y Puerto de escucha SSL a un valor de puerto no utilizado (como 8002). En un servidor independiente, el puerto SSL predeterminado es 7002.
1. Haga clic en **Versión de configuración**.
1. En Entorno, en Configuraciones de dominio, haga clic en **Servidores > Servidor [**]administrado > Configuración > General**.
1. En General, en Configuración, seleccione **Palabras clave**.
1. En el Centro de cambios, haga clic en **Bloquear y editar** para modificar las selecciones y los valores.
1. Haga clic en **Cambiar** para obtener la lista del almacén de claves como lista desplegable y seleccione Identidad **personalizada y Confianza** personalizada.
1. En Identidad, especifique los siguientes valores:

   **Custom Identity Keystore**: *[appserverdomain]*/adobe/*[server name]*/ads-credentials.jks, where *[appserverdomain] *is the actual path and *[server name]* is the name of the application server.

   **Tipo** de almacén de claves de identidad personalizada: JKS

   **Custom Identity Keystore Passphrase**: *mypassword* (custom identity keystore password)

1. Under Trust, specify the following values:

   **Custom Trust Keystore File Name**: `*[appserverdomain]*/adobe/*'server'*/ads-ca.jks`, where `*[appserverdomain]*` is the actual path

   **Custom Trust Keystore Type**: JKS

   **Custom Trust Keystore Pass Phrase**: *mypassword* (custom trust key password)

1. Under General, in Configuration, select **SSL**.
1. By default, Keystore is selected for Identity and Trust Locations. If not, change it to keystore.
1. Under Identity, specify the following values:

   **Private Key Alias**: ads-credentials

   **Passphrase**: *mypassword*

1. Click **Release Configuration**.

## Disable the Hostname Verification feature {#disable-the-hostname-verification-feature}

1. On the Configuration tab, click SSL.
1. Under Advanced, select None from the Hostname Verification list.

   If Hostname Verification is not disabled, the Common Name (CN) must contain the server host name.

1. Under Change Center, click Lock &amp; Edit to modify selections and values.
1. Reinicie el servidor de aplicaciones.

