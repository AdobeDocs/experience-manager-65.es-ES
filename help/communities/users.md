---
title: Administración de usuarios y grupos de usuarios
description: Los usuarios de AEM Communities pueden registrarse y editar sus perfiles automáticamente
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 4237085a-d70d-41de-975d-153f58336daa
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 0%

---

# Administración de usuarios y grupos de usuarios {#managing-users-and-user-groups}

## Información general {#overview}

En AEM Communities, en el entorno de publicación, los usuarios pueden registrarse y editar sus perfiles. Dados los permisos adecuados, también pueden:

* Crear subcomunidades dentro del sitio de la comunidad (consulte ). [grupos comunitarios](creating-groups.md)).

* [Moderar](moderation.md) contenido generado por el usuario (UGC).

* Be [privilegiado](#privileged-members-group) para crear entradas para blogs, calendarios, controles de calidad y foros.

Los usuarios registrados en el entorno de publicación generalmente se denominan *miembros de la comunidad (miembros)* para distinguirlos de *usuarios* en el entorno de creación.

Los permisos se conceden asignando miembros a uno de los [grupos de miembros (usuarios)](#publish-group-roles) se crea dinámicamente cuando el sitio de la comunidad es [created](sites-console.md) o [modificado](sites-console.md#modifying-site-properties) del entorno de creación. Cuando se trabaja desde el entorno de creación, los miembros son visibles desde el entorno de publicación mediante el [servicio túnel](#tunnel-service).

Por diseño, los miembros y grupos de miembros creados en el entorno de publicación no deberían aparecer en el entorno de creación. De forma similar, los usuarios y grupos de usuarios creados en el entorno de creación tienen la intención de permanecer en el entorno de creación.

Cuando los usuarios de autor y los miembros de publicación proceden de la misma lista de usuarios, como sincronizados desde el mismo directorio LDAP, no se consideran el mismo usuario con los mismos permisos y pertenencia a grupos tanto en los entornos de autor como de publicación. Las funciones de miembros y usuarios deben establecerse por separado en la publicación y el autor, según corresponda.

Para un [publicar conjunto de servidores](topologies.md), el registro y las modificaciones realizadas en una instancia de publicación deben sincronizarse con otras instancias de publicación para que tengan acceso a los mismos datos de usuario. Para obtener más información, consulte [Sincronización de usuarios](sync.md), que incluye una sección que describe [¿Qué sucede cuando...?](sync.md#what-happens-when).

### Límites de contribución {#contribution-limits}

Para protegerse contra el correo no deseado, es posible limitar la frecuencia de publicación de contenido por parte de los miembros. Además, es posible limitar automáticamente las contribuciones de los miembros recién registrados.

Para obtener más información, consulte [Límites de contribución de miembros](limits.md).

### Grupos de usuarios creados dinámicamente {#dynamically-created-user-groups}

Cuando se crea un nuevo sitio de comunidad, los nuevos grupos de usuarios se crean dinámicamente con identificadores únicos (uid) y permisos adecuados para diversas funciones administrativas necesarias para administrar el sitio de comunidad en el entorno de creación (consulte [Roles del grupo de autores](#author-group-roles)) o el entorno de publicación (consulte [Publicar roles de grupo](#publish-group-roles)).

Los nombres de los grupos se generan a partir del nombre asignado al sitio durante [creación de sitios de la comunidad](sites-console.md#step13asitetemplate). Los identificadores únicos evitan conflictos de nombres para sitios de comunidad con nombres similares y grupos de comunidad en el mismo servidor.

Por ejemplo, si el nombre del sitio fuese &quot;*enganchar*&quot; para un sitio llamado &quot; Participación &quot;, uno de los grupos de usuarios creados sería:

* Comunidad *Participación* Miembros

## Entorno de creación {#author-environment}

### Servicio de túnel {#tunnel-service}

Cuando se utiliza el entorno de creación para lo siguiente: [crear sitios](sites-console.md), [modificar propiedades del sitio](sites-console.md#modifying-site-properties) y [administrar miembros y grupos de miembros de la comunidad](members.md), es necesario acceder a los usuarios y grupos de usuarios registrados en el entorno de publicación.

El servicio de túnel proporciona este acceso mediante el agente de replicación en el autor.

* Para obtener más información, consulte [instrucciones de configuración](deploy-communities.md#tunnel-service-on-author) en la página implementación.

El [Consola Miembros y grupos de Communities](members.md) tienen el único propósito de administrar usuarios (miembros) y grupos de usuarios (grupos de miembros) registrados únicamente en el entorno de publicación.

Para administrar usuarios y grupos de usuarios registrados en el entorno de creación, utilice el [Consola de seguridad](../../help/sites-administering/security.md)

### Roles del grupo de autores {#author-group-roles}

| Si es miembro del grupo... | Rol principal |
|---|---|
| administradores | El grupo de administradores está formado por administradores del sistema que tienen todas las capacidades de un administrador de la comunidad y la capacidad de administrar el grupo de administradores de la comunidad. |
| Administradores de comunidad | El grupo Administradores de la comunidad se convierte automáticamente en miembro de todos los sitios de la comunidad y de todos los grupos de la comunidad creados en el sitio. Un miembro inicial del grupo Administradores de la comunidad es el grupo Administradores. En el entorno de creación, los administradores de la comunidad pueden crear sitios de la comunidad, administrar sitios, administrar miembros (pueden prohibir a miembros de la comunidad) y moderar contenido. |
| Comunidad &lt;*nombre del sitio*> Sitecontentmanager | AEM El Administrador de contenido de sitios de la comunidad puede realizar tareas tradicionales de creación de contenido, creación de contenido y modificación de páginas para un sitio de la comunidad. |
| Ninguno | Un visitante anónimo del sitio no puede acceder al entorno de creación. |

### Administradores del sistema {#system-administrators}

AEM Los miembros del grupo de administradores son administradores del sistema que pueden realizar la configuración inicial de una instalación de tanto para los entornos de creación como de publicación.

Para fines de demostración y desarrollo, el grupo de administradores tiene un miembro cuyo userid es *administrador* y la contraseña es *administrador*.

Para entornos de producción, se debe modificar el grupo de administradores predeterminado.

Asegúrese de seguir las [Lista de comprobación de seguridad](../../help/sites-administering/security-checklist.md).

## Entorno de publicación {#publish-environment}

### Hacerse miembro {#becoming-a-member}

En el entorno de publicación, según la variable [configuración](sites-console.md#user-management) del sitio de la comunidad, un visitante del sitio puede convertirse en miembro de la comunidad:

* Cuando el sitio de la comunidad es privado (cerrado):
   * Por invitación
   * Por acciones de un administrador

* Cuando el sitio de la comunidad es público (abierto):
   * Mediante registro automático
   * Por inicio de sesión social con Facebook y Twitter

>[!NOTE]
>
>Si el visitante de un sitio se registra como miembro de un sitio de comunidad abierto, automáticamente se convierte en miembro de otros sitios de comunidad abiertos en el mismo entorno de publicación.

### Publicar roles de grupo {#publish-group-roles}

| Si es miembro del grupo... | Rol principal |
|---|---|
| Comunidad &lt;*nombre del sitio*> Miembros | Un miembro del sitio de la comunidad es un usuario registrado. Pueden iniciar sesión, modificar su perfil, unirse a un grupo de comunidad abierto, publicar contenido en la comunidad, enviar mensajes a otros miembros y seguir las actividades del sitio. |
| Comunidad &lt;*nombre del sitio*> Moderadores | Un moderador del sitio de la comunidad es un miembro de la comunidad de confianza que puede moderar el UGC de forma masiva, mediante la consola de moderación o en contexto, en la página en la que se publica el contenido. |
| Comunidad &lt;*nombre del sitio*> &lt;*nombre de grupo*> Miembros | Un miembro de un grupo de comunidad es un miembro de la comunidad que se ha unido a un grupo de comunidad abierto o que ha sido invitado a un grupo de comunidad cerrado. Tienen las capacidades de un miembro para ese grupo de la comunidad dentro del sitio. |
| Comunidad &lt;*nombre del sitio*> Groupadministrators | Un administrador de grupo de sitio de comunidad es un miembro de la comunidad de confianza que tiene asignada la tarea de crear y administrar subcomunidades (grupos) dentro de un sitio de comunidad. Se incluye la capacidad de proporcionar moderación en contexto. |
| *Grupo de seguridad de miembros privilegiados* | Grupo de usuarios creado y mantenido manualmente con el fin de restringir la creación de contenido. Consulte [Grupo de miembros privilegiados](#privileged-members-group). |
| Ninguno | Un visitante anónimo del sitio, que descubre el sitio, puede ver y buscar en sitios de la comunidad que permiten el acceso anónimo. Para participar y publicar contenido, el usuario debe registrarse (si se le permite) y convertirse en miembro de la comunidad. |

### Asignar miembros a roles de grupo de publicación {#assigning-members-to-publish-group-roles}

Cuándo [crear un sitio de la comunidad](sites-console.md) en el entorno de creación o cuando [modificación de propiedades del sitio,](sites-console.md#modifying-site-properties) a los miembros se les pueden asignar diversas funciones realizadas en el entorno de publicación, como moderadores, administradores de grupos, contactos de recursos o miembros privilegiados.

[Activación del servicio de túnel](sync.md#accessingpublishusersfromauthor) da como resultado que las opciones de asignación se presenten desde los miembros al publicar en lugar de desde los usuarios al crear.

Los miembros seleccionados se asignarán automáticamente al [grupo apropiado](#publish-group-roles) y sus suscripciones se incluirán cuando se (re)publique el sitio de la comunidad.

### Grupo de miembros privilegiados {#privileged-members-group}

El propósito de un grupo de seguridad de miembros privilegiados es restringir la creación de contenido para determinadas funciones de la comunidad a un subconjunto privilegiado de los miembros de un sitio de la comunidad.

El grupo de miembros privilegiados es un grupo de miembros creado y administrado mediante [Consola de grupos de Communities](members.md).

Después de crear un grupo de miembros privilegiados, y con la variable [servicio de túnel habilitado](sync.md#accessingpublishusersfromauthor), la estructura de un sitio de la comunidad existente puede ser [modificado](sites-console.md#modify-structure) para editar la configuración de sus funciones de comunidad en &quot;Permitir miembros privilegiados&quot; y añadir el grupo creado.

Las funciones de comunidad que permiten especificar uno o más grupos de miembros privilegiados son:

* [Función Blog](functions.md#blog-function) - Para restringir la creación de nuevos artículos.
* [Función Calendario](functions.md#calendar-function) : para restringir la creación de nuevos eventos.
* [Función Foro](functions.md#forum-function) - Para restringir la creación de nuevos temas.
* [Función QnA](functions.md#qna-function) - Restringir la creación de nuevas preguntas.

Cuando una función de la comunidad no está protegida (no se ha asignado ningún grupo de miembros privilegiados), todos los miembros del sitio de la comunidad pueden crear contenido de funciones (artículos, eventos, temas, preguntas).

>[!NOTE]
>
>Añadir un usuario a un grupo de miembros privilegiados para un sitio de comunidad solo les otorgará privilegios de creación si también son miembros de ese mismo sitio de comunidad.

## Creación de miembros de la comunidad {#creating-community-members}

### Ubicación del repositorio {#repository-location}

Para que determinadas funciones funcionen correctamente, es necesario crear usuarios y grupos de usuarios con los privilegios adecuados.

Cuando se crean miembros en `/home/users/community`Además, heredan las ACL adecuadas que otorgan privilegios de lectura a los perfiles de los miembros.

Del mismo modo, los grupos de usuarios de la comunidad personalizados (como los grupos de miembros privilegiados) deben crearse en `/home/groups/community`.

Uso del [Consola Miembros y grupos de Communities](members.md) creará usuarios y grupos en estas rutas.

Para especificar una ruta personalizada, es necesario utilizar la IU de seguridad clásica, a la que se puede acceder desde [https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin).

Para conceder privilegios de lectura para rutas de miembros personalizadas, en todas las instancias de publicación establezca ACL similares a `/home/users/community`:

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

Para conceder los privilegios adecuados para las rutas de grupo de miembros personalizadas, como /home/groups/mycompany, en todas las instancias de publicación establezca ACL similares a `/home/groups/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### Consolas {#consoles}

Hay cuatro consolas independientes disponibles solo en el entorno de creación:

| consolar | Herramientas, Seguridad, Usuarios | Herramientas, Seguridad, Grupos | Comunidades, Miembros | Comunidades, grupos |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| administra | usuarios en autor | grupos de usuarios en autor | miembros al publicar | grupos de miembros al publicar |
| requiere | permiso de administrador | permiso de administrador | permiso de administrador, servicio de túnel, sincronización de usuarios para la granja de servidores de publicación | permiso de administrador, servicio de túnel, sincronización de usuarios para la granja de servidores de publicación |

### Función Administradores de la comunidad {#community-administrators-role}

Como se indica en la [Roles del grupo de autores](#author-group-roles) , los miembros del grupo Administradores de la comunidad pueden crear sitios de la comunidad, administrar sitios, administrar miembros (pueden prohibir miembros de la comunidad) y moderar contenido.

Siga los mismos pasos que para crear y asignar un usuario a la función de administrador de habilitación, pero agregue c `ommunity-administrators` en la pestaña Grupos del usuario.

### Integración de LDAP {#ldap-integration}

AEM Compatibilidad con el uso de LDAP para la autenticación de usuarios y la creación de cuentas de usuario. Esto se detalla en [AEM Configuración de LDAP con 6](../../help/sites-administering/ldap-config.md).

A continuación se muestran algunos detalles de configuración específicos de los miembros y grupos de miembros de la comunidad.

1. AEM Configure LDAP para cada instancia de publicación de la.
2. [El proveedor de identidad LDAP](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * No hay instrucciones especiales

3. [El controlador de sincronización](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * Establezca las siguientes propiedades:

      * **[!UICONTROL Abono automático de usuario]**: `community-<site name>-<uid>-members`
      * **[!UICONTROL Prefijo de ruta de usuario]**: `/community`
      * **[!UICONTROL Prefijo de ruta de grupo]**: `/community`

4. [El módulo de inicio de sesión externo](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * no hay instrucciones especiales

Esto hace que los usuarios se asignen automáticamente al grupo de miembros del sitio de la comunidad y que la ubicación del repositorio sea `/home/users/community` y `/home/groups/community`, para que hereden los permisos adecuados para ver el perfil del otro.

* El `User auto membership` el valor debe ser `rep:authorizableId` propiedad, no el `givenName` (nombre para mostrar) del perfil.

## AEM Sincronización de usuarios entre instancias de {#synchronizing-users-among-aem-instances}

Cuando se utiliza un [publicar conjunto de servidores](topologies.md), asegúrese de que los usuarios tengan la misma ruta en cada instancia de publicación importando primero los usuarios a una instancia y [habilitar sincronización de usuarios](sync.md) para Sling, distribuya los usuarios a las demás instancias de publicación.

Si importa grupos de usuarios, para asegurarse de que los grupos de usuarios tengan la misma ruta en cada instancia de publicación, importe a una instancia y, a continuación, [creación de un paquete](../../help/sites-administering/package-manager.md#creating-a-new-package) para la exportación e instale ese paquete en todas las demás instancias de publicación.

Aunque la sincronización de grupos de usuarios mediante la sincronización de usuarios se incluirá en una versión futura, actualmente solo el *abono* de un grupo de usuarios se sincronizará cuando se ejecute la sincronización de usuarios.

## Acerca de los grupos de comunidad {#about-community-groups}

Cuando se tratan los grupos, hay dos temas distintos:

* **[Grupos de comunidad](overview.md#communitygroups)**

  Los grupos de comunidad son las subcomunidades que se pueden crear en el entorno de publicación para un sitio de comunidad que apoye la creación de grupos de comunidad. La creación de un grupo de comunidad resulta en más páginas agregadas al sitio web y se administran de una manera similar a su sitio de comunidad principal. Para obtener más información, visite [Elementos esenciales del grupo de comunidad](essentials-groups.md) para desarrolladores y [Grupo de comunidad](creating-groups.md) para autores.

* **[Grupos de miembros](../../help/sites-administering/security.md)**

  Los grupos de miembros son los grupos a los que pueden pertenecer los miembros y se administran mediante la consola Grupos. Gran parte del debate de esta página se ha dedicado a los grupos de miembros. Los grupos de miembros creados automáticamente para un sitio de la comunidad, que llevan el prefijo *`Community`*, puede denominarse grupo comunitario, por lo que debe considerarse el contexto de la discusión.
