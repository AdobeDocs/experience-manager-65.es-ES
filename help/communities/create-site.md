---
title: Crear un nuevo sitio de comunidad
seo-title: Crear un nuevo sitio de comunidad
description: Cómo crear un nuevo sitio de AEM Communities
seo-description: Cómo crear un nuevo sitio de AEM Communities
uuid: 4f609f5f-ef07-44fc-aeb3-1c616e120d46
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8ae324ea-8b84-47a3-aabf-1fee2a3bd46d
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# Crear un nuevo sitio de comunidad{#author-a-new-community-site}

## Crear un sitio de comunidad {#create-a-community-site}

Utilice la instancia de autor para crear un sitio de comunidad. En la instancia de AEM Author:

1. Inicie sesión con privilegios de administrador.
1. Desde la navegación global, vaya a **Navegación, Comunidades, Sitios.**

La consola Sitios de comunidades proporciona un asistente para guiar uno a través de los pasos para crear un sitio de comunidad. Es posible avanzar al `Next`paso o `Back`al paso anterior antes de comprometer el sitio en el paso final.

Para empezar a crear un nuevo sitio de comunidad:

* seleccione el `Create`botón.

![createcommunitysite](assets/createcommunitysite.png)

### Paso 1: Plantilla de sitio {#step-site-template}

![plantilla para crear el sitio](assets/create-site.png)

En el paso [Plantilla de](/help/communities/sites-console.md#step2013asitetemplate)sitio, escriba un título, una descripción, el nombre de la dirección URL y seleccione una plantilla de sitio de comunidad, por ejemplo:

* **Título del sitio de la comunidad**: `Getting Started Tutorial`
* **Descripción del sitio de la comunidad**: `A site for engaging with the community.`
* **Raíz** del sitio de la comunidad: (dejar en blanco para la raíz predeterminada `/content/sites`)
* **Configuraciones** de nube: (deje en blanco si no se especifica ninguna configuración de nube) proporcione la ruta a las configuraciones de nube especificadas.
* **Idioma** base del sitio de la comunidad: (dejar intacto para un solo idioma: Inglés) utilice la lista desplegable para elegir uno *o más* idiomas básicos de los disponibles: alemán, italiano, francés, japonés, español, portugués (Brasil), chino (tradicional) y chino (simplificado). Se creará un sitio de comunidad para cada idioma agregado y existirá dentro de la misma carpeta de sitio siguiendo las optimizaciones descritas en [Traducir contenido para sitios](/help/sites-administering/translation.md)multilingües. La página raíz de cada sitio contendrá una página secundaria con el nombre del código de idioma de uno de los idiomas seleccionados, como &quot;en&quot; para inglés o &quot;fr&quot; para francés.

* **Nombre** del sitio de la comunidad: participar

   * verifique dos veces el nombre, ya que no es fácil cambiarlo después de crear el sitio
   * la dirección URL inicial se mostrará debajo del nombre del sitio de la comunidad
   * para una dirección URL válida, anexe un código de idioma base + &quot;.html&quot;
   * *por ejemplo*, https://localhost:4502/content/sites/ `engage/en.html`

* **Plantilla**: desplegable para elegir `Reference Site`

Seleccione **Siguiente**

### Paso 2: Diseño {#step-design}

El paso Diseño se presenta en dos secciones para seleccionar el tema y la pancarta de marca:

#### COMMUNITY SITE THEME {#community-site-theme}

Seleccione el estilo que desee aplicar a la plantilla. Cuando se selecciona, el tema se superpone con una marca de verificación.

#### COMMUNITY SITE BRANDING {#community-site-branding}

(opcional) Cargue una imagen de pancarta para mostrarla en las páginas del sitio. La pancarta se fija en el borde izquierdo del explorador, entre el encabezado del sitio de la comunidad y los vínculos de navegación. La altura de la pancarta se recorta a 120 píxeles. No se puede cambiar el tamaño del letrero para que se ajuste al ancho del navegador y a la altura de 120 píxeles.

![chlimage_1-58](assets/chlimage_1-58.png) ![chlimage_1-59](assets/chlimage_1-59.png)

Seleccione **Siguiente**.

### Paso 3:Configuración {#step-settings}

En el paso Configuración, antes de seleccionar `Next`, tenga en cuenta que hay siete secciones que proporcionan acceso a configuraciones que incluyen administración de usuarios, etiquetado, moderación, administración de grupos, análisis, traducción y habilitación.

Visite el tutorial [Introducción a Comunidades de AEM para la habilitación](/help/communities/getting-started-enablement.md) para experimentar el trabajo con las funciones de habilitación.

#### Administración de usuarios {#user-management}

Marcar todas las casillas de verificación para Administración [de usuarios](/help/communities/sites-console.md#user-management)

* para permitir que los visitantes del sitio se automatriculen
* para permitir que los visitantes del sitio vean el sitio sin iniciar sesión
* permitir a los miembros enviar y recibir mensajes de otros miembros de la comunidad
* para permitir el inicio de sesión en Facebook en lugar de registrar y crear un perfil
* para permitir el inicio de sesión con Twitter en lugar de registrar y crear un perfil

>[!NOTE]
>
>Para un entorno de producción, es necesario crear aplicaciones personalizadas de Facebook y Twitter. Consulte Inicio de sesión en [Social con Facebook y Twitter](/help/communities/social-login.md).

![configuración del sitio de comunidad](assets/site-settings.png)

#### TAGGING {#tagging}

Las etiquetas que se pueden aplicar al contenido de la comunidad se controlan seleccionando los espacios de nombres de AEM definidos previamente mediante la Consola [de](/help/sites-administering/tags.md#tagging-console) etiquetado (como el espacio de nombres [Tutorial](/help/communities/setup.md#create-tutorial-tags)).

La búsqueda de espacios de nombres es sencilla mediante la búsqueda por tipo. Por ejemplo,

* type &#39;tut&#39;
* select `Tutorial`

![chlimage_1-60](assets/chlimage_1-60.png)

#### ROLES {#roles}

[Las funciones](/help/communities/users.md) de miembro de la comunidad se asignan mediante la configuración de la sección Roles.

Para permitir que un miembro de la comunidad (o grupo de miembros) experimente el sitio como administrador de la comunidad, utilice la búsqueda de tipo por adelantado y seleccione el nombre del miembro o grupo en las opciones de la lista desplegable.

Por ejemplo,

* type &quot;q&quot;
* seleccionar [Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[El servicio](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) de túnel permite seleccionar miembros y grupos que solo existen en el entorno de publicación.

![funciones de usuario en el nuevo sitio](assets/site-admin-1.png)

#### MODERATION {#moderation}

Acepte la configuración global predeterminada para [moderar](/help/communities/sites-console.md#moderation) el contenido generado por el usuario (UGC).

![chlimage_1-61](assets/chlimage_1-61.png)

#### ANALYTICS {#analytics}

Si Adobe Analytics tiene licencia y se ha configurado un marco y un servicio en la nube de Analytics, es posible activar Analytics y seleccionar el marco.

Consulte Configuración [de Analytics para funciones](/help/communities/analytics.md)de comunidades.

![chlimage_1-62](assets/chlimage_1-62.png)

#### TRANSLATION {#translation}

La configuración [de](/help/communities/sites-console.md#translation) traducción especifica el idioma base del sitio, así como si se puede traducir o no UGC y en qué idioma, si es así.

* marcar **Permitir traducción automática**
* deje los idiomas predeterminados seleccionados para la traducción por el servicio predeterminado de traducción automática
* dejar el proveedor de traducción predeterminado y la configuración
* no hay necesidad de una tienda global porque no hay copias de idioma
* seleccionar **Traducir toda la página**
* dejar persistencia predeterminada, opción

![chlimage_1-63](assets/chlimage_1-63.png)

#### ENABLEMENT {#enablement}

Deje vacío al crear una comunidad de participación.

Para ver un tutorial similar con el fin de crear rápidamente una comunidad [de](/help/communities/overview.md#enablement-community)habilitación, consulte [Introducción a Comunidades de AEM para la habilitación](/help/communities/getting-started-enablement.md).

Seleccione **Siguiente**.

### Paso 4: Crear sitio de comunidades {#step-create-communities-site}

Seleccione **Crear.**

![chlimage_1-64](assets/chlimage_1-64.png)

Cuando se completa el proceso, la carpeta del nuevo sitio se muestra en la consola Comunidades - Sitios.

![communitiessitesconsole](assets/communitiessitesconsole.png)

## Publicar el sitio de la comunidad {#publish-the-community-site}

El sitio creado debe administrarse desde la consola Comunidades - Sitios, la misma consola desde la que se pueden crear nuevos sitios.

Después de seleccionar la carpeta del sitio de la comunidad para abrirlo, coloque el puntero sobre el icono del sitio para que aparezcan cuatro iconos de acción:

![siteactionicons-1](assets/siteactionicons-1.png)

Al seleccionar el cuarto icono de elipses (Más acciones), aparecen las opciones Exportar sitio y Eliminar sitio.

![siteactionsnew-1](assets/siteactionsnew-1.png)

De izquierda a derecha están:

* **Abrir sitio** seleccione el icono de lápiz para abrir el sitio de la comunidad en modo de edición de autor, para agregar o configurar componentes de página

* **Editar sitio** seleccione el icono de propiedades para abrir el sitio de la comunidad y modificar las propiedades, como el título o cambiar el tema

* **Publicar sitio** seleccione el icono mundial para publicar el sitio de la comunidad (por ejemplo, si el servidor de publicación se está ejecutando en el equipo local y, a continuación, en localhost:4503 de forma predeterminada)

* **Exportar sitio** seleccione el icono de exportación para crear un paquete del sitio de la comunidad que se almacene en el administrador [de](/help/sites-administering/package-manager.md) paquetes y se descargue.
Tenga en cuenta que UGC no se incluye en el paquete del sitio.

* **Eliminar sitio**seleccione el icono Eliminar para eliminar el sitio de comunidad desde la consola Comunidades > Sitios. Esta acción elimina todos los elementos asociados con el sitio, como UGC, grupos de usuarios, recursos y registros de bases de datos.

![siteacciones](assets/siteactions.png)

>[!NOTE]
>
>Si no utiliza el puerto predeterminado 4503 para la instancia de publicación, edite el agente de replicación predeterminado para establecer el número de puerto en el valor correcto.
>
>En la instancia de creación, en el menú principal:
>
>1. Vaya al menú Herramientas > Operaciones > Replicación.
1. Seleccione &quot;Agentes en el autor&quot;.
1. Seleccione &quot;Agente predeterminado (publicación)&quot;.
1. Al lado de &quot;Configuración&quot;, seleccione &quot;Editar&quot;.
1. En el cuadro de diálogo emergente Configuración del agente, seleccione la ficha Transporte.
1. En URI, cambie el número de puerto, 4503, al número de puerto deseado >
   * por ejemplo, para utilizar el puerto 6103:
https://localhost:6103/bin/receive?sling:authRequestLogin=1
1. Seleccione &quot;Aceptar&quot;.
1. (opcional) Seleccione &quot;Borrar&quot; o &quot;Forzar reintento&quot; para restablecer la cola de replicación.




### Seleccione Publicar {#select-publish}

Después de asegurarse de que el servidor de publicación se está ejecutando, seleccione el icono del mundo para publicar el sitio de comunidad.

![chlimage_1-65](assets/chlimage_1-65.png)

Cuando el sitio de la comunidad se ha publicado correctamente, aparece brevemente un mensaje:

![chlimage_1-66](assets/chlimage_1-66.png)

### Nuevos grupos de usuarios de la comunidad {#new-community-user-groups}

Junto con el nuevo sitio de comunidad, se crean nuevos grupos de usuarios que tienen los permisos adecuados establecidos para diversas funciones administrativas. Para obtener más información, visite Grupos [de usuarios para sitios](/help/communities/users.md#usergroupsforcommunitysites)de la comunidad.

Para este nuevo sitio de comunidad, dado el nombre del sitio &quot;participar&quot; en el Paso 1, los cuatro nuevos grupos de usuarios pueden verse desde la consola [](/help/communities/members.md) Grupos (navegación global: Comunidades, Grupos):

* Administradores de comunidad de participación
* Administradores del grupo de participación de la comunidad
* Miembros de participación de la comunidad
*  Moderadores de participación de la comunidad
* Miembros privilegiados de participación en la comunidad
* Administrador de contenido del sitio de participación de la comunidad

Tenga en cuenta que [Aaron McDonald](/help/communities/tutorials.md#demo-users) es miembro de

* Administradores de comunidad de participación
*  Moderadores de participación de la comunidad
* Miembros de participación de la comunidad (indirectamente como miembro del grupo Moderadores)

![chlimage_1-67](assets/chlimage_1-67.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![chlimage_1-68](assets/chlimage_1-68.png)

## Error de configuración para autenticación {#configure-for-authentication-error}

Una vez que un sitio se ha configurado y se ha insertado para publicar, [configure la asignación](/help/communities/sites-console.md#configure-for-authentication-error) de inicio de sesión ( `Adobe Granite Login Selector Authentication Handler`) en la instancia de publicación. La ventaja es que cuando las credenciales de inicio de sesión no se especifican correctamente, el error de autenticación vuelve a mostrar la página de inicio de sesión del sitio de la comunidad con un mensaje de error.

Agregar un `Login Page Mapping` como

* /content/sites/engagement/es/sign:/content/sites/engagement/es

## Pasos opcionales {#optional-steps}

### Cambiar la página principal predeterminada {#change-the-default-home-page}

Al trabajar con el sitio de publicación con fines de demostración, puede resultar útil cambiar la página principal predeterminada al nuevo sitio.

Para ello, es necesario utilizar [CRXDE](https://localhost:4503/crx/de) Lite para editar la tabla de asignación [de](/help/sites-deploying/resource-mapping.md) recursos al realizar la publicación.

Para empezar:

1. En la instancia de publicación, inicie sesión con privilegios de administrador.
1. Vaya a [https://localhost:4503/crx/de](https://localhost:4503/crx/de).
1. En el navegador del proyecto, expanda `/etc/map.`
1. Seleccione el `http` nodo:

   * Seleccione **Crear nodo:**

      * **Nombre** localhost.4503( *no use* &#39;:&#39;)

      * **Type** [sling:Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Con `localhost.4503` nodo recién creado seleccionado:

   * Agregar propiedad:

      * **Nombre** sling:match
      * **Cadena de tipo**
      * **Valor** localhost.4503/$(debe terminar con &#39;$&#39; char)
   * Agregar propiedad:

      * **Nombre** sling:internalRedirect
      * **Cadena de tipo**
      * **Valor** /content/sites/engage/en.html


1. Seleccione **Guardar todo.**
1. (opcional) Elimine el historial de exploración.
1. Vaya a https://localhost:4503/.

   * llegar a https://localhost:4503/content/sites/engage/en.html

>[!NOTE]
Para deshabilitar, simplemente anteponga el valor de la `sling:match` propiedad con un prefijo &#39;x&#39; - `xlocalhost.4503/$` - y **Guardar todo**.

![chlimage_1-69](assets/chlimage_1-69.png)

#### Resolución de problemas: Error al guardar el mapa {#troubleshooting-error-saving-map}

Si no se pueden guardar los cambios, asegúrese de que el nombre del nodo está `localhost.4503`separado por un separador de puntos y no `localhost:4503` por un separador de dos puntos, ya que no `localhost`es un prefijo de espacio de nombres válido.

![chlimage_1-70](assets/chlimage_1-70.png)

#### Resolución de problemas: Error al redirigir {#troubleshooting-fail-to-redirect}

El valor &#39;**$**&#39; al final de la `sling:match`cadena de expresión regular es crucial, por lo que solo `https://localhost:4503/` se asigna exactamente, de lo contrario el valor de redireccionamiento se antepone a cualquier ruta que pueda existir después de server:port en la dirección URL. Por lo tanto, cuando AEM intenta redireccionar a la página de inicio de sesión, se produce un error.

### Modificar el sitio {#modify-the-site}

Una vez creado el sitio por primera vez, los autores pueden utilizar el icono [](/help/communities/sites-console.md#authoring-site-content) Abrir sitio para realizar actividades de creación de AEM estándar.

Además, los administradores pueden utilizar el icono [](/help/communities/sites-console.md#modifying-site-properties) Editar sitio para modificar las propiedades del sitio, como el título.

Después de realizar cualquier modificación, recuerde **guardar** y volver a **publicar** el sitio.

>[!NOTE]
Si no está familiarizado con AEM, consulte la documentación sobre la gestión [](/help/sites-authoring/basic-handling.md) básica y una guía [rápida para crear páginas](/help/sites-authoring/qg-page-authoring.md).

