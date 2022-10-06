---
title: Administración de identidades
seo-title: Identity Management
description: Obtenga información sobre la administración de identidades en AEM.
seo-description: Learn about identity management in AEM.
uuid: d9b83cd7-c47a-41a5-baa4-bbf385d13bfd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 994a5751-7267-4a61-9bc7-01440a256c65
docset: aem65
exl-id: acb5b235-523e-4c01-9bd2-0cc2049f88e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 7%

---

# Administración de identidades{#identity-management}

Los visitantes individuales del sitio web solo se pueden identificar cuando se les permite iniciar sesión. Existen varias razones por las que puede que desee proporcionar una capacidad de inicio de sesión:

* [AEM Communities](/help/communities/overview.md)Es necesario que los visitantes del sitio inicien sesión para publicar contenido en la comunidad.
* [Grupos de usuarios cerrados](/help/sites-administering/cug.md)

   Es posible que deba limitar el acceso al sitio web (o a secciones de él) a visitantes específicos.

* [Personalización](/help/sites-administering/personalization.md) Permitir a los visitantes configurar ciertos aspectos de cómo acceden al sitio web.

La funcionalidad de inicio (y cierre) de sesión la proporciona un [cuenta con un **Perfil**](#profiles-and-user-accounts), que contiene información adicional sobre el visitante registrado (usuario). Los procedimientos reales de registro y autorización pueden diferir:

* Autoregistro desde el sitio web

   A [Sitio de la comunidad](/help/communities/sites-console.md) se pueden configurar para permitir a los visitantes registrarse por su cuenta de Facebook o Twitter o iniciar sesión por su cuenta.

* Solicitud de inscripción en el sitio web

   Para un grupo de usuarios cerrado, puede permitir a los visitantes solicitar el registro, pero exigir la autorización mediante un flujo de trabajo.

* Registrar cada cuenta desde el entorno de creación

   Si tiene un número pequeño de perfiles, que de todas formas necesitarán autorización, puede decidir registrar cada uno directamente.

Para permitir que los visitantes se registren, se pueden utilizar una serie de componentes y formularios para recopilar la información de identificación necesaria y, a continuación, la información de perfil adicional (a menudo opcional). Una vez registrados, también deben poder verificar y actualizar los detalles que han enviado.

Se puede configurar o desarrollar una funcionalidad adicional:

* Configure cualquier replicación inversa necesaria.
* Permita que un usuario elimine su perfil desarrollando un formulario junto con un flujo de trabajo.

>[!NOTE]
>
>La información especificada en el perfil también se puede utilizar para proporcionar al usuario contenido de destino mediante [Segmentos](/help/sites-administering/campaign-segmentation.md) y [Campañas](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

## Registro de Forms {#registration-forms}

A [formulario](/help/sites-authoring/default-components.md#form-component) se puede utilizar para recopilar la información de registro y generar la nueva cuenta y perfil.

Por ejemplo, los usuarios pueden solicitar un nuevo perfil mediante la página de Geometrixx
`http://localhost:4502/content/geometrixx-outdoors/en/user/register.html`

![registerform](assets/registerform.png)

Al enviar la solicitud, se abre la página de perfil, donde el usuario puede proporcionar detalles personales.

![profilepage](assets/profilepage.png)

La nueva cuenta también está visible en el [Consola de usuarios](/help/sites-administering/security.md).

## Inicio de sesión {#login}

El componente de inicio de sesión se puede utilizar para recopilar la información de inicio de sesión y, a continuación, activar el proceso de inicio de sesión.

Esto proporciona al visitante los campos estándar de **Nombre de usuario** y **Contraseña**, con un **Inicio de sesión** para activar el proceso de inicio de sesión cuando se introducen las credenciales.

Por ejemplo, los usuarios pueden iniciar sesión o crear una cuenta nueva mediante la **Iniciar sesión** en la barra de herramientas de Geometrixx, que utiliza la página:

`http://localhost:4502/content/geometrixx-outdoors/en/user/sign-in.html`

![inicio de sesión](assets/login.png)

## Cerrar sesión {#logging-out}

Como hay un mecanismo de inicio de sesión, también se requiere un mecanismo de cierre de sesión. Esta opción está disponible como **Cerrar sesión** en Geometrixx.

## Visualización y actualización de un perfil {#viewing-and-updating-a-profile}

Según el formulario de registro, es posible que el visitante tenga información registrada en su perfil. Deberían poder ver o actualizar esto en una etapa posterior. Esto puede hacerse de una forma similar; por ejemplo, en Geometrixx:

```
http://localhost:4502/content/geometrixx-outdoors/en/user/profile.html
```

Para ver los detalles de su perfil, haga clic en **Mi perfil** en la esquina superior derecha de cualquier página; por ejemplo, con la variable `admin` cuenta:
`http://localhost:4502/home/users/a/admin/profile.form.html/content/geometrixx-outdoors/en/user/profile.html.`

Puede ver otro perfil utilizando la variable [contexto de cliente](/help/sites-administering/client-context.md) (en el entorno de creación y con privilegios suficientes):

1. Abra una página; por ejemplo, la página de Geometrixx:

   `http://localhost:4502/cf#/content/geometrixx/en.html`

1. Haga clic en **Mi perfil** en la esquina superior derecha. Verá el perfil de su cuenta actual; por ejemplo, el administrador.
1. Press **control-alt-C** para abrir ClientContext.
1. En la esquina superior izquierda del contexto del cliente, haga clic en el botón **Cargar un perfil** botón.

   ![](do-not-localize/loadprofile.png)

1. Seleccione otro perfil en la lista desplegable de la ventana de diálogo; por ejemplo, **Alison Parker**.
1. Haga clic en **Aceptar**.
1. Haga clic de nuevo en **Mi perfil**. El formulario se actualizará con los detalles de Alison.

   ![profilealison](assets/profilealison.png)

1. Ahora puede usar **Editar perfil** o **Cambiar contraseña** para actualizar los detalles.

## Adición de campos a la definición del perfil {#adding-fields-to-the-profile-definition}

Puede agregar campos a la definición del perfil. Por ejemplo, para agregar un campo &quot;Color favorito&quot; al perfil de Geometrixx:

1. Desde la consola Sitios web , vaya a Sitio de Geometrixx Outdoors > Inglés > Usuario >Mi perfil.
1. Haga doble clic en el **Mi perfil** para abrirla y editarla.
1. En el **Componentes** de la barra de tareas expanda la **Formulario** para obtener más información.
1. Arrastre un **Lista desplegable** de la barra de tareas al formulario, justo debajo del **Acerca de mí** campo .
1. Haga doble clic en el botón **Lista desplegable** para abrir el cuadro de diálogo de configuración e introducir:

   * **Nombre de elemento** - `favoriteColor`
   * **Título** - `Favorite Color`
   * **Elementos** - Añadir varios colores como elementos

   Haga clic en **Aceptar** para guardar.

1. Cierre la página y vuelva a la **Sitios web** y active la página Mi perfil.

   La próxima vez que vea un perfil, puede seleccionar un color favorito:

   ![aparkerfavorcolor](assets/aparkerfavcolour.png)

   El campo se guardará en la sección **perfil** de la cuenta de usuario correspondiente:

   ![aparkercrxdelite](assets/aparkercrxdelite.png)

## Estados de perfil {#profile-states}

Hay varios casos de uso que requieren saber si un usuario (o su perfil) está en una *estado específico* o no.

Esto implica definir una propiedad adecuada en el perfil de usuario de una manera que:

* es visible y accesible para el usuario
* define dos estados para cada propiedad
* permite alternar entre los dos estados definidos

Esto se hace con:

* [Proveedores estatales](#state-providers)

   Para administrar los dos estados de una propiedad específica y las transiciones entre los dos.

* [Flujos de trabajo](#workflows)

   Para administrar acciones relacionadas con los estados.

Se pueden definir varios estados; por ejemplo, en la Geometrixx se incluyen:

* suscripción (o cancelación de la suscripción) a notificaciones en boletines informativos o subprocesos de comentarios
* agregar y quitar una conexión con un amigo

### Proveedores estatales {#state-providers}

Un proveedor de estado administra el estado actual de la propiedad en cuestión, junto con las transiciones entre los dos estados posibles.

Los proveedores de estado se implementan como componentes, por lo que se pueden personalizar para su proyecto. En Geometrixx, estos incluyen:

* Suscribirse/cancelar suscripción de tema de foro
* Agregar/eliminar amigo

### Flujos de trabajo {#workflows}

Los proveedores de estado administran una propiedad de perfil y sus estados.

Se necesita un flujo de trabajo para implementar las acciones relacionadas con los estados. Por ejemplo, al suscribirse a notificaciones, el flujo de trabajo gestiona la acción de suscripción real; al cancelar la suscripción a las notificaciones, el flujo de trabajo gestiona la eliminación del usuario de la lista de suscripción.

## Perfiles y cuentas de usuario {#profiles-and-user-accounts}

Los perfiles se almacenan en el repositorio de contenido como parte del[cuenta de usuario](/help/sites-administering/user-group-ac-admin.md).

El perfil se puede encontrar en `/home/users/geometrixx`:

![chlimage_1-138](assets/chlimage_1-138.png)

En una instalación estándar (autor o publicación), todos tienen acceso de lectura a toda la información de perfil de todos los usuarios. todos son &quot;*Grupo integrado que contiene automáticamente todos los usuarios y grupos existentes. La lista de miembros no se puede editar*&quot;.

Estos derechos de acceso están definidos por el siguiente ACL comodín:

/home todos permiten jcr:read rep:glob = &#42;/profile&#42;

Esto permite:

* foro, comentarios o anuncios de blog para mostrar información (como icono o nombre completo) del perfil adecuado
* vínculos a páginas de perfil de geometrixx

Si dicho acceso no es apropiado para su instalación, puede cambiar esta configuración predeterminada.

Esto se puede hacer utilizando la variable **[Control de acceso](/help/sites-administering/user-group-ac-admin.md#access-right-management)** pestaña:

![aclmanager](assets/aclmanager.png)

## Componentes de perfil {#profile-components}

También hay una serie de componentes de perfil disponibles para definir los requisitos de perfil del sitio.

### Campo de contraseña activado {#checked-password-field}

Este componente proporciona dos campos para:

* La introducción de una contraseña.
* Una verificación para confirmar que la contraseña se ha escrito correctamente.

Con la configuración predeterminada el componente aparecerá del modo siguiente:

![dc_profiles_checkedpassword](assets/dc_profiles_checkedpassword.png)

### Fotografía de avatar de perfil {#profile-avatar-photo}

Este componente proporciona al usuario un mecanismo para seleccionar y cargar un archivo de fotografía de avatar.

![dc_profiles_avatarpicture](assets/dc_profiles_avatarphoto.png)

### Nombre detallado de perfil {#profile-detailed-name}

Ese componente permite que usuario introduzca un nombre detallado.

![dc_profiles_detailname](assets/dc_profiles_detailedname.png)

### Género de perfil {#profile-gender}

Este componente permite al usuario introducir su género.

![dc_profiles_gender](assets/dc_profiles_gender.png)
