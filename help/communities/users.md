---
title: Administración de usuarios y grupos de usuarios
seo-title: Managing Users and User Groups
description: Los usuarios de AEM Communities pueden registrarse y editar sus perfiles
seo-description: Users of AEM Communities can self-register and edit their profiles
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
role: Admin
exl-id: 4237085a-d70d-41de-975d-153f58336daa
source-git-commit: cc0574ae22758d095a3ca6b91f0ceae4a8691f0e
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 0%

---

# Administración de usuarios y grupos de usuarios {#managing-users-and-user-groups}

## Información general {#overview}

En AEM Communities, en el entorno de publicación, los usuarios pueden registrarse automáticamente y editar sus perfiles. Dados los permisos adecuados, también pueden:

* Crear subcomunidades dentro del sitio de la comunidad (consulte [grupos de la comunidad](creating-groups.md)).

* [Moderar](moderation.md) contenido generado por el usuario (UGC).

* Be [privilegiado](#privileged-members-group) para crear entradas para blogs, calendarios, QnA y foros.

Los usuarios registrados en el entorno de publicación suelen denominarse *miembros de la comunidad (miembros)* para distinguirlos de *usuarios* en el entorno de creación.

Los permisos se conceden asignando miembros a uno de los [grupos de miembros (usuarios)](#publish-group-roles) creado dinámicamente cuando el sitio de comunidad es [created](sites-console.md) o [modificado](sites-console.md#modifying-site-properties) del entorno de creación. Al trabajar desde el entorno de creación, los miembros se pueden ver desde el entorno de publicación mediante la variable [servicio de túnel](#tunnel-service).

Por diseño, los miembros y los grupos de miembros creados en el entorno de publicación no deberían aparecer en el entorno de creación. Los usuarios y grupos de usuarios creados en el entorno de creación tienen la misma intención de permanecer en el entorno de creación.

Cuando los usuarios del autor y los miembros de la publicación provienen de la misma lista de usuarios, como sincronizados desde el mismo directorio LDAP, no se consideran el mismo usuario con los mismos permisos y pertenencia a grupos en los entornos de autor y publicación. Las funciones de los miembros y usuarios deben establecerse por separado en el momento de la publicación y del autor, según proceda.

Para un [publicar granja](topologies.md), el registro y las modificaciones realizadas en una instancia de publicación deben sincronizarse con otras instancias de publicación para que tengan acceso a los mismos datos de usuario. Para obtener más información, consulte [Sincronización de usuarios](sync.md), que incluye una sección que describe [Qué sucede cuando...](sync.md#what-happens-when).

### Límites de contribución {#contribution-limits}

Para protegerse contra el spam, es posible limitar la frecuencia de publicación del contenido por parte de los miembros. Además, es posible limitar automáticamente las contribuciones de los miembros recién inscritos.

Para obtener más información, consulte [Límites de contribución de miembros](limits.md).

### Grupos de usuarios creados dinámicamente {#dynamically-created-user-groups}

Cuando se crea un nuevo sitio de comunidad, se crean nuevos grupos de usuarios de forma dinámica con id únicos (uid) y permisos adecuados para diversas funciones administrativas necesarias para administrar el sitio de la comunidad en el entorno de creación (consulte [Funciones del grupo de creación](#author-group-roles)) o el entorno de publicación (consulte [Publicar funciones de grupo](#publish-group-roles)).

Los nombres de los grupos se generan a partir del nombre dado al sitio durante [creación de sitios de comunidad](sites-console.md#step13asitetemplate). Los identificadores únicos evitan conflictos de nombres para sitios de comunidad y grupos de comunidades con nombres similares en el mismo servidor.

Por ejemplo, si el nombre del sitio fuera &quot;*participación*&quot; para un sitio titulado &quot;We.Retail Engage&quot;, uno de los grupos de usuarios creados sería:

* Comunidad *Participación* Miembros

## Entorno de creación {#author-environment}

### Servicio de túnel {#tunnel-service}

Al utilizar el entorno de creación para [crear sitios](sites-console.md), [modificar las propiedades del sitio](sites-console.md#modifying-site-properties) y [administrar miembros de la comunidad y grupos de miembros](members.md), es necesario acceder a los usuarios y grupos de usuarios registrados en el entorno de publicación.

El servicio de túnel proporciona este acceso mediante el agente de replicación en el autor.

* Para obtener más información, consulte [instrucciones de configuración](deploy-communities.md#tunnel-service-on-author) en la página de implementación.

La variable [Consolas Miembros y Grupos de Comunidades](members.md) tienen el único propósito de administrar usuarios (miembros) y grupos de usuarios (grupos de miembros) registrados únicamente en el entorno de publicación.

Para administrar los usuarios y grupos de usuarios registrados en el entorno de creación, use la variable [Consola de seguridad](../../help/sites-administering/security.md)

### Funciones del grupo de creación {#author-group-roles}

| Si es miembro del grupo... | Función principal |
|---|---|
| administradores | El grupo de administradores está formado por administradores de sistemas que tienen todas las capacidades de un administrador de la comunidad, así como la capacidad de gestionar el grupo de administradores de la comunidad. |
| Administradores de la comunidad | El grupo Administradores de la comunidad se convierte automáticamente en miembro de todos los sitios de la comunidad y de cualquier grupo de la comunidad creado en el sitio. Un miembro inicial del grupo Administradores de la comunidad es el grupo de administradores. En el entorno de creación, los administradores de la comunidad pueden crear sitios de la comunidad, administrar sitios, administrar miembros (pueden prohibir miembros de la comunidad) y moderar contenido. |
| Comunidad &lt;*nombre del sitio*> Sitecontentmanager | El Administrador de contenido de sitios de la comunidad puede realizar la creación de AEM tradicional, la creación de contenido y la modificación de páginas para un sitio de la comunidad. |
| Ninguno | Es posible que un visitante anónimo del sitio no acceda al entorno de creación. |

### Administradores del sistema {#system-administrators}

Los miembros del grupo de administradores son administradores del sistema que pueden realizar la configuración inicial de una instalación de AEM para los entornos de autor y publicación.

Para fines de demostración y desarrollo, el grupo de administradores tiene un miembro cuyo userid es *admin* y la contraseña es *admin*.

Para los entornos de producción, se debe modificar el grupo de administradores predeterminado.

Asegúrese de seguir la [Lista de comprobación de seguridad](../../help/sites-administering/security-checklist.md).

## Entorno de publicación {#publish-environment}

### Convertirse en miembro {#becoming-a-member}

En el entorno de publicación, según la variable [configuración](sites-console.md#user-management) del sitio de la comunidad, el visitante del sitio puede convertirse en miembro de la comunidad:

* Cuando el sitio de la comunidad es privado (cerrado):
   * Por invitación
   * Mediante acciones de un administrador

* Cuando el sitio de la comunidad es público (abierto):
   * Por registro propio
   * Mediante inicio de sesión social con Facebook y Twitter

>[!NOTE]
>
>Si el visitante de un sitio se registra como miembro de un sitio de comunidad abierto, automáticamente se convierte en miembro de otros sitios de comunidad abiertos en el mismo entorno de publicación.

### Publicar funciones de grupo {#publish-group-roles}

| Si es miembro del grupo... | Función principal |
|---|---|
| Comunidad &lt;*nombre del sitio*> Miembros | Un miembro del sitio de la comunidad es un usuario registrado. Pueden iniciar sesión, modificar su perfil, unirse a un grupo de comunidad abierto, publicar contenido en la comunidad, enviar mensajes a otros miembros y seguir las actividades del sitio. |
| Comunidad &lt;*nombre del sitio*> Moderadores | Un moderador de sitio de la comunidad es un miembro de la comunidad de confianza que puede moderar UGC de forma masiva, mediante la consola de moderación o en contexto, en la página en la que se publica el contenido. |
| Comunidad &lt;*nombre del sitio*> &lt;*nombre del grupo*> Miembros | Un miembro del grupo comunitario es un miembro de la comunidad que se ha unido a un grupo de la comunidad abierta o ha sido invitado a un grupo de la comunidad cerrado. Tienen las capacidades de un miembro para ese grupo de la comunidad dentro del sitio. |
| Comunidad &lt;*nombre del sitio*> Administradores de grupos | Un administrador de grupo de sitios de la comunidad es un miembro de la comunidad de confianza que está asignado para crear y administrar subcomunidades (grupos) dentro de un sitio de la comunidad. Se incluye la capacidad de proporcionar moderación en contexto. |
| *Grupo de seguridad de miembros privilegiados* | Grupo de usuarios creado y mantenido manualmente con el fin de restringir la creación de contenido. Consulte [Grupo de miembros privilegiados](#privileged-members-group). |
| Ninguno | Un visitante anónimo del sitio, que descubra el sitio, puede ver y buscar sitios de la comunidad que permitan el acceso anónimo. Para participar y publicar contenido, el usuario debe registrarse (si se permite) y convertirse en miembro de la comunidad. |

### Asignación de miembros a funciones de grupo de publicación {#assigning-members-to-publish-group-roles}

When [creación de un sitio de comunidad](sites-console.md) en el entorno de creación o cuando [modificar las propiedades del sitio,](sites-console.md#modifying-site-properties) a los miembros se les pueden asignar diversas funciones realizadas en el entorno de publicación, como moderadores, administradores de grupos, contactos de recursos o miembros privilegiados.

[Activación del servicio de túnel](sync.md#accessingpublishusersfromauthor) como resultado, las opciones de asignación se presentan desde miembros en la publicación en lugar de usuarios en el autor.

Los miembros seleccionados se asignarán automáticamente al [grupo apropiado](#publish-group-roles) y sus pertenencias se incluirán cuando el sitio de la comunidad se vuelva a publicar.

### Grupo de miembros privilegiados {#privileged-members-group}

El objetivo de un grupo de seguridad de miembros privilegiados es restringir la creación de contenido para ciertas funciones de la comunidad a un subconjunto privilegiado de miembros de un sitio de la comunidad.

El grupo de miembros privilegiados es un grupo de miembros creado y administrado mediante la variable [Consola Grupos de comunidades](members.md).

Después de crear un grupo de miembros privilegiados y con la variable [servicio de túnel habilitado](sync.md#accessingpublishusersfromauthor), la estructura de un sitio de comunidad existente puede ser [modificado](sites-console.md#modify-structure) para editar la configuración de sus funciones de comunidad en &quot;Permitir miembros privilegiados&quot; y añadir el grupo creado.

Las funciones de la comunidad que permiten especificar uno o más grupos de miembros privilegiados son:

* [Función del blog](functions.md#blog-function) - Restringir la creación de nuevos artículos.
* [Función del calendario](functions.md#calendar-function) - Restringir la creación de nuevos eventos.
* [Función de foro](functions.md#forum-function) - Restringir la creación de nuevos temas.
* [Función QnA](functions.md#qna-function) - Restringir la creación de nuevas preguntas.

Cuando una función de comunidad no está segura (no se ha asignado ningún grupo de miembros privilegiados), todos los miembros del sitio de la comunidad pueden crear contenido de funciones (artículos, eventos, temas, preguntas).

>[!NOTE]
>
>Agregar un usuario a un grupo de miembros privilegiados para un sitio de comunidad solo les otorgará privilegios de creación si también son miembros de ese mismo sitio de comunidad.

## Creación de miembros de la comunidad {#creating-community-members}

### Ubicación del repositorio {#repository-location}

Para que ciertas funciones funcionen correctamente, es necesario crear usuarios y grupos de usuarios con los privilegios adecuados.

Cuando los miembros se crean en `/home/users/community`, heredan las ACL adecuadas que otorgan privilegios de lectura a los perfiles de los miembros.

Del mismo modo, los grupos de usuarios de la comunidad personalizados (como los grupos de miembros privilegiados) deben crearse en `/home/groups/community`.

Al usar la variable [Consolas Miembros y Grupos de Comunidades](members.md) creará usuarios y grupos en estas rutas.

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

Para conceder los privilegios adecuados para las rutas de grupos de miembros personalizadas, como /home/groups/mycompany, en todas las instancias de publicación establezca ACL similares a `/home/groups/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### Consolas {#consoles}

Hay cuatro consolas independientes disponibles solo en el entorno de creación:

| consola | Herramientas, Seguridad, Usuarios | Herramientas, Seguridad, Grupos | Comunidades, miembros | Comunidades, grupos |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| administre | usuarios en author | grupos de usuarios en author | miembros al publicar | grupos de miembros al publicar |
| requirements | permiso de administrador | permiso de administrador | permiso de administrador, servicio de túnel, sincronización de usuarios para la granja de publicaciones | permiso de administrador, servicio de túnel, sincronización de usuarios para la granja de publicaciones |

### Función de administradores de la comunidad {#community-administrators-role}

Como se indica en la [Funciones del grupo de creación](#author-group-roles) , los miembros del grupo Administradores de la comunidad pueden crear sitios de la comunidad, administrar sitios, administrar miembros (pueden prohibir a los miembros de la comunidad) y moderar contenido.

Siga los mismos pasos que para crear y asignar un usuario a la función de administrador de habilitación, pero agregue c `ommunity-administrators` en la ficha Grupos del usuario.

### Integración LDAP {#ldap-integration}

AEM admite el uso de LDAP para la autenticación de usuarios, así como la creación de cuentas de usuario. Esto se detalla en [Configuración de LDAP con AEM 6](../../help/sites-administering/ldap-config.md).

A continuación se detallan algunos detalles de configuración específicos para miembros de la comunidad y grupos de miembros.

1. Configure LDAP para cada instancia de publicación AEM.
2. [El proveedor de identidad LDAP](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * No hay instrucciones especiales

3. [Controlador de sincronización](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * Establezca las siguientes propiedades:

      * **[!UICONTROL Pertenencia automática del usuario]**: `community-<site name>-<uid>-members`
      * **[!UICONTROL Prefijo de ruta de usuario]**: `/community`
      * **[!UICONTROL Prefijo de ruta de grupo]**: `/community`

4. [El módulo de inicio de sesión externo](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * instrucciones especiales

Esto hace que los usuarios se asignen automáticamente al grupo de miembros del sitio de la comunidad y a la ubicación del repositorio `/home/users/community` y `/home/groups/community`, de modo que hereden los permisos adecuados para ver el perfil de los demás.

* La variable `User auto membership` debe ser `rep:authorizableId` no la propiedad `givenName` (nombre para mostrar) del perfil.

## Sincronización de usuarios entre instancias de AEM {#synchronizing-users-among-aem-instances}

Al usar un [publicar granja](topologies.md), asegúrese de que los usuarios tengan la misma ruta en cada instancia de publicación importando primero a los usuarios y [activación de la sincronización de usuarios](sync.md) para que Sling distribuya los usuarios a las demás instancias de publicación.

Si importa grupos de usuarios, para asegurarse de que los grupos de usuarios tengan la misma ruta en cada instancia de publicación, importe a una instancia y, a continuación, [crear un paquete](../../help/sites-administering/package-manager.md#creating-a-new-package) para exportar e instalar ese paquete en todas las demás instancias de publicación.

Aunque la sincronización de grupos de usuarios mediante la sincronización de usuarios se incluirá en una versión futura, actualmente solo la variable *abono* de un grupo de usuarios se sincronizará cuando se ejecute la sincronización de usuarios.

## Acerca de los grupos de comunidades {#about-community-groups}

Al discutir grupos, hay dos temas diferentes:

* **[Grupos de la comunidad](overview.md#communitygroups)**

   Los grupos comunitarios son las subcomunidades que pueden crearse en el entorno de publicación de un sitio comunitario que apoya la creación de grupos comunitarios. La creación de un grupo de comunidad da como resultado más páginas agregadas al sitio web y se administran de manera similar al sitio de la comunidad principal. Para obtener más información, visite [Community Group Essentials](essentials-groups.md) para desarrolladores y [Grupo de la comunidad](creating-groups.md) para autores.

* **[Grupos de miembros](../../help/sites-administering/security.md)**

   Los grupos de miembros son los grupos a los que los miembros pueden pertenecer y se administran a través de la consola Grupos . Gran parte del debate en esta página se ha dedicado a grupos miembros. Los grupos de miembros se crean automáticamente para un sitio de comunidad, con el prefijo *`Community`*, puede denominarse grupo comunitario, por lo que debe considerarse el contexto de la discusión.
