---
title: Experiencia del sitio publicado
seo-title: Experience the Published Site
description: Buscar un sitio publicado
seo-description: Browse to a published site
uuid: 44594e9e-27ad-475d-953d-3611b04f0df8
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: dd0cbc05-a361-46bc-b9f1-d045f8f23890
docset: aem65
exl-id: ebc4e1e7-34f0-4f4e-9f00-178dfda23ce4
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 1%

---

# Experiencia del sitio publicado {#experience-the-published-site}

## Buscar nuevo sitio en la publicación {#browse-to-new-site-on-publish}

Ahora que se ha publicado el sitio de comunidades recién creado, vaya a la URL mostrada al crear el sitio, pero en el servidor de publicación, por ejemplo:

* URL de autor = https://localhost:4502/content/sites/engage/en.html
* URL de publicación = https://localhost:4503/content/sites/engage/en.html

Para minimizar la confusión sobre qué miembro ha iniciado sesión en el autor y en la publicación, se recomienda utilizar distintos navegadores para cada instancia.

Al llegar por primera vez al sitio publicado, el visitante del sitio no suele haber iniciado sesión y sería anónimo.

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![autorpublicado](assets/authorpublished.png)

## Visitante anónimo del sitio {#anonymous-site-visitor}

Un visitante anónimo del sitio ve lo siguiente en la interfaz de usuario:

* Título del sitio (tutorial de introducción)
* Sin vínculo de perfil
* Ningún vínculo de mensajes
* Ningún vínculo de notificaciones
* Campo de búsqueda
* Vínculo de inicio de sesión
* El banner de la marca
* Vínculos de menú para los componentes incluidos en la plantilla de sitio de referencia.

Si selecciona varios vínculos, verá que están en modo de solo lectura.

### Impedir el acceso anónimo en JCR {#prevent-anonymous-access-on-jcr}

Una limitación conocida expone el contenido del sitio de la comunidad a visitantes anónimos a través del contenido jcr y json , aunque **permitir acceso anónimo** está desactivado para el contenido del sitio. Sin embargo, este comportamiento se puede controlar mediante restricciones de Sling como solución.

Para proteger el contenido del sitio de la comunidad del acceso de usuarios anónimos a través del contenido jcr y json , siga estos pasos:

1. En la instancia de AEM Author, vaya a https:// hostname:port/editor.html/content/site/sitename.html.

   >[!NOTE]
   >
   >No vaya al sitio localizado.

1. Vaya a **Propiedades de página**.

   ![page-properties](assets/page-properties.png)

1. Vaya a **Avanzadas** pestaña .

1. Habilitar **Requisito de autenticación**.

   ![autenticación de sitios](assets/site-authentication.png)

1. Añada la ruta de la página de inicio de sesión. Por ejemplo, **/content/......./GetStarted**.
1. Publique la página.

## Miembro de la comunidad de confianza {#trusted-community-member}

Esta experiencia supone [Aaron McDonald](/help/communities/tutorials.md#demo-users) se le asignaron las funciones de [administrador de la comunidad y moderador](/help/communities/create-site.md#roles). Si no es así, vuelva al entorno de creación a [modificar la configuración del sitio](/help/communities/sites-console.md#modifying-site-properties) y seleccione Aaron McDonald como administrador de la comunidad y moderador.

En la esquina superior derecha, seleccione `Log in`y firme con el nombre de usuario (aaron.mcdonald@mailinator.com) y la contraseña (contraseña). Tenga en cuenta la capacidad de iniciar sesión con credenciales de Twitter o Facebook.

![inicio de sesión](assets/login.png)

Una vez que haya iniciado sesión como miembro de la comunidad registrada, observe los siguientes elementos de menú para hacer clic y explorar su sitio de la comunidad:

* **Perfil** permite ver y editar el perfil.
* [Mensajes](/help/communities/configure-messaging.md) le dirige a la sección de mensajería directa, donde puede:

   1. Vea los mensajes directos recibidos (Bandeja de entrada), enviados (Elementos enviados) y eliminados (Papelera).
   1. Componga nuevos mensajes directos para enviarlos a personas y grupos.

* [Notificaciones](/help/communities/notifications.md) le dirige a la sección de notificaciones, donde puede ver los eventos de interés y editar la configuración de las notificaciones.
* [Administración](/help/communities/published-site.md#moderationlink) le dirige a la página de moderación de AEM Communities si tiene privilegios de moderación.

![adminscreen](assets/adminscreen.png)

Observe que la página de calendario es la página principal porque la plantilla de sitio de referencia elegida incluyó primero la función de calendario, seguida de la función de flujo de actividad, la función de foro, etc. Esta estructura se puede ver en la sección [Plantilla del sitio](/help/communities/sites.md#edit-site-template) o al modificar las propiedades del sitio en el entorno de creación:

![sitetemplate](assets/sitetemplate.png)

>[!NOTE]
>
>Para obtener más información sobre los componentes y funciones de Communities, visite:
>
>* [Componentes de Communities](/help/communities/author-communities.md) (para autores)
>* [Componentes, funciones y características esenciales](/help/communities/essentials.md) (para desarrolladores)


### Vínculo del foro {#forum-link}

Para ver la función básica del foro, seleccione el vínculo Foro .

Los miembros pueden publicar un tema nuevo o seguir un tema.

Los visitantes del sitio pueden ver las publicaciones y ordenarlas de diversas maneras.

![forumlink](assets/forumlink.png)

### Vínculo de grupos {#groups-link}

Dado que Aaron es administrador de grupos, la selección del vínculo Grupos permitirá a Aaron crear un nuevo grupo de comunidades seleccionando una plantilla de grupo, una imagen, si el grupo es abierto o secreto, e invitando a los miembros.

Este es un ejemplo de cómo se crea un grupo en el entorno de publicación.

Los grupos también se pueden crear en el entorno de creación y administrar dentro del sitio de la comunidad en el entorno de creación ([Consola de grupos de la comunidad](/help/communities/groups.md)). La experiencia de [creación de grupos en author](/help/communities/nested-groups.md) es siguiente en este tutorial.

![grouplink](assets/grouplink.png)

Crear un grupo de referencia:

1. Select **Nuevo grupo**
1. **Ficha Configuración**

   * Nombre del grupo : `Sports`
   * Descripción : `A parent group for various sporting groups`.
   * Nombre de URL del grupo : `sports`
   * Select `Open Group` (permitir que cualquier miembro de la comunidad participe mediante la unión)

1. **Ficha Plantilla**

   * Select `Reference Group` (contiene una función de grupos en su estructura para permitir grupos anidados)

1. Select **Crear grupo**

   ![creategroup](assets/creategroup.png)

Una vez creado el nuevo grupo, **seleccione el nuevo grupo Deportes** para crear dos grupos (anidados) dentro de él. Como la estructura de un sitio no puede comenzar con la función de grupos, después de abrir el grupo Deportes, es necesario seleccionar el vínculo Grupos :

![grouplink1](assets/grouplink1.png)

El segundo conjunto de vínculos, comenzando por `Blog`, pertenezcan al grupo seleccionado actualmente, la variable `Sports` grupo. Seleccionando los deportes&#39; `Groups` , es posible anidar dos grupos dentro del grupo de deportes.

Como ejemplo, agregue dos `new groups`.

* Un nombre `Baseball`

   * Deje establecido como `Open Group` (pertenencia obligatoria).
   * En la ficha Plantillas, seleccione `Conversational Group`.

* Un nombre `Gymnastics`

   * Cambie su configuración a `Member Only Group` (membresía restringida).
   * En la ficha Plantillas, seleccione `Conversational Group`.

**Aviso**:

* Puede que sea necesario actualizar la página antes de que se muestren ambos grupos.
* Esta plantilla sí *not* incluya la función groups , por lo que no será posible anidar grupos más.
* Al autor, la variable [Consola Grupos](/help/communities/groups.md) ofrece una tercera opción: `Public Group` (pertenencia opcional).

Una vez creados ambos grupos, seleccione el grupo de béisbol, un grupo abierto y observe sus enlaces:

`Discussions` `What's New` `Members`

Los vínculos del grupo se muestran debajo de los vínculos del sitio principal y los resultados se muestran de la siguiente manera:

![grouplink2](assets/grouplink2.png)

En el autor: con privilegios administrativos, vaya a la [Consola Grupos de comunidades](/help/communities/members.md) y agregue Weston McCall a la `Community Engage Gymnastics <uid> Members` grupo.

Continuando con la publicación, cierre la sesión como Aaron McDonald y vea los grupos en el grupo de deportes como un visitante anónimo del sitio:

* Desde la página de inicio
* Select `Groups` vínculo
* Select `Sports` vínculo
* Seleccione Sports&#39; `Groups` vínculo

Sólo el grupo de béisbol será visible.

Inicie sesión como Weston McCall (weston.mccall@dodgit.com / password) y navegue a la misma ubicación. Observe que Weston puede `Join` abrir `Baseball` grupo y `enter or Leave` privado `Gymnastics` grupo.

![grouplink3](assets/grouplink3.png)

### Vínculo de página web {#web-page-link}

Para ver la página web básica incluida en el sitio, seleccione el vínculo Página web . Las herramientas AEM de creación estándar se pueden utilizar para añadir contenido a esta página en el entorno de creación.

Por ejemplo, vaya a **author** , abra el `engage` en la carpeta [Consola Sitios de Communities](/help/communities/sites-console.md), seleccione **Abrir sitio** para entrar al modo de edición de autor. A continuación, seleccione el modo de vista previa para seleccionar la variable `Web Page` vínculo y, a continuación, seleccione el modo de edición para añadir los componentes Título y Texto . Por último, vuelva a publicar solo la página o todo el sitio.

![webpagelink](assets/webpagelink.png)

### Vínculo de moderación {#moderationlink}

Cuando el miembro de la comunidad tiene privilegios de moderación, el vínculo Moderación será visible y, al seleccionarlo, se mostrará el contenido de la comunidad publicado y se permitirá que [moderado](/help/communities/moderate-ugc.md) de forma similar a la [consola de moderación](/help/communities/moderation.md) en el entorno de creación.

Utilice el botón Atrás del explorador para volver al sitio publicado. No se puede acceder a la mayoría de las consolas desde la navegación global en el entorno de publicación.

![moderationlink](assets/moderationlink.png)

## Autoregistro {#self-registration}

Después de cerrar la sesión, es posible crear un nuevo registro de usuario.

* Seleccione `Log In`
* Seleccione `Sign up for a new account`

![registro](assets/registration.png)

![signup](assets/signup.png)

De forma predeterminada, la dirección de correo electrónico es el identificador de inicio de sesión. Si no está marcada, el visitante puede introducir su propio ID de inicio de sesión (nombre de usuario). El nombre de usuario debe ser único en el entorno de publicación.

Después de especificar el nombre, el correo electrónico y la contraseña del usuario, seleccione `Sign Up` creará el usuario y le permitirá firmarlo.

Una vez que haya iniciado sesión, la primera página presentada será su `Profile` , que pueden personalizar.

![El perfil.](assets/profile.png)

Si el miembro olvida su id de inicio de sesión, es posible recuperar si utiliza su dirección de correo electrónico.

![olvigotusername](assets/forgotusername.png)
