---
title: Configurar la administración de usuarios para un servidor LDAP habilitado para SSL
description: Obtenga información sobre cómo configurar la administración de usuarios para un servidor LDAP habilitado para SSL con el fin de permitir que la sincronización funcione correctamente en LDAPS.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 606e84f2-6728-47a9-a439-dbe2e55100ad
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 5%

---

# Configurar la administración de usuarios para un servidor LDAP habilitado para SSL {#configure-user-management-for-an-ssl-enabled-ldap-server}

Para que la sincronización funcione correctamente en LDAPS, los certificados LDAP emitidos por la autoridad de certificación (CA) deben estar presentes en el entorno de tiempo de ejecución de Java (JRE) del servidor de aplicaciones. Importe el certificado en el archivo cacerts JRE del servidor de aplicaciones, que normalmente se encuentra en el *[JAVA_HOME]* directorio /jre/lib/security/cacerts.

1. Habilite SSL en el servidor de directorio. Para obtener más información, consulte la documentación proporcionada por el proveedor del directorio.
1. Exporte un certificado de cliente desde el servidor de directorios.
1. AEM Utilice el programa keytool para importar el archivo de certificado del cliente en el almacén de certificados predeterminado de la máquina virtual Java (JVM™) del servidor de aplicaciones de formularios de la El procedimiento para esta tarea varía, según las rutas de instalación de JVM y cliente. Por ejemplo, si utiliza BEA WebLogic Server con JDK 1.5, desde un símbolo del sistema, escriba este texto:

   `keytool -import -alias`*alias* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. Cuando se le pida, escriba la contraseña. (En Java, la contraseña predeterminada es `changeit`.) Aparece un mensaje que indica que el certificado se ha importado correctamente.
1. Cuando se le solicite, escriba `Yes` para confiar en el certificado.
1. Habilite SSL en Administración de usuarios y, al configurar los valores del directorio, seleccione Sí para la opción SSL y cambie la configuración del puerto en consecuencia. El número de puerto predeterminado es 636.

>[!NOTE]
>
>Si tiene algún problema al utilizar SSL, utilice un explorador LDAP para comprobar si puede acceder al sistema LDAP al utilizar SSL. Si el explorador LDAP no puede obtener acceso, el certificado o el servidor de aplicaciones no están configurados correctamente. Si el explorador LDAP funciona correctamente y sigue experimentando problemas, la administración de usuarios no está configurada correctamente.
