---
title: Administración de usuarios y grupos de usuarios
seo-title: Administración de usuarios y grupos de usuarios
description: Los usuarios de AEM Communities pueden registrarse y editar sus perfiles
seo-description: Los usuarios de AEM Communities pueden registrarse y editar sus perfiles
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 0%

---


# Administración de usuarios y grupos de usuarios {#managing-users-and-user-groups}

## Información general {#overview}

En AEM Communities, en el entorno de publicación, los usuarios pueden registrarse automáticamente y editar sus perfiles. Dados los permisos adecuados, también podrán:

* Cree subcomunidades dentro del sitio de la comunidad (consulte [grupos de la comunidad](creating-groups.md)).

* [Contenido generado por ](moderation.md) moderador (UGC).

* Tener [contactos de recursos de habilitación](resources.md).

* Tenga [privilegios](#privileged-members-group) para crear entradas para blogs, calendarios, QnA y foros.

Los usuarios registrados en el entorno de publicación generalmente se conocen como *miembros de la comunidad (miembros)* para distinguirlos de *usuarios* en el entorno de creación.

Los permisos se conceden asignando miembros a uno de los [grupos de miembros (usuarios)](#publish-group-roles) creados dinámicamente cuando el sitio de comunidad se [crea](sites-console.md) o [modifica](sites-console.md#modifying-site-properties) desde el entorno de creación. Cuando se trabaja desde el entorno de creación, los miembros son visibles desde el entorno de publicación mediante el [servicio de túnel](#tunnel-service).

Por diseño, los miembros y los grupos de miembros creados en el entorno de publicación no deberían aparecer en el entorno de creación. Los usuarios y los grupos de usuarios creados en el entorno de creación tienen la misma intención de permanecer en el entorno de creación.

Cuando los usuarios de la creación y los miembros de la publicación proceden de la misma lista de usuarios, como sincronizados desde el mismo directorio LDAP, no se consideran el mismo usuario con los mismos permisos y pertenencia a grupos en los entornos de creación y publicación. Las funciones de los miembros y usuarios deben establecerse por separado al publicar y crear, según proceda.

Para un [conjunto de servidores de publicación](topologies.md), el registro y las modificaciones realizadas en una instancia de publicación deben sincronizarse con otras instancias de publicación para que tengan acceso a los mismos datos de usuario. Para obtener más información, consulte [Sincronización de usuarios](sync.md), que incluye una sección que describe [Qué sucede cuando...](sync.md#what-happens-when).

### Límites de contribución {#contribution-limits}

Para protegerse del spam, es posible limitar la frecuencia de publicación del contenido de los miembros. Además, es posible limitar automáticamente las contribuciones de los miembros recién inscritos.

Para obtener más información, consulte [Límites de contribución de miembros](limits.md).

### Grupos de usuarios creados dinámicamente {#dynamically-created-user-groups}

Cuando se crea un nuevo sitio de comunidad, se crean de forma dinámica nuevos grupos de usuarios con identificadores únicos (uid) y permisos adecuados para diversas funciones administrativas necesarias para administrar el sitio de comunidad, ya sea en el entorno de creación (consulte [Funciones de grupo de creación](#author-group-roles)) o en el entorno de publicación (consulte [Funciones de grupo de publicación](#publish-group-roles)).

Los nombres de los grupos se generan a partir del nombre dado al sitio durante la [creación del sitio de comunidad](sites-console.md#step13asitetemplate). Los identificadores únicos evitan conflictos de nombres para sitios de comunidad con nombres similares y grupos de comunidad en el mismo servidor.

Por ejemplo, si el nombre del sitio fuera &quot;*engagement*&quot; para un sitio llamado &quot;We.Retail Engage&quot;, uno de los grupos de usuarios creados sería:

* Miembros de la comunidad *Participación*

## Entorno de creación {#author-environment}

### Servicio de túnel {#tunnel-service}

Al utilizar el entorno de creación para [crear sitios](sites-console.md), [modificar las propiedades del sitio](sites-console.md#modifying-site-properties) y [administrar los miembros de la comunidad y los grupos de miembros](members.md), es necesario tener acceso a los usuarios y grupos de usuarios registrados en el entorno de publicación.

El servicio de túnel proporciona este acceso mediante el agente de replicación del autor.

* Para obtener más información, consulte [instrucciones de configuración](deploy-communities.md#tunnel-service-on-author) en la página de implementación.

Las [consolas Miembros y grupos de comunidades](members.md) tienen el único propósito de administrar usuarios (miembros) y grupos de usuarios (grupos de miembros) registrados solamente en el entorno de publicación.

Para administrar usuarios y grupos de usuarios registrados en el entorno de creación, utilice la [Consola de seguridad](../../help/sites-administering/security.md)

### Funciones de grupo de creación {#author-group-roles}

| Si es miembro del grupo... | Función principal |
|---|---|
| administradores | El grupo de administradores está formado por administradores de sistema que tienen todas las capacidades de un administrador de comunidad, así como la capacidad de administrar el grupo de administradores de comunidad. |
| Administradores de la comunidad | El grupo Administradores de la comunidad se convierte automáticamente en miembro de todos los sitios de la comunidad y de cualquier grupo de la comunidad creado en el sitio. Un miembro inicial del grupo Administradores de comunidad es el grupo de administradores. En el entorno de creación, los administradores de la comunidad pueden crear sitios de la comunidad, administrar sitios, administrar miembros (pueden prohibir miembros de la comunidad) y moderar contenido. |
| Comunidad &lt;*nombre del sitio* Sitecontentmanager | El Administrador de contenido del sitio de la comunidad puede realizar la creación de contenido, la creación de contenido y la modificación de páginas AEM tradicionales para un sitio de la comunidad. |
| Administradores de habilitación de la comunidad | El grupo Administradores de habilitación de la comunidad está formado por usuarios que están disponibles para asignación para administrar el grupo Administradores de habilitación de un sitio de la comunidad. |
| Comunidad &lt;*nombre del sitio* > Administradores de inicialización | El grupo Administradores de habilitación de sitio de comunidad está formado por usuarios que han sido asignados para administrar la habilitación de [recursos](resources.md) de un sitio de comunidad. |
| Ninguna | Un visitante anónimo del sitio no puede acceder al entorno del autor. |

### Administradores de sistemas {#system-administrators}

Los miembros del grupo de administradores son administradores del sistema que pueden realizar la configuración inicial de una instalación de AEM para los entornos de creación y publicación.

Para fines de demostración y desarrollo, el grupo de administradores tiene un miembro cuyo userid es *admin* y la contraseña es *admin*.

Para los entornos de producción, se debe modificar el grupo de administradores predeterminado.

Asegúrese de seguir la [lista de comprobación de seguridad](../../help/sites-administering/security-checklist.md).

## Entorno de publicación {#publish-environment}

### Cómo convertirse en miembro {#becoming-a-member}

En el entorno de publicación, según la [configuración](sites-console.md#user-management) del sitio de comunidad, un visitante del sitio puede convertirse en miembro de la comunidad:

* Cuando el sitio de la comunidad es privado (cerrado):
   * Por invitación
   * Por acciones de un administrador

* Cuando el sitio de la comunidad es público (abierto):
   * Por inscripción automática
   * Por inicio de sesión social con Facebook y Twitter

>[!NOTE]
>
>Si un visitante del sitio se registra como miembro de un sitio de comunidad abierta, automáticamente se convierte en miembro de otros sitios de comunidad abierta en el mismo entorno de publicación.

### Publicar roles de grupo {#publish-group-roles}

| Si es miembro del grupo... | Función principal |
|---|---|
| Miembros de la comunidad &lt;*nombre del sitio* | Un miembro del sitio de la comunidad es un usuario registrado. Pueden iniciar sesión, modificar su perfil, unirse a un grupo de la comunidad abierta, publicar contenido en la comunidad, enviar mensajes a otros miembros y seguir las actividades del sitio. |
| Moderadores de &lt;*nombre del sitio* de la comunidad | Un moderador del sitio de la comunidad es un miembro de la comunidad de confianza que puede moderar UGC de forma masiva, mediante la consola de moderación o en contexto, en la página en la que se anuncia el contenido. |
| Miembros de la comunidad &lt;*nombre del sitio*> &lt;*nombre del grupo*> | Un miembro del grupo comunitario es un miembro de la comunidad que se ha unido a un grupo de la comunidad abierta o que ha sido invitado a un grupo de la comunidad cerrado. Tienen las capacidades de un miembro para ese grupo de la comunidad dentro del sitio. |
| Comunidad &lt;*nombre del sitio* Administradores de grupos | Un administrador de grupos de sitios de la comunidad es un miembro de la comunidad de confianza que está asignado para crear y administrar subcomunidades (grupos) dentro de un sitio de la comunidad. Se incluye la capacidad de proporcionar moderación en contexto. |
| *Grupo de seguridad de miembros privilegiados* | Grupo de usuarios creado y mantenido manualmente con el fin de restringir la creación de contenido. Consulte [Grupo de miembros privilegiados](#privileged-members-group). |
| Ninguna | Un visitante anónimo del sitio, que descubre el sitio, puede realizar vistas y búsquedas en los sitios de la comunidad que permiten el acceso anónimo. Para participar y publicar contenido, el usuario debe registrarse (si se permite) y convertirse en miembro de la comunidad. |

### Asignación de miembros a funciones de grupo de publicación {#assigning-members-to-publish-group-roles}

Cuando [crea un sitio de comunidad](sites-console.md) en el entorno del autor o cuando [modifica las propiedades del sitio,](sites-console.md#modifying-site-properties) los miembros pueden tener asignadas varias funciones realizadas en el entorno de publicación, como moderadores, administradores de grupos, contactos de recursos o miembros privilegiados.

[Al habilitar los ](sync.md#accessingpublishusersfromauthor) servicios de túnel, las opciones de asignación se presentan desde los miembros en la publicación en lugar de los usuarios en el autor.

Los miembros seleccionados se asignarán automáticamente al [grupo apropiado](#publish-group-roles) y sus miembros se incluirán cuando se (re)publique el sitio de la comunidad.

### Grupo de miembros privilegiados {#privileged-members-group}

El propósito de un grupo de seguridad de miembros privilegiados es restringir la creación de contenido para ciertas funciones de la comunidad a un subconjunto privilegiado de miembros del sitio de la comunidad.

El grupo de miembros privilegiados es un grupo de miembros creado y administrado mediante la consola [Grupos de comunidades](members.md).

Después de crear un grupo de miembros privilegiados, y con el [servicio de túnel habilitado](sync.md#accessingpublishusersfromauthor), la estructura de un sitio de comunidad existente puede [modificarse](sites-console.md#modify-structure) para editar la configuración de sus funciones de comunidad en &#39;Permitir miembros privilegiados&#39; y agregar el grupo creado.

Las funciones de comunidad que permiten especificar uno o más grupos de miembros privilegiados son:

* [Función](functions.md#blog-function)  de blog - Para restringir la creación de nuevos artículos.
* [Función](functions.md#calendar-function)  de calendario: para restringir la creación de nuevos eventos.
* [Función](functions.md#forum-function)  Foro: para restringir la creación de nuevos temas.
* [Función](functions.md#qna-function)  QnA: restringir la creación de nuevas preguntas.

Cuando una función de comunidad no está segura (no se ha asignado ningún grupo de miembros privilegiados), todos los miembros del sitio de la comunidad pueden crear contenido de funciones (artículos, eventos, temas, preguntas).

>[!NOTE]
>
>Añadir un usuario a un grupo de miembros privilegiados para un sitio de comunidad solo les otorgará privilegios de creación si también son miembros de ese mismo sitio de comunidad.

## Creación de miembros de la comunidad {#creating-community-members}

### Ubicación del repositorio {#repository-location}

Para que determinadas funciones funcionen correctamente, es necesario crear usuarios y grupos de usuarios con los privilegios adecuados.

Cuando los miembros se crean en `/home/users/community`, heredan las ACL adecuadas que otorgan privilegios de lectura a los perfiles de los miembros.

Del mismo modo, los grupos de usuarios de la comunidad personalizados (como los grupos de miembros privilegiados) deben crearse en `/home/groups/community`.

El uso de las consolas [Miembros y grupos de comunidades](members.md) creará usuarios y grupos en estas rutas.

Para especificar una ruta de acceso personalizada, es necesario utilizar la IU de seguridad clásica, a la que se puede acceder desde [https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin).

Para otorgar privilegios de lectura para rutas de miembros personalizadas, en todas las instancias de publicación establezca ACL similares a `/home/users/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="everyone"
  rep:privileges="{Name}[jcr:read]" >
  <rep:restrictions
    jcr:primaryType="rep:Restrictions"
    rep:glob="*/profile*" />
</allow>
```

Para otorgar los privilegios adecuados para las rutas de grupo de miembros personalizadas, como /home/groups/miempresa, en todas las instancias de publicación establezca ACL similares a `/home/groups/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### Consolas {#consoles}

Solo hay cuatro consolas independientes disponibles en el entorno de creación:

| console | Herramientas, Seguridad, Usuarios | Herramientas, Seguridad, Grupos | Comunidades, miembros | Comunidades, grupos |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| administra | usuarios en el autor | grupos de usuarios en el autor | miembros en la publicación | grupos de miembros al publicar |
| requiere | permiso de administración | permiso de administración | permiso de administración, servicio de túnel, sincronización de usuario para la granja de servidores de publicación | permiso de administración, servicio de túnel, sincronización de usuario para la granja de servidores de publicación |

### Función Administrador de habilitación de la comunidad {#community-enablement-manager-role}

La capacidad de un visitante del sitio para registrarse por sí mismo generalmente no está permitida para una [comunidad de habilitación](overview.md#enablement-community), ya que hay costos asociados con cada miembro. Los alumnos y recursos de habilitación son administrados por un usuario asignado a la [función](#author-group-roles) de `enablement manager` [durante la creación del sitio](sites-console.md#enablement) en el autor (agregado como miembro del grupo `Community <site-name> Siteenablementmanagers`). El `enablement manager` también es responsable de [asignar recursos de aprendizaje](resources.md) a los miembros de la comunidad del autor.

Solo los usuarios que son miembros del grupo `Community Enablement Managers` global pueden seleccionarse como `enablement manager` para un sitio de comunidad específico.

Para crear un usuario al que se le pueda asignar la función de `Community Site Enablement Manager`, utilice la consola de seguridad de la IU clásica para especificar la ruta:

En una instancia de autor:

1. Iniciado con privilegios de administrador, vaya a la consola de seguridad clásica de la interfaz de usuario.

   Por ejemplo: [http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. En el menú Editar, seleccione **[!UICONTROL Crear usuario]**.
3. Complete el cuadro de diálogo `Create User`.
   * La ruta debe ser `/home/users/community`.
4. Seleccione **[!UICONTROL Crear]**.

   ![create-community-user](assets/create-community-user.png)

* En el panel izquierdo, busque el usuario recién creado y seleccione mostrar en el panel derecho.

   ![community-user](assets/view-community-user.png)

En el panel izquierdo:

1. Borre el cuadro de búsqueda y seleccione **[!UICONTROL Ocultar usuarios]**.
2. Busque y arrastre `community-enablementmanagers` a la ficha **[!UICONTROL Grupos]** del nuevo usuario que se muestra en el panel derecho.

   ![assign-group](assets/assign-group.png)

### Función de administrador de comunidad {#community-administrators-role}

Como se indica en el gráfico [Funciones de grupo de creación](#author-group-roles), los miembros del grupo Administradores de comunidad pueden crear sitios de comunidad, administrar sitios, administrar miembros (pueden prohibir miembros de la comunidad) y moderar contenido.

Siga los mismos pasos que para crear y asignar un usuario a la función de [administrador de habilitación](#communitysiteenablementmanagerrole), pero agregue el grupo c `ommunity-administrators` en la ficha Grupos del usuario.

### Integración de LDAP {#ldap-integration}

AEM admite el uso de LDAP para la autenticación de usuarios, así como la creación de cuentas de usuario. Esto se detalla en [Configuración de LDAP con AEM 6](../../help/sites-administering/ldap-config.md).

A continuación se proporcionan algunos detalles de configuración específicos para miembros de la comunidad y grupos de miembros.

1. Configure LDAP para cada instancia de publicación AEM.
2. [Proveedor de identidad LDAP](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * No hay instrucciones especiales

3. [Controlador de sincronización](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * Establezca las siguientes propiedades:

      * **[!UICONTROL Pertenencia]** automática del usuario:  `community-<site name>-<uid>-members`
      * **[!UICONTROL Prefijo]** de ruta de usuario:  `/community`
      * **[!UICONTROL Prefijo]** de ruta de grupo:  `/community`

4. [Módulo de inicio de sesión externo](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * sin instrucciones especiales

Esto hace que los usuarios se asignen automáticamente al grupo de miembros del sitio de la comunidad y que la ubicación del repositorio sea `/home/users/community` y `/home/groups/community`, de modo que hereden los permisos adecuados para ver el perfil de los demás.

* El valor `User auto membership` debe ser la propiedad `rep:authorizableId`, no el `givenName` (nombre para mostrar) del perfil.

## Sincronización de usuarios entre instancias de AEM {#synchronizing-users-among-aem-instances}

Al utilizar un [conjunto de servidores de publicación](topologies.md), asegúrese de que los usuarios tengan la misma ruta en cada instancia de publicación importando los usuarios primero a una instancia y [habilitando la sincronización de usuarios](sync.md) para que Sling distribuya los usuarios a las demás instancias de publicación.

Si importa grupos de usuarios, para asegurarse de que los grupos de usuarios tienen la misma ruta en cada instancia de publicación, importe a una instancia, [cree un paquete](../../help/sites-administering/package-manager.md#creating-a-new-package) para la exportación e instale dicho paquete en todas las demás instancias de publicación.

Aunque la sincronización de grupos de usuarios mediante la sincronización de usuarios se incluirá en una versión futura, actualmente solo se sincronizará la *pertenencia* de un grupo de usuarios cuando se ejecute la sincronización de usuarios.

## Acerca de los grupos de la comunidad {#about-community-groups}

Al discutir grupos, hay dos temas diferentes:

* **[Grupos de la comunidad](overview.md#communitygroups)**

   Los grupos comunitarios son las subcomunidades que pueden crearse en el entorno de publicación de un sitio comunitario que apoya la creación de grupos comunitarios. La creación de un grupo de comunidad resulta en más páginas agregadas al sitio web y administradas de manera similar al sitio de la comunidad principal. Para obtener más información, visite [Community Group Essentials](essentials-groups.md) para desarrolladores y [Community Group](creating-groups.md) para autores.

* **[Grupos de miembros](../../help/sites-administering/security.md)**

   Los grupos de miembros son los grupos a los que pueden pertenecer los miembros y que se administran a través de la consola Grupos. Gran parte del debate en esta página se ha dedicado a grupos de miembros. Los grupos de miembros creados automáticamente para un sitio de la comunidad, con el prefijo *`Community`*, pueden ser referidos como un grupo de la comunidad, por lo tanto debe considerarse el contexto del debate.
