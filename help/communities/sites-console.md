---
title: Consola Sitios de comunidades
description: Obtenga información sobre cómo acceder a la consola Sitios de Communities para crear, editar y administrar sitios.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 426e3adf-3723-4d17-a988-6eb050939e68
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '3084'
ht-degree: 0%

---

# Consola Sitios de comunidades {#communities-sites-console}

La consola Sitios de Communities proporciona acceso a:

* Creación del sitio
* Edición del sitio
* Administración del sitio
* [Creación y edición de grupos anidados](/help/communities/groups.md) (subcomunidades)

Consulte [Introducción a AEM Communities](/help/communities/getting-started.md), donde podrá experimentar la rapidez con que se puede crear un sitio de comunidad en el entorno de creación y cómo crear grupos de comunidad a partir de los entornos de creación y publicación.

>[!NOTE]
>
>Los menús principales de Communities para la creación de [sitios de la comunidad](/help/communities/sites-console.md), [plantillas de sitios de la comunidad](/help/communities/sites.md), [plantillas de grupos de la comunidad](/help/communities/tools-groups.md) y [funciones de la comunidad](/help/communities/functions.md) se utilizan solamente en el entorno de creación.

## Requisitos previos {#prerequisites}

Antes de crear un sitio de la comunidad, es *necesario*:

* Asegúrese de que se estén ejecutando una o más instancias de Publish.
* Habilite el [servicio de túnel](/help/communities/deploy-communities.md#tunnel-service-on-author) para administrar miembros y grupos de miembros.
* Identifique al [editor principal](/help/communities/deploy-communities.md#primary-publisher).
* [Configurar replicación](/help/communities/deploy-communities.md#replication-agents-on-author) cuando el puerto del editor principal no es el predeterminado (4503).

La práctica recomendada, para asegurarse de que el sitio está preparado para admitir muchas funciones, es seguir los siguientes pasos:

* Instale [el último paquete de funciones](/help/communities/deploy-communities.md#latestfeaturepack).
* Habilitar [Adobe Analytics](/help/communities/analytics.md) para AEM Communities.
* Configurar [correo electrónico](/help/communities/email.md)
* Identificar a [administradores de la comunidad](/help/communities/users.md#creating-community-members).
* [Habilitar el controlador OAuth](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler) para el inicio de sesión social.

## Acceder a la consola Sitios de Communities {#accessing-communities-sites-console}

En el entorno Autor, para llegar a la consola Sitios de Communities:

* Desde la navegación global: **[!UICONTROL Comunidades]** > **[!UICONTROL Sitios]**

La consola Sitios de comunidades muestra todos los sitios de la comunidad existentes. Desde esta consola, se pueden crear, editar, administrar y eliminar sitios de la comunidad.

Para crear un sitio de la comunidad, seleccione el icono **Crear**.

Para acceder a un sitio de la comunidad existente para crear, modificar, publicar, exportar o agregar un grupo anidado, seleccione el icono de carpeta del sitio.

## Creación del sitio {#site-creation}

La consola de creación de sitios proporciona un método paso a paso para combinar características del sitio basadas en una [plantilla y configuración del sitio de la comunidad](/help/communities/sites.md) seleccionadas.

Todos los sitios creados incluyen una función de inicio de sesión, ya que los visitantes del sitio deben iniciar sesión antes de poder publicar contenido, enviar mensajes o participar en un grupo. Otras funciones incluidas son los perfiles de usuario, los mensajes, las notificaciones, el menú del sitio, la búsqueda, el establecimiento de temas y la marca.

El proceso se inicia seleccionando el botón `Create` en la parte superior de la consola Sitios de Communities.

El proceso de creación es una serie de pasos que se presentan como paneles que contienen un conjunto de funciones que se van a configurar (presentadas como subpaneles). Es posible avanzar al paso **Siguiente** o **Atrás** al paso anterior antes de comprometer el sitio en el paso final.

### Paso 1: Plantilla del sitio {#step-site-template}

![newsitetemplate](assets/newsitetemplate.png)

En el panel Plantilla del sitio, se especifican el Título, la Descripción, la Raíz del sitio, el Idioma base, el Nombre y la Plantilla del sitio:

* **Título del sitio de la comunidad**

  Un título para mostrar para el sitio.

  El título aparece en el sitio publicado y en la interfaz de usuario de administración del sitio.

* **Descripción del sitio de la comunidad**

  Una descripción del sitio.

  La descripción no aparece en el sitio publicado.

* **Raíz del sitio de la comunidad**

  Ruta raíz al sitio.

  La raíz predeterminada es `/content/sites`, pero se puede mover a cualquier ubicación del sitio web.

* **Idioma de base del sitio de la comunidad**

  (Dejar intacto para un solo idioma: inglés) Utilice el menú desplegable para elegir uno o más *idiomas base entre los idiomas disponibles: alemán, italiano, francés, japonés, español, portugués (Brasil), chino (tradicional) y chino (simplificado).* Se crea un sitio de la comunidad para cada idioma agregado y existe en la misma carpeta del sitio según la práctica recomendada descrita en [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md). La página raíz de cada sitio contiene una página secundaria denominada por el código de idioma de uno de los idiomas seleccionados, como &quot;en&quot; para inglés o &quot;fr&quot; para francés.

* **Nombre del sitio de la comunidad**:

  Nombre de la página raíz del sitio que aparece en la dirección URL.

   * Compruebe el nombre, ya que no se cambia fácilmente después de crear el sitio.
   * La dirección URL base ( `https://server:port/site root/site name)`) se muestra debajo de `Community Site Name`.

   * Para una URL válida, añada un código de idioma base + &quot;.html&quot;

     *Por ejemplo*, `https://localhost:4502/content/sites/mysight/en.html`

* Menú **Plantilla de sitio de la comunidad**

  Utilice el menú desplegable para elegir una [plantilla del sitio de la comunidad](/help/communities/tools.md) disponible.

* Seleccione **Siguiente**.

### Paso 2: Diseño {#step-design}

El panel Diseño contiene dos subpaneles para seleccionar el tema y el titular de la marca:

#### TEMA DEL SITIO DE LA COMUNIDAD {#community-site-theme}

![tema del sitio](assets/sitetheme.png)

El marco de trabajo utiliza `Twitter Bootstrap` para llevar un diseño flexible y adaptable al sitio. Se puede seleccionar una de las muchas temáticas del Bootstrap precargadas para aplicar estilo a la plantilla del sitio de la comunidad seleccionada o se puede cargar una temática del Bootstrap.

Cuando se selecciona, la temática se superpone con una marca de verificación azul opaca.

Una vez publicado el sitio de la comunidad, es posible [editar las propiedades](#modifying-site-properties) y seleccionar un tema diferente.

#### MARCA DEL SITIO DE LA COMUNIDAD {#community-site-branding}

![promoción de marca en el sitio](assets/site-branding.png)

La marca del sitio de comunidad es una imagen que se muestra como encabezado en la parte superior de cada página.

El tamaño de la imagen debe ser igual de ancho que la visualización esperada de la página en el explorador y 120 píxeles de alto.

Al crear o seleccionar una imagen, tenga en cuenta lo siguiente:

* La altura de la imagen se recorta a 120 píxeles medidos desde el borde superior de la imagen.
* La imagen se fija al borde izquierdo de la ventana del explorador.
* No se cambia el tamaño de la imagen, de modo que cuando el ancho de la imagen es...

   * Menor que el ancho del explorador, la imagen se repite horizontalmente.
   * Con un ancho mayor que el del explorador, la imagen parece recortada.

* Seleccione **Siguiente**.

### Paso 3: Configuración {#step-settings}

El panel Configuración contiene varios subpaneles que presentan las funciones que se deben configurar antes de pasar al último paso para crear el sitio.

* [USER MANAGEMENT](#user-management)
* [ETIQUETADO](#tagging)
* [ROLES](#roles)
* [MODERACIÓN](#moderation)
* [ANALYTICS](#analytics)
* [TRADUCCIÓN](#translation)

>[!NOTE]
>
>**Habilitar servicio de túnel**
>
>Varios de los subpaneles Configuración permiten asignar un miembro de confianza para moderar UGC, administrar grupos o ser contactos para habilitar recursos en el entorno de publicación.
>
>La convención es que [usuarios y grupos de usuarios](/help/communities/users.md) (miembros y grupos de miembros) del lado de la publicación no se dupliquen en el entorno de creación.
>
>Por lo tanto, al crear el sitio de la comunidad en el entorno de creación y asignar miembros de confianza a diversas funciones, es necesario recuperar datos de miembros del entorno de publicación.
>
>Esto se logra habilitando ` [AEM Communities Publish Tunnel Service](/help/communities/deploy-communities.md#tunnel-service-on-author)` para el entorno de creación.

#### USER MANAGEMENT {#user-management}

![createsitesettings](assets/createsitesettings.png)

* **Permitir el registro de usuarios**

  Si se selecciona, los visitantes del sitio pueden convertirse en miembros de la comunidad mediante el registro automático.
Si no se selecciona, el sitio de la comunidad está *restringido* y los visitantes del sitio deben asignarse al grupo de miembros del sitio de la comunidad, realizar una solicitud o recibir una invitación por correo electrónico. Si no se selecciona, no se debe permitir el acceso anónimo.
Desmarque un sitio de la comunidad *private*. La opción predeterminada está activada.

* **Permitir acceso anónimo**

  Si se selecciona, el sitio de la comunidad está *abierto* y cualquier visitante del sitio puede acceder al sitio.
Si no se selecciona, solo los miembros que han iniciado sesión pueden acceder al sitio.
Desmarque un sitio de la comunidad *private*. La opción predeterminada está activada.

* **Permitir mensajes**

  Si esta opción está activada, los miembros pueden enviarse mensajes entre sí y al grupo dentro del sitio de la comunidad.
Si no se selecciona, la mensajería no está configurada para la comunidad.
El valor predeterminado está desmarcado.

* **Permitir inicios de sesión sociales: Facebook**

  Si se selecciona, permita que los visitantes del sitio inicien sesión con las credenciales de su cuenta de Facebook. La [configuración de nube de Facebook](/help/communities/social-login.md#create-a-facebook-connect-cloud-service) seleccionada debe configurarse para agregar usuarios al grupo de miembros del sitio de la comunidad una vez que se haya creado el sitio de la comunidad.
Si no se selecciona, no se muestra ningún inicio de sesión de Facebook.
Deje sin marcar un sitio de la comunidad *private*. El valor predeterminado está desmarcado.

* **Permitir inicios de sesión sociales: Twitter**

  Si se selecciona, permita que los visitantes del sitio inicien sesión con las credenciales de su cuenta de Twitter. La [configuración de nube de Twitter](/help/communities/social-login.md#create-a-twitter-connect-cloud-service) seleccionada debe configurarse para agregar usuarios al grupo de miembros del sitio de la comunidad una vez que se haya creado el sitio de la comunidad.
Si no se selecciona, no se muestra ningún inicio de sesión de Twitter.
Deje sin marcar un sitio de la comunidad *private*. El valor predeterminado está desmarcado.

>[!NOTE]
>
>**Permitir inicios de sesión sociales**
>
>Aunque pueden existir configuraciones de Twitter y Facebook de ejemplo que se pueden seleccionar para un [entorno de producción](/help/sites-administering/production-ready.md), es necesario crear aplicaciones de Twitter y Facebook personalizadas. Ver [Inicio de sesión social con Facebook y Twitter](/help/communities/social-login.md).

#### ETIQUETADO {#tagging}

![etiquetado de sitios](assets/site-tagging.png)

Las etiquetas, que se pueden aplicar al contenido de la comunidad, se controlan seleccionando Espacios de nombres de etiquetas definidos anteriormente mediante [Consola de etiquetado](/help/sites-administering/tags.md#tagging-console).

Además, la selección de áreas de nombres de etiquetas para el sitio de la comunidad limita la selección presentada al definir catálogos y recursos.

* cuadro de búsqueda de texto: empiece a escribir para identificar las etiquetas que se pueden utilizar en el sitio.

#### ROLES {#roles}

![Funciones de la comunidad](assets/site-admin-2.png)

Las [funciones de los miembros de la comunidad](/help/communities/users.md) se asignan con esta configuración.

Encontrar miembros de la comunidad es fácil mediante la búsqueda anticipada.

* **Administradores de la comunidad**

  Empiece a escribir para seleccionar uno o más miembros de la comunidad o grupos de miembros que puedan administrar miembros de la comunidad y grupos de miembros.

* **Moderadores de la comunidad**

  Empiece a escribir para seleccionar uno o varios miembros de la comunidad o grupos de miembros en los que se debe confiar como moderadores del contenido generado por el usuario.

* **Miembros privilegiados de la comunidad**

  Empiece a escribir para seleccionar uno o más miembros o grupos de miembros de la comunidad para que se les conceda la capacidad de crear contenido cuando se haya seleccionado `Allow Privileged Member` para una [función de la comunidad](/help/communities/functions.md).

* **Administradores de la comunidad**

  Empiece a escribir para seleccionar uno o varios administradores del sitio que puedan administrar la estructura del sitio independientemente de otros administradores del sitio y del administrador de la comunidad predeterminado. Pueden crear grupos en cualquier nivel de la jerarquía y convertirse en el administrador predeterminado de los grupos anidados (pero más tarde se pueden eliminar de la función de administrador de los grupos anidados).

#### MODERACIÓN {#moderation}

![moderación del sitio](assets/site-moderation.png)

La configuración global para moderar el contenido generado por el usuario (UGC) está controlada por esta configuración. Los componentes individuales tienen ajustes adicionales para controlar la moderación.

* **Contenido con moderación previa**

  Si se selecciona, el contenido publicado en la comunidad no aparece hasta que lo apruebe un moderador. El valor predeterminado está desmarcado. Para obtener más información, consulte [Moderar el contenido de la comunidad](/help/communities/moderate-ugc.md#premoderation).

* **Umbral de indicación antes de ocultar el contenido**

  Si es mayor que 0, el número de veces que se debe marcar un tema o una publicación antes de ocultarlo de la vista pública. Si se establece en -1, el tema o la publicación marcados nunca se ocultarán de la vista pública. El valor predeterminado es 5.

#### ANALYTICS {#analytics}

![análisis del sitio](assets/site-analytics.png)

* **Habilitar Analytics**

  Solo está disponible cuando Adobe Analytics se ha [configurado](/help/communities/analytics.md) para las características de Communities.
El valor predeterminado está desmarcado. Cuando se selecciona, aparece un menú de selección adicional:

![site-analytics-enable](assets/site-analytics-enable.png)

* **Referencia del marco de configuración de nube**

  En el menú desplegable, seleccione el marco de servicio de Analytics Cloud configurado para este sitio de la comunidad.
  `Communities` es el ejemplo de marco de trabajo de la documentación de [Configuración de Analytics para funciones de comunidades](/help/communities/analytics.md#aem-analytics-framework-configuration).

#### TRADUCCIÓN {#translation}

![traducción del sitio](assets/site-translation.png)

* **Permitir traducción automática**

  Cuando se selecciona (la opción predeterminada está desactivada), la traducción automática está habilitada para UGC dentro del sitio. Esto no afecta a ningún otro contenido, como el contenido de la página, aunque el sitio esté configurado como multilingüe. Consulte [Traducción de contenido generado por el usuario](/help/communities/translate-ugc.md) para obtener información sobre cómo configurar un servicio de traducción con licencia para AEM Communities. Consulte [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md) para obtener una descripción general completa.

![permitir-traducción automática](assets/allow-machine-translation.png)

* **Habilitar la traducción automática para los idiomas seleccionados**

  Los idiomas habilitados para la traducción automática tienen de forma predeterminada la configuración del sistema especificada en [configuración de integración de traducción](/help/communities/translate-ugc.md#translation-integration-configuration). Esta configuración predeterminada se puede sobrescribir para este sitio eliminando los valores predeterminados o seleccionando otros idiomas en el menú desplegable.

* **Elegir un proveedor de traducción**

  De manera predeterminada, el proveedor de servicios es un servicio de prueba que utiliza `microsoft` únicamente con fines de demostración. Si no hay ningún proveedor de servicios de traducción con licencia, **Permitir traducción automática** debe estar desmarcado.

* **Elegir un almacén compartido global**

  Para un sitio web con varias copias de idioma, un almacén compartido global proporciona un único hilo de conversación, visible desde cada copia de idioma. Esto se logra seleccionando uno de los idiomas incluidos como copia de idioma. El valor predeterminado es *Sin almacén compartido global*.

* **Elegir configuración del proveedor de traducción**

  Elija un [marco de trabajo de integración de traducciones](/help/sites-administering/tc-tic.md) creado para el proveedor de traducción con licencia.

* **Seleccione las opciones de traducción para el sitio de la comunidad**

   * **Traducir toda la página**

     Si se selecciona, todos los UGC de una página se traducen al idioma base de la página.

     El valor predeterminado es *no seleccionado*.

   * **Traducir solo la selección**

     Si se selecciona, aparece una opción de traducción junto a cada entrada que permite traducir entradas individuales al idioma base de la página.
El valor predeterminado es *seleccionado*.

* **Seleccionar opciones de persistencia**

   * **Traducir contribuciones a petición del usuario y continuar después**
Si se selecciona, el contenido no se traduce hasta que se realiza una solicitud. Una vez traducida, la traducción se almacena en el repositorio.

     El valor predeterminado es *no seleccionado*.

   * **No mantener traducciones**

     Si se selecciona, las traducciones no se almacenan en el repositorio.

     Si no se selecciona, las traducciones se mantienen.

     El valor predeterminado es *no seleccionado*.

* **Procesamiento inteligente**

  Seleccione una de las siguientes opciones:

   * `Always show contributions in the original language` (predeterminada)
   * `Always show contributions in user preferred language`
   * `Show contributions in user preferred language for only logged-in users`

### Paso 4: Crear sitio de comunidades {#step-create-communities-site}

Si es necesario hacer algún ajuste, usa el botón **Atrás** para hacerlo.

Una vez que **Create** se selecciona e inicia, el proceso de creación del sitio no se puede interrumpir.

Una vez creado el sitio:

* No se admite el cambio de la dirección URL (nombre de nodo).
* Los cambios futuros en la plantilla del sitio de la comunidad no afectan al sitio de la comunidad creado.
* La deshabilitación de la plantilla del sitio de la comunidad no afecta al sitio de la comunidad creado.
* Es posible editar la [ESTRUCTURA](#modify-structure) de un sitio de la comunidad modificando sus propiedades.

![crear sitio](assets/create-site1.png)

Cuando finaliza el proceso, la carpeta del nuevo sitio se muestra en la consola Sitios de Communities, desde donde los autores pueden agregar contenido de página o los administradores pueden modificar las propiedades del sitio.

![modificar-sitio-propiedad](assets/modify-site-property.png)

Para editar un sitio de la comunidad, seleccione su carpeta de proyecto para abrirlo:

![proyecto del sitio](assets/site-project.png)

Al pasar el ratón por encima de un sitio o tocar una tarjeta del sitio, aparecen iconos que permiten lo siguiente:

* [edición del sitio en modo de autor](#authoring-site-content)
* [abrir las propiedades del sitio para modificarlas](#modifying-site-properties)
* [publicación del sitio](#publishing-the-site)
* [exportación del sitio](#exporting-the-site)
* [eliminar el sitio](#deleting-the-site)

## Creación de contenido del sitio {#authoring-site-content}

AEM El contenido de un sitio puede crearse con las mismas herramientas que cualquier otro sitio web de la. Para abrir el sitio para la creación, seleccione el icono `Open Site` que aparece al pasar el ratón por el sitio. El sitio se abre en una nueva ficha de forma que la consola Sitios de Communities permanece accesible.

![contenido del sitio](assets/site-content.png)

>[!NOTE]
>
>AEM Si no está familiarizado con el uso de las páginas, vea la documentación sobre [manejo básico](/help/sites-authoring/basic-handling.md) y una [guía rápida para crear páginas](/help/sites-authoring/qg-page-authoring.md).

## Modificación de propiedades del sitio {#modifying-site-properties}

![editar sitio](assets/edit-site.png)

Las propiedades de un sitio existente, especificadas durante el proceso de creación del sitio, se pueden modificar seleccionando el icono `Edit Site` que aparece al pasar el ratón por el sitio.

`Details of the following properties match the descriptions provided in the` [Creación de sitio](#site-creation) sección.

![modify-site-basicinfo](assets/modify-site-basicinfo.png)

### Modificar básico {#modify-basic}

El panel BÁSICO permite modificar lo siguiente:

* Título del sitio de la comunidad
* Descripción del sitio de la comunidad

El nombre del sitio de la comunidad no se puede modificar.

Elegir una plantilla de sitio de comunidad diferente no tendría ningún efecto en un sitio de comunidad existente, ya que no queda ninguna conexión entre las plantillas y los sitios.

En su lugar, se puede modificar la [ESTRUCTURA](#modify-structure) del sitio de la comunidad.

### Modificar estructura {#modify-structure}

El panel ESTRUCTURA permite modificar la estructura creada inicialmente a partir de la plantilla de sitio de la comunidad seleccionada. Desde el panel, es posible:

* Arrastre y suelte [funciones de la comunidad](/help/communities/functions.md) adicionales en la estructura del sitio.
* En una instancia de una función de comunidad en la estructura del sitio:

   * **`gear icon`**

     Editar la configuración, incluidos el título para mostrar y el nombre de dirección URL, y [grupos de miembros privilegiados](/help/communities/users.md#privilegedmembersgroups).

   * **`trashcan icon`**

     Quitar (eliminar) funciones de la estructura del sitio.

   * **`grid icon`**

     Modifique el orden de las funciones tal como se muestran en la barra de navegación de nivel superior del sitio.

>[!NOTE]
>
>Puede cambiar el orden de todas las funciones en la estructura del sitio a excepción de la función de la parte superior. Por lo tanto, no se puede cambiar la página principal de un sitio de la comunidad.

>[!CAUTION]
>
>* Aunque el título para mostrar se puede cambiar sin efectos secundarios, no se recomienda editar el nombre de la URL de una función de la comunidad que pertenece a un sitio de la comunidad.
>
>Por ejemplo, al cambiar el nombre de la URL no se mueve el UGC existente, por lo que se &quot;pierde&quot; el UGC.

>[!CAUTION]
>
>La función de grupos debe *no* ser la función *primero ni la única* en la estructura del sitio.
>
>Cualquier otra función, como [page function](/help/communities/functions.md#page-function), debe incluirse y enumerarse primero.

#### Ejemplo : Agregar una función de catálogo a una estructura de sitio de la comunidad {#example-adding-a-catalog-function-to-a-community-site-structure}

![agregar-catálogo-sitio](assets/add-catalog-site.png)

### Modificar diseño {#modify-design}

El panel DISEÑO permite aplicar una nueva temática:

* [Tema del sitio de la comunidad](#community-site-theme)
* [Marca del sitio de la comunidad](#community-site-branding)

   * Desplácese hasta la parte inferior del panel para poder cambiar la imagen de marca.

### Modificar configuración {#modify-settings}

El panel CONFIGURACIÓN permite acceder a la mayoría de las configuraciones en los subpaneles de para el paso 3 de la creación del sitio de la comunidad:

* [Administración de usuarios](#user-management)
* [Etiquetas](#tagging)
* [Moderación](#moderation)
* [Funciones de miembro](#roles)
* [Análisis](#analytics)
* [Traducción](#translation)

### Modificar miniatura {#modify-thumbnail}

El panel MINIATURA permite cargar una imagen para representar el sitio en la consola Sitios de Communities.

## Publicación del sitio {#publishing-the-site}

Después de crear o modificar un sitio de la comunidad, es posible publicarlo (activarlo) seleccionando el icono `Publish Site` que aparece al pasar el ratón sobre el sitio.

![sitio de publicación](assets/publish-site.png)

Hay una indicación después de que el sitio se publique correctamente.

![publicado en el sitio](assets/site-published.png)

### Publicación con grupos anidados {#publishing-with-nested-groups}

Después de publicar un sitio de la comunidad, es necesario publicar individualmente cada subcomunidad (grupo anidado) creada mediante la [consola Grupos](/help/communities/groups.md).

## Exportación del sitio {#exporting-the-site}

![sitio de exportación](assets/export-site.png)

Seleccione el icono de exportación cuando pase el ratón sobre el sitio, para que pueda crear un paquete del sitio de la comunidad que esté almacenado en [Administrador de paquetes](/help/sites-administering/package-manager.md) y descargado.

UGC no está incluido en el paquete del sitio.

## Eliminación del sitio {#deleting-the-site}

![deleteicon](assets/deleteicon.png)

Para eliminar el sitio de la comunidad, seleccione el icono Eliminar sitio que aparece al pasar el ratón por encima del sitio en la Consola del sitio de Communities. Esta acción elimina todos los elementos asociados con el sitio, como UGC, grupos de usuarios, recursos y registros de bases de datos.

## Grupos de usuarios de la comunidad creados {#created-community-user-groups}

Una vez publicado el nuevo sitio de la comunidad, se crean nuevos grupos de miembros (grupos de usuarios en el entorno de publicación) que tienen los permisos adecuados establecidos para diversas funciones administrativas y de miembro.

El nombre creado para los grupos de miembros incluye *site-name* dado en [Paso 1](#step13asitetemplate) (el nombre que aparece en la dirección URL). También incluye un ID único para evitar conflictos con los sitios y grupos de la comunidad que tienen el mismo nombre de sitio para diferentes raíces de sitio de la comunidad.

Por ejemplo: si los nombres fueran &quot;participación&quot; para un sitio titulado &quot;Tutorial de introducción&quot;, el grupo de usuarios para moderadores sería:

* title: Moderadores de participación de la comunidad
* nombre: comunidad-*engage-uid*-moderators

Los miembros que tengan asignadas funciones como moderadores o administradores de grupos al crear el sitio se asignan al grupo correspondiente y se asignan al grupo de miembros. Estos grupos y asignaciones de miembros se crean al publicar el nuevo sitio.

Para obtener más información, consulte [Administración de usuarios y grupos de usuarios](/help/communities/users.md).

>[!NOTE]
>
>Si [Permitir inicio de sesión social: Facebook](#user-management) está habilitado, una vez que el grupo de usuarios `community-<site-name>-<uid>-members`
>se ha creado, el [servicio de nube Facebook](/help/communities/social-login.md#createafacebookcloudservice) aplicado debe configurarse para agregar usuarios a este grupo.

## Configurar para error de autenticación {#configure-for-authentication-error}

De forma predeterminada, un sitio de la comunidad redirige a una página de inicio de sesión de ejemplo cuando el usuario introduce credenciales incorrectas y no puede iniciar sesión. Este inicio de sesión de muestra no está presente en [servidor de producción](/help/sites-administering/production-ready.md).

Para redirigir correctamente, una vez que se ha configurado un sitio y se ha insertado para publicarlo, complete estos pasos para obtener el error de autenticación para redirigir al sitio de la comunidad:

* AEM En cada instancia de publicación de la.
* Iniciar sesión con privilegios de administrador.
* Acceda a la [consola web](/help/sites-deploying/configuring-osgi.md).

   * Por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

* Busque `Adobe Granite Login Selector Authentication Handler`.
* Seleccione el icono `pencil` para poder abrir la configuración y editarla.
* Escriba **Asignaciones de página de inicio de sesión** como se indica a continuación:

  `/content/sites/<site-name>/path/to/login/page:/content/sites/<site-name>`

  Por ejemplo:
  `/content/sites/engage/en/signin:/content/sites/engage/en`

* Seleccione **Guardar**.

![error de autenticación](assets/auth-error.png)

### Probar redirección de autenticación {#test-authentication-redirection}

AEM En la misma instancia de publicación de configurada con una asignación de página de inicio de sesión para el sitio de la comunidad:

* Vaya a la página de inicio del sitio de la comunidad.

   * Por ejemplo, [https://localhost:4503/content/sites/engage/en.html](https://localhost:4503/content/sites/engage/en.html)

* Seleccione Cerrar sesión.
* Seleccione Iniciar sesión.
* Introduzca credenciales incorrectas, como el nombre de usuario &quot;x&quot; y la contraseña &quot;x&quot;.
* La página de inicio de sesión debe mostrarse con el error &quot;inicio de sesión no válido&quot;.

![prueba-autenticación](assets/test-authentication.png)

## Acceder a los sitios de la comunidad desde la consola Sitios principales {#accessing-community-sites-from-main-sites-console}

Desde la consola Sitios de navegación global, los sitios de la comunidad se encuentran en la carpeta `Community Sites`.

Aunque es posible acceder a un sitio de la comunidad de esta manera, para tareas administrativas, se debe acceder al sitio de la comunidad desde la consola Sitios de comunidades.

![sitio de acceso](assets/access-site.png)
