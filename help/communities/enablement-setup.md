---
title: Configuración inicial para la habilitación
seo-title: Initial Setup
description: Configuración inicial para la habilitación
seo-description: Initial Setup for Enablement
uuid: 873ec41d-c088-41d9-a535-de5300661de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: f2ac3d66-cc79-498f-83fb-dd96feb88de2
exl-id: ed494922-3e15-4778-84c1-35c8846ce980
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 2%

---

# Configuración inicial para la habilitación  {#initial-setup-for-enablement}

## Iniciar instancias de autor y publicación {#start-author-and-publish-instances}

Para fines de desarrollo y demostración, será necesario ejecutar un autor y una instancia de publicación.

Siga los AEM básicos [Introducción](../../help/sites-deploying/deploy.md#getting-started) instrucciones que resultarán en

* Entorno de creación en [localhost:4502](http://localhost:4502/)
* Publicar entorno en [localhost:4503](http://localhost:4503/)

Para AEM Communities,

* El entorno de creación es para:

   * Desarrollo de sitios, plantillas, componentes, recursos de habilitación y rutas de aprendizaje.
   * Asignación de miembros y grupos de miembros a recursos de habilitación y rutas de aprendizaje.
   * Generación de informes sobre asignaciones, vistas y publicaciones.
   * Tareas administrativas y de configuración.

* El entorno de publicación es para:

   * Aprendizaje/formación basado en temas administrados por el administrador de habilitación.
   * Recursos de habilitación y rutas de aprendizaje de comentarios y clasificación.
   * Contactar con los contactos de recursos.

>[!NOTE]
>
>Si no está familiarizado con AEM, consulte la documentación de [tratamiento básico](../../help/sites-authoring/basic-handling.md) y [guía rápida para la creación de páginas](../../help/sites-authoring/qg-page-authoring.md).

## Instalación de la última versión de Communities {#install-latest-communities-release}

Este tutorial crea un [sitio de la comunidad de habilitación](overview.md#enablement-community). Para asegurarse de que está instalado el paquete de funciones más reciente, visite:

* [Últimas versiones](deploy-communities.md#latest-releases)

Para un tutorial que cree un [sitio de la comunidad de participación](overview.md#engagement-community), visita [Introducción a AEM Communities](getting-started.md).

## Configurar funciones de habilitación {#configure-enablement-features}

Para seguir este tutorial, es necesario instalar correctamente y [configurar habilitación](enablement.md), que requiere productos de terceros, como MySQL y FFmpeg.

## Configurar Analytics {#configure-analytics}

When [Adobe Analytics está configurado para el sitio de la comunidad](analytics.md), encontrará más información en la [informes](reports.md) se genera en recursos de habilitación y rutas de aprendizaje asignadas a miembros de la comunidad (estudiantes).

## Configurar el correo electrónico para las notificaciones {#configure-email-for-notifications}

La función de notificaciones está disponible de forma predeterminada para todos los sitios creados con el `Communities Sites` proporciona un canal de correo electrónico para las notificaciones.

Lo que es necesario es que el correo electrónico esté configurado correctamente para el sitio.

Consulte [Configuración del correo electrónico](email.md).

## Habilitar el servicio de túnel {#enable-the-tunnel-service}

Al crear un sitio de comunidad en el entorno de creación, el servicio de túnel permite crear y administrar usuarios y grupos de usuarios registrados en el entorno de publicación (miembros), asignar funciones a miembros de comunidad de confianza y asignar contenido a los estudiantes.

Para obtener más información, consulte [Administración de usuarios y grupos de usuarios](users.md).

Para obtener instrucciones sencillas para habilitar el servicio de túnel, consulte [Servicio de túnel](deploy-communities.md#tunnel-service-on-author).

## Creación de etiquetas de tutorial {#create-tutorial-tags}

Cree etiquetas para utilizarlas en los tutoriales de interacción y habilitación, utilizando el espacio de nombres de las etiquetas de `Tutorial`.

Utilice la variable [Consola de etiquetado](../../help/sites-administering/tags.md#tagging-console) para crear las etiquetas siguientes:

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutoriales-etiquetas](assets/tutorial-tags.png)

A continuación, siga las instrucciones para:

1. [Definición de los permisos de etiqueta](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [Publicación de las etiquetas](../../help/sites-administering/tags.md#publishing-tags)

Paquete de muestra de etiquetas creadas para los Tutorials de introducción a AEM Communities

[Obtener archivo](assets/communities_tutorialtags-10.zip)

## Crear miembros y grupos de habilitación {#create-enablement-members-and-groups}

Para un sitio de la comunidad de habilitación, los visitantes del sitio no deben poder [registrarse automáticamente y usar inicio de sesión social](sites-console.md#user-management).

En su lugar, con la variable [servicio de túnel](#enable-the-tunnel-service) activada, la variable [Consola Miembros](members.md) se utiliza para registrar nuevos miembros en el entorno de publicación.

En este tutorial, se crean tres miembros en el entorno de publicación. Dos miembros se convertirán en miembros de un grupo de usuarios asignado a una ruta de aprendizaje, mientras que el tercer miembro se convertirá en un contacto de recursos de habilitación.

Se crea un cuarto usuario en el entorno de creación y se asignan las funciones de administrador de comunidades y administrador de habilitación de la comunidad.

>[!NOTE]
>
>Estos miembros se están creando antes de la creación de la variable *Tutorial de habilitación* sitio de la comunidad.
>
>Si se crearon posteriormente, se podrían agregar como miembros del *Grupo de miembros del tutorial de habilitación* durante la creación del miembro.
>
>En su lugar, más tarde, serán [asignado al grupo de miembros](enablement-create-site.md#assignuserstocommunityenablemembersgroup).

### Riley Taylor: inscrito {#riley-taylor-enrollee}

[Crear un miembro](members.md#create-new-member) que se agregarán a un grupo de Alumnos: el grupo de Clase de Esquí Comunitaria.

* **ID**: riley
* **Correo electrónico**: riley.taylor@mailinator.com
* **Contraseña**: password
* **Confirmar contraseña**: password
* **Nombre**: Riley
* **Apellidos**: Taylor

### Sidney Croft - Participante {#sidney-croft-enrollee}

[Crear un segundo miembro](members.md#create-new-member) que se añadirán al grupo Community Ski Class.

* **ID**: sidney
* **Correo electrónico**: sidney.croft@mailinator.com
* **Contraseña**: password
* **Confirmar contraseña**: password
* **Nombre**: Sidney
* **Apellidos**: Recortar

### Quinn Harper - Moderador y contacto del recurso de habilitación {#quinn-harper-enablement-resource-contact-and-moderator}

[Crear un miembro](members.md#create-new-member) que se agregarán al grupo de miembros del sitio de la comunidad una vez que se haya creado el sitio. Esta pertenencia permitirá que el miembro se asigne como la habilitación [Contacto de recurso](resources.md#settings) cuando se crea un recurso de habilitación para el sitio.

* **ID**: quinn
* **Correo electrónico**: quinn.harper@mailinator.com
* **Contraseña**: password
* **Confirmar contraseña**: password
* **Nombre**: Quinn
* **Apellidos**: Muelle

### Agregar un grupo de usuarios: clase de esquí de la comunidad {#add-a-user-group-community-ski-class}

[Agregar un nuevo grupo](members.md#create-new-group) se denomina clase Community Ski.

* **ID**: clase community-ski
* **Nombre**: Clase Community Ski
* **Descripción**: un grupo de muestra para asignar recursos de habilitación
* **Agregar miembros al grupo** &quot;añadir&quot;:

   * riley
   * sidney

* Seleccione **[!UICONTROL Guardar]**

### Propiedades de la clase Community Ski {#community-ski-class-properties}

![ski-class-properties](assets/ski-class-properties.png)

>[!NOTE]
>
>Durante la creación del sitio de la comunidad, los miembros y grupos existentes pueden agregarse al grupo de miembros del sitio de la comunidad.

## Función de administrador de la comunidad {#community-administrator-role}

Los miembros del grupo Administradores de la comunidad pueden crear sitios de la comunidad, administrar sitios, administrar miembros (pueden prohibir a los miembros de la comunidad) y moderar contenido.

### Crear usuario {#create-user}

Crear un usuario en *author*, a quien se asigna la función de administrador de la comunidad:

* En la instancia de autor

   * Por ejemplo, [http://localhost:4502/](http://localhost:4503/)

* Iniciar sesión con privilegios de administrador

   * Por ejemplo, el nombre de usuario &quot;admin&quot;/contraseña &quot;admin&quot;

* Desde la consola principal, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.
* En el **[!UICONTROL Editar]** seleccione **[!UICONTROL Agregar usuario]**.

* En el `Create New User` introduzca el cuadro de diálogo:

   * **ID&amp;ast;**: sirius
   * **Dirección De Correo Electrónico**: sirius.nilson@mailinator.com
   * **Contraseña&amp;ast;**: password
   * **Confirmar contraseña&amp;ast;**: password
   * **Nombre**: Sirius
   * **Apellido&amp;o;**: Nilson

### Asignar Sirius al grupo de administradores de la comunidad {#assign-sirius-to-community-administrators-group}

Desplácese hacia abajo hasta `Add User to Groups`:

* Escriba &quot;C&quot; para buscar

   * Seleccione `Community Administrators`
   * Seleccione `Community Enablement Managers`

* Seleccione **[!UICONTROL Guardar]**

![admin-role](assets/admin-role.png)
