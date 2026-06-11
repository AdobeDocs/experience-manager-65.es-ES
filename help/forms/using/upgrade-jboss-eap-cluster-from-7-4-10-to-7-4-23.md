---
title: Actualizar el clúster EAP de JBoss de 7.4.10 a 7.4.23 para AEM Forms en JEE
description: Pasos adicionales para actualizar un clúster EAP de JBoss de 7.4.10 a 7.4.23 para AEM Forms en JEE.
exl-id: 2c9e7f41-a8d6-4b03-8e5c-1a4f6d9e0b72
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms on JEE
role: User, Developer
source-git-commit: dffa92539a8205387d21d3873ab9424508182f19
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 1%

---

# Actualizar el clúster EAP de JBoss de 7.4.10 a 7.4.23 para AEM Forms en JEE {#upgrade-jboss-eap-cluster-from-7-4-10-to-7-4-23}

## Información general {#overview}

Al actualizar un clúster EAP de JBoss de la versión 7.4.10 a la 7.4.23 para AEM Forms en JEE, se requiere una configuración adicional más allá de los pasos de actualización independientes. La configuración específica del clúster, como los localizadores de caché, la autenticación maestro-esclavo, los enlaces de host y la configuración del controlador de dominio deben actualizarse en la nueva instalación de JBoss.

## Se aplica a {#applies-to}

Este artículo se aplica a:

* AEM Forms en JEE que se ejecuta en JBoss EAP 7.4.10 en un entorno de clúster
* Configuraciones EAP de JBoss maestro-esclavo en Windows y Linux

## Requisitos previos {#prerequisites}

Complete todos los pasos de [Actualizar JBoss EAP de 7.4.10 a 7.4.23 para AEM Forms en JEE](/help/forms/using/upgrade-jboss-eap-from-7-4-10-to-7-4-23.md), incluyendo la copia de la URL de conexión, el nombre de usuario y la contraseña de la instalación existente a los nuevos archivos de configuración.

## Etapas {#steps}

Realice los siguientes pasos adicionales específicos del clúster:

### Actualizar domain.conf.bat {#update-domain-conf-bat}

1. En su `domain.conf.bat`, agregue la información de ubicaciones de la configuración existente al nuevo archivo:

   ```text
   set "JAVA_OPTS=%JAVA_OPTS% -Doak.documentMK.maxServerTimeDiffMillis=-1"
   set "JAVA_OPTS=%JAVA_OPTS% -Dadobe.cache.cluster-locators=<ip-address-master>[22345],<ip-address-slave>[22345]"
   set "JAVA_OPTS=%JAVA_OPTS% -DentityExpansionLimit=10000"
   ```

### Configurar la autenticación maestro-esclavo {#configure-master-slave-authentication}

1. Cree un nuevo usuario para la autenticación maestro-esclavo en el nodo maestro.
1. En los nodos esclavos, actualice la contraseña de usuario en `host.xml`:

   ```xml
   <server-identities>
       <secret value="Y2hhbmdlaXQ="/>
   </server-identities>
   ```

### Actualizar direcciones IP en host.xml {#update-ip-addresses-in-host-xml}

1. Actualizar las direcciones IP de los nodos maestro y esclavo en `host.xml`:

   ```xml
   <interfaces>
       <interface name="management">
           <inet-address value="${jboss.bind.address.management:<ip-address>}"/>
       </interface>
       <interface name="public">
           <inet-address value="${jboss.bind.address:<ip-address>}"/>
       </interface>
   </interfaces>
   ```

### Quitar implementaciones de la configuración del dominio {#remove-deployments-from-domain-configuration}

1. Asegúrese de que no haya ninguna sección `<deployments>` en el nuevo archivo `domain_<db>.xml`.
1. No copie el siguiente bloque de la configuración existente:

   ```xml
   <deployments>
       <deployment name="adobe-forms-ivs-jboss.ear" runtime-name="adobe-forms-ivs-jboss.ear"/>
       <deployment name="adobe-livecycle-cq-author.ear" runtime-name="adobe-livecycle-cq-author.ear"/>
       <deployment name="adobe-livecycle-jboss.ear" runtime-name="adobe-livecycle-jboss.ear"/>
       <deployment name="adobe-livecycle-native-jboss-x86_win32.ear" runtime-name="adobe-livecycle-native-jboss-x86_win32.ear"/>
       <deployment name="adobe-livecycle-native-jboss-x86_win64.ear" runtime-name="adobe-livecycle-native-jboss-x86_win64.ear"/>
       <deployment name="adobe-output-ivs-jboss.ear" runtime-name="adobe-output-ivs-jboss.ear"/>
       <deployment name="adobe-workspace-client.ear" runtime-name="adobe-workspace-client.ear"/>
   </deployments>
   ```

### Actualizar la clase de controlador en la configuración de dominio {#update-driver-class-in-domain-configuration}

1. Actualice la sección de clase de controlador en `domain_<db>.xml` según el motor de base de datos:

   **MSSQL:**

   ```xml
   <xa-datasource-class>com.microsoft.sqlserver.jdbc.SQLServerXADataSource</xa-datasource-class>
   ```

   **Oracle:**

   ```xml
   <xa-datasource-class>oracle.jdbc.xa.client.OracleXADataSource</xa-datasource-class>
   ```

### Actualizar el controlador de dominio en los nodos esclavos {#update-domain-controller-on-slave-nodes}

1. Actualice el bloque del controlador de dominio en el nodo esclavo de `host.xml` con la dirección IP maestra, el puerto `9999`, el nombre de usuario `slave1` y el dominio kerberos `ManagementRealm`:

   ```xml
   <remote host="<ip-address>" port="9999" username="slave1" realm="ManagementRealm"/>
   ```

### Actualizar jboss-cli.xml {#update-jboss-cli-xml}

1. Actualice la entrada `<host>` en `jboss-cli.xml` en los nodos maestro y esclavo.
