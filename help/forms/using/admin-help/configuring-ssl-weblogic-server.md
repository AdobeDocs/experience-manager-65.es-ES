---
title: Configuración de SSL para WebLogic Server
seo-title: Configuring SSL for WebLogic Server
description: Obtenga información sobre cómo crear una credencial SSL para utilizarla en el servidor de WebLogic y cómo configurar SSL para el servidor de WebLogic.
seo-description: Learn how to create an SSL credential for use on WebLogic server and how to configure SSL for WebLogic Server.
uuid: 8ee979fd-2615-451b-a607-4f73ecfed4f9
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 968c2574-ec9a-45ca-9c64-66f4caeec285
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 1%

---


# Configuración de SSL para WebLogic Server {#configuring-ssl-for-weblogic-server}

Para configurar SSL en WebLogic Server, necesita una credencial SSL para la autenticación. Puede utilizar la herramienta clave de Java para realizar las siguientes tareas y crear una credencial:

* Cree un par de claves pública y privada, ajuste la clave pública en un certificado autofirmado X.509 v1 que se almacene como una cadena de certificados de un solo elemento y, a continuación, almacene la cadena de certificados y la clave privada en un nuevo almacén de claves. Este repositorio de claves es el repositorio de claves de identidad personalizada del servidor de aplicaciones.
* Extraiga el certificado e insértelo en un nuevo repositorio de claves. Este repositorio de claves es el repositorio de claves de confianza personalizada del servidor de aplicaciones.

A continuación, configure WebLogic de modo que utilice el almacén de claves de identidad personalizada y el almacén de claves de confianza personalizada que ha creado. Además, deshabilite la función Verificación de nombre de host de WebLogic porque el nombre distintivo utilizado para crear los archivos del almacén de claves no incluía el nombre del equipo que aloja WebLogic.

## Creación de una credencial SSL para su uso en WebLogic Server {#creating-an-ssl-credential-for-use-on-weblogic-server}

El comando keytool se encuentra generalmente en el directorio Java jre/bin y debe incluir varias opciones y valores de opción, que se enumeran en la siguiente tabla.

<table>
 <thead>
  <tr>
   <th><p>Opción Keytool</p></th>
   <th><p>Descripción</p></th>
   <th><p>Valor de opción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>-alias</p></td>
   <td><p>El alias del almacén de claves.</p></td>
   <td>
    <ul>
     <li><p>Almacén de claves de identidad personalizado: <code>ads-credentials</code></p></li>
     <li><p>Almacén de claves de confianza personalizada: <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>Algoritmo que se utiliza para generar el par de claves.</p></td>
   <td><p>RSA</p><p>Puede utilizar un algoritmo diferente, según la política de su compañía.</p></td>
  </tr>
  <tr>
   <td><p>-keystore</p></td>
   <td><p>Ubicación y nombre del archivo de almacén de claves.</p><p>La ubicación puede incluir la ruta absoluta del archivo. O bien, puede ser relativa al directorio actual del símbolo del sistema donde se introduce el comando keytool.</p></td>
   <td>
    <ul>
     <li><p>Almacén de claves de identidad personalizado: <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[nombre del servidor]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>Almacén de claves de confianza personalizada: <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[nombre del servidor]</i><code>/ads-ca.jks</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-file</p></td>
   <td><p>La ubicación y el nombre del archivo de certificado.</p></td>
   <td><code> ads-ca.cer</code></td>
  </tr>
  <tr>
   <td><p>-validez</p></td>
   <td><p>Número de días durante los cuales el certificado se considera válido.</p></td>
   <td><p>3650</p><p>Puede utilizar un valor diferente, según la política de su compañía.</p></td>
  </tr>
  <tr>
   <td><p>-storepass</p></td>
   <td><p>Contraseña que protege el contenido del almacén de claves. </p></td>
   <td>
    <ul>
     <li><p>Almacén de claves de identidad personalizado: la contraseña del almacén de claves debe corresponder a la contraseña de credencial SSL especificada para el componente Almacén de confianza de la consola de administración.</p></li>
     <li><p>Almacén de claves de confianza personalizado: utilice la misma contraseña que utilizó para el almacén de claves de identidad personalizada.</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keypass</p></td>
   <td><p>Contraseña que protege la clave privada del par de claves.</p></td>
   <td><p>Utilice la misma contraseña que utilizó para el <code>-storepass</code> opción. La contraseña de la clave debe tener al menos seis caracteres.</p></td>
  </tr>
  <tr>
   <td><p>-dname</p></td>
   <td><p>Nombre distintivo que identifica a la persona propietaria del almacén de claves.</p></td>
   <td><p><code>"CN=</code><code>[User name]</code><code>,OU=</code><code>[Group Name]</code><code>, O=</code><code>[Company Name]</code><code>, L=</code><code>[City Name]</code><code>, S=</code><code>[State or province]</code><code>, C=</code><code>[Country Code]</code><code>"</code></p>
    <ul>
     <li><p><code><i>[User name]</i></code> es la identificación del usuario propietario del almacén de claves.</p></li>
     <li><p><code><i>[Group Name]</i></code> es la identificación del grupo corporativo al que pertenece el propietario del almacén de claves.</p></li>
     <li><p><code><i>[Company Name]</i></code> es el nombre de su organización.</p></li>
     <li><p><code><i>[City Name]</i></code> es la ciudad en la que se encuentra su organización.</p></li>
     <li><p><code><i>[State or province]</i></code> es el estado o la provincia donde se encuentra su organización.</p></li>
     <li><p><code><i>[Country Code]</i></code> es el código de dos letras del país en el que se encuentra su organización.</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

Para obtener más información sobre el uso del comando keytool, consulte el archivo keytool.html que forma parte de la documentación de JDK.

## Crear los almacenes de claves Identidad personalizada y Confianza {#create-the-custom-identity-and-trust-keystores}

1. Desde un símbolo del sistema, vaya a *[appserverdomain]*/adobe/*[nombre del servidor]*.
1. Introduzca el siguiente comando:

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >Reemplazar `[JAVA_HOME]`*con el directorio en el que está instalado el JDK y reemplace el texto en cursiva por valores que se correspondan con su entorno.*

   Por ejemplo:

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   El archivo del almacén de claves de identidad personalizada llamado &quot;ads-credentials.jks&quot; se crea en [appserverdomain]/adobe/[nombre del servidor] directorio.

1. Extraiga el certificado del almacén de claves ads-credentials introduciendo el siguiente comando:

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**contraseña**

   >[!NOTE]
   >
   >Reemplazar `[JAVA_HOME]` con el directorio en el que está instalado el JDK y reemplace `store`*_* `password`* con la contraseña del almacén de claves de identidad personalizada.*

   Por ejemplo:

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   El archivo de certificado denominado &quot;ads-ca.cer&quot; se crea en la variable [appserverdomain]/adobe/[*nombre del servidor*] directorio.

1. Copie el archivo ads-ca.cer en cualquier equipo host que necesite una comunicación segura con el servidor de aplicaciones.
1. Inserte el certificado en un nuevo archivo de almacén de claves (el almacén de claves de confianza personalizada) introduciendo el siguiente comando:

   [JAVA_HOME] `/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >Reemplazar `[JAVA_HOME]` con el directorio en el que está instalado el JDK y reemplace `store`*_* `password` y `key`*_* `password` *con sus propias contraseñas.*

   Por ejemplo:

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

El archivo del almacén de claves de confianza personalizada llamado &quot;ads-ca.jks&quot; se crea en la variable [appserverdomain]directorio /adobe/&#39;server&#39;.

Configure WebLogic de modo que utilice el repositorio de claves de identidad personalizada y el repositorio de claves de confianza personalizada que ha creado. Además, deshabilite la función de comprobación del nombre de host de WebLogic porque el nombre distintivo utilizado para crear los archivos del almacén de claves no incluía el nombre del equipo que aloja WebLogic Server.

## Configuración de WebLogic para utilizar SSL {#configure-weblogic-to-use-ssl}

1. Inicie la consola de administración de WebLogic Server escribiendo `https://`*[nombre de host ]*`:7001/console` en la línea URL de un explorador web.
1. En Entorno, en Configuraciones de dominio, seleccione **Servidores > &quot;server&quot; > Configuración > General**.
1. En General, en Configuración, asegúrese de que **Puerto de escucha habilitado** y **Puerto de escucha SSL habilitado** están seleccionados. Si no está activada, haga lo siguiente:

   1. En el Centro de cambios, haga clic en **Bloquear y editar** para modificar selecciones y valores.
   1. Compruebe la **Puerto de escucha habilitado** y **Puerto de escucha SSL habilitado** casillas de verificación.

1. Si este servidor es un servidor administrado, cambie Puerto de escucha por un valor de puerto no utilizado (como 8001) y Puerto de escucha SSL por un valor de puerto no utilizado (como 8002). En un servidor independiente, el puerto SSL predeterminado es 7002.
1. Clic **Configuración de versión**.
1. En Entorno, en Configuraciones de dominio, haga clic en **Servidores > [*Servidor administrado*] > Configuración > General**.
1. En General, en Configuración, seleccione **Almacenes de claves**.
1. En el Centro de cambios, haga clic en **Bloquear y editar** para modificar selecciones y valores.
1. Clic **Cambiar** a para obtener la lista de almacén de claves como lista desplegable y seleccione **Identidad Personalizada Y Confianza Personalizada**.
1. En Identidad, especifique los siguientes valores:

   **Almacén de claves de identidad personalizado**: *[appserverdomain]*/adobe/*[nombre del servidor]*/ads-credentials.jks, donde *[appserverdomain] * es la ruta real y *[nombre del servidor]* es el nombre del servidor de aplicaciones.

   **Tipo de almacén de claves de identidad personalizada**: JKS

   **Frase de clave de identidad personalizada**: *mypassword* (contraseña del almacén de claves de identidad personalizada)

1. En Confianza, especifique los siguientes valores:

   **Nombre de archivo del almacén de claves de confianza personalizada**: `*[appserverdomain]*/adobe/*'server'*/ads-ca.jks`, donde `*[appserverdomain]*` es la ruta real

   **Tipo de almacén de claves de confianza personalizada**: JKS

   **Frase de contraseña de almacén de claves de confianza personalizada**: *mypassword* (contraseña de clave de confianza personalizada)

1. En General, en Configuración, seleccione **SSL**.
1. De forma predeterminada, la opción Almacén de claves está seleccionada para Ubicaciones de identidad y confianza. Si no es así, cámbielo a almacén de claves.
1. En Identidad, especifique los siguientes valores:

   **Alias de clave privada**: ads-credentials

   **Frase de contraseña**: *mypassword*

1. Clic **Configuración de versión**.

## Desactivar la función de verificación del nombre de host {#disable-the-hostname-verification-feature}

1. En la pestaña Configuración, haga clic en SSL.
1. En Avanzado, seleccione Ninguno en la lista Verificación de nombre de host.

   Si la verificación del nombre de host no está desactivada, el nombre común (CN) debe contener el nombre de host del servidor.

1. En Centro de cambios, haga clic en Bloquear y editar para modificar las selecciones y los valores.
1. Reinicie el servidor de la aplicación.

