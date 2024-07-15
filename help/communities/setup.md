---
title: Configuración inicial
description: Obtenga información sobre cómo configurar inicialmente Adobe Experience Manager Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 2%

---

# Configuración inicial {#initial-setup}

## Iniciar instancias de autor y Publish {#start-author-and-publish-instances}

Para fines de desarrollo y demostración, es necesario ejecutar una instancia de autor y otra de publicación.

Para ello, siga las instrucciones básicas de Adobe Experience Manager AEM () [Introducción](../../help/sites-deploying/deploy.md#getting-started), que resultan en lo siguiente:

* Entorno de creación en [localhost:4502](http://localhost:4502/)
* Entorno Publish en [localhost:4503](http://localhost:4503/)

Para AEM Communities,

* El entorno de creación es para:

   * Desarrollo de sitios, plantillas y componentes.
   * Tareas administrativas y de configuración.

* El entorno de Publish es para:

   * La experiencia de la comunidad al publicar y moderar contenido.
   * Creación de grupos comunitarios, miembros y grupos de miembros.

>[!NOTE]
>
>AEM Si no está familiarizado con el uso de las páginas, vea la documentación sobre [manejo básico](../../help/sites-authoring/basic-handling.md) y una [guía rápida para crear páginas](../../help/sites-authoring/qg-page-authoring.md).

## Instalar la última versión de Communities {#install-latest-communities-release}

Este tutorial crea un [sitio de la comunidad de participación](overview.md#engagement-community) y se basa en la versión 1.10 del paquete de funciones de AEM Communities 6.2.

Para asegurarse de que está instalado el paquete de funciones más reciente, visite:

* [Últimas versiones](deploy-communities.md#latest-releases)

## Configurar Analytics {#configure-analytics}

Cuando [Adobe Analytics está configurado para el sitio de la comunidad](analytics.md), hay disponible información sobre la actividad de la comunidad que mejora la experiencia del miembro de la comunidad y proporciona comentarios a los administradores del sitio.

La integración con Adobe Analytics es opcional.

## Configurar correo electrónico para notificaciones {#configure-email-for-notifications}

La característica de notificaciones, disponible de forma predeterminada para todos los sitios creados con la consola `Communities Sites`, proporciona un canal de correo electrónico para las notificaciones.

Lo que es necesario es que el correo electrónico se configure correctamente para el sitio.

Consulte [Configuración del correo electrónico](email.md).

## Activación del servicio de túnel {#enable-the-tunnel-service}

Al crear un sitio de comunidad en el entorno de creación, el servicio de túnel permite asignar funciones a miembros de comunidad de confianza registrados en el entorno de Publish. El servicio de túnel también permite el acceso a los miembros de la comunidad desde las consolas [Miembros y grupos](members.md) en el entorno de creación.

La convención es para que los miembros y grupos de miembros creados en el entorno de Publish *no* se vuelvan a crear en el entorno de creación. Para obtener más información, consulte [Administración de usuarios y grupos de usuarios](users.md).

Para obtener instrucciones sencillas sobre cómo habilitar el servicio de túnel en una instancia de **Author**, consulte [Servicio de túnel](deploy-communities.md#tunnel-service-on-author).

## Función de administrador de comunidad {#community-administrator-role}

Los miembros del grupo Administradores de la comunidad pueden crear sitios de la comunidad, administrar sitios, administrar miembros (pueden prohibir miembros de la comunidad) y moderar contenido.

### Crear usuario {#create-user}

Cree un usuario en *author*, a quien se le asigna la función de administrador de la comunidad:

* En la instancia de autor

   * Por ejemplo, [http://localhost:4502/](http://localhost:4503/)

* Iniciar sesión con privilegios de administrador

   * Por ejemplo, nombre de usuario &#39;admin&#39; / contraseña &#39;admin&#39;

* Desde la consola principal, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.
* En el menú **Editar**, seleccione **[!UICONTROL Agregar usuario]**

* En el cuadro de diálogo `Create New User` escriba:

   * **[!UICONTROL ID]**: sirius
   * **[!UICONTROL Dirección de correo electrónico]**: sirius.nilson@mailinator.com
   * **[!UICONTROL Contraseña]**: password
   * **[!UICONTROL Confirmar contraseña&amp;ast;]**: contraseña
   * **[!UICONTROL Nombre]**: Sirius
   * **[!UICONTROL Apellido]**: Nilson

### Asignar Sirius al grupo de administradores de la comunidad {#assign-sirius-to-community-administrators-group}

Desplazarse hacia abajo hasta `Add User to Groups`:

* Escriba &quot;C&quot; para buscar

   * Seleccionar `Community Administrators`
   * Seleccionar `Community Enablement Managers`

* Seleccione **[!UICONTROL Guardar]**.

![create-user](assets/create-user.png)

## Habilitar inicio de sesión social {#enable-social-login}

Antes de que se puedan utilizar las versiones de demostración del inicio de sesión social con Facebook y Twitter, es necesario lo siguiente

1. Instale un paquete de correcciones o [último paquete de funciones](deploy-communities.md#latestfeaturepack) (para cambios de la API de Facebook de marzo de 2017).
1. [Habilite el proveedor de OAuth](social-login.md#adobe-granite-oauth-authentication-handler) en el entorno de publicación.

Para los servidores de producción, es necesario crear los servicios en la nube necesarios para proporcionar el inicio de sesión social.

Ver [Inicio de sesión social con Facebook y Twitter](social-login.md).

## Creación de etiquetas de tutorial {#create-tutorial-tags}

Cree etiquetas para poder utilizarlas en los tutoriales de Engage, usando el área de nombres de etiquetas de `Tutorial`.

Use la [consola de etiquetado](../../help/sites-administering/tags.md#tagging-console) para crear las siguientes etiquetas:

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![etiquetas de tutorial](assets/tutorial-tags.png)

A continuación, siga las instrucciones para:

1. [Establezca los permisos de etiquetas](../../help/sites-administering/tags.md#setting-tag-permissions).
1. [Publish usa las etiquetas](../../help/sites-administering/tags.md#publishing-tags).

Paquete de muestra de etiquetas creado para los Tutorials de introducción de AEM Communities

[Obtener archivo](assets/tutorial_tags-v63.zip)

## Almacén común de MongoDB para UGC {#mongodb-for-ugc-common-store}

Se recomienda, pero es opcional, establecer [MSRP](msrp.md) (MongoDB) como [almacén común](working-with-srp.md) para experimentar la flexibilidad de moderar todos los UGC desde entornos de publicación o creación.

Para obtener instrucciones, visite [Cómo configurar MongoDB para la demostración](demo-mongo.md).

AEM De manera predeterminada, la instalación de las instancias de creación y publicación de la publicación hace que el contenido generado por el usuario (UGC) se almacene en [JCR Tar storage](../../help/sites-deploying/platform.md), al que se accede mediante [JSRP](jsrp.md). JSRP no es un almacén común, lo que significa que UGC solo es visible en la instancia en la que se introdujo. Normalmente, el UGC se introduce en una instancia de publicación y no se puede ver en el entorno de creación, por lo que todas las tareas de moderación deben utilizar la instancia de publicación.
