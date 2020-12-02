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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 1%

---


# Configuración inicial para la habilitación {#initial-setup-for-enablement}

## Instancias de creación y publicación de inicio {#start-author-and-publish-instances}

Para fines de desarrollo y demostración, será necesario ejecutar un autor y una instancia de publicación.

Siga las instrucciones básicas de AEM [Introducción](../../help/sites-deploying/deploy.md#getting-started) que resultarán en

* Entorno de autor en [localhost:4502](http://localhost:4502/)
* Publicar entorno en [localhost:4503](http://localhost:4503/)

Para AEM Communities,

* El entorno de autor está a favor de:

   * Desarrollo de sitios, plantillas, componentes, recursos de habilitación y rutas de aprendizaje.
   * Asignación de miembros y grupos de miembros para habilitar recursos y rutas de aprendizaje.
   * Generación de informes sobre asignaciones, vistas y anuncios.
   * Tareas administrativas y de configuración.

* El entorno de publicación es para:

   * Aprendizaje/formación basado en temas gestionados por el administrador de habilitación.
   * Recursos de habilitación de comentario y clasificación y rutas de aprendizaje.
   * Póngase en contacto con los contactos de recursos.

>[!NOTE]
>
>Si no está familiarizado con AEM, vista la documentación sobre [administración básica](../../help/sites-authoring/basic-handling.md) y una [guía rápida para crear páginas](../../help/sites-authoring/qg-page-authoring.md).

## Instalar la versión de comunidades más recientes {#install-latest-communities-release}

Este tutorial crea un [sitio de comunidad de habilitación](overview.md#enablement-community). Para asegurarse de que está instalado el paquete de funciones más reciente, visite:

* [Últimas versiones](deploy-communities.md#latest-releases)

Para ver un tutorial que crea un [sitio de comunidad de participación](overview.md#engagement-community), visite [Introducción a AEM Communities](getting-started.md).

## Configurar características de habilitación {#configure-enablement-features}

Para seguir este tutorial, es necesario instalar y [configurar correctamente la habilitación](enablement.md), que requiere productos de terceros, como MySQL y FFmpeg.

## Configurar Analytics {#configure-analytics}

Cuando [Adobe Analytics está configurado para el sitio de la comunidad](analytics.md), hay más información disponible en los [informes](reports.md) generados en los recursos de habilitación y las rutas de aprendizaje asignadas a los miembros de la comunidad (alumnos).

## Configurar correo electrónico para notificaciones {#configure-email-for-notifications}

La función de notificaciones, disponible de forma predeterminada para todos los sitios creados con la consola `Communities Sites`, proporciona un canal de correo electrónico para las notificaciones.

Lo que se necesita es que el correo electrónico se configure correctamente para el sitio.

Consulte [Configuración de correo electrónico](email.md).

## Habilitar el servicio de túnel {#enable-the-tunnel-service}

Al crear un sitio de comunidad en el entorno de creación, el servicio de túnel permite crear y administrar usuarios y grupos de usuarios registrados en el entorno de publicación (miembros), asignar funciones a miembros de comunidad de confianza y asignar contenido a los alumnos.

Para obtener más información, consulte [Administración de usuarios y grupos de usuarios](users.md).

Para obtener instrucciones sencillas para habilitar el servicio de túnel, consulte [Servicio de túnel](deploy-communities.md#tunnel-service-on-author).

## Crear etiquetas de tutorial {#create-tutorial-tags}

Cree etiquetas para utilizarlas en los tutoriales de participación y activación, con la Área de nombres de etiquetas `Tutorial`.

Utilice la [consola de etiquetado](../../help/sites-administering/tags.md#tagging-console) para crear las etiquetas siguientes:

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

A continuación, siga las instrucciones para:

1. [Definir los permisos de etiqueta](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [Publicación de las etiquetas](../../help/sites-administering/tags.md#publishing-tags)

Paquete de muestra de etiquetas creadas para los Tutorials de introducción de AEM Communities

[Obtener archivo](assets/communities_tutorialtags-10.zip)

## Crear miembros y grupos de habilitación {#create-enablement-members-and-groups}

Para un sitio de comunidad de habilitación, los visitantes del sitio no deben ser capaces de [registrarse automáticamente ni utilizar el inicio de sesión social](sites-console.md#user-management).

En su lugar, con el [servicio de túnel](#enable-the-tunnel-service) habilitado, la [consola de miembros](members.md) se utiliza para registrar nuevos miembros en el entorno de publicación.

En este tutorial, se crean tres miembros en el entorno de publicación. Dos miembros se convertirán en miembros de un grupo de usuarios asignado a una ruta de aprendizaje, mientras que el tercer miembro se convertirá en un contacto de recursos de habilitación.

Se crea un cuarto usuario en el entorno de creación y se asignan las funciones de Administrador de comunidades y Administrador de habilitación de la comunidad.

>[!NOTE]
>
>Estos miembros se crean antes de la creación del *Tutorial de habilitación* sitio de la comunidad.
>
>Si se crearon posteriormente, podrían agregarse como miembros del grupo de miembros *Tutorial de habilitación* durante la creación de miembros.
>
>Más adelante, se [asignarán al grupo de miembros](enablement-create-site.md#assignuserstocommunityenablemembersgroup).

### Riley Taylor - Participante {#riley-taylor-enrollee}

[Cree un ](members.md#create-new-member) miembro que se agregará a un grupo de Alumnos: el grupo Clase de esquí de la comunidad.

* **ID**: riley
* **Correo electrónico**: riley.taylor@mailinator.com
* **Contraseña**: password
* **Confirmar contraseña**: password
* **Nombre**: Riley
* **Apellido**: Taylor

### Sidney Croft - Alumno {#sidney-croft-enrollee}

[Cree un segundo ](members.md#create-new-member) miembro que se agregará al grupo Community Ski Class.

* **ID**: sidney
* **Correo electrónico**: sidney.croft@mailinator.com
* **Contraseña**: password
* **Confirmar contraseña**: password
* **Nombre**: Sidney
* **Apellido**: Recortar

### Quinn Harper - Moderador y contacto de recursos de habilitación {#quinn-harper-enablement-resource-contact-and-moderator}

[Cree un ](members.md#create-new-member) miembro que se agregará al grupo de miembros del sitio de la comunidad una vez que se haya creado el sitio. Esta pertenencia permitirá que el miembro se asigne como la habilitación [Contacto de recurso](resources.md#settings) cuando se cree un recurso de habilitación para el sitio.

* **ID**: quinn
* **Correo electrónico**: quinn.harper@mailinator.com
* **Contraseña**: password
* **Confirmar contraseña**: password
* **Nombre**: Quinn
* **Apellido**: Harper

### Añadir un grupo de usuarios - Clase de esquí de la comunidad {#add-a-user-group-community-ski-class}

[Añada un nuevo ](members.md#create-new-group) grupo llamado Community Ski Class.

* **ID**: community-ski-class
* **Nombre**: Clase de esquí de comunidad
* **Descripción**: un grupo de muestra para asignar recursos de habilitación
* **Añadir miembros al grupo**  &#39;agregar&#39;:

   * riley
   * sidney

* Seleccione **[!UICONTROL Guardar]**

### Propiedades de la clase de esquí de la comunidad {#community-ski-class-properties}

![ski-class-properties](assets/ski-class-properties.png)

>[!NOTE]
>
>Durante la creación del sitio de la comunidad, los miembros y grupos existentes pueden agregarse al grupo de miembros del sitio de la comunidad.

## Función de administrador de comunidad {#community-administrator-role}

Los miembros del grupo Administradores de la comunidad pueden crear sitios de la comunidad, administrar sitios, administrar miembros (pueden prohibir miembros de la comunidad) y moderar contenido.

### Crear usuario {#create-user}

Cree un usuario en *author*, al que se le asigna la función de administrador de comunidad:

* En la instancia de autor

   * Por ejemplo: [http://localhost:4502/](http://localhost:4503/)

* Iniciar sesión con privilegios de administrador

   * Por ejemplo: nombre de usuario &#39;admin&#39; / contraseña &#39;admin&#39;

* Desde la consola principal, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.
* En el menú **[!UICONTROL Editar]**, seleccione **[!UICONTROL Añadir usuario]**.

* En el cuadro de diálogo `Create New User` escriba:

   * **ID&amp;ast;**: sirius
   * **Dirección** de correo electrónico: sirius.nilson@mailinator.com
   * **Contraseña&amp;ast;**: password
   * **Confirmar contraseña&amp;ast;**: password
   * **Nombre**: Sirius
   * **Apellidos;**: Nilson

### Asignar Sirius al grupo de administradores de la comunidad {#assign-sirius-to-community-administrators-group}

Desplácese hacia abajo hasta `Add User to Groups`:

* Escriba &#39;C&#39; para buscar

   * Seleccione `Community Administrators`
   * Seleccione `Community Enablement Managers`

* Seleccione **[!UICONTROL Guardar]**

![admin-role](assets/admin-role.png)

