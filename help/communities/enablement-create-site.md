---
title: Crear un nuevo sitio de comunidad para habilitarlo
seo-title: Crear un nuevo sitio de comunidad para habilitarlo
description: Crear un sitio de comunidad para habilitarlo
seo-description: Crear un sitio de comunidad para habilitarlo
uuid: a75fa566-a570-45fd-aabc-23651ef819cc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: b9333558-6af9-46b2-9f03-3722645c69a6
docset: aem65
translation-type: tm+mt
source-git-commit: e9d5a7acad04d841cbc7d62050163f3de998fab6
workflow-type: tm+mt
source-wordcount: '1728'
ht-degree: 3%

---


# Crear un nuevo sitio de comunidad para habilitarlo {#author-a-new-community-site-for-enablement}

## Crear sitio de comunidad {#create-community-site}

[La ](/help/communities/sites-console.md) creación del sitio de comunidad emplea un asistente que lo guía a través de los pasos para crear un sitio de comunidad. Es posible avanzar al paso `Next` o `Back` al paso anterior antes de comprometer el sitio en el paso final.

Para empezar a crear un nuevo sitio de comunidad:

Uso de la instancia de autor [](https://localhost:4502/)

* Inicie sesión con privilegios de administrador y vaya a **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.

* Seleccione **Crear**.

### Paso 1: Plantilla de sitio {#step-site-template}

![plantilla de sitio de habilitación](assets/enablement-site-template.png)

En el paso **Plantilla de sitio**, escriba un título, una descripción, el nombre de la dirección URL y seleccione una plantilla de sitio de comunidad, por ejemplo:

* **Título del sitio de la comunidad**: `Enablement Tutorial`.

* **Descripción del sitio de la comunidad**: `A site for enabling the community to learn.`

* **Raíz** del sitio de la comunidad: (dejar en blanco para la raíz predeterminada  `/content/sites`)

* **Configuraciones** de nube: (deje en blanco si no se especifica ninguna configuración de nube) proporcione la ruta a las configuraciones de nube especificadas.
* **Idioma** base del sitio de la comunidad: (dejar intacto para un solo idioma: Inglés) utilice la lista desplegable para elegir uno  *o* varios idiomas disponibles: alemán, italiano, francés, japonés, español, portugués (Brasil), chino (tradicional) y chino (simplificado). Se creará un sitio de comunidad para cada idioma agregado y existirá dentro de la misma carpeta de sitio siguiendo las optimizaciones descritas en [Traducir contenido para sitios multilingües](/help/sites-administering/translation.md). La página raíz de cada sitio contendrá una página secundaria con el nombre del código de idioma de uno de los idiomas seleccionados, como &quot;en&quot; para inglés o &quot;fr&quot; para francés.

* **Nombre del sitio de la comunidad**: `enable`

   * La dirección URL inicial se mostrará debajo del nombre del sitio de la comunidad
   * Para una dirección URL válida, anexe un código de idioma base + &quot;.html&quot;
      *Por ejemplo*, https://localhost:4502/content/sites/  `enable/en.html`

* **Plantilla** de sitio de referencia: desplegable para elegir  `Reference Structured Learning Site Template`

Seleccione **Siguiente**.

### Paso 2: Diseño {#step-design}

El paso Diseño se presenta en dos secciones para seleccionar el tema y la pancarta de marca:

#### TEMA DEL SITIO COMUNITARIO {#community-site-theme}

Seleccione el estilo que desee aplicar a la plantilla. Cuando se selecciona, el tema se superpone con una marca de verificación.

#### MARCA DEL SITIO COMUNITARIO {#community-site-branding}

(Opcional) Cargue una imagen de pancarta para mostrarla en las páginas del sitio. La pancarta se fija en el borde izquierdo del explorador, entre el encabezado del sitio de la comunidad y el menú (vínculos de navegación). La altura de la pancarta se recorta a 120 píxeles. No se puede cambiar el tamaño del letrero para que se ajuste al ancho del navegador y a la altura de 120 píxeles.

![site-branding1](assets/site-branding1.png)

![site-branding2](assets/site-branding2.png)

Seleccione **Siguiente**.

### Paso 3: Configuración {#step-settings}

En el paso Configuración, antes de seleccionar `Next`, observe que hay siete secciones que proporcionan acceso a configuraciones que incluyen administración de usuarios, etiquetado, funciones, moderación, análisis, traducción y habilitación.

#### ADMINISTRACIÓN DE USUARIOS {#user-management}

Se recomienda que [comunidades habilitadoras](/help/communities/overview.md#enablement-community) sean privadas.

Un sitio de la comunidad es privado cuando se deniega el acceso a los visitantes anónimos del sitio, es posible que no se registre por sí mismo y que no utilice el inicio de sesión en redes sociales.

Asegúrese de que la mayoría de las casillas de verificación no estén seleccionadas para [Administración de usuarios](/help/communities/sites-console.md#user-management):

* NO permita que los visitantes del sitio se autorregistren.
* NO permita que visitantes anónimos del sitio realicen vistas en el sitio.
* Opcional si se permite o no la mensajería entre los miembros de la comunidad.
* NO permitir el inicio de sesión con Facebook.
* NO permitir el inicio de sesión con Twitter.

![user-mgmt](assets/user-mgmt.png)

#### ETIQUETADO {#tagging}

Las etiquetas que se pueden aplicar al contenido de la comunidad se controlan seleccionando AEM Áreas de nombres previamente definidas mediante la [Consola de etiquetado](/help/sites-administering/tags.md#tagging-console) (como la [Área de nombres del tutorial](/help/communities/enablement-setup.md#create-tutorial-tags)).

Además, la selección de Áreas de nombres de etiquetas para el sitio de la comunidad limita la selección presentada al definir los catálogos y los recursos de habilitación. Consulte [Etiquetado de recursos de habilitación](/help/communities/tag-resources.md) para obtener información importante.

La búsqueda de Áreas de nombres es sencilla mediante la búsqueda por tipo. Por ejemplo,

* Tipo `tut`
* Seleccione `Tutorial`

![habilitación y etiquetado](assets/enablement-tagging.png)

### ROLES {#roles}

[Las ](/help/communities/users.md) funciones de miembros de la comunidad se asignan mediante la configuración de la sección Roles.

Para permitir que un miembro de la comunidad (o grupo de miembros) experimente el sitio como administrador de la comunidad, utilice la búsqueda de tipo por adelantado y seleccione el nombre del miembro o grupo en las opciones de la lista desplegable.

Por ejemplo,

* Tipo `q`
* Seleccione [Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[El servicio ](/help/communities/deploy-communities.md#tunnel-service-on-author) de túnel permite seleccionar miembros y grupos que solo existen en el entorno de publicación.

![roles de habilitación](assets/site-admin.png)

#### MODERACIÓN {#moderation}

Acepte la configuración global predeterminada para [moderar](/help/communities/sites-console.md#moderation) contenido generado por el usuario (UGC).

![moderación1](assets/moderation1.png)

#### ANALYTICS {#analytics}

En la lista desplegable, seleccione el marco de servicios en la nube de Analytics configurado para este sitio de comunidad.

La selección que se ve en la captura de pantalla, `Communities`, es el ejemplo del marco de trabajo de la documentación de configuración [.](/help/communities/analytics.md#aem-analytics-framework-configuration)

![análisis](assets/analytics.png)

#### TRADUCCIÓN {#translation}

La [configuración de traducción](/help/communities/sites-console.md#translation) especifica si se puede traducir o no UGC y en qué idioma, si es así.

* Marque **Permitir traducción automática**
* Usar la configuración predeterminada

![traducción](assets/translation.png)

#### HABILITACIÓN {#enablement}

Para una comunidad de habilitación, es necesario identificar uno o varios administradores de habilitación de la comunidad.

* **Administradores**
 de habilitación (requeridos) Miembros de la 
`Community Enablement Managers` están disponibles para ser seleccionados para administrar este sitio de comunidad.

   * Tipo `s`
   * Seleccione `Sirius Nilson`

* **ID**
 de organización de Marketing Cloud (opcional) El ID de una cuenta de Adobe Analytics que es necesario para incluir  [Video Heartbeat ](/help/communities/analytics.md#video-heartbeat-analytics) Analytics en el sistema de informes de habilitación.

![habilitación](assets/enablement.png)

Seleccione **Siguiente**.

### Paso 4: Crear sitio de comunidad {#step-create-community-site}

Seleccione **Crear.**

![previsualización](assets/preview.png)

Cuando se completa el proceso, la carpeta del nuevo sitio se muestra en la consola Comunidades > Sitios.

![enablementsitecreated](assets/enablementsitecreated.png)

### Publicar el nuevo sitio de comunidad {#publish-the-new-community-site}

El sitio creado debe administrarse desde la consola Comunidades - Sitios, la misma consola desde la que se pueden crear nuevos sitios.

Después de seleccionar la carpeta del sitio de comunidad, coloque el puntero sobre el icono del sitio para que aparezcan cuatro iconos de acción:

![siteactionicons](assets/siteactionicons.png)

Al seleccionar el icono de elipses (icono Más acciones), aparecen las opciones Exportar sitio y Eliminar sitio.

![siteactionsnew](assets/siteactionsnew.png)

De izquierda a derecha están:

* **Abrir sitio**

   Seleccione el icono del lápiz para abrir el sitio de la comunidad en modo de edición de autor, para agregar o configurar componentes de página.

* **Editar sitio**

   Seleccione el icono de propiedades para abrir el sitio de la comunidad y modificar las propiedades, como el título, o para cambiar el tema.

* **Publicar sitio**

   Seleccione el icono mundial para publicar el sitio de comunidad (en localhost:4503 de forma predeterminada).

* **Exportar sitio**

   Seleccione el icono de exportación para crear un paquete del sitio de la comunidad que se almacene en [administrador de paquetes](/help/sites-administering/package-manager.md) y se descargue.
Tenga en cuenta que UGC no se incluye en el paquete del sitio.

* **Eliminar sitio**

   Para eliminar el sitio de comunidad, seleccione el icono Eliminar sitio que aparece al pasar el ratón sobre el sitio en la Consola de sitio de comunidades. Esta acción elimina todos los elementos asociados con el sitio, como UGC, grupos de usuarios, recursos y registros de bases de datos.

   ![enablesiteactions](assets/enablesiteactions.png)

#### Seleccione Publicar {#select-publish}

Seleccione el icono del mundo para publicar el sitio de la comunidad.

![publish-site](assets/publish-site.png)

Habrá una indicación de que el sitio fue publicado.

![sitio publicado](assets/site-published.png)

## Usuarios y grupos de usuarios de la comunidad {#community-users-user-groups}

### Aviso de nuevos grupos de usuarios de la comunidad {#notice-new-community-user-groups}

Junto con el nuevo sitio de comunidad, se crean nuevos grupos de usuarios que tienen los permisos adecuados establecidos para diversas funciones administrativas. Para obtener más información, visite [Grupos de usuarios para sitios de la comunidad](/help/communities/users.md#usergroupsforcommunitysites).

Para este nuevo sitio de comunidad, dado el nombre del sitio &quot;habilitar&quot; en el Paso 1, los nuevos grupos de usuarios que existen en el entorno de publicación pueden verse desde la [consola Miembros y grupos de comunidades](/help/communities/members.md#groups-console):

![community_usergroup](assets/community_usergroup.png)

### Asignar miembros al grupo de miembros de habilitación de comunidad {#assign-members-to-community-enable-members-group}

Al crear, con el servicio de túnel habilitado, es posible asignar los [usuarios creados durante la configuración inicial](/help/communities/enablement-setup.md#publishcreateenablementmembers) al grupo Miembros de la comunidad para el sitio de la comunidad recién creado.

Mediante la consola Grupos de la comunidad, los miembros se pueden agregar de forma individual o mediante la pertenencia a un grupo.

En este ejemplo, el grupo `Community Ski Class` se agrega como miembro del grupo `Community Enable Members` así como como miembro `Quinn Harper`.

* Vaya a la consola **Communities, Groups**
* Seleccionar grupo *Miembros de habilitación de comunidad*
* Escriba &#39;ski&#39; en el cuadro de búsqueda **Añadir miembros al grupo**
* Seleccione *Clase de esquí de la comunidad* (grupo de alumnos)
* Escriba &#39;quinn&#39; en el cuadro de búsqueda
* Seleccione *Quinn Harper* (contacto de recursos de habilitación)

* Seleccione **Guardar**

![edit-group-settings](assets/edit-group-settings.png)

## Configuraciones en la publicación {#configurations-on-publish}

`https://localhost:4503/content/sites/enable/en.html {#http-localhost-content-sites-enable-en-html}`

![habilitación-inicio de sesión](assets/enablement-login.png)

### Error de configuración para autenticación {#configure-for-authentication-error}

Una vez configurado y insertado un sitio para publicar, [configure la asignación de inicio de sesión](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) en la instancia de publicación. La ventaja es que cuando las credenciales de inicio de sesión no se especifican correctamente, el error de autenticación vuelve a mostrar la página de inicio de sesión del sitio de la comunidad con un mensaje de error.

Añada un `Login Page Mapping` como:

* `/content/sites/enable/en/signin:/content/sites/enable/en`

### (Opcional) Cambie la Página de inicio predeterminada {#optional-change-the-default-home-page}

Al trabajar con el sitio de publicación con fines de demostración, puede resultar útil cambiar la página de inicio predeterminada al nuevo sitio.

Para ello, es necesario utilizar [CRX|DE](https://localhost:4503/crx/de) Lite para editar la tabla [asignación de recursos](/help/sites-deploying/resource-mapping.md) al publicar.

Para empezar:

1. Al realizar la publicación, acceda a CRXDE e inicie sesión con privilegios de administrador

   * Por ejemplo: vaya a [https://localhost:4503/crx/de](https://localhost:4503/crx/de) e inicie sesión con `admin/admin`

1. En el explorador del proyecto, expanda `/etc/map`
1. Seleccione el nodo `http`

   * Seleccione **Crear nodo**

      * **** Namelocalhost.4503

         (do *no* use &#39;:&#39;)

      * **** [Escritos:Asignación](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Con el nodo `localhost.4503` recién creado seleccionado

   * Añadir propiedad

      * **** Namesling:match
      * **** TypeString
      * **** Valuelocalhost.4503/$

   (debe terminar con &#39;$&#39; char)

   * Añadir propiedad

      * **** Namesling:internalRedirect
      * **** TypeString
      * **Valor** /content/sites/enable/en.html


1. Seleccione **Guardar todo**
1. (Opcional) Eliminar el historial de exploración
1. Vaya a https://localhost:4503/

   * Llegar a https://localhost:4503/content/sites/enable/en.html

>[!NOTE]
>
>Para deshabilitar, simplemente anteponga el valor de la propiedad `sling:match` con una &#39;x&#39; - `xlocalhost.4503/$` - y **Guardar todo**.

![change-default-homepage](assets/change-default-homepage.png)

#### Resolución de problemas: Error al guardar el mapa {#troubleshooting-error-saving-map}

Si no puede guardar los cambios, asegúrese de que el nombre del nodo sea `localhost.4503`, con un separador de &#39;punto&#39; y no `localhost:4503` con un separador de &#39;dos puntos&#39;, ya que `localhost` no es un prefijo de Área de nombres válido.

![error-map](assets/error-map.png)

#### Resolución de problemas: Error al redirigir {#troubleshooting-fail-to-redirect}

El &#39;**$**&#39; al final de la cadena `sling:match` de la expresión regular es crucial, de modo que sólo se asigna exactamente `https://localhost:4503/`, de lo contrario el valor de redirección se antepone a cualquier ruta que pueda existir después del servidor:puerto en la dirección URL. Por lo tanto, cuando AEM intenta redireccionar a la página de inicio de sesión, se produce un error.

## Modificación del sitio de comunidad {#modifying-the-community-site}

Una vez creado el sitio por primera vez, los autores pueden utilizar el [icono Abrir sitio](/help/communities/sites-console.md#authoring-site-content) para realizar actividades de creación de AEM estándar.

Además, los administradores pueden utilizar el [icono Editar sitio](/help/communities/sites-console.md#modifying-site-properties) para modificar las propiedades del sitio, como el título.

Después de cualquier modificación, recuerde **Guardar** y volver a-**Publicar** el sitio.

>[!NOTE]
>
>Si no está familiarizado con AEM, vista la documentación sobre [administración básica](/help/sites-authoring/basic-handling.md) y una [guía rápida para crear páginas](/help/sites-authoring/qg-page-authoring.md).

### Añadir un catálogo {#add-a-catalog}

La plantilla de sitio de comunidad elegida para este sitio de comunidad debe contener la función de catálogo.

Si no es así, la función de catálogo se puede añadir fácilmente. Esto permitiría a otros miembros de la comunidad, no asignados a recursos de habilitación o a una ruta de aprendizaje, seleccionar recursos de habilitación de un catálogo.

Si la estructura del sitio ya contiene la función de catálogo, se puede cambiar su Título.

Para modificar la estructura del sitio, vaya a la consola **[!UICONTROL Communities]** > **[!UICONTROL Sites]**, abra la carpeta `enable` y seleccione el icono **Editar sitio** para acceder a las propiedades de `Enablement Tutorial`.

Seleccione el panel ESTRUCTURA para añadir un catálogo o modificar uno existente:

* **Título**: `Ski Catalog`

* **URL**: `catalog`

* **Seleccionar todas las Áreas de nombres**: dejar como predeterminado.

* Seleccione **Guardar**.

![modify-site-structure](assets/modify-site-structure.png)

Utilice el icono Posición para mover la función Catálogo a la segunda posición, después de Asignaciones.

![move-catalog-func](assets/move-catalog-func.png)

Seleccione **Guardar** en la esquina superior derecha para guardar los cambios en el sitio de comunidad.

A continuación, vuelva a-**Publicar** el sitio.

