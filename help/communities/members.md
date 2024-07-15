---
title: Consolas de administración de miembros y grupos
description: Cómo acceder a las consolas de administración de miembros y grupos
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---


# Consolas de administración de miembros y grupos {#members-groups-management-consoles}

## Información general {#overview}

Las funciones de AEM Communities suelen requerir que los visitantes del sitio se registren e inicien sesión antes de participar en una comunidad en el entorno de publicación. Su registro de usuario solo necesita existir en el entorno de publicación y comúnmente se les denomina *miembros* para distinguirlos de *usuarios* registrados en el entorno de creación.

### Miembros (usuarios) en Publish {#members-users-on-publish}

Mediante las consolas Miembros de comunidades y grupos, los miembros y grupos de miembros registrados en el entorno *publish* se pueden crear y administrar desde el entorno *author*. Esto solo es posible cuando el [servicio de túnel](deploy-communities.md#tunnel-service-on-author) está habilitado.

### Usuarios en Author {#users-on-author}

Para administrar usuarios y grupos registrados en el entorno *author*, es necesario usar la consola de seguridad de la plataforma:

* En la navegación global, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.
* En la navegación global, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Grupos]**.

>[!NOTE]
>
>Con el contenido de muestra implementado y habilitado, muchos usuarios de muestra existen en los entornos de creación y publicación. Estos usuarios no estarán presentes cuando se ejecute con [nosamplecontent runmode](../../help/sites-administering/production-ready.md).

## Consola Miembros {#members-console}

En el entorno de creación, para llegar a la consola Miembros para administrar miembros registrados en el entorno de publicación:

* En la navegación global, seleccione **[!UICONTROL Navegación]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Miembros]**

>[!CAUTION]
>
>No se podrá usar la consola Miembros si el [servicio de túnel](deploy-communities.md#tunnel-service-on-author) no está habilitado.

![La consola de miembros](assets/member-console1.png)

### Búsqueda {#search-features}

Seleccione el icono del panel lateral en el lado izquierdo del encabezado `Members` para activar o desactivar y abrir el panel lateral de búsqueda.

![Icono del panel lateral de búsqueda.](assets/leftpanel-icon.png)


![Opciones de filtro para la consola de miembros](assets/member-console2.png)

Seleccione el icono de búsqueda en el lado izquierdo del encabezado `Members` para alternar el cierre del panel lateral de búsqueda.

### Estadísticas de miembros {#member-statistics}

Las columnas que muestran `Views`, `Posts`, `Follows` y `Likes` se actualizan cuando el usuario es miembro de uno o más sitios de la comunidad con Adobe Analytics [habilitado](sites-console.md#analytics).

### Exportar CSV {#export-csv}

Si se selecciona el vínculo `Export CSV`, se descargarán todos los miembros como una lista de valores separados por comas, adecuados para su importación en una hoja de cálculo.

Los encabezados de columna son

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## Crear nuevo miembro {#create-new-member}

Seleccione `Create Member` para crear un usuario en el entorno de publicación.

![La ventana Crear nuevo miembro](assets/create-member1.png)

### GENERAL: detalles del miembro {#general-member-details}

La mayoría de los campos son campos opcionales que el miembro puede rellenar posteriormente en su perfil.

* **[!UICONTROL ID]**

(*Obligatorio*) El identificador autorizado es el identificador de inicio de sesión del miembro.
De forma predeterminada, el ID se establece en el valor de la dirección de correo electrónico requerida.
*Una vez creado, es posible que el identificador no se modifique*.

* **[!UICONTROL Dirección de correo electrónico]**

(*Requerido*) La dirección de correo electrónico del miembro.
El usuario puede cambiar su dirección de correo electrónico al actualizar su perfil.I
Si la dirección de correo electrónico es la predeterminada, la ID *no* cambiará cuando se cambie la dirección de correo electrónico.

* **[!UICONTROL Contraseña]**

  (*Requerido*) La contraseña de inicio de sesión.

* **[!UICONTROL Contraseña de Retype]**

  (*Requerido*) Vuelva a escribir la contraseña para la verificación.

* **[!UICONTROL Agregar miembro a los sitios]**

  (*Opcional*) Seleccione entre los sitios de la comunidad existentes para agregar el miembro al grupo de miembros del sitio de la comunidad.

* **[!UICONTROL Agregar miembro a grupos]**

  (*Opcional*) Seleccione entre los grupos de miembros existentes para agregar el miembro a ese grupo.

* Seleccionar **[!UICONTROL Guardar]**

### GENERAL: Configuración de la cuenta {#general-account-settings}

En Configuración de cuenta, un administrador de la comunidad puede hacer lo siguiente:

* **[!UICONTROL Estado]**
   * Prohibido
Un miembro no puede iniciar sesión, lo que le impide ver páginas o participar en actividades que requieran iniciar sesión. Todavía pueden visitar de forma anónima un sitio de la comunidad abierto.

   * No prohibido
Un miembro tiene acceso completo al sitio de la comunidad.

  El valor predeterminado es `Not Banned`.

* **[!UICONTROL Límites de contribución]**

  Si se selecciona, la capacidad del miembro para publicar contenido es limitada.
El valor predeterminado depende de la configuración de los límites de contribución.
Ver [Límites de contribución de miembros](limits.md).

* **[!UICONTROL Cambiar contraseña]**

  Vínculo que está presente al modificar un miembro existente. Proporciona la capacidad para que un administrador de la comunidad restablezca una contraseña para un miembro.

### GENERAL - Foto {#general-photo}

Para proporcionar un avatar para el miembro, comience seleccionando **[!UICONTROL Cargar imagen]** y elija una imagen de tipo .jpg, .png, .tif o .gif. El tamaño preferido para una imagen es de 240 x 240 píxeles a 72 ppp.

### GENERAL: Añadir miembro a los sitios {#general-add-member-to-sites}

El miembro puede agregarse a uno o más grupos de miembros de sitios de la comunidad. Comience introduciendo texto en el cuadro de texto.

### GENERAL: Añadir miembro a los grupos {#general-add-member-to-groups}

El miembro puede agregarse a uno o varios grupos de miembros. Comience introduciendo texto en el cuadro de texto.

### Pestaña INSIGNIAS {#badges-tab}

El panel `BADGES` proporciona la capacidad de asignar insignias manualmente y revocarlas. Las insignias pueden ser para roles asignados y distintivos ganados normalmente.

Ver también [Puntuación e insignias](implementing-scoring.md).

![Ventana Editar configuración de pertenencia](assets/create-member2.png)

* **[!UICONTROL Agregar insignias]**
   * Empiece a escribir para seleccionar entre [insignias disponibles](badges.md). Una vez seleccionado un distintivo, elija cada sitio, o todos los sitios, en los que el distintivo debe mostrarse junto con el avatar del miembro.
   * Se pueden elegir varios distintivos y sitios.
* **[!UICONTROL Quitar insignias]**
   * Seleccione el icono de la papelera que hay junto a un distintivo para eliminarlo.

## Consola de grupos {#groups-console}

La consola Grupos, disponible en el entorno de creación, permite la creación y administración de grupos de miembros registrados en el entorno de publicación. Resulta particularmente útil para [grupos de miembros privilegiados](users.md#privilegedmembersgroups).

Para acceder a la consola de grupos:
* En la navegación global, seleccione **[!UICONTROL Navegación]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Grupos]**.

>[!CAUTION]
>
>No se podrá usar la consola de grupos si el [servicio de túnel](deploy-communities.md#tunnel-service-on-author) no está habilitado.

### Crear un grupo nuevo {#create-new-group}

Seleccione `Add Group` para crear un grupo en el entorno de publicación.

![La ventana Crear nuevo grupo](assets/group-console1.png)

Los campos obligatorios para crear un grupo de miembros del lado de publicación son:

* **[!UICONTROL ID]**

  (*Requerido*) El identificador único del grupo.

  *Una vez creado, no se puede modificar el identificador.*

* **[!UICONTROL Nombre]**

  (*Opcional*) El nombre para mostrar del grupo.

  El valor predeterminado es el ID.

* **[!UICONTROL Descripción]**

  (*Opcional*) Una descripción del propósito y los permisos del grupo.

* **[!UICONTROL Agregar Miembros Al Grupo]**

  (*Opcional*) Seleccione los miembros de publicación que se incluirán como miembros iniciales del grupo.

* Seleccionar **[!UICONTROL Guardar]**

## Administradores autorizados {#authorized-administrators}

Cuando se trabaja con miembros en la consola de miembros de Communities, es necesario iniciar sesión como un usuario con los permisos apropiados y que el agente de replicación utilizado por el [servicio de túnel](deploy-communities.md#tunnel-service-on-author) esté configurado correctamente.

Si no inició sesión como `admin`, el usuario que inició sesión debe ser miembro del grupo de usuarios `administrators`.

Consulte también [Agentes de replicación en Autor](deploy-communities.md#replication-agents-on-author).
