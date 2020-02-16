---
title: Cómo auditar las operaciones de administración de usuarios en AEM
seo-title: Cómo auditar las operaciones de administración de usuarios en AEM
description: Obtenga información sobre cómo auditar las operaciones de administración de usuarios en AEM.
seo-description: Obtenga información sobre cómo auditar las operaciones de administración de usuarios en AEM.
uuid: 9d177afb-172c-4858-a678-254c97cfa472
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: ba6a56e5-b91c-4779-9154-d4300b2827f8
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538

---


# Cómo auditar las operaciones de administración de usuarios en AEM{#how-to-audit-user-management-operations-in-aem}

## Introducción {#introduction}

AEM ha introducido la capacidad de registrar cambios en los permisos para que puedan auditarse posteriormente.

La mejora permite auditar acciones de CRUD (Crear, Leer, Actualizar, Eliminar) en permisos y asignaciones de grupos de usuarios. Más específicamente, registrará:

* Se está creando un nuevo usuario
* Un usuario que se está agregando a un grupo
* Cambios de permisos de un usuario o grupo existente

De forma predeterminada, las entradas se escribirán en el `error.log` archivo. Para facilitar la supervisión, se recomienda que se redirijan a un archivo de registro independiente. Más información sobre cómo hacerlo en el párrafo siguiente.

## Redireccionamiento del resultado a un archivo de registro independiente {#redirecting-the-output-to-a-separate-log-file}

Para redireccionar el resultado de registro a un archivo de registro independiente, deberá crear una nueva configuración del registrador de registros **Apache Sling** . Utilizaremos `useraudit.log` como nombre del archivo independiente en el ejemplo siguiente.

1. Vaya a la consola web navegando a *https://serveraddress:serverport/system/console/configMgr*
1. Busque la configuración **del registrador de registros Sling de** Apache. A continuación, presione &quot;+&quot; en el lado derecho de la entrada para crear una nueva configuración de fábrica.
1. Cree la siguiente configuración:

   * **** Nivel de registro:Información
   * **** Archivo de registro: logs/useraudit.log
   * **** Patrón de mensajes: nivel predeterminado
   * **** Registrador: com.adobe.granite.security.user.internal.audit, com.adobe.granite.security.user.internal.servlets.AuthorizableServlet
   Para introducir ambos registradores en el campo **Registrador** , debe introducir el nombre del primero, luego crear otro campo pulsando el botón &quot;+&quot; e introduciendo el nombre del segundo registrador.

## Ejemplo de salida {#example-output}

Si se configura correctamente, el resultado debería tener el siguiente aspecto:

```xml
19.05.2017 15:15:08.933 *INFO* [0:0:0:0:0:0:0:1 [1495196108932] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Create Group 'group1' operation initiated by User 'admin' (administrator)
19.05.2017 15:15:08.934 *INFO* [0:0:0:0:0:0:0:1 [1495196108932] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction Group 'group1' was created

19.05.2017 15:16:25.698 *INFO* [0:0:0:0:0:0:0:1 [1495196185696] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Create User 'user1' operation initiated by User 'admin' (administrator)
19.05.2017 15:16:25.700 *INFO* [0:0:0:0:0:0:0:1 [1495196185696] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction User 'user1' was created

19.05.2017 15:16:25.728 *INFO* [0:0:0:0:0:0:0:1 [1495196185726] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Edit Membership for Group 'group1' operation initiated by User 'admin' (administrator)
19.05.2017 15:16:25.729 *INFO* [0:0:0:0:0:0:0:1 [1495196185726] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditGroupAction User 'user1' was added to the group 'group1'

19.05.2017 15:17:29.830 *INFO* [0:0:0:0:0:0:0:1 [1495196249828] POST /home/users/5/5dI6iK4HkZmrfTjcLBoI.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Password Change for User 'user2' operation initiated by User 'admin' (administrator)
19.05.2017 15:17:29.832 *INFO* [0:0:0:0:0:0:0:1 [1495196249828] POST /home/users/5/5dI6iK4HkZmrfTjcLBoI.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction Password for User 'user2' was changed

19.05.2017 15:17:54.906 *INFO* [0:0:0:0:0:0:0:1 [1495196274904] POST /home/users/5/5dI6iK4HkZmrfTjcLBoI.rw.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Delete User 'user2' operation initiated by User 'admin' (administrator)
19.05.2017 15:17:54.906 *INFO* [0:0:0:0:0:0:0:1 [1495196274904] POST /home/users/5/5dI6iK4HkZmrfTjcLBoI.rw.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction User 'user2' was removed

19.05.2017 15:19:11.050 *INFO* [0:0:0:0:0:0:0:1 [1495196351049] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Create User 'user3' operation initiated by User 'admin' (administrator)
19.05.2017 15:19:11.052 *INFO* [0:0:0:0:0:0:0:1 [1495196351049] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction User 'user3' was created
19.05.2017 15:19:36.899 *INFO* [0:0:0:0:0:0:0:1 [1495196376898] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Edit Membership for Group 'group1' operation initiated by User 'admin' (administrator)

19.05.2017 15:19:36.916 *INFO* [0:0:0:0:0:0:0:1 [1495196376915] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Edit Membership for Group 'group1' operation initiated by User 'admin' (administrator)
19.05.2017 15:19:36.917 *INFO* [0:0:0:0:0:0:0:1 [1495196376915] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditGroupAction User 'user1' was removed from the group 'group1'

19.05.2017 15:21:34.419 *INFO* [0:0:0:0:0:0:0:1 [1495196494417] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Delete Group 'group1' operation initiated by User 'admin' (administrator)
19.05.2017 15:21:34.419 *INFO* [0:0:0:0:0:0:0:1 [1495196494417] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction Group 'group1' was removed

19.05.2017 15:44:10.404 *INFO* [0:0:0:0:0:0:0:1 [1495197850401] POST /home/users/3/35XVpVtLRx4a5J9gKrVG.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Password Change for User 'john' operation initiated by User 'john' (not administrator)
19.05.2017 15:44:10.405 *INFO* [0:0:0:0:0:0:0:1 [1495197850401] POST /home/users/3/35XVpVtLRx4a5J9gKrVG.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction Password for User 'john' was changed
```

## IU clásica {#classic-ui}

En la IU clásica, la información sobre las operaciones de CRUD registradas en el registro de auditoría en relación con la adición y eliminación de usuarios se limita al ID del usuario afectado y el momento en que se produjo el cambio.

Por ejemplo:

```
10.05.2019 18:01:09.123 INFO [0:0:0:0:0:0:0:1 [1557491469096] POST /libs/cq/security/authorizables/POST HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction User 'test' was created
```

