---
title: Administración de usuarios y grupos de usuarios
seo-title: Administración de usuarios y grupos de usuarios
description: Los usuarios de Comunidades AEM pueden registrarse y editar sus perfiles
seo-description: Los usuarios de Comunidades AEM pueden registrarse y editar sus perfiles
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Managing Users and User Groups {#managing-users-and-user-groups}

## Información general {#overview}

En AEM Communities, en el entorno de publicación, los usuarios pueden registrarse automáticamente y editar sus perfiles. Dados los permisos adecuados, también podrán

* Crear subcomunidades dentro del sitio de la comunidad (ver grupos [de](creating-groups.md)la comunidad)
* [Moderar](moderation.md) contenido generado por el usuario (UGC)
* Estar [habilitando contactos de recursos](resources.md)
* Tenga [el privilegio](#privileged-members-group) de crear entradas para blogs, calendarios, QnA y foros

Los usuarios registrados en el entorno de publicación generalmente se conocen como miembros de *la comunidad (miembros)* para distinguirlos de *usuarios *en el entorno de creación.

Los permisos se conceden asignando miembros a uno de los grupos [de](#publish-group-roles) miembros (usuarios) creados dinámicamente cuando el sitio de comunidad se [crea](sites-console.md) o [modifica](sites-console.md#modifying-site-properties) desde el entorno de creación. Cuando se trabaja desde el entorno de creación, los miembros son visibles desde el entorno de publicación mediante el servicio [de](#tunnel-service)túnel.

Por diseño, los miembros y los grupos de miembros creados en el entorno de publicación no deberían aparecer en el entorno de creación. Los usuarios y los grupos de usuarios creados en el entorno de creación tienen la misma intención de permanecer en el entorno de creación.

Cuando los usuarios que participan en la creación y los miembros en la publicación provienen de la misma lista de usuarios, como sincronizados desde el mismo directorio LDAP, no se consideran el mismo usuario con los mismos permisos y pertenencia a grupos en los entornos de creación y publicación. Las funciones de los miembros y usuarios deben establecerse por separado al publicar y crear, según proceda.

Para un conjunto de servidores [de](topologies.md)publicación, el registro y las modificaciones realizadas en una instancia de publicación deben sincronizarse con otras instancias de publicación para que tengan acceso a los mismos datos de usuario. [Para obtener más información, consulte Sincronización ](sync.md)de usuarios[, que incluye una sección en la que se describe ](sync.md#what-happens-when)Qué sucede cuando... .

### Límites de contribución {#contribution-limits}

Para protegerse del spam, es posible limitar la frecuencia de publicación del contenido de los miembros. Además, es posible limitar automáticamente las contribuciones de los miembros recién inscritos.

Para obtener más información, consulte Límites de contribución [de miembros](limits.md).

### Grupos de usuarios creados dinámicamente {#dynamically-created-user-groups}

Cuando se crea un nuevo sitio de comunidad, se crean de forma dinámica nuevos grupos de usuarios con identificadores únicos (uid) y permisos adecuados para diversas funciones administrativas necesarias para administrar el sitio de comunidad en el entorno de creación (consulte Funciones [de grupo de](#author-group-roles)autores) o en el entorno de publicación (consulte [Publicar funciones](#publish-group-roles)de grupo).

Los nombres de los grupos se generan a partir del nombre dado al sitio durante la creación [del sitio de la](sites-console.md#step13asitetemplate)comunidad. Los identificadores únicos evitan conflictos de nombres para sitios de comunidad con nombres similares y grupos de comunidad en el mismo servidor.

Por ejemplo, si el nombre del sitio fuera &quot;*comprometer*&quot; para un sitio llamado &quot;Compromiso de We.Retail&quot;, uno de los grupos de usuarios creados sería:

* Miembros de *participación* de la comunidad

## Entorno de creación {#author-environment}

### Servicio de túnel {#tunnel-service}

Al utilizar el entorno de creación para [crear sitios](sites-console.md), [modificar propiedades](sites-console.md#modifying-site-properties) del sitio y [administrar miembros de la comunidad y grupos](members.md)de miembros, es necesario acceder a los usuarios y grupos de usuarios registrados en el entorno de publicación.

El servicio de túnel proporciona este acceso mediante el agente de replicación del autor.

* Para obtener más información, consulte las instrucciones [de](deploy-communities.md#tunnel-service-on-author) configuración en la página de implementación

Las consolas [Miembros y Grupos de](members.md) comunidades tienen el único propósito de administrar usuarios (miembros) y grupos de usuarios (grupos de miembros) registrados únicamente en el entorno de publicación.

Para administrar usuarios y grupos de usuarios registrados en el entorno de creación, utilice la consola [Seguridad](../../help/sites-administering/security.md)

### Funciones de grupo de creación {#author-group-roles}

| Si es miembro del grupo... | Función principal |
|---|---|
| administradores | El grupo de administradores está formado por administradores de sistema que tienen todas las capacidades de un administrador de comunidad, así como la capacidad de administrar el grupo de administradores de comunidad. |
| Administradores de la comunidad | El grupo Administradores de la comunidad se convierte automáticamente en miembro de todos los sitios de la comunidad y de cualquier grupo de la comunidad creado en el sitio. Un miembro inicial del grupo Administradores de comunidad es el grupo de administradores. En el entorno de creación, los administradores de la comunidad pueden crear sitios de la comunidad, administrar sitios, administrar miembros (pueden prohibir miembros de la comunidad) y moderar contenido. |
| Comunidad &lt;nombre ** del sitio> Sitecontentmanager | Community Site Content Manager puede realizar la creación tradicional de AEM, la creación de contenido y la modificación de páginas para un sitio de comunidad. |
| Administradores de habilitación de la comunidad | El grupo Administradores de habilitación de la comunidad está formado por usuarios que están disponibles para asignación para administrar el grupo Administradores de habilitación de un sitio de la comunidad. |
| Comunidad &lt;nombre *del sitio* > Administradores de habilitación de sitios | El grupo Administradores de habilitación de sitio de comunidad está formado por usuarios que han sido asignados para administrar [los recursos](resources.md)de habilitación de un sitio de comunidad. |
| Ninguna | Es posible que un visitante anónimo del sitio no tenga acceso al entorno de creación. |

### Administradores de sistemas {#system-administrators}

Los miembros del grupo de administradores son administradores del sistema que pueden realizar la configuración inicial de una instalación de AEM tanto para los entornos de creación como de publicación.

Para fines de demostración y desarrollo, el grupo de administradores tiene un miembro cuyo userid es *administrador* y la contraseña es *administrador*.

Para los entornos de producción, se debe modificar el grupo de administradores predeterminado.

Asegúrese de seguir la lista de comprobación [de seguridad](../../help/sites-administering/security-checklist.md).

## Entorno de publicación {#publish-environment}

### Cómo hacerse miembro {#becoming-a-member}

En el entorno de publicación, según la [configuración](sites-console.md#user-management) del sitio de la comunidad, un visitante del sitio puede convertirse en miembro de la comunidad

* Cuando el sitio de la comunidad es privado (cerrado):
   * Por invitación
   * Por acciones de un administrador

* Cuando el sitio de la comunidad es público (abierto):
   * Por inscripción automática
   * Por inicio de sesión social con Facebook y Twitter

>[!NOTE]
>
>Si un visitante del sitio se registra como miembro de un sitio de comunidad abierta, automáticamente se convierte en miembro de otros sitios de comunidad abiertos en el mismo entorno de publicación.

### Publicar funciones de grupo {#publish-group-roles}

| Si es miembro del grupo... | Función principal |
|---|---|
| Miembros de la comunidad &lt;nombre *del* sitio> | Un miembro del sitio de la comunidad es un usuario registrado. Pueden iniciar sesión, modificar su perfil, unirse a un grupo de la comunidad abierta, publicar contenido en la comunidad, enviar mensajes a otros miembros y seguir las actividades del sitio. |
| Moderadores de la comunidad &lt;nombre *del* sitio> | Un moderador del sitio de la comunidad es un miembro de la comunidad de confianza que puede moderar UGC de forma masiva, mediante la consola de moderación o en contexto, en la página en la que se anuncia el contenido. |
| Comunidad &lt;nombre ** del sitio> &lt;nombre del *grupo*> Miembros | Un miembro del grupo comunitario es un miembro de la comunidad que se ha unido a un grupo de la comunidad abierta o que ha sido invitado a un grupo de la comunidad cerrado. Tienen las capacidades de un miembro para ese grupo de la comunidad dentro del sitio. |
| Comunidad &lt;nombre ** del sitio> Administradores de grupos | Un administrador de grupos de sitios de la comunidad es un miembro de la comunidad de confianza que está asignado para crear y administrar subcomunidades (grupos) dentro de un sitio de la comunidad. Se incluye la capacidad de proporcionar moderación en contexto. |
| *Grupo de seguridad de miembros privilegiados* | Grupo de usuarios creado y mantenido manualmente con el fin de restringir la creación de contenido. Consulte Grupo [de miembros](#privileged-members-group)privilegiados. |
| Ninguna | Un visitante anónimo del sitio, que descubre el sitio, puede ver y buscar sitios de la comunidad que permiten el acceso anónimo. Para participar y publicar contenido, el usuario debe registrarse (si se permite) y convertirse en miembro de la comunidad. |

### Asignación de miembros a funciones de grupo de publicación {#assigning-members-to-publish-group-roles}

Al [crear un sitio](sites-console.md) de comunidad en el entorno de creación o al [modificar las propiedades del sitio,](sites-console.md#modifying-site-properties) se pueden asignar a los miembros diversas funciones realizadas en el entorno de publicación, como moderadores, administradores de grupos, contactos de recursos o miembros privilegiados.

[Al habilitar el servicio](sync.md#accessingpublishusersfromauthor) de túnel, se presentan las opciones de asignación de los miembros en la publicación en lugar de los usuarios del autor.

Los miembros seleccionados se asignarán automáticamente al grupo [](#publish-group-roles) correspondiente y sus miembros se incluirán cuando se vuelva a publicar el sitio de la comunidad.

### Grupo de miembros privilegiados {#privileged-members-group}

El propósito de un grupo de seguridad de miembros privilegiados es restringir la creación de contenido para ciertas funciones de la comunidad a un subconjunto privilegiado de miembros del sitio de la comunidad.

El grupo de miembros privilegiados es un grupo de miembros creado y administrado mediante la consola [Grupos de](members.md)comunidades.

Después de crear un grupo de miembros privilegiados y de habilitar [el servicio de](sync.md#accessingpublishusersfromauthor)túnel, se puede [modificar](sites-console.md#modify-structure) la estructura de un sitio de comunidad existente para editar la configuración de sus funciones de comunidad en &quot;Permitir miembros privilegiados&quot; y agregar el grupo creado.

Las funciones de comunidad que permiten especificar uno o más grupos de miembros privilegiados son:

* [Función](functions.md#blog-function) de blog - para restringir la creación de nuevos artículos
* [Función](functions.md#calendar-function) de calendario: para restringir la creación de nuevos eventos
* [Función](functions.md#forum-function) Foro: para restringir la creación de nuevos temas
* [Función](functions.md#qna-function) QnA: para restringir la creación de nuevas preguntas

Cuando una función de comunidad no está segura (no se ha asignado ningún grupo de miembros privilegiados), todos los miembros del sitio de la comunidad pueden crear contenido de funciones (artículos, eventos, temas, preguntas).

>[!NOTE]
>
>Agregar un usuario a un grupo de miembros privilegiados para un sitio de comunidad solo les otorgará privilegios de creación si también son miembros de ese mismo sitio de comunidad.

## Creación de miembros de la comunidad {#creating-community-members}

### Ubicación del repositorio {#repository-location}

Para que determinadas funciones funcionen correctamente, es necesario crear usuarios y grupos de usuarios con los privilegios adecuados.

Cuando se crean miembros en `/home/users/community`, heredan las ACL adecuadas que otorgan privilegios de lectura a los perfiles de los miembros.

Del mismo modo, se deben crear grupos de usuarios de comunidad personalizados (como grupos de miembros privilegiados) en `/home/groups/community`.

El uso de las consolas [Miembros y grupos de](members.md) comunidades creará usuarios y grupos en estas rutas.

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

Hay cuatro consolas independientes disponibles solo en el entorno de creación:

| console | Herramientas, Seguridad, Usuarios | Herramientas, Seguridad, Grupos | Comunidades, miembros | Comunidades, grupos |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| administra | usuarios en el autor | grupos de usuarios en el autor | miembros en la publicación | grupos de miembros al publicar |
| requiere | permiso de administración | permiso de administración | permiso de administración, servicio de túnel, sincronización de usuario para la granja de servidores de publicación | permiso de administración, servicio de túnel, sincronización de usuario para la granja de servidores de publicación |

### Función Administrador de habilitación de la comunidad {#community-enablement-manager-role}

La capacidad de un visitante del sitio para registrarse por sí mismo generalmente no está permitida para una comunidad [de](overview.md#enablement-community) habilitación, ya que hay costos asociados con cada miembro. Los alumnos y recursos de habilitación son administrados por un usuario al que se le asigna la [función](#author-group-roles) de `enablement manager` durante la creación [del sitio al autor (agregado como miembro del grupo](sites-console.md#enablement) `Community <site-name> Siteenablementmanagers`). El `enablement manager` es también responsable de [asignar recursos](resources.md) de aprendizaje a los miembros de la comunidad que son autores.

Solo los usuarios que sean miembros del `Community Enablement Managers` grupo global pueden seleccionarse como `enablement manager` para un sitio de comunidad específico.

Para crear un usuario al que se le pueda asignar la función de `Community Site Enablement Manager`, utilice la consola de seguridad de la IU clásica para especificar la ruta:

En una instancia de autor:

1. Iniciado con privilegios de administrador, vaya a la consola de seguridad clásica de la interfaz de usuario.
Por ejemplo, [http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. En el menú Editar, seleccione **[!UICONTROL Crear usuario]**.
3. Complete el cuadro de `Create User` diálogo.
   * La ruta debe ser `/home/users/community`
4. Seleccione **[!UICONTROL Crear]**

![chlimage_1-130](assets/chlimage_1-130.png)

* En el panel izquierdo, busque el usuario recién creado y seleccione mostrar en el panel derecho.

![chlimage_1-135](assets/chlimage_1-131.png)

En el panel izquierdo:

1. Borre el cuadro de búsqueda y seleccione **[!UICONTROL Ocultar usuarios]**
2. Localice y arrastre `community-enablementmanagers` a la ficha **[!UICONTROL Grupos]** del nuevo usuario que se muestra en el panel derecho

![chlimage_1-132](assets/chlimage_1-132.png)

### Función de administrador de comunidad {#community-administrators-role}

Como se indica en el gráfico Funciones [de grupo de](#author-group-roles) autores, los miembros del grupo Administradores de la comunidad pueden crear sitios de la comunidad, administrar sitios, administrar miembros (pueden prohibir miembros de la comunidad) y moderar contenido.

Siga los mismos pasos que para crear y asignar un usuario a la función de administrador [de](#communitysiteenablementmanagerrole)habilitación, pero agregue c `ommunity-administrators` group en la ficha Grupos del usuario.

### Integración de LDAP {#ldap-integration}

AEM admite el uso de LDAP para la autenticación de usuarios, así como la creación de cuentas de usuario. Esto se detalla en [Configuración de LDAP con AEM 6](../../help/sites-administering/ldap-config.md).

A continuación se proporcionan algunos detalles de configuración específicos para miembros de la comunidad y grupos de miembros.

1. Configurar LDAP para cada instancia de publicación de AEM
2. [Proveedor de identidad LDAP](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * No hay instrucciones especiales

3. [Controlador de sincronización](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * Establezca las siguientes propiedades:

      * **[!UICONTROL Pertenencia]** automática del usuario: `community-<site name>-<uid>-members`
      * **[!UICONTROL Prefijo]** de ruta de usuario: `/community`
      * **[!UICONTROL Prefijo]** de ruta de grupo: `/community`

4. [Módulo de inicio de sesión externo](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * sin instrucciones especiales

Esto hace que los usuarios se asignen automáticamente al grupo de miembros del sitio de la comunidad y que la ubicación del repositorio sea `/home/users/community` y `/home/groups/community`, de modo que hereden los permisos adecuados para ver el perfil de los demás.

* El `User auto membership` valor debe ser la `rep:authorizableId` propiedad, no el `givenName` (nombre para mostrar) del perfil.

## Sincronización de usuarios entre instancias de AEM {#synchronizing-users-among-aem-instances}

Al utilizar un conjunto de servidores [de](topologies.md)publicación, asegúrese de que los usuarios tienen la misma ruta en cada instancia de publicación importando primero los usuarios a una instancia y [habilitando la sincronización](sync.md) de usuarios en Sling para distribuir los usuarios a las demás instancias de publicación.

Si importa grupos de usuarios, para asegurarse de que los grupos de usuarios tienen la misma ruta en cada instancia de publicación, importe a una instancia y, a continuación, [cree un paquete](../../help/sites-administering/package-manager.md#creating-a-new-package) para exportar e instale dicho paquete en todas las demás instancias de publicación.

Aunque la sincronización de grupos de usuarios mediante la sincronización de usuarios se incluirá en una versión futura, actualmente solo se sincronizará la *pertenencia *de un grupo de usuarios cuando se ejecute la sincronización de usuarios.

## Acerca de los grupos de la comunidad {#about-community-groups}

Al discutir grupos, hay dos temas diferentes:

* **[Los grupos](overview.md#communitygroups)**comunitarios son las subcomunidades que pueden crearse en el entorno de publicación para un sitio comunitario que apoya la creación de grupos comunitarios. La creación de un grupo de comunidad resulta en más páginas agregadas al sitio web y administradas de manera similar al sitio de la comunidad principal. Para obtener más información, visite[Community Group Essentials](essentials-groups.md)para desarrolladores y[Community Group](creating-groups.md)para autores.

* **[Grupos](../../help/sites-administering/security.md)**de miembros Los grupos de miembros son los grupos a los que pueden pertenecer los miembros y que se administran a través de la consola Grupos. Gran parte del debate en esta página se ha dedicado a grupos de miembros. Los grupos de miembros creados automáticamente para un sitio de la comunidad, con el prefijo *`Community`*, pueden ser referidos como un grupo de la comunidad, por lo que debe considerarse el contexto del debate.
