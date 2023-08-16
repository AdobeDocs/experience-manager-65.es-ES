---
title: Consola de moderación
seo-title: Moderation Console
description: Cómo acceder a la consola de moderación
seo-description: How to access the Moderation console
uuid: d3b8a160-85b2-43f4-9891-5fafa8c48c5f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 404582ab-bb4c-4775-9ae3-17356d376dca
docset: aem65
role: Admin
exl-id: 829da16a-4083-43c1-857d-f2666b363bfc
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2041'
ht-degree: 4%

---

# Consola de moderación {#moderation-console}

En AEM Communities, de forma masiva [moderación de contenido de la comunidad](/help/communities/moderate-ugc.md) es posible desde los entornos de creación y publicación por parte de los administradores y moderadores de la comunidad (miembros de la comunidad de confianza asignados como moderadores).

También pueden actuar los administradores y los moderadores de la comunidad [moderación en contexto](/help/communities/in-context.md) en el entorno de publicación.

Una característica de todas las [sitios de la comunidad](/help/communities/sites-console.md) es un `Administration` elemento de menú disponible para los usuarios que inician sesión con privilegios administrativos. El `Administration` proporciona acceso a la consola de moderación.

Desde la consola de moderación, los administradores y los moderadores de la comunidad tendrán acceso a todo el contenido generado por el usuario (UGC) para el que tengan permiso de moderación. Si se permite moderar varios sitios, es posible ver las publicaciones de todos los sitios o filtrar por sitios de comunidades seleccionadas.

Para obtener información más detallada, visite [Administración de usuarios y grupos de usuarios](/help/communities/users.md).

La consola Moderación admite:

* Realización de tareas de moderación por lotes.
* Buscando UGC.
* Visualización de detalles de UGC.
* Se muestran detalles del autor de UGC.

Solo cuando se ha iniciado sesión como administrador o un miembro con ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`, pueden realizarse tareas de moderación.

## Acceso al entorno de publicación {#publish-environment-access}

El acceso a la consola de moderación desde un sitio publicado de la comunidad se realiza mediante un vínculo de administración que aparece cuando se inicia sesión con un moderador de la comunidad.

![publishweretail](assets/publishweretail.png)

Al seleccionar el vínculo Administration, aparece la consola Moderación:

![moderation-console-publish](assets/moderation-console-publish.png)

## Acceso al entorno de creación {#author-environment-access}

En el entorno de creación, para llegar a la consola de moderación

* En la navegación global, seleccione **[!UICONTROL Communities]** > **[!UICONTROL Moderación]**.

Solo cuando se ha iniciado sesión como administrador o como miembro con [permisos de moderador](/help/communities/in-context.md#identifyingtrustedmembers), se pueden realizar tareas de moderación. El único contenido de la comunidad que se muestra es el que el miembro que ha iniciado sesión puede moderar.

>[!NOTE]
>
>UGC desde el entorno de publicación solo será visible en el autor si el SRP elegido implementa un almacén común. Por ejemplo, de forma predeterminada, el almacenamiento es JSRP, que no es un almacén común para creación y publicación. Consulte [Almacenamiento de contenido de comunidad](/help/communities/working-with-srp.md).

![moderationconsoleauthor](assets/moderationconsoleauthor.png)

## IU de consola de moderación {#moderation-console-ui}

Dejando a un lado el carril izquierdo de navegación (que aparece en el autor, pero no en la publicación), la interfaz de usuario de la moderación tiene las siguientes áreas principales:

* **[Barra de navegación superior](#top-navigation-bar)**
* **[Barra de herramientas](#toolbar)**
* **[Área de contenido](#content-area)**

### Barra de navegación superior {#top-navigation-bar}

La barra de navegación superior es constante en todas las consolas. Para obtener más información, consulte [Gestión básica](/help/sites-authoring/basic-handling.md).

### Barra de herramientas {#toolbar}

La barra de herramientas, situada debajo de la barra de navegación superior, proporciona el siguiente interruptor de alternancia en el lado izquierdo:

* [Carril de filtro](/help/communities/moderation.md#filterrail)
abre un carril que permite elegir las propiedades en las que desea filtrar el contenido.

La barra de herramientas, situada debajo de la barra de navegación superior, proporciona el siguiente interruptor de alternancia en el lado izquierdo:

![interruptor](assets/toggleswitch.png)

[Carril de filtro](/help/communities/moderation.md#filterrail)
abre un carril, al seleccionar Buscar, que permite elegir las propiedades en las que filtrar el contenido.

![carril de filtro](assets/filterrail.png)

### Área de contenido {#content-area}

El área de contenido contiene información para el UGC publicado:

* UGC publicado
* Nombre de miembro
* Avatar del miembro
* Ubicación del puesto.
* Cuando se publicó.
* Número de respuestas a la publicación.
* [Opinión](/help/communities/moderate-ugc.md#sentiment) asociado con la publicación
* Si se aprueba, se muestra una marca de verificación.
* Si hay un archivo adjunto, se muestra un clip.

>[!NOTE]
> 
>El área de contenido incluye un *desplazamiento infinito*, lo que significa que le permitirá continuar desplazándose hasta que haya llegado al final del contenido. La barra de herramientas permanece en una posición fija y visible sobre el área de contenido, incluso mientras se desplaza.

### Carril de filtro {#ootbfilters}

![open-filterrail](assets/open-filterrail.png)

El icono del panel lateral abre el carril del filtro. El carril de filtro, que aparece a la izquierda del área de contenido, proporciona diferentes filtros, cada uno de los cuales tiene un efecto inmediato en el UGC al que se hace referencia que aparece en el área de contenido.

Los filtros dentro de cada categoría son **O**&#39;d juntos, y los filtros en diferentes categorías son **Y** Estaban juntos.

Por ejemplo, si marca ambas **Pregunta** y **Respuesta**, verá contenido que sea una de las siguientes opciones **Pregunta** *o* un **Respuesta**.

Sin embargo, si marca **Pregunta** y **Pendiente**, solo verá contenido que sea un **Pregunta** y es **Pendiente**.

>[!NOTE]
>
>Los moderadores de la comunidad pueden marcar los filtros predefinidos en la IU de la consola de moderación. Como estos filtros se anexan al final de la dirección URL (como parámetros de cadena de consulta), los moderadores pueden volver más tarde a los filtros marcados y también compartir estos vínculos.

![searchicon](assets/searchicon.png)

Cuando el carril del filtro está abierto, el icono Buscar conmuta el panel lateral para cerrarlo. Sin embargo, para cerrar el carril del filtro y ver solo el contenido generado por el usuario, haga clic en el icono Buscar y seleccione la opción Solo contenido.

#### Ruta de contenido {#content-path}

Ruta de contenido limita el UGC de referencia mostrado a las publicaciones colocadas en el repositorio de contenido especificado.

![content-path](assets/content-path.png)

#### Búsqueda de texto {#text-search}

La búsqueda de texto limita el CGU al que se hace referencia mostrado a las publicaciones en las que se incluye el texto introducido.

![búsqueda de texto](assets/text-search.png)

#### Sitio {#site}

El sitio limita el UGC al que se hace referencia mostrado a las publicaciones de sitios de la comunidad seleccionados. Si no se comprueba ningún sitio, se muestran todas las referencias a UGC.

![panel de sitio](assets/site-panel.png)

>[!NOTE]
>
>Cuando un administrador accede a la consola de moderación masiva, se muestran todas las referencias a UGC, incluidos los sitios no creados con [asistente de creación de sitios](/help/communities/sites-console.md), como los ejemplos de Geometrixx.
>
>Cuando un miembro de la comunidad de confianza accede a la consola de moderación en masa al publicarla, solo se muestran las referencias a UGC creadas para sitios de la comunidad que el miembro está autorizado a moderar, y pueden filtrarse con el filtro de sitio.

#### Tipo de contenido {#content-type}

Tipo de contenido limita el CGU al que se hace referencia que se muestra a las publicaciones del tipo de recurso seleccionado. Se pueden seleccionar uno o más de los siguientes tipos. Se muestran todos los tipos si no se selecciona ninguno.

* **Comentar**
* **Tema de foro**
* **Respuesta del foro**
* **Pregunta de P y R**
* **Respuesta de P y R**
* **Artículo de blog**
* **Comentario de blog**
* **Evento de calendario**
* **Comentario del calendario**
* **Carpeta de la biblioteca de archivos**
* **Documento de la biblioteca de archivos**
* **Idea**
* **Comentario de ideación**

![content-types](assets/content-types.png)

#### Tipos de contenido adicionales {#additional-content-types}

Para añadir recursos adicionales sobre los que filtrar:

* Inicie sesión en la instancia de autor como administrador.
* Abrir [Consola web](https://localhost:4502/system/console/configMgr).
* Localizar `AEM Communities Moderation Dashboard Filters`.
* Seleccione la configuración que desea abrir en el modo de edición.
* Introduzca el ResourceType de un componente por el que filtrar:

   * Por ejemplo, para filtrar los componentes de votación incluidos, introduzca:

     `Voting=social/tally/components/hbs/voting`

  ![additional-contenttype](assets/additional-contenttype.png)

* Seleccione Guardar.
* Actualice la consola Comunidades - Moderación.

El resultado es un nuevo filtro seleccionable para `Voting` en el `Content Type` grupo de filtros.

Cuando se selecciona ese filtro, el contenido del tablero muestra UGC que coincide con cualquiera de los ResourceTypes introducidos.

#### Estado {#status}

El estado limita el UGC al que se hace referencia que se muestra a las publicaciones del estado seleccionado, que puede ser uno o más de Pendiente, Aprobado, Denegado o Cerrado, así como Borrador o Programado para Artículos de Blog y Respondido o No Respondido para Preguntas de Control de Calidad. Si no se selecciona ninguno, se muestran todos.

>[!NOTE]
>
>Si solo se selecciona el estado Sin respuesta, el moderador verá todo el contenido (para todos los tipos de contenido) excepto las preguntas respondidas. Esto se debe a que la propiedad responsable de la Pregunta respondida no existe en el caso de preguntas no respondidas y otros contenidos como tema de foro, artículo de blog o comentarios.

![estados](assets/statuses.png)

#### Indicación {#flagging}

El marcado limita el UGC al que se hace referencia que se muestra a las publicaciones marcadas u ocultas.

Una vez que se marca un fragmento de contenido, permanece marcado hasta que se desmarca ese fragmento de contenido único seleccionando la opción **Indicador** botón una vez más. Tenga en cuenta que no hay niveles de indicación, como importante o de seguimiento.

![indicador](assets/flagging.png)

#### Miembros {#members}

Miembros limita el UGC al que se hace referencia que se muestra al UGC publicado por el nombre de miembro introducido.

![miembros](assets/members.png)

#### Enviado en el último {#posted-in-the-last}

Publicado en los últimos límites que el UGC al que se hace referencia muestra a las publicaciones realizadas en la última hora, día, semana, mes o año.

![posted-last](assets/posted-last.png)

#### Opinión {#sentiment}

[Opinión](/help/communities/moderate-ugc.md#sentiment) limita el UGC al que se hace referencia que se muestra a las publicaciones con un valor de opinión positivo, negativo o neutro.

![opinión](assets/sentiment.png)

## Filtros personalizados {#custom-filters}

Aparte de los filtros predeterminados de [Carril de filtro](/help/communities/moderation.md#ootbfilters)Sin embargo, se pueden agregar filtros personalizados adicionales en los metadatos a la IU de moderación. Los desarrolladores pueden utilizar el código de ejemplo de Github para ampliar los filtros de la IU de moderación existentes.

![custom-tag-filter](assets/custom-tag-filter.png)

El [proyecto de ejemplo](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter) en Github implementa el Filtro de etiquetas para filtrar la lista UGC en función de si las etiquetas específicas se aplican al contenido generado por el usuario. Puede seguir el código de ejemplo y crear filtros análogos para otros campos de metadatos UGC similares.

Para instalar el ejemplo para el filtro Etiquetas:

1. AEM Abra el administrador de paquetes en el Autor de la (`https://[aem-author]:4502/crx/packmgr/index.jsp`AEM ) instancia y publicación de la (`https://[aem-publish]:4503/crx/packmgr/index.jsp`) instancia.
1. Genere el paquete `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` desde el código de Github e instale y habilite la misma.
1. AEM Abra la consola Paquetes en el Autor de la ( `https://[aem-author]:4502/system/console/bundles`AEM ) instancia y publicación de la ( `https://[aem-publish]:4503/system/console/bundles`) instancia.
1. Cree el paquete (`[com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar`) de Github, e instale y habilite la misma.
1. Ir a **/apps/social/moderation/facets** AEM nodo en el autor de la (`https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets`AEM ) y Publicación de la (`https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facets`) instancia.
1. Añadir un usuario técnico **communities-utility-reader** con `jcr:read` permisos.

Para exponer los filtros personalizados en sitios de la comunidad existentes:

1. Editar `Clientlibs` de la página de moderación existente `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * Añadir nueva categoría `cq.social.hbs.moderation.v2.`

1. Vaya a `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * Establecer en componente nuevo `sling:resourceType = social/moderation/v2/filters.`

1. Vaya a `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`.

   * Establecer en componente nuevo `sling:resourceType = social/moderation/v2/modcontainer`.

## Acciones de moderación {#moderation-actions}

[Acciones de moderación](/help/communities/moderate-ugc.md#moderation-actions) se puede realizar en una o más selecciones realizadas en el área de contenido o al ver los detalles del contenido.

Para moderar las publicaciones de forma masiva, en el área de contenido haga clic en Seleccionar (![selecticono](assets/selecticon.png)) icono en una publicación, que aparece al pasar el ratón por encima (escritorio) o al pulsar y mantener un dedo en la publicación (móvil). Al hacerlo, entras al modo de selección múltiple y ahora puedes seleccionar las publicaciones subsiguientes que serán moderadas masivamente simplemente haciendo clic en ellas. Utilice los botones mostrados en la barra de herramientas para realizar acciones de moderación en las publicaciones seleccionadas. Todas las acciones solicitarán confirmación.

Para moderar una sola publicación en el área de contenido, pase el ratón sobre ella (escritorio) o mantenga presionado un dedo en la publicación (móvil) de modo que aparezcan botones en la publicación. Al trabajar con un solo detalle de contenido, solo una acción de eliminación solicitará confirmación.

### Moderar varias publicaciones {#moderating-multiple-posts}

Introduzca el modo de selección masiva haciendo clic en `Select` icono en una publicación:

![select-icon](assets/select-icon.png)

Para salir del modo de selección masiva, seleccione el icono Cancel (x) de la barra de herramientas:

Las acciones de moderación que se pueden realizar en varias publicaciones son las siguientes:

* Denegar
* Eliminar
* Cerrar/volver a abrir las publicaciones

Los iconos que permiten estas acciones solo aparecen en la barra de herramientas cuando se seleccionan varias publicaciones.

![bulkmoderado](assets/bulkmoderate.png)

### Moderar una sola publicación {#moderating-a-single-post}

En el modo de selección única, es posible:

* Vea los detalles del usuario seleccionando el nombre del usuario.
* Vea la publicación en contexto seleccionando el vínculo a la publicación.
* [respuesta](#reply)
* [Permitir](#allow)
* [Denegar](#deny)
* [Eliminar](#delete)
* [Cerrar](#close)
* Ver [Historial de moderación](#moderation-history)
* [Ver detalles](#viewdetails)

En la vista de la tarjeta, encima de los iconos de acción de moderación, está el texto de la publicación y, debajo, los datos que indican:

* Si tiene respuestas, y si es así, precedido por el número de respuestas.
* Si se ha marcado.
* Si se ha aprobado.
* Cuando se publicó el UGC.

![monomando](assets/singleselectmode.png)

#### respuesta {#reply}

![responder](assets/reply.png)

Al trabajar con una sola publicación, aparece un icono de respuesta si el tipo UGC admite respuestas y está configurado para permitirlas.

#### Permitir {#allow}

![permitir](assets/allow.png)

Al trabajar con una sola publicación, el icono Permitir aparecerá cuando la publicación se haya marcado o rechazado. Si se marca, al seleccionar Permitir se borran todas las marcas.

#### Denegar {#deny}

![denegar](assets/deny.png)

El **Denegar** la acción de moderación solo está disponible para contenido moderado y no aparece en contenido no moderado excepto en el modo de selección múltiple.

El contenido que no está moderado siempre se aprueba.

El contenido que se modera inicialmente entra en un estado Pendiente y luego se puede modificar para aprobarlo o denegarlo.

El contenido que deja el estado pendiente nunca puede volver a un estado pendiente. El contenido marcado como aprobado o denegado se puede cambiar a un estado diferente en cualquier momento.

#### Eliminar {#delete}

![eliminar](assets/delete.png)

En la selección única o en el modo por lotes, puede seleccionar elementos y eliminarlos. La acción de eliminación genera un cuadro de diálogo de confirmación. Una vez eliminados, estos elementos desaparecen inmediatamente del área de contenido. **Una vez eliminado, el UGC se elimina permanentemente del repositorio y no se puede recuperar posteriormente**.

#### Cerrar {#close}

![cerrar](assets/close.png)

Al trabajar con una sola publicación, aparecerá un icono Cerrar si el tipo UGC admite la capacidad de evitar nuevas publicaciones para ese recurso.

#### Historial de moderación {#moderation-history}

![moderación](assets/moderation.png)

Al trabajar con una sola publicación, aparecerá un icono de Historial de moderación al pasar el ratón por encima. Si se selecciona el icono, se mostrará un panel que contiene un historial de las acciones realizadas con respecto a la publicación de UGC.

Para volver a la visualización del área de contenido de varias publicaciones de UGC, seleccione la X en la esquina superior derecha del panel de detalles de vista.

Por ejemplo:

![moderation-history](assets/moderation-history.png)

#### Ver detalles {#view-detail}

![vista](assets/view.png)

Al trabajar con una sola publicación, se pueden ver más detalles abriendo el UGC en modo de detalle.

Para ello, pase el ratón sobre la publicación para mostrar el `View Detail` y selecciónelo para mostrar un panel que contenga más detalles de la publicación.

Para volver a la visualización del área de contenido de varias publicaciones de UGC, seleccione la X en la esquina superior derecha del panel de detalles de vista.

Por ejemplo:

![view1](assets/view1.png)
