---
title: Administración de usuarios de Forms | Gestión de datos de usuario
seo-title: Administración de usuarios de Forms | Gestión de datos de usuario
description: Administración de usuarios de Forms | Gestión de datos de usuario
uuid: 2b76b69f-6f3a-4f1a-a2a4-d39f5e529f75
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a88fc933-f1af-4798-b72f-10e7b0d2fd11
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---


# Administración de usuarios de Forms | Gestión de datos de usuario {#forms-user-management-handling-user-data}

La administración de usuarios es un componente JEE de AEM Forms que permite a los usuarios de AEM Forms crear, administrar y autorizar el acceso a AEM Forms. La administración de usuarios utiliza los dominios como directorio para obtener información del usuario. Se admiten los siguientes tipos de dominio:

**Dominios** locales: Este tipo de dominio no está conectado a un sistema de almacenamiento de terceros. En su lugar, los usuarios y grupos se crean localmente y residen en la base de datos de Administración de usuarios. Las contraseñas se almacenan localmente y la autenticación se realiza mediante una base de datos local.

**Dominios** híbridos: Este tipo de dominio no está conectado a un sistema de almacenamiento de terceros. En su lugar, los usuarios y grupos se crean localmente y residen en la base de datos de Administración de usuarios. A diferencia de los dominios locales, los dominios híbridos utilizan un proveedor de autenticación externo, que puede ser LDAP, Kerberos, SAML o un proveedor de autenticación personalizado.

**Dominios** empresariales: Consiste en usuarios y grupos que residen en un sistema de almacenamiento de terceros, como un directorio LDAP. La Administración de usuarios no escribe en el sistema de almacenamiento de terceros. En su lugar, Administración de usuarios sincroniza la información de usuarios y grupos con la base de datos de Administración de usuarios. Los dominios de empresa también utilizan un proveedor de autenticación externo, que puede ser LDAP, Kerberos, SAML o un proveedor de autenticación personalizado.

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## Almacenes de datos y datos del usuario {#user-data-and-data-stores}

La administración de usuarios almacena datos de usuario en una base de datos, como My Sql, Oracle, MS SQL Server e IBM DB2. Además, cualquier usuario que haya iniciado sesión al menos una vez en aplicaciones de Forms en AEM autor de `https://'[server]:[port]'lc`, el usuario se creará en AEM repositorio. Por lo tanto, la administración de usuarios se almacena en los siguientes almacenes de datos:

* Base de datos
* AEM repositorio
* Almacenamientos de terceros como directorio LDAP

>[!NOTE]
>
>Los datos almacenados en almacenamientos de terceros están fuera del ámbito de este documento. Póngase en contacto directamente con el proveedor de terceros para administrar los datos de usuario en dichos almacenamientos.

### Base de datos {#database}

La administración de usuarios almacena datos de usuario en las siguientes tablas de base de datos:

<table>
 <tbody>
  <tr>
   <td>Tabla de base de datos</td>
   <td>Descripción</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalEntity</code></td>
   <td><p>Almacena información sobre entidades principales. Un principal puede ser un usuario, un grupo o una función.</p> <p> </p> </td>
  </tr>
  <tr>
   <td><code>EdcPrincipalUserEntity</code></td>
   <td>Almacena información de identificación personal (PII) de los usuarios. Contiene una entrada para cada usuario de dominios locales, empresariales e híbridos.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>(bases de datos Oracle y MS SQL)</p> </td>
   <td>Almacena datos solo para usuarios locales.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>(bases de datos Oracle y MS SQL)</p> </td>
   <td>Contiene entradas de todos los usuarios de dominios locales, empresariales e híbridos. Contiene los ID de correo electrónico del usuario.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code> (bases de datos Oracle y MS SQL)</p> </td>
   <td>Almacena la asignación entre usuarios y grupos.</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalRoleEntity</code></td>
   <td>Almacena la asignación entre roles y principales para usuarios y grupos.</td>
  </tr>
  <tr>
   <td><code>EdcPriResPrmEntity</code></td>
   <td>Almacena la asignación entre principal y permisos para usuarios y grupos.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code> (bases de datos Oracle y MS SQL)</p> </td>
   <td>Almacena valores de atributos nuevos y antiguos correspondientes a un principal.<br /> </td>
  </tr>
 </tbody>
</table>

### Repositorio de AEM {#aem-repository}

Los datos de administración de usuarios para los usuarios que al menos una vez accedieron a las aplicaciones de Forms en `https://'[server]:[port]'lc` también se almacenan en AEM repositorio.

## Acceso y eliminación de datos de usuario {#access-and-delete-user-data}

Puede acceder a los datos de administración de usuarios y exportarlos para los usuarios de las bases de datos de administración de usuarios y AEM repositorio y, si es necesario, eliminarlos de forma permanente.

### Base de datos {#database-1}

Para exportar o eliminar datos de usuario de la base de datos de administración de usuarios, debe conectarse a la base de datos con un cliente de base de datos y averiguar el ID principal basado en alguna PII del usuario. Por ejemplo, para recuperar el identificador principal de un usuario mediante un identificador de inicio de sesión, ejecute el siguiente comando `select` en la base de datos.

En el comando `select`, reemplace el `<user_login_id>` por el identificador de inicio de sesión del usuario cuyo identificador principal desee recuperar.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

Una vez que conozca el ID principal, puede exportar o eliminar los datos del usuario.

#### Exportar datos de usuario {#export-user-data}

Ejecute los siguientes comandos de base de datos para exportar datos de administración de usuarios para un ID principal desde tablas de base de datos. En el comando `select`, reemplace `<principal_id>` por el identificador principal del usuario cuyos datos desee exportar.

>[!NOTE]
>
>Los siguientes comandos utilizan nombres de tabla de base de datos en bases de datos My SQL e IBM DB2. Al ejecutar estos comandos en bases de datos Oracle y MS SQL, reemplace los siguientes nombres de tabla en los comandos:
>
>* Reemplazar `EdcPrincipalLocalAccountEntity` con `EdcPrincipalLocalAccount`
   >
   >
* Reemplazar `EdcPrincipalEmailAliasEntity` con `EdcPrincipalEmailAliasEn`
   >
   >
* Reemplazar `EdcPrincipalMappingEntity` con `EdcPrincipalMappingEntit`
   >
   >
* Reemplazar `EdcPrincipalGrpCtmntEntity` con `EdcPrincipalGrpCtmntEnti`

>



```sql
Select * from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (Select id from EDCPRINCIPALENTITY where id='<principal_id>'));

Select * from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalEntity where id='<principal_id>';
```

#### Eliminar datos de usuario {#delete-user-data}

Haga lo siguiente para eliminar los datos de administración de usuarios de un ID principal de las tablas de base de datos.

1. Elimine los datos de usuario de AEM repositorio, si corresponde, tal como se describe en [Eliminar datos de usuario](/help/forms/using/user-management-handling-user-data.md#delete-aem).
1. Cierre el servidor de AEM Forms.
1. Ejecute los siguientes comandos de base de datos para eliminar los datos de administración de usuarios para un ID principal de las tablas de base de datos. En el comando `Delete`, reemplace `<principal_id>` por el identificador principal del usuario cuyos datos desee eliminar.

   ```sql
   Delete from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (select id from EdcPrincipalEntity where id='<principal_id>'));
   
   Delete from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalEntity where id='<principal_id>';
   ```

1. Inicio del servidor AEM Forms.

### Repositorio de AEM {#aem-repository-1}

Los usuarios de Forms JEE tienen sus datos en AEM repositorio si han accedido al menos a la instancia de creación de AEM Forms. Puede acceder a los datos de usuario y eliminarlos de AEM repositorio.

#### Obtener acceso a los datos de usuario {#access-user-data}

Para vista de usuarios creados en AEM repositorio, inicie sesión en `https://'[server]:[port]'/lc/useradmin` con AEM credenciales de administrador. Tenga en cuenta que `server` y `port` en la dirección URL son los de la instancia de creación de AEM. Aquí puede buscar usuarios con su nombre de usuario. Haga clic con el botón doble en un usuario para vista de información como propiedades, permisos y grupos para el usuario. La propiedad `Path` de un usuario especifica la ruta al nodo de usuario creado en AEM repositorio.

#### Eliminar datos de usuario {#delete-aem}

Para eliminar un usuario:

1. Vaya a `https://'[server]:[port]'/lc/useradmin` con AEM credenciales de administrador.
1. Busque un usuario y haga clic con el botón doble en el nombre de usuario para abrir las propiedades del usuario. Copie la propiedad `Path`.
1. Vaya a AEM CRX DELite en `https://'[server]:[port]'/lc/crx/de/index.jsp` y navegue o busque la ruta del usuario.
1. Elimine la ruta y haga clic en **[!UICONTROL Guardar todo]** para eliminar permanentemente al usuario de AEM repositorio.

