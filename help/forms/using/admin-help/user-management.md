---
title: Administración de usuarios
seo-title: Administración de usuarios
description: La administración de usuarios le permite activar SSO entre los módulos de formularios AEM y las aplicaciones protegidas por Netegrity SiteMinder mediante SAML. Este documento proporciona más información sobre la Administración de usuarios.
seo-description: La administración de usuarios le permite activar SSO entre los módulos de formularios AEM y las aplicaciones protegidas por Netegrity SiteMinder mediante SAML. Este documento proporciona más información sobre la Administración de usuarios.
uuid: f0c8331a-d995-483d-97b7-259df53b1a1a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 10e6177a-8228-4515-aba9-bbe59bede449
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Administración de usuarios {#user-management}

La administración de usuarios le permite habilitar el inicio de sesión único (SSO) entre los módulos de formularios AEM y las aplicaciones protegidas por Netegrity SiteMinder mediante el lenguaje de marcado de aserción de seguridad (SAML). Cuando se implementa SSO, las páginas de inicio de sesión del usuario de los formularios AEM no son necesarias y no se muestran si el usuario ya está autenticado a través del portal de la empresa.

Para obtener información sobre cómo mejorar el rendimiento de sincronización de directorios y bases de datos para DB2, consulte Base de datos DB2 de [IBM: Ejecución de comandos para mantenimiento](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance)regular.

## Configuración de la administración de usuarios para un servidor LDAP habilitado para SSL {#configuring-user-management-for-an-ssl-enabled-ldap-server}

Si tiene un servidor LDAP habilitado para SSL, configure la Administración de usuarios para que funcione con él. (Consulte [Configuración de la administración de usuarios para un servidor](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)LDAP con SSL habilitado).

## Configuración de privilegios de usuario para su uso con Document Security {#setting-user-privileges-for-use-with-document-security}

Cree un usuario administrador con los privilegios adecuados para crear usuarios y grupos. Si su entorno de formularios AEM incluye Document Security, conceda el privilegio de administrar los usuarios invitados y locales a un usuario que será el administrador de estos usuarios. También asigne la función de usuario de la consola de administración para proporcionar al usuario acceso a la consola de administración. (Consulte [Creación y configuración de funciones](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)).

Para ver usuarios y grupos en dominios seleccionados durante las búsquedas de usuarios de directivas, un superadministrador o un administrador de conjuntos de directivas debe seleccionar y agregar dominios (creados en Administración de usuarios) a la lista visible de usuarios y grupos para cada conjunto de directivas creado.

La lista visible de usuarios y grupos es visible para el coordinador de conjuntos de políticas y se utiliza para restringir los dominios que el usuario final puede examinar al elegir usuarios o grupos para agregar a las políticas. Si no se realiza esta tarea, el coordinador de conjuntos de políticas no encontrará ningún usuario o grupo para agregar a la política. Puede haber más de un coordinador de conjunto de políticas para un conjunto de políticas determinado.

>[!NOTE]
>
>La creación de dominios debe realizarse antes de poder crear políticas.

### Configurar usuarios y grupos visibles {#set-visible-users-and-groups}

Después de instalar y configurar el entorno de formularios AEM con Document Security, configure todos los dominios adecuados en Administración de usuarios.

1. En la consola de administración, haga clic en Servicios > Document Security > Directivas y, a continuación, haga clic en la ficha Conjuntos de directivas.
1. Seleccione Conjunto de directivas globales y, a continuación, haga clic en la ficha Usuarios y grupos visibles.
1. Haga clic en Agregar dominio(s) y agregue los dominios existentes según sea necesario.
1. Vaya a Servicios > Seguridad del documento > Configuración > Mis políticas y haga clic en la ficha Usuarios y grupos visibles.
1. Haga clic en Agregar dominio(s) y agregue los dominios existentes según sea necesario.

## Restricciones del usuario administrador {#administrator-user-restrictions}

Los usuarios con determinados tipos de privilegios de administrador no pueden acceder a las páginas web del usuario final de Workspace por motivos de seguridad. Dado que estas páginas web pueden existir fuera de un servidor de seguridad, permitir tareas de nivel de administración podría suponer un riesgo para la seguridad. Solo los usuarios que tienen privilegios de administrador de Workspace o de usuario de Workspace pueden acceder a las páginas web del usuario final.

>[!NOTE]
>
>Flex Workspace está en desuso para la versión de formularios AEM.

