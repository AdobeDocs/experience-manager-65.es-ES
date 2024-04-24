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

Consulte [Introducción a AEM Communities](/help/communities/getting-started.md) dónde puede experimentar la rapidez con la que se puede crear un sitio de comunidad en el entorno de creación y cómo crear grupos de comunidad a partir de los entornos de creación y publicación.

>[!NOTE]
>
>Los principales menús de Communities para la creación de [sitios de la comunidad](/help/communities/sites-console.md), [plantillas de sitio de comunidad](/help/communities/sites.md), [plantillas de grupo de comunidad](/help/communities/tools-groups.md), y [funciones de comunidad](/help/communities/functions.md) solo se utilizan en el entorno de creación.

## Requisitos previos {#prerequisites}

Antes de crear un sitio de la comunidad, es *obligatorio* hasta:

* Asegúrese de que se estén ejecutando una o más instancias de publicación.
* Habilite la [servicio túnel](/help/communities/deploy-communities.md#tunnel-service-on-author) para administrar miembros y grupos de miembros.
* Identificar el [editor principal](/help/communities/deploy-communities.md#primary-publisher).
* [Configurar replicación](/help/communities/deploy-communities.md#replication-agents-on-author) cuando el puerto del editor principal no es el predeterminado (4503).

La práctica recomendada, para asegurarse de que el sitio está preparado para admitir muchas funciones, es seguir los siguientes pasos:

* Instale el [último paquete de funciones](/help/communities/deploy-communities.md#latestfeaturepack).
* Activar [Adobe Analytics](/help/communities/analytics.md) para AEM Communities.
* Configurar [email](/help/communities/email.md)
* Identificar [Administradores de comunidad](/help/communities/users.md#creating-community-members).
* [Habilitar el controlador OAuth](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler) para el inicio de sesión social.

## Acceder a la consola Sitios de Communities {#accessing-communities-sites-console}

En el entorno Autor, para llegar a la consola Sitios de Communities:

* Desde la navegación global: **[!UICONTROL Communities]** > **[!UICONTROL Sites]**

La consola Sitios de comunidades muestra todos los sitios de la comunidad existentes. Desde esta consola, se pueden crear, editar, administrar y eliminar sitios de la comunidad.

Para crear un sitio de la comunidad, seleccione la **Crear** icono.

Para acceder a un sitio de la comunidad existente para crear, modificar, publicar, exportar o agregar un grupo anidado, seleccione el icono de carpeta del sitio.

## Creación del sitio {#site-creation}

La consola de creación de sitios proporciona un enfoque paso a paso para ensamblar las características del sitio en función de un elemento seleccionado [plantilla del sitio de la comunidad](/help/communities/sites.md) Configuración de y.

Todos los sitios creados incluyen una función de inicio de sesión, ya que los visitantes del sitio deben iniciar sesión antes de poder publicar contenido, enviar mensajes o participar en un grupo. Otras funciones incluidas son los perfiles de usuario, los mensajes, las notificaciones, el menú del sitio, la búsqueda, el establecimiento de temas y la marca.

El proceso se inicia seleccionando la variable `Create` en la parte superior de la consola Sitios de Communities.

El proceso de creación es una serie de pasos que se presentan como paneles que contienen un conjunto de funciones que se van a configurar (presentadas como subpaneles). Es posible pasar a la sección **Siguiente** paso o **Atrás** Vaya al paso anterior antes de comprometer el sitio en el paso final.

### Paso 1: Plantilla del sitio {#step-site-template}

![newsitetemplate](assets/newsitetemplate.png)

En el panel Plantilla del sitio, se especifican el Título, la Descripción, la Raíz del sitio, el Idioma base, el Nombre y la Plantilla del sitio:

* **Título del sitio de comunidad**

  Un título para mostrar para el sitio.

  El título aparece en el sitio publicado y en la interfaz de usuario de administración del sitio.

* **Descripción del sitio de comunidad**

  Una descripción del sitio.

  La descripción no aparece en el sitio publicado.

* **Raíz del sitio de comunidad**

  Ruta raíz al sitio.

  La raíz predeterminada es `/content/sites`, pero la raíz se puede mover a cualquier ubicación dentro del sitio web.

* **Idioma base del sitio de la comunidad**

  (No tocar para un solo idioma: Inglés) Utilice el menú desplegable para elegir uno *o más* idiomas base de los idiomas disponibles: alemán, italiano, francés, japonés, español, portugués (Brasil), chino (tradicional) y chino (simplificado). Se crea un sitio de comunidad para cada idioma agregado y existe en la misma carpeta de sitio según la práctica recomendada descrita en [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md). La página raíz de cada sitio contiene una página secundaria denominada por el código de idioma de uno de los idiomas seleccionados, como &quot;en&quot; para inglés o &quot;fr&quot; para francés.

* **Nombre del sitio de comunidad**:

  Nombre de la página raíz del sitio que aparece en la dirección URL.

   * Compruebe el nombre, ya que no se cambia fácilmente después de crear el sitio.
   * La dirección URL base ( `https://server:port/site root/site name)` se muestra debajo de `Community Site Name`.

   * Para una URL válida, añada un código de idioma base + &quot;.html&quot;

     *Por ejemplo*, `https://localhost:4502/content/sites/mysight/en.html`

* **Plantilla del sitio de comunidad** menú

  Utilice el menú desplegable para elegir un disponible [plantilla del sitio de la comunidad](/help/communities/tools.md).

* Seleccione **Siguiente**.

### Paso 2: Diseño {#step-design}

El panel Diseño contiene dos subpaneles para seleccionar el tema y el titular de la marca:

#### TEMA DEL SITIO DE LA COMUNIDAD {#community-site-theme}

![tema del sitio](assets/sitetheme.png)

El marco de trabajo utiliza `Twitter Bootstrap` para llevar un diseño flexible y adaptable al sitio. Se puede seleccionar una de las muchas temáticas del Bootstrap precargadas para aplicar estilo a la plantilla del sitio de la comunidad seleccionada o se puede cargar una temática del Bootstrap.

Cuando se selecciona, la temática se superpone con una marca de verificación azul opaca.

Una vez publicado el sitio de la comunidad, es posible [editar las propiedades](#modifying-site-properties) y seleccione una temática diferente.

#### MARCA DEL SITIO DE LA COMUNIDAD {#community-site-branding}

![promoción de la marca en el sitio](assets/site-branding.png)

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
>La convención es para publicación [usuarios y grupos de usuarios](/help/communities/users.md) (miembros y grupos de miembros) para que no se dupliquen en el entorno de creación.
>
>Por lo tanto, al crear el sitio de la comunidad en el entorno de creación y asignar miembros de confianza a diversas funciones, es necesario recuperar datos de miembros del entorno de publicación.
>
>Esto se logra habilitando la variable ` [AEM Communities Publish Tunnel Service](/help/communities/deploy-communities.md#tunnel-service-on-author)` para el entorno de creación.

#### USER MANAGEMENT {#user-management}

![createsitesettings](assets/createsitesettings.png)

* **Permitir el registro de usuarios**

  Si se selecciona, los visitantes del sitio pueden convertirse en miembros de la comunidad mediante el registro automático.
Si no se selecciona, el sitio de la comunidad es *restringido* y los visitantes del sitio deben estar asignados al grupo de miembros del sitio de la comunidad, realizar una solicitud o recibir una invitación por correo electrónico. Si no se selecciona, no se debe permitir el acceso anónimo.
Desmarque para un *privado* sitio de la comunidad. La opción predeterminada está activada.

* **Permitir acceso anónimo**

  Si se selecciona, el sitio de la comunidad es *open* y cualquier visitante del sitio puede acceder al sitio.
Si no se selecciona, solo los miembros que han iniciado sesión pueden acceder al sitio.
Desmarque para un *privado* sitio de la comunidad. La opción predeterminada está activada.

* **Permitir mensajes**

  Si esta opción está activada, los miembros pueden enviarse mensajes entre sí y al grupo dentro del sitio de la comunidad.
Si no se selecciona, la mensajería no está configurada para la comunidad.
El valor predeterminado está desmarcado.

* **Permitir inicios de sesión sociales: Facebook**

  Si se selecciona, permita que los visitantes del sitio inicien sesión con las credenciales de su cuenta de Facebook. El seleccionado [Configuración de nube de facebook](/help/communities/social-login.md#create-a-facebook-connect-cloud-service) debe configurarse para agregar usuarios al grupo de miembros del sitio de la comunidad una vez creado el sitio de la comunidad.
Si no se selecciona, no se muestra ningún inicio de sesión de Facebook.
Dejar sin marcar para ver un *privado* sitio de la comunidad. El valor predeterminado está desmarcado.

* **Permitir inicios de sesión sociales: Twitter**

  Si se selecciona, permita que los visitantes del sitio inicien sesión con las credenciales de su cuenta de Twitter. El seleccionado [configuración de nube de twitter](/help/communities/social-login.md#create-a-twitter-connect-cloud-service) debe configurarse para agregar usuarios al grupo de miembros del sitio de la comunidad una vez creado el sitio de la comunidad.
Si no se selecciona, no se muestra ningún inicio de sesión de Twitter.
Dejar sin marcar para ver un *privado* sitio de la comunidad. El valor predeterminado está desmarcado.

>[!NOTE]
>
>**Permitir inicios de sesión sociales**
>
>Aunque pueden existir configuraciones de Twitter y Facebook de muestra que se pueden seleccionar para una [entorno de producción](/help/sites-administering/production-ready.md), es necesario crear aplicaciones de Twitter y Facebook personalizadas. Consulte [Inicio de sesión social con Facebook y Twitter](/help/communities/social-login.md).

#### ETIQUETADO {#tagging}

![etiquetado de sitios](assets/site-tagging.png)

Las etiquetas, que se pueden aplicar al contenido de la comunidad, se controlan seleccionando Espacios de nombres de etiqueta definidos anteriormente a través de la variable [Consola de etiquetado](/help/sites-administering/tags.md#tagging-console).

Además, la selección de áreas de nombres de etiquetas para el sitio de la comunidad limita la selección presentada al definir catálogos y recursos.

* cuadro de búsqueda de texto: empiece a escribir para identificar las etiquetas que se pueden utilizar en el sitio.

#### ROLES {#roles}

![Funciones de comunidad](assets/site-admin-2.png)

El [funciones de los miembros de la comunidad](/help/communities/users.md) tienen asignada esta configuración.

Encontrar miembros de la comunidad es fácil mediante la búsqueda anticipada.

* **Administradores de la comunidad**

  Empiece a escribir para seleccionar uno o más miembros de la comunidad o grupos de miembros que puedan administrar miembros de la comunidad y grupos de miembros.

* **Moderadores de comunidad**

  Empiece a escribir para seleccionar uno o varios miembros de la comunidad o grupos de miembros en los que se debe confiar como moderadores del contenido generado por el usuario.

* **Miembros privilegiados de la comunidad**

  Empiece a escribir para seleccionar uno o varios miembros de la comunidad o grupos de miembros a los que se les dará la capacidad de crear contenido cuando `Allow Privileged Member` se ha seleccionado para una [función comunitaria](/help/communities/functions.md).

* **Administradores de comunidad**

  Empiece a escribir para seleccionar uno o varios administradores del sitio que puedan administrar la estructura del sitio independientemente de otros administradores del sitio y del administrador de la comunidad predeterminado. Pueden crear grupos en cualquier nivel de la jerarquía y convertirse en el administrador predeterminado de los grupos anidados (pero más tarde se pueden eliminar de la función de administrador de los grupos anidados).

#### MODERACIÓN {#moderation}

![moderación del sitio](assets/site-moderation.png)

La configuración global para moderar el contenido generado por el usuario (UGC) está controlada por esta configuración. Los componentes individuales tienen ajustes adicionales para controlar la moderación.

* **Contenido con moderación previa**

  Si se selecciona, el contenido publicado en la comunidad no aparece hasta que lo apruebe un moderador. El valor predeterminado está desmarcado. Para obtener más información, consulte [Moderar contenido de la comunidad](/help/communities/moderate-ugc.md#premoderation).

* **Umbral de indicación antes de ocultar el contenido**

  Si es mayor que 0, el número de veces que se debe marcar un tema o una publicación antes de ocultarlo de la vista pública. Si se establece en -1, el tema o la publicación marcados nunca se ocultarán de la vista pública. El valor predeterminado es 5.

#### ANALYTICS {#analytics}

![site-analytics](assets/site-analytics.png)

* **Habilitar Analytics**

  Solo está disponible cuando Adobe Analytics se ha [configurado](/help/communities/analytics.md) para las funciones de Communities.
El valor predeterminado está desmarcado. Cuando se selecciona, aparece un menú de selección adicional:

![site-analytics-enable](assets/site-analytics-enable.png)

* **Referencia del marco de configuración de nube**

  En el menú desplegable, seleccione el marco de servicio de Analytics Cloud configurado para este sitio de la comunidad.
  `Communities` es el ejemplo de módulo de [Configuración de Analytics para funciones de Communities](/help/communities/analytics.md#aem-analytics-framework-configuration) documentación.

#### TRADUCCIÓN {#translation}

![traducción del sitio](assets/site-translation.png)

* **Permitir traducción automática**

  Cuando se selecciona (la opción predeterminada está desactivada), la traducción automática está habilitada para UGC dentro del sitio. Esto no afecta a ningún otro contenido, como el contenido de la página, aunque el sitio esté configurado como multilingüe. Consulte [Traducción del contenido generado por el usuario](/help/communities/translate-ugc.md) para obtener información sobre la configuración de un servicio de traducción con licencia para AEM Communities. Consulte [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md) para obtener una descripción general completa.

![allow-machine-translation](assets/allow-machine-translation.png)

* **Habilitar la traducción automática para los idiomas seleccionados**

  Los idiomas habilitados para la traducción automática tienen de forma predeterminada la configuración del sistema especificada por el [configuración de integración de traducción](/help/communities/translate-ugc.md#translation-integration-configuration). Esta configuración predeterminada se puede sobrescribir para este sitio eliminando los valores predeterminados o seleccionando otros idiomas en el menú desplegable.

* **Elija un proveedor de traducción**

  De forma predeterminada, el proveedor de servicios es un servicio de prueba que utiliza `microsoft` solo para demostración. Si no hay ningún proveedor de servicios de traducción con licencia, **Permitir traducción automática** debe estar desmarcada.

* **Elegir un almacén compartido global**

  Para un sitio web con varias copias de idioma, un almacén compartido global proporciona un único hilo de conversación, visible desde cada copia de idioma. Esto se logra seleccionando uno de los idiomas incluidos como copia de idioma. El valor predeterminado es *No hay almacén compartido global*.

* **Elegir configuración del proveedor de traducción**

  Elija una [marco de integración de traducción](/help/sites-administering/tc-tic.md) creado para el proveedor de traducción con licencia.

* **Seleccione las opciones de traducción del sitio de la comunidad**

   * **Traducir toda la página**

     Si se selecciona, todos los UGC de una página se traducen al idioma base de la página.

     El valor predeterminado es *no seleccionado*.

   * **Traducir solo la selección**

     Si se selecciona, aparece una opción de traducción junto a cada entrada que permite traducir entradas individuales al idioma base de la página.
El valor predeterminado es *seleccionado*.

* **Seleccionar opciones de persistencia**

   * **Traducir las contribuciones a petición del usuario y continuar posteriormente**
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

Si es necesario realizar algún ajuste, utilice el **Atrás** para hacerlas.

Una **Crear** está seleccionado e iniciado, el proceso de creación del sitio no se puede interrumpir.

Una vez creado el sitio:

* No se admite el cambio de la dirección URL (nombre de nodo).
* Los cambios futuros en la plantilla del sitio de la comunidad no afectan al sitio de la comunidad creado.
* La deshabilitación de la plantilla del sitio de la comunidad no afecta al sitio de la comunidad creado.
* Es posible editar la variable [ESTRUCTURA](#modify-structure) de un sitio de la comunidad modificando sus propiedades.

![create-site](assets/create-site1.png)

Cuando finaliza el proceso, la carpeta del nuevo sitio se muestra en la consola Sitios de Communities, desde donde los autores pueden agregar contenido de página o los administradores pueden modificar las propiedades del sitio.

![modify-site-property](assets/modify-site-property.png)

Para editar un sitio de la comunidad, seleccione su carpeta de proyecto para abrirlo:

![sitio-proyecto](assets/site-project.png)

Al pasar el ratón por encima de un sitio o tocar una tarjeta del sitio, aparecen iconos que permiten lo siguiente:

* [edición del sitio en modo de autor](#authoring-site-content)
* [abrir las propiedades del sitio para modificarlas](#modifying-site-properties)
* [publicación del sitio](#publishing-the-site)
* [exportación del sitio](#exporting-the-site)
* [eliminar el sitio](#deleting-the-site)

## Creación de contenido del sitio {#authoring-site-content}

AEM El contenido de un sitio puede crearse con las mismas herramientas que cualquier otro sitio web de la. Para abrir el sitio para la creación, seleccione la `Open Site` que aparece al pasar el ratón por el sitio. El sitio se abre en una nueva ficha de forma que la consola Sitios de Communities permanece accesible.

![site-content](assets/site-content.png)

>[!NOTE]
>
>AEM Si no está familiarizado con el uso de la, consulte la documentación de en [manipulación básica](/help/sites-authoring/basic-handling.md) y una [guía rápida para la creación de páginas](/help/sites-authoring/qg-page-authoring.md).

## Modificación de propiedades del sitio {#modifying-site-properties}

![edit-site](assets/edit-site.png)

Las propiedades de un sitio existente, especificadas durante el proceso de creación del sitio, se pueden modificar seleccionando el `Edit Site`que aparece al pasar el ratón por el sitio.

`Details of the following properties match the descriptions provided in the` [Creación del sitio](#site-creation) sección.

![modify-site-basicinfo](assets/modify-site-basicinfo.png)

### Modificar básico {#modify-basic}

El panel BÁSICO permite modificar lo siguiente:

* Título del sitio de la comunidad
* Descripción del sitio de la comunidad

El nombre del sitio de la comunidad no se puede modificar.

Elegir una plantilla de sitio de comunidad diferente no tendría ningún efecto en un sitio de comunidad existente, ya que no queda ninguna conexión entre las plantillas y los sitios.

En su lugar, la variable [ESTRUCTURA](#modify-structure) del sitio de la comunidad puede modificarse.

### Modificar estructura {#modify-structure}

El panel ESTRUCTURA permite modificar la estructura creada inicialmente a partir de la plantilla de sitio de la comunidad seleccionada. Desde el panel, es posible:

* Arrastrar y soltar elementos adicionales [funciones de comunidad](/help/communities/functions.md) en la estructura del sitio.
* En una instancia de una función de comunidad en la estructura del sitio:

   * **`gear icon`**

     Editar la configuración, incluidos el título para mostrar y el nombre de la URL, y [grupos de miembros privilegiados](/help/communities/users.md#privilegedmembersgroups).

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
>La función de grupos debe *no* ser el *primero ni el único* función en la estructura del sitio.
>
>Cualquier otra función, como la [función de página](/help/communities/functions.md#page-function), debe incluirse y enumerarse primero.

#### Ejemplo : Agregar una función de catálogo a una estructura de sitio de la comunidad {#example-adding-a-catalog-function-to-a-community-site-structure}

![add-catalog-site](assets/add-catalog-site.png)

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

Una vez que se ha creado o modificado un sitio de la comunidad, es posible publicarlo (activarlo) seleccionando la variable `Publish Site` que aparece al pasar el ratón por encima del sitio.

![publish-site](assets/publish-site.png)

Hay una indicación después de que el sitio se publique correctamente.

![publicado en el sitio](assets/site-published.png)

### Publicación con grupos anidados {#publishing-with-nested-groups}

Después de publicar un sitio de comunidad, es necesario publicar individualmente cada subcomunidad (grupo anidado) creada con el [Consola de grupos](/help/communities/groups.md).

## Exportación del sitio {#exporting-the-site}

![export-site](assets/export-site.png)

Seleccione el icono de exportación, al pasar el ratón sobre el sitio, para poder crear un paquete del sitio de la comunidad que esté almacenado en el [Administrador de paquetes](/help/sites-administering/package-manager.md) y descargado.

UGC no está incluido en el paquete del sitio.

## Eliminación del sitio {#deleting-the-site}

![deleteicon](assets/deleteicon.png)

Para eliminar el sitio de la comunidad, seleccione el icono Eliminar sitio que aparece al pasar el ratón por encima del sitio en la Consola del sitio de Communities. Esta acción elimina todos los elementos asociados con el sitio, como UGC, grupos de usuarios, recursos y registros de bases de datos.

## Grupos de usuarios de la comunidad creados {#created-community-user-groups}

Una vez publicado el nuevo sitio de la comunidad, se crean nuevos grupos de miembros (grupos de usuarios en el entorno de publicación) que tienen los permisos adecuados establecidos para diversas funciones administrativas y de miembro.

El nombre creado para los grupos de miembros incluye el *site-name* dado en [Paso 1](#step13asitetemplate) (el nombre que aparece en la dirección URL). También incluye un ID único para evitar conflictos con los sitios y grupos de la comunidad que tienen el mismo nombre de sitio para diferentes raíces de sitio de la comunidad.

Por ejemplo: si los nombres fueran &quot;participación&quot; para un sitio titulado &quot;Tutorial de introducción&quot;, el grupo de usuarios para moderadores sería:

* title: Moderadores de participación de la comunidad
* nombre: community-*enganchar-uid*-moderadores

Los miembros que tengan asignadas funciones como moderadores o administradores de grupos al crear el sitio se asignan al grupo correspondiente y se asignan al grupo de miembros. Estos grupos y asignaciones de miembros se crean al publicar el nuevo sitio.

Para obtener más información, consulte [Administración de usuarios y grupos de usuarios](/help/communities/users.md).

>[!NOTE]
>
>If [Permitir inicio de sesión social: Facebook](#user-management) está habilitado, una vez que el grupo de usuarios `community-<site-name>-<uid>-members`
>se crea, se aplica el [Facebook Cloud Service](/help/communities/social-login.md#createafacebookcloudservice) debe configurarse para agregar usuarios a este grupo.

## Configurar para error de autenticación {#configure-for-authentication-error}

De forma predeterminada, un sitio de la comunidad redirige a una página de inicio de sesión de ejemplo cuando el usuario introduce credenciales incorrectas y no puede iniciar sesión. Este inicio de sesión de muestra no está presente en un [servidor de producción](/help/sites-administering/production-ready.md).

Para redirigir correctamente, una vez que se ha configurado un sitio y se ha insertado para publicarlo, complete estos pasos para obtener el error de autenticación para redirigir al sitio de la comunidad:

* AEM En cada instancia de publicación de la.
* Iniciar sesión con privilegios de administrador.
* Acceda a la [Consola web](/help/sites-deploying/configuring-osgi.md).

   * Por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

* Localizar `Adobe Granite Login Selector Authentication Handler`.
* Seleccione el `pencil` para poder abrir la configuración y editarla.
* Introduzca una **Asignaciones de página de inicio de sesión** como sigue:

  `/content/sites/<site-name>/path/to/login/page:/content/sites/<site-name>`

  Por ejemplo:
  `/content/sites/engage/en/signin:/content/sites/engage/en`

* Seleccione **Guardar**.

![auth-error](assets/auth-error.png)

### Probar redirección de autenticación {#test-authentication-redirection}

AEM En la misma instancia de publicación de configurada con una asignación de página de inicio de sesión para el sitio de la comunidad:

* Vaya a la página de inicio del sitio de la comunidad.

   * Por ejemplo, [https://localhost:4503/content/sites/engage/en.html](https://localhost:4503/content/sites/engage/en.html)

* Seleccione Cerrar sesión.
* Seleccione Iniciar sesión.
* Introduzca credenciales incorrectas, como el nombre de usuario &quot;x&quot; y la contraseña &quot;x&quot;.
* La página de inicio de sesión debe mostrarse con el error &quot;inicio de sesión no válido&quot;.

![test-authentication](assets/test-authentication.png)

## Acceder a los sitios de la comunidad desde la consola Sitios principales {#accessing-community-sites-from-main-sites-console}

Desde la consola Sitios de navegación global, los sitios de la comunidad se encuentran en la variable `Community Sites` carpeta.

Aunque es posible acceder a un sitio de la comunidad de esta manera, para tareas administrativas, se debe acceder al sitio de la comunidad desde la consola Sitios de comunidades.

![access-site](assets/access-site.png)
