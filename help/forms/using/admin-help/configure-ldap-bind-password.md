---
title: Configurar la contraseña de enlace LDAP
description: Obtenga información sobre cómo configurar el campo de contraseña de enlace antes de importar el archivo de configuración en otro sistema.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c72794f5-8767-409e-a1df-91a8fdc54d18
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 5%

---

# Configurar la contraseña de enlace LDAP{#configure-the-ldap-bind-password}

Para evitar riesgos de seguridad, el campo de contraseña de enlace del archivo de configuración exportado (config.xml) no está configurado. Antes de importar el archivo de configuración a otro sistema, asegúrese de configurar esta contraseña. Esta contraseña anula una contraseña existente almacenada en la base de datos. Una contraseña nula no reemplaza un valor de contraseña no nula existente.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.
1. Para exportar la configuración actual a un archivo, haga clic en Exportar y guarde el archivo de configuración en otra ubicación.
1. En el archivo, busque el nodo `Domains` > *[Su nombre de dominio]* > `DirectoryConfigs` > `LDAPGroupConfig`. A continuación se muestra un ejemplo:

   ```xml
    <node name="LDAPGroupConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="batchSize" value="200" />
            <entry key="binduser" value="cn=Directory Manager" />
            <entry key="bindpassword" value="" />
        </map>
   ```

   Escriba un valor para `bindpassword` y guarde los cambios.

1. En el archivo, busque el nodo `Domains` > *[Su nombre de dominio]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig`. A continuación se muestra un ejemplo:

   ```xml
    <node name="LDAPUserConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="batchSize" value="200" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="bindpassword" value="" />
            <entry key="binduser" value="cn=Directory Manager" />
        </map>
   ```

   Escriba un valor para `bindpassword` y guarde los cambios.

1. Para importar el archivo actualizado, en Administración de usuarios, haga clic en Configuración > Importar y exportar archivos de configuración.
1. Haga clic en Examinar para buscar el archivo, en Importar y, a continuación, en Aceptar.
