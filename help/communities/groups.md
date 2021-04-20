---
title: Consola de grupos de la comunidad
seo-title: Consola de grupos de la comunidad
description: La consola Grupos permite crear grupos de la comunidad
seo-description: La consola Grupos permite crear grupos de la comunidad
uuid: 21e2bde3-7354-4193-bcb3-c672c6342252
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d381ea40-fe49-4d32-bfad-1379c7a02aba
docset: aem65
pagetitle: Community Groups Console
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1679'
ht-degree: 2%

---


# Consola de grupos de la comunidad {#community-groups-console}

La consola Grupos proporciona acceso a la creación de grupos de la comunidad cuando la [estructura de plantilla](/help/communities/sites-console.md#step1) de un sitio de la comunidad incluye la [función de grupos](/help/communities/functions.md#groups-function).

* AEM Communities permite anidar grupos dentro de otros grupos. El anidado de grupos es posible cuando la [estructura del nuevo grupo](/help/communities/tools-groups.md) contiene la función de grupos.
* Solo para el entorno de creación, hay un asistente de creación de grupos similar al asistente de creación de sitios.
* Tanto si los miembros pueden crear grupos en el entorno de publicación como si no, se puede configurar al agregar una función Grupos a una estructura de sitio de la comunidad o de grupo de la comunidad.

De las tres plantillas de grupo incluidas, solo la plantilla `Reference Group` incluye una función de grupo en su estructura.

Las diferentes facetas de los grupos comunitarios son:

* **Creación**: se puede crear un nuevo grupo en el autor y, opcionalmente, en la instancia de publicación.
* **Control**: puede ser abierto o secreto.
* **Anidado**: puede contener cero o más grupos.

<!-- This is a 404 on helpx. Please update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), will not be listed in the Community Groups console, and thus, are not modifiable using the console.
-->

>[!NOTE]
>
>Esta consola Grupos , a la que solo se puede acceder desde la consola Sitios de Communities, no se debe confundir con el miembro [Consola de Grupos](/help/communities/members.md) para administrar los grupos de miembros.
>
>Los grupos de miembros son grupos de usuarios registrados en el entorno de publicación a los que se accede desde el entorno de creación mediante el [servicio de túnel](/help/communities/deploy-communities.md#tunnel-service-on-author).

## Creación de grupos {#group-creation}

Para acceder a la consola Grupos :

* En el autor, inicie sesión con privilegios de administrador.
* Desde la navegación global: **[!UICONTROL Comunidades]** > **[!UICONTROL Sitios]**.
* Seleccione una carpeta de sitio de la comunidad existente para abrirla.
* Seleccione una instancia de un sitio de comunidad dentro de la carpeta .

   * La estructura del sitio de la comunidad debe incluir una función de grupo.
   * Estas capturas de pantalla proceden del tutorial Introducción después de [crear grupos en publish](/help/communities/published-site.md).

   ![create-group](assets/create-group.png)

* Seleccione la **Groups folder** para abrirla.

   Cuando se abren, se muestran todos los grupos existentes, tanto si se crean en el autor como en la publicación.

   Desde esta consola Grupos es posible crear nuevos grupos.

   ![create-new-group](assets/create-new-group.png)

* Seleccione el botón **Crear grupo**.

### Paso 1: Plantilla de grupo de la comunidad {#step-community-group-template}

![Grupos de comunidades multilingües](assets/multi-lingual-group.png)

* **Título del grupo de la comunidad**

   Un título para mostrar para el grupo.
El título aparece en el sitio publicado para el grupo.

* **Descripción del grupo de la comunidad**

   Descripción del grupo.

* **Raíz de grupo de la comunidad**

   Ruta raíz al grupo.
La raíz predeterminada es el sitio principal, pero la raíz se puede mover a cualquier ubicación dentro del sitio web. No se recomienda cambiarlo.

* **Menú Idiomas de grupo de la comunidad disponibles adicionales** 

   Utilice la lista desplegable para seleccionar los idiomas de grupo de comunidad disponibles. El menú muestra todos los idiomas en los que se crea el sitio de la comunidad principal. Los usuarios pueden seleccionar entre estos idiomas para crear grupos en varias configuraciones regionales en este solo paso. El mismo grupo se crea en varios idiomas especificados en la consola Grupos de los respectivos sitios de la comunidad.

* **Nombre del grupo de la comunidad**

   Nombre de la página raíz del grupo que aparece en la dirección URL.

   * Vuelva a comprobar el nombre porque no es fácil cambiarlo después de crear el grupo.
   * La dirección URL base se muestra debajo de `Community Group Name`.
   * Para una dirección URL válida, añada &quot;.html&quot;
      *por ejemplo*,  `https://localhost:4502/content/sites/mysight/en/mygroup.html`.

* **Grupo de la comunidad** Templatemenu

   Utilice la lista desplegable para elegir una [plantilla de grupo de comunidad](/help/communities/tools.md) disponible.

### Paso 2: Diseño {#step-design}

### TEMA {#community-group-theme} DEL GRUPO DE LA COMUNIDAD

![communitygrouptheme](assets/communitygrouptheme.png)

El marco utiliza [Twitter Bootstrap](https://twitterbootstrap.org/) para llevar un diseño flexible y adaptable al sitio. Se puede seleccionar uno de los muchos temas del Bootstrap precargados para que tengan un estilo con la plantilla de grupo de comunidad seleccionada, o se puede cargar un tema del Bootstrap.

Cuando se selecciona, el tema se superpone con una marca de verificación azul opaco.

Es posible seleccionar un tema que difiera del tema del sitio principal.

Una vez publicado el sitio de la comunidad, es posible [editar las propiedades](#modifyinggroupproperties) y seleccionar un tema diferente.

### MARCA DE GRUPO DE LA COMUNIDAD {#community-group-branding}

![marca de grupo de la comunidad](assets/community-group-branding.png)

La marca del sitio de la comunidad es una imagen que se muestra como un encabezado en la parte superior de cada página. Es posible mostrar un banner para el grupo que difiera de otras páginas del sitio.

El tamaño de la imagen debe ser tan grande como la visualización esperada de la página en el explorador y 120 píxeles de altura.

Al crear o seleccionar una imagen, tenga en cuenta:

* La altura de la imagen se recortará a 120 píxeles medidos desde el borde superior de la imagen
* La imagen se fija en el borde izquierdo de la ventana del explorador
* No hay cambio de tamaño de la imagen, por lo que cuando el ancho de la imagen es:

   * Menos que el ancho del explorador, la imagen se repetirá horizontalmente.
   * Buena que la anchura del explorador, la imagen parece recortarse.

### Paso 3: Configuración {#step-settings}

**MODERACIÓN**

![seleccionar funciones de miembro del grupo de la comunidad](assets/group-admin.png)

**Moderadores del grupo de la comunidad**

De forma predeterminada, se hereda la lista de moderadores del sitio de la comunidad principal.

Es posible añadir moderadores específicos al grupo. Busque miembros (del entorno de publicación) para agregarlos como moderadores

**Administradores de grupo**

De forma predeterminada, el administrador del sitio de la comunidad principal también es el administrador de los grupos.

Sin embargo, es posible asignar administradores de grupo independientes. Los administradores de grupos pueden administrar su grupo (por ejemplo, G1) y crear un subgrupo anidado en G1. También pueden asignar diferentes administradores para el subgrupo.

Por lo tanto, un usuario U1 puede ser administrador en un grupo G1 y un usuario normal en su grupo anidado G2.

**MIEMBROS**

La configuración de membresía permite seleccionar una de las tres formas de asegurar un grupo de comunidad.

![community-group-membership](assets/community-group-membership.png)

* **Suscripción opcional**

   Si se selecciona, el grupo de comunidad es un grupo público. Los miembros del sitio pueden participar en el grupo y publicar sin unirse explícitamente al grupo. El valor predeterminado está seleccionado.

* **Suscripción requerida**

   Si se selecciona, el grupo de comunidad es un grupo abierto. Los miembros del sitio de la comunidad pueden ver el contenido del grupo, pero necesitan unirse al grupo para publicar contenido. Los miembros se unen seleccionando el botón `Join` en el entorno de publicación. El valor predeterminado no está seleccionado.

* **Suscripción restringida**

   Si se selecciona, el grupo de comunidad es un grupo secreto. Los miembros de la comunidad deben ser invitados explícitamente. Los miembros invitados se introducen en el cuadro de búsqueda. Los miembros se pueden agregar posteriormente utilizando las [consolas Miembros y Grupos](/help/communities/members.md) en el entorno de creación. El valor predeterminado no está seleccionado.

**MINIATURA**

![community-group-thumbnail](assets/community-group-thumbnail.png)

La miniatura es una imagen que se mostrará para el grupo al crear y publicar.

El tamaño óptimo de una imagen de grupo es de 170 x 90 píxeles en un formato de imagen compatible (como JPG o PNG).

Si no se añade ninguna imagen, se muestra una imagen predeterminada.

![thumbnail-image](assets/thumbnail-image.png)

### Paso 4: Crear grupo {#step-create-group}

![community-create-group](assets/community-create-group.png)

Si es necesario realizar algún ajuste, utilice el botón **Back** para hacerlo.

Una vez que **Create** está seleccionado e iniciado, no se puede interrumpir el proceso de creación del grupo.

Cuando el proceso termina, la tarjeta del nuevo sitio de la subcomunidad (grupo) se muestra en la consola Grupos de sitios de Communities, desde donde los autores pueden agregar contenido de página o los administradores pueden modificar las propiedades del sitio.

![crear grupo de la comunidad](assets/create-community-groups.png)

>[!NOTE]
>
>El grupo se crea en todos los idiomas, tal como se especifica en el [paso 1: Plantilla de grupo de la comunidad](/help/communities/groups.md#step-community-group-template) en idiomas de grupo de la comunidad disponibles adicionales, en la consola Grupos de la comunidad de los sitios de la comunidad respectivos.

## Contenido del grupo de creación {#author-group-content}

![open-site](assets/open-site.png)

El contenido de la página de un grupo se puede crear con las mismas herramientas que cualquier otra página AEM. Para abrir el grupo para la creación, seleccione el icono Abrir sitio que aparece al pasar el ratón por encima de la tarjeta del grupo.

## Modificar propiedades de grupo {#modify-group-properties}

Las propiedades de un sitio de subcomunidad existente, especificadas durante el proceso de creación del grupo de comunidad, se pueden modificar seleccionando el icono Editar sitio que aparece al pasar el ratón por encima de la tarjeta del grupo:

![editar-sitio](assets/edit-site.png)

Los detalles de las siguientes propiedades coinciden con las descripciones proporcionadas en la sección [Creación de grupos](#group-creation). Se puede modificar cualquier grupo anidado, tanto si se crea en el entorno de publicación como en el entorno de creación.

![community-group-basic](assets/community-group-basic.png)

### Modificar básico {#modify-basic}

El panel BASIC permite la modificación de

* Título del grupo de la comunidad
* Descripción del grupo de la comunidad

El nombre del grupo comunitario no podrá modificarse.

Elegir una plantilla de grupo de comunidad diferente no tendría ningún efecto en un sitio de grupo de comunidad existente, ya que no queda ninguna conexión entre plantillas y sitios.

En su lugar, se puede modificar la [ESTRUCTURA](#modify-structure) de la subcomunidad.

### Modificar estructura {#modify-structure}

El panel ESTRUCTURA permite modificar la estructura creada inicialmente a partir de la plantilla de grupo de comunidad seleccionada al crear el sitio de subcomunidad desde el entorno de creación o publicación. Desde el panel, es posible:

* Arrastre y suelte [funciones de comunidad](/help/communities/functions.md) adicionales en la estructura del sitio.
* En una instancia de una función de comunidad en la estructura del sitio:

   * **`Gear icon`**
Edite la configuración, que incluye el título de visualización, la dirección URL y los grupos de miembros  [con privilegios](/help/communities/users.md#privilegedmembersgroups).

   * **`Trashcan icon`**
Quitar (eliminar) funciones de la estructura del sitio.

   * **`Grid icon`**
Modifique el orden de las funciones tal y como se muestra en la barra de navegación de nivel superior del sitio.

>[!CAUTION]
>
>Aunque el título de visualización se puede cambiar sin efectos secundarios, no se recomienda editar el nombre de la URL de una función de comunidad que pertenece a un sitio de comunidad.
>
>Por ejemplo, cambiar el nombre de la URL no moverá el UGC existente, lo que tendrá el efecto de &quot;perder&quot; UGC.

>[!CAUTION]
>
>La función de grupos debe *no* ser la *primera ni la única* de la estructura del sitio.
>
>Cualquier otra función, como la [función de página](/help/communities/functions.md#page-function), debe incluirse y enumerarse primero.

**Ejemplo: Adición de una función de calendario a una estructura de subcomunidad (grupo)**

![community-group-add-calendar](assets/community-group-add-calendar.png)

### Modificar diseño {#modify-design}

El panel DISEÑO permite la modificación del tema:

* [Tema del grupo de la comunidad](#community-group-theme)
* [Marca del grupo de la comunidad](#community-group-branding)

   * Desplácese hasta la parte inferior del panel para cambiar la imagen de marca.

### Modificar configuración {#modify-settings}

El panel CONFIGURACIÓN permite agregar [moderadores](#moderation) de la comunidad.

### Modificar pertenencia {#modify-membership}

El panel [MEMBERSHIP](#membership) solo es informativo. No es posible modificar el tipo de pertenencia a un grupo establecido, ya sea opcional, obligatoria o restringida.

### Modificar miniatura {#modify-thumbnail}

El panel [THUMBNAIL](#thumbnail) permite cargar una imagen para representar el grupo de la comunidad en los visitantes del sitio en el entorno de publicación, así como en la consola Grupos del sitio de Communities en el entorno de creación.

## Publicar el grupo {#publish-the-group}

![publish-site](assets/publish-site.png)

Después de crear o modificar un grupo de comunidad, es posible publicarlo (activarlo) seleccionando el icono `Publish Site`.

Una vez que el grupo se publique correctamente, aparecerá un mensaje:

![publicado en grupo](assets/group-published.png)

>[!CAUTION]
>
>El sitio de la comunidad principal y los grupos principales ya deberían haberse publicado.
>
>El sitio de la comunidad y los grupos anidados deberían publicarse de forma descendente.

## Eliminar el grupo {#delete-the-group}

![icono eliminar](assets/deleteicon.png)

Elimine un grupo de la consola Grupos de la comunidad seleccionando el icono Eliminar grupo , que aparece al pasar el ratón por encima del grupo.

Esto elimina todos los elementos asociados al grupo, por ejemplo, todo el contenido del grupo se elimina de forma permanente y las suscripciones de los usuarios se eliminan del sistema.
