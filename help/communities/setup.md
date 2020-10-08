---
title: Configuración inicial
seo-title: Configuración inicial
description: Configuración de comunidades
seo-description: Configuración de comunidades
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 2%

---


# Configuración inicial {#initial-setup}

## Instancias de creación y publicación de inicio {#start-author-and-publish-instances}

Para fines de desarrollo y demostración, será necesario ejecutar un autor y una instancia de publicación.

Para ello, siga las instrucciones básicas de [introducción](../../help/sites-deploying/deploy.md#getting-started) de AEM, que resultarán en:

* Entorno de autor en [localhost:4502](http://localhost:4502/)
* Entorno de publicación en [localhost:4503](http://localhost:4503/)

Para AEM Communities,

* El entorno de autor está a favor de:

   * Desarrollo de sitios, plantillas y componentes.
   * Tareas administrativas y de configuración.

* El entorno de publicación es para:

   * Experiencia de la comunidad de publicar y moderar contenido.
   * Creación de grupos de comunidad, miembros y grupos miembros.

>[!NOTE]
>
>Si no está familiarizado con AEM, vista la documentación sobre el manejo [](../../help/sites-authoring/basic-handling.md) básico y una guía [rápida para la creación de páginas](../../help/sites-authoring/qg-page-authoring.md).

## Instalar la versión más reciente de las comunidades {#install-latest-communities-release}

Este tutorial crea un sitio [de comunidad de](overview.md#engagement-community) participación y se basa en el paquete de funciones de AEM Communities 6.2 versión 1.10.

Para asegurarse de que está instalado el paquete de funciones más reciente, visite:

* [Últimas versiones](deploy-communities.md#latest-releases)

Para ver un tutorial que crea un sitio [de comunidad de](overview.md#enablement-community)habilitación, visite [Introducción a AEM Communities para la habilitación](getting-started-enablement.md).

## Configurar Analytics {#configure-analytics}

Cuando [Adobe Analytics está configurado para el sitio](analytics.md)de la comunidad, se encuentra disponible información sobre la actividad de la comunidad que mejora la experiencia del miembro de la comunidad y también proporciona comentarios a los administradores del sitio.

La integración con Adobe Analytics es opcional.

## Configurar correo electrónico para notificaciones {#configure-email-for-notifications}

La función de notificaciones, disponible de forma predeterminada para todos los sitios creados mediante la `Communities Sites` consola, proporciona un canal de correo electrónico para las notificaciones.

Lo que se necesita es que el correo electrónico se configure correctamente para el sitio.

See [Configuring Email](email.md).

## Habilitar el servicio de túnel {#enable-the-tunnel-service}

Al crear un sitio de comunidad en el entorno de creación, el servicio de túnel permite asignar funciones a miembros de comunidad de confianza registrados en el entorno de publicación. El servicio de túnel también permite el acceso a los miembros de la comunidad desde las consolas [](members.md) Miembros y Grupos en el entorno de creación.

La convención es que los miembros y los grupos miembros creados en el entorno de publicación *no se recreen* en el entorno de creación. Para obtener más información, consulte [Administración de usuarios y grupos](users.md)de usuarios.

Para obtener instrucciones sencillas para habilitar el servicio de túnel en una instancia de **autor** , consulte Servicio [de túnel](deploy-communities.md#tunnel-service-on-author).

## Función de administrador de comunidad {#community-administrator-role}

Los miembros del grupo Administradores de la comunidad pueden crear sitios de la comunidad, administrar sitios, administrar miembros (pueden prohibir miembros de la comunidad) y moderar contenido.

### Crear usuario {#create-user}

Cree un usuario en el *autor*, al que se le asigna la función de administrador de comunidad:

* En la instancia de autor

   * Por ejemplo, [http://localhost:4502/](http://localhost:4503/)

* Iniciar sesión con privilegios de administrador

   * Por ejemplo: nombre de usuario &#39;admin&#39; / contraseña &#39;admin&#39;

* Desde la consola principal, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.
* En el menú **Editar** , seleccione **[!UICONTROL Añadir usuario]**

* En el `Create New User` cuadro de diálogo, introduzca:

   * **[!UICONTROL ID]**: sirius
   * **[!UICONTROL Dirección]** de correo electrónico: sirius.nilson@mailinator.com
   * **[!UICONTROL Contraseña]**: password
   * **[!UICONTROL Confirmar contraseña&amp;Último;]**: password
   * **[!UICONTROL Nombre]**: Sirius
   * **[!UICONTROL Apellido]**: Nilson

### Asignar Sirius al grupo de administradores de la comunidad {#assign-sirius-to-community-administrators-group}

Desplácese hacia abajo hasta `Add User to Groups`:

* Escriba &#39;C&#39; para buscar

   * Seleccione `Community Administrators`
   * Seleccione `Community Enablement Managers`

* Seleccione **[!UICONTROL Guardar]**.

![create-user](assets/create-user.png)

## Habilitar inicio de sesión social {#enable-social-login}

Antes de utilizar las versiones de demostración de inicio de sesión social con Facebook y Twitter, es necesario

1. Instale un paquete de correcciones o un paquete [de funciones](deploy-communities.md#latestfeaturepack) más reciente (para los cambios de la API de Facebook de marzo de 2017).
1. [Habilite el proveedor](social-login.md#adobe-granite-oauth-authentication-handler) de OAuth en el entorno de publicación.

Para los servidores de producción, es necesario crear los servicios de nube necesarios para proporcionar inicio de sesión social.

Consulte Inicio de sesión en [Social con Facebook y Twitter](social-login.md).

## Crear etiquetas de tutoriales {#create-tutorial-tags}

Cree etiquetas para utilizarlas en los tutoriales de participación y activación mediante la Área de nombres de etiquetas de `Tutorial`.

Utilice la consola [Etiquetado](../../help/sites-administering/tags.md#tagging-console) para crear las etiquetas siguientes:

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

A continuación, siga las instrucciones para:

1. [Establezca los permisos](../../help/sites-administering/tags.md#setting-tag-permissions)de etiqueta.
1. [Publique las etiquetas](../../help/sites-administering/tags.md#publishing-tags).

Paquete de muestra de etiquetas creadas para los Tutorials de introducción de AEM Communities

[Obtener archivo](assets/tutorial_tags-v63.zip)

## MongoDB para UGC Common Store {#mongodb-for-ugc-common-store}

Se recomienda, pero es opcional, establecer el [MSRP](msrp.md) (MongoDB) como almacén [](working-with-srp.md) común para experimentar la flexibilidad de moderar todo UGC desde entornos de publicación y/o autor.

Para obtener instrucciones, visite [How to Setup MongoDB for Demo](demo-mongo.md).

De forma predeterminada, la instalación de las instancias de creación y publicación AEM hace que el contenido generado por el usuario (UGC) se almacene en [JCR Tar almacenamiento](../../help/sites-deploying/platform.md) , al que se accede mediante [JSRP](jsrp.md). JSRP no es un almacén común, lo que significa que UGC solo está visible en la instancia en la que se introdujo. Generalmente, UGC se introduce en una instancia de publicación y no estaría visible en el entorno del autor, lo que daría como resultado que todas las tareas de moderación necesitaran utilizar la instancia de publicación.