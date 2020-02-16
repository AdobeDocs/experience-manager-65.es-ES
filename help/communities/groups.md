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
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Consola de grupos de la comunidad{#community-groups-console}

La consola Grupos proporciona acceso a la creación de grupos de comunidad cuando la estructura [de](/help/communities/sites-console.md#step1) plantilla de un sitio de comunidad incluye la función [](/help/communities/functions.md#groups-function)Grupos.

* Las comunidades AEM admiten la anidación de grupos dentro de otros grupos. El anidado de grupos es posible cuando la [estructura del nuevo grupo](/help/communities/tools-groups.md) contiene la función de grupos.
* Solo para el entorno de creación, existe un asistente para la creación de grupos similar al asistente para la creación de sitios.
* Si los miembros pueden o no crear grupos en el entorno de publicación, se puede configurar al agregar una función Grupos a una estructura de sitio de comunidad o de grupo de comunidad.

De las tres plantillas de grupo incluidas, solo la `Reference Group` plantilla incluye una función de grupo en su estructura.

Las diferentes facetas de los grupos comunitarios son:

* **Creación**: se puede crear un nuevo grupo en el autor y, opcionalmente, en la publicación
* **Control**: el grupo puede ser abierto o secreto
* **Anidado**: un grupo puede contener cero o más grupos

<!-- This is a 404 on helpx. Please update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), will not be listed in the Community Groups console, and thus, are not modifiable using the console.-->

>[!NOTE]
>
>Esta consola Grupos, a la que solo se puede acceder desde la consola Sitios de comunidades, no debe confundirse con la consola [](/help/communities/members.md) Grupos de miembros para administrar grupos de miembros.
>
>Los grupos de miembros son grupos de usuarios registrados en el entorno de publicación a los que se accede desde el entorno de creación mediante el servicio [de](/help/communities/deploy-communities.md#tunnel-service-on-author)túnel.

## Creación de grupos {#group-creation}

Para acceder a la consola Grupos:

* Al crear, inicie sesión con privilegios de administrador
* Desde la navegación global: **Comunidades, Sitios**
* Seleccione una carpeta de sitio de comunidad existente para abrirla
* Seleccione una instancia de un sitio de comunidad dentro de la carpeta

   * la estructura del sitio de la comunidad debe incluir una función de grupos
   * estas capturas de pantalla proceden del tutorial Introducción después de [crear grupos al publicar](/help/communities/published-site.md)

Seleccione la carpeta **** Grupos para abrirla.

Al abrirse, se muestran todos los grupos existentes, tanto si se han creado al crear como al publicar.

Desde esta consola Grupos, es posible crear nuevos grupos.

![chlimage_1-200](assets/chlimage_1-200.png)

* Seleccione el botón **Crear grupo** .

### Paso 1: Plantilla de grupo de comunidad {#step-community-group-template}

![Grupos comunitarios multilingües](assets/multi-lingual-group.png)

* **Título**del grupo de la comunidad: un título de visualización para el grupo.
El título aparece en el sitio publicado para el grupo.

* **Descripción** del grupo de la comunidad: una descripción del grupo.
* **Raíz**del grupo de la comunidad: la ruta raíz del grupo.
La raíz predeterminada es el sitio principal, pero la raíz se puede mover a cualquier ubicación dentro del sitio web. No se recomienda cambiarlo.

* ****** Menú Idiomas del grupo de la comunidad disponibles adicionales: **utilice la lista desplegable para seleccionar los idiomas de grupo de comunidad disponibles. El menú muestra todos los idiomas en los que se crea el sitio de comunidad principal. Los usuarios pueden seleccionar entre estos idiomas para crear grupos en varias configuraciones regionales en este solo paso. El mismo grupo se crea en varios idiomas especificados en la consola Grupos de los respectivos sitios de la comunidad.

* **Nombre** del grupo de la comunidad: el nombre de la página raíz del grupo que aparece en la dirección URL

   * compruebe dos veces el nombre, ya que no es fácil cambiarlo después de crear el grupo
   * la dirección URL base se mostrará debajo de la variable `Community Group Name`
   * para una dirección URL válida, anexe &quot;.html&quot;
      *por ejemplo*, `https://localhost:4502/content/sites/mysight/en/mygroup.html`

* **Menú Plantilla** de grupo de comunidad: utilice la lista desplegable para elegir una plantilla [de grupo de](/help/communities/tools.md)comunidad disponible.

### Paso 2: Diseño {#step-design}

#### COMMUNITY GROUP THEME {#community-group-theme}

El marco utiliza [Twitter Bootstrap](https://twitterbootstrap.org/) para llevar un diseño flexible y adaptable al sitio. Se puede seleccionar uno de los muchos temas precargados de Bootstrap para aplicar estilo a la plantilla de grupo de comunidad seleccionada o se puede cargar un tema de Bootstrap.

Cuando se selecciona, el tema se superpone con una marca de verificación azul opaca.

Es posible seleccionar un tema que difiera del tema del sitio principal.

Después de publicar el sitio de la comunidad, es posible [editar las propiedades](#modifyinggroupproperties) y seleccionar un tema diferente.

#### COMMUNITY GROUP BRANDING {#community-group-branding}

![chlimage_1-201](assets/chlimage_1-201.png)

La marca del sitio de la comunidad es una imagen que se muestra como encabezado en la parte superior de cada página. Es posible mostrar una pancarta para el grupo que difiera de otras páginas del sitio.

El tamaño de la imagen debe ser tan grande como la visualización esperada de la página en el navegador y 120 píxeles de altura.

Al crear o seleccionar una imagen, tenga en cuenta:

* La altura de la imagen se recortará a 120 píxeles medidos desde el borde superior de la imagen
* La imagen se fija en el borde izquierdo de la ventana del navegador
* No hay cambio de tamaño de la imagen, de modo que cuando el ancho de la imagen es:

   * menor que el ancho del navegador, la imagen se repetirá horizontalmente
   * mayor que la anchura del navegador, la imagen aparecerá recortada

### Paso 3:Configuración {#step-settings}

#### MODERATION {#moderation}

![seleccionar funciones de miembro del grupo de comunidad](assets/group-admin.png)

**Moderadores del grupo de la comunidad**

De forma predeterminada, se hereda la lista de moderadores del sitio de la comunidad principal.

Es posible agregar moderadores específicos al grupo. Busque miembros (desde el entorno de publicación) para agregarlos como moderadores

**Administradores de grupo**

De forma predeterminada, el administrador del sitio de la comunidad principal también es el administrador de los grupos.

Sin embargo, es posible asignar administradores de grupos independientes. Los administradores de grupos pueden administrar su grupo (por ejemplo, G1) y crear un subgrupo anidado en G1. Además, pueden asignar diferentes administradores para el subgrupo.

Por lo tanto, un usuario U1 puede ser administrador de un grupo G1 y un usuario normal de su grupo anidado G2.

#### MEMBERSHIP {#membership}

La configuración de pertenencia permite seleccionar una de las tres formas de asegurar un grupo de comunidad.

![chlimage_1-202](assets/chlimage_1-202.png)

* **Pertenencia** opcional Si se selecciona, el grupo de comunidad es un grupo público. Los miembros del sitio pueden participar en el grupo y publicar sin unirse explícitamente al grupo. Predeterminado está seleccionado.

* **Pertenencia** requerida Si se selecciona, el grupo de comunidad es un grupo abierto. Los miembros del sitio de la comunidad pueden ver el contenido del grupo, pero necesitan unirse al grupo para publicar contenido. Los miembros se unen seleccionando el `Join` botón en el entorno de publicación. El valor predeterminado no está seleccionado.

* **Pertenencia** restringida Si se selecciona, el grupo de comunidad es un grupo secreto. Los miembros de la comunidad deben ser invitados explícitamente. Los miembros invitados se introducen en el cuadro de búsqueda. Los miembros se pueden agregar más adelante mediante las consolas [Miembros y Grupos](/help/communities/members.md) del entorno de creación. El valor predeterminado no está seleccionado.

#### MINIATURA {#thumbnail}

![chlimage_1-203](assets/chlimage_1-203.png)

La miniatura es una imagen que se muestra para el grupo al crear y publicar.

El tamaño óptimo de una imagen de grupo es de 170 x 90 píxeles en un formato de imagen admitido (como JPG o PNG).

Si no se agrega ninguna imagen, se muestra una imagen predeterminada.

![chlimage_1-204](assets/chlimage_1-204.png)

### Paso 4: Crear grupo {#step-create-group}

![chlimage_1-205](assets/chlimage_1-205.png)

Si es necesario realizar algún ajuste, utilice el botón **Atrás **para realizarlo.

Una vez seleccionada la opción **Crear** e iniciada, el proceso de creación del grupo no se puede interrumpir.

Cuando se completa el proceso, la tarjeta para el nuevo sitio de subcomunidad (grupo) se muestra en la consola Grupos de sitios de comunidades, desde donde los autores pueden agregar contenido de página o los administradores pueden modificar las propiedades del sitio.

![crear grupo de comunidad](assets/create-community-groups.png)

>[!NOTE]
>
>El grupo se crea en todos los idiomas, tal como se especifica en el [paso 1: Plantilla](/help/communities/groups.md#step-community-group-template) de grupo de la comunidad en idiomas de grupo de la comunidad disponibles adicionales, en la consola Grupos de la comunidad de los sitios de la comunidad respectivos.

## Contenido del grupo de creación {#author-group-content}

![chlimage_1-205](assets/chlimage_1-206.png)

El contenido de página de un grupo se puede crear con las mismas herramientas que cualquier otra página de AEM. Para abrir el grupo para la creación, seleccione el icono Abrir sitio que aparece al pasar el ratón por encima de la tarjeta del grupo.

## Modificar propiedades del grupo {#modify-group-properties}

Las propiedades de un sitio de subcomunidad existente, especificadas durante el proceso de creación de grupos de comunidad, se pueden modificar seleccionando el icono Editar sitio que aparece al pasar el ratón por encima de la tarjeta de grupo:

![chlimage_1-207](assets/chlimage_1-207.png)

Los detalles de las siguientes propiedades coinciden con las descripciones proporcionadas en la sección Creación [de](#group-creation) grupos. Se puede modificar cualquier grupo anidado, tanto si se crea en el entorno de publicación como en el entorno de creación.

![chlimage_1-208](assets/chlimage_1-208.png)

### Modificar básico {#modify-basic}

El panel BASIC permite modificar

* Título del grupo de la comunidad
* Descripción del grupo de la comunidad

No se puede modificar el nombre del grupo de la comunidad.

La elección de una plantilla de grupo de comunidad diferente no afectaría a un sitio de grupo de comunidad existente, ya que no queda ninguna conexión entre plantillas y sitios.

En cambio, la [ESTRUCTURA](#modify-structure) de la subcomunidad puede modificarse.

### Modificar estructura {#modify-structure}

El panel ESTRUCTURA permite modificar la estructura creada inicialmente a partir de la plantilla de grupo de comunidad seleccionada al crear el sitio de subcomunidad desde el entorno de creación o publicación. Desde el panel, es posible

* Arrastrar y soltar funciones [de](/help/communities/functions.md) comunidad adicionales en la estructura del sitio
* En una instancia de una función de comunidad en la estructura del sitio:

   * **`Gear icon`**
Edite la configuración, incluidos el título para mostrar y el nombre de la dirección URL* y los grupos [de miembros](/help/communities/users.md#privilegedmembersgroups)privilegiados.

   * **`Trashcan icon`**
Quitar (eliminar) funciones de la estructura del sitio.

   * **`Grid icon`**
Modifique el orden de las funciones como se muestra en la barra de navegación de nivel superior del sitio.

>[!CAUTION]
>
>* Aunque el título de visualización se puede cambiar sin efectos secundarios, no se recomienda editar el nombre de la dirección URL de una función de comunidad que pertenece a un sitio de comunidad.
Por ejemplo, si se cambia el nombre de la URL, no se moverá el UGC existente, lo que tendrá el efecto de &#39;perder&#39; UGC.

>[!CAUTION]
La función de grupos *no debe ser la *primera ni la única* función de la estructura del sitio.
Cualquier otra función, como la función [de](/help/communities/functions.md#page-function)página, debe incluirse y enumerarse en primer lugar.

#### Ejemplo: Adición de una función de calendario a una estructura de subcomunidad (grupo) {#example-adding-a-calendar-function-to-a-sub-community-group-structure}

![chlimage_1-209](assets/chlimage_1-209.png)

### Modificar diseño {#modify-design}

El panel DISEÑO permite modificar el tema:

* [Tema del grupo de la comunidad](#community-group-theme)
* [Marca del grupo de la comunidad](#community-group-branding)

   * desplácese hasta la parte inferior del panel para cambiar la imagen de marca

### Modificar configuración {#modify-settings}

El panel CONFIGURACIÓN permite agregar [moderadores](#moderation)de comunidad.

### Modificar pertenencia {#modify-membership}

El panel [MIEMBROS](#membership) es meramente informativo. No es posible modificar el tipo de pertenencia a un grupo establecido, ya sea opcional, obligatoria o restringida.

### Modificar miniatura {#modify-thumbnail}

El panel [MINIATURAS](#thumbnail) permite cargar una imagen para representar el grupo de la comunidad a los visitantes del sitio en el entorno de publicación, así como en la consola Grupos del sitio de comunidades en el entorno de creación.

## Publicar el grupo {#publish-the-group}

![chlimage_1-210](assets/chlimage_1-210.png)

Una vez creado o modificado un grupo de comunidad, es posible publicar (activar) el grupo seleccionando el icono `Publish Site` .

Una vez que el grupo se haya publicado correctamente, aparecerá un mensaje:

![chlimage_1-211](assets/chlimage_1-211.png)

>[!CAUTION]
El sitio de la comunidad principal y los grupos principales ya deberían haberse publicado.
El sitio de la comunidad y los grupos anidados deberían publicarse de manera vertical.

## Eliminar el grupo {#delete-the-group}

![icono Eliminar]()

Para eliminar un grupo desde la consola Grupos de la comunidad, seleccione el icono Eliminar grupo, que aparece al pasar el ratón sobre el grupo.

Esto elimina todos los elementos asociados al grupo, por ejemplo, se elimina de forma permanente todo el contenido del grupo y se eliminan las pertenencias de los usuarios del sistema.
