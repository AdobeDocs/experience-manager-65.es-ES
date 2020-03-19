---
title: Configuración inicial para la habilitación
seo-title: Configuración inicial
description: Configuración inicial para la habilitación
seo-description: Configuración inicial para la habilitación
uuid: 873ec41d-c088-41d9-a535-de5300661de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: f2ac3d66-cc79-498f-83fb-dd96feb88de2
translation-type: tm+mt
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# Configuración inicial para la habilitación {#initial-setup-for-enablement}

## Iniciar instancias de creación y publicación {#start-author-and-publish-instances}

Para fines de desarrollo y demostración, será necesario ejecutar un autor y una instancia de publicación.

Siga las instrucciones básicas de [introducción](../../help/sites-deploying/deploy.md#getting-started) de AEM que resultarán en

* Entorno de creación en [localhost:4502](http://localhost:4502/)
* Entorno de publicación en [localhost:4503](http://localhost:4503/)

Para AEM Communities,

* El entorno de creación es para

   * Desarrollo de sitios, plantillas, componentes, recursos de habilitación y rutas de aprendizaje
   * Asignación de miembros y grupos de miembros para habilitar recursos y rutas de aprendizaje
   * Generación de informes sobre asignaciones, vistas y anuncios
   * Tareas administrativas y de configuración

* El entorno de publicación es para

   * Aprendizaje/formación basado en temas administrados por el administrador de habilitación
   * Recursos y rutas de aprendizaje de habilitación de comentario y clasificación
   * Ponerse en contacto con los contactos de recursos

>[!NOTE]
>
>Si no está familiarizado con AEM, consulte la documentación sobre la gestión [](../../help/sites-authoring/basic-handling.md) básica y una guía [rápida para crear páginas](../../help/sites-authoring/qg-page-authoring.md).

## Instalar la versión más reciente de las comunidades {#install-latest-communities-release}

Este tutorial crea un sitio [de comunidad de](overview.md#enablement-community)habilitación. Para asegurarse de que está instalado el paquete de funciones más reciente, visite:

* [Últimas versiones](deploy-communities.md#latest-releases)

Para ver un tutorial que crea un sitio [de comunidad de](overview.md#engagement-community)participación, visite [Introducción a las comunidades](getting-started.md)de AEM.

## Configurar funciones de habilitación {#configure-enablement-features}

Para seguir este tutorial, es necesario instalar y [configurar correctamente la habilitación](enablement.md), que requiere productos de terceros, como MySQL y FFmpeg.

## Configurar Analytics {#configure-analytics}

Cuando [Adobe Analytics está configurado para el sitio](analytics.md)de la comunidad, hay más información disponible en los [informes](reports.md) generados sobre los recursos de habilitación y las rutas de aprendizaje asignadas a los miembros de la comunidad (alumnos).

## Configurar correo electrónico para notificaciones {#configure-email-for-notifications}

La función de notificaciones, disponible de forma predeterminada para todos los sitios creados con la `Communities Sites` consola, proporciona un canal de correo electrónico para las notificaciones.

Lo que se necesita es que el correo electrónico se configure correctamente para el sitio.

See [Configuring Email](email.md).

## Habilitar el servicio de túnel {#enable-the-tunnel-service}

Al crear un sitio de comunidad en el entorno de creación, el servicio de túnel permite crear y administrar usuarios y grupos de usuarios registrados en el entorno de publicación (miembros), asignar funciones a miembros de comunidad de confianza y asignar contenido a los alumnos.

Para obtener más información, consulte [Administración de usuarios y grupos](users.md)de usuarios.

Para obtener instrucciones sencillas para habilitar el servicio de túnel, consulte Servicio [de túnel](deploy-communities.md#tunnel-service-on-author).

## Crear etiquetas de tutoriales {#create-tutorial-tags}

Cree etiquetas para utilizarlas en los tutoriales de participación y activación, utilizando el espacio de nombres de etiquetas de `Tutorial`.

Utilice la consola [Etiquetado](../../help/sites-administering/tags.md#tagging-console) para crear las etiquetas siguientes:

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![chlimage_1-417](assets/chlimage_1-417.png)

Siga las instrucciones para

1. [Definir los permisos de etiqueta](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [Publicación de las etiquetas](../../help/sites-administering/tags.md#publishing-tags)

Paquete de muestra de etiquetas creadas para los tutoriales de introducción de AEM Communities

[Obtener archivo](assets/communities_tutorialtags-10.zip)

## Crear miembros y grupos de habilitación {#create-enablement-members-and-groups}

Para un sitio de comunidad de habilitación, los visitantes del sitio no deben poder [registrarse ni utilizar el inicio de sesión](sites-console.md#user-management)social.

En su lugar, con el servicio [de](#enable-the-tunnel-service) túnel habilitado, se utiliza la consola [](members.md) Miembros para registrar nuevos miembros en el entorno de publicación.

En este tutorial, se crean tres miembros en el entorno de publicación. Dos miembros se convertirán en miembros de un grupo de usuarios asignado a una ruta de aprendizaje, mientras que el tercer miembro se convertirá en un contacto de recursos de habilitación.

Se crea un cuarto usuario en el entorno de creación y se asignan las funciones Administrador de comunidades y Administrador de habilitación de la comunidad.

>[!NOTE]
>
>Estos miembros se están creando antes de la creación del sitio de la comunidad Tutorial *de* habilitación.
>
>Si se crearon posteriormente, podrían agregarse como miembros del grupo *de miembros del Tutorial de* habilitación durante la creación de miembros.
>
>Más adelante, se [asignarán al grupo](enablement-create-site.md#assignuserstocommunityenablemembersgroup)de miembros.

### Riley Taylor - Participante {#riley-taylor-enrollee}

[Cree un miembro](members.md#create-new-member) que se agregará a un grupo de alumnos: el grupo Clase de esquí de la comunidad.

* **ID**: riley
* **Correo electrónico**: riley.taylor@mailinator.com
* **Contraseña**: password
* **Confirmar contraseña**: password
* **Nombre**: Riley
* **Apellido**: Taylor

### Sidney Croft - Alumno {#sidney-croft-enrollee}

[Cree un segundo miembro](members.md#create-new-member) que se agregará al grupo Community Ski Class.

* **ID**: sidney
* **Correo electrónico**: sidney.croft@mailinator.com
* **Contraseña**: password
* **Confirmar contraseña**: password
* **Nombre**: Sidney
* **Apellido**: Recortar

### Quinn Harper - Moderador y contacto de recursos de habilitación {#quinn-harper-enablement-resource-contact-and-moderator}

[Cree un miembro](members.md#create-new-member) que se agregará al grupo de miembros del sitio de la comunidad una vez que se haya creado el sitio. Esta pertenencia permitirá que el miembro se asigne como contacto [de](resources.md#settings) recursos de habilitación cuando se cree un recurso de habilitación para el sitio.

* **ID**: quinn
* **Correo electrónico**: quinn.harper@mailinator.com
* **Contraseña**: password
* **Confirmar contraseña**: password
* **Nombre**: Quinn
* **Apellido**: Harper

### Agregar un grupo de usuarios: Clase de esquí de la comunidad {#add-a-user-group-community-ski-class}

[Agregue un nuevo grupo](members.md#create-new-group) denominado Community Ski Class.

* **ID**: community-ski-class
* **Nombre**: Clase de esquí de comunidad
* **Descripción**: un grupo de muestra para asignar recursos de habilitación
* **Agregar miembros al grupo** &#39;agregar&#39;:

   * riley
   * sidney

* Seleccione **[!UICONTROL Guardar]**

### Propiedades de la clase de esquí de la comunidad {#community-ski-class-properties}

![chlimage_1-418](assets/chlimage_1-418.png)

>[!NOTE]
>
>Durante la creación del sitio de la comunidad, los miembros y grupos existentes pueden agregarse al grupo de miembros del sitio de la comunidad.

## Función de administrador de comunidad {#community-administrator-role}

Los miembros del grupo Administradores de la comunidad pueden crear sitios de la comunidad, administrar sitios, administrar miembros (pueden prohibir miembros de la comunidad) y moderar contenido.

### Crear usuario {#create-user}

Cree un usuario en el *autor*, al que se le asigna la función de administrador de comunidad:

* En la instancia de creación

   * Por ejemplo, [http://localhost:4502/](http://localhost:4503/)

* Iniciar sesión con privilegios de administrador

   * Por ejemplo: nombre de usuario &#39;admin&#39; / contraseña &#39;admin&#39;

* Desde la consola principal, vaya a **[!UICONTROL Herramientas, Operaciones > Seguridad > Usuarios]**
* En el menú **[!UICONTROL Editar]** , seleccione **[!UICONTROL Agregar usuario]**

* En el cuadro de diálogo `Create New User` , introduzca

   * **ID&amp;Último;**: sirius
   * **Dirección** de correo electrónico: sirius.nilson@mailinator.com
   * **Contraseña&amp;Último;**: password
   * **Confirmar contraseña&amp;Último;**: password
   * **Nombre**: Sirius
   * **Apellido&amp;ma;Último;**: Nilson

### Asignar Sirius al grupo de administradores de la comunidad {#assign-sirius-to-community-administrators-group}

Desplácese hacia abajo hasta `Add User to Groups`:

* Escriba &#39;C&#39; para buscar

   * Seleccione `Community Administrators`
   * Seleccione `Community Enablement Managers`

* Seleccione **[!UICONTROL Guardar]**

![chlimage_1-419](assets/chlimage_1-419.png)

