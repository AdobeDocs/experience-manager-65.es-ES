---
title: Seguridad de documento | Gestión de datos de usuario
seo-title: Seguridad de documento | Gestión de datos de usuario
description: Seguridad de documento | Gestión de datos de usuario
uuid: 1624a465-8b0c-4347-a53f-1118bfa6e18f
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 898268cb-4426-421f-8f63-d75bd85cb57f
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---


# Seguridad de documento | Gestión de datos de usuario {#document-security-handling-user-data}

La seguridad de AEM Forms documento le permite crear, almacenar y aplicar a sus documentos configuraciones de seguridad predefinidas. Garantiza que solo los usuarios autorizados puedan utilizar los documentos. Puede proteger documentos mediante políticas. Una directiva es una recopilación de información que incluye la configuración de seguridad y una lista de usuarios autorizados. Puede aplicar una política a uno o varios documentos y autorizar a los usuarios que se agreguen en la administración de usuarios de AEM Forms JEE.

<!-- Fix broken link For more information about how document security works, see AEM Forms JEE administration help. -->

## Almacenes de datos y datos de usuarios {#user-data-and-data-stores}

La seguridad de documento almacena directivas y datos relacionados con documentos protegidos, incluidos datos de usuario en una base de datos, como My Sql, Oracle, MS SQL Server e IBM DB2. Además, los datos de los usuarios autorizados en una directiva almacenada en la administración de usuarios. Para obtener información sobre los datos almacenados en la administración de usuarios, consulte Administración de usuarios de [Forms: Gestión de datos](/help/forms/using/user-management-handling-user-data.md)de usuario.

La siguiente tabla muestra cómo organiza la seguridad de documento los datos en las tablas de base de datos.

<table>
 <tbody>
  <tr>
   <td>Tabla de base de datos</td>
   <td>Descripción</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalKeyEntity</code></td>
   <td>Almacena información sobre claves principales para los usuarios. Las claves se utilizan en flujos de trabajo de seguridad de documento sin conexión.</td>
  </tr>
  <tr>
   <td><code>EdcAuditEntity</code></td>
   <td>Almacena información sobre eventos de auditoría como eventos de usuario, eventos de documento y eventos de políticas.</td>
  </tr>
  <tr>
   <td><p><code>EdcLicenseEntity</code></p> </td>
   <td>Almacena el registro de un documento protegido. Almacena los detalles de licencia de cada documento protegido.</td>
  </tr>
  <tr>
   <td><p><code>EdcDocumentEntity</code></p> </td>
   <td>Almacena el nombre del documento para cada licencia creada en el sistema.</td>
  </tr>
  <tr>
   <td><p><code>EdcRevokationEntity</code></p> </td>
   <td>Almacena información sobre la revocación y la restauración de documentos protegidos.</td>
  </tr>
  <tr>
   <td><code>EdcMyPolicyListEntity</code></td>
   <td>Almacena información sobre los usuarios que pueden crear políticas personales que aparecen en la ficha Mis políticas de la página Directivas. </td>
  </tr>
  <tr>
   <td><code>EdcPolicyEntity</code></td>
   <td>Almacena información sobre directivas. Cada política corresponde a una fila de esta tabla.</td>
  </tr>
  <tr>
   <td><code>EdcPolicyXmlEntity</code></td>
   <td>Almacena archivos XML para directivas activas. Un XML<sup> de directivas </sup>contiene referencias a los ID principales de los usuarios asociados a la directiva. Policy XML se almacena como un objeto Blob.</td>
  </tr>
  <tr>
   <td><code>EdcPolicyArchiveEntity</code></td>
   <td>Almacena información sobre políticas archivadas. Una directiva archivada contiene su política XML almacenada como un objeto Blob.</td>
  </tr>
  <tr>
   <td><p><code>EdcPolicySetPrincipalEntity</code></p> <p><code>EdcPolicySetPrincipalEnt</code> (bases de datos Oracle y MS SQL)</p> </td>
   <td>Almacena la asignación entre el conjunto de directivas y los usuarios.</td>
  </tr>
  <tr>
   <td><code>EdcInvitedUserEntity</code></td>
   <td>Almacena información sobre el usuario invitado.</td>
  </tr>
 </tbody>
</table>

## Acceso y eliminación de datos de usuario {#access-and-delete-user-data}

Puede acceder y exportar datos de seguridad de documento para los usuarios de las bases de datos y, si es necesario, eliminarlos de forma permanente.

Para exportar o eliminar datos de usuario de una base de datos, debe conectarse a la base de datos con un cliente de base de datos y averiguar el ID principal en función de alguna información personal del usuario. Por ejemplo, para recuperar el ID principal de un usuario mediante un ID de inicio de sesión, ejecute el siguiente `select` comando en la base de datos.

En el `select` comando, reemplace el `<user_login_id>` por el ID de inicio de sesión del usuario cuyo ID principal desee recuperar de la tabla de la `EdcPrincipalUserEntity` base de datos.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

Una vez que conozca el ID principal, puede exportar o eliminar los datos del usuario.

### Exportar datos de usuario {#export-user-data}

Ejecute los siguientes comandos de base de datos para exportar datos de usuario para un ID principal desde tablas de base de datos. En el `select` comando, reemplace `<principal_id>` por el ID principal del usuario cuyos datos desee exportar.

>[!NOTE]
>
>Los siguientes comandos utilizan nombres de tabla de base de datos en bases de datos My SQL e IBM DB2. Al ejecutar estos comandos en bases de datos Oracle y MS SQL, reemplace `EdcPolicySetPrincipalEntity` por `EdcPolicySetPrincipalEnt` en los comandos.

```sql
Select * from EdcPrincipalKeyEntity where principalid = '<principal_id>';

Select * from EdcLicenseEntity where publisherId = '<principal_id>';

Select * from EdcDocumentEntity where id in (Select documentid from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcRevokationEntity where licenseid in (Select id from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcMyPolicyListEntity where principalId = '<principal_id>';

Select * from edcpolicyentity where policyownerId = '<principal_id>';

Select * from edcpolicyxmlentity where policyidref in (Select id from edcpolicyentity where policyownerId = '<principal_id>');

Select * from edcpolicyarchiveentity where policyownerId = '<principal_id>';

Select * from edcpolicysetprincipalentity where principalId = '<principal_id>';

Select * from edcinviteduserentity where principalId = '<principal_id>';
```

>[!NOTE]
>
>Para exportar datos de la `EdcAuditEntity` tabla, utilice la API [EventManager.exportEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) que toma [EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) como parámetro para exportar datos de auditoría basados en `principalId`, `policyId`o `licenseId`.

Para obtener datos completos sobre un usuario en el sistema, debe acceder a los datos y exportarlos desde la base de datos de administración de usuarios. Para obtener más información, consulte Administración de usuarios de [Forms: Gestión de datos](/help/forms/using/user-management-handling-user-data.md)de usuario.

### Eliminar datos de usuario {#delete-user-data}

Haga lo siguiente para eliminar los datos de seguridad de documento para un ID principal de las tablas de base de datos.

1. Cierre el servidor de AEM Forms.
1. Ejecute los siguientes comandos de base de datos para eliminar datos del ID principal de las tablas de base de datos para la seguridad de documento. En el `Delete` comando, reemplace `<principal_id>` por el identificador principal del usuario cuyos datos desee eliminar.

   ```sql
   Delete from EdcPrincipalKeyEntity where principalid = '<principal_id>';
   
   Delete from EdcMyPolicyListEntity where principalId = '<principal_id>';
   
   Delete from edcpolicyarchiveentity where policyownerId = '<principal_id>';
   
   Delete from edcpolicysetprincipalentity where principalId = '<principal_id>';
   
   Delete from edcinviteduserentity where principalId = '<principal_id>';
   ```

   >[!NOTE]
   >
   >Para eliminar datos de la `EdcAuditEntity` tabla, utilice la API [EventManager.deleteEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) que toma [EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) como parámetro para eliminar datos de auditoría basados en `principalId`, `policyId`o `licenseId`.

1. Los archivos XML de directivas activas y archivadas se almacenan en las tablas `EdcPolicyXmlEntity` y `EdcPolicyArchiveEntity` base de datos, respectivamente. Para eliminar datos de un usuario de estas tablas, haga lo siguiente:

   1. Abra el blob XML de cada fila de la tabla `EdcPolicyXMLEntity` o `EdcPolicyArchiveEntity` y extraiga el archivo XML. El archivo XML es similar al que se muestra a continuación.
   1. Edite el archivo XML para eliminar el blob del ID principal.
   1. Repita los pasos 1 y 2 para el otro archivo.

   >[!NOTE]
   >
   >Debe eliminar el blob completo de la `Principal` etiqueta para un ID principal o el XML de directiva puede dañarse o quedar inutilizable.

   ```xml
   <ns2:Principal PrincipalNameType="USER">
       <ns2:PrincipalDomain>OID</ns2:PrincipalDomain>
       <ns2:PrincipalName>56F33FEB-098A-1036-A651-00000A2A2656</ns2:PrincipalName>
   </ns2:Principal>
   </ns2:PolicyEntry>
       <ns2:Property PropertyName="isCertified">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">false</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="encryptionAlgorithm">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">AES128</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="AccessDeniedErrorMessage">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string"></ns2:PropertyValue>
       </ns2:Property>
   <ns2:PolicyEntry>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.onlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.copy" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.offlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.accessible" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.editNotes" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.edit" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.fillAndSign" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printHigh" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printLow" Access="ALLOW"/>
   ```

   Además de eliminar datos directamente de la `EdcPolicyXmlEntity` tabla, existen dos formas más de lograrlo:

   **Uso de la consola de administración**

   1. Como administrador, inicie sesión en la consola de administración de Forms JEE en https://[*server*]:[*port*]/adminui.
   1. Vaya a **[!UICONTROL Servicios > Seguridad de Documento > Conjuntos]** de directivas.
   1. Abra un conjunto de directivas y elimine el usuario de la directiva.

   **Uso de la página web de seguridad de documento**

   Los usuarios de seguridad de documento que tengan permisos para crear políticas personales pueden eliminar datos de usuario de sus políticas. Para ello:

   1. Los usuarios con políticas personales inician sesión en la página web de seguridad de documento en https://[*server*]:[*port*]/edc.
   1. Vaya a **[!UICONTROL Servicios > Seguridad de Documento > Mis políticas]**.
   1. Abra una directiva y elimine el usuario de la misma.

   >[!NOTE]
   >
   >Los administradores pueden buscar, acceder y eliminar datos de usuario de las políticas personales de otros usuarios en **[!UICONTROL Servicios > Seguridad de Documento > Mis políticas]** mediante la consola de administración.

1. Elimine los datos del ID principal de la base de datos de administración de usuarios. Para ver los pasos detallados, consulte Administración de usuarios de [Forms | Gestión de datos](/help/forms/using/user-management-handling-user-data.md)de usuario.
1. Inicio del servidor AEM Forms.

