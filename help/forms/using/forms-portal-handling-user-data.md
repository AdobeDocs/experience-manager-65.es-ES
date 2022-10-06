---
title: Portal de Forms | Gestión de datos de usuario
seo-title: Forms Portal | Handling user data
description: Portal de Forms | Gestión de datos de usuario
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
role: Admin
exl-id: 791524a4-a8bb-4632-a68d-e96864e139a9
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 3%

---

# Portal de Forms | Gestión de datos de usuario {#forms-portal-handling-user-data}

[!DNL AEM Forms] portal proporciona componentes que puede utilizar para listar formularios adaptables, formularios HTML5 y otros recursos de Forms en [!DNL AEM Sites] página. Además, se puede configurar para que muestre los borradores y envíe formularios adaptables y formularios HTML5 para un usuario que ha iniciado sesión. Para obtener más información sobre el portal de formularios, consulte [Introducción a la publicación de formularios en un portal](/help/forms/using/introduction-publishing-forms.md).

Cuando un usuario que ha iniciado sesión guarda un formulario adaptable como borrador o lo envía, se muestran en las fichas Borradores y envíos del portal de formularios. Los datos de borradores o formularios enviados se almacenan en el almacén de datos configurado para AEM implementación. Los borradores y envíos de usuarios anónimos no se muestran en la página del portal de formularios; sin embargo, los datos se almacenan en el almacén de datos configurado. Para obtener más información, consulte [Configuración de servicios de almacenamiento para borradores y envíos](/help/forms/using/configuring-draft-submission-storage.md).

## Almacenamiento de datos y datos de usuarios {#user-data-and-data-stores}

El portal de Forms almacena datos para formularios en borrador y enviados en los siguientes casos:

* La acción de envío configurada en el formulario adaptable es **Acción de envío del portal de Forms**.
* Para enviar acciones que no sean **Acción de envío del portal de Forms**, el **[!UICONTROL Almacenar datos en el portal de formularios]** está activada en el **[!UICONTROL Envío]** propiedades del contenedor de formulario adaptable.

Para cada borrador y formulario enviado para usuarios anónimos e iniciados sesión, el portal de formularios almacena los siguientes datos:

* Metadatos de formulario, como el nombre del formulario, la ruta del formulario, el ID de borrador o envío, la ruta de acceso de los archivos adjuntos y el ID de datos de usuario
* Datos adjuntos de formulario como bytes de datos
* Datos de formulario como bytes de datos

Según la persistencia del almacén de datos configurado, los borradores y los datos de formulario enviados se almacenan en las siguientes ubicaciones.

<table>
 <tbody>
  <tr>
   <td><p><strong>Tipo de persistencia</strong></p> </td>
   <td><p><strong>Almacén de datos</strong></p> </td>
   <td><p><strong>Lugar de residencia</strong></p> </td>
  </tr>
  <tr>
   <td><p>Predeterminado</p> </td>
   <td><p>AEM repositorio de instancias de autor y publicación</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Remoto</p> </td>
   <td><p>AEM repositorio de instancias de AEM remotas y de autor</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Base de datos</p> </td>
   <td><p>AEM repositorio de instancias de autor y tablas de base de datos</p> </td>
   <td>Tablas de base de datos <code>data</code>, <code>metadata</code>y <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## Acceso y eliminación de datos de usuario {#access-and-delete-user-data}

Puede acceder a los datos de los formularios borrador y enviados para los usuarios que iniciaron sesión y los anónimos en los almacenes de datos configurados y, si es necesario, eliminarlos.

### AEM instancias {#aem-instances}

Todos los borradores y los datos de formulario enviados en AEM instancias (autor, publicación o remota) para usuarios conectados y anónimos se almacenan en la `/content/forms/fp/` del repositorio de AEM aplicable. Cada vez que un usuario anónimo o con sesión iniciada guarda un borrador o envía un formulario, se guarda un `draft ID` o `submission ID`, `user data ID`y aleatorio `ID` para cada archivo adjunto (si procede) se genera, que se asocia al proyecto o presentación respectivo.

#### Acceso a los datos de usuario {#access-user-data}

Cuando un usuario que ha iniciado sesión guarda un borrador o envía un formulario, se crea un nodo secundario con su ID de usuario. Por ejemplo, borradores y datos de envío para Sarah Rose cuyo ID de usuario es `srose` se almacenan en `/content/forms/fp/srose/` en AEM repositorio. Dentro del nodo de ID de usuario, los datos se organizan en una estructura jerárquica.

En la tabla siguiente se explica cómo funcionan los datos de todos los borradores de `srose` se almacena en AEM repositorio.

>[!NOTE]
>
>Una estructura exacta como `drafts` se replica para formularios enviados para `srose` en el `/content/forms/fp/srose/submit/` nodo .
>
>Todos los proyectos y presentaciones de `anonymous` los usuarios se almacenan en la sección `/content/forms/fp/anonymous/` , que organiza borradores y envíos para todos los usuarios anónimos en el `draft` y `submit` nodos.

| Nodo | Descripción |
|---|---|
| `/content/forms/fp/srose/drafts` | Datos de nodo de contenedor para todos los borradores del usuario |
| `/content/forms/fp/srose/drafts/attachments/` | Organiza todos los archivos adjuntos para el usuario en función del ID de borrador |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | Contiene datos adjuntos del ID seleccionado en formato binario |
| `/content/forms/fp/srose/drafts/metadata/` | Organiza los metadatos del formulario para el usuario en función del ID de borrador |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | Contiene metadatos de formulario para el ID de borrador seleccionado |
| `/content/forms/fp/srose/drafts/data/` | Organiza los datos de los formularios para el usuario en función de su ID |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | Contiene datos de formulario para el ID de datos de usuario seleccionado en formato binario |

#### Eliminación de los datos de usuario {#delete-user-data}

Para eliminar por completo los datos de usuario de borradores y envíos para un usuario que ha iniciado sesión desde AEM sistemas, debe eliminar la variable `user ID` para un usuario específico del nodo de autor. Debe eliminar manualmente los datos de todas las instancias de AEM aplicables.

Los borradores y los datos de envío de todos los usuarios anónimos se almacenan dentro de los `drafts` y `submit` nodos bajo `/content/forms/fp/anonymous`. No hay ningún método para encontrar datos para un usuario anónimo en particular a menos que se conozca alguna información identificable. En este caso, puede buscar la información que identifica al usuario anónimo en AEM repositorio y eliminar manualmente el nodo que lo contiene de todas las instancias de AEM aplicables para eliminar datos del sistema AEM. Sin embargo, para eliminar los datos de todos los usuarios anónimos, puede eliminar la variable `anonymous` para eliminar borradores y enviar datos para todos los usuarios anónimos.

### Base de datos {#database}

Cuando AEM está configurado para almacenar datos en una base de datos, los datos de borrador y envío del portal de formularios se almacenan en las siguientes tablas de base de datos para los usuarios que iniciaron sesión y los anónimos:

* data
* metadatos
* metadatos adicionales

#### Acceso a los datos de usuario {#access-user-data-1}

Para acceder a los datos de borradores y envíos de usuarios anónimos y conectados a la base de datos, ejecute el siguiente comando de base de datos. En la consulta, reemplace `logged-in user` con el ID de usuario cuyos datos desea acceder a o con `anonymous` para usuarios anónimos.

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### Eliminación de los datos de usuario {#delete-user-data-1}

Para eliminar borradores y enviar datos para un usuario que ha iniciado sesión desde las tablas de la base de datos, ejecute el siguiente comando de base de datos. En la consulta, reemplace `logged-in user` con el ID de usuario cuyos datos desea eliminar o con `anonymous` para usuarios anónimos. Tenga en cuenta que para eliminar de la base de datos los datos de un usuario anónimo en particular, debe encontrarlos utilizando información identificable y eliminarlos de las tablas de la base de datos que contengan la información.

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```
