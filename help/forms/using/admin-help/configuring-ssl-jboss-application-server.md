---
title: Configuración de SSL para el servidor de aplicaciones JBoss
seo-title: Configuración de SSL para el servidor de aplicaciones JBoss
description: Obtenga información sobre cómo configurar SSL para el servidor de aplicaciones JBoss.
seo-description: Obtenga información sobre cómo configurar SSL para el servidor de aplicaciones JBoss.
uuid: 7c13cf00-ea89-4894-a4fc-aaeec7ae9f66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c187daa4-41b7-47dc-9669-d7120850cafd
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---


# Configuración de SSL para el servidor de aplicaciones JBoss {#configuring-ssl-for-jboss-application-server}

Para configurar SSL en el servidor de aplicaciones JBoss, necesita una credencial SSL para la autenticación. Puede utilizar la herramienta de clave de Java para crear una credencial o una solicitud e importar una credencial desde una entidad de certificación (CA). Luego debe habilitar SSL en JBoss.

Puede ejecutar keytool utilizando un único comando que incluya toda la información necesaria para crear el almacén de claves.

En este procedimiento:

* `[appserver root]` es el directorio principal del servidor de aplicaciones que ejecuta AEM formularios.
* `[type]` es un nombre de carpeta que varía según el tipo de instalación que haya realizado.

## Crear una credencial SSL {#create-an-ssl-credential}

1. En un símbolo del sistema, navegue hasta *[JAVA HOME]*/bin y escriba el siguiente comando para crear la credencial y el almacén de claves:

   `keytool -genkey -dname "CN=`*Nombre* `, OU=`*del host* `, O=`*Nombre del grupo Nombre de la empresa* `,L=`*Nombre de la ciudad* `, S=`** `, C=`Nombre del estado Código del país&quot;  `-alias "AEMForms Cert"` `-keyalg RSA -keypass`*key_* `-keystore`*password nombredeclave* `.keystore`

   >[!NOTE]
   >
   >Reemplace `[JAVA_HOME]` por el directorio donde está instalado el JDK y reemplace el texto en cursiva por valores que correspondan con su entorno. Nombre de host es el nombre de dominio completo del servidor de aplicaciones.

1. Introduzca `keystore_password` cuando se le solicite una contraseña. La contraseña del almacén de claves y la clave deben ser idénticas.

   >[!NOTE]
   >
   >El `keystore_password` *introducido en este paso puede ser la misma contraseña (key_password) que especificó en el paso 1, o puede ser diferente.*

1. Copie el *keystorename*.keystore en el directorio `[appserver root]/server/[type]/conf` escribiendo uno de los siguientes comandos:

   * (Windows Single Server) `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * (Clúster de Windows Server) copia `keystorename.keystore[appserver root]\domain\configuration`
   * (Linux Single Server) `cp keystorename.keystore [appserver root]/standalone/configuration`
   * (Clúster de servidor Linux) `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. Exporte el archivo de certificado escribiendo el siguiente comando:

   * (Servidor único) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * (Clúster de servidor) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. Introduzca la *contraseña de keystore* cuando se le solicite una contraseña.
1. Copie el archivo AEMForms_cert.cer en el directorio *[appserver root] \conf* escribiendo el siguiente comando:

   * (Windows Single Server) `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * (Clúster de Windows Server) `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * (Linux Single Server) `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * (Clúster de servidor Linux) `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. Para vista del contenido del certificado, escriba el siguiente comando:

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. Para proporcionar acceso de escritura al archivo cacerts en `[JAVA_HOME]\jre\lib\security`, si es necesario, lleve a cabo la siguiente tarea:

   * (Windows) Haga clic con el botón derecho en el archivo cacerts, seleccione Propiedades y, a continuación, anule la selección del atributo de sólo lectura.
   * (Linux) Tipo `chmod 777 cacerts`

1. Importe el certificado escribiendo el siguiente comando:

   `keytool -import -alias “AEMForms Cert” -file`*AEMForms_* `.cer -keystore`*certJAVA_HOME* `\jre\lib\security\cacerts`

1. Escriba `changeit` como contraseña. Esta contraseña es la contraseña predeterminada para una instalación de Java y es posible que la haya cambiado el administrador del sistema.
1. Cuando se le pida `Trust this certificate? [no]`:, escriba `yes`. Se muestra la confirmación de &quot;Se agregó el certificado al almacén de claves&quot;.
1. Si se está conectando a través de SSL desde Workbench, instale el certificado en el equipo de Workbench.
1. En un editor de texto, abra los siguientes archivos para editarlos:

   * Servidor único: `[appserver root]`/standalone/configuration/lc_&lt;dbname/turnkey>.xml

   * Clúster del servidor: `[appserver root]`/domain/configuration/host.xml

   * Clúster del servidor: `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **Para un único servidor,** en el archivo lc_&lt;dbaname>.xml, agregue la siguiente  &lt;security-realms> sección:

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   Busque la sección `<server>` presente después del siguiente código:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Añada lo siguiente en la sección &lt;server> presente después del código anterior:

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **Para el clúster de servidores,** en  [appserver root]\domain\configuration\host.xml en todos los nodos, agregue lo siguiente después de la  &lt;security-realms> sección:

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   En el nodo principal del clúster de servidores, en la [raíz de appserver]\domain\configuration\domain_&lt;dbname>.xml, busque la sección &lt;server> presente después del siguiente código:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Añada lo siguiente en la sección &lt;server> presente después del código anterior:

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. Cambie el valor del atributo `keystoreFile` y el atributo `keystorePass` a la contraseña del almacén de claves que especificó al crear el almacén de claves.
1. Reinicie el servidor de aplicaciones:

   * Para instalaciones llave en mano:

      * En el Panel de control de Campaign de Windows, haga clic en Herramientas administrativas y, a continuación, en Servicios.
      * Seleccione JBoss para formularios Adobe Experience Manager.
      * Seleccione Acción > Detener.
      * Espere a que el estado del servicio aparezca como detenido.
      * Seleccione Acción > Inicio.
   * Para instalaciones de JBoss preconfiguradas o configuradas manualmente por Adobe:

      * Desde un símbolo del sistema, desplácese a *`[appserver root]`*/bin.
      * Para detener el servidor, introduzca el siguiente comando:

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * Espere hasta que el proceso de JBoss se haya cerrado completamente (cuando el proceso de JBoss devuelve el control al terminal en el que se inició).
      * Introduzca el siguiente comando para inicio del servidor:

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`



1. Para acceder a la consola de administración mediante SSL, escriba `https://[host name]:'port'/adminui` en un explorador Web:

   El puerto SSL predeterminado para JBoss es 8443. A partir de aquí, especifique este puerto al acceder a AEM formularios.

## Solicitar una credencial de una CA {#request-a-credential-from-a-ca}

1. En un símbolo del sistema, navegue hasta *[JAVA HOME]*/bin y escriba el siguiente comando para crear el almacén de claves y la clave:

   `keytool -genkey -dname "CN=`*Nombre* `, OU=`*de host* `, O=`*Nombre de grupo Nombre de* `, L=`*empresa* `, S=`** `, C=`*Nombre de la ciudad Código* de estado&quot;  `-alias "AEMForms Cert"` `-keyalg RSA -keypass`-*key_* `-keystore`*pass_keystorename* `.keystore`

   >[!NOTE]
   >
   >Reemplace *`[JAVA_HOME]`* por el directorio donde está instalado el JDK y reemplace el texto en cursiva por valores que correspondan con su entorno.

1. Escriba el siguiente comando para generar una solicitud de certificado que se enviará a la autoridad de certificación:

   `keytool -certreq -alias` &quot;Cert AEMForms&quot;  `-keystore`** `.keystore -file`*keystorenameAEMFormscertRequest.csr*

1. Cuando se complete la solicitud de un archivo de certificado, complete el siguiente procedimiento.

## Utilice una credencial obtenida de una CA para habilitar SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. En un símbolo del sistema, navegue hasta *`[JAVA HOME]`*/bin y escriba el siguiente comando para importar el certificado raíz de la CA con la que se ha firmado el CSR:

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   Si el certificado raíz no está en el explorador, impórtelo también allí.

   >[!NOTE]
   >
   >Reemplace *`[JAVA_HOME]`por el directorio donde está instalado el JDK y reemplace el texto en cursiva por valores que correspondan con su entorno.*

1. En un símbolo del sistema, navegue hasta *`[JAVA HOME]`*/bin y escriba el siguiente comando para importar la credencial en el almacén de claves:

   `keytool -import -trustcacerts -file`** `.crt -keystore`*CACCertificateNamekeystorename* `.keystore`

   >[!NOTE]
   >
   >* Reemplace `[JAVA_HOME]` por el directorio donde está instalado el JDK y reemplace el texto en cursiva por valores que correspondan con su entorno.
   >* El certificado de CA firmado importado reemplazará a un certificado público con firma automática si existe.


1. Complete los pasos 13 a 18 de Crear una credencial SSL.
