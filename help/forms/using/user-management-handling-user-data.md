---
title: Administración de usuarios de formularios| Gestión de datos de usuario
seo-title: Administración de usuarios de formularios| Gestión de datos de usuario
description: nulo
seo-description: nulo
uuid: 2b76b69f-6f3a-4f1a-a2a4-d39f5e529f75
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a88fc933-f1af-4798-b72f-10e7b0d2fd11
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# Administración de usuarios de formularios| Gestión de datos de usuario {#forms-user-management-handling-user-data}

La administración de usuarios es un componente JEE de AEM Forms que permite a los usuarios de AEM Forms acceder a AEM Forms mediante la creación, la gestión y la autorización. La administración de usuarios utiliza los dominios como directorio para obtener información del usuario. Se admiten los siguientes tipos de dominio:

**Dominios** locales: Este tipo de dominio no está conectado a un sistema de almacenamiento de terceros. En su lugar, los usuarios y grupos se crean localmente y residen en la base de datos de Administración de usuarios. Las contraseñas se almacenan localmente y la autenticación se realiza mediante una base de datos local.

**Dominios** híbridos: Este tipo de dominio no está conectado a un sistema de almacenamiento de terceros. En su lugar, los usuarios y grupos se crean localmente y residen en la base de datos de Administración de usuarios. A diferencia de los dominios locales, los dominios híbridos utilizan un proveedor de autenticación externo, que puede ser LDAP, Kerberos, SAML o un proveedor de autenticación personalizado.

**Dominios** empresariales: Consiste en usuarios y grupos que residen en un sistema de almacenamiento de terceros, como un directorio LDAP. La Administración de usuarios no escribe en el sistema de almacenamiento de terceros. En su lugar, Administración de usuarios sincroniza la información de usuarios y grupos con la base de datos de Administración de usuarios. Los dominios de empresa también utilizan un proveedor de autenticación externo, que puede ser LDAP, Kerberos, SAML o un proveedor de autenticación personalizado.

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## Almacenes de datos y datos de usuarios {#user-data-and-data-stores}

La administración de usuarios almacena datos de usuario en una base de datos, como My Sql, Oracle, MS SQL Server e IBM DB2. Además, cualquier usuario que haya iniciado sesión al menos una vez en las aplicaciones de Forms en AEM `https://[server]:[host]/lc`, el usuario se creará en el repositorio de AEM. Por lo tanto, la administración de usuarios se almacena en los siguientes almacenes de datos:

* Base de datos
* Repositorio de AEM
* Almacenamiento de terceros como directorio LDAP

>[!NOTE]
>
>Los datos almacenados en almacenamiento de terceros están fuera del alcance de este documento. Póngase en contacto directamente con el proveedor de terceros para administrar los datos de usuario en dichos almacenes.

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
   <td>Almacena valores de atributo antiguos y nuevos correspondientes a un principal.<br /> </td>
  </tr>
 </tbody>
</table>

### Repositorio de AEM {#aem-repository}

Los datos de administración de usuarios para los usuarios que al menos una vez accedieron a las aplicaciones de Forms en `https://[server]:[host]/lc` se almacenan también en el repositorio de AEM.

## Acceso y eliminación de datos de usuario {#access-and-delete-user-data}

Puede acceder a los datos de administración de usuarios y exportarlos en las bases de datos de administración de usuarios y en el repositorio de AEM, y si es necesario, eliminarlos de forma permanente.

### Base de datos {#database-1}

Para exportar o eliminar datos de usuario de la base de datos de administración de usuarios, debe conectarse a la base de datos con un cliente de base de datos y averiguar el ID principal basado en alguna PII del usuario. Por ejemplo, para recuperar el ID principal de un usuario mediante un ID de inicio de sesión, ejecute el siguiente `select` comando en la base de datos.

En el `select` comando, reemplace el `<user_login_id>` por el ID de inicio de sesión del usuario cuyo ID principal desee recuperar.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

Una vez que conozca el ID principal, puede exportar o eliminar los datos del usuario.

#### Exportar datos de usuario {#export-user-data}

Ejecute los siguientes comandos de base de datos para exportar datos de administración de usuarios para un ID principal desde tablas de base de datos. En el `select` comando, reemplace `<principal_id>` por el ID principal del usuario cuyos datos desee exportar.

>[!NOTE]
>
>Los siguientes comandos utilizan nombres de tabla de base de datos en bases de datos My SQL e IBM DB2. Al ejecutar estos comandos en bases de datos Oracle y MS SQL, reemplace los siguientes nombres de tabla en los comandos:
>
>* Replace `EdcPrincipalLocalAccountEntity` with `EdcPrincipalLocalAccount`
   >
   >
* Replace `EdcPrincipalEmailAliasEntity` with `EdcPrincipalEmailAliasEn`
   >
   >
* Replace `EdcPrincipalMappingEntity` with `EdcPrincipalMappingEntit`
   >
   >
* Replace `EdcPrincipalGrpCtmntEntity` with `EdcPrincipalGrpCtmntEnti`
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

1. Elimine los datos de usuario del repositorio de AEM, si procede, tal como se describe en [Eliminar datos](/help/forms/using/user-management-handling-user-data.md#delete-aem)de usuario.
1. Cierre el servidor de AEM Forms.
1. Ejecute los siguientes comandos de base de datos para eliminar los datos de administración de usuarios para un ID principal de las tablas de base de datos. En el `Delete` comando, reemplace `<principal_id>` por el identificador principal del usuario cuyos datos desee eliminar.

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

1. Inicie el servidor de AEM Forms.

### Repositorio de AEM {#aem-repository-1}

Los usuarios de JEE de Forms tienen sus datos en el repositorio de AEM si han accedido al menos a una instancia de autor de AEM Forms. Puede acceder a sus datos de usuario y eliminarlos del repositorio de AEM.

#### Acceso a los datos de usuario {#access-user-data}

Para ver el usuario creado en el repositorio de AEM, inicie sesión `https://[server]:[port]/lc/useradmin` con las credenciales de administrador de AEM. Tenga en cuenta que `server` y `port` en la URL son las de la instancia de creación de AEM. Aquí puede buscar usuarios con su nombre de usuario. Haga doble clic en un usuario para ver información como propiedades, permisos y grupos para el usuario. La `Path` propiedad de un usuario especifica la ruta al nodo de usuario creado en el repositorio de AEM.

#### Eliminar datos de usuario {#delete-aem}

Para eliminar un usuario:

1. Vaya a `https://[server]:[port]/lc/useradmin` con las credenciales de administrador de AEM.
1. Busque un usuario y haga doble clic en el nombre de usuario para abrir las propiedades del usuario. Copie la `Path` propiedad.
1. Vaya a AEM CRX DELite en `https://[server]:[port]/lc/crx/de/index.jsp` y navegue o busque la ruta del usuario.
1. Elimine la ruta y haga clic en **[!UICONTROL Guardar todo]** para eliminar de forma permanente al usuario del repositorio de AEM.

