---
title: Configuración de la administración de usuarios para un servidor LDAP habilitado para SSL
seo-title: Configuración de la administración de usuarios para un servidor LDAP habilitado para SSL
description: Obtenga información sobre cómo configurar la administración de usuarios para un servidor LDAP habilitado para SSL para permitir que la sincronización funcione correctamente en LDAPS.
seo-description: Obtenga información sobre cómo configurar la administración de usuarios para un servidor LDAP habilitado para SSL para permitir que la sincronización funcione correctamente en LDAPS.
uuid: 4b3f8ac7-fa38-4adf-a851-82d55fe431fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e6e7e2fa-579d-4b36-8598-6ced469a94b1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Configurar la administración de usuarios para un servidor LDAP habilitado para SSL {#configure-user-management-for-an-ssl-enabled-ldap-server}

Para que la sincronización funcione correctamente en LDAPS, los certificados LDAP emitidos por la autoridad de certificación (CA) deben estar presentes en el entorno de tiempo de ejecución de Java (JRE) del servidor de aplicaciones. Importe el certificado en el archivo cacerts JRE del servidor de aplicaciones, que normalmente se encuentra en el directorio *[JAVA_HOME]*/jre/lib/security/cacerts.

1. Habilite SSL en el servidor de directorio. Para obtener más información, consulte la documentación proporcionada por el proveedor del directorio.
1. Exporte un certificado de cliente desde el servidor de directorio.
1. Utilice el programa keytool para importar el archivo de certificado de cliente en el almacén de certificados predeterminado de la máquina virtual Java (JVM™) del servidor de aplicaciones de formularios AEM. El procedimiento para esta tarea varía según las rutas de instalación de JVM y cliente. Por ejemplo, si utiliza BEA WebLogic Server con JDK 1.5, desde un símbolo del sistema, escriba este texto:

   `keytool -import -alias`*alias* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. Cuando se le solicite, escriba la contraseña. (Para Java, la contraseña predeterminada es `changeit`). Aparece un mensaje que indica que el certificado se ha importado correctamente.
1. Cuando se le solicite, escriba `Yes` para confiar en el certificado.
1. Habilite SSL en Administración de usuarios y, al configurar la configuración del directorio, seleccione Sí en la opción SSL y cambie la configuración del puerto en consecuencia. El número de puerto predeterminado es 636.

>[!NOTE]
>
>Si experimenta algún problema con SSL, utilice un navegador LDAP para comprobar si puede acceder al sistema LDAP al utilizar SSL. Si el explorador LDAP no puede obtener acceso, el certificado o el servidor de aplicaciones no están configurados correctamente. Si el explorador LDAP funciona correctamente y sigue teniendo problemas, Administración de usuarios no está configurada correctamente.

