---
title: Experimente el sitio publicado
description: Obtenga información sobre cómo buscar la dirección URL que se muestra al crear un sitio, pero en el servidor de publicación.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: ebc4e1e7-34f0-4f4e-9f00-178dfda23ce4
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 1%

---

# Experimente el sitio publicado {#experience-the-published-site}

## Examinar el nuevo sitio al publicar {#browse-to-new-site-on-publish}

Ahora que se ha publicado el sitio de comunidades recién creado, vaya a la URL que se muestra al crear el sitio, pero en el servidor de publicación, por ejemplo:

* URL del autor = https://localhost:4502/content/sites/engage/en.html
* URL de publicación = https://localhost:4503/content/sites/engage/en.html

Para minimizar la confusión sobre qué miembro ha iniciado sesión en Autor y Publicación, se recomienda utilizar diferentes exploradores para cada instancia.

Al llegar por primera vez al sitio publicado, el visitante del sitio no suele haber iniciado sesión ya y es anónimo.

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![publicado por autor](assets/authorpublished.png)

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

Sin embargo, una limitación conocida expone el contenido del sitio de la comunidad a visitantes anónimos a través del contenido jcr y json **permitir acceso anónimo** está deshabilitado para el contenido del sitio. Sin embargo, este comportamiento se puede controlar mediante las restricciones de Sling como solución alternativa.

Para proteger el contenido del sitio de su comunidad del acceso de usuarios anónimos a través del contenido jcr y json , siga estos pasos:

1. AEM En la instancia de autor de la, vaya a https:// hostname:port/editor.html/content/site/sitename.html.

   >[!NOTE]
   >
   >No vaya al sitio localizado.

1. Ir a **Propiedades de página**.

   ![page-properties](assets/page-properties.png)

1. Ir a **Avanzadas** pestaña.

1. Activar **Requisito de autenticación**.

   ![site-authentication](assets/site-authentication.png)

1. Añada la ruta de la página de inicio de sesión. Por ejemplo, **/content/......./GetStarted**.
1. Publique la página.

## Miembro de comunidad de confianza {#trusted-community-member}

Esta experiencia da por hecho [Aaron McDonald](/help/communities/tutorials.md#demo-users) se le asignaron las funciones de [administrador y moderador de la comunidad](/help/communities/create-site.md#roles). Si no es así, vuelva al entorno de creación en [modificar la configuración del sitio](/help/communities/sites-console.md#modifying-site-properties) y seleccione a Aaron McDonald como administrador y moderador de la comunidad.

En la esquina superior derecha, seleccione `Log in`y firme con el nombre de usuario (aaron.mcdonald@mailinator.com) y la contraseña (contraseña). Observe la capacidad de iniciar sesión con credenciales de Twitter o Facebook.

![login](assets/login.png)

Una vez que haya iniciado sesión como miembro registrado de la comunidad, observe los siguientes elementos de menú para hacer clic y explorar el sitio de la comunidad:

* **Perfil** Esta opción le permite ver y editar su perfil.
* [Mensajes](/help/communities/configure-messaging.md) le dirige a la sección mensajería directa, donde puede hacer lo siguiente:

   1. Ver los mensajes directos recibidos (Bandeja de entrada), enviados (Elementos enviados) y eliminados (Papelera).
   1. Componga nuevos mensajes directos para que pueda enviarlos a particulares y grupos.

* [Notificaciones](/help/communities/notifications.md) le dirige a la sección notificaciones, donde puede ver los eventos de interés y editar la configuración de las notificaciones.
* [Administration](/help/communities/published-site.md#moderationlink) le dirige a la página Moderación de AEM Communities, si tiene privilegios de moderación.

![adminscreen](assets/adminscreen.png)

Observe que la página de calendario es la página principal porque la Plantilla de sitio de referencia seleccionada incluía primero la función de calendario, seguida de la función Flujo de actividad, Función de foro, etc. Esta estructura es visible desde el [Plantilla del sitio](/help/communities/sites.md#edit-site-template) o al modificar las propiedades del sitio en el entorno de creación:

![sitetemplate](assets/sitetemplate.png)

>[!NOTE]
>
>Para obtener más información sobre los componentes y las funciones de las comunidades, visite:
>
>* [Componentes de Communities](/help/communities/author-communities.md) (para autores)
>* [Aspectos básicos de componentes, funciones y funciones](/help/communities/essentials.md) (para desarrolladores)

### Vínculo de foro {#forum-link}

Vea la función básica de foro seleccionando el vínculo Foro.

Los miembros pueden publicar un nuevo tema o seguir un tema.

Los visitantes del sitio pueden ver las publicaciones y ordenarlas de varias formas.

![enlace de foro](assets/forumlink.png)

### Vínculo de grupos {#groups-link}

Dado que Aaron es administrador de un grupo, al seleccionar el vínculo Grupos, Aaron puede crear un grupo de comunidad seleccionando una plantilla de grupo, una imagen, si el grupo es abierto o secreto e invitando a miembros.

Este es un ejemplo en el que se crea un grupo en el entorno de publicación.

Los grupos también se pueden crear en el entorno de creación y administrar dentro del sitio de la comunidad en el entorno de creación ([Consola Grupos de la comunidad](/help/communities/groups.md)). La experiencia de [creación de grupos en autor](/help/communities/nested-groups.md) es el siguiente paso en este tutorial.

![grouplink](assets/grouplink.png)

Crear un grupo de referencia:

1. Seleccionar **Nuevo grupo**
1. **Pestaña Configuración**

   * Nombre del grupo : `Sports`
   * Descripción : `A parent group for various sporting groups`.
   * Nombre de URL del grupo : `sports`
   * Seleccionar `Open Group` (permitir que cualquier miembro de la comunidad participe uniéndose)

1. **Pestaña Plantilla**

   * Seleccionar `Reference Group` (contiene una función de grupos en su estructura para permitir grupos anidados)

1. Seleccionar **Crear grupo**

   ![creategroup](assets/creategroup.png)

Una vez creado el nuevo grupo, **seleccione el nuevo grupo Deportes** para crear dos grupos (anidados) dentro de él. Como la estructura de un sitio no puede comenzar con la función de grupos, después de abrir el grupo Deportes, es necesario seleccionar el vínculo Grupos:

![grouplink1](assets/grouplink1.png)

El segundo conjunto de vínculos, que comienza con `Blog`, pertenecen al grupo seleccionado actualmente, el `Sports` grupo. Seleccionando el de Deportes&#39; `Groups` , es posible anidar dos grupos dentro del grupo Deportes.

Por ejemplo, añada dos `new groups`.

* Uno llamado `Baseball`

   * Déjelo establecido como una `Open Group` (abono obligatorio).
   * En la pestaña Plantillas, seleccione `Conversational Group`.

* Uno llamado `Gymnastics`

   * Cambie su configuración a `Member Only Group` (abono restringido).
   * En la pestaña Plantillas, seleccione `Conversational Group`.

**Aviso**:

* Es posible que sea necesario actualizar la página antes de mostrar ambos grupos.
* Esta plantilla sí *no* incluya la función grupos, de modo que no sea posible anidar más grupos.
* En autor, la variable [Consola de grupos](/help/communities/groups.md) proporciona una tercera opción: una `Public Group` (abono opcional).

Una vez creados ambos grupos, seleccione el grupo de béisbol, un grupo abierto y observe sus vínculos:

`Discussions` `What's New` `Members`

Los vínculos del grupo se muestran debajo de los vínculos del sitio principal y los resultados en la siguiente pantalla:

![grouplink2](assets/grouplink2.png)

En Autor: con privilegios administrativos, vaya a [Consola de grupos de Communities](/help/communities/members.md) y agregue Weston McCall al `Community Engage Gymnastics <uid> Members` grupo.

Continuando con la publicación, cierre la sesión de Aaron McDonald y vea los grupos del grupo de deportes como un visitante anónimo del sitio:

* Desde la página de inicio
* Seleccionar `Groups` vincular
* Seleccionar `Sports` vincular
* Seleccione el de deportes `Groups` vincular

Solo el grupo de béisbol es visible.

Inicie sesión como Weston McCall (weston.mccall@dodgit.com / contraseña) y vaya a la misma ubicación. Tenga en cuenta que Weston puede `Join` la apertura `Baseball` grupo y o bien `enter or Leave` el privado `Gymnastics` grupo.

![grouplink3](assets/grouplink3.png)

### Vínculo de página web {#web-page-link}

Ver la página web básica incluida en el sitio seleccionando el vínculo Página web. AEM Las herramientas de creación de contenido estándar se pueden utilizar para añadir contenido a esta página en el entorno de creación.

Por ejemplo, vaya a **autor** , abra el `engage` carpeta en el [Consola Sitios de Communities](/help/communities/sites-console.md), seleccione la **Abrir sitio** para acceder al modo de edición de autor. A continuación, seleccione el modo de vista previa para poder seleccionar el `Web Page` y, a continuación, seleccione el modo de edición para añadir los componentes Título y Texto. Por último, vuelva a publicar solo la página o todo el sitio.

![webpagelink](assets/webpagelink.png)

### Vínculo de moderación {#moderationlink}

Cuando el miembro de la comunidad tiene privilegios de moderación, se puede ver el vínculo Moderación. Al seleccionar el vínculo, se muestra el contenido de la comunidad que se publica y se permite [moderado](/help/communities/moderate-ugc.md) de forma similar a la [consola de moderación](/help/communities/moderation.md) en el entorno de creación.

Utilice el botón Atrás del explorador para volver al sitio publicado. La mayoría de las consolas no son accesibles desde la navegación global en el entorno de publicación.

![moderationlink](assets/moderationlink.png)

## Registro automático {#self-registration}

Después de cerrar la sesión, es posible crear un registro de usuario.

* Seleccione lo siguiente `Log In`
* Seleccione lo siguiente `Sign up for a new account`

![registro](assets/registration.png)

![registro](assets/signup.png)

De forma predeterminada, la dirección de correo electrónico es el ID de inicio de sesión. Si no se selecciona, el visitante puede introducir su propio ID de inicio de sesión (nombre de usuario). El nombre de usuario debe ser único en el entorno de publicación.

Después de especificar el nombre de usuario, el correo electrónico y la contraseña, seleccione `Sign Up` crea el usuario y le permite firmar.

Después de iniciar sesión, la primera página que se presenta es su `Profile` , que pueden personalizar.

![perfil](assets/profile.png)

Si el miembro olvida su ID de inicio de sesión, es posible recuperar mediante su dirección de correo electrónico.

![olvidadnombredeusuario](assets/forgotusername.png)
