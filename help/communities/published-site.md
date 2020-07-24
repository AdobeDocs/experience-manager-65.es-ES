---
title: Experimente el sitio publicado
seo-title: Experimente el sitio publicado
description: Explorar un sitio publicado
seo-description: Explorar un sitio publicado
uuid: 44594e9e-27ad-475d-953d-3611b04f0df8
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: dd0cbc05-a361-46bc-b9f1-d045f8f23890
docset: aem65
translation-type: tm+mt
source-git-commit: 65e2b98cfd980f17302b4751127e25827decec22
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 0%

---


# Experimente el sitio publicado {#experience-the-published-site}

## Ir a un nuevo sitio al publicar {#browse-to-new-site-on-publish}

Ahora que se ha publicado el sitio de comunidades recién creado, busque la dirección URL que se muestra al crear el sitio, pero en el servidor de publicación, por ejemplo:

* URL del autor = https://localhost:4502/content/sites/engage/en.html
* URL de publicación = https://localhost:4503/content/sites/engage/en.html

Para minimizar la confusión sobre qué miembro ha iniciado sesión en el autor y la publicación, se recomienda utilizar distintos navegadores para cada instancia.

Al llegar por primera vez al sitio publicado, el visitante del sitio no suele haber iniciado sesión y sería anónimo.

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![chlimage_1-31](assets/chlimage_1-31.png)

## Visitante de sitio anónimo {#anonymous-site-visitor}

Un visitante de sitio anónimo ve lo siguiente en la interfaz de usuario:

* Título del sitio (Tutorial de introducción)
* Sin vínculo de perfil
* Ningún vínculo de mensajes
* Ningún vínculo de notificaciones
* Campo de búsqueda
* Vínculo de inicio de sesión
* La pancarta de la marca
* Vínculos de menú para los componentes incluidos en la plantilla de sitio de referencia.

Si selecciona varios vínculos, encontrará que están en modo de solo lectura.

### Impedir el acceso anónimo a JCR {#prevent-anonymous-access-on-jcr}

Una limitación conocida expone el contenido del sitio de la comunidad a visitantes anónimos a través del contenido jcr y json, aunque **permitir el acceso** anónimo está deshabilitado para el contenido del sitio. Sin embargo, este comportamiento se puede controlar mediante restricciones de Sling como solución alternativa.

Para proteger el contenido del sitio de la comunidad del acceso de usuarios anónimos a través del contenido jcr y json, siga estos pasos:

1. En la instancia de AEM Author, vaya a https:// hostname:port/editor.html/content/site/sitename.html.

   >[!NOTE]
   >
   >No vaya al sitio localizado.

1. Vaya a Propiedades **de la página**.

   ![site-authentication](assets/site-authentication.png)

1. Vaya a la ficha **Avanzado** .

   ![page-properties](assets/page-properties.png)

1. Enable **Authentication Requirement**.
1. Añada la ruta de la página de inicio de sesión. Por ejemplo, **/content/......./GetStarted**.
1. Publique la página.

## Miembro de la comunidad de confianza {#trusted-community-member}

Esta experiencia supone que a [Aaron McDonald](/help/communities/tutorials.md#demo-users) se le asignaron las funciones de administrador de [comunidad y moderador](/help/communities/create-site.md#roles). Si no es así, vuelva al entorno de creación para [modificar la configuración](/help/communities/sites-console.md#modifying-site-properties) del sitio y seleccione Aaron McDonald como administrador de comunidad y moderador.

En la esquina superior derecha, seleccione `Log in`y firme con el nombre de usuario (aaron.mcdonald@mailinator.com) y la contraseña (contraseña). Tenga en cuenta la capacidad de iniciar sesión con credenciales de Twitter o Facebook.

![chlimage_1-32](assets/chlimage_1-32.png)

Una vez que haya iniciado sesión como miembro de la comunidad registrado, observe los siguientes elementos de menú para hacer clic y explorar el sitio de la comunidad:

* **La opción Perfil** le permite realizar vistas y editar el perfil.
* [La opción Mensajes](/help/communities/configure-messaging.md) le dirige a la sección de mensajes directos, donde puede:

   1. Vista los mensajes directos recibidos (Bandeja de entrada), enviados (Elementos enviados) y eliminados (Papelera).
   1. Redacte nuevos mensajes directos para enviarlos a personas y grupos.

* [La opción Notificaciones](/help/communities/notifications.md) le dirige a la sección de notificaciones, donde puede realizar la vista de sus eventos de interés y editar la configuración de las notificaciones.
* [Administración](/help/communities/published-site.md#moderationlink) le dirige a la página Moderación de AEM Communities, si tiene privilegios de moderación.

![chlimage_1-33](assets/chlimage_1-33.png)

Observe que la página Calendario es la página de inicio porque la plantilla de sitio de referencia elegida incluía primero la función Calendario, seguida de la función Flujo de Actividad, la función Foro, etc. Esta estructura está visible desde la consola Plantilla [](/help/communities/sites.md#edit-site-template) del sitio o al modificar las propiedades del sitio en el entorno de creación:

![chlimage_1-34](assets/chlimage_1-34.png)

>[!NOTE]
>
>Para obtener más información sobre los componentes y funciones de Communities, visite:
>
>* [Componentes](/help/communities/author-communities.md) de comunidades (para autores)
>* [Componentes, funciones y características esenciales](/help/communities/essentials.md) (para desarrolladores)

>



### Vínculo de foro {#forum-link}

Para Vista de la función básica de foro, seleccione el vínculo Foro.

Los miembros pueden publicar un tema nuevo o seguir un tema.

Los visitantes del sitio pueden realizar vistas de anuncios y ordenarlos de diversas maneras.

![chlimage_1-35](assets/chlimage_1-35.png)

### Vínculo Grupos {#groups-link}

Como Aaron es administrador de grupos, si selecciona el vínculo Grupos, Aaron podrá crear un nuevo grupo de la comunidad seleccionando una plantilla de grupo, una imagen, si el grupo es abierto o secreto, e invitando a los miembros.

Este es un ejemplo en el que se crea un grupo en el entorno de publicación.

Los grupos también pueden crearse en el entorno del autor y gestionarse dentro del sitio de la comunidad en el entorno del autor (consola[Grupos](/help/communities/groups.md)de la comunidad). La experiencia de [crear grupos en el autor](/help/communities/nested-groups.md) es la siguiente en este tutorial.

![classic-ui](assets/classic-ui.png)

Crear un grupo de referencia:

1. Seleccionar **nuevo grupo**
1. **Ficha Configuración**

   * Nombre del grupo : `Sports`
   * Descripción : `A parent group for various sporting groups`.
   * Nombre de URL del grupo : `sports`
   * Seleccionar `Open Group` (permite que cualquier miembro de la comunidad participe mediante la participación)

1. **Ficha Plantilla**

   * Seleccionar `Reference Group` (contiene una función de grupo en su estructura para permitir grupos anidados)

1. Seleccionar **crear grupo**

![classic-ui-website](assets/classic-ui-website.png)

Una vez creado el nuevo grupo, **seleccione el nuevo grupo** Deportes para crear dos grupos (anidados) dentro de él. Como una estructura de sitio no puede comenzar con la función de grupos, después de abrir el grupo Deportes, es necesario seleccionar el vínculo Grupos:

![classic-ui-create-page](assets/classic-ui-create-page.png)

El segundo conjunto de vínculos, comenzando por `Blog`, pertenece al grupo seleccionado actualmente, el `Sports` grupo. Al seleccionar el vínculo Deportes, es posible anidar dos grupos dentro del grupo Deportes `Groups` .

Como ejemplo, agregue dos `new groups`.

* Un nombre `Baseball`

   * Déjelo configurado como un `Open Group` (pertenencia requerida).
   * En la ficha Plantillas, seleccione `Conversational Group`.

* Un nombre `Gymnastics`

   * Cambie su configuración a `Member Only Group` (pertenencia restringida).
   * En la ficha Plantillas, seleccione `Conversational Group`.

**Aviso**:

* Es posible que sea necesario actualizar la página antes de que se muestren ambos grupos.
* Esta plantilla *no incluye* la función de grupos, por lo que no será posible anidar más grupos.
* En el momento de la creación, la consola [](/help/communities/groups.md) Grupos ofrece una tercera opción: una `Public Group` (suscripción opcional).

Una vez creados ambos grupos, seleccione el grupo de béisbol, un grupo abierto y observe sus vínculos:

`Discussions` `What's New` `Members`

Los vínculos del grupo se muestran debajo de los vínculos del sitio principal y se muestran de la siguiente manera:

![classic-ui-website-page](assets/classic-ui-website-page.png)

En el caso del autor: con privilegios administrativos, vaya a la consola [Grupos de](/help/communities/members.md) comunidades y agregue Weston McCall al `Community Engage Gymnastics <uid> Members` grupo.

Continuando con la publicación, cierre la sesión como Aaron McDonald y vista los grupos en el grupo de deportes como un visitante anónimo en el sitio:

* Desde página de inicio
* Select `Groups` link
* Select `Sports` link
* Seleccione el vínculo Deportes `Groups`

Sólo el grupo de béisbol será visible.

Inicie sesión como Weston McCall (weston.mccall@dodgit.com / contraseña) y navegue a la misma ubicación. Observe que Weston es capaz `Join` del grupo abierto `Baseball` y `enter or Leave` del `Gymnastics` grupo privado.

![classic-ui-repository-vista](assets/classic-ui-repository-view.png)

### Vínculo de página Web {#web-page-link}

Vista la página Web básica incluida en el sitio seleccionando el vínculo Página Web. Las herramientas de creación de AEM estándar pueden utilizarse para añadir contenido a esta página en el entorno de creación.

Por ejemplo, vaya a la instancia de **autor** , abra la `engage` carpeta en la consola [Sitios de](/help/communities/sites-console.md)comunidades, seleccione el icono **Abrir sitio** para entrar al modo de edición de autor. A continuación, seleccione el modo de previsualización para seleccionar el `Web Page` vínculo y, a continuación, seleccione el modo de edición para añadir los componentes Título y Texto. Por último, vuelva a publicar solo la página o todo el sitio.

![classic-ui-Repository-path](assets/classic-ui-repository-path.png)

### Vínculo de moderación {#moderationlink}

Cuando el miembro de la comunidad tiene privilegios de moderación, el vínculo Moderación estará visible y, al seleccionarlo, se mostrará el contenido de la comunidad publicado y se podrá [moderar](/help/communities/moderate-ugc.md) de forma similar a la consola [de](/help/communities/moderation.md) moderación del entorno de creación.

Utilice el botón Atrás del explorador para volver al sitio publicado. La mayoría de las consolas no son accesibles desde la navegación global en el entorno de publicación. [](/help/communities/moderate-ugc.md)

![chlimage_1-42](assets/chlimage_1-42.png)

## Autoregistro {#self-registration}

Después de cerrar sesión, es posible crear un nuevo registro de usuario.

* Seleccione `Log In`
* Seleccione `Sign up for a new account`

![chlimage_1-43](assets/chlimage_1-43.png) ![chlimage_1-44](assets/chlimage_1-44.png)

De forma predeterminada, la dirección de correo electrónico es la identificación de inicio de sesión. Si no se selecciona, el visitante puede introducir su propia identificación de inicio de sesión (nombre de usuario). El nombre de usuario debe ser único en el entorno de publicación.

Después de especificar el nombre, el correo electrónico y la contraseña del usuario, al seleccionar `Sign Up` se creará el usuario y se le permitirá firmarlo.

Una vez iniciada la sesión, la primera página presentada es su `Profile` página, que pueden personalizar.

![chlimage_1-45](assets/chlimage_1-45.png)

Si el miembro olvida su identificación de inicio de sesión, es posible recuperarla utilizando su dirección de correo electrónico.

![chlimage_1-46](assets/chlimage_1-46.png)

