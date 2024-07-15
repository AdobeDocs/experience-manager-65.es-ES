---
title: Crear un sitio de la comunidad
description: Obtenga información sobre cómo crear un sitio de comunidades Adobe Experience Manager.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: d4c1895f-421c-4146-b94a-8d11065ef9e3
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 0%

---

# Crear un sitio de la comunidad{#author-a-new-community-site}

## Crear un sitio de la comunidad {#create-a-community-site}

Utilice la instancia de autor para crear un sitio de la comunidad. AEM En la instancia de autor de:

1. Iniciar sesión con privilegios de administrador.
1. Desde la navegación global, vaya a **[!UICONTROL Comunidades]** > **[!UICONTROL Sitios]**.

La consola Sitios de Communities proporciona un asistente para guiar a uno a través de los pasos para crear un sitio de comunidad. Es posible avanzar al paso `Next` o `Back` al paso anterior antes de comprometer el sitio en el paso final.

Para empezar a crear un sitio de la comunidad:

* Seleccione el botón `Create`.

![createcommunitysite](assets/createcommunitysite.png)

### Paso 1: Plantilla del sitio {#step-site-template}

![plantilla para crear el sitio](assets/create-site.png)

En el [paso Plantilla del sitio](/help/communities/sites-console.md#step2013asitetemplate), escriba un título, una descripción, el nombre de la dirección URL y seleccione una plantilla de sitio de la comunidad, por ejemplo:

* **Título del sitio de la comunidad**: `Getting Started Tutorial`
* **Descripción del sitio de la comunidad**: `A site for engaging with the community.`
* **Raíz del sitio de la comunidad**: (dejar en blanco para la raíz predeterminada `/content/sites`)
* **Configuraciones de nube**: (déjelo en blanco si no se especifican configuraciones de nube) proporcione la ruta a las configuraciones de nube especificadas.
* **Idioma base del sitio de la comunidad**: (no tocar para un solo idioma: inglés) use la lista desplegable para elegir uno o más *3} idiomas base entre los idiomas disponibles: alemán, italiano, francés, japonés, español, portugués (Brasil), chino (tradicional) y chino (simplificado).* Se crea un sitio de la comunidad para cada idioma agregado y existe en la misma carpeta del sitio según la práctica recomendada descrita en [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md). La página raíz de cada sitio contiene una página secundaria denominada por el código de idioma de uno de los idiomas seleccionados, como &quot;en&quot; para inglés o &quot;fr&quot; para francés.

* **Nombre del sitio de la comunidad**: engarzar

   * Compruebe el nombre, ya que no se cambia fácilmente después de crear el sitio
   * La dirección URL inicial se muestra debajo del Nombre del sitio de la comunidad
   * Para una URL válida, añada un código de idioma base + &quot;.html&quot;
   * *Por ejemplo*, https://localhost:4502/content/sites/ `engage/en.html`

* **Plantilla**: desplegar para elegir `Reference Site`

* Seleccione **Siguiente**.

### Paso 2: Diseño {#step-design}

El paso Diseño se presenta en dos secciones para seleccionar el tema y el titular de la marca:

#### TEMA DEL SITIO DE LA COMUNIDAD {#community-site-theme}

Seleccione el estilo que desee aplicar a la plantilla. Cuando se selecciona, la temática se superpone con una marca de verificación.

#### MARCA DEL SITIO DE LA COMUNIDAD {#community-site-branding}

(Opcional) Cargue una imagen de titular para mostrarla en las páginas del sitio. El banner está anclado al borde izquierdo del explorador, entre el encabezado del sitio de la comunidad y los vínculos de navegación. La altura del titular se recorta a 120 píxeles. No se cambia el tamaño del titular para ajustarse a la anchura del explorador y a la altura de 120 píxeles.

![promoción de marca en el sitio de la comunidad](assets/community-site-branding.png)

![upload-image-site](assets/upload-image-site.png)

Seleccione **Siguiente**.

### Paso 3: Configuración {#step-settings}

En el paso Configuración, antes de seleccionar `Next`, hay siete secciones que proporcionan acceso a configuraciones que implican administración de usuarios, etiquetado, moderación, administración de grupos, análisis y traducción.

#### Administración de usuarios {#user-management}

Marque todas las casillas de verificación de [Administración de usuarios](/help/communities/sites-console.md#user-management)

* Para permitir que los visitantes del sitio se registren automáticamente
* Para permitir que los visitantes del sitio vean el sitio sin iniciar sesión
* Para permitir que los miembros envíen y reciban mensajes de otros miembros de la comunidad
* Para permitir el inicio de sesión con Facebook en lugar de registrar y crear un perfil
* Para permitir el inicio de sesión con Twitter en lugar de registrar y crear un perfil

>[!NOTE]
>
>Para un entorno de producción, es necesario crear aplicaciones de Twitter y Facebook personalizadas. Ver [Inicio de sesión social con Facebook y Twitter](/help/communities/social-login.md).

![configuración del sitio de la comunidad](assets/site-settings.png)

#### ETIQUETADO {#tagging}

AEM Las etiquetas aplicadas al contenido de la comunidad se controlan seleccionando áreas de nombres definidas previamente mediante la [Consola de etiquetado](/help/sites-administering/tags.md#tagging-console) (como el [espacio de nombres del tutorial](/help/communities/setup.md#create-tutorial-tags)).

Encontrar áreas de nombres es fácil mediante la búsqueda de escritura anticipada. Por ejemplo,

* Tipo `tut`
* Seleccionar `Tutorial`

![etiquetado](assets/tagging.png)

#### ROLES {#roles}

[Las funciones de miembro de la comunidad](/help/communities/users.md) se asignan mediante la configuración de la sección Funciones.

Para permitir que un miembro de la comunidad (o grupo de miembros) experimente el sitio como administrador de la comunidad, use la búsqueda de escritura anticipada y seleccione el nombre del miembro o grupo en las opciones de la lista desplegable.

Por ejemplo,

* Tipo `q`
* Seleccione a Quinn Harper

>[!NOTE]
>
>[El servicio de túnel](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) permite la selección de miembros y grupos que sólo existen en el entorno de publicación.

![roles de usuario en el nuevo sitio](assets/site-admin-1.png)

#### MODERACIÓN {#moderation}

Acepte la configuración global predeterminada para [moderar](/help/communities/sites-console.md#moderation) contenido generado por el usuario (UGC).

![moderación](assets/moderation1.png)

#### ANALYTICS {#analytics}

Si Adobe Analytics tiene licencia y se han configurado un servicio y una estructura de Analytics Cloud, es posible habilitar Analytics y seleccionar la estructura.

Consulte [Configuración de Analytics para funciones de comunidades](/help/communities/analytics.md).

![análisis](assets/analytics.png)

#### TRADUCCIÓN {#translation}

La [configuración de traducción](/help/communities/sites-console.md#translation) especifica el idioma base del sitio, si se puede traducir UGC y a qué idioma, en caso afirmativo.

* Comprobar **Permitir traducción automática**
* Deje seleccionados los idiomas predeterminados para la traducción mediante el servicio de traducción automática predeterminado
* Dejar el proveedor de traducción y la configuración predeterminados
* No es necesario un almacén global porque no hay copias de idioma
* Seleccionar **Traducir toda la página**
* Dejar la opción de persistencia predeterminada

![configuración de traducción](assets/translation-settings.png)

### Paso 4: Crear sitio de comunidades {#step-create-communities-site}

Seleccione **Crear.**

![crear sitio](assets/create-site2.png)

Cuando el proceso termina, la carpeta del nuevo sitio se muestra en la consola Comunidades - Sitios.

![communitiessitesconsole](assets/communitiessitesconsole.png)

## Publish el sitio de la comunidad {#publish-the-community-site}

El sitio creado debe administrarse desde la consola Comunidades - Sitios, la misma consola desde la que se pueden crear nuevos sitios.

Después de seleccionar la carpeta del sitio de la comunidad para abrirlo, pase el ratón sobre el icono del sitio de modo que aparezcan cuatro iconos de acción:

![siteactionicon-1](assets/siteactionicons-1.png)

Al seleccionar el cuarto icono de elipses (Más acciones), aparecerán las opciones Exportar sitio y Eliminar sitio.

![siteactionsnew-1](assets/siteactionsnew-1.png)

De izquierda a derecha son:

* **Abrir sitio**

  Al seleccionar el icono de lápiz, se abre el sitio de la comunidad en el modo de edición de Autor, donde puede agregar o configurar componentes de página.

* **Editar sitio**

  Al seleccionar el icono de propiedades, se abre el sitio de la comunidad para modificar las propiedades, como el título o para cambiar el tema.

* **Sitio de Publish**

  Al seleccionar el icono del mundo, se publica el sitio de la comunidad (por ejemplo, si el servidor de publicación se está ejecutando en el equipo local y, a continuación, en localhost:4503 de forma predeterminada).

* **Exportar sitio**

  Al seleccionar el icono de exportación, se crea un paquete del sitio de la comunidad que está almacenado en [Administrador de paquetes](/help/sites-administering/package-manager.md) y que se ha descargado. UGC no está incluido en el paquete del sitio.

* **Eliminar sitio**

  Al seleccionar el icono de eliminación, se eliminará el sitio de la comunidad de **[!UICONTROL Communities > Consola de sitios]**. Esta acción elimina todos los elementos asociados con el sitio, como UGC, grupos de usuarios, recursos y registros de bases de datos.

![siteactions](assets/siteactions.png)

>[!NOTE]
>
>Si no utiliza el puerto predeterminado 4503 para la instancia de publicación, edite el agente de replicación predeterminado para establecer el número de puerto en el valor correcto.
>
>En la instancia de autor, en el menú principal:
>
>1. Vaya al menú **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Replicación]**.
>1. Seleccionar **[!UICONTROL agentes en autor]**.
>1. Seleccione **[!UICONTROL Agente predeterminado (publicar)]**.
>1. Junto a **[!UICONTROL Configuración]**, seleccione **[!UICONTROL Editar]**.
>1. En el cuadro de diálogo emergente de Configuración del agente, seleccione la ficha **[!UICONTROL Transporte]**.
>1. En URI, cambie el número de puerto 4503 por el número de puerto deseado. Por ejemplo, para utilizar el puerto 6103: https://localhost:6103/bin/receive?sling:authRequestLogin=1
>1. Seleccione **[!UICONTROL Aceptar]**.
>1. (Opcional) Seleccione **[!UICONTROL Borrar]** o **[!UICONTROL Forzar reintento]** para restablecer la cola de replicación.

### Seleccionar Publish {#select-publish}

Después de asegurarse de que el servidor de publicación se está ejecutando, seleccione el icono del mundo para publicar el sitio de la comunidad.

![sitio de publicación](assets/publish-site.png)

Cuando el sitio de la comunidad se ha publicado correctamente, aparece brevemente el mensaje &quot;Sitio publicado&quot;.

### Nuevos grupos de usuarios de la comunidad {#new-community-user-groups}

Junto con el nuevo sitio de la comunidad, se crean nuevos grupos de usuarios que tienen los permisos adecuados establecidos para diversas funciones administrativas. Para obtener más información, visite [Grupos de usuarios para sitios de la comunidad](/help/communities/users.md#usergroupsforcommunitysites).

Para este nuevo sitio de comunidad, dado el nombre de sitio &quot;participar&quot; en el paso 1, los cuatro nuevos grupos de usuarios pueden verse desde la [consola Grupos](/help/communities/members.md) (navegación global: Comunidades, Grupos):

* Community Engage Administradores de la comunidad
* Administradores del grupo de participación de comunidad
* Miembros de Community Engage
* Moderadores de Community Engage
* Miembros privilegiados de Community Engage
* Administrador de contenido del sitio Community Engage

[Aaron McDonald](/help/communities/tutorials.md#demo-users) es miembro de

* Community Engage Administradores de la comunidad
* Moderadores de Community Engage
* Miembros de participación de la comunidad (indirectamente como miembro del grupo de moderadores)

![grupo de usuarios](assets/user-group.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![participar](assets/engage.png)

## Configurar para error de autenticación {#configure-for-authentication-error}

Una vez configurado e insertado un sitio para la publicación, [configure el inicio de sesión en la asignación](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) en la instancia de publicación. La ventaja es que cuando las credenciales de inicio de sesión no se introducen correctamente, el error de autenticación vuelve a mostrar la página de inicio de sesión del sitio de la comunidad con un mensaje de error.

Agregar `Login Page Mapping` como

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## Pasos opcionales {#optional-steps}

### Cambiar la página principal predeterminada {#change-the-default-home-page}

Al trabajar con el sitio de publicación con fines de demostración, puede resultar útil cambiar la página principal predeterminada al nuevo sitio.

Para ello, es necesario usar [CRXDE](https://localhost:4503/crx/de) Lite para editar la tabla de [asignación de recursos](/help/sites-deploying/resource-mapping.md) al publicar.

Para empezar:

1. En una instancia de publicación, inicie sesión con privilegios de administrador.
1. Vaya a [https://localhost:4503/crx/de](https://localhost:4503/crx/de).
1. En el explorador del proyecto, expanda `/etc/map.`
1. Seleccione el nodo `http`:

   * Seleccionar **Crear nodo:**

      * **Nombre** localhost.4503
(no *no* usa &#39;:&#39;)

      * **Tipo** [sling:Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Con el nodo `localhost.4503` recién creado seleccionado:

   * Agregar propiedad:

   * **Nombre** sling:match
      * Cadena **Type**
      * **Valor** localhost.4503/$
(debe finalizar con &#39;$$&#39; char)

   * Agregar propiedad:

      * **Nombre** sling:internalRedirect
      * Cadena **Type**
      * **Valor** /content/sites/engage/en.html

1. Seleccione **Guardar todo.**
1. (Opcional) Elimine el historial de exploración.
1. Vaya a https://localhost:4503/.

   * Llegada a https://localhost:4503/content/sites/engage/en.html

>[!NOTE]
>
>Para deshabilitarlo, simplemente agregue un prefijo al valor de la propiedad `sling:match` con una &quot;x&quot; (`xlocalhost.4503/$`) y **Guardar todo**.

![pasos-opcionales](assets/optional-steps.png)

#### Solución de problemas: Error al guardar el mapa {#troubleshooting-error-saving-map}

Si no puede guardar los cambios, asegúrese de que el nombre del nodo es `localhost.4503`, con un separador de &quot;puntos&quot;, y no `localhost:4503` con un separador de &quot;dos puntos&quot;, ya que `localhost` no es un prefijo de espacio de nombres válido.

![mensaje de error](assets/error-message.png)

#### Solución de problemas: error al redirigir {#troubleshooting-fail-to-redirect}

El &#39;**$**&#39; al final de la cadena de expresión regular `sling:match`es crucial, de modo que solo se asigna `https://localhost:4503/`; de lo contrario, el valor de redirección se antepone a cualquier ruta de acceso que pueda existir después de server:port en la dirección URL. AEM Por lo tanto, cuando el usuario intenta redirigir a la página de inicio de sesión, se produce un error.

### Modificación del sitio {#modify-the-site}

AEM Una vez creado el sitio por primera vez, los autores pueden usar el [icono Abrir sitio](/help/communities/sites-console.md#authoring-site-content) para realizar actividades de creación de contenido estándar para la creación de contenido en el sitio de la página web.

Además, los administradores pueden usar el [icono Editar sitio](/help/communities/sites-console.md#modifying-site-properties) para modificar las propiedades del sitio, como el título.

Después de realizar cualquier modificación, recuerda **guardar** y volver a **Publish** el sitio.

>[!NOTE]
>
>AEM Si no está familiarizado con el uso de las páginas, vea la documentación sobre [manejo básico](/help/sites-authoring/basic-handling.md) y una [guía rápida para crear páginas](/help/sites-authoring/qg-page-authoring.md).
