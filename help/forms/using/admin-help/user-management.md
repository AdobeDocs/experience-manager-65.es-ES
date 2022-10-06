---
title: Administración de usuarios
seo-title: User Management
description: La administración de usuarios permite habilitar SSO entre módulos de formularios AEM y aplicaciones protegidas por Netegrity SiteMinder mediante SAML. Este documento proporciona más información sobre la Administración de usuarios.
seo-description: User Management allows you to enable SSO between AEM forms modules and Netegrity SiteMinder-protected applications by using SAML. This document provides more information about User Management.
uuid: f0c8331a-d995-483d-97b7-259df53b1a1a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 10e6177a-8228-4515-aba9-bbe59bede449
exl-id: 1da1f6de-ac0d-4e0d-b8bb-956420e42699
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Administración de usuarios {#user-management}

La administración de usuarios permite habilitar el inicio de sesión único (SSO) entre módulos de formularios AEM y aplicaciones protegidas por Netegrity SiteMinder mediante el uso del lenguaje de marcado de aserción de seguridad (SAML). Cuando se implementa SSO, las páginas de inicio de sesión del usuario de los formularios AEM no son necesarias y no se muestran si el usuario ya está autenticado a través del portal de la empresa.

Para obtener información sobre cómo mejorar el rendimiento de sincronización de directorios y bases de datos para DB2, consulte [Base de datos IBM DB2: Ejecución de comandos para mantenimiento regular](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance).

## Configuración de la administración de usuarios para un servidor LDAP habilitado para SSL {#configuring-user-management-for-an-ssl-enabled-ldap-server}

Si tiene un servidor LDAP habilitado para SSL, configure User Management para que funcione con él. (Consulte [Configuración de la administración de usuarios para un servidor LDAP habilitado para SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)

## Configuración de privilegios de usuario para su uso con Document Security {#setting-user-privileges-for-use-with-document-security}

Cree un usuario administrador que tenga los privilegios adecuados para crear usuarios y grupos. Si el entorno de AEM forms incluye Document Security, conceda el privilegio de administrar los usuarios invitados y locales a un usuario que sea el administrador de estos usuarios. Asigne también la función Usuario de la consola de administración para proporcionar al usuario acceso a la consola de administración. (Consulte [Creación y configuración de funciones](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

Para ver usuarios y grupos en dominios seleccionados durante las búsquedas de usuarios de directivas, un superadministrador o un administrador de conjuntos de directivas deben seleccionar y agregar dominios (creados en Administración de usuarios) a la lista de usuarios y grupos visible para cada conjunto de directivas creado.

La lista visible de usuarios y grupos es visible para el coordinador del conjunto de directivas y se utiliza para restringir los dominios que el usuario final puede examinar al elegir usuarios o grupos para agregar a directivas. Si no se realiza esta tarea, el coordinador del conjunto de políticas no encontrará ningún usuario o grupo que agregar a la directiva. Puede haber más de un coordinador de conjunto de políticas para un conjunto de políticas determinado.

>[!NOTE]
>
>La creación de dominios debe realizarse antes de poder crear cualquier política.

### Configurar usuarios y grupos visibles {#set-visible-users-and-groups}

Después de instalar y configurar el entorno de AEM forms con Document Security, configure todos los dominios adecuados en User Management.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Directivas y, a continuación, haga clic en la ficha Conjuntos de directivas .
1. Seleccione Conjunto de directivas globales y, a continuación, haga clic en la ficha Usuarios y grupos visibles .
1. Haga clic en Añadir dominio y añada dominios existentes según sea necesario.
1. Vaya a Servicios > Seguridad del documento > Configuración > Mis políticas y haga clic en la ficha Usuarios y grupos visibles .
1. Haga clic en Añadir dominio y añada dominios existentes según sea necesario.

## Restricciones de usuario administrador {#administrator-user-restrictions}

Los usuarios con ciertos tipos de privilegios de administrador no pueden acceder a las páginas web del usuario final del espacio de trabajo por motivos de seguridad. Dado que estas páginas web pueden existir fuera de un cortafuegos, permitir tareas de nivel de administración podría suponer un riesgo para la seguridad. Solo los usuarios con privilegios de administrador de Workspace o usuario de Workspace pueden acceder a las páginas web del usuario final.

>[!NOTE]
>
>Flex Workspace está en desuso para AEM versión de formularios.
