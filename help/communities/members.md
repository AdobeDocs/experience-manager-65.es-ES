---
title: Consolas de administración de miembros y grupos
seo-title: Members & Groups Management Consoles
description: Cómo acceder a las consolas de administración de miembros y grupos
seo-description: How to access Members and Groups Management consoles
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 4%

---

# Consolas de administración de miembros y grupos {#members-groups-management-consoles}

## Información general {#overview}

Las funciones de AEM Communities suelen requerir que los visitantes del sitio se registren e inicien sesión antes de participar en una comunidad en el entorno de publicación. Su registro de usuario solo debe existir en el entorno de publicación y suelen denominarse *miembros* para distinguirlos de *usuarios* registrado en el entorno de creación.

### Miembros (usuarios) al publicar {#members-users-on-publish}

Uso de las consolas Miembros de comunidades y grupos, miembros y grupos de miembros registrados en *publicar* entorno se puede crear y administrar desde el *autor* entorno. Esto solo es posible cuando la variable [servicio túnel](deploy-communities.md#tunnel-service-on-author) está activada.

### Usuarios en Author {#users-on-author}

Para administrar usuarios y grupos registrados en *autor* entorno, es necesario para utilizar la consola de seguridad de la plataforma:

* En la navegación global, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.
* En la navegación global, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Grupos]**.

>[!NOTE]
>
>Con el contenido de muestra implementado y habilitado, muchos usuarios de muestra existen en los entornos de creación y publicación. Estos usuarios no estarán presentes cuando se ejecute con [nosamplecontent runmode](../../help/sites-administering/production-ready.md).

## Consola Miembros {#members-console}

En el entorno de creación, para llegar a la consola Miembros para administrar miembros registrados en el entorno de publicación:

* En la navegación global, seleccione **[!UICONTROL Navegación]** > **[!UICONTROL Communities]** > **[!UICONTROL Miembros]**

>[!CAUTION]
>
>No será posible utilizar la consola Miembros si la variable [servicio túnel](deploy-communities.md#tunnel-service-on-author) no está activada.

![member-console1](assets/member-console1.png)

### Búsqueda {#search-features}

Seleccione el icono del panel lateral en el lado izquierdo del `Members` encabezado para alternar y abrir el panel lateral de búsqueda.

![](assets/leftpanel-icon.png)


![member-console2](assets/member-console2.png)

Seleccione el icono de búsqueda en la parte izquierda de la `Members` encabezado para alternar el panel lateral de búsqueda cerrado.

### Estadísticas de miembros {#member-statistics}

Las columnas que muestran `Views`, `Posts`, `Follows` y `Likes` se actualizan cuando el usuario es miembro de uno o más sitios de la comunidad con Adobe Analytics [activado](sites-console.md#analytics).

### Exportar CSV {#export-csv}

Selección de la `Export CSV` Este vínculo resulta en la descarga de todos los miembros como una lista de valores separados por comas, adecuados para su importación en una hoja de cálculo.

Los encabezados de columna son

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## Crear nuevo miembro {#create-new-member}

Seleccionar `Create Member` para crear un usuario en el entorno de publicación.

![create-member1](assets/create-member1.png)

### GENERAL: detalles del miembro {#general-member-details}

La mayoría de los campos son campos opcionales que el miembro puede rellenar posteriormente en su perfil.

* **[!UICONTROL ID]**

(*Requerido*) El ID autorizado es el ID de inicio de sesión del miembro.
De forma predeterminada, el ID se establece en el valor de la dirección de correo electrónico requerida.
*Una vez creada, no se puede modificar la ID*.

* **[!UICONTROL Dirección de correo electrónico]**

(*Requerido*) La dirección de correo electrónico del miembro.
El miembro puede cambiar su dirección de correo electrónico al actualizar su perfil.I Si el ID tiene de forma predeterminada la dirección de correo electrónico, el ID *no* cambiar cuando se cambia la dirección de correo electrónico.

* **[!UICONTROL Contraseña]**

   (*Requerido*) La contraseña de inicio de sesión.

* **[!UICONTROL Repetir contraseña]**

   (*Requerido*) Vuelva a introducir la contraseña para la verificación.

* **[!UICONTROL Añadir miembro a los sitios]**

   (*Opcional*) Seleccione entre los sitios de la comunidad existentes para agregar al miembro al grupo de miembros del sitio de la comunidad.

* **[!UICONTROL Añadir miembro a los grupos]**

   (*Opcional*) Seleccione entre los grupos de miembros existentes para agregar el miembro a ese grupo.

* Seleccione **[!UICONTROL Guardar]**

### GENERAL: Configuración de la cuenta {#general-account-settings}

En Configuración de cuenta, un administrador de la comunidad puede hacer lo siguiente:

* **[!UICONTROL Estado]**
   * Prohibido Un miembro no puede iniciar sesión, lo que le impide ver páginas o participar en actividades que requieran iniciar sesión. Todavía pueden visitar de forma anónima un sitio de la comunidad abierto.

   * No prohibido Un miembro tiene acceso completo al sitio de la comunidad.

   El valor predeterminado es `Not Banned`.

* **[!UICONTROL Límites de contribución]**

   Si se selecciona, la capacidad del miembro para publicar contenido es limitada.
El valor predeterminado depende de la configuración de los límites de contribución.
Consulte [Límites de contribución de miembros](limits.md).

* **[!UICONTROL Cambiar contraseña]**

   Vínculo que está presente al modificar un miembro existente. Proporciona la capacidad para que un administrador de la comunidad restablezca una contraseña para un miembro.

### GENERAL - Foto {#general-photo}

Para proporcionar un avatar para el miembro, comience seleccionando **[!UICONTROL Cargar imagen]** y elija una imagen de tipo .jpg, .png, .tif o .gif. El tamaño preferido para una imagen es de 240 x 240 píxeles a 72 ppp.

### GENERAL: Añadir miembro a los sitios {#general-add-member-to-sites}

El miembro puede agregarse a uno o más grupos de miembros de sitios de la comunidad. Comience introduciendo texto en el cuadro de texto.

### GENERAL: Añadir miembro a los grupos {#general-add-member-to-groups}

El miembro puede agregarse a uno o varios grupos de miembros. Comience introduciendo texto en el cuadro de texto.

### Pestaña INSIGNIAS {#badges-tab}

El `BADGES` el panel permite asignar insignias manualmente y revocarlas. Las insignias pueden ser para funciones asignadas, así como insignias ganadas normalmente.

Consulte también [Puntuación y distintivos](implementing-scoring.md).

![create-member2](assets/create-member2.png)

* **[!UICONTROL Añadir insignias]**
   * Empiece a escribir para seleccionar [insignias disponibles](badges.md). Una vez seleccionado un distintivo, elija cada sitio, o todos los sitios, en los que el distintivo debe mostrarse junto con el avatar del miembro.
   * Se pueden elegir varios distintivos y sitios.
* **[!UICONTROL Quitar insignias]**
   * Seleccione el icono de la papelera que hay junto a un distintivo para eliminarlo.

## Consola de grupos {#groups-console}

La consola Grupos, disponible en el entorno de creación, permite la creación y administración de grupos de miembros registrados en el entorno de publicación. Resulta especialmente útil para [Grupos de miembros privilegiados](users.md#privilegedmembersgroups).

Para acceder a la consola de grupos:
* En la navegación global, seleccione **[!UICONTROL Navegación]** > **[!UICONTROL Communities]** > **[!UICONTROL Grupos]**.

>[!CAUTION]
>
>No será posible utilizar la consola de grupos si la variable [servicio túnel](deploy-communities.md#tunnel-service-on-author) no está activada.

### Crear un grupo nuevo {#create-new-group}

Seleccionar `Add Group` para crear un grupo en el entorno de publicación.

![group-console1](assets/group-console1.png)

Los campos obligatorios para crear un nuevo grupo de miembros del lado de publicación son:

* **[!UICONTROL ID]**

   (*Requerido*) El ID único del grupo.

   *Una vez creada, no se puede modificar la ID.*

* **[!UICONTROL Nombre]**

   (*Opcional*) El nombre para mostrar del grupo.

   El valor predeterminado es el ID.

* **[!UICONTROL Descripción]**

   (*Opcional*) Una descripción del propósito y los permisos del grupo.

* **[!UICONTROL Añadir miembros al grupo]**

   (*Opcional*) Seleccione los miembros de publicación que se incluirán como miembros iniciales del grupo.

* Seleccione **[!UICONTROL Guardar]**

## Administradores autorizados {#authorized-administrators}

Cuando se trabaja con miembros en la consola de miembros de Communities, es necesario iniciar sesión como un usuario con los permisos adecuados y para el agente de replicación que usa el [servicio túnel](deploy-communities.md#tunnel-service-on-author) para configurarse correctamente.

Si no ha iniciado sesión como `admin`, el usuario que ha iniciado sesión debe ser miembro de `administrators` grupo de usuarios.

Consulte también [Agentes de replicación en Autor](deploy-communities.md#replication-agents-on-author).
