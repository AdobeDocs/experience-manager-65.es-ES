---
title: Experimente el sitio publicado
description: Obtenga información sobre cómo buscar la dirección URL que se muestra al crear un sitio, pero en el servidor de publicación.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: ebc4e1e7-34f0-4f4e-9f00-178dfda23ce4
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 0%

---

# Experimente el sitio publicado {#experience-the-published-site}

## Examinar el nuevo sitio en Publish {#browse-to-new-site-on-publish}

Ahora que se ha publicado el sitio de comunidades recién creado, vaya a la URL que se muestra al crear el sitio, pero en el servidor de publicación, por ejemplo:

* URL del autor = https://localhost:4502/content/sites/engage/en.html
* URL DE PUBLISH = https://localhost:4503/content/sites/engage/en.html

Para minimizar la confusión sobre qué miembro ha iniciado sesión en Autor y Publicación, se recomienda utilizar diferentes exploradores para cada instancia.

Al llegar por primera vez al sitio publicado, el visitante del sitio no suele haber iniciado sesión ya y es anónimo.

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![autorpublicado](assets/authorpublished.png)

## Visitante anónimo del sitio {#anonymous-site-visitor}

Un visitante anónimo del sitio ve lo siguiente en la interfaz de usuario:

* Título del sitio (tutorial de introducción)
* Sin vínculo de perfil
* Sin vínculo de mensajes
* Sin vínculo de notificaciones
* Campo de búsqueda
* Vínculo de inicio de sesión
* El banner de la marca
* Vínculos de menú para los componentes incluidos en la Plantilla del sitio de referencia.

Si selecciona varios vínculos, verá que están en modo de solo lectura.

### Impedir el acceso anónimo en JCR {#prevent-anonymous-access-on-jcr}

Una limitación conocida expone el contenido del sitio de la comunidad a visitantes anónimos a través del contenido jcr y json , aunque **permitir el acceso anónimo** está deshabilitado para el contenido del sitio. Sin embargo, este comportamiento se puede controlar mediante las restricciones de Sling como solución alternativa.

Para proteger el contenido del sitio de su comunidad del acceso de usuarios anónimos a través del contenido jcr y json , siga estos pasos:

1. AEM En la instancia de autor de la, vaya a https:// hostname:port/editor.html/content/site/sitename.html.

   >[!NOTE]
   >
   >No vaya al sitio localizado.

1. Vaya a **Propiedades de página**.

   ![propiedades de página](assets/page-properties.png)

1. Vaya a la ficha **Avanzadas**.

1. Habilitar **requisito de autenticación**.

   ![autenticación de sitio](assets/site-authentication.png)

1. Añada la ruta de la página de inicio de sesión. Por ejemplo, **/content/......./GetStarted**.
1. Publique la página.

## Miembro de comunidad de confianza {#trusted-community-member}

Esta experiencia supone que a [Aaron McDonald](/help/communities/tutorials.md#demo-users) se le asignaron los roles de [administrador y moderador de la comunidad](/help/communities/create-site.md#roles). Si no es así, vuelva al entorno de creación para [modificar la configuración del sitio](/help/communities/sites-console.md#modifying-site-properties) y seleccione a Aaron McDonald como administrador y moderador de la comunidad.

En la esquina superior derecha, seleccione `Log in` e inicie sesión con el nombre de usuario (aaron.mcdonald@mailinator.com) y la contraseña (contraseña). Observe la capacidad de iniciar sesión con credenciales de Twitter o Facebook.

![iniciar sesión](assets/login.png)

Una vez que haya iniciado sesión como miembro registrado de la comunidad, observe los siguientes elementos de menú para hacer clic y explorar el sitio de la comunidad:

* La opción **Perfil** le permite ver y editar su perfil.
* La opción [Mensajes](/help/communities/configure-messaging.md) le dirige a la sección de mensajería directa, donde puede hacer lo siguiente:

   1. Ver los mensajes directos recibidos (Bandeja de entrada), enviados (Elementos enviados) y eliminados (Papelera).
   1. Componga nuevos mensajes directos para que pueda enviarlos a particulares y grupos.

* La opción [Notificaciones](/help/communities/notifications.md) le dirige a la sección de notificaciones, donde puede ver los eventos de interés y editar la configuración de las notificaciones.
* [Administración](/help/communities/published-site.md#moderationlink) le dirige a la página de moderación de AEM Communities, si tiene privilegios de moderación.

![adminscreen](assets/adminscreen.png)

Observe que la página de calendario es la página principal porque la Plantilla de sitio de referencia seleccionada incluía primero la función de calendario, seguida de la función Flujo de actividad, Función de foro, etc. Esta estructura es visible desde la consola [Plantilla del sitio](/help/communities/sites.md#edit-site-template) o al modificar las propiedades del sitio en el entorno de creación:

![plantilla del sitio](assets/sitetemplate.png)

>[!NOTE]
>
>Para obtener más información sobre los componentes y las funciones de las comunidades, visite:
>
>* [Componentes de comunidades](/help/communities/author-communities.md) (para autores)
>* [Componentes, funciones y características esenciales](/help/communities/essentials.md) (para desarrolladores)

### Vínculo de foro {#forum-link}

Vea la función básica de foro seleccionando el vínculo Foro.

Los miembros pueden publicar un nuevo tema o seguir un tema.

Los visitantes del sitio pueden ver las publicaciones y ordenarlas de varias formas.

![vínculo de foro](assets/forumlink.png)

### Vínculo de grupos {#groups-link}

Dado que Aaron es administrador de un grupo, al seleccionar el vínculo Grupos, Aaron puede crear un grupo de comunidad seleccionando una plantilla de grupo, una imagen, si el grupo es abierto o secreto e invitando a miembros.

Este es un ejemplo en el que se crea un grupo en el entorno de publicación.

Los grupos también se pueden crear en el entorno de creación y administrar dentro del sitio de la comunidad en el entorno de creación ([Consola de grupos de la comunidad](/help/communities/groups.md)). La experiencia de [crear grupos en Author](/help/communities/nested-groups.md) es la siguiente en este tutorial.

![vínculo de grupo](assets/grouplink.png)

Crear un grupo de referencia:

1. Seleccionar **nuevo grupo**
1. **Ficha Configuración**

   * Nombre de grupo: `Sports`
   * Descripción: `A parent group for various sporting groups`.
   * Nombre de URL del grupo: `sports`
   * Seleccione `Open Group` (permitir que cualquier miembro de la comunidad participe uniéndose)

1. **Ficha de plantilla**

   * Seleccione `Reference Group` (contiene una función de grupos en su estructura para permitir grupos anidados)

1. Seleccionar **Crear grupo**

   ![creategroup](assets/creategroup.png)

Una vez creado el nuevo grupo, **seleccione el nuevo grupo de deportes** para crear dos grupos (anidados) dentro de él. Como la estructura de un sitio no puede comenzar con la función de grupos, después de abrir el grupo Deportes, es necesario seleccionar el vínculo Grupos:

![grouplink1](assets/grouplink1.png)

El segundo conjunto de vínculos, que comienza por `Blog`, pertenece al grupo seleccionado actualmente, el grupo `Sports`. Al seleccionar el vínculo `Groups` de Sports, es posible anidar dos grupos dentro del grupo Sports.

Por ejemplo, agregue dos `new groups`.

* Uno de nombre `Baseball`

   * Déjelo establecido como `Open Group` (suscripción requerida).
   * En la ficha Plantillas, seleccione `Conversational Group`.

* Uno de nombre `Gymnastics`

   * Cambie su configuración a `Member Only Group` (pertenencia restringida).
   * En la ficha Plantillas, seleccione `Conversational Group`.

**Aviso**:

* Es posible que sea necesario actualizar la página antes de mostrar ambos grupos.
* Esta plantilla *no* incluye la función de grupos, por lo que no es posible anidar más grupos.
* En el autor, la [consola de grupos](/help/communities/groups.md) proporciona una tercera opción: `Public Group` (pertenencia opcional).

Una vez creados ambos grupos, seleccione el grupo de béisbol, un grupo abierto y observe sus vínculos:

`Discussions` `What's New` `Members`

Los vínculos del grupo se muestran debajo de los vínculos del sitio principal y los resultados en la siguiente pantalla:

![grouplink2](assets/grouplink2.png)

En Autor - con privilegios administrativos, vaya a la [Consola de grupos de comunidades](/help/communities/members.md) y agregue Weston McCall al grupo `Community Engage Gymnastics <uid> Members`.

Continuando con la publicación, cierre la sesión de Aaron McDonald y vea los grupos del grupo de deportes como un visitante anónimo del sitio:

* Desde la página de inicio
* Seleccionar vínculo `Groups`
* Seleccionar vínculo `Sports`
* Seleccione el enlace `Groups` de los deportes

Solo el grupo de béisbol es visible.

Inicie sesión como Weston McCall (weston.mccall@dodgit.com / contraseña) y vaya a la misma ubicación. Observe que Weston puede `Join` el grupo `Baseball` abierto y `enter or Leave` el grupo `Gymnastics` privado.

![grouplink3](assets/grouplink3.png)

### Vínculo de página web {#web-page-link}

Ver la página web básica incluida en el sitio seleccionando el vínculo Página web. AEM Las herramientas de creación de contenido estándar se pueden utilizar para añadir contenido a esta página en el entorno de creación.

Por ejemplo, vaya a la instancia **author**, abra la carpeta `engage` en la consola [Communities Sites](/help/communities/sites-console.md), seleccione el icono **Abrir sitio** para entrar en el modo de edición de autor. A continuación, seleccione el modo de vista previa para poder seleccionar el vínculo `Web Page` y, a continuación, seleccione el modo de edición para agregar los componentes Título y Texto. Por último, vuelva a publicar solo la página o todo el sitio.

![webpagelink](assets/webpagelink.png)

### Vínculo de moderación {#moderationlink}

Cuando el miembro de la comunidad tiene privilegios de moderación, se puede ver el vínculo Moderación. Al seleccionar el vínculo, se muestra el contenido de la comunidad que se publica y permite que sea [moderado](/help/communities/moderate-ugc.md) de una manera similar a la [consola de moderación](/help/communities/moderation.md) en el entorno de creación.

Utilice el botón Atrás del explorador para volver al sitio publicado. La mayoría de las consolas no son accesibles desde la navegación global en el entorno de publicación.

![moderationlink](assets/moderationlink.png)

## Registro automático {#self-registration}

Después de cerrar la sesión, es posible crear un registro de usuario.

* Seleccionar `Log In`
* Seleccionar `Sign up for a new account`

![registro](assets/registration.png)

![registro](assets/signup.png)

De forma predeterminada, la dirección de correo electrónico es el ID de inicio de sesión. Si no se selecciona, el visitante puede introducir su propio ID de inicio de sesión (nombre de usuario). El nombre de usuario debe ser único en el entorno de publicación.

Después de especificar el nombre de usuario, el correo electrónico y la contraseña, al seleccionar `Sign Up` se crea el usuario y se le permite firmar.

Después de iniciar sesión, la primera página que se presenta es su página `Profile`, que pueden personalizar.

![perfil](assets/profile.png)

Si el miembro olvida su ID de inicio de sesión, es posible recuperar mediante su dirección de correo electrónico.

![olvidó un nombre de usuario](assets/forgotusername.png)
