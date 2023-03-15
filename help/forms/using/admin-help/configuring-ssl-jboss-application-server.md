---
title: Configurar SSL para el servidor de aplicaciones JBoss
seo-title: Configuring SSL for JBoss Application Server
description: Obtenga información sobre cómo configurar SSL para el servidor de aplicaciones JBoss.
seo-description: Learn how to configure SSL for JBoss Application Server.
uuid: 7c13cf00-ea89-4894-a4fc-aaeec7ae9f66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c187daa4-41b7-47dc-9669-d7120850cafd
exl-id: 8eb4f691-a66b-498e-8114-307221f63718
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 2%

---

# Configurar SSL para el servidor de aplicaciones JBoss {#configuring-ssl-for-jboss-application-server}

Para configurar SSL en el servidor de aplicaciones JBoss, necesita una credencial SSL para la autenticación. Puede utilizar la herramienta clave de Java para crear una credencial o solicitud e importar una credencial de una entidad emisora de certificados (CA). A continuación, debe habilitar SSL en JBoss.

Puede ejecutar keytool con un solo comando que incluya toda la información necesaria para crear el almacén de claves.

En este procedimiento:

* `[appserver root]` AEM es el directorio principal del servidor de aplicaciones que ejecuta formularios en la aplicación de la aplicación.
* `[type]` es un nombre de carpeta que varía según el tipo de instalación que haya realizado.

## Crear una credencial SSL {#create-an-ssl-credential}

1. En un símbolo del sistema, vaya a *[INICIO DE JAVA]*/bin y escriba el siguiente comando para crear la credencial y el almacén de claves:

   `keytool -genkey -dname "CN=`*Nombre de host* `, OU=`*Nombre de grupo* `, O=`*Nombre de empresa* `,L=`*Nombre de ciudad* `, S=`*Estado* `, C=`Código de país&quot; `-alias "AEMForms Cert"` `-keyalg RSA -keypass`*key_password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >Reemplazar `[JAVA_HOME]` con el directorio en el que está instalado el JDK y reemplace el texto en cursiva por valores que se correspondan con su entorno. El nombre de host es el nombre de dominio completo del servidor de aplicaciones.

1. Introduzca el `keystore_password` cuando se le pida una contraseña. La contraseña del almacén de claves y la clave deben ser idénticas.

   >[!NOTE]
   >
   >El `keystore_password` *La contraseña introducida en este paso puede ser la misma contraseña (key_password) introducida en el paso 1 o puede ser diferente.*

1. Copie el *keystorename*.keystore a `[appserver root]/server/[type]/conf` al escribir uno de los siguientes comandos:

   * (Windows Single Server) `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * (Clúster de Windows Server) copiar `keystorename.keystore[appserver root]\domain\configuration`
   * (Servidor único Linux) `cp keystorename.keystore [appserver root]/standalone/configuration`
   * (Clúster de servidor Linux) `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. Exporte el archivo de certificado escribiendo el siguiente comando:

   * (Un solo servidor) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * (clúster de servidor) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. Introduzca el *keystore_password* cuando se le pida una contraseña.
1. Copie el archivo AEMForms_cert.cer en *[raíz de appserver] \conf* al escribir el siguiente comando:

   * (Windows Single Server) `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * (Clúster de Windows Server) `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * (Servidor único Linux) `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * (Clúster de servidor Linux) `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. Vea el contenido del certificado escribiendo el siguiente comando:

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. Para proporcionar acceso de escritura al archivo cacerts en `[JAVA_HOME]\jre\lib\security`, si es necesario, realice la siguiente tarea:

   * (Windows) Haga clic con el botón derecho en el archivo cacerts y seleccione Propiedades y, a continuación, anule la selección del atributo Sólo lectura.
   * Tipo (Linux) `chmod 777 cacerts`

1. Importe el certificado escribiendo el siguiente comando:

   `keytool -import -alias "AEMForms Cert" -file`*AEMForms_cert* `.cer -keystore`*JAVA_HOME* `\jre\lib\security\cacerts`

1. Tipo `changeit` como contraseña. Esta contraseña es la contraseña predeterminada para una instalación de Java y el administrador del sistema puede haberla cambiado.
1. Cuando se le solicite `Trust this certificate? [no]`:, tipo `yes`. Aparece la confirmación &quot;Se agregó el certificado al almacén de claves&quot;.
1. Si se está conectando a través de SSL desde Workbench, instale el certificado en el equipo de Workbench.
1. En un editor de texto, abra los siguientes archivos para editarlos:

   * Servidor único - `[appserver root]`/standalone/configuration/lc_&lt;dbname turnkey=&quot;&quot;>.xml

   * Clúster de servidor - `[appserver root]`/domain/configuration/host.xml

   * Clúster de servidor - `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **Para un solo servidor,** en el lc_&lt;dbaname tunkey=&quot;&quot;>archivo .xml, agregue lo siguiente después de &lt;security-realms> sección:

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   Busque el `<server>` presente después del siguiente código:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Añada lo siguiente a &lt;server> sección presente después del código anterior:

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **Para el clúster de servidores,** en el [raíz de appserver]\domain\configuration\host.xml en todos los nodos, agregue lo siguiente después de &lt;security-realms> sección:

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   En el nodo principal del clúster de servidor, en el [raíz de appserver]\domain\configuration\domain_&lt;dbname>.xml, busque &lt;server> presente después del siguiente código:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Añada lo siguiente a &lt;server> sección presente después del código anterior:

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. Cambie el valor de `keystoreFile` y el atributo `keystorePass` a la contraseña del almacén de claves que especificó al crear el almacén de claves.
1. Reinicie el servidor de la aplicación:

   * Para instalaciones llave en mano:

      * En el Panel de control de Campaign de Windows, haga clic en Herramientas administrativas y, a continuación, haga clic en Servicios.
      * Seleccione JBoss para formularios Adobe Experience Manager.
      * Seleccione Acción > Detener.
      * Espere a que el estado del servicio aparezca como detenido.
      * Seleccione Acción > Iniciar.
   * Para instalaciones de JBoss preconfiguradas o configuradas manualmente en Adobe:

      * Desde un símbolo del sistema, vaya a *`[appserver root]`*/bin.
      * Detenga el servidor introduciendo el siguiente comando:

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * Espere hasta que el proceso de JBoss se haya cerrado completamente (cuando el proceso de JBoss devuelva el control al terminal en el que se inició).
      * Inicie el servidor introduciendo el siguiente comando:

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`



1. Para acceder a la consola de administración mediante SSL, escriba `https://[host name]:'port'/adminui` en un explorador web:

   El puerto SSL predeterminado para JBoss es 8443. AEM A partir de ahora, especifique este puerto al acceder a los formularios de.

## Solicitar una credencial de una CA {#request-a-credential-from-a-ca}

1. En un símbolo del sistema, vaya a *[INICIO DE JAVA]*/bin y escriba el siguiente comando para crear el almacén de claves y la clave:

   `keytool -genkey -dname "CN=`*Nombre de host* `, OU=`*Nombre de grupo* `, O=`*Nombre de empresa* `, L=`*Nombre de ciudad* `, S=`*Estado* `, C=`*Código del país*&quot; `-alias "AEMForms Cert"` `-keyalg RSA -keypass`-*key_password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >Reemplazar *`[JAVA_HOME]`* con el directorio en el que está instalado el JDK y reemplace el texto en cursiva por valores que se correspondan con su entorno.

1. Escriba el siguiente comando para generar una solicitud de certificado para enviarla a la autoridad de certificación:

   `keytool -certreq -alias` &quot;Certificado de AEM Forms&quot; `-keystore`*keystorename* `.keystore -file`*AEMFormscertRequest.csr*

1. Cuando se complete la solicitud de un archivo de certificado, complete el siguiente procedimiento.

## Utilice una credencial obtenida de una CA para habilitar SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. En un símbolo del sistema, vaya a *`[JAVA HOME]`*/bin y escriba el siguiente comando para importar el certificado raíz de la CA con la que se ha firmado la CSR:

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   Si el certificado raíz no está en el explorador, impórtelo también allí.

   >[!NOTE]
   >
   >Reemplazar *`[JAVA_HOME]`con el directorio en el que está instalado el JDK y reemplace el texto en cursiva por valores que se correspondan con su entorno.*

1. En un símbolo del sistema, vaya a *`[JAVA HOME]`*/bin y escriba el siguiente comando para importar las credenciales en el almacén de claves:

   `keytool -import -trustcacerts -file`*CACertificateName* `.crt -keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >* Reemplazar `[JAVA_HOME]` con el directorio en el que está instalado el JDK y reemplace el texto en cursiva por valores que se correspondan con su entorno.
   >* El certificado firmado por la CA importada reemplazará a un certificado público firmado automáticamente si existe.


1. Complete los pasos 13 y 18 de Creación de una credencial SSL.
