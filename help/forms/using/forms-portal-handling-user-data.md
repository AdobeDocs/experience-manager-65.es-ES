---
title: Forms Portal| Gestión de datos de usuario
seo-title: Forms Portal| Gestión de datos de usuario
description: nulo
seo-description: nulo
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Forms Portal| Gestión de datos de usuario {#forms-portal-handling-user-data}

AEM Forms Portal proporciona componentes que se pueden utilizar para mostrar formularios adaptables, formularios HTML5 y otros recursos de formularios en la página Sitios de AEM. Además, puede configurarlo para que muestre borradores y formularios adaptables y HTML5 enviados para un usuario que ha iniciado sesión. Para obtener más información sobre el portal de formularios, consulte [Introducción a la publicación de formularios en un portal](/help/forms/using/introduction-publishing-forms.md).

Cuando un usuario que ha iniciado sesión guarda un formulario adaptable como borrador o lo envía, se muestra en las fichas Borradores y envíos del portal de formularios. Los datos de borradores o formularios enviados se almacenan en el almacén de datos configurado para la implementación de AEM. Los borradores y los envíos de usuarios anónimos no se muestran en la página del portal de formularios; sin embargo, los datos se almacenan en el almacén de datos configurado. Para obtener más información, consulte [Configuración de servicios de almacenamiento para borradores y envíos](/help/forms/using/configuring-draft-submission-storage.md).

## Almacenes de datos y datos de usuarios {#user-data-and-data-stores}

Forms Portal almacena datos para formularios de borrador y enviados en los siguientes escenarios:

* La acción de envío configurada en el formulario adaptable es Acción **de envío de** Forms Portal.
* Para enviar acciones que no sean Acción **de envío de** Forms Portal, la opción **[!UICONTROL Almacenar datos en el portal]** de formularios está activada en las propiedades de **envío** del contenedor de formularios adaptables.

Por cada borrador y formulario enviado para usuarios anónimos e iniciados, el portal de formularios almacena los siguientes datos:

* Metadatos del formulario como, por ejemplo, el nombre del formulario, la ruta del formulario, el ID de envío o borrador, la ruta de acceso de los archivos adjuntos y el ID de datos del usuario
* Datos adjuntos de formulario como bytes de datos
* Datos de formulario como bytes de datos

Según la persistencia del almacén de datos configurado, los borradores y los datos de formularios enviados se almacenan en las siguientes ubicaciones.

<table>
 <tbody>
  <tr>
   <td><p><strong>Tipo de persistencia</strong></p> </td>
   <td><p><strong>Almacén de datos</strong></p> </td>
   <td><p><strong>Lugar de residencia</strong></p> </td>
  </tr>
  <tr>
   <td><p>Predeterminado</p> </td>
   <td><p>Repositorio de instancias de creación y publicación de AEM</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Remoto</p> </td>
   <td><p>Repositorio de AEM de instancias de AEM de autor y remotas</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Base de datos</p> </td>
   <td><p>Repositorio de AEM de instancias de creación y tablas de bases de datos</p> </td>
   <td>Tablas de base de datos <code>data</code>, <code>metadata</code>y <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## Acceso y eliminación de datos de usuario {#access-and-delete-user-data}

Puede acceder a los datos de los formularios de borrador y enviados para los usuarios anónimos e iniciados en los almacenes de datos configurados y, si es necesario, eliminarlos.

### Instancias de AEM {#aem-instances}

Todos los borradores y los datos de formularios enviados en instancias de AEM (autor, publicación o remoto) para usuarios que iniciaron sesión y anónimos se almacenan en el `/content/forms/fp/` nodo del repositorio de AEM aplicable. Cada vez que un usuario anónimo o que ha iniciado sesión guarda un borrador o envía un formulario, se genera un formulario, un formulario `draft ID` o `submission ID`, un `user data ID`, y un aleatorio `ID` para cada archivo adjunto (si corresponde), que se asocia al borrador o envío correspondiente.

#### Acceso a los datos de usuario {#access-user-data}

Cuando un usuario que ha iniciado sesión guarda un borrador o envía un formulario, se crea un nodo secundario con su ID de usuario. Por ejemplo, los borradores y los datos de envío de Sarah Rose cuyo ID de usuario `srose` se almacena en el `/content/forms/fp/srose/` nodo del repositorio de AEM. Dentro del nodo de ID de usuario, los datos se organizan en una estructura jerárquica.

En la tabla siguiente se explica cómo se almacenan los datos de todos los borradores por `srose` en el repositorio de AEM.

>[!NOTE]
>
>Se replica una estructura exacta como `drafts` para los formularios enviados `srose` en el `/content/forms/fp/srose/submit/` nodo.
>
>Todos los borradores y envíos de `anonymous` usuarios se almacenan en el `/content/forms/fp/anonymous/` nodo, que organiza borradores y envíos para todos los usuarios anónimos en los nodos `draft` y `submit` .

| Nodo | Descripción |
|---|---|
| `/content/forms/fp/srose/drafts` | Datos de nodo de contenedor para todos los borradores del usuario |
| `/content/forms/fp/srose/drafts/attachments/` | Organiza todos los datos adjuntos para el usuario según el ID de borrador |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | Contiene datos adjuntos para el ID seleccionado en formato binario |
| `/content/forms/fp/srose/drafts/metadata/` | Organiza los metadatos del formulario para el usuario en función del ID de borrador |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | Contiene metadatos de formulario para el ID de borrador seleccionado |
| `/content/forms/fp/srose/drafts/data/` | Organiza los datos de formularios para el usuario en función de su ID de datos |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | Contiene datos de formulario para el ID de datos de usuario seleccionado en formato binario |

#### Eliminar datos de usuario {#delete-user-data}

Para eliminar completamente los datos de usuario de borradores y envíos para un usuario que ha iniciado sesión en los sistemas AEM, debe eliminar el nodo de un usuario específico del nodo de creación `user ID` . Debe eliminar manualmente los datos de todas las instancias de AEM aplicables.

Los borradores y los datos de envío de todos los usuarios anónimos se almacenan en los nodos comunes `drafts` y `submit` en `/content/forms/fp/anonymous`. No hay ningún método para buscar datos de un usuario anónimo concreto a menos que se conozca alguna información identificable.En este caso, puede buscar la información que identifica al usuario anónimo en el repositorio de AEM y eliminar manualmente el nodo que lo contiene de todas las instancias de AEM aplicables para eliminar datos del sistema AEM. Sin embargo, para eliminar datos de todos los usuarios anónimos, puede eliminar el `anonymous` nodo para eliminar borradores y datos de envío de todos los usuarios anónimos.

### Base de datos {#database}

Cuando AEM está configurado para almacenar datos en una base de datos, los datos de envío y borrador del portal de formularios se almacenan en las siguientes tablas de base de datos para los usuarios que inician sesión y los usuarios anónimos:

* data
* metadata
* metadatos adicionales

#### Acceso a los datos de usuario {#access-user-data-1}

Para acceder a los datos de borradores y envíos de los usuarios anónimos e iniciados en las tablas de la base de datos, ejecute el siguiente comando de la base de datos. En la consulta, reemplace `logged-in user` por el ID de usuario cuyos datos desee obtener acceso o por `anonymous` para usuarios anónimos.

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### Eliminar datos de usuario {#delete-user-data-1}

Para eliminar borradores y datos de envío de un usuario que ha iniciado sesión desde las tablas de la base de datos, ejecute el siguiente comando de base de datos. En la consulta, reemplace `logged-in user` por el ID de usuario cuyos datos desee eliminar o por `anonymous` para usuarios anónimos. Tenga en cuenta que para eliminar datos de un usuario anónimo concreto de la base de datos, debe encontrarlos utilizando alguna información identificable y eliminarlos de las tablas de la base de datos que contienen la información.

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```

